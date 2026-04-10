---
title: "Module 21: Dépannage de la connectivité sans fil"
module: 21
type: notes
topics: [wireless-troubleshooting, WLC, client-connectivity, signal-metrics, client-states, AP-troubleshooting]
difficulty: intermediate
updated: 2026-03-18
---

# Module 21: Dépannage de la connectivité sans fil

## Vue d'ensemble
Le dépannage sans fil exige une approche systématique: collecte des faits, test de la connectivité, enregistrement des résultats, puis diagnostic approfondissez. Ce module couvre les outils WLC GUI, les métriques client, les états de connexion, et les techniques de diagnostic des APs.

## Méthodologie de troubleshooting (Framework quatre étapes)

### Étape 1: Gather Facts (Collecte d'informations)
Avant tout diagnostic, assembler contexte complet:

**Questions clés:**
- Quand problème est apparu? (hier, cette semaine, au déploiement)
- Quel client affecté? (un seul, groupe, tous les devices)
- Quel AP/SSID? (spécifique ou aléatoire)
- Quel type problème? (connection impossible, slow, intermittent, disconnect)
- Client configuration? (SSID forgotten, date/heure incorrect, certificate expired)
- AP health? (signal, coverage, clientload)

**Sources d'information:**
- WLC dashboard (client counts, latency, air quality)
- AP metrics (radio utilization, channel interference)
- Client statistics (signal, rate, state)
- Network logs (authentication failures, DHCP issues)
- DNS/DHCP status (server reachability, scope exhaustion)

### Étape 2: Test Reachability (Test de connectivité)
Valider access layer connectivity via tools simplifié:

**Client-side tests:**
- Ping to gateway: ```ping <gateway-ip>``` → baseline latency
- DNS resolution: ```nslookup example.com``` → DNS working
- HTTP access: **curl** or browser check → upstream connectivity

**WLC-side tests (from device):**
- Ping to client: WLC dashboard → Client → Ping Test = 5 ICMP echo requests
- Trace client path: Mobility topology view = WLC → AP → Client
- Validate VLAN: Vérifier client VLAN matches policy expected

### Étape 3: Record Outcome (Enregistrement des résultats)
Documenter findings pour analyse comparative:

- **Success**: "Client X connected, signal -45dBm, rate 144 Mbps, score 95%"
- **Failure**: "Client X association fail, Error 31 (Unsupported Auth Type)"
- **Intermittent**: "Client X disconnects every 2-3 minutes during data transfer"

### Étape 4: Further Diagnosis (Diagnostic approfondi)
Si étapes 1-3 ne résolvent:
- Escalade device/network logs
- Capture packet via SPAN/RSPAN
- ISE policy review (EAP failures, posture blocks)
- AP radio diagnostics (interference, coverage prediction)

---

## Accès et navigation WLC GUI

### Connexion WLC Dashboard
```
1. Browser: https://<WLC-management-ip> [port 8443 default HTTPS]
2. Credentials: admin / password [local ou RADIUS authenticated]
3. Landing page: Dashboard = real-time WLC status
   ├─ Client count (connected/authenticated)
   ├─ APs connected (healthy/degraded)
   ├─ Air quality metrics (interference, load)
   └─ Recent events (client events, AP drops)
```

### Client Search et Client View

#### Recherche client par MAC address
```
WLC GUI → Client → Search
├─ Input: MAC address = XX:XX:XX:XX:XX:XX [format]
│  └─ Example: 78:4b:87:7b:af:96
├─ [Search button]
└─ IF found → Auto-load Client View screen
   IF not found → "Client not associated" message = offline
```

#### Client View écran principal
Écran divisé gauche/droite affichant détails client complets:

**Panneau gauche (General Information):**
```
Hardware Information
├─ Client MAC Address: XX:XX:XX:XX:XX:XX
├─ Hostname: [device name if registered]
├─ Client Type: [MacOS|Windows|iOS|Android|Linux|Other]
├─ OS Version: [if detected]
├─ Client IP Address: [currently assigned]
└─ Associated AP: [AP hostname/IP # radio]

Session Information
├─ SSID: [wireless network name]
├─ Authentication Alias: [username if 802.1x, empty if PSK]
├─ Connection State: [Start|Association|Authentication|DHCP|Online]
├─ Session Time: [duration connected]
├─ Last Session Time: [previous connection duration]
└─ Current Uptime: [session start]

IPv6 Information (if applicable)
├─ IPv6 Address: [if assigned]
└─ IPv6 Link-Local: [fe80:: prefix]
```

