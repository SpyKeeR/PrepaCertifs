---
title: "Module 27: Virtualization"
module: 27
type: notes
topics: [VM, Containers, Hypervisor, vSwitch, NFV, NFVI, VNF, MANO]
difficulty: advanced
updated: 2026-03-18
---

# Module 27: Virtualization

## Vue d'ensemble
Le module **Virtualization** (Module 27) couvre l'abstraction matérielle (VMs/Containers) et Network Functions Virtualization (NFV). Ce module est essentiel pour comprendre comment moderniser l'infrastructure réseau en remplaçant appliances dédiées par logiciels virtualisés exécutés sur serveurs x86.

---

## 1. Virtualisation Serveur: Concepts Fondamentaux

### 1.1 Problème & Solution

**Avant virtualisation**:
```
Serveur 1 [OS] [App] → 30% CPU utilisé
Serveur 2 [OS] [App] → 20% CPU utilisé
Serveur 3 [OS] [App] → 10% CPU utilisé
─────────────────────────────────────
Total: 60% CPU, 40% gaspillé
Budget: 3 serveurs physiques, 3 OS, 3 maintenances
```

**Après virtualisation**:
```
Serveur x86 Physique
├─── [Hypervisor]
│    ├─ VM1 [OS] [App]  → 30% CPU
│    ├─ VM2 [OS] [App]  → 20% CPU
│    └─ VM3 [OS] [App]  → 10% CPU
└─ Total: 60% CPU du serveur unique

Budget: 1 serveur = coût réduit (CapEx/OpEx)
Densité: 10-20 VMs/serveur selon taille
```

### 1.2 Types de Virtualisation

1. **Server Virtualization**: VMs exécutant OSs complets + applications
2. **Container Virtualization**: Applications légères + dépendances, OS partagé
3. **Network Functions Virtualization (NFV)**: Fonctions réseau (firewall, router) virtualisées

---

## 2. Virtual Machines (VMs)

### 2.1 Définition
**VM** = émulation logicielle complète d'un serveur physique (matériel + OS complet).

### 2.2 Composants VM

```
┌─────────────────────────────────┐
│       Virtual Machine           │
├─────────────────────────────────┤
│   [Guest OS] (Windows/Linux)    │
│   [Executables/Libraries]       │
│   [Applications]                │
│   [Dependencies]                │
│                                 │
│   ~ 5-15 GB disque              │
│   ~ 2-4 GB RAM                  │
│   ~ Minutes à démarrer          │
└─────────────────────────────────┘
        ↓
    [Hypervisor]
        ↓
    [Matériel physique]
```

### 2.3 Avantages VMs

1. **Live Migration**: déplacement VM entre serveurs sans downtime
   - Utile pour maintenance matériel
   - Aucune interruption service

2. **High Availability (HA)**: basculement automatique serveur défaillant
   - Cluster HA détecte panne
   - VM redémarrage serveur sain
   - RTO très court

3. **Consolidation**: réduction serveurs physiques

---

## 3. Hypervisors: Type 1 vs Type 2

### 3.1 Type 1 Hypervisor (Bare Metal)

**Exécuté directement sur matériel** (pas OS hôte requis):

```
┌─────────────────┐
│   Hypervisor    │ ← Installed on hardware directly
├─────────────────┤
│ [VM1] [VM2] ... │ ← VMs exécutent OS invité
├─────────────────┤
│  Physical CPU   │
└─────────────────┘
```

**Solutions Type 1 Cisco/Enterprise**:
- **VMware vSphere/ESXi**: leader marché, HA/vMotion advanced
- **Microsoft Hyper-V**: intégration Windows Server
- **Citrix XenServer**: alternativement
- **Red Hat KVM**: open-source, Linux-based

### 3.2 Type 2 Hypervisor (Hosted)

**Exécuté en tant qu'application** sur OS hôte:

```
┌──────────────────────┐
│   Host OS (Win/Mac)  │
├──────────────────────┤
│  [Hypervisor App]    │ ← VMware Fusion, VirtualBox
│  [VM1] [VM2] ...     │ ← VMs invités
├──────────────────────┤
│  Desktop Hardware    │
└──────────────────────┘
```

