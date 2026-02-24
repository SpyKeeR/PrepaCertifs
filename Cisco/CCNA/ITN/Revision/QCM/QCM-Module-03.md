# QCM - Module 03 : Modèles et protocoles
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **18 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Combien de couches comporte le modèle OSI ?

- [ ] A. 4 couches
- [ ] B. 5 couches
- [ ] C. 7 couches
- [ ] D. 9 couches

### Question 2
Quelle couche du modèle OSI est responsable de l'adressage logique (IP) et du routage ?

- [ ] A. Couche 2 - Liaison de données
- [ ] B. Couche 3 - Réseau
- [ ] C. Couche 4 - Transport
- [ ] D. Couche 7 - Application

### Question 3
Quels protocoles fonctionnent à la couche Transport (Couche 4) du modèle OSI ?

- [ ] A. TCP
- [ ] B. IP
- [ ] C. UDP
- [ ] D. HTTP

### Question 4
Quel est le PDU (Protocol Data Unit) de la couche Transport ?

- [ ] A. Trame (Frame)
- [ ] B. Paquet (Packet)
- [ ] C. Segment (Segment)
- [ ] D. Bits

### Question 5
Quel standard IEEE définit les réseaux Wi-Fi ?

- [ ] A. IEEE 802.3
- [ ] B. IEEE 802.11
- [ ] C. IEEE 802.1Q
- [ ] D. IEEE 802.5

### Question 6
Quel organisme est responsable du développement et de la maintenance des standards Internet (RFC) ?

- [ ] A. IEEE
- [ ] B. ISO
- [ ] C. IETF
- [ ] D. ICANN

### Question 7
Dans le modèle TCP/IP, combien y a-t-il de couches ?

- [ ] A. 3 couches
- [ ] B. 4 couches
- [ ] C. 5 couches
- [ ] D. 7 couches

### Question 8
Quelle couche du modèle OSI est responsable de la détection d'erreurs avec le CRC (Frame Check Sequence) ?

- [ ] A. Couche 1 - Physique
- [ ] B. Couche 2 - Liaison de données
- [ ] C. Couche 3 - Réseau
- [ ] D. Couche 4 - Transport

### Question 9
Quels sont les avantages d'utiliser un modèle en couches pour les réseaux ?

- [ ] A. Modularité - chaque couche a un rôle spécifique
- [ ] B. Interopérabilité - standards communs entre fabricants
- [ ] C. Facilité de dépannage - isolation des problèmes par couche
- [ ] D. Coût réduit des équipements

### Question 10
Le protocole HTTP fonctionne à quelle couche du modèle OSI ?

- [ ] A. Couche 2
- [ ] B. Couche 4
- [ ] C. Couche 6
- [ ] D. Couche 7

### Question 11
Quel est le PDU (Protocol Data Unit) de la couche Liaison de données ?

- [ ] A. Segment
- [ ] B. Paquet
- [ ] C. Trame
- [ ] D. Données

### Question 12
Quel protocole est utilisé pour la résolution de noms de domaine (conversion nom → IP) ?

- [ ] A. DHCP
- [ ] B. DNS
- [ ] C. ARP
- [ ] D. HTTP

### Question 13
Dans le processus d'encapsulation, que se passe-t-il lorsque les données descendent du modèle OSI ?

- [ ] A. Chaque couche supprime un en-tête
- [ ] B. Chaque couche ajoute son propre en-tête
- [ ] C. Les données sont chiffrées
- [ ] D. Les données sont compressées

### Question 14
Lors d'une communication entre deux réseaux distants, quelle adresse change à chaque saut (routeur) ?

- [ ] A. Adresse IP source
- [ ] B. Adresse IP destination
- [ ] C. Adresse MAC source
- [ ] D. Adresse MAC destination

### Question 15
Que signifie "RFC" dans le contexte des standards Internet ?

- [ ] A. Real Fast Communication
- [ ] B. Request For Comments
- [ ] C. Router Function Code
- [ ] D. Reliable Frame Control

### Question 16
Quel protocole de la couche Application est utilisé pour le transfert de fichiers ?

- [ ] A. HTTP
- [ ] B. SMTP
- [ ] C. FTP
- [ ] D. Telnet

### Question 17
Quelle couche du modèle OSI est responsable de la segmentation et du réassemblage des données ?

- [ ] A. Couche 3 - Réseau
- [ ] B. Couche 4 - Transport
- [ ] C. Couche 5 - Session
- [ ] D. Couche 7 - Application

### Question 18
Lequel de ces protocoles est considéré comme un protocole ouvert ?

- [ ] A. TCP/IP
- [ ] B. HTTP
- [ ] C. Cisco EIGRP (historiquement)
- [ ] D. SMTP

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : C**

