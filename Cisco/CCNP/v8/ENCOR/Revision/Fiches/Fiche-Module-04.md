# Fiche de révision - Module 4 : Multiple Spanning Tree Protocol (MSTP)
**CCNP ENCOR v8 - Protocole Spanning Tree Multiple**

---

## 🎯 Concept MSTP

### Problème de PVST+

**PVST+ (Per-VLAN Spanning Tree Plus) :**
- 1 instance STP par VLAN
- Overhead massif dans grands réseaux

**Exemple calcul BPDUs :**
```
100 VLANs × 50 switches = 2500 BPDUs/seconde
→ Surcharge CPU, bande passante, mémoire
```

### Solution MSTP

**MSTP (IEEE 802.1s) :**
- Regroupe plusieurs VLANs dans une même instance STP
- Réduction 10x à 100x des BPDUs
- Convergence rapide (basé sur RSTP 802.1w)
- Supporte 0-64 instances

**Comparaison :**
```
PVST+ :
VLAN 10 → Instance 10     100 instances
VLAN 20 → Instance 20  =  100 × BPDUs
...

MSTP :
VLANs 10-30 → Instance 1     3 instances
VLANs 40-60 → Instance 2  =  3 × BPDUs
...
```

**💡 Réduction : 90% de BPDUs en moins !**

---

## 🗺️ Régions MSTP

### Concept

**Région MSTP** = Groupe de switches avec configuration identique

### 3 paramètres de région (doivent être IDENTIQUES)

| Paramètre | Description | Plage |
|-----------|-------------|-------|
| **Nom de région** | Identifiant textuel (case-sensitive) | 0-32 caractères |
| **Révision** | Version de la configuration | 0-65535 |
| **Mapping VLAN-Instance** | Quelle VLAN → Quelle instance | VLANs 1-4094 → Inst 0-64 |

**Vérification cohérence :** Hash MD5 de la config partagé dans BPDUs

### Frontière de région

**Frontière** = Port connectant :
- 2 régions MSTP différentes, OU
- 1 région MSTP et domaine non-MSTP (PVST+, STP)

**Comportement à la frontière :**
- Seul l'**IST (Instance 0)** est échangé
- Les **MSTI (1-64)** restent internes à la région
- Région vue comme un "switch virtuel" par l'extérieur

```
Région A          |  Région B
                  |
IST + MSTI 1-2   |   IST + MSTI 1-2
     [SW1]─────IST only────[SW3]
           Frontière
```

**💡 Une seule différence de config → Frontière créée**

---

## 🌳 Instances MSTP

### Types d'instances

#### 1. IST (Internal Spanning Tree) - Instance 0

- **Instance par défaut** (obligatoire)
- VLANs non mappés explicitement
- Interface avec l'extérieur (autres régions, PVST+, STP)

#### 2. MSTI (Multiple Spanning Tree Instance) - Instances 1-64

- Instances supplémentaires (optionnelles)
- Regroupent des VLANs spécifiques
- Calculent leur propre spanning tree

### CIST (Common and Internal Spanning Tree)

**CIST = IST + CST**

- **IST** : Interne à la région
- **CST** : Inter-régions (Common Spanning Tree)
- **CIST** : Combinaison des deux

```
Région A         Région B
  IST               IST
  MSTI 1           MSTI 1
  MSTI 2           MSTI 2
    |                |
    └──────CST───────┘
         CIST
```

---

## 🔧 Configuration MSTP

### Configuration complète

```cisco
! 1. Mode MSTP
spanning-tree mode mst

! 2. Configuration région (IDENTIQUE sur tous switches)
spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10,20,30
 instance 2 vlan 100-199
 instance 3 vlan 200-299
 
 ! Vérifier avant de quitter
 show current
 
 ! Appliquer
 exit

! 3. Root Bridges par instance
spanning-tree mst 0 root primary
spanning-tree mst 1 root primary
spanning-tree mst 2 root secondary

! 4. Priorité manuelle (alternative)
spanning-tree mst 0 priority 24576
spanning-tree mst 1 priority 28672

! 5. Coût/priorité de port (optionnel)
interface gi0/1
 spanning-tree mst 0 cost 10
 spanning-tree mst 1 port-priority 64
exit

! 6. Fonctionnalités avancées
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default
```

