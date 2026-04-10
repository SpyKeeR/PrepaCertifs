---
title: "Module 23: Technologies Fabric (SD-Access et SD-WAN)"
module: 23
type: notes
topics: [fabric-networks, SD-Access, VXLAN, LISP, TrustSec, SGT, overlay, underlay, DNA-Center]
difficulty: advanced
updated: 2026-03-18
---

# Module 23: Technologies Fabric (SD-Access et SD-WAN)

## Vue d'ensemble
Les technologies Fabric modernes abstraient l'infrastructure physique via overlay networks virtuels, permettant automation, segmentation, et mobilité utilisateur. Ce module couvre SD-Access (campus fabric), LISP contrôle-plan, VXLAN data-plan, TrustSec policies SGT, et orchestration DNA Center.

## Concept fondamental: Fabric networks

### Définition simplifiée
**Fabric network** = overlay virtual network (VXLAN tunneling) déployée sur infrastructure physique underlay (switches, routers), créant une abstraction de service indépendamment de topology physique.

```
Application Layer (user services)
    ↓
Policy Plane (SGACLs, group-based policies)
    ↓
Control Plane (LISP mapping)
    ↓
Data Plane (VXLAN encapsulation)
    ↓↓↓
Underlay Network (physical switches/routers/WAN)
    ↓
Physical Devices (Catalyst, ISR, WLC, AP controllers)
```

### Bénéfices fabric vs traditional switched networks
| Aspect | Traditional | Fabric (SD-Access) |
|--------|-----------|---------|
| **Network automation** | Manual CLI/API | DNA Center orchestration |
| **Policy model** | IP-based ACLs | Identity/group-based SGACLs |
| **Host mobility** | VLAN change required | Seamless (wired ↔ wireless) |
| **Segmentation** | VLAN boundaries static | Virtual Networks (VRFs) dynamic |
| **Encryption** | Per-link TLS/IPsec | Network-wide VxLAN/TrustSec |
| **Scalability** | STP limits (~200 VLANs) | 4000+ Virtual Networks |
| **Analytics** | Syslog, NetFlow | Real-time telemetry dashboards |

---

## SD-Access (Software-Defined Campus)

### Définition SD-Access
SD-Access = Cisco Campus Fabric Solution + DNA Center orchestration, providing:
1. **Network Automation**: DNA Center automates underlay/overlay provisioning
2. **Assurance & Analytics**: Telemetry-based network health dashboards
3. **Host Mobility**: Seamless roaming wired/wireless, same IP address retained
4. **Identity Services**: ISE integration, user/group/device contexte authentication
5. **Policy Enforcement**: SGACLs (Scalable Group Access Control Lists) vs traditional IP ACLs
6. **Secure Segmentation**: Virtual Networks (VN) = isolated broadcast domains
7. **Network Virtualization**: VRF-like isolation, but provisioned via policy

### Componentes SD-Access

#### Management Orchestration: Cisco DNA Center
```
DNA Center (Management appliance)
├─ Roles:
│  ├─ Policy Controller: Define network policies (authentication, authorization, accounting)
│  ├─ Assurance Engine: Collect telemetry, predict issues, suggest remediation
│  ├─ Provisioning Orchestrator: Automate device configs (push VXLAN, LISP, routing)
│  └─ Dashboard: Web UI for operators (network health, client analytics, troubleshooting)
├─ Architecture deployment:
│  ├─ Single appliance: Suitable small campus (<500 APs)
│  ├─ HA cluster: 3+ appliances for redundancy/scale
│  └─ Cloud-hosted: DNA Center cloud (managed service)
└─ Integration:
   ├─ Catalyst switches (automatic discovery via LLDP)
   ├─ Cisco ISE (user identity, posture validation)
   └─ Third-party devices (API-based integration)
```

