# Module 5 : VLAN Trunks & EtherChannel
**CCNP ENCOR v8 - Trunks VLAN et Agrégation de Liens**

---

## 📋 Vue d'ensemble

### Objectifs du module

- ✅ Maîtriser la configuration des **trunks 802.1Q** (native VLAN, allowed VLANs)
- ✅ Comprendre le **DTP (Dynamic Trunking Protocol)** et ses modes
- ✅ Configurer **VTP (VLAN Trunking Protocol)** v1/v2/v3
- ✅ Implémenter **EtherChannel** pour l'agrégation de liens
- ✅ Différencier **PAgP** (Cisco) vs **LACP** (standard IEEE)
- ✅ Configurer le **load-balancing** EtherChannel
- ✅ Dépanner les **misconfigurations** EtherChannel

### Thèmes principaux

1. **Trunks 802.1Q** : Transport multi-VLANs, tagging, native VLAN
2. **DTP** : Négociation automatique trunks (modes desirable/auto)
3. **VTP** : Synchronisation base VLANs (modes server/client/transparent)
4. **EtherChannel** : Agrégation physique → Bande passante et redondance
5. **PAgP vs LACP** : Protocoles négociation (Cisco proprietary vs IEEE standard)
6. **Load-balancing** : Distribution trafic (src-mac, dst-mac, src-dst-ip, etc.)
7. **Troubleshooting** : Erreurs communes (mismatch speed, duplex, VLAN, etc.)

---

## 🌐 1. Trunks 802.1Q

### 1.1 Concept

**Trunk (lien agrégé)** : Connexion transportant **plusieurs VLANs** simultanément

**Cas d'usage :**
- Switch ↔ Switch
- Switch ↔ Routeur (Router-on-a-Stick)
- Switch ↔ Serveur (802.1Q tagging capable)

### 1.2 Encapsulation 802.1Q

**IEEE 802.1Q** : Standard d'encapsulation VLAN

**Trame Ethernet 802.1Q :**
```
┌────────────────────────────────────────────────────────────┐
│ Dest MAC │ Src MAC │ 802.1Q Tag │ Type │ Data │ FCS        │
└────────────────────────────────────────────────────────────┘
                      ▲
                      │
            ┌─────────┴─────────┐
            │ TPID │ TCI        │ 4 bytes
            │0x8100│ PRI│CFI│VID│
            └──────┴────────────┘
                    ▼
                [VLAN ID: 12 bits = 1-4094]
```

**Champs 802.1Q Tag :**
- **TPID (Tag Protocol Identifier)** : `0x8100` (identifie trame taggée)
- **PRI (Priority)** : 3 bits (QoS / CoS)
- **CFI (Canonical Format Indicator)** : 1 bit (Ethernet vs Token Ring)
- **VID (VLAN ID)** : 12 bits → 4094 VLANs (0 et 4095 réservés)

### 1.3 Native VLAN

**Concept :** VLAN transporté **sans tag** sur un trunk 802.1Q

**Règles :**
- Trafic Native VLAN **non taggé** (compatibilité legacy)
- Par défaut : **VLAN 1** (changeable)
- **Doit être identique** sur les deux extrémités du trunk

**Importance :**
- ⚠️ **Mismatch Native VLAN** → Risque de violation sécurité (VLAN hopping)
- ⚠️ **CDP/VTP warnings** si mismatch détecté
- ✅ Best practice : **Ne pas utiliser VLAN 1** (changer Native VLAN)

**Configuration Native VLAN :**
```cisco
interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 999
exit
```

**Vérification :**
```cisco
show interfaces trunk

Port        Mode             Encapsulation  Status        Native vlan
Gi0/1       on               802.1q         trunking      999
```

**🔒 Sécurité : Ne jamais utiliser VLAN 1 comme Native VLAN (vulnérabilité VLAN hopping)**

### 1.4 Allowed VLANs

**Concept :** Liste des VLANs autorisés sur un trunk (filtre)

