---
title: "Fiche Modules 28-29: Programmability & Automation"
type: fiche
modules: [28, 29]
topics: [API, REST, DNA Center, Postman, EEM, Puppet, Ansible, Automation]
difficulty: advanced
updated: 2026-03-18
---

# Fiche Synthèse: Modules 28-29 - Programmability & Automation

## MODULE 28: Foundational Network Programmability Concepts

### CLI vs Programmabilité: Problématique

**CLI Avantages**:
- Interaction immédiate
- Feedback instant
- Pas programmation requise

**CLI Inconvénients** (Critical):
- **Misconfiguration risque élevé**: humain tape commandes
- **Erreurs humaines**: scaling impossible (complexité coûts outages)
- **Pas automatisation**: répétition manuelle multiples devices

### Automatisation CLI Tools
- **Expect scripts**: interprétation texte
- **Ansible**: push config SSH
- **Puppet/Chef**: agent-based management
- **EEM**: Embedded Event Manager local

---

## APIs (Application Programming Interfaces)

### Concept Fondamental
- **API** = interface logicielle communication/manipulation données
- **Network Context**: communication contrôleur ↔ devices

### API Directions

#### Northbound API
```
Management Apps (GUI, scripts) 
           ↓ HTTPS/TLS
    Network Controller (DNA Center)
```
- **Function**: Management software → Controller
- **Security**: TLS encryption, token authentication

#### Southbound API
```
    Network Controller (DNA Center)
           ↓ HTTPS/TLS, NETCONF, YANG
         Devices (Router, Switch, WAP)
```
- **Function**: Controller → Devices (config pushdown)
- **Security**: TLS, device credentials

---

## REST APIs (RESTful Services)

### Concept REST
- **Style architecture** HTTP pour manipulation ressources
- **CRUD operations** (Create-Read-Update-Delete)
- **Vendor consistent**: HTTP standard interface

### HTTP Methods: CRUD

| Verb | Operation | Use Case |
|------|-----------|----------|
| **POST** | CREATE | device creation |
| **GET** | READ | device query/list |
| **PUT** | UPDATE | complete resource replacement |
| **PATCH** | PARTIAL UPDATE | attribute modification |
| **DELETE** | DELETE | resource removal |

### Avantages REST
- ✓ HTTP standard universel
- ✓ Vendor consistency
- ✓ Scalable (stateless, load-balanceable)
- ✓ Integration facile (JSON/XML)

---

## Data Formats: JSON vs XML

### JSON (JavaScript Object Notation)
```json
{
  "devices": [
    {
      "id": "device1",
      "hostname": "router1",
      "ipAddress": "192.168.1.1",
      "interfaces": [
        {"name": "GigabitEthernet0/0", "status": "up"},
        {"name": "GigabitEthernet0/1", "status": "down"}
      ]
    }
  ]
}
```

**Avantages JSON**:
- Simpler que XML
- Directement JavaScript-compatible
- Moins verbeux
- Parsing rapide

### XML (Extensible Markup Language)
```xml
<devices>
  <device>
    <id>device1</id>
    <hostname>router1</hostname>
    <interfaces>
      <interface>
        <name>GigabitEthernet0/0</name>
        <status>up</status>
      </interface>
    </interfaces>
  </device>
</devices>
```

**Inconvénients XML**:
- Verbeux (tags répétés)
- Parsing complexe
- Taille fichier augmentée

**Conclusion**: JSON > XML pour APIs modernes

---

## HTTP Status Codes

### Catégories
| Range | Category | Meaning |
|-------|----------|---------|
| **1xx** | Informational | Request received, processing continues |
| **2xx** | Success | Operation completed successfully |
| **3xx** | Redirection | Additional action required |
| **4xx** | Client Error | Invalid/unauthorized request |
| **5xx** | Server Error | Server failed to complete |

### Codes Courants
- **200 OK**: GET/PUT success
- **201 Created**: POST success (ressource créée)
- **204 No Content**: DELETE success
- **400 Bad Request**: client parameters invalides
- **401 Unauthorized**: credentials manquants
- **403 Forbidden**: insufficient permissions
- **404 Not Found**: ressource inexistante
- **500 Server Error**: backend bug
- **503 Unavailable**: service down

---

## Cisco DNA Center APIs

### DNA Center Architecture
```
[DNA Center Controller]
├─ REST API Northbound (/api/system/v1/, /api/v1/)
├─ NETCONF/YANG Southbound (vers devices)
└─ Devices (Router, Switch, WAP)
```

### Token Authentication: First Step
```
POST https://sandboxdnac.cisco.com/api/system/v1/auth/token

Auth: Basic Auth (username + password)
Headers: Content-Type: application/json
Body: {} (empty)

Response:
{
  "Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### Token Usage: Subsequent Calls
```
Headers:
  Content-Type: application/json
  X-Auth-Token: <token_from_auth>
```

### Network Device Inventory API
```
GET https://sandboxdnac.cisco.com/api/v1/network-device

Headers:
  Content-Type: application/json
  X-Auth-Token: [token]

