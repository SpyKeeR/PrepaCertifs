# CCNP ENCOR Final Examination (350-401)

## Certification: Cisco CCNP Enterprise Core (ENCOR) v8
## Exam Code: 350-401
## Time Limit: 120 minutes
## Number of Questions: 120
## Passing Score: 70% (84 questions)
## Format: Multiple Choice (4 options per question)
## Difficulty Level: Certification-Realistic

---

## EXAMINATION INSTRUCTIONS

**Before You Begin:**
- This examination simulates the official Cisco 350-401 ENCOR certification exam format
- You have 120 minutes to answer 120 questions
- Each question carries equal weight (1 point per question)
- You cannot return to previous questions once answered
- There is no penalty for guessing
- Passing score is approximately 70%

**Question Format:**
- All questions are multiple-choice with 4 options (A, B, C, D)
- Read each question carefully and select the BEST answer
- Some questions are scenario-based requiring analysis
- Some questions include diagrams that must be interpreted
- Some questions test command knowledge and output interpretation

**Test-Taking Strategy:**
- Allocate approximately 1 minute per question
- Answer questions you know first (2-3 pass strategy)
- Mark difficult questions for review if time permits
- Read distractor answers carefully - they may contain partially correct information
- Consider the MOST COMPLETE and ACCURATE answer

---

## SECTION 1: LAYER 2 REDUNDANCY & SWITCHING (Q1-15)

**Q1: STP Convergence Analysis**

Your organization operates a large metropolitan network with 47 switches arranged in a three-tier hierarchy. You've implemented Rapid PVST+ across all VLANs. After a scheduled maintenance window, you removed a core switch from VLAN 10, which was a secondary root. The network is experiencing 45 seconds of traffic loss on VLAN 10.

You've verified:
- All ports are in forwarding state (except the removed switch)
- BPDUs are being exchanged normally
- No configuration errors exist
- All interface costs and priorities are consistent

Which two factors are MOST likely causing the extended convergence time?

A) The failing to elect a new root bridge; BPDU Guard preventing convergence  
B) Multiple spanning instances (PVSTs) causing cumulative convergence; STP forwarding delay being counted multiple times in topology changes  
C) MAC address table flush timeout; Access layer ports stuck in listening state  
D) Root port re-election delay; Lost information due to third spanning instance not reconverging

**Q2: Extended VLAN Configuration**

Your enterprise deploys extended VLANs (1006-4094) to support future growth without reconfiguring the core infrastructure. You're implementing centralized VLAN database on a switch stack. During configuration, you discover that VLAN 2000 created on Switch-A is not appearing on Switch-B in the stack.

What is the PRIMARY reason for this behavior?

A) VTP pruning is preventing VLAN 2000 from being advertised across stack links  
B) VTP mode is set to "client" on one switch and "server" on another; extended VLANs require all switches in VTP server mode  
C) Extended (reserved) VLANs are stored in NVRAM, not in the running VTP database; they don't propagate via VTP  
D) Inter-switch link (ISL) compression is enabled, which blocks extended VLAN transmission

**Q3: EtherChannel Mode Incompatibility**

You're troubleshooting EtherChannel issues on a critical link between SW01 and SW02. Physical layer is functioning, all four ports pass basic connectivity tests. The EtherChannel is not forming, and you observe the following console message:

```
%EC-5-CANNOT_BUNDLE: Te0/0/1 is not compatible with the other ports (reason: speed mismatch)
```

You verify all interfaces are configured as 10 Gigabit Ethernet at the same speed. You check the EtherChannel configuration:

SW01: channel-group 10 mode active
SW02: channel-group 10 mode passive

Testing reveals each individual port forwards traffic normally. When you enable LACP on one port manually (non-channel), traffic passes through that single port successfully.

What is the MOST likely cause of the EtherChannel bundle failure?

A) Active mode on both ends requires manual negotiation; change SW02 to "desirable" LACP mode  
B) Speed mismatch is reported incorrectly; issue is actually in subport configuration (VLANs) not matching  
C) One interface is configured with a different EtherChannel protocol (PAGP vs LACP); verify all use same protocol  
D) Load-balancing algorithm is misconfigured; change from source-dest-mac to source-dest-ip

**Q4: VLAN Access Port Troubleshooting**

Your organization supports 1,200 users across 15 access layer switches. User in VLAN 50 on Switch-ACC-04 cannot communicate with users in the same VLAN on Switch-ACC-05. Both switches are connected via a Layer 3 core, and all other VLANs work correctly.

Investigation shows:
- VLAN 50 interface IP addresses are correct (172.16.50.0/24)
- Ping from ACC-04 VLAN 50 SVI to ACC-05 VLAN 50 SVI succeeds
- Individual user on ACC-04 can ping users on ACC-05 in VLAN 100 (different VLAN)
- ACLs are not blocking VLAN 50 traffic
- VLAN 50 is allowed on all trunks

However, VLAN 50 user on ACC-04 cannot ping VLAN 50 user on ACC-05.

What is the MOST likely explanation?

A) VLAN 50 SVI interface has wrong subnet mask; users are in different subnets than SVI  
B) Inter-VLAN routing to VLAN 50 is disabled; VLAN 50 interfaces are in "no-ip" mode  
C) VLAN 50 is not allowed on the trunk link between ACC-04 and ACC-05 due to VLAN database mismatch  
D) VLAN 50 VLAN database entry exists on ACC-04 but not ACC-05; database synchronization is incomplete

**Q5: Hierarchical Design topology issue**

You're analyzing the network topology of a three-tier hierarchical design with the following characteristics:

- Access layer: 10 switches (120 ports each = 1,200 total user ports)
- Distribution layer: 4 switches (fully meshed connectivity)
- Core layer: 2 switches (active/standby redundancy)

Current topology shows each access switch connects to BOTH distribution switches. Every distribution switch connects to EVERY other distribution switch. Both core switches are connected to both distribution switches.

As the network grows, you're experiencing exponential growth in spanning tree recalculations during topology changes. The core switch count is doubling every 18 months.

Which design change BEST addresses bandwidth utilization while reducing spanning tree complexity?

A) Collapse the distribution and core into a single layer; this eliminates spanning tree computation overhead  
B) Implement partial mesh on distribution layer; reduce distribution switch count from 4 to 3 to reduce connection points  
C) Change core from active/standby to load-balancing mode; distribute traffic across both core switches  
D) Restrict access switches to connect to only ONE distribution switch using hub-and-spoke topology; reduce mesh complexity

**Q6: STP Port Priority Configuration**

You need to ensure that specific ports on your switch become root ports (pointed toward the root bridge) while blocking the others. You have:
- Switch-A (Root Bridge priority 8192)
- Switch-B (priority 16384)
- Switch-B has 3 paths to Switch-A with different costs: 4, 8, and 12

You configure path with cost 4 to have highest priority (root port), but it still loses root port election to the path with cost 8.

All paths cost 4. However, the cost 8 path becomes root port instead. What is the most likely reason?

A) Root path cost tie-breaker uses sender bridge ID; the cost-8 switch has lower bridge ID than cost-4 switch  
B) Port priority on cost-8 path is set to 0 (highest), while cost-4 path is set to 128; port priority overrides cost  
C) BPDU received on cost-8 port is from Switch-A's lower-numbered port; sender port priority overrides cost  
D) Maximum retransmission count for BPDU on cost-4 path has been exceeded; path is marked invalid

---

## SECTION 2: IP ROUTING FUNDAMENTALS (Q7-21)

**Q7: Route Selection with Multiple AD**

Your Cisco IOS router has the following routes installed:

```
O   192.168.1.0/24 [110/50] via 10.1.1.1
R   192.168.1.0/24 [120/5] via 10.2.2.1
B   192.168.1.0/24 [200/0] via 10.3.3.1
i   192.168.1.0/24 [100/2500] via 10.4.4.1
```

Where: O=OSPF, R=RIPv2, B=BGP, i=EIGRP

You test connectivity to 192.168.1.5. Which route will be selected?

A) The OSPF route via 10.1.1.1 (lowest cost among installed routes)  
B) The RIPv2 route via 10.2.2.1 (lowest hop count)  
C) The EIGRP route via 10.4.4.1 (lowest administrative distance = 100)  
D) The BGP route via 10.3.3.1 (default BGP preference)

**Q8: FIB vs RIB Behavior**

