# Checkpoint Exam: BGP
## Modules 11-12: Border Gateway Protocol & Advanced BGP

**Exam Code:** ENCOR-CHK-11-12  
**Duration:** 90 minutes  
**Total Questions:** 50  
**Passing Score:** 70% (35/50)  
**Topics Covered:** BGP Fundamentals, Multihoming, Route Filtering, Route Maps, Communities, Path Selection

---

## SECTION 1: BGP FUNDAMENTALS (Questions 1-20)

### Question 1
Quel est le protocole d'application utilisé par BGP pour établir les sessions de routage?

A) UDP port 179  
B) TCP port 179  
C) TCP port 180  
D) IP protocol 179  

**Answer:** B  
**Explanation:** BGP utilise le port TCP 179 pour établir et maintenir les sessions avec les routeurs pairs. Contrairement aux IGPs qui utilisent l'UDP (EIGRP, RIPv2) ou qui tournent directement sur IP (OSPF #89), BGP repose sur TCP pour la fiabilité garantie et les contrôles de flux.

---

### Question 2
Lequel des éléments suivants est un exemple correct de plage d'ASN privé?

A) 1-63999  
B) 64000-65000  
C) 64512-65535  
D) 65536-100000  

**Answer:** C  
**Explanation:** Les ASNs privés 16-bit sont dans la plage **64512-65535** (RFC 1918 pour ASNs). La plage moderne 32-bit d'ASNs privés est **4200000000-4294967294**. Ces plages sont réservées pour l'utilisation interne et ne doivent pas être utilisées sur l'Internet public.

---

### Question 3
Quel est l'administrative distance (AD) pour une route iBGP?

A) 20  
B) 90  
C) 110  
D) 200  

**Answer:** D  
**Explanation:** Les routes iBGP ont un AD par défaut de **200**, tandis que les routes eBGP ont un AD de **20**. Cela signifie que eBGP (routes des fournisseurs de services externes) sont fortement préférées aux iBGP, reflétant le fait que eBGP représente habituellement le chemin optimal vers des destinations externes.

---

### Question 4
Qu'est-ce qu'un "Autonomous System" (AS) dans le contexte BGP?

A) Un groupe de routeurs exécutant le même IGP sous une administration commune  
B) Une seule adresse IP unique sur Internet  
C) Une interface de routeur administrativement configurée  
D) Un processus OSPF s'exécutant sur un routeur  

**Answer:** A  
**Explanation:** Un **Autonomous System (AS)** est un groupe de réseaux interconnectés et de routeurs gérés sous une Administration Commune. Tous les routeurs dans un AS exécutent le même IGP et partagent la même politique de routage. Les ASs sont identifiés par un numéro d'AS (ASN) unique.

---

### Question 5
Quel est le rôle principal du champ AS_Path dans les annonces BGP?

A) Stocker la métrique du coût du chemin  
B) Prévenir les boucles de routage en listant tous les ASs traversés  
C) Identifier le prochain saut immédiat vers la destination  
D) Marquer la priorité locale d'une route  

**Answer:** B  
**Explanation:** L'**AS_Path** est un attribut BGP well-known mandatory qui contient une liste de tous les Autonomous Systems que la route a traversés. Si un routeur voit son propre AS dans l'AS_Path d'une annonce reçue, il rejette la route pour éviter la boucle. Ceci est la méthode BGP de prévention des boucles.

---

### Question 6
Quel est le désavantage principal d'utiliser une seule connexion BGP vers un fournisseur de services (SP)?

A) Coût plus élevé  
B) Point unique de défaillance (SPOF) si SP ou lien échoue  
C) Impossibilité de annoncer les routes locales  
D) Incapacité à utiliser MP-BGP  

**Answer:** B  
**Explanation:** Avec une seule connexion eBGP vers un SP, la défaillance de cette liaison ou du réseau du SP entraîne une perte totale de connectivité Internet/externe. Le **BGP Multihoming** ajoute des connexions redondantes vers un ou plusieurs SPs pour assurer la continuité du service.

---

### Question 7
Quel concept de conception redondante BGP utilise des connexions vers des fournisseurs DIFFÉRENTS?

A) Single Provider Multihoming  
B) Dual Provider Multihoming  
C) BGP Path Redundancy  
D) iBGP Mesh  

**Answer:** B  
**Explanation:** Le **Dual Provider (ou Multi-Provider) Multihoming** utilise deux ou plus de fournisseurs Internet différents pour assurer la redondance non seulement contre les défaillances de lien, mais aussi contre les défaillances du réseau du SP lui-même. Ceci offre la plus haute niveau de redondance.

---

### Question 8
Quel est le problème principal du "Transit Routing" non planifié dans une topologie multihoming?

A) Il réduit la bande passante disponible  
B) Il cause le trafic d'autres sites à transiter via des routeurs branche non préparés  
C) Il augmente le délai de convergence BGP  
D) Il désactive automatiquement la route sortante  

**Answer:** B  
**Explanation:** Le "Transit Routing non planifié" se produit quand un routeur branche accepte du trafic de transit entre d'autres sites sans être préparé pour cela. Par exemple, le trafic entre Site 3 et Site 5 traverse incorrectement le routeur branche R41, saturant ses circuits non dimensionnés pour ce trafic. Ceci est évité via des **Outbound Route Filters (ORF)**.

---

### Question 9
Comment BGP utilise-t-il les Address Families (AFI/SAFI) dans MP-BGP?

A) Pour identifier le processus BGP sur un routeur  
B) Pour supporter plusieurs protocoles (IPv4, IPv6) et types (unicast, multicast) sur la même session  
C) Pour établir des sessions TCP séparées par famille  
D) Pour augmenter le nombre maximum de voisins BGP  

