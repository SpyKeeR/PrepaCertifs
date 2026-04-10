# Checkpoint Exam: OSPF & OSPFv3
## Modules 8-10: OSPF Fundamentals, Advanced OSPF, & OSPFv3

**Exam Code:** ENCOR-CHK-08-10  
**Duration:** 120 minutes  
**Total Questions:** 50  
**Passing Score:** 70% (35/50)  
**Topics Covered:** OSPF Basics, Areas, LSAs, ABRs, OSPF Optimization, OSPFv3, IPv6 Routing

---

## SECTION 1: OSPF FUNDAMENTALS (Questions 1-18)

### Question 1
Quel est le rôle principal de la Link-State Database (LSDB) dans OSPF?

A) Stocker les meilleures routes vers toutes les destinations  
B) Contenir une carte complète de la topologie du réseau  
C) Gérer les adjacencies entre routeurs voisins  
D) Calculer les distances administratives  

**Answer:** B  
**Explanation:** La Link-State Database (LSDB) contient une représentation identique de la topologie complète pour tous les routeurs dans la même OSPF area. Elle contient les Link-State Advertisements (LSAs) reçus de chaque routeur. Tous les routeurs dans une area OSPF maintiennent une copie identique de la LSDB, ce qui permet au SPF (Shortest Path First) algorithm de calculer indépendamment les meilleures routes.

---

### Question 2
Quel est le protocole de routage sur lequel OSPF est basé?

A) Bellman-Ford Algorithm  
B) Diffusing Update Algorithm (DUAL)  
C) Shortest Path First (SPF) Algorithm - Dijkstra  
D) Path Vector Algorithm  

**Answer:** C  
**Explanation:** OSPF utilise l'algorithme Shortest Path First (SPF), également connu sous le nom d'algorithme de Dijkstra. Chaque routeur exécute indépendamment le calcul SPF sur sa copie locale de la LSDB pour déterminer le meilleur (plus court) chemin vers chaque destination. Cela rend OSPF un protocole link-state robuste.

---

### Question 3
Quel est l'administrative distance (AD) par défaut pour OSPF?

A) 5  
B) 90  
C) 110  
D) 120  

**Answer:** C  
**Explanation:** L'administrative distance par défaut pour OSPF est 110. Les routes OSPF sont moins préférées que les routes EIGRP (90) mais plus préférées que les routes RIPv2 (120). Cette hiérarchie AD reflète la fiabilité générale et la performance de chaque protocole.

---

### Question 4
Quel multicast address OSPF utilise-t-il pour envoyer les Hello packets?

A) 224.0.0.5  
B) 224.0.0.6  
C) 224.0.0.10  
D) 224.0.0.9  

**Answer:** A  
**Explanation:** OSPF utilise 224.0.0.5 (All OSPF Routers) pour transmettre les Hello packets et les mises à jour de topologie générales. L'adresse 224.0.0.6 (All OSPF DR Routers) est utilisée par les non-DR/BDR pour envoyer les updates uniquement aux DR et BDR. EIGRP utilise 224.0.0.10 et RIPv2 utilise 224.0.0.9.

---

### Question 5
Quel est le processus par lequel deux routeurs OSPF deviennent "neighbors"?

A) Échange automatique de mises à jour de routage  
B) Échange et synchronisation de Hello packets  
C) Configuration statique sur les deux routeurs  
D) Découverte dynamique via CDP (Cisco Discovery Protocol)  

**Answer:** B  
**Explanation:** Le processus de découverte de voisins OSPF commence par l'échange de Hello packets sur l'interface multicast 224.0.0.5. Si les deux routeurs partagent les mêmes paramètres clés (area ID, timers, etc.), ils peuvent devenir neighbors et entrer dans le processus d'établissement d'adjacency pour échanger des LSAs.

---

### Question 6
Quel paramètre Hello n'est PAS requis pour correspondre entre deux routeurs OSPF pour former une adjacency?

A) Area ID  
B) Hello Interval  
C) Dead Interval  
D) Interface Speed (Bandwidth)  

**Answer:** D  
**Explanation:** Les paramètres qui DOIVENT correspondre pour une adjacency OSPF :
- RIDs doivent être uniques
- Area IDs doivent être identiques
- Hello/Dead timers doivent être identiques
- MTU doivent être identiques
- Authentication (si configurée) doivent correspondre

La vitesse de l'interface (bandwidth) ne doit PAS nécessairement correspondre ; seule la connectivité est nécessaire.

---

### Question 7
Quel est le rôle du Router ID (RID) dans OSPF?

A) Identifier l'interface par laquelle OSPF envoie les paquets  
B) Identifier la priorité du routeur pour DR election  
C) Identifier globalement ce routeur dans le domaine OSPF  
D) Définir la métrique par défaut pour les interfaces du routeur  

