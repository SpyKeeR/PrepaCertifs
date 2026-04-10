---
title: "Checkpoint Exam CP8: Wireless Authentication & Troubleshooting (50 questions)"
checkpoint: CP8
modules: [20, 21]
type: checkpoint
topics: [wireless-auth, troubleshooting, PSK, 802.1x, WLC, client-connectivity]
difficulty: advanced
exam_level: certification
time_limit: 90
passing_score: 35
updated: 2026-03-18
---

# Checkpoint CP8: Authentification sans fil & Dépannage (50 questions)

## Examen de certification rigoureux - Niveau expert CCNP ENCOR

**Format:** 50 questions à 4 réponses | Durée: 90 minutes | Passing: 70% (35/50)
**Rubrique:** 90-100%=mastery, 80-89%=strong, 70-79%=passing, <70%=review needed

---

## Section A: Authentification sans fil (Q1-25)

### **Q1: Open Authentication Deployment**

Organisation publique demande WLAN accès sans mot de passe. Configuration GUI WLC?

A) WLAN → Security → Layer 2 = None, puis DHCP auto-assign
B) WLAN → Authentication → Open Mode with portal backup
C) WLAN → Interface = Management, Security = Disabled
D) WLAN → Create with SSID, Security tab = None, Apply VLAN

**Réponse: D** - Configuration correcte Layer 2=None + VLAN assignment

---

### **Q2: WPA2-PSK Configuration Details**

Client WPA2-PSK fails authentication avec message "4-Way Handshake timeout". PSK config WLC montre "abcde12345" (10 caractères ASCII). Problème?

A) PSK trop court (minimum 12 caractères recommended)
B) PSK format doit être hexadécimal (64 caractères, pas ASCII)
C) PSK correct, issue = client WPA version mismatch (client = WPA, AP = WPA2)
D) PSK correct, issue = CCMP cipher not supported by legacy client

**Réponse: A** - PSK 10 chars acceptable (8-63 minimum), mais trop faible pour sécurité (brute-force feasible 10!)

---

### **Q3: SAE Dragonfly Features**

WPA3-Personal déploiement demande forward secrecy. Quel mécanisme WPA3 fournit?

A) 4-Way Handshake avec PTK rotation per-packet (vs per-session)
B) SAE Dragonfly protocol = clés dérivées fresh per-connection (isolation sessions)
C) TKIP encryption (rotating keys automatically)
D) Certificate-based authentication (like 802.1x, but simplified)

**Réponse: B** - SAE forward secrecy = per-session key derivation (unique clés chaque connexion/roam)

---

### **Q4: RADIUS Server Failover**

WLC configured:
- Primary RADIUS: 10.50.50.50 (active)
- Secondary RADIUS: 10.50.50.51 (standby)

Primary server down. Client authentication behavior?

A) Client stuck (no failover, manual reconfiguration needed)
B) WLC tries primary 3×, then failover secondary automatiquement
C) Client must re-authenticate to trigger secondary attempt
D) Both [B] and [C] - depends device capability

**Réponse: B** - WLC automatic failover after timeout/retries (transparent to client)

---

### **Q5: 802.1x vs PSK Security Model**

Enterprise ambiente (500 users) decide 802.1x deployment. Key advantage over PSK?

A) Faster client connection (PSK slower)
B) Per-user accountability + granular policies (vs shared PSK key)
C) Cheaper (no ISE/RADIUS license fees required)
D) Simplr configuration (less WLC setup)

**Réponse: B** - 802.1x = per-user identity (audit trail, context-aware policies)

---

### **Q6: EAP Method Selection**

ISE administrator chooses EAP method for certificate + password hybrid auth. Best choice?

A) EAP-TLS (mutual cert validation)
B) EAP-PEAP (server cert, client password in TLS tunnel)
C) EAP-MD5 (simple, no infrastructure needed)
D) EAP-FAST (lightweight, best performance)

