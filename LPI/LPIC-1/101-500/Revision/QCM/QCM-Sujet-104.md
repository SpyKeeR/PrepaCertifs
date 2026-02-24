# 🎯 QCM - Sujet 104 : Périphériques, Systèmes de Fichiers Linux, FHS

> **Poids du sujet :** 6 points (~15% de l'examen)  
> **Questions :** 25 au total  
> **Objectif :** 19/25 minimum (75%) - Viser 21+ (85%)  
> **Temps estimé :** 25-30 minutes

---

## 📋 Instructions

- Lisez attentivement chaque question
- Une ou plusieurs réponses peuvent être correctes (indiqué)
- Notez vos réponses et vérifiez avec les explications
- Calculez votre score final

---

## 📝 Questions

#### Question 1
Quel outil utiliser pour créer une table de partitions **GPT** ?

- [ ] A) `fdisk`  
- [ ] B) `gdisk`  
- [ ] C) `parted`  
- [ ] D) Les deux B et C

---

#### Question 2
Comment créer un système de fichiers **ext4** sur `/dev/sdb1` ?

- [ ] A) `mkfs /dev/sdb1`  
- [ ] B) `mkfs.ext4 /dev/sdb1`  
- [ ] C) `mkfs -t ext4 /dev/sdb1`  
- [ ] D) Les deux B et C

---

#### Question 3
Quelle commande affiche l'**UUID** d'une partition ?

- [ ] A) `lsblk`  
- [ ] B) `blkid`  
- [ ] C) `fdisk -l`  
- [ ] D) `df -h`

---

#### Question 4
Comment créer et activer une partition **swap** ?

- [ ] A) `mkswap /dev/sdb2` puis `swapon /dev/sdb2`  
- [ ] B) `mkfs.swap /dev/sdb2` puis `mount /dev/sdb2`  
- [ ] C) `mkswap -L Swap /dev/sdb2` puis `swapon /dev/sdb2`  
- [ ] D) Les deux A et C

---

#### Question 5
Quelle est la **différence principale** entre ext4 et XFS ?

- [ ] A) ext4 est plus récent  
- [ ] B) XFS est optimisé pour gros fichiers et hautes performances  
- [ ] C) XFS ne supporte pas le journaling  
- [ ] D) ext4 ne peut pas être réduit

---

#### Question 6
Quelle commande **vérifier et réparer** un filesystem ext4 ?

- [ ] A) `fsck /dev/sdb1`  
- [ ] B) `e2fsck /dev/sdb1`  
- [ ] C) `fsck.ext4 /dev/sdb1`  
- [ ] D) Toutes les réponses

---

#### Question 7
Comment afficher les **détails** d'un filesystem ext4 (superblock, inodes, etc.) ?

- [ ] A) `dumpe2fs /dev/sdb1`  
- [ ] B) `tune2fs -l /dev/sdb1`  
- [ ] C) `blkid /dev/sdb1`  
- [ ] D) Les deux A et B

---

#### Question 8
Comment vérifier un filesystem **XFS** ?

- [ ] A) `fsck /dev/sdc1`  
- [ ] B) `xfs_repair /dev/sdc1`  
- [ ] C) `xfs_check /dev/sdc1`  
- [ ] D) `e2fsck /dev/sdc1`

---

#### Question 9
Quelle commande affiche le nombre d'**inodes libres** ?

- [ ] A) `df -i`  
- [ ] B) `df -h`  
- [ ] C) `tune2fs -l /dev/sdb1 | grep -i inode`  
- [ ] D) Les deux A et C

---

#### Question 10
Comment monter `/dev/sdb1` sur `/mnt/data` en **lecture seule** ?

- [ ] A) `mount /dev/sdb1 /mnt/data`  
- [ ] B) `mount -o ro /dev/sdb1 /mnt/data`  
- [ ] C) `mount -o readonly /dev/sdb1 /mnt/data`  
- [ ] D) `mount -r /dev/sdb1 /mnt/data`

---

#### Question 11
Quel fichier configure les montages **automatiques** au démarrage ?

