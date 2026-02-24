# QCM - Module 07 : Commutation Ethernet
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **20 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Combien d'octets contient une adresse MAC ?

- [ ] A. 4 octets (32 bits)
- [ ] B. 6 octets (48 bits)
- [ ] C. 8 octets (64 bits)
- [ ] D. 16 octets (128 bits)

### Question 2
Dans une adresse MAC, que représente l'OUI (Organizationally Unique Identifier) ?

- [ ] A. Les 3 premiers octets identifiant le fabricant
- [ ] B. Les 3 derniers octets identifiant le périphérique
- [ ] C. L'adresse complète de 6 octets
- [ ] D. Le numéro de série unique

### Question 3
Quelle est l'adresse MAC de broadcast Ethernet ?

- [ ] A. 00:00:00:00:00:00
- [ ] B. FF:FF:FF:FF:FF:FF
- [ ] C. 01:00:5E:00:00:00
- [ ] D. 255.255.255.255

### Question 4
Quelle est la taille minimale d'une trame Ethernet (sans compter le préambule et le SFD) ?

- [ ] A. 46 octets
- [ ] B. 64 octets
- [ ] C. 128 octets
- [ ] D. 1500 octets

### Question 5
Quelle est la taille maximale d'une trame Ethernet standard (sans préambule et SFD) ?

- [ ] A. 1500 octets
- [ ] B. 1518 octets
- [ ] C. 9000 octets
- [ ] D. 65535 octets

### Question 6
Quel champ de la trame Ethernet est utilisé pour la détection d'erreurs ?

- [ ] A. Préambule
- [ ] B. SFD (Start Frame Delimiter)
- [ ] C. EtherType
- [ ] D. FCS (Frame Check Sequence)

### Question 7
Quel format d'adresse MAC indique une adresse multicast IPv4 ?

- [ ] A. 00:00:5E:--:--:--
- [ ] B. 01:00:5E:--:--:--
- [ ] C. 33:33:--:--:--:--
- [ ] D. FF:FF:FF:FF:FF:FF

### Question 8
Quel format d'adresse MAC indique une adresse multicast IPv6 ?

- [ ] A. 01:00:5E:--:--:--
- [ ] B. 33:33:--:--:--:--
- [ ] C. FF:02:--:--:--:--
- [ ] D. FF:FF:FF:FF:FF:FF

### Question 9
Comment un commutateur apprend-il les adresses MAC ?

- [ ] A. En examinant l'adresse MAC source des trames reçues
- [ ] B. En examinant l'adresse MAC de destination des trames reçues
- [ ] C. Par configuration manuelle uniquement
- [ ] D. En envoyant des requêtes ARP

### Question 10
Que fait un commutateur lorsqu'il reçoit une trame avec une adresse MAC de destination qu'il ne connaît pas ?

- [ ] A. Il jette la trame
- [ ] B. Il envoie la trame sur tous les ports sauf le port source (flooding)
- [ ] C. Il envoie une requête ARP
- [ ] D. Il stocke la trame en attendant d'apprendre l'adresse

### Question 11
Quelle commande affiche la table d'adresses MAC d'un commutateur Cisco ?

- [ ] A. `show arp`
- [ ] B. `show mac`
- [ ] C. `show mac address-table`
- [ ] D. `show mac-table`

### Question 12
Quelle est la durée par défaut (en secondes) avant qu'une entrée de la table MAC n'expire si aucune trame n'est reçue de cette adresse ?

- [ ] A. 60 secondes
- [ ] B. 180 secondes
- [ ] C. 300 secondes
- [ ] D. 600 secondes

### Question 13
Quelle méthode de commutation reçoit la trame complète et vérifie le FCS avant de la transférer ?

- [ ] A. Cut-Through
- [ ] B. Fast-Forward
- [ ] C. Store-and-Forward
- [ ] D. Fragment-Free

### Question 14
Quelle méthode de commutation offre la latence la plus faible mais ne détecte pas les erreurs ?

- [ ] A. Store-and-Forward
- [ ] B. Cut-Through
- [ ] C. Half-Duplex
- [ ] D. Full-Duplex

