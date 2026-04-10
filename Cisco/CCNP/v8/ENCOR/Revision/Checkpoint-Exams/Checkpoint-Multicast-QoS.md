# Checkpoint Exam: Multicast & QoS
## Modules 13-14: Multicast Routing & Quality of Service

**Exam Code:** ENCOR-CHK-13-14  
**Duration:** 90 minutes  
**Total Questions:** 50  
**Passing Score:** 70% (35/50)  
**Topics Covered:** Multicast Fundamentals, IGMP, PIM, Rendezvous Points, QoS Models, Classification, Policing, Shaping, Congestion Management

---

## SECTION 1: MULTICAST FUNDAMENTALS (Questions 1-15)

### Question 1
Quel est l'intervalle d'adresses IP réservées pour la communication multicast?

A) 192.168.0.0/16  
B) 224.0.0.0/4  
C) 239.0.0.0/8  
D) 10.0.0.0/8  

**Answer:** B  
**Explanation:** La plage multicast IPv4 est **224.0.0.0 à 239.255.255.255** (classe D). Cette plage commence par les 4 bits `1110` en binaire. Les subdivisions incluent:
- **224.0.0.0/24** : Local network control (non forwardé)
- **224.0.1.0/24** : Internetwork control
- **232.0.0.0/8** : Source Specific Multicast (SSM)
- **233.0.0.0/8** : GLOP
- **239.0.0.0/8** : Administratively scoped

---

### Question 2
Quel est l'avantage principal de la communication multicast comparé au broadcast?

A) Réduit la bande passante au lieu d'envoyer des trafics inutiles aux hôtes non intéressés  
B) Augmente la couverture du réseau  
C) Simplifie la configuration des routeurs  
D) Élimine le besoin de routage dynamique  

**Answer:** A  
**Explanation:** Multicast offre une **efficacité spectaculaire** sur le broadcast:
- Seuls les hôtes INTÉRESSÉS reçoivent le trafic multicast (via IGMP join)
- Le trafic n'est pas répliqué sur les branches qui n'en ont pas besoin
- Exemple : vidéo 10 Mbps au lieu de 50 Mbps (5 destinations) utilise SEULEMENT 10 Mbps sur tous les liens

---

### Question 3
Comment fonctionne le mapping entre une adresse IP multicast et une adresse MAC?

A) L'adresse MAC est identical dérivée de l'adresse IP  
B) Les 23 bits bas de l'adresse IP sont mappés aux 23 bits bas de la MAC, précédés de 01:00:5E  
C) DHCP automatiquement attribue une MAC multicast unique  
D) Les ADMINs configurent manuellement chaque mapping  

**Answer:** B  
**Explanation:** Le mapping multicast IP → MAC :
- **Prefix MAC:** `01:00:5E` (24 bits fixes pour distinguer multicast)
- Le **23e bit bas** de l'adresse IP multicast est mappé directement aux **23 bits bas** de la MAC
- **Exemple :** 224.1.1.1 → 01:00:5e:01:01:01

**Important :** Cela signifie que 32 adresses multicast IP différentes mappent à la **MÊME MAC** (car seuls 23 bits de 24 bits d'adresse IP disponibles sont utilisés). Les switches avec IGMP snooping gèrent cela correctement.

---

### Question 4
Quel protocole utilisent les récepteurs multicast pour notifier les routeurs locaux qu'ils souhaitent recevoir un groupe multicast spécifique?

A) OSPF  
B) IGMP (Internet Group Management Protocol)  
C) PIM (Protocol Independent Multicast)  
D) MSDP  

**Answer:** B  
**Explanation:** **IGMP (Internet Group Management Protocol)** fonctionne entre :
- **Hôts reçepteurs** ↔ **Routeur multicast local**

IGMP permet aux hôtes de dire "Je veux recevoir le groupe 224.1.1.1" (IGMPv2) ou "Je veux recevoir le groupe 224.1.1.1 SEULEMENT de la source 10.1.1.1" (IGMPv3).

Le routeur multicast local CONTRÔLE ALORS via PIM pour que le groupe soit envoyé vers ce lien.

---

### Question 5
Quel est le rôle du "Rendezvous Point" (RP) dans une topologie multicast?

A) Le routeur qui crée le groupe multicast  
B) Le point central où les sources et les récepteurs se rencontrent pour établir le arbre de distribution multicast  
C) Un serveur qui distribue les adresses multicast  
D) Un routeur qui filtre le trafic multicast  

**Answer:** B  
**Explanation:** Le **Rendezvous Point (RP)** dans PIM Sparse Mode :
- Est un routeur **stratégiquement placé** dans la topologie multicast
- Les **sources multicast** envoient d'abord vers le RP
- Les **récepteurs** envoient joins vers le RP
- Le RP coordonne l'établissement de l'**arbre de distribution multicast (MDT)**

Une fois que le chemin source-to-receiver est optimisé, le trafic peut shortcut le RP (Fastest Path).

---

### Question 6
Quel est le fonctionnement du mécanisme "shared tree" dans PIM?

A) Tous les routeurs partagent une table de routage unique  
B) Tous les sources et récepteurs d'un groupe utilisent un arbre común enraciné au RP  
C) Les routeurs distribuent les mises à jour en même temps  
D) Un arbre secondaire est créé pour la backup  

**Answer:** B  
**Explanation:** L'**arbre partagé (shared tree)** dans PIM Sparse Model :
- Tous les sources du même **groupe multicast** envoient via un **RP commun**
- Tous les **récepteurs** reçoivent via le même RP
- Cela crée un arbre "*,G" (any source, groupe G) **dirigé vers le RP**
- Idéal pour les situations où les sources et récepteurs sont nombreux et dispersés

Deux types d'arbres :
1. **(*, G) tree** - arbre partagé vers RP
2. **(S, G) tree** - arbre source-spécifique, créé après une convergence

---

### Question 7
Quel est le mécanisme de "IGMP Snooping" sur un switch Layer 2?

A) Les switches examinent les paquets IGMP pour apprendre les abonnements multicast et limiter la inondation multicast aux ports intéressés  
B) Les switches se comportent como des routeurs multicast  
C) Les switches bloquent tout le trafic multicast par défaut  
D) IGMP Snooping est utilisé uniquement pour la validation de sécurité  

