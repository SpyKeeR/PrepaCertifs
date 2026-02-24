# 📄 Fiche Master : Commandes Essentielles LPIC-1 102-500

**Référence complète** | Tous sujets (105-110)

---

## 🐚 Shells et Scripts (105)

```bash
# Variables environnement
export VAR=valeur               # Créer variable globale
env                             # Afficher variables
printenv HOME
unset VAR                       # Supprimer

# Principales variables
$PATH $HOME $USER $SHELL $PWD $OLDPWD $PS1 $LANG

# Fichiers config
/etc/profile                    # Système login
~/.bash_profile                 # User login
~/.bashrc                       # User non-login
~/.bash_logout                  # Déconnexion

# Scripts
$0 $1 $2 $# $@ $? $$           # Arguments et codes
[ -f file ]                     # Test fichier
[ $a -eq $b ]                   # Test numérique
for i in {1..10}; do echo $i; done
while [ condition ]; do cmd; done

```

---

## 🖥️ Interfaces Graphiques (106)

```bash
# X11
$DISPLAY                        # :0 (local)
xhost +hostname                 # Autoriser affichage
startx                          # Démarrer X
xrandr                          # Config écrans

# Display managers
gdm3, lightdm, sddm, xdm
systemctl status gdm3

# Desktop environments
GNOME, KDE, XFCE, LXDE, MATE, Cinnamon

# Accessibilité
orca                            # Lecteur écran
onboard                         # Clavier virtuel
```

---

## 👥 Utilisateurs et Tâches (107)

```bash
# Users
useradd -m -s /bin/bash user    # Créer avec home
usermod -aG sudo user           # Ajouter à groupe
usermod -L user                 # Lock
userdel -r user                 # Supprimer + home
passwd -l/-u/-e user            # Lock/unlock/expire
chage -l user                   # Infos expiration
chage -M 90 user                # Validité 90 jours
chage -d 0 user                 # Forcer changement
id user                         # UID, GID, groupes
groups user                     # Groupes
last                            # Historique connexions
w                               # Users + activité

# Groups
groupadd groupe
usermod -aG groupe user         # APPEND!
groupdel groupe

# Fichiers
/etc/passwd                     # Users (7 champs)
/etc/shadow                     # Passwords (9 champs)
/etc/group                      # Groupes
/etc/skel/                      # Squelette home

# Cron
crontab -e                      # Éditer crontab
crontab -l                      # Lister
# min heure jour mois jour_semaine commande
0 2 * * *       /backup.sh      # 2h00 tous jours
*/15 * * * *    /check.sh       # Toutes 15 min
@daily          /script.sh      # Minuit
@reboot         /startup.sh     # Au boot

/etc/cron.d/                    # Tâches système
/etc/cron.daily/                # Scripts quotidiens
/etc/cron.allow                 # Users autorisés

# at
at 14:30                        # Tâche unique
at now + 2 hours
atq                             # Liste tâches
atrm 5                          # Supprimer tâche

# Locale
locale                          # Afficher locale
locale -a                       # Disponibles
export LANG=fr_FR.UTF-8
localectl set-locale LANG=fr_FR.UTF-8
timedatectl set-timezone Europe/Paris
timedatectl set-ntp true        # NTP
```

---

## ⏰ Services Système (108)