**Panneau droite (Connectivity & Performance):**
```
Connected AP Information
├─ AP MAC: [physical radio MAC]
├─ BSSID: [same as AP MAC]
├─ Channel: [frequency + width | ex: 5180 MHz @ 20MHz]
├─ Radio Class: [a|b|g|n|ac|ax]
├─ Max Data Rate: [theoretical max | ex: 144 Mbps (802.11ac)]
└─ Signal Strength Details [voir section below]

Network Performance Metrics
├─ Real-time Data Rate: [actual current rate]
├─ Sent Bytes / Received Bytes: [traffic statistics]
├─ TX/RX Packets
└─ Connection Score: [0-100% | voir interpretation]

Policy Summary
├─ Wireless Policy: [policy name applied]
├─ VLAN: [assigned vlan #]
├─ QoS Level: [platinum|gold|silver|bronze]
└─ Security Policy: [WPA2-PSK|WPA3|802.1x|None]

Application Info (Optional)
├─ [Application usage if DPI enabled]
├─ Traffic category breakdown
└─ [Helpful for QoS troubleshooting]
```

---

## Métriques signal et performance

### Signal Strength (dBm interpretation)

**Définition dBm**: Décibels relative 1 milliwatt (logarithmique)
- **Positive values**: Impossible radio (≥0 dBm = physically impossible)<br/>
- **Negative values**: Standard RF representation (-30 to -100 dBm typical)

#### Tableau référence dBm signal levels

| dBm Range | Quality | Description | Action |
|-----------|---------|-------------|--------|
| **-30 to -50** | Excellent | Very strong signal, max rate capability | None, ideal |
| **-50 to -70** | Good | Good signal, minimal packet loss | Acceptable for most use |
| **-70 to -85** | Fair | Weaker signal, rate reduction possible | Monitor, potential roaming issues |
| **-85 to -100** | Weak | Poor signal, high loss/retransmission | Issue, consider AP placement |
| **< -100** | Critical | Unusable connection, frequent disconnects | Problem - move closer or reposition AP |

**Exemple WLC view**: "Signal Strength: -76 dBm" = Between fair/weak range, potential issues if sustained.

### SNR (Signal-to-Noise Ratio)

**Définition SNR**: Ratio signal power vs noise floor Power (dB linear ratio)
- Formula: SNR = Signal<sub>dBm</sub> - Noise<sub>dBm</sub> (décibels, not linear)
- Higher SNR = cleaner signal = better throughput

#### Tableau référence SNR

| SNR (dB) | Quality | Interpretation |
|----------|---------|---------|
| **> 40 dB** | Excellent | Very clean signal, no interference |
| **30-40 dB** | Good | Clean signal, minimal noise |
| **20-30 dB** | Fair | Some noise, noticeable impact rate |
| **15-20 dB** | Weak | Significant noise, rate reduction ~50% |
| **10-15 dB** | Poor | High noise, connection unstable |
| **< 10 dB** | Critical | Unusable, frequent drops |

**Exemple**: WLC shows "SNR: 18 dB" = Low fair range, not optimal, consider coverage investigation.

### Data Rate (Mbps)

**Représentation**: Actual PHY rate where client currently transmitting
- **Negotiation**: Rate set dynamically based signal/noise conditions (rate adaptation)
- **Factors affecting**: Signal strength, SNR, channel bandwidth, 802.11 standard (n/ac/ax)

#### Exemples rates par standard:

- **802.11n (2.4 GHz, 20 MHz)**: Up to 72 Mbps
- **802.11n (5 GHz, 40 MHz)**: Up to 300 Mbps
- **802.11ac (5 GHz, 80 MHz)**: Up to 867 Mbps (3 spatial streams)
- **802.11ax (2.4+5 GHz, 80/160 MHz)**: Up to 4.8 Gbps (theoretical)

**Observation troubleshooting**:
- Rate drops progressively → signal issue (client moving away, interference)
- Rate stable but low (ex: 6 Mbps) → WLC rate limiting, AP class rate setting (see advanced config)

### Connection Score (Composite metric)

**Formula**:
$$\text{Connection Score} = \frac{\text{Actual Data Rate}}{\text{Max Data Rate}} \times 100\%$$

**Exemple calculation**:
- Client actual rate: 29 Mbps
- Client max capable rate: 144 Mbps (802.11ac 1ss)
- Connection Score: (29 ÷ 144) × 100 = **20%**

#### Interprétation Connection Score

