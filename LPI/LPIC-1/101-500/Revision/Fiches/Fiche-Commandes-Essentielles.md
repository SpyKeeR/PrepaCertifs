# 📄 Fiche Master : Commandes Essentielles LPIC-1 101-500

**Référence complète** | Tous sujets (101-104)

---

## 🖥️ Matériel et Système (101.1, 101.2)

```bash
# Hardware
lspci                  # Périphériques PCI
lspci -v               # Détails
lsusb                  # USB devices
dmesg                  # Messages kernel
dmesg | grep -i error
lsmod                  # Modules kernel
modprobe module        # Charger module

# Infos système
/proc/cpuinfo          # CPU
/proc/meminfo          # RAM
/proc/interrupts       # IRQ
cat /proc/cpuinfo | grep "model name"
free -h                # RAM libre

# Boot
journalctl -b          # Logs boot actuel
journalctl -k          # Kernel logs
journalctl -b -1       # Boot précédent
```

---

## 🎯 Systemd et Services (101.3)

```bash
# Targets
systemctl get-default
systemctl set-default multi-user.target
systemctl isolate graphical.target

# Services
systemctl start service
systemctl stop service
systemctl restart service
systemctl status service
systemctl enable service       # Activer boot
systemctl disable service
systemctl is-enabled service
systemctl is-active service

# Units
systemctl list-units --type=service
systemctl daemon-reload
systemctl cat service
journalctl -u service

# Power
systemctl reboot
systemctl poweroff
systemctl suspend
```

---

## 💾 Disques et Partitions (102.1, 104.1)

```bash
# Partitionnement
fdisk /dev/sdb         # MBR (interactive)
gdisk /dev/sdb         # GPT
parted /dev/sdb        # Universel

# Infos
lsblk                  # Tree view
lsblk -f               # + UUID, filesystems
blkid                  # UUID, TYPE
fdisk -l               # Liste partitions
df -h                  # Espace utilisé
df -T                  # + type FS
df -i                  # Inodes

# Filesystems
mkfs.ext4 /dev/sdb1
mkfs.xfs /dev/sdc1
mkfs.vfat /dev/sdd1
mkswap /dev/sdb2
swapon /dev/sdb2
swapoff /dev/sdb2
swapon --show
```

---

## 🔧 GRUB Bootloader (102.2)

```bash
# Config
/etc/default/grub      # Éditer ici
update-grub            # Debian/Ubuntu
grub2-mkconfig -o /boot/grub2/grub.cfg  # RHEL

# Installation
grub-install /dev/sda

# Paramètres kernel boot
single, 1, S           # Single-user
3                      # Multi-user CLI
5                      # Graphical
init=/bin/bash         # Shell direct
```

---

## 📦 Packages Debian (102.4)

```bash
# APT (haut niveau)
apt update             # MAJ listes
apt upgrade            # MAJ packages
apt full-upgrade       # + résout dépendances
apt install package
apt remove package
apt purge package      # + config
apt autoremove
apt search keyword
apt show package

# dpkg (bas niveau)
dpkg -i package.deb    # Installer
dpkg -r package        # Supprimer
dpkg -P package        # Purge
dpkg -l                # Liste installés
dpkg -L package        # Fichiers installés
dpkg -S /path/file     # Package propriétaire
dpkg -s package        # Statut

# Config
/etc/apt/sources.list
dpkg-reconfigure package
```

---

## 📦 Packages RPM (102.5)

```bash
# YUM/DNF
yum update             # MAJ tout
yum install package
yum remove package
yum search keyword
yum info package
yum list installed
yum provides /path/file
yum clean all

dnf update             # Idem YUM (RHEL 8+)
dnf install package

# RPM (bas niveau)
rpm -i package.rpm     # Installer
rpm -U package.rpm     # Upgrade
rpm -e package         # Supprimer
rpm -qa                # Query all
rpm -qi package        # Query info
rpm -ql package        # Query list files
rpm -qf /path/file     # Query file owner
rpm -V package         # Verify

# Options
rpm -ivh package.rpm   # Install verbose hash
rpm -Uvh package.rpm   # Upgrade verbose
```

---

## 📚 Bibliothèques (102.3)

```bash
ldd /bin/ls            # Dépendances binaire
ldconfig               # MAJ cache libs
ldconfig -p            # Afficher cache

/etc/ld.so.conf        # Config
/etc/ld.so.conf.d/*.conf
```

