# Fiche de révision - Module 1 : Packet Forwarding
**CCNP ENCOR v8 - Acheminement des paquets**

---

## 🎯 Concepts essentiels

### Couche 2 vs Couche 3

| Aspect | Couche 2 (Liaison) | Couche 3 (Réseau) |
|--------|-------------------|-------------------|
| **Adressage** | MAC (48 bits) | IP (32/128 bits) |
| **Portée** | Segment local | Inter-réseaux |
| **Périphérique** | Switch | Routeur |
| **Protocole clé** | Ethernet, 802.1Q | IP, ICMP |
| **Domaine** | Collision, Broadcast | Routage |

---

## 🔄 Acheminement L2 (Switches)

###  Adresses MAC
```
Format: XX:XX:XX:XX:XX:XX (hexadécimal)
├─ 24 bits OUI (fabricant)
└─ 24 bits Device ID (unique)

Types:
- Unicast: Un seul périphérique
- Multicast: Groupe de périphériques
- Broadcast: FF:FF:FF:FF:FF:FF (tous)
```

### Domaines de collision

**Hub :** 1 domaine de collision partagé (obsolète)  
**Switch :** 1 domaine par port (standard)

**CSMA/CD :** Mécanisme pour éviter les collisions (half-duplex legacy)

### Table MAC (CAM)

**Apprentissage :**
```
Trame reçue → Examine MAC source → Enregistre (MAC, Port, VLAN)
```

**Commandes clés :**
```cisco
show mac address-table                    ! Afficher table complète
show mac address-table vlan 10            ! Filtrer par VLAN
show mac address-table interface Gi0/1    ! Filtrer par interface
clear mac address-table dynamic           ! Effacer table dynamique
mac address-table aging-time 600          ! Modifier délai expiration
```

**CAM :** Mémoire ultra-rapide, recherche parallèle en 1 cycle d'horloge

---

## 🏢 VLANs (Virtual LANs)

### Concept

**Avantages :**
- ✅ Segmentation logique des broadcasts
- ✅ Sécurité accrue (isolation trafic)
- ✅ Flexibilité (pas besoin de recâblage)
- ✅ Meilleure utilisation des ports

### Standard 802.1Q

**Tag VLAN :** 32 bits ajoutés à la trame
- **TPID** (16 bits) : 0x8100
- **PCP** (3 bits) : Priorité QoS (0-7)
- **DEI** (1 bit) : Drop Eligible Indicator
- **VLAN ID** (12 bits) : 1-4094

**Plages :**
- Standard : 1-1005
- Extended : 1006-4094
- VLAN 1 : Natif par défaut (ne PAS utiliser)

### Configuration

```cisco
! Créer un VLAN
vlan 10
 name SALES
exit

! Port d'accès
interface Gi0/4
 switchport mode access
 switchport access vlan 10
 description PC-Sales
exit

! Port trunk
interface Gi0/1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,99
exit
```

### Vérification

```cisco
show vlan brief                    ! VLANs et ports assignés
show vlan id 10                    ! Détails VLAN 10
show interfaces trunk              ! Informations trunks
show interfaces Gi0/1 switchport   ! Détails switchport
show interfaces status             ! Vue condensée tous ports
```

---

## 🌉 Trunks 802.1Q

### Caractéristiques

**Fonction :** Transporter **plusieurs VLANs** sur un seul lien

**VLAN natif :**
- Trafic **non-tagué** (sans 802.1Q)
- Par défaut : VLAN 1
- ⚠️ Doit correspondre des 2 côtés
- 🔒 Best practice : VLAN dédié non-utilisé (ex: 999)

### VLANs autorisés

```cisco
switchport trunk allowed vlan 10,20,30        ! Liste spécifique
switchport trunk allowed vlan add 40          ! Ajouter
switchport trunk allowed vlan remove 1        ! Retirer
switchport trunk allowed vlan all             ! Tous
switchport trunk allowed vlan none            ! Aucun
switchport trunk allowed vlan except 1-10     ! Tous sauf 1-10
```

**Sortie `show interfaces trunk` :**
1. **Section 1** : Mode, encapsulation, statut, VLAN natif
2. **Section 2** : VLANs autorisés sur trunk
3. **Section 3** : VLANs autorisés ET actifs
4. **Section 4** : VLANs forwarding (non-bloqués par STP)