Response:
{
  "response": [
    {
      "id": "device-uuid",
      "hostname": "router1",
      "managementIpAddress": "192.168.1.1",
      "platformId": "Cisco ASR1000",
      "softwareVersion": "16.12.03",
      "serialNumber": "ABC123"
    }
  ],
  "count": 1
}
```

---

## Postman: API Testing Tool

### Sections Postman Interface
- **History**: recent API calls
- **Collections**: grouped requests (workspace organization)
- **New Tab**: individual API testing
- **URL Bar**: specific API endpoint
- **Send Button**: execute request
- **Auth**: authentication configuration
- **Headers**: HTTP headers
- **Body**: request payload (JSON/XML)
- **Response**: server response output

### Workflow Postman
1. Create request (URL, method, auth)
2. Add authentication (Basic Auth, Bearer Token)
3. Set headers (Content-Type, X-Auth-Token)
4. Click Send
5. Observe response (status code, JSON body)

---

## GitHub: Version Control & Collaboration

### Roles GitHub
- **Version Control**: tracking code changes (git)
- **Collaboration**: multiple developers same project
- **Backup**: code stocké cloud
- **Community**: code sharing public

### Workflow GitHub
```
Local editing → git add → staging
              → git commit → local history
              → git push → remote master
              → pull request → code review
              → merge → production
```

---

## Python: Automation Language

### Rôle Python
- **Langage populaire** automatisation réseau
- **Libraries**: requests (HTTP), paramiko (SSH), netmiko (Cisco CLI)
- **Cross-platform**: Windows/Linux/macOS

### Exemple Python: DNA Center API Call
```python
import requests
from requests.auth import HTTPBasicAuth

# Step 1: Obtain Token
token_url = "https://sandboxdnac.cisco.com/api/system/v1/auth/token"
response = requests.post(
    token_url,
    auth=HTTPBasicAuth('admin', 'Cisco123'),
    headers={'Content-Type': 'application/json'},
    verify=False
)
token = response.json()['Token']

# Step 2: Get Devices
device_url = "https://sandboxdnac.cisco.com/api/v1/network-device"
headers = {
    'Content-Type': 'application/json',
    'X-Auth-Token': token
}
response = requests.get(device_url, headers=headers, verify=False)
devices = response.json()['response']

# Step 3: Process Results
for device in devices:
    print(f"{device['hostname']} ({device['managementIpAddress']})")
```

---

## Cisco DevNet & Sandboxes

### DevNet Resources
- **Sandboxes**: environments lab gratuits
  - DNA Center Sandbox
  - NETCONF/YANG Sandbox
  - ISE Sandbox
- **Certifications**: DevNet Associate, Professional
- **Documentation**: APIs, SDKs

---

## MODULE 29: Introduction to Automation Tools

## EEM (Embedded Event Manager): On-Device Automation

### Concept EEM
- **Plateforme automation intégrée** Cisco devices (routeurs/switches)
- **Event-driven**: automatiquement exécute tâches déclenché par événements
- **On-box**: logique locale device, pas dépendance externe

### Architecture EEM

```
EVENT (Trigger)           ACTION (Response)
├─ Syslog pattern    -->  ├─ enable/configure
├─ CLI command       -->  ├─ send email
├─ Interface status  -->  ├─ log message
├─ Timer             -->  ├─ run Tcl script
└─ SNMP trap         -->  └─ reload device
```

### Event Detectors
- **Syslog**: pattern matching (ex: "Loopback0 down")
- **CLI**: command execution (ex: "write memory")
- **Interface**: status changes (up→down)
- **Timer**: time interval (ex: every 5 seconds)
- **SNMP**: trap threshold (ex: uptime > 3600s)

### EEM Actions
- **Require "enable"** + **"configure terminal"** commands
- Email notifications (notification_email, email_server, email_cc)
- Syslog messages (logging)
- CLI configuration (shutdown/no shutdown interfaces)

### Tcl Scripts
- **Scripting engine** pour logique complexe applets
- **Trigger**: `event manager run applet-name`
- **List scripts**: `more flash:filename`

### Avantages EEM
- ✓ **Rapid response**: immediate event reaction
- ✓ **Autonomous**: local logic device
- ✓ **Error reduction**: automation eliminates human errors
- ✓ **Cost effective**: embedded all Cisco routers

---

## Puppet: Enterprise Configuration Management

### Concept Puppet
- **Configuration management platform** device lifecycle (deploy → configure → maintain)
- **Master-agent architecture**: Puppet master ↔ agents on devices
- **SSL certificate-based** authentication

### Puppet Master-Agent
```
[Puppet Master (Server)]
        ↕ HTTPS/SSL
├─ Device1 Agent
├─ Device2 Agent
└─ Device3 Agent (up to 4000 agents monolithic)
```

### Puppet Deployment Models

#### Monolithic
- Single master → max 4000 agents

#### Large-Scale (Recommended)
```
[Master of Masters (MoM)]
        ↓
[Compile Master 1]  [Compile Master 2] (load-balanced)
        ↓                     ↓
   [Agents]              [Agents]