**Par défaut :** Tous les VLANs (1-4094) sont autorisés

**Bonnes pratiques :**
✅ Limiter aux VLANs réellement utilisés (sécurité, performances)  
✅ Réduire le trafic broadcast inutile  
✅ Isoler les VLANs sensibles

**Configuration :**
```cisco
interface GigabitEthernet0/1
 switchport trunk allowed vlan 10,20,30,100-199,999
exit
```

**Ajout/Suppression VLANs :**
```cisco
! Ajouter VLAN 40
switchport trunk allowed vlan add 40

! Supprimer VLAN 30
switchport trunk allowed vlan remove 30

! Tout autoriser (par défaut)
switchport trunk allowed vlan all

! Tout interdire sauf...
switchport trunk allowed vlan except 1-5,1005-1029
```

**Vérification :**
```cisco
show interfaces trunk

Port        Vlans allowed on trunk
Gi0/1       10,20,30,40,100-199,999
```

### 1.5 Pruning (élagage)

**VTP Pruning** : Limite propagation trafic broadcast/multicast

**Sans Pruning :**
```
SW1 (VLAN 10,20,30) ──trunk─→ SW2 (VLAN 10) 
                              │
                              └─→ Reçoit broadcasts VLANs 20,30 inutiles
```

**Avec Pruning :**
```
SW1 (VLAN 10,20,30) ──trunk─→ SW2 (VLAN 10)
                              │
                              └─→ Ne reçoit que broadcasts VLAN 10
```

**Configuration :**
```cisco
! Sur serveur VTP
vtp pruning
```

**💡 VTP Pruning améliore performances (moins de trafic inutile)**

---

## 🔄 2. DTP (Dynamic Trunking Protocol)

### 2.1 Concept

**DTP (Dynamic Trunking Protocol)** : Protocole Cisco proprietary pour négocier automatiquement les trunks

**Utilité :** Évite configuration manuelle des trunks

**⚠️ Risque sécurité :** Attaques VLAN hopping (DTP enabled par défaut)

### 2.2 Modes DTP

| Mode | Description | Initiates Trunk | Responds to Trunk |
|------|-------------|-----------------|-------------------|
| **trunk** | Force trunk (pas de négociation) | ✅ Oui | ✅ Oui |
| **access** | Force access (pas de négociation) | ❌ Non | ❌ Non |
| **dynamic desirable** | Initie négociation trunk | ✅ Oui | ✅ Oui |
| **dynamic auto** | Attend négociation (passif) | ❌ Non | ✅ Oui (si demandé) |
| **nonegotiate** | Désactive DTP (mode trunk obligatoire) | ❌ Non | ❌ Non |

### 2.3 Négociation DTP

**Combinaisons possibles :**

