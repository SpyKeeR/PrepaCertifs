# Fiche Module 07 : Commutation Ethernet
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Standard Ethernet (IEEE 802.3)
- Technologie LAN la plus répandue
- Couche liaison de données (Couche 2)
- Évolutif : 10 Mbps → 100 Gbps et plus

---

## 📊 Variantes Ethernet

| Standard | Nom | Débit | Média |
|----------|-----|-------|-------|
| **10BASE-T** | Ethernet | 10 Mbps | Cuivre UTP Cat 3 |
| **100BASE-TX** | Fast Ethernet | 100 Mbps | Cuivre UTP Cat 5/5e |
| **1000BASE-T** | Gigabit Ethernet | 1 Gbps | Cuivre UTP Cat 5e/6 |
| **1000BASE-SX** | Gigabit Ethernet | 1 Gbps | Fibre multimode |
| **1000BASE-LX** | Gigabit Ethernet | 1 Gbps | Fibre monomode |
| **10GBASE-T** | 10 Gigabit Ethernet | 10 Gbps | Cuivre UTP Cat 6a |
| **10GBASE-SR** | 10 Gigabit Ethernet | 10 Gbps | Fibre multimode |
| **10GBASE-LR** | 10 Gigabit Ethernet | 10 Gbps | Fibre monomode |

**Format** : *XBASE-Y*
- **X** : Débit (10 = 10 Mbps, 100 = 100 Mbps, 1000 = 1 Gbps)
- **BASE** : Bande de base
- **Y** : Média (T = Twisted pair, S = Short fiber, L = Long fiber)

---

## 📊 Structure de la trame Ethernet

```
┌──────────┬────────┬──────┬────────┬──────────────┬──────┐
│ Preamble │  SFD   │ Dest │ Source │     Data     │ FCS  │
│  7 bytes │ 1 byte │6 byte│ 6 byte │  46-1500 B   │4 byte│
└──────────┴────────┴──────┴────────┴──────────────┴──────┘
```

### Champs de la trame Ethernet

