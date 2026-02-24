# 🎓 Mock Exam LPIC-1 101-500 - Examen Blanc Complet

> **Format réel** : 60 questions | 90 minutes | 500/800 minimum (62.5%)  
> **Objectif visé** : 700/800 (87.5%) = 52+ bonnes réponses

---

## 📋 Instructions Examen

### Conditions réelles
- ⏱️ **Temps** : 90 minutes chrono (1h30)
- 📝 **Questions** : 60 au total
- ✅ **Réussite** : 500/800 minimum (38/60 questions)
- 🎯 **Objectif** : 700/800 (52/60 questions)
- 📵 **Sans aide** : Pas de notes, internet, documentation

### Consignes
1. Préparez une feuille pour noter vos réponses (1-60)
2. Démarrez chronomètre 90 minutes
3. Répondez dans l'ordre ou marquez les questions difficiles
4. Une seule réponse correcte par question
5. Pas de pénalité pour mauvaise réponse
6. À la fin : comparez avec grille de correction

### Répartition par sujet
| Sujet | Poids | Questions | % Examen |
|-------|-------|-----------|----------|
| 101 - Architecture Système | 8 pts | 12 Q | 20% |
| 102 - Installation & Packages | 10 pts | 15 Q | 25% |
| 103 - Commandes GNU/Unix | 16 pts | 24 Q | 40% |
| 104 - Filesystems & FHS | 6 pts | 9 Q | 15% |

---

## 📝 EXAMEN - 60 Questions

### Question 1 (Sujet 101)
Quelle commande affiche les **périphériques PCI** avec les modules kernel associés ?

- [ ] A) `lspci`  
- [ ] B) `lspci -k`  
- [ ] C) `lsusb`  
- [ ] D) `lsmod`

---

### Question 2 (Sujet 103)
Comment afficher les **10 dernières lignes** d'un fichier log en temps réel ?

- [ ] A) `head -10 /var/log/syslog`  
- [ ] B) `tail -10 /var/log/syslog`  
- [ ] C) `tail -f /var/log/syslog`  
- [ ] D) `cat /var/log/syslog | tail`

---

### Question 3 (Sujet 102)
Quelle commande **met à jour la liste des packages** disponibles sur Debian/Ubuntu ?

- [ ] A) `apt upgrade`  
- [ ] B) `apt update`  
- [ ] C) `apt install`  
- [ ] D) `dpkg --update`

---

### Question 4 (Sujet 104)
Dans `/etc/fstab`, que signifie le champ **pass=2** ?

- [ ] A) Monter en 2ème position  
- [ ] B) fsck après la partition root  
- [ ] C) Monter 2 fois  
- [ ] D) Ignorer fsck

---

### Question 5 (Sujet 103)
Quelle commande **supprime les lignes en double** dans un fichier trié ?

- [ ] A) `sort file`  
- [ ] B) `uniq file`  
- [ ] C) `sort -u file`  
- [ ] D) Les deux B et C

---

### Question 6 (Sujet 101)
Quel fichier contient les **informations CPU** ?

- [ ] A) `/proc/cpuinfo`  
- [ ] B) `/sys/cpu`  
- [ ] C) `/dev/cpu`  
- [ ] D) `/etc/cpu.conf`

---

### Question 7 (Sujet 102)
Comment installer un package **RPM** avec verbose et progress bar ?

- [ ] A) `rpm -i package.rpm`  
- [ ] B) `rpm -ivh package.rpm`  
- [ ] C) `rpm -Uvh package.rpm`  
- [ ] D) Les deux B et C

---

### Question 8 (Sujet 104)
Quelle commande affiche l'**UUID** d'une partition ?

- [ ] A) `fdisk -l`  
- [ ] B) `blkid`  
- [ ] C) `df -h`  
- [ ] D) `lsblk`

---

### Question 9 (Sujet 103)
Comment rediriger **stdout ET stderr** vers un fichier ?

- [ ] A) `cmd > file 2>&1`  
- [ ] B) `cmd &> file`  
- [ ] C) `cmd > file 2> file`  
- [ ] D) Les deux A et B