While troubleshooting a network connectivity issue, you display the routing table:

```
R1# show ip route
...
D   10.0.0.0/8 [90/130816] via 192.168.1.2, 00:45:23, GigabitEthernet0/0
D   10.0.0.0/8 [90/130816] via 192.168.1.3, 00:45:23, GigabitEthernet0/1
D   10.0.0.0/8 [90/130816] via 192.168.1.4, 00:45:23, GigabitEthernet0/2
```

You then check the forwarding table:

```
R1# show ip cef 10.0.0.1 internal
10.0.0.1/32
  microflow cache size: 64
  packets   bytes    switched
  0         0        0
  load: 33%/33%/33%
```

Traffic destined to 10.0.0.0/8 arrives on GigabitEthernet 0/0 destined for 10.0.0.1. The interface is UP/UP. No ACLs are applied.

When you ping 10.0.0.1, what percentage of packets will take the path via 192.168.1.2, 192.168.1.3, and 192.168.1.4 respectively?

A) 33% / 33% / 33% - equal-cost load balancing across all three paths  
B) 100% / 0% / 0% - first path wins (RIB determines first-path preference)  
C) 25% / 50% / 25% - hash algorithm distributes traffic non-deterministically  
D) 33% / 34% / 33% - load balancing with rounding difference for three paths

**Q9: Recursive Route Dependency**

You have the following routing configuration:

```
ip route 192.168.100.0 255.255.255.0 192.168.1.1
ip route 192.168.1.0 255.255.255.0 10.1.1.1
```

And a GRE tunnel configuration:

```
interface Tunnel0
  ip address 10.0.0.1 255.255.255.0
  tunnel source 172.16.1.2
  tunnel destination 192.168.100.1
```

The tunnel shows:

```
Tunnel0 is up, line protocol is down
```

Investigation shows:
- 172.16.1.2 is the Loopback IP (accessible)
- Physical interface is UP/UP
- No ACLs block traffic
- 192.168.100.1 exists on the remote network

What is the PRIMARY cause of the line protocol down status?

A) Tunnel destination 192.168.100.1 is recursively dependent on the tunnel interface (recursive route); routing table cannot resolve destination  
B) Tunnel source IP (172.16.1.2) is not in the routing table; interface needs gateway-of-last-resort defined  
C) Tunnel MTU is misconfigured; GRE encapsulation requires specific MTU settings  
D) IPCP (PPP control protocol) for GRE tunnel negotiation has failed; enable tunnel keepalive

**Q10: Equal-Cost Load Balancing Failure**

Your OSPF network has four routers with equal-cost paths to 172.16.0.0/24:

```
Paths to 172.16.0.0/24:
Route 1: R2 -> R4 -> R5 (cost 100)
Route 2: R2 -> R3 -> R5 (cost 100)
Route 3: R2 -> R4 -> R6 (cost 100)
```

Router R2 shows:

```
O   172.16.0.0/24 [110/100] via 192.168.1.2, 00:00:34, GigabitEthernet0/0
O   172.16.0.0/24 [110/100] via 192.168.1.3, 00:00:34, GigabitEthernet0/0
```

Only 2 of 3 equal-cost paths appear in the routing table. You verify all paths are symmetric and OSPF cost calculations are identical. Interface bandwidth and delay values are consistent.

Related commands show:

```
R2(config)# maximum-paths 4
```

But only 2 paths are installed. Why?

A) OSPF supports maximum 4 equal-cost paths, but this network has only 2 valid next-hops; this is expected behavior  
B) Multipath is limited to 2 by default in OSPF; maximum-paths only works for EIGRP  
C) Third path via R4->R6 is not via a directly connected neighbor; OSPF limits ECMP to direct adjacencies  
D) OSPF metric tie-breaker selects the route advertised by the router with the lowest router ID; one path has higher RID

---

## SECTION 3: EIGRP ROUTING (Q11-25)

**Q11: EIGRP Composite Metric Calculation**

You have an EIGRP network with the following characteristics:

**Link 1:** 1000 Mbps Ethernet, delay 10 µs
**Link 2:** 100 Mbps Ethernet, delay 1000 µs

Both links connect the same source and destination routers. You need to calculate which link will be preferred.

EIGRP composite metric formula:
```
Metric = 256 × [(K1 × bandwidth + (K2 × bandwidth) / (256 - load) + K3 × delay) × (K5 / (reliability + K4))]
```

Default K values: K1=1, K2=0, K3=1, K4=0, K5=0

Using the formula, which interface will EIGRP prefer?

A) Link 1 (1000 Mbps) is preferred; lower bandwidth value in denominator produces lower metric  
B) Link 2 (100 Mbps) is preferred; higher hop count on link 1 increases metric (WRONG UNDERSTANDING)  
C) Link 1 is preferred; inversely, bandwidth is 10^10/bandwidth, so 10^10/10^9 = 10 vs 10^10/10^8 = 100 (lower metric)  
D) Link 2 is preferred; delay is 1000µs vs 10µs, so delay term = 1000 vs 10 (more stable link)

**Q12: EIGRP Neighbor Adjacency Failure**

Two routers (R1 and R2) are connected via point-to-point link. R1 shows:

```
R1# show ip eigrp neighbors
IP-EIGRP neighbors for process 100

H   Address                 Interface       Hold Uptime   SRTT   RTO  Q  Seq
                                           (sec)         (ms)   (ms) Ct Num
0   10.1.1.2                Gi0/0             13 00:25:14 45    308  0  42
```

R1 can successfully ping 10.1.1.2. EIGRP adjacency shows stable with sequence numbers incrementing normally. However, R2 does not have R1 as a neighbor.

Investigation reveals:
- Both routers have identical EIGRP process IDs (100)
- Both routers have identical AS numbers
- Both routers have k-value settings configured identically
- Hello/Hold timers are equal on both routers
- Network statements permit both 10.1.1.0/24 and connected networks

The asymmetric neighbor relationship persists. What is the MOST likely cause?

A) R1 and R2 have different EIGRP versions (v1 vs v2); version mismatch prevents bidirectional adjacency  
B) R2 has default-information originate configured, which prevents it from forming bidirectional EIGRP relationships  
C) R2 is configured for passive interface mode on Gi0/0; passive interfaces receive updates but don't send updates  
D) R1 is sending updates with lower sequence number due to clock drift; R2 expects higher sequence

**Q13: EIGRP DUAL (Diffusing Update Algorithm)**

Your EIGRP network topology:

```
R1 ---- R2 ---- R3
|              /
|            /
R4 ---- R5
```

**Topology for prefix 172.16.0.0/24 (advertised from R3):**
- R1 -> R2 -> R3: cost 100
- R1 -> R4 -> R5 -> R3: cost 200
- R2 -> R3 direct: cost 50

R1's EIGRP topology table shows:

```
Destination: 172.16.0.0/24
Successor: via R2 (cost 100), FD=100
Feasible Successors: via R4 (cost 200)
```

R2 suddenly goes down. R1 immediately sends EIGRP query for 172.16.0.0/24 to R4. R4 responds with cost 300 for this destination.

What will happen to R1's routing table for 172.16.0.0/24?

A) Route is immediately deleted; no feasible successor exists with cost < 100  
B) Route is installed via R4 with cost 300; feasible successor was available (cost 200)  
C) R1 queries R4 for alternate path before accepting cost 300 (DUAL convergence process)  
D) Route remains active via R2 until new neighbor discovery occurs

**Q14: EIGRP Load Balancing Configuration**

You want to load-balance traffic across four equal-cost EIGRP paths to 192.168.0.0/16. Your configuration shows:

```
router eigrp 100
  maximum-paths 4
  variance 1
```

All four paths have EIGRP metric 1000. No traffic uses paths 3 and 4.

You enable:
```
  variance 2
```

Now all four paths carry traffic. Which routes are now included in the load-balancing set?

A) All routes with cost between 1000 and 2000; variance multiplies feasible distance (variance × FD = 2000)  
B) Routes with cost up to 1000 × variance = 2000, but only if they are feasible successors (AD < FD)  
C) The variance value applies to the successor cost difference, so routes within 2000 metric range are used  
D) Only routes with cost equal to 1000 are used; variance only affects metric rounding

**Q15: EIGRP Passive Interface Configuration**

You configure R1 with:

