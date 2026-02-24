# 📘 Notes de Révision - Sujet 102 : Installation Linux et Gestion des Paquets

> **Poids du sujet :** 10 points (~25% de l'examen)  
> **Temps de lecture estimé :** 3-4 heures  
> **Niveau :** Fondamental - Compétences essentielles administrateur !

---

## 📋 Table des matières

- [102.1 - Conception du schéma de partitionnement (Poids: 2)](#1021---conception-du-schéma-de-partitionnement)
- [102.2 - Installation d'un gestionnaire de démarrage (Poids: 2)](#1022---installation-dun-gestionnaire-de-démarrage)
- [102.3 - Gestion des bibliothèques partagées (Poids: 1)](#1023---gestion-des-bibliothèques-partagées)
- [102.4 - Gestion des paquets Debian (Poids: 3)](#1024---gestion-des-paquets-debian)
- [102.5 - Gestion des paquets RPM et YUM (Poids: 3)](#1025---gestion-des-paquets-rpm-et-yum)

---

## 102.1 - Conception du schéma de partitionnement

### 🎯 Objectifs clés
- Comprendre partitionnement MBR et GPT
- Créer et gérer partitions
- Configurer systèmes RAID logiciel et LVM
- Comprendre points de montage et FHS

### 💾 Types de partitionnement

#### MBR (Master Boot Record)

**Caractéristiques :**
- **Standard ancien** (1983)
- **Limite disque :** 2 TB maximum
- **Partitions primaires :** 4 maximum
- **Solution :** Partition étendue + partitions logiques
- **Secteur :** 512 octets (premier secteur du disque)
- **Boot loader :** Stocké dans les 446 premiers octets

**Structure MBR :**
```
Secteur 0 (512 octets)
├── Boot code (446 octets)
├── Partition table (64 octets = 4 × 16 octets)
└── Signature (2 octets: 0x55AA)
```

**Types de partitions MBR :**
- **Primaire** : 4 maximum, bootable
- **Étendue** : Conteneur pour partitions logiques (compte comme 1 primaire)
- **Logique** : Dans partition étendue, nombre illimité

**Exemple schéma MBR classique :**
```
/dev/sda1 - Primaire (Boot)     500 MB
/dev/sda2 - Primaire (/)         30 GB
/dev/sda3 - Primaire (swap)       4 GB
/dev/sda4 - Étendue
  ├─ /dev/sda5 - Logique (/home) 50 GB
  └─ /dev/sda6 - Logique (/var)  20 GB
```

#### GPT (GUID Partition Table)

**Caractéristiques :**
- **Standard moderne** (partie UEFI)
- **Limite disque :** 9.4 ZB (zettabytes) - pratiquement illimité
- **Partitions :** 128 par défaut (extensible)
- **Redondance :** Table de partition dupliquée (début + fin du disque)
- **CRC32 :** Détection d'erreurs
- **Compatibilité :** MBR de protection (protective MBR)

**Structure GPT :**
```
Secteur 0: Protective MBR (compatibilité)
Secteur 1: GPT Header
Secteurs 2-33: Partition Entry Array (128 entrées)
...
Données des partitions
...
Secteurs -33 à -2: Backup Partition Entry Array
Secteur -1: Backup GPT Header
```

**Avantages GPT :**
- ✅ Disques > 2 TB
- ✅ Nombre partitions quasi-illimité
- ✅ Redondance et détection d'erreurs
- ✅ Noms de partitions (GUID)
- ✅ Requis pour boot UEFI

### 🔧 Outils de partitionnement

#### `fdisk` - Outil MBR/GPT interactif

```bash
# Lister partitions de tous les disques
sudo fdisk -l

# Mode interactif sur un disque
sudo fdisk /dev/sda

# Commandes interactives fdisk:
m    # Aide (menu)
p    # Afficher table de partitions
n    # Nouvelle partition
d    # Supprimer partition
t    # Changer type de partition
a    # Toggle bootable flag
w    # Écrire modifications et quitter
q    # Quitter sans sauvegarder
l    # Lister types de partitions

# Vérifier table de partitions
sudo fdisk -l /dev/sda
```

**Exemple création partition avec fdisk :**
```bash
sudo fdisk /dev/sdb

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-104857599, default 2048): [Enter]
Last sector, +sectors or +size{K,M,G} (2048-104857599, default 104857599): +10G

Command (m for help): w
```

**Types de partitions courants (code hexa) :**
- `83` = Linux filesystem
- `82` = Linux swap
- `8e` = Linux LVM
- `fd` = Linux RAID auto
- `ef` = EFI System Partition

#### `gdisk` - Outil GPT interactif

```bash
# Mode interactif GPT
sudo gdisk /dev/sda

# Commandes similaires à fdisk
p    # Afficher partitions
n    # Nouvelle partition
d    # Supprimer
t    # Type
w    # Écrire et quitter
q    # Quitter sans sauvegarder

# Convertir MBR vers GPT
sudo gdisk /dev/sda
Command: r    # Recovery/transformation
Command: f    # Load MBR and convert to GPT
```

**Types de partitions GPT (codes) :**
- `8300` = Linux filesystem
- `8200` = Linux swap
- `8e00` = Linux LVM
- `fd00` = Linux RAID
- `ef00` = EFI System Partition

#### `parted` - Outil universel ligne de commande

```bash
# Mode interactif
sudo parted /dev/sda

# Mode commande directe
sudo parted /dev/sda print
sudo parted /dev/sda mklabel gpt
sudo parted /dev/sda mkpart primary ext4 0% 100%

# Commandes interactives parted:
print           # Afficher partitions
mklabel gpt     # Créer table GPT
mklabel msdos   # Créer table MBR
mkpart          # Créer partition
rm 2            # Supprimer partition 2
resizepart      # Redimensionner partition
quit            # Quitter

# Afficher tous les disques
sudo parted -l

# Créer partition directement
sudo parted /dev/sdb mkpart primary ext4 1MiB 10GiB
```

**Unités parted :**
- `s` = Secteurs
- `B` = Octets
- `MiB`, `GiB`, `TiB` = Binaire (1024)
- `MB`, `GB`, `TB` = Décimal (1000)
- `%` = Pourcentage du disque

### 💿 Création de systèmes de fichiers

#### Commande `mkfs` - Make FileSystem

```bash
# Syntaxe générale
mkfs.type /dev/sdXN

# ext4 (par défaut Linux)
sudo mkfs.ext4 /dev/sdb1

# ext3 (ancien)
sudo mkfs.ext3 /dev/sdb1

# ext2 (très ancien, pas de journalisation)
sudo mkfs.ext2 /dev/sdb1

# XFS (haute performance, RHEL par défaut)
sudo mkfs.xfs /dev/sdb1

# Btrfs (moderne, snapshots)
sudo mkfs.btrfs /dev/sdb1

# FAT32 (compatibilité Windows)
sudo mkfs.vfat -F 32 /dev/sdb1

# NTFS (Windows)
sudo mkfs.ntfs /dev/sdb1

# Swap
sudo mkswap /dev/sdb2
sudo swapon /dev/sdb2
```

**Options mkfs.ext4 :**
```bash
# Avec label
sudo mkfs.ext4 -L "MonDisque" /dev/sdb1

# Réserver espace pour root (défaut 5%)
sudo mkfs.ext4 -m 1 /dev/sdb1   # 1% au lieu de 5%

# Spécifier taille de bloc
sudo mkfs.ext4 -b 4096 /dev/sdb1

# Sans journalisation (pas recommandé)
sudo mkfs.ext4 -O ^has_journal /dev/sdb1
```

#### Swap (Mémoire virtuelle)

```bash
# Créer partition swap
sudo mkswap /dev/sdb2

# Activer swap
sudo swapon /dev/sdb2

# Désactiver swap
sudo swapoff /dev/sdb2

# Voir swap actif
swapon --show
free -h

# Priorité swap (0-32767, plus haut = prioritaire)
sudo swapon -p 10 /dev/sdb2

# Fichier swap (alternative à partition)
sudo dd if=/dev/zero of=/swapfile bs=1M count=2048  # 2 GB
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

### 🗂️ Montage de systèmes de fichiers

#### Commande `mount`

```bash
# Monter partition
sudo mount /dev/sdb1 /mnt

# Monter avec type spécifique
sudo mount -t ext4 /dev/sdb1 /mnt

# Monter avec options
sudo mount -o rw,noexec,nosuid /dev/sdb1 /mnt

# Lister montages
mount
mount | grep sdb

# Démonter
sudo umount /mnt
sudo umount /dev/sdb1

# Démonter force (si busy)
sudo umount -f /mnt

# Démonter lazy (quand plus utilisé)
sudo umount -l /mnt
```

**Options de montage courantes :**
- `rw` / `ro` : Lecture-écriture / Lecture seule
- `noexec` : Empêcher exécution binaires
- `nosuid` : Ignorer bit SUID
- `nodev` : Ignorer fichiers périphériques
- `noatime` : Ne pas mettre à jour access time (performance)
- `user` : Autoriser utilisateurs non-root à monter
- `auto` / `noauto` : Monter auto au boot
- `defaults` : `rw,suid,dev,exec,auto,nouser,async`

#### Fichier `/etc/fstab` - Montages permanents

**Format fstab :**
```
<device>  <mount_point>  <type>  <options>  <dump>  <pass>
```

**Exemple /etc/fstab :**
```bash
# Device                Mount Point   Type    Options              Dump Pass
UUID=xxx-xxx-xxx        /             ext4    defaults             0    1
UUID=yyy-yyy-yyy        /home         ext4    defaults,noatime     0    2
UUID=zzz-zzz-zzz        none          swap    sw                   0    0
/dev/sdb1               /mnt/data     ext4    defaults,noauto      0    0
tmpfs                   /tmp          tmpfs   defaults,size=2G     0    0
//server/share          /mnt/smb      cifs    credentials=/root/.smbcreds,uid=1000  0  0
```

**Colonnes fstab :**
1. **Device** : UUID, LABEL, ou /dev/sdXN
2. **Mount Point** : Chemin de montage
3. **Type** : ext4, xfs, swap, ntfs, vfat, etc.
4. **Options** : Options de montage (voir ci-dessus)
5. **Dump** : Sauvegarde avec dump (0=non, 1=oui) - obsolète
6. **Pass** : Ordre fsck (0=skip, 1=root, 2=autres)

**Commandes fstab :**
```bash
# Tester fstab AVANT redémarrage
sudo mount -a

# Monter une seule entrée fstab
sudo mount /home

# Obtenir UUID d'une partition
sudo blkid /dev/sdb1

# Lister tous les UUID
sudo blkid

# Éditer fstab
sudo nano /etc/fstab
```

**⚠️ IMPORTANT :** Toujours tester `mount -a` après modification de fstab ! Erreur = boot impossible.

### 🔄 LVM (Logical Volume Manager)

#### Concepts LVM

**Hiérarchie LVM :**
```
Disques physiques (/dev/sda, /dev/sdb)
    ↓
Physical Volumes (PV) - Disques initialisés LVM
    ↓
Volume Groups (VG) - Pool de stockage
    ↓
Logical Volumes (LV) - Partitions virtuelles
    ↓
Systèmes de fichiers (ext4, xfs...)
```

**Avantages LVM :**
- ✅ Redimensionnement à chaud (online)
- ✅ Snapshots (sauvegarde instantanée)
- ✅ Plusieurs disques = 1 volume logique
- ✅ Migration de données entre disques
- ✅ Thin provisioning

#### Commandes LVM - Physical Volumes

```bash
# Créer PV
sudo pvcreate /dev/sdb
sudo pvcreate /dev/sdc

# Lister PV
sudo pvs          # Résumé
sudo pvdisplay    # Détaillé
sudo pvscan       # Scan système

# Supprimer PV
sudo pvremove /dev/sdb

# Infos PV spécifique
sudo pvdisplay /dev/sdb
```

#### Commandes LVM - Volume Groups

```bash
# Créer VG (combine plusieurs PV)
sudo vgcreate vg_data /dev/sdb /dev/sdc

# Étendre VG (ajouter PV)
sudo vgextend vg_data /dev/sdd

# Réduire VG (retirer PV)
sudo vgreduce vg_data /dev/sdd

# Lister VG
sudo vgs
sudo vgdisplay
sudo vgscan

# Supprimer VG
sudo vgremove vg_data

# Activer/Désactiver VG
sudo vgchange -a y vg_data   # Activer
sudo vgchange -a n vg_data   # Désactiver

# Renommer VG
sudo vgrename vg_old vg_new
```

#### Commandes LVM - Logical Volumes

```bash
# Créer LV (100 GB)
sudo lvcreate -L 100G -n lv_backups vg_data

# Créer LV (100% de l'espace libre)
sudo lvcreate -l 100%FREE -n lv_archive vg_data

# Lister LV
sudo lvs
sudo lvdisplay
sudo lvscan

# Étendre LV (+50G)
sudo lvextend -L +50G /dev/vg_data/lv_backups

# Réduire LV (DANGER : perte données si pas préparé)
sudo lvreduce -L -20G /dev/vg_data/lv_backups

# Redimensionner LV + filesystem en une commande
sudo lvextend -r -L +50G /dev/vg_data/lv_backups

# Supprimer LV
sudo lvremove /dev/vg_data/lv_backups

# Renommer LV
sudo lvrename vg_data lv_old lv_new
```

#### Workflow complet LVM

```bash
# 1. Créer PV sur disques
sudo pvcreate /dev/sdb /dev/sdc

# 2. Créer VG
sudo vgcreate vg_data /dev/sdb /dev/sdc

# 3. Créer LV
sudo lvcreate -L 200G -n lv_backups vg_data

# 4. Créer filesystem
sudo mkfs.ext4 /dev/vg_data/lv_backups

# 5. Monter
sudo mkdir /mnt/backups
sudo mount /dev/vg_data/lv_backups /mnt/backups

# 6. Ajouter à fstab (pour montage permanent)
echo "/dev/vg_data/lv_backups  /mnt/backups  ext4  defaults  0  2" | sudo tee -a /etc/fstab
```

#### Redimensionner filesystem après LVM

```bash
# Étendre ext4 (online - monté)
sudo resize2fs /dev/vg_data/lv_backups

# Étendre XFS (online)
sudo xfs_growfs /mnt/backups

# Réduire ext4 (offline - démonté)
sudo umount /mnt/backups
sudo e2fsck -f /dev/vg_data/lv_backups
sudo resize2fs /dev/vg_data/lv_backups 180G
sudo lvreduce -L 180G /dev/vg_data/lv_backups
sudo mount /dev/vg_data/lv_backups /mnt/backups

# Note: XFS ne peut PAS être réduit
```

#### Snapshots LVM

```bash
# Créer snapshot (10G de cache)
sudo lvcreate -L 10G -s -n lv_backups_snap /dev/vg_data/lv_backups

# Monter snapshot
sudo mkdir /mnt/snap
sudo mount /dev/vg_data/lv_backups_snap /mnt/snap

# Restaurer depuis snapshot
sudo umount /mnt/backups
sudo lvconvert --merge /dev/vg_data/lv_backups_snap
# Au prochain activation, LV sera restauré

# Supprimer snapshot
sudo lvremove /dev/vg_data/lv_backups_snap
```

### ⚡ RAID logiciel (mdadm)

#### Niveaux RAID courants

| RAID | Disques min | Capacité | Tolérance panne | Performance | Usage |
|------|-------------|----------|-----------------|-------------|-------|
| **0** | 2 | 100% (n×) | Aucune | Lecture/Écriture ++ | Performance |
| **1** | 2 | 50% (n÷2) | n-1 disques | Lecture ++ | Fiabilité |
| **5** | 3 | (n-1)× | 1 disque | Lecture +, Écriture - | Balance |
| **6** | 4 | (n-2)× | 2 disques | Lecture +, Écriture -- | Haute fiabilité |
| **10** | 4 | 50% | 1 par miroir | Lecture/Écriture + | Performance + fiabilité |

#### Commandes mdadm

```bash
# Créer RAID 1 (miroir)
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc

# Créer RAID 5 (3 disques)
sudo mdadm --create /dev/md1 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd

# Examiner array RAID
sudo mdadm --detail /dev/md0

# Examiner disque
sudo mdadm --examine /dev/sdb

# Arrêter RAID
sudo mdadm --stop /dev/md0

# Assembler RAID (après reboot)
sudo mdadm --assemble /dev/md0 /dev/sdb /dev/sdc

# Scan et auto-assemble
sudo mdadm --assemble --scan

# Ajouter disque spare (remplacement auto)
sudo mdadm --add /dev/md0 /dev/sdd

# Retirer disque failed
sudo mdadm --remove /dev/md0 /dev/sdb

# Marquer disque comme failed
sudo mdadm --fail /dev/md0 /dev/sdb

# Surveiller RAID
cat /proc/mdstat

# Configuration persistante
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
sudo update-initramfs -u
```

**Fichier /proc/mdstat :**
```bash
cat /proc/mdstat
# Personalities : [raid1] [raid6] [raid5] [raid4]
# md0 : active raid1 sdb1[0] sdc1[1]
#       104320 blocks super 1.2 [2/2] [UU]
```

---

## 102.2 - Installation d'un gestionnaire de démarrage

### 🎯 Objectifs clés
- Installer GRUB sur MBR et GPT
- Configurer GRUB Legacy et GRUB 2
- Interagir avec bootloader au démarrage
- Configurer alternatives (LILO)

### 🥾 GRUB 2 - Installation

#### Installation sur disque MBR (BIOS)

```bash
# Installer GRUB sur MBR de /dev/sda
sudo grub-install /dev/sda

# Spécifier répertoire boot
sudo grub-install --boot-directory=/mnt/boot /dev/sda

# Forcer installation (réinstallation)
sudo grub-install --force /dev/sda

# Vérifier installation
sudo grub-install --version
```

**⚠️ IMPORTANT :** Installer sur **disque** (/dev/sda), PAS partition (/dev/sda1) !

#### Installation sur système UEFI (GPT)

```bash
# Installer GRUB UEFI
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi

# Avec bootloader-id personnalisé
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB

# Pour système 32-bit UEFI (rare)
sudo grub-install --target=i386-efi --efi-directory=/boot/efi

# Vérifier installation
ls /boot/efi/EFI/
efibootmgr -v
```

#### Générer configuration GRUB

```bash
# Debian/Ubuntu
sudo update-grub

# Équivalent universel
sudo grub-mkconfig -o /boot/grub/grub.cfg

# Red Hat/CentOS
sudo grub2-mkconfig -o /boot/grub2/grub.cfg

# Avec verbosité
sudo grub-mkconfig -v -o /boot/grub/grub.cfg
```

### ⚙️ Configuration GRUB 2

#### Fichier `/etc/default/grub`

**Paramètres principaux :**
```bash
# Entrée par défaut (0=première, 1=deuxième, etc.)
GRUB_DEFAULT=0

# Ou par nom d'entrée
GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 5.15.0-58"

# Dernière entrée utilisée
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true

# Timeout (secondes)
GRUB_TIMEOUT=5

# Timeout style
GRUB_TIMEOUT_STYLE=menu     # Afficher menu
# GRUB_TIMEOUT_STYLE=hidden  # Cacher (Shift pour afficher)
# GRUB_TIMEOUT_STYLE=countdown  # Compte à rebours

# Paramètres kernel (tous modes)
GRUB_CMDLINE_LINUX="crashkernel=auto"

# Paramètres kernel (mode normal)
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

# Désactiver recovery mode
GRUB_DISABLE_RECOVERY="true"

# Résolution console graphique
GRUB_GFXMODE=1024x768

# Désactiver os-prober (détection autres OS)
GRUB_DISABLE_OS_PROBER=true

# Thème graphique
GRUB_THEME="/boot/grub/themes/starfield/theme.txt"

# Background image
GRUB_BACKGROUND="/boot/grub/background.png"
```

#### Scripts `/etc/grub.d/`

**Ordre d'exécution (numéro = priorité) :**
```bash
00_header           # En-tête configuration
05_debian_theme     # Thème (si présent)
10_linux            # Détecte kernels Linux
20_linux_xen        # Xen hypervisor
30_os-prober        # Détecte autres OS (Windows, etc.)
40_custom           # Entrées personnalisées
41_custom           # Idem (préservé lors mises à jour)
```

**Fichier `/etc/grub.d/40_custom` exemple :**
```bash
#!/bin/sh
exec tail -n +3 $0
# Entrées personnalisées ci-dessous

menuentry "Ubuntu Recovery Shell" {
    set root=(hd0,1)
    linux /vmlinuz root=/dev/sda1 ro single
    initrd /initrd.img
}

menuentry "Memtest86+" {
    linux16 /memtest86+.bin
}
```

**Rendre script exécutable :**
```bash
sudo chmod +x /etc/grub.d/40_custom
sudo update-grub
```

### 🔧 Ligne de commande GRUB

#### Shell GRUB (appuyer sur `c` au menu)

```bash
# Lister disques et partitions
ls
# (hd0) (hd0,gpt1) (hd0,gpt2) (hd1)

# Afficher contenu partition
ls (hd0,1)/
# lost+found/ etc/ bin/ boot/ ...

# Afficher contenu fichier
cat (hd0,1)/etc/hostname

# Définir partition root
set root=(hd0,1)

# Voir variables
set

# Charger module
insmod ext2
insmod lvm

# Charger kernel manuellement
linux /vmlinuz root=/dev/sda1 ro
initrd /initrd.img
boot

# Rechercher fichier
search --file --set=root /vmlinuz
```

#### Éditer entrée GRUB (appuyer sur `e`)

**Modifications temporaires (une session) :**
1. Au menu GRUB, sélectionner entrée
2. Appuyer sur **`e`**
3. Modifier ligne `linux` (ajouter paramètres)
4. **`Ctrl+X`** ou **`F10`** pour booter

**Exemple - Mode single user :**
```bash
# Ligne originale:
linux /vmlinuz-5.15.0-58 root=UUID=xxx ro quiet splash

# Modifier en:
linux /vmlinuz-5.15.0-58 root=UUID=xxx ro single

# Ctrl+X pour booter
```

### 📜 GRUB Legacy (ancien - connaître pour examen)

**Différences GRUB Legacy vs GRUB 2 :**

| Aspect | GRUB Legacy | GRUB 2 |
|--------|-------------|---------|
| Fichier config | `/boot/grub/menu.lst` | `/boot/grub/grub.cfg` |
| Éditable | Oui, directement | Non, généré automatiquement |
| Commande install | `grub-install` | `grub-install` |
| Syntaxe partitions | `(hd0,0)` = 1ère partition | `(hd0,1)` = 1ère partition |
| Scripts config | Non | Oui (`/etc/grub.d/`) |
| Version | 0.9x | 1.9x / 2.x |

**Exemple menu.lst (GRUB Legacy) :**
```bash
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz

title Ubuntu 10.04
root (hd0,0)
kernel /vmlinuz root=/dev/sda1 ro quiet splash
initrd /initrd.img

title Ubuntu 10.04 (recovery mode)
root (hd0,0)
kernel /vmlinuz root=/dev/sda1 ro single
initrd /initrd.img
```

### 🔐 Protection par mot de passe GRUB

#### GRUB 2 - Mot de passe

```bash
# Générer hash mot de passe
grub-mkpasswd-pbkdf2
# Enter password: ********
# Reenter password: ********
# PBKDF2 hash: grub.pbkdf2.sha512.10000.LONG_HASH

# Ajouter dans /etc/grub.d/40_custom
cat << 'EOF' | sudo tee -a /etc/grub.d/40_custom
set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.LONG_HASH
EOF

# Protéger entrée spécifique
menuentry "Ubuntu Secure" --users admin {
    # ...
}

# Entrée non protégée (accessible sans mot de passe)
menuentry "Ubuntu" --unrestricted {
    # ...
}

# Régénérer config
sudo update-grub
```

### 🛠️ Dépannage GRUB

#### GRUB Rescue (erreur boot)

**Scénario :** Message `grub rescue>`

```bash
# 1. Lister partitions
grub rescue> ls
(hd0) (hd0,gpt1) (hd0,gpt2)

# 2. Trouver partition Linux
grub rescue> ls (hd0,gpt2)/
lost+found/ etc/ bin/ boot/ ...

# 3. Définir root et prefix
grub rescue> set root=(hd0,gpt2)
grub rescue> set prefix=(hd0,gpt2)/boot/grub

# 4. Charger module normal
grub rescue> insmod normal

# 5. Lancer normal mode
grub rescue> normal

# 6. Une fois booté, réinstaller GRUB
sudo grub-install /dev/sda
sudo update-grub
```

#### Réinstaller GRUB depuis Live USB

```bash
# 1. Booter sur Live USB
# 2. Identifier partition root
sudo fdisk -l

# 3. Monter partition root
sudo mount /dev/sda2 /mnt

# 4. Monter partitions système
sudo mount --bind /dev /mnt/dev
sudo mount --bind /dev/pts /mnt/dev/pts
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys

# 5. Si UEFI, monter ESP
sudo mount /dev/sda1 /mnt/boot/efi

# 6. Chroot dans système
sudo chroot /mnt

# 7. Réinstaller GRUB
# BIOS:
grub-install /dev/sda

# UEFI:
grub-install --target=x86_64-efi --efi-directory=/boot/efi

# 8. Régénérer config
update-grub

# 9. Sortir et redémarrer
exit
sudo umount -R /mnt
sudo reboot
```

---

## 102.3 - Gestion des bibliothèques partagées

### 🎯 Objectifs clés
- Comprendre bibliothèques partagées (.so)
- Localiser bibliothèques systèmes
- Charger bibliothèques partagées
- Configurer chemins de bibliothèques

### 📚 Concept de bibliothèques partagées

**Bibliothèque partagée (Shared Library) :**
- Fichier `.so` (Shared Object) - équivalent `.dll` Windows
- Code réutilisable par plusieurs programmes
- Chargée en mémoire une seule fois (partagée)
- Économie mémoire et espace disque

**Types de bibliothèques :**
- **Statiques** (`.a`) : Intégrées dans binaire (plus gros)
- **Dynamiques** (`.so`) : Chargées au runtime (plus petit)

**Nomenclature :**
```
libNOM.so.VERSION
│   │    │  │
│   │    │  └─ Numéro version (1, 2.0, 2.1.5...)
│   │    └─ Extension shared object
│   └─ Nom bibliothèque
└─ Préfixe

Exemple: libssl.so.1.1
```

### 🔍 Localiser bibliothèques

#### Commande `ldd` - List Dynamic Dependencies

```bash
# Afficher bibliothèques utilisées par programme
ldd /bin/ls

# Sortie exemple:
#   linux-vdso.so.1 (0x00007ffd123ab000)
#   libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007f8c9e2a0000)
#   libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f8c9e0a0000)
#   /lib64/ld-linux-x86-64.so.2 (0x00007f8c9e6f0000)

# Vérifier dépendances application
ldd /usr/bin/firefox

# Vérifier bibliothèque elle-même
ldd /usr/lib/x86_64-linux-gnu/libssl.so.1.1

# Afficher unused dependencies
ldd -u /bin/ls

# Verbose
ldd -v /bin/ls
```

**Interprétation sortie ldd :**
```
libssl.so.1.1 => /usr/lib/x86_64-linux-gnu/libssl.so.1.1 (0x7f...)
│             │  │                                         │
│             │  │                                         └─ Adresse mémoire
│             │  └─ Chemin complet bibliothèque
│             └─ Symbole "trouvée ici"
└─ Nom bibliothèque demandée

=> not found : ERREUR - bibliothèque manquante
```

#### Commande `ldconfig` - Configure dynamic linker

```bash
# Mettre à jour cache des bibliothèques
sudo ldconfig

# Afficher cache
ldconfig -p | grep ssl
# libssl.so.1.1 (libc6,x86-64) => /usr/lib/x86_64-linux-gnu/libssl.so.1.1

# Verbose (affiche directories scannés)
sudo ldconfig -v

# Afficher version
ldconfig -V

# Chercher bibliothèque spécifique
ldconfig -p | grep libpython
```

**Quand exécuter ldconfig :**
- Après installation bibliothèque manuelle
- Après modification `/etc/ld.so.conf`
- Après ajout fichiers dans `/usr/local/lib`

### 📁 Chemins de bibliothèques

#### Fichier `/etc/ld.so.conf`

**Contenu typique :**
```bash
cat /etc/ld.so.conf
# include /etc/ld.so.conf.d/*.conf
```

**Fichiers inclus :**
```bash
ls /etc/ld.so.conf.d/
# libc.conf
# x86_64-linux-gnu.conf
# fakeroot-x86_64-linux-gnu.conf
```

**Exemple `/etc/ld.so.conf.d/custom.conf` :**
```bash
# Ajouter chemin personnalisé
/opt/myapp/lib
/usr/local/lib64
```

**Après modification :**
```bash
sudo ldconfig
```

#### Variable d'environnement `LD_LIBRARY_PATH`

```bash
# Ajouter temporairement chemin bibliothèques
export LD_LIBRARY_PATH=/opt/myapp/lib:$LD_LIBRARY_PATH

# Lancer application avec bibliothèques spécifiques
LD_LIBRARY_PATH=/custom/lib ./myapp

# Vérifier
echo $LD_LIBRARY_PATH

# Permanent (dans ~/.bashrc)
echo 'export LD_LIBRARY_PATH=/opt/myapp/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
```

**⚠️ ATTENTION :** `LD_LIBRARY_PATH` peut causer conflits de versions. Préférer `ldconfig` pour configuration système.

#### Chemins standard de bibliothèques

```bash
# Bibliothèques système (64-bit)
/lib/x86_64-linux-gnu/
/usr/lib/x86_64-linux-gnu/

# Bibliothèques système (32-bit sur système 64-bit)
/lib/i386-linux-gnu/
/usr/lib/i386-linux-gnu/

# Bibliothèques locales
/usr/local/lib/
/usr/local/lib64/

# Bibliothèques optionnelles
/opt/*/lib/

# Cache
/etc/ld.so.cache
```

### 🔗 Liens symboliques de bibliothèques

**Structure typique :**
```bash
ls -l /usr/lib/x86_64-linux-gnu/libssl*

# lrwxrwxrwx libssl.so -> libssl.so.1.1
# lrwxrwxrwx libssl.so.1.1 -> libssl.so.1.1.1
# -rw-r--r-- libssl.so.1.1.1

# libssl.so      : Lien compilation
# libssl.so.1.1  : Lien compatibilité version majeure.mineure
# libssl.so.1.1.1: Fichier réel
```

**Créer liens après installation manuelle :**
```bash
# Copier bibliothèque
sudo cp libcustom.so.2.5.1 /usr/local/lib/

# Créer lien version majeure
sudo ln -s /usr/local/lib/libcustom.so.2.5.1 /usr/local/lib/libcustom.so.2

# Créer lien compilation
sudo ln -s /usr/local/lib/libcustom.so.2 /usr/local/lib/libcustom.so

# Mettre à jour cache
sudo ldconfig
```

---

## 102.4 - Gestion des paquets Debian

### 🎯 Objectifs clés
- Installer, mettre à jour, supprimer paquets (apt/dpkg)
- Gérer dépendances
- Rechercher paquets
- Configurer sources de paquets

### 📦 Système de paquets Debian

**Format :** `.deb` (Debian Package)

**Outils principaux :**
- **`dpkg`** : Bas niveau, gère paquets .deb locaux
- **`apt`** / **`apt-get`** / **`apt-cache`** : Haut niveau, gère dépôts + dépendances
- **`aptitude`** : Interface alternative (TUI)

### 🔧 dpkg - Debian Package Manager

#### Installation et suppression

```bash
# Installer paquet .deb
sudo dpkg -i package.deb

# Installer plusieurs paquets
sudo dpkg -i *.deb

# Supprimer paquet (garder fichiers config)
sudo dpkg -r package_name

# Purger paquet (supprimer tout)
sudo dpkg -P package_name

# Reconfigurer paquet
sudo dpkg-reconfigure package_name

# Exemple: reconfigurer timezone
sudo dpkg-reconfigure tzdata
```

#### Recherche et information

```bash
# Lister tous les paquets installés
dpkg -l

# Lister avec filtre
dpkg -l | grep ssh

# Statut d'un paquet
dpkg -s openssh-server

# Lister fichiers d'un paquet installé
dpkg -L openssh-server

# Trouver quel paquet fournit un fichier
dpkg -S /bin/ls
# coreutils: /bin/ls

# Lister contenu .deb (sans installer)
dpkg -c package.deb

# Infos sur .deb (sans installer)
dpkg -I package.deb
```

#### Dépannage dpkg

```bash
# Configurer paquets partiellement installés
sudo dpkg --configure -a

# Forcer installation (si conflit)
sudo dpkg -i --force-all package.deb

# Liste des options --force
dpkg --force-help

# Vérifier intégrité paquets installés
sudo dpkg --verify

# Audit paquets (fichiers modifiés)
sudo dpkg --audit
```

### 📦 APT - Advanced Package Tool

#### apt vs apt-get vs apt-cache

**`apt`** (moderne, recommandé) :
```bash
apt install package      # Installer
apt remove package       # Supprimer
apt search keyword       # Rechercher
apt update              # Mettre à jour index
apt upgrade             # Mettre à jour paquets
apt full-upgrade        # Upgrade + gestion dépendances
apt autoremove          # Supprimer paquets inutiles
apt list --installed    # Lister installés
apt show package        # Infos paquet
```

**`apt-get`** (classique, scripts) :
```bash
apt-get install package
apt-get remove package
apt-get update
apt-get upgrade
apt-get dist-upgrade    # = apt full-upgrade
apt-get autoremove
apt-get clean           # Nettoyer cache
apt-get autoclean       # Nettoyer paquets obsolètes
```

**`apt-cache`** (recherche/info) :
```bash
apt-cache search keyword
apt-cache show package
apt-cache policy package    # Versions disponibles
apt-cache depends package   # Dépendances
apt-cache rdepends package  # Reverse dependencies
apt-cache pkgnames         # Liste tous les paquets
```

#### Commandes apt courantes

```bash
# Mettre à jour liste des paquets
sudo apt update

# Mettre à jour tous les paquets
sudo apt upgrade

# Mettre à jour + gérer dépendances/conflits
sudo apt full-upgrade

# Installer paquet
sudo apt install nginx

# Installer version spécifique
sudo apt install nginx=1.18.0-1ubuntu1

# Installer sans confirmation
sudo apt install -y nginx

# Simuler installation (dry-run)
sudo apt install -s nginx

# Télécharger sans installer
sudo apt install --download-only nginx

# Supprimer paquet (garder config)
sudo apt remove nginx

# Purger paquet (tout supprimer)
sudo apt purge nginx

# Supprimer paquets inutilisés
sudo apt autoremove

# Rechercher paquet
apt search "web server"

# Infos détaillées paquet
apt show nginx

# Lister paquets installés
apt list --installed

# Lister paquets upgradables
apt list --upgradable

# Nettoyer cache téléchargements
sudo apt clean

# Vérifier dépendances cassées
sudo apt check

# Réparer dépendances
sudo apt --fix-broken install
```

#### Sources de paquets `/etc/apt/sources.list`

**Format :**
```
deb [options] URI distribution composants
```

**Exemple `/etc/apt/sources.list` (Ubuntu) :**
```bash
# Ubuntu Main Repository
deb http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse

# Updates
deb http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse

# Security
deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

# Backports
deb http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
```

**Composants Ubuntu :**
- **main** : Supporté officiellement, open-source
- **restricted** : Supporté, propriétaire (drivers)
- **universe** : Communauté, open-source
- **multiverse** : Non supporté, propriétaire

**Composants Debian :**
- **main** : DFSG-compliant (free)
- **contrib** : Free mais dépend de non-free
- **non-free** : Propriétaire

**Fichiers additionnels :**
```bash
/etc/apt/sources.list.d/
# custom-repo.list
# ppa-name.list
```

#### Ajouter dépôts (PPA - Ubuntu)

```bash
# Ajouter PPA
sudo add-apt-repository ppa:user/ppa-name

# Exemple: PHP 8.1
sudo add-apt-repository ppa:ondrej/php

# Mettre à jour
sudo apt update

# Supprimer PPA
sudo add-apt-repository --remove ppa:user/ppa-name

# Ou manuellement
sudo rm /etc/apt/sources.list.d/ppa-name.list
```

#### Clés GPG de dépôts

```bash
# Lister clés
apt-key list

# Ajouter clé depuis serveur
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys KEY_ID

# Ajouter clé depuis fichier
wget -O- https://example.com/key.gpg | sudo apt-key add -

# Supprimer clé
sudo apt-key del KEY_ID

# Méthode moderne (sans apt-key - déprécié)
wget -O- https://example.com/key.gpg | sudo tee /etc/apt/trusted.gpg.d/repo-name.asc
```

#### Préférences et pinning

**Fichier `/etc/apt/preferences` :**
```bash
# Préférer version spécifique
Package: nginx
Pin: version 1.18.*
Pin-Priority: 1001

# Préférer dépôt spécifique
Package: *
Pin: release o=Ubuntu,a=jammy-backports
Pin-Priority: 500
```

**Priorités :**
- `> 1000` : Downgrade autorisé
- `990-1000` : Préférence haute
- `500` : Version installée
- `100` : Non installé
- `< 0` : Blacklist

### 🔄 aptitude (alternative TUI)

```bash
# Lancer interface
sudo aptitude

# Mode commande (comme apt)
sudo aptitude install package
sudo aptitude remove package
sudo aptitude search keyword
sudo aptitude update
sudo aptitude upgrade
sudo aptitude full-upgrade

# Recherche avancée
aptitude search '~i!~M'    # Installés manuellement
aptitude search '~c'       # Config files restants
aptitude search '~o'       # Obsolètes
```

---

## 102.5 - Gestion des paquets RPM et YUM

### 🎯 Objectifs clés
- Gérer paquets RPM (Red Hat Package Manager)
- Utiliser yum/dnf pour gestion de dépôts
- Comprendre différences avec système Debian

### 📦 Système de paquets RPM

**Format :** `.rpm` (Red Hat Package Manager)

**Distributions :**
- Red Hat Enterprise Linux (RHEL)
- CentOS / Rocky Linux / AlmaLinux
- Fedora
- openSUSE

**Outils :**
- **`rpm`** : Bas niveau, gestion paquets locaux
- **`yum`** : Haut niveau (RHEL 7, CentOS 7)
- **`dnf`** : Successeur de yum (RHEL 8+, Fedora)
- **`zypper`** : openSUSE

### 🔧 RPM - Red Hat Package Manager

#### Installation et suppression

```bash
# Installer paquet .rpm
sudo rpm -ivh package.rpm
# -i = install
# -v = verbose
# -h = hash (progress bar)

# Mettre à jour paquet
sudo rpm -Uvh package.rpm
# -U = upgrade (ou install si pas présent)

# Mise à jour seulement si déjà installé
sudo rpm -Fvh package.rpm
# -F = freshen

# Supprimer paquet
sudo rpm -e package_name

# Forcer suppression (ignorer dépendances)
sudo rpm -e --nodeps package_name
```

#### Recherche et information

```bash
# Lister tous les paquets installés
rpm -qa

# Lister avec filtre
rpm -qa | grep ssh

# Infos sur paquet installé
rpm -qi openssh-server

# Lister fichiers d'un paquet installé
rpm -ql openssh-server

# Quel paquet fournit un fichier
rpm -qf /usr/sbin/sshd
# openssh-server-8.0p1-4.el8.x86_64

# Lister contenu .rpm (sans installer)
rpm -qpl package.rpm

# Infos .rpm (sans installer)
rpm -qpi package.rpm

# Scripts d'installation
rpm -q --scripts openssh-server

# Dépendances d'un paquet
rpm -qR openssh-server

# Paquets qui dépendent de X
rpm -q --whatrequires libssl.so.1.1

# Fichiers de configuration
rpm -qc openssh-server

# Documentation
rpm -qd openssh-server
```

#### Vérification

```bash
# Vérifier paquet installé
rpm -V package_name

# Codes de sortie:
# S : Size differs
# M : Mode differs (permissions)
# 5 : MD5 sum differs
# D : Device major/minor number mismatch
# L : readLink(2) path mismatch
# U : User ownership differs
# G : Group ownership differs
# T : mTime differs
# P : caPabilities differ

# Vérifier tous les paquets
rpm -Va

# Vérifier intégrité .rpm
rpm -K package.rpm
# --checksig
```

#### Base de données RPM

```bash
# Reconstruire base de données (si corrompue)
sudo rpm --rebuilddb

# Import clé GPG
sudo rpm --import https://example.com/RPM-GPG-KEY

# Lister clés GPG
rpm -q gpg-pubkey --qf '%{name}-%{version}-%{release} --> %{summary}\n'
```

### 📦 YUM - Yellowdog Updater Modified

#### Commandes yum de base

```bash
# Mettre à jour cache
sudo yum check-update

# Mettre à jour tous les paquets
sudo yum update

# Mettre à jour paquet spécifique
sudo yum update package_name

# Installer paquet
sudo yum install nginx

# Installer sans confirmation
sudo yum install -y nginx

# Supprimer paquet
sudo yum remove nginx

# Rechercher paquet
yum search keyword

# Infos paquet
yum info nginx

# Lister paquets installés
yum list installed

# Lister paquets disponibles
yum list available

# Lister tous les paquets
yum list all

# Groupes de paquets
yum grouplist
yum groupinfo "Development Tools"
sudo yum groupinstall "Development Tools"
sudo yum groupremove "Development Tools"

# Historique
yum history
yum history info 5
sudo yum history undo 5

# Nettoyer cache
sudo yum clean all

# Vérifier dépendances
yum deplist nginx

# Quel paquet fournit un fichier
yum provides /usr/sbin/httpd
# httpd-2.4.37-30.el8.x86_64

# Lister dépôts
yum repolist
yum repolist all    # Inclus désactivés

# Installer depuis .rpm local
sudo yum localinstall package.rpm
```

#### Configuration `/etc/yum.conf`

```bash
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=3
```

#### Dépôts `/etc/yum.repos.d/`

**Exemple `/etc/yum.repos.d/custom.repo` :**
```bash
[custom-repo]
name=Custom Repository
baseurl=http://repo.example.com/centos/$releasever/$basearch/
enabled=1
gpgcheck=1
gpgkey=http://repo.example.com/RPM-GPG-KEY-custom
```

**Paramètres :**
- `[repo-id]` : Identifiant unique
- `name` : Nom descriptif
- `baseurl` : URL du dépôt
- `mirrorlist` : URL liste de miroirs (alternatif à baseurl)
- `enabled` : 1=activé, 0=désactivé
- `gpgcheck` : Vérifier signatures GPG
- `gpgkey` : URL clé GPG

**Variables :**
- `$releasever` : Version distribution (7, 8, 9...)
- `$basearch` : Architecture (x86_64, i386...)

**Gérer dépôts :**
```bash
# Activer dépôt
sudo yum-config-manager --enable repo-id

# Désactiver dépôt
sudo yum-config-manager --disable repo-id

# Ajouter dépôt
sudo yum-config-manager --add-repo https://example.com/repo.repo
```

#### Plugins yum

```bash
# Installer plugin
sudo yum install yum-plugin-name

# Plugins courants:
yum-plugin-fastestmirror    # Choisir miroir le plus rapide
yum-plugin-security         # Mises à jour sécurité
yum-plugin-versionlock      # Verrouiller versions

# Verrouiller version
sudo yum versionlock add nginx
sudo yum versionlock list
sudo yum versionlock delete nginx
```

### 📦 DNF - Dandified YUM

**DNF** = Successeur de yum (RHEL 8+, Fedora 22+)

#### Commandes dnf

```bash
# Syntaxe identique à yum (rétrocompatible)
sudo dnf update
sudo dnf install package
sudo dnf remove package
sudo dnf search keyword
dnf info package

# Améliorations DNF:
# - Plus rapide
# - Meilleure résolution dépendances
# - API Python 3

# Commandes spécifiques DNF
dnf repoquery --whatprovides /usr/bin/docker
dnf repoquery --requires docker

# Downgrade paquet
sudo dnf downgrade package

# Historique (amélioré)
dnf history
dnf history userinstalled    # Paquets installés manuellement

# Modules (Fedora/RHEL 8+)
dnf module list
dnf module install nodejs:14/default
dnf module enable nodejs:14
```

#### Configuration `/etc/dnf/dnf.conf`

```bash
[main]
gpgcheck=1
installonly_limit=3
clean_requirements_on_remove=True
best=True
skip_if_unavailable=False
fastestmirror=True
max_parallel_downloads=10
```

### 🆚 Comparaison Debian vs RPM

| Aspect | Debian/Ubuntu | Red Hat/CentOS |
|--------|---------------|----------------|
| **Format** | `.deb` | `.rpm` |
| **Outil bas niveau** | `dpkg` | `rpm` |
| **Outil haut niveau** | `apt`/`apt-get` | `yum`/`dnf` |
| **Sources** | `/etc/apt/sources.list` | `/etc/yum.repos.d/` |
| **Cache paquets** | `/var/cache/apt/` | `/var/cache/yum/` |
| **Base de données** | `/var/lib/dpkg/` | `/var/lib/rpm/` |
| **Scripts** | preinst, postinst, prerm, postrm | %pre, %post, %preun, %postun |
| **Dépendances** | Depends, Recommends | Requires |

---

## 📝 Résumé et points clés à retenir

### Commandes essentielles par catégorie

#### Partitionnement
```bash
fdisk, gdisk, parted
lsblk, blkid
mkfs.ext4, mkfs.xfs
mount, umount
/etc/fstab
```

#### LVM
```bash
pvcreate, pvs, pvdisplay
vgcreate, vgs, vgextend
lvcreate, lvs, lvextend, resize2fs
```

#### RAID
```bash
mdadm --create, mdadm --detail
cat /proc/mdstat
```

#### GRUB
```bash
grub-install, update-grub
/etc/default/grub
/etc/grub.d/40_custom
```

#### Bibliothèques
```bash
ldd, ldconfig
/etc/ld.so.conf
LD_LIBRARY_PATH
```

#### Paquets Debian
```bash
dpkg -i, dpkg -l, dpkg -L, dpkg -S
apt update, apt install, apt remove
apt search, apt show
/etc/apt/sources.list
```

#### Paquets RPM
```bash
rpm -ivh, rpm -qa, rpm -ql, rpm -qf
yum install, yum update, yum remove
yum search, yum info
/etc/yum.repos.d/
```

### Différences clés

| Concept | MBR | GPT |
|---------|-----|-----|
| Limite disque | 2 TB | 9.4 ZB |
| Partitions | 4 primaires | 128+ |
| Boot | BIOS | UEFI (ou BIOS) |
| Notation fdisk | /dev/sda1 | /dev/sda1 |
| Notation GRUB2 | (hd0,1) | (hd0,1) |

### Checklist avant examen

- [ ] Je comprends MBR vs GPT
- [ ] Je sais créer partitions (fdisk, parted)
- [ ] Je maîtrise LVM (PV, VG, LV)
- [ ] Je connais les niveaux RAID (0, 1, 5, 6, 10)
- [ ] Je peux installer et configurer GRUB 2
- [ ] Je sais dépanner GRUB (rescue mode)
- [ ] Je comprends les bibliothèques partagées (ldd, ldconfig)
- [ ] Je maîtrise apt (install, remove, search, update)
- [ ] Je maîtrise yum/dnf (install, remove, search, update)
- [ ] Je connais /etc/fstab et options de montage

---

## 🔬 Labs pratiques recommandés

### Lab 1 : Partitionnement et formatage
```bash
# 1. Créer partition avec fdisk
sudo fdisk /dev/sdb
# n, p, 1, [Enter], +10G, w

# 2. Formater en ext4
sudo mkfs.ext4 /dev/sdb1

# 3. Monter
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data

# 4. Tester
echo "test" | sudo tee /mnt/data/test.txt

# 5. Ajouter à fstab (avec UUID)
sudo blkid /dev/sdb1
# Copier UUID
echo "UUID=xxx /mnt/data ext4 defaults 0 2" | sudo tee -a /etc/fstab

# 6. Tester fstab
sudo umount /mnt/data
sudo mount -a
ls /mnt/data
```

### Lab 2 : LVM de base
```bash
# 1. Créer PV
sudo pvcreate /dev/sdb

# 2. Créer VG
sudo vgcreate vg_test /dev/sdb

# 3. Créer LV de 5G
sudo lvcreate -L 5G -n lv_test vg_test

# 4. Formater
sudo mkfs.ext4 /dev/vg_test/lv_test

# 5. Monter
sudo mkdir /mnt/lvm_test
sudo mount /dev/vg_test/lv_test /mnt/lvm_test

# 6. Étendre (+2G)
sudo lvextend -L +2G /dev/vg_test/lv_test
sudo resize2fs /dev/vg_test/lv_test

# 7. Vérifier
df -h /mnt/lvm_test
```

### Lab 3 : Gestion paquets (Debian/Ubuntu)
```bash
# 1. Mettre à jour cache
sudo apt update

# 2. Rechercher paquet
apt search nginx

# 3. Infos paquet
apt show nginx

# 4. Installer
sudo apt install nginx

# 5. Vérifier fichiers
dpkg -L nginx

# 6. Vérifier dépendances binaire
ldd /usr/sbin/nginx

# 7. Supprimer
sudo apt remove nginx

# 8. Autoremove
sudo apt autoremove
```

### Lab 4 : Configuration GRUB
```bash
# 1. Sauvegarder config
sudo cp /etc/default/grub /etc/default/grub.backup

# 2. Modifier timeout
sudo nano /etc/default/grub
# GRUB_TIMEOUT=10

# 3. Ajouter paramètre kernel
# GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"

# 4. Régénérer
sudo update-grub

# 5. Vérifier config générée
grep timeout /boot/grub/grub.cfg

# 6. Restaurer (si besoin)
sudo cp /etc/default/grub.backup /etc/default/grub
sudo update-grub
```

---

## 📖 Ressources complémentaires

- **Man pages :** `man fdisk`, `man lvm`, `man grub`, `man apt`, `man yum`
- **Documentation LPI :** LPI-Learning-Material-101-500-fr.md
- **Cours KodeKloud :** Modules Sujet 102
- **Anki :** 84 cartes Sujet 102

---

**🎯 Objectif : Maîtriser le Sujet 102 à 100% avant de passer au Sujet 103 !**

*Prochaine étape : [QCM-Sujet-102.md](../QCM/QCM-Sujet-102.md) pour tester vos connaissances !*