**Answer:** B  
**Explanation:** Les **Address Families (AFI - Address Family Identifier et SAFI - SubAddress Family Identifier)** dans **Multiprotocol BGP (MP-BGP)** permettent une seule session BGP de supporter multiples protocoles de routage. Par exemple, une session peut transporter à la fois des routes IPv4 et IPv6 en utilisant les attributs **MP_REACH_NLRI** et **MP_UNREACH_NLRI**.

---

### Question 10
Quel est le rôle des "Well-Known Mandatory" path attributes dans BGP?

A) Ils s'acheminent automatiquement via les chemins les plus courts  
B) Ils doivent être inclus dans CHAQUE annonce BGP et reconnus par tous les routeurs BGP  
C) Ils sont optionnels et ignorés si non compris  
D) Ils s'appliquent uniquement à l'iBGP interne  

**Answer:** B  
**Explanation:** Les **Well-Known Mandatory** attributes (comme ORIGIN, AS_Path, NEXT_HOP) doivent être :
- Inclus dans CHAQUE annonce de préfixe BGP
- Reconnus et compris par TOUS les routeurs BGP
- Transmis à tous les pairs BGP (sauf direction)

Leur absence ou modification non appropriée peut casser le protocole.

---

### Question 11
Comment les sessions BGP multi-hop diffèrent-elles des sessions single-hop?

A) Multi-hop doit utiliser EBGP uniquement  
B) Multi-hop utilise TCP avec un processus underlay pour établir la session  
C) Multi-hop n'utilise pas le port 179  
D) Multi-hop est exclusiv à l'iBGP  

**Answer:** B  
**Explanation:** Les **sessions BGP multi-hop** (par exemple iBGP entre deux loopback addresses non directement connectées) nécessitent:
- Une route existante dans la RIB (via tout IGP) pour atteindre le destinataire
- Une session TCP qui utilise cette route comme chemin underlay
- Une configuration **neighbor <IP> update-source loopback<X>**

Les sessions single-hop (ebgp) directement connectées ne necessitent pas ceci.

---

### Question 12
Quel est l'objectif principal des Access Control Lists (ACLs) dans le contexte du routage BGP?

A) Filtrer le trafic de données ingérant sur les interfaces  
B) Identifier les réseaux pour le filtrage et la manipulation de routes de routage  
C) Limiter le nombre de voisins BGP  
D) Configurer les priorités des interfaces  

**Answer:** B  
**Explanation:** Dans le contexte BGP (et routage), les ACLs sont utilisées pour:
- **Classification de trafic** - identifier les prefixes/réseaux pour appliquer des politiques
- Filtrage de routes - permettre ou bloquer les annonces basé sur la destination
- Pas pour le filtrage des données de utilisateur (bien que ACLs s'appliquent aussi là)

Les ACLs Standard utilisent uniquement la source, les ACLs Extended ajoutent la destination et les protocoles.

---

### Question 13
Quel est le rôle des "Prefix Lists" par rapport aux ACLs pour le filtrage BGP?

A) Prefix Lists ne peut pas être utilisé para BGP  
B) Prefix Lists sont plus spécifiques et efficaces pour le filtering de BGP  
C) Prefix Lists s'appliquent uniquement à IPv6  
D) Prefix Lists remplace les ACLs obsolètes obligatoirement  

**Answer:** B  
**Explanation:** Les **Prefix Lists** pour les routes BGP:
- Sont l'**approche préférée moderne** pour le filtrage BGP comparé aux ACLs
- Permettent le filtrage basé sur **prefix ET prefix-length** (pas seulement la destination)
- Syntaxe plus simple et plus efficace pour les politiques de routage
- Exemple : `ip prefix-list FILTER seq 10 permit 10.1.0.0/16 le 32`

---

### Question 14
Quelle est la structure basic d'une Route Map dans Cisco IOS?

A) route-map <nom> permit | deny <séquence> { conditions } { actions }  
B) map <nom> allowing-routes <destination> <action>  
C) route-policy <nom> { matching rules ; setting actions ; }  
D) bgp route-map <nom> filter <source>  

**Answer:** A  
**Explanation:** La structure correcte est:
```
route-map <name> {permit | deny} <sequence>
 match <condition>
 set <action>
```

Par exemple :
```
route-map BGP-OUT permit 10
 match prefix-list INTERNAL-NETWORKS
 set local-preference 150
```

Les Route Maps sont utilisés pour le filtrage/manipulation complexe de routes.

---

### Question 15
Quel est le "match" d'une Route Map BGP si vous voulez filtrer basé sur le AS_Path?

A) match as-path <ACL>  
B) match bgp-path <pattern>  
C) match as <number>  
D) match autonomous-system <value>  

**Answer:** A  
**Explanation:** Pour correspondre les routes basé sur le AS_Path (ou plus généralement, le numero d'AS):
```
route-map FILTER-AS permit 10
 match as-path 1
!
ip as-path access-list 1 permit _65001_
```

La AS-Path ACL utilise des regular expressions pour correspondre la chaîne AS_Path. Par exemple, `_65001_` correspond à AS 65001 n'importe où dans le chemin et en l'entourant.

---

### Question 16
Quel est le rôle des "BGP Communities" dans la politique de routage BGP?

A) Identifier les voisins BGP dans le neighbors table  
B) Taguer les routes avec une marque permettant l'application de politiques dans le même AS ou d'autres ASs  
C) Limiter le nombre d'équipes qui gèrent le BGP  
D) Configurer la redondance du chemin  

