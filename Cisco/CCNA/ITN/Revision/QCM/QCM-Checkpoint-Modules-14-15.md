# QCM Checkpoint - Modules 14-15 : Communications des applications du réseau

**Nombre de questions :** 30  
**Durée estimée :** 45 minutes  
**Seuil de réussite :** 75% (23/30 questions)

**Couverture :**
- Module 14 : Protocoles de Transport (TCP/UDP) (15 questions)
- Module 15 : Protocoles de la couche Application (15 questions)

---

## MODULE 14 - Protocoles de Transport (TCP/UDP)

### Question 1

Une application de vidéoconférence doit transmettre de la voix et de la vidéo en temps réel. Quel protocole de transport est le plus approprié et pourquoi ? (Choix unique)

- [ ] A. TCP, car il garantit la livraison de tous les paquets
- [ ] B. UDP, car il minimise la latence et tolère les pertes occasionnelles
- [ ] C. TCP, car il supporte le multiplexage par ports
- [ ] D. UDP, car il utilise des numéros de séquence

---

### Question 2

Quelles caractéristiques sont associées au protocole TCP ? (Choix multiples - 3 réponses)

- [ ] A. Établissement de connexion via 3-way handshake
- [ ] B. Pas d'accusé de réception
- [ ] C. Contrôle de flux avec fenêtre glissante
- [ ] D. Overhead faible (8 octets d'en-tête)
- [ ] E. Réordonnancement des segments
- [ ] F. Protocole best-effort sans garantie de livraison

---

### Question 3

Quelle est la taille minimum et maximum de l'en-tête TCP ? (Choix unique)

- [ ] A. 8 octets minimum, 60 octets maximum
- [ ] B. 20 octets minimum, 60 octets maximum
- [ ] C. 20 octets minimum, 40 octets maximum
- [ ] D. 16 octets minimum, 64 octets maximum

---

### Question 4

Dans un en-tête TCP, quel champ indique la quantité de données (en octets) que le récepteur peut accepter sans attendre un accusé de réception ? (Choix unique)

- [ ] A. Sequence Number
- [ ] B. Acknowledgment Number
- [ ] C. Window Size
- [ ] D. Checksum

---

### Question 5

Un client TCP envoie un segment avec SEQ=3000 contenant 500 octets de données. Quel numéro d'accusé de réception (ACK) le serveur devrait-il envoyer en réponse ? (Choix unique)

- [ ] A. ACK=3000
- [ ] B. ACK=3500
- [ ] C. ACK=3499
- [ ] D. ACK=3501

---

### Question 6

À quoi sert le champ "Data Offset" dans l'en-tête TCP ? (Choix unique)

- [ ] A. Indiquer le décalage des données urgentes
- [ ] B. Indiquer la longueur de l'en-tête TCP en mots de 32 bits
- [ ] C. Indiquer la position du segment dans le flux de données
- [ ] D. Indiquer le nombre d'octets de données dans le segment

---

### Question 7

Quels flags TCP sont utilisés lors de l'établissement d'une connexion (3-way handshake) ? (Choix multiples - 2 réponses)

- [ ] A. SYN
- [ ] B. FIN
- [ ] C. ACK
- [ ] D. RST
- [ ] E. PSH

---

### Question 8

Un serveur reçoit une requête de connexion TCP sur un port fermé. Quel flag TCP le serveur envoie-t-il pour refuser la connexion ? (Choix unique)

- [ ] A. FIN
- [ ] B. RST
- [ ] C. PSH
- [ ] D. URG

---

### Question 9

Lors du 3-way handshake, le client envoie SYN avec SEQ=1000. Le serveur répond avec SYN-ACK SEQ=5000, ACK=1001. Quels sont les numéros SEQ et ACK du troisième segment envoyé par le client ? (Choix unique)

- [ ] A. SEQ=1000, ACK=5000
- [ ] B. SEQ=1001, ACK=5000
- [ ] C. SEQ=1001, ACK=5001
- [ ] D. SEQ=1002, ACK=5001

---

### Question 10

Un récepteur TCP a un buffer de 12 000 octets disponibles et annonce Window Size = 12000. Le MSS est de 1500 octets. Combien de segments complets l'émetteur peut-il envoyer sans attendre un ACK ? (Choix unique)

- [ ] A. 6 segments
- [ ] B. 8 segments
- [ ] C. 10 segments
- [ ] D. 12 segments

---

### Question 11

Dans le mécanisme de fenêtre glissante TCP, que se passe-t-il si le récepteur envoie Window Size = 0 ? (Choix unique)

- [ ] A. L'émetteur ferme immédiatement la connexion
- [ ] B. L'émetteur arrête d'envoyer des données jusqu'à recevoir une fenêtre non nulle
- [ ] C. L'émetteur continue d'envoyer mais à débit réduit
- [ ] D. L'émetteur envoie un segment RST

---

### Question 12

Dans l'algorithme Slow Start de TCP, comment évolue la fenêtre de congestion (CWND) à chaque ACK reçu ? (Choix unique)

- [ ] A. CWND augmente linéairement (+1 MSS par RTT)
- [ ] B. CWND double à chaque ACK
- [ ] C. CWND augmente de 10% à chaque ACK
- [ ] D. CWND reste constante

---

### Question 13

Un émetteur TCP détecte une perte de paquet (timeout). Actuellement CWND = 32 MSS. Quelles actions sont effectuées ? (Choix multiples - 2 réponses)

- [ ] A. ssthresh = CWND / 2 = 16 MSS
- [ ] B. CWND = 1 MSS
- [ ] C. CWND = ssthresh
- [ ] D. La connexion est fermée
- [ ] E. CWND reste à 32 MSS

---

### Question 14

Quelle est la taille de l'en-tête UDP ? (Choix unique)

- [ ] A. 4 octets
- [ ] B. 8 octets
- [ ] C. 20 octets
- [ ] D. 16 octets

---

### Question 15

Un réseau Ethernet a un MTU de 1500 octets. En utilisant IPv4 (en-tête de 20 octets) et TCP (en-tête de 20 octets), quelle est la valeur maximale du MSS (Maximum Segment Size) ? (Choix unique)

- [ ] A. 1500 octets
- [ ] B. 1480 octets
- [ ] C. 1460 octets
- [ ] D. 1440 octets

---

## MODULE 15 - Protocoles de la couche Application

### Question 16

Quels sont les ports utilisés par HTTP et HTTPS ? (Choix unique)

- [ ] A. HTTP: 80, HTTPS: 443
- [ ] B. HTTP: 443, HTTPS: 80
- [ ] C. HTTP: 8080, HTTPS: 8443
- [ ] D. HTTP: 23, HTTPS: 22

---

### Question 17

Un utilisateur tente d'accéder à une page web qui n'existe plus sur le serveur. Quel code de statut HTTP le serveur retourne-t-il ? (Choix unique)

- [ ] A. 200 OK
- [ ] B. 301 Moved Permanently
- [ ] C. 404 Not Found
- [ ] D. 500 Internal Server Error

---

### Question 18

Quelle est la fonction principale du DNS ? (Choix unique)

- [ ] A. Attribuer automatiquement des adresses IP aux clients
- [ ] B. Traduire les noms de domaine en adresses IP
- [ ] C. Chiffrer les communications web
- [ ] D. Transférer des fichiers entre serveurs

---

### Question 19

Quel port utilise le DNS pour les requêtes standards et quel protocole de transport ? (Choix unique)

- [ ] A. Port 53 UDP
- [ ] B. Port 53 TCP
- [ ] C. Port 67 UDP
- [ ] D. Port 80 TCP

---

### Question 20

Associez chaque type d'enregistrement DNS à sa fonction. Quelles correspondances sont correctes ? (Choix multiples - 3 réponses)

- [ ] A. A → Adresse IPv4
- [ ] B. AAAA → Adresse IPv6
- [ ] C. CNAME → Serveur de messagerie
- [ ] D. MX → Serveur de messagerie
- [ ] E. PTR → Alias vers un autre nom
- [ ] F. NS → Serveur DNS autoritaire

---

### Question 21

Dans la hiérarchie DNS, quel est l'ordre correct de résolution du nom "www.cisco.com" ? (Choix unique)

- [ ] A. Root (.) → .com → cisco.com → www.cisco.com
- [ ] B. www → cisco → .com → Root (.)
- [ ] C. cisco.com → .com → Root (.) → www
- [ ] D. .com → www.cisco.com → Root (.)

---

### Question 22

Quels ports sont utilisés par le processus DHCP ? (Choix unique)

- [ ] A. Port 67 (serveur) et 68 (client) - UDP
- [ ] B. Port 68 (serveur) et 67 (client) - TCP
- [ ] C. Port 53 (serveur) et 54 (client) - UDP
- [ ] D. Port 80 (serveur) et 81 (client) - TCP

---

### Question 23

Dans le processus DORA du DHCP, quelle est la séquence correcte des étapes ? (Choix unique)

- [ ] A. Discover → Offer → Request → Acknowledge
- [ ] B. Offer → Discover → Acknowledge → Request
- [ ] C. Request → Discover → Offer → Acknowledge
- [ ] D. Discover → Request → Offer → Acknowledge

---

### Question 24

Un client DHCP envoie un message DHCP DISCOVER. Quelles sont les adresses IP source et destination de ce message ? (Choix unique)

- [ ] A. Source: 0.0.0.0, Destination: 255.255.255.255
- [ ] B. Source: 192.168.1.1, Destination: 255.255.255.255
- [ ] C. Source: 0.0.0.0, Destination: 192.168.1.1
- [ ] D. Source: 255.255.255.255, Destination: 0.0.0.0

---

### Question 25

Un client DHCP obtient un bail de 24 heures. À quel moment le client tente-t-il de renouveler son bail auprès du serveur DHCP qui lui a attribué l'adresse ? (Choix unique)

- [ ] A. À T1 (50% du bail) = 12 heures
- [ ] B. À T2 (87.5% du bail) = 21 heures
- [ ] C. À 100% (expiration) = 24 heures
- [ ] D. À 25% du bail = 6 heures

---

### Question 26

Un réseau d'entreprise a plusieurs VLANs et un seul serveur DHCP centralisé. Comment permettre aux clients des autres VLANs d'obtenir des adresses IP ? (Choix unique)

- [ ] A. Installer un serveur DHCP dans chaque VLAN
- [ ] B. Configurer un DHCP Relay Agent (ip helper-address) sur le routeur
- [ ] C. Activer le DHCP Snooping sur tous les switches
- [ ] D. Utiliser des adresses IP statiques

---

### Question 27

Quels protocoles sont utilisés pour l'envoi et la réception d'emails ? (Choix multiples - 3 réponses)

- [ ] A. SMTP pour l'envoi (client → serveur)
- [ ] B. HTTP pour la réception
- [ ] C. POP3 pour la réception (téléchargement local)
- [ ] D. FTP pour l'envoi
- [ ] E. IMAP pour la gestion sur le serveur
- [ ] F. DNS pour l'acheminement des emails

---

### Question 28

Quelles sont les principales différences entre POP3 et IMAP ? (Choix multiples - 2 réponses)

- [ ] A. POP3 stocke les emails localement, IMAP les conserve sur le serveur
- [ ] B. POP3 utilise TCP, IMAP utilise UDP
- [ ] C. IMAP permet la synchronisation multi-appareils, POP3 non
- [ ] D. POP3 utilise le port 443, IMAP le port 25
- [ ] E. IMAP ne supporte pas le chiffrement TLS

---

### Question 29

Quelles affirmations concernant les protocoles de transfert de fichiers sont correctes ? (Choix multiples - 3 réponses)

- [ ] A. FTP utilise les ports 20 et 21 avec TCP
- [ ] B. TFTP utilise le port 69 avec UDP
- [ ] C. TFTP nécessite une authentification par nom d'utilisateur et mot de passe
- [ ] D. SSH utilise le port 22 et chiffre les communications
- [ ] E. Telnet utilise le port 23 et chiffre les communications
- [ ] F. SFTP est FTP sur SSH (port 22)

---

### Question 30

Une entreprise utilise SMB pour le partage de fichiers. Quelle version de SMB doit être désactivée pour des raisons de sécurité et sur quel port fonctionne SMB moderne ? (Choix unique)

- [ ] A. Désactiver SMB 3.0, port 139
- [ ] B. Désactiver SMB 1.0, port 445
- [ ] C. Désactiver SMB 2.0, port 80
- [ ] D. Désactiver SMB 3.1.1, port 443

---

## Réponses et explications

### Question 1
**Réponse correcte :** B

**Explication :**
Les applications de vidéoconférence privilégient la **faible latence** plutôt que la fiabilité absolue. UDP est le protocole approprié car :
- Il minimise l'overhead (pas d'établissement de connexion, pas d'ACK)
- Il tolère les pertes occasionnelles (quelques images/échantillons perdus sont acceptables)
- La retransmission de paquets perdus dans TCP créerait des délais inacceptables pour du temps réel
- Le temps réel nécessite un flux continu même si quelques paquets sont perdus

TCP serait trop lent à cause des retransmissions et du contrôle de flux.

---

### Question 2
**Réponses correctes :** A, C, E

**Explication :**
Les caractéristiques de TCP sont :
- **A. Établissement de connexion via 3-way handshake** ✅ (SYN, SYN-ACK, ACK)
- **B. Pas d'accusé de réception** ❌ TCP utilise des ACK
- **C. Contrôle de flux avec fenêtre glissante** ✅ (Window Size)
- **D. Overhead faible (8 octets)** ❌ TCP = 20-60 octets, UDP = 8 octets
- **E. Réordonnancement des segments** ✅ (grâce aux numéros SEQ)
- **F. Best-effort sans garantie** ❌ C'est UDP, TCP est fiable

---

### Question 3
**Réponse correcte :** B

**Explication :**
L'en-tête TCP fait :
- **Minimum** : 20 octets (sans options)
- **Maximum** : 60 octets (avec options, car Data Offset = 4 bits → max 15 × 4 = 60 octets)

Les options TCP peuvent inclure : MSS, Window Scale, SACK, Timestamps, etc.

---

### Question 4
**Réponse correcte :** C

**Explication :**
Le champ **Window Size** (16 bits) indique la taille de la fenêtre de réception en octets. Il permet le contrôle de flux pour empêcher la surcharge du buffer du récepteur.

- **Sequence Number** : Numéro du premier octet de données
- **Acknowledgment Number** : Prochain octet attendu
- **Checksum** : Vérification d'intégrité

---

### Question 5
**Réponse correcte :** B

**Explication :**
Calcul de l'ACK :
- Segment envoyé : SEQ=3000, contenant 500 octets de données
- Données couvrent les octets 3000 à 3499
- Le récepteur acquitte le **prochain octet attendu** : ACK = 3000 + 500 = **3500**

L'ACK est cumulatif : il confirme la réception de tous les octets jusqu'à ACK-1.

---

### Question 6
**Réponse correcte :** B

**Explication :**
Le champ **Data Offset** (4 bits) indique la longueur de l'en-tête TCP en **mots de 32 bits** (4 octets).

Calcul :
- Valeur minimum : 5 → 5 × 4 = 20 octets
- Valeur maximum : 15 → 15 × 4 = 60 octets

Cela permet de savoir où commencent les données applicatives après l'en-tête.

---

### Question 7
**Réponses correctes :** A, C

**Explication :**
Le 3-way handshake utilise :
1. **Client → Serveur** : SYN (SEQ=x)
2. **Serveur → Client** : SYN-ACK (SEQ=y, ACK=x+1)
3. **Client → Serveur** : ACK (SEQ=x+1, ACK=y+1)

Les flags **SYN** et **ACK** sont donc utilisés.

- **FIN** est pour la fermeture de connexion
- **RST** pour réinitialisation brutale
- **PSH** pour push immédiat au processus applicatif

---

### Question 8
**Réponse correcte :** B

**Explication :**
Le flag **RST (Reset)** est utilisé pour :
- Refuser une connexion sur un port fermé
- Réinitialiser brutalement une connexion
- Signaler une erreur

Exemples d'utilisation :
- Port fermé → RST
- Connexion corrompue → RST
- Détection d'attaque → RST

**FIN** est pour une fermeture propre, pas un refus.

---

### Question 9
**Réponse correcte :** C

**Explication :**
Déroulement du 3-way handshake :
1. **Client → Serveur** : SYN, SEQ=1000
2. **Serveur → Client** : SYN-ACK, SEQ=5000, ACK=1001
3. **Client → Serveur** : ACK, SEQ=1001, ACK=5001

Le client utilise SEQ=1001 (son prochain numéro après 1000) et ACK=5001 (acquitte le SYN du serveur qui utilisait SEQ=5000).

---

### Question 10
**Réponse correcte :** B

**Explication :**
Calcul :
- Window Size = 12 000 octets
- MSS = 1500 octets par segment
- Nombre de segments = 12 000 / 1500 = **8 segments**

L'émetteur peut envoyer 8 segments de 1500 octets chacun (total 12 000 octets) sans attendre d'ACK.

---

### Question 11
**Réponse correcte :** B

**Explication :**
Quand le récepteur annonce **Window Size = 0** :
- Le buffer du récepteur est plein
- L'émetteur **arrête d'envoyer des données**
- L'émetteur envoie périodiquement des "window probes" pour vérifier si la fenêtre s'est ouverte
- Quand le récepteur annonce Window Size > 0, la transmission reprend

C'est un mécanisme de contrôle de flux pour protéger le récepteur.

---

### Question 12
**Réponse correcte :** B

**Explication :**
L'algorithme **Slow Start** utilise une croissance **exponentielle** :
- Démarre avec CWND = 1 MSS
- À chaque ACK reçu : **CWND double**
- Progression : 1 → 2 → 4 → 8 → 16 → 32 MSS

Quand CWND atteint le seuil (ssthresh), on passe en **Congestion Avoidance** (croissance linéaire +1 MSS par RTT).

---

### Question 13
**Réponses correctes :** A, B

**Explication :**
Lors d'une perte détectée par timeout :
- **ssthresh = CWND / 2** → ssthresh = 32 / 2 = **16 MSS** ✅
- **CWND = 1 MSS** (recommence Slow Start) ✅
- La connexion n'est PAS fermée (TCP continue)
- CWND ne reste pas à 32 MSS

Ensuite : Slow Start jusqu'à ssthresh (16 MSS), puis Congestion Avoidance.

---

### Question 14
**Réponse correcte :** B

**Explication :**
L'en-tête UDP est très simple : **8 octets** seulement

Structure :
- Source Port : 2 octets
- Destination Port : 2 octets
- Length : 2 octets
- Checksum : 2 octets

C'est beaucoup plus léger que TCP (20-60 octets), d'où le faible overhead d'UDP.

---

### Question 15
**Réponse correcte :** C

**Explication :**
Calcul du MSS :
- MTU = 1500 octets
- En-tête IP = 20 octets
- En-tête TCP = 20 octets
- **MSS = 1500 - 20 - 20 = 1460 octets**

Le MSS représente la quantité maximale de données applicatives dans un segment TCP, excluant les en-têtes.

---

### Question 16
**Réponse correcte :** A

**Explication :**
Ports standards :
- **HTTP** : port **80** (TCP) - non chiffré
- **HTTPS** : port **443** (TCP) - chiffré avec TLS

HTTPS = HTTP over TLS (anciennement SSL). C'est la version sécurisée du protocole web.

---

### Question 17
**Réponse correcte :** C

**Explication :**
Codes de statut HTTP :
- **200 OK** : La ressource existe et est retournée
- **301 Moved Permanently** : Redirection permanente
- **404 Not Found** : La ressource demandée n'existe pas (ou plus) ✅
- **500 Internal Server Error** : Erreur côté serveur (bug, crash)

Le code **404** est le plus emblématique du web pour signaler une page introuvable.

---

### Question 18
**Réponse correcte :** B

**Explication :**
Le **DNS (Domain Name System)** est le "service d'annuaire d'Internet" :
- Fonction : **Traduire noms de domaine → adresses IP**
- Exemple : www.cisco.com → 72.163.4.185

Les autres réponses correspondent à :
- **A** : DHCP (attribution d'IP)
- **C** : TLS/SSL (chiffrement)
- **D** : FTP/TFTP (transfert de fichiers)

---

### Question 19
**Réponse correcte :** A

**Explication :**
Le DNS utilise :
- **Port 53**
- **UDP** pour les requêtes DNS normales (rapide, faible overhead)
- **TCP** pour les transferts de zones (zone transfers) entre serveurs DNS

UDP est privilégié car les requêtes DNS sont courtes et une éventuelle perte peut être récupérée par retransmission au niveau applicatif.

---

### Question 20
**Réponses correctes :** A, B, D

**Explication :**
Types d'enregistrements DNS :
- **A** → Adresse IPv4 (www.example.com → 93.184.216.34) ✅
- **AAAA** → Adresse IPv6 (www.example.com → 2606:2800:220:1:...) ✅
- **CNAME** → Alias (blog.example.com → www.example.com) [pas serveur email]
- **MX** → Serveur de messagerie (example.com → mail.example.com) ✅
- **PTR** → Résolution inverse (IP → Nom) [pas alias]
- **NS** → Serveur DNS autoritaire ✅

---

### Question 21
**Réponse correcte :** A

**Explication :**
Résolution DNS pour "www.cisco.com" :
1. **Root (.)** : Serveur racine
2. **.com** : TLD (Top-Level Domain)
3. **cisco.com** : Second-Level Domain
4. **www.cisco.com** : Subdomain

Le résolveur DNS interroge de haut en bas dans la hiérarchie pour trouver le serveur autoritaire final.

---

### Question 22
**Réponse correcte :** A

**Explication :**
Le DHCP utilise :
- **Port 67** : Serveur DHCP (écoute)
- **Port 68** : Client DHCP (écoute)
- **Protocole** : **UDP** (pas TCP)

Le client envoie au port 67, le serveur répond au port 68. C'est un protocole léger qui n'a pas besoin de la fiabilité de TCP.

---

### Question 23
**Réponse correcte :** A

**Explication :**
Le processus DHCP est **DORA** :
1. **D**iscover : Client → Broadcast (cherche un serveur DHCP)
2. **O**ffer : Serveur → Client (propose une IP)
3. **R**equest : Client → Broadcast (accepte l'offre)
4. **A**cknowledge : Serveur → Client (confirme l'attribution)

Mnémonique : **DORA** l'exploratrice explore le réseau ! 🎒

---

### Question 24
**Réponse correcte :** A

**Explication :**
Le message **DHCP DISCOVER** utilise :
- **Source IP** : **0.0.0.0** (le client n'a pas encore d'adresse IP)
- **Destination IP** : **255.255.255.255** (broadcast pour atteindre tous les serveurs DHCP)

C'est le seul moment où une machine utilise 0.0.0.0 comme source, car elle cherche justement à obtenir une IP.

---

### Question 25
**Réponse correcte :** A

**Explication :**
Le renouvellement du bail DHCP suit ce calendrier :
- **T1 (50% du bail)** : Renouvellement auprès du serveur DHCP qui a attribué l'IP ✅
  - 24h × 50% = **12 heures**
- **T2 (87.5% du bail)** : Broadcast à tous les serveurs si T1 échoue
  - 24h × 87.5% = 21 heures
- **100% (expiration)** : Le client perd l'IP et recommence DORA

---

### Question 26
**Réponse correcte :** B

**Explication :**
Le problème : DHCP utilise le **broadcast** (ne traverse pas les routeurs par défaut)

La solution : **DHCP Relay Agent** (ou IP Helper sur Cisco)
- Configuration : `ip helper-address [IP du serveur DHCP]`
- Le routeur convertit le broadcast DHCP en **unicast**
- Il l'envoie au serveur DHCP centralisé
- Le serveur répond au routeur qui transmet au client

Cela évite d'avoir un serveur DHCP par VLAN.

---

### Question 27
**Réponses correctes :** A, C, E

**Explication :**
Architecture email :
- **SMTP (port 25/587)** : Envoi d'emails (client → serveur, serveur → serveur) ✅
- **POP3 (port 110)** : Réception avec téléchargement local, un seul appareil ✅
- **IMAP (port 143)** : Gestion sur le serveur, synchronisation multi-appareils ✅

HTTP n'est pas un protocole email (c'est pour le web), FTP est pour les fichiers, DNS résout les noms de domaine.

---

### Question 28
**Réponses correctes :** A, C

**Explication :**
Différences POP3 vs IMAP :
- **Stockage** :
  - POP3 : Télécharge les emails **localement**, les supprime du serveur ✅
  - IMAP : Conserve les emails **sur le serveur** ✅
- **Multi-appareils** :
  - POP3 : Un seul appareil (emails locaux)
  - IMAP : Synchronisation entre tous les appareils (PC, smartphone, tablette) ✅

Les deux utilisent **TCP**, pas UDP. Ports : POP3 = 110, IMAP = 143 (pas 443/25). Les deux supportent TLS.

---

### Question 29
**Réponses correctes :** A, B, D, F

**Explication :**
Protocoles de transfert et accès distant :
- **FTP** : Ports 20 (données) et 21 (contrôle), TCP, avec authentification ✅
- **TFTP** : Port 69, UDP, **sans authentification** (pas de user/pass) ✅
- **SSH** : Port 22, chiffré (sécurisé) ✅
- **Telnet** : Port 23, **non chiffré** (obsolète, vulnérable)
- **SFTP** : FTP sur SSH, port 22 ✅

TFTP est utilisé pour le boot réseau (PXE) et la configuration d'équipements réseau de manière simple.

---

### Question 30
**Réponse correcte :** B

**Explication :**
SMB (Server Message Block) :
- **SMB 1.0** doit être **désactivé** ✅
  - Vulnérabilités critiques : EternalBlue, WannaCry, NotPetya
  - Aucune raison de l'utiliser aujourd'hui
- **Port** : **445** (TCP) pour SMBv2/v3 direct ✅
- Port 139 : NetBIOS over TCP (ancien)

Versions recommandées : SMB 3.0, 3.1.1 (Windows 10/11, Server 2016+) avec chiffrement AES.

---

## Récapitulatif des réponses

| Question | Réponse(s) | Question | Réponse(s) |
|----------|------------|----------|------------|
| 1 | B | 16 | A |
| 2 | A, C, E | 17 | C |
| 3 | B | 18 | B |
| 4 | C | 19 | A |
| 5 | B | 20 | A, B, D |
| 6 | B | 21 | A |
| 7 | A, C | 22 | A |
| 8 | B | 23 | A |
| 9 | C | 24 | A |
| 10 | B | 25 | A |
| 11 | B | 26 | B |
| 12 | B | 27 | A, C, E |
| 13 | A, B | 28 | A, C |
| 14 | B | 29 | A, B, D, F |
| 15 | C | 30 | B |

---

## Conseils pour l'examen

### Module 14 - Protocoles de Transport

**Points clés à réviser :**
- ✅ Différences fondamentales TCP vs UDP (connexion, fiabilité, overhead)
- ✅ Structure et taille en-tête TCP (20-60 octets) et UDP (8 octets)
- ✅ Rôle des champs : SEQ, ACK, Window Size, Checksum
- ✅ Flags TCP : SYN, ACK, FIN, RST, PSH, URG
- ✅ 3-way handshake et 4-way termination
- ✅ Calcul des numéros SEQ et ACK
- ✅ Fenêtre glissante : contrôle de flux (Window Size)
- ✅ Contrôle de congestion : Slow Start, Congestion Avoidance, ssthresh, CWND
- ✅ Calcul du MSS : MTU - IP - TCP

**Pièges fréquents :**
- Ne pas confondre SEQ (1er octet envoyé) et ACK (prochain octet attendu)
- Window Size = 0 → arrêt émission (pas fermeture connexion)
- Slow Start = croissance exponentielle, Congestion Avoidance = linéaire
- UDP n'a pas de numéros SEQ/ACK (protocole sans connexion)

### Module 15 - Protocoles de la couche Application

**Points clés à réviser :**
- ✅ Ports standards : HTTP 80, HTTPS 443, DNS 53, DHCP 67/68, SMTP 25, POP3 110, IMAP 143, FTP 20/21, TFTP 69, SSH 22, Telnet 23, SMB 445
- ✅ Codes HTTP : 200 OK, 404 Not Found, 500 Internal Server Error
- ✅ DNS : Types d'enregistrements (A, AAAA, CNAME, MX, PTR, NS), hiérarchie, résolution
- ✅ DHCP : Processus DORA, adresses source/destination, T1/T2, DHCP Relay
- ✅ Email : SMTP envoi, POP3 vs IMAP réception, différences stockage/synchronisation
- ✅ FTP vs TFTP : TCP/UDP, authentification, ports
- ✅ SSH vs Telnet : chiffrement, sécurité

**Pièges fréquents :**
- DHCP DISCOVER : source 0.0.0.0, destination 255.255.255.255
- DNS utilise UDP (requêtes) ET TCP (transferts de zones)
- POP3 = local/un appareil, IMAP = serveur/multi-appareils
- TFTP = pas d'authentification (contrairement à FTP)
- SMB 1.0 doit être désactivé (vulnérable)

---

**Bon courage pour votre examen ! 🚀**
