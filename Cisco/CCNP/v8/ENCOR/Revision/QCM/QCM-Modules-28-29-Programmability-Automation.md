---
title: "QCM Modules 28-29: Programmability & Automation"
type: qcm
modules: [28, 29]
questions: 50
difficulty: certification
updated: 2026-03-18
---

# QCM: Modules 28-29 - Programmability & Automation
## 50 Questions - Certification Level

---

## MODULE 28: Foundational Network Programmability

### Q1: CLI Disadvantage
**Quel est principal inconvénient CLI manuel pour automation?**
A) Pas interactif  
B) Risque misconfiguration élevé, erreurs humaines scaling  
C) Performance lente  
D) Pas de feedback  

**Réponse: B** — CLI = risque humain, complexity outages

---

### Q2: API Definition
**API (Application Programming Interface) permet quoi?**
A) Chiffrement données  
B) Communication et manipulation données entre applications  
C) Management GUI uniquement  
D) Backup automation  

**Réponse: B** — API = interface communication/données

---

### Q3: Northbound API
**Northbound API va de où à où?**
A) Device → Controllers  
B) Controller → Management app  
C) CLI → Management interface  
D) Device → Device  

**Réponse: B** — Northbound = Controller → Management (upward)

---

### Q4: Southbound API
**Southbound API communique de quoi à quoi?**
A) Management → Controller  
B) Device → Device  
C) Controller → Devices (config pushdown)  
D) GUI → CLI  

**Réponse: C** — Southbound = Controller → Devices (downward)

---

### Q5: REST API
**REST API utilise quel protocole standard?**
A) SNMP  
B) HTTP methods (CRUD)  
C) SSH  
D) Telnet  

**Réponse: B** — REST = HTTP-based CRUD

---

### Q6: HTTP POST
**HTTP POST est utilisé pour quelle opération CRUD?**
A) Lire données  
B) Créer ressource  
C) Modifier ressource  
D) Supprimer ressource  

**Réponse: B** — POST = CREATE

---

### Q7: HTTP GET
**HTTP GET est utilisé pour?**
A) Ajouter ressource  
B) Lire/Récupérer ressource  
C) Remplacer ressource  
D) Supprimer  

**Réponse: B** — GET = READ

---

### Q8: HTTP PUT vs PATCH
**PUT remplace comment vs PATCH?**
A) Identical, synonymes  
B) PUT = complet, PATCH = partiel  
C) PUT = partiel, PATCH = complet  
D) PUT réseau seulement  

**Réponse: B** — PUT = replace complete, PATCH = partial update

---

### Q9: HTTP DELETE
**HTTP DELETE supprime comment la ressource?**
A) Marque supprimée seulement  
B) Suppression logique  
C) Données réellement supprimées (comme CLI)  
D) Archive seulement  

**Réponse: C** — DELETE = réelle supression (data gone)

---

### Q10: API Testing Tool
**Quel outil permet tester REST APIs sans code?**
A) CLI terminal  
B) Python script  
C) Postman applica­tion  
D) SSH client  

**Réponse: C** — Postman = API testing GUI

---

### Q11: Postman Collections
**Collections Postman fournissent quoi?**
A) History requêtes seulement  
B) Grouped API requests organization  
C) Single endpoint testing  
D) Documentation only  

**Réponse: B** — Collections = organize related requests

---

### Q12: Postman Sections
**Laquelle est NOT section Postman interface?**
A) History  
B) Collections  
C) Configuration tab  
D) New Tab  

**Réponse: C** — Configuration tab n'existe pas (sections = History, Collections, Tabs, URL Bar, etc.)

---

### Q13: JSON Format
**JSON utilise quel structure données?**
A) Tag-based (start/end)  
B) Key/value pairs, objects {}, arrays []  
C) Propriétaire XML  
D) Binary encoding  

**Réponse: B** — JSON = key-value + {objects} + [arrays]

---

### Q14: XML Structure
**XML utilise quoi pour définir données?**
A) Crochets simples []  
B) Parenthèses ()  
C) Tags start/end <tag></tag>  
D) Variables $var  

**Réponse: C** — XML = tag-based

---

### Q15: JSON vs XML
**Avantage JSON vs XML?**
A) Meilleur parsing des données complexes  
B) Plus verbeux mais meilleur pour humans  
C) Simpler, moins verbeux, parsing rapide  
D) Support meilleur pour legacy systems  

**Réponse: C** — JSON > XML pour APIs modernes

---

### Q16: HTTP Status Codes
**Quelle plage status codes indiquez succès?**
A) 1xx  
B) 2xx  
C) 3xx  
D) 4xx  

