---
title: "Module 29: Introduction to Automation Tools"
module: 29
type: notes
topics: [EEM, Tcl, Puppet, Chef, Ansible, SaltStack, Automation Benefits]
difficulty: advanced
updated: 2026-03-18
---

# Module 29: Introduction to Automation Tools

## Vue d'ensemble
Le module **Introduction to Automation Tools** (Module 29) couvre outils d'automatisation configuration réseau. Ce module présente approches on-device (EEM) vs centralisées (Puppet, Chef, Ansible) pour réduire erreurs et accélérer déploiements.

---

## 1. Embedded Event Manager (EEM): Automatisation On-Device

### 1.1 Concept EEM

**EEM** (Embedded Event Manager) = plateforme automation **intégrée routeurs/switches Cisco**, exécutant **automatiquement tâches** déclenché par **événements**.

Avantage: **Pas dépendance externes**, logique locale routeur.

### 1.2 Architecture EEM: Event-Action

```
┌──────────────────────────┐
│   EEM Applet             │
├──────────────────────────┤
│                          │
│  EVENT (Déclencheur)     │
│  ├─ Syslog pattern       │
│  ├─ CLI command          │
│  ├─ Interface status     │
│  ├─ Timer                │
│  └─ SNMP trap            │
│         ↓                │
│  ACTION (Réponse)        │
│  ├─ Enable/configure     │
│  ├─ Send email           │
│  ├─ Log message          │
│  └─ Run Tcl script       │
│                          │
└──────────────────────────┘
```

### 1.3 EEM Event Detectors (Déclencheurs)

| Detector | Déclenchement | Exemple |
|----------|--------------|---------|
| **Syslog** | Pattern syslog match | "Interface Loopback0 down" |
| **CLI** | Commande exécutée | "write memory", "reload" |
| **Interface** | Status interface change | Ethernet0/0 up→down |
| **Timer** | Temps écoulé | Toutes les 5 secondes |
| **SNMP** | SNMP trap reçue | sysUpTimeInstance > 3600 |
| **Application** | Autre applet achevée | Applet X completed |

### 1.4 Cas d'usage EEM Pratique

**Scénario**: Interface Loopback0 tombe, automatiquement réinitialiser.

**Applet EEM**:
```
event manager applet LOOPBACK_MONITOR
 event syslog pattern "Loopback0 down"
 action 0 syslog msg "ERROR: Loopback0 interface down!"
 action 1 enable
 action 2 configure terminal
 action 3 interface Loopback0
 action 4 shutdown
 action 5 no shutdown
 action 6 exit
 action 7 end
 action 8 syslog msg "INFO: Loopback0 reset completed"
 action 9 event manager run SEND_EMAIL
```

### 1.5 EEM Email Actions

Notifier administrateurs via email:

```
event manager applet SEND_EMAIL
 action 0 cli command "show interfaces Loopback0"
 action 1 mail server 10.0.0.1
 action 2 mail from router@company.com
 action 3 mail to admin@company.com
 action 4 mail cc backup-admin@company.com
 action 5 mail subject "Alert: Loopback0 Interface Issue"
 action 6 mail body "Loopback0 automatically reset at $sysUpTime seconds"
```

### 1.6 EEM CLI Pattern: Sauvegarde Automatique Config

**Scénario**: Utilisateur tape "write memory" → backup config TFTP automatiquement.

```
event manager applet CONFIG_BACKUP
 event cli pattern "write memory" sync yes occur 1
 action 0 syslog msg "Backing up config to TFTP server..."
 action 1 enable
 action 2 configure terminal
 action 3 event manager run TFTP_BACKUP
 
event manager applet TFTP_BACKUP
 action 0 cli command "copy running-config tftp://10.0.0.1/backup.cfg"
 action 1 syslog msg "Config backup completed"
```

### 1.7 Tcl Scripts: EEM Extension

**Tcl** (Tool Command Language) = langage scripting intégré EEM.

**Utilisation Tcl**: logique complexe au-delà applets simples.

