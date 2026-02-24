# QCM - Module 06 : Couche de liaison de données
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **17 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Quelle couche du modèle OSI est responsable de l'encadrement des paquets en trames ?

- [ ] A. Couche 1 - Physique
- [ ] B. Couche 2 - Liaison de données
- [ ] C. Couche 3 - Réseau
- [ ] D. Couche 4 - Transport

### Question 2
Quelles sont les responsabilités principales de la couche Liaison de données ?

- [ ] A. Accès au média (contrôle qui peut émettre)
- [ ] B. Routage des paquets entre réseaux
- [ ] C. Adressage physique (MAC)
- [ ] D. Détection d'erreurs (FCS/CRC)

### Question 3
En quoi sont divisées les deux sous-couches de la couche Liaison de données selon le modèle IEEE ?

- [ ] A. LLC (Logical Link Control)
- [ ] B. IP (Internet Protocol)
- [ ] C. MAC (Media Access Control)
- [ ] D. TCP (Transmission Control Protocol)

### Question 4
Quel est le rôle du champ FCS (Frame Check Sequence) dans une trame ?

- [ ] A. Identifier le type de protocole encapsulé
- [ ] B. Détecter les erreurs de transmission
- [ ] C. Corriger automatiquement les erreurs
- [ ] D. Indiquer l'adresse de destination

### Question 5
Quelle est l'adresse MAC de broadcast Ethernet ?

- [ ] A. 00:00:00:00:00:00
- [ ] B. FF:FF:FF:FF:FF:FF
- [ ] C. 01:00:5E:00:00:00
- [ ] D. 255.255.255.255

### Question 6
Quelle est la taille maximale des données (MTU) dans une trame Ethernet standard ?

- [ ] A. 64 octets
- [ ] B. 1500 octets
- [ ] C. 1518 octets
- [ ] D. 9000 octets

### Question 7
Quel est le PDU (Protocol Data Unit) de la couche Liaison de données ?

- [ ] A. Bit
- [ ] B. Trame (Frame)
- [ ] C. Paquet (Packet)
- [ ] D. Segment

### Question 8
Quelle topologie LAN physique est la plus courante dans les réseaux modernes ?

- [ ] A. Bus
- [ ] B. Anneau (Ring)
- [ ] C. Étoile (Star)
- [ ] D. Maillée (Mesh)

### Question 9
Dans une topologie WAN point-à-point, combien de nœuds sont directement connectés ?

- [ ] A. 1 nœud
- [ ] B. 2 nœuds
- [ ] C. 3 nœuds ou plus
- [ ] D. Tous les nœuds du réseau

### Question 10
Quelle commande IOS affiche la table d'adresses MAC d'un commutateur ?

- [ ] A. `show ip route`
- [ ] B. `show mac address-table`
- [ ] C. `show interfaces`
- [ ] D. `show arp`

### Question 11
Que signifie le statut "up/down" pour une interface réseau ?

- [ ] A. Couche physique OK, problème de couche 2 (protocole)
- [ ] B. Couche physique et couche 2 toutes deux OK
- [ ] C. Interface désactivée volontairement
- [ ] D. Câble déconnecté

### Question 12
Quel algorithme de détection d'erreurs est utilisé dans le FCS des trames Ethernet ?

- [ ] A. MD5
- [ ] B. CRC-32
- [ ] C. SHA-256
- [ ] D. Checksum simple

### Question 13
Quelle sous-couche de la couche Liaison de données gère l'interaction avec le matériel physique ?

- [ ] A. LLC (Logical Link Control)
- [ ] B. MAC (Media Access Control)
- [ ] C. Network
- [ ] D. Session

### Question 14
Quels types d'adresses MAC existent dans les communications réseau ?

- [ ] A. Unicast (un-à-un)
- [ ] B. Broadcast (un-vers-tous)
- [ ] C. Multicast (un-vers-plusieurs)
- [ ] D. Anycast

### Question 15
Quelle topologie WAN offre le plus haut niveau de redondance en connectant chaque site à tous les autres ?

- [ ] A. Point-à-point
- [ ] B. Hub-and-spoke
- [ ] C. Mesh complet (Full mesh)
- [ ] D. Bus

### Question 16
Que se passe-t-il lorsqu'une trame Ethernet reçue a un FCS invalide ?

- [ ] A. La trame est corrigée automatiquement
- [ ] B. La trame est retransmise immédiatement
- [ ] C. La trame est rejetée (jetée)
- [ ] D. Une alerte est envoyée à l'administrateur

### Question 17
Dans la sortie de la commande `show interfaces`, que signifie "administratively down" ?

- [ ] A. L'interface est activée mais le câble est déconnecté
- [ ] B. L'interface a été désactivée volontairement avec la commande `shutdown`
- [ ] C. L'interface fonctionne normalement
- [ ] D. Il y a trop d'erreurs sur l'interface

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : B**

