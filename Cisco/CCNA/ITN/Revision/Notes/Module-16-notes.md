# Module 16 : Principes fondamentaux de la sécurité du réseau
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module présente les principes fondamentaux de la sécurité réseau, les menaces courantes, et les techniques pour sécuriser les équipements Cisco.

**Durée estimée :** 4-5 heures  
**Objectifs :** Comprendre les menaces réseau et implémenter les mesures de sécurité de base

---

## 16.1 Menaces et failles de sécurité

### Types de menaces

**Menaces internes**
- Employés malveillants ou négligents
- Accès non autorisé aux données
- Vol ou perte d'équipements
- Erreurs humaines (mauvaise configuration)

**Menaces externes**
- Hackers amateurs (script kiddies)
- Hackers professionnels (black hat)
- Hackers éthiques (white hat)
- Organisations criminelles
- Hacktivistes
- Attaques parrainées par des États

### Vulnérabilités courantes

**Vulnérabilités technologiques**
- Faiblesses des systèmes d'exploitation
- Bugs logiciels non corrigés
- Équipements réseau mal configurés
- Protocoles de sécurité faibles
- Absence de chiffrement

**Vulnérabilités de configuration**
- Comptes avec mots de passe par défaut
- Services inutiles activés
- Ports ouverts non nécessaires
- Absence de pare-feu
- Logs désactivés

**Vulnérabilités de politique**
- Absence de politique de sécurité
- Formation insuffisante du personnel
- Absence de plan de continuité
- Contrôles d'accès inadéquats

---

## 16.2 Attaques de réseau

### Reconnaissance

**Objectif :** Collecter des informations sur la cible

**Techniques :**
- **Balayage de ports (port scanning)** : Identifier les ports ouverts
- **Analyse de paquets (packet sniffing)** : Capturer le trafic réseau
- **Recherche d'informations (footprinting)** : Collecte via sources publiques
- **Ingénierie sociale** : Manipulation psychologique

**Outils :**
- Nmap (scanner de ports)
- Wireshark (analyseur de protocoles)
- Google Hacking (recherche avancée)

### Attaques d'accès

**Vol d'informations d'identification**
- Attaques par dictionnaire
- Attaques par force brute
- Hameçonnage (phishing)
- Keyloggers

**Exploitation de confiance**
- Usurpation d'identité (spoofing)
- Man-in-the-middle (MITM)
- ARP poisoning

**Élévation de privilèges**
- Exploitation de vulnérabilités
- Buffer overflow
- Exploitation de configuration faible

### Attaques par déni de service (DoS)

**Objectif :** Rendre un service indisponible

**Types d'attaques DoS :**

**1. DoS simple**
- Saturation de bande passante
- Épuisement des ressources système
- Provoqué par une seule source

**2. DDoS (Distributed DoS)**
- Attaque coordonnée depuis plusieurs sources
- Utilisation de botnets (réseaux de machines compromises)
- Difficile à bloquer

**Techniques courantes :**
- **SYN Flood** : Saturation avec des requêtes TCP SYN
- **Ping of Death** : Envoi de paquets ICMP malformés
- **Smurf Attack** : Amplification via broadcast ICMP
- **UDP Flood** : Saturation avec des paquets UDP

### Attaques sur les données

**Interception de données**
- Sniffing de mots de passe
- Capture de données sensibles
- Session hijacking

**Modification de données**
- Altération de fichiers
- Injection SQL
- Modification de paquets en transit

**Vol de données**
- Exfiltration d'informations
- Vol de propriété intellectuelle
- Violation de données personnelles

---

## 16.3 Atténuation des attaques du réseau

### Défense en profondeur

Approche multicouche de la sécurité :

**Couche 1 : Sécurité physique**
- Contrôle d'accès aux locaux
- Surveillance vidéo
- Serveurs sécurisés en salle dédiée

**Couche 2 : Sécurité périmétrique**
- Pare-feu (firewalls)
- Systèmes de détection d'intrusion (IDS)
- Systèmes de prévention d'intrusion (IPS)
- VPN pour accès distant

**Couche 3 : Sécurité réseau**
- Segmentation réseau (VLANs)
- ACL (Access Control Lists)
- Authentification 802.1X
- Sécurité sans fil (WPA3)

**Couche 4 : Sécurité des équipements**
- Mots de passe robustes
- SSH plutôt que Telnet
- AAA (Authentication, Authorization, Accounting)
- Désactivation des services inutiles

**Couche 5 : Sécurité applicative**
- Pare-feu applicatifs
- Chiffrement des données
- Validation des entrées
- Mises à jour régulières

**Couche 6 : Sécurité des données**
- Chiffrement au repos
- Sauvegardes régulières
- Contrôle d'accès aux fichiers
- Classification des données

### Technologies de sécurité

**Pare-feu (Firewalls)**
- Filtrage de paquets (stateless)
- Inspection avec état (stateful)
- Pare-feu applicatifs
- Next-Generation Firewalls (NGFW)

**Systèmes de détection/prévention**
- **IDS** : Détecte et alerte
- **IPS** : Détecte et bloque
- Signatures d'attaques
- Analyse comportementale

