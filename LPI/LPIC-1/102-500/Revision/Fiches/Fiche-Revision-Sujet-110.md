# 📄 Fiche Sujet 110 : Sécurité

**Poids : 12 points (20%)** | Révision rapide

---

## 110.1 : Tâches d'administration de sécurité (3 pts)

### Permissions spéciales
```bash
# SUID (4000) : exécute avec droits propriétaire
chmod 4755 fichier              # ou chmod u+s
find / -perm -4000              # Trouver fichiers SUID

# SGID (2000) : exécute avec droits groupe / héritage groupe (dir)
chmod 2755 répertoire           # ou chmod g+s
find / -perm -2000              # Trouver SGID

# Sticky bit (1000) : seulement proprio peut supprimer (dir)
chmod 1777 /tmp                 # ou chmod +t
find / -perm -1000              # Trouver sticky

# Combinaisons
chmod 6755 fichier              # SUID + SGID
find / -perm /6000              # SUID OU SGID (/)
find / -perm -6000              # SUID ET SGID (-)

# Symbolique
rws = SUID avec exécution       rwS = SUID sans exécution
rws = SGID avec exécution       rwS = SGID sans exécution
rwt = Sticky avec exécution     rwT = Sticky sans exécution
```

### Gestion mots de passe
```bash
# passwd
passwd user                     # Changer mot de passe
passwd -l user                  # Lock (verrouiller)
passwd -u user                  # Unlock (déverrouiller)
passwd -e user                  # Expire (forcer changement)
passwd -d user                  # Delete password
passwd -S user                  # Status (7 champs)

# chage (change age)
chage -l user                   # Liste infos
chage -m 1 user                 # Min 1 jour entre changements
chage -M 90 user                # Max 90 jours validité
chage -W 14 user                # Warning 14 jours avant
chage -I 7 user                 # Inactive 7 jours après expiration
chage -E 2027-12-31 user        # Expire compte à date
chage -d 0 user                 # Forcer changement au login

# usermod
usermod -L user                 # Lock
usermod -U user                 # Unlock
usermod -e 2027-12-31 user      # Expiration
usermod -f 7 user               # Jours inactivité
```

### Surveillance réseau
```bash
# lsof (list open files)
lsof -i                         # Tous fichiers Internet
lsof -i :80                     # Port 80
lsof -i :22-25                  # Plage ports
lsof -i@192.168.1.100           # Connexions vers IP
lsof -i4                        # IPv4 uniquement
lsof -i6                        # IPv6 uniquement

# fuser (file user)
fuser -v /home                  # Qui utilise /home
fuser -vn tcp 80                # Processus port TCP 80
fuser -k -n tcp 80              # Kill processus port 80

# netstat (obsolète, utiliser ss)
netstat -tulpn                  # Ports écoute
# -t TCP, -u UDP, -l listening, -p PID, -n numérique

# ss (socket statistics, moderne)
ss -tulpn                       # Ports écoute
ss -tunap                       # Toutes connexions

# nmap
nmap localhost                  # Scan localhost
nmap 192.168.1.0/24             # Scan réseau
nmap -p 22,80,443 host          # Ports spécifiques
nmap -p- host                   # Tous ports (65535)
nmap -F host                    # Fast scan (100 ports)
nmap -sV host                   # Version services
nmap -A host                    # Agressif (OS, version, scripts)
```

### Limites ressources
```bash
# ulimit (user limits)
ulimit -a                       # Toutes limites soft
ulimit -Ha                      # Toutes limites hard
ulimit -u                       # Max processus (soft)
ulimit -Hu                      # Max processus (hard)
ulimit -f                       # Max taille fichier (blocs)
ulimit -n                       # Max fichiers ouverts
ulimit -v                       # Max mémoire virtuelle
ulimit -m                       # Max RSS

# Définir limites
ulimit -u 100                   # Soft limit 100 processus
ulimit -Hu 200                  # Hard limit 200 processus
ulimit -Sf 1000                 # Soft file size 1000 blocs

# Règles
# - User peut réduire hard limit
# - User peut augmenter soft jusqu'à hard
# - Seul root peut augmenter hard limit

# Persistance
/etc/security/limits.conf
# Format: domain type item value
user soft nproc 100
@group hard nofile 4096
* soft core 0
```

