---
title: "QCM Module 27: Virtualization"
type: qcm
module: 27
questions: 25
difficulty: certification
updated: 2026-03-18
---

# QCM: Module 27 - Virtualization
## 25 Questions - Certification Level

---

### Q1: Server Virtualization Benefit
**Quel est le principal bénéfice server virtualization?**
A) Augmentation CPU performance  
B) Consolidation multiple VMs → 1 serveur physique  
C) Réduction latence réseau  
D) Simplification CLI configuration  

**Réponse: B** — Consolidation = multiple VMs/serveur, réduction coûts

---

### Q2: VM vs Container
**Quelle est la taille image típique d'une VM?**
A) 100-500 MB  
B) 1-5 GB  
C) 5-15 GB  
D) 50-100 GB  

**Réponse: C** — VM = 5-15 GB (OS complet inclus)

---

### Q3: VM Startup Time
**Temps de démarrage típique VM?**
A) Secondes  
B) 30 secondes  
C) Minutes  
D) Heures  

**Réponse: C** — VMs démarrent en minutes

---

### Q4: Hypervisor Type 1
**Quel est exemple Hypervisor Type 1 enterprise?**
A) VMware Fusion  
B) VirtualBox  
C) VMware vSphere/ESXi  
D) Parallels Desktop  

**Réponse: C** — vSphere/ESXi = Type 1 bare metal

---

### Q5: Hypervisor Type 2
**Hypervisor Type 2 s'exécute comment?**
A) Directement sur matériel  
B) Comme application sur OS hôte  
C) En kernel mode  
D) Sans OS requis  

**Réponse: B** — Type 2 = application sur OS hôte

---

### Q6: Live Migration
**Live Migration permet quoi?**
A) Déplacer VM entre serveurs sans downtime  
B) Copier fichiers VM seulement  
C) Backup automatique VM  
D) Snapshot management  

**Réponse: A** — Live Migration = zéro downtime VM relocation

---

### Q7: High Availability
**Qu'est-ce que VM High Availability (HA)?**
A) Backup automatique  
B) Basculement automatique serveur panne  
C) Load balancing VM  
D) VM replication  

**Réponse: B** — HA = basculement serveur défaillant automatique

---

### Q8: Container Kernel
**Containers partagent quel niveau OS?**
A) Tout l'OS (complet)  
B) Kernel seulement  
C) Filesystem seulement  
D) Aucun partage  

**Réponse: B** — Containers partagent kernel Linux hôte

---

### Q9: Container Startup
**Temps de démarrage típique container?**
A) Heures  
B) Minutes  
C) Secondes  
D) Millisecondes  

**Réponse: C** — Containers démarrent secondes

---

### Q10: Container vs VM Densité
**Combien de containers vs VMs par serveur?**
A) Identique (10-20)  
B) VMs: 10-20, Containers: 100+  
C) Containers: 10-20, VMs: 100+  
D) Dépend matériel seulement  

**Réponse: B** — Containers = haute densité (100+), VMs = basse densité

---

### Q11: vSwitch Function
**Quel est rôle vSwitch?**
A) Routeur L3  
B) Commutateur L2 logiciel intra-host  
C) Firewall  
D) Load balancer  

**Réponse: B** — vSwitch = L2 software switch

---

### Q12: pNIC Role
**Quel est rôle pNIC (physical NIC) dans vSwitch?**
A) Connecter vSwitch au réseau physique externe  
B) Communication intra-VM seulement  
C) Management traffic seulement  
D) Backup seulement  

**Réponse: A** — pNIC = connexion au réseau physique

---

### Q13: Multiple vSwitches
**Si 2 vSwitches sur même serveur sans trunk, traffic entre eux?**
A) Passe par vSwitch bridge  
B) Pas de communication directe (isolation)  
C) Via management interface  
D) Via VLAN tagging automatique  

**Réponse: B** — Pas communication directe entre vSwitches (isolation)

---

### Q14: DVS Distributed Virtual Switch
**DVS agrège quoi?**
A) vSwitches sur 1 serveur  
B) vSwitches multiples serveurs → switch distribué  
C) Firewalls virtuels  
D) Hypervisors seulement  

**Réponse: B** — DVS agrège vSwitches cluster → 1 distributed switch

---

### Q15: DVS Benefit
**Quel est principal bénéfice DVS?**
A) Meilleure performance  
B) Centralized management + policy portability (migrate with VMs)  
C) Réduction VM densité  
D) Encryption automatique  

**Réponse: B** — DVS = centralized config, policy migrate avec VMs

---

### Q16: NFV Concept
**NFV (Network Functions Virtualization) découple quoi?**
A) VMs de containers  
B) Network functions du hardware dédié  
C) Hypervisors du matériel  
D) Routers de switches  

**Réponse: B** — NFV = decoupler network appliances → logiciel x86

---

### Q17: ETSI NFV Framework
**ETSI = quel organisme?**
A) Cisco propriétaire  
B) European Telecommunications Standards Institute  
C) Engineering Testing Standards International  
D) Embedded Technology Specification Initiative  

**Réponse: B** — ETSI = standards organization

---

### Q18: Cisco VNF Example
**Laquelle est Cisco VNF?**
A) VMware vSphere  
B) CSR 1000V (Cloud Services Router)  
C) Kubernetes  
D) Docker Engine  

**Réponse: B** — CSR1000v = Cisco VNF router

---

### Q19: NFVI Definition
**NFVI = quel composant NFV?**
A) Orchestrator  
B) VNF Manager  
C) Compute/Storage/Network Infrastructure  
D) Cloud management  

**Réponse: C** — NFVI = hardware + virtualization layer

---

### Q20: VIM Role
**VIM (Virtualized Infrastructure Manager) gère quoi?**
A) VNF configuration seulement  
B) Compute/Storage/Network resources + lifecycle  
C) GUI management seulement  
D) Billing et accounting  

**Réponse: B** — VIM = infrastructure resource manager + lifecycle

---

### Q21: EM/EMS FCAPS
**FCAPS = quel acronyme?**
A) Firewall, CPU, Application, Protocol, Support  
B) Fault, Configuration, Accounting, Performance, Security  
C) File, Cache, Access, Processor, Stack  
D) Firewall, Cache, Archive, Protocol, Session  

**Réponse: B** — FCAPS = management functions

---

### Q22: NFV Orchestrator Role
**NFV Orchestrator créé/maintient quel niveau services?**
A) Individual VNF functions  
B) End-to-end multi-VNF services  
C) VM hypervisor seulement  
D) Cloud infrastructure  

**Réponse: B** — Orchestrator = end-to-end service composition

---

### Q23: Service Chaining
**Service Chaining connecte quoi?**
A) Fysieke servers entre eux  
B) VNFs pour end-to-end services (ex: Router→FW→LB)  
C) Cloud providers  
D) Data centers  

**Réponse: B** — Service Chaining = VNF sequencing

---

### Q24: NFV Advantage
**Quel ist principal NFV cost advantage?**
A) Meilleure performance  
B) Réduction CapEx (hardware commodity) + OpEx (puissance/cool)  
C) Simplification management  
D) Réduction latence  

**Réponse: B** — NFV = cost reduction hardware + operational

---

### Q25: MANO Architecture
**MANO combine quel 3 composants?**
A) Controller, Manager, Agent  
B) Orchestrator, VNF Manager, VIM  
C) GUI, CLI, API  
D) Master, Slave, Backup  

**Réponse: B** — MANO = Orchestrator + VNF Manager + VIM