**Explication :**
Le modèle OSI (Open Systems Interconnection) comporte **7 couches** : Application, Présentation, Session, Transport, Réseau, Liaison de données, et Physique. Le modèle TCP/IP en a 4.

**💡 Point clé :** Mnémotechnique pour retenir les 7 couches (de bas en haut) : "Please Do Not Throw Sausage Pizza Away" (Physical, Data Link, Network, Transport, Session, Presentation, Application).

---

## Question 2
**Réponse correcte : B**

**Explication :**
La **Couche 3 - Réseau** est responsable de l'adressage logique (adresses IP) et du routage des paquets entre réseaux. Les protocoles de cette couche incluent IP, ICMP, OSPF, EIGRP.

**💡 Point clé :** La couche Réseau détermine le meilleur chemin pour acheminer les paquets de la source à la destination, même si elles sont sur des réseaux différents. C'est la couche des routeurs.

---

## Question 3
**Réponses correctes : A, C**

**Explication :**
TCP (Transmission Control Protocol) et UDP (User Datagram Protocol) fonctionnent à la couche Transport (Couche 4). IP fonctionne à la couche Réseau (Couche 3), et HTTP à la couche Application (Couche 7).

**💡 Point clé :** TCP est fiable et orienté connexion (garantit la livraison), tandis qu'UDP est non fiable mais plus rapide (pas de garantie de livraison). Utilisez TCP pour les données critiques, UDP pour les flux temps réel (VoIP, streaming).

---

## Question 4
**Réponse correcte : C**

**Explication :**
Le PDU de la couche Transport est le **Segment** (pour TCP) ou **Datagramme** (pour UDP). Les autres PDU : Trame (Couche 2), Paquet (Couche 3), Bits (Couche 1), Données (Couche 5-7).

**💡 Point clé :** Mémorisez les PDU par couche :
- Couche 5-7 : **Données**
- Couche 4 : **Segment/Datagramme**
- Couche 3 : **Paquet**
- Couche 2 : **Trame**
- Couche 1 : **Bits**

---

## Question 5
**Réponse correcte : B**

**Explication :**
Le standard **IEEE 802.11** définit les réseaux Wi-Fi (WLAN). Les autres standards : 802.3 (Ethernet), 802.1Q (VLANs), 802.5 (Token Ring - obsolète).

**💡 Point clé :** Les variantes 802.11 à connaître : 802.11a/b/g/n/ac/ax (Wi-Fi 6). Chaque génération apporte plus de vitesse et de fonctionnalités.

---

## Question 6
**Réponse correcte : C**

**Explication :**
L'**IETF** (Internet Engineering Task Force) développe et maintient les standards Internet publiés sous forme de RFC (Request For Comments). IEEE gère les standards LAN, ISO le modèle OSI, et ICANN les noms de domaine et adresses IP.

**💡 Point clé :** Les RFC sont des documents numérotés qui définissent les protocoles Internet. Exemples : RFC 791 (IPv4), RFC 2460 (IPv6), RFC 793 (TCP).

---

## Question 7
**Réponse correcte : B**

**Explication :**
Le modèle TCP/IP comporte **4 couches** : Application, Transport, Internet, et Accès réseau. C'est le modèle pratique utilisé sur Internet, par opposition au modèle OSI qui est théorique avec 7 couches.

**💡 Point clé :** Le modèle TCP/IP regroupe les couches hautes de l'OSI (5, 6, 7) en une seule couche Application, et les couches basses (1, 2) en une couche Accès réseau.

---

## Question 8
**Réponse correcte : B**

**Explication :**
La **Couche 2 - Liaison de données** est responsable de la détection d'erreurs grâce au FCS (Frame Check Sequence) qui utilise un calcul CRC-32. Elle détecte les trames corrompues mais ne les corrige pas, elle les rejette.

**💡 Point clé :** Le FCS est calculé sur l'ensemble de la trame par l'émetteur et placé dans le trailer. Le récepteur recalcule le FCS : si le résultat diffère, la trame est jetée. La retransmission est gérée par les couches supérieures (TCP).

---

## Question 9
**Réponses correctes : A, B, C**

**Explication :**
Les avantages des modèles en couches incluent :
- **Modularité (A)** : Chaque couche a un rôle spécifique et indépendant
- **Interopérabilité (B)** : Standards permettant aux équipements de différents fabricants de communiquer
- **Facilité de dépannage (C)** : On peut isoler les problèmes par couche

Le coût (D) n'est pas un avantage direct du modèle en couches.

**💡 Point clé :** Les modèles en couches facilitent également l'évolution : on peut modifier une couche sans affecter les autres, tant que les interfaces entre couches restent stables.

---

## Question 10
**Réponse correcte : D**