**Answer:** C  
**Explanation:** Le Router ID (RID) est une adresse IPv4 32-bit qui identifie globalement un routeur dans le domaine OSPF. Le RID est choisi selon cet ordre:
1. RID statiquement configuré avec **router-id**
2. Adresse IPv4 la plus élevée des interfaces Loopback
3. Adresse IPv4 la plus élevée des interfaces physiques actives

Une fois le RID établi, le changer nécessite un redémarrage du processus OSPF.

---

### Question 8
Quel est l'intervalle par défaut entre les Hello packets OSPF?

A) 1 seconde  
B) 5 secondes  
C) 10 secondes  
D) 30 secondes  

**Answer:** C  
**Explanation:** L'intervalle par défaut pour les Hello packets OSPF est 10 secondes sur les interfaces de type broadcast et point-to-point. Le Dead Interval (hold time) par défaut est 40 secondes (4 × hello). Sur les interfaces non-broadcast (Frame Relay, ATM), les timers sont 30 et 120 secondes respectivement.

---

### Question 9
Qu'est-ce qu'une Designated Router (DR) dans OSPF?

A) Un routeur avec la plus haute priorité  
B) Un routeur choisi pour représenter un segment multi-access et réduire les adjacencies  
C) Un routeur qui connecte deux OSPF areas  
D) Un routeur qui redistribue les routes externes  

**Answer:** B  
**Explanation:** La Designated Router (DR) est élue sur tous les segments multi-access (comme l'Ethernet). Son rôle est de réduire le "flooding" de LSAs. Au lieu que chaque routeur envoie des mises à jour à tous les autres (N² adjacencies), chaque routeur forme une adjacency avec le DR et apprend les mises à jour via le DR. Cela réduit drastiquement le trafic de contrôle.

---

### Question 10
Combien d'adjacencies OSPF se forment sur un segment Ethernet avec 4 routeurs sans DR?

A) 4  
B) 6  
C) 8  
D) 12  

**Answer:** B  
**Explanation:** Sans DR/BDR, chaque routeur doit former une adjacency avec tous les autres routeurs sur le segment. Avec 4 routeurs, le nombre d'adjacencies est C(4,2) = 4!/(2!×2!) = 6 adjacencies. Avec un DR, les 4 routeurs forment 3 adjacencies avec le DR (réduisant le flooding) et chaque routeur maintient une relation de "2-way" (non-adjacent) avec les autres non-DR routeurs.

---

### Question 11
Quel est le critère principal pour l'élection du DR/BDR dans OSPF?

A) La plus ancienne configuration  
B) La plus basse adresse IP d'interface  
C) La plus haute priorité configurée, puis la plus haute RID  
D) La plus basse métrique  

**Answer:** C  
**Explanation:** La Designated Router est élue selon:
1. **Priorité d'interface OSPF** - plus haute gagne (par défaut 1, plage 0-255; 0 = ne peut pas être DR)
2. Si égalité, **Router ID (RID)** le plus élevé devient DR
3. Le **second** RID le plus élevé devient BDR

La priorité peut être configurée avec : **ip ospf priority <value>**

---

### Question 12
Quel est l'avantage principal des Loopback Interfaces pour la stabilité OSPF?

A) Augmenter la bande passante utilisée  
B) Fournir un RID stable qui n'est jamais défaillant  
C) Réduire le nombres de LSAs enviées  
D) Augmenter la distance administrative  

**Answer:** B  
**Explanation:** Les interfaces Loopback:
- Fournissent une Loopback address (généralement 127.0.1 à 127.255.255) stable
- Ne devumt JAMAIS être défaillantes (sauf matériel complet)
- Sont utilisées comme source RID stable
- Aident à la stabilité puisque le RID ne change jamais, évitant les recalculations SPF

Il est recommandé de configurer chaque routeur avec une loopback interface pour OSPF.

---

### Question 13
Quel est le maximum de "hops" ou transitions dans OSPF?

A) Illimité  
B) 15  
C) 256  
D) Aucune limite théorique  

**Answer:** A  
**Explanation:** OSPF n'a pas de limite théorique en nombre de hops. C'est un énorme avantage par rapport à RIPv2. La seule limite est le coût cumulatif et le traitement SPF overhead sur un domaine excessivement grand.

---

### Question 14
Quel type d'interface OSPF est utilisé pour une connexion PPP point-to-point?

A) Broadcast  
B) Point-to-Point  
C) Non-Broadcast Multi-Access (NBMA)  
D) Point-to-Multipoint  

**Answer:** B  
**Explanation:** Les interfaces point-to-point (comme PPP, HDLC serial direct, some Ethernet emulés) n'élisent pas de DR/BDR et forment une adjacency directe. OSPF détecte automatiquement le type, mais peut être forcé avec : **ip ospf network point-to-point**

