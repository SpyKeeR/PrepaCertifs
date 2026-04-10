---
title: "Checkpoint CP9: Architecture Enterprise, Fabric & Network Assurance (Modules 22-24)"
checkpoint: CP9
modules: [22, 23, 24]
type: checkpoint-exam
topics: [enterprise-architecture, SD-Access, fabric, LISP, VXLAN, TrustSec, network-assurance]
difficulty: advanced
questions: 50
exam_duration: "90 minutes"
passing_score: "70% (35/50)"
updated: 2026-03-18
---

# Checkpoint CP9: Architecture d'Entreprise, Fabric & Assurance (50 questions)

**Format:** 50 questions certification-level | Scenario-based | Advanced difficulty
**Duration:** 90 minutes | **Passing Score:** 70% (35/50) | **Mastery Rubric:** 90%+ = expert

---

## Section A: Enterprise Architecture (Q1-25)

### **Q1: Multi-site campus topology design**

Global company 6 campuses (HQ + 5 regional branches). HQ = 40 distribution switches + 200 access switches + 10 data centers. Regional = 2-4 distribution each + 30-50 access. Recommended architecture HQ vs branches?

A) All sites = identical 3-tier (standardize operations easy management)
B) HQ = 3-tier (expensive justified scale), branches = simplified 2-tier (cost control)
C) HQ = leaf-spine (data center optimized), branches = collapsed core (WAN edge)
D) All sites = SD-Access fabric (modern unified platform)

**Réponse: B**

HQ 40 distribution pairs → genuine core layer justified (performance, redundancy, resilience)
Branches 2-4 distribution → 2-tier collapse acceptable (cost < HQ investment)
Mixed architecture common large enterprises (optimize each site)

---

### **Q2: VLAN scoping enterprise design**

HQ 50 VLANs (all 24-hour access). New policy: VLAN 100 (employees) limited hours 6AM-6PM only. Implementation?

A) Access layer filtering (port-based time policy)
B) Distribution + ACL scheduler (time-based permit/deny)
C) VLAN removal (disable VLAN off-hours, prevents access)
D) ISE policy (authentication + time-based VLAN assignment)

**Réponse: D**

ISE best practice (centralized identity + time context)
Template-driven policy (flexible, auditable, scalable)
ACL scheduling B) alternative but ISE modern + richer context

---

### **Q3: Layer 2 vs Layer 3 access hybrid**

Building A VLAN-based (legacy requirement 200 devices), Building B routed access (new network). Inter-building connectivity design?

A) Single L2 trunk (extend VLAN across buildings, STP convergence risk)
B) L3 routing between buildings (separate VLAN/IP ranges, inter-connect distribution)
C) Both models coexist, each optimized per building (hybrid valid complex)
D) Migrate all to routed access (standardize, deprecate L2)

**Réponse: C**

Legacy + new coexist reality (deprecation phased)
L2 Building A = legacy constraints
L3 Building B = future-state efficiency
Border devices handle translation (trunk + routed interface)

---

### **Q4: STP tuning convergence**

STP convergence time > 30 seconds (user complaints). Optimization options?

A) Lower bridge priority (faster root election)
B) RSTP enable (20s STP → 6s RSTP convergence)
C) Disable STP (routed access simplification)
D) All three valid options

**Réponse: D**

All valid per context:
- B = immediate improvement rapid RSTP
- C = best long-term (eliminate STP complexity routed)
- A = quick parameter tune (if root election delay issue)

---

### **Q5: OSPF area design campus**

Campus 100 routers organized 5 distribution pairs. OSPF area design?

A) Single area (all routers area 0, simple)
B) Area 0 (distribution) + 5 area 1-5 (per distribution pair access subtree)
C) Flat area across all (area 1, no area 0)
D) Area 0 only critical routers (distribution + core)

**Réponse: B**

Hierarchical area design optimal (distribution = area boundary router)
Summarization (area X route → AB summarize → area 0)
Scalability constraint (area 0 = backbone, distribution = ABR)