**VPN (Virtual Private Network)**
- Chiffrement des communications
- Tunneling sécurisé
- Accès distant sécurisé
- IPsec ou SSL/TLS

**Antivirus et antimalware**
- Protection endpoint
- Analyse en temps réel
- Mises à jour de signatures
- Sandbox pour fichiers suspects

---

## 16.4 Sécurité des périphériques

### Sécurisation des mots de passe

**Bonnes pratiques :**
- Longueur minimale de 8 caractères (recommandé 12+)
- Combinaison majuscules, minuscules, chiffres, symboles
- Changement régulier
- Unicité (pas de réutilisation)
- Pas de mots du dictionnaire

**Configuration sur équipements Cisco :**

```cisco
! Mot de passe enable secret (chiffré avec MD5)
Router(config)# enable secret Cisco@2026!

! Chiffrement de tous les mots de passe en clair
Router(config)# service password-encryption

! Mot de passe console
Router(config)# line console 0
Router(config-line)# password Cons0le@Pass
Router(config-line)# login

! Mot de passe VTY (Telnet/SSH)
Router(config)# line vty 0 4
Router(config-line)# password VTY@SecureP@ss
Router(config-line)# login
```

### Configuration SSH (Secure Shell)

**SSH vs Telnet :**
- **Telnet** : Non chiffré, obsolète, dangereux
- **SSH** : Chiffré, authentification forte, sécurisé

**Configuration SSH sur routeur/switch Cisco :**

```cisco
! 1. Configurer hostname (requis pour SSH)
Router(config)# hostname R1

! 2. Configurer nom de domaine (requis pour clé RSA)
R1(config)# ip domain-name example.com

! 3. Générer clé RSA (minimum 1024 bits)
R1(config)# crypto key generate rsa modulus 2048

! 4. Créer utilisateur local
R1(config)# username admin privilege 15 secret Admin@2026!

! 5. Configurer lignes VTY pour SSH uniquement
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local

! 6. Définir version SSHv2 (plus sécurisé que v1)
R1(config)# ip ssh version 2

! 7. Optionnel : Timeout de connexion
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 3
```

**Vérification :**
```cisco
R1# show ip ssh
R1# show ssh
```

### Bannières de sécurité

**Types de bannières :**

```cisco
! Message of the Day (MOTD) - affiché avant le login
Router(config)# banner motd #
**************************************************
*  ACCES AUTORISE UNIQUEMENT                     *
*  Toute connexion non autorisée sera poursuivie *
*  Les connexions sont surveillées et loggées    *
**************************************************
#

! Bannière login - affichée avant l'authentification
Router(config)# banner login #
Entrez vos identifiants pour accéder au système
#

! Bannière exec - affichée après authentification réussie
Router(config)# banner exec #
Bienvenue sur R1 - Accès autorisé
#
```

**⚠️ Attention :** Éviter les termes "Bienvenue" ou "Welcome" dans MOTD (implication légale)

### Désactivation des services inutilisés

**Services à désactiver pour la sécurité :**

```cisco
! Désactiver serveur HTTP (interface web)
Router(config)# no ip http server
Router(config)# no ip http secure-server

! Désactiver CDP sur interfaces externes
Router(config)# interface g0/0
Router(config-if)# no cdp enable

! Désactiver CDP globalement
Router(config)# no cdp run

! Désactiver finger service
Router(config)# no service finger

! Désactiver small servers (echo, discard, etc.)
Router(config)# no service tcp-small-servers
Router(config)# no service udp-small-servers
```

### AAA (Authentication, Authorization, Accounting)

**Composantes :**

**1. Authentication (Authentification)**
- Vérification de l'identité
- "Qui êtes-vous ?"
- Méthodes : local, RADIUS, TACACS+

**2. Authorization (Autorisation)**
- Permissions et privilèges
- "Que pouvez-vous faire ?"
- Contrôle d'accès aux commandes

**3. Accounting (Comptabilité)**
- Journalisation des actions
- "Qu'avez-vous fait ?"
- Audit et traçabilité

**Configuration AAA de base :**

```cisco
! Activer AAA
Router(config)# aaa new-model

! Authentification locale pour connexions
Router(config)# aaa authentication login default local

! Liste d'authentification personnalisée
Router(config)# aaa authentication login SSH-LOGIN local

! Appliquer à lignes VTY
Router(config)# line vty 0 4
Router(config-line)# login authentication SSH-LOGIN
```

### Limitation du timeout

**Timeout console :**
```cisco
Router(config)# line console 0
Router(config-line)# exec-timeout 5 0
! Déconnexion après 5 minutes d'inactivité
```

**Timeout VTY :**
```cisco
Router(config)# line vty 0 4
Router(config-line)# exec-timeout 10 0
! Déconnexion après 10 minutes d'inactivité
```

**Timeout privilégié :**
```cisco
! Retour au mode utilisateur après inactivité
Router(config)# privilege exec level 15 timeout 30
```

### Syslog et surveillance

**Configuration du logging :**

