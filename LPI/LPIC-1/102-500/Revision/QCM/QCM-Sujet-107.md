# 📝 QCM de Révision - Sujet 107 : Tâches Administratives

**LPIC-1 Exam 102-500**  
**Poids du sujet : 12 points**

---

## 📋 Instructions

- Ce QCM contient **60 questions** réparties sur les 3 objectifs du Sujet 107
- Chaque question comporte une ou plusieurs bonnes réponses
- Les réponses et explications détaillées sont fournies à la fin
- Temps recommandé : 90 minutes

**Répartition des questions :**
- 107.1 - Gestion des comptes utilisateurs et groupes : 25 questions
- 107.2 - Automatisation des tâches : 20 questions
- 107.3 - Paramètres régionaux et langues : 15 questions

---

## 🎯 Objectif 107.1 - Gestion des Comptes Utilisateurs et Groupes (25 questions)

### Question 1
Quelle commande permet de créer un nouvel utilisateur avec un répertoire personnel ?

- [ ] A. `useradd michael`  
- [ ] B. `useradd -m michael`  
- [ ] C. `adduser michael`  
- [ ] D. `createuser -h michael`

---

### Question 2
Quelle option de `usermod` permet d'ajouter un utilisateur à un groupe secondaire sans supprimer ses groupes existants ?

- [ ] A. `usermod -G developers michael`  
- [ ] B. `usermod -a -G developers michael`  
- [ ] C. `usermod -append -G developers michael`  
- [ ] D. `usermod -add -G developers michael`

---

### Question 3
Dans `/etc/passwd`, quel est le troisième champ ?

- [ ] A. Le nom d'utilisateur  
- [ ] B. Le mot de passe chiffré  
- [ ] C. L'UID (User ID)  
- [ ] D. Le GID (Group ID)

---

### Question 4
Quel fichier contient les mots de passe chiffrés des utilisateurs ?

- [ ] A. `/etc/passwd`  
- [ ] B. `/etc/shadow`  
- [ ] C. `/etc/security`  
- [ ] D. `/etc/passwords`

---

### Question 5
Quelle commande permet de verrouiller un compte utilisateur ?

- [ ] A. `passwd -l michael`  
- [ ] B. `usermod -L michael`  
- [ ] C. `chage -E 0 michael`  
- [ ] D. Toutes les réponses ci-dessus

---

### Question 6
Dans `/etc/shadow`, que signifie un mot de passe qui commence par `!` ?

- [ ] A. Le compte n'a pas de mot de passe  
- [ ] B. Le compte est verrouillé  
- [ ] C. Le mot de passe a expiré  
- [ ] D. Le compte doit changer son mot de passe

---

### Question 7
Quelle commande équivaut à `passwd -x 90 michael` ?

- [ ] A. `chage -M 90 michael`  
- [ ] B. `chage -m 90 michael`  
- [ ] C. `chage -E 90 michael`  
- [ ] D. `chage -W 90 michael`

---

### Question 8
Quel répertoire contient les fichiers copiés automatiquement dans le répertoire personnel des nouveaux utilisateurs ?

- [ ] A. `/etc/default`  
- [ ] B. `/etc/skel`  
- [ ] C. `/home/template`  
- [ ] D. `/etc/users/template`

---

### Question 9
Dans `/etc/login.defs`, quelle directive définit la plage des UID pour les utilisateurs ordinaires ?

- [ ] A. `USER_UID_MIN` et `USER_UID_MAX`  
- [ ] B. `UID_MIN` et `UID_MAX`  
- [ ] C. `NORMAL_UID_MIN` et `NORMAL_UID_MAX`  
- [ ] D. `REGULAR_UID_MIN` et `REGULAR_UID_MAX`

---

### Question 10
Quelle commande permet d'afficher les informations d'expiration du mot de passe d'un utilisateur ?

- [ ] A. `passwd -S michael`  
- [ ] B. `chage -l michael`  
- [ ] C. `getent shadow michael`  
- [ ] D. A et B

---

### Question 11
Comment supprimer l'utilisateur `michael` ainsi que son répertoire personnel et son spool de courrier ?

- [ ] A. `userdel michael`  
- [ ] B. `userdel -r michael`  
- [ ] C. `userdel -f michael`  
- [ ] D. `deluser --remove-home michael`

---

### Question 12
Dans `/etc/group`, combien de champs y a-t-il par ligne ?

- [ ] A. 3  
- [ ] B. 4  
- [ ] C. 5  
- [ ] D. 7

---

### Question 13
Quelle commande permet de définir le mot de passe d'un groupe ?

