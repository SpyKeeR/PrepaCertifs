# Module 04 : Couche physique
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module couvre la couche physique du modèle OSI : transmission des bits, caractéristiques des médias, et types de câblage.

**Durée estimée :** 4-5 heures  
**Objectifs :** Comprendre la transmission physique des données

---

## 4.1 Rôle de la couche physique

### Fonction
- **Couche 1 du modèle OSI**
- Transport des **bits** (0 et 1) sur le média physique
- Conversion des trames (couche 2) en signaux
- Définit les spécifications électriques, mécaniques et procédurales

### Responsabilités
1. **Médias physiques** : Câbles, connecteurs
2. **Encodage** : Représentation des bits (tension, lumière, ondes)
3. **Signalisation** : Méthode de transmission
4. **Bande passante** : Capacité du média

---

## 4.2 Caractéristiques de la couche physique

### Standards de la couche physique
Définis par des organismes :
- **ISO** : Organisation internationale
- **IEEE** : Standards Ethernet, Wi-Fi
- **ANSI** : Standards américains
- **ITU** : Télécommunications
- **TIA/EIA** : Câblage réseau

### Composantes standards
1. **Composants physiques** : Cartes réseau, connecteurs, câbles
2. **Encodage** : Patterns de bits en signaux
3. **Signalisation** : Représente les 1 et 0 (tension haute/basse, lumière on/off)

### Bande passante
- **Définition** : Capacité de transport de données (débit)
- **Unités** : bps (bits par seconde), Kbps, Mbps, Gbps, Tbps
- **Facteurs influençant** :
  - Propriétés du média physique
  - Technologies d'encodage
  - Distance

**Débit vs Bande passante :**
- **Bande passante** : Capacité théorique maximale
- **Débit (Throughput)** : Bande passante réelle mesurée
- **Goodput** : Débit utile (sans overhead des en-têtes)

**Latence** : Délai de transmission de bout en bout

### Terminologie
- **Latence** : Temps total de transmission
- **Jitter** : Variation de la latence
- **Bande passante** : Capacité (Mbps, Gbps)
- **Débit** : Mesure effective
- **Goodput** : Données utiles reçues

---

## 4.3 Câblage en cuivre

### Caractéristiques
- **Transmission** : Impulsions électriques
- **Sensibilité** : Interférences électromagnétiques (EMI)
- **Atténuation** : Perte de signal sur la distance
- **Mesure** : Ohms (résistance)

### Types d'interférences

**1. EMI (Electromagnetic Interference)**
- Interférences électromagnétiques
- Sources : Moteurs, lumières fluorescentes, lignes électriques

**2. RFI (Radio Frequency Interference)**
- Interférences radio
- Sources : Émetteurs radio, micro-ondes

**3. Diaphonie (Crosstalk)**
- Interférence entre fils voisins dans un même câble
- Types :
  - **NEXT** (Near-End Crosstalk) : Diaphonie à l'extrémité proche
  - **FEXT** (Far-End Crosstalk) : Diaphonie à l'extrémité éloignée

**Protection** : Blindage, torsade des paires, respect des distances

### Types de câbles cuivre

**1. UTP (Unshielded Twisted Pair)**
- Paires de fils torsadés non blindés
- Le moins cher, le plus courant
- Catégories : Cat 5e (1 Gbps), Cat 6 (10 Gbps), Cat 6a, Cat 7

**2. STP (Shielded Twisted Pair)**
- Paires torsadées avec blindage
- Réduction des EMI/RFI
- Plus cher, nécessite mise à la terre

**3. Câble coaxial**
- Conducteur central + blindage
- Utilisé : Câble TV, Internet par câble
- Meilleure protection contre interférences que UTP
- Moins flexible

---

## 4.4 Câblage à paires torsadées non blindées (UTP)

### Standard UTP
- **Norme** : TIA/EIA-568
- **Connecteur** : RJ-45 (8 broches)
- **4 paires** de fils torsadés
- **Couleurs** : Orange, vert, bleu, brun (+ rayé de blanc)

### Catégories de câbles