---

## 🐚 Shell et Scripts (103.1)

```bash
# Variables
VAR="value"
export VAR="value"
echo $VAR
$0                     # Nom script
$1-$9                  # Arguments
$#                     # Nombre args
$?                     # Code retour
$$                     # PID

# Tests
[ -f file ]            # Fichier regular
[ -d dir ]             # Directory
[ -e file ]            # Existe
[ -r file ]            # Readable
[ -z "$str" ]          # String vide
[ $a -eq $b ]          # Égalité numérique

# Structures
if [ condition ]; then
    commands
fi

for i in list; do
    commands
done

while [ condition ]; do
    commands
done

# Opérateurs
cmd1 && cmd2           # ET
cmd1 || cmd2           # OU
```

---

## 📝 Filtres Texte (103.2)

```bash
# Affichage
cat file
cat -n file            # Numéros lignes
head -n 20 file
tail -n 20 file
tail -f /var/log/syslog

# Traitement
cut -d: -f1 /etc/passwd
sort file
sort -n file           # Numérique
sort -r file           # Reverse
sort -k2 file          # Colonne 2
uniq file
sort file | uniq
uniq -c file           # Compter
wc -l file             # Lignes
nl file                # Numéroter

# Transformation
tr 'a-z' 'A-Z' < file  # Majuscules
tr -d 'chars' < file   # Supprimer
tr -s ' ' < file       # Squeeze espaces
```

---

## 📁 Gestion Fichiers (103.3)

```bash
# Lister
ls -l                  # Long
ls -la                 # + cachés
ls -lh                 # Human-readable
ls -lt                 # Tri date
ls -ltr                # Ancien → récent
ls -R                  # Récursif
ls -i                  # Inodes

# Copier/Déplacer
cp source dest
cp -r dir dest         # Récursif
cp -a dir dest         # Archive (attrs)
cp -p file dest        # Preserve
mv source dest
rm file
rm -rf dir

# Créer
mkdir dir
mkdir -p path/to/dir
touch file

# Infos
file fichier
du -sh directory
```

---

## 🔀 Redirections et Pipes (103.4)

```bash
# Redirections
cmd > file             # Stdout → file (écrase)
cmd >> file            # Append
cmd 2> file            # Stderr → file
cmd &> file            # Stdout + Stderr
cmd 2>/dev/null        # Ignorer erreurs
cmd < file             # Stdin ← file

# Pipes
cmd1 | cmd2
cmd1 | tee file | cmd2
find . -name "*.tmp" | xargs rm

# Exemples
ps aux | grep apache
cat file | sort | uniq -c
dmesg | grep -i error | less
```

---

## ⚙️ Processus (103.5)

```bash
# Affichage
ps aux                 # Tous processus (BSD)
ps -ef                 # Tous (System V)
ps -u username
top                    # Temps réel
htop                   # Top amélioré
pgrep processname      # PID par nom
pidof processname

# Jobs
command &              # Background
jobs                   # Liste jobs
fg %1                  # Foreground
bg %1                  # Background
Ctrl+Z                 # Suspend
Ctrl+C                 # Kill

# Kill
kill PID               # SIGTERM (15)
kill -9 PID            # SIGKILL (force)
kill -HUP PID          # SIGHUP (reload)
killall processname
pkill processname
pkill -u username

# Priorité
nice -n 10 command     # Lancer +10
renice 15 -p PID       # Modifier priorité
# -20 (max) à +19 (min), défaut=0

# Persistance
nohup command &
screen
tmux
```

---

## 🔍 Regex et Recherche (103.7)

```bash
# Regex
^          # Début ligne
$          # Fin ligne
.          # N'importe quel caractère
*          # 0 ou +
+          # 1 ou + (grep -E)
?          # 0 ou 1 (grep -E)
[]         # Classe
[^]        # Négation
|          # OU (grep -E)

# grep
grep pattern file
grep -i pattern file       # Insensible casse
grep -v pattern file       # Inverser
grep -r pattern dir        # Récursif
grep -n pattern file       # Numéros lignes
grep -c pattern file       # Compter
grep -w pattern file       # Mot entier
grep -E "regex" file       # Extended
grep -A 3 pattern file     # 3 lignes après
grep -B 3 pattern file     # 3 avant
grep -C 3 pattern file     # 3 avant+après

# Exemples
grep '^root' /etc/passwd
grep -E 'error|warning' log
ps aux | grep apache | grep -v grep

# sed
sed 's/old/new/' file      # Remplacer 1ère
sed 's/old/new/g' file     # Toutes
sed -i 's/old/new/g' file  # Modifier fichier
```

