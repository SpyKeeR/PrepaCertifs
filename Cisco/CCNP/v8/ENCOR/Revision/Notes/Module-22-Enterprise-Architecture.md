---
title: "Module 22: Architecture du réseau d'entreprise"
module: 22
type: notes
topics: [network-architecture, hierarchical-design, access-distribution-core, two-tier, three-tier, leaf-spine, routed-access]
difficulty: intermediate
updated: 2026-03-18
---

# Module 22: Architecture du réseau d'entreprise

## Vue d'ensemble
L'architecture réseau d'entreprise moderne s'appuie sur une conception hiérarchique modulaire offrant performance, scalabilité, et isolation des défauts. Ce module couvre les modèles de conception (2-tier, 3-tier), les fonctions de chaque couche, et les alternatives modernes (leaf-spine, SD-Access).

## Principes conception hiérarchique

### Bénéfices fondamentaux

**1. Performance**
- **Décomposition tâches**: Chaque couche spécialisée (accès=switching simple, distribution=aggregation+routing, core=backbone)
- **Réduction latence**: Chemin optimal via hierarchical routing
- **Prévisibilité**: QoS boundaries clairs, no bottlenecks traversal

**2. Scalabilité**
- **Modularité couche**: Ajouter access switches sans re-architecture core
- **Croissance non-disruptive**: New buildings/segments via distribution pairs
- **Gestion taille routing**: IP summarization at distribution = smaller core routing tables (can scale 100.000+ routes)

**3. Isolation et confinement défauts**
- **STP boundary**: L2 loops contained within tier (no campus-wide blocking)
- **Routing isolation**: Failed access switch = loss segment only, not entire campus
- **Fault domain**: Layer 2 spanning tree limited to access+distribution, not core

**4. Maintenabilité**
- **Simplified troubleshooting**: Fault likely within affected tier/switch-pair
- **Organized cabling**: Strategic port/VLAN allocation per layer
- **Standardized design**: Repeatable architecture across buildings

---

## Modèle trois couches (3-Tier Hierarchical Design)

### Couche 1: Access Layer (Réseau des utilisateurs/Edge)

#### Rôle et fonction
L'access layer est where users/endpoints physically connect au réseau via Gigabit Ethernet (câblé) ou wireless APs (sans fil).

**Responsabilités Access Layer:**
- **User connectivity**: Fournir ports physiques pour endpoints (workstations, printers, VoIP phones)
- **VLAN segmentation**: Attribuer clients à VLANs (security, performance, management isolation)
- **QoS trust boundary**: Mark packets with CoS/DSCP valeurs pour downstream prioritization
- **Prevent bridging loops**: Access switches ne doivent **pas inter-connectés** directement
- **Port security**: Basic security (802.1x, port-security MAC limits, etc.)

#### Design caractéristiques Access Layer

| Aspect | Détail |
|--------|--------|
| **Topologie** | Star: All endpoints → single access switch (no direct peer-to-peer) |
| **Interconnectivité** | **No mesh interconnects** between access switches |
| **Spanning Tree** | Not needed within access switches (no loops possible) |
| **Routing** | Layer 2 only (switches), all inter-vlan via distribution gateway |
| **VLAN scope** | Single access switch (limited loop risk) OR Multiple switches if STP used |
| **Link capacity** | Gigabit Ethernet (1G minimum), 10G optional for power users |
| **Wireless** | APs associate to WLC, clients VLAN assigned per AP SSID |

#### Access layer devices
```
Physical: Catalyst 2900/3900 Series switches (stackable common)
├─ Ports: 24/48 Gigabit Ethernet typically
├─ PoE: Power-over-Ethernet (APs, VoIP phones)
├─ Optional: L3 module for direct routing (Advanced tier design)
└─ Uplink: Dual uplinks to distribution switches (redundancy)

Wireless: Cisco Catalyst 9100/9115 Access Points
├─ Radio: Dual-band (2.4 + 5 GHz) 802.11n/ac/ax
├─ Association: Static to primary WLC (management)
├─ Failover: Secondary WLC for HA (if configured)
└─ Client traffic: Tunneled to WLC (split-MAC architecture)
```

### Couche 2: Distribution Layer (Agrégation et limites L2/L3)

#### Rôle et fonction
Distribution layer agrège access switches, définit routing boundaries, et distributes services (security, QoS, policy marking).