**Answer:** A  
**Explanation:** Le **IGMP Snooping** sur les switches Layer 2 :
- Les switches **lisent les messages IGMP** entre les hôtes et les routeurs décisifs
- Quand un hôte envoie "IGMP Join pour 224.1.1.1", le switch **apprend** que ce port veut ce groupe
- Le switch **limite la inondation multicast** UNIQUEMENT aux ports avec récepteurs actifs (+ port routeur)
- **Sans IGMP Snooping :** tout le trafic multicast est inondé sur tous les ports (broadcast-like)

Cela **réduit spectaculairement** l'utilisation de bande passante LAN.

---

### Question 8
Quel est l'avantage principal de "IGMPv3" par rapport à "IGMPv2"?

A) IGMPv3 élimine le besoin de RP  
B) IGMPv3 supporte "_Source Specific Multicast (SSM)_ pour contrôler EXACTEMENT quelle source le récepteur accepte  
C) IGMPv3 remplace complètement le PIM  
D) IGMPv3 chiffre automatiquement le trafic multicast  

**Answer:** B  
**Explanation:** **IGMPv3** ajoute une granularité source :
- **IGMPv2 :** "Je veux le groupe 224.1.1.1" (de n'importe quelle source)
- **IGMPv3 :** "Je veux le groupe 224.1.1.1 SEULEMENT de la source 10.1.1.1" ou "Je veux le groupe SAUF de la source 10.2.2.2"

Cela permet :
- Sécurité accrue (le récepteur rejette les sources non autorisées)
- **Source Specific Multicast (SSM)**
- Moins de vulnérabilité aux attaques multicast malveillantes

---

### Question 9
Quel est le comportement du "PIM Dense Mode"?

A) RSS déploie les routeurs via la propagation initialement, puis les routeurs sans intérêt "prune" eux-mêmes  
B) Le mode se comporté comme IGMP uniquement  
C) Tous les routeurs doivent être préconfigurés avec les groupes multicast  
D) Dense Mode utilise toujours un RP central  

**Answer:** A  
**Explanation:** **PIM Dense Mode (PIM-DM)** utilise une approche **"flood and prune"** :
1. Inicialmente, les routeurs **inondent** le trafic multicast sur tous les liens sauf celui reçu
2. Si un routeur n'a **PAS de récepteurs intéressés** pour ce groupe, il envoie un message **"Prune"** au routeur source
3. Le trafic cesse d'être envoyé sur les branches "élagées"

Avantages : Pas besoin de RP (automatique)  
Désavantages : Utilisation initiale de bande passante + overhead de pruning

---

### Question 10
Quel est le rôle de "PIM Sparse Mode"?

A) Les routeurs inondent d'abord, puis élagent les branches inutiles  
B) Les routeurs NE PROPAGENT le trafic que SI un récepteur explicitement "join"  
C) Le mode ne fonctionne que sur les réseaux à basse bande passante  
D) PIM Sparse Mode remplace le protocole IGP  

**Answer:** B  
**Explanation:** **PIM Sparse Mode (PIM-SM)** est une approche **"join-driven"** :
1. Les routeurs NE propagent PAS le trafic par défaut
2. Quand un hôte Join, un message est envoyé UP l'arbre vers le RP
3. L'RP amorce le trafic source DOWN vers le récepteur
4. Les arbres sont créés **ON-DEMAND** plutôt que inondés

Avantages : Économie de bande passante (pas de flood initial), nécessite un RP  
Idéal pour : Les réseaux étendus avec des sources/récepteurs éloignés

---

### Question 11
Quel est le "MSDP" (Multicast Source Discovery Protocol)?

A) Un protocole utilisé pour découvrir les sources multicast entre les domaines PIM SM avec différents RPs  
B) Un protocole IGP pour le routage multicast  
C) Un remplacement du protocole PIM  
D) Un protocole pour valider les adresses MAC multicast  

**Answer:** A  
**Explanation:** **MSDP** résout un problème clé dans PIM SM avec plusieurs RPs :
- Si une source S1 en domaine PIM-SM A avec RP-A reçoit des paquets, RP-A localise S1
- Mais les récepteurs en domaine B avec RP-B ne **sauront pas** que S1 existe (RP-B ne sait pas)
- **MSDP** entre les RPs tell "Je connais une source pour le groupe 224.1.1.1" et partage cette info

MSDP établit des sessions TCP entre les RPs des différents domaines PIM.

---

### Question 12
Quel est le mécanisme "Fast Reroute (FRR)" dans le contexte multicast?

A) Résout immédiatement les défaillances de lien en changeant rapidement le RP  
B) Utilisé pour les sauvegardes automatiques des données multicast  
C) Techniquement pas un déstandardisé multicast, plutôt une fonction MPLS TE  
D) N/A - le multicast ne supporte pas la reroutage rapide  

**Answer:** C  
**Explanation:** Le **Fast Reroute (FRR)** n'est pas spécifique au multicast. C'est une technique **MPLS Traffic Engineering** pour la haute disponibilité:
- Quand un lien MPLS échoue, les paquets sont immédiatement commutés vers un chemin alternatif pré-calculé
- Le multicast peut tourner OVER MPLS TE avec FRR, mais FRR lui-même est un mécanisme d'infrastructure

Pour la **haute disponibilité multicast**, on utilise plutôt **RP redundancy** et **multiple RPs**.

---

### Question 13
Comment configurez-vous un "Bootstrap Router (BSR)" pour l'élection dynamique du RP dans PIM?

A) Chaque routeur devient candidat BSR avec la priorité manuellement configurée  
B) Un seul routeur peut être élu BSR basé sur la priorité et l'adresse IP  
C) BSR est uniquement utilisé dans PIM Dense Mode  
D) BSR élimine complètement le besoin du RP  

**Answer:** A (partiellement), B (mieux)  
**Explanation:** Le **Bootstrap Router (BSR)** automatiše l'élection du RP dans PIM SM :
1. Les routeurs candidats BSR **annoncent leur candidature** via Bootstrap messages
2. L'élection est basée sur **priorité (plus haut gagne)**, puis **adresse IP (plus élevée gagne)**
3. Le BSR **distribue les informations du RP-Candidate** à tous les routeurs du domaine

