# Checkpoint Exam : L2 Redundancy
**CCNP ENCOR v8 - Modules 1 à 5**

---

## 📋 Instructions

### Format de l'examen
- **Couverture :** Modules 1 à 5 (Packet Forwarding, STP, Advanced STP, MSTP, VLAN Trunks & EtherChannel)
- **Nombre de questions :** 45 questions
- **Durée recommandée :** 60 minutes
- **Score minimal :** 75% (34/45)
- **Type :** QCM, certaines questions à choix multiples

### Conseils
- Gérez votre temps (≈ 1,3 min par question)
- Lisez attentivement chaque question
- Certaines questions peuvent avoir plusieurs réponses correctes
- Ne laissez aucune question sans réponse
- Conditions d'examen : sans notes ni documentation

---

## Questions

### Question 1
Quel est le rôle principal de Spanning Tree Protocol (STP) dans un réseau?

- [ ] A. Augmenter la bande passante disponible
- [ ] B. Éliminer les boucles de couche 2
- [ ] C. Accélérer la convergence du réseau
- [ ] D. Chiffrer le trafic entre switches

---

### Question 2
Dans une topologie STP, quel switch devient le root bridge?

- [ ] A. Le switch avec l'adresse MAC la plus élevée
- [ ] B. Le switch avec la priorité la plus basse
- [ ] C. Le switch avec le plus de ports
- [ ] D. Le switch configuré en premier

---

### Question 3
Quelle est la valeur de priorité par défaut pour un switch dans STP?

- [ ] A. 0
- [ ] B. 4096
- [ ] C. 32768
- [ ] D. 65535

---

### Question 4
Quelles sont les trois conséquences d'une boucle de couche 2? (Choisissez trois réponses)

- [ ] A. Broadcast storms
- [ ] B. Instabilité de la table MAC
- [ ] C. Baisse de la latence
- [ ] D. Trames dupliquées
- [ ] E. Augmentation de la bande passante

---

### Question 5
Dans quel ordre se déroulent les états des ports STP lors de la convergence?

- [ ] A. Blocking → Listening → Learning → Forwarding
- [ ] B. Listening → Blocking → Learning → Forwarding
- [ ] C. Learning → Listening → Blocking → Forwarding
- [ ] D. Blocking → Learning → Listening → Forwarding

---

### Question 6
Quelle commande configure manuellement un switch comme root bridge pour le VLAN 10?

- [ ] A. `spanning-tree vlan 10 root primary`
- [ ] B. `spanning-tree vlan 10 priority 0`
- [ ] C. `spanning-tree root vlan 10`
- [ ] D. `set spanning-tree root vlan 10`

---

### Question 7
Quel est le temps de convergence typique de STP IEEE 802.1D?

- [ ] A. 2 secondes
- [ ] B. 15 secondes
- [ ] C. 30-50 secondes
- [ ] D. 60 secondes

---

### Question 8
Quelle est la différence principale entre PVST+ et RSTP?

- [ ] A. PVST+ est plus rapide que RSTP
- [ ] B. RSTP converge plus rapidement (quelques secondes)
- [ ] C. RSTP ne supporte pas les VLANs
- [ ] D. PVST+ est un standard IEEE

---

### Question 9
Quel type de port STP se connecte directement aux hôtes finaux et ne devrait jamais recevoir de BPDUs?

- [ ] A. Root port
- [ ] B. Designated port
- [ ] C. Edge port (PortFast)
- [ ] D. Alternate port

---

### Question 10
Quelle fonctionnalité désactive automatiquement un port s'il reçoit un BPDU?

- [ ] A. PortFast
- [ ] B. BPDU Guard
- [ ] C. BPDU Filter
- [ ] D. Root Guard

---

### Question 11
Un administrateur souhaite empêcher un switch aval de devenir root bridge. Quelle fonctionnalité devrait-il configurer?

- [ ] A. BPDU Guard
- [ ] B. Loop Guard
- [ ] C. Root Guard
- [ ] D. PortFast

---

### Question 12
Quelle commande active PortFast sur une interface?

- [ ] A. `spanning-tree portfast`
- [ ] B. `portfast enable`
- [ ] C. `spanning-tree fast-port`
- [ ] D. `set portfast true`

