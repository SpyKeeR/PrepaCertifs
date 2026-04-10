# QCM Module 7 : EIGRP

## Questions

### Question 1
**Enoncé** : Deux routeurs EIGRP avec les configurations suivantes :
- Routeur A : K values 1, 0, 1, 0, 0
- Routeur B : K values 1, 1, 1, 0, 0

Que se passe-t-il ?

A) Les routeurs deviennent voisins actifs  
B) Les routeurs ne deviennent pas adjacents (neighbours détectés mais inactifs)  
C) Seul le routage statique fonctionne  
D) Une erreur de configuration est générée

**Réponse** : B) Les routeurs ne deviennent pas adjacents (neighbours détectés mais inactifs)

**Explication** : Les K values (K1-K5) DOIVENT être identiques. Si divergents, les routeurs se détectent (Hello reçu) mais ne deviennent pas ADJACENTS. Ils restent en état down/passive. Ceci est une safeguard DUAL pour éviter les incohérences de métrique.

---

### Question 2
**Enoncé** : Quel est le délai de détection de voisin EIGRP typique sur une interface FastEthernet ?

A) 5 secondes  
B) 15 secondes  
C) 60 secondes  
D) 180 secondes

**Réponse** : B) 15 secondes

**Explication** : Hold time par défaut = 3 × Hello interval. Sur FastEthernet, Hello = 5 sec, donc Hold = 15 sec. Si aucun Hello reçu après 15 secondes, le routeur déclare le voisin inaccessible.

---

### Question 3
**Enoncé** : Deux voisins EIGRP ont des Hello intervals différents : Routeur A = 5 sec, Routeur B = 10 sec. Quel sera le résultat ?

A) Hold time divergent ; la adjacency failera après 3× l'interval plus court  
B) Hold time sera 15 sec (A) et 30 sec (B) ; adjacency stable  
C) EIGRP auto-synchronisera les Hello  
D) Erreur de configuration, adjacency refusée

**Réponse** : B) Hold time sera 15 sec (A) et 30 sec (B) ; adjacency stable

**Explication** : Chaque routeur maintient un hold time INDÉPENDANT basé sur son propre hello interval (3× his interval). Hold time n'a PAS à être identique. Les timers EIGRP peuvent diverger sans problème.

---

### Question 4
**Enoncé** : Quelle est la métrique composante BW pour une interface Serial 64k ?

A) 64,000  
B) 156,250  
C) 1,000,000  
D) 100,000,000

**Réponse** : B) 156,250

**Explication** : Formule EIGRP BW = 10^7 / Bande passante (en kbps)
= 10,000,000 / 64 = 156,250

---

### Question 5
**Enoncé** : Dans EIGRP, la métrique par défaut utilise quels K values ?

A) K1=1, K2=0, K3=1, K4=0, K5=0  
B) K1=1, K2=1, K3=1, K4=1, K5=1  
C) K1=0, K2=0, K3=0, K4=0, K5=0  
D) K1=2, K2=0, K3=3, K4=0, K5=0

**Réponse** : A) K1=1, K2=0, K3=1, K4=0, K5=0

**Explication** : Les K values par défaut activent BW (K1) et Delay (K3), désactivent Load (K2), Reliability (K4), et MTU (K5). Métrique = BW + Delay.

---

### Question 6
**Enoncé** : Quel est l'algorithme utilisé par EIGRP pour sélectionner les routes et éviter les boucles ?

A) SPF (Shortest Path First)  
B) DUAL (Diffusing Update Algorithm)  
C) Dijkstra  
D) Bellman-Ford

**Réponse** : B) DUAL (Diffusing Update Algorithm)

**Explication** : DUAL est l'algorithme breveté Cisco qui garantit :
- Sélection rapide de successor et feasible successor
- Prévention des boucles (test Feasible Successor)
- Convergence sans boucles transitoires

---

### Question 7
**Enoncé** : Quelle est la condition pour qu'une route soit un Feasible Successor ?

A) Métrique identique au Successor  
B) Advertised Distance (AD) du voisin < Feasible Distance (FD) actuelle  
C) Métrique du voisin < métrique Du successor  
D) La route doit avoir un meilleur AD

**Réponse** : B) Advertised Distance (AD) du voisin < Feasible Distance (FD) actuelle

**Explication** : Le test Feasible Successor est : $AD_{voisin} < FD_{actuel}$

