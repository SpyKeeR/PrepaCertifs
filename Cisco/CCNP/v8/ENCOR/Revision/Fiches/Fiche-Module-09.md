# Fiche Révision Module 9 : Advanced OSPF

## 1. Tableau Comparatifs - Types d'Areas

### Résumé Fonctionnalités

| Feature | Standard | Stub | Totally Stubby | NSSA |
|---------|----------|------|---|---|
| **Type 1 LSA (Router)** | ✓ | ✓ | ✓ | ✓ |
| **Type 2 LSA (Network)** | ✓ | ✓ | ✓ | ✓ |
| **Type 3 LSA (Network Summary)** | ✓ | ✓ | ✗ | ✓ |
| **Type 4 LSA (ASBR Summary)** | ✓ | ✗ | ✗ | ✗ |
| **Type 5 LSA (AS External)** | ✓ | ✗ | ✗ | ✗ |
| **Type 7 LSA (NSSA External)** | ✗ | ✗ | ✗ | ✓ |
| **ASBR redistribution local** | ✓ | ✗ | ✗ | ✓ |
| **Default route (0.0.0.0)** | Manual usually | Auto | Auto | Auto |
| **Use Case** | Default | Branch office | Small branch | ISP edge |

### Impact LSDB Size

```
Standard        : Toutes routes + Type 5 + Type 7
Stub            : Sans Type 4,5 (moins LSA)
Totally Stubby  : Sans Type 3,4,5 (très petit LSDB)
NSSA            : Type 7 seulement (local redistribution)
```

## 2. Configuration Types d'Areas

### Standard Area
```
router ospf 100
 network 192.168.1.0 0.0.0.255 area 0
 ! Aucune config area spéciale
```

### Stub Area
```
! Sur TOUS les routeurs Area 10 :
router ospf 100
 area 10 stub
 ! Sur ABR, paramètre coût défaut :
 area 10 default-cost 10
```

### Totally Stubby Area
```
! Configuration spéciale Cisco :
! Sur ABR seulement :
router ospf 100
 area 20 stub no-summary   ! "no-summary" = totally stubby
```

### NSSA
```
! Sur tous routeurs Area 30 :
router ospf 100
 area 30 nssa

! Configuration ASBR dans NSSA :
router ospf 100
 area 30 nssa
 redistribute connected subnets    ! Routes locales → Type 7
 redistribute bgp 65000 subnets   ! Routes BGP → Type 7
```

## 3. Route Summarization - Syntaxe

### Inter-area (ABR - résume intra-area)
```
router ospf 100
 area <area-id> range <network> <mask> [advertise|not-advertise] [cost <value>]
```

**Exemple** :
```
router ospf 100
 area 10 range 192.168.0.0 255.255.252.0     ! Résume 4 /24s
 area 10 range 10.0.0.0 255.255.240.0        ! Résume /16
```

### Intra-area (ASBR - résume routes redistribut)
```
router ospf 100
 summary-address <network> <mask> [not-advertise] [tag <value>]
```

**Exemple** :
```
router ospf 100
 redistribute bgp 65000 subnets
 summary-address 172.16.0.0 255.255.240.0    ! Résume 16 /24s
```

## 4. Route Filtering - Distribute-List

### Syntaxe
```
router ospf 100
 distribute-list prefix <prefix-list-name> [in|out [<interface>]]
```

### Exemples

```
! Filtre routes entrantes dans RIB
router ospf 100
 distribute-list prefix DENY-EXTERNAL in

! Filtre routes sortantes via interface
router ospf 100
 distribute-list prefix ALLOW-BGP out Gi0/0

! Filtre récursif sur interface pointant à area
router ospf 100
 distribute-list prefix ABC in Serial0/0
```

### Prefix-List Associée

```
ip prefix-list DENY-EXTERNAL seq 10 deny 172.16.0.0/12 ge 24 le 24
ip prefix-list DENY-EXTERNAL seq 20 permit 0.0.0.0/0 le 32

ip prefix-list ALLOW-BGP seq 10 permit 10.0.0.0/8 ge 16 le 24
ip prefix-list ALLOW-BGP seq 20 permit 0.0.0.0/0 le 32
```

## 5. Area Filter-List (ABR - Type 3 LSA)

### Syntaxe
```
router ospf 100
 area <area-id> filter-list prefix <prefix-list> [in|out]
```

### Exemple

```
! Filtre routes qui quittent Area 10
router ospf 100
 area 10 filter-list prefix OUT-OF-10 out

! Filtre routes qui entrent dans Area 10
router ospf 100
 area 10 filter-list prefix IN-TO-10 in

ip prefix-list OUT-OF-10 seq 10 deny 172.16.0.0/12
ip prefix-list OUT-OF-10 seq 20 permit 0.0.0.0/0 le 32
```

## 6. External Type LSA Selection

### Type 5 - AS External (Standard Route Externe)

- Générée par **ASBR** (redistribution)
- Flooded **AS-wide** (sauf NSSA areas)
- Type 1 : Métrique cumulative
- Type 2 : Métrique fixe au ASBR (par défaut)

### Type 7 - NSSA External

