---
title: "Fiche Module 23: SD-Access et technologies Fabric"
module: 23
type: fiche
topics: [SD-Access, VXLAN, LISP, TrustSec, SGT, DNA-Center, fabric-quick-ref]
difficulty: advanced
updated: 2026-03-18
---

# Fiche Module 23: SD-Access et technologies Fabric

## Architecture SD-Access: Vue ensemble

### Composants clés
```
Application Layer
        ↓
DNA Center (Orchestration) + ISE (Identity)
        ↓
Policy Plane (TrustSec, SGACLs, SGT)
        ↓
Control Plane (LISP: EID→RLOC mapping)
        ↓
Data Plane (VXLAN: IP/UDP encapsulation)
        ↓
Underlay Network (Physical switches/routers, OSPF)
        ↓
Physical Infrastructure (Catalyst, WLC, AP, Controllers)
```

---

## Tableau: SD-Access vs Traditional Network

| Aspect | Traditional | SD-Access |
|--------|-----------|----------|
| **Automation** | Manual CLI | DNA Center orchestrated |
| **Policy basis** | IP addresses (ACLs) | User/group identity (SGACLs) |
| **Mobility** | VLAN change required | Seamless (EID portable) |
| **Segmentation** | VLAN boundaries (200 max) | Virtual Networks (4000+ possible) |
| **Encryption** | TLS per-link (app-level) | Network-wide VXLAN+TrustSec |
| **Analytics** | Syslog polling (latency) | Real-time telemetry (DNA Center) |
| **Complexity** | Simpler initial | Complex, centralized |

---

## Underlay Network (Physical Foundation)

### Manual Underlay
- CLI configuration each device manually
- IP addressing planned + entered individually
- OSPF/BGP adjacency manual setup
- *Prone to errors, not scalable*

### Automated Underlay (DNA Center)
```
DNA Center → Discovery (LLDP)
           → IP planning auto-generate
           → Config template generation
           → Push via NETCONF
           → Verify reachability
           
Benefits:
✓ Consistent templates
✓ Fewer errors
✓ Faster deployment
✓ Automated remediation (config drift)
```

---

## Overlay Network: 3-Plane architecture

### Plane 1: Control Plane - LISP (Locator/ID Separation)

#### Concept
```
Traditional routing: IP = Identity + Location (same)
LISP: Separates EID (endpoint identity) from RLOC (routing locator)

Benefits:
├─ Host mobility: EID stays same, RLOC changes
├─ Smaller routing tables: Aggregated by RLOC
├─ Flexible addressing: IPv4/IPv6/MAC-agnostic
└─ Scalability: No per-host routes
```

#### Components
```
Mapping system:
├─ Map Server (MS): Central database EID→RLOC
├─ Ingress Tunnel Router (ITR): Encapsulate packets
├─ Egress Tunnel Router (ETR): Decapsulate packets
└─ Locator Address: Physical IP (RLOC, e.g., AP management IP)

Client roaming example:
├─ AP1 (RLOC 192.168.1.1): Client IP 10.1.1.50
├─ Roaming → AP2 (RLOC 192.168.1.2)
└─ Map Server updated: EID 10.1.1.50 → new RLOC 192.168.1.2
   → Client keeps 10.1.1.50, seamless mobility
```

### Plane 2: Data Plane - VXLAN (Virtual eXtensible LAN)

#### Encapsulation
```
Original packet:
┌─ Ethernet (MAC dest)
│─ IP (dest IP)
│─ TCP/UDP (payload)
└─

VXLAN encapsulated:
┌─ Outer Ethernet (fabric switch MACs)
├─ Outer IP (source RLOC → dest RLOC)
├─ Outer UDP (port 4789)
├─ VXLAN Header:
│  ├─ VNI (24-bit: 16 million virtual networks)
│  ├─ G-Bit (SGT present flag)
│  └─ D-Bit (don't learn flag)
├─ VXLAN-GPO: Group Policy ID (SGT tag)
└─ Original Ethernet + IP + TCP/UDP
```

#### VXLAN-GPO fields
```
Group Policy ID (16-bit): SGT (Scalable Group Tag)
├─ G-Bit: 1 = GPO present, 0 = not present
├─ D-Bit: 1 = don't learn, 0 = normal learning
└─ A-Bit: 1 = policy applied, 0 = pending

Implementation:
├─ Encapsulated in VXLAN header (after VNI)
├─ Enables SGT propagation data plane
└─ SGACL enforcement based SGT source/dest
```

