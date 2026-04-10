# Module 13 : Multicast

## Introduction

Le multicast permet la transmission **un-à-plusieurs** (one-to-many) d'une source vers plusieurs récepteurs. Contrairement à l'unicast (1-to-1) et au broadcast (1-to-all sur le LAN), le multicast utilise un adressage spécialisé et des protocoles de gestion pour optimiser l'utilisation de la bande passante réseau.

## Multicast Fundamentals

### Concept du Multicast

**Multicast** : Mécanisme réseau permettant une source d'envoyer du trafic une seule fois, et le réseau le réplique vers plusieurs destinations intéressées.

**Cas d'usage** :
- Diffusion de vidéos/audio (IPTV, conférences)
- Mise à jour logicielle distribuée
- Jeux en ligne multijoueurs
- Applications financières temps réel

### Modèles de Communication

| Modèle | Source | Destinations | Exemples |
|--------|--------|--------------|----------|
| **Unicast** | 1 | 1 | HTTP, Email, SSH |
| **Broadcast** | 1 | All (LAN only) | ARP, DHCP discovery |
| **Multicast** | 1 | Many (Selected) | IPTV, Vidéo streaming |
| **Anycast** | 1 | Nearest | DNS, LISP |

## Adressage Multicast

### Plage d'Adresses Class D

**Classe D IPv4** : `224.0.0.0/4` (224.0.0.0 à 239.255.255.255)

| Plage | Usages |
|-------|--------|
| `224.0.0.0/24` | Reserved (lien-local) |
| `224.0.1.0 - 224.0.1.255` | Globally scoped |
| `224.1.0.0 - 224.251.255.255` | Globally scoped |
| `224.252.0.0 - 224.255.255.255` | Administratively scoped |
| `239.0.0.0 - 239.255.255.255` | Administratively scoped |

### Mappage Adresse MAC Multicast

**Mapping IPv4 Multicast → MAC Layer** :

Format MAC multicast : `01:00:5E:xx:xx:xx`

**Processus** :
1. Prendre l'adresse multicast IPv4 (ex: `224.10.20.30`)
2. Garder les 23 bits bas (ignorer les 9 bits hauts)
3. Mapper vers le préfixe `01:00:5E` + 23 bits bas

**Exemple** :
```
Multicast IPv4 : 224.10.20.30
Binaire :        224=11100000, 10=00001010, 20=00010100, 30=00011110
23 bits bas :    00001010 00010100 00011110 (0A:14:1E)
MAC multicast :  01:00:5E:0A:14:1E
```

### IPv6 Multicast

**Plage IPv6 Multicast** : `ff00::/8`

**Format** :
- Préfixe : `ff` (FF00::/8)
- Niveau de scope (4 bits) : 1=Node, 2=Link, 5=Site, 8=Org, E=Global
- Group ID 112 bits

**Exemple** : `ff02::1` (All Nodes sur le lien local)

## IGMP (Internet Group Management Protocol)

### IGMP Versions

| Version | Catégorie | Timeout | Features |
|---------|-----------|---------|----------|
| **IGMPv1** | Obsolète | Quelques min | Basique, pas de lien-local |
| **IGMPv2** | Standard | 260 sec | Leave messages explicites |
| **IGMPv3** | Moderne | Configurable | Filtre source (Source-Specific) |

### IGMPv2 (Standard Actuel)

**Membres du groupe IGMP** :

1. **Host Interested in Group**
   - Envoie IGMP MEMBERSHIP REPORT au groupe
   - Reçoit le trafic multicast du groupe

2. **Host NOT Interested in Group**
   - Envoie IGMP LEAVE MESSAGE (IGMPv2)
   - Cesse de recevoir le trafic

3. **Querier (Routeur)**
   - Envoie périodiquement MEMBERSHIP QUERY
   - Collecte les REPORTS pour connaître les groupes actifs

**Timers** :
- Query Interval : 125 sec (défaut)
- Max Response Time : 10 sec (défaut)
- Group Membership Interval : 260 sec

### IGMPv3 (Source-Specific Multicast)

**Avancé** : Permet de spécifier les sources autorisées pour un groupe.

**Message** : `Group,Source List`
```
(Group=224.10.0.1, Sources={10.1.1.1, 10.2.2.2})
```

**Modes** :
- **INCLUDE** : Accepter seulement de ces sources
- **EXCLUDE** : Accepter de toutes SAUF ces sources

## IGMP Snooping

### Concept

**IGMP Snooping** : Technique sur les switches Ethernet pour "écouter" les messages IGMP et maintenir une table multicast Layer 2.

**Avantage** : Évite de flood le trafic multicast sur tous les ports (gaspillage BW)

### Fonctionnement

```
Source → Envoie multicast 224.10.0.1
  ↓
Switch écoute IGMP REPORT sur port X
  ↓
Switch maintient : 224.10.0.1 → {Port B, Port C}
  ↓
Trafic multicast copiés vers ports B, C seulement
  ↓
Port A ne reçoit PAS le multicast (pas de report IGMP)
```

### Configuration

```cisco
interface vlan 10
  ip igmp snooping        ! Enable IGMP snooping
  ip igmp snooping querier address 10.1.1.1
```

## PIM (Protocol Independent Multicast)

### Modes PIM

PIM est **Protocol Independent** car il utilise la table de routage unicast existante (pas de topologie séparée).

