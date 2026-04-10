# QCM Module 2 : Spanning Tree Protocol
**CCNP ENCOR v8 - Protocole Spanning Tree**

---

## 📋 Instructions

- **Nombre de questions :** 25
- **Durée recommandée :** 40 minutes
- **Score minimum :** 70% (18/25)
- **Conseils :** Certaines questions peuvent avoir plusieurs réponses correctes

---

## Questions

### Question 1
Quel est le principal problème causé par une boucle Layer 2 dans un réseau commuté?

- [ ] A. Collisions excessives sur les liens
- [ ] B. Tempêtes de broadcast (broadcast storms)
- [ ] C. Fragmentation des paquets IP
- [ ] D. Augmentation du délai de routage

---

### Question 2
Quels sont les trois problèmes causés par les boucles Layer 2? (Choisissez trois réponses)

- [ ] A. Tempêtes de broadcast
- [ ] B. Instabilité de la table MAC (MAC flapping)
- [ ] C. Augmentation du TTL des paquets
- [ ] D. Trames dupliquées
- [ ] E. Corruption de la table ARP

---

### Question 3
Quel standard IEEE définit le Spanning Tree Protocol original?

- [ ] A. IEEE 802.1D
- [ ] B. IEEE 802.1w
- [ ] C. IEEE 802.1s
- [ ] D. IEEE 802.1Q

---

### Question 4
Quelle est la longueur totale du Bridge ID (BID)?

- [ ] A. 32 bits
- [ ] B. 48 bits
- [ ] C. 64 bits
- [ ] D. 128 bits

---

### Question 5
Quelle est la valeur de priorité par défaut d'un switch dans STP?

- [ ] A. 0
- [ ] B. 4096
- [ ] C. 24576
- [ ] D. 32768

---

### Question 6
Par quels incréments peut-on modifier la priorité de pont (bridge priority) dans STP?

- [ ] A. 1
- [ ] B. 16
- [ ] C. 256
- [ ] D. 4096

---

### Question 7
Comment est élu le Root Bridge dans STP?

- [ ] A. Switch avec la priorité la plus élevée
- [ ] B. Switch avec le Bridge ID le plus bas
- [ ] C. Switch avec le plus grand nombre de ports
- [ ] D. Switch avec l'adresse IP la plus basse

---

### Question 8
Si deux switches ont la même priorité de pont, quel critère détermine le Root Bridge?

- [ ] A. Nombre de ports actifs
- [ ] B. Adresse IP la plus basse
- [ ] C. Adresse MAC la plus basse
- [ ] D. Vitesse des liens

---

### Question 9
Quelle commande Cisco configure un switch comme Root Primary pour le VLAN 10?

- [ ] A. `spanning-tree vlan 10 priority 0`
- [ ] B. `spanning-tree vlan 10 root primary`
- [ ] C. `spanning-tree vlan 10 root-bridge`
- [ ] D. `spanning-tree vlan 10 set-root`

---

### Question 10
Quelle est la priorité configurée par la commande `spanning-tree vlan 10 root primary`?

- [ ] A. 0
- [ ] B. 4096
- [ ] C. 24576
- [ ] D. 28672

---

### Question 11
Combien de Root Ports un switch non-root peut-il avoir?

- [ ] A. Aucun
- [ ] B. Exactement un
- [ ] C. Un par VLAN
- [ ] D. Autant que de chemins vers le Root

---

### Question 12
Quel est le rôle d'un Designated Port dans STP?

- [ ] A. C'est le port avec le meilleur chemin vers le Root Bridge
- [ ] B. C'est le port qui forward le trafic sur un segment
- [ ] C. C'est le port bloqué pour éviter les boucles
- [ ] D. C'est le port administrativement désactivé

---

### Question 13
Quels types de ports sont en état Forwarding dans STP? (Choisissez deux réponses)

- [ ] A. Root Ports
- [ ] B. Designated Ports
- [ ] C. Alternate Ports
- [ ] D. Blocked Ports

---

