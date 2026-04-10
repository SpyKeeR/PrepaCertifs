# Module 19 : Roaming Wireless et Services de Localisation
## Notes Complètes de Révision

---

## 1. APERÇU DU ROAMING

### Association de client et transitions BSS

Un **BSS (Basic Service Set)** est une cellule wireless unique – un AP et tous les clients qui y sont connectés. Trois concepts fondamentaux :

**Association Client:**

Avant d'utiliser un BSS, un client establit une association:
1. Client scan (active/passive) pour découvrir APs
2. Client sélectionne AP et SSID
3. Authentification (802.1x, PSK, Open)
4. Client « associé » – peut maintenant transmettre trafic via cet AP

**Transitions BSS (Roaming):**

Lors que le client se déplace hors couverture d'un AP vers un autre :
1. Client détecte signal se dégrade de l'AP courant
2. Client initie scan probe request vers d'autres APs
3. Client sélectionne nouveau AP (fort signal, même SSID, meilleur RSSI)
4. Client envoie reassociation request au nouveau AP
5. **Brève déconnexion** (~100-500 ms) durant le processus

**Décision Roaming Client:**

Le client (pas le réseau) décide quand roamer. Algorithme PROPRIÉTAIRE du client:
- Client Windows peut avoir hysteresis 70 dBm
- Client Mac peut avoir règles différentes
- Client cellulaire peut être agressif (roamer souvent)
- Client IoT peut être conservateur (rester sur même AP même signal faible)

### Roaming dans Architecture Lightweight (Split-MAC)

Contrairement à Autonomous où chaque AP est indépendant, un WLC centralisé gère le roaming:

**Roaming Même WLC:**

Si client roame d'AP1 → AP2, tous deux connects au même WLC :

1. Client se réassocie à AP2
2. WLC met à jour table d'association client (MAC → AP2)
3. WLC sait où est le client maintenant
4. Trafic client rerouter immédiatement à AP2

**Roaming Entre WLCs Différents (Intercontroller Roam):**

Si AP1 et AP2 appartiennent à des WLCs différents, c'est complexe:

1. Client existant sur WLC1, AP1
2. Client roame vers AP2 (connecté à WLC2)
3. WLC2 détecte nouvelle association
4. WLC considère ce client « foreign » (intrus temporaire)
5. WLC2 contacte WLC1 (ancien contrôleur)
6. WLC1 envoie contexte client à WLC2 (clés, acl, etc.)
7. Roam progresse

### Processus Roaming Détail

**1. Scan Client:**

Client envoie probe requests sur canaux (rapidement):

```
Client: "Hey, anybody there?" (broadcast probe)
AP1: "I'm here! (RSSI -45 dBm)"
AP2: "Me too! (RSSI -65 dBm)"
AP3: "I'm here (RSSI -80 dBm)"
```

Client reçoit réponses, compare RSSI.

**2. Sélection et Tentative Réassociation:**

Client sélectionne meilleur (généralement RSSI plus fort):

```
Client → AP2: "Reassociation Request (Auth MAC XXXX)"
AP2: "Reassociation Response (Accept)"
```

**3. Impact DHCP et 802.1x:**

Deux choses potentiellement lentes durant roaming:

**DHCP Renewal:**
- Si client roame vers AP dans DIFFÉRENT subnet (VLAN different)
- Peut demander nouveau lease DHCP
- Typiquement rapide (< 100 ms)

**802.1x Re-authentication:**
- Si sécurité EAP requise, client re-auth avec RADIUS serveur
- TRÈS LENT (500 ms - 2 secondes!)
- Raison principale les techniques d'optimisation existent

### Techniques d'Optimisation Roaming

**1. CCKM (Cisco Centralized Key Management):**

Une seule WLC / serveur RADIUS fournit paire de clés à multiples APs:

- Client pre-estabelit authentification + keying avec une WLC
- Autre WLC ou AP « trusted » share les mêmes clés
- Client roame vers nouvel AP : clés alreadymémorized, pas de RADIUS needed
- Amélioration: 2-5 secondes → < 50 ms roaming time
- Limitation: Requiert CCX clients (Apple, Cisco, certain Android)

**2. Key Caching (802.11i):**

Client stocke jusqu'à 8 paires (AP MAC, PMK clé) localement :

- Quand client était sur AP1, enregistré (AP1-MAC, cached-key)
- Roame plus tard vers AP1 : clé déjà présente, pas Full EAP
- Accélère roaming vers APs déjà visités
- Standard 802.11i / WPA2 built-in