**Limites Type 2**:
- Performance réduite (passe par OS hôte)
- Destktop/laptop usage, pas production
- VMware Fusion = option Apple

---

## 4. Containers: Alternative Légère

### 4.1 Concept Containers

**Container** = environnement isolé pour application **sans OS complet**.

```
┌──────────────────────────────┐
│      Container Runtime       │
│      (Docker Engine)         │
├──────────────────────────────┤
│ ┌─────────┐ ┌─────────┐     │
│ │Container1│ │Container2│ ← App + dépendances seulement
│ │ [App]    │ │ [App]   │   
│ │ [Libs]   │ │ [Libs]  │
│ └─────────┘ └─────────┘
│                              │
│ [Shared Linux Kernel]        │ ← Utilise noyau hôte
├──────────────────────────────┤
│     Linux Host              │
│     [Physical Hardware]     │
└──────────────────────────────┘
```

### 4.2 VM vs Container: Comparaison

| Aspect | VM | Container |
|--------|----|---------  |
| **OS** | OS complet (Windows/Linux) | OS partagé kernel |
| **Taille image** | 5-15 GB | 100-500 MB |
| **Démarrage** | Minutes | Secondes |
| **Overhead** | Élevé (multiple OS) | Faible |
| **Abst. niveau** | Material emulation | Application emulation |
| **Isolat.** | Complète | Procédés isolés |
| **Outil Cisco** | VMware vSphere/KVM | Docker, Kubernetes |

### 4.3 Container Images

**Container Image** = fichier snapshot:
- Application code
- Runtime environment
- Dépendances/librairies
- Variables environnement

Stocked en registries (Docker Hub, Artifactory).

---

## 5. Virtual Networking: vSwitches

### 5.1 Concept vSwitch

**vSwitch** (Virtual Switch) = commutateur Layer 2 **logiciel** sur hypervisor.

```
┌─────────────────────────────────┐
│   Physical Server               │
│  ┌────────────────────────────┐ │
│  │  Hypervisor                │ │
│  │  ┌──────────────────────┐  │ │
│  │  │  vSwitch0            │  │ │
│  │  │  ┌─ VM1 eth0 ────┐   │  │ │
│  │  │  ├─ VM2 eth0 ────┤   │  │ │
│  │  │  └─ VM3 eth0 ────┤   │  │ │
│  │  │                  ↓   │  │ │
│  │  │           [pNIC eth0]│  │ │
│  │  └──────────────────────┘  │ │
│  └────────────────────────────┘ │
│         ↓                        │
│   [Réseau physique]              │
└─────────────────────────────────┘
```

**Fonctions vSwitch**:
- Forwarding L2 entre VMs
- Forward vers réseau physique via pNIC
- VLAN tagging (802.1Q)

### 5.2 Multiple vSwitches par Hypervisor

Chaque vSwitch indépendant requiert sa propre pNIC:

```
Hypervisor Physique
├─ vSwitch0 → pNIC0 → Réseau Production
├─ vSwitch1 → pNIC1 → Réseau Management
└─ vSwitch2 → pNIC2 → Réseau vMotion (live migration)
```

**Important**: Pas de communication directe entre vSwitches (isolation)

### 5.3 Distributed Virtual Switch (DVS)

**DVS** agrège vSwitches multiples serveurs en **switch distribué unique**:

```
┌──────────────────────────────────────────┐
│     Distributed Virtual Switch (DVS)     │
│                                          │
│  ┌────────────────┐   ┌────────────────┐│
│  │ Server1        │   │ Server2        ││
│  │  vSwitch0      │   │  vSwitch0      ││
│  │  [VM1][VM2]    │   │  [VM3][VM4]    ││
│  └────────────────┘   └────────────────┘│
│                                          │
│  [Centralized policy management]        │
│  [Live migration avec politique intact] │
└──────────────────────────────────────────┘
```

**DVS Avantages**:
- **Gestion centralisée**: une policy pour cluster
- **Policy Portabilité**: configuration migrate avec VM
- **Configuration Consistency**: tous serveurs identiques

---

## 6. Container Networking

