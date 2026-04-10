# QCM Checkpoint - Modules 11-13 : Adressage IP

**Nombre de questions :** 30  
**Durée estimée :** 45 minutes  
**Seuil de réussite :** 75% (23/30 questions)

**Couverture :**
- Module 11 : Adressage IPv4 (10 questions)
- Module 12 : Adressage IPv6 (10 questions)
- Module 13 : ICMP et protocoles de connectivité (10 questions)

---

## MODULE 11 - ADRESSAGE IPv4

### Question 1
À quelle classe appartient l'adresse IP `172.25.100.50` ? (Choix unique)

- [ ] Classe A
- [ ] Classe B
- [ ] Classe C
- [ ] Classe D

---

### Question 2
Parmi les plages suivantes, lesquelles correspondent aux adresses privées définies par RFC 1918 ? (Choix multiples - 3 réponses)

- [ ] 10.0.0.0 - 10.255.255.255
- [ ] 169.254.0.0 - 169.254.255.255
- [ ] 172.16.0.0 - 172.31.255.255
- [ ] 172.0.0.0 - 172.255.255.255
- [ ] 192.168.0.0 - 192.168.255.255
- [ ] 127.0.0.0 - 127.255.255.255

---

### Question 3
À quel sous-réseau appartient l'adresse `192.168.10.75/26` ? (Choix unique)

- [ ] 192.168.10.0/26
- [ ] 192.168.10.64/26
- [ ] 192.168.10.128/26
- [ ] 192.168.10.32/26

---

### Question 4
Combien d'adresses d'hôtes utilisables peut-on obtenir avec un masque /27 ? (Choix unique)

- [ ] 14 hôtes
- [ ] 30 hôtes
- [ ] 32 hôtes
- [ ] 62 hôtes

---

### Question 5
Une entreprise a besoin d'un sous-réseau pouvant accueillir au minimum 120 hôtes. Quel est le masque de sous-réseau le plus approprié ? (Choix unique)

- [ ] /24 (255.255.255.0)
- [ ] /25 (255.255.255.128)
- [ ] /26 (255.255.255.192)
- [ ] /27 (255.255.255.224)

---

### Question 6
Vous devez mettre en place un plan d'adressage VLSM pour le réseau `192.168.1.0/24` avec les besoins suivants :
- Réseau A : 50 hôtes
- Réseau B : 25 hôtes
- Réseau C : 10 hôtes

Quelle allocation est correcte ? (Choix unique)

- [ ] A: /25, B: /26, C: /27
- [ ] A: /26, B: /27, C: /28
- [ ] A: /27, B: /28, C: /29
- [ ] A: /24, B: /25, C: /26

---

### Question 7
Un administrateur réseau doit créer 8 sous-réseaux à partir du réseau `10.1.0.0/16`. Quel masque doit-il utiliser et combien d'hôtes par sous-réseau obtiendra-t-il ? (Choix unique)

- [ ] /19 avec 8 190 hôtes par sous-réseau
- [ ] /20 avec 4 094 hôtes par sous-réseau
- [ ] /21 avec 2 046 hôtes par sous-réseau
- [ ] /24 avec 254 hôtes par sous-réseau

---

### Question 8
Quelles affirmations concernant l'agrégation de routes (route summarization) sont correctes ? (Choix multiples - 2 réponses)

- [ ] Elle permet de réduire la taille des tables de routage
- [ ] Elle nécessite obligatoirement un routage classful
- [ ] Elle regroupe plusieurs réseaux contigus en une seule route
- [ ] Elle augmente le nombre d'entrées dans les tables de routage

---

### Question 9
Quelle est la plage d'adresses du deuxième sous-réseau utilisable lors de la segmentation de `172.16.0.0/16` en sous-réseaux /18 ? (Choix unique)

- [ ] 172.16.0.0 - 172.16.63.255
- [ ] 172.16.64.0 - 172.16.127.255
- [ ] 172.16.128.0 - 172.16.191.255
- [ ] 172.16.192.0 - 172.16.255.255

---

### Question 10
Associez chaque adresse spéciale à sa fonction correcte. (Choix multiples - 3 réponses)

- [ ] 127.0.0.1 : Adresse de bouclage (loopback)
- [ ] 169.254.0.0/16 : Adresse APIPA (link-local)
- [ ] 0.0.0.0/0 : Route par défaut
- [ ] 224.0.0.0/4 : Adresses broadcast
- [ ] 255.255.255.255 : Adresse multicast

---

## MODULE 12 - ADRESSAGE IPv6

### Question 11
Quelle est la forme correctement compressée de l'adresse `2001:0db8:0000:0042:0000:0000:0000:0100` ? (Choix unique)

- [ ] 2001:db8:0:42::100
- [ ] 2001:db8::42::100
- [ ] 2001:db8:0:42:0:0:0:100
- [ ] 2001:0db8::42:0:0:0:100

---

### Question 12
Quelle est la forme complète de l'adresse IPv6 compressée `FE80::1` ? (Choix unique)

- [ ] FE80:0000:0000:0000:0000:0000:0000:0001
- [ ] FE80:0001:0000:0000:0000:0000:0000:0000
- [ ] FE80:0000:0000:0001:0000:0000:0000:0000
- [ ] FE80:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:0001

---

### Question 13
Une organisation reçoit le préfixe `2001:db8:acad::/48`. Quelle est la structure correcte d'une adresse GUA dans ce réseau ? (Choix unique)

- [ ] 48 bits de Global Routing Prefix, 16 bits de Subnet ID, 64 bits d'Interface ID
- [ ] 32 bits de Global Routing Prefix, 32 bits de Subnet ID, 64 bits d'Interface ID
- [ ] 64 bits de Global Routing Prefix, 64 bits d'Interface ID
- [ ] 48 bits de préfixe, 80 bits d'Interface ID

