# Module 4 : Multiple Spanning Tree Protocol (MSTP)
**CCNP ENCOR v8 - Protocole Spanning Tree Multiple**

---

## 📋 Vue d'ensemble du module

### Objectifs du module
Ce module couvre le Multiple Spanning Tree Protocol (MSTP IEEE 802.1s), qui optimise l'utilisation de STP dans les réseaux avec de nombreux VLANs. MSTP combine la convergence rapide de RSTP avec une efficacité accrue en regroupant plusieurs VLANs dans une même instance STP, réduisant ainsi l'overhead de PVST+.

### Thèmes principaux
1. **Limitations de PVST+** - Overhead dans les grands réseaux
2. **Concept MSTP** - Regroupement de VLANs en instances
3. **Régions MSTP** - Configuration de domaines MSTP
4. **Instances MSTP (MSTI)** - Gestion des instances multiples
5. **IST et CIST** - Arbre interne et commun
6. **Configuration et vérification MSTP**
7. **Interopérabilité avec PVST+ et STP**

---

## ⚠️ Limitations de PVST+

### Rappel : Fonctionnement de PVST+

**PVST+ (Per-VLAN Spanning Tree Plus) :**
- Crée **une instance STP par VLAN**
- Permet le load-balancing entre VLANs
- Utilise le trunking 802.1Q (standard)
- Convergence lente : 30-50 secondes (802.1D classique)

**Rapid-PVST+ :**
- Même principe qu'une instance par VLAN
- Convergence rapide : 1-2 secondes (802.1w RSTP)
- Mode par défaut sur switches Cisco modernes

### Problèmes de PVST+ dans les grands réseaux

#### 1. Overhead important de BPDUs

**Calcul du trafic BPDU :**

```
Environnement typique :
- 100 VLANs actifs
- 50 switches
- Hello Time = 2 secondes

BPDUs par switch :
- 100 VLANs × 1 BPDU toutes les 2s = 50 BPDUs/seconde

BPDUs totaux dans le réseau :
- 50 switches × 50 BPDUs/s = 2500 BPDUs/seconde
- Soit 1 BPDU toutes les 0,4 millisecondes !
```

**Conséquences :**
- 🚫 Consommation de bande passante (surtout sur liens lents)
- 🚫 CPU des switches surchargé (traitement de milliers de BPDUs)
- 🚫 Délai de convergence cumulé si tous les VLANs reconvergent simultanément

#### 2. Consommation de ressources CPU/mémoire

**Chaque instance STP consomme :**
- Mémoire pour la table STP (états, timers, BPDUs)
- CPU pour calculer le spanning tree
- CPU pour traiter les BPDUs reçus

**Exemple :**
```
Switch avec 1000 VLANs :
- 1000 instances STP indépendantes
- 1000 calculs STA (Spanning Tree Algorithm)
- 1000 états de ports à maintenir
- Utilisation CPU significative, même en état stable
```

#### 3. Complexité de gestion

**Challenges administratifs :**
- Configuration du Root Bridge pour chaque VLAN
- Vérification de la convergence pour chaque VLAN
- Dépannage complexe (quelle instance STP est problématique ?)
- Documentation de la topologie pour tous les VLANs

**💡 Point clé :** PVST+ fonctionne bien pour les petits réseaux (<50 VLANs), mais devient inefficace et difficile à gérer dans les grands réseaux d'entreprise avec des centaines de VLANs.

---

## 🌐 Concept de MSTP (IEEE 802.1s)

### Présentation de MSTP

**MSTP (Multiple Spanning Tree Protocol)** est un standard IEEE 802.1s publié en 2002.

**Objectifs :**
- Réduire l'overhead de PVST+ (moins de BPDUs)
- Maintenir la convergence rapide de RSTP
- Permettre le load-balancing (comme PVST+)
- Améliorer la scalabilité

### Principe de fonctionnement

**Idée centrale :** Regrouper plusieurs VLANs dans une **même instance STP**.

**Comparaison PVST+ vs MSTP :**

