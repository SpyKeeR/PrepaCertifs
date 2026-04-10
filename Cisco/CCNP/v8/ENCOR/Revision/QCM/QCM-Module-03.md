# QCM Module 3 : Advanced Spanning Tree Tuning
**CCNP ENCOR v8 - Optimisation avancée du Spanning Tree**

---

## 📋 Instructions

- **Nombre de questions :** 25
- **Durée recommandée :** 40 minutes
- **Score minimum :** 70% (18/25)
- **Conseils :** Certaines questions peuvent avoir plusieurs réponses correctes

---

## Questions

### Question 1
Quel est le principal objectif de PortFast?

- [ ] A. Bloquer les BPDUs indésirables
- [ ] B. Permettre à un port d'accéder immédiatement à l'état Forwarding
- [ ] C. Empêcher un switch de devenir Root Bridge
- [ ] D. Réduire le nombre de BPDUs envoyés

---

### Question 2
Sur quels types de ports PortFast doit-il être activé? (Choisissez deux réponses)

- [ ] A. Ports connectés à des PC
- [ ] B. Ports connectés à des serveurs
- [ ] C. Ports trunk vers d'autres switches
- [ ] D. Liaisons inter-switch

---

### Question 3
Quelle commande active PortFast globalement sur tous les ports en mode access?

- [ ] A. `portfast enable`
- [ ] B. `spanning-tree portfast`
- [ ] C. `spanning-tree portfast default`
- [ ] D. `spanning-tree portfast enable`

---

### Question 4
Que se passe-t-il si PortFast est activé par erreur sur un port trunk connectant deux switches?

- [ ] A. Aucun problème, STP gère automatiquement
- [ ] B. Création temporaire d'une boucle Layer 2 avant convergence STP
- [ ] C. Le port est immédiatement mis en err-disabled
- [ ] D. Les VLANs sont automatiquement bloqués

---

### Question 5
Quelle est l'action de BPDU Guard lorsqu'un BPDU est reçu sur un port?

- [ ] A. Ignore le BPDU
- [ ] B. Met le port en état Blocking
- [ ] C. Met le port en état err-disabled
- [ ] D. Envoie une alerte SNMP uniquement

---

### Question 6
Quelle commande active BPDU Guard globalement sur tous les ports PortFast?

- [ ] A. `spanning-tree bpduguard enable`
- [ ] B. `spanning-tree portfast bpduguard`
- [ ] C. `spanning-tree portfast bpduguard default`
- [ ] D. `bpduguard default`

---

### Question 7
Comment récupérer manuellement un port en état err-disabled à cause de BPDU Guard?

- [ ] A. `clear interface gi0/5`
- [ ] B. `no spanning-tree bpduguard`
- [ ] C. `shutdown` puis `no shutdown`
- [ ] D. `spanning-tree portfast disable` puis `enable`

---

### Question 8
Quelle commande active la récupération automatique des ports err-disabled par BPDU Guard?

- [ ] A. `errdisable auto-recovery bpduguard`
- [ ] B. `errdisable recovery cause bpduguard`
- [ ] C. `spanning-tree bpduguard recovery`
- [ ] D. `auto-recovery bpduguard enable`

---

### Question 9
Quelle est la différence principale entre BPDU Guard et BPDU Filter?

- [ ] A. BPDU Guard bloque le port, BPDU Filter ignore les BPDUs
- [ ] B. BPDU Guard ignore les BPDUs, BPDU Filter bloque le port
- [ ] C. Il n'y a aucune différence, ce sont des alias
- [ ] D. BPDU Filter est plus sécurisé que BPDU Guard

---

### Question 10
Quel est le comportement de BPDU Filter configuré en mode global (spanning-tree portfast bpdufilter default)?

- [ ] A. Ignore définitivement tous les BPDUs
- [ ] B. Se désactive automatiquement si un BPDU est reçu
- [ ] C. Met le port en err-disabled si un BPDU est reçu
- [ ] D. Bloque uniquement l'envoi de BPDUs

---

### Question 11
Quel est le risque principal d'activer BPDU Filter en mode interface (spanning-tree bpdufilter enable)?

- [ ] A. Performance réseau dégradée
- [ ] B. Création de boucles Layer 2
- [ ] C. Perte de connectivité temporaire
- [ ] D. Incompatibilité avec PVST+

