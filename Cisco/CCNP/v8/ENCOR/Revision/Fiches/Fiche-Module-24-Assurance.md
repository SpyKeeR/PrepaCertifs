---
title: "Fiche Module 24: Network Assurance et diagnostics"
module: 24
type: fiche
topics: [ping-traceroute, OSPF-debugging, NetFlow, SPAN, IP-SLA, DNA-Center, network-monitoring]
difficulty: intermediate
updated: 2026-03-18
---

# Fiche Module 24: Network Assurance et diagnostics

## Outils diagnostics comparatif

| Outil | But | Quand utiliser | Sortie |
|-------|-----|--------|--------|
| **ping** | Reachability + latency | Baseline connectivity | RTT (ms), loss % |
| **traceroute** | Path determination | Where does packet go? | Hop IP + latency per hop |
| **debug OSPF** | Protocol adjacency | Adjacency fails formation | Detailed state machine |
| **NetFlow** | Application traffic | Who uses bandwidth? | Flow summary (bytes, packets) |
| **SPAN** | Packet inspection | Deep protocol analysis | Wireshark capture |
| **IP SLA** | Service availability | Monitor server availability | Success/fail + RTT |
| **DNA Center** | Network health | Holistic monitoring | Dashboard + ML insights |

---

## Ping: Réference rapide

### Format commande standard
```
ping 8.8.8.8

Résult:
├─ 5 packets sent (default)
├─ Responses: 5/5 successful ✓ OK
├─ RTT: min/avg/max = 20/25/30 ms
└─ Status: Reachability verified
```

### Extended ping options (Cisco)

| Option | Syntax | Utilité |
|--------|--------|---------|
| **Repeat count** | `-c 100` | Send 100 packets (vs 5 default) |
| **Packet size** | `-s 1500` | Test MTU size (1500 = standard Ethernet) |
| **Timeout** | `-W 5` | Wait 5 sec per reply (vs 2s default) |
| **DF bit** | `Set DF bit? yes` | Test path fragmentation requirements |
| **ToS/DSCP** | `Type of service: 184` | Test QoS marking (EF = expedited) |
| **Source IP** | `-I 10.0.0.1` | Bind source interface binding |

### Interprétation ping output

```
All replies received:
└─ "5/5 successful, 0% loss" ✓ Reachability OK

Partial loss (intermittent):
└─ "3/5 successful, 40% loss" ⚠ Flaky link or rate-limiting

No replies:
└─ "0/5 successful, 100% loss" ✗ Host down, no route, ICMP disabled

High latency:
└─ "Average = 150ms" (normal ~25ms) → congestion or distant host

Fragmentation issue (with DF bit):
└─ "Fragmentation needed but DF set" → MTU mismatch (fix: reduce MTU or enable PMTUD)
```

---

## Traceroute: Référence rapide

### Format commande
```
traceroute 8.8.8.8

Output:
 1  router.local (192.168.1.1)  1.2 ms  1.3 ms  1.4 ms
 2  isp-gw.net (203.0.113.1)    5.1 ms  5.2 ms  5.3 ms
 3  * * *  [No response]
 4  core-router (198.51.100.5)  15.1 ms 15.2 ms 15.3 ms
 5  8.8.8.8 (Google DNS)        20.1 ms 20.2 ms 20.3 ms

Hops: Cumulative path = 5 routers to destination
Asterisks (*): Hop not responding (firewall ICMP filtering?)
Latency: RTT increasing per hop normally
```

### Extended traceroute options (Cisco)

| Option | Syntax | Utilité |
|--------|--------|---------|
| **Numeric** | `-n` | Skip DNS reverse lookup (faster) |
| **Timeout** | `-w 5` | Wait 5 seconds per hop reply |
| **Max hops** | `-m 15` | Stop after 15 hops (vs 30 default) |
| **Probes** | `-q 1` | Send 1 probe per hop (vs 3 default) |
| **ToS** | `Type of service: 184` | Test specific QoS path |

### Troubleshooting avec traceroute

```
Scenario 1: File transfer slow endpoint-to-endpoint
├─ Traceroute shows all hops < 5ms ✓ Path latency OK
└─ Issue likely: QoS rate-limiting or application problem (not network path)

Scenario 2: Remote site unreachable
├─ Traceroute stops at hop 3: "Host unreachable"
└─ Diagnosis:
  ├─ No route exists from that point
  ├─ Firewall blocking return traffic
  └─ Asymmetric routing (goes up, can't come back)

Scenario 3: Latency spikes at particular hop
├─ Hops 1-3: 5ms each
├─ Hops 4-5: "* * *" (no response, router doesn't generate ICMP exceed)
└─ Assessment: Likely legacy router ignoring TTL (not critical)
```

---

## OSPF Adjacency Debugging

### Debug command activation
```
Router# debug ip ospf adj

Output interpretation:
├─ "Rcv hello from 10.0.0.2" ✓ OSPF running
├─ "2 Way Communication established" ✓ Bidirectional OK
├─ "Database Descriptor exchange" ✓ EXSTART→EXCHANGE
├─ "Synchronized with 10.0.0.2" ✓ FULL adjacency
└─ [Errors if any]
```

