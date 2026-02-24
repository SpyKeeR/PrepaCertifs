# Module 07 : Commutation Ethernet
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module couvre les trames Ethernet, les adresses MAC, le fonctionnement des commutateurs et les méthodes de transmission.

**Durée estimée :** 5-6 heures  
**Objectifs :** Comprendre Ethernet et la commutation de couche 2

---

## 7.1 Trames Ethernet

### Standard Ethernet (IEEE 802.3)

**Ethernet** est la technologie LAN la plus répandue :
- Standard IEEE 802.3
- Couche liaison de données (Couche 2)
- Évolutif : 10 Mbps → 100 Gbps et plus

**Variantes Ethernet :**
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

**Note :** Le format *XBASE-Y* signifie :
- **X** : Débit (10 = 10 Mbps, 100 = 100 Mbps, 1000 = 1 Gbps)
- **BASE** : Bande de base (opposed to broadband)
- **Y** : Type de média (T = Twisted pair, S = Short fiber, L = Long fiber)

### Structure de la trame Ethernet II

**Trame Ethernet (802.3) :**

```
┌──────────┬────────┬──────┬────────┬──────────────┬──────┐
│ Preamble │  SFD   │ Dest │ Source │     Data     │ FCS  │
│  7 bytes │ 1 byte │6 byte│ 6 byte │  46-1500 B   │4 byte│
└──────────┴────────┴──────┴────────┴──────────────┴──────┘
```

**Champs de la trame Ethernet :**

**1. Préambule (Preamble) - 7 octets**
- Synchronisation des horloges
- Pattern : `10101010` répété 7 fois
- Ne fait pas partie de la trame proprement dite

**2. SFD (Start Frame Delimiter) - 1 octet**
- Délimiteur de début de trame
- Pattern : `10101011`
- Indique que les champs de la trame suivent

**3. Adresse MAC de destination - 6 octets**
- Adresse MAC du destinataire
- Peut être unicast, multicast ou broadcast

**4. Adresse MAC source - 6 octets**
- Adresse MAC de l'émetteur
- Toujours une adresse unicast

**5. Type/Longueur (EtherType) - 2 octets**
- Indique le protocole de couche supérieure encapsulé
- Valeurs courantes :
  - `0x0800` : IPv4
  - `0x0806` : ARP
  - `0x86DD` : IPv6
  - `0x8100` : VLAN (802.1Q)

**6. Données (Data/Payload) - 46 à 1500 octets**
- Paquet de couche 3 (IP) encapsulé
- **Taille minimale : 46 octets** (padding ajouté si moins)
- **Taille maximale : 1500 octets** (MTU - Maximum Transmission Unit)

**7. FCS (Frame Check Sequence) - 4 octets**
- Détection d'erreurs (CRC-32)
- Calculé sur l'ensemble de la trame (sauf préambule et FCS lui-même)
- Si le FCS reçu ≠ FCS calculé → trame corrompue, jetée

**⚠️ Taille de trame Ethernet :**
- **Taille minimale** : 64 octets (sans préambule + SFD)
- **Taille maximale** : 1518 octets (sans préambule + SFD)
- **Jumbo frames** : Jusqu'à 9000 octets (non standard, utilisé en datacenter)

**Calcul de la taille minimale :**
```
En-tête Ethernet : 14 octets (6 + 6 + 2)
Données minimum : 46 octets
FCS : 4 octets
Total : 64 octets
```

Si les données sont < 46 octets, du **padding** (remplissage de zéros) est ajouté.

---

## 7.2 Adresse MAC Ethernet

### Format de l'adresse MAC

**Adresse MAC (Media Access Control) :**
- **Taille** : 48 bits (6 octets)
- **Format** : Hexadécimal
- **Notation** : XX:XX:XX:XX:XX:XX ou XX-XX-XX-XX-XX-XX
- **Exemple** : `00:1A:2B:3C:4D:5E`

**Structure :**
```
┌─────────────────────┬──────────────────────┐
│   OUI (24 bits)     │  Device ID (24 bits) │
│  00:1A:2B           │     3C:4D:5E         │
└─────────────────────┴──────────────────────┘
```

**OUI (Organizationally Unique Identifier) :**
- 3 premiers octets (24 bits)
- Identifie le fabricant
- Attribué par IEEE
- Exemples :
  - `00:1A:2B` : Cisco (certains modèles)
  - `00:50:56` : VMware
  - `08:00:27` : VirtualBox

