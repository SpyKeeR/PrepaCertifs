# QCM Module 8 : OSPF

## Questions

### Question 1
**Enoncé** : Un routeur OSPF n'a pas de loopback configurée et ses interfaces physiques ont IPs : 192.168.1.1, 10.0.0.1, 172.16.0.1. Quel sera le RID choisi ?

A) 192.168.1.1  
B) 10.0.0.1  
C) 172.16.0.1  
D) 0.0.0.0 (pas de RID)

**Réponse** : C) 172.16.0.1

**Explication** : OSPF sélectionne le RID comme l'adresse IP la PLUS ÉLEVÉE parmi les interfaces physiques. 172.16.0.1 > 192.168.1.1 > 10.0.0.1. C'est pourquoi configurer explicitement RID (loopback) est recommandé pour éviter ces sélections inattendues.

---

### Question 2
**Enoncé** : Deux routeurs OSPF tentent de devenir voisins. Le routeur A envoie Hello tous les 10 secondes, et le routeur B envoie Hello tous les 5 secondes. Quel est le résultat ?

A) Adjacency établie, les deux utilisent 10 sec  
B) Adjacency établie, les deux utilisent 5 sec  
C) Voisinage refusé à cause des timers différents  
D) Adjacency établie mais instable

**Réponse** : C) Voisinage refusé à cause des timers différents

**Explication** : Les timers Hello et Dead DOIVENT être identiques entre voisins. OSPF valide ces paramètres dans le paquet Hello. Si divergents, le voisin est rejeté (pas d'adjacency). Les deux routeurs reçoivent les Hellos mais restent en état "Init" (pas de 2-Way).

---

### Question 3
**Enoncé** : Quel est le Dead Interval par défaut pour une interface Ethernet OSPF configurée avec Hello 10 sec ?

A) 10 secondes  
B) 20 secondes  
C) 30 secondes  
D) 40 secondes

**Réponse** : D) 40 secondes

**Explication** : Dead Interval = 4 × Hello Interval par défaut. Si Hello = 10 sec, Dead = 40 sec. C'est le délai avant déclaration voisin inaccessible.

---

### Question 4
**Enoncé** : Trois routeurs sur un segment Ethernet avec priorités : R1=100, R2=50, R3=1. Quel est l'impact si la priorité de R1 est changée à 0 ?

A) R2 devient DR (priorité 50)  
B) R3 prend le rôle (plus haute RID)  
C) R1 reste DR (pas de changement de rôle)  
D) Tous les rôles sont réélus

**Réponse** : C) R1 reste DR (pas de changement de rôle)

**Explication** : Changement **priorité n'affecte pas DR/BDR en cours**. OSPF n'élit que lors de :
- Démarrage du protocole
- Défaillance du DR/BDR
- Wait Timer expiration (rare)

Mettre R1 priorité à 0 après élection ne la change pas (R1 reste DR jusqu'à défaillance).

---

### Question 5
**Enoncé** : Quel état OSPF indique que DR/BDR ont été élus et la sélection master/slave est en cours ?

A) 2-Way  
B) ExStart  
C) Exchange  
D) Loading

**Réponse** : B) ExStart

**Explication** : États OSPF :
- 2-Way : DR/BDR **élus** ICI
- ExStart : Master/Slave élus (routeur RID supérieur = Master)
- Exchange : DD packets échangés
- Loading : LSR/LSU traités

ExStart est où Master/Slave détermine qui envoie les premiers DD packets.

---

### Question 6
**Enoncé** : Une interface Ethernet a le wildcard mask 0.0.0.255 pour la network statement. Quel est le masque CIDR équivalent ?

A) /8  
B) /16  
C) /24  
D) /32

**Réponse** : C) /24

**Explication** : Wildcard 0.0.0.255 match les 3 premiers octets (24 bits). CIDR = /24.
Formule : Host bits (wildcard) = 32 - CIDR
Ici : 8 host bits = 32 - 24 = /24

