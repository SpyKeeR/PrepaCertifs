# Module 15 - Protocoles de la couche Application

**Date :** 27 février 2026  
**Cours :** CCNA ITN (Introduction to Networks)  
**Sujet :** Protocoles de la couche Application (Layer 7)

---

## 1. Introduction à la couche Application

### Rôle de la couche 7

La **couche Application** (Layer 7 du modèle OSI) est la couche la plus proche de l'utilisateur final :
- **Interface utilisateur** : interaction entre l'application et le réseau
- **Services réseau** : accès aux ressources réseau (fichiers, emails, web, etc.)
- **Protocoles applicatifs** : définissent le format et les règles de communication

### Modèle OSI vs TCP/IP

| Modèle OSI | Modèle TCP/IP | Exemples |
|------------|---------------|----------|
| **7. Application** | **Application** | HTTP, DNS, SMTP, FTP, SSH |
| **6. Présentation** | (Intégré dans Application) | Chiffrement SSL/TLS, encodage |
| **5. Session** | (Intégré dans Application) | Gestion de sessions |
| 4. Transport | Transport | TCP, UDP |
| 3. Réseau | Internet | IP, ICMP |
| 2. Liaison | Accès réseau | Ethernet, Wi-Fi |
| 1. Physique | (Intégré dans Accès réseau) | Câbles, ondes radio |

### Modèle Client-Serveur

La plupart des protocoles applicatifs utilisent le **modèle client-serveur** :
- **Client** : initie la connexion, demande des services
- **Serveur** : écoute sur un port, répond aux requêtes

**Exemple :**
```
Client (192.168.1.10:54321) → Serveur (93.184.216.34:80)
Requête : GET /index.html HTTP/1.1

Serveur → Client
Réponse : HTTP/1.1 200 OK + contenu de la page
```

### Modèle Peer-to-Peer (P2P)

Alternative au client-serveur :
- Chaque nœud est **à la fois client et serveur**
- Partage de ressources décentralisé
- **Exemples** : BitTorrent, Skype (ancien), blockchain

---

## 2. HTTP et HTTPS (Web)

### 2.1 HTTP (HyperText Transfer Protocol)

HTTP est le protocole du **World Wide Web** :
- **Port** : 80 (TCP)
- **Fonction** : Transfert de pages web (HTML, CSS, JavaScript, images, etc.)
- **Modèle** : Requête-Réponse (Request-Response)
- **Sans état** : Chaque requête est indépendante (utilise cookies pour sessions)

#### Méthodes HTTP

| Méthode | Rôle |
|---------|------|
| **GET** | Récupérer une ressource |
| **POST** | Envoyer des données au serveur (formulaires) |
| **PUT** | Créer ou remplacer une ressource |
| **DELETE** | Supprimer une ressource |
| **HEAD** | Récupérer uniquement les en-têtes (sans body) |
| **OPTIONS** | Lister les méthodes supportées |
| **PATCH** | Modification partielle d'une ressource |

#### Codes de statut HTTP

| Code | Catégorie | Signification |
|------|-----------|---------------|
| **1xx** | Information | Requête reçue, traitement en cours |
| **2xx** | Succès | Requête traitée avec succès |
| **3xx** | Redirection | Redirection vers une autre URL |
| **4xx** | Erreur client | Erreur dans la requête du client |
| **5xx** | Erreur serveur | Erreur lors du traitement côté serveur |

**Codes courants :**
- **200 OK** : Succès
- **301 Moved Permanently** : Redirection permanente
- **302 Found** : Redirection temporaire
- **400 Bad Request** : Requête mal formée
- **401 Unauthorized** : Authentification requise
- **403 Forbidden** : Accès interdit
- **404 Not Found** : Ressource introuvable
- **500 Internal Server Error** : Erreur serveur
- **503 Service Unavailable** : Serveur surchargé ou en maintenance

#### Structure d'une requête HTTP

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
Accept-Language: fr-FR
Connection: keep-alive
```

#### Structure d'une réponse HTTP

```http
HTTP/1.1 200 OK
Date: Thu, 27 Feb 2026 10:00:00 GMT
Server: Apache/2.4.41
Content-Type: text/html; charset=UTF-8
Content-Length: 1234
Connection: keep-alive