**Réponse: B** - EAP-PEAP = cert server + password client = hybrid balance (security + usability)

---

### **Q7: 4-Way Handshake Attack Resistance**

Hacker sniffs 4-Way Handshake frames off-air. Can derive PMK/PSK?

A) Yes (computational effort feasible 48 hours)
B) No (MIC validation requires correct keys, no offline attack)
C) Yes (Wireshark automatic decryption if weak PSK)
D) Partially (only if PSK < 10 characters)

**Réponse: B** - MIC (Message Integrity Code) prevents offline dictionary brute-force (key required validation)

---

### **Q8: WebAuth vs PSK - Use Cases**

Guest VLAN needs rapid access (no credential installation). Recommended auth method?

A) WPA2-PSK (simple password shared all guests)
B) 802.1x + EAP (certificate provisioning)
C) WebAuth (portal login, no pre-config)
D) Open + MAC filtering (simple MAC-based ACLs)

**Réponse: C** - WebAuth = zero pre-config, portal login (ideal guest experience)

---

### **Q9: RADIUS & WLC Integration Error**

WLC configured RADIUS server 10.50.50.50 shared secret "MySecret". ISE same shared secret configured. Client 802.1x fails. Diagnostic?

A) WLC RADIUS port 1812, ISE port 1813 (mismatch)
B) Shared secret correct, issue = RADIUS server IP routing unreachable from WLC
C) WLC AAA Servers tab not assigned to WLAN (configuration incomplete)
D) ISE posture policy blocking client (device health check failed)

**Réponse: C** - WLC create WLAN → Security → 802.1x methode chosen, PUIS AAA Servers tab assign RADIUS

---

### **Q10: PSK Rotation Best Practice**

PSK "CompanyWifi2024!" shared IT office. Change frequency recommendation?

A) Never (static PSK acceptable indefinitely)
B) Every 12 months (annual rotation)
C) Every 90 days (quarterly rotation)
D) Weekly (high-security environments)

**Réponse: C** - Industry standard = 90 days rotation (balances security + administrative burden)

---

### **Q11: Client State Machine - "Authentication" Stuck**

Client state shows "Authentication" > 10 seconds (normal 1-5 sec). Probable causes?

A) Signal too weak (client can't hear 4-Way frames)
B) PSK mismatch OR RADIUS server timeout OR EAP credential wrong
C) DHCP server unavailable (blocking DHCP state)
D) AP radio failure (customer can't hear AP)

**Réponse: B** - Authentication state = PSK handshake or EAP exchange (RADIUS reachability crucial)

---

### **Q12: Management Frame Protection 802.11w**

MFP disabled. Attacker sends spoofed deauth frames. Client impact?

A) No impact (deauth frames ignored automatically)
B) Client disconnects (deauth effective, must re-authenticate)
C) Client roams (deauth treated as signal weakness)
D) Network breakdown (cascade disconnections)

**Réponse: B** - MFP disabled = deauth unprotected (attacker can force disconnect, DoS attack)

---

### **Q13: WLAN Encryption Cipher Hybrid**

WLAN configured WPA Version = "WPA2/WPA3" (transition mode). Client WPA2 only. Encryption?

A) Client uses CCMP-AES WPA2 cipher
B) Client upgraded WPA3 automatically (not possible)
C) Connection fails (incompatible versions)
D) Cipher negotiated per-client (AES vs CCMP dynamic)

**Réponse: A** - Transition mode = mixed (WPA2 clients = CCMP, WPA3 = CCMP + enhanced)

---

### **Q14: Client Blacklist Cause & Prevention**

Client MAC 00:11:22:33:44:55 repeatedly fails authentication (wrong PSK entered = 10+ attempts). WLC action?

A) Automatic blacklist after 3 failures
B) Manual blacklist via show client blacklist command
C) Auto-removal blacklist after 30 minutes
D) Both [A] and automatic removal [C]

**Réponse: A** - WLC auto-blacklists after threshold failures protect brute-force attacks

