---
title: "QCM Modules 25-26: Security & Access Control"
type: qcm
modules: [25, 26]
questions: 50
difficulty: certification
updated: 2026-03-18
---

# QCM: Modules 25-26 - Security & Access Control
## 50 Questions - Certification Level

---

## MODULE 25: Secure Network Access Control

### Q1: SAFE Framework - PINs
**Cisco SAFE Framework couvre 6 Physical Infrastructure Networks (PINs). Laquelle des suivantes est PAS un PIN SAFE?**

A) Data Center PIN  
B) Campus PIN  
C) Application PIN  
D) Cloud PIN  

**Réponse: C** — Application n'est pas SAFE PIN. Les 6 PINs sont: Branch, Campus, Data Center, Edge, Cloud, WAN

---

### Q2: SAFE Domains
**Laquelle des 6 SAFE Domains se concentre sur conformité et gouvernance?**

A) Management Domain  
B) Compliance Domain  
C) Segmentation Domain  
D) Security Intelligence Domain  

**Réponse: B** — Compliance Domain gère gouvernance et audit

---

### Q3: Attack Continuum
**Dans Attack Continuum, quelle phase inclut "patch et remediation"?**

A) BEFORE (Prévention)  
B) DURING (Détection)  
C) AFTER (Remédiation)  
D) Toutes les phases  

**Réponse: C** — AFTER phase inclut remediation après compromission

---

### Q4: Cisco Talos
**Combien de sources Talos agrège pour threat intelligence?**

A) 3 sources  
B) 5 sources  
C) 7+ sources  
D) 10+ sources  

**Réponse: C** — Talos utilise 7+ sources (Microsoft, honeypots, AEGIS, Threat Grid, etc.)

---

### Q5: Threat Grid Sandbox
**Quel est le nom de l'environnement sandbox propriétaire Cisco dans Threat Grid?**

A) Sandbox VM  
B) Glovebox  
C) ThreatBox  
D) AnalysisLab  

**Réponse: B** — Glovebox est l'environnement sandbox Threat Grid

---

### Q6: Threat Grid Deployment
**Cisco Threat Grid peut être déployé de deux façons. Laquelle est appropriée pour données sensibles?**

A) Cloud-based seulement  
B) On-premises appliance  
C) Les deux identiquement  
D) Aucune (TG obligatoirement cloud)  

**Réponse: B** — On-premises appliance pour données sensibles

---

### Q7: AMP Architecture
**AMP for Endpoints sur iOS s'appelle comment?**

A) iOS AMP  
B) Cisco iOS Security  
C) Cisco Security Connector (CSC)  
D) AMP for Mobile  

**Réponse: C** — CSC est l'agent AMP sur iOS (limitation Apple)

---

### Q8: AMP Components
**Lequel des suivants N'EST PAS un composant AMP?**

A) AMP Cloud  
B) AMP for Endpoints  
C) AMP for Networks  
D) AMP for Infrastructure  

**Réponse: D** — AMP for Infrastructure n'existe pas. Les vrais: Cloud, Endpoints, Networks, Email, Web, Meraki

---

### Q9: AnyConnect Modules
**Laquelle des modules AnyConnect fournit visibilité trafic endpoint?**

A) Posture Module  
B) Stealthwatch Module  
C) VPN Module  
D) Umbrella Module  

**Réponse: B** — Stealthwatch Module fournit visibilité trafic

---

### Q10: AnyConnect Protocols
**AnyConnect supporte quel(s) protocole(s) de chiffrement?**

A) TLS/SSL seulement  
B) IPsec IKEv2 seulement  
C) TLS/SSL + IPsec IKEv2  
D) PPTP + IPsec  

**Réponse: C** — AnyConnect utilise TLS/SSL + IPsec IKEv2 (redondance)

---

### Q11: Cisco Umbrella
**Cisco Umbrella fournit défense basée sur quel niveau?**

A) Layer 7 (Application)  
B) Layer 4 (Transport)  
C) Layer 3 (DNS/Network)  
D) Layer 2 (L2)  

