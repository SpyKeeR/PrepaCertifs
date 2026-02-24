# 📘 Notes de Révision - Sujet 101 : Architecture Système

> **Poids du sujet :** 8 points (~20% de l'examen)  
> **Temps de lecture estimé :** 2-3 heures  
> **Niveau :** Fondamental - Essentiel à maîtriser !

---

## 📋 Table des matières

- [101.1 - Détermination et configuration des paramètres du matériel (Poids: 2)](#1011---détermination-et-configuration-des-paramètres-du-matériel)
- [101.2 - Démarrage du système (Poids: 3)](#1012---démarrage-du-système)
- [101.3 - Modification des runlevels / boot targets et arrêt ou redémarrage du système (Poids: 3)](#1013---modification-des-runlevels--boot-targets-et-arrêt-ou-redémarrage-du-système)

---

## 101.1 - Détermination et configuration des paramètres du matériel

### 🎯 Objectifs clés
- Activer et désactiver périphériques intégrés
- Différencier types de périphériques de stockage
- Déterminer ressources matérielles
- Utiliser outils d'inspection matérielle
- Comprendre sysfs, udev, dbus

### 📁 Fichiers et répertoires importants

#### `/proc/` - Système de fichiers virtuel
Interface vers les informations du noyau et des processus.

```bash
# Informations CPU
cat /proc/cpuinfo

# Informations mémoire
cat /proc/meminfo

# Version du kernel
cat /proc/version

# Modules kernel chargés
cat /proc/modules

# Périphériques de caractères et blocs
cat /proc/devices

# Partitions montées
cat /proc/mounts
```

**Points clés `/proc/` :**
- Fichiers virtuels (n'existent pas physiquement sur disque)
- Créés dynamiquement par le kernel
- Lecture seule (sauf certains dans `/proc/sys/`)
- Un sous-dossier par processus (PID)

#### `/sys/` - Interface sysfs
Représentation hiérarchique des périphériques et du kernel.

```bash
# Structure de /sys
ls /sys/
# block/  - Périphériques blocs
# bus/    - Bus système (PCI, USB, etc.)
# class/  - Classes de périphériques
# dev/    - Numéros majeur/mineur
# devices/- Tous les périphériques
# firmware/- Firmware (ex: EFI)
# kernel/ - Paramètres kernel
# module/ - Modules chargés
# power/  - Gestion énergie

# Exemple : Lister cartes réseau
ls /sys/class/net/

# Exemple : Adresse MAC d'une interface
cat /sys/class/net/eth0/address
```

**Points clés `/sys/` :**
- Introduit dans kernel 2.6
- Plus organisé que `/proc/`
- Utilisé par `udev` pour créer `/dev/`
- Certains fichiers modifiables pour config matériel

#### `/dev/` - Fichiers de périphériques
Fichiers spéciaux représentant les périphériques.

```bash
# Types de fichiers dans /dev/
ls -l /dev/ | head -20

# Périphériques bloc (b) - Stockage
# Ex: sda, sdb, nvme0n1, sr0

# Périphériques caractères (c) - E/S série
# Ex: tty, random, null, zero

# Fichiers spéciaux importants
/dev/null   # Trou noir (ignore toutes écritures)
/dev/zero   # Source infinie de zéros
/dev/random # Générateur aléatoire (bloquant)
/dev/urandom# Générateur aléatoire (non-bloquant)
```

**Nomenclature des disques :**
- **SATA/SCSI :** `/dev/sda`, `/dev/sdb`, etc.
  - Partitions : `/dev/sda1`, `/dev/sda2`
- **NVMe :** `/dev/nvme0n1`, `/dev/nvme0n2`
  - Partitions : `/dev/nvme0n1p1`, `/dev/nvme0n1p2`
- **CD/DVD :** `/dev/sr0`, `/dev/sr1`
- **Anciens IDE :** `/dev/hda`, `/dev/hdb` (obsolètes)

### 🔧 Commandes d'inspection matérielle

#### `lspci` - Lister périphériques PCI

```bash
# Liste basique
lspci

# Format détaillé (-v = verbose)
lspci -v

# Très détaillé
lspci -vv

# Ultra détaillé (pour debug)
lspci -vvv

# Afficher numéros hexadécimaux (vendor/device ID)
lspci -nn

# Sélectionner périphérique spécifique
lspci -s 01:00.0

# Afficher arbre hiérarchique
lspci -t

# Afficher modules kernel utilisés
lspci -k

# Sortie lisible par machine
lspci -m
```

**Exemple de sortie :**
```
01:00.0 VGA compatible controller: NVIDIA Corporation GM107 [GeForce GTX 750 Ti] (rev a2)
04:02.0 Network controller: Ralink corp. RT2561/RT61 802.11g PCI
```

**Décoder l'adresse PCI : `01:00.0`**
- `01` = Bus
- `00` = Device (slot)
- `0` = Function

#### `lsusb` - Lister périphériques USB

```bash
# Liste basique
lsusb

# Format détaillé
lsusb -v

# Arbre hiérarchique
lsusb -t

# Sélectionner périphérique par ID
lsusb -d 1234:5678

# Sélectionner par bus et device
lsusb -s 001:005
```

**Exemple de sortie :**
```
Bus 001 Device 029: ID 1781:0c9f Multiple Vendors USBtiny
Bus 001 Device 028: ID 093a:2521 Pixart Imaging, Inc. Optical Mouse
```

**Décoder :**
- `Bus 001` = Port USB principal
- `Device 029` = Numéro du périphérique
- `ID 1781:0c9f` = Vendor ID : Product ID

#### `lsblk` - Lister périphériques blocs

```bash
# Liste basique
lsblk

# Afficher système de fichiers
lsblk -f

# Taille en octets
lsblk -b

# Format JSON
lsblk -J

# Format personnalisé
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT
```

**Exemple de sortie :**
```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  500G  0 disk 
├─sda1   8:1    0  512M  0 part /boot/efi
├─sda2   8:2    0  450G  0 part /
└─sda3   8:3    0   50G  0 part [SWAP]
sr0     11:0    1 1024M  0 rom  
```

#### `lscpu` - Informations CPU

```bash
# Afficher infos CPU
lscpu

# Format parsable
lscpu --parse

# Infos étendues
lscpu --extended
```

**Informations affichées :**
- Architecture
- Nombre de CPUs
- Modèle
- MHz
- Caches (L1, L2, L3)
- Virtualisation (VT-x, AMD-V)

### 📦 Gestion des modules kernel

#### Comprendre les modules
- **Module = Driver** pour un périphérique
- Chargeables dynamiquement (sans recompiler kernel)
- Stockés dans `/lib/modules/$(uname -r)/`
- Configuration dans `/etc/modprobe.d/`

#### `lsmod` - Lister modules chargés

```bash
# Lister tous les modules
lsmod

# Filtrer par nom
lsmod | grep e1000

# Compter modules chargés
lsmod | wc -l
```

**Sortie :**
```
Module                  Size  Used by
kvm_intel             138528  0
kvm                   421021  1 kvm_intel
snd_hda_intel          44075  7
```

Colonnes :
- **Module** : Nom du module
- **Size** : Taille en mémoire (octets)
- **Used by** : Nombre d'utilisations + modules dépendants

#### `modinfo` - Informations sur un module

```bash
# Infos complètes sur module
modinfo e1000

# Afficher seulement les paramètres
modinfo -p nouveau

# Afficher seulement la description
modinfo -d bluetooth

# Afficher dépendances
modinfo -F depends e1000e
```

**Informations affichées :**
- `filename` : Chemin du fichier .ko
- `description` : Description
- `author` : Auteur
- `license` : Licence (GPL, etc.)
- `alias` : Alias
- `depends` : Dépendances
- `parm` : Paramètres configurables

#### `modprobe` - Charger/décharger modules

```bash
# Charger un module (avec dépendances)
sudo modprobe bluetooth

# Décharger un module
sudo modprobe -r bluetooth

# Décharger module + dépendances inutilisées
sudo modprobe -r --remove-dependencies bluetooth

# Simulation (dry-run)
modprobe -n bluetooth

# Afficher dépendances
modprobe --show-depends e1000e
```

**Différences `modprobe` vs `insmod` :**
| Commande | Dépendances | Chemin | Usage |
|----------|-------------|--------|-------|
| `modprobe` | ✅ Gère auto | Nom module | Production |
| `insmod` | ❌ Manuel | Chemin .ko | Debug |
| `rmmod` | ❌ Erreur si utilisé | Nom module | Direct |

#### Configuration des modules

**Fichier `/etc/modprobe.d/*.conf` :**
```bash
# Exemple: /etc/modprobe.d/blacklist.conf
# Empêcher chargement d'un module
blacklist nouveau

# Exemple: /etc/modprobe.d/alsa-base.conf
# Définir paramètres de module
options snd-hda-intel model=auto

# Exemple: Créer alias
alias wifi iwlwifi
```

**Tester paramètres temporairement :**
```bash
# Charger module avec paramètres
sudo modprobe nouveau modeset=0
```

### 🔌 udev - Gestionnaire de périphériques

#### Qu'est-ce que udev ?
- **U**ser-space **DEV**ice manager
- Gère `/dev/` dynamiquement
- Crée noms de périphériques persistants
- Exécute actions lors détection matériel

#### Règles udev
**Emplacement :** `/etc/udev/rules.d/*.rules` et `/lib/udev/rules.d/`

**Exemple de règle :**
```bash
# /etc/udev/rules.d/99-usb-custom.rules
# Créer lien symbolique pour clé USB spécifique
SUBSYSTEM=="block", ATTRS{idVendor}=="1234", ATTRS{idProduct}=="5678", SYMLINK+="my_usb_key"
```

**Commandes udev :**
```bash
# Recharger règles
sudo udevadm control --reload

# Déclencher événements
sudo udevadm trigger

# Monitorer événements en temps réel
sudo udevadm monitor

# Informations sur périphérique
udevadm info /dev/sda

# Tester règle
udevadm test /sys/class/block/sda
```

### 📡 D-Bus - Communication inter-processus

#### Qu'est-ce que D-Bus ?
- **Desktop BUS** = Bus de communication
- Permet aux processus de communiquer
- Deux types de bus :
  - **System bus** : Communication système
  - **Session bus** : Communication utilisateur

#### Commandes D-Bus

```bash
# Lister services sur system bus
dbus-send --system --dest=org.freedesktop.DBus --print-reply /org/freedesktop/DBus org.freedesktop.DBus.ListNames

# Machine ID unique
dbus-uuidgen --get

# Monitorer bus système
dbus-monitor --system
```

### 🎓 Concepts clés BIOS vs UEFI

#### BIOS (Basic Input/Output System)
- **Ancien standard** (années 1980)
- **Limite :** Disques max 2 TB
- **Partitions :** Max 4 primaires (MBR)
- **Boot :** Lit MBR (512 octets)
- **Interface :** Mode texte

#### UEFI (Unified Extensible Firmware Interface)
- **Nouveau standard** (2000+)
- **Avantages :**
  - Disques > 2 TB (GPT)
  - Partitions illimitées
  - Secure Boot
  - Interface graphique
  - Réseau intégré
- **Boot :** Lit partition ESP (EFI System Partition)
- **Format :** FAT32 sur /boot/efi

**Vérifier type de firmware :**
```bash
# Si dossier existe = UEFI
ls /sys/firmware/efi

# Sinon = BIOS
```

---

## 101.2 - Démarrage du système

### 🎯 Objectifs clés
- Comprendre processus de boot
- Configurer bootloader (GRUB 2)
- Passer paramètres au kernel
- Vérifier événements de boot

### 🔄 Processus de démarrage (séquence complète)

```
1. POWER ON
   ↓
2. POST (Power-On Self-Test)
   ↓
3. BIOS/UEFI
   - Initialise matériel
   - Lit configuration boot
   ↓
4. BOOTLOADER (GRUB 2)
   - BIOS: Lit MBR → charge GRUB
   - UEFI: Lit ESP → charge GRUB EFI
   ↓
5. KERNEL
   - Décompresse kernel (vmlinuz)
   - Charge en mémoire
   - Initialise drivers
   ↓
6. INITRAMFS / INITRD
   - Mini-système temporaire en RAM
   - Contient drivers essentiels
   - Monte vrai système de fichiers
   ↓
7. INIT / SYSTEMD (PID 1)
   - Premier processus
   - Lance services système
   ↓
8. RUNLEVEL / TARGET
   - Multi-user mode
   - Graphical mode
   ↓
9. LOGIN PROMPT
   - Getty sur TTY
   - Display Manager (graphique)
```

### 🥾 GRUB 2 (GRand Unified Bootloader)

#### Fichiers de configuration

```bash
# Configuration principale (NE PAS ÉDITER DIRECTEMENT)
/boot/grub/grub.cfg  # ou /boot/grub2/grub.cfg

# Fichier à éditer pour modifications
/etc/default/grub

# Scripts de génération
/etc/grub.d/
├── 00_header
├── 05_debian_theme
├── 10_linux          # Détecte kernels Linux
├── 20_linux_xen
├── 30_os-prober      # Détecte autres OS
├── 40_custom         # Entrées personnalisées
└── 41_custom
```

#### Configuration de base `/etc/default/grub`

```bash
# Éditer configuration
sudo nano /etc/default/grub

# Paramètres importants:
GRUB_DEFAULT=0              # Entrée par défaut (0 = première)
GRUB_TIMEOUT=5              # Délai en secondes
GRUB_TIMEOUT_STYLE=menu     # hidden, countdown, menu
GRUB_CMDLINE_LINUX=""       # Paramètres kernel (tous modes)
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"  # Paramètres par défaut
GRUB_DISABLE_RECOVERY="false"  # Activer mode recovery

# Après modification, regénérer grub.cfg:
sudo update-grub            # Debian/Ubuntu
sudo grub2-mkconfig -o /boot/grub2/grub.cfg  # Red Hat/CentOS
```

#### Entrées personnalisées `/etc/grub.d/40_custom`

```bash
#!/bin/sh
exec tail -n +3 $0
# Entrée personnalisée exemple

menuentry "Mon Linux Custom" {
    set root=(hd0,1)
    linux /vmlinuz root=/dev/sda1 ro quiet
    initrd /initrd.img
}
```

**Syntaxe GRUB pour disques :**
- `(hd0,1)` = Premier disque, première partition
  - **Attention :** Disques comptés depuis 0, partitions depuis 1 (GRUB 2)
  - GRUB Legacy : partitions depuis 0 aussi
- `(hd1,3)` = Deuxième disque, troisième partition

#### Commandes GRUB (mode shell)

Accès au shell GRUB : Appuyer sur `c` au menu boot

```bash
# Lister disques et partitions
ls

# Afficher contenu partition
ls (hd0,1)/

# Définir partition root
set root=(hd0,1)

# Charger kernel
linux /vmlinuz root=/dev/sda1 ro

# Charger initramfs
initrd /initrd.img

# Booter
boot

# Éditer entrée : Appuyer sur 'e' au menu
# Valider modifications : Ctrl+X ou F10
```

#### Installation de GRUB

```bash
# Installer sur MBR (BIOS)
sudo grub-install /dev/sda

# Installer sur ESP (UEFI)
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi

# Vérifier installation
sudo grub-install --version
```

### 🐧 Kernel et initramfs

#### Fichiers kernel dans `/boot`

```bash
ls -lh /boot/
# Fichiers importants:
vmlinuz-5.15.0-58-generic       # Kernel compressé
initrd.img-5.15.0-58-generic    # ou initramfs (RAM disk initial)
System.map-5.15.0-58-generic    # Table symboles kernel
config-5.15.0-58-generic        # Configuration compilation kernel
```

#### Rôle de initramfs/initrd

**Problème :** Kernel a besoin de drivers pour lire système de fichiers root, mais ces drivers sont SUR le système de fichiers root !

**Solution :** initramfs (Initial RAM File System)
- Mini-système de fichiers en RAM
- Contient drivers essentiels (SATA, SCSI, LVM, RAID, filesystem)
- Monte le vrai `/` 
- Passe contrôle à vrai système

**Créer/Mettre à jour initramfs :**
```bash
# Debian/Ubuntu
sudo update-initramfs -u

# Red Hat/CentOS
sudo dracut --force

# Lister contenu
lsinitramfs /boot/initrd.img-5.15.0-58-generic
```

### ⚙️ Paramètres kernel au boot

Passer des paramètres au kernel pour modifier son comportement.

#### Paramètres courants

```bash
# Mode single user (maintenance)
single
# ou
1
# ou
init=/bin/bash

# Mode recovery
recovery

# Désactiver quiet/splash (voir messages boot)
# Supprimer: quiet splash

# Changer partition root
root=/dev/sda2
# ou
root=UUID=xxxxx-xxxxx-xxxxx

# Mode lecture seule
ro

# Mode lecture-écriture
rw

# Désactiver Plymouth (splash screen)
plymouth.enable=0

# Limiter mémoire RAM
mem=2G

# Désactiver ACPI
acpi=off

# Désactiver APIC
noapic

# Définir runlevel/target
systemd.unit=multi-user.target
# ou
3

# Debug mode
debug

# Mode verbose
verbose

# Désactiver Kernel Mode Setting (GPU)
nomodeset

# Paramètres réseau (pour boot réseau)
ip=dhcp
ip=192.168.1.100::192.168.1.1:255.255.255.0:myhost:eth0:off
```

#### Appliquer paramètres (temporaire)

1. Au menu GRUB, appuyer sur `e`
2. Trouver ligne commençant par `linux`
3. Ajouter paramètres à la fin
4. `Ctrl+X` ou `F10` pour booter

#### Appliquer paramètres (permanent)

```bash
# Éditer /etc/default/grub
sudo nano /etc/default/grub

# Modifier ligne
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
# en (exemple)
GRUB_CMDLINE_LINUX_DEFAULT="quiet"

# Régénérer config
sudo update-grub
```

### 📋 Vérifier événements de boot

#### `dmesg` - Messages kernel

```bash
# Afficher tous les messages
dmesg

# Avec horodatage lisible
dmesg -T

# Avec couleurs
dmesg -L

# Niveau de log spécifique
dmesg -l err   # Erreurs seulement
dmesg -l warn  # Warnings

# Effacer buffer
sudo dmesg -C

# Suivre en temps réel
dmesg -w

# Filtrer par mot-clé
dmesg | grep -i usb
```

**Niveaux de log :**
- `emerg` : Urgence (système inutilisable)
- `alert` : Action immédiate requise
- `crit` : Critique
- `err` : Erreur
- `warn` : Warning
- `notice` : Notice
- `info` : Information
- `debug` : Debug

#### `journalctl` - Logs systemd

```bash
# Logs depuis dernier boot
journalctl -b

# Boot précédent
journalctl -b -1

# Boot spécifique
journalctl --list-boots   # Lister boots
journalctl -b <ID>

# Suivre en temps réel
journalctl -f

# Niveau priorité
journalctl -p err

# Service spécifique
journalctl -u sshd.service

# Kernel messages seulement
journalctl -k

# Depuis date
journalctl --since "2026-01-28 10:00"

# Vers date
journalctl --until "2026-01-28 12:00"

# Inverser ordre (plus récent d'abord)
journalctl -r

# Format JSON
journalctl -o json

# Vérifier intégrité
journalctl --verify
```

---

## 101.3 - Modification des runlevels / boot targets et arrêt ou redémarrage du système

### 🎯 Objectifs clés
- Comprendre runlevels (SysVinit) et targets (systemd)
- Changer de runlevel/target
- Arrêter, redémarrer, hiberner système
- Notifier utilisateurs avant shutdown

### 🔢 Runlevels (SysVinit - ancien système)

#### Tableau des runlevels

| Runlevel | Description | Usage |
|----------|-------------|-------|
| **0** | Halt | Arrêt système |
| **1** | Single-user mode | Maintenance (root only, pas réseau) |
| **2** | Multi-user sans réseau | Rarement utilisé |
| **3** | Multi-user avec réseau | Mode texte (serveur) |
| **4** | Inutilisé | Personnalisable |
| **5** | Multi-user graphique | Mode graphique (desktop) |
| **6** | Reboot | Redémarrage |

#### Commandes runlevel (SysVinit)

```bash
# Afficher runlevel actuel
runlevel
# Sortie: N 5
# N = runlevel précédent (N si aucun changement)
# 5 = runlevel actuel

# Changer runlevel
sudo telinit 3   # Passer en mode texte
sudo telinit 5   # Passer en mode graphique
sudo telinit 1   # Mode single-user
sudo telinit 6   # Redémarrer
sudo telinit 0   # Arrêter

# Runlevel par défaut (ancien)
# Défini dans /etc/inittab
# id:5:initdefault:
```

#### Scripts de runlevel

```bash
# Scripts pour chaque runlevel
/etc/rc0.d/    # Runlevel 0 (halt)
/etc/rc1.d/    # Runlevel 1 (single)
/etc/rc2.d/    # Runlevel 2
/etc/rc3.d/    # Runlevel 3
/etc/rc4.d/    # Runlevel 4
/etc/rc5.d/    # Runlevel 5 (graphical)
/etc/rc6.d/    # Runlevel 6 (reboot)

# Scripts réels dans
/etc/init.d/

# Liens symboliques dans /etc/rcX.d/
# K = Kill (arrêter service)
# S = Start (démarrer service)
# Numéro = Ordre d'exécution

# Exemple:
ls /etc/rc3.d/
# S01networking -> ../init.d/networking
# S02cron -> ../init.d/cron
# K01apache2 -> ../init.d/apache2
```

### 🎯 Systemd Targets (système moderne)

#### Targets principaux

| Target | Équivalent Runlevel | Description |
|--------|---------------------|-------------|
| `poweroff.target` | 0 | Arrêt système |
| `rescue.target` | 1 | Mode rescue (single-user) |
| `multi-user.target` | 3 | Multi-user texte |
| `graphical.target` | 5 | Multi-user graphique |
| `reboot.target` | 6 | Redémarrage |
| `emergency.target` | - | Mode urgence (minimal) |

#### Commandes systemd

```bash
# Afficher target actuel
systemctl get-default

# Changer target par défaut
sudo systemctl set-default multi-user.target
sudo systemctl set-default graphical.target

# Changer target temporairement (session actuelle)
sudo systemctl isolate multi-user.target
sudo systemctl isolate graphical.target
sudo systemctl isolate rescue.target

# Lister tous les targets
systemctl list-units --type=target

# Lister targets actifs
systemctl list-units --type=target --state=active

# Voir dépendances target
systemctl list-dependencies graphical.target
```

#### Fichiers target

```bash
# Targets système dans
/lib/systemd/system/*.target

# Targets personnalisés dans
/etc/systemd/system/*.target

# Lien symbolique default
ls -l /etc/systemd/system/default.target
# -> /lib/systemd/system/graphical.target
```

### 🔌 Arrêt et redémarrage

#### Commande `shutdown`

```bash
# Arrêter dans 10 minutes
sudo shutdown -h +10

# Arrêter dans 5 minutes avec message
sudo shutdown -h +5 "Maintenance système, déconnectez-vous!"

# Arrêter à heure précise (format HH:MM)
sudo shutdown -h 23:00

# Arrêter maintenant
sudo shutdown -h now

# Redémarrer dans 5 minutes
sudo shutdown -r +5

# Redémarrer maintenant
sudo shutdown -r now

# Annuler shutdown planifié
sudo shutdown -c

# Mettre en veille
sudo shutdown -H now
```

**Options shutdown :**
- `-h` : Halt (arrêt)
- `-r` : Reboot (redémarrage)
- `-H` : Halt (mais pas power off)
- `-P` : Power off
- `-c` : Cancel
- `-k` : Fake (envoie message mais n'arrête pas)

#### Autres commandes d'arrêt

```bash
# Halt (arrêt sans power off)
sudo halt

# Power off (arrêt complet)
sudo poweroff

# Reboot
sudo reboot

# Systemctl (méthode moderne)
sudo systemctl halt
sudo systemctl poweroff
sudo systemctl reboot
sudo systemctl suspend       # Mise en veille
sudo systemctl hibernate     # Hibernation
sudo systemctl hybrid-sleep  # Hybride
```

### 💬 Notification utilisateurs

#### `wall` - Write to all

```bash
# Envoyer message à tous les utilisateurs connectés
wall "Attention: Redémarrage dans 10 minutes!"

# Depuis fichier
wall < message.txt

# Shutdown avec message automatique
sudo shutdown -h +10 "Maintenance planifiée"
# Tous les utilisateurs reçoivent le message via wall
```

#### Fichier `/etc/motd` - Message of the day

```bash
# Message affiché après login
sudo nano /etc/motd

# Exemple:
#############################
# Serveur de Production     #
# Accès restreint           #
# Contact: admin@domain.com #
#############################
```

### 🔐 ACPI et gestion énergie

#### États ACPI (Advanced Configuration and Power Interface)

```
G0 = S0 : Working (système allumé)
G1 = S1-S4 : Sleeping
  S1 : Standby (CPU arrêté, RAM alimentée)
  S2 : (Rarement utilisé)
  S3 : Suspend to RAM (RAM alimentée uniquement)
  S4 : Suspend to Disk (Hibernation)
G2 = S5 : Soft Off (alimentation coupée, mais peut redémarrer)
G3 : Mechanical Off (interrupteur physique off)
```

#### Commandes ACPI

```bash
# État batterie (laptops)
acpi -b

# Température
acpi -t

# Tout afficher
acpi -V

# Événements ACPI
acpi_listen
```

---

## 📝 Résumé et points clés à retenir

### Commandes essentielles par catégorie

#### Inspection matériel
```bash
lspci, lsusb, lsblk, lscpu
cat /proc/cpuinfo, cat /proc/meminfo
ls /sys/class/net/
```

#### Modules kernel
```bash
lsmod, modinfo, modprobe, modprobe -r
/etc/modprobe.d/blacklist.conf
```

#### Boot et GRUB
```bash
/etc/default/grub, update-grub
/boot/grub/grub.cfg
dmesg, journalctl -b
```

#### Runlevels / Targets
```bash
runlevel, telinit
systemctl get-default, systemctl isolate
```

#### Arrêt système
```bash
shutdown, halt, poweroff, reboot
systemctl reboot, systemctl poweroff
wall
```

### Différences clés

| Concept | SysVinit (ancien) | systemd (moderne) |
|---------|-------------------|-------------------|
| **Unité** | Runlevel (0-6) | Target |
| **Config** | /etc/inittab | systemctl |
| **Scripts** | /etc/init.d/ | /lib/systemd/system/ |
| **Changer** | telinit | systemctl isolate |
| **Défaut** | /etc/inittab | systemctl set-default |
| **Status** | runlevel | systemctl get-default |

### Checklist avant examen

- [ ] Je connais la différence entre `/proc`, `/sys`, `/dev`
- [ ] Je sais utiliser `lspci`, `lsusb`, `lsblk`
- [ ] Je comprends les modules kernel (`lsmod`, `modprobe`)
- [ ] Je peux configurer GRUB 2 (`/etc/default/grub`)
- [ ] Je connais le processus de boot complet
- [ ] Je sais passer des paramètres au kernel
- [ ] Je différencie runlevels et systemd targets
- [ ] Je peux arrêter/redémarrer le système proprement
- [ ] Je comprends BIOS vs UEFI

---

## 🔬 Labs pratiques recommandés

### Lab 1 : Exploration système
```bash
# 1. Inspecter CPU et mémoire
cat /proc/cpuinfo | grep "model name"
free -h
lscpu

# 2. Lister périphériques
lspci
lsusb
lsblk

# 3. Explorer /sys
ls /sys/class/net/
cat /sys/class/net/eth0/address
```

### Lab 2 : Modules kernel
```bash
# 1. Lister modules
lsmod | head -20

# 2. Info sur module
modinfo e1000

# 3. Charger/décharger (si possible)
sudo modprobe dummy
lsmod | grep dummy
sudo modprobe -r dummy
```

### Lab 3 : Configuration GRUB
```bash
# 1. Voir config actuelle
cat /etc/default/grub

# 2. Sauvegarder
sudo cp /etc/default/grub /etc/default/grub.backup

# 3. Modifier timeout
sudo nano /etc/default/grub
# GRUB_TIMEOUT=10

# 4. Régénérer
sudo update-grub

# 5. Restaurer sauvegarde
sudo cp /etc/default/grub.backup /etc/default/grub
sudo update-grub
```

### Lab 4 : Logs de boot
```bash
# 1. Messages kernel
dmesg | less

# 2. Avec timestamp
dmesg -T | tail -50

# 3. Journalctl
journalctl -b
journalctl -b -1  # Boot précédent
journalctl -k     # Kernel seulement
```

### Lab 5 : Systemd targets
```bash
# 1. Target actuel
systemctl get-default

# 2. Lister targets
systemctl list-units --type=target

# 3. Dépendances
systemctl list-dependencies graphical.target

# 4. (Optionnel) Changer target temporairement
# ATTENTION : Cela va changer l'interface !
# sudo systemctl isolate multi-user.target
```

---

## 📖 Ressources complémentaires

- **Man pages :** `man lspci`, `man grub`, `man systemd`
- **Documentation LPI :** LPI-Learning-Material-101-500-fr.md
- **Cours KodeKloud :** Modules Sujet 101
- **Anki :** 37 cartes Sujet 101

---

**🎯 Objectif : Maîtriser le Sujet 101 à 100% avant de passer au Sujet 102 !**

*Prochaine étape : [QCM-Sujet-101.md](../QCM/QCM-Sujet-101.md) pour tester vos connaissances !*
