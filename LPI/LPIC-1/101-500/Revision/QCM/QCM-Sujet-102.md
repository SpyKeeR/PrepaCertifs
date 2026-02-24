# 🧪 QCM Sujet 102 : Installation Linux et Gestion des Paquets

> **Nombre de questions :** 40  
> **Poids du sujet :** 10 points (~25% de l'examen)  
> **Durée estimée :** 60 minutes  
> **Objectif :** 75% minimum (30/40)

---

## 📋 Instructions

- Lisez attentivement chaque question
- Une seule réponse correcte par question (sauf mention contraire)
- Les réponses sont en fin de document avec explications détaillées
- Ne trichez pas ! Testez vos vraies connaissances
- Notez vos réponses avant de regarder les corrections

---

## 💾 Section 102.1 : Conception du schéma de partitionnement (12 questions)

### Question 1
Quelle est la limite de taille maximale d'un disque avec partitionnement MBR ?

- [ ] A) 1 TB  
- [ ] B) 2 TB  
- [ ] C) 4 TB  
- [ ] D) 8 TB

---

### Question 2
Combien de partitions primaires maximum peut-on créer sur un disque MBR ?

- [ ] A) 2  
- [ ] B) 4  
- [ ] C) 8  
- [ ] D) 16

---

### Question 3
Quelle commande crée un système de fichiers ext4 sur /dev/sdb1 ?

- [ ] A) `mkfs /dev/sdb1 ext4`  
- [ ] B) `mkfs.ext4 /dev/sdb1`  
- [ ] C) `format -t ext4 /dev/sdb1`  
- [ ] D) `ext4fs /dev/sdb1`

---

### Question 4
Dans le fichier /etc/fstab, que signifie le dernier chiffre (6ème colonne) ?

- [ ] A) Priorité de montage  
- [ ] B) Ordre de vérification fsck  
- [ ] C) Numéro de partition  
- [ ] D) Niveau de dump

---

### Question 5
Quelle option de montage empêche l'exécution de binaires sur une partition ?

- [ ] A) `norun`  
- [ ] B) `noexec`  
- [ ] C) `nobinary`  
- [ ] D) `secure`

---

### Question 6
**CHOIX MULTIPLES** - Quelles commandes permettent de créer des partitions ?

- [ ] A) `fdisk`  
- [ ] B) `gdisk`  
- [ ] C) `parted`  
- [ ] D) `mkpart`  
- [ ] E) `diskpart`

---

### Question 7
Dans LVM, quel est l'ordre hiérarchique correct ?

- [ ] A) VG → PV → LV  
- [ ] B) PV → VG → LV  
- [ ] C) LV → VG → PV  
- [ ] D) PV → LV → VG

---

### Question 8
Quelle commande crée un Physical Volume LVM sur /dev/sdc ?

- [ ] A) `lvcreate /dev/sdc`  
- [ ] B) `vgcreate /dev/sdc`  
- [ ] C) `pvcreate /dev/sdc`  
- [ ] D) `pvmake /dev/sdc`

---

### Question 9
Quelle commande étend un Logical Volume de 10 GB supplémentaires ?

- [ ] A) `lvextend -L +10G /dev/vg/lv`  
- [ ] B) `lvgrow +10G /dev/vg/lv`  
- [ ] C) `lvexpand -s 10G /dev/vg/lv`  
- [ ] D) `lvresize --add 10G /dev/vg/lv`

---

### Question 10
Quel niveau RAID offre la meilleure tolérance aux pannes (2 disques peuvent tomber) ?

- [ ] A) RAID 0  
- [ ] B) RAID 1  
- [ ] C) RAID 5  
- [ ] D) RAID 6

---

### Question 11
Quelle commande active une partition swap ?

- [ ] A) `swap -a /dev/sdb2`  
- [ ] B) `swapon /dev/sdb2`  
- [ ] C) `mount -t swap /dev/sdb2`  
- [ ] D) `enable-swap /dev/sdb2`

---

### Question 12
Dans /etc/fstab, quelle option empêche le montage automatique au boot ?

- [ ] A) `noboot`  
- [ ] B) `noauto`  
- [ ] C) `manual`  
- [ ] D) `nomount`

---

## 🥾 Section 102.2 : Installation d'un gestionnaire de démarrage (8 questions)

### Question 13
Quelle commande installe GRUB 2 sur le MBR de /dev/sda ?

- [ ] A) `grub-install /dev/sda1`  
- [ ] B) `grub-install /dev/sda`  
- [ ] C) `install-grub /dev/sda`  
- [ ] D) `grub2-setup /dev/sda`

---

### Question 14
Quel fichier doit être édité pour modifier la configuration GRUB 2 de manière permanente ?

- [ ] A) `/boot/grub/grub.cfg`  
- [ ] B) `/etc/default/grub`  
- [ ] C) `/etc/grub.conf`  
- [ ] D) `/boot/grub/menu.lst`

---

### Question 15
Quelle commande régénère le fichier grub.cfg sur Debian/Ubuntu ?

- [ ] A) `grub-update`  
- [ ] B) `update-grub`  
- [ ] C) `grub-mkconfig`  
- [ ] D) `grub-refresh`

---

### Question 16
Dans GRUB 2, que représente la notation (hd0,1) ?

- [ ] A) Premier disque, première partition  
- [ ] B) Deuxième disque, première partition  
- [ ] C) Premier disque, deuxième partition  
- [ ] D) Disque 0, secteur 1

---

### Question 17
Quelle touche permet d'éditer une entrée GRUB au démarrage ?

- [ ] A) `F2`  
- [ ] B) `e`  
- [ ] C) `Tab`  
- [ ] D) `Esc`

---

### Question 18
Où se monte généralement la partition ESP (EFI System Partition) sur un système UEFI ?

- [ ] A) `/boot`  
- [ ] B) `/boot/efi`  
- [ ] C) `/efi`  
- [ ] D) `/sys/firmware/efi`

---

### Question 19
Dans /etc/default/grub, quel paramètre définit le délai d'attente du menu GRUB en secondes ?

- [ ] A) `GRUB_DELAY`  
- [ ] B) `GRUB_TIMEOUT`  
- [ ] C) `GRUB_WAIT`  
- [ ] D) `GRUB_TIMER`

---

### Question 20
**SCÉNARIO** - GRUB est cassé et vous voyez "grub rescue>". Quelle est la première commande pour lister les partitions ?

- [ ] A) `list`  
- [ ] B) `ls`  
- [ ] C) `show partitions`  
- [ ] D) `fdisk -l`

---

## 📚 Section 102.3 : Gestion des bibliothèques partagées (5 questions)

### Question 21
Quelle commande affiche les bibliothèques partagées utilisées par /bin/ls ?

- [ ] A) `libs /bin/ls`  
- [ ] B) `ldd /bin/ls`  
- [ ] C) `ldconfig -l /bin/ls`  
- [ ] D) `showlibs /bin/ls`

---

### Question 22
Quelle commande met à jour le cache des bibliothèques partagées ?

- [ ] A) `ldconfig`  
- [ ] B) `ldd -u`  
- [ ] C) `updatelibs`  
- [ ] D) `libcache --refresh`

---

### Question 23
Dans quel fichier configure-t-on les chemins de recherche des bibliothèques partagées ?

- [ ] A) `/etc/libraries.conf`  
- [ ] B) `/etc/ld.so.conf`  
- [ ] C) `/etc/lib.conf`  
- [ ] D) `/etc/ldconfig.conf`

---

### Question 24
Quelle variable d'environnement permet d'ajouter temporairement un chemin de bibliothèques ?

- [ ] A) `LIBRARY_PATH`  
- [ ] B) `LD_LIBRARY_PATH`  
- [ ] C) `LIB_PATH`  
- [ ] D) `SHARED_LIBS`

---

### Question 25
Quelle extension ont les bibliothèques partagées sous Linux ?

- [ ] A) `.dll`  
- [ ] B) `.lib`  
- [ ] C) `.so`  
- [ ] D) `.dylib`

---

## 📦 Section 102.4 : Gestion des paquets Debian (10 questions)

### Question 26
Quelle commande installe un fichier .deb local ?

- [ ] A) `apt install package.deb`  
- [ ] B) `dpkg -i package.deb`  
- [ ] C) `deb-install package.deb`  
- [ ] D) `apt-get -f package.deb`

---

### Question 27
Quelle commande supprime un paquet en conservant les fichiers de configuration ?

- [ ] A) `apt purge package`  
- [ ] B) `apt remove package`  
- [ ] C) `dpkg -P package`  
- [ ] D) `apt delete package`

---

### Question 28
Quelle commande liste tous les paquets installés avec dpkg ?

- [ ] A) `dpkg --list`  
- [ ] B) `dpkg -l`  
- [ ] C) `dpkg --get-selections`  
- [ ] D) Toutes les réponses ci-dessus

---

### Question 29
Quelle commande permet de trouver quel paquet fournit le fichier /bin/ls ?

- [ ] A) `dpkg -S /bin/ls`  
- [ ] B) `apt-file search /bin/ls`  
- [ ] C) `dpkg --search /bin/ls`  
- [ ] D) A et C sont correctes

---

### Question 30
Quelle commande met à jour la liste des paquets disponibles ?

- [ ] A) `apt upgrade`  
- [ ] B) `apt update`  
- [ ] C) `apt refresh`  
- [ ] D) `apt fetch`

---

### Question 31
Où se trouve le fichier de configuration principal des sources de paquets ?

- [ ] A) `/etc/apt/sources.conf`  
- [ ] B) `/etc/apt/sources.list`  
- [ ] C) `/etc/sources.list`  
- [ ] D) `/etc/apt.conf`

---