---

### **Q6: Access layer VLAN allocation**

Access switch 48 ports. Max VLANs per access port isolation?

A) 1 VLAN per port (4-port server exception)
B) Multiple VLAN trunk ports (inter-switch links)
C) Depends configuration (host vs trunk mode)
D) Unlimited (modern VLAN capability)

**Réponse: C**

Access mode = 1 VLAN only (access port)
Trunk mode = multiple VLANs (switch interconnect)
Design rule = star access (no inter-access trunk directly)

---

### **Q7: Redundancy distribution pair topology**

Distribution-A active (primary routing), Distribution-B standby. Failover time target = 1 second. Protocol?

A) STP (30s+ convergence, too slow)
B) HSRP (3s-5s failover, adequate)
C) VRRP (1s failover minimal)
D) LAG active-active (both lines active, instant failover)

**Réponse: D**

Active-active LAG ideal (both lines utilized + instant failover)
HSRP/VRRP B/C compromise (ok for 1s target with tuning)
STP too slow for sub-second failover

---

### **Q8: Core layer design validation**

Core topology should include:

A) Full mesh (every core router connects every core router)
B) Complete without single failure risk (CLOS fabric possible)
C) Shortest path preference (avoid extra hops)
D) All [A] [B] [C]

**Réponse: D**

Core design requires all three (full mesh standard, CLOS scalable alternative)
Single router failure = non-issue (alternate paths exist)
Path optimization critical (core bottleneck resource)

---

### **Q9: Service blocks edge connectivity**

Collapsed core 2-tier. WAN edge, Data Center, Internet blocks placement?

A) Access layer (not recommended, services = shared infrastructure)
B) Distribution layer (correct, shared edge services)
C) Separate tier (unnecessary, distribution capable)
D) Virtual (cloud-based, no physical campus router)

**Réponse: B**

Distribution = service block termination point
2-tier no separate core → distribution = core services
Access = user/device only

---

### **Q10: MTU path discovery misconfig**

End-to-end path MTU = 1200 bytes. Host assumes 1500 (Ethernet MTU). DF bit set (fragmentation prevention).

A) Ping works (ICMP ER from router)
B) Ping succeeds (lucky fragmentation avoided)
C) Ping fails (ICMP unreachable: fragmentation needed)
D) Dependent destination (external vs internal)

**Réponse: C**

Standard PMTUD (Path MTU Discovery)
IPv4 DF set + MTU required fragmentation = ICMP Type 3 Code 4
Ping fails until adjusted smaller

---

### **Q11: Hierarchical redundancy design**

Distribution-A pair (primary distribution), Distribution-B pair (secondary distribution, different building). Failure scenarios:

1. One distribution-A fails
2. Complete building-A power loss

Survivable both?

A) No (building-A outage = complete loss)
B) Yes if distribution-B provides full capacity backup
C) Depends (building-A restoration priority)
D) Design limitation (geographic separation trade-off)

**Réponse: B or D**

Building-A outage = users bypass to B (possible if B capacity sufficient)
Realistically geographic redundancy cost vs single-building failure risk trade-off
Preferred = true geographic diversity (different utility companies, zones)

---

### **Q12: VLAN summarization distribution**

HQ distribution-A: 10.0.0.0/24 - 10.0.9.0/24 (10 VLANs)
HQ distribution-B: 10.0.10.0/24 - 10.0.19.0/24 (10 VLANs)

OSPF summarization route distribution → core?

A) No summarization (10 separate routes × 2 distribution = 20 routes core)
B) Summarize distribution-A: 10.0.0.0/21 summarize (covers .0-.7)
C) Summarize distribution-A: 10.0.0.0/22 summarize (covers .0-.3)
D) Summarize both distribution: distribution-A=10.0.0.0/21 distribution-B=10.0.8.0/21 (slight overlap risk)

**Réponse: D** (careful subnet alignment)