<!DOCTYPE html>
<html>
...
</html>
```

### 2.2 HTTPS (HTTP Secure)

HTTPS est HTTP **chiffré avec SSL/TLS** :
- **Port** : 443 (TCP)
- **Fonction** : Même que HTTP, mais sécurisé
- **Sécurité** : Chiffrement, intégrité, authentification du serveur
- **Certificat SSL/TLS** : Émis par une autorité de certification (CA)

#### Protocoles de sécurité

| Protocole | Statut | Versions |
|-----------|--------|----------|
| **SSL** (Secure Sockets Layer) | Obsolète (vulnérable) | SSL 2.0, 3.0 |
| **TLS** (Transport Layer Security) | Actuel | TLS 1.0, 1.1 (déprécié), **1.2**, **1.3** |

**TLS 1.2 et 1.3** sont les versions recommandées actuellement.

#### Fonctionnement HTTPS

1. **Client → Serveur** : Client Hello (versions TLS, suites de chiffrement supportées)
2. **Serveur → Client** : Server Hello (version TLS choisie, suite de chiffrement, **certificat**)
3. **Client** : Vérification du certificat (chaîne de confiance, CA, validité)
4. **Échange de clés** : Diffie-Hellman ou RSA pour établir une clé de session
5. **Communication chiffrée** : Toutes les données HTTP sont chiffrées avec la clé de session

#### Avantages HTTPS

- ✅ **Confidentialité** : Les données sont chiffrées
- ✅ **Intégrité** : Les données ne peuvent pas être modifiées
- ✅ **Authentification** : Le certificat prouve l'identité du serveur
- ✅ **SEO** : Google privilégie les sites HTTPS

---

## 3. DNS (Domain Name System)

### 3.1 Fonction du DNS

Le DNS est le **service d'annuaire d'Internet** :
- **Fonction** : Traduire noms de domaine → adresses IP
- **Port** : 53 (UDP pour requêtes, TCP pour transferts de zones)
- **Exemple** : www.google.com → 142.250.185.78

### 3.2 Hiérarchie DNS

Le DNS est organisé en **hiérarchie** :

```
                    . (root)
                    |
        ┌───────────┼───────────┐
       .com        .org        .fr
        |           |           |
   ┌────┼────┐      |      ┌────┼────┐
 google cisco yahoo |    gouv orange
   |                |      |
  www              www    www
```

**Niveaux DNS :**
1. **Root (.)** : 13 serveurs racine (a.root-servers.net à m.root-servers.net)
2. **TLD (Top-Level Domain)** : .com, .org, .fr, .net, .edu, etc.
3. **Second-Level Domain** : google.com, cisco.com
4. **Subdomain** : www.google.com, mail.google.com

### 3.3 Types d'enregistrements DNS

| Type | Nom complet | Rôle |
|------|-------------|------|
| **A** | Address | IPv4 address (www.example.com → 93.184.216.34) |
| **AAAA** | IPv6 Address | IPv6 address (www.example.com → 2606:2800:220:1:...) |
| **CNAME** | Canonical Name | Alias vers un autre nom (blog.example.com → www.example.com) |
| **MX** | Mail Exchange | Serveur de messagerie (example.com → mail.example.com) |
| **NS** | Name Server | Serveur DNS autoritaire pour la zone |
| **PTR** | Pointer | Résolution inverse (IP → Nom) |
| **TXT** | Text | Texte libre (SPF, DKIM, vérifications) |
| **SOA** | Start of Authority | Informations sur la zone DNS |
| **SRV** | Service | Services disponibles (SIP, XMPP) |

### 3.4 Processus de résolution DNS

#### Résolution récursive (client → serveur DNS récursif)

```
1. Client tape : www.google.com

2. Client → Résolveur DNS (8.8.8.8)
   "Quelle est l'adresse IP de www.google.com ?"

3. Résolveur → Root Server
   "Où trouver .com ?"
   Root → Résolveur : "Demande à X.X.X.X (serveur .com)"

4. Résolveur → Serveur .com
   "Où trouver google.com ?"
   Serveur .com → Résolveur : "Demande à Y.Y.Y.Y (serveur google.com)"

5. Résolveur → Serveur google.com
   "Quelle est l'IP de www.google.com ?"
   Serveur google.com → Résolveur : "142.250.185.78"

6. Résolveur → Client
   "www.google.com = 142.250.185.78"