- [ ] A) `/etc/mtab`  
- [ ] B) `/etc/fstab`  
- [ ] C) `/proc/mounts`  
- [ ] D) `/etc/auto.mount`

---

#### Question 12
Dans `/etc/fstab`, quelle option permet à un **utilisateur normal** de monter un device ?

- [ ] A) `auto`  
- [ ] B) `user`  
- [ ] C) `users`  
- [ ] D) `owner`

---

#### Question 13
Comment démonter **proprement** un filesystem occupé ?

- [ ] A) `umount -f /mnt/data`  
- [ ] B) Identifier processus avec `lsof /mnt/data` puis les arrêter  
- [ ] C) `umount -l /mnt/data`  
- [ ] D) Redémarrer système

---

#### Question 14
Quelle option `/etc/fstab` **désactive MAJ access time** (performance) ?

- [ ] A) `noatime`  
- [ ] B) `nodiratime`  
- [ ] C) `relatime`  
- [ ] D) Les deux A et C (compromis)

---

#### Question 15
Comment remonter `/mnt/data` en **read-write** sans démonter ?

- [ ] A) `mount -o rw /mnt/data`  
- [ ] B) `mount -o remount,rw /mnt/data`  
- [ ] C) `umount /mnt/data && mount -o rw /dev/sdb1 /mnt/data`  
- [ ] D) Impossible, doit démonter

---

#### Question 16
Que signifie `chmod 755 script.sh` ?

- [ ] A) rwxr-xr-x  
- [ ] B) rwxrwxrwx  
- [ ] C) rw-r--r--  
- [ ] D) rwx------

---

#### Question 17
Comment donner **seulement** le droit d'exécution au propriétaire ?

- [ ] A) `chmod +x file`  
- [ ] B) `chmod u+x file`  
- [ ] C) `chmod 744 file`  
- [ ] D) Les deux B et C

---

#### Question 18
Quelle commande change le **propriétaire** ET le **groupe** d'un fichier ?

- [ ] A) `chown user file`  
- [ ] B) `chgrp group file`  
- [ ] C) `chown user:group file`  
- [ ] D) `chmod user:group file`

---

#### Question 19
Qu'est-ce que le **SUID bit** et comment l'activer ?

- [ ] A) Bit permettant exécution avec permissions du propriétaire  
- [ ] B) `chmod u+s file` ou `chmod 4755 file`  
- [ ] C) Exemple : `/usr/bin/passwd` (user peut changer MDP)  
- [ ] D) Toutes les réponses

---

#### Question 20
Quelle est la fonction du **sticky bit** sur `/tmp` ?

- [ ] A) Empêcher exécution fichiers  
- [ ] B) Seulement propriétaire peut supprimer ses fichiers  
- [ ] C) Tous peuvent créer fichiers mais pas supprimer ceux des autres  
- [ ] D) Les deux B et C

---

#### Question 21
Quelle commande crée un **lien symbolique** ?

- [ ] A) `ln file link`  
- [ ] B) `ln -s /path/to/file link`  
- [ ] C) `link file link`  
- [ ] D) `symlink file link`

---

#### Question 22
Quelle est la **différence principale** entre symlink et hardlink ?

- [ ] A) Symlink peut traverser filesystems, hardlink non  
- [ ] B) Si cible supprimée : symlink cassé, hardlink reste valide  
- [ ] C) Hardlink a même inode, symlink différent  
- [ ] D) Toutes les réponses

---

#### Question 23
Comment voir la **cible** d'un lien symbolique ?

- [ ] A) `ls -l link`  
- [ ] B) `readlink link`  
- [ ] C) `file link`  
- [ ] D) Toutes les réponses

---

#### Question 24
Dans le FHS, quel répertoire contient les **configurations système** ?

- [ ] A) `/usr`  
- [ ] B) `/etc`  
- [ ] C) `/var`  
- [ ] D) `/opt`

---

#### Question 25
Quelle commande trouve tous les fichiers **modifiés dans les 7 derniers jours** ?

- [ ] A) `find / -mtime -7`  
- [ ] B) `find / -mtime +7`  
- [ ] C) `find / -atime -7`  
- [ ] D) `locate -m 7`

