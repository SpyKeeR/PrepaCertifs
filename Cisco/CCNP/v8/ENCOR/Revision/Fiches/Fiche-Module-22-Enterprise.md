---
title: "Fiche Module 22: Architecture d'entreprise"
module: 22
type: fiche
topics: [hierarchical-design, access-distribution-core, vlan-design, two-tier, three-tier, leaf-spine, routed-access]
difficulty: intermediate
updated: 2026-03-18
---

# Fiche Module 22: Architecture d'entreprise

## Comparatif modèles design

### Two-Tier vs Three-Tier decision matrix

| Facteur décision | Two-Tier (Collapsed Core) | Three-Tier (Dedicated Core) |
|--------|---|---|
| **Distribution pairs count** | ≤ 3 pairs OK | > 3 pairs requis |
| **Campus size** | < 10 buildings | 10+ buildings |
| **User count** | < 3000 users | 3000+ users |
| **Cost** | ✓ Lower initiale | Higher (core devices) |
| **Scaling future** | Limited (tight core) | Excellent (modular core) |
| **Complexity** | Simple (fewer devices) | More complex (core management) |
| **Recommendation** | PME, petits campus | Grandes enterprises |

---

## Hiérarchie trois couches (Core-Distribution-Access)

### Tableau fonctions par couche

| Couche | Nom | Rôle | Connexion | Taille typical |
|--------|-----|------|-----------|--------|
| **1 (Edge)** | Access Layer | User connectivity, VLANs, QoS | Star: All → access switch | 24-48 ports |
| **2 (Agg)** | Distribution Layer | L2/L3 boundary, Aggregation, STP root | Pair: Active+Standby redundancy | 48-96 ports |
| **3 (Backbone)** | Core Layer | Backbone interconnect WAN/DC | Full mesh links | 96-400 ports |

### Access Layer
```
Fonctions:
├─ Endpoint connectivity (workstations, phones, APs)
├─ VLAN segmentation (security, performance)
├─ QoS trust boundary (CoS/DSCP marking)
└─ Port security (802.1x, MAC limits)

Design rule: Access switches NOT interconnected directly
└─ All inter-access traffic → Distribution layer
└─ Prevents loops, simplifies VLAN management

Switch types: Catalyst 2900/3900 (Gigabit, PoE)
Uplinks: 2× 10G to Distribution pair (redundancy)
```

### Distribution Layer
```
Fonctions:
├─ Access aggregation (consolidate access switches)
├─ L2/L3 boundary (inter-vlan routing)
├─ STP boundary (limits fault propagation)
├─ IP route summarization (aggregated subnets → core)
└─ QoS policy marking (per-access granularity)

Design pattern: Paired switches (Active/Active ou Active/Passive)
├─ Distribution-A (Primary)
├─ Distribution-B (Secondary/Standby)
└─ Interconnects (L2 trunk OR L3 routing link)

Switch types: Catalyst 4900/6800 (Advanced LAN modules)
Uplinks: 2× 10G to Core (or WAN if no core)
Redundancy: HSRP (Hot-Standby Routing Protocol)
```

### Core Layer (IF > 3 distribution pairs)
```
Fonctions:
├─ Backbone fast fabric (40-100G links)
├─ WAN/Data Center/Internet service aggregation
└─ No user-facing services (isolation principle)

Topology: Full mesh (N switches = N×(N-1)/2 links)
Examples:
├─ 4 core switches = 6 links
├─ 5 core switches = 10 links
└─ Scales non-linearly (careful planning)

Switch types: Catalyst 6880/9500H (terabit-scale)
Throughput: Line-rate 40-100G (no congestion)
Routing: BGP (multi-AS) or OSPF (single domain)
```

---

## Layer 2 vs Layer 3 Access models

### Layer 2 Access (Traditional STP-based)

**Configuration:**
- Access switches = Layer 2 only (no routing)
- Distribution switches = L3 gateway (inter-vlan routing)
- VLAN spans multiple access switches (STP prevents loops)

