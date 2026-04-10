# Fiche Révision Module 10 : OSPFv3

## 1. OSPFv3 vs OSPFv2 - Tableau Comparatif

| Critère | OSPFv2 | OSPFv3 |
|---------|--------|--------|
| **IP Version** | IPv4 uniquement | IPv6 natif (+ IPv4 via AF) |
| **Multicast Hello** | 224.0.0.5 | FF02::5 |
| **Multicast DR/BDR** | 224.0.0.6 | FF02::6 |
| **Router ID** | IPv4 format | IPv4 format (même IPv6) |
| **Link-Local** | Non utilisé | OBLIGATOIRE |
| **Hello Source** | Adresse interface | Link-Local |
| **Next-Hop** | Adresse interface | Link-Local |
| **Auth Method** | MD5 | IPsec |
| **LSA Types** | 1-7 | 1-8 (8 = Prefix) |
| **Process ID** | ospf `number` | ospfv3 `number` |

## 2. Adresses IPv6 en OSPFv3

### Global Unicast Address (GUA)
```
2001:db8:1::1/64     ! Public/routé (utilisation)
2001:db8:2::1/64     ! Routage inter-area
```

### Link-Local Address (LLA)
```
fe80::1/10           ! OBLIGATOIRE pour voisinage
fe80::2/10           ! Générée auto ou config
```

**Configuration Complète** :
```
interface Gi0/0
 ipv6 address 2001:db8:1::1/64              ! GUA
 ipv6 address fe80::1 link-local            ! LLA explicite
 ipv6 ospf 100 area 0
```

## 3. Router ID OSPFv3

### Sélection (Ordre)
1. **Configuré explicitement** (recommandé)
2. Highest loopback IPv4

3. Highest physical IPv4

### Configuration
```
router ospfv3 100
 router-id 1.1.1.1              ! Format IPv4 (requis)
```

## 4. Configuration de Base OSPFv3

### IPv6 Simple
```
router ospfv3 100
 router-id 1.1.1.1

interface Gi0/0
 ipv6 address 2001:db8:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 ospf 100 area 0

interface Gi0/1
 ipv6 address 2001:db8:2::1/64
 ipv6 address fe80::2 link-local
 ipv6 ospf 100 area 1
```

### IPv4 + IPv6 (Address Families)
```
router ospfv3 100
 router-id 1.1.1.1

 address-family ipv4 unicast
  network 192.168.1.0 0.0.0.255 area 0
  exit-address-family

 address-family ipv6 unicast
  network 2001:db8:1::/48 area 0
  exit-address-family

interface Gi0/0
 ip address 192.168.1.1 255.255.255.0
 ipv6 address 2001:db8:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 ospf 100 area 0
```

## 5. Timers OSPFv3

### Defaults
| Type | Valeur |
|---|---|
| **Hello Interface** | 10 sec |
| **Dead Interval** | 40 sec (4× Hello) |
| **Retransmit** | 5 sec |

### Configuration
```
interface Gi0/0
 ipv6 ospf hello-interval 5                ! 5 secondes
 ipv6 ospf dead-interval 20                ! 20 sec (4×5)
 ipv6 ospf retransmit-interval 3           ! LSU retransmit
 ipv6 ospf transmit-delay 1                ! Ajout délai LSU
```

## 6. DR/BDR Election

### Priorité
```
interface Gi0/0
 ipv6 ospf priority 100              ! 0-255, défaut 1
 ! 0 = Never DR/BDR
```

### Election
- **1ère** : Priorité (plus haute)
- **2e** : RID (plus élevé si priorité égale)

## 7. Cost/Métrique

### Formule (Identique OSPFv2)
$$Coût = \frac{100,000,000}{Bande\_passante\_{(bps)}}$$

### Configuration
```
interface Gi0/0
 ipv6 ospf cost 50              ! Force coût 50
```

## 8. LSA Types OSPFv3

### Types 1-8

```
1 : Router LSA (Topologie routeur)
2 : Network LSA (Réseau multi-accès)
3 : Inter-Area Prefix LSA (Routes résumées)
4 : Inter-Area Router LSA (ASBR annonce)
5 : AS External Prefix LSA (Routes externes)
6 : Group Membership (Obsolete)
7 : NSSA External LSA (NSSA routes)
8 : Link Prefix LSA (IPv6 prefix per-link)  ← NEW
```

### Type 8 - Link Prefix LSA
- Scope = single link (plus petit flooder)
- Optimisation pour IPv6 prefixes
- Séparation topologie de prefixes

