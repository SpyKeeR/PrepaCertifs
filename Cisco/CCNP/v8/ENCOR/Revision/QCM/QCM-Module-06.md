# QCM Module 6 : IP Routing Essentials

## Questions

### Question 1
**Enoncé** : Vous avez configuré deux routes vers le réseau 10.0.0.0/8 :
- Route A via EIGRP : AD 90, métrique 2560
- Route B via OSPF : AD 110, métrique 100

Quelle route sera installée dans la RIB ?

A) Route A (métrique inférieure)  
B) Route B (AD plus spécifique)  
C) Route A (AD inférieure)  
D) Les deux routes avec ECMP

**Réponse** : C) Route A (AD inférieure)

**Explication** : La Distance Administrative est le second critère après la longueur du préfixe. Route A avec AD 90 prime sur Route B avec AD 110. La métrique OSPF n'est jamais comparée à la métrique EIGRP. AD détermine la confiance en la source de routage, pas la métrique du chemin.

---

### Question 2
**Enoncé** : Dans une topologie avec plusieurs chemins EIGRP vers 192.168.1.0/24 tous avec AD 90 mais des métriques différentes :
- Chemin 1 : Métrique 2560
- Chemin 2 : Métrique 5120
- Chemin 3 : Métrique 7680

Le routeur est configuré avec `maximum-paths 4` et `variance 1`. Combien de chemins seront utilisés pour l'équilibrage de charge ?

A) 1 chemin  
B) 2 chemins  
C) 3 chemins  
D) 4 chemins

**Réponse** : A) 1 chemin

**Explication** : Avec `variance 1`, seules les routes avec la MÊME métrique que le meilleur chemin (2560) seront acceptées. C'est la définition d'ECMP (Equal-Cost Multipath). Les chemins 2 et 3 sont rejetés. Variance 1 signifie métrique_alternatif ≤ 1 × 2560, donc seulement 2560 = 2560.

---

### Question 3
**Enoncé** : Vous devez créer un route statique backup vers 10.0.0.0/8 qui sera utilisée seulement si la route OSPF devient inaccessible. OSPF a un AD de 110. Quelle valeur AD devez-vous utiliser pour la route statique ?

A) AD 100  
B) AD 109  
C) AD 111  
D) AD 170

**Réponse** : C) AD 111

**Explication** : Pour que la route statique soit backup, elle doit avoir une AD PLUS ÉLEVÉE que OSPF (110). Une valeur comme 111 ou supérieure l'installera seulement quand OSPF devient inaccessible. AD 100 ou 109 remplacerait OSPF. AD 170 est l'AD pour eBGP externe.

---

### Question 4
**Enoncé** : Lors du processus de sélection de route, dans quel ordre les critères sont-ils évalués ?

A) Métrique → AD → Prefix Length  
B) Prefix Length → Métrique → AD  
C) AD → Prefix Length → Métrique  
D) Prefix Length → AD → Métrique

**Réponse** : D) Prefix Length → AD → Métrique

**Explication** : La hiérarchie est systématique :
1. **Prefix Length** : Route la plus spécifique TOUJOURS gagne (ex: /24 vs /16)
2. **AD** : Entre sources de routage différentes (OSPF vs EIGRP)
3. **Métrique** : Seulement si même protocole et AD

---

### Question 5
**Enoncé** : Vous avez un lien FastEthernet (100 Mbps) dans votre topologie OSPF. Quel sera le coût OSPF de cette interface ?

A) 10  
B) 100  
C) 1000  
D) 100000

**Réponse** : C) 1000

**Explication** : Coût OSPF = 100,000,000 / Bande passante (en bps)
= 100,000,000 / 100,000,000 = 1000
FastEthernet = 100 Mbps = 100,000,000 bps

---

### Question 6
**Enoncé** : Quelle est la différence principale entre RIB et FIB ?

A) RIB gère la commutation, FIB la convergence  
B) RIB contient toutes les routes candidates, FIB contient seulement la/les meilleures  
C) RIB utilise CEF, FIB utilise les protocoles de routage  
D) RIB est optimisée hardware, FIB est optimisée software

**Réponse** : B) RIB contient toutes les routes candidates, FIB contient seulement la/les meilleures