Ceci garantit que le chemin alternatif ne boucle pas (loop-free guarantee).

---

### Question 8
**Enoncé** : Un routeur EIGRP détecte que son Successor vers une destination ne répond plus ET qu'il n'a pas de Feasible Successor. Que se passe-t-il ?

A) Route est supprimée immédiatement  
B) Une nouvelle route est cherchée via DUAL ACTIVE (QUERY/REPLY)  
C) Un failover statique est utilisé  
D) La topologie attend 3 minutes avant réaction

**Réponse** : B) Une nouvelle route est cherchée via DUAL ACTIVE (QUERY/REPLY)

**Explication** : DUAL entre en état ACTIVE :
1. Routeur envoie QUERY à tous voisins
2. Voisins répondent avec REPLY
3. Nouvelle meilleure route sélectionnée
4. Route revient à PASSIVE

Ceci peut prendre quelques secondes (pire cas 3 min timeout).

---

### Question 9
**Enoncé** : Quelle commande configure l'intervalle Hello à 10 secondes sur une interface Gigabit spécifique ?

A) `router eigrp 100` → `hello-interval 10`  
B) `interface Gi0/0` → `ip hello-interval eigrp 100 10`  
C) `interface Gi0/0` → `eigrp hello-interval 10`  
D) `router eigrp 100` → `interface timers hello 10`

**Réponse** : B) `interface Gi0/0` → `ip hello-interval eigrp 100 10`

**Explication** : Les timers EIGRP se configurent PER INTERFACE, pas globalement. Format : `ip hello-interval eigrp [AS] [seconds]`

---

### Question 10
**Enoncé** : Dans une topologie avec variance 2 et maximum-paths 4, le Successor a FD=1000. Quelle sera la limite acceptée pour un chemin alternatif ?

A) Métrique ≤ 1000  
B) Métrique ≤ 1500  
C) Métrique ≤ 2000  
D) Métrique ≤ 4000

**Réponse** : C) Métrique ≤ 2000

**Explication** : Formule unequal-cost : $Metrique_{alt} \leq Variance \times FD_{successor}$
= 2 × 1000 = 2000

Maximum-paths limite NOMBRE de chemins (4 ici), variance limite RATIO des métriques.

---

### Question 11
**Enoncé** : Pourquoi la commande `show ip eigrp topology` est importante pour diagnostiquer EIGRP ?

A) Elle affiche les voisins actifs seulement  
B) Elle montre la topology table brute avec successors et feasible successors  
C) Elle affiche l'utilisation de bande passante en temps réel  
D) Elle liste toutes les routes en état ACTIVE

**Réponse** : B) Elle montre la topology table brute avec successors et feasible successors

**Explication** : `show ip eigrp topology` est la vue de la Topology Table EIGRP. Elle montre :
- FD (Feasible Distance)
- AD (Advertised Distance) de chaque voisin
- État Successor/FS
- Routes en ACTIVE (si applicable)

---

### Question 12
**Enoncé** : Comment configurer une résumé de route EIGRP sur l'interface Gi0/1 pour agrégé 192.168.0.0/16 suite à 192.168.1.0/24 et 192.168.2.0/24 ?

A) `router eigrp 100` → `aggregate-route 192.168.0.0 255.255.0.0`  
B) `interface Gi0/1` → `ip summary-address eigrp 100 192.168.0.0 255.255.0.0`  
C) `interface Gi0/1` → `route-map aggregate 1`  
D) `router eigrp 100` → `summary-interface Gi0/1 192.168.0.0 255.255.0.0`

**Réponse** : B) `interface Gi0/1` → `ip summary-address eigrp 100 192.168.0.0 255.255.0.0`

**Explication** : Résumé EIGRP manuel se configure PER INTERFACE. Format : `ip summary-address eigrp [AS] [network] [mask]`

---

### Question 13
**Enoncé** : Quelle est la différence fondamentale entre ECMP (variance 1) et Unequal-Cost Load Balancing (variance >1) ?

A) ECMP utilise plusieurs chemins, UC LB n'en utilise qu'un  
B) ECMP est pour routes identiques, UC LB pour routes de coûts différents mais acceptables  
C) UC LB a meilleure performance que ECMP  
D) ECMP nécessite maximum-paths, UC LB non

**Réponse** : B) ECMP est pour routes identiques, UC LB pour routes de coûts différents mais acceptables