---

### Question 10 (Sujet 101)
Quelle est la **target systemd** équivalente au runlevel 5 ?

- [ ] A) `multi-user.target`  
- [ ] B) `graphical.target`  
- [ ] C) `rescue.target`  
- [ ] D) `default.target`

---

### Question 11 (Sujet 102)
Où sont stockés les **fichiers de configuration des repos YUM** ?

- [ ] A) `/etc/yum.conf`  
- [ ] B) `/etc/yum.repos.d/`  
- [ ] C) `/var/lib/yum/`  
- [ ] D) `/usr/share/yum/`

---

### Question 12 (Sujet 104)
Comment monter une partition en **lecture seule** ?

- [ ] A) `mount -r /dev/sdb1 /mnt`  
- [ ] B) `mount -o ro /dev/sdb1 /mnt`  
- [ ] C) `mount -o readonly /dev/sdb1 /mnt`  
- [ ] D) Les deux A et B

---

### Question 13 (Sujet 103)
Quelle variable contient le **code retour** de la dernière commande ?

- [ ] A) `$?`  
- [ ] B) `$!`  
- [ ] C) `$$`  
- [ ] D) `$0`

---

### Question 14 (Sujet 101)
Comment afficher les **logs du boot actuel** avec systemd ?

- [ ] A) `dmesg`  
- [ ] B) `journalctl -b`  
- [ ] C) `journalctl --boot`  
- [ ] D) Les deux B et C

---

### Question 15 (Sujet 102)
Quelle commande trouve le **package propriétaire** d'un fichier sur système Debian ?

- [ ] A) `dpkg -S /path/file`  
- [ ] B) `dpkg -L /path/file`  
- [ ] C) `apt-file search /path/file`  
- [ ] D) `which /path/file`

---

### Question 16 (Sujet 104)
Que signifie `chmod 755 script.sh` ?

- [ ] A) `rwxr-xr-x`  
- [ ] B) `rwxrwxrwx`  
- [ ] C) `rw-r--r--`  
- [ ] D) `rwx------`

---

### Question 17 (Sujet 103)
Comment chercher le mot "error" dans tous les fichiers `.log` récursivement ?

- [ ] A) `grep -r error *.log`  
- [ ] B) `grep -r error /var/log/`  
- [ ] C) `find /var/log/ -name "*.log" -exec grep error {} \;`  
- [ ] D) Les deux B et C

---

### Question 18 (Sujet 101)
Quelle commande **active un service** au démarrage avec systemd ?

- [ ] A) `systemctl start service`  
- [ ] B) `systemctl enable service`  
- [ ] C) `systemctl activate service`  
- [ ] D) `systemctl boot service`

---

### Question 19 (Sujet 102)
Comment afficher la **version disponible** d'un package avec APT ?

- [ ] A) `apt show package`  
- [ ] B) `apt-cache policy package`  
- [ ] C) `apt version package`  
- [ ] D) Les deux A et B

---

### Question 20 (Sujet 104)
Quelle commande vérifie l'**intégrité d'un filesystem ext4** ?

- [ ] A) `fsck /dev/sdb1`  
- [ ] B) `e2fsck /dev/sdb1`  
- [ ] C) `fsck.ext4 /dev/sdb1`  
- [ ] D) Toutes les réponses

---

### Question 21 (Sujet 103)
Comment supprimer tous les fichiers `.tmp` trouvés par find ?

- [ ] A) `find . -name "*.tmp" -delete`  
- [ ] B) `find . -name "*.tmp" -exec rm {} \;`  
- [ ] C) `find . -name "*.tmp" | xargs rm`  
- [ ] D) Toutes les réponses

---

### Question 22 (Sujet 101)
Quel paramètre kernel permet de **démarrer en mode rescue** ?

- [ ] A) `single`  
- [ ] B) `1`  
- [ ] C) `rescue`  
- [ ] D) Les deux A et B

---

### Question 23 (Sujet 102)
Comment **créer une table de partitions GPT** avec parted ?