---

#### Question 26
Comment trouver tous les fichiers **SUID** (sécurité) ?

- [ ] A) `find / -perm 4000`  
- [ ] B) `find / -perm -4000`  
- [ ] C) `find / -perm -u+s`  
- [ ] D) Les deux B et C

---

#### Question 27
Quelle commande trouve fichiers **plus gros que 100MB** ?

- [ ] A) `find / -size 100M`  
- [ ] B) `find / -size +100M`  
- [ ] C) `find / -size -100M`  
- [ ] D) `du -h / | grep 100M`

---

#### Question 28
Quelle commande trouve fichiers **vides** ?

- [ ] A) `find / -size 0`  
- [ ] B) `find / -empty`  
- [ ] C) `find / -type f -size 0`  
- [ ] D) Toutes les réponses

---

#### Question 29
Comment chercher fichiers **appartenant à un utilisateur spécifique** ?

- [ ] A) `find / -user username`  
- [ ] B) `find / -uid 1000`  
- [ ] C) `find / -owner username`  
- [ ] D) Les deux A et B

---

#### Question 30
Dans FHS, où sont stockés les **logs système** ?

- [ ] A) `/var/log`  
- [ ] B) `/var/spool`  
- [ ] C) `/tmp`  
- [ ] D) `/usr/log`

---


---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

### Question 1
**Réponse correcte : D**

**B) gdisk** : Outil spécialisé GPT (interface similaire à fdisk).
```bash
gdisk /dev/sdb
n, Enter, Enter, +50G, 8300, w
```

**C) parted** : Outil universel supportant MBR et GPT.
```bash
parted /dev/sdb mklabel gpt
parted /dev/sdb mkpart primary ext4 0% 50GB
```

**Pourquoi A est incorrecte :** `fdisk` est limité au MBR (max 2TB, 4 partitions primaires). Pour GPT moderne, utiliser gdisk ou parted.

**À retenir :** GPT = gdisk ou parted | MBR = fdisk

---

### Question 2
**Réponse correcte : D**

Les deux syntaxes sont équivalentes :
```bash
mkfs.ext4 /dev/sdb1           # Direct
mkfs -t ext4 /dev/sdb1        # Spécifier type
mkfs.ext4 -L DataDisk /dev/sdb1  # Avec label
```

**Pourquoi A est insuffisante :** `mkfs` seul nécessite l'option `-t` pour spécifier le type de filesystem. Sans type, erreur ou comportement imprévisible.

**Commandes associées :**
- `mkfs.xfs` : Filesystem XFS
- `mkfs.vfat` : FAT32
- `mkswap` : Partition swap

---

### Question 3
**Réponse correcte : B**

```bash
blkid /dev/sdb1
# /dev/sdb1: UUID="a1b2c3d4..." TYPE="ext4" PARTUUID="..."

# UUID seulement
blkid -s UUID -o value /dev/sdb1

# Tous les devices
blkid
```

**Alternatives partielles :**
- **A) `lsblk -f`** affiche UUID mais moins détaillé
- **C) `fdisk -l`** affiche partitions mais PAS les UUID
- **D) `df -h`** affiche utilisation, pas UUID

**Pourquoi UUID important :** Stable même si device change (/dev/sdb → /dev/sdc). **Obligatoire dans /etc/fstab** pour l'examen !

---

### Question 4
**Réponse correcte : D**

**Procédure swap :**
```bash
# 1. Créer swap
mkswap /dev/sdb2
mkswap -L SwapPartition /dev/sdb2    # Avec label

# 2. Activer
swapon /dev/sdb2

# Vérifier
swapon --show
free -h

# Désactiver
swapoff /dev/sdb2

# Permanent: ajouter à /etc/fstab
/dev/sdb2  none  swap  sw  0  0
```