#### Contrôle d'accès réseau: Cisco ISE (Identity Services Engine)
```
Cisco ISE
├─ Rôles:
│  ├─ Authentication: RADIUS/TACACS+ identity validation
│  ├─ Authorization: Policy enforcement (VLAN, QoS attributes)
│  ├─ Accounting: Session logging, audit trails
│  ├─ Posture Validation: Device health checks (antivirus, patches)
│  └─ Profiling: Device type detection (iPhone, Windows, IoT, etc.)
├─ Integration SD-Access:
│  └─ SGT assignment: Users/devices tagged with Scalable Group Tags
└─ Network flows:
   ├─ Client auth → ISE → SGT returned → TrustSec marking
   └─ Policies enforcement: SGACL based SGT source/destination pairs
```

### SD-Access Architecture (4 couches)

#### Couche 1: Physical Layer (Devices physiques)

```
Physical Infrastructure:
├─ Fabrication Devices (Fabric Edge, Fabric Border):
│  ├─ Catalyst 9300/9400 switches (campus fabric edge)
│  ├─ ASR/ISR/CSR routers (WAN fabric border)
│  └─ Flexible NetFlow data collection capability
├─ Non-Fabric Devices:
│  ├─ Legacy switches (no VXLAN support, connected via fabric border)
│  ├─ Servers, network appliances (FCBSE - Fabric Common Border Switch Element)
│  └─ Third-party devices (integrated via fabric border)
├─ Wireless:
│  ├─ Catalyst 9800-CL/9800 WLC
│  ├─ Catalyst 9100/9115 APs (802.11n/ac/ax capable)
│  └─ WLAN clients (any device supporting 802.1x + standard Wi-Fi)
└─ Management/Controller:
   ├─ DNA Center (orchestration, policy management)
   └─ ISE (identity, posture, SGT assignment)
```

#### Couche 2: Network Layer (Underlay + Overlay)

**Underlay Network (Physical routing layer):**
- Provides IP reachability between fabric nodes
- Deployment options:
  - **Manual Underlay**: CLI provisioning legacy networks (IP addresses manually configured)
  - **Automated Underlay**: DNA Center LAN Automation, IS-IS protocol, Network Plug & Play

**Overlay Network (VXLAN tunnels + control plane):**
- LISP (control plane): Maps EIDs → RLOCs, dynamic endpoint mobility
- VXLAN (data plane): IP/UDP encapsulation, transparent service delivery
- TrustSec (policy plane): SGT tagging, SGACL enforcement

#### Couche 3: Controller Layer (Intelligence + Orchestration)

```
DNA Center + ISE Integration:
├─ Policy Definition:
│  ├─ Who: Users/groups (AD/LDAP directory)
│  ├─ What: Device types (iPhone, Laptop, Printer)
│  ├─ Where: Location/building (DHCP subnet, AP name)
│  └─ When: Time-based policies (business hours, after-hours)
├─ Decision Making:
│  └─ IF [user dept = Sales] AND [device = MacOS] THEN [QoS = Gold, VLAN = Corp, Encrypt = AES256]
├─ Enforcement:
│  ├─ SGT assignment: ISE marks traffic with source/dest tag
│  ├─ DELTA sync: DNA Center pushes config to fabric nodes
│  └─ CoA updates: Real-time policy changes (mid-session)
└─ Assurance Dashboard:
   ├─ Health score (device CPU/memory/disk usage)
   ├─ Network connectivity anomalies (latency spikes, packet loss)
   ├─ Application experience (throughput, delay, MOS for VoIP)
   └─ Security posture (threats, vulnerable devices)
```

#### Couche 4: Application Layer (User services + Integrations)

```
Business Applications:
├─ Enterprise Apps: ERP, CRM, File sharing
├─ Cloud Services: SaaS (Office365, Salesforce, Slack)
├─ Real-time: Cisco Webex, Microsoft Teams
└─ AI/ML: Powered by telemetry insights from DNA Center
```

---

## Underlay Network (Fondation physique)

