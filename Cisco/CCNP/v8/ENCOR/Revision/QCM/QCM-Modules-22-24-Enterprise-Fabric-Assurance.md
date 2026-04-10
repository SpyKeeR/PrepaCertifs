---
title: "QCM Module 22-24: Architecture Enterprise, Fabric & Assurance"
modules: [22, 23, 24]
type: qcm
topics: [hierarchical-design, SD-Access, fabric, LISP, VXLAN, network-assurance, monitoring]
difficulty: [intermediate, advanced]
questions: 75
updated: 2026-03-18
---

# QCM Module 22-24: Architecture Enterprise, Fabric & Assurance (75 questions)

**Format:** 75 questions (25 per module) | Difficulté progressive
**Target Score:** ≥ 60/75 (80%) pour certification readiness

---

## Module 22: Architecture d'entreprise (Q1-25)

### **Q1: Three-tier decision criteria**

Campus de 6 bâtiments, 15 distribution pair planifiées. Quel modèle?

A) 2-Tier (collapsed core) = cost effective
B) 3-Tier (dedicated core) = scalability critical
C) Leaf-Spine = WAN-optimized
D) SD-Access = moderna overlay

**Réponse: B** - 15 distribution pairs > 3 seuil → core layer nécessaire

### **Q2: Access layer design rule**

Access switches configuration correcte?

A) Dual-connected (AP1 → Dist-A AND Dist-B with STP)
B) Single uplink (AP1 → Dist-A only, single point failure)
C) Mesh (Access1 ↔ Access2 interconnected, prevents loops)
D) Star topology (ALL ports end-devices, uplinks only to distribution)

**Réponse: D** - Access = star (pas inter-access directe)

### **Q3: Distribution layer functions**

Distribution agrège 8 access switch. Quels rôles?

A) Pass-through switching (no additional processing)
B) L2/L3 boundary + STP root + IP route summarization
C) Core backbone (direct WAN connect)
D) Client authentication (ISE integration)

**Réponse: B** - Distribution = aggregation + routing + STP

### **Q4: Core layer link topology**

4 core switches. Combien liens full mesh?

A) 4 links (star topology core)
B) 6 links (full mesh = 4×3/2)
C) 8 links (each pair redundancy)
D) 12 links (dual paths each)

**Réponse: B** - N(N-1)/2 where N=4: 4×3/2 = 6

### **Q5: Layer 2 Access model**

VLAN 100 spans Acc-1, Acc-2, Acc-3. STP state mostlikely?

A) No STP (single access = no loop possible)
B) STP one active trunk (loop prevention)
C) RSTP all trunks active (fast convergence)
D) Mesh no STP (triangle topology supported)

**Réponse: B** - Multi-access VLAN = STP required (one trunk blocked)

### **Q6: Layer 3 Access routing**

Access-A VLAN 10 (10.1.0.0/24), Access-B VLAN 20 (10.2.0.0/24). Routing between?

A) Direct access-to-access (no distribution hop)
B) Via distribution layer (distribution = L3 gateway)
C) Via OSPF adjacency (routed access model)
D) Static routing (manual route configuration)

**Réponse: C** - Routed access = OSPF peer-to-peer (direct adjacency)

### **Q7: STP Priority Configuration**

Distribution-A = root bridge (priority = ?). Distribution-B backup (priority = ?).

A) Dist-A=0, Dist-B=4096 (0 = prevent override)
B) Dist-A=4096, Dist-B=8192 (standard values)
C) Dist-A=32768, Dist-B=16384 (defaults)
D) Dist-A=40960, Dist-B=45056 (custom increment)

**Réponse: B** - Standard: root=4096, backup=8192 (multiples 4096)

### **Q8: DHCP scope allocation**

VLAN 100 subnet 10.1.0.0/24 (gateway 10.1.0.254). DHCP scope ideally where?

