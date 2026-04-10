# Fiche Module 17 : Conception d'un réseau de petite taille
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Module final ITN
Consolidation de tous les concepts : conception, configuration, dépannage de réseau complet

---

## 🏢 Petit réseau - Équipements typiques

| Équipement | Fonction | Exemples |
|------------|----------|----------|
| **Routeur ISR** | Routage, NAT, DHCP, firewall, VPN | Cisco ISR 1000, 4000 |
| **Switch(es)** | Commutation L2/L3, VLANs | Catalyst 2960, 3750 |
| **Point d'accès Wi-Fi** | Connectivité sans fil | AP, contrôleur WLC |
| **Serveur(s)** | Fichiers, email, apps | Physique ou cloud |
| **Périphériques finaux** | Utilisateurs | PC, smartphones, imprimantes, IoT |

### ISR (Integrated Services Router) - Tout-en-un

**Fonctions intégrées :**
- Routage vers Internet (passerelle par défaut)
- NAT/PAT (conservation IP)
- Pare-feu de base (ACL)
- Serveur DHCP ou relais DHCP
- VPN (accès distant sécurisé)
- Switch intégré (4-24 ports)
- Point d'accès Wi-Fi (optionnel)

---

## 📐 Hiérarchie réseau

### Modèle 3 couches (grands réseaux)

| Couche | Fonction | Caractéristiques |
|--------|----------|------------------|
| **Core** | Commutation haute vitesse | Redondance maximale, pas de manipulation paquets |
| **Distribution** | Routage inter-VLAN, agrégation | ACL, QoS, liens vers accès |
| **Accès** | Connexion périphériques | Port security, VLANs, PoE |

### Petit réseau = 2 couches

**Distribution + Accès** (pas de couche Core nécessaire)

---

## 🔧 Services réseau essentiels

| Service | Port | Protocole | Fonction |
|---------|------|-----------|----------|
| **HTTP** | 80 | TCP | Web non chiffré |
| **HTTPS** | 443 | TCP | Web chiffré |
| **DNS** | 53 | UDP/TCP | Résolution noms |
| **DHCP** | 67-68 | UDP | Attribution IP auto |
| **SMTP** | 25 | TCP | Envoi email |
| **POP3** | 110 | TCP | Réception email |
| **IMAP** | 143 | TCP | Réception email |
| **FTP** | 20-21 | TCP | Transfert fichiers |
| **SSH** | 22 | TCP | Accès distant sécurisé |
| **Telnet** | 23 | TCP | Accès distant (obsolète) |
| **NTP** | 123 | UDP | Synchronisation temps |
| **SNMP** | 161-162 | UDP | Gestion réseau |

---

## 🛠️ Commandes de vérification

### Windows

```cmd
ipconfig                    # Config IP basique
ipconfig /all              # Config détaillée
ipconfig /release          # Libérer IP DHCP
ipconfig /renew            # Renouveler IP DHCP
ipconfig /flushdns         # Vider cache DNS
ping <IP/hostname>         # Test connectivité
tracert <IP/hostname>      # Tracer route
arp -a                     # Table ARP
netstat -ano               # Connexions + ports
nslookup <hostname>        # Requête DNS
route print                # Table routage
```

### Linux

```bash
ip addr show               # Config IP
ip route show              # Table routage
ping <IP>                  # Test connectivité
traceroute <IP>            # Tracer route
dig <hostname>             # Requête DNS détaillée
ss -tuln                   # Sockets/ports
ip neigh show              # Table ARP/NDP
```

### Cisco IOS

```cisco
show ip interface brief    # Résumé interfaces
show interfaces            # Détails interfaces
show ip route              # Table routage
show vlan brief            # VLANs
show mac address-table     # Table MAC
show arp                   # Table ARP
show running-config        # Config active (RAM)
show startup-config        # Config sauvegardée (NVRAM)
show version               # Version IOS, uptime
ping <IP>                  # Test connectivité
traceroute <IP>            # Tracer route
```

---

## 🔍 Méthodologies de dépannage

### Approche structurée en 7 étapes

1. **Identifier le problème** : Collecter infos, reproduire, définir portée
2. **Établir une théorie** : Causes probables, commencer par le simple
3. **Tester la théorie** : Confirmer ou infirmer
4. **Établir un plan** : Étapes de résolution, impact
5. **Implémenter** : Appliquer changements, documenter
6. **Vérifier** : Tester fonctionnalité, confirmer avec user
7. **Documenter** : Problème, cause, solution → base de connaissances

### Modèle OSI pour dépannage

**Bottom-Up (bas → haut) - Approche courante**

| Couche | Vérifications | Commandes |
|--------|---------------|-----------|
| **1 - Physique** | Câbles, voyants, connecteurs | `show interfaces` |
| **2 - Liaison** | VLANs, trunking, MAC | `show vlan`, `show mac address-table` |
| **3 - Réseau** | IP, masque, gateway, routage | `show ip interface brief`, `show ip route` |
| **4 - Transport** | Ports, services, pare-feu | `netstat`, `ss` |
| **5-7 - Supérieures** | Applications, DNS, services | Tests applicatifs |

**Top-Down (haut → bas)**
- Commencer par application
- Descendre vers physique
- Utile pour problèmes applicatifs spécifiques

**Divide and Conquer (diviser pour régner)**
- Commencer couche médiane (3 ou 4)
- Si OK → problème couches supérieures
- Si KO → problème couches inférieures
- **Approche la plus efficace**

---

## 🚨 Scénarios de dépannage courants

### Scénario 1 : Pas d'Internet

**Symptômes :** Ping gateway OK, ping 8.8.8.8 ÉCHEC

**Causes possibles :**
- Route par défaut manquante (PC ou routeur)
- Interface WAN down
- NAT mal configuré
- Problème FAI