**Réponse: C** — Umbrella est DNS-based defense (Layer 3)

---

### Q12: Umbrella Global Data Centers
**Combien de global data centers Umbrella maintient?**

A) 10  
B) 20  
C) 30  
D) 50  

**Réponse: C** — Umbrella maintient 30 global data centers

---

### Q13: Umbrella Anycast DNS
**Quel technologie Umbrella utilise pour garantir latence basse?**

A) GeoDNS  
B) Anycast DNS  
C) Unicast optimisé  
D) CDN clustering  

**Réponse: B** — Anycast DNS pour routage vers data center le plus proche

---

### Q14: WSA Before Attack
**Laquelle des suivants est protection WSA "BEFORE" attack?**

A) AMP Retrospection  
B) Continuous Scanning  
C) Web Reputation Filters  
D) Disposition Change Alerts  

**Réponse: C** — Web Reputation Filters = BEFORE protection

---

### Q15: WSA During Attack
**Laquelle des technologies WSA fournit détection zero-day?**

A) URL Filtering  
B) Malware Inspection heuristique  
C) Application Control  
D) Web Reputation  

**Réponse: B** — Heuristiques détectent zero-days

---

### Q16: WSA After Attack
**Quelle fonction WSA "AFTER" attack notifie administrateur sur malware retrouvé?**

A) Disposition Change Alerts  
B) Retrospection Scanning  
C) File Reclassification  
D) AMP Update Notification  

**Réponse: A** — Disposition Change Alerts notifient quand "clean" → "malware"

---

### Q17: WSA Deployment
**WSA peut être déployé dans combien de modèles?**

A) 1 (on-prem seulement)  
B) 2 (cloud ou virtual)  
C) 3 (cloud, virtual, on-prem)  
D) 4+ (multiple options)  

**Réponse: C** — Cloud, Virtual, On-Prem

---

### Q18: Global Threat Analytics (GTA)
**GTA corrèle données de combien de sources?**

A) Web browsing seulement  
B) Endpoints seulement  
C) Network seulement  
D) Web + Endpoints + Network (3 sources)  

**Réponse: D** — GTA corrèle 3 sources: web, endpoints, network

---

### Q19: NAC - 802.1X
**Laquelle des technologies NAC vérifie conformité device (antivirus, firewall, patches)?**

A) WebAuth  
B) MAB  
C) Posture Checking  
D) TrustSec  

**Réponse: C** — Posture Checking (HostScan en AnyConnect) vérifie conformité

---

### Q20: NAC - MAB
**MAC Authentication Bypass (MAB) est utilisé pour quel type de devices?**

A) Laptops et desktops  
B) Téléphones (802.1X capable)  
C) Devices non-802.1X (imprimantes, photocopieuses)  
D) Smartphones seulement  

**Réponse: C** — MAB pour devices sans 802.1X (imprimantes, etc.)

---

## MODULE 26: Network Device Access Control & Infrastructure

### Q21: ACL Processing
**Dans quel ordre les ACEs sont-elles évaluées?**

A) Random order  
B) Bottom to top  
C) Top to bottom (first-match)  
D) Selon importance  

**Réponse: C** — ACEs évaluées top-to-bottom, first match wins

---

### Q22: Implicit Deny
**Quelle est l'action implicite à fin de toute ACL si pas de match?**

A) Permit (par défaut)  
B) Deny (implicite)  
C) Log et deny  
D) Continue évaluation  

**Réponse: B** — Implicit deny à fin de toute ACL

---

### Q23: Standard ACL Numbers
**Quels sont les ranges de numéros Standard ACL?**

A) 1-99 et 1300-1999  
B) 100-199 et 2000-2699  
C) 1-199  
D) 2000-2999  

**Réponse: A** — Standard ACL: 1-99 et 1300-1999

---

### Q24: Extended ACL Numbers
**Quels sont les ranges de numéros Extended ACL?**

