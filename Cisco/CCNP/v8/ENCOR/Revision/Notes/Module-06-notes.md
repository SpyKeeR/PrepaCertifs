# Module 6 : IP Routing Essentials - Notes Détaillées

## Introduction

Le routage IP est la base du fonctionnement des réseaux modernes. Ce module couvre les concepts fondamentaux du routage, incluant les différentes classifications des protocoles de routage, les processus de sélection des chemins, et les technologies essentielles comme le VRF (Virtual Routing and Forwarding). Comprendre ces concepts est crucial pour pouvoir configurer et optimiser les solutions de routage dans les réseaux d'entreprise.

## Concepts Clés

- **RIB (Routing Information Base)** : Base de données contenant toutes les routes apprises par les protocoles de routage et du routage statique
- **FIB (Forwarding Information Base)** : Table optimisée utilisée pour la prise de décision de commutation rapide en temps réel
- **Administrative Distance (AD)** : Valeur de confiance accordée à une source de routage (0-255)
- **Métriques** : Valeurs utilisées pour comparer les routes apprises via le même protocole
- **Prefix Length** : Longueur du préfixe réseau (influençant la sélection du chemin le plus spécifique)
- **ECMP** : Equal-Cost Multipath - équilibrage de charge sur plusieurs chemins de coût égal
- **Unequal-Cost Load Balancing** : Équilibrage sur chemins de coûts différents

## 1. Vue d'ensemble des Protocoles de Routage

### Classification des Protocoles de Routage

#### Distance Vector (Protocoles de Vecteur de Distance)

Les protocoles de vecteur de distance déterminent la meilleure route en fonction de la distance vers la destination et de la direction (vecteur).

**Caractéristiques** :
- Utilisent uniquement les informations de voisins directs
- Mises à jour régulières de la table de routage
- Convergence plus lente
- Moins d'utilisation de bande passante pour les mises à jour
- Exemple : RIPv2

**Limitation du "problème du comptage jusqu'à l'infini"** :
- Les protocoles distance vector souffrent d'une convergence lente en cas de défaillance
- Solutions : Split horizon, poison reverse, hold-down timers

#### Enhanced Distance Vector (EIGRP)

EIGRP combine les avantages des protocoles distance vector et link-state.

**Caractéristiques** :
- Envoie des mises à jour uniquement lorsque la topologie change
- Utilise l'algorithme DUAL (Diffusing Update Algorithm)
- Faible consommation de bande passante
- Convergence rapide
- Propriétaire Cisco (bien que dépôt au IANA)

#### Link-State (Protocoles État de Lien)

Les protocoles link-state construisent une carte complète de la topologie du réseau.

**Caractéristiques** :
- Chaque routeur apprend la topologie complète du domaine de routage
- Utilise l'algorithme SPF (Shortest Path First de Dijkstra)
- Convergence rapide en cas de changement
- Consommation mémoire et CPU plus élevée
- Les inondations LSA (Link State Advertisements) sont amorties
- Exemple : OSPF, IS-IS

#### Path Vector (Vecteur de Chemin)

Protocoles de routage inter-domaine utilisés dans les réseaux et internet.

**Caractéristiques** :
- Utilisés pour le routage entre domaines autonomes
- Incluent les attributs du chemin (Path Attributes)
- Exemple : BGP

### Tableau Comparatif des Protocoles

| Aspect | Distance Vector | EIGRP | Link-State |
|--------|-----------------|-------|-----------|
| Espace mémoire | Bas | Moyen | Élevé |
| Utilisation CPU | Basse | Moyenne | Élevée |
| Convergence | Lente | Rapide | Rapide |
| Mises à jour | Périodiques | Basées sur changements | Basées sur changements |
| Scalabilité | Faible | Moyenne-Bonne | Bonne |
| Nombre de sauts max | 15 | 224 | Illimité |

## 2. Sélection des Chemins (Path Selection)

### Processus de Sélection

Le routeur utilise une hiérarchie de critères pour sélectionner la "meilleure" route :

