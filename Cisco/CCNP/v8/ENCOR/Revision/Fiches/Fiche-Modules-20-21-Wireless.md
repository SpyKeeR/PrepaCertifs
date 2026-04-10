---
title: "Fiche Module 20-21: Authentification et Dépannage sans fil"
modules: [20, 21]
type: fiche
topics: [wireless-quick-ref, authentication-methods, troubleshooting-checklist, WLC-commands, client-states]
difficulty: intermediate
updated: 2026-03-18
---

# Fiche Module 20-21: Authentification et Dépannage sans fil

## Tableau comparatif: Méthodes authentification wireless

| Méthode | Sécurité | Configuration | Cas d'usage | Avantages | Inconvénients |
|---------|----------|---------------|-----------|-----------|--------------|
| **Open (aucune)** | ❌ Aucune | WLAN → Security → None | Wi-Fi public, invités | Simple, accès rapide | Aucune protection données |
| **WPA2-PSK** | ⭐⭐⭐⭐ | WLAN → Security → WPA2 + CCMP | PME, petits réseaux | Rapide, déploiement simple | Key partagée = audit limité |
| **WPA3-SAE** | ⭐⭐⭐⭐⭐ | WLAN → Security → WPA3 + SAE | Modernes, sécurité haute | Forward secrecy, resistant dict attacks | Devices supportant W...3 rares encore |
| **802.1x (Enterprise)** | ⭐⭐⭐⭐⭐ | WLAN → Security → 802.1x + EAP | Entreprise, audit requis | User accountability, policies flexibles | Infrastructure ISE/RADIUS requise |
| **WebAuth (Portal)** | ⭐⭐ | WLAN → Web-Auth → Enable | Guests, BYOD, quick access | Pas config client, rapid onboarding | Password simple, audit basique |

---

## Processus WPA2-PSK 4-Way Handshake

```
Client                          AP
  |                              |
  |  ← ← ← ← ← Message 1 ← ← ← ← | (ANonce, AP nonce)
  |                              |
  | Message 2 (SNonce, MIC) → → → |
  |                              |
  | ← ← ← ← ← Message 3 ← ← ← ← | (GTK groupkey, MIC)
  |                              |
  | Message 4 (MIC ACK) → → → → | 
  |                              |
  | [Key installation] → → → → → |
  |                              |
  | ← ← ← ← [Online] ← ← ← ← ← | 

Clés dérivées:
├─ PMK (Pairwise Master Key) = PSK pré-partagée
├─ PTK= (Pairwise Transient Key) dérivée PMK + Nonces + MACs
└─ GTK (Group Transient Key) pour broadcast/multicast
```

---

## Comparatif WPA/WPA2/WPA3

| Aspect | WPA | WPA2 | WPA3 |
|--------|-----|------|------|
| **État** | ❌ EOL (2002-2006) | ✓ Courant | ✓ New standard |
| **Chiffrement** | TKIP (faible) | CCMP-AES (fort) | CCMP-AES (très fort) |
| **Handshake** | 4-Way similaire | 4-Way standard | SAE Dragonfly (nouveau) |
| **Forward secrecy** | Non | Non (PTK réutilisée) | **OUI (par session)** |
| **Dictionary attacks** | Faible | Moyens offline | ❌ Impossible en-ligne |
| **Fragmentation protection** | TKIP tkip_michael | MIC dans 4-way | TBD |

---

## Vérification et configuration RADIUS WLC (GUI)

### Ajout serveur RADIUS (Authentication)
```
WLC Dashboard → Administration → AAA → RADIUS → Authentication
├─ [New] button
│  ├─ IP Address: 10.50.50.50 [ISE/RADIUS server IP]
│  ├─ Shared Secret: MySecret123! [same on server + WLC]
│  ├─ Port: 1812 [standard, modifiable]
│  ├─ Timeout: 5 [secondes]
│  ├─ Retries: 2
│  └─ ☑ Enable Network User Authentication [CRITICAL pour 802.1x]
└─ [Save/Apply]

Vérification:
├─ WLC show commands (CLI):
│  └─ show radius auth servers [affiche RADIUS config]
├─ Test connectivity (CLI):
│  └─ test radius server 10.50.50.50 [envoi test packet RADIUS]
└─ ISE side checks:
   └─ ISE Dashboard → Radius → Live Logs [confirmer packets reçus]
```

