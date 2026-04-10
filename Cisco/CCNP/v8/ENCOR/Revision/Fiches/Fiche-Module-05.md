# Fiche de révision - Module 5 : VLAN Trunks & EtherChannel
**CCNP ENCOR v8 - Trunks VLAN et Agrégation de Liens**

---

## 🎯 Concepts essentiels

### Trunk 802.1Q

**Trunk** = Connexion transportant **plusieurs VLANs** simultanément

**Encapsulation 802.1Q :**
```
┌──────────────────────────────────────────┐
│ Dest MAC │ Src MAC │ 802.1Q Tag │ Data  │
│                     └─ 4 bytes   │       │
│                       0x8100 + VID       │
└──────────────────────────────────────────┘
```

**Native VLAN :**
- Trafic **non taggé** sur trunk
- Défaut : **VLAN 1** (à changer !)
- ⚠️ **Doit être identique** sur les deux extrémités
- **Mismatch → VLAN hopping risk**

**Allowed VLANs :**
- Liste VLANs autorisés sur trunk
- Défaut : Tous (1-4094)
- Best practice : Limiter aux VLANs utilisés

### DTP (Dynamic Trunking Protocol)

**Cisco proprietary** : Négocie trunks automatiquement

**Modes DTP :**
- **trunk** : Force trunk
- **access** : Force access
- **dynamic desirable** : Initie trunk (actif)
- **dynamic auto** : Attend trunk (passif)
- **nonegotiate** : Désactive DTP

### VTP (VLAN Trunking Protocol)

**Cisco proprietary** : Synchronise base VLANs

**Modes VTP :**
- **Server** : Crée/modifie/supprime VLANs, propage
- **Client** : Lecture seule, applique changements
- **Transparent** : Config locale, relaie updates
- **Off** (v3) : Désactive VTP

**Configuration Revision** : Compteur incrémental (plus élevé → Synchronise)

### EtherChannel

**Agrégation 2-8 liens physiques** → 1 lien logique

**Protocoles :**
- **On** : Statique, pas de négociation
- **PAgP** : Cisco proprietary (desirable/auto)
- **LACP** : IEEE 802.3ad standard (active/passive) ✅

**Load-balancing :** Distribution trafic (src-dst-ip, src-dst-mac)

---

## 📊 Trunks 802.1Q - Configuration

### Configuration trunk basique

```cisco
interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 999  ← Changer Native VLAN
 switchport trunk allowed vlan 10,20,30,100-199
 switchport nonegotiate  ← Désactiver DTP (sécurité)
exit
```

### Gestion Allowed VLANs

```cisco
! Définir liste
switchport trunk allowed vlan 10,20,30

! Ajouter VLANs
switchport trunk allowed vlan add 40,50

! Supprimer VLANs
switchport trunk allowed vlan remove 30

! Tout autoriser
switchport trunk allowed vlan all

! Tout sauf...
switchport trunk allowed vlan except 1-5,1005-1029
```

### Vérification

```cisco
show interfaces trunk

Port        Mode         Encapsulation  Status        Native vlan
Gi0/1       on           802.1q         trunking      999

Port        Vlans allowed on trunk
Gi0/1       10,20,30,100-199

Port        Vlans allowed and active in management domain
Gi0/1       10,20,30,100-105
```

---

## 🔄 DTP (Dynamic Trunking Protocol)

### Modes DTP

| Mode | Initiates | Responds | Envoi DTP |
|------|-----------|----------|-----------|
| trunk | ✅ | ✅ | Oui |
| access | ❌ | ❌ | Oui |
| dynamic desirable | ✅ | ✅ | Oui |
| dynamic auto | ❌ | ✅ | Oui |
| nonegotiate | ❌ | ❌ | Non |

### Négociation DTP