```
Pros:
✓ Simple conceptually (access = dumb switches)
✓ AP mobility preserved (clients same VLAN across APs)
✓ Minimal configuration

Cons:
✗ STP required (blocks redundant links)
✗ Single VLAN = no loop (multi-VLAN = STP overhead)
✗ Slower convergence on topology change
```

**Example:**
```
VLAN 10 (Corp) spans:
├─ Acc-1 ports 1-24
├─ Acc-2 ports 1-24
└─ Both trunk to Dist-A,Dist-B with STP
   └─ STP blocks one trunk (reduces redundancy)
```

### Layer 3 Access (Routed Access)

**Configuration:**
- Access switches = L3 routers (OSPF adjacency)
- Each access switch own subnet (gateway = access IP)
- No STP needed (routed design loop-free)

```
Pros:
✓ No STP (naturally loop-free)
✓ Direct access-to-access routing
✓ Scalable VLAN deployments

Cons:
✗ L3 processing on access switches (more CPU)
✗ Roaming complex (DHCP IP reassignment)
✗ Non-traditional (troubleshooting different)
```

**Example:**
```
Access-A VLAN 10: 10.1.0.0/24 (Gi0 = 10.1.0.254)
Access-B VLAN 20: 10.2.0.0/24 (Gi0 = 10.2.0.254)
Both OSPF-adjacent via Dist-A → inter-vlan via routing
```

---

## VLAN design best practices

### VLAN allocation templates

| VLAN Range | Allocation | Exemple |
|-----|---|---|
| **1-50** | Management + Systems | Admin(2), WLC(10), ISE(15), Syslog(20) |
| **100-199** | Corporate / User groups | Sales(100), Eng(110), Finance(120) |
| **200-299** | Devices / IoT | Printers(201), Cameras(210), Sensors(220) |
| **300-399** | Special services | Guest(300), Contractor(310) |
| **400-499** | Wireless networks | Corp-WiFi(400), Guest-WiFi(401) |
| **500-599** | Voice / VoIP | VoIP-Phones(500), Softphones(501) |

### VLAN scoping rules
```
Access layer VLANs:
├─ Single access switch = simple (no loop)
└─ Multiple access = STP trunk required

Typical: Single access switch (VLAN confined)
├─ VLAN 100: Access-1 ports (no spanning)
├─ VLAN 101: Access-2 ports (no spanning)
└─ All routing via Distribution layer

Advanced: Multi-access VLAN
├─ VLAN 100: Access-1 AND Access-2 (STP trunk)
├─ Pro: More flexibility
└─ Con: STP overhead, slower convergence
```

---

## Service blocks placement

### Two-Tier edge blocks (Distribution pair connects all)

```
Service Blocks (L3 connected to Distribution):

1. WAN Edge:
   └─ ISR/CSR routers
     ├─ WAN circuit termination (MPLS, Internet)
     ├─ BGP/EIGRP routing
     └─ VPN gateway

2. Data Center:
   └─ Servers + SAN storage
     ├─ Dedicated VLAN (10.10.x.x typically)
     ├─ Database servers
     └─ Virtual hosts

3. Internet Edge:
   └─ Firewall, Load balancer, WAF
     ├─ DMZ protection
     ├─ DDoS mitigation
     └─ SSL termination

4. Network Services:
   └─ WLC, DHCP, DNS, ISE, AAA
     ├─ Management plane
     ├─ Infrastructure support
     └─ Monitoring (syslog, NetFlow)
```

---

## Leaf-Spine architecture (Data Center)

### When to use leaf-spine vs three-tier
```
Three-Tier Hierarchical:
├─ North-South bias (client ↔ server model)
├─ Multi-hop paths (3+ stage networks)
├─ East-West inefficient

Leaf-Spine (Clos topology):
├─ East-West optimized (server ↔ server data)
├─ Consistent 2 hops (leaf → spine → leaf)
├─ ECMP multipath load-balancing
└─ Modern data centers (scale-out architecture)
```