### Configuration WLAN avec 802.1x
```
WLCs → Create/Edit WLAN
├─ General:
│  └─ SSID: enterprise-auth
├─ Security → Layer 2:
│  ├─ Authentication Method: 802.1x
│  ├─ WPA Version: WPA2 [OU WPA3]
│  ├─ WPA Encryption: CCMP (AES)
│  └─ Managed Key Caching: Enabled [fast roaming]
├─ AAA Servers:
│  └─ RADIUS Authentication Server: [sélectionner serveur primaire + failover]
├─ Advanced:
│  └─ 802.11w MFP: Required [protection deauth]
└─ Interface/VLAN: [sélectionner vlan de l'utilisateur]
```

---

## États client sans fil (Progression et troubleshooting)

### State Machine diagram
```
[Start] → [Association] → [Authentication] → [DHCP] → [Online]
   ↓           ↓              ↓               ↓         ↓
  <1s       <100ms          1-5s            1-3s     Active
 
Stuck? Check:  Wrong SSID   PSK/EAP Fail,  DHCP     Gateway
              AP capacity   RADIUS down    down      reachable?
              Wrong channel EAP timeout    Scope     Firewall
                            802.1X policy  full      blocking
```

### État-par-état debugging

| État | Normal duration | Si stuck | Diagnostic |
|------|---|---|---|
| **Start** | < 1 sec | > 2 sec | `show client detail [MAC]` look for "State: Start" |
| **Association** | < 100 ms | > 500 ms | Verify SSID broadcast, AP has capacity, channel supported |
| **Authentication** | 1-5 sec | > 10 sec | Check PSK correct, RADIUS reachable (show radius statistics), EAP timeout |
| **DHCP** | 1-3 sec | > 5 sec | ping DHCP server, verify DHCP scope on client vlan |
| **Online** | Duration | N/A (healthy state) | Connection score > 70% = good signal |

---

## Métriques client WLC (Interpretation rapide)

### Signal dBm reference
```
-30 to -50 dBm  ⭐⭐⭐⭐⭐ Excellent (max rate)
-50 to -70 dBm  ⭐⭐⭐⭐  Good (acceptable)
-70 to -85 dBm  ⭐⭐⭐   Fair (rate reduction)
-85 to -100 dBm ⭐⭐   Weak (frequent issues)
< -100 dBm      ⭐    Critical (unusable)

Typical acceptable: -40 to -70 dBm
```

### SNR (Signal-to-Noise Ratio) reference
```
> 40 dB  ⭐⭐⭐⭐⭐ Excellent (no interference)
30-40 dB ⭐⭐⭐⭐  Good (clean signal)
20-30 dB ⭐⭐⭐   Fair (some noise)
15-20 dB ⭐⭐   Weak (significant noise)
10-15 dB ⭐    Poor (connection unstable)
< 10 dB  ✗    Critical (unusable)
```

### Connection Score formula
```
Score % = (Actual Rate Mbps / Max Rate Mbps) × 100

Examples:
├─ 144 Mbps actual / 144 Mbps max = 100% ✓ Perfect
├─ 72 Mbps actual / 144 Mbps max = 50% ⚠ Fair
├─ 29 Mbps actual / 144 Mbps max = 20% ❌ Poor (troubleshoot signal)
└─ 6 Mbps actual / 144 Mbps max = 4% ❌ Critical (likely AP/rate limit issue)
```

---

## Outils diagnostic client rapide

### Ping Test (WLC)
```
WLC Client View → [Client] → Client Tools → Ping Test
├─ Destination: [default = client gateway]
├─ Count: 5 [packets]
├─ Size: 100 [bytes, change to 1500 for MTU test]
└─ Result:
   ├─ 5/5 successful ✓ Client reach gateway (IP connectivity working)
   ├─ 3/5 successful ⚠ Intermittent loss (weak signal or QoS rate limiting)
   └─ 0/5 successful ✗ No reachability (routing/firewall/server down)
```

### Connection Test (3-minute deep check)
```
WLC Client View → [Client] → Client Tools → Connection Test
├─ Duration: 3 minutes continuous testing
├─ Tests:
│  ├─ EAP/PSK authentication success
│  ├─ DHCP IP acquisition success
│  ├─ Gateway reachability (ping)
│  └─ Signal stability over time
└─ Pass/Fail result: Indicates step-by-step issue
   ├─ "Authentication failed: Wrong Key" → PSK issue
   ├─ "DHCP failed: Timeout" → DHCP server down or vlan mismatch
   └─ "Internet Test failed: Host unreachable" → Gateway/firewall issue
```

