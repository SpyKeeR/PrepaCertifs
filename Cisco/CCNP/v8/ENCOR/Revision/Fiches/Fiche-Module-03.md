# Fiche de révision - Module 3 : Advanced Spanning Tree Tuning
**CCNP ENCOR v8 - Optimisation avancée du Spanning Tree**

---

## 🎯 Vue d'ensemble des fonctionnalités

| Fonctionnalité | Objectif | Port concerné | Action | Récupération |
|----------------|----------|---------------|--------|--------------|
| **PortFast** | Forwarding immédiat | Ports accès | Bypass Listening/Learning | N/A |
| **BPDU Guard** | Sécurité rogue switch | Ports PortFast | err-disabled | Manuelle |
| **BPDU Filter** | Bloquer BPDUs | Cas spécifiques | Ignore BPDUs | N/A |
| **Root Guard** | Protéger hiérarchie Root | Designated Ports | root-inconsistent | Auto |
| **Loop Guard** | Prévenir boucles unidirectionnelles | Alternate Ports | loop-inconsistent | Auto |
| **UplinkFast** | Convergence rapide accès | Switches accès | Failover 1-2s | N/A |
| **BackboneFast** | Convergence rapide indirect | Tous switches | Réduit Max Age | N/A |

---

## ⚡ PortFast

### Concept

**Problème :** Port d'accès attend 30-50s (Listening 15s + Learning 15s) avant Forwarding  
**Solution :** PortFast → Transition directe Blocking → Forwarding en ~2 secondes

### Configuration

```cisco
! Par interface
interface gi0/5
 switchport mode access
 spanning-tree portfast
exit

! Globalement (tous les ports access)
spanning-tree portfast default

! Désactiver sur une interface spécifique
interface gi0/1
 spanning-tree portfast disable
exit
```

### Vérification

```cisco
show spanning-tree interface gi0/5 detail
! Rechercher : "The port is in the portfast mode"

show spanning-tree summary
! Vérifier : "Portfast Default : enabled"
```

### ⚠️ Règles d'usage

| Périphérique | PortFast | Raison |
|--------------|----------|--------|
| PC, serveur, imprimante | ✅ Oui | Hôte final, aucun risque |
| Téléphone IP seul | ✅ Oui | Hôte final |
| Port trunk | ❌ NON | Risque de boucle temporaire |
| Lien inter-switch | ❌ NON | Risque majeur de boucle |

**💡 PortFast ne doit JAMAIS être activé sur un port connecté à un switch**

---

## 🛡️ BPDU Guard

### Concept

**Problème :** Switch indésirable (rogue) connecté sur port d'accès  
**Solution :** BPDU Guard → Port en err-disabled si BPDU reçu

### Configuration

```cisco
! Par interface
interface gi0/5
 spanning-tree portfast
 spanning-tree bpduguard enable
exit

! Globalement (tous les ports PortFast)
spanning-tree portfast bpduguard default
```

### Vérification

```cisco
show spanning-tree interface gi0/5 detail
! Rechercher : "Bpdu guard is enabled"

show interfaces status err-disabled
! Affiche les ports en err-disabled avec raison

Port      Name               Status       Reason               
Gi0/5     PC-User-01         err-disabled bpduguard
```

### Récupération

**Manuelle :**
```cisco
interface gi0/5
 shutdown
 no shutdown
exit
```

**Automatique :**
```cisco
! Activer récupération automatique
errdisable recovery cause bpduguard

! Délai de récupération (défaut 300s)
errdisable recovery interval 600

! Vérifier
show errdisable recovery
```

**💡 Toujours activer BPDU Guard avec PortFast sur les ports d'accès**

---

## 🔇 BPDU Filter

### BPDU Guard vs BPDU Filter

| Aspect | BPDU Guard | BPDU Filter |
|--------|-----------|-------------|
| **Si BPDU reçu** | Port err-disabled | Ignore BPDU |
| **Envoi BPDUs** | Continue | Arrête |
| **Sécurité** | ✅ Élevée | ⚠️ Faible |
| **Usage** | Ports accès | Rare, cas spécifiques |

### Configuration

**Mode global (relativement sûr) :**
```cisco
spanning-tree portfast bpdufilter default
! Se désactive auto si BPDU reçu
```

**Mode interface (dangereux) :**
```cisco
interface gi0/5
 spanning-tree bpdufilter enable
 ! Ignore COMPLÈTEMENT STP → Risque de boucle !
exit
```

### Vérification

```cisco
show spanning-tree summary
! "Portfast BPDU Filter Default : enabled"

show spanning-tree interface gi0/5 detail
! "Bpdu filter is enabled"
```

