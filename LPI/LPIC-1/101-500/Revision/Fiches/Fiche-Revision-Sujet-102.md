# 📄 Fiche Sujet 102 : Installation Linux et Gestion Packages

**Poids : 10 points (25%)** | Révision rapide

---

## 102.1 : Dimensionner Disques (2 pts)

### Schéma partitionnement
```bash
# Standard
/boot    500MB-1GB   ext4    (kernel, initrd)
swap     = RAM       swap    (si RAM < 8GB)
/        20-50GB     ext4    (système)
/home    Reste       ext4    (données users)

# Serveur
/        20GB        ext4
/boot    1GB         ext4
/var     10-50GB     ext4    (logs, cache)
/tmp     5-10GB      ext4    (temporaire)
/home    Reste       ext4
swap     1-2x RAM
```

### MBR vs GPT
| Aspect | MBR | GPT |
|--------|-----|-----|
| **Taille max** | 2 TB | >2 TB (9 ZB) |
| **Partitions** | 4 primaires | 128 |
| **Boot** | BIOS | UEFI |
| **Backup** | Non | Oui (CRC32) |
| **Outil** | fdisk | gdisk, parted |

### Swap sizing
```
RAM ≤ 2GB   → swap = 2x RAM
RAM 2-8GB   → swap = RAM
RAM > 8GB   → swap = 8GB (ou 0.5x RAM)
Hibernate   → swap ≥ RAM
```

---

## 102.2 : Bootloader GRUB (2 pts)

### GRUB Legacy (GRUB 1)
```bash
# Config
/boot/grub/menu.lst        # Ou grub.conf

# Installation
grub-install /dev/sda

# Structure menu.lst
default 0
timeout 10
title Ubuntu
  root (hd0,0)
  kernel /vmlinuz root=/dev/sda1 ro
  initrd /initrd.img
```

### GRUB 2 (actuel)
```bash
# Config principal
/boot/grub/grub.cfg               # Généré AUTO (NE PAS éditer)
/etc/default/grub                 # Paramètres
/etc/grub.d/                      # Scripts génération

# Paramètres /etc/default/grub
GRUB_TIMEOUT=10
GRUB_DEFAULT=0
GRUB_CMDLINE_LINUX="quiet splash"
GRUB_DISABLE_RECOVERY=false

# Commandes
update-grub                       # Debian/Ubuntu
grub2-mkconfig -o /boot/grub2/grub.cfg  # RHEL/CentOS

grub-install /dev/sda             # Installer GRUB
grub-install --boot-directory=/mnt/boot /dev/sda  # Disque externe
```

### Boot kernel manuel (GRUB rescue)
```
grub> set root=(hd0,1)
grub> linux /vmlinuz root=/dev/sda1 ro
grub> initrd /initrd.img
grub> boot
```

### Paramètres kernel boot
```
quiet           # Messages réduits
splash          # Écran splash
single          # Single-user mode
1, S            # Runlevel 1 (rescue)
3               # Runlevel 3 (multi-user CLI)
init=/bin/bash  # Shell root direct (reset password)
ro              # Read-only root
rw              # Read-write root
```

---

## 102.3 : Gestion Bibliothèques (1 pt)

### Localisation libs
```bash
/lib                # Libs système essentielles (32-bit)
/lib64              # Libs 64-bit
/usr/lib            # Libs applications
/usr/local/lib      # Libs custom
```

### Commandes
```bash
ldd /bin/ls                  # Dépendances binaire
ldd /usr/bin/python3

ldconfig                     # MAJ cache libs
ldconfig -p                  # Affiche cache
ldconfig -v                  # Verbose

# Config
/etc/ld.so.conf              # Fichier principal
/etc/ld.so.conf.d/*.conf     # Includes
/etc/ld.so.cache             # Cache (binaire)

# Variables
LD_LIBRARY_PATH=/custom/libs  # Chemin libs custom (export)
```

---

## 102.4 : Packages Debian (3 pts)

### dpkg (bas niveau)
```bash
# Installation
dpkg -i package.deb              # Installer
dpkg -r package                  # Supprimer (garde config)
dpkg -P package                  # Purge (supprime config)

# Infos
dpkg -l                          # Liste installés
dpkg -l | grep package           # Chercher
dpkg -L package                  # Fichiers installés
dpkg -S /path/to/file            # Package propriétaire
dpkg -s package                  # Statut/infos
dpkg --get-selections            # Liste sélections

# Config
dpkg-reconfigure package         # Reconfigurer
dpkg-reconfigure tzdata          # Timezone
dpkg-reconfigure locales         # Langues
```

### APT (haut niveau)
```bash
# MAJ bases
apt update                       # MAJ listes packages
apt upgrade                      # MAJ packages installés
apt full-upgrade                 # MAJ + résout dépendances (anciennement dist-upgrade)

# Installation
apt install package              # Installer
apt install package1 package2    # Multiples
apt reinstall package            # Réinstaller
apt remove package               # Supprimer (garde config)
apt purge package                # Purge complète
apt autoremove                   # Supprimer dépendances inutiles

# Recherche
apt search keyword               # Chercher
apt show package                 # Détails
apt list --installed             # Liste installés
apt list --upgradable            # MAJ disponibles

# Cache
apt-cache search keyword         # Chercher
apt-cache show package           # Infos
apt-cache depends package        # Dépendances
apt-cache policy package         # Versions disponibles
```

