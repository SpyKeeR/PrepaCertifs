# 📄 Fiche Sujet 104 : Périphériques, Systèmes de Fichiers, FHS

**Poids : 6 points (15%)** | Révision rapide

---

## 104.1 : Partitions et Systèmes de Fichiers (2 pts)

### Outils partitionnement
```bash
# fdisk (MBR uniquement)
fdisk /dev/sdb
  m     # Aide
  p     # Afficher partitions
  n     # Nouvelle partition
  d     # Supprimer
  t     # Type partition
  w     # Écrire (sauvegarder)
  q     # Quitter sans sauvegarder

# gdisk (GPT)
gdisk /dev/sdb
  # Commandes similaires fdisk

# parted (MBR et GPT)
parted /dev/sdb mklabel gpt
parted /dev/sdb mkpart primary ext4 0% 50GB
parted /dev/sdb print
```

### Types partitions
```
83    # Linux
82    # Swap
8e    # LVM
fd    # RAID
ef    # EFI System
```

### Créer filesystems
```bash
# ext4
mkfs.ext4 /dev/sdb1
mkfs.ext4 -L DataDisk /dev/sdb1       # Avec label

# XFS
mkfs.xfs /dev/sdc1
mkfs.xfs -L BackupDisk /dev/sdc1

# VFAT (FAT32)
mkfs.vfat /dev/sdd1

# Swap
mkswap /dev/sdb2
swapon /dev/sdb2
swapoff /dev/sdb2
swapon --show
```

### Infos partitions
```bash
lsblk                  # Tree view
lsblk -f               # Avec filesystems, UUID
blkid                  # UUID, TYPE
blkid /dev/sdb1
blkid -s UUID -o value /dev/sdb1   # Seulement UUID
df -h                  # Espace utilisé
df -T                  # Avec type filesystem
fdisk -l               # Liste toutes partitions
```

---

## 104.2 : Intégrité Systèmes de Fichiers (2 pts)

### fsck/e2fsck
```bash
# ⚠️ TOUJOURS démonter avant fsck
umount /dev/sdb1
fsck /dev/sdb1
e2fsck /dev/sdb1
fsck.ext4 /dev/sdb1

# Options
fsck -y /dev/sdb1      # Auto-réparer
fsck -n /dev/sdb1      # Dry-run (pas de modifs)
fsck -f /dev/sdb1      # Force check
fsck -A                # Tous filesystems (/etc/fstab)
fsck -AR               # Tous sauf root

# Codes retour
0   # Pas d'erreur
1   # Erreurs corrigées
2   # Reboot nécessaire
4   # Erreurs NON corrigées
8   # Erreur opération
16  # Erreur usage
```

### tune2fs
```bash
tune2fs -l /dev/sdb1                # Afficher infos
tune2fs -L NewLabel /dev/sdb1       # Changer label
tune2fs -c 30 /dev/sdb1             # Check tous 30 montages
tune2fs -i 2w /dev/sdb1             # Check tous 2 weeks
tune2fs -c 0 -i 0 /dev/sdb1         # Désactiver checks auto
tune2fs -m 2 /dev/sdb1              # 2% réservé root (défaut 5%)
```

### dumpe2fs
```bash
dumpe2fs /dev/sdb1                  # Toutes infos
dumpe2fs -h /dev/sdb1               # Seulement superblock
```

### XFS tools
```bash
# ⚠️ Démonter avant xfs_repair
umount /dev/sdc1
xfs_repair /dev/sdc1
xfs_repair -n /dev/sdc1             # Dry-run

xfs_info /mnt/xfs                   # Infos (FS monté)
xfs_admin -l /dev/sdc1              # Label
xfs_admin -L NewLabel /dev/sdc1     # Changer label
xfs_admin -u /dev/sdc1              # UUID
```

### Inodes
```bash
df -i                               # Inodes libres
tune2fs -l /dev/sdb1 | grep -i inode
```

---

## 104.3 : Montage/Démontage (3 pts)

### mount
```bash
mount /dev/sdb1 /mnt/data
mount -t ext4 /dev/sdb1 /mnt/data
mount -o ro /dev/sdb1 /mnt/data     # Read-only
mount -o rw /dev/sdb1 /mnt/data     # Read-write
mount -o remount,rw /mnt/data       # Remonter sans démonter
mount -o noexec /dev/sdb1 /mnt      # Pas d'exécution
mount -o nosuid /dev/sdb1 /mnt      # Ignorer SUID
mount -o noatime /dev/sdb1 /mnt     # Pas MAJ access time

mount                               # Liste montages
mount | grep sdb1
cat /proc/mounts
findmnt
```

