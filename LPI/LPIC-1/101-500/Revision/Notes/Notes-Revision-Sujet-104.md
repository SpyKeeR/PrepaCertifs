# 📚 Notes de Révision - Sujet 104 : Périphériques, Systèmes de Fichiers Linux, FHS

> **Poids du sujet :** 6 points (~15% de l'examen)  
> **Sections :** 5 objectifs (104.1, 104.2, 104.3, 104.5, 104.6, 104.7)  
> **Focus :** Gestion disques, filesystems, montage, permissions, FHS

---

## 🎯 Objectifs du Sujet 104

| Objectif | Description | Poids |
|----------|-------------|-------|
| 104.1 | Créer partitions et systèmes de fichiers | 2 |
| 104.2 | Maintenir l'intégrité des systèmes de fichiers | 2 |
| 104.3 | Contrôler le montage et démontage | 3 |
| 104.5 | Gérer permissions et propriétés fichiers | 3 |
| 104.6 | Créer et modifier liens (hard/symbolic) | 2 |
| 104.7 | Trouver fichiers système et FHS | 2 |

---

## 📖 Section 104.1 : Créer partitions et systèmes de fichiers

### Outils de partitionnement

#### fdisk (MBR - legacy)
```bash
# Lister partitions
fdisk -l
fdisk -l /dev/sda

# Mode interactif
fdisk /dev/sdb
# Commandes:
# m  : aide
# p  : afficher table partitions
# n  : nouvelle partition
# d  : supprimer partition
# t  : changer type partition
# w  : écrire modifications (! destructif)
# q  : quitter sans sauver

# Exemple création partition
fdisk /dev/sdb
n       # nouvelle
p       # primaire
1       # numéro 1
Enter   # premier secteur (défaut)
+10G    # taille 10GB
w       # écrire
```

**Limites MBR :**
- Max 4 partitions primaires (ou 3 primaires + 1 étendue)
- Max 2 TB par disque
- Type de partition sur 1 octet

#### gdisk (GPT - moderne)
```bash
# GPT Partitioning Tool
gdisk /dev/sdc

# Commandes similaires fdisk
# Avantages GPT:
# - Supporte disques > 2TB
# - 128 partitions possibles
# - Table partition dupliquée (backup)
# - CRC32 checksums
# - GUID uniques par partition

# Exemple
gdisk /dev/sdc
n       # nouvelle partition
Enter   # numéro (défaut)
Enter   # premier secteur
+50G    # taille
8300    # type Linux filesystem
w       # écrire
```

#### parted (universel MBR/GPT)
```bash
# Outil universel (ligne de commande ou interactif)
parted /dev/sdd

# Créer table GPT
(parted) mklabel gpt

# Créer partition
(parted) mkpart primary ext4 0% 50%
(parted) mkpart primary ext4 50% 100%

# Afficher
(parted) print

# Mode non-interactif
parted /dev/sdd mklabel gpt
parted /dev/sdd mkpart primary ext4 0% 25GB
```

### Types de partitions

| Code | Type | Usage |
|------|------|-------|
| 83 | Linux | Système fichiers standard |
| 82 | Linux swap | Mémoire swap |
| 8e | Linux LVM | Logical Volume Manager |
| fd | Linux RAID | Software RAID |
| ef | EFI System | Boot UEFI |

### Création systèmes de fichiers

#### ext4 (standard Linux)
```bash
# Créer filesystem ext4
mkfs.ext4 /dev/sdb1
mkfs -t ext4 /dev/sdb1

# Options
mkfs.ext4 -L MonDisque /dev/sdb1     # Label
mkfs.ext4 -m 1 /dev/sdb1              # 1% reserved (défaut 5%)
mkfs.ext4 -N 1000000 /dev/sdb1        # Nombre inodes

# Vérifier
blkid /dev/sdb1
tune2fs -l /dev/sdb1
```

#### XFS (haute performance)
```bash
# Créer XFS
mkfs.xfs /dev/sdc1
mkfs.xfs -L DataDisk /dev/sdc1

# Caractéristiques:
# - Très performant grands fichiers
# - Utilisé RHEL/CentOS par défaut
# - Journaling avancé
# - Allocation retardée

# Gestion
xfs_admin -L "NewLabel" /dev/sdc1    # Changer label
xfs_info /mnt/xfs                     # Infos filesystem monté
xfs_repair /dev/sdc1                  # Réparation
```

#### VFAT/FAT32 (compatibilité)
```bash
# Créer FAT32
mkfs.vfat /dev/sdd1
mkfs -t vfat /dev/sdd1

# USB/clés compatibles Windows
mkfs.vfat -F 32 -n USBKEY /dev/sdd1

# Limites:
# - Fichiers max 4GB
# - Partitions max 32GB (Windows)
# - Pas de permissions Unix
```

#### Swap (mémoire virtuelle)
```bash
# Créer partition swap
mkswap /dev/sdb2
mkswap -L SwapPartition /dev/sdb2

# Activer
swapon /dev/sdb2
swapon -a    # Active tout (/etc/fstab)

# Vérifier
swapon --show
free -h

# Désactiver
swapoff /dev/sdb2

# Priorité
swapon -p 10 /dev/sdb2    # Priorité 10
```

### Comparaison filesystems

| Filesystem | Avantages | Inconvénients | Usage |
|------------|-----------|---------------|-------|
| **ext4** | Stable, mature, compatible | Moins performant très grands volumes | Standard Linux |
| **XFS** | Haute perf, gros fichiers | Difficile réduire taille | Serveurs, bases données |
| **Btrfs** | Snapshots, RAID natif | Moins mature | Serveurs modernes |
| **VFAT** | Compatible Windows | Pas de permissions | USB, boot EFI |

### Commandes utiles

```bash
# Lister tous les disques
lsblk
lsblk -f    # Avec filesystems

# Infos partition
blkid
blkid /dev/sda1

# UUID (identifiant unique)
blkid -s UUID -o value /dev/sda1

# Taille disques
df -h         # Montés
fdisk -l      # Tous

# Partitions utilisées
cat /proc/partitions
```

---

## 📖 Section 104.2 : Maintenir l'intégrité des systèmes de fichiers

### Vérification et réparation (ext2/ext3/ext4)

#### fsck (File System Check)
```bash
# IMPORTANT: Démonter avant fsck !
umount /dev/sdb1
fsck /dev/sdb1

# Par type
fsck.ext4 /dev/sdb1
e2fsck /dev/sdb1        # Équivalent ext

# Options
fsck -A          # Vérifier tout (/etc/fstab)
fsck -AR         # Tout sauf root
fsck -C          # Progress bar
fsck -y /dev/sdb1   # Auto-réparer (yes à tout)
fsck -n /dev/sdb1   # Dry-run (no changes)

# Force check
fsck -f /dev/sdb1

# Niveau vérification
e2fsck -p /dev/sdb1    # Preen (auto-fix safe)
e2fsck -y /dev/sdb1    # Yes à tout
e2fsck -c /dev/sdb1    # Scan bad blocks
```

**Codes retour fsck :**
- 0 : Pas d'erreur
- 1 : Erreurs corrigées
- 2 : Système devrait rebooter
- 4 : Erreurs NON corrigées
- 8 : Erreur opération
- 16 : Erreur usage/syntaxe

#### tune2fs (configuration ext)
```bash
# Afficher infos
tune2fs -l /dev/sdb1

# Label
tune2fs -L MonVolume /dev/sdb1

# Check interval
tune2fs -c 30 /dev/sdb1        # Tous les 30 montages
tune2fs -i 2w /dev/sdb1        # Tous les 2 weeks
tune2fs -c 0 -i 0 /dev/sdb1    # Désactiver checks auto

# Reserved blocks (root)
tune2fs -m 2 /dev/sdb1         # 2% réservé (défaut 5%)

# Journal
tune2fs -O has_journal /dev/sdb1      # Activer journal
tune2fs -O ^has_journal /dev/sdb1     # Désactiver

# UUID
tune2fs -U random /dev/sdb1    # Nouveau UUID
```

#### dumpe2fs (infos détaillées)
```bash
# Afficher tout
dumpe2fs /dev/sdb1

# Seulement superblock
dumpe2fs -h /dev/sdb1

# Infos clés:
# - Block size
# - Inode count
# - Block count
# - Free blocks/inodes
# - Mount count
# - Last check time
```

### XFS (filesystem moderne)

```bash
# Vérifier XFS (démonté)
xfs_repair /dev/sdc1

# Options
xfs_repair -n /dev/sdc1    # Dry-run
xfs_repair -v /dev/sdc1    # Verbose

# Infos XFS
xfs_info /mnt/data

# Admin XFS
xfs_admin -l /dev/sdc1           # Afficher label
xfs_admin -L "NewLabel" /dev/sdc1  # Changer label
xfs_admin -u /dev/sdc1           # Afficher UUID

# Défragmenter XFS (monté)
xfs_fsr /mnt/data
xfs_fsr -v /mnt/data    # Verbose
```

### Gestion inodes

```bash
# Vérifier inodes
df -i            # Inodes utilisés par filesystem

# Détails
tune2fs -l /dev/sda1 | grep -i inode

# Créer avec plus d'inodes
mkfs.ext4 -N 2000000 /dev/sdb1    # 2M inodes

# Trouver fichiers consommant inodes
for dir in /var/*; do
    echo "$dir: $(find $dir -type f | wc -l)"
done
```

### Monitoring santé disques

```bash
# SMART monitoring
smartctl -a /dev/sda
smartctl -H /dev/sda    # Health status

# Activer SMART
smartctl -s on /dev/sda

# Test rapide
smartctl -t short /dev/sda

# Vérifier résultat
smartctl -l selftest /dev/sda

# Bad blocks
badblocks -v /dev/sdb1
badblocks -w /dev/sdb1    # Write test (! destructif)
```

---

## 📖 Section 104.3 : Contrôler le montage et démontage

### Montage manuel

```bash
# Monter partition
mount /dev/sdb1 /mnt/data
mount -t ext4 /dev/sdb1 /mnt/data    # Spécifier type

# Options courantes
mount -o ro /dev/sdb1 /mnt/data           # Read-only
mount -o rw /dev/sdb1 /mnt/data           # Read-write
mount -o noexec /dev/sdb1 /mnt/data       # Pas d'exécution
mount -o nosuid /dev/sdb1 /mnt/data       # Ignorer SUID
mount -o noatime /dev/sdb1 /mnt/data      # Pas MAJ access time
mount -o remount,ro /mnt/data             # Remonter ro

# ISO
mount -o loop image.iso /mnt/iso

# Réseau (NFS)
mount -t nfs server:/share /mnt/nfs

# CIFS/SMB (Windows)
mount -t cifs //server/share /mnt/smb -o username=user
```

### Démontage

```bash
# Démonter
umount /mnt/data
umount /dev/sdb1

# Force (attention: perte données possibles)
umount -f /mnt/data

# Lazy unmount (détache immédiatement, nettoie après)
umount -l /mnt/data

# Vérifier qui utilise
lsof /mnt/data
fuser -m /mnt/data

# Tuer processus utilisant
fuser -km /mnt/data    # ! Tue tous processus
```

### /etc/fstab (montage automatique)

#### Structure /etc/fstab
```bash
# Format: device  mountpoint  fstype  options  dump  pass
/dev/sda1  /          ext4    defaults        1  1
/dev/sda2  /home      ext4    defaults        1  2
/dev/sdb1  /data      ext4    defaults        0  2
/dev/sdc1  /backup    xfs     noatime         0  2
/dev/sdd1  none       swap    sw              0  0
UUID=xxx   /mnt/usb   vfat    noauto,user     0  0

# Champs:
# 1. Device (UUID préféré)
# 2. Mount point
# 3. Filesystem type
# 4. Options (comma-separated)
# 5. Dump (0=no backup, 1=backup)
# 6. Pass (ordre fsck: 0=skip, 1=root, 2=autres)
```

#### Options mount courantes

| Option | Description |
|--------|-------------|
| `defaults` | rw,suid,dev,exec,auto,nouser,async |
| `auto` / `noauto` | Monter avec mount -a / manuel |
| `user` | User peut monter |
| `nouser` | Seulement root peut monter |
| `exec` / `noexec` | Autoriser/interdire exécution |
| `suid` / `nosuid` | Respecter/ignorer SUID bits |
| `ro` / `rw` | Read-only / read-write |
| `noatime` | Pas MAJ access time (perf) |
| `nodiratime` | Pas MAJ access time directories |
| `relatime` | MAJ atime si < mtime (compromis) |
| `sync` / `async` | Sync / async writes |

#### Utilisation UUID (recommandé)
```bash
# Trouver UUID
blkid /dev/sdb1
lsblk -f

# Exemple fstab avec UUID
UUID=a1b2c3d4-...  /data  ext4  defaults  0  2

# Avantages UUID:
# - Stable même si device change (/dev/sdb → /dev/sdc)
# - Évite erreurs montage mauvais disque
```

#### Tester fstab
```bash
# Vérifier syntaxe
mount -a        # Monte tout
mount -av       # Verbose

# Test sans montage réel
mount -a -f     # Fake (dry-run)

# Remonter entry fstab
mount /data     # Si défini dans fstab
```

### Montages spéciaux

```bash
# tmpfs (RAM)
mount -t tmpfs -o size=1G tmpfs /mnt/ramdisk

# bind mount (duplique répertoire)
mount --bind /source /destination

# Loop device
losetup /dev/loop0 disk.img
mount /dev/loop0 /mnt/img

# Procfs, sysfs (virtuels)
mount -t proc proc /proc
mount -t sysfs sys /sys
```

### Commandes utiles

```bash
# Lister montages
mount
cat /proc/mounts
findmnt

# Colonnes lisibles
findmnt -t ext4
findmnt /dev/sda1

# Montages actifs
df -h
df -T    # Avec type filesystem

# Utilisation détaillée
du -sh /var/*
ncdu /var    # Interactif (si installé)
```

---

## 📖 Section 104.5 : Gérer permissions et propriétés fichiers

### Permissions Unix (rwx)

#### Structure permissions
```bash
ls -l file.txt
# -rw-r--r-- 1 user group 1234 Jan 28 10:00 file.txt
# │││││││││
# ││└─┴─┴─── Autres (other)
# │└──┴───── Groupe (group)
# └────────── Propriétaire (user/owner)
# Premier caractère: type (- fichier, d répertoire, l lien)

# Permissions:
# r (read)    = 4
# w (write)   = 2
# x (execute) = 1
```

#### chmod (changer permissions)

**Mode octal (numérique) :**
```bash
chmod 644 file.txt    # rw-r--r--
chmod 755 script.sh   # rwxr-xr-x
chmod 600 private.key # rw-------
chmod 777 file.txt    # rwxrwxrwx (éviter!)
chmod 700 ~/.ssh      # rwx------ (dossier privé)

# Calcul:
# 644 = 4+2+0 (user) + 4+0+0 (group) + 4+0+0 (other)
# 755 = 4+2+1 (user) + 4+0+1 (group) + 4+0+1 (other)
```

**Mode symbolique :**
```bash
# u=user, g=group, o=other, a=all
chmod u+x script.sh        # Ajouter exec pour user
chmod g-w file.txt         # Retirer write pour group
chmod o-r private.txt      # Retirer read pour other
chmod a+r public.txt       # Ajouter read pour tous

# Combinaisons
chmod ug+rw,o-rwx file.txt # user+group rw, other rien
chmod u=rwx,g=rx,o=r file  # Set exact

# Récursif
chmod -R 755 /var/www/html
```

**Permissions répertoires :**
```bash
# r : Lister contenu (ls)
# w : Créer/supprimer fichiers
# x : Traverser (cd), accéder fichiers

chmod 755 directory/    # Standard
chmod 700 ~/.ssh/       # Privé
chmod 1777 /tmp/        # Sticky bit (voir plus bas)
```

#### chown (changer propriétaire)

```bash
# Changer user
chown newuser file.txt

# User + group
chown user:group file.txt
chown user.group file.txt    # Syntaxe alternative

# Seulement group
chown :group file.txt
chgrp group file.txt         # Équivalent

# Récursif
chown -R www-data:www-data /var/www/

# Copier permissions d'un fichier
chown --reference=ref.txt file.txt
```

#### umask (masque permissions défaut)

```bash
# Afficher umask
umask
# 0022 (octal)

# Calcul permissions par défaut:
# Fichiers: 666 - umask = 644 (rw-r--r--)
# Dossiers: 777 - umask = 755 (rwxr-xr-x)

# Changer umask
umask 0027    # Fichiers 640, dossiers 750
umask 0077    # Fichiers 600, dossiers 700 (privé)

# Permanent
echo "umask 0027" >> ~/.bashrc
```

### Bits spéciaux

#### SUID (Set User ID) - bit 4
```bash
# Exécuter avec permissions du propriétaire (user)
chmod u+s /usr/bin/passwd
chmod 4755 /usr/bin/passwd

# Exemple
ls -l /usr/bin/passwd
# -rwsr-xr-x root root ... (s au lieu de x)

# User lambda peut changer MDP (besoin root temporairement)
```

#### SGID (Set Group ID) - bit 2
```bash
# Fichier: exécuter avec permissions du groupe
chmod g+s /usr/bin/wall
chmod 2755 /usr/bin/wall

# Répertoire: fichiers créés héritent groupe du dossier
chmod g+s /shared/
chmod 2775 /shared/

# Utile partage collaboratif
```

#### Sticky bit - bit 1
```bash
# Sur répertoire: seulement propriétaire peut supprimer fichiers
chmod +t /tmp/
chmod 1777 /tmp/

ls -ld /tmp
# drwxrwxrwt ... (t au lieu de x)

# Exemple: /tmp
# - Tout le monde peut créer fichiers
# - Seulement propriétaire peut supprimer ses fichiers
```

#### Tableau récapitulatif bits spéciaux

| Bit | Octal | Symbole | Sur fichier | Sur répertoire |
|-----|-------|---------|-------------|----------------|
| SUID | 4000 | `s` (user) | Exécute comme owner | (sans effet) |
| SGID | 2000 | `s` (group) | Exécute comme group | Fichiers héritent groupe |
| Sticky | 1000 | `t` (other) | (rarement utilisé) | Seul owner peut supprimer |

```bash
# Exemples combinés
chmod 4755 file    # SUID + 755
chmod 2755 dir     # SGID + 755
chmod 1777 /tmp    # Sticky + 777
chmod 6755 file    # SUID + SGID + 755
```

### Attributs étendus (chattr/lsattr)

```bash
# Voir attributs
lsattr file.txt

# Immuable (même root ne peut modifier/supprimer)
chattr +i file.txt
rm file.txt         # Erreur: Permission denied

# Retirer
chattr -i file.txt

# Append-only (seulement ajouter à la fin)
chattr +a logfile.log

# Autres attributs
chattr +a file    # Append only
chattr +c file    # Compression automatique
chattr +s file    # Secure deletion (overwrite)
chattr +u file    # Undeletable (garde données)
```

### ACL (Access Control Lists)

```bash
# Permissions avancées (au-delà de user/group/other)

# Voir ACL
getfacl file.txt

# Set ACL
setfacl -m u:username:rwx file.txt        # User spécifique
setfacl -m g:groupname:rx file.txt        # Group spécifique
setfacl -m o::r file.txt                  # Other

# Supprimer ACL
setfacl -x u:username file.txt
setfacl -b file.txt                       # Tout

# Récursif
setfacl -R -m u:user:rwx directory/

# Copier ACL
getfacl file1 | setfacl --set-file=- file2
```

---

## 📖 Section 104.6 : Créer et modifier liens

### Liens symboliques (symlinks)

```bash
# Créer symlink
ln -s /path/to/target linkname
ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/

# Caractéristiques:
# - Pointeur vers fichier/dossier
# - Peut traverser filesystems
# - Si cible supprimée → lien cassé
# - Permissions du lien ignorées (suit cible)
# - Taille = longueur du chemin

# Exemples
ls -l linkname
# lrwxrwxrwx 1 user group 15 Jan 28 10:00 linkname -> /path/to/target

# Symlink relatif vs absolu
ln -s ../config.conf link       # Relatif
ln -s /etc/config.conf link     # Absolu

# Force (écraser existant)
ln -sf /new/target linkname

# Trouver cible
readlink linkname
readlink -f linkname    # Chemin absolu
```

### Liens physiques (hard links)

```bash
# Créer hardlink
ln /path/to/file hardlinkname

# Caractéristiques:
# - Même inode que fichier original
# - Compte de liens (link count) incrémenté
# - Si original supprimé → hardlink reste valide
# - NE peut PAS traverser filesystems
# - Seulement pour fichiers (pas dossiers)
# - Permissions identiques (même inode)

# Vérifier
ls -li file1 hardlink1
# Même numéro inode

# Compter liens
stat file.txt | grep Links
```

### Différences symlink vs hardlink

| Aspect | Symlink | Hardlink |
|--------|---------|----------|
| **Référence** | Chemin fichier | Inode direct |
| **Traverser FS** | ✅ Oui | ❌ Non |
| **Dossiers** | ✅ Oui | ❌ Non (sauf . et ..) |
| **Cible supprimée** | ❌ Lien cassé | ✅ Reste valide |
| **Taille** | Longueur chemin | Taille fichier |
| **Inode** | Différent | Identique |
| **Permissions** | Lien ignoré | Identiques (même inode) |

```bash
# Exemple comparaison
# Original
echo "test" > original.txt
ls -li original.txt
# 12345 -rw-r--r-- 1 user group 5 Jan 28 10:00 original.txt

# Symlink
ln -s original.txt symlink.txt
ls -li symlink.txt
# 67890 lrwxrwxrwx 1 user group 12 Jan 28 10:01 symlink.txt -> original.txt
# Inode différent

# Hardlink
ln original.txt hardlink.txt
ls -li hardlink.txt
# 12345 -rw-r--r-- 2 user group 5 Jan 28 10:00 hardlink.txt
# Même inode, link count = 2

# Supprimer original
rm original.txt

# Symlink cassé
cat symlink.txt     # Erreur: No such file
ls -l symlink.txt   # Rouge (cassé)

# Hardlink OK
cat hardlink.txt    # "test" (OK!)
```

### Cas d'usage

```bash
# Symlinks couramment utilisés
/usr/bin/python -> python3.11         # Version défaut
/etc/localtime -> /usr/share/zoneinfo/Europe/Paris
/var/www/html -> /home/user/public_html

# Hardlinks
# - Backups incrémentiels (rsync --link-dest)
# - Snapshots filesystem (économise espace)
# - Fichiers partagés même inode
```

---

## 📖 Section 104.7 : Trouver fichiers système et FHS

### Filesystem Hierarchy Standard (FHS)

#### Structure racine /

| Répertoire | Contenu | Montage |
|------------|---------|---------|
| `/` | Racine | Partition root |
| `/bin` | Binaires essentiels (tous users) | Statique |
| `/boot` | Kernel, initramfs, GRUB | Souvent partition séparée |
| `/dev` | Device files | tmpfs/devtmpfs |
| `/etc` | Configuration système | Statique |
| `/home` | Répertoires users | Souvent partition séparée |
| `/lib`, `/lib64` | Bibliothèques partagées | Statique |
| `/media` | Montage automatique (USB, CD) | - |
| `/mnt` | Montage temporaire manuel | - |
| `/opt` | Logiciels optionnels tiers | - |
| `/proc` | Infos processus/kernel (virtuel) | procfs |
| `/root` | Home directory de root | Statique |
| `/run` | Runtime data (PID, sockets) | tmpfs |
| `/sbin` | Binaires système (admin) | Statique |
| `/srv` | Données serveurs (web, FTP) | - |
| `/sys` | Infos hardware/kernel (virtuel) | sysfs |
| `/tmp` | Fichiers temporaires | tmpfs (optionnel) |
| `/usr` | Programmes utilisateur | Souvent partition séparée |
| `/var` | Données variables (logs, cache) | Souvent partition séparée |

#### Détails /usr

```bash
/usr/bin        # Binaires users (non essentiels)
/usr/sbin       # Binaires système (non essentiels)
/usr/lib        # Bibliothèques
/usr/local/     # Logiciels compilés localement
/usr/share/     # Données indépendantes archi (docs, man)
/usr/include/   # Headers C
/usr/src/       # Code source kernel
```

#### Détails /var

```bash
/var/log/       # Logs système et applications
/var/cache/     # Cache applications
/var/spool/     # Files d'attente (print, mail)
/var/tmp/       # Temp persistant entre reboots
/var/www/       # Racine web (Apache, Nginx)
/var/lib/       # Données état applications
/var/run/       # Runtime (symlink vers /run)
```

#### /etc configuration

```bash
/etc/passwd     # Users
/etc/group      # Groups
/etc/shadow     # Passwords hashés
/etc/fstab      # Filesystems montage auto
/etc/hosts      # Résolution noms locale
/etc/hostname   # Nom machine
/etc/resolv.conf # Serveurs DNS
/etc/network/   # Config réseau (Debian)
/etc/sysconfig/ # Config système (RHEL)
/etc/systemd/   # Units systemd
```

### Commandes find

#### Syntaxe de base
```bash
# Structure
find [path] [options] [tests] [actions]

# Exemples simples
find /etc -name "*.conf"              # Par nom
find /home -user username             # Par user
find /var -size +100M                 # Par taille
find /tmp -mtime -7                   # Modifié 7 derniers jours
```

#### Options de recherche

**Par nom :**
```bash
find / -name "file.txt"               # Exact
find / -iname "file.txt"              # Case-insensitive
find / -name "*.log"                  # Wildcard
find / -name "*.conf" -o -name "*.cfg" # OR
```

**Par type :**
```bash
find / -type f        # Fichiers
find / -type d        # Répertoires
find / -type l        # Symlinks
find / -type b        # Block devices
find / -type c        # Character devices
find / -type s        # Sockets
find / -type p        # Named pipes
```

**Par taille :**
```bash
find / -size +100M    # > 100 MB
find / -size -10k     # < 10 KB
find / -size 50M      # Exactement 50 MB
find / -size +1G      # > 1 GB

# Unités: c (bytes), k (KB), M (MB), G (GB)
```

**Par date/temps :**
```bash
find / -mtime -7      # Modifié < 7 jours
find / -mtime +30     # Modifié > 30 jours
find / -mtime 7       # Modifié exactement il y a 7 jours

find / -atime -1      # Accédé dernier jour
find / -ctime -7      # Changé (metadata) < 7 jours

# Minutes
find / -mmin -60      # Modifié < 60 minutes
find / -amin -30      # Accédé < 30 minutes
```

**Par permissions :**
```bash
find / -perm 644      # Exactement 644
find / -perm -644     # Au moins 644 (all bits set)
find / -perm /644     # N'importe quel bit de 644

find / -perm -u+s     # SUID
find / -perm -g+s     # SGID
find / -perm -1000    # Sticky bit
```

**Par user/group :**
```bash
find / -user username
find / -group groupname
find / -uid 1000
find / -gid 1000
find / -nouser        # Pas de user (orphelins)
find / -nogroup       # Pas de group
```

#### Actions

```bash
# Afficher (défaut)
find / -name "*.log"
find / -name "*.log" -print

# Exec commande
find / -name "*.tmp" -exec rm {} \;
find / -name "*.log" -exec gzip {} \;
find / -type f -name "*.txt" -exec chmod 644 {} \;

# Exec batch (+)
find / -name "*.tmp" -exec rm {} +    # Plus rapide

# Delete
find /tmp -name "*.tmp" -delete

# Ok (confirmation)
find / -name "*.bak" -ok rm {} \;     # Demande confirmation
```

#### Combinaisons logiques

```bash
# AND (défaut)
find / -name "*.log" -size +10M

# OR
find / -name "*.log" -o -name "*.txt"
find / \( -name "*.log" -o -name "*.txt" \) -size +1M

# NOT
find / ! -name "*.txt"
find / -not -name "*.txt"
```

#### Exemples pratiques

```bash
# Fichiers modifiés aujourd'hui
find /var/log -type f -mtime 0

# Gros fichiers (>1GB)
find / -type f -size +1G 2>/dev/null

# Fichiers SUID (sécurité)
find / -perm -4000 -ls 2>/dev/null

# Fichiers world-writable (risque)
find / -perm -002 -type f 2>/dev/null

# Fichiers vides
find / -type f -empty
find / -type d -empty

# Duplicates (même nom)
find / -name "config.conf" 2>/dev/null

# Logs anciens (>30j) à nettoyer
find /var/log -name "*.log" -mtime +30 -delete

# Répertoires modifiés cette semaine
find /home -type d -mtime -7
```

### Autres commandes de recherche

#### locate (base données)
```bash
# Recherche rapide (base de données)
locate filename
locate "*.conf"

# Update base
updatedb        # Root, cron quotidien

# Options
locate -i pattern      # Case-insensitive
locate -c pattern      # Compter résultats
locate -r 'regex'      # Regex

# Limites: pas temps réel, pas tout (honore updatedb.conf)
```

#### which (binaires PATH)
```bash
# Trouver chemin commande
which python
which -a python    # Tous dans PATH
```

#### whereis (binaires + man + sources)
```bash
# Plus large que which
whereis python
# python: /usr/bin/python /usr/lib/python3.11 /usr/share/man/man1/python.1.gz
```

#### type (builtin bash)
```bash
type cd        # cd is a shell builtin
type ls        # ls is /usr/bin/ls
type -a echo   # Tous (builtin + binaire)
```

---

## 🧪 Exercices pratiques

### Lab 1 : Partitions et filesystems
```bash
# 1. Créer partition GPT
sudo gdisk /dev/sdb
n, Enter, Enter, +10G, 8300, w

# 2. Formater ext4
sudo mkfs.ext4 -L DataDisk /dev/sdb1

# 3. Monter temporaire
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data

# 4. Vérifier
df -h | grep sdb1
lsblk -f
```

### Lab 2 : /etc/fstab
```bash
# 1. Récupérer UUID
blkid /dev/sdb1

# 2. Éditer fstab
sudo vim /etc/fstab
# Ajouter:
UUID=xxxx-xxxx  /data  ext4  defaults,noatime  0  2

# 3. Créer point montage
sudo mkdir /data

# 4. Tester
sudo mount -a
df -h | grep /data

# 5. Reboot test
sudo reboot
df -h | grep /data
```

### Lab 3 : Permissions avancées
```bash
# 1. Créer répertoire partagé
sudo mkdir /shared
sudo chmod 2775 /shared    # SGID + rwxrwxr-x
sudo chown :team /shared

# 2. Tester
touch /shared/file.txt
ls -l /shared/file.txt
# Groupe = team (hérité)

# 3. Sticky bit /tmp
ls -ld /tmp
# drwxrwxrwt (t = sticky)
```

### Lab 4 : Find avancé
```bash
# 1. Fichiers SUID
sudo find / -perm -4000 -ls 2>/dev/null

# 2. Gros fichiers
find /var -type f -size +100M -exec ls -lh {} \;

# 3. Logs anciens
find /var/log -name "*.log" -mtime +30

# 4. Fichiers modifiés aujourd'hui
find /etc -type f -mtime 0
```

---

## 📋 Checklist révision

### Partitions et FS
- [ ] Différence MBR vs GPT
- [ ] fdisk, gdisk, parted
- [ ] mkfs.ext4, mkfs.xfs, mkfs.vfat
- [ ] mkswap, swapon, swapoff
- [ ] blkid, lsblk, UUID

### Intégrité FS
- [ ] fsck, e2fsck codes retour
- [ ] tune2fs options
- [ ] xfs_repair, xfs_info
- [ ] dumpe2fs
- [ ] smartctl, badblocks

### Montage
- [ ] mount options (-o ro,rw,noexec,etc.)
- [ ] umount, umount -l, umount -f
- [ ] /etc/fstab format
- [ ] UUID vs device name
- [ ] mount -a, findmnt

### Permissions
- [ ] chmod octal (644,755,etc.)
- [ ] chmod symbolique (u+x,g-w)
- [ ] chown user:group
- [ ] umask calcul
- [ ] SUID, SGID, sticky bit
- [ ] chattr +i, +a

### Liens
- [ ] Symlink: ln -s
- [ ] Hardlink: ln
- [ ] Différences symlink/hardlink
- [ ] readlink

### FHS et find
- [ ] Structure FHS (/,/usr,/var,/etc)
- [ ] find -name, -type, -size
- [ ] find -mtime, -atime, -perm
- [ ] find -exec, -delete
- [ ] locate, updatedb
- [ ] which, whereis

---

## 🎯 Points clés pour l'examen

1. **UUID obligatoire** dans /etc/fstab (pas /dev/sdX)
2. **fsck seulement sur FS démonté** (risque corruption)
3. **Permissions répertoires** : x obligatoire pour traverser
4. **Sticky bit /tmp** : seulement owner peut supprimer
5. **SGID sur dossier** : fichiers héritent groupe
6. **Hardlink ne traverse pas FS**, symlink oui
7. **FHS**: connaître /usr, /var, /etc, /opt, /srv
8. **find -exec {} \;** vs **{} +** (batch)
9. **mount -o remount** pour changer options sans démonter
10. **tune2fs -c 0 -i 0** désactive checks automatiques

---

**Sujet 104 complet - Prêt pour le QCM ! 🚀**