```
event manager applet ADVANCED_TASK
 action 0 puts "Starting Tcl script..."
 action 1 foreach i {1 2 3 4 5} {
           puts "Processing VLAN $i"
           cli_open
           cli_cmd "vlan $i"
           cli_cmd "name VLAN_$i"
          }
 action 2 puts "Tcl script completed"
```

### 1.8 Lancer Scripts Tcl Manuellement

Via CLI:
```
router# event manager run MY_APPLET
```

Voir contenu script:
```
router# more flash:my_script.tcl
```

### 1.9 Avantages EEM

- ✓ **Rapidité**: réaction immédiate événements
- ✓ **Autonome**: pas dépendance contrôleur externe
- ✓ **Réduction erreurs**: automatisation élimina humain
- ✓ **Coût réduit**: intégré tous routeurs Cisco

---

## 2. Puppet: Configuration Management Centralisée

### 2.1 Concept Puppet

**Puppet** = plateforme **configuration management** entreprise, gère **lifecycle devices**:
1. Deployment
2. Configuration
3. Compliance
4. Repurposing

### 2.2 Architecture Puppet: Master-Agent

```
┌─────────────────────┐
│  Puppet Master      │
│  (Server)           │
├─────────────────────┤
│ • Policy compilation│
│ • Cert management   │
│ • Reporting         │
└────────┬────────────┘
         │ HTTPS (SSL cert-based)
    ┌────┴────┬────────┬────────┐
    │          │        │        │
 ┌──▼──┐    ┌──▼──┐ ┌──▼──┐ ┌──▼──┐
 │Agent│    │Agent│ │Agent│ │Agent│
 │Dev1 │    │Dev2 │ │Dev3 │ │Dev4 │
 └─────┘    └─────┘ └─────┘ └─────┘
 (Routeurs/Switches/Firewalls)
```

### 2.3 Puppet Deployment Models

#### Model 1: Monolithic
```
Single Master ←→ up to 4000 Agents
(Limitation: Un serveur gérant milliers devices)
```

#### Model 2: Large-Scale (Recommended)
```
┌─────────────────────────┐
│ Master of Masters (MoM) │
└────────┬────────────────┘
         │
    ┌────┴────────────┐
    ↓                 ↓
┌──────────┐    ┌──────────┐
│ Compile  │    │ Compile  │
│ Master 1 │    │ Master 2 │
│(Load     │    │(Load     │
│ balanced)│    │ balanced)│
└────┬─────┘    └────┬─────┘
     │               │
  [Agents]        [Agents]
```

### 2.4 Puppet Modules: Structure

Chaque module Puppet contient:
```
my_module/
├── manifests/
│   ├── init.pp             (classe principale)
│   ├── ntp_server.pp       (ressource NTP)
│   └── motd.pp             (Message of Day)
├── templates/
│   └── ntp.conf.erb        (fichier template)
└── files/
    └── access_list.acl     (fichiers statiques)
```

### 2.5 Puppet Manifests: Ruby DSL

**Manifest** = fichier `.pp` définissant configuration devices.

Syntaxe:
```ruby
class { 'ntp_server':
  ensure  => 'present',
  service => 'ntp',
}
```

Exemple NTP Configuration Manifest:
```puppet
# modules/ntp/manifests/ntp_server.pp

class ntp_server (
  $ensure = 'present',
  $ntp_servers = ['8.8.8.8', '1.1.1.1'],
) {
  
  package { 'ntp':
    ensure => $ensure,
  }

  file { '/etc/ntp.conf':
    content => template('ntp/ntp.conf.erb'),
    require => Package['ntp'],
  }

  service { 'ntp':
    ensure  => running,
    enable  => true,
    require => File['/etc/ntp.conf'],
  }
}
```

Exemple MOTD (Message of Day) Manifest:
```puppet
# modules/motd/manifests/motd.pp

class motd (
  $message = "Welcome to Cisco Network!",
) {
  
  file { '/etc/motd':
    ensure  => present,
    content => $message,
    mode    => '0644',
  }
}
```

