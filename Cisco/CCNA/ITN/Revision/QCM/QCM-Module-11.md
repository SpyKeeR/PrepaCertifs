# QCM Module 11 - Adressage IPv4

**Nombre de questions :** 18
**Durée estimée :** 25 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quelle est la plage d'adresses de la classe B en IPv4 ?

- [ ] 1.0.0.0 à 126.255.255.255
- [ ] 128.0.0.0 à 191.255.255.255
- [ ] 192.0.0.0 à 223.255.255.255
- [ ] 172.16.0.0 à 172.31.255.255

---

## Question 2
À quelle classe appartient l'adresse IP 172.16.45.10 ?

- [ ] Classe A
- [ ] Classe B
- [ ] Classe C
- [ ] Classe D

---

## Question 3
Quelles sont les adresses privées définies par la RFC 1918 ? **(Sélectionner 3 réponses)**

- [ ] 10.0.0.0/8
- [ ] 172.16.0.0/12
- [ ] 192.168.0.0/16
- [ ] 127.0.0.0/8
- [ ] 169.254.0.0/16

---

## Question 4
Quel est le masque de sous-réseau par défaut pour une adresse de classe C ?

- [ ] 255.0.0.0 ou /8
- [ ] 255.255.0.0 ou /16
- [ ] 255.255.255.0 ou /24
- [ ] 255.255.255.128 ou /25

---

## Question 5
Quelle adresse représente l'adresse de bouclage (loopback) en IPv4 ?

- [ ] 0.0.0.0
- [ ] 127.0.0.1
- [ ] 169.254.1.1
- [ ] 255.255.255.255

---

## Question 6
Quelle est la fonction de l'adresse 255.255.255.255 ?

- [ ] Route par défaut
- [ ] Adresse de broadcast limitée au réseau local
- [ ] Adresse de loopback
- [ ] Adresse APIPA

---

## Question 7
Combien d'hôtes utilisables peut-on avoir dans un sous-réseau /26 ?

- [ ] 30
- [ ] 62
- [ ] 126
- [ ] 254

---

## Question 8
Quel est le "Magic Number" pour un masque de sous-réseau 255.255.255.224 (/27) ?

- [ ] 16
- [ ] 32
- [ ] 64
- [ ] 128

---

## Question 9
Pour le réseau 192.168.10.75/26, quelle est l'adresse du sous-réseau ?

- [ ] 192.168.10.0
- [ ] 192.168.10.32
- [ ] 192.168.10.64
- [ ] 192.168.10.128

---

## Question 10
Combien de sous-réseaux /27 pouvez-vous créer à partir d'un réseau /24 ?

- [ ] 4
- [ ] 8
- [ ] 16
- [ ] 32

---

## Question 11
Quelle notation CIDR permet d'avoir exactement 2 hôtes utilisables (pour un lien point-à-point) ?

- [ ] /28
- [ ] /29
- [ ] /30
- [ ] /31

---

## Question 12
Quelles affirmations concernant le VLSM sont correctes ? **(Sélectionner 2 réponses)**

- [ ] VLSM permet d'utiliser différents masques au sein d'un même réseau principal
- [ ] VLSM optimise l'utilisation des adresses IP
- [ ] VLSM est supporté par RIPv1
- [ ] VLSM nécessite obligatoirement le CIDR

---

## Question 13
Si vous avez besoin de 100 hôtes dans un sous-réseau, quel est le plus petit masque approprié ?

- [ ] /24 (254 hôtes)
- [ ] /25 (126 hôtes)
- [ ] /26 (62 hôtes)
- [ ] /27 (30 hôtes)

---

## Question 14
Quelle est la plage d'adresses multicast IPv4 ?

- [ ] 192.0.0.0 à 223.255.255.255
- [ ] 224.0.0.0 à 239.255.255.255
- [ ] 240.0.0.0 à 255.255.255.255
- [ ] 169.254.0.0 à 169.254.255.255

---

## Question 15
Pour le réseau 192.168.1.0/24, quelle est l'adresse de broadcast ?

