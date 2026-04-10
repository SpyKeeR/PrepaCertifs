# Module 2 : Spanning Tree Protocol (STP)
**CCNP ENCOR v8 - Protocole Spanning Tree**

---

## 📋 Vue d'ensemble du module

### Objectifs du module
Ce module couvre le protocole Spanning Tree (STP), mécanisme essentiel pour prévenir les boucles dans les réseaux commutés redondants. Vous apprendrez comment STP élimine les boucles tout en maintenant la redondance pour la haute disponibilité.

### Thèmes principaux
1. **Problèmes de redondance Layer 2**
   - Tempêtes de broadcast
   - Instabilité de la table MAC
   - Trames dupliquées

2. **Fonctionnement du Spanning Tree Protocol**
   - Élection du Root Bridge
   - Processus de sélection des ports
   - États des ports STP
   - Échange de BPDUs

3. **Variantes du Spanning Tree**
   - STP 802.1D (original)
   - PVST (Per-VLAN Spanning Tree)
   - PVST+ (Per-VLAN Spanning Tree Plus)
   - Rapid-PVST+ (introduction au module suivant)

---

## 🔄 Redondance Layer 2 : Nécessité et défis

### Pourquoi la redondance ?

**Objectif :** Éliminer les points de défaillance uniques (Single Points of Failure - SPOF)

**Avantages de la redondance :**
- ✅ **Haute disponibilité** : Le réseau reste opérationnel même si un lien ou un équipement tombe
- ✅ **Tolérance aux pannes** : Basculement automatique vers un chemin alternatif
- ✅ **Maintenance facilitée** : Possibilité d'effectuer des opérations sans interruption de service

**Architecture redondante typique :**
```
          [Core Switch 1]------[Core Switch 2]
                |      \      /      |
                |       \    /       |
                |        \  /        |
                |         \/         |
                |         /\         |
                |        /  \        |
                |       /    \       |
          [Distrib 1]--------[Distrib 2]
                |              |
             [Access]------[Access]
```

**💡 Point clé :** La redondance est essentielle dans les réseaux d'entreprise, mais crée des boucles au niveau Layer 2 qui doivent être contrôlées.

---

## ⚠️ Problèmes causés par les boucles Layer 2

### 1. Tempêtes de broadcast (Broadcast Storms)

**Scénario :**
```
    [SW1]-------[SW2]
      |           |
      +----[SW3]--+
```

Lorsqu'un broadcast est envoyé dans une topologie en boucle :

1. Le switch SW1 reçoit un broadcast d'un hôte
2. SW1 forward le broadcast sur tous ses ports (vers SW2 et SW3)
3. SW2 et SW3 reçoivent le broadcast et le forwardent
4. Chaque switch reforward indéfiniment les broadcasts reçus
5. Le trafic augmente de façon exponentielle

**Conséquences :**
- 🚫 Saturation de la bande passante
- 🚫 CPU des switches à 100%
- 🚫 CPU des hôtes surchargé par le traitement des broadcasts
- 🚫 Réseau complètement inutilisable en quelques secondes

### 2. Instabilité de la table MAC (MAC Flapping)

**Problème :** Les switches apprennent constamment la même adresse MAC sur différents ports.

**Scénario :**
```
PC-A (MAC: aaaa.aaaa.aaaa) connecté à SW1

Trame de PC-A arrive à SW2:
- Via SW1 directement    → SW2 apprend MAC sur port 1
- Via SW1 → SW3 → SW2    → SW2 apprend MAC sur port 2
- Via SW1 → SW2          → SW2 apprend MAC sur port 1
(boucle infinie)
```

**Conséquences :**
- 🚫 Table MAC jamais stable
- 🚫 Mauvaise décision de forwarding
- 🚫 CPU du switch surchargé par les mises à jour constantes
- 🚫 Trames envoyées vers le mauvais port

### 3. Trames dupliquées (Duplicate Frames)

**Problème :** Les trames unicast peuvent être reçues plusieurs fois par la destination.

**Scénario :**
```
PC-A envoie une trame unicast à PC-B

Chemins possibles:
- PC-A → SW1 → SW2 → PC-B
- PC-A → SW1 → SW3 → SW2 → PC-B

PC-B reçoit la même trame deux fois (ou plus)
```

**Conséquences :**
- 🚫 Protocoles de couche supérieure perturbés
- 🚫 Connexions TCP réinitialisées
- 🚫 Corruption potentielle des données
- 🚫 Comportement applicatif imprévisible

**💡 Point clé :** Sans mécanisme de prévention, la redondance Layer 2 crée des boucles qui rendent le réseau complètement inutilisable. C'est là qu'intervient le Spanning Tree Protocol.

---

## 🌳 Spanning Tree Protocol (STP) - Concepts fondamentaux

### Présentation du STP

**Standard :** IEEE 802.1D (original, publié en 1990)

**Objectif :** Créer une topologie logique sans boucle dans un réseau physiquement redondant.

**Principe de fonctionnement :**
- STP identifie tous les liens du réseau
- Il **bloque stratégiquement** certains ports pour éliminer les boucles
- Il maintient les ports bloqués en **standby** pour une activation rapide en cas de panne
- Il crée un arbre couvrant (spanning tree) à partir d'un switch racine

**Analogie :**
```
Topologie physique (avec boucles):      Spanning Tree (sans boucle):
    [SW1]-------[SW2]                        [SW1]-------[SW2]
      |           |                            |           
      +----[SW3]--+                            +----[SW3]--X
                                                           (bloqué)
```

### Algorithme STA (Spanning Tree Algorithm)

**STA** est l'algorithme utilisé par STP pour déterminer quels ports bloquer.

**Processus en 4 étapes :**

