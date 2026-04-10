# QCM - Module 4 : Multiple Spanning Tree Protocol (MSTP)
**CCNP ENCOR v8 - Protocole Spanning Tree Multiple**

---

## 📋 Instructions

- **25 questions à choix multiples**
- **1 seule réponse correcte** par question
- **Durée recommandée** : 30 minutes
- **Seuil de réussite** : 80% (20/25)

---

## 🎯 Questions

### Question 1
Dans un réseau avec 100 VLANs et 50 switches, combien de BPDUs/seconde sont générés avec PVST+ ?
- A) 100 BPDUs/seconde
- B) 500 BPDUs/seconde
- C) 2500 BPDUs/seconde
- D) 5000 BPDUs/seconde

### Question 2
Quelle est la principale limitation de PVST+ que MSTP résout ?
- A) PVST+ ne supporte pas la convergence rapide
- B) PVST+ crée 1 instance STP par VLAN, générant un overhead massif
- C) PVST+ ne fonctionne qu'avec les switches Cisco
- D) PVST+ ne supporte pas le load-balancing

### Question 3
Quel standard IEEE définit MSTP ?
- A) IEEE 802.1D
- B) IEEE 802.1w
- C) IEEE 802.1s
- D) IEEE 802.1Q

### Question 4
Combien d'instances MSTP peuvent être configurées sur un switch Cisco ?
- A) 0-16 instances
- B) 0-64 instances
- C) 1-128 instances
- D) 1-4094 instances

### Question 5
Quels sont les 3 paramètres qui définissent une région MSTP et doivent être IDENTIQUES sur tous les switches de la région ?
- A) Nom de région, Bridge ID, VTP domain
- B) Nom de région, Révision, Mapping VLAN-Instance
- C) Bridge ID, Révision, VTP mode
- D) Nom de région, Native VLAN, Trunk allowed

### Question 6
Le nom de région MSTP peut contenir jusqu'à :
- A) 16 caractères
- B) 32 caractères
- C) 64 caractères
- D) 128 caractères

### Question 7
Quel mécanisme MSTP utilise-t-il pour vérifier la cohérence de configuration entre switches d'une région ?
- A) VTP digest
- B) Hash MD5
- C) Checksum CRC32
- D) Bridge Priority

### Question 8
Qu'est-ce que l'IST (Internal Spanning Tree) ?
- A) L'instance STP pour VLANs 1-100
- B) L'instance 0 (obligatoire) qui contient les VLANs non mappés et interface avec l'extérieur
- C) L'instance STP des trunks inter-régions uniquement
- D) L'algorithme de convergence rapide de MSTP

### Question 9
Les instances MSTI (Multiple Spanning Tree Instance) sont :
- A) Instance 0 uniquement
- B) Instances 1-64
- C) Instances 1-4094
- D) Instances 0-15

### Question 10
Qu'est-ce que le CIST (Common and Internal Spanning Tree) ?
- A) L'instance 0 seulement
- B) Toutes les MSTI regroupées
- C) IST (interne région) + CST (inter-régions)
- D) Le protocole de convergence rapide de MSTP

### Question 11
Que se passe-t-il à la frontière entre deux régions MSTP ?
- A) Tous les BPDUs (IST + MSTI) sont échangés
- B) Seul l'IST (Instance 0) est échangé
- C) Seules les MSTI sont échangées
- D) Aucun BPDU n'est échangé

### Question 12
Quelle commande active le mode MSTP sur un switch ?
- A) `spanning-tree mode mstp`
- B) `spanning-tree mode mst`
- C) `spanning-tree protocol mst`
- D) `mst enable`

### Question 13
Comment entrer dans le mode de configuration de la région MSTP ?
- A) `mst region-config`
- B) `spanning-tree region`
- C) `spanning-tree mst configuration`
- D) `spanning-tree mst region`

### Question 14
Quelle commande permet de mapper les VLANs 10, 20 et 30 à l'instance MSTP 1 ?
- A) `instance 1 vlan 10 20 30`
- B) `instance 1 vlan 10,20,30`
- C) `vlan 10,20,30 instance 1`
- D) `map vlan 10-30 instance 1`

### Question 15
Avant de quitter le mode de configuration MSTP, quelle commande permet de vérifier la configuration ?
- A) `show mst`
- B) `show running-config`
- C) `show current`
- D) `verify config`

### Question 16
Quelle commande définit un switch comme Root Primary pour l'instance MSTP 2 ?
- A) `spanning-tree mst 2 root`
- B) `spanning-tree mst 2 root primary`
- C) `spanning-tree mst 2 priority 0`
- D) `mst 2 root primary`

