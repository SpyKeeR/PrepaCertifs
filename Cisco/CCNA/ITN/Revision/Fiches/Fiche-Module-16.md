# Fiche Module 16 : Principes fondamentaux de la sécurité du réseau
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Triangle CIA de la sécurité
- **C**onfidentialité : Seuls les autorisés accèdent aux données
- **I**ntégrité : Les données ne sont pas altérées
- **D**isponibilité (Availability) : Les services sont accessibles quand nécessaire

### Types de menaces
- **Internes** : Employés, erreurs humaines, négligence
- **Externes** : Hackers, organisations criminelles, hacktivistes, États

---

## 🎯 Attaques réseau principales

| Type | Description | Exemples |
|------|-------------|----------|
| **Reconnaissance** | Collecte d'informations | Port scanning, packet sniffing, footprinting |
| **Accès** | Vol/exploitation de credentials | Phishing, brute force, MitM, spoofing |
| **DoS/DDoS** | Rendre service indisponible | SYN flood, ping of death, UDP flood |
| **Données** | Interception/modification/vol | Sniffing, SQL injection, session hijacking |

---

## 🛡️ Défense en profondeur (6 couches)

| Couche | Protection | Exemples |
|--------|-----------|----------|
| **1. Physique** | Accès aux locaux | Vidéo surveillance, badges, salles sécurisées |
| **2. Périmétrique** | Frontière réseau | Firewalls, IDS/IPS, VPN |
| **3. Réseau** | Segmentation | VLANs, ACL, 802.1X, WPA3 |
| **4. Équipements** | Sécurité devices | Mots de passe, SSH, AAA, désactivation services |
| **5. Applicative** | Sécurité apps | Pare-feu applicatifs, chiffrement, validation |
| **6. Données** | Protection data | Chiffrement au repos, backups, classification |

---

## 🔐 Configuration sécurité Cisco - Essentiel

### Mots de passe

```cisco
! Enable secret (MD5)
enable secret Str0ng@P@ss!

! Chiffrer tous les mots de passe en clair
service password-encryption

! Console
line console 0
 password Cons0le@P@ss
 login
 exec-timeout 5 0

! VTY avec utilisateur local
username admin privilege 15 secret Admin@P@ss!
line vty 0 4
 login local
 exec-timeout 10 0
```

### SSH (Secure Shell)

```cisco
! 1. Hostname + domaine (requis)
hostname R1
ip domain-name company.local

! 2. Générer clé RSA (min 1024, recommandé 2048)
crypto key generate rsa modulus 2048

! 3. SSHv2 uniquement
ip ssh version 2

! 4. VTY SSH only
line vty 0 4
 transport input ssh
 login local
```

**Commandes de vérification :**
```cisco
show ip ssh
show ssh
```

### Bannières

```cisco
! MOTD - avant login (légal, pas "Welcome")
banner motd #Accès autorisé uniquement#

! Login - pendant authentification
banner login #Entrez vos identifiants#

! Exec - après authentification
banner exec #Bienvenue sur R1#
```

### Désactiver services inutiles

```cisco
! HTTP/HTTPS
no ip http server
no ip http secure-server

! CDP (sur interfaces externes ou globalement)
no cdp run

! Small servers
no service tcp-small-servers
no service udp-small-servers
```

### Logging

```cisco
! Timestamps
service timestamps log datetime msec

! Niveaux de log
logging console warnings
logging buffered 16384 informational

! Serveur Syslog externe
logging host 192.168.1.100
logging trap informational
```

---

## 📊 Technologies de sécurité

| Technologie | Fonction | Types |
|-------------|----------|-------|
| **Firewall** | Filtrage du trafic | Stateless, Stateful, Applicatif, NGFW |
| **IDS** | Détection d'intrusion | Alerte seulement |
| **IPS** | Prévention d'intrusion | Détection + Blocage |
| **VPN** | Tunnel sécurisé | IPsec, SSL/TLS |
| **Antivirus** | Protection malware | Signatures, comportemental, sandbox |

---

## 🔑 AAA (Authentication, Authorization, Accounting)