Configuration :
```
router pim
 bsr-candidate Gi0/0 51    ← Prioricy 51 (défaut 64)
 rp-candidate Gi0/0 120    ← Prioricy 120 (plus bas = meilleur)
```

---

### Question 14
Quel est le rôle des "Rendezvous Point (RP) Redundancy"?

A) Avoir plusieurs RPs permet la haute disponibilité si un RP échoue  
B) Élimine le besoin d'un RP physique  
C) Les RPs redondants doivent être configurés avec le même ASN  
D) N/A - RP redundancy n'est pas supportée dans les réseaux modernes  

**Answer:** A  
**Explanation:** La **RP Redundancy** assure que si un RP échoue, un autre RP backup prend immédiatement le relais :
- **Statique :** Configurer manuellement les routeurs candidate RP (très disponible)
- **Dynamique :** Utiliser **BSR (Bootstrap Router)** pour élire automatiquement l'RP
- **MSDP** : Coordonner entre multiples domaines PIM SM avec leurs propres RPs

Cela FACILITATEs la **haute disponibilité multicast** pour les services critiques (IPTV, vidéo conférence en direct).

---

### Question 15
Quel est l'avantage principal du mode "PIM Bidirectional"?

A) Allows multicast in both IPv4 et IPv6 simultanément  
B) Réduit encore plus l'utilisation de bande passante comparé au PIM SM en utilisant un seul arbre bidrectionnel  
C) Remplace complètement les arbres partagés et source-spécifiques  
D) Nécessite moins de configuration que PIM Sparse Mode  

**Answer:** B  
**Explanation:** **PIM Bidirectional (PIM-Bidir)** utilise un seul arbre optimisé :
- Contrairement à PIM SM qui crée d'abord un arbre partagé `(*,G)` puis optimize vers `(S,G)`,
- **PIM-Bidir utilise UN SEUL arbre réadapté au RP** dans BOTH directions
- Les sources envoient UP vers le RP, les récepteurs envoient REQUESTS UP vers le RP
- Le RP réplique DOWN vers tous les récepteurs

Efficacité : **Unique arbre = moins d'overhead** que deux arbres (shared + source-specific)

---

## SECTION 2: QoS FUNDAMENTALS & MECHANISMS (Questions 16-50)

### Question 16
Quel est le problème principal du "best effort delivery model" dans les réseaux?

A) Les paquets arrivent toujours dans le même ordre mais avec délai variable  
B) Les paquets peuvent être perdus, retardés, ou délivrés hors d'ordre, affectant gravement les applications temps réel  
C) Les routeurs doivent analyser chaque paquet manuellement  
D) N/A - best-effort est parfait pour tous les types de trafic  

**Answer:** B  
**Explanation:** Le **Best-Effort delivery** (modèle par défaut Internet) :
- **N'offre AUCUNE garantie** sur la livraison, l'ordre ou le délai
- Paquets peuvent être **perdus** (congestion), **retardés** (queuing), **réordonnés** (chemins différents)
- Pour les applications temps réel (**VoIP, vidéo en direct**), c'est catastrophique :
  - Perte = trou audio/vidéo
  - Délai > 150 ms = qualité dégradée
  - Jitter = audio haché

C'est pourquoi **QoS** implante les garanties nécessaires.

---

### Question 17
Quels sont les trois problèmes de "Quality Issues" principaux énumérés dans le cours, causant une mauvaise QoS?

A) Encryption, routing instability, MAC address conflicts  
B) Bandwidth insuffisant, Latency, Jitter, Packet Loss  
C) BGP convergence time, OSPF SPF calculation, EIGRP queries  
D) ISP throttling uniquement  

**Answer:** B  
**Explanation:** Les trois **causes principales de problèmes de QoS** :
1. **Manque de bande passante** : le lien est saturé, paquets sont droppés
2. **Latency (delai)** : propagation, serialization, processing delays > 150 ms
3. **Jitter (variation de délai)** : les paquets arrivent à des intervalles irréguliers

Solutions :
- Augmenter la bande passante (coûteux, pas toujours possible)
- Implémenter **QoS** : classification, marking, policing, shaping, queuing

---

### Question 18
Quel est le modèle "IntServ (Integrated Services)" et ses limitations?

A) IntServ demande une réservation de ressources préalable (RSVP) pour chaque flux de données  
B) IntServ est le modèle par défaut moderne utilisé universellement  
C) IntServ n'affecte que la bande passante, pas le délai  
D) IntServ élimine complètement le besoin de QoS avancée  

**Answer:** A  
**Explanation:** **IntServ (Integrated Services)** utilise **RSVP (Resource Reservation Protocol)** :
- Chaque application envoie un message RSVP disant "Je besoin de 1 Mbps, délai < 50 ms"
- Les routeurs réservent les ressources dans leur buffer et bande passante
- **Avantages :** Garanties strictes per-flow
- **Limitations :**
  - **Scalabilité pauvre** : 1000+ appel simultanés = 1000+ réservations
  - **État complexe** : chaque routeur maintient l'état de chaque flow
  - Pas largement déployé sur l'Internet public

---

### Question 19
Quel est le modèle "DiffServ (Differentiated Services)" et ses avantages?

A) DiffServ classe les paquets en catégories de service et applique des traitements différenciés sans réservation par-flow  
B) DiffServ remplace complètement IntServ et RSVP  
C) DiffServ fonctionne seulement sur les liens Ethernet  
D) N/A - DiffServ n'existe que en théorie  

**Answer:** A  
**Explanation:** **DiffServ** est le modèle déployé largement :
1. **Classification :** Identifier le trafic (VoIP, vidéo, données)
2. **Marking :** Ajouter un "tag" au paquet (DSCP dans IPv4 ToS field)
3. **Behandlung différencié :** 
   - VoIP (DSCP 46) → priorité haute, peu de queue
   - Vidéo (DSCP 34) → priorité moyenne
   - Données (DSCP 0) → best-effort

**Avantages :**
- **Scalable** : Pas de réservation per-flow, juste per-class
- **Simple** : Un seul DSCP value, pas d'état d'état complexe
- Largement déployé (Internet moderne, réseaux d'entreprise)

---

### Question 20
Quel est le champ "DSCP (Differentiated Services Code Point)" et où se trouve-t-il?

A) Un numéro 6-bit dans le champ ToS (Type of Service) d'IPv4 header  
B) Un numéro 8-bit dans le champ TTL  
C) Un pointeur vers une table de classification MAC  
D) Un numéro dans le champ UDP sport  