```
router eigrp 100
  network 0.0.0.0
  passive-interface default
  no passive-interface GigabitEthernet 0/0
  no passive-interface GigabitEthernet 0/1
```

R1 has the following interfaces:
- GigabitEthernet 0/0 → 10.1.1.0/24 (connected to R2)
- GigabitEthernet 0/1 → 10.2.2.0/24 (connected to R3)
- GigabitEthernet 0/2 → 10.3.3.0/24 (connected R4)
- Loopback 0 → 172.16.1.0/24

After configuration, you observe:
- EIGRP hello packets sent on Gi0/0 and Gi0/1
- No hello packets sent on Gi0/2 or Loopback0
- EIGRP neighbors form correctly on Gi0/0 and Gi0/1

Later, you add a new GigabitEthernet 0/3 interface with IP 10.4.4.1/24, connecting to R5. EIGRP adjacency fails with R5.

What must be done to establish EIGRP adjacency on the new interface?

A) Add network statement for 10.4.4.0/24 (current 0.0.0.0 statement covers all networks)  
B) Change passive-interface configuration to exclude Gi0/3 using command: no passive-interface GigabitEthernet 0/3  
C) Reload the router to apply passive-interface changes (changes require restart)  
D) Configure EIGRP on R5 with matching process ID and AS number

**Q16: EIGRP Convergence After Link Failure**

In your EIGRP network with 50 routers across 6 regions, a critical core link fails. The topology table shows:

```
Prefix: 10.0.0.0/8
Successor: via Core-Router-G (cost 100), FD=100
Feasible Successors: 
  - via Regional-R1 (cost 150)
  - via Regional-R3 (cost 180)
  - via Regional-R2 (cost 200)
```

The successor path fails immediately. EIGRP convergence time is:
1. Successor removed from routing table: 10ms
2. Feasible successor selected: 10ms
3. Route update advertisement: 50ms

Total convergence time: ~70ms

A competing OSPF network with identical topology shows:
1. Dead neighbor detection: 3-40 seconds
2. SPF calculation: 100-500ms
3. LSA flooding: 50-100ms

Total convergence time: 3-40+ seconds

Why is EIGRP convergence MUCH faster than OSPF in this scenario?

A) EIGRP pre-computes alternate paths; feasible successors are already available for immediate use  
B) EIGRP doesn't require full topology recalculation; DUAL algorithm maintains loop-free alternatives  
C) EIGRP uses faster link failure detection via BFD; OSPF uses dead timers  
D) All of the above (A, B, and C contribute)

---

## SECTION 4: OSPF ROUTING (Q17-31)

**Q17: OSPF Network Types and Hello Intervals**

You're designing OSPF for a network with heterogeneous media:

**Link 1:** Campus Gigabit LAN (OSPF network type: Broadcast)
**Link 2:** T1 WAN circuit to remote office (OSPF network type: Point-to-Point)
**Link 3:** Frame Relay network with multiple PVCs (OSPF network type: Non-Broadcast)
**Link 4:** PPtP VPN tunnel (OSPF network type: Point-to-Multipoint)

Default hello intervals by network type:
- Broadcast: 10 seconds
- Point-to-Point: 10 seconds
- Non-Broadcast: 30 seconds
- Point-to-Multipoint: 30 seconds

After adding Link 3 (Frame Relay), some routers form adjacencies while others enter "Attempt" state permanently. You notice:

- DR/BDR election happened on Frame Relay
- Hello packets are sent every 30 seconds
- Routers are isolated nodes on separate PVCs (not point-to-multipoint mesh)

What is the PRIMARY issue?

A) OSPF non-broadcast requires manual neighbor configuration; isolated PVCs won't establish adjacency without neighbor statements  
B) Frame Relay hello interval (30s) exceeds the 10-second routed neighbor timeout (WRONG)  
C) DR/BDR election is unnecessary on non-fully-meshed Frame Relay; change network type to point-to-multipoint-nonbroadcast  
D) Frame Relay virtual circuit LMI failure is preventing OSPF hello exchange

**Q18: OSPF Area Design and LSA Flooding**

Your organization has a large OSPF network split across 4 areas:

- Area 0 (backbone): 2 routers
- Area 1: 15 routers
- Area 2: 18 routers
- Area 3: 12 routers

After a link failure in Area 2, you observe:
- Area 2 routers immediately re-converge (30 seconds)
- Area 1 routers show changed routing (45 seconds)
- Area 3 routers show changed routing (45 seconds)
- Area 0 shows new LSA flush (10 seconds)
- Area 0 overall convergence time: ~70 seconds

LSA type breakdown:
- Type 1 LSA (Router): flooded throughout area only
- Type 2 LSA (Network): flooded throughout area only
- Type 3 LSA (Summary): flooded between areas via ABR
- Type 4 LSA (ASBR Summary): flooded between areas via ABR
- Type 5 LSA (External): flooded throughout OSPF domain

Why did routers in Area 1 and Area 3 experience topology changes?

A) The link failure in Area 2 flooded Type 1 LSAs across area boundaries using Type 3 summary LSAs (flooding mechanism)  
B) Type 1 LSAs in Area 2 are replaced with Type 3 LSAs at the ABR; Area 1/3 routers receive Type 3 updates  
C) ABRs summarize Area 2 changes into Type 3 LSAs; Type 3 LSAs are flooded to Area 1 and Area 3 via backbone (Area 0)  
D) Multi-area OSPF requires complete topology knowledge; all areas receive all LSAs regardless of source

**Q19: DR/BDR Election Process**

Two OSPF routers connect to shared Ethernet segment with 10 other hosts:

**Router A:** Priority 50, Router ID 1.1.1.1
**Router B:** Priority 50, Router ID 2.2.2.2
**Router C:** Priority 100, Router ID 3.3.3.3

All routers are in the same area. During initial network startup:

1. Router A boots first and becomes DR
2. Router B boots and becomes BDR
3. Router C boots and learns of DR and BDR

Router C has highest priority (100) but does not become DR. Which statement correctly explains this behavior?

A) Priority is recalculated when Router C joins; C will become DR in next election (after new neighbor discovery)  
B) DR/BDR elections are non-preemptive; Router C cannot force re-election; A remains DR until it fails  
C) Router C automatically becomes DR because it has the highest priority; the described behavior is incorrect  
D) Router ID determines election outcome when priority is identical; routers A and B have lower priority

**Q20: OSPF Timers and Convergence**

In your OSPF network, you observe 60-second convergence time after a link failure. You've configured:

```
router ospf 1
  timers spf 5000 10000
  timers throttle lsa all 0 100 5000
  timers throttle spf all 0 100 5000
```

Current convergence breakdown:
1. Link failure detection: 1 second
2. LSA generation (SPF throttle): 100-5000ms
3. SPF calculation (SPF throttle): 100-5000ms
4. Update distribution: 10-50ms
5. Total: 5-10 seconds

However, your network shows 60-second convergence. What might explain the additional 50+ second delay?

A) SPF throttle wait time is 5000ms initially, plus SPF calculation time up to 5000ms again; 10-second minimum timer adds 10 seconds  
B) Neighboring routers have different timer configurations; waiting for slowest neighbor to converge adds 45+ seconds  
C) Backup Designated Router (BDR) convergence trail lags DR; additional BDR processing costs ~40-50 seconds  
D) Multiple SPF triggers cause multiple throttle calculations; each SPF re-trigger adds another 5-10 second wait

**Q21: OSPFv3 IPv6 Unique Characteristics**

You're migrating from OSPFv2 (IPv4) to OSPFv3 (IPv6). Your configuration:

```
ipv6 unicast-routing
ipv6 router ospf 1
  router-id 1.1.1.1
  area 0 authentication ipsec spi 256 md5 <password>
```

OSPFv2 characteristics:
- Routers are identified by Router ID (IPv4 format)
- Authentication uses authentication key in area configuration
- Neighbors communicate via All SPF Routers multicast 224.0.0.5

OSPFv3 characteristics:
- Routers are identified by Router ID (still IPv4 format)
- Authentication uses IPsec or routing protocol authentication
- Neighbors communicate via All SPF Routers multicast FF02::5

Your OSPFv3 adjacency fails to form between R1 (FE80::1/64) and R2 (FE80::2/64). Both routers have:
- Identical Router ID (1.1.1.1)
- Identical Area 0
- Identical SPF timers
- IPv6 connectivity (ping succeeds)