**Responsabilités Distribution Layer:**
- **Access aggregation**: Consolidate access switches sous distribution pairs
- **L2/L3 boundary**: Perform inter-vlan routing (Layer 3 gateway for all access VLANs)
- **Policy distribution**: QoS remarking, ACLs, filtering per access tier
- **Redundancy**: Paired switches pour high availability (active/active or active/passive)
- **STP boundary**: Define switch instance boundaries (limits L2 fault propagation)
- **IP address summarization**: Advertise aggregated subnets to core (reduce core routing tables)

#### Design caractéristiques Distribution Layer

| Aspect | Détail |
|--------|--------|
| **Topologie** | Paired deployment: Distribution-A + Distribution-B |
| **Inter-pair links** | L2 link (STP trunk) OR L3 link (point-to-point routing) |
| **Access connection** | Multiple access switches to each distribution switch |
| **STP role** | Defines RSTP instance boundaries, root bridge for access subtree |
| **Routing** | Layer 3 primary function: OSPF, BGP, or static routes |
| **Link capacity** | 10G uplinks to core (40G optional large campus) |
| **Port count** | 48-96 ports typical for aggregation load |

#### Distribution layer devices
```
Physical: Catalyst 4900 or 6800 Series (typical campus)
├─ Advanced LAN modules: L3 modules, redundancy features
├─ Throughput: Line-rate processing for all access switches
├─ Redundancy: Active/standby or HSRP (hot-standby routing protocol)
├─ Dual uplinks: Link to core layer (if exists) or WAN edge

Architecture 2-switch pair:
Distribution-A (Primary):
├─ IP: 10.0.0.254/24 (gateway VLAN 10)
├─ Uplink: 10G to Core (or WAN edge if no core)
└─ Access ports: Trunks to Access-A, Access-B, Access-C

Distribution-B (Secondary/Redundant):
├─ IP: same VLAN, secondary gateway
├─ Uplink: 10G to Core (different path)
└─ Access ports: Trunks to Access-D, Access-E, Access-F

Inter-switch link (L2 or L3):
├─ IF L2: STP trunk, priority settings for load balancing
├─ IF L3: Point-to-point OSPF adjacency
└─ Bandwidth: 10G or dual-10G for HA
```

### Couche 3: Core Layer (Backbone réseau)

#### Quand Core layer est nécessaire?
```
Considération: IF number of distribution pairs > 3:
├─ YES (>3 pairs) → Deploy dedicated core layer
├─ NO (≤3 pairs) → Two-tier "collapsed core" acceptable
└─ Reason: Scaling laws (core growth O(N²) complexity, distribution scaling O(N))
```

#### Rôle et fonction Core
- **Backbone interconnect**: High-speed fabric connecting all distribution pairs
- **Service aggregation**: WAN edge, Data Center, Internet edge, Network Services blocks consolidated
- **Optimal path selection**: BGP/OSPF with multipath for load balancing
- **No access services**: Core never houses user-facing services (isolation principle)

#### Design caractéristiques Core Layer

| Aspect | Détail |
|--------|--------|
| **Topologie** | Full mesh OR partial mesh (depends scale) |
| **Links formula** | Full mesh = N × (N-1) ÷ 2 links (ex: 4 cores = 6 links) |
| **Throughput** | 40-100G line-rate, no congestion |
| **Latency** | < 1ms inter-pair (no queuing) |
| **Routing** | BGP (if multiple Autonomous Systems) or OSPF (single domain) |
| **Redundancy** | Every link critical (no single point failure) |

#### Core layer devices
```
Physical: Catalyst 6880 or 9500H Series (high-end)
├─ Port density: 96-400 ports (various modules)
├─ Throughput: Terabit-scale (4Tbps+)
├─ ASICs: Specialized forwarding hardware
└─ Reliability: Dual supplyies, modular design (hot-swap linecards)

Example 4-core design (full mesh):
Core-1 --- 10G --- Core-2
├─ 10G --- 10G
Core-3 --- 10G --- Core-4
Each distribution pair (A,B,C,D) connect each core (partially routed)
```

---

## Modèle deux couches (2-Tier Collapsed Core)

### Vue ensemble
Two-tier design absorbs core functions into distribution layer, suitable small/medium campus (< 10 buildings, < 3000 users).