| Catégorie | Bande passante | Application | Distance max |
|-----------|----------------|-------------|--------------|
| **Cat 3** | 10 Mbps | Téléphone, Ethernet 10BASE-T | 100 m |
| **Cat 5** | 100 Mbps | Ethernet 100BASE-TX (obsolète) | 100 m |
| **Cat 5e** | 1 Gbps | Ethernet 1000BASE-T | 100 m |
| **Cat 6** | 10 Gbps | Ethernet 10GBASE-T (jusqu'à 55 m) | 100 m (1G), 55 m (10G) |
| **Cat 6a** | 10 Gbps | Ethernet 10GBASE-T | 100 m |
| **Cat 7** | 10+ Gbps | Datacenters (blindé) | 100 m |

**⚠️ Distance maximale pour UTP : 100 mètres** (entre équipements actifs)

### Types de câbles Ethernet

**1. Câble droit (Straight-through)**
- **Utilisation** : Connexions différentes (PC vers switch, routeur vers switch)
- **Broches** : 1-1, 2-2, 3-3, 4-4, 5-5, 6-6, 7-7, 8-8 (identiques des deux côtés)
- **Standards** : T568A ou T568B (même standard aux deux extrémités)

**2. Câble croisé (Crossover)**
- **Utilisation** : Connexions identiques (PC vers PC, switch vers

 switch, routeur vers routeur)
- **Broches** : T568A d'un côté, T568B de l'autre
- **Croisement** : Paires TX et RX inversées
  - 1 ↔ 3
  - 2 ↔ 6

**3. Câble console (Rollover)**
- **Utilisation** : Connexion console d'administration (PC vers port console)
- **Broches** : Totalement inversées (1↔8, 2↔7, 3↔6, 4↔5)

**⚠️ Note :** Les équipements modernes ont **Auto-MDIX** : détection automatique du type de câble, donc câble droit fonctionne toujours.

### Standards de câblage

**T568A :**
| Broche | Couleur |
|--------|---------|
| 1 | Blanc/Vert |
| 2 | Vert |
| 3 | Blanc/Orange |
| 4 | Bleu |
| 5 | Blanc/Bleu |
| 6 | Orange |
| 7 | Blanc/Brun |
| 8 | Brun |

**T568B (plus courant) :**
| Broche | Couleur |
|--------|---------|
| 1 | Blanc/Orange |
| 2 | Orange |
| 3 | Blanc/Vert |
| 4 | Bleu |
| 5 | Blanc/Bleu |
| 6 | Vert |
| 7 | Blanc/Brun |
| 8 | Brun |

**Paires utilisées (Ethernet 100/1000BASE-T) :**
- **Broches 1-2** : Paire TX (Transmission)
- **Broches 3-6** : Paire RX (Réception)
- **Broches 4-5, 7-8** : Non utilisées en Fast Ethernet, utilisées en Gigabit Ethernet

---

## 4.5 Câblage à fibre optique

### Caractéristiques
- **Transmission** : Impulsions lumineuses (LED ou laser)
- **Avantages** :
  - **Bande passante très élevée** : 10/100 Gbps et plus
  - **Longue distance** : Plusieurs kilomètres sans répéteur
  - **Immunité aux EMI/RFI** : Pas d'interférence électromagnétique
  - **Sécurité** : Difficile à intercepter
- **Inconvénients** :
  - Plus coûteux (câble et connecteurs)
  - Installation plus complexe
  - Fragile (verre)

### Types de fibre optique

**1. Fibre monomode (SMF - Single-Mode Fiber)**
- **Caractéristiques** :
  - Cœur très fin (8-10 µm)
  - Un seul rayon lumineux (mode)
  - Laser comme source lumineuse
- **Usage** : Longue distance (jusqu'à 100 km et plus)
- **Applications** : WAN, liaisons inter-bâtiments, datacenter interconnects
- **Couleur de la gaine** : Jaune

**2. Fibre multimode (MMF - Multi-Mode Fiber)**
- **Caractéristiques** :
  - Cœur plus large (50-62.5 µm)
  - Plusieurs rayons lumineux (modes)
  - LED comme source lumineuse
- **Usage** : Courte distance (jusqu'à 2 km)
- **Applications** : LAN, campus, datacenters
- **Couleur de la gaine** : Orange (OM1/OM2) ou Aqua (OM3/OM4)

**Comparaison :**
| Type | Cœur | Distance | Coût | Source lumineuse | Couleur |
|------|------|----------|------|------------------|---------|
| **Monomode** | 8-10 µm | 100+ km | Élevé | Laser | Jaune |
| **Multimode** | 50-62.5 µm | < 2 km | Moyen | LED | Orange/Aqua |

### Connecteurs fibre optique

**Connecteurs courants :**
- **SC (Subscriber Connector)** : Connecteur carré, push-pull
- **LC (Lucent Connector)** : Petit format, latching
- **ST (Straight Tip)** : Connecteur à baïonnette (twist-lock)
- **FC** : Ferrule, vissé (moins courant aujourd'hui)

**Différence Duplex/Simplex :**
- **Simplex** : Une seule fibre (communication unidirectionnelle)
- **Duplex** : Deux fibres (bidirectionnelle full-duplex)

### Câbles patch fibre

**Types de patch cords :**
- **UPC (Ultra Physical Contact)** : Poli plat, retour de -50 dB
- **APC (Angled Physical Contact)** : Poli à 8°, retour de -60 dB, moins de réflexion (préféré)

---

## 4.6 Supports sans fil

### Caractéristiques
- **Transmission** : Ondes radio ou micro-ondes
- **Portée limitée** : Quelques mètres à plusieurs kilomètres
- **Partagé** : Tous les périphériques partagent le média (collision possible)
- **Sensible aux interférences** : Obstacles, autres signaux

### Types de sans fil

**1. Wi-Fi (802.11)**
- WLAN (Wireless LAN)
- Standards :
  - **802.11a** : 5 GHz, 54 Mbps
  - **802.11b** : 2.4 GHz, 11 Mbps
  - **802.11g** : 2.4 GHz, 54 Mbps
  - **802.11n** : 2.4/5 GHz, 600 Mbps
  - **802.11ac (Wi-Fi 5)** : 5 GHz, 1+ Gbps
  - **802.11ax (Wi-Fi 6)** : 2.4/5/6 GHz, 10+ Gbps
- Portée : 30-100 mètres (intérieur)

**2. Bluetooth**
- WPAN (Wireless Personal Area Network)
- Courte portée : 10-100 mètres
- Faible consommation
- Appareils : Casques, claviers, souris, wearables

**3. WiMAX**
- WMAN (Wireless Metropolitan Area Network)
- Longue portée : Plusieurs kilomètres
- Alternative au DSL/câble

**4. Cellulaire (3G/4G/5G)**
- WAN sans fil
- Couverture large zone
- Mobilité

### Limitations du sans fil

**1. Zone de couverture limitée**
- Affaibli par les obstacles (murs, meubles)
- Distance dépend de la puissance

**2. Interférences**
- Autres Wi-Fi, Bluetooth, micro-ondes
- Chevauchement de canaux

**3. Sécurité**
- Signal accessible à tous dans la portée
- Nécessite chiffrement (WPA2, WPA3)

**4. Média partagé**
- Partage de bande passante entre tous les clients
- Collisions possibles (CSMA/CA)

---

## 💡 Points clés à retenir

1. **Couche physique** : Transmission de bits sur le média
2. **Câble cuivre UTP** : Cat 5e (1 Gbps), Cat 6 (10 Gbps), longueur max 100 m
3. **Types de câbles** : Droit (dispositifs différents), croisé (dispositifs identiques), console
4. **Fibre optique** : Monomode (longue distance), multimode (courte distance)
5. **Sans fil** : Wi-Fi 802.11, Bluetooth, cellulaire
6. **Interférences** : EMI, RFI, diaphonie (cuivre) / Obstacles, autres signaux (sans fil)

---

## 🔗 Commandes

Aucune commande IOS spécifique (module théorique).

**Vérification des interfaces physiques :**
```cisco
show interfaces status                 # État des interfaces
show ip interface brief                # Résumé interfaces IP
```

---

## 📝 Exercices pratiques

1. **Identifier** quel type de câble utiliser pour :
   - PC vers Switch : Droit
   - Switch vers Switch : Croisé (ou droit si Auto-MDIX)
   - PC vers port console : Console (rollover)

2. **Packet Tracer** :
   - Créer une topologie et câbler correctement
   - Observer l'état des liens (vert = opérationnel)

3. **Calculer** le débit effectif (goodput) sachant :
   - Bande passante : 100 Mbps
   - Overhead : 20%
   - Goodput = 100 - 20% = 80 Mbps

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
