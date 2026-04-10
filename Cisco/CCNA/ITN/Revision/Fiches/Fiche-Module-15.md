# Fiche Module 15 - Protocoles de la couche Application

**Date :** 27 février 2026  
**Cours :** CCNA ITN  
**Sujet :** Protocoles de la couche Application (Layer 7)

---

## 🎯 Concepts clés

**Rôle de la couche Application :**
- Interface utilisateur avec le réseau
- Services réseau (web, email, DNS, fichiers)
- Format et règles de communication

**Modèles :**
- **Client-Serveur** : Client demande, serveur répond (HTTP, DNS, SMTP)
- **Peer-to-Peer (P2P)** : Chaque nœud = client + serveur (BitTorrent)

---

## 📋 Tableaux récapitulatifs

### HTTP/HTTPS

| Protocole | Port | Transport | Sécurité | Usage |
|-----------|------|-----------|----------|-------|
| **HTTP** | 80 | TCP | Non chiffré | Web (pages HTML, CSS, JS, images) |
| **HTTPS** | 443 | TCP | Chiffré TLS | Web sécurisé (certificat SSL/TLS) |

**Méthodes HTTP :**

| Méthode | Rôle |
|---------|------|
| **GET** | Récupérer une ressource |
| **POST** | Envoyer des données (formulaires) |
| **PUT** | Créer/remplacer une ressource |
| **DELETE** | Supprimer une ressource |

**Codes de statut HTTP :**

| Code | Signification |
|------|---------------|
| **200 OK** | Succès |
| **301 Moved Permanently** | Redirection permanente |
| **400 Bad Request** | Requête mal formée |
| **401 Unauthorized** | Authentification requise |
| **403 Forbidden** | Accès interdit |
| **404 Not Found** | Ressource introuvable |
| **500 Internal Server Error** | Erreur serveur |
| **503 Service Unavailable** | Serveur surchargé |

**TLS (Transport Layer Security) :**
- TLS 1.2 et 1.3 recommandés (SSL obsolète)
- Certificat émis par CA (Certificate Authority)
- Confidentialité + Intégrité + Authentification

---

### DNS (Domain Name System)

**Fonction :** Nom de domaine → Adresse IP

| Paramètre | Valeur |
|-----------|--------|
| **Port** | 53 (UDP requêtes, TCP transferts zones) |
| **Transport** | UDP (< 512 octets), TCP (> 512 octets) |
| **Exemple** | www.google.com → 142.250.185.78 |

**Hiérarchie DNS :**
```
. (root)
  |
  ├─ .com (TLD)
  │   ├─ google.com (Second-Level)
  │   │   └─ www.google.com (Subdomain)
  │   └─ cisco.com
  └─ .fr
```

**Types d'enregistrements DNS :**

| Type | Rôle | Exemple |
|------|------|---------|
| **A** | IPv4 | www.example.com → 93.184.216.34 |
| **AAAA** | IPv6 | www.example.com → 2606:2800:220:1:... |
| **CNAME** | Alias | blog.example.com → www.example.com |
| **MX** | Serveur email | example.com → mail.example.com |
| **NS** | Serveur DNS autoritaire | example.com → ns1.example.com |
| **PTR** | Résolution inverse | 93.184.216.34 → www.example.com |
| **TXT** | Texte (SPF, DKIM) | Vérifications, configurations |

**Cache DNS :**
- TTL (Time To Live) : durée de validité en secondes
- Cache résolveur, OS, navigateur

**Serveurs DNS publics :**
- Google : 8.8.8.8, 8.8.4.4
- Cloudflare : 1.1.1.1, 1.0.0.1
- Quad9 : 9.9.9.9

**Commandes DNS :**
```powershell
# Windows
nslookup www.google.com
ipconfig /displaydns    # Afficher cache
ipconfig /flushdns      # Vider cache

# Linux
dig www.google.com
host www.google.com
```

---

### DHCP (Dynamic Host Configuration Protocol)

**Fonction :** Allocation automatique IP + masque + passerelle + DNS