- [ ] A. `grouppasswd developers`  
- [ ] B. `passwd -g developers`  
- [ ] C. `gpasswd developers`  
- [ ] D. `groupmod -p developers`

---

### Question 14
Comment ajouter l'utilisateur `michael` au groupe `developers` en utilisant `gpasswd` ?

- [ ] A. `gpasswd -a michael developers`  
- [ ] B. `gpasswd -add michael developers`  
- [ ] C. `gpasswd -A michael developers`  
- [ ] D. `gpasswd -m michael developers`

---

### Question 15
Quelle commande permet de lister les entrées de la base de données des utilisateurs via NSS ?

- [ ] A. `cat /etc/passwd`  
- [ ] B. `grep michael /etc/passwd`  
- [ ] C. `getent passwd`  
- [ ] D. `list passwd`

---

### Question 16
Quel est l'UID de l'utilisateur root ?

- [ ] A. 0  
- [ ] B. 1  
- [ ] C. 100  
- [ ] D. 1000

---

### Question 17
Quelle option de `useradd` permet de créer un utilisateur sans répertoire personnel ?

- [ ] A. `useradd -M michael`  
- [ ] B. `useradd -no-home michael`  
- [ ] C. `useradd -d /dev/null michael`  
- [ ] D. `useradd -H michael`

---

### Question 18
Comment forcer un utilisateur à changer son mot de passe lors de la prochaine connexion ?

- [ ] A. `passwd -e michael`  
- [ ] B. `chage -d 0 michael`  
- [ ] C. `usermod -p expired michael`  
- [ ] D. A et B

---

### Question 19
Dans `/etc/shadow`, quel champ représente le nombre de jours d'avertissement avant l'expiration du mot de passe ?

- [ ] A. Champ 5  
- [ ] B. Champ 6  
- [ ] C. Champ 7  
- [ ] D. Champ 8

---

### Question 20
Quelle commande permet de renommer le groupe `developers` en `devteam` ?

- [ ] A. `groupmod -n devteam developers`  
- [ ] B. `groupmod -r devteam developers`  
- [ ] C. `grouprename developers devteam`  
- [ ] D. `mv developers devteam`

---

### Question 21
Quelle commande affiche l'UID, le GID et les groupes d'un utilisateur ?

- [ ] A. `groups michael`  
- [ ] B. `id michael`  
- [ ] C. `whoami michael`  
- [ ] D. `userinfo michael`

---

### Question 22
Pourquoi ne peut-on pas supprimer un groupe s'il est le groupe primaire d'un utilisateur ?

- [ ] A. C'est une limitation technique  
- [ ] B. Cela rendrait l'utilisateur invalide  
- [ ] C. Le groupe primaire doit toujours exister pour les permissions de fichiers  
- [ ] D. B et C

---

### Question 23
Quelle est la permission spéciale activée sur `/usr/bin/passwd` ?

- [ ] A. Sticky bit  
- [ ] B. SUID  
- [ ] C. SGID  
- [ ] D. Aucune

---

### Question 24
Comment définir la durée de vie minimale du mot de passe à 10 jours pour l'utilisateur `michael` ?

- [ ] A. `passwd -n 10 michael`  
- [ ] B. `chage -m 10 michael`  
- [ ] C. `usermod -m 10 michael`  
- [ ] D. A et B

---

### Question 25
Quel fichier contient les administrateurs et membres d'un groupe avec les mots de passe chiffrés des groupes ?

- [ ] A. `/etc/group`  
- [ ] B. `/etc/gshadow`  
- [ ] C. `/etc/passwd`  
- [ ] D. `/etc/shadow`

---

## 🎯 Objectif 107.2 - Automatisation des Tâches (20 questions)

### Question 26
Dans une crontab utilisateur, combien de champs sont nécessaires pour définir une tâche ?

- [ ] A. 5  
- [ ] B. 6  
- [ ] C. 7  
- [ ] D. 8

---

### Question 27
Que signifie l'entrée cron suivante : `0 10 * * * /home/user/script.sh` ?

- [ ] A. Exécuter le script tous les jours à 10h00  
- [ ] B. Exécuter le script toutes les 10 minutes  
- [ ] C. Exécuter le script le 10 de chaque mois  
- [ ] D. Exécuter le script 10 fois par jour

---

### Question 28
Quelle est la signification de `*/15` dans un champ minute d'une crontab ?

- [ ] A. Toutes les 15 minutes  
- [ ] B. À la 15ème minute  
- [ ] C. 15 fois par heure  
- [ ] D. Tous les 15 jours