---

### Question 12
Quel est l'objectif principal de Root Guard?

- [ ] A. Empêcher un port de recevoir des BPDUs
- [ ] B. Empêcher un port de devenir Root Port
- [ ] C. Protéger le Root Bridge contre les pannes
- [ ] D. Accélérer la convergence STP

---

### Question 13
Sur quels types de ports Root Guard doit-il être configuré?

- [ ] A. Root Ports
- [ ] B. Alternate Ports
- [ ] C. Designated Ports pointant vers la périphérie
- [ ] D. Tous les ports du Root Bridge

---

### Question 14
Quel est l'état d'un port lorsque Root Guard est déclenché?

- [ ] A. err-disabled
- [ ] B. Blocking
- [ ] C. root-inconsistent
- [ ] D. loop-inconsistent

---

### Question 15
La récupération d'un port en état root-inconsistent est-elle automatique ou manuelle?

- [ ] A. Automatique dès que les BPDUs indésirables cessent
- [ ] B. Manuelle uniquement
- [ ] C. Automatique après 300 secondes
- [ ] D. Nécessite un redémarrage du switch

---

### Question 16
Quel est l'objectif principal de Loop Guard?

- [ ] A. Empêcher un switch de devenir Root Bridge
- [ ] B. Prévenir les boucles causées par une perte unidirectionnelle de BPDUs
- [ ] C. Bloquer les BPDUs indésirables
- [ ] D. Accélérer la convergence en cas de panne

---

### Question 17
Sur quels types de ports Loop Guard est-il typiquement activé?

- [ ] A. Designated Ports
- [ ] B. Root Ports
- [ ] C. Alternate/Blocked Ports
- [ ] D. Ports en mode access avec PortFast

---

### Question 18
Quelle commande active Loop Guard globalement sur tous les ports point-to-point non-PortFast?

- [ ] A. `spanning-tree loopguard enable`
- [ ] B. `spanning-tree guard loop`
- [ ] C. `spanning-tree loopguard default`
- [ ] D. `loopguard global`

---

### Question 19
Quel est l'état d'un port lorsque Loop Guard est déclenché?

- [ ] A. err-disabled
- [ ] B. root-inconsistent
- [ ] C. loop-inconsistent
- [ ] D. Blocking

---

### Question 20
Quelle fonctionnalité permet une convergence quasi-instantanée (~1s) lorsque le Root Port d'un switch d'accès tombe?

- [ ] A. BackboneFast
- [ ] B. PortFast
- [ ] C. UplinkFast
- [ ] D. Root Guard

---

### Question 21
Quels sont les effets automatiques de la commande `spanning-tree uplinkfast`? (Choisissez deux réponses)

- [ ] A. Augmente la Bridge Priority à 49152
- [ ] B. Diminue la Bridge Priority à 4096
- [ ] C. Augmente le Path Cost de tous les ports de 3000
- [ ] D. Active PortFast sur tous les ports

---

### Question 22
Sur quels types de switches UplinkFast doit-il être activé?

- [ ] A. Root Bridge
- [ ] B. Switches Core
- [ ] C. Switches d'accès avec deux uplinks
- [ ] D. Switches de distribution

---

### Question 23
Quel est le gain de temps apporté par BackboneFast en cas de panne indirecte?

- [ ] A. 10 secondes
- [ ] B. 15 secondes
- [ ] C. 20 secondes (bypass du Max Age)
- [ ] D. 30 secondes

---

### Question 24
Quelle est la contrainte mathématique entre Max Age et Hello Time dans STP?

- [ ] A. Max Age ≤ Hello Time × 2
- [ ] B. Max Age ≥ 2 × (Hello Time + 1)
- [ ] C. Max Age = Hello Time × 10
- [ ] D. Max Age ≥ Hello Time + 5

---

### Question 25
Pourquoi UplinkFast et BackboneFast sont-ils considérés comme obsolètes dans les réseaux modernes?

- [ ] A. Ils ne fonctionnent pas avec les VLANs
- [ ] B. Ils sont incompatibles avec 802.1Q
- [ ] C. Rapid-PVST+ (RSTP) converge naturellement aussi vite sans leurs limitations
- [ ] D. Ils consomment trop de ressources CPU

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
**Réponse correcte :** B. Permettre à un port d'accéder immédiatement à l'état Forwarding

