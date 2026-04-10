# Module 12 - Adressage IPv6

## Table des matières
1. [Introduction à IPv6](#introduction)
2. [Structure des adresses IPv6](#structure)
3. [Compression des adresses IPv6](#compression)
4. [Types d'adresses IPv6](#types-adresses)
5. [GUA - Global Unicast Address](#gua)
6. [LLA - Link-Local Address](#lla)
7. [Adresses unicast spéciales](#unicast-speciales)
8. [Adresses multicast IPv6](#multicast)
9. [Multicast et NDP](#multicast-ndp)
10. [Adresses anycast](#anycast)
11. [Segmentation IPv6](#segmentation)
12. [Plan d'adressage IPv6](#plan-adressage)
13. [Configuration d'interfaces IPv6](#configuration)

---

## 1. Introduction à IPv6 {#introduction}

### Pourquoi IPv6 ?
- **Épuisement des adresses IPv4** : ~4,3 milliards d'adresses insuffisantes
- **Croissance d'Internet** : IoT, mobiles, objets connectés
- **Simplification** : entête simplifié, auto-configuration
- **Sécurité** : IPsec intégré nativement

### Avantages d'IPv6
- ✅ Espace d'adressage **quasi infini** : 340 sextillions d'adresses (2^128)
- ✅ **Auto-configuration** : SLAAC sans serveur DHCP
- ✅ **Pas de NAT nécessaire** : connectivité de bout en bout
- ✅ **Multicast amélioré** : plus de broadcast
- ✅ **Mobilité** et QoS intégrés
- ✅ **Entête simplifié** : traitement plus rapide

---

## 2. Structure des adresses IPv6 {#structure}

### Format de base
- **128 bits** (vs 32 bits pour IPv4)
- Notation **hexadécimale** (base 16)
- **8 groupes** de 16 bits (4 chiffres hexa) séparés par `:`

**Format complet** :
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

**Décomposition** :
```
2001 : 0db8 : 85a3 : 0000 : 0000 : 8a2e : 0370 : 7334
 |      |      |      |      |      |      |      |
 16bits 16bits 16bits 16bits 16bits 16bits 16bits 16bits

Total : 8 × 16 bits = 128 bits
```

### Chiffres hexadécimaux
```
0 1 2 3 4 5 6 7 8 9 A B C D E F
0-9 : valeurs décimales 0-9
A-F : valeurs décimales 10-15
```

---

## 3. Compression des adresses IPv6 {#compression}

### Règle 1 : Suppression des zéros de tête
On peut **omettre les zéros de tête** dans chaque groupe de 16 bits.

**Exemple** :
```
Forme complète :    2001:0db8:0000:0042:0000:8a2e:0070:7334
Forme compressée :  2001:db8:0:42:0:8a2e:70:7334
```

**Détails** :
- `0db8` → `db8` (zéro de tête supprimé)
- `0000` → `0` (tous les zéros sauf un)
- `0042` → `42` (zéros de tête supprimés)
- `0070` → `70` (zéro de tête supprimé)

⚠️ **Attention** : on doit garder **au moins un zéro** par groupe

### Règle 2 : Utilisation de `::`
On peut remplacer **une seule séquence** de groupes consécutifs de zéros par `::`.

⚠️ **IMPORTANT** : Cette compression ne peut être utilisée **qu'une seule fois** dans une adresse.

**Exemple 1** :
```
Forme complète :    2001:0db8:0000:0000:0000:0000:0000:0001
Règle 1 :           2001:db8:0:0:0:0:0:1
Règle 2 (::) :      2001:db8::1
```

**Exemple 2** :
```
Forme complète :    fe80:0000:0000:0000:0210:5aff:fe3e:78cf
Règle 1 :           fe80:0:0:0:210:5aff:fe3e:78cf
Règle 2 (::) :      fe80::210:5aff:fe3e:78cf
```

**Exemple 3** : Adresse de bouclage (loopback)
```
Forme complète :    0000:0000:0000:0000:0000:0000:0000:0001
Règle 2 (::) :      ::1
```

**Exemple 4** : Adresse non spécifiée
```
Forme complète :    0000:0000:0000:0000:0000:0000:0000:0000
Règle 2 (::) :      ::
```

### Pourquoi une seule fois ?
Si on utilisait `::` plusieurs fois, on ne pourrait pas déterminer combien de zéros chaque `::` représente.

**Exemple d'ambiguïté** (❌ INVALIDE) :
```
2001::42::7334   # Invalide ! On ne sait pas où sont les zéros
```

### Expansion d'une adresse compressée

**Question** : Quelle est la forme complète de `2001:db8::8a2e:370:7334` ?

**Méthode** :
1. Compter le nombre de groupes présents : 2001, db8, 8a2e, 370, 7334 = **5 groupes**
2. Nombre de groupes manquants : 8 - 5 = **3 groupes**
3. Remplacer `::` par 3 groupes de `0000`

**Résultat** :
```
2001:db8::8a2e:370:7334
    ↓
2001:0db8:0000:0000:0000:8a2e:0370:7334
```

---

## 4. Types d'adresses IPv6 {#types-adresses}

IPv6 utilise **trois types** d'adresses (pas de broadcast) :

| Type | Description | Portée |
|------|-------------|--------|
| **Unicast** | Communication **un-à-un** | Un seul destinataire |
| **Multicast** | Communication **un-à-plusieurs** | Groupe d'hôtes abonnés |
| **Anycast** | Communication **un-à-un parmi plusieurs** | Le plus proche d'un groupe |

⚠️ **Point important** : IPv6 **n'a pas d'adresse broadcast**. Le broadcast est remplacé par le **multicast**.

---

## 5. GUA - Global Unicast Address {#gua}

### Définition
Les **GUA (Global Unicast Address)** sont les adresses IPv6 **routables globalement** sur Internet (équivalent des adresses publiques IPv4).

### Caractéristiques
- **Plage** : `2000::/3` (commence par 001 en binaire)
- **Routables** sur Internet
- **Uniques mondialement**
- **Structure hiérarchique** pour faciliter le routage

### Structure d'une GUA

```
|     48 bits      |  16 bits  |        64 bits         |
+------------------+-----------+------------------------+
| Global Prefix    | Subnet ID |     Interface ID       |
| (Routage global) | (Interne) | (Identifiant d'hôte)   |
+------------------+-----------+------------------------+
```

#### Global Routing Prefix (48 bits)
- Attribué par un **RIR** (Regional Internet Registry) ou un **ISP**
- Identifie l'**organisation** sur Internet
- Typiquement : `/48` pour une organisation
- Permet **65 536 sous-réseaux** (/48 → /64)

#### Subnet ID (16 bits)
- Utilisé pour créer des **sous-réseaux internes**
- Géré par l'**administrateur réseau**
- Permet de créer **65 536 sous-réseaux** différents

#### Interface ID (64 bits)
- Identifie une **interface** sur un sous-réseau
- Peut être généré :
  - **Manuellement** (configuration statique)
  - **EUI-64** (dérivé de l'adresse MAC)
  - **Aléatoirement** (privacy extensions)
  - **SLAAC** (auto-configuration)

### Exemple de GUA
```
2001:0db8:acad:0001:0000:0000:0000:0100/64

Décomposition :
- Global Routing Prefix : 2001:0db8:acad (48 bits)
- Subnet ID : 0001 (16 bits)
- Interface ID : 0000:0000:0000:0100 (64 bits)

Forme compressée : 2001:db8:acad:1::100/64
```

### Allocation typique
```
ISP alloue :        2001:db8::/32  (RIR → ISP)
Organisation reçoit : 2001:db8:acad::/48
Sous-réseaux :
  - VLAN 10 :       2001:db8:acad:1::/64
  - VLAN 20 :       2001:db8:acad:2::/64
  - VLAN 30 :       2001:db8:acad:3::/64
  ...
  - VLAN 65535 :    2001:db8:acad:ffff::/64
```

---

## 6. LLA - Link-Local Address {#lla}

### Définition
Les **LLA (Link-Local Address)** sont des adresses IPv6 **non routables** utilisées pour la communication sur un **seul lien** (segment réseau local).

### Caractéristiques ⚠️ **SECTION IMPORTANTE**
- **Plage** : `FE80::/10` (1111 1110 10xx xxxx)
- **Non routables** : ne traversent jamais un routeur
- **Obligatoires** : chaque interface IPv6 doit avoir une LLA
- **Uniques par lien** : peuvent être identiques sur des liens différents
- **Auto-générées** : dès qu'une interface IPv6 est activée

### Structure d'une Link-Local

```
|   10 bits  |     54 bits    |        64 bits         |
+------------+----------------+------------------------+
| 1111111010 | 0000...0000    |     Interface ID       |
|  (FE80)    | (tous à zéro)  | (EUI-64 ou manuel)     |
+------------+----------------+------------------------+

Préfixe standard : FE80:0000:0000:0000 (ou FE80::)
```

**Note** : En pratique, les 54 bits après FE80 sont **toujours à zéro**, donc toutes les LLA commencent par `FE80::`.

### Génération automatique de la LLA

Quand une interface IPv6 est activée, une LLA est **automatiquement générée** avec **EUI-64** :

**Exemple** :
```
Adresse MAC :     00:1A:2B:3C:4D:5E

Étapes EUI-64 :
1. Diviser la MAC en deux : 00:1A:2B | 3C:4D:5E
2. Insérer FFFE au milieu : 00:1A:2B:FF:FE:3C:4D:5E
3. Inverser le 7e bit (U/L bit) :
   00 (hex) = 0000 0000 (bin)
           → 0000 0010 (bin) = 02 (hex)
4. Interface ID : 021A:2BFF:FE3C:4D5E

Link-Local complète : FE80::021A:2BFF:FE3C:4D5E
```

### Utilisations de la Link-Local ⚠️ **RÔLE CRUCIAL**

#### 1. Passerelle par défaut
Les hôtes IPv6 utilisent l'**adresse link-local du routeur** comme passerelle par défaut (pas la GUA).

**Exemple de configuration client** :
```
Adresse IPv6 : 2001:db8:acad:1::10/64
Passerelle par défaut : FE80::1  (link-local du routeur)
```

**Pourquoi ?** 
- La LLA du routeur est **stable** (ne change pas si la GUA change)
- **Simplifie la configuration** (même LLA sur toutes les interfaces du routeur)
- **Fonctionne même sans GUA** configurée

#### 2. Protocoles de routage
Les protocoles de routage (OSPFv3, EIGRP pour IPv6) utilisent les LLA pour communiquer entre routeurs voisins.

#### 3. Neighbor Discovery Protocol (NDP)
- **RS/RA** : découverte de routeurs
- **NS/NA** : résolution d'adresse (équivalent ARP)
- **Redirect** : messages de redirection

#### 4. Communication locale
- Échanges entre périphériques du même segment
- Ne nécessite **pas de routage**

### Configuration manuelle de la LLA (recommandée)

**Pourquoi configurer manuellement ?**
- LLA générées automatiquement (EUI-64) sont **longues et complexes**
- Configuration manuelle permet d'utiliser des adresses **simples et mémorisables**
- **Facilite l'administration** et le troubleshooting

**Commande** :
```
Router(config-if)# ipv6 address fe80::1 link-local
```

**Exemple de configuration complète** :
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown

R1(config)# interface g0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
```

**Avantages** :
- ✅ Même LLA (`FE80::1`) sur toutes les interfaces du routeur
- ✅ **Facile à mémoriser** pour les administrateurs
- ✅ **Cohérence** dans la configuration
- ✅ **Simplification** de la passerelle par défaut pour les clients

### Comparaison LLA auto vs manuelle

| Aspect | Auto-générée (EUI-64) | Configurée manuellement |
|--------|----------------------|------------------------|
| **Exemple** | FE80::021A:2BFF:FE3C:4D5E | FE80::1 |
| **Lisibilité** | ❌ Complexe | ✅ Simple |
| **Mémorisation** | ❌ Difficile | ✅ Facile |
| **Administration** | ❌ Moins pratique | ✅ Très pratique |
| **Cohérence** | Variable selon MAC | ✅ Homogène |

---

## 7. Adresses unicast spéciales {#unicast-speciales}

### Adresse de bouclage (Loopback)
- **Adresse** : `::1/128`
- Équivalent de `127.0.0.1` en IPv4
- Utilisée pour les **tests locaux**
- Paquet ne quitte **jamais** l'hôte

**Utilisation** :
```
ping ::1
ping ipv6 ::1
```

### Adresse non spécifiée (Unspecified Address)
- **Adresse** : `::/128` (tous les bits à 0)
- Équivalent de `0.0.0.0` en IPv4
- Utilisée pour indiquer l'**absence d'adresse**
- Utilisée dans les messages **DHCP / SLAAC** avant d'obtenir une adresse

### Unique Local Address (ULA)
- **Plage** : `FC00::/7` (commence par FC ou FD)
- **Usage pratique** : `FD00::/8`
- Équivalent des **adresses privées IPv4** (RFC 1918)
- **Non routables** sur Internet
- **Routables** dans une organisation

**Exemple** :
```
FD00:1234:5678:1::1/64
```

**Utilisation** :
- Réseaux internes d'entreprise
- Communication inter-sites privée
- Pas besoin de NAT (contrairement à IPv4)

---

## 8. Adresses multicast IPv6 {#multicast}

### Définition
Les adresses **multicast** permettent d'envoyer un paquet à **un groupe d'interfaces** abonnées.

### Caractéristiques
- **Plage** : `FF00::/8` (commence par FF)
- Remplace le **broadcast IPv4**
- Plus **efficace** que le broadcast (pas de traitement inutile)

### Structure d'une adresse multicast

```
|  8 bits |  4 bits | 4 bits |         112 bits          |
+---------+---------+--------+---------------------------+
|   FF    |  Flags  | Scope  |        Group ID           |
+---------+---------+--------+---------------------------+
```

#### Flags (4 bits)
- Bit 0-2 : Réservés (0)
- Bit 3 : 
  - **0** = Adresse multicast **permanente** (well-known)
  - **1** = Adresse multicast **temporaire** (dynamique)

#### Scope (4 bits)
Définit la **portée** du multicast :

| Valeur | Scope | Description |
|--------|-------|-------------|
| **1** | Interface-Local | Limité à une interface (loopback) |
| **2** | Link-Local | Limité au lien local (segment) |
| **5** | Site-Local | Limité à un site |
| **8** | Organization-Local | Limité à une organisation |
| **E** | Global | Portée mondiale (Internet) |

### Adresses multicast well-known (permanentes)

| Adresse | Description | Utilisation |
|---------|-------------|-------------|
| **FF02::1** | All nodes (tous les nœuds) | Tous les périphériques IPv6 du lien |
| **FF02::2** | All routers (tous les routeurs) | Tous les routeurs IPv6 du lien |
| **FF02::5** | OSPFv3 routers | Routeurs OSPFv3 sur le lien |
| **FF02::6** | OSPFv3 DR/BDR | Designated/Backup Designated Router OSPF |
| **FF02::9** | RIPng routers | Routeurs RIPng |
| **FF02::A** | EIGRP routers | Routeurs EIGRP pour IPv6 |
| **FF02::D** | PIM routers | Routeurs PIM (Protocol Independent Multicast) |
| **FF02::1:2** | DHCP agents | Serveurs et relais DHCPv6 |
| **FF02::1:FF00:0/104** | Solicited-node | Résolution d'adresse (NDP) |

---

## 9. Multicast et NDP {#multicast-ndp}

### Adresse multicast solicited-node ⚠️ **TRÈS IMPORTANT**

#### Définition
Les adresses **solicited-node** sont des adresses multicast spéciales utilisées par **NDP** pour la résolution d'adresse (équivalent ARP en IPv4).

#### Format
```
FF02::1:FF[24 derniers bits de l'adresse unicast]
```

**Structure** :
```
FF02:0000:0000:0000:0000:0001:FF[xx:xxxx]
                                  └─ 24 bits (6 derniers chiffres hexa)
```

#### Génération

Pour chaque adresse **unicast** (GUA ou LLA), une adresse **solicited-node** correspondante est automatiquement créée.

**Exemple 1** :
```
Adresse unicast :     2001:db8:acad:1::10
                                      └─ Derniers 24 bits : 00:0010

Solicited-node :      FF02::1:FF00:0010
```

**Exemple 2** :
```
Adresse unicast :     2001:db8:acad:1:a8bb:ccff:fe00:6700
                                       └─ Derniers 24 bits : 00:6700

Solicited-node :      FF02::1:FF00:6700
```

**Exemple 3** :
```
Link-Local :          FE80::021A:2BFF:FE3C:4D5E
                                      └─ Derniers 24 bits : 3C:4D5E

Solicited-node :      FF02::1:FF3C:4D5E
```

#### Fonctionnement avec NDP

Lorsqu'un hôte veut résoudre une adresse IPv6 en adresse MAC, il envoie un **Neighbor Solicitation (NS)** à l'adresse **solicited-node multicast** correspondante.

**Processus** :
1. PC1 veut communiquer avec `2001:db8:acad:1::20`
2. PC1 calcule la solicited-node : `FF02::1:FF00:0020`
3. PC1 envoie un **NS** à `FF02::1:FF00:0020` (multicast)
4. Seuls les périphériques ayant `2001:db8:acad:1::20` **traitent** le message
5. PC2 répond avec un **NA** (Neighbor Advertisement) en unicast

**Avantage** :
- Plus **efficace** que le broadcast IPv4 (FF:FF:FF:FF:FF:FF)
- Seuls les périphériques concernés traitent le message
- Réduit la **charge réseau**

#### Adresse MAC multicast correspondante

Les adresses multicast IPv6 sont mappées sur des adresses MAC multicast Ethernet :

**Format MAC multicast** : `33:33:[4 derniers octets de l'IPv6 multicast]`

**Exemple** :
```
IPv6 multicast :      FF02::1:FF00:6700
                               └─ Derniers 4 octets : 00:01:FF00:6700

MAC multicast :       33:33:FF:00:67:00
                            └─ 4 derniers octets
```

**Comparaison avec IPv4** :
- IPv4 multicast MAC : `01:00:5E:[23 derniers bits de l'IPv4 multicast]`
- IPv6 multicast MAC : `33:33:[4 derniers octets de l'IPv6 multicast]`

### Multicast pour NDP

Les messages NDP utilisent des adresses multicast :

| Message NDP | Adresse multicast de destination |
|-------------|----------------------------------|
| **RS** (Router Solicitation) | `FF02::2` (All routers) |
| **RA** (Router Advertisement) | `FF02::1` (All nodes) ou unicast |
| **NS** (Neighbor Solicitation) | `FF02::1:FF[24 derniers bits]` (Solicited-node) |
| **NA** (Neighbor Advertisement) | Unicast (réponse) ou `FF02::1` (annonce) |
| **Redirect** | Unicast |

---

## 10. Adresses anycast {#anycast}

### Définition
Une adresse **anycast** est une adresse assignée à **plusieurs interfaces** (généralement sur différents périphériques). Le paquet est délivré à **l'interface la plus proche** (selon la métrique de routage).

### Caractéristiques
- Même **format** qu'une adresse unicast
- Assignée à **plusieurs périphériques**
- Le routeur choisit l'**itinéraire optimal**
- Utilisée pour la **redondance** et la **répartition de charge**

### Utilisation
- **DNS** : serveurs DNS racine (plusieurs serveurs avec la même IP)
- **CDN** : réseau de distribution de contenu
- **Services redondants** : plusieurs serveurs offrant le même service

### Exemple
```
Trois serveurs DNS dans différents pays :
- Serveur 1 (USA) : 2001:db8::100 (anycast)
- Serveur 2 (Europe) : 2001:db8::100 (anycast)
- Serveur 3 (Asie) : 2001:db8::100 (anycast)

Un client en Europe qui contacte 2001:db8::100 sera automatiquement 
dirigé vers le serveur en Europe (le plus proche).
```

---

## 11. Segmentation IPv6 {#segmentation}

### Hiérarchie d'allocation

```
IANA (Internet Assigned Numbers Authority)
   ↓
RIR (Regional Internet Registry) : /12 à /23
   ↓
ISP (Internet Service Provider) : /32
   ↓
Organisation : /48
   ↓
Sous-réseaux : /64 (standard pour un segment)
```

### Tailles de préfixes recommandées

| Entité | Préfixe typique | Sous-réseaux possibles |
|--------|----------------|------------------------|
| **RIR** | /12 à /23 | Des milliards |
| **ISP** | /32 | 65 536 organisations (/48) |
| **Organisation** | /48 | 65 536 sous-réseaux (/64) |
| **Sous-réseau** | /64 | 18 trillions d'hôtes |
| **Point-à-point** | /127 | 2 hôtes (recommandé RFC 6164) |
| **Loopback** | /128 | 1 adresse |

### Segmentation standard : /48 → /64

**Allocation typique** :
```
Organisation reçoit :   2001:db8:acad::/48

Subnet ID = 16 bits (FFFF en hexa = 65 535 sous-réseaux)

Sous-réseaux /64 :
  - 2001:db8:acad:0::/64     # Sous-réseau 0
  - 2001:db8:acad:1::/64     # Sous-réseau 1
  - 2001:db8:acad:2::/64     # Sous-réseau 2
  ...
  - 2001:db8:acad:ffff::/64  # Sous-réseau 65535
```

### Pourquoi /64 pour un sous-réseau ?

Le **/64** est le standard IPv6 pour un segment réseau :
- ✅ Compatible avec **SLAAC** (nécessite /64)
- ✅ Compatible avec **EUI-64** (Interface ID = 64 bits)
- ✅ **Largement suffisant** : 2^64 = 18 trillions d'hôtes par sous-réseau
- ✅ **Simplifie la gestion** (pas besoin de calculer des sous-réseaux plus petits)

⚠️ **Exception** : liens point-à-point entre routeurs peuvent utiliser **/127** (RFC 6164)

### Segmentation hiérarchique

**Exemple** : Organisation avec plusieurs sites

```
Organisation : 2001:db8:acad::/48

Site 1 (Siège) : 2001:db8:acad:1xxx::/52 (4096 sous-réseaux)
  - VLAN 10 :    2001:db8:acad:1000::/64
  - VLAN 20 :    2001:db8:acad:1001::/64
  - VLAN 30 :    2001:db8:acad:1002::/64

Site 2 (Succursale) : 2001:db8:acad:2xxx::/52
  - VLAN 10 :    2001:db8:acad:2000::/64
  - VLAN 20 :    2001:db8:acad:2001::/64

Site 3 (Bureau distant) : 2001:db8:acad:3xxx::/56 (256 sous-réseaux)
  - VLAN 10 :    2001:db8:acad:3000::/64
  - VLAN 20 :    2001:db8:acad:3001::/64
```

---

## 12. Plan d'adressage IPv6 {#plan-adressage}

### Méthodologie de planification

#### Étape 1 : Obtenir un préfixe de l'ISP
- Typiquement : **/48** ou **/56** pour une organisation
- Demander un préfixe **statique** (pas dynamique)

#### Étape 2 : Définir le Subnet ID
- Utiliser les **16 bits** (ou moins selon le préfixe reçu) pour créer des sous-réseaux
- Adopter une **nomenclature logique**

#### Étape 3 : Allouer les sous-réseaux /64
- Un **/64** par segment réseau (VLAN, site, etc.)
- Documenter chaque allocation

#### Étape 4 : Planifier l'Interface ID
- **Serveurs** : adresses statiques simples (::1, ::10, ::100)
- **Routeurs** : LLA manuelles (FE80::1, FE80::2)
- **Clients** : SLAAC ou DHCPv6

### Exemple de plan d'adressage scénarisé

**Scénario** :
```
Entreprise avec préfixe : 2001:db8:acad::/48
- Siège social : 3 VLANs (Admin, Production, Invités)
- Succursale : 2 VLANs (Admin, Production)
- Serveurs : 1 VLAN (DMZ)
- Liens WAN : 2 liens entre sites
```

**Plan d'adressage** :

| Segment | Subnet ID | Réseau | Utilisation |
|---------|-----------|--------|-------------|
| Siège - Admin | 0001 | 2001:db8:acad:1::/64 | Employés administratifs |
| Siège - Production | 0002 | 2001:db8:acad:2::/64 | Employés production |
| Siège - Invités | 0003 | 2001:db8:acad:3::/64 | WiFi invités |
| Succursale - Admin | 0010 | 2001:db8:acad:10::/64 | Employés administratifs |
| Succursale - Prod | 0011 | 2001:db8:acad:11::/64 | Employés production |
| DMZ Serveurs | 0100 | 2001:db8:acad:100::/64 | Serveurs publics |
| Lien WAN 1 | FFF0 | 2001:db8:acad:fff0::/127 | Routeur Siège ↔ Succursale |
| Lien WAN 2 | FFF1 | 2001:db8:acad:fff1::/127 | Routeur Siège ↔ Internet |

**Configuration des routeurs** :
```
# Routeur Siège
interface g0/0
  description VLAN 1 - Admin
  ipv6 address 2001:db8:acad:1::1/64
  ipv6 address fe80::1 link-local

interface g0/1
  description VLAN 2 - Production
  ipv6 address 2001:db8:acad:2::1/64
  ipv6 address fe80::1 link-local

interface serial 0/0/0
  description Lien WAN vers Succursale
  ipv6 address 2001:db8:acad:fff0::1/127
  ipv6 address fe80::1 link-local
```

### Bonnes pratiques
- ✅ **Cohérence** : utiliser une logique dans les Subnet ID (ex: Xyyy, X=site, yyy=VLAN)
- ✅ **Documentation** : tableau récapitulatif obligatoire
- ✅ **Réservation** : laisser des plages pour la croissance
- ✅ **Simplicité** : Interface ID simples pour serveurs (::1, ::10, ::100)
- ✅ **LLA manuelles** : FE80::1, FE80::2, etc. sur routeurs
- ✅ **/64 standard** : sauf exception (liens point-à-point /127)

---

## 13. Configuration d'interfaces IPv6 {#configuration}

### Activation du routage IPv6
```
Router(config)# ipv6 unicast-routing
```
⚠️ **Obligatoire** pour que le routeur route les paquets IPv6 et envoie des RA.

### Configuration d'une GUA et LLA

**Exemple 1 : Configuration manuelle complète**
```
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# description LAN Admin
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
```

**Exemple 2 : Configuration avec EUI-64**
```
R1(config)# interface gigabitEthernet 0/1
R1(config-if)# description LAN Production
R1(config-if)# ipv6 address 2001:db8:acad:2::/64 eui-64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
```

### Configuration de routes statiques

**Route statique standard**
```
R1(config)# ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2
```

**Route par défaut**
```
R1(config)# ipv6 route ::/0 2001:db8:acad:100::1
```

**Route avec LLA (nécessite interface de sortie)**
```
R1(config)# ipv6 route 2001:db8:acad:4::/64 serial0/0/0 fe80::2
```

### Vérification
```
R1# show ipv6 interface brief
R1# show ipv6 interface g0/0
R1# show ipv6 route
R1# show ipv6 neighbors
R1# ping ipv6 2001:db8:acad:1::10
```

---

## Résumé des points clés 🎯

### Structure et compression
- ✅ **128 bits** : 8 groupes de 16 bits (hexadécimal)
- ✅ **Compression** : supprimer zéros de tête, `::` une seule fois
- ✅ **Format** : 2001:db8:acad:1::100/64

### Types d'adresses
- ✅ **GUA** (2000::/3) : routables globalement, structure /48 → /64
- ✅ **LLA** (FE80::/10) : non routables, obligatoires, passerelle par défaut
- ✅ **Multicast** (FF00::/8) : remplace broadcast, FF02::1/2 courants
- ✅ **Anycast** : même adresse, routage vers la plus proche

### Link-Local ⚠️ **IMPORTANT**
- ✅ **FE80::/10** : auto-générée (EUI-64) ou manuelle
- ✅ **Configuration manuelle recommandée** : `ipv6 address fe80::1 link-local`
- ✅ **Utilisée comme passerelle** par les clients
- ✅ **Non routable** : communication locale uniquement

### Multicast et NDP
- ✅ **FF02::1** : tous les nœuds
- ✅ **FF02::2** : tous les routeurs
- ✅ **Solicited-node** : FF02::1:FF[24 derniers bits] pour NDP
- ✅ **MAC multicast** : 33:33:[4 derniers octets]

### Segmentation
- ✅ **Organisation** : /48 (65 536 sous-réseaux /64)
- ✅ **Sous-réseau standard** : /64 (18 trillions d'hôtes)
- ✅ **Point-à-point** : /127 (2 hôtes)
- ✅ **16 bits Subnet ID** : permet 65 536 sous-réseaux

### Plan d'adressage
- ✅ Préfixe ISP : /48 ou /56
- ✅ Nomenclature logique pour Subnet ID
- ✅ /64 par segment (VLAN, site)
- ✅ LLA manuelles sur routeurs (FE80::1, FE80::2)

---

**Prochaine étape** : Module 13 - ICMP et connectivité