A) Access switch (limited DHCP server capability)
B) Distribution switch (centralized DHCP)
C) Dedicated DHCP server (scalable, HA)
D) WLC (wireless devices only)

**Réponse: C** - Centralized DHCP server infrastructure (HA pair typical)

### **Q9: Campus two-tier edge blocks**

Collapsed core design. Outside blocks connect WHERE?

A) Only core (non-existent separate core)
B) Distribution pairs (edge services)
C) Access switches (not recommended)
D) Separate tier (doesn't fit 2-tier model)

**Réponse: B** - 2-tier: distribution = core + distribution combined (edge blocks attach distribution)

### **Q10: Routed access STP impact**

Routed access implementation. STP required?

A) Yes (still prevent loops at data link)
B) No (routing naturally loop-free)
C) Partial (STP disabled, OSPF loop detection)
D) Optional (HSRP alternative)

**Réponse: B** - Routed = IP loop prevention (STP unnecessary)

### **Q11: VLAN trunking mismatch error**

Access switch trunk VLAN 1,100,200,300. Distribution receives VLAN 1-4000 (all). Access switch VLAN 200 traffic NOT routed. Why?

A) VLAN 200 not on trunk (configuration missing)
B) STP blocked VLAN 200 port (convergence issue)
C) VLAN 200 on trunk, but not configured distribution (L3 missing)
D) MTU mismatch (VLAN jumbo frames, regular frames)

**Réponse: C** - Trunk passthrough VLAN data (L3 interface required routing)

### **Q12: Core throughput calculation**

5 distribution pairs, each 10Gb uplink to core. Core full-mesh = minimum aggregate design?

A) 10Gb (single link all)
B) 20Gb (2 distribution pairs)
C) 40Gb (4 × 10Gb)
D) 100Gb full mesh unlikely (cost)

**Réponse: D** - Core design = highly dependent scale (typically 40+ Gbps aggregate minimum large campus)

### **Q13: IP subnetting hierarchy**

Campus 10.0.0.0/16. Distribution pairs 10.X.0.0/24. Access VLAN 10.X.Y.0/25. Allocation efficient?

A) Inefficient (wasted address space /25 restrictive)
B) Efficient (hierarchical summarization works)
C) Impossible (overlap risk distribution/access)
D) Only works IPv6 (IPv4 fragmentation issue)

**Réponse: B** - Hierarchical 10.0.0.0/16 → /24 dist → /25 access = good design

### **Q14: Collapsed core MPLS deployment**

2-tier campus. MPLS backbone terminates where?

A) Core layer (non-existent 2-tier)
B) Distribution pairs (edge routers)
C) Access switches (can't do MPLS)
D) Separate tier (beyond 2-tier scope)

**Réponse: B** - 2-tier: distribution = core function (MPLS edge routers distribution-level)

### **Q15: Campus simplifiée (single building)**

Petit bureau (100 users, 1 building). Recommended architecture?

A) Full 3-tier (overkill)
B) 2-tier collapsed (right fit)
C) Single distribution (non-redundant)
D) Leaf-spine (data center architecture)

**Réponse: C or B** - Single distribution + redundant access acceptable (or dual distribution simplified)

### **Q16: OSPF cost configuration**

Distribution-A uplink Gigabit (cost 1). Distribution-B uplink serial 256k (cost 391). Traffic prefers which link?

A) Cost 1 (lower cost preferred)
B) Cost 391 (parallel path balancing)
C) Automatic ECMP (equal cost)
D) Serial link (legacy preference)

**Réponse: A** - OSPF selects minimum cost path (1 < 391)

### **Q17: Network segmentation VLAN scope**

Guidelines: VLAN 100 span maximum 3 access switches. Risk if larger?

A) No risk (L2 scale unlimited)
B) Risk = STP complexity (larger VLANs = more STP instances)
C) Risk = convergence time (topology changes affect many users)
D) Both [B] and [C]

