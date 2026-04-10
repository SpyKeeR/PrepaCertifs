# Module 8 : OSPF - Notes Détaillées

## Introduction

OSPF (Open Shortest Path First) est un protocole de routage de l'état de lien standardisé (RFC 2328 OSPFv2, RFC 5340 OSPFv3) largement déployé dans les réseaux d'entreprise et les ISP. Contrairement aux protocoles distance vector (RIPv2, EIGRP primitif), OSPF construit une carte complète de la topologie du réseau et utilise l'algorithme SPF (Shortest Path First) de Dijkstra pour les décisions de routage. Ce module couvre les fondamentaux OSPFv2, la configuration de base, et les optimisations courantes.

## Concepts Clés

- **LSA (Link-State Advertisement)** : Message de mise à jour topologique
- **LSDB (Link State Database)** : Base de données complète de la topologie
- **SPF (Shortest Path First)** : Algorithme de Dijkstra pour meilleur chemin
- **RID (Router ID)** : Identifiant unique du routeur (adresse IP)
- **DR/BDR (Designated Router/Backup DR)** : Rôles élus pour réduction de trafic
- **Areas** : Domaines logiques pour la scalabilité
- **ABR (Area Border Router)** : Routeur connectant plusieurs zones
- **ASBR (AS Border Router)** : Routeur injectant routes externes
- **SPT (Shortest Path Tree)** : Arbre des chemins plus courts depuis un routeur

## 1. Fondamentaux OSPF

### Caractéristiques Principales

**OSPF est un protocole link-state pur** :
- ✓ Convergence rapide (SPF recompilation)
- ✓ Scalabilité excellente via Areas
- ✓ Comportement prévisible
- ✓ Métrique simple (coût inverse bande passante)
- ✓ Support multi-vendeur (standardisé)
- ✓ Supporte VLSM et CIDR
- ✓ Authentification MD5 et HMAC
- ✓ Supporte multi-VRF
- ✓ Complexité CPU/Mémoire plus élevée que EIGRP

### Architecture de Base

```
OSPF Domain (Autonomous System)
├── Area 0 (Backbone)
│   ├── Router 1 (Core)
│   └── Router 2 (Core)
├── Area 1
│   ├── Router 3 (Normal)
│   └── ABR (connecte Area 1 → Area 0)
└── Area 2
    ├── Router 4 (Normal)
    └── ABR (connecte Area 2 → Area 0)
```

## 2. Fondamentaux OSPF

### Router ID (RID)

**Définition** : Identifiant unique du routeur dans le domaine OSPF (32 bits, format IP).

**Sélection automatique** (dans cet ordre) :
1. RID configuré explicitement
2. Adresse IP la plus élevée d'une interface loopback
3. Adresse IP configurée la plus élevée d'une interface physique

**Configuration explicite** (recommandée) :
```
router ospf 100
 router-id 1.1.1.1
```

**Vérification** :
```
show ip ospf
show ip ospf interface loopback0
```

**IMPORTANT** : RID est établi au démarrage OSPF. Changement ultérieur nécessite `clear ip ospf process`.

### Voisinage OSPF (Adjacency)

#### Discovery Phase : Hello Packets

OSPF utilise les paquets **Hello** pour :
1. Découvrir voisins potentiels
2. Établir voisinage
3. Maintenir voisinage
4. Élire DR/BDR

**Paramètres Hello (par défaut)** :

| Type d'Interface | Hello | Dead (Hold) |
|---|---|---|
| **Ethernet/All multi-access** | 10 sec | 40 sec (4×Hello) |
| **Point-to-point** | 10 sec | 40 sec |
| **Point-to-multipoint** | 30 sec | 120 sec |
| **NBMA (Non-Broadcast)** | 30 sec | 120 sec |

**Conditions pour Hello valide** :
1. Adresse de source dans même sous-réseau
2. Même Area ID
3. Même masque de sous-réseau
4. Même métrique de route
5. Même timers (Hello/Dead)
6. Même stub area flag
7. Même MTU (si échange DD)

**Incompatibilité** : Si l'un de ces paramètres diverge, OSPF détecte neighbour mais ne le considère pas ADJACENT.

#### Formation d'Adjacency (Echange de Bases de Données)

L'adjacency OSPF passe par 8 états :

```
Down → Init → ExStart → Exchange → Loading → Full
```

