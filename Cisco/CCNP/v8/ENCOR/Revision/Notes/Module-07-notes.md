# Module 7 : EIGRP - Notes Détaillées

## Introduction

EIGRP (Enhanced Interior Gateway Routing Protocol) est un protocole de routage propriétaire Cisco qui combine les avantages des protocoles de vecteur de distance (efficacité) et de l'état de lien (convergence rapide). Le Module 6 a couvert les concepts d'routing fondamentaux ; ce module approfondit EIGRP comme l'un des protocoles les plus robustes et performants pour les réseaux d'entreprise modernes. EIGRP utilise l'algorithme DUAL pour garantir une convergence sans boucles et une haute vitesse.

## Concepts Clés

- **DUAL (Diffusing Update Algorithm)** : Algorithme breveté pour sélection de route et prévention de boucles
- **Successor** : Route primaire vers une destination (meilleure métrique)
- **Feasible Successor** : Route de secours valide sans boucles
- **Topology Table** : Base de données contenant toutes les routes potentielles
- **Neighbors** : Routeurs adjacents EIGRP
- **Feasible Distance (FD)** : Métrique totale vers une destination via le successor
- **Advertised Distance (AD)** : Métrique depuis un voisin vers une destination
- **ECMP/Variance** : Équilibrage de charge égal et inégal

## 1. Fondamentaux EIGRP

### Caractéristiques Principales

**EIGRP est un protocole hybride** :
- Plus efficace en bande passante que les protocoles distance vector classiques
- Plus rapide en convergence que les protocoles link-state purs
- Meilleur utilisation des ressources (CPU, mémoire, bande passante)

**Avantages clés** :
- ✓ Convergence rapide (utilise DUAL)
- ✓ Bande passante réduite (inc. uniquement changements)
- ✓ Mises à jour incrémentales non périodiques
- ✓ Supporte VLSM et CIDR
- ✓ Métriques composites (Bande passante, Délai, Fiabilité, Charge, MTU)
- ✓ Scalabilité excellente (224 sauts max vs 15 RIP)
- ✓ Authentification MD5 et HMAC
- ✓ Supporte multi-VRF
- ✓ Convergence multi-voie (ECMP/Unequal-cost)

### Topologie de Réseau EIGRP

```
Routeur A ← Hello/Update → Routeur B
   ↓                          ↓
Topology Table      Topology Table
   ↓                          ↓
RIB/FIB Install      RIB/FIB Install
   ↓                          ↓
Data Forwarding    Data Forwarding
```

## 2. Formation et Maintenance de Voisinage

### Découverte de Voisins

EIGRP utilise les paquets **Hello** pour découvrir et maintenir les voisinages.

#### Paramètres Hello (par défaut)

| Interface Type | Hello Interval | Hold Time |
|---|---|---|
| **Ethernet/Fast Ethernet** | 5 secondes | 15 secondes (3×Hello) |
| **Serial < 1.544 Mbps** | 60 secondes | 180 secondes (3×Hello) |
| **Serial ≥ 1.544 Mbps** | 5 secondes | 15 secondes |

**Hold Time** : Délai avant de déclarer un voisin inaccessible.

#### Conditions de Voisinage

Pour qu'un routeur EIGRP voisin soit reconnu :
1. Routeurs sur le même segment de lien (adjacence directe)
2. **Même numéro de processus AS (Autonomous System)**
3. **K values identiques** (K1, K2, K3, K4, K5)
4. **Même réseau IP** (interfaces sur même sous-réseau)
5. Pas d'authentification requise par défaut

**IMPORTANT** : Si les K values diffèrent, le lien ne devient pas actif (routeur remet en voisin passif - state down).

### Configuration de Voisinage

```
! Activation simple
router eigrp 100
 network 192.168.1.0
 network 192.168.2.0

! Timers personnalisés (sur l'interface)
interface Gi0/0
 ip hello-interval eigrp 100 10   ! Hello tous les 10 sec
 ip hold-time eigrp 100 30        ! Hold après 30 sec

! Vérification
show ip eigrp neighbors
show ip eigrp neighbors detail
```

## 3. Topology Table et DUAL

### Topology Table (Table de Topologie)

La **Topology Table** est la base de données centrale d'EIGRP. Elle contient :
- Tous les chemins appris (pas seulement le meilleur)
- Feasible Distance (FD) pour chaque route
- Advertised Distance (AD) depuis chaque voisin
- État de sélection (Successor/Feasible Successor)

**Entrée Topology Table** :
```
P 192.168.1.0/24, 1 successors, FD is 2560
      via 192.168.1.1 (2560/2560), Serial 0/0
      via 192.168.1.2 (3072/2560), Serial 0/1  ← Feasible Successor
```

