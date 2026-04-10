---
title: "Module 28: Foundational Network Programmability Concepts"
module: 28
type: notes
topics: [API, REST, HTTP, JSON, XML, DNA Center, Postman, GitHub, Python]
difficulty: advanced
updated: 2026-03-18
---

# Module 28: Foundational Network Programmability Concepts

## Vue d'ensemble
Le module **Foundational Network Programmability Concepts** (Module 28) introduit programmabilité réseau, APIs, et automatisation. Ce module transition de CLI vers APIs programmatiques pour gestion infrastructure réseau moderne.

---

## 1. CLI vs Programmabilité: Problématique

### 1.1 Limites CLI

**Avantages CLI**:
- ✓ Interaction directe et immédiate
- ✓ Feedback immédiat
- ✓ Pas connaissance programmation requise
- ✓ Configuration granulaire simplement

**Inconvénients CLI** (critique):
- ✗ **Risque misconfiguration élevé**: humain tape commandes
- ✗ **Erreurs humaines**: répétition manuelle multiples devices
- ✗ **Pas d'automatisation**: scaling devient prohibitif
- ✗ **Coûts élevés complexité**: outages dus configuration erreurs

### 1.2 Automatisation CLI

**Outils CLI automation** réduisent risques:
- **Expect scripts**: interprétation texte bash
- **Ansible**: push config SSH-based
- **Puppet/Chef**: agent-based management
- **EEM**: Embedded Event Manager

---

## 2. APIs (Application Programming Interfaces)

### 2.1 Concept API

**API** = interface logicielle permettant **communication et manipulation données** entre applications/systèmes.

```
Logiciel A → [API] → Logiciel B
  (Requête)   (Contrat)  (Réponse)
```

### 2.2 API Directions dans Réseau

#### Northbound API
```
┌──────────────┐
│ Management   │ ← GUI, scripts, dashboards
│ Applications │
└───────┬──────┘
        │ Northbound API (HTTPS/TLS)
        ↓
┌──────────────┐
│ Network      │
│ Controller   │ ← DNA Center, APIC, etc.
│ (Orchestr.)  │
└───────┬──────┘
```

**Fonction**: Management logiciels → Controller

**Sécurité**: HTTPS/TLS (chiffrement), token authentication

#### Southbound API
```
┌──────────────┐
│ Network      │
│ Controller   │
└───────┬──────┘
        │ Southbound API (HTTPS/TLS, NETCONF, YANG)
        ↓
┌──────────────┐
│ Devices      │
│ (Router,     │ ← Configuration pushdown
│  Switch,     │
│  WAP)        │
└──────────────┘
```

**Fonction**: Controller → Devices

**Sécurité**: HTTPS/TLS, device credentials

---

## 3. REST APIs (RESTful Services)

### 3.1 Concept REST

**REST** (Representational State Transfer) = style architecture pour HTTP APIs utilisant **CRUD operations** pour manipulation données.

### 3.2 HTTP Methods: CRUD

| Opération | HTTP Verb | Action | Exemple |
|-----------|-----------|--------|---------|
| **Create** | POST | Créer ressource | POST /devices (créer device) |
| **Read** | GET | Récupérer ressource | GET /devices (lister tous) |
| **Update** | PUT | Remplacer ressource | PUT /devices/1 (remplacer config) |
| **Partial Update** | PATCH | Modification partielle | PATCH /devices/1 (modifier attribut) |
| **Delete** | DELETE | Supprimer ressource | DELETE /devices/1 (supprimer device) |

### 3.3 Avantages REST API

- **HTTP Standard**: utilise protocole web universel
- **Vendor Consistency**: interface commune tous vendors
- **Scalabilité**: stateless, load-balanceable
- **Intégration facile**: JSON/XML standard

### 3.4 Désavantages

- **REST API Deletion**: contraire API GET (données réellement supprimées)
- **Apprentissage**: courbe compréhension premiers pas

---

## 4. Postman: Testing REST APIs

### 4.1 Introduction Postman

**Postman** = application testant REST APIs sans code, interface graphique.

### 4.2 Sections Postman

```
┌─────────────────────────────────────┐
│        POSTMAN INTERFACE            │
├─────────────┬───────────────────────┤
│             │                       │
│ History     │  URL Bar              │
│ (Recent)    │  [GET] [https://...] │
│             │                       │
│ Collections │  [Send] [Params]      │
│ (Grouped    │  [Auth] [Headers]     │
│  requests)  │  [Body] [Tests]       │
│             │                       │
│ New Tab     │  [Response Window]    │
│ (Individual)│  Status: 200 OK       │
│             │  Body: [JSON output]  │
│             │                       │
└─────────────┴───────────────────────┘
```

### 4.3 Workflow Postman

**Étape 1**: Créer request
- URL: `https://sandboxdnac.cisco.com/api/v1/network-device`
- Méthode: GET
- Headers: `Content-Type: application/json`