| Switch A | Switch B | Résultat |
|----------|----------|----------|
| trunk | trunk | ✅ Trunk |
| trunk | dynamic desirable | ✅ Trunk |
| trunk | dynamic auto | ✅ Trunk |
| dynamic desirable | dynamic desirable | ✅ Trunk |
| dynamic desirable | dynamic auto | ✅ Trunk |
| **dynamic auto** | **dynamic auto** | ❌ **Access** |
| access | access | ✅ Access |

**💡 Règle : Si UN switch dit "trunk/desirable" → Trunk**

### Configuration DTP

```cisco
! Mode TRUNK (force)
interface GigabitEthernet0/1
 switchport mode trunk
exit

! Mode ACCESS (force)
interface GigabitEthernet0/2
 switchport mode access
exit

! DESIRABLE (négocie activement)
interface GigabitEthernet0/3
 switchport mode dynamic desirable
exit

! AUTO (négocie passivement - défaut)
interface GigabitEthernet0/4
 switchport mode dynamic auto
exit

! TRUNK + NONEGOTIATE (sécurisé)
interface GigabitEthernet0/5
 switchport mode trunk
 switchport nonegotiate  ← Désactive DTP
exit
```

### Sécurité DTP

**🔒 Best practice :**
```cisco
! Ports ACCESS : mode access + nonegotiate
interface range GigabitEthernet0/1-24
 switchport mode access
 switchport nonegotiate
exit

! Ports TRUNK : mode trunk + nonegotiate
interface GigabitEthernet0/48
 switchport mode trunk
 switchport nonegotiate
exit
```

**💡 Désactiver DTP sur TOUS les ports (prévenir VLAN hopping)**

---

## 🗂️ VTP (VLAN Trunking Protocol)

### Modes VTP

| Mode | Crée VLANs | Modifie | Supprime | Propage | Stocke |
|------|------------|---------|----------|---------|--------|
| Server | ✅ | ✅ | ✅ | ✅ | ✅ NVRAM |
| Client | ❌ | ❌ | ❌ | ✅ | ❌ |
| Transparent | ✅ Local | ✅ Local | ✅ Local | Relaie | ✅ NVRAM |
| Off (v3) | ✅ | ✅ | ✅ | ❌ | ✅ |

**Mode défaut : Server** ⚠️

### Configuration Revision

**Compteur incrémental** (0-4,294,967,295)

**Comportement :**
- Client reçoit révision > sienne → **Synchronise**
- Client reçoit révision < sienne → **Ignore**
- ⚠️ **Switch avec révision élevée → Écrase VLANs existants !**

**Réinitialiser révision :**
```cisco
! Méthode 1 : Mode Transparent temporaire
vtp mode transparent
vtp mode server

! Méthode 2 : Changer domaine
vtp domain TEMP
vtp domain PROD

! Méthode 3 : Supprimer vlan.dat (hors config)
delete flash:vlan.dat
reload
```

### VTP v1 vs v2 vs v3

| Fonctionnalité | v1 | v2 | v3 |
|----------------|----|----|-----|
| Consistency checks | ❌ | ✅ | ✅ |
| Extended VLANs (1006-4094) | ❌ | ❌ | ✅ |
| Mode Off | ❌ | ❌ | ✅ |
| Primary Server | ❌ | ❌ | ✅ |
| MST propagation | ❌ | ❌ | ✅ |

**💡 VTPv3 recommandé**

### Configuration VTP

#### VTPv2

```cisco
! Mode Server
vtp version 2
vtp domain ENTREPRISE
vtp password SecureP@ss hidden
vtp mode server
vtp pruning

! Mode Client
vtp version 2
vtp domain ENTREPRISE
vtp password SecureP@ss hidden
vtp mode client

! Mode Transparent (recommandé)
vtp mode transparent
```

#### VTPv3

```cisco
! Mode Server
vtp version 3
vtp domain ENTREPRISE
vtp password SecureP@ss hidden
vtp mode server
vtp primary  ← Désigner Primary Server

! Mode Off (recommandé)
vtp version 3
vtp mode off
```

