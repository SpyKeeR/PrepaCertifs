---
title: "Checkpoint CP11: Virtualization, Programmability & Automation (Modules 27-29)"
type: checkpoint
checkpoint: 11
modules: [27, 28, 29]
questions: 50
difficulty: certification
updated: 2026-03-18
---

# Checkpoint CP11: Virtualization, Programmability & Automation
## 50 Certification-Level Questions

---

### Q1: Consolidation Scenario
**Entreprise 500 devices: routers, switches, firewalls physiques. Coût capex/opex élevé puissance/refroidissement. Strategy modernisé?**

A) Acheter plus devices physiques  
B) NFV sur x86 commodity servers  
C) Désactiver dispositifs  
D) Manuel CLI configuration  

**Réponse: B** — NFV = consolidation x86 servers, cost reduction

---

### Q2: VM vs Container Trade-off
**Application modernization: rapid deployment + isolat légère versus. Choix?**

A) VMs (5-15 GB, minutes startup)  
B) Containers (100-500 MB, secondes) pour agilité  
C) Bare metal (meilleure performance)  
D) Mainframe legacy  

**Réponse: B** — Containers = rapid deployment = modern best practice

---

### Q3: Hypervisor Selection
**Production environment 1000 VMs vMotion + HA critical. Type 1 ou Type 2?**

A) Type 2 VMware Fusion (desktop)  
B) Type 1 VMware vSphere/ESXi (bare metal)  
C) Hyper-V seulement  
D) VirtualBox open-source  

**Réponse: B** — Type 1 = production grade (vSphere, HA/vMotion)

---

### Q4: vSwitch Isolation
**Datacenter 2 vSwitches: vSwitch0 (production), vSwitch1 (management). Communication direct possible?**

A) Oui, par pNIC bridge  
B) Non, isolation (separate switches/pNICs)  
C) Oui, via management interface  
D) Only avec VLAN tagging  

**Réponse: B** — vSwitch isolation = no direct inter-vSwitch traffic

---

### Q5: Distributed Virtual Switch (DVS)
**Cluster 10 ESXi servers géré individuellement vSwitches different. Impact VM migration + policies?**

A) Policies consistent cluster-wide  
B) Inconsistency (per-server config different)  
C) Policies reset après migration  
D) Manual reconfiguration post-vMotion  

**Réponse: B** — Without DVS = inconsistency, DVS = centralized policy + portability

---

### Q6: Container Networking
**Container 3+ nécessite communication. Technologie?**

A) Direct vSwitch connection  
B) Virtual Ethernet pairs (veth) + bridge (docker0)  
C) Physical cable chaque container  
D) NAT uniquement  

**Réponse: B** — veth + bridge = container L2 networking

---

### Q7: NFV Enterprise Example
**Branch 50 WAN sites: Cisco router + firewall + LB physiques à chaque site. Consolidation NFV?**

A) Ajouter plus appliances  
B) Une x86 server/site, CSR1000v + ASAv + VNF LB virtualisé  
C) Eliminer security  
D) Retain appliances  

**Réponse: B** — NFV consolidation = VNF service chaining single server

---

### Q8: NFVI Components
**Virtualisation réseau infrastructure comprendre quel(s) composant(s)?**

A) VNF seulement  
B) Compute/Storage/Network + hypervisor (KVM/vSphere)  
C) Cloud applications uniquement  
D) CLI tooling  

**Réponse: B** — NFVI = infrastructure platform (compute+storage+network+hypervisor)

---

### Q9: VIM Responsibility
**Cluster 20 servers gérer dynamiquement déploiement multi-VNF service. Manager?**

A) Manual resource allocation  
B) VIM (resource manager, lifecycle, chaining)  
C) EEM automation  
D) SNMP monitoring seulement  

**Réponse: B** — VIM = automatic infrastructure management

---

### Q10: Service Chaining Scenario
**Branch nécessite: routing (CSR) → firewall (ASAv) → WAN optimization (VNF). Order?**

A) ASAv → CSR (reverse)  
B) CSR → ASAv → WAN optimization (correct sequence)  
C) WAN opt → firewall → router  
D) All parallel  