### Question 14
Quel est le coût STP (short path cost) d'un lien Gigabit Ethernet?

- [ ] A. 2
- [ ] B. 4
- [ ] C. 10
- [ ] D. 19

---

### Question 15
Quel est le coût STP (short path cost) d'un lien Fast Ethernet (100 Mbps)?

- [ ] A. 4
- [ ] B. 10
- [ ] C. 19
- [ ] D. 100

---

### Question 16
Comment est calculé le Root Path Cost?

- [ ] A. Coût du port d'entrée uniquement
- [ ] B. Somme des coûts de tous les liens entre le switch et le Root Bridge
- [ ] C. Coût moyen de tous les chemins vers le Root
- [ ] D. Nombre de sauts (hops) vers le Root Bridge

---

### Question 17
Quels sont les critères de sélection du Root Port, dans l'ordre de priorité? (Choisissez quatre réponses et ordonnez-les)

- [ ] A. Root Path Cost le plus bas
- [ ] B. Sender Bridge ID le plus bas
- [ ] C. Vitesse du lien
- [ ] D. Sender Port ID le plus bas
- [ ] E. Local Port ID le plus bas
- [ ] F. MAC Address du switch local

---

### Question 18
Dans quel état un port STP ne forwarde PAS de trafic, mais apprend les adresses MAC?

- [ ] A. Blocking
- [ ] B. Listening
- [ ] C. Learning
- [ ] D. Forwarding

---

### Question 19
Quelle est la durée de l'état Listening dans STP 802.1D?

- [ ] A. 2 secondes
- [ ] B. 15 secondes
- [ ] C. 20 secondes
- [ ] D. 30 secondes

---

### Question 20
Quel est le temps total de convergence minimum pour qu'un port passe de Blocking à Forwarding dans STP 802.1D?

- [ ] A. 15 secondes
- [ ] B. 20 secondes
- [ ] C. 30 secondes
- [ ] D. 50 secondes

---

### Question 21
Quelle est la fréquence d'envoi des BPDUs par le Root Bridge (Hello Time par défaut)?

- [ ] A. 1 seconde
- [ ] B. 2 secondes
- [ ] C. 10 secondes
- [ ] D. 15 secondes

---

### Question 22
Quelle est la valeur par défaut du timer Max Age dans STP?

- [ ] A. 2 secondes
- [ ] B. 10 secondes
- [ ] C. 15 secondes
- [ ] D. 20 secondes

---

### Question 23
Sur quel switch faut-il configurer les timers STP (Hello Time, Forward Delay, Max Age)?

- [ ] A. Sur tous les switches du réseau
- [ ] B. Sur le Root Bridge uniquement
- [ ] C. Sur les switches de distribution uniquement
- [ ] D. Sur les switches d'accès uniquement

---

### Question 24
Quelle variante de STP crée une instance STP par VLAN et supporte le trunking 802.1Q?

- [ ] A. STP (802.1D)
- [ ] B. PVST
- [ ] C. PVST+
- [ ] D. MSTP

---

### Question 25
Quelle commande affiche l'état du Root Bridge pour tous les VLANs?

- [ ] A. `show spanning-tree`
- [ ] B. `show spanning-tree root`
- [ ] C. `show spanning-tree summary`
- [ ] D. `show root bridge`

---

## ✅ Grille de réponses

| Q1 | Q2 | Q3 | Q4 | Q5 | Q6 | Q7 | Q8 | Q9 | Q10 |
|----|----|----|----|----|----|----|----|----|----|
| ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

| Q11 | Q12 | Q13 | Q14 | Q15 | Q16 | Q17 | Q18 | Q19 | Q20 |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

| Q21 | Q22 | Q23 | Q24 | Q25 |
|-----|-----|-----|-----|-----|
| ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

---

## 📝 Corrigé

### Question 1 : **B**
**Réponse correcte :** B. Tempêtes de broadcast (broadcast storms)