#### Étape 1 : Élection du Root Bridge
- Un switch est élu comme **pont racine** (root bridge)
- Le root bridge est le point de référence de tout le spanning tree
- **Critère d'élection :** Switch avec le **Bridge ID le plus bas**

#### Étape 2 : Sélection des Root Ports
- Sur tous les switches **non-root**, sélectionner le **Root Port (RP)**
- Le Root Port est le port avec le **meilleur chemin** vers le root bridge
- **Critère :** Coût cumulé le plus bas vers le root

#### Étape 3 : Sélection des Designated Ports
- Pour chaque **segment** (lien), élire un **Designated Port (DP)**
- Le DP est le port qui envoie les BPDUs sur ce segment
- **Critère :** Switch avec le meilleur chemin vers le root

#### Étape 4 : Blocage des ports non-Designated
- Tous les ports qui ne sont **ni Root Port ni Designated Port** sont **bloqués**
- Ces ports sont appelés **Alternate Ports** ou **Blocked Ports**
- Ils ne forwardent pas de trafic mais écoutent les BPDUs

**💡 Point clé :** L'algorithme STA garantit qu'il n'y a qu'un seul chemin actif entre deux switches, éliminant ainsi toutes les boucles.

---

## 🔧 Bridge ID (BID) - Identifiant du pont

### Structure du Bridge ID

Le **Bridge ID** est l'identifiant unique de chaque switch dans le domaine STP.

**Composition (8 octets / 64 bits) :**

| Bridge Priority | Extended System ID | MAC Address |
|----------------|--------------------|-------------|
| 4 bits | 12 bits | 48 bits |

**Format classique (802.1D original) :**
```
┌────────────────┬──────────────────────────────┐
│ Bridge Priority│       MAC Address            │
│   (16 bits)    │         (48 bits)            │
│   0-65535      │     XX:XX:XX:XX:XX:XX        │
└────────────────┴──────────────────────────────┘
         Bridge ID (64 bits)
```

**Format étendu (PVST+ et 802.1t) :**
```
┌─────────┬──────────────┬──────────────────────────────┐
│Priority │ Extended     │       MAC Address            │
│ (4 bits)│ System ID    │         (48 bits)            │
│ 0-15    │ (12 bits)    │     XX:XX:XX:XX:XX:XX        │
│ *4096   │ VLAN ID      │                              │
└─────────┴──────────────┴──────────────────────────────┘
         Bridge ID (64 bits)
```

### Bridge Priority

**Valeurs par défaut :**
- **STP 802.1D :** 32768
- **PVST+ :** 32768 + VLAN ID

**Valeurs configurables :**
- **Plage complète :** 0 à 65535
- **Incréments :** Multiples de 4096 (0, 4096, 8192, 16384, 24576, 32768, 40960, 49152, 57344, 61440)
- **Raison :** Les 4 bits de poids fort (valeurs 0-15) sont multipliés par 4096

**Exemple de calcul du Bridge ID (PVST+) :**
```
VLAN 10, Priority 32768:
- Priority de base : 32768
- Extended System ID : 10
- Bridge Priority effective : 32768 + 10 = 32778
- MAC Address : 0c:e3:e1:1a:ba:00

Bridge ID complet : 32778.0ce3.e11a.ba00
```

**💡 Point clé :** Plus le Bridge ID est **bas**, plus le switch a de chances d'être élu Root Bridge.

---

## 🏆 Élection du Root Bridge

### Processus d'élection

**Principe :** Le switch avec le **Bridge ID le plus bas** devient le Root Bridge.

**Étapes :**
1. Au démarrage, **chaque switch** s'assume comme Root Bridge
2. Les switches échangent des **BPDUs** (Bridge Protocol Data Units)
3. Chaque switch compare son Bridge ID avec celui reçu dans les BPDUs
4. Le switch avec le plus petit BID est progressivement reconnu comme Root
5. L'élection converge lorsque tous les switches s'accordent sur le même Root

**Critères de comparaison (ordre de priorité) :**

| Critère | Préférence |
|---------|-----------|
| 1. Bridge Priority | Plus bas |
| 2. MAC Address | Plus basse |

**Exemple d'élection :**
```
SW1: Priority 32768, MAC 0000.0c11.1111  → BID = 32768.0000.0c11.1111
SW2: Priority 32768, MAC 0000.0c22.2222  → BID = 32768.0000.0c22.2222
SW3: Priority 24576, MAC 0000.0c33.3333  → BID = 24576.0000.0c33.3333

Résultat: SW3 devient Root Bridge (plus petit BID)
```

### Configuration manuelle du Root Bridge

**Méthode 1 : Définir manuellement la priorité**
```cisco
SW3(config)# spanning-tree vlan 10 priority 4096
```

**Méthode 2 : Utiliser la commande root (Cisco)**
```cisco
! Devenir root primary (Priority = 24576 ou plus bas que le root actuel)
SW3(config)# spanning-tree vlan 10 root primary

! Devenir root secondary (Priority = 28672)
SW3(config)# spanning-tree vlan 10 root secondary
```

**💡 Point clé :** Toujours configurer manuellement le Root Bridge dans un réseau de production pour contrôler la topologie STP. Sinon, un switch ajouté avec une MAC basse pourrait devenir Root par accident.

---

## 📤 BPDUs (Bridge Protocol Data Units)

### Rôle des BPDUs

Les **BPDUs** sont des trames spéciales échangées entre switches pour :
- Élire le Root Bridge
- Identifier les meilleurs chemins
- Détecter les changements de topologie
- Maintenir l'état du spanning tree

### Types de BPDUs

#### 1. Configuration BPDU
- **Usage :** Élection du Root, calcul du spanning tree
- **Fréquence :** Envoyé toutes les 2 secondes (Hello Time) par le Root Bridge
- **Propagation :** Relayé par tous les switches sur leurs Designated Ports