---

### **Q15: SSID Broadcast vs Hidden**

Hidden SSID deployment (security by obscurity). 802.1x authentication bypass?

A) No (authentication happens regardless SSID visibility)
B) Yes (hidden SSID = weaker security requirement)
C) Partial (client must enter SSID manually, harder disassociate)
D) Not applicable (SSID broadcast ≠ authentication layer concern)

**Réponse: D** - SSID broadcast = discovery only (authentication Layer 2 independent)

---

### **Q16: Local EAP Server Option**

WLC supports local EAP server (without external RADIUS ISE). Scenario deployment?

A) Small organization, no ISE license, simple user@password database
B) WAN-connected branch office (latency critical RADIUS reach remote HQ)
C) Multi-site federated authentication (RADIUS not suitable)
D) Temporary fallback (ISE down, need emergency auth)

**Réponse: D** - Local EAP = fallback only (limited functionality vs full ISE/RADIUS)

---

### **Q17: Captive Portal Redirect Mechanism**

WebAuth configured. Client associates WLAN, DHCP assigned 10.1.1.50. How redirected portal page?

A) DNS-based (client's DNS queries redirected login page)
B) DHCP Option 150 (WLC IP pushed to client)
C) HTTP 302 redirect (any web request intercepted)
D) All [A] [B] [C] - multiple methods (devices choose)

**Réponse: D** - Multiple redirect mechanisms (DNS, DHCP, HTTP) coexist (device compatibility)

---

### **Q18: PSK Character Strength Analysis**

Three PSK options. Which MOST resistant brute-force?

A) "12345678" (8 numeric)
B) "MyWifi2024" (mixed case + numeric, 10 char)
C) "MyWifi2024@#$%&" (mixed case + special, 16 char)
D) "abcdefgh" (8 lowercase)

**Réponse: C** - Entropy = character set × length (special chars = 94 possible per position, longer = better)

---

### **Q19: Roaming between APs - VLAN Consistency**

Client roams AP-A → AP-B (different APs, same WLC). Both APs transmit SSID = "Corporate" VLAN = 100. Client impact?

A) IP address preserved (same VLAN = same subnet)
B) DHCP re-request (may get different IP same subnet)
C) Layer 2 key renegotiation (fast roaming 802.11r if enabled)
D) All above [A] [B] [C] possible

**Réponse: D** - Roaming = no VLAN change (IP preserved or re-dhcp same subnet), 802.11r = faster auth

---

### **Q20: EAP-TLS Certificate Failure**

Client EAP-TLS failing "Certificate verification failed" error. Root cause?

A) Client certificate expired (verify date validation)
B) Server certificate (WLC/ISE) untrusted (client trust store missing root CA)
C) Certificate chain incomplete (intermediates missing)
D) All [A] [B] [C] possible

**Réponse: D** - EAP-TLS mutual cert validation requires BOTH sides valid + trusted

---

### **Q21: PMK (Pairwise Master Key) Derivation**

PMK = function of what input parameters (WPA2-PSK)?

A) PSK + SSID (via PBKDF2 4096 iterations, RFC 3962)
B) PSK alone (pure hash)
C) PSK + client MAC address
D) Dynamically generated per-session (no PSK)

**Réponse: A** - PBKDF2 (Password-Based Key Derivation Function) = PSK + SSID (slowing brute-force)

---

### **Q22: EAPOL Frame Types in 4-Way**

Which EAPOL frame type used 4-Way Handshake?

A) EAP packets (Type 0)
B) EAP-Key (Type 3, EAPOL-Key frames)
C) Logoff (Type 2, termination)
D) Both [A] and [B]

**Réponse: B** - EAPOL-Key frames = Type 3 (Key Exchange messages)

---

### **Q23: Mobility Anchor Concept**

WLC deployment distributed (Dist-A = primary WLC, Dist-B = secondary). Client roams between WLCs. Mobility anchor role?

