---
title: "Checkpoint CP10: Security & Access Control (Modules 25-26)"
type: checkpoint
checkpoint: 10
modules: [25, 26]
questions: 50
difficulty: certification
updated: 2026-03-18
---

# Checkpoint CP10: Security & Access Control
## 50 Certification-Level Questions

---

### Q1: SAFE Scenario
**Vous déployez infrastructure sécurité enterprise couvrant sites distants, campus principaux et cloud. Quel framework Cisco guide cette architecture?**

A) CCNP Enterprise  
B) Cisco SAFE (Security Architectural Framework)  
C) Cisco Catalyst  
D) Cisco DNA  

**Réponse: B** — SAFE = framework couvrant tous PINs (Branch, Campus, Cloud, etc.)

---

### Q2: Threat Intelligence Sources
**Votre SOC nécessite real-time threat intelligence pour blocage IPs malveillantes. Quel composant Cisco fournit cette donnée?**

A) Stealthwatch  
B) Cisco Talos  
C) ISE (Identity Services Engine)  
D) DNA Center  

**Réponse: B** — Talos = threat intelligence aggregation

---

### Q3: Zero-Day Malware Detection
**Un malware nouveau-zéro jour découvert sur endpoint utilisateur. Quel Cisco service l'aurait détecté dynamiquement?**

A) AMP Static Analysis  
B) Threat Grid Sandbox (behavioral detection)  
C) Antivirus signature match  
D) URL reputation, filters  

**Réponse: B** — Threat Grid = dynamic behavioral analysis

---

### Q4: AMP All Attack Phases
**Vous implémentez AMP pour protéger BEFORE, DURING, et AFTER attack. AMP composant couvre **AFTER** compromission?**

A) AMP Cloud prevention  
B) AMP Endpoints detection  
C) AMP Retrospection (disposition change)  
D) AMP Network blocking  

**Réponse: C** — AMP Retrospection = retroactive file disposition alerts

---

### Q5: Mobile VPN Security
**Sales team nécessite VPN sécurisé iPad + Stealthwatch visibilité trafic. Quel Cisco client supporte modules multiples?**

A) Cisco ASA VPN  
B) Cisco AnyConnect modulaire  
C) Cisco Umbrella seulement  
D) Cisco ISE  

**Réponse: B** — AnyConnect = modular (VPN, Posture, Stealthwatch, Umbrella)

---

### Q6: DNS-Based Cloud Defense
**Filiale accède cloud SaaS. Besoin défense 100% cloud bloquer malware domains **avant** connexion. Quel service?**

A) WSA (Web Security Appliance)  
B) Cisco Umbrella (DNS-based)  
C) Firewall ASA  
D) Content Delivery Network  

**Réponse: B** — Umbrella = DNS-level cloud defense

---

### Q7: Web Gateway Threat Detection
**Utilisateurs visitent sites avec hidden malware dans contenu. Gateway scanner analyse fichiers téléchargés. Quel Cisco appliance?**

A) NGFW Firewall  
B) WSA (Web Security Appliance)  
C) ESA (Email Security Appliance)  
D) ISE  

**Réponse: B** — WSA = web gateway malware + reputation filtering

---

### Q8: Malware Retrospection
**Fichier téléchargé marked "clean" jeudi, puis découvert "malware" vendredi (disposition change). Quel service notifie admin?**

A) Cloud AMP prevention  
B) WSA continuous scanning  
C) AMP Retrospection alerts (disposition change)  
D) Threat Grid update only  

**Réponse: C** — AMP Retrospection = retroactive alerts

---

### Q9: Multi-Source Threat Correlation
**SOC détecte: (1) endpoint malware, (2) anomalies réseau, (3) web malicious URL. Quelle plateforme corrèle ces 3 sources?**

A) Stealthwatch seulement  
B) Talos Intelligence  
C) Global Threat Analytics (GTA)  
D) DNA Center  

**Réponse: C** — GTA = analytics corrèle web+endpoints+réseau

---

### Q10: Device Compliance Before Network Access
**BYOD devices nécessitent validation antivirus/firewall activé avant réseau access. Quel contrôle?**

A) Dynamic Access Control (DAC)  
B) NAC Posture Checking  
C) Port Security  
D) MAC address filtering  

**Réponse: B** — NAC Posture (HostScan) = device compliance check

---

### Q11: ACL Implicit Deny
**Standard ACL créée: 'permit 192.168.1.0 0.0.0.255'. Interface appliquée. Tout autre trafic = action?**

A) Permit (par défaut)  
B) Deny (implicit)  
C) Log + Drop  
D) Redirect  

**Réponse: B** — Implicit deny = chaque ACL, tout non-match = bloqué