**Signification** :
- FD = 2560 : Métrique totale via le meilleur chemin
- via 192.168.1.1 (2560/2560) : Métrique locale / AD du voisin
- via 192.168.1.2 (3072/2560) : Métrique locale / AD du voisin (valide comme backup)

### DUAL - Diffusing Update Algorithm

DUAL est l'algorithme qui détermine le Successor et les Feasible Successors.

#### Concept de Feasible Successor

Une route est un **Feasible Successor** si :
$$Advertised \, Distance \, (du \, voisin) < Feasible \, Distance \, (actuel)$$

**Exemple** :
- Lien actuel (Successor) : FD = 2560, AD = 2560
- Lien candidat (possible FS) : AD = 2048
- Test : 2048 < 2560 ? **OUI** → C'est un Feasible Successor
- Avantage : Convergence INSTANTANÉE (pas de requête)

#### Successor vs Feasible Successor

| Aspect | Successor | Feasible Successor |
|--------|-----------|-------------------|
| **Rôle** | Route primaire | Route backup (standby) |
| **Utilisation** | Transport normal du trafic | Activé seulement si successor échoue |
| **Sélection** | Métrique la plus basse | AD candidate < FD successor |
| **Convergence** | Immédiate si FS disponible | Sinon recherche DUAL active |

### DUAL Active Process

Quand un Successor devient inaccessible **ET pas de Feasible Successor** :
1. Route entre en état **ACTIVE**
2. EIGRP envoie **QUERY** à tous les voisins
3. Voisins répondent avec **REPLY**
4. Nouvelle route sélectionnée
5. Route revient à état **PASSIVE**

**Temps Active** : Peut causer un délai si pas de Feasible Successor (par défaut 3 min max).

**Commandes** :
```
show ip eigrp topology          ! Topology table
show ip eigrp topology active   ! Routes en active
debug eigrp packets             ! Trace QUERY/REPLY
```

## 4. Calcul des Métriques

### Métriques Classiques vs Wide Metrics

EIGRP supporte deux formats de métriques :

#### Métriques Classiques (16 bits)
- Utilisées sur tous les routeurs Cisco modernes
- Maximum 32 bits (compréhensibilité)
- Formule : $Metrique = K_1 \times BW + \frac{K_2 \times BW}{256 - Load} + K_3 \times Delay$

#### Wide Metrics (64 bits)
- Support pour les liens très rapides (100G+)
- Plus de précision
- Pas compatible directement avec métriques classiques

### K Values et Métrique Composite

**K values par défaut** :
- K1 = 1 (Bandwidth - activé)
- K2 = 0 (Load - désactivé)
- K3 = 1 (Delay - activé)
- K4 = 0 (Reliability - désactivé)
- K5 = 0 (MTU - désactivé)

**Métrique par défaut** : $Metrique = BW + Delay$

### Composants de la Métrique

#### 1. Bande Passante (Bandwidth)
- **Bande passante MINIMALE** du chemin
- Pas la somme, mais le lien le plus lent
- Unité : kbps (kilobits par seconde)
- Formule : $BW = \frac{10^7}{Bande \, passante \, min \, (kbps)}$

**Exemples** :
```
FastEthernet 100 Mbps = 10^7 / 100,000 = 100
GigabitEthernet 1000 Mbps = 10^7 / 1,000,000 = 10
Serial 64 kbps = 10^7 / 64 = 156,250
```

#### 2. Délai (Delay)
- **Somme** de tous les délais du chemin
- Unité : microsécondes (µsec)
- Par défaut : 10 µsec par saut (Ethernet)
- Formule dans métrique : $Delay = \frac{Retard \, total}{10}$

**Valeurs par défaut** :
```
Ethernet : 10 µsec
Serial T1 (1.544 Mbps) : 20,000 µsec
Serial 64k : 20,000 µsec
FastEthernet : 100 µsec
GigabitEthernet : 10 µsec
```

#### 3. Fiabilité (Reliability)
- Pourcentage de paquets transmis sans erreur
- Activée si K4 ≠ 0
- Rarement utilisée en moderne (utilice K4=0)

#### 4. Charge (Load)
- Utilisation de l'interface
- Activée si K2 ≠ 0
- Rarement utilisée (utilise K2=0)

#### 5. MTU (Maximum Transmission Unit)
- Taille maximale du paquet
- Activée si K5 ≠ 0
- Rarement modifiée (utilise K5=0)

### Configuration de K Values

```
router eigrp 100
 metric weights 0 K1 K2 K3 K4 K5
 metric weights 0 1 0 1 0 0    ! Override (K1=1, K3=1, autres=0)

! Les voisins ne deviennent adjacents que si K values identiques
! Si K values divergent : routeurs restent voisins mais pas actifs
```

