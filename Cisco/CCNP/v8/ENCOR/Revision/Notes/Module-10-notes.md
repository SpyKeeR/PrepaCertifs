# Module 10 : OSPFv3 - Notes Détaillées

## Introduction

OSPFv3 est l'évolution d'OSPF pour supporter nativement IPv6 (et IPv4 via Address Families). Il améliore OSPFv2 avec support du routage IPv6, une architecture de protocole améliorée, et une meilleure scalabilité. Ce module couvre les concepts OSPFv3, les différences clés avec OSPFv2, la configuration IPv6, et le support IPv4 dans OSPFv3 via Address Families.

## Concepts Clés OSPFv3

- **IPv6 Support** : Routage natif IPv6
- **Link-Local Addresses** : Utilisées pour adjacency
- **Address Families** : Support IPv4 et IPv6 simultanément
- **LSA Types Nouveaux** : Types spécifiques IPv6
- **Front-Seat Topology** : Interface-unique LSA scope
- **Router ID** : Format IPv4 (32 bits) même en IPv6
- **Prefix LSA** : Type 8 LSA pour IPv6 prefixes
- **Anycast Address** : Support IPv6 anycast

## 1. OSPFv3 vs OSPFv2 - Différences Clés

### Tableau Comparatif

| Aspect | OSPFv2 | OSPFv3 |
|--------|--------|--------|
| **Version IP** | IPv4 seulement | IPv6 natif (+ IPv4 via AF) |
| **Hello Protocol** | IPv4 multicast 224.0.0.5 | IPv6 multicast FF02::5 |
| **Router ID** | IPv4 (32 bits) | IPv4 (32 bits) |
| **Link Local** | N/A | Utilisé pour adjacency |
| **LSA Types** | 1-7 | 1,2,3,4,5,6,7,8 (8 = Prefix) |
| **SPF Algorithm** | Dijkstra (inchangé) | Dijkstra (inchangé) |
| **Areas** | Supportées | Supportées |
| **Authentication** | MD5 dans IPv4 header | IPsec dans IPv6 |
| **Segment Routing** | Non (v2 legacy) | Supporté (modern OSPFv3) |
| **Scalability** | Par zones | Par zones + topologies |

### Améliorations Principales

**OSPFv3 améliore** :
1. **Support IPv6** : Routage native 128-bits
2. **Flooding** : Plus efficace (interface-centric)
3. **Topology Calculation** : Optimisée pour IPv6
4. **Address Families** : Support IPv4 + IPv6 simultanément

## 2. IPv6 Fundamentals dans OSPFv3

### Adresses IPv6 en OSPF

#### Global Unicast Address (GUA)
- Adresse IPv6 publique (2000::/3)
- Utilisée pour routage global
- Format : 2001:db8::/32 (example documentaire)

#### Link-Local Address (LLA)
- Adresse locale au lien (fe80::/10)
- **OBLIGATOIRE** pour adjacency OSPFv3
- Générée automatiquement ou configurée
- Format : fe80::x/10

**Exemple** :
```
Interface Gi0/0
 ipv6 address 2001:db8:1::1/64        ! GUA
 ipv6 address fe80::1 link-local       ! LLA
```

#### Link-Local Scoping

OSPFv3 utilise **link-local** pour :
- Paquets Hello (directement voisin)
- Database Description (DD)
- Link State Requests (LSR)
- Link State Updates (LSU)
- Link State Acknowledgments (LSAck)

**Adresse next-hop OSPF** = **Link-Local** du voisin (pas GUA).

### Router ID OSPFv3

**Format** : IPv4 32-bits (même en IPv6).

**Sélection** (identique OSPFv2) :
1. Configured `router-id` (recommandé)
2. Highest loopback IPv4 address
3. Highest physical interface IPv4 address

**Configuration** :
```
router ospfv3 100
 router-id 1.1.1.1           ! Format IPv4
```

## 3. OSPFv3 Configuration de Base

### Activation OSPFv3

```
! Process OSPFv3 (format identique OSPF)
router ospfv3 100
 router-id 1.1.1.1

! Configuration interface
interface Gi0/0
 ipv6 address 2001:db8:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 ospf 100 area 0            ! Activation par interface
```

### Address Family Configuration

OSPFv3 peut supporter IPv4 et IPv6 via **Address Families** :

```
! IPv6 (par défaut)
router ospfv3 100
 router-id 1.1.1.1
 address-family ipv6 unicast
  network 2001:db8:1::/48 area 0

! IPv4 (via Address Family)
address-family ipv4 unicast
  network 192.168.1.0 0.0.0.255 area 0
```

### Configuration Multi-Area OSPFv3

```
router ospfv3 100
 router-id 1.1.1.1

interface Gi0/0
 ipv6 address 2001:db8:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 ospf 100 area 0         ! Area 0 (Backbone)

interface Gi0/1
 ipv6 address 2001:db8:2::1/64
 ipv6 address fe80::2 link-local
 ipv6 ospf 100 area 1         ! Area 1
```

## 4. OSPFv3 Address Families (IPv4 et IPv6)

### Concept

OSPFv3 **peut supporter IPv4 et IPv6 simultanément** via Address Families.