Types d'interface OSPF:
- **Broadcast**: Ethernet, Fast Ethernet - élit DR/BDR
- **Point-to-Point**: PPP, HDLC, Serial Direct - pas de DR/BDR
- **NBMA**: Frame Relay, ATM - peut configurer statiquement les voisins

---

### Question 15
Quel LSA type est utilisé par un routeur pour annoncer ses liens directement connectés?

A) Type 1 - Router LSA  
B) Type 2 - Network LSA  
C) Type 3 - Summary LSA  
D) Type 4 - ASBR Summary LSA  

**Answer:** A  
**Explanation:** **Type 1 LSAs (Router LSAs)** sont générés par chaque routeur OSPF et annoncent:
- L'adresse du routeur (RID)
- Tous les liens (interfaces) directement connectés au routeur
- La métrique (coût) de chaque interface

Les Type 1 LSAs ne sont pas inondés en dehors de l'area où le routeur est actif. C'est pourquoi les topologies internes d'une area sont masquées aux autres areas.

---

### Question 16
Quel est le coût OSPF par défaut pour une interface Gigabit Ethernet?

A) 1  
B) 10  
C) 100  
D) 1  

**Answer:** A  
**Explanation:** Avec la formule OSPF par défaut:
**Cost = Reference Bandwidth / Interface Bandwidth**

Avec Reference Bandwidth par défaut = 100 Mbps:
- FastEthernet (100 Mbps): 100/100 = 1
- Gigabit (1000 Mbps): 100/1000 = 0.099 ≈ arrondi à 1
- Serial (1.544 Mbps): 100/1.544 ≈ 65

**Important**: Sur les réseaux modernes avec du 10G, il faut changer la reference bandwidth avec:
**auto-cost reference-bandwidth 1000000** (en Mbps, donc pour 1 Tbps)

---

### Question 17
Quel est l'intervalle par défaut pour la réflexion des LSDB dans OSPF?

A) 30 secondes  
B) 300 secondes  
C) 1800 secondes (30 minutes)  
D) 3600 secondes (60 minutes)  

**Answer:** C  
**Explanation:** Chaque LSA inclut un **Age** qui incrémente de 1 par seconde. Quand l'age atteint 1800 secondes (30 minutes), le routeur qui a originé le LSA envoie une nouvelle copie de ce LSA avec l'age réinitialisé à 0. Si un LSA n'est pas mis à jour et atteint 3600 secondes, il est marqué comme invalide et retiré de la LSDB.

---

### Question 18
Quel est le rôle des "Passive Interfaces" dans OSPF?

A) Arrêter OSPF sur cette interface complètement  
B) Inclure le réseau dans la LSDB mais ne pas former d'adjacencies  
C) Réduire la métrique de l'interface  
D) Bloquer tous les Hello packets  

**Answer:** B  
**Explanation:** Une interface passive dans OSPF:
- **INCLUT** le réseau connecté à cette interface dans la LSDB (Type 1 LSA)
- **N'envoie pas** de Hello packets
- **Ne forme pas** d'adjacencies
- **N'accepte pas** les paquets OSPF

C'est utile pour les interfaces avec des clients ou du personnel (p.ex., segments clients en DMZ) où OSPF n'est pas nécessaire mais le réseau doit être propagé.

---

## SECTION 2: OSPF AREAS & ABRs (Questions 19-32)

### Question 19
Quel est le rôle spécial de l'Area 0 dans OSPF?

A) C'est un stub area qui ne reçoit pas les routes externes  
B) C'est le "backbone" - auquel tous les autres areas doivent se connecter  
C) C'est réservée à la configuration de sécurité  
D) C'est l'area par défaut pour tous les routeurs  

**Answer:** B  
**Explanation:** Area 0 est le **backbone OSPF**. C'est une area spéciale:
- Tous les autres areas DOIVENT se connecter à Area 0
- Les routes inter-area DOIVENT passer par Area 0
- Si une topologie n'a pas Area 0, les areas ne peuvent pas communiquer directement

Configuration: **network 10.0.1.0 0.0.0.255 area 0**

---

### Question 20
Qu'est-ce qu'une ABR (Area Border Router)?

A) Un routeur qui connecte plusieurs areas et participe à Area 0  
B) Un routeur qui redistribue les routes externes  
C) Un routeur qui élit le DR d'une area  
D) Un routeur qui filtre les routes entre areas  

**Answer:** A  
**Explanation:** Un **Area Border Router (ABR)** est un routeur connecté à PLUSIEURS OSPF areas, notamment l'Area 0 (backbone). L'ABR:
- Maintient une LSDB séparée pour CHAQUE area
- Exécute SPF séparément pour chaque area
- Annonce (avec Type 3 LSAs) les routes apprises d'une area aux autres areas
- Reçoit et inonde les Type 1 LSAs que localement (au sein de chaque area)

