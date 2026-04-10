# QCM Module 14 : QoS

## Questions 1-10

### Q1 : Quel paramètre est le plus critique pour les applications VoIP en QoS ?
**A)** Perte de paquet (< 10%)  
**B)** Latence (< 150ms)  
**C)** Bande passante (> 100 Mbps)  
**D)** Jitter (< 100ms)  

**Réponse : B** - **Latence < 150ms** est critique pour VoIP. Jitter < 30ms aussi important.

---

### Q2 : Quel modèle QoS définit une réservation de ressources bout-à-bout avec RSVP ?
**A)** Best Effort  
**B)** IntServ  
**C)** DiffServ  
**D)** QoE (Quality of Experience)  

**Réponse : B** - **IntServ** utilise **RSVP** pour réserver ressources strictement, mais peu scalable.

---

### Q3 : Quel modèle QoS est recommandé pour les réseaux modernes?
**A)** Best Effort (aucun QoS)  
**B)** IntServ (réservé)  
**C)** DiffServ (classification scalable)  
**D)** MPLS (étiquetage seulement)  

**Réponse : C** - **DiffServ** (classification + marking) est recommandé pour scalabilité et flexibilité.

---

### Q4 : À quelle couche OSI fonctionne le CoS (Class of Service) ?
**A)** Layer 1 (Physique)  
**B)** Layer 2 (Data Link/Ethernet)  
**C)** Layer 3 (Network/IP)  
**D)** Layer 4 (Transport/TCP-UDP)  

**Réponse : B** - **CoS** est un tag **Layer 2** (3 bits dans VLAN 802.1p header).

---

### Q5 : Quel est le nombre de bits utilisés par CoS ?
**A)** 1 bit  
**B)** 2 bits  
**C)** 3 bits  
**D)** 6 bits  

**Réponse : C** - **CoS = 3 bits** dans VLAN tag (plage 0-7).

---

### Q6 : À quelle couche OSI fonctionne le DSCP (Differentiated Services Code Point) ?
**A)** Layer 2 (Ethernet)  
**B)** Layer 3 (IP)  
**C)** Layer 4 (TCP/UDP)  
**D)** Layer 7 (Application)  

**Réponse : B** - **DSCP** est un tag **Layer 3** (6 bits dans champ ToS de l'IP header).

---

### Q7 : Quel est le nombre de bits utilisés par DSCP ?
**A)** 3 bits  
**B)** 4 bits  
**C)** 6 bits  
**D)** 8 bits  

**Réponse : C** - **DSCP = 6 bits** (plage 0-63).

---

### Q8 : Quel est la valeur DSCP pour Expedited Forwarding (EF) ?
**A)** 0  
**B)** 26  
**C)** 46  
**D)** 63  

**Réponse : C** - **EF (Expedited Forwarding) = DSCP 46**, utilisé pour VoIP priorité.

---

### Q9 : Quel est le principal avantage de DSCP par rapport à CoS ?
**A)** Meilleure vitesse transmission  
**B)** Portée end-to-end (survit routage)  
**C)** Réduction MTU  
**D)** Support IPv6 natif  

**Réponse : B** - **CoS = LAN seulement** (supprimé traversant routeurs); **DSCP = end-to-end** (survit routage).

---

### Q10 : Quel est la différence principal entre Policing et Shaping ?
**A)** Policing est pour inbound, Shaping pour outbound  
**B)** Policing drop si limit, Shaping queue  
**C)** Policing est plus cher en ressources  
**D)** Both A et B  

**Réponse : D** - **Policing = drop au-delà limite (inbound)**; **Shaping = queue/buffer (outbound)**.

---

## Questions 11-20

### Q11 : Quel est l'avantage principal de Shaping vs Policing ?
**A)** Shaping est plus simple à configurer  
**B)** Shaping évite perte paquet via buffering  
**C)** Shaping a latence plus basse  
**D)** Shaping utilise moins CPU  

**Réponse : B** - **Shaping = queue** → moins perte; **Policing = drop** → perte possible.

---

### Q12 : Quel est le type de queue "First-In-First-Out" ?
**A)** FIFO  
**B)** PQ  
**C)** WFQ  
**D)** CBQ  

**Réponse : A** - **FIFO** est le queueing simple sans priorité (premier entré, premier sorti).

---

### Q13 : Quel type de queueing risque de "starvation" pour les basses priorités ?
**A)** FIFO  
**B)** Priority Queueing (PQ)  
**C)** Weighted Fair Queueing (WFQ)  
**D)** Class-Based Queueing (CBQ)  