**Étape 2**: Ajouter authentication
- Type: Basic Auth
- Username
- Password

**Étape 3**: Cliquer Send

**Étape 4**: Observer response
- Status: 200 OK = succès, 400/401/404/500 = erreur
- Body: JSON output contenant données

---

## 5. Data Formats: JSON vs XML

### 5.1 JSON (JavaScript Object Notation)

**JSON** = format données **clé/valeur**, simple, lisible.

Structure:
- **Objects**: `{ }` (dictionnaire)
- **Arrays**: `[ ]` (liste)
- **Primitives**: strings, numbers, booleans, null

Exemple:
```json
{
  "devices": [
    {
      "id": "device1",
      "hostname": "router1",
      "ipAddress": "192.168.1.1",
      "isActive": true,
      "interfaces": [
        {
          "name": "GigabitEthernet0/0",
          "status": "up"
        },
        {
          "name": "GigabitEthernet0/1",
          "status": "down"
        }
      ]
    }
  ]
}
```

**Avantages JSON**:
- ✓ Simpler que XML
- ✓ Directement JavaScript-compatible
- ✓ Moins verbeux
- ✓ Parsing rapide

### 5.2 XML (Extensible Markup Language)

**XML** = format données basé **tags**, structure hiérarchique.

Syntaxe: `<tag>content</tag>`

Exemple équivalent:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<devices>
  <device>
    <id>device1</id>
    <hostname>router1</hostname>
    <ipAddress>192.168.1.1</ipAddress>
    <isActive>true</isActive>
    <interfaces>
      <interface>
        <name>GigabitEthernet0/0</name>
        <status>up</status>
      </interface>
      <interface>
        <name>GigabitEthernet0/1</name>
        <status>down</status>
      </interface>
    </interfaces>
  </device>
</devices>
```

**Inconvénients XML**:
- ✗ Verbeux (tags répétés)
- ✗ Parsing plus complexe
- ✗ Taille fichier augmentée

**JSON > XML** pour APIs modernes

---

## 6. HTTP Status Codes

### 6.1 Catégories Status Codes

| Code Range | Catégorie | Signification |
|------------|-----------|---------------|
| **1xx** | Informatif | Demande reçue, traitement continue |
| **2xx** | Succès | Opération complétée avec succès |
| **3xx** | Redirection | Action supplémentaire requise |
| **4xx** | Client Error | Demande invalide ou non-autorisée |
| **5xx** | Server Error | Serveur fail compléter demande |

### 6.2 Codes Courants

| Code | Signification | Contexte |
|------|---------------|---------|
| **200 OK** | Succès GET/PUT | Données retournées |
| **201 Created** | Succès POST | Ressource créée |
| **204 No Content** | Succès DELETE | Ressource supprimée |
| **400 Bad Request** | Erreur client | Paramètres invalides |
| **401 Unauthorized** | Auth manquante | Pas credentials/token |
| **403 Forbidden** | Permission refusée | Crédentials insuffisants |
| **404 Not Found** | Ressource introuvable | Route API inexistante |
| **500 Server Error** | Erreur serveur | Bug API backend |
| **503 Unavailable** | Service down | Serveur maintenance |

---

## 7. Cisco DNA Center: APIs

### 7.1 DNA Center Architecture

**DNA Center** = contrôleur/orchestrateur Cisco pour infrastructure.

Component hierarchy:
```
┌─────────────────────────────────────┐
│     DNA Center (Controller)          │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ REST API (Northbound)       │   │
│  │ /api/system/v1/             │   │
│  │ /api/v1/network-device      │   │
│  └─────────────────────────────┘   │
│           ↓                         │
│  ┌─────────────────────────────┐   │
│  │ NETCONF/YANG (Southbound)   │   │
│  │ Vers devices                │   │
│  └─────────────────────────────┘   │
│           ↓                         │
│  ┌─────────────────────────────┐   │
│  │ Devices (Router, Switch)    │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

### 7.2 DNA Center Authentication: Token API

**Token API** = premier appel pour obtenir **authentication token** (session identifier).

Endpoint:
```
POST https://sandboxdnac.cisco.com/api/system/v1/auth/token
```

Configuration:
- **Method**: POST
- **Auth**: Basic Auth (username + password)
- **Headers**: `Content-Type: application/json`
- **Body**: Empty ou `{}`

Réponse:
```json
{
  "Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Utilisation Token**: Ajouter header pour requêtes suivantes:
```
X-Auth-Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### 7.3 Network Device Inventory API

**Endpoint**: GET `/api/v1/network-device`

Configuration:
```
Method: GET
URL: https://sandboxdnac.cisco.com/api/v1/network-device
Headers:
  Content-Type: application/json
  X-Auth-Token: [token obtenu authentification]
```