### umount
```bash
umount /mnt/data
umount /dev/sdb1
umount -f /mnt/data                 # Force (⚠️ perte données)
umount -l /mnt/data                 # Lazy (détache immédiatement)

# Si occupé
lsof /mnt/data                      # Processus utilisant
fuser -m /mnt/data
fuser -km /mnt/data                 # Kill processus (⚠️)
```

### /etc/fstab
```bash
# Format: device  mountpoint  fstype  options  dump  pass
UUID=xxx  /data  ext4  defaults  0  2
/dev/sdb1  /backup  xfs  noatime  0  2
/dev/sdc1  none  swap  sw  0  0

# Champs
# 1. Device (UUID recommandé)
# 2. Mount point
# 3. Filesystem type
# 4. Options (defaults, ro, rw, noexec, nosuid, noatime, user)
# 5. Dump (0=no backup, 1=backup)
# 6. Pass (0=skip fsck, 1=root first, 2=others)

# Tester fstab
mount -a                            # Monte tout
mount -av                           # Verbose
mount -a -f                         # Dry-run (fake)
mount /data                         # Si défini dans fstab
```

### Options mount courantes
```
defaults      # rw,suid,dev,exec,auto,nouser,async
ro            # Read-only
rw            # Read-write
noexec        # Pas d'exécution
nosuid        # Ignorer SUID/SGID
noatime       # Pas MAJ access time (performance)
relatime      # MAJ atime si < mtime (défaut moderne)
user          # User normal peut monter
nouser        # Seulement root (défaut)
auto          # Monte avec mount -a
noauto        # Ne monte PAS avec mount -a
```

---

## 104.5 : Permissions et Propriété (3 pts)

### chmod
```bash
# Octal
chmod 644 file         # rw-r--r--
chmod 755 script       # rwxr-xr-x
chmod 600 private      # rw-------
chmod 777 all          # rwxrwxrwx (⚠️)

# Calcul: r=4, w=2, x=1
# 644 = 4+2+0, 4+0+0, 4+0+0 = rw-r--r--

# Symbolique
chmod u+x file         # User: ajouter execute
chmod g-w file         # Group: retirer write
chmod o-r file         # Other: retirer read
chmod a+r file         # All: ajouter read
chmod u=rwx,g=rx,o=r file  # Set exact

# Récursif
chmod -R 755 directory/
```

### chown, chgrp
```bash
chown user file                 # Changer owner
chown user:group file           # Owner + group
chown :group file               # Seulement group
chgrp group file                # Seulement group (équivalent)

chown -R user:group directory/  # Récursif
```

### umask
```bash
umask                  # Afficher (ex: 0022)
umask 0027             # Set nouveau

# Calcul
# Fichiers: 666 - umask
# Dirs: 777 - umask
# umask 0022 → files 644, dirs 755
# umask 0077 → files 600, dirs 700
```

### Bits spéciaux
```bash
# SUID (4000, u+s) - Execute comme owner
chmod u+s /usr/bin/program
chmod 4755 /usr/bin/program
# Exemple: /usr/bin/passwd (user peut changer MDP)

# SGID (2000, g+s)
# Fichier: Execute comme group
# Directory: Fichiers créés héritent groupe
chmod g+s /shared/project
chmod 2775 /shared/project

# Sticky bit (1000, +t) - Seulement owner peut supprimer
chmod +t /tmp
chmod 1777 /tmp
# Exemple: /tmp (multi-users)

# Combinaisons
chmod 6755 file        # SUID + SGID
ls -l
# -rwsr-sr-x    # SUID (s), SGID (s)
# drwxrwxrwt    # Sticky (t)
```

### Trouver bits spéciaux
```bash
find / -perm -4000 2>/dev/null    # SUID
find / -perm -2000 2>/dev/null    # SGID
find / -perm -1000 2>/dev/null    # Sticky
```

---

## 104.6 : Liens (2 pts)

### Liens symboliques
```bash
ln -s /path/to/target linkname
ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/
ln -sf /new/target link            # Force (écrase existant)

readlink link                      # Voir cible
readlink -f link                   # Chemin absolu complet

ls -l link
# lrwxrwxrwx ... link -> /path/to/target
```

### Liens hard
```bash
ln /path/to/file hardlink

ls -li file hardlink
# 12345 -rw-r--r-- 2 ... (même inode, link count=2)
```

### Différences
| Aspect | Symlink | Hardlink |
|--------|---------|----------|
| **Traverse FS** | ✅ Oui | ❌ Non |
| **Cible supprimée** | ❌ Cassé | ✅ OK |
| **Inode** | Différent | Identique |
| **Directories** | ✅ Oui | ❌ Non |
| **Commande** | `ln -s` | `ln` |

---

## 104.7 : Find et FHS (2 pts)