**Explication** :
- **ECMP** (variance=1) : Métrique_alt = FD (identiques)
- **Unequal-Cost** (variance>1) : FD < Métrique_alt ≤ Variance × FD (différents)

---

### Question 14
**Enoncé** : Deux interfaces EIGRP : Serial 0/0 avec délai 20,000 µsec et Ethernet avec délai 10 µsec. Quel est le composant Delay dans la métrique EIGRP ?

A) 20,010  
B) 2,001  
C) 2,000  
D) 20,000

**Réponse** : B) 2,001

**Explication** : Delay composant = (Somme délais) / 10
= (20,000 + 10) / 10 = 20,010 / 10 = 2,001

---

### Question 15
**Enoncé** : Quel commande EIGRP permet visualiser routes actuellement en état ACTIVE (c.-à-d. cherchant nouvelle route) ?

A) `show ip route active`  
B) `show ip eigrp topology active`  
C) `show ip eigrp active routes`  
D) `debug eigrp active-state`

**Réponse** : B) `show ip eigrp topology active`

**Explication** : `show ip eigrp topology active` liste toutes les routes EIGRP actuellement en état ACTIVE (recherche QUERY/REPLY en cours). État ACTIVE est rare en réseau stable.

---

### Question 16
**Enoncé** : Pourquoi est-il recommandé d'utiliser `no auto-summary` en configuration EIGRP moderne ?

A) Auto-summary augmente la scalabilité  
B) Auto-summary peut causer problèmes de routage discontigus et routes en null  
C) Auto-summary est requis pour ECMP  
D) Auto-summary réduit utilisation de bande passante

**Réponse** : B) Auto-summary peut causer problèmes de routage discontigus et routes en null

**Explication** : `auto-summary` résume routes aux limites de classe (ex: 192.168.0.0/16). Ceci peut créer :
- Routes null vers des réseaux discontigus
- Problèmes de routage imprévisibles
- Comportements asymétriques

Recommendation : `no auto-summary` (défaut sur IOS plus récent)

---

### Question 17 (Avancée)
**Enoncé** : EIGRP avec variance 3, FD=100. Quelle métrique de chemin alternatif sera REFUSÉE pour l'équilibrage ?

A) 150  
B) 250  
C) 300  
D) 350

**Réponse** : D) 350

**Explication** : Limite acceptée = Variance × FD = 3 × 100 = 300
- 150 ✓ accepté (150 ≤ 300)
- 250 ✓ accepté (250 ≤ 300)
- 300 ✓ accepté (300 ≤ 300)
- 350 ✗ refusé (350 > 300)

---

### Question 18 (Avancée)
**Enoncé** : Configuration EIGRP : métrique K1=2, K2=0, K3=2. Quel sera l'impact sur la sélection de route ?

A) La métrique sera 2× plus lourde que défaut  
B) Seul BW sera utilisé pour sélection  
C) Delay sera doublé dans le calcul  
D) Les voisins ne pourront pas former d'adjacence

**Réponse** : D) Les voisins ne pourront pas former d'adjacence

**Explication** : K values non-standard empêchent ADJACENCE EIGRP. Tous les voisins doivent avoir les MÊMES K values. Configuration K1=2, K3=2 divergerait des défaults, provoquant rejection de voisinage.

---

### Question 19 (Avancée)
**Enoncé** : Quel est l'avantage principal d'avoir un Feasible Successor en EIGRP ?

A) Réduction de la bande passante  
B) Convergence instantanée (~100ms) sans QUERY/REPLY  
C) Augmentation de la métrique de sécurité  
D) Supprime la nécessité d'ACL

**Réponse** : B) Convergence instantanée (~100ms) sans QUERY/REPLY

**Explication** : Feasible Successor est une route PRÉ-VALIDÉE sans boucles. Si le Successor défaille, le FS peut être utilisé IMMÉDIATEMENT sans recherche DUAL active. Ceci offre :
- Sub-100ms failover
- Pas de QUERY/REPLY delay
- Haute disponibilité

---

### Question 20
**Enoncé** : Configuré : `router eigrp 100` + `network 192.168.1.0` + `distance 130`. Quel est l'AD des routes EIGRP apprises ?

A) 90 (AD EIGRP standard)  
B) 100 (numéro AS)  
C) 130 (distance customisée)  
D) 110 (AD OSPF par comparaison)