#### 1. Longueur du Préfixe (Prefix Length)

La route avec le préfixe le plus long (le plus spécifique) est toujours préférée.

**Exemple** :
```
Route 1 : 192.168.1.0/24 via OSPF AD 110
Route 2 : 192.168.0.0/16 via RIP AD 120
Destination : 192.168.1.50

Résultat : Route 1 est sélectionnée (préfixe /24 plus long que /16)
```

#### 2. Distance Administrative (AD)

Si plusieurs routes existent avec le même préfixe, celle avec la plus basse AD est choisie.

**Valeurs AD par défaut** :
- Directly connected : 0
- Static route : 1
- EIGRP : 90
- OSPF : 110
- RIPv2 : 120
- External EIGRP : 170
- Unknown : 255 (inaccessible)

**Configuration manuelle d'AD** :
```
ip route 10.0.0.0 255.255.255.0 192.168.1.1 [AD personnalisée]
```

#### 3. Métriques

À AD égale, le protocole utilisant sa métrique pour désigner la meilleure route.

**Métriques par protocole** :
- **RIP** : Nombre de sauts (1-15)
- **EIGRP** : Composite (bande passante, délai, fiabilité, charge, MTU)
- **OSPF** : Coût (inverse de la bande passante : 100,000,000 / BW en bps)
- **IS-IS** : Métrique interne/externe

### ECMP (Equal-Cost Multipath)

Lorsque plusieurs routes ont exactement la même AD et la même métrique :

**Avantages** :
- Équilibrage de la charge
- Utilisation optimale de la bande passante
- Redondance automatique

**Configuration EIGRP ECMP** :
```
router eigrp 100
 maximum-paths 4  ! Par défaut 4, max 16 avec multipath
 variance 1       ! Pour ECMP uniquement
```

**Vérification** :
```
show ip route [destination]
```

### Unequal-Cost Load Balancing

Autorise l'équilibrage sur des routes de coûts différents, contrôlé par le paramètre `variance`.

**Concept** :
```
variance = multiplicateur du coût accepté
Acceptation si : (coût_alternatif ≤ variance × coût_successor)
```

**Configuration EIGRP** :
```
router eigrp 100
 variance 2  ! Accepte les routes avec un coût jusqu'à 2× le meilleur
```

## 3. Routage Statique

### Vision d'ensemble

Le routage statique permet au réseau d'administrateur de définir manuellement les chemins vers les destinations réseau.

### Types de Routes Statiques

#### Route Statique Standard
```
ip route destination mask next-hop-ip [ad] [permanent]
```

**Exemple** :
```
ip route 192.168.2.0 255.255.255.0 192.168.1.1
ip route 0.0.0.0 0.0.0.0 203.0.113.1  ! Route par défaut
```

#### Route Statique Récursive
Le next-hop est résolu via une autre route.

```
ip route 10.0.0.0 255.255.255.0 192.168.1.1
! Le routeur résout d'abord 192.168.1.1
```

#### Route Statique via Interface
Le next-hop est une interface de sortie directe.

```
ip route 10.0.0.0 255.255.255.0 Serial 0/0
```

### Commandes essentielles

```
! Configuration
ip route destination mask next-hop [ad]
ip route destination mask interface [ad]

! Vérification
show ip route
show ip route static
show ip route [destination]
ip route summary

! Suppression
no ip route destination mask next-hop
```

### Avantages et Inconvénients

| Avantage | Inconvénient |
|----------|-------------|
| Pas de surcharge CPU | Pas de scalabilité |
| Pas de converstation | Configuration manuelle |
| Bande passante minimale | Pas d'adaptation aux changements de topologie |
| Sécurité (sélection des routes) | Maintenance complexe |

## 4. Virtual Routing and Forwarding (VRF)

### Concept Fondamental

VRF permet de créer **plusieurs instances de routage indépendantes** sur un seul routeur physique, fonctionnant comme plusieurs routeurs virtuels.