### Vérification VTP

```cisco
show vtp status

VTP Version capable             : 1 to 3
VTP version running             : 2
VTP Domain Name                 : ENTREPRISE
VTP Pruning Mode                : Enabled
Configuration Revision          : 42
Number of existing VLANs        : 15
```

---

## 🔗 EtherChannel

### Concept

**2 à 8 liens physiques** → **1 lien logique**

**Avantages :**
- ✅ Bande passante agrégée (4×1G = 4G)
- ✅ Redondance (échec 1 lien → Autres actifs)
- ✅ Pas de boucle STP (1 lien logique)
- ✅ Load-balancing trafic

**Prérequis (TOUS identiques) :**
- ✅ Speed (1G, 10G)
- ✅ Duplex (full)
- ✅ VLANs (access : même VLAN, trunk : même allowed/native)
- ✅ Mode (tous access OU tous trunk)

**❌ Mismatch → EtherChannel échoue (err-disabled)**

### Protocoles EtherChannel

| Protocole | Type | Modes | Recommandé |
|-----------|------|-------|------------|
| **On** | Statique | on | ❌ (pas de négociation) |
| **PAgP** | Cisco | desirable/auto | ❌ (proprietary) |
| **LACP** | IEEE 802.3ad | active/passive | ✅ (standard) |

### Modes négociation

#### PAgP (Cisco proprietary)

| Switch A | Switch B | Résultat |
|----------|----------|----------|
| desirable | desirable | ✅ EtherChannel |
| desirable | auto | ✅ EtherChannel |
| **auto** | **auto** | ❌ **Erreur** |

#### LACP (IEEE 802.3ad)

| Switch A | Switch B | Résultat |
|----------|----------|----------|
| active | active | ✅ EtherChannel |
| active | passive | ✅ EtherChannel |
| **passive** | **passive** | ❌ **Erreur** |

**💡 Au moins UN switch doit être actif (desirable/active)**

### Configuration EtherChannel

#### Trunk EtherChannel (LACP)

```cisco
! Liens physiques
interface range GigabitEthernet0/1-4
 description EtherChannel to Core
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 999
 switchport trunk allowed vlan 10,20,30,100-199
 channel-group 1 mode active  ← LACP active
 no shutdown
exit

! Port-Channel logique
interface Port-channel1
 description Trunk EtherChannel
 switchport mode trunk
 switchport trunk native vlan 999
 switchport trunk allowed vlan 10,20,30,100-199
 no shutdown
exit
```

#### Access EtherChannel (PAgP)

```cisco
! Liens physiques
interface range GigabitEthernet0/5-6
 switchport mode access
 switchport access vlan 100
 channel-group 2 mode desirable  ← PAgP desirable
 no shutdown
exit

! Port-Channel
interface Port-channel2
 switchport mode access
 switchport access vlan 100
 no shutdown
exit
```

#### Layer 3 EtherChannel

```cisco
! Liens physiques
interface range GigabitEthernet0/10-11
 no switchport
 channel-group 3 mode active
 no shutdown
exit

! Port-Channel L3
interface Port-channel3
 no switchport
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit
```

### Load-Balancing

**Algorithmes disponibles :**

| Algorithme | Basé sur | Utilisation |
|------------|----------|-------------|
| src-mac | MAC source | Simple |
| dst-mac | MAC destination | Simple |
| **src-dst-mac** | MAC src + dst | ✅ **L2 recommandé** |
| src-ip | IP source | L3 |
| dst-ip | IP destination | L3 |
| **src-dst-ip** | IP src + dst | ✅ **L3 recommandé** |
| src-port | Port TCP/UDP src | L4 |
| dst-port | Port TCP/UDP dst | L4 |

**Configuration :**
```cisco
! L2 switches
port-channel load-balance src-dst-mac

! L3 switches/routers
port-channel load-balance src-dst-ip
```