Distribution-A 10.0.0.0/21 covers 10.0.0 - 10.0.7 (8 subnets)
Distribution-B offset 10.0.8.0/21 covers 10.0.8 - 10.0.15 (8 subnets)
20 routes → 2 summarized (excellent scaling)

---

### **Q13: Access layer design scalability limit**

Single distribution pair with 64 access switches attached (star topology, each access = 48 ports). Practical limit?

A) No limit (all 64 possible)
B) ~32 access (oversubscription ratio management)
C) ~16 access (STP, VLAN propagation concern)
D) ~8 access (per-interface bandwidth limitation)

**Réponse: B**

Oversubscription 2:1 typical (64 access × 48 ports = 3k devices, 2× distribution capacity)
STP convergence not typically bottleneck unless VLAN count excessive
Bandwidth fundamental scaling

---

### **Q14: Collapsed core service delivery**

2-tier design. Database server (critical database), backup server (HA pair), Internet gateway - all attach distribution layer?

A) Yes (all critical services equal distribution attachment)
B) Separate placement recommendations (different priority backup only)
C) Database + backup = distribution, Internet = separate (firewalled)
D) All distributed (redundancy architecture)

**Réponse: C or D**

Database + backup = distribution attachment (LAN resilience priority)
Internet edge = typically security border (separate firewall, not direct distribution)
Depends security model (unified vs segmented)

---

### **Q15: OSPF multi-area complexity**

2 area design (area 0 distribution + area 1 access). Access link down. Reconvergence time?

A) Few seconds (OSPF routed = fast, no STP)
B) Area 0 + area 1 separate reconvergence (ABR aggregates)
C) Area 1 reconverge, area 0 unchanged (summarization isolates)
D) Full network reconvergence (all routers impact)

**Réponse: C** (best case hierarchical area design)

Area 1 failure = area 1 converge locally (few seconds)
ABR summary route unchanged (area 0 unaware details)
Other area 1 subnets temporarily unreachable (failover recovery alternative paths)

---

### **Q16: Leaf-spine data center adopted campus**

East-west traffic (server-to-server) = 80%, north-south (Internet) = 20%. Topology impact?

A) Traditional 3-tier excessive (north-south designed)
B) Leaf-spine optimized (east-west priority)
C) Depends application (cache vs cloud split)
D) Hybrid (top-of-rack + core specialization)

**Réponse: B**

Leaf-spine = 2-hop maximum all traffic (east-west optimized)
3-tier inherently north-south (uneven path lengths)
DC modern standard (leaf-spine superior 80% traffic pattern)

---

### **Q17: Network device power consumption scaling**

Core layer 4 routers (high-end modular). Distribution 10 routers (mid-range). Access 64 switches (fixed). Power estimate?

A) Access > distribution + core (scale)
B) Core > distribution > access (performance)
C) Similar all (standardized per device)
D) Depends deployment

**Réponse: A** (typically access most devices = total power)

Access 64 × 125W = 8KW
Distribution 10 × 250W = 2.5KW
Core 4 × 500W = 2KW
Total = 12.5KW (access 64% power budget)

---

### **Q18: QoS marking hierarchy**

Access layer marks packets DSCP EF (VoIP priority) per user port. Distribution applies re-marking (DSCP CS7 = highest).

A) Correct (distribution can override access marking)
B) Incorrect (access marking sacred, no rewrite)
C) Conditional (depends trust boundary policy)
D) Forward error (conflict resolution undefined)

**Réponse: C**

Trust boundary design critical (typically access = trust, distribution = enforce policing)
Override possible (policy call, may conflict if customer SLA expects EF)
Best practice = consistent marking (one-pass, no re-marking)

---

### **Q19: Campus expansion planning**

Current 20 distribution switches. Growth plan = 5 years, 100 distribution (5× increase). Architecture evolved?

A) Stay 3-tier (add more core capacity)
B) Transition SD-Access fabric (modern scalable)
C) Leaf-spine campus (data center style)
D) Multiple independent campuses (geographic split)