---

## 📝 vi/vim (103.8)

```bash
# Modes
ESC        # Commande
i          # Insert
a          # Insert après
o          # Ligne dessous
v          # Visual

# Déplacements
h j k l    # ← ↓ ↑ →
w b        # Mot suivant/précédent
0 $        # Début/Fin ligne
gg G       # Début/Fin fichier
:n         # Ligne n

# Édition
x          # Supprimer char
dd         # Supprimer ligne
yy         # Copier ligne
p P        # Coller après/avant
u          # Undo
Ctrl+R     # Redo

# Recherche
/pattern   # Chercher
n N        # Suivant/Précédent
:s/old/new/g           # Remplacer ligne
:%s/old/new/g          # Tout fichier
:%s/old/new/gc         # Avec confirm

# Fichiers
:w         # Sauvegarder
:q         # Quitter
:wq        # Sauv + quit
:q!        # Quit sans sauv
ZZ         # Sauv + quit
```

---

## 💿 Montage et Intégrité (104.2, 104.3)

```bash
# Montage
mount /dev/sdb1 /mnt/data
mount -o ro /dev/sdb1 /mnt
mount -o remount,rw /mnt
umount /mnt/data
umount -f /mnt         # Force
umount -l /mnt         # Lazy

# /etc/fstab
# device  mountpoint  fstype  options  dump  pass
UUID=xxx  /data  ext4  defaults  0  2

mount -a               # Monte tout
mount -av              # Verbose
mount /data            # Si dans fstab

# Vérifier occupation
lsof /mnt/data
fuser -m /mnt/data
fuser -km /mnt/data    # Kill processus

# Intégrité
umount /dev/sdb1
fsck /dev/sdb1
fsck -y /dev/sdb1      # Auto-réparer
e2fsck /dev/sdb1
xfs_repair /dev/sdc1

# Infos FS
tune2fs -l /dev/sdb1
dumpe2fs -h /dev/sdb1
xfs_info /mnt/xfs
```

---

## 🔐 Permissions (104.5)

```bash
# chmod
chmod 644 file         # rw-r--r--
chmod 755 script       # rwxr-xr-x
chmod 600 private      # rw-------
chmod u+x file         # Ajouter x user
chmod g-w file         # Retirer w group
chmod -R 755 dir       # Récursif

# Calcul: r=4, w=2, x=1

# chown
chown user file
chown user:group file
chown :group file
chgrp group file
chown -R user:group dir

# umask
umask                  # Afficher
umask 0022             # Set
# Files: 666 - umask
# Dirs: 777 - umask

# Bits spéciaux
chmod u+s file         # SUID (4000)
chmod g+s dir          # SGID (2000)
chmod +t /tmp          # Sticky (1000)
chmod 4755 file        # SUID + 755
chmod 2775 dir         # SGID + 775
chmod 1777 /tmp        # Sticky + 777

# Trouver
find / -perm -4000     # SUID
find / -perm -2000     # SGID
find / -perm -1000     # Sticky
```

---

## 🔗 Liens (104.6)

```bash
# Symlink
ln -s /path/target link
ln -sf target link     # Force
readlink link          # Voir cible
readlink -f link       # Absolu

# Hardlink
ln /path/file hardlink
ls -li file hardlink   # Même inode
```

---

## 🔎 Find et FHS (104.7)

```bash
# find
find / -name "*.conf"
find / -iname file     # Insensible casse
find / -type f         # Fichiers
find / -type d         # Directories
find / -size +100M     # > 100MB
find / -size -10k      # < 10KB
find / -mtime -7       # < 7 jours
find / -mtime +30      # > 30 jours
find / -mtime 0        # Aujourd'hui
find / -user alice
find / -group dev
find / -perm 644       # Exact
find / -perm -4000     # SUID
find / -empty          # Vides
find / -name "*.tmp" -delete
find / -name "*.log" -exec rm {} \;

# Autres
locate filename        # Rapide (DB)
updatedb               # MAJ DB locate
which command          # Dans PATH
whereis command        # Binary + man
type command           # Type
```

---

## 📂 FHS - Structure Essentielle