**3. 802.11r (Fast BSS Transition, FT):**

Processus roaming radio-aware COMPLÈTEMENT REDESIGNÉ:

- Client pre-position une dérivée de la clé d'authentification serveur (seule la WLC a la clé master)
- AP cache cette dérivée
- Roam ne nécessite PAS de RADIUS (keying derive localement)
- Amélioration : < 100 ms pour transition
- Supporte key caching + QoS parameters traverse APs
- Moderne, built-in 802.11-2020, mais nécessite support client/AP

**Comparaison Rapidité Roaming:**

| Technique | Temps Total Roaming |
|-----------|-------------------|
| **Aucune (roaming standard)** | 1-2 secondes (RADIUS needed) |
| **Key Caching (pre-cached)** | 200-500 ms |
| **CCKM** | 50-100 ms |
| **802.11r (FT)** | < 100 ms |

---

## 2. ROAMING INTERCONTROLLER (MULTI-CONTROLEUR)

### Roaming Même VLAN / Couche 2 Intercontroller

Quand un client roame d'une AP sur WLC1 à une AP sur WLC2, et les deux APs assignments MÊME VLAN (exemple, VLAN 100) :

**Procédure:**

1. Client initially sur WLC1, AP1, VLAN 100 (IP 192.168.100.X, gateway 192.168.100.1)
2. Client roame → WLC2, AP2, toujours VLAN 100 (même sous-réseau)
3. WLC2 reconnaît client via MAC (via Mobility List)
4. **Pas de tunnel requis** – client reste sur même VLAN/IP
5. Client continue sans re-DHCP ou re-auth majeure

**Terme:** Cette transition = « Layer 2 roam » ou « VLAN roam »

### Roaming VLAN Différent / Couche 3 Intercontroller

Scénario plus complexe: Client sur WLC1 VLAN 100, roame vers WLC2 VLAN 200 :

**Problème:**
- Client IP = 192.168.100.X (VLAN 100)
- Nouvel AP = VLAN 200 (subnet 192.168.200.0/24)
- Client ne peut pas rester 192.168.100.X dans VLAN 200 (wrong subnet!)

**Solution: WLC Tunneling (Anchor/Foreign Pattern):**

```
Client (192.168.100.X)
   │
   ├─ WLC1 (Anchor Controller, VLAN 100)
   │    └─ AP1 (VLAN 100, client associé inizial)
   │
   └─ WLC2 (Foreign Controller, VLAN 200)
        └─ AP2 (VLAN 200, client roame ici)
        
   Entre WLC1 ↔ WLC2: Tunnel de données établi
   (Client traffic: AP2 → Tunnel → WLC1 → VLAN 100)
```

**Procédure Détail:**

1. Client sur WLC1/VLA 100, reçoit DHCP IP 192.168.100.50
2. Client roame vers AP2 (WLC2, VLAN 200)
3. WLC2 identifie que c'est un client étranger (foreign)
4. WLC2 contacte WLC1 (Anchor) via CAPWAP ou liaison control
5. WLC1 accepte rôle d'Anchor (maintient client original VLAN/IP)
6. **Tunnel bidirectionnel établi** entre WLC1 ↔ WLC2
7. Client trafic sortant : 192.168.100.50 → AP2 → Tunnel WLC2 ↔ WLC1 → Sortir VLAN 100
8. Client trafic entrant : VLAN 100 → WLC1 → Tunnel → WLC2 → AP2 → Client

**Avantage:** Client gardant IP original (ne necessité DHCP release)

### Mobility Groups

Une **Mobility Group** est un groupe de WLCs qui se trust mutuellement et partagent info client:

**Configuration Mobility Group:**

```
WLC1 (Mobility List):
  WLC1 MAC: AA:BB:CC:01:01:01 (self, mobililty group "main")
  WLC2 MAC: AA:BB:CC:02:02:02 (peer, mobility group "main")
  WLC3 MAC: AA:BB:CC:03:03:03 (peer, mobility group "main")
  
WLC2 (identique):
  WLC1 MAC: AA:BB:CC:01:01:01 (peer, mobility group "main")
  WLC2 MAC: AA:BB:CC:02:02:02 (self)
  WLC3 MAC: AA:BB:CC:03:03:03 (peer)
```

**Roaming au sein Mobility Group (Fast):**

- WLCs dans même groupe = fast roaming (< 100 ms possible)
- Auth info cached, clés préparégées
- Roaming seamlessess

**Roaming ENTRE Mobility Groups (Slow):**