**Réponse: B or D** (both valid evolution strategies)

B = SD-Access scales VXLAN/LISP (modern best practice)
D = Geographic distributed (independent campuses resilient)
A = 3-tier limits realistically (~50 distribution practical max)

---

### **Q20: VLAN engineering numbering scheme**

Design 500+ VLAN campus. Allocation strategy?

A) Sequential 1-500 (simple tracking)
B) Hierarchical 1xx=site, x2x=function (scalable, self-documenting)
C) Random assignment (irrelevant, VLAN ID just number)
D) Per-device allocation (switch manages VLANs)

**Réponse: B** (hierarchical best practice)

101-109 = HQ building 1 (VoIP)
111-119 = HQ building 1 (data)
201-209 = branch 1 VoIP (etc)
Self-documentation + reduced allocation errors

---

### **Q21: Network services in core/distribution**

Services location recommendation:

A) Core only (backbone critical path)
B) Distribution only (scalable edge service)
C) Distributed (HA pair distribution services)
D) Separate (services tier non-routed access)

**Réponse: C** (HA pair distribution typical)

DHCP, DNS, internal services = distribution location
HA pair = redundancy
Separate tier = unnecessary complexity campus scale

---

### **Q22: STP root bridge election multi-building**

Building A distribution-A (priority 8192), Building B distribution-B (priority 12288), Building C distribution-C (default 32768). Root bridge selection?

A) Building A distribution-A (lowest priority = root)
B) Building B distribution-B (secondary lowest)
C) Building C distribution-C (backup)
D) Tie-break by MAC address (if equal priority)

**Réponse: A** (lowest priority elected root)

8192 < 12288 < 32768 → distribution-A root
Building A key infrastructure location (STP root placement)

---

### **Q23: Routed access protocol selection**

Routed access implementation. OSPF vs IS-IS comparison. Campus choice?

A) OSPF (widespread routing legacy support)
B) IS-IS (modern efficient, carrier-grade)
C) Either (both support routed access)
D) BGP (not campus typical)

**Réponse: A or C** (OSPF most common campus, IS-IS alternative valid)

OSPF = RFC abundance, familiarity, quick convergence (~3s)
IS-IS = tlv-efficient, faster convergence possible
Campus = OSPF standard (BGP = WAN typical)

---

### **Q24: Campus growth NMS capability**

Current 500 devices (Syslog + SNMP v2c basic monitoring). Growth = 5000 devices (10x). Assurance capability?

A) Stick SNMP v2c (scale with collector)
B) Add SNMP v3 (encryption + auth)
C) Adopt streaming telemetry + DNA Center (modern assurance)
D) Hybrid v2c core + v3 new devices (gradual migration)

**Réponse: C** (modern assurance platform)

DNA Center = AI/ML analytics (predictive, not reactive)
SNMP v2c 5000 devices = problematic scale (v2c = no encryption, less efficient)
Streaming telemetry = faster, richer data DNA Center processes

---

### **Q25: Interconnection design resilience**

HQ distribution pair connected core by 4 physical links (LAG 4× 10Gb). Single link failure impact?

A) No impact (LAG redundancy, other 3 links active)
B) Capacity reduction LAG 30Gb → 20Gb (25% loss)
C) Brief interruption (LAG reconvergence <1s)
D) Both [A] and [B]

**Réponse: D** (no traffic loss, capacity impacts)

LAG redundancy active-active
Single link failure = LAG rebalance (sub-second)
Throughput reduced proportionally (3/4 capacity)

---

## Section B: Fabric & Network Assurance (Q26-50)

### **Q26: Fabric underlay design automation**

DNA Center LAN Automation discovers 50-switch campus underlay. Configuration automation steps?

A) Manual CLI per router (no automation)
B) DNA Center discovers topology → auto-generates OSPF config → NETCONF push
C) Pre-configured template (zero discovery)
D) Mesh VLAN connectivity (non-routed)