**Vérification :**
```cisco
show etherchannel load-balance

EtherChannel Load-Balancing Configuration:
        src-dst-ip
```

### Vérification EtherChannel

```cisco
! Résumé
show etherchannel summary

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi0/1(P)    Gi0/2(P)    Gi0/3(P)    Gi0/4(P)

! Codes :
! S = Layer 2 (switched)
! U = Up (en service)
! P = Port bundled (dans EtherChannel)
! (SU) = ✅ EtherChannel fonctionnel

! Détails EtherChannel
show etherchannel 1 detail

! État Port-Channel
show interfaces Port-channel1

! Voisins LACP
show lacp neighbor
```

---

## 🔧 Troubleshooting EtherChannel

### Erreurs communes

#### 1. Speed/Duplex Mismatch

**Problème :** EtherChannel ne se forme pas

**Solution :**
```cisco
interface range GigabitEthernet0/1-4
 speed 1000
 duplex full
exit
```

#### 2. VLAN Mismatch

**Trunk :**
```cisco
! Allowed VLANs différents → Erreur
interface range GigabitEthernet0/1-4
 switchport trunk allowed vlan 10,20,30  ← Identiques !
exit
```

**Native VLAN :**
```cisco
! Native VLAN différent → CDP warnings
interface range GigabitEthernet0/1-4
 switchport trunk native vlan 999  ← Identique !
exit
```

#### 3. Mode Mismatch

**Problème :** PAgP sur un switch, LACP sur l'autre

**Solution :**
```cisco
! Les DEUX switches : même protocole
! Switch A et B
channel-group 1 mode active  ← LACP
```

#### 4. Passive/Passive ou Auto/Auto

**Problème :** Aucun switch n'initie négociation

**Solution :**
```cisco
! Switch A : ACTIF
channel-group 1 mode active

! Switch B : peut rester passif
channel-group 1 mode passive
```

#### 5. Configuration incohérente

**Problème :** Config Port-Channel ≠ Physical ports

**Solution :**
```cisco
! Physical ports ET Port-Channel : même config
interface range GigabitEthernet0/1-4
 switchport mode trunk
 switchport trunk native vlan 999
exit

interface Port-channel1
 switchport mode trunk
 switchport trunk native vlan 999
exit
```

### Checklist dépannage

✅ `show etherchannel summary` → Code (SU) = OK  
✅ `show interfaces status` → Tous ports up/up  
✅ Comparer speed, duplex, VLANs, mode  
✅ Vérifier protocole (LACP active/passive, PAgP desirable/auto)  
✅ Comparer config physical ports vs Port-Channel  
✅ Tester câbles physiques

---

## 🎯 Comparaisons

### Trunks : DTP Modes

| Mode | Envoi DTP | Initie Trunk | Répond Trunk |
|------|-----------|--------------|--------------|
| trunk | Oui | ✅ | ✅ |
| access | Oui | ❌ | ❌ |
| dynamic desirable | Oui | ✅ | ✅ |
| dynamic auto | Oui | ❌ | ✅ |
| nonegotiate | ❌ | ❌ | ❌ |

### VTP : Modes

| Mode | Modifie local | Propage | Reçoit updates | Stocke NVRAM |
|------|---------------|---------|----------------|--------------|
| Server | ✅ | ✅ | ✅ | ✅ |
| Client | ❌ | ✅ | ✅ | ❌ |
| Transparent | ✅ | Relaie | ❌ | ✅ |
| Off (v3) | ✅ | ❌ | ❌ | ✅ |

### EtherChannel : Protocoles

| Protocole | Type | Modes | Multi-vendor | Recommandé |
|-----------|------|-------|--------------|------------|
| On | Statique | on | ✅ | ❌ |
| PAgP | Cisco | desirable/auto | ❌ | ❌ |
| LACP | IEEE 802.3ad | active/passive | ✅ | ✅ |

