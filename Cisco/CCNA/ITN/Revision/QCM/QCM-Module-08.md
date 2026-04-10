# QCM Module 8 - Couche Réseau (Network Layer)

**Nombre de questions :** 18
**Durée estimée :** 25 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quelle est la fonction principale de la couche réseau (Layer 3) dans le modèle OSI ?

- [ ] Fragmenter les données en segments
- [ ] Router les paquets entre différents réseaux
- [ ] Assurer la livraison fiable des données
- [ ] Encapsuler les paquets dans des trames

---

## Question 2
Quel est le champ de l'entête IPv4 qui empêche les boucles de routage infinies ?

- [ ] Protocol
- [ ] Total Length
- [ ] Time to Live (TTL)
- [ ] Fragment Offset

---

## Question 3
**Sélectionnez DEUX réponses correctes.**

Quelles sont les valeurs correctes du champ "Protocol" dans l'entête IPv4 ?

- [ ] 1 = ICMP
- [ ] 6 = UDP
- [ ] 17 = UDP
- [ ] 89 = OSPF
- [ ] 58 = ICMPv6

---

## Question 4
Un paquet IPv4 a un champ TTL initial de 64. Après avoir traversé 8 routeurs, quelle sera la valeur du TTL ?

- [ ] 64
- [ ] 56
- [ ] 0
- [ ] 8

---

## Question 5
Quelle est la taille **fixe** de l'entête IPv6 (sans extensions) ?

- [ ] 20 octets
- [ ] 40 octets
- [ ] 60 octets
- [ ] Variable selon les options

---

## Question 6
Quel champ de l'entête IPv6 est l'équivalent du champ "Protocol" d'IPv4 ?

- [ ] Flow Label
- [ ] Traffic Class
- [ ] Next Header
- [ ] Hop Limit

---

## Question 7
**Sélectionnez TROIS réponses correctes.**

Quelles valeurs du champ "Next Header" IPv6 sont correctes ?

- [ ] 6 = TCP
- [ ] 17 = UDP
- [ ] 43 = Routing Header
- [ ] 58 = ICMP
- [ ] 89 = OSPF

---

## Question 8
Quelle est la différence principale entre la fragmentation IPv4 et IPv6 ?

- [ ] IPv4 ne supporte pas la fragmentation
- [ ] IPv6 permet aux routeurs de fragmenter les paquets
- [ ] IPv4 permet aux routeurs de fragmenter, IPv6 seulement la source
- [ ] Il n'y a aucune différence

---

## Question 9
Dans l'entête IPv4, quel flag (bit) indique "Don't Fragment" ?

- [ ] Bit 0
- [ ] Bit 1 (DF)
- [ ] Bit 2 (MF)
- [ ] Bit 7

---

## Question 10
Lors du routage d'un paquet à travers plusieurs routeurs, qu'est-ce qui **change** à chaque saut ?

- [ ] Adresses IP source et destination
- [ ] Adresses MAC source et destination
- [ ] Numéro de port source et destination
- [ ] Valeur du champ Protocol

---

## Question 11
Examinez cette entrée de table de routage :
```
D    10.1.1.0/24 [90/2170112] via 209.165.200.226, 00:00:05, Serial0/0/0
```
Que représente la valeur **90** ?

- [ ] La métrique de la route
- [ ] La distance administrative (AD)
- [ ] Le nombre de sauts
- [ ] Le temps en secondes depuis l'apprentissage

---

## Question 12
Quelle distance administrative (AD) est la plus fiable ?

- [ ] Route statique : 1
- [ ] EIGRP interne : 90
- [ ] OSPF : 110
- [ ] RIP : 120

---

## Question 13
Un routeur reçoit deux routes vers le réseau 192.168.10.0 :
- Route 1 : 192.168.10.0/24 via OSPF (AD=110)
- Route 2 : 192.168.10.0/28 via RIP (AD=120)

Quelle route sera choisie et pourquoi ?

- [ ] Route 1, car OSPF a une AD plus faible
- [ ] Route 2, car RIP a une AD plus élevée
- [ ] Route 2, car elle a le préfixe le plus long (longest prefix match)
- [ ] Les deux routes seront utilisées en parallèle