**Réponse: D** - Large VLAN scope = STP complexity + convergence impact

### **Q18: Access switch stacking**

3 switches stacked (single logical unit). Supported architecture?

A) Valid access layer (simplified cabling, single management)
B) Invalid (stacking = implicit mesh, breaks design rule)
C) Depends (can work if no inter-stack trunking)
D) Recommended (modern approach)

**Réponse: A** - Stack = logical switch (single unit, valid access design)

### **Q19: PoE power budget**

Distribution pair must power 200 APs (15W each = 3000W needed). Approach?

A) Single power supply distribution (undersized)
B) Redundant PSU pairs distribution (HA power)
C) Dedicated power module (injection modules via distribution)
D) Both [B] and [C]

**Réponse: D** - High PoE load = redundant + potential injection points

### **Q20: ERP (Ethernet Ring Protection)**

Campus ring topology (loop). STP adequate?

A) Yes (STP prevents loops)
B) No (STP single-tree, ring ring inefficient)
C) PVST (per-VLAN spanning different trees)
D) Ciscos proprietary ERP (ring-specific protocol)

**Réponse: C** - PVST+ allows multiple STP instances per VLAN (ring optimization possible)

### **Q21: Firewall placement campus**

Security-important. Firewall connects:

A) Access layer (near users, inspection heavy)
B) Distribution layer (traffic aggregation point)
C) Core layer (all campus traffic inspection required)
D) Separate tier (DMZ architecture)

**Réponse: D or C** - Firewall typically separate (or core border, not access/distribution)

### **Q22: Link aggregation (LAG) implementation**

Distribution pair redundancy. Uplinks aggregated LAG (2×10G = 20Gb)?

A) Yes (bundle for capacity + redundancy)
B) No (LAG unnecessary, individual paths sufficient)
C) Depends (cost vs performance trade-off)
D) Impossible (LAG not supported large campus)

**Réponse: A** - LAG improves throughput + failover (redundancy elegant)

### **Q23: Campus migration 2-tier → 3-tier**

Growth = 5 distribution pairs planned. Migration strategy?

A) Flag-day cutover (all devices simultaneously)
B) Phased (add core nodes, redirect traffic gradually)
C) Parallel (run both 2-tier + 3-tier, switch after stabilization)
D) Non-disruptive overlay (add 3-tier UNDERlay, migration transparent)

**Réponse: B or D** - Phased migration preferred (minimizes disruption)

### **Q24: SNMP monitoring hierarchical design**

Campus 2000 switches + APs. Centralized SNMP collector sufficient?

A) Yes (single collector scales unlimited)
B) No (aggregator tiers needed = collector → collector → central)
C) Depends (2000 devices = likely yes with proper engineering)
D) Optional (not critical infrastructure)

**Réponse: C** - Scalability depends engineering (2000 devices challenging, hierarchical aggregation helps)

### **Q25: Scenario exam - Multisite design**

Company HQ + 5 branch offices, WAN Cisco MPLS backbone. Campus design philosophy?

A) Each site = independent 2-tier (no inter-site L2)
B) HQ = 3-tier, branches = 1-tier (star architecture)
C) All sites = identical (standardized design)  
D) Each site best-fit (HQ=3-tier, branches=simplified collapse)

**Réponse: D** - Optimize per-site (HQ expensive justified, branches cost-conscious)

---

## Module 23: SD-Access & Fabric (Q26-50)

### **Q26: Fabric network definition**

Fabric network = ?

A) Physical topology (switches connected physically)
B) Virtual overlay network (tunneling über physical underlay)
C) Routing protocol (OSPF fabric)
D) Cloud connectivity (public cloud link)

**Réponse: B** - Fabric = virtual overlay (VXLAN tunnels over physical network)

### **Q27: DNA Center role SD-Access**

DNA Center functionality primary?

A) Syslog aggregation (logging only)
B) Network orchestration + policy management + assurance
C) Firewall management (security appliance)
D) Cloud storage (data warehouse)