| Score % | Assessment | Likely Cause | Action |
|---------|-----------|--------|---------|
| **90-100%** | Excellent | Ideal conditions | None required |
| **70-89%** | Good | Minor signal degradation | Monitor |
| **50-69%** | Fair | Moderate signal/interference | Investigate signal |
| **20-49%** | Poor | Significant signal issue or rate limiting | Review AP placement or QoS config |
| **< 20%** | Critical | Severe connectivity issue | Immediate diagnosis needed |

**Considération**: Low score NOT always client fault - può WLC QoS class rate limit intentional (ex: guest vlan = max 5 Mbps).

---

## États de connexion client (State machine)

### État progression diagram
```
[Start] 
   ↓
[Association] ← (802.11 auth + association success)
   ↓
[Authentication] ← (WPA2-PSK 4-way / WPA3-SAE / 802.1x EAP success)
   ↓
[DHCP] ← (IP assignment via DHCP)
   ↓
[Online] ← (fully authorized, can transmit data)
```

### Détails état-par-état

#### État 1: Start
- **Contexte**: Client recent association attempt initiated, not yet associated
- **Durée typique**: < 1 second (rapide transition)
- **Observation troubleshooting**: Si stuck > 2s = association issue (wrong SSID, AP not broadcasting, channel mismatch)

#### État 2: Association
- **Contexte**: Client has exchanged 802.11 association frames with AP
- **Frames**: Association Request (client) → Association Response (AP)
- **Status bits**: AP capabilities negotiation (rate, channels support)
- **Durée typique**: Milliseconds (très rapide)
- **Issue si stuck**: AP rejecting association (BSSID not found, wrong band/channel, AP capacity full)

#### État 3: Authentication
- **Contexte**: Client undergoing security authentication method
- **Sub-flows**:
  - **PSK mode**: 4-Way Handshake in progress
  - **802.1x mode**: EAP exchange with RADIUS ongoing
  - **WPA3-SAE**: Dragonfly sequence underway
- **Durée typique**: 1-5 seconds (depending EAP type)
- **Issue si stuck**: Security mismatch (client expects WPA3, AP only WPA2), EAP timeout, RADIUS unavailable

#### État 4: DHCP
- **Contexte**: Client obtained IP address, acquiring network configuration
- **DHCP process**: DISCOVER → OFFER → REQUEST → ACK
- **Durée typique**: 1-3 seconds (depends DHCP server responsiveness)
- **Issue si stuck**: DHCP server down, DHCP vlan mismatch (DHCP server not on client vlan), DHCP scope exhausted

#### État 5: Online
- **Contexte**: Client fully authenticated + has IP, authorized to transmit data
- **Traffic capable**: Can ping gateway, DNS query, web browsing
- **Durée**: Duration of connection/session
- **Transition out**: Client disassociation (explicit or watchdog timer)

### État diagnostique WLC GUI
```
WLC Client View → Connection State: [showing current state]
├─ IF Online: "Uptime: XX hours YY min" = normal operation
├─ IF stuck state > 60s: TAC log likely contains failure reason
└─ Retrigger association: [Re-Connect button] to restart state machine
```

---

## Topologie mobilité (Mobility Topology)

### Vue hiérarchique
```
WLC Controller
├─ Name: [WLC hostname]
├─ IP: [management IP]
├─ Model: Catalyst 9800-40 (example)
└─ Status: [Ready|Busy]
   ↓
   Access Point (serving client's connection)
   ├─ AP Name: [AP-name-building]
   ├─ AP IP: [AP management IP]
   ├─ AP Model: [Catalyst 9115]
   └─ Radio: [802.11a (5GHz bande) | 802.11g (2.4GHz bande)]
      ↓
      Client Endpoint
      ├─ Client MAC: [XX:XX:XX:XX:XX:XX]
      ├─ Client hostname/device type
      ├─ Assigned IP: [xxx.xxx.xxx.xxx]
      ├─ VLAN: [vlan number]
      └─ Status: [Connected|Roaming|Disconnected]
```

**Utilitère**: Voir immédiatement AP serving client, déterminer AP position géographiquement, examine VLAN assignment.

---

## Politiques sans fil (Wireless Policies)

### Éléments politique détails

#### Paramètres réseau
```
IP Address Configuration:
├─ IP Lease Mode: [DHCP|Static] (typically DHCP)
├─ IP: [currently assigned | shows DHCP lease]
├─ Subnet Mask: [/24 typical]
├─ Default Gateway: [vlan gateway IP]
├─ DNS Servers: [primary/secondary DNS IPs]
└─ DHCP Server Details: [which DHCP serving client's vlan]
```

