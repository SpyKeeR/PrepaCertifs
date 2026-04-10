---
title: "Fiche Module 27: Virtualization"
type: fiche
module: 27
topics: [VM, Containers, Hypervisor, vSwitch, NFV, NFVI, VNF, VIM, MANO]
difficulty: advanced
updated: 2026-03-18
---

# Fiche Synthèse: Module 27 - Virtualization

## Virtualisation Serveur: Concepts Core

### Problem Statement
- **Before**: 1 device = 1 OS = 60% CPU average utilization = gaspillage
- **After**: Consolidation: 10-20 VMs/serveur physique = utilisation 80%+ = cost reduction

### Types de Virtualisation
1. **Server Virtualization**: VMs exécutant OSs complets (Windows/Linux)
2. **Container Virtualization**: Applications légères, OS partagé kernel
3. **Network Functions Virtualization (NFV)**: Network appliances virtualisées

---

## Virtual Machines (VMs)

### Définition & Composants
- **Emulation logicielle** complète serveur physique (matériel + OS)
- **Taille image**: 5-15 GB
- **RAM**: 2-4 GB typical
- **Startup**: minutes
- **OS invité**: Windows, Linux, possibilité coexistence

### VM Avantages
1. **Live Migration**: déplacer VMs entre serveurs sans downtime
2. **High Availability (HA)**: basculement automatique serveur défaillant
3. **Consolidation**: consolidation matériel, coût réduit

---

## Hypervisors

### Type 1: Bare Metal (Production)
Exécuté directement sur matériel (pas OS hôte requis)
- **VMware vSphere/ESXi**: leader marché, HA/vMotion advanced
- **Microsoft Hyper-V**: intégration Windows Server
- **Citrix XenServer**: alternative
- **Red Hat KVM**: open-source, Linux-based

```
[Hypervisor Type 1]
├─ VM1 [Linux]
├─ VM2 [Windows]
└─ VM3 [Appliance]
[Physical Hardware]
```

### Type 2: Hosted (Desktop Testing)
Exécuté comme application sur OS hôte
- **VMware Fusion**: Apple macOS
- **VirtualBox**: cross-platform
- **Limitation**: performance (passe par OS hôte)

---

## Containers: Alternative Légère

### Concept
- **Application + dépendances** sans OS complet
- **OS kernel partagé** (Linux) 
- **Taille image**: 100-500 MB
- **Startup**: secondes
- **Runtime**: Docker, containerd

```
[Container Runtime]
├─ Container1 [App + Libs]
├─ Container2 [App + Libs]
└─ Container3 [App + Libs]
[Shared Linux Kernel]
```

### VM vs Container Comparison

| Aspect | VM | Container |
|--------|----|---------  |
| **OS** | Complet (5-15 GB) | Partagé kernel |
| **Démarrage** | Minutes | Secondes |
| **Overhead** | Élevé | Faible |
| **Densité** | 10-20 / serveur | 100+ / serveur |
| **Isolation** | Complète | Procédés |

---

## Virtual Networking: vSwitches

### vSwitch (Virtual Switch)
- **Layer 2 logiciel** commutateur
- **Intra-host communication**: entre VMs
- **Externe access**: via pNIC (physical NIC)
- **VLAN tagging**: 802.1Q support

```
[Hypervisor]
├─ vSwitch0 → pNIC0 → Production Network
├─ vSwitch1 → pNIC1 → Management Network
└─ vSwitch2 → pNIC2 → vMotion Network
```

### Multiple vSwitches: Isolation
- Chaque vSwitch = separate logical switch
- Chaque vSwitch = requiert pNIC distinct
- **Pas communication directe** entre vSwitches (isolation réseau)

### Distributed Virtual Switch (DVS)
- **Agrège vSwitches** multiples serveurs = 1 distributed switch
- **Centralized management**: une policy pour cluster
- **Policy portability**: config migrate avec VM live migration
- **Benefits**: configuration consistency, policy mobility

---

## Container Networking: veth

### Virtual Ethernet Pairs (veth)
- Containers utilisent veth interfaces pour communication
- Docker bridge (docker0) agit comme L2 switch

```
Container1 [veth1] ←→ docker0 bridge ←→ [veth2] Container2
                           ↓
                      Physical NIC
```

---

## Network Functions Virtualization (NFV)

### Concept Principal
- **Décorréler** network functions (routes, firewall, LB) **du hardware dédié**
- **Exécuter comme logiciel** sur serveurs x86 commodity
- **ETSI Framework**: standard NFV architecture

### Before vs After NFV

```
BEFORE NFV:
┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌──────────┐
│ Cisco ASR   │   │ Cisco ASA   │   │ F5 LB       │   │ WAN Opt  │
│ $ 100K      │   │ $ 50K       │   │ $ 80K       │   │ $ 40K    │
└─────────────┘   └─────────────┘   └─────────────┘   └──────────┘
Total: ~$270,000 capital

AFTER NFV:
┌──────────────────────────────────────┐
│ x86 Server ($20K)                    │
│ ├─ CSR1000v Router VNF ($5K/yr)     │
│ ├─ ASAv Firewall VNF ($8K/yr)       │
│ ├─ VNF Load Balancer ($3K/yr)       │
│ └─ Hypervisor (KVM/vSphere)         │
└──────────────────────────────────────┘
Total: ~$50-75K + licensing
Saving: ~$200K capital + OpEx reduction
```