**Answer:** B  
**Explanation:** Les **BGP Communities** sont des attributs optionnels transitive qui "tagent" une route avec une marque (pair numérique). Les routeurs dans le même AS (ou d'autres ASs avec lesquels nous partageons des routes) peuvent reconnaître cette marque et appliquer des politiques (par ex., set LOCAL_PREFERENCE). Format : **ASN:value** (p.ex., 65001:100).

---

### Question 17
Quel est la bien-known community "NO_EXPORT" et son rôle?

A) Elle indique que la route ne doit pas être exportée à d'autres ASs eBGP  
B) Elle signifie que la route doit obtenir la priorité d'export maximal  
C) Elle configure le coût d'export de la route  
D) Elle n'a pas d'effet spécial sur les routes BGP  

**Answer:** A  
**Explanation:** La well-known community **NO_EXPORT** (valeur standard 65535:65281) indique que la route:
- Ne doit pas être annoncée à d'autres sessions **eBGP** (routeurs dans des ASs différents)
- PEUT être annoncée aux routeurs **iBGP** (dans le même AS)
- Useful untuk les routes internes à un AS qui ne doivent pas traverser vers l'extérieur

Autres well-known: NO_ADVERTISE, INTERNET.

---

### Question 18
Quel est le premier critère utilisé par BGP pour sélectionner la meilleure route?

A) Highest weight (Cisco proprietary)  
B) Local Preference (si égales, continued)  
C) AS_Path length  
D) Lowest MED  

**Answer:** A  
**Explanation:** L'ordre BGP Best Path Selection est (simplifié):
1. **Weight** (0-65535, défaut 32768 pour local, 0 pour learned) - PLUS ÉLEVÉ gagne 
2. Local Preference (défaut 100) - UNE SEULE FOIS dans l'AS - PLUS ÉLEVÉE gagne
3. Locally originated (aggregate ou redistribute) gagne sur learned
4. AS_Path length - PLUS COURT gagne
5. Origin type (IGP > EGP > Incomplete)
6. MED - PLUS BAS gagne
7. eBGP > iBGP
8. IGP metric to next-hop
9. Router ID (le plus élevé)

---

### Question 19
Comment configurer la Local Preference pour influencer la sélection de route BGP sortante?

A) **bgp local-preference <value>** (global)  
B) **set local-preference <value>** (dans route-map)  
C) **local-preference <value>** (sous neighbor)  
D) **ip preference <value>** (interface)  

**Answer:** B  
**Explanation:** Pour modifier Local Preference:
```
route-map BGP-IN permit 10
 match prefix-list EXTERNAL-ROUTES
 set local-preference 150
!
router bgp 65001
 neighbor <ip> route-map BGP-IN in
```

Ou globalement pour toutes les routes reçues via un neighbor:
```
router bgp 65001
 neighbor <ip> default-local-preference 150
```

Local Preference s'applique AU SEIN d'un AS et affecte les décisions d'export iBGP.

---

### Question 20
Quel est l'avantage d'utiliser **Outbound Route Filtering (ORF)** dans un design BGP Multihoming?

A) Augmenter la bande passante disponible  
B) Empêcher les routeurs branche de devenir des routeurs de transit  
C) Réduire l'administrative distance des routes  
D) Augmenter la convergence BGP  

**Answer:** B  
**Explanation:** **Outbound Route Filtering (ORF)** permet à une branche de filtrer ce qu'elle ANNONCE vers ses voisins BGP. Par exemple, une branche dit "Je n'annonce QUE mes routes locales (LAN), pas les routes que j'ai apprises d'autres voisins". Ceci empêche le transit non planifié où le trafic site-to-site essaierait de traverser cette branche.

Format :
```
route-map BRANCH-OUT permit 10
 match prefix-list OWN-NETWORKS
!
neighbor <SP> route-map BRANCH-OUT out
```

---

## SECTION 2: ADVANCED BGP & BGP OPTIMIZATION (Questions 21-50)

### Question 21
Quel est le but principal des "Route Reflectors" (RR) dans une topologie iBGP?

A) Réduire la taille de l'AS_Path dans les routes  
B) Remplacer la nécessité d'une mesh iBGP complète  
C) Filtrer les routes eBGP reçues  
D) Augmenter le nombre de voisins iBGP maximum  

**Answer:** B  
**Explanation:** Un **Route Reflector (RR)** dans iBGP:
- Permet à **certains routeurs iBGP de ne pas faire une mesh complète** (pleine adjacencies avec tous les autres routeurs iBGP)
- Les routeurs clients (non-RR) font que une adjacency iBGP avec le RR
- Le RR **réfléchit les routes** entre clients et vers d'autres routeurs (comme OSPF ABR réflète les routes)
- Ceci réduit drastiquement le nombre d'adjacencies iBGP dans les gros ASs

Configuration : `router bgp <AS> ; address-family ipv4 ; bgp route-reflector-cluster-id <id>`

---

### Question 22
Quel régularExpression pattern capturait AS 65001 si c'est le dernier AS au AS_Path?

A) 65001$  
B) ^65001  
C) _65001_  
D) 65001.*  

**Answer:** A  
**Explanation:** Dans les AS-Path regex pour BGP:
- `$` = fin de chaîne (match AS si dernier)
- `^` = début de chaîne
- `_` = mot border (AS séparé)

Donc `65001$` capture AS 65001 seulement s'il est le DERNIER AS (l'annonceur direct), tandis que `_65001_` capture n'importe où dans le chemin.