### Question 17
Quelle commande permet de vérifier la configuration de la région MSTP ?
- A) `show spanning-tree`
- B) `show spanning-tree mst`
- C) `show spanning-tree mst configuration`
- D) `show mst region`

### Question 18
Que voit un réseau PVST+ lorsqu'il est connecté à une région MSTP ?
- A) Toutes les instances MSTP (IST + MSTI)
- B) Uniquement l'IST (Instance 0) avec BPDUs PVST+ générés
- C) Un domaine STP standard 802.1D
- D) Rien, l'interopérabilité est impossible

### Question 19
Quelle commande interface est nécessaire pour l'interopérabilité MSTP vers PVST+ ?
- A) `spanning-tree mode pvst+`
- B) `spanning-tree mst pre-standard`
- C) `spanning-tree pvst-compatibility`
- D) `switchport trunk mode pvst`

### Question 20
Que se passe-t-il si deux switches ont des noms de région MSTP différents mais le même révision et mapping ?
- A) Ils sont dans la même région
- B) Une frontière de région est créée
- C) Le switch avec la priorité la plus basse impose son nom
- D) Erreur de configuration, les switches ne communiquent pas

### Question 21
Combien de fois le réduction de BPDUs peut-elle atteindre avec MSTP par rapport à PVST+ ?
- A) 2x à 5x
- B) 5x à 10x
- C) 10x à 100x
- D) 100x à 1000x

### Question 22
Dans quel scénario MSTP est-il le plus recommandé ?
- A) Réseau avec moins de 20 VLANs
- B) Réseau avec 20-50 VLANs
- C) Réseau avec plus de 100 VLANs
- D) MSTP n'est jamais recommandé, PVST+ est toujours préférable

### Question 23
Quelle est la convergence typique de MSTP ?
- A) 30-50 secondes
- B) 15-20 secondes
- C) 5-10 secondes
- D) 1-2 secondes

### Question 24
Quel est l'effet d'incrémenter le numéro de révision MSTP ?
- A) Force la reconvergence de toutes les instances
- B) Indique une modification du mapping VLAN-Instance
- C) Change la priorité du Root Bridge
- D) Active la compatibilité avec PVST+

### Question 25
Qu'affiche la commande `show spanning-tree mst 1` ?
- A) La configuration de la région MSTP
- B) L'état de l'instance MSTP 1 (Root Bridge, ports, rôles, états)
- C) Les VLANs mappés à l'instance 1
- D) Le nombre de BPDUs sur l'instance 1

---

## ✅ Grille de réponses

| Question | Réponse | Question | Réponse | Question | Réponse |
|----------|---------|----------|---------|----------|---------|
| 1        | ⬜ A ⬜ B ⬜ C ⬜ D | 10 | ⬜ A ⬜ B ⬜ C ⬜ D | 19 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 2        | ⬜ A ⬜ B ⬜ C ⬜ D | 11 | ⬜ A ⬜ B ⬜ C ⬜ D | 20 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 3        | ⬜ A ⬜ B ⬜ C ⬜ D | 12 | ⬜ A ⬜ B ⬜ C ⬜ D | 21 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 4        | ⬜ A ⬜ B ⬜ C ⬜ D | 13 | ⬜ A ⬜ B ⬜ C ⬜ D | 22 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 5        | ⬜ A ⬜ B ⬜ C ⬜ D | 14 | ⬜ A ⬜ B ⬜ C ⬜ D | 23 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 6        | ⬜ A ⬜ B ⬜ C ⬜ D | 15 | ⬜ A ⬜ B ⬜ C ⬜ D | 24 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 7        | ⬜ A ⬜ B ⬜ C ⬜ D | 16 | ⬜ A ⬜ B ⬜ C ⬜ D | 25 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 8        | ⬜ A ⬜ B ⬜ C ⬜ D | 17 | ⬜ A ⬜ B ⬜ C ⬜ D |    |         |
| 9        | ⬜ A ⬜ B ⬜ C ⬜ D | 18 | ⬜ A ⬜ B ⬜ C ⬜ D |    |         |

---

## 📖 Corrigé détaillé

### Question 1 - Réponse : C
**C) 2500 BPDUs/seconde**

**Explication :**
- PVST+ génère 1 BPDU toutes les 2 secondes par VLAN
- 100 VLANs × 50 switches = 5000 instances STP
- 5000 instances ÷ 2 secondes = 2500 BPDUs/seconde
- Cet overhead massif est la principale raison d'utiliser MSTP

**Pourquoi les autres réponses sont fausses :**
- A) 100 serait le nombre de VLANs uniquement
- B) 500 ne correspond à aucun calcul valide
- D) 5000 serait le nombre d'instances, pas BPDUs/seconde