**Réponse: B** - DNA Center = central intelligence (automation, policy, analytics)

### **Q28: Underlay network automation**

DNA Center LAN Automation discovers 50 switches. Configuration approach?

A) Manual CLI per switch (tedious but controlled)
B) Template generation + automated NETCONF push (scale)
C) Vendor scripts (third-party, limited features)
D) No automation (switches pre-configured)

**Réponse: B** - DNA Center automates underlay (IP, OSPF, etc.)

### **Q29: LISP EID vs RLOC**

Client IP 10.1.1.50 roams AP1 (RLOC 192.168.1.1) → AP2 (RLOC 192.168.1.2). Mapping change?

A) EID 10.1.1.50 → RLOC 192.168.1.1 (before) → RLOC 192.168.1.2 (after)
B) EID 10.1.1.50 (unchanged), RLOC updates only
C) Both EID + RLOC change (complete remapping)
D) No change (static mapping permanent)

**Réponse: B** - LISP mobility = EID portable, RLOC changes

### **Q30: VXLAN encapsulation format**

VXLAN-GPO header after VNI (24-bit) contains?

A) Only source/dest IP (no change from standard VXLAN)
B) Group Policy ID (16-bit SGT) + flags (G,D,A bits)
C) Encryption keys (inline security)
D) Compression header (bandwidth optimization)

**Réponse: B** - VXLAN-GPO = VNI + GPO fields (SGT tagging data plane)

### **Q31: SGT (Scalable Group Tag) assignment ISE**

User "john@sales" joins wireless. SGT assignment workflow?

A) Manual admin assign (not scalable)
B) ISE policy engine (IF user=Sales THEN SGT=100)
C) Automatic device detection (IoT = SGT 50 auto)
D) Both [B] and [C] (multiple assignment methods)

**Réponse: D** - ISE flexible (user identity + device profiling both SGT sources)

### **Q32: SGACL enforcement point**

SGACL policy: "SGT100→SGT301 allow TCP 80,443". Enforcement occurs WHERE?

A) Ingress switch (source side, before encapsulation)
B) Egress switch (destination side, after decapsulation)
C) Core fabric (middle routers, transport agnostic)
D) Client device (local policy check)

**Réponse: B** - Egress enforcement (extract SGT from VXLAN-GPO, apply SGACL)

### **Q33: SD-Access 4-layer architecture**

Layers: Physical, Network, Controller, Application. Network layer contains?

A) Physical cables + devices
B) Underlay + overlay networks (OSPF + VXLAN + LISP)
C) DNA Center policies
D) User applications

**Réponse: B** - Network layer = underlay (physical routing) + overlay (tunneling)

### **Q34: LISP Map Server deployment**

10-site SD-Access campus. Map Server instances recommended?

A) Single (centralized database)
B) Two (primary + secondary HA)
C) One per site (distributed)
D) Based traffic volume (scaling variable)

**Réponse: B** - HA pair standard (redundancy, synchronization)

### **Q35: VXLAN MTU impact**

Standard Ethernet MTU 1500 bytes. VXLAN encapsulation overhead = 54 bytes. Safe payload?

A) 1500 (no change)
B) 1446 (1500 - 54)
C) 1554 (1500 + 54, jumbo frames)
D) 1280 (safety margin)

**Réponse: B** - Safe payload = 1500 - 54 = 1446 (avoid fragmentation)

### **Q36: TrustSec vs traditional ACLs**

Comparison key difference?

A) TrustSec = faster (no ACL processing)
B) TrustSec = identity-based (vs IP-based ACLs)
C) TrustSec = simpler configuration (vs complex ACL lists)
D) All [A] [B] [C]

**Réponse: D** - TrustSec superior multiple dimensions

### **Q37: ISE role SD-Access**

ISE primary function fabric?

