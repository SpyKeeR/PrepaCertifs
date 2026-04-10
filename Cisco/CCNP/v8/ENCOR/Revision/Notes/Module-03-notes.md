# Module 3 : Advanced Spanning Tree Tuning
**CCNP ENCOR v8 - Optimisation avancée du Spanning Tree**

---

## 📋 Vue d'ensemble du module

### Objectifs du module
Ce module couvre les fonctionnalités avancées et les mécanismes d'optimisation du Spanning Tree Protocol. Vous apprendrez à accélérer la convergence, à sécuriser votre topologie STP, et à améliorer la disponibilité du réseau grâce à des fonctionnalités comme PortFast, BPDU Guard, Root Guard, et UplinkFast.

### Thèmes principaux
1. **PortFast** - Activation immédiate des ports d'accès
2. **BPDU Guard** - Protection contre les BPDUs indésirables
3. **BPDU Filter** - Filtrage de l'envoi/réception de BPDUs
4. **Root Guard** - Protection de la hiérarchie Root Bridge
5. **Loop Guard** - Protection contre les pertes unidirectionnelles de BPDUs
6. **UplinkFast** - Convergence rapide pour les liens d'accès
7. **BackboneFast** - Convergence rapide pour les liens de backbone
8. **Tuning des timers STP**

---

## ⚡ PortFast

### Problématique

**Situation :** Un PC ou serveur connecté à un port d'accès doit attendre **30-50 secondes** avant de pouvoir communiquer sur le réseau pendant que le port transite par les états STP (Listening → Learning → Forwarding).

**Impact :**
- 🚫 Délai de connexion au réseau
- 🚫 Échec DHCP (timeout avant l'obtention d'une @ IP)
- 🚫 Échec PXE boot (démarrage réseau)
- 🚫 Scripts de démarrage en échec
- 🚫 Mauvaise expérience utilisateur

### Fonctionnement de PortFast

**Concept :** PortFast permet à un port d'**accéder immédiatement à l'état Forwarding**, en contournant les états Listening et Learning.

**Comportement :**
- ✅ Transition directe : **Blocking → Forwarding** en quelques secondes
- ✅ Pas d'attente de 30 secondes
- ✅ Le port reste en écoute des BPDUs (sécurité préservée)
- ⚠️ **À utiliser UNIQUEMENT sur les ports d'accès connectés à des hôtes finaux (PC, serveurs, imprimantes)**

**💡 Point clé :** PortFast ne doit **JAMAIS** être activé sur un port connecté à un autre switch, car cela créerait temporairement une boucle avant que STP ne reconverge.

### Configuration PortFast

#### Configuration par interface

```cisco
interface GigabitEthernet0/5
 description PC-User-01
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 !
 ! Confirmation message :
 ! %Warning: portfast should only be enabled on ports connected to a single
 ! host. Connecting hubs, concentrators, switches, bridges, etc... to this
 ! interface when portfast is enabled, can cause temporary bridging loops.
exit
```

#### Configuration globale pour tous les ports d'accès

```cisco
! Activer PortFast sur TOUS les ports en mode access
spanning-tree portfast default

! Désactiver PortFast sur une interface spécifique
interface gi0/1
 spanning-tree portfast disable
exit
```

**💡 Recommandation :** Utiliser `spanning-tree portfast default` pour activer globalement PortFast sur tous les ports access, puis le désactiver manuellement sur les ports trunk ou uplink.

### Vérification PortFast

```cisco
! Vérifier le statut PortFast
show spanning-tree interface gigabitEthernet 0/5 detail

Port 5 (GigabitEthernet0/5) of VLAN0010 is forwarding
   Port path cost 4, Port priority 128, Port Identifier 128.5.
   Designated root has priority 24586, address 0ce3.e11a.ba00
   Designated bridge has priority 32778, address 0011.2233.4455
   Designated port id is 128.5, designated path cost 4
   Timers: message age 2, forward delay 0, hold 0
   Number of transitions to forwarding state: 1
   The port is in the portfast mode         ← PortFast activé
   Link type is point-to-point by default
   BPDU: sent 156, received 0

! Vérifier la configuration globale
show spanning-tree summary

Switch is in rapid-pvst mode
Root bridge for: VLAN0010
Extended system ID           : enabled
Portfast Default             : enabled     ← PortFast par défaut activé
PortFast BPDU Guard Default  : disabled
Portfast BPDU Filter Default : disabled
```

### Scénarios d'utilisation

| Scénario | PortFast | Raison |
|----------|----------|--------|
| **PC utilisateur** | ✅ Activer | Hôte final, pas de boucle possible |
| **Serveur standalone** | ✅ Activer | Hôte final, besoin de connectivité rapide |
| **Imprimante réseau** | ✅ Activer | Hôte final |
| **Téléphone IP (seul)** | ✅ Activer | Hôte final |
| **PC + Téléphone IP daisy-chain** | ⚠️ Prudence | Risque si le PC est un switch |
| **Port trunk vers switch** | ❌ NE JAMAIS activer | Risque de boucle temporaire |
| **Liaison inter-switch** | ❌ NE JAMAIS activer | Risque majeur de boucle |

**💡 Point clé :** En cas de doute, ne pas activer PortFast. Il vaut mieux attendre 30 secondes que de créer une boucle temporaire dans le réseau.

---

## 🛡️ BPDU Guard

### Problématique

**Situation :** Un port avec PortFast activé reçoit un BPDU (Bridge Protocol Data Unit).