---

### Question 2 - Réponse : B
**B) PVST+ crée 1 instance STP par VLAN, générant un overhead massif**

**Explication :**
- PVST+ : 1 instance STP par VLAN → Overhead CPU, RAM, bande passante
- MSTP regroupe plusieurs VLANs en instances (0-64)
- Réduction de 10x à 100x des BPDUs
- C'est THE limitation que MSTP résout

**Pourquoi les autres réponses sont fausses :**
- A) RSTP/Rapid-PVST+ supportent la convergence rapide
- C) Vrai mais ce n'est pas la limitation que MSTP résout
- D) PVST+ supporte le load-balancing (Root par VLAN)

---

### Question 3 - Réponse : C
**C) IEEE 802.1s**

**Explication :**
- **IEEE 802.1D** : STP original (1990)
- **IEEE 802.1w** : RSTP (2001)
- **IEEE 802.1s** : MSTP (2002) - basé sur RSTP
- **IEEE 802.1Q** : Trunking VLAN (pas STP)

**Pourquoi les autres réponses sont fausses :**
- A) 802.1D = STP original
- B) 802.1w = RSTP (base de MSTP mais pas MSTP lui-même)
- D) 802.1Q = VLAN trunking

---

### Question 4 - Réponse : B
**B) 0-64 instances**

**Explication :**
- **Instance 0 (IST)** : Obligatoire, par défaut
- **Instances 1-64 (MSTI)** : Optionnelles, au choix
- Total : 65 instances possibles (0-64)
- Limitation matérielle Cisco

**Pourquoi les autres réponses sont fausses :**
- A) 0-16 est trop limité
- C) 1-128 dépasse la limite Cisco
- D) 1-4094 serait 1 instance par VLAN (= PVST+)

---

### Question 5 - Réponse : B
**B) Nom de région, Révision, Mapping VLAN-Instance**

**Explication :**
- **3 paramètres critiques** pour région MSTP :
  1. **Nom** (0-32 caractères, case-sensitive)
  2. **Révision** (0-65535)
  3. **Mapping VLAN-Instance** (quelle VLAN → quelle instance)
- Hash MD5 vérifie cohérence
- UNE seule différence → Frontière créée

**Pourquoi les autres réponses sont fausses :**
- A) Bridge ID n'est pas un paramètre de région
- C) VTP mode n'est pas lié à MSTP
- D) Native VLAN et Trunk allowed concernent les trunks, pas MSTP

---

### Question 6 - Réponse : B
**B) 32 caractères**

**Explication :**
- Nom de région MSTP : 0-32 caractères
- Case-sensitive (PARIS ≠ paris)
- Doit être IDENTIQUE sur tous switches de la région
- Bonnes pratiques : Nom descriptif (ex: SITE_PARIS_DC1)

**Pourquoi les autres réponses sont fausses :**
- A) 16 est trop court
- C) 64 dépasse la limite
- D) 128 dépasse largement la limite

---

### Question 7 - Réponse : B
**B) Hash MD5**

**Explication :**
- MSTP calcule un **hash MD5** de la configuration région
- Hash MD5 inclut : nom, révision, mapping VLAN-Instance
- BPDUs contiennent ce hash
- Switches comparent les hash pour détecter incohérences
- Hash différent → Frontière de région

**Pourquoi les autres réponses sont fausses :**
- A) VTP digest est pour VTP, pas MSTP
- C) CRC32 est pour détection erreurs, pas cohérence config
- D) Bridge Priority n'est pas un mécanisme de vérification

---

### Question 8 - Réponse : B
**B) L'instance 0 (obligatoire) qui contient les VLANs non mappés et interface avec l'extérieur**

**Explication :**
- **IST (Internal Spanning Tree)** = Instance 0
- Rôles :
  1. VLANs **non mappés** explicitement aux MSTI
  2. **Interface** avec l'extérieur (autres régions, PVST+, STP)
  3. **Obligatoire** (existe toujours)
- IST + CST = CIST

**Pourquoi les autres réponses sont fausses :**
- A) Pas limité aux VLANs 1-100
- C) Pas uniquement les trunks
- D) C'est une instance, pas un algorithme

---

### Question 9 - Réponse : B
**B) Instances 1-64**

**Explication :**
- **MSTI (Multiple Spanning Tree Instance)** : Instances 1-64
- Optionnelles (vs IST obligatoire)
- Regroupent VLANs spécifiques selon mapping
- Calculent leur propre spanning tree
- Invisibles hors de la région