7. Client se connecte à 142.250.185.78
```

### 3.5 Cache DNS

Pour accélérer les résolutions, le DNS utilise un **cache** :
- **Résolveur DNS** : met en cache les réponses (TTL = Time To Live)
- **Système d'exploitation** : cache local (Windows, Linux, macOS)
- **Navigateur** : cache interne

**TTL (Time To Live)** :
- Durée de validité d'un enregistrement DNS (en secondes)
- Exemple : A record avec TTL=3600 → valide 1 heure

### 3.6 Serveurs DNS publics

| Fournisseur | Adresses IP |
|-------------|-------------|
| **Google Public DNS** | 8.8.8.8, 8.8.4.4 |
| **Cloudflare DNS** | 1.1.1.1, 1.0.0.1 |
| **Quad9** | 9.9.9.9, 149.112.112.112 |
| **OpenDNS** | 208.67.222.222, 208.67.220.220 |

### 3.7 Commandes DNS

#### Windows

```powershell
# Résolution DNS
nslookup www.google.com

# Résolution avec serveur spécifique
nslookup www.google.com 8.8.8.8

# Afficher le cache DNS
ipconfig /displaydns

# Vider le cache DNS
ipconfig /flushdns
```

#### Linux

```bash
# Résolution DNS (ancien)
nslookup www.google.com

# Résolution DNS (moderne)
dig www.google.com

# Résolution DNS simple
host www.google.com

# Vider le cache DNS (systemd-resolved)
sudo systemd-resolve --flush-caches
```

### 3.8 DNSSEC

**DNSSEC (DNS Security Extensions)** ajoute la sécurité au DNS :
- Signature cryptographique des enregistrements DNS
- Prévention du **DNS spoofing** (empoisonnement du cache)
- Authentification et intégrité

---

## 4. DHCP (Dynamic Host Configuration Protocol)

### 4.1 Fonction du DHCP

DHCP permet l'**allocation automatique d'adresses IP** :
- **Fonction** : Attribuer IP, masque, passerelle, DNS automatiquement
- **Ports** : 67 (serveur), 68 (client) - **UDP**
- **Avantage** : Pas de configuration manuelle, gestion centralisée

### 4.2 Processus DHCP (DORA)

Le processus d'obtention d'une adresse IP comporte **4 étapes** (DORA) :

```
Client                        Serveur DHCP
  |                               |
  | 1. DHCP DISCOVER (broadcast)  |
  |------------------------------>|
  | Source: 0.0.0.0               |
  | Destination: 255.255.255.255  |
  | "Y a-t-il un serveur DHCP ?"  |
  |                               |
  | 2. DHCP OFFER (unicast ou     |
  |    broadcast)                 |
  |<------------------------------|
  | "Voici une IP : 192.168.1.100"|
  | + masque, passerelle, DNS     |
  |                               |
  | 3. DHCP REQUEST (broadcast)   |
  |------------------------------>|
  | "J'accepte l'IP 192.168.1.100"|
  |                               |
  | 4. DHCP ACK (unicast)         |
  |<------------------------------|
  | "Confirmation, IP attribuée"  |
  |                               |