### Distribution pair rôles "collapsed"
```
Distribution pair acts as:
├─ L2/L3 boundary (access aggregation) [traditional distribution role]
├─ **AND** Core backbone interconnect [absorbed core role]
├─ **AND** Edge service blocks (WAN, DC, Internet, Network Services)
└─ Result: Simplified architecture, lower cost, reduced complexity
```

### Edge service blocks (2-tier focus)

#### Blocs services typiques

**WAN Edge Block:**
- ISR/CSR routers terminate WAN circuits (MPLS, Internet)
- BGP/EIGRP dynamic routing to headquarters
- IP VPN termination (site-to-site VPN tunnels)

**Data Center Block:**
- Servers, SAN storage, virtualization hosts
- Often dedicated VLAN per DC (10.10.x.x range typical)
- Direct connect to distribution (no access layer)

**Internet Edge Block:**
- Firewalls, load balancers, web servers (DMZ)
- Gateway-of-last-resort (any-to-internet traffic)
- DDoS mitigation, WAF, SSL termination

**Network Services Block:**
- WLC management, DHCP servers, DNS, AAA (ISE)
- System monitoring (Syslog, NetFlow collectors)
- Critical infrastructure (not user-facing)

#### Connexion blocs dans 2-tier
```
Access Layer (users)
└─ Distribution Pair (L3 routers)
   ├─→ WAN Edge block
   ├─→ Data Center block
   ├─→ Internet Edge block
   └─→ Network Services block
   
   All blocks are L3 connected to distribution (no L2 bridging)
   Routing via OSPF/BGP determines path
```

---

## Modèle trois couches détail complet

### Architecture visuelle
```
                        ┌─────────────┐
                        │ Core Layer  │
                  ┌────→│(if >3 dist) │←────┐
                  │     └─────────────┘     │
                  │                         │
           ┌──────┴──────┐          ┌──────┴──────┐
           │Distribution │          │Distribution │
           │   Pair A    │          │   Pair B    │
           └──────┬──────┘          └──────┬──────┘
                  │                         │
        ┌─────────┴────┬────────────────┬───┴─────────┬────────┐
        │              │                │             │        │
    ┌───▼──┐      ┌───▼──┐        ┌───▼──┐      ┌───▼──┐  ┌──▼───┐
    │Acc-1 │      │Acc-2 │        │Acc-3 │      │Acc-4 │  │WAN/DC│
    └───┬──┘      └───┬──┘        └───┬──┘      └───┬──┘  └──┬───┘
        │             │                │             │        │
     [Users/Phones]  [Wireless] [Labs/IoT] [Printers]      [Services]

VLAN assignment examples:
├─ Acc-1: VLAN 10 (Corporate), VLAN 90 (VoIP)
├─ Acc-2: VLAN 20 (Guest via WLC SSID)
├─ Acc-3: VLAN 30 (Lab equipment)
├─ Acc-4: VLAN 40 (Printing devices)
└─ Services: VLAN 50 (Data Center), VLAN 60 (WAN)
```

---

## Layer 2 vs Layer 3 Access design decision

### Design option A: Layer 2 Access Layer (STP-based)

**Configuration:**
- Access switches operate Layer 2 only
- Distribution switches = Layer 3 gateway for all VLANs
- Clients in VLAN X on any access switch route via Distribution

**Pros:**
- ✓ Simple conceptually (access = dumb switches)
- ✓ Preserves AP mobility (clients stay same VLAN across APs)
- ✓ Minimal access switch configuration

**Cons:**
- ✗ STP required (single switch VLAN = no loop, multi-switch = STP blocking some links)
- ✗ All inter-vlan traffic traverses distribution (potential bottleneck)
- ✗ VLAN scale limited (STP instance per VLAN = processing overhead)

#### Exemple L2 Access single VLAN:
```
VLAN 10 (Corporate):
Acc-1 (port 1-24, VLAN 10) 
└─ Uplinks STP trunk to Dist-A/B
Client A (connected Acc-1:port 5):
├─ Same VLAN 10 = direct switching (no routing)
└─ No loop possible (single switch access)

VLAN 10 spanning multiple access:
Acc-A (port 1-24, VLAN 10)
Acc-B (port 1-24, VLAN 10)
Both trunk same distribution Dist-A
└─ STP required (trunk loop: Acc-A → Dist-A → Acc-B → back to Acc-A)
   → STP blocks one path, only one active (reduced redundancy)
```

### Design option B: Layer 3 Access Layer (Routed Access design)