```
PVST+ (1 instance par VLAN) :
VLAN 10 → Instance 10
VLAN 20 → Instance 20
VLAN 30 → Instance 30
VLAN 40 → Instance 40
...
VLAN 100 → Instance 100

Total : 100 instances STP = 100 × BPDUs


MSTP (regroupement en instances) :
VLANs 10, 20, 30 → Instance 1
VLANs 40, 50, 60 → Instance 2
VLANs 70, 80, 90 → Instance 3
...

Total : 10 instances MSTP = 10 × BPDUs

Réduction : 90% de BPDUs en moins !
```

**Avantages MSTP :**
- ✅ Réduction drastique du nombre de BPDUs (10x à 100x moins selon regroupement)
- ✅ Moins de charge CPU (moins d'instances à calculer)
- ✅ Convergence rapide (basé sur RSTP 802.1w)
- ✅ Load-balancing possible (instances différentes peuvent utiliser des chemins différents)
- ✅ Scalabilité : Supporte jusqu'à **65 instances** (0-64)

**Inconvénients MSTP :**
- ⚠️ Configuration plus complexe
- ⚠️ Nécessite une planification minutieuse
- ⚠️ Tous les switches doivent avoir la même configuration de région
- ⚠️ Interopérabilité avec PVST+ limitée

**💡 Point clé :** MSTP est le choix optimal pour les grands réseaux d'entreprise avec de nombreux VLANs. Il combine efficacité (moins de BPDUs) et rapidité de convergence (RSTP).

---

## 🗺️ Régions MSTP

### Concept de région MSTP

Une **région MSTP** est un groupe de switches qui partagent :
1. **Même nom de région**
2. **Même numéro de révision**
3. **Même mapping VLAN-vers-Instance**

**Règle d'or :** Tous les switches d'une région MSTP doivent avoir une configuration **identique** sur ces trois paramètres.

### Paramètres de région

#### 1. Nom de région (Region Name)

**Caractéristiques :**
- Chaîne de caractères ASCII
- Longueur : 0 à 32 caractères
- **Sensible à la casse** (case-sensitive)
- Valeur par défaut : vide

**Usage :** Identifier logiquement la région (par site, par bâtiment, etc.)

#### 2. Numéro de révision (Revision Number)

**Caractéristiques :**
- Entier non signé
- Plage : 0 à 65535
- Valeur par défaut : 0

**Usage :** Indiquer la version de la configuration de la région (incrémenté à chaque modification)

#### 3. Mapping VLAN-vers-Instance (VLAN-to-Instance Mapping)

**Caractéristiques :**
- Table associant chaque VLAN (1-4094) à une instance MSTP (0-64)
- Par défaut : Tous les VLANs mappés à l'instance 0 (IST)

**Usage :** Définir quels VLANs appartiennent à quelle instance

### Exemple de région MSTP

```
Région "PARIS_DATACENTER"
Révision : 1

Mapping VLAN-Instance :
- VLANs 1-10, 20, 30    → Instance 0 (IST)
- VLANs 100-199         → Instance 1
- VLANs 200-299         → Instance 2
- VLANs 300-399         → Instance 3

Tous les switches de cette région doivent avoir exactement cette configuration.
```

### Vérification de la cohérence de région

**MSTP calcule un hash (MD5) de la configuration de région :**
- Nom de région
- Numéro de révision
- Mapping VLAN-Instance complet

**Processus :**
1. Chaque switch calcule le hash de sa configuration
2. Les switches échangent ces hash dans les BPDUs
3. Si les hash correspondent → Même région
4. Si les hash diffèrent → Régions différentes

**💡 Point clé :** Un seul caractère de différence dans le nom de région, ou une seule différence dans le mapping VLAN, et les switches seront dans des régions différentes (même s'ils sont physiquement connectés).

### Frontières de région

**Frontière de région (Region Boundary) :** Port connectant deux régions MSTP différentes, ou une région MSTP et un domaine non-MSTP (PVST+, STP).

**Comportement à la frontière :**
- Seules les informations de **l'IST (Instance 0)** sont échangées
- Les instances 1-64 (MSTI) ne sont pas propagées au-delà de la région
- La région est vue comme un "switch virtuel" (black box) par le STP externe

```
Région A                |  Région B
                        |
VLANs 10-20 → Inst 1   |  VLANs 10-20 → Instance 1
VLANs 30-40 → Inst 2   |  VLANs 30-40 → Instance 2
                        |
[SW1]-------[SW2]-------+-------[SW3]-------[SW4]
              |         |         |
          Frontière     |     Pas de frontière
     (hash différents)  |   (hashes identiques)
```

**💡 Point clé :** La cohérence de la région est critique. Une seule erreur de configuration sur un switch peut le placer dans une région différente, créant une frontière non désirée.

---

## 🌳 Instances MSTP (MSTI)

### Types d'instances MSTP

MSTP utilise deux types d'instances :

#### 1. IST (Internal Spanning Tree) - Instance 0

**Caractéristiques :**
- **Instance par défaut** (numéro 0)
- **Obligatoire** sur tous les switches MSTP
- Tous les VLANs qui ne sont pas explicitement mappés à une autre instance appartiennent à l'IST
- Utilisée pour communiquer avec les régions externes

**Rôle de l'IST :**
- Calculer le spanning tree pour les VLANs non mappés
- Interface avec les régions MSTP externes ou domaines STP/PVST+

#### 2. MSTI (Multiple Spanning Tree Instance) - Instances 1 à 64

**Caractéristiques :**
- Instances supplémentaires (numéros 1 à 64)
- Optionnelles
- Chaque MSTI calcule son propre spanning tree indépendamment

**Usage :** Regrouper des VLANs avec des besoins de topologie similaires

### CIST (Common and Internal Spanning Tree)

Le **CIST** est la combinaison de :
- **IST** : Spanning tree à l'intérieur d'une région MSTP
- **CST** : Common Spanning Tree entre les régions

**Fonctionnement du CIST :**
```
Région A             Région B              Région C
   |                    |                     |
  IST  ←──────────────CST──────────────→    IST
   |                    |                     |
 MSTI 1              MSTI 1                MSTI 1
 MSTI 2              MSTI 2                MSTI 2

CIST = IST + CST
```

**💡 Point clé :** Le CIST permet l'interopérabilité entre les régions MSTP et avec les domaines STP/PVST+. À l'extérieur d'une région, seul l'IST est visible (les MSTI sont internes).

---

## 🔧 Configuration de MSTP

### Étapes de configuration

#### Étape 1 : Définir le mode MSTP

```cisco
! Passer en mode MSTP
spanning-tree mode mst
```

#### Étape 2 : Configurer la région MSTP

```cisco
! Entrer en mode de configuration MST
spanning-tree mst configuration

! Nom de la région (32 caractères max, case-sensitive)
name PARIS_DC

! Numéro de révision (0-65535)
revision 1

! Mapper les VLANs aux instances
instance 1 vlan 10-20,30
instance 2 vlan 100-199
instance 3 vlan 200-299

! Vérifier la configuration avant de quitter
show current

! Appliquer et quitter
exit
```

**Output de `show current` :**
```
Current MST configuration
Name      [PARIS_DC]
Revision  1     Instances configured 4

Instance  Vlans mapped
--------  ---------------------------------------------------------------------
0         1-9,21-29,31-99,300-4094
1         10-20,30
2         100-199
3         200-299
-------------------------------------------------------------------------------
```

#### Étape 3 : Configurer les Root Bridges par instance

**Définir le Root Bridge pour chaque instance :**
```cisco
! Root Primary pour l'instance 0 (IST)
spanning-tree mst 0 root primary

! Root Primary pour l'instance 1
spanning-tree mst 1 root primary

! Root Secondary pour l'instance 2
spanning-tree mst 2 root secondary
```

**Ou définir manuellement la priorité :**
```cisco
! Priorité pour l'instance 0
spanning-tree mst 0 priority 24576

! Priorité pour l'instance 1
spanning-tree mst 1 priority 28672
```

**💡 Point clé :** Comme en PVST+, il est essentiel de configurer manuellement les Root Bridges pour chaque instance afin de contrôler la topologie.

#### Étape 4 : Configurer les coûts et priorités de ports (optionnel)

```cisco
interface GigabitEthernet0/1
 ! Coût pour l'instance 0
 spanning-tree mst 0 cost 10
 
 ! Coût pour l'instance 1
 spanning-tree mst 1 cost 20
 
 ! Priorité de port pour l'instance 2
 spanning-tree mst 2 port-priority 64
exit
```

### Exemple de configuration complète

**Switch Core (Root Bridge) :**
```cisco
hostname Core-SW1

! Activer MSTP
spanning-tree mode mst

! Configuration de la région
spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10,20,30
 instance 2 vlan 100,200,300
 exit

! Configurer comme Root Primary pour toutes les instances
spanning-tree mst 0 root primary
spanning-tree mst 1 root primary
spanning-tree mst 2 root primary

! PortFast et BPDU Guard globaux (ports d'accès)
spanning-tree portfast default
spanning-tree portfast bpduguard default

! Loop Guard global
spanning-tree loopguard default
```

**Switch Distribution (Root Secondary) :**
```cisco
hostname Distrib-SW1

! Activer MSTP
spanning-tree mode mst

! Configuration de la région (IDENTIQUE au Core)
spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10,20,30
 instance 2 vlan 100,200,300
 exit

! Configurer comme Root Secondary
spanning-tree mst 0 root secondary
spanning-tree mst 1 root secondary
spanning-tree mst 2 root secondary

! PortFast, BPDU Guard, Loop Guard
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default
```

**Switch Access :**
```cisco
hostname Access-SW1

! Activer MSTP
spanning-tree mode mst

! Configuration de la région (IDENTIQUE)
spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10,20,30
 instance 2 vlan 100,200,300
 exit

! Pas de configuration Root (ce switch ne sera pas Root)

! PortFast, BPDU Guard, Loop Guard
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default
```

**💡 Point clé :** La configuration de la région (name, revision, mapping) doit être **STRICTEMENT IDENTIQUE** sur tous les switches de la région. Une seule différence et les switches seront dans des régions séparées.

---

## 🔍 Vérification de MSTP

### Commandes de vérification essentielles

#### 1. Afficher la configuration MST

```cisco
! Afficher la configuration MST actuelle
show spanning-tree mst configuration

Name      [ENTREPRISE_HQ]
Revision  1     Instances configured 3

Instance  Vlans mapped
--------  ---------------------------------------------------------------------
0         1-9,11-19,21-29,31-99,101-199,201-299,301-4094
1         10,20,30
2         100,200,300
-------------------------------------------------------------------------------
```

#### 2. Afficher l'état MST

```cisco
! Vue d'ensemble de toutes les instances
show spanning-tree mst

##### MST0    vlans mapped:   1-9,11-19,21-29,31-99,101-199,201-299,301-4094
Bridge        address 0ce3.e11a.ba00  priority      24576 (24576 sysid 0)
Root          this bridge is the root

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 20000     128.1    P2p
Gi0/2               Desg FWD 20000     128.2    P2p


##### MST1    vlans mapped:   10,20,30
Bridge        address 0ce3.e11a.ba00  priority      24577 (24576 sysid 1)
Root          this bridge is the root

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 20000     128.1    P2p
Gi0/2               Desg FWD 20000     128.2    P2p


##### MST2    vlans mapped:   100,200,300
Bridge        address 0ce3.e11a.ba00  priority      24578 (24576 sysid 2)
Root          this bridge is the root

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Desg FWD 20000     128.1    P2p
Gi0/2               Desg FWD 20000     128.2    P2p
```

#### 3. Afficher une instance spécifique

```cisco
! Afficher uniquement l'instance 1
show spanning-tree mst 1

##### MST1    vlans mapped:   10,20,30
Bridge        address 0ce3.e11a.ba00  priority      28673 (28672 sysid 1)
Root          address 0ce3.e11a.ba00  priority      24577 (24576 sysid 1)
              port    Gi0/1           path cost     20000

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/1               Root FWD 20000     128.1    P2p
Gi0/2               Altn BLK 20000     128.2    P2p
```

#### 4. Afficher les détails d'une interface

```cisco
show spanning-tree mst interface GigabitEthernet0/1

GigabitEthernet0/1 of MST0 is designated forwarding
  Port info  port id      128.1  priority  128  cost   20000
  Designated root  address  0ce3.e11a.ba00  priority  24576
  Designated bridge address 0ce3.e11a.ba00  priority  24576
  ...

GigabitEthernet0/1 of MST1 is designated forwarding
  Port info  port id      128.1  priority  128  cost   20000
  Designated root  address  0ce3.e11a.ba00  priority  24577
  ...
```

#### 5. Afficher un résumé

```cisco
show spanning-tree summary

Switch is in mst mode
Root bridge for: MST0, MST1, MST2
Extended system ID           : enabled
Portfast Default             : enabled
PortFast BPDU Guard Default  : enabled
Portfast BPDU Filter Default : disabled
Loopguard Default            : enabled
...

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
MST0                   0        0         0        2          2
MST1                   0        0         0        2          2
MST2                   1        0         0        1          2
---------------------- -------- --------- -------- ---------- ----------
3 mst                  1        0         0        5          6
```

---

## 🔄 Interopérabilité MSTP avec PVST+ et STP

### Scénarios d'interopérabilité

MSTP peut coexister avec d'autres variantes de STP dans le même réseau.

#### 1. MSTP ↔ MSTP (régions différentes)

**Comportement :**
- Seul l'IST (Instance 0) est échangé entre les régions
- Chaque région est vue comme un "switch virtuel" par les autres régions
- Les MSTI (1-64) restent internes à chaque région

```
Région A                  Région B
  IST (Inst 0)              IST (Inst 0)
  MSTI 1                    MSTI 1
  MSTI 2                    MSTI 2
      |                         |
   [SW1]----IST BPDUs----[SW3]
      |                         |
   Pas d'échange           Pas d'échange
   de MSTI 1/2             de MSTI 1/2
```

#### 2. MSTP ↔ PVST+

**Problème :** PVST+ envoie un BPDU par VLAN, MSTP envoie un BPDU par instance (regroupant plusieurs VLANs).

**Mécanisme de compatibilité :**
- MSTP détecte les BPDUs PVST+ sur un port
- Ce port est marqué comme une **frontière** (boundary)
- MSTP envoie des BPDUs PVST+ pour **tous les VLANs** mappés sur l'IST (Instance 0) vers ce port
- Les MSTI (1-64) ne sont pas visibles par le domaine PVST+

**Comportement :**
```
Région MSTP                     Domaine PVST+
  IST : VLANs 1-100               VLAN 10 : Instance 10
  MSTI 1 : VLANs 101-200          VLAN 20 : Instance 20
  MSTI 2 : VLANs 201-300          ...
      |                           VLAN 100 : Instance 100
   [SW-MSTP]---Frontière---[SW-PVST+]
      |                           |
Envoie BPDUs PVST+          Reçoit BPDUs PVST+
pour VLANs 1-100            pour chaque VLAN
```

**Limitations :**
- Seul l'IST (Instance 0) participe à l'interopérabilité
- Les MSTI (1-64) sont invisibles pour PVST+
- Load-balancing limité (tous les VLANs de l'IST suivent le même chemin côté MSTP)

**Configuration requise :**

Sur le switch MSTP connecté au domaine PVST+ :
```cisco
interface GigabitEthernet0/10
 description Lien vers domaine PVST+
 spanning-tree mst pre-standard
 ! Force l'envoi de BPDUs compatibles PVST+
exit
```

#### 3. MSTP ↔ STP 802.1D (CST)

**Comportement :**
- MSTP envoie des BPDUs IST (Instance 0) sur les ports connectés à un domaine STP
- Le domaine STP voit la région MSTP comme un seul "switch"
- Une seule instance STP inter-régions (CST)

**Interaction :**
```
Région MSTP                     Domaine STP 802.1D
  IST                             CST (1 instance)
  MSTI 1                          (tous les VLANs)
  MSTI 2
      |
   [SW-MSTP]------IST BPDUs------[SW-STP]
      |                              |
Vue comme 1 switch             Vue comme 1 région
```

**💡 Point clé :** L'interopérabilité entre MSTP et PVST+ fonctionne, mais avec des limitations. Pour un déploiement optimal, préférez une migration complète vers MSTP sur tous les switches.

---

## 🎯 Meilleures pratiques MSTP

### Planification de la région

✅ **Définir une région unique pour le réseau entier** (ou par site si géographiquement distribué)  
✅ **Utiliser un nom de région descriptif** (ex: "SITE_PARIS_BATIMENT_A")  
✅ **Incrémenter la révision à chaque modification** de la configuration MST  
✅ **Documenter le mapping VLAN-Instance** dans un document de référence  
✅ **Valider la configuration avec `show current`** avant de quitter `spanning-tree mst configuration`

### Regroupement des VLANs en instances

✅ **Regrouper les VLANs par fonction ou par bâtiment** (ex: VLAN DATA, VLAN VOIX, VLAN SERVEURS)  
✅ **Limiter le nombre d'instances** (typiquement 3-5 instances suffisent)  
✅ **Assigner les VLANs critiques à l'IST (Instance 0)** pour garantir la connectivité de base  
✅ **Créer des instances distinctes pour le load-balancing** (instances avec des Root Bridges différents)

**Exemple de regroupement :**
```
Instance 0 (IST) : Management, natif, VLANs de base
Instance 1 : VLANs DATA utilisateurs (10-50)
Instance 2 : VLANs VOIX (100-150)
Instance 3 : VLANs SERVEURS (200-250)
```

### Configuration du Root Bridge

✅ **Configurer Root Primary et Secondary pour chaque instance**  
✅ **Utiliser le même switch comme Root pour toutes les instances** (topologie cohérente)  
✅ **Ou varier les Root Bridges par instance** (load-balancing inter-instances)

**Exemple load-balancing :**
```
Core-SW1 : Root Primary pour Instances 0 et 1
Core-SW2 : Root Primary pour Instances 2 et 3
```

### Déploiement progressif

✅ **Tester MSTP en lab avant production**  
✅ **Migrer progressivement** (commencer par une zone isolée)  
✅ **Documenter tous les changements de configuration**  
✅ **Prévoir une fenêtre de maintenance** (changement de mode STP peut causer une reconvergence)

### Surveillance et maintenance

✅ **Monitorer les changements de topologie** avec SNMP traps/Syslog  
✅ **Vérifier la cohérence de région régulièrement** (`show spanning-tree mst configuration`)  
✅ **Auditer la configuration MST sur tous les switches** (scripts automatisés)  
✅ **Documenter la topologie MST** (diagrammes, instances, mappings)

**💡 Point clé :** La clé du succès avec MSTP est une **planification rigoureuse** et une **cohérence de configuration** sur tous les switches de la région.

---

## 📊 Comparaison finale : PVST+ vs MSTP vs STP

| Critère | STP 802.1D | PVST+ | Rapid-PVST+ | MSTP |
|---------|-----------|-------|-------------|------|
| **Standard** | IEEE 802.1D | Cisco | Cisco/802.1w | IEEE 802.1s |
| **Instances** | 1 (CST) | 1 par VLAN | 1 par VLAN | Multiple (0-64) |
| **Convergence** | ~30-50s | ~30-50s | ~1-2s | ~1-2s |
| **Load-balancing** | ❌ Non | ✅ Par VLAN | ✅ Par VLAN | ✅ Par instance |
| **BPDUs (100 VLANs)** | 1 BPDU/2s | 100 BPDUs/2s | 100 BPDUs/2s | 3-10 BPDUs/2s |
| **Overhead CPU** | Faible | Élevé | Élevé | Faible |
| **Scalabilité** | Faible | Limitée | Limitée | Excellente |
| **Complexité config** | Simple | Moyenne | Moyenne | Élevée |
| **Usage recommandé** | Legacy | Petits réseaux | Réseaux moyens | Grands réseaux |

### Recommandations par taille de réseau

| Taille réseau | VLANs | Recommandation | Justification |
|---------------|-------|----------------|---------------|
| **Petit** | < 50 | Rapid-PVST+ | Simple, efficace, convergence rapide |
| **Moyen** | 50-100 | Rapid-PVST+ ou MSTP | Transition possible vers MSTP si overhead devient problématique |
| **Grand** | > 100 | **MSTP** | Réduction significative overhead, meilleure scalabilité |
| **Data Center** | Variable | **MSTP** | Contrôle fin de la topologie, efficacité maximale |

**💡 Point clé :** Pour les réseaux avec plus de 100 VLANs, MSTP est la solution optimale. Pour les réseaux plus petits, Rapid-PVST+ reste une excellente option grâce à sa simplicité.

---

## 🎯 Points clés à retenir - Module 4

### Limitations de PVST+

- ✅ PVST+ crée 1 instance STP par VLAN → Overhead important (BPDUs, CPU, mémoire)
- ✅ Dans un réseau de 100 VLANs avec 50 switches : **2500 BPDUs par seconde** !
- ✅ Complexité de gestion accrue (configuration Root pour chaque VLAN)

### Concept MSTP

- ✅ **MSTP (IEEE 802.1s)** regroupe plusieurs VLANs dans une même instance STP
- ✅ Réduction drastique du nombre de BPDUs (10x à 100x moins)
- ✅ Convergence rapide (basé sur RSTP 802.1w) : ~1-2 secondes
- ✅ Supporte jusqu'à **65 instances** (0-64)

### Régions MSTP

- ✅ **Région** = Groupe de switches avec config identique (nom, révision, mapping)
- ✅ Trois paramètres de région : **Nom** (32 car), **Révision** (0-65535), **Mapping VLAN-Instance**
- ✅ Cohérence critique : Une seule différence → Switches dans régions différentes
- ✅ Frontière de région : Seul l'IST (Instance 0) est échangé

### Instances MSTP

- ✅ **IST (Instance 0)** : Instance par défaut, obligatoire, interface avec extérieur
- ✅ **MSTI (1-64)** : Instances supplémentaires, optionnelles, regroupent VLANs
- ✅ **CIST** : Combinaison IST (interne) + CST (inter-régions)

### Configuration MSTP

```cisco
! Mode MSTP
spanning-tree mode mst

! Configuration région (IDENTIQUE sur tous les switches)
spanning-tree mst configuration
 name ENTREPRISE_HQ
 revision 1
 instance 1 vlan 10,20,30
 instance 2 vlan 100-199
 exit

! Root Bridges par instance
spanning-tree mst 0 root primary
spanning-tree mst 1 root primary

! Fonctionnalités avancées
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default
```

### Vérification MSTP

```cisco
show spanning-tree mst configuration     ! Config région
show spanning-tree mst                   ! État toutes instances
show spanning-tree mst 1                 ! État instance 1
show spanning-tree mst interface gi0/1   ! Détails port
show spanning-tree summary               ! Résumé
```

### Interopérabilité

- ✅ **MSTP ↔ MSTP (régions différentes)** : Seul IST échangé, MSTI restent internes
- ✅ **MSTP ↔ PVST+** : Frontière détectée, BPDUs PVST+ générés pour VLANs de l'IST
- ✅ **MSTP ↔ STP 802.1D** : Région vue comme un switch unique
- ⚠️ Limitations : MSTI invisibles hors région, load-balancing limité à la frontière

### Meilleures pratiques

- ✅ Planifier rigoureusement le mapping VLAN-Instance
- ✅ Une région unique par site/réseau (cohérence configuration)
- ✅ Limiter à 3-5 instances (suffisant pour la plupart des cas)
- ✅ Incrémenter la révision à chaque modification
- ✅ Documenter la configuration MST (mapping, topologie)
- ✅ Tester en lab avant production

### Choix PVST+ vs MSTP

- ✅ **Rapid-PVST+** : < 50 VLANs, réseau simple, convergence rapide
- ✅ **MSTP** : > 100 VLANs, grand réseau, data center, optimisation overhead
- ✅ Transition recommandée vers MSTP si overhead PVST+ devient problématique

---

## 🚀 Conclusion

Le Multiple Spanning Tree Protocol (MSTP) est la solution optimale pour les grands réseaux d'entreprise avec de nombreux VLANs. Il combine **efficacité** (réduction drastique des BPDUs), **rapidité** (convergence RSTP), et **flexibilité** (load-balancing par instance).

**Avantages clés :**
- Réduction de l'overhead réseau (CPU, bande passante, mémoire)
- Meilleure scalabilité (jusqu'à des milliers de VLANs)
- Convergence rapide (1-2 secondes)
- Contrôle fin de la topologie

**Complexité :**
- Configuration plus élaborée que PVST+
- Nécessite une planification minutieuse
- Cohérence stricte de la région obligatoire

**Dans le prochain module (Module 5),** nous étudierons les **VLAN Trunks et EtherChannel**, qui permettent l'agrégation de liens pour augmenter la bande passante et la redondance, en complément parfait de STP/MSTP.

---

**📚 Fin du Module 4 - Multiple Spanning Tree Protocol (MSTP)**
