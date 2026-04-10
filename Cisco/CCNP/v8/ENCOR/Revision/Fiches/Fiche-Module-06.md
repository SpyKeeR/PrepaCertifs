# Fiche Révision Module 6 : IP Routing Essentials

## 1. Classifications des Protocoles de Routage

```
PROTOCOLES DE ROUTAGE
├── Distance Vector
│   └── RIPv2 : Métrique = Nombre de sauts (max 15)
├── Enhanced Distance Vector
│   └── EIGRP : Métrique = Composite (AD=90)
├── Link-State
│   └── OSPF : Métrique = Coût (AD=110)
│   └── IS-IS
└── Path Vector
    └── BGP : Pour le routage inter-domaine
```

## 2. Table de Sélection de Routes

| Critère | Ordre | Explication |
|---------|-------|-------------|
| **Prefix Length** | 1er | Route la plus spécifique gagne |
| **AD (Distance Administrative)** | 2e | Plus basse AD gagne |
| **Métrique** | 3e | Même protocole, plus basse métrique gagne |
| **ECMP** | 4e | Routes identiques → Équilibrage de charge |

## 3. Valeurs Administrative Distance (AD)

| Source de Routage | AD |
|-------------------|-----|
| Directly Connected (Interface) | 0 |
| Static Route | 1 |
| EIGRP | 90 |
| OSPF | 110 |
| RIPv2 | 120 |
| External EIGRP (eBGP) | 170 |
| Unknown/Inaccessible | 255 |

## 4. Métriques par Protocole

### RIPv2
- Nombre de sauts (1-15 max)
- Simple mais limitation de scalabilité

### EIGRP
- **Formule** : $K_1 \times BW + K_2 \times BW / (256 - Load) + K_3 \times Delay$
- Par défaut : K₁=1, K₂=0, K₃=1 → **Metrique = BW + Delay**
- **BW** : Bande passante minimale du chemin
- **Delay** : Somme des délais du chemin

### OSPF
- **Formule** : $Coût = \frac{100,000,000}{Bandwidth_{bps}}$
- Exemple : Interface 1 Gbps = 100,000,000 / 1,000,000,000 = 100
- Plus la bande passante est haute, plus le coût est bas

## 5. Commandes Essentielles - Routage Statique

```bash
# Configuration
ip route <destination> <mask> <next-hop> [AD]
ip route 0.0.0.0 0.0.0.0 203.0.113.1          # Route par défaut
ip route 192.168.2.0 255.255.255.0 192.168.1.1 150  # Avec AD personnalisée

# Vérification
show ip route                     # Affiche la table de routage
show ip route <prefix>            # Affiche les routes vers un réseau
show ip route static              # Affiche seulement les routes statiques
show ip route summary             # Résumé statistique

# Suppression
no ip route 192.168.2.0 255.255.255.0 192.168.1.1
```

## 6. ECMP vs Unequal-Cost Load Balancing

### ECMP (Equal-Cost Multipath)
- **Condition** : Même AD + Même métrique
- **Configuration EIGRP** : `variance 1`
- **Commande** : `maximum-paths <nombre>`
- **Résultat** : Trafic équilibré entre routes identiques

### Unequal-Cost Load Balancing
- **Condition** : Même AD + Métriques différentes
- **Configuration EIGRP** : `variance > 1`
- **Formule acceptation** : $Metrique_{alt} \leq Variance \times Metrique_{best}$
- **Exemple** : variance 2 accepte routes avec métrique jusqu'à 2× la meilleure

```
Router EIGRP Config :
router eigrp 100
 maximum-paths 6        # Jusqu'à 6 chemins
 variance 2             # Accepte chemins avec coût 2× le meilleur
```

## 7. RIB vs FIB

| RIB | FIB |
|-----|-----|
| Contient toutes les routes candidates | Contient seulement le meilleur chemin |
| Mise à jour = protocole + révision | Mise à jour = installation en FIB |
| `show ip route` affiche la RIB | `show ip cef` affiche la FIB |
| Gère convergence et protocoles | Gère la commutation rapide |

## 8. VRF (Virtual Routing and Forwarding) - Structure

```
Routeur Physique
├── VRF customer-a
│   ├── RIB propre
│   ├── FIB propre
│   ├── Routes OSPF (ospf 100)
│   ├── Interface Gi0/1 → 192.168.1.0/24
│   └── Interface Gi0/2 → 192.168.2.0/24
├── VRF customer-b
│   ├── RIB propre
│   ├── FIB propre
│   ├── Routes statiques
│   ├── Interface Gi0/3 → 10.0.0.0/24
│   └── Interface Gi0/4 → 10.0.1.0/24
└── VRF Management (défaut)
    └── Interface Gi0/0
```

## 9. Configuration VRF - Checklist

```bash
# 1. Créer VRF
ip vrf customer-a
 description Client A
 rd 65000:100              # Route Distinguisher

# 2. Assigner Interface
interface Gi0/1
 ip vrf forwarding customer-a
 ip address 192.168.1.1 255.255.255.0

# 3. Configurer Routage
router ospf 100 vrf customer-a
 network 192.168.1.0 0.0.0.255 area 0

# 4. Vérification
show ip vrf
show ip route vrf customer-a
ping vrf customer-a 192.168.1.2
```

## 10. Concepts Clés - Mind Map Texte

```
SÉLECTION DE ROUTE
├── Niveau 1 : Prefix Length
│   └── Plus spécifique gagne toujours
├── Niveau 2 : AD (Distance Administrative)
│   └── Plus basse valeur gagne
├── Niveau 3 : Métrique
│   └── Utilisée si AD est identique
└── Niveau 4 : ECMP/Unequal-Cost
    └── Équilibrage sur routes identiques ou similaires

MÉTRIQUES
├── RIPv2 : Sauts (simple)
├── EIGRP : Composite (BW + Delay)
├── OSPF : Coût inverse bande passante
└── Comparaison : Jamais entre protocoles différents

AD HIÉRARCHIE
├── 0   : Direct (plus fiable)
├── 1   : Statique
├── 90  : EIGRP (dynamique fiable)
├── 110 : OSPF (dynamique)
├── 120 : RIP (moins fiable)
└── 255 : Impossible
```

## 11. Points Clés pour l'Examen

✓ Comprendre pourquoi prefix length prime sur AD  
✓ Mémoriser AD par défaut : 0, 1, 90, 110, 120, 170  
✓ EIGRP métrique = BW + Delay (par défaut)  
✓ OSPF coût = 100M / BW  
✓ ECMP = métriques identiques, Unequal = variance > 1  
✓ VRF = instances de routage isolées  
✓ RIB candidates, FIB commutation  
✓ Route statique peut être backup (AD > protocoles)

## 12. Piégez Courants

❌ Oublier que prefix length prime sur AD  
❌ Confondre métrique EIGRP (composite BW+ Delay)  
❌ AD 1 (statique) < AD 90 (EIGRP) — statique préférée  
❌ Variance 1 = ECMP uniquement, variance 2+ = Unequal  
❌ Oublier que VRF = instances RIB/FIB indépendantes  
❌ Utiliser `ip route` sans VRF dans un contexte VRF

---
**Temps révision** : 30 min | **Niveau** : Basique-Intermédiaire