**⚠️ BPDU Filter en mode interface peut créer des boucles. Préférer BPDU Guard !**

---

## 🔒 Root Guard

### Concept

**Problème :** Switch avec BID plus bas ajouté sur port périphérique → Devient Root par accident  
**Solution :** Root Guard empêche le port de devenir Root Port

### Fonctionnement

```
Port reçoit BPDU "supérieur" (BID plus bas que Root actuel)
  ↓
Root Guard détecte tentative de devenir Root Port
  ↓
Port placé en état root-inconsistent (bloqué)
  ↓
Trafic bloqué sur ce port
  ↓
Récupération auto dès que BPDUs "supérieurs" cessent
```

### Configuration

```cisco
! Sur les Designated Ports pointant vers périphérie
interface gi0/10
 description Lien vers Access Layer
 spanning-tree guard root
exit

! Sur plusieurs interfaces
interface range gi0/10 - 20
 spanning-tree guard root
exit
```

### Vérification

```cisco
show spanning-tree interface gi0/10 detail
! "Root guard is enabled on the port"

show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             Gi0/10                 Root Inconsistent

show spanning-tree vlan 10

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/10              Desg BKN*4         128.10   P2p *ROOT_Inc
```

### Placement

```
[Core-SW] ← Root Bridge
    |
Root Guard ↓ (sur les ports Designated vers périphérie)
    |
[Distrib-SW]
    |
Root Guard ↓
    |
[Access-SW]
```

**💡 Activer Root Guard sur tous les Designated Ports tournés vers la périphérie**

---

## 🔁 Loop Guard

### Concept

**Problème :** Perte unidirectionnelle de BPDUs (lien physiquement up, mais BPDUs non reçus)  
**Solution :** Loop Guard empêche Alternate Port de passer en Forwarding

### Fonctionnement

**Sans Loop Guard :**
```
Port Alternate ne reçoit plus de BPDUs
  → Après Max Age (20s)
  → Port devient Designated et Forwarding
  → BOUCLE créée !
```

**Avec Loop Guard :**
```
Port Alternate ne reçoit plus de BPDUs
  → Loop Guard détecte anomalie
  → Port en loop-inconsistent (bloqué)
  → Pas de boucle
  → Récupération auto dès réception BPDUs
```

### Configuration

```cisco
! Global (recommandé) - sur tous les ports p2p non-PortFast
spanning-tree loopguard default

! Par interface
interface gi0/2
 spanning-tree guard loop
exit
```

### Vérification

```cisco
show spanning-tree summary
! "Loopguard Default : enabled"

show spanning-tree interface gi0/2 detail
! "Loop guard is enabled on the port"

show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             Gi0/2                  Loop Inconsistent

show spanning-tree vlan 10

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/2               Altn BKN*4         128.2    P2p *LOOP_Inc
```

### Loop Guard vs Root Guard

| Aspect | Loop Guard | Root Guard |
|--------|-----------|-----------|
| **Protège contre** | Perte unidirectionnelle BPDUs | Périphérique devenant Root |
| **Port concerné** | Alternate/Blocked Ports | Designated Ports |
| **État d'erreur** | loop-inconsistent | root-inconsistent |
| **Placement** | Ports p2p non-PortFast | DP vers périphérie |
| **Récupération** | Automatique | Automatique |

**💡 Loop Guard et Root Guard sont complémentaires. Activez les deux !**

---

## 🚀 UplinkFast (Legacy)

### Concept

**Problème :** Convergence 30-50s quand Root Port tombe sur switch d'accès  
**Solution :** UplinkFast → Failover immédiat vers Alternate Port (~1s)

### Fonctionnement

```
Switch d'accès avec 2 uplinks :
  Gi0/1 (Root Port - actif)
  Gi0/2 (Alternate - bloqué)

Panne Gi0/1 :
  → UplinkFast active immédiatement Gi0/2
  → Transition directe vers Forwarding
  → Convergence ~1 seconde
```

### Configuration

```cisco
! Commande globale (sur switch d'accès uniquement)
spanning-tree uplinkfast

! ⚠️ Effets automatiques :
! - Bridge Priority augmentée à 49152
! - Path Cost de tous les ports +3000
! → Empêche ce switch de devenir Root ou chemin préféré
```

### Vérification

```cisco
show spanning-tree summary
! "UplinkFast : enabled"

show spanning-tree vlan 10
! Vérifier Bridge Priority = 49152
```

### ⚠️ Restrictions