| Champ | Taille | Description |
|-------|--------|-------------|
| **Préambule** | 7 octets | Synchronisation (pattern `10101010` × 7) |
| **SFD** | 1 octet | Délimiteur de début (`10101011`) |
| **MAC Destination** | 6 octets | Adresse MAC du destinataire |
| **MAC Source** | 6 octets | Adresse MAC de l'émetteur |
| **Type/Longueur** | 2 octets | Protocole L3 (0x0800 = IPv4, 0x86DD = IPv6, 0x0806 = ARP) |
| **Données** | 46-1500 octets | Paquet L3 encapsulé (MTU = 1500 octets) |
| **FCS** | 4 octets | Frame Check Sequence (CRC-32, détection d'erreurs) |

**⚠️ Tailles de trame Ethernet :**
- **Taille minimale** : 64 octets (hors préambule + SFD)
- **Taille maximale** : 1518 octets (hors préambule + SFD)
- **Jumbo frames** : Jusqu'à 9000 octets (datacenter, non standard)

**Padding :** Si données < 46 octets → Remplissage de zéros

---

## 📊 Adresse MAC (48 bits)

### Format de l'adresse MAC

```
┌─────────────────────┬──────────────────────┐
│   OUI (24 bits)     │  Device ID (24 bits) │
│  00:1A:2B           │     3C:4D:5E         │
└─────────────────────┴──────────────────────┘
```

**Structure :**
- **OUI** (Organizationally Unique Identifier) : 3 premiers octets (fabricant)
- **Device ID** : 3 derniers octets (numéro unique du fabricant)

**Notation :** XX:XX:XX:XX:XX:XX ou XX-XX-XX-XX-XX-XX (hexadécimal)

**Exemples d'OUI :**
- `00:1A:2B` : Cisco
- `00:50:56` : VMware
- `08:00:27` : VirtualBox

---

## 📊 Types d'adresses MAC

| Type | Format | Description | Exemple | Usage |
|------|--------|-------------|---------|-------|
| **Unicast** | Bit 0 = 0 | Un-à-un | `00:1A:2B:3C:4D:5E` | Communication normale |
| **Broadcast** | Tous bits à 1 | Un-vers-tous | `FF:FF:FF:FF:FF:FF` | ARP, DHCP Discover |
| **Multicast IPv4** | **`01:00:5E:--:--:--`** | Un-vers-groupe IPv4 | `01:00:5E:00:00:0A` | OSPF, EIGRP, streaming |
| **Multicast IPv6** | **`33:33:--:--:--:--`** | Un-vers-groupe IPv6 | `33:33:00:00:00:01` | OSPFv3, NDP, RIPng |

### ⚠️ IMPORTANT : Adresses MAC Multicast

**IPv4 Multicast :**
- **Format** : **`01:00:5E:xx:xx:xx`**
- Les **3 premiers octets** sont **`01:00:5E`**
- Les 23 bits restants = 23 bits de poids faible de l'adresse IPv4 multicast
- **Plage IPv4 multicast** : 224.0.0.0 à 239.255.255.255
- **Exemples** :
  - 224.0.0.10 (EIGRP) → `01:00:5E:00:00:0A`
  - 224.0.0.5 (OSPF) → `01:00:5E:00:00:05`

**IPv6 Multicast :**
- **Format** : **`33:33:xx:xx:xx:xx`**
- Les **2 premiers octets** sont **`33:33`**
- Les 32 bits restants = 32 bits de poids faible de l'adresse IPv6 multicast
- **Plage IPv6 multicast** : FF00::/8
- **Exemples** :
  - FF02::1 (tous les nœuds) → `33:33:00:00:00:01`
  - FF02::2 (tous les routeurs) → `33:33:00:00:00:02`

**Protocoles utilisant multicast :**
- **IPv4** : OSPF, EIGRP, PIM, streaming vidéo
- **IPv6** : OSPFv3, RIPng, NDP (Neighbor Discovery Protocol)

---

## 📊 Commutateur (Switch)

### Fonctions du commutateur
- **Segmentation du domaine de collision** : Chaque port = domaine de collision séparé
- **Apprentissage des adresses MAC** : Table MAC (CAM table)
- **Transmission des trames** : Vers le port approprié
- **Full-duplex** : Communication bidirectionnelle simultanée (pas de collisions)

### Table MAC (CAM Table)

| Adresse MAC | Port | VLAN | Âge |
|-------------|------|------|-----|
| 00:1A:2B:3C:4D:5E | Fa0/1 | 1 | 120 s |
| 00:50:56:AA:BB:CC | Fa0/2 | 1 | 80 s |
| 08:00:27:11:22:33 | Fa0/3 | 10 | 200 s |

**Commande de vérification :**
```cisco
show mac address-table
```

### Méthodes de transmission du switch

**1. Store-and-Forward (Stocker et transmettre)**
- **Fonctionnement** : Reçoit la trame complète, vérifie le FCS, puis transmet
- **Avantages** : Détection d'erreurs, pas de trames corrompues transmises
- **Inconvénients** : Latence plus élevée
- **Usage** : Switches modernes (méthode standard)

**2. Cut-Through (Traversée rapide)**
- **Fonctionnement** : Transmet dès réception de l'adresse MAC de destination
- **Avantages** : Latence très faible
- **Inconvénients** : Ne vérifie pas les erreurs, peut transmettre des trames corrompues
- **Variantes** :
  - **Fast-forward** : Transmet après adresse MAC destination (latence minimale)
  - **Fragment-free** : Transmet après 64 premiers octets (évite les collisions)

---

## 📊 Processus de transmission

### Unicast
1. **Source envoie la trame** avec MAC destination spécifique
2. **Switch consulte la table MAC** :
   - Si MAC destination connue → Transmet sur le port approprié
   - Si MAC destination inconnue → **Flooding** (diffusion sur tous les ports sauf source)
3. **Destination reçoit la trame**

### Broadcast
- **MAC destination** : `FF:FF:FF:FF:FF:FF`
- **Switch diffuse** sur tous les ports (sauf port source)
- **Tous les périphériques** reçoivent et traitent

### Multicast
- **MAC destination** : `01:00:5E:--:--:--` (IPv4) ou `33:33:--:--:--:--` (IPv6)
- **Switch diffuse** sur tous les ports (sauf si IGMP Snooping activé)
- **Seuls les périphériques abonnés** traitent

---

## 📊 Domaines de collision et de diffusion

| Domaine | Switch | Hub |
|---------|--------|-----|
| **Domaine de collision** | **Chaque port = domaine séparé** | Tous les ports = 1 domaine |
| **Domaine de diffusion** | Tous les ports = 1 domaine (par VLAN) | Tous les ports = 1 domaine |

**Avantages du switch :**
- ✅ Pas de collisions (full-duplex)
- ✅ Segmentation des domaines de collision
- ✅ Apprentissage des adresses MAC
- ✅ Transmission intelligente (pas de flooding inutile)

**Hub (obsolète) :**
- ❌ Half-duplex (collisions possibles)
- ❌ Tous les ports dans le même domaine de collision
- ❌ Diffuse tout le trafic (pas d'intelligence)

---

## 🔧 Commandes de vérification Switch

```cisco
show mac address-table              # Table MAC
show interfaces status              # État des interfaces
show interfaces <interface>         # Détails d'une interface
show interfaces trunk               # Interfaces trunk (VLAN)
show vlan brief                     # Résumé des VLANs
```

---

## 💡 À retenir absolument

✅ **Ethernet** = IEEE 802.3 (couche 2)  
✅ **Trame Ethernet** : Min 64 octets, Max 1518 octets (hors préambule)  
✅ **MTU Ethernet** : 1500 octets (taille max des données)  
✅ **Adresse MAC** : 48 bits (6 octets), format hexadécimal  
✅ **OUI** : 3 premiers octets (fabricant)  
✅ **Broadcast MAC** : `FF:FF:FF:FF:FF:FF`  
✅ **Multicast IPv4** : **`01:00:5E:--:--:--`**  
✅ **Multicast IPv6** : **`33:33:--:--:--:--`**  
✅ **Switch** : Segmente les domaines de collision, apprentissage MAC, full-duplex  
✅ **Store-and-Forward** : Vérifie FCS (méthode standard)  
✅ **Cut-Through** : Latence faible (pas de vérification erreurs)  
✅ **Flooding** : Diffusion quand MAC destination inconnue  
✅ **FCS** (Frame Check Sequence) : CRC-32, 4 octets  
✅ **1000BASE-T** : Gigabit Ethernet sur cuivre Cat 5e/6  
✅ **10GBASE-T** : 10 Gigabit Ethernet sur cuivre Cat 6a  