**Explication** : La RIB (Routing Information Base) conserve TOUTES les routes apprises. La FIB (Forwarding Information Base) contient copie de la meilleure route (ou routes en cas ECMP) et est optimisée pour les recherches rapides hardware.

---

### Question 7
**Enoncé** : Vous devez séparer les réseaux de gestion et production sur un routeur unique tout en gardant le routeur physique. Quel technologie utilisez-vous ?

A) VLAN  
B) Subinterface  
C) VRF (Virtual Routing and Forwarding)  
D) Policy-based routing

**Réponse** : C) VRF (Virtual Routing and Forwarding)

**Explication** : VRF crée plusieurs instances de routage logiques (RIB/FIB séparées) sur un routeur physique unique. C'est la solution pour multi-tenancy, isolation réseau et gestion sécurisée. VLAN sépare les données layer 2, VRF sépare le routage layer 3.

---

### Question 8
**Enoncé** : Configuré dans EIGRP : `maximum-paths 6` et `variance 2`. Un meilleur chemin a une métrique de 1000. Quel chemin alternatif avec métrique 1800 sera accepté ?

A) Non, car 1800 > 2000  
B) Oui, car 1800 ≤ 2000  
C) Non, car variance 2 signifie exactement 2000  
D) Oui, car maximum-paths 6 le permet

**Réponse** : B) Oui, car 1800 ≤ 2000

**Explication** : Avec variance 2 et métrique meilleure = 1000, la limite acceptée est 1000 × 2 = 2000. 
Formule : Métrique_alternatif ≤ Variance × Métrique_meilleure
1800 ≤ 2 × 1000 = 1800 ≤ 2000 ✓

---

### Question 9
**Enoncé** : Comment afficher toutes les routes statiques actuelles sur un routeur ?

A) `show ip static`  
B) `show ip route static`  
C) `show static routes`  
D) `show ip route configured`

**Réponse** : B) `show ip route static`

**Explication** : La commande `show ip route static` filtre et affiche seulement les routes statiques dans la table de routage. `show ip route` affiche toutes les routes (connectées, statiques, dynamiques).

---

### Question 10
**Enoncé** : Quel protocole de routage utilise l'algorithme DUAL (Diffusing Update Algorithm) ?

A) RIPv2  
B) OSPF  
C) EIGRP  
D) BGP

**Réponse** : C) EIGRP

**Explication** : DUAL est l'algorithme propriétaire Cisco utilisé par EIGRP pour garantir une convergence rapide sans boucles. DUAL utilise les concepts de Successor (meilleure route) et Feasible Successor (route backup valide).

---

### Question 11
**Enoncé** : Vous configurez une route statique vers 172.16.0.0/12 via l'interface Serial 0/0. Quel type de route statique est ceci ?

A) Recursive static route  
B) Directly connected static route  
C) Floating static route  
D) Static route with outgoing interface

**Réponse** : D) Static route with outgoing interface

**Explication** : Cette route statique spécifie directement l'interface de sortie (Serial 0/0) plutôt qu'un next-hop IP. Types de routes statiques :
- **Recursive** : next-hop IP, résolu via autre route
- **Directly connected** : via interface
- **Floating** : avec AD > 1 pour backup

---

### Question 12
**Enoncé** : Quel est l'AD (Administrative Distance) d'une interface directement connectedue ?

A) 0  
B) 1  
C) 90  
D) 255

**Réponse** : A) 0

**Explication** : L'AD 0 est la plus haute confiance, accordée aux interfaces directement connectées. C'est la route la plus fiable car c'est la machine elle-même qui est attachée au réseau.
| Source | AD |
|-|-|
| Direct | 0 |
| Static | 1 |
| EIGRP | 90 |
| OSPF | 110 |
| RIP | 120 |

---

### Question 13
**Enoncé** : Quel est le nombre MAXIMUM de sauts pour un réseau routé par RIPv2 ?

A) 15  
B) 16  
C) 30  
D) 255

**Réponse** : A) 15

**Explication** : RIPv2 a une limite de 15 sauts. Une destination à 16 sauts ou plus est considérée comme inaccessible. C'est une limitation majeure de RIPv2 qui le rend impropre aux grands réseaux.

---

### Question 14
**Enoncé** : Dans EIGRP, la métrique composite utilise par défaut :

A) Bandwidth seulement  
B) Bandwidth et Delay  
C) Bandwidth, Delay et Reliability  
D) Tous les K values (K1-K5)