**Causes possibles :**
- Un switch (rogue switch) est connecté par erreur ou malicieusement
- Un hub avec plusieurs périphériques dont un switch
- Un utilisateur connecte son propre switch au réseau
- Configuration erronée d'un port trunk

**Risques :**
- 🚫 Changement de topologie STP non désiré
- 🚫 Nouveau Root Bridge élu par accident
- 🚫 Boucle Layer 2 temporaire
- 🚫 Instabilité du réseau

### Fonctionnement de BPDU Guard

**Concept :** BPDU Guard met **immédiatement** un port en état **err-disabled** dès qu'il reçoit un BPDU.

**Comportement :**
1. Le port avec PortFast + BPDU Guard reçoit un BPDU
2. Le switch détecte une anomalie (un hôte final ne devrait jamais envoyer de BPDU)
3. Le port est placé en état **err-disabled** instantanément
4. Le trafic est coupé sur ce port
5. Une alerte SNMP/Syslog est générée
6. **Intervention manuelle requise** pour réactiver le port

**💡 Point clé :** BPDU Guard est un mécanisme de sécurité proactif qui protège le réseau contre les connexions incorrectes de switches.

### Configuration BPDU Guard

#### Méthode 1 : Par interface (recommandée pour un contrôle fin)

```cisco
interface GigabitEthernet0/5
 description PC-User-01
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
exit
```

#### Méthode 2 : Globalement (recommandée pour tous les ports PortFast)

```cisco
! Activer BPDU Guard globalement sur tous les ports PortFast
spanning-tree portfast bpduguard default

! Cette commande active BPDU Guard automatiquement sur tous les ports
! où PortFast est activé (via portfast ou portfast default)
```

**💡 Meilleure pratique :** Utiliser `spanning-tree portfast bpduguard default` pour protéger automatiquement tous les ports d'accès.

### Vérification BPDU Guard

```cisco
! Vérifier le statut BPDU Guard
show spanning-tree interface gigabitEthernet 0/5 detail

Port 5 (GigabitEthernet0/5) of VLAN0010 is forwarding
   ...
   The port is in the portfast mode
   Bpdu guard is enabled                    ← BPDU Guard activé
   Link type is point-to-point by default

! Vérifier la configuration globale
show spanning-tree summary

Portfast Default             : enabled
PortFast BPDU Guard Default  : enabled     ← BPDU Guard par défaut activé

! Vérifier les ports en err-disabled
show interfaces status err-disabled

Port      Name               Status       Reason               Err-disabled Vlans
Gi0/5     PC-User-01         err-disabled bpduguard            
```

### Récupération d'un port en err-disabled

**Option 1 : Récupération manuelle**
```cisco
interface GigabitEthernet0/5
 shutdown
 ! Attendre quelques secondes
 no shutdown
exit
```

**Option 2 : Récupération automatique (errdisable recovery)**
```cisco
! Activer la récupération automatique pour bpduguard
errdisable recovery cause bpduguard

! Définir le délai de récupération (par défaut 300 secondes)
errdisable recovery interval 600

! Vérifier la configuration
show errdisable recovery

ErrDisable Reason            Timer Status
-----------------            --------------
bpduguard                    Enabled
...

Timer interval: 600 seconds
```

**⚠️ Attention :** La récupération automatique doit être utilisée avec précaution. Si le problème (switch branché) persiste, le port sera désactivé à nouveau en boucle.

### Scénarios BPDU Guard

```
Scénario 1 : Utilisation normale
[Switch]─────[Gi0/5 PortFast+BPDU Guard]─────[PC]
✅ Aucun BPDU reçu, port opérationnel

Scénario 2 : Switch branché par erreur
[Switch]─────[Gi0/5 PortFast+BPDU Guard]─────[Rogue Switch]
                                                    ↓ Envoie BPDU
❌ Port Gi0/5 passe en err-disabled immédiatement
```

**💡 Point clé :** BPDU Guard + PortFast est la combinaison de sécurité standard pour tous les ports d'accès dans un réseau d'entreprise.

---

## 🔇 BPDU Filter

### Différence entre BPDU Guard et BPDU Filter

| Fonctionnalité | BPDU Guard | BPDU Filter |
|----------------|-----------|-------------|
| **Action si BPDU reçu** | Port en err-disabled | Ignore le BPDU |
| **Envoi de BPDUs** | Continue d'envoyer | Arrête d'envoyer |
| **Usage typique** | Ports d'accès (sécurité) | Cas très spécifiques |
| **Recommandé** | ✅ Oui | ⚠️ Rare |

### Fonctionnement de BPDU Filter

**BPDU Filter** empêche un port d'**envoyer** et de **recevoir** des BPDUs.

**Deux modes de configuration :**

#### Mode 1 : Global (sur tous les ports PortFast)

**Comportement :**
- Le port **arrête d'envoyer** des BPDUs tant qu'il ne reçoit aucun BPDU
- **Si le port reçoit un BPDU**, BPDU Filter est **désactivé automatiquement** et le port redevient un port STP normal
- Mécanisme de protection : si un switch est connecté, STP reprend le contrôle

```cisco
! Activer BPDU Filter globalement sur tous les ports PortFast
spanning-tree portfast bpdufilter default
```

**💡 Point clé (mode global) :** BPDU Filter se désactive automatiquement si un BPDU est reçu, permettant à STP de reprendre le contrôle. C'est un mécanisme relativement sûr.

#### Mode 2 : Par interface (dangereux)