#### 2. Topology Change Notification (TCN) BPDU
- **Usage :** Signaler un changement de topologie
- **Direction :** Envoyé vers le Root Bridge
- **Effet :** Réduit le timer d'expiration MAC pour réapprendre plus vite

### Contenu d'une Configuration BPDU

**Informations essentielles :**
```
┌────────────────────────────────┐
│ Root Bridge ID                 │  ← BID du Root Bridge
├────────────────────────────────┤
│ Root Path Cost                 │  ← Coût vers le Root depuis ce switch
├────────────────────────────────┤
│ Sender Bridge ID               │  ← BID du switch envoyeur
├────────────────────────────────┤
│ Sender Port ID                 │  ← Port d'envoi
├────────────────────────────────┤
│ Timers (Hello, MaxAge, Fwd Dly)│  ← Temporisations STP
└────────────────────────────────┘
```

**Champs détaillés :**
- **Protocol ID :** 0x0000 (STP)
- **Version :** 0x00 (802.1D)
- **BPDU Type :** 0x00 (Configuration BPDU)
- **Flags :** TC (Topology Change), TCA (TC Acknowledgment)
- **Root Bridge ID :** 8 octets
- **Root Path Cost :** 4 octets
- **Bridge ID :** 8 octets (du switch envoyeur)
- **Port ID :** 2 octets
- **Message Age :** Âge du BPDU
- **Max Age :** 20 secondes (timer max pour la perte du Root)
- **Hello Time :** 2 secondes (intervalle d'envoi)
- **Forward Delay :** 15 secondes (durée des états Listening/Learning)

### Flux des BPDUs

**Fonctionnement normal :**
```
[Root Bridge] --BPDU--> [Switch A] --BPDU--> [Switch B]
     (génère)            (relaie)             (relaie)

- Seul le Root GÉNÈRE les Configuration BPDUs originaux
- Les autres switches RELAIENT les BPDUs sur leurs Designated Ports
- Les switches comparent les BPDUs reçus avec leurs informations locales
```

**💡 Point clé :** Les BPDUs sont échangés en permanence (toutes les 2 secondes). Si un switch ne reçoit plus de BPDUs du Root pendant 20 secondes (Max Age), il considère le Root comme perdu et redémarre le processus d'élection.

---

## 💰 Path Cost - Coût du chemin

### Concept du Path Cost

Le **Path Cost** est la métrique utilisée par STP pour déterminer le meilleur chemin vers le Root Bridge.

**Règle de base :**
- Le coût **augmente** dans la direction **vers les switches périphériques**
- Le coût **s'additionne** au fur et à mesure qu'on s'éloigne du Root
- Le Root Bridge a un coût de **0** vers lui-même

### Table des coûts STP

**Coûts par vitesse de lien (802.1D original - short path cost) :**

| Vitesse du lien | Coût 802.1D (16 bits) |
|-----------------|----------------------|
| 10 Mbps (Ethernet) | 100 |
| 100 Mbps (Fast Ethernet) | 19 |
| 1 Gbps (Gigabit Ethernet) | 4 |
| 10 Gbps | 2 |

**Coûts révisés (802.1t / 802.1w - long path cost) :**

| Vitesse du lien | Coût 802.1t (32 bits) | Usage |
|-----------------|----------------------|-------|
| 10 Mbps | 2,000,000 | Legacy |
| 100 Mbps | 200,000 | Legacy |
| 1 Gbps | 20,000 | Courant |
| 10 Gbps | 2,000 | Courant |
| 100 Gbps | 200 | Data Center |
| 1 Tbps | 20 | Futur |

**💡 Point clé :** Les équipements Cisco utilisent par défaut les coûts "short" (802.1D) pour la compatibilité, mais recommandent les coûts "long" pour les réseaux modernes avec des liens 10G+.

### Calcul du Root Path Cost

**Définition :** Somme des coûts de tous les liens sur le chemin depuis le switch jusqu'au Root Bridge.

**Exemple de calcul :**
```
                    [Root Bridge]
                         |
                     Cost = 0
                         |
                    1 Gbps (cost 4)
                         |
                      [SW1]
                         |
                  Root Path Cost = 4
                         |
                    1 Gbps (cost 4)
                         |
                      [SW2]
                         |
                  Root Path Cost = 8
```

**Calcul depuis SW2 :**
- Coût du lien SW1-Root : 4
- Coût du lien SW2-SW1 : 4
- **Root Path Cost total de SW2 : 4 + 4 = 8**

### Configuration manuelle du coût

**Modifier le coût d'une interface :**
```cisco
interface GigabitEthernet0/1
 spanning-tree cost 10
exit
```

**Modifier le mode de calcul du coût (court vs long) :**
```cisco
! Mode court (16 bits, 802.1D)
spanning-tree pathcost method short

! Mode long (32 bits, 802.1w)
spanning-tree pathcost method long
```

**💡 Point clé :** Le Root Path Cost est cumulé en **entrant** sur chaque switch. Un switch ajoute le coût du port sur lequel il reçoit le BPDU.

---

## 🔌 Rôles des ports dans STP

STP assigne un **rôle** à chaque port selon sa position dans le spanning tree.

### 1. Root Port (RP)

**Définition :** Port qui offre le **meilleur chemin** (coût le plus bas) vers le Root Bridge.

**Caractéristiques :**
- ✅ Un seul Root Port par switch (sauf sur le Root Bridge lui-même)
- ✅ État : **Forwarding** (transmet le trafic)
- ✅ Reçoit les BPDUs du Root Bridge

**Critères de sélection (ordre de priorité) :**

| Critère | Préférence |
|---------|-----------|
| 1. Root Path Cost | Plus bas |
| 2. Sender Bridge ID | Plus bas |
| 3. Sender Port ID | Plus bas |
| 4. Local Port ID | Plus bas |

**Exemple :**
```
          [Root Bridge]
           /         \
      Cost 4       Cost 19
         /             \
      [SW1]          [SW1]
       Gi0/1          Fa0/1
         RP           
(Root Port sur Gi0/1, coût plus bas)
```

### 2. Designated Port (DP)

**Définition :** Port qui envoie les BPDUs sur un segment et assure le forwarding sur ce segment.

**Caractéristiques :**
- ✅ Un Designated Port **par segment** (lien)
- ✅ État : **Forwarding**
- ✅ Envoie les BPDUs vers les switches en aval
- ✅ Tous les ports du Root Bridge sont Designated Ports

**Rôle :**
- Assurer la communication sur le segment
- Relayer les BPDUs vers les switches non-root

**Exemple :**
```
[Root Bridge]
 DP    DP
  |    |
Tous les ports du Root sont DP
```

### 3. Alternate Port / Blocked Port (BP)

**Définition :** Port qui n'est **ni Root Port ni Designated Port** — il est bloqué pour éviter les boucles.

**Caractéristiques :**
- ✅ État : **Blocking** (802.1D) ou **Discarding** (802.1w)
- ✅ Ne forwarde pas de trafic
- ✅ Écoute les BPDUs (pour détecter les changements)
- ✅ Peut devenir actif si le Root Port ou Designated Port tombe

**Rôle :**
- Prévenir les boucles
- Fournir de la redondance (chemin de secours)

**Exemple :**
```
    [Root]
     /  \
    /    \
  DP      DP
  /        \
[SW1]-----[SW2]
 DP        BP
     (lien bloqué pour éviter la boucle)
```

**💡 Point clé :** Le rôle de chaque port (Root, Designated, Blocked) est déterminé par l'algorithme STA pour garantir une topologie sans boucle.

---

## 🔄 États des ports STP (802.1D)

STP fait transitionner les ports à travers plusieurs **états** pour assurer une convergence sûre sans créer de boucles temporaires.

### Les 5 états STP

| État | Description | Durée | Trafic | BPDUs | Apprentissage MAC |
|------|-------------|-------|--------|-------|-------------------|
| **Disabled** | Port administrativement éteint | N/A | ❌ | ❌ | ❌ |
| **Blocking** | Port bloqué, écoute les BPDUs | 20 sec (Max Age) | ❌ | ✅ Reçoit | ❌ |
| **Listening** | Participe à l'élection STP | 15 sec (Fwd Delay) | ❌ | ✅ Envoie/Reçoit | ❌ |
| **Learning** | Apprend les adresses MAC | 15 sec (Fwd Delay) | ❌ | ✅ Envoie/Reçoit | ✅ |
| **Forwarding** | État opérationnel normal | Permanent | ✅ | ✅ Envoie/Reçoit | ✅ |

### Diagramme de transition d'états

```
   DISABLED
      |
      | (port activé)
      v
   BLOCKING ←──────┐
      |            │
      | (port sélectionné comme RP ou DP)
      |            │
      v            │
   LISTENING       │
      |            │
      | (15 sec)   │
      |            │
      v            │
   LEARNING        │
      |            │
      | (15 sec)   │
      |            │
      v            │
   FORWARDING      │
                   │
   (changement de topologie ou perte du lien)
                   │
                   └─────────────┘
```

### Détails des états

#### 1. Disabled
- **Cause :** Commande `shutdown` ou port défectueux
- **Comportement :** Le port n'envoie ni ne reçoit aucun trafic ni BPDU

#### 2. Blocking
- **Durée :** Jusqu'à 20 secondes (Max Age timer)
- **Rôle :** Écouter pour détecter si le port devrait devenir actif
- **Comportement :**
  - ❌ Ne forwarde pas de trames
  - ❌ N'apprend pas d'adresses MAC
  - ✅ Reçoit et traite les BPDUs
- **Transition :** Si le port doit devenir Root Port ou Designated Port → passe à Listening

#### 3. Listening
- **Durée :** 15 secondes (Forward Delay)
- **Rôle :** Participer activement à la détermination de la topologie STP
- **Comportement :**
  - ❌ Ne forwarde pas de trames
  - ❌ N'apprend pas d'adresses MAC
  - ✅ Envoie et reçoit des BPDUs
  - ✅ Participe à l'élection du Root et au calcul du spanning tree

#### 4. Learning
- **Durée :** 15 secondes (Forward Delay)
- **Rôle :** Préparer le port au forwarding en apprenant les MACs
- **Comportement :**
  - ❌ Ne forwarde pas de trames
  - ✅ Apprend les adresses MAC
  - ✅ Envoie et reçoit des BPDUs

#### 5. Forwarding
- **Durée :** Indéfinie (jusqu'à un changement de topologie)
- **Rôle :** État opérationnel normal
- **Comportement :**
  - ✅ Forwarde les trames
  - ✅ Apprend les adresses MAC
  - ✅ Envoie et reçoit des BPDUs

**💡 Point clé :** La transition complète de Blocking à Forwarding prend **30 à 50 secondes** (15s Listening + 15s Learning). C'est le temps de convergence du STP 802.1D, amélioration majeure dans le RSTP (Rapid STP).

---

## ⏱️ Timers STP

STP utilise trois timers principaux pour gérer la convergence et la détection de pannes.

### Les 3 timers STP

| Timer | Valeur par défaut | Plage configurable | Rôle |
|-------|-------------------|-------------------|------|
| **Hello Time** | 2 secondes | 1-10 sec | Fréquence d'envoi des BPDUs |
| **Forward Delay** | 15 secondes | 4-30 sec | Durée des états Listening/Learning |
| **Max Age** | 20 secondes | 6-40 sec | Temps avant de considérer un BPDU trop vieux |

### 1. Hello Time

**Fonction :** Intervalle entre les envois de BPDUs par le Root Bridge.

**Valeur par défaut :** 2 secondes

**Impact :**
- Plus court → Détection plus rapide des changements, mais plus de trafic de contrôle
- Plus long → Moins de trafic, mais détection plus lente

**Configuration :**
```cisco
spanning-tree vlan 10 hello-time 3
```

### 2. Forward Delay

**Fonction :** Durée de chaque état transitoire (Listening et Learning).

**Valeur par défaut :** 15 secondes

**Calcul de convergence :**
```
Temps total = Listening (15s) + Learning (15s) = 30 secondes
```

**Impact :**
- Plus court → Convergence plus rapide, mais risque de boucles temporaires
- Plus long → Convergence plus sûre, mais interruption de service plus longue

**Configuration :**
```cisco
spanning-tree vlan 10 forward-time 20
```

### 3. Max Age

**Fonction :** Durée maximale pendant laquelle un BPDU est considéré valide.

**Valeur par défaut :** 20 secondes

**Comportement :**
- Chaque switch incrémente le champ "Message Age" dans les BPDUs qu'il relaie
- Si Message Age atteint Max Age, le BPDU est rejeté
- Si aucun BPDU n'est reçu pendant Max Age, le switch considère que le Root est perdu

**Impact :**
- Plus court → Détection plus rapide des pannes, mais risque de faux positifs
- Plus long → Réseau plus stable, mais basculement plus lent

**Configuration :**
```cisco
spanning-tree vlan 10 max-age 25
```

### Contraintes et relations entre les timers

**IEEE 802.1D impose des relations mathématiques :**

```
Max Age ≥ 2 × (Hello Time + 1)
Max Age ≤ 2 × (Forward Delay - 1)
```

**Exemple de vérification :**
```
Hello Time = 2s
Forward Delay = 15s
Max Age = 20s

Vérifications:
20 ≥ 2 × (2 + 1) = 6  ✅
20 ≤ 2 × (15 - 1) = 28 ✅
```

**💡 Point clé :** Seul le Root Bridge génère les timers STP. Tous les autres switches utilisent les timers reçus dans les BPDUs du Root. Si vous modifiez les timers, faites-le uniquement sur le Root Bridge.

---

## 🔧 Configuration de base STP

### Vérifier l'état actuel de STP

**Afficher le spanning tree pour tous les VLANs :**
```cisco
SW1# show spanning-tree

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    24586 (priority 24576 sys-id-ext 10)
             Address     0ce3.e11a.ba00
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 4         128.1    P2p
Gi0/2               Desg FWD 4         128.2    P2p
```

**Afficher STP pour un VLAN spécifique :**
```cisco
SW1# show spanning-tree vlan 10
```

**Afficher un résumé compact :**
```cisco
SW1# show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0010, VLAN0020
Extended system ID           : enabled
Portfast Default             : disabled
PortFast BPDU Guard Default  : disabled
Portfast BPDU Filter Default : disabled
Loopguard Default            : disabled
EtherChannel misconfig guard : enabled
UplinkFast                   : disabled
BackboneFast                 : disabled
Configured Pathcost method used is short
```

**Afficher les détails d'une interface :**
```cisco
SW1# show spanning-tree interface GigabitEthernet0/1 detail
```

### Configuration du Root Bridge

**Méthode 1 : Priorité manuelle**
```cisco
! Définir la priorité à 24576 pour le VLAN 10
SW1(config)# spanning-tree vlan 10 priority 24576
```

**Méthode 2 : Commande root primary/secondary (Cisco)**
```cisco
! Configurer comme Root Primary
! (Priority = 24576, ou plus bas que le root actuel -4096)
SW1(config)# spanning-tree vlan 10 root primary

! Configurer comme Root Secondary
! (Priority = 28672)
SW2(config)# spanning-tree vlan 10 root secondary
```

**Méthode 3 : Root primary avec diameter**
```cisco
! Spécifier le diamètre du réseau (nombre de switches entre deux extrémités)
! Ajuste automatically les timers selon la taille du réseau
SW1(config)# spanning-tree vlan 10 root primary diameter 4
```

### Modifier les timers STP

**⚠️ Attention :** À configurer **uniquement sur le Root Bridge**.

```cisco
! Modifier le Hello Time (1-10 secondes)
SW1(config)# spanning-tree vlan 10 hello-time 3

! Modifier le Forward Delay (4-30 secondes)
SW1(config)# spanning-tree vlan 10 forward-time 20

! Modifier le Max Age (6-40 secondes)
SW1(config)# spanning-tree vlan 10 max-age 25
```

### Modifier le coût d'un port

```cisco
interface GigabitEthernet0/1
 ! Coût manuel (1-200000000)
 spanning-tree cost 10
 
 ! Coût par VLAN
 spanning-tree vlan 10 cost 15
exit
```

### Modifier la priorité d'un port

**Utilisé comme tie-breaker lors de la sélection du Root Port.**

```cisco
interface GigabitEthernet0/1
 ! Priorité (0-240, par incréments de 16)
 spanning-tree port-priority 64
 
 ! Priorité par VLAN
 spanning-tree vlan 10 port-priority 32
exit
```

**Port ID** = Priority (4 bits) + Numéro de port (12 bits)

Exemple : Priority 128 sur port Gi0/1 → Port ID = 128.1

### Activer/Désactiver STP

**Désactiver STP (⚠️ non recommandé sauf cas très spécifiques) :**
```cisco
! Désactiver pour un VLAN
SW1(config)# no spanning-tree vlan 10

! Désactiver globalement (dangereux!)
SW1(config)# no spanning-tree vlan 1-4094
```

**Réactiver STP :**
```cisco
SW1(config)# spanning-tree vlan 10
```

**💡 Point clé :** Dans un environnement de production, configurez toujours manuellement le Root Bridge Primary et Secondary pour contrôler la topologie. Ne laissez jamais l'élection se faire automatiquement basée uniquement sur les adresses MAC.

---

## 🌐 Variantes du Spanning Tree

### Comparaison des variantes STP

| Variante | Standard | Instances STP | Convergence | Description |
|----------|----------|---------------|-------------|-------------|
| **STP** | IEEE 802.1D | 1 (CST) | ~30-50s | Spanning Tree original, une instance pour tous les VLANs |
| **PVST** | Cisco proprietary | 1 par VLAN | ~30-50s | Per-VLAN STP, utilise ISL (obsolète) |
| **PVST+** | Cisco proprietary | 1 par VLAN | ~30-50s | PVST avec support 802.1Q, compatible avec CST |
| **RSTP** | IEEE 802.1w | 1 (CST) | ~1-2s | Rapid STP, convergence rapide |
| **Rapid PVST+** | Cisco proprietary | 1 par VLAN | ~1-2s | RSTP avec une instance par VLAN |
| **MSTP** | IEEE 802.1s | Multiple (MSTI) | ~1-2s | Multiple STP, regroupe plusieurs VLANs par instance |

### STP (802.1D) - Common Spanning Tree (CST)

**Caractéristiques :**
- ✅ Standard IEEE original (1990)
- ✅ Une seule instance STP pour tous les VLANs (CST - Common Spanning Tree)
- ❌ Convergence lente (30-50s)
- ❌ Pas d'optimisation par VLAN

**Architecture :**
```
VLANs 1, 10, 20, 30 → Une seule instance STP

              [Root]
               / \
Chemin        /   \        Chemin
actif        /     \       bloqué
            /       \
         [SW1]----[SW2]
                X
         (même topologie pour tous les VLANs)
```

**Limitation :** Impossible de faire du load-balancing entre VLANs.

### PVST (Per-VLAN Spanning Tree)

**Caractéristiques :**
- ✅ Cisco proprietary (première version)
- ✅ Une instance STP par VLAN
- ��� Load-balancing possible entre VLANs
- ❌ Utilise ISL (Inter-Switch Link) pour le trunking - obsolète
- ❌ Convergence lente (30-50s)

**Architecture :**
```
VLAN 10 :           VLAN 20 :
  [Root10]            [Root20]
    / \                 / \
   /   X(bloqué)       X   \
  /     \             /     \
[SW1]--[SW2]      [SW1]--[SW2]
        DP          RP

Load-balancing : VLAN 10 utilise un chemin, VLAN 20 utilise l'autre
```

**Avantage :** Meilleure utilisation de la bande passante grâce au load-balancing.

### PVST+ (Per-VLAN Spanning Tree Plus)

**Caractéristiques :**
- ✅ Cisco proprietary (évolution de PVST)
- ✅ Une instance STP par VLAN
- ✅ Support du trunking 802.1Q (standard)
- ✅ Interopérabilité avec 802.1D (CST)
- ✅ Load-balancing par VLAN
- ❌ Convergence lente (30-50s)
- ❌ Overhead important (1 BPDU par VLAN toutes les 2s)

**Mode par défaut sur les switches Catalyst modernes (sauf si RSTP activé).**

**Configuration :**
```cisco
! PVST+ est activé par défaut sur Cisco
SW1(config)# spanning-tree mode pvst
```

**BPDUs PVST+ :**
- Utilise l'adresse MAC multicast Cisco : `01:00:0C:CC:CC:CD`
- Encapsulation SNAP (Subnetwork Access Protocol)
- Non-standard IEEE

**Interopérabilité :**
- **PVST+ ↔ 802.1D CST :** Fonctionne, mais un seul spanning tree sur le switch 802.1D
- **PVST+ ↔ PVST+ :** Full interoperability
- **PVST+ ↔ RSTP/MSTP :** Nécessite des ajustements

**💡 Point clé :** PVST+ est le mode STP par défaut des switches Cisco Catalyst. Il offre du load-balancing par VLAN mais génère un overhead important dans les réseaux avec de nombreux VLANs.

### Rapid PVST+ (aperçu)

**Caractéristiques :**
- ✅ Cisco proprietary
- ✅ Basé sur IEEE 802.1w (Rapid STP)
- ✅ Une instance par VLAN
- ✅ **Convergence rapide (~1-2 secondes)**
- ✅ Load-balancing par VLAN

**Configuration :**
```cisco
SW1(config)# spanning-tree mode rapid-pvst
```

**💡 Point clé :** Rapid PVST+ est le mode recommandé pour les nouveaux déploiements Cisco. Il combine la flexibilité de PVST+ avec la vitesse de convergence du RSTP. Ce sera l'objet du module suivant.

---

## 🔍 Dépannage STP

### Commandes de vérification essentielles

**1. Vue d'ensemble du STP**
```cisco
show spanning-tree
show spanning-tree summary
show spanning-tree vlan 10
```

**2. Identifier le Root Bridge**
```cisco
show spanning-tree root
```
Output :
```
                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0010         24586 0ce3.e11a.ba00        4     2   20  15  Gi0/1
```

**3. Vérifier les rôles et états des ports**
```cisco
show spanning-tree interface gigabitEthernet 0/1
```

**4. Afficher les statistiques STP**
```cisco
show spanning-tree detail
show spanning-tree vlan 10 detail
```

**5. Voir l'historique des changements de topologie**
```cisco
show spanning-tree vlan 10 detail | include changes
```

### Problèmes courants

#### 1. Mauvais Root Bridge élu

**Symptôme :** Un switch de distribution ou d'accès devient Root au lieu du switch Core.

**Cause :**
- Priorité non configurée
- Switch avec MAC basse ajouté au réseau

**Vérification :**
```cisco
SW1# show spanning-tree root

Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0010         32778 0000.0c11.1111       8     2   20  15  Gi0/2
                 ^^^^^
          Non optimal (devrait être plus bas)
```

**Solution :**
```cisco
! Sur le switch qui devrait être Root
CoreSW(config)# spanning-tree vlan 10 root primary
```

#### 2. Boucle Layer 2 détectée

**Symptômes :**
- CPU du switch à 100%
- Logs répétitifs de changements de topologie
- Trafic de broadcast excessif
- Adresses MAC qui "flappent" entre ports

**Vérification :**
```cisco
show spanning-tree inconsistentports
show interfaces status err-disabled
show logging | include STP
```

**Causes possibles :**
- STP désactivé sur un lien
- Problème unidirectionnel (lien défectueux)
- Configuration STP incompatible

**Solution :**
```cisco
! Identifier le port problématique
show spanning-tree inconsistentports

! Diagnostiquer
show interfaces gi0/1
show spanning-tree interface gi0/1 detail

! Réactiver le port si err-disabled
interface gi0/1
 shutdown
 no shutdown
exit
```

#### 3. Convergence lente

**Symptôme :** Interruptions de 30-50 secondes lors d'une panne de lien.

**Cause :** Utilisation du STP 802.1D classique au lieu de Rapid STP.

**Vérification :**
```cisco
show spanning-tree summary | include mode
```

**Solution :**
```cisco
! Passer en Rapid PVST+
spanning-tree mode rapid-pvst
```

#### 4. Port bloqué de façon inattendue

**Symptôme :** Un port qui devrait être Forwarding est en Blocking.

**Vérification :**
```cisco
show spanning-tree vlan 10

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Altn BLK 4         128.1    P2p
                         ^^^
                      Bloqué
```

**Causes possibles :**
- Coût du chemin plus élevé qu'un chemin alternatif
- Mauvais root bridge
- Configuration de priorité incorrecte

**Solution :**
```cisco
! Vérifier le Root Path Cost
show spanning-tree vlan 10 | include Cost

! Ajuster le coût si nécessaire
interface gi0/1
 spanning-tree vlan 10 cost 2
exit
```

#### 5. Incompatibilité entre switches

**Symptôme :** STP ne converge pas correctement entre différents switches.

**Causes :**
- Mélange de modes STP (PVST+ vs RSTP vs MSTP)
- Problèmes de compatibilité entre fabricants
- Configuration de VLAN incohérente

**Vérification :**
```cisco
! Vérifier le mode STP
show spanning-tree summary

! Vérifier la config VLAN
show vlan brief
show interfaces trunk
```

**Solution :**
- Normaliser le mode STP sur tous les switches
- Assurer la cohérence des VLANs sur tous les switches
- Utiliser RSTP/MSTP pour l'interopérabilité

**💡 Point clé :** La plupart des problèmes STP proviennent d'une configuration inadéquate du Root Bridge ou d'une utilisation de STP 802.1D au lieu de RSTP. Toujours configurer manuellement le Root Primary et Secondary, et utiliser Rapid PVST+ dans les réseaux modernes.

---

## 📊 Exemple de topologie STP complète

### Scénario de configuration

**Topologie :**
```
                    [Core-SW] (Root Bridge)
                    Priority: 24576
                    BID: 24586.0ce3.e11a.ba00
                         |
                     Gi0/1 (DP, Cost 4)
                         |
                    +---------+---------+
                    |                   |
                Gi0/1 (RP)          Gi0/1 (RP)
               [Distrib-SW1]       [Distrib-SW2]
               BID: 32778        BID: 32778
                    |                   |
                Gi0/2 (DP)          Gi0/2 (DP)
                    |                   |
                    +--------+----------+
                             |
                          Gi0/3 (Altn/BLK)
                          [Access-SW]
                          BID: 32778
```

### Configuration complète

**Core-SW (Root Bridge) :**
```cisco
hostname Core-SW

! Configurer comme Root Primary pour VLAN 10
spanning-tree vlan 10 root primary

! Vérifier
show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    24586 (priority 24576 sys-id-ext 10)
             Address     0ce3.e11a.ba00
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 4         128.1    P2p
Gi0/2               Desg FWD 4         128.2    P2p
```

**Distrib-SW1 :**
```cisco
hostname Distrib-SW1

! Vérifier le rôle Root Port vers Core-SW
show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             Cost        4
             Port        1 (GigabitEthernet0/1)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32778 (priority 32768 sys-id-ext 10)
             Address     0011.2233.4455

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Root FWD 4         128.1    P2p  (vers Core-SW)
Gi0/2               Desg FWD 4         128.2    P2p  (vers Access-SW)
```

**Access-SW :**
```cisco
hostname Access-SW

! Vérifier les rôles des ports
show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             Cost        8
             Port        1 (GigabitEthernet0/1)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32778 (priority 32768 sys-id-ext 10)
             Address     0055.6677.8899

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Root FWD 4         128.1    P2p  (vers Distrib-SW1)
Gi0/2               Altn BLK 4         128.2    P2p  (vers Distrib-SW2)
Gi0/3               Altn BLK 4         128.3    P2p  (lien redondant, bloqué)

! Le port Gi0/3 est bloqué pour éviter la boucle
! Si Gi0/1 tombe, Gi0/2 deviendra le Root Port
```

**💡 Point clé :** Dans cette topologie, le Core-SW est le Root Bridge pour VLAN 10. Tous les autres switches ont un Root Port pointant vers le Core-SW (directement ou indirectement). Le lien redondant entre Distrib-SW2 et Access-SW est bloqué pour prévenir les boucles.

---

## 🎯 Points clés à retenir - Module 2

### Problèmes de redondance L2

- ✅ **Broadcast storms** : Les broadcasts sont propagés indéfiniment dans une topologie en boucle
- ✅ **MAC flapping** : La table MAC devient instable avec des adresses apprises sur différents ports
- ✅ **Trames dupliquées** : Les destinations reçoivent plusieurs copies de la même trame

### Spanning Tree Protocol (STP)

- ✅ **Rôle** : Éliminer les boucles L2 tout en maintenant la redondance
- ✅ **Standard** : IEEE 802.1D (1990)
- ✅ **Algorithme** : STA (Spanning Tree Algorithm)
- ✅ **Convergence** : 30-50 secondes (802.1D classique)

### Bridge ID (BID)

- ✅ **Structure** : Priority (4 bits) + Extended System ID (12 bits) + MAC (48 bits)
- ✅ **Priorité par défaut** : 32768
- ✅ **Incréments** : Multiples de 4096
- ✅ **Élection** : Le BID le plus bas devient Root Bridge

### Processus STP en 4 étapes

1. **Élire le Root Bridge** : Switch avec le BID le plus bas
2. **Sélectionner les Root Ports** : Port avec le meilleur coût vers le Root (1 par switch non-root)
3. **Sélectionner les Designated Ports** : Meilleur port pour chaque segment (1 par segment)
4. **Bloquer les autres ports** : Tous les ports restants sont bloqués (Alternate Ports)

### Rôles des ports

- **Root Port (RP)** : Meilleur chemin vers le Root Bridge (Forwarding)
- **Designated Port (DP)** : Port forwardant sur chaque segment (Forwarding)
- **Alternate/Blocked Port (BP)** : Port bloqué pour éviter les boucles (Blocking/Discarding)

### États des ports STP

| État | Trafic | Apprentissage MAC | BPDUs | Durée |
|------|--------|------------------|-------|-------|
| Blocking | ❌ | ❌ | Reçoit | Variable |
| Listening | ❌ | ❌ | Envoie/Reçoit | 15s |
| Learning | ❌ | ✅ | Envoie/Reçoit | 15s |
| Forwarding | ✅ | ✅ | Envoie/Reçoit | Permanent |

**Convergence totale : 30-50 secondes**

### BPDUs (Bridge Protocol Data Units)

- ✅ **Fréquence** : Envoyés toutes les 2 secondes (Hello Time) par le Root Bridge
- ✅ **Contenu** : Root BID, Sender BID, Root Path Cost, Timers
- ✅ **Types** : Configuration BPDU, TCN BPDU (Topology Change Notification)

### Path Cost

- **10 Mbps** : 100
- **100 Mbps** : 19
- **1 Gbps** : 4
- **10 Gbps** : 2

**Root Path Cost** = Somme des coûts sur le chemin vers le Root

### Timers STP

- **Hello Time** : 2 secondes (fréquence des BPDUs)
- **Forward Delay** : 15 secondes (durée Listening/Learning)
- **Max Age** : 20 secondes (expiration des BPDUs)

**⚠️ Configurer uniquement sur le Root Bridge**

### Variantes STP

| Variante | Standard | Instances | Convergence | Usage |
|----------|----------|-----------|-------------|-------|
| STP | IEEE 802.1D | 1 (CST) | ~30-50s | Legacy |
| PVST+ | Cisco | 1 par VLAN | ~30-50s | Cisco, load balancing |
| Rapid-PVST+ | Cisco/802.1w | 1 par VLAN | ~1-2s | **Recommandé** |
| MSTP | IEEE 802.1s | Multiple | ~1-2s | Enterprise |

### Commandes essentielles

```cisco
! Afficher l'état STP
show spanning-tree
show spanning-tree vlan 10
show spanning-tree summary
show spanning-tree root

! Configurer le Root Bridge
spanning-tree vlan 10 priority 24576
spanning-tree vlan 10 root primary
spanning-tree vlan 10 root secondary

! Modifier les coûts/priorités
interface gi0/1
 spanning-tree cost 10
 spanning-tree port-priority 64
exit

! Modifier les timers (sur le Root uniquement)
spanning-tree vlan 10 hello-time 2
spanning-tree vlan 10 forward-time 15
spanning-tree vlan 10 max-age 20

! Changer de mode STP
spanning-tree mode pvst
spanning-tree mode rapid-pvst
```

### Meilleures pratiques

- ✅ **Toujours configurer le Root Bridge manuellement** (root primary/secondary)
- ✅ **Utiliser Rapid-PVST+ au lieu de PVST+** (convergence rapide)
- ✅ **Documenter la topologie STP** (identifier clairement le Root, les chemins actifs/bloqués)
- ✅ **Activer PortFast/BPDU Guard** sur les ports d'accès (voir Module 3)
- ✅ **Surveiller les changements de topologie** (logs, SNMP)
- ✅ **Éviter de désactiver STP** sauf cas très spécifique et maîtrisé

---

## 🚀 Conclusion

Le Spanning Tree Protocol est un protocole fondamental dans les réseaux Layer 2 redondants. Il élimine les boucles tout en maintenant la haute disponibilité. Bien que le STP 802.1D original ait une convergence lente (30-50s), il a posé les bases des protocoles modernes comme RSTP et MSTP qui convergent en 1-2 secondes.

**Dans le prochain module (Module 3),** nous étudierons l'optimisation avancée de STP avec des fonctionnalités comme PortFast, BPDU Guard, Root Guard, et les mécanismes d'accélération de convergence (UplinkFast, BackboneFast).

**Dans le Module 4,** nous explorerons le Multiple Spanning Tree Protocol (MSTP), qui permet de réduire l'overhead de PVST+ en regroupant plusieurs VLANs dans une même instance STP.

---

**📚 Fin du Module 2 - Spanning Tree Protocol**