---

### Question 14
Dans l'adresse GUA `2001:db8:acad:1a2b::10/64`, identifiez les composants. (Choix multiples - 2 réponses)

- [ ] Le Global Routing Prefix est 2001:db8:acad
- [ ] Le Subnet ID est 1a2b
- [ ] L'Interface ID est 0010
- [ ] Le préfixe complet est 2001:db8:acad:1a2b::/48

---

### Question 15
Pourquoi est-il recommandé de configurer manuellement les adresses link-local sur les routeurs ? (Choix multiples - 3 réponses)

- [ ] Les adresses générées automatiquement (EUI-64) sont complexes et difficiles à mémoriser
- [ ] Cela permet d'utiliser la même LLA (ex: FE80::1) sur toutes les interfaces du routeur
- [ ] Les LLA manuelles augmentent la vitesse de routage
- [ ] Cela simplifie la configuration de la passerelle par défaut pour les clients
- [ ] Les LLA automatiques ne fonctionnent pas avec IPv6

---

### Question 16
Quel rôle joue l'adresse link-local (LLA) d'un routeur dans un réseau IPv6 ? (Choix unique)

- [ ] Elle sert d'adresse de broadcast pour le réseau
- [ ] Elle est utilisée comme passerelle par défaut par les hôtes IPv6
- [ ] Elle permet le routage des paquets sur Internet
- [ ] Elle remplace l'adresse MAC au niveau liaison de données

---

### Question 17
Un hôte possède l'adresse unicast `2001:db8:acad:1:a8bb:ccff:fe00:6700/64`. Quelle est l'adresse solicited-node multicast correspondante ? (Choix unique)

- [ ] FF02::1:FF00:6700
- [ ] FF02::1:FFFF:6700
- [ ] FF02::1:FE00:6700
- [ ] FF02::1:CCFF:FE00

---

### Question 18
Quelle adresse MAC multicast correspond à l'adresse IPv6 multicast `FF02::1:FF3C:4D5E` ? (Choix unique)

- [ ] 33:33:FF:3C:4D:5E
- [ ] 01:00:5E:3C:4D:5E
- [ ] 33:33:00:01:00:02
- [ ] 01:00:5E:00:00:01

---

### Question 19
Une organisation reçoit le préfixe `/48`. Combien de sous-réseaux `/64` peut-elle créer ? (Choix unique)

- [ ] 256 sous-réseaux
- [ ] 4 096 sous-réseaux
- [ ] 16 384 sous-réseaux
- [ ] 65 536 sous-réseaux

---

### Question 20
Associez chaque adresse multicast IPv6 à sa fonction. (Choix multiples - 3 réponses)

- [ ] FF02::1 : Tous les nœuds IPv6 du lien
- [ ] FF02::2 : Tous les routeurs IPv6 du lien
- [ ] FF02::5 : Routeurs OSPFv3
- [ ] FF02::1:2 : Tous les hôtes du réseau global
- [ ] FF02::A : Serveurs DHCP

---

## MODULE 13 - ICMP ET CONNECTIVITÉ

### Question 21
Un routeur reçoit un paquet IP destiné à un réseau pour lequel il n'a aucune route. Quel message ICMP envoie-t-il à la source ? (Choix unique)

- [ ] ICMPv4 Type 3 Code 0 (Network Unreachable)
- [ ] ICMPv4 Type 3 Code 1 (Host Unreachable)
- [ ] ICMPv4 Type 11 Code 0 (TTL Exceeded)
- [ ] ICMPv4 Type 5 (Redirect)

---

### Question 22
Un routeur envoie des requêtes ARP pour joindre un hôte sur son réseau local, mais ne reçoit aucune réponse. Quel message ICMP envoie-t-il finalement à la source ? (Choix unique)

- [ ] ICMPv4 Type 3 Code 0 (Network Unreachable)
- [ ] ICMPv4 Type 3 Code 1 (Host Unreachable)
- [ ] ICMPv4 Type 3 Code 3 (Port Unreachable)
- [ ] ICMPv4 Type 11 Code 0 (TTL Exceeded)

---

### Question 23
Quel message ICMP est utilisé par la commande `traceroute` pour découvrir le chemin réseau ? (Choix multiples - 2 réponses)

- [ ] ICMPv4 Type 11 Code 0 (TTL Exceeded in Transit)
- [ ] ICMPv4 Type 3 Code 3 (Port Unreachable)
- [ ] ICMPv4 Type 8 (Echo Request)
- [ ] ICMPv4 Type 0 (Echo Reply)

---

