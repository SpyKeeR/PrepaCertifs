# QCM - Module 16 : Principes fondamentaux de la sécurité du réseau
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
Quels sont les trois éléments du triangle CIA de la sécurité informatique ?

- [ ] A. Confidentialité
- [ ] B. Cryptographie
- [ ] C. Intégrité
- [ ] D. Autorisation
- [ ] E. Disponibilité (Availability)

### Question 2
Quelle commande Cisco est recommandée pour sécuriser le mot de passe du mode privilégié ?

- [ ] A. `enable password Cisco123`
- [ ] B. `enable secret Cisco123`
- [ ] C. `password enable Cisco123`
- [ ] D. `secret password Cisco123`

### Question 3
Quelle est la principale différence entre Telnet et SSH ?

- [ ] A. SSH est plus rapide que Telnet
- [ ] B. SSH chiffre les communications, Telnet non
- [ ] C. Telnet est plus sécurisé que SSH
- [ ] D. SSH nécessite moins de ressources système

### Question 4
Quelles sont les trois étapes minimales requises pour configurer SSH sur un routeur Cisco ? (Choisissez trois réponses)

- [ ] A. Configurer un hostname
- [ ] B. Configurer un nom de domaine
- [ ] C. Générer une clé RSA
- [ ] D. Activer le serveur HTTP
- [ ] E. Configurer un mot de passe VTY
- [ ] F. Désactiver Telnet

### Question 5
Quel type d'attaque tente de rendre un service ou un réseau indisponible en le saturant de trafic ?

- [ ] A. Attaque de reconnaissance
- [ ] B. Attaque par déni de service (DoS)
- [ ] C. Attaque d'accès
- [ ] D. Attaque de phishing

### Question 6
Quelle commande chiffre tous les mots de passe en clair dans la configuration d'un routeur ?

- [ ] A. `password encryption enable`
- [ ] B. `service password-encryption`
- [ ] C. `encrypt all passwords`
- [ ] D. `enable password encryption`

### Question 7
Dans le contexte de AAA, que signifie "Authentication" ?

- [ ] A. Définir ce qu'un utilisateur peut faire
- [ ] B. Vérifier l'identité d'un utilisateur
- [ ] C. Enregistrer les actions des utilisateurs
- [ ] D. Autoriser l'accès aux ressources

### Question 8
Quelle commande permet de limiter le temps d'inactivité avant déconnexion automatique sur une ligne console à 5 minutes ?

- [ ] A. `timeout 5`
- [ ] B. `exec-timeout 5 0`
- [ ] C. `idle-timeout 300`
- [ ] D. `disconnect after 5`

### Question 9
Quel est l'ordre correct des étapes pour activer SSH sur un routeur Cisco ?

- [ ] A. Générer clé RSA → Configurer hostname → Configurer domaine → Configurer VTY
- [ ] B. Configurer hostname → Générer clé RSA → Configurer domaine → Configurer VTY
- [ ] C. Configurer hostname → Configurer domaine → Générer clé RSA → Configurer VTY
- [ ] D. Configurer domaine → Configurer hostname → Générer clé RSA → Configurer VTY

### Question 10
Quelle technologie permet de détecter ET bloquer automatiquement les intrusions réseau ?

- [ ] A. IDS (Intrusion Detection System)
- [ ] B. IPS (Intrusion Prevention System)
- [ ] C. Firewall stateless
- [ ] D. Antivirus

### Question 11
Quelles commandes permettent de désactiver des services non nécessaires sur un routeur Cisco pour améliorer la sécurité ? (Choisissez trois réponses)

- [ ] A. `no ip http server`
- [ ] B. `disable unnecessary services`
- [ ] C. `no cdp run`
- [ ] D. `shutdown unused services`
- [ ] E. `no service tcp-small-servers`

### Question 12
Quelle est la taille minimale recommandée pour une clé RSA lors de la configuration SSH ?

- [ ] A. 512 bits
- [ ] B. 768 bits
- [ ] C. 1024 bits
- [ ] D. 2048 bits

### Question 13
Quel type de bannière doit être configuré pour afficher un avertissement légal AVANT que l'utilisateur ne se connecte ?

- [ ] A. Banner login
- [ ] B. Banner exec
- [ ] C. Banner motd (Message of the Day)
- [ ] D. Banner security

### Question 14
Quelle commande permet de forcer l'utilisation uniquement de SSH sur les lignes VTY ?

- [ ] A. `protocol ssh`
- [ ] B. `transport input ssh`
- [ ] C. `access ssh-only`
- [ ] D. `allow ssh only`

