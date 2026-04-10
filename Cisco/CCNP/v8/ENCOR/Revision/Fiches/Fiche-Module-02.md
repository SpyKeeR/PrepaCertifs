# Fiche de révision - Module 2 : Spanning Tree Protocol
**CCNP ENCOR v8 - Protocole Spanning Tree**

---

## 🎯 Concepts essentiels

### Problèmes de redondance Layer 2

| Problème | Description | Conséquence |
|----------|-------------|-------------|
| **Broadcast Storms** | Propagation infinie des broadcasts dans une boucle | Saturation totale du réseau |
| **MAC Flapping** | Une même MAC apprise sur plusieurs ports | Table MAC instable, forwarding erroné |
| **Trames dupliquées** | La même trame reçue plusieurs fois | Connexions TCP brisées, corruption |

**💡 Sans STP, la redondance L2 = réseau inutilisable en quelques secondes**

---

## 🌳 Spanning Tree Protocol - Vue d'ensemble

### Principe de base

**Objectif :** Créer une topologie logique sans boucle dans un réseau physiquement redondant.

**Méthode :**
- Bloquer stratégiquement certains ports pour éliminer les boucles
- Maintenir ces ports en standby pour convergence rapide en cas de panne
- Créer un "arbre" depuis un switch racine (Root Bridge)

### Algorithme STA en 4 étapes

```
1. Élire le Root Bridge
   └─> Switch avec le Bridge ID (BID) le plus bas

2. Sélectionner les Root Ports (RP)
   └─> 1 par switch non-root, meilleur chemin vers Root

3. Sélectionner les Designated Ports (DP)
   └─> 1 par segment, meilleur switch pour ce segment

4. Bloquer les autres ports (Alternate/Blocked)
   └─> Tous les ports restants sont bloqués
```

---

## 🔧 Bridge ID (BID)

### Structure (64 bits)

```
┌─────────────┬─────────────────┬──────────────────────────┐
│  Priority   │  Extended Sys   │      MAC Address         │
│  (4 bits)   │     ID          │      (48 bits)           │
│  0-15       │  (12 bits)      │  XX:XX:XX:XX:XX:XX       │
│  *4096      │  VLAN ID        │                          │
└─────────────┴─────────────────┴──────────────────────────┘
        Bridge ID (64 bits)
```

**Format affiché :** `Priority.MAC`  
Exemple : `32778.0ce3.e11a.ba00`

### Priorité

- **Valeur par défaut :** 32768
- **Plage :** 0 à 65535
- **Incréments :** Multiples de 4096
- **Valeurs courantes :** 0, 4096, 8192, 16384, 24576, 32768...

**Calcul PVST+ :**
```
Bridge Priority = Base Priority + VLAN ID
Exemple : 32768 + 10 = 32778 (pour VLAN 10)
```

**💡 Plus le BID est bas, plus le switch a de chances d'être Root**

---

## 🏆 Élection du Root Bridge

### Critères d'élection (ordre)

| Ordre | Critère | Préférence |
|-------|---------|-----------|
| 1 | Bridge Priority | Plus basse |
| 2 | MAC Address | Plus basse |

### Configuration

**Méthode 1 : Priorité manuelle**
```cisco
spanning-tree vlan 10 priority 24576
```

**Méthode 2 : Commande root (recommandée)**
```cisco
! Root Primary (Priority = 24576 ou -4096 si Root actuel < 24576)
spanning-tree vlan 10 root primary

! Root Secondary (Priority = 28672)
spanning-tree vlan 10 root secondary
```

**⚠️ Toujours configurer manuellement le Root dans un environnement de production !**

---

## 🔌 Rôles des ports STP

| Rôle | Par switch/segment | État | Fonction |
|------|-------------------|------|----------|
| **Root Port (RP)** | 1 par switch non-root | Forwarding | Meilleur chemin vers Root |
| **Designated Port (DP)** | 1 par segment | Forwarding | Forward sur le segment |
| **Alternate/Blocked (BP)** | Variable | Blocking | Prévenir les boucles |

### Sélection du Root Port

**Critères (ordre de priorité) :**

| Ordre | Critère | Préférence |
|-------|---------|-----------|
| 1 | Root Path Cost | Plus bas |
| 2 | Sender Bridge ID | Plus bas |
| 3 | Sender Port ID | Plus bas |
| 4 | Local Port ID | Plus bas |

---

## 💰 Path Cost - Coût du chemin

### Table des coûts