**Réponse: B** — 2xx = success (200 OK, 201 Created, etc.)

---

### Q17: HTTP 200 vs 201
**Différence 200 OK et 201 Created?**
A) Identiques  
B) 200 = GET success, 201 = POST resource created  
C) 200 = error, 201 = success  
D) 200 = delete, 201 = create  

**Réponse: B** — 200 = any success, 201 = resource created

---

### Q18: HTTP 4xx Codes
**HTTP 4xx codes indiquez quel type erreur?**
A) Server error  
B) Client error (invalid request/auth)  
C) Network error  
D) Configuration error  

**Réponse: B** — 4xx = client error

---

### Q19: 401 vs 403
**401 Unauthorized vs 403 Forbidden?**
A) Identiques  
B) 401 = no credentials, 403 = insufficient permissions  
C) 401 = server error, 403 = client error  
D) 401 = firewall block, 403 = policy block  

**Réponse: B** — 401 = auth missing, 403 = auth insufficient

---

### Q20: DNA Center Token API
**DNA Center Token API utilise quel HTTP verb?**
A) GET  
B) PUT  
C) POST  
D) DELETE  

**Réponse: C** — Token obtention = POST

---

### Q21: Token API Endpoint
**DNA Center Token API endpoint?**
A) /api/v1/Token  
B) /api/system/v1/auth/token  
C) /auth/token  
D) /api/authenticate  

**Réponse: B** — `/api/system/v1/auth/token`

---

### Q22: Token Header Usage
**Comment utiliser token après obtention?**
A) Password header  
B) Authorization header Basic Auth  
C) X-Auth-Token header  
D) Token parameter URL  

**Réponse: C** — Token dans `X-Auth-Token` header

---

### Q23: Device Inventory API
**DNA Center device inventory API méthode?**
A) POST /network-device  
B) GET /network-device  
C) PUT /network-device  
D) DELETE /network-device  

**Réponse: B** — GET /network-device pour lister devices

---

### Q24: GitHub Version Control
**GitHub fournit quoi?**
A) API testing uniquement  
B) Version control + collaboration + backup  
C) Container registry seulement  
D) DNS service  

**Réponse: B** — GitHub = version control, collaboration

---

### Q25: Python Automation
**Python est utilisé pour automatisation réseau par?**
A) Cisco seulement  
B) DevNet, Ansible, scripts custom  
C) CLI commands  
D) Hardware seulement  

**Réponse: B** — Python = popular automation language

---

## MODULE 29: Introduction to Automation Tools

### Q26: EEM Purpose
**Embedded Event Manager (EEM) permet quoi?**
A) Configuration management cloud  
B) On-device event-triggered automation, Tcl scripts  
C) Network monitoring seulement  
D) Firewall rules  

**Réponse: B** — EEM = local device automation

---

### Q27: EEM Concept
**EEM fonctionne sur modèle quoi?**
A) Master-agent  
B) Event-Action (trigger-response)  
C) Polling  
D) Heartbeat  

**Réponse: B** — EEM = événement déclenche action

---

### Q28: EEM Event Detectors
**Laquelle est EEM event detector?**
A) BGP neighbor up  
B) Syslog pattern "Interface down"  
C) CPU utilization  
D) Bandwidth threshold  

**Réponse: B** — Syslog pattern = valid detector

---

### Q29: EEM CLI Pattern
**EEM CLI pattern utilisé pour?**
A) Firewall rules matching  
B) Déclencher action quand commande spécifique exécutée  
C) Interface configuration only  
D) BGP policy  

**Réponse: B** — CLI pattern déclenche quand commande match

---

### Q30: EEM Actions
**EEM actions doivent commencer comment?**
A) Configure uniquement  
B) Enable + configure terminal  
C) Interface command  
D) Syslog message  

**Réponse: B** — EEM actions nécessitent "enable" et "configure terminal"

---

### Q31: EEM Email Notification
**Laquelle est variable EEM email valide?**
A) smtp_server  
B) notification_email  
C) from_address  
D) email_body  

**Réponse: B** — `notification_email` est variable valide

---

### Q32: Tcl in EEM
**Tcl scripts dans EEM permettent?**
A) Configuration seulement  
B) Logique complexe au-delà applets simples  
C) Routing protocols  
D) VLAN management uniquement  

**Réponse: B** — Tcl = advanced scripting

---

