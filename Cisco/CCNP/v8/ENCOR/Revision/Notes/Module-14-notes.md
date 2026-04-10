# Module 14 : QoS (Quality of Service)

## Introduction

QoS (Quality of Service) est l'ensemble des mécanismes permettant de garantir ou d'optimiser la performance réseau pour appliquer les critères : bande passante, latence, gigue, et perte de paquets. QoS est crucial pour les applications sensibles (voix, vidéo, transactions financières).

## The Need for QoS

### Problèmes sans QoS

**Meilleur effort** (Best Effort) :
- Pas de garanties de performance
- Premier arrivé, premier servi
- Applications sensibles souffrent des pics de trafic

### Dimensions Clés de QoS

| Paramètre | Définition | Impact |
|-----------|-----------|--------|
| **Bande passante** | Débit disponible (Mbps) | Plus haute = plus trafic |
| **Latence** | Délai transmission (ms) | Plus bas = meilleur pour VoIP |
| **Gigue (Jitter)** | Variation latence | Voix robuste si < 30 ms |
| **Perte paquet** | % paquets perdus | Voice/Video: < 1% acceptable |

### Cas d'Usage QoS

- **VoIP** : Latence < 150ms, Jitter < 30ms
- **Vidéo streaming** : Débit stable, < 5% perte
- **Applications critiques** : Garanties de bande
- **Meilleur effort** : Résidu bande passante

## QoS Models

### 1. Best Effort (Aucun QoS)

**Approche** : Aucune garantie

```
Toutes les sources traitées identiquement
Basé sur file FIFO (First In First Out)
```

**Problème** : Applications sensibles peuvent souffrir

### 2. IntServ (Integrated Services)

**Approche** : Réservation de ressources (rigide)

**Protocoles** :
- **RSVP** (Reservation Protocol) : Réserve ressources bout-à-bout

**Caractéristiques** :
- Garanties strictes de bande/latence
- État per-flow (complexe)
- Scalabilité limitée

**Exemple** : VoIP réserve 64 kbps pour call spécifique

### 3. DiffServ (Differentiated Services)

**Approche** : Classification et marquage (flexible, scalable)

**Principes** :
- **Classification** : Identifier trafic
- **Marking** : Assigner tags priorité
- **Per-hop behaviors** : Actions routeur