**Réponse: B** (DNA Center golden path automation)

Discovery = topology learning
Config generation = OSPF cost, areas, summary optimization
NETCONF/YANG push = atomic application

---

### **Q27: LISP mobility example**

Client EID 10.1.1.100:
- Hour 1: connects AP1 (RLOC 192.168.1.50)
- Hour 2: roams AP2 (RLOC 192.168.1.51)
- Hour 3: roams off-campus VPN (RLOC 1.2.3.4 public IP)

LISP mapping entry evolution?

A) Fixed (EID → single RLOC permanent)
B) EID unchanged, RLOC updated (EID portable concept)
C) New EID assigned (new network = new identity)
D) Dual mapping (old + new RLOCs)

**Réponse: B** (LISP core concept: EID identity, RLOC location)

EID 10.1.1.100 = client identity (session-persistent)
RLOC changes as roaming occurs (Map Server updates → ITR lookup)
VPN RLOC = public endpoint allocation (fabric can tunnel multi-hop)

---

### **Q28: VXLAN gateway function**

Traditional switch (non-fabric) VLAN 100. Fabric overlay VXLAN VN100. Gateway connectivity?

A) Direct connection (no gateway needed)
B) VXLAN gateway device (convert VLAN ↔ VXLAN)
C) ISE mediation (identity-based translation)
D) No connectivity (fabric isolated)

**Réponse: B** (fabric border/gateway device needed)

Gateway device "translates" VLAN frames → VXLAN VLAN100↔VN100
Typically Catalyst border router or ASR edge
ISE C) = authentication, not bridging

---

### **Q29: VXLAN-GPO field content**

VXLAN encapsulated packet contains:
[IP][UDP 4789][VNI-24bit][???][Payload]

Missing field composition?

A) Layer 3 IP header (no, already outer IP)
B) VXLAN-GPO "group policy" 16-bit SGT + flags
C) Ethernet FCS (no, layer 2 removed)
D) Custom app header (no standard)

**Réponse: B** (VXLAN-GPO = SGT encoding data plane)

G-bit = group policy present flag
D-bit = don't learn flag (no source MAC learning)
A-bit = unknown unicast address bit

---

### **Q30: TrustSec SGT assignment workflow**

User "alice@accounting" connects ISE-enabled WLAN. SGT decision process?

A) Manual allocation (admin assigns)
B) ISE policy engine evaluates identity + device → SGT 105 (accounting group)
C) Device self-selection (not scalable)
D) Random SGT (non-deterministic)

**Réponse: B** (ISE intelligent identity + device profiling)

ISE rules: IF department="Accounting" AND device="Corporate-Laptop" THEN SGT=105
Deterministic, auditable, scalable

---

### **Q31: SGACL enforcement direction**

SGACL: SGT100 (Sales) → SGT301 (Printers) allow TCP 9100

Enforcement location + direction?

A) Ingress Sales (before entering fabric)
B) Egress Printer side (exiting fabric, targeting SGT301)
C) Core per-router (mid-fabric nodes)
D) Bi-directional (both directions)

**Réponse: B** (egress enforcement standard)

Egress enforcement = after destination identified
SGT101 packet exiting toward SGT301 = enforcement point
Reverse flow (SGT301 → SGT100) = separate policy rule

---

### **Q32: SD-Access failover wireless active-active**

Dual WLC active-alike, same fabric VNs. Client roams WLC-A → WLC-B. Tunnel state?

A) Interruption (tunnel switchover delay)
B) Seamless (LISP mobility handles WLC-B RLOC update)
C) Depends (fabric intelligence unknown)
D) Requires ISE failover sync (identity follow-along)

**Réponse: B** (LISP roaming elegant)

WLC-A RLOC = 192.168.1.1
WLC-B RLOC = 192.168.1.2
Client roam = Map Server learns new RLOC
Existing ITR → ETR tunnel transparently updated (LISP clever)
ISE sync D) = additional layer (not required tunnel continuity)