### Question 15
Dans quel mode de transmission deux périphériques peuvent-ils émettre et recevoir simultanément ?

- [ ] A. Simplex
- [ ] B. Half-Duplex
- [ ] C. Full-Duplex
- [ ] D. Auto-Duplex

### Question 16
Quel protocole est utilisé en mode Half-Duplex pour détecter et gérer les collisions ?

- [ ] A. CSMA/CA
- [ ] B. CSMA/CD
- [ ] C. ARP
- [ ] D. STP

### Question 17
Que permet la technologie Auto-MDIX sur un commutateur moderne ?

- [ ] A. Négociation automatique de la vitesse
- [ ] B. Détection automatique du type de câble (droit ou croisé)
- [ ] C. Chiffrement automatique des trames
- [ ] D. Attribution automatique d'adresses IP

### Question 18
Combien d'octets contient le champ de données (payload) minimum dans une trame Ethernet ?

- [ ] A. 1 octet
- [ ] B. 46 octets
- [ ] C. 64 octets
- [ ] D. 1500 octets

### Question 19
Quel standard définit Gigabit Ethernet sur câble cuivre ?

- [ ] A. 10BASE-T
- [ ] B. 100BASE-TX
- [ ] C. 1000BASE-T
- [ ] D. 10GBASE-T

### Question 20
Que signifie "MTU" dans le contexte d'Ethernet ?

- [ ] A. Maximum Transmission Unit (taille maximale des données dans une trame)
- [ ] B. Minimum Transfer Unit
- [ ] C. Media Type Utilization
- [ ] D. Multi-Trunk Unit

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : B**

**Explication :**
Une adresse MAC contient **6 octets (48 bits)**. Elle est généralement représentée en hexadécimal : XX:XX:XX:XX:XX:XX.

**💡 Point clé :** Format : 3 premiers octets = OUI (fabricant), 3 derniers octets = numéro de série du périphérique. Exemple : 00:1A:2B:3C:4D:5E.

---

## Question 2
**Réponse correcte : A**

**Explication :**
L'**OUI (Organizationally Unique Identifier)** représente les **3 premiers octets** de l'adresse MAC et identifie le fabricant du matériel. Il est attribué par l'IEEE.

**💡 Point clé :** Exemples d'OUI :
- 00:1A:2B : Cisco (certains modèles)
- 00:50:56 : VMware
- 08:00:27 : VirtualBox

Les 3 derniers octets sont le Device ID (numéro de série unique).

---

## Question 3
**Réponse correcte : B**

**Explication :**
L'adresse MAC de broadcast est **FF:FF:FF:FF:FF:FF** (tous les bits à 1). Tous les périphériques du réseau local reçoivent et traitent les trames envoyées à cette adresse.

**💡 Point clé :** Le broadcast est utilisé par :
- ARP (résolution IP → MAC)
- DHCP Discover
- Annonces de protocoles

255.255.255.255 (D) est une adresse IP broadcast, pas MAC.

---

## Question 4
**Réponse correcte : B**

**Explication :**
La taille minimale d'une trame Ethernet (sans préambule ni SFD) est de **64 octets** : 14 octets d'en-tête + 46 octets de données minimum + 4 octets de FCS.

**💡 Point clé :** Si les données sont inférieures à 46 octets, du **padding** (remplissage de zéros) est ajouté pour atteindre 46 octets. Cette taille minimale permet la détection des collisions en CSMA/CD.

---

## Question 5
**Réponse correcte : B**

**Explication :**
La taille maximale d'une trame Ethernet standard est de **1518 octets** :
- En-tête : 14 octets (6 + 6 + 2)
- Données : 1500 octets (MTU)
- FCS : 4 octets

