# QCM Module 12 - Adressage IPv6

**Nombre de questions :** 20
**Durée estimée :** 30 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quelle est la taille d'une adresse IPv6 ?

- [ ] 32 bits
- [ ] 64 bits
- [ ] 128 bits
- [ ] 256 bits

---

## Question 2
Combien de groupes hexadécimaux composent une adresse IPv6 ?

- [ ] 4 groupes de 32 bits
- [ ] 6 groupes de 16 bits
- [ ] 8 groupes de 16 bits
- [ ] 16 groupes de 8 bits

---

## Question 3
Quelle est la forme compressée correcte de l'adresse `2001:0db8:0000:0000:0000:0000:0000:0001` ?

- [ ] 2001:db8:0:0:0:0:0:1
- [ ] 2001:0db8::1
- [ ] 2001:db8::1
- [ ] 2001:db8:0000::1

---

## Question 4
Combien de fois peut-on utiliser la compression `::` dans une adresse IPv6 ?

- [ ] Autant de fois que nécessaire
- [ ] Une seule fois
- [ ] Deux fois maximum
- [ ] Jamais, c'est une syntaxe invalide

---

## Question 5
Quelle est la forme complète (non compressée) de l'adresse `FE80::1` ?

- [ ] FE80:0000:0000:0000:0000:0000:0000:0001
- [ ] FE80:0001:0000:0000:0000:0000:0000:0000
- [ ] FE80:0000:0001:0000:0000:0000:0000:0000
- [ ] FE80:1111:1111:1111:1111:1111:1111:1111

---

## Question 6
Quelle plage d'adresses est utilisée pour les adresses GUA (Global Unicast Address) ?

- [ ] FE80::/10
- [ ] FC00::/7
- [ ] 2000::/3
- [ ] FF00::/8

---

## Question 7
Quelle est la structure typique d'une GUA ? **(Sélectionner 3 éléments)**

- [ ] Global Routing Prefix (48 bits)
- [ ] Subnet ID (16 bits)
- [ ] Interface ID (64 bits)
- [ ] Scope ID (32 bits)

---

## Question 8
Quelle est la plage réservée aux adresses Link-Local (LLA) ?

- [ ] FE00::/10
- [ ] FE80::/10
- [ ] FC80::/10
- [ ] FF80::/10

---

## Question 9
Quelles affirmations concernant les Link-Local Address (LLA) sont correctes ? **(Sélectionner 3 réponses)**

- [ ] Les LLA sont obligatoires sur chaque interface IPv6
- [ ] Les LLA sont routables sur Internet
- [ ] Les LLA sont utilisées comme passerelle par défaut
- [ ] Les LLA commencent toujours par FE80::

---

## Question 10
Pourquoi est-il recommandé de configurer manuellement les LLA sur les routeurs ?

- [ ] Pour économiser de la mémoire
- [ ] Pour avoir des adresses simples et mémorisables (ex: FE80::1)
- [ ] Parce que l'auto-configuration ne fonctionne pas
- [ ] Pour améliorer la sécurité

---

## Question 11
Quelle commande Cisco configure une Link-Local manuelle ?

- [ ] `ipv6 address FE80::1/10`
- [ ] `ipv6 address FE80::1 link-local`
- [ ] `ipv6 link-local FE80::1`
- [ ] `ipv6 ll FE80::1`

---

## Question 12
Quelle adresse multicast représente "tous les routeurs" sur le lien local ?

- [ ] FF02::1
- [ ] FF02::2
- [ ] FF02::5
- [ ] FF02::A

---

## Question 13
Quelle est la structure d'une adresse multicast solicited-node ?

- [ ] FF02::1:FF + 16 derniers bits de l'unicast
- [ ] FF02::1:FF + 24 derniers bits de l'unicast
- [ ] FF02::FF + 32 derniers bits de l'unicast
- [ ] FF02::1 + Interface ID complète

---

## Question 14
Pour l'adresse unicast `2001:db8:acad:1::20`, quelle est l'adresse solicited-node correspondante ?

- [ ] FF02::1:FF00:0001
- [ ] FF02::1:FF00:0020
- [ ] FF02::1:FF01:0020
- [ ] FF02::1:FFAC:AD01

---

## Question 15
Quelle adresse MAC multicast correspond à l'adresse IPv6 multicast `FF02::1:FF00:6700` ?

- [ ] 01:00:5E:00:67:00
- [ ] 33:33:00:67:00:00
- [ ] 33:33:FF:00:67:00
- [ ] FF:FF:FF:00:67:00

---

## Question 16
Quelle est la taille standard d'un sous-réseau IPv6 ?

- [ ] /48
- [ ] /56
- [ ] /64
- [ ] /128

---

## Question 17
Combien de sous-réseaux /64 peut-on créer à partir d'un préfixe /48 ?