**Pourquoi B est fausse :** Pas de `mkfs.swap` (n'existe pas). Swap utilise `mkswap` et `swapon` (pas mount).

---

### Question 5
**Réponse correcte : B**

**XFS :**
- Optimisé gros fichiers et I/O intensif
- Utilisé par défaut RHEL/CentOS
- Très performant, allocation retardée
- **Limite** : Difficile de réduire taille

**ext4 :**
- Standard Linux, mature et stable
- Facile à redimensionner (agrandir/réduire)
- Bon compromis performance/compatibilité

**Pourquoi autres incorrectes :**
- **A** : ext4 est plus ancien et mature
- **C** : XFS a un excellent journaling
- **D** : ext4 peut être réduit avec `resize2fs`

**Commandes :**
```bash
mkfs.xfs /dev/sdc1
mkfs.ext4 /dev/sdb1
```

---

### Question 6
**Réponse correcte : D**

Trois syntaxes équivalentes pour ext4 :
```bash
fsck /dev/sdb1           # Détecte type auto
e2fsck /dev/sdb1         # Spécifique ext2/3/4
fsck.ext4 /dev/sdb1      # Explicite ext4

# Options importantes
fsck -y /dev/sdb1        # Auto-réparer
fsck -n /dev/sdb1        # Dry-run (pas de modifs)
fsck -f /dev/sdb1        # Force check
```

**⚠️ CRITIQUE :** **Toujours démonter avant fsck** sinon risque corruption !
```bash
umount /dev/sdb1
fsck /dev/sdb1
```

**Codes retour :** 0=OK, 1=corrigé, 2=reboot needed, 4=erreurs restantes

---

### Question 7
**Réponse correcte : D**

**A) dumpe2fs** : Affiche TOUT (superblock, groupes, blocks)
```bash
dumpe2fs /dev/sdb1
dumpe2fs -h /dev/sdb1    # Seulement superblock
```

**B) tune2fs -l** : Affiche infos configurables
```bash
tune2fs -l /dev/sdb1
# Affiche: UUID, label, block size, inode count, mount count, check interval, etc.
```

**C) blkid** : Seulement UUID/TYPE (moins détaillé)

**Commandes tune2fs utiles :**
```bash
tune2fs -L NewLabel /dev/sdb1        # Changer label
tune2fs -c 30 /dev/sdb1              # Check tous les 30 montages
tune2fs -i 2w /dev/sdb1              # Check tous les 2 weeks
tune2fs -c 0 -i 0 /dev/sdb1          # Désactiver checks auto
tune2fs -m 2 /dev/sdb1               # 2% réservé root (défaut 5%)
```

---

### Question 8
**Réponse correcte : B**

```bash
# XFS utilise xfs_repair (pas fsck)
umount /dev/sdc1
xfs_repair /dev/sdc1

# Options
xfs_repair -n /dev/sdc1    # Dry-run (pas de modifs)
xfs_repair -v /dev/sdc1    # Verbose

# Infos XFS
xfs_info /mnt/xfs          # FS monté
xfs_admin -l /dev/sdc1     # Label
xfs_admin -u /dev/sdc1     # UUID
```

**Pourquoi autres incorrectes :**
- **A/D** : `fsck`/`e2fsck` pour ext, pas XFS
- **C** : `xfs_check` déprécié (utiliser `xfs_repair -n`)

**Note :** XFS ne peut pas être réduit (seulement agrandi avec `xfs_growfs`).

---

### Question 9
**Réponse correcte : D**

**A) df -i** : Affiche inodes pour filesystems montés
```bash
df -i
# Filesystem  Inodes  IUsed  IFree  IUse%  Mounted on
# /dev/sda1   500000  12000  488000   3%   /
```

**C) tune2fs -l** : Détails partition (montée ou non)
```bash
tune2fs -l /dev/sdb1 | grep -i inode
# Inode count: 500000
# Free inodes: 488000
```

**Pourquoi B incorrecte :** `df -h` affiche **blocks** (espace disque), pas inodes.

**Problème inodes :** Si `IUse% = 100%`, impossible créer fichiers même si espace libre !
```bash
# Créer FS avec plus d'inodes
mkfs.ext4 -N 2000000 /dev/sdb1
```

---

### Question 10
**Réponse correcte : B**