#### Paramètres VLAN et QoS
```
VLAN Assignment:
├─ VLAN ID: [numeric | ex: 100]
├─ VLAN Name: [descriptive | ex: Corporate]
└─ Dynamic VLAN: [IF enabled, RADIUS can override per-user]

Quality of Service:
├─ QoS Policy Applied: [Policy Name]
├─ QoS Queue Level: [platinum|gold|silver|bronze]
├─ Priority Queue: [mapped to 802.1p priority levels]
├─ Bandwidth Allocation: [% or Kbps cap if configured]
└─ Rate Limiting: [CIR/PIR if shaping enabled]
```

#### Paramètres sécurité
```
Security Configuration:
├─ Security Policy: [WPA2-Personal|WPA2-Enterprise|WPA3-Personal|Open]
├─ Encryption Cipher: [CCMP-AES|TKIP|None]
├─ Authentication Method: [PSK|802.1x|WebAuth|None]
├─ Management Frame Protection (MFP): [Optional|Required|Disabled]
├─ Roaming Assist: [Fast Roaming enabled|disabled]
└─ IP Filtering: [IF enabled, client = restricted IP destinations]
```

### Vérification policy WLC
```
WLC GUI → Client → [Select client] → Wireless Policy
├─ Review toutes sections above
├─ Validate VLAN = expected access tier
├─ Validate QoS = expected for user group
├─ Validate Encryption = configured WLAN encryption
└─ IF policy not matching expectations:
   ├─ RADIUS attribute assignment wrong (ISE policy issue)
   ├─ VLAN not properly defined on WLC
   └─ Or client may need re-auth to pick up new policy
```

---

## Outils diagnostic client WLC

### 1. Ping Test (Reachability ICMP)

#### Configuration exécution
```
WLC Client View → Client Tools → Ping Test
├─ Source: [Auto select = WLC as source]
├─ Destination: [Target IP | default = client's gateway]
├─ Packet Count: [5 default | configurable]
├─ Packet Size: [100 bytes default | 1500 for MTU test]
├─ Timeout: [2 seconds standard]
└─ [Execute]
```

**Résultat output:**
```
Ping Test Results:
├─ 5 packets sent to <destination-ip>
├─ Responses:
│  ├─ "5/5 successful" = ✓ Client can reach destination
│  ├─ "3/5 successful" = ⚠ Intermittent loss
│  └─ "0/5 successful" = ✗ No reachability (routing/firewall)
├─ Round-Trip Time (RTT): [min/avg/max milliseconds]
│  └─ Example: "min=1ms, avg=2ms, max=5ms"
└─ [If MTU test (size 1500), check ICMP fragmentation]
```

### 2. Connection Test (Dynamic 3-minute probe)

#### Utilitère détail
Connection Test goes beyond simple ping: teste complet WPA2 authentication flow + DHCP + application connectivity durant 3 minutes.

```
WLC Client View → Client Tools → Connection Test
├─ Objective: Deep diagnostic authentication + network access
├─ Duration: 3 minutes continuous monitoring
├─ Metrics captured:
│  ├─ EAP/PSK authentication success/failure
│  ├─ DHCP IP acquisition success/failure
│  ├─ Gateway ping success (application reachability)
│  ├─ SNR stability over 3 minutes
│  ├─ Rate stability/changes
│  └─ Roaming behavior if client moves
└─ [Execute]

Result Summary:
├─ Test Status: [Pass|Fail]
├─ Authentication Result: [Success|Timeout|Wrong Key|Unsupported Auth]
├─ DHCP Result: [Success|Timeout|NACK]
├─ Internet Reachability: [Success|Failure]
└─ Stability Score: [0-100%]
```

### 3. Event Log (Detailed join history)

#### Analyse événement
```
WLC Client View → Client Tools → Event Log
├─ Timeline: [Shows all events for client session]
├─ Event types captured:
│  ├─ [Timestamp] Client Associated to AP
│  ├─ [Timestamp] EAPOL Started (if 802.1x)
│  ├─ [Timestamp] 4-Way Handshake Completed (if WPA-PSK)
│  ├─ [Timestamp] DHCP Discover Sent
│  ├─ [Timestamp] DHCP ACK Received [IP assigned]
│  ├─ [Timestamp] QoS Initialized
│  └─ [Timestamp] Client Roaming to AP-B
├─ TAC (Technical Assistance Center) Info:
│  └─ Detailed error messages if join failed (ex: "EAPOL timeout waiting msg 3 of 4")
└─ [Export to file for offline analysis]
```