- [ ] 192.168.1.0
- [ ] 192.168.1.1
- [ ] 192.168.1.254
- [ ] 192.168.1.255

---

## Question 16
Quelle est l'utilisation de l'adresse 169.254.0.0/16 ?

- [ ] Adresse de loopback
- [ ] APIPA (Automatic Private IP Addressing) pour configuration automatique sans DHCP
- [ ] Adresse multicast
- [ ] Adresse de broadcast

---

## Question 17
Combien d'adresses hôtes sont disponibles dans un réseau de classe A par défaut (sans subnetting) ?

- [ ] 254
- [ ] 65 534
- [ ] 16 777 214
- [ ] 2 147 483 646

---

## Question 18
En VLSM, si vous devez allouer des sous-réseaux pour 500 hôtes, 200 hôtes, 50 hôtes et deux liens point-à-point, par quelle allocation devez-vous commencer ?

- [ ] Les liens point-à-point (/30)
- [ ] Le réseau de 50 hôtes
- [ ] Le réseau de 200 hôtes
- [ ] Le réseau de 500 hôtes

---

## Réponses et explications

### Question 1
**Réponse correcte :** B (128.0.0.0 à 191.255.255.255)

**Explication :**
La classe B couvre les adresses dont le premier octet est compris entre 128 et 191. Les deux premiers bits d'une adresse de classe B sont toujours "10". Le masque par défaut est /16 (255.255.0.0).

---

### Question 2
**Réponse correcte :** B (Classe B)

**Explication :**
L'adresse 172.16.45.10 a un premier octet de 172, qui se situe dans la plage 128-191, caractéristique de la classe B. Cette adresse fait également partie de la plage privée RFC 1918 (172.16.0.0/12).

---

### Question 3
**Réponses correctes :** A (10.0.0.0/8), B (172.16.0.0/12), C (192.168.0.0/16)

**Explication :**
La RFC 1918 définit trois plages d'adresses privées :
- Classe A : 10.0.0.0/8 (1 réseau de classe A)
- Classe B : 172.16.0.0/12 (16 réseaux de classe B)
- Classe C : 192.168.0.0/16 (256 réseaux de classe C)

127.0.0.0/8 est la plage de loopback, et 169.254.0.0/16 est la plage APIPA.

---

### Question 4
**Réponse correcte :** C (255.255.255.0 ou /24)

**Explication :**
Les adresses de classe C (192.0.0.0 à 223.255.255.255) utilisent un masque par défaut de /24 ou 255.255.255.0. Cela signifie que les trois premiers octets représentent la partie réseau et le dernier octet représente la partie hôte, permettant 254 hôtes utilisables.

---

### Question 5
**Réponse correcte :** B (127.0.0.1)

**Explication :**
L'adresse 127.0.0.1 (ou toute adresse du réseau 127.0.0.0/8) est utilisée comme adresse de loopback. Elle permet de tester la pile TCP/IP locale d'un hôte. Les paquets envoyés à cette adresse ne quittent jamais l'hôte.

---

### Question 6
**Réponse correcte :** B (Adresse de broadcast limitée au réseau local)

**Explication :**
L'adresse 255.255.255.255 est appelée "limited broadcast" (broadcast limité). Elle est utilisée pour envoyer des paquets à tous les hôtes du réseau local. Elle ne traverse jamais un routeur et est notamment utilisée par DHCP Discover.

---

### Question 7
**Réponse correcte :** B (62)

**Explication :**
Un masque /26 laisse 6 bits pour les hôtes (32 - 26 = 6 bits).
Nombre d'hôtes = 2^6 - 2 = 64 - 2 = 62 hôtes utilisables.
On soustrait 2 pour exclure l'adresse de réseau et l'adresse de broadcast.

---

### Question 8
**Réponse correcte :** B (32)

**Explication :**
Pour un masque /27, le dernier octet vaut 224 (255.255.255.224).
Magic Number = 256 - 224 = 32.
Cela signifie que les sous-réseaux commencent à 0, 32, 64, 96, 128, 160, 192, 224.

---

### Question 9
**Réponse correcte :** C (192.168.10.64)