**Visual:**
```
         Spine1    Spine2    Spine3    Spine4
            ↑↓        ↑↓       ↑↓        ↑↓
         (full     mesh,    each     leaf
          connected to all spines)

    Leaf-A    Leaf-B    Leaf-C
      ↑↓        ↑↓        ↑↓
   Servers    Servers   Servers

   Latency any path: Leaf → Spine → Leaf = 2 hops fixed
   Throughput: 400Gb/s (4×100G per leaf, 5 leaves = 2Tbps total)
```

---

## STP (Spanning Tree Protocol) in hierarchical design

### STP configuration strategy

**Access + Distribution spanning:**
```
Root Bridge Election:
├─ Usually Distribution-A (primary)
│  └─ Priority: 4096 (lower = preferred)
│
├─ Distribution-B (secondary backup)
│  └─ Priority: 8192 (higher priority = not preferred)
│
└─ Access switches: Default priority (32768)

Port roles:
├─ Root port: Fastest path to root (typically uplink)
├─ Designated port: Forwarding (per segment)
└─ Blocked port: Standby (redundancy link)

Result: Single access tree (no loops)
```

**Convergence tuning:**
```
STP Timers:
├─ hello-time: 2 seconds [frequency BPDUs]
├─ forward-delay: 15 seconds [listening→learning→forward]
├─ max-age: 20 seconds [BPDU stale timeout]

Modern (RSTP):
├─ Much faster (< 1 sec convergence)
└─ Recommended over legacy STP

Configuration:
spanning-tree mode rapid-pvst  [enable RSTP]
spanning-tree vlan 100 root primary  [Dist-A = root]
spanning-tree vlan 100 priority 8192  [Dist-B = backup]
```

---

## Configuration checklists

### Design validation checklist
```
☐ Campus size < 3000 users? Consider 2-tier
☐ > 3 distribution pairs needed? Plan 3-tier core
☐ L2 STP loops prevented (access not inter-connected)?
☐ VLANs scoped appropriately (single or dual access)
☐ IP addressing summarized (10.X.0.0/16 from distribution)
☐ Redundancy: Distribution pairs configured active/passive
☐ Routing protocol (OSPF) adjacency configured core
☐ QoS trust boundary at access (mark CoS/DSCP)
☐ Service blocks L3 connected (not L2 bridged)
☐ Root bridge election verified (show spanning-tree)
```

### OSPF configuration template
```
Router(config)# router ospf 100
Router(config-router)# network 10.0.0.0 0.255.255.255 area 0
Router(config-router)# network 10.1.0.0 0.0.255.255 area 1
Router(config-router)# passive-interface default
Router(config-router)# no passive-interface GigabitEthernet0/0
Router(config-router)# default-information originate [if border router]

Interface configuration:
interface GigabitEthernet0/0
  ip ospf cost 100  [adjust link cost]
  ip ospf network-type broadcast
  ip ospf hello-interval 10
  ip ospf dead-interval 40
```

---

## Troubleshooting rapide

### Symptômes et causes possibles

| Symptôme | Causes possibles | Diagnostic |
|----------|-----|------|
| **STP blocking ports** | Wrong root priority, loop detected | `show spanning-tree` - check priorities |
| **OSPF not adjacent** | MTU, hello/dead interval, network-type | `debug ip ospf adj` |
| **VLAN can't reach gateway** | VLAN not on distribution, STP blocking | `show vlan` on all switches |
| **Slow inter-vlan** | Distribution uplink congestion, QoS rate-limit | Check utilization, QoS policy |
| **Users all same VLAN slow** | AP/access switch capacity, interference | Check client count, signal |

---

## Ressources quick-reference
- Default STP priority: 32768 (root bridge lower)
- Root Bridge priority minimum: 0 (not recommended, use 4096)
- OSPF cost formula: 100,000 / bandwidth (Mbps)
- Gigabit: OSPF cost = 1, Serial 64k: cost = 1562
- VLAN 1: Native (never VLAN trunk native VLAN mismatch)
- STP BPDU multicast: 01:80:C2:00:00:00 (not relayed)
- Core uplinks: Minimum 10G (40G recommended large campus)