**Pourquoi les autres réponses sont fausses :**
- A) Instance 0 = IST, pas MSTI
- C) 1-4094 serait le nombre de VLANs
- D) 0-15 est trop limité

---

### Question 10 - Réponse : C
**C) IST (interne région) + CST (inter-régions)**

**Explication :**
- **CIST (Common and Internal Spanning Tree)**
- **IST** : Internal Spanning Tree (Instance 0 interne région)
- **CST** : Common Spanning Tree (inter-régions)
- **CIST** = Combinaison des deux
- Vue globale du spanning tree

**Pourquoi les autres réponses sont fausses :**
- A) IST seul n'est qu'une partie
- B) MSTI sont séparés, pas regroupés dans CIST
- D) CIST n'est pas un protocole de convergence

---

### Question 11 - Réponse : B
**B) Seul l'IST (Instance 0) est échangé**

**Explication :**
- À la **frontière de région** :
  - Seul **IST (Instance 0)** traversé
  - **MSTI (1-64)** restent internes
  - Région vue comme "switch virtuel" par l'extérieur
- Permet interopérabilité avec PVST+, STP

**Pourquoi les autres réponses sont fausses :**
- A) MSTI ne sont jamais échangés hors région
- C) Seules les MSTI est faux (c'est l'IST qui est échangé)
- D) IST est bien échangé

---

### Question 12 - Réponse : B
**B) `spanning-tree mode mst`**

**Explication :**
- Commande : `spanning-tree mode mst`
- Active MSTP sur le switch
- Change du mode PVST+ → MSTP
- **Attention** : Provoque reconvergence !

**Pourquoi les autres réponses sont fausses :**
- A) `mstp` n'est pas la bonne abréviation (c'est `mst`)
- C) `protocol` n'est pas utilisé
- D) `mst enable` n'existe pas

---

### Question 13 - Réponse : C
**C) `spanning-tree mst configuration`**

**Explication :**
- Commande : `spanning-tree mst configuration`
- Entre en mode de configuration région MSTP
- Sub-commandes : `name`, `revision`, `instance`
- **Important** : `show current` avant `exit`

**Pourquoi les autres réponses sont fausses :**
- A) `mst region-config` n'existe pas
- B) `spanning-tree region` n'existe pas
- D) `spanning-tree mst region` n'existe pas

---

### Question 14 - Réponse : B
**B) `instance 1 vlan 10,20,30`**

**Explication :**
- Syntaxe : `instance <num> vlan <list>`
- Liste VLANs : Séparés par virgules OU plages
- Exemples :
  - `instance 1 vlan 10,20,30`
  - `instance 1 vlan 10-30`
  - `instance 1 vlan 10,20,30-40`

**Pourquoi les autres réponses sont fausses :**
- A) Espaces entre VLANs (invalide)
- C) Ordre inversé
- D) `map` n'existe pas

---

### Question 15 - Réponse : C
**C) `show current`**

**Explication :**
- **`show current`** : Dans mode config MSTP
- Affiche config avant application
- Permet validation AVANT `exit`
- **Critique** : Évite erreurs de mapping

**Pourquoi les autres réponses sont fausses :**
- A) `show mst` n'existe pas dans ce mode
- B) `show running-config` fonctionne mais moins spécifique
- D) `verify config` n'existe pas

---

### Question 16 - Réponse : B
**B) `spanning-tree mst 2 root primary`**

**Explication :**
- Syntaxe : `spanning-tree mst <instance> root primary`
- Définit Root Bridge pour instance spécifique
- Priorité automatiquement ajustée (24576)
- Alternative : `spanning-tree mst 2 priority <value>`

**Pourquoi les autres réponses sont fausses :**
- A) Manque `primary`
- C) Priority 0 réservé (utiliser 4096)
- D) Manque `spanning-tree`

---

### Question 17 - Réponse : C
**C) `show spanning-tree mst configuration`**

**Explication :**
- `show spanning-tree mst configuration` : Affiche config région
- Montre : Nom, Révision, Mapping VLAN-Instance
- Permet vérifier cohérence entre switches
- Différent de `show spanning-tree mst` (état instances)

**Pourquoi les autres réponses sont fausses :**
- A) Trop général
- B) Affiche état instances, pas config région
- D) `show mst region` n'existe pas

---

### Question 18 - Réponse : B
**B) Uniquement l'IST (Instance 0) avec BPDUs PVST+ générés**

**Explication :**
- MSTP détecte frontière PVST+
- Génère BPDUs PVST+ pour **VLANs de l'IST uniquement**
- **MSTI restent invisibles** pour PVST+
- Limitation : Load-balancing réduit

