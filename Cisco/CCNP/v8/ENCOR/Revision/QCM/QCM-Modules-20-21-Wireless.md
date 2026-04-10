---
title: "QCM Module 20-21: Authentification et Dépannage sans fil"
modules: [20, 21]
type: qcm
topics: [wireless-authentication, PSK, 802.1x, troubleshooting, WLC, client-states]
difficulty: [beginner, intermediate]
questions: 25
updated: 2026-03-18
---

# QCM Module 20-21: Authentification et Dépannage sans fil (25 questions)

## Questions (Partie A: Modules 20-21)

---

### **Q1: Configuration Open Authentication**

Une organisation déploie WLAN avec accès public (pas de mot de passe). Quel est le chemin correct de configuration WLC GUI?

A) WLANs → Security → Layer 2 → WPA2 + CCMP
B) WLANs → Security → Layer 2 → None (aucune sécurité)
C) WLANs → Security → Layer 3 → OPEN
D) WLANs → Authentication → Open Mode

**Réponse: B**

**Explication technique:**
L'authentification ouverte sur WLC est configurée en définissant Layer 2 Security = "None". Cette configuration supprime toute cryptographie et authentification 802.11, permettant accès public. Les options WPA2/CCMP ou Layer 3 ne correspondent pas au modèle open auth (qui fonctionne à Layer 2). "Open Mode" est une terminologie non-standard Cisco WLC.

---

### **Q2: PSK Pre-Shared Key - Caractéristiques WPA2-PSK**

Quels sont les éléments clés du protocole WPA2-PSK avec CCMP-AES?

A) Chiffrement TKIP, clé partagée 8 caractères
B) Chiffrement CCMP-AES, fournir PMK (Pairwise Master Key) = PSK, 4-way handshake, aucune forward secrecy
C) Chiffrement ECC, support SAE (Simultaneous Authentication of Equals), forward secrecy per-session
D) Authentification par certificat, chiffrement variable (TLS)

**Réponse: B**

**Explication technique:**
WPA2-PSK + CCMP-AES utilise: (1) Chiffrement CCMP avec AES (256-bit); (2) PMK = PSK pré-partagée (8-63 chars ASCII ou 64 hex); (3) 4-Way Handshake pour dériver PTK; (4) MIC validation à chaque frame; (5) Aucune forward secrecy inter-session (PTK réutilisée). TKIP = WPA hérité (obsolète). SAE = WPA3 (pas WPA2). Certificats = EAP enterprise (pas PSK).

---

### **Q3: SAE vs 4-Way Handshake**

Quel avantage clé SAE (WPA3-Personal) offre-t-il par rapport au 4-Way Handshake (WPA2-Personal)?

A) Réduction du nombre de frames EAPOL
B) Forward secrecy par session + résistance attaques dictionary offline
C) Chiffrement avec AES-256 (vs AES-128 WPA2)
D) Support multi-user authentication (vs mono-utilisateur WPA2)

**Réponse: B**

**Explication technique:**
SAE (Simultaneous Authentication of Equals) basé Dragonfly Protocol offre: (1) Forward secrecy par session = clés dérivées fresh (pas réuse); (2) Résistance dictionary attacks offline = une tentative par connection on-the-wire (infaisable réseau); (3) Mutual authentication égale (pas hierarchie AP>client). Réduction frames = vrai mais pas clé. AES-256 = même WPA2. Multi-user = non applicable PSK.

---

### **Q4: Configuration 802.1x RADIUS sur WLC**

Lors configuration serveur RADIUS pour 802.1x, quel élément CRITIQUE manque souvent?

```
WLC → Administration → AAA → RADIUS → Authentication
├─ IP Address: 10.50.50.50 ✓
├─ Shared Secret: MySecret123! ✓
├─ Port: 1812 ✓
└─ ??? = CRITQUE
```

A) Enable Network User Authentication checkbox
B) Enable Accounting Server
C) Set RADIUS timeout > 10 seconds
D) Sélectionner la vlan de management

**Réponse: A**