**Réponse** : C) 130 (distance customisée)

**Explication** : Commande `distance [AD] [source]` override l'AD EIGRP. Si configurée globalement, elle s'applique à toutes les routes EIGRP apprise. AD devient 130 au lieu du défaut 90.

---

### Question 21 (Avancée)
**Enoncé** : Topology table EIGRP montre:
```
P 10.0.0.0/24, 1 successors, FD is 2560
  via 10.1.1.1 (2560/2560), Gi0/1
  via 10.1.1.2 (3072/2048), Gi0/2
```

Est-ce que 10.1.1.2 est un Feasible Successor ?

A) Non, car FD (2560) < AD (2048)  
B) Oui, car AD (2048) < FD (2560)  
C) Non, car métrique (3072) > FD (2560)  
D) Oui, car le routeur est voisin

**Réponse** : B) Oui, car AD (2048) < FD (2560)

**Explication** : Test FS : AD_voisin < FD_actuel
2048 < 2560 ✓ → C'est un Feasible Successor valide

Cet FS peut être utilisé immédiatement si Successor 10.1.1.1 défaille (failover instant).

---

### Question 22 (Avancée)
**Enoncé** : Quel est l'ordre de priorité pour la convergence EIGRP ?

A) FS instantané → DUAL ACTIVE search  
B) DUAL ACTIVE search → FS instantane  
C) Numéro AS → K values → FS  
D) Métrique → AD → Prefix Length

**Réponse** : A) FS instantané → DUAL ACTIVE search

**Explication** : Si Successor défaille :
1. Si Feasible Successor existe → Installation immédiate (~<100ms)
2. Si pas FS → DUAL ACTIVE query/reply (quelques sec, max 3 min)

Feasible Successor offre le failover le plus rapide.

---

### Question 23 (Avancée)
**Enoncé** : Comment EIGRP diffère de RIPv2 concernant la convergence lors d'une panne ?

A) EIGRP envoie mises à jour complètes périodiquement  
B) EIGRP ne converge jamais sans recalcul SPF  
C) EIGRP converge sans boucles transitoires grâce à DUAL  
D) RIPv2 converge plus vite grâce au recharts périodiquement

**Réponse** : C) EIGRP converge sans boucles transitoires grâce à DUAL

**Explication** : DUAL garantit des routes loop-free même pendant la transition. RIPv2 peut créer des boucles transitoires (counting to infinity). EIGRP via FS ou recherche DUAL active prévient ceci.

---

### Question 24 (Avancée)
**Enoncé** : EIGRP route Discontiguous Summarization : comment configurer ?

A) `no auto-summary` + résumé manuel par interface  
B) `auto-summary` + RIP redistribution  
C) `summary-network-statement` globalement  
D) Impossible avec EIGRP discontigu

**Réponse** : A) `no auto-summary` + résumé manuel par interface

**Explication** : Pour réseaux discontigus avec résumé :
1. Désactiver `auto-summary` (creates null routes)
2. Configurer `ip summary-address eigrp [AS] [network] [mask]` manuellement
3. Chaque interface résume ses routes spécifiquement

---

### Question 25 (Avancée)
**Enoncé** : Quel commande révisle si les K values sont les mêmes entre voisins EIGRP (avant formation adjacency) ?

A) `show ip eigrp neighbors`  
B) `show ip eigrp topology`  
C) `show ip protocols`  
D) Impossible à vérifier (protocole décide)

**Réponse** : C) `show ip protocols`

**Explication** : `show ip protocols` affiche les K values actuellement utilisés sur ce routeur. Combinez avec le voisin configuré pour vérifier correspondance. Divergence K values empêche adjacency (état down/passive).

---

## Résumé des Réponses

| Q | Rép | Q | Rép |
|---|-----|---|-----|
| 1 | B | 13 | B |
| 2 | B | 14 | B |
| 3 | B | 15 | B |
| 4 | B | 16 | B |
| 5 | A | 17 | D |
| 6 | B | 18 | D |
| 7 | B | 19 | B |
| 8 | B | 20 | C |
| 9 | B | 21 | B |
| 10 | C | 22 | A |
| 11 | B | 23 | C |
| 12 | B | 24 | A |

---
**Durée estimée** : 60-75 minutes  
**Difficulté** : Basique (Q1-9), Intermédiaire (Q10-17), Avancée (Q18-25)