---

### Q12: Extended ACL Design
**Bloquer pings (ICMP) office vers internet, mais permettre HTTP/HTTPS. Quel type ACL minimum requis?**

A) Standard ACL (source seulement)  
B) Extended ACL (protocol + port specification)  
C) Named ACL seulement  
D) PACL  

**Réponse: B** — Extended ACL = source/dest/protocol/port control

---

### Q13: Wildcard Mask Calculation
**Subnet 192.168.10.0/25. Quelle wildcard mask?**

A) 0.0.0.127  
B) 0.0.0.255  
C) 255.255.255.128  
D) 255.255.255.255  

**Réponse: A** — /25 subnet = 255.255.255.128, wildcard = 0.0.0.127

---

### Q14: Named ACL Management
**Équipe réseau nécessite ACL facile modification (insertion ACEs sans renumbering). Solution?**

A) Numbered Standard ACL  
B) Numbered Extended ACL  
C) Named ACL (modern approach)  
D) VLAN ACL  

**Réponse: C** — Named ACL = easy modification, reordering

---

### Q15: Port ACL (PACL) Scenario
**Port access switch filtrer Layer 2 traffic spécifique port. Limitation PACL?**

A) Filtre IPv4 + IPv6  
B) Inbound + Outbound  
C) Inbound-only, ne filtre pas L2 control (CDP/VTP/DTP)  
D) Software processing  

**Réponse: C** — PACL = inbound, no L2 control bypass

---

### Q16: VLAN ACL (VACL) Use Case
**Isoler VLAN données confidentiales permettre communication spécifique. Contrôle?**

A) Port ACL seulement  
B) Interface ACL  
C) VLAN ACL (vlan access-map)  
D) Zone-based firewall  

**Réponse: C** — VACL = VLAN-wide L2 filtering

---

### Q17: ACL Processing Order
**Standard ACL config:**
```
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 permit 192.168.2.0 0.0.0.255
access-list 10 deny any
```
**Paquet source 192.168.3.0 → action?**

A) Permit (anycast rule)  
B) Deny (ACE#3 implicit match)  
C) Log then deny  
D) Matching ACE#2  

**Réponse: B** — Implicit deny = 3e match "deny any"

---

### Q18: Console Access Security
**Router console port nécessite password access control. Configuration?**

A) Line vty 0 4 password  
B) Line console 0 password  
C) TACACS+ configuration  
D) SSH setup  

**Réponse: B** — Line console 0 = local console auth

---

### Q19: Terminal Line Authentication
**5 admins nécessitent Telnet access avec usernames/passwords. Quel approche simplicité?**

A) AAA + TACACS+ (centralized)  
B) Local database (login local) + usernames  
C) CLI hardcoded password  
D) VTY password simple match  

**Réponse: B** — Login local + username = simple local DB approach

---

### Q20: Privilege Levels
**Operator role peut exécuter show + clear commands seulement. Quel privilege level + config?**

A) Level 1 (user default)  
B) Level 5 custom RBAC  
C) Level 15 (enable, full admin)  
D) Level 0  

**Réponse: B** — Level 5 custom = fine-grained permissions for operator

---

### Q21: RBAC Implementation
**Réseau 2000 devices. Assigner rôles users (admin, operator, viewer) plutôt que permissions individuelles. Approche?**

A) Per-device ACLs  
B) Role-Based Access Control (RBAC)  
C) Physical device isolation  
D) Bandwidth limiting  

**Réponse: B** — RBAC = role assignment + permissions delegation

---

### Q22: AAA Components
**AAA "Authentication" = ? "Authorization" = ? "Accounting" = ?**

A) Auth=access, Authz=identity, Acct=logging  
B) Auth=identity, Authz=access, Acct=logging  
C) Auth=logging, Authz=access, Acct=identity  
D) Identique components  

**Réponse: B** — Auth (who), Authz (what), Acct (logging)

---

### Q23: TACACS+ Server
**Enterprise déploie centralized authentication 2000 routers. Protocole AAA Cisco propriétaire?**

A) RADIUS seulement  
B) TACACS+ (Cisco propriétaire)  
C) LDAP seulement  
D) Kerberos  

**Réponse: B** — TACACS+ = Cisco propriétaire AAA

---

### Q24: AAA Method Lists
**AAA authentication attempt: TACACS+ indisponible → fallback local database. Configuration?**

A) group tacacs+ seulement  
B) group tacacs+ fallback local ou group tacacs+ local  
C) local seulement  
D) enable password  

**Réponse: B** — Method list = sequential fallback (tacacs+ → local)

---