**Explication :** PortFast permet à un port de contourner les états Listening (15s) et Learning (15s) pour passer directement de Blocking à Forwarding. Cela élimine l'attente de 30-50 secondes habituelle. Cette fonctionnalité est essentielle pour les ports d'accès connectés à des hôtes finaux (PC, serveurs) qui ont besoin d'une connectivité immédiate au démarrage (par exemple pour obtenir une adresse DHCP ou effectuer un PXE boot).

---

### Question 2 : **A, B**
**Réponses correctes :**
- A. Ports connectés à des PC
- B. Ports connectés à des serveurs

**Explication :** PortFast doit être activé **uniquement** sur les ports connectés à des **hôtes finaux** (end devices) tels que PC, serveurs, imprimantes, téléphones IP. Ces périphériques ne génèrent pas de BPDUs et ne peuvent pas créer de boucles. **Ne JAMAIS** activer PortFast sur des ports trunk (C) ou des liaisons inter-switch (D), car cela créerait une boucle temporaire avant que STP ne reconverge.

---

### Question 3 : **C**
**Réponse correcte :** C. `spanning-tree portfast default`

**Explication :** La commande **`spanning-tree portfast default`** active PortFast globalement sur **tous les ports configurés en mode access**. Cette approche est recommandée car elle garantit que tous les ports d'accès bénéficient de PortFast sans configuration individuelle. Note : `spanning-tree portfast` (B) s'applique uniquement à l'interface en cours de configuration, pas globalement.

---

### Question 4 : **B**
**Réponse correcte :** B. Création temporaire d'une boucle Layer 2 avant convergence STP

**Explication :** Si PortFast est activé sur un port trunk ou une liaison inter-switch, le port passe immédiatement en Forwarding sans attendre la convergence STP. Si le switch distant fait de même, **une boucle Layer 2 se forme** momentanément, causant une tempête de broadcast jusqu'à ce que STP détecte et bloque un port (après 30-50 secondes). Cela peut saturer complètement le réseau pendant ce temps. C'est pourquoi PortFast ne doit JAMAIS être utilisé sur des liens inter-switch.

---

### Question 5 : **C**
**Réponse correcte :** C. Met le port en état err-disabled

**Explication :** **BPDU Guard** est un mécanisme de sécurité qui place immédiatement un port en état **err-disabled** dès qu'il reçoit un BPDU. Le raisonnement : si PortFast est activé, le port est censé être connecté à un hôte final qui n'envoie jamais de BPDUs. Si un BPDU est reçu, cela indique qu'un switch (potentiellement indésirable/rogue) a été connecté. Le port est désactivé pour protéger le réseau, et une alerte est générée.

---

### Question 6 : **C**
**Réponse correcte :** C. `spanning-tree portfast bpduguard default`

**Explication :** La commande **`spanning-tree portfast bpduguard default`** active BPDU Guard globalement sur **tous les ports où PortFast est activé** (soit par configuration individuelle, soit via `spanning-tree portfast default`). C'est la méthode recommandée pour protéger automatiquement tous les ports d'accès contre les connexions inattendues de switches.

---

### Question 7 : **C**
**Réponse correcte :** C. `shutdown` puis `no shutdown`

**Explication :** Pour récupérer manuellement un port en état **err-disabled**, il faut d'abord **arrêter** le port avec `shutdown`, puis le **réactiver** avec `no shutdown`. Cette séquence force le switch à réinitialiser l'état du port. Avant de le faire, il est essentiel de résoudre le problème sous-jacent (déconnecter le switch indésirable, par exemple), sinon le port sera immédiatement remis en err-disabled.

---

### Question 8 : **B**
**Réponse correcte :** B. `errdisable recovery cause bpduguard`

**Explication :** La commande **`errdisable recovery cause bpduguard`** active la récupération automatique pour les ports mis en err-disabled par BPDU Guard. Par défaut, la récupération se fait après **300 secondes** (modifiable avec `errdisable recovery interval`). **Attention :** Si le problème persiste (switch indésirable toujours connecté), le port sera remis en err-disabled après récupération, créant un cycle.

---