#### 1. **PIM Dense Mode (DM)**

**Approche** : **Flood & Prune**
- Flood le trafic partout
- Hosts prune les branches non intéressées

**Utilisé** : Petits réseaux, groupes denses (beaucoup de receveurs)

```cisco
router(config-if)# ip pim dense-mode
```

#### 2. **PIM Sparse Mode (SM)** (Recommandé)

**Approche** : **Rendezvous Point (RP)**
- Sources envoient au RP
- Récepteurs s'abonnent au RP
- RP dirige le trafic

**Utilisé** : Réseaux larges, groupes épars

```cisco
router(config-if)# ip pim sparse-mode
```

### Arbre PIM

**RPT (RP Tree)** :
```
Source → RP → Receivers
         ↓
         (Root de l'arbre)
```

**SPT (Shortest Path Tree)** :
```
Source → Receivers
         (Source est root)
         (Meilleure latence)
```

## Rendezvous Points (RP)

### Concept et Fonction

**Rendezvous Point** : Routeur central négocie entre sources et récepteurs multicast.

**Rôle** :
- Reçoit Register messages de sources
- Envoie Join/Prune aux récepteurs
- Dirige le trafic initial (RPT)
- Offre transition vers SPT

### Élection du RP

**PIM Election** : Critère pour élire un RP

```cisco
router(config)# ip pim rp-address 10.1.1.1 10          ! Priority 10 (plus bas = meilleur)
```

**BSR (Bootstrap Router)** : Découverte automatique du RP

```cisco
router(config)# ip pim bsr-candidate loopback0 30   ! Candidat avec priorité 30
router(config)# ip pim rp-candidate loopback0
```

### Priorité RP

- **Plage** : 0-255
- **Défaut** : 0 (meilleur)
- **Plus petit = Meilleur**

```cisco
ip pim rp-address 10.1.1.1 0      ! Priorité 0 = Élu
ip pim rp-address 10.2.2.2 100    ! Priorité 100 = Backup
```

## MDT (Multicast Distribution Tree)

### Types d'Arbres Multicast

#### RPT (RP Tree)

```
        RP (Root)
        /|\
       / | \
    R1  R2 R3
    |    |  |
    H1  H2 H3
```

**Caractéristiques** :
- RP au centre
- Optimal pour récepteurs épars
- Source → RP → Récepteurs

#### SPT (Source-Specific Tree)

```
    Source (Root)
      /|\
     / | \
    R1 R2 R3
    |  |  |
   H1 H2 H3
```

**Caractéristiques** :
- Source au root
- Optimal pour latence
- Meilleur chemin source-récepteur
- RPT → SPT transition automatique

### MDT Construction

```
1. Source envoie trafic multicast
2. Récepteur interesse envoie IGMP REPORT
3. PIM maintient arbre (RPT ou SPT)
4. Trafic suit l'arbre
5. Branches prunées si pas d'intérêt
```

## Administratively Scoped Multicast

### Concept

**Administratively Scoped** : Adresse multicast avec restriction de portée.

**Plage standard** : `239.0.0.0/8`

**Boundaries** : Routeurs n'envoient pas ces groupes au-delà d'une limite configurée.

```cisco
router(config)# pim boundary access-list 10 filter-autorp
ip access-list extended filter-autorp
  deny udp any any range 496 497
```

## GLOP Addressing

### Concept GLOP (RFC 3180)

**GLOP** : Réservation globale d'adresses multicast basée sur l'ASN.

**Format** : `233.ASN.0.0/16`

**Exemple** : ASN 64500 → `233.252.244.0/16` (64500 = 0xFBF4 en hex)

**Avantage** : Unicité globale sans coordination centrale

## Configuration Multicast Complète

### Routeur Multicast Basique

```cisco
! Enable PIM
router(config)# ip multicast-routing
router(config)# ip pim rp-address 10.1.1.1

! Sur interfaces
router(config-if)# ip pim sparse-mode
router(config-if)# ip igmp version 3
router(config-if)# ip igmp query-interval 125
router(config-if)# ip igmp query-max-response-time 10
```

### Vérification

```cisco
show ip mroute                           ! Routage multicast
show ip mroute [group]                   ! Détails groupe
show ip pim neighbor                     ! Voisins PIM
show ip pim rp [mapping]                 ! RP mappings
show ip igmp groups                      ! IGMP groups joints
show ip igmp groups [interface]          ! Groups sur interface
debug ip igmp                             ! Debug IGMP
debug ip pim                              ! Debug PIM
```

## Points Importants à Retenir

1. **Multicast = 1-to-Many** via adresses Class D (224.0.0.0/4)
2. **MAC multicast** : `01:00:5E` + 23 bits bas d'IP multicast
3. **IGMP** : Protocole hôte-routeur; IGMPv3 supporte Source-Specific Multicast
4. **IGMP Snooping** : Switch Layer 2 écoute IGMP pour LAN multicast optimal
5. **PIM** : Utilise table unicast; Mode Sparse-Mode (+ RP) recommandé
6. **RP** : Central pour SPM; élection basée sur priorité
7. **RPT vs SPT** : RPT initial, transition SPT si nécessaire (source directe)
8. **MDT** : Arbre multicast distribue trafic aux récepteurs
9. **ASN boundaries** : Restrictrion portée avec administratively scoped
10. **GLOP** : Réservation unique multicast via ASN (233.ASN.0.0/16)
