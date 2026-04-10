# QCM Module 14 - Protocoles de Transport (TCP/UDP)

**Nombre de questions :** 20  
**Durée estimée :** 30 minutes  
**Seuil de réussite :** 75% (15/20)

---

## Question 1
Quelle est la taille **minimale** de l'en-tête TCP ? (Choix unique)

- [ ] 8 octets
- [ ] 16 octets
- [ ] 20 octets
- [ ] 60 octets

---

## Question 2
Quels sont les rôles du protocole TCP ? (Choix multiples - Sélectionner 3 réponses)

- [ ] Établissement de connexion avec 3-way handshake
- [ ] Transmission rapide sans garantie de livraison
- [ ] Contrôle de flux avec fenêtre glissante
- [ ] Support du multicast et broadcast
- [ ] Fiabilité avec accusés de réception et retransmissions

---

## Question 3
Dans l'en-tête TCP, quel champ indique le **numéro du premier octet de données** dans le segment ? (Choix unique)

- [ ] Acknowledgment Number
- [ ] Sequence Number
- [ ] Data Offset
- [ ] Window Size

---

## Question 4
Le champ **Window Size** de l'en-tête TCP sert à : (Choix unique)

- [ ] Contrôler la congestion du réseau
- [ ] Indiquer le nombre de segments en attente
- [ ] Contrôler le flux en spécifiant la taille du buffer du récepteur
- [ ] Détecter les erreurs de transmission

---

## Question 5
Quels sont les **flags TCP** utilisés lors du 3-way handshake ? (Choix multiples - Sélectionner 3 réponses)

- [ ] SYN
- [ ] ACK
- [ ] FIN
- [ ] RST
- [ ] PSH

---

## Question 6
Dans le 3-way handshake TCP, quelle est la **séquence correcte** des étapes ? (Choix unique)

- [ ] SYN → ACK → SYN-ACK
- [ ] SYN → SYN-ACK → ACK
- [ ] ACK → SYN → SYN-ACK
- [ ] SYN-ACK → SYN → ACK

---

## Question 7
Un client envoie un segment TCP avec **SEQ=2000** contenant **150 octets de données**. Quel sera le numéro **ACK** renvoyé par le serveur s'il reçoit correctement le segment ? (Choix unique)

- [ ] ACK=2000
- [ ] ACK=2001
- [ ] ACK=2150
- [ ] ACK=2151

---

## Question 8
Pendant le 4-way termination TCP, quel flag est utilisé pour demander la fermeture de la connexion ? (Choix unique)

- [ ] SYN
- [ ] ACK
- [ ] FIN
- [ ] RST

---

## Question 9
Un récepteur annonce une **Window Size = 8000 octets** et le **MSS = 1600 octets**. Combien de segments l'émetteur peut-il envoyer **sans attendre d'ACK** ? (Choix unique)

- [ ] 4 segments
- [ ] 5 segments
- [ ] 6 segments
- [ ] 8 segments

---

## Question 10
Lors du **Slow Start** en contrôle de congestion TCP, comment évolue la fenêtre de congestion (CWND) ? (Choix unique)

- [ ] Elle reste constante
- [ ] Elle augmente de 1 MSS par RTT (croissance linéaire)
- [ ] Elle double à chaque ACK (croissance exponentielle)
- [ ] Elle diminue de moitié à chaque perte

---

## Question 11
Quelles sont les différences entre TCP et UDP ? (Choix multiples - Sélectionner 3 réponses)

- [ ] TCP est orienté connexion, UDP est sans connexion
- [ ] TCP a un en-tête de 8 octets, UDP de 20 octets
- [ ] TCP garantit la fiabilité, UDP ne garantit pas la livraison
- [ ] TCP supporte le broadcast, UDP non
- [ ] TCP est plus lent mais fiable, UDP est plus rapide mais non fiable

---

## Question 12
Quelle est la taille de l'en-tête UDP ? (Choix unique)

- [ ] 4 octets
- [ ] 8 octets
- [ ] 20 octets
- [ ] 32 octets

---

## Question 13
Dans l'en-tête UDP, le champ **Checksum** est : (Choix unique)

- [ ] Obligatoire en IPv4 et IPv6
- [ ] Optionnel en IPv4, obligatoire en IPv6
- [ ] Optionnel en IPv4 et IPv6
- [ ] Obligatoire en IPv4, optionnel en IPv6

---

## Question 14
Quel protocole de transport (TCP ou UDP) est le plus approprié pour une application de **VoIP** (Voice over IP) ? (Choix unique)

