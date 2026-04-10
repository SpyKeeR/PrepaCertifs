# QCM Module 1 : Packet Forwarding
**CCNP ENCOR v8 - Acheminement des paquets**

---

## 📋 Instructions

- **Nombre de questions :** 25
- **Durée recommandée :** 35 minutes
- **Score minimum :** 70% (18/25)
- **Conseils :** Certaines questions peuvent avoir plusieurs réponses correctes

---

## Questions

### Question 1
Quelle est la longueur d'une adresse MAC?

- [ ] A. 32 bits
- [ ] B. 48 bits
- [ ] C. 64 bits
- [ ] D. 128 bits

---

### Question 2
Un switch reçoit une trame avec une adresse MAC de destination inconnue (pas dans sa table MAC). Quel est le comportement du switch?

- [ ] A. Il supprime la trame
- [ ] B. Il envoie la trame au routeur par défaut
- [ ] C. Il l'envoie sur tous les ports sauf le port source (flooding)
- [ ] D. Il envoie une requête ARP

---

### Question 3
Quelle commande affiche la table MAC d'un switch Cisco?

- [ ] A. `show mac table`
- [ ] B. `show mac-address-table`
- [ ] C. `show arp`
- [ ] D. `show cam table`

---

### Question 4
Combien de bits sont ajoutés à une trame Ethernet par le tag 802.1Q?

- [ ] A. 16 bits
- [ ] B. 24 bits
- [ ] C. 32 bits
- [ ] D. 64 bits

---

### Question 5
Quelle est la plage de VLANs standard sur les switches Cisco?

- [ ] A. 1-512
- [ ] B. 1-1005
- [ ] C. 1-4094
- [ ] D. 1-16384

---

### Question 6
Quel est le VLAN natif par défaut sur un trunk 802.1Q?

- [ ] A. VLAN 0
- [ ] B. VLAN 1
- [ ] C. VLAN 99
- [ ] D. VLAN 1002

---

### Question 7
Quelle commande configure un port en mode trunk sur un switch Catalyst?

- [ ] A. `switchport mode dynamic`
- [ ] B. `switchport mode access`
- [ ] C. `switchport mode trunk`
- [ ] D. `switchport trunk enable`

---

### Question 8
Quelles sont les trois conditions nécessaires pour qu'une SVI soit en état up/up? (Choisissez trois réponses)

- [ ] A. Le VLAN doit exister dans la base VLAN
- [ ] B. Au moins un port doit être assigné au VLAN en état up/up
- [ ] C. La commande `no shutdown` doit être appliquée à la SVI
- [ ] D. Le routage IP doit être désactivé
- [ ] E. Le VLAN doit être dans la plage extended (1006-4094)

---

### Question 9
Quel protocole est utilisé pour mapper une adresse IP à une adresse MAC?

- [ ] A. ICMP
- [ ] B. ARP
- [ ] C. RARP
- [ ] D. DNS

---

### Question 10
Dans le contexte d'une trame ARP Request, quel type d'adresse MAC de destination est utilisé?

- [ ] A. Unicast
- [ ] B. Multicast
- [ ] C. Broadcast
- [ ] D. Anycast

---

### Question 11
Lorsqu'un paquet est routé d'un réseau à un autre, quelles adresses changent et lesquelles restent constantes?

- [ ] A. Les adresses IP et MAC changent toutes les deux
- [ ] B. Les adresses IP restent constantes, les adresses MAC changent
- [ ] C. Les adresses IP changent, les adresses MAC restent constantes
- [ ] D. Les adresses IP et MAC restent toutes les deux constantes

---

### Question 12
Quelle est la différence principale entre un hub et un switch?

- [ ] A. Le hub fonctionne en full-duplex, le switch en half-duplex
- [ ] B. Le switch crée un domaine de collision par port, le hub a un seul domaine de collision
- [ ] C. Le hub est plus rapide que le switch
- [ ] D. Il n'y a pas de différence

---