---

## 🌐 Acheminement L3 (Routeurs)

### Acheminement local (même sous-réseau)

**Processus :**
```
PC1 (192.168.10.5) → PC2 (192.168.10.6)
1. Détection: même réseau
2. Consulte table ARP pour IP destination
3. Si absent: Envoie ARP Request (broadcast)
4. Reçoit ARP Reply avec MAC
5. Encapsule trame avec MAC destination
```

### Protocole ARP

**Fonction :** Mapper IP (L3) → MAC (L2)

**Messages :**
- **ARP Request** : Broadcast "Qui a 192.168.10.6?"
- **ARP Reply** : Unicast "C'est moi, ma MAC = XX:XX:XX:XX:XX:XX"

**Commandes :**
```cisco
show ip arp                        ! Table ARP complète
show ip arp 192.168.10.5           ! Entrée spécifique
show ip arp vlan 10                ! Filtrer par VLAN
clear ip arp                       ! Effacer table ARP
```

### Routage inter-réseau

**Processus :**
```
PC1 (192.168.10.5) → Serveur (192.168.20.10)
1. Détection: réseau différent
2. Consulte table de routage locale → Gateway 192.168.10.1
3. ARP pour gateway (si nécessaire)
4. Encapsule avec:
   - IP src: 192.168.10.5 (inchangée)
   - IP dst: 192.168.20.10 (inchangée)
   - MAC src: MAC de PC1
   - MAC dst: MAC du routeur
```

**Sur le routeur :**
```
1. Reçoit trame (MAC dst = interface routeur)
2. Décapsule couche 2
3. Examine IP dst (192.168.20.10)
4. Consulte table de routage
5. Décrémente TTL (si 0: drop + ICMP Time Exceeded)
6. Résolution ARP pour next-hop
7. Réencapsule avec nouvelles MACs L2
8. Transfère sur interface de sortie
```

**💡 Point clé :** Les IP restent constantes, les MACs changent à chaque saut

---

## 🎯 Configuration IP

### Interfaces routeur

```cisco
! IPv4 sur interface
interface Gi0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

! IPv4 secondaire
interface Gi0/0
 ip address 192.168.10.1 255.255.255.0
 ip address 192.168.11.1 255.255.255.0 secondary
exit

! IPv6 sur interface
ipv6 unicast-routing                    ! Activer routage IPv6
interface Gi0/0
 ipv6 address 2001:DB8:ACAD:10::1/64
 no shutdown
exit
```

**Résultat :** Route **Connected** injectée dans table de routage (AD = 0)

---

## 🔀 Routage inter-VLAN

### Méthode 1 : Router-on-a-Stick (Sous-interfaces)

```cisco
! Switch: trunk vers routeur
interface Gi0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
exit

! Routeur: sous-interfaces
interface Gi0/0
 no shutdown
exit

interface Gi0/0.10
 encapsulation dot1q 10
 ip address 192.168.10.1 255.255.255.0
exit

interface Gi0/0.20
 encapsulation dot1q 20
 ip address 192.168.20.1 255.255.255.0
exit
```

**Syntaxe :** `interface.subinterface-number`  
**Best practice :** Numéro sous-interface = numéro VLAN

### Méthode 2 : SVIs (Switch multicouche)

```cisco
! Créer VLANs
vlan 10
 name SALES
vlan 20
 name ENGINEERING
exit

! Interfaces VLAN (SVIs)
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

! Activer routage IP
ip routing
```

**Conditions pour SVI up/up :**
1. VLAN existe dans base VLAN
2. Au moins 1 port assigné au VLAN en `up/up`
3. SVI configurée avec `no shutdown`

**Avantage :** Routage **hardware-based** (CEF), bien plus rapide que router-on-a-stick

---

## 🚀 Architectures d'acheminement

### Évolution

| Méthode | Traitement | Performance | CPU | Statut |
|---------|------------|-------------|-----|--------|
| **Process Switching** | CPU par paquet | Très lente | Très élevé | Obsolète |
| **Fast Switching** | Cache décisions | Moyenne | Moyen | Legacy |
| **CEF** | Tables pré-calculées | Très rapide | Très faible | **Standard** |

### CEF (Cisco Express Forwarding)

**Composants :**