- [ ] 256
- [ ] 4 096
- [ ] 65 536
- [ ] 16 777 216

---

## Question 18
Quel préfixe est recommandé pour les liens point-à-point entre routeurs en IPv6 ?

- [ ] /64
- [ ] /112
- [ ] /126
- [ ] /127

---

## Question 19
Quelles adresses multicast sont utilisées par les protocoles de routage ? **(Sélectionner 3 réponses)**

- [ ] FF02::5 (OSPFv3)
- [ ] FF02::9 (RIPng)
- [ ] FF02::A (EIGRP)
- [ ] FF02::1:2 (DHCPv6)

---

## Question 20
Quelle est l'adresse de loopback en IPv6 ?

- [ ] ::1/128
- [ ] FE80::1
- [ ] 127.0.0.1
- [ ] 0000:0000:0000:0000:0000:0000:0000:0001

---

## Réponses et explications

### Question 1
**Réponse correcte :** C (128 bits)

**Explication :**
IPv6 utilise des adresses de 128 bits, soit 4 fois plus que IPv4 (32 bits). Cela permet un espace d'adressage de 2^128 adresses, soit environ 340 sextillions d'adresses, résolvant définitivement le problème d'épuisement des adresses IPv4.

---

### Question 2
**Réponse correcte :** C (8 groupes de 16 bits)

**Explication :**
Une adresse IPv6 est composée de 8 groupes de 16 bits (soit 8 × 16 = 128 bits). Chaque groupe est représenté par 4 chiffres hexadécimaux (0-9, A-F) séparés par des deux-points (:). Exemple : 2001:0db8:85a3:0000:0000:8a2e:0370:7334.

---

### Question 3
**Réponse correcte :** C (2001:db8::1)

**Explication :**
Les règles de compression IPv6 :
1. Supprimer les zéros de tête dans chaque groupe : 0db8 → db8
2. Remplacer une séquence de groupes de zéros par :: (une seule fois)

Résultat : 2001:db8::1 (la forme la plus courte et correcte).

---

### Question 4
**Réponse correcte :** B (Une seule fois)

**Explication :**
La compression :: ne peut être utilisée qu'UNE SEULE FOIS dans une adresse IPv6. Si on l'utilisait plusieurs fois, il serait impossible de déterminer combien de groupes de zéros chaque :: représente. Cette règle garantit qu'une adresse compressée peut toujours être expansée de manière unique.

---

### Question 5
**Réponse correcte :** A (FE80:0000:0000:0000:0000:0000:0000:0001)

**Explication :**
Pour expanser FE80::1 :
1. Compter les groupes présents : FE80 et 1 = 2 groupes
2. Nombre de groupes manquants : 8 - 2 = 6 groupes
3. Remplacer :: par 6 groupes de 0000
4. Ajouter les zéros de tête : 1 → 0001

Résultat : FE80:0000:0000:0000:0000:0000:0000:0001

---

### Question 6
**Réponse correcte :** C (2000::/3)

**Explication :**
Les GUA (Global Unicast Address) utilisent la plage 2000::/3. Ces adresses commencent par les bits 001 en binaire. Elles sont routables globalement sur Internet, équivalentes aux adresses publiques IPv4. Actuellement, l'IANA alloue principalement des préfixes commençant par 2001::/16.

---

### Question 7
**Réponses correctes :** A (Global Routing Prefix 48 bits), B (Subnet ID 16 bits), C (Interface ID 64 bits)

**Explication :**
Structure d'une GUA :
- **Global Routing Prefix** (48 bits) : identifie l'organisation sur Internet
- **Subnet ID** (16 bits) : permet de créer 65 536 sous-réseaux internes
- **Interface ID** (64 bits) : identifie une interface sur le sous-réseau

Total : 48 + 16 + 64 = 128 bits. Le Scope ID n'existe pas dans cette structure.

---

### Question 8
**Réponse correcte :** B (FE80::/10)

**Explication :**
Les Link-Local Address (LLA) utilisent le préfixe FE80::/10. En binaire, cela correspond à 1111 1110 10xx xxxx. Bien qu'il s'agisse techniquement d'un /10, en pratique, les 54 bits suivants sont toujours à zéro, donc toutes les LLA commencent par FE80:0000:0000:0000 ou FE80::.

---

### Question 9
**Réponses correctes :** A (obligatoires), C (passerelle par défaut), D (commencent par FE80::)

**Explication :**
Les LLA sont :
- **Obligatoires** sur chaque interface IPv6 active
- **Non routables** (ne traversent pas les routeurs)
- **Utilisées comme passerelle par défaut** par les clients (point crucial)
- Commencent toujours par FE80:: (en pratique)

Les clients IPv6 utilisent la LLA du routeur (ex: FE80::1) comme passerelle, pas la GUA.

---

### Question 10
**Réponse correcte :** B (Pour avoir des adresses simples et mémorisables)