```bash
# Date/Heure
date                            # Date système
date +%Y-%m-%d                  # Format custom
hwclock                         # Horloge matérielle
hwclock --hctosys               # RTC → système
hwclock --systohc               # Système → RTC
timedatectl                     # Infos complètes
timedatectl set-time "14:30:00"
timedatectl set-timezone Europe/Paris
timedatectl set-ntp true        # Activer NTP

# NTP
systemctl status systemd-timesyncd
ntpq -p                         # Serveurs (ntpd)
chronyc sources                 # Serveurs (chronyd)

# Logs
/var/log/syslog                 # Général (Debian)
/var/log/messages               # Général (Red Hat)
/var/log/auth.log               # Auth (Debian)
/var/log/secure                 # Auth (Red Hat)

tail -f /var/log/syslog         # Suivi temps réel
grep "error" /var/log/syslog

# journalctl (systemd)
journalctl                      # Tous logs
journalctl -f                   # Temps réel
journalctl -u service           # Service spécifique
journalctl -b                   # Boot actuel
journalctl -b -1                # Boot précédent
journalctl -k                   # Kernel
journalctl -p err               # Priorité err+
journalctl --since "1 hour ago"
journalctl --since "2026-01-28"

# rsyslog
/etc/rsyslog.conf
# facility.priority action
mail.*          /var/log/mail.log
*.emerg         *

# Priorities
debug < info < notice < warn < err < crit < alert < emerg

# logger
logger "Message test"
logger -p user.warn "Attention"
logger -t script "Info"

# logrotate
/etc/logrotate.conf
/etc/logrotate.d/
logrotate -f /etc/logrotate.conf

# Mail (Postfix)
systemctl status postfix
mailq                           # Voir queue
postqueue -f                    # Forcer envoi
postsuper -d ALL                # Vider queue
/etc/aliases                    # Aliases mail
newaliases                      # Régénérer DB
~/.forward                      # Redirection user
```

---

## 🌐 Réseaux (109)

```bash
# IPv4
Classes A/B/C
Privés: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
CIDR: /24=256 IPs, /30=4 IPs

# IPv6
::1                             # Loopback
fe80::/10                       # Link-local
fc00::/7                        # Privé

# Ports
22 SSH, 25 SMTP, 53 DNS, 80 HTTP, 110 POP3, 
143 IMAP, 443 HTTPS, 3306 MySQL, 5432 PostgreSQL

# NetworkManager
nmcli                           # Infos
nmcli con show                  # Connexions
nmcli device status             # Interfaces
nmcli con up/down connexion
nmcli con add type ethernet ifname eth0 \
  con-name static ip4 192.168.1.100/24 \
  gw4 192.168.1.1
nmtui                           # Interface texte

# ip (moderne)
ip addr show                    # Adresses
ip a                            # Court
ip addr add 192.168.1.100/24 dev eth0
ip addr del 192.168.1.100/24 dev eth0
ip link set eth0 up/down
ip route show                   # Routes
ip r                            # Court
ip route add default via 192.168.1.1
ip route add 10.0.0.0/8 via 192.168.1.254
ip route del default
ip route get 8.8.8.8            # Route vers IP

# DNS
/etc/resolv.conf                # Serveurs DNS
# nameserver 8.8.8.8
/etc/hosts                      # Résolution locale
/etc/nsswitch.conf              # Ordre résolution

# Hostname
hostname                        # Afficher
hostname -f                     # FQDN
hostnamectl                     # Infos complètes
hostnamectl set-hostname server.example.com

# Diagnostic
ping -c 4 8.8.8.8
ping6 ::1
traceroute google.com
mtr google.com                  # Ping + trace
host google.com                 # DNS simple
dig google.com                  # DNS détaillé
dig +short google.com
dig @8.8.8.8 google.com         # Serveur spécifique
nslookup google.com

# Ports
ss -tulpn                       # Moderne
netstat -tulpn                  # Obsolète
nc -zv host 80                  # Test port

# ARP
ip neigh                        # Table ARP
arp -a                          # Obsolète

# Interface stats
ip -s link
ethtool eth0
```

---

## 🔐 Sécurité (110)