**Réponse** : B) Bandwidth et Delay

**Explication** : Par défaut, les K values EIGRP sont :
- K1 = 1 (Bandwidth activé)
- K2 = 0 (Load inactivé)
- K3 = 1 (Delay activé)
- K4 = 0 (Reliability inactivé)
- K5 = 0 (MTU inactivé)

Métrique = K1×BW + K3×Delay = BW + Delay

---

### Question 15
**Enoncé** : Vous ajoutez une interface à un VRF existant qui avait déjà une configuration IP. Que se passe-t-il ?

A) L'adresse IP est conservée  
B) L'adresse IP est supprimée lors de l'association VRF  
C) Une adresse IPv6 est attribuée automatiquement  
D) La configuration reste mais change de VRF

**Réponse** : B) L'adresse IP est supprimée lors de l'association VRF

**Explication** : Quand vous associez une interface existante à un VRF avec `ip vrf forwarding`, sa configuration IP précédente est supprimée. Vous devez reconfigurer l'adresse IP APRÈS l'association au VRF.

```bash
interface Gi0/1
 ip address 192.168.1.1 255.255.255.0
 # Puis :
 ip vrf forwarding customer-a
 # Puis reconfigurer :
 ip address 192.168.1.1 255.255.255.0
```

---

### Question 16
**Enoncé** : Quel critère determiniera le choix entre ces deux routes ?
- Route 1 : 192.168.1.0/25 via OSPF (AD 110)
- Route 2 : 192.168.1.0/24 via RIP (AD 120)
Destination : 192.168.1.100

A) AD (OSPF gagne)  
B) Métrique (moins de sauts)  
C) Prefix Length (Route 1 gagne /25)  
D) Protocole (OSPF est plus fiable)

**Réponse** : C) Prefix Length (Route 1 gagne /25)

**Explication** : **Prefix Length prime TOUJOURS sur tous autres critères**. Route 1 avec /25 est plus spécifique que Route 2 avec /24, donc Route 1 est sélectionnée même si OSPF a une AD moins fiable que RIP. Une route /25 est plus spécifique.

---

### Question 17
**Enoncé** : Quel commande active CEF globalement et valide sa FIB sur une interface Gigabit ?

A) `enable cef` / `ip cef`  
B) `ip cef` globalement  
C) `ip cef load-sharing` sur l'interface  
D) CEF est activé par défaut sur tous les routeurs modernes

**Réponse** : B) `ip cef` globalement

**Explication** : CEF (Cisco Express Forwarding) est activé avec `ip cef` en mode global configuration. CEF crée et maintient la FIB pour des recherches de routage ultra-rapides. Sur les routeurs modernes, CEF est souvent activé par défaut.

---

### Question 18
**Enoncé** : Vous devez vérifier quelles routes sont actuellement dans la FIB (pas RIB). Quel commande utilisez-vous ?

A) `show ip route`  
B) `show ip fib`  
C) `show ip cef`  
D) `show forwarding table`

**Réponse** : C) `show ip cef`

**Explication** : `show ip cef` affiche le contenu de la FIB (préfixes et que next-hops). 
- `show ip route` = RIB (toutes les routes)
- `show ip cef` = FIB (routes actives/commutation)
- `show ip cef detail` = FIB avec détails d'adjacences

---

### Question 19
**Enoncé** : Quel est le préfixe maximal pour une route spécifique possible ?

A) /24  
B) /30  
C) /32  
D) /128

**Réponse** : C) /32

**Explication** : Pour IPv4, le préfixe maximal est /32 (un seul hôte - une route hôte). Pour IPv6, c'est /128. Plus le préfixe est long, plus la route est spécifique.

---

### Question 20
**Enoncé** : Quel commande affiche l'AD assignee à une route statique configurée pour un VRF ?

A) `show ip vrf customer-a static`  
B) `show ip route vrf customer-a`  
C) `show ip static vrf customer-a`  
D) `show running-config interface`

**Réponse** : B) `show ip route vrf customer-a`

**Explication** : `show ip route vrf [VRF-name]` affiche la table de routage pour ce VRF spécifique, incluant l'AD entre parenthèses. Format : `[AD/métrique]`.

---

### Question 21
**Enoncé** : Vous avez configuré ces deux routes statiques :
```
ip route 192.168.1.0 255.255.255.0 192.168.1.1 100
ip route 192.168.1.0 255.255.255.0 192.168.1.2 50
```