### Question 13
Quelle adresse MAC représente une adresse de broadcast Ethernet?

- [ ] A. 00:00:00:00:00:00
- [ ] B. FF:FF:FF:FF:FF:FF
- [ ] C. 01:00:5E:00:00:00
- [ ] D. FF:00:00:00:00:00

---

### Question 14
Dans la commande `switchport trunk allowed vlan add 30`, quel est l'effet de cette commande?

- [ ] A. Remplace tous les VLANs autorisés par le VLAN 30
- [ ] B. Ajoute le VLAN 30 à la liste existante des VLANs autorisés
- [ ] C. Supprime le VLAN 30 de la liste des VLANs autorisés
- [ ] D. Configure le VLAN 30 comme VLAN natif

---

### Question 15
Quelle commande permet de configurer une adresse IPv4 secondaire sur une interface?

- [ ] A. `ip address 192.168.1.1 255.255.255.0 secondary`
- [ ] B. `ip address secondary 192.168.1.1 255.255.255.0`
- [ ] C. `ip secondary-address 192.168.1.1 255.255.255.0`
- [ ] D. `secondary ip address 192.168.1.1 255.255.255.0`

---

### Question 16
Quelle architecture d'acheminement utilise une FIB (Forwarding Information Base) et une Adjacency Table?

- [ ] A. Process Switching
- [ ] B. Fast Switching
- [ ] C. CEF (Cisco Express Forwarding)
- [ ] D. Distributed Switching

---

### Question 17
Quel délai d'expiration par défaut est utilisé pour les entrées dynamiques de la table MAC?

- [ ] A. 60 secondes
- [ ] B. 300 secondes
- [ ] C. 600 secondes
- [ ] D. 3600 secondes

---

### Question 18
Dans une configuration router-on-a-stick, quelle commande est nécessaire pour associer une sous-interface à un VLAN spécifique?

- [ ] A. `vlan-id 10`
- [ ] B. `switchport access vlan 10`
- [ ] C. `encapsulation dot1q 10`
- [ ] D. `trunk vlan 10`

---

### Question 19
Que se passe-t-il lorsque le VLAN natif ne correspond pas des deux côtés d'un trunk?

- [ ] A. Le trunk ne s'établit pas
- [ ] B. Le trafic peut changer de VLAN de manière involontaire
- [ ] C. Les deux switches redémarrent automatiquement
- [ ] D. Aucun problème, c'est une configuration normale

---

### Question 20
Quelle technologie de mémoire est utilisée pour stocker la table MAC sur un switch?

- [ ] A. RAM
- [ ] B. ROM
- [ ] C. NVRAM
- [ ] D. CAM (Content Addressable Memory)

---

### Question 21
Un technicien souhaite limiter les VLANs sur un trunk aux VLANs 10, 20 et 99 uniquement. Quelle commande devrait-il utiliser?

- [ ] A. `switchport trunk vlan 10,20,99`
- [ ] B. `switchport trunk allowed vlan 10,20,99`
- [ ] C. `switchport trunk permit vlan 10,20,99`
- [ ] D. `switchport allowed vlan 10,20,99`

---

### Question 22
Quelle commande active le routage IPv6 sur un routeur Cisco?

- [ ] A. `ipv6 enable`
- [ ] B. `ipv6 routing`
- [ ] C. `ipv6 unicast-routing`
- [ ] D. `ip routing ipv6`

---

### Question 23
Dans le modèle OSI, à quelle couche se situe le protocole Ethernet?

- [ ] A. Couche 1 (Physique)
- [ ] B. Couche 2 (Liaison de données)
- [ ] C. Couche 3 (Réseau)
- [ ] D. Couche 4 (Transport)

---

### Question 24
Quel avantage principal offre CEF (Cisco Express Forwarding) par rapport au Process Switching?

- [ ] A. CEF utilise moins de mémoire
- [ ] B. CEF nécessite moins de configuration
- [ ] C. CEF offre des performances bien plus élevées en libérant le CPU
- [ ] D. CEF est compatible avec plus de protocoles

