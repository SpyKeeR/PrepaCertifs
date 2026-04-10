# QCM Module 9 : Advanced OSPF

## Questions

### Question 1
**Enoncé** : Quelle est la principale différence entre une Stub Area et une Totally Stubby Area ?

A) Stub accepte Type 4, Totally Stubby rejette Type 4  
B) Stub rejette Type 5, Totally Stubby rejette Type 3  
C) Stub accepte Type 3, Totally Stubby rejette Type 3  
D) Totalement Stubby n'existe pas (concept Cisco spécifique)

**Réponse** : C) Stub accepte Type 3, Totally Stubby rejette Type 3

**Explication** :
- **Stub** : Rejette Type 4,5 (routes externes) mais accepte Type 3 (inter-area)
- **Totally Stubby** : Rejette Type 3,4,5 (seulement intra-area + défaut)
Totally Stubby = configuration `area X stub no-summary` sur ABR Cisco.

---

### Question 2
**Enoncé** : Configuré Stub Area sans `default-cost`. Quel coût est utilisé pour la route par défaut 0.0.0.0/0 ?

A) 1  
B) 10  
C) 100  
D) Pas de défaut (erreur)

**Réponse** : A) 1

**Explication** : Sans configuration `default-cost`, OSPF défaut = coût **1** pour la route par défaut générée vers Stub Area. Ce valeur est généralement trop bas (utilisé tout comme direct). Recommandation : configurer `area X default-cost 10` ou plus.

---

### Question 3
**Enoncé** : Quel type LSA est rejeté par une Stub Area mais accepté par une NSSA ?

A) Type 3 (Network Summary)  
B) Type 4 (ASBR Summary)  
C) Type 5 (AS External)  
D) Type 7 (NSSA External)

**Réponse** : D) Type 7 (NSSA External)

**Explication** : NSSA est une "Stub Area améliorée qui accepte Type 7". Les Type 7 LSAs représentent routes externes locales (ASBR dans NSSA). Stub rejette Type 5, NSSA transforme Type 7 → Type 5 via ABR.

---

### Question 4
**Enoncé** : Quelle est la configuration pour résumer 4 subnets /24 (192.168.0-3.0/24) en une seule route inter-area via ABR ?

A) `router ospf 100` → `summary-address 192.168.0.0 255.255.252.0`  
B) `router ospf 100` → `area 10 range 192.168.0.0 255.255.252.0`  
C) `interface Gi0/0` → `ip ospf area range 192.168.0.0 255.255.252.0`  
D) `ip ospf-process 100` → `summarize 192.168.0.0 255.255.252.0`

**Réponse** : B) `router ospf 100` → `area 10 range 192.168.0.0 255.255.252.0`

**Explication** : ABR utilise `area X range` pour **résumer routes intra-area**. Summary-address est pour **ASBR résumer routes redistribut**.

---

### Question 5
**Enoncé** : Type 5 LSA (AS External) est utilisé pour quel type de routes ?

A) Routes intra-area  
B) Routes inter-area (résumées)  
C) Routes externes redistribuées  
D) Routes point-to-point

**Réponse** : C) Routes externes redistribuées

**Explication** : Type 5 LSA représente routes **redistribuées vers OSPF** depuis un protocole externe (BGP, EIGRP, connectées, etc.). Générée par ASBR, flooded AS-wide (sauf NSSA).

---

### Question 6
**Enoncé** : OSPF externe route choix : E1 [110/25] vs E2 [110/20]. Laquelle est installée dans RIB ?

A) E1 (type premier)  
B) E2 (coût plus bas)  
C) Les deux ECMP  
D) E1 après 10 sec

**Réponse** : B) E2 (coût plus bas)

**Explication** : Même Type externe (soit E1 soit E2), OSPF sélectionne basé sur **coût plus bas**. E2 20 < E1 25, donc E2 gagne. E1 vs E2 : E1 toujours préféré si disponible (avant E2), mais ici même Type.

---

### Question 7
**Enoncé** : Type 1 (E1) signifie quelle propriété pour la métrique externe ?

A) Métrique fixe au ASBR  
B) Métrique cumulative (ASBR+ABR)  
C) Métrique interne area  
D) Métrique redistribution

**Réponse** : B) Métrique cumulative (ASBR+ABR)