A) 1-99 et 1300-1999  
B) 100-199 et 2000-2699  
C) 1-199  
D) 2000-2999  

**Réponse: B** — Extended ACL: 100-199 et 2000-2699

---

### Q25: Standard vs Extended ACL
**Standard ACL peut filtrer sur quel(s) paramètre(s)?**

A) Source seulement  
B) Source et Destination  
C) Source, Dest, Protocol, Port  
D) Toute information L3-L4  

**Réponse: A** — Standard ACL = source seulement

---

### Q26: Wildcard Mask Calculation
**Si subnet mask est 255.255.255.0, qual est wildcard mask?**

A) 255.255.255.0  
B) 0.0.0.255  
C) 0.0.0.0  
D) 255.255.255.255  

**Réponse: B** — Wildcard = 255.255.255.255 - 255.255.255.0 = 0.0.0.255

---

### Q27: Named ACLs
**Quel est l'avantage principal des Named ACLs vs Numbered ACLs?**

A) Meilleure performance  
B) Noms descriptifs, insertion/suppression faciles  
C) Moins configuration requise  
D) Moins de lignes config  

**Réponse: B** — Named ACLs permettent noms descriptifs + modification facile

---

### Q28: ACL Application
**Combien d'ACLs inbound peuvent être appliquées sur une interface simple?**

A) 0  
B) 1  
C) 2  
D) Illimité  

**Réponse: B** — Max 1 inbound + 1 outbound par interface

---

### Q29: PACL Restrictions
**Quel est la principale restriction PACLs (Port ACLs)?**

A) Seulement IPv4  
B) Inbound-only, ne filtre pas L2 control protocols  
C) Performance faible  
D) Support limited devices  

**Réponse: B** — PACLs inbound-only, ne filtre pas CDP/VTP/DTP/PAgP/UDLD/STP

---

### Q30: PACL L2 Control Bypass
**Pourquoi les protocoles L2 control (CDP, VTP) bypass PACLs?**

A) Trop importants pour filtrer  
B) PACLs hardware-only, L2 control au-delà ACLs  
C) Cisco design choice uniquement  
D) Pour interoperability  

**Réponse: B** — L2 control = critical infrastructure, bypass ACLs

---

### Q31: VACL Match Actions
**Quelles sont les deux actions VACL?**

A) Permit et Deny  
B) Forward et Drop  
C) Allow et Discard  
D) Pass et Block  

**Réponse: B** — VACL actions sont Forward et Drop

---

### Q32: VACL Application Scope
**VACLs s'appliquent à quel scope?**

A) Interfaces seulement  
B) Toute VLAN ou groupes VLAN  
C) Virtual Machines seulement  
D) Distribution layer seulement  

**Réponse: B** — VACLs appliquées à VLAN entière ou groupes VLANs

---

### Q33: Terminal Line Passwords
**Laquelle des lignes nécessite password pour accès distance?**

A) Line console 0  
B) Line vty 0 4  
C) Line aux 0  
D) Line tty 1  

**Réponse: B** — Line vty 0 4 pour Telnet/SSH access

---

### Q34: Local Authentication
**Laquelle des configurations fournit authentication locale sans AAA?**

A) AAA new-model  
B) Tacacs+ server  
C) Username + login local  
D) Line password seulement  

**Réponse: C** — Username + login local = local DB auth

---

### Q35: Privilege Levels
**Quel privilege level correspond "enable" mode?**

A) Level 0  
B) Level 1  
C) Level 15  
D) Level 7  

**Réponse: C** — Level 15 = enable mode (full admin)

---

### Q36: Custom Privilege Levels
**Quel range de privilege levels sont custom (non-predefined)?**

A) 0-1  
B) 2-14  
C) 15  
D) 16-255  

**Réponse: B** — Custom levels 2-14

---

### Q37: RBAC Definition
**Role-Based Access Control (RBAC) assigne permissions basé sur quoi?**

A) IP address  
B) Device hostname  
C) User role/group  
D) Timestamp  