Exemple AS-Path ACL :
```
ip as-path access-list 1 permit ^65001$
```
Ceci correspond aux routes originaires de AS 65001 uniquement.

---

### Question 23
Quel est l'effet de configurer **set metric <value>** (MED) dans une route-map BGP?

A) Influence la sélection de route iBGP au sein du propre AS  
B) Indique les coûts de lien pour l'OSPF métrique  
C) Envoie un signal au voisin eBGP sur la préférence du prochain saut (loin des autres routeurs)  
D) C'est strictement utilisé para la classification du trafic QoS  

**Answer:** C  
**Explanation:** La **Multi-Exit Discriminator (MED)**, aussi appelée "metric", est envoyée aux **voisins eBGP** pour indiquer "si tu as multiples chemins vers ce préfixe par mon AS, préfère celui avec le MED le plus BAS". 

par exemple, si nous avons deux connexions vers le même SP :
- Connexion A: MED 100
- Connexion B: MED 200

Le SP préférera envoyer le trafic vers nous via la connexion A (MED plus bas).

```
route-map MED-ATT1 permit 10
 set metric 100
!
router bgp 65001
 neighbor <SP> route-map MED-ATT1 out
```

---

### Question 24
Quel est le comportement par défaut de BGP pour les routes reçues via iBGP vers les autres routeurs iBGP?

A) Les routes sont annoncées à tous les pairs iBGP  
B) Les routes NE sont PAS annoncées aux pairs iBGP (sauf par route-reflection)  
C) Les routes sont annoncées uniquement aux pairs eBGP  
D) Les routes créent automatiquement une adjacency IBGP mesh  

**Answer:** B  
**Explanation:** C'est une règle clé d'iBGP:
- Un routeur iBGP **NE fera PAS re-advertiser** une route apprise d'un autre routeur iBGP vers les tiers iBGP
- Il ADVERTISera uniquement vers les pairs eBGP
- Ceci empêche les boucles dans les topologies iBGP

Solutions :
- **Route Reflector** - un RR fait re-advertiser les routes apprises iBGP
- **Confederation** - logiquement divise un grand AS en plusieurs mini-ASs

Ceci s'applique uniquement aux routes APPRISES iBGP, pas celles originaires localement ou apprises via eBGP.

---

### Question 25
Quel est l'impact de changer la **Weight** dans BGP comparé à changer **Local Preference**?

A) Weight affecte TOUTES les routes, Local Preference affecte uniquement iBGP  
B) Weight est local au routeur, Local Preference affecte la décision au sein du AS  
C) Elles ont le même impact, utiliser l'une ou l'autre  
D) Weight est une standard IETF, Local Preference est propriétaire Cisco  

**Answer:** B  
**Explanation:**
- **Weight** (0-65535) : 
  - C'est un attribut **propriétaire Cisco**
  - S'applique UNIQUEMENT au routeur LOCAL
  - Affecte les décisions de routage SUR CE ROUTEUR pour ces routes
  - Plus élevé = préféré

- **Local Preference** (0-65535, défaut 100) :
  - C'est un attribut IETF standard **transmitted entre routeurs iBGP**
  - Affecte la décision pour TOUS les routeurs du même AS
  - Plus élevé = préféré

Cas d'usage : Weight pour tuner localement, Local Pref pour coordonner tout l'AS.

---

### Question 26
Comment appliquer une route-map au trafic reçu d'un NEIGHBOR BGP spécifique?

A) **route-map <name> in** (sous neighbor)  
B) **neighbor <ip> route-map <name> in** (sous router bgp)  
C) **apply route-map <name> from neighbor** (N/A - pas valide)  
D) **policy-map neighbor <ip> <route-map>**  

**Answer:** B  
**Explanation:** Syntaxe correcte :
```
router bgp 65001
 address-family ipv4
  neighbor <ip> route-map FILTER-IN in
  neighbor <ip> route-map FILTER-OUT out
!
route-map FILTER-IN permit 10
 match <condition>
 set <action>
```

- `in` = appliquer pour les routes REÇUES de ce neighbor
- `out` = appliquer pour les routes ANNONCÉES à ce neighbor

---

### Question 27
Quel est le rôle de la **aggregate-address** dans BGP?

A) Combiner multiples routes dans une seule route plus proche  
B) Augmenter la métrique pour les routes agrégées  
C) Filtrer les routes en double  
D) Créer des limites de zone administrative  

**Answer:** A  
**Explanation:** L'**aggregate-address** consolidate multiples routes spécifiques en une seule route résumée:
```
router bgp 65001
 address-family ipv4
  aggregate-address 10.0.0.0 255.0.0.0
```

Ceci:
- Crée une route agrégée 10.0.0.0/8 
- Par défaut, SUPPRIMe les routes spécifiques (10.1.0.0/16, 10.2.0.0/16, etc.)
- Réduit drastiquement la taille des tables de routage

Avec `summary-only`, UNIQUEMENT la route agrégée est annoncée.
Avec `suppress-map`, on peut sélectivement annoncer certaines routes malgré l'agrégation.

---

### Question 28
Quel est le premier élément que BGP vérifie quand il reçoit une annonce d'une route existante avec un AS_Path différent?

A) Changer automatiquement vers le nouveau AS_Path  
B) Comparer le nouvel AS_Path avec l'existant via la sélection de route  
C) Rejeter la nouvelle annonce car la route existe déjà  
D) Demander au neighbor de confirmer l'AS_Path  

