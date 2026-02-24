# 🧪 QCM Sujet 101 : Architecture Système

> **Nombre de questions :** 30  
> **Poids du sujet :** 8 points (~20% de l'examen)  
> **Durée estimée :** 45 minutes  
> **Objectif :** 75% minimum (23/30)

---

## 📋 Instructions

- Lisez attentivement chaque question
- Une seule réponse correcte par question (sauf mention contraire)
- Les réponses sont en fin de document avec explications détaillées
- Ne trichez pas ! Testez vos vraies connaissances
- Notez vos réponses avant de regarder les corrections

---

## 🔍 Section 101.1 : Détermination et configuration du matériel (10 questions)

### Question 1
Quel fichier contient des informations sur le CPU dans le système de fichiers virtuel ?

- [ ] A) `/sys/cpu/info`  
- [ ] B) `/proc/cpuinfo`  
- [ ] C) `/dev/cpu`  
- [ ] D) `/etc/cpu.conf`

---

### Question 2
Quelle commande permet de lister tous les périphériques PCI avec les modules kernel utilisés ?

- [ ] A) `lspci -m`  
- [ ] B) `lspci -k`  
- [ ] C) `lspci -v`  
- [ ] D) `lspci --modules`

---

### Question 3
Dans la sortie de `lspci`, que signifie l'adresse `02:05.0` ?

- [ ] A) Bus 2, Device 5, Function 0  
- [ ] B) Bus 2, Device 0, Function 5  
- [ ] C) Bus 0, Device 2, Function 5  
- [ ] D) Partition 2, Block 5, Sector 0

---

### Question 4
Quelle commande affiche des informations détaillées sur un module kernel nommé `e1000` ?

- [ ] A) `modinfo e1000`  
- [ ] B) `lsmod e1000`  
- [ ] C) `modprobe --info e1000`  
- [ ] D) `module-info e1000`

---

### Question 5
**QUESTION À CHOIX MULTIPLES** - Sélectionnez TOUTES les réponses correctes.

Quels répertoires contiennent des informations sur les périphériques système ?

- [ ] A) `/proc`  
- [ ] B) `/sys`  
- [ ] C) `/dev`  
- [ ] D) `/hardware`  
- [ ] E) `/devices`

---

### Question 6
Quelle est la différence principale entre `modprobe` et `insmod` ?

- [ ] A) `modprobe` est pour kernel 2.4, `insmod` pour kernel 2.6+  
- [ ] B) `modprobe` gère les dépendances automatiquement, `insmod` non  
- [ ] C) `insmod` est plus rapide que `modprobe`  
- [ ] D) `modprobe` nécessite le chemin complet du module, `insmod` non

---

### Question 7
Dans quel fichier de configuration peut-on empêcher le chargement automatique d'un module kernel ?

- [ ] A) `/etc/modules.blacklist`  
- [ ] B) `/etc/modprobe.d/blacklist.conf`  
- [ ] C) `/proc/modules/disabled`  
- [ ] D) `/sys/module/blacklist`

---

### Question 8
Quelle commande permet d'afficher l'arbre hiérarchique des périphériques USB ?

- [ ] A) `lsusb --tree`  
- [ ] B) `lsusb -h`  
- [ ] C) `lsusb -t`  
- [ ] D) `lsusb --hierarchy`

---

### Question 9
Quel est le rôle principal de `udev` ?

- [ ] A) Charger les modules kernel au démarrage  
- [ ] B) Gérer dynamiquement les fichiers de périphériques dans `/dev`  
- [ ] C) Compiler les drivers matériels  
- [ ] D) Mettre à jour le firmware des périphériques

---

### Question 10
Dans la sortie de `lsusb`, que représente `ID 1234:5678` ?

- [ ] A) Bus ID : Device ID  
- [ ] B) Vendor ID : Product ID  
- [ ] C) Major Number : Minor Number  
- [ ] D) Port USB : Numéro de série

---

## 🥾 Section 101.2 : Démarrage du système (10 questions)

### Question 11
Quel est le fichier de configuration principal de GRUB 2 (NE PAS éditer directement) ?

- [ ] A) `/etc/default/grub`  
- [ ] B) `/boot/grub/grub.cfg`  
- [ ] C) `/etc/grub.conf`  
- [ ] D) `/boot/grub/menu.lst`

---

### Question 12
Après avoir modifié `/etc/default/grub`, quelle commande régénère la configuration GRUB sur Debian/Ubuntu ?

- [ ] A) `grub-update`  
- [ ] B) `update-grub`  
- [ ] C) `grub2-mkconfig`  
- [ ] D) `grub-install`

---

### Question 13
Dans la notation GRUB 2, que représente `(hd0,1)` ?

- [ ] A) Premier disque, première partition  
- [ ] B) Deuxième disque, première partition  
- [ ] C) Premier disque, deuxième partition  
- [ ] D) Disque 0, secteur 1

---

### Question 14
Quel paramètre kernel permet de démarrer en mode single-user ?

- [ ] A) `init=1`  
- [ ] B) `single`  
- [ ] C) `init=/bin/bash`  
- [ ] D) Toutes les réponses ci-dessus

---

### Question 15
Quel est le rôle principal de l'initramfs/initrd ?

- [ ] A) Stocker la configuration du bootloader  
- [ ] B) Fournir un mini-système temporaire avec drivers essentiels  
- [ ] C) Sauvegarder l'état du système avant boot  
- [ ] D) Contenir les fichiers de logs de démarrage