| ✅ À utiliser | ❌ Ne PAS utiliser |
|-------------|------------------|
| Switches d'accès | Root Bridge |
| Exactement 2 uplinks | Switches Core/Distribution |
| Topologie simple | Plus de 2 uplinks |

**💡 UplinkFast est OBSOLÈTE avec Rapid-PVST+ (RSTP converge aussi vite naturellement)**

---

## 🔗 BackboneFast (Legacy)

### Concept

**Problème :** Panne indirecte dans le backbone → Convergence 50s (Max Age 20s + Listening 15s + Learning 15s)  
**Solution :** BackboneFast → Bypass Max Age → Convergence 30s

### Fonctionnement

```
Panne indirecte détectée (BPDU "inférieur" reçu)
  ↓
Envoi requête RLQ (Root Link Query) pour confirmer
  ↓
Si confirmé, expire immédiatement BPDUs (sans attendre Max Age)
  ↓
Convergence réduite à 30s (Listening 15s + Learning 15s)

Gain : 20 secondes (Max Age bypassed)
```

### Configuration

```cisco
! Commande globale (sur TOUS les switches !)
spanning-tree backbonefast

! ⚠️ Doit être activé partout pour fonctionner
```

### Vérification

```cisco
show spanning-tree summary
! "BackboneFast : enabled"
```

**💡 BackboneFast est OBSOLÈTE avec RSTP (convergence ~1-2s pour tous types de pannes)**

---

## ⏱️ Tuning des timers STP

### Les 3 timers

| Timer | Défaut | Plage | Rôle |
|-------|--------|-------|------|
| **Hello Time** | 2s | 1-10s | Intervalle envoi BPDUs |
| **Forward Delay** | 15s | 4-30s | Durée Listening/Learning |
| **Max Age** | 20s | 6-40s | Expiration BPDU |

### Contraintes mathématiques

```
Max Age ≥ 2 × (Hello Time + 1)
Max Age ≤ 2 × (Forward Delay - 1)
```

**Exemple :**
```
Hello=2, Forward Delay=15, Max Age=20
Vérif 1: 20 ≥ 2×(2+1) = 6  ✅
Vérif 2: 20 ≤ 2×(15-1) = 28 ✅
```

### Configuration (sur Root uniquement)

```cisco
! Sur le Root Bridge
spanning-tree vlan 10 hello-time 1
spanning-tree vlan 10 forward-time 10
spanning-tree vlan 10 max-age 15

! Méthode simplifiée (diameter)
spanning-tree vlan 10 root primary diameter 4
! Cisco calcule automatiquement les timers optimaux
```

### Vérification

```cisco
show spanning-tree vlan 10

Root ID    Priority    24586
           Address     0ce3.e11a.ba00
           This bridge is the root
           Hello Time   1 sec  Max Age 15 sec  Forward Delay 10 sec
```

### ⚠️ Recommandations

- ✅ Modifier uniquement sur Root Bridge
- ✅ Respecter les contraintes mathématiques
- ✅ Tester en lab avant production
- ⚠️ Ne pas diminuer Forward Delay < 10s (risque boucles)
- ⚠️ Ne pas diminuer Max Age < 10s (risque faux positifs)
- ✅ **Meilleure solution : Utiliser Rapid-PVST+ au lieu de tuner 802.1D**

---

## 🔧 Configuration recommandée moderne

### Switch Core (Root Bridge)

```cisco
hostname CoreSW

! Rapid-PVST+ (convergence naturelle 1-2s)
spanning-tree mode rapid-pvst

! Root Primary
spanning-tree vlan 10,20,30 root primary

! Loop Guard global
spanning-tree loopguard default

! Root Guard sur ports vers distribution
interface range gi0/1-4
 description Liens Distribution Layer
 spanning-tree guard root
exit
```

### Switch Distribution (Root Secondary)

```cisco
hostname DistribSW

! Rapid-PVST+
spanning-tree mode rapid-pvst

! Root Secondary
spanning-tree vlan 10,20,30 root secondary

! Loop Guard global
spanning-tree loopguard default

! Root Guard sur ports vers accès
interface range gi0/10-24
 description Liens Access Layer
 spanning-tree guard root
exit
```

### Switch Access

```cisco
hostname AccessSW

! Rapid-PVST+
spanning-tree mode rapid-pvst

! PortFast + BPDU Guard globalement
spanning-tree portfast default
spanning-tree portfast bpduguard default

! Loop Guard global
spanning-tree loopguard default

! Ports d'accès (PortFast/BPDU Guard auto)
interface range fa0/1-24
 description User Ports
 switchport mode access
 switchport access vlan 10
exit

! Désactiver PortFast sur uplinks
interface range gi0/1-2
 description Uplinks vers Distribution
 spanning-tree portfast disable
exit
```