**Dépannage :**
```cisco
ipconfig                      # Vérifier gateway sur PC
Router# show ip route         # Vérifier route 0.0.0.0/0
Router# show ip interface brief  # Vérifier interface WAN UP
Router# ping 8.8.8.8          # Test depuis routeur
```

### Scénario 2 : DNS ne fonctionne pas

**Symptômes :** Ping 8.8.8.8 OK, ping google.com ÉCHEC

**Causes possibles :**
- Pas de serveur DNS configuré
- Serveur DNS incorrect ou inaccessible
- Pare-feu bloque port 53 UDP

**Dépannage :**
```cmd
ipconfig /all                 # Vérifier DNS configuré
ipconfig /flushdns           # Vider cache
nslookup google.com          # Test résolution
nslookup google.com 8.8.8.8  # Test DNS spécifique
```

### Scénario 3 : Un hôte sans accès

**Symptômes :** PC1 OK, PC2 KO (même VLAN)

**Causes possibles :**
- Câble défectueux ou déconnecté
- Port shutdown
- VLAN incorrect
- Duplex mismatch
- Configuration IP incorrecte

**Dépannage :**
```cisco
Switch# show interfaces <port>      # Vérifier status, erreurs
Switch# show vlan brief              # Vérifier VLAN
Switch# show mac address-table       # Vérifier apprentissage MAC

PC: ipconfig /all                    # Vérifier config IP
PC: ipconfig /release                # Test DHCP
PC: ipconfig /renew
```

### Scénario 4 : Connectivité intermittente

**Symptômes :** Coupures aléatoires, pertes de paquets

**Causes possibles :**
- Duplex mismatch
- Câble défectueux
- Câble trop long (> 100m UTP)
- Boucle réseau
- Surcharge

**Dépannage :**
```cisco
show interfaces <port> | include duplex  # Vérifier duplex
show interfaces <port>                    # Erreurs, collisions, CRC
show processes cpu                        # Charge CPU
show memory                               # Utilisation mémoire
```

---

## 💡 À retenir absolument

✅ **Hiérarchie réseau**
- Grand réseau : Core + Distribution + Accès (3 couches)
- Petit réseau : Distribution + Accès (2 couches)

✅ **ISR = Router multifonction**
Routage + NAT + DHCP + Firewall + VPN + Switch intégré

✅ **Méthodologie dépannage : 7 étapes**
Identifier → Théorie → Tester → Plan → Implémenter → Vérifier → Documenter

✅ **Approches dépannage OSI**
- **Bottom-Up** : Couche 1 → 7 (approche courante)
- **Top-Down** : Couche 7 → 1 (problèmes applicatifs)
- **Divide and Conquer** : Commencer milieu (LA PLUS EFFICACE)

✅ **Ping = Couche 3**
Test connectivité IP (ICMP)

✅ **Traceroute/tracert = Traçage chemin**
Identifie où le trafic s'arrête

✅ **ipconfig /all = Best friend Windows**
Config IP complète (adresse, masque, gateway, DNS, DHCP)

✅ **show ip interface brief = Best friend Cisco**
Vue rapide de toutes les interfaces et leurs états

✅ **DNS = Port 53 UDP**
Résolution noms de domaine → IP

✅ **DHCP = Ports 67-68 UDP**
Server : 67, Client : 68

✅ **Duplex mismatch = Cause fréquente**
Connectivité intermittente, collisions, lenteur

✅ **Un changement à la fois lors du dépannage**
Tester l'impact, pouvoir revenir en arrière

---

## 📝 Checklist de conception petit réseau

### Infrastructure
- [ ] ISR avec capacité NAT, DHCP, firewall
- [ ] Switch(es) avec ports suffisants + croissance
- [ ] Point(s) d'accès Wi-Fi WPA3
- [ ] Câblage structuré (Cat 6 minimum)
- [ ] Redondance sur liens critiques

### Adressage
- [ ] Plan d'adressage IP documenté
- [ ] Utilisation VLSM pour optimisation
- [ ] DHCP pour clients, statique pour serveurs/équipements
- [ ] Passerelles par défaut configurées

### Services
- [ ] DHCP avec pools/exclusions/options
- [ ] DNS (interne + forwarders)
- [ ] NAT/PAT sur routeur bordure
- [ ] NTP pour synchronisation

### Sécurité
- [ ] SSH (pas Telnet)
- [ ] Mots de passe forts
- [ ] ACL sur interfaces externes
- [ ] Port security sur accès
- [ ] VLANs pour segmentation
- [ ] Firewall sur périphérie

### Documentation
- [ ] Diagrammes physique et logique
- [ ] Plan d'adressage détaillé
- [ ] Configurations sauvegardées
- [ ] Procédures de dépannage
- [ ] Contacts support/FAI

---

## 🔑 Commandes essentielles par situation

**Vérifier connectivité réseau :**
```
ping <IP>                       # Base
traceroute <IP>                 # Chemin
show ip route                   # Routage
show ip interface brief         # Interfaces
```

**Problème DHCP :**
```
ipconfig /release               # Libérer (Windows)
ipconfig /renew                 # Renouveler (Windows)
show ip dhcp binding            # IOS : Leases DHCP
show ip dhcp pool               # IOS : Pools DHCP
```

**Problème DNS :**
```
ipconfig /flushdns              # Vider cache (Windows)
nslookup <domain>               # Test résolution
dig <domain>                    # Test résolution (Linux)
```

**Problème VLAN/Switch :**
```
show vlan brief                 # Liste VLANs
show interfaces trunk           # Trunks
show mac address-table          # Table MAC
```

---

**Félicitations ! Vous maîtrisez la conception et le dépannage de réseaux de petite taille !**