### Utilisateurs connectés
```bash
# last
last                            # Historique connexions
last -n 10                      # 10 dernières
last user                       # Connexions user
last reboot                     # Redémarrages
lastb                           # Échecs connexion

# who
who                             # Utilisateurs actuels
who -H                          # Avec en-têtes
who -b                          # Dernier boot
who -r                          # Runlevel

# w
w                               # Users + activité
# Colonnes: USER, TTY, FROM, LOGIN@, IDLE, JCPU, PCPU, WHAT
# JCPU = tous processus TTY
# PCPU = processus actuel
```

### su et sudo
```bash
# su (switch user)
su                              # Devenir root (garde env)
su -                            # Devenir root (charge env root)
su - user                       # Devenir user (avec env)
su -c "commande" user           # Exécuter commande comme user

# sudo
sudo commande                   # Exécuter comme root
sudo -u user commande           # Comme autre user
sudo -i                         # Shell root interactif
sudo -s                         # Shell avec env user
sudo -l                         # Lister privilèges
sudo -k                         # Invalider cache credentials

# /etc/sudoers (TOUJOURS avec visudo!)
visudo                          # Éditer sudoers

# Format: user hosts=(runas) commands
root ALL=(ALL:ALL) ALL
%sudo ALL=(ALL:ALL) ALL         # Groupe sudo
user ALL=(ALL) NOPASSWD: /usr/bin/systemctl status *

# Alias
Host_Alias SERVERS = server1, server2
User_Alias ADMINS = alice, bob, %sysadmin
Cmnd_Alias SERVICES = /usr/bin/systemctl *

ADMINS SERVERS = SERVICES
```

---

## 110.2 : Configuration de la sécurité du système (3 pts)

### Shadow passwords
```bash
# Fichiers
/etc/passwd                     # 7 champs (login:x:UID:GID:GECOS:home:shell)
/etc/shadow                     # 9 champs (mot de passe haché)
/etc/group                      # Groupes
/etc/gshadow                    # Mots de passe groupes

# /etc/shadow format
# name:hash:lastchange:min:max:warn:inactive:expire:reserved
# hash : $6$ = SHA-512, $5$ = SHA-256, $1$ = MD5
# ! ou !! = compte verrouillé
```

### Prévention connexions
```bash
# /etc/nologin : bloque tous users sauf root (temporaire)
echo "Maintenance en cours" > /etc/nologin
rm /etc/nologin                 # Réactiver

# /sbin/nologin : shell pour bloquer user (permanent)
usermod -s /sbin/nologin user
# Aussi: /bin/false
```

### xinetd (super-daemon)
```bash
# Config
/etc/xinetd.conf                # Principal
/etc/xinetd.d/*                 # Par service

# Exemple /etc/xinetd.d/ssh
service ssh
{
    disable         = no        # yes = désactivé
    socket_type     = stream    # stream=TCP, dgram=UDP
    protocol        = tcp
    wait            = no        # no pour TCP multi-thread
    user            = root
    server          = /usr/sbin/sshd
    server_args     = -i
    interface       = 192.168.1.1
}

systemctl restart xinetd
```

### systemd.socket (alternative moderne)
```bash
systemctl start ssh.socket      # Démarrer socket
systemctl enable sshd.socket    # Activer au boot
lsof -i :22                     # Vérifier (PID 1 = systemd)
```

### Gestion services
```bash
# systemd
systemctl list-units --type service --state active
systemctl disable service --now # Désactiver + arrêter

# SysV-init (ancien)
service --status-all            # Tous services
update-rc.d service remove      # Debian
chkconfig service off           # Red Hat
```

### TCP Wrappers (legacy, obsolète)
```bash
# Vérifier support
ldd /usr/sbin/sshd | grep libwrap

# Fichiers (ordre: allow → deny)
/etc/hosts.allow                # Autorisations
/etc/hosts.deny                 # Blocages

# Format: daemon: client_list
sshd: ALL                       # Dans hosts.deny = bloquer tout
sshd: 192.168.1.                # Dans hosts.allow = autoriser réseau
sshd: LOCAL                     # Réseau local
sshd: ALL EXCEPT 192.168.1.100  # Tout sauf IP
```