---

### Question 7
**Enoncé** : Quelle formule OSPF calcule le coût d'une interface Gigabit (1000 Mbps) ?

A) 1000 Mbps / 100M = 10  
B) 100,000,000 / 1,000,000 = 100  
C) 100,000,000 / 1,000,000,000 = 1  
D) 1000 / 100 = 10

**Réponse** : C) 100,000,000 / 1,000,000,000 = 1

**Explication** : Coût OSPF = 100,000,000 / BW(bps)
1 Gbps = 1,000,000,000 bps
Coût = 100,000,000 / 1,000,000,000 = 1 (meilleur lien)

---

### Question 8
**Enoncé** : Type LSA 2 (Network LSA) est généré et flooded par quel routeur ?

A) Router avoir RID le plus élevé  
B) Designated Router (DR)  
C) Area Border Router (ABR)  
D) Tous les routeurs intra-area

**Réponse** : B) Designated Router (DR)

**Explication** : LSA Type 2 est généré **seulement par DR** sur chaque segment multi-accès. Il décrit le réseau et liste tous routeurs attachés (y compris DR/BDR).

---

### Question 9
**Enoncé** : Quel type LSA est flooded **AS-wide** (tous areas sauf NSSA) ?

A) Type 1 (Router)  
B) Type 3 (Network Summary)  
C) Type 5 (AS External)  
D) Type 7 (NSSA External)

**Réponse** : C) Type 5 (AS External)

**Explication** : Type 5 LSA représente routes externes (redistribuées). Elles sont flooded à **tout le domaine OSPF** sauf NSSA areas (où Type 7 utilisé à la place).

---

### Question 10
**Enoncé** : Quelle commande affiche la Link-State Database complète pour Area 0 ?

A) `show ip ospf database area 0`  
B) `show ip ospf database`  
C) `show ip route ospf`  
D) `show ip ospf lsdb area 0`

**Réponse** : B) `show ip ospf database`

**Explication** : `show ip ospf database` affiche la LSDB complète (tous areas du routeur). `show ip ospf database router` montre Type 1 LSAs, `show ip ospf database summary` montre Type 3, etc.

---

### Question 11
**Enoncé** : Une route OSPF dans RIB affiche "O IA 10.0.0.0/24 [110/20]". Qu'est-ce que "IA" signifie ?

A) Internal Area  
B) Inter-Area  
C) Intra-Area  
D) Internal Adjacent

**Réponse** : B) Inter-Area

**Explication** : 
- **O** = Route OSPF
- **IA** = Inter-Area (route apprise d'une autre area via ABR)
- **O** seul = Intra-Area (même area)
- **O E1/E2** = Externe

Inter-Area routes sont générées par ABRs et ont un coût supplémentaire (20 vs 10).

---

### Question 12
**Enoncé** : Comment forcer OSPF à recalculer RID après changement de loopback ?

A) `reload`  
B) `clear ip ospf process`  
C) `restart ospf`  
D) Changement automatique (pas besoin)

**Réponse** : B) `clear ip ospf process`

**Explication** : RID se fixe au démarrage OSPF et **ne change pas dynamiquement**. Après changement loopback, `clear ip ospf process` redémarre le protocole pour relire RID.

---

### Question 13
**Enoncé** : Quel algorithme OSPF utilise pour calculer le chemin le plus court ?

A) Bellman-Ford  
B) Dijkstra (SPF)  
C) DUAL  
D) Vector Distance

**Réponse** : B) Dijkstra (SPF)

**Explication** : OSPF utilise **SPF (Shortest Path First)**, l'algorithme de Dijkstra. Chaque routeur calcule l'arbre les chemins plus courts (SPT) depuis sa LSDB locale. C'est pourquoi chaque routeur converge indépendamment.

---

### Question 14
**Enoncé** : Si une interface OSPF est configurée avec `ip ospf priority 0`, que devient le routeur ?