**Answer:** B  
**Explanation:** Quand BGP reçoit une route avec un **paththrough différent**:
1. La route entrante est comparée VERSUS l'existante via l'**algorithme de sélection du meilleur chemin** (Weight → LocalPref → ...AS_Path → ...)
2. Si le nouveau chemin est meilleur (selon cet algorithme), la route est mises à jour
3. Une route FLAP/ADVERTISEMENT change est générée

BGP supporte efficacement la **redundance** et **convergence rapide** à de meilleurs chemins.

---

### Question 29
Comment fonctionne le "bestpath compare-routerid" dans Cisco BGP?

A) Comparer les router-id pour département qui est le meilleur chemin lorsque d'autres critères sont égaux  
B) Forcer les routeurs à broadcaster leurs router-ids  
C) Créer une limitation de neighbors basée sur les router-ids  
D) N/A - pas une commande Cisco valide  

**Answer:** A  
**Explanation:** Par défaut, dans la sélection de route BGP, si tout est égal (weight, local-pref, sourcing, AS_Path, origin, MED, eBGP vs iBGP, IGP metric), BGP compares les **router-id du next-hop** - le router-id le plus ÉLEVÉ gagne. C'est un tiebreaker final.

Avec `bgp bestpath compare-routerid`, Cisco force ce comparison AVANT de comparer les IGP metrics, changeant la précédence.

Utilité : Pour un comportement prévisible déterministe dans les gros ASs avec multiples RRs.

---

### Question 30
Quel est le désavantage principal de configurer les routes redistribuées (ex OSPF → BGP) uniquement?

A) Les routes prennent trop longtemps à converger  
B) Les routes internes (comme les réseaux clients) ne sont pas propagées vers nos pairs  
C) Cela crée des boucles BGP automatiquement  
D) La redistribution est illégale sur certains types de lien  

**Answer:** B  
**Explanation:** Si vous UNIQUEMENT redistribuez des routes (ex, redister OSPF vers BGP), les réseaux connectés DIRECTEMENT (network statements dans BGP) NE se propagent pas. Dans les configurations production d'Enterprise :
- Utilizer les **network statements pour annoncer les préfixes locaux/authentiques**
- Utilizer la **redistribution pour annoncer les routes apprises d'autres sources** (autres IGPs, défaultes routes)

Cela assure que tout le vrai réseau local est publicisé.

```
router bgp 65001
 address-family ipv4
  network 10.1.0.0 mask 255.255.0.0  ← LOCAL
  redistribute ospf 1              ← FROM OTHER SOURCES
```

---

### Question 31
Qu'est-ce qui se passe si un routeur iBGP reçoit une route avec une NEXT_HOP inaccessible?

A) La route s'installed automatiquement avec le next-hop mis à jour  
B) La route ne s'installe pas dans la table de routage (route remain dans BGP table as inconnu pending)  
C) Un message ICMP DEST UNREACHABLE est envoyé au sender  
D) La route est redistribuée automatiquement aux autres IGPs  

**Answer:** B  
**Explanation:** Pour une route iBGP, le **next-hop ne doit pas être changé** (sauf en utilisant **next-hop-self**). Si le NEXT_HOP n'est PAS accessible via une route dans la RIB:
- La route **reste dans la BGP table** mais n'est **PAS installée** dans la RIB/routing table
- Cela s'appelle **"inaccessible" ou "unreachable" dans le contexte BGP**
- Une fois que la RIB contient une route vers le NEXT_HOP, la route BGP peut être installée

C'est pourquoi l'iBGP dépend d'un IGP fiable pour atteindre tous les next-hops.

---

### Question 32
Quel est l'administratif du "no synchronization" dans BGP?

A) Désactiver la vérification que les routes iBGP sont aussi apprises via IGP  
B) Augmenter la vitesse de convergence BGP  
C) Disableler les timers BGP de syncopation  
D) Permet à l'iBGP d'ignorer NEXT_HOP accessibility  

**Answer:** A  
**Explanation:** L'older BGP **synchronization rule** requérais qu'une route iBGP **soit AUSSI apprise via l'IGP interne** avant de pouvoir être annoncée à d'autres eBGP voisins. Cela assurait que les clients pouvaient atteindre les destinations via l'IGP.

Avec **no synchronization** (défaut modern IOS) :
- Une route iBGP can être immédiatement annoncée vers eBGP voisins
- Plus rapide, car pas d'attente pour la propagation IGP

C'est par défaut `no synchronization` sur les Cisco modernes.

```
router bgp 65001
 no synchronization  (défault; rarement besoin de configurer)
```

---

### Question 33
Quel attribut BGP contrôle si une route est propagée en dehors d'un confédération?

A) CONFEDERATION_SEQUENCE  
B) LOCAL_PREFERENCE  
C) NO_EXPORT community  
D) CONFEDERATION_SET versus CONFEDERATION_SEQUENCE PATH  

**Answer:** C ou autre - dépend du contexte.  
**Explanation:** Techniquement, les attributs de confédération (CONFEDERATION_SEQUENCE, CONFEDERATION_SET) ne faut pas directement contrôler la propagation. Le contrôle principal est via **Communities** (NO_EXPORT) ou d'autres politiques de route-map.

MAIS dans une **confédération BGP** :
- Les routes au sein de la confédération utilisent **CONFEDERATION_SEQUENCE dans le AS_Path**
- Les routes à l'extérieur voient uniquement le **numéro de sous-AS, pas CONFEDERATION internals**

NO_EXPORT empêche la propagation à l'extérieur de l'AS/confédération.

---

### Question 34
Quel est l'effet de la commande **neighbor <IP> allowas-in <count>**?

