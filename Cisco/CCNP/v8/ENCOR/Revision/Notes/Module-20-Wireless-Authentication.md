---
title: "Module 20: Authentification des clients sans fil"
module: 20
type: notes
topics: [wireless-authentication, PSK, WPA2, WPA3, SAE, 802.1x, RADIUS, EAP, WebAuth]
difficulty: intermediate
updated: 2026-03-18
---

# Module 20: Authentification des clients sans fil

## Vue d'ensemble
L'authentification sans fil est la fondation de la sécurité WLAN. Ce module couvre les méthodes d'authentification courantes : Open Authentication, Pre-Shared Key (PSK), et l'authentification Enterprise via 802.1x/RADIUS avec support des protocoles EAP. Nous examinerons également les mécanismes modernes comme SAE (Simultaneous Authentication of Equals) pour WPA3.

## Authentification Ouverte (Open Authentication)

### Concept fondamental
L'authentification ouverte permet à tous les appareils de se connecter au réseau WLAN sans fournir d'identifiants. C'est la méthode la plus basique et la moins sécurisée.

**Caractéristiques clés:**
- **Pas de vérification d'identité**: Toute station peut envoyer une requête d'authentification 802.11
- **Configuration GUI WLC**: Security tab → Layer 2 → None (nettoyage du champ de sécurité)
- **Aucun chiffrement de sécurité**: Si nécessaire, utiliser une couche application (HTTPS) ou complément séparé
- **Cas d'usage**: Réseaux publics (aéroports, cafés), VLAN client invité

### Flux d'authentification Open
1. Client envoie IEEE 802.11 Authentication Request
2. AP répond avec Authentication Response (Success)
3. Client envoie Association Request
4. AP répond avec Association Response + SSID information

### Configuration WLC (GUI)
```
WLCs → Create New WLAN
├─ General tab: SSID = [nom]
├─ Security tab:
│  ├─ Layer 2 Security: None
│  └─ [Aucune autre configuration sécurité]
├─ Advanced tab: [paramètres optionnels]
└─ Interface/VLAN: Sélectionner interface/VLAN association
```

---

## Pre-Shared Key (PSK) - Authentification personnelle

### Versions PSK progressives
L'évolution PSK montre une amélioration continue de la sécurité:

#### WPA (Deprecated)
- **Statut**: Obsolète, ne plus déployer
- **Algorithme chiffrement**: TKIP (Temporal Key Integrity Protocol)
- **Échange clé**: PTK (Pairwise Transient Key) similaire WPA2
- **Vulnérabilités**: Attaques TKIP connues, KRACK

#### WPA2 (Standard actuel avec AES)
- **Adoption**: Standard de facto pendant 15+ ans
- **Algorithme chiffrement**: CCMP (Counter Mode with CBC-MAC Protocol) avec AES
- **Force**: 256-bit clés, protection approuvée
- **Protocole négociation**: 4-Way Handshake (détaillé ci-après)
- **Configuration clé pré-partagée**: ASCII ou hexadécimal, 8-63 caractères ASCII ou 64 hex
- **Limitations**: Pas de forward secrecy entre sessions, sensible à dictionary attacks hors ligne

#### WPA3 (Dernière génération - SAE)
- **Protocole substitutif**: SAE (Simultaneous Authentication of Equals) remplace 4-Way Handshake
- **Sécurité améliorée**: Protection dictionary attacks offlines, forward secrecy session-by-session
- **Implémentation**: Disponible Catalyst 9800/9100 WLCs, APs modernes 802.11ax+
- **Rétrocompatibilité**: WPA3-Personal mode (802.11w Mandatory Frame Protection)
- **Déploiement hybride**: Mode transition WPA2/WPA3 supporté

### 4-Way Handshake (WPA2-PSK détail)

#### Contexte cryptographique
Avant handshake, client et AP partagent PMK (Pairwise Master Key) = PSK (Pre-Shared Key) pour WPA2-Personal.