---

### Question 25
Sur un switch multicouche, quelle commande est nécessaire pour activer le routage inter-VLAN via des SVIs?

- [ ] A. `routing enable`
- [ ] B. `ip routing`
- [ ] C. `multilayer-routing`
- [ ] D. `vlan routing`

---

## Grille de réponses

| Q | Rép | Q | Rép | Q | Rép | Q | Rép | Q | Rép |
|---|-----|---|-----|---|-----|---|-----|---|-----|
| 1 | | 6 | | 11 | | 16 | | 21 | |
| 2 | | 7 | | 12 | | 17 | | 22 | |
| 3 | | 8 | | 13 | | 18 | | 23 | |
| 4 | | 9 | | 14 | | 19 | | 24 | |
| 5 | | 10 | | 15 | | 20 | | 25 | |

---

## Corrigé des réponses

### Réponses

1. **B** - 48 bits
2. **C** - Flooding sur tous les ports sauf source
3. **B** - `show mac-address-table`
4. **C** - 32 bits
5. **B** - 1-1005
6. **B** - VLAN 1
7. **C** - `switchport mode trunk`
8. **A, B, C** - VLAN existe, port assigné up/up, no shutdown
9. **B** - ARP
10. **C** - Broadcast
11. **B** - IPs constantes, MACs changent
12. **B** - Switch = 1 domaine/port, Hub = 1 domaine partagé
13. **B** - FF:FF:FF:FF:FF:FF
14. **B** - Ajoute VLAN 30 à la liste
15. **A** - `ip address ... secondary`
16. **C** - CEF
17. **B** - 300 secondes
18. **C** - `encapsulation dot1q 10`
19. **B** - Trafic peut changer de VLAN involontairement
20. **D** - CAM
21. **B** - `switchport trunk allowed vlan 10,20,99`
22. **C** - `ipv6 unicast-routing`
23. **B** - Couche 2
24. **C** - Performances élevées, CPU libéré
25. **B** - `ip routing`

---

## Explications détaillées

### Question 1 - Longueur adresse MAC
**Réponse : B (48 bits)**

**Explication :**
Une adresse MAC est composée de 48 bits (6 octets), généralement représentée en hexadécimal :
- Format : `XX:XX:XX:XX:XX:XX`
- 24 bits (3 octets) : OUI (Organizationally Unique Identifier) - identifie le fabricant
- 24 bits (3 octets) : Identifiant unique du périphérique

Exemple : `00:1A:2B:3C:4D:5E`

💡 **Point clé :** Les adresses MAC sont uniques au niveau mondial (en théorie).

---

### Question 2 - MAC inconnue
**Réponse : C (Flooding)**

**Explication :**
Lorsqu'un switch reçoit une trame avec une adresse MAC de destination qui n'est pas dans sa table MAC :
1. Le switch effectue un **unknown unicast flooding**
2. La trame est envoyée sur **tous les ports** sauf le port source
3. Le périphérique destination répond, permettant au switch d'apprendre sa MAC

Ce comportement ressemble au broadcast mais n'en est pas un techniquement.

💡 **Point clé :** C'est le mécanisme d'apprentissage dynamique des switches.

---

### Question 8 - Conditions SVI up/up
**Réponse : A, B, C**

**Explication :**
Une SVI (Switched Virtual Interface) ne peut être en état `up/up` que si **trois conditions** sont remplies :

1. **Le VLAN doit exister** dans la base de données VLAN du switch
   ```cisco
   vlan 10
   ```

2. **Au moins un port** doit être assigné au VLAN et en état `up/up`
   ```cisco
   interface Gi0/1
    switchport access vlan 10
   ```

3. **La SVI doit être activée** avec `no shutdown`
   ```cisco
   interface vlan 10
    no shutdown
   ```

Si l'une de ces conditions manque, la SVI sera `down`.