**Explication :**
Les LLA générées automatiquement via EUI-64 sont longues et complexes (ex: FE80::021A:2BFF:FE3C:4D5E). La configuration manuelle permet d'utiliser des adresses simples comme FE80::1, FE80::2, etc., ce qui :
- Facilite l'administration
- Simplifie le troubleshooting
- Permet une configuration cohérente (même LLA sur toutes les interfaces d'un routeur)

---

### Question 11
**Réponse correcte :** B (`ipv6 address FE80::1 link-local`)

**Explication :**
La commande correcte sur un routeur Cisco est :
```
Router(config-if)# ipv6 address FE80::1 link-local
```
Le mot-clé `link-local` indique qu'il s'agit d'une Link-Local Address. On ne spécifie pas le /10 car c'est implicite pour les LLA.

---

### Question 12
**Réponse correcte :** B (FF02::2)

**Explication :**
Les adresses multicast importantes :
- **FF02::1** : Tous les nœuds (all nodes)
- **FF02::2** : Tous les routeurs (all routers)
- **FF02::5** : Routeurs OSPFv3
- **FF02::A** : Routeurs EIGRP

FF02::2 est utilisée notamment pour les Router Solicitations (RS).

---

### Question 13
**Réponse correcte :** B (FF02::1:FF + 24 derniers bits de l'unicast)

**Explication :**
Une adresse solicited-node est construite ainsi :
- Préfixe : FF02:0000:0000:0000:0000:0001:FF
- Suivi des **24 derniers bits** (6 derniers chiffres hexa) de l'adresse unicast

Elle est utilisée par NDP pour la résolution d'adresse, remplaçant le broadcast ARP d'IPv4.

---

### Question 14
**Réponse correcte :** B (FF02::1:FF00:0020)

**Explication :**
Pour 2001:db8:acad:1::20 :
1. Identifier les 24 derniers bits : ::0020 = 00:0020
2. Créer la solicited-node : FF02::1:FF + 00:0020
3. Résultat : FF02::1:FF00:0020

Cette adresse multicast est utilisée pour envoyer des Neighbor Solicitation (NS) lors de la résolution d'adresse.

---

### Question 15
**Réponse correcte :** C (33:33:FF:00:67:00)

**Explication :**
Les adresses IPv6 multicast sont mappées sur des adresses MAC multicast :
- Format : **33:33** + [4 derniers octets de l'IPv6 multicast]
- Pour FF02::1:FF00:6700, les 4 derniers octets sont FF:00:67:00
- MAC multicast : 33:33:FF:00:67:00

(Note : IPv4 utilise 01:00:5E pour le multicast)

---

### Question 16
**Réponse correcte :** C (/64)

**Explication :**
Le /64 est le standard pour un sous-réseau IPv6 :
- Compatible avec SLAAC (nécessite /64)
- Compatible avec EUI-64 (Interface ID = 64 bits)
- Permet 2^64 = 18 trillions d'hôtes par sous-réseau
- Simplifie la gestion (pas de calcul complexe)

Exception : /127 pour les liens point-à-point (RFC 6164).

---

### Question 17
**Réponse correcte :** C (65 536)

**Explication :**
De /48 à /64, on utilise 16 bits pour le Subnet ID (64 - 48 = 16 bits).
Nombre de sous-réseaux = 2^16 = 65 536 sous-réseaux /64.

C'est pourquoi une organisation qui reçoit un /48 peut créer 65 536 sous-réseaux différents, ce qui est largement suffisant pour la plupart des organisations.

---

### Question 18
**Réponse correcte :** D (/127)

**Explication :**
Le RFC 6164 recommande l'utilisation du /127 pour les liens point-à-point entre routeurs :
- Permet exactement 2 adresses (2^1 = 2)
- Évite les problèmes de sécurité du /64 sur les liens point-à-point
- Économise l'espace d'adressage

Le /64 fonctionne aussi mais gaspille des adresses.

---

### Question 19
**Réponses correctes :** A (FF02::5 - OSPFv3), B (FF02::9 - RIPng), C (FF02::A - EIGRP)

**Explication :**
Adresses multicast des protocoles de routage IPv6 :
- **FF02::5** : Routeurs OSPFv3
- **FF02::9** : Routeurs RIPng (RIP next generation)
- **FF02::A** : Routeurs EIGRP pour IPv6

FF02::1:2 est l'adresse pour les serveurs/relais DHCPv6, pas un protocole de routage.

---

### Question 20
**Réponse correcte :** A (::1/128)

**Explication :**
L'adresse de loopback IPv6 est ::1/128 (ou 0000:0000:0000:0000:0000:0000:0000:0001/128 en forme complète). C'est l'équivalent de 127.0.0.1 en IPv4. Elle est utilisée pour tester la pile TCP/IP locale. Le /128 indique qu'il s'agit d'une adresse hôte unique (tous les 128 bits).