---

## Question 14
Quel code de route indique un réseau directement connecté dans la table de routage ?

- [ ] S (Static)
- [ ] C (Connected)
- [ ] L (Local)
- [ ] D (EIGRP)

---

## Question 15
Quelle est la notation de la route par défaut en IPv4 ?

- [ ] 255.255.255.255/32
- [ ] 0.0.0.0/0
- [ ] ::/0
- [ ] FF:FF:FF:FF:FF:FF

---

## Question 16
Quel champ de l'entête IPv6 remplace le champ "TTL" d'IPv4 ?

- [ ] Flow Label
- [ ] Payload Length
- [ ] Hop Limit
- [ ] Next Header

---

## Question 17
**Sélectionnez DEUX réponses correctes.**

Quels sont les avantages du protocole IPv6 par rapport à IPv4 ?

- [ ] Entête plus simple (40 octets fixes)
- [ ] Pas de fragmentation par les routeurs
- [ ] Utilise le protocole ARP pour la résolution d'adresse
- [ ] Supporte nativement IPsec
- [ ] Utilise uniquement le broadcast

---

## Question 18
Quelle commande IOS affiche la table de routage IPv6 ?

- [ ] show ip route
- [ ] show ipv6 neighbors
- [ ] show ipv6 route
- [ ] show ipv6 interface brief

---

## Réponses et explications

### Question 1
**Réponse correcte :** Router les paquets entre différents réseaux

**Explication :**
La couche réseau (Layer 3) a pour fonction principale de **router les paquets** entre différents réseaux en utilisant les adresses IP. La fragmentation en segments est effectuée par la couche Transport (Layer 4). L'encapsulation dans des trames est réalisée par la couche Liaison de données (Layer 2). La livraison fiable est assurée par TCP (Layer 4), pas par IP qui est "best-effort".

---

### Question 2
**Réponse correcte :** Time to Live (TTL)

**Explication :**
Le champ **TTL** (8 bits) est décrémenté de 1 à chaque passage par un routeur. Si TTL atteint 0, le paquet est détruit et un message ICMP "Time Exceeded" est envoyé à la source. Cela empêche les paquets de circuler indéfiniment dans le réseau en cas de boucle de routage.

---

### Question 3
**Réponses correctes :** 1 = ICMP, 17 = UDP, 89 = OSPF

**Explication :**
Le champ "Protocol" (8 bits) identifie le protocole de couche supérieure (Layer 4) :
- **1** = ICMP
- **6** = TCP (pas UDP)
- **17** = UDP
- **89** = OSPF
- **88** = EIGRP
- **58** = ICMPv6 (dans IPv6, pas IPv4)

---

### Question 4
**Réponse correcte :** 56

**Explication :**
Le TTL est **décrémenté de 1** à chaque routeur traversé. Calcul : 64 - 8 = **56**. Si le TTL atteignait 0, le paquet serait détruit.

---

### Question 5
**Réponse correcte :** 40 octets

**Explication :**
L'entête IPv6 a une taille **fixe de 40 octets**, contrairement à IPv4 qui a une taille variable (20 à 60 octets) en raison du champ "Options". Cette simplification améliore les performances de traitement par les routeurs.

---

### Question 6
**Réponse correcte :** Next Header