---

### Question 16
Quelle commande permet de voir les messages du kernel depuis le dernier démarrage ?

- [ ] A) `dmesg -b`  
- [ ] B) `journalctl -b`  
- [ ] C) `kernlog --boot`  
- [ ] D) `syslog --last-boot`

---

### Question 17
Dans le processus de démarrage, quel composant est exécuté en PREMIER après le POST ?

- [ ] A) Kernel  
- [ ] B) GRUB  
- [ ] C) BIOS/UEFI  
- [ ] D) initramfs

---

### Question 18
Où se trouve la partition ESP (EFI System Partition) généralement montée sur un système UEFI ?

- [ ] A) `/boot`  
- [ ] B) `/boot/efi`  
- [ ] C) `/efi`  
- [ ] D) `/sys/firmware/efi`

---

### Question 19
Quelle commande affiche les messages kernel avec horodatage lisible par l'humain ?

- [ ] A) `dmesg -H`  
- [ ] B) `dmesg -T`  
- [ ] C) `dmesg --human`  
- [ ] D) `dmesg --timestamp`

---

### Question 20
Quel fichier kernel contient la table des symboles kernel (pour débogage) ?

- [ ] A) `/boot/vmlinuz`  
- [ ] B) `/boot/System.map`  
- [ ] C) `/boot/config`  
- [ ] D) `/proc/kallsyms`

---

## 🎯 Section 101.3 : Runlevels/Targets et arrêt système (10 questions)

### Question 21
Quel runlevel SysVinit correspond au mode multi-user graphique ?

- [ ] A) Runlevel 3  
- [ ] B) Runlevel 4  
- [ ] C) Runlevel 5  
- [ ] D) Runlevel 6

---

### Question 22
Quelle commande systemd permet de changer le target par défaut en mode texte multi-user ?

- [ ] A) `systemctl isolate multi-user.target`  
- [ ] B) `systemctl set-default multi-user.target`  
- [ ] C) `systemctl change-target multi-user.target`  
- [ ] D) `systemctl default multi-user.target`

---

### Question 23
Quelle commande affiche le runlevel actuel sur un système SysVinit ?

- [ ] A) `whoami`  
- [ ] B) `runlevel`  
- [ ] C) `init --status`  
- [ ] D) `level`

---

### Question 24
Quel systemd target équivaut au runlevel 1 (single-user mode) ?

- [ ] A) `emergency.target`  
- [ ] B) `rescue.target`  
- [ ] C) `single-user.target`  
- [ ] D) `maintenance.target`

---

### Question 25
Comment annuler un shutdown planifié ?

- [ ] A) `shutdown -a`  
- [ ] B) `shutdown -c`  
- [ ] C) `shutdown --cancel`  
- [ ] D) `killall shutdown`

---

### Question 26
Quelle commande planifie un redémarrage dans 15 minutes avec un message d'avertissement ?

- [ ] A) `reboot +15 "Maintenance"`  
- [ ] B) `shutdown -r +15 "Maintenance"`  
- [ ] C) `systemctl reboot --delay=15 "Maintenance"`  
- [ ] D) `init 6 +15 "Maintenance"`

---

### Question 27
Quelle commande envoie un message à tous les utilisateurs connectés ?

- [ ] A) `broadcast`  
- [ ] B) `notify-all`  
- [ ] C) `wall`  
- [ ] D) `announce`

---

### Question 28
Sur un système systemd, quelle commande affiche le target actuel par défaut ?

- [ ] A) `systemctl get-target`  
- [ ] B) `systemctl show-default`  
- [ ] C) `systemctl get-default`  
- [ ] D) `systemctl default`

---

### Question 29
Quel état ACPI correspond à l'hibernation (Suspend to Disk) ?

- [ ] A) S1  
- [ ] B) S2  
- [ ] C) S3  
- [ ] D) S4

---

### Question 30
**SCÉNARIO** - Sur un serveur de production, vous devez redémarrer le système ce soir à 22h30. Quelle commande utilisez-vous ?

- [ ] A) `shutdown -r 22:30`  
- [ ] B) `shutdown -r +22:30`  
- [ ] C) `reboot --at 22:30`  
- [ ] D) `systemctl reboot --scheduled=22:30`

---

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Section 101.1 : Détermination et configuration du matériel

### Question 1 : **Réponse B** - `/proc/cpuinfo`

**Explication :**
- `/proc/cpuinfo` contient les informations détaillées sur le ou les processeurs
- `/proc/` est un système de fichiers virtuel créé dynamiquement par le kernel
- Commande classique : `cat /proc/cpuinfo | grep "model name"`

**Pourquoi les autres sont fausses :**
- A) `/sys/cpu/info` n'existe pas
- C) `/dev/cpu` n'existe généralement pas (périphériques seulement)
- D) `/etc/cpu.conf` n'est pas un fichier standard Linux

**Pour aller plus loin :**
- `lscpu` est une alternative formatée pour lire les infos CPU
- `/proc/meminfo` pour la mémoire RAM
- `/proc/version` pour la version du kernel

---

### Question 2 : **Réponse B** - `lspci -k`

**Explication :**
- L'option `-k` affiche les modules kernel (drivers) utilisés par chaque périphérique
- Très utile pour identifier quel driver gère quel matériel
- Exemple de sortie :
  ```
  01:00.0 VGA compatible controller: NVIDIA Corporation
  Kernel driver in use: nouveau
  Kernel modules: nvidiafb, nouveau
  ```