- [ ] TCP, car la fiabilité est critique pour la voix
- [ ] TCP, car il gère mieux les pertes de paquets
- [ ] UDP, car la vitesse et le temps réel sont prioritaires
- [ ] UDP, car il gère automatiquement la retransmission

---

## Question 15
Parmi ces ports, lesquels utilisent le protocole **TCP** ? (Choix multiples - Sélectionner 4 réponses)

- [ ] 22 (SSH)
- [ ] 53 (DNS)
- [ ] 80 (HTTP)
- [ ] 443 (HTTPS)
- [ ] 67 (DHCP)
- [ ] 3389 (RDP)

---

## Question 16
Comment est calculé le **MSS (Maximum Segment Size)** typique pour Ethernet ? (Choix unique)

- [ ] MSS = MTU = 1500 octets
- [ ] MSS = MTU - IP Header = 1500 - 20 = 1480 octets
- [ ] MSS = MTU - IP Header - TCP Header = 1500 - 20 - 20 = 1460 octets
- [ ] MSS = MTU + TCP Header = 1500 + 20 = 1520 octets

---

## Question 17
Lorsque TCP détecte **3 ACK dupliqués**, quelle action est entreprise ? (Choix unique)

- [ ] La connexion est réinitialisée avec un flag RST
- [ ] L'émetteur attend le timeout avant de retransmettre
- [ ] Fast Retransmit : retransmission immédiate du segment perdu
- [ ] Slow Start : CWND revient à 1 MSS

---

## Question 18
Quelles sont les caractéristiques du flag **PSH** (Push) dans TCP ? (Choix unique)

- [ ] Il demande l'établissement d'une connexion
- [ ] Il indique que les données doivent être envoyées immédiatement au processus applicatif
- [ ] Il termine proprement la connexion TCP
- [ ] Il signale une réinitialisation brutale de la connexion

---

## Question 19
Parmi ces services, lesquels utilisent le protocole **UDP** ? (Choix multiples - Sélectionner 4 réponses)

- [ ] DNS (résolution de noms)
- [ ] DHCP (allocation d'adresses IP)
- [ ] FTP (transfert de fichiers)
- [ ] TFTP (transfert de fichiers simple)
- [ ] HTTPS (web sécurisé)
- [ ] NTP (synchronisation horloge)

---

## Question 20
Dans le contrôle de congestion TCP, lorsque la fenêtre de congestion (CWND) atteint le seuil **ssthresh**, quel mode est activé ? (Choix unique)

- [ ] Slow Start avec croissance exponentielle
- [ ] Congestion Avoidance avec croissance linéaire
- [ ] Fast Recovery avec maintien de CWND
- [ ] Fast Retransmit avec retour à CWND = 1

---

## Réponses et explications

### Question 1
**Réponse correcte :** C (20 octets)

**Explication :**  
L'en-tête TCP a une taille **minimale de 20 octets** sans options. Il peut atteindre jusqu'à 60 octets avec des options (MSS, Window Scale, SACK, Timestamps). Le champ **Data Offset** (4 bits) indique la longueur de l'en-tête en mots de 32 bits (minimum 5 = 5 × 4 = 20 octets).

---

### Question 2
**Réponses correctes :** A, C, E

**Explication :**  
TCP est un protocole **orienté connexion** qui établit une connexion avec le 3-way handshake (A). Il assure la **fiabilité** avec des ACK et des retransmissions en cas de perte (E). Il implémente le **contrôle de flux** avec la fenêtre glissante (Window Size) pour éviter de surcharger le récepteur (C). TCP ne supporte **pas** le multicast/broadcast (réservé à UDP) et privilégie la fiabilité sur la vitesse.

---

### Question 3
**Réponse correcte :** B (Sequence Number)

**Explication :**  
Le champ **Sequence Number (SEQ)** sur 32 bits indique le numéro du **premier octet de données** contenu dans le segment TCP. Il permet de réordonner les segments reçus dans le désordre et de détecter les pertes. L'**Acknowledgment Number (ACK)** indique le prochain octet attendu (acquittement cumulatif).

---

### Question 4
**Réponse correcte :** C

**Explication :**  
Le champ **Window Size** (16 bits) indique la taille du buffer de réception du récepteur, en octets. Il sert au **contrôle de flux** pour éviter que l'émetteur n'envoie plus de données que le récepteur ne peut en traiter. Si Window Size = 0, l'émetteur doit arrêter d'envoyer. C'est différent du **contrôle de congestion** qui protège le réseau (et non le récepteur).

---

### Question 5
**Réponses correctes :** A, B

**Explication :**  
Le 3-way handshake utilise les flags **SYN** et **ACK** :
1. Client → Serveur : **SYN** (SEQ=X)
2. Serveur → Client : **SYN-ACK** (SEQ=Y, ACK=X+1)
3. Client → Serveur : **ACK** (ACK=Y+1)

Les flags FIN (fermeture), RST (reset) et PSH (push) ne sont **pas** utilisés lors de l'établissement de connexion.

---

### Question 6
**Réponse correcte :** B (SYN → SYN-ACK → ACK)

**Explication :**  
Le 3-way handshake TCP suit toujours cet ordre :
1. **SYN** : Le client initie la connexion
2. **SYN-ACK** : Le serveur accepte et renvoie son propre SYN
3. **ACK** : Le client acquitte le SYN du serveur

Après ces 3 étapes, la connexion est **ESTABLISHED** et le transfert de données peut commencer.

---

### Question 7
**Réponse correcte :** C (ACK=2150)

**Explication :**  
Le numéro **ACK** indique le **prochain octet attendu** (acquittement cumulatif). Si le client envoie SEQ=2000 avec 150 octets de données, cela signifie qu'il envoie les octets 2000 à 2149. Le serveur répond donc avec **ACK=2150** pour indiquer qu'il attend l'octet 2150 (donc il a bien reçu jusqu'à 2149).