## 5. Détection de Défaillance et Timers

### Timers EIGRP

#### Hello Interval
- Fréquence envoi de paquets Hello
- Par défaut : 5 sec (Ethernet), 60 sec (Serial <1.544M)
- Configurable par interface

#### Hold Time
- Délai avant déclaration neighbor down
- Par défaut : 3 × Hello Interval (15 sec Ethernet)
- Peut être différent que Hello Interval
- Négocié lors formation voisinage (prend la valeur reçue)

### Configuration des Timers

```
! Globalement (par type interface)
router eigrp 100
 timers active-time 3          ! Délai max recherche DUAL active (3 min)
 timers hello-interval eigrp 100 10
 timers hold-time eigrp 100 30

! Par interface
interface Gi0/0
 ip hello-interval eigrp 100 3    ! Hello tous les 3 sec
 ip hold-time eigrp 100 10        ! Hold après 10 sec
```

### Convergence

**Convergence rapide** est l'avantage clé d'EIGRP :
- Avec Feasible Successor : < 100 ms
- Sans FS (DUAL active) : quelques secondes
- Pas de boucles durant la transition

## 6. Route Summarization (Agrégation)

### Résumé Réseau (Manual Summarization)

Combine plusieurs routes en une seule route agrégée pour réduire taille de la table.

#### Résumé Automatique

Par défaut, EIGRP résume les routes à la limite de classe :
```
router eigrp 100
 auto-summary  ! Activé par défaut (peut causer problèmes)
```

Exemple : Routes 192.168.1.0/24, 192.168.2.0/24 résumées en 192.168.0.0/16

#### Résumé Manuel (Interface)

```
interface Gi0/0
 ip summary-address eigrp 100 192.168.0.0 255.255.0.0
```

- Crée une route agrégée
- Résume plusieurs routes
- Meilleure contrôle que auto-summary
- ✓ Recommandé en production

### Avantages du Résumé

| Avantage | Détail |
|----------|--------|
| Réduction table de routage | Moins de routes dans RIB/FIB |
| BW réduite | Nécessite moins de mises à jour |
| CPU/Mémoire | Moins de traitement |
| Stabilité | Défaillances se propagent moins |
| Scalabilité | Réseaux plus grands gérables |

## 7. Load Balancing - ECMP et Variance

### ECMP (Equal-Cost Multipath)

**Configuration** :
```
router eigrp 100
 maximum-paths 4   ! 1-16, par défaut 4
 variance 1        ! ECMP exact (une seule métrique acceptée)
```

Distribue trafic sur chemins avec MÊME métrique.

### Unequal-Cost Load Balancing

```
router eigrp 100
 maximum-paths 6
 variance 2        ! Accepte chemins jusqu'à 2× meilleur chemin
```

**Acceptation** : $Metrique_{alt} \leq Variance \times Metrique_{successor}$

### Détails ECMP vs Unequal-Cost

| Propriété | ECMP (V=1) | Unequal (V>1) |
|-----------|-----------|---------------|
| **Conditions** | Métriques identiques | Métriques différentes |
| **Formule acceptation** | = FD | ≤ V × FD |
| **Distribution** | Equal split | Per-destination basis |
| **Avantages** | Optimal, simple | Utilise toutes les routes |
| **Risques** | Limite nombre de chemins | Peut charge asymétrique |

### Vérification

```
show ip route                    ! Montre toutes les routes ECMP/Unequal
show ip eigrp topology [prefix]  ! Montre successors et FS
debug eigrp packets              ! Trace les mises à jour
```

## 8. Points Importants à Retenir

**Hiérarchie DUAL** :
1. Successor = meilleure métrique
2. Feasible Successor = backup sans boucles valides
3. Si pas FS → DUAL active query

**Métrique EIGRP** :
- Défaut : BW + Delay (K1=1, K3=1, autres=0)
- BW = inverse de la bande passante minimale
- Delay = somme des délais

**Voisinage** :
- K values doivent être IDENTIQUES
- Numéro AS doit être IDENTIQUE
- Même sous-réseau nécessaire

**Timers** :
- Hello 5 sec (Ethernet), 60 sec (Serial <1.544M)
- Hold = 3 × Hello
- Active timeout = 3 min

**Configuration clés** :
```
router eigrp 100
 no auto-summary          ! Bon practice (évite problèmes)
 maximum-paths 4          ! ECMP/Unequal
 variance 2               ! Pour unequal-cost
```

---

**Temps d'étude estimé** : 3h00  
**Préalables** : Module 6 (IP Routing Essentials)  
**Module suivant** : Module 8 - OSPF (pour comparaison de protocoles de routage)