**Pourquoi les autres réponses sont fausses :**
- A) MSTI ne sont jamais visibles hors région
- C) Pas vu comme STP standard
- D) Interopérabilité possible

---

### Question 19 - Réponse : B
**B) `spanning-tree mst pre-standard`**

**Explication :**
- `spanning-tree mst pre-standard` : Sur interface vers PVST+
- Active génération BPDUs PVST+ compatibles
- Nécessaire pour interopérabilité MSTP ↔ PVST+
- Appliqué sur interface trunk

**Pourquoi les autres réponses sont fausses :**
- A) Change le mode global, pas l'interop
- C) Commande n'existe pas
- D) Trunk mode concerneles VLANs, pas STP

---

### Question 20 - Réponse : B
**B) Une frontière de région est créée**

**Explication :**
- **UNE seule différence** → Frontière créée
- 3 paramètres doivent être **TOUS identiques** :
  1. Nom de région
  2. Révision
  3. Mapping VLAN-Instance
- Hash MD5 détecte incohérences
- Frontière → Seul IST échangé

**Pourquoi les autres réponses sont fausses :**
- A) Faux, ils sont dans des régions différentes
- C) Aucun mécanisme d'imposition
- D) Communication fonctionne via IST

---

### Question 21 - Réponse : C
**C) 10x à 100x**

**Explication :**
- Exemple :
  - PVST+ avec 100 VLANs : 100 BPDUs/2s
  - MSTP avec 3 instances : 3 BPDUs/2s
  - Réduction : 100 ÷ 3 = 33x
- Réduction typique : **10x à 100x**
- Dépend du nombre de VLANs vs instances

**Pourquoi les autres réponses sont fausses :**
- A) 2x-5x est trop faible
- B) 5x-10x est insuffisant
- D) 100x-1000x est exagéré

---

### Question 22 - Réponse : C
**C) Réseau avec plus de 100 VLANs**

**Explication :**
- **< 50 VLANs** : Rapid-PVST+ suffisant (simple)
- **50-100 VLANs** : Transition possible
- **> 100 VLANs** : MSTP recommandé (réduction overhead)
- **Data Center** : MSTP optimal (efficacité)

**Pourquoi les autres réponses sont fausses :**
- A) Rapid-PVST+ suffisant pour petit réseau
- B) Transition, pas obligatoire
- D) MSTP est recommandé pour grands réseaux

---

### Question 23 - Réponse : D
**D) 1-2 secondes**

**Explication :**
- MSTP basé sur **RSTP (802.1w)**
- Convergence rapide : **1-2 secondes**
- Vs STP original : 30-50 secondes
- Identique à Rapid-PVST+

**Pourquoi les autres réponses sont fausses :**
- A) 30-50s = STP 802.1D original
- B) 15-20s = Convergence intermédiaire (inexacte)
- C) 5-10s = Trop lent pour RSTP/MSTP

---

### Question 24 - Réponse : B
**B) Indique une modification du mapping VLAN-Instance**

**Explication :**
- **Révision** : Version de la configuration région
- Incrémenter après modification mapping
- Bonnes pratiques : Documentation des changements
- Hash MD5 change → Switches détectent modification

**Pourquoi les autres réponses sont fausses :**
- A) Ne force pas reconvergence directement
- C) Priorité Root est séparée
- D) Révision ne contrôle pas compatibilité

---

### Question 25 - Réponse : B
**B) L'état de l'instance MSTP 1 (Root Bridge, ports, rôles, états)**

**Explication :**
- `show spanning-tree mst 1` : État instance 1
- Affiche :
  - Root Bridge (adresse, priorité)
  - Ports (rôles, états, coûts)
  - Topologie instance spécifique
- Différent de `show spanning-tree mst configuration`

**Pourquoi les autres réponses sont fausses :**
- A) Config région = `show spanning-tree mst configuration`
- C) VLANs mappés visible dans config région
- D) Nombre BPDUs non affiché directement

---

## 📊 Tableau de scoring

| Score | Niveau | Appréciation |
|-------|--------|--------------|
| 23-25 | Excellent | Maîtrise parfaite de MSTP |
| 20-22 | Très bien | Bonne compréhension, réviser détails |
| 17-19 | Bien | Compréhension correcte, approfondir instances |
| 14-16 | Moyen | Réviser concepts région et interopérabilité |
| 11-13 | Insuffisant | Revoir cours complet, focus sur IST/MSTI |
| 0-10 | Très insuffisant | Étude approfondie nécessaire |

---

**🎯 Seuil de réussite CCNP : 20/25 (80%)**

---

**📚 Fin du QCM - Module 4 : Multiple Spanning Tree Protocol (MSTP)**