**Pourquoi les autres sont fausses :**
- A) `-m` affiche un format lisible par machine (non les modules)
- C) `-v` affiche des détails verbeux mais pas spécifiquement les modules
- D) `--modules` n'est pas une option valide de `lspci`

**Options utiles de lspci :**
- `-v` : Verbose (détails)
- `-vv` : Très verbose
- `-nn` : Affiche vendor/device IDs en hexa
- `-t` : Format arbre

---

### Question 3 : **Réponse A** - Bus 2, Device 5, Function 0

**Explication :**
- Format : `BB:DD.F`
  - **BB** = Bus (00-FF en hexa)
  - **DD** = Device/Slot (00-1F en hexa)
  - **F** = Function (0-7)
- `02:05.0` = Bus 2, Device 5, Function 0

**Exemple réel :**
- `00:00.0` = Bus 0, Device 0, Function 0 (souvent le contrôleur mémoire)
- `01:00.0` = Bus 1, Device 0, Function 0 (souvent carte graphique)

**Pourquoi les autres sont fausses :**
- B, C, D) Mauvaise interprétation de l'ordre des champs

**Conseil pour l'examen :**
Retenez le format `Bus:Device.Function` !

---

### Question 4 : **Réponse A** - `modinfo e1000`

**Explication :**
- `modinfo` affiche toutes les informations sur un module :
  - filename (chemin du .ko)
  - description
  - author
  - license
  - depends (dépendances)
  - parm (paramètres configurables)
  - alias

**Exemple d'utilisation :**
```bash
modinfo e1000
modinfo -p e1000      # Seulement les paramètres
modinfo -d bluetooth  # Seulement la description
```

**Pourquoi les autres sont fausses :**
- B) `lsmod` liste les modules chargés, ne prend pas d'argument de module
- C) `modprobe --info` n'existe pas
- D) `module-info` n'est pas une commande standard

---

### Question 5 : **Réponses A, B, C** - `/proc`, `/sys`, `/dev`

**Explication :**
- **`/proc/`** : Système de fichiers virtuel
  - Infos kernel et processus
  - Exemple : `/proc/cpuinfo`, `/proc/meminfo`
  
- **`/sys/`** : Interface sysfs
  - Représentation hiérarchique des périphériques
  - Exemple : `/sys/class/net/`, `/sys/block/`
  
- **`/dev/`** : Fichiers de périphériques
  - Interfaces vers périphériques matériels
  - Exemple : `/dev/sda`, `/dev/tty`, `/dev/null`

**Pourquoi les autres sont fausses :**
- D) `/hardware` n'existe pas
- E) `/devices` n'est pas un répertoire standard (existe dans `/sys/devices/`)

**Conseil :** Bien comprendre la différence entre ces 3 répertoires !

---

### Question 6 : **Réponse B** - `modprobe` gère les dépendances automatiquement

**Explication :**

| Caractéristique | `modprobe` | `insmod` |
|-----------------|------------|----------|
| Dépendances | ✅ Auto | ❌ Manuel |
| Argument | Nom module | Chemin .ko |
| Usage | Production | Debug |
| Configuration | Lit `/etc/modprobe.d/` | Non |

**Exemple concret :**
```bash
# modprobe : simple et intelligent
sudo modprobe bluetooth
# Charge bluetooth + ses dépendances automatiquement

# insmod : manuel et basique
sudo insmod /lib/modules/$(uname -r)/kernel/net/bluetooth/bluetooth.ko
# Échoue si dépendances non chargées
```

**Pourquoi les autres sont fausses :**
- A) Tous deux fonctionnent sur kernels modernes
- C) Vitesse similaire
- D) C'est l'inverse !

---

### Question 7 : **Réponse B** - `/etc/modprobe.d/blacklist.conf`

**Explication :**
- La blacklist empêche le chargement automatique de modules
- Fichier typique : `/etc/modprobe.d/blacklist.conf`
- Syntaxe : `blacklist nom_module`

**Exemple pratique :**
```bash
# Empêcher chargement du driver Nouveau (NVIDIA)
echo "blacklist nouveau" | sudo tee -a /etc/modprobe.d/blacklist.conf

# Regénérer initramfs
sudo update-initramfs -u

# Redémarrer
sudo reboot
```

**Pourquoi les autres sont fausses :**
- A) Nom de fichier incorrect
- C) `/proc/` est généralement en lecture seule
- D) `/sys/module/` liste les modules, ne les configure pas

**Conseil :** Ne pas confondre blacklist (empêche chargement auto) et rmmod (décharge module)

---

### Question 8 : **Réponse C** - `lsusb -t`

**Explication :**
- L'option `-t` affiche l'arbre hiérarchique des bus et périphériques USB
- Utile pour visualiser la topologie USB

**Exemple de sortie :**
```
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ehci-pci/3p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/8p, 480M
        |__ Port 3: Dev 5, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 4: Dev 6, If 0, Class=Mass Storage, Driver=usb-storage, 480M
```

**Autres options utiles :**
- `lsusb -v` : Verbose (détails)
- `lsusb -d 1234:5678` : Filtre par vendor:product ID

**Pourquoi les autres sont fausses :**
- A) `--tree` n'existe pas (c'est `-t`)
- B) `-h` affiche l'aide
- D) `--hierarchy` n'existe pas

---

### Question 9 : **Réponse B** - Gérer dynamiquement `/dev`