### Question 9 : **A**
**Réponse correcte :** A. BPDU Guard bloque le port, BPDU Filter ignore les BPDUs

**Explication :** 
- **BPDU Guard** : Si un BPDU est reçu → Port en **err-disabled** (action drastique, sécuritaire)
- **BPDU Filter** : Si un BPDU est reçu → **Ignore** le BPDU (pas de blocage, plus permissif)

BPDU Guard est un mécanisme de **sécurité** (empêche les connexions indésirables). BPDU Filter est plus permissif et **dangereux** (peut créer des boucles si mal utilisé). Dans 99% des cas, **BPDU Guard est la solution appropriée**.

---

### Question 10 : **B**
**Réponse correcte :** B. Se désactive automatiquement si un BPDU est reçu

**Explication :** En mode **global** (`spanning-tree portfast bpdufilter default`), BPDU Filter a un comportement "intelligent" :
- Le port **arrête d'envoyer des BPDUs** tant qu'il ne reçoit aucun BPDU
- **Si un BPDU est reçu**, BPDU Filter se **désactive automatiquement** et STP reprend le contrôle normal
- Ce mécanisme offre une protection : si un switch est connecté, STP peut fonctionner normalement

C'est différent du mode interface où BPDU Filter est permanent (plus dangereux).

---

### Question 11 : **B**
**Réponse correcte :** B. Création de boucles Layer 2

**Explication :** BPDU Filter en mode **interface** (`spanning-tree bpdufilter enable`) désactive **complètement STP** sur le port :
- Le port n'envoie ni ne reçoit de BPDUs
- Même si un switch est connecté et envoie des BPDUs, ils sont **ignorés**
- Si deux switches sont connectés de façon redondante et BPDU Filter est actif, **une boucle Layer 2 se forme**
- Résultat : Tempête de broadcast, saturation du réseau

**Règle d'or :** Ne JAMAIS utiliser BPDU Filter en mode interface sauf cas ultra-spécifique et maîtrisé.

---

### Question 12 : **B**
**Réponse correcte :** B. Empêcher un port de devenir Root Port

