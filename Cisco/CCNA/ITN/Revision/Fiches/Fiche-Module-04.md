# Fiche Module 04 : Couche physique
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Rôle de la couche physique (Couche 1)
- Transport des **bits** (0 et 1) sur le média physique
- Conversion des trames (couche 2) en signaux (électriques, lumière, ondes)
- Définit les spécifications électriques, mécaniques, procédurales

**Responsabilités :**
- Médias physiques (câbles, connecteurs)
- Encodage (représentation des bits)
- Signalisation (méthode de transmission)
- Bande passante (capacité du média)

---

## 📊 Terminologie de la couche physique

| Terme | Définition |
|-------|------------|
| **Bande passante** | Capacité théorique maximale (Mbps, Gbps) |
| **Débit (Throughput)** | Bande passante réelle mesurée |
| **Goodput** | Débit utile (sans overhead des en-têtes) |
| **Latence** | Délai de transmission de bout en bout |
| **Jitter** | Variation de la latence |

---

## 📊 Câblage en cuivre

### Caractéristiques
- **Transmission** : Impulsions électriques
- **Sensibilité** : Interférences EMI/RFI, diaphonie
- **Atténuation** : Perte de signal sur la distance
- **Distance max** : **100 mètres** (entre équipements actifs)

### Types d'interférences
- **EMI** (Electromagnetic Interference) : Moteurs, lumières fluorescentes
- **RFI** (Radio Frequency Interference) : Émetteurs radio, micro-ondes
- **Diaphonie (Crosstalk)** : Interférence entre fils voisins
  - **NEXT** : Near-End Crosstalk (extrémité proche)
  - **FEXT** : Far-End Crosstalk (extrémité éloignée)

### Types de câbles cuivre

| Type | Description | Usage | Protection |
|------|-------------|-------|------------|
| **UTP** (Unshielded Twisted Pair) | Paires torsadées non blindées | Le plus courant (Ethernet) | Torsade des paires |
| **STP** (Shielded Twisted Pair) | Paires torsadées blindées | Environnements bruyants | Blindage + torsade |
| **Coaxial** | Conducteur central + blindage | Câble TV, Internet câble | Blindage |

---

## 📊 Catégories de câbles UTP

| Catégorie | Bande passante | Application | Distance max |
|-----------|----------------|-------------|--------------|
| **Cat 3** | 10 Mbps | Téléphone, 10BASE-T | 100 m |
| **Cat 5** | 100 Mbps | 100BASE-TX (obsolète) | 100 m |
| **Cat 5e** | 1 Gbps | 1000BASE-T (Gigabit) | 100 m |
| **Cat 6** | 10 Gbps | 10GBASE-T (55 m max) | 100 m (1G), 55 m (10G) |
| **Cat 6a** | 10 Gbps | 10GBASE-T complet | 100 m |
| **Cat 7** | 10+ Gbps | Datacenters (blindé) | 100 m |

---

## 📊 Types de câbles Ethernet

### 1. Câble droit (Straight-through)
- **Utilisation** : Connexions **différentes**
  - PC → Switch
  - Routeur → Switch
  - PC → Hub
- **Broches** : Identiques des deux côtés (T568A-T568A ou T568B-T568B)

### 2. Câble croisé (Crossover)
- **Utilisation** : Connexions **identiques**
  - PC → PC
  - Switch → Switch
  - Routeur → Routeur
- **Broches** : T568A d'un côté, T568B de l'autre
- **Croisement** : 1↔3, 2↔6

### 3. Câble console (Rollover)
- **Utilisation** : Accès console (configuration initiale)
- **Broches** : Inversées (1↔8, 2↔7, etc.)

**⚠️ Auto-MDIX** : Détection automatique du type de câble (équipements modernes)

---

## 📊 Standards de câblage T568A et T568B

**Connecteur RJ-45 (8 broches) :**

| Broche | T568A | T568B |
|--------|-------|-------|
| 1 | Blanc/Vert | Blanc/Orange |
| 2 | Vert | Orange |
| 3 | Blanc/Orange | Blanc/Vert |
| 4 | Bleu | Bleu |
| 5 | Blanc/Bleu | Blanc/Bleu |
| 6 | Orange | Vert |
| 7 | Blanc/Brun | Blanc/Brun |
| 8 | Brun | Brun |

**Paires utilisées pour Ethernet (10/100 Mbps) :**
- **TX** (Transmission) : Broches 1, 2
- **RX** (Réception) : Broches 3, 6

**Gigabit Ethernet (1000BASE-T) :** Utilise les 4 paires

---

## 📊 Fibre optique

### Caractéristiques
- **Transmission** : Impulsions lumineuses
- **Immunité** : Aucune interférence EMI/RFI
- **Distance** : Plusieurs kilomètres
- **Bande passante** : Très élevée (10 Gbps, 100 Gbps, plus)
- **Coût** : Plus cher que le cuivre

### Types de fibre

| Type | Distance | Diamètre cœur | Usage | Connecteurs |
|------|----------|---------------|-------|-------------|
| **Monomode (SMF)** | Longue distance (plusieurs km) | 9 µm | WAN, datacenter, campus | LC, SC |
| **Multimode (MMF)** | Courte distance (jusqu'à 2 km) | 50 ou 62.5 µm | LAN, intra-bâtiment | LC, SC, ST |

### Connecteurs fibre
- **LC** (Lucent Connector) : Petit, moderne, duplex
- **SC** (Subscriber Connector) : Carré, poussoir
- **ST** (Straight Tip) : Baïonnette, ancien

---

## 📊 Transmission sans fil

### Caractéristiques
- **Transmission** : Ondes radio (Wi-Fi, Bluetooth, cellulaire)
- **Avantages** : Mobilité, pas de câble
- **Inconvénients** : Sensible aux interférences, obstacles, portée limitée, sécurité

### Standards Wi-Fi (IEEE 802.11)

| Standard | Fréquence | Débit max | Portée |
|----------|-----------|-----------|--------|
| **802.11a** | 5 GHz | 54 Mbps | Courte |
| **802.11b** | 2.4 GHz | 11 Mbps | Moyenne |
| **802.11g** | 2.4 GHz | 54 Mbps | Moyenne |
| **802.11n** (Wi-Fi 4) | 2.4/5 GHz | 600 Mbps | Longue |
| **802.11ac** (Wi-Fi 5) | 5 GHz | 1+ Gbps | Longue |
| **802.11ax** (Wi-Fi 6) | 2.4/5 GHz | 9+ Gbps | Longue |

---

## 💡 À retenir absolument

✅ **Couche 1** = Transmission des bits (signaux physiques)  
✅ **Distance max UTP** : **100 mètres**  
✅ **Cat 5e** = 1 Gbps, **Cat 6/6a** = 10 Gbps  
✅ **Câble droit** = Connexions différentes (PC → Switch)  
✅ **Câble croisé** = Connexions identiques (PC → PC, Switch → Switch)  
✅ **UTP** = Le plus courant (économique, Ethernet)  
✅ **Fibre monomode** = Longue distance, **Multimode** = Courte distance  
✅ **Fibre optique** = Immunité EMI/RFI, grande bande passante  
✅ **EMI/RFI** = Interférences électromagnétiques/radio  
✅ **Diaphonie (Crosstalk)** = Interférence entre fils voisins  
✅ **T568A** et **T568B** = Standards de câblage RJ-45  
✅ **Auto-MDIX** = Détection automatique du type de câble (moderne)  