- [ ] A) `parted /dev/sdb mklabel gpt`  
- [ ] B) `parted /dev/sdb mkpart gpt`  
- [ ] C) `fdisk /dev/sdb` puis `g`  
- [ ] D) Les deux A et C

---

### Question 24 (Sujet 104)
Quelle option `/etc/fstab` permet à un **user normal** de monter un device ?

- [ ] A) `auto`  
- [ ] B) `user`  
- [ ] C) `users`  
- [ ] D) `nouser`

---

### Question 25 (Sujet 103)
Comment afficher le **nombre de lignes** d'un fichier ?

- [ ] A) `wc file`  
- [ ] B) `wc -l file`  
- [ ] C) `cat file | wc -l`  
- [ ] D) Les deux B et C

---

### Question 26 (Sujet 101)
Quelle commande liste les **modules kernel chargés** ?

- [ ] A) `lsmod`  
- [ ] B) `modprobe -l`  
- [ ] C) `modinfo`  
- [ ] D) `insmod -l`

---

### Question 27 (Sujet 102)
Comment **reconfigurer les locales** sur Debian ?

- [ ] A) `dpkg-reconfigure locales`  
- [ ] B) `apt-reconfigure locales`  
- [ ] C) `locale-config`  
- [ ] D) `update-locale`

---

### Question 28 (Sujet 104)
Qu'est-ce que le **SUID bit** et comment l'activer ?

- [ ] A) Execute avec permissions owner, `chmod u+s`  
- [ ] B) Execute avec permissions group, `chmod g+s`  
- [ ] C) Seulement owner peut supprimer, `chmod +t`  
- [ ] D) Protection écriture, `chmod +i`

---

### Question 29 (Sujet 103)
Quelle regex grep trouve les lignes **commençant par "root"** ?

- [ ] A) `grep "root" file`  
- [ ] B) `grep "^root" file`  
- [ ] C) `grep "root$" file`  
- [ ] D) `grep "*root" file`

---

### Question 30 (Sujet 101)
Comment changer la **target par défaut** au boot avec systemd ?

- [ ] A) `systemctl set-default graphical.target`  
- [ ] B) `systemctl default graphical.target`  
- [ ] C) `systemctl isolate graphical.target`  
- [ ] D) `systemd-target graphical.target`

---

### Question 31 (Sujet 102)
Quelle commande liste **tous les packages installés** sur système RPM ?

- [ ] A) `rpm -qa`  
- [ ] B) `rpm -ql`  
- [ ] C) `yum list`  
- [ ] D) `yum installed`

---

### Question 32 (Sujet 104)
Comment créer un **lien symbolique** ?

- [ ] A) `ln file link`  
- [ ] B) `ln -s /path/target link`  
- [ ] C) `symlink /path/target link`  
- [ ] D) `link -s file link`

---

### Question 33 (Sujet 103)
Comment trier un fichier par **ordre numérique** ?

- [ ] A) `sort file`  
- [ ] B) `sort -n file`  
- [ ] C) `sort -r file`  
- [ ] D) `sort -numeric file`

---

### Question 34 (Sujet 101)
Quel fichier éditer pour **configurer GRUB 2** ?

- [ ] A) `/boot/grub/grub.cfg`  
- [ ] B) `/etc/default/grub`  
- [ ] C) `/boot/grub/menu.lst`  
- [ ] D) `/etc/grub.conf`

---

### Question 35 (Sujet 102)
Comment installer un fichier `.deb` avec dpkg ?

- [ ] A) `dpkg package.deb`  
- [ ] B) `dpkg -i package.deb`  
- [ ] C) `dpkg --install package.deb`  
- [ ] D) Les deux B et C

---

### Question 36 (Sujet 104)
Dans FHS, où sont stockés les **logs système** ?

- [ ] A) `/var/log/`  
- [ ] B) `/var/spool/`  
- [ ] C) `/tmp/`  
- [ ] D) `/usr/log/`

---

### Question 37 (Sujet 103)
Comment copier une ligne dans vi/vim ?

