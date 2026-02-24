# Fiche Module 06 : Couche liaison de données
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Couche 2 du modèle OSI

**Responsabilités principales :**
1. **Accès au média** : Contrôle qui peut émettre
2. **Encadrement (Framing)** : Encapsulation des paquets en trames
3. **Adressage physique** : Adresses MAC source et destination
4. **Détection d'erreurs** : Vérification de l'intégrité (CRC/FCS)

**PDU de la couche 2 : Trame (Frame)**

### Services de la couche liaison de données
- **Adressage** : Adresses MAC (48 bits)
- **Délimitation des trames** : Début et fin de trame
- **Contrôle d'accès au média** : Gestion des collisions (CSMA/CD)
- **Détection d'erreurs** : FCS (Frame Check Sequence) - CRC-32

**⚠️ Important :** La couche 2 **détecte** les erreurs mais ne les **corrige pas** (juste rejette)

---

## 📊 Sous-couches de la couche liaison de données

| Sous-couche | Nom | Rôle | Standard IEEE |
|-------------|-----|------|---------------|
| **LLC** | Logical Link Control | Interface avec couche réseau, identification protocole L3 | 802.2 |
| **MAC** | Media Access Control | Adresses MAC, encapsulation trames, accès média | Spécifique à chaque technologie |

**Schéma :**
```
Couche Réseau (Paquet)
        ↕
   LLC (802.2)
        ↕
   MAC (Trames, adresses MAC)
        ↕
Couche Physique (Bits)
```

---

## 📊 Topologies réseau

### Topologies WAN

| Topologie | Description | Avantages | Inconvénients |
|-----------|-------------|-----------|---------------|
| **Point-à-point** | Connexion directe entre deux nœuds | Full-duplex, pas de collisions, bande passante dédiée | Limité à 2 nœuds |
| **Hub-and-Spoke** | Hub central + sites périphériques | Centralisé, gestion simple | Hub = point de défaillance |
| **Mesh (Maillé)** | Full mesh (tous interconnectés) ou partial mesh | Haute redondance | Coûteux (liens = n(n-1)/2) |

**Protocoles WAN point-à-point :** HDLC, PPP

### Topologies LAN

| Topologie | Description | Usage moderne |
|-----------|-------------|---------------|
| **Bus** | Tous sur un câble unique | ❌ Obsolète (10BASE2, 10BASE5) |
| **Étoile** | Tous connectés à un switch central | ✅ Topologie LAN moderne |
| **Étoile étendue** | Hiérarchie de switches | ✅ Topologie d'entreprise |
| **Anneau** | Token Ring, FDDI | ❌ Obsolète (LAN) |

**Topologie logique Ethernet :** Bus (domaine de diffusion partagé)

---

## 📊 Structure d'une trame (générale)

```
┌─────────┬─────────┬──────────┐
│ Header  │  Data   │ Trailer  │
└─────────┴─────────┴──────────┘
```

**Composants :**

**1. En-tête (Header)**
- Adresse de destination (à qui)
- Adresse source (de qui)
- Type/Longueur (protocole L3 ou taille)
- Contrôle (selon le protocole)

**2. Données (Data/Payload)**
- Paquet de couche 3 (IP) encapsulé
- **MTU Ethernet** : 1500 octets

**3. Trailer (Queue)**
- **FCS** (Frame Check Sequence) : Détection d'erreurs (CRC)

---

## 📊 Types d'adresses de couche 2

| Type | Description | Exemple | Usage |
|------|-------------|---------|-------|
| **Unicast** | Un-à-un | MAC spécifique | Communication normale PC → PC |
| **Broadcast** | Un-vers-tous | `FF:FF:FF:FF:FF:FF` | ARP, DHCP Discover, Wake-on-LAN |
| **Multicast** | Un-vers-groupe | `01:00:5E:xx:xx:xx` (IPv4) | OSPF, EIGRP, streaming vidéo |

---

## 📊 Contrôle d'accès au média

### Topologies à accès contrôlé

**Exemples :**
- **Token Ring** : Jeton circulant (obsolète)
- **FDDI** : Fibre optique, anneau (obsolète)

**Caractéristique :** Pas de collisions (accès déterministe)

### Topologies à accès par contention

**Ethernet (CSMA/CD - Carrier Sense Multiple Access / Collision Detection)**

**Fonctionnement :**
1. **Écoute** : Le périphérique écoute si le média est libre
2. **Transmission** : Si libre, transmet
3. **Détection de collision** : Si deux transmettent en même temps → collision
4. **Backoff** : Attente aléatoire, puis retransmission

**⚠️ CSMA/CD obsolète aujourd'hui :**
- Switches modernes = full-duplex
- Pas de domaine de collision (communication bidirectionnelle simultanée)

**CSMA/CA (Collision Avoidance) :**
- Utilisé en Wi-Fi (802.11)
- Évite les collisions (ne les détecte pas)

---

## 💡 À retenir absolument

✅ **Couche 2** = Adressage MAC, encapsulation en trames, détection d'erreurs  
✅ **PDU Couche 2** = Trame (Frame)  
✅ **Sous-couches** : LLC (interface L3) + MAC (adresses MAC, accès média)  
✅ **FCS** (Frame Check Sequence) : Détection d'erreurs (CRC-32)  
✅ **Couche 2 détecte les erreurs** mais **ne les corrige pas** (juste rejette)  
✅ **MTU Ethernet** : 1500 octets (taille maximale des données)  
✅ **Adresse MAC broadcast** : `FF:FF:FF:FF:FF:FF`  
✅ **Topologie LAN moderne** : Étoile avec switches  
✅ **CSMA/CD** : Détection de collisions (Ethernet ancien, hubs)  
✅ **Full-duplex** : Pas de collisions (switches modernes)  
✅ **Ethernet logique** : Bus (domaine de diffusion partagé)  
✅ **Topologies WAN** : Point-à-point (HDLC, PPP), Hub-and-Spoke, Mesh  

**Trames selon la technologie :**
- **Ethernet** : 802.3
- **Wi-Fi** : 802.11
- **PPP** : Point-to-Point Protocol (WAN)
- **HDLC** : High-Level Data Link Control (WAN Cisco)