### Manual Underlay Deployment
Traditionalmethod: Manual CLI configuration chaque device

**Steps:**
1. Plan IP addressing: Core 10.0.0.0/8, Distribution 10.x.0.0/24, Access 10.x.1.0/28
2. Configure interfaces: IP addresses, routing protocol adjacency (OSPF)
3. BGP/OSPF routing: Establish reachability between all fabric nodes
4. Verify: ping, traceroute, show ip route validation

**Avantages:**
- ✓ Full control, customizable
- ✓ Legacy network support (no DNA Center dependency)

**Désavantages:**
- ✗ Error-prone (typos, subnet misconfigurations)
- ✗ Scalability challenges (100+ devices = manual burden)
- ✗ No template consistency (configs drift)

### Automated Underlay (DNA Center LAN Automation)

DNA Center LAN Automation discovers and auto-configures fabric nodes:

```
DNA Center LAN Automation workflow:
├─ Discovery:
│  ├─ LLDP neighbor detection (switch-to-switch links)
│  ├─ Network Plug & Play (OnBox discovery for new devices)
│  └─ Device inventory build
├─ Underlay planning:
│  ├─ Auto-generate IP addressing per roles (edge/border/core)
│  ├─ OSPF area assignment (area 0 core, area X non-core)
│  └─ Adjacency planning (which devices interconnect)
├─ Configuration generation:
│  ├─ Generates running-configs per device (templates-based)
│  ├─ IP addresses, interface configs, OSPF timers
│  └─ IS-IS optional (BGP for WAN)
└─ Deployment:
   ├─ Push configs via NETCONF/RESTCONF
   ├─ Verify reachability (PING test automation)
   └─ Alert on failures (config mismatch corrects)

Benefits:
├─ ✓ Consistent configurations (templates enforced)
├─ ✓ Faster deployment (5-10 devices minutes, not hours)
├─ ✓ Reduced errors (DNA Center validates before push)
└─ ✓ Auto-remediation (config drift correction)
```

---

## Overlay Network (SD-Access Fabric Details)

### Three-Plane Architecture

#### Plan 1: Control Plane (LISP - Locator/ID Separation Protocol RFC 6830)

**Concept LISP:**
Decouples endpoint identity (EID) from routing locator (RLOC):
- **EID** (Endpoint IDentifier): User/device IP address (10.1.1.5)
- **RLOC** (Routing Locator): Physical switch/router IP (192.168.1.1)
- **Benefit**: Host mobility = EID portable, RLOC changes transparently

**LISP Components:**
```
LISP Map Server (MS): Centralized mapping database
├─ Stores EID → RLOC mappings
├─ Deployed in fabric border nodes (WAN gateway)
└─ Fault tolerance: HA pair (primary/secondary)

Ingress Tunnel Router (ITR):
├─ Encapsulates packets destined to EIDs
├─ Queries Map Server: "Where is destination EID?"
├─ Receives RLOC → Encapsulates in LISP tunnel

Egress Tunnel Router (ETR):
├─ Receives LISP-encapsulated packets
├─ Decapsulates inner packet
├─ Forwards to local endpoint

LISP Data Structure:
├─ LISP cache (ITR): Recently queried EID→RLOC mappings
├─ Negative cache entry: EID not found (60 seconds TTL)
└─ TTL refresh: Re-query Map Server before expiration
```

**LISP Mobility example:**
```
Scenario: MacBook client roams AP1 (RLOC 192.168.1.1) → AP2 (RLOC 192.168.1.2)
├─ MacBook IP: 10.1.1.50 (EID, same before/after roaming)
├─ Before roaming:
│  └─ LISP mapping: EID 10.1.1.50 → RLOC 192.168.1.1 (AP1)
├─ Roaming happens → AP2 detects association
├─ AP2 → Map Server: New mapping EID 10.1.1.50 → RLOC 192.168.1.2
├─ After roaming:
│  └─ LISP mapping: EID 10.1.1.50 → RLOC 192.168.1.2 (AP2)
└─ Client impact: Seamless, same IP, applications continue (except brief ARP timeout)
```