### Question 32
Quelle commande recherche un paquet contenant le mot-clé "nginx" ?

- [ ] A) `apt search nginx`  
- [ ] B) `apt find nginx`  
- [ ] C) `apt-cache search nginx`  
- [ ] D) A et C sont correctes

---

### Question 33
Quelle commande affiche des informations détaillées sur le paquet nginx ?

- [ ] A) `apt info nginx`  
- [ ] B) `apt show nginx`  
- [ ] C) `apt-cache show nginx`  
- [ ] D) B et C sont correctes

---

### Question 34
Quelle commande supprime les paquets qui ne sont plus nécessaires ?

- [ ] A) `apt clean`  
- [ ] B) `apt autoclean`  
- [ ] C) `apt autoremove`  
- [ ] D) `apt purge-unused`

---

### Question 35
**CHOIX MULTIPLES** - Quels sont les composants principaux d'un dépôt Ubuntu ?

- [ ] A) `main`  
- [ ] B) `core`  
- [ ] C) `restricted`  
- [ ] D) `universe`  
- [ ] E) `multiverse`  
- [ ] F) `contrib`

---

## 🔴 Section 102.5 : Gestion des paquets RPM et YUM (5 questions)

### Question 36
Quelle commande installe un fichier .rpm avec affichage de progression ?

- [ ] A) `rpm -i package.rpm`  
- [ ] B) `rpm -ivh package.rpm`  
- [ ] C) `rpm --install package.rpm`  
- [ ] D) `rpm -Uvh package.rpm`

---

### Question 37
Quelle commande liste tous les paquets installés avec RPM ?

- [ ] A) `rpm -l`  
- [ ] B) `rpm -qa`  
- [ ] C) `rpm --list`  
- [ ] D) `rpm --all`

---

### Question 38
Quelle commande permet de trouver quel paquet RPM fournit le fichier /usr/sbin/httpd ?

- [ ] A) `rpm -qf /usr/sbin/httpd`  
- [ ] B) `rpm --whatprovides /usr/sbin/httpd`  
- [ ] C) `rpm -S /usr/sbin/httpd`  
- [ ] D) `yum provides /usr/sbin/httpd`

---

### Question 39
Où se trouvent les fichiers de configuration des dépôts yum/dnf ?

- [ ] A) `/etc/yum.conf.d/`  
- [ ] B) `/etc/yum.repos.d/`  
- [ ] C) `/etc/dnf/repos/`  
- [ ] D) `/etc/repositories/`

---

### Question 40
Quelle commande est le successeur de yum sur RHEL 8+ et Fedora ?

- [ ] A) `yum2`  
- [ ] B) `dnf`  
- [ ] C) `zypper`  
- [ ] D) `pacman`

---

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Section 102.1 : Conception du schéma de partitionnement

### Question 1 : **Réponse B** - 2 TB

**Explication :**
- **MBR** (Master Boot Record) a une limite de **2 TB** par disque
- Limitation due à l'adressage 32-bit avec secteurs de 512 octets
- Calcul : 2^32 × 512 octets = 2 TB

**Pourquoi MBR limité à 2 TB :**
- Adressage LBA (Logical Block Addressing) sur 32 bits
- 2^32 = 4,294,967,296 secteurs
- 4,294,967,296 × 512 octets = 2,199,023,255,552 octets ≈ 2 TB

**Solution pour disques > 2 TB :**
- Utiliser **GPT** (GUID Partition Table)
- Limite GPT : 9.4 ZB (zettabytes) - pratiquement illimitée

**Pourquoi les autres sont fausses :**
- A) 1 TB : Trop bas
- C, D) 4 TB et 8 TB : Dépassent la limite MBR

**Conseil pour l'examen :**
Retenez : MBR = 2 TB max, GPT = quasi illimité

---

### Question 2 : **Réponse B** - 4

**Explication :**
Sur un disque MBR, vous pouvez créer **4 partitions primaires maximum**.

**Solutions pour plus de 4 partitions :**
1. Utiliser **1 partition étendue** (compte comme primaire)
2. Créer **partitions logiques** dans l'étendue (nombre illimité)

**Schéma classique :**
```
Primaire 1: /boot       500 MB
Primaire 2: /           30 GB
Primaire 3: swap        4 GB
Étendue (Primaire 4):
  ├─ Logique 5: /home   50 GB
  ├─ Logique 6: /var    20 GB
  └─ Logique 7: /opt    10 GB
```

**Avec GPT :**
- Jusqu'à **128 partitions** par défaut (extensible)
- Pas de distinction primaire/étendue/logique

**Pourquoi les autres sont fausses :**
- A) 2 : Trop peu
- C) 8, D) 16 : Nombre de partitions logiques possibles, pas primaires

---

### Question 3 : **Réponse B** - `mkfs.ext4 /dev/sdb1`

**Explication :**
La commande correcte est `mkfs.ext4` suivie du périphérique.

**Syntaxe générale :**
```bash
mkfs.type /dev/device
```

**Exemples pour différents systèmes de fichiers :**
```bash
mkfs.ext4 /dev/sdb1      # ext4 (Linux standard)
mkfs.ext3 /dev/sdb1      # ext3 (ancien)
mkfs.xfs /dev/sdb1       # XFS (RHEL par défaut)
mkfs.vfat -F 32 /dev/sdb1  # FAT32
mkfs.ntfs /dev/sdb1      # NTFS (Windows)
mkfs.btrfs /dev/sdb1     # Btrfs (moderne)
```

**Options utiles ext4 :**
```bash
# Avec label
mkfs.ext4 -L "Data" /dev/sdb1

# Réserver moins d'espace pour root (1% au lieu de 5%)
mkfs.ext4 -m 1 /dev/sdb1

# Taille de bloc spécifique
mkfs.ext4 -b 4096 /dev/sdb1
```

**Pourquoi les autres sont fausses :**
- A) Ordre des arguments inversé
- C) `format` n'existe pas sous Linux (commande DOS/Windows)
- D) `ext4fs` n'est pas une commande

---

### Question 4 : **Réponse B** - Ordre de vérification fsck

**Explication :**
Le 6ème champ de /etc/fstab définit l'ordre de vérification par `fsck` au boot.

**Valeurs possibles :**
- **0** : Pas de vérification fsck
- **1** : Première vérification (réservé pour `/`)
- **2** : Vérification après `/` (autres partitions)

**Format complet /etc/fstab :**
```
<device>  <mount>  <type>  <options>  <dump>  <pass>
```

**Exemple annoté :**
```bash
# Root : vérifié en premier (pass=1)
UUID=xxx  /      ext4  defaults  0  1

# Home : vérifié en second (pass=2)
UUID=yyy  /home  ext4  defaults  0  2

# Swap : jamais vérifié (pass=0)
UUID=zzz  none   swap  sw        0  0

# Partition noauto : pas vérifié
/dev/sdb1 /mnt/data ext4 noauto   0  0
```

**Comportement fsck :**
- `pass=0` : Ignoré
- `pass=1` : Vérifié seul (critique)
- `pass=2` : Vérifié en parallèle après pass=1

**Pourquoi les autres sont fausses :**
- A) Priorité de montage : Non, c'est l'ordre dans fstab
- C) Numéro de partition : Non, c'est le 1er champ (device)
- D) Niveau de dump : Non, c'est le 5ème champ (obsolète)

---

### Question 5 : **Réponse B** - `noexec`

**Explication :**
L'option `noexec` empêche l'exécution de binaires sur la partition montée.

**Usage typique :**
```bash
# Monter /tmp avec noexec (sécurité)
tmpfs  /tmp  tmpfs  defaults,noexec,nosuid,nodev  0  0

# Partition utilisateur sans exécution
UUID=xxx  /home/user/downloads  ext4  noexec,nosuid  0  2
```

**Autres options de sécurité :**
- **`nosuid`** : Ignore bit SUID/SGID (empêche élévation privilèges)
- **`nodev`** : Ignore fichiers de périphériques
- **`ro`** : Lecture seule (read-only)

**Options de performance :**
- **`noatime`** : Ne met pas à jour access time (plus rapide)
- **`nodiratime`** : Idem pour répertoires seulement
- **`relatime`** : Mise à jour access time relative (compromise)

**Options courantes :**
- **`defaults`** = `rw,suid,dev,exec,auto,nouser,async`
- **`rw`** / **`ro`** : Read-write / Read-only
- **`auto`** / **`noauto`** : Montage automatique boot
- **`user`** : Autoriser utilisateurs à monter

**Pourquoi les autres sont fausses :**
- A, C, D) Ces options n'existent pas

**Conseil sécurité :**
Toujours utiliser `noexec,nosuid,nodev` sur `/tmp`, `/var/tmp`, et partitions utilisateur.

---

### Question 6 : **Réponses A, B, C** - fdisk, gdisk, parted

**Explication :**

**`fdisk`** - Outil classique (MBR et GPT)
```bash
sudo fdisk /dev/sda
# Mode interactif
# Commandes : n (new), d (delete), p (print), w (write)
```

**`gdisk`** - Spécialisé GPT
```bash
sudo gdisk /dev/sda
# Syntaxe similaire à fdisk
# Optimisé pour partitions GPT
```

**`parted`** - Universel (MBR et GPT)
```bash
sudo parted /dev/sda
# Mode interactif ou commande directe
sudo parted /dev/sda mkpart primary ext4 1MiB 10GiB
```

**Comparaison :**

| Outil | MBR | GPT | Interface | Usage |
|-------|-----|-----|-----------|-------|
| fdisk | ✅ | ✅ | Interactive | Classique |
| gdisk | ❌ | ✅ | Interactive | GPT only |
| parted | ✅ | ✅ | Interactive + CLI | Flexible |
| cfdisk | ✅ | ✅ | TUI (ncurses) | Visuel |
| sgdisk | ❌ | ✅ | CLI only | Scripts |