| Vitesse | Coût 802.1D (short) | Coût 802.1t (long) |
|---------|--------------------|--------------------|
| 10 Mbps | 100 | 2,000,000 |
| 100 Mbps | 19 | 200,000 |
| 1 Gbps | **4** | 20,000 |
| 10 Gbps | **2** | 2,000 |
| 100 Gbps | N/A | 200 |

**💡 Par défaut, Cisco utilise les coûts "short" (802.1D)**

### Root Path Cost

**Définition :** Somme des coûts de tous les liens depuis le switch jusqu'au Root Bridge.

**Exemple :**
```
[Root] ─── 1Gbps (cost 4) ─── [SW1] ─── 1Gbps (cost 4) ─── [SW2]
   0                             4                             8
(Root Path Cost)
```

**Configuration manuelle :**
```cisco
interface GigabitEthernet0/1
 spanning-tree cost 10
 spanning-tree vlan 10 cost 15
exit
```

---

## 🔄 États des ports STP (802.1D)

| État | Trafic | Apprentissage MAC | BPDUs | Durée | Description |
|------|--------|------------------|-------|-------|-------------|
| **Disabled** | ❌ | ❌ | ❌ | N/A | Port éteint |
| **Blocking** | ❌ | ❌ | ✅ Reçoit | Variable | Écoute les BPDUs |
| **Listening** | ❌ | ❌ | ✅ Envoie/Reçoit | 15s | Participe à l'élection |
| **Learning** | ❌ | ✅ | ✅ Envoie/Reçoit | 15s | Apprend les MACs |
| **Forwarding** | ✅ | ✅ | ✅ Envoie/Reçoit | Permanent | État opérationnel |

### Transition d'états

```
BLOCKING
   ↓ (port sélectionné comme RP ou DP)
LISTENING (15 secondes)
   ↓
LEARNING (15 secondes)
   ↓
FORWARDING

Temps total : 30 secondes minimum
```

**💡 Convergence STP 802.1D : 30-50 secondes**

---

## 📤 BPDUs (Bridge Protocol Data Units)

### Types de BPDUs

| Type | Usage | Émetteur | Fréquence |
|------|-------|----------|-----------|
| **Configuration BPDU** | Élection, calcul spanning tree | Root Bridge (généré) / Autres (relayés) | Toutes les 2s |
| **TCN BPDU** | Signaler changement topologie | Tout switch détectant un changement | Événementiel |

### Contenu d'une Configuration BPDU

```
┌─────────────────────────────┐
│ Root Bridge ID              │ ← BID du Root
├─────────────────────────────┤
│ Root Path Cost              │ ← Coût vers Root depuis envoyeur
├─────────────────────────────┤
│ Sender Bridge ID            │ ← BID du switch envoyeur
├─────────────────────────────┤
│ Sender Port ID              │ ← Port d'envoi
├─────────────────────────────┤
│ Timers                      │ ← Hello, MaxAge, Forward Delay
└─────────────────────────────┘
```

**💡 Seul le Root Bridge GÉNÈRE les Configuration BPDUs originaux. Les autres switches les RELAIENT.**

---

## ⏱️ Timers STP

| Timer | Valeur défaut | Plage | Fonction |
|-------|--------------|-------|----------|
| **Hello Time** | 2 secondes | 1-10s | Intervalle envoi BPDUs |
| **Forward Delay** | 15 secondes | 4-30s | Durée états Listening/Learning |
| **Max Age** | 20 secondes | 6-40s | Expiration BPDU |

### Relations entre timers

```
Max Age ≥ 2 × (Hello Time + 1)
Max Age ≤ 2 × (Forward Delay - 1)
```

**Configuration (sur Root uniquement) :**
```cisco
spanning-tree vlan 10 hello-time 2
spanning-tree vlan 10 forward-time 15
spanning-tree vlan 10 max-age 20
```

**⚠️ Ne modifier les timers que sur le Root Bridge !**

---

## 🌐 Variantes du Spanning Tree

| Variante | Standard | Instances | Convergence | Trunking | Notes |
|----------|----------|-----------|-------------|----------|-------|
| **STP** | IEEE 802.1D | 1 (CST) | ~30-50s | - | Original, 1 instance tous VLANs |
| **PVST** | Cisco | 1 par VLAN | ~30-50s | ISL | Obsolète (ISL deprecated) |
| **PVST+** | Cisco | 1 par VLAN | ~30-50s | 802.1Q | Mode défaut Cisco, load-balancing |
| **Rapid-PVST+** | Cisco/802.1w | 1 par VLAN | ~1-2s | 802.1Q | **Recommandé** |
| **MSTP** | IEEE 802.1s | Multiple | ~1-2s | 802.1Q | Regroupe VLANs, réduit overhead |