- Générée par **ASBR dans NSSA**
- Flooded **NSSA only**
- Traduit → Type 5 par ABR vers autre areas
- Utile pour ISP edge NSSA

## 7. External Type E1 vs E2 - Decision Tree

```
Route Externe dans RIB ?
├─ E1 disponible ?
│  └─ E2 disponible ?
│     ├─ Métrique E1 < Métrique E2 ?
│     │  ├─ OUI → Installer E1
│     │  └─ NON → Installer E2
│     └─ Seul E2 ? → Installer E2
└─ Seul E2 ? → Installer E2
```

### Configuration
```
router ospf 100
 redistribute bgp 65000 subnets metric-type 1     ! Force E1
 redistribute bgp 65000 subnets                   ! Défaut E2
```

## 8. SPF Timers - Optimization

### Syntaxe
```
router ospf 100
 timers throttle spf <initial-delay> <min-hold> <max-hold>
 ! Tous en millisecondes (ms)
```

### Valeurs Typiques

```
timers throttle spf 200 1000 5000
 ├─ 200 ms   : Délai initial avant SPF (évite SPF cascade)
 ├─ 1000 ms  : Min hold (aggravation si changements rapides)
 └─ 5000 ms  : Max hold (cap maximal)
```

## 9. OSPF Path Preference Order

```
Route Preference Hierarchy
1. Intra-area (Type O)
   └─ Coûts calculés vers destination
2. Inter-area (Type O IA)
   └─ Via ABR résumé
3. External Type 1 (Type O E1)
   └─ Métrique cumulative depuis ASBR
4. External Type 2 (Type O E2)
   └─ Métrique fixe (ne change pas distance)
```

**Règle** : Intra-area **gagne toujours** sur inter-area (même si coïts plus bas).

## 10. Stub Area Configuration Detail

```
Topology :
    Area 0 (Core)
        ↓ ABR Link
    Area 10 (Stub)
        ├── R1 (Internal)
        ├── R2 (Internal)
        └── ABR

Config :
# Sur R1 :
router ospf 100
 area 10 stub

# Sur R2 :
router ospf 100
 area 10 stub

# Sur ABR :
router ospf 100
 area 10 stub
 area 10 default-cost 20    ! Coût vers 0.0.0.0/0
```

## 11. NSSA Configuration Detail

```
Topology :
    Area 0
        ↓ ABR Link
    Area 30 (NSSA)
        ├── R1 (Internal)
        └── R2 (ASBR + Internal)
            ↓ Redistribution
        BGP 65000

Config :
# Sur R1 :
router ospf 100
 area 30 nssa

# Sur R2 (ASBR) :
router ospf 100
 area 30 nssa
 redistribute bgp 65000 subnets
 ! Type 7 LSA flooded vers tout NSSA
 ! ABR traduit Type 7 → Type 5 vers Area 0
```

## 12. Mind Map - Advanced OSPF Topics

```
ADVANCED OSPF
├── Area Types
│   ├── Standard (default, toutes LSA types)
│   ├── Stub (sans Type 4,5)
│   ├── Totally Stubby (sans Type 3,4,5)
│   └── NSSA (Stub + Type 7)
├── Summarization
│   ├── Inter-area (ABR `area range`)
│   └── Intra-area (ASBR `summary-address`)
├── Filtering
│   ├── Distribute-list (routes RIB)
│   └── Area filter-list (Type 3 LSAs)
├── External Routes
│   ├── Type 5 (AS-wide)
│   ├── Type 7 (NSSA-only)
│   ├── E1 (métrique cumulative)
│   └── E2 (métrique fixe)
├── Optimization
│   ├── SPF timers throttle
│   ├── LSDB reduction (stub areas)
│   └── Route filtering
└── Design Patterns
    ├── Hub-Spoke (central Area 0)
    ├── Fully Meshed (backbone)
    └── Discontiguous avoidance
```

## 13. Checklist Configuration Avancée

- [ ] Area type correct (Standard/Stub/NSSA)
- [ ] ABR range summarization pour inter-area
- [ ] Distribute-list ou filter-list pour filtrage
- [ ] ASBR summary-address pour routes redistribut
- [ ] External type (E1 vs E2) configuré correctement
- [ ] SPF timers optimisé si nécessaire
- [ ] NSSA translation ABR vérifiée (si applicable)
- [ ] Discontiguous networks évité ou gérés
- [ ] Routes dans RIB vérifiées (show ip route ospf)
- [ ] Adjacencies Full dans toutes areas

## 14. Pièges Avancés Courants

❌ Oublier configurer `area X stub` sur **TOUS les routeurs** Area X  
❌ Stub Area sans configuration default-cost (ABR defaults à 1)  
❌ Stub Area avec ASBR local (impossible, utiliser NSSA)  
❌ Area filter-list en `in` sur ABR (souvent inversé)  
❌ Summarization trop agressif (routes null)  
❌ Extern Type E1 configuration oubliée (E2 par défaut)  
❌ SPF timers trop optimisés (instabilité)  
❌ Discontiguous networks sans plan (routes imprévisibles)

---
**Temps révision** : 50 min | **Niveau** : Avancé