### FHS Structure
```bash
/           # Racine
/bin        # Binaires essentiels (symlink → /usr/bin)
/boot       # Kernel, initrd, GRUB
/dev        # Fichiers devices
/etc        # Configurations système
/home       # Users home directories
/lib        # Bibliothèques (symlink → /usr/lib)
/media      # Points montage amovibles (USB, CD)
/mnt        # Points montage temporaires
/opt        # Applications tierces optionnelles
/proc       # Virtual FS (infos kernel/processus)
/root       # Home root
/run        # Runtime data (tmpfs)
/sbin       # Binaires admin (symlink → /usr/sbin)
/srv        # Données services (web, FTP)
/sys        # Virtual FS (devices, drivers)
/tmp        # Temporaire (nettoyé)
/usr        # User programs (secondaire)
  /usr/bin       # Binaires utilisateur
  /usr/sbin      # Binaires admin
  /usr/lib       # Bibliothèques
  /usr/local     # Logiciels custom
  /usr/share     # Données partagées (docs, man)
/var        # Données variables
  /var/log       # Logs système
  /var/cache     # Cache applications
  /var/spool     # Files attente (print, mail)
  /var/tmp       # Temporaire persistant
  /var/www       # Racine web
```

### find
```bash
# Structure
find [path] [options] [tests] [actions]

# Par nom
find / -name "*.conf"
find / -iname "file.txt"        # Insensible casse

# Par type
find / -type f                  # Fichiers
find / -type d                  # Directories
find / -type l                  # Symlinks

# Par taille
find / -size +100M              # > 100 MB
find / -size -10k               # < 10 KB
find / -size +1G                # > 1 GB

# Par date
find / -mtime -7                # Modifié < 7 jours
find / -mtime +30               # Modifié > 30 jours
find / -mtime 0                 # Modifié aujourd'hui
find / -mmin -60                # Modifié < 60 minutes

# Par permissions
find / -perm 644                # Exactement 644
find / -perm -644               # Au moins 644
find / -perm -u+s               # SUID
find / -perm -g+s               # SGID
find / -perm -1000              # Sticky

# Par user/group
find / -user alice
find / -group developers
find / -nouser                  # Orphelins (user supprimé)

# Actions
find / -name "*.tmp" -delete
find / -name "*.log" -exec rm {} \;
find / -type f -size +1G -exec ls -lh {} \;
find / -name "file*" -ok rm {} \;   # Avec confirmation

# Vide
find /tmp -empty                # Fichiers/dirs vides
find /tmp -type f -empty -delete

# Combinaisons
find / -name "*.log" -mtime +30 -size +100M
find / -type f \( -name "*.tmp" -o -name "*.bak" \) -delete
```

### Autres commandes
```bash
locate filename                 # Recherche rapide (base données)
updatedb                        # MAJ base locate
which command                   # Cherche dans PATH
whereis command                 # Binary + man + sources
type command                    # Type commande (alias, builtin, file)
```

---

## 🎯 Points clés examen

1. **UUID obligatoire** dans /etc/fstab (pas /dev/sdX)
2. **fsck uniquement démonté** (corruption sinon)
3. **GPT** : gdisk ou parted | **MBR** : fdisk
4. **mount -o remount,rw** : Changer options sans démonter
5. **fstab pass** : 0=skip, 1=root, 2=others
6. **chmod 755** = rwxr-xr-x
7. **SUID** : chmod u+s ou chmod 4755 (exec comme owner)
8. **SGID dir** : Fichiers héritent groupe
9. **Sticky /tmp** : Seulement owner peut supprimer
10. **Symlink traverse FS**, hardlink non
11. **find -mtime -7** : < 7 jours | **+7** : > 7 jours
12. **find -perm -4000** : SUID files
13. **/etc** : Configurations | **/var/log** : Logs
14. **umask 0022** : files 644, dirs 755

---

## 📋 Checklist révision

- [ ] fdisk (MBR) vs gdisk (GPT) vs parted
- [ ] mkfs.ext4, mkfs.xfs, mkswap
- [ ] blkid (UUID), lsblk -f
- [ ] fsck codes retour (0,1,2,4)
- [ ] tune2fs -c/-i (check intervals)
- [ ] xfs_repair (démonter avant)
- [ ] mount -o ro/rw/noexec/nosuid/noatime
- [ ] /etc/fstab format (6 champs)
- [ ] umount -f (force) vs -l (lazy)
- [ ] chmod octal (644, 755, 600)
- [ ] chown user:group
- [ ] umask calcul (666-umask, 777-umask)
- [ ] SUID (4000), SGID (2000), Sticky (1000)
- [ ] ln -s (symlink) vs ln (hardlink)
- [ ] find -name/-type/-size/-mtime/-perm
- [ ] FHS : /etc, /var/log, /usr, /opt, /srv