```bash
mount -o ro /dev/sdb1 /mnt/data
# ro = read-only

# Vérifier
mount | grep sdb1
# /dev/sdb1 on /mnt/data type ext4 (ro,relatime)

# Remonter en rw sans démonter
mount -o remount,rw /mnt/data
```

**Pourquoi D partiellement correcte :** `mount -r` fonctionne mais `-o ro` est la syntaxe standard pour l'examen.

**Options mount courantes :**
```bash
-o rw          # Read-write (défaut)
-o noexec      # Pas d'exécution binaires
-o nosuid      # Ignorer SUID bits
-o noatime     # Pas MAJ access time (performance)
-o sync        # Écritures synchrones
```

---

### Question 11
**Réponse correcte : B**

```bash
# /etc/fstab format:
# device  mountpoint  fstype  options  dump  pass

# Exemple
UUID=xxx  /data  ext4  defaults  0  2
/dev/sdb1  /backup  xfs  noatime  0  2
/dev/sdc1  none  swap  sw  0  0

# Champs pass (fsck order):
# 0 = skip
# 1 = root (/)
# 2 = autres (après root)
```

**Pourquoi autres incorrectes :**
- **A) /etc/mtab** : Liste montages actuels (symlink vers /proc/self/mounts)
- **C) /proc/mounts** : État actuel kernel (virtuel)
- **D** : N'existe pas

**Tester fstab :**
```bash
mount -a     # Monte tout
mount -av    # Verbose
mount /data  # Si défini dans fstab
```

---

### Question 12
**Réponse correcte : B**

```bash
# /etc/fstab avec option user
/dev/sdd1  /mnt/usb  vfat  noauto,user  0  0

# User normal peut alors:
mount /mnt/usb
umount /mnt/usb

# Sans user, seulement root peut monter
```

**Options associées :**
- `user` : User peut monter, seulement lui peut démonter
- `users` : N'importe quel user peut monter ET démonter
- `nouser` : Seulement root (défaut)
- `noauto` : Ne monte PAS avec `mount -a` (manuel)
- `owner` : Seulement propriétaire du device

**Cas d'usage :** USB, CD/DVD montables par users.

---

### Question 13
**Réponse correcte : B**

**Méthode propre :**
```bash
# 1. Identifier qui utilise
lsof /mnt/data
fuser -m /mnt/data

# 2. Arrêter processus
kill <PID>

# 3. Démonter
umount /mnt/data
```

**Pourquoi autres sont risquées :**
- **A) -f (force)** : Peut causer perte données
- **C) -l (lazy)** : Détache immédiatement mais nettoie plus tard (masque problème)
- **D** : Extrême, inutile

**Tuer automatiquement (⚠️ risqué) :**
```bash
fuser -km /mnt/data    # Kill tous processus
umount /mnt/data
```

**Identifier processus :**
```bash
lsof +D /mnt/data      # Récursif
fuser -v /mnt/data     # Verbose
```

---

### Question 14
**Réponse correcte : D**

**A) noatime** : Ne met JAMAIS à jour access time
```bash
UUID=xxx  /data  ext4  defaults,noatime  0  2
# Gain performance (moins d'écritures)
# Utile serveurs web, bases données
```

**C) relatime** : MAJ atime seulement si < mtime (défaut moderne)
```bash
UUID=xxx  /data  ext4  defaults,relatime  0  2
# Compromis performance/compatibilité
```

**B) nodiratime** : Seulement pour répertoires (fichiers normaux)

**Options autres :**
```bash
strictatime    # MAJ toujours (ancien défaut)
noatime        # Jamais MAJ (max perf)
relatime       # MAJ si modifié (défaut actuel)
nodiratime     # Pas MAJ dirs
```

**Impact :** noatime réduit écritures disque → améliore performance SSD/HDD.

---

### Question 15
**Réponse correcte : B**

```bash
# Remonter avec nouvelles options
mount -o remount,rw /mnt/data
mount -o remount,ro /mnt/data

# Vérifier
mount | grep /mnt/data

# Utile pour:
# - Passer de ro à rw
# - Modifier options (noatime, etc.)
# - Filesystem racine /
```

**Pourquoi A incorrecte :** Tente de monter (déjà monté → erreur).