### Question 15
Quelle est la différence entre une attaque DoS et une attaque DDoS ?

- [ ] A. DoS est plus puissante que DDoS
- [ ] B. DDoS provient de plusieurs sources, DoS d'une seule
- [ ] C. DoS affecte les serveurs, DDoS affecte les clients
- [ ] D. Il n'y a pas de différence significative

### Question 16
Dans le concept de défense en profondeur, combien de couches de sécurité sont généralement recommandées ?

- [ ] A. 3 couches
- [ ] B. 4 couches
- [ ] C. 6 couches
- [ ] D. 8 couches

### Question 17
Quelle commande affiche la configuration actuelle de SSH sur un routeur ?

- [ ] A. `show ssh config`
- [ ] B. `show ip ssh`
- [ ] C. `display ssh`
- [ ] D. `show crypto ssh`

### Question 18
Quel niveau de logging Syslog doit être utilisé pour enregistrer les messages d'erreur ?

- [ ] A. Level 0 (Emergency)
- [ ] B. Level 3 (Error)
- [ ] C. Level 5 (Notice)
- [ ] D. Level 7 (Debugging)

### Question 19
Quel élément de AAA est responsable de l'enregistrement et de l'audit des actions des utilisateurs ?

- [ ] A. Authentication
- [ ] B. Authorization
- [ ] C. Accounting
- [ ] D. Access Control

### Question 20
Quelle affirmation concernant la commande `enable secret` est correcte ?

- [ ] A. Elle est chiffrée en Type 7 et peut être facilement déchiffrée
- [ ] B. Elle utilise MD5 pour le hachage du mot de passe
- [ ] C. Elle est moins sécurisée que `enable password`
- [ ] D. Elle ne peut pas être utilisée avec AAA

---

## Réponses et Explications

### Question 1
**Réponses correctes : A, C, E**

**Explication :**
Le triangle CIA représente les trois piliers fondamentaux de la sécurité informatique :
- **Confidentialité (Confidentiality)** : Les données ne sont accessibles qu'aux personnes autorisées
- **Intégrité (Integrity)** : Les données ne sont pas modifiées ou altérées de manière non autorisée
- **Disponibilité (Availability)** : Les services et données sont accessibles quand nécessaire

**💡 Point clé :** CIA est l'acronyme universel de la sécurité informatique. La cryptographie (B) et l'autorisation (D) sont des outils/méthodes pour atteindre les objectifs CIA, mais ne font pas partie du triangle lui-même.

---

### Question 2
**Réponse correcte : B**

**Explication :**
`enable secret` est la commande recommandée car elle utilise le hachage MD5, beaucoup plus sécurisé que le chiffrement Type 7 utilisé par `enable password`.

**Syntaxe :**
```cisco
Router(config)# enable secret Str0ng@P@ss!
```

**💡 Point clé :** Si `enable secret` et `enable password` sont tous deux configurés, `enable secret` prend la priorité et `enable password` est ignoré.

---

### Question 3
**Réponse correcte : B**

**Explication :**
SSH (Secure Shell) chiffre toutes les communications entre le client et le serveur, y compris l'authentification et les données transmises. Telnet transmet tout en clair, ce qui permet l'interception facile des mots de passe par sniffing.

**💡 Point clé :** Telnet est considéré comme obsolète et dangereux. SSH doit TOUJOURS être utilisé pour l'administration à distance en production.

---

### Question 4
**Réponses correctes : A, B, C**

**Explication :**
Les trois prérequis minimaux pour SSH sont :

1. **Hostname** : `hostname R1`
2. **Nom de domaine** : `ip domain-name company.local`
3. **Clé RSA** : `crypto key generate rsa modulus 2048`

Ces trois éléments sont nécessaires car la clé RSA est générée en utilisant le hostname et le nom de domaine comme partie du FQDN.

**💡 Point clé :** Sans ces trois éléments, la commande `crypto key generate rsa` échouera.

---

### Question 5
**Réponse correcte : B**

**Explication :**
Une attaque par déni de service (DoS - Denial of Service) vise à rendre un service indisponible en saturant les ressources (bande passante, CPU, mémoire) ou en exploitant des vulnérabilités qui provoquent des crashs.

**Types courants :**
- SYN Flood
- UDP Flood
- Ping of Death
- Smurf Attack

**💡 Point clé :** DDoS (Distributed DoS) utilise plusieurs sources (botnet) pour amplifier l'attaque et la rendre plus difficile à bloquer.

---

### Question 6
**Réponse correcte : B**