1. **Down** : Pas de Hello reçu
2. **Init** : Hello reçu, mais sans RID du routeur local (voisin unidirectionnel)
3. **2-Way** : Hello reçu avec RID du routeur local (bidirectionnel, DR/BDR élu ici)
4. **ExStart** : Master/Slave élu pour DB exchange (routeur avec plus haut RID = Master)
5. **Exchange** : Database Description (DD) packets échangés
6. **Loading** : Link State Requests (LSR) et Link State Updates (LSU) échangés
7. **Full** : Bases de données synchronisées

## 3. Élection DR/BDR

### Rôles DR et BDR

**DR (Designated Router)** :
- Rôle d'interface multi-accès (Ethernet, Serial NBMA, etc.)
- Responsable de flooder LSA sur tous les voisins (centralise traffic)
- Réduit nombre de adjacencies (n routeurs = 1 DR + n-1 voisins au DR)

**BDR (Backup Designated Router)** :
- Prêt à prendre rôle de DR si DR défaille
- Reçoit copie de tous les LSA
- Converge en cas défaillance DR (transition Fast)

**Autres (DROther)** :
- Routeurs normaux attachés au segment
- Établissent adjacency complète seulement avec DR et BDR

### Critères d'Élection

**Priorité d'élection (dans cet ordre)** :
1. **Priorité d'interface OSPF** (0-255, défaut 1)
   - 0 = Jamais élu (link passive)
   - Plus élevé = Priorité supérieure
2. Si Priorités égales → **RID la plus élevée** gagne

**Configuration** :
```
interface Gi0/0
 ip ospf priority 100  ! Élevé priorité (défaut 1)
```

**Élection Special** :
- Première DR élue = premier routeur avec plus haut RID (si pas de priorité)
- Changement priorité ne force pas réélection (rester avec DR actuel)
- Réélection seulement si DR/BDR défaille

**Vérification** :
```
show ip ospf neighbor
show ip ospf interface
show ip ospf neighbor detail
```

## 4. Link State Advertisements (LSA)

### Types LSA (dans OSPF classic)

| Type | Nom | Scope | Fonction |
|---|---|---|---|
| **1** | Router LSA | Intra-area | Liens du routeur, coûts |
| **2** | Network LSA | Intra-area | Réseau multi-accès, DR annonce |
| **3** | Network Summary LSA | Inter-area | ABR résume area |
| **4** | ASBR Summary LSA | Inter-area | ABR annonce ASBR |
| **5** | AS External LSA | AS-wide | Routes externes redistribuées |
| **7** | NSSA External LSA | NSSA area | Routes externes dans NSSA |

**LSA Type 1 (Router)** :
- Générée par chaque routeur
- Listes liens du routeur et coûts
- Flooded intra-area seulement

**LSA Type 2 (Network)** :
- Générée par DR
- Décrit réseau multi-accès
- Inclut tous routeurs attachés

**LSA Type 3 (Network Summary)** :
- Générée par ABR
- Résume routes intra-area
- Permet scalabilité inter-area

**LSA Type 5 (AS External)** :
- Générée par ASBR
- Routes redistribuées du routeur externe
- Flooded AS-wide (tous areas sauf NSSA)

### LSDB (Link-State Database)

La **LSDB** contient :
- Tous les LSA du domaine OSPF
- Graphe complet de la topologie
- Chaque routeur calcule SPF depuis sa LSDB
- Inondation LSA à tous les routeurs

**Vérification** :
```
show ip ospf database                ! Résumé LSDB
show ip ospf database router         ! Détail Type 1 LSAs
show ip ospf database network        ! Détail Type 2 LSAs
show ip ospf database summary        ! Détail Type 3 LSAs
show ip ospf database external       ! Détail Type 5 LSAs
```

## 5. OSPF Areas et Hiérarchie

### Concept des Areas

OSPF divise la domain en **Areas** pour:
- Réduire la taille de la LSDB
- Simplifier SPF computation (par area)
- Contrôler inondation LSA
- Meilleure scalabilité

### Area 0 (Backbone Area)

- **Area 0 est obligatoire** dans OSPF
- Centre de la hiérarchie OSPF
- Toutes les areas doivent être connectées à Area 0 (directement ou via transit area)
- Inter-area traffic **passe toujours par Area 0**

**Designs vérifiés** :
```
Area 0 ---ABR--- Area 1
  |
  +---ABR--- Area 2
  
ALL inter-area traffic via Area 0
```

### Types de Routeurs

**Internal Router** : Tous interfaces dans même area

**Area Border Router (ABR)** :
- Interfaces dans Area 0 + autres areas
- Génère LSA Type 3 (Network Summary)
- Résume routes entre areas