**Answer:** A  
**Explanation:** Le **DSCP (6 bits) du champ IPv4 ToS (8 bits)** :
```
IPv4 ToS octet (8 bits):
[DSCP (6 bits)][ECN (2 bits)]
```

**DSCP values communs :**
- **46 (0x2E)** : EF (Expedited Forwarding) - VoIP/Real-time
- **34 (0x22)** : AF31 - Vidéo
- **26 (0x1A)** : AF21 - Données importantes
- **0** : Best Effort (défaut)

DSCP remplace l'ancien système **ToS/IP Precedence (3 bits)**.

---

### Question 21
Quel est le rôle principal de la "Classification" dans QoS?

A) Détecter et rejeter les paquets malformés  
B) **Identifier le type de trafic** pour appliquer des politiques QoS appropriées  
C) Chiffrer les paquets de données sensibles  
D) Compresser les paquets pour augmenter la bande passante  

**Answer:** B  
**Explanation:** La **Classification** est la PREMIÈRE étape du QoS :
- Identifier quels paquets sont VoIP, Vidéo, Email, etc.
- Méthodes :
  - **ACL-based** : Regarder source/dest IP, port (flux5-tuple)
  - **NBAR (Network Based Application Recognition)** : Identifier par deep packet inspection (p.ex., Skype, Netflix)
  - **Layer 7** : Inspect le contenu de l'application

Une fois classifié, les paquets sont **MARKED** (taggés) avec DSCP ou CoS pour le reste du voyage.

---

### Question 22
Quel est le rôle de "Marking" dans QoS?

A) Ajouter un "tag" au paquet (DSCP/CoS) pour porter l'information de classification à travers le réseau  
B) Ajouter une signature numérique pour la sécurité  
C) Réduire la taille du paquet  
D) Diviser un grands paquet en plus petits paquets  

**Answer:** A  
**Explanation:** **Marking** encode la décision de classification dans le paquet :
- IPv4 : **set DSCP** dans le champ ToS
- IPv4/IPv6 : **set IP Precedence** (3 bits, hérité)
- Ethernet (Classe 2 switches): **set CoS (Class of Service)** dans 802.1Q tag (3 bits)

Exemple :
```
route-map MARK permit 10
 match ip address VoIP
 set dscp ef  ← Mark paquet avec EF (46)
```

Cela permet aux routeurs/switches **entre domains** de reconnaître et traiter le trafic appropriément.

---

### Question 23
Quel est le "CoS (Class of Service)" et comment diffère-t-il du DSCP?

A) CoS (3 bits) dans le 802.1Q tag Ethernet, DSCP (6 bits) dans IPv4 ToS  
B) Identiques ; noms différents pour le même concept  
C) DSCP fonctionne uniquement IPv6  
D) CoS est dépracié et remplacé complètement par DSCP  

**Answer:** A  
**Explanation:**
- **CoS (Class of Service)** :
  - 3 bits dans l'**en-tête 802.1Q (VLAN tag)** Ethernet
  - Utilisé par les **switches Layer 2** pour les décisions de queuing
  - Portée : **local link uniquement** (le tag est retiré/remplacé en franchissant les domaines VLAN)

- **DSCP (Differentiated Services Code Point)** :
  - 6 bits dans l'**en-tête IPv4 ToS**
  - Utilisé par les **routeurs Layer 3** end-to-end
  - Portée : **tout le way à travers l'Internet** (survit au routage)

**Mappage typique :** CoS 5 (élevé) → DSCP 46 (EF)

---

### Question 24
Quel est le rôle de la "Policing" dans QoS?

A) Appliquer une limitation de débit sur le trafic et dropper l'excédent  
B) Limiter la taille du paquet  
C) Authentifier la source du trafic  
D) Rediriger le trafic vers une adresse IP alternative  

**Answer:** A  
**Explanation:** **Policing (ou rate- limiting)** :
- **Mesure** le débit du trafic entrant
- Si le trafic **dépasse le taux configuré**, les actions sont :
  - **Drop** (éliminer) les paquets en excès
  - **Mark** les paquets en excès avec un DSCP plus bas
  - **Delay** est moins courant (plus coûteux en CPU)

Exemple :
```
police rate 1000000 bps burst 100000 bytes
 conform-action transmit
 exceed-action drop
```

Cela fait un **"hard limit"** sur le trafic. Le trafic en excès est simplement supprimé.

---

### Question 25
Quel est le rôle de la "Shaping" et comment diffère-t-il de la Policing?

A) Shaping stocke l'excédent dans une queue ; Policing le droppe simplement  
B) Shaping fonctionne seulement sur IPv6  
C) Policing et Shaping sont identiques  
D) Shaping réécrit les adresses IP  

**Answer:** A  
**Explanation:**
- **Shaping (Traffic Shaping)** :
  - **Stocke l'excédent** dans une file d'attente (buffer)
  - Envoie progressivement quand la bande passante se libère
  - **Lisse** le trafic "burst" sur le temps
  - **Approche non-destructive** (aucun paquet n'est perdu)
  - Utilisé auprès de **WAN links** où jamais gaspiller de bande passante disponible

- **Policing (Rate Limiting)** :
  - **Droppe l'excédent** immédiatement
  - **Approche destructive** (certains paquets sont perdus)
  - Utilisé auprès de **client-facing links** pour appliquer SLA strict

**Cas d'usage :**
- Shaping : lien WAN vers ISP (ne perdez pas la bande passante)
- Policing : client paying pour 10 Mbps SLA (enforcer le limite)

---

### Question 26
Quel est le "Congestion Management" et quel le "Congestion Avoidance"?

A) Tous deux contrôlent la congestion au nom des techniques différentes  
B) CM gère les files d'attente ; CA prédit et prévient la congestion  
C) CM est obsolète ; CA le remplace complètement  
D) CM signifie "Classifier Mapping" ; CA signifie "Centralized Archive"  

