# Fiche Rapide Module 14 : QoS

## Quatre Dimensions QoS

| Dimension | Exemplaire | Impact |
|-----------|-----------|--------|
| **Bande passante** | 1-1000 Mbps | Débit total |
| **Latence** | 1-150 ms | VoIP: < 150ms |
| **Gigue (Jitter)** | 1-100 ms | Voix robuste < 30ms |
| **Perte paquet** | 0-5% | VoIP/Video: < 1% |

## Trois Modèles QoS

```
┌─────────────────────┐
│ BEST EFFORT (Défaut)│  Aucune garantie
└─────────────────────┘

┌─────────────────────┐
│ IntServ (Réservé)   │  RSVP → strict garantie
│ Per-flow état       │  Peu scalable
└─────────────────────┘

┌─────────────────────┐
│ DiffServ (Moderne)  │  Classification+Marking
│ Scalable,flexible   │  ✓ Recommandé
└─────────────────────┘
```

## CoS vs DSCP

| Aspect | CoS | DSCP |
|--------|-----|------|
| **Couche** | Layer 2 (Ethernet) | Layer 3 (IP) |
| **Bits** | 3 bits (802.1p) | 6 bits (ToS) |
| **Plage** | 0-7 | 0-63 |
| **Portée** | LAN seulement | End-to-end |
| **Format** | VLAN tag | IP header |

### CoS Format
```
Ethernet Frame: |Dest|Src|[CoS(3)|VLAN ID]|Type|...
                          vvv
                         (7-5)
```

### DSCP Format
```
IP Header: |ToS: DSCP(6)|ECN(2)|...
                  vvvvvv  ee
```

## DSCP Values (Standards)

| Code | Value | Classe | Usage |
|------|-------|--------|-------|
| **EF** | 46 | Expedited | VoIP, mission-critical |
| **AF41** | 34 | Gold | Streaming vidéo |
| **AF31** | 26 | Silver | Trans données |
| **AF21** | 18 | Bronze | BDD/FTP |
| **AF11** | 10 | Platinum1 | Web interactive |
| **CS0** | 0 | Best Effort | Défaut/Bulk data |
| **CS1-7** | 8,16,24... | Classe Select | Legacy apps |

## Policing vs Shaping

### Policing (Limitation Sévère)

```
DROP PATH:
Trafic → Rate limiteur → Drop/Mark overflow
│
└─→ Strict limite
    Latence bas
    Perte possible
    Inbound typique
```

**Config** :
```cisco
police rate 1000k burst 100k exceed-action drop
```

### Shaping (Limitation Douce)

```
QUEUE PATH:
Trafic → Rate buffer/queue → Forward régulièrement
│
└─→ Trafic lissé
    Latence plus haute
    Pas de drop (buffer)
    Outbound typique
```

**Config** :
```cisco
shape average 1000k
```

## Queueing Algorithms

### FIFO (First-In-First-Out)

```
Queue: [A A A B B C C C]
Output: A A A B B C C C (ordre d'arrivée)
```
❌ Pas de priorité

### Priority Queueing (PQ)

```
Queue1 (HIGH):  [V V V]
Queue2 (MEDIUM):[W W W]
Queue3 (LOW):   [X X X]

Output: V V V W W W X X X (HIGH vidé d'abord)
```
⚠️ Risk: Low priority starvation

### Weighted Fair Queueing (WFQ)

```
Allocation poids:
HIGH:   50% bande passante
MEDIUM: 30% bande passante
LOW:    20% bande passante
```
✓ Équitable + protection

### Class-Based Queueing (CBQ)

```
Voice:      100 Mbps garanti
Video:      200 Mbps garanti
Best-Effort: Résidu/overflow
```
✓ Garanties claires

## RED / WRED (Congestion Avoidance)

### RED (Random Early Detection)

```
% Drop vs Queue Load:

100% ├─ Always Drop (queue full)
     ├─ Gradient Drop (30-80% queue)
50%  ├─ 
     ├─ No Drop (0-30% queue)
 0%  └─
     └─────────────────
       Queue depth %
```

### WRED (Weighted RED par classe)

```
HIGH (EF):   Drop 5% au 80% queue
MEDIUM:      Drop 10% au 60% queue
LOW:         Drop 20% au 40% queue
```

## QoS Configuration Template

### 1. Identifier (Class-Map)

```cisco
class-map match-any VOICE
  match protocol rtp
  match dscp ef
  match port udp eq 5060
```

### 2. Action (Policy-Map)

```cisco
policy-map QoS-POLICY
  class VOICE
    priority 100000      ← Priorité+bande
    set dscp ef          ← Marquer
    police 100k          ← Limiter
  
  class VIDEO
    bandwidth 200000
    set dscp af31
    shape average 1000k
    
  class BEST-EFFORT
    fair-queue
```

### 3. Appliquer (Interface)

```cisco
interface GigabitEthernet0/0/0
  service-policy input QoS-POLICY
  service-policy output QoS-POLICY
```

## Vérification QoS

```cisco
show policy-map                  ! Policies créées
show policy-map interface [int]  ! Stats par interface
show class-map                   ! Classes définies
show queue interface [int]       ! Queue statistics
show priority-queue             ! PQ counters
```

## Points Critiques Cisco

- **CoS supprimé en eBGP** → Besoin de re-marquer
- **DSCP survit routage** → Layer 3 end-to-end
- **Priority queue = Absolute** → Peut starve autres
- **Fair-queue = WFQ** (par défaut)
- **police = inbound**; **shape = outbound** (norm)
- **WRED > RED** pour DiffServ (par classe)
- **Remarquer au edge** (border router)

## Checklist Mini QoS

- ☐ Traffic classification définie (match criteria)
- ☐ Class-maps créées (trafic identifiant)
- ☐ Policy-maps appliquées (actions)
- ☐ DSCP marquage configuré (ou CoS)
- ☐ Policing/Shaping appliquée
- ☐ Queueing strategy choisie
- ☐ WRED ou congestion avoidance
- ☐ Service-policy appliquée interfaces
- ☐ Priorities testées (VoIP>Video>Best)
- ☐ Stats vérifiées (show policy-map)

## Exemples de DSCP Typiques

```
VoIP:              EF (46)
Signaling SIP:     CS3 (24)
Vidéo-conf:        AF31 (26) ou AF41 (34)
Applications crit: AF21/AF31
Web interactif:    AF11 (10)
FTP/Bulk:          CS1 (8)
Défaut/Best:       CS0 (0)
```