---

### Question 21
Quel est le type de LSA utilisé pour annoncer les routes d'autres areas?

A) Type 1 - Router LSA  
B) Type 2 - Network LSA  
C) Type 3 - Summary LSA  
D) Type 4 - ASBR Summary LSA  

**Answer:** C  
**Explanation:** **Type 3 LSAs (Summary LSAs ou Interarea Routes)** sont générés par les ABRs pour:
- Annoncer les réseaux apprises d'une area aux autres areas
- UNIQUEMENT les meilleur route (résumé) vers chaque destination est annoncée
- Réduire dramatiquement le nombre d'annonces inter-area

Format typique dans la table de routage: **O IA** (OSPF Inter-Area)

---

### Question 22
Quel est l'avantage principal de diviser un grand domaine OSPF en multiples areas?

A) Augmenter la bande passante  
B) Réduire la taille de la LSDB et le overhead SPF  
C) Améliorer la sécurité du routeur  
D) Augmenter le nombre de voisins  

**Answer:** B  
**Explanation:** En divisant en multiples areas:
- Chaque routeur ne maintient qu'une **partielle LSDB** (juste sa propre area + Area 0)
- Les changements de topologie dans une area ne déclenchent PAS les recalculs SPF dans les autres areas
- Le trafic de flooding LSA est limité au sein de chaque area
- Le réseau **scalabilité-énorme améliore**

C'est l'une des forces clés de OSPF sur les grands réseaux.

---

### Question 23
Comment les routes intra-area sont-elles représentées dans la table de routage OSPF?

A) O  
B) O IA  
C) O E1  
D) O E2  

**Answer:** A  
**Explanation:** Les routes intra-area (routes au sein de la même area) sont indiquées par un simple **"O"** dans la table de routage. Les routes inter-area sont indiquées par **"O IA"**. Les routes externes sont **"O E1"** (Type 1 external) ou **"O E2"** (Type 2 external).

---

### Question 24
Quel est le type de LSA utilisé pour annoncer l'existence d'un ASBR (AS Boundary Router)?

A) Type 3 - Summary LSA  
B) Type 4 - ASBR Summary LSA  
C) Type 5 - AS External LSA  
D) Type 7 - NSSA External LSA  

**Answer:** B  
**Explanation:** **Type 4 LSAs (ASBR Summary LSAs)** sont générés par les ABRs pour:
- Annoncer l'existence et l'accessibilité d'un ASBR (routeur qui redistribue le trafic externe)
- Fournir un chemin vers cet ASBR

Type 4 LSAs permettent aux routeurs dans les non-border areas d'atteindre les routes externes publicadas par l'ASBR via le Type 5 LSA.

---

### Question 25
Quel est le type d'area utilisé pour réduire la publicité des routes externes dans OSPF?

A) Transit Area  
B) Stub Area  
C) Totally Stubby Area  
D) Not-So-Stubby Area (NSSA)  

**Answer:** B - ou C  
**Explanation:**
- **Stub Area**: blocque Type 5 LSAs (AS External) mais reçoit toujours une défaut route vers ASBR via Type 4 LSA
- **Totally Stubby Area**: bloque Type 5 AND Type 4 LSAs. Seules les routes intra-area + une défaut route
- **NSSA**: bloque Type 5 LSAs mais permet les routes externes via Type 7 LSAs convertis en Type 5

Idéal pour les spokes distant qui n'ont pas besoin de connaître tous les ASBRs.

---

### Question 26
Quel est l'avantage de la Route Summarization sur un ABR dans OSPF?

A) Augmenter la métrique des routes  
B) Réduire le nombre de Type 3 LSAs annoncés  
C) Réduire la priorité du routeur  
D) Bloquer les querys de voisins  

**Answer:** B  
**Explanation:** La Route Summarization sur un ABR consolide multiples routes spécifiques en une seule route résumée (par ex., au lieu d'annoncer /24s individuels, annoncer un /16). Cela:
- Réduit le nombre de Type 3 LSAs
- Réduit la taille de la LSDB des autres areas
- Accélère la convergence
- Réduit le trafic de mise à jour

Configuré avec : **area <area-id> range <network> <mask>**

---

### Question 27
Quel est le type d'area utilisé dans les réseaux VPN multi-client où chaque client a besoin de routes externes?

A) Stub Area  
B) Stub Area with external routes redistributed  
C) Virtual Link Area  
D) NSSA (Not-So-Stubby Area)  