#### Plan 2: Data Plane (VXLAN - Virtual eXtensible LAN RFC 7348)

**VXLAN Encapsulation:**
```
Original Frame:
┌─────────────────────────┐
│ Ethernet (MAC dest)     │
│ IP header (dest IP)     │
│ TCP/UDP payload         │
└─────────────────────────┘

VXLAN Encapsulated:
┌──────────────────────────────────────┐
│ Outer Ethernet (fabric switch MACs)  │ ← fabric network
│ Outer IP (RLOC source/dest)          │
│ Outer UDP (port 4789 VXLAN standard) │
├──────────────────────────────────────┤
│ VXLAN header:                        │
│  ├─ VNI (24-bit, 16M virtual nets)   │
│  ├─ G-Bit (SGT present flag)         │
│  └─ D-Bit (don't learn flag)         │
├──────────────────────────────────────┤
│ Original Ethernet + IP + TCP/UDP     │ ← tunneled payload
└──────────────────────────────────────┘
```

**VXLAN-GPO (Group Policy Option RFC 8974 - enhanced):**
```
VXLAN-GPO Fields (added after VNI):
├─ Group Policy ID (16-bit SGT): Scalable Group Tag
├─ G-Bit (1-bit): SGT valid flag (1=present, 0=not present)
├─ D-Bit (1-bit): Don't Learn flag (suppress fabric learning)
└─ A-Bit (1-bit): Policy Applied (1=policy action applied, 0=pending)

Benefits:
├─ Tags embedded in data plane (no separate signaling)
├─ Support encryption (TrustSec AES-GCM)
└─ Policy enforcement at egress (ingress switch knows SGT destination)
```

**VXLAN advantages:**
- ✓ IP/UDP encapsulation: Works over any IP network (legacy switches tolerate)
- ✓ Independent underlay: No topology constraints (mesh, star, hierarchical OK)
- ✓ Stateless forward: Simple switch forwarding (no per-VNI state machine)
- ✓ Standards-based: RFC 7348, multi-vendor support

#### Plan 3: Policy Plane (TrustSec with SGT)

### Cisco TrustSec Framework

**Paradigme**: Group-based access control replaces traditional IP ACLs

```
Traditional IP-based policy:
├─ "Allow 10.1.1.0/24 → 10.2.1.0/24 port 443"
├─ Problem: User roams, new IP, policy not applied
└─ Brittle: IP addresses change, policies stale

TrustSec group-based policy:
├─ "Allow Sales-Users (SGT 100) → FileServers (SGT 401) port 443"
├─ Benefit: User identity tags, IP-agnostic
└─ Dynamic: User moves, SGT follows (policies always applicable)
```

**SGT (Scalable Group Tag):**
```
Definition: 16-bit tag (0-65535 range) identifying group
├─ User groups: Sales=100, Engineering=101, Support=102, etc.
├─ Device groups: Printers=201, Phones=202, Servers=301, etc.
├─ Reserved: SGT 0 (untagged), SGT 65535 (deny default)
└─ Assignment: ISE policy per username/MAC/device type

SGT Propagation Paths:
├─ 802.1x: ISE returns SGT in RADIUS access-accept
├─ MAB (MAC Authentication Bypass): Device profiling assigns SGT
├─ CoA (Change-of-Authorization): ISE updates mid-session tag
└─ LISP: Fabric automatically tags endpoints based ISE assignment
```