---

### **Q33: Virtual Network isolation enforcement**

Corporate VN (trusted), Guest VN (untrusted). Client roaming Corprate → Guest VLAN?

A) Automatic (same network, VLAN change transparent)
B) Blocked (VN boundary = security boundary)
C) Policy override (manual VLAN assignment possible, breach)
D) ISE redirection (user re-authentication, policy mismatch detected)

**Réponse: D** (ISE policy enforcement catches mismatch)

VN isolation = primary security (prevent cross-VN)
Roaming same device = ISE policy re-evaluation needed
Mismatch = CoA enforcement (client pulled different VN)

---

### **Q34: Fabric scalability vs traditional 3-tier**

Campus 50,000 devices (wireless + wired). Architecture comparison?

A) Traditional 3-tier = 500 distribution × 3-tier (management nightmare)
B) Fabric = VXLAN segments 4094 VXLAN IDs possible (scaling elegant)
C) Both equally scalable (depends tools)
D) 50K = cloud-only (campus design limit)

**Réponse: B** (fabric modern scaling design)

VXLAN VNI = 24-bit = 16M possible (practical ~4094)
4094 VNs vs 4094 VLAN limit = no difference (VN = VLAN+++ policy)
Fabric = LISP/VXLAN (design elegant overlay)
3-tier = STP/OSPF (design adequate, less elegant)

---

### **Q35: DNA Center assurance anomaly detection**

Client "laptop1" roaming pattern:
- Week 1-2: AP1 → AP2 → AP3 (Monday-Friday pattern)
- Week 3: AP1 → AP5 → AP8 (unusual roaming distance)

DNA Center alert?

A) No alert (expected variation)
B) Alert roaming behavior change (anomaly detected)
C) Network issue investigation (AP connectivity problem)
D) Automatic quarantine (security threat response)

**Réponse: B** (DNA Center behavioral baseline learning)

ML baseline = typical roaming (AP1-3 proximity)
Week 3 deviation = anomaly (alert investigation)
C) = possible root cause (but alert primary)
D) = overkill without confirming reason (could be legitimate campus expansion)

---

### **Q36: Ping extended options WAN testing**

Campus ↔ Branch WAN latency test. Requirements:
- End-to-end delay measure
- Path MTU discover
- QoS class verification

Which ping options?

A) Standard `ping` (basic only)
B) Extended ping: timeout, repeat, DF bit, ToS field
C) Traceroute (different tool)
D) Both [B] standard ping insufficient

**Réponse: B** (extended ping capability)

Ping options:
- timeout = delay tolerance
- DF bit = MTU troubleshooting
- ToS = QoS class test (ToS 184 = EF DSCP)
- source IP = routing path selection test

---

### **Q37: OSPF adjacency state machine troubleshooting**

Debug shows:
```
OSPF: Hello received from [neighbor]
OSPF: 2WAY communication
OSPF: ExStart received [seq 100]
OSPF: ExStart received [seq 99] - retransmit
[stuck, never progresses]
```

Likely cause?

A) MTU mismatch (database exchange stuck at DD sequence)
B) Hardware issue (link physical problem)
C) Neighbor reboot (sequence number reset)
D) Timer mismatch (hello/dead synchronization)

**Réponse: A** (MTU mismatch classic OSPF issue)

DD = Database Descriptor fragment (payload sensitive MTU)
MTU < fragmentation needed = DD loss, retransmit loop
Solution: verify `show ip interface [interface]` MTU both sides = match

---

### **Q38: NetFlow export troubleshooting**

NetFlow collector receiving flows from R1 (10.0.0.1) but ICMP ping to collector successful.

A) Flow export working (collector confirms)
B) Collector unreachable (ICMP success ≠ UDP 2055 success)
C) Depends export version (v5 vs v9 different ports)
D) Network ACL blocking NetFlow only

**Réponse: B or D** (ICMP ≠ UDP, ACL possible)

