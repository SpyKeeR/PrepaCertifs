# Module 12 : Advanced BGP

## Introduction

Après les bases de BGP, le module 12 couvre les techniques avancées permettant de déployer BGP à grande échelle dans les environnements critiques. Cela inclut la gestion de la redondance, les politiques de routage complexes, et l'optimisation des chemins sélectionnés par BGP.

## BGP Multihoming

### Concept de Multihoming

**Multihoming** : Technique de connexion d'un site (généralement une entreprise) à travers plusieurs fournisseurs d'accès Internet (ISP) pour assurer la redondance et améliorer la disponibilité.

### Types de Multihoming

#### 1. **Multihoming avec le même AS**

Lorsqu'une entreprise obtient un ASN unique et se connecte à plusieurs ISP :

```
     AS 100 (ISP1)
         |
    [Customer Router]
         |
     AS 200 (ISP2)
```

**Avantages** :
- Contrôle complet du routage avec une seule politique AS
- Pas de dépendance d'un ISP pour les routes

**Configuré** :
```cisco
router bgp 65001           ! ASN unique du client
  neighbor 10.1.1.254 remote-as 100    ! eBGP vers ISP1
  neighbor 10.2.2.254 remote-as 200    ! eBGP vers ISP2
  address-family ipv4 unicast
    network 10.0.0.0 mask 255.255.255.0 ! Annonce au deux ISP
    neighbor 10.1.1.254 activate
    neighbor 10.2.2.254 activate
```

#### 2. **Multihoming avec différents AS**

Lorsqu'une entreprise n'a pas de propre ASN et annonce les routes sous différents ASN ISP :

```
     AS 100 (ISP1)
         |
    [Customer]
         |
     AS 200 (ISP2)
```

**Défis** :
- Les routes sont vues comme différentes (AS_Path différent)
- Plus difficile à gérer les politiques

### Redondance et Basculement

**Path Protection** :
```
Chemin primaire = Meilleur chemin selon Best Path Algorithm
Chemin sécondi = Deuxième meilleur chemin (stocké mais non utilisé)
```

Si le chemin primaire tombe, BGP bascule automatiquement au chemin secondaire.

**Failover Time** :
- Détection : Keepalive timeout (180 sec défaut)
- Reconvergence : Dépend de la complexité des politiques (quelques secondes à minutes)

### Load Balancing en BGP

BGP supporte **Equal-Cost Multi-Path (ECMP)** :

```cisco
router bgp 65001
  bgp bestpath as-path multipath-relax
  address-family ipv4 unicast
    maximum-paths 4    ! Accepts jusqu'à 4 chemins égaux
```

## Transit Routing et Outbound Route Filtering

### Transit Routing (Problème)

**Transit routing** : Situation où le trafic d'un AS extrêmement traverse un autre AS sans destination locale.

**Exemple du problème** :
```
AS100 → [Customer AS] → AS200
```

Si le Customer n'a pas de lien direct vers AS200, le trafic AS100-AS200 passe par Customer (indésirable si pas d'accord de transit).

### Outbound Route Filtering (ORF)

**ORF** : Mécanisme permettant aux voisins BGP de communiquer des préfixes qu'ils désirent recevoir.

**Types d'ORF** :
- **Address Prefix ORF** : Filtre basé sur les préfixes IP
- **AS Path ORF** : Filtre basé sur l'AS Path

**Configuration** :
```cisco
router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 capability orf prefix-list send
    neighbor 10.1.1.254 filter-list 1 out
```

### Prévention du Transit (Départ ORF)

```cisco
! Créer une prefix-list de routes locales uniquement
ip prefix-list COMMUNITY-PREFIXES seq 10 permit 10.0.0.0/8
ip prefix-list COMMUNITY-PREFIXES seq 20 permit 172.16.0.0/12

! Appliquer sur neighbor
router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 prefix-list COMMUNITY-PREFIXES out
```

## Route Filtering avec ACLs et Prefix Lists

### Access Control Lists (ACLs)

**ACL Standard** : Filtre sur l'adresse source uniquement

```cisco
! ACL pour filtrer un préfixe spécifique
access-list 1 permit 10.0.0.0 0.0.0.255
access-list 1 deny any

router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 distribute-list 1 in
```

### Prefix Lists (Meilleure pratique)

**Syntax** :
```cisco
ip prefix-list NAME [seq N] {permit|deny} PREFIX [ge M] [le N]
```

**Paramètres** :
- `ge M` : Longueur minimum du préfixe (greater-or-equal)
- `le N` : Longueur maximum du préfixe (less-or-equal)

**Exemples** :
```cisco
! Accepter seulement /24 ou plus spécifique (ge 24)
ip prefix-list SPECIFICS seq 10 permit 10.0.0.0/8 ge 24

! Accepter tout sauf /32
ip prefix-list NO-HOST seq 10 permit 0.0.0.0/0 le 31

! Appliquer
router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 prefix-list SPECIFICS in
```

### Regular Expressions (RegEx) pour AS Path

**Filtering par AS Path** :

