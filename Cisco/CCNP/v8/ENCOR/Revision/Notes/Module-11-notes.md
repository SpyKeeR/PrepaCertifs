# Module 11 : BGP Fundamentals

## Introduction

BGP (Border Gateway Protocol) est le protocole de routage externe standard utilisé sur Internet. Contrairement aux protocoles IGP (OSPF, EIGRP) basés sur la métrique et la topologie, BGP est un protocole **Path Vector** qui prend des décisions de routage basées sur les chemins AS (Autonomous System) et les politiques administratives.

## Concepts Clés

### BGP, EGP et AS (Autonomous System)

**Autonomous System (AS)** : Un ensemble de réseaux sous contrôle administratif unique, utilisant une politique de routage interne cohérente. Chaque AS est identifié par un numéro unique (ASN).

**EGP (Exterior Gateway Protocol)** : Famille de protocoles utilisés pour router le trafic entre AS différents. BGP est le standard actuel.

**Interior Gateway Protocol (IGP)** : Protocoles utilisés pour router au sein d'un AS (OSPF, EIGRP, RIP).

### BGP et ses Variantes

- **eBGP (External BGP)** : Session BGP entre routeurs de différents AS
  - Distance administrative : 20
  - Change les attributs BGP à chaque annonce
  
- **iBGP (Internal BGP)** : Session BGP entre routeurs du même AS
  - Distance administrative : 200
  - Maintient la distance administrative plus élevée pour éviter les boucles internes

### ASN (Autonomous System Numbers)

| Type | Plage | Usage |
|------|-------|-------|
| ASN public 16-bit | 1-64511, 64512-65534 | Assignés par IANA, registres régionaux |
| ASN 16-bit privé | 64512-65535 | Réseaux privés, labs, démonstrations |
| ASN public 32-bit | 65536+ (4200000000-4294967294) | Extension de l'espace d'adressage |
| ASN réservé | 64512-65534 (autres plages) | RFC 5398, RFC 3758 |

## Algorithm Path Vector

### Fonctionnement

BGP utilise un **algorithme Path Vector** pour :

1. **Sélectionner le meilleur chemin** basé sur les attributs de chemin
2. **Prévenir les boucles de routage** via l'attribut AS_Path
3. **Permettre les politiques administratives** pour contrôler le flux de trafic

### Prévention des Boucles (Loop Prevention)

**AS_Path** : Attribut obligatoire BGP contenant la liste des AS traversés pour atteindre une destination.

**Mécanisme de prévention** :
- Lors de la réception d'une annonce de route, un routeur vérifie l'AS_Path
- Si son propre ASN est dans le chemin, la route est rejetée
- Si le routeur annonce une route externe reçue, il ajoute son ASN au début du chemin

**Exemple** :
```
AS 100 → 200 → 300 → 400
AS 200 reçoit cette annonce et voit que 200 est déjà dans AS_Path
La route est REJETÉE (boucle évitée)
```

## BGP Sessions et Communications

### Paramètres de Session BGP

| Paramètre | Valeur | Description |
|-----------|--------|-------------|
| Port TCP | 179 | Port standard BGP |
| Keepalive | 60 sec (défaut) | Intervalle entre les keepalives |
| Hold Time | 180 sec (défaut) | Délai avant considérer la session morte |
| Hold Timer | 3 × Keepalive | Valeur négociée (la plus basse gagne) |

### Établissement de Session BGP

1. **TCP 3-way handshake** sur port 179
2. **Échange de OPEN message** (ASN, BGP ID, Hold Time)
3. **Synchronisation** avec KEEPALIVE
4. **État ESTABLISHED** pour commencer l'échange de routes
5. **UPDATE messages** contiennent les annonces et les retraits de routes

## Address Families et MP-BGP

### Address Families (AFI/SAFI)