**Answer:** D  
**Explanation:** Une **NSSA (Not-So-Stubby Area)** permet:
- DE bloquer Type 5 LSAs (comme un Stub Area)
- DE PERMETTRE les routes externes via Type 7 LSAs (local redistributed routes)
- L'ABR convertit les Type 7 LSAs converties en Type 5 LSAs pour les otras areas

Idéal pour les réseaux où des routeurs redistribuent des routes externes locale dans une area mais ne veulent pas recevoir routes d'autres ASBRs.

---

### Question 28
Quel est le coût OSPF par défaut d'une interface Serial T1 (1.544 Mbps)?

A) 1  
B) 48  
C) 64  
D) 65  

**Answer:** D  
**Explanation:** Utilisant la formule OSPF par défaut:
**Cost = Reference Bandwidth / Interface Bandwidth = 100 Mbps / 1.544 Mbps ≈ 64.8 ≈ 65**

C'est un coût significativement plus élevé que Ethernet, ce qui est correct puisque T1 est beaucoup plus lent. C'est pourquoi il est important de manuellement configurer la reference bandwidth sur les réseaux modernes avec des liens très rapides (10G+).

---

### Question 29
Quelle commande configure statiquement le Router ID dans OSPF?

A) **ospf router-id <RID>**  
B) **router-id <RID>** (sous le processus OSPF)  
C) **ospf rif <RID>**  
D) **set ospf router-id <RID>**  

**Answer:** B  
**Explanation:** La commande correcte est:
```
router ospf <process-id>
  router-id <32-bit-address>
```

Par exemple:
```
router ospf 1
  router-id 192.168.0.1
```

Après configuration, le processus OSPF doit être réinitialisé avec : **clear ip ospf process** pour appliquer le nouveu RID.

---

### Question 30
Quel est le rôle d'une Virtual Link dans OSPF?

A) Connecter virtuellement deux routeurs à travers une WAN  
B) Connecter une discontiguous area à l'Area 0 par un chemin virtuel  
C) Configurer une interface virtuelle pour les tests  
D) Créer une redondance pour le DR/BDR  

**Answer:** B  
**Explanation:** Une **Virtual Link** dans OSPF est entièrement virtuelle et permet:
- Une area non-directement connectée à Area 0 de se connecter via une area transitoire
- Utile en cas d'erreur de conception ou de migration OSPF

Configuré comme:
```
area <transit-area> virtual-link <remote-router-id>
```

Les Virtual Links sont une solution "patch" temporaire ; une bonne conception devrait éviter cette situation.

---

### Question 31
Quel est le maximum administratif de la Recursive Lookup dans OSPF?

A) 1 lookup  
B) 2 lookups  
C) Illimité  
D) Basé sur la bande passante  

**Answer:** C  
**Explanation:** OSPF permet les "recursive lookups" - c'est-à-dire une préfixe qui pointe vers un successor qui à son tour pointe vers un autre successor, et ainsi de suite. Ceci est théoriquement sans limite. En pratique, un bien conçu réseau OSPF minimise la profondeur des lookups.

---

### Question 32
Quel est l'avantage principal du "Summarization" sur un ASBR dans OSPF?

A) Réduire le nombre de Type 1 LSAs  
B) Réduire le nombre de Type 5 LSAs (routes externes)  
C) Réduire la priorité DR  
D) Augmenter la métrique  

**Answer:** B  
**Explanation:** La Route Summarization (agrégation) sur un ASBR réduit le nombre de Type 5 LSAs annoncés au domaine OSPF. Au lieu d'annoncer chaque route externe individuellement (p.ex., depuis BGP), l'ASBR peut résumer des gammes entières de routes externes en un seul Type 5 LSA. Cela réduit significativement le overhead de flooding et la taille de la LSDB.

---

## SECTION 3: OSPF ADVANCED & OSPFv3 (Questions 33-50)

### Question 33
Quel type de LSA est utilisé par un ASBR pour annoncer les routes redistributées (externes)?

A) Type 3 - Summary  
B) Type 4 - ASBR Summary  
C) Type 5 - AS External  
D) Type 6 - OSPF External Group Member  

**Answer:** C  
**Explanation:** **Type 5 LSAs (AS External LSAs)** sont générés par les ASBRs pour annoncer les routes redistributées (par exemple, depuis BGP, static routes, ou autres IGPs). Type 5 LSAs:
- Sont inondés à travers TOUS les areas (sauf Stub/Totally Stubby)
- Identifient le coût et le type externe (E1 ou E2)
- Permettent à tous les routeurs du domaine OSPF de connaître les routes externes

---

### Question 34
Quel est la différence entre un Type 1 et Type 2 cost externe dans OSPF?