**Explication :**
La commande `service password-encryption` chiffre automatiquement tous les mots de passe en clair (Type 7) dans la configuration, notamment :
- Mot de passe console
- Mot de passe VTY
- `enable password` (pas `enable secret` qui est déjà en MD5)

**Syntaxe :**
```cisco
Router(config)# service password-encryption
```

**💡 Point clé :** Le chiffrement Type 7 est faible et peut être déchiffré facilement. C'est pourquoi `enable secret` (MD5) est préférable à `enable password`.

---

### Question 7
**Réponse correcte : B**

**Explication :**
AAA signifie :
- **Authentication** : "Qui êtes-vous ?" - Vérification de l'identité (login/password, certificat, biométrie)
- **Authorization** : "Que pouvez-vous faire ?" - Permissions et privilèges
- **Accounting** : "Qu'avez-vous fait ?" - Journalisation et audit des actions

**💡 Point clé :** L'authentification DOIT réussir avant que l'autorisation ne soit vérifiée. Accounting enregistre les actions pour audit ultérieur.

---

### Question 8
**Réponse correcte : B**

**Explication :**
La commande `exec-timeout <minutes> <secondes>` configure le délai d'inactivité avant déconnexion automatique.

**Syntaxe :**
```cisco
Router(config)# line console 0
Router(config-line)# exec-timeout 5 0
! 5 minutes et 0 secondes
```

**Valeurs courantes :**
- Console : 5 minutes (`exec-timeout 5 0`)
- VTY : 10 minutes (`exec-timeout 10 0`)
- Désactiver : `exec-timeout 0 0` (DANGEREUX en production)

**💡 Point clé :** Ne JAMAIS utiliser `exec-timeout 0 0` en production, cela désactive le timeout et laisse les sessions ouvertes indéfiniment.

---

### Question 9
**Réponse correcte : C**

**Explication :**
L'ordre correct pour configurer SSH :

1. **Configurer hostname** : `hostname R1`
2. **Configurer domaine** : `ip domain-name company.local`
3. **Générer clé RSA** : `crypto key generate rsa modulus 2048`
4. **Configurer VTY** : `line vty 0 4` puis `transport input ssh`

**💡 Point clé :** Le hostname et le domaine DOIVENT être configurés AVANT de générer la clé RSA, car ils sont utilisés dans la génération de la clé.

---

### Question 10
**Réponse correcte : B**

**Explication :**
- **IDS (Intrusion Detection System)** : DÉTECTE les intrusions et génère des alertes, mais ne bloque pas
- **IPS (Intrusion Prevention System)** : DÉTECTE ET BLOQUE activement les intrusions

**💡 Point clé :** IPS = IDS + capacité de blocage actif. IPS est placé en ligne (in-line) dans le flux réseau, IDS est généralement en mode passif (monitoring).

---

### Question 11
**Réponses correctes : A, C, E**

**Explication :**
Services à désactiver pour améliorer la sécurité :

```cisco
! Serveur HTTP/HTTPS
no ip http server
no ip http secure-server

! CDP (Cisco Discovery Protocol) si non nécessaire
no cdp run

! Small servers (echo, discard, chargen, etc.)
no service tcp-small-servers
no service udp-small-servers

! Finger service
no service finger
```

**💡 Point clé :** Principe de sécurité : Désactiver tout service non nécessaire pour réduire la surface d'attaque.

---

### Question 12
**Réponse correcte : C (minimum acceptable) ou D (recommandé)**

**Explication :**
Tailles de clés RSA :
- **512 bits** : Obsolète, non sécurisé
- **768 bits** : Faible, déconseillé
- **1024 bits** : Minimum acceptable pour SSH
- **2048 bits** : **Recommandé** (standard actuel)
- **4096 bits** : Très sécurisé (peut être lent sur anciens équipements)

**Syntaxe :**
```cisco
Router(config)# crypto key generate rsa modulus 2048
```

**💡 Point clé :** Cisco IOS accepte 1024 comme minimum, mais 2048 est fortement recommandé pour une sécurité moderne.

---

### Question 13
**Réponse correcte : C**

**Explication :**
Types de bannières :

| Bannière | Moment d'affichage | Usage |
|----------|-------------------|-------|
| **motd** | Avant login | Avertissement légal |
| **login** | Pendant login | Instructions de connexion |
| **exec** | Après login réussi | Message de bienvenue |

**Configuration :**
```cisco
Router(config)# banner motd #
**************************************************
*   ACCES AUTORISE UNIQUEMENT                   *
*   Connexions surveillées et enregistrées      *
**************************************************
#
```