ICMP permitted ≠ UDP 2055 permitted (separate ACL rules)
Debug: `debug ip flow export` (shows export failures)
Verify: `show ip flow export counters` (export packet count)

---

### **Q39: SPAN ERSPAN deployment scale**

WLC SPAN source (mirror AP traffic 100Mbps expected), analyzer remote (GRE tunnel). ERSPAN CPU impact analyzer?

A) Negligible (GRE decapsulation minimal)
B) ~10% CPU (processing metadata extraction)
C) Variable (depends analyzer model + traffic volume)
D) Unacceptable (ERSPAN reserved lab only)

**Réponse: C** (depends architecture)

High-end analyzers (dedicated network TAP) = minimal impact
Software-based analyzer (laptop Wireshark) = significant (100Mbps challenging)
Professional network monitor = engineered ERSPAN (acceptable <5% overhead)

---

### **Q40: IP SLA RTT baseline per application**

Company SLA: User video=<50ms, VoIP=<150ms, email=<500ms

IP SLA probes requirement?

A) Single HTTP probe (represents all)
B) Three probes (video=ICMP, VoIP=UDP jitter, email=TCP)
C) Flow-based (aggregate all traffic baseline)
D) Depends application protocol

**Réponse: B or D** (application-specific probes)

ICMP = network path generic
UDP jitter = real-time focused (VoIP-realistic)
TCP Connect = application availability check (email)
Aggregate probing = better insights

---

### **Q41: DNA Center telemetry data volume**

500 devices reporting telemetry 30s interval (10MB per device per hour).

A) 500 × 10MB/hr = 5GB/hr = 120GB/day (storage planning needed)
B) Compressed/deduplicated reducing (actual ~20-30% raw)
C) Streaming filtered (not all data stored)
D) Calculate actual required capacity

**Réponse: D** (realistic planning = 20-50 GB/day likely)

Raw = 5GB/hr = 120GB/day (unrealistic)
Deduplicated = 20-30% compressibility
Filtered streaming = sample not store all
Reality = 20-50 GB/day (week = TB size)
SIEM database sizing critical

---

### **Q42: Encrypted traffic health monitoring**

VPN headend traffic (all encrypted). DNA Center visibility?

A) Zero visibility (encryption opaque)
B) Flow statistics + behavioral analysis possible
C) Payload analysis requiring decryption (privacy issue)
D) Both [B] no payload needed

**Réponse: D** (behavioral sans decryption)

Flow: source, destination, volume, rate, packet size
Behavioral: normal = consistent volume spike = anomaly
Encryption irrelevant (application-layer agnostic)

---

### **Q43: OSPF adjacency failure recovery timing**

neighbor down → reconvergence how long?

A) Hello timeout = dead interval = 40s (default broadcast)
B) Less (OSPF flood immediately notification)
C) Faster with tuning (hello 1s, dead 4s possible)
D) Depends detection (failure type)

**Réponse: C** (tunable for sub-second convergence)

Default Broadcast = 10/40 → 40s convergence
Point-to-point = 10/40 (same)
Tuned aggressive = 1/4 → 4s convergence
Fast failure detection = OSPF bfd (sub-100ms)

---

### **Q44: NetFlow unidirectional flow tracking**

Client→Server: 5 packets, 1KB
Server→Client: 8 packets, 100KB

NetFlow v9 tracking as?

A) Single bi-directional flow (aggregate both directions)
B) Two unidirectional flows (A→B separate B→A)
C) Depends ingress/egress interfaces (sampling point)
D) Collector determines post-processing

**Réponse: B** (NetFlow v9 directional)

NetFlow v9/IPFIX tracks direction (source/dest asymmetry captured)
v5 = aggregate bidirectional
v9 = separate flows per direction (richer detail)

---

### **Q45: SNMP v3 encryption authentication**

Configuration:
```
snmp-server user alice v3 auth sha password123 priv aes password456
```