A) Type 1 inclut le coût OSPF interne ; Type 2 ne l'inclut pas  
B) Type 1 est pour BGP ; Type 2 est pour RIP  
C) Type 1 expire après 30 secondes ; Type 2 est permanent  
D) Type 1 bloque les voisins ; Type 2 les accepte  

**Answer:** A  
**Explanation:** 
- **E1 (External Type 1)**: La métrique totale = coût externe + coût OSPF interne pour atteindre l'ASBR. Préféré si différents ASBRs annoncent  la même route externe.
- **E2 (External Type 2) - Défaut**: La métrique = coût externe UNIQUEMENT. Si deux ASBRs annoncent la même route avec différents coûts E2, celui avec le coût E2 le plus bas est préféré.

Dans le tableau de routage: **O E1** ou **O E2**

---

### Question 35
Quel est le timeout par défaut de l'adj-side dans OSPF?

A) 30 secondes  
B) 40 secondes  
C) 120 secondes  
D) 180 secondes  

**Answer:** B  
**Explanation:** Le **Dead Interval** (ou Hold Time) par défaut dans OSPF est 40 secondes sur la plupart des interfaces broadcast/point-to-point. C'est égal à 4 × Hello Interval (10 sec × 4 = 40 sec). Si un routeur ne reçoit pas de paquet OSPF (Hello, Update, etc.) d'un voisin avant 40 secondes, ce voisin est déclaré DOWN.

Sur les interfaces NBMA (Frame Relay), le défaut est 120 secondes (30 × 4).

---

### Question 36
Quel paramètre est utilisé pour "slow down" la convergence OSPF en cas de oscillations de liens?

A) **hello-interval**  
B) **dead-interval**  
C) **spf-hold-time**  
D) **spf-start-interval**  

**Answer:** C ou D  
**Explanation:** Les paramètres SPF timer dans OSPF contôlent la rythme de calcul SPF:
- **spf-start-interval <milliseconds>**: Le délai avant le premier SPF après un changement (défaut 0)
- **spf-hold-interval <milliseconds>**: Le délai minimum entre les SPF consecutifs (défaut 200 ms)
- **spf-max-interval <milliseconds>**: Le délai maximum entre les SPF (défaut 5 sec)

Ces timers empêchent OSPF de recalculer incessamment si un lien "flaps" rapidement.

---

### Question 37
Qu'est-ce qu'OSPFv3?

A) Une version plus ancienne de OSPF  
B) OSPF avec support IPv6 et IPv4  
C) Un remplacemeent complètement de OSPF pour IPv4  
D) Une extension de OSPF pour les Mult-area routing uniquement  

**Answer:** B  
**Explanation:** **OSPFv3** est la version 3 d'OSPF qui:
- Supporte **IPv6 natively** (et optionellement IPv4 via Address Family)
- Utilise les **link-local addresses** pour les adjacencies routeur-à-routeur
- Supprime l'authentification du protocole (maintenant véhiculée via IPsec)
- Utilise les mêmes **5 packet types** que OSPFv2 (Hello, DBD, LSR, LSU, LSAck)
- Introduit de nouveaux **LSA types** pour IPv6 prefixes

---

### Question 38
Quel est le protocole IP utilisé par OSPFv3?

A) IP 89 (comme OSPF v2)  
B) IP 88  
C) IP 41  
D) IPv6 Extension Header Type 89  

**Answer:** A  
**Explanation:** OSPFv3 utilise le même **protocole IP 89** que OSPFv2. La différence est que:
- OSPFv2 s'exécute **sur IPv4** (groupe multicast 224.0.0.5/6)
- OSPFv3 s'exécute **nativement sur IPv6** (groupe multicast FF02::5/6)

Mais dans les deux cas, le numéro de protocole IP est 89.

---

### Question 39
Quel est l'adresse multicast utilisée par OSPFv3 pour envoyer les Hello?

A) FF02::5  
B) FF02::6  
C) 224.0.0.5  
D) 224.0.0.6  

**Answer:** A  
**Explanation:** En IPv6, OSPFv3 utilise:
- **FF02::5** (All SPFRouters) - pour les Hellos et mises à jour régulés
- **FF02::6** (All DR) - pour les updates envoyées au DR/BDR uniquement

Comparé à OSPFv2 avec 224.0.0.5 et 224.0.0.6 en IPv4.

---

### Question 40
Quel est le rôle de "link-local address" dans OSPFv3?

A) C'est une adresse IPv6 globale  
B) C'est utilisée pour les adjacencies routeur-à-routeur sur un lien donné  
C) C'est optionnel dans OSPFv3  
D) C'est utilisée pour la redistribution externe uniquement  

**Answer:** B  
**Explanation:** Dans OSPFv3, les **link-local addresses** (fe80::/10 scope):
- Sont REQUISES sur chaque interface OSPFv3
- Sont utilisées comme source pour les paquets OSPF Hello/Update
- Permettent les adjacencies même si les interfaces n'ont pas d'adresse globale
- Assurent que les voisins OSPF sont toujours accessibles au niveau lien

