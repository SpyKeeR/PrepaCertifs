# QCM Module 15 - Protocoles de la couche Application

**Nombre de questions :** 20  
**Durée estimée :** 30 minutes  
**Seuil de réussite :** 75% (15/20)

---

## Question 1
Quels sont les ports utilisés par **HTTP** et **HTTPS** ? (Choix unique)

- [ ] HTTP : 21, HTTPS : 22
- [ ] HTTP : 80, HTTPS : 443
- [ ] HTTP : 443, HTTPS : 80
- [ ] HTTP : 53, HTTPS : 443

---

## Question 2
Quelle méthode HTTP est utilisée pour **récupérer une ressource** (ex : une page web) ? (Choix unique)

- [ ] POST
- [ ] GET
- [ ] PUT
- [ ] DELETE

---

## Question 3
Que signifie le code de statut HTTP **404** ? (Choix unique)

- [ ] Requête traitée avec succès
- [ ] Redirection permanente vers une autre URL
- [ ] Ressource introuvable
- [ ] Erreur interne du serveur

---

## Question 4
Quelle est la fonction principale du protocole **DNS** ? (Choix unique)

- [ ] Attribuer automatiquement des adresses IP aux clients
- [ ] Traduire les noms de domaine en adresses IP
- [ ] Transférer des fichiers entre serveurs
- [ ] Envoyer des emails entre serveurs

---

## Question 5
Le DNS utilise principalement le port **53**. Quel protocole de transport utilise-t-il pour les **requêtes DNS standard** ? (Choix unique)

- [ ] TCP uniquement
- [ ] UDP uniquement
- [ ] UDP pour les requêtes, TCP pour les transferts de zones
- [ ] ICMP

---

## Question 6
Dans la hiérarchie DNS, quel est l'ordre correct des niveaux pour **www.google.com** ? (Choix unique)

- [ ] www → google → com → root (.)
- [ ] root (.) → com → google → www
- [ ] com → root (.) → google → www
- [ ] google → www → com → root (.)

---

## Question 7
Quels types d'enregistrements DNS sont corrects ? (Choix multiples - Sélectionner 4 réponses)

- [ ] **A** : Associe un nom de domaine à une adresse IPv4
- [ ] **AAAA** : Associe un nom de domaine à une adresse IPv6
- [ ] **CNAME** : Crée un alias vers un autre nom de domaine
- [ ] **MX** : Spécifie le serveur de messagerie pour un domaine
- [ ] **PTR** : Associe un nom de domaine à un port TCP

---

## Question 8
Quelle est la signification de **TTL (Time To Live)** dans le contexte DNS ? (Choix unique)

- [ ] Le nombre maximum de sauts qu'un paquet peut effectuer
- [ ] La durée de validité d'un enregistrement DNS en cache (en secondes)
- [ ] Le temps maximal pour établir une connexion TCP
- [ ] La taille maximale d'une réponse DNS

---

## Question 9
Quel est le rôle du protocole **DHCP** ? (Choix unique)

- [ ] Traduire les noms de domaine en adresses IP
- [ ] Attribuer automatiquement des adresses IP, masques, passerelles et DNS
- [ ] Transférer des fichiers entre un client et un serveur
- [ ] Synchroniser l'horloge système avec un serveur de temps

---

## Question 10
Quels sont les ports utilisés par DHCP et leur protocole de transport ? (Choix unique)

- [ ] 67 (serveur) et 68 (client) - TCP
- [ ] 67 (serveur) et 68 (client) - UDP
- [ ] 53 (serveur) et 54 (client) - UDP
- [ ] 80 (serveur) et 81 (client) - TCP

---

## Question 11
Dans le processus **DORA** de DHCP, que signifie chaque lettre ? (Choix unique)

- [ ] Deliver, Offer, Request, Assign
- [ ] Discover, Offer, Request, Acknowledge
- [ ] Discover, Order, Receive, Accept
- [ ] Deliver, Order, Request, Accept

---

## Question 12
Un client DHCP envoie un message **DHCP DISCOVER**. Quelle est l'adresse IP destination utilisée ? (Choix unique)