### Q25: Zone-Based Firewall (ZBFW) Concept
**Router déploie stateful firewall par zones (inside/outside). Approche?**

A) Interface-based ACLs  
B) Zone-based firewall (ZBFW)  
C) Extended ACL seulement  
D) PACL configuration  

**Réponse: B** — ZBFW = zone-pair policies stateful

---

### Q26: ZBFW Configuration Steps
**Configurer ZBFW. Ordre étapes?**

A) Apply zone-pair → Create zones → Assign interfaces → Class-maps → Policy-maps  
B) Create zones → Assign interfaces → Class-maps → Policy-maps → Apply zone-pair  
C) Policy-maps → Class-maps → Zones → Interfaces  
D) Zones seulement, pas autre config  

**Réponse: B** — Correct order = zones → interfaces → classifications → policies → pairs

---

### Q27: Zone-Pair Direction
**Zone-pair inside→outside signifie quoi?**

A) Outside→Inside (reverse)  
B) Inside→Outside traffic direction  
C) Bidirectionnel  
D) Management traffic seulement  

**Réponse: B** — Pair direction = source→dest policy application

---

### Q28: ZBFW Policy Maps
**ZBFW class-map matches trafic, policy-map définit quelle action?**

A) Permit/deny seulement  
B) Inspect (stateful), drop, log, etc.  
C) Rate-limiting  
D) Routing decision  

**Réponse: B** — Policy-map = inspect+drop+log+other actions

---

### Q29: Control Plane Protection
**DoS attack flood CPU control-plane routing protocols destabilized. Protection?**

A) Interface ACL  
B) Control Plane Policing (CoPP)  
C) High-speed line card  
D) BGP route filtering  

**Réponse: B** — CoPP = rate-limit control-plane traffic

---

### Q30: CoPP Mechanism
**CoPP protège CPU par?**

A) Blocking tous control-plane packets  
B) Rate-limiting inbound CPU-destined packets  
C) Ignoring management traffic  
D) BGP session termination  

**Réponse: B** — CoPP = rate-limit management + routing, permit prioritized traffic

---

### Q31: CoPP Priority
**CoPP config prioritize quel traffic type?**

A) All equally  
B) SSH, OSPF, BGP, SNMP prioritaires  
C) Email traffic priority  
D) Web browsing priority  

**Réponse: B** — CoPP prioritizes critical protocols (routing, management)

---

### Q32: ACL Optimization
**Large ACL 100 entries. Best practice ordering?**

A) Random order  
B) Specific rules before general  
C) Least-used rules first  
D) Random, process same  

**Réponse: B** — Specific before general = DRY principle, efficiency

---

### Q33: Syslog ACL Logging
**ACL log sur match enable auditing. Configuration?**

A) access-list 10 permit 192.168.1.0 0.0.0.255 nolog  
B) access-list 10 permit 192.168.1.0 0.0.0.255 log  
C) IP access-group 10 log  
D) Syslog automatique  

**Réponse: B** — ACL keyword `log` = generate syslog message

---

### Q34: RBAC + AAA Combined
**Utilisateurs auth via TACACS+, assignés privilege levels (5=operator, 15=admin), command authorization checked. Architecture complète?**

A) RBAC seulement  
B) AAA seulement  
C) RBAC + AAA integrated (Authz privilege + command restrict)  
D) CLI seulement  

**Réponse: C** — RBAC+AAA = complete auth+authz+accounting

---

### Q35: NAC 802.1X Integration
**Utilisateur wifi nécessite certificat device + posture check avant accès réseau. Tech?**

A) Umbrella seulement  
B) 802.1X authentification + NAC posture  
C) MAB seulement  
D) WebAuth seulement  

**Réponse: B** — 802.1X auth + posture check = full NAC

---

### Q36: Security Posture Check
**Device notebook: antivirus X (antivirus Y requis). ISE/NAC détecte non-compliant → quarantine VLAN. Technology?**

A) Dynamic Host Configuration Protocol (DHCP)  
B) Network Admission Control (NAC) posture  
C) Port security  
D) VLAN hopping prevention  

**Réponse: B** — NAC posture = compliance enforcement

---

### Q37: SAFE Management Domain
**Infrastructure sécurité gestion supervisée centralement (policies orchestration). SAFE domain?**

A) Threat Defense Domain  
B) Compliance Domain  
C) Management Domain  
D) Segmentation Domain  

**Réponse: C** — Management Domain = orchestration supervision

---

### Q38: Segmentation Architecture
**Appliquer micro-segmentation: Finance isolée, Sales isolée, HQ interconnecté. SAFE domain?**

A) Management  
B) Segmentation Domain  
C) Security Intelligence  
D) Threat Defense  