A) Policy definitions (who, what, where, when)
B) Device profiling (identify endpoints)
C) Remediation (push patches endpoint)
D) All [A] [B] [C]

**Réponse: D** - ISE comprehensive identity + policy engine

### **Q38: Virtual Network (VN) isolation**

Multiple VNs (Corporate, Guest, IoT). Client roam between VNs possible?

A) Yes (same client, different VLAN per VN)
B) No (VN isolation = no cross-VN roaming)
C) Possible (with policy override, not typical)
D) Automatic (DHCP vlan assignment)

**Réponse: C** - VN isolation strict (manual policy change required cross-VN, not transparent roaming)

### **Q39: SD-Access scaling advantages**

Compared traditional 3-tier LAN, advantage?

A) Simpler architecture (fewer layers)
B) Higher VLAN count (4000+ VNs vs 200 VLANs)
C) Faster convergence (STP eliminated)
D) All [A] [B] [C]

**Réponse: D** - SD-Access modern, scalable

### **Q40: CoA (Change-of-Authorization) ISE**

Mid-session user context changes (department switch). ISE action?

A) Client must re-authenticate (disruption)
B) ISE sends CoA to fabric (policy update, zero downtime)
C) Manual admin intervention (scale constraint)
D) No action (old policy persists)

**Réponse: B** - CoA = dynamic policy update (vlan change, QoS adjust, seamless)

### **Q41: Fabric border function**

Catalyst 9300 border router deployment. Role?

A) Connect legacy switches (non-fabric nodes)
B) Internet gateway (WAN edge)
C) Data center link (border campus ↔ DC)
D) All [A] [B] [C]

**Réponse: D** - Border = integration legacy + external services

### **Q42: LISP mobile node roaming**

Client EID 10.1.1.50, AP1→AP2 roaming. ITR updated mapping ITR→ETR tunnel?

A) ITR queries Map Server (new RLOC discovery)
B) ITR uses cached mapping (stale, packets misdirected)
C) Fabric auto-updates ITR cache (proactive)
D) Client notifies ITR (client-pull model)

**Réponse: A** - ITR cache timeout → Map Server query → learn new RLOC

### **Q43: DNA Center assurance dashboard**

Real-time network health shows:
- Client latency spike (100ms → 500ms)
- AP CPU 85% (abnormal high)
- Roaming events 10/minute (excessive)

Root cause diagnosis?

A) Client device fault (software crash)
B) AP overload (capacity exceeded)
C) Wireless interference (spectrum crowding)
D) Multiple possible (AI/ML analysis needed)

**Réponse: D** - DNA Center anomaly detection (multiple hypotheses, investigate all)

### **Q44: Fabric split-MAC architecture**

Wireless client encryption. Tunnel endpoint?

A) Client → AP (local decryption)
B) Client → WLC (centralized decryption)
C) No tunnel (client → AP direct)
D) Depends deployment (variable)

**Réponse: B** - SD-Access WLC = tunnel endpoint (data plane encapsulation)

### **Q45: Multi-tier fabric campus**

HQ = large fabric (VXLAN+LISP), branch = simplified (traditional network). Inter-site?

A) Direct L2 extend (VXLAN across WAN, problematic)
B) WAN Gateway (fabric border router → traditional backbone)
C) SD-WAN overlay (separate transport)
D) Both [B] and [C]

**Réponse: B or D** - Fabric border + SD-WAN typical hybrid

### **Q46: SGT 0 vs SGT 65535 treatment**

SGT 0 = untagged, SGT 65535 = deny. Traffic without tag?

A) Accepted (untagged = implicit permit)
B) Default dropped (no SGT = no policy match)
C) Policy exception (depends SGACL default)
D) Forwarded unmodified (passthrough)

**Réponse: C** - SGACL default deny (no match = drop, unless explicit permit untagged)

### **Q47: Fabric scalability comparison**

Traditional 3-tier vs SD-Access:

A) 3-tier = unlimited (STP not bottleneck)
B) SD-Access = limited (overlay processing)
C) SD-Access = superior (VXLAN/LISP elegant)
D) Similar (both depend device count)

**Réponse: C** - SD-Access modern design (better scalability)

### **Q48: Encrypted traffic analytics (ETA)**

Client using HTTPS (TLS encrypted). DNA Center capability?

A) Decrypt payload (break encryption, privacy risk)
B) Behavior analysis (flow pattern, size distribution)
C) Binary passthrough (ignore encrypted content)
D) Force plaintext (man-in-the-middle)

**Réponse: B** - ETA = behavioral heuristics (no decryption needed)

### **Q49: ISE-DNA Center sync issues**

ISE SGT assignment delayed (5min lag). Impact?

A) Client gets old policy (temporary mismatch)
B) Client waits new policy (application blocked)
C) Network failure (cascading disruption)
D) Fallback policy (default-allow)

**Réponse: A** - ISE-DNA latency = transient policy mismatch (converges quick)

### **Q50: Fabric migration non-disruptive**

Add fabric overlay traditional campus. Downtime possible?

A) Yes (complete rebuild = disruptive)
B) No (fabric overlay transparent to L3)
C) Minimal (per-device onboarding, brief outage)
D) Depends (client migration strategy)

**Réponse: B or C** - Well-engineered = minimal disruption (phased onboarding)

---

## Module 24: Network Assurance (Q51-75)

### **Q51: Ping timeout adjustment**

Default ping timeout = 2 seconds. When increase?

A) Always (more generous)
B) Long-distance WAN (higher latency expected)
C) High-congestion network (temporary delays)
D) All [B] and [C]

**Réponse: D** - WAN/congestion → extend timeout

### **Q52: Extended ping DF bit usage**

DF bit set = 1500-byte test. Response "Fragmentation needed but DF set". Meaning?

A) Network supports full MTU (no issue)
B) Path MTU < 1500 (fragmentation required)
C) Sender MTU misconfigured (client side)
D) Random network glitch (transient)

**Réponse: B** - DF fail = MTU limit in path (adjust app payload)

### **Q53: Traceroute timeout pattern**

Traceroute output:
```
1  gw.local (192.168.1.1) 2ms
2  isp.net (203.0.113.1) 5ms
3  * * *  [timeout]
4  backbone.isp (198.51.100.1) 15ms
5  destination.com (93.184.216.34) 20ms
```

Hop 3 interpretation?

A) Unreachable (packet dropped)
B) Router not responding to ICMP TTL=3 (but path continues)
C) Path loss (end-to-end unreachable)
D) Routing loop (hop 3 sends back)

**Réponse: B** - Hop 3 silent (forwards packet, doesn't generate ICMP exceed)

### **Q54: OSPF adjacency MTU issue**

Debug shows:
```
OSPF: Rcv hello... OK
OSPF: 2 Way Communication... OK
OSPF: Database Descriptor... [ERROR] Mismatch MTU
```

Resolution?

A) Reboot routers (flush caches)
B) Check interface MTU both sides: `show ip interface [int]`
C) Adjust OSPF timers
D) Enable PMTUD (Path MTU Discovery)

**Réponse: B** - MTU mismatch diagnosis (interfaces must match)

### **Q55: OSPF network type significance**

Interface OSPF network type = "non-broadcast". Hello interval?

A) 10 seconds (broadcast default)
B) 30 seconds (non-broadcast default)
C) 60 seconds (enterprise mode)
D) Configurable (no default)

**Réponse: B** - Non-broadcast type = 30s hello, 120s dead

### **Q56: NetFlow export reliability**

NetFlow UDP export → collector. Packet loss during export?

A) Retransmission (UDP reliability)
B) Flow data loss (no guarantee, UDP best-effort)
C) Collector buffers (queue overflow tolerates loss)
D) Redundant export (dual collectors)

