# 📚 Notes de Révision - Sujet 110 : Sécurité

## 📋 Informations générales

- **Sujet** : 110 - Sécurité
- **Poids** : 12 points
- **Nombre d'objectifs** : 3

### Répartition des objectifs

| Objectif | Titre | Poids |
|----------|-------|-------|
| 110.1 | Tâches d'administration de sécurité | 3 points |
| 110.2 | Configuration de la sécurité du système | 3 points |
| 110.3 | Sécurisation des données avec le chiffrement | 6 points |

---

## 📑 Table des matières

1. [110.1 - Tâches d'administration de sécurité](#1101---tâches-dadministration-de-sécurité)
2. [110.2 - Configuration de la sécurité du système](#1102---configuration-de-la-sécurité-du-système)
3. [110.3 - Sécurisation des données avec le chiffrement](#1103---sécurisation-des-données-avec-le-chiffrement)
4. [Checklist de révision](#-checklist-de-révision)
5. [Exercices pratiques](#-exercices-pratiques)
6. [Ressources complémentaires](#-ressources-complémentaires)
7. [Points clés pour l'examen](#-points-clés-pour-lexamen)

---

## 110.1 - Tâches d'administration de sécurité

### 🔐 Permissions SUID et SGID

#### Concept

| Permission | Représentation numérique | Représentation symbolique | Effet |
|------------|-------------------------|---------------------------|-------|
| **SUID** | 4000 | s (minuscule) ou S (majuscule) | Exécution avec privilèges du propriétaire |
| **SGID** | 2000 | s (minuscule) ou S (majuscule) | Exécution avec privilèges du groupe |
| **Sticky Bit** | 1000 | t (minuscule) ou T (majuscule) | Protection des fichiers dans /tmp |

**Différence entre s et S** :
- **s minuscule** (rws) : SUID/SGID + permission d'exécution
- **S majuscule** (rwS) : SUID/SGID sans permission d'exécution sous-jacente

#### Commandes find pour les permissions spéciales

```bash
# Rechercher fichiers avec SUID uniquement
find . -perm 4000
find . -perm u+s

# Rechercher fichiers avec SUID (+ autres permissions)
find /usr/bin -perm -4000
find /usr/bin -perm -u+s

# Rechercher fichiers avec SGID uniquement
find . -perm 2000
find . -perm g+s

# Rechercher fichiers avec SGID (+ autres permissions)
find /usr/bin -perm -2000
find /usr/bin -perm -g+s

# Rechercher fichiers avec SUID OU SGID
find /usr/bin -perm /6000

# Définir SGID sur un répertoire
chmod 2755 shared_directory
```

**Syntaxe find -perm** :
- `-perm valeur` : Permission exclusive
- `-perm -valeur` : Permission présente (+ autres permissions)
- `-perm /valeur` : L'une OU l'autre des permissions

---

### 👤 Gestion des mots de passe et expiration

#### Commande passwd

```bash
# Afficher état du compte
passwd -S carol
# Résultat : carol P 12/07/2019 0 99999 7 -1

# Verrouiller mot de passe
passwd -l utilisateur
usermod -L utilisateur        # Alternative

# Déverrouiller mot de passe
passwd -u utilisateur
usermod -U utilisateur        # Alternative

# Forcer changement au prochain login
passwd -e utilisateur

# Supprimer le mot de passe (dangereux)
passwd -d utilisateur
```

**Champs de passwd -S** :
1. Nom d'utilisateur
2. État : P (password), L (locked), NP (no password)
3. Date dernier changement
4. Durée minimale (jours entre changements)
5. Durée maximale (validité en jours)
6. Période d'avertissement (jours)
7. Période d'inactivité (jours après expiration)

#### Commande chage

```bash
# Afficher informations d'expiration
chage -l utilisateur

# Mode interactif
chage utilisateur

# Options principales
chage -m 5 utilisateur      # Min jours entre changements
chage -M 30 utilisateur     # Max jours validité (0-99999)
chage -d 0 utilisateur      # Forcer changement au login
chage -W 7 utilisateur      # Période avertissement
chage -I 10 utilisateur     # Inactivité après expiration
chage -E 2050-12-13 user    # Date expiration compte (AAAA-MM-JJ)

# Désactiver expiration
chage -M 99999 utilisateur
chage -E -1 utilisateur
```

---

### 🌐 Dépistage des ports ouverts

#### Commande lsof

```bash
# Afficher tous les fichiers réseau Internet
lsof -i

# Filtrer par hôte
lsof -i@192.168.1.7

# Filtrer par port
lsof -i :22
lsof -i :22,80              # Ports multiples
lsof -i :22-80              # Plage de ports

# Filtrer par protocole
lsof -i4                    # IPv4 uniquement
lsof -i6                    # IPv6 uniquement
lsof -i tcp                 # TCP uniquement
lsof -i udp                 # UDP uniquement

# Combinaisons
lsof -i@192.168.1.7:22,80
lsof -i tcp:80
```

#### Commande fuser

```bash
# Afficher processus utilisant répertoire courant
fuser .
fuser -v .                  # Verbose

# Afficher processus sur port réseau
fuser -n tcp 80
fuser -vn tcp 80            # Verbose

# Tuer processus utilisant un port
fuser -k 80/tcp
fuser -vn tcp 80 -k         # Verbose + kill
```

**Colonnes fuser -v** :
- **USER** : Propriétaire
- **PID** : Process ID
- **ACCESS** : Type d'accès (c=current dir, e=executable, f=open file, F=open for write, r=root dir, m=mmap)
- **COMMAND** : Commande associée

#### Commande netstat

```bash
# Afficher connexions actives
netstat

# Afficher ports en écoute
netstat -l                  # Listening
netstat -lt                 # TCP listening
netstat -lu                 # UDP listening
netstat -lute               # TCP+UDP + extended info

# Afficher connexions établies
netstat -t                  # TCP
netstat -u                  # UDP
netstat -ute                # TCP+UDP + extended

# Format numérique (pas de résolution DNS)
netstat -ltn                # Listening TCP numérique
netstat -uten               # UDP+TCP established numérique

# Afficher table de routage
netstat -r
netstat -rn                 # Numérique
```

**Options netstat** :
- `-l, --listening` : Ports en écoute
- `-t, --tcp` : Protocole TCP
- `-u, --udp` : Protocole UDP
- `-n, --numeric` : Adresses numériques
- `-e, --extend` : Informations étendues
- `-r, --route` : Table de routage

#### Commande nmap

```bash
# Scanner un hôte
nmap localhost
nmap 192.168.1.10

# Scanner plusieurs hôtes
nmap localhost 192.168.1.7
nmap 192.168.1.3-20         # Plage
nmap 192.168.1.*            # Wildcard
nmap 192.168.1.0/24         # CIDR
nmap 192.168.1.0/24 --exclude 192.168.1.7

# Scanner un port spécifique
nmap -p 22 localhost
nmap -p ssh localhost       # Nom de service
nmap -p 22,80,443 host      # Ports multiples
nmap -p 22-80 host          # Plage
nmap -p- host               # Tous les ports (1-65535)

# Options utiles
nmap -F localhost           # Fast scan (100 ports courants)
nmap -v localhost           # Verbose
nmap -A localhost           # Aggressive (OS detection, version, scripts, traceroute)
nmap -sV localhost          # Version detection

# Ping scan (découverte hôtes)
nmap -sn 192.168.1.0/24
```

---

### ⚙️ Limiter ressources avec ulimit

#### Concept

**Deux types de limites** :
- **Soft limit** (-S) : Limite souple, modifiable par utilisateur
- **Hard limit** (-H) : Limite stricte, modifiable uniquement par root

```bash
# Afficher limites actuelles
ulimit                      # Blocs fichiers soft
ulimit -a                   # Toutes limites soft
ulimit -Sa                  # Toutes limites soft (explicite)
ulimit -Ha                  # Toutes limites hard

# Afficher limite spécifique
ulimit -u                   # Max processus (soft)
ulimit -Su                  # Max processus soft
ulimit -Hu                  # Max processus hard
```

#### Options de ressources

| Option | Ressource | Description |
|--------|-----------|-------------|
| `-b` | Socket buffer size | Taille tampon socket |
| `-c` | Core file size | Taille fichiers core |
| `-d` | Data seg size | Taille segment données |
| `-f` | File size | Taille fichiers écrits |
| `-l` | Locked memory | Mémoire verrouillée |
| `-m` | RSS size | Taille ensemble résident |
| `-n` | Open files | Nombre fichiers ouverts |
| `-u` | Max processes | Nombre max processus |
| `-v` | Virtual memory | Mémoire virtuelle |

#### Définir limites

```bash
# Définir limite soft
ulimit -Sf 500              # Taille fichiers à 500 blocs

# Définir limite hard
ulimit -Hf 1000

# Définir les deux (soft + hard)
ulimit -f 500

# Définir soft sans dépasser hard
ulimit -Sf 200              # OK si hard >= 200

# Valeurs spéciales
ulimit -f unlimited         # Illimité
ulimit -f soft              # Valeur soft actuelle
ulimit -f hard              # Valeur hard actuelle
```

**⚠️ Règles importantes** :
- Utilisateurs normaux peuvent **réduire** hard limits
- Utilisateurs normaux peuvent **augmenter** soft limits (jusqu'à hard)
- Seul **root** peut augmenter hard limits
- Limites persistent dans session shell uniquement
- Pour persistance : modifier `/etc/security/limits.conf`

---

### 📊 Gérer utilisateurs connectés

#### Commande last

```bash
# Afficher derniers utilisateurs connectés
last

# Afficher pour utilisateur spécifique
last carol

# Fichier source
/var/log/wtmp

# Afficher tentatives échouées
lastb
```

**Lecture du résultat last** :
```
carol pts/0 192.168.1.4 Sat Jun 6 14:25 still logged in
```
- **carol** : Utilisateur
- **pts/0** : Terminal (Pseudo Terminal Slave)
- **192.168.1.4** : Hôte distant
- **Sat Jun 6 14:25** : Heure connexion
- **still logged in** : Toujours connecté

#### Commande who

```bash
# Afficher utilisateurs connectés
who

# Options utiles
who -H                      # Avec en-têtes
who -b                      # Heure dernier boot
who -r                      # Runlevel actuel
```

**Format** : `utilisateur terminal date_heure (hôte)`

#### Commande w

```bash
# Afficher utilisateurs + activité
w

# Pour utilisateur spécifique
w mimi
```

**En-tête** :
- Heure actuelle
- Uptime (durée fonctionnement)
- Nombre utilisateurs
- Load average (1, 5, 15 min)

**Colonnes** :
- **USER** : Nom utilisateur
- **TTY** : Terminal
- **FROM** : Hôte distant
- **LOGIN@** : Heure connexion
- **IDLE** : Temps inactivité
- **JCPU** : Temps processus attachés au tty
- **PCPU** : Temps processus actuel
- **WHAT** : Commande en cours

---

### 🔑 Commandes su et sudo

#### Commande su

```bash
# Devenir root
su                          # Conserve environnement
su -                        # Charge environnement root
su - root                   # Explicite

# Devenir autre utilisateur
su - carol
su - carol -c "whoami"      # Exécuter commande
```

**Différence - (tiret)** :
- **Avec -** : Charge environnement utilisateur cible
- **Sans -** : Conserve environnement actuel

#### Commande sudo

```bash
# Exécuter commande en tant que root
sudo commande

# Exécuter en tant qu'autre utilisateur
sudo -u mimi whoami
sudo -u mimi systemctl status apache2

# Lancer shell root
sudo -i                     # Login shell
sudo -s                     # Non-login shell
sudo su -                   # Alternative
```

**Avantages sudo vs su** :
- Nécessite mot de passe utilisateur (pas root)
- Commandes ponctuelles (pas nouveau shell)
- Traçabilité (logs)
- Politique de sécurité configurable

#### Fichier /etc/sudoers

**⚠️ Toujours éditer avec** : `visudo`

**Syntaxe de base** :
```
utilisateur hôtes=(run_as) commandes
```

**Exemples** :
```bash
# Root peut tout faire partout
root ALL=(ALL:ALL) ALL

# Groupe sudo peut tout faire
%sudo ALL=(ALL:ALL) ALL

# Carol peut vérifier Apache
carol ALL=(ALL:ALL) /usr/bin/systemctl status apache2

# Sans mot de passe
carol ALL=(ALL:ALL) NOPASSWD: /usr/bin/systemctl status apache2

# Hôte spécifique, utilisateur spécifique
carol 192.168.1.7=(mimi) /usr/bin/systemctl status apache2

# Définir éditeur par défaut
Defaults editor=/usr/bin/nano

# Timeout cache credentials (défaut 15 min)
Defaults timestamp_timeout=5
```

**Alias** :
```bash
# Alias d'hôtes
Host_Alias SERVERS = 192.168.1.7, server1, server2

# Alias d'utilisateurs
User_Alias ADMINS = carol, %sudo, !john

# Alias de commandes
Cmnd_Alias SERVICES = /usr/bin/systemctl *

# Utilisation
ADMINS SERVERS=SERVICES
```

**Symboles spéciaux** :
- `%groupe` : Membres du groupe
- `!utilisateur` : Exclure utilisateur
- `ALL` : Tout (hôtes, utilisateurs, commandes)
- `NOPASSWD:` : Pas de mot de passe requis

---

## 110.2 - Configuration de la sécurité du système

### 🔒 Mots de passe cachés (Shadow Passwords)

#### Fichiers /etc/passwd et /etc/shadow

**Structure /etc/passwd** (7 champs) :
```
carol:x:1001:1001:Carol User:/home/carol:/bin/bash
```
1. Identifiant de connexion
2. Substitut mot de passe (`x` = mot de passe dans /etc/shadow)
3. UID (User ID)
4. GID (Group ID)
5. GECOS (commentaire)
6. Répertoire personnel
7. Shell par défaut

**Structure /etc/shadow** :
```
carol:$6$hash...:18778:0:99999:7:::
```
1. Nom utilisateur
2. Mot de passe haché (vide = pas de mot de passe, ! = verrouillé)
3. Date dernier changement (jours depuis 1970-01-01)
4. Jours min entre changements
5. Jours max validité
6. Jours avertissement
7. Jours inactivité après expiration
8. Date expiration compte
9. Réservé

#### Empêcher connexions

```bash
# Créer /etc/nologin (tous sauf root)
sudo sh -c 'echo "Maintenance système" > /etc/nologin'
sudo rm /etc/nologin        # Supprimer

# Définir shell nologin pour utilisateur
sudo usermod -s /sbin/nologin emma
```

---

### 🛡️ Super-démons (xinetd et systemd.socket)

#### xinetd (Internet Super Daemon)

**Concept** : Surveille ports réseau et démarre services à la demande (économie ressources).

**Fichiers de configuration** :
- `/etc/xinetd.conf` : Configuration principale
- `/etc/xinetd.d/*` : Configuration par service

**Exemple /etc/xinetd.d/ssh** :
```bash
service ssh
{
    disable         = no
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/sshd
    server_args     = -i
    flags           = IPv4
    interface       = 192.168.178.1
}
```

**Directives importantes** :
- `disable` : yes/no (activer/désactiver)
- `socket_type` : stream (TCP) / dgram (UDP)
- `protocol` : tcp / udp
- `wait` : no (TCP) / yes (UDP multi-thread)
- `user` : Utilisateur propriétaire
- `server` : Chemin exécutable
- `server_args` : Options (ex: -i pour SSH)
- `interface` : Interface réseau (ou `bind`)

```bash
# Redémarrer xinetd
systemctl restart xinetd.service

# Vérifier port en écoute
lsof -i :22
```

#### systemd.socket

**Alternative moderne à xinetd.**

```bash
# Démarrer socket SSH
systemctl start ssh.socket
systemctl start sshd.socket     # Selon distribution

# Vérifier
lsof -i :22 -P
```

---

### 🔍 Vérifier services actifs

#### Systèmes SysV-init

```bash
# Afficher tous services
service --status-all

# Désactiver service (Debian)
update-rc.d SERVICE-NAME remove

# Désactiver service (Red Hat)
chkconfig SERVICE-NAME off
```

#### Systèmes systemd

```bash
# Lister services actifs
systemctl list-units --state active --type service

# Désactiver et arrêter service
systemctl disable UNIT --now

# Afficher services réseau en écoute
ss -ltu                     # Moderne
netstat -ltu                # Obsolète (net-tools)
```

---

### 🚧 TCP Wrappers

**⚠️ Note** : Supprimé dans Red Hat/Fedora récent, mais utile pour systèmes legacy.

**Fichiers de configuration** :
- `/etc/hosts.deny` : Règles de blocage
- `/etc/hosts.allow` : Règles d'autorisation

**Ordre d'évaluation** : allow → deny

```bash
# Vérifier si démon supporte libwrap
ldd /usr/sbin/sshd | grep "libwrap"

# Exemple : bloquer SSH sauf réseau local
# /etc/hosts.deny
sshd: ALL

# /etc/hosts.allow
sshd: LOCAL
sshd: 192.168.1.0/24

# Syntaxe
daemon: client_list
```

**Options client_list** :
- `ALL` : Tous
- `LOCAL` : Réseau local
- `192.168.1.0/255.255.255.0` : Sous-réseau
- `192.168.1.` : Préfixe
- `.example.com` : Domaine
- `EXCEPT` : Exception

---

## 110.3 - Sécurisation des données avec le chiffrement

### 🔐 OpenSSH : Configuration et utilisation

#### Connexion SSH de base

```bash
# Connexion avec utilisateur spécifié
ssh utilisateur@hôte
ssh carol@192.168.1.77

# Connexion (utilisateur identique local/distant)
ssh hôte
ssh 192.168.1.77

# Exécuter commande à distance
ssh utilisateur@hôte commande
ssh ina@halof ls -l
```

**Première connexion** :
- Vérification empreinte clé hôte
- Ajout à `~/.ssh/known_hosts`

#### Authentification par clé SSH

**Étape 1 : Générer paire de clés**
```bash
# Générer clé ECDSA 256 bits
ssh-keygen -t ecdsa -b 256

# Générer clé Ed25519 (recommandé, le plus sûr)
ssh-keygen -t ed25519

# Générer clé RSA 4096 bits
ssh-keygen -t rsa -b 4096

# Emplacement par défaut
~/.ssh/id_TYPE          # Clé privée
~/.ssh/id_TYPE.pub      # Clé publique
```

**Types d'algorithmes** :

| Algorithme | Taille clé | Sécurité | Notes |
|------------|------------|----------|-------|
| **RSA** | 1024-4096 bits (2048 défaut) | Bonne | Standard, compatible |
| **DSA** | 1024 bits fixe | ❌ Faible | Déprécié depuis OpenSSH 7.0 |
| **ECDSA** | 256, 384, 521 bits | Très bonne | Amélioration de DSA |
| **Ed25519** | 256 bits fixe | ⭐ Excellente | Recommandé, plus sûr |

**Étape 2 : Copier clé publique sur serveur**
```bash
# Méthode 1 : ssh-copy-id (recommandé)
ssh-copy-id utilisateur@hôte

# Méthode 2 : Manuelle via cat/ssh
cat ~/.ssh/id_ecdsa.pub | ssh user@host 'cat >> .ssh/authorized_keys'

# Méthode 3 : scp
scp ~/.ssh/id_ecdsa.pub user@host:~/.ssh/authorized_keys
```

**Étape 3 : Se connecter**
```bash
# Avec phrase de passe
ssh utilisateur@hôte
# → Demande phrase de passe de la clé

# Sans phrase de passe
ssh utilisateur@hôte
# → Connexion directe
```

#### Agent d'authentification SSH (ssh-agent)

**Sécurité + Confort** : Stocker clé en mémoire pour session.

```bash
# Lancer agent dans nouveau shell
ssh-agent /bin/bash

# Ajouter clé privée
ssh-add
# → Demande phrase de passe UNE FOIS

# Lister clés chargées
ssh-add -l

# Supprimer toutes clés
ssh-add -D

# Se connecter (sans redemander phrase)
ssh utilisateur@hôte
```

#### Gestion known_hosts

```bash
# Supprimer clé d'un hôte
ssh-keygen -R hostname
ssh-keygen -R 192.168.1.77
ssh-keygen -f ~/.ssh/known_hosts -R hostname

# Afficher empreinte clé
ssh-keygen -l -f ~/.ssh/id_ecdsa
ssh-keygen -lv -f ~/.ssh/id_ecdsa  # + art ASCII
```

---

### 🖥️ Clés d'hôte du serveur OpenSSH

#### Emplacement et structure

```
/etc/ssh/
├── ssh_host_rsa_key          # Clé privée RSA
├── ssh_host_rsa_key.pub      # Clé publique RSA
├── ssh_host_dsa_key          # Clé privée DSA
├── ssh_host_dsa_key.pub      # Clé publique DSA
├── ssh_host_ecdsa_key        # Clé privée ECDSA
├── ssh_host_ecdsa_key.pub    # Clé publique ECDSA
├── ssh_host_ed25519_key      # Clé privée Ed25519
├── ssh_host_ed25519_key.pub  # Clé publique Ed25519
├── ssh_config                # Config client
└── sshd_config               # Config serveur
```

**Permissions** :
- Clés privées : `0600` (-rw-------)
- Clés publiques : `0644` (-rw-r--r--)

#### Afficher empreintes

```bash
# Empreinte clé hôte
ssh-keygen -l -f /etc/ssh/ssh_host_ed25519_key
ssh-keygen -l -f /etc/ssh/ssh_host_ed25519_key.pub

# Empreinte + art ASCII
ssh-keygen -lv -f /etc/ssh/ssh_host_ed25519_key.pub
```

---

### 🔀 Tunnels de ports SSH

#### Tunnel local (Local Port Forwarding)

**Syntaxe** : `ssh -L port_local:destination:port_dest hôte_intermédiaire`

```bash
# Tunnel vers www.gnu.org via localhost:8585
ssh -L 8585:www.gnu.org:80 localhost

# Tunnel via serveur distant
ssh -L 8585:www.gnu.org:80 -Nf user@remote_server

# Accéder
curl http://localhost:8585
```

**Options** :
- `-L` : Local port forwarding
- `-N` : Pas de shell interactif (redirection seule)
- `-f` : Exécution en arrière-plan

**Cas d'usage** :
- Accéder service distant via tunnel chiffré
- Contourner pare-feu
- Sécuriser protocole non chiffré

#### Tunnel distant (Remote Port Forwarding)

**Syntaxe** : `ssh -R port_distant:destination:port_dest hôte_distant`

```bash
# Rendre serveur web local accessible via serveur distant
ssh -R 8585:localhost:80 -Nf user@remote_server

# Autoriser toutes interfaces (nécessite GatewayPorts yes)
ssh -R 0.0.0.0:8585:localhost:80 -Nf user@remote

# Sur serveur distant
curl http://localhost:8585
```

**Directive sshd_config** :
```bash
# /etc/ssh/sshd_config
GatewayPorts yes            # Autoriser bind sur toutes interfaces
```

**Cas d'usage** :
- Accès externe vers machine locale
- NAT traversal
- Exposer service local temporairement

#### Tunnel X11 (X11 Forwarding)

```bash
# Activer X11 forwarding
ssh -X utilisateur@hôte

# Lancer application graphique
firefox                     # S'affiche localement

# Désactiver X11 forwarding
ssh -x utilisateur@hôte
```

**Directive sshd_config** :
```bash
X11Forwarding yes
```

#### Tunnels multiples

```bash
# Deux tunnels locaux
ssh -L 8080:www.gnu.org:80 -L 8585:www.melpa.org:80 -Nf user@host
```

---

### 🔐 GnuPG (GNU Privacy Guard)

#### Configuration de base

```bash
# Générer paire de clés
gpg --gen-key
# → Demande nom, email, phrase de passe

# Génération complète (plus d'options)
gpg --full-generate-key

# Lister clés publiques
gpg --list-keys

# Lister clés privées
gpg --list-secret-keys

# Afficher empreinte
gpg --fingerprint USER-ID
```

**Répertoire de configuration** : `~/.gnupg/`

| Fichier/Dossier | Description |
|----------------|-------------|
| `pubring.kbx` | Trousseau clés publiques |
| `trustdb.gpg` | Base de données de confiance |
| `private-keys-v1.d/` | Clés privées |
| `openpgp-revocs.d/` | Certificats de révocation |

**Anatomie d'une clé** :
```
pub   rsa3072 2020-07-03 [SC] [expires: 2022-07-03]
      D18FA0021F644CDAF57FD0F919BBEFD16813034E
uid           [ultimate] carol <carol@debian>
sub   rsa3072 2020-07-03 [E] [expires: 2022-07-03]
```
- **Empreinte** : `D18FA0021F644CDAF57FD0F919BBEFD16813034E`
- **KEY-ID** : 8 derniers digits (`6813034E`)
- **USER-ID** : `carol` ou `carol <carol@debian>`

#### Exporter et importer clés

```bash
# Exporter clé publique (binaire)
gpg --export carol > carol.pub.key

# Exporter clé publique (ASCII armored)
gpg --export --armor carol > carol.pub.asc
gpg -a --export carol > carol.pub.asc

# Exporter clé privée
gpg --export-secret-keys --armor carol > carol.priv.asc

# Importer clé publique
gpg --import carol.pub.key

# Serveurs de clés
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID
gpg --keyserver keyserver.ubuntu.com --recv-keys KEY-ID
```

#### Révocation de clés

```bash
# Générer certificat de révocation
gpg --output revocation.asc --gen-revoke carol
# → Choisir raison (0=pas spécifiée, 1=compromise, 2=remplacée, 3=plus utilisée)

# Révoquer clé (importer certificat)
gpg --import revocation.asc

# Vérifier révocation
gpg --list-keys
# → uid [revoked]

# Distribuer clé révoquée
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID
```

#### Chiffrer et déchiffrer fichiers

```bash
# Chiffrer fichier
gpg --output encrypted.gpg --recipient carol --encrypt message.txt
gpg -o encrypted.gpg -r carol -e message.txt  # Abrégé

# Chiffrer (ASCII armored)
gpg --armor --output encrypted.asc --recipient carol --encrypt message.txt
gpg -a -o encrypted.asc -r carol -e message.txt

# Chiffrer pour plusieurs destinataires
gpg -r alice -r bob --encrypt message.txt

# Déchiffrer fichier
gpg --output message.txt --decrypt encrypted.gpg
gpg -o message.txt -d encrypted.gpg
gpg --decrypt encrypted.gpg              # Afficher à l'écran
```

#### Signer et vérifier fichiers

```bash
# Signer fichier (format binaire compressé)
gpg --output message.sig --sign message.txt
gpg -o message.sig -s message.txt

# Signer (ASCII armored)
gpg --armor --output message.asc --sign message.txt

# Signature claire (texte lisible + signature)
gpg --clearsign message.txt             # → message.txt.asc
gpg --output message.asc --clearsign message.txt

# Signature détachée (signature séparée)
gpg --detach-sign message.txt           # → message.txt.sig
gpg --armor --detach-sign message.txt   # → message.txt.asc

# Vérifier signature
gpg --verify message.sig
gpg --verify message.txt.asc
gpg --verify message.txt.sig message.txt  # Signature détachée

# Déchiffrer et vérifier
gpg --output message.txt --decrypt message.sig
gpg -o message.txt -d message.sig
```

#### Chiffrer ET signer

```bash
# Chiffrer + signer
gpg --encrypt --sign --recipient bob --output message.gpg message.txt
gpg -e -s -r bob -o message.gpg message.txt

# Déchiffrer et vérifier signature
gpg --decrypt message.gpg
```

#### GPG-Agent

```bash
# Démarrer agent (souvent automatique)
gpg-agent --daemon

# Lister clés en cache
gpg-agent --help

# Arrêter agent
gpgconf --kill gpg-agent
```

#### Gestion des clés (--edit-key)

```bash
# Mode édition interactif
gpg --edit-key carol

# Commandes courantes
gpg> help                   # Aide
gpg> list                   # Lister clés
gpg> trust                  # Définir niveau confiance
gpg> sign                   # Signer clé
gpg> adduid                 # Ajouter USER-ID
gpg> deluid                 # Supprimer USER-ID
gpg> expire                 # Changer date expiration
gpg> passwd                 # Changer phrase de passe
gpg> save                   # Sauvegarder
gpg> quit                   # Quitter
```

---

## ✅ Checklist de révision

### 110.1 - Administration sécurité

- [ ] Je comprends SUID, SGID et sticky bit (4000, 2000, 1000)
- [ ] Je sais utiliser `find` avec `-perm` (valeur, -valeur, /valeur)
- [ ] Je maîtrise `passwd` (-l, -u, -e, -d, -S)
- [ ] Je maîtrise `chage` (-m, -M, -d, -W, -I, -E, -l)
- [ ] Je sais utiliser `lsof -i` pour ports/sockets
- [ ] Je sais utiliser `fuser -vn tcp PORT`
- [ ] Je maîtrise `netstat` (-l, -t, -u, -n, -e)
- [ ] Je sais scanner avec `nmap` (-p, -F, -v, -A)
- [ ] Je comprends `ulimit` (soft/hard, -S/-H, options ressources)
- [ ] Je sais utiliser `last`, `who`, `w`
- [ ] Je maîtrise différence `su` vs `sudo`
- [ ] Je sais configurer `/etc/sudoers` avec `visudo`
- [ ] Je comprends alias (Host_Alias, User_Alias, Cmnd_Alias)

### 110.2 - Configuration sécurité

- [ ] Je comprends `/etc/passwd` vs `/etc/shadow`
- [ ] Je sais utiliser `/etc/nologin` et `nologin` shell
- [ ] Je comprends concept super-démon (xinetd)
- [ ] Je sais configurer `/etc/xinetd.d/SERVICE`
- [ ] Je connais directives xinetd (disable, socket_type, protocol, wait, server)
- [ ] Je sais utiliser systemd.socket
- [ ] Je sais lister services (`service --status-all`, `systemctl list-units`)
- [ ] Je sais désactiver services (update-rc.d, chkconfig, systemctl disable)
- [ ] Je comprends TCP wrappers (`/etc/hosts.allow`, `/etc/hosts.deny`)
- [ ] Je sais vérifier support libwrap avec `ldd`

### 110.3 - Chiffrement données

- [ ] Je sais me connecter via SSH (`ssh user@host`)
- [ ] Je sais exécuter commande distante
- [ ] Je maîtrise génération clés SSH (`ssh-keygen -t TYPE -b SIZE`)
- [ ] Je connais algorithmes (RSA, DSA, ECDSA, Ed25519) et recommandations
- [ ] Je sais copier clé publique (`ssh-copy-id`, cat/ssh, scp)
- [ ] Je sais utiliser `ssh-agent` et `ssh-add`
- [ ] Je sais gérer `~/.ssh/known_hosts` (`ssh-keygen -R`)
- [ ] Je comprends clés hôte serveur (`/etc/ssh/ssh_host_*`)
- [ ] Je sais afficher empreintes (`ssh-keygen -l -f`)
- [ ] Je maîtrise tunnels SSH locaux (`-L`)
- [ ] Je maîtrise tunnels SSH distants (`-R`)
- [ ] Je comprends X11 forwarding (`-X`, `-x`)
- [ ] Je sais générer paire clés GPG (`gpg --gen-key`)
- [ ] Je connais structure `~/.gnupg/`
- [ ] Je sais exporter/importer clés (`--export`, `--import`, `--armor`)
- [ ] Je sais utiliser serveurs de clés (`--keyserver`, `--send-keys`, `--recv-keys`)
- [ ] Je sais révoquer clés (`--gen-revoke`, import certificat)
- [ ] Je maîtrise chiffrement/déchiffrement (`-e`, `-d`, `-r`, `-o`)
- [ ] Je maîtrise signature/vérification (`-s`, `--verify`, `--clearsign`, `--detach-sign`)
- [ ] Je connais `gpg-agent`

---

## 💻 Exercices pratiques

### Exercice 1 : Audit sécurité SUID/SGID

**Objectif** : Identifier fichiers avec permissions spéciales.

```bash
# 1. Trouver tous fichiers SUID dans /usr/bin
find /usr/bin -perm -4000 -ls

# 2. Trouver tous fichiers SGID dans /usr/bin
find /usr/bin -perm -2000 -ls

# 3. Trouver fichiers SUID OU SGID dans /usr/bin
find /usr/bin -perm /6000 -ls

# 4. Trouver fichiers SUID dans tout le système (attention à la sortie volumineuse)
sudo find / -perm -4000 2>/dev/null

# 5. Analyse
# - Sont-ils légitimes ?
# - Exemple légitime : /usr/bin/passwd (SUID root pour modifier /etc/shadow)
# - Exemple légitime : /usr/bin/sudo (SUID root)

# 6. Définir SGID sur répertoire partagé
mkdir ~/shared_project
chmod 2775 ~/shared_project
ls -ld ~/shared_project
# → drwxrwsr-x (le 's' dans groupe)

# 7. Tester héritage groupe
touch ~/shared_project/test_file
ls -l ~/shared_project/test_file
# → Groupe propriétaire = groupe du répertoire
```

---

### Exercice 2 : Gestion expiration mots de passe

**Objectif** : Configurer politique de mots de passe.

```bash
# Créer utilisateur test
sudo useradd -m alice

# 1. Définir mot de passe
sudo passwd alice

# 2. Afficher état
sudo passwd -S alice
sudo chage -l alice

# 3. Configurer politique stricte
sudo chage -m 1 alice          # Min 1 jour entre changements
sudo chage -M 90 alice         # Validité 90 jours
sudo chage -W 14 alice         # Avertissement 14 jours avant
sudo chage -I 7 alice          # Inactivité 7 jours après expiration

# 4. Forcer changement au prochain login
sudo chage -d 0 alice

# 5. Définir expiration compte
sudo chage -E 2025-12-31 alice

# 6. Vérifier configuration
sudo chage -l alice

# 7. Tester (se connecter en tant qu'alice)
su - alice
# → Demande changement mot de passe

# 8. Verrouiller compte
sudo passwd -l alice
sudo passwd -S alice           # → Statut 'L'

# 9. Déverrouiller
sudo passwd -u alice

# 10. Cleanup
sudo userdel -r alice
```

---

### Exercice 3 : Surveillance réseau et ports

**Objectif** : Identifier services réseau actifs.

```bash
# 1. Lister tous ports en écoute
sudo lsof -i -P
sudo netstat -tulnp
sudo ss -tulnp

# 2. Identifier processus sur port 22 (SSH)
sudo lsof -i :22
sudo fuser -vn tcp 22
sudo ss -tlnp | grep :22

# 3. Trouver tous ports TCP en écoute (format court)
sudo ss -tln | grep LISTEN
sudo netstat -tln | grep LISTEN

# 4. Scanner localhost
nmap localhost
nmap -p- localhost             # Tous ports
nmap -F localhost              # Fast scan
nmap -A localhost              # Aggressive

# 5. Scanner réseau local
nmap 192.168.1.0/24
nmap -sn 192.168.1.0/24        # Ping scan uniquement

# 6. Tester port spécifique
nmap -p 22,80,443 localhost
nc -vz localhost 22

# 7. Identifier services inutiles
systemctl list-units --type service --state running
# → Désactiver si inutile :
# sudo systemctl disable SERVICE --now
```

---

### Exercice 4 : Configuration sudo

**Objectif** : Créer politique sudo personnalisée.

```bash
# 1. Créer utilisateurs et groupes test
sudo useradd -m bob
sudo useradd -m alice
sudo groupadd webadmins
sudo usermod -aG webadmins bob

# 2. Éditer sudoers
sudo visudo

# 3. Ajouter configurations
# Alias
Host_Alias WEBSERVERS = localhost, 192.168.1.10
User_Alias WEBADMINS = bob, alice, %webadmins
Cmnd_Alias WEBSERVICES = /usr/bin/systemctl status apache2, \
                          /usr/bin/systemctl restart apache2

# Règle : WEBADMINS peut gérer services web sur WEBSERVERS sans mot de passe
WEBADMINS WEBSERVERS = NOPASSWD: WEBSERVICES

# Règle : alice peut tout faire
alice ALL=(ALL:ALL) ALL

# 4. Tester (en tant que bob)
su - bob
sudo systemctl status apache2  # → OK sans mot de passe
sudo systemctl stop apache2    # → Refusé (pas dans WEBSERVICES)

# 5. Vérifier logs sudo
sudo tail -f /var/log/auth.log | grep sudo

# 6. Cleanup
sudo userdel -r bob alice
sudo groupdel webadmins
```

---

### Exercice 5 : Authentification SSH par clé

**Objectif** : Configurer authentification par clé SSH.

```bash
# === Sur machine cliente ===

# 1. Générer clé Ed25519 (recommandé)
ssh-keygen -t ed25519 -C "mon_email@example.com"
# → Sauvegarder dans ~/.ssh/id_ed25519
# → Entrer phrase de passe forte

# 2. Générer clé RSA 4096 bits (alternative)
ssh-keygen -t rsa -b 4096 -C "mon_email@example.com"

# 3. Vérifier clés créées
ls -l ~/.ssh/
# → id_ed25519, id_ed25519.pub

# 4. Afficher empreinte
ssh-keygen -l -f ~/.ssh/id_ed25519.pub
ssh-keygen -lv -f ~/.ssh/id_ed25519.pub  # + art ASCII

# 5. Copier clé sur serveur
ssh-copy-id user@serveur.com
# → Entrer mot de passe (dernière fois)

# Méthode alternative manuelle
cat ~/.ssh/id_ed25519.pub | ssh user@serveur \
    'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'

# === Sur serveur ===

# 6. Vérifier authorized_keys
cat ~/.ssh/authorized_keys

# 7. Permissions correctes (important!)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

# === Retour sur client ===

# 8. Tester connexion
ssh user@serveur
# → Demande phrase de passe de la clé

# 9. Utiliser ssh-agent pour confort
eval $(ssh-agent)
ssh-add ~/.ssh/id_ed25519
# → Entrer phrase de passe UNE fois

# 10. Se connecter (sans redemander phrase)
ssh user@serveur

# 11. Lister clés chargées
ssh-add -l

# 12. Supprimer clés de l'agent
ssh-add -D

# === Sécurité avancée ===

# 13. Sur serveur : désactiver auth par mot de passe
sudo nano /etc/ssh/sshd_config
# → PasswordAuthentication no
# → PubkeyAuthentication yes

sudo systemctl restart sshd

# 14. Tester depuis autre machine (sans clé)
ssh user@serveur
# → Refusé (permission denied)
```

---

### Exercice 6 : Tunnels SSH

**Objectif** : Créer tunnels pour sécuriser connexions.

```bash
# === Tunnel local ===

# 1. Tunnel vers serveur web interne via bastion
ssh -L 8080:internal-server:80 -N bastion-host
# → En arrière-plan
ssh -L 8080:internal-server:80 -Nf bastion-host

# 2. Accéder au serveur interne
curl http://localhost:8080
firefox http://localhost:8080

# 3. Tunnels multiples
ssh -L 8080:server1:80 -L 8443:server2:443 -Nf bastion

# 4. Tunnel vers base de données
ssh -L 3307:db-server:3306 -Nf bastion
mysql -h 127.0.0.1 -P 3307 -u user -p

# === Tunnel distant ===

# 5. Exposer serveur local via serveur public
ssh -R 8080:localhost:80 -Nf user@public-server
# → Sur public-server, localhost:8080 → votre machine locale

# 6. Vérifier sur serveur distant
ssh user@public-server
curl http://localhost:8080

# 7. Autoriser accès externe (nécessite GatewayPorts yes sur serveur)
ssh -R 0.0.0.0:8080:localhost:80 -Nf user@public-server

# === X11 Forwarding ===

# 8. Lancer app graphique distante
ssh -X user@remote-server
firefox                        # S'affiche localement
gedit                          # Éditeur distant affiché localement

# === Gestion tunnels ===

# 9. Lister tunnels actifs
ps aux | grep "ssh -"
netstat -tlnp | grep ssh

# 10. Tuer tunnel
pkill -f "ssh -L 8080"
```

---

### Exercice 7 : GnuPG chiffrement et signature

**Objectif** : Maîtriser chiffrement et signatures GPG.

```bash
# === Configuration initiale ===

# 1. Générer paire de clés
gpg --full-generate-key
# → RSA (default)
# → 4096 bits
# → Expire dans 2 ans
# → Nom : Alice Dupont
# → Email : alice@example.com
# → Phrase de passe forte

# 2. Lister clés
gpg --list-keys
gpg --list-secret-keys

# 3. Afficher empreinte
gpg --fingerprint alice@example.com

# === Export/Import ===

# 4. Exporter clé publique (ASCII)
gpg --armor --export alice@example.com > alice_pub.asc

# 5. Exporter clé privée (backup sécurisé!)
gpg --armor --export-secret-keys alice@example.com > alice_priv.asc

# 6. Importer clé publique d'un correspondant
gpg --import bob_pub.asc

# 7. Publier sur serveur de clés
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID

# 8. Récupérer clé depuis serveur
gpg --keyserver keyserver.ubuntu.com --recv-keys KEY-ID

# === Chiffrement ===

# 9. Créer fichier test
echo "Informations confidentielles" > secret.txt

# 10. Chiffrer pour Bob
gpg --encrypt --recipient bob@example.com secret.txt
# → Crée secret.txt.gpg

# 11. Chiffrer (ASCII armored)
gpg --armor --encrypt --recipient bob secret.txt
# → Crée secret.txt.asc

# 12. Chiffrer pour plusieurs destinataires
gpg -e -r alice@example.com -r bob@example.com secret.txt

# 13. Déchiffrer
gpg --decrypt secret.txt.gpg > secret_decrypted.txt
gpg -d secret.txt.gpg          # Afficher à l'écran

# === Signature ===

# 14. Signer fichier
gpg --sign document.txt
# → Crée document.txt.gpg (compressé + signé, binaire)

# 15. Signer (ASCII armored)
gpg --armor --sign document.txt
# → Crée document.txt.asc

# 16. Signature claire (texte lisible)
gpg --clearsign document.txt
# → document.txt.asc (texte original + signature)

# 17. Signature détachée
gpg --detach-sign document.txt
# → document.txt.sig (signature séparée)

# 18. Vérifier signature
gpg --verify document.txt.gpg
gpg --verify document.txt.sig document.txt

# === Chiffrer ET signer ===

# 19. Chiffrer + signer
gpg --encrypt --sign --recipient bob@example.com message.txt

# 20. Déchiffrer et vérifier
gpg --decrypt message.txt.gpg

# === Révocation ===

# 21. Générer certificat de révocation
gpg --output revoke.asc --gen-revoke alice@example.com
# → Raison : 1 (clé compromise)

# 22. Révoquer clé (importer certificat)
gpg --import revoke.asc

# 23. Vérifier révocation
gpg --list-keys
# → uid [revoked]

# 24. Publier révocation
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID

# === Gestion avancée ===

# 25. Éditer clé
gpg --edit-key alice@example.com
# Commandes : trust, sign, adduid, expire, passwd, save, quit

# 26. Définir confiance
gpg --edit-key bob@example.com
gpg> trust
# → 5 (ultimate trust)
gpg> save
```

---

## 📚 Ressources complémentaires

### Pages de manuel essentielles

```bash
# Sécurité système
man find
man chmod
man passwd
man chage
man usermod

# Surveillance réseau
man lsof
man fuser
man netstat
man ss
man nmap

# Limites ressources
man bash                    # Pour ulimit
man limits.conf

# Connexions utilisateurs
man last
man who
man w

# Élévation privilèges
man su
man sudo
man sudoers
man visudo

# Configuration sécurité
man shadow
man nologin
man xinetd.conf
man hosts.allow
man hosts.deny

# SSH
man ssh
man ssh-keygen
man ssh-agent
man ssh-add
man ssh_config
man sshd_config

# GnuPG
man gpg
man gpg-agent
```

### Fichiers de configuration clés

```bash
# Sécurité utilisateurs
/etc/passwd                 # Comptes utilisateurs
/etc/shadow                 # Mots de passe cachés
/etc/group                  # Groupes
/etc/sudoers                # Configuration sudo
/etc/sudoers.d/*            # Fichiers sudo additionnels
/etc/security/limits.conf   # Limites ressources
/etc/nologin                # Bloquer connexions

# Services et démons
/etc/xinetd.conf            # Config xinetd principale
/etc/xinetd.d/*             # Config services xinetd
/etc/init.d/*               # Scripts init SysV
/etc/systemd/system/        # Units systemd

# TCP Wrappers
/etc/hosts.allow            # Règles autorisation
/etc/hosts.deny             # Règles blocage

# SSH client
~/.ssh/config               # Config client
~/.ssh/id_rsa               # Clé privée RSA
~/.ssh/id_rsa.pub           # Clé publique RSA
~/.ssh/id_ecdsa             # Clé privée ECDSA
~/.ssh/id_ecdsa.pub         # Clé publique ECDSA
~/.ssh/id_ed25519           # Clé privée Ed25519
~/.ssh/id_ed25519.pub       # Clé publique Ed25519
~/.ssh/authorized_keys      # Clés autorisées
~/.ssh/known_hosts          # Hôtes connus

# SSH serveur
/etc/ssh/sshd_config        # Config serveur
/etc/ssh/ssh_host_*_key     # Clés hôte privées
/etc/ssh/ssh_host_*_key.pub # Clés hôte publiques

# GnuPG
~/.gnupg/pubring.kbx        # Trousseau clés publiques
~/.gnupg/trustdb.gpg        # Base confiance
~/.gnupg/private-keys-v1.d/ # Clés privées
~/.gnupg/openpgp-revocs.d/  # Certificats révocation

# Logs
/var/log/auth.log           # Authentifications (Debian)
/var/log/secure             # Authentifications (Red Hat)
/var/log/wtmp               # Connexions utilisateurs (last)
```

### Commandes de référence rapide

```bash
# === PERMISSIONS SPÉCIALES ===
find / -perm /6000          # SUID ou SGID
chmod 4755 file             # SUID
chmod 2755 dir              # SGID
chmod 1777 /tmp             # Sticky bit

# === MOTS DE PASSE ===
passwd -S user              # Statut
passwd -l user              # Verrouiller
chage -l user               # Infos expiration
chage -M 90 user            # Validité 90 jours
chage -d 0 user             # Forcer changement

# === PORTS ET SOCKETS ===
lsof -i :PORT               # Processus sur port
fuser -vn tcp PORT          # Processus sur port
netstat -tulnp              # Tous ports écoute
ss -tulnp                   # Moderne
nmap -F localhost           # Scan rapide

# === UTILISATEURS CONNECTÉS ===
last                        # Historique connexions
who                         # Actuellement connectés
w                           # Connectés + activité

# === SUDO ===
visudo                      # Éditer sudoers
sudo -u user cmd            # Exécuter en tant que
sudo -i                     # Shell root

# === SSH ===
ssh-keygen -t ed25519       # Générer clé
ssh-copy-id user@host       # Copier clé
ssh -L 8080:dest:80 host    # Tunnel local
ssh -R 8080:dest:80 host    # Tunnel distant
ssh -X host                 # X11 forwarding

# === GPG ===
gpg --gen-key               # Générer paire
gpg -e -r user file         # Chiffrer
gpg -d file.gpg             # Déchiffrer
gpg -s file                 # Signer
gpg --verify file.sig       # Vérifier
```

---

## 🎯 Points clés pour l'examen

### À maîtriser absolument

**110.1 - Administration sécurité** :
- ✅ SUID (4000), SGID (2000), Sticky (1000)
- ✅ `find -perm` avec valeur, -valeur, /valeur
- ✅ `passwd -l/-u/-e/-d/-S`
- ✅ `chage -m/-M/-d/-W/-I/-E/-l`
- ✅ `lsof -i :PORT`, `fuser -vn tcp PORT`
- ✅ `netstat -tulnp` vs `ss -tulnp`
- ✅ `nmap -p PORT`, `nmap -F`
- ✅ `ulimit` soft (-S) vs hard (-H)
- ✅ `last`, `who`, `w`
- ✅ `su -` vs `sudo -u`
- ✅ `/etc/sudoers` avec `visudo`

**110.2 - Configuration sécurité** :
- ✅ `/etc/passwd` (7 champs) vs `/etc/shadow`
- ✅ `/etc/nologin` (fichier) vs `/sbin/nologin` (shell)
- ✅ xinetd : `/etc/xinetd.d/SERVICE`
- ✅ Directives xinetd : disable, socket_type, protocol, server
- ✅ systemd.socket : `systemctl start SERVICE.socket`
- ✅ `service --status-all`, `systemctl list-units`
- ✅ TCP wrappers : `/etc/hosts.allow`, `/etc/hosts.deny`
- ✅ `ldd /usr/sbin/DAEMON | grep libwrap`

**110.3 - Chiffrement** :
- ✅ `ssh user@host`, `ssh user@host commande`
- ✅ `ssh-keygen -t TYPE -b SIZE`
- ✅ Algorithmes : Ed25519 (meilleur), ECDSA, RSA, DSA (déprécié)
- ✅ `ssh-copy-id user@host`
- ✅ `ssh-agent`, `ssh-add`
- ✅ `~/.ssh/authorized_keys`, `~/.ssh/known_hosts`
- ✅ `/etc/ssh/ssh_host_*_key`
- ✅ Tunnel local : `ssh -L port_local:dest:port_dest host`
- ✅ Tunnel distant : `ssh -R port_distant:dest:port_dest host`
- ✅ X11 : `ssh -X host`
- ✅ `gpg --gen-key`, `gpg --list-keys`
- ✅ `gpg --export/-import`
- ✅ `gpg -e -r user file`, `gpg -d file.gpg`
- ✅ `gpg -s file`, `gpg --verify file.sig`

### Pièges courants à éviter

❌ Confondre `find -perm 4000` (exclusif) et `find -perm -4000` (+ autres permissions)  
❌ Oublier que SUID sur script shell ne fonctionne pas (sécurité)  
❌ Confondre `passwd -l` (verrouiller) et `passwd -e` (forcer expiration)  
❌ Oublier que `chage -M 0` n'expire PAS le mot de passe (utiliser 99999 pour désactiver)  
❌ Confondre `netstat` (obsolète) et `ss` (moderne)  
❌ Oublier que hard limits ne peuvent être augmentées que par root  
❌ Éditer `/etc/sudoers` directement au lieu d'utiliser `visudo`  
❌ Oublier le `-` dans `su -` (charge environnement)  
❌ Confondre `/etc/nologin` (fichier temporaire) et `/sbin/nologin` (shell permanent)  
❌ Oublier que DSA est déprécié depuis OpenSSH 7.0  
❌ Confondre tunnel local (`-L`) et distant (`-R`)  
❌ Oublier `-N` pour tunnel sans shell interactif  
❌ Confondre `--export` (publique) et `--export-secret-keys` (privée)  
❌ Oublier `--armor` pour ASCII (emails)  

### Astuces pour l'examen

⏱️ **Gestion du temps** : Ce sujet vaut 12 points, allouez ~25-30 minutes  
🔐 **Sécurité** : Toujours vérifier permissions (600 pour clés privées, 644 pour publiques)  
📝 **Syntaxe** : Connaître options courtes (-e, -d, -s) ET longues (--encrypt, --decrypt, --sign)  
🎯 **Priorités** : 110.3 (6 pts) > 110.1 (3 pts) = 110.2 (3 pts)  
🧪 **Pratique** : Créer lab virtuel et tester TOUS les scénarios  
📋 **Mémorisation** : SUID=4000, SGID=2000, Sticky=1000  

### Distribution des points par difficulté

- **Facile (40%)** : Commandes de base (passwd, chage, lsof, ssh, gpg --gen-key)
- **Moyen (45%)** : Configuration (sudoers, xinetd, tunnels SSH, chiffrement GPG)
- **Difficile (15%)** : Scénarios complexes (alias sudoers, tunnels multiples, révocation GPG)

---

**Bon courage pour votre préparation ! 🔐**

*La sécurité est fondamentale : maîtrisez ces concepts pour protéger vos systèmes !*