### Q33: EEM Avantage Over CLI
**EEM avantage vs CLI manuel?**
A) Meilleure interface graphique  
B) Réduction erreurs, réponses rapides automatiques  
C) Configuration simplifiée  
D) Moins configuration requise  

**Réponse: B** — EEM = automatisation, moins erreurs

---

### Q34: Puppet Architecture
**Puppet utilise quel architecture?**
A) Serverless  
B) Master-Agent (server-client)  
C) Agentless SSH  
D) Cloud seulement  

**Réponse: B** — Puppet = master-agent

---

### Q35: Puppet Manifests
**Puppet Manifests = quel langage?**
A) Bash  
B) Python  
C) Ruby-based DSL  
D) JSON  

**Réponse: C** — Puppet DSL = Ruby-based domain language

---

### Q36: Puppet Modules
**Puppet Module contient quoi?**
A) Manifests + Templates + Files  
B) CLI commands seulement  
C) YAML configurations  
D) Bash scripts  

**Réponse: A** — Module = Manifests (.pp) + Templates + Files

---

### Q37: Puppet Monolithic Deployment
**Puppet Monolithic deployment gère max combien agents?**
A) 100  
B) 500  
C) 2000  
D) 4000  

**Réponse: D** — Monolithic = max 4000 agents

---

### Q38: Chef Platform
**Chef est alternative quoi?**
A) Ansible  
B) Puppet (configuration management)  
C) Terraform  
D) Jenkins  

**Réponse: B** — Chef = alternative Puppet

---

### Q39: Chef Language
**Chef utilise quel(s) langage(s)?**
A) Puppet DSL  
B) Only Python  
C) Ruby + Erlang  
D) Go  

**Réponse: C** — Chef = Ruby + Erlang

---

### Q40: Ansible Agent
**Ansible require agent sur devices?**
A) Oui, obligatoire  
B) Non, agentless SSH-based  
C) Optionnel  
D) Container seulement  

**Réponse: B** — Ansible = agentless (SSH)

---

### Q41: Ansible Playbooks
**Ansible Playbooks écrit en quel format?**
A) Python  
B) Ruby  
C) YAML  
D) JSON  

**Réponse: C** — Playbooks = YAML format

---

### Q42: SaltStack Deployment
**SaltStack supporte quel(s) mode(s)?**
A) Agent-based seulement  
B) Agentless seulement  
C) Agent-based + Agentless (hybrid)  
D) Cloud seulement  

**Réponse: C** — SaltStack = hybrid (minion + SSH)

---

### Q43: Agentless Advantage
**Agentless tool advantage vs agent-based?**
A) Meilleure performance  
B) Pas d'agent installation requirement, zero footprint  
C) Moins configuration  
D) Network independance  

**Réponse: B** — Agentless = no agent install overhead

---

### Q44: Agent-Based Scalability
**Agent-based systems gèrent combien devices typically?**
A) 100  
B) 1000  
C) 10,000+  
D) Illimité  

**Réponse: B** — Agent-based ~1000 agents/master

---

### Q45: Automation Benefit
**Principal automation benefit?**
A) Meilleur interface  
B) Speed + Consistency + Risk Reduction  
C) Moins licensing  
D) Simplification interface  

**Réponse: B** — Automation = speed, consistency, risk reduction

---

### Q46: Automation Risk Reduction
**Comment automation réduit risque?**
A) Verified syntax avant deployment  
B) Humain fait moins erreurs à travers  
C) Réduction misconfiguration  
D) All above  

**Réponse: D** — Automation = validation + consistency + reduced errors

---

### Q47: Automation Speed Gain
**Speedup estimation automation vs manual 100 devices?**
A) 10% faster  
B) 50% faster  
C) 90%+ faster  
D) Identique speed  

**Réponse: C** — Automation = 90%+ time reduction

---

### Q48: Puppet PuppetDB
**PuppetDB stocke quoi?**
A) Inventory seulement  
B) Node facts, catalogs, reports, metrics  
C) Firewall rules  
D) Passwords encrypted  

**Réponse: B** — PuppetDB = central repository device data

---

### Q49: Tool Selection Criteria
**Pour quick deployment agentless préféré ou agent?**
A) Agent-based (meilleur)  
B) Agentless (rapid no install)  
C) Identique avantage  
D) Depends on cloud only  

**Réponse: B** — Agentless = immediate, no setup

---

### Q50: Automation Evolution
**Latest generation automation trend?**
A) CLI scripts seulement  
B) EEM/Puppet dominance  
C) Ansible/GitOps/Infrastructure as Code  
D) Manual configuration preferred  

**Réponse: C** — Modern trend = IaC + GitOps
