---
title: "Module 24: Network Assurance et outils diagnostics"
module: 24
type: notes
topics: [network-assurance, ping, traceroute, OSPF-debugging, NetFlow, SPAN, IP-SLA, DNA-Center-Assurance]
difficulty: intermediate
updated: 2026-03-18
---

# Module 24: Network Assurance et outils diagnostics

## Vue d'ensemble
Network Assurance garantit performance, disponibilité, et compliance du réseau via monitoring proactif, diagnostic approfondi, et telemetry analytics. Ce module couvre tools diagnostics classiques (ping, traceroute), technologies monitoring (NetFlow, SPAN, IP SLA), et solutions modernes (DNA Center Assurance).

## Diagnostic Tools fondamentaux

### Tool 1: Ping (ICMP Echo Test)

#### Concept fondamental
Ping envoie ICMP Echo Requests et attend réponses (Echo Replies), permettant tester basic reachability sans ouvrir protocoles de transport (TCP/UDP).

#### Paramètres ping standard

| Parameter | Default | Notes |
|-----------|---------|-------|
| **packet count** | 5 | Number ICMP echo requests sent |
| **packet size** | 100 bytes | Payload + 8 byte ICMP header = 108 total |
| **timeout** | 2 seconds | Wait time per reply before marking LOST |
| **interval** | 1 second | Wait between successive pings |
| **source interface** | Device default route | Optional binding source IP |

#### Interprétalion ping output

**Successful ping:**
```
Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=25ms TTL=56
Reply from 8.8.8.8: bytes=32 time=24ms TTL=56
Reply from 8.8.8.8: bytes=32 time=25ms TTL=56
Reply from 8.8.8.8: bytes=32 time=26ms TTL=56

Ping statistics for 8.8.8.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
    Approximate round trip times in milli-seconds:
        Minimum = 24ms, Maximum = 26ms, Average = 25ms

Result: ✓ Reachability verified
```

**Failed ping (no response):**
```
Pinging 192.168.99.99 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.99.99:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)

Result: ✗ Host unreachable (no route, host down, firewall blocked, or ICMP disabled)
```

**Partial loss (intermittent issue):**
```
Ping statistics:
    Packets: Sent = 5, Received = 3, Lost = 2 (40% loss)
    Average = 150ms [vs normal 25ms typical]

Result: ⚠ Intermittent connectivity (flaky link, congestion, or rate-limiting)
```

#### Extended ping options (Cisco routers/switches)

**Exemplaire usages:**
```
Router# ping 10.1.1.1 [standard ping]
Router# ping
Protocol [ip]: <enter>
Target IP address: 10.1.1.1
Repeat count [5]: 100 [send 100 packets instead 5]
Datagram size [100]: 1500 [test maximum MTU path]
Timeout in seconds [2]: 5 [wait longer for reply]
Extended commands [n]: y [enter extended mode]
Source address or interface: 10.0.0.1 [bind source IP]
Type of service [0]: 184 [EF DSCP for QoS]
Set DF bit in IP header? [no]: yes [test fragmentation requirement]
Validate reply data? [no]: yes [check payload integrity]
Data pattern [0xABCD]: [enter custom hex pattern]
Loose, Strict, Record, Timestamp, Verbose[none]: record [enable IP record route]
Sweep range of sizes [n]: y [test varying sizes]
```

#### Important ping options explained