**Explication** : 
- **E1 (Type 1)** : "$Métrique = ASBR\_metric + ABR\_to\_dest\_metric$" (accumule)
- **E2 (Type 2)** : "$Métrique = ASBR\_metric\_only$" (fixe)

E1 préféré si distance ASBR importante, E2 pour simplicité.

---

### Question 8
**Enoncé** : Comment forcer une route externe à être Type 1 (E1) au lieu de Type 2 (E2) par défaut ?

A) `redistribute bgp 65000 metric-type 1 subnets`  
B) `area 0` → `external-type 1`  
C) `interface Gi0/0` → `ip ospf external-type 1`  
D) `redistribute bgp 65000 type 1 subnets`

**Réponse** : A) `redistribute bgp 65000 metric-type 1 subnets`

**Explication** : Paramètre `metric-type 1` sur commande redistribute force **Type 1 (E1) LSAs**. Sans `metric-type 1`, défaut = Type 2 (E2).

---

### Question 9
**Enoncé** : Quel est le préfixe liste utilisé avec `distribute-list` pour filtrer routes OSPF dans RIB ?

A) ACL standard  
B) Prefix-list avec `ip prefix-list`  
C) Route-map  
D) Policy-map

**Réponse** : B) Prefix-list avec `ip prefix-list`

**Explication** : `distribute-list prefix [name] in/out` utilise **prefix-lists** (pas ACL). Format :
```
ip prefix-list FILTER seq 10 deny 172.16.0.0/16
ip prefix-list FILTER seq 20 permit 0.0.0.0/0 le 32
```

---

### Question 10
**Enoncé** : Commande `area 20 filter-list prefix OUT-LIST out` sur ABR. Qu'est-ce qui est filtré ?

A) Routes entrantes dans Area 20  
B) LSA Type 1 quittant Area 20  
C) LSA Type 3 quittant Area 20  
D) Voisins Area 20

**Réponse** : C) LSA Type 3 quittant Area 20

**Explication** : `area X filter-list` filtre **Type 3 LSAs** (Network Summary) entre areas. Direction `out` = LSA 3 quittant cette area vers autre areas.

---

### Question 11
**Enoncé** : Une NSSA avec ASBR local génère Type 7 LSA. Qu'advient-il quand cette LSA traverse l'ABR vers Area 0 ?

A) Type 7 reste Type 7  
B) Type 7 est traduit en Type 5  
C) Type 7 est annulée (rejetée)  
D) Type 7 devient Type 3

**Réponse** : B) Type 7 est traduit en Type 5

**Explication** : **ABR Translation** : Type 7 LSAs générées dans NSSA sont converties en **Type 5** quand quittent vers autres areas. Ceci permet routes NSSA-local redistribuées d'être connues AS-wide.

---

### Question 12
**Enoncé** : Comment configurer `summary-address` sur ASBR pour résumer 4 subnets /24 ?

A) `router ospf 100` → `summary-address 192.168.0.0 255.255.252.0`  
B) `area 10` → `summary 192.168.0.0 255.255.252.0`  
C) Comme `area range` sur ABR  
D) Impossible (OSPF n'a pas summary-address)

**Réponse** : A) `router ospf 100` → `summary-address 192.168.0.0 255.255.252.0`

**Explication** : **ASBR summary-address résume routes**  (redistrib) en **Type 5 LSAs**. Différent de `area range` (ABR résume Type 3). Format identique (réseau + wildcard mask).

---

### Question 13
**Enoncé** : Quel impact conforme Option `area X range not-advertise` ?

A) Supprime la route du résumé (null route)  
B) Marque route comme standby  
C) Empêche ABR de flooder  
D) Inverse direction du résumé

**Réponse** : A) Supprime la route du résumé (null route)

**Explication** : `not-advertise` génère une route **black hole** (null 0) pour cette route. Utile pour éviter boucles si cette subnet est discontigué ailleurs.

---

### Question 14
**Enoncé** : Timers throttle SPF : `timers throttle spf 200 1000 5000`. Qu'est-ce que signifie le second paramètre (1000) ?

A) Délai avant premier SPF (200 ms plus pertinent)  
B) Délai minimum entre SPF recalculs successive  
C) Delai maximum global  
D) Hold time de lien