---

### Question 29
Comment éditer sa propre crontab ?

- [ ] A. `nano /var/spool/cron/username`  
- [ ] B. `crontab -e`  
- [ ] C. `edit crontab`  
- [ ] D. `vi ~/.crontab`

---

### Question 30
Quel raccourci cron exécute une tâche tous les jours à minuit ?

- [ ] A. `@hourly`  
- [ ] B. `@daily`  
- [ ] C. `@midnight`  
- [ ] D. B et C

---

### Question 31
Dans une crontab système, quelle est la différence avec une crontab utilisateur ?

- [ ] A. Elle a 7 champs au lieu de 6  
- [ ] B. Elle inclut le nom d'utilisateur qui exécute la commande  
- [ ] C. Elle se trouve dans `/etc/crontab`  
- [ ] D. Toutes les réponses ci-dessus

---

### Question 32
Quelle variable d'environnement dans une crontab permet d'éviter l'envoi d'emails ?

- [ ] A. `MAILTO=""`  
- [ ] B. `NOEMAIL=true`  
- [ ] C. `SILENT=yes`  
- [ ] D. `MAIL=false`

---

### Question 33
Quel fichier permet de restreindre l'accès à cron pour certains utilisateurs ?

- [ ] A. `/etc/cron.allow`  
- [ ] B. `/etc/cron.deny`  
- [ ] C. `/etc/crontab.conf`  
- [ ] D. A et B

---

### Question 34
Si `/etc/cron.allow` existe, qui peut utiliser cron ?

- [ ] A. Tous les utilisateurs  
- [ ] B. Seuls les utilisateurs listés dans ce fichier  
- [ ] C. Tous sauf ceux listés dans `/etc/cron.deny`  
- [ ] D. Uniquement root

---

### Question 35
Comment planifier une tâche qui s'exécute tous les lundis à 8h30 ?

- [ ] A. `30 8 * * 1 commande`  
- [ ] B. `30 8 * * Mon commande`  
- [ ] C. `30 8 * * monday commande`  
- [ ] D. A et B

---

### Question 36
Quelle commande permet de planifier une tâche ponctuelle à 10h00 demain ?

- [ ] A. `cron 10:00 tomorrow`  
- [ ] B. `at 10:00 tomorrow`  
- [ ] C. `schedule 10:00 tomorrow`  
- [ ] D. `crontab tomorrow 10:00`

---

### Question 37
Comment lister toutes les tâches `at` en attente ?

- [ ] A. `at -l`  
- [ ] B. `atq`  
- [ ] C. `at --list`  
- [ ] D. A et B

---

### Question 38
Quelle commande permet de supprimer la tâche `at` numéro 12 ?

- [ ] A. `atrm 12`  
- [ ] B. `at -d 12`  
- [ ] C. `at -r 12`  
- [ ] D. A et B

---

### Question 39
Quel démon doit être en cours d'exécution pour utiliser `at` ?

- [ ] A. `crond`  
- [ ] B. `atd`  
- [ ] C. `scheduled`  
- [ ] D. `systemd-timer`

---

### Question 40
Dans un timer systemd, quelle section contient l'option `OnCalendar` ?

- [ ] A. `[Unit]`  
- [ ] B. `[Timer]`  
- [ ] C. `[Install]`  
- [ ] D. `[Service]`

---

### Question 41
Quelle syntaxe `OnCalendar` exécute une tâche tous les jours à 8h30 ?

- [ ] A. `OnCalendar=*-*-* 08:30:00`  
- [ ] B. `OnCalendar=daily 08:30`  
- [ ] C. `OnCalendar=08:30:00`  
- [ ] D. `OnCalendar=* * * 08:30`

---

### Question 42
Comment lister tous les timers systemd actifs ?

- [ ] A. `systemctl list-timers`  
- [ ] B. `systemctl status timers`  
- [ ] C. `timerctl list`  
- [ ] D. `journalctl --timers`

---

### Question 43
Quelle commande permet de voir les logs d'un service déclenché par un timer ?

- [ ] A. `tail /var/log/timer.log`  
- [ ] B. `journalctl -u service-name.service`  
- [ ] C. `systemctl logs service-name`  
- [ ] D. `cat /var/log/systemd/service-name.log`

---

### Question 44
Quel raccourci `OnCalendar` exécute une tâche chaque lundi à minuit ?

- [ ] A. `weekly`  
- [ ] B. `monday`  
- [ ] C. `@weekly`  
- [ ] D. `Mon 00:00:00`

---