A) Permettre les routes avec l'ASN du routeur dans l'AS_Path  
B) Augurise le nombre de fois que ce neighbor spécifique peut être rejoint  
C) Limite les routes annoncées au neighbor  
D) Augmente le MED pour les routes du neighbor  

**Answer:** A  
**Explanation:** Par défaut, BGP rejette TOUTES les annonces contenant son propre AS dans l'AS_Path (loop prevention). Cependant, dans certaines situations légitimes (multples ASN pour un provider, confederation, RRs):

```
router bgp 65001
 neighbor 10.1.1.1 allowas-in 2
```

Cela PERMET à ce neighbor d'annoncer des routes avec AS 65001 dans l'AS_Path, up à 2 fois. Bien sûr, ceci DOIT être très contrôlé pour éviter les boucles réelles.

Cas d'usage : Fournisseur utilisant multiple ASNs,confédérations, RRs dans une configuration spéciale.

---

### Question 35
Comment fixer rapidement un problem où le voisin eBGP est non-reachable parce qu'il n'a pas de route jusqu'à lui?

A) Ajouter une route statique vers le IP du voisin  
B) Configurer **neighbor <IP> update-source <interface>**  
C) Redistribuer une défault route dans l'IGP  
D) Augmenter le BGP timers connecter  

**Answer:** A  
**Explanation:** Rapide fix :
```
ip route <neighbor-ip> 255.255.255.255 <next-hop>
```

Ou mieux, via l'IGP - faire sûr que le chemin vers le neighbor IP est annoncé via OSPF, EIGRP, etc.

`update-source` est utile pour iBGP loopback sessions, pas pour l'accessibilité immédiate.

---

### Question 36
Quel est l'avantage de configurer **passive-interface** pour BGP (quand applicable)?

A) Prévenir la propagation de routes BGP sur cette interface  
B) N/A - BGP ne supporte pas de passive-interfaces comme les IGPs  
C) Reduce la CPU usage sur l'interface  
D) Faire la neighbor automatiquement via une découverte  

**Answer:** B  
**Explanation:** BGP n'a pas de concept "passive interface" comme OSPF ou EIGRP. Pourquoi ?
- BGP neighbors sont DÉFINIS EXPLICITEMENT avec une commande **neighbor**
- BGP n'a pas d'hello découverte - c'est tout manuel
- Tous les interfaces run BGP SEULEMENT si configuré via **neighbor statements**

Donc, il n'est pas besoin marketing de "passive" - si vous ne créez pas un neighbor, la interface n'est pas BGP active.

---

### Question 37
Comment utiliser un "route target" dans le contexte d'une MPLS VPN BGP?

A) Identifier les routes qui appartiennent à un VPN customer spécifique  
B) Filtrer sélectivement les packets plutôt que les routes  
C) Définir la politiquement préférée pour les changements de route  
D) Assurer les conditions d'authentification du voisin  

**Answer:** A  
**Explanation:** Dans les **MPLS L3 VPNs** (RFC 4364), le **Route Target (RT)** est une Extended Community attendre à chaque VPN route. Il identifie quels clients VPEs et les sites devraient recevoir cette route.

Par exemple :
- Client A routes : RT 65001:100
- Client B routes : RT 65001:200

Un VPE situé à deux clients peut "importer" les deux RTs configurées pour recevoir les deux ensembles de routes.

Permet la ségrégation des clients sûrement sur shared infrastructure MPLS.

---

### Question 38
Quel est le comportement d'une route-map explicitement DENIED?

A) Les routes modifiées sont annoncées  
B) Les routes sont annoncées non modifiées  
C) Les routes sont FILTRÉES (rejetées)  
D) Les routes sont mises en queue pour later processing  

**Answer:** C  
**Explanation:** Les route maps actions :
- **permit** = lignes correspondantes sont traitées ET (opérationnelle continues au prochain permit clause si pas de explicitly denied)
- **deny** = les lignes CORRESPONDANT cette clause sont **FILTRÉES/REJETÉES** (non annoncées)

Exemple :
```
route-map BGP-OUT deny 10
 match prefix-list BLOCK
!
route-map BGP-OUT permit 20
 match prefix-list ALLOW
```

Tout ayant "BLOCK" va être rejeté. Tout ayant "ALLOW" va être annoncé.

---

### Question 39
Si deux eBGP routeurs directement connectées ont des administratives distances conflictives (un dit 20, un dit 200), quel impact?

A) La connexion eBGP échoue  
B) Pas d'impact - AD est local à chaque routeur  
C) Utilisez le plus élevé des deux  
D) BGP interrompt la session  

**Answer:** B  
**Explanation:** L'**Administrative Distance (AD)** est une propriété **LOCALE à chaque routeur**. Elle détermine comment ce routeur préfère les routes entre les protocoles.

Même si deux neighbors ont des AD différentes internes :
- Routeur A : eBGP AD = 20, iBGP AD = 200
- Routeur B : eBGP AD = 25, iBGP AD = 210

Les routes apprises via BGP sont toutes acceptées. L'AD affecte seulement la priorité COMPARÉE aux autres protocoles (OSPF, EIGRP) sur ce routeur.

---

### Question 40
Quel est l'indicateur que BGP utilise pour la "timely" route recurrence detection?

A) TTL (Time-to-Live) dans le IP header  
B) AS_Path + Origin validation  
C) BGP Border ASN matching  
D) UPDATE message sequence numbers  

**Answer:** B  
**Explanation:** BGP loop detection est basée sur :
- **AS_Path** - si votre AS apparaît dans le chemin, rejecter
- **Origin Type** - igualmente pour les indicateurs du degré de confiance