### 2.6 Puppet Cisco iOS Module

**cisco_ios** module autoriser configuration Cisco devices via SSH:

```puppet
class { 'cisco_ios_tests':
  device => 'device1',
}

# Configure VLAN
cisco_vlan { '100':
  ensure => 'present',
  name   => 'DATA_VLAN',
}

# Configure Interface
cisco_interface { 'Ethernet0/0':
  description  => 'Uplink to Core',
  mtu          => 1500,
  shutdown     => 'false',
}
```

### 2.7 Puppet Console

**Puppet Console** = interface web gestion:
- Deploy changes to nodes
- View node reports
- Manage credentials
- Schedule deployments

### 2.8 PuppetDB

**PuppetDB** = centrale data repository stockant:
- Node facts
- Resource catalogs
- Event reports
- Metric data
- Query interface

---

## 3. Chef: Alternative Configuration Management

### 3.1 Concept Chef

**Chef** = plateforme configuration management **alternative Puppet**, utilisant **Ruby + Erlang**.

### 3.2 Chef vs Puppet

| Aspect | Chef | Puppet |
|--------|------|--------|
| **Langage** | Ruby native | Puppet DSL (Ruby-based) |
| **Architecture** | Master-Agent ou Agentless | Master-Agent |
| **Flexibility** | Plus permissif | Plus rigid |
| **Learning Curve** | Plus steep | Plus shallow |

### 3.3 Chef Components

```
┌───────────────────┐
│ Chef Server       │
│ (Policy storage)  │
└────────┬──────────┘
         │ HTTPS
    ┌────┴────────────┐
    │                 │
 ┌──▼──┐          ┌──▼──┐
 │Chef  │          │Chef  │
 │Client│          │Client│
 │Node1 │          │Node2 │
 └─────┘          └─────┘
```

---

## 4. Agentless Tools: Ansible & SaltStack

### 4.1 Ansible: SSH-Based Automation

**Ansible** = plateforme automation **agentless** utilisant **SSH existant**.

Avantages Agentless:
- ✓ **Pas d'agent installé**: SSH déjà présent
- ✓ **Facile déploier**: zéro machine prerequis
- ✓ **Scalabilité rapide**: prêt immédiatement

Architecture:
```
┌──────────────────┐
│ Ansible Control  │
│ Machine (CLI)    │
└────────┬─────────┘
         │ SSH (Agentless)
    ┌────┴────────────┐
    │                 │
 ┌──▼────┐         ┌──▼────┐
 │Device1 │         │Device2 │
 │(Router)│         │(Switch)│
 └────────┘         └────────┘
```

Playbook example:
```yaml
---
- hosts: network_devices
  gather_facts: no
  tasks:
    - name: Configure NTP
      cisco.ios.ios_config:
        lines:
          - ntp server 8.8.8.8
          - ntp server 1.1.1.1
        
    - name: Configure ACL
      cisco.ios.ios_config:
        lines:
          - access-list 10 permit 192.168.1.0 0.0.0.255
```

### 4.2 SaltStack: Remote Execution

**SaltStack** = automation framework **remote execution + configuration management**.

Hybrid approach:
- Agent-based option (Salt Minion)
- Agentless option (Salt SSH)

---

## 5. Agent-Based vs Agentless Comparison

| Aspect | Agent-Based | Agentless |
|--------|------------|-----------|
| **Installation** | Agent binary installé | SSH seulement |
| **Performance** | Supérieur (agent local) | Acceptable |
| **Scalabilité** | ∼ 1000 agents/master | ∼ 100 par run (limité SSH) |
| **Exemples** | Puppet, Chef, SaltStack minion | Ansible, SaltStack SSH |
| **Overhead** | Processus background agent | Zéro footprint |
| **Temps Setup** | Plus long | Immédiat |

---

## 6. Automation Benefits: Impacs Tangibles

### 6.1 Speed (Vitesse)