### Validation configuration

**Avant de quitter `spanning-tree mst configuration` :**
```cisco
show current

Current MST configuration
Name      [ENTREPRISE_HQ]
Revision  1     Instances configured 4

Instance  Vlans mapped
--------  ---------------------------------------------------------------------
0         1-9,11-19,21-29,31-99,300-4094
1         10,20,30
2         100-199
3         200-299
```

**💡 Valider avec `show current` avant `exit` pour éviter erreurs !**

---

## 🔍 Vérification MSTP

### Commandes essentielles

```cisco
! Configuration région
show spanning-tree mst configuration

! État toutes instances
show spanning-tree mst

! État instance spécifique
show spanning-tree mst 1

! Détails interface
show spanning-tree mst interface gi0/1

! Résumé
show spanning-tree summary

! Vérifier mode STP
show spanning-tree summary | include mode
```

### Output typique

```cisco
show spanning-tree mst

##### MST0    vlans mapped:   1-9,11-99,300-4094
Bridge        address 0ce3.e11a.ba00  priority  24576 (24576 sysid 0)
Root          this bridge is the root

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 20000     128.1    P2p
Gi0/2               Desg FWD 20000     128.2    P2p

##### MST1    vlans mapped:   10,20,30
Bridge        address 0ce3.e11a.ba00  priority  24577 (24576 sysid 1)
Root          this bridge is the root

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 20000     128.1    P2p
Gi0/2               Altn BLK 20000     128.2    P2p
```

---

## 🔄 Interopérabilité

### MSTP ↔ MSTP (régions différentes)

**Comportement :**
- Seul **IST (Instance 0)** échangé entre régions
- **MSTI (1-64)** invisibles hors région
- Région vue comme "switch virtuel"

### MSTP ↔ PVST+

**Problème :** PVST+ envoie 1 BPDU/VLAN, MSTP envoie 1 BPDU/instance

**Solution :**
- MSTP détecte frontière PVST+
- Génère BPDUs PVST+ pour **VLANs de l'IST uniquement**
- MSTI restent invisibles

**Configuration requise :**
```cisco
interface gi0/10
 description Lien vers PVST+
 spanning-tree mst pre-standard
exit
```

**Limitations :**
- Seul IST (Instance 0) participe
- MSTI (1-64) invisibles pour PVST+
- Load-balancing limité

### MSTP ↔ STP 802.1D

**Comportement :**
- Région MSTP → Vue comme 1 switch par STP
- Seul IST échangé
- CST (Common Spanning Tree) entre domaines

---

## 📊 Comparaison PVST+ vs MSTP

| Aspect | PVST+ | Rapid-PVST+ | MSTP |
|--------|-------|-------------|------|
| **Standard** | Cisco | Cisco/802.1w | IEEE 802.1s |
| **Instances** | 1 par VLAN | 1 par VLAN | 0-64 instances |
| **Convergence** | ~30-50s | ~1-2s | ~1-2s |
| **BPDUs (100 VLANs)** | 100/2s | 100/2s | 3-10/2s |
| **Overhead CPU** | Élevé | Élevé | Faible |
| **Scalabilité** | Limitée | Limitée | Excellente |
| **Complexité** | Moyenne | Moyenne | Élevée |
| **Load-balancing** | ✅ Par VLAN | ✅ Par VLAN | ✅ Par instance |

### Recommandations usage

| Réseau | VLANs | Choix | Justification |
|--------|-------|-------|---------------|
| Petit | < 50 | **Rapid-PVST+** | Simple, convergence rapide |
| Moyen | 50-100 | Rapid-PVST+ ou MSTP | Transition si overhead croissant |
| Grand | > 100 | **MSTP** | Réduction overhead significative |
| Data Center | Variable | **MSTP** | Efficacité + contrôle topologie |

**💡 MSTP optimal pour réseaux > 100 VLANs**

---

## 🎯 Meilleures pratiques

### Planification

✅ **Région unique** par site/réseau (cohérence)  
✅ **Nom descriptif** (`SITE_PARIS_DC1`)  
✅ **Incrémenter révision** à chaque modif  
✅ **Documenter mapping** VLAN-Instance  
✅ **Limiter à 3-5 instances** (suffisant)