**💡 Cette configuration combine toutes les meilleures pratiques**

---

## 🔍 Commandes de vérification essentielles

### Vue d'ensemble

```cisco
! Résumé de toutes les fonctionnalités
show spanning-tree summary

Switch is in rapid-pvst mode
Root bridge for: VLAN0010, VLAN0020
Extended system ID           : enabled
Portfast Default             : enabled
PortFast BPDU Guard Default  : enabled
Portfast BPDU Filter Default : disabled
Loopguard Default            : enabled
UplinkFast                   : disabled
BackboneFast                 : disabled
```

### Vérifications par port

```cisco
! Détails d'une interface
show spanning-tree interface gi0/5 detail

Port 5 (GigabitEthernet0/5) of VLAN0010 is forwarding
   The port is in the portfast mode
   Bpdu guard is enabled
   Loop guard is enabled on the port

! Vérifier les ports inconsistants
show spanning-tree inconsistentports

Name                 Interface              Inconsistency
-------------------- ---------------------- ------------------
VLAN0010             Gi0/10                 Root Inconsistent
VLAN0020             Gi0/2                  Loop Inconsistent

! Ports en err-disabled
show interfaces status err-disabled

Port      Name               Status       Reason               
Gi0/8     PC-User-03         err-disabled bpduguard
```

---

## 🎯 Points clés à retenir

### Fonctionnalités essentielles

✅ **PortFast** : Forwarding immédiat pour ports d'accès (bypass 30s convergence)  
✅ **BPDU Guard** : Sécurité contre rogue switches (err-disabled si BPDU reçu)  
✅ **Root Guard** : Protection hiérarchie Root (bloque si tentative devenir Root Port)  
✅ **Loop Guard** : Prévention boucles unidirectionnelles (bloque si perte BPDUs)  
⚠️ **BPDU Filter** : Rare, dangereux (désactive STP sur port)  
⚠️ **UplinkFast/BackboneFast** : Legacy, obsolètes avec RSTP

### Meilleures pratiques

✅ **Toujours PortFast + BPDU Guard** sur ports d'accès  
✅ **Root Guard** sur Designated Ports vers périphérie  
✅ **Loop Guard** global sur tous les switches  
✅ **Rapid-PVST+** au lieu de STP 802.1D  
✅ Timers STP : Modifier uniquement sur Root Bridge si nécessaire  
❌ **Ne JAMAIS** PortFast sur trunk ou lien inter-switch  
❌ **Ne JAMAIS** BPDU Filter en mode interface (sauf cas ultra-spécifique)

### États d'erreur

| État | Cause | Récupération |
|------|-------|--------------|
| **err-disabled** | BPDU reçu (BPDU Guard) | Manuelle ou errdisable recovery |
| **root-inconsistent** | BPDU supérieur reçu (Root Guard) | Automatique |
| **loop-inconsistent** | Perte BPDUs (Loop Guard) | Automatique |

### Configuration type (Access Switch)

```cisco
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree loopguard default

interface range gi0/1-2
 spanning-tree portfast disable
 ! Uplinks
exit
```

### Commandes de vérification

```cisco
show spanning-tree summary                    ! Vue d'ensemble
show spanning-tree interface gi0/5 detail     ! Détails port
show spanning-tree inconsistentports          ! Ports bloqués
show interfaces status err-disabled           ! Ports err-disabled
show errdisable recovery                      ! Config récupération auto
```

---

## 💡 Astuces d'examen

✅ **PortFast** : Uniquement sur ports d'accès, jamais sur trunk/inter-switch  
✅ **BPDU Guard** : Met en err-disabled, récupération manuelle (ou errdisable recovery)  
✅ **BPDU Filter** : Très rare en production, préférer BPDU Guard  
✅ **Root Guard** : Sur Designated Ports, bloque tentatives de devenir Root  
✅ **Loop Guard** : Sur Alternate Ports, prévient boucles si perte BPDUs  
✅ **UplinkFast** : Switches d'accès, Priority → 49152, obsolète avec RSTP  
✅ **BackboneFast** : Réduit convergence indirecte 50s → 30s, obsolète avec RSTP  
✅ **Timers** : Configurer sur Root Bridge uniquement  
✅ **Rapid-PVST+** : Meilleure solution moderne (convergence 1-2s)  
✅ **root-inconsistent** = Root Guard, **loop-inconsistent** = Loop Guard

---

**📚 Fin de la fiche - Module 3 : Advanced Spanning Tree Tuning**