**Réponse: B** — Service chain = ordered VNF sequence

---

### Q11: MANO Architecture
**Déployer dynamiquement multi-VNF service, configuration VNF, ressources. Components?**

A) Orchestrator + VNF Manager + VIM (MANO)  
B) Orchestrator seulement  
C) VIM seulement  
D) Manual config  

**Réponse: A** — MANO = Orchestrator+VNF Manager+VIM combined

---

### Q12: CLI vs Automation Problem
**Network admin 100 ACLs configuration manuelle → erreur, config inconsistent. Solution?**

A) Utiliser CLI plus careful  
B) Automation tool (template-driven ACL)  
C) Multiple admins review  
D) Disable ACLs  

**Réponse: B** — Automation = consistency, error reduction

---

### Q13: Northbound API
**Management app GUI besoin requête device list. Direction API?**

A) Southbound (device config)  
B) Northbound (controller → mgmnt)  
C) East-West (peer-to-peer)  
D) Management interface seulement  

**Réponse: B** — Northbound = upward (controller → management)

---

### Q14: REST API CRUD
**DNA Center API requête: créer nouveau device. Quel HTTP verb?**

A) GET  
B) POST (create resource)  
C) PUT  
D) DELETE  

**Réponse: B** — POST = CREATE

---

### Q15: Postman API Testing
**Tester DNA Center API sans Python script. Tool?**

A) Excel spreadsheet  
B) Postman application (GUI API testing)  
C) SSH terminal  
D) Cisco CLI  

**Réponse: B** — Postman = interactive API testing

---

### Q16: JSON Data Format
**API response format JSON: 'devices': [{id, hostname, ip},…]. Structure?**

A) Key-value pairs, nested objects [], arrays  
B) XML tags <tag></tag>  
C) CSV comma-separated  
D) Binary encoding  

**Réponse: A** — JSON = objects + arrays + key-value

---

### Q17: HTTP Status Code
**POST request créer device succès. Expected HTTP response code?**

A) 200 OK  
B) 201 Created (resource création)  
C) 204 No Content  
D) 400 Bad Request  

**Réponse: B** — 201 = resource creation success

---

### Q18: Authentication Token
**DNA Center Token API obtention. Usage subsequent requests?**

A) Basic Auth répétée  
B) X-Auth-Token header (token)  
C) Username/password inline  
D) No auth needed after first  

**Réponse: B** — Token dans header X-Auth-Token

---

### Q19: API Rate Limiting
**DNA Center API 100 devices requête séquentiel rapide = risque. Problème?**

A) API successful response  
B) DDos protection = 429 Too Many Requests  
C) Matériel overload  
D) Network congestion  

**Réponse: B** — Rate limiting = protect API server

---

### Q20: GitHub Collaboration
**Équipe réseau collaborate Ansible playbooks, track versions, code review. Platform?**

A) Email attachments  
B) GitHub (version control+collaboration)  
C) Excel shared  
D) FTP server  

**Réponse: B** — GitHub = version control + collaboration

---

### Q21: Python Automation Advantage
**Script Python call DNA Center API, parse results JSON, provision devices bulk. Benefit vs CLI?**

A) Identique speed  
B) Automation = 90%+ speed, consistency, error elimination  
C) CLI meilleur  
D) Manuel preferable  

**Réponse: B** — Automation = rapid, consistent, reliable

---

### Q22: EEM Event Trigger
**Router interface Lo0 tombe (syslog "Interface Loopback0 down") → automat reset. Technology?**

A) Manual CLI restart  
B) EEM applet event-triggered action  
C) Periodic polling only  
D) SNMP trap ignored  

**Réponse: B** — EEM = event-driven automation

---

### Q23: EEM Action Configuration
**EEM applet execute CLI commands shutdown/no shutdown interface. Required syntax?**

A) Direct CLI seulement  
B) Action 0 enable, Action 1 configure terminal, then CLI  
C) Syslog message seulement  
D) Script perl/bash  

**Réponse: B** — EEM actions requièrent "enable" + "configure terminal"

---