- [ ] A) `cc`  
- [ ] B) `yy`  
- [ ] C) `dd`  
- [ ] D) `cp`

---

### Question 38 (Sujet 102)
Quelle commande **met à jour le cache des bibliothèques** ?

- [ ] A) `ldconfig`  
- [ ] B) `ldd`  
- [ ] C) `ldupdate`  
- [ ] D) `libcache`

---

### Question 39 (Sujet 104)
Comment trouver tous les fichiers **SUID** (sécurité) ?

- [ ] A) `find / -perm 4000`  
- [ ] B) `find / -perm -4000`  
- [ ] C) `find / -perm -u+s`  
- [ ] D) Les deux B et C

---

### Question 40 (Sujet 103)
Quelle commande envoie un processus en **arrière-plan** ?

- [ ] A) `command &`  
- [ ] B) `bg command`  
- [ ] C) `background command`  
- [ ] D) `nohup command`

---

### Question 41 (Sujet 101)
Comment afficher les **services actifs** avec systemd ?

- [ ] A) `systemctl list-units --type=service`  
- [ ] B) `systemctl status`  
- [ ] C) `systemctl list-services`  
- [ ] D) `service --status-all`

---

### Question 42 (Sujet 102)
Quelle commande cherche un fichier dans les **packages RPM** ?

- [ ] A) `rpm -qf /path/file`  
- [ ] B) `rpm -ql /path/file`  
- [ ] C) `yum provides /path/file`  
- [ ] D) Les deux A et C

---

### Question 43 (Sujet 104)
Quelle commande change **propriétaire ET groupe** d'un fichier ?

- [ ] A) `chown user file`  
- [ ] B) `chown user:group file`  
- [ ] C) `chgrp user:group file`  
- [ ] D) `chmod user:group file`

---

### Question 44 (Sujet 103)
Comment extraire le **champ 1** d'un fichier délimité par `:` ?

- [ ] A) `cut -d: -f1 file`  
- [ ] B) `cut -c1 file`  
- [ ] C) `awk -F: '{print $1}' file`  
- [ ] D) Les deux A et C

---

### Question 45 (Sujet 101)
Comment recharger la **configuration systemd** après modification d'un unit file ?

- [ ] A) `systemctl reload`  
- [ ] B) `systemctl daemon-reload`  
- [ ] C) `systemctl restart`  
- [ ] D) `systemctl update`

---

### Question 46 (Sujet 102)
Dans `/etc/apt/sources.list`, que signifie **`deb-src`** ?

- [ ] A) Sources binaires  
- [ ] B) Sources code source  
- [ ] C) Sources secondaires  
- [ ] D) Sources sécurisées

---

### Question 47 (Sujet 104)
Comment remonter `/mnt` en **read-write** sans démonter ?

- [ ] A) `mount -o rw /mnt`  
- [ ] B) `mount -o remount,rw /mnt`  
- [ ] C) `umount /mnt && mount -o rw /mnt`  
- [ ] D) Impossible sans démonter

---

### Question 48 (Sujet 103)
Quelle commande tue un processus par son **nom** ?

- [ ] A) `kill processname`  
- [ ] B) `killall processname`  
- [ ] C) `pkill processname`  
- [ ] D) Les deux B et C

---

### Question 49 (Sujet 101)
Quel répertoire contient les **units systemd personnalisées** (priorité) ?

- [ ] A) `/usr/lib/systemd/system/`  
- [ ] B) `/etc/systemd/system/`  
- [ ] C) `/lib/systemd/system/`  
- [ ] D) `/var/lib/systemd/`

---

### Question 50 (Sujet 102)
Comment lister les **groupes de packages** disponibles avec YUM ?

- [ ] A) `yum grouplist`  
- [ ] B) `yum list groups`  
- [ ] C) `yum groups`  
- [ ] D) `yum package-groups`

---

### Question 51 (Sujet 104)
Quelle est la fonction du **sticky bit** sur `/tmp` ?

- [ ] A) Empêcher exécution  
- [ ] B) Seulement owner peut supprimer ses fichiers  
- [ ] C) Root seulement  
- [ ] D) Protection lecture