A) Primary WLC tunnels client traffic (even if secondaire AP chosen)
B) Load balanced (traffic optimal per AP WLC)
C) Fallback only (secondary takes over if primary down)
D) Irrelevant (client disconnects WLC change)

**Réponse: A** - Mobility Anchor = client maintains tunnel primary WLC (seamless roaming)

---

### **Q24: Shared Network Secret Exposure Risk**

PSK "WifiPassword123" logged in WLC syslog message (clear text). Risk?

A) No risk (syslog typically encrypted TLS)
B) High risk (capture syslog = PSK compromise)
C) Medium risk (attacker needs network access + WLC IP)
D) No difference (PSK always at risk over WLAN)

**Réponse: B** - Syslog security-critical (must TLS encrypt if containing credentials)

---

### **Q25: Scenario Exam - Multi-Problem Diagnosis**

Client cannot connect WLAN "CorpNet":
- Several other clients on CorpNet: OK
- Same client OK on "GuestNet" (open auth)
- WLC Ping Test client: Fails (0/5)
- Client MAC: AA:BB:CC:DD:EE:FF

Diagnostic steps order?

1) Verify SSID broadcast (CorpNet exists)
2) Check client blacklist (show client blacklist)
3) Test PSK (reenter password client)
4) Verify DHCP reachability
5) Check RADIUS server online

A) 3 → 2 → 1 → 5 → 4 (top-down credential first)
B) 1 → 2 → 3 → 5 → 4 (basics first)
C) 2 → 3 → 5 → 1 → 4 (blacklist/PSK/RADIUS critical)
D) 5 → 1 → 2 → 3 → 4 (RADIUS/SSID/blacklist/PSK/DHCP)

**Réponse: B** - 1→2→3→5→4: Start basics (SSID exists), then blacklist, PSK, RADIUS, DHCP

---

## Section B: Troubleshooting sans fil (Q26-50)

### **Q26: Client Signal Analysis - Rate Adaptation**

Client dBm = -65 (good signal range). Yet rate = 6 Mbps (minimum basic rate, not 100+ Mbps 802.11ac capable). Why?

A) 802.11a/b/g legacy device (doesn't support 802.11ac)
B) WLC QoS class rate-limiting (bandwidth cap per-user policy)
C) Signal adequate but noise nearby (SNR bad = rate adaptation down)
D) Client RTS/CTS enabled (protection mode = lower throughput)

**Réponse: B or C** - Good signal NOT guarantee max rate (QoS/noise separate factors)

---

### **Q27: SNR vs dBm - Independent Metrics**

Client metrics:
- Signal: -60 dBm (excellent by dBm scale)
- SNR: 8 dB (poor by SNR scale)

Client actual experience likely?

A) Perfect (signal excellent)
B) Good (dBm overrides SNR)
C) Poor (SNR = limiting factor, high noise interference)
D) Can't determine (conflicting metrics irrelevant)

**Réponse: C** - SNR = rate-limiting factor (high noise despite strong signal = suboptimal rates)

---

### **Q28: Connection Score Interpretation Scenario**

Client score = 15% (actual 21.6 Mbps, max 144 Mbps). User reports "videos buffering". Troubleshoot action?

A) Blame ISP (external internet issue)
B) Check AP signal/interference (local WLAN issue likely)
C) Configure QoS (rate-limiting customer benefit)
D) Upgrade client to 802.11ax (solve hardware limitation)

**Réponse: B** - 15% score = WLAN signal/interference issue (local troubleshooting first)

---

### **Q29: Client State Transition Timing**

Client state progression observed:
```
[12:00:00] Start → Association [12:00:01] ✓
[12:00:01] → Authentication [12:00:05] ✓
[12:00:05] → DHCP [12:00:06]
[12:00:20] → Still DHCP (stuck 15 seconds!)
```

Root cause most likely?