**Explication technique:**
"Enable Network User Authentication" CHECKBOX est critère pour 802.1x client authentication (vs MAC authentication uniquement). Sans cette case, WLC n'accepte pas authentifications 802.1x (EAP supplicant). Accounting optionnel (pour syslog). Timeout 5s standard OK. VLAN = configuration distincte.

---

### **Q5: WLAN 802.1x – Configuration AAA Servers**

Une WLAN 802.1x nécessite sélection serveur RADIUS. Quel onglet WLC contient cette configuration?

A) General tab → AAA Servers option
B) Security tab → RADIUS list
C) AAA Servers tab → sélectionner RADIUS primaire + failover
D) Advanced tab → Authentication Server selection

**Réponse: C**

**Explication technique:**
WLC WLAN creation/editing: AAA Servers tab = lieu sélection RADIUS pour 802.1x authentication. Ce tab distinct indépendant de Security tab (qui configure Layer 2 type). Failover support = multiple serveurs listés (HA).

---

### **Q6: 4-Way Handshake WPA2 – Étape clé (Message 1)**

Lors 4-Way Handshake WPA2, quel élément Message 1 (AP → Client) contient?

A) SNonce (Station Nonce) + MIC client
B) ANonce (AP Nonce) + demande client envoyer SNonce
C) PTK dérivée + GTK (Group Transient Key)
D) EAPOL-Key frame avec clés symétriques établies

**Réponse: B**

**Explication technique:**
Message 1 (AP → Client): AP envoie ANonce (AP's aléatoire nonce) + demande client répondre. Client utilise ANonce + SNonce (client's nonce) pour dériver PTK. PTK = dérivée message 1-2 uniquement (pas transmise). GTK = message 3.

---

### **Q7: EAP Framework – Définition et types**

EAP n'est PAS une méthode authentification unique. Qu'est-ce réellement?

A) Protocole spécifique (comme Kerberos)
B) Framework flexible supportant multiples méthodes (EAP-TLS, EAP-PEAP, EAP-FAST)
C) Standard chiffrement (comme AES)
D) Format transport RADIUS (même chose que Access-Accept)

**Réponse: B**

**Explication technique:**
EAP = Extensible Authentication Protocol, framework qui encapsule diverses méthodes (TLS, PEAP, TTLS, FAST, MD5). Cette flexibilité permet déployer diverses technos (certs, passwords, OTP) sans remplacer infrastructure complète.

---

### **Q8: WebAuth Captive Portal – Configuration Layer 2**

Une WLAN utilisant WebAuth (authentification portal page web) quel Layer 2 Security doit configurer?

A) WPA2-PSK + CCMP (puis portal login)
B) 802.1x + EAP-PEAP (puis portal)
C) None (aucune sécurité Layer 2)
D) Open + 802.11w MFP

**Réponse: C**

**Explication technique:**
WebAuth = portal HTTP-based login (séparé Layer 2 security). Layer 2 = None (pas PSK/EAP). Authentification réalisée APRÈS association via captive portal (HTTP redirect DHCP). Layer 2 sécurité viendrait APRÈS (pas optimal pour guest flow).

---

### **Q9: Troubleshooting – Client Stuck "Association" State**

Client WLC reste bloqué état "Association" (> 500ms, normal < 100ms). Quelles diagnostiques premiers?

A) Vérifier RADIUS server reachability
B) Vérifier SSID diffusée + AP capacité + channel supporté par client
C) Tester DHCP server disponibilité
D) Vérifier user credentials correctes

**Réponse: B**

**Explication technique:**
État "Association" = échange frames 802.11 (auth + assoc) avec AP. Si stuck: (1) SSID not broadcast (hidden SSID = problème); (2) AP capacité full (too many clients); (3) Client doesn't support channel/band (legacy 11b-only client vs 802.11n). RADIUS = Authentication state (postérieur). DHCP = DHCP state. Credentials = Authentication state.

---

### **Q10: Client States – Progression "Start" → "Online"**

Un client affiche state "DHCP" et reste stuck. Qui est responsable configuration DHCP?

A) Client WLAN (configuration réseau client)
B) WLC (must have DHCP server embedded)
C) DHCP server sur client VLAN (allocated par WLC assignment)
D) AP (DHCP relay)