---

### Question 13
Quel timer STP définit l'intervalle d'envoi des BPDUs?

- [ ] A. Forward Delay
- [ ] B. Max Age
- [ ] C. Hello Time
- [ ] D. Message Age

---

### Question 14
Dans RSTP, quel rôle de port remplace le "Blocking" state de STP classique?

- [ ] A. Alternate Port
- [ ] B. Backup Port
- [ ] C. Discarding
- [ ] D. Disabled

---

### Question 15
Quelle est la valeur par défaut du Hello Time dans STP?

- [ ] A. 1 seconde
- [ ] B. 2 secondes
- [ ] C. 5 secondes
- [ ] D. 10 secondes

---

### Question 16
Quel protocole IEEE définit Multiple Spanning Tree Protocol (MSTP)?

- [ ] A. 802.1D
- [ ] B. 802.1w
- [ ] C. 802.1s
- [ ] D. 802.1Q

---

### Question 17
Dans MSTP, quelle configuration doit être identique sur tous les switches d'une même région? (Choisissez trois réponses)

- [ ] A. Nom de région
- [ ] B. Numéro de révision
- [ ] C. Mapping VLAN vers instance
- [ ] D. Priorité STP
- [ ] E. Adresse MAC

---

### Question 18
Combien d'instances STP exécute PVST+ dans un réseau avec 50 VLANs?

- [ ] A. 1 instance
- [ ] B. 16 instances
- [ ] C. 50 instances
- [ ] D. 64 instances

---

### Question 19
Quel est l'avantage principal de MSTP par rapport à PVST+?

- [ ] A. Configuration plus simple
- [ ] B. Réduction significative de l'overhead (utilisation CPU/mémoire)
- [ ] C. Convergence plus rapide
- [ ] D. Meilleure compatibilité

---

### Question 20
Quelle commande affiche l'état actuel de Spanning Tree sur un switch?

- [ ] A. `show spanning-tree`
- [ ] B. `show stp`
- [ ] C. `display spanning-tree`
- [ ] D. A est correcte

---

### Question 21
Dans une configuration EtherChannel, quel protocole est le standard IEEE?

- [ ] A. PAgP
- [ ] B. LACP
- [ ] C. CDP
- [ ] D. LLDP

---

### Question 22
Quel mode EtherChannel initie activement la négociation LACP?

- [ ] A. On
- [ ] B. Active
- [ ] C. Passive
- [ ] D. Auto

---

### Question 23
Combien de liens physiques maximum peut contenir un EtherChannel sur les switches Catalyst modernes?

- [ ] A. 2
- [ ] B. 4
- [ ] C. 8
- [ ] D. 16

---

### Question 24
Quelle est la conséquence si les liens d'un EtherChannel ont des configurations différentes (speed, duplex, VLAN)?

- [ ] A. L'EtherChannel fonctionne normalement
- [ ] B. L'EtherChannel ne se forme pas
- [ ] C. Seul le premier lien est actif
- [ ] D. Le switch redémarre

---

### Question 25
Quelle méthode de load-balancing EtherChannel utilise les adresses MAC source et destination?

- [ ] A. `src-mac`
- [ ] B. `dst-mac`
- [ ] C. `src-dst-mac`
- [ ] D. `src-dst-ip`

---

### Question 26
Dans VTP, quel mode permet à un switch de créer, modifier et supprimer des VLANs?

- [ ] A. Server
- [ ] B. Client
- [ ] C. Transparent
- [ ] D. Off

---

### Question 27
Quel est le risque principal d'ajouter un switch VTP Server avec un numéro de révision plus élevé dans un domaine VTP?

- [ ] A. Le switch ne se connecte pas
- [ ] B. Il peut écraser la configuration VLAN de tous les switches du domaine
- [ ] C. Il devient automatiquement root bridge
- [ ] D. Aucun risque

---

### Question 28
Quelle version de VTP permet la configuration de VLANs extended (1006-4094)?

- [ ] A. VTP version 1
- [ ] B. VTP version 2
- [ ] C. VTP version 3
- [ ] D. Toutes les versions

---

### Question 29
Sur un trunk 802.1Q, quel trafic n'est PAS tagué?