Pas de TTL-based loop detection comme les IGP. BGP utilise également :
- **Route Origin Validation (ROV)** - via RPKI, validate que les ASNs annonce réellement les routes qu'ils claimaient
- **BGPSEC** - extension signage des mises à jour BGP

---

### Question 41
Quell est le ORIGIN path attribute et comment l'interpréter?

A) Identificateur du routeur source  
B) INDICATEUR du type d'origin : IGP, EGP ou INCOMPLETE  
C) Numéro du prefix original  
D) Timestamp de when quand la route a été first learned  

**Answer:** B  
**Explanation:** **ORIGIN** est un Well-Known Mandatory attribute:
- **IGP** (code 0) = Route produits localement via `network` statement ou redistribution directe IGP
- **EGP** (code 1) = Apprise via EGP (déprécié, rarement vu)
- **INCOMPLETE** (code 2) = Route apprises via redistribution d'autres sources (statique, différent IGP)

Dans la sélection de route BGP, IGP > EGP > INCOMPLETE, donc les routes avec ORIGIN IGP sont préférées.

---

### Question 42
Comment rapidement visualize tous les routes dans la BGP table pour un routeur spécifique neighbor?

A) `show ip bgp neighbors <ip> routes`  
B) `show ip bgp <ip> advertised-routes`  
C) `show ip bgp summary neighbor <ip>`  
D) `show ip bgp neighbors <ip> advertised-routes`  

**Answer:** D  
**Explanation :** Commandes Cisco pour revisit les routes BGP :
- `show ip bgp summary` - estatut du neighbors
- `show ip bgp neighbors <ip> advertised-routes` - **routes ANNONCÉES À ce neighbor**
- `show ip bgp neighbors <ip> received-routes` - routes **REÇUES DE ce neighbor**
- `show ip bgp` - la BGP table complète

---

### Question 43
Si une route iBGP a un NEXT_HOP vers un externe (non-local) interface, qu'adveniet-il?

A) La route s'installe dans la RIB directement  
B) La route reste dans BGP table mais inaccessible jusqu'à ce que le next-hop soit atteigible  
C) BGP automatiquement modifie le next-hop à local  
D) The BGP session est réinitialisé  

**Answer:** B  
**Explanation:** Dans une configuration iBGP standard :
- Quand routeur eBGP apprend une route, il anoncia le next-hop vers le routeur iBGP voisins
- Le routeur iBGP essaie d'atteindre ce next-hop via la RIB (IGP)
- Si le next-hop n'est pas présent dans la RIB, la route demeure inaccessible et installable

C'est pourquoi la **IGP reliability** est CRITICAL pour la stabilité de la BGP. Typiquement :
- La route next-hop hop doit être connue via OSPF, EIGRP, etc.
- Configuration **next-hop-self** corrige souvent ce problème

---

### Question 44
Quel est le comportement du **bestpath as-path-ignore** dans BGP?

A) Ignore COMPLETELY la AS_Path dans la sélection de route  
B) Comparer les routes basé sur AS_Path quand d'autres criterès sont égaux  
C) Utilisé uniquement dans les confederation networks  
D) NOVALIDATE BGP AS_Path contre les voisins  

**Answer:** A  
**Explanation:** Avec **`bgp bestpath as-path-ignore`** :
```
router bgp 65001
 bgp bestpath as-path-ignore
```

Le AS_Path length **NE AFFECTE PAS** la sélection de route - les autres criteria sont utilisées à la place. C'est TRÈS dangereux à utiliser car :
- Peut créer une routing très sous-optimal
- Peut causer des loop si pas contrôlé

Typiquement utilisé dans des CERTS lab seulement pour tester d'autres concepts sans les interfères AS_Path.

---

### Question 45
Dans une configuration "confederation", quel est le rôle des numbers d'AS confédérés?

A) Identifier uniquement les routeurs d'edge externes  
B) Logiquement diviser un large AS en multiples petits ASs,sub chacun exécutant iBGP sans mesh complètes  
C) Replaçant completement le iBGP traditionnel  
D) Filtrer les routes basé sur les IDs confédérés  

**Answer:** B  
**Explanation:** Une **confédération BGP** regroupe plusieurs ASNs cans dans lequel logiquement un "meta-AS" pour la vue externe :
```
router bgp 65001            ← Numero de routeur locale
 bgp confederation identifier 65000  ← Global confederation meta-AS
 bgp confederation peers 65002 65003 65004
```

Avantages :
- Division d'un GRS AS (ex. 65000) en sub-confedés (65001, 65002, etc.)
- Chaque sub-confederation is_iBGP au sein, mais eBGP entre sous-confédérés
- Réduit explosion mesh iBGP sans avoir besoin au **routeur-reflector**
- EXTERNAL vois la confederation comme un seul AS (65000)

---

### Question 46
Quelle est la principale différence entre **suppress-map** et **unsuppress-map** dans **aggregate-address**?

A) `suppress-map` cachés des routes spécifiques lors de la aggregation ; `unsuppress-map` annoncé selectivement routes spécifiques malgré la suppression  
B) `suppress-map` ajoute des routes ; `unsuppress-map` les annule  
C) Elles sont identiques ; alias pour chacune autre  
D) Applicables seulement à eBGP, pas iBGP  

**Answer:** A  
**Explanation:** Quand vous créer une aggregate route:
```
route-map SUPPRESS permit 10
 match ip address prefix-list HIDE  ← Ces /24s vont être cachés
!
router bgp 65001
 address-family ipv4
  aggregate-address 10.0.0.0 255.0.0.0 suppress-map SUPPRESS
```