**Pourquoi les autres sont fausses :**
- D) `mkpart` : C'est une **commande** de parted, pas un outil
- E) `diskpart` : Outil Windows, pas Linux

---

### Question 7 : **Réponse B** - PV → VG → LV

**Explication :**
La hiérarchie LVM est :

```
1. Physical Volumes (PV) - Disques physiques
   ↓
2. Volume Groups (VG) - Pool de PVs
   ↓
3. Logical Volumes (LV) - Partitions virtuelles
```

**Analogie :**
- **PV** = Briques individuelles
- **VG** = Palette de briques
- **LV** = Constructions faites avec briques de la palette

**Exemple concret :**
```bash
# 1. Créer PVs (disques /dev/sdb et /dev/sdc)
sudo pvcreate /dev/sdb /dev/sdc

# 2. Créer VG (combiner les PVs)
sudo vgcreate vg_data /dev/sdb /dev/sdc
# VG de 2 TB si 2 disques de 1 TB

# 3. Créer LVs (découper le VG)
sudo lvcreate -L 500G -n lv_backups vg_data
sudo lvcreate -L 1T -n lv_archives vg_data
sudo lvcreate -l 100%FREE -n lv_temp vg_data

# 4. Formater et utiliser LVs
mkfs.ext4 /dev/vg_data/lv_backups
mount /dev/vg_data/lv_backups /mnt/backups
```

**Pourquoi cette hiérarchie :**
- Flexibilité : Ajouter disques au VG à chaud
- Redimensionnement : Étendre/réduire LVs facilement
- Snapshots : Sauvegardes instantanées

**Pourquoi les autres sont fausses :**
- A, C, D) Ordre incorrect

---

### Question 8 : **Réponse C** - `pvcreate /dev/sdc`

**Explication :**
`pvcreate` initialise un disque/partition comme Physical Volume LVM.

**Commandes LVM par niveau :**

**Physical Volumes :**
```bash
pvcreate /dev/sdc        # Créer PV
pvs                      # Lister PVs (résumé)
pvdisplay                # Lister PVs (détaillé)
pvremove /dev/sdc        # Supprimer PV
```

**Volume Groups :**
```bash
vgcreate vg_name /dev/sdc /dev/sdd  # Créer VG
vgs                      # Lister VGs
vgdisplay                # Détails VGs
vgextend vg_name /dev/sde  # Ajouter PV au VG
vgreduce vg_name /dev/sde  # Retirer PV du VG
vgremove vg_name         # Supprimer VG
```

**Logical Volumes :**
```bash
lvcreate -L 100G -n lv_name vg_name  # Créer LV
lvs                      # Lister LVs
lvdisplay                # Détails LVs
lvextend -L +50G /dev/vg/lv  # Étendre LV
lvreduce -L -20G /dev/vg/lv  # Réduire LV
lvremove /dev/vg/lv      # Supprimer LV
```

**Pourquoi les autres sont fausses :**
- A) `lvcreate` : Crée Logical Volume (étape 3)
- B) `vgcreate` : Crée Volume Group (étape 2)
- D) `pvmake` : N'existe pas

**Conseil mnémotechnique :**
**p**v = **p**hysique, **v**g = **g**roupe, **l**v = **l**ogique

---

### Question 9 : **Réponse A** - `lvextend -L +10G /dev/vg/lv`

**Explication :**
`lvextend -L +10G` ajoute 10 GB au Logical Volume.

**Syntaxe lvextend :**
```bash
# Ajouter taille relative
lvextend -L +10G /dev/vg_data/lv_backups

# Définir taille absolue
lvextend -L 200G /dev/vg_data/lv_backups

# Utiliser tout l'espace libre
lvextend -l +100%FREE /dev/vg_data/lv_backups

# Étendre + redimensionner filesystem automatiquement
lvextend -r -L +10G /dev/vg_data/lv_backups
```

**⚠️ IMPORTANT :** Après lvextend, redimensionner filesystem !

```bash
# Pour ext4 (online - monté)
resize2fs /dev/vg_data/lv_backups

# Pour XFS (online)
xfs_growfs /mnt/backups

# Pour ext4 (offline - démonté)
umount /mnt/backups
e2fsck -f /dev/vg_data/lv_backups
resize2fs /dev/vg_data/lv_backups
mount /dev/vg_data/lv_backups /mnt/backups
```

**Workflow complet :**
```bash
# 1. Vérifier espace disponible VG
vgs vg_data

# 2. Étendre LV
sudo lvextend -L +10G /dev/vg_data/lv_backups

# 3. Étendre filesystem
sudo resize2fs /dev/vg_data/lv_backups

# 4. Vérifier
df -h /mnt/backups
```

**Pourquoi les autres sont fausses :**
- B) `lvgrow` : N'existe pas
- C) `lvexpand` : N'existe pas
- D) `lvresize --add` : Syntaxe incorrecte (`lvresize -L +10G` existe)

---

### Question 10 : **Réponse D** - RAID 6

**Explication :**
**RAID 6** tolère la panne de **2 disques simultanément**.

**Tableau comparatif RAID :**

| RAID | Disques min | Capacité | Pannes tolérées | Performance Lecture | Performance Écriture |
|------|-------------|----------|-----------------|--------------------|--------------------|
| **0** | 2 | 100% (n×) | Aucune | +++  | +++ |
| **1** | 2 | 50% (n÷2) | n-1 | ++   | + |
| **5** | 3 | (n-1)× | **1 disque** | ++   | - |
| **6** | 4 | (n-2)× | **2 disques** ✅ | ++   | -- |
| **10** | 4 | 50% | 1 par miroir | +++  | ++ |

**RAID 6 - Double parité :**
- Utilise **2 disques** pour parité (au lieu de 1 pour RAID 5)
- Peut perdre **2 disques** sans perte de données
- Reconstruction plus lente que RAID 5
- Meilleur pour grandes capacités (risque panne pendant rebuild)

**Exemple RAID 6 avec 6 disques de 1 TB :**
- Capacité utilisable : (6-2) × 1 TB = **4 TB**
- Parité : 2 TB
- Peut perdre 2 disques quelconques

**Pourquoi les autres sont fausses :**
- A) RAID 0 : Aucune tolérance (striping pur)
- B) RAID 1 : Tolère n-1 disques (miroir)
- C) RAID 5 : Tolère 1 disque seulement

**Conseil :**
RAID 6 pour données critiques, RAID 10 pour performance + fiabilité.

---

### Question 11 : **Réponse B** - `swapon /dev/sdb2`

**Explication :**
`swapon` active une partition ou fichier swap.

**Workflow complet swap :**
```bash
# 1. Créer partition swap (type 82)
sudo fdisk /dev/sdb
# n, p, 2, [Enter], +4G, t, 2, 82, w

# 2. Formater en swap
sudo mkswap /dev/sdb2

# 3. Activer swap
sudo swapon /dev/sdb2

# 4. Vérifier
swapon --show
free -h

# 5. Rendre permanent (/etc/fstab)
echo "/dev/sdb2  none  swap  sw  0  0" | sudo tee -a /etc/fstab
```

**Autres commandes swap :**
```bash
# Désactiver swap
swapoff /dev/sdb2

# Afficher swap actifs
swapon --show
swapon -s

# Activer avec priorité
swapon -p 10 /dev/sdb2

# Activer tous les swaps de fstab
swapon -a
```

**Fichier swap (alternative à partition) :**
```bash
# Créer fichier de 2 GB
sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Permanent
echo "/swapfile  none  swap  sw  0  0" >> /etc/fstab
```

**Pourquoi les autres sont fausses :**
- A) `swap -a` : Commande n'existe pas
- C) `mount -t swap` : Swap ne se monte pas (s'active)
- D) `enable-swap` : N'existe pas

---

### Question 12 : **Réponse B** - `noauto`

**Explication :**
L'option `noauto` empêche le montage automatique au démarrage.

**Exemple /etc/fstab avec noauto :**
```bash
# Partition montée automatiquement au boot
UUID=xxx  /home  ext4  defaults  0  2

# Partition NON montée au boot (montage manuel)
UUID=yyy  /mnt/backup  ext4  defaults,noauto  0  0

# CD/DVD (jamais auto, utilisateur peut monter)
/dev/sr0  /media/cdrom  auto  noauto,user  0  0
```

**Usage typique de noauto :**
- Partitions externes (USB, disques amovibles)
- Partitions de backup (montées à la demande)
- CD/DVD
- Partitions réseau (NFS, CIFS) optionnelles

**Montage manuel partition noauto :**
```bash
# Monter via fstab (suffit de préciser mount point)
sudo mount /mnt/backup

# Équivalent complet
sudo mount -t ext4 /dev/sdb1 /mnt/backup
```

**Autres options de montage importantes :**
- **`auto`** : Montage automatique (défaut dans `defaults`)
- **`user`** : Utilisateurs non-root peuvent monter
- **`nouser`** : Seul root peut monter (défaut)
- **`_netdev`** : Attendre réseau avant montage (NFS, iSCSI)

**Pourquoi les autres sont fausses :**
- A) `noboot` : N'existe pas
- C) `manual` : N'existe pas
- D) `nomount` : N'existe pas

---

## Section 102.2 : Installation d'un gestionnaire de démarrage

### Question 13 : **Réponse B** - `grub-install /dev/sda`

**Explication :**
GRUB s'installe sur le **disque entier** (/dev/sda), PAS sur une partition (/dev/sda1).