**Explication :**
- **udev** = **U**serspace **DEV**ice manager
- Rôles principaux :
  1. Créer/supprimer fichiers dans `/dev/` à la volée
  2. Créer noms persistants (ex: `/dev/disk/by-uuid/`)
  3. Définir permissions des périphériques
  4. Exécuter actions lors détection matériel

**Exemple concret :**
```bash
# Règle udev personnalisée
# /etc/udev/rules.d/99-usb-backup.rules
SUBSYSTEM=="block", ATTRS{idVendor}=="1234", SYMLINK+="backup_disk"

# Recharger règles
sudo udevadm control --reload
sudo udevadm trigger
```

**Pourquoi les autres sont fausses :**
- A) C'est le rôle de modprobe/systemd
- C) udev ne compile pas de drivers
- D) udev ne gère pas le firmware (c'est le kernel + firmware-utils)

**Commandes udev importantes :**
- `udevadm monitor` : Surveiller événements en temps réel
- `udevadm info /dev/sda` : Infos sur périphérique

---

### Question 10 : **Réponse B** - Vendor ID : Product ID

**Explication :**
- Format : `ID VVVV:PPPP`
  - **VVVV** = Vendor ID (4 chiffres hexa)
  - **PPPP** = Product ID (4 chiffres hexa)

**Exemple réel :**
```
Bus 001 Device 005: ID 046d:c52b Logitech, Inc. Unifying Receiver
```
- `046d` = Logitech (vendor)
- `c52b` = Unifying Receiver (produit spécifique)

**Base de données USB IDs :**
- Fichier : `/usr/share/hwdata/usb.ids` ou `/var/lib/usbutils/usb.ids`
- Recherche : `grep "046d" /usr/share/hwdata/usb.ids`

**Pourquoi les autres sont fausses :**
- A) Bus et Device sont affichés avant l'ID
- C) Major/Minor sont pour `/dev/`, pas USB IDs
- D) Aucun rapport avec port physique

---

## Section 101.2 : Démarrage du système

### Question 11 : **Réponse B** - `/boot/grub/grub.cfg`

**Explication :**
- `/boot/grub/grub.cfg` est le fichier de configuration **généré automatiquement**
- ⚠️ **NE JAMAIS éditer directement** ce fichier !
- Modifications écrasées à chaque `update-grub`

**Workflow correct :**
```bash
# 1. Éditer le fichier source
sudo nano /etc/default/grub

# 2. Régénérer grub.cfg
sudo update-grub

# Le fichier /boot/grub/grub.cfg est recréé automatiquement
```

**Pourquoi les autres sont fausses :**
- A) `/etc/default/grub` est le fichier à **éditer** (pas le principal)
- C) `/etc/grub.conf` est utilisé par GRUB Legacy (ancien)
- D) `/boot/grub/menu.lst` est aussi GRUB Legacy

**Variante Red Hat/CentOS :**
- Fichier config : `/boot/grub2/grub.cfg`
- Commande : `grub2-mkconfig -o /boot/grub2/grub.cfg`

---

### Question 12 : **Réponse B** - `update-grub`

**Explication :**
- `update-grub` est un script Debian/Ubuntu qui appelle `grub-mkconfig`
- Scanne automatiquement :
  - Kernels dans `/boot`
  - Autres OS (via os-prober)
  - Scripts dans `/etc/grub.d/`
- Génère `/boot/grub/grub.cfg`

**Équivalences entre distributions :**

| Distribution | Commande |
|--------------|----------|
| Debian/Ubuntu | `update-grub` |
| Red Hat/CentOS/Fedora | `grub2-mkconfig -o /boot/grub2/grub.cfg` |
| Arch Linux | `grub-mkconfig -o /boot/grub/grub.cfg` |

**Pourquoi les autres sont fausses :**
- A) `grub-update` n'existe pas
- C) `grub2-mkconfig` existe mais nécessite `-o` (option Red Hat)
- D) `grub-install` installe GRUB sur disque, ne regénère pas config

**Conseil :** Toujours tester après modification GRUB (ne pas redémarrer directement en prod !)

---

### Question 13 : **Réponse A** - Premier disque, première partition

**Explication :**
- GRUB 2 compte :
  - **Disques depuis 0** : hd0, hd1, hd2...
  - **Partitions depuis 1** : 1, 2, 3...
  
**Tableau de correspondance :**

| Notation GRUB 2 | Notation Linux | Description |
|-----------------|----------------|-------------|
| `(hd0,1)` | `/dev/sda1` | 1er disque, 1ère partition |
| `(hd0,2)` | `/dev/sda2` | 1er disque, 2ème partition |
| `(hd1,1)` | `/dev/sdb1` | 2ème disque, 1ère partition |
| `(hd2,5)` | `/dev/sdc5` | 3ème disque, 5ème partition |

**⚠️ Différence avec GRUB Legacy :**
- GRUB Legacy : partitions aussi depuis 0
  - `(hd0,0)` = `/dev/sda1`
  - `(hd0,1)` = `/dev/sda2`

**Pourquoi les autres sont fausses :**
- B, C, D) Mauvaise interprétation de la numérotation

**Exemple dans grub.cfg :**
```
set root=(hd0,1)
linux /vmlinuz root=/dev/sda1 ro
```

---

### Question 14 : **Réponse D** - Toutes les réponses

**Explication :**
Plusieurs paramètres kernel permettent de démarrer en single-user mode :

1. **`single`** - Méthode standard
   ```
   linux /vmlinuz root=/dev/sda1 ro single
   ```