A) PSK/EAP issue (Authentication OK = rules out)
B) DHCP server IP address not in client vlan scope
C) DHCP server not responding (down/unreachable)
D) Both [B] and [C]

**Réponse: D** - DHCP stuck = server down OR mismatch (not vlan)

---

### **Q30: Event Log TAC Information**

Event Log displays:
```
[Timestamp] 802.1x Authentication Failed: RADIUS Access-Reject
Additional info: EAP-PEAP: TLS Certificate verification failed
```

Cause?

A) User credentials wrong (username/password incorrect)
B) ISE/RADIUS server certificate untrusted (client trust store missing)
C) Client certificate expired (if mutual auth)
D) All above possible

**Réponse: B** - EAP-PEAP TLS cert issue = server cert validation (not user credentials)

---

### **Q31: AP Health Check - Multiple Users Affected**

Building X (20 users, AP-A) ALL slow simultaneously. Building Y (30 users, AP-B) normal. What check priority?

A) Individual client issues (wrong device types)
B) AP-A CPU/memory utilization (health metrics)
C) AP-A channel interference check (spectrum analysis)
D) Both [B] and [C]

**Réponse: D** - AP health + interference chief suspects (multiple users = AP issue)

---

### **Q32: Roaming Test - Client Moves between APs**

Client walks around building (AP-A → AP-B → AP-C). Connection interrupted:
```
[Time] AP-A signal -45dBm rate 100 Mbps
[+5sec] AP-B signal -40dBm rate 120 Mbps (roaming inprogress)
[+8sec] Disconnected! ("connection lost")
[+10sec] AP-C associated -50dBm rate 100 Mbps Online
```

Roaming issue diagnosis?

A) Overlapping channels (AP-B should have better signal, unexpected)
B) 802.11k/v/w not enabled (slow handoff, connection lost)
C) AP-B temporarily out of service (brief unavailability)
D) Client device weak roaming support (legacy 802.11n)

**Réponse: B** - Disconnection during roam = slow handoff (802.11k=neighbor report, 11v=transition, 11w=FT needed)

---

### **Q33: Packet Capture EAPOL Analysis**

Wireshark capture EAPOL frames:
```
Frame 1: EAPOL Key (Msg 1, AP→Client)
Frame 2: EAPOL Key (Msg 2, Client→AP) ✓
Frame 3: [MISSING - no Msg 3 reply]
Frame 4+: Timeout, retry Msg 1
```

Result?

A) Client decryption issue (can't read Msg 1)
B) Client can't derive PTK (wrong PSK)
C) Client not responding (crashed hardware)
D) Network congestion (Msg 3 lost in transit)

**Réponse: B** - Msg 2 success = received M1 + derived PTK. No M3 = AP rejected M2 (MIC mismatch = wrong PSK)

---

### **Q34: WLC Bandwidth Policy Check**

QoS policy "Gold" assigned guest user. However, iperf throughput = 2 Mbps (vs expected 100 Mbps). WLC settings check?

A) Confirm Gold policy bandwidth cap (show qos policy Gold)
B) Check per-user bandwidth limit (not per-policy)
C) Verify interface uplink capacity (WLC → distribution)
D) All [A] [B] [C] valid

**Réponse: D** - Throughput limited by policy cap / per-user limit / interface bottleneck

---

### **Q35: Client Search Case Sensitivity**

WLC Client Search MAC address: "aa:bb:cc:dd:ee:ff" (lowercase). Result?

A) No match (case-sensitive search, must be uppercase)
B) Auto-convert to uppercase, finds client
C) Case agnostic (either case works)
D) Depends WLC OS version

**Réponse: C** - Most MAC address parsers = case-agnostic (00:11:22:33:44:55 same 00:AA:BB:CC:DD:EE)

---

### **Q36: Mobility Topology - VLAN Assignment**

Mobility Topology shown client:
- WLC: Catalyst 9800 (192.168.1.1)
- AP: AP-Building (10.1.1.1)
- Client VLAN: 200
- Client IP: 10.200.1.50