**Installation GRUB BIOS/MBR :**
```bash
# Installer sur MBR de /dev/sda
sudo grub-install /dev/sda

# Avec répertoire boot personnalisé
sudo grub-install --boot-directory=/mnt/boot /dev/sda

# Forcer réinstallation
sudo grub-install --force /dev/sda

# Vérifier version
grub-install --version
```

**Installation GRUB UEFI :**
```bash
# Installer pour UEFI 64-bit
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi

# Avec bootloader-id personnalisé
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Ubuntu

# UEFI 32-bit (rare)
sudo grub-install --target=i386-efi --efi-directory=/boot/efi
```

**⚠️ ERREUR FRÉQUENTE :**
```bash
# INCORRECT (ne fonctionne pas)
grub-install /dev/sda1   # Partition !

# CORRECT
grub-install /dev/sda    # Disque !
```

**Pourquoi :**
- MBR se trouve dans **premier secteur du disque**, pas d'une partition
- GRUB écrit boot code dans MBR + secteurs suivants

**Après installation :**
```bash
# Générer config
sudo update-grub

# Ou
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

**Pourquoi les autres sont fausses :**
- A) `/dev/sda1` : Partition (erreur fréquente !)
- C) `install-grub` : Commande n'existe pas
- D) `grub2-setup` : Commande obsolète/interne

---

### Question 14 : **Réponse B** - `/etc/default/grub`

**Explication :**
**NE JAMAIS éditer `/boot/grub/grub.cfg` directement !** Ce fichier est généré automatiquement.

**Workflow correct :**
```bash
# 1. Éditer fichier source
sudo nano /etc/default/grub

# 2. Modifier paramètres (exemple)
GRUB_TIMEOUT=10
GRUB_CMDLINE_LINUX_DEFAULT="quiet"

# 3. Régénérer grub.cfg
sudo update-grub