2. **`init=1`** ou **`1`** - Via le runlevel
   ```
   linux /vmlinuz root=/dev/sda1 ro 1
   ```

3. **`init=/bin/bash`** - Shell direct (mode urgence)
   ```
   linux /vmlinuz root=/dev/sda1 ro init=/bin/bash
   ```

**Usage typique :**
- Réinitialiser mot de passe root
- Réparer système de fichiers
- Debugging système

**Mode rescue vs emergency (systemd) :**
- `systemd.unit=rescue.target` = Mode rescue (≈ single-user)
- `systemd.unit=emergency.target` = Mode urgence (minimal)

---

### Question 15 : **Réponse B** - Mini-système temporaire avec drivers

**Explication :**
**Problème du chicken-and-egg :**
- Le kernel a besoin de drivers SATA/SCSI pour lire le disque
- Mais les drivers sont SUR le disque !

**Solution : initramfs (Initial RAM FileSystem)**
1. Chargé en RAM par GRUB
2. Contient drivers essentiels :
   - SATA, SCSI, NVMe (stockage)
   - LVM, RAID, encryption
   - Systèmes de fichiers (ext4, xfs...)
3. Monte le vrai `/`
4. Passe contrôle via `switch_root`

**Schéma du processus :**
```
GRUB → Charge vmlinuz + initramfs en RAM
     → Kernel s'exécute
     → Monte initramfs comme /
     → Charge drivers depuis initramfs
     → Monte VRAI / (disque)
     → switch_root vers vrai /
     → Lance /sbin/init
```

**Pourquoi les autres sont fausses :**
- A) Configuration bootloader = `/boot/grub/grub.cfg`
- C) Pas de sauvegarde d'état
- D) Logs = `/var/log/`, pas initramfs

**Commandes utiles :**
```bash
# Recréer initramfs
sudo update-initramfs -u  # Debian/Ubuntu
sudo dracut --force       # Red Hat/CentOS

# Lister contenu
lsinitramfs /boot/initrd.img-$(uname -r)
```

---

### Question 16 : **Réponse B** - `journalctl -b`

**Explication :**
- `journalctl -b` affiche les logs systemd depuis le dernier boot
- Option `-b` = boot actuel
- `-b -1` = boot précédent
- `-b -2` = avant-avant-dernier boot...

**Exemples :**
```bash
# Boot actuel
journalctl -b

# Boot précédent
journalctl -b -1

# Lister tous les boots
journalctl --list-boots

# Boot spécifique par ID
journalctl -b 3c3a9b...
```

**Pourquoi les autres sont fausses :**
- A) `dmesg -b` n'existe pas (dmesg utilise `-T` pour timestamp)
- C) `kernlog` n'est pas une commande standard
- D) `syslog` est un daemon, pas une commande d'affichage

**Alternative avec dmesg :**
```bash
# Messages kernel (boot actuel uniquement)
dmesg

# Avec timestamp lisible
dmesg -T
```

**Différence journalctl vs dmesg :**
- `dmesg` : Buffer kernel seulement (ring buffer limité)
- `journalctl` : Tous les logs système (persistent sur disque)

---

### Question 17 : **Réponse C** - BIOS/UEFI

**Explication :**
**Séquence de boot complète :**

```
1. ⚡ POWER ON
   └─> Alimentation activée

2. 🔍 POST (Power-On Self-Test)
   └─> Test RAM, CPU, périphériques

3. 🖥️ BIOS/UEFI ← PREMIÈRE ÉTAPE LOGICIELLE
   ├─> Initialise matériel
   ├─> Lit configuration boot (boot order)
   └─> Charge bootloader depuis disque

4. 🥾 GRUB (Bootloader)
   ├─> Affiche menu
   ├─> Charge kernel (vmlinuz)
   └─> Charge initramfs

5. 🐧 KERNEL
   ├─> Décompresse
   ├─> Initialise drivers
   └─> Monte initramfs

6. 📦 INITRAMFS
   └─> Monte vrai système de fichiers

7. 🎯 INIT/SYSTEMD (PID 1)
   └─> Lance services système
```

**Pourquoi les autres sont fausses :**
- A) Kernel vient APRÈS BIOS/UEFI
- B) GRUB vient APRÈS BIOS/UEFI
- D) initramfs vient APRÈS kernel

**POST vs BIOS :**
- **POST** = Tests matériels (partie du firmware BIOS/UEFI)
- **BIOS/UEFI** = Firmware complet (inclut POST + boot manager)

---

### Question 18 : **Réponse B** - `/boot/efi`

**Explication :**
- Sur systèmes **UEFI**, la partition ESP est montée sur **`/boot/efi`**
- **ESP** = EFI System Partition
- Format : **FAT32** (obligatoire par spec UEFI)
- Contient : bootloaders UEFI (`.efi` files)

**Structure typique :**
```
/boot/efi/
└── EFI/
    ├── BOOT/
    │   └── BOOTX64.EFI    # Bootloader par défaut
    ├── ubuntu/
    │   └── grubx64.efi    # GRUB pour Ubuntu
    ├── debian/
    │   └── grubx64.efi    # GRUB pour Debian
    └── Microsoft/
        └── Boot/
            └── bootmgfw.efi  # Windows Boot Manager
```

**Vérifier le montage :**
```bash
# Voir partitions montées
mount | grep efi
# /dev/sda1 on /boot/efi type vfat

# Ou via lsblk
lsblk -f | grep -i efi
```