**Réponse: C**

**Explication technique:**
État "DHCP" = WLC assigne client VLAN, client envoie DHCP request. DHCP server réside sur VLAN assignée (peut être switch externe, WLC n'héberge pas DHCP tout seul sauf option). Si DHCP server down ou scope exhausted = stuck DHCP state.

---

### **Q11: Signal dBm Interpretation**

Client signal -76 dBm. Quel est l'état de signal?

A) Excellent (max rate)
B) Good (acceptable)
C) Fair/Weak (rate reduction expected)
D) Critical (unusable)

**Réponse: C**

**Explication technique:**
dBm scale: -30 to -50 = excellent; -50 to -70 = good; -70 to -85 = fair; -85 to -100 = weak; < -100 = critical. -76 dBm = fair/weak range (begin rate reduction, potential roaming issues).

---

### **Q12: SNR (Signal-to-Noise Ratio) Reference**

Un client affiche SNR 18 dB. Comment interpreter?

A) Excellent (no interference)
B) Good (clean signal)
C) Fair (some noise, noticeable impact)
D) Weak (significant noise)

**Réponse: D**

**Explication technique:**
SNR reference: > 40 dB excellent; 30-40 = good; 20-30 = fair; 15-20 = weak; 10-15 = poor; < 10 = critical. SNR 18 dB = weak/poor range (significant noise, rate adaptation will reduce)

---

### **Q13: Connection Score Calculation**

Client WLC shows: Actual Rate 29 Mbps, Max Rate 144 Mbps. Connection Score = ?

A) 20%
B) 50%
C) 80%
D) 100%

**Réponse: A**

**Explication technique:**
Formula: Connection Score = (Actual Rate ÷ Max Rate) × 100. (29 ÷ 144) × 100 = 20.14% ≈ 20%. Interpretation: 20% = poor (troubleshoot signal/interference).

---

### **Q14: Client View – Wireless Policy Information**

WLC Client View → Wireless Policy affiche:
```
VLAN: 100
QoS Policy: Gold
Security Policy: WPA2-PSK
Encryption: CCMP AES
```

Quel élément indique config problématique?

A) Aucun problème, config standard
B) VLAN 100 réservée management (doit être 101+)
C) Gold QoS non-approprié guest (doit être Silver/Bronze)
D) Encryption CCMP sans WPA3-SAE

**Réponse: A**

**Explication technique:**
Politique affichée = valides: VLAN 100 OK (peut être any); Gold QoS OK si user premium; WPA2-PSK + CCMP standard. Aucune violation visible. (B) VLAN numbering = policy-based, non-critique. (C) Gold QoS = policy-based. (D) CCMP = WPA2/WPA3 both use.

---

### **Q15: Client Ping Test (WLC Tool)**

Client Ping Test result: "4/5 successful, 1 packet lost". Quel est diagnostic?

A) Client completely offline (can't reach gateway)
B) Client fully online (excellent connectivity)
C) Intermittent connectivity (flaky link or rate-limiting)
D) DHCP server unavailable

**Réponse: C**

**Explication technique:**
4/5 successful = 20% loss intermittent. 5/5 = online OK. 0/5 = offline. 4/5 = flaky (weak signal causing retransmissions, or QoS dropping packets stochastically).

---

### **Q16: Connection Test vs Ping Test**

Difference clé entre "Ping Test" et "Connection Test" WLC?

A) Ping = ICMP only; Connection Test = multiple protocol (EAP, DHCP, ping)
B) Ping = instant result; Connection = long-running 3 minutes benchmark
C) Both identiques, same functionality
D) Ping test client-initiated; Connection test AP-initiated

**Réponse: B (partially A also correct)**

**Explication technique:**
Ping Test: 5 ICMP echo packets, instant result (< 2 seconds).
Connection Test: 3-minute deep diagnostic testing EAP/PSK + DHCP + ping + stability. Connection Test = more thorough for root cause.

---

### **Q17: Event Log – Client Join Analysis**