| AFI | SAFI | Description | Usage |
|-----|------|-------------|-------|
| 1 (IPv4) | 1 | Unicast IPv4 | Routage standard |
| 1 (IPv4) | 2 | Multicast IPv4 | Routage multicast |
| 2 (IPv6) | 1 | Unicast IPv6 | Routage IPv6 |
| 2 (IPv6) | 2 | Multicast IPv6 | Routage multicast IPv6 |
| 1 (IPv4) | 128 | MPLS-labeled IPv4 | MPLS |

### MP-BGP (Multiprotocol BGP)

**MP-BGP** permet à une seule session BGP de supporter plusieurs address families :

```
router bgp 100
  address-family ipv4 unicast
    network 10.0.0.0 mask 255.255.255.0
  address-family ipv6 unicast
    network 2001:db8::/32
```

**Avantages** :
- Une seule session TCP pour plusieurs familles d'adresses
- Réduction de la surcharge
- Gestion simplifiée des politiques cross-family

## Path Attributes

### Attributs Obligatoires

| Attribut | Type | Description |
|----------|------|-------------|
| AS_Path | Bien-connu Obligatoire | Chemin des AS parcourus |
| Origin | Bien-connu Obligatoire | IGP, EGP, ou Incomplete (?) |
| Next Hop | Bien-connu Obligatoire | Adresse IP du prochain saut |

### Attributs Optionnels (Communs)

| Attribut | Description | Impact |
|----------|-------------|--------|
| Local Preference | Préférence locale (0-4294967295) | Contrôle les routes sortantes |
| MED (Multi-Exit Discriminator) | Métrique de sortie (0-4294967295) | Recommandation au peering AS |
| Community | Tags pour les politiques | Flexible, réutilisable |

### Ordre de Préférence Générique

1. **Weight** (Cisco propriétaire) : 0-65535, plus élevé = meilleur
2. **Local Preference** (iBGP) : 0-4294967295, plus élevée = meilleure
3. **Locally originated** routes (200 vs 20 AD)
4. **AS_Path length** : Plus court = meilleur
5. **Origin** : IGP > EGP > Incomplete
6. **MED** (entre même AS) : Moins élevé = meilleur
7. **Préférence eBGP vs iBGP**
8. **IGP cost** pour next-hop
9. **Égalité** : Route ID, peer IP

## Configuration BGP de Base

### Démarrage de BGP

```cisco
! Sur un routeur Cisco
router bgp 100
  bgp router-id 1.1.1.1
  neighbor 10.1.1.1 remote-as 200
  neighbor 10.2.2.2 remote-as 100
  address-family ipv4 unicast
    network 192.168.0.0 mask 255.255.255.0
    neighbor 10.1.1.1 activate
    neighbor 10.2.2.2 activate
    no auto-summary
```

### Commandes de Diagnostic

```cisco
show ip bgp summary                    ! Résumé des sessions BGP
show ip bgp neighbors 10.1.1.1         ! Détails voisin BGP
show ip bgp neighbors 10.1.1.1 received-routes  ! Routes reçues
show ip bgp neighbors 10.1.1.1 advertised-routes ! Routes annoncées
show ip bgp [prefix]                  ! Détails route BGP
show ip route bgp                      ! Routes BGP dans RIB
clear ip bgp *                         ! Réinitialiser sessions BGP
```

## Points Importants à Retenir

1. **BGP est un protocole Path Vector**, pas basé sur la métrique simple
2. **L'attribut AS_Path** prévient intrinsèquement les boucles de routage
3. **Distance administrative** : eBGP=20, iBGP=200
4. **TCP port 179** est utilisé pour toutes les sessions BGP
5. **ASN 16-bit privés** : 64512-65535 ; **32-bit** : 4200000000-4294967294
6. **MP-BGP** permet plusieurs familles d'adresses sur une session
7. **BGP Router ID** doit être unique dans l'AS
8. **Next Hop** change en eBGP, reste le même en iBGP (normalement)
9. **Local Preference** contrôle les routes **sortantes** (iBGP)
10. **MED** recommande les routes **rentrantes** au peering AS