VLAN 200 logical placement?

A) AP (VLAN assignment at radio)
B) WLC (VLAN assignment at controller)
C) Upstream distribution switch (client vlan defined network-wide)
D) Both [B] and [C] (WLC assigns, distribution provides subnet)

**Réponse: D** - WLC assigns VLAN per-WLAN, distribution provides routing + DHCP

---

### **Q37: AP Load Balancing Configuration**

Two APs (AP-1, AP-2) same SSID, same channel. Client connects AP-1 (100 clients, high utilization). AP-2 empty. How load-balance?

A) Client manual switch (no automatic load balancing)
B) WLC band steering (push 5GHz clients → different AP)
C) Client count limit per-AP (excess clients forced roam)
D) Idle connection termination (random client kick = rebalance)

**Réponse: C** - WLC client-per-AP limit trigger (client count policy enforcement)

---

### **Q38: Hidden SSID Attack Vector**

SSID hidden (not broadcast). Implication security?

A) Stronger security (SSID unknown = hidden network)
B) Weaker security (SSID sent unencrypted probe response)
C) No security implication (SSID separate authentication)
D) Variable (depends WLAN version WPA2 vs WPA3)

**Réponse: C** - SSID visibility = discovery only (authentication Layer 2 independent, no security delta)

---

### **Q39: Rate Limit QoS Calculation**

QoS policy limit = 10 Mbps per-user. 3 simultaneous connections same user (mobile + laptop + tablet). QoS applied?

A) 10 Mbps per-user total (shared 3 devices = 3.3 Mbps each)
B) 10 Mbps per-device (30 Mbps total)
C) Depends policy configuration (per-user vs per-device policy)
D) QoS not enforced multi-device (limitation technical)

**Réponse: C** - Policy-dependent (WLC flexible, can configure per-user aggregate OR per-device individual)

---

### **Q40: Legacy 802.11b Client Support**

WLAN configured 802.11a only (5 GHz, no 2.4 GHz band). Legacy 802.11b device (2.4GHz only) attempt connect. Result?

A) Auto-fallback 2.4 GHz (device compatibility auto-switch)
B) Connection fails (device unsupported, no 5GHz radio)
C) Slow rate fallback (11b rates like 1, 2 Mbps)
D) Works partially (2-minute connection timeout)

**Réponse: B** - 802.11b 2.4GHz only (no 5GHz support = no connection if WLAN 5GHz exclusive)

---

### **Q41: DHCP Option 150 - WLC IP**

Client receives DHCP Option 150 = 10.50.50.50. Implication?

A) WLC management IP = 10.50.50.50 (client configuration validation)
B) Call manager (Cisco VOIP), not WebAuth
C) WLC data IP (different management IP)
D) Not applicable (legacy DHCP option, modern systems ignore)

**Réponse: A** - Option 150 = WLC IP signaling to client (WebAuth portal lookup)

---

### **Q42: IP SLA Probe Impact Client Traffic**

WLC configured IP SLA = 100 probes/second to client endpoint (10.1.1.50). Client experience?

A) No impact (synthetic probes separate from real traffic)
B) Performance degradation (probe traffic competes bandwidth)
C) QoS prioritize probes (ISE probes over regular traffic)
D) Intermittent disconnection (probe loss triggers failover)

**Réponse: A** - IP SLA synthetic = negligible bandwidth impact (few packets per second typical)

---

### **Q43: NetFlow per Client Monitoring**

NetFlow enabled on WLC uplink. Can filter "per-client" statistics?

A) Yes (NetFlow source IP = client IP)
B) Partial (NetFlow shows aggregated flows, not per-client detail)
C) No (NetFlow campus-level, client detail not captured)
D) Depends NetFlow version (v9 yes, v5 no)

**Réponse: B** - NetFlow = flow-level aggregation (client detail visible in flow source IP, not real-time detail)

---

### **Q44: Connection Test - What Verified**