#### Processus étape-par-étape

**Étape 1: AP → Client (Message 1)**
- AP génère ANonce (AP Nonce) aléatoire
- AP envoie requête avec ANonce
- Client dérive PTK (Pairwise Transient Key) en utilisant ANonce + SNonce + Address MAC AP/Client

**Étape 2: Client → AP (Message 2)**
- Client génère SNonce (Station Nonce) aléatoire
- Client dérive PTK (même hash PMK + Nonces + MACs dans ordre inverse)
- Client envoie SNonce + MIC (Message Integrity Check) signé avec GTK initial (optionnel)

**Étape 3: AP → Client (Message 3)**
- AP vérifie MIC du message 2 (validation SMac = CMac)
- AP envoie Grand Total Key (GTK), Installation demande key material
- MIC signé avec KCK (Key Confirmation Key) dérivée PTK

**Étape 4: Client → AP (Message 4)**
- Client confirme GTK reçu + key material installation
- MIC validation complète client
- Installation paire de clés (PTK pour unicast, GTK pour broadcast/multicast)

#### Intégrité handshake
- **MIC computation**: HMAC-MD5 (WPA2) ou HMAC-SHA1 (WPA2-Personal mode avancé)
- **Détection attaque**: Clé incorrecte = MIC mismatch = rejet, client redémarre tentative
- **Replay protection**: Timestamp + Message Sequence Number

### Configuration PSK - WLAN 802.11i (WPA2)

#### Via GUI WLC
```
WLCs → Create New WLAN
├─ General tab: 
│  ├─ SSID: [nom réseau]
│  └─ Status: Enable
├─ Security tab:
│  └─ Layer 2:
│     ├─ **Authentication Method**: [PSK]
│     ├─ **WPA Policy**: WPA2
│     ├─ **WPA2 Encryption**: CCMP (AES)
│     └─ **Pre-Shared Key (PSK)**:
│        ├─ Key Type: ASCII [8-63 chars] OU Hex [64 chars]
│        └─ Pass Phrase: [saisir clé]
├─ Interface/VLAN tab: Sélectionner interface
└─ Advanced: Optional (QoS, Band Steering, etc.)
```

#### Paramètres avancés facultatifs
- **WPA2 Cipher Suites**: CCMP (recommandé), TKIP (backward compat, non recommandé)
- **Management Frame Protection**: Optional/Required/Disabled
- **PMF (802.11w)**: Activé pour WPA3 transition, protection Deauthentication floods

#### Bonnes pratiques PSK
- **Force Pass Phrase**: Minimum 20 caractères pour résister brute-force
- **Rotation**: Changer clé tous les 90 jours
- **Isolation guest**: VLAN séparé avec PSK couleur pour invités
- **Monitoring**: WLC client count + rate monitoring pour détecteur anomalies

---

## SAE (Simultaneous Authentication of Equals) - WPA3-Personal

### Contraste avec 4-Way Handshake

| Aspect | 4-Way Handshake (WPA2) | SAE (WPA3) |
|--------|--------|---------|
| **Paradigme** | Asymétrique (AP initiateur + client) | Équitable (mutuellement authentifié) |
| **Force dict attacks** | Faible offline (hash PMK réutilisable) | Très forte (impossible offline, clés dérivées distinctes) |
| **Forward secrecy** | Par clé PTK, réutilisée session | Par session (clés nouvelles chaque connexion) |
| **Frame count** | 4 frames EAPOL | Variable (dragonfly exchange) |

### Mécanisme SAE détail

#### Phase 1: Commitment Exchange
- **Dragonfly protocol** (RFC 7748 inspiré): Client et AP échangent engagements (commitments)
- **MAC filtering**: Proof-of-work léger (anti-DoS) évalué côté récepteur
- **Password encoding**: PMK généré via Dragonfly, non dérivé 4-way

#### Phase 2: Confirm Exchange
- **Échange confirmations** (confirm messages) validant engagement mutuellement
- **Clés session-specific**: Clés unicast (PTK) générées fresh, aucune réutilisation