```

#### Détails des étapes DORA

1. **DHCP DISCOVER** : Le client envoie un broadcast pour trouver un serveur DHCP
   - Source IP : 0.0.0.0 (pas encore d'IP)
   - Destination IP : 255.255.255.255 (broadcast)

2. **DHCP OFFER** : Le serveur propose une adresse IP
   - Contient : IP proposée, masque, passerelle, DNS, bail (lease)

3. **DHCP REQUEST** : Le client accepte l'offre (ou en choisit une si plusieurs serveurs)
   - Broadcast pour informer les autres serveurs

4. **DHCP ACK** : Le serveur confirme l'attribution
   - L'IP est maintenant attribuée au client

### 4.3 Informations fournies par DHCP

| Information | Option DHCP | Exemple |
|-------------|-------------|---------|
| **Adresse IP** | Yiaddr | 192.168.1.100 |
| **Masque de sous-réseau** | Option 1 | 255.255.255.0 |
| **Passerelle par défaut** | Option 3 | 192.168.1.1 |
| **Serveur DNS** | Option 6 | 8.8.8.8, 8.8.4.4 |
| **Durée du bail (Lease)** | Option 51 | 86400 secondes (24h) |
| **Serveur TFTP** | Option 66 | 192.168.1.10 (pour PXE) |
| **Nom de domaine DNS** | Option 15 | example.com |

### 4.4 Durée du bail (Lease)

Le **bail DHCP** a une durée limitée :
- Le client doit **renouveler** le bail avant expiration
- **T1 (50% du bail)** : Le client demande un renouvellement au serveur DHCP qui a attribué l'IP
- **T2 (87.5% du bail)** : Si pas de réponse, le client envoie un broadcast à tous les serveurs
- **Expiration** : Si aucune réponse, le client perd l'IP et recommence DORA

**Exemple :**
```
Bail = 24 heures (86400 secondes)
T1 = 12 heures → Renouvellement auprès du serveur
T2 = 21 heures → Broadcast si T1 échoue
Expiration = 24 heures → Perte de l'IP
```

### 4.5 DHCP Relay Agent

**Problème** : DHCP utilise le **broadcast** (ne traverse pas les routeurs)

**Solution** : **DHCP Relay Agent** (ip helper-address sur Cisco)
- Le routeur reçoit le broadcast DHCP DISCOVER
- Il le **convertit en unicast** et l'envoie au serveur DHCP
- Le serveur répond au routeur
- Le routeur **renvoie la réponse au client**

**Configuration Cisco IOS :**
```cisco
interface GigabitEthernet0/0
 ip helper-address 10.1.1.10
```

### 4.6 Commandes DHCP

#### Windows

```powershell
# Afficher la configuration IP (incluant DHCP)
ipconfig /all

# Libérer l'adresse IP DHCP
ipconfig /release

# Renouveler l'adresse IP DHCP
ipconfig /renew
```

#### Linux

```bash
# Afficher la configuration IP
ip addr show
ifconfig

# Libérer et renouveler (dhclient)
sudo dhclient -r eth0  # Release
sudo dhclient eth0     # Renew

# Libérer et renouveler (NetworkManager)
sudo nmcli connection down "Connexion Ethernet"
sudo nmcli connection up "Connexion Ethernet"
```

### 4.7 DHCPv6

**DHCPv6** fonctionne de manière similaire pour IPv6 :
- **Ports** : 546 (client), 547 (serveur)
- **Multicast** : FF02::1:2 (All_DHCP_Relay_Agents_and_Servers)
- **Processus** : SOLICIT, ADVERTISE, REQUEST, REPLY
- **3 méthodes d'allocation** : SLAAC Only, SLAAC + DHCPv6 Stateless, DHCPv6 Stateful

---

## 5. SMTP, POP et IMAP (Email)

### 5.1 Fonctionnement général

Les emails utilisent **3 protocoles** :
- **SMTP** : Envoi d'emails (client → serveur, serveur → serveur)
- **POP/IMAP** : Réception d'emails (serveur → client)

```
Expéditeur (Alice)
    |
    | SMTP (port 25)
    ↓
Serveur SMTP (smtp.alice.com)
    |
    | SMTP (port 25)
    ↓
Serveur SMTP (smtp.bob.com)
    |
    | POP/IMAP (port 110/143)
    ↓
Destinataire (Bob)
```

### 5.2 SMTP (Simple Mail Transfer Protocol)

SMTP est le protocole d'**envoi d'emails** :
- **Port** : 25 (serveur à serveur), 587 (client à serveur, avec TLS), 465 (SMTPS, obsolète)
- **Protocole** : TCP
- **Fonction** : Relayer les emails d'un serveur à l'autre

#### Commandes SMTP

| Commande | Rôle |
|----------|------|
| **HELO/EHLO** | Identification du client |
| **MAIL FROM** | Adresse de l'expéditeur |
| **RCPT TO** | Adresse du destinataire |
| **DATA** | Début du contenu de l'email |
| **QUIT** | Terminer la session |
| **RSET** | Réinitialiser la session |
| **VRFY** | Vérifier l'existence d'une adresse |
| **NOOP** | Aucune opération (keep-alive) |

#### Exemple de session SMTP

```smtp
Client: EHLO client.example.com
Serveur: 250-smtp.example.com Hello client.example.com
Serveur: 250-SIZE 10240000
Serveur: 250 STARTTLS

Client: MAIL FROM:<alice@example.com>
Serveur: 250 OK

Client: RCPT TO:<bob@example.com>
Serveur: 250 OK

Client: DATA
Serveur: 354 Start mail input; end with <CRLF>.<CRLF>