**Explication :** Les boucles Layer 2 causent principalement des tempêtes de broadcast où les trames broadcast sont propagées indéfiniment, saturant complètement le réseau en quelques secondes. Les collisions (A) sont liées aux hubs et au half-duplex, pas aux boucles. La fragmentation IP (C) et le délai de routage (D) sont des concepts de Layer 3.

---

### Question 2 : **A, B, D**
**Réponses correctes :** 
- A. Tempêtes de broadcast
- B. Instabilité de la table MAC (MAC flapping)
- D. Trames dupliquées

**Explication :** Les trois problèmes principaux des boucles L2 sont :
1. **Broadcast storms** : propagation infinie des broadcasts
2. **MAC flapping** : une même MAC apprise sur plusieurs ports
3. **Trames dupliquées** : réception multiple de la même trame

Le TTL (C) est un concept Layer 3, et la table ARP (E) n'est pas directement corrompue par les boucles L2.

---

### Question 3 : **A**
**Réponse correcte :** A. IEEE 802.1D

**Explication :** Le standard **IEEE 802.1D** définit le Spanning Tree Protocol original publié en 1990. Les autres standards sont :
- **802.1w** : Rapid Spanning Tree Protocol (RSTP)
- **802.1s** : Multiple Spanning Tree Protocol (MSTP)
- **802.1Q** : VLAN Trunking Protocol (pas STP)

---

### Question 4 : **C**
**Réponse correcte :** C. 64 bits

**Explication :** Le Bridge ID est composé de :
- **16 bits** : Bridge Priority (4 bits) + Extended System ID (12 bits)
- **48 bits** : Adresse MAC
- **Total : 64 bits (8 octets)**

---

### Question 5 : **D**
**Réponse correcte :** D. 32768

**Explication :** La priorité par défaut dans STP est **32768** pour tous les switches Cisco. Dans PVST+, cette valeur est augmentée du VLAN ID (Extended System ID). Par exemple, pour VLAN 10 : 32768 + 10 = 32778.

---

### Question 6 : **D**
**Réponse correcte :** D. 4096

**Explication :** La priorité de pont peut uniquement être modifiée par **incréments de 4096** (0, 4096, 8192, 16384, 24576, 32768, 40960, 49152, 57344, 61440). Ceci est dû au fait que seuls les 4 bits de poids fort sont utilisés pour la priorité configurable, les 12 bits restants étant réservés pour l'Extended System ID (VLAN ID).

---

### Question 7 : **B**
**Réponse correcte :** B. Switch avec le Bridge ID le plus bas

**Explication :** Le Root Bridge est élu en comparant les Bridge IDs (BID) de tous les switches. Le switch avec le **BID le plus bas** devient Root. Le BID est d'abord comparé par priorité, puis par adresse MAC si les priorités sont identiques.

---

### Question 8 : **C**
**Réponse correcte :** C. Adresse MAC la plus basse

**Explication :** Si deux switches ont la même priorité de pont (Bridge Priority), c'est l'**adresse MAC la plus basse** qui détermine le Root Bridge. Le BID est comparé dans l'ordre : Priority d'abord, puis MAC Address.

---

### Question 9 : **B**
**Réponse correcte :** B. `spanning-tree vlan 10 root primary`

**Explication :** La commande **`spanning-tree vlan 10 root primary`** configure le switch comme Root Primary pour le VLAN 10. Cisco définit automatiquement la priorité à 24576 (ou 4096 de moins que le Root actuel si celui-ci a une priorité inférieure à 24576). Bien que `spanning-tree vlan 10 priority 0` (A) fonctionnerait, ce n'est pas la méthode recommandée par Cisco.

---

### Question 10 : **C**
**Réponse correcte :** C. 24576

**Explication :** La commande `spanning-tree vlan 10 root primary` configure la priorité à **24576** (ou 4096 de moins que le Root actuel si sa priorité est < 24576). La commande `root secondary` configure la priorité à 28672.

---

### Question 11 : **B**
**Réponse correcte :** B. Exactement un