**Cas d'usage :** Système démarré en single-user (/ en ro), remonter en rw :
```bash
mount -o remount,rw /
```

---

### Question 16
**Réponse correcte : A**

```bash
chmod 755 script.sh
# 7 = 4+2+1 = rwx (user)
# 5 = 4+0+1 = r-x (group)
# 5 = 4+0+1 = r-x (other)
# → rwxr-xr-x

ls -l script.sh
# -rwxr-xr-x 1 user group ... script.sh
```

**Calcul permissions :**
- r (read) = 4
- w (write) = 2
- x (execute) = 1

**Permissions courantes :**
```bash
644 = rw-r--r--  # Fichiers standard
755 = rwxr-xr-x  # Scripts exécutables
600 = rw-------  # Fichiers privés
700 = rwx------  # Scripts privés
777 = rwxrwxrwx  # Tout (⚠️ éviter)
```

---

### Question 17
**Réponse correcte : B**

```bash
chmod u+x file
# u = user (owner)
# + = ajouter
# x = execute

# Avant: rw-r--r-- (644)
# Après: rwxr--r-- (744)
```

**Pourquoi A incorrecte :** `chmod +x` ajoute x pour **TOUS** (user, group, other).

**Pourquoi C incorrecte :** `chmod 744` donne aussi `r` (lecture) à group/other, pas seulement `x` au user.

**Symboles chmod :**
```bash
u = user/owner
g = group
o = other
a = all (ugo)

+ = ajouter
- = retirer
= = set exact

chmod u+x,g-w,o-r file    # Combinaisons
chmod a+r file            # Tous
chmod u=rwx,g=rx,o=r file # Set exact
```

---

### Question 18
**Réponse correcte : C**

```bash
chown user:group file.txt
chown user.group file.txt    # Syntaxe alternative

# Exemples
chown alice:developers file.txt
chown www-data:www-data /var/www/index.html

# Récursif
chown -R user:group directory/
```

**Pourquoi autres incorrectes :**
- **A** : Change seulement user, pas group
- **B** : `chgrp` change seulement group, pas user
- **D** : `chmod` gère permissions, pas ownership

**Variantes :**
```bash
chown user file         # Seulement user
chown :group file       # Seulement group
chgrp group file        # Équivalent
chown -R user:group dir # Récursif
```

---

### Question 19
**Réponse correcte : D**

**SUID (Set User ID) :**
```bash
# Activer
chmod u+s /usr/bin/program
chmod 4755 /usr/bin/program    # 4 = SUID

# Vérifier
ls -l /usr/bin/passwd
# -rwsr-xr-x root root ... (s au lieu de x)
```

**Fonctionnement :** User lambda exécute programme avec permissions du **propriétaire** (souvent root).

**Exemple `/usr/bin/passwd` :**
- Propriétaire : root
- SUID activé
- User normal peut changer son MDP (nécessite écriture `/etc/shadow` = root)

**Bits spéciaux :**
```bash
SUID: 4000 (u+s)  # Exec comme owner
SGID: 2000 (g+s)  # Exec comme group OU héritage groupe (dirs)
Sticky: 1000 (+t) # Seulement owner peut supprimer (/tmp)

chmod 4755 file   # SUID + 755
chmod 2775 dir    # SGID + 775
chmod 1777 /tmp   # Sticky + 777
```

---

### Question 20
**Réponse correcte : D**

```bash
ls -ld /tmp
# drwxrwxrwt ... /tmp
#         └─ t = sticky bit

chmod +t /tmp
chmod 1777 /tmp    # Sticky + 777
```

**Comportement :**
- Tous peuvent créer fichiers dans `/tmp` (rwx pour tous)
- **Seulement propriétaire** peut supprimer/renommer **ses propres** fichiers
- User A ne peut pas supprimer fichier de User B

**Sans sticky :** Si `chmod 777 /tmp`, n'importe qui pourrait supprimer fichiers des autres (chaos).

**Cas d'usage :**
- `/tmp` : Partage temporaire multi-utilisateurs
- `/var/tmp` : Idem
- Répertoires partagés