**Réponse : B** - **Priority Queueing (PQ)** peut laisser mourir les basses priorités (complete starvation).

---

### Q14 : Quel type de queueing garantit une allocation pondérée de bande passante ?
**A)** FIFO  
**B)** PQ  
**C)** WFQ (Weighted Fair Queueing)  
**D)** LIFO (Last-In-First-Out)  

**Réponse : C** - **WFQ** (Weighted Fair Queueing) alloue bande passante basée sur poids.

---

### Q15 : Quel est l'acronyme pour "Random Early Detection" ?
**A)** RED  
**B)** WRED  
**C)** RED (Random Early Detect)  
**D)** Tous sont corrects, WRED est extension  

**Réponse : D** - **RED** = version simple; **WRED** = version pondérée par classe (préférée).

---

### Q16 : Quel est le principal objectif de RED / WRED ?
**A)** Augmenter débit réseau  
**B)** Éviter congestion soudaine en signalant source (juste aléatoirement)  
**C)** Réduire latence  
**D)** Supprimer complètement perte paquet  

**Réponse : B** - **RED/WRED = signale source avant congestion complète** → source adapte taux.

---

### Q17 : Quel comando Cisco applique une politique QoS à une interface ?
**A)** `policy-map [name]`  
**B)** `service-policy [name]`  
**C)** `apply policy [name]`  
**D)** `qos-policy [name]`  

**Réponse : B** - **`service-policy input/output`** applique une politique sur interface.

---

### Q18 : Quel est la différence entre AF11, AF21, AF31, AF41 en DSCP ?
**A)** Aucune, tous équivalent  
**B)** Différentes plages de priorité et seuils de drop  
**C)** Seulement numénriques, pas de signification  
**D)** Dépend du fournisseur réseau  

**Réponse : B** - **AF** = Assured Forwarding; **AF11-AF13** basse prio, **AF41-AF43** haute prio.

---

### Q19 : Quel est l'impact de CoS sur le trafic traversant un routeur eBGP ?
**A)** CoS est préservé  
**B)** CoS est supprimé/remis à zéro  
**C)** CoS est remappé en DSCP  
**D)** Dépend de implémentation routeur  

**Réponse : B** - **CoS Layer 2** est supprimé traversant routeur → Besoin re-marquer en DSCP pour end-to-end.

---

### Q20 : Quel est l'avantage de CBQ (Class-Based Queueing) vs WFQ ?
**A)** CBQ est plus simple  
**B)** CBQ fournit garanties de bande passante explicites par classe  
**C)** CBQ réduit latence  
**D)** CBQ élimine perte paquet  

**Réponse : B** - **CBQ = garanties explicites** (ex: Voice = 100 Mbps garanti); **WFQ = pondéré seulement**.

---

## Questions 21-25

### Q21 : À quel moment le trafic doit-être marqué avec DSCP pour meilleur résultat ?
**A)** Au destination (hôte récifie)  
**B)** À l'edge du réseau (border router)  
**C)** Au cœur du réseau seulement  
**D)** Aucun marquage n'est nécessaire en DiffServ  

**Réponse : B** - **Marquer à l'edge** (routeur border) pour contrôle admission + consistance.

---

### Q22 : Quel paramètre QoS mesure variation de latence ?
**A)** Throughput  
**B)** Bandwidth  
**C)** Jitter (Gigue)  
**D)** MOS (Mean Opinion Score)  

**Réponse : C** - **Jitter = variation latence** (VoIP: < 30ms acceptable).

---

### Q23 : Quel est le seuil de perte de paquet acceptable pour VoIP ?
**A)** < 5%  
**B)** < 3%  
**C)** < 1%  
**D)** < 0.1%  

**Réponse : C** - **VoIP = < 1% perte** acceptable; Vidéo < 5% possible.

---

### Q24 : Quel est la capacité de MarqueUE d'un hôte envoyer du trafic avant police intervient ?
**A)** Rate spécifié même  
**B)** Rate + burst size  
**C)** Rate × burst time  
**D)** Aucune tolérance, strict enforcement  

**Réponse : B** - **Police = Rate + Burst (token bucket)**, tolérant un peu overflow du burst.

---

### Q25 : Quel est le vrai bénéfice de DiffServ sur IntServ ?
**A)** DiffServ garantit plus strictement  
**B)** DiffServ est plus simple et plus scalable (pas per-flow state)  
**C)** DiffServ support plus de trafic types  
**D)** DiffServ éliminer entièrement perte paquet  

**Réponse : B** - **DiffServ = scalable** (pas état per-flow), vs IntServ = complexe per-flow (RSVP).