**Explication :**
La **Couche 2 - Liaison de données** est responsable de l'encadrement (framing) des paquets de couche 3 en trames. Elle ajoute un en-tête avec les adresses MAC et un trailer avec le FCS.

**💡 Point clé :** L'encadrement encapsule le paquet IP dans une trame avec :
- En-tête : Adresses MAC source/destination, type/longueur
- Données : Le paquet de couche 3
- Trailer : FCS pour la détection d'erreurs

---

## Question 2
**Réponses correctes : A, C, D**

**Explication :**
Les responsabilités de la couche Liaison de données incluent :
- **Accès au média (A)** : Contrôler qui peut émettre sur le média partagé
- **Adressage physique (C)** : Utiliser les adresses MAC
- **Détection d'erreurs (D)** : Vérifier l'intégrité avec FCS/CRC

Le routage (B) est le rôle de la couche Réseau (Couche 3).

**💡 Point clé :** La couche 2 ne route pas entre réseaux, elle livre localement sur le même segment réseau. Elle détecte les erreurs mais ne les corrige pas (c'est le rôle des couches supérieures comme TCP).

---

## Question 3
**Réponses correctes : A, C**

**Explication :**
Selon le modèle IEEE, la couche Liaison de données est divisée en :
- **LLC - Logical Link Control (A)** : Interface avec les protocoles de couche supérieure
- **MAC - Media Access Control (C)** : Gestion des adresses MAC et accès au média

**💡 Point clé :** LLC est la sous-couche supérieure (interface protocoles), MAC est la sous-couche inférieure (matériel). Cette division permet à différentes technologies de couche 2 (Ethernet, Wi-Fi, PPP) de coexister.

---

## Question 4
**Réponse correcte : B**

**Explication :**
Le **FCS (Frame Check Sequence)** détecte les erreurs de transmission en utilisant un calcul CRC-32. Le récepteur recalcule le FCS : si le résultat diffère, la trame est corrompue et est jetée.

**💡 Point clé :** Le FCS détecte les erreurs mais ne les corrige PAS. La retransmission éventuelle est gérée par les protocoles de couches supérieures (comme TCP). Le FCS est placé dans le trailer de la trame.

---

## Question 5
**Réponse correcte : B**

**Explication :**
L'adresse MAC de broadcast Ethernet est **FF:FF:FF:FF:FF:FF** (tous les bits à 1). Tous les périphériques du segment réseau reçoivent et traitent les trames avec cette adresse de destination.

**💡 Point clé :** Le broadcast est utilisé par :
- ARP (résolution IP → MAC)
- DHCP Discover (recherche de serveur DHCP)
- Certaines annonces de protocoles

Attention : 255.255.255.255 (D) est une adresse IP de broadcast, pas une adresse MAC.

---

## Question 6
**Réponse correcte : B**

**Explication :**
La **MTU (Maximum Transmission Unit)** d'Ethernet est de **1500 octets**. C'est la taille maximale des données (payload) dans une trame Ethernet standard. 1518 octets (C) est la taille totale de la trame (en-têtes + données + FCS).

**💡 Point clé :** Structure trame Ethernet :
- En-tête : 14 octets (6 + 6 + 2)
- Données : 46 à 1500 octets (MTU = 1500)
- FCS : 4 octets
- Taille totale : 64 à 1518 octets

Les Jumbo Frames (9000 octets) sont utilisées en datacenter mais ne sont pas standard.

---

## Question 7
**Réponse correcte : B**

**Explication :**
Le PDU de la couche Liaison de données est la **Trame (Frame)**. Elle contient les adresses MAC, les données encapsulées, et le FCS.

**💡 Point clé :** Rappel des PDU par couche :
- Couche 4 : Segment/Datagramme
- Couche 3 : Paquet
- Couche 2 : **Trame**
- Couche 1 : Bits

---

## Question 8
**Réponse correcte : C**

**Explication :**
La topologie **Étoile (Star)** est la plus courante dans les LAN modernes. Tous les périphériques se connectent à un commutateur central. Les topologies bus et anneau sont obsolètes pour les LAN.

**💡 Point clé :** Avantages de l'étoile :
- Facile à installer et dépanner
- Défaillance isolée (un câble coupé n'affecte qu'un périphérique)
- Évolutif

Inconvénient : Le switch central est un point de défaillance unique.

---

## Question 9
**Réponse correcte : B**

**Explication :**
Dans une topologie point-à-point, exactement **2 nœuds** sont directement connectés. C'est la topologie WAN la plus simple, utilisée pour les liaisons série entre routeurs.

**💡 Point clé :** Point-à-point caractéristiques :
- Pas de contrôle d'accès au média nécessaire
- Full-duplex (communication bidirectionnelle simultanée)
- Bande passante dédiée
- Protocoles : PPP, HDLC

---

## Question 10
**Réponse correcte : B**

**Explication :**
La commande `show mac address-table` affiche la table d'adresses MAC d'un commutateur, montrant quelle adresse MAC est accessible par quelle interface.

**💡 Point clé :** Exemple de sortie :
```
Switch# show mac address-table
          Mac Address Table
-------------------------------------------
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0cd9.96e8.8a01    DYNAMIC     Gi0/1
   1    0060.2fe2.4ab1    DYNAMIC     Gi0/2
```

Les autres commandes :
- `show ip route` : Table de routage
- `show interfaces` : État des interfaces
- `show arp` : Table ARP

---

## Question 11
**Réponse correcte : A**

**Explication :**
Le statut **"up/down"** signifie que la couche physique (Couche 1) fonctionne mais il y a un problème au niveau de la couche 2 (protocole de liaison). Cela peut indiquer un problème de configuration du protocole ou d'encapsulation.

**💡 Point clé :** Statuts courants :
- **up/up** : Tout fonctionne (physique et protocole OK)
- **down/down** : Câble déconnecté ou interface éteinte
- **up/down** : Physique OK, problème protocole
- **administratively down** : Interface désactivée avec `shutdown`

---

## Question 12
**Réponse correcte : B**

**Explication :**
Ethernet utilise **CRC-32** (Cyclic Redundancy Check 32 bits) pour le calcul du FCS. C'est un algorithme mathématique qui génère une valeur de contrôle basée sur le contenu de la trame.

**💡 Point clé :** Le CRC-32 est très efficace pour détecter les erreurs (bits inversés, rajoutés, supprimés) mais ne peut pas les corriger. MD5 et SHA-256 sont des fonctions de hachage cryptographiques, pas utilisées pour le FCS.

---

## Question 13
**Réponse correcte : B**

**Explication :**
La sous-couche **MAC (Media Access Control)** gère l'interaction avec le matériel physique, les adresses MAC, l'encapsulation des trames, et le contrôle d'accès au média. Elle est spécifique à chaque technologie (Ethernet, Wi-Fi, etc.).

**💡 Point clé :** 
- **MAC** : Proche du matériel, spécifique à la technologie
- **LLC** : Interface avec les protocoles supérieurs, indépendante de la technologie

---

## Question 14
**Réponses correctes : A, B, C**

**Explication :**
Les types d'adresses MAC sont :
- **Unicast (A)** : Communication un-à-un (adresse MAC normale)
- **Broadcast (B)** : Communication un-vers-tous (FF:FF:FF:FF:FF:FF)
- **Multicast (C)** : Communication un-vers-plusieurs (groupe)

Anycast (D) est un concept d'adressage IPv6, pas un type d'adresse MAC.

**💡 Point clé :** Adresses multicast MAC :
- IPv4 multicast : Commence par 01:00:5E
- IPv6 multicast : Commence par 33:33

---

## Question 15
**Réponse correcte : C**

**Explication :**
La topologie **Mesh complet (Full mesh)** offre la redondance maximale car chaque site est directement connecté à tous les autres sites. Si un lien tombe, plusieurs chemins alternatifs existent.

**💡 Point clé :** Nombre de liens en full mesh : n(n-1)/2 où n = nombre de sites
- 3 sites : 3 liens
- 4 sites : 6 liens
- 5 sites : 10 liens

Cette topologie est coûteuse mais offre la meilleure disponibilité, d'où son utilisation dans les réseaux critiques.

---

## Question 16
**Réponse correcte : C**

**Explication :**
Lorsqu'une trame a un FCS invalide (erreur de transmission détectée), elle est **rejetée (jetée)** immédiatement par le commutateur ou la carte réseau. La couche 2 ne corrige pas et ne retransmet pas les erreurs.

**💡 Point clé :** Le processus :
1. Réception de la trame
2. Calcul du FCS sur les données reçues
3. Comparaison avec le FCS reçu
4. Si différent → trame jetée (dropped)
5. Pas d'accusé de réception au niveau couche 2

La retransmission éventuelle est gérée par TCP (Couche 4) si nécessaire.

---

## Question 17
**Réponse correcte : B**

**Explication :**
Le statut **"administratively down"** signifie que l'interface a été désactivée volontairement par un administrateur avec la commande `shutdown`. C'est un état intentionnel, pas une panne.

**💡 Point clé :** Pour réactiver une interface :
```cisco
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# no shutdown
```

Par défaut, les interfaces de switch Cisco sont activées (up), mais les interfaces de routeur sont désactivées (shutdown).

---

**Score recommandé pour valider le module : 13/17 minimum (76%)**

**Révision conseillée si score < 13/17 :**
- Section 6.1 (Rôle de la couche liaison de données)
- Section 6.2 (Topologies réseau)
- Section 6.3 (Structure de la trame)
- Pratiquer avec `show interfaces` et `show mac address-table` dans Packet Tracer