💡 **Point clé :** Une SVI peut être configurée mais rester down si aucun port actif n'est dans le VLAN.

---

### Question 11 - Routage et adresses
**Réponse : B**

**Explication :**
Lors du routage d'un paquet d'un réseau à un autre :

**Adresses IP (Couche 3) :**
- ✅ **Restent constantes** tout au long du chemin
- IP source = adresse de l'hôte émetteur
- IP destination = adresse de l'hôte destination

**Adresses MAC (Couche 2) :**
- ❌ **Changent à chaque saut** (chaque routeur)
- MAC source = interface de sortie du routeur actuel
- MAC destination = interface d'entrée du routeur suivant (ou destination finale)

Exemple :
```
PC1 (192.168.1.10) → R1 → R2 → Serveur (192.168.20.10)

Segment 1 (PC1 → R1):
  IP src: 192.168.1.10,  IP dst: 192.168.20.10
  MAC src: PC1,          MAC dst: R1-Gi0/0

Segment 2 (R1 → R2):
  IP src: 192.168.1.10,  IP dst: 192.168.20.10
  MAC src: R1-Gi0/1,     MAC dst: R2-Gi0/0

Segment 3 (R2 → Serveur):
  IP src: 192.168.1.10,  IP dst: 192.168.20.10
  MAC src: R2-Gi0/1,     MAC dst: Serveur
```

💡 **Point clé :** C'est fondamental pour comprendre l'encapsulation et le routage.

---

### Question 16 - CEF
**Réponse : C (Cisco Express Forwarding)**

**Explication :**
CEF (Cisco Express Forwarding) est l'architecture d'acheminement moderne qui utilise :

**1. FIB (Forwarding Information Base) :**
- Copie optimisée de la table de routage (RIB)
- Contient les préfixes, next-hops et interfaces de sortie
- Mise à jour en temps réel

**2. Adjacency Table :**
- Informations de couche 2 (adresses MAC)
- Associe les next-hops IP à leurs adresses MAC
- Permet la réécriture rapide des en-têtes Ethernet

**Avantages :**
- Wire-speed forwarding (performances maximales)
- Hardware-based (ASIC/TCAM)
- CPU libéré pour tâches de contrôle
- Latence déterministe

```cisco
Router# show ip cef
Prefix              Next Hop             Interface
0.0.0.0/0           10.0.0.2             Gi0/1
192.168.10.0/24     attached             Gi0/0
```

💡 **Point clé :** CEF est activé par défaut sur tous les équipements Cisco modernes.

---

### Question 18 - Router-on-a-stick
**Réponse : C**

**Explication :**
Dans une configuration **router-on-a-stick**, on utilise des sous-interfaces pour router entre VLANs.

**Configuration complète :**
```cisco
! Interface physique (doit être up)
interface Gi0/0
 no shutdown
exit

! Sous-interface pour VLAN 10
interface Gi0/0.10
 encapsulation dot1q 10          ! Associe au VLAN 10
 ip address 192.168.10.1 255.255.255.0
exit

! Sous-interface pour VLAN 20
interface Gi0/0.20
 encapsulation dot1q 20          ! Associe au VLAN 20
 ip address 192.168.20.1 255.255.255.0
exit
```

**Commande clé :** `encapsulation dot1q vlan-id`
- Indique au routeur quel tag 802.1Q traiter
- Doit correspondre au VLAN trunk du switch

**Côté switch :**
```cisco
interface Gi0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
```

💡 **Point clé :** Sans `encapsulation dot1q`, la sous-interface ne sait pas quel VLAN traiter.

---

### Question 19 - VLAN natif mismatch
**Réponse : B**

**Explication :**
Un **mismatch de VLAN natif** entre deux switches peut causer de sérieux problèmes :

**Scénario problématique :**
```
Switch1 : Native VLAN 1
Switch2 : Native VLAN 99
```