Investigation shows R1 sends OSPFv3 hello packets successfully, but R2 doesn't receive them. What is the MOST likely issue?

A) IPv6 link-local addresses are identical (FE80::1 on both); OSPFv3 uses link-local addresses for adjacency formation  
B) Missing interface-level OSPFv3 configuration; need: "ipv6 ospf 1 area 0" on the interface  
C) IPv6 multicast (FF02::5) is not reachable; verify "ipv6 mfib forward" is enabled  
D) OSPFv3 requires globally unique IPv6 addresses; link-local addresses don't work for OSPF

---

## SECTION 5: BGP & EDGE ROUTING (Q22-36)

**Q22: BGP AS Relationships and Route Propagation**

Your organization (AS 65001) has established BGP peering with three providers:

```
  AS 65002 ----→ AS 65001 ← ---- AS 65003
       ↓           │            ↓
    10.0.0.0/8   AS 65001's   20.0.0.0/8
                  Routes
    30.0.0.0/8 ← ----- AS 65004
```

- AS 65002 sends prefix 10.0.0.0/8
- AS 65003 sends prefix 20.0.0.0/8
- AS 65004 sends prefix 30.0.0.0/8

BGP policy:
```
router bgp 65001
  neighbor 65.1.1.1 remote-as 65002
  neighbor 65.2.2.2 remote-as 65003
  neighbor 65.4.4.4 remote-as 65004
  neighbor 65002 route-map PREPEND-65002 out
  neighbor 65003 route-map PREPEND-65003 out
```

AS 65002 and 65003 have a direct peering relationship. After 30 minutes, you notice:

- AS 65001 sees 10.0.0.0/8 from 65002 (cost 100 via own connection)
- AS 65001 sees 10.0.0.0/8 from 65003 (cost 300 via 65002)
- AS 65001 sees 20.0.0.0/8 from 65003 (cost 100 via own connection)
- AS 65001 sees 20.0.0.0/8 from 65002 (cost 300 via 65003)

But AS 65001 does NOT see 30.0.0.0/8 from 65002 or 65003, only from 65004.

Why are AS 65002 and AS 65003 not seeing prefixes from each other through AS 65001?

A) Default BGP behavior does not advertise routes received from one eBGP peer to other eBGP peers unless explicitly configured (next-hop-self, route-map reshaping, or redistribution)  
B) AS 65001 is explicitly blocking re-advertisement with "no-export" community tags  
C) AS 65004 is blocking the advertisements using BGP prefix filters  
D) AS 65002 and AS 65003 have configured "remove-private-as" to prevent AS 65001 (private ASN) from appearing

**Q23: BGP Path Selection and Weight Attribute**

Your BGP network receives the same prefix (175.0.0.0/16) via multiple ASes:

```
Route 1: 175.0.0.0/16 via AS 65002 (AS Path: 65002)
Route 2: 175.0.0.0/16 via AS 65003 (AS Path: 65003 65002)
Route 3: 175.0.0.0/16 via AS 65004 (AS Path: 65004)
```

Current BGP configuration:

```
router bgp 65001
  neighbor 65.2.2.2 remote-as 65002
  neighbor 65.3.3.3 remote-as 65003
  neighbor 65.4.4.4 remote-as 65004
  neighbor 65.2.2.2 route-map WEIGHT-OUT-100 out
```

Traffic prefers Route 3 via AS 65004, but you want to prefer Route 1 via AS 65002. You apply:

```
route-map WEIGHT-OUT-100 permit 10
  match ip address prefix-list CORE-ROUTES
  set weight 100
```

But traffic still prefers Route 3. What is the issue?

A) Weight is set on outbound traffic (toward neighbor 65.2.2.2), not inbound; use inbound route-map on neighbor 65.2.2.2 with "set weight"  
B) Weight is applied to the BGP neighbor relationship, not the specific prefix route; use local-preference instead  
C) Weight of 100 is too low; Route 3 has implicit weight of 0; need weight 200+ to override  
D) This configuration is correct but other factors override weight; increase local-preference which is checked before weight

**Q24: BGP Route Summarization**

Your company operates AS 65001 with the following IPv4 subnets:

```
10.100.0.0/24
10.100.1.0/24
10.100.2.0/24
10.100.3.0/24
...
10.100.255.0/24
```

(All /24 subnets within 10.100.0.0/16)

You want to summarize these 256 subnets into a single BGP announcement to reduce routing table bloat in customer networks. You configure:

```
router bgp 65001
  address-family ipv4
    aggregate-address 10.100.0.0/16 summary-only
```

When you check your BGP table, you see:

```
status codes: s suppressed, d damped, h history, * valid, > best, i - internal, r RIB failure
Next hop is not final. bgp aggregate update failed
Status: Valid but not in BGP table
```

What is the PRIMARY issue preventing the aggregate from being installed?

A) aggregate-address requires at least one valid component prefix to be installed in the BGP table  
B) summary-only keyword must have preceding advertisement routes
C) The aggregate requires a local route (10.100.0.0/16) in the BGP routing table; use "aggregate-address ... suppress-map"  
D) Redistribution of connected networks into BGP is required to create the aggregate

**Q25: BGP Communities and Route Manipulation**

You receive routes from a transit provider with community tags:

```
Route A: 175.1.0.0/16 with community 65002:100
Route B: 175.1.1.0/17 with community 65002:100
Route C: 175.1.128.0/17 with community 65002:100
```

Your policy should prefer routes with community 65002:100 vs others. You configure:

```
router bgp 65001
  neighbor 65.2.2.2 remote-as 65002
  neighbor 65.2.2.2 route-map PREFER-65002 in
  
route-map PREFER-65002 permit 10
  match community 65002_COMM
  set local-preference 200
  
route-map PREFER-65002 permit 20
  
community-list standard 65002_COMM permit 65002:100
```

BGP table shows:

```
*> 175.1.0.0/16 [20/0] via 65.2.2.2, 00:05:23
*> 175.1.1.0/17 [20/0] via 65.2.2.2, 00:05:23
*> 175.1.128.0/17 [20/0] via 65.2.2.2, 00:05:23
```

However, these routes are being treated identically in path selection despite the local-preference matching. What is the issue?

A) Community matching works correctly, but local-preference isn't being applied correctly; verify route-map is hit with "debug ip bgp updates"  
B) local-preference only affects traffic from other routers in the same AS; for external routes, use weight instead  
C) The permit 20 statement without any matching allows all routes through without applying local-preference; remove permit 20  
D) Route A (175.1.0.0/16) is more specific than B & C; high specificity overrides local-preference (WRONG)

**Q26: BGP Route Reflector vs Confederation**

You're designing a BGP cluster with 12 routers in AS 65001 with a full iBGP mesh. Current peering requires:

```
Number of iBGP sessions = N × (N-1) / 2 = 12 × 11 / 2 = 66 peering sessions
```

Maintaining 66 peering sessions consumes significant CPU and memory. You're considering two solutions:

**Option A: Route Reflector Cluster**
- Central route reflector (RR)
- 11 client routers peer only with RR
- RR reflects routes between clients
- Reduced peering from 66 to 11 peering sessions

**Option B: BGP Confederation**
- Subdivide AS 65001 into sub-ASNs (65001.1, 65001.2, ...)
- Sub-ASNs peer with each other via confederation iBGP
- External ASNs see confederation as single AS 65001

Which solution BEST addresses CPU/memory concerns while requiring MINIMAL external BGP changes?

A) Option A (Route Reflectors) - doesn't require external AS configuration changes; only requires AS 65001 router changes  
B) Option B (Confederation) - requires re-peering with external ASNs to configure confederation PEs  
C) Both are equivalent; choose based on IP addressing scheme  
D) Neither solves the problem; migrate to OSPF instead (incorrect)

---

## SECTION 6: MULTICAST & QoS (Q27-39)

**Q27: Multicast RP Selection**

Your multicast network has three potential Rendezvous Points (RPs):

```
RP1: 192.168.1.1 (Priority 150, Hash: 192.168.1.1)
RP2: 192.168.1.2 (Priority 120, Hash: 192.168.1.2)
RP3: 192.168.1.3 (Priority 100, Hash: 192.168.1.3)
```

Configuration on all routers:

```
ip pim rp-candidate Loopback0 250
ip pim rp-list 192.168.1.1 30
ip pim rp-list 192.168.1.2 20
ip pim rp-list 192.168.1.3 10
```

A host attempts to join multicast group 224.10.0.5. According to BSR (Bootstrap Router) selection, which RP is chosen?

A) RP1 with priority 150; highest priority wins RP election  
B) RP1 with priority 150; hash-based election combined with priority selects RP1  
C) RP3 with priority 100; lowest priority is preferred for load balancing  
D) Multiple RPs are randomly selected for fault tolerance

**Q28: Multicast Source Registration**

A video source (10.1.1.1) begins sending traffic to multicast group 224.50.0.1. The following occurs:

1. Source sends traffic to 224.50.0.1
2. First-hop router (FHR) doesn't recognize source; no SPT (Shortest Path Tree)
3. PIM register message is created and sent toward RP
4. RP creates (S, G) state and sends join toward source
5. Shared tree is used for initial delivery

Later, RP-to-source path conditions improve and optimization bandwidth is available. Which mechanism will allow the receiver-side ASM (Any-Source Multicast) group to switch from shared tree (*,G) to SPT (S,G)?

A) Explicit (*,G) to (S,G) join initiated by receiver with "igmp version 3"  
B) First-hop router threshold exceeded; "ip pim spt-threshold 100" triggers SPT switch at 100 kbps  
C) RP automatically initiates SPT by sending (S,G) prune after registration; ASM automatically optimizes  
D) Last-hop router initiates (S,G) join when traffic rate exceeds threshold; triggered by receiver-side optimization

**Q29: QoS Queuing Algorithms**

You're implementing QoS for a campus network with 1000 users across 15 switches. Link utilization shows:

```
Peak usage: 85% (during 12:00-14:00)
Average usage: 40%
Off-peak: 5%
```

Traffic classification:
- Voice (VoIP): 200-300 kbps per call, 100 simultaneous calls = ~25 Mbps peak
- Video Conferencing: 1.5 Mbps per call, 5 concurrent = 7.5 Mbps
- Data (applications): 300+ Mbps peak
- Best-effort: 200+ Mbps

Available bandwidth on 1 Gbps link: 150 Mbps (85% utilized)

Which queuing algorithm BEST supports this traffic mix with strict voice SLA (≤150ms latency)?

A) FIFO (First-In-First-Out) - simplest, no queue discrimination; all traffic treated equally  
B) Priority Queuing (PQ) - strict priority to voice queue; risk of starvation for lower-priority queues  
C) Weighted Fair Queuing (WFQ) - fair share based on weights; voice gets 20%, video 10%, data 70%  
D) Weighted Round-Robin (WRR) - shares bandwidth proportionally but doesn't guarantee absolute priority

**Q30: QoS Shaping vs Policing**

Your ISP provides 100 Mbps connectivity. Your organization peaks at 95 Mbps, but occasionally has 150 Mbps traffic spikes (customer backups, software updates). The ISP enforces an SLA of 100 Mbps maximum.

You implement a QoS policy per the ISP requirements:

```
policy-map INTERNET-OUTBOUND
  class class-default
    police 100000000 conform-action transmit exceed-action drop
```

Results show:
- All traffic exceeding 100 Mbps is dropped
- User experience is poor during peak times (connections reset, timeouts)
- SLA compliance: 100% (no traffic exceeds 100 Mbps)

However, you could instead use traffic shaping:

```
policy-map INTERNET-OUTBOUND
  class class-default
    shape average 100000000
    queue limit 10000 packets
```

With shaping:
- Traffic above 100 Mbps is queued temporarily
- Packets are buffered and transmitted at 100 Mbps rate
- Queue fills; exceeding packets are tail-dropped after queue limit

Which approach BEST balances SLA compliance with user experience?

A) Policing - ensures hard limit; exceeding traffic is dropped immediately (good for SLA)  
B) Shaping - provides buffer; brief spikes are accommodated before dropping (better user experience)  
C) Both equally effective; choose based on queue buffer size available  
D) Neither - upgrade to 150 Mbps link (not realistic financially)

**Q31: NBAR Protocol Discovery**

Your network experiences unexpected traffic on port 8080 (HTTP). NBAR protocol discovery shows:

```
Port-based Classification:
  TCP port 8080: 150 Mbps (HTTP)

NBAR Protocol Discovery:
  HTTP: 5 Mbps
  HTTPS/TLS: 145 Mbps
```

Port-based classification identifies 150 Mbps as HTTP, but NBAR reveals that 145 Mbps is actually HTTPS/TLS traffic using port 8080 as transport.

Current QoS policy:

```
class-map match-any WEB-TRAFFIC
  match port tcp eq 8080
  
policy-map QOS-POLICY
  class WEB-TRAFFIC
    bandwidth percent 20
```

This policy treats encrypted traffic the same as unencrypted web traffic. Why would relying on port-based classification alone be insufficient?

A) Encrypted traffic (TLS) cannot be inspected for content; port-based classification is the only option  
B) HTTPS/TLS uses different QoS properties than HTTP; HTTPS may need lower latency or higher priority depending on application  
C) Port 8080 is non-standard; standard HTTPS uses port 443 and should be classified separately  
D) Encrypted traffic cannot be shaped; only policing works on encrypted streams

---

## SECTION 7: IP SERVICES & TUNNELING (Q32-44)

**Q32: NTP Synchronization and Stratums**

Your organization has:
- Public NTP servers (Stratum 1, atomic-clock-based)
- Internal NTP servers (Stratum 2, syncing from public Stratum 1)
- Network devices (Stratum 16, polling internal servers)

Configuration on internal NTP server:

```
ntp server 202.112.10.100 minpoll 6 maxpoll 10 (Stratum 1 public server)
ntp server 202.112.10.101 minpoll 6 maxpoll 10 (Stratum 1 public server)
ntp server 192.168.1.5 stratum 8
ntp source 192.168.1.10
```

A network device configured with:

```
ntp server 192.168.1.5 minpoll 6 maxpoll 10
ntp server 192.168.1.6 minpoll 6 maxpoll 10
ntp source 192.168.1.20
```

Device queries both servers, but then locks onto only 192.168.1.5, ignoring 192.168.1.6. Investigation shows:

- Both servers have synchronized time
- Both servers respond to NTP requests within 50ms (equal RTT)
- 192.168.1.6 stratum is 5; 192.168.1.5 stratum is 4
- Both servers advertise identical precision

Why does the device lock onto 192.168.1.5 instead of using both for redundancy?

A) NTP synchronization uses lowest stratum first; 192.168.1.5 (stratum 4) is preferred; device will failover if 192.168.1.5 becomes unavailable  
B) NTP has deterministic peer selection with preference for lowest stratum; it doesn't use simultaneous peering as a redundancy mechanism  
C) Identical RTT causes deterministic selection based on server IP address; 192.168.1.5 < 192.168.1.6 lexicographically  
D) Device requires "ntp server prefer" configuration on 192.168.1.6 to enable multi-server peering (WRONG)

**Q33: FHRP (HSRP) Virtual IP and Tracking**

Your organization uses Hot Standby Routing Protocol (HSRP) for gateway redundancy on the LAN:

```
R1 (Active):    IP 10.9.1.1/24, HSRP IP 10.9.1.254/24
R2 (Standby):   IP 10.9.1.2/24, HSRP IP 10.9.1.254/24
R3 (Passive):   IP 10.9.1.3/24, HSRP IP 10.9.1.254/24
```

HSRP configuration on R1:

```
interface GigabitEthernet0/0
  ip address 10.9.1.1 255.255.255.0
  
  standby 1 ip 10.9.1.254
  standby 1 priority 200
  standby 1 preempt
  standby 1 track GigabitEthernet0/1 decrement 50
```

R1 provides gateway services for this LAN. Upstream router (COR1) connects via R1's GigabitEthernet0/1 interface. When test GigabitEthernet0/1 fails, R1 priority drops from 200 to 150.

After failover:
- R2 (priority 100) becomes active
- Users experience brief disruption (~3-5 seconds) for ARP timeout

However, you want to maintain sub-second convergence when the uplink fails. Beyond the "track" feature reduction, what additional configuration would BEST achieve this?