**Pourquoi les autres sont fausses :**
- A) `/boot` contient kernels, pas spécifiquement ESP
- C) `/efi` n'est pas standard
- D) `/sys/firmware/efi` est un pseudo-système de fichiers, pas montage ESP

**Conseil :** Sur BIOS, pas de `/boot/efi` (GRUB dans MBR ou partition boot)

---

### Question 19 : **Réponse B** - `dmesg -T`

**Explication :**
- Option `-T` = **T**imestamp (format humain)
- Convertit les timestamps kernel en dates lisibles

**Comparaison :**
```bash
# Sans -T (timestamp kernel en secondes depuis boot)
$ dmesg | head -1
[    0.000000] Linux version 5.15.0-58-generic

# Avec -T (timestamp lisible)
$ dmesg -T | head -1
[Mon Jan 28 09:15:32 2026] Linux version 5.15.0-58-generic
```

**Autres options utiles de dmesg :**
```bash
dmesg -w      # Watch (suivre en temps réel)
dmesg -l err  # Erreurs seulement
dmesg -l warn # Warnings
dmesg -H      # Human-readable (pager + couleurs)
dmesg -c      # Clear buffer
dmesg | grep -i usb  # Filtrer par mot-clé
```

**Pourquoi les autres sont fausses :**
- A) `-H` = Human-readable (active pager, pas timestamps)
- C) `--human` n'existe pas
- D) `--timestamp` n'existe pas

---

### Question 20 : **Réponse B** - `/boot/System.map`

**Explication :**
- **System.map** contient la table des symboles du kernel
- Map entre adresses mémoire et noms de fonctions/variables kernel
- Utilisé pour :
  - Débogage kernel
  - Analyse de crashes (oops, kernel panic)
  - Profiling et optimisation

**Contenu typique :**
```
ffffffff81000000 T _stext
ffffffff81000030 T startup_64
ffffffff81000100 T secondary_startup_64
```

Format : `Adresse Type Nom_symbole`

**Pourquoi les autres sont fausses :**
- A) `/boot/vmlinuz` = Kernel compressé (binaire)
- C) `/boot/config` = Configuration de compilation kernel
- D) `/proc/kallsyms` = Symboles kernel EN COURS (runtime, équivalent dynamique)

**Différence System.map vs kallsyms :**
| Fichier | Type | Usage |
|---------|------|-------|
| `/boot/System.map` | Statique | Déboguer kernel compilé |
| `/proc/kallsyms` | Dynamique | Kernel en cours d'exécution |

**Exemple d'utilisation :**
```bash
# Trouver adresse d'une fonction kernel
grep "sys_open" /boot/System.map-$(uname -r)
```

---

## Section 101.3 : Runlevels/Targets et arrêt système

### Question 21 : **Réponse C** - Runlevel 5

**Explication :**
**Tableau complet des runlevels SysVinit :**

| Runlevel | Description | Usage typique |
|----------|-------------|---------------|
| **0** | Halt (arrêt) | `telinit 0` |
| **1** | Single-user | Maintenance root |
| **2** | Multi-user sans réseau | Rarement utilisé |
| **3** | Multi-user avec réseau | **Mode texte serveur** |
| **4** | Non défini | Personnalisable |
| **5** | Multi-user graphique | **Mode desktop** ✅ |
| **6** | Reboot | `telinit 6` |

**Runlevel par défaut :**
```bash
# Ancien système (/etc/inittab)
id:5:initdefault:
```

**Pourquoi les autres sont fausses :**
- A) Runlevel 3 = Multi-user TEXTE (pas graphique)
- B) Runlevel 4 = Non utilisé par défaut
- D) Runlevel 6 = Reboot

**Équivalent systemd :**
- Runlevel 5 = `graphical.target`
- Runlevel 3 = `multi-user.target`

---

### Question 22 : **Réponse B** - `systemctl set-default multi-user.target`

**Explication :**
- `set-default` modifie le target **par défaut** (permanent)
- Crée un lien symbolique `/etc/systemd/system/default.target`

**Différence set-default vs isolate :**

| Commande | Effet | Persistance |
|----------|-------|-------------|
| `set-default` | Change target par défaut | ✅ Permanent (prochain boot) |
| `isolate` | Change target immédiatement | ❌ Temporaire (session actuelle) |

**Exemples :**
```bash
# Définir mode texte par défaut (permanent)
sudo systemctl set-default multi-user.target

# Vérifier
systemctl get-default
# multi-user.target

# Changer immédiatement vers mode texte (temporaire)
sudo systemctl isolate multi-user.target

# Revenir au graphique (temporaire)
sudo systemctl isolate graphical.target

# Remettre graphique par défaut (permanent)
sudo systemctl set-default graphical.target
```

**Pourquoi les autres sont fausses :**
- A) `isolate` change temporairement (ne modifie pas défaut)
- C) `change-target` n'existe pas
- D) `default` n'existe pas (c'est `set-default` ou `get-default`)

---

### Question 23 : **Réponse B** - `runlevel`

**Explication :**
- Commande `runlevel` affiche le runlevel actuel et précédent
- Format de sortie : `X Y`
  - **X** = Runlevel précédent (N si aucun changement depuis boot)
  - **Y** = Runlevel actuel

**Exemples :**
```bash
# Au boot (aucun changement)
$ runlevel
N 5
# N = Pas de runlevel précédent
# 5 = Runlevel actuel

# Après changement de runlevel
$ sudo telinit 3
$ runlevel
5 3
# 5 = Runlevel précédent
# 3 = Runlevel actuel
```