#### Résistance attacks
- **Brute-force dictionary**: Attaque exige 1 tentative par connection on-the-wire (infaisable réseau)
- **Forward secrecy**: Compromise clé session N ≠ compromise sessions N+1 ou N-1
- **PMF integration**: Management Frame Protection obligatoire WPA3-Personal, protection deauth attacks

### Configuration WPA3-Personal (Catalyst 9800 WLC)
```
WLCs → Create New WLAN
├─ Security tab:
│  └─ Layer 2:
│     ├─ Authentication Method: [PSK]
│     ├─ WPA Version: WPA3-Personal [OU WPA2/WPA3 Transition]
│     ├─ WPA3 Encryption: CCMP (AES)
│     ├─ Pre-Shared Key (PSK):
│     │  └─ [25+ caractères recommandé]
│     └─ 802.11w (MFP): **Required**
└─ [Autres paramètres standard]
```

---

## Authentification Enterprise: 802.1x et RADIUS

### Architecture 802.1x (Port-Based Network Access Control)

#### Rôles trois-participants

**1. Supplicant (Client - Station WLAN)**
- Entité demandant accès
- Envoie EAP messages via EAPOL (EAP over LAN)
- Signe à l'authenticator avec credentials (username/password, certificat, etc.)

**2. Authenticator (WLC - Wireless Controller)**
- Intermédiaire entre client et serveur AAA
- Agit comme pont/proxy:
  - Encapsule EAPOL frames → RADIUS → serveur authentification
  - Détermine succès/échec basé réponse RADIUS
  - Applique policies post-authentification (VLAN asignment, QoS)
- Ne valide PAS directement credentials (délégué serveur)

**3. Authentication Server (Serveur RADIUS - ISE/FreeRADIUS)**
- Valide credentials utilisateur
- Renvoie **Accept** ou **Reject** + attributes (VLAN, ACLs, timeout)
- Communique uniquement avec authenticator (WLC), jamais directement client

#### Standard IEEE 802.1x
- **Port state model**: Controlled port (accès restreint) → Authorized (accès full)
- **Deauthentication handling**: Suppression client = port state → controlled (accès coupé)
- **Timeout supplicant**: Si aucune response EAP dans délai → déconnexion client

### Configuration RADIUS côté WLC

#### Ajout serveur RADIUS en GUI

```
WLC Management Interface (Browser - management IP)
├─ Administration → AAA → RADIUS → Authentication
├─ [Button] New
│  ├─ IP Address: [ISE/RADIUS server IP]
│  ├─ Shared Secret: [secret clé partagée - similaire configs réseau]
│  ├─ Port: [1812 - default] (modifiable si serveur custom port)
│  ├─ Timeout: [5 secondes - default]
│  ├─ Retries: [2 - default]
│  └─ ✓ Enable Network User Authentication
│     └─ [Validation checkbox - critique pour 802.1x client auth]
└─ [Save/Apply]
```

#### Paramètres critiques RADIUS
- **Shared Secret**: Identique config serveur RADIUS, ne transiter jamais non-encrypted (même HTTPS WLC)
- **Port 1812**: UDP authentification (port 1813 = accounting, différent)
- **Network User checkbox**: Activer pour 802.1x supplicant (client) authentication (vs MAC auth)

### Configuration WLAN avec 802.1x

#### Activation 802.1x en GUI WLC