**Réponse** : B) Délai minimum entre SPF recalculs successive

**Explication** : SPF timers
- **200 ms** : Initial delay avant premier SPF
- **1000 ms** : Min hold (augmente si changements rapides)
- **5000 ms** : Max hold (cap maximal)

Algorithme backoff : augmente délai si changements continues.

---

### Question 15
**Enoncé** : Une route Intra-area (O) et une Inter-area (O IA) existent pour même destination. OSPF préfère laquelle ?

A) O IA (plus stable)  
B) O (Intra-area gagne toujours)  
C) Les deux ECMP  
D) Basé sur coût

**Réponse** : B) O (Intra-area gagne toujours)

**Explication** : **Path Preference Hierarchy** : Intra-area **prime toujours** sur inter-area, peu importe coûts. Même si O IA a coût 5 et O a coût 100, O (intra) est sélectionnée.

---

### Question 16 (Avancée)
**Enoncé** : Configuration OSPF multi-area : `area 0`, `area 10`, `area 20`. Area 10 est Stub, Area 20 est Standard. Impact sur Area 10 ?

A) Area 10 recoit routes Area 20 via Type 3  
B) Area 10 n'a pas routes Area 20  
C) Area 10 n'accepte aucune external (Type 5)  
D) A et C

**Réponse** : D) A et C

**Explication** : Stub Area (10) :
- Accepte Type 3 (inter-area sommaires) depuis Area 20 via Area 0 ✓
- Rejette Type 5 (routes externes) ✓
- Reçoit défaut 0.0.0.0/0 vers infrastructure

---

### Question 17 (Avancée)
**Enoncé** : Prefix-list `ip prefix-list EXPORT seq 10 deny 192.168.0.0/16 ge 24 le 24` appliquée via `distribute-list prefix EXPORT out Gi0/0`. Qu'est-ce qui est bloqué ?

A) Toutes routes 192.168.0.0/16  
B) Routes 192.168.0.0/24 SEULEMENT  
C) Routes <= /24 in 192.168.0.0/16  
D) Routes > /24 in 192.168.0.0/16

**Réponse** : B) Routes 192.168.0.0/24 SEULEMENT

**Explication** : Prefix-list avec `ge 24 le 24` = "greater than or equal /24 AND less than or equal /24" = exactement **/24**. Bloque seulement 192.168.0.0/24, pas autres subnets like /23 ou /25.

---

### Question 18 (Avancée)
**Enoncé** : Une Stub Area avec 3 Internal Routers. Si ABR défaille, qu'arrive aux routes inter-area ?

A) Routes deviennent unknowns (inaccessibles)  
B) Type 3 LSAs pas mises à jour (ne change)  
C) Failover instantané via backup ABR  
D) A est le plus probant

**Réponse** : A) Routes deviennent unknowns (inaccessibles)

**Explication** : Stub Area reçoit routes inter-area et externes via défaut 0.0.0.0/0 annoncée par ABR. Si ABR défaille, **pas de backup** (à moins deux ABRs configurés). Stub Area planifier avec multiple ABRs pour redundance.

---

### Question 19 (Avancée)
**Enoncé** : NSSA avec ASBR redistribue BGP 65000 avec 100 subnets. Impact LSDB ?

A) 100 Type 5 LSAs flooded AS-wide  
B) 100 Type 7 LSAs generées, traduit Type 5 via ABR  
C) 1 Type 5+100 Type 7 (double)  
D) Pas de LSA (NSSA rejette external)

**Réponse** : B) 100 Type 7 LSAs generées, traduit Type 5 via ABR

**Explication** : Routes redistribuées dans NSSA deviennent **Type 7 LSAs**, flooded dans NSSA Area seulement. ABR **traduit** chaque Type 7 → Type 5 quand flooded vers Area 0 (AS-wide).

---

### Question 20 (Avancée)
**Enoncé** : OSPF Totally Stubby Area 30 (+ no-summary). Quelles routes Area 30 routers connaissent ?

A) Que routes intra-area + défaut 0.0.0.0/0  
B) Intra-area + inter-area via Type 3  
C) Toutes routes (standard area)  
D) Aucune route

**Réponse** : A) Que routes intra-area + défaut 0.0.0.0/0