- Par défaut : l'aggregate (`10.0.0.0/8`) est annonciée + routes spécificos suppressed
- `suppress-map` : reject DÉFINI EXPLICITEMENT certaines routes spécifiques
- `unsuppress-map` : si vous versement d'avoir la globale suppression (summary-only), ceci sélectivement RE-ENABLES certaines routes

---

### Question 47  
Quel est le "graceful restart" dans BGP et son bénéfice?

A) Stoppez gracefully toutes the BGP sessions avant un redémarrage  
B) Permet aux routeurs voisine de maintenir les routes apprises même si l'élève temporairement perd la session BGP  
C) Filtrer gracefully les routes invalides  
D) Ralentir la convergence intentionnellement  

**Answer:** B  
**Explanation:** **BGP Graceful Restart** (support moderne des Cisco et chaque provider) permet:
1. Quand un routeur redémarre, il signale aux voisinfällt "Je redémarre, s'il vous plaît conserver les routes"
2. Les voisinsa une brève période sans purger la BGP RIB
3. Quand routeur redémarrés revient EN LIGNE, il reestablishes la session BGP immédiatement
4. Pas de black-hole ou de flapping routes

C'est TRÈS précieux dalam les réseaux grandes où un BNG redémarrage peut afforeditar le trafic.

Configuration :
```
router bgp 65001
 bgp graceful-restart restart-time 120
 bgp graceful-restart stalepath-time 300
```

---

### Question 48
Quel est l'avantage principal d'utiliser **offset-list** dans une route-map BGP?

A) Ajouter une valeur constante à la métrica Avant d'annoncer  
B) Incrémenter la métrique de MED par une valeur Spécifique  
C) Modifier la LOCAL_PREFERENCE augmentation/diminution  
D) Décaler les route-map sequence numbers  

**Answer:** B  
**Explanation:** **offset-list** (techniquement pour OSPF/EIGRP avec **set metric** dans route-map pour BGP):

Pour BGP, c'est :
```
route-map MED-ADJUST permit 10
 set metric +50
```

Ceci **ajoute 50 à la MED** des routes matchés. Utile pour :
- Incrementer graduellement le coût pour des routes préférer pas
- Ajoute sophistiqué routeur politiques sans override complet

---

### Question 49
Comment s'assurer qu'une route iBGP reçu d'un neighbor EST INSTALLER dans le RIB (supposé next-hop accessibilité)?

A) Configurer **next-hop-self** sur le neighbor**  
B) **Ensure** le next-hop adresse est reachable via l'IGP  
C) BOTH A et B sont nécessaire  
D) Seulement la synchronization doit être desactivée  

**Answer:** B (principalement), C (pour total solvency)  
**Explanation:** Pour une route iBGP pour être installée :
1. **Le next-hop MUST être accessible** via une route dans la RIB (IGP) - ceci est le principal
2. La route doit passer tous les filtres (pas explicitement denied)
3. L'attribut NEXT_HOP doit être valid

**next-hop-self** est utilisé par un eBGP router quandHAYANAF ses routes à iBGP voisine; il change le next-hop à soi même:
```
router bgp 65001
 neighbor <Internal_IP> next-hop-self ← Outil pour iBGP next-hop issues
```

Mais la racine est toujours **IGP accessibilité du next-hop**.

---

### Question 50
Quel est le maximum nombre de équales mixes chemins que Cisco BGP installe par défaut?

A) 1 (implicable meilleur seulement)  
B) 4  
C) 8  
D) 16  

**Answer:** A (défaut), but the answer expected might be **B** pour les configurations modernes  
**Explanation:** Par défaut, Cisco BGP installe **1 meilleur chemin** (le chemin de "widać best path selection") dans la RIB. Cependant:

```
router bgp 65001
 address-family ipv4
  maximum-paths 4  ← ECLMP - installazione jusqu'à 4 égales routes
```

Avec **ECMP** (equal-cost multipathe) configuré, le routeur peut installer upright à 4 (or 8, ou 16 sombres dépendant routeur) routes avec en égalité métrique.

Rappel: BGP par défaut doesn't install unqual-cost chemins comme EIGRP (avec variance). Chaque chemin doit avoir une métrique identique.

---

## ANSWER KEY SUMMARY

| Q# | Answer | Q# | Answer | Q# | Answer | Q# | Answer |
|----|--------|----|----|----|----|----|----|
| 1 | B | 14 | A | 27 | A | 40 | B |
| 2 | C | 15 | A | 28 | B | 41 | B |
| 3 | D | 16 | B | 29 | A | 42 | D |
| 4 | A | 17 | A | 30 | B | 43 | B |
| 5 | B | 18 | A | 31 | B | 44 | A |
| 6 | B | 19 | B | 32 | A | 45 | B |
| 7 | B | 20 | B | 33 | C | 46 | A |
| 8 | B | 21 | B | 34 | A | 47 | B |
| 9 | B | 22 | A | 35 | A | 48 | B |
| 10 | B | 23 | C | 36 | B | 49 | B |
| 11 | B | 24 | B | 37 | A | 50 | A/B |
| 12 | B | 25 | B | 38 | C | | |
| 13 | B | 26 | B | 39 | B | | |

---

## Scoring Guide

- **90-100% (45-50 correct):** BGP mastery - Ready for production deploiement
- **80-89% (40-44 correct):** Strong understanding - A few gaps à révision
- **70-79% (35-39 correct):** Passing - Meets minimum requirements
- **Below 70%:** Needs further study - Focus sur weak areas (Multihoming, Route Maps)

**Exam Completed** - Proceed to Multicast & QoS checkpoint.