**💡 Point clé :** MOTD doit contenir un avertissement légal mais éviter les termes "Bienvenue" ou "Welcome" qui peuvent impliquer consentement d'accès.

---

### Question 14
**Réponse correcte : B**

**Explication :**
La commande `transport input ssh` restreint l'accès aux lignes VTY uniquement via SSH, bloquant Telnet.

**Configuration complète :**
```cisco
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# login local
```

**Options de transport :**
- `transport input ssh` : SSH uniquement
- `transport input telnet` : Telnet uniquement
- `transport input ssh telnet` : SSH et Telnet
- `transport input all` : Tous les protocoles (défaut)
- `transport input none` : Aucun accès

**💡 Point clé :** En production, toujours utiliser `transport input ssh` uniquement.

---

### Question 15
**Réponse correcte : B**

**Explication :**
- **DoS (Denial of Service)** : Attaque provenant d'une seule source
- **DDoS (Distributed DoS)** : Attaque coordonnée provenant de multiples sources (botnet)

**Caractéristiques DDoS :**
- Plus puissant (agrégation de bande passante)
- Plus difficile à bloquer (multiples IPs sources)
- Utilise des machines compromises (zombies)

**💡 Point clé :** DDoS est beaucoup plus dangereux car bloquer une seule IP source ne suffit pas.

---

### Question 16
**Réponse correcte : C**

**Explication :**
Le modèle de défense en profondeur recommande **6 couches** de sécurité :

1. **Physique** : Accès aux locaux
2. **Périmétrique** : Firewalls, VPN
3. **Réseau** : VLANs, ACL, 802.1X
4. **Équipements** : Sécurité des devices
5. **Applicative** : Sécurité des applications
6. **Données** : Chiffrement, backups

**💡 Point clé :** La sécurité multicouche garantit que si une couche est compromise, les autres continuent de protéger.

---

### Question 17
**Réponse correcte : B**

**Explication :**
Commandes de vérification SSH :

```cisco
! Configuration SSH
show ip ssh

! Connexions SSH actives
show ssh

! Utilisateurs connectés (SSH et console)
show users
```

**Sortie `show ip ssh` :**
- Version SSH (1.99 ou 2.0)
- Timeout
- Tentatives d'authentification
- État du service

**💡 Point clé :** `show ip ssh` affiche la CONFIG, `show ssh` affiche les SESSIONS actives.

---

### Question 18
**Réponse correcte : B**

**Explication :**
Niveaux de logging Syslog (0-7) :

| Niveau | Nom | Usage |
|--------|-----|-------|
| 0 | Emergency | Système inutilisable |
| 1 | Alert | Action immédiate requise |
| 2 | Critical | Condition critique |
| **3** | **Error** | **Erreurs** |
| 4 | Warning | Avertissements |
| 5 | Notice | Normal mais significatif |
| 6 | Informational | Informations |
| 7 | Debugging | Debug (éviter en prod) |

**Configuration :**
```cisco
Router(config)# logging trap 3
! Envoyer niveau Error et supérieur (0-3)
```

**💡 Point clé :** Un niveau de logging capture ce niveau ET tous les niveaux supérieurs (plus critiques).

---

### Question 19
**Réponse correcte : C**

**Explication :**
**Accounting** est responsable de :
- Enregistrement des connexions/déconnexions
- Journalisation des commandes exécutées
- Durée des sessions
- Audit et conformité

**Configuration basique :**
```cisco
aaa new-model
aaa accounting exec default start-stop group tacacs+
aaa accounting commands 15 default start-stop group tacacs+
```

**💡 Point clé :** Accounting permet la traçabilité : "Qui a fait quoi, quand, et pendant combien de temps ?"

---

### Question 20
**Réponse correcte : B**

**Explication :**
`enable secret` utilise le hachage MD5 (Type 5) pour stocker le mot de passe de manière sécurisée.

**Comparaison :**
- `enable password` : Type 7 (faible, réversible)
- `enable secret` : MD5 Type 5 (fort, irréversible)

**Dans running-config :**
```cisco
enable secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
! Le "5" indique MD5
```

**💡 Point clé :** `enable secret` remplace toujours `enable password` si les deux sont configurés. Utiliser UNIQUEMENT `enable secret` en production.

---

**Score recommandé pour valider le module : 16/20 minimum (80%)**

**Révision conseillée si score < 16/20 :**
- Section 16.2 (Attaques réseau)
- Section 16.4 (Sécurité des périphériques - SSH, AAA)
- Commandes de configuration Cisco
