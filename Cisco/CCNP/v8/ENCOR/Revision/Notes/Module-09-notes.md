# Module 9 : Advanced OSPF - Notes Détaillées

## Introduction

Le Module 8 a couvert les fondamentaux OSPF. Ce module avancé approfondit les architectures complexes, les types d'area spécialisés, le design hiérarchique, le résumé des routes inter-area, le filtrage, et les optimisations de performance. Ces concepts sont essentiels pour déployer OSPF dans les réseaux d'entreprise à grande échelle, ce qui est un aspect clé de la certification CCNP ENCOR.

## Concepts Clés Avancés

- **Multi-area Design** : Hiérarchie backbone + areas standards
- **Stub Areas** : Réduction LSDB sans routes externes
- **Totally Stubby Areas** : Plus agressif, pas même routes inter-area
- **NSSA (Not-So-Stubby Area)** : Stub Area qui accepte routes externes de redistribution
- **Area Types Comparison** : Quand utiliser chaque type
- **Route Summarization** : Inter-area vs Intra-area
- **Route Filtering** : Distribuer-list, prefix-lists
- **ABR Filtering** : Contrôle routes inter-area

## 1. OSPF Areas - Design Avancé

### Concept Hiérarchique

OSPF divise le domaine en Areas pour réduire complexité :

```
OSPF Domain (AS)
├── Area 0 (Backbone - OBLIGATOIRE)
│   └── Internal Routers + ABRs
├── Area 11 (Standard Area)
│   ├── Internal Routers
│   └── ABR (connecte Area 0)
├── Area 21 (Stub Area)
│   ├── Internal Routers
│   └── ABR (connecte Area 0)
├── Area 22 (NSSA)
│   ├── Internal Routers
│   ├── ASBR local possible
│   └── ABR (connecte Area 0)
└── Area 30 (Totally Stubby)
    ├── Internal Routers
    └── ABR (connecte Area 0)
```

### Types d'Areas et Avantages

| Area Type | Accepte | Rejette | RIB Impact | Cas d'usage |
|---|---|---|---|---|
| **Standard** | Type 1,2,3,4,5 | - | Routes toutes | Default |
| **Stub** | Type 1,2,3 | Type 4,5 | Pas externes | Branch office |
| **Totally Stubby** | Type 1,2 | Type 3,4,5 | Que intra-area + défaut | Small branch |
| **NSSA** | Type 1,2,3,7 | Type 4,5 | Routes externes locales | ISP redistrib |

## 2. Stub Areas

### Concept

Stub Area = Area qui **rejette LSA Type 4 et 5** (routes externes).

**Avantages** :
- Réduit taille LSDB (pas de Type 5 LSAs)
- CPU/Mémoire réduits
- Convergence plus rapide
- Idéal pour branch offices

**Limitation** : Routes vers réseaux externes via route par défaut (0.0.0.0/0).

### Configuration

```
! Sur ALL routeurs dans la Stub Area (dont ABR) :
router ospf 100
 area 21 stub
 default-cost 10                  ! Coût défaut route 0.0.0.0/0 (ABR)
```

### Propagation Route par Défaut

L'ABR génère automatiquement route par défaut (0.0.0.0/0) vers Stub Area via Type 3 LSA quand area configured `stub`.

**Vérification** :
```
show ip route                      ! Vérifie 0.0.0.0/0 présente
show ip ospf database summary      ! Type 3 LSA pour défaut
```

## 3. Totally Stubby Areas

### Concept

Totally Stubby Area = Stub Area qui **rejette aussi LSA Type 3 inter-area**.

**Configuration** :
```
! Sur ABR seulement :
router ospf 100
 area 30 stub no-summary          ! Syntaxe Cisco spéciale
```

**Impact** :
- LSDB même plus petit (pas Type 3 inter-area)
- Seule route par défaut 0.0.0.0/0 pour inter-area
- Trafic inter-area + externes via défaut

**Restriction** : Cisco spécifique (pas standard OSPF).

## 4. NSSA (Not-So-Stubby Area)

### Concept

NSSA = Stub Area + Permet ASBR local avec redistribution.

**Problème résolu** : Stub Area rejette tous les Type 5 (routes externes). NSSA accepte Type 7 LSAs (routes externes NSSA) générées par ASBRs locaux.

### Configuration

```
! Sur tous les routeurs dans Area 22 (NSSA) :
router ospf 100
 area 22 nssa

! Configuration ASBR redistribution dans NSSA :
router ospf 100
 area 22 nssa
 redistribute bgp 65000 subnets    ! Routes BGP deviennent Type 7 LSAs
```

### Type 7 vs Type 5 LSAs

| Propriété | Type 5 | Type 7 |
|---|---|---|
| **Scope** | AS-wide | NSSA only |
| **Généré par** | ASBR n'importe où | ASBR dans NSSA |
| **Accepté dans** | Toutes areas (sauf NSSA) | NSSA seulement |
| **Translation** | - | ABR→Type 5 si quitte NSSA |

### Translation Type 7 → Type 5

Quand Type 7 LSA quitte NSSA vers Area 0 :
1. **ASBR in NSSA** genère Type 7
2. **ABR (NSSA Border)** retraduit Type 7 → Type 5
3. **Type 5 flooded** vers autres areas

**Configuration ABR translation** (Cisco) :
```
router ospf 100
 area 22 nssa filter-list prefix FROM-NSSA in   ! Filtre Type 7
```

## 5. Route Summarization Avancé

### Types de Summarization

#### Inter-area Summarization (ABR)

L'ABR **résume intra-area routes** quand les annonce vers d'autres areas :

```
router ospf 100
 area 21 range 192.168.0.0 255.255.252.0    ! Résume 4 à 1 route
 area 21 range 10.0.0.0 255.255.240.0
```