### Question 45
Quelle commande permet de créer un timer systemd transitoire qui exécute `date` dans 5 minutes ?

- [ ] A. `systemd-run --on-active="5m" date`  
- [ ] B. `systemd-timer --delay=5m date`  
- [ ] C. `systemctl run --in=5m date`  
- [ ] D. `timerctl create --delay=5 date`

---

## 🎯 Objectif 107.3 - Paramètres Régionaux et Langues (15 questions)

### Question 46
Que signifie UTC ?

- [ ] A. Universal Time Code  
- [ ] B. Unified Time Coordination  
- [ ] C. Universal Time Coordinated (Temps Universel Coordonné)  
- [ ] D. United Time Clock

---

### Question 47
Quelle commande affiche la date et l'heure actuelles sous Linux ?

- [ ] A. `time`  
- [ ] B. `date`  
- [ ] C. `clock`  
- [ ] D. `datetime`

---

### Question 48
Sur un système systemd, quelle commande permet de définir le fuseau horaire ?

- [ ] A. `tzset Europe/Paris`  
- [ ] B. `timedatectl set-timezone Europe/Paris`  
- [ ] C. `date -z Europe/Paris`  
- [ ] D. `timezone set Europe/Paris`

---

### Question 49
Quel fichier contient le nom du fuseau horaire par défaut du système ?

- [ ] A. `/etc/timezone`  
- [ ] B. `/etc/localtime`  
- [ ] C. `/etc/time.conf`  
- [ ] D. `/etc/tz`

---

### Question 50
Quelle variable d'environnement définit le fuseau horaire pour la session shell ?

- [ ] A. `TIMEZONE`  
- [ ] B. `TZ`  
- [ ] C. `TZNAME`  
- [ ] D. `TIME_ZONE`

---

### Question 51
Quel format représente un locale complet ?

- [ ] A. `fr_FR`  
- [ ] B. `fr.UTF-8`  
- [ ] C. `fr_FR.UTF-8`  
- [ ] D. `UTF-8_fr_FR`

---

### Question 52
Quelle variable d'environnement définit le locale par défaut pour toutes les catégories ?

- [ ] A. `LOCALE`  
- [ ] B. `LANG`  
- [ ] C. `LC_ALL`  
- [ ] D. `LANGUAGE`

---

### Question 53
Quelle variable écrase toutes les autres variables `LC_*` ?

- [ ] A. `LANG`  
- [ ] B. `LC_ALL`  
- [ ] C. `LC_OVERRIDE`  
- [ ] D. `LOCALE_ALL`

---

### Question 54
Comment afficher tous les paramètres régionaux actuels ?

- [ ] A. `locale`  
- [ ] B. `locale -a`  
- [ ] C. `locale -l`  
- [ ] D. `show-locale`

---

### Question 55
Sur un système systemd, quelle commande permet de définir le locale système ?

- [ ] A. `locale set fr_FR.UTF-8`  
- [ ] B. `localectl set-locale LANG=fr_FR.UTF-8`  
- [ ] C. `timedatectl set-locale fr_FR.UTF-8`  
- [ ] D. `set-locale LANG=fr_FR.UTF-8`

---

### Question 56
Quelle commande permet de générer les locales sur Debian/Ubuntu ?

- [ ] A. `locale-gen`  
- [ ] B. `generate-locale`  
- [ ] C. `locale-install`  
- [ ] D. `dpkg-reconfigure locales`

---

### Question 57
Quel est l'encodage de caractères recommandé pour les systèmes Linux modernes ?

- [ ] A. ASCII  
- [ ] B. ISO-8859-1  
- [ ] C. UTF-8  
- [ ] D. UTF-16

---

### Question 58
Quelle commande permet de convertir un fichier de ISO-8859-1 vers UTF-8 ?

- [ ] A. `convert -f ISO-8859-1 -t UTF-8 file.txt`  
- [ ] B. `iconv -f ISO-8859-1 -t UTF-8 file.txt`  
- [ ] C. `encoding change file.txt ISO-8859-1 UTF-8`  
- [ ] D. `recode ISO-8859-1..UTF-8 file.txt`

---

### Question 59
Combien de bytes peut utiliser un caractère UTF-8 au maximum ?

- [ ] A. 1  
- [ ] B. 2  
- [ ] C. 3  
- [ ] D. 4

---

### Question 60
Quelle commande permet de détecter l'encodage d'un fichier ?

- [ ] A. `file -i fichier.txt`  
- [ ] B. `encoding fichier.txt`  
- [ ] C. `charset fichier.txt`  
- [ ] D. `detect-encoding fichier.txt`