### Configuration sources
```bash
# Fichiers
/etc/apt/sources.list            # Sources principal
/etc/apt/sources.list.d/*.list   # Sources additionnelles

# Format sources.list
deb http://archive.ubuntu.com/ubuntu jammy main restricted
deb-src http://archive.ubuntu.com/ubuntu jammy main

# Composants
main          # Officiel open-source
restricted    # Pilotes propriétaires
universe      # Communauté
multiverse    # Logiciels non-libres
```

---

## 102.5 : Packages RPM (3 pts)

### RPM (bas niveau)
```bash
# Installation
rpm -i package.rpm               # Installer
rpm -U package.rpm               # Upgrade (install si absent)
rpm -F package.rpm               # Freshen (upgrade si déjà installé)
rpm -e package                   # Supprimer

# Options installation
rpm -ivh package.rpm             # Install + verbose + hash progress
rpm -Uvh package.rpm             # Upgrade + verbose + hash
rpm --force                      # Forcer
rpm --nodeps                     # Ignorer dépendances (⚠️)

# Requêtes
rpm -qa                          # Query all (liste tous)
rpm -qi package                  # Query info
rpm -ql package                  # Query list (fichiers)
rpm -qf /path/to/file            # Query file (package propriétaire)
rpm -qd package                  # Query documentation
rpm -qc package                  # Query configuration files
rpm -q --scripts package         # Scripts pré/post install

# Vérification
rpm -V package                   # Verify (intégrité)
rpm -Va                          # Verify all
```

### YUM (RHEL/CentOS 6-7)
```bash
# MAJ
yum check-update                 # Vérifier MAJ
yum update                       # Tout mettre à jour
yum update package               # MAJ package spécifique

# Installation
yum install package              # Installer
yum reinstall package            # Réinstaller
yum remove package               # Supprimer
yum autoremove                   # Supprimer dépendances inutiles

# Recherche
yum search keyword               # Chercher
yum info package                 # Infos
yum list installed               # Liste installés
yum list available               # Disponibles
yum provides /path/to/file       # Package contenant fichier

# Groupes
yum grouplist                    # Liste groupes
yum groupinstall "Group Name"    # Installer groupe
yum groupremove "Group Name"     # Supprimer groupe

# Repos
yum repolist                     # Liste repos actifs
yum repolist all                 # Tous repos
yum-config-manager --enable repo # Activer repo
yum-config-manager --disable repo # Désactiver

# Cache
yum clean all                    # Nettoyer cache
yum makecache                    # Créer cache
```

### DNF (RHEL/CentOS 8+, Fedora)
```bash
# Syntaxe identique à YUM
dnf update
dnf install package
dnf search keyword
dnf info package
dnf remove package
dnf autoremove
dnf clean all
```

### Configuration repos
```bash
# Fichiers
/etc/yum.repos.d/*.repo

# Format .repo
[epel]
name=EPEL Repository
baseurl=https://download.fedoraproject.org/pub/epel/8/Everything/x86_64/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-8
```

---

## 102.6 : Virtualisation Linux (1 pt)

### Concepts
| Type | Description | Exemples |
|------|-------------|----------|
| **Type 1** | Hyperviseur bare-metal | KVM, Xen, VMware ESXi |
| **Type 2** | Hyperviseur hosted | VirtualBox, VMware Workstation |
| **Conteneurs** | OS-level virtualization | Docker, LXC, Podman |

### Fichiers /proc virtualisation
```bash
/proc/cpuinfo        # Flags: vmx (Intel VT-x), svm (AMD-V)
/proc/modules        # Modules kernel (kvm, kvm_intel, kvm_amd)

# Vérifier support
grep -E 'vmx|svm' /proc/cpuinfo
lsmod | grep kvm
```

### Commandes
```bash
# Infos VM
virsh list --all             # Liste VMs (libvirt)
docker ps                    # Conteneurs Docker
lxc-ls                       # Conteneurs LXC

# Cloud-init
cloud-init                   # Init cloud instances
```

---

## 🎯 Points clés examen

1. **Swap** : 2x RAM si RAM<2GB, = RAM si 2-8GB
2. **MBR** : 2TB max, 4 partitions, BIOS
3. **GPT** : >2TB, 128 partitions, UEFI
4. **GRUB 2 config** : /etc/default/grub + update-grub
5. **Kernel param** : `init=/bin/bash` (reset password)
6. **ldconfig** : MAJ cache libs (/etc/ld.so.cache)
7. **dpkg -i** : Installer .deb
8. **apt update** avant apt install
9. **rpm -qa** : Liste tous packages
10. **rpm -qf /file** : Package propriétaire
11. **yum provides** : Chercher fichier
12. **sources.list** : deb vs deb-src
13. **/etc/yum.repos.d/** : Repos RPM
14. **Virtualisation flags** : vmx (Intel), svm (AMD)

---

## 📋 Checklist révision

- [ ] Schéma partitionnement standard
- [ ] Calcul taille swap selon RAM
- [ ] MBR vs GPT (limites, outils)
- [ ] /etc/default/grub + update-grub
- [ ] Boot manuel GRUB (set root, linux, initrd, boot)
- [ ] ldconfig -p (cache libs)
- [ ] dpkg -i/-r/-P/-L/-S
- [ ] apt update vs upgrade vs full-upgrade
- [ ] rpm -qa/-qi/-ql/-qf
- [ ] yum install/search/provides
- [ ] Format /etc/yum.repos.d/*.repo
- [ ] Vérifier support virtualisation (vmx/svm)