| Composante | Question | Fonction |
|------------|----------|----------|
| **Authentication** | Qui êtes-vous ? | Vérification identité (local, RADIUS, TACACS+) |
| **Authorization** | Que pouvez-vous faire ? | Permissions et privilèges |
| **Accounting** | Qu'avez-vous fait ? | Journalisation, audit, traçabilité |

**Configuration AAA basique :**
```cisco
! Activer AAA
aaa new-model

! Authentification locale
aaa authentication login default local

! Liste personnalisée
aaa authentication login SSH-LOGIN local
line vty 0 4
 login authentication SSH-LOGIN
```

---

## 🚨 Niveaux de logging Syslog

| Niveau | Nom | Usage |
|--------|-----|-------|
| **0** | Emergency | Système inutilisable |
| **1** | Alert | Action immédiate requise |
| **2** | Critical | Condition critique |
| **3** | Error | Erreurs |
| **4** | Warning | Avertissements |
| **5** | Notice | Normal mais significatif |
| **6** | Informational | Informations générales |
| **7** | Debugging | Debug détaillé (éviter en prod) |

---

## 💡 À retenir absolument

✅ **SSH vs Telnet**
- Telnet = non chiffré, obsolète, dangereux ❌
- SSH = chiffré, authentification forte, sécurisé ✅

✅ **Mots de passe Cisco**
- `enable password` = Type 7 (faiblement chiffré) ❌
- `enable secret` = MD5 (plus fort) ✅
- `service password-encryption` = chiffre Type 7

✅ **SSH Requirements (3 éléments)**
1. Hostname configuré
2. Nom de domaine configuré
3. Clé RSA générée (min 1024 bits)

✅ **Timeout**
- `exec-timeout <min> <sec>` sur console et VTY
- Valeur 0 0 = désactivé (dangereux en production)

✅ **Commandes show essentielles**
- `show ip ssh` : Configuration SSH
- `show ssh` : Connexions SSH actives
- `show users` : Utilisateurs connectés
- `show running-config` : Config actuelle
- `show logging` : Logs système

✅ **Principe du moindre privilège**
Donner uniquement les accès nécessaires, pas plus

✅ **Défense en profondeur**
Sécurité multicouche, jamais un seul point de protection

✅ **DoS vs DDoS**
- DoS = une source
- DDoS = plusieurs sources (botnet), plus difficile à bloquer

✅ **Triangle CIA**
Fondement de la sécurité informatique : Confidentiality, Integrity, Availability

---

## 🔍 Checklist sécurisation rapide

**Configuration minimale :**
- [ ] Hostname et domaine configurés
- [ ] `enable secret` défini (pas `enable password`)
- [ ] `service password-encryption` activé
- [ ] SSH configuré (clé RSA 2048 bits)
- [ ] Telnet désactivé sur VTY (`transport input ssh`)
- [ ] Utilisateurs locaux créés
- [ ] Timeouts configurés (console 5 min, VTY 10 min)
- [ ] Bannière MOTD sans "Welcome"
- [ ] Services inutiles désactivés (HTTP, CDP)
- [ ] Logging activé avec timestamps
- [ ] Configuration sauvegardée

**Vérifications :**
- [ ] Tester connexion SSH
- [ ] Vérifier impossibilité Telnet
- [ ] Confirmer timeout fonctionnel
- [ ] Vérifier bannière affichée
- [ ] Consulter logs

---

## 📝 Différences clés

| Aspect | Non sécurisé ❌ | Sécurisé ✅ |
|--------|----------------|------------|
| **Accès distant** | Telnet (clair) | SSH (chiffré) |
| **Enable** | enable password | enable secret |
| **Authentification** | Mot de passe unique | Utilisateurs individuels |
| **Timeout** | Désactivé (0 0) | Activé (5-10 min) |
| **Services** | Tous actifs | Seulement nécessaires |
| **Logging** | Désactivé | Activé avec timestamps |
| **CDP** | Actif partout | Désactivé externe |

---

**Commandes de vérification rapides :**
```cisco
show ip ssh                    ! Config SSH
show ssh                        ! Sessions SSH
show users                      ! Utilisateurs connectés
show running-config | include enable
show running-config | section line
show logging
```