1. **FIB (Forwarding Information Base)**
   - Copie optimisée de la RIB (table de routage)
   - Contient next-hops et interfaces de sortie
   - Mise à jour temps réel

2. **Adjacency Table**
   - Informations couche 2 (MACs)
   - Associe next-hops IP → MACs
   - Permet réécriture rapide en-têtes Ethernet

**Fonctionnement :**
```
Paquet → ASIC consulte FIB → ASIC consulte Adjacency Table
      → Réécriture en-têtes L2 → Transfert
      (SANS solliciter le CPU)
```

**Avantages :**
- ✅ Wire-speed (performances maximales)
- ✅ CPU libéré pour tâches de contrôle
- ✅ Latence déterministe et constante
- ✅ Scalabilité élevée

**Commandes :**
```cisco
show ip cef              ! Afficher FIB
show cef state           ! Vérifier activation CEF
show adjacency           ! Afficher adjacency table
```

**💡 Point clé :** CEF activé par défaut sur équipements modernes

---

## 📊 Tableau récapitulatif des commandes

### VLANs et Switches

| Commande | Usage |
|----------|-------|
| `vlan 10` | Créer VLAN 10 |
| `show vlan brief` | Afficher VLANs et ports |
| `switchport mode access` | Configurer port en mode access |
| `switchport access vlan 10` | Assigner port au VLAN 10 |
| `switchport mode trunk` | Configurer port en mode trunk |
| `switchport trunk native vlan 99` | Définir VLAN natif |
| `switchport trunk allowed vlan 10,20` | Limiter VLANs sur trunk |
| `show interfaces trunk` | Afficher informations trunks |
| `show interfaces status` | Vue condensée statut ports |

### Tables MAC et ARP

| Commande | Usage |
|----------|-------|
| `show mac address-table` | Afficher table MAC |
| `show mac address-table vlan 10` | Filtrer par VLAN |
| `clear mac address-table dynamic` | Effacer table MAC |
| `show ip arp` | Afficher table ARP |
| `show ip arp vlan 10` | Filtrer table ARP par VLAN |
| `clear ip arp` | Effacer table ARP |

### Routage

| Commande | Usage |
|----------|-------|
| `ip address 192.168.1.1 255.255.255.0` | Configurer IP interface |
| `ip address ... secondary` | Ajouter IP secondaire |
| `ipv6 address 2001:DB8::1/64` | Configurer IPv6 |
| `ipv6 unicast-routing` | Activer routage IPv6 |
| `encapsulation dot1q 10` | Associer sous-interface à VLAN |
| `interface vlan 10` | Créer SVI |
| `ip routing` | Activer routage sur switch L3 |
| `show ip interface brief` | Afficher interfaces IP |
| `show ip route` | Afficher table routage |
| `show ip cef` | Afficher FIB (CEF) |

---

## 🎓 Points clés à retenir

### Couche 2
1. Switch crée 1 domaine collision/port, hub = 1 domaine partagé
2. Table MAC associe : MAC → Port → VLAN
3. CAM = mémoire ultra-rapide pour lookups MAC
4. VLANs segmentent logiquement en domaines broadcast
5. Trunk 802.1Q transporte plusieurs VLANs, VLAN natif non-tagué
6. VLAN natif doit correspondre des 2 côtés du trunk

### Couche 3
7. ARP mappe IP → MAC pour forwarding local
8. Routage : IPs constantes, MACs changent à chaque saut
9. TTL décrémenté à chaque saut (empêche boucles)
10. Sous-interfaces = Router-on-a-stick (1 interface physique, plusieurs VLANs)
11. SVIs = routage inter-VLAN sur switch L3 (hardware-based)

### Architectures
12. CEF (FIB + Adjacency) = standard actuel, hardware-based
13. CEF : wire-speed, CPU libéré, latence déterministe

---

## 🔗 Liens avec autres modules

- **Module 2-4** : STP utilise VLANs et trunks pour la redondance L2
- **Module 5** : EtherChannel agrège plusieurs liens et supporte trunks
- **Module 6-7** : Routage dynamique (EIGRP) s'appuie sur interfaces IP
- **Module 8-10** : OSPF utilise interfaces et sous-réseaux
- **Module 15** : Services IP (DHCP, NAT) dépendent de SVIs

---

**Fiche suivante :** [Module 2 - Spanning Tree Protocol](Fiche-Module-02.md)