```
WLCs → Create New WLAN [OU Edit Existant]
├─ General tab:
│  ├─ SSID: [nom réseau]
│  └─ Status: Enabled
├─ Security tab:
│  └─ Layer 2:
│     ├─ Authentication Method: **802.1x**
│     ├─ WPA Policy: WPA2 [OU WPA3 si APs support]
│     ├─ WPA2 Encryption: CCMP (AES)
│     ├─ Managed Key Caching: [Enabled - optimise reconnect = Fast Roaming]
│     └─ [RADIUS servers not visible ici - see separate AAA tab]
│
├─ AAA Servers tab:
│  └─ **Secondary AAA Servers**:
│     ├─ RADIUS Accounting: [Sélectionner serveur RADIUS]
│     ├─ RADIUS Authentication: [Sélectionner serveur RADIUS primaire + failover]
│     └─ Max Retries RADIUS: [3 - default]
│
├─ Interface/VLAN tab:
│  ├─ Interface: [Sélectionner interface WLC - ex: management]
│  └─ VLAN: [Sélectionner VLAN destination]
│
└─ Advanced tab:
   ├─ Mobility Anchor: [Optional - roaming WLC primaire]
   └─ [Autres options facultatives]
```

#### Handshake 802.1x complet (WPA2 + RADIUS)
```
Phase 1: EAPoL Exchange (Client ↔ WLC)
├─ Client → WLC: EAPOL-Start
├─ WLC → Client: EAP-Request/Identity
├─ Client → WLC: EAP-Response/Identity [username]
└─ [Forwarding to RADIUS]

Phase 2: RADIUS Exchange (WLC ↔ RADIUS Server)
├─ WLC → RADIUS: Access-Request [username + EAP message]
├─ RADIUS → WLC: Access-Challenge [EAP prompt - ex: password]
├─ WLC → RADIUS: Access-Request [EAP response - ex: password]
├─ [Validation RADIUS - typically via LDAP Backend]
└─ RADIUS → WLC: Access-Accept [+ VLAN/QoS attributes]

Phase 3: 4-Way Handshake (Client ↔ WLC)
├─ PMK established (shared from RADIUS MSK)
├─ Client ↔ WLC: 4-Way Handshake (WPA2 standard)
└─ -> Client: Online + DHCP

Post-Authentication:
├─ WLC apply RADIUS attributes: VLAN reassignment, QoS policies
├─ Client DHCP request within vlan (typically)
└─ RADIUS CoA (Change-of-Authorization) pour inline policy updates
```

### EAP (Extensible Authentication Protocol)

#### Rôle EAP
EAP n'est **pas une méthode d'authentification unique** mais un **framework flexible** supportant multiples méthodes. Ce design permet:
- Déployer diverses technos d'authentification (password, certificate, OTP, etc.)
- Éviter remplacement complet infrastructure si nouvelle méthode émerge
- Intégration identity services (LDAP, AD, RADIUS, 2FA)

#### Types EAP courants en déploiement

| Type EAP | Description | Sécurité | Déploiement |
|----------|----------|----------|----------|
| **EAP-TLS** | Client + server certificate mutuels | Très haute (TLS tunnel) | Entreprise exigeante |
| **EAP-PEAP** (Microsoft) | Server cert, client password in tunnel | Haute (tunnel TLS sécurisé password) | Windows + ISE/AD |
| **EAP-TTLS** | Server cert, client password/token in tunnel | Haute (similaire PEAP) | Déploiement hétérogène |
| **EAP-FAST** | Lightweight, session resumption, provisioned PAC | Moyenne (PAC-based, pas certs) | Performance-critical, mobiles |
| **EAP-MD5** | Legacy, password basic | **Basse (no encryption)** | **NE PAS DÉPLOYER** |

#### Intégration ISE (Identity Services Engine)
```
ISE Architecture:
├─ Policy Service Node (PSN): AAA logic, RADIUS backend
├─ Monitoring & Troubleshooting (MnT): Logs, reports, real-time dashboard
└─ Inline Posture Validation: Device health check pré-network access

Policy Engine (en ISE):
├─ Authentication Policy:
│  ├─ Identity: External (LDAP/AD) vs ISE InternalDB
│  └─ IF <conditions> THEN <authentication method>
├─ Authorization Policy:
│  ├─ IF <identity conditions + device posture> THEN <VLAN/QoS/ACL>
│  └─ Example: IF [Authenticated User] AND [Endpoint.Type == "MacOS"] THEN [VLAN=300+QoS=2Mbps]
└─ Change-of-Authorization (CoA): Mid-session policy update (ex: downgrade QoS si posture fails)
```