**Explication :** Un switch non-root a **exactement un Root Port** par instance STP. Cette règle s'applique individuellement à chaque VLAN dans PVST+. Le Root Port est le port avec le meilleur chemin vers le Root Bridge. Le Root Bridge lui-même n'a aucun Root Port.

---

### Question 12 : **B**
**Réponse correcte :** B. C'est le port qui forward le trafic sur un segment

**Explication :** Un **Designated Port (DP)** est le port qui forwarde le trafic sur un segment particulier. Il y a un DP par segment de réseau. Le DP est responsable d'envoyer les BPDUs sur ce segment. Le port avec le meilleur chemin vers le Root (A) est le Root Port. Les ports bloqués (C) sont les Alternate Ports.

---

### Question 13 : **A, B**
**Réponses correctes :**
- A. Root Ports
- B. Designated Ports

**Explication :** Seuls les **Root Ports (RP)** et **Designated Ports (DP)** sont en état **Forwarding**. Les **Alternate Ports** et **Blocked Ports** sont en état **Blocking** (802.1D) ou **Discarding** (802.1w) et ne forwardent pas de trafic.

---

### Question 14 : **B**
**Réponse correcte :** B. 4

**Explication :** Le coût STP (short path cost, 802.1D) d'un lien **Gigabit Ethernet (1 Gbps)** est **4**. Tableau complet :
- 10 Mbps = 100
- 100 Mbps (Fast Ethernet) = 19
- 1 Gbps (Gigabit Ethernet) = 4
- 10 Gbps = 2

---

### Question 15 : **C**
**Réponse correcte :** C. 19

**Explication :** Le coût STP (short path cost) d'un lien **Fast Ethernet (100 Mbps)** est **19**. Il est important de mémoriser ce coût car il est encore utilisé dans de nombreux réseaux legacy.

---

### Question 16 : **B**
**Réponse correcte :** B. Somme des coûts de tous les liens entre le switch et le Root Bridge

**Explication :** Le **Root Path Cost** est la **somme cumulative** des coûts de tous les liens sur le chemin depuis le switch jusqu'au Root Bridge. Chaque switch **ajoute** le coût du port d'**entrée** au Root Path Cost reçu dans le BPDU. Exemple : Root (0) → SW1 via 1G (coût 4) → SW2 via 1G (coût 4) = Root Path Cost de SW2 = 8.

---

### Question 17 : **A, B, D, E (dans cet ordre)**
**Réponses correctes (ordre de priorité) :**
1. A. Root Path Cost le plus bas
2. B. Sender Bridge ID le plus bas
3. D. Sender Port ID le plus bas
4. E. Local Port ID le plus bas

**Explication :** L'ordre de sélection du Root Port est critique pour l'examen. Les critères sont évalués dans cet ordre jusqu'à ce qu'un seul port soit sélectionné :
1. **Root Path Cost** : Le port avec le coût le plus bas vers le Root
2. **Sender Bridge ID** : Si égalité, l'ID du switch voisin le plus bas
3. **Sender Port ID** : Si égalité, le port d'envoi du voisin le plus bas
4. **Local Port ID** : En dernier recours, le port local le plus bas

La vitesse du lien (C) n'est pas un critère direct (elle influence le coût). La MAC locale (F) fait partie du BID mais n'est pas un critère séparé.

---

### Question 18 : **C**
**Réponse correcte :** C. Learning

**Explication :** Dans l'état **Learning**, le port :
- ❌ Ne forwarde PAS de trafic
- ✅ Apprend les adresses MAC (remplit la table MAC)
- ✅ Envoie et reçoit des BPDUs

Dans l'état **Blocking**, le port n'apprend pas les MACs. Dans **Listening**, le port ne forwarde pas et n'apprend pas non plus. Dans **Forwarding**, le port fait tout (forward + apprendre).

---

### Question 19 : **B**
**Réponse correcte :** B. 15 secondes

**Explication :** L'état **Listening** dure **15 secondes**, correspondant au timer **Forward Delay**. Pendant cette période, le port participe à l'élection STP (envoi/réception de BPDUs) mais ne forwarde pas de trafic et n'apprend pas d'adresses MAC.