---

## ✅ Réponses et Explications

### Objectif 107.1 - Gestion des Comptes Utilisateurs et Groupes

**Question 1 : B**
- `useradd -m michael` crée l'utilisateur et son répertoire personnel grâce à l'option `-m`
- Sans `-m`, le répertoire personnel n'est pas créé (sauf si `CREATE_HOME=yes` dans `/etc/login.defs`)

**Question 2 : B**
- `usermod -a -G developers michael` ajoute le groupe `developers` sans supprimer les groupes existants
- Sans `-a`, l'option `-G` remplacerait tous les groupes secondaires

**Question 3 : C**
- Structure de `/etc/passwd` : `nom:x:UID:GID:GECOS:home:shell`
- Le 3ème champ est l'UID (User ID)

**Question 4 : B**
- `/etc/shadow` contient les mots de passe chiffrés (systèmes avec shadow passwords)
- Lisible uniquement par root pour des raisons de sécurité

**Question 5 : D**
- `passwd -l` verrouille en ajoutant `!` devant le mot de passe dans `/etc/shadow`
- `usermod -L` fait la même chose
- `chage -E 0` définit l'expiration au 1er janvier 1970, désactivant le compte

**Question 6 : B**
- Un mot de passe commençant par `!` indique un compte verrouillé
- L'utilisateur ne peut pas se connecter avec un mot de passe

**Question 7 : A**
- `passwd -x` ↔ `chage -M` : durée de vie maximale du mot de passe
- Autres équivalences : `-n`↔`-m`, `-w`↔`-W`, `-i`↔`-I`

**Question 8 : B**
- `/etc/skel` contient les fichiers copiés dans le répertoire personnel des nouveaux utilisateurs
- Utilisé par `useradd` lors de la création du compte

**Question 9 : B**
- `UID_MIN` et `UID_MAX` définissent la plage des UID pour utilisateurs ordinaires
- Généralement : 1000 - 60000

**Question 10 : D**
- `passwd -S michael` affiche un résumé de l'état du mot de passe
- `chage -l michael` affiche des informations détaillées sur l'expiration

**Question 11 : B**
- `userdel -r michael` supprime l'utilisateur, son répertoire personnel et son spool de courrier
- Sans `-r`, seul le compte est supprimé

**Question 12 : B**
- Structure de `/etc/group` : `nom:x:GID:membres`
- 4 champs séparés par `:`

**Question 13 : C**
- `gpasswd developers` définit le mot de passe du groupe
- Permet aux non-membres de rejoindre le groupe avec `newgrp`

**Question 14 : A**
- `gpasswd -a michael developers` ajoute `michael` au groupe `developers`
- `-A` définit les administrateurs du groupe

**Question 15 : C**
- `getent passwd` interroge la base de données via NSS (Name Service Switch)
- Fonctionne avec LDAP, NIS, fichiers locaux, etc.

**Question 16 : A**
- L'utilisateur root a toujours l'UID 0
- C'est une convention universelle sous Unix/Linux

**Question 17 : A**
- `useradd -M michael` crée l'utilisateur sans répertoire personnel
- Utile pour les comptes système

**Question 18 : D**
- `passwd -e michael` force l'expiration immédiate du mot de passe
- `chage -d 0 michael` définit la date de dernier changement au 1er janvier 1970

**Question 19 : B**
- Structure de `/etc/shadow` (9 champs)
- Champ 6 : jours d'avertissement avant expiration

**Question 20 : A**
- `groupmod -n devteam developers` renomme le groupe
- `-n` = new name

**Question 21 : B**
- `id michael` affiche l'UID, le GID et tous les groupes
- `groups` affiche uniquement les groupes

**Question 22 : D**
- Le groupe primaire est essentiel pour les permissions de fichiers
- Supprimer le groupe primaire rendrait l'utilisateur invalide

**Question 23 : B**
- `/usr/bin/passwd` a le bit SUID activé (`-rwsr-xr-x`)
- Permet aux utilisateurs de changer leur mot de passe avec les privilèges root

**Question 24 : D**
- `passwd -n 10 michael` et `chage -m 10 michael` sont équivalents
- Définit la durée de vie minimale du mot de passe à 10 jours

**Question 25 : B**
- `/etc/gshadow` contient les mots de passe chiffrés des groupes
- Également : administrateurs et membres du groupe

---

### Objectif 107.2 - Automatisation des Tâches