---

## 🎯 Points clés à retenir

### Trunks 802.1Q

✅ **802.1Q** : Tag 4 bytes (TPID 0x8100 + VID 12 bits)  
✅ **Native VLAN** : Non taggé, défaut VLAN 1 (à changer)  
✅ **Allowed VLANs** : Filtre VLANs autorisés (défaut : tous)  
✅ **Mismatch Native VLAN** → VLAN hopping risk

**Configuration :**
```cisco
switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 10,20,30
switchport nonegotiate
```

### DTP

✅ **DTP** : Cisco proprietary, négocie trunks auto  
✅ **desirable** : Initie trunk (actif)  
✅ **auto** : Attend trunk (passif, défaut)  
✅ **auto + auto** = Access (aucun n'initie)  
✅ **🔒 Sécurité** : `switchport nonegotiate` sur TOUS ports

### VTP

✅ **VTP** : Synchronise base VLANs (Cisco proprietary)  
✅ **Server** : Crée/modif/supprime VLANs  
✅ **Client** : Lecture seule  
✅ **Transparent** : Config locale, relaie  
✅ **Configuration Revision** : Plus élevé → Synchronise  
✅ **⚠️ Danger** : Révision élevée → Écrase VLANs  
✅ **Best practice** : Mode Transparent ou Off (v3)

### EtherChannel

✅ **2-8 liens physiques** → 1 lien logique  
✅ **Avantages** : Bande passante, redondance, pas boucle STP  
✅ **Prérequis** : Speed, duplex, VLANs identiques  
✅ **LACP** : IEEE 802.3ad (✅ recommandé)  
✅ **active** : Initie LACP  
✅ **passive** : Attend LACP  
✅ **passive + passive** = Erreur  
✅ **Load-balancing** : src-dst-ip (L3), src-dst-mac (L2)  
✅ **Code (SU)** = EtherChannel fonctionnel

---

## 💡 Astuces d'examen

✅ **Native VLAN mismatch** → CDP/VTP warnings, VLAN hopping  
✅ **DTP auto + auto** → Forme Access (pas trunk)  
✅ **DTP desirable + auto** → Forme Trunk  
✅ **VTP révision élevée** → Écrase VLANs (danger !)  
✅ **VTPv3** : Supporte Extended VLANs (1006-4094), Primary Server  
✅ **LACP active + passive** → EtherChannel OK  
✅ **LACP passive + passive** → EtherChannel échoue  
✅ **PAgP desirable + auto** → EtherChannel OK  
✅ **PAgP auto + auto** → EtherChannel échoue  
✅ **Load-balancing src-dst-ip** → Meilleur équilibrage L3  
✅ **Code (SU)** dans `show etherchannel summary` → OK  
✅ **Mismatch speed/duplex/VLAN** → EtherChannel échoue  
✅ **VTP Pruning** → Réduit trafic broadcast inutile  
✅ **nonegotiate** → Désactive DTP (sécurisé)

---

## 📋 Commandes essentielles

### Trunks

```cisco
! Configuration trunk
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 10,20,30
switchport nonegotiate

! Vérification
show interfaces trunk
show interfaces switchport
```

### VTP

```cisco
! Configuration VTP
vtp version 3
vtp domain ENTREPRISE
vtp password SecureP@ss hidden
vtp mode transparent  (ou off en v3)

! Vérification
show vtp status
show vtp password
```

### EtherChannel

```cisco
! Configuration LACP
interface range GigabitEthernet0/1-4
 channel-group 1 mode active
exit

interface Port-channel1
 switchport mode trunk
exit

! Load-balancing
port-channel load-balance src-dst-ip

! Vérification
show etherchannel summary
show etherchannel 1 detail
show etherchannel load-balance
show lacp neighbor
```

---

**📚 Fin de la fiche - Module 5 : VLAN Trunks & EtherChannel**
