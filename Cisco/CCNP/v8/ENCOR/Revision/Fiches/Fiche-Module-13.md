# Fiche Rapide Module 13 : Multicast

## Adressage Multicast IPv4

```
┌──────────────────────────────┐
│ Class D : 224.0.0.0/4        │
├──────────────────────────────┤
│ 224.0.0.0 - 224.255.255.255  │
│  (224-239 premier octet)     │
└──────────────────────────────┘

Répartition :
Reserved   : 224.0.0.0/24
Globales   : 224.0.1.0 - 224.251.255.255
Admin Scoped : 239.0.0.0/8
```

## MAC Multicast Layer 2

**Format** : `01:00:5E:xx:xx:xx`

**Calcul** : 
- Prendre 23 bits bas de l'IP multicast
- Joindre au préfixe `01:00:5E`

**Exemple**:
```
IP: 224.10.20.30     →  MAC: 01:00:5E:0A:14:1E
IP: 224.1.1.1        →  MAC: 01:00:5E:01:01:01
```

## IGMP Versions

| Version | Type | Timeout | Caractéristiques |
|---------|------|---------|------------------|
| **IGMPv1** | ❌ Obsolète | ∞ | Basique, ancien |
| **IGMPv2** | ✓ Standard | 260s | Leave message explicite |
| **IGMPv3** | ✓✓ Moderne | Config | **Source-Specific** |

### IGMPv2 Flow

```
1. Host envoie MEMBERSHIP REPORT
   → "Je veux groupe 224.10.0.1"
   
2. Routeur maintient la liste

3. Host envoie LEAVE MESSAGE
   → "Je quitte le groupe"
```

## IGMP Snooping (Switch)

**Rôle** : Écouter IGMP en Layer 2 pour éviter flood multicast

```
Trafic multicast →
    Switch voit IGMP REPORT sur port X
    ↓
    Copie multicast → ports avec membres IGMP
    ↓
    Pas de flood sur tous ports
```

## PIM Modes

### PIM Dense Mode (DM)

**Strategy** : **Flood & Prune**
```
Envoie partout
Hosts qui ne veulent pas → Prune
```
- Petit réseau
- Beaucoup de receveurs
- Faible latence

### PIM Sparse Mode (SM) ✓ Recommandé

**Strategy** : **Source → RP → Receivers**
```
     Source ──Register──→ RP
                          ↓
                     Receivers
                    ← Join/Prune
```
- Grand réseau
- Groupes épars
- Meilleur scalabilité

## Rendezvous Point (RP)

**Fonction** : Routeur pivot central pour SPM

| Élément | Détail |
|---------|--------|
| **Rôle** | Négocie sources/receveurs |
| **Élection** | Basée sur **Priorité** |
| **Priorité** | 0-255 : Plus bas = Meilleur |
| **BSR Election** | Découverte auto (si configuré) |
| **Défaut** | Aucun (statique = meilleur) |

### Configuration RP

```cisco
! Statique (simple)
ip pim rp-address 10.1.1.1 0

! Multicandidat (Auto-election)
ip pim rp-candidate loopback0 10
ip pim bsr-candidate loopback0 20
```

## Arbres Multicast

### RPT (RP Tree)

```
        RP (Root)
        /   |   \
    R1     R2    R3
    |      |     |
   H1     H2    H3
```

- Source → RP → Récepteurs
- Optimal pour groupes épars
- Latence plus élevée

### SPT (Shortest Path Tree)

```
    Source (Root)
      /   |   \
    R1    R2   R3
    |     |    |
   H1    H2   H3
```

- Source = root
- Latence minimale
- RPT → SPT transition auto

## GLOP Addressing (RFC 3180)

**Format** : `233.ASN.0.0/16`

**Calcul** : Convertir ASN en hex
```
ASN 64500 = 0xFBF4 en hex
GLOP = 233.251.244.0/16
```

**Bénéfice** : Unicité globale sans coordination

## Admin Scoped (Boundaries)

**Plage** : `239.0.0.0/8`

**Utilité** : Limiter portée groupe multicast
```cisco
pim boundary BOUNDARY-ACL
ip access-list standard BOUNDARY-ACL
  deny 239.0.0.1
```

## Configuration Minimale Multicast

```cisco
! Globale
ip multicast-routing
ip pim rp-address 10.1.1.1 0

! Interface
interface GigabitEthernet0/0/1
  ip pim sparse-mode
  ip igmp version 3
  ip igmp query-interval 125
```

## Vérification Clés

```cisco
show ip mroute [group]           ! Arbres multicast
show ip pim neighbor             ! Voisins PIM
show ip pim rp mapping           ! RP info
show ip igmp groups [int]        ! IGMP groups
show ip igmp interface           ! IGMP stats
```

## Nuances Critiques

- **MAC Multicast = 01:00:5E + 23 bits bas IP**
- **IGMPv3 = Source-Specific Multicast (SSM)**
- **IGMP Snooping ≠ multicast routing** (Layer 2 vs 3)
- **PIM Sparse ≈ mieux scalabilité** (recommandé)
- **RP = point unique de défaillance** (redondance conseil)
- **RPT initial, SPT meilleur** (transition auto)
- **Admin-scoped = 239.0.0.0/8** (pas d'export)
- **GLOP = 233.ASN.0.0/16** (uniqueness garantie)

## Checklist Mini

- ☐ Multicast routing enabled (`ip multicast-routing`)
- ☐ PIM mode chosen (Dense/Sparse)
- ☐ RP configured (priorité < 128)
- ☐ Interfaces IGMP active
- ☐ Voisins PIM établis
- ☐ Sources announcées RP
- ☐ Receivers joignent groupe (IGMPv3)
- ☐ Trafic suit RPT/SPT
- ☐ Pas d'admin-scoped unintended
- ☐ GLOP utilisé si propre ASN