**Sur système systemd :**
```bash
# runlevel fonctionne toujours (compatibilité)
$ runlevel
N 5

# Équivalent systemd
$ systemctl get-default
graphical.target
```

**Pourquoi les autres sont fausses :**
- A) `whoami` affiche le nom d'utilisateur
- C) `init --status` n'existe pas
- D) `level` n'est pas une commande

---

### Question 24 : **Réponse B** - `rescue.target`

**Explication :**
**Correspondance runlevels ↔ targets :**

| Runlevel | Systemd Target | Description |
|----------|----------------|-------------|
| 0 | `poweroff.target` | Arrêt |
| 1 | `rescue.target` | **Single-user/Rescue** ✅ |
| 2, 3, 4 | `multi-user.target` | Multi-user texte |
| 5 | `graphical.target` | Multi-user graphique |
| 6 | `reboot.target` | Redémarrage |
| - | `emergency.target` | Mode urgence (encore plus minimal) |

**Différence rescue vs emergency :**
- **`rescue.target`** (≈ runlevel 1) :
  - Monte systèmes de fichiers
  - Active quelques services basiques
  - Shell root
  - Réseau généralement désactivé

- **`emergency.target`** :
  - Mount `/` en lecture seule
  - Aucun service (sauf absolu minimum)
  - Shell root direct
  - Mode debugging maximal

**Passer en mode rescue :**
```bash
# Au boot (éditer GRUB)
systemd.unit=rescue.target

# En cours d'exécution
sudo systemctl isolate rescue.target
```

**Pourquoi les autres sont fausses :**
- A) `emergency.target` est encore plus minimal
- C, D) Ces targets n'existent pas

---

### Question 25 : **Réponse B** - `shutdown -c`

**Explication :**
- Option `-c` = **C**ancel (annuler shutdown planifié)
- Envoie message broadcast à tous les utilisateurs

**Scénario typique :**
```bash
# 1. Planifier shutdown dans 30 minutes
$ sudo shutdown -h +30 "Maintenance serveur"
Shutdown scheduled for Mon 2026-01-28 15:45:00 CET, use 'shutdown -c' to cancel.

# 2. Les utilisateurs reçoivent le message
Broadcast message from root@server (Mon 2026-01-28 15:15:00 CET):

Maintenance serveur
The system is going down for poweroff at Mon 2026-01-28 15:45:00 CET!

# 3. Annuler si changement de plan
$ sudo shutdown -c
Shutdown cancelled.

# 4. Message d'annulation broadcasté
Broadcast message from root@server (Mon 2026-01-28 15:20:00 CET):

The system shutdown has been cancelled
```

**Pourquoi les autres sont fausses :**
- A) `-a` n'existe pas
- C) `--cancel` n'existe pas (syntaxe courte `-c` seulement)
- D) `killall shutdown` ne fonctionnera pas correctement

**Note :** Si shutdown immédiat (`shutdown now`), pas le temps d'annuler !

---

### Question 26 : **Réponse B** - `shutdown -r +15 "Maintenance"`

**Explication :**
Syntaxe complète de `shutdown` :
```bash
shutdown [OPTIONS] TIME [MESSAGE]
```

**Options principales :**
- `-h` : Halt (arrêt)
- `-r` : Reboot (redémarrage) ✅
- `-H` : Halt sans power off
- `-P` : Power off
- `-c` : Cancel
- `-k` : Fake (envoie message mais n'arrête pas)

**Format de TIME :**
- `now` : Immédiatement
- `+M` : Dans M minutes (ex: `+15`)
- `HH:MM` : À heure précise (ex: `22:30`)

**Exemples pratiques :**
```bash
# Redémarrer dans 15 min avec message
sudo shutdown -r +15 "Maintenance système"

# Arrêter à 23h00
sudo shutdown -h 23:00

# Arrêter dans 5 min
sudo shutdown -h +5

# Redémarrer maintenant
sudo shutdown -r now

# Fake shutdown (test notifications)
sudo shutdown -k +10 "Test message"
```

**Pourquoi les autres sont fausses :**
- A) `reboot` ne prend pas de délai ni message
- C) `systemctl reboot` ne supporte pas `--delay`
- D) `init 6` ne prend pas d'arguments

---

### Question 27 : **Réponse C** - `wall`

**Explication :**
- **wall** = **W**rite to **ALL** users
- Envoie message broadcast à TOUS les utilisateurs connectés (tous les terminaux)
- Utilisé par `shutdown` automatiquement

**Exemples d'utilisation :**
```bash
# Message simple
wall "Le serveur sera redémarré dans 10 minutes!"

# Message depuis fichier
wall < /tmp/maintenance_notice.txt

# Message avec echo
echo "Attention: mise à jour en cours" | wall

# Sur tous les terminaux (nécessite sudo pour autres utilisateurs)
sudo wall "URGENT: Sauvegardez votre travail!"
```

**Ce que voient les utilisateurs :**
```
Broadcast message from admin@server (Mon Jan 28 15:30:00 2026):

Le serveur sera redémarré dans 10 minutes!
```

**Pourquoi les autres sont fausses :**
- A) `broadcast` n'est pas une commande standard
- B) `notify-all` n'existe pas
- D) `announce` n'existe pas

**Commandes similaires :**
- `write <user>` : Envoyer message à UN utilisateur spécifique
- `mesg y/n` : Autoriser/bloquer réception de messages

---

### Question 28 : **Réponse C** - `systemctl get-default`