Connection Test WLC runs 3 minutes. Metrics check?

A) PSK/EAP authentication flow
B) DHCP IP assignment
C) Gateway ping (IP reachability)
D) All [A] [B] [C]

**Réponse: D** - Connection Test = comprehensive (auth + DHCP + ping + stability)

---

### **Q45: Event Log Retention**

Event Log TAC data = critical troubleshooting. Storage location + retention?

A) WLC memory (reboot = lost, buffer typically 2000 events)
B) External syslog server (persistent, GBs possible)
C) ISE database (centralized, months retention)
D) All [A] [B] [C] (data replicated everywhere)

**Réponse: A** - Event Log in WLC local memory (export external syslog for permanent record)

---

### **Q46: Packet Capture Data Volume**

Client Packet Capture 60 seconds duration, high traffic. Expected file size?

A) Minimal (few KB)
B) Moderate (few MB, manageable)
C) Large (100s MB, limit capture duration)
D) Huge (GB, requires external storage)

**Réponse: C** - High-traffic capture = large PCAP (1-2 GB possible, throttle if needed)

---

### **Q47: Wireshark Decryption CCMP Frames**

Packet Capture CCMP-encrypted frames in Wireshark. Can decrypt without PSK?

A) No (PSK required decryption, Wireshark keylog feature)
B) Yes (CCMP weak encryption, brute-forcible)
C) Partial (frame headers visible, payload encrypted)
D) Only if WPA Crack tools installed (separate from Wireshark)

**Réponse: A** - CCMP strong (Wireshark needs PSK keylog file to decrypt, else payload encrypted)

---

### **Q48: Client State Transitions Fault Tolerance**

Client stuck state "Authentication" 60 seconds. WLC auto-recovery?

A) Automatic retry (no operator action needed)
B) Manual trigger (reboot client required)
C) Auto-timeout + disconnect (retry new authentication)
D) Depends WLC timer configuration (tunable)

**Réponse: C** - WLC timeout client (authentication fails), client restarts join process

---

### **Q49: Cross-Layer Diagnosis Scenario**

End-user report: "WiFi works, but file transfer very slow (2 Mbps actual vs 100 Mbps expected)". Troubleshooting checklist priority?

1) Check Link utilization (WLC uplink congested?)
2) Client signal metrics (-dBm, SNR, connection score)
3) Application layer (file server reachable, not downstream bottleneck)
4) WLC QoS policy (per-user bandwidth cap)

Recommended order?

A) 2 → 4 → 1 → 3 (access layer first)
B) 1 → 2 → 4 → 3 (network first)
C) 3 → 1 → 2 → 4 (application first, then network)
D) 4 → 2 → 1 → 3 (policy first, then signal, link, app)

**Réponse: A** - 2→4→1→3: Client signal (local issue), QoS policy (client limit), link util, app reachability

---

### **Q50: Exam Conclusion - Knowledge Check**

Review your knowledge: Which statement FALSE about wireless troubleshooting?

A) Signal dBm = only factor throughput (correct = other factors apply)
B) Connection Score formula = (rate/max) × 100
C) SNR > 20 dB typically acceptable
D) Event Log contains TAC-level details for root cause

**Réponse: A** - FALSE: dBm alone insufficient (SNR, QoS, AP load also affect throughput)

---

## Résumé Checkpoint CP8

**Total questions:** 50 | **Format:** Multiple choice, 4 options
**Duration:** 90 minutes recommended study | **Passing score:** 35/50 (70%)
**Topics coverage:** Wireless authentication (Q1-25), Troubleshooting (Q26-50)

**Score rubric:**
- **90-100% (45-50):** Mastery - Ready for exam
- **80-89% (40-44):** Strong - Minor gaps
- **70-79% (35-39):** Passing - Review weak areas
- **< 70% (< 35):** Review needed - Restudy modules

**Next steps if < 80%:** Focus weak modules, retake quiz, study notes/fiches again