**Explication :**
Le champ **Next Header** (8 bits) d'IPv6 est l'équivalent du champ "Protocol" d'IPv4. Il identifie le type de l'entête suivant (TCP, UDP, ICMPv6, entêtes d'extension, etc.).

---

### Question 7
**Réponses correctes :** 6 = TCP, 17 = UDP, 43 = Routing Header

**Explication :**
Valeurs correctes du champ "Next Header" :
- **6** = TCP
- **17** = UDP
- **43** = Routing Header (extension IPv6)
- **44** = Fragment Header
- **58** = ICMPv6 (pas 58 = ICMP)
- **89** = OSPF (mais rarement utilisé directement dans Next Header)

---

### Question 8
**Réponse correcte :** IPv4 permet aux routeurs de fragmenter, IPv6 seulement la source

**Explication :**
En **IPv4**, les routeurs peuvent fragmenter les paquets si nécessaire. En **IPv6**, seul l'hôte source peut fragmenter (en utilisant l'entête d'extension "Fragment Header"). Les routeurs IPv6 ne fragmentent jamais, ils envoient un message ICMPv6 "Packet Too Big" à la source.

---

### Question 9
**Réponse correcte :** Bit 1 (DF)

**Explication :**
Les 3 bits de "Flags" dans l'entête IPv4 :
- **Bit 0** : Réservé (toujours 0)
- **Bit 1 (DF - Don't Fragment)** : Si 1, ne pas fragmenter le paquet
- **Bit 2 (MF - More Fragments)** : Si 1, d'autres fragments suivent

---

### Question 10
**Réponse correcte :** Adresses MAC source et destination

**Explication :**
À chaque saut, le routeur :
- **Change les adresses MAC** (nouvelle trame Layer 2 avec sa MAC source et celle du prochain saut en destination)
- **Conserve les adresses IP** source et destination (elles restent identiques de bout en bout)
- Décrémente le TTL

---

### Question 11
**Réponse correcte :** La distance administrative (AD)

**Explication :**
Format : `[AD/Métrique]`
- **90** = distance administrative d'EIGRP
- **2170112** = métrique de la route
La distance administrative indique la fiabilité de la source de la route (plus c'est bas, plus c'est fiable).

---

### Question 12
**Réponse correcte :** Route statique : 1

**Explication :**
Distance administrative (plus c'est **bas**, plus c'est **fiable**) :
- **Interface connectée** : 0 (le plus fiable)
- **Route statique** : 1
- **EIGRP (résumé)** : 5
- **EIGRP (interne)** : 90
- **OSPF** : 110
- **RIP** : 120

---

### Question 13
**Réponse correcte :** Route 2, car elle a le préfixe le plus long (longest prefix match)

**Explication :**
Le principe de **longest prefix match** est prioritaire. La route avec le préfixe le plus long (/28) est plus spécifique que /24, donc elle sera choisie, même si RIP a une AD moins bonne (120) que OSPF (110). L'AD n'est utilisée que si plusieurs routes ont le **même préfixe**.

---

### Question 14
**Réponse correcte :** C (Connected)

**Explication :**
Codes de routes :
- **C** = Connected (réseau directement connecté)
- **L** = Local (adresse IP locale de l'interface)
- **S** = Static (route statique)
- **D** = EIGRP
- **O** = OSPF
- **R** = RIP

---

### Question 15
**Réponse correcte :** 0.0.0.0/0

**Explication :**
- **IPv4** : route par défaut = `0.0.0.0/0` (couvre toutes les destinations)
- **IPv6** : route par défaut = `::/0`
Elle est utilisée quand aucune route spécifique ne correspond à la destination.

---

### Question 16
**Réponse correcte :** Hop Limit

**Explication :**
Le champ **Hop Limit** (8 bits) d'IPv6 est l'équivalent du **TTL** d'IPv4. Il est décrémenté de 1 à chaque routeur. Si Hop Limit = 0, le paquet est détruit et un message ICMPv6 "Time Exceeded" est envoyé.

---

### Question 17
**Réponses correctes :** Entête plus simple (40 octets fixes), Pas de fragmentation par les routeurs

**Explication :**
Avantages d'IPv6 :
- ✅ Entête fixe de 40 octets (vs 20-60 pour IPv4) = traitement plus rapide
- ✅ Pas de fragmentation par les routeurs = meilleures performances
- ✅ Support natif IPsec
- ✅ Utilise **NDP** (pas ARP) pour la résolution d'adresse
- ✅ Utilise le **multicast** (pas broadcast, qui n'existe plus en IPv6)

---

### Question 18
**Réponse correcte :** show ipv6 route

**Explication :**
Commandes de vérification :
- `show ip route` : table de routage IPv4
- `show ipv6 route` : table de routage IPv6
- `show ipv6 neighbors` : cache NDP (équivalent ARP pour IPv6)
- `show ipv6 interface brief` : résumé des interfaces IPv6