Client: From: alice@example.com
Client: To: bob@example.com
Client: Subject: Test Email
Client:
Client: Bonjour Bob, ceci est un test.
Client: .
Serveur: 250 OK

Client: QUIT
Serveur: 221 Bye
```

#### SMTP sécurisé

- **STARTTLS** (port 587) : Commande pour passer en TLS
- **SMTPS** (port 465) : SMTP sur SSL (obsolète, remplacé par STARTTLS)

### 5.3 POP (Post Office Protocol)

POP est un protocole de **réception d'emails** :
- **Port** : 110 (POP3), 995 (POP3S avec SSL/TLS)
- **Protocole** : TCP
- **Fonction** : Télécharger les emails du serveur vers le client

#### Caractéristiques de POP3

- ✅ **Simple** : Téléchargement des emails
- ❌ **Pas de synchronisation** : Les emails sont supprimés du serveur après téléchargement
- ❌ **Un seul appareil** : Pas adapté pour accès multi-appareils
- ✅ **Stockage local** : Les emails sont stockés sur l'appareil client

#### Commandes POP3

| Commande | Rôle |
|----------|------|
| **USER** | Nom d'utilisateur |
| **PASS** | Mot de passe |
| **STAT** | Statistiques (nombre de messages, taille totale) |
| **LIST** | Lister les messages |
| **RETR** | Récupérer un message |
| **DELE** | Supprimer un message |
| **QUIT** | Terminer la session (appliquer les suppressions) |

#### Exemple de session POP3

```pop3
Client: USER alice
Serveur: +OK

Client: PASS motdepasse123
Serveur: +OK Logged in

Client: STAT
Serveur: +OK 2 320

Client: LIST
Serveur: +OK 2 messages (320 octets)
Serveur: 1 120
Serveur: 2 200
Serveur: .