# Le fichier /boot/grub/grub.cfg est recréé automatiquement
```

**Fichiers de configuration GRUB 2 :**

| Fichier | Rôle | Éditable ? |
|---------|------|------------|
| `/etc/default/grub` | Configuration principale | ✅ OUI |
| `/etc/grub.d/*.sh` | Scripts génération | ✅ OUI (avancé) |
| `/boot/grub/grub.cfg` | Config générée | ❌ NON (auto) |

**Paramètres courants `/etc/default/grub` :**
```bash
GRUB_DEFAULT=0                    # Entrée par défaut
GRUB_TIMEOUT=5                    # Délai secondes
GRUB_CMDLINE_LINUX=""             # Params tous modes
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"  # Params normal
GRUB_DISABLE_RECOVERY="false"     # Activer recovery
GRUB_GFXMODE=1024x768             # Résolution
GRUB_BACKGROUND="/path/image.png" # Image fond
```

**Pourquoi les autres sont fausses :**
- A) `/boot/grub/grub.cfg` : Fichier GÉNÉRÉ (ne pas éditer !)
- C) `/etc/grub.conf` : GRUB Legacy (ancien)
- D) `/boot/grub/menu.lst` : GRUB Legacy

---

### Question 15 : **Réponse B** - `update-grub`

**Explication :**
`update-grub` est un script Debian/Ubuntu qui régénère grub.cfg.

**Par distribution :**

| Distribution | Commande |
|--------------|----------|
| Debian/Ubuntu | `update-grub` |
| RHEL/CentOS 7 | `grub2-mkconfig -o /boot/grub2/grub.cfg` |
| RHEL/CentOS 8+ | `grub2-mkconfig -o /boot/grub2/grub.cfg` |
| Arch Linux | `grub-mkconfig -o /boot/grub/grub.cfg` |

**Équivalence :**
```bash
# Ces commandes sont équivalentes:
update-grub

grub-mkconfig -o /boot/grub/grub.cfg
```

**Quand exécuter update-grub :**
- Après modification `/etc/default/grub`
- Après modification scripts `/etc/grub.d/`
- Après installation nouveau kernel
- Après modification partitions

**Processus update-grub :**
1. Lit `/etc/default/grub`
2. Exécute scripts `/etc/grub.d/` (ordre numérique)
3. Détecte kernels dans `/boot`
4. Détecte autres OS (Windows, etc.)
5. Génère `/boot/grub/grub.cfg`

**Pourquoi les autres sont fausses :**
- A) `grub-update` : N'existe pas
- C) `grub-mkconfig` : Existe mais nécessite `-o` (pas direct)
- D) `grub-refresh` : N'existe pas

---

### Question 16 : **Réponse A** - Premier disque, première partition

**Explication :**
Dans GRUB 2, la notation `(hd0,1)` signifie :
- **hd0** : Premier disque (disques comptés depuis 0)
- **1** : Première partition (partitions comptées depuis 1)

**Table de correspondance GRUB 2 ↔ Linux :**

| GRUB 2 | Linux | Description |
|--------|-------|-------------|
| `(hd0,1)` | `/dev/sda1` | 1er disque, 1ère partition |
| `(hd0,2)` | `/dev/sda2` | 1er disque, 2ème partition |
| `(hd1,1)` | `/dev/sdb1` | 2ème disque, 1ère partition |
| `(hd2,5)` | `/dev/sdc5` | 3ème disque, 5ème partition |

**⚠️ Différence GRUB Legacy :**
GRUB Legacy comptait **partitions depuis 0** aussi :
- `(hd0,0)` = `/dev/sda1`
- `(hd0,1)` = `/dev/sda2`

**GRUB 2 : disques depuis 0, partitions depuis 1** ✅

**Exemple dans grub.cfg :**
```bash
menuentry "Ubuntu" {
    set root=(hd0,1)           # /dev/sda1
    linux /vmlinuz root=/dev/sda1 ro
    initrd /initrd.img
}
```

**Pourquoi les autres sont fausses :**
- B) Deuxième disque serait `(hd1,1)`
- C) Deuxième partition serait `(hd0,2)`
- D) Mauvaise interprétation

**Conseil exam :** Retenez que GRUB 2 compte partitions depuis 1 (pas 0) !

---

### Question 17 : **Réponse B** - `e`

**Explication :**
Au menu GRUB, appuyer sur **`e`** permet d'éditer l'entrée sélectionnée.

**Raccourcis clavier GRUB :**

| Touche | Action |
|--------|--------|
| **`e`** | Éditer entrée sélectionnée |
| **`c`** | Ouvrir ligne de commande GRUB |
| **`Esc`** | Retour au menu |
| **`Ctrl+X`** ou **`F10`** | Booter avec modifications |

**Workflow édition GRUB (mode rescue/debug) :**
```
1. Au menu GRUB, sélectionner entrée
2. Appuyer sur 'e'
3. Modifier ligne 'linux' (ajouter paramètres)
   Exemple: Ajouter 'single' pour single-user mode
4. Ctrl+X ou F10 pour booter
```

**Exemple - Démarrer en single-user :**
```bash
# Ligne originale :
linux /vmlinuz root=UUID=xxx ro quiet splash

# Modifier en :
linux /vmlinuz root=UUID=xxx ro single

# Ctrl+X pour booter
```

**Modifications temporaires (session unique) :**
- Changements perdus après redémarrage
- Utile pour dépannage ou récupération mot de passe
- Pour changements permanents : éditer `/etc/default/grub`

**Pourquoi les autres sont fausses :**
- A) F2 : Souvent accès BIOS, pas GRUB
- C) Tab : Complétion dans shell GRUB
- D) Esc : Retour menu (annule édition)

---

### Question 18 : **Réponse B** - `/boot/efi`

**Explication :**
Sur systèmes UEFI, la partition ESP (EFI System Partition) est montée sur **`/boot/efi`**.

**Caractéristiques ESP :**
- **Taille** : 100-550 MB (recommandé 512 MB)
- **Type** : FAT32 (requis par spécification UEFI)
- **Montage** : `/boot/efi`
- **Contenu** : Bootloaders (.efi files)

**Structure typique :**
```bash
/boot/efi/
└── EFI/
    ├── BOOT/
    │   └── BOOTX64.EFI         # Bootloader par défaut
    ├── ubuntu/
    │   ├── grubx64.efi         # GRUB Ubuntu
    │   └── shimx64.efi         # Shim (Secure Boot)
    ├── debian/
    │   └── grubx64.efi
    └── Microsoft/
        └── Boot/
            └── bootmgfw.efi    # Windows Boot Manager
```

**Vérifier montage ESP :**
```bash
# Via mount
mount | grep efi
# /dev/sda1 on /boot/efi type vfat (rw,relatime,...)

# Via lsblk
lsblk -f | grep -i efi

# Via df
df -h /boot/efi
```

**Entrée /etc/fstab pour ESP :**
```bash
UUID=xxxx-xxxx  /boot/efi  vfat  umask=0077  0  1
```

**Pourquoi les autres sont fausses :**
- A) `/boot` : Contient kernels, pas ESP spécifiquement
- C) `/efi` : Nom non standard
- D) `/sys/firmware/efi` : Pseudo-filesystem kernel, pas montage

**Note :** Certaines distributions anciennes utilisaient `/boot/efi`, mais `/boot/efi` est le standard moderne.

---

### Question 19 : **Réponse B** - `GRUB_TIMEOUT`

**Explication :**
`GRUB_TIMEOUT` définit le délai d'attente en secondes avant boot automatique.

**Paramètres timeout dans `/etc/default/grub` :**
```bash
# Délai en secondes (0 = immédiat, -1 = infini)
GRUB_TIMEOUT=5

# Style d'affichage timeout
GRUB_TIMEOUT_STYLE=menu       # Afficher menu
# GRUB_TIMEOUT_STYLE=hidden   # Cacher (Shift pour afficher)
# GRUB_TIMEOUT_STYLE=countdown # Compte à rebours

# Exemple configurations courantes:

# Serveur : boot rapide, pas de menu
GRUB_TIMEOUT=0
GRUB_TIMEOUT_STYLE=hidden

# Desktop : laisser temps de choisir
GRUB_TIMEOUT=10
GRUB_TIMEOUT_STYLE=menu

# Dual-boot : toujours afficher menu
GRUB_TIMEOUT=30
GRUB_TIMEOUT_STYLE=menu
```

**Comportement par valeur :**
- **0** : Boot immédiat sur entrée par défaut
- **1-99** : Attendre X secondes
- **-1** : Attendre infiniment (choix manuel requis)

**Après modification :**
```bash
sudo nano /etc/default/grub
# Modifier GRUB_TIMEOUT=10
sudo update-grub
sudo reboot
```

**Pourquoi les autres sont fausses :**
- A) `GRUB_DELAY` : N'existe pas
- C) `GRUB_WAIT` : N'existe pas
- D) `GRUB_TIMER` : N'existe pas

---

### Question 20 : **Réponse B** - `ls`

**Explication :**
En mode `grub rescue>`, la commande `ls` liste les disques et partitions disponibles.

**Scénario GRUB Rescue (erreur "no such partition") :**
```bash
grub rescue> ls
(hd0) (hd0,gpt1) (hd0,gpt2) (hd0,gpt3)

# Identifier partition Linux (tester chacune)
grub rescue> ls (hd0,gpt2)/
lost+found/ etc/ bin/ boot/ home/ ...

# Définir root
grub rescue> set root=(hd0,gpt2)

# Définir prefix (chemin GRUB)
grub rescue> set prefix=(hd0,gpt2)/boot/grub

# Charger module normal
grub rescue> insmod normal

# Lancer mode normal
grub rescue> normal

# Une fois booté, réinstaller GRUB
sudo grub-install /dev/sda
sudo update-grub
```

**Commandes disponibles en grub rescue :**
```bash
ls                    # Lister disques/partitions
ls (hd0,1)/          # Contenu partition
set                  # Afficher variables
set var=value        # Définir variable
insmod module        # Charger module
normal               # Mode normal
```

**Pourquoi GRUB Rescue apparaît :**
- Partition `/boot` déplacée/redimensionnée
- grub.cfg corrompu/supprimé
- UUID partition changé
- Mauvaise réinstallation système

**Pourquoi les autres sont fausses :**
- A) `list` : N'existe pas
- C) `show partitions` : Syntaxe incorrecte
- D) `fdisk -l` : Commande Linux, pas GRUB

---

## Section 102.3 : Gestion des bibliothèques partagées

### Question 21 : **Réponse B** - `ldd /bin/ls`

**Explication :**
`ldd` (List Dynamic Dependencies) affiche les bibliothèques partagées utilisées par un binaire.

**Exemple sortie :**
```bash
$ ldd /bin/ls
    linux-vdso.so.1 (0x00007ffd8a3e2000)
    libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007f9c8e800000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f9c8e600000)
    libpcre2-8.so.0 => /lib/x86_64-linux-gnu/libpcre2-8.so.0 (0x00007f9c8e500000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f9c8ea00000)
```

**Interprétation :**
```
libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x7f...)
│               │  │                                         │
│               │  │                                         └─ Adresse mémoire
│               │  └─ Chemin réel
│               └─ "trouvée ici"
└─ Bibliothèque demandée
```

**Options ldd :**
```bash
# Afficher unused dependencies
ldd -u /bin/ls

# Verbose
ldd -v /bin/ls

# Vérifier dépendances manquantes
ldd /usr/bin/myapp
# libcustom.so.1 => not found    # ERREUR !
```

**Cas d'usage :**
- Vérifier dépendances avant déploiement
- Diagnostiquer "library not found"
- Analyser dépendances d'une application

**⚠️ SÉCURITÉ :** Ne pas utiliser ldd sur binaires non fiables (exécute code).

**Pourquoi les autres sont fausses :**
- A) `libs` : N'existe pas
- C) `ldconfig -l` : `ldconfig` gère cache, pas dépendances binaires
- D) `showlibs` : N'existe pas

---

### Question 22 : **Réponse A** - `ldconfig`

**Explication :**
`ldconfig` crée/met à jour le cache des bibliothèques partagées (`/etc/ld.so.cache`).

**Usage ldconfig :**
```bash
# Mettre à jour cache
sudo ldconfig

# Afficher cache (bibliothèques disponibles)
ldconfig -p
ldconfig -p | grep ssl
# libssl.so.1.1 (libc6,x86-64) => /usr/lib/x86_64-linux-gnu/libssl.so.1.1

# Verbose (afficher répertoires scannés)
sudo ldconfig -v

# Afficher version
ldconfig -V

# Chercher bibliothèque
ldconfig -p | grep libpython3
```

**Quand exécuter ldconfig :**
1. Après installation bibliothèque manuelle
2. Après modification `/etc/ld.so.conf`
3. Après ajout fichiers dans `/usr/local/lib`
4. Après compilation bibliothèque custom

**Exemple workflow :**
```bash
# 1. Installer bibliothèque custom
sudo cp libcustom.so.1.0.0 /usr/local/lib/
sudo ln -s /usr/local/lib/libcustom.so.1.0.0 /usr/local/lib/libcustom.so.1
sudo ln -s /usr/local/lib/libcustom.so.1 /usr/local/lib/libcustom.so

# 2. Mettre à jour cache
sudo ldconfig

# 3. Vérifier
ldconfig -p | grep libcustom
# libcustom.so.1 (libc6,x86-64) => /usr/local/lib/libcustom.so.1

# 4. Tester avec application
ldd /usr/bin/myapp | grep libcustom
# libcustom.so.1 => /usr/local/lib/libcustom.so.1 (0x7f...)
```

**Fichiers gérés par ldconfig :**
- **Input :** `/etc/ld.so.conf` + `/etc/ld.so.conf.d/*.conf`
- **Output :** `/etc/ld.so.cache` (cache binaire)

**Pourquoi les autres sont fausses :**
- B) `ldd -u` : Affiche unused dependencies d'un binaire
- C) `updatelibs` : N'existe pas
- D) `libcache --refresh` : N'existe pas

---

### Question 23 : **Réponse B** - `/etc/ld.so.conf`

**Explication :**
`/etc/ld.so.conf` configure les chemins de recherche des bibliothèques partagées.

**Structure typique :**
```bash
$ cat /etc/ld.so.conf
include /etc/ld.so.conf.d/*.conf
```

**Fichiers inclus (/etc/ld.so.conf.d/) :**
```bash
$ ls /etc/ld.so.conf.d/
libc.conf
x86_64-linux-gnu.conf
fakeroot-x86_64-linux-gnu.conf
```

**Exemple de contenu :**
```bash
$ cat /etc/ld.so.conf.d/x86_64-linux-gnu.conf
# Multiarch support
/usr/local/lib/x86_64-linux-gnu
/lib/x86_64-linux-gnu
/usr/lib/x86_64-linux-gnu
```

**Ajouter chemin personnalisé :**
```bash
# Créer fichier config
echo "/opt/myapp/lib" | sudo tee /etc/ld.so.conf.d/myapp.conf

# Mettre à jour cache
sudo ldconfig

# Vérifier
ldconfig -p | grep myapp
```

**Chemins standard (sans config) :**
- `/lib`
- `/usr/lib`
- `/lib64` (systèmes 64-bit)
- `/usr/lib64`

**Chemins additionnels (via /etc/ld.so.conf) :**
- `/usr/local/lib`
- `/opt/*/lib`
- Chemins custom

**Pourquoi les autres sont fausses :**
- A) `/etc/libraries.conf` : N'existe pas
- C) `/etc/lib.conf` : N'existe pas
- D) `/etc/ldconfig.conf` : N'existe pas

**Conseil :** Préférer `/etc/ld.so.conf.d/` pour organisation (un fichier par application).

---

### Question 24 : **Réponse B** - `LD_LIBRARY_PATH`

**Explication :**
`LD_LIBRARY_PATH` est une variable d'environnement qui ajoute temporairement des chemins de bibliothèques.

**Usage :**
```bash
# Définir temporairement
export LD_LIBRARY_PATH=/opt/myapp/lib:$LD_LIBRARY_PATH

# Lancer application avec chemins custom
LD_LIBRARY_PATH=/custom/lib:/other/lib ./myapp

# Vérifier
echo $LD_LIBRARY_PATH

# Permanent (utilisateur)
echo 'export LD_LIBRARY_PATH=/opt/myapp/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

**Ordre de recherche bibliothèques :**
```
1. RPATH/RUNPATH (compilé dans binaire)
2. LD_LIBRARY_PATH (variable environnement)
3. /etc/ld.so.cache (cache ldconfig)
4. /lib, /usr/lib (chemins par défaut)
```

**⚠️ ATTENTION - Problèmes LD_LIBRARY_PATH :**
- Peut causer conflits de versions
- Affecte TOUS les programmes lancés
- Peut casser système si mal utilisé
- Difficile à déboguer

**Préférer ldconfig pour configuration système :**
```bash
# MIEUX (permanent, propre)
echo "/opt/myapp/lib" | sudo tee /etc/ld.so.conf.d/myapp.conf
sudo ldconfig

# AU LIEU DE (temporaire, peut causer problèmes)
export LD_LIBRARY_PATH=/opt/myapp/lib
```

**Cas d'usage légitime LD_LIBRARY_PATH :**
- Test de nouvelles versions bibliothèques
- Développement (sans installer système)
- Debugging
- Applications portables

**Pourquoi les autres sont fausses :**
- A) `LIBRARY_PATH` : Utilisé lors compilation, pas runtime
- C) `LIB_PATH` : N'existe pas
- D) `SHARED_LIBS` : N'existe pas