```cisco
! Créer une AS path access-list
ip as-path access-list 1 permit ^100$        ! Seulement AS 100
ip as-path access-list 1 permit ^100_200$    ! AS 100, puis 200

router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254filter-list 1 in
```

**Regex communs** :
- `^` : Début du chemin (AS adjascent)
- `$` : Fin du chemin
- `_` : Séparateur AS
- `.*` : N'importe quel AS
- `?` : Zéro ou une occurrence

## Route Maps

### Structure des Route Maps

Une **route map** est une série de clause numérotées contenant :
1. **Match criteria** : Condition sur la route
2. **Set actions** : Actionne si match = true

```cisco
route-map NAME [permit|deny] SEQUENCE
  match [criteria]
  set [action]
```

### Match Criteria Courants

| Critère | Description |
|---------|-------------|
| `match ip address` | Match ACL ou prefix list |
| `match as-path` | Match AS path access-list |
| `match community` | Match BGP community |
| `match prefix-list` | Match prefix-list |
| `match tag` | Match tag de route |
| `match metric` | Match métrique |

### Set Actions Courants

| Action | Description |
|--------|-------------|
| `set local-preference` | Définir Local Preference (0-4294967295) |
| `set metric` | Définir MED |
| `set as-path prepend` | Allonger AS_Path |
| `set community` | Ajouter Community tag |
| `set weight` | Définir Weight (Cisco) |
| `set origin` | Définir Origin (igp/egp/incomplete) |

### Exemple Complet de Route Map

```cisco
! Accepter seulement les prefixes /24 et augmenter Local Pref
route-map ISP1-IMPORT permit 10
  match prefix-list /24-PREFIXES
  set local-preference 200

route-map ISP1-IMPORT deny 20

! Appliquer
router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 route-map ISP1-IMPORT in
```

## BGP Communities

### Concept de Communities

**Community** : Attribut BGP permettant le tagging des routes pour appliquer des politiques groupées.

**Format** : `ASN:VALUE` (exemple : `100:1`, `65001:100`)

**Portée** :
- **Well-known Communities** : Significacations spéciales (RFC sanctionnées)
- **Private Communities** : Définies propres par l'AS

### Well-known Communities

| Valeur | Signification |
|--------|---------------|
| `no-export` (65535:65281) | Ne pas exporter hors de l'AS |
| `no-advertise` (65535:65282) | Ne pas annoncer du tout |
| `local-as` (65535:65283) | Rester dans le sous-AS (confidédération) |
| `internet` (0) | Aucune restriction |

### Configuration des Communities

```cisco
! Tagger une route avec community
route-map COMMUNITY-TAG permit 10
  match ip address prefix-list INTERNAL-NETS
  set community 100:1

! Exporter seulement sans restriction
route-map COMMUNITY-OUT permit 10
  match community 100:1
  set community no-export

router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 route-map COMMUNITY-TAG in
    neighbor 10.1.1.254 route-map COMMUNITY-OUT out
    neighbor 10.1.1.254 send-community both
```

## BGP Best Path Algorithm (Détails)

### Ordre de Sélection Complet

1. Weight (Cisco proprietary) : Plus haut = meilleur
2. Local Preference (iBGP) : Plus haute = meilleure
3. Locally originated (redistribute vs advertised)
4. AS_Path length : Plus court = meilleur
5. Origin : IGP > EGP > Incomplete
6. MED (Multi-Exit Discriminator) : Plus bas = meilleur
7. neighborType : eBGP préféré sur iBGP
8. IGP metric au next-hop
9. BGP route reflector cluster-list length
10. BGP Route ID du routeur annonceur
11. Neighbor IP address (tiebreaker final)

### Manipulating Best Path

**Augmenter Local Preference** (préférer une route sortante) :
```cisco
route-map PREFER-ISP1 permit 10
  set local-preference 200

router bgp 65001
  neighbor 10.1.1.254 remote-as 100
  address-family ipv4 unicast
    neighbor 10.1.1.254 route-map PREFER-ISP1 in
```

**AS Path Prepend** (faire paraître un chemin plus long) :
```cisco
route-map AVOID-ISP2 permit 10
  set as-path prepend 65001 65001 65001

router bgp 65001
  neighbor 10.1.1.254 remote-as 200
  address-family ipv4 unicast
    neighbor 10.1.1.254 route-map AVOID-ISP2 in
```

## Points Importants à Retenir

1. **Multihoming** améliore la disponibilité via redondance ISP
2. **ORF** prévient le transit en filtrant les annonces reçues
3. **Prefix Lists** sont préférées aux ACLs pour BGP
4. **Route Maps** appliquent des politiques complexes match-action
5. **Communities** agissent comme des tags flexibles pour les routes
6. **Local Preference** contrôle les routes **sortantes**
7. **MED** recommande au peering AS pour routes **rentrantes**
8. **AS Path Prepend** allonge artificiellement le chemin pour déprioritiser
9. **Best Path Algorithm** a un ordre strict et déterministe
10. **Weight** (Cisco proprietary) est le critère de plus haute priorité