---

### Question 20 : **C**
**Réponse correcte :** C. 30 secondes

**Explication :** Le temps total minimum de convergence dans STP 802.1D est de **30 secondes** :
- **Listening** : 15 secondes (Forward Delay)
- **Learning** : 15 secondes (Forward Delay)
- **Total** : 30 secondes

En pratique, la convergence peut prendre jusqu'à 50 secondes si on compte le Max Age (20s) pour détecter une panne. C'est pourquoi RSTP (convergence ~1-2s) est préféré.

---

### Question 21 : **B**
**Réponse correcte :** B. 2 secondes

**Explication :** Le **Hello Time** par défaut est de **2 secondes**. Le Root Bridge génère et envoie des Configuration BPDUs toutes les 2 secondes. Les autres switches relaient ces BPDUs sur leurs Designated Ports. Ce timer peut être modifié (plage 1-10s) uniquement sur le Root Bridge.

---

### Question 22 : **D**
**Réponse correcte :** D. 20 secondes

**Explication :** Le **Max Age** par défaut est de **20 secondes**. Il s'agit de la durée maximale pendant laquelle un BPDU est considéré valide. Si un switch ne reçoit pas de BPDU du Root pendant 20 secondes, il considère que le Root est perdu et redémarre le processus d'élection.

---

### Question 23 : **B**
**Réponse correcte :** B. Sur le Root Bridge uniquement

**Explication :** Les timers STP (Hello Time, Forward Delay, Max Age) doivent être configurés **uniquement sur le Root Bridge**. Le Root Bridge génère les BPDUs originaux contenant ces timers, et tous les autres switches utilisent les valeurs reçues dans les BPDUs. Si vous configurez les timers sur un switch non-root, ils seront ignorés.

---

### Question 24 : **C**
**Réponse correcte :** C. PVST+

**Explication :** **PVST+ (Per-VLAN Spanning Tree Plus)** est une variante Cisco proprietary qui :
- Crée une instance STP par VLAN
- Supporte le trunking **802.1Q** (standard)
- Permet le load-balancing entre VLANs

**PVST** (B) utilise ISL (obsolète). **STP 802.1D** (A) a une seule instance pour tous les VLANs (CST). **MSTP** (D) regroupe plusieurs VLANs dans une instance.

---

### Question 25 : **B**
**Réponse correcte :** B. `show spanning-tree root`

**Explication :** La commande **`show spanning-tree root`** affiche un résumé du Root Bridge pour tous les VLANs, incluant le Root ID, le Root Path Cost, et le Root Port. Output exemple :
```
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0010         24586 0ce3.e11a.ba00        4     2   20  15  Gi0/1
```

`show spanning-tree` (A) affiche l'état complet de STP mais est plus verbeux. `show spanning-tree summary` (C) affiche un résumé de configuration, pas les Root Bridges.

---

## 📊 Scoring

| Score | Niveau |
|-------|--------|
| 23-25 (92-100%) | 🌟 Excellent - Maîtrise parfaite de STP |
| 20-22 (80-88%) | ✅ Très bien - Bonne compréhension |
| 18-19 (72-76%) | ✅ Bien - Niveau suffisant |
| 15-17 (60-68%) | ⚠️ Moyen - Réviser les concepts clés |
| < 15 (< 60%) | ❌ Insuffisant - Révision complète nécessaire |

---

## 🎯 Thèmes à réviser selon vos erreurs

**Questions 1-3 :** Problèmes de redondance L2 et standards STP  
**Questions 4-10 :** Bridge ID, priorité, élection du Root Bridge  
**Questions 11-13 :** Rôles des ports STP  
**Questions 14-17 :** Path Cost et sélection du Root Port  
**Questions 18-20 :** États des ports et convergence  
**Questions 21-23 :** Timers STP et configuration  
**Questions 24-25 :** Variantes STP et vérification

---

**📚 Fin du QCM - Module 2 : Spanning Tree Protocol**