Client Event Log displays:
```
[12:34:15] Client Associated to AP Building-1
[12:34:16] EAPOL Started
[12:34:20] 4-Way Handshake: Message 3 timeout waiting...
[12:34:22] Authentication failed: Wrong PSK
```

Quel est problème?

A) PSK incorrect (client + AP mismatch)
B) AP radio defect (timeout)
C) RADIUS server down (EAP timeout)
D) DHCP server not reachable

**Réponse: A**

**Explication technique:**
Log shows: Association OK → EAPOL start OK → 4-way stuck (message 3 timeout) → auth fail "Wrong PSK". Indicates PSK mismatch (client entered wrong password OR AP config differs). RADIUS = EAP flow (not 4-way). Radio = would show assoc fail. DHCP = later state.

---

### **Q18: AP Troubleshooting – Multiple Users Same Area Slow**

Plusieurs utilisateurs (20+) même zone (Office Building) rapportent slow WiFi. 2-3 users autres zones OK. Diagnostic probable?

A) Client device hardware defects
B) Individual user configuration errors
C) AP capacity exceeded OR AP radio defect
D) Firewall ACL blocking specific user IPs

**Réponse: C**

**Explication technique:**
Multiple users same area = AP problem (not individual clients). Likely: (1) Client count exceeds AP capacity (60+ clients overload); (2) AP radio defect/crashed; (3) Channel interference (same as neighbor). Individual device issues = only 1 user affected. Firewall ACL = specific IPs, not "slow".

---

### **Q19: Packet Capture Analysis – Wireshark Filter EAPOL**

WLC Packet Capture exported, opened Wireshark. Quels filter à utiliser pur analyzeر 4-Way Handshake?

A) Filter "tcp" (TCP protocol inspection)
B) Filter "eapol" (EAPOL frame inspection)
C) Filter "dhcp" (DHCP exchange inspection)
D) Filter "802.11" (wireless frames)

**Réponse: B**

**Explication technique:**
4-Way Handshake uses EAPOL (EAP over LAN) frames. Filter "eapol" in Wireshark displays Key Exchange frames (message 1, 2, 3, 4). DHCP = IP assignment (later). TCP = application traffic. 802.11 = radio layer (but EAPOL nested inside).

---

### **Q20: WLC Client Double-Check Blacklist**

Client associates briefly, then immediately disassociates (stuck "Association" state). WLC check options?

A) Show client detail [MAC] | include state
B) Show client blacklist [check if MAC listed]
C) Show ap associations [verify AP healthy]
D) Show wlan security config [verify PSK]

**Réponse: B**

**Explication technique:**
Immediate disassociation = likely MAC address blacklisted (after failed authentications or manual blocking). Command: `show client blacklist` lists blocked MACs. Option A = shows state (slow tracking). Option C = AP healthy (may be OK). Option D = security config (not blocking issue).

---

### **Q21: RADIUS Shared Secret Security Practice**

Shared secret RADIUS entre WLC et ISE est sensible donnée. Meilleure pratique stockage?

A) Plain text WLC configuration (visible show running-config)
B) Encrypted vault/password manager (not human-readable)
C) Printed on post-it (aide mémoire staff)
D) Hash MD5 dans config

**Réponse: B**

**Explication technique:**
Shared Secret RADIUS = authentication credentials (like password). Meilleure practice: (1) Vault/password manager encrypted storage; (2) Never plain text; (3) Rotate periodically; (4) Not accessible show running-config (Cisco masks with asterisks). Printing/hashing = ineffective protection.

---

### **Q22: PSK vs Enterprise Auth – Choice Criteria**

Une PME (100 utilisateurs) choisit entre WPA2-PSK vs 802.1x. Recommendation?

A) PSK (simpler, faster deployment, adequate security)
B) 802.1x (must-have enterprise security)
C) WebAuth (guest-friendly, suitable small org)
D) Open Auth (cost-free, no infrastructure)

**Réponse: A**

**Explication technique:**
PME 100 users: PSK acceptable (clé complexe, rotation policy). 802.1x overkill (ISE/RADIUS infrastructure unnecessary). Guest = separate network (not primary). Open = aucune sécurité. Budget = PSK wins, scalability concern future = 802.1x reconsider.