```bash
# Permissions spéciales
chmod 4755 file                 # SUID (4000)
chmod 2755 dir                  # SGID (2000)
chmod 1777 /tmp                 # Sticky (1000)
find / -perm -4000              # Trouver SUID
find / -perm /6000              # SUID OU SGID

# Passwords
passwd -l user                  # Lock
passwd -u user                  # Unlock
passwd -e user                  # Expire
passwd -S user                  # Status
chage -l user                   # Liste infos
chage -M 90 user                # Max 90 jours
chage -W 14 user                # Warning 14j
chage -I 7 user                 # Inactive 7j
chage -E 2027-12-31 user        # Expire compte
chage -d 0 user                 # Forcer changement

# Surveillance ports
lsof -i                         # Tous ports
lsof -i :80                     # Port spécifique
fuser -vn tcp 80                # Processus port 80
fuser -k -n tcp 80              # Kill processus
ss -tulpn                       # Ports écoute
nmap localhost                  # Scan local
nmap -F host                    # Fast scan
nmap -sV host                   # Version services

# Limites
ulimit -a                       # Toutes limites soft
ulimit -Ha                      # Toutes limites hard
ulimit -u 100                   # Max 100 processus
/etc/security/limits.conf       # Persistant

# Users connectés
last                            # Historique
last -n 10
who                             # Actuels
w                               # Actuels + activité

# sudo
visudo                          # Éditer sudoers
sudo -l                         # Lister privilèges
sudo -u user cmd                # Exécuter comme user
sudo -i                         # Shell root
# /etc/sudoers:
# user ALL=(ALL) NOPASSWD: /cmd

# Fichiers
/etc/passwd                     # 7 champs
/etc/shadow                     # 9 champs
/etc/nologin                    # Bloquer connexions (temp)
usermod -s /sbin/nologin user   # Bloquer user (perm)

# Services
systemctl list-units --type service --state active
systemctl disable service --now
ss -tulpn                       # Ports écoute

# SSH connexion
ssh user@host
ssh -p 2222 user@host           # Port custom
ssh user@host commande          # Exécuter commande

# SSH clés
ssh-keygen -t ed25519           # Générer (RECOMMANDÉ)
ssh-keygen -t rsa -b 4096       # RSA 4096
ssh-copy-id user@host           # Copier clé
~/.ssh/authorized_keys          # Sur serveur
~/.ssh/known_hosts              # Hôtes connus
ssh-keygen -R hostname          # Retirer hôte

# ssh-agent
ssh-agent /bin/bash             # Démarrer agent
ssh-add                         # Ajouter clé
ssh-add -l                      # Lister clés
ssh-add -D                      # Supprimer clés

# Clés hôte serveur
/etc/ssh/ssh_host_*_key         # Privées (600)
/etc/ssh/ssh_host_*_key.pub     # Publiques (644)
ssh-keygen -l -f key.pub        # Empreinte

# Tunnels SSH
ssh -L 8080:dest:80 bastion     # Local
ssh -R 8080:localhost:80 remote # Distant
ssh -X user@host                # X11 forwarding
-N                              # Pas de shell
-f                              # Arrière-plan

# GnuPG clés
gpg --gen-key                   # Générer paire
gpg --list-keys                 # Lister publiques
gpg --list-secret-keys          # Lister privées
gpg --fingerprint user          # Empreinte

# Export/Import
gpg --export user > pub.key     # Export public
gpg -a --export user > pub.asc  # ASCII
gpg -a --export-secret-keys     # Export privé
gpg --import key.asc            # Import

# Serveurs clés
gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID
gpg --keyserver keyserver.ubuntu.com --recv-keys KEY-ID

# Chiffrement
gpg -e -r user file             # Encrypt
gpg -a -e -r user file          # ASCII
gpg -e -r alice -r bob file     # Multi destinataires
gpg -d file.gpg                 # Decrypt
gpg -o clear.txt -d file.gpg    # Vers fichier

# Signature
gpg -s file                     # Sign
gpg -a --clearsign file         # Texte lisible
gpg --detach-sign file          # Signature séparée
gpg --verify file.sig           # Vérifier

# Encrypt + Sign
gpg -a -e -s -r user file

# Révocation
gpg --gen-revoke user           # Générer certificat
gpg --import revoke.asc         # Révoquer
```

---

## 🎯 Commandes par fréquence à l'examen

### Très fréquent (maîtriser absolument)
```bash
# User management
useradd -m, usermod -aG, passwd -l/-e, chage -M/-d
id, groups, last, w

# Cron
crontab -e/-l, format: min heure jour mois jour_sem cmd
*/15 * * * *, @daily, @reboot

# Logs
journalctl -u/-f/-b/-k/-p, tail -f /var/log/syslog

# Réseau
ip addr, ip route, nmcli con show/up/down
ping, dig, ss -tulpn
/etc/resolv.conf, /etc/hosts

# Sécurité
find -perm -4000, chmod u+s/g+s/+t
lsof -i, fuser -vn tcp, nmap
ssh-keygen -t ed25519, ssh-copy-id
gpg -e -r, gpg -d, gpg -s
visudo, sudo -l

# Date/Time
timedatectl set-time/set-timezone/set-ntp
hwclock --hctosys/--systohc
```