**Configuration:**
- Access switches run routing protocols (OSPF)
- Each access VLAN = unique subnet with access switch as gateway
- Client roaming = VLAN change → new subnet/IP assignment (not typical WLAN)

**Pros:**
- ✓ No STP needed (routed design naturally loop-free)
- ✓ Direct access-to-access routing (no distribution hop for same-tier traffic)
- ✓ More scalable VLAN deployments

**Cons:**
- ✗ Access switches must support L3 forwarding + routing protocol CPU
- ✗ Complex client roaming (DHCP reassignment needed, AP per-VLAN bindings)
- ✗ Modern but not traditional campus design

#### Exemple L3 routed access:
```
Access-A VLAN 10: 10.1.0.0/24 (gateway 10.1.0.254)
├─ OSPF adjacency to Dist-A (10.5.0.0/24)
└─ Clients 10.1.0.1-253
   └─ Inter-vlan to Access-B (VLAN 20) = Acc-A → Dist-A → Acc-B path

Access-B VLAN 20: 10.2.0.0/24 (gateway 10.2.0.254)
├─ OSPF adjacency to Dist-A (10.5.0.0/24)
└─ Clients 10.2.0.1-253
   └─ Same tier VLAN 10 traffic loops back via Dist-A (no direct peer link)
```

---

## Alternative designs modernes

### Leaf-Spine (Data Center Clos topology)

#### Contexte
Leaf-spine adresse limitation traditional 3-tier design pour data center: east-west traffic (server-to-server) not optimized par three-tier (north-south bias for client-server).

#### Architecture
```
Spine Layer (Core fabric)
├─ Spine-1
├─ Spine-2
├─ Spine-3
└─ Spine-4
   ↑ (each interconnected full-mesh)

Leaf Layer
├─ Leaf-A ↔ [Spine-1,2,3,4] ↔ Servers
├─ Leaf-B ↔ [Spine-1,2,3,4] ↔ Servers
└─ Leaf-C ↔ [Spine-1,2,3,4] ↔ Servers
```

**Caractéristiques:**
- **ECMP multipath**: Servers A → Server B = multiple paths (load balanced)
- **Latency**: Any leaf-to-leaf = 2 hops (leaf → spine → leaf, consistent)
- **Scalability**: Add leaf nodes without re-architecture spine (horizontal growth)
- **Use case**: Mostly data center, not campus access

### SD-Access (Software-Defined Campus)

Covered in depth Module 23 (Fabric Technologies), but brief overview:
- **Overlay network**: Virtual VXLAN tunnels over physical underlay
- **Centralized policies**: DNA Center orchestrates automation
- **Identity-based**: Policies per user/group, not IP-based
- **Modern evolution**: 3-tier stays physical, SD-Access adds virtualization layer

---

## Points clés à retenir

### Sélection design decision tree
```
Nombre distribution pairs?
├─ ≤ 3 pairs: Use 2-tier collapsed core (cost-effective)
├─ > 3 pairs: Use 3-tier with dedicated core
└─ Data center: Consider leaf-spine (east-west optimization)

L2 vs L3 access?
├─ L2 (traditional): Simpler, STP required, good WLAN support
├─ L3 (modern): Routed, no STP, complex roaming
└─ Recommendation: L2 for campus, L3 for enterprise core
```

### Configuration best practices
- **Access switches**: No inter-connection (star topology to distribution)
- **Distribution pairs**: Always redundant active/active or active/passive with HSRP
- **Core links**: Full mesh or near-full mesh (no single point failure)
- **VLAN scoping**: Typically single access switch or max 2 access switches
- **IP summarization**: Distribute aggregate 10.X.0.0/16 from distribution (not per-access /24)

### Troubleshooting tips
- **Slow north-south traffic**: Check distribution uplink saturation
- **STP blocking**: Verify root bridge election (priority values) + port costs
- **OSPF issue**: Ensure routing protocol enabled on L3 boundaries, subnet mask compatibility
- **VLAN spanning issue**: May indicate design violation (access switches inter-connected)

---

## Ressources complémentaires
- Cisco Campus Design Best Practices (CVD - Cisco Validated Design)
- SAFE Architecture Guide (enterprise security overlays)
- Spanning Tree Protocol (IEEE 802.1d/802.1w RSTP standards)
- OSPF routing (RFC 2328, Cisco IOS configuration)