### PVST+ (Per-VLAN Spanning Tree Plus)

**Caractéristiques :**
- ✅ 1 instance STP par VLAN
- ✅ Load-balancing possible entre VLANs
- ✅ Support 802.1Q (standard)
- ❌ Overhead important (1 BPDU/VLAN toutes les 2s)
- ❌ Convergence lente (30-50s)

**Architecture PVST+ load-balancing :**
```
VLAN 10 :                    VLAN 20 :
[Root10=SW1]--[SW2]          [SW1]--[Root20=SW2]
      |    X (bloqué)      (bloqué) X    |
    [SW3]                              [SW3]

VLANs utilisent des chemins différents
```

**Configuration :**
```cisco
spanning-tree mode pvst
```

**💡 Avantage majeur : Load-balancing par VLAN, meilleure utilisation des liens**

---

## 🔧 Commandes essentielles

### Vérification

```cisco
! Vue d'ensemble STP
show spanning-tree
show spanning-tree vlan 10
show spanning-tree summary

! Identifier le Root Bridge
show spanning-tree root

! Détails d'une interface
show spanning-tree interface gigabitEthernet 0/1
show spanning-tree interface gi0/1 detail

! Mode STP actuel
show spanning-tree summary | include mode
```

### Configuration de base

```cisco
! Changer le mode STP
spanning-tree mode pvst
spanning-tree mode rapid-pvst

! Configurer Root Bridge
spanning-tree vlan 10 priority 24576
spanning-tree vlan 10 root primary
spanning-tree vlan 10 root secondary

! Modifier coût d'un port
interface gi0/1
 spanning-tree cost 10
 spanning-tree vlan 10 cost 15
exit

! Modifier priorité d'un port (tie-breaker)
interface gi0/1
 spanning-tree port-priority 64
 spanning-tree vlan 10 port-priority 32
exit
```

### Configuration des timers (Root uniquement)

```cisco
spanning-tree vlan 10 hello-time 3
spanning-tree vlan 10 forward-time 20
spanning-tree vlan 10 max-age 25
```

---

## 🔍 Dépannage STP

### Problèmes courants

#### 1. Mauvais Root Bridge

**Symptôme :** Switch de distribution/accès devient Root au lieu du Core

**Diagnostic :**
```cisco
show spanning-tree root
! Vérifier quelle est la priorité du Root actuel
```

**Solution :**
```cisco
! Sur le switch qui devrait être Root
spanning-tree vlan 10 root primary
```

---

#### 2. Boucle Layer 2

**Symptômes :**
- CPU switch à 100%
- Trafic broadcast excessif
- MAC flapping entre ports

**Diagnostic :**
```cisco
show spanning-tree inconsistentports
show interfaces status err-disabled
show logging | include STP
```

**Solution :**
```cisco
! Identifier le port problématique
show spanning-tree inconsistentports

! Réactiver si err-disabled
interface gi0/1
 shutdown
 no shutdown
exit
```

---

#### 3. Convergence lente

**Symptôme :** Interruptions de 30-50s lors d'une panne

**Diagnostic :**
```cisco
show spanning-tree summary | include mode
! Si mode = pvst → problème
```

**Solution :**
```cisco
spanning-tree mode rapid-pvst
```

---

#### 4. Port bloqué de façon inattendue

**Diagnostic :**
```cisco
show spanning-tree vlan 10
! Vérifier rôle et coût du port

show spanning-tree vlan 10 | include Cost
! Comparer Root Path Cost
```

**Solution :**
```cisco
! Ajuster le coût si nécessaire
interface gi0/1
 spanning-tree vlan 10 cost 2
exit
```

---

## 📊 Exemple de configuration complète

### Topologie

```
              [Core-SW] (Root Bridge)
              Priority: 24576
                   |
               Gi0/1 (DP, Cost 4)
                   |
          +--------+--------+
          |                 |
      Gi0/1 (RP)        Gi0/1 (RP)
    [Distrib-SW1]     [Distrib-SW2]
          |                 |
      Gi0/2 (DP)        Gi0/2 (DP)
          |                 |
          +--------+--------+
                   |
              Gi0/3 (Altn/BLK)
              [Access-SW]
```

### Configuration