### Q24: Tcl in EEM
**EEM applet complexe: loop VLAN configuration, conditional logic. Nécessité?**

A) Applet seulement  
B) Tcl scripting (langage scripting EEM)  
C) Bash scripts  
D) Python external  

**Réponse: B** — Tcl = EEM advanced scripting

---

### Q25: EEM Email Notification
**Incident détecté, admin notifiée email. EEM config?**

A) Syslog message uniquement  
B) Email variables (notification_email, email_server, email_subject)  
C) No notification capability  
D) Manual email alert  

**Réponse: B** — EEM email variables = automated notification

---

### Q26: Puppet Master-Agent
**Enterprise 4000 routers configuration management. Architecture?**

A) Single master (monolithic, max 4000 agents)  
B) Master of Masters (MoM) + compile masters load-balanced  
C) Manual per-device  
D) Agentless  

**Réponse: B** — Large-scale Puppet = MoM + compile master architecture

---

### Q27: Puppet Manifests Language
**Puppet manifests (.pp files) écrit quel langage DSL?**

A) Bash  
B) Python  
C) Ruby-based DSL  
D) JSON  

**Réponse: C** — Puppet = Ruby-based domain-specific language

---

### Q28: Puppet Module Structure
**Puppet module organisation?**

A) Single configuration file  
B) Manifests (.pp) + Templates + Files (modular structure)  
C) Python scripts  
D) Bash seulement  

**Réponse: B** — Module = Manifests + Templates + Files

---

### Q29: Chef Configuration Management
**Alternative Puppet plus flexible Ruby-based. Quel tool?**

A) Ansible  
B) Chef  
C) SaltStack  
D) Terraform  

**Réponse: B** — Chef = alternative Puppet

---

### Q30: Ansible Agentless Advantage
**Déployer automation 100 legacy routers, pas agent installation capable. Solution?**

A) Agent-based Puppet (must install)  
B) Agentless Ansible (SSH exists only)  
C) Manual CLI change  
D) Retire devices  

**Réponse: B** — Agentless = no install overhead, immediate deployment

---

### Q31: Ansible Playbooks
**Ansible Playbooks décrit automatisation. Format?**

A) Python scripts  
B) YAML human-readable format  
C) JSON binary  
D) Cisco CLI  

**Réponse: B** — Playbooks = YAML syntax

---

### Q32: Agent-Based Architecture
**Puppet agents 1000 routers report → master server centralized. Scalability concern?**

A) Unlimited agents manageable  
B) master peut gérer ~1000 agents (per-master limit)  
C) Agents infinité seulement  
D) Matériel no limit  

**Réponse: B** — Master scalability ~1000 agents típico

---

### Q33: SaltStack Hybrid
**SaltStack supporte both agent (Salt Minion) et agentless (Salt SSH). Flexibility?**

A) Agent-based seulement  
B) Agentless seulement  
C) Hybrid (choose per-deployment)  
D) Cloud seulement  

**Réponse: C** — SaltStack = hybrid flexibility

---

### Q34: Automation Speed Benefit
**Configuration 100 routers manually 100 hours vs automation 5 hours. Gain?**

A) 10% faster  
B) 50% faster  
C) 95% time reduction!  
D) Identique speed  

**Réponse: C** — Automation typically 95%+ faster

---

### Q35: Configuration Consistency
**Manual config by human A inconsistent human B. Automation outcome?**

A) Identique inconsistency  
B) All devices identical config (consistency)  
C) More errors  
D) Unpredictable  

**Réponse: B** — Automation = guaranteed consistency (templates)

---

### Q36: Risk Reduction
**Configuration typo router → interface shutdown → 1 hour outage ($50K loss). Prevention?**

A) More careful human (same risk)  
B) Automation syntax validation before deploy  
C) Manual review (time consuming)  
D) Accept outage  

**Réponse: B** — Automation validation = zero typo risk

---

### Q37: Compliance Auditing
**Qui a changé ACL quand approval history? Automation logging?**

A) Manual check impossible  
B) Automation logs (who/when/what approved)  
C) Guess based  
D) No audit trail  

**Réponse: B** — Automation audit trail = compliance evidence

---