**Réponse: B** — Segmentation Domain = architectural isolation

---

### Q39: Attack Continuum Integration
**Incident détecté: (1) malware avant delivery (BEFORE), (2) detection dynamique (DURING), (3) remediation incident response (AFTER). Architecte SAFE phase?**

A) Single phase sufficient  
B) All 3 phases integrated (complete continuum)  
C) Only BEFORE critical  
D) DURING phase seulement  

**Réponse: B** — Complete continuum coverage = before+during+after

---

### Q40: Threat Intelligence Consumption
**WSA, NGFW, AMP tous reçoivent mises à jour signatures Talos. Flux intel?**

A) Chaque produit update indépendant  
B) Talos → distribute multiples Cisco products  
C) AMP seulement → broadcast autres tools  
D) Manual updates only  

**Réponse: B** — Talos = central intel distribution

---

### Q41: AnyConnect Posture Module
**Require antivirus active, Windows Firewall on, OS patches current avant VPN connection. Feature?**

A) VPN encryption seulement  
B) AnyConnect Posture Module (HostScan)  
C) ISE Posture  
D) Umbrella DNS check  

**Réponse: B** — Posture Module = device compliance validation

---

### Q42: Stealthwatch with AnyConnect
**Utilisateur VPN connecté. Nécessite visibilité trafic utilisateur actions réseau. AnyConnect module?**

A) VPN module  
B) Stealthwatch module (visibility)  
C) Umbrella module  
D) NGFW filtering  

**Réponse: B** — Stealthwatch module = flow analytics/visibility

---

### Q43: 802.1X Port State
**Port switch: 802.1X device authentification réussie → quel VLAN access?**

A) Guest VLAN  
B) Access VLAN déterminé authentification  
C) Management VLAN  
D) Aucun (port down)  

**Réponse: B** — 802.1X success → authorized VLAN assign

---

### Q44: MAB Device Example
**Imprimante réseau NO 802.1X support. NAC access assignment?**

A) Deny access complètement  
B) MAC Authentication Bypass (MAB) → vérifier MAC registered  
C) 802.1X failover toujours requis  
D) WebAuth redirect impossible imprimante  

**Réponse: B** — MAB = MAC-based access pour devices sans 802.1X

---

### Q45: TrustSec Security Groups
**Segmentation basée confiance device plutôt que VLAN réseau. Cisco tech?**

A) VLAN tagging seulement  
B) 802.1X authentication  
C) TrustSec Security Group Tags (SGT)  
D) Port security  

**Réponse: C** — TrustSec SGTs = identity-based segmentation

---

### Q46: Compliance Auditing
**Audit trail: qui a modifié ACL quand approval? AAA accounting enregistre?**

A) Seulement changement config  
B) Authenticity + authorization + all actions (TACACS+ accounting)  
C) Rien automatique  
D) SSH session seulement  

**Réponse: B** — TACACS+ accounting = audit trail complet (who/when/what)

---

### Q47: End-to-End Security
**Utilisateur branch accès data center secure = (1) VPN SAFE access, (2) NAC compliance check, (3) ZBFW zone policy, (4) server-side ACL. Layers?**

A) Layer 1 sufficient  
B) Layers defense-in-depth (4 étudiées)  
C) Duplicate protection  
D) Conflicting policies  

**Réponse: B** — Defense-in-depth = multiple complementary layers

---

### Q48: Misconfiguration Risk
**ACL ordre:  #20 deny IP any any, #10 permit 192.168.1.0 0.0.0.255. Résultat trafic 192.168.1.0?**

A) Permit (ACE#10 match première)  
B) Deny (ACE#20 processée première)  
C) Processing ambiguity  
D) Implicit allow  

**Réponse: A** — First-match wins = ACE#10 processed first, permit

---

### Q49: Zone-Pair Traffic Flow
**Inside→Outside policy: inspect TCP. Retour Outside→Inside? Déjà tracked par?**

A) Separate policy requis  
B) Stateful = retour trafic automatiquement permitted (inside←outside track)  
C) Both directions identique  
D) Aucun retour allowed  

**Réponse: B** — Stateful firewall = tracking bi-directionnel

---

### Q50: Security Design Verification
**Infrastructure déploiement: SAFE framework, Talos intel, AMP BEFORE/DURING/AFTER, AnyConnect VPN, WSA, Umbrella, ZBF, CoPP, NAC. Verification?**

A) Fonctionnalité complète vérifiée  
B) Config validation audit trail  
C) Pilot branch deployment, vérifier threats détectées  
D) Documentation seulement  

**Réponse: C** — Field testing + threat detection validation = deployment verification