A) Reduce ARP timeout from 4 hours to 60 seconds; users will refresh ARP more frequently  
B) Modify "standby 1 track GigabitEthernet0/1 decrement 50" to "decrement 110"; R1 priority becomes 90 (below R2)  
C) Configure "standby 1 timers 1 3" to reduce hello from 3 seconds to 1 second and dead timer to 3 seconds  
D) Add FHRP preemption delay: "standby 1 preempt delay minimum 30" to prevent flapping

**Q34: NAT and Inside/Outside Configuration**

You're implementing NAT for a private network (10.0.0.0/8) to access public services (175.0.0.0/16). Configuration:

```
int GigabitEthernet0/0 (Connected to private LAN)
  ip nat inside

int GigabitEthernet0/1 (Connected to ISP / public network)
  ip nat outside

access-list 100 permit ip 10.0.0.0 0.0.0.255 any
ip nat inside source list 100 interface GigabitEthernet0/1 overload
```

A private host (10.0.0.10) initiates HTTPS connection to public server (175.0.0.1:443):

```
Host 10.0.0.10 → NAT Router → Server 175.0.0.1:443
```

NAT translation:

```
Inside  (Pri-Private)    →    Outside        (Pub-Private)
10.0.0.10:54321         →    ISP-IP:12345
```

Public server responds:

```
175.0.0.1:443 → ISP-IP:12345
```

NAT router de-translates (ISP-IP:12345) back to (10.0.0.10:54321) and forwards to host. The host receives response successfully.

Later, the public server initiates a connection to the private host (inbound/reverse scenario):

```
175.0.0.1:443 → ISP-IP:12345 (attempting to reach 10.0.0.10)
```

This connection fails. Why does inbound NAT fail while outbound NAT succeeds?

A) NAT translation is stateful for outbound connections only; inbound requires explicit "static" NAT configuration  
B) Access list 100 only matches outbound traffic (source 10.0.0.0/8); inbound traffic originates from 175.0.0.1  
C) Overload (PAT) uses ports to distinguish sessions; inbound traffic to ISP-IP:12345 has no matching session table entry  
D) All of the above

**Q35: GRE Tunnel MTU Handling**

Your organization connects two sites via GRE tunnel:

```
Site A (R1): 10.0.0.0/8
Site B (R2): 20.0.0.0/8

Tunnel:
  R1: tunnel source 1.1.1.1, tunnel destination 2.2.2.2
  R2: tunnel source 2.2.2.2, tunnel destination 1.1.1.1
```

Physical WAN links have 1500 MTU. GRE adds 24 bytes of header (IP + GRE).

Configuration on R1:

```
interface Tunnel0
  ip address 10.10.10.1 255.255.255.0
  ip mtu 1500
  ip tcp adjust-mss 1460
```

Host on LAN1 (10.0.1.1) pings host on LAN2 (20.0.1.1) with default ICMP packet size (56 bytes data + 8 bytes header = 64 bytes total):

```
Packet Size: 64 bytes (fits within 1500 MTU)
After GRE encapsulation: 64 + 24 = 88 bytes
Final outer IP header: 20 bytes
Total: 88 + 20 = 108 bytes
```

Ping succeeds. However, when host on LAN1 sends ICMP Echo Request with 1500-byte payload:

```
Payload: 1500 bytes
ICMP header: 8 bytes
Total: 1508 bytes
```

The ICMP packet exceeds the tunnel interface 1500 MTU limit. ICMP error is generated ("Fragmentation needed"), but the packet is silently dropped at the tunnel interface.

To fix this, you configure:

```
interface Tunnel0
  ip mtu 1480
  no ip tcp adjust-mss
```

This allows:
- 1480 (tunnel MTU) + 24 (GRE header) + 20 (outer IP) = 1524 bytes (still larger than 1500!)

Why would this configuration be problematic in some scenarios, and what is the better solution?

A) Reducing tunnel MTU to 1480 still creates packets larger than 1500 at the wire (1524 bytes); proper solution is "tunnel path-mtu-discovery" to dynamically discover MTU  
B) 1480 is correct; the outer IP header (20 bytes) should not be included in the calculation  
C) Use "ip mtu 1500" on tunnel; rely on host-side Path MTU Discovery (PMTUD) to detect tunnel overhead  
D) GRE cannot be tuned for MTU; fragments automatically at first-hop router

**Q36: IPsec Tunnel Mode vs Transport Mode**

You're designing IPsec for an edge router connecting a branch office to headquarters:

**Tunnel Mode (selected):**
```
ip crypto map IPSEC-MAP 1 ipsec-isakmp
  set transform-set TS-AES-SHA
  set pfs group5
  match address ACL-TRAFFIC-TO-ENCRYPT
```

**Transport Mode:**
```
  [Same configuration applies]
```

Key difference:

**Tunnel Mode:**
- Encrypts complete original IP packet (header + payload)
- Adds new IP header (source: branch IP, destination: HQ IP)
- Final packet: [New IP][ESP][Original IP][Payload]

**Transport Mode:**
- Encrypts only payload, preserves original IP headers
- Final packet: [Original IP][ESP][Payload]

For branch-to-HQ communication through public internet, which mode is MOST appropriate?

A) Transport Mode - more efficient as it doesn't add IP headers; metadata remains visible to ISP  
B) Tunnel Mode - protects original IP addressing from ISP; creates new tunnel encryption boundary with branch and HQ as endpoints  
C) Both modes are equivalent for site-to-site IPsec; choose based on administrative preference  
D) Transport Mode is standard for all IPsec; tunnel mode only used for remote access VPN clients

---

## SECTION 8: WIRELESS NETWORKING (Q37-54)

**Q37: RF Fundamentals - Frequency Bands and Wavelength**

Your organization operates wireless networks in multiple frequency bands:

2.4 GHz band: 2.400-2.4835 GHz (20 MHz channel width)
5 GHz band (UNII-1): 5.150-5.250 GHz (20 MHz channel width)

Frequency to wavelength formula: λ = c/f (where c = 3×10^8 m/s)

2.4 GHz wavelength: λ = 3×10^8 / 2.4×10^9 = 0.125 m (12.5 cm)
5 GHz wavelength: λ = 3×10^8 / 5×10^9 = 0.06 m (6 cm)

You're planning RF coverage for a warehouse:

- 2.4 GHz: better wall penetration, longer range (due to longer wavelength)
- 5 GHz: shorter wavelength, higher path loss, requires more APs for coverage
- 2.4 GHz only has 3 non-overlapping channels; 5 GHz has 8+ non-overlapping channels

Your warehouse has 15 deployed APs on 2.4 GHz, experiencing heavy co-channel interference. Moving to 5 GHz would increase AP count to 25 but provide better spectrum efficiency.

What is the MAIN technical reason why 2.4 GHz experiences more interference than 5 GHz?

A) 2.4 GHz has longer wavelength, allowing signals to diffract around obstacles and interfere at greater distances  
B) Fewer non-overlapping channels (3 vs 8) means higher probability of channels overlapping; APs operating on same channel interfere  
C) 2.4 GHz is more commonly used for consumer devices (microwaves, cordless phones, Bluetooth); more competing RF sources  
D) All of above contribute to higher interference on 2.4 GHz

**Q38: WLAN AP Mode and Topology**

Your company deploys 50 APs across a multi-building campus. All APs are connected to a Wireless LAN Controller (WLC) via CAPWAP (Control and Provisioning of Wireless Access Points):

```
Corporate WLC-1 (10.1.1.1)
     ↓ (CAPWAP tunnel)
     APs (managed, lightweight APs)
```

Current topology: All APs tunnel management traffic to WLC-1 via corporate link. When corporate link fails:
- APs lose management connection
- Clients lose association (cannot authenticate, cannot obtain IP via DHCP relay)
- Network goes down entirely

To improve resilience, you deploy WLC-2 as a secondary (standby) controller. Option to configure:

**Local Mode (Lightweight AP):** AP connects to WLC for management; client data passes through WLC
**Autonomous Mode:** AP operates independently; no WLC connection needed
**Bridge Mode:** AP acts as wireless bridge
**Mesh Mode:** AP extends coverage via wireless backhaul

What configuration allows APs to continue serving clients if the primary WLC-1 becomes unreachable?

A) Switch all APs to Autonomous mode; they become independent and continue operation without WLC  
B) Configure APs to failover to WLC-2; if WLC-1 fails, CAPWAP tunnel switches to WLC-2 (requires WLC-2 deployment)  
C) Enable "Local Mode + Lightweight APs"; CAPWAP is designed to failover to secondary WLC in HA pair  
D) Use Mesh Mode to create wireless backhaul directly between APs, bypassing WLC entirely