**Explication :**
HTTP (HyperText Transfer Protocol) fonctionne à la **Couche 7 - Application**. C'est le protocole utilisé pour la navigation web.

**💡 Point clé :** D'autres protocoles de couche Application : HTTPS (HTTP sécurisé), FTP (transfert fichiers), SMTP (email), DNS (résolution noms), Telnet/SSH (accès distant), DHCP (attribution IP).

---

## Question 11
**Réponse correcte : C**

**Explication :**
Le PDU de la couche Liaison de données est la **Trame** (Frame). Elle contient les adresses MAC source/destination, les données encapsulées (paquet de couche 3), et le FCS pour la détection d'erreurs.

**💡 Point clé :** La trame est spécifique au type de média : trame Ethernet sur Ethernet, trame PPP sur liaison série, trame 802.11 sur Wi-Fi. Le format varie mais le concept reste le même.

---

## Question 12
**Réponse correcte : B**

**Explication :**
**DNS** (Domain Name System) est le protocole utilisé pour résoudre les noms de domaine en adresses IP (ex: www.google.com → 142.250.185.46). DHCP attribue des IP, ARP résout IP → MAC, HTTP transfère des pages web.

**💡 Point clé :** DNS fonctionne généralement sur le port UDP 53. C'est un service essentiel : sans DNS, vous devriez mémoriser les adresses IP de tous les sites web !

---

## Question 13
**Réponse correcte : B**

**Explication :**
Lors de l'encapsulation, lorsque les données descendent les couches du modèle OSI, **chaque couche ajoute son propre en-tête** (header) avec ses informations de contrôle. C'est le processus inverse lors de la désencapsulation (réception).

**💡 Point clé :** Encapsulation (émission) : Données → +En-tête Transport → +En-tête IP → +En-tête Ethernet → Bits. Désencapsulation (réception) : Bits → -En-tête Ethernet → -En-tête IP → -En-tête Transport → Données.

---

## Question 14
**Réponses correctes : C, D**

**Explication :**
Lors d'une communication entre réseaux distants, les **adresses MAC source (C) et destination (D)** changent à chaque saut (chaque routeur). Les adresses IP source et destination restent identiques de bout en bout.

**💡 Point clé :** Les adresses MAC ne sont utilisées que pour la livraison locale (même réseau). À chaque routeur, la trame est désencapsulée, le routeur examine l'IP destination, consulte sa table de routage, puis réencapsule le paquet dans une nouvelle trame avec de nouvelles adresses MAC.

---

## Question 15
**Réponse correcte : B**

**Explication :**
**RFC** signifie "Request For Comments". Ce sont des documents techniques et organisationnels publiés par l'IETF qui définissent les standards Internet.

**💡 Point clé :** Malgré leur nom "Request for Comments", les RFC approuvés deviennent des standards officiels. Exemples : RFC 791 (IPv4), RFC 826 (ARP), RFC 2328 (OSPF).

---

## Question 16
**Réponse correcte : C**

**Explication :**
**FTP** (File Transfer Protocol) est utilisé pour le transfert de fichiers. HTTP transfère des pages web, SMTP envoie des emails, et Telnet permet l'accès distant en ligne de commande.

**💡 Point clé :** FTP utilise deux connexions : une pour les commandes (port 21) et une pour les données (port 20 en mode actif). SFTP (SSH File Transfer Protocol) est la version sécurisée recommandée aujourd'hui.

---

## Question 17
**Réponse correcte : B**

**Explication :**
La **Couche 4 - Transport** est responsable de la segmentation (découpage) des données en segments lors de l'émission, et du réassemblage de ces segments dans le bon ordre lors de la réception.

**💡 Point clé :** La segmentation est nécessaire car les couches inférieures ont des limites de taille (MTU). TCP utilise des numéros de séquence pour garantir le réassemblage dans l'ordre correct, même si les segments arrivent dans le désordre.

---

## Question 18
**Réponses correctes : A, B, D**

**Explication :**
TCP/IP (A), HTTP (B), et SMTP (D) sont des protocoles ouverts, c'est-à-dire des standards publics permettant l'interopérabilité entre différents fabricants. EIGRP (C) était historiquement un protocole propriétaire Cisco (bien qu'ouvert depuis 2013).

**💡 Point clé :** Les protocoles ouverts sont essentiels pour Internet car ils permettent à tout le monde de les implémenter. Les protocoles propriétaires donnent un contrôle exclusif au fabricant mais limitent l'interopérabilité.

---

**Score recommandé pour valider le module : 14/18 minimum (78%)**

**Révision conseillée si score < 14/18 :**
- Section 3.5 (Modèles OSI et TCP/IP)
- Section 3.6 (Encapsulation de données)
- Section 3.7 (Adresses réseau)
- Créer un schéma visuel des 7 couches OSI avec les PDU