| Paramètre | Valeur |
|-----------|--------|
| **Ports** | 67 (serveur), 68 (client) |
| **Transport** | **UDP** |
| **Broadcast** | 255.255.255.255 |

**Processus DHCP : DORA**

```
Client                        Serveur DHCP
  |                               |
  | 1. DISCOVER (broadcast)       |
  |------------------------------>|
  | "Y a-t-il un serveur DHCP ?"  |
  |                               |
  | 2. OFFER (proposition IP)     |
  |<------------------------------|
  | "Voici IP: 192.168.1.100"     |
  |                               |
  | 3. REQUEST (broadcast)        |
  |------------------------------>|
  | "J'accepte l'IP 192.168.1.100"|
  |                               |
  | 4. ACK (confirmation)         |
  |<------------------------------|
  | "IP attribuée"                |
```

**Étapes détaillées :**
1. **D**iscover : Client → Broadcast (0.0.0.0 → 255.255.255.255)
2. **O**ffer : Serveur → Client (proposition IP + config)
3. **R**equest : Client → Broadcast (acceptation)
4. **A**cknowledge : Serveur → Client (confirmation)

**Informations fournies par DHCP :**

| Information | Option | Exemple |
|-------------|--------|---------|
| **Adresse IP** | Yiaddr | 192.168.1.100 |
| **Masque** | Option 1 | 255.255.255.0 |
| **Passerelle** | Option 3 | 192.168.1.1 |
| **DNS** | Option 6 | 8.8.8.8, 8.8.4.4 |
| **Bail (Lease)** | Option 51 | 86400 sec (24h) |

**Renouvellement du bail :**
- **T1 (50%)** : Renouvellement auprès du serveur DHCP
- **T2 (87.5%)** : Broadcast si T1 échoue
- **Expiration** : Perte IP, recommence DORA

**DHCP Relay Agent :**
- Convertit broadcast en unicast pour traverser routeurs
- Configuration Cisco : `ip helper-address 10.1.1.10`

**Commandes DHCP :**
```powershell
# Windows
ipconfig /all        # Afficher config
ipconfig /release    # Libérer IP
ipconfig /renew      # Renouveler IP

# Linux
sudo dhclient -r eth0   # Release
sudo dhclient eth0      # Renew
```

---

### Email (SMTP, POP, IMAP)

**Architecture :**
```
Expéditeur → SMTP (587) → Serveur SMTP
                              ↓ SMTP (25)
                         Serveur SMTP
                              ↓ POP/IMAP
                         Destinataire
```

#### SMTP (Simple Mail Transfer Protocol)

**Envoi d'emails**

| Paramètre | Valeur |
|-----------|--------|
| **Ports** | 25 (serveur-serveur), 587 (client-serveur + TLS) |
| **Transport** | TCP |
| **Fonction** | Relayer emails |

**Commandes SMTP :** HELO, MAIL FROM, RCPT TO, DATA, QUIT

#### POP3 vs IMAP

| Critère | POP3 | IMAP |
|---------|------|------|
| **Ports** | 110 (POP3), 995 (POP3S) | 143 (IMAP), 993 (IMAPS) |
| **Transport** | TCP | TCP |
| **Stockage** | Téléchargement local | Synchronisation serveur |
| **Multi-appareils** | Non (un seul appareil) | Oui (synchronisation) |
| **Gestion** | Limitée | Dossiers, recherche, flags |
| **Usage** | Email local, connexion unique | Multi-appareils, accès web |

---

### Autres protocoles importants

#### SMB (Server Message Block)

| Paramètre | Valeur |
|-----------|--------|
| **Port** | 445 (TCP) |
| **Fonction** | Partage fichiers/imprimantes Windows |
| **Versions** | SMB 1.0 (vulnérable, désactiver) / SMB 3.0+ (recommandé) |

#### FTP / TFTP

| Protocole | Ports | Transport | Sécurité | Usage |
|-----------|-------|-----------|----------|-------|
| **FTP** | 20-21 | TCP | Authentification | Transfert fichiers fiable |
| **TFTP** | 69 | UDP | Aucune | Transfert simple (boot PXE) |

#### SSH / Telnet