Formule : **ACK = SEQ + Nombre d'octets**

---

### Question 8
**Réponse correcte :** C (FIN)

**Explication :**  
Le flag **FIN (Finish)** est utilisé pour **terminer proprement** une connexion TCP. Le 4-way termination fonctionne ainsi :
1. **FIN** : Une partie demande la fermeture
2. **ACK** : L'autre partie acquitte
3. **FIN** : L'autre partie demande aussi la fermeture
4. **ACK** : Acquittement final

Le flag **RST** (Reset) est utilisé pour une fermeture **brutale** (erreur, port fermé, attaque).

---

### Question 9
**Réponse correcte :** B (5 segments)

**Explication :**  
Le calcul est simple :
```
Window Size = 8000 octets
MSS = 1600 octets
Nombre de segments = 8000 / 1600 = 5 segments
```

L'émetteur peut envoyer **5 segments** (5 × 1600 = 8000 octets) avant de devoir attendre un ACK. C'est le principe de la **fenêtre glissante** pour le contrôle de flux.

---

### Question 10
**Réponse correcte :** C (Elle double à chaque ACK - croissance exponentielle)

**Explication :**  
Lors du **Slow Start**, la fenêtre de congestion (CWND) commence à 1 MSS et **double à chaque ACK reçu** :
- CWND = 1 MSS → Envoie 1 segment
- ACK reçu → CWND = 2 MSS
- Envoie 2 segments → CWND = 4 MSS
- Envoie 4 segments → CWND = 8 MSS

C'est une **croissance exponentielle** rapide. Lorsque CWND atteint **ssthresh**, TCP passe en mode **Congestion Avoidance** avec croissance linéaire (+1 MSS par RTT).

---

### Question 11
**Réponses correctes :** A, C, E

**Explication :**  
- **TCP** est orienté connexion (3-way handshake), **UDP** est sans connexion (A)
- **TCP** garantit la fiabilité (ACK, retransmissions), **UDP** ne garantit pas la livraison (best effort) (C)
- **TCP** est plus lent mais fiable (overhead élevé), **UDP** est plus rapide mais non fiable (E)