### 6.1 veth (Virtual Ethernet Pairs)

Containers utilisent **veth interfaces** pour communication:

```
Container1        Container2
  │                 │
[veth1] ───────── [veth2] ← communication directe
  │                 │
  └──────────┬──────┘
             │
       [docker0 bridge] ← S'interconnecter
             │
       [Physical NIC]
```

**Docker bridge**: agit comme switch L2, routage entre containers

---

## 7. Network Functions Virtualization (NFV)

### 7.1 Concept NFV

**NFV** = décorréler **network functions** (routeurs, firewalls) du **dedicated hardware** → exécuter comme **software sur serveurs x86**.

```
Before NFV:
Router (Cisco ASR)  Firewall (ASA)  LB (F5)  WAN Opt
[Proprietary]       [Proprietary]   [Prop]   [Proprietary]
$ 100,000 each      $ 50,000        $ 80,000 $ 40,000

After NFV:
┌─────────────────────────────────────────┐
│   x86 Server                            │
│  ┌──────────────┐  ┌──────────────┐   │
│  │ CSR1000v     │  │ ASAv         │   │
│  │ (VNF Router) │  │ (VNF FW)     │   │
│  │ $5,000/yr    │  │ $8,000/yr    │   │
│  └──────────────┘  └──────────────┘   │
│                                        │
│  Hypervisor (vSphere/KVM)              │
└─────────────────────────────────────────┘
$ 20,000 initial + licensing logiciel
```

### 7.2 ETSI NFV Framework

**ETSI** (European Telecommunications Standards Institute) = standard NFV architecture.

### 7.3 Avantages NFV

| Avantage | Impact |
|----------|--------|
| **CapEx réduit** | Matériel commodity x86 |
| **OpEx optimisé** | Électricité/refroidissement réduits |
| **TTM (Time-to-Market)** | Déploiement rapidement |
| **Élasticité** | Scale up/down dynamiquement |
| **Innovation** | Testable, déploiement faible risque |
| **Marché ouvert** | Multiple vendors (pas lock-in) |

---

## 8. NFV Architecture: Composants

### 8.1 NFVI (NFV Infrastructure)

**NFVI** = platform physique/logiciel supportant déploiement VNF:

```
┌─────────────────────────────────────┐
│        NFV INFRASTRUCTURE            │
│  ┌──────────────────────────────┐   │
│  │ Compute/Storage/Network      │   │
│  │ [Serveurs x86 physiques]     │   │
│  │ [Fibre Optique réseau]       │   │
│  │ [Storage arrays]             │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ Virtualization Layer          │   │
│  │ [Hypervisors: KVM/vSphere]   │   │
│  │ [Virtual networking: OvS]    │   │
│  │ [Storage: QCOW2/Images]      │   │
│  └──────────────────────────────┘   │
└─────────────────────────────────────┘
```

### 8.2 VNF (Virtual Network Function)

**VNF** = application network function exécutée virtualizée.

**Types VNF**:

| Layer | Exemples VNF |
|-------|-------------|
| **L4-7** | Load Balancers, Application Delivery Controllers (ADC), Firewalls, IDS, WAN Optimization |
| **L2-3** | Routers, Switches |

**Cisco VNFs**:
- **CSR 1000V**: Cloud Services Router (routing)
- **ISRv**: Integrated Services Router virtualisé
- **NGFWv**: Next-Gen Firewall virtual
- **ASAv**: Adaptive Security Appliance virtual
- **CSP 2100**: Cloud Services Platform (aggregation de VNFs)

### 8.3 VIM (Virtualized Infrastructure Manager)

**VIM** = gestionnaire ressources NFVI:

Fonctions:
- **Resource Management**: compute, storage, network
- **Lifecycle Management**: créer/modifier/terminer VMs
- **Service Chaining**: assembler VNFs (ex: FW → LB → Router)
- **Monitoring**: santé infrastructure

Tools: OpenStack, VMware vCloud, Kubernetes

### 8.4 EM/EMS (Element Manager / Management System)

**EM/EMS** = gestion fonctionnelle VNF (FCAPS):