---

### Question 25 : **Réponse C** - `.so`

**Explication :**
Les bibliothèques partagées Linux ont l'extension **`.so`** (Shared Object).

**Nomenclature bibliothèques Linux :**
```
libNOM.so.VERSION
│   │    │  │
│   │    │  └─ Numéro version (ex: 1.1.0)
│   │    └─ Extension .so
│   └─ Nom bibliothèque
└─ Préfixe "lib"

Exemples:
libssl.so.1.1          # OpenSSL version 1.1
libc.so.6              # GNU C Library version 6
libpython3.9.so.1.0    # Python 3.9
```

**Structure liens symboliques :**
```bash
$ ls -l /usr/lib/x86_64-linux-gnu/libssl*
lrwxrwxrwx libssl.so -> libssl.so.1.1
lrwxrwxrwx libssl.so.1.1 -> libssl.so.1.1.1
-rw-r--r-- libssl.so.1.1.1

# libssl.so       : Lien développement (compilation)
# libssl.so.1.1   : Lien compatibilité ABI
# libssl.so.1.1.1 : Fichier réel
```

**Comparaison multi-plateforme :**

| OS | Extension | Exemple |
|----|-----------|---------|
| **Linux** | `.so` | `libssl.so.1.1` |
| **Windows** | `.dll` | `openssl.dll` |
| **macOS** | `.dylib` | `libssl.1.1.dylib` |

**Types bibliothèques Linux :**
- **Partagées** : `.so` (chargées runtime)
- **Statiques** : `.a` (intégrées dans binaire)

**Pourquoi les autres sont fausses :**
- A) `.dll` : Windows (Dynamic Link Library)
- B) `.lib` : Windows (bibliothèque statique ou import)
- D) `.dylib` : macOS (Dynamic Library)

**Conseil :** Retenir `.so` = **S**hared **O**bject

---

## Section 102.4 : Gestion des paquets Debian

### Question 26 : **Réponse B** - `dpkg -i package.deb`

**Explication :**
`dpkg -i` installe un fichier .deb local (sans gestion dépendances automatique).

**Installation .deb :**
```bash
# Installer paquet local
sudo dpkg -i package.deb

# Problème fréquent : dépendances manquantes
# Erreur: dpkg: dependency problems prevent configuration...

# Solution : installer dépendances avec apt
sudo apt install -f
# ou
sudo apt --fix-broken install

# Workflow complet :
wget https://example.com/package.deb
sudo dpkg -i package.deb
sudo apt install -f    # Si dépendances manquantes
```

**Options dpkg :**
```bash
# Installer
dpkg -i package.deb

# Installer multiple
dpkg -i *.deb

# Supprimer (garder config)
dpkg -r package_name

# Purger (tout supprimer)
dpkg -P package_name

# Lister contenu .deb sans installer
dpkg -c package.deb

# Infos .deb sans installer
dpkg -I package.deb
```

**Différence dpkg vs apt :**

| Aspect | dpkg | apt |
|--------|------|-----|
| Dépendances | ❌ Manuel | ✅ Automatique |
| Source | Fichier local | Dépôts |
| Usage | Bas niveau | Haut niveau |

**Pourquoi les autres sont fausses :**
- A) `apt install package.deb` : Fonctionne (modern apt) mais pas classique
- C) `deb-install` : N'existe pas
- D) `apt-get -f` : `-f` répare, n'installe pas

**Note :** apt moderne (apt install ./package.deb) gère dépendances, mais dpkg est la réponse classique.

---

### Question 27 : **Réponse B** - `apt remove package`

**Explication :**
`apt remove` supprime le paquet mais **conserve les fichiers de configuration**.

**Différence remove vs purge :**

| Commande | Binaires | Config | Usage |
|----------|----------|--------|-------|
| `apt remove` | ❌ Supprimé | ✅ Conservé | Désinstallation temporaire |
| `apt purge` | ❌ Supprimé | ❌ Supprimé | Désinstallation complète |

**Exemples :**
```bash
# Supprimer nginx (garder config)
sudo apt remove nginx
# /etc/nginx/ conservé

# Réinstaller plus tard (garde config)
sudo apt install nginx
# Configuration précédente restaurée !

# Purger nginx (tout supprimer)
sudo apt purge nginx
# /etc/nginx/ supprimé aussi

# Supprimer + purger en une commande
sudo apt remove --purge nginx
```

**Équivalents dpkg :**
```bash
# Remove (garder config)
sudo dpkg -r package

# Purge (tout supprimer)
sudo dpkg -P package
```

**Vérifier paquets avec config restante :**
```bash
# Lister paquets "rc" (removed, config restante)
dpkg -l | grep "^rc"

# Purger tous les paquets rc
sudo apt purge $(dpkg -l | grep "^rc" | awk '{print $2}')
```

**Pourquoi les autres sont fausses :**
- A) `apt purge` : Supprime AUSSI la config
- C) `dpkg -P` : Idem que purge
- D) `apt delete` : N'existe pas

**Conseil :** `remove` si hésitant, `purge` si certain.

---

### Question 28 : **Réponse D** - Toutes les réponses

**Explication :**
Ces trois commandes listent tous les paquets installés :

```bash
# Forme longue
dpkg --list

# Forme courte (identique)
dpkg -l

# Format selections
dpkg --get-selections
```

**Comparaison sorties :**

**`dpkg -l` (format tableau) :**
```bash
$ dpkg -l | head -5
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name           Version      Architecture Description
+++-==============-============-============-================================
ii  adduser        3.118ubuntu2 all          add and remove users and groups
ii  apt            2.0.2ubuntu0 amd64        commandline package manager
```

**Colonnes dpkg -l :**
- **1ère** : Desired state (i=install, r=remove, p=purge)
- **2ème** : Status (i=installed, c=config-files, n=not-installed)
- **3ème** : Erreur (vide si OK)

**États courants :**
- `ii` : Installé correctement
- `rc` : Removed, config files restants
- `un` : Unknown (jamais installé)

**`dpkg --get-selections` (format simple) :**
```bash
$ dpkg --get-selections | head -5
adduser                     install
apt                         install
apt-utils                   install
base-files                  install
base-passwd                 install
```

**Filtrer résultats :**
```bash
# Chercher paquet spécifique
dpkg -l | grep ssh

# Compter paquets installés
dpkg -l | grep "^ii" | wc -l

# Lister noms seulement
dpkg -l | awk '/^ii/{print $2}'
```

**Pourquoi D est correct :**
Les trois commandes sont valides et affichent les paquets installés (formats différents).

---

### Question 29 : **Réponse D** - A et C sont correctes

**Explication :**
`dpkg -S` et `dpkg --search` sont **identiques** (forme courte et longue).

**Rechercher quel paquet fournit un fichier :**
```bash
# Forme courte
dpkg -S /bin/ls
# coreutils: /bin/ls

# Forme longue (identique)
dpkg --search /bin/ls
# coreutils: /bin/ls

# Avec pattern
dpkg -S '*/sshd'
# openssh-server: /usr/sbin/sshd

# Fichier config
dpkg -S /etc/nginx/nginx.conf
# nginx-core: /etc/nginx/nginx.conf
```

**⚠️ LIMITATION dpkg -S :**
Ne cherche que dans paquets **installés** !

**Pour chercher dans dépôts (paquets non installés) :**
```bash
# Installer apt-file
sudo apt install apt-file
sudo apt-file update

# Chercher fichier dans tous les paquets
apt-file search /bin/programX

# Ou avec apt (commande provides inexistante directement)
```

**Workflow recherche fichier :**
```bash
# 1. Trouver chemin complet
which sshd
# /usr/sbin/sshd

# 2. Chercher paquet
dpkg -S /usr/sbin/sshd
# openssh-server: /usr/sbin/sshd

# 3. Infos sur paquet
apt show openssh-server
```

**Pourquoi D est correct :**
- A) `dpkg -S` : ✅ Valide (forme courte)
- B) `apt-file search` : ✅ Existe mais outil séparé (pas dpkg)
- C) `dpkg --search` : ✅ Valide (forme longue)

**A et C sont dpkg, B est apt-file (outil différent).**

---

### Question 30 : **Réponse B** - `apt update`

**Explication :**
`apt update` met à jour la **liste des paquets disponibles** (pas les paquets eux-mêmes).

**Différence update vs upgrade :**

| Commande | Action | Fichiers modifiés |
|----------|--------|-------------------|
| `apt update` | Met à jour **index** | `/var/lib/apt/lists/` |
| `apt upgrade` | Met à jour **paquets** | Système entier |

**Workflow typique :**
```bash
# 1. Mettre à jour liste
sudo apt update
# Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
# Get:2 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [114 kB]
# Fetched 1,234 kB in 2s (617 kB/s)

# 2. Voir paquets à mettre à jour
apt list --upgradable

# 3. Mettre à jour paquets
sudo apt upgrade
```

**Que fait apt update exactement :**
1. Lit `/etc/apt/sources.list`
2. Télécharge index depuis dépôts (fichiers `Packages.gz`)
3. Stocke dans `/var/lib/apt/lists/`
4. Reconstruit cache local

**Fréquence recommandée :**
```bash
# Serveurs : quotidien
sudo apt update && sudo apt upgrade -y

# Desktop : hebdomadaire
sudo apt update
sudo apt upgrade

# Combiné (update + upgrade)
sudo apt update && sudo apt upgrade
```

**Pourquoi les autres sont fausses :**
- A) `apt upgrade` : Met à jour paquets (pas liste)
- C) `apt refresh` : N'existe pas
- D) `apt fetch` : N'existe pas

**Analogie :** `apt update` = "Consulter catalogue magasin", `apt upgrade` = "Acheter nouveaux produits"