### Plane 3: Policy Plane - Cisco TrustSec

#### Concept SGT (Scalable Group Tag)
```
Traditional: "Allow 10.1.1.0/24 → 10.2.1.0/24 port 443"
  Problem: User roams IP changes, policy stale

TrustSec: "Allow Sales-Users (SGT 100) → FileServers (SGT 401) port 443"
  Benefit: User identity, IP-agnostic, auto-follows roaming
```

#### SGT examples allocation
```
User Groups:
├─ Sales: SGT 100
├─ Engineering: SGT 101
├─ Support: SGT 102
└─ Contractors: SGT 103

Device Groups:
├─ Printers: SGT 201
├─ Phones: SGT 202
├─ Servers: SGT 301
└─ IoT Sensors: SGT 401

Reserved:
├─ SGT 0: Untagged
└─ SGT 65535: Deny default (implicit drop)
```

#### SGACL enforcement
```
Policy matrix:
Source SGT → Dest SGT: Action

Examples:
├─ SGT 100 (Sales) → SGT 301 (Servers): PERMIT TCP 80,443,445
├─ SGT 100 (Sales) → SGT 401 (IoT): DENY
├─ SGT 101 (Eng) → SGT 301 (Servers): PERMIT TCP 22,3389,445
└─ All others: DENY (implicit)

Enforcement point: Egress switch
├─ Extract SGT from VXLAN-GPO
├─ Lookup SGACL (source = dest)
├─ Forward/Drop per policy
└─ ASIC accelerated (no CPU impact)
```

---

## DNA Center Management

### Functionality
```
1. Policy Controller:
   ├─ Define: Authentication, Authorization, Accounting
   └─ Implement: Device configs, WLAN policies, QoS rules

2. Assurance Engine:
   ├─ Collect: Telemetry data (every 30-60 sec)
   ├─ Analyze: ML algorithms (anomaly detection)
   └─ Predict: Pro-active risk prediction

3. Provisioning Orchestrator:
   ├─ Auto-generate: Device configs
   ├─ Push: NETCONF/RESTCONF deployment
   └─ Verify: Compliance vs intended state

4. Web Dashboard:
   ├─ Network health (device CPU/memory/disk)
   ├─ Client experience (latency, throughput, MOS)
   ├─ Application performance (per-app SLA)
   └─ Security posture (threats, posture compliance)
```

### ISE Integration
```
ISE + DNA Center workflows:
├─ User authenticates via 802.1x
├─ ISE validates identity (AD/LDAP backend)
├─ ISE assigns SGT based policy engine
├─ DNA Center provision: SGT → authorization rules
├─ Fabric nodes: Enforce SGACL automatically
└─ User roams: ISE CoA updates SGT (mid-session)

ISE Components:
├─ PAN (Primary Admin Node): Policy rules
├─ PSN (Policy Service Node): RADIUS AAA backend
├─ MnT (Monitoring & Troubleshooting): Logs + analytics
└─ MDM (Device Management): Posture validation, profiling
```

---

## Virtual Networks (VN)

### VN deployment example
```
Campus segmentation (4 VNs):

1. Corporate VN:
   ├─ Users (dept employees)
   ├─ Servers (business apps, databases)
   └─ Policies: Internal access allowed, strict security

2. Guest VN:
   ├─ Visitors (temporal access)
   ├─ Limited services (internet only)
   └─ Policies: Isolated from corporate, no access back

3. IoT VN:
   ├─ Sensors, cameras, building automation
   ├─ Limited bandwidth/CPU
   └─ Policies: One-way outbound only (to servers)

4. Management VN:
   ├─ WLCs, DHCP, DNS, ISE, Syslog
   ├─ Admin-only access
   └─ Policies: Restricted access, high security
```

### VN design rules
```
Each VN = Isolated broadcast domain
├─ Separate VXLAN tunnel (different VNI)
├─ Separate LISP map domain
├─ Inter-VN communication: Policy-controlled only
└─ SGT assignments: Defines which VN group belongs

Example policy cross-VN:
├─ Sales-Users (SGT 100, VN Corp) → file-servers (SGT 301, VN Corp) = PERMIT
├─ Sales-Users (SGT 100, VN Corp) → IoT-sensors (SGT 401, VN IoT) = DENY
└─ Admins (SGT 50, VN Mgmt) → all VNs = PERMIT (special privilege)
```