**Explication** : Totally Stubby = rejette Type 3,4,5 (inter-area & external). Routeurs ont LSDB minimum :
- Type 1 LSAs (local intra-area)
- Type 2 LSAs (local networks)
- Default 0.0.0.0/0 via ABR

---

### Question 21 (Avancée)
**Enoncé** : Filtrage : `distribute-list prefix DENY-BGPROUTES in Serial0/0` OSPF process. Le filtre affecte quoi ?

A) LSA Type 5 reçues  
B) Routes RIB (après installation)  
C) LSAs routes BGP redistribuées  
D) Flooding OSPF locales

**Réponse** : B) Routes RIB (après installation)

**Explication** : `distribute-list in` opère sur **routes finales RIB**, pas LSAs. Filtre appliqué APRÈS SPF et installation RIB. LSAs restent dans LSDB (mais route bloquée de RIB).

---

### Question 22 (Avancée)
**Enoncé** : Area filter-list `area 10 filter-list prefix OUT out` sur ABR. Si route 10.0.0.0/24 filtrée, qu'arrive ?

A) Route annulée dans Area 0  
B) Type 3 LSA 10.0.0.0/24 pas flooded vers Area 0  
C) Area 10 routers ne connaissent pas la route  
D) B et C faux

**Réponse** : B) Type 3 LSA 10.0.0.0/24 pas flooded vers Area 0

**Explication** : `area X filter-list prefix Y out` = **ABR ne génère pas Type 3** pour routes matchant prefix-list. Route reste connue dans Area X mais pas annoncée inter-area.

---

### Question 23 (Avancée)
**Enoncé** : Réseaux discontigus : Area 0 a 10.0.0.0/24 et Area 2 a aussi 10.0.0.0/24. Risque ?

A) OSPF détecte et corrige automatiquement  
B) Trafic peut prendre mauvaise route (non-deterministic)  
C) Routeurs Cisco refusent config  
D) Les deux 10.0.0.0/24 sont installées ECMP

**Réponse** : B) Trafic peut prendre mauvaise route (non-deterministic)

**Explication** : OSPF accepte discontigus (contrairement EIGRP). Mais RIB installation peut être imprévisible (dépend timing SPF, ABR ordering, etc.). **Solution : Éviter discontigus ou utiliser full routes** (pas de résumé).

---

### Question 24 (Avancée)
**Enoncé** : ASBR dans NSSA configué `summary-address 172.16.0.0 255.255.240.0 not-advertise`. Impact ?

A) Route 172.16.0.0/20 supprimée (null route Type 7)  
B) Route 172.16.0.0/20 acceptée mais bloquée RIB  
C) Aucune impact (not-advertise ignée)  
D) Type 5 LSAs bloquées

**Réponse** : A) Route 172.16.0.0/20 supprimée (null route Type 7)

**Explication** : `summary-address not-advertise` crée route **null 0** (black hole) dans cette ASBR. Trafic destiné à cette résumé est droppé localement (symétrique discontigu prevention).

---

### Question 25 (Avancée)
**Enoncé** : Priorité route OSPF : Intra-O [110/10], Inter-O IA [110/5], External-E1 [110/20], External-E2 [110/1]. Laquelle est installée RIB ?

A) E2 [110/1] (coût minimal)  
B) O [110/10] (intra-area)  
C) O IA [110/5] (inter-area)  
D) E1 [110/20] (external type 1)

**Réponse** : B) O [110/10] (intra-area)

**Explication** : **Path Preference Prime** :
1. Intra-area (O) **wins** even higher costs
2. Inter-area (O IA) next
3. External E1/E2 last

Même si autres routes ont coûts bas, Intra-area sélectionnée.

---

## Résumé des Réponses

| Q | Rép | Q | Rép |
|---|-----|---|-----|
| 1 | C | 13 | A |
| 2 | A | 14 | B |
| 3 | D | 15 | B |
| 4 | B | 16 | D |
| 5 | C | 17 | B |
| 6 | B | 18 | A |
| 7 | B | 19 | B |
| 8 | A | 20 | A |
| 9 | B | 21 | B |
| 10 | C | 22 | B |
| 11 | B | 23 | B |
| 12 | A | 24 | A |

---
**Durée estimée** : 75-90 minutes  
**Difficulté** : Intermédiaire (Q1-12), Avancée (Q13-25)