| Switch A | Switch B | Résultat |
|----------|----------|----------|
| trunk | trunk | ✅ **Trunk** |
| trunk | dynamic desirable | ✅ **Trunk** |
| trunk | dynamic auto | ✅ **Trunk** |
| trunk | access | ❌ **Erreur** (mismatch) |
| dynamic desirable | dynamic desirable | ✅ **Trunk** |
| dynamic desirable | dynamic auto | ✅ **Trunk** |
| dynamic auto | dynamic auto | ❌ **Access** (aucun n'initie) |
| access | access | ✅ **Access** |
| trunk + nonegotiate | trunk + nonegotiate | ✅ **Trunk** (pas DTP) |

**💡 Règle : Si UN switch dit "trunk/desirable" → Trunk formé**

### 2.4 Configuration DTP

```cisco
! Mode TRUNK (force trunk, envoie DTP)
interface GigabitEthernet0/1
 switchport mode trunk
exit

! Mode ACCESS (force access, envoie DTP)
interface GigabitEthernet0/2
 switchport mode access
exit

! Mode DYNAMIC DESIRABLE (négocie activement)
interface GigabitEthernet0/3
 switchport mode dynamic desirable
exit

! Mode DYNAMIC AUTO (négocie passivement - par défaut)
interface GigabitEthernet0/4
 switchport mode dynamic auto
exit

! Mode TRUNK + NONEGOTIATE (pas DTP, sécurisé)
interface GigabitEthernet0/5
 switchport mode trunk
 switchport nonegotiate
exit
```

**Vérification :**
```cisco
show interfaces GigabitEthernet0/1 switchport

Name: Gi0/1
Switchport: Enabled
Administrative Mode: trunk
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: On  ← DTP actif
```

### 2.5 Sécurité DTP

**⚠️ Vulnérabilités DTP :**
- **VLAN Hopping** : Attaquant envoie trames DTP → Switch crée trunk
- **Double Tagging** : Exploitation Native VLAN

**🔒 Mitigation :**
```cisco
! Désactiver DTP sur TOUS les ports non-trunk
interface range GigabitEthernet0/1-24
 switchport mode access
 switchport nonegotiate
exit

! Ports trunk : nonegotiate
interface GigabitEthernet0/48
 switchport mode trunk
 switchport nonegotiate
exit
```

**💡 Best practice : `switchport nonegotiate` sur TOUS les ports (trunk et access)**

---

## 🗂️ 3. VTP (VLAN Trunking Protocol)

### 3.1 Concept

**VTP (VLAN Trunking Protocol)** : Protocole Cisco pour synchroniser la base VLANs

**Utilité :**
- Centraliser gestion VLANs
- Propager ajouts/suppressions VLANs
- Éviter configuration manuelle répétitive

**⚠️ Risques :**
- **Suppression accidentelle VLANs** (serveur avec révision plus élevée)
- **Configuration revision mismatch**

### 3.2 Modes VTP

| Mode | Crée VLANs | Modifie VLANs | Supprime VLANs | Propage VLANs | Stocke config |
|------|------------|---------------|----------------|---------------|---------------|
| **Server** | ✅ Oui | ✅ Oui | ✅ Oui | ✅ Oui | ✅ Oui (NVRAM) |
| **Client** | ❌ Non | ❌ Non | ❌ Non | ✅ Oui | ❌ Non |
| **Transparent** | ✅ Oui (local) | ✅ Oui (local) | ✅ Oui (local) | ✅ Relaie | ✅ Oui (NVRAM) |
| **Off** (v3) | ✅ Oui | ✅ Oui | ✅ Oui | ❌ Non | ✅ Oui |

**Mode par défaut :** **Server** (⚠️ Danger !)

### 3.3 Configuration Revision

**Configuration Revision Number** : Compteur incrémental (0-4,294,967,295)

**Comportement :**
- Switch **Client** reçoit révision > sienne → Synchronise
- Switch **Client** reçoit révision < sienne → Ignore
- Switch **Server** avec révision plus élevée → Écrase base VLANs

**⚠️ Danger :** Ajouter switch avec révision élevée → Efface tous les VLANs !

**Réinitialiser révision :**
```cisco
! Méthode 1 : Mode Transparent temporaire
vtp mode transparent
vtp mode server

! Méthode 2 : Changer domaine puis revenir
vtp domain OLD_DOMAIN
vtp domain NEW_DOMAIN

! Méthode 3 : Supprimer vlan.dat (hors config)
delete flash:vlan.dat
reload
```

**Vérification révision :**
```cisco
show vtp status

VTP Version capable             : 1 to 3
VTP version running             : 2
VTP Domain Name                 : ENTREPRISE
VTP Pruning Mode                : Disabled
VTP Traps Generation            : Disabled
Configuration Revision          : 42  ← Numéro révision
Number of existing VLANs        : 15
```

### 3.4 VTP v1 vs v2 vs v3

| Fonctionnalité | VTPv1 | VTPv2 | VTPv3 |
|----------------|-------|-------|-------|
| **Consistency checks** | Non | Oui | Oui |
| **Token Ring VLANs** | Non | Oui | Oui |
| **Transparent mode relais** | Limité | ✅ Oui | ✅ Oui |
| **Extended VLANs (1006-4094)** | ❌ Non | ❌ Non | ✅ Oui |
| **Mode Off** | ❌ Non | ❌ Non | ✅ Oui |
| **Primary Server** | ❌ Non | ❌ Non | ✅ Oui |
| **Protected VLANs** | ❌ Non | ❌ Non | ✅ Oui |
| **MST propagation** | ❌ Non | ❌ Non | ✅ Oui |

**💡 VTPv3 recommandé (Extended VLANs, Primary Server, Mode Off)**

### 3.5 Configuration VTP

#### VTP v1/v2

```cisco
! Mode Server
vtp version 2
vtp domain ENTREPRISE
vtp password SecureP@ssw0rd
vtp mode server
vtp pruning

! Mode Client
vtp version 2
vtp domain ENTREPRISE
vtp password SecureP@ssw0rd
vtp mode client

! Mode Transparent
vtp mode transparent
```

#### VTP v3

```cisco
! Mode Server
vtp version 3
vtp domain ENTREPRISE
vtp password SecureP@ssw0rd hidden
vtp mode server

! Désigner Primary Server (un seul)
vtp primary

! Mode Client
vtp version 3
vtp domain ENTREPRISE
vtp password SecureP@ssw0rd hidden
vtp mode client

! Mode Off (désactive VTP complètement)
vtp mode off
```

**Vérification :**
```cisco
show vtp status
show vtp password
```

### 3.6 Sécurité VTP

**🔒 Best practices :**
✅ **Mode Transparent ou Off** : Évite propagation accidentelle  
✅ **VTP Password** : Authentification (hash MD5)  
✅ **VTPv3 Primary Server** : Contrôle strict modifications  
✅ **Pruning** : Réduit trafic broadcast  
✅ **Documenter révision** : Évite écrasement accidentel

**Configuration sécurisée :**
```cisco
! Option 1 : Transparent (independence)
vtp mode transparent

! Option 2 : VTPv3 Off
vtp version 3
vtp mode off

! Option 3 : VTPv3 avec contrôle strict
vtp version 3
vtp domain SECURE_DOMAIN
vtp password ComplexP@ssw0rd! hidden
vtp mode server
vtp pruning
! Désigner Primary Server sur UN switch core
vtp primary
```

---

## 🔗 4. EtherChannel (Agrégation de Liens)

### 4.1 Concept

**EtherChannel** : Agrégation de **2 à 8 liens physiques** en **1 lien logique**

**Avantages :**
- ✅ **Bande passante** : Agrégation (2×1G = 2G, 4×10G = 40G)
- ✅ **Redondance** : Échec 1 lien → Autres liens actifs
- ✅ **Pas de boucle** : STP voit 1 lien logique (pas 8 liens physiques)
- ✅ **Load-balancing** : Distribution trafic entre liens

**Sans EtherChannel :**
```
SW1 ──link1──→ SW2      STP bloque link2, link3, link4
    ──link2──→          Bande passante perdue
    ──link3──→          Pas de redondance
    ──link4──→
```

**Avec EtherChannel :**
```
SW1 ══PortChannel══→ SW2    STP voit 1 lien logique
    (4×1G = 4G)            Tous liens actifs
                           Load-balancing
```

### 4.2 Prérequis EtherChannel

**Tous les liens doivent être IDENTIQUES :**

✅ **Speed** : Même vitesse (1G, 10G, etc.)  
✅ **Duplex** : Même mode (full-duplex)  
✅ **VLANs** :
  - Access : Même VLAN
  - Trunk : Mêmes Allowed VLANs, Native VLAN
✅ **Spanning Tree** : Même paramètres (coût, priorité)  
✅ **Mode** : Tous trunk OU tous access (pas mixte)

**❌ Mismatch → EtherChannel ne se forme pas (err-disabled)**

### 4.3 Modes EtherChannel

**3 options :**
1. **Mode On** : Pas de négociation (statique)
2. **PAgP** : Négociation Cisco proprietary
3. **LACP** : Négociation IEEE 802.3ad standard

#### Mode On

**Caractéristiques :**
- Pas de protocole négociation
- Configuration statique
- ⚠️ Risque de boucle si misconfiguration

**Configuration :**
```cisco
interface range GigabitEthernet0/1-4
 channel-group 1 mode on
exit

interface Port-channel1
 switchport mode trunk
exit
```

#### PAgP (Port Aggregation Protocol)

**Cisco proprietary** (❌ Non compatible autres vendors)

**Modes PAgP :**
| Mode | Initiates PAgP | Responds to PAgP |
|------|----------------|------------------|
| **desirable** | ✅ Oui (actif) | ✅ Oui |
| **auto** | ❌ Non (passif) | ✅ Oui (si demandé) |

**Négociation :**
| Switch A | Switch B | Résultat |
|----------|----------|----------|
| desirable | desirable | ✅ EtherChannel |
| desirable | auto | ✅ EtherChannel |
| auto | auto | ❌ **Erreur** (aucun n'initie) |

**Configuration :**
```cisco
interface range GigabitEthernet0/1-4
 channel-group 1 mode desirable
exit

interface Port-channel1
 switchport mode trunk
exit
```

#### LACP (Link Aggregation Control Protocol)

**IEEE 802.3ad standard** (✅ Compatible multi-vendor)

**Modes LACP :**
| Mode | Initiates LACP | Responds to LACP |
|------|----------------|------------------|
| **active** | ✅ Oui (actif) | ✅ Oui |
| **passive** | ❌ Non (passif) | ✅ Oui (si demandé) |

**Négociation :**
| Switch A | Switch B | Résultat |
|----------|----------|----------|
| active | active | ✅ EtherChannel |
| active | passive | ✅ EtherChannel |
| passive | passive | ❌ **Erreur** (aucun n'initie) |

**Configuration :**
```cisco
interface range GigabitEthernet0/1-4
 channel-group 1 mode active
exit

interface Port-channel1
 switchport mode trunk
exit
```

**💡 LACP recommandé (standard, interopérable)**

### 4.4 Load-Balancing EtherChannel

**Méthode distribution trafic** entre liens physiques

**Algorithmes disponibles :**

| Algorithme | Basé sur | Utilisation |
|------------|----------|-------------|
| **src-mac** | MAC source | Simple, déséquilibré si 1 source |
| **dst-mac** | MAC destination | Simple, déséquilibré si 1 destination |
| **src-dst-mac** | ✅ MAC src + dst | ✅ **Équilibré** (recommandé L2) |
| **src-ip** | IP source | Niveau 3 |
| **dst-ip** | IP destination | Niveau 3 |
| **src-dst-ip** | ✅ IP src + dst | ✅ **Équilibré** (recommandé L3) |
| **src-port** | Port TCP/UDP source | Niveau 4 |
| **dst-port** | Port TCP/UDP destination | Niveau 4 |
| **src-dst-port** | Port src + dst | Niveau 4 |

**Principe :** Hash du champ sélectionné → Modulo nombre de liens → Lien assigné

**Exemple src-dst-ip :**
```
Hash(10.1.1.1 → 192.168.1.10) = 0xABCD → Modulo 4 = Lien 1
Hash(10.1.1.2 → 192.168.1.20) = 0x1234 → Modulo 4 = Lien 0
```

**Configuration :**
```cisco
! Global (tous EtherChannels)
port-channel load-balance ?
  dst-ip       Dst IP Addr
  dst-mac      Dst Mac Addr
  src-dst-ip   Src XOR Dst IP Addr
  src-dst-mac  Src XOR Dst Mac Addr
  src-ip       Src IP Addr
  src-mac      Src Mac Addr

! Configuration (L2 switches)
port-channel load-balance src-dst-mac

! Configuration (L3 switches/routers)
port-channel load-balance src-dst-ip
```

**Vérification :**
```cisco
show etherchannel load-balance

EtherChannel Load-Balancing Configuration:
        src-dst-ip

EtherChannel Load-Balancing Addresses Used Per-Protocol:
Non-IP: Source XOR Destination MAC address
  IPv4: Source XOR Destination IP address
  IPv6: Source XOR Destination IP address
```

**💡 Best practice : `src-dst-ip` (L3) ou `src-dst-mac` (L2) pour meilleur équilibrage**

### 4.5 Configuration complète EtherChannel

#### Trunk EtherChannel (LACP)

```cisco
! Configuration liens physiques
interface range GigabitEthernet0/1-4
 description EtherChannel to Core-SW
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 999
 switchport trunk allowed vlan 10,20,30,100-199
 channel-group 1 mode active
 no shutdown
exit

! Configuration Port-Channel logique
interface Port-channel1
 description Trunk EtherChannel to Core-SW
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 999
 switchport trunk allowed vlan 10,20,30,100-199
 no shutdown
exit

! Load-balancing
port-channel load-balance src-dst-ip
```

#### Access EtherChannel (PAgP)

```cisco
! Configuration liens physiques
interface range GigabitEthernet0/5-6
 description EtherChannel to Server
 switchport mode access
 switchport access vlan 100
 channel-group 2 mode desirable
 no shutdown
exit

! Configuration Port-Channel
interface Port-channel2
 description Access EtherChannel to Server
 switchport mode access
 switchport access vlan 100
 no shutdown
exit
```

#### Routed EtherChannel (Layer 3)

```cisco
! Configuration liens physiques
interface range GigabitEthernet0/10-11
 no switchport
 channel-group 3 mode active
 no shutdown
exit

! Configuration Port-Channel Layer 3
interface Port-channel3
 description L3 EtherChannel to Router
 no switchport
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit
```

### 4.6 Vérification EtherChannel

```cisco
! Résumé EtherChannels
show etherchannel summary

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi0/1(P)    Gi0/2(P)    Gi0/3(P)    Gi0/4(P)
2      Po2(SU)         PAgP      Gi0/5(P)    Gi0/6(P)

! Détails EtherChannel 1
show etherchannel 1 detail

Group state = L2
Ports: 4   Maxports = 8
Port-channels: 1 Max Port-channels = 1
Protocol:   LACP
Minimum Links: 0

! État Port-Channel
show interfaces Port-channel1

Port-channel1 is up, line protocol is up (connected)
  Hardware is EtherChannel, address is 0ce3.e11a.ba00
  MTU 1500 bytes, BW 4000000 Kbit/sec

! LACP neighbor
show lacp neighbor

Flags:  S - Device is requesting Slow LACPDUs
        F - Device is requesting Fast LACPDUs
        A - Device is in Active mode       P - Device is in Passive mode

Port      Neighbor             Port     Age  Flags   Admin  Oper  Port
          Port ID    Devid                              Key Key  Priority
Gi0/1     32769      0ce3.e11a.ba10      29s  SA      0x1  0x1  32768
Gi0/2     32770      0ce3.e11a.ba10      29s  SA      0x1  0x1  32768
```

**Codes flags Summary :**
- **S** : Layer 2 (switched)
- **U** : EtherChannel en service (up)
- **P** : Port bundled dans Port-Channel
- **D** : Down
- **H** : Hot-standby (non utilisé)
- **I** : Stand-alone (pas dans bundle)

**💡 Code `(SU)` = Switched + Up = ✅ EtherChannel fonctionnel**

---

## 🔧 5. Troubleshooting EtherChannel

### 5.1 Erreurs communes

#### 1. Speed/Duplex Mismatch

**Symptôme :** EtherChannel ne se forme pas, ports err-disabled

**Cause :**
```cisco
interface GigabitEthernet0/1
 speed 1000
 duplex full

interface GigabitEthernet0/2
 speed 100    ← MISMATCH
 duplex half   ← MISMATCH
```

**Solution :**
```cisco
interface range GigabitEthernet0/1-4
 speed 1000
 duplex full
exit
```

#### 2. VLAN Mismatch (Trunk)

**Symptôme :** EtherChannel formé mais trafic perdu

**Cause :**
```cisco
interface GigabitEthernet0/1
 switchport trunk allowed vlan 10,20,30

interface GigabitEthernet0/2
 switchport trunk allowed vlan 10,20,40  ← MISMATCH
```

**Solution :**
```cisco
interface range GigabitEthernet0/1-4
 switchport trunk allowed vlan 10,20,30
exit
```

#### 3. Native VLAN Mismatch

**Symptôme :** CDP warnings, trafic perdu

**Cause :**
```cisco
interface GigabitEthernet0/1
 switchport trunk native vlan 999

interface GigabitEthernet0/2
 switchport trunk native vlan 1  ← MISMATCH
```

**Solution :**
```cisco
interface range GigabitEthernet0/1-4
 switchport trunk native vlan 999
exit
```

#### 4. Mode Mismatch (PAgP/LACP)

**Symptôme :** EtherChannel ne se forme pas

**Cause :**
```cisco
! Switch A
channel-group 1 mode active  (LACP)

! Switch B
channel-group 1 mode desirable  (PAgP)  ← MISMATCH
```

**Solution :** Utiliser même protocole
```cisco
! Les deux switches
channel-group 1 mode active
```

#### 5. Passive/Passive ou Auto/Auto

**Symptôme :** EtherChannel ne se forme pas

**Cause :**
```cisco
! Switch A
channel-group 1 mode passive  (LACP)

! Switch B
channel-group 1 mode passive  (LACP)  ← Aucun n'initie
```

**Solution :** Au moins 1 switch actif
```cisco
! Switch A
channel-group 1 mode active

! Switch B reste passive (OK)
channel-group 1 mode passive
```

#### 6. Port-Channel config vs Physical ports config

**Symptôme :** Configuration incohérente

**Cause :** Config sur Port-Channel pas appliquée aux physical ports

**Solution :** Appliquer config sur physical ports ET Port-Channel
```cisco
! Physical ports
interface range GigabitEthernet0/1-4
 switchport mode trunk
 switchport trunk native vlan 999
 channel-group 1 mode active
exit

! Port-Channel (doit avoir même config)
interface Port-channel1
 switchport mode trunk
 switchport trunk native vlan 999
exit
```

### 5.2 Commandes debug

```cisco
! Activer debug LACP
debug lacp all

! Activer debug PAgP
debug pagp events
debug pagp packets

! Désactiver debugs
no debug all
undebug all
```

### 5.3 Dépannage méthodique

**Checklist :**
1. ✅ Vérifier `show etherchannel summary` (code SU = OK)
2. ✅ Vérifier `show interfaces status` (tous ports up/up)
3. ✅ Comparer config physical ports (speed, duplex, VLANs, trunk)
4. ✅ Vérifier mode négociation (LACP active/passive, PAgP desirable/auto)
5. ✅ Vérifier `show etherchannel X detail` (erreurs, mismatch)
6. ✅ Comparer config Port-Channel vs physical ports
7. ✅ Tester câbles physiques (link up/down)

---

## 🎯 Meilleures pratiques

### Trunks 802.1Q

✅ **Native VLAN ≠ VLAN 1** (sécurité VLAN hopping)  
✅ **Native VLAN identique** sur les deux extrémités  
✅ **Allowed VLANs** : Limiter aux VLANs utilisés  
✅ **VTP Pruning** : Réduire trafic broadcast

### DTP

✅ **Désactiver DTP** : `switchport nonegotiate` sur TOUS les ports  
✅ **Mode trunk explicite** sur trunks (pas dynamic)  
✅ **Mode access explicite** sur access ports

### VTP

✅ **Mode Transparent ou Off** : Éviter propagation accidentelle  
✅ **VTPv3** : Supporte Extended VLANs, Primary Server, Mode Off  
✅ **VTP Password** : Sécurité (hash MD5)  
✅ **Documenter révision** : Éviter écrasement accidentel  
✅ **Test en lab avant production**

### EtherChannel

✅ **LACP préféré** : Standard IEEE, interopérable  
✅ **Load-balancing** : `src-dst-ip` (L3) ou `src-dst-mac` (L2)  
✅ **Prérequis identiques** : Speed, duplex, VLANs, mode  
✅ **Config cohérente** : Physical ports + Port-Channel  
✅ **Documenter** : Nombre liens, protocole, load-balancing

---

## 📋 Points clés à retenir

### Trunks 802.1Q

✅ **802.1Q** : Standard encapsulation VLAN (tag 4 bytes)  
✅ **Native VLAN** : Non taggé sur trunk (défaut VLAN 1)  
✅ **Allowed VLANs** : Filtre VLANs autorisés sur trunk  
✅ **Mismatch Native VLAN** → Risque VLAN hopping

### DTP

✅ **DTP** : Cisco proprietary, négocie trunks automatiquement  
✅ **Modes** : trunk, access, dynamic desirable, dynamic auto, nonegotiate  
✅ **desirable + auto** → Trunk formé  
✅ **auto + auto** → Access (aucun n'initie)  
✅ **🔒 Sécurité** : Désactiver DTP (`nonegotiate`)

### VTP

✅ **VTP** : Synchronise base VLANs (Cisco proprietary)  
✅ **Modes** : Server (crée/modif/supprime), Client (lecture seule), Transparent (local), Off (v3)  
✅ **Configuration Revision** : Switch avec revision > sienne → Synchronise  
✅ **⚠️ Danger** : Révision élevée → Efface VLANs existants  
✅ **VTPv3** : Extended VLANs, Primary Server, Mode Off

### EtherChannel

✅ **EtherChannel** : Agrège 2-8 liens physiques → 1 lien logique  
✅ **Avantages** : Bande passante, redondance, pas de boucle STP  
✅ **Prérequis** : Speed, duplex, VLANs, mode identiques  
✅ **Protocoles** : On (statique), PAgP (Cisco), LACP (IEEE 802.3ad ✅)  
✅ **LACP modes** : active (initie), passive (attend)  
✅ **Load-balancing** : src-dst-ip (L3), src-dst-mac (L2)

### Troubleshooting

✅ **Mismatch** : Speed, duplex, VLANs, Native VLAN, mode  
✅ **Passive + Passive** → Échec (aucun n'initie)  
✅ **Code SU** = EtherChannel fonctionnel  
✅ **Vérification** : `show etherchannel summary`, `show interfaces trunk`

---

## 🎓 Conclusion

Module 5 couvre les fondamentaux des **trunks VLAN**, **DTP**, **VTP**, et **EtherChannel** :

- **Trunks 802.1Q** : Transport multi-VLANs avec tagging, attention au Native VLAN
- **DTP** : Négociation automatique trunks (désactiver pour sécurité)
- **VTP** : Synchronisation VLANs (mode Transparent/Off recommandé)
- **EtherChannel** : Agrégation liens (LACP + src-dst-ip optimal)

**Points critiques examen :**
- Native VLAN mismatch = VLAN hopping risk
- DTP auto + auto = Access (pas trunk)
- VTP révision élevée = Écrase VLANs
- LACP active + passive = EtherChannel OK
- Load-balancing src-dst-ip = Meilleur équilibrage

**🚀 Maîtriser ces concepts = Réseau Layer 2 robuste et sécurisé !**

---

**📚 Fin du Module 5 : VLAN Trunks & EtherChannel**