```cisco
! Activer timestamps pour logs
Router(config)# service timestamps log datetime msec

! Niveau de logging
Router(config)# logging console warnings
Router(config)# logging buffered 16384 informational

! Serveur Syslog externe
Router(config)# logging host 192.168.1.100
Router(config)# logging trap informational
```

**Niveaux de logging (0-7) :**
| Niveau | Nom | Description |
|--------|-----|-------------|
| 0 | Emergency | Système inutilisable |
| 1 | Alert | Action immédiate requise |
| 2 | Critical | Condition critique |
| 3 | Error | Erreur |
| 4 | Warning | Avertissement |
| 5 | Notice | Normal mais significatif |
| 6 | Informational | Information |
| 7 | Debugging | Debug détaillé |

### Port security (Sécurité des ports)

**Aperçu rapide :**
```cisco
! Activer port security sur interface switch
Switch(config)# interface f0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# switchport port-security mac-address sticky
```

**Note :** Port security sera approfondi dans SRWE (cours 2)

---

## 💡 Bonnes pratiques de sécurité résumées

### Pour les équipements Cisco

✅ **Toujours faire :**
1. Utiliser `enable secret` plutôt que `enable password`
2. Activer `service password-encryption`
3. Configurer SSH et désactiver Telnet
4. Utiliser des mots de passe complexes et uniques
5. Configurer des bannières légales
6. Définir des timeouts sur console et VTY
7. Créer des comptes utilisateurs individuels
8. Désactiver services inutilisés (HTTP, CDP externe)
9. Activer logging et timestamps
10. Sauvegarder régulièrement les configurations

❌ **Ne jamais faire :**
1. Laisser mots de passe par défaut (cisco/cisco)
2. Utiliser Telnet en production
3. Laisser ligne VTY sans mot de passe
4. Activer tous les services par défaut
5. Ignorer les mises à jour de sécurité IOS
6. Négliger les logs et alertes
7. Donner accès privilège 15 à tous
8. Désactiver les timeouts
9. Exposer interfaces d'administration sur Internet
10. Réutiliser mots de passe entre équipements

---

## 🔒 Checklist de sécurisation d'un routeur/switch

```cisco
! === SÉCURISATION BASIQUE ROUTEUR/SWITCH CISCO ===

! 1. Hostname et domaine
configure terminal
hostname R1
ip domain-name company.local

! 2. Mots de passe
enable secret Str0ng@EnableP@ss!
service password-encryption

! 3. Utilisateurs locaux
username admin privilege 15 secret Admin@SecureP@ss2026!
username operator privilege 5 secret Oper@torP@ss2026!

! 4. Bannière
banner motd #Accès autorisé uniquement - Surveillance active#

! 5. SSH
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 3

! 6. Console
line console 0
 password Cons0le@P@ss!
 login
 exec-timeout 5 0
 logging synchronous

! 7. VTY (SSH uniquement)
line vty 0 4
 transport input ssh
 login local
 exec-timeout 10 0
 logging synchronous

! 8. Désactiver services inutiles
no ip http server
no ip http secure-server
no cdp run
no service tcp-small-servers
no service udp-small-servers

! 9. Logging
service timestamps log datetime msec
logging buffered 16384 informational
logging console warnings

! 10. Sauvegarder
end
copy running-config startup-config
```

---

## 📊 Résumé des commandes de sécurité

| Commande | Description |
|----------|-------------|
| `enable secret <password>` | Mot de passe enable chiffré (MD5) |
| `service password-encryption` | Chiffre les mots de passe en clair (Type 7) |
| `username <name> privilege <level> secret <pass>` | Créer utilisateur local |
| `crypto key generate rsa modulus <bits>` | Générer clé RSA pour SSH |
| `ip ssh version 2` | Forcer SSHv2 uniquement |
| `transport input ssh` | Autoriser SSH uniquement sur VTY |
| `login local` | Utiliser base utilisateurs locale |
| `exec-timeout <min> <sec>` | Timeout d'inactivité |
| `banner motd #message#` | Bannière Message of the Day ||`show ip ssh` | Afficher config SSH |
| `show ssh` | Afficher connexions SSH actives |
| `show users` | Afficher utilisateurs connectés |
| `show logging` | Afficher logs système |

---

## 🎯 Points clés à retenir

1. **Sécurité = Défense en profondeur** : Plusieurs couches de protection
2. **Triangle CIA** : Confidentialité, Intégrité, Disponibilité
3. **SSH > Telnet** : Toujours préférer SSH (chiffré)
4. **Mots de passe forts** : Complexes, uniques, changés régulièrement
5. **Principe du moindre privilège** : Donner uniquement accès nécessaire
6. **Désactiver l'inutile** : Réduire surface d'attaque
7. **Surveiller et logger** : Détection et investigation
8. **Mises à jour** : Patcher vulnérabilités connues
9. **Backup réguliers** : Plan de continuité
10. **Formation utilisateurs** : Maillon faible de la sécurité

---

**Module suivant :** [Module 17 - Conception d'un réseau de petite taille](Module-17-notes.md)