**SGACL (Scalable Group Access Control List):**
```
Policy matrix (source SGT → destination SGT):
└─ IF [source_SGT=100 Sales] AND [dest_SGT=200 Marketing] THEN [permit TCP 80,443]
   IF [source_SGT=100 Sales] AND [dest_SGT=400 Finance] THEN [deny]
   IF [source_SGT=200 Marketing] AND [dest_SGT=100 Sales] THEN [permit TCP 445]

Enforcement point: Egress switch (knows packet SGT tags via VXLAN-GPO)
├─ Decapsulate VXLAN, extract SGT
├─ Apply SGACL lookup (source → destination)
├─ Forward/drop based policy
└─ No CPU intensive ACL matching (ASIC accelerated)
```

**Integration ISE + DNA Center:**
```
Workflow:
├─ User joins WLAN (via 802.1x): ISE authenticates
├─ ISE assigns SGT: Machine = "Sales-Users" SGT 100
├─ DNA Center provision: Maps SGT 100 to policies
├─ Fabric nodes: Implement SGACL rules globally
├─ User roams: ISE CoA updates SGT (if dept changed)
└─ Fabric automatically enforces new policies (zero downtime)
```

---

## Virtual Networks (VRF-like isolation)

**Virtual Network (VN)** = Isolated overlay network (separate broadcast domain)

```
Example campus deployment:
├─ Corporate VN: Users, servers, managed devices (ISE authenticated)
├─ Guest VN: Visitors, public Wi-Fi, limited access
├─ IoT VN: Sensors, cameras, restricted bandwidth
├─ Facilities VN: HVAC, lighting control, isolated segment
└─ Management VN: Admins, WLC management, restricted access

Each VN:
├─ Has separate VXLANs (different VNI)
├─ Isolated LISP map domains
├─ Restricted inter-VN communication (policy-based)
└─ Potential different ISP/QoS per VN
```

**Intégration VN + SGT:**
```
Policy examples:
├─ Sales-Users (SGT 100) in Corporate VN (VN 1) only
├─ Guest-Users (SGT 101) in Guest VN (VN 2) only
├─ IoT-Devices (SGT 200) in IoT VN (VN 3), cannot access Corporate VN
└─ Management (SGT 50) in all VNs (special privilege)
```

---

## Comparaison LISP vs VXLAN

| Aspect | LISP | VXLAN |
|--------|------|-------|
| **Layer OSI** | Control plane (routing) | Data plane (encapsulation) |
| **Standard** | RFC 6830 | RFC 7348 + 8974 (GPO) |
| **Función** | Maps EID → RLOC | Encapsulates payload in tunnel |
| **Deployment** | Cisco SD-Access primary | Industry standard (multi-vendor) |
| **Mobility** | Dynamic mapping, fast roaming | IP reassignment typical |
| **Tunneling** | LISP encapsulation IF needed | Always encapsulated |
| **Usage combo** | LISP control + VXLAN data | VXLAN alone (underlay agnostic) |

---

## Points clés à retenir

### SD-Access architecture decisions
- **Fabric-enabled devices**: Catalyst 9300+ (campus), ASR/ISR (WAN border)
- **Orchestration**: DNA Center mandatory for automation
- **Identity**: ISE integration for SGT assignment
- **Virtual Networks**: Plan segmentation (corporate/guest/IoT/facilities)

### Policy enforcement design
- **SGT allocation**: Based user dept/device type/location (business logic)
- **SGACL rules**: Define source → destination pair permissions
- **Default deny**: SGT 65535 = implicit drop (whitelist approach)

### Troubleshooting fabric
- **LISP mapping issues**: Show lisp map-cache (verify EID→RLOC entries)
- **VXLAN encapsulation**: Packet capture to validate outer headers
- **SGT mismatch**: ISE policy not assigning correct tag
- **DNA Center sync**: Verify device configs match intended state

---

## Ressources complémentaires
- RFC 6830 (LISP standard)
- RFC 7348 (VXLAN standard)
- RFC 8974 (VXLAN-GPO standard)
- Cisco DNA Center documentation (LAN automation, assurance)
- Cisco TrustSec design guide (ISE configuration)