**Answer:** A/B  
**Explanation:**
- **Congestion Management (Queuing)** :
  - Quand la congestion **existe**, gérer les files d'attente :
  - **FIFO** : First-In-First-Out (une seule queue)
  - **PQ** : Priority Queuing (class 1, 2, 3 strict priority)
  - **WFQ** : Weighted Fair Queuing (classes avec poids)
  - **CBWFQ** : Class-Based WFQ(QoS réels, classes multiples avec bande passante réservée)

- **Congestion Avoidance** :
  - Avant que la congestion N'EXISTE, **prédire et éviter**
  - **WRED** : Weighted Random Early Detection
  - Quand une queue commence à se remplir, random DROPS paquets dans advance
  - Les flows réduisent graduellement leur envoi (TCP backoff)

---

### Question 27
Quel est le rôle des "Queued Buffers" dans QoS?

A) Stocker les paquets temporairement attendre leur transmission quand la bande passante est disponible  
B) Rejeter les paquets immédiatement si le lien est occupé  
C) Compresser les paquets pour réduire la mémoire utilisée  
D) Fragmenter les paquets en plus petits blocs  

**Answer:** A  
**Explanation:** Les **Buffers de queue** :
- Stockent les paquets temporairement quand le lien est occupé
- Les paquets **haute priorité** (VoIP, vidéo) sont en queue **avant** les faibles priorité (données bulk)
- Quand la bande passante se libère, le routeur **transmet les paquets haute priorité EN PREMIER**

**Configuration (CBWFQ - Class-Based WFQ)** :
```
class-map VOICE
 match dscp ef
!
policy-map QoS
 class VOICE
  priority percentage 30  ← 30% de la bande réservée pour VoIP
 class DATA
  bandwidth percentage 70  ← 70% pour données
!
interface Gi0/0
 service-policy output QoS
```

---

### Question 28
Quel est le "WRED (Weighted Random Early Detection)"?

A) Ajouter du poids aléatoire aux paquets pour équilibrer les charges  
B) Détecter précocement la congestion, puis probabilistically drop paquets HIGH-DSCP pour signaler le contrôle de congestion TCP  
C) Wrapper le protocole RIP dans un tunnel sécurisé  
D) Reséquencer les paquets out-of-order  

**Answer:** B  
**Explanation:** **WRED** est une stratégie proactive de congestion avoidance :
1. Surveillance la profondeur moyenne de la queue
2. Quand la queue commence à **se remplir**, ne pas attendre la saturation
3. **Aléatoirement lever des paquets METRIQUES**:
   - Les paquets **DSCP bas** (données) sont dropés plus souvent
   - Les paquets **DSCP haut** (VoIP) sont dropés rarement
4. Les émetteurs TCP détectent la perte → réduire automatiquement la transmission

**Avantage:** Prévient la congestion catastrophique (queue full = tous les paquets droppés)

---

### Question 29
Quel est le problème avec "FIFO (First-In-First-Out)" dans un réseau congestionné?

A) Les paquets haute priorité attendent derrière les données bulk  
B) FIFO dropped les paquets trop tôt  
C) N/A - FIFO est optimal pour tous les réseaux  
D) FIFO nécessite une configuration complexe  

**Answer:** A  
**Explanation:** **FIFO (défaut)** :
- Une seule queue : **tous les paquets sont traités dans l'ordre ils arrivent**
- Si 10 paquets email arrivent avant 1 paquet VoIP → **VoIP doit attendre**
- Résultat : **qualité VoIP dégradée** (délai > 150 ms)

C'est pourquoi les implémentations QoS utilisent **multiples queues** :
- Queue 1 (Priorité) : VoIP (DSCP 46)
- Queue 2 (Standard) : Vidéo (DSCP 34)
- Queue 3 (Best Effort) : Données (DSCP 0)

Le routeur transmet tous les paquets de Queue 1 → Queue 2 → Queue 3.

---

### Question 30
Quel est le "serialization delay" et comment peut-on le minimiser?

A) Le délai pour placer tous les BITS d'un paquet sur le lien ; minimiser augmentation la bande passante  
B) La durée de la sérialisation du paquet au format réseau  
C) Le délai de transmission TCP/IP handshake  
D) N/A - serialization delay n'est pas un concept réel  

**Answer:** A  
**Explanation:** Le **Serialization Delay** :
- **Calcul :** Délai = Taille paquet (bits) / Vitesse du lien (bps)
- **Exemple :** Paquet 1500 bytes sur Serial T1 (1.544 Mbps)
  - 1500 bytes = 12,000 bits
  - Délai = 12,000 / 1,544,000 ≈ 7.77 ms

Pour les **réseaux WAN lents**, ce délai est NON-NEGLIGIBLE :
- T1 (1.544 Mbps) : 1500-byte paquet ≈ 7.7 ms
- Technologie : **MTU  compression**, réduire la taille du paquet

**Configuration (Fragment des paquets)** :
```
interface Serial0/0
 ip mtu 576  ← Réduit la MTU, réduit la serialization delay
```

---

### Question 31
Quel est le rôle des "Link Fragmentation and Interleaving (LFI)"?

A) Diviser les paquets volumineux et interleaver des paquets VOIP petits pour réduire le délai VoIP  
B) Fragmenter automatiquement les adresses IP  
C) Diviser les connexions VPN en segments  
D) Interleaver codes de correction d'erreur  

**Answer:** A  
**Explanation:** **LFI (Link Fragmentation and Interleaving)** sur les liens WAN lents (T1, E1, etc.):
1. **Décomposer les paquets volumineux** (p.ex., fichier de téléchargement 12 KB) en fragments
2. **Interleaver les petits paquets VoIP** entre les fragments
3. Résultat : **Le paquet VoIP ne doit pas attendre 12 KB entier**

Exemple :
- T1 (1.544 Mbps) avec MTU 1500 bytes = 7.7 ms de délai
- 12 KB fichier = 8 paquets × 7.7 ms = 61 ms (inacceptable pour VoIP)
- LFI : Fragment à 256 bytes → 0.65 ms per fragment → VoIP peut être interleeavé

---

### Question 32
Quel est le "Local Preference" dans le contexte QoS (pas BGP)?

A) Marquer les paquets pour être traités localement  
B) Configurer la queue préférée sur une interface  
C) N/A - Local Preference est uniquement un concept BGP  
D) Créer une politique de données locales  

**Answer:** C  
**Explanation:** C'est une "piègeQuestion d'examen" - **Local Preference est UNIQUEMENT un concept BGP**, pas QoS.