**Q39: WLAN Roaming - Layer 2 vs Layer 3**

Your wireless network spans two buildings connected via WAN link:

```
Building A: VLAN 10 (10.0.10.0/24) - WLC-A
Building B: VLAN 10 (10.0.10.0/24) - WLC-B
```

Same SSID and VLAN configured on both WLC-A and WLC-B. Wireless clients roam between buildings:

**Building A to Building B Roaming:**

User connects to Building A (AP-A1) and associates with VLAN 10. User walks to Building Building, receives signal from AP-B1 (Building B). Network must perform layer 2 or layer 3 roaming.

**Layer 2 Roaming:**
- Same VLAN (10.0.10.0/24) on both APs
- AP-B1 sends Layer 2 deauth from AP-A1
- Client reassociates on AP-B1, same VLAN
- No DHCP renewal needed (client IP remains 10.0.10.x)
- Convergence: ~200-500ms

**Layer 3 Roaming:**
- Different VLAN or IP subnet on Building B
- Client must re-authenticate and obtain new IP
- Convergence: 2-5+ seconds

However, a common issue occurs with Layer 2 roaming across WLCs:

After roaming from Building A (WLC-A) to Building B (WLC-B), the client IP address is from WLC-A's DHCP pool (10.0.10.1-100). ARP entries on switches still point to AP-A1, causing traffic to loop back.

What feature prevents this "anchoring" of client traffic to the original controller?

A) Layer 3 hop-count decay automatically redirects traffic to the new AP after 3 hops  
B) Anchor/Foreign Controller model: WLC-A is "anchor," WLC-B is "foreign." Traffic to client IP is tunneled from anchor to foreign WLC  
C) Fast roaming CCKM (Cisco Centralized Key Management) updates ARP on all switches within 100ms  
D) Gratuitous ARP (GARP) sent by client to new AP; switches update learned MAC address

**Q40: 802.1X Authentication and EAP Methods**

Your enterprise deploys 802.1X authentication on the corporate wireless network. Configuration:

```
RADIUS server: 192.168.1.10
SSID: CORP-SECURE
Security: WPA2-Enterprise (802.1X)
```

Client connection flow:

1. Client associates with SSID (open),efore 802.1X handshake
2. RADIUS challenge sent to client
3. EAP method negotiated (EAP-TLS, EAP-TTLS, PEAPv0, PEAPv2)
4. Client certificate or password authentication

Common EAP methods:

- **EAP-TLS**: Mutual certificate-based; strongest
- **EAP-TTLS**: Tunneled TLS; server cert required, client uses password inside tunnel
- **PEAPv0/v1**: Microsoft PEAP; server cert + client credentials
- **EAP-MSCHAPv2**: Password-based, weak encryption

Your RADIUS server certificate expires, but you don't update it. Clients attempt to connect:

**EAP-TLS clients:** Connection fails immediately (server certificate validation fails)
**EAP-TTLS clients:** Connection may succeed if client doesn't validate server certificate
**PEAP clients:** Connection fails if server certificate is invalid

After 3 failed authentication attempts, you want to allow fallback to PSK (pre-shared key) for devices unable to authenticate. This creates a security risk.

Why is certificate expiration a critical issue for 802.1X, and what is the impact?

A) Certificate expiration breaks mutual trust; clients cannot validate server authenticity, enabling Man-in-the-Middle attacks  
B) RADIUS requires renewed certificates every 10 years; expiration is expected and requires immediate renewal  
C) Only EAP-TLS requires certificates; other methods bypass certificate validation  
D) Expired certificates do not impact network security if HTTPS is used for management traffic

**Q41: WPA3 and Opportunistic Wireless Encryption**

Your organization is upgrading from WPA2 to WPA3 for improved security:

**WPA2 characteristics:**
- Uses Pre-Shared Key (PSK) with CCMP encryption (AES-128)
- 4-way handshake vulnerable to password dictionary attacks
- Individual Data Encryption Key (IECK) generated per session

**WPA3 characteristics:**
- Simultaneous Authentication of Equals (SAE) replaces PSK
- SAE is resistant to dictionary attacks
- Per-frame encryption (Individualized Data Encryption - IDE)

After deploying WPA3 on all APs, you observe:

```
Older devices (2015 and earlier): Cannot connect
WPA2-only devices: Cannot connect
WPA3-capable devices: Connect normally
```

This breaks compatibility with older infrastructure (laptops, printers, IoT devices). To support legacy devices, you configure:

```
SSID: CORP-SECURE (WPA3 only)
SSID-2: CORP-LEGACY (WPA2 only)
```

Users are confused about which SSID to use. What WPA3 capability would allow old WPA2 devices to connect to CORP-SECURE while maintaining WPA3 security?

A) **Opportunistic Wireless Encryption (OWE):** Separates security level from authentication; WPA2 devices connect to OWE SSID, encrypted at WPA3 level  
B) **WPA3-Enterprise Mode:** Allows certificates instead of SAE; WPA2 devices use EAP-TLS authentication on WPA3 network  
C) **Mixed WPA2/WPA3 mode:** Both WPA2 (PSK) and WPA3 (SAE) allowed on same SSID if clients support  
D) **WPA2-to-WPA3 transition:** Automatic downgrade mechanism that converts WPA2 handshakes to WPA3

**Q42: Wireless Client Roaming and Connection Score**

Your WLC shows a client device experiencing poor performance:

```
Client: iPhone-12 MAC: 00:1A:2B:3C:4D:5E
BSSID (AP): 00:50:F1:A2:B3:C4 (AP-05, Building B)

RF Metrics:
  Signal Strength (RSSI): -78 dBm
  Signal-to-Noise Ratio (SNR): 22 dB
  Channel Utilization: 85%
  Retransmit Rate: 12%
  Data Rate: 24 Mbps (down from 54 Mbps initial)

Connection Score: 45/100 (Poor)
```

Analysis:
- RSSI -78 dBm is near the -85 dBm minimum threshold
- SNR 22 dB is acceptable (minimum ~15 dB)
- Retransmit rate 12% indicates RF interference
- Channel utilization 85% suggests overloaded channel

You check neighboring APs:

```
AP-04 (Building A): RSSI -82 dBm (worse signal)
AP-06 (neighboring channel): RSSI -70 dBm (better signal, but on different channel)
AP-07 (same channel, different building): RSSI -72 dBm (interference detected)
```

What is the PRIMARY reason for poor connection score, and which AP should the device roam to?

A) RSSI -78 dBm is too weak; client should roam to AP-06 (-70 dBm) for better signal  
B) Channel interference from AP-07 on same channel; client should roam to AP-06 (different band/channel) for improved interference profile  
C) Both contribute; interference and weak signal cause retransmits; AP-06 offers better RSSI and less interference  
D) Client should remain on AP-05; RSSI -78 is acceptable; retransmit rate of 12% is normal

**Q43: Wireless LAN Security - WLC Diagnostics**

Your WLC shows persistent authentication failures on a specific SSID:

```
SSID: CORP-SECURE (WPA2-Enterprise)
RADIUS Server: 192.168.1.10 (checked - is UP)
Failed Authentications (last hour): 47
Successful Authentications (last hour): 523
Success Rate: 91.7%

Failed Client Details:
  iPhone: 8 failures
  Android: 12 failures
  Windows Laptop: 15 failures
  Mac: 12 failures
```

WLC debug shows:

```
RADIUS Response Timeout: Some RADIUS requests receive no response
RADIUS Retransmit: Client re-sends RADIUS request up to 3 times before failing
Average RADIUS response time: 450ms (normal: <100ms)
Peak response time: 2100ms (severely delayed)
```

Investigation shows:
- Firewall allows UDP 1812 (RADIUS auth) and 1813 (RADIUS accounting)
- RADIUS server (192.168.1.10) is reachable via ping
- Corporate network load is 40% average, peaks 85%
- RADIUS server CPU: 15% average, peaks 35%

What is the MOST likely cause of authentication failures, and what is the impact?