```
Manual Configuration:
  1 router × 10 commands × 1 min = 10 minutes
  100 routers = 1000 minutes = 16+ heures

Automation:
  100 routers × 10 commands = parallel run
  Temps total: 5 minutes
  
Gain: 95% réduction temps!
```

### 6.2 Consistency (Cohérence)

```
Manual Config:
  Admin1 configures R1 légèrement différent
  Admin2 configures R2 autre style
  → Configurations inconsistentes
  → Harder troubleshot
  → Policy enforcement problème

Automation:
  Tous devices config IDENTIQUE
  → Behavior prévisible
  → Troubleshooting simple
```

### 6.3 Risk Reduction (Réduction Risques)

```
Manual:
  Typo commande → interface shutdown
  → Outage 30 minutes
  Cost: $50,000 (revenue loss)

Automation:
  Approuvé syntax vérifié avant déploiement
  → Zéro risque typo
  → Rollback simple si besoin
```

### 6.4 Compliance & Audit

```
Automation logs:
  - Qui a changé quoi
  - Quand change appliquée
  - Template utilisé
  - Approvals audit trail
  
→ Compliance audit facile
→ Security posture démontrée
```

---

## 7. Common Automation Use Cases

| Use Case | Benefit |
|----------|---------|
| **VLAN Provisioning** | 5 min vs 30 min manual |
| **Device Config Backup** | Automatique chaque jour |
| **ACL Management** | Template-driven, versionned |
| **QoS Configuration** | Consistent policy enforcement |
| **Usernames/Passwords** | Centralized, rotated regularly |
| **SNMP Community Strings** | Compliance avec policy |
| **Firmware Upgrade** | Parallel devices, no downtime |

---

## 8. Tool Selection Decision Tree

```
                    Need to Automate?
                           │
              ┌────────────┴────────────┐
              │                         │
    On-Device Automation        Centralized Management
    (Local device)              (Multiple devices)
           │                           │
         EEM                    ┌──────┴──────┐
           │                    │             │
    (If Cisco only)    Agentless?      Agent-Based?
                            │                 │
                        Ansible             Puppet
                      (SSH easy)         (Master-Agent)
                                              │
                                            Chef
                                       (Ruby flexible)
```

---

## 9. EEM vs Puppet vs Ansible: Quick Comparison

| Tool | Scope | Complexity | Dependency | Best For |
|------|-------|-----------|-----------|---------|
| **EEM** | Single device | Low | None (on-device) | Simple event-driven |
| **Puppet** | Enterprise | High | Master/Cert | Large networks |
| **Ansible** | Multi-vendor | Medium | SSH | Quick deployment |

---

## 10. Résumé Automation Evolution

```yaml
Generation 1 (2000s):
  Manual CLI → Expect scripts → Syslog parsing
  
Generation 2 (2010s):
  EEM → Puppet/Chef → Configuration templates
  
Generation 3 (2020s):
  Ansible → Terraform → Infrastructure as Code
  Kubernetes → Container orchestration
  GitOps → Version-controlled automation
```

---

## 11. Points d'Examen Clés

✓ **EEM**: embedded device automation, Tcl scripting  
✓ **EEM Event Detectors**: syslog, CLI, interface, timer, SNMP  
✓ **EEM Actions**: enable/configure/syslog/email  
✓ **EEM Email Variables**: notification_email, email_server, email_cc, email_subject  
✓ **Puppet**: master-agent, manifests, monolithic/large-scale  
✓ **Puppet Modules**: Manifests + Templates + Files  
✓ **Puppet Manifests**: Ruby DSL, ensure => 'present', SSL certs  
✓ **Puppet cisco_ios**: SSH-based Cisco device management  
✓ **Chef**: Ruby + Erlang, alternative Puppet  
✓ **Ansible**: agentless SSH-based automation  
✓ **SaltStack**: remote execution, hybrid agent/agentless  
✓ **Agent-Based**: Puppet/Chef/SaltStack Minion  
✓ **Agentless**: Ansible/SaltStack SSH  
✓ **Automation Benefits**: speed, consistency, risk reduction, compliance