**💡 Point clé :** Les trames plus grandes (jusqu'à 9000 octets) sont appelées "Jumbo Frames" et ne sont pas standard, mais utilisées dans les datacenters.

---

## Question 6
**Réponse correcte : D**

**Explication :**
Le **FCS (Frame Check Sequence)** utilise un calcul CRC-32 pour détecter les erreurs de transmission. Il est placé dans le trailer de la trame (4 derniers octets).

**💡 Point clé :** Le FCS détecte les erreurs mais ne les corrige pas. Si le FCS reçu ne correspond pas au FCS calculé, la trame est jetée. La retransmission est gérée par TCP si nécessaire.

---

## Question 7
**Réponse correcte : B**

**Explication :**
Les adresses multicast IPv4 commencent par **01:00:5E** suivi de 23 bits de poids faible de l'adresse IP multicast.

**💡 Point clé :** Exemple :
- IP multicast : 224.0.0.10 (EIGRP)
- MAC multicast : 01:00:5E:00:00:0A

Utilisé par les protocoles de routage (OSPF, EIGRP, PIM).

---

## Question 8
**Réponse correcte : B**

**Explication :**
Les adresses multicast IPv6 commencent par **33:33** suivi de 32 bits de poids faible de l'adresse IPv6 multicast.

**💡 Point clé :** Exemple :
- IPv6 multicast : FF02::1 (tous les nœuds)
- MAC multicast : 33:33:00:00:00:01

Utilisé par NDP (Neighbor Discovery Protocol), OSPFv3, RIPng.

---

## Question 9
**Réponse correcte : A**

**Explication :**
Un commutateur apprend les adresses MAC en examinant l'**adresse MAC source** des trames reçues. Il enregistre : "Cette MAC est accessible via ce port".

**💡 Point clé :** Processus d'apprentissage :
1. Réception d'une trame sur un port
2. Lecture de l'adresse MAC source
3. Ajout dans la table : MAC → Port
4. Timer de 300 secondes par défaut

---

## Question 10
**Réponse correcte : B**

**Explication :**
Lorsque l'adresse MAC de destination est inconnue, le commutateur effectue un **flooding** : il envoie la trame sur tous les ports sauf le port source. Cela s'appelle "unknown unicast flooding".

**💡 Point clé :** Lorsque le destinataire répond, le switch apprendra son adresse MAC et pourra ensuite faire du forwarding intelligent vers le bon port uniquement.

---

## Question 11
**Réponse correcte : C**

**Explication :**
La commande `show mac address-table` affiche la table d'adresses MAC du commutateur, montrant quelle adresse MAC est accessible par quelle interface.

**💡 Point clé :** Variantes utiles :
- `show mac address-table dynamic` : Entrées apprises dynamiquement
- `show mac address-table interface gi0/1` : MACs sur un port spécifique
- `clear mac address-table dynamic` : Effacer la table

---

## Question 12
**Réponse correcte : C**

**Explication :**
Par défaut, une entrée de la table MAC expire après **300 secondes (5 minutes)** d'inactivité. Si le switch ne reçoit aucune trame avec cette MAC source pendant 300s, l'entrée est supprimée.

**💡 Point clé :** Ce mécanisme d'aging permet au switch de s'adapter aux changements (périphériques déplacés, déconnectés, etc.). Le timer est configurable avec `mac address-table aging-time`.

---

## Question 13
**Réponse correcte : C**

**Explication :**
La méthode **Store-and-Forward** reçoit la trame complète, vérifie le FCS (détection d'erreurs), puis transmet si le FCS est valide. Si le FCS est invalide, la trame est jetée.

**💡 Point clé :** Avantages :
- Détection d'erreurs (ne transmet pas les trames corrompues)
- Supporte différentes vitesses sur les ports (buffering)

C'est la méthode par défaut sur tous les switches modernes.

---

## Question 14
**Réponse correcte : B**

**Explication :**
La méthode **Cut-Through** commence à transférer la trame dès que l'adresse MAC de destination est lue (6 premiers octets), sans attendre la trame complète ni vérifier le FCS. Cela offre la latence la plus faible mais ne détecte pas les erreurs.

**💡 Point clé :** Variantes :
- **Fast-Forward** : Transfert immédiat après lecture de la MAC destination
- **Fragment-Free** : Lit les 64 premiers octets pour éviter les runts (trames trop petites)

Utilisé dans les environnements haute performance (datacenters).

---

## Question 15
**Réponse correcte : C**

**Explication :**
En mode **Full-Duplex**, deux périphériques peuvent émettre et recevoir simultanément. La bande passante effective est doublée (ex: 1 Gbps émission + 1 Gbps réception = 2 Gbps total).

**💡 Point clé :** Full-Duplex :
- Pas de collisions
- CSMA/CD désactivé
- Standard sur tous les switches modernes
- Requiert des connexions point-à-point

Half-Duplex permet une communication bidirectionnelle mais pas simultanée.

---

## Question 16
**Réponse correcte : B**

**Explication :**
**CSMA/CD (Carrier Sense Multiple Access with Collision Detection)** est utilisé en mode Half-Duplex pour détecter et gérer les collisions. Lorsqu'une collision est détectée, les périphériques attendent un délai aléatoire avant de retransmettre.

**💡 Point clé :** 
- CSMA/CD : Ethernet filaire (Half-Duplex)
- CSMA/CA : Wi-Fi (Collision Avoidance)

En Full-Duplex, CSMA/CD est désactivé car il n'y a pas de collisions possibles.

---

## Question 17
**Réponse correcte : B**

**Explication :**
**Auto-MDIX** (Automatic Medium-Dependent Interface Crossover) permet au switch de détecter automatiquement si un câble droit ou croisé est connecté et d'ajuster ses paires TX/RX en conséquence.

**💡 Point clé :** Avec Auto-MDIX, vous pouvez utiliser n'importe quel type de câble (droit ou croisé) pour n'importe quelle connexion. Cette fonctionnalité est activée par défaut sur les switches modernes avec `mdix auto`.

---

## Question 18
**Réponse correcte : B**

**Explication :**
Le champ de données minimum dans une trame Ethernet est de **46 octets**. Si les données à transmettre sont inférieures à 46 octets, du padding (remplissage) est ajouté.

**💡 Point clé :** Calcul de la taille minimale de trame :
- En-tête : 14 octets
- Données : **46 octets minimum**
- FCS : 4 octets
- Total : **64 octets minimum**

Le maximum est 1500 octets (MTU).

---

## Question 19
**Réponse correcte : C**

**Explication :**
**1000BASE-T** est le standard pour Gigabit Ethernet (1 Gbps) sur câble cuivre UTP. Il utilise les 4 paires du câble Cat 5e ou Cat 6.

**💡 Point clé :** Standards Ethernet à connaître :
- **10BASE-T** : 10 Mbps, Cat 3, 100m
- **100BASE-TX** : 100 Mbps (Fast Ethernet), Cat 5/5e, 100m
- **1000BASE-T** : 1 Gbps (Gigabit), Cat 5e/6, 100m
- **10GBASE-T** : 10 Gbps, Cat 6a, 100m

---

## Question 20
**Réponse correcte : A**

**Explication :**
**MTU (Maximum Transmission Unit)** représente la taille maximale des données (payload) dans une trame. Pour Ethernet, le MTU standard est de **1500 octets**.

**💡 Point clé :** Le MTU ne compte pas les en-têtes et le trailer :
- MTU = 1500 octets (données uniquement)
- Trame totale = 1518 octets (+ en-tête 14 + FCS 4)

Si un paquet IP est plus grand que le MTU, il doit être fragmenté.

---

**Score recommandé pour valider le module : 16/20 minimum (80%)**

**Révision conseillée si score < 16/20 :**
- Section 7.1 (Trames Ethernet - structure et champs)
- Section 7.2 (Adresses MAC - types et formats)
- Section 7.3 (Table d'adresses MAC - apprentissage et transfert)
- Section 7.4 (Méthodes de commutation et duplex)
- Pratiquer avec `show mac address-table` dans Packet Tracer
- Observer le processus d'apprentissage en mode simulation

**💡 Exercice pratique recommandé :**
Dans Packet Tracer, créez un réseau simple avec un switch et 4 PC. En mode simulation, envoyez des pings et observez :
1. L'apprentissage des adresses MAC (flooding puis forwarding)
2. Les différents types d'adresses (unicast, broadcast)
3. L'évolution de la table MAC
