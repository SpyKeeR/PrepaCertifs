# Module 18 : Infrastructure Wireless
## Notes Complètes de Révision

---

## 1. TOPOLOGIES WIRELESS LAN

### Modes d'AP : Autonomous vs Lightweight

**Mode Autonomous (Standalone AP):**

Un AP autonome est une unité complète et indépendante – elle contient son propre système d'exploitation (IOS), sa propre RAM/Flash, sa propre configuration locale. Elle n'a besoin d'aucun « contrôleur » pour fonctionner.

Chaque AP autonome:
- Gère ses propres paramètres SSIDs
- Traite l'authentification et l'encryption client localement
- Agit comme point d'accès à un réseau VLAN spécifique
- Possède sa propre adresse IP de gestion
- Envoie trafic client directement sur le réseau commuté

**Mode Lightweight (Contrôlé):**

Un AP léger est dépendant d'un contrôleur WLC (Wireless LAN Controller) pour ses fonctions:
- Le WLC envoie la configuration de l'AP au démarrage
- Le WLC traite les décisions de roaming
- Le WLC gère l'authentification centralisée des clients
- L'AP devient simplement une extension radio du WLC
- Relationship: CAPWAP tunnel entre AP-WLC (Control and Provisioning of Wireless Access Points)

### Topologie Autonome

**Architecture:**

```
Client Wi-Fi → AP Autonome → Commutateur L3/L2 → Réseau Entreprise (IOS chaque AP)
```

**Caractéristiques:**
- Chaque AP est indépendant
- Clients se connectent à VLAN spécifique mappé à cet AP
- Pas de tunnel entre APs
- Client-to-client via commutateur réseau ou directement via AP (dépend de configuration)

**Avantages:**
- Configuration simple pour petits déploiements (1-3 APs)
- Pas besoin de WLC coûteux
- Indépendance: perte d'un AP n'affecte pas les autres
- Latence faible : trafic client direct sans tunnel

**Limitations:**
- Pas de mobilité client automatique (client doit se re-authentifier quand change d'AP)
- Configuration manuelle sur CHAQUE AP
- Mise à jour logiciel sur chaque AP individuellement
- Pas centralisé – inefficace pour > 5-10 APs
- Pas de roaming transparent

### Topologie Centralisée avec WLC

**Architecture:**

```
AP-1 —┐
AP-2 ─┤═ CAPWAP Tunnel ═> WLC Central (Couche 3) ← VLANs/politiques centralisées
AP-3 —┘
```

**Splits MAC Architecture:**

Dans topologie centralisée, les fonctions 802.11 sont divisées:

- **AP Lightweight** : Gère real-time 802.11 (PHY/MAC frame timing critique)
- **WLC** : Gère security, NAS (Network Access Server), politiques, roaming, DHCP relay

Cependant, le trafic client (data plane) va souvent via le tunnel également.

**Topologie standard Ciscoienne:**

- Un WLC central (Catalyst 9800, 3504, etc.) peut supporte jusqu'à 6000 APs
- APs utilisent un lien d'accès (pas trunk) vers un commutateur L2
- Tous les APs peuvent être sur le même VLAN d'accès – le routage L3 réel se fait au WLC
- Le WLC est l'endroit unique où les VLANs client existent
- Les clients roaming gardent leur IP même en changeant d'AP (WLC gère l'ancrage)

**Avantages:**
- Scalabilité: une seule WLC gère des milliers d'APs
- Mobilité: WLC maintient l'association client travers APs
- Configuration centralisée: politiques appliquées sur WLC, propagées aux APs
- Roaming rapide: WLC optimise avec caching de clés (CCKM) ou 802.11r
- Sécurité: WLC point unique de contrôle access

**Limitations:**
- WLC est critique – défaillance = tous APs impactés
- Latence RTT AP→WLC doit rester < 100ms (exigence Cisco)
- WLC coûteux (matériel + licences)
- Trafic client tunnelisé = légèrement plus latence/overhead

### Topologie Embedded

**Architecture:**

```
WLC = embarqué dans Commutateur Access Layer L3
       │
       ├─ Suite de ports pour Ethernet
       ├─ Suite de radios pour Wi-Fi
       └─ CPU/RAM WLC intégré
```

**Caractéristiques:**
- WLC est physiquement situé dans un switch 3850/9300/Nexus
- Fusion des couches d'accès filaire et wireless
- APs sur même commutateur ou distants (via CAPWAP)
- Typiquement supporte 100-200 APs (moins que WLC centralisé)
- RTT faible pour APs physiquement proches

**Avantages:**
- Coût-efficace pour succursales/PME
- Même plate-forme pour trafic filaire et wireless
- Moins matériel à gérr
- CAPWAP RTT court = performance

**Limitations:**
- Commutateur failure = loss de wireless
- Moins d'APes supportés qu'un WLC dédié
- Encore centralisation (pas aussi flexible que autonomous)

### Mobilité Express

**Concept:**

Un AP avec WLC embarqué – « WLC in an AP ». Idéal pour sites multiples sans WLC dédié.

- Chaque site a son propre AP+WLC
- Les APs se connectent via CAPWAP
- Supporte typiquement 50-100 APs
- Très pour PME/multi-site

---

## 2. APPAIRAGE APS ET WLCS (ZERO-TOUCH DEPLOYMENT)

### Processus Zero-Touch Boot