**Symbole :**
- `t` si other a execute (x)
- `T` si other n'a pas execute

---

### Question 21
**Réponse correcte : B**

```bash
ln -s /path/to/file linkname
ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/

# Vérifier
ls -l linkname
# lrwxrwxrwx ... linkname -> /path/to/file

# Absolu vs relatif
ln -s /etc/config.conf link    # Absolu
ln -s ../config.conf link      # Relatif (préféré parfois)

# Force (écraser existant)
ln -sf /new/target link
```

**Pourquoi A incorrecte :** `ln file link` crée **hardlink**, pas symlink.

**Commandes utiles :**
```bash
readlink link          # Voir cible
readlink -f link       # Chemin absolu
ls -l link             # Affiche target
```

---

### Question 22
**Réponse correcte : D**

| Aspect | Symlink | Hardlink |
|--------|---------|----------|
| **Traverser FS** | ✅ Oui | ❌ Non |
| **Cible supprimée** | ❌ Cassé | ✅ Valide |
| **Inode** | Différent | Identique |
| **Dossiers** | ✅ Oui | ❌ Non |
| **Taille** | Longueur chemin | Taille fichier |

**Exemples :**
```bash
# Original
echo "data" > original.txt

# Symlink
ln -s original.txt sym.txt
ls -li sym.txt
# 67890 lrwxrwxrwx ... sym.txt -> original.txt (inode différent)

# Hardlink
ln original.txt hard.txt
ls -li hard.txt
# 12345 -rw-r--r-- 2 ... hard.txt (même inode que original, link count=2)

# Supprimer original
rm original.txt

# Symlink cassé
cat sym.txt    # Erreur

# Hardlink OK
cat hard.txt   # "data" (toujours accessible)
```

---

### Question 23
**Réponse correcte : D**

**A) ls -l** : Affiche link → target
```bash
ls -l mylink
# lrwxrwxrwx ... mylink -> /etc/config.conf
```

**B) readlink** : Affiche seulement cible
```bash
readlink mylink
# /etc/config.conf

readlink -f mylink    # Chemin absolu complet
```

**C) file** : Identifie type + cible
```bash
file mylink
# mylink: symbolic link to /etc/config.conf
```

**Vérifier lien cassé :**
```bash
# Lien cassé si cible n'existe pas
ls -l broken_link
# lrwxrwxrwx ... broken_link -> /nonexistent (rouge)

# Trouver liens cassés
find /path -type l ! -exec test -e {} \; -print
```

---

### Question 24
**Réponse correcte : B**

```bash
/etc    # Configurations système

# Exemples fichiers importants:
/etc/fstab       # Montages auto
/etc/passwd      # Users
/etc/group       # Groups
/etc/shadow      # Passwords
/etc/hosts       # Résolution locale
/etc/hostname    # Nom machine
/etc/resolv.conf # DNS
/etc/ssh/        # Config SSH
/etc/nginx/      # Config Nginx
/etc/systemd/    # Units systemd
```

**Pourquoi autres incorrectes :**
- **A) /usr** : Programmes utilisateur
- **C) /var** : Données variables (logs, cache)
- **D) /opt** : Logiciels tiers optionnels

**Règle FHS :** Fichiers texte éditables, pas de binaires.

---

### Question 25
**Réponse correcte : A**

```bash
find / -mtime -7
# -mtime -7 : modifié < 7 jours (moins de)
# -mtime +7 : modifié > 7 jours (plus de)
# -mtime 7  : modifié exactement il y a 7 jours

# Exemples
find /home -mtime -1      # Modifié aujourd'hui
find /var/log -mtime +30  # Modifié > 30 jours
find /etc -mtime 0        # Modifié aujourd'hui (24h)
```

**Options temps find :**
```bash
-mtime  # Modification (content)
-atime  # Accès (lecture)
-ctime  # Changement (metadata: permissions, owner)

# Minutes
-mmin -60    # Modifié < 60 minutes
-amin -30    # Accédé < 30 minutes
```

**Pourquoi B incorrecte :** `+7` = plus de 7 jours (anciens), pas récents.
**Pourquoi C incorrecte :** `-atime` = accès, pas modification.