| Protocole | Port | Transport | Sécurité | Usage |
|-----------|------|-----------|----------|-------|
| **SSH** | 22 | TCP | Chiffré | Administration sécurisée |
| **Telnet** | 23 | TCP | Non chiffré | Administration (obsolète) |

---

## 💡 Points examen

**HTTP/HTTPS :**
- ✅ HTTP : Port 80 (TCP), non sécurisé
- ✅ HTTPS : Port 443 (TCP), chiffré TLS
- ✅ Méthodes : GET (récupérer), POST (envoyer), PUT (créer/remplacer), DELETE (supprimer)
- ✅ Codes : 200 OK, 404 Not Found, 500 Server Error

**DNS :**
- ✅ Port 53 (UDP requêtes, TCP transferts zones)
- ✅ Hiérarchie : Root (.) → TLD (.com) → Second-Level (google.com) → Subdomain (www)
- ✅ A (IPv4), AAAA (IPv6), CNAME (alias), MX (email), NS (serveur DNS), PTR (résolution inverse)
- ✅ Cache : TTL (Time To Live)
- ✅ Commandes : nslookup, dig, ipconfig /flushdns

**DHCP :**
- ✅ Ports 67 (serveur), 68 (client) - **UDP**
- ✅ **DORA** : Discover → Offer → Request → Acknowledge
- ✅ Broadcast : 255.255.255.255
- ✅ Infos : IP, masque, passerelle (Option 3), DNS (Option 6), Lease (Option 51)
- ✅ Relay Agent : ip helper-address
- ✅ Renouvellement : T1 (50%), T2 (87.5%), Expiration (100%)

**Email :**
- ✅ SMTP : Envoi (ports 25, 587)
- ✅ POP3 : Réception locale (ports 110, 995) - un seul appareil
- ✅ IMAP : Synchronisation serveur (ports 143, 993) - multi-appareils

**Autres :**
- ✅ SMB : Port 445 (TCP), partage Windows
- ✅ FTP : Ports 20-21 (TCP), transfert fiable
- ✅ TFTP : Port 69 (UDP), transfert simple
- ✅ SSH : Port 22 (TCP), chiffré
- ✅ Telnet : Port 23 (TCP), non chiffré (obsolète)

---

## 🔢 Tableau récapitulatif des ports

### TCP

| Port | Service | Description |
|------|---------|-------------|
| 20-21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Telnet (obsolète) |
| 25 | SMTP | Email (serveur-serveur) |
| 80 | HTTP | Web non sécurisé |
| 110 | POP3 | Email (réception) |
| 143 | IMAP | Email (synchronisation) |
| 443 | HTTPS | Web sécurisé (TLS) |
| 445 | SMB | Partage Windows |
| 587 | SMTP+TLS | Email (client-serveur) |
| 993 | IMAPS | IMAP sécurisé |
| 995 | POP3S | POP3 sécurisé |
| 3389 | RDP | Remote Desktop |

### UDP

| Port | Service | Description |
|------|---------|-------------|
| 53 | DNS | Domain Name System |
| 67-68 | DHCP | Dynamic Host Configuration |
| 69 | TFTP | Trivial FTP |
| 123 | NTP | Network Time Protocol |
| 161-162 | SNMP | Network Management |
| 514 | Syslog | Logs système |

---

## ⚡ Révision rapide

1. **HTTP** (80 TCP) vs **HTTPS** (443 TCP chiffré TLS) | Codes : 200 OK, 404 Not Found, 500 Error
2. **DNS** (53 UDP/TCP) : A (IPv4), AAAA (IPv6), CNAME (alias), MX (email), PTR (inverse) | Cache TTL
3. **DHCP** (67-68 UDP) : **DORA** (Discover → Offer → Request → Ack) | Infos : IP, masque, passerelle (Opt 3), DNS (Opt 6)
4. **Email** : SMTP (25/587 envoi) | POP3 (110 local) vs IMAP (143 sync multi-appareils)
5. **Autres** : SMB (445 Windows) | FTP (20-21 TCP) | TFTP (69 UDP) | SSH (22 chiffré) | Telnet (23 obsolète)