**Question 26 : B**
- Crontab utilisateur : 6 champs (minute, heure, jour du mois, mois, jour de la semaine, commande)
- Crontab système : 7 champs (+ nom d'utilisateur)

**Question 27 : A**
- `0 10 * * *` = minute 0, heure 10, tous les jours
- Exécute le script chaque jour à 10h00

**Question 28 : A**
- `*/15` dans le champ minute = toutes les 15 minutes
- Équivaut à : 0, 15, 30, 45

**Question 29 : B**
- `crontab -e` ouvre l'éditeur pour éditer sa crontab
- N'éditez jamais les fichiers crontab directement

**Question 30 : D**
- `@daily` et `@midnight` sont synonymes
- Équivalent à : `0 0 * * *`

**Question 31 : D**
- Crontab système : 7 champs (ajout du nom d'utilisateur)
- Se trouve dans `/etc/crontab` et `/etc/cron.d/`
- Modifiable uniquement par root

**Question 32 : A**
- `MAILTO=""` (valeur vide) désactive l'envoi d'emails
- Définir en haut de la crontab

**Question 33 : D**
- `/etc/cron.allow` : liste des utilisateurs autorisés
- `/etc/cron.deny` : liste des utilisateurs interdits
- Si `cron.allow` existe, il a la priorité

**Question 34 : B**
- Si `/etc/cron.allow` existe, seuls les utilisateurs listés peuvent utiliser cron
- Les autres sont automatiquement bloqués

**Question 35 : D**
- `30 8 * * 1` et `30 8 * * Mon` sont équivalents
- Lundi = 1 ou Mon (les 3 premières lettres)

**Question 36 : B**
- `at 10:00 tomorrow` planifie une tâche ponctuelle
- `at` est conçu pour les tâches ponctuelles, `cron` pour les tâches récurrentes

**Question 37 : D**
- `at -l` et `atq` sont synonymes
- Affichent les tâches en attente avec leur ID

**Question 38 : D**
- `atrm 12` et `at -d 12` sont synonymes
- Suppriment la tâche numéro 12

**Question 39 : B**
- Le démon `atd` doit être en cours d'exécution
- Vérifier avec `systemctl status atd`

**Question 40 : B**
- La section `[Timer]` contient les options de planification
- `OnCalendar` définit les timers basés sur le calendrier

**Question 41 : A**
- `OnCalendar=*-*-* 08:30:00` = tous les jours à 8h30
- Format : `DayOfWeek Year-Month-Day Hour:Minute:Second`

**Question 42 : A**
- `systemctl list-timers` liste les timers actifs
- Ajouter `--all` pour inclure les inactifs

**Question 43 : B**
- `journalctl -u service-name.service` affiche les logs du service
- Intégration native avec le journal de systemd

**Question 44 : A**
- `weekly` = chaque lundi à minuit
- Équivalent à : `Mon *-*-* 00:00:00`

**Question 45 : A**
- `systemd-run --on-active="5m" date` crée un timer transitoire
- `--on-active` définit un délai relatif

---

### Objectif 107.3 - Paramètres Régionaux et Langues

**Question 46 : C**
- UTC = Universal Time Coordinated (Temps Universel Coordonné)
- Référence mondiale pour les fuseaux horaires

**Question 47 : B**
- `date` affiche la date et l'heure actuelles
- Également utilisée pour définir l'heure (root)

**Question 48 : B**
- `timedatectl set-timezone Europe/Paris` définit le fuseau horaire
- Commande systemd standard

**Question 49 : A**
- `/etc/timezone` contient le nom du fuseau horaire
- Exemple : `Europe/Paris` ou `America/New_York`

**Question 50 : B**
- `TZ` définit le fuseau horaire pour la session
- Priorité sur `/etc/timezone`

**Question 51 : C**
- Format complet : `langue_PAYS.encodage`
- Exemple : `fr_FR.UTF-8`

**Question 52 : B**
- `LANG` définit le locale par défaut pour toutes les catégories
- Valeur de secours si les variables `LC_*` ne sont pas définies

**Question 53 : B**
- `LC_ALL` écrase toutes les autres variables `LC_*` et `LANG`
- À utiliser avec précaution

**Question 54 : A**
- `locale` affiche tous les paramètres régionaux actuels
- `locale -a` liste les locales disponibles

**Question 55 : B**
- `localectl set-locale LANG=fr_FR.UTF-8` définit le locale système
- Commande systemd standard

**Question 56 : A**
- `locale-gen` génère les locales (Debian/Ubuntu)
- Après avoir édité `/etc/locale.gen`

**Question 57 : C**
- UTF-8 est l'encodage universel recommandé
- Compatible ASCII, supporte toutes les langues

**Question 58 : B**
- `iconv -f ISO-8859-1 -t UTF-8 file.txt` convertit l'encodage
- `-f` = from (source), `-t` = to (cible)

**Question 59 : D**
- UTF-8 utilise de 1 à 4 bytes par caractère
- 1 byte pour ASCII, jusqu'à 4 pour les emojis et certains caractères rares

**Question 60 : A**
- `file -i fichier.txt` détecte l'encodage
- Affiche le type MIME et le charset

---

## 📊 Grille de Notation

### Calcul de votre score

- **Questions 1-25 (107.1) :** _____ / 25
- **Questions 26-45 (107.2) :** _____ / 20
- **Questions 46-60 (107.3) :** _____ / 15

**Score total :** _____ / 60

### Interprétation

| Score | Niveau | Recommandation |
|-------|--------|----------------|
| 54-60 | Excellent | Vous maîtrisez le sujet ! Passez au suivant. |
| 48-53 | Bon | Révisez les points faibles identifiés. |
| 42-47 | Moyen | Relisez les notes et refaites le QCM. |
| < 42 | Insuffisant | Reprenez les concepts de base. |

---

## 🎯 Exercices Complémentaires

### Exercice 1 : Scénario Complet Gestion Utilisateurs

Vous êtes administrateur système et devez configurer un environnement pour une nouvelle équipe.

**Tâches :**

1. Créer les groupes `developers`, `designers` et `managers`
2. Créer les utilisateurs suivants :
   - `alice` (groupe primaire : developers, groupes secondaires : managers)
   - `bob` (groupe primaire : designers)
   - `charlie` (groupe primaire : developers)
3. Définir une politique de mot de passe :
   - Durée de vie minimale : 7 jours
   - Durée de vie maximale : 90 jours
   - Avertissement : 14 jours avant expiration
4. Forcer `alice` à changer son mot de passe à la prochaine connexion
5. L'utilisateur `bob` quitte l'entreprise : supprimer son compte et tous ses fichiers
6. Ajouter `charlie` au groupe `designers`

**Commandes attendues :**

```bash
# 1. Créer les groupes
groupadd developers
groupadd designers
groupadd managers

# 2. Créer les utilisateurs
useradd -m -g developers -G managers alice
useradd -m -g designers bob
useradd -m -g developers charlie

# 3. Politique de mot de passe
for user in alice bob charlie; do
    chage -m 7 -M 90 -W 14 $user
done

# 4. Forcer le changement de mot de passe
passwd -e alice
# ou
chage -d 0 alice

# 5. Supprimer bob
userdel -r bob

# 6. Ajouter charlie au groupe designers
usermod -a -G designers charlie
```

### Exercice 2 : Planification de Sauvegardes

Configurer un système de sauvegarde automatique.

**Tâches :**

1. Créer un script de sauvegarde `/usr/local/bin/backup.sh`
2. Le script doit s'exécuter :
   - Tous les jours à 2h30 du matin
   - Rediriger les logs vers `/var/log/backup.log`
   - Ne pas envoyer d'emails sauf en cas d'erreur
3. Créer également une sauvegarde complète le premier dimanche de chaque mois à 3h00

**Solution avec cron :**

```bash
# 1. Créer le script
sudo nano /usr/local/bin/backup.sh

#!/bin/bash
# Script de sauvegarde
date >> /var/log/backup.log
rsync -av /home/ /backup/home/ >> /var/log/backup.log 2>&1
echo "Sauvegarde terminée" >> /var/log/backup.log

# Rendre exécutable
sudo chmod +x /usr/local/bin/backup.sh

# 2. Éditer la crontab système
sudo nano /etc/crontab

# Ajouter :
MAILTO=""
30 2 * * * root /usr/local/bin/backup.sh > /dev/null
0 3 1-7 * Sun root /usr/local/bin/backup.sh > /dev/null
```

**Solution avec systemd timer :**

```bash
# 1. Créer le service
sudo nano /etc/systemd/system/backup.service

[Unit]
Description=Daily Backup Service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/backup.sh

# 2. Créer le timer
sudo nano /etc/systemd/system/backup.timer

[Unit]
Description=Daily Backup Timer

[Timer]
OnCalendar=*-*-* 02:30:00
Persistent=true

[Install]
WantedBy=timers.target

# 3. Activer et démarrer
sudo systemctl daemon-reload
sudo systemctl enable backup.timer
sudo systemctl start backup.timer
```

### Exercice 3 : Configuration Locale et Fuseau Horaire

Configurer un serveur pour une entreprise internationale.

**Tâches :**

1. Définir le fuseau horaire à `Europe/Paris`
2. Configurer le locale système à `fr_FR.UTF-8`
3. Générer également le locale `en_US.UTF-8` pour certaines applications
4. Vérifier que l'horloge système est synchronisée avec NTP
5. Convertir un fichier de documentation `doc.txt` de ISO-8859-1 vers UTF-8

**Commandes attendues :**

```bash
# 1. Fuseau horaire
sudo timedatectl set-timezone Europe/Paris

# 2. Locale système
sudo localectl set-locale LANG=fr_FR.UTF-8

# 3. Générer les locales (Debian/Ubuntu)
sudo locale-gen fr_FR.UTF-8
sudo locale-gen en_US.UTF-8

# 4. Vérifier NTP
timedatectl
# Vérifier : "System clock synchronized: yes"

# 5. Convertir le fichier
iconv -f ISO-8859-1 -t UTF-8 doc.txt -o doc_utf8.txt
```

---

## 📚 Ressources pour Aller Plus Loin

### Commandes à Pratiquer

**Gestion utilisateurs :**
```bash
# Créer un utilisateur complet
useradd -m -c "John Doe" -s /bin/bash -G sudo,developers john

# Voir tous les détails d'un utilisateur
getent passwd john
id john
chage -l john

# Lister tous les utilisateurs
getent passwd | cut -d: -f1

# Lister tous les groupes
getent group | cut -d: -f1
```

**Cron et at :**
```bash
# Voir toutes les crontabs système
cat /etc/crontab
ls -l /etc/cron.d/
ls -l /etc/cron.daily/

# Tester une commande cron
date >> /tmp/test.log

# Simuler une tâche at
at now +1 minute
at> echo "Test" > /tmp/at-test.txt
at> Ctrl+D

atq
# Attendre 1 minute
cat /tmp/at-test.txt
```

**Locales et encodage :**
```bash
# Afficher tous les locales disponibles
locale -a

# Voir les détails d'un locale
locale -ck LC_TIME

# Tester un changement de locale temporaire
LANG=en_US.UTF-8 date
LANG=fr_FR.UTF-8 date

# Détecter l'encodage de plusieurs fichiers
for file in *.txt; do
    echo "$file: $(file -i "$file")"
done
```

### Labs Pratiques Recommandés

1. **KodeKloud - Linux User Management**
2. **Sadservers - Cron Troubleshooting Scenarios**
3. **Linux Academy - Working with Systemd Timers**

### Documentation Officielle

- [LPI 102-500 Exam Objectives](https://www.lpi.org/our-certifications/exam-102-objectives)
- [Systemd Timer Man Pages](https://www.freedesktop.org/software/systemd/man/systemd.timer.html)
- [Cron Format Documentation](https://man7.org/linux/man-pages/man5/crontab.5.html)
- [Unicode and UTF-8](https://www.unicode.org/faq/utf_bom.html)

---

## ✅ Points Clés à Retenir pour l'Examen

### Gestion Utilisateurs (107.1)

1. **useradd/usermod/userdel** sont les 3 commandes principales
2. **-a -G** pour ajouter des groupes sans écraser (très important !)
3. **passwd** et **chage** sont partiellement équivalents pour l'expiration
4. **/etc/shadow** : 9 champs, commence par `!` = compte verrouillé
5. **getent** interroge NSS (pas seulement les fichiers locaux)

### Automatisation (107.2)

1. **Crontab utilisateur** : 6 champs / **Système** : 7 champs (+ utilisateur)
2. **Opérateurs** : `*` (tout), `,` (liste), `-` (plage), `/` (paliers)
3. **Raccourcis** : @hourly, @daily, @weekly, @monthly, @yearly, @reboot
4. **Systemd timers** : Fichiers `.timer` + `.service`, `OnCalendar=`
5. **at** : Planification ponctuelle, atq (lister), atrm (supprimer)

### Locales et Temps (107.3)

1. **UTC** = référence mondiale, **TZ** = variable fuseau horaire
2. **timedatectl** : Outil systemd pour date/heure/fuseau
3. **Locale** : Format `langue_PAYS.encodage` (ex: fr_FR.UTF-8)
4. **LANG** (défaut), **LC_*** (catégories), **LC_ALL** (écrase tout)
5. **UTF-8** : Encodage universel recommandé, **iconv** pour convertir

---

**📌 Fin du QCM - Sujet 107**

💪 Bon courage pour vos révisions et votre examen !