### Common issues resolved

| Issue | Symptôme | Résolution |
|-------|----------|-----------|
| **MTU mismatch** | EXCHANGE state stuck | Set `ip mtu 1500` both sides |
| **Hello interval** | INIT → 2-WAY (no progress) | Verify `ip ospf hello-interval 10` |
| **Dead interval** | Quick adjacency drop | Check `ip ospf dead-interval 40` |
| **Network type** | Unicast vs multicast mismatch | Set `ip ospf network-type broadcast` |

### OSPF network types table

| Type | Hello | Dead | Broadcast | Use case |
|------|-------|------|-----------|----------|
| **Broadcast** | 10s | 40s | Yes (224.0.0.5) | Ethernet |
| **Point-to-Point** | 10s | 40s | No | Serial, VPN tunnel |
| **Non-Broadcast** | 30s | 120s | No | Frame Relay |
| **Loopback** | N/A | N/A | N/A | Virtual testing |

---

## NetFlow monitoring

### Versions

```
NetFlow v5 (Legacy):
├─ Fields: Source IP, Dest IP, Sport, Dport, Protocol
├─ Export: Every 60 seconds
└─ Workflow: Enable on interface → collector receives flows

NetFlow v9 (Flexible):
├─ Template-based (customizable fields)
├─ Bi-directional flow tracking
└─ Extended field set (90+ options)

IPFIX (Standard RFC 5101):
├─ Multi-vendor standard
├─ Forward compatible
└─ Recommended for new deployments
```

### Configuration example
```
Router(config)# flow exporter NetFlowCollector
Router(config-flow-exporter)# destination 10.50.50.50 2055
Router(config-flow-exporter)# transport udp
Router(config-flow-exporter)# version 9

Router(config)# flow monitor TrafficMonitor
Router(config-flow-monitor)# exporter NetFlowCollector
Router(config-flow-monitor)# record netflow ipv4 original-input

Router(config-if)# interface GigabitEthernet0/0
Router(config-if)# ip flow monitor TrafficMonitor input
```

### Collector analysis uses
```
Top talkers: Identify high-bandwidth sources
Application breakdown: % by protocol (TCP, UDP, ICMP)
Anomaly detection: Sudden traffic spikes
Trend analysis: Long-term bandwidth growth
Compliance: Verify data flow conformance
```

---

## SPAN (Port/VLAN Analyzer)

### Types SPAN

| Type | Scope | Use case | Setup |
|------|-------|----------|-------|
| **Local SPAN** | Same switch | 1 port → 1 port mirroring | `monitor session 1 source interface Gi0/1` |
| **RSPAN** | Remote switch | VLAN-based (isolated trunk) | VLAN 100 (RSPAN VLAN) + source → destination |
| **ERSPAN** | Remote via GRE | IP-routed (WAN capable) | GRE tunnel encapsulation + ERSPAN header |

### Configuration exemple Local SPAN
```
Switch# monitor session 1 source interface Gigabit0/1 [traffic source]
Switch# monitor session 1 destination interface Gigabit0/48 [analyzer PC]
Switch# monitor session 1 direction both [ingress + egress]
Switch# show monitor session 1 [verify active]

Résultat: Wireshark PC on Gi0/48 sees all traffic from Gi0/1
```

### Configuration ERSPAN (Recommended)
```
Source Switch:
monitor session 1 type erspan-source
 source interface Gigabit0/1 direction both
 destination ip 10.50.50.50 [analyzer IP]
 erspan-id 100
 ip ttl 64

Destination Switch/PC: Receives GRE-encapsulated packets
├─ GRE tunnel decapsulates automatically
├─ Payload = original Ethernet frame
└─ Wireshark analyzes normally

Benefits:
✓ Works across WAN
✓ No VLAN burden
✓ Scalable (many sources → 1 analyzer)
```

---

## IP SLA Monitoring

### Operations types

```
ICMP Echo:
├─ Probe: ICMP echo every N sec
├─ Metric: RTT + packet loss
└─ Use: Simple latency baseline

TCP/UDP Connect:
├─ Probe: TCP SYN to IP:port
├─ Metric: Connection success + RTT
└─ Use: Service availability (HTTP:80, HTTPS:443)

HTTP GET:
├─ Probe: HTTP GET request
├─ Metric: HTTP status code + download time
└─ Use: Web server functionality

DNS Query:
├─ Probe: DNS A record lookup
├─ Metric: Resolution time + success/fail
└─ Use: DNS server health
```

### Configuration + scheduling
```
Router(config)# ip sla 1
Router(config-ip-sla)# icmp-echo 8.8.8.8 [Google DNS target]
Router(config-ip-sla-echo)# frequency 60 [probe every 60 sec]
Router(config-ip-sla-echo)# timeout 5000 [5 second max wait]
Router(config-ip-sla-echo)# exit

Router(config)# ip sla schedule 1 life forever start-time now [continuous]

View results:
Router# show ip sla statistics 1
├─ Latest Probe Duration: 2 msec
├─ Min/Max/Average: 1/5/2 msec
├─ Connection Loss: 0
└─ RTT Summary: monitored continuously
```

