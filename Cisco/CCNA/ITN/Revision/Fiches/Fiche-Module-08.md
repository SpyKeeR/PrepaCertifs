# 📝 Fiche de Révision - Module 8 : Couche Réseau

## 🎯 Concepts clés

### Rôle de la couche réseau (Layer 3)
- **Encapsulation** des segments en paquets
- **Routage** des paquets vers leur destination
- **Interconnexion** de différents réseaux (LAN, WAN, Internet)
- Protocole **sans connexion** (connectionless) et **non fiable** (best-effort delivery)
- Indépendance du média (cuivre, fibre, sans fil)

### Protocoles principaux
- **IPv4** : 32 bits (~4,3 milliards d'adresses)
- **IPv6** : 128 bits (340 sextillions d'adresses)
- **ICMP/ICMPv6** : diagnostic et messages d'erreur
- **Protocoles de routage** : OSPF, EIGRP, BGP, RIP

### Limitations IPv4 et solutions
- **Problème** : épuisement des adresses
- **Solutions temporaires** : NAT, CIDR, adresses privées (RFC 1918)
- **Solution définitive** : migration vers IPv6

---

## 📋 Tableaux récapitulatifs

### Champs importants de l'entête IPv4 (20-60 octets)

| Champ | Taille | Description | Valeurs importantes |
|-------|--------|-------------|---------------------|
| **Version** | 4 bits | Version IP | `0100` (IPv4) |
| **IHL** | 4 bits | Longueur entête en mots de 32 bits | Min: 5 (20 octets), Max: 15 (60 octets) |
| **ToS/DSCP** | 8 bits | Priorité QoS | Utilisé pour VoIP, vidéo |
| **Total Length** | 16 bits | Taille paquet (entête + données) | Max: 65 535 octets |
| **TTL** ⚠️ | 8 bits | Nombre max de sauts | Décrémenté à chaque routeur |
| **Protocol** ⚠️ | 8 bits | Protocole Layer 4 | 1=ICMP, 6=TCP, 17=UDP, 89=OSPF |
| **Source IP** | 32 bits | Adresse IPv4 source | 4 octets |
| **Destination IP** | 32 bits | Adresse IPv4 destination | 4 octets |

**Points critiques** :
- **TTL** : Si TTL=0 → paquet détruit + message ICMP Time Exceeded
- **Protocol** : identifie TCP, UDP, ICMP, OSPF, EIGRP
- **Header Checksum** : recalculé à chaque routeur (car TTL change)

### Champs importants de l'entête IPv6 (40 octets fixes)

| Champ | Taille | Description | Équivalent IPv4 |
|-------|--------|-------------|----------------|
| **Version** | 4 bits | Version IP | `0110` (IPv6) |
| **Traffic Class** ⚠️ | 8 bits | Priorité QoS | ToS/DSCP |
| **Flow Label** | 20 bits | Identifie un flux | - |
| **Payload Length** | 16 bits | Taille données (sans l'entête) | Total Length |
| **Next Header** ⚠️ | 8 bits | Type du prochain entête | Protocol |
| **Hop Limit** ⚠️ | 8 bits | Nombre max de sauts | TTL |
| **Source Address** | 128 bits | Adresse IPv6 source | 16 octets |
| **Destination Address** | 128 bits | Adresse IPv6 destination | 16 octets |

**Valeurs Next Header** :
- 6 = TCP
- 17 = UDP
- 58 = ICMPv6
- 43 = Routing Header
- 44 = Fragment Header

**Améliorations vs IPv4** :
- ✅ Entête **fixe 40 octets** (traitement plus rapide)
- ✅ **Pas de checksum** (gain de performances)
- ✅ **Pas de fragmentation** par les routeurs (seulement par l'hôte source)
- ✅ IPsec intégré nativement

---

### Codes des routes dans la table de routage

| Code | Source | Description | Distance Administrative |
|------|--------|-------------|------------------------|
| **C** | Connected | Réseau directement connecté | 0 |
| **L** | Local | Adresse IP locale de l'interface | 0 |
| **S** | Static | Route statique | 1 |
| **D** | EIGRP | Route EIGRP (interne) | 90 |
| **O** | OSPF | Route OSPF | 110 |
| **R** | RIP | Route RIP | 120 |
| **B** | BGP | Route BGP externe | 20 (eBGP) |

### Distance administrative (AD)

**Règle** : Plus la valeur est **faible**, plus la route est **fiable**.

| Source | AD |
|--------|-----|
| Interface connectée | 0 |
| Route statique | 1 |
| eBGP | 20 |
| EIGRP (interne) | 90 |
| OSPF | 110 |
| RIP | 120 |
| EIGRP (externe) | 170 |
| iBGP | 200 |

---

### Processus de routage

**Réception → Traitement → Transmission**

1. **Réception** (De-encapsulation Layer 2)
   - Vérifier FCS de la trame
   - Extraire le paquet IP

2. **Traitement** (Layer 3)
   - Lire l'adresse IP de destination
   - **Décrémenter TTL/Hop Limit** (-1)
   - Si TTL=0 → détruire paquet + ICMP Time Exceeded
   - Consulter table de routage
   - Déterminer interface de sortie et next-hop

3. **Transmission** (Re-encapsulation Layer 2)
   - **MAC source** : interface de sortie du routeur
   - **MAC destination** : next-hop (routeur suivant ou hôte final)
   - **Adresses IP restent identiques** de bout en bout

---

### Sélection de la meilleure route

**Ordre de décision** :
1. **Longest prefix match** (route la plus spécifique)
   - /28 préférée à /24 pour même destination
2. **Distance administrative** (si même préfixe)
3. **Métrique** (si même AD)

---

## ⚡ Commandes IOS essentielles

### Affichage de la table de routage
```
Router# show ip route                    # Table IPv4
Router# show ipv6 route                  # Table IPv6
Router# show ip route connected          # Routes connectées
Router# show ip route static             # Routes statiques
Router# show ip route ospf               # Routes OSPF
Router# show ip route 10.1.1.0           # Route spécifique
```

### Configuration de routes statiques
```
# IPv4 (route normale)
Router(config)# ip route 192.168.3.0 255.255.255.0 10.1.1.2

# IPv4 (route par défaut)
Router(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1

# IPv6 (route normale)
Router(config)# ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2

# IPv6 (route par défaut)
Router(config)# ipv6 route ::/0 2001:db8:acad:2::1
```

### Vérification de la connectivité
```
Router# ping 192.168.1.10
Router# ping ipv6 2001:db8:acad:1::10
Router# traceroute 8.8.8.8
Router# traceroute ipv6 2001:4860:4860::8888
```

---

## 💡 Points importants pour l'examen

### ⚠️ À retenir absolument

1. **TTL/Hop Limit** :
   - Décrémenté de **1** à chaque routeur
   - Si = 0 → paquet détruit + ICMP Time Exceeded
   - Empêche les boucles de routage infinies
   - Valeur initiale typique : 64 ou 128

2. **Champ Protocol (IPv4) / Next Header (IPv6)** :
   - Identifie le protocole de couche supérieure
   - 1=ICMP, 6=TCP, 17=UDP, 58=ICMPv6, 89=OSPF

3. **Adresses MAC changent à chaque saut, IP restent identiques**
   - Layer 2 : adresses MAC modifiées par chaque routeur
   - Layer 3 : adresses IP source/destination invariables

4. **IPv6 : entête fixe de 40 octets** (vs 20-60 pour IPv4)
   - Plus rapide à traiter
   - Pas de checksum
   - Extensions pour fonctionnalités supplémentaires

5. **Distance Administrative** :
   - Connected = 0 (plus fiable)
   - Static = 1
   - EIGRP = 90
   - OSPF = 110
   - RIP = 120

6. **MTU (Maximum Transmission Unit)** :
   - Ethernet : 1500 octets
   - IPv4 : fragmentation possible par les routeurs
   - IPv6 : fragmentation uniquement par l'hôte source

7. **Route par défaut** :
   - IPv4 : `0.0.0.0/0`
   - IPv6 : `::/0`
   - Utilisée quand aucune route spécifique ne correspond

8. **Sélection de route** :
   - **1.** Longest prefix match
   - **2.** Distance administrative
   - **3.** Métrique

### Différences clés IPv4 vs IPv6

| Caractéristique | IPv4 | IPv6 |
|----------------|------|------|
| Taille adresse | 32 bits | 128 bits |
| Notation | Décimale pointée | Hexadécimale |
| Entête | 20-60 octets (variable) | 40 octets (fixe) |
| Checksum entête | Oui | Non |
| Fragmentation | Par routeurs | Uniquement par source |
| Broadcast | Oui (FF:FF:FF:FF:FF:FF) | Non (remplacé par multicast) |
| TTL | TTL | Hop Limit |
| Protocol | Protocol | Next Header |

---

**🎓 Conseils pour l'examen** :
- Savoir identifier les champs d'entête IPv4 et IPv6
- Comprendre le rôle du TTL/Hop Limit
- Reconnaître les codes de routes (C, L, S, D, O, R)
- Maîtriser la distance administrative
- Comprendre que les adresses MAC changent, pas les IP