**DF Bit (Don't Fragment):**
- Testing MTU path (Maximum Transmission Unit)
- If DF=1 and packet > interface_MTU → "Fragmentation needed but DF set" response
- Useful: Diagnose PMTUD (Path MTU Discovery) issues

Example:
```
Router# ping
... [settings above]
Set DF bit in IP header? [no]: yes
Datagram size [100]: 1500

IF response: "Fragmentation needed and DF set"
→ Somewhere in path, MTU < 1500 bytes
→ Issue: Misconfiguous MTU values on links, black-holing traffic
```

**ToS (Type of Service) = DSCP marking:**
- DSCP value 0-63 (6 bits) + 2 ECN bits = 8-bit ToS field
- Example: 184 decimal = 0xB8 binary = 101110 00
- Meaning: EF (Expedited Forwarding) DSCP 46 (binary 101110)
- Testing QoS: Verify different packet markings routed identically (no special treatment)

---

### Tool 2: Traceroute (Path determination)

#### Concept fondamental
Traceroute identifies path packets traverse from source to destination by sending UDP packets with incrementing TTL (Time-To-Live), causing each hop to ICMP-reply with its address.

#### Mecánica traceroute standard

```
Traceroute phases:

Phase 1: TTL=1
├─ Source sends 3 UDP packets (port 33434 typically) to destination
├─ First hop router receiving TTL=1 → decrements to 0 → ICMP exceed time
└─ Source receives ICMP from hop 1 + latency measurement

Phase 2: TTL=2
├─ Next set 3 UDP packets with TTL=2
├─ Hop 1 forwards, Hop 2 decrements to 0 → ICMP exceed
└─ Source receives ICMP from hop 2 + latency measurement

Phase N: TTL=N
├─ Continue until destination reached OR max TTL (usually 30)
└─ Destination receives UDP packet → ICMP port unreachable OR accepts packet

Output format:
traceroute to example.com (93.184.216.34), 30 hops max
 1  router.local (192.168.1.1)  1.234 ms  1.567 ms  1.890 ms
 2  isp-gw.example.net (203.0.113.1)  5.234 ms  5.456 ms  5.678 ms
 3  * * *  [Hop 3 no response - firewall blocking ICMP?]
 4  core-router.isp.net (198.51.100.5)  15.234 ms  15.456 ms  15.678 ms
 5  example.com (93.184.216.34)  20.234 ms  20.456 ms  20.678 ms
```

#### Interpretación traceroute output

| Output | Meaning | Action |
|--------|---------|--------|
| **IP address shown** | Hop responding normally | Note latency, look for spikes |
| ***** three asterisks | No response from hop | Firewall ICMP filter OR router doesn't respond |
| **Increasing latency** | Cumulative delay | Normal unless sudden spikes |
| **Stops before destination** | Path truncation | Firewall, no route, or TTL limit reached |
| **"Host unreachable"** | Destination can't be reached | Target down or routing hole |

#### Extended traceroute options

```
Router# traceroute
Protocol [ip]: <enter>
Target IP address: 8.8.8.8
Source address: 10.0.0.1 [bind source interface]
Numeric display [no]: yes [skip DNS reverse lookup - faster]
Timeout in seconds [3]: 5 [wait longer for ICMP responses]
Probe count [3]: 1 [send 1 packet per hop instead 3]
Minimum TTL [1]: 1 [start TTL value]
Maximum TTL [30]: 15 [limit max hops (useful if 30 default slow)]
Port Number [33434]: 12345 [custom UDP port]
Type of service [0]: 184 [EF ToS for QoS path testing]
```

**Cas d'usage troubleshooting:**
```
Scenario: File transfer slow between two campus buildings
├─ Traceroute shows 5 hops normal latency (<5ms each)
├─ But iperf shows only 2 Mbps vs expected 100 Mbps
└─ Issue likely: QoS rate-limiting, not path-based latency
   → Go deeper: NetFlow packet analysis OR check QoS policies

Scenario: Remote user VPN can't reach specific server
├─ Traceroute to server stops after hop 3
├─ Error: "Host unreachable"
└─ Issues possible:
   ├─ No route from company datacenter to server IP
   ├─ ACL/firewall blocking return traffic
   └─ Server not routing back via same path (asymmetric routing)
```

---

## Deep Protocol Debugging

### OSPF Adjacency Troubleshooting

#### Debug OSPF Adjacency Command

**Enablement:**
```
Router# debug ip ospf adj [adjacency formation debugging]
OSPF Adjacency events debugging is on

[Sample output:]
OSPF: Interface FastEthernet0/0 address 10.0.0.1 added to OSPF area 0
OSPF: Build router LSA for area 0, router ID 1.1.1.1, seq 0x80000001
OSPF: Rcv pkt from 10.0.0.2 (FastEthernet0/0): Mismatch hello. Originator ID 2.2.2.2
OSPF: Rcv hello from 10.0.0.2 area 0 (1) gen 0xa [valid]
OSPF: 2 Way Communication to 2.2.2.2, state EXSTART [adjacency forming]
OSPF: Send DB Description to 2.2.2.2 on FastEthernet0/0 seq 0x7d opt 0x52 flag 0x7 len 32
OSPF: Rcv DB Description from 2.2.2.2 on FastEthernet0/0 seq 0x123 opt 0x52 flag 0x3 len 536
OSPF: Exchange Done with 2.2.2.2 on FastEthernet0/0 [exchange complete]
OSPF: Synchronized with 2.2.2.2 on FastEthernet0/0, state FULL [adjacency complete]
```

#### OSPF Adjacency states
```
Adjacency progression:
├─ DOWN: No hello heard yet
├─ INIT: Hello received but bidirectional not confirmed
├─ 2-WAY: Bidirectional communication established
├─ EXSTART: Master/slave negotiation starts (Database Descriptor)
├─ EXCHANGE: Sending Database Descriptors (LSA summary exchange)
├─ LOADING: Requesting full LSA updates (Link State Request)
├─ FULL: Database synchronized, adjacency complete

Stuck states indicate issues:
├─ INIT → 2-WAY: Verify hello parameters match (interval, dead timer)
├─ 2-WAY → EXSTART: MTU mismatch likely (see below)
├─ EXSTART → EXCHANGE: Master role negotiation failed (timer expire)
└─ LOADING → FULL: LSA request timeout (missing route or bad LSA)
```

#### Common OSPF Issues resolved with debugging

**Issue 1: MTU Mismatch**
```
Debug output shows:
OSPF: Rcv hello from 10.0.0.2 area 0... [OK]
OSPF: 2 Way Communication... [OK]
OSPF: Send DB Description... [OK]
OSPF: Rcv DB Description... [ERROR] Mismatch MTU
OSPF: Interface FastEthernet0/0 MTUQ=1500 Mtuip=1500, MTU mismatch...

Cause: Interface MTU values differ (one 1500, other 1460)
Resolution: Ensure both sides MTU same
Router# show ip ospf interface [check MTU in output]
Router# interface FastEthernet0/0
Router(config-if)# ip mtu 1500 [set matching value]
```

**Issue 2: Hello Timer Mismatch**
```
Debug output shows:
OSPF: Rcv hello interval mismatch from 10.0.0.2 [ISSUE]
OSPF: Hello interval [10 vs 20 seconds]
OSPF: Dead interval [40 vs 60 seconds]

Cause: OSPF timer configurations don't match
Resolution:
Router# interface FastEthernet0/0
Router(config-if)# ip ospf hello-interval 10
Router(config-if)# ip ospf dead-interval 40
[Configure matching timers both routers]
```

**Issue 3: IP Subnet Mismatch**
```
Debug output shows:
OSPF: Ignoring hello from 10.0.0.2 - subnet 255.255.255.0 NOT adjacent to 255.255.0.0

Cause: Interfaces in different subnets (10.0.0.0/24 vs 10.0.0.0/16)
Resolution: Verify subnet mask configuration both routers
Router# show ip interface FastEthernet0/0
[Verify "Internet address is 10.0.0.1 255.255.255.0"]
```

**Issue 4: Network Type Mismatch**
```
Debug output shows:
OSPF: Rcv hello from 10.0.0.2, network type mismatch [ISSUE]
[One side thinks point-to-point, other thinks broadcast]

Resolution:
Router# interface FastEthernet0/0
Router(config-if)# ip ospf network-type broadcast [force broadcast]
[OR]
Router(config-if)# ip ospf network-type point-to-point [force p-to-p]
```

#### OSPF Network Types table

| Type | Hello interval | Dead interval | Use case | Broadcast |
|------|---|---|---|---|
| **Broadcast** | 10 seconds | 40 seconds | Ethernet, Fast Ethernet | Yes (multicast 224.0.0.5) |
| **Point-to-point** | 10 seconds | 40 seconds | Serial WAN links, P2P tunnels | No |
| **Non-broadcast** | 30 seconds | 120 seconds | Frame Relay, X.25 | No |
| **Loopback** | N/A | N/A | Virtual loopbacks | N/A |

---

## Flow Monitoring Technologies

### NetFlow (Traffic analytics)

#### NetFlow versions
```
NetFlow v5 (Legacy but common):
├─ Flows captured: Source IP, Destination IP, Source Port, Dest Port, Protocol
├─ Export interval: 60 seconds default (configurable)
├─ Collector: External NETFLOW collector (Cisco NetFlow Analyzer typical)
└─ Field count: ~7 key fields

NetFlow v9 (Flexible):
├─ Template-based: Customizable field sets (not fixed)
├─ Bi-directional flows: Separate A→B vs B→A tracking
├─ Flow counters: Bytes, packets, duration, flags
└─ Field count: 90+ optional fields

IPFIX (Internet Protocol Flow Information eXport - RFC 5101):
├─ Standardized successor NetFlow v9
├─ IETF standard, multi-vendor support
├─ Forward compatibility: New fields dynamically added
└─ Encryption: Optional TLS transport
```

#### Flexible NetFlow deployment
```
Router# flow exporter NetFlowCollector
Router(config-flow-exporter)# destination 10.50.50.50 [collector IP]
Router(config-flow-exporter)# transport udp 2055 [UDP port]
Router(config-flow-exporter)# source 10.0.0.1 [source IP binding]
Router(config-flow-exporter)# version 9 [export format]

Router# flow monitor TrafficMonitor
Router(config-flow-monitor)# exporter NetFlowCollector [attach exporter]
Router(config-flow-monitor)# record netflow ipv4 original-input [fields captured]

Router# interface GigabitEthernet0/0
Router(config-if)# ip flow monitor TrafficMonitor input [enable on input]

Collector analysis:
├─ Top talkers: Which IPs generating most traffic
├─ Protocol breakdown: % TCP vs UDP vs ICMP
├─ Application identification: Port-based app detection (port 443=HTTPS, 80=HTTP)
└─ Anomaly detection: Sudden traffic spike OR unusual protocols
```

---

## Packet Mirroring (SPAN)

### SPAN Variants

#### Local SPAN (Same switch)
```
Switch# monitor session 1 source interface Gigabit0/1 [source port to mirror]
Switch# monitor session 1 destination interface Gigabit0/48 [destination port (Wireshark PC)]
Switch# monitor session 1 direction both [mirror ingress + egress traffic]

Traffic flow:
PC on Gi0/1 ↔ Switch [mirrored to Gi0/48]
├─ Packets sent FROM PC also mirrored
├─ Packets received TO PC also mirrored
└─ Wireshark on Gi0/48 captures all activity PC interface
```

#### RSPAN (Remote SPAN - different switches)
```
Source Switch (where traffic originates):
├─ VLAN 100 used as RSPAN VLAN (isolated, no user access)
├─ Session source: Gi0/1 → RSPAN VLAN 100

Trunk link (Gi0/1 trunk):
├─ RSPAN VLAN 100 allowed on trunk
├─ Mirrored packets transported in VLAN 100

Destination Switch (where Wireshark analyzer connected):
├─ VLAN 100 configured as RSPAN VLAN (matching source)
├─ Monitor session: RSPAN VLAN 100 → Gi0/48 (analyzer interface)

Benefit:
└─ Analyze traffic remotely without connecting locally
```

#### ERSPAN (Encapsulated Remote - GRE tunnel)
```
Source Switch:
├─ Monitor session 1
├─ Source: Interface Gi0/1 (or VLAN)
├─ Destination IP: 10.50.50.50 [analyzer router IP]
├─ ERSPAN ID: 100
└─ Direction: Both

Traffic encapsulation:
GRE(IP_SRC=10.0.0.1 [source switch IP], IP_DST=10.50.50.50) {
  ├─ ERSPAN header (Session ID, Sequence)
  └─ Mirrored packet [Ethernet + IP + TCP/UDP]
}

Destination Analyzer:
├─ Receives ERSPAN encapsulated packets
├─ GRE decapsulation
├─ Payload inspection (original packet)
└─ Wireshark analysis

Benefits:
└─ Works across multiple sites (IP routing, WAN compatible)
```

---

## IP SLA (Service Level Agreement Monitoring)

#### Concept IP SLA
IP SLA sends synthetic probes measuring network performance: latency, jitter, packet loss, connectivity verification.

#### IP SLA operations types

```
1. ICMP Echo (ping-like):
├─ Probes sent: ICMP echo every N seconds
├─ Response: RTT + packet loss measurement
├─ Use: Simple reachability, baseline latency

2. TCP/UDP Connect:
├─ Probes sent: TCP SYN to target IP:port
├─ Response: Connection success/failure, response time
├─ Use: Verify service availability (HTTP port 80, HTTPS 443)

3. DNS Query:
├─ Probes sent: DNS A record query
├─ Response: Resolution success, query time
├─ Use: Verify DNS server functionality

4. HTTP GET:
├─ Probes sent: HTTP GET request to URL
├─ Response: HTTP status (200=success, 404=not found), download time
├─ Use: Web server monitoring (SAP portal availability, etc.)

5. JITTER (advanced):
├─ Probes sent: Stream of N packets (UDP typically)
├─ Response: Min/max/avg latency, jitter, packet loss
├─ Use: VoIP quality assessment (MOS Mean Opinion Score)
```

#### Configuration IP SLA example
```
Router# ip sla 1
Router(config-ip-sla)# icmp-echo 8.8.8.8 [target Google DNS]
Router(config-ip-sla-echo)# frequency 60 [probe every 60 seconds]
Router(config-ip-sla-echo)# timeout 5000 [wait 5 seconds max]
Router(config-ip-sla-echo)# exit

Router# ip sla schedule 1 life forever start-time now

[Scheduling continuous monitoring]

Viewing results:
Router# show ip sla summary [overview all SLAs]
Router# show ip sla statistics 1 [detailed results SLA 1]
├─ Latest Probe Duration: 2 msec
├─ Min/Max/Average: 1/5/2 msec
├─ Packet loss: 0%
├─ Connection Loss Counts: 0
```

#### IP SLA alerting
```
Router# ip sla reaction-configuration 1 [setup alerts on SLA 1]
Router(config-sla-react)# react value-type round-trip-time threshold 50 [alert if RTT > 50ms]
Router(config-sla-react)# action-type trap [send SNMP trap]

Trigger actions:
├─ IF threshold exceeded → SNMP trap sent to monitoring station
├─ OR IF link down → Failover to secondary WAN (with IP routing changes)
└─ OR IF service unavailable → Escalation alert (page admins)
```

---

## Cisco DNA Center Assurance

### Assurance capabilities overview
```
DNA Center Assurance module provides:

1. Network Health Dashboard:
├─ Device health: CPU, memory, disk utilization
├─ Interface status: Up/down, errors, drops
├─ Application performance: Latency, throughput, MOS (VoIP)
└─ Client experience: Device count, roaming, bandwidth

2. Proactive Issue Detection:
├─ ML algorithms identify anomalies vs baseline
├─ Predictive: "Storage filling rate = out in 7 days"
├─ Root cause analysis: Suggests likely issues
└─ Remediation suggestions: "Increase QoS bandwidth allocation"

3. Encrypted Traffic Analytics (ETA):
├─ TLS flow decryption impossible (end-to-end encryption)
├─ BUT: Behavioral analysis (flow patterns, payload size distribution)
├─ Enterprise app identification: Slack, Zoom, Teams without DPI
└─ Security: Detect encrypted malware C&C communications

4. Real-time Workflows:
├─ Telemetry collection: Every 30-60 seconds from devices
├─ Data processing: ML analysis for patterns
├─ Dashboard update: Real-time visibility (not syslog polling delays)
└─ Scalability: Handles 1000+ devices efficiently
```

### DNA Center assurance workflow example

```
Scenario: IT team notices slow network performance for 50 users in building

Step 1: DNA Center detects anomaly
├─ Latency spike detected (normal 10ms → 150ms)
├─ Packet loss increased (0% → 5%)
└─ Application latency increase (user complaints about Slowloads)

Step 2: Root cause analysis
├─ DNA Center correlates: Building X Access Switch CPU = 85%
├─ Distribution Link Gigabit0/1 → Gi0/2 has 40% utilization (vs normal 5%)
├─ Wireless: AP interference detected (same channel as neighboring org)
└─ ISE: Large number 802.1x authentications (new policy deployment)

Step 3: Dashboard alerts
├─ Device health card: Distribution-X CPU threshold
├─ Link utilization graph: Spike at 2:15 PM
├─ Client experience: 50 users "Poor" score
└─ Application analytics: File transfer latency 30s+ (normal 2s)

Step 4: Suggested remediation
├─ "Disable/move APs to non-overlapping channel"
├─ "Increase bandwidth allocation Distribution-X uplink"
├─ "Review ISE policy change deployment (delay roll-out)"
└─ "Scale access switch resources (add capacity)"

Step 5: Operator action
├─ Implement suggested fixes
├─ Re-run diagnosis (DNA Center rebaselines)
├─ Performance returns to normal within 10 minutes
└─ Issue resolved, RCA documentation archived
```

---

## Points clés à retenir

### Diagnostic tools selection
- **Ping**: Quick reachability check (is target alive?)
- **Traceroute**: Path discovery (where does packet go?)
- **OSPF debug**: Adjacency formation troubleshooting (why not neighbors?)
- **NetFlow**: Traffic analysis (what applications, top talkers?)
- **SPAN**: Packet-level inspection (protocol analysis, Wireshark)
- **IP SLA**: Service availability monitoring (is web server responding?)
- **DNA Center**: Holistic health (network-wide performance, ML-based insights)

### Configuration best practices
- **Extended ping**: Test DF bit for MTU issues, ToS for QoS verification
- **Traceroute**: Combine with show ip route to understand path selection
- **OSPF debug**: Enable, reproduce issue, save output for analysis
- **NetFlow**: Always enable on links carrying traffic (ingress + egress)
- **SPAN**: Use GRE (ERSPAN) for remote analyzer (more scalable than RSPAN VLAN)
- **IP SLA**: Threshold tuning critical (too loose = false alerts, too strict = ignored)

### Modern assurance integration
- **DNA Center**: Primary tool for health/anomalies (replaces manual troubleshooting)
- **ISE integration**: ETA capabilities embedded in DNA Center dashboards
- **Telemetry**: Real-time push vs pull (NETCONF push superior to NetFlow pull)
- **Historical trending**: 1-month + retention for comparative analysis

---

## Ressources complémentaires
- Cisco OSPF configuration guide (debug ip ospf commands)
- Wireshark documentation (packet analysis, protocol dissectors)
- RFC 3575 (RADIUS accounting/auth)
- RFC 4898 (TCP extended diagnostics)
- DNA Center release notes (assurance feature additions)
- IP SLA Best Practices (Cisco whitepaper)
