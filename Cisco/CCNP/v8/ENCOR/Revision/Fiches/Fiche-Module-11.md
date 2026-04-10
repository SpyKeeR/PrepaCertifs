# Fiche Rapide Module 11 : BGP Fundamentals

## Terminologie Essentielle

| Terme | Signification |
|-------|--------------|
| **BGP** | Border Gateway Protocol - EGP standard |
| **AS** | Autonomous System - groupe de réseaux sous contrôle unique |
| **ASN** | AS Number - identifiant unique 16 ou 32 bits |
| **eBGP** | BGP entre AS différents (AD 20) |
| **iBGP** | BGP dans le même AS (AD 200) |
| **EGP** | Exterior Gateway Protocol (BGP est le standard) |
| **IGP** | Interior Gateway Protocol (OSPF, EIGRP, RIP) |

## Numérotation AS (ASN)

```
┌─────────────────────────────────────┐
│ ASN 16-bit                          │
├─────────────────────────────────────┤
│ Public:    1-64511, 64512-65534     │
│ Privé:     64512-65535              │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ ASN 32-bit                          │
├─────────────────────────────────────┤
│ Public:    65536+                   │
│ (4200000000-4294967294)             │
└─────────────────────────────────────┘
```

## Path Vector Algorithm

**Boucle Prevention** :
- **AS_Path** = liste des AS sur le chemin
- Un routeur rejette une route si son ASN est dans AS_Path
- Lors de l'annonce, le routeur ajoute son ASN au chemin

**Exemple** : AS100→200→300 annoncé à AS200
→ AS200 voit 200 déjà dans chemin → **REJETTE**

## Paramètres BGP Critiques

| Paramètre | Standard |
|-----------|----------|
| **Port** | TCP 179 |
| **Keepalive** | 60 sec (défaut) |
| **Hold Time** | 180 sec (défaut) |
| **BGP ID** | Identifiant 32-bit unique |
| **Weight (Cisco)** | 0-65535, défaut 0 ou 32768 |

## État AD (Administrative Distance)

```
eBGP:  20 (très fiable, externe)
iBGP:  200 (moins préféré, interne)
```

## Configuration Minimale

```cisco
router bgp 100
  bgp router-id 1.1.1.1
  neighbor 10.1.1.1 remote-as 200          ! eBGP
  neighbor 10.2.2.2 remote-as 100          ! iBGP
  address-family ipv4 unicast
    network 192.168.0.0 mask 255.255.255.0
    neighbor 10.1.1.1 activate
    neighbor 10.2.2.2 activate
```

## Vérification Rapide

```cisco
show ip bgp summary                    ! Résumé sessions
show ip bgp [prefix] [mask]            ! Détails route
show ip bgp neighbors [IP] [option]    ! État voisin/routes
show ip route bgp                      ! Routes BGP actives
```

## Address Families (MP-BGP)

| AFI | SAFI | Description |
|-----|------|-------------|
| 1 | 1 | IPv4 Unicast ✓ Standard |
| 1 | 2 | IPv4 Multicast |
| 2 | 1 | IPv6 Unicast |
| 2 | 2 | IPv6 Multicast |

## Attributs PATH - Ordre de Préférence

1. **Weight** (Cisco) : plus haut = meilleur
2. **Local Preference** (iBGP) : plus haut = meilleur
3. **Routes locales** vs reçues
4. **AS_Path length** : plus court = meilleur  
5. **Origin** : IGP > EGP > Incomplete
6. **MED** : plus bas = meilleur (même AS)
7. **eBGP vs iBGP** : eBGP préféré
8. **IGP cost** pour next-hop
9. **Tie-break** : Router ID, peer IP

## Attributs Obligatoires

- **AS_Path** : Chemin des AS
- **Origin** : IGP/EGP/Incomplete
- **Next Hop** : IP prochain saut

## Session BGP - Processus

```
1. TCP SYN/SYN-ACK/ACK sur port 179
2. OPEN message (ASN, BGP ID, Hold Time)
3. KEEPALIVE réponse (sync)
4. État ESTABLISHED
5. UPDATE messages (routes/retraits)
6. KEEPALIVE périodiquement
```

## Checklist Mini

- ☐ ASN unique par AS
- ☐ BGP Router ID distinct
- ☐ Port TCP 179 accessible
- ☐ Address-family activée
- ☐ Voisins configurés (remote-as)
- ☐ Prefixes annoncés (network)
- ☐ next-hop reachable
- ☐ Pas d'AS_Path loop

## Nuances Importantes

- **eBGP change Next Hop** (incrément +1 en Cisco)
- **iBGP préserve Next Hop** (IBGP constraint)
- **TTL décrémenté** lors de chaque AS (sauf IBGP TTL hacks)
- **BGP ne stabilise PAS** - meilleures routes propagées immédiatement
- **AD iBGP vs IGP** : iBGP 200 > OSPF 110, donc IGP gagne si utilisé