- Client roame de WLC1 (groupe1) → WLC4 (groupe2)
- WLC4 UNKNOWN cliente (pas dans mobility group)
- Full re-authentication required (1-2 secondes)
- Plus lent

---

## 3. SERVICES DE LOCALISATION (LOCATION SERVICES)

### Importance des Services Localisation

Cas d'usage:

- **Hospital Tracking**: Patients, équipements critiques positionnement
- **Retail**: Clients Wi-Fi anonymes tracking (store analytics)
- **Entrepôt**: Asset tracking, forklifts, inventory
- **Sécurité**: Rogue device detection, interference source location

### Limitation : Localisation Single AP

Avec un seul AP, on peut estimer DISTANCE via RSS (Received Signal Strength) :

- RSS = -40 dBm → Client très proche
- RSS = -80 dBm → Client loin

MAIS: Impossible déterminer DIRECTION ou EXACT LOCATION avec 1 seule AP.

### Trilatération Multi-AP (3+ APs Requis)

Avec 3 ou plus APs mesurant RSS simultanément vers un client :

**Procédure Trilatération:**

1. **AP1** mesure RSS = -50 dBm (client X mètres, rayon R1)
2. **AP2** mesure RSS = -65 dBm (client Y mètres, rayon R2)
3. **AP3** mesure RSS = -45 dBm (client Z mètres, rayon R3)

Mathématiquement, 3 cercles (intersection) définissent un point. Location du client = intersection exacte.

**Précision:**

- Meilleur RSS si 3-4 APs très proches
- Peut être ~2-5 mètres precision en idéal espaces
- Réalité: Walls, objets reflètent RF → imprecision

### Cartographie et Localisation Visuelle

Cisco DNA Spaces (ex Cisco Mobility Services Engine):

- **Importation de plan étage**: Upload floor plan image
- **Positionnement AP manuel**: Click sur floor plan où AP physique situé
- **Visualization**: Dashboard affiche **icône client** sur floor plan avec distance APs
- **Real-time tracking**: Client smartphone icon move pendant marche

### Décices Non-Associé (Rogue + Interference Detection)

Au-delà des clients connectés, on peut localiser TOUT dispositivo Wi-Fi:

**Devices Non-Associé:**

Tout périphérique Wi-Fi qui **n'essaie pas de connecter** mais **émet probe requests**:

- Smartphone new client cherchant SSID préféré
- Laptop dormant qui scan périodique
- Unknown AP rogue nearby

Network peut localiser ces via probe request RSS multiAP.

**Interférence Non-802.11:**

Certaines interférences NE SONT PAS du Wi-Fi standard:

- Four à micro-ondes (2.4 GHz)
- Téléphone sans fil vieux (900 MHz, pas Wi-Fi)
- Caméra vidéo propriétaire sans fil
- Dispositivos industrielspropriétaires

Ces émettent signal dans bande 2.4 GHz ou 5 GHz mais protocole UNKNOWN.

Network peut détecter via:
- Paquet non-802.11 reçu
- Energy présente mais pas décodable
- RSS triangulation → locate source

**Utilité:** Rogue device détecter et éliminer, interference source locate.

### RFID Integration

Active RFID Tags:

- Petit tag attaché objet (inventory, tool)
- Tag a transceiver Wi-Fi intégré
- Tag périodiquement wake, envoie probe request 802.11
- Network localise via RSS multiAP trilatération
- **Tracking personne/objet continu**

Passive RFID (moins commun en wireless context):

- Tag très petit, batterie-free
- Activelement reader (handheld scanner) pour lire
- Moins utile pour "real-time network tracking"

---

## Résumé et Points clés

1. **Roaming Client**: Client décide (scan RSS, sélectionne, réassocie). Brief déconnexion (~100-500 ms).

2. **Même WLC**: Roamning transparent, WLC met à jour association.

3. **Entre WLCs**: Anchor/Foreign pattern, tunnel données si VLAN different.

4. **Mobility Groups**: WLCs trust mutuellement. Même groupe = fast roaming. Cross-groupe = slow (re-auth).

5. **Optimisation**: CCKM (50-100 ms), Key Caching (200-500 ms), 802.11r (< 100 ms).

6. **Localisation**: RSS single AP = distance seulement. Trilatération 3+ APs = exact location.

7. **DNA Spaces**: Visual floor plan, client tracking, rogue detection.

8. **Interférence**: Non-802.11 sources localisable via RSS energia.

---

*Dernière révision : 18 mars 2026*
*Révision CCNP ENCOR Module 19*