**Conséquences :**
1. Le trafic non-tagué de Switch1 (VLAN 1) arrive sur Switch2
2. Switch2 l'interprète comme VLAN 99 (son natif)
3. **Le trafic change de VLAN involontairement**
4. Problèmes de connectivité imprévisibles
5. Faille de sécurité potentielle (VLAN hopping)

**Best practices :**
- ✅ Toujours configurer le même VLAN natif des 2 côtés
- ✅ Utiliser un VLAN dédié non-utilisé (ex: VLAN 999)
- ✅ Ne jamais utiliser VLAN 1 comme natif

```cisco
! Des deux côtés du trunk
switchport trunk native vlan 999
```

💡 **Point clé :** Cisco IOS affiche un message d'alerte en cas de mismatch : "CDP: Native VLAN mismatch discovered".

---

### Question 20 - Mémoire CAM
**Réponse : D**

**Explication :**
La **CAM (Content Addressable Memory)** est une technologie de mémoire spéciale utilisée pour stocker la table MAC.

**Caractéristiques :**
- **Recherche ultra-rapide** : Résultat en 1 cycle d'horloge
- **Recherche parallèle** : Compare simultanément avec toutes les entrées
- **Résultat binaire** : 0 (pas trouvé) ou 1 (trouvé)

**Différences avec RAM standard :**
| Aspect | RAM | CAM |
|--------|-----|-----|
| Recherche | Séquentielle | Parallèle |
| Vitesse | Lente | Ultra-rapide |
| Coût | Faible | Élevé |
| Usage | Stockage général | Tables de lookup |

**Fonctionnement :**
```
Requête: "Où est la MAC 0050.7966.6800?"
├─ CAM compare avec TOUTES les entrées en parallèle
└─ Résultat instantané: "Port Gi0/4, VLAN 10"
```

💡 **Point clé :** La CAM permet aux switches de commuter à wire-speed (vitesse du câble).

---

### Question 24 - Avantage CEF
**Réponse : C**

**Explication :**
CEF offre un **avantage de performance majeur** par rapport au Process Switching :

**Process Switching (ancien) :**
- Chaque paquet traité par le **CPU**
- Recherche complète dans table de routage pour chaque paquet
- **Très lent** et **consomme beaucoup de CPU**
- Limite : ~10,000 paquets/seconde

**CEF (moderne) :**
- Paquets traités par **ASIC/TCAM** (hardware)
- Tables pré-calculées (FIB + Adjacency)
- **CPU totalement libéré** pour tâches de contrôle (protocoles de routage, management)
- Limite : Wire-speed (plusieurs millions de paquets/seconde)

**Comparaison :**
```
Process Switching:
Paquet → CPU → Table routage → CPU décide → CPU transfère
         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
              Tout passe par le CPU

CEF:
Paquet → ASIC → FIB → Adjacency → Transfère
         ^^^^^^^^^^^^^^^^^^^^^^^^^
          Tout en hardware
```

**Impact :**
- Latence réduite et déterministe
- Scalabilité (supporttrafic élevé)
- Stabilité accrue (CPU disponible pour protocoles)

💡 **Point clé :** CEF est la raison pour laquelle les routeurs modernes peuvent gérer des débits de plusieurs Tbps.

---

## Tableau de scoring

| Score | Pourcentage | Évaluation |
|-------|-------------|------------|
| 23-25 | 92-100% | 🏆 Excellent - Concepts parfaitement maîtrisés |
| 20-22 | 80-88% | ✅ Très bien - Prêt pour le checkpoint |
| 18-19 | 72-76% | ⚠️ Bien - Réviser les points faibles |
| 15-17 | 60-68% | 📚 Moyen - Révision approfondie recommandée |
| < 15 | < 60% | ❌ Insuffisant - Revoir le module complet |

---

**Prochaine étape :** Si score ≥ 18/25 (72%), passer au [Module 2 - Spanning Tree Protocol](QCM-Module-02.md). Sinon, réviser la [fiche du module](../Fiches/Fiche-Module-01.md) et les [notes détaillées](../Notes/Module-01-notes.md).