---

### Question 31 : **Réponse B** - `/etc/apt/sources.list`

**Explication :**
`/etc/apt/sources.list` est le fichier principal de configuration des sources de paquets.

**Format du fichier :**
```
deb [options] URI distribution composants
```

**Exemple /etc/apt/sources.list (Ubuntu 22.04) :**
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

**Champs :**
- **deb** : Paquets binaires (.deb)
- **deb-src** : Paquets sources (code source)
- **URI** : URL du dépôt
- **Distribution** : jammy, focal, bullseye, etc.
- **Composants** : main, restricted, universe, multiverse

**Composants Ubuntu :**
- **main** : Supporté officiellement, open-source
- **restricted** : Supporté, propriétaire (drivers)
- **universe** : Communauté, open-source
- **multiverse** : Non supporté, propriétaire

**Fichiers additionnels :**
```bash
/etc/apt/sources.list.d/
├── custom-ppa.list
├── docker.list
└── google-chrome.list
```

**Exemple ajout dépôt :**
```bash
# Ajouter ligne dans sources.list
echo "deb http://deb.debian.org/debian bullseye main" | sudo tee -a /etc/apt/sources.list

# Ou créer fichier séparé (MIEUX)
echo "deb http://repo.example.com/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/custom.list

# Mettre à jour
sudo apt update
```

**Pourquoi les autres sont fausses :**
- A) `/etc/apt/sources.conf` : Nom incorrect
- C) `/etc/sources.list` : Mauvais emplacement
- D) `/etc/apt.conf` : Fichier config apt (pas sources)

---

### Question 32 : **Réponse D** - A et C sont correctes

**Explication :**
`apt search` et `apt-cache search` recherchent des paquets (identique fonctionnalité).

**Commandes équivalentes :**
```bash
# Moderne (apt)
apt search nginx

# Classique (apt-cache)
apt-cache search nginx

# Résultats identiques !
```

**Exemples recherche :**
```bash
# Recherche simple
apt search web server

# Recherche exacte (nom paquet)
apt search ^nginx$

# Recherche avec regex
apt search 'python3-.*sql'

# Résultats détaillés
apt search --names-only nginx
```

**Différence apt vs apt-cache :**

| Commande | Outil | Privilèges | Usage |
|----------|-------|------------|-------|
| `apt search` | apt | Non-root OK | Moderne, recommandé |
| `apt-cache search` | apt-cache | Non-root OK | Classique, scripts |

**Autres commandes recherche :**
```bash
# Chercher dans noms seulement
apt-cache search --names-only nginx

# Chercher dans descriptions
apt-cache search "web server"

# Compter résultats
apt-cache search nginx | wc -l
```

**Filtrer résultats :**
```bash
# Avec grep
apt search python | grep -i flask

# Format personnalisé
apt-cache search --names-only python3 | cut -d' ' -f1
```

**Pourquoi D est correct :**
- A) `apt search` : ✅ Moderne, recommandé
- B) `apt find` : ❌ N'existe pas
- C) `apt-cache search` : ✅ Classique, fonctionne toujours

**A et C sont valides !**

---

### Question 33 : **Réponse D** - B et C sont correctes

**Explication :**
`apt show` et `apt-cache show` affichent des informations détaillées sur un paquet (identique).

**Commandes équivalentes :**
```bash
# Moderne
apt show nginx

# Classique
apt-cache show nginx

# Résultats identiques !
```

**Informations affichées :**
```bash
$ apt show nginx
Package: nginx
Version: 1.18.0-6ubuntu14.3
Priority: optional
Section: web
Maintainer: Ubuntu Developers
Installed-Size: 95.2 kB
Depends: nginx-core | nginx-full | nginx-light | nginx-extras
Homepage: https://nginx.org
Description: small, powerful, scalable web/proxy server
 Nginx ("engine X") is a high-performance web and reverse proxy server
 ...
```

**Champs importants :**
- **Package** : Nom
- **Version** : Version disponible
- **Depends** : Dépendances
- **Description** : Description détaillée
- **Homepage** : Site web
- **Installed-Size** : Taille installé

**Autres commandes info :**
```bash
# Politique versions (installé vs disponible)
apt-cache policy nginx

# Dépendances
apt-cache depends nginx

# Reverse dependencies (qui dépend de X)
apt-cache rdepends nginx

# Stats globales
apt-cache stats
```

**Différence avec dpkg :**
```bash
# apt show : Info depuis DÉPÔTS (installé ou non)
apt show nginx

# dpkg -s : Info paquets INSTALLÉS seulement
dpkg -s nginx
```

**Pourquoi D est correct :**
- A) `apt info` : ❌ N'existe pas
- B) `apt show` : ✅ Moderne, recommandé
- C) `apt-cache show` : ✅ Classique, fonctionne

**B et C sont valides !**

---

### Question 34 : **Réponse C** - `apt autoremove`

**Explication :**
`apt autoremove` supprime les paquets installés comme dépendances mais devenus inutiles.

**Scénario typique :**
```bash
# 1. Installer application (avec dépendances)
sudo apt install application-x
# Installe: application-x + lib1 + lib2 + lib3

# 2. Supprimer application
sudo apt remove application-x
# Supprime application-x
# lib1, lib2, lib3 restent installées (orphelines)

# 3. Supprimer dépendances inutiles
sudo apt autoremove
# Removing lib1 lib2 lib3...
```

**Différence avec autres commandes :**

| Commande | Action |
|----------|--------|
| `apt clean` | Supprime paquets .deb du cache (`/var/cache/apt/archives/`) |
| `apt autoclean` | Supprime .deb obsolètes du cache |
| `apt autoremove` | Supprime paquets devenus inutiles |

**Exemples :**
```bash
# Supprimer dépendances inutiles
sudo apt autoremove

# Avec purge (supprimer config aussi)
sudo apt autoremove --purge

# Simuler (voir ce qui serait supprimé)
apt autoremove --dry-run

# Combiné avec upgrade
sudo apt update && sudo apt upgrade && sudo apt autoremove
```

**Vérifier paquets inutiles avant suppression :**
```bash
# Lister paquets auto-installés non utilisés
apt-mark showauto | sort
```

**Sécurité :**
```bash
# Marquer paquet comme installé manuellement (protéger)
sudo apt-mark manual package_name

# Marquer comme auto (autoriser autoremove)
sudo apt-mark auto package_name
```

**Pourquoi les autres sont fausses :**
- A) `apt clean` : Nettoie cache .deb
- B) `apt autoclean` : Nettoie cache .deb obsolètes
- D) `apt purge-unused` : N'existe pas

---

### Question 35 : **Réponses A, C, D, E** - main, restricted, universe, multiverse

**Explication :**
Les composants d'un dépôt **Ubuntu** sont :

**main** - Logiciels libres, supportés officiellement
- Support complet Ubuntu (5 ans LTS)
- Open-source, DFSG-compliant
- Exemples : bash, apache2, mysql

**restricted** - Logiciels propriétaires, supportés
- Drivers propriétaires couramment utilisés
- Support officiel mais licence propriétaire
- Exemples : drivers NVIDIA, firmware wifi

**universe** - Logiciels libres, communauté
- Open-source mais support communauté
- Pas de garanties de sécurité officielles
- Milliers de paquets additionnels

**multiverse** - Logiciels propriétaires, communauté
- Licence propriétaire, pas de support
- Codecs, firmwares, logiciels commerciaux
- Exemples : codecs multimédia, flashplugin

**Comparaison :**

| Composant | Licence | Support | Exemples |
|-----------|---------|---------|----------|
| **main** | Libre | ✅ Officiel | bash, gcc, python |
| **restricted** | Propriétaire | ✅ Officiel | nvidia-driver |
| **universe** | Libre | 👥 Communauté | redis, mongodb |
| **multiverse** | Propriétaire | 👥 Communauté | rar, steam |

**Activation dans sources.list :**
```bash
deb http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
```

**Composants Debian (différent) :**
- **main** : Logiciels libres DFSG
- **contrib** : Libres mais dépendent de non-free
- **non-free** : Propriétaires

**Pourquoi les autres sont fausses :**
- B) `core` : N'existe pas (Ubuntu)
- F) `contrib` : Debian, pas Ubuntu

**Note :** Ubuntu a 4 composants, Debian en a 3 (différents).

---

## Section 102.5 : Gestion des paquets RPM et YUM

### Question 36 : **Réponse B** - `rpm -ivh package.rpm`

**Explication :**
`rpm -ivh` installe un paquet .rpm avec barre de progression.

**Options rpm :**
- **`-i`** : Install
- **`-v`** : Verbose (affiche détails)
- **`-h`** : Hash marks (barre progression `#####`)

**Exemples installation :**
```bash
# Installer avec progression
sudo rpm -ivh package.rpm
Preparing...                ########################################### [100%]
   1:package                ########################################### [100%]

# Installer sans progression
sudo rpm -i package.rpm

# Mettre à jour (upgrade)
sudo rpm -Uvh package.rpm
# -U = Upgrade (ou install si absent)

# Freshen (upgrade seulement si déjà installé)
sudo rpm -Fvh package.rpm
# -F = Freshen
```

**Autres options installation :**
```bash
# Forcer installation (ignorer conflits)
sudo rpm -ivh --force package.rpm

# Ignorer dépendances (DANGEREUX)
sudo rpm -ivh --nodeps package.rpm

# Test (simulation)
sudo rpm -ivh --test package.rpm

# Verbose maximum
sudo rpm -ivvh package.rpm
```

**Différence -i vs -U :**

| Option | Paquet absent | Paquet présent |
|--------|---------------|----------------|
| `-i` | Installe | Erreur |
| `-U` | Installe | Met à jour |

