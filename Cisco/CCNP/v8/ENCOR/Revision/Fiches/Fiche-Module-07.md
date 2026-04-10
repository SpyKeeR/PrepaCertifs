# Fiche Révision Module 7 : EIGRP

## 1. Hiérarchie de Sélection de Route EIGRP

```
EIGRP ROUTE SELECTION
├── Successor
│   └── Route avec métrique la plus BASSE
│   └── Installée dans RIB/FIB immédiatement
├── Feasible Successor (Backup)
│   └── Condition : AD_voisin < FD_actuel
│   └── Prêt à l'emploi si Successor défaille
└── Routes nulles
    └── Pas de FS → DUAL ACTIVE (query/reply)
```

## 2. Métriques EIGRP - Formule Simplifiée

### Par Défaut (K1=1, K3=1, autres=0)
$$Metrique = BW + Delay$$

### Composants

| Composant | Définition | Formule |
|---|---|---|
| **BW** | Bande passante MIN du chemin | $BW = \frac{10^7}{BP_{min}(kbps)}$ |
| **Delay** | SOMME des délais du chemin | $Delay = \frac{Retard_{total}}{10}$ |
| **Fiabilité** | % paquets reçus sans erreur | Activée si K4 ≠ 0 |
| **Load** | Utilisation interface | Activée si K2 ≠ 0 |
| **MTU** | Paquet max du chemin | Activée si K5 ≠ 0 |

### Valeurs Typiques BW Composant
```
64 kbps Serial     → BW = 10^7 / 64 = 156,250
1.544 Mbps T1      → BW = 10^7 / 1,544 = 6,476
10 Mbps Ethernet   → BW = 10^7 / 10,000 = 1,000
100 Mbps Fast-E    → BW = 10^7 / 100,000 = 100
1000 Mbps Gig-E    → BW = 10^7 / 1,000,000 = 10
```

## 3. Timers EIGRP - Par Défaut

| Type Interface | Hello | Hold | Ratio Hold:Hello |
|---|---|---|---|
| Ethernet | 5 sec | 15 sec | 3:1 |
| Fast Ethernet | 5 sec | 15 sec | 3:1 |
| Gigabit Ethernet | 5 sec | 15 sec | 3:1 |
| Serial ≥1.544M | 5 sec | 15 sec | 3:1 |
| Serial <1.544M | 60 sec | 180 sec | 3:1 |

**Hold Time TOUJOURS = 3 × Hello interval par défaut**

## 4. Conditions Voisinage EIGRP

✓ **DOIVENT correspondre** : K values (K1-K5)  
✓ **DOIVENT correspondre** : Numéro AS (Autonomous System)  
✓ **DOIVENT correspondre** : Même sous-réseau IP  
✓ **Peuvent différer** : Hold time (prend valeur reçue)  
✗ **N'est PAS nécessaire** : Authentification (optionnelle)

**Impact divergence K-values** : Routeurs détectent voisin mais ne deviennent pas ADJACENTS (état down/passive)

## 5. DUAL Algorithm - Concepts

### Termes Clés

| Terme | Définition |
|---|---|
| **FD (Feasible Distance)** | Métrique TOTALE du meilleur chemin (Successor) |
| **AD (Advertised Distance)** | Métrique du VOISIN jusqu'à la destination |
| **Successor** | Route primaire (meilleure métrique) |
| **Feasible Successor** | Route backup valide sans boucles |

### Test Feasible Successor

**Condition** : $AD_{voisin} < FD_{actuel}$

**Exemple** :
```
Successor : FD = 2560
  └─ via 10.0.0.1/AD=2560

Candidat FS : 
  └─ via 10.0.0.2/AD=2048

Test : 2048 < 2560 → OUI ✓ C'est un FS valide
```

### DUAL Active vs Passive

| État | Condition | Action | Convergence |
|---|---|---|---|
| **PASSIVE** | Route stable | Installation RIB | Instantanée |
| **ACTIVE** | Successor défaillant, pas FS | QUERY/REPLY voisins | Quelques sec |

## 6. Commandes Essentielles

### Configuration

```bash
# Activation EIGRP
router eigrp <AS-number>
 network <classful-network>
 metric weights 0 <K1> <K2> <K3> <K4> <K5>  # Override K values
 maximum-paths <1-16>                         # ECMP (défaut 4)
 variance <multiplicateur>                    # Unequal-cost (défaut 1)
 no auto-summary                              # Bon practice

# Configuration Interface
interface <interface>
 ip hello-interval eigrp <AS> <secondes>
 ip hold-time eigrp <AS> <secondes>
 ip summary-address eigrp <AS> <network> <mask>
 bandwidth <kbps>                             # Modifie métrique BW
 delay <tens-of-microseconds>                 # Modifie métrique Delay
```