### WebAuth (Captive Portal Authentication)

#### Architecture WebAuth
WebAuth offre authentification non-802.1x via HTTP redirect + portal login.

**Cas d'usage:**
- Guest networks (accès public + billing)
- Bring-Your-Own-Device (BYOD) - alternative 802.1x certificats
- Rapid onboarding guest access (no credential install needed)

#### Flux WebAuth

```
1. Client associe WLAN [webauth enabled, no security Layer 2]
2. WLC DHCP server assigne IP (web-auth vlan)
3. Client DNS request → redirect Web Portal
4. Browser automatic open (Captive Portal)
   ├─ Login page: username/password [OU guestcode]
   └─ [Internal ISE or Radius backend validating]
5. Browser → DHCP option 150 (Cisco default)
   └─ OR DNS-based redirect (RFC 6694)
6. Portal check authentication status
   ├─ IF accepted → HTTP redirect to success page + WLC apply policy
   ├─ WLC switch client VLAN to main corp vlan (if configured)
   └─ Client online avec permissions appropriées
```

#### Configuration WLC WebAuth

```
WLCs → Create New WLAN
├─ General: SSID = [nom]
├─ Security tab → Layer 2: **None** [pas EAP/PSK]
├─ Web-Based Authentication (WBA) tab:
│  ├─ ✓ Enable Web-Based Authentication
│  ├─ AAA Servers:
│  │  └─ Sélectionner serveur RADIUS pour authentication backend
│  ├─ Web Authentication Type: Splash (redirection URL), Internal (WLC hosted)
│  ├─ Redirect URL: [portal login page - ex: ISE portal URL]
│  └─ Success Redirect: [success page URL ou re-apply policy]
├─ Advanced tab:
│  ├─ DHCP Server: Enable + configure DHCP scope
│  │  └─ [IP range pour web-auth users]
│  └─ Guest Isolation: IF enabled → clients cannot communicate peers (guest-only)
└─ Interface/VLAN: web-auth isolation vlan
```

#### Secondary RADIUS (Optionnel)
```
WLAN → AAA Servers → Secondary RADIUS (WBA):
├─ Sélectionner serveur RADIUS alternatif
├─ Failover logic: Primaire down → Secondary activated
└─ Typically ISE pour web-auth backend (vs external FreeRADIUS)
```

---

## Points clés à retenir

### Authentification comparative
- **Open**: Zéro sécurité, cas invité public uniquement
- **PSK**: Rapide déploiement, but All users = shared key = no individual audit
- **802.1x/EAP**: Enterprise-grade, user accountability, certificate/password auth options
- **WebAuth**: Guest-friendly, no device config, portal-based

### Sécurité progressive
1. **WPA2-PSK**: Minimum viable, acceptable PME avec clé complexe + rotation
2. **WPA3-Personal (SAE)**: Recommandé petites/moyennes orgs, device support croissant
3. **802.1x + EAP-TLS**: Maximum sécurité, certificate-based, audit complet
4. **ISE integration**: Policy-centric, CoA dynamic updates, posture compliance

### Points d'implémentation critique
- **Shared Secret RADIUS**: Ne jamais stocker plain text, utiliser vault
- **PMF 802.11w**: Obligatoire WPA3, recommandé WPA2 (protection deauth floods)
- **PSK strength**: Pas dicts humains, 20+ caractères aléatoires
- **RADIUS failover**: Toujours configuration secondaire RADIUS pour HA
- **VLAN isolation**: Supplicants authentification respecte VLAN boundary (compliance/isolation)

---

## Ressources d'étude complémentaires
- RFC 4017 (EAP overview)
- RFC 7748 (Dragonfly for WPA3-SAE)
- Cisco ISE Administration Guide (EAP policy configuration)
- 802.1x/802.11i standards (IEEE official docs)