### 4. Packet Capture (Wireshark-compatible PCAP)

#### Capture exécution
```
WLC Client Tools → Packet Capture
├─ Source: [Client MAC]
├─ Destination: [Optional filter | default = all traffic]
├─ Duration: [5-60 seconds | default 10]
├─ Frame Limit: [limit packets captured | default unlimited]
└─ [Start Capture]

Post-capture Actions:
├─ [Download PCAP file] → transfer FTP/SFTP to workstation
├─ Open Wireshark: File → Import → [select .pcap]
├─ Analysis:
│  ├─ Filter "eapol" to inspect 4-way handshake frames
│  ├─ Filter "dhcp" to inspect DHCP four-way exchange
│  ├─ Filter "icmp" to inspect ping/probe traffic
│  └─ Inspect packet details (ICV, MIC, encryption)
└─ [Decode expected behavior vs actual]
```

---

## Dépannage AP et couverture radicale

### Diagnostic AP-level

#### Symptômes indicateurs problème AP
```
Scenario 1: Multiple users same area report slow/disconnect
├─ Probléma likelyhood: [HIGH] = AP issue, not individual client
├─ Diagnostique:
│  ├─ Check AP CPU/memory utilization via WLC
│  ├─ Check AP client count (capacity exceeded?)
│  ├─ Check AP channel utilization (interference?)
│  ├─ Verify AP radio status (enabled, not crashed)
│  └─ Check temperature (thermal throttling?)
├─ Resolution:
│  ├─ Reboot AP if hung
│  ├─ Adjust client load balancing (band steering, AP limits)
│  ├─ Change channel if interference detected
│  └─ OR replace AP if radio defect

Scenario 2: Specific radio band all clients weak signal
├─ Problem: Defective radio, antenna disconnected, or RF path issue
├─ Action:
│  ├─ ISE radio details: Power level, antenna status
│  ├─ Visual inspect antenna connections, cables
│  ├─ Test AP at different location
│  └─ Replace radio or AP if confirmed defect
```

### Coverage prediction model
```
Coverage Challenges:
├─ Obstruction (walls, metal) → Signal attenuation
├─ Distance (path loss) → Signal drops ~6dB per doubling distance (free space)
├─ Interference (co-channel, adjacent) → SNR degradation
└─ Multipath (reflections, bounces) → Fading

Design mitigation:
├─ AP density: ~30m coverage (outdoor), ~15m (dense indoor)
├─ Channel planning: Minimize overlap 5GHz (36-48 non-overlapping)
├─ Power optimization: Not always max power (can create overlap/interference)
├─ Placement: Elevated, centralized (avoid walls between AP/client)
└─ Validation: Site survey tools (Ekahau, AirMagnet) for coverage heatmaps
```

---

## Points clés à retenir

### Framework troubleshooting
1. **Gather facts**: Timeline, scope, environment context
2. **Test reachability**: Ping, trace, access verification
3. **Record outcome**: Document findings for comparison
4. **Further diagnosis**: Escalate if needed (packet capture, ISE logs, AP diagnostics)

### Métriques interprétation
- **-30 dBm**: Excellent; **-70 dBm**: Acceptable; **-85 dBm**: Poor
- **SNR 30+ dB**: Good; **< 15 dB**: Weak
- **Connection Score > 70%**: Healthy; **< 50%**: Investigate
- **Signal trends**: Gradual drop = roaming issue; abrupt = AP problem

### Client state diagnostique
- **Stuck Association**: AP association failure, SSID/channel mismatch
- **Stuck Authentication**: PSK wrong, EAP timeout, RADIUS unavailable
- **Stuck DHCP**: Server down, vlan mismatch, scope exhausted
- **Frequent reconnects**: Roaming threshold too aggressive, poor SNR

### Outils utilisation
- **Ping Test**: Quick baseline reachability
- **Connection Test**: Deep 3min authentication + DHCP flow
- **Event Log**: Detailed timeline for root cause analysis
- **Packet Capture**: Deep packet inspection (handshake, protocol issues)
- **Mobility Topology**: Show AP location, VLAN assignment quickly

---

## Ressources complémentaires
- Cisco WLC CLI reference (show client, show ap, debug commands)
- Wireshark wireless dissectors (802.11, EAP, DHCP)
- Ekahau Pro (site survey, interference prediction)
- ISE troubleshooting logs (EAP failure reasons, CoA status)