**Explication :**
Pour un masque /26 (255.255.255.192), le Magic Number est 256 - 192 = 64.
Les sous-réseaux sont : 0, 64, 128, 192.
L'adresse 192.168.10.75 se trouve dans le sous-réseau 192.168.10.64/26 (plage 64-127).

---

### Question 10
**Réponse correcte :** B (8)

**Explication :**
Pour passer de /24 à /27, on emprunte 3 bits (27 - 24 = 3).
Nombre de sous-réseaux = 2^3 = 8 sous-réseaux.
Chaque sous-réseau /27 aura 2^5 - 2 = 30 hôtes utilisables.

---

### Question 11
**Réponse correcte :** C (/30)

**Explication :**
Un masque /30 (255.255.255.252) laisse 2 bits pour les hôtes.
Nombre d'hôtes = 2^2 - 2 = 4 - 2 = 2 hôtes utilisables.
C'est le masque standard pour les liens point-à-point entre routeurs. (Note : /31 peut aussi être utilisé selon RFC 3021, mais /30 est le choix traditionnel).

---

### Question 12
**Réponses correctes :** A (VLSM permet d'utiliser différents masques), B (optimise l'utilisation)

**Explication :**
VLSM (Variable Length Subnet Masking) permet d'utiliser différents masques de sous-réseau au sein d'un même réseau principal, optimisant ainsi l'utilisation des adresses IP. RIPv1 ne supporte PAS VLSM (seuls RIPv2, OSPF, EIGRP le supportent). VLSM utilise le CIDR mais n'est pas limité au CIDR.

---

### Question 13
**Réponse correcte :** B (/25 avec 126 hôtes)

**Explication :**
Pour 100 hôtes, il faut minimum 2^n - 2 ≥ 100, donc 2^n ≥ 102.
- /26 : 2^6 - 2 = 62 hôtes (insuffisant)
- /25 : 2^7 - 2 = 126 hôtes (suffisant)

Le masque /25 est le plus petit masque permettant d'héberger 100 hôtes.

---

### Question 14
**Réponse correcte :** B (224.0.0.0 à 239.255.255.255)

**Explication :**
La plage 224.0.0.0 à 239.255.255.255 est réservée pour le multicast IPv4 (classe D). Les adresses multicast permettent la communication un-à-plusieurs. Exemples : 224.0.0.1 (tous les hôtes), 224.0.0.2 (tous les routeurs), 224.0.0.5 (routeurs OSPF).

---

### Question 15
**Réponse correcte :** D (192.168.1.255)

**Explication :**
Pour un réseau 192.168.1.0/24, l'adresse de broadcast est obtenue en mettant tous les bits de la partie hôte à 1. Avec un masque /24, le dernier octet représente la partie hôte. Tous les bits à 1 donnent 255.
Plage : 192.168.1.1 à 192.168.1.254 (hôtes utilisables), 192.168.1.255 (broadcast).

---

### Question 16
**Réponse correcte :** B (APIPA pour configuration automatique sans DHCP)

**Explication :**
169.254.0.0/16 est la plage APIPA (Automatic Private IP Addressing). Un hôte Windows s'attribue automatiquement une adresse de cette plage quand aucun serveur DHCP n'est disponible et qu'aucune adresse statique n'est configurée. La communication est limitée au lien local (non routable).

---

### Question 17
**Réponse correcte :** C (16 777 214)

**Explication :**
Une adresse de classe A utilise un masque par défaut /8 (255.0.0.0), laissant 24 bits pour les hôtes.
Nombre d'hôtes = 2^24 - 2 = 16 777 216 - 2 = 16 777 214 hôtes utilisables.
Les classes A sont destinées aux très grands réseaux.

---

### Question 18
**Réponse correcte :** D (Le réseau de 500 hôtes)

**Explication :**
En VLSM, la règle d'or est de commencer par le réseau nécessitant le PLUS grand nombre d'hôtes et de descendre progressivement. Cela évite le gaspillage d'adresses et permet d'allouer efficacement l'espace d'adressage. Ordre : 500 hôtes, puis 200, puis 50, puis les deux liens point-à-point.