**Explication :**
- Affiche le target par défaut (celui au boot)
- Lit le lien symbolique `/etc/systemd/system/default.target`

**Exemples :**
```bash
# Afficher target par défaut
$ systemctl get-default
graphical.target

# Changer target par défaut
$ sudo systemctl set-default multi-user.target
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target → /lib/systemd/system/multi-user.target.

# Vérifier
$ systemctl get-default
multi-user.target

# Voir le lien symbolique directement
$ ls -l /etc/systemd/system/default.target
lrwxrwxrwx 1 root root 40 Jan 28 10:00 /etc/systemd/system/default.target -> /lib/systemd/system/multi-user.target
```

**Commandes systemd pour targets :**
```bash
systemctl get-default           # Afficher target par défaut
systemctl set-default <target>  # Définir target par défaut
systemctl isolate <target>      # Changer vers target (temporaire)
systemctl list-units --type=target  # Lister tous les targets
```

**Pourquoi les autres sont fausses :**
- A) `get-target` n'existe pas
- B) `show-default` n'existe pas
- D) `default` seul n'existe pas

---

### Question 29 : **Réponse D** - S4

**Explication :**
**États ACPI (Advanced Configuration and Power Interface) :**

| État | Nom | Description | RAM | Disque | Réveil |
|------|-----|-------------|-----|--------|--------|
| **S0** | Working | Système allumé | ✅ | ✅ | N/A |
| **S1** | Standby | CPU arrêté | ✅ | ✅ | Rapide |
| **S2** | (Rarement utilisé) | | ✅ | ✅ | |
| **S3** | Suspend to RAM | Sleep/Veille | ✅ | ❌ | Rapide (2-3s) |
| **S4** | Suspend to Disk | **Hibernation** ✅ | ❌ | ✅ | Lent (20-30s) |
| **S5** | Soft Off | Arrêt logiciel | ❌ | ❌ | Boot complet |
| **G3** | Mechanical Off | Interrupteur physique | ❌ | ❌ | Impossible |

**S4 - Hibernation détaillée :**
- Contenu RAM → Sauvegardé sur disque (swap/partition dédiée)
- Système éteint complètement (0 W consommation)
- Au réveil : Swap → Restauré en RAM
- État exact restauré (applications, fichiers ouverts...)

**Commandes Linux :**
```bash
# Suspend to RAM (S3)
sudo systemctl suspend

# Hibernation (S4)
sudo systemctl hibernate

# Hybride (S3 + S4)
sudo systemctl hybrid-sleep
```

**Pourquoi les autres sont fausses :**
- A) S1 = Standby (CPU off, RAM alimentée)
- B) S2 = Rarement implémenté
- C) S3 = Suspend to RAM (veille classique)

---

### Question 30 : **Réponse A** - `shutdown -r 22:30`

**Explication :**
Format `HH:MM` pour heure absolue (24h)

**Syntaxe shutdown TIME :**
1. **Immédiat :** `now`
2. **Relatif (minutes) :** `+M` (ex: `+30`)
3. **Absolu (heure) :** `HH:MM` (ex: `22:30`) ✅

**Exemples concrets :**
```bash
# À 22h30 précise (ce soir)
sudo shutdown -r 22:30

# Dans 90 minutes
sudo shutdown -r +90

# Demain à 03h00 (si après minuit)
# Utiliser 'at' ou cron pour planifications futures
echo "shutdown -r now" | at 03:00 tomorrow
```

**Pourquoi les autres sont fausses :**
- B) `+22:30` serait interprété comme "+22 minutes" (`:30` ignoré/erreur)
- C) `reboot` ne supporte pas `--at`
- D) `systemctl reboot` ne supporte pas `--scheduled`

**Alternative pour planifications complexes :**
```bash
# Planifier avec 'at'
echo "shutdown -r now" | at 22:30

# Planifier avec cron
# Dans crontab -e:
30 22 * * * /sbin/shutdown -r now
```

**Conseil pour l'examen :**
- `+M` = Relatif (dans M minutes)
- `HH:MM` = Absolu (à cette heure)
- Pas de `+HH:MM` !

---

## 📊 Tableau de scoring

| Score | Évaluation | Action recommandée |
|-------|------------|-------------------|
| 28-30 | 🏆 Excellent | Sujet maîtrisé ! Passez au suivant |
| 24-27 | ✅ Très bien | Relire sections avec erreurs |
| 20-23 | ⚠️ Bien | Revoir notes + refaire QCM |
| 15-19 | 📚 Moyen | Retravailler le sujet en profondeur |
| < 15 | ❌ Insuffisant | Reprendre depuis le début |

---

## 🎯 Prochaines étapes

1. **Notez votre score :** _____ / 30
2. **Identifiez vos points faibles :**
   - [ ] Section 101.1 (matériel)
   - [ ] Section 101.2 (boot)
   - [ ] Section 101.3 (runlevels/shutdown)
3. **Relisez les notes** pour vos sections faibles
4. **Pratiquez en labs** les commandes que vous maîtrisez mal
5. **Refaites le QCM** dans 2-3 jours (objectif 100%)

---

**🎓 Conseil final :**  
L'examen LPIC-1 teste la COMPRÉHENSION, pas la mémorisation pure. Assurez-vous de comprendre le **pourquoi** derrière chaque commande et concept !

**Prêt pour le Sujet 102 ?** → [Notes-Revision-Sujet-102.md](../Notes/Notes-Revision-Sujet-102.md)