---

### Question 52 (Sujet 103)
Comment afficher les **processus d'un utilisateur** spécifique ?

- [ ] A) `ps -u username`  
- [ ] B) `ps aux | grep username`  
- [ ] C) `top -u username`  
- [ ] D) Toutes les réponses

---

### Question 53 (Sujet 101)
Quelle commande affiche les **messages kernel du boot** ?

- [ ] A) `dmesg`  
- [ ] B) `journalctl -k`  
- [ ] C) `cat /var/log/dmesg`  
- [ ] D) Les deux A et B

---

### Question 54 (Sujet 102)
Comment **supprimer un package** avec APT en gardant la config ?

- [ ] A) `apt remove package`  
- [ ] B) `apt purge package`  
- [ ] C) `apt delete package`  
- [ ] D) `apt uninstall package`

---

### Question 55 (Sujet 104)
Comment trouver les fichiers **modifiés dans les 7 derniers jours** ?

- [ ] A) `find / -mtime -7`  
- [ ] B) `find / -mtime +7`  
- [ ] C) `find / -atime -7`  
- [ ] D) `find / -ctime -7`

---

### Question 56 (Sujet 103)
En vi, comment **sauvegarder et quitter** ?

- [ ] A) `:w`  
- [ ] B) `:q`  
- [ ] C) `:wq`  
- [ ] D) `:x`  
- [ ] E) Les deux C et D

---

### Question 57 (Sujet 102)
Quel outil créer des partitions **MBR et GPT** ?

- [ ] A) `fdisk`  
- [ ] B) `gdisk`  
- [ ] C) `parted`  

---

### Question 58 (Sujet 104)
Quelle commande crée un **filesystem XFS** ?

- [ ] A) `mkfs.xfs /dev/sdb1`  
- [ ] B) `mkfs -t xfs /dev/sdb1`  
- [ ] C) `xfs_mkfs /dev/sdb1`  
- [ ] D) Les deux A et B

---

### Question 59 (Sujet 103)
Comment donner la **priorité maximale** à un processus (root) ?

- [ ] A) `nice -n 20 command`  
- [ ] B) `nice -n -20 command`  
- [ ] C) `renice 0 -p PID`  
- [ ] D) `nice -n 0 command`

---

### Question 60 (Sujet 104)
Quel code retour `fsck` indique **erreurs NON corrigées** ?

- [ ] A) `0`  
- [ ] B) `1`  
- [ ] C) `2`  
- [ ] D) `4`

---

## ✅ CORRECTION COMPLÈTE

### Question 1 : **B** - `lspci -k`
Affiche périphériques PCI + modules kernel (`-k`). `lspci` seul = sans modules.

### Question 2 : **C** - `tail -f /var/log/syslog`
`-f` = follow (temps réel). `-10` = seulement 10 lignes statiques.

### Question 3 : **B** - `apt update`
MAJ listes packages. `apt upgrade` = installe MAJ, `apt install` = installe package.

### Question 4 : **B** - fsck après root
Pass: 0=skip, 1=root first, 2=others after root.

### Question 5 : **D** - Les deux B et C
`uniq` sur fichier trié, `sort -u` tri + supprime doublons en une commande.

### Question 6 : **A** - `/proc/cpuinfo`
Infos CPU. `/proc/meminfo` = RAM, `/proc` = virtual filesystem.

### Question 7 : **D** - Les deux B et C
`-i` install, `-U` upgrade, `-v` verbose, `-h` hash. `-Uvh` plus courant.

### Question 8 : **B** - `blkid`
Affiche UUID. `lsblk -f` aussi mais `blkid` plus direct.

### Question 9 : **D** - Les deux A et B
`2>&1` (ancien) ou `&>` (moderne) redirigent stdout+stderr.

### Question 10 : **B** - `graphical.target`
Runlevel 5 = GUI = graphical.target. Runlevel 3 = multi-user.target.

### Question 11 : **B** - `/etc/yum.repos.d/`
Fichiers `.repo`. `/etc/yum.conf` = config général.