Client: RETR 1
Serveur: +OK 120 octets
Serveur: [contenu de l'email]
Serveur: .

Client: DELE 1
Serveur: +OK Message 1 deleted

Client: QUIT
Serveur: +OK Logging out
```

### 5.4 IMAP (Internet Message Access Protocol)

IMAP est un protocole de **gestion d'emails** :
- **Port** : 143 (IMAP), 993 (IMAPS avec SSL/TLS)
- **Protocole** : TCP
- **Fonction** : Gérer les emails directement sur le serveur

#### Caractéristiques d'IMAP

- ✅ **Synchronisation** : Les emails restent sur le serveur
- ✅ **Multi-appareils** : Accès depuis plusieurs appareils (PC, smartphone, tablette)
- ✅ **Gestion avancée** : Dossiers, flags (lu/non lu), recherche
- ✅ **Accès sélectif** : Télécharger uniquement les en-têtes ou corps au besoin
- ❌ **Consomme de l'espace serveur** : Nécessite de la capacité de stockage serveur

#### Commandes IMAP

| Commande | Rôle |
|----------|------|
| **LOGIN** | Authentification |
| **SELECT** | Sélectionner un dossier (INBOX, Sent, etc.) |
| **FETCH** | Récupérer un message ou une partie |
| **STORE** | Modifier les flags d'un message (lu, supprimé, etc.) |
| **SEARCH** | Rechercher des messages |
| **CREATE** | Créer un dossier |
| **DELETE** | Supprimer un dossier |
| **LOGOUT** | Terminer la session |

### 5.5 Comparaison POP3 vs IMAP

| Critère | POP3 | IMAP |
|---------|------|------|
| **Stockage** | Local (client) | Serveur |
| **Synchronisation** | Non | Oui |
| **Multi-appareils** | Non | Oui |
| **Gestion dossiers** | Non | Oui (INBOX, Sent, Drafts, etc.) |
| **Flags (lu/non lu)** | Non | Oui |
| **Consommation bande passante** | Élevée (télécharge tout) | Faible (télécharge à la demande) |
| **Espace serveur** | Faible (emails supprimés) | Élevé (emails conservés) |
| **Complexité** | Simple | Plus complexe |
| **Usage recommandé** | Un seul appareil | Plusieurs appareils |

---

## 6. FTP et TFTP (Transfert de fichiers)

### 6.1 FTP (File Transfer Protocol)

FTP est un protocole de **transfert de fichiers** :
- **Ports** : 21 (contrôle), 20 (données) - **TCP**
- **Fonction** : Upload/Download de fichiers
- **Authentification** : Nom d'utilisateur et mot de passe

#### Modes FTP

| Mode | Description |
|------|-------------|
| **Mode Actif** | Le serveur initie la connexion de données vers le client (problématique avec NAT/firewall) |
| **Mode Passif** | Le client initie les deux connexions (contrôle et données) |

#### FTP sécurisé

- **FTPS** (FTP Secure) : FTP sur SSL/TLS (ports 990, 989)
- **SFTP** (SSH File Transfer Protocol) : FTP via SSH (port 22)

### 6.2 TFTP (Trivial File Transfer Protocol)

TFTP est une **version simplifiée de FTP** :
- **Port** : 69 - **UDP**
- **Fonction** : Transfert de fichiers simple
- **Pas d'authentification** : Aucun mot de passe
- **Usage** : Boot réseau (PXE), configuration de routeurs/switches

#### Différences FTP vs TFTP

| Critère | FTP | TFTP |
|---------|-----|------|
| **Protocole** | TCP | UDP |
| **Authentification** | Oui (user/pass) | Non |
| **Ports** | 20, 21 | 69 |
| **Fiabilité** | Oui (TCP) | Basique (simple ACK) |
| **Complexité** | Élevée | Faible |
| **Usage** | Transfert de fichiers général | Boot réseau, config équipements |

---

## 7. SMB (Server Message Block)

### Fonction de SMB

SMB est un protocole de **partage de fichiers et d'imprimantes** :
- **Port** : 445 (TCP) - SMBv2/v3 direct, 139 (NetBIOS over TCP)
- **Fonction** : Partage de ressources (fichiers, imprimantes) sur réseau local
- **Système** : Principalement Windows, mais aussi Linux (Samba), macOS

### Versions de SMB

| Version | Année | Caractéristiques |
|---------|-------|------------------|
| **SMB 1.0** | 1983 | Version originale, **vulnérable** (WannaCry, EternalBlue) |
| **SMB 2.0** | 2006 | Windows Vista/2008, amélioration performance |
| **SMB 2.1** | 2010 | Windows 7/2008 R2 |
| **SMB 3.0** | 2012 | Windows 8/2012, chiffrement, multichannel |
| **SMB 3.1.1** | 2015 | Windows 10/2016, chiffrement AES-128-GCM |

**Important** : SMB 1.0 doit être **désactivé** (vulnérabilités critiques).

### Utilisation de SMB

**Partage de fichiers Windows :**
```
\\192.168.1.10\PartageDocuments
\\SERVEUR\Partage
```

**Samba (Linux)** :
- Implémentation open-source de SMB
- Permet l'interopérabilité Linux/Windows

---

## 8. Autres protocoles applicatifs

### 8.1 Telnet

**Telnet** : Accès distant en ligne de commande
- **Port** : 23 (TCP)
- **Fonction** : Shell distant, administration
- **Sécurité** : ❌ **Non chiffré** (mot de passe en clair)
- **Remplacement** : SSH (sécurisé)

### 8.2 SSH (Secure Shell)

**SSH** : Accès distant sécurisé
- **Port** : 22 (TCP)
- **Fonction** : Shell distant, SFTP, tunneling
- **Sécurité** : ✅ **Chiffré** (authentification + confidentialité)
- **Clés** : Authentification par clé publique/privée
- **Usage** : Administration serveurs Linux, switches/routeurs Cisco

### 8.3 SNMP (Simple Network Management Protocol)

**SNMP** : Gestion et surveillance réseau
- **Ports** : 161 (requêtes), 162 (traps) - **UDP**
- **Fonction** : Monitoring équipements réseau (routeurs, switches, serveurs)
- **Versions** : SNMPv1, SNMPv2c, **SNMPv3** (sécurisé)
- **MIB** : Management Information Base (base de données des objets gérés)

### 8.4 NTP (Network Time Protocol)

**NTP** : Synchronisation de l'horloge
- **Port** : 123 (UDP)
- **Fonction** : Synchroniser l'horloge système avec une référence
- **Précision** : Jusqu'à quelques millisecondes
- **Hiérarchie** : Stratum 0 (horloge atomique) → Stratum 1 → Stratum 2, etc.

### 8.5 Syslog

**Syslog** : Collecte de logs
- **Port** : 514 (UDP)
- **Fonction** : Centraliser les logs systèmes et équipements réseau
- **Niveaux** : Emergency (0), Alert (1), Critical (2), Error (3), Warning (4), Notice (5), Info (6), Debug (7)

### 8.6 RDP (Remote Desktop Protocol)

**RDP** : Bureau à distance Windows
- **Port** : 3389 (TCP)
- **Fonction** : Accès graphique à distance (Windows)
- **Sécurité** : Chiffrement, authentification NLA (Network Level Authentication)

---

## 9. Ports récapitulatifs

### Ports TCP

| Port | Protocole | Service |
|------|-----------|---------|
| 20 | FTP Data | Transfert de données FTP |
| 21 | FTP Control | Contrôle FTP |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Accès distant non sécurisé |
| 25 | SMTP | Envoi d'emails |
| 53 | DNS | Transferts de zones DNS |
| 80 | HTTP | Web non sécurisé |
| 110 | POP3 | Réception d'emails |
| 143 | IMAP | Gestion d'emails |
| 443 | HTTPS | Web sécurisé |
| 445 | SMB | Partage de fichiers/imprimantes |
| 587 | SMTP (Submission) | Envoi d'emails avec TLS |
| 993 | IMAPS | IMAP sécurisé |
| 995 | POP3S | POP3 sécurisé |
| 3389 | RDP | Bureau à distance Windows |

### Ports UDP

| Port | Protocole | Service |
|------|-----------|---------|
| 53 | DNS | Requêtes DNS |
| 67 | DHCP Server | Serveur DHCP |
| 68 | DHCP Client | Client DHCP |
| 69 | TFTP | Transfert de fichiers simple |
| 123 | NTP | Synchronisation horloge |
| 161 | SNMP | Requêtes SNMP |
| 162 | SNMP Trap | Notifications SNMP |
| 514 | Syslog | Logs système |

---

## 10. Modèle OSI - Encapsulation

### Encapsulation des données

```
Application (7)  → Données (HTTP, DNS, etc.)
Présentation (6) → (Intégré dans Application)
Session (5)      → (Intégré dans Application)
Transport (4)    → Segment (TCP) / Datagramme (UDP)
Réseau (3)       → Paquet (IP)
Liaison (2)      → Trame (Ethernet)
Physique (1)     → Bits (signaux électriques/optiques)
```

### Processus d'envoi

1. **Application** : Génère les données (ex: requête HTTP)
2. **Transport** : Ajoute en-tête TCP/UDP (ports source/destination)
3. **Réseau** : Ajoute en-tête IP (adresses IP source/destination)
4. **Liaison** : Ajoute en-tête Ethernet (adresses MAC source/destination)
5. **Physique** : Conversion en signaux électriques/optiques

### Processus de réception

1. **Physique** : Reçoit les signaux et les convertit en bits
2. **Liaison** : Lit l'en-tête Ethernet, vérifie MAC destination
3. **Réseau** : Lit l'en-tête IP, vérifie IP destination
4. **Transport** : Lit l'en-tête TCP/UDP, démultiplexe vers l'application (port)
5. **Application** : Traite les données (ex: affiche la page web)

---

## 11. Points clés pour l'examen CCNA

### HTTP/HTTPS

✅ **HTTP** : Port 80 (TCP), protocole du web, sans état
✅ **HTTPS** : Port 443 (TCP), HTTP chiffré avec SSL/TLS
✅ **Méthodes** : GET, POST, PUT, DELETE
✅ **Codes** : 200 (OK), 404 (Not Found), 500 (Server Error)

### DNS

✅ **Fonction** : Nom de domaine → Adresse IP
✅ **Port** : 53 (UDP pour requêtes, TCP pour transferts de zones)
✅ **Hiérarchie** : Root (.) → TLD (.com) → Second-Level (google.com) → Subdomain (www)
✅ **Types** : A (IPv4), AAAA (IPv6), CNAME (alias), MX (email), NS (serveur DNS)
✅ **Cache** : TTL (Time To Live) pour durée de validité

### DHCP

✅ **Fonction** : Allocation automatique d'adresses IP
✅ **Ports** : 67 (serveur), 68 (client) - UDP
✅ **Processus DORA** : Discover → Offer → Request → Acknowledge
✅ **Informations** : IP, masque, passerelle, DNS, durée du bail
✅ **Relay Agent** : ip helper-address pour traverser les routeurs

### Email

✅ **SMTP** : Port 25 (envoi), 587 (submission avec TLS) - TCP
✅ **POP3** : Port 110 (réception), téléchargement local, un seul appareil
✅ **IMAP** : Port 143 (gestion), synchronisation serveur, multi-appareils

### Autres protocoles

✅ **SMB** : Port 445, partage de fichiers/imprimantes Windows
✅ **FTP** : Ports 20-21 (TCP), transfert de fichiers avec authentification
✅ **TFTP** : Port 69 (UDP), transfert simple sans authentification
✅ **SSH** : Port 22 (TCP), accès distant sécurisé (remplace Telnet)
✅ **Telnet** : Port 23 (TCP), accès distant **non sécurisé** (obsolète)

---

## 12. Scénarios pratiques

### Scénario 1 : Résolution DNS

**Question :** Un utilisateur tape www.cisco.com dans son navigateur. Décrivez le processus.

**Réponse :**
1. Le navigateur vérifie son **cache DNS**
2. Si absent, le système vérifie le **cache OS**
3. Si absent, requête au **résolveur DNS** (ex: 8.8.8.8)
4. Le résolveur interroge les serveurs DNS :
   - Root server → serveur .com → serveur cisco.com
5. Le résolveur reçoit l'**adresse IP** (ex: 72.163.4.185)
6. Le résolveur retourne l'IP au client et la met en **cache** (TTL)
7. Le navigateur se connecte à 72.163.4.185:443 (HTTPS)

### Scénario 2 : DHCP sur plusieurs sous-réseaux

**Question :** Un serveur DHCP est sur le réseau 10.1.1.0/24. Un client sur 10.1.2.0/24 veut obtenir une IP. Comment faire ?

**Réponse :**
1. Le client envoie un **DHCP DISCOVER** en broadcast (255.255.255.255)
2. Le **routeur** reçoit le broadcast
3. Le routeur a un **ip helper-address 10.1.1.10** configuré
4. Le routeur convertit le broadcast en **unicast** et l'envoie au serveur DHCP (10.1.1.10)
5. Le serveur DHCP répond au routeur
6. Le routeur **relaye la réponse** au client (10.1.2.x)
7. Le client obtient son IP via le processus DORA complet

### Scénario 3 : Choix POP3 vs IMAP

**Question :** Quand utiliser POP3 ou IMAP ?

**Réponse :**

| Scénario | Protocole | Justification |
|----------|-----------|---------------|
| Utilisateur avec 1 seul PC | **POP3** | Simple, stockage local |
| Utilisateur avec PC + smartphone + tablette | **IMAP** | Synchronisation multi-appareils |
| Espace serveur limité | **POP3** | Emails supprimés du serveur |
| Besoin de lire emails hors ligne | **POP3** | Stockage local complet |
| Besoin d'organiser emails en dossiers | **IMAP** | Gestion avancée |

---

## 13. Résumé

### Protocoles Web

- **HTTP** : Port 80, web non sécurisé, méthodes GET/POST/PUT/DELETE
- **HTTPS** : Port 443, HTTP chiffré avec TLS, certificats SSL

### DNS

- **Fonction** : Nom → IP (www.google.com → 142.250.185.78)
- **Port** : 53 (UDP requêtes, TCP transferts)
- **Hiérarchie** : Root → TLD → Second-Level → Subdomain
- **Types** : A (IPv4), AAAA (IPv6), CNAME, MX, NS, PTR

### DHCP

- **Fonction** : Allocation automatique IP + masque + passerelle + DNS
- **Ports** : 67 (serveur), 68 (client) - UDP
- **DORA** : Discover → Offer → Request → Acknowledge
- **Relay** : ip helper-address pour traverser routeurs

### Email

- **SMTP** : Envoi d'emails, port 25/587, serveur à serveur
- **POP3** : Réception, port 110, téléchargement local
- **IMAP** : Gestion, port 143, synchronisation serveur

### Autres

- **SMB** : Partage fichiers/imprimantes, port 445
- **FTP** : Transfert fichiers, ports 20-21 (TCP)
- **TFTP** : Transfert simple, port 69 (UDP)
- **SSH** : Accès distant sécurisé, port 22
- **Telnet** : Accès distant non sécurisé (obsolète), port 23

---

**Fin du Module 15 - Protocoles de la couche Application**