**Device ID (ou Serial Number) :**
- 3 derniers octets (24 bits)
- Numéro unique attribué par le fabricant
- Garantit l'unicité de l'adresse MAC

### Types d'adresses MAC

**1. Unicast (communication un-à-un)**
- Bit de poids faible du premier octet = 0
- Exemple : `00:1A:2B:3C:4D:5E`
- Le bit de diffusion (U/L bit) est à 0

**2. Broadcast (communication un-vers-tous)**
- Adresse spéciale : `FF:FF:FF:FF:FF:FF`
- Tous les bits à 1
- Tous les périphériques du réseau local reçoivent et traitent
- Exemples d'usage :
  - Requêtes ARP
  - DHCP Discover
  - Wake-on-LAN

**3. Multicast (communication un-vers-groupe)**
- Bit de poids faible du premier octet = 1
- Seuls les périphériques abonnés au groupe traitent

**⚠️ IMPORTANT - Adresses MAC de multidiffusion :**

**Pour IPv4 multicast :**
- **Format** : `01:00:5E:xx:xx:xx`
- Les 3 premiers octets sont **01:00:5E**
- Les 23 bits restants correspondent aux 23 bits de poids faible de l'adresse IPv4 multicast
- **Exemple** : 
  - Adresse IP multicast : 224.0.0.10 (EIGRP)
  - Adresse MAC multicast : `01:00:5E:00:00:0A`
- **Plage IPv4 multicast** : 224.0.0.0 à 239.255.255.255
- Protocoles utilisant multicast : OSPF, EIGRP, PIM, streaming vidéo

**Pour IPv6 multicast :**
- **Format** : `33:33:xx:xx:xx:xx`
- Les 2 premiers octets sont **33:33**
- Les 32 bits restants correspondent aux 32 bits de poids faible de l'adresse IPv6 multicast
- **Exemple** :
  - Adresse IPv6 multicast : FF02::1 (tous les nœuds)
  - Adresse MAC multicast : `33:33:00:00:00:01`
- **Plage IPv6 multicast** : FF00::/8
- Protocoles utilisant multicast : OSPFv3, RIPng, NDP (Neighbor Discovery Protocol)

**Résumé des formats multicast :**
| Protocole | Format MAC Multicast | Exemple |
|-----------|----------------------|---------|
| **IPv4** | **01:00:5E:--:--:--** | 01:00:5E:00:00:0A (224.0.0.10) |
| **IPv6** | **33:33:--:--:--:--** | 33:33:00:00:00:01 (FF02::1) |

### Bit I/G et U/L

**Structure du premier octet (bits de contrôle) :**
```
┌───┬───┬───┬───┬───┬───┬───┬───┐
│ 7 │ 6 │ 5 │ 4 │ 3 │ 2 │ 1 │ 0 │
│ U │ I │               │ G │   │
│ / │ / │               │   │   │
│ L │ G │               │   │   │
└───┴───┴───┴───┴───┴───┴───┴───┘
```

**Bit 0 (I/G - Individual/Group) :**
- **0** : Unicast (adresse individuelle)
- **1** : Multicast/Broadcast (adresse de groupe)

**Bit 1 (U/L - Universal/Local) :**
- **0** : Adresse universelle (OUI enregistré)
- **1** : Adresse localement administrée

**Exemples :**
- `00:1A:2B:3C:4D:5E` : 00 (hex) = 00000000 (bin) → Unicast, Universelle
- `01:00:5E:00:00:0A` : 01 (hex) = 00000001 (bin) → Multicast IPv4
- `33:33:00:00:00:01` : 33 (hex) = 00110011 (bin) → Multicast IPv6
- `FF:FF:FF:FF:FF:FF` : FF (hex) = 11111111 (bin) → Broadcast

---

## 7.3 La table d'adresses MAC

### Fonctionnement du commutateur (Switch)

Un **commutateur** (switch) de couche 2 :
- Maintient une **table d'adresses MAC** (CAM table)
- Associe chaque adresse MAC à un port
- Prend des décisions de transfert intelligentes

**Processus d'apprentissage et de transfert :**

**1. Apprentissage (Learning)**
- Le switch reçoit une trame
- Il examine l'**adresse MAC source**
- Il enregistre : "MAC source se trouve sur ce port"
- Entrée ajoutée dans la table avec un timer (généralement 300 secondes)

**2. Transfert (Forwarding)**
- Le switch examine l'**adresse MAC de destination**
- **Trois scénarios possibles :**