Chaque interface doit avoir automatiquement ou manuellement une link-local address.

---

### Question 41
Comment on configure OSPFv3 sur une interface dans Cisco IOS moderne?

A) **ipv6 router ospf <process-id>** (legacy)  
B) **ipv6 ospf <process-id> area <area-id>** (legacy)  
C) **ospfv3 <process-id> ipv6 area <area-id>** (modern)  
D) **router ospfv3 <process-id>**  

**Answer:** C  
**Explanation:** Les commandes modernes pour Cisco IOS XE:

```
interface Gi0/0
  ipv6 address 2001:DB8::1/64
  ospfv3 1 ipv6 area 0
```

Les commandes héritage (legacy) `ipv6 router ospf` et `ipv6 ospf` sont toujours supportées mais Cisco recommande la transition vers `ospfv3 ... ipv6`.

---

### Question 42
Quel est le rôle de "Instance ID" dans OSPFv3?

A) Identifier le processus OSPF sur le routeur  
B) Permettre multiples instances d'OSPFv3 sur la même interface  
C) Identifier les adjacencies avec les voisins  
D) Contrôler la priorité DR/BDR  

**Answer:** B  
**Explanation:** L'**Instance ID** dans OSPFv3 permet:
- Multiples instances **indépendantes** du protocole OSPFv3 sur la même interface
- Chaque instance a sa propre LSDB, RIB, voisinnage
- Utile pour créer des "logically separate" topologies sur un lien physique

Par défaut, Instance ID 0 est utilisée. D'autres instances (1-255) peuvent être configurées.

---

### Question 43
Quel est le support IPv4 dans OSPFv3?

A) OSPFv3 ne supporte que IPv6  
B) OSPFv3 peut être utilisé pour router IPv4 via une address family separée  
C) OSPFv3 est un remplacement de OSPF v2 pour IPv4  
D) OSPFv3 supporte IPv4 identiquement à OSPFv2  

**Answer:** B  
**Explanation:** OSPFv3 supporte BOTH IPv6 **et** IPv4 en utilisant **separate address families**:

```
router ospfv3 1
  address-family ipv6 unicast
    area 0 range 2001:DB8::/32
  !
  address-family ipv4 unicast
    area 0 range 10.0.0.0 255.0.0.0
```

Cela permet une migration progressive d'OSPFv2 à OSPFv3.

---

### Question 44
Quel est le type LSA utilisé par OSPFv3 pour annoncer les IPv6 prefixes intra-area?

A) Type 1 - Router LSA  
B) Type 3 - Summary LSA  
C) Type 8 - Intra-Area Prefix LSA  
D) Type 9 - Link-Local LSA  

**Answer:** C  
**Explanation:** Dans OSPFv3, les LSA types sont différents:
- **Type 1**: Router LSA - même en v2 (pas les prefixes, juste la topologie)
- **Type 8**: Intra-Area Prefix LSA - **NOUVEAU** pour annoncer les IPv6 prefixes
- **Type 9**: Link-Local LSA - **NOUVEAU** pour annoncer les link-local addresses

Cette séparation rend OSPFv3 plus efficace et flexibile.

---

### Question 45
Quel est le rôle de l'adresse IPv6 global unicast dans OSPFv3?

A) Uniquement pour les adjacencies routeur-à-routeur  
B) Annoncée dans les Intra-Area Prefix LSAs pour reachability  
C) Optionnelle; seule la link-local est nécessaire  
D) Utilisée pour l'identification du Router ID uniquement  

**Answer:** B  
**Explanation:** Dans OSPFv3:
- La **link-local address** est utilisée pour les paquets OSPF eux-mêmes et les adjacencies
- La **global unicast address** est annoncée dans les **Type 8 (Intra-Area Prefix) LSAs** pour que les autres routeurs puissent router vers elle
- La **link-local** est necessaire ; la **global** est optionnelle mais typiquement configurée

---

### Question 46
Quel est le numéro de Router ID utilisé automatiquement par OSPFv3 s'il n'est pas manuellement configuré?

A) L'adresse link-local la plus élevée  
B) L'adresse IPv4 loopback la plus élevée  
C) L'adresse IPv6 loopback la plus élevée  
D) Aucun - le RID DOIT être manuellement configuré  

**Answer:** D  
**Explanation:** Contrairement à OSPF v2 qui peut choisir automatiquement un RID depuis n'importe quelle interface IPv4, **OSPFv3 NÉCESSITE** que le Router ID soit **manuellement configuré**. Cela reflète le fait que le RID doit être stable et explicitement contrôlé par l'administrateur.

