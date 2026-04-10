# Module 8 - Couche Réseau (Network Layer)

## Table des matières
1. [Introduction à la couche réseau](#introduction)
2. [Caractéristiques de la couche réseau](#caractéristiques)
3. [Protocole IPv4](#ipv4)
4. [Entête du paquet IPv4](#entête-ipv4)
5. [Protocole IPv6](#ipv6)
6. [Entête du paquet IPv6](#entête-ipv6)
7. [Routage des paquets](#routage)
8. [Table de routage](#table-routage)
9. [Commandes IOS utiles](#commandes)

---

## 1. Introduction à la couche réseau {#introduction}

### Rôle de la couche 3
La **couche réseau (Layer 3)** a pour responsabilité principale de :
- **Fournir des services** permettant aux périphériques d'**échanger des données** sur un réseau
- **Encapsuler les segments** de la couche Transport en **paquets**
- **Router les paquets** vers leur destination finale
- **Interconnecter différents réseaux** (LAN, WAN, Internet)

### Protocoles de la couche réseau
- **IPv4** (Internet Protocol version 4) : protocole le plus utilisé
- **IPv6** (Internet Protocol version 6) : nouvelle génération
- **ICMP** (Internet Control Message Protocol) : messages de diagnostic (ping, traceroute)
- **Protocoles de routage** : OSPF, EIGRP, BGP, RIP

### Avantages d'un protocole sans connexion
IP est un protocole **sans connexion (connectionless)** :
- ✅ Pas d'établissement de session préalable
- ✅ Overhead réduit (moins de ressources consommées)
- ✅ Meilleure évolutivité (scalabilité)
- ⚠️ Non fiable : pas de garantie de livraison (déléguée à TCP niveau 4)

---

## 2. Caractéristiques de la couche réseau {#caractéristiques}

### Encapsulation
- La couche réseau **reçoit un segment** (Layer 4) contenant les données et l'entête de protocole
- Elle **ajoute un entête IP** créant ainsi un **paquet**
- Le paquet est ensuite transmis à la couche Liaison de données (Layer 2)

### Best-Effort Delivery (Livraison au mieux)
- IP = protocole **non fiable**
- Pas de mécanisme de **confirmation de réception**
- Pas de **retransmission automatique** en cas de perte
- Pas de **contrôle de flux**
- ⚠️ La fiabilité est assurée par les **protocoles de couche supérieure** (TCP)

### Indépendance du média
- IP fonctionne **indépendamment du support** (cuivre, fibre, sans fil)
- La couche liaison de données (Layer 2) gère l'accès au média
- IP n'a pas besoin de connaître le type de média utilisé
- **MTU (Maximum Transmission Unit)** : taille maximale d'une trame que le média peut transporter
  - Ethernet : MTU = 1500 octets
  - Si paquet > MTU → **fragmentation** (IPv4) ou **message d'erreur** (IPv6)

---

## 3. Protocole IPv4 {#ipv4}

### Limitations d'IPv4
- **Épuisement des adresses** : ~4,3 milliards d'adresses disponibles
- **Problèmes de tables de routage** : croissance exponentielle
- **Manque de connectivité de bout en bout** : à cause du NAT

### Solutions temporaires
- **NAT (Network Address Translation)** : partager des adresses publiques
- **CIDR (Classless Inter-Domain Routing)** : allocation plus efficace
- **Adresses privées** : RFC 1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16)

### Transition vers IPv6
IPv6 est la solution à long terme pour résoudre les limitations d'IPv4.

---

## 4. Entête du paquet IPv4 {#entête-ipv4}

### Structure de l'entête IPv4

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |Type of Service|          Total Length         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|      Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |    Protocol   |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source IP Address                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination IP Address                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### Champs importants de l'entête IPv4

#### Version (4 bits)
- Valeur : **0100** (4 en binaire)
- Identifie la version du protocole IP (IPv4)

#### IHL - Internet Header Length (4 bits)
- Taille de l'entête en **mots de 32 bits** (4 octets)
- Valeur minimale : **5** (5 × 4 = 20 octets)
- Valeur maximale : **15** (15 × 4 = 60 octets)
- Permet de gérer les options variables

#### Type of Service - ToS / DSCP (8 bits)
- Appelé aussi **Differentiated Services (DS)**
- Permet de **prioriser certains paquets** (QoS)
- Utilisé pour la **VoIP, vidéo, données critiques**

#### Total Length (16 bits)
- Taille **totale du paquet** (entête + données)
- Taille en **octets**
- Valeur maximale : **65 535 octets**

#### Identification (16 bits)
- Identifie **de manière unique** le paquet original
- Utilisé pour **réassembler les fragments**
- Tous les fragments d'un même paquet ont la même valeur

#### Flags (3 bits)
- **Bit 0 (Réservé)** : toujours à 0
- **Bit 1 (Don't Fragment - DF)** : si 1 → ne pas fragmenter le paquet
- **Bit 2 (More Fragments - MF)** : si 1 → d'autres fragments suivent

#### Fragment Offset (13 bits)
- Indique la **position du fragment** dans le paquet original
- Exprimé en blocs de **8 octets**
- Permet de réassembler les fragments dans le bon ordre

#### Time to Live - TTL (8 bits) ⚠️ **CHAMP IMPORTANT**
- Nombre maximal de **sauts (hops)** que le paquet peut effectuer
- **Décrémenté de 1** à chaque passage par un routeur
- Si TTL = 0 → paquet **détruit** et message **ICMP Time Exceeded** envoyé
- Empêche les **boucles de routage infinies**
- Valeur initiale typique : **64** ou **128**

#### Protocol (8 bits) ⚠️ **CHAMP IMPORTANT**
- Identifie le **protocole de couche supérieure** (Layer 4)
- Valeurs courantes :
  - **1** = ICMP
  - **6** = TCP
  - **17** = UDP
  - **89** = OSPF
  - **88** = EIGRP

#### Header Checksum (16 bits)
- Détection d'**erreurs dans l'entête** uniquement (pas les données)
- Recalculé à chaque routeur (car TTL change)

#### Source IP Address (32 bits)
- Adresse IPv4 de **l'émetteur** du paquet (32 bits = 4 octets)

#### Destination IP Address (32 bits)
- Adresse IPv4 du **destinataire** du paquet (32 bits = 4 octets)

#### Options (variable) et Padding
- Champ **optionnel** rarement utilisé
- Padding = remplissage pour aligner l'entête sur 32 bits

---

## 5. Protocole IPv6 {#ipv6}

### Améliorations d'IPv6

#### Espace d'adressage étendu
- **128 bits** (vs 32 bits pour IPv4)
- **340 sextillions** d'adresses (3,4 × 10³⁸)
- Notation **hexadécimale** : 2001:0db8:85a3:0000:0000:8a2e:0370:7334

#### Simplification de l'entête
- Entête **fixe de 40 octets** (vs 20-60 pour IPv4)
- Moins de champs → **traitement plus rapide** par les routeurs
- Pas de checksum de l'entête → gain de performances

#### Pas de fragmentation par les routeurs
- Seul l'**hôte source** peut fragmenter
- Extension "Fragment Header" utilisée si nécessaire
- Améliore les performances des routeurs

#### Découverte de voisins améliorée
- **NDP (Neighbor Discovery Protocol)** remplace ARP
- Messages **ICMPv6** au lieu de protocole séparé
- **SLAAC** : auto-configuration sans DHCP

#### Support natif de la mobilité et de l'IPsec
- IPsec intégré comme **extension obligatoire**
- Meilleure sécurité de bout en bout

---

## 6. Entête du paquet IPv6 {#entête-ipv6}

### Structure de l'entête IPv6 (40 octets fixes)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version| Traffic Class |           Flow Label                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Payload Length        |  Next Header  |   Hop Limit   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                         Source Address                        +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                      Destination Address                      +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### Champs de l'entête IPv6

#### Version (4 bits)
- Valeur : **0110** (6 en binaire)
- Identifie IPv6

#### Traffic Class (8 bits) ⚠️ **CHAMP IMPORTANT**
- Équivalent du champ **ToS/DSCP** d'IPv4
- Utilisé pour la **QoS (Quality of Service)**
- Permet de **prioriser certains flux** (VoIP, vidéo)

#### Flow Label (20 bits)
- Identifie un **flux de paquets** nécessitant un traitement spécial
- Permet aux routeurs de maintenir un **état pour un flux**
- Améliore la QoS pour les applications temps réel

#### Payload Length (16 bits)
- Taille des **données** (sans l'entête de base)
- Taille en **octets**
- Valeur maximale : **65 535 octets**
- ⚠️ N'inclut PAS l'entête IPv6 (contrairement à IPv4)

#### Next Header (8 bits) ⚠️ **CHAMP IMPORTANT**
- Équivalent du champ **Protocol** d'IPv4
- Identifie le type du prochain entête :
  - **6** = TCP
  - **17** = UDP
  - **58** = ICMPv6
  - **0** = Hop-by-Hop Options
  - **43** = Routing Header
  - **44** = Fragment Header
  - **51** = Authentication Header (AH)
  - **50** = Encapsulating Security Payload (ESP)
  - **60** = Destination Options

#### Hop Limit (8 bits) ⚠️ **CHAMP IMPORTANT**
- Équivalent du **TTL** d'IPv4
- **Décrémenté de 1** à chaque routeur
- Si Hop Limit = 0 → paquet détruit
- Message **ICMPv6 Time Exceeded** envoyé à la source

#### Source Address (128 bits)
- Adresse IPv6 de l'émetteur (16 octets)

#### Destination Address (128 bits)
- Adresse IPv6 du destinataire (16 octets)

### Entêtes d'extension IPv6
Les fonctionnalités optionnelles sont gérées par des **entêtes d'extension** chainés :
- **Hop-by-Hop Options** : traité par chaque routeur
- **Routing** : liste de routeurs à traverser
- **Fragment** : gestion de la fragmentation
- **Authentication Header (AH)** : authentification IPsec
- **Encapsulating Security Payload (ESP)** : chiffrement IPsec
- **Destination Options** : traité uniquement par la destination

---

## 7. Routage des paquets {#routage}

### Processus de routage

#### Décision de routage de l'hôte (Host Routing)
Lorsqu'un hôte envoie un paquet, il détermine si la destination est :
- **Locale (même réseau)** : livraison directe via ARP/NDP
- **Distante (autre réseau)** : envoi vers la passerelle par défaut

**Méthode** :
1. Comparer l'adresse IP de destination avec l'adresse IP source et le masque de sous-réseau
2. Si même réseau → **livraison directe**
3. Si réseau différent → **livraison indirecte** via la passerelle

#### Routage dans le réseau
Chaque routeur :
1. **Reçoit le paquet** sur une interface  
2. **Examine l'adresse IP de destination**
3. **Consulte sa table de routage**
4. **Détermine le prochain saut (next-hop)**
5. **Encapsule le paquet** dans une nouvelle trame (changement d'adresses MAC)
6. **Transmet le paquet** vers le routeur suivant

#### Livraison finale
Le **dernier routeur** :
- Détermine que la destination est dans un réseau **directement connecté**
- Effectue la **livraison directe** au destinataire
- Utilise **ARP (IPv4)** ou **NDP (IPv6)** pour résoudre l'adresse MAC

### Opérations du routeur

#### Réception du paquet (De-encapsulation Layer 2)
1. Vérifier le **FCS** (Frame Check Sequence) de la trame
2. Si OK → extraire le paquet (supprimer l'entête Layer 2)
3. Si erreur → rejeter la trame

#### Traitement du paquet (Layer 3)
1. Lire l'**adresse IP de destination**
2. **Décrémenter le TTL** (IPv4) ou **Hop Limit** (IPv6)
3. Si TTL/Hop Limit = 0 → détruire le paquet et envoyer ICMP Time Exceeded
4. **Consulter la table de routage** pour trouver la meilleure route
5. Déterminer l'**interface de sortie** et le **next-hop**

#### Transmission du paquet (Re-encapsulation Layer 2)
1. Créer une **nouvelle trame** Layer 2 :
   - **MAC source** : adresse MAC de l'interface de sortie du routeur
   - **MAC destination** : adresse MAC du prochain saut (routeur suivant ou hôte final)
2. **Transmettre la trame** via l'interface de sortie

### Comparaison des adresses MAC

| Étape | Adresse MAC Source | Adresse MAC Destination |
|-------|-------------------|------------------------|
| **Hôte A → Routeur 1** | MAC de A | MAC de R1 interface G0/0 |
| **Routeur 1 → Routeur 2** | MAC de R1 interface G0/1 | MAC de R2 interface G0/0 |
| **Routeur 2 → Hôte B** | MAC de R2 interface G0/1 | MAC de B |

⚠️ **Point clé** : Les adresses **MAC changent** à chaque saut, les adresses **IP restent identiques**

---

## 8. Table de routage {#table-routage}

### Fonction de la table de routage
La **table de routage** contient les informations nécessaires pour router les paquets :
- Routes vers les **réseaux distants** (appris via protocoles de routage)
- Routes vers les **réseaux directement connectés** (interfaces actives)
- Route **par défaut** (0.0.0.0/0 ou ::/0)

### Construction de la table de routage

#### Sources des routes
1. **Réseaux directement connectés (C)** : interfaces configurées et actives
2. **Routes statiques (S)** : configurées manuellement par l'administrateur
3. **Protocoles de routage dynamique** :
   - **RIP** (Routing Information Protocol) : protocole à vecteur de distance
   - **OSPF** (Open Shortest Path First) : protocole à état de lien
   - **EIGRP** (Enhanced Interior Gateway Routing Protocol) : Cisco propriétaire
   - **BGP** (Border Gateway Protocol) : routage Internet

#### Affichage de la table de routage

**IPv4** :
```
Router# show ip route
```

**IPv6** :
```
Router# show ipv6 route
```

### Lecture d'une entrée de la table de routage

Exemple d'entrée IPv4 :
```
D    10.1.1.0/24 [90/2170112] via 209.165.200.226, 00:00:05, Serial0/0/0
```

Décomposition :
- **D** : route apprise via protocole **EIGRP**
- **10.1.1.0/24** : réseau de destination
- **[90/2170112]** :
  - **90** = distance administrative (AD) d'EIGRP
  - **2170112** = métrique (coût de la route)
- **via 209.165.200.226** : adresse IP du **prochain saut (next-hop)**
- **Serial0/0/0** : **interface de sortie**
- **00:00:05** : temps écoulé depuis l'apprentissage de la route

### Codes des routes

| Code | Source | Description |
|------|--------|-------------|
| **C** | Connected | Réseau directement connecté |
| **L** | Local | Adresse IP locale de l'interface |
| **S** | Static | Route statique |
| **D** | EIGRP | Route apprise via EIGRP |
| **O** | OSPF | Route apprise via OSPF |
| **R** | RIP | Route apprise via RIP |
| **B** | BGP | Route apprise via BGP |
| **S*** | Static | Route statique candidate par défaut |

### Distance administrative (AD)

La **distance administrative** définit la **fiabilité** d'une source de route :
- Plus la valeur est **faible**, plus la route est **fiable**
- Si plusieurs routes existent vers la même destination, celle avec la **plus petite AD** est préférée

| Source | AD |
|--------|-----|
| Interface connectée | 0 |
| Route statique | 1 |
| EIGRP (résumé) | 5 |
| eBGP | 20 |
| EIGRP (interne) | 90 |
| OSPF | 110 |
| RIP | 120 |
| EIGRP (externe) | 170 |
| iBGP | 200 |

### Sélection de la meilleure route

Processus de décision du routeur :
1. **Longest prefix match** (correspondance la plus spécifique)
   - Route /28 préférée à /24 pour la même destination
2. **Distance administrative** (si plusieurs routes avec même préfixe)
3. **Métrique** (si même AD)

### Route par défaut (Gateway of Last Resort)

- Notation IPv4 : **0.0.0.0/0** (toutes les destinations)
- Notation IPv6 : **::/0**
- Utilisée quand **aucune route spécifique** ne correspond
- Généralement pointée vers l'**ISP** ou le **routeur du cœur de réseau**

Configuration d'une route par défaut :
```
Router(config)# ip route 0.0.0.0 0.0.0.0 [next-hop-ip]
Router(config)# ipv6 route ::/0 [next-hop-ip]
```

---

## 9. Commandes IOS utiles {#commandes}

### Affichage de la table de routage

```
Router# show ip route
Router# show ipv6 route
```

### Afficher des informations sur les routes

```
Router# show ip route connected      # Routes connectées IPv4
Router# show ip route static         # Routes statiques IPv4
Router# show ip route ospf           # Routes OSPF

Router# show ipv6 route connected    # Routes connectées IPv6
Router# show ipv6 route static       # Routes statiques IPv6
```

### Afficher une route spécifique

```
Router# show ip route 10.1.1.0
Router# show ipv6 route 2001:db8:acad:1::/64
```

### Vérification de la connectivité

```
Router# ping [ip-address]
Router# ping ipv6 [ipv6-address]
Router# traceroute [ip-address]
Router# traceroute ipv6 [ipv6-address]
```

### Configuration de routes statiques

**IPv4** :
```
Router(config)# ip route [network] [mask] [next-hop-ip | exit-interface]
```

**IPv6** :
```
Router(config)# ipv6 route [prefix/length] [next-hop-ipv6 | exit-interface]
```

### Activation du routage IPv6

```
Router(config)# ipv6 unicast-routing
```

---

## Résumé des points clés 🎯

### IPv4
- ✅ Entête variable : **20 à 60 octets**
- ✅ Champs importants : **TTL, Protocol, Source/Dest IP**
- ✅ TTL décrémenté à chaque routeur pour éviter les boucles
- ✅ Fragmentation par les routeurs possible

### IPv6
- ✅ Entête fixe : **40 octets**
- ✅ Champs importants : **Hop Limit, Next Header, Traffic Class**
- ✅ Hop Limit = équivalent TTL
- ✅ Next Header = chaînage des entêtes d'extension
- ✅ Pas de fragmentation par les routeurs (seulement par la source)

### Routage
- ✅ Adresses **MAC changent** à chaque saut
- ✅ Adresses **IP identiques** de bout en bout
- ✅ Table de routage : décision basée sur **longest prefix match**
- ✅ Distance administrative : critère de **fiabilité** des routes

### Table de routage
- ✅ Routes connectées (C), statiques (S), dynamiques (D, O, R)
- ✅ Route par défaut : 0.0.0.0/0 (IPv4) ou ::/0 (IPv6)
- ✅ Commandes : `show ip route`, `show ipv6 route`

---

**Prochaine étape** : Module 9 - Résolution d'adresse (ARP et NDP)
