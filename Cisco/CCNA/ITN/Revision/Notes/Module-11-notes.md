# Module 11 - Adressage IPv4

## Table des matières
1. [Types d'adresses IPv4](#types-adresses)
2. [Adresses unicast](#unicast)
3. [Adresses de réseau et de broadcast](#reseau-broadcast)
4. [Classes d'adresses IPv4](#classes)
5. [Adresses publiques et privées](#publiques-privees)
6. [Adresses spéciales](#adresses-speciales)
7. [CIDR - Classless Inter-Domain Routing](#cidr)
8. [Subnetting](#subnetting)
9. [VLSM - Variable Length Subnet Masking](#vlsm)
10. [Conception d'un plan d'adressage](#plan-adressage)
11. [Calculs de sous-réseaux](#calculs)

---

## 1. Types d'adresses IPv4 {#types-adresses}

### Vue d'ensemble
Il existe trois types principaux d'adresses IPv4 :

| Type | Description | Portée |
|------|-------------|--------|
| **Unicast** | Communication **un-à-un** (1 émetteur → 1 destinataire) | Adresse d'un hôte spécifique |
| **Broadcast** | Communication **un-à-tous** (1 émetteur → tous les hôtes du réseau) | Tous les hôtes d'un segment |
| **Multicast** | Communication **un-à-plusieurs** (1 émetteur → groupe d'hôtes abonnés) | Groupe multicast (224.0.0.0/4) |

---

## 2. Adresses unicast {#unicast}

### Définition
Une **adresse unicast** identifie **un seul hôte** sur un réseau.
- Utilisée pour la communication point-à-point
- Chaque interface réseau a une adresse unicast unique

### Composition d'une adresse IPv4
Une adresse IPv4 = **32 bits** divisée en deux parties :

```
[   Partie Réseau   ] [  Partie Hôte  ]
     Network ID            Host ID
```

**Masque de sous-réseau** : détermine la frontière entre la partie réseau et la partie hôte
- Notation décimale : `255.255.255.0`
- Notation CIDR : `/24`

### Exemple
```
Adresse IP :     192.168.10.15
Masque :         255.255.255.0 (/24)

Partie réseau :  192.168.10.0
Partie hôte :    15
```

---

## 3. Adresses de réseau et de broadcast {#reseau-broadcast}

### Adresse de réseau (Network Address)
- **Premier** élément d'un sous-réseau
- Tous les bits de la partie hôte = **0**
- Identifie le réseau lui-même
- **Non assignable** à un hôte

**Exemple** : 192.168.10.0/24
```
192.168.10.0        # Adresse de réseau
```

### Adresse de broadcast (Broadcast Address)
- **Dernier** élément d'un sous-réseau
- Tous les bits de la partie hôte = **1**
- Utilisée pour envoyer à **tous les hôtes** du réseau
- **Non assignable** à un hôte

**Exemple** : 192.168.10.255/24
```
192.168.10.255      # Adresse de broadcast
```

### Adresses d'hôtes utilisables
```
Réseau :              192.168.10.0/24
Première adresse :    192.168.10.1     (assignable)
Dernière adresse :    192.168.10.254   (assignable)
Broadcast :           192.168.10.255   (non assignable)

Nombre d'hôtes :      2^8 - 2 = 254 hôtes utilisables
```

**Formule** : Nombre d'hôtes = `2^n - 2`
- `n` = nombre de bits de la partie hôte
- `-2` : exclure l'adresse de réseau et de broadcast

---

## 4. Classes d'adresses IPv4 {#classes}

### Système de classes (obsolète mais utile pour comprendre)

Le système de **classes** divisait l'espace d'adressage IPv4 en 5 classes (A, B, C, D, E) basées sur les premiers bits.

| Classe | Premier octet | Masque par défaut | Plage d'adresses | Utilisation |
|--------|---------------|-------------------|------------------|-------------|
| **A** | 1-126 | /8 (255.0.0.0) | 1.0.0.0 - 126.255.255.255 | Très grands réseaux (16M hôtes) |
| **B** | 128-191 | /16 (255.255.0.0) | 128.0.0.0 - 191.255.255.255 | Réseaux moyens (65K hôtes) |
| **C** | 192-223 | /24 (255.255.255.0) | 192.0.0.0 - 223.255.255.255 | Petits réseaux (254 hôtes) |
| **D** | 224-239 | N/A | 224.0.0.0 - 239.255.255.255 | Multicast |
| **E** | 240-255 | N/A | 240.0.0.0 - 255.255.255.255 | Réservé (expérimental) |

### Détails par classe

#### Classe A
- **Bits de début** : `0xxxxxxx` (premier bit = 0)
- **Masque** : /8 (255.0.0.0)
- **Format** : `Réseau.Hôte.Hôte.Hôte`
- **Réseaux disponibles** : 126 (1-126)
- **Hôtes par réseau** : 16 777 214 (2^24 - 2)
- **Exemple** : 10.0.0.0/8

⚠️ **Note** : 0.0.0.0 et 127.0.0.0 ne sont pas utilisés pour des réseaux de classe A

#### Classe B
- **Bits de début** : `10xxxxxx` (premiers bits = 10)
- **Masque** : /16 (255.255.0.0)
- **Format** : `Réseau.Réseau.Hôte.Hôte`
- **Réseaux disponibles** : 16 384
- **Hôtes par réseau** : 65 534 (2^16 - 2)
- **Exemple** : 172.16.0.0/16

#### Classe C
- **Bits de début** : `110xxxxx` (premiers bits = 110)
- **Masque** : /24 (255.255.255.0)
- **Format** : `Réseau.Réseau.Réseau.Hôte`
- **Réseaux disponibles** : 2 097 152
- **Hôtes par réseau** : 254 (2^8 - 2)
- **Exemple** : 192.168.1.0/24

#### Classe D (Multicast)
- **Plage** : 224.0.0.0 - 239.255.255.255
- Utilisée pour la **multidiffusion** (multicast)
- Pas d'hôtes individuels
- Exemples :
  - `224.0.0.1` : Tous les hôtes du sous-réseau local
  - `224.0.0.2` : Tous les routeurs du sous-réseau local
  - `224.0.0.5` : Routeurs OSPF
  - `224.0.0.6` : Routeurs OSPF désignés
  - `224.0.0.9` : Routeurs RIPv2
  - `224.0.0.10` : Routeurs EIGRP

#### Classe E (Expérimentale)
- **Plage** : 240.0.0.0 - 255.255.255.255
- Réservée pour usage expérimental
- Non utilisée sur Internet

---

## 5. Adresses publiques et privées {#publiques-privees}

### Adresses publiques (Public IP)
- **Routables sur Internet**
- **Uniques mondialement**
- Attribuées par les **RIR (Regional Internet Registries)** :
  - ARIN (Amérique du Nord)
  - RIPE NCC (Europe, Moyen-Orient)
  - APNIC (Asie-Pacifique)
  - LACNIC (Amérique Latine)
  - AFRINIC (Afrique)

### Adresses privées (Private IP) - RFC 1918

Les **adresses privées** sont réservées pour une utilisation **interne** et ne sont **pas routables sur Internet**.

| Classe | Plage d'adresses privées | Masque par défaut | Nombre de réseaux |
|--------|-------------------------|-------------------|-------------------|
| **A** | 10.0.0.0 - 10.255.255.255 | /8 | 1 réseau de classe A |
| **B** | 172.16.0.0 - 172.31.255.255 | /12 | 16 réseaux de classe B |
| **C** | 192.168.0.0 - 192.168.255.255 | /16 | 256 réseaux de classe C |

**Utilisation** :
- Réseaux locaux (LAN)
- Réseaux d'entreprise
- Réseaux domestiques
- ✅ **Doivent utiliser NAT** pour accéder à Internet

---

## 6. Adresses spéciales {#adresses-speciales}

### Loopback (127.0.0.0/8)
- **Plage** : 127.0.0.1 - 127.255.255.254
- **Adresse la plus courante** : `127.0.0.1` (localhost)
- Utilisée pour les **tests locaux** (communication interne à l'hôte)
- Les paquets ne quittent **jamais** l'hôte

**Utilisation** :
```
ping 127.0.0.1       # Vérifier la pile TCP/IP locale
```

### Link-Local (APIPA) - 169.254.0.0/16
- **Plage** : 169.254.0.1 - 169.254.255.254
- **APIPA** : Automatic Private IP Addressing
- Attribuée automatiquement quand :
  - Aucun serveur DHCP n'est disponible
  - Configuration statique échoue
- Communication limitée au **lien local** (même segment réseau)
- **Non routable**

### Adresse par défaut (Default Route)
- **0.0.0.0/0** : route par défaut, représente "toutes les destinations"
- Utilisée dans les tables de routage comme "Gateway of Last Resort"

### Adresse dirigée (Directed Broadcast)
- Broadcast vers un **réseau spécifique distant**
- Exemple : `192.168.10.255` (broadcast du réseau 192.168.10.0/24)
- **Désactivé par défaut** sur les routeurs Cisco (sécurité)

### Adresse limitée (Limited Broadcast)
- **255.255.255.255**
- Broadcast limité au **réseau local**
- Ne traverse **jamais** un routeur
- Utilisé par DHCP Discover

---

## 7. CIDR - Classless Inter-Domain Routing {#cidr}

### Historique
- Introduit en **1993** (RFC 1519)
- Remplace le système de **classes** (classful addressing)
- Objectif : **optimiser l'utilisation des adresses IPv4**

### Principe du CIDR
Le CIDR permet d'utiliser des **masques de sous-réseau de longueur variable** (VLSM) sans respecter les limites des classes.

**Notation CIDR** : `adresse-IP/préfixe`
- Le **préfixe** indique le nombre de bits de la partie réseau
- Exemple : `192.168.10.0/24` → masque = 255.255.255.0 (24 bits à 1)

### Avantages du CIDR
- ✅ **Réduction du gaspillage d'adresses**
- ✅ **Agrégation de routes** (route summarization)
- ✅ **Tables de routage plus petites**
- ✅ **Flexibilité** dans la taille des réseaux

### Exemples de notation CIDR

| Notation CIDR | Masque de sous-réseau | Bits hôte | Nombre d'hôtes |
|---------------|----------------------|-----------|----------------|
| /8 | 255.0.0.0 | 24 | 16 777 214 |
| /16 | 255.255.0.0 | 16 | 65 534 |
| /24 | 255.255.255.0 | 8 | 254 |
| /25 | 255.255.255.128 | 7 | 126 |
| /26 | 255.255.255.192 | 6 | 62 |
| /27 | 255.255.255.224 | 5 | 30 |
| /28 | 255.255.255.240 | 4 | 14 |
| /29 | 255.255.255.248 | 3 | 6 |
| /30 | 255.255.255.252 | 2 | 2 |
| /31 | 255.255.255.254 | 1 | 2 (point-à-point uniquement) |
| /32 | 255.255.255.255 | 0 | 1 (hôte unique) |

### Agrégation de routes (Route Summarization)
**Principe** : Regrouper plusieurs réseaux en une seule route pour réduire la taille des tables de routage.

**Exemple** :
```
Réseaux individuels :
- 192.168.0.0/24
- 192.168.1.0/24
- 192.168.2.0/24
- 192.168.3.0/24

Route agrégée :
- 192.168.0.0/22 (englobe les 4 réseaux)
```

---

## 8. Subnetting {#subnetting}

### Définition
Le **subnetting** consiste à diviser un réseau en plusieurs **sous-réseaux** plus petits.

**Objectifs** :
- Segmenter un réseau pour améliorer les performances
- Réduire le domaine de broadcast
- Améliorer la sécurité (isolation des segments)
- Optimiser l'utilisation des adresses

### Principe
On **emprunte des bits** de la partie hôte pour créer des sous-réseaux.

**Formules** :
- **Nombre de sous-réseaux** : `2^n` (n = bits empruntés)
- **Nombre d'hôtes par sous-réseau** : `2^h - 2` (h = bits restants pour les hôtes)

### Exemple : Subnetting d'un réseau /24

**Réseau initial** : `192.168.10.0/24` (254 hôtes)

**Besoin** : 4 sous-réseaux

**Solution** : Emprunter **2 bits** (2^2 = 4 sous-réseaux)
- Nouveau masque : /26 (255.255.255.192)
- Hôtes par sous-réseau : 2^6 - 2 = 62

**Sous-réseaux créés** :

| Sous-réseau | Adresse réseau | Première IP | Dernière IP | Broadcast | Hôtes |
|-------------|----------------|-------------|-------------|-----------|-------|
| 1 | 192.168.10.0/26 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 | 62 |
| 2 | 192.168.10.64/26 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 | 62 |
| 3 | 192.168.10.128/26 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 | 62 |
| 4 | 192.168.10.192/26 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 | 62 |

### Méthode rapide : "Magic Number"

Le **Magic Number** (incrément) = 256 - valeur de l'octet du masque

**Exemple avec /26** :
- Masque : 255.255.255.**192**
- Magic Number : 256 - 192 = **64**
- Sous-réseaux : 0, 64, 128, 192

**Exemple avec /27** :
- Masque : 255.255.255.**224**
- Magic Number : 256 - 224 = **32**
- Sous-réseaux : 0, 32, 64, 96, 128, 160, 192, 224

---

## 9. VLSM - Variable Length Subnet Masking {#vlsm}

### Définition
**VLSM** permet d'utiliser **différents masques de sous-réseau** au sein d'un même réseau principal.

**Avantage** : Optimise l'utilisation des adresses en adaptant la taille des sous-réseaux aux besoins réels.

### Principe
- Créer des sous-réseaux de **tailles différentes**
- Allouer la taille appropriée pour chaque segment
- Éviter le gaspillage d'adresses

### Exemple de VLSM

**Réseau alloué** : `192.168.1.0/24`

**Besoins** :
- Réseau A : 100 hôtes
- Réseau B : 50 hôtes
- Réseau C : 25 hôtes
- Lien point-à-point 1 : 2 hôtes
- Lien point-à-point 2 : 2 hôtes

**Solution VLSM** :

| Réseau | Besoin | Masque | Adresse réseau | Plage utilisable | Hôtes disponibles |
|--------|--------|--------|----------------|------------------|-------------------|
| A | 100 | /25 | 192.168.1.0/25 | .1 - .126 | 126 |
| B | 50 | /26 | 192.168.1.128/26 | .129 - .190 | 62 |
| C | 25 | /27 | 192.168.1.192/27 | .193 - .222 | 30 |
| Lien 1 | 2 | /30 | 192.168.1.224/30 | .225 - .226 | 2 |
| Lien 2 | 2 | /30 | 192.168.1.228/30 | .229 - .230 | 2 |

**Adresses restantes** : 192.168.1.232/29 à 192.168.1.255 (réservées pour croissance)

### Protocoles de routage supportant VLSM
- ✅ **RIPv2** (avec classless)
- ✅ **OSPF**
- ✅ **EIGRP**
- ✅ **IS-IS**
- ✅ **BGP**
- ❌ **RIPv1** (ne supporte pas VLSM)

---

## 10. Conception d'un plan d'adressage {#plan-adressage}

### Méthodologie de planification

#### Étape 1 : Analyser le cahier des charges
- Nombre de sites/emplacements
- Nombre d'hôtes par site
- Types de périphériques (serveurs, PCs, imprimantes, IoT)
- Besoins de croissance future
- Liens WAN (point-à-point)

#### Étape 2 : Déterminer les exigences
- **Lister tous les réseaux** nécessaires
- **Estimer le nombre d'hôtes** par réseau
- **Ajouter une marge de croissance** (20-30% recommandé)
- **Ordonner par taille** (du plus grand au plus petit)

#### Étape 3 : Choisir le réseau principal
- Utiliser une plage **privée** (RFC 1918)
  - 10.0.0.0/8 : grands réseaux (millions d'hôtes)
  - 172.16.0.0/12 : réseaux moyens (centaines de milliers)
  - 192.168.0.0/16 : petits réseaux (milliers)

#### Étape 4 : Appliquer VLSM
- Commencer par le **réseau le plus grand**
- Choisir le masque approprié (2^n - 2 ≥ nombre d'hôtes requis)
- Allouer les adresses séquentiellement
- Documenter chaque allocation

#### Étape 5 : Réserver des adresses
- **Liens point-à-point** : /30 (2 hôtes)
- **Loopbacks** : /32 (1 adresse)
- **Réseaux de gestion** : petits sous-réseaux dédiés

### Exemple : Scénario complet

**Cahier des charges** :
```
Entreprise multi-sites :
- Site principal : 500 employés
- Site secondaire : 200 employés
- Succursale : 50 employés
- DMZ (serveurs) : 20 serveurs
- 3 liens WAN entre les sites
- Réseau de gestion : 10 périphériques

Réseau alloué : 172.16.0.0/16
```

**Analyse des besoins** :
1. Site principal : 500 hôtes → /23 (510 hôtes)
2. Site secondaire : 200 hôtes → /24 (254 hôtes)
3. Succursale : 50 hôtes → /26 (62 hôtes)
4. DMZ : 20 hôtes → /27 (30 hôtes)
5. Gestion : 10 hôtes → /28 (14 hôtes)
6. Lien WAN 1 : 2 hôtes → /30 (2 hôtes)
7. Lien WAN 2 : 2 hôtes → /30 (2 hôtes)
8. Lien WAN 3 : 2 hôtes → /30 (2 hôtes)

**Plan d'adressage VLSM** :

| Réseau | Masque | Adresse réseau | Plage utilisable | Broadcast |
|--------|--------|----------------|------------------|-----------|
| Site principal | /23 | 172.16.0.0/23 | 172.16.0.1 - 172.16.1.254 | 172.16.1.255 |
| Site secondaire | /24 | 172.16.2.0/24 | 172.16.2.1 - 172.16.2.254 | 172.16.2.255 |
| Succursale | /26 | 172.16.3.0/26 | 172.16.3.1 - 172.16.3.62 | 172.16.3.63 |
| DMZ | /27 | 172.16.3.64/27 | 172.16.3.65 - 172.16.3.94 | 172.16.3.95 |
| Gestion | /28 | 172.16.3.96/28 | 172.16.3.97 - 172.16.3.110 | 172.16.3.111 |
| Lien WAN 1 | /30 | 172.16.3.112/30 | 172.16.3.113 - 172.16.3.114 | 172.16.3.115 |
| Lien WAN 2 | /30 | 172.16.3.116/30 | 172.16.3.117 - 172.16.3.118 | 172.16.3.119 |
| Lien WAN 3 | /30 | 172.16.3.120/30 | 172.16.3.121 - 172.16.3.122 | 172.16.3.123 |

**Adresses réservées pour croissance** : 172.16.3.124 - 172.16.255.255

### Bonnes pratiques
- ✅ **Documenter** : créer un tableau récapitulatif
- ✅ **Cohérence** : utiliser un schéma logique (site 1 = .0, site 2 = .1, etc.)
- ✅ **Réserver** : prévoir de la place pour la croissance
- ✅ **Standardiser** : utiliser les mêmes masques pour des réseaux similaires (si possible)
- ✅ **Séparer** : VLANs différents pour utilisateurs, serveurs, voix, gestion
- ✅ **Sécuriser** : isoler les réseaux sensibles (DMZ, gestion)

---

## 11. Calculs de sous-réseaux {#calculs}

### Conversion binaire ↔ décimale

**Puissances de 2** (à mémoriser) :
```
2^0 = 1       2^4 = 16      2^8 = 256
2^1 = 2       2^5 = 32      2^9 = 512
2^2 = 4       2^6 = 64      2^10 = 1024
2^3 = 8       2^7 = 128     2^11 = 2048
```

### Masques de sous-réseau en binaire

| CIDR | Masque décimal | Binaire |
|------|----------------|---------|
| /24 | 255.255.255.0 | 11111111.11111111.11111111.00000000 |
| /25 | 255.255.255.128 | 11111111.11111111.11111111.10000000 |
| /26 | 255.255.255.192 | 11111111.11111111.11111111.11000000 |
| /27 | 255.255.255.224 | 11111111.11111111.11111111.11100000 |
| /28 | 255.255.255.240 | 11111111.11111111.11111111.11110000 |
| /29 | 255.255.255.248 | 11111111.11111111.11111111.11111000 |
| /30 | 255.255.255.252 | 11111111.11111111.11111111.11111100 |

### Valeurs clés à retenir

| Bits empruntés | Valeur décimale | Sous-réseaux | Hôtes par sous-réseau |
|----------------|-----------------|--------------|----------------------|
| 1 | 128 | 2 | 126 |
| 2 | 192 | 4 | 62 |
| 3 | 224 | 8 | 30 |
| 4 | 240 | 16 | 14 |
| 5 | 248 | 32 | 6 |
| 6 | 252 | 64 | 2 |

### Exercice : Déterminer le sous-réseau d'une adresse

**Question** : À quel sous-réseau appartient l'adresse `192.168.10.75/26` ?

**Méthode 1 : Magic Number**
1. Masque /26 = 255.255.255.192
2. Magic Number = 256 - 192 = 64
3. Multiples de 64 : 0, 64, 128, 192
4. 75 est entre 64 et 128
5. **Réponse** : Sous-réseau `192.168.10.64/26`
   - Réseau : 192.168.10.64
   - Première IP : 192.168.10.65
   - Dernière IP : 192.168.10.126
   - Broadcast : 192.168.10.127

**Méthode 2 : Binaire**
```
75 en binaire : 01001011
Masque /26 :    11000000 (192)
                --------
Résultat AND :  01000000 = 64

Sous-réseau : 192.168.10.64/26
```

### Calcul rapide : Nombre d'hôtes nécessaires → Masque

**Question** : Quel masque pour 50 hôtes ?

1. Trouver la puissance de 2 immédiatement supérieure : 2^6 = 64
2. Ajouter 2 pour réseau et broadcast : 64 - 2 = 62 hôtes disponibles ✅
3. Bits hôte = 6 → Masque = 32 - 6 = **/26**

---

## Résumé des points clés 🎯

### Types d'adresses
- ✅ **Unicast** : un-à-un (communication standard)
- ✅ **Broadcast** : un-à-tous (255.255.255.255 ou adresse de broadcast du réseau)
- ✅ **Multicast** : un-à-plusieurs (224.0.0.0/4)

### Classes IPv4
- ✅ **Classe A** : /8 (1-126.x.x.x) - 16M hôtes
- ✅ **Classe B** : /16 (128-191.x.x.x) - 65K hôtes
- ✅ **Classe C** : /24 (192-223.x.x.x) - 254 hôtes
- ✅ **Classe D** : Multicast (224-239.x.x.x)

### Adresses privées (RFC 1918)
- ✅ **10.0.0.0/8** (Classe A)
- ✅ **172.16.0.0/12** (Classe B)
- ✅ **192.168.0.0/16** (Classe C)

### CIDR et subnetting
- ✅ **CIDR** : notation /préfixe (ex: /24)
- ✅ **Subnetting** : diviser un réseau en sous-réseaux
- ✅ **VLSM** : masques de longueur variable
- ✅ **Formule hôtes** : 2^n - 2

### Plan d'adressage
- ✅ Analyser les besoins
- ✅ Utiliser VLSM pour optimiser
- ✅ Commencer par les plus grands réseaux
- ✅ Réserver pour la croissance
- ✅ Documenter le plan

---

**Prochaine étape** : Module 12 - Adressage IPv6
