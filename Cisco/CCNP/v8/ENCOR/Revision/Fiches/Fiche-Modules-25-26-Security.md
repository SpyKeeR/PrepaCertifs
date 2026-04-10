---
title: "Fiche Modules 25-26: Security & Access Control"
type: fiche
modules: [25, 26]
topics: [SAFE, Threat Intelligence, AMP, ACL, Terminal Lines, RBAC, AAA, ZBFW, CoPP]
difficulty: advanced
updated: 2026-03-18
---

# Fiche Synthèse: Modules 25-26 - Security & Access Control

## MODULE 25: Secure Network Access Control

### SAFE Framework (6 PINs)
- **Branch**: sites distants, accès internet direct
- **Campus**: siège social, multi-VLAN complexe
- **Data Center**: données critiques, hautes perfs
- **Edge**: IoT, partenaires, accès distant
- **Cloud**: AWS, Azure, GCP, hybride
- **WAN**: MPLS, SD-WAN, inter-sites

### SAFE 6 Domains
1. **Management**: supervision, orchestration
2. **Security Intelligence**: threat intel, analytics, visibilité
3. **Compliance**: gouvernance, audit
4. **Segmentation**: micro-segmentation, isolation
5. **Threat Defense**: prévention intrusions, malware
6. **Secure Services**: chiffrement, VPN, web

### Attack Continuum: Before-During-After
```
BEFORE (Prévention)  → Talos, Threat Grid, URL Filtering
DURING (Détection)   → Stealthwatch, AMP, Behavioral Analytics  
AFTER (Remédiation)  → AMP Retrospection, Patch, Response
```

### Cisco Talos: Threat Intelligence
- **7+ sources**: Microsoft, honeypots, AEGIS, Threat Grid, partenaires
- **Mise à jour**: WSA, NGFW, AMP (signatures)
- **Disposition fichiers**: TG/GTA enrichissent intel

### Threat Grid: Dynamic Malware Analysis
- **Glovebox sandbox**: envirt. sécurisé Cisco, comportement réel malware
- **Statique vs Dynamique**: fichier seul vs exécution VM
- **Déploiement**: cloud (Cisco) ou on-prem (données sensibles)
- **Z-Day**: détection polymorphe avancée

### Cisco AMP: Full Continuum Protection
- **Cloud**: infrastructure chiffrement, Talos intel
- **Endpoints**: Windows, macOS, iOS (CSC), Android, Linux
- **Networks**: NGFW, NGIPS, ISRs
- **Email**: ESA (Email Security Appliance)
- **Web**: WSA (Web Security Appliance)
- **Meraki**: protection appliances cloud

### Cisco AnyConnect: Modular VPN Client
- **Protocoles**: TLS/SSL + IPsec IKEv2 (redondance)
- **Modules**: VPN, Posture (HostScan), ISE Posture, Web Security, Stealthwatch, Umbrella
- **Plateformes**: 8 (Windows, macOS, iOS, Android, Linux, WinPhone, BB, ChromeOS)
- **Posture**: antivirus, firewall, patch validation

### Cisco Umbrella: 100% Cloud DNS-Based Defense
- **Concept**: blocage domaines **avant connexion** (DNS-level)
- **30 Global Data Centers**: latence basse, Anycast DNS
- **100% Uptime**: SLA critique, redondance automatique
- **Blocage**: malware domains, C&C, phishing IPs, malware URLs

### WSA (Web Security Appliance): 3-Phase Protection
#### BEFORE Attack
- Web Reputation Filters (réputation domaine/IP)
- URL Filtering (catégories bloc)
- Application Usage Control (apps non-autorisées)
- Malware Inspection (téléchargement scan)

#### DURING Attack
- CASB Providers (Cloud SaaS monitoring)
- Talos Intelligence (menace temps réel)
- AMP for Networks (comportement malveillant)
- Zero-Day Detection (heuristiques)

#### AFTER Attack
- Continuous Scanning (files rescan)
- AMP Retrospection (clean → malware notification)
- Talos/Threat Grid Update (disposition change alerts)
- Incident Logging (détection logs)

**WSA Deployment**: Cloud (SaaS), Virtual (VM), On-Prem (appliance)

### Global Threat Analytics (GTA)
- **Analytics Plateforme**: corrélation 3 data sources
  1. WSA web traffic
  2. AMP endpoints
  3. Stealthwatch network anomalies
- **Cas d'usage**: détection APT multi-vecteur, incidents coordonnés

### NAC (Network Access Control)
- **802.1X**: authentification port, VLAN assignment, accounting
- **WebAuth**: redirection page login invités
- **MAB (MAC Auth Bypass)**: devices non-802.1X (imprimantes)
- **TrustSec**: SGT (Security Group Tags), segmentation confiance
- **MACsec**: chiffrement L2, intégrité

---

## MODULE 26: Network Device Access Control & Infrastructure Security

### ACLs: Fondamentaux
- **Processing**: top-down (first-match), implicit deny end
- **5 Types Cisco**: Standard, Extended, Named, PACL, VACL
- **Numbers**: Standard (1-99, 1300-1999), Extended (100-199, 2000-2699)
- **Application**: 1 ACL inbound + 1 outbound max/interface

### Standard ACL (Source Only)
```
access-list {1-99|1300-1999} {permit|deny} source [wildcard]
Example: access-list 10 permit 192.168.1.0 0.0.0.255
Apply: ip access-group 10 in
```