### Vérification

```bash
show ip eigrp neighbors
show ip eigrp neighbors detail
show ip eigrp topology               # Topology table complète
show ip eigrp topology <prefix>      # Info spécifique
show ip eigrp topology active        # Routes en ACTIVE
show ip route                        # RIB/FIB
show ip route eigrp                  # Routes EIGRP seulement
show ip protocols                    # Résumé EIGRP activation
```

### Dépannage

```bash
debug eigrp packets                  # HELLO, UPDATE, QUERY, REPLY
debug eigrp fsm                      # FSM DUAL state transitions
debug ip eigrp                       # Informations générales
debug ip eigrp summary               # Résumé des événements
```

## 7. Load Balancing Configurations

### ECMP (Exact Cost)
```
router eigrp 100
 maximum-paths 4        # Par défaut
 variance 1             # ECMP seulement (défaut)
```
**Utilisation** : Toutes les routes avec métrique = FD

### Unequal-Cost Load Balancing
```
router eigrp 100
 maximum-paths 6
 variance 2             # Accepte jusqu'à 2× FD
```
**Utilisation** : Routes où FD_alt ≤ 2 × FD_best

### Exemple Calcul Unequal-Cost
```
Successor : FD = 1000
Variance = 2

Limite acceptée : 2 × 1000 = 2000

Routes candidates :
  - 1000 → OUI (ECMP)
  - 1500 → OUI (1500 ≤ 2000)
  - 2000 → OUI (2000 ≤ 2000)
  - 2100 → NON (2100 > 2000)
  - 3000 → NON (3000 > 2000)
```

## 8. Route Summarization

### Manuel (Recommandé)
```bash
interface Gi0/0
 ip summary-address eigrp <AS> <network> <mask>
```
- Crée route agrégée
- Réduit taille topology table
- Meilleur contrôle = production

### Automatique (Legacy - À éviter)
```bash
router eigrp 100
 auto-summary
```
- Résume aux limites de classe B/C/A
- Peut causer problèmes discontigus
- Non recommandé en moderne

## 9. Mind Map Texte - Vue Complète EIGRP

```
EIGRP
├── Voisinage
│   ├── Hello interval
│   ├── Hold time (3× Hello)
│   ├── K values (DOIVENT matcher)
│   └── AS number (DOIT matcher)
├── Topology Table
│   ├── Successor (meilleure métrique)
│   ├── Feasible Successor (backup AD < FD)
│   ├── Autres routes candidates
│   └── DUAL test
├── Métriques (Par défaut : BW + Delay)
│   ├── BW = 10^7 / MIN_BW
│   ├── Delay = somme / 10
│   └── K-values (K1=1, K3=1 défaut)
├── DUAL Convergence
│   ├── Passive (stable)
│   ├── Active (FS manquant, QUERY/REPLY)
│   └── Rapid failover (< 100ms avec FS)
├── Load Balancing
│   ├── ECMP (variance 1, métriques égales)
│   └── Unequal (variance >1, ratio limité)
└── Summarization
    ├── Manuel (interface)
    └── Automatique (limite classe)
```

## 10. Checklist Configuration EIGRP

- [ ] AS number configuré et actif
- [ ] K values vérifiées (défaut 1 0 1 0 0)
- [ ] Network statements configurés (classful)
- [ ] no auto-summary activé (modern)
- [ ] Voisinage: lister avec `show ip eigrp neighbors`
- [ ] Topology stable (show ip eigrp topology)
- [ ] Routes dans RIB (show ip route eigrp)
- [ ] ECMP/Variance configuré si nécessaire
- [ ] Timers personnalisés testés si appliquable
- [ ] Authentification MD5/SHA si requis

## 11. Formule EIGRP Complète

$$Metrique = [K_1 \times BW + \frac{K_2 \times BW}{256-Load} + K_3 \times Delay + K_4 \times Reliability + K_5 \times MTU] \times 256$$

**Avec K values défaut (1, 0, 1, 0, 0)** :
$$Metrique = (BW + Delay) \times 256$$

Le ×256 est interne Cisco (cosmétique, ne change pas comparaison)

## 12. Pièges Courants à Éviter

❌ K values différents entre voisins → Pas adjacence active  
❌ AS numbers différents → Pas voisinage du tout  
❌ Auto-summary avec réseaux discontigus → Problèmes de routage  
❌ Variance trop élevée → Unequal-cost agressif , possibles boucles  
❌ Oublier no auto-summary dans configuration moderne  
❌ Hold time plus bas que pour recevoir Hello → Déclaration prématurée  
❌ Négliger interface bandwidth pour calcul BW composant

---
**Temps révision** : 40 min | **Niveau** : Intermédiaire