**Réponse: B** - NetFlow UDP = best-effort (loss possible, acceptable sampling bias)

### **Q57: SPAN local mirroring overhead**

Port mirroring enabled source → destination. Performance impact?

A) None (mirroring transparent)
B) ~5% bandwidth (copy traffic small overhead)
C) ~10-15% (switch ASIC load)
D) Depends traffic volume (variable)

**Réponse: D** - SPAN overhead scales traffic (high volume = significant impact)

### **Q58: ERSPAN decapsulation**

Analyzer receives ERSPAN encapsulated packets. Wireshark analysis?

A) Automatic decapsulation (Wireshark built-in)
B) Manual decapsulation (GRE unpack needed)
C) Plain payload (GRE transparent)
D) Separate capture (ERSPAN separate format)

**Réponse: A** - Wireshark ERSPAN dissector (auto-decode)

### **Q59: IP SLA threshold tuning**

IP SLA ICMPecho probe: RTT normally 10ms, spike 50ms detected. Threshold setting?

A) 20ms (tight = many false alerts)
B) 50ms (match observed spike)
C) 100ms (loose = miss real issues)
D) Network dependent (custom tuning per environment)

**Réponse: D** - Threshold tuning art + science (baselines + business requirement balance)

### **Q60: IP SLA failover automation**

IP SLA detects destination unreachable. Automatic failover?

A) No (manual intervention)
B) Yes (if failover policy configured)
C) Optional (depends application)
D) Device-specific (varies router model)

**Réponse: B** - IP SLA ACL + static route manipulation (policy-driven failover)

### **Q61: DNA Center telemetry collection**

Default telemetry push interval = ?

A) 5 seconds (real-time)
B) 30-60 seconds (near real-time + dashboard update lag)
C) 5 minutes (batch collection)
D) Event-driven (no fixed interval)

**Réponse: B** - DNA Center ~30-60s typical (balance real-time vs processing load)

### **Q62: DNA Center ML anomaly detection**

Baseline period = 1 week (learning phase). Alert on spike = +300% latency. Timing?

A) Week 2 (data available model training)
B) Week 1 (immediate upon baseline)
C) After 2 weeks (statistical significance)
D) Dashboard only (no alerts early)

**Réponse: A** - ML requires baseline (convergence ~1 week + testing)

### **Q63: Encrypted traffic visibility DNA Center**

Corporate uses Office365 (TLS encrypted). DNA Center sees?

A) Nothing (encryption opaque)
B) Packet rates, flow counts (behavioral signals)
C) User identity (if integrated AD)
D) Both [B] and [C]

**Réponse: D** - Behavioral analytics + identity integration possible

### **Q64: NetFlow bi-directional flows**

Client→Server HTTP (10packets, 5KB), Server→Client response (15 packets, 100KB). NetFlow tracking?

A) Single flow (aggregate both directions)
B) Dual flows (separate A→B, B→A)
C) depends version (v5 = single, v9 = dual)
D) Depends collector (post-processing)

**Réponse: C** - NetFlow v5 = aggregate, v9/IPFIX = directional flexibility

### **Q65: SPAN multicast traffic**

SPAN mirroring source = VLAN containing multicast app (streaming video). Mirrored traffic volume?

A) Single copy (no multicast duplication)
B) Multicast received frames all copied (volume spike)
C) Depends (source selection type)
D) Filtered (analyzer requested RTP only)

**Réponse: B** - Multicast = all received copies mirrored (bandwidth heavy)

### **Q66: IP SLA jitter measurement**

VoIP quality monitoring. Jitter measurement requires?

A) Single icmp-echo (simple latency)
B) UDP stream (variable packet spacing = jitter)
C) TCP connection (reliability)
D) DNS query (application availability)

**Réponse: B** - Jitter = inter-packet delay variance (IP SLA UDP jitter operation)

### **Q67: Debugging enable impact performance**