A) Désactivé OSPF  
B) Jamais élu DR/BDR (passive)  
C) RID utilisé pour élection (passif aussi)  
D) Routeur critique (plus haute priorité)

**Réponse** : B) Jamais élu DR/BDR (passive)

**Explication** : Priority 0 = **l'exclusion de l'élection DR/BDR**. Le routeur reçoit toujours les Hellos et devient voisin mais **ne participe jamais** à l'élection. Utile pour réduire nombre de DRothers.

---

### Question 15
**Enoncé** : Trois routeurs sur point-to-point serial link. Combien d'adjacencies OSPF full se forment ?

A) 0 (pas d'adjacency point-to-point)  
B) 1 (une par link)  
C) 2 (une par direction)  
D) 3 (complète mesh)

**Réponse** : B) 1 (une par link)

**Explication** : Point-to-point serial links (PPP, HDLC) forment seulement **UNE adjacency par interface**. Pas de DR/BDR sur point-to-point. Pas de problème flooding (deux routeurs seulement = deux Hellos).

---

### Question 16
**Enoncé** : Quel type de routeur génère LSA Type 3 (Network Summary) pour le résumé inter-area ?

A) Internal Router  
B) Area Border Router (ABR)  
C) AS Boundary Router (ASBR)  
D) Virtual Link Router

**Réponse** : B) Area Border Router (ABR)

**Explication** : ABR genère **Type 3 LSAs** pour résumer les routes intra-area d'une area vers d'autres areas. Ceci permet à OSP de scaler (LSDB locals plus petite par area).

---

### Question 17 (Avancée)
**Enoncé** : Un routeur OSPF recalcule SPF après une LSA reçue. Quel est le gain majeur de SPF vs distance vector protocols ?

A) SPT optimisé par Interface  
B) Loop-free garantie (pas de routing loops)  
C) Plus d'adjacencies  
D) Utilisation moins de mémoire

**Réponse** : B) Loop-free garantie (pas de routing loops)

**Explication** : SPF avec topologie complète garantit qu'il n'y a **jamais de boucles de routage** (contrairement RIPv2 qui peut avoir loops transitoires, comptage à l'infini). C'est un avantage majeur des link-state protocols.

---

### Question 18 (Avancée)
**Enoncé** : Deux ABRs connectent Area 1 vers Area 0. Quel est le route intra-area path en provenance Area 1 vers Area 0 ?

A) Via le ABR avec coût le plus bas  
B) Equal-cost multipath sur les deux ABRs  
C) Via le ABR avec RID plus élevé  
D) Via un seul ABR (pas ECMP inter-area)

**Réponse** : A) Via le ABR avec coût le plus bas

**Explication** : OSPF sélectionne routes based sur coût SPF. Si deux ABRs offrent routes différentes vers Area 1, OSPF choisit celui avec coût inférieur. ECMP possible si coûts identiques.

---

### Question 19 (Avancée)
**Enoncé** : Configuration OSPF network statement : `network 0.0.0.0 255.255.255.255 area 0`. Quel impact ?

A) Activé OSPF sur aucune interface  
B) Activé OSPF sur TOUTES les interfaces  
C) Only loopbacks  
D) Erreur de configuration

**Réponse** : B) Activé OSPF sur TOUTES les interfaces

**Explication** : Wildcard 255.255.255.255 match **toutes les adresses IP**. Ceci place chaque interface IP du routeur en Area 0. Problématique pour multi-area (généralement utiliser network statements précis).

---

### Question 20 (Avancée)
**Enoncé** : Une route OSPF affiche "O E1 172.16.0.0/16 [110/30]" et une autre "O E2 172.16.0.0/16 [110/5]". Laquelle sera installée dans RIB ?

A) E1 (coût plus haut = plus fiable)  
B) E2 (coût plus bas)  
C) Les deux ECMP  
D) Ni l'une ni l'autre (ambiguïté)

**Réponse** : B) E2 (coût plus bas)