**Avantages** :
- Réduit Type 3 LSAs flooded
- Stabilise inter-area topology changes
- Résume routes indisponibles vers null (si configuré)

#### Intra-area Summarization (ASBR)

L'ASBR peut résumer routes **redistribuées** :

```
router ospf 100
 redistribute bgp 65000 subnets
 summary-address 172.16.0.0 255.255.240.0        ! Résume routes externes
```

### Route Suppression (Not Advertise)

Routes pas couvertes par résumé peuvent être supprimées :
```
router ospf 100
 area 21 range 192.168.0.0 255.255.252.0 not-advertise
 ! Cette route n'est pas annoncée (suppression totale)
```

## 6. Route Filtering Avancé

### Distribute-List (Legacy mais puissant)

```
! Filtre routes OSPF basées sur ACL/Prefix-list
router ospf 100
 distribute-list prefix IMPORT-FILTER in       ! Filtre entrées 
 distribute-list prefix EXPORT-FILTER out Gi0/1 ! Filtre sorties

ip prefix-list IMPORT-FILTER seq 10 permit 192.168.0.0/16
ip prefix-list IMPORT-FILTER seq 20 deny 192.168.100.0/24
ip prefix-list IMPORT-FILTER seq 30 permit 0.0.0.0/0 le 32
```

### Area Filter-List (ABR)

Filtre Type 3 LSAs **entre areas** :

```
router ospf 100
 area 20 filter-list prefix OUT-FILTER-20 out  ! Sort de Area 20
 area 20 filter-list prefix IN-FILTER-20 in    ! Entre dans Area 20

ip prefix-list OUT-FILTER-20 seq 10 permit 10.100.0.0/16
ip prefix-list OUT-FILTER-20 seq 20 deny 10.200.0.0/16
ip prefix-list OUT-FILTER-20 seq 30 permit 0.0.0.0/0 le 32
```

## 7. OSPF Path Selection Avancé

### Intra-area vs Inter-area vs External

OSPF préfère les routes dans cet ordre (path calculation) :
1. **Intra-area** (Type O)
2. **Inter-area** (Type O IA)
3. **External Type 1** (Type O E1) - métrique cumulative
4. **External Type 2** (Type O E2) - métrique fixe au boundary

### External Type E1 vs E2

| Propriété | E1 | E2 |
|---|---|---|
| **Métrique** | Cumulative (ASBR→dest) | Fixe au ASBR |
| **Exemple RIB** | [110/25] | [110/20] |
| **Préférence** | E1 si coût E1 < E2 | Défaut si coût E2 standard |
| **Configuration** | `redistribute ... metric-type 1` | Défaut (metric-type 2) |

## 8. Discontiguous Networks

### Problème

Réseaux discontigus = deux areas avec même subnet mais via routes différentes.

```
Area 0 ← ABR1 → Area 1
         ↓
    10.0.0.0/24
       ↓
    Area 2 ← ABR2 → Autre 10.0.0.0/24
```

**Problème** : OSPF résume automatiquement à limites classiques (risque routes null).

### Solution : Disable auto-summary (Concept Area)

Contrairement EIGRP, OSPF **n'a pas auto-summary**. Résumé manuel via:
```
router ospf 100
 area 1 range 10.0.0.0 255.255.255.0     ! Rendre dépendant du réseau
 area 2 range 10.0.0.0 255.255.255.0     ! Chaque area résume distinct
```

## 9. Optimisation Performance OSPF

### Reducing SPF Computation

**Timers SPF** :
```
router ospf 100
 timers throttle spf 200 1000 5000    ! Init delay, backoff min, max
```

- **200 ms** : Délai initial avant premier SPF
- **1000 ms** : Délai backoff min (augmente si changements rapides)
- **5000 ms** : Délai backoff max (cap de convergence)

### Reducing LSDB Size

**Methods** :
1. Utiliser Stub/Totally Stubby/NSSA areas
2. Résumer routes (area range, summary-address)
3. Filtrer routes (distribute-list, filter-list)

### Interface-Level Optimizations

```
interface Gi0/0
 ip ospf network broadcast              ! Force broadcast type
 ip ospf demand-circuit                 ! Suppress hello on stable link
 ip ospf db-filter all out             ! Ne pas flood vers routeur
```

## 10. Discontiguous Networks Detail

### Exemple Problématique

```
Area 0                Area 1
 10.0.1.0/24          10.0.2.0/24
 10.0.3.0/24          (Area 1 verra résumé 10.0.0.0/16 depuis Area 0)
```

Si Area 1 injecte les propres 10.0.2.0/24, il y a ambiguïté (deux routes même subnet).

### Limitations OSPF

Contrairement EIGRP (qui le refuse), OSPF **accepte discontiguous networks**. Mais RIB installations peuvent être **imprévisibles**.

**Solution** :
- Éviter discontiguous si possible (redesign)
- Si nécessaire : ne pas résumer, utiliser full routes

## 11. Points Importants à Retenir

**Area Types** :
- **Standard** : Défaut, accepte tout
- **Stub** : Rejette Type 4,5 (externes)
- **Totally Stubby** : Rejette Type 3,4,5
- **NSSA** : Stub + Type 7 local

**Summarization** :
- ABR : `area X range` (résume intra-area)
- ASBR : `summary-address` (résume routes redistribut)

**Filtering** :
- `distribute-list` : Legacy mais flexible
- `area filter-list` : Type 3 LSA filtering

---

**Temps d'étude estimé** : 3h00  
**Préalables** : Module 8 (OSPF Fundamentals)  
**Module suivant** : Module 10 - OSPFv3 (IPv6)