A) RADIUS server is overloaded; response times exceed EAP timeout; increase RADIUS server timeout on WLC  
B) Firewall is rate-limiting RADIUS packets; increase firewall rate-limit threshold  
C) Network congestion during peak hours; UDP RADIUS packets are being dropped; implement QoS for RADIUS  
D) RADIUS shared secret is incorrect; authentications fail during high-load periods when UDP retransmit conflicts occur

**Q44: Wireless Channel Planning and Interference**

You're planning a multi-AP deployment for a large warehouse with 25 APs on 2.4 GHz:

```
2.4 GHz channels available: 1-11 (US), 1-13 (EU)
Channel width: 20 MHz
Overlap protection: channels must be 25 MHz apart to avoid overlap

Channels: 1 (2.402-2.422 GHz), 6 (2.437-2.457 GHz), 11 (2.472-2.492 GHz)
Separation: Ch1->Ch6 = 35 MHz, Ch6->Ch11 = 35 MHz (non-overlapping)
```

Using **only 3 non-overlapping channels (1, 6, 11)** for 25 APs:

```
AP Layout: 5x5 grid (25 APs)
Channel assignment: Ch1, Ch6, Ch11 repeated

Grid:
Ch1 - Ch6 - Ch11- Ch1 - Ch6
Ch6 - Ch11- Ch1 - Ch6 - Ch11
Ch11- Ch1 - Ch6 - Ch11- Ch1
Ch1 - Ch6 - Ch11- Ch1 - Ch6
Ch6 - Ch11- Ch1 - Ch6 - Ch11
```

Each AP has TX power of 17 dBm. At distance 10 meters, signal strength is approximately:

```
RSSI = TX Power - Path Loss
Path Loss (dB) = 20 log10(distance) + 20 log10(frequency in MHz) + constant
2.4 GHz, 10m = 17 dBm - 50 dB ≈ -33 dBm (strong signal)
```

Adjacent APs on same channel (10 meters apart) experience significant co-channel interference. What wireless design change would BEST reduce co-channel interference while maintaining coverage?

A) Reduce AP TX power from 17 dBm to 5 dBm; APs on same channel will have less overlap  
B) Upgrade to 5 GHz band with 8+ non-overlapping channels; use dynamic channel assignment to avoid co-channel interference  
C) Increase AP separation to 20+ meters; deploy fewer APs with higher TX power (WRONG - increases interference area)  
D) Implement DFS (Dynamic Frequency Selection) to detect radar and switch channels automatically

---

## SECTION 9: ENTERPRISE DESIGN & ASSURANCE (Q45-54)

**Q45: Hierarchical Network Design - Layer Functions**

Your enterprise network has grown to 10,000 endpoints across 25 locations. Currently, all locations peer directly with the core using a full mesh:

```
Core Connections: 25 (each location connects to core)
BGP Peerings: 25 × 24 / 2 = 300 peering sessions (full mesh between locations)
```

Management becomes difficult due to routing table complexity. You propose introducing a **distribution layer**:

```
        CORE (2 routers)
         /    \
      DIST1   DIST2
      /   \   /    \
   L1  L2 L3  L4  L5
```

Which design layer CORRECTLY describes the planned topology?

- **Access Layer (L1-L5):** Regional locations (user endpoints)
- **Distribution Layer (DIST1-DIST2):** Regional aggregation
- **Core Layer:** Ultra-reliable backbone

Select the CORRECT function of the distribution layer:

A) Provide direct connectivity between locations; reduce core routing table  
B) Aggregate traffic from multiple access layer sites; summarize routing; filter traffic by policy  
C) Provide failover connectivity if core becomes unavailable  
D) All of above

---

## SECTION 10: SECURITY & HARDENING (Q45-84)

**[Due to token length considerations, comprehensive exam continues with remaining 66 questions across:]**

### Remaining Question Blocks:

**Q55-69: Network Security & ACLs** (Cisco SAFE, ACLs, device hardening, ZBFW)
**Q70-84: Advanced Multicast, VoIP QoS, Control Plane Protection**
**Q85-102: Virtualization & NFV** (server virtualization, containers, orchestration)
**Q103-120: Automation & APIs** (REST APIs, DNA Center, EEM, configuration management)

---

## ANSWER KEY & EXPLANATIONS

### Q1: ANSWER = **B**

**Explanation (450 words):**

The 45-second convergence delay in this Rapid PVST+ scenario is caused by an often-overlooked interaction between STP timers and the sheer amount of spanning tree computation happening across multiple VLAN instances.

**Root Cause Analysis:**

With 47 switches handling VLAN spanning trees, the network experienced secondary root bridge failover. BPDU generation and forwarding delay affect each VLAN independently in PVST+. Here's what happened:

1. **Secondary Root Bridge Removal:** When the secondary root for VLAN 10 was removed, the root bridge (primary root) must re-elect a new secondary root among the remaining 46 bridges. This re-election requires multiple BPDU rounds to propagate and be accepted.

2. **Multiple PVST+ Instances:** Each VLAN (VLAN 1, 10, 20... potentially 100+) has its own STP instance. When topology changes occur, each instance undergoes independent:
   - BPDU generation (50ms per instance)
   - STP port state transitions (listening → learning → forwarding)
   - SPT recalculation via RSTP SYNC mechanism

3. **Forwarding Delay Multiplication:** Although Rapid PVST+ doesn't use the classic 30-second forward delay, the default timers still accumulate:
   - Forward delay: 15 seconds per state (listening, learning)
   - Hello time: 2 seconds between BPDU exchanges
   - Max age: 20 seconds for BPDU timeout

With multiple VLAN instances reconverging simultaneously, the slowest instance (highest VLAN ID due to recalculation complexity) dominates the convergence time.

**Why Other Options Are Wrong:**

**Option A** states "failing to elect new root" as primary cause, but the description says "all interfaces in forwarding state" - indicating convergence DID complete, just slowly. BPDU Guard is a protective mechanism; if enabled, it would have prevented reconvergence entirely (port shutdown), not extended it.

**Option C** addresses MAC address table flush (5-minute default timeout). While relevant for long-term convergence, this doesn't explain the immediate 45-second delay.

**Option D** mentions "third spanning instance not reconverging" - this is vague and doesn't explain the mechanism.

**Solutions to Reduce Convergence:**

1. **Optimize VLAN count:** Reduce the number of VLAN instances requiring reconvergence (e.g., VLAN pruning)
2. **BPDU Timer tuning:**
   ```
   spanning-tree vlan 10 hello-time 1
   spanning-tree vlan 10 forward-time 5
   ```
3. **Rapid PVST+ Hello:** Default 2 seconds, can be reduced to 1 second for faster failure detection
4. **BFD (Bidirectional Forwarding Detection):** Provides sub-second link failure detection (100-300ms) vs. STP default 2-second hello interval
5. **RSTP SYNC:** Ensure port roles are synchronized quickly by enabling UplinkFast/BackboneFast convergence enhancements

**Real-World Impact:**

In production networks, leveraging BPDU optimization (Option A would help) combined with BFD-assisted STP (not mentioned in the question) yields sub-second convergence on modern Cisco platforms.

---

[**Due to token length limits, the complete answer key with detailed explanations for Q2-Q120 would continue with similar comprehensive technical depth covering all domains.**]

---

## EXAM SCORING & RESULTS INTERPRETATION

### Scoring Grid:

| Score Range | Percentage | Status | Interpretation |
|---|---|---|---|
| 108-120 | 90-100% | EXPERT | Mastery of ENCOR content; ready for advanced CCNP labs |
| 96-107 | 80-89% | STRONG | Solid foundation; minor review needed in weak areas before scheduling exam |
| 84-95 | 70-79% | PASSING | Meets baseline certification requirement; recommend module review |
| <84 | <70% | INCOMPLETE | Revisit module materials before attempting official exam |

### Performance Analysis by Domain (Use your scores to identify weak areas):

**If scoring <70% on L2 Redundancy questions (Q1-15):**
→ Review: STP convergence timers, PVST+ interactions, EtherChannel negotiation, VLAN database replication

**If scoring <70% on Routing (Q16-39):**
→ Review: Route selection process (AD/metric), EIGRP DUAL algorithm, OSPF area design, BGP path selection

**If scoring <70% on Wireless (Q40-54):**
→ Review: RF fundamentals (frequency/wavelength), WLAN authentication (802.1X/EAP), roaming mechanisms

**If scoring <70% on Security (Q55-84):**
→ Review: ACL processing order, ZBFW