### Question 12 : **D** - Les deux A et B
`-r` ou `-o ro` = read-only. `-o ro` plus explicite.

### Question 13 : **A** - `$?`
Code retour (0=succès). `$$`=PID, `$!`=PID dernier background, `$0`=nom script.

### Question 14 : **D** - Les deux B et C
`journalctl -b` ou `--boot` équivalents. `-b -1` = boot précédent.

### Question 15 : **A** - `dpkg -S /path/file`
`-S` = search package owner. `-L` = list files in package.

### Question 16 : **A** - `rwxr-xr-x`
755 = 7(rwx) 5(r-x) 5(r-x). 644 = rw-r--r--.

### Question 17 : **D** - Les deux B et C
`grep -r` récursif, `find -exec grep` aussi. Option B plus simple.

### Question 18 : **B** - `systemctl enable service`
Enable = activer boot. Start = démarrer maintenant.

### Question 19 : **D** - Les deux A et B
`apt show` et `apt-cache policy` affichent versions disponibles.

### Question 20 : **D** - Toutes
`fsck`, `e2fsck`, `fsck.ext4` équivalents pour ext4.

### Question 21 : **D** - Toutes
`-delete`, `-exec rm`, `| xargs rm` fonctionnent. `-delete` plus efficace.

### Question 22 : **D** - Les deux A et B
`single`, `1`, `S` = single-user/rescue mode.

### Question 23 : **A** - parted /dev/sdb mklabel gpt 
`parted /dev/sdb mklabel gpt`  crée une table de partition GPT.

### Question 24 : **B** - `user`
Option `user` permet user normal de monter. `users` = n'importe qui peut démonter.

### Question 25 : **D** - Les deux B et C
`wc -l` compte lignes. Pipe aussi mais moins efficace.

### Question 26 : **A** - `lsmod`
Liste modules chargés. `modinfo` = infos module, `modprobe` = charger.

### Question 27 : **A** - `dpkg-reconfigure locales`
Outil Debian reconfiguration packages. Aussi timezone (`tzdata`).

### Question 28 : **A** - Execute comme owner, `chmod u+s`
SUID = execute avec permissions propriétaire. Exemple: `/usr/bin/passwd`.

### Question 29 : **B** - `grep "^root" file`
`^` = début ligne. `$` = fin ligne. `*` = répétition (regex).

### Question 30 : **A** - `systemctl set-default graphical.target`
Set-default = target par défaut boot. Isolate = changer immédiatement.

### Question 31 : **A** - `rpm -qa`
Query all packages. `yum list installed` aussi mais `rpm -qa` plus direct.

### Question 32 : **B** - `ln -s /path/target link`
`-s` = symbolic. `ln` sans option = hardlink.

### Question 33 : **B** - `sort -n file`
`-n` = numérique. `-r` = reverse, défaut = alphabétique.

### Question 34 : **B** - `/etc/default/grub`
Éditer ici puis `update-grub`. `/boot/grub/grub.cfg` = généré (NE PAS éditer).

### Question 35 : **D** - Les deux B et C
`-i` et `--install` équivalents.

### Question 36 : **A** - `/var/log/`
Logs système. `/var/spool/` = queues (mail, print).

### Question 37 : **B** - `yy`
Yank line. `dd` = delete, `p` = paste, `cc` = change line.

### Question 38 : **A** - `ldconfig`
MAJ cache libs (`/etc/ld.so.cache`). `ldd` = affiche dépendances.

### Question 39 : **D** - Les deux B et C
`-perm -4000` ou `-perm -u+s` trouvent SUID. `-perm 4000` = exact (rare).

### Question 40 : **A** - `command &`
`&` = background. `bg %1` = reprendre job suspendu. `nohup` = persiste après logout.

### Question 41 : **A** - `systemctl list-units --type=service`
Liste services actifs. `--state=active` pour filtrer.

### Question 42 : **D** - Les deux A et C
`rpm -qf` package propriétaire fichier local. `yum provides` cherche dans repos.

