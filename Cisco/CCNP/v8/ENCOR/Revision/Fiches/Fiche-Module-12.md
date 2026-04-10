# Fiche Rapide Module 12 : Advanced BGP

## Multihoming - Types

```
┌─────────────────────────────────────┐
│ MÊME ASN (Recommended)              │
├─────────────────────────────────────┤
│ Customer obtient 1 ASN              │
│ Se connecte à 2+ ISP                │
│ Contrôle total de la politique      │
│                                     │
│  ISP1 (AS100)                       │
│      \                              │
│       [Customer AS65001]            │
│      /                              │
│  ISP2 (AS200)                       │
└─────────────────────────────────────┘

DIFFÉRENT ASN (Problématique)
- Routes différentes par AS_Path
- Moins de contrôle
```

## ORF (Outbound Route Filtering)

**Objectif** : Informer les voisins BGP des préfixes DÉSIRÉS
→ Évite le transit involontaire

```cisco
! Configuration ORF
neighbor 10.1.1.254 capability orf prefix-list send
neighbor 10.1.1.254 filter-list 1 out
```

## Filtering - Prefix List vs ACL

| Critère | ACL | Prefix-List |
|---------|-----|------------|
| **Spécificité** | Source seulement | Préfixe complet |
| **Longueur** | Non contrôlable | ge/le pour plages |
| **Usage BGP** | Basique | ✓ Recommandé |
| **Performance** | Rapide | Plus rapide |

### Prefix List Syntax

```cisco
ip prefix-list NAME seq N {permit|deny} PREFIX [ge M] [le N]
```

**Exemples clés** :
```cisco
! /24 et plus spécifique
ip prefix-list SPECIFICS seq 10 permit 10.0.0.0/8 ge 24

! Tout SAUF /32
ip prefix-list NO-HOST seq 10 permit 0.0.0.0/0 le 31
```

## Route Maps - Structure

```cisco
route-map NAME [permit|deny] SEQ
  match [criteria]     ← Condition
  set [action]         ← Action si match true
```

### Match Criteria Essentiels

- `match ip address PREFIIX-LIST`
- `match as-path AS-PATH-ACL`
- `match community COMMUNITY-LIST`
- `match metric VALUE`

### Set Actions Essentiels

| Action | Contrôle |
|--------|----------|
| `set local-preference N` | Routes SORTANTES (iBGP) |
| `set as-path prepend X` | Allonger AS_Path (éviter) |
| `set metric N` | MED (routes entrantes) |
| `set weight N` | Weight Cisco (0-65535) |
| `set community X:Y` | Ajouter tag |

## AS Path Filtering avec Regex

| Pattern | Signification |
|---------|--------------|
| `^100$` | Seulement AS 100 adjacent |
| `^100_200$` | AS 100, puis 200 adjacents |
| `^100.*200$` | AS 100 au début, 200 à la fin |
| `^[0-9]+_100_[0-9]+$` | AS 100 au milieu |
| `.*` | N'importe quel AS path |

### Config AS Path ACL

```cisco
ip as-path access-list 1 permit ^100$
ip as-path access-list 1 permit ^100_200$

router bgp 65001
  neighbor 10.1.1.254 route-map ISP1-FILTER in
route-map ISP1-FILTER permit 10
  match as-path 1
```

## BGP Communities

### Well-known Communities

| Community | Signification |
|-----------|--------------|
| `no-export` (65535:65281) | Ne pas exporter hors AS |
| `no-advertise` (65535:65282) | Pas d'annonce du tout |
| `local-as` (65535:65283) | Reste en confédération |
| `internet` (0) | Aucune restriction |

### Configuration

```cisco
! Tagger
route-map TAG-IT permit 10
  match prefix-list INTERNAL
  set community 100:1

! Envoyer community flag
neighbor 10.1.1.254 send-community both
```

## Best Path Algorithm Recap (7 premiers)

1. **Weight** → Cisco proprietary, plus haut = meilleur
2. **Local Pref** → iBGP seulement, plus haut = meilleur  
3. **Originated locally** → redistribute vs received
4. **AS_Path length** → Les court = meilleur
5. **Origin** → IGP > EGP > Incomplete
6. **MED** → Moins élevé = meilleur (même AS)
7. **eBGP vs iBGP** → eBGP > iBGP

**Restant** : IGP cost, Cluster-list, Router ID, Peer IP

## Manipulation du Path Sélection

### Préférer une Route (Local Preference)

```cisco
! Augmenter Local Pref pour ISP1 (meilleur sortant)
route-map PREFER-ISP1 permit 10
  set local-preference 200

! Baisser pour ISP2 (déprioritiser)
route-map AVOID-ISP2 permit 10
  set local-preference 50
```

### Déprioritiser via AS_Path Prepend

```cisco
! Allonger AS_Path artificiel (routes entrantes moins préférées)
route-map DEPRIORITIZE permit 10
  set as-path prepend 65001 65001 65001
```

**Effet** : Route paraît plus loin (AS_Path de 4 au lieu de 1)

## Checklist Advanced BGP

- ☐ Multihoming configuré avec même/différent ASN
- ☐ ORF activé si applicable (ISP support)
- ☐ Prefix-lists créées pour filtrage
- ☐ Route maps pour matching/tagging
- ☐ Communities utilisées pour politiques
- ☐ Local Pref pour contrôle sortant
- ☐ MED pour routes rentrantes
- ☐ Failover/basculement testé
- ☐ Redundant paths vérifiés (show ip bgp)
- ☐ Pas de transit involontaire

## Nuances Critiques

- **Local Pref s'échange en iBGP** → Ne sort pas en eBGP
- **MED reste dans même AS** → Ne remonte pas en eBGP
- **Communities = tags réutilisables** → Très flexible
- **AS Path manipulé ne trompe jamais boucle loop** → Loop prevention reste OK
- **ORF = information client demande** → ISP honore ou ignore
- **Weight ne sort pas** → Cisco seulement, local significance