```
/            Racine
/bin         Binaires essentiels → /usr/bin
/boot        Kernel, initrd, GRUB
/dev         Devices
/etc         Configurations système
/home        Home directories users
/lib         Libs → /usr/lib
/media       Montage amovibles (USB)
/mnt         Montage temporaires
/opt         Apps tierces
/proc        Virtual FS (kernel/processus)
/root        Home root
/run         Runtime (tmpfs)
/sbin        Admin binaries → /usr/sbin
/srv         Services data (web, FTP)
/sys         Virtual FS (devices)
/tmp         Temporaire (nettoyé)
/usr         User programs
  /usr/bin       Binaires
  /usr/sbin      Admin
  /usr/lib       Libs
  /usr/local     Custom
  /usr/share     Docs, man
/var         Données variables
  /var/log       Logs ★★★
  /var/cache     Cache
  /var/spool     Queues (mail, print)
  /var/tmp       Temp persistant
  /var/www       Web root
```

---

## 🎯 Commandes Top 50 Examen

### Critique (à connaître parfaitement)
```bash
1.  systemctl start/stop/enable/disable
2.  journalctl -b / -u / -k
3.  apt update && apt install
4.  yum/dnf install
5.  dpkg -i / -l / -L / -S
6.  rpm -qa / -qi / -ql / -qf
7.  lsblk / blkid
8.  mount / umount
9.  chmod / chown
10. find -name / -type / -size / -mtime
11. grep -r / -i / -E
12. ps aux / top
13. kill / killall
14. tail -f
15. vi :wq / dd / yy / p
16. cat / head / tail
17. sort / uniq
18. cp -r / mv / rm -rf
19. ls -la / ls -ltr
20. df -h / du -sh
```

### Important (pratique régulière)
```bash
21. mkfs.ext4 / mkswap
22. fsck / e2fsck
23. tune2fs -l
24. sed 's/old/new/g'
25. cut -d: -f1
26. wc -l
27. tar -czf / -xzf
28. dmesg | grep
29. lspci / lsusb
30. nice / renice
31. ln -s / ln
32. readlink
33. pgrep / pidof
34. lsof
35. fuser
36. update-grub
37. /etc/fstab
38. /etc/default/grub
39. /etc/apt/sources.list
40. /etc/yum.repos.d/
```

### Utile (connaître syntaxe)
```bash
41. tr 'a-z' 'A-Z'
42. paste / join
43. split
44. xargs
45. nohup
46. screen / tmux
47. ldconfig
48. modprobe / lsmod
49. xfs_repair / xfs_info
50. dumpe2fs
```

---

## 💡 Trucs et Astuces Examen

### Codes retour
```bash
echo $?        # 0 = succès, ≠0 = erreur
```

### Ignorer erreurs
```bash
command 2>/dev/null
find / -name file 2>/dev/null
```

### Combinaisons fréquentes
```bash
ps aux | grep process | grep -v grep
sort file | uniq -c | sort -rn
find / -name "*.log" -mtime +30 -delete
tar -czf backup.tar.gz /data 2>/dev/null
```

### Permissions rapides
```bash
644 → rw-r--r--   # Fichiers
755 → rwxr-xr-x   # Scripts/Dirs
600 → rw-------   # Privé
```

### UUID obligatoire fstab
```bash
blkid /dev/sdb1
# UUID=xxx dans /etc/fstab (pas /dev/sdX)
```

### fsck TOUJOURS démonté
```bash
umount /dev/sdb1
fsck /dev/sdb1
```

---

## ✅ Checklist Finale Examen

- [ ] systemd : start/stop/enable/status
- [ ] apt/yum : install/update/search
- [ ] dpkg/rpm : -i/-l/-L/-S / -qa/-qi/-ql/-qf
- [ ] Partitions : fdisk/gdisk, mkfs, blkid
- [ ] mount/umount, /etc/fstab (UUID)
- [ ] chmod (644,755), chown, SUID/SGID/Sticky
- [ ] find -name/-type/-size/-mtime/-perm
- [ ] grep -r/-i/-E, sed, sort|uniq
- [ ] ps aux, kill -9, nice/renice
- [ ] vi modes, :wq, dd, yy
- [ ] Shell vars ($0,$1,$?), tests [ ]
- [ ] Redirections >, 2>, |
- [ ] FHS : /etc, /var/log, /usr, /boot
- [ ] GRUB : /etc/default/grub, update-grub
- [ ] fsck codes (0,1,2,4)

**🚀 Bon courage pour l'examen !**