**Avantages** :
- Scalable (pas d'état per-flow)
- Flexible (peut adapter comportement)
- Hiérarchique

## Classification and Marking

### Identification du Trafic

**Critères de classification** :

| Critère | Exemple |
|---------|---------|
| Source IP | 10.1.1.0/24 |
| Destination IP | 8.8.8.8 |
| Port source | 5060 (SIP) |
| Port destination | 80 (HTTP) |
| Protocol | TCP, UDP |
| DSCP | Pre-marked value |

### Mécanismes de Marquage

#### CoS (Class of Service)

**Layer 2 tag** : 3 bits dans VLAN header (802.1p)

- **Plage** : 0-7
- **Scope** : LAN seulement
- **Temps de vie** : Supprimé à l'eBGP

```
Ethernet Frame : |Dest|Src|[CoS(3-bit)|VLAN]|Type|Payload|CRC|
                                    (7-5)
```

#### DSCP (Differentiated Services Code Point)

**Layer 3 tag** : 6 bits dans champ IP ToS

- **Plage** : 0-63
- **Scope** : End-to-end (IP)
- **Temps de vie** : Survit routage

**Format** : `xxxxx0` (6 bits, 2-7 en octet)

```
IP Header : |ToS Byte: DSCP(6-bit) | ECN(2-bit)|
                       vvvvvv00      ee
```

#### Common DSCP Values

| DSCP | Value | Usage |
|------|-------|-------|
| **EF** | 46 | Expedited Forwarding (VoIP) |
| **AF11** | 10 | Assured Forwarding low |
| **AF21** | 18 | Assured Forwarding medium |
| **AF31** | 26 | Assured Forwarding high |
| **CS0** | 0 | Best Effort (défaut) |
| **CS1-CS7** | 8,16,24,32,40,48,56 | Class Selector |

## Policing and Shaping

### Policing (Limitation sévère)

**Objectif** : Rejeter/marquer paquets au-delà du débit limite

**Fonctionnement** :
```
Trafic entrant > Limite ?
  ├─ OUI  → Drop (ou marquer)
  └─ NON  → Pass
```

**Algorithme** : Token Bucket
- Bucket accumule "tokens" au débit configuré
- Paquet consomme token
- Sans token = drop

**Configuration** :
```cisco
policy-map POLICE
  class HIGH-PRIORITY
    police rate 1000k burst 100k exceed-action drop

interface GigabitEthernet0/0/0
  service-policy input POLICE
```

**Impact** : Retards possibles, perte paquet

### Shaping (Limitation douce)

**Objectif** : Lisser trafic en excès (sans drop)

**Fonctionnement** :
```
Trafic > Limite ?
  ├─ OUI  → Queue (buffering)
  └─ NON  → Forward
```

**Avantages vs Policing** :
- Pas de perte immédiate
- Trafic "lissé"
- Meilleure performance applicative

**Configuration** :
```cisco
policy-map SHAPE
  class HIGH-PRIORITY
    shape average 1000k 10000

interface GigabitEthernet0/0/0
  service-policy output SHAPE
```

### Policing vs Shaping Comparaison

| Aspect | Policing | Shaping |
|--------|----------|---------|
| **Action** | Drop/Mark | Queue (buffering) |
| **Perte** | Possible | Rare |
| **Latence** | Minimal | Plus élevée |
| **Usage** | Inbound, límit strict | Outbound, lisse tout |

## Congestion Management

### Queueing (File d'attente)

**Défi** : Quand liens congestionné, quel paquet forward d'abord?

**Options** :

#### FIFO (First-In-First-Out)

```
Tous paquets égaux
Queue: AAABBBCCC
Envoi: A,A,A,B,B,B,C,C,C
```
**Problème** : Pas de priorité

#### Priority Queueing (PQ)

```
Vraie priorité : Vider queue HIGH avant MEDIUM
HIGH: 1
MEDIUM: 1
NORMAL: 2
LOW: 3
```
**Problème** : Starvation des basses priorités

#### Weighted Fair Queueing (WFQ)

```
Partage équitable pondéré
HIGH: 50% bande passante
MEDIUM: 30% bande passante
LOW: 20% bande passante
```
**Avantage** : Équitable + protection basse priorité

#### Class-Based Queueing (CBQ)

```
Allocate bande passante par classe
Voice: 100 Mbps garanti
Video: 200 Mbps garanti
Best Effort: Résidu
```
**Avantage** : Garanties claires par classe

## Congestion Avoidance

### Stratégies de Perte

**RED (Random Early Detection)** :
```
% perte augmente graduellement quand charge Q augmente
Charge basse   : 0% perte
Charge moyen   : 5% perte (drop aléatoire)
Charge haute   : 20% perte (drop plus aléatoire)
Charge max     : 100% perte (queue pleine)
```

**Avantage** : Évite congestion soudaine, signale source d'adapter

### WRED (Weighted RED)

**Extension** : Appliquer RED par classe priorité

```
HIGH (DSCP 46)  : Seuil 80%, Drop 5%
MEDIUM (DSCP 18): Seuil 60%, Drop 10%
LOW (DSCP 0)    : Seuil 40%, Drop 20%
```

**Effet** : Basses priorités droppées avant hautes

## Configuration QoS Complète

### Policy-Map (Classe-Action)

**Structure** :
```cisco
policy-map QoS-POLICY
  class VOICE          ← Classe BGP
    priority 100000    ← Garantir 100 Mbps
    set dscp ef        ← Marquer EF
    police 100k        ← Limiter 100 Kbps avec police
    
  class VIDEO
    bandwidth 200000   ← Garantir 200 Mbps
    set dscp af31      ← Marquer AF31
    shape average 1000k ← Lisser à 1 Mbps
    
  class BEST-EFFORT
    fair-queue         ← WFQ pour resta
```

### Class-Map (Identificateur)

```cisco
class-map match-any VOICE
  match protocol rtp   ← RTP (VoIP)
  match dscp ef        ← Déjà marqué EF
  match port udp 5060  ← SIP signaling

class-map match-all VIDEO
  match protocol rtsp  ← RTSP streaming
  match access-group 110 ← ACL vidéo IPs

class-map BEST-EFFORT
  match any
```

### Application sur Interface

```cisco
interface GigabitEthernet0/0/0
  service-policy input INPUT-POLICY
  service-policy output OUTPUT-POLICY
```

### Exemple Complet

```cisco
! ACLs
ip access-list extended VOICE-IPs
  permit ip 10.1.1.0 0.0.0.255 any
  
ip access-list extended VIDEO-IPs
  permit ip 10.2.2.0 0.0.0.255 any

! Classes
class-map match-any VOICE
  match access-group name VOICE-IPs
  match port udp eq 5060

class-map match-any VIDEO
  match access-group name VIDEO-IPs

class-map BEST-EFFORT
  match any

! Politics
policy-map QoS-ENTRANCE
  class VOICE
    priority 100000
    set dscp ef
    
  class VIDEO
    bandwidth 200000
    set dscp af31
    
  class BEST-EFFORT
    fair-queue

! Interface
interface GigabitEthernet1/1
  service-policy input QoS-ENTRANCE
```

## Points Importants à Retenir

1. **QoS necessary** pour garantir performance applications sensibles
2. **Best Effort** : Aucune garantie (par défaut)
3. **IntServ** : Réservation stricte (peu scalable)
4. **DiffServ** : Classification-marking (scalable, récommandé)
5. **CoS** : Layer 2 (3 bits VLAN), scope LAN
6. **DSCP** : Layer 3 (6 bits IP ToS), end-to-end
7. **EF (46)** : Expedited Forwarding pour VoIP
8. **AF classes** : Assured Forwarding (AF11-AF41)
9. **Policing** : Limite sévère → drop possible
10. **Shaping** : Limite douce → queue/buffering
11. **Queueing** : FIFO, PQ, WFQ, CBQ
12. **WRED** : Random Early Detection par classe
13. **Policy-Maps** : Lier classe à actions
14. **Service-Policy** : Appliquer politique à interface