**Comportement :**
- Le port **ignore complètement STP** (n'envoie ni ne reçoit de BPDUs)
- **Même si un BPDU est reçu**, il est ignoré
- Le port reste en Forwarding quoi qu'il arrive
- **⚠️ Très dangereux : risque de boucle Layer 2 !**

```cisco
interface GigabitEthernet0/5
 spanning-tree bpdufilter enable
exit
```

**⚠️ DANGER :** Cette configuration empêche complètement STP de fonctionner sur le port. Si un switch est connecté, une boucle Layer 2 sera créée.

### Cas d'utilisation de BPDU Filter

**Cas légitimes (rares) :**
1. **Connexion à un équipement qui génère des BPDUs invalides**
   - Certains équipements anciens ou mal configurés envoient des BPDUs malformés
   - BPDU Filter peut éviter des reconvergences STP intempestives

2. **Tests et démonstrations**
   - Environnement de lab pour simuler des topologies sans interférence STP

3. **Interconnexion avec un réseau externe non contrôlé**
   - Cas très spécifique où l'on veut isoler STP entre deux domaines

**💡 Recommandation :** **Éviter BPDU Filter en mode interface dans les réseaux de production**. Préférer BPDU Guard qui offre une protection sans désactiver complètement STP.

### Vérification BPDU Filter

```cisco
! Vérifier la configuration globale
show spanning-tree summary

Portfast BPDU Filter Default : enabled     ← BPDU Filter par défaut activé

! Vérifier sur une interface
show spanning-tree interface gigabitEthernet 0/5 detail

Port 5 (GigabitEthernet0/5) of VLAN0010 is forwarding
   ...
   The port is in the portfast mode
   Bpdu filter is enabled                   ← BPDU Filter activé
```

**💡 Point clé :** BPDU Filter doit être utilisé avec une extrême prudence. Dans 99% des cas, **BPDU Guard est la solution appropriée** pour les ports d'accès.

---

## 🔒 Root Guard

### Problématique

**Situation :** Un switch avec une priorité plus basse (ou MAC plus basse) est ajouté au réseau sur un port de distribution ou d'accès.

**Conséquence :**
- Ce nouveau switch devient le **Root Bridge** par défaut (élection STP normale)
- La topologie STP change complètement
- Le trafic est redirigé de manière non optimale
-  Les chemins de communication sont modifiés de façon imprévisible

**Exemple :**
```
Topologie planifiée :
    [Core-SW] ← Root Bridge planifié
      /    \
  [Dist1]  [Dist2]
     |
  [Access-SW]

Après ajout d'un switch avec MAC basse :
  [Core-SW]
      |
   [Dist1]------[New-SW] ← Devient Root par accident !
                   |
                [Dist2]
                   |
                [Access-SW]

Topologie STP complètement changée !
```

### Fonctionnement de Root Guard

**Concept :** Root Guard empêche un port de devenir **Root Port**. Si un BPDU "supérieur" (indiquant un meilleur Root Bridge) est reçu sur un port avec Root Guard, le port est placé en état **root-inconsistent** (bloqué).

**Comportement :**
1. Le port reçoit un BPDU annonçant un Bridge ID inférieur au Root actuel
2. Root Guard détecte que ce port voudrait devenir Root Port
3. Le port est placé en état **root-inconsistent** (équivalent à Blocking)
4. Le trafic est bloqué sur ce port
5. **Dès que les BPDUs "supérieurs" cessent**, le port reprend automatiquement l'état Forwarding

**💡 Point clé :** Contrairement à BPDU Guard (err-disabled permanent), Root Guard bloque temporairement le port et le récupère automatiquement dès que le problème disparaît.

### Configuration Root Guard

**À configurer sur les ports vers la périphérie du réseau (Designated Ports).**

```cisco
! Sur un switch Core ou Distribution
interface GigabitEthernet0/10
 description Lien vers Access-SW
 spanning-tree guard root
exit

! Peut être configuré sur plusieurs ports
interface range GigabitEthernet0/1 - 12
 description Liaisons vers Access Layer
 spanning-tree guard root
exit
```

**💡 Recommandation :** Activer Root Guard sur tous les **Designated Ports** qui pointent vers les switches de distribution et d'accès pour protéger la hiérarchie du Root Bridge.

### Vérification Root Guard

```cisco
! Vérifier Root Guard sur une interface
show spanning-tree interface gigabitEthernet 0/10 detail

Port 10 (GigabitEthernet0/10) of VLAN0010 is forwarding
   ...
   Root guard is enabled on the port        ← Root Guard activé

! Vérifier les ports en état root-inconsistent
show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             GigabitEthernet0/10    Root Inconsistent

Number of inconsistent ports (segments) in the system : 1

! Afficher les détails d'un port inconsistent
show spanning-tree vlan 10

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/10              Desg BKN*4         128.10   P2p *ROOT_Inc
                         ^^^                         ^^^^^^^^
                      Broken/Blocked              Root Inconsistent
```

### Récupération automatique

**Root Guard se récupère automatiquement :**
- Dès que le switch "rogue" est déconnecté
- Ou dès que sa priorité est augmentée pour ne plus être supérieure au Root actuel
- Le port passe de root-inconsistent à Forwarding automatiquement

**Pas d'intervention manuelle nécessaire** (contrairement à BPDU Guard).

### Placement de Root Guard dans la topologie

```
          [Core-SW] ← Root Bridge
          /        \
         /          \
    [Dist1]        [Dist2]
   Root Guard     Root Guard
   activé ↓       activé ↓
     [Access-SW]  [Access-SW]
     Root Guard   Root Guard
     activé ↓     activé ↓
       [PC]         [PC]

Root Guard sur tous les Designated Ports tournés vers la périphérie
```

**💡 Point clé :** Root Guard protège la hiérarchie STP en empêchant les switches périphériques de devenir Root Bridge. Toujours l'activer sur les ports Designated qui pointent "vers le bas" dans la hiérarchie.

---

## 🔁 Loop Guard

### Problématique : Perte unidirectionnelle de BPDUs

**Situation :** Un lien perd la capacité de transmettre des BPDUs dans une direction, mais reste physiquement up.

**Causes possibles :**
- Défaillance d'un émetteur optique (SFP) dans une direction
- Problème de câblage unilatéral
- Bug logiciel sur un switch

**Scénario :**
```
     [Root Bridge]
          |
      Gi0/1 (DP) ──────┐
          |             │ BPDUs envoyés ↓
          ↓             │
      Gi0/1 (RP)        X BPDUs ne remontent plus ↑
       [Switch A]       │ (lien unidirectionnel)
          |             │
      Gi0/2 (Altn/BLK) ─┘

Problème :
1. Switch A ne reçoit plus de BPDUs sur Gi0/1 (Root Port)
2. Après Max Age (20s), le BPDU expire
3. Switch A pense que le Root est perdu
4. Gi0/2 (précédemment Alternate) passe en Designated et Forwarding
5. BOUCLE créée ! (Gi0/1 et Gi0/2 forwardent tous les deux)
```

**Conséquence :** Création d'une **boucle Layer 2** alors que le lien est physiquement up.

### Fonctionnement de Loop Guard

**Concept :** Loop Guard empêche un port Alternate/Blocked de passer en Forwarding s'il cesse de recevoir des BPDUs.

**Comportement normal (sans Loop Guard) :**
```
Port Alternate/Blocked ne reçoit plus de BPDUs
  → Après Max Age (20s)
  → Port devient Designated et passe en Forwarding
  → RISQUE DE BOUCLE
```

**Comportement avec Loop Guard :**
```
Port Alternate/Blocked ne reçoit plus de BPDUs
  → Loop Guard détecte l'anomalie
  → Port placé en état loop-inconsistent (bloqué)
  → Pas de transition vers Forwarding
  → PAS DE BOUCLE
  → Récupération automatique dès réception de BPDUs
```

**💡 Point clé :** Loop Guard protège contre les boucles causées par une perte unidirectionnelle de BPDUs.

### Configuration Loop Guard

#### Option 1 : Global (recommandée)

```cisco
! Activer Loop Guard globalement sur tous les ports point-to-point non-edge
spanning-tree loopguard default
```

**Comportement global :**
- Loop Guard est activé automatiquement sur tous les ports :
  - **Point-to-point** (liaison switch-to-switch)
  - **Non-PortFast** (pas des ports d'accès)
- Ne s'applique pas aux ports d'accès avec PortFast

#### Option 2 : Par interface

```cisco
interface GigabitEthernet0/2
 description Lien vers Switch B (backup link)
 spanning-tree guard loop
exit
```

### Vérification Loop Guard

```cisco
! Vérifier la configuration globale
show spanning-tree summary

Loopguard Default            : enabled     ← Loop Guard global activé

! Vérifier sur une interface
show spanning-tree interface gigabitEthernet 0/2 detail

Port 2 (GigabitEthernet0/2) of VLAN0010 is alternate blocking
   ...
   Loop guard is enabled on the port        ← Loop Guard activé

! Vérifier les ports en état loop-inconsistent
show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             GigabitEthernet0/2     Loop Inconsistent

! Afficher les détails d'un port loop-inconsistent
show spanning-tree vlan 10

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/2               Altn BKN*4         128.2    P2p *LOOP_Inc
                         ^^^                         ^^^^^^^^
                      Broken/Blocked              Loop Inconsistent
```

### Récupération automatique

**Loop Guard se récupère automatiquement :**
- Dès que les BPDUs sont à nouveau reçus sur le port
- Le port passe de loop-inconsistent à son rôle STP normal (généralement Alternate)
- Pas d'intervention manuelle nécessaire

### Loop Guard vs Root Guard

| Caractéristique | Loop Guard | Root Guard |
|-----------------|-----------|-----------|
| **Protège contre** | Perte unidirectionnelle de BPDUs | Périphérique devenant Root |
| **Port affecté** | Alternate/Blocked Ports | Designated Ports |
| **État d'erreur** | loop-inconsistent | root-inconsistent |
| **Placement** | Sur tous les ports non-PortFast | Sur les DP vers périphérie |
| **Récupération** | Automatique | Automatique |

**💡 Point clé :** Loop Guard et Root Guard sont complémentaires. Loop Guard protège les ports Alternate, Root Guard protège les ports Designated. Les deux peuvent être activés simultanément dans le réseau.

---

## 🚀 UplinkFast

### Problématique

**Situation :** Un switch d'accès a deux liens vers le réseau (redondance), un Root Port (actif) et un Alternate Port (bloqué).

**Scénario de panne :**
```
     [Distribution Switch]
          |         |
       Gi0/1     Gi0/2
       (DP)      (DP)
          |         |
       Gi0/1     Gi0/2
       (RP)      (Altn)
      [Access Switch]

Panne du lien Gi0/1 (Root Port)
  → STP doit reconverger
  → Gi0/2 doit passer de Alternate à Root Port
  → Convergence normale = 30-50 secondes (Max Age + Listening + Learning)
```

**Impact :**
- Interruption de 30-50 secondes pour les utilisateurs
- Perte de connectivité des PC/serveurs connectés au switch d'accès

### Fonctionnement de UplinkFast

**Concept :** UplinkFast permet une convergence **quasi-instantanée** (1-2 secondes) lorsque le Root Port tombe, en activant immédiatement l'Alternate Port.

**Mécanisme :**
1. Le switch maintient une **liste de ports Alternate** (backup uplinks)
2. Lorsque le Root Port tombe, UplinkFast active immédiatement un Alternate Port
3. Transition directe vers Forwarding (bypass Listening/Learning)
4. Convergence en **environ 1 seconde**

**Fonctionnalités supplémentaires :**
- **Mise à jour de la table MAC :** Envoie des "dummy multicast frames" pour forcer les switches amont à réapprendre les MACs via le nouveau chemin
- **Prévention de Root Bridge :** Augmente la Bridge Priority à 49152 pour éviter que ce switch devienne Root

**💡 Point clé :** UplinkFast est conçu pour les switches d'**accès** avec des liens redondants vers la distribution. Ne pas l'utiliser sur les switches Core/Distribution.

### Configuration UplinkFast

```cisco
! Activer UplinkFast (commande globale)
spanning-tree uplinkfast

! Vérifier la configuration
show spanning-tree summary

UplinkFast                   : enabled     ← UplinkFast activé

! Vérifier la nouvelle priorité
show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             Cost        4
             Port        1 (GigabitEthernet0/1)

  Bridge ID  Priority    49162 (priority 49152 sys-id-ext 10)
             ^^^^^
          Augmenté automatiquement à 49152
```

**Effets de la commande `spanning-tree uplinkfast` :**

1. **Augmentation de la Bridge Priority à 49152**
   - Empêche ce switch de devenir Root Bridge

2. **Augmentation du Path Cost des ports à +3000**
   - Fait en sorte que ce switch ne devienne pas un chemin préféré pour les autres switches

3. **Activation de la convergence rapide**
   - Transition immédiate Alternate → Forwarding en cas de panne du Root Port

### Cas d'utilisation UplinkFast

**✅ À utiliser sur :**
- Switches d'accès (Access Layer)
- Switches avec exactement 2 uplinks vers la distribution (1 RP + 1 Alternate)

**❌ Ne PAS utiliser sur :**
- Root Bridge
- Switches Core ou Distribution
- Switches avec plus de 2 uplinks
- Toute topologie complexe

**💡 Point clé :** UplinkFast est spécifiquement conçu pour les switches d'accès à double uplink. L'utiliser ailleurs peut causer des problèmes de topologie STP.

### Remarque : UplinkFast vs RSTP

**UplinkFast est **obsolète** avec Rapid-PVST+ (RSTP) :**
- RSTP converge naturellement en 1-2 secondes (même performance qu'UplinkFast)
- RSTP ne modifie pas la Bridge Priority ni les Path Costs
- RSTP fonctionne sur tous les types de switches

**Recommandation moderne :**
```cisco
! Préférer Rapid-PVST+ au lieu d'UplinkFast
spanning-tree mode rapid-pvst
```

**💡 Point clé :** Dans les réseaux modernes, utilisez **Rapid-PVST+** au lieu d'UplinkFast. UplinkFast est maintenu uniquement pour la compatibilité legacy.

---

## 🔗 BackboneFast

### Problématique : Panne indirecte

**Situation :** Un lien tombe dans le backbone/core du réseau, mais pas directement connecté au switch qui doit reconverger.

**Scénario :**
```
        [Root Bridge]
             |
          Gi0/1 (DP)
             |
          Gi0/1 (RP)
         [Switch A]
          /      \
     Gi0/2      Gi0/3
     (DP)       (DP)
      /            \
  Gi0/1          Gi0/1
  (RP)           (RP)
[Switch B]      [Switch C]
    |               |
  Gi0/2           Gi0/2
  (Altn)          (Altn)
    |               |
    +-------+-------+
            |
       Panne du lien Root - Switch A

Sans BackboneFast :
  → Switch B reçoit un BPDU "inférieur" de Switch C via Gi0/2
  → Doit attendre Max Age (20s) avant de considérer le BPDU comme invalide
  → Convergence totale = 20s (Max Age) + 30s (Listening+Learning) = 50s
```

**Problème :** En cas de panne **indirecte** (dans le backbone), un switch doit attendre l'expiration du Max Age (20s) avant d'accepter un nouveau chemin, même si un BPDU indiquant une meilleure route arrive.

### Fonctionnement de BackboneFast

**Concept :** BackboneFast permet de réduire le délai de convergence de **50 secondes à 30 secondes** en cas de panne indirecte.

**Mécanisme :**
1. Un switch reçoit un BPDU "inférieur" sur un port Alternate/Blocked
2. Le switch détecte que le Root Bridge a potentiellement changé
3. BackboneFast envoie une requête **RLQ (Root Link Query)** pour vérifier si le Root est vraiment perdu
4. Si confirmé, le switch **expire immédiatement** les BPDUs (sans attendre Max Age)
5. Convergence réduite à **30 secondes** (Listening 15s + Learning 15s)

**Gain :** 20 secondes économisées (Max Age bypassed).

**💡 Point clé :** BackboneFast réduit le Max Age de 20s en cas de panne indirecte, mais les états Listening/Learning (30s) restent nécessaires en STP 802.1D.

### Configuration BackboneFast

```cisco
! Activer BackboneFast (commande globale)
spanning-tree backbonefast

! ⚠️ DOIT être activé sur TOUS les switches du réseau pour fonctionner !

! Vérifier la configuration
show spanning-tree summary

BackboneFast                 : enabled     ← BackboneFast activé
```

**💡 Important :** BackboneFast doit être activé sur **tous les switches** du domaine STP pour fonctionner correctement. Si un seul switch n'a pas BackboneFast, la convergence sera ralentie.

### Cas d'utilisation BackboneFast

**✅ À utiliser sur :**
- Tous les switches dans un réseau STP 802.1D (PVST+)

**❌ Inutile avec :**
- Rapid-PVST+ (RSTP)
- MSTP

### Remarque : BackboneFast vs RSTP

**BackboneFast est **obsolète** avec RSTP :**
- RSTP converge en 1-2 secondes pour tous les types de pannes (directes et indirectes)
- Pas besoin de mécanisme spécial comme BackboneFast
- RSTP utilise le mécanisme de **proposal/agreement** pour une convergence ultra-rapide

**Recommandation moderne :**
```cisco
! Préférer Rapid-PVST+ au lieu de BackboneFast
spanning-tree mode rapid-pvst
```

**💡 Point clé :** BackboneFast est une fonctionnalité legacy pour STP 802.1D. Dans les réseaux modernes, utilisez **Rapid-PVST+** qui rend BackboneFast obsolète.

---

## ⏱️ Tuning des timers STP

### Objectifs du tuning

**Pourquoi ajuster les timers STP ?**
- Accélérer la convergence (au prix de la stabilité)
- Adapter STP à la taille du réseau
- Optimiser pour des topologies spécifiques

**⚠️ Avertissement :** Modifier les timers STP peut rendre le réseau **instable** si mal configuré. Toujours effectuer des tests avant de déployer en production.

### Les 3 timers ajustables

| Timer | Valeur défaut | Plage | Impact si diminué | Impact si augmenté |
|-------|--------------|-------|-------------------|-------------------|
| **Hello Time** | 2s | 1-10s | Détection rapide, plus de BPDUs | Détection lente, moins de BPDUs |
| **Forward Delay** | 15s | 4-30s | Convergence rapide, risque boucle | Convergence lente, sécurité accrue |
| **Max Age** | 20s | 6-40s | Détection rapide, risque faux positif | Détection lente, stabilité accrue |

### Contraintes mathématiques

**IEEE 802.1D impose des relations obligatoires :**

```
1. Max Age ≥ 2 × (Hello Time + 1)
2. Max Age ≤ 2 × (Forward Delay - 1)
```

**Exemple de vérification :**
```
Hello Time = 2s
Forward Delay = 15s
Max Age = 20s

Vérification 1: 20 ≥ 2 × (2 + 1) = 6  ✅
Vérification 2: 20 ≤ 2 × (15 - 1) = 28 ✅

Configuration valide !
```

### Configuration des timers

**⚠️ À configurer UNIQUEMENT sur le Root Bridge !**

```cisco
! Modifier Hello Time (1-10 secondes)
CoreSW(config)# spanning-tree vlan 10 hello-time 1

! Modifier Forward Delay (4-30 secondes)
CoreSW(config)# spanning-tree vlan 10 forward-time 10

! Modifier Max Age (6-40 secondes)
CoreSW(config)# spanning-tree vlan 10 max-age 15

! Vérifier les timers
CoreSW# show spanning-tree vlan 10

VLAN0010
  Spanning tree enabled protocol rstp
  Root ID    Priority    24586
             Address     0ce3.e11a.ba00
             This bridge is the root
             Hello Time   1 sec  Max Age 15 sec  Forward Delay 10 sec
                          ^^^^^          ^^^^^                ^^^^^
                          Modifié       Modifié              Modifié
```

### Configuration avec diameter (Cisco)

**Cisco propose une méthode simplifiée basée sur le diamètre du réseau :**

```cisco
! Diamètre = nombre maximum de switches entre deux extrémités du réseau
spanning-tree vlan 10 root primary diameter 4

! Cisco calcule automatiquement les timers optimaux
```

**Calcul automatique selon le diamètre :**

| Diameter | Hello Time | Forward Delay | Max Age |
|----------|-----------|---------------|---------|
| 2 | 2s | 15s | 20s (défaut) |
| 3 | 2s | 15s | 20s |
| 4 | 2s | 15s | 20s |
| 5 | 2s | 15s | 22s |
| 6 | 2s | 15s | 24s |
| 7 | 2s | 15s | 26s |

**💡 Point clé :** Le paramètre diameter ajuste principalement Max Age pour s'adapter au nombre de sauts entre switches.

### Exemples de tuning

#### Exemple 1 : Réseau petit et rapide (aggressive tuning)

**Contexte :** 3 switches, liens Gigabit, besoin de convergence rapide

```cisco
! Sur le Root Bridge
spanning-tree vlan 10 hello-time 1
spanning-tree vlan 10 forward-time 10
spanning-tree vlan 10 max-age 12

! Convergence = 20 secondes (au lieu de 30s)
! Risque : Moins de tolérance aux pertes de BPDUs
```

#### Exemple 2 : Réseau large et stable (conservative tuning)

**Contexte :** 15 switches, plusieurs sites, liens WAN, stabilité prioritaire

```cisco
! Sur le Root Bridge
spanning-tree vlan 10 hello-time 3
spanning-tree vlan 10 forward-time 20
spanning-tree vlan 10 max-age 30

! Convergence = 40 secondes (plus lente mais plus stable)
! Avantage : Tolérance élevée aux pertes de BPDUs
```

### Meilleures pratiques pour le tuning

**✅ Recommandations :**
1. **Ne modifier les timers que si nécessaire** (les valeurs par défaut conviennent dans 90% des cas)
2. **Toujours configurer sur le Root Bridge uniquement**
3. **Tester en lab avant déploiement en production**
4. **Respecter les contraintes mathématiques**
5. **Documenter les changements**
6. **Préférer Rapid-PVST+ au lieu de tuner STP 802.1D**

**❌ À éviter :**
1. Diminuer Forward Delay en dessous de 10s (risque de boucles temporaires)
2. Diminuer Max Age en dessous de 10s (risque de faux positifs)
3. Modifier les timers sur des switches non-root (seront ignorés)

**💡 Point clé :** La meilleure optimisation STP n'est pas de tuner les timers 802.1D, mais de passer à **Rapid-PVST+** qui converge naturellement en 1-2 secondes sans risque de déstabilisation.

---

## 🔧 Tableau récapitulatif des fonctionnalités avancées

| Fonctionnalité | Objectif | Port concerné | Action si déclenchée | Récupération | Usage recommandé |
|----------------|----------|---------------|---------------------|--------------|------------------|
| **PortFast** | Convergence rapide hôtes | Ports d'accès | Forwarding immédiat | N/A | ✅ Tous ports accès |
| **BPDU Guard** | Sécurité contre rogue switch | Ports PortFast | err-disabled | Manuelle | ✅ Tous ports accès |
| **BPDU Filter** | Bloquer envoi/réception BPDUs | Cas spécifiques | Ignore BPDUs | N/A | ⚠️ Rare, dangereux |
| **Root Guard** | Protéger hiérarchie Root | Designated Ports | root-inconsistent | Automatique | ✅ DP vers périphérie |
| **Loop Guard** | Prévenir boucles unidirectionnelles | Alternate Ports | loop-inconsistent | Automatique | ✅ Tous ports non-PortFast |
| **UplinkFast** | Convergence rapide accès | Switches d'accès | Failover 1-2s | N/A | ⚠️ Legacy (utiliser RSTP) |
| **BackboneFast** | Convergence rapide indirect | Tous switches | Réduit Max Age | N/A | ⚠️ Legacy (utiliser RSTP) |

---

## 💡 Configuration recommandée pour un réseau moderne

### Switch Core (Root Bridge)

```cisco
hostname CoreSW

! Mode Rapid-PVST+ (préféré)
spanning-tree mode rapid-pvst

! Configurer comme Root Primary
spanning-tree vlan 10,20,30 root primary

! Activer Loop Guard globalement
spanning-tree loopguard default

! Root Guard sur les ports vers distribution (optionnel, pour sécurité)
interface range GigabitEthernet0/1 - 4
 description Liens vers Distribution Layer
 spanning-tree guard root
exit
```

### Switch Distribution (Root Secondary)

```cisco
hostname DistribSW

! Mode Rapid-PVST+
spanning-tree mode rapid-pvst

! Configurer comme Root Secondary
spanning-tree vlan 10,20,30 root secondary

! Loop Guard global
spanning-tree loopguard default

! Root Guard sur les ports vers accès
interface range GigabitEthernet0/10 - 24
 description Liens vers Access Layer
 spanning-tree guard root
exit
```

### Switch Access

```cisco
hostname AccessSW

! Mode Rapid-PVST+
spanning-tree mode rapid-pvst

! PortFast et BPDU Guard sur tous les ports d'accès
spanning-tree portfast default
spanning-tree portfast bpduguard default

! Loop Guard global
spanning-tree loopguard default

! Configuration des ports d'accès
interface range FastEthernet0/1 - 24
 description User Ports
 switchport mode access
 switchport access vlan 10
 ! PortFast et BPDU Guard activés automatiquement grâce aux commandes globales
exit

! Désactiver PortFast sur les uplinks
interface range GigabitEthernet0/1 - 2
 description Uplinks vers Distribution
 spanning-tree portfast disable
exit
```

**💡 Point clé :** Cette configuration combine **Rapid-PVST+** pour la convergence rapide, **PortFast + BPDU Guard** pour la sécurité des ports d'accès, **Root Guard** pour protéger la hiérarchie, et **Loop Guard** pour prévenir les boucles unidirectionnelles.

---

## 🔍 Commandes de vérification

### Vérifier l'état des fonctionnalités avancées

```cisco
! Vue d'ensemble de toutes les fonctionnalités
show spanning-tree summary

Switch is in rapid-pvst mode
Root bridge for: VLAN0010, VLAN0020
Extended system ID           : enabled
Portfast Default             : enabled
PortFast BPDU Guard Default  : enabled
Portfast BPDU Filter Default : disabled
Loopguard Default            : enabled
EtherChannel misconfig guard : enabled
UplinkFast                   : disabled
BackboneFast                 : disabled

! Vérifier les ports inconsistants
show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             Gi0/5                  Root Inconsistent
VLAN0020             Gi0/10                 Loop Inconsistent

! Vérifier un port spécifique
show spanning-tree interface gigabitEthernet 0/5 detail

Port 5 (GigabitEthernet0/5) of VLAN0010 is forwarding
   ...
   The port is in the portfast mode
   Bpdu guard is enabled
   Root guard is enabled on the port

! Vérifier les ports err-disabled
show interfaces status err-disabled

Port      Name               Status       Reason               Err-disabled Vlans
Gi0/8     PC-User-03         err-disabled bpduguard            

! Vérifier les timers STP
show spanning-tree vlan 10 | include Time

Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
```

---

## 🎯 Points clés à retenir - Module 3

### PortFast

- ✅ **Rôle :** Accès immédiat à l'état Forwarding pour les ports d'accès (bypass Listening/Learning)
- ✅ **Usage :** Ports connectés à des hôtes finaux (PC, serveurs, imprimantes)
- ✅ **Configuration :** `spanning-tree portfast` (interface) ou `spanning-tree portfast default` (global)
- ⚠️ **JAMAIS sur un port trunk ou vers un switch** (risque de boucle temporaire)

### BPDU Guard

- ✅ **Rôle :** Sécurité contre les switches indésirables (rogue switches)
- ✅ **Action :** Met le port en err-disabled si un BPDU est reçu
- ✅ **Configuration :** `spanning-tree bpduguard enable` (interface) ou `spanning-tree portfast bpduguard default` (global)
- ✅ **Récupération :** Manuelle (`shutdown` / `no shutdown`) ou automatique (`errdisable recovery`)
- ✅ **Meilleure pratique :** Toujours activer avec PortFast sur les ports d'accès

### BPDU Filter

- ⚠️ **Rôle :** Bloquer l'envoi/réception de BPDUs (dangereux)
- ⚠️ **Mode global :** Se désactive automatiquement si BPDU reçu (relativement sûr)
- ⚠️ **Mode interface :** Ignore complètement STP (très dangereux, risque de boucle)
- ⚠️ **Usage :** Très rare, cas spécifiques uniquement
- ✅ **Préférer BPDU Guard** dans 99% des cas

### Root Guard

- ✅ **Rôle :** Empêcher un port de devenir Root Port (protège la hiérarchie du Root Bridge)
- ✅ **Placement :** Sur les Designated Ports pointant vers la périphérie
- ✅ **Action :** Met le port en root-inconsistent si un BPDU "supérieur" est reçu
- ✅ **Récupération :** Automatique dès que les BPDUs indésirables cessent
- ✅ **Configuration :** `spanning-tree guard root` (interface)

### Loop Guard

- ✅ **Rôle :** Prévenir les boucles causées par une perte unidirectionnelle de BPDUs
- ✅ **Placement :** Sur les ports Alternate/Blocked (point-to-point non-PortFast)
- ✅ **Action :** Met le port en loop-inconsistent s'il cesse de recevoir des BPDUs
- ✅ **Récupération :** Automatique dès réception de BPDUs
- ✅ **Configuration :** `spanning-tree loopguard default` (global recommandé)

### UplinkFast & BackboneFast (Legacy)

- ⚠️ **UplinkFast :** Convergence rapide pour switches d'accès (1-2s) — **Obsolète avec RSTP**
- ⚠️ **BackboneFast :** Réduit Max Age en cas de panne indirecte — **Obsolète avec RSTP**
- ✅ **Recommandation moderne :** Utiliser **Rapid-PVST+** qui rend ces fonctionnalités inutiles

### Tuning des timers

- ✅ **Timers :** Hello Time (2s), Forward Delay (15s), Max Age (20s)
- ✅ **Configuration :** Sur le Root Bridge uniquement
- ✅ **Contraintes :** `Max Age ≥ 2 × (Hello + 1)` et `Max Age ≤ 2 × (Forward Delay - 1)`
- ⚠️ **Prudence :** Modifier les timers peut déstabiliser le réseau
- ✅ **Meilleure approche :** Utiliser Rapid-PVST+ au lieu de tuner STP 802.1D

### Configuration recommandée moderne

```cisco
! Activer Rapid-PVST+
spanning-tree mode rapid-pvst

! Root Primary/Secondary
spanning-tree vlan 10,20,30 root primary
spanning-tree vlan 10,20,30 root secondary

! PortFast + BPDU Guard sur tous les ports d'accès
spanning-tree portfast default
spanning-tree portfast bpduguard default

! Loop Guard global
spanning-tree loopguard default

! Root Guard sur les DP vers périphérie
interface gi0/10
 spanning-tree guard root
exit
```

---

## 🚀 Conclusion

Les fonctionnalités avancées de Spanning Tree permettent d'**optimiser la convergence**, de **sécuriser la topologie**, et d'**améliorer la disponibilité** du réseau Layer 2.

**Fonctionnalités essentielles pour un réseau de production :**
1. **PortFast + BPDU Guard** (ports d'accès) : Convergence rapide et sécurité
2. **Root Guard** (Designated Ports) : Protection de la hiérarchie
3. **Loop Guard** (ports non-PortFast) : Prévention des boucles unidirectionnelles
4. **Rapid-PVST+** (au lieu de 802.1D) : Convergence globale rapide (1-2s)

**Dans le prochain module (Module 4),** nous étudierons le **Multiple Spanning Tree Protocol (MSTP)**, qui permet de réduire l'overhead de PVST+ en regroupant plusieurs VLANs dans une même instance STP, tout en maintenant la convergence rapide de RSTP.

---

**📚 Fin du Module 3 - Advanced Spanning Tree Tuning**