```
router ospfv3 1
  router-id 192.168.1.1
```

---

### Question 47
Quel est l'avantage du protocole RTP propriétaire utilisé par OSPF par rapport à TCP?

A) TCP brûle trop de bande passante  
B) RTP garantit UNICAST delivery comme TCP, mais sans connexion persistante  
C) RTP n'est pas nécessaire sur les réseaux modernes  
D) TCP crée trop de sessions simultanées  

**Answer:** B  
**Explanation:** OSPF utilise le **Reliable Transport Protocol (RTP)** propriétaire:
- Il garantit la livraison des mises à jour (comme TCP)
- Mais n'établit PAS une session TCP persistante
- Utilise moins de ressources qu'une session TCP complète
- Permet un meilleur contrôle des timers et de la fiabilité spécifique à OSPF

---

### Question 48
Quel est le coût OSPF d'une interface configurée manuellement avec **ip ospf cost 50**?

A) 50  
B) Calculé à partir de reference bandwidth  
C) Défaut 1  
D) Dépend de la bande passante de l'interface  

**Answer:** A  
**Explanation:** Si une interface has une **ip ospf cost** configurée manuellement, cette valeur fixe **remplace complètement** la formule de calcul automatique:

```
interface Gi0/0
  ip ospf cost 50
```

Cette configuration surcharge la formule et utilise directement 50. Ceci peut être utile pour:
- Forcer le trafic vers chemins spécifiques
- Contourner les limitations de calcul de coût
- Implémenter des politiques de routage spéciales

---

### Question 49
Quel est le comportement de OSPF si deux ASBRs annoncent la même route externe avec **metric-type e1** et un a une métrique plus basse?

A) Aucun n'est préféré ; ECMP s'applique  
B) Celle avec la métrique OSPF interne la plus basse vers l'ASBR est préférée  
C) Celle avec la métrique E1 la plus basse (interne + externe) est préférée  
D) Celle announcée en premier chronologiquement est préférée  

**Answer:** C  
**Explanation:** Avec **Type 1 External (E1)**:
- La métrique complète = coût externe + coût OSPF pour atteindre l'ASBR
- Si deux ASBRs annoncent la même route avec E1, celle avec la **métrique E1 totale** la plus basse est préférée
- Ceci encourage le trafic vers le meilleur ASBR au total, pas juste le coût external

Avec **Type 2 External (E2 - défaut)**:
- Seul le coût externe est utilisé, le coût interne est ignoré

---

### Question 50
Quel est l'avantage principal d'utiliser un "loopback interface" avec une /32 subnet comme Router ID dans OSPF?

A) Augmente la stabilité du RID car une interface loopback n'est jamais down  
B) Réduit la bande passante utilisée par OSPF  
C) Augmente le MDT (Maximum Transmission Unit) de l'interface  
D) Permet multiples RIDs  

**Answer:** A  
**Explanation:** Une interface Loopback:
- Est TOUJOURS up (s'il y a de l'énergie au routeur)
- N'est jamais administrativement down (sauf configuration manuelle)
- Fournit un RID stable qui ne change jamais
- Une /32 est isolée et ne dépend d'aucun lien physique

Best practice: configurer chaque routeur avec une loopback (p.ex., 192.168.1.1/32 pour R1, 192.168.2.2/32 pour R2) et utiliser comme RID OSPF.

---

## ANSWER KEY SUMMARY

| Q# | Answer | Q# | Answer | Q# | Answer |
|----|--------|----|----|----|----|
| 1 | B | 18 | B | 35 | B |
| 2 | C | 19 | B | 36 | C |
| 3 | C | 20 | A | 37 | B |
| 4 | A | 21 | C | 38 | A |
| 5 | B | 22 | B | 39 | A |
| 6 | D | 23 | A | 40 | B |
| 7 | C | 24 | B | 41 | C |
| 8 | C | 25 | B | 42 | B |
| 9 | B | 26 | B | 43 | B |
| 10 | B | 27 | D | 44 | C |
| 11 | C | 28 | D | 45 | B |
| 12 | B | 29 | B | 46 | D |
| 13 | A | 30 | B | 47 | B |
| 14 | B | 31 | C | 48 | A |
| 15 | A | 32 | B | 49 | C |
| 16 | A | 33 | C | 50 | A |
| 17 | C | 34 | A | | |

---

## Scoring Guide

- **90-100% (45-50 correct):** Advanced OSPF mastery - Ready for production design
- **80-89% (40-44 correct):** Strong understanding - Some areas need review
- **70-79% (35-39 correct):** Passing - Meets minimum requirements
- **Below 70%:** Needs further study - Focus on weak areas

---

**Exam Completed** - Review weak areas and proceed to next section of ENCOR.