### Regroupement VLANs

**Exemple :**
```
Instance 0 (IST) : Management, natif
Instance 1 : VLANs DATA (10-50)
Instance 2 : VLANs VOIX (100-150)
Instance 3 : VLANs SERVEURS (200-250)
```

### Root Bridges

**Option 1 : Même Root pour toutes instances**
```cisco
! Core-SW : Root Primary pour toutes instances
spanning-tree mst 0-3 root primary
```

**Option 2 : Load-balancing entre Core**
```cisco
! Core-SW1 : Root Primary Inst 0,1
! Core-SW2 : Root Primary Inst 2,3
```

### Déploiement

✅ Tester en lab avant production  
✅ Migration progressive (zone isolée d'abord)  
✅ Fenêtre de maintenance (changement mode = reconvergence)  
✅ Scripts pour auditer cohérence région  
✅ Monitorer changements topologie (SNMP, Syslog)

---

## 🎯 Points clés à retenir

### Limitations PVST+

✅ **1 instance par VLAN** → Overhead massif (BPDUs, CPU, mémoire)  
✅ **100 VLANs × 50 switches** = 2500 BPDUs/seconde  
✅ Complexité gestion (Root par VLAN, dépannage)

### Concept MSTP

✅ **IEEE 802.1s** : Regroupe VLANs en instances  
✅ **Réduction 10x à 100x** des BPDUs  
✅ **Convergence rapide** (RSTP) : 1-2 secondes  
✅ **0-64 instances** supportées

### Régions MSTP

✅ **Région** = Config identique (nom, révision, mapping)  
✅ **3 paramètres critiques** (tous doivent être identiques)  
✅ **Hash MD5** vérifie cohérence  
✅ **Frontière** = Seul IST échangé

### Instances

✅ **IST (Instance 0)** : Obligatoire, VLANs non mappés, interface ext  
✅ **MSTI (1-64)** : Optionnelles, regroupement VLANs  
✅ **CIST** = IST (interne) + CST (inter-régions)

### Configuration

```cisco
spanning-tree mode mst

spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10-30
 instance 2 vlan 100-199
 show current  ← Valider avant exit
 exit

spanning-tree mst 0 root primary
spanning-tree mst 1 root primary

spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default
```

### Vérification

```cisco
show spanning-tree mst configuration   ! Config région
show spanning-tree mst                 ! État instances
show spanning-tree mst 1               ! Instance spécifique
show spanning-tree summary             ! Résumé
```

### Interopérabilité

✅ **MSTP ↔ MSTP** (régions diff) : Seul IST échangé  
✅ **MSTP ↔ PVST+** : Frontière, BPDUs PVST+ générés pour IST  
✅ **MSTP ↔ STP** : Région = 1 switch virtuel  
⚠️ **MSTI invisibles** hors région

### Choix technologie

✅ **< 50 VLANs** : Rapid-PVST+ (simple, convergence rapide)  
✅ **> 100 VLANs** : MSTP (réduction overhead, scalabilité)  
✅ **Data Center** : MSTP (efficacité maximale)

---

## 💡 Astuces d'examen

✅ **MSTP = IEEE 802.1s**, basé sur **RSTP 802.1w**  
✅ **3 paramètres région** : Nom + Révision + Mapping (TOUS doivent être identiques)  
✅ **IST = Instance 0** (obligatoire, interface externe)  
✅ **MSTI = Instances 1-64** (optionnelles, internes)  
✅ **CIST = IST + CST** (interne + inter-régions)  
✅ **Frontière** = Seul IST traversé, MSTI invisibles  
✅ **`show current`** : Valider config AVANT `exit`  
✅ **Révision** : Incrémenter à chaque modif mapping  
✅ **Load-balancing** : Root Bridges différents par instance  
✅ **Interop PVST+** : `spanning-tree mst pre-standard`  
✅ **Réduction overhead** : 10x à 100x moins BPDUs que PVST+  
✅ **Convergence** : 1-2s (même que RSTP)

---

**📚 Fin de la fiche - Module 4 : Multiple Spanning Tree Protocol (MSTP)**