`debug ip ospf adj` enabled production network. Impact?

A) No impact (background, negligible CPU)
B) Minor (~2-3% CPU overhead)
C) Significant (CPU spike, console output blocking)
D) Depends interface count (scales)

**Réponse: D** - Debug heavy task (typically disable production, enable troubleshooting only)

### **Q68: Syslog centralization assurance**

WLC configured syslog server 10.50.50.50:514 UDP. Single server only. Risk?

A) No risk (UDP connectionless)
B) Risk = server down = lost logs (no alerting)
C) Acceptable (log loss temporary, non-critical)
D) Recommend redundancy (dual syslog servers)

**Réponse: D** - Syslog HA pair standard (critical data)

### **Q69: SNMP v3 vs v2c assurance**

Comparison security?

A) v2c = encrypted (more secure)
B) v3 = encrypted + authentication (stronger)
C) v2c adequate (simplicity > security)
D) Same security (version doesn't matter)

**Réponse: B** - SNMP v3 = AES encryption + MD5/SHA auth (superior v2c plain-text)

### **Q70: Packet loss measurement ICMP**

Ping loss 5% (96 packets sent, 5 lost). Assessment?

A) Excellent (no concern)
B) Acceptable (< 1% CRitic, 1-5% warning)
C) Poor (> 5% indicates issue)
D) Variable (application-dependent)

**Réponse: D** - Loss tolerance: VoIP <1%, video <3%, file 0-5% acceptable

### **Q71: RTT (Round-Trip Time) variability**

Ping results: min=1ms, avg=5ms, max=20ms. Interpretation?

A) Excellent (tight, consistent)
B) Good (max 4× average)
C) Fair (variability acceptable)
D) Poor (jitter = QoS issue)

**Réponse: C** - Variability acceptable (background traffic causes variance)

### **Q72: Traceroute multipath visualization**

GigabitEthernet load-balanced 2 equal paths. Traceroute output?

A) Single path (deterministic, one displayed)
B) Multipath (can vary per packet, ECMP shown)
C) Depends IP (Windows = single, Linux = multiple)
D) Not traceroute capable (tool limitation)

**Réponse: B** - Modern traceroute Paris-traceroute (multipath capable)

### **Q73: NetFlow sampling ratio**

1-in-10 sampling (10% flows captured). Accuracy implication?

A) Perfect (10% × 10 = 100% estimate)
B) Biased (sampling errors possible)
C) Acceptable ( Internet 1-in-100 typical)
D) Depends collector (post-extrapolation)

**Réponse: C** - Sampling always introduces bias (balance accuracy vs load)

### **Q74: DNA Center predictive alerting**

Dashboard alert: "Storage device will fill in 7 days." Action timing?

A) Immediate (urgent action)
B) Week-end (plan weekend action)
C) Monitor (schedule maintenance)
D) Ignore (predictive false positives)

**Réponse: C** - Predictive alert = planning opportunity (not critical until closer)

### **Q75: Assurance ROI (Return on Investment)**

Why enterprise monitor network extensively (DNA Center, NetFlow, SPAN)?

A) Compliance requirement (audit trail needed)
B) Performance optimization (reduce troubleshooting MTTR)
C) Proactive risk detection (prevent issues before users notice)
D) All [A] [B] [C]

**Réponse: D** - Modern assurance = business value (compliance + performance + resilience)

---

## Rubric & Scoring

**Total: 75 questions** | **Target: 60+ (80%)** | **Passing: 52 (70%)**

**Breakdown by module:**
- Module 22: Q1-25 (25 points) - Enterprise architecture
- Module 23: Q26-50 (25 points) - Fabric technologies
- Module 24: Q51-75 (25 points) - Network assurance

**Score interpretation:**
- 70-79% (52-59): Passing, some gaps
- 80-89% (60-66): Strong understanding
- 90-100% (67-75): Mastery, exam ready