### Q38: Tool Selection Decision
**Quick deployment 10 switches, no agent. Tool?**

A) Puppet master-agent (slow setup)  
B) Chef (complex)  
C) Ansible agentless (rapid SSH)  
D) Manual CLI  

**Réponse: C** — Agentless = best quick deployment

---

### Q39: Puppet PuppetDB
**Puppet nodes centralized data storage fatos, catalogs, reports. Système?**

A) Individual config files  
B) PuppetDB (central repository)  
C) Filesystem only  
D) SNMP traps  

**Réponse: B** — PuppetDB = central node intelligence

---

### Q40: EEM Use Case
**Simple automation: CONFIG_BACKUP applet détecte "write memory" → backup TFTP. Oul?**

A) Manual backup seulement  
B) EEM CLI pattern applet (local automation)  
C) Puppet required  
D) Cloud service  

**Réponse: B** — EEM perfect for simple local event-driven tasks

---

### Q41: Automation Dependency
**Puppet master unavailable → agents continue working. Expected?**

A) Agents stop sans master  
B) Agents maintain config cached (resilient)  
C) Network down  
D) No impact  

**Réponse: B** — Agent resilience = cached config continues

---

### Q42: Cloud Programmability
**DNA Center controller nécessite REST API intégration cloud SaaS app. Direction?**

A) Southbound (devices)  
B) Northbound (external app → controller)  
C) CLI seulement  
D) Propriétaire integration  

**Réponse: B** — Northbound API = cloud integration

---

### Q43: CI/CD Automation Pipeline
**Code Ansible playbook → validation syntax → test VLAN lab → production deployment. Workflow?**

A) Manual steps  
B) Gitops/CI-CD continuous integration  
C) Monthly scheduled  
D) No testing  

**Réponse: B** — CI/CD pipeline = automated validation + deployment

---

### Q44: Orchestration Complexity
**100 VNFs déployées, multi-service en parallèle, resource allocation auto. Outil NFV?**

A) Manual VNF deployment  
B) NFV Orchestrator (automated end-to-end)  
C) VIM seulement  
D) SSH scripts  

**Réponse: B** — Orchestrator = complex service automation

---

### Q45: IaC (Infrastructure as Code)
**Entière réseau infrastructure (VMs, VNFs, configs) décrit fichiers code versionned. Approche?**

A) Manual documentation  
B) Infrastructure as Code (IaC) + version control  
C) GUI clickops  
D) Verbal configuration  

**Réponse: B** — IaC = predictable, reproducible, versionned

---

### Q46: Microservices Deployment
**Application microservices 50 containers, auto-scaling traffic spikes. Orchestration?**

A) Manual container management  
B) Kubernetes orchestration  
C) Docker run commands  
D) No scaling  

**Réponse: B** — Kubernetes = container orchestration at scale

---

### Q47: Configuration Template
**100 sitess identical config différent IP/VLAN/neighbors. Approach?**

A) 100 separate config files identical  
B) Template + variable substitution (automation)  
C) Manual per-site  
D) Copy-paste error-prone  

**Réponse: B** — Templates = reusable configuration scale

---

### Q48: Intelligent Automation
**Système détecte capacity utilisation trending → proactive provision additional VMs. Technology?**

A) Manual monitoring  
B) Analytics + automation (intelligent scaling)  
C) Reactive seulement  
D) No prediction  

**Réponse: B** — Analytics-driven automation = proactive management

---

### Q49: Zero-Trust Automation
**New endpoint joining nécessite dynamically micro-segmentation policy application. Automation?**

A) Manual policy per device  
B) Automation + identity-based policies (TrustSec SGTs)  
C) Open network  
D) Static policies  

**Réponse: B** — Automation + identity = zero-trust implementation

---

### Q50: Operational Excellence
**Infrastructure: EEM local events + Puppet enterprise + Ansible cloud + DNA Center orchestration. Integration complète?**

A) Separate tools conflicting  
B) Integrated automation stack (layered automation)  
C) Complexity non-necessary  
D) Manual management better  

**Réponse: B** — Layered automation = on-device + enterprise + cloud + orchestration