Dans le contexte QoS, on utilise :
- **Priority** : pour priorité queue
- **Bandwidth** : pour réserver la bande passante à la classe
- **DSCP** : pour marking

---

### Question 33
Comment configurez-vous une "Traffic Class" avec la bande passante garantie de 30% dans une politique QoS?

A) **bandwidth percent 30** (dans class-map)  
B) **priority percentage 30**  
C) **bandwidth percent 30** (dans policy-map, config classe)  
D) **qos class 30 percent**  

**Answer:** C  
**Explanation:** Syntaxe Cisco pour QoS avec CBWFQ :
```
policy-map LAN-QoS
 class VoIP
  priority percentage 30  ← Strict priorité pour VoIP
 class Video
  bandwidth percentage 40  ← Bande réservée pour vidéo
 class Data
  bandwidth percentage 30  ← Bande réservée pour données
!
interface Gi0/0
 service-policy output LAN-QoS
```

**Différence :**
- **priority** : Strict priorité (transmet AVANT les autres classes)
- **bandwidth** : Bande minimale réservée (utilise l'excès si libre)

---

### Question 34
Quel "QoS Metering" ou "Rate Measuring" est utilisé pour faire valoir les politiques?

A) Tokens Bucket Algorithm (TBA)  
B) Leaky Bucket Algorithm  
C) Random Early Detection (RED)  
D) Tous A et B  

**Answer:** D  
**Explanation:**
- **Token Bucket** :
  - Génère des tokens à un débit spécifié
  - Les paquets peuvent être envoyés si tokens disponibles
  - Les tokens inutilisés s'accumulent (petit burst permis)
  - Utilisé dans policing et shaping

- **Leaky Bucket** :
  - L'eau (paquets) s'accumule dans un seau
  - L'eau fuit à un débit constant (débit garanti)
  - Seau plein → paquets dropés
  - Lisse les bursts

Deux implémentations du même concept : **rate limiting avec accumulation de burst permise**.

---

### Question 35
Quel est "RFC 2598" et "RFC 2597" dans le contexte DSCP?

A) Spécifications pour différents types IPv6  
B) Définir EF (Expedited Forwarding) et AF (Assured Forwarding)  
C) Équivalent moderne de ToS/IP Precedence  
D) Standards pour DMVPN et MPLS VPNs  

**Answer:** B  
**Explanation:**
- **RFC 2598** : **Expedited Forwarding (EF)** - DSCP 46
  - Pour le trafic en tempo réel sensible (VoIP, vidéo interactive)
  - Traitement : **Priorité stricte**, peu de delai/jitter
  - SLA : délai < 50 ms, jitter minimal

- **RFC 2597** : **Assured Forwarding (AF)**
  - 4 niveaux de priority (1-4) × 3 niveaux de drop probability (1-3)
  - AF41 (34) : Vidéo en direct
  - AF31 (26) : Données business-critical
  - AF11 (10) : Données bulk

---

### Question 36
Quel est le rôle des "MQC (Modular QoS CLI)" dans les implémentations QoS Cisco?

A) La structure de configuration standardisée pour QoS (class-map → policy-map → interface)  
B) Un protocole multicast spécifique à Cisco  
C) Un algorithme de sélection de queue alternatif  
D) N/A - MQC est dépracié  

**Answer:** A  
**Explanation:** **MQC (Modular QoS CLI)** est l'approche Cisco standard pour la configuration de QoS :

**Structure hiérarchique :**
```
1. class-map [match-type] <name>
   match <criteria>

2. policy-map <name>
   class <class-name>
   [bandwidth | priority] <value>
   [set dscp <value>]

3. interface <interface>
   service-policy [input | output] <policy-name>
```

MQC permet une **configuration reprochée et réutilisable** des politiques QoS.

---

### Question 37
Quel est le "match-type" pour une class-map (match-any vs match-all)?

A) **match-any** : La classe corresponds si AU MOINS UN critère correspond  
B) **match-all** : La classe corresponds si TOUS les critères correspondent  
C) Les deux sont identiques  
D) match-any n'existe pas, seulement match-all  

**Answer:** A/B (both true)  
**Explanation:**
- **match-any** (défaut si rien n'est spécifié) :
  - Correspond si n'importe quel critère correspond
  - Exemple :
    ```
    class-map match-any VOICE
     match dscp ef
     match ip address 10  ← OU si dans l'ACL 10
    ```
    Donc : DSCP ef OU matches ACL 10 → classe VOICE

- **match-all** :
  - Correspond UNIQUEMENT si TOUS les critères correspondent
  - Très restrictif, rarement utilisé

---

### Question 38
Quel est le comportement par défaut de "remainder traffic" (trafic qui NE CORRESPOND À AUCUNE classe)?

A) Dirigé vers une "default class"  
B) Dropé immédiatement  
C) Traité comme best-effort  
D) Rejeté avec un message ICMP  

**Answer:** A/C  
**Explanation:** Quand un paquet n'est pas **explicitement classifié** :
- S'il existe une **class-default visée** → utilisée
- Sinon → traité comme **best-effort (DSCP 0, bande passante non réservée)**

Recommandation :
```
class class-default  ← Capture tout ce qui ne match pas les autres classes
 bandwidth percent 20  ← Assurer au moins de la bande pour le trafic par défaut
```

Cela empêche les paquets de rester intérêts de configuration QoS incomplètes.

---

### Question 39
Quel est l'avantage d'utiliser des "Named ACL" comparé aux "Numbered ACL" pour la classification QoS?

A) Les Named ACL sont plus rapides  
B) Les Named ACL sont plus lisibles et maintenables  
C) Les numérotés ACL sont meilleurs pour Ipv6  
D) Immédiat - les deux offrent les mêmes avantages  

**Answer:** B  
**Explanation:**
- **Numbered ACL :** `access-list 10 permit ip any host 192.168.1.1`
  - Difficile à identifier quel numéro fait quoi
  - No control de modifitions (ne peut pas insérer au milieu)

- **Named ACL :** `ip access-list INTERNAL-NETWORKS / permit ip any host 192.168.1.1`
  - Descriptif ; facile d'identifier l'objectif
  - Peut envoyer des modify ACE au sein (inseert/remove spécifique)
  - Meilleure pratique pour QoS moderne