**Explication :** **Root Guard** protège la hiérarchie du Root Bridge en empêchant un port de devenir **Root Port**. Si un port avec Root Guard reçoit un BPDU annonçant un Bridge ID **inférieur** au Root actuel (indiquant qu'un "meilleur" Root existe de ce côté), Root Guard bloque le port au lieu de le faire devenir Root Port. Cela empêche un switch périphérique de prendre le contrôle de la topologie STP et de devenir le nouveau Root Bridge.

---

### Question 13 : **C**
**Réponse correcte :** C. Designated Ports pointant vers la périphérie

**Explication :** Root Guard doit être configuré sur les **Designated Ports** qui pointent **vers la périphérie** du réseau (de la distribution vers l'accès, du core vers la distribution). Ces ports ne doivent **jamais** devenir Root Ports car cela indiquerait qu'un chemin vers le Root existe en aval (anormal). Root Guard garantit que le Root Bridge reste au niveau souhaité (typiquement le Core).

---

### Question 14 : **C**
**Réponse correcte :** C. root-inconsistent

**Explication :** Lorsque Root Guard est déclenché, le port est placé en état **root-inconsistent**. Dans cet état, le port est **bloqué** (similaire à Blocking) et ne forwarde pas de trafic. Cet état est temporaire : dès que les BPDUs "supérieurs" (annonçant un BID plus bas) cessent d'être reçus, le port **récupère automatiquement** et repasse en Forwarding.

Contrairement à **err-disabled** (qui nécessite une intervention manuelle), root-inconsistent se résout automatiquement.

---

### Question 15 : **A**
**Réponse correcte :** A. Automatique dès que les BPDUs indésirables cessent

**Explication :** La récupération d'un port en état **root-inconsistent** est **automatique**. Dès que le switch cesse de recevoir des BPDUs annonçant un Bridge ID inférieur au Root actuel (par exemple, le switch indésirable est déconnecté ou sa priorité est augmentée), le port repasse automatiquement à son état STP normal (généralement Designated/Forwarding). Aucune intervention manuelle n'est nécessaire, contrairement à BPDU Guard (err-disabled).

---

### Question 16 : **B**
**Réponse correcte :** B. Prévenir les boucles causées par une perte unidirectionnelle de BPDUs

**Explication :** **Loop Guard** protège contre une situation spécifique : un lien qui perd la capacité de transmettre des BPDUs dans **une direction** (lien unidirectionnel) tout en restant physiquement up. Causes possibles : SFP défectueux, problème de câblage, bug logiciel. 

Sans Loop Guard :
- Un port Alternate/Blocked cesse de recevoir des BPDUs
- Après Max Age (20s), il passe en Designated/Forwarding
- **Boucle Layer 2** créée

Avec Loop Guard :
- Le port est immédiatement placé en **loop-inconsistent** (bloqué)
- Pas de boucle
- Récupération auto dès réception de BPDUs

---

### Question 17 : **C**
**Réponse correcte :** C. Alternate/Blocked Ports

**Explication :** Loop Guard est typiquement activé sur les **ports Alternate/Blocked** (ports de backup, non-utilisés). Ces ports sont en état Blocking car ils reçoivent des BPDUs "supérieurs". Si ces BPDUs cessent d'arriver (perte unidirectionnelle), le port pourrait passer en Forwarding et créer une boucle. Loop Guard empêche cela en plaçant le port en loop-inconsistent.

En pratique, Loop Guard est souvent activé **globalement** (`spanning-tree loopguard default`) pour protéger automatiquement tous les ports point-to-point non-PortFast.

---

### Question 18 : **C**
**Réponse correcte :** C. `spanning-tree loopguard default`

**Explication :** La commande **`spanning-tree loopguard default`** active Loop Guard **globalement** sur tous les ports :
- **Point-to-point** (liaisons switch-to-switch)
- **Non-PortFast** (pas des ports d'accès)

C'est la méthode **recommandée** car elle protège automatiquement tous les liens inter-switch sans configuration individuelle. Loop Guard ne s'applique pas aux ports d'accès avec PortFast actif.

---

### Question 19 : **C**
**Réponse correcte :** C. loop-inconsistent

**Explication :** Lorsque Loop Guard est déclenché (un port Alternate/Blocked cesse de recevoir des BPDUs), le port est placé en état **loop-inconsistent**. Dans cet état :
- Le port est **bloqué** (ne forwarde pas de trafic)
- Le port reste dans cet état jusqu'à ce que les BPDUs soient à nouveau reçus
- Récupération **automatique** dès réception de BPDUs

Distinction :
- **root-inconsistent** = Root Guard
- **loop-inconsistent** = Loop Guard
- **err-disabled** = BPDU Guard

---

### Question 20 : **C**
**Réponse correcte :** C. UplinkFast

**Explication :** **UplinkFast** permet une convergence **quasi-instantanée** (~1 seconde) lorsque le Root Port d'un switch d'accès tombe. Le switch maintient une liste de ports Alternate (backup uplinks) et active immédiatement l'un d'eux lorsque le Root Port tombe, en contournant les états Listening et Learning.

Comparaison :
- **Sans UplinkFast** : Convergence ~30-50 secondes
- **Avec UplinkFast** : Convergence ~1 seconde

**BackboneFast** (A) accélère la convergence en cas de panne indirecte, mais seulement de 50s à 30s. **PortFast** (B) est pour les ports d'accès vers hôtes. **Root Guard** (D) est une protection, pas une accélération.

---

### Question 21 : **A, C**
**Réponses correctes :**
- A. Augmente la Bridge Priority à 49152
- C. Augmente le Path Cost de tous les ports de 3000

**Explication :** La commande `spanning-tree uplinkfast` a deux effets automatiques :

1. **Bridge Priority augmentée à 49152** : Empêche ce switch de devenir Root Bridge (49152 est bien plus haut que les valeurs typiques 24576-32768)

2. **Path Cost augmenté de 3000 sur tous les ports** : Fait en sorte que ce switch ne devienne pas un chemin préféré pour d'autres switches

Ces modifications garantissent qu'UplinkFast n'est utilisé que sur des switches d'accès en position "feuille" dans la topologie, jamais sur des switches de distribution ou core.

---

### Question 22 : **C**
**Réponse correcte :** C. Switches d'accès avec deux uplinks

**Explication :** UplinkFast est conçu **spécifiquement** pour les **switches d'accès** ayant **exactement deux uplinks** vers la couche distribution :
- Un uplink actif (Root Port)
- Un uplink de backup (Alternate Port)

**Ne PAS utiliser UplinkFast sur :**
- **Root Bridge** (A) : N'a pas de Root Port
- **Switches Core** (B) : Topologie trop complexe
- **Switches de distribution** (D) : Peut perturber la topologie

UplinkFast modifie la Bridge Priority et les Path Costs, ce qui n'est acceptable que pour des switches en position périphérique.

---

### Question 23 : **C**
**Réponse correcte :** C. 20 secondes (bypass du Max Age)

**Explication :** **BackboneFast** réduit le temps de convergence en cas de panne **indirecte** (dans le backbone, pas directement connectée) :

**Sans BackboneFast :**
- Max Age : 20 secondes (attente expiration BPDU)
- Listening : 15 secondes
- Learning : 15 secondes
- **Total : 50 secondes**

**Avec BackboneFast :**
- Max Age : **bypassé** (requête RLQ pour confirmation immédiate)
- Listening : 15 secondes
- Learning : 15 secondes
- **Total : 30 secondes**

**Gain : 20 secondes** (le Max Age est éliminé).

---

### Question 24 : **B**
**Réponse correcte :** B. Max Age ≥ 2 × (Hello Time + 1)

**Explication :** IEEE 802.1D impose deux contraintes mathématiques pour garantir la stabilité de STP :

1. **Max Age ≥ 2 × (Hello Time + 1)**
2. **Max Age ≤ 2 × (Forward Delay - 1)**

Ces formules assurent que :
- Le Max Age est suffisamment long pour tolérer quelques pertes de BPDUs
- Mais pas trop long pour ralentir la détection de pannes

**Exemple de vérification avec les valeurs par défaut (Hello=2, ForwardDelay=15, MaxAge=20) :**
```
20 ≥ 2 × (2 + 1) = 6  ✅
20 ≤ 2 × (15 - 1) = 28 ✅
```

---

### Question 25 : **C**
**Réponse correcte :** C. Rapid-PVST+ (RSTP) converge naturellement aussi vite sans leurs limitations

**Explication :** **UplinkFast** et **BackboneFast** sont considérés comme **obsolètes** dans les réseaux modernes car :

**Rapid-PVST+ (RSTP 802.1w) :**
- Converge naturellement en **1-2 secondes** pour tous types de pannes (directes et indirectes)
- Pas besoin de fonctionnalités spéciales comme UplinkFast/BackboneFast
- Ne modifie pas la Bridge Priority ni les Path Costs (pas de limitations)
- Fonctionne sur tous les types de switches (pas limité à l'accès)

**Limitations UplinkFast/BackboneFast :**
- UplinkFast : Augmente Priority à 49152, uniquement pour switches d'accès
- BackboneFast : Réduit seulement de 50s à 30s (RSTP fait mieux : 1-2s)
- Compatibilité limitée

**Recommandation moderne :** Toujours utiliser **`spanning-tree mode rapid-pvst`**

---

## 📊 Scoring

| Score | Niveau |
|-------|--------|
| 23-25 (92-100%) | 🌟 Excellent - Maîtrise parfaite des fonctionnalités avancées STP |
| 20-22 (80-88%) | ✅ Très bien - Bonne compréhension |
| 18-19 (72-76%) | ✅ Bien - Niveau suffisant |
| 15-17 (60-68%) | ⚠️ Moyen - Réviser les concepts clés |
| < 15 (< 60%) | ❌ Insuffisant - Révision complète nécessaire |

---

## 🎯 Thèmes à réviser selon vos erreurs

**Questions 1-4 :** PortFast (concept, configuration, restrictions)  
**Questions 5-8 :** BPDU Guard (action, configuration, récupération)  
**Questions 9-11 :** BPDU Filter (différence avec BPDU Guard, risques)  
**Questions 12-15 :** Root Guard (objectif, placement, états)  
**Questions 16-19 :** Loop Guard (perte unidirectionnelle, loop-inconsistent)  
**Questions 20-22 :** UplinkFast (convergence rapide, effets, restrictions)  
**Questions 23-25 :** BackboneFast, timers STP, obsolescence avec RSTP

---

**📚 Fin du QCM - Module 3 : Advanced Spanning Tree Tuning**