```
F - Fault:         Détection défaillances
C - Configuration: Paramètres VNF
A - Accounting:    Utilisation ressources
P - Performance:   Métriques vitales
S - Security:      Sécurité VNF
```

---

## 9. NFV Management & Orchestration (MANO)

### 9.1 NFV Orchestrator

**Orchestrator** = créer/maintenir/arrêter services multi-VNF:

```
Demande: "Créer service WAN secure"
                ↓
[NFV Orchestrator]
      ↓
1. Allouer ressources compute/storage
2. Instantier CSR1000v (router VNF)
3. Instantier ASAv (firewall VNF)
4. Service Chaining: Router → Firewall → WAN
5. Config paramètres
6. Health monitoring
```

### 9.2 VNF Manager

**VNF Manager** = gestion lifecycle + FCAPS pour **chaque VNF**:

- Startup/shutdown VNF
- Configuration management
- Performance monitoring
- Fault recovery

### 9.3 MANO (Management & Orchestration)

**MANO** = **Orchestrator + VNF Manager + VIM** combinés.

```
┌─────────────────────────────────────┐
│      NFV MANO                       │
├──────────────┬──────────┬───────────┤
│ Orchestrator │ VNF Mgr  │ VIM       │
├──────────────┼──────────┼───────────┤
│Create/modify │ Lifecycle│ Resource  │
│services      │ Mgmt     │ Mgmt      │
│Service Chain │FCAPS     │ Compute   │
│end-to-end    │          │ Storage   │
│              │          │ Network   │
└──────────────┴──────────┴───────────┘
```

---

## 10. Service Chaining

### 10.1 Concept
**Service Chaining** = connecter multiples VNFs pour création services end-to-end.

### 10.2 Exemple Practical: WAN Secure

```
Branch Internet ──┐
                  │
             [CSR1000v Router VNF]
                  ↓
             [ASAv Firewall VNF]
                  ↓
             [ISRv Router VNF]
                  ↓
             Data Center
```

Services enchaînés:
1. **CSR = routing WAN** (EIGRP/BGP)
2. **ASAv = filtrage sécurité** (connexions drop)
3. **ISRv = routage côté data center**

---

## 11. OSS/BSS Systems

### 11.1 Définition
- **OSS** (Operations Support System)
- **BSS** (Business Support System)

### 11.2 Fonctions OSS

Services providers/grandes entreprises:
- **Inventory Management**: suivi ressources
- **Service Provisioning**: allocation VNF
- **Device Configuration**: paramètres appliances
- **Incident Resolution**: troubleshooting

---

## 12. Résumé Comparatif: VM vs Container vs Bare Metal

| Aspect | Bare Metal | VM | Container |
|--------|-----------|----|---------  |
| **Performance** | Maximale | ~90% | ~95% |
| **Isolation** | N/A | Complète | Procédés |
| **Démarrage** | Minutes | Minutes | Secondes |
| **Densité** | 1 OS/serveur | 10-20 VMs | 100+ containers |
| **Gestion** | Manuelle | Infa-as-Code | Orchestration |
| **Fondateur** | Physical machines | VMware (1999) | Docker (2013) |

---

## 13. Points d'Examen Clés

✓ **Hypervisor Type 1**: bare metal (vSphere, Hyper-V, XenServer, KVM)  
✓ **Hypervisor Type 2**: hôte OS requis (VMware Fusion)  
✓ **VMs**: OS complet, minutes démarrage, live migration, HA  
✓ **Containers**: OS partagé, secondes démarrage, légèr  
✓ **vSwitch**: L2 software switch, multiple pNICs  
✓ **DVS**: centralized management, policy portability  
✓ **veth**: container networking interfaces  
✓ **NFV**: découple NF du hardware, ETSI framework  
✓ **NFVI**: compute/storage/network infrastructure  
✓ **VNF**: router/firewall/LB virtualisé (CSR/ASAv/NGFWv)  
✓ **VIM**: resource manager, lifecycle, service chaining  
✓ **EM/EMS**: FCAPS management  
✓ **MANO**: Orchestrator + VNF Manager + VIM  
✓ **Service Chaining**: multi-VNF end-to-end services