### Extended ACL (Source/Dest/Protocol/Port)
```
access-list {100-199|2000-2699} {permit|deny} protocol src-wildcard dst-wildcard [options]
Example: access-list 101 permit tcp 192.168.1.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 80
```

### Named ACLs (Modern Approach)
```
ip access-list standard|extended {name|#}
 [seq] {permit|deny} ...
Advantage: descriptie noms, insertion/suppression faciles
```

### Wildcard Mask Calculation
- **Formula**: wildcard = 255.255.255.255 - subnet mask
- **Example**: 255.255.255.0 subnet → 0.0.0.255 wildcard
- **Keywords**: `any` (0.0.0.0 255.255.255.255), `host` (spécifique)

### PACLs (Port ACLs): Layer 2 Filtering
- **Restriction**: inbound-only, pas outbound
- **Pas filtre**: L2 control (CDP/VTP/DTP/PAgP/UDLD/STP)
- **Hardware**: table CAM, pas CPU
- **Pas support**: IPv6, ARP, MPLS
- **Apply**: `ip access-group {name|#} in` sur port

### VACLs (VLAN ACLs): VLAN-Wide Filtering
```
ip access-list standard|extended {name|#}
vlan access-map {map-name} {seq} 
 match ip address {acl-name|#}
 match mac address acl-name
 action forward|drop [log]
vlan filter {map-name} vlan-list {vlan-range}
```

### Processing ACL Order
- **Bridged** (même VLAN): PACL in → VACL in → VACL out
- **Routed** (inter-VLAN): PACL in → VACL in → SVI in → routage → SVI out → VACL out

### Terminal Line Security
```
line console 0 → local console authentication
line vty 0 4   → Telnet/SSH authentication
password {pass} → simple auth
login local     → local database auth (username/privilege)
```

### Privilege Levels (0-15)
- **0**: Disable (disable only), **1**: User (show/ping), **15**: Enable (full admin)
- **2-14**: Custom levels, `privilege exec {level} {command}`
- **RBAC**: assign users privilege groups

### AAA (Authentication, Authorization, Accounting)
- **Auth**: identity verification (username/password)
- **Authz**: permission assignment (privilege level)
- **Acct**: action logging (syslog)
- **Server**: TACACS+ (Cisco proprietary) vs RADIUS
- **Config**: 
  ```
  aaa new-model
  tacacs server TACACS_SERVER1
   address ipv4 10.0.0.1
   key TacacsSecret123
  aaa authentication login default group tacacs+ local
  ```

### Zone-Based Firewall (ZBFW)
- **Concept**: stateful firewall par zones, pas interfaces
- **Zones**: security zones (inside, outside, dmz, guest)
- **Zone-Pair**: définit policies (zone-pair source-dest)
- **Steps**:
  1. `zone security {name}`
  2. `interface → zone-member security {name}`
  3. `class-map type inspect match-any {name}` (traffic classification)
  4. `policy-map type inspect {name}` (actions)
  5. `zone-pair security {src}-{dst} source {src} destination {dst}`
     `service-policy type inspect {policy-name}`

### Control Plane Policing (CoPP)
- **Purpose**: protect router CPU/RP from DoS/flooding
- **Rate-Limit**: paquets destined CPU (management traffic prioritized)
- **Config**:
  1. ACLs classify packets (SSH, OSPF, ICMP, default)
  2. Class-maps match ACLs
  3. Policy-map define rate-limits
  4. `control-plane → service-policy input {policy-name}`

---

## Résumé Comparatif: Sécurité Before-During-After

| Phase | Composant | Fonction |
|-------|-----------|----------|
| **BEFORE** | Umbrella/Talos | DNS block, threat intel |
| **BEFORE** | WSA filters | URL reputation, malware detect |
| **BEFORE** | AMP prevention | Endpoint protection |
| **DURING** | Stealthwatch | Network behavioral analytics |
| **DURING** | Threat Grid | Malware sandbox |
| **DURING** | AMP detection | Endpoint behavior detection |
| **AFTER** | GTA correlation | Multi-source incident analysis |
| **AFTER** | AMP retrospection | Historical file disposition change |
| **AFTER** | Incident response | Device isolation, remediation |

---

## Hiérarchie Sécurité Réseau

```
L4-L7: Application Security (WSA, IPS)
       ↓
L3-L4: Network Firewall (ZBFW, CoPP, NGFW)
       ↓
L2-L3: Device Access (ACL, PACL, VACL)
       ↓
L1-L2: Terminal Access (Console, VTY, Privilege)
       ↓
Identity: AAA Authentication & Authorization
```

---

## Checklists: Security Control Implementation

### Access Control Checklist
- [ ] Standard ACL pour source filtering
- [ ] Extended ACL pour protocol/port filtering
- [ ] Named ACLs réseau-wide (version control)
- [ ] PACLs pour port access restricting
- [ ] VACLs pour inter-VLAN isolation
- [ ] ACEs logged pour auditing

### Device Management Checklist
- [ ] Console password défini
- [ ] VTY password défini
- [ ] Local database (login local)
- [ ] Privilege levels assigné par rôle
- [ ] TACACS+ configured (centralized)
- [ ] AAA authentication policies définies

### Infrastructure Hardening Checklist
- [ ] ZBFW zones définie
- [ ] Zone-pair policies configured
- [ ] CoPP policies deployed (CPU protect)
- [ ] Syslog configured (audit trail)
- [ ] TACACS+ backup servers (HA)
- [ ] Device health monitoring (SNMP)