### Alerting/Actions
```
Router(config)# ip sla react 1
Router(config-sla-react)# react value-type round-trip-time [which metric]
Router(config-sla-react)# threshold 50 [trigger if RTT > 50ms]
Router(config-sla-react)# action-type trap [send SNMP trap]

Triggered actions:
├─ SNMP trap to monitoring station
├─ Failover routing (with IP track objects)
└─ Page admin on severity level
```

---

## DNA Center Assurance

### Capabilities

```
1. Dashboard Health:
   ├─ Device CPU/memory/disk usage
   ├─ Interface status + errors/drops
   ├─ Application latency + throughput
   └─ Client experience (roaming, bandwidth)

2. Proactive Detection:
   ├─ ML anomaly detection (vs baseline)
   ├─ Predictive alerts (storage = full in 7 days)
   ├─ Root cause analysis (suggests likely issue)
   └─ Fixes recommendations (auto-remediation)

3. Encrypted Traffic Analytics (ETA):
   ├─ TLS flow analysis (no payload decryption)
   ├─ Behavioral pattern recognition
   ├─ App identification (Zoom, Teams without DPI)
   └─ Encrypted malware detection (C&C patterns)

4. Telemetry:
   ├─ Collection: Every 30-60 seconds from devices
   ├─ Processing: ML algorithms for pattern
   ├─ Visualization: Real-time dashboards
   └─ Retention: 1 month+ historical data
```

### DNA Center workflow example

```
Issue detected: Slow application response
        ↓
DNA Center correlates:
├─ Building X WiFi: User latency spike (normal 50ms → 500ms)
├─ AP density: 200 clients per AP (max 100 recommended)
├─ Interference: 2.4GHz channel 6 overlap with neighbor org
├─ WLC CPU: 75% utilization (normal 20-30%)
└─ WLAN policy: New rate-limiting applied today
        ↓
Root cause: AP overload + interference (not application)
        ↓
Recommendation:
├─ Adjust 5GHz band steering (force 5GHz clients)
├─ Change 2.4GHz channel to 11 (avoid overlap)
├─ Consider additional AP (split client load)
└─ Review new WLAN rate-limiting policy
        ↓
Operator action: Apply fixes → Performance restored
```

---

## Commandes CLI troubleshooting rapide

### Ping/Traceroute
```
# Standard diagnostics
ping 8.8.8.8                              [simple reachability]
ping -c 100 -s 1500 8.8.8.8               [MTU test + high count]
traceroute -n 8.8.8.8                     [path determination]

# Router extended (Cisco)
Router# ping
[Interactive mode for extended options]
```

### OSPF debug
```
Router# debug ip ospf adj                  [adjacency formation debug]
Router# debug ip ospf hello                [hello packet exchange]
Router# show ip ospf interface G0/0        [verify timers + network type]
Router# show ip ospf neighbor              [neighbor relationships summary]
```

### SPAN (Local example)
```
Switch# monitor session 1 source interface Gi0/1
Switch# monitor session 1 destination interface Gi0/48
Switch# show monitor session 1             [verify config]
```

### Flow monitoring
```
Router# show ip flow monitor TrafficMonitor cache [active flows]
Router# show ip flow exporter NetFlowCollector statistics [export stats]
```

---

## Performance baselines et tuning

### Ping latency expectations
```
Same LAN:            < 5 ms
WAN (100 miles):     10-50 ms
Intercontinental:    50-150 ms
Satellite:           300+ ms (geo return latency)
```

### OSPF convergence targets (RSTP)
```
Link failure detection:       < 1 second
SPF computation:              < 200 ms
Hello timeout (dead):         40 seconds default
Full adjacency restoration:   < 2-3 seconds (modern)
```

### NetFlow export intervals
```
Flow timeout timeout:         15 minutes (inactive)
Active timeout:               30 minutes (long-lived flows)
Export frequency:             60 seconds (typical, tunable)
Collector processing:         Near real-time (< 2 min delay)
```

### IP SLA thresholds recommendations
```
RTT latency:
├─ Critical threshold: > 100 ms
├─ Warning threshold: > 50 ms
└─ Normal range: < 20 ms

Packet loss:
├─ Critical: > 5%
├─ Warning: > 1%
└─ Normal: < 0.1%

Availability:
├─ SLA target: 99.9% uptime
├─ Test frequency: Every 60 seconds
└─ Monitoring: 24/7 continuous
```

---

## Ressources quick-ref
- **Ping timeout default**: 2 seconds
- **Traceroute max hops default**: 30 (configurable)
- **OSPF hello default**: 10 seconds (broadcast)
- **OSPF dead default**: 40 seconds (4 × hello)
- **NetFlow port default**: UDP 2055 or 9996
- **SPAN mirroring overhead**: ~10% bandwidth impact (may congestion if not monitored)
- **IP SLA sampling**: Synthetic traffic, non-production (doesn't affect real traffic)
- **DNA Center retention**: 1 month default (configurable longer)
- **VXLAN MTU impact**: 1554 bytes minimum (1500 payload + 54 VXLAN overhead)