---

### **Q23: MFP (Management Frame Protection) – 802.11w**

Quelle vulnérabilité MFP (802.11w) protège?

A) WPA2 encryption weakness
B) PSK brute-force attacks
C) Deauthentication frame floods (denial of service)
D) RADIUS server identity spoofing

**Réponse: C**

**Explication technique:**
MFP (802.11w Management Frame Protection) encrypts + authenticates management frames (deauth, disassoc). Protection: Attacker can't spoof deauth frames (would require PTK knowledge). Attacker sends raw deauth frame → client ignores (MIC validation fails). Recommended WPA3 (mandatory), WPA2 (optional).

---

### **Q24: Roaming Assist – Fast Roaming WLC**

Client roams AP A → AP B different SSID. WLC option "Managed Key Caching" enabled. Benefit?

A) Client automatically changes SSID (impossible, same SSID)
B) PTK cached (re-derive faster, reduce roaming latency)
C) DHCP lease preserved (same IP)
D) QoS policies synchronized (no service disruption)

**Réponse: B**

**Explication technique:**
Managed Key Caching (802.11r Fast Roaming predecessor): Client + AP cache PTK, 4-way bypass on roam. Benefit: Reduce authentication delay (critical VoIP). Modern = 802.11r (FT = Fast Transition, explicit standard). Same IP = managed by DHCP (lease still valid via ARP). QoS = policy inheritance per VLAN.

---

### **Q25: Integration ISE + WLC – Data Flow**

Workflow authentication 802.1x sur WLC avec ISE backend. Data flow correct?

A) Client → WLC (EAPOL) → ISE (RADIUS) → Client answer → Online
B) Client → ISE directly (EAP) → WLC (policy) → Permit/Deny
C) WLC → ISE (RADIUS) → Client (EAPOL response) → 4-Way → Online
D) Client → AP (EAPOL) → WLC (proxy) → ISE (RADIUS) → Forward answser → Client

**Réponse: D**

**Explication techniques:**
Workflow: Client sends EAPOL frames → AP (radio layer) → WLC (centralized AAA proxy, split-MAC architecture) → ISE (RADIUS Access-Request) → ISE validates (AD/LDAP) → RADIUS Access-Accept/Challenge → Back to client EAPOL response → Client validtes → Online. (A) Correct high-level. (B) Direct ISE = incorrect (WLC mandatory proxy). (C) Missing 4-way detail.

---

## Résumé des résponses

| Q# | Réponse | Domaine | Difficulté |
|----|---------|---------|-----------|
| 1 | B | Open Auth config | Beginner |
| 2 | B | WPA2-PSK mechanics | Intermediate |
| 3 | B | WPA3 vs WPA2 | Advanced |
| 4 | A | RADIUS config critique | Intermediate |
| 5 | C | WLC GUI navigation | Beginner |
| 6 | B | 4-Way handshake detail | Intermediate |
| 7 | B | EAP framework | Beginner |
| 8 | C | WebAuth configuration | Intermediate |
| 9 | B | Troubleshooting Association | Intermediate |
| 10 | C | DHCP role | Beginner |
| 11 | C | Signal dBm interpretation | Beginner |
| 12 | D | SNR interpretation | Beginner |
| 13 | A | Connection Score math | Beginner |
| 14 | A | Policy verification | Intermediate |
| 15 | C | Ping result interpretation | Beginner |
| 16 | B | Tools comparison | Intermediate |
| 17 | A | Event log analysis | Intermediate |
| 18 | C | AP troubleshooting | Intermediate |
| 19 | B | Wireshark filtering | Advanced |
| 20 | B | Blacklist checking | Intermediate |
| 21 | B | Shared secret security | Advanced |
| 22 | A | PSK vs Enterprise | Intermediate |
| 23 | C | MFP protection | Advanced |
| 24 | B | Roaming optimization | Intermediate |
| 25 | D | ISE integration flow | Advanced |

**Score cible: ≥ 20/25 (80%) pour certification readiness**