### NFV Advantages
- **CapEx réduit**: hardware commodity x86
- **OpEx optimisé**: puissance/refroidissement réduits
- **TTM (Time-to-Market)**: déploiement rapide
- **Elasticité**: scale up/down dynamiquement
- **Innovation**: testable, déploiement faible risque
- **Market Opening**: multiple vendors, pas lock-in

---

## NFV Infrastructure & Architecture

### NFVI (NFV Infrastructure)
- **Platform physique/logiciel** supportant déploiement VNF
- **Composants**:
  - Compute: serveurs x86
  - Storage: arrays
  - Network: fibre optique
  - Virtualization Layer: hypervisors (KVM/vSphere), OvS (Open vSwitch)

### VNF (Virtual Network Function)
- **Network function virtualisée**: router, firewall, LB, ADC, WAN optimization
- **Cisco VNFs**:
  - CSR 1000V: Cloud Services Router
  - ISRv: Integrated Services Router virtual
  - NGFWv: Next-Gen Firewall virtual
  - ASAv: Adaptive Security Appliance virtual

### VIM (Virtualized Infrastructure Manager)
- **Gère ressources NFVI**: compute, storage, network
- **Lifecycle management**: créer/modifier/terminer VMs
- **Service chaining**: assembler VNFs
- **Tools**: OpenStack, VMware vCloud, Kubernetes

### EM/EMS (Element Manager / Management System)
- **Gestion fonctionnelle VNF** (FCAPS):
  - **F**ault: détection défaillances
  - **C**onfiguration: paramètres VNF
  - **A**ccounting: utilisation ressources
  - **P**erformance: métriques vitales
  - **S**ecurity: sécurité VNF

---

## NFV Management & Orchestration (MANO)

### NFV Orchestrator
- **Créer/maintenir/arrêter services** multi-VNF end-to-end
- **Service Chaining**: connecter VNFs (ex: Router → Firewall → LB)

### VNF Manager
- **Lifecycle VNF**: startup/shutdown
- **Configuration management**
- **Performance monitoring**
- **Fault recovery & escalation**

### MANO (Combined)
```
┌─────────────────────────────────────┐
│ NFV MANO (Management & Orchestr.)   │
├────────────────┬──────────┬─────────┤
│ Orchestrator   │VNF Mgr   │ VIM     │
├────────────────┼──────────┼─────────┤
│ Services       │ Lifecycle│ Resources
│ end-to-end     │ FCAPS    │ Compute
│ Chaining       │ Config   │ Storage
│ Deployment     │ Monitoring Network
└────────────────┴──────────┴─────────┘
```

---

## Service Chaining Practical Example

### WAN Secure Branch Scenario
```
Branch Internet
      ↓
[CSR1000v Router VNF]       ← Routing (EIGRP/BGP)
      ↓
[ASAv Firewall VNF]         ← Security filtering
      ↓
[ISRv Router VNF]           ← Data center routing
      ↓
Data Center
```

**Benefits**:
- Unified security policy
- Single management console
- Flexible service insertion
- Easy policy changes

---

## OSS/BSS Systems

### OSS (Operations Support System)
Service providers/grandes entreprises:
- **Inventory Management**: suivi ressources
- **Service Provisioning**: allocation VNF automatique
- **Device Configuration**: paramètres appliances
- **Incident Resolution**: troubleshooting automation

### BSS (Business Support System)
- **Billing**: facturation client
- **CRM**: customer relationship
- **Order Management**: automatisation commandes

---

## Comparaison: Bare Metal vs VM vs Container

| Aspect | Bare Metal | VM | Container |
|--------|-----------|----|---------  |
| **Performance** | 100% | ~90% | ~95% |
| **Isolation** | N/A | Complète | Procédés |
| **Densité** | 1 app | 10-20 | 100+ |
| **Startup** | Boot | Minutes | Secondes |
| **Management** | Manuel | Infa-as-Code | Orchestration |

---

## Key Points Exam

✓ **Hypervisor Type 1**: bare metal (vSphere, Hyper-V, KVM, XenServer)  
✓ **Hypervisor Type 2**: hosted (Fusion, VirtualBox)  
✓ **VMs**: complet OS, live migration, HA  
✓ **Containers**: léger, OS partagé, secondes démarrage  
✓ **vSwitch**: L2 logiciel, intra-host/external access  
✓ **DVS**: centralized management cluster  
✓ **veth**: container networking interfaces  
✓ **NFV Concept**: décorréler NF du hardware  
✓ **NFVI**: compute/storage/network infrastructure  
✓ **VNF**: CSR/ASAv/NGFWv/ISRv virtualisés  
✓ **VIM**: resource manager, lifecycle, orchestration  
✓ **EM/EMS**: FCAPS management VNFs  
✓ **MANO**: Orchestrator + VNF Manager + VIM combinés  
✓ **Service Chaining**: multi-VNF end-to-end services  
✓ **ETH Framework**: standard NFV architecture