---

### Question 40
Quel est le total des pourcentages de "bandwidth" attribué qui est permis dans une policy-map?

A) 100% maximum  
B) 99% (1% réservé pour la signalisation)  
C) Peut dépasser 100% si certaines classes ne reçoivent pas le trafic  
D) Pas de limites strictes - peut configurer 200%+  

**Answer:** C (principalement)  
**Explanation:** Dans Cisco QoS :
- Vous **pouvez théoriquement configurer** plus de 100%
- MAIS au moment de l'exécution :
  - Si AUCUNE classe n'utilise sa allocation → les autres peuvent utiliser le surplus
  - Si TOUTES les classes consomment la bande = congestion continu

**Best practice :**
```
policy-map WAN
 class VoIP
  priority 256  ← Priorité stricte (pas de %)
 class Video
  bandwidth 512  ← 512 kbps garanti
 class Data
  bandwidth 512  ← 512 kbps garanti
 class class-default
  bandwidth 256  ← Reste
```

Total pour WAN lien = 1280 + overhead. Flexible à 1.5 Mbps total.

---

### Question 41
Quel est l'impact de la configuration "no auto-qos" sur une interface?

A) Désactiver la configuration automtique QoS (Cisco AutoQoS feature)  
B) Forcer QoS à appliquer uniquement au trafic sortant  
C) Réseter tous les paramètres QoS à défaut  
D) ACTIVATE une option QoS automatique  

**Answer:** A  
**Explanation:** **Cisco AutoQoS** est une fonctionnalité de configuration automatique simplifiée :
```
interface Gi0/0
 auto qos
  ← Configure automatiquement une politique QoS simple
```

Cela :
- Crée des class-maps/policy-maps basées sur NBAR (Application Recognition)
- Assigne DSCP automatiquement
- Applique un modèle "One-to-One" (VoIP priorité, vidéo bande passante réservée)

Avec **`no auto qos`** → AutoQoS est **désactivé**. Vous configurez manuellement.

---

### Question 42
Quelle est la relationship entre "MTU reduction" et "Serialization Delay" da WAN links?

A) Réduire MTU réduit directement la serialization delay, bénéfique pour VoIP sur les liens lents  
B) La réduction MTU n'a aucun impact sur serialization delay  
C) La réduction MTU augmente serialization delay  
D) Seules les modifications des outils matériels peuvent réduire serialization delay  

**Answer:** A  
**Explanation:** **Serialization Delay** = Taille paquet / Vitesse du lien

Réduire la MTU → paquets plus petits → délai réduit :
- T1 (1.544 Mbps), MTU 1500 bytes → 7.7 ms
- T1 (1.544 Mbps), MTU 256 bytes → 1.3 ms

Beaucoup moins de délai pour VoIP !

**Configuration :**
```
interface Serial0/0
 ip mtu 256  ← Fragmente MTU plus petite
```

C'est pourquoi **LFI (Link Fragmentation and Interleaving)** est critique pour les WAN lents.

---

### Question 43
Quel est le "voice-friendly QoS" requirements généralement?

A) Réserver au moins 10% de la bande passante pour VoIP  
B) Marquer tous les VoIP comme DSCP 46 (EF), limiter délai < 150 ms, jitter < 30 ms  
C) Désactiver tous les autres trafics pendant les appels VoIP  
D) Vous n'avez pas besoin de QoS pour VoIP moderne  

**Answer:** B  
**Explanation:** Pour une bonne **qualité VoIP** :
1. **DSCP Marking** : EF (46) pour tous les paquets VoIP
2. **Délai** : < 150 ms end-to-end (ITU G.114)
   - > 200 ms = dégradation notable
   - > 400 ms = inacceptable
3. **Jitter** : < 30 ms variation de délai
4. **Packet Loss** : < 1% acceptable

**Configuration SIP Call Exemple :**
- SIP signalisation : AF31 (26)
- RTP média (voix) : EF (46)
- Réserver 30% de la bande passante pour VoIP

---

### Question 44
Quel est le rôle du "ECN (Explicit Congestion Notification)" dans moderne QoS?

A) Les routeurs délibérément marquent les paquets ECN quand la congestion commence  
B) Les émetteurs TCP reconnaissent le marquage ECN et réduisent le transmission (plus gracieux que la perte)  
C) ECN est la technologie clé pour DiffServ moderne  
D) ECN remplace complètement WRED  

**Answer:** A/B et C/D partiellement  
**Explanation:** **ECN (RFC 3168)** :
1. Les **routeurs** marquent les paquets avec ECN bits WHEN congestion détecte (alternative à dropper)
2. Les **hosts** TCP reconnaissez ECN → réduisent cwnd (congestion window)
3. Résultat : **Pas de perte paquet, seulement ralentissement**

ECN + WRED = **stratégie optimale** :
- WRED détecte précocement la congestion
- Marque ECN (pas droppe) si supporté
- Les émetteur TCP réduisent gracieusement
- Si ECN pas supporté, WRED droppe

**Enabler :** Le système opérierat modern (Linux, Windows) supportent ECN.

---

### Question 45
Quelle est la difference entre "Hard Guarantees" et "Soft Guarantees" en QoS?

A) Hard = DSCP uniquement, Soft = avec CoS aussi  
B) Hard = garantie par LE SERVICE PROVIDER ;  Soft = tentative best-effort  
C) Hard = priorité stricte sans révocation ; Soft = priorité basé sur la disponibilité  
D) Elles sont identiques ; syntaxe différente uniquement  

**Answer:** B/C  
**Explanation:**
- **Hard Guarantees** :
  - **Service Provider SLA garantit** minimum bande passante, max délai
  - Idem "priorité stricte" = VoIP reçoit TOUJOURS sa 30% bande réservée
  - Coûteux (requiert over-provisioning)

- **Soft Guarantees** :
  - **Best-effort** : tenter de maintenir les niveaux QoS, mais pas garanti
  - Si le réseau est faiblement congestionné, le trafic obtiendra souvent les traitements
  - Si surchargé, les garanties s'effrondent