```
Process OSPFv3 100
├── Address Family IPv6
│   ├── Topology IPv6
│   ├── Interfaces IPv6
│   └── Routes IPv6
└── Address Family IPv4
    ├── Topology IPv4
    ├── Interfaces IPv4
    └── Routes IPv4
```

### Configuration IPv4 in OSPFv3

```
router ospfv3 100
 router-id 1.1.1.1

 address-family ipv4 unicast
  network 192.168.1.0 0.0.0.255 area 0
  network 192.168.2.0 0.0.0.255 area 0
  exit-address-family

 address-family ipv6 unicast
  network 2001:db8:1::/48 area 0
  network 2001:db8:2::/48 area 0
  exit-address-family
```

### Topologies Séparées

Chaque Address Family a :
- **Topologie indépendante** (LSA/LSDB séparées)
- **RIB distinct** (routes IPv4 vs IPv6)
- **SPF calc indépendant** (performance)

## 5. LSA Types OSPFv3

### LSA Types en OSPFv3

| Type | Nom | Scope | Fonction | IPv4/IPv6 |
|---|---|---|---|---|
| **1** | Router LSA | Area | Liens du routeur | Both |
| **2** | Network LSA | Area | Réseau multi-accès | Both |
| **3** | Inter-Area Prefix | Area | Routes inter-area | Both |
| **4** | Inter-Area Router | Area | ASBR inter-area | Both |
| **5** | AS External Prefix | AS-wide | Routes externes | Both |
| **6** | Group Membership | (obsolete) | N/A | Both |
| **7** | Type 7 NSSA | NSSA | Routes NSSA | Both |
| **8** | Link Prefix LSA | Link | IPv6 prefixes | IPv6 only |

### Type 8 LSA - Prefix IPv6 (NEW in OSPFv3)

**Rôle** : Annonce prefixes IPv6 séparés de la topologie.

**Caractéristiques** :
- Scope = un seul lien (plus petit)
- Réduit flooding pour changements prefix
- Efficace pour IPv6 prefix management

## 6. Adjacency OSPFv3

### Formation d'Adjacency

Formation identique OSPFv2 (8 états), utile avec IPv6 :

```
Down → Init → 2-Way → ExStart → Exchange → Loading → Full
```

**Condition spécifique IPv6** :
- **Link-Local Source Required** : Hello source = LLA
- **LLA Used in Database Exchange** : DD/LSR/LSU via LLA
- **Next-Hop = LLA** : Routes pointent vers LLA du voisin

## 7. Authentification OSPFv3

### IPsec Authentication

OSPFv3 utilise **IPsec** pour l'authentification (vs MD5 OSPFv2).

```
! Configuration IPsec pour OSPFv3
ip ospf authentication ipsec spi 256 md5 1234567890ABCDEF1234567890ABCDEF
```

**Avantages IPsec** :
- Standard (vs Cisco-specific MD5)
- Strong encryption options
- Integrated with IPv6 security

## 8. Configuration Avancée OSPFv3

### Timers OSPFv3

Identique OSPFv2 :
```
interface Gi0/0
 ipv6 ospf hello-interval 10
 ipv6 ospf dead-interval 40
```

### Coûts d'Interface

```
interface Gi0/0
 ipv6 ospf cost 50          ! Override coût (défaut basé BW)
```

### DR/BDR Election

Identique OSPFv2 (priorité + RID) :
```
interface Gi0/0
 ipv6 ospf priority 100     ! DR priority
```

## 9. Migration OSPFv2 → OSPFv3

### Stratégies de Migration

**Parallel Running** :
1. Configurer OSPFv3 avec IPv6
2. Maintenir OSPFv2 pour IPv4
3. Vérifier convergence
4. Retirer OSPFv2 (ou utiliser OSPFv3 Address Family IPv4)

**Cutover Complete** :
1. Migrer OSPFv2 → OSPFv3 IPv4 (Address Family)
2. Ajouter IPv6 address family
3. Vérifier toutes routes

### Vérification Convergence

```
show ipv6 ospf                    ! État OSPFv3
show ipv6 ospf neighbor           ! Voisins IPv6
show ipv6 ospf database          ! LSDB
show ipv6 route ospf             ! Routes OSPFv3
show ipv6 route                  ! RIB complet
```

## 10. Points Importants à Retenir

**Router ID OSPFv3** :
- Format IPv4 (32-bits) même pour IPv6
- Doit être configuré explicitement

**Link-Local Addresses** :
- OBLIGATOIRES pour adjacency OSPFv3
- Utilisé pour tout trafic OSPF
- Next-hop = LLA du voisin

**Address Families** :
- IPv4 et IPv6 topologies indépendantes
- LSDB séparées par AF
- SPF calcul par AF

**LSA Type 8** :
- Nouveau en OSPFv3
- Scope lien (prefix IPv6)
- Efficacité flooding

**Authentication** :
- OSPFv2 = MD5
- OSPFv3 = IPsec (standard)

---

**Temps d'étude estimé** : 2h00  
**Préalables** : Module 8 (OSPF fondamentals), IPv6 basics  
**Module suivant** : Révision complète modules 6-10