**Explication** : E1 et E2 sont des routes externes différentes. OSPF préfère **E2 si coût inférieur E2**. E1 vs E2 priorité : E1 < E2 en métrique. Ici E2 [110/5] < E1 [110/30] → E2 gagne.

---

### Question 21 (Avancée)
**Enoncé** : Configuré OSPF avec `default-information originate always metric 50`. Quel type LSA injecte la route par défaut ?

A) Type 1 (Router LSA)  
B) Type 3 (Network Summary)  
C) Type 5 (AS External)  
D) Type 7 (NSSA External)

**Réponse** : C) Type 5 (AS External)

**Explication** : `default-information originate` génère LSA Type 5 (AS externe) pour la route 0.0.0.0/0 depuis ce routeur (ASBR implicit). Type 5 est flooded à tout le domaine.

---

### Question 22 (Avancée)
**Enoncé** : OSPF voisin stuck en estado "Exchange". Quel est le problème probable ?

A) RID identiques (impossible)  
B) Timers Hello/Dead mismatch  
C) List State Request (LSR) timeout - base non-sync  
D) Priority mismatch DR/BDR

**Réponse** : C) List State Request (LSR) timeout - base non-sync

**Explication** : Exchange state signifie DB Description (DD) échange en cours. Si voisin reste stuck ici, c'est généralement parce que **LSRs ne sont pas reçues/répondues** (problèmes réseau, config MSS, ACLs). Non-synchronisation LSDB = stuck en Exchange/Loading.

---

### Question 23 (Avancée)
**Enoncé** : OSPF Type 1 LSA (Router LSA) est généré par quel routeur et flooded où ?

A) Seulement DR, flooded area  
B) Chaque routeur, flooded area (intra-area)  
C) ABR seulement, flooded AS-wide  
D) ASBR seulement, flooded AS-wide

**Réponse** : B) Chaque routeur, flooded area (intra-area)

**Explication** : Type 1 LSA est généré **par CHAQUE routeur** pour décrire ses liens et coûts. Flooded **intra-area seulement** (Type 3 utilisé inter-area pour résumé).

---

### Question 24 (Avancée)
**Enoncé** : ABR reçoit intra-area routes de Area 1 et les annonce vers Area 0 via "O IA" par quel mécanisme ?

A) Redistribution de routes  
B) Génération de Type 3 LSA (Network Summary)  
C) Changement route type de "O" à "O IA"  
D) Flooding intra-area LSA vers Area 0

**Réponse** : B) Génération de Type 3 LSA (Network Summary)

**Explication** : ABR genère **Type 3 LSA** pour résumer chaque route intra-area vers les autres areas. Ceci permet à Area 0 (et autres areas) de connaître les réseaux Area 1 sans avoir la LSDB Area 1 complète (scalabilité).

---

### Question 25 (Avancée)
**Enoncé** : OSPF route install dans RIB utilise quelle source administrative distance ?

A) AD 50  
B) AD 90  
C) AD 110  
D) AD 170

**Réponse** : C) AD 110

**Explication** : OSPF AD par défaut = 110. C'est moins fiable qu'EIGRP (90) mais plus que RIP (120). Routes statiques peuvent obtenir AD 111+ pour servir de backup à OSPF.

---

## Résumé des Réponses

| Q | Rép | Q | Rép |
|---|-----|---|-----|
| 1 | C | 13 | B |
| 2 | C | 14 | B |
| 3 | D | 15 | B |
| 4 | C | 16 | B |
| 5 | B | 17 | B |
| 6 | C | 18 | A |
| 7 | C | 19 | B |
| 8 | B | 20 | B |
| 9 | C | 21 | C |
| 10 | B | 22 | C |
| 11 | B | 23 | B |
| 12 | B | 24 | B |

---
**Durée estimée** : 60-75 minutes  
**Difficulté** : Basique (Q1-12), Intermédiaire (Q13-18), Avancée (Q19-25)