Le protocole AP boot est conçu pour être aussi automatique que possible. Vous mettez un AP neuf sur le switch port d'accès (avec pouvoir en ligne), et il se trouve et se configure seul.

### Étapes de démarrage d'AP

**Étape 1 : Boot de l'AP**

L'AP démarre avec une petite IOS image (quelques MB). Il n'a pas les complètes fonctions 802.11 embeddées – juste le strict minimum pour les radio basiques et découverte WLC.

```
AP Boot: Loading IOS image...
```

**Étape 2 : Obtenir une adresse IP**

L'AP négocie une adresse IP via DHCP depuis le commutateur (ou config statique).

```
AP DHCP Request → Switch → IP acquired (192.168.1.100)
```

**Étape 3 : Découverte WLC**

L'AP cherche un WLC. Cisco supporte plusieurs méthodes (dans cet ordre):

1. **DHCP Option 43** : Le serveur DHCP peut indiquer la WLC IP
2. **DNS** : Résoudre « Cisco-Capwap-Controller.local » ou « CISCO-LWAPP-CONTROLLER »
3. **IP Helper** : Le switch local peut faire forward broadcast CAPWAP
4. **Défaut** : Recherche de multicast 224.0.1.44 (CAPWAP Multicast)
5. **Consolle Config** : Admin peut manuellement spécifier WLC IP

**Étape 4 : Construire tunnel CAPWAP**

Une fois que l'AP a identifié un WLC, il négocie un tunnel CAPWAP (couche 3 UDP).

```
AP: "Hello WLC, je voudrais rejoindre"
WLC: "D'accord, construisons un tunnel encrypté DTLS"
[Échange de certificats numériques pour sécurité]
```

**Étape 5 : Soumission de Join Request**

L'AP envoie une demande de rejoindre le WLC avec ses capacités, son modèle, etc.

```
AP: "Je suis Cisco AP3802, Wi-Fi 6, antenne MIMO 4×4"
WLC: "OK, réponse d'acceptation Join"
```

**Étape 6 : Téléchargement de l'image si nécessaire**

Le WLC vérifies si l'image IOS de l'AP correspond à sa version. Si non:

```
WLC: "Vous exécutez 17.3. Ma version est 17.9. Mise à jour"
AP: "Téléchargement depuis WLC... [Streaming binaire]\nRéboot"
AP: Redémarrage avec nouvelle image
→ Retour à Étape 3 (Discovery)
```

**Étape 7 : Téléchargement de la configuration**

Maintenant, l'AP (avec bonne image) reçoit la configuration du WLC:

- SSIDs (quel SSID diffuser)
- Paramètres de sécurité
- Channel et puissance
- Politiques de qualité de service

```
WLC sends config block:
  SSID "Corp-LAN"
  Auth: WPA2-Enterprise via RADIUS
  Channel: Auto
  ...
AP reçoit et applique
```

---

## 3. UTILISATION DES ANTENNES POUR COUVERTURE WIRELESS

### Types d'antennes et profils de couverture

**Omnidirectionnelle (Dipôle):**

- Rayon: sphérique (360° horizontal, champs verticaux)
- Cas d'usage: APs à plafond couvrant grande zone
- Exemple: Antenne dipôle classique 2.4 GHz (petit bâton)

**Directionnelle (Yagi, Patch):**

- Rayon: forcé dans direction (exemple, vers l'est)
- Cas d'usage: Point-to-point, extension distance
- Exemple: Antenne patch 5 GHz sur mur extérieur vers distant bâtiment

**MIMO Antennes:**

- Multiples éléments pour diversité
- Améliore SNR (signal-to-noise ratio)
- Cas d'usage: 802.11n/ac/ax clients

### Planification de déploiement

**Densité d'AP:**

Pour une couverture homogène sans trous, vous avez besoin d'APs suffisants. Règles générales:

- **2.4 GHz** : Portée ~50-80 mètres en intérieur (dépend des obstacles)
- **5 GHz** : Portée ~30-50 mètres (atténuation plus haute fréquence)
- **Overlap requis** : 20-30% pour roaming sans rupture client

**Dimensions de cellulaire:**

- Modèle prédictif: FSPL (Free Space Path Loss) ou modèle d'espace bâti
- Mesure post-déploiement: Wi-Fi surveille RSS (Received Signal Strength) des clients

**Placement Antenne:**

- **Au plafond** : Omnidirectionnelle optimale pour couverture étage
- **Murs** : Directionnelle pour zones spécifiques
- **Hauteur** : Au-dessus des obstacles principaux (baies, murs épais)
- **Distance APs** : ~25 mètres 2.4 GHz avec ~20% chevauchement

---

## Résumé et Points clés

1. **Autonomous**: Indépendant, simple, pas scalable > 10 APs
2. **Lightweight**: Dépendt WLC, scalable mille AP, roaming
3. **Centralisé**: WLC point unique contrôle, RTT < 100ms requis
4. **Embedded**: WLC dans switch, bon compromise
5. **Mobilité Express**: AP+WLC pour sites multiples
6. **AP Boot**: 7 étapes, design zero-touch (DHCP → Discovery → CAPWAP → Config)
7. **Antennes**: Omnidirectionnelle (couverture), Directionnelle (distance)

---

*Dernière révision : 18 mars 2026*
*Révision CCNP ENCOR Module 18*