**Pourquoi les autres sont fausses :**
- A) `rpm -i` : Correct mais sans progression (`-h`)
- C) `rpm --install` : Forme longue de `-i` (sans `-vh`)
- D) `rpm -Uvh` : **Aussi correct** (upgrade), mais question demande "install"

**Note :** `-Uvh` est souvent préféré car fonctionne dans tous les cas.

---

### Question 37 : **Réponse B** - `rpm -qa`

**Explication :**
`rpm -qa` (Query All) liste tous les paquets installés.

**Options query rpm :**
```bash
# Lister tous les paquets
rpm -qa

# Avec filtre
rpm -qa | grep ssh

# Compter paquets
rpm -qa | wc -l

# Tri alphabétique
rpm -qa | sort

# Format personnalisé
rpm -qa --qf '%{NAME}-%{VERSION}\n'
```

**Autres queries :**
```bash
# Infos paquet installé
rpm -qi package_name

# Fichiers d'un paquet
rpm -ql package_name

# Quel paquet fournit fichier
rpm -qf /usr/sbin/sshd

# Documentation paquet
rpm -qd package_name

# Fichiers config paquet
rpm -qc package_name

# Scripts installation
rpm -q --scripts package_name

# Dépendances
rpm -qR package_name

# Qui dépend de ce paquet
rpm -q --whatrequires package_name
```

**Query sur fichier .rpm (non installé) :**
```bash
# Ajouter 'p' pour package file
rpm -qpi package.rpm      # Infos
rpm -qpl package.rpm      # Fichiers
rpm -qpR package.rpm      # Dépendances
```

**Formats de sortie :**
```bash
# Format par défaut
rpm -qa

# Format personnalisé
rpm -qa --qf '%{NAME} %{VERSION} %{ARCH}\n'

# Équivalent JSON (avec jq)
rpm -qa --qf '%{NAME}|%{VERSION}\n' | jq -R -s 'split("\n")'
```

**Pourquoi les autres sont fausses :**
- A) `rpm -l` : Liste fichiers (nécessite nom paquet)
- C) `rpm --list` : Idem que `-l`
- D) `rpm --all` : N'existe pas (c'est `-qa` = query all)

---

### Question 38 : **Réponse A** - `rpm -qf /usr/sbin/httpd`

**Explication :**
`rpm -qf` (Query File) trouve quel paquet fournit un fichier installé.

**Usage :**
```bash
# Trouver paquet d'un fichier
rpm -qf /usr/sbin/httpd
# httpd-2.4.37-30.module_el8.3.0+462+ba287492.x86_64

# Autre exemple
rpm -qf /bin/ls
# coreutils-8.30-8.el8.x86_64

# Config file
rpm -qf /etc/ssh/sshd_config
# openssh-server-8.0p1-4.el8.x86_64
```

**⚠️ LIMITATION :** Cherche seulement fichiers **installés** !

**Pour fichiers dans paquets non installés :**
```bash
# Utiliser yum/dnf provides
yum provides /usr/bin/docker
# docker-ce-20.10.7-3.el8.x86_64 : The open-source application container engine

dnf provides */sshd
# openssh-server-8.0p1-4.el8.x86_64 : SSH server daemon
```

**Workflow investigation :**
```bash
# 1. Trouver chemin complet
which httpd
# /usr/sbin/httpd

# 2. Trouver paquet
rpm -qf /usr/sbin/httpd
# httpd-2.4.37-30.x86_64

# 3. Infos paquet
rpm -qi httpd

# 4. Tous les fichiers du paquet
rpm -ql httpd
```

**Pourquoi les autres sont fausses :**
- B) `rpm --whatprovides` : Fonctionne mais pour **capacités** (ex: `perl(CGI)`), pas fichiers
- C) `rpm -S` : N'existe pas
- D) `yum provides` : ✅ Fonctionne mais c'est YUM, pas RPM

**Conseil :** `rpm -qf` pour fichiers installés, `yum provides` pour recherche large.

---

### Question 39 : **Réponse B** - `/etc/yum.repos.d/`

**Explication :**
Les fichiers de configuration des dépôts yum/dnf sont dans **`/etc/yum.repos.d/`**.

**Structure :**
```bash
ls /etc/yum.repos.d/
CentOS-Base.repo
epel.repo
docker-ce.repo
custom.repo
```

**Format fichier .repo :**
```bash
# /etc/yum.repos.d/custom.repo
[custom-repo]
name=Custom Repository
baseurl=http://repo.example.com/centos/$releasever/$basearch/
enabled=1
gpgcheck=1
gpgkey=http://repo.example.com/RPM-GPG-KEY-custom
```

**Champs importants :**
- **[repo-id]** : Identifiant unique
- **name** : Nom descriptif
- **baseurl** : URL du dépôt
- **mirrorlist** : URL liste miroirs (alternatif)
- **enabled** : 1=activé, 0=désactivé
- **gpgcheck** : Vérifier signatures (1=oui)
- **gpgkey** : URL clé GPG

**Variables automatiques :**
- **$releasever** : Version OS (7, 8, 9)
- **$basearch** : Architecture (x86_64, i386)

**Gérer dépôts :**
```bash
# Lister dépôts actifs
yum repolist

# Lister tous (actifs + désactivés)
yum repolist all

# Activer dépôt
sudo yum-config-manager --enable repo-id

# Désactiver dépôt
sudo yum-config-manager --disable repo-id

# Ajouter dépôt
sudo yum-config-manager --add-repo https://example.com/repo.repo

# Installer depuis dépôt spécifique
sudo yum --enablerepo=epel install package
```

**Fichier config principal :**
```bash
/etc/yum.conf        # Configuration globale yum
/etc/dnf/dnf.conf    # Configuration globale dnf
```

**Pourquoi les autres sont fausses :**
- A) `/etc/yum.conf.d/` : N'existe pas
- C) `/etc/dnf/repos/` : N'existe pas
- D) `/etc/repositories/` : N'existe pas

**Conseil :** Un fichier .repo par dépôt pour organisation.

---

### Question 40 : **Réponse B** - `dnf`

**Explication :**
**DNF** (Dandified YUM) est le successeur de yum sur RHEL 8+, CentOS 8+, et Fedora 22+.

**Évolution :**
```
yum (RHEL 7, CentOS 7)
  ↓
dnf (RHEL 8+, CentOS 8+, Fedora 22+)
```

**Compatibilité :**
```bash
# Sur RHEL 8+, "yum" est un lien vers "dnf"
ls -l /usr/bin/yum
lrwxrwxrwx /usr/bin/yum -> dnf-3

# Commandes identiques:
yum install package
dnf install package
```

**Améliorations DNF vs YUM :**
- ✅ **Performance** : Résolution dépendances plus rapide
- ✅ **API** : Python 3 (yum = Python 2)
- ✅ **Mémoire** : Consommation réduite
- ✅ **Modules** : Support AppStream (RHEL 8)
- ✅ **Fiabilité** : Meilleure gestion conflits

**Commandes identiques :**
```bash
# Syntaxe 100% compatible
dnf install package     = yum install package
dnf update              = yum update
dnf remove package      = yum remove package
dnf search keyword      = yum search keyword
```

**Nouvelles fonctionnalités DNF :**
```bash
# Modules (AppStream)
dnf module list
dnf module install nodejs:14/default

# Historique amélioré
dnf history userinstalled

# Downgrade
dnf downgrade package

# Repoquery intégré
dnf repoquery --whatprovides /bin/bash
```

**Par distribution :**

| Distribution | Version | Gestionnaire |
|--------------|---------|--------------|
| RHEL 7 / CentOS 7 | - | yum |
| **RHEL 8+ / CentOS 8+ / Rocky 8+ / Alma 8+** | - | **dnf** |
| **Fedora 22+** | - | **dnf** |

**Pourquoi les autres sont fausses :**
- A) `yum2` : N'existe pas
- C) `zypper` : Gestionnaire openSUSE (pas successeur yum)
- D) `pacman` : Gestionnaire Arch Linux

**Conseil :** Sur RHEL 8+, utiliser `dnf` (même si `yum` fonctionne).

---

## 📊 Tableau de scoring

| Score | Évaluation | Action recommandée |
|-------|------------|-------------------|
| 38-40 | 🏆 Excellent | Sujet maîtrisé ! Passez au suivant |
| 33-37 | ✅ Très bien | Relire sections avec erreurs |
| 28-32 | ⚠️ Bien | Revoir notes + refaire QCM |
| 20-27 | 📚 Moyen | Retravailler le sujet |
| < 20 | ❌ Insuffisant | Reprendre depuis le début |

---

## 🎯 Prochaines étapes

1. **Notez votre score :** _____ / 40
2. **Identifiez vos points faibles :**
   - [ ] Section 102.1 (partitionnement, LVM, RAID)
   - [ ] Section 102.2 (GRUB)
   - [ ] Section 102.3 (bibliothèques)
   - [ ] Section 102.4 (paquets Debian)
   - [ ] Section 102.5 (paquets RPM/YUM)
3. **Relisez les notes** pour vos sections faibles
4. **Pratiquez en labs** les commandes mal maîtrisées
5. **Refaites le QCM** dans 2-3 jours (objectif 100%)

---

**🎓 Conseil final :**  
Le Sujet 102 est **essentiel** (25% de l'examen). Maîtrisez particulièrement :
- LVM (création, extension)
- GRUB 2 (configuration, dépannage)
- apt/dpkg (Debian)
- yum/rpm (Red Hat)

**Prêt pour le Sujet 103 ?** → [Notes-Revision-Sujet-103.md](../Notes/Notes-Revision-Sujet-103.md)

*Le Sujet 103 représente 40% de l'examen (16 points) - le plus important !*