### Question 43 : **B** - `chown user:group file`
Syntaxe `user:group`. `chgrp` = seulement groupe.

### Question 44 : **D** - Les deux A et C
`cut -d: -f1` et `awk -F:` équivalents. `awk` plus puissant.

### Question 45 : **B** - `systemctl daemon-reload`
Recharge configuration systemd après edit unit file.

### Question 46 : **B** - Sources code source
`deb` = binaires, `deb-src` = code source.

### Question 47 : **B** - `mount -o remount,rw /mnt`
Remount change options sans démonter.

### Question 48 : **D** - Les deux B et C
`killall` et `pkill` tuent par nom. `kill` nécessite PID.

### Question 49 : **B** - `/etc/systemd/system/`
Prioritaire sur `/usr/lib/systemd/system/` (défaut système).

### Question 50 : **A** - `yum grouplist`
Liste groupes packages. `yum groupinstall "Group"` = installer groupe.

### Question 51 : **B** - Seulement owner peut supprimer
Sticky bit `/tmp` (1777) : chacun crée mais supprime seulement ses fichiers.

### Question 52 : **D** - Toutes
`ps -u`, `ps aux | grep`, `top -u` fonctionnent.

### Question 53 : **D** - Les deux A et B
`dmesg` et `journalctl -k` affichent messages kernel.

### Question 54 : **A** - `apt remove package`
Remove = garde config. Purge = supprime config.

### Question 55 : **A** - `find / -mtime -7`
`-7` = moins de 7 jours. `+7` = plus de 7 jours (ancien).

### Question 56 : **E** - Les deux C et D
`:wq` et `:x` équivalents. `ZZ` aussi.

### Question 57 : **D** - Seulement C
`parted` supporte MBR ET GPT. `fdisk` = MBR seulement, `gdisk` = GPT seulement.

### Question 58 : **D** - Les deux A et B
`mkfs.xfs` et `mkfs -t xfs` équivalents.

### Question 59 : **B** - `nice -n -20 command`
-20 = priorité max (root seulement). +19 = min. Défaut = 0.

### Question 60 : **D** - `4`
Codes fsck: 0=OK, 1=corrigé, 2=reboot needed, 4=erreurs restantes.

---

## 📊 Calcul Score

### Formule
```
Score/800 = (Bonnes réponses / 60) × 800
```

### Barème
| Bonnes réponses | Score/800 | % | Résultat |
|-----------------|-----------|---|----------|
| **60** | 800 | 100% | 🏆 Parfait |
| **56-59** | 747-787 | 93-98% | ⭐ Excellent |
| **52-55** | 693-733 | 87-92% | ✅ Très bien (objectif) |
| **48-51** | 640-687 | 80-85% | ✅ Bien |
| **38-47** | 507-627 | 63-78% | ✅ Passé (juste) |
| **<38** | <507 | <63% | ❌ Échec |

**Minimum requis** : 38/60 (500/800)  
**Objectif visé** : 52/60 (700/800)

---

## 🎯 Recommandations Post-Examen

### Score ≥ 700/800 (52+/60) - ✅ PRÊT
**Vous êtes prêt pour l'examen !**
- ✅ Continuez révision légère quotidienne
- ✅ Anki cards 30min/jour
- ✅ Relire Fiche-Commandes-Essentielles.md
- ✅ Pratiquer commandes CLI
- 📅 Planifier examen sous 1-2 semaines

**Dernière semaine** :
- J-7 à J-3 : Anki + Labs pratiques
- J-2 : Repos mental
- J-1 : Fiche-Commandes-Essentielles uniquement

---

### Score 600-693/800 (45-51/60) - ⚠️ PRESQUE
**Bon niveau, consolidation nécessaire**
- 📚 Identifier sujets faibles (analyse ci-dessus)
- 📖 Relire Notes sujets faibles
- 🎯 Refaire QCM sujets faibles
- 🔄 Refaire Mock Exam dans 1 semaine
- ⏱️ Objectif : +10% au 2ème essai
- 📅 Examen dans 2-3 semaines