**AS Boundary Router (ASBR)** :
- Injecte routes externes (redistribution)
- Génère LSA Type 5 (AS External)
- Peut être dans area quelconque

### Routes OSPF dans RIB

Les routes OSPF sont annoncées dans la RIB avec Types spécifiques :

| Type | Notation | Exemple |
|---|---|---|
| **Intra-area** | O | O 192.168.1.0/24 [110/10] |
| **Inter-area** | O IA | O IA 10.0.0.0/24 [110/20] |
| **External Type 1** | O E1 | O E1 172.16.0.0/16 [110/30] |
| **External Type 2** | O E2 | O E2 172.16.0.0/16 [110/20] |

## 6. Configuration OSPF de Base

### Activation Simple

```
! Configuration minimum
router ospf 100
 router-id 1.1.1.1                      ! RID recommandé
 network 192.168.1.0 0.0.0.255 area 0  ! Classful avec wildcard
 network 192.168.2.0 0.0.0.255 area 0
```

### Network Statement

**Format** : `network <network-address> <wildcard-mask> area <area-id>`

**Wildcard Mask** :
- Inverse du masque de sous-réseau standard
- Exemple : /24 (255.255.255.0) → Wildcard 0.0.0.255

```
! Exemples network statements
network 192.168.1.0 0.0.0.255 area 0     ! /24 précis
network 192.168.0.0 0.0.255.255 area 0   ! /16 large
network 0.0.0.0 255.255.255.255 area 0   ! Anywhere (passif généralement)
```

### Configuration Interface-Spécifique

```
interface Gi0/0
 ip ospf 100 area 0                      ! Alternative network statement
 ip ospf cost 50                         ! Override coût (défaut 100M/BW)
 ip ospf priority 100                    ! DR/BDR priority
 ip ospf hello-interval 10               ! Hello timer
 ip ospf dead-interval 40                ! Dead timer
 ip ospf network point-to-point          ! Force point-to-point
```

### Commandes de Vérification

```
show ip ospf                             ! État OSPF général
show ip ospf neighbor                    ! Voisins et états
show ip ospf interface                   ! État interfaces OSPF
show ip ospf database                    ! LSDB
show ip route ospf                       ! Routes OSPF dans RIB
debug ip ospf adjacency                  ! Dépannage adjacency
```

## 7. Optimisations courantes OSPF

### Cost (Métrique)

**Formule** : Cost = 100,000,000 / Bande passante (en bps)

**Exemples** :
```
1 Gbps → Cost = 100,000,000 / 1,000,000,000 = 1
100 Mbps → Cost = 100,000,000 / 100,000,000 = 10
10 Mbps → Cost = 100,000,000 / 10,000,000 = 100
1 Mbps → Cost = 100,000,000 / 1,000,000 = 100 (max OSPF)
```

**Override Coût** :
```
interface Gi0/0
 ip ospf cost 50                         ! Override défaut
```

### Détection de Défaillance

**Fast Failure Detection** :
```
interface Gi0/0
 ip ospf dead-interval minimal hello-multiplier 5
 ! Dead time = Hello × 5 (ex: 1 sec × 5 = 5 sec)
```

**Timers Standard** :
```
interface Gi0/0
 ip ospf hello-interval 10               ! 10 sec
 ip ospf dead-interval 40                ! 40 sec (4× Hello)
```

### Default Route Advertisement

```
router ospf 100
 default-information originate always [metric 10]
 ! Injecte route par défaut vers voisins OSPF
```

## 8. Points Importants à Retenir

**Concepts clés** :
1. **RID** : Identifiant unique (format IP)
2. **DR/BDR** : Rôles d'interface, élus par priorité/RID
3. **LSA** : Unités d'inondation, Types 1-5 (standard OSPFv2)
4. **LSDB** : Graphe complet de topologie
5. **SPF** : Récalculé après LSA reçue
6. **Areas** : Hiérarchie, Area 0 obligatoire

**Configuration Essentielles** :
```
router ospf 100
 router-id 1.1.1.1
 network 192.168.0.0 0.0.255.255 area 0
 network 10.0.0.0 0.0.255.255 area 1
```

**Timers standard** :
- Hello : 10 sec (Ethernet)
- Dead : 40 sec (4× Hello)

**Coût défaut** : 100M / Bandwidth

---

**Temps d'étude estimé** : 3h00  
**Préalables** : Module 6 (Concepts de routage)  
**Module suivant** : Module 9 - Advanced OSPF (Areas, LSA, Design)