---

## 110.3 : Sécurisation des données avec le chiffrement (6 pts)

### SSH - Connexion
```bash
# Basique
ssh user@host                   # Connexion
ssh user@host commande          # Exécuter commande
ssh -p 2222 user@host           # Port non-standard

# Première connexion
# Vérifier empreinte ECDSA/ED25519
# Ajouté à ~/.ssh/known_hosts

# Retirer hôte
ssh-keygen -R hostname
ssh-keygen -R 192.168.1.10
```

### SSH - Clés
```bash
# Génération
ssh-keygen                      # RSA 2048 par défaut
ssh-keygen -t ed25519           # Ed25519 (RECOMMANDÉ)
ssh-keygen -t rsa -b 4096       # RSA 4096
ssh-keygen -t ecdsa -b 521      # ECDSA 521

# Algorithmes
Ed25519 : 256 bits, MEILLEUR sécurité
ECDSA   : 256/384/521 bits, très bon
RSA     : 2048-4096 bits, bon, compatible
DSA     : 1024 bits, DÉPRÉCIÉ, ÉVITER

# Fichiers
~/.ssh/id_ed25519               # Clé privée (600)
~/.ssh/id_ed25519.pub           # Clé publique (644)

# Copier clé publique
ssh-copy-id user@host           # Automatique (recommandé)
cat ~/.ssh/id_ed25519.pub | ssh user@host 'cat >> .ssh/authorized_keys'

# Serveur
~/.ssh/authorized_keys          # Clés autorisées (600)
```

### ssh-agent
```bash
# Démarrer agent
ssh-agent /bin/bash             # Nouveau shell avec agent
eval $(ssh-agent)               # Shell actuel

# Ajouter clé
ssh-add                         # Clé par défaut
ssh-add ~/.ssh/id_ed25519       # Clé spécifique
ssh-add -l                      # Lister clés chargées
ssh-add -D                      # Supprimer toutes clés

# Utilisation
# Entrer passphrase UNE FOIS, puis connexions sans passphrase
```

### Clés hôte serveur
```bash
# Localisation
/etc/ssh/ssh_host_*_key         # Privées (600, root)
/etc/ssh/ssh_host_*_key.pub     # Publiques (644)

# Types (4 paires par serveur)
ssh_host_rsa_key
ssh_host_dsa_key
ssh_host_ecdsa_key
ssh_host_ed25519_key

# Afficher empreinte
ssh-keygen -l -f /etc/ssh/ssh_host_ed25519_key.pub
ssh-keygen -lv -f FILE          # + art ASCII
```

### Tunnels SSH
```bash
# Local (-L) : port local → destination via intermédiaire
ssh -L 8080:dest:80 user@bastion
# Accès: localhost:8080 → bastion → dest:80

# Distant (-R) : port distant → destination via local
ssh -R 8080:localhost:80 user@serveur_public
# serveur_public:8080 → votre localhost:80

# Options
-N                              # Pas de shell (tunnel seul)
-f                              # Arrière-plan
-L 8080:dest:80 -L 8443:dest:443 # Multiples tunnels

# X11 forwarding
ssh -X user@host                # Activer X11
ssh -x user@host                # Désactiver X11
# Config serveur: X11Forwarding yes dans /etc/ssh/sshd_config
```

### GnuPG - Clés
```bash
# Génération
gpg --gen-key                   # Basique
gpg --full-generate-key         # Options complètes

# Lister
gpg --list-keys                 # Clés publiques
gpg --list-secret-keys          # Clés privées
gpg --fingerprint USER-ID       # Empreinte
gpg -k                          # Court pour list-keys
gpg -K                          # Court pour list-secret-keys

# Structure ~/.gnupg/
pubring.kbx                     # Trousseau public
trustdb.gpg                     # Base confiance
private-keys-v1.d/              # Clés privées
openpgp-revocs.d/               # Certificats révocation
```