- [ ] 127.0.0.1 (localhost)
- [ ] 0.0.0.0 (pas d'IP)
- [ ] 255.255.255.255 (broadcast)
- [ ] 192.168.1.1 (passerelle par défaut)

---

## Question 13
Quel est le rôle du **DHCP Relay Agent** (ip helper-address sur Cisco) ? (Choix unique)

- [ ] Accélérer les réponses DHCP en mettant en cache les attributions
- [ ] Convertir les broadcasts DHCP en unicast pour traverser les routeurs
- [ ] Chiffrer les communications DHCP pour plus de sécurité
- [ ] Équilibrer la charge entre plusieurs serveurs DHCP

---

## Question 14
Quels protocoles sont utilisés pour les **emails** et quels sont leurs rôles ? (Choix multiples - Sélectionner 3 réponses)

- [ ] **SMTP (port 25)** : Envoi d'emails de serveur à serveur
- [ ] **POP3 (port 110)** : Réception d'emails avec téléchargement local
- [ ] **IMAP (port 143)** : Gestion d'emails avec synchronisation serveur
- [ ] **FTP (port 21)** : Envoi d'emails chiffrés
- [ ] **DNS (port 53)** : Résolution des adresses email

---

## Question 15
Quelle est la différence principale entre **POP3** et **IMAP** ? (Choix unique)

- [ ] POP3 utilise TCP, IMAP utilise UDP
- [ ] POP3 télécharge les emails localement (un seul appareil), IMAP synchronise avec le serveur (multi-appareils)
- [ ] POP3 est sécurisé, IMAP ne l'est pas
- [ ] POP3 gère les dossiers, IMAP non

---

## Question 16
Quel protocole utilise le port **445** et à quoi sert-il ? (Choix unique)

- [ ] FTP - Transfert de fichiers
- [ ] SMB - Partage de fichiers et d'imprimantes
- [ ] SMTP - Envoi d'emails
- [ ] SSH - Accès distant sécurisé

---

## Question 17
Quelle est la différence entre **FTP** et **TFTP** ? (Choix multiples - Sélectionner 3 réponses)

- [ ] FTP utilise TCP, TFTP utilise UDP
- [ ] FTP nécessite une authentification, TFTP non
- [ ] FTP utilise les ports 20-21, TFTP utilise le port 69
- [ ] TFTP est plus sécurisé que FTP
- [ ] FTP est plus complexe et fiable que TFTP

---

## Question 18
Quel protocole doit-on utiliser à la place de **Telnet** pour un accès distant sécurisé ? (Choix unique)

- [ ] FTP
- [ ] SSH
- [ ] HTTP
- [ ] TFTP

---

## Question 19
Associez les protocoles suivants à leur numéro de port correct. (Choix multiples - Sélectionner 4 réponses)

- [ ] **HTTP** : 80
- [ ] **HTTPS** : 443
- [ ] **DNS** : 53
- [ ] **DHCP Client** : 68
- [ ] **SMTP** : 110
- [ ] **FTP Data** : 443

---

## Question 20
Un utilisateur tape **www.cisco.com** dans son navigateur. Dans quel ordre les serveurs DNS sont-ils interrogés lors de la **résolution récursive** ? (Choix unique)

- [ ] Serveur cisco.com → Serveur .com → Root Server
- [ ] Root Server → Serveur .com → Serveur cisco.com
- [ ] Serveur .com → Root Server → Serveur cisco.com
- [ ] Serveur cisco.com → Root Server → Serveur .com

---

## Réponses et explications

### Question 1
**Réponse correcte :** B (HTTP : 80, HTTPS : 443)

**Explication :**  
- **HTTP** utilise le port **80** (TCP) pour le web non sécurisé
- **HTTPS** utilise le port **443** (TCP) pour le web sécurisé avec chiffrement SSL/TLS

HTTPS est simplement HTTP encapsulé dans une connexion TLS, garantissant **confidentialité, intégrité** et **authentification** du serveur via des certificats SSL.

---

### Question 2
**Réponse correcte :** B (GET)

**Explication :**  
La méthode **GET** est utilisée pour **récupérer une ressource** (page HTML, image, fichier CSS, etc.) depuis le serveur. C'est la méthode HTTP la plus courante.

Les autres méthodes :
- **POST** : Envoyer des données au serveur (formulaires)
- **PUT** : Créer ou remplacer une ressource
- **DELETE** : Supprimer une ressource

---

### Question 3
**Réponse correcte :** C (Ressource introuvable)

**Explication :**  
Le code **404 Not Found** signifie que la ressource demandée (page, image, fichier) n'existe **pas** sur le serveur. C'est l'une des erreurs HTTP les plus connues.

Les autres codes importants :
- **200 OK** : Succès
- **301 Moved Permanently** : Redirection permanente
- **400 Bad Request** : Requête mal formée
- **401 Unauthorized** : Authentification requise
- **403 Forbidden** : Accès interdit
- **500 Internal Server Error** : Erreur serveur
- **503 Service Unavailable** : Serveur surchargé

---

### Question 4
**Réponse correcte :** B (Traduire les noms de domaine en adresses IP)

**Explication :**  
Le **DNS (Domain Name System)** est le "annuaire d'Internet". Il traduit les **noms de domaine** lisibles par les humains (ex : www.google.com) en **adresses IP** utilisables par les machines (ex : 142.250.185.78).

Sans DNS, il faudrait mémoriser les adresses IP de tous les sites web !

---

### Question 5
**Réponse correcte :** C (UDP pour les requêtes, TCP pour les transferts de zones)

**Explication :**  
Le DNS utilise le **port 53** avec deux protocoles :
- **UDP** : Pour les **requêtes/réponses DNS standard** (< 512 octets) - rapide et léger
- **TCP** : Pour les **transferts de zones** (AXFR, IXFR) entre serveurs DNS - fiabilité nécessaire

La plupart du temps, DNS utilise **UDP** pour la rapidité. Si la réponse dépasse 512 octets, TCP est utilisé.

---

### Question 6
**Réponse correcte :** B (root (.) → com → google → www)

**Explication :**  
La hiérarchie DNS fonctionne de **droite à gauche** et du **haut vers le bas** :

1. **Root (.)** : Racine (13 serveurs racine : a.root-servers.net à m.root-servers.net)
2. **TLD (.com)** : Top-Level Domain (.com, .org, .fr, .net)
3. **Second-Level (google)** : Nom de domaine enregistré (google.com)
4. **Subdomain (www)** : Sous-domaine (www.google.com, mail.google.com)

Le FQDN complet est : **www.google.com.**

---

### Question 7
**Réponses correctes :** A, B, C, D

**Explication :**  
Les types d'enregistrements DNS corrects :
- **A (Address)** : Nom → **IPv4** (www.example.com → 93.184.216.34)
- **AAAA** : Nom → **IPv6** (www.example.com → 2606:2800:220:1:...)
- **CNAME (Canonical Name)** : **Alias** (blog.example.com → www.example.com)
- **MX (Mail Exchange)** : **Serveur email** (example.com → mail.example.com)

Les autres types importants :
- **NS** : Serveur DNS autoritaire
- **PTR** : Résolution **inverse** (IP → Nom)
- **TXT** : Texte libre (SPF, DKIM)

**PTR** n'associe **pas** un nom à un port TCP.

---

### Question 8
**Réponse correcte :** B (La durée de validité d'un enregistrement DNS en cache, en secondes)

**Explication :**  
Le **TTL (Time To Live)** dans DNS indique la **durée de validité** (en secondes) d'un enregistrement DNS dans le cache. Une fois le TTL expiré, le résolveur doit **interroger à nouveau** le serveur DNS autoritaire.

**Exemples :**
- **TTL = 3600** → Valide 1 heure
- **TTL = 86400** → Valide 24 heures
- **TTL faible** → Mises à jour rapides (changement d'IP)
- **TTL élevé** → Moins de requêtes DNS (performance)

---

### Question 9
**Réponse correcte :** B (Attribuer automatiquement des adresses IP, masques, passerelles et DNS)

**Explication :**  
Le **DHCP (Dynamic Host Configuration Protocol)** permet l'**allocation automatique** de paramètres réseau aux clients :
- **Adresse IP** (Yiaddr)
- **Masque de sous-réseau** (Option 1)
- **Passerelle par défaut** (Option 3)
- **Serveurs DNS** (Option 6)
- **Durée du bail (Lease)** (Option 51)

Sans DHCP, il faudrait configurer **manuellement** chaque appareil (erreurs, conflits d'IP).

---

### Question 10
**Réponse correcte :** B (67 (serveur) et 68 (client) - UDP)

**Explication :**  
DHCP utilise le protocole **UDP** (sans connexion, rapide) avec :
- **Port 67** : Serveur DHCP (écoute sur ce port)
- **Port 68** : Client DHCP (reçoit les réponses sur ce port)

DHCP utilise UDP car il doit fonctionner **avant** que le client n'ait une adresse IP (broadcast initial).

---

### Question 11
**Réponse correcte :** B (Discover, Offer, Request, Acknowledge)

**Explication :**  
Le processus **DORA** décrit les 4 étapes d'obtention d'une adresse IP via DHCP :

1. **Discover** : Client → Broadcast (recherche serveur DHCP)
2. **Offer** : Serveur → Client (propose IP + config)
3. **Request** : Client → Broadcast (accepte l'offre)
4. **Acknowledge** : Serveur → Client (confirme l'attribution)

À la fin du processus DORA, le client a une **adresse IP valide** et peut communiquer sur le réseau.

---

### Question 12
**Réponse correcte :** C (255.255.255.255 - broadcast)

**Explication :**  
Le message **DHCP DISCOVER** est envoyé en **broadcast** car :
- Le client **n'a pas encore d'adresse IP** (source : 0.0.0.0)
- Il ne connaît **pas l'adresse du serveur DHCP**
- Il doit **joindre tous les serveurs DHCP** du réseau local

**Destination : 255.255.255.255** (broadcast de niveau 2 et 3)

Tous les serveurs DHCP du réseau local recevront le DISCOVER et peuvent répondre avec un OFFER.

---

### Question 13
**Réponse correcte :** B (Convertir les broadcasts DHCP en unicast pour traverser les routeurs)

**Explication :**  
**Problème** : Les broadcasts DHCP (255.255.255.255) ne traversent **pas** les routeurs par défaut.

**Solution** : Le **DHCP Relay Agent** (configuré avec `ip helper-address` sur Cisco) :
1. Reçoit le broadcast DHCP DISCOVER du client
2. Le **convertit en unicast**
3. L'envoie au serveur DHCP (sur un autre réseau)
4. **Relaye la réponse** du serveur au client

Cela permet d'avoir **un seul serveur DHCP** pour plusieurs sous-réseaux.

---

### Question 14
**Réponses correctes :** A, B, C

**Explication :**  
Les **3 protocoles email** principaux :

1. **SMTP (Simple Mail Transfer Protocol) - Port 25/587** :
   - **Envoi** d'emails (client → serveur, serveur → serveur)
   - Port 25 : Serveur à serveur
   - Port 587 : Client à serveur avec TLS

2. **POP3 (Post Office Protocol v3) - Port 110** :
   - **Réception** d'emails avec téléchargement local
   - Emails supprimés du serveur après téléchargement

3. **IMAP (Internet Message Access Protocol) - Port 143** :
   - **Gestion** d'emails avec synchronisation serveur
   - Emails restent sur le serveur, multi-appareils

---

### Question 15
**Réponse correcte :** B (POP3 télécharge localement, IMAP synchronise avec le serveur)

**Explication :**  
**Comparaison POP3 vs IMAP** :

| Critère | POP3 | IMAP |
|---------|------|------|
| **Stockage** | Local (client) | Serveur |
| **Synchronisation** | Non | Oui |
| **Multi-appareils** | Non (un seul appareil) | Oui (PC, smartphone, tablette) |
| **Gestion dossiers** | Non | Oui (INBOX, Sent, Drafts) |

**Utilisation recommandée** :
- **POP3** : Un seul appareil, stockage local
- **IMAP** : Plusieurs appareils, synchronisation nécessaire

---

### Question 16
**Réponse correcte :** B (SMB - Partage de fichiers et d'imprimantes)

**Explication :**  
Le protocole **SMB (Server Message Block)** utilise le port **445 (TCP)** pour le **partage de fichiers et d'imprimantes** sur réseau local :
- **Windows** : Partages réseau (\\SERVEUR\Partage)
- **Linux** : Samba (implémentation open-source de SMB)
- **macOS** : Support SMB natif

**Important** : SMB 1.0 doit être **désactivé** (vulnérabilités critiques : WannaCry, EternalBlue). Utiliser **SMB 3.0+**.

---

### Question 17
**Réponses correctes :** A, B, C, E

**Explication :**  
**Différences FTP vs TFTP** :

| Critère | FTP | TFTP |
|---------|-----|------|
| **Protocole** | **TCP** (fiable) | **UDP** (simple) |
| **Authentification** | **Oui** (user/pass) | **Non** |
| **Ports** | **20 (données), 21 (contrôle)** | **69** |
| **Complexité** | **Élevée** (commandes, modes) | **Faible** (basique) |
| **Sécurité** | Peut être sécurisé (FTPS, SFTP) | **Non sécurisé** |

**Usage** :
- **FTP** : Transfert de fichiers général
- **TFTP** : Boot réseau (PXE), configuration routeurs/switches

TFTP est **moins sécurisé** que FTP.

---

### Question 18
**Réponse correcte :** B (SSH)

**Explication :**  
**Telnet (port 23)** transmet les données **en clair**, y compris les mots de passe. C'est un risque de sécurité majeur.

**SSH (Secure Shell, port 22)** doit être utilisé à la place car :
- ✅ **Chiffrement** : Toutes les données sont chiffrées
- ✅ **Authentification** : Clés publiques/privées ou mot de passe
- ✅ **Intégrité** : Protection contre la manipulation
- ✅ **Tunneling** : Port forwarding, SFTP

**Telnet doit être désactivé** sur tous les équipements réseau.

---

### Question 19
**Réponses correctes :** A, B, C, D

**Explication :**  
Les ports corrects :
- **HTTP** : **80** (TCP)
- **HTTPS** : **443** (TCP)
- **DNS** : **53** (UDP/TCP)
- **DHCP Client** : **68** (UDP)

Les erreurs :
- **SMTP** utilise le port **25** (pas 110 qui est POP3)
- **FTP Data** utilise le port **20** (pas 443 qui est HTTPS)

**Autres ports importants** :
- FTP Control : 21
- SSH : 22
- Telnet : 23
- POP3 : 110
- IMAP : 143
- SMB : 445
- RDP : 3389

---

### Question 20
**Réponse correcte :** B (Root Server → Serveur .com → Serveur cisco.com)

**Explication :**  
La **résolution DNS récursive** suit cet ordre :

1. **Client → Résolveur DNS** (ex : 8.8.8.8) : "Quelle est l'IP de www.cisco.com ?"

2. **Résolveur → Root Server** (.) : "Où trouver .com ?"
   - Root → Résolveur : "Demande à X.X.X.X (serveur TLD .com)"

3. **Résolveur → Serveur .com** : "Où trouver cisco.com ?"
   - Serveur .com → Résolveur : "Demande à Y.Y.Y.Y (serveur cisco.com)"

4. **Résolveur → Serveur cisco.com** : "Quelle est l'IP de www.cisco.com ?"
   - Serveur cisco.com → Résolveur : "72.163.4.185"

5. **Résolveur → Client** : "www.cisco.com = 72.163.4.185"

Le résolveur fait tout le travail (récursif), le client reçoit juste la réponse finale.

---

**Fin du QCM Module 15**

**Score de passage :** 15/20 (75%)  
**Bonne chance !** 🚀