**Internet moderne :** Généralement "soft guarantees" (pas d'overprovisioning)
**Enterprise/SP :** "Hard guarantees" (SLAs payants)

---

### Question 46
Quel est le "Bandwidth Reservation" et comment s'applique-t-il ?

A) Administrateur réserve une certaine bande passante pour une classe, garantie disponible  
B) Les réservations sont toujours obligatoires pour QoS  
C) Réservé la bande passante signifie ces classes ne peuvent jamais dépasser la limite  
D) N/A - pas vraiment de réservation possible sur Internet

**Answer:** A partially, C partiellement  
**Explanation:** **Bandwidth Reservation :**
- Administrative déclare : "VoIP = 30% de 1 Mbps = 300 kbps guaranteed"
- **Available** : Cette allocation est réservée (d'autres classes ne peuvent pas l'utiliser)
- **Flexible** : Si VoIP utilise seulement 100 kbps, autres classes reçoivent les 200 kbps extras
- **Limite** : VoIP peut générer consommer PLUS si d'autres classes ne l'exigent pas

Configuré avec `bandwidth percent <value>` ou `bandwidth <kbps>`.

---

### Question 47
Quel est l'avantage d'une "Hierarchical QoS Policy"?

A) Appliquer différentes politiques à multiples sous-interfaces mais les propager de manière logique  
B) Créer des politique arborescences qui refléter la topologie réseau physique  
C) Améliorer les performances en réduisant les lookups nécessaires  
D) N/A - QoS est toujours plat, pas hiérarchique  

**Answer:** A/B  
**Explanation:** Si une **interface Gi0/0 a 100 sub-interfaces** (VLAN), une politique hiérarchique :
```
interface Gi0/0
 service-policy output PARENT-QoS
  ← Applique une logique parente

interface Gi0/0.100
 service-policy output CHILD-QoS
  ← Chaque VLAN peut avoir une sous-politique optionnelle
```

Cela permet :
- Poliques **communes** au niveau parent (toutes les VLANs)
- Poliques **VLAN-spécifiques** au niveau enfant
- Configuration plus maintenable

---

### Question 48
Quel est le "Jitter Buffer" et pourquoi est-il important pour VoIP?

A) Un buffer qui stocke les paquets et les joue à un débit constant pour adoucir la variation de délai  
B) Un buffer qui supprime aléatoirement les paquets-jitter  
C) Un buffer uniquement pour les paquets de contrôle IGMP  
D) N/A - Jitter Buffer n'existe pas en VoIP moderne  

**Answer:** A  
**Explanation:** **Jitter Buffer** sur les **téléphones VoIP/clients** :
- Reçoit les paquets RTP arrivent à des temps irréguliers
- **Stocke** dans un buffer d'assez grande profondeur
- **Joue progressivement** à un débit constant
- Résultat : adoucit le jitter perçu

Impact :
- **Petit buffer :** jitter audible (écho, interruptions)
- **Grand buffer :** accumulation délai (inacceptable > 150 ms)

Généralement ~100-400 ms configurable par VoIP client.

---

### Question 49
Quel est le "Voice VLAN" et comment diffère-t-il du "Data VLAN"?

A) Voice VLAN est un VLAN physique séparé pour les téléphones IP ; Data VLAN pour PC/serveurs  
B) Voice VLAN est marquée avec CoS/DSCP priorité plus élevé que Data VLAN  
C) Voice VLAN ne nécessite pas de routage (non routé)  
D) N/A - Voice et Data ne peuvent pas coexister sur les VLANs  

**Answer:** A/B  
**Explanation:** Le **Voice VLAN design** :
1. **Physical segregation** : Téléphones (Voice VLAN) vs. PCs (Data VLAN)
2. **Logical separation** : Téléphones envoient le trafic RTP marqué DSCP 46 (EF)
3. **Switch configuration :**
   ```
   interface Gi0/1
    switchport mode access
    switchport access vlan 100  ← Data VLAN
    switchport voice vlan 110  ← Voice VLAN (téléphones détection automatique)
   ```
4. Politique QoS appliquée : Voice traffic obtient priorité stricte

---

### Question 50
Quel est la SLA (Service Level Agreement) et comment QoS s'y rapporte?

A) Contrat entre client et provider définissant garanties de service (bande passante, délai, uptime)  
B) Une commande Cisco pour configurer les niveaux de service  
C) Un standard IETF pour la configuration QoS  
D) Un protocole de routage alternatif  

**Answer:** A  
**Explanation:** Une **SLA (Service Level Agreement)** :
- **Garantises contractuelles** entre Client and Service Provider
- Exemples :
  - "Bande passante >= 50 Mbps" (mesuré via netflow/sflow)
  - "Disponibilité >= 99.9%"
  - "Délai E2E <= 50 ms pour VoIP"
  - "Packet Loss < 0.1%"

**QoS s'applique :**
- Provider utilise des **politiques QoS** pour ASSURER la SLA
- Client reçoit un **niveau de service garanti** en échange $$$
- Violation SLA = **crédits/pénalités** au client

Cela justifie l'investissement QoS complexe.

---

## ANSWER KEY SUMMARY

| Q# | Answer | Q# | Answer | Q# | Answer | Q# | Answer |
|----|--------|----|----|----|----|----|----|
| 1 | B | 14 | A | 27 | A | 40 | A |
| 2 | A | 15 | B | 28 | B | 41 | A |
| 3 | B | 16 | B | 29 | A | 42 | A |
| 4 | B | 17 | B | 30 | A | 43 | B |
| 5 | B | 18 | A | 31 | A | 44 | A |
| 6 | B | 19 | A | 32 | C | 45 | B |
| 7 | A | 20 | A | 33 | C | 46 | A |
| 8 | B | 21 | B | 34 | A | 47 | A |
| 9 | A | 22 | A | 35 | B | 48 | A |
| 10 | B | 23 | A | 36 | A | 49 | A |
| 11 | A | 24 | B | 37 | A | 50 | A |
| 12 | C | 25 | B | 38 | C | | |
| 13 | B | 26 | A | 39 | B | | |

---

## Scoring Guide

- **90-100% (45-50 correct):** Multicast & QoS mastery - Ready for production
- **80-89% (40-44 correct):** Strong understanding - Review weak areas
- **70-79% (35-39 correct):** Passing - Meets minimum requirements
- **Below 70%:** Needs further study - Focus on Multicast and QoS mechanisms

**Exam Completed** - You have finished Modules 13-14 checkpoint assessment!