**Core-SW :**
```cisco
hostname Core-SW
spanning-tree vlan 10 root primary
! Résultat : Priority = 24576 + 10 = 24586
```

**Distrib-SW1 / Distrib-SW2 :**
```cisco
hostname Distrib-SW1
spanning-tree vlan 10 root secondary
! Résultat : Priority = 28672 + 10 = 28682
! Gi0/1 devient Root Port (vers Core-SW)
! Gi0/2 devient Designated Port (vers Access-SW)
```

**Access-SW :**
```cisco
hostname Access-SW
! Pas de configuration spéciale
! Gi0/1 devient Root Port (vers Distrib-SW1)
! Gi0/2 bloqué (Alternate Port) pour prévenir boucle
```

---

## 🎯 Points clés à retenir

### Essentiels STP

✅ **Rôle de STP :** Éliminer les boucles L2 tout en maintenant la redondance  
✅ **Convergence 802.1D :** 30-50 secondes (Listening 15s + Learning 15s)  
✅ **Bridge ID :** Priority (4 bits * 4096) + Ext Sys ID (12 bits VLAN) + MAC (48 bits)  
✅ **Élection Root :** BID le plus bas devient Root Bridge  
✅ **TOUJOURS configurer manuellement le Root Primary et Secondary**

### Rôles des ports

✅ **Root Port (RP) :** 1 par switch non-root, meilleur chemin vers Root, Forwarding  
✅ **Designated Port (DP) :** 1 par segment, envoie BPDUs sur segment, Forwarding  
✅ **Alternate Port (BP) :** Bloqué pour prévenir boucles, Blocking/Discarding

### Path Cost

✅ **1 Gbps = 4**, **10 Gbps = 2**, **100 Mbps = 19**, **10 Mbps = 100**  
✅ **Root Path Cost :** Somme des coûts sur le chemin vers Root  
✅ Le coût augmente en s'éloignant du Root

### BPDUs

✅ **Fréquence :** Toutes les 2 secondes (Hello Time)  
✅ **Génération :** Seul le Root génère les Configuration BPDUs originaux  
✅ **Relais :** Les autres switches relaient sur leurs Designated Ports  
✅ **Expiration :** 20 secondes (Max Age)

### Timers

✅ **Hello Time :** 2s (intervalle entre BPDUs)  
✅ **Forward Delay :** 15s (durée Listening et Learning)  
✅ **Max Age :** 20s (expiration BPDU)  
✅ **Configuration :** Sur le Root Bridge uniquement !

### Variantes

✅ **STP 802.1D :** 1 instance, convergence lente, legacy  
✅ **PVST+ :** 1 instance/VLAN, load-balancing, convergence lente, mode défaut Cisco  
✅ **Rapid-PVST+ :** 1 instance/VLAN, convergence rapide (~1-2s), **RECOMMANDÉ**  
✅ **MSTP :** Multiple instances, convergence rapide, réduit overhead

### Meilleures pratiques

✅ Toujours configurer manuellement Root Primary/Secondary  
✅ Utiliser Rapid-PVST+ au lieu de PVST+ classique  
✅ Documenter la topologie STP (Root, chemins actifs/bloqués)  
✅ Surveiller les changements de topologie (logs)  
✅ Activer PortFast/BPDU Guard sur ports d'accès (Module 3)

### Commandes indispensables

```cisco
show spanning-tree
show spanning-tree vlan 10
show spanning-tree root
show spanning-tree interface gi0/1

spanning-tree vlan 10 root primary
spanning-tree vlan 10 root secondary
spanning-tree mode rapid-pvst

interface gi0/1
 spanning-tree cost 10
 spanning-tree port-priority 64
exit
```

---

## 💡 Astuces d'examen

✅ **Élection Root :** Priorité d'abord, puis MAC (plus bas gagne)  
✅ **Root Port :** 1 seul par switch non-root (sauf Root Bridge = 0 RP)  
✅ **DP par segment :** Chaque lien a 1 DP  
✅ **États 802.1D :** Blocking → Listening (15s) → Learning (15s) → Forwarding  
✅ **Coût 1G = 4 :** Mémoriser pour calculs Path Cost  
✅ **PVST+ = 1 instance/VLAN :** Permet load-balancing, overhead important  
✅ **Configuration Root :** `root primary` = 24576, `root secondary` = 28672  
✅ **Timers modifiés uniquement sur Root Bridge**

---

**📚 Fin de la fiche - Module 2 : Spanning Tree Protocol**