**Scénario A : Adresse MAC connue (Unicast)**
```
MAC de destination trouvée dans la table
→ Switch transmet UNIQUEMENT sur le port associé
```
**Avantage :** Pas de trafic inutile sur les autres ports

**Scénario B : Adresse MAC inconnue (Unknown Unicast)**
```
MAC de destination NOT trouvée dans la table
→ Switch transmet sur TOUS les ports (sauf le port source)
→ Appelé "flooding"
```

**Scénario C : Broadcast ou Multicast**
```
MAC de destination = FF:FF:FF:FF:FF:FF (broadcast)
ou
MAC de destination = 01:00:5E:xx:xx:xx (multicast IPv4)
ou
MAC de destination = 33:33:xx:xx:xx:xx (multicast IPv6)
→ Switch transmet sur TOUS les ports (sauf le port source)
```

**3. Filtrage (Filtering)**
- Si MAC source et MAC destination sont sur le même port
- La trame est **ignorée** (pas d'acheminement nécessaire)

**4. Vieillissement (Aging)**
- Les entrées de la table MAC ont un timer (300 secondes par défaut)
- Si aucune trame avec cette MAC source n'est reçue avant expiration
- L'entrée est supprimée de la table
- **Raison** : Les périphériques peuvent se déplacer de port ou être retirés du réseau

### Table d'adresses MAC - Exemple

**Topologie :**
```
PC1 (00:AA) ──┐
PC2 (00:BB) ──┤
              │
           [Switch]
              │
PC3 (00:CC) ──┤
PC4 (00:DD) ──┘
```

**Étapes :**
1. **PC1 (00:AA) envoie à PC3 (00:CC)**
   - Switch apprend : 00:AA sur port 1
   - MAC destination 00:CC inconnue → **flooding** (envoi sur ports 2, 3, 4)

2. **PC3 (00:CC) répond à PC1 (00:AA)**
   - Switch apprend : 00:CC sur port 3
   - MAC destination 00:AA connue (port 1) → **forwarding** uniquement sur port 1

3. **Table MAC après ces échanges :**
   ```
   MAC Address    Port
   00:AA          1
   00:CC          3
   ```

4. **PC2 (00:BB) envoie un broadcast**
   - Switch apprend : 00:BB sur port 2
   - Broadcast → envoi sur tous les ports (1, 3, 4)

**Table MAC finale :**
```
MAC Address    Port    Age (seconds)
00:AA          1       120
00:BB          2       45
00:CC          3       120
00:DD          4       200
```

### Commandes IOS - Table MAC

```cisco
Switch# show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  1     0011.2233.4455    DYNAMIC     Fa0/1
  1     0022.3344.5566    DYNAMIC     Fa0/2
  1     0033.4455.6677    DYNAMIC     Fa0/5
Total Mac Addresses for this criterion: 3
```

**Options de la commande :**
```cisco
show mac address-table                 # Toutes les entrées
show mac address-table dynamic         # Seulement les entrées dynamiques
show mac address-table static          # Seulement les entrées statiques
show mac address-table interface fa0/1 # Entrées sur un port spécifique
show mac address-table address 0011.2233.4455  # Recherche d'une MAC
```

**Effacer la table MAC :**
```cisco
Switch# clear mac address-table dynamic  # Effacer toutes les entrées dynamiques
Switch# clear mac address-table dynamic interface fa0/1  # Sur un port
```

---

## 7.4 Méthodes de transmission et vitesses de commutation

### Méthodes de commutation

**1. Store-and-Forward (Stocker et transmettre)**
- Le switch reçoit la **trame complète**
- Calcule et vérifie le **FCS** (détection d'erreurs)
- Si FCS OK : transfert de la trame
- Si FCS incorrect : trame jetée
- **Avantages** :
  - Détection d'erreurs
  - Supporte différentes vitesses sur les ports (buffering)
- **Inconvénient** : Latence plus élevée
- **Usage** : Switches modernes par défaut

**2. Cut-Through (Commutation à la volée)**
- Le switch lit **seulement l'adresse MAC de destination** (6 premiers octets après préambule)
- Commence à transférer la trame **avant de la recevoir complètement**
- **Ne vérifie PAS le FCS**
- **Avantages** :
  - Très faible latence
- **Inconvénients** :
  - Transfère les trames corrompues
  - Ne supporte pas les différentes vitesses (même vitesse requise)
- **Variants** :
  - **Fast-Forward** : Transfert dès lecture de l'adresse de destination
  - **Fragment-Free** : Lit les 64 premiers octets (évite les runts) puis transfert

**Comparaison :**
| Méthode | Latence | Détection erreurs | Buffering | Usage |
|---------|---------|-------------------|-----------|-------|
| **Store-and-Forward** | Plus élevée | Oui (FCS) | Oui | Par défaut, recommandé |
| **Cut-Through** | Très faible | Non | Non | Datacenters haute performance |

### Modes duplex

**1. Half-Duplex (Semi-duplex)**
- Communication bidirectionnelle, mais pas simultanée
- Un seul périphérique peut émettre à la fois
- **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) requis
- Les collisions sont possibles
- **Usage** : Hubs (obsolètes), Wi-Fi

**2. Full-Duplex (Duplex intégral)**
- Communication bidirectionnelle **simultanée**
- Émission et réception en même temps
- **Pas de collisions**
- Désactive CSMA/CD
- **Bande passante effective doublée** (1 Gbps émission + 1 Gbps réception = 2 Gbps agrégé)
- **Usage** : Tous les switches modernes

**⚠️ Configuration duplex :**
- **Auto-négociation** : Recommandée (par défaut)
- **Mismatch duplex** : Un côté en full, l'autre en half → Collisions, performances dégradées
- Toujours vérifier que les deux côtés négocient correctement

**Commandes IOS :**
```cisco
Switch(config)# interface gi0/1
Switch(config-if)# duplex auto             # Auto-négociation (recommandé)
Switch(config-if)# duplex full             # Forcer full-duplex
Switch(config-if)# speed auto              # Auto-négociation vitesse
Switch(config-if)# speed 1000              # Forcer 1 Gbps

Switch# show interfaces gi0/1 status       # Voir vitesse et duplex
```

### Auto-MDIX

**MDIX (Medium Dependent Interface Crossover) :**
- Détection automatique du type de câble (droit ou croisé)
- Ajuste automatiquement les paires TX/RX
- Permet d'utiliser **n'importe quel type de câble**
- **Activé par défaut** sur les switches modernes

**Commande :**
```cisco
Switch(config-if)# mdix auto               # Activer Auto-MDIX (par défaut)
```

---

## 💡 Points clés à retenir

1. **Trame Ethernet** : 
   - Taille : 64 à 1518 octets (sans préambule)
   - Champs : Préambule, SFD, MAC dest, MAC source, Type, Données (46-1500), FCS
2. **Adresse MAC** : 48 bits (6 octets) en hexadécimal, OUI (fabricant) + Device ID
3. **Types d'adresses** :
   - Unicast : Un-à-un
   - Broadcast : `FF:FF:FF:FF:FF:FF`
   - Multicast IPv4 : **01:00:5E:--:--:--**
   - Multicast IPv6 : **33:33:--:--:--:--**
4. **Table MAC** : Associe adresses MAC aux ports, learning/forwarding/aging
5. **Commutation** : Store-and-Forward (vérifie FCS), Cut-Through (faible latence)
6. **Duplex** : Half (collisions) vs Full (simultané, pas de collisions)

---

## 🔗 Commandes essentielles

```cisco
show mac address-table                 # Voir table MAC
show mac address-table interface gi0/1 # MAC sur un port
clear mac address-table dynamic        # Effacer table MAC

show interfaces gi0/1                  # Détails interface
show interfaces gi0/1 status           # État, vitesse, duplex
show interfaces gi0/1 switchport       # Infos switchport

interface gi0/1
  duplex auto                          # Auto-négociation duplex
  speed auto                           # Auto-négociation vitesse
  mdix auto                            # Auto-MDIX
```

---

## 📝 Exercices pratiques

1. **Identifier** les types d'adresses MAC :
   - `00:1A:2B:3C:4D:5E` : Unicast
   - `FF:FF:FF:FF:FF:FF` : Broadcast
   - `01:00:5E:00:00:0A` : Multicast IPv4
   - `33:33:00:00:00:01` : Multicast IPv6

2. **Packet Tracer** :
   - Observer le processus d'apprentissage de la table MAC
   - Mode simulation : voir flooding puis forwarding

3. **Calculer** la taille minimale de données si une trame fait 64 octets
   - En-tête : 14 octets
   - FCS : 4 octets
   - Données : 64 - 14 - 4 = 46 octets

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