---

### Question 26
**Réponse correcte : D**

```bash
# Méthode octale
find / -perm -4000 2>/dev/null
# -4000 : au moins SUID bit

# Méthode symbolique
find / -perm -u+s 2>/dev/null

# Afficher détails
find / -perm -4000 -ls 2>/dev/null

# SUID courants
/usr/bin/passwd
/usr/bin/su
/usr/bin/sudo
```

**Différence - vs / vs exact :**
```bash
-perm 755    # Exactement 755
-perm -755   # Au moins tous bits de 755
-perm /755   # N'importe quel bit de 755
```

**Autres bits spéciaux :**
```bash
find / -perm -2000    # SGID
find / -perm -1000    # Sticky
find / -perm -6000    # SUID + SGID
```

**Audit sécurité :** Vérifier régulièrement fichiers SUID (potentiel escalade privilèges).

---

### Question 27
**Réponse correcte : B**

```bash
find / -size +100M 2>/dev/null
# + : plus grand que
# - : plus petit que
# (rien) : exactement

# Exemples
find / -size +1G      # > 1 GB
find / -size +500M -size -2G    # Entre 500M et 2G
find /var -type f -size +100M -exec ls -lh {} \;

# Unités
c : bytes
k : kilobytes
M : megabytes
G : gigabytes

find /home -size +10M -size -50M    # 10-50 MB
```

**Pourquoi autres incorrectes :**
- **A** : Exactement 100M (rare)
- **C** : Plus petit que 100M
- **D** : `du` montre utilisation, mais syntaxe incorrecte

**Trouver gros fichiers :**
```bash
find / -type f -size +1G -exec ls -lh {} \; | sort -k5 -hr
```

---

### Question 28
**Réponse correcte : D**

```bash
# Méthode -empty (recommandée)
find /var/log -empty
find /var/log -type f -empty    # Seulement fichiers
find /var/log -type d -empty    # Seulement répertoires

# Méthode -size 0
find /tmp -size 0
find /tmp -type f -size 0

# Supprimer fichiers vides
find /tmp -type f -empty -delete
```

**Cas d'usage :**
- Nettoyer logs vides
- Trouver dirs vides (potentiel suppression)
- Audit espace disque

**Répertoires vides :**
```bash
find /var -type d -empty
# Utile avant suppression structure obsolète
```

---

### Question 29
**Réponse correcte : D**

```bash
# Par nom user
find / -user alice 2>/dev/null
find /home -user bob

# Par UID
find / -uid 1000
find / -uid 0    # Root

# Par groupe
find / -group developers
find / -gid 1001

# Utilisateurs orphelins (user supprimé)
find / -nouser
find / -nogroup
```

**Exemples pratiques :**
```bash
# Tous fichiers d'un user
find /var/www -user www-data

# Fichiers root hors /root
find /home -user root

# Changer ownership en masse
find /data -user olduser -exec chown newuser {} \;
```

**Pourquoi C incorrecte :** `-owner` n'existe pas (correct = `-user`).

---

### Question 30
**Réponse correcte : A**

```bash
/var/log    # Logs système et applications

# Logs importants:
/var/log/syslog          # Logs système (Debian/Ubuntu)
/var/log/messages        # Logs système (RHEL/CentOS)
/var/log/auth.log        # Authentifications
/var/log/kern.log        # Kernel
/var/log/dmesg           # Boot messages
/var/log/apache2/        # Apache
/var/log/nginx/          # Nginx
/var/log/journal/        # Systemd journal

# Analyser logs
tail -f /var/log/syslog
journalctl -xe
grep "error" /var/log/syslog
```

**Structure /var :**
```bash
/var/log      # Logs
/var/cache    # Cache apps
/var/spool    # Files attente (print, mail)
/var/tmp      # Temp persistant
/var/www      # Racine web
/var/lib      # Données état apps
```

**Pourquoi autres incorrectes :**
- **B) /var/spool** : Files attente, pas logs
- **C) /tmp** : Temporaire, nettoyé
- **D) /usr/log** : N'existe pas

---