### GnuPG - Export/Import
```bash
# Export public
gpg --export user@example.com > public.key
gpg --armor --export user > public.asc      # ASCII
gpg -a --export user > public.asc           # Court

# Export privé (BACKUP!)
gpg --armor --export-secret-keys user > private.asc

# Import
gpg --import public.asc
gpg --import private.asc

# Serveurs de clés
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID
gpg --keyserver keyserver.ubuntu.com --recv-keys KEY-ID
```

### GnuPG - Chiffrement
```bash
# Chiffrer
gpg --encrypt --recipient user file
gpg -e -r user file             # Court
gpg -a -e -r user file          # ASCII
gpg -e -r alice -r bob file     # Multi destinataires
gpg -o output.gpg -e -r user file

# Déchiffrer
gpg --decrypt file.gpg          # Afficher
gpg -d file.gpg                 # Court
gpg -o clear.txt -d file.gpg    # Vers fichier
```

### GnuPG - Signature
```bash
# Signer
gpg --sign file                 # Binaire compressé
gpg -s file                     # Court
gpg -a --sign file              # ASCII
gpg --clearsign file            # Texte lisible + signature
gpg --detach-sign file          # Signature séparée (.sig)

# Vérifier
gpg --verify file.sig
gpg --verify file.sig original  # Signature détachée

# Chiffrer + signer
gpg -e -s -r user file
gpg --encrypt --sign --recipient user file
```

### GnuPG - Révocation
```bash
# Générer certificat
gpg --output revoke.asc --gen-revoke user@example.com
# Raisons: 0=aucune, 1=compromise, 2=remplacée, 3=plus utilisée

# Révoquer
gpg --import revoke.asc
gpg --list-keys                 # Voir [revoked]

# Distribuer clé révoquée
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID
```

---

## 🎯 Points clés examen

### Must know
- ✅ SUID=4000, SGID=2000, Sticky=1000
- ✅ `find / -perm -4000` (SUID), `/6000` (SUID OU SGID)
- ✅ `passwd -l/-u/-e`, `chage -M/-m/-W/-I/-E/-d`
- ✅ `lsof -i :PORT`, `fuser -vn tcp PORT`, `ss -tulpn`
- ✅ `ulimit -a/-Ha`, soft vs hard limits
- ✅ `/etc/sudoers` avec `visudo`, `NOPASSWD:`
- ✅ `/etc/passwd` (7 champs), `/etc/shadow` (9 champs)
- ✅ `ssh-keygen -t ed25519` (recommandé)
- ✅ `ssh-copy-id`, `ssh-agent`, `ssh-add`
- ✅ Tunnels : `-L` (local), `-R` (distant), `-X` (X11)
- ✅ `gpg --gen-key`, `-e -r` (encrypt), `-d` (decrypt)
- ✅ `gpg -s` (sign), `--verify` (vérifier)

### Pièges
- ❌ `find -perm 4000` (exact) vs `-perm -4000` (+ autres)
- ❌ Ne JAMAIS éditer `/etc/sudoers` sans `visudo`
- ❌ DSA déprécié, préférer Ed25519 ou RSA ≥2048
- ❌ Oublier `-a` pour export GPG ASCII (binaire par défaut)
- ❌ Permissions SSH : privée 600, publique 644

### Astuces rapides
```bash
# Audit SUID system
find / -perm /6000 -type f 2>/dev/null

# Forcer changement password au login
chage -d 0 user

# Voir ports écoute
ss -tulpn

# SSH Ed25519 + agent
ssh-keygen -t ed25519
ssh-copy-id user@host
ssh-agent /bin/bash
ssh-add

# Tunnel local
ssh -L 8080:internal:80 -Nf bastion

# GPG encrypt + sign
gpg -a -e -s -r alice file.txt

# GPG verify + decrypt
gpg --verify file.gpg
gpg -o clear.txt -d file.gpg
```

---

**💡 Conseil :** Sujet CRUCIAL (12 pts, 20% exam). Maîtrisez permissions spéciales, `chage`, `sudoers`, SSH (Ed25519 + tunnels), et GPG (encrypt/sign/verify).