- [ ] A. Trafic du VLAN 1
- [ ] B. Trafic du VLAN natif
- [ ] C. Trafic multicast
- [ ] D. Trafic de management

---

### Question 30
Quelle commande affiche les détails d'un channel-group spécifique?

- [ ] A. `show etherchannel 1 summary`
- [ ] B. `show interface port-channel 1`
- [ ] C. `show channel-group 1`
- [ ] D. A et B sont correctes

---

### Question 31
Quel protocole découvre automatiquement si un port devrait être un trunk ou un access port?

- [ ] A. VTP
- [ ] B. DTP (Dynamic Trunking Protocol)
- [ ] C. CDP
- [ ] D. STP

---

### Question 32
Quelle combinaison de modes DTP forme un trunk? (Choisissez deux réponses)

- [ ] A. Trunk ↔ Trunk
- [ ] B. Trunk ↔ Dynamic Desirable
- [ ] C. Dynamic Auto ↔ Dynamic Auto
- [ ] D. Dynamic Desirable ↔ Dynamic Desirable

---

### Question 33
Un technicien configure un EtherChannel avec les commandes suivantes. Que devrait-il vérifier?

```cisco
interface range Gi0/1-2
 channel-group 1 mode active
 switchport mode trunk
```

- [ ] A. Le load-balancing est configuré
- [ ] B. Les interfaces ont la même vitesse et duplex
- [ ] C. LACP est activé globalement
- [ ] D. Rien, la configuration est complète

---

### Question 34
Quelle fonctionnalité UplinkFast améliore-t-elle?

- [ ] A. Convergence lors de la panne d'un lien direct vers le root bridge
- [ ] B. Convergence lors d'une panne dans le backbone
- [ ] C. Vitesse de transmission des trames
- [ ] D. Détection des boucles

---

### Question 35
Loop Guard protège contre quelle condition?

- [ ] A. Réception de BPDUs sur un edge port
- [ ] B. Perte unidirectionnelle de BPDUs
- [ ] C. Switch aval devenant root bridge
- [ ] D. Trames dupliquées

---

### Question 36
Dans RSTP, quel type de lien permet une transition immédiate vers Forwarding?

- [ ] A. Point-to-Multipoint
- [ ] B. Point-to-Point
- [ ] C. Shared
- [ ] D. Trunk

---

### Question 37
Quelle commande affiche la topologie STP vue par un switch?

- [ ] A. `show spanning-tree summary`
- [ ] B. `show spanning-tree detail`
- [ ] C. `show spanning-tree root`
- [ ] D. Toutes ces commandes

---

### Question 38
Le Bridge ID est composé de quels éléments?

- [ ] A. Priorité + Adresse MAC
- [ ] B. Priorité + VLAN ID
- [ ] C. Priorité + VLAN ID + Adresse MAC (System ID)
- [ ] D. Adresse MAC seule

---

### Question 39
Sur un switch, quelle valeur est ajoutée à la priorité de base pour former la priorité effective dans PVST+?

- [ ] A. Le numéro du port
- [ ] B. Le VLAN ID (System ID Extended)
- [ ] C. L'adresse MAC
- [ ] D. Le coût du port

---

### Question 40
Quel est le coût STP par défaut d'un lien Gigabit Ethernet?

- [ ] A. 2
- [ ] B. 4
- [ ] C. 19
- [ ] D. 100

---

### Question 41
Un switch a deux chemins vers le root bridge. Comment détermine-t-il le root port?

- [ ] A. Coût de chemin le plus bas
- [ ] B. Priorité de port la plus basse
- [ ] C. Numéro de port le plus bas
- [ ] D. Ordre : Coût → Bridge ID voisin → Priorité port → Numéro port

---

### Question 42
Dans une région MSTP, quel arbre gère la communication avec les régions externes?

- [ ] A. IST (Internal Spanning Tree)
- [ ] B. MSTI (Multiple Spanning Tree Instance)
- [ ] C. CIST (Common and Internal Spanning Tree)
- [ ] D. PVST

---

### Question 43
Quel mode VTP ne propage ni ne reçoit les mises à jour VTP, mais les transfère?