Laquelle sera utilisée pour l'équilibrage de charge ?

A) First route only (192.168.1.1)  
B) Second route only (192.168.1.2)  
C) Both routes with ECMP  
D) Aucuno, car AD différentes

**Réponse** : B) Second route only (192.168.1.2)

**Explication** : Même si les ADs sont différentes, le routeur sélectionnera seulement la route avec la plus basse AD (50). L'autre route (AD 100) est ignorée. C'est l'inverse d'ECMP — il n'y a pas d'équilibrage.

---

### Question 22 (Avancée)
**Enoncé** : Dans une configuration EIGRP multi-site avec `variance 3` et `maximum-paths 8`, le meilleur chemin (successor) a une métrique de 2048. Combien de chemins alternatifs avec métrique 4096 seront ajoutés à l'équilibrage ?

A) 0  
B) 1  
C) Limité par maximum-paths  
D) Tous jusqu'à 8 total

**Réponse** : D) Tous jusqu'à 8 total

**Explication** : Variance 3 accepte métriques ≤ 3 × 2048 = 6144.
4096 ≤ 6144 ✓ Tous les chemins 4096 seront acceptés (jusqu'à maximum-paths 8 total).

---

### Question 23 (Avancée)
**Enoncé** : Quel est l'objectif principal du Route Distinguisher (RD) dans une VRF ?

A) Isoler les interfaces physiques  
B) Rendre les routes VRF uniques globalement (en MPLS VPN)  
C) Augmenter la sécurité du VRF  
D) Limiter le nombre de routes par VRF

**Réponse** : B) Rendre les routes VRF uniques globalement (en MPLS VPN)

**Explication** : Route Distinguisher est un identifiant ADD à chaque route VRF pour la rendre globalement unique en environnement MPLS VPN. Format : AS:value ou IP:value (ex: 65000:100).

---

### Question 24 (Avancée)
**Enoncé** : Vous tentez de configurer un protocole OSPF séparé pour deux VRFs sur le même routeur :
```
router ospf 100 vrf customer-a
 network 192.168.1.0 0.0.0.255 area 0

router ospf 101 vrf customer-b
 network 10.0.0.0 0.0.0.255 area 0
```

Pourquoi cette configuration dans ce module est-elle valide ?

A) Chaque VRF a sa propre instance OSPF indépendante  
B) Les Process IDs doivent être identiques  
C) Impossible car OSPF par VRF nécessite des Process IDs différents  
D) Les networks doivent être les mêmes dans tous les VRFs

**Réponse** : A) Chaque VRF a sa propre instance OSPF indépendante

**Explication** : VRF supporte les protocoles de routage indépendants. Process ID 100 (VRF customer-a) et Process ID 101 (VRF customer-b) fonctionnent indépendamment avec leurs propres domaines OSPF, adjacencies et bases de données.

---

### Question 25 (Avancée)
**Enoncé** : Quelle est la relation entre la longueur du préfixe et l'AD en sélection de route ?

A) Ils ont la même importance  
B) AD prime sur prefix length  
C) Prefix length prime sur AD, sans exception  
D) Aucun, ils fonctionnent en parallèle

**Réponse** : C) Prefix length prime sur AD, sans exception

**Explication** : **Règle d'or du routage IP** : La longueur du préfixe est TOUJOURS le critère primaire de sélection, même avant AD. Une route /25 sera sélectionnée sur une route /24 peu importe les ADs, même si l'AD /24 vient d'OSPF et l'AD /25 vient de RIP (AD 120 vs 110).

---

## Résumé des Réponses

| Q | Réponse | Q | Réponse |
|---|---------|---|---------|
| 1 | C | 13 | A |
| 2 | A | 14 | B |
| 3 | C | 15 | B |
| 4 | D | 16 | C |
| 5 | C | 17 | B |
| 6 | B | 18 | C |
| 7 | C | 19 | C |
| 8 | B | 20 | B |
| 9 | B | 21 | B |
| 10 | C | 22 | D |
| 11 | D | 23 | B |
| 12 | A | 24 | A |

---
**Durée estimée** : 45-60 minutes  
**Difficulté** : Basique (Q1-12), Intermédiaire (Q13-20), Avancée (Q21-25)