```

### Puppet Modules: Structure
```
my_module/
├── manifests/        (policy)
│   ├── init.pp       (main class)
│   ├── ntp_server.pp
│   └── motd.pp
├── templates/        (template variables)
│   └── ntp.conf.erb
└── files/            (static files)
    └── access_list.acl
```

### Puppet Manifests: Ruby DSL
- **Domain-specific language** (Ruby-based)
- **Declarative**: describe desired state
- **Example**:
  ```ruby
  class { 'ntp_server':
    ensure  => 'present',
    ntp_servers => ['8.8.8.8', '1.1.1.1'],
  }
  ```

### Puppet PuppetDB
- Central repository storage:
  - Node facts
  - Resource catalogs
  - Event reports

---

## Chef: Alternative Configuration Management

### Concept Chef
- **Configuration management alternative** Puppet
- **Ruby + Erlang** based
- **Imperative** approach (vs Puppet declarative)

### Chef vs Puppet

| Aspect | Chef | Puppet |
|--------|------|--------|
| **Language** | Ruby native | Puppet DSL (Ruby) |
| **Approach** | More flexible | More rigid |
| **Learning** | Steeper | Gentler |

---

## Agentless Tools: Ansible & SaltStack

### Ansible: SSH-Based Automation
- **Agentless**: no agent installation (SSH exists)
- **Push-based**: control machine → devices
- **Playbooks**: YAML configuration files

**Advantage**:
- ✓ No agent overhead
- ✓ Zero device prerequis
- ✓ Rapid scaling

### SaltStack: Hybrid Approach
- **Agent-based** (Salt Minion) OR **Agentless** (Salt SSH)
- **Remote execution** framework

---

## Agent-Based vs Agentless: Comparison

| Aspect | Agent-Based | Agentless |
|--------|------------|-----------|
| **Installation** | Agent binary required | SSH only |
| **Performance** | Superior | Acceptable |
| **Scalability** | ~1000 agents/master | ~100 per run |
| **Examples** | Puppet, Chef | Ansible, Terraform |
| **Overhead** | Background process | Zero |
| **Setup time** | Longer | Immediate |

---

## Automation Benefits

### Speed (Vitesse)
```
Manual: 100 routers × 10 commands × 1 min = 1000 min (16+ hrs)
Auto:   100 routers parallel × 10 commands = 5 min
Gain:   95% time reduction!
```

### Consistency (Cohérence)
- All devices configured identically
- No variation human errors
- Predictable behavior
- Simplified troubleshooting

### Risk Reduction
```
Manual: Typo command → interface shutdown → 30 min outage
Auto:   Syntax verified before deployment → zero typo risk
```

### Compliance & Audit
- Who changed what (audit trail)
- When changes applied
- Approvals documentation
- Reusable templates

---

## Common Automation Use Cases

- **VLAN Provisioning**: 5 min vs 30 min manual
- **Config Backup**: automatic daily
- **ACL Management**: template-driven
- **QoS Policy**: consistent enforcement
- **Usernames/Passwords**: centralized rotation
- **SNMP Credentials**: compliance
- **Firmware Upgrade**: parallel, no downtime

---

## Tool Selection Decision Tree

```
Need Automation?
    │
    ├─ On-Device? ──→ EEM (Cisco only)
    │
    └─ Centralized?
       │
       ├─ Agentless? ──→ Ansible (SSH easy)
       │
       └─ Agent-Based?
          │
          ├─ Flexibility ──→ Chef (Ruby)
          │
          └─ Simplicity ──→ Puppet (DSL)
```

---

## Automation Generation Evolution

```
Gen 1 (2000s):  Manual CLI → Expect scripts → Syslog parsing
Gen 2 (2010s):  EEM → Puppet/Chef → Configuration templates
Gen 3 (2020s):  Ansible → Terraform → Infrastructure as Code
                Kubernetes → Container orchestration
                GitOps → Version-controlled automation
```

---

## Key Points Exam

✓ **CLI issue**: misconfiguration risque élevé, erreurs humaines  
✓ **Northbound API**: Management → Controller  
✓ **Southbound API**: Controller → Devices  
✓ **REST**: HTTP CRUD (POST/GET/PUT/PATCH/DELETE)  
✓ **JSON**: objects, arrays, simpler XML  
✓ **HTTP Status**: 1xx (info), 2xx (success), 3xx (redirect), 4xx (client), 5xx (server)  
✓ **DNA Center Token API**: POST /auth/token, Basic Auth  
✓ **DNA Center Device API**: GET /network-device, X-Auth-Token header  
✓ **Postman**: REST API testing GUI  
✓ **GitHub**: version control, collaboration  
✓ **Python**: automation language, requests library  
✓ **EEM**: event-triggered automation, Tcl scripting  
✓ **Puppet**: master-agent, manifests, certificate-based  
✓ **Chef**: Ruby-based, flexible  
✓ **Ansible**: agentless SSH, playbooks  
✓ **Agent-Based vs Agentless**: agent overhead vs zero footprint  
✓ **Automation Benefits**: speed, consistency, risk reduction, compliance