**Plan révision** :
1. Jour 1-3 : Sujet le plus faible
2. Jour 4-6 : 2ème sujet faible
3. Jour 7 : Mock Exam v2
4. Si >700 : Continuer, sinon répéter

---

### Score 500-599/800 (38-44/60) - ⚠️ JUSTE
**Réussite limite, révision intensive requise**
- ❌ **NE PAS planifier examen maintenant**
- 📚 Révision complète tous sujets
- 📖 Relire TOUTES les Notes
- 🎯 Refaire TOUS les QCM (objectif 85%+)
- 🔄 Mock Exam hebdomadaire
- 📅 Examen dans 3-4 semaines minimum

**Plan révision intensive** :
- Semaine 1 : Sujets 101+102 (Notes + QCM)
- Semaine 2 : Sujet 103 (Notes + QCM)
- Semaine 3 : Sujet 104 + Mock v2
- Semaine 4 : Anki intensif + Mock v3
- Si Mock v3 >700 : Planifier examen

---

### Score <500/800 (<38/60) - ❌ ÉCHEC
**Base insuffisante, révision complète nécessaire**
- 🛑 **Stopper préparation actuelle**
- 📚 Retour aux fondamentaux
- 📖 Relire TOUTES les Notes (2 passages)
- 🎯 Refaire QCM jusqu'à 90%+ chacun
- 💻 Pratiquer CLI intensivement (VM Linux)
- 🔄 Mock Exam toutes les 2 semaines
- 📅 Examen dans 6-8 semaines

**Plan révision complète** :
1. **Semaines 1-2** : Sujet 101+102
   - Lire Notes 2x
   - QCM jusqu'à 90%+
   - Labs pratiques quotidiens
   
2. **Semaines 3-4** : Sujet 103
   - Lire Notes 2x
   - QCM jusqu'à 90%+
   - Shell scripting pratique
   
3. **Semaine 5** : Sujet 104
   - Lire Notes 2x
   - QCM jusqu'à 90%+
   - Permissions/mount pratique
   
4. **Semaines 6-8** :
   - Mock Exam hebdomadaire
   - Anki quotidien (1h)
   - CLI pratique (2h/jour)
   - Si 3 Mock >700 : OK examen

**Ressources additionnelles recommandées** :
- KodeKloud Linux courses
- LPI Learning Materials
- Linux VM pratique quotidienne
- Cours vidéo complementaires

---

## 📝 Notes Examen Réel

### Points d'attention
1. **Gestion temps** : 90min ÷ 60Q = 1.5min/question
2. **Questions difficiles** : Marquer, passer, revenir après
3. **Pas de pénalité** : Toujours répondre (élimination)
4. **Commandes exactes** : Syntaxe précise demandée
5. **UUID obligatoire** : Dans fstab (pas /dev/sdX)
6. **fsck démonté** : TOUJOURS démonter avant
7. **Permissions calcul** : r=4, w=2, x=1 rapidement

### Erreurs fréquentes à éviter
- Confondre `systemctl enable` (boot) et `start` (maintenant)
- `rpm -qa` vs `rpm -ql` (all vs list)
- `dpkg -S` vs `dpkg -L` (search owner vs list)
- `find -mtime -7` (récent) vs `+7` (ancien)
- `chmod 755` vs `644` (scripts vs fichiers)
- SUID (`u+s`) vs SGID (`g+s`) vs Sticky (`+t`)
- `mount -o remount` oublié (modif options)

### Stratégie examen
1. **1er passage** (60 min) : Questions faciles/moyennes
2. **2ème passage** (20 min) : Questions difficiles marquées
3. **Vérification** (10 min) : Relecture réponses douteuses

---

## 🚀 Prochaines Étapes

1. **Calculer score** : ___/60 = ___/800
2. **Analyser par sujet** : Identifier faiblesses
3. **Suivre recommandations** : Plan selon score
4. **Refaire Mock** : Dans 1-2 semaines
5. **Planifier examen** : Quand 3 Mock >700/800

**Bon courage ! Vous avez tous les outils pour réussir ! 🎯**
