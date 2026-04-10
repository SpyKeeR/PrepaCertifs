---
title: "Module 25: Secure Network Access Control"
module: 25
type: notes
topics: [SAFE, Talos, Threat Grid, AMP, AnyConnect, Umbrella, WSA, NAC]
difficulty: advanced
updated: 2026-03-18
---

# Module 25: Secure Network Access Control

## Vue d'ensemble
Le **Secure Network Access Control** (Module 25) constitue la première brique de la sécurité dans l'architecture ENCOR. Ce module couvre le framework SAFE, les technologies de protection contre les menaces et les contrôles d'accès réseau de Cisco.

---

## 1. Cisco SAFE (Security Architectural Framework)

### 1.1 Introduction au SAFE
Le **SAFE** (Cisco's Security Architectural Framework for Enterprise) est un framework holistique qui guide la conception de solutions de sécurité périmètre-to-cloud.

**Objectif principal**: Protéger les **6 PINs** (Physical Infrastructure Networks) dans l'architecture d'entreprise

### 1.2 Les 6 PINs du SAFE

| PIN | Description | Caractéristiques |
|-----|-------------|------------------|
| **Branch** | Sites distants/succursales | Accès internet direct, sécurité simplifiée |
| **Campus** | Siège social/bureaux principaux | Dense, complexe, multi-VLAN |
| **Data Center** | Centre de données | Stockage données critiques, hautes performances |
| **Edge** | Points de présence externes | IoT, partenaires, accès distant |
| **Cloud** | Infrastructure en cloud | AWS, Azure, GCP, hybride |
| **WAN** | Réseau étendu | Connexion inter-sites, mpls, sd-wan |

### 1.3 Les 6 SAFE Domains

Le SAFE divise la protection en **6 domaines opérationnels**:

1. **Management Domain**: supervision, orchestration, automatisation
2. **Security Intelligence Domain**: threat intelligence, analytics, visibilité
3. **Compliance Domain**: gouvernance, audit, conformité
4. **Segmentation Domain**: micro-segmentation, isolation de données
5. **Threat Defense Domain**: prévention intrusions, malware, DDoS
6. **Secure Services Domain**: chiffrement, VPN, web security

### 1.4 Attack Continuum

La défense se structure sur le continuum d'attaque en **3 phases**:

```
┌─────────────────────────────────────────────────────┐
│            ATTACK CONTINUUM (Cisco)                 │
├─────────────────┬──────────────┬────────────────────┤
│   BEFORE        │   DURING     │     AFTER          │
│  (Prévention)   │  (Détection) │   (Remédiation)    │
├─────────────────┼──────────────┼────────────────────┤
│ • Talos intel   │• Stealthwatch│ • AMP retrospection│
│ • Threat Grid   │• Threat Grid │ • Alert disposition│
│ • URL Filtering │• AMP sandbox │ • Incident response│
│ • Malware detect│• Behavioral  │ • Patch & remediate│
│ • Sandbox       │  analytics   │ • Threat hunting   │
└─────────────────┴──────────────┴────────────────────┘
```

---

## 2. Cisco Talos: Menace Intelligence

### 2.1 Présentation de Talos
**Cisco Talos** est l'organisation de renseignement sur les menaces de Cisco, fournissant des flux de menaces temps réel aux solutions de sécurité Cisco.

### 2.2 Sources des flux de Talos

Talos aggrège les données depuis **7+ sources**:

1. **Microsoft Disclosures**: exploits Microsoft, vulnérabilités Windows
2. **AMP Community Data**: détections de malwares des endpoints AMP
3. **Honeypots**: systèmes pièges captant attaquants
4. **AEGIS Platform**: analyse comportementale avancée
5. **Threat Feeds Externes**: partenaires tiers, ISAC
6. **Dynamic Analysis**: analyse comportementale en bac à sable
7. **Partenaires Cisco**: intégration données techniques

### 2.3 Utilisation de Talos
- Mise à jour des **signatures dans WSA/NGFW/AMP**
- **Threat Grid** intègre Talos pour disposition des fichiers
- **Stealthwatch** enrichit vis-à-vis anomalies réseau
- **Cisco Umbrella** utilise Talos pour blocage domaines/IPs

---

## 3. Cisco Threat Grid: Analyse Dynamique

### 3.1 Principes
**Threat Grid** réalise l'analyse dynamique (comportementale) de fichiers suspects, complétant l'analyse statique.

### 3.2 Analyse Statique vs Dynamique

| Aspect | Statique | Dynamique |
|--------|----------|-----------|
| **Méthode** | Inspection fichier seul | Exécution en environnement sécurisé |
| **Outil Cisco** | (non spécifique) | Threat Grid |
| **Détection** | Signatures, heuristiques | Comportements malveillants |
| **Temps** | Immédiat | Minutes à heures |
| **Évasion** | Peut échouer | Meilleure détection polymorphe |

### 3.3 Glovebox: Environnement Sandbox
**Glovebox** est l'environnement sandbox propriétaire Cisco pour observer le **comportement réel** du malware:

```
Fichier suspect
      ↓
  [Threat Grid Sandbox]
      ↓
   Glovebox (VM contrôlée)
      ↓
[Détection comportement malveillant]
      ↓
Disposition: Clean/Suspicious/Malware
```

### 3.4 Déploiement Threat Grid

Deux modes de déploiement:

1. **Cloud-Based**: service hébergé Cisco, scalabilité automatique
2. **On-Premises Appliance**: déploiement local/privé pour données sensibles

---

## 4. Cisco Advanced Malware Protection (AMP)

### 4.1 Vision AMP
**AMP** (Advanced Malware Protection) protège sur **tout le continuum d'attaque**:
- **Before**: détection précoce, fichiers suspects bloqués
- **During**: détection comportement malveillant temps réel
- **After**: malware connu → retrospection automatique

### 4.2 Architecture AMP

```
┌─────────────────────────────────────┐
│      AMP Cloud Infrastructure       │
│  ┌───────────────────────────────┐  │
│  │ Private Cloud | Public Cloud  │  │
│  └───────────────────────────────┘  │
└────────┬────────────────────────────┘
         │
    [AMP Connectors]
         │
    ┌────┴─────┬──────────┬──────────┬────────┐
    │           │          │          │        │
  Endpoints   Network    Email      Web     Meraki
   (Windows)  (NGFW)    (ESA)      (WSA)    (MX)
   (macOS)    (NGIPS)
   (iOS)      (ISRs)
   (Linux)
   (Android)
```

### 4.3 Composants AMP

#### AMP Cloud
- **Infrastructure centrale**: stockage analytique, intelligence menace
- **Cloud Public**: fournisseur tiers (AWS)
- **Cloud Privé**: déploiement client isolé
- **Talos Integration**: mises à jour signatures

#### AMP for Endpoints
Protège les devices personnels (Windows, macOS, iOS, Android, Linux):
- Isolation de fichiers malveillants
- Détection comportement

#### AMP for Networks
Protège les équipements réseau:
- **NGFW** (Next-Gen Firewalls)
- **NGIPS** (Next-Gen IPS)
- **ISRs** (Integrated Services Routers)

#### AMP for Email (ESA)
- **Cisco ESA** (Email Security Appliance)
- Détection pièces jointes/liens malveillants

#### AMP for Web (WSA)
- **Cisco WSA** (Web Security Appliance)
- Inspection contenu web, URLs malveillantes

#### AMP for Meraki
- Protection appliances Meraki MX
- API-based, cloud-native

### 4.4 iOS: Cisco Security Connector
En iOS, AMP for Endpoints s'appelle **Cisco Security Connector (CSC)** car iOS ne permet pas agents classiques.

---

## 5. Cisco AnyConnect: Accès VPN Sécurisé

### 5.1 Présentation
**AnyConnect** est le client VPN modulaire de Cisco, fournissant **chiffrement et posture devices**.

### 5.2 Protocoles VPN/Chiffrement

| Protocole | Description | Cas d'usage |
|-----------|-------------|-----------|
| **TLS/SSL** | Chiffrement HTTPS-style | Applications web, legacy |
| **IPsec IKEv2** | Protocole VPN natif | Mobilité, haute disponibilité |
| **Combinaison** | TLS/SSL + IPsec | Redondance, flexibilité |

### 5.3 Modules AnyConnect

**AnyConnect est modulaire** - chaque client peut avoir différents modules:

1. **VPN Core Module**: chiffrement TLS/SSL + IPsec
2. **Posture Module (HostScan)**: évalue conformité device
   - Antivirus actif?
   - Windows Firewall activé?
   - Patch OS appliqué?
3. **ISE Posture Module**: intégration Cisco Identity Services Engine
4. **Cisco Cloud Web Security Module**: filtrage cloud
5. **Stealthwatch Module**: visibilité trafic endpoint
6. **Cisco Umbrella Module**: DNS protection

### 5.4 Plateformes Supportées (8 plates-formes)

```
Windows | macOS | iOS | Android | Linux | Windows Phone | BlackBerry | ChromeOS
```

---

## 6. Cisco Umbrella: Défense DNS Cloud

### 6.1 Concept
**Cisco Umbrella** est une **défense DNS 100% cloud** qui bloque les domaines/IPs/URLs **avant que la connexion soit établie**.

### 6.2 Avantages DNS-Based

```
Demande utilisateur → Umbrella DNS (cloud)
                           ↓
                    (Vérifier domaine)
                           ↓
          [Domaine malveillant?] → Bloquer
          [Domaine légitime?]    → Résoudre IP
```

**Avantage**: Protection même si HTTPS (pas inspection contenu URL possible en HTTPS)

### 6.3 Architecture Umbrella

- **30 Global Data Centers**: latence très basse, HA
- **Anycast DNS**: même IP serveur, routage vers data center le plus proche
- **100% Uptime**: design critique service de Cisco
- **Redondance automatique**: basculement instant en cas défaillance

### 6.4 Capacités de Blocage

1. **Domaines Malveillants**: command & control botnets, exploits
2. **IPs Malveillantes**: serveurs attaquants
3. **URLs Malveillantes**: pages phishing, malware distribution
4. **Catégories**: jeux, réseaux sociaux, proxies, etc. (politique client)

---

## 7. Cisco Web Security Appliance (WSA)

### 7.1 Présentation
**Cisco WSA** (Web Security Appliance) est une **gateway de sécurité web** inspectant trafic HTTP/HTTPS.

### 7.2 Protection Before Attack

**Avant infection**, WSA intervient:
- **Web Reputation Filters**: réputation domaine/IP
- **URL Filtering**: blocage catégories non-approuvées
- **Application Usage Control**: blocage applications non-autorisées
- **Malware Inspection**: détection malware dans téléchargements

### 7.3 Protection During Attack

**Pendant l'attaque**, WSA collabore:
- **CASB Providers** (Cloud Access Security Brokers): surveillance cloud SaaS
- **Talos Intelligence**: données menace temps réel
- **AMP for Networks**: détection comportement malveillant
- **Zero-Day Detection**: heuristiques détection nouveaux malwares

### 7.4 Protection After Attack

**Après compromission**, WSA agit:
- **Continuous Scanning**: rescanning fichiers téléchargés
- **AMP Retrospection**: si fichier = malware → alerte rétroactive
- **Talos/Threat Grid Update**: dispositionchangement ("clean" → "malware")
- **Disposition Change Alerts**: notifications administrateur

### 7.5 Déploiement WSA

```
┌─────────────────────────────────────┐
│       WSA Deployment Options        │
├─────────────┬───────────┬───────────┤
│   CLOUD     │  VIRTUAL  │ ON-PREM   │
│ (SaaS)      │ (VM)      │ (Appliance)
├─────────────┼───────────┼───────────┤
│ • Scalable  │ • Flexible│ • Privé   │
│ • No CapEx  │ • Cost    │ • Contrôle│
│ • Managed   │ • Hybrid  │ • Donnéess│
└─────────────┴───────────┴───────────┘
```

---

## 8. Global Threat Analytics (GTA)

### 8.1 Définition
**GTA** (alias Cognitive Threat Analytics) = plateforme d'analyse analytique menace analysant **3 sources de données**:

1. **Web Traffic**: trafic passant par WSA
2. **AMP Endpoints Data**: détections endpoints AMP
3. **Stealthwatch Network Data**: anomalies réseau

### 8.2 Cas d'usage GTA

```
Utilisateur A → Visite site malveillant (WSA log)
Utilisateur B → Endpoint détecte malware (AMP alert)
Utilisateur C → Trafic anom. suspect (Stealthwatch alert)

              ↓ [GTA Analysis]

Corrélation: Même APT group attaquant multiple vecteurs
Verdict: Incident de sécurité coordiné
Réponse: Isolation immédiate tous utilisateurs
```

---

## 9. Network Access Control (NAC)

### 9.1 Concept
**NAC** (Network Access Control) = contrôle qui peut accéder au réseau et avec quels droits.

### 9.2 Méthodes de NAC

#### 802.1X (Port-Based)
- **Authentification**: utilisateur/device avant accès
- **Authorization**: VLAN assigné selon identité
- **Accounting**: logging accès

#### WebAuth (Web-Based)
- Redirection navigateur page login
- Saisie crédentials avant accès
- Flexibilité invités

#### MAB (MAC Authentication Bypass)
- Identification par adresse MAC
- Pas d'authentification utilisateur
- Pour devices non-802.1X (imprimantes)

#### Cisco TrustSec
- **Tag-based system**: étiquetage devices
- **SGT** (Security Group Tag)
- Segmentation basée identité/confiance

#### MACsec
- **Chiffrement couche 2**: entre switches
- **Intégrité données**: validation contenu
- Protection même LAN

---

## 10. Intégration Sécurité Cisco: Flux Complet

### 10.1 Scénario Complet

```
Utilisateur distant (AnyConnect) → Umbrella (DNS)
                                      ↓
                          [Domaine malveillant?]
                                      ↓
                              Bloquer si mal.
                                      ↓
        [Si domaine légitime] → NAC (802.1X/TrustSec)
                                      ↓
                          [Device posture OK?]
                                      ↓
                          Accès réseau accordé
                                      ↓
                     [Navigation web interne]
                                      ↓
                        WSA (proxy transparent)
                                      ↓
                              URL bloquée/scanning
                                      ↓
                              Talos + AMP + GTA
```

---

## 11. Résumé des Concepts Clés

| Composant | Fonction | Phase Attack |
|-----------|----------|--------------|
| **Talos** | Threat Intelligence | Before |
| **Threat Grid** | Dynamic Malware Analysis | Before/During |
| **AMP** | Malware Protection | Before/During/After |
| **AnyConnect** | Secure VPN + Posture | Before |
| **Umbrella** | DNS-Based Defense | Before |
| **WSA** | Web Security Gateway | Before/During/After |
| **GTA** | Threat Analytics Correlation | During/After |
| **NAC** | Network Access Control | Before |

---

## 12. Points d'Examen Clés

✓ **SAFE 6 PINs**: Branch, Campus, DC, Edge, Cloud, WAN  
✓ **Attack Continuum**: Before (prévention), During (détection), After (remédiation)  
✓ **Talos Sources**: 7+ sources (Microsoft, honeypots, AEGIS, Threat Grid)  
✓ **Threat Grid**: Sandbox Glovebox, analyse comportementale  
✓ **AMP**: Cloud + Connectors (Endpoints/Networks/Email/Web/Meraki)  
✓ **AnyConnect**: TLS/SSL + IPsec IKEv2, 8 plateformes, modules posture  
✓ **Umbrella**: 100% cloud DNS, 30 data centers, Anycast  
✓ **WSA**: Before/During/After protection, déploiement cloud/virtual/on-prem  
✓ **GTA**: Analytics web + endpoints + réseau  
✓ **NAC**: 802.1X, WebAuth, MAB, TrustSec, MACsec