Les erreurs :
- TCP a un en-tête de **20-60 octets**, UDP de **8 octets** (pas l'inverse)
- **UDP** supporte broadcast/multicast, **TCP** non

---

### Question 12
**Réponse correcte :** B (8 octets)

**Explication :**  
L'en-tête UDP est **très simple et compact** : seulement **8 octets** composés de 4 champs :
- **Source Port** (16 bits / 2 octets)
- **Destination Port** (16 bits / 2 octets)
- **Length** (16 bits / 2 octets)
- **Checksum** (16 bits / 2 octets)

Cette simplicité rend UDP **rapide et léger**, parfait pour les applications temps réel (VoIP, streaming).

---

### Question 13
**Réponse correcte :** B (Optionnel en IPv4, obligatoire en IPv6)

**Explication :**  
Le champ **Checksum** dans UDP :
- **IPv4** : **Optionnel** (peut être mis à 0 si non calculé)
- **IPv6** : **Obligatoire** (RFC 2460)

Le checksum vérifie l'intégrité de l'en-tête UDP + données + pseudo-en-tête IP. Si le checksum est incorrect, le datagramme est **éliminé silencieusement** (pas d'erreur renvoyée).

---

### Question 14
**Réponse correcte :** C (UDP, car la vitesse et le temps réel sont prioritaires)

**Explication :**  
La **VoIP** (Voice over IP) nécessite :
- **Faible latence** : transmission en temps réel
- **Quelques pertes acceptables** : l'oreille humaine tolère de petites pertes
- **Pas de retransmissions** : un paquet en retard est inutile pour la voix

**UDP** est donc le meilleur choix car il est **rapide, léger** et n'a pas l'overhead de TCP (pas d'ACK, pas de retransmissions). TCP serait trop lent et causerait des délais inacceptables pour la voix.

---

### Question 15
**Réponses correctes :** A, C, D, F

**Explication :**  
Les ports utilisant **TCP** :
- **22 (SSH)** : Accès distant sécurisé
- **80 (HTTP)** : Web non sécurisé
- **443 (HTTPS)** : Web sécurisé
- **3389 (RDP)** : Bureau à distance Windows

Les ports utilisant **UDP** :
- **53 (DNS)** : Requêtes DNS (utilise aussi TCP pour transferts de zones)
- **67 (DHCP)** : Serveur DHCP

---

### Question 16
**Réponse correcte :** C (MSS = 1460 octets)

**Explication :**  
Le **MSS (Maximum Segment Size)** est la taille maximale des **données** dans un segment TCP (sans compter les en-têtes). Le calcul pour Ethernet :

```
MSS = MTU - En-tête IP - En-tête TCP
MSS = 1500 - 20 - 20 = 1460 octets
```

- **MTU** : 1500 octets (Maximum Transmission Unit pour Ethernet)
- **En-tête IP** : 20 octets (sans options)
- **En-tête TCP** : 20 octets (minimum)

Le MSS est **négocié lors du 3-way handshake** via l'option TCP MSS.

---

### Question 17
**Réponse correcte :** C (Fast Retransmit)

**Explication :**  
Lorsque TCP reçoit **3 ACK dupliqués** (même numéro ACK répété 3 fois), cela indique qu'un segment est probablement **perdu**. Au lieu d'attendre le timeout (qui prendrait du temps), TCP utilise le mécanisme **Fast Retransmit** :
- **Retransmission immédiate** du segment perdu (sans attendre)
- Puis **Fast Recovery** : CWND = ssthresh (pas de retour à CWND=1)

C'est plus efficace que d'attendre le timer de retransmission.

---

### Question 18
**Réponse correcte :** B

**Explication :**  
Le flag **PSH (Push)** indique que les données doivent être **envoyées immédiatement au processus applicatif**, sans attendre que le buffer soit plein. Cela permet de traiter les données **urgentes** ou interactives (ex : commande Telnet, requête HTTP).

Les autres flags :
- **SYN** : Établissement de connexion
- **FIN** : Fermeture propre
- **RST** : Réinitialisation brutale

---

### Question 19
**Réponses correctes :** A, B, D, F

**Explication :**  
Les services utilisant **UDP** :
- **DNS (53)** : Résolution de noms (requêtes rapides < 512 octets)
- **DHCP (67-68)** : Allocation d'adresses IP (broadcast)
- **TFTP (69)** : Transfert de fichiers simple
- **NTP (123)** : Synchronisation de l'horloge

Les services utilisant **TCP** :
- **FTP (20-21)** : Transfert de fichiers (fiabilité critique)
- **HTTPS (443)** : Web sécurisé (intégrité des données)

---

### Question 20
**Réponse correcte :** B (Congestion Avoidance avec croissance linéaire)

**Explication :**  
Le contrôle de congestion TCP fonctionne en deux phases :

1. **Slow Start** : CWND double à chaque ACK (croissance exponentielle) jusqu'à atteindre **ssthresh**
2. **Congestion Avoidance** : Lorsque CWND ≥ ssthresh, croissance **linéaire** (+1 MSS par RTT)

Si une perte est détectée :
- **ssthresh = CWND / 2**
- **CWND = 1 MSS** (recommence Slow Start)

Cela permet d'éviter de saturer le réseau tout en maximisant le débit.

---

**Fin du QCM Module 14**

**Score de passage :** 15/20 (75%)  
**Bonne chance !** 🚀