**Cas d'usage** :
- Isolation de clients (MPLS VPN)
- Séparation des réseaux de gestion et de données
- Multi-tenancy
- Réseau d'administration sécurisé (VRF pour les activités de gestion)

### Architecture VRF

Chaque VRF contient :
- **Propre RIB** (Routing Information Base)
- **Propre FIB** (Forwarding Information Base)
- **Propres interfaces**
- **Propres protocoles de routage**
- **Propre table ARP**

### Configuration VRF

#### Création de VRF
```
ip vrf customer-a
 description Client A Network
 rd 65000:100  ! Route Distinguisher pour l'unicité
```

#### Association d'Interface
```
interface Gi0/1
 ip vrf forwarding customer-a
 ip address 192.168.1.1 255.255.255.0
```

#### Configuration de Routage dans VRF
```
router ospf 100 vrf customer-a
 network 192.168.1.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
```

#### Routage Statique dans VRF
```
ip route vrf customer-a 10.0.0.0 255.255.255.0 192.168.2.1
```

### Commandes de Vérification

```
show ip vrf                           ! Lister tous les VRF
show ip vrf detail                    ! Détails avec interfaces
show ip route vrf customer-a          ! Routes dans un VRF spécifique
show ip protocol vrf customer-a       ! Protocoles de routage actifs
ping vrf customer-a destination       ! Ping dans un VRF spécifique
```

### Interconnexion de VRFs

Les VRFs peuvent être interconnectés via des mécanismes comme :
- **VRF Leaking** : Routes importées d'un VRF à l'autre
- **Sub-interfaces** : Chaque VLAN mappé à un VRF différent
- **Virtual Sub-interfaces** : Utiliser des VLANs et des sous-interfaces

**Configuration VRF Leaking** :
```
ip route vrf customer-b 10.0.0.0 255.255.255.0 customer-a 192.168.1.2
```

## 5. RIB et FIB - Détails Techniques

### Routing Information Base (RIB)

**Définition** : Base de données complète contenant toutes les routes candidates.

**Composition** :
- Routes apprises par les protocoles dynamiques
- Routes statiques configurées
- Routes directement connectées

**Processus** :
1. Route entre via protocole ou statique
2. Ad et métrique sont évaluées
3. Meilleure route installée dans le FIB
4. Route affichée avec `show ip route`

### Forwarding Information Base (FIB)

**Définition** : Table de commutation optimisée pour les recherches rapides.

**Caractéristiques** :
- Copie de la meilleure route depuis la RIB
- Optimisée pour la performance (recherche O(1) en hardware)
- Mise à jour en millisecondes
- Contient routes de next-hop immédiat

**Processus CEF (Cisco Express Forwarding)** :
```
RIB → FIB (via CEF adjacency table)
```

**Commandes** :
```
show ip cef                    ! Affiche la FIB
show ip cef 192.168.1.0/24    ! Affiche une entrée FIB spécifique
show ip cef detail             ! Détails avec interfaces de sortie
debug ip cef                   ! Pour le dépannage
```

## 6. Points Importants à Retenir

**Pour l'examen CCNP** :

1. **Hiérarchie de sélection de route** : Prefix length → AD → Métrique
2. **AD par défaut** : Directement connecté (0), Statique (1), EIGRP (90), OSPF (110), RIP (120)
3. **ECMP vs Unequal-Cost** : ECMP = `variance 1`, Unequal = `variance > 1`
4. **VRF** : Instances de routage isolées avec propres RIB/FIB
5. **RIB vs FIB** : RIB = candidates, FIB = utilisée pour la commutation
6. **Métrique OSPF** : Coût = 100,000,000 / Bandwidth(en bps)
7. **Métrique EIGRP** : Basée sur bande passante et délai par défaut
8. **Routage statique** : Bonne AD permet utiliser comme backup

---

**Temps d'étude estimé** : 2h00  
**Préalables** : Concepts IP fondamentaux, modèle OSI  
**Module suivant** : Module 7 - EIGRP (utilise certains concepts du routage essentiels)