- [ ] A. Server
- [ ] B. Client
- [ ] C. Transparent
- [ ] D. Off

---

### Question 44
Quelle commande configure le load-balancing EtherChannel basé sur les adresses IP source et destination?

- [ ] A. `port-channel load-balance src-dst-ip`
- [ ] B. `etherchannel load-balance src-dst-ip`
- [ ] C. `channel-group load-balance src-dst-ip`
- [ ] D. Aucune, c'est une commande globale

---

### Question 45
Un administrateur souhaite empêcher DTP sur un port. Quelle configuration est recommandée?

- [ ] A. `switchport mode access` + `switchport nonegotiate`
- [ ] B. `switchport mode trunk` + `switchport nonegotiate`
- [ ] C. `switchport mode dynamic auto`
- [ ] D. A ou B selon le type de port souhaité

---

## Grille de réponses

| Q | Rép | Q | Rép | Q | Rép | Q | Rép | Q | Rép |
|---|-----|---|-----|---|-----|---|-----|---|-----|
| 1 | | 10 | | 19 | | 28 | | 37 | |
| 2 | | 11 | | 20 | | 29 | | 38 | |
| 3 | | 12 | | 21 | | 30 | | 39 | |
| 4 | | 13 | | 22 | | 31 | | 40 | |
| 5 | | 14 | | 23 | | 32 | | 41 | |
| 6 | | 15 | | 24 | | 33 | | 42 | |
| 7 | | 16 | | 25 | | 34 | | 43 | |
| 8 | | 17 | | 26 | | 35 | | 44 | |
| 9 | | 18 | | 27 | | 36 | | 45 | |

---

## Corrigé des réponses

### Réponses

1. **B** - Éliminer les boucles de couche 2
2. **B** - Switch avec priorité la plus basse
3. **C** - 32768
4. **A, B, D** - Broadcast storms, Instabilité MAC, Trames dupliquées
5. **A** - Blocking → Listening → Learning → Forwarding
6. **A** - `spanning-tree vlan 10 root primary`
7. **C** - 30-50 secondes
8. **B** - RSTP converge plus rapidement
9. **C** - Edge port (PortFast)
10. **B** - BPDU Guard
11. **C** - Root Guard
12. **A** - `spanning-tree portfast`
13. **C** - Hello Time
14. **C** - Discarding
15. **B** - 2 secondes
16. **C** - 802.1s
17. **A, B, C** - Nom, révision, mapping VLAN
18. **C** - 50 instances (1 par VLAN)
19. **B** - Réduction overhead
20. **D** - `show spanning-tree` est correcte
21. **B** - LACP (802.3ad)
22. **B** - Active
23. **C** - 8 liens
24. **B** - EtherChannel ne se forme pas
25. **C** - `src-dst-mac`
26. **A** - Server
27. **B** - Écrase la config VLAN
28. **C** - VTP version 3
29. **B** - Trafic du VLAN natif
30. **D** - Les deux commandes
31. **B** - DTP
32. **A, B, D** - Trunk↔Trunk, Trunk↔Dynamic Desirable, Desirable↔Desirable
33. **B** - Vérifier speed/duplex identiques
34. **A** - Convergence lien direct vers root
35. **B** - Perte unidirectionnelle BPDUs
36. **B** - Point-to-Point
37. **D** - Toutes ces commandes
38. **C** - Priorité + VLAN ID + MAC
39. **B** - VLAN ID
40. **B** - 4
41. **D** - Ordre : Coût → BID voisin → Priorité → Numéro port
42. **C** - CIST
43. **C** - Transparent
44. **A** - `port-channel load-balance src-dst-ip`
45. **D** - A ou B + nonegotiate

---

## Explications clés

### Question 2 - Élection Root Bridge
**Réponse : B**

**Processus d'élection :**
1. **Priorité la plus basse** (défaut 32768)
2. Si égalité : **Adresse MAC la plus basse**

**Exemple :**
```
Switch A: Priorité 32768, MAC 0000.1111.2222
Switch B: Priorité 32768, MAC 0000.3333.4444
Switch C: Priorité 4096,  MAC 0000.5555.6666

Root Bridge = Switch C (priorité 4096 plus basse)
```