---

## Tableau: LISP vs VXLAN vs TrustSec

| Aspect | LISP | VXLAN | TrustSec |
|--------|------|-------|----------|
| **Layer OSI** | Control plane | Data plane | Policy enforcement |
| **Standard** | RFC 6830 | RFC 7348 | Cisco proprietary |
| **Fonction** | Map EID→RLOC | Encapsulate tunneling | SGT marking + SGACL |
| **Deployment** | SD-Access | Industry standard | Cisco (ISE) |
| **Mobility** | Dynamic remapping | IP reassignment | With ISE, CoA |
| **Integration** | DNA Center required | Works standalone | + ISE mandatory |

---

## Configuration checklist SD-Access deployment

```
☐ Phase 1: Underlay commissioning
  ├─ IP addressing planned
  ├─ DNA Center LAN Automation: Discovery → config generation
  ├─ OSPF adjacency verified (show ip ospf neighbor)
  └─ All fabric nodes reachable (ping, traceroute)

☐ Phase 2: Overlay provisioning
  ├─ LISP Map Server(s) configured + HA
  ├─ VXLAN VNI assigned + VLAN mapping
  ├─ VXLAN-GPO enabled on switches (hardware support check)
  └─ Initial reachability test (client IP stays same roaming)

☐ Phase 3: ISE + TrustSec integration
  ├─ ISE configured with AD/LDAP backend
  ├─ SGT assignment policies defined (per user/device/location)
  ├─ DNA Center + ISE API connectivity verified
  └─ SGACL policies deployed to fabric edge nodes

☐ Phase 4: Assurance validation
  ├─ DNA Center telemetry collection enabled
  ├─ Baseline health metrics established
  ├─ Alerting thresholds configured
  └─ Dashboard dashboards accessible to ops team

☐ Phase 5: Pilot + production rollout
  ├─ Test VN (pilot users): Verify policies + mobility
  ├─ Staging before full production
  ├─ User training: Identity-based vs IP-based policies
  └─ Runbook documentation (troubleshooting procedures)
```

---

## Dépannage rapide SD-Access

### LISP mapping issues
```
Debug LISP status:
show lisp map-cache  [verify EID→RLOC mappings]
show lisp statistics [request/reply counts]
debug lisp control [enable detailed logging]

Symptômes:
├─ No map entry: Client endpoint not discovered
  └─ Action: ISE profiling may be slow, manual SGT assignment possible
├─ Stale RLOC: Client roamed, RLOC not updated
  └─ Action: Trigger manual refresh (restart client connection)
```

### VXLAN encapsulation issues
```
Packet capture analysis:
├─ Filter: "vxlan" in Wireshark
├─ Verify: Outer IP = fabric RLOCs, VNI = configured value
└─ Check: G-Bit set (SGT should be present if enabled)

Symptoms:
├─ VXLAN decap fails: Client offline
  └─ Action: Check hardware support (some old switches)
├─ Wrong VNI: Traffic on different VN
  └─ Action: Verify VLAN→VNI mapping on edge nodes
```

### SGT assignment problems
```
Verify ISE assignments:
show mac-address-table dynamic [find client MAC]
show eigrp neighbors [verify routing]

ISE troubleshooting:
├─ Check: User in correct security group (AD membership)
├─ Check: Device profiling rules matching
├─ Check: CoA deployment intervals (slow changes = config delay)
└─ Action: Manual SGT override (temporary test)
```

---

## Ressources quick-lookup
- **VXLAN port**: UDP 4789 (IANA registered)
- **VNI range**: 0-16777215 (24 bits) = 16 million networks
- **SGT range**: 0-65535 (16 bits)
- **LISP Map Server**: HA pair recommended (2+ copies synchronization)
- **DNA Center default**: https://[IP]:8443/dnac (admin/Cisco123 default)
- **OSPF cost Gigabit**: 1 (100,000/1000)
- **Minimum MTU VXLAN**: 1554 bytes (1500 payload + 54 byte overhead)
- **ISE default port**: RADIUS 1812, API 8910