A) alice user, SHA authentication, AES 128-bit encryption
B) alice user, password123 auth, password456 encr (separate)
C) alice user, both passwords sampled (less secure)
D) Configuration invalid (SNMP v3 syntax)

**Réponse: A** (SNMP v3 auth + priv correct)

- auth SHA = authentication, message integrity
- priv AES = privacy encryption
- Passwords = key derivation (not literal)

---

### **Q46: Syslog filtering assurance**

Campus 5000 devices syslog → central server. Log volume overwhelming (100,000 msgs/min). Filtering strategy?

A) No filtering (collect all, analyze later)
B) Device-level filtering (each device send critical+ only)
C) Parser-side filtering (server processes, stores critical)
D) Both [B] and [C] (belt + suspenders)

**Réponse: D** (optimal data reduction)

Device filtering = reduce network bandwidth (first filter point)
Server parsing = secondary (catch device-config misses)
Critical/alert only = ~20-30% of raw traffic typically

---

### **Q47: Predictive analysis DNA Center limits**

Historical data 3 months (storage available). Predictive accuracy?

A) Excellent (seasonality captured)
B) Fair (3-month pattern limited)
C) Poor (requires 1+ year baseline)
D) Good enough business decision

**Réponse: D** (context-dependent)

3-month = captures quarterly cycles (conferences, fiscal)
Not seasonal (requires annual)
Good for tactical planning (maintenance windows)
Limited strategic (long-term trend analysis)

---

### **Q48: Troubleshooting priority multi-layer issue**

User report: "Email slow"

Investigation findings:
- Ping: 5ms (ok)
- DNS resolution: 200ms (high)
- SMTP: 2000ms (high)
- Network trace: 0% packet loss

Root cause layer?

A) Network (packet loss observed)
B) Application (SMTP latency, email server issue)
C) DNS (resolution delay affecting email client)
D) Multiple (chain: DNS → SMTP server overload)

**Réponse: D** (likely chain DNS delay + SMTP slow)

DNS 200ms = suspicious (should < 50ms)
SMTP 2000ms = application layer (more critical)
Combined = cascading failure (DNS slow → app timeout retry → SMTP overload)
Priority: SMTP server (investigate first)

---

### **Q49: Change management assurance windows**

Maintenance window: Maintenance distribution router (planned 30min). Assurance pre/post verification?

A) Before change (baseline capture DNA Center)
B) During change (monitor convergence live)
C) After change (verify restoration to baseline)
D) All three checkpoints

**Réponse: D** (comprehensive change validation)

Before = baseline metrics capture
During = real-time convergence monitoring (detect issues)
After = post-change stability (trending anomaly detection)
Change success = quantified by baselines

---

### **Q50: Compliance auditing through assurance**

Regulation: "Network changes logged, approved, auditable trail required."

Which assurance component meets requirement?

A) NetFlow alone (insufficient, no change context)
B) Configuration syslog (what changed, not context)
C) DNA Center + ISE + syslog (change + identity + approval)
D) Manual ticket tracking (external, non-automated)

**Réponse: C** (integrated compliance narrative)

DNA Center = topology changes (device config)
ISE = policy changes (identity-driven)
Syslog = detailed logs (audit trail)
Combined = compliance audit package
D) = necessary supplementary (ticketing system context)

---

## Exam Rubric & Scoring

**Total: 50 questions** | **Duration: 90 minutes** | **Passing: 70% (35/50)**

**Breakdown by section:**
- **Section A**: Q1-25 (Enterprise architecture) - 25 points
- **Section B**: Q26-50 (Fabric + Assurance) - 25 points

**Mastery Rubrics:**
- **90-100% (45-50 points):** Expert-level understanding, ready advanced troubleshooting
- **80-89% (40-44 points):** Strong mastery, certification-ready
- **70-79% (35-39 points):** Passing, gaps exist, study weak areas
- **<70% (<35 points):** Review material, re-test after study

**Target Performance:** ≥80/50 (41+ points) for certification confidence