**Configuration manuelle :**
```cisco
! Méthode 1: Root primary (priorité 24576)
spanning-tree vlan 10 root primary

! Méthode 2: Priorité manuelle
spanning-tree vlan 10 priority 4096
```

💡 **Point clé :** La priorité doit être un multiple de 4096 (0, 4096, 8192, ..., 61440).

---

### Question 4 - Conséquences boucles L2
**Réponse : A, B, D**

**Problèmes causés par les boucles :**

**1. Broadcast Storms :**
- Broadcasts se propagent indéfiniment
- Consomment toute la bande passante
- Switch CPU à 100%

**2. Instabilité table MAC :**
- Même MAC vue sur plusieurs ports
- Table MAC "flapping"
- Frames envoyées au mauvais port

**3. Trames dupliquées :**
- Même trame reçue plusieurs fois
- Corruption de données applicatives
- Confusion des protocoles

**Schéma :**
```
     [SW1]
     /   \
   /       \
[SW2]-----[SW3]
     BOUCLE!

Frame broadcast PC1:
SW1 → SW2 → SW3 → SW1 → SW2 → SW3 → ...
(Infiniment jusqu'à saturation)
```

💡 **Point clé :** STP empêche ces problèmes en bloquant certains ports pour créer une topologie sans boucle.

---

### Question 18 - PVST+ instances
**Réponse : C (50 instances)**

**Explication :**
PVST+ (Per-VLAN Spanning Tree Plus) exécute **une instance STP par VLAN**.

**Calcul :**
- 50 VLANs configurés = **50 instances STP**
- Chaque instance envoie ses propres BPDUs
- Overhead significatif (CPU, mémoire, bande passante)

**Impact :**
```
50 VLANs × BPDUs toutes les 2 sec = 25 BPDUs/sec par port trunk
Sur 48 ports = 1200 BPDUs/sec pour le switch
```

**Solution MSTP :**
Regrouper plusieurs VLANs dans une même instance :
```
MSTI 1: VLANs 10-20 (1 instance)
MSTI 2: VLANs 30-40 (1 instance)
Total: 2 instances au lieu de 50 ✅
```

💡 **Point clé :** MSTP réduit drastiquement l'overhead en permettant plusieurs VLANs par instance.

---

### Question 22 - Mode LACP actif
**Réponse : B (Active)**

**Modes LACP :**

| Mode | Comportement |
|------|--------------|
| **Active** | Initie activement la négociation LACP |
| **Passive** | Attend la négociation, répond uniquement |
| **On** | Pas de négociation, force l'EtherChannel |

**Résultats de combinaisons :**
- Active ↔ Active = ✅ EtherChannel formé
- Active ↔ Passive = ✅ EtherChannel formé
- Passive ↔ Passive = ❌ Pas d'EtherChannel
- Active ↔ On = ❌ Incompatible
- On ↔ On = ✅ EtherChannel formé (sans négociation)

**Best practice :** Utiliser **Active** des deux côtés pour LACP.

💡 **Point clé :** "Active" est l'équivalent de "Desirable" pour PAgP.

---

### Question 27 - Risque VTP
**Réponse : B**

**Scénario dangereux :**
```
Réseau production:
- SW1 (VTP Server, Révision 50, VLANs 10-50 configurés)
- SW2 (VTP Server, Révision 50, VLANs 10-50 configurés)

Ancien switch réactivé:
- SW3 (VTP Server, Révision 100, VLANs 1 seulement)

Connexion SW3 au réseau:
→ SW3 a révision plus élevée (100 > 50)
→ SW1 et SW2 synchronisent depuis SW3
→ TOUS les VLANs 10-50 SUPPRIMÉS! ⚠️
→ Perte de connectivité massive
```

**Protection :**
```cisco
! Méthode 1: Mode Transparent
vtp mode transparent

! Méthode 2: VTP version 3 (avec mot de passe)
vtp version 3
vtp password SecurePass123

! Méthode 3: Désactiver VTP
vtp mode off
```

**Avant d'ajouter un switch :**
1. Vérifier le numéro de révision : `show vtp status`
2. Si élevé, réinitialiser :
   ```cisco
   vtp mode transparent
   vtp mode server
   ! Ou changer le domaine temporairement
   ```