### Question 24
Un paquet IP doit traverser un lien avec un MTU de 1400 octets, mais le paquet fait 1500 octets et le bit DF (Don't Fragment) est positionné à 1. Que se passe-t-il ? (Choix unique)

- [ ] Le routeur fragmente le paquet en plusieurs morceaux
- [ ] Le routeur envoie ICMPv4 Type 3 Code 4 (Fragmentation Needed) à la source
- [ ] Le routeur transmet le paquet sans modification
- [ ] Le routeur envoie ICMPv4 Type 11 Code 0 (TTL Exceeded)

---

### Question 25
Un routeur reçoit un paquet dont le TTL vient d'atteindre 0. Quelle action effectue-t-il ? (Choix multiples - 2 réponses)

- [ ] Le routeur rejette le paquet
- [ ] Le routeur envoie ICMPv4 Type 11 Code 0 (TTL Exceeded) à la source
- [ ] Le routeur réinitialise le TTL et transmet le paquet
- [ ] Le routeur envoie ICMPv4 Type 3 Code 0 à la source

---

### Question 26
Associez chaque code ICMPv6 Type 1 (Destination Unreachable) à sa description. (Choix multiples - 3 réponses)

- [ ] Code 0 : No route to destination
- [ ] Code 1 : Communication administratively prohibited
- [ ] Code 3 : Address unreachable (échec de résolution NDP)
- [ ] Code 4 : Port unreachable (utilisé par traceroute IPv6)
- [ ] Code 5 : TTL Exceeded

---

### Question 27
Quelle est la différence principale entre ICMPv4 Type 3 Code 4 et ICMPv6 Type 2 ? (Choix unique)

- [ ] ICMPv6 Type 2 est un message dédié "Packet Too Big" alors qu'en IPv4 c'est un sous-code du Type 3
- [ ] ICMPv6 Type 2 indique un TTL expiré
- [ ] Il n'y a pas de différence, les deux sont identiques
- [ ] ICMPv4 Type 3 Code 4 n'existe pas

---

### Question 28
Associez chaque type de message NDP à son numéro ICMPv6. (Choix multiples - 5 réponses)

- [ ] Type 133 : Router Solicitation (RS)
- [ ] Type 134 : Router Advertisement (RA)
- [ ] Type 135 : Neighbor Solicitation (NS)
- [ ] Type 136 : Neighbor Advertisement (NA)
- [ ] Type 137 : Redirect

---

### Question 29
Un hôte envoie un message Router Solicitation (RS). Quelle est l'adresse de destination et quel type ICMPv6 est utilisé ? (Choix unique)

- [ ] Destination FF02::1 (tous les nœuds), Type 133
- [ ] Destination FF02::2 (tous les routeurs), Type 133
- [ ] Destination FF02::1 (tous les nœuds), Type 134
- [ ] Destination FF02::2 (tous les routeurs), Type 134

---

### Question 30
Un routeur envoie un Router Advertisement (RA) avec les flags M=0 et O=1. Quelle méthode d'allocation IPv6 est configurée ? (Choix unique)

- [ ] SLAAC Only (pas de serveur DHCPv6 nécessaire)
- [ ] SLAAC + DHCPv6 Stateless (SLAAC pour l'adresse, DHCPv6 pour DNS)
- [ ] DHCPv6 Stateful (le serveur DHCPv6 attribue l'adresse complète)
- [ ] Configuration manuelle uniquement

---

---

## RÉPONSES ET EXPLICATIONS

### Question 1
**Réponse correcte :** B (Classe B)

**Explication :**
L'adresse `172.25.100.50` commence par 172, qui se situe dans la plage 128-191. Cette plage correspond à la **Classe B** :
- Classe A : 1-126
- **Classe B : 128-191**
- Classe C : 192-223
- Classe D : 224-239 (multicast)

Le premier octet (172) détermine la classe. Les adresses de Classe B ont un masque par défaut de /16 (255.255.0.0).

---

### Question 2
**Réponse correcte :** A, C, E

**Explication :**
Selon **RFC 1918**, les trois plages d'adresses privées sont :
- **10.0.0.0 - 10.255.255.255** (Classe A : 10.0.0.0/8)
- **172.16.0.0 - 172.31.255.255** (Classe B : 172.16.0.0/12)
- **192.168.0.0 - 192.168.255.255** (Classe C : 192.168.0.0/16)

**Pourquoi les autres sont incorrectes :**
- 169.254.0.0/16 : adresses **APIPA** (link-local), pas RFC 1918
- 172.0.0.0 - 172.255.255.255 : trop large, seul 172.16.0.0 à 172.31.255.255 est privé
- 127.0.0.0/8 : adresses de **bouclage (loopback)**, pas privées

---

### Question 3
**Réponse correcte :** B (192.168.10.64/26)

**Explication :**
**Méthode Magic Number :**
1. Masque /26 = 255.255.255.**192**
2. Magic Number = 256 - 192 = **64**
3. Multiples de 64 : 0, 64, 128, 192
4. 75 est compris entre **64** et 128

**Donc le sous-réseau est 192.168.10.64/26 :**
- Réseau : 192.168.10.64
- Première IP utilisable : 192.168.10.65
- Dernière IP utilisable : 192.168.10.126
- Broadcast : 192.168.10.127

---

### Question 4
**Réponse correcte :** B (30 hôtes)

**Explication :**
**Formule :** Nombre d'hôtes utilisables = `2^n - 2`
- n = nombre de bits hôte
- /27 signifie 27 bits réseau, donc **32 - 27 = 5 bits hôte**
- Calcul : `2^5 - 2 = 32 - 2 = 30 hôtes`

Le `-2` exclut :
- L'adresse de réseau (tous les bits hôte à 0)
- L'adresse de broadcast (tous les bits hôte à 1)

**Tableau de référence :**
- /27 → 5 bits → 30 hôtes
- /28 → 4 bits → 14 hôtes
- /29 → 3 bits → 6 hôtes
- /30 → 2 bits → 2 hôtes

---

### Question 5
**Réponse correcte :** B (/25)

**Explication :**
Pour 120 hôtes, on doit trouver le masque qui fournit **au moins** 120 adresses utilisables.

**Vérification des options :**
- /27 : 2^5 - 2 = **30 hôtes** ❌ (insuffisant)
- /26 : 2^6 - 2 = **62 hôtes** ❌ (insuffisant)
- **/25 : 2^7 - 2 = 126 hôtes** ✅ (suffisant)
- /24 : 2^8 - 2 = **254 hôtes** ✅ (mais gaspille des adresses)

**Réponse :** /25 est le masque le **plus approprié** (juste assez d'adresses sans gaspillage excessif).

---

### Question 6
**Réponse correcte :** B (A: /26, B: /27, C: /28)

**Explication :**
**Principe VLSM :** Allouer le masque juste nécessaire pour chaque réseau.

**Calculs :**
- **Réseau A : 50 hôtes**
  - /26 : 2^6 - 2 = **62 hôtes** ✅
  - /27 : 2^5 - 2 = 30 hôtes ❌ (insuffisant)

- **Réseau B : 25 hôtes**
  - /27 : 2^5 - 2 = **30 hôtes** ✅
  - /28 : 2^4 - 2 = 14 hôtes ❌

- **Réseau C : 10 hôtes**
  - /28 : 2^4 - 2 = **14 hôtes** ✅
  - /29 : 2^3 - 2 = 6 hôtes ❌

**Allocation optimale :** A: /26, B: /27, C: /28

---

### Question 7
**Réponse correcte :** A (/19 avec 8 190 hôtes)

**Explication :**
**Besoin :** 8 sous-réseaux à partir de /16

**Formule :** 2^n sous-réseaux (n = bits empruntés)
- 2^3 = 8 sous-réseaux → emprunter **3 bits**
- Nouveau masque : /16 + 3 = **/19**

**Hôtes par sous-réseau :**
- Bits hôte restants : 32 - 19 = 13 bits
- Hôtes : 2^13 - 2 = **8 192 - 2 = 8 190 hôtes**

**Pourquoi pas les autres :**
- /20 : 2^4 = 16 sous-réseaux (trop)
- /21 : 2^5 = 32 sous-réseaux (trop)
- /24 : 2^8 = 256 sous-réseaux (trop)

---

### Question 8
**Réponse correcte :** A, C

**Explication :**
L'**agrégation de routes (route summarization)** consiste à regrouper plusieurs réseaux contigus en une seule route de résumé.

**Affirmations correctes :**
- ✅ **A** : Elle **réduit** la taille des tables de routage (moins d'entrées)
- ✅ **C** : Elle **regroupe** plusieurs réseaux en une seule route

**Affirmations incorrectes :**
- ❌ B : Elle fonctionne avec le routage **classless** (CIDR), pas classful
- ❌ D : Elle **réduit** le nombre d'entrées, ne l'augmente pas

**Exemple :**
```
Avant : 192.168.0.0/24, 192.168.1.0/24, 192.168.2.0/24, 192.168.3.0/24
Après : 192.168.0.0/22 (une seule entrée)
```

---

### Question 9
**Réponse correcte :** B (172.16.64.0 - 172.16.127.255)

**Explication :**
**Segmentation de 172.16.0.0/16 en /18 :**
- /18 emprunte 2 bits (18 - 16 = 2)
- 2^2 = **4 sous-réseaux**

**Calcul du Magic Number :**
- Masque /18 = 255.255.**192**.0
- Magic Number = 256 - 192 = **64**
- Incrément sur le **troisième octet**

**Les 4 sous-réseaux :**
1. 172.16.**0**.0 - 172.16.**63**.255
2. **172.16.64.0 - 172.16.127.255** ✅ (deuxième sous-réseau)
3. 172.16.128.0 - 172.16.191.255
4. 172.16.192.0 - 172.16.255.255

---

### Question 10
**Réponse correcte :** A, B, C

**Explication :**
**Adresses spéciales IPv4 :**

✅ **127.0.0.1** : Adresse de **bouclage (loopback)**
- Utilisée pour tester la pile TCP/IP locale
- Les paquets ne quittent jamais l'hôte

✅ **169.254.0.0/16** : Adresse **APIPA (link-local)**
- Attribuée automatiquement si aucun serveur DHCP
- Communication limitée au segment local

✅ **0.0.0.0/0** : **Route par défaut**
- Représente "toutes les destinations"
- Gateway of Last Resort

**Pourquoi les autres sont incorrectes :**
- ❌ 224.0.0.0/4 : adresses **multicast**, pas broadcast
- ❌ 255.255.255.255 : **limited broadcast**, pas multicast

---

### Question 11
**Réponse correcte :** A (2001:db8:0:42::100)

**Explication :**
**Règles de compression IPv6 :**
1. **Règle 1 :** Supprimer les zéros de tête dans chaque groupe
2. **Règle 2 :** Remplacer **une seule séquence** de groupes consécutifs de zéros par `::`

**Application :**
```
Forme originale : 2001:0db8:0000:0042:0000:0000:0000:0100

Étape 1 (supprimer zéros de tête) :
2001:db8:0:42:0:0:0:100

Étape 2 (utiliser ::) :
2001:db8:0:42::100
```

**Pourquoi les autres sont incorrectes :**
- ❌ B : `::` utilisé **deux fois** (invalide)
- ❌ C : Non compressée (valide mais pas la forme la plus compressée)
- ❌ D : Garde les zéros de tête (0db8), pas optimal

---

### Question 12
**Réponse correcte :** A (FE80:0000:0000:0000:0000:0000:0000:0001)

**Explication :**
Pour **étendre** une adresse compressée :
1. Compter les groupes présents : FE80 et 1 = **2 groupes**
2. Calcul : 8 groupes total - 2 présents = **6 groupes manquants**
3. Remplacer `::` par **6 groupes de 0000**

**Résultat :**
```
FE80::1
    ↓
FE80:0000:0000:0000:0000:0000:0000:0001
```

**Structure d'une Link-Local :**
- 10 bits : 1111 1110 10 (FE80)
- 54 bits : tous à zéro
- 64 bits : Interface ID

---

### Question 13
**Réponse correcte :** A (48 bits Global Routing Prefix, 16 bits Subnet ID, 64 bits Interface ID)

**Explication :**
**Structure standard d'une GUA (Global Unicast Address) :**

```
|     48 bits      |  16 bits  |        64 bits         |
+------------------+-----------+------------------------+
| Global Prefix    | Subnet ID |     Interface ID       |
| 2001:db8:acad    |  (0-FFFF) |   (hôte unique)        |
+------------------+-----------+------------------------+
     /48                /64            Total /128
```

**Exemple concret :**
- Organisation reçoit : `2001:db8:acad::/48`
- Peut créer : **65 536 sous-réseaux** /64 (2^16)
- Sous-réseau 1 : `2001:db8:acad:0001::/64`
- Sous-réseau 2 : `2001:db8:acad:0002::/64`
- etc.

**Pourquoi /64 est standard :**
- Compatible avec **SLAAC**
- Compatible avec **EUI-64**
- Chaque sous-réseau a 2^64 = 18 trillions d'hôtes

---

### Question 14
**Réponse correcte :** A, B

**Explication :**
**Analyse de l'adresse `2001:db8:acad:1a2b::10/64` :**

```
2001:db8:acad : 1a2b : 0000:0000:0000:0010
      |           |              |
   48 bits     16 bits        64 bits
  (Global)    (Subnet)     (Interface)
```

✅ **A** : Global Routing Prefix = `2001:db8:acad` (48 bits = 3 groupes de 16 bits)

✅ **B** : Subnet ID = `1a2b` (16 bits = 1 groupe)

**Pourquoi les autres sont incorrectes :**
- ❌ C : L'Interface ID est `0000:0000:0000:0010` (64 bits), pas seulement `0010`
- ❌ D : Le préfixe complet est `/64`, pas `/48`

---

### Question 15
**Réponse correcte :** A, B, D

**Explication :**
**Avantages de la configuration manuelle des Link-Local sur routeurs :**

✅ **A** : Adresses EUI-64 automatiques sont complexes
- Auto : `FE80::021A:2BFF:FE3C:4D5E`
- Manuel : `FE80::1`

✅ **B** : Permet d'utiliser la même LLA sur toutes les interfaces
```
R1(config-if)# interface g0/0
R1(config-if)# ipv6 address fe80::1 link-local

R1(config-if)# interface g0/1
R1(config-if)# ipv6 address fe80::1 link-local
```

✅ **D** : Simplifie la configuration client
- Passerelle par défaut : `FE80::1` (facile à mémoriser)
- Cohérence sur tous les VLANs

**Pourquoi les autres sont incorrectes :**
- ❌ C : Aucun impact sur la vitesse de routage
- ❌ E : Les LLA automatiques fonctionnent parfaitement

---

### Question 16
**Réponse correcte :** B (Utilisée comme passerelle par défaut)

**Explication :**
**Rôle principal de la LLA du routeur :**

Les hôtes IPv6 utilisent l'**adresse link-local du routeur** comme **passerelle par défaut** :

```
Client Windows :
IPv6 Address : 2001:db8:acad:1::10/64
Default Gateway : FE80::1  ← Link-Local du routeur
```

**Pourquoi la LLA et pas la GUA ?**
- La LLA est **stable** (ne change pas si la GUA change)
- **Simplifie** la configuration (même LLA sur toutes les interfaces)
- **Fonctionne** même sans GUA configurée

**Autres rôles de la LLA :**
- Protocoles de routage (OSPFv3, EIGRP IPv6)
- NDP (Neighbor Discovery Protocol)
- Communication locale sur le lien

**Pourquoi les autres sont incorrectes :**
- ❌ A : IPv6 n'a **pas de broadcast**
- ❌ C : LLA n'est **pas routable** (limitée au lien local)
- ❌ D : LLA est de **couche 3**, MAC est **couche 2**

---

### Question 17
**Réponse correcte :** A (FF02::1:FF00:6700)

**Explication :**
**Calcul de l'adresse solicited-node multicast :**

**Formule :** `FF02::1:FF[24 derniers bits de l'adresse unicast]`

**Adresse unicast :** `2001:db8:acad:1:a8bb:ccff:fe00:6700`

**Étapes :**
1. Identifier les **24 derniers bits** (6 derniers chiffres hexa) : `00:6700`
2. Préfixe solicited-node : `FF02::1:FF`
3. Résultat : `FF02::1:FF00:6700`

**Forme complète :**
```
FF02:0000:0000:0000:0000:0001:FF00:6700
                              └─ 24 bits
```

**Utilisation :**
- Messages **Neighbor Solicitation (NS)** de NDP
- Résolution d'adresse (équivalent ARP IPv4)
- Duplicate Address Detection (DAD)

---

### Question 18
**Réponse correcte :** A (33:33:FF:3C:4D:5E)

**Explication :**
**Mapping IPv6 multicast → MAC multicast :**

**Format :** `33:33:[4 derniers octets de l'IPv6 multicast]`

**IPv6 multicast :** `FF02::1:FF3C:4D5E`

**Forme complète :**
```
FF02:0000:0000:0000:0000:0001:FF3C:4D5E
                              └──────┘
                         4 derniers octets
```

**Extraction des 4 derniers octets :**
- `00:01:FF:3C:4D:5E` → prendre les 4 derniers : `FF:3C:4D:5E`

**MAC multicast résultante :**
```
33:33:FF:3C:4D:5E
└─┘ └──────────┘
 |       |
 |       └─ 4 derniers octets IPv6
 |
 └─ Préfixe multicast IPv6
```

**Comparaison avec IPv4 :**
- IPv4 multicast MAC : `01:00:5E:[23 derniers bits]`
- IPv6 multicast MAC : `33:33:[4 derniers octets]`

---

### Question 19
**Réponse correcte :** D (65 536 sous-réseaux)

**Explication :**
**Segmentation /48 → /64 :**

**Calcul :**
- Préfixe reçu : `/48` (48 bits fixes)
- Sous-réseaux créés : `/64` (64 bits fixes)
- **Subnet ID** = 64 - 48 = **16 bits**

**Nombre de sous-réseaux :**
- 2^16 = **65 536 sous-réseaux /64**

**Exemple pratique :**
```
Organisation : 2001:db8:acad::/48

Subnet ID (16 bits) : 0x0000 à 0xFFFF

Sous-réseaux :
- 2001:db8:acad:0000::/64
- 2001:db8:acad:0001::/64
- 2001:db8:acad:0002::/64
  ...
- 2001:db8:acad:FFFF::/64

Total : 65 536 sous-réseaux
```

**Rappel :**
- Chaque sous-réseau /64 peut contenir **2^64 hôtes** (18 trillions)
- /64 est le standard pour un segment réseau IPv6

---

### Question 20
**Réponse correcte :** A, B, C

**Explication :**
**Adresses multicast IPv6 well-known (permanentes) :**

✅ **FF02::1** : **All nodes** (tous les nœuds IPv6 du lien local)
- Tous les périphériques IPv6 écoutent cette adresse
- Équivalent du broadcast IPv4 pour le lien local
- Utilisé par : Router Advertisement (RA)

✅ **FF02::2** : **All routers** (tous les routeurs IPv6 du lien local)
- Seuls les routeurs écoutent cette adresse
- Utilisé par : Router Solicitation (RS)

✅ **FF02::5** : **All OSPFv3 routers**
- Routeurs OSPFv3 écoutent cette adresse
- Similaire à 224.0.0.5 en IPv4

**Pourquoi les autres sont incorrectes :**
- ❌ D : FF02::1:2 = serveurs/relais **DHCPv6**, pas "tous les hôtes globaux"
- ❌ E : FF02::A = routeurs **EIGRP IPv6**, pas serveurs DHCP

**Autres adresses importantes :**
- `FF02::6` : OSPFv3 DR/BDR
- `FF02::9` : Routeurs RIPng
- `FF02::A` : Routeurs EIGRP IPv6
- `FF02::1:2` : Serveurs/relais DHCPv6

---

### Question 21
**Réponse correcte :** A (ICMPv4 Type 3 Code 0)

**Explication :**
**Scénario :** Routeur n'a **aucune route** vers le réseau de destination

**Message ICMP :** Type 3 Code 0 - **Network Unreachable**

**Processus :**
1. Client envoie paquet vers 10.1.1.10
2. Routeur consulte sa table de routage
3. **Aucune route** vers 10.1.1.0/24 (pas de route spécifique, pas de route par défaut)
4. Routeur **rejette** le paquet
5. Routeur envoie **ICMP Type 3 Code 0** à la source

**Différence avec Code 1 (Host Unreachable) :**
- **Code 0** : pas de route vers le **réseau**
- **Code 1** : route vers le réseau existe, mais l'**hôte** ne répond pas (ARP échoue)

**Type 3 - Destination Unreachable - Codes importants :**
- Code 0 : Network Unreachable
- Code 1 : Host Unreachable
- Code 3 : Port Unreachable
- Code 4 : Fragmentation Needed (DF set)

---

### Question 22
**Réponse correcte :** B (ICMPv4 Type 3 Code 1)

**Explication :**
**Scénario :** Le routeur a une route vers le réseau, mais l'hôte ne répond pas aux ARP

**Message ICMP :** Type 3 Code 1 - **Host Unreachable**

**Processus détaillé :**
1. Routeur reçoit un paquet pour 192.168.1.50
2. Routeur **a une route** vers 192.168.1.0/24 (interface connectée)
3. Routeur doit résoudre l'adresse MAC avec **ARP Request**
4. Routeur envoie plusieurs ARP Request (broadcast FF:FF:FF:FF:FF:FF)
5. **Aucune réponse ARP** (hôte éteint, déconnecté, ou n'a pas l'IP)
6. Routeur **abandonne** après timeout
7. Routeur envoie **ICMP Type 3 Code 1** à la source

**Différence avec Code 0 :**
- **Code 0** : **Pas de route** vers le réseau (problème de routage)
- **Code 1** : Route existe, mais **hôte inaccessible** (problème au niveau hôte)

**Causes possibles de Host Unreachable :**
- Hôte est éteint
- Câble réseau déconnecté
- Adresse IP incorrecte ou non configurée
- Firewall bloque ARP (rare)

---

### Question 23
**Réponse correcte :** A, B

**Explication :**
**Fonctionnement de traceroute :**

✅ **A - ICMPv4 Type 11 Code 0 (TTL Exceeded)** :
- Traceroute envoie des paquets avec **TTL croissant** (1, 2, 3, ...)
- Chaque routeur le long du chemin **décrémente le TTL**
- Quand TTL atteint 0, le routeur renvoie **ICMP Type 11 Code 0**
- Permet d'identifier **chaque saut** du chemin

✅ **B - ICMPv4 Type 3 Code 3 (Port Unreachable)** :
- Quand le paquet atteint la **destination**
- Traceroute utilise des paquets **UDP** vers un **port élevé non utilisé** (33434+)
- La destination répond **ICMP Type 3 Code 3**
- Indique que la destination est atteinte

**Séquence traceroute :**
```
1. TTL=1 → Routeur 1 → ICMP Type 11 Code 0
2. TTL=2 → Routeur 2 → ICMP Type 11 Code 0
3. TTL=3 → Routeur 3 → ICMP Type 11 Code 0
...
N. TTL=N → Destination → ICMP Type 3 Code 3 (Port Unreachable)
```

**Pourquoi pas C et D (ping) :**
- Type 8 (Echo Request) et Type 0 (Echo Reply) sont utilisés par **ping**, pas traceroute
- Traceroute utilise TTL/UDP, pas Echo Request

---

### Question 24
**Réponse correcte :** B (ICMPv4 Type 3 Code 4)

**Explication :**
**Scénario :** Paquet trop grand + bit DF (Don't Fragment) = 1

**Message ICMP :** Type 3 Code 4 - **Fragmentation Needed and DF set**

**Processus détaillé :**
1. Paquet de 1500 octets arrive au routeur
2. Lien suivant a MTU de **1400 octets**
3. Paquet doit être **fragmenté**, mais bit **DF = 1** (Don't Fragment)
4. Routeur **ne peut pas fragmenter**
5. Routeur **rejette le paquet**
6. Routeur envoie **ICMP Type 3 Code 4** à la source avec le **MTU du lien**
7. Source **réduit** la taille de ses paquets

**Utilisation :** **Path MTU Discovery (PMTUD)**
- Permet de déterminer le plus petit MTU sur le chemin
- Évite la fragmentation en cours de route
- Améliore les performances

**Message ICMP Type 3 Code 4 contient :**
- **Next-Hop MTU** : la taille maximale que le routeur peut accepter

**Différence IPv4 vs IPv6 :**
- **IPv4** : Type 3 Code 4 (Fragmentation Needed)
- **IPv6** : Type 2 (**Packet Too Big**) - message dédié

---

### Question 25
**Réponse correcte :** A, B

**Explication :**
**Scénario :** TTL (Time To Live) atteint 0

✅ **A - Le routeur rejette le paquet** :
- Quand TTL = 0, le paquet **ne peut plus être transféré**
- Le routeur **drop** (jette/rejette) le paquet
- Empêche les **boucles de routage infinies**

✅ **B - Le routeur envoie ICMP Type 11 Code 0** :
- Message : **Time Exceeded - TTL Exceeded in Transit**
- Envoyé à l'**adresse source** du paquet rejeté
- Informe la source que le paquet a été rejeté

**Processus détaillé :**
```
1. Routeur reçoit paquet avec TTL=1
2. Routeur décrémente TTL : 1 - 1 = 0
3. TTL est maintenant 0 → paquet ne peut pas être transmis
4. Routeur REJETTE le paquet (action A)
5. Routeur envoie ICMP Type 11 Code 0 à la source (action B)
```

**Pourquoi les autres sont incorrectes :**
- ❌ C : Le routeur **ne réinitialise jamais le TTL** (ce serait une boucle infinie)
- ❌ D : Type 3 Code 0 = Network Unreachable (problème différent)

**Utilisation du Type 11 Code 0 :**
- **Traceroute** : découverte du chemin réseau
- **Détection de boucles** de routage
- **Diagnostic** réseau

**Valeur initiale du TTL :**
- Windows : 128
- Linux : 64
- Cisco : 255

---

### Question 26
**Réponse correcte :** A, B, C (et D aussi, mais limité à 3 réponses selon consigne)

**Explication :**
**ICMPv6 Type 1 - Destination Unreachable - Codes importants :**

✅ **Code 0 : No route to destination**
- Le routeur n'a **aucune route** vers la destination
- Équivalent de ICMPv4 Type 3 Code 0/1
- Problème de routage

✅ **Code 1 : Communication administratively prohibited**
- Communication **bloquée** par une ACL ou un firewall
- Politique de sécurité refuse le trafic
- Équivalent de ICMPv4 Type 3 Code 13

✅ **Code 3 : Address unreachable**
- La résolution d'adresse **NDP a échoué**
- Équivalent de "ARP échoue" en IPv4
- Hôte ne répond pas aux Neighbor Solicitation

✅ **Code 4 : Port unreachable**
- Le port de destination est **fermé** ou non écouté
- Utilisé par **traceroute IPv6**
- Équivalent de ICMPv4 Type 3 Code 3

**Pourquoi E est incorrect :**
- ❌ Code 5 n'existe pas dans Type 1
- TTL Exceeded = ICMPv6 **Type 3 Code 0** (pas Type 1)

**Comparaison ICMPv4 vs ICMPv6 :**
- ICMPv4 Type 3 : 14 codes différents
- ICMPv6 Type 1 : 7 codes (regroupement simplifié)

---

### Question 27
**Réponse correcte :** A (ICMPv6 Type 2 est un message dédié)

**Explication :**
**Différence de gestion du MTU entre IPv4 et IPv6 :**

**IPv4 :**
- Utilise **ICMPv4 Type 3 Code 4** : Destination Unreachable - **Fragmentation Needed (DF set)**
- C'est un **sous-code** du message "Destination Unreachable"
- Fragmentation **possible** par les routeurs intermédiaires

**IPv6 :**
- Utilise **ICMPv6 Type 2** : **Packet Too Big** (message dédié complet)
- **Pas un sous-code**, c'est un type à part entière
- Fragmentation **interdite** en cours de route (seulement par la source)

**Conséquences pratiques :**

**IPv4** :
```
- Routeur peut fragmenter les paquets (si DF=0)
- PMTUD optionnel (si DF=1)
```

**IPv6** :
```
- Routeur NE PEUT JAMAIS fragmenter
- PMTUD OBLIGATOIRE
- Si paquet trop grand → ICMP Type 2 + rejet
```

**Message ICMPv6 Type 2 contient :**
- **MTU du lien** : taille maximale acceptée

**Pourquoi c'est important :**
- IPv6 **simplifie** le traitement par les routeurs (pas de fragmentation)
- IPv6 **oblige** la source à découvrir le Path MTU
- Améliore les **performances** globales

---

### Question 28
**Réponse correcte :** Toutes (A, B, C, D, E)

**Explication :**
**Les 5 types de messages NDP (Neighbor Discovery Protocol) :**

✅ **Type 133 : Router Solicitation (RS)**
- **Envoyé par** : Hôtes
- **Destination** : FF02::2 (tous les routeurs)
- **Rôle** : Demander aux routeurs de s'annoncer immédiatement
- **Quand** : Au démarrage ou connexion réseau

✅ **Type 134 : Router Advertisement (RA)**
- **Envoyé par** : Routeurs
- **Destination** : FF02::1 (tous les nœuds) ou unicast
- **Rôle** : Annoncer la présence du routeur et fournir infos réseau
- **Contenu** : Préfixe, flags M/O, MTU, durée de vie

✅ **Type 135 : Neighbor Solicitation (NS)**
- **Envoyé par** : Hôtes ou routeurs
- **Destination** : Solicited-node multicast (FF02::1:FF[24 bits])
- **Rôle** : Résoudre IPv6 → MAC (équivalent ARP Request)
- **Aussi utilisé pour** : DAD, NUD

✅ **Type 136 : Neighbor Advertisement (NA)**
- **Envoyé par** : Hôte ou routeur qui possède l'adresse
- **Destination** : Unicast (réponse) ou FF02::1 (annonce)
- **Rôle** : Répondre à NS (équivalent ARP Reply)

✅ **Type 137 : Redirect**
- **Envoyé par** : Routeur
- **Destination** : Unicast vers l'hôte concerné
- **Rôle** : Informer qu'un meilleur chemin existe

**Résumé :**
```
RS (133) : "Y a-t-il des routeurs ?"
RA (134) : "Je suis un routeur, voici les infos"
NS (135) : "Qui a cette IPv6 ? Quelle est votre MAC ?"
NA (136) : "C'est moi, voici ma MAC"
Redirect (137) : "Utilisez ce routeur pour cette destination"
```

**NDP remplace en IPv4 :**
- ARP (NS/NA)
- ICMP Router Discovery (RS/RA)
- ICMP Redirect (Redirect)

---

### Question 29
**Réponse correcte :** B (Destination FF02::2, Type 133)

**Explication :**
**Message Router Solicitation (RS) :**

**Type ICMPv6 :** 133

**Destination :** `FF02::2` (All routers - tous les routeurs du lien local)

**Pourquoi FF02::2 ?**
- Les hôtes veulent **contacter les routeurs**
- `FF02::2` est l'adresse multicast écoutée par **tous les routeurs IPv6**
- Seuls les **routeurs** traitent ce message

**Processus complet :**
```
1. Hôte démarre ou se connecte au réseau
2. Hôte génère une Link-Local (FE80::/10)
3. Hôte envoie RS (Type 133) à FF02::2
   "Y a-t-il des routeurs sur ce réseau ?"
4. Routeur(s) répond(ent) avec RA (Type 134)
   "Je suis un routeur, voici les infos de configuration"
```

**Contenu du RS :**
```
Source : FE80::[Interface ID] (link-local de l'hôte)
        ou :: (si pas encore d'adresse)
Destination : FF02::2 (tous les routeurs)
Type ICMPv6 : 133
Options : Peut inclure l'adresse MAC source
```

**Pourquoi pas les autres options :**
- ❌ FF02::1 = tous les **nœuds** (hôtes + routeurs), pas seulement routeurs
- ❌ Type 134 = **Router Advertisement** (réponse, pas la demande)

**Remarque :**
- Les routeurs envoient aussi des **RA périodiques** (non sollicités) toutes les 200 secondes par défaut
- RS permet d'obtenir un RA **immédiatement** sans attendre

---

### Question 30
**Réponse correcte :** B (SLAAC + DHCPv6 Stateless)

**Explication :**
**Analyse des flags M=0 et O=1 :**

| Flag | Valeur | Signification |
|------|--------|---------------|
| **M** (Managed) | 0 | **Ne pas utiliser DHCPv6 pour l'adresse** |
| **O** (Other) | 1 | **Utiliser DHCPv6 pour d'autres informations** |

**Méthode résultante : SLAAC + DHCPv6 Stateless**

**Processus complet :**

1. **Pour l'adresse IPv6 (M=0) :**
   - Hôte utilise **SLAAC** (Stateless Address Autoconfiguration)
   - Préfixe du RA (ex: 2001:db8:acad:1::/64)
   - Interface ID généré (EUI-64 ou aléatoire)
   - Résultat : `2001:db8:acad:1:[Interface ID]/64`

2. **Pour les autres infos (O=1) :**
   - Hôte contacte serveur **DHCPv6 Stateless**
   - Obtient : **DNS**, nom de domaine, NTP, etc.
   - Le serveur DHCPv6 **ne gère pas** les adresses (stateless)

**Configuration routeur :**
```
Router(config-if)# no ipv6 nd managed-config-flag  (M=0)
Router(config-if)# ipv6 nd other-config-flag       (O=1)
```

**Comparaison des 3 méthodes :**

| Méthode | M | O | Adresse | DNS | Serveur DHCPv6 |
|---------|---|---|---------|-----|----------------|
| SLAAC Only | 0 | 0 | SLAAC | ❌ | Non requis |
| **SLAAC + DHCPv6 Stateless** | **0** | **1** | **SLAAC** | **✅** | **Requis (stateless)** |
| DHCPv6 Stateful | 1 | x | DHCPv6 | ✅ | Requis (stateful) |

**Avantages de cette méthode :**
- ✅ Simplicité de SLAAC (pas de gestion d'état des adresses)
- ✅ **DNS automatique** (résout le principal problème de SLAAC seul)
- ✅ **Méthode recommandée** pour la plupart des entreprises

**Utilisation typique :**
- Réseaux d'entreprise nécessitant DNS automatique
- Évite la configuration manuelle DNS sur chaque client
- Combine le meilleur de SLAAC et DHCPv6

---

**Félicitations !** Vous avez terminé ce QCM Checkpoint.

**Barème de réussite :**
- 23/30 ou plus (≥75%) : ✅ **Réussi** - Vous maîtrisez bien les concepts
- 20-22/30 (67-73%) : ⚠️ **À revoir** - Revoir les points faibles
- Moins de 20/30 (<67%) : ❌ **À refaire** - Étudier à nouveau les modules

**Points à réviser selon vos erreurs :**
- **Module 11** : Subnetting, VLSM, classes, adresses spéciales
- **Module 12** : Compression, GUA/LLA, solicited-node, segmentation
- **Module 13** : Codes ICMP, NDP, méthodes d'allocation IPv6