**Réponse: C** — RBAC assigne permissions selon user role

---

### Q38: AAA Components
**Dans AAA, "Authorization" détermine quoi?**

A) Qui es-tu? (identity)  
B) Que peux-tu faire? (permissions)  
C) Quoi as-tu fait? (logging)  
D) Configuration management  

**Réponse: B** — Authorization = permissions/privileges

---

### Q39: TACACS+ Protocol
**TACACS+ est quel type de serveur AAA?**

A) Radius seulement  
B) Cisco propriétaire  
C) Open-source universel  
D) Microsoft propriétaire  

**Réponse: B** — TACACS+ est Cisco propriétaire

---

### Q40: ZBFW Concept
**Zone-Based Firewall s'applique par quoi?**

A) Par interface  
B) Par direction (in/out)  
C) Par zones de sécurité  
D) Par VLAN  

**Réponse: C** — ZBFW appliqué par zones (inside,outside,dmz)

---

### Q41: ZBFW Stateful Inspection
**ZBFW fournit quel type d'inspection?**

A) Stateless seulement  
B) Stateful (tracking connexions)  
C) Application-level seulement  
D) Policy-based seulement  

**Réponse: B** — ZBFW fournit stateful inspection

---

### Q42: Zone-Pair Direction
**Dans zone-pair, quel est le rôle du "source" et "destination"?**

A) Sens traffic flow  
B) Policy application direction  
C) Input vs output  
D) Primary vs backup  

**Réponse: B** — source→destination détermine policy direction

---

### Q43: ZBFW Components
**Laquelle est composant ZBFW config?**

A) Zones, Zone-pairs, Class-maps, Policy-maps  
B) Routes, VLANs, Subnets  
C) TCP states, SQL rules  
D) BGP neighbors, OSPF areas  

**Réponse: A** — ZBFW components: zones, zone-pairs, class-maps, policy-maps

---

### Q44: CoPP Purpose
**Control Plane Policing (CoPP) protège quel composant du routeur?**

A) Line card  
B) Interface  
C) Route Processor (CPU)  
D) Memory  

**Réponse: C** — CoPP protège Route Processor (CPU)

---

### Q45: CoPP DoS Scenario
**Dans quel scénario CoPP est vraiment critique?**

A) Backup data transfer  
B) Normal routing operations  
C) DoS/flooding attack vers CPU  
D) Bandwidth utilization management  

**Réponse: C** — CoPP critique contre DoS CPU flooding

---

### Q46: CoPP Configuration Step
**Quel est le premier step pour configurer CoPP?**

A) Apply zone-pair  
B) Create ACLs classifier packets  
C) Enable policy-map  
D) Configure control-plane  

**Réponse: B** — First step = créer ACLs pour classifier (SSH, routing, etc.)

---

### Q47: CoPP Application
**Sur quel composant CoPP s'applique?**

A) Interface Ethernet0/0  
B) Control-plane  
C) BGP router  
D) VLAN interface  

**Réponse: B** — CoPP appliqué sur `control-plane`

---

### Q48: ACL Order Importance
**Pourquoi l'ordre des ACEs est-il critique?**

A) Pour lisibilité seulement  
B) First-match processing (pas réévaluation)  
C) Pour performance  
D) Pour backup/restore  

**Réponse: B** — First matching ACE wins, pas d'évaluation suite

---

### Q49: Access Control Strategy
**Quelle est la meilleure pratique ACL?**

A) Placer "deny any" au début  
B) Placer "permit any" à fin  
C) Ordre des règles = specific avant general  
D) Randomize les règles  

**Réponse: C** — Specific before general (DRY principle)

---

### Q50: Terminal Security End-to-End
**Laquelle est séquence complète authentication terminal?**

A) Password → Privilege level → Command execution  
B) Username → Password → Privilege level → AAA check  
C) AAA → Password → Privilege → Command authorization  
D) RBAC → Privilege → Username → Password  

**Réponse: C** — AAA (identity) → Password (security) → Privilege (authorization) → Command checked