💡 **Point clé :** VTP est dangereux dans les grands réseaux. Best practice : mode Transparent ou Off.

---

### Question 32 - Modes DTP  
**Réponse : A, B, D**

**Table de négociation DTP :**

| Mode ↓ Mode → | **Trunk** | **Dynamic Desirable** | **Dynamic Auto** | **Access** |
|---------------|-----------|----------------------|------------------|------------|
| **Trunk** | ✅ Trunk | ✅ Trunk | ✅ Trunk | ❌ Limited |
| **Dynamic Desirable** | ✅ Trunk | ✅ Trunk | ✅ Trunk | ❌ Access |
| **Dynamic Auto** | ✅ Trunk | ✅ Trunk | ❌ Access | ❌ Access |
| **Access** | ❌ Limited | ❌ Access | ❌ Access | ✅ Access |

**Résumé formations trunk :**
- Trunk ↔ Trunk = ✅
- Trunk ↔ Dynamic Desirable = ✅
- Trunk ↔ Dynamic Auto = ✅
- Dynamic Desirable ↔ Dynamic Desirable = ✅
- Dynamic Desirable ↔ Dynamic Auto = ✅
- Dynamic Auto ↔ Dynamic Auto = ❌ (devient Access)

**Désactiver DTP (recommended) :**
```cisco
interface Gi0/1
 switchport mode trunk
 switchport nonegotiate   ! Désactive DTP
```

💡 **Point clé :** "Desirable" = actif, "Auto" = passif (comme LACP).

---

### Question 41 - Sélection Root Port
**Réponse : D**

**Critères de sélection du Root Port (ordre) :**

1. **Coût de chemin le plus bas vers root bridge**
   ```
   Port A: Coût 4 (1 Gbps direct)
   Port B: Coût 8 (2× 100 Mbps)
   → Port A sélectionné
   ```

2. **Si égalité : Bridge ID voisin le plus bas**
   ```
   Port A via SW1 (BID 32768.0000.1111.1111)
   Port B via SW2 (BID 32768.0000.2222.2222)
   → Port A sélectionné (BID SW1 plus bas)
   ```

3. **Si égalité : Priorité de port voisin la plus basse**
   ```
   Port A connecté à SW1-Gi0/1 (priorité 128)
   Port B connecté à SW1-Gi0/2 (priorité 64)
   → Port B sélectionné
   ```

4. **Si égalité : Numéro de port voisin le plus bas**
   ```
   Port A connecté à SW1-Gi0/1
   Port B connecté à SW1-Gi0/2
   → Port A sélectionné (Gi0/1 < Gi0/2)
   ```

**Formule mnémotechnique :** **CBPN** (Cost, BID, Priority, Number)

💡 **Point clé :** Le premier critère à différer détermine le root port.

---

## Tableau de scoring

| Score | Pourcentage | Évaluation |
|-------|-------------|------------|
| 41-45 | 91-100% | 🏆 Excellent - Parfaite maîtrise L2 Redundancy |
| 37-40 | 82-89% | ✅ Très bien - Prêt pour les modules suivants |
| 34-36 | 76-80% | ⚠️ Bien - Revoir les points faibles identifiés |
| 30-33 | 67-73% | 📚 Moyen - Révision approfondie recommandée |
| < 30 | < 67% | ❌ Insuffisant - Revoir les modules 1-5 |

---

## Recommandations post-checkpoint

### Score ≥ 37/45 (82%+)
✅ Excellente compréhension des technologies L2  
➡️ Continuez avec le **Module 6** (IP Routing Essentials)

### Score 34-36/45 (76-80%)
⚠️ Bonnes bases mais quelques lacunes  
➡️ Réviser les fiches des modules faibles  
➡️ Refaire les QCM concernés  
➡️ Puis passer au Module 6

### Score < 34/45 (< 76%)
❌ Fondamentaux L2 insuffisants  
➡️ Révision complète modules 1-5 nécessaire  
➡️ Relire les notes  
➡️ Refaire tous les QCM  
➡️ Reprendre ce checkpoint avant de continuer

---

**Bloc suivant :** [Module 6 - IP Routing Essentials](../Notes/Module-06-notes.md)