## 9. Commandes Vérification OSPFv3

### État Général
```
show ipv6 ospf [process-number]        ! OSPFv3 résumé
show ipv6 ospf interface               ! Interfaces OSPFv3
show ipv6 ospf interface detail        ! Détails full
show ipv6 ospf neighbor                ! Voisins et états
show ipv6 ospf neighbor detail         ! Detail voisins
```

### LSDB et Routes
```
show ipv6 ospf database                ! LSDB complète
show ipv6 ospf database router         ! Type 1 LSAs
show ipv6 ospf database network        ! Type 2 LSAs
show ipv6 ospf database prefix         ! Type 8 LSAs

show ipv6 route ospf                   ! Routes OSPFv3
show ipv6 route [prefix]               ! Route spécifique
```

### Adjacency Detail
```
show ipv6 ospf neighbor gi0/0 detail   ! Detail voisin interface
debug ipv6 ospf adjacency              ! Dépannage adjacency
debug ipv6 ospf spf                    ! Trace SPF calculs
```

## 10. Address Families en OSPFv3

### Concept
Chaque AF = topologie indépendante

```
Process OSPFv3 100
├── AF IPv4
│   ├── Topology séparée
│   ├── LSDB propre
│   ├── RIB IPv4
│   └── SPF calc indépendant
└── AF IPv6
    ├── Topology séparée
    ├── LSDB propre
    ├── RIB IPv6
    └── SPF calc indépendant
```

## 11. Link-Local Addressing Détail

### Importance
- **OBLIGATOIRE** pour adjacence OSPFv3
- Source de tous paquets OSPF
- Next-hop dans routes
- Hello source adresse

### Format
```
fe80::[Interface ID]

Exemple :
 fe80::1      → link-local du routeur
 fe80::FFFF:192.168.1.1  → généré from IPv4
```

### Configuration
```
interface Gi0/0
 ipv6 address fe80::1 link-local    ! Config manuel
 ! ou auto-generated fe80::...
```

## 12. Authentification OSPFv3

### IPsec pour OSPFv3
```
ip ospf authentication ipsec spi <spi> <algorithm> <key>
```

### Exemple
```
ip ospf authentication ipsec spi 256 md5 1234567890ABCDEF1234567890ABCDEF
```

## 13. Stub/NSSA Areas en OSPFv3

### Configuration Stub Area
```
router ospfv3 100
 area 10 stub
 area 10 default-cost 10
```

### Configuration NSSA
```
router ospfv3 100
 area 20 nssa
 
! ASBR dans NSSA :
 redistribute bgp 65000 subnets
```

## 14. Configuration Multi-Area OSPFv3

```
Area 0 (Backbone)
├── Gi0/0 : 2001:db8:1::1/64
├── Gi0/1 : 2001:db8:2::1/64 → Area 1
└── Gi0/2 : 2001:db8:3::1/64 → Area 2

Configuration :
router ospfv3 100
 router-id 1.1.1.1
 area 0 range 2001:db8:1::/48
 area 1 range 2001:db8:2::/48

interface Gi0/0
 ipv6 address 2001:db8:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 ospf 100 area 0

interface Gi0/1
 ipv6 address 2001:db8:2::1/64
 ipv6 address fe80::2 link-local
 ipv6 ospf 100 area 1
```

## 15. Checklist Configuration OSPFv3

- [ ] Router ID configuré (IPv4 format)
- [ ] Link-Local addresses sur toutes interfaces
- [ ] Global Unicast addresses configurées
- [ ] `ipv6 ospf [AS] area [X]` activé
- [ ] Voisins détectés (show ipv6 ospf neighbor)
- [ ] États Full établis
- [ ] Routes dans RIB (show ipv6 route ospf)
- [ ] Address Families si IPv4 également
- [ ] Redistribution si nécessaire
- [ ] Timers vérifiés/optimisés

## 16. Pièges Courants OSPFv3

❌ Oublier Link-Local (LLA) sur interfaces  
❌ Confondre OSPFv3 IPv4 AF avec OSPFv2  
❌ Router ID au format IPv6 (DOIT être IPv4)  
❌ Pas de GUA configurée (LLA seul insuffisant)  
❌ Adjacency stuck (problème LLA/timers)  
❌ Address Family oubliée (pas routes IPv4)  
❌ IPsec authentication incorrecte (OSPFv3 vs v2)

---
**Temps révision** : 35 min | **Niveau** : Basique-Intermédiaire