### Event Log (Detailed timeline)
```
WLC Client View → [Client] → Client Tools → Event Log
├─ Shows: [Timestamp] Event details
│  ├─ "Client Associated to AP BLDG-1"
│  ├─ "EAPOL Started" (if 802.1x enabled)
│  ├─ "4-Way Handshake Completed" (if WPA-PSK)
│  ├─ "DHCP Discover Sent"
│  ├─ "DHCP ACK Received: IP=10.1.1.50"
│  └─ "Client Status: Online"
└─ TAC info: Detailed error if join fails
```

### Packet Capture (PCAP export)
```
WLC Client Tools → Packet Capture [Client MAC]
├─ Duration: 5-60 seconds
├─ [Start] → captures traffic to/from client
├─ [Download PCAP]
└─ Analyze Wireshark:
   ├─ Filter "eapol" → inspect 4-way handshake frames
   ├─ Filter "dhcp" → check DHCP exchange
   ├─ Filter "icmp" → verify ping/probe traffic
   └─ Inspect encryption/MIC fields for validation
```

---

## Checklist troubleshooting rapide

### Client can't connect WLAN
```
☐ Step 1: Verify SSID visible (broadcast enabled?)
☐ Step 2: Check WLAN enabled on WLC (status = enabled)
☐ Step 3: Verify client not blacklisted (show client blacklist)
☐ Step 4: Check security key correct
  ├─ PSK mode: pwd matches config
  ├─ 802.1x mode: user/pwd correct, ISE accepting
  └─ WebAuth mode: portal accessible
☐ Step 5: Verify WLC-AP connectivity (show ap summary)
☐ Step 6: Check VLAN/interface configured (show interface)
☐ Step 7: Test RADIUS server reachability + shared secret
☐ Step 8: Verify MTU matched (typical 1500 bytes)
☐ Step 9: Check DHCP server reachable on client VLAN
☐ Step 10: Review AP client count (capacity exceeded?)
```

### Client connected but slow
```
☐ Signal strength: show client detail [MAC] → check dBm (-70dBm+ = issue)
☐ SNR level: Look for < 20 dB range (noise issue)
☐ Connection score: Calculate (rate/max) × 100 → if < 50% = signal issue
☐ AP load: show ap summary → high client count = AP capacity issue
☐ Channel interference: Check neighboring APs same channel
☐ Data rate: Too low rate = signal or rate limiting
  ├─ 6, 12, 24 Mbps basic rates = legacy devices or signal very weak
  ├─ Compare to AP max (144+ for 802.11ac)
  └─ If capped artificially = check WLC QoS policies
☐ DHCP: Verify client IP in correct VLAN subnet
☐ QoS policy: Check bandwidth limits applied per user/group
```

---

## Commandes CLI WLC essentielles

```bash
# Affichage client
show client summary               # Nombre clients, AP associations
show client detail [MAC address]  # Détails complets client spécifique
show ap summary                   # Liste APs + states
show ap config general            # Détails configuration AP

# WLAN configuration
show wlan summary                 # Résumé WLANs activées
show wlan id 1                    # Détails WLAN 1 (security, vlan, etc.)

# RADIUS server status
show radius statistics            # Request/response counts
show radius auth servers          # Listen servers de renvoi
test radius server 10.50.50.50    # Teste connectivité serveur RADIUS

# Interface/VLAN
show interface summary            # Summary interfaces IP + status
show interface Vlan100            # Détails interface VLAN 100

# Troubleshooting
debug client [MAC]                # Detailed logging client spécifique
debug client [MAC] packet          # Observe EAPOL frames
show client blacklist             # MAC addresses blacklisted
```

---

## Ressources quick-lookup
- **WLC IP default access**: https://[WLC-IP]:8443 (port 8443 HTTPS)
- **PSK bits**: 8-63 ASCII OR 64 hexadécimal characters
- **RADIUS standard port**: UDP 1812 (auth), UDP 1813 (accounting)
- **802.1x WLAN setting**: Authentication Method = "802.1x" (not PSK)
- **Speed test**: iperf3 client→server same VLAN (validate LAN, not WLAN)