### Fréquent (bien connaître)
```bash
# Scripts
$1-$9, $#, $@, $?, $$
[ -f ], [ -d ], [ $a -eq $b ]
for, while, if-then-fi

# Locale
locale, locale -a, localectl
export LANG=fr_FR.UTF-8

# Mail
mailq, postqueue -f, postsuper -d ALL
/etc/aliases, newaliases

# Services
systemctl status/enable/disable
systemctl list-units --type service
```

### Occasionnel (connaître existence)
```bash
# X11
$DISPLAY, xhost, xrandr, startx
gdm3, lightdm

# Accessibilité
orca, onboard

# xinetd
/etc/xinetd.d/, systemctl restart xinetd

# TCP Wrappers (obsolète)
/etc/hosts.allow, /etc/hosts.deny

```

---

## 💡 Astuces mémo rapides

### Ordre priorité fichiers config
```
Login shell:
/etc/profile → ~/.bash_profile → ~/.bash_login → ~/.profile

Non-login shell:
/etc/bash.bashrc → ~/.bashrc
```

### Tests shell
```bash
-f fichier    -d répertoire    -e existe    -r lisible
-w modifiable -x exécutable    -s non vide
-z vide       -n non vide      = égal       != différent
-eq égal      -ne différent    -lt <        -gt >
-le ≤         -ge ≥
```

### Crontab format
```
min heure jour mois jour_semaine commande
 *   *     *    *    *
 0-59 0-23 1-31 1-12 0-7 (0 et 7 = dimanche)

Exemples:
0 2 * * *       Tous jours 2h00
*/15 * * * *    Toutes 15 min
0 0 * * 1       Lundi 0h00
```

### rsyslog priorities
```
debug < info < notice < warn < err < crit < alert < emerg
```

### Réseaux privés
```
10.0.0.0/8        Classe A
172.16.0.0/12     16 réseaux B
192.168.0.0/16    256 réseaux C
```

### CIDR rapide
```
/24 = 256 IPs (254 hôtes)
/25 = 128 IPs (126 hôtes)
/26 = 64 IPs (62 hôtes)
/27 = 32 IPs (30 hôtes)
/28 = 16 IPs (14 hôtes)
/30 = 4 IPs (2 hôtes, point-à-point)
```

### Permissions spéciales
```
SUID = 4000 = u+s  (exécute comme proprio)
SGID = 2000 = g+s  (exécute comme groupe/héritage)
Sticky = 1000 = +t (seulement proprio supprime)
```

### SSH algorithmes (du meilleur au pire)
```
Ed25519 : 256 bits, MEILLEUR
ECDSA   : 256/384/521, très bon
RSA     : 2048-4096, bon
DSA     : 1024, DÉPRÉCIÉ
```

---

## 🚨 Pièges fréquents à l'examen

### ❌ Erreurs à éviter

**Utilisateurs**
- `usermod -G` écrase groupes → utiliser `-aG`
- Oublier `-m` avec `useradd` → pas de home créé

**Cron**
- Confondre jour du mois (3e) et jour semaine (5e)
- Oublier chemin absolu dans commandes cron
- Variables environnement limitées dans cron

**Réseau**
- Oublier masque dans `ip addr add` → OBLIGATOIRE
- `ifconfig`/`route` obsolètes → utiliser `ip`
- Confondre `nmcli con` et `nmcli device`

**Sécurité**
- `find -perm 4000` (exact) vs `-perm -4000` (inclusif)
- Éditer `/etc/sudoers` sans `visudo` → DANGEREUX
- Clé privée SSH pas 600 → refusée
- Oublier `-a` pour export GPG → binaire au lieu ASCII

**Logs**
- `journalctl -b` (boot actuel) vs `-b -1` (précédent)
- Confondre priorities: `err` existe, pas `error`

**Date/Heure**
- `hwclock --hctosys` (RTC→sys) vs `--systohc` (sys→RTC)

---

**Bon courage pour la certification LPIC-1 102-500 ! 🎓**

*Révisez avec les fiches par sujet pour approfondir chaque thème.*