Réponse:
```json
{
  "response": [
    {
      "id": "device-uuid-1",
      "hostname": "router1",
      "managementIpAddress": "192.168.1.1",
      "platformId": "Cisco ASR1000",
      "softwareVersion": "16.12.03",
      "serialNumber": "ABC123",
      "site": "New York"
    },
    {
      "id": "device-uuid-2",
      "hostname": "switch1",
      "managementIpAddress": "192.168.1.2",
      "platformId": "Cisco Catalyst 9300",
      "softwareVersion": "16.12.04",
      "serialNumber": "DEF456",
      "site": "Chicago"
    }
  ],
  "count": 2
}
```

---

## 8. JSON Response Format

### 8.1 Structure Response

```json
{
  "statusCode": 200,
  "message": "Success",
  "response": {
    // données requêtées
  }
}
```

### 8.2 Erreur Response

```json
{
  "statusCode": 401,
  "message": "Unauthorized - Invalid credentials",
  "error": "Authentication failed"
}
```

---

## 9. GitHub: Version Control & Collaboration

### 9.1 Concept GitHub

**GitHub** = plateforme **version control** + collaboration code.

Utilité:
- **Version Control**: tracking changes fichiers (git)
- **Collaboration**: multiple développeurs même projet
- **Backup**: code stocké cloud
- **Community**: partage code public

### 9.2 Workflow GitHub Basique

```
Local Machine                GitHub Repository
  (git repo)                    (cloud)
     │                            │
  1. Code editing  ────(git add)──→ 2. Staging
     │                            │
  3. git commit ───(git commit)──→ 4. Local history
     │                            │
  5. git push ─────(git push)────→ 6. Remote master
     │                            │
  7. Pull request ──→ Review ──→ 8. Code review
     │                 │
  9. git merge ←──────┘ Approvalsa
```

---

## 10. Python: Programmation Automatisation

### 10.1 Rôle Python

**Python** = langage programmation **utilisé automatisation réseau** (Ansible playbooks, API calls, data parsing).

### 10.2 Avantages Python pour Réseau

- ✓ Syntaxe simple, apprentissage rapide
- ✓ Libraries riches: `requests` (HTTP), `paramiko` (SSH), `netmiko` (Cisco CLI)
- ✓ Cross-platform (Windows/Linux/macOS)
- ✓ Communauté large (DevNet)

### 10.3 Python HTTP API Call Exemple

```python
import requests
from requests.auth import HTTPBasicAuth

# DNA Center Token Auth
token_url = "https://sandboxdnac.cisco.com/api/system/v1/auth/token"
response = requests.post(
    token_url,
    auth=HTTPBasicAuth('admin', 'Cisco123'),
    headers={'Content-Type': 'application/json'},
    verify=False  # ignoré self-signed certs (lab)
)

token = response.json()['Token']
print(f"Token: {token}")

# Get Network Devices
device_url = "https://sandboxdnac.cisco.com/api/v1/network-device"
headers = {
    'Content-Type': 'application/json',
    'X-Auth-Token': token
}

response = requests.get(device_url, headers=headers, verify=False)
devices = response.json()['response']

for device in devices:
    print(f"Device: {device['hostname']} ({device['managementIpAddress']})")
```

---

## 11. Cisco DevNet

### 11.1 Définition
**Cisco DevNet** = plateforme apprentissage + ressources + sandboxes pour développeurs.

### 11.2 Ressources DevNet

- **Sandboxes**: environnements lab gratuits
  - DNA Center Sandbox
  - NETCONF/YANG Sandbox
  - ISE Sandbox
- **Certifications**: DevNet Associate, DevNet Professional
- **Community**: forum, code examples
- **Documentation**: APIs, SDKs guides

---

## 12. Autres Concepts Programmabilité

### 12.1 WebHooks
Callbacks HTTP notifiant événements:
```
Device A → [Event] → Api calls webhook → App B
```

### 12.2 Rate Limiting
Contrôle nombre requêtes/secondes:
```
Max 100 requêtes/min → au-delà = 429 Too Many Requests
```

### 12.3 API Versioning
Multiple versions API simultanément:
```
/api/v1/
/api/v2/
/api/v3/
```

---

## 13. Points d'Examen Clés

✓ **CLI vs Automation**: CLI risque humain, automation réduit erreurs  
✓ **Northbound API**: Management → Controller (HTTPS/TLS)  
✓ **Southbound API**: Controller → Devices (config pushdown)  
✓ **REST API**: HTTP CRUD (POST/GET/PUT/PATCH/DELETE)  
✓ **Postman**: API testing GUI  
✓ **JSON**: objet/array/string, simpler XML  
✓ **XML**: tags, verbeux  
✓ **HTTP Codes**: 1xx (info), 2xx (success), 3xx (redirect), 4xx (client error), 5xx (server error)  
✓ **DNA Center Token API**: POST /auth/token, Basic Auth  
✓ **DNA Center Device API**: GET /network-device, X-Auth-Token header  
✓ **GitHub**: version control, collaboration, backup  
✓ **Python**: automation language, requests library REST
