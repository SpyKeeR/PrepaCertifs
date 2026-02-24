# 📘 Notes de Révision - Sujet 107 : Tâches Administratives

**LPIC-1 Exam 102-500**  
**Poids du sujet : 5 points**

---

## 📋 Table des Matières

1. [Vue d'ensemble du sujet](#vue-densemble-du-sujet)
2. [107.1 - Gestion des comptes utilisateurs et des groupes (Poids : 5)](#1071---gestion-des-comptes-utilisateurs-et-des-groupes)
3. [107.2 - Automatisation des tâches d'administration (Poids : 4)](#1072---automatisation-des-tâches-dadministration)
4. [107.3 - Paramètres régionaux et langues (Poids : 3)](#1073---paramètres-régionaux-et-langues)
5. [Exercices pratiques](#exercices-pratiques)
6. [Checklist de révision](#checklist-de-révision)
7. [Ressources complémentaires](#ressources-complémentaires)

---

## 🎯 Vue d'ensemble du sujet

Le **Sujet 107** couvre les tâches administratives essentielles sous Linux :

| Objectif | Description | Poids |
|----------|-------------|-------|
| **107.1** | Gestion des comptes utilisateurs et des groupes ainsi que des fichiers systèmes concernés | ⭐⭐⭐⭐⭐ (5 pts) |
| **107.2** | Automatisation des tâches d'administration par la planification des travaux | ⭐⭐⭐⭐ (4 pts) |
| **107.3** | Paramètres régionaux et langues | ⭐⭐⭐ (3 pts) |

**Total du sujet : 12 points**

---

## 107.1 - Gestion des comptes utilisateurs et des groupes

### 🎯 Objectifs de cette section

- ✅ Ajouter, modifier et supprimer des utilisateurs et des groupes
- ✅ Gérer les informations associées aux utilisateurs et aux groupes dans les fichiers de bases de données système
- ✅ Créer et gérer de comptes pour des usages spécifiques et limités

### 📚 Concepts Clés

#### 1. Gestion des Utilisateurs

##### Ajouter des utilisateurs

La commande `useradd` permet de créer de nouveaux comptes utilisateurs :

```bash
# Créer un nouvel utilisateur avec configuration par défaut
useradd michael

# Définir le mot de passe
passwd michael

# Vérifier les informations
id michael
groups michael
```

**Options importantes de useradd :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `-c` | Ajouter un commentaire (nom complet) | `useradd -c "Michael User" michael` |
| `-d` | Spécifier le répertoire personnel | `useradd -d /home/custom michael` |
| `-e` | Définir la date d'expiration du compte | `useradd -e 2025-12-31 michael` |
| `-f` | Jours d'inactivité avant désactivation | `useradd -f 7 michael` |
| `-g` | Définir le groupe primaire (GID) | `useradd -g 1000 michael` |
| `-G` | Ajouter à des groupes secondaires | `useradd -G admin,developers michael` |
| `-m` | Créer le répertoire personnel | `useradd -m michael` |
| `-M` | Ne pas créer le répertoire personnel | `useradd -M michael` |
| `-s` | Définir le shell de connexion | `useradd -s /bin/bash michael` |
| `-u` | Spécifier l'UID | `useradd -u 1500 michael` |

💡 **Astuce :** Lorsque vous utilisez `useradd`, les bases de données de mots de passe et de groupes sont automatiquement mises à jour.

##### Modifier des utilisateurs

La commande `usermod` permet de modifier les paramètres d'un compte existant :

```bash
# Changer le shell de connexion
usermod -s /bin/tcsh michael

# Ajouter un commentaire
usermod -c "Michael User Account" michael

# Modifier le répertoire personnel et déplacer les fichiers
usermod -d /home/newdir -m michael

# Ajouter un groupe secondaire (sans supprimer les existants)
usermod -a -G developers michael
```

**Options importantes de usermod :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `-c` | Modifier le commentaire | `usermod -c "New Comment" michael` |
| `-d` | Changer le répertoire personnel | `usermod -d /home/new michael` |
| `-d -m` | Changer et déplacer le répertoire | `usermod -d /home/new -m michael` |
| `-e` | Définir la date d'expiration | `usermod -e 2025-12-31 michael` |
| `-g` | Changer le groupe primaire | `usermod -g developers michael` |
| `-G` | Définir les groupes secondaires | `usermod -G admin,dev michael` |
| `-a -G` | Ajouter des groupes secondaires | `usermod -a -G web michael` |
| `-l` | Changer le nom d'utilisateur | `usermod -l newname michael` |
| `-L` | Verrouiller le compte | `usermod -L michael` |
| `-U` | Déverrouiller le compte | `usermod -U michael` |
| `-s` | Changer le shell | `usermod -s /bin/zsh michael` |
| `-u` | Changer l'UID | `usermod -u 1600 michael` |

⚠️ **Attention :** Lorsque vous modifiez le login d'un utilisateur, vous devez également renommer manuellement son répertoire personnel et ses fichiers de spool de courrier.

##### Supprimer des utilisateurs

La commande `userdel` permet de supprimer un compte utilisateur :

```bash
# Supprimer uniquement le compte
userdel michael

# Supprimer le compte, le répertoire personnel et le spool de courrier
userdel -r michael
```

⚠️ **Important :** Les fichiers situés en dehors du répertoire personnel ne sont pas supprimés automatiquement.

#### 2. Gestion des Groupes

##### Ajouter des groupes

```bash
# Créer un groupe avec GID spécifique
groupadd -g 1090 developer

# Créer un groupe avec GID par défaut
groupadd webdev
```

⚠️ **Rappel :** Les groupes doivent exister avant d'ajouter un utilisateur qui y appartient.

##### Modifier des groupes

```bash
# Renommer un groupe et changer son GID
groupmod -n web-developer -g 1050 developer
```

⚠️ **Attention :** Si vous changez le GID, vous devrez ajuster manuellement les permissions des fichiers appartenant à ce groupe.

##### Supprimer des groupes

```bash
# Supprimer un groupe
groupdel web-developer
```

⚠️ **Limitation :** Vous ne pouvez pas supprimer un groupe s'il est le groupe primaire d'un utilisateur.

#### 3. Fichiers de Configuration

##### Le répertoire squelette (/etc/skel)

Le répertoire `/etc/skel` contient les fichiers et dossiers copiés automatiquement dans le répertoire personnel des nouveaux utilisateurs :

```bash
# Voir le contenu du répertoire squelette
ls -al /etc/skel

# Ajouter un fichier par défaut pour tous les nouveaux utilisateurs
cp .bashrc_custom /etc/skel/
```

💡 **Usage :** Personnalisez `/etc/skel` pour standardiser l'environnement des nouveaux utilisateurs.

##### Le fichier /etc/login.defs

Ce fichier définit les paramètres par défaut pour la création des utilisateurs et des groupes :

**Directives importantes :**

| Directive | Description | Valeur typique |
|-----------|-------------|----------------|
| `UID_MIN` / `UID_MAX` | Plage des UID pour utilisateurs ordinaires | 1000 - 60000 |
| `GID_MIN` / `GID_MAX` | Plage des GID pour groupes ordinaires | 1000 - 60000 |
| `CREATE_HOME` | Créer le répertoire personnel par défaut | yes |
| `USERGROUPS_ENAB` | Créer un groupe par utilisateur | yes |
| `MAIL_DIR` | Répertoire de stockage du courrier | /var/mail |
| `PASS_MAX_DAYS` | Durée de vie maximale du mot de passe | 99999 |
| `PASS_MIN_DAYS` | Durée de vie minimale du mot de passe | 0 |
| `PASS_MIN_LEN` | Longueur minimale du mot de passe | 5 |
| `PASS_WARN_AGE` | Jours d'avertissement avant expiration | 7 |

💡 **Conseil :** Vérifiez toujours `/etc/login.defs` pour comprendre le comportement par défaut du système.

#### 4. Gestion des Mots de Passe

##### La commande passwd

La commande `passwd` permet de gérer les mots de passe et leur expiration :

```bash
# Changer le mot de passe (utilisateur courant)
passwd

# Changer le mot de passe d'un autre utilisateur (root uniquement)
passwd michael

# Vérifier les permissions
ls -l /usr/bin/passwd
# -rwsr-xr-x (bit SUID activé)
```

**Options de passwd :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `-d` | Supprimer le mot de passe (désactiver le compte) | `passwd -d michael` |
| `-e` | Forcer le changement de mot de passe | `passwd -e michael` |
| `-i` | Jours d'inactivité avant désactivation | `passwd -i 7 michael` |
| `-l` | Verrouiller le compte | `passwd -l michael` |
| `-n` | Durée de vie minimale du mot de passe | `passwd -n 10 michael` |
| `-S` | Afficher l'état du mot de passe | `passwd -S michael` |
| `-u` | Déverrouiller le compte | `passwd -u michael` |
| `-x` | Durée de vie maximale du mot de passe | `passwd -x 90 michael` |
| `-w` | Jours d'avertissement avant expiration | `passwd -w 14 michael` |

📝 **Note :** Le bit SUID permet à `passwd` de s'exécuter avec les privilèges de root, permettant aux utilisateurs de changer leur propre mot de passe.

##### La commande chage

La commande `chage` (change age) est dédiée à la gestion de l'expiration des mots de passe :

```bash
# Lister les informations d'expiration (utilisateur courant)
chage -l michael

# Définir la date de dernier changement
chage -d 2025-01-15 michael

# Définir la date d'expiration du compte
chage -E 2025-12-31 michael
```

**Options de chage :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `-d` | Dernier changement de mot de passe | `chage -d 2025-01-15 michael` |
| `-E` | Date d'expiration du compte | `chage -E 2025-12-31 michael` |
| `-I` | Jours d'inactivité avant désactivation | `chage -I 7 michael` |
| `-l` | Lister les informations d'expiration | `chage -l michael` |
| `-m` | Durée de vie minimale du mot de passe | `chage -m 10 michael` |
| `-M` | Durée de vie maximale du mot de passe | `chage -M 90 michael` |
| `-W` | Jours d'avertissement avant expiration | `chage -W 14 michael` |

**Équivalences passwd ↔ chage :**

| passwd | chage | Description |
|--------|-------|-------------|
| `passwd -n` | `chage -m` | Durée de vie minimale |
| `passwd -x` | `chage -M` | Durée de vie maximale |
| `passwd -w` | `chage -W` | Jours d'avertissement |
| `passwd -i` | `chage -I` | Jours d'inactivité |
| `passwd -S` | `chage -l` | Afficher l'état |

#### 5. Fichiers de Bases de Données

##### /etc/passwd

Fichier lisible par tous contenant les informations de base sur les utilisateurs :

**Format (7 champs séparés par `:`) :**

```
username:password:UID:GID:GECOS:home:shell
```

**Exemple :**

```
michael:x:1000:1000:Michael User:/home/michael:/bin/bash
```

**Champs :**

| Champ | Description | Exemple |
|-------|-------------|---------|
| 1 - Nom d'utilisateur | Login de l'utilisateur | `michael` |
| 2 - Mot de passe | `x` si shadow, sinon hash | `x` |
| 3 - UID | Identifiant utilisateur | `1000` |
| 4 - GID | Identifiant du groupe primaire | `1000` |
| 5 - GECOS | Commentaire (nom complet, etc.) | `Michael User` |
| 6 - Répertoire personnel | Chemin absolu | `/home/michael` |
| 7 - Shell | Programme de connexion | `/bin/bash` |

##### /etc/group

Fichier lisible par tous contenant les informations de base sur les groupes :

**Format (4 champs séparés par `:`) :**

```
groupname:password:GID:members
```

**Exemple :**

```
developers:x:1050:michael,emma,dave
```

**Champs :**

| Champ | Description | Exemple |
|-------|-------------|---------|
| 1 - Nom du groupe | Nom du groupe | `developers` |
| 2 - Mot de passe | `x` si shadow, sinon hash | `x` |
| 3 - GID | Identifiant du groupe | `1050` |
| 4 - Membres | Liste des membres (sauf groupe primaire) | `michael,emma,dave` |

##### /etc/shadow

Fichier lisible uniquement par root contenant les mots de passe chiffrés :

**Format (9 champs séparés par `:`) :**

```
username:encrypted_password:last_change:min:max:warn:inactive:expire:reserved
```

**Exemple :**

```
michael:$6$abc123...:18015:10:90:7:14:19000:
```

**Champs :**

| Champ | Description | Valeur |
|-------|-------------|--------|
| 1 - Nom d'utilisateur | Login | `michael` |
| 2 - Mot de passe chiffré | Hash (si commence par `!`, compte verrouillé) | `$6$abc123...` |
| 3 - Dernier changement | Jours depuis 01/01/1970 | `18015` |
| 4 - Âge minimum | Jours minimum entre changements | `10` |
| 5 - Âge maximum | Jours maximum avant changement obligatoire | `90` |
| 6 - Avertissement | Jours d'avertissement avant expiration | `7` |
| 7 - Inactivité | Jours d'inactivité avant désactivation | `14` |
| 8 - Expiration | Jours depuis 01/01/1970 (compte expire) | `19000` |
| 9 - Réservé | Usage futur | (vide) |

💡 **Sécurité :** Le fichier `/etc/shadow` a des permissions `400` ou `600`, accessible uniquement par root.

##### /etc/gshadow

Fichier lisible uniquement par root contenant les mots de passe chiffrés des groupes :

**Format (4 champs séparés par `:`) :**

```
groupname:encrypted_password:admins:members
```

**Exemple :**

```
developers:!:emma:michael,emma,dave
```

**Champs :**

| Champ | Description | Valeur |
|-------|-------------|--------|
| 1 - Nom du groupe | Nom du groupe | `developers` |
| 2 - Mot de passe chiffré | Hash (si `!`, newgrp bloqué) | `!` |
| 3 - Administrateurs | Liste des admins du groupe | `emma` |
| 4 - Membres | Liste des membres | `michael,emma,dave` |

#### 6. Interrogation des Bases de Données

##### Avec grep

```bash
# Rechercher un utilisateur dans /etc/passwd
grep emma /etc/passwd

# Rechercher un groupe dans /etc/group
grep developers /etc/group

# Utiliser cat avec grep
cat /etc/shadow | grep michael
```

##### Avec getent

La commande `getent` permet d'interroger les bases de données NSS (Name Service Switch) :

```bash
# Afficher un utilisateur
getent passwd emma

# Afficher un groupe
getent group developers

# Afficher toutes les entrées
getent passwd        # Tous les utilisateurs
getent group         # Tous les groupes
getent shadow emma   # Info shadow (nécessite root)
```

💡 **Avantage :** `getent` fonctionne avec toutes les sources NSS (LDAP, NIS, etc.), pas seulement les fichiers locaux.

⚠️ **Configuration :** `getent` utilise `/etc/nsswitch.conf` pour déterminer les sources de données.

#### 7. Gestion des Mots de Passe de Groupes

##### La commande gpasswd

```bash
# Définir un mot de passe pour un groupe
gpasswd developers

# Ajouter un utilisateur au groupe
gpasswd -a michael developers

# Supprimer un utilisateur du groupe
gpasswd -d michael developers

# Définir les administrateurs du groupe
gpasswd -A emma,dave developers

# Définir les membres ordinaires
gpasswd -M michael,frank developers
```

##### La commande newgrp

Permet de rejoindre temporairement un groupe (avec mot de passe si nécessaire) :

```bash
# Changer de groupe primaire temporairement
newgrp developers

# Revenir au groupe original
exit
```

### 🔑 Commandes Essentielles

#### Tableau récapitulatif des commandes

| Commande | Description | Exemple |
|----------|-------------|---------|
| `useradd` | Créer un nouveau compte utilisateur | `useradd -m -s /bin/bash michael` |
| `usermod` | Modifier un compte utilisateur | `usermod -a -G developers michael` |
| `userdel` | Supprimer un compte utilisateur | `userdel -r michael` |
| `groupadd` | Créer un nouveau groupe | `groupadd -g 1050 developers` |
| `groupmod` | Modifier un groupe | `groupmod -n webdev developers` |
| `groupdel` | Supprimer un groupe | `groupdel developers` |
| `passwd` | Gérer les mots de passe | `passwd michael` |
| `chage` | Gérer l'expiration des mots de passe | `chage -E 2025-12-31 michael` |
| `getent` | Interroger les bases de données NSS | `getent passwd michael` |
| `gpasswd` | Gérer les mots de passe et membres des groupes | `gpasswd -a michael developers` |
| `newgrp` | Changer de groupe primaire temporairement | `newgrp developers` |
| `id` | Afficher UID, GID et groupes | `id michael` |
| `groups` | Afficher les groupes d'un utilisateur | `groups michael` |

### 💡 Conseils Pratiques

#### Verrouillage de Comptes

**Méthodes pour verrouiller un compte :**

```bash
# Méthode 1 : usermod
usermod -L michael

# Méthode 2 : passwd
passwd -l michael

# Vérification
grep michael /etc/shadow
# Le mot de passe commence par !
```

**Méthodes pour déverrouiller un compte :**

```bash
# Méthode 1 : usermod
usermod -U michael

# Méthode 2 : passwd
passwd -u michael
```

#### Gestion des Groupes Secondaires

```bash
# Ajouter un groupe secondaire (sans supprimer les existants)
usermod -a -G webdev michael

# Remplacer tous les groupes secondaires
usermod -G admin,developers michael

# Supprimer un groupe secondaire (en redéfinissant la liste)
# Si michael est dans admin,developers,webdev et vous voulez retirer webdev :
usermod -G admin,developers michael
```

#### Conventions d'ID

| Type de compte | Plage d'ID | Usage |
|----------------|------------|-------|
| root | 0 | Superutilisateur |
| Comptes système | 1-99 ou 500-999 | Services et démons |
| Utilisateurs ordinaires | ≥ 1000 | Utilisateurs humains |

💡 **Vérification :** Consultez `UID_MIN` et `UID_MAX` dans `/etc/login.defs` pour votre distribution.

---

## 107.2 - Automatisation des tâches d'administration

### 🎯 Objectifs de cette section

- ✅ Gérer les tâches cron et at
- ✅ Configurer les accès aux services cron et atd
- ✅ Comprendre les unités d'horloge systemd (systemd timer units)

### 📚 Concepts Clés

#### 1. Planification avec Cron

##### Qu'est-ce que Cron ?

**Cron** est un démon qui s'exécute en continu et vérifie toutes les minutes s'il y a des tâches à exécuter. Les tâches sont définies dans des fichiers appelés **crontabs** (cron tables).

**Caractéristiques :**
- ✅ Adapté aux systèmes toujours allumés
- ✅ Permet des tâches récurrentes (horaires, quotidiennes, hebdomadaires, etc.)
- ✅ Utilisable par les utilisateurs ordinaires et root
- ⚠️ Les tâches ne s'exécutent que si le système est allumé à l'heure prévue

💡 **Alternative :** **anacron** pour les systèmes qui peuvent être éteints (portables, desktops) - exécute les tâches manquées au prochain démarrage.

##### Structure d'une Crontab Utilisateur

**Emplacement :** `/var/spool/cron/` ou `/var/spool/cron/crontabs/` (selon la distribution)

**Format (6 champs) :**

```
minute heure jour-du-mois mois jour-de-la-semaine commande
```

**Plages de valeurs :**

| Champ | Valeurs | Description |
|-------|---------|-------------|
| **Minute** | 0-59 | Minute de l'heure |
| **Heure** | 0-23 | Heure du jour |
| **Jour du mois** | 1-31 | Jour du mois |
| **Mois** | 1-12 ou jan-dec | Mois de l'année |
| **Jour de la semaine** | 0-7 ou sun-sat | Jour de la semaine (0 et 7 = dimanche) |
| **Commande** | texte | Commande à exécuter |

**Opérateurs :**

| Opérateur | Signification | Exemple |
|-----------|---------------|---------|
| `*` | Toutes les valeurs | `* * * * *` = chaque minute |
| `,` | Liste de valeurs | `0,15,30,45` = 0, 15, 30 et 45 minutes |
| `-` | Plage de valeurs | `1-5` = du lundi au vendredi |
| `/` | Valeurs par paliers | `*/15` = toutes les 15 minutes |

**Exemples pratiques :**

```bash
# Exécuter foo.sh tous les jours à 10h00
0 10 * * * /home/frank/foo.sh

# Exécuter bar.sh tous les mardis à 8h00, 8h15, 8h30, 8h45
0,15,30,45 08 * * 2 /home/frank/bar.sh

# Exécuter foobar.sh à 20h30 du lundi au vendredi, du 1 au 15 janvier et juin
30 20 1-15 1,6 1-5 /home/frank/foobar.sh

# Exécuter une commande toutes les 20 minutes
*/20 * * * * /home/frank/check.sh

# Exécuter le premier jour de chaque mois à minuit
0 0 1 * * /home/frank/monthly.sh
```

##### Structure d'une Crontab Système

**Emplacement :** `/etc/crontab` et `/etc/cron.d/`

**Format (7 champs - ajout du nom d'utilisateur) :**

```
minute heure jour-du-mois mois jour-de-la-semaine utilisateur commande
```

**Exemple :**

```bash
# Exécuter barfoo.sh à 01h30 en tant que root
30 01 * * * root /root/barfoo.sh >>/root/output.log 2>>/root/error.log
```

**Répertoires système pour cron :**

| Répertoire | Fréquence d'exécution |
|------------|----------------------|
| `/etc/cron.hourly/` | Toutes les heures |
| `/etc/cron.daily/` | Tous les jours |
| `/etc/cron.weekly/` | Toutes les semaines |
| `/etc/cron.monthly/` | Tous les mois |

💡 **Usage :** Placez vos scripts directement dans ces répertoires pour une exécution automatique.

##### Raccourcis de Spécifications Horaires

| Raccourci | Équivalent | Description |
|-----------|------------|-------------|
| `@reboot` | - | Au démarrage du système |
| `@hourly` | `0 * * * *` | Chaque heure (minute 0) |
| `@daily` ou `@midnight` | `0 0 * * *` | Chaque jour à minuit |
| `@weekly` | `0 0 * * 0` | Chaque dimanche à minuit |
| `@monthly` | `0 0 1 * *` | Le 1er de chaque mois à minuit |
| `@yearly` ou `@annually` | `0 0 1 1 *` | Le 1er janvier à minuit |

**Exemples :**

```bash
@hourly /home/frank/backup.sh
@daily /usr/local/bin/cleanup.sh
@reboot /home/frank/startup.sh
```

##### Variables d'Environnement Crontab

Vous pouvez définir des variables d'environnement en haut d'un fichier crontab :

```bash
HOME=/home/frank
MAILTO=admin@example.com
PATH=/usr/local/bin:/usr/bin:/bin
SHELL=/bin/bash

# Tâches cron
0 10 * * * /home/frank/foo.sh
```

**Variables courantes :**

| Variable | Description | Valeur par défaut |
|----------|-------------|-------------------|
| `HOME` | Répertoire où cron invoque les commandes | Répertoire personnel de l'utilisateur |
| `MAILTO` | Destinataire des sorties (vide = pas d'email) | Propriétaire de la crontab |
| `PATH` | Chemin de recherche des commandes | `/usr/bin:/bin` |
| `SHELL` | Shell à utiliser | `/bin/sh` |

##### Gestion des Crontabs Utilisateur

**Créer/Éditer une crontab :**

```bash
# Ouvrir l'éditeur pour éditer sa crontab
crontab -e

# Première utilisation : choix de l'éditeur
Select an editor:
  1. /bin/nano
  2. /usr/bin/vim
Choose 1-2 [1]: 1
```

**Autres commandes crontab :**

```bash
# Lister sa crontab actuelle
crontab -l

# Supprimer sa crontab
crontab -r

# Éditer la crontab d'un autre utilisateur (root uniquement)
crontab -u michael -e
```

⚠️ **Important :** N'éditez jamais les fichiers crontab directement. Utilisez toujours `crontab -e`.

##### Gestion des Crontabs Système

```bash
# Éditer /etc/crontab avec un éditeur
sudo nano /etc/crontab

# Ajouter un fichier dans /etc/cron.d/
sudo nano /etc/cron.d/mon-script
```

**Exemple de /etc/crontab :**

```bash
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h  dom mon dow   user    command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || run-parts --report /etc/cron.daily
47 6    * * 7   root    test -x /usr/sbin/anacron || run-parts --report /etc/cron.weekly
52 6    1 * *   root    test -x /usr/sbin/anacron || run-parts --report /etc/cron.monthly
```

##### Redirection de la Sortie

```bash
# Rediriger la sortie vers un fichier
30 01 * * * root /root/script.sh >> /root/output.log 2>> /root/error.log

# Rediriger uniquement stdout vers /dev/null (recevoir les erreurs par email)
30 01 * * * root /root/script.sh > /dev/null

# Ne rien recevoir par email
30 01 * * * root /root/script.sh > /dev/null 2>&1
```

💡 **Conseil :** Redirigez toujours la sortie pour éviter de recevoir des emails pour chaque exécution.

##### Contrôle d'Accès à Cron

**Fichiers de contrôle :**

| Fichier | Description |
|---------|-------------|
| `/etc/cron.allow` | Liste des utilisateurs autorisés (si existe) |
| `/etc/cron.deny` | Liste des utilisateurs interdits (si allow n'existe pas) |

**Logique de contrôle :**

1. Si `/etc/cron.allow` existe → Seuls les utilisateurs listés peuvent utiliser cron
2. Sinon, si `/etc/cron.deny` existe → Tous sauf ceux listés peuvent utiliser cron
3. Si `/etc/cron.deny` est vide → Tous les utilisateurs peuvent utiliser cron
4. Si aucun fichier n'existe → Dépend de la distribution

**Format :**

```bash
# Un nom d'utilisateur par ligne
michael
emma
dave
```

#### 2. Alternative à Cron : Systemd Timers

##### Qu'est-ce qu'un Timer Systemd ?

Les **timers** sont des unités systemd (fichiers `.timer`) qui permettent de planifier l'exécution de services. Ils sont une alternative moderne à cron.

**Avantages :**
- ✅ Intégration avec systemd
- ✅ Journalisation avec `journalctl`
- ✅ Gestion avec `systemctl`
- ✅ Timers monotoniques (relatifs au démarrage)
- ✅ Persistance des tâches manquées

##### Structure d'un Timer

**Fichier timer :** `/etc/systemd/system/foobar.timer`

```ini
[Unit]
Description=Run the foobar service

[Timer]
OnCalendar=Mon *-*-1..7 05:30:00
Persistent=true

[Install]
WantedBy=timers.target
```

**Fichier service correspondant :** `/etc/systemd/system/foobar.service`

```ini
[Unit]
Description=Foobar Service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/foobar.sh
```

##### Syntaxe OnCalendar

**Format complet :**

```
DayOfWeek Year-Month-Day Hour:Minute:Second
```

**Exemples :**

| Spécification | Description |
|---------------|-------------|
| `*-*-* 08:30:00` | Tous les jours à 08h30 |
| `Mon *-*-* 10:00:00` | Chaque lundi à 10h00 |
| `*-*-01 00:00:00` | Le 1er de chaque mois à minuit |
| `Mon,Fri *-*-* 14:00:00` | Lundi et vendredi à 14h00 |
| `*-01-01 00:00:00` | Le 1er janvier à minuit |
| `Sat,Sun *-*-* 05:00:00` | Samedi et dimanche à 05h00 |
| `*-*-* *:00/05:00` | Toutes les 5 minutes |

**Raccourcis OnCalendar :**

| Raccourci | Équivalent | Description |
|-----------|------------|-------------|
| `hourly` | `*-*-* *:00:00` | Toutes les heures |
| `daily` | `*-*-* 00:00:00` | Tous les jours à minuit |
| `weekly` | `Mon *-*-* 00:00:00` | Chaque lundi à minuit |
| `monthly` | `*-*-01 00:00:00` | Le 1er de chaque mois |
| `yearly` | `*-01-01 00:00:00` | Le 1er janvier |

##### Gestion des Timers

```bash
# Activer un timer (démarrage automatique au boot)
systemctl enable foobar.timer

# Démarrer un timer immédiatement
systemctl start foobar.timer

# Vérifier l'état d'un timer
systemctl status foobar.timer

# Lister tous les timers actifs
systemctl list-timers

# Lister tous les timers (actifs et inactifs)
systemctl list-timers --all

# Recharger la configuration après modification
systemctl daemon-reload

# Arrêter un timer
systemctl stop foobar.timer

# Désactiver un timer
systemctl disable foobar.timer
```

##### Timers Monotoniques

Les timers monotoniques s'activent après un délai relatif à un point de départ :

```ini
[Timer]
# 5 minutes après le démarrage du système
OnBootSec=5min

# 10 minutes après l'activation du timer
OnActiveSec=10min

# 1 heure après la fin de la dernière exécution
OnUnitActiveSec=1h
```

**Options monotoniques :**

| Option | Point de départ |
|--------|----------------|
| `OnBootSec` | Démarrage du système |
| `OnStartupSec` | Démarrage de systemd |
| `OnActiveSec` | Activation du timer |
| `OnUnitActiveSec` | Dernière activation du service |
| `OnUnitInactiveSec` | Dernière désactivation du service |

##### Journalisation des Timers

```bash
# Voir les logs d'un timer
journalctl -u foobar.timer

# Voir les logs d'un service déclenché par un timer
journalctl -u foobar.service

# Suivre les logs en temps réel
journalctl -u foobar.service -f

# Logs depuis le dernier démarrage
journalctl -u foobar.timer --boot
```

💡 **Avantage :** Intégration native avec le système de journalisation de systemd.

#### 3. Planification Ponctuelle avec at

##### Qu'est-ce que at ?

**at** permet de planifier l'exécution d'une commande à un moment précis dans le futur (une seule fois).

**Caractéristiques :**
- ✅ Exécution ponctuelle (pas récurrente)
- ✅ Utilisable par les utilisateurs ordinaires
- ✅ Sorties envoyées par email par défaut
- ⚠️ Nécessite le démon `atd` en cours d'exécution

💡 **Alternative :** **batch** pour exécuter une tâche lorsque la charge système est basse.

##### Utilisation de base

```bash
# Planifier une tâche dans 5 minutes
at now +5 minutes
warning: commands will be executed using /bin/sh
at> date
at> Ctrl+D
job 12 at Sat Sep 14 09:15:00 2019

# Planifier une tâche à une heure précise
at 09:30 AM
at> ./foo.sh
at> Ctrl+D
job 13 at Sat Sep 14 09:30:00 2019

# Planifier une tâche dans 2 heures
at now +2 hours
at> ./bar.sh
at> Ctrl+D
job 14 at Sat Sep 14 11:10:00 2019
```

##### Options de at

| Option | Description | Exemple |
|--------|-------------|---------|
| `-c` | Afficher les commandes d'une tâche | `at -c 12` |
| `-d` | Supprimer une tâche (alias de atrm) | `at -d 12` |
| `-f` | Lire les commandes depuis un fichier | `at -f script.sh 10:00` |
| `-l` | Lister les tâches (alias de atq) | `at -l` |
| `-m` | Envoyer un email même sans sortie | `at -m 10:00` |
| `-q` | Spécifier une file d'attente (a-z, A-Z) | `at -q b 10:00` |
| `-v` | Afficher l'heure d'exécution prévue | `at -v 10:00` |

##### Spécifications Horaires pour at

**Formats d'heure :**

```bash
# Format HH:MM (12 ou 24 heures)
at 08:30
at 08:30 AM
at 08:30 PM
at 20:30
```

**Formats de date :**

```bash
# nom-du-mois jour-du-mois [année]
at 10:00 January 15
at 10:00 Jan 15 2025

# MMDDYY, MM/DD/YY, DD.MM.YY, YYYY-MM-DD
at 10:00 011525
at 10:00 01/15/25
at 10:00 15.01.25
at 10:00 2025-01-15
```

**Mots-clés temporels :**

| Mot-clé | Description | Exemple |
|---------|-------------|---------|
| `midnight` | Minuit | `at midnight` |
| `noon` | Midi | `at noon` |
| `teatime` | 16h00 | `at teatime` |
| `now` | Maintenant | `at now +30 minutes` |
| `today` | Aujourd'hui | `at 10:00 today` |
| `tomorrow` | Demain | `at 10:00 tomorrow` |
| `next week` | Semaine prochaine | `at 10:00 next week` |

**Unités de temps relatif :**

```bash
at now +5 minutes
at now +2 hours
at now +3 days
at now +1 week
```

**Exemples complets :**

```bash
# Le 31 octobre à 10h30
at 10:30 AM October 31

# Demain à 10h00
at 10:00 AM tomorrow

# Dans 30 minutes
at now +30 minutes

# Le 1er janvier 2025 à 07h15
at 07:15 AM Jan 01 2025
```

##### Lister les tâches : atq

```bash
# Lister toutes les tâches en attente
atq

# Exemple de sortie
14 Sat Sep 14 11:10:00 2019 a frank
13 Sat Sep 14 09:30:00 2019 a frank
12 Sat Sep 14 09:15:00 2019 a frank
```

**Format de sortie :**

```
ID date heure année file_d'attente utilisateur
```

💡 **Note :** Root peut voir les tâches de tous les utilisateurs.

##### Supprimer des tâches : atrm

```bash
# Supprimer une tâche
atrm 14

# Supprimer plusieurs tâches
atrm 12 13 14
```

💡 **Note :** Root peut supprimer les tâches de tous les utilisateurs.

##### Contrôle d'Accès à at

**Fichiers de contrôle :**

| Fichier | Description |
|---------|-------------|
| `/etc/at.allow` | Liste des utilisateurs autorisés (si existe) |
| `/etc/at.deny` | Liste des utilisateurs interdits (si allow n'existe pas) |

**Logique de contrôle :**

1. Si `/etc/at.allow` existe → Seuls les utilisateurs listés peuvent utiliser at
2. Sinon, si `/etc/at.deny` existe → Tous sauf ceux listés peuvent utiliser at
3. Si `/etc/at.deny` est vide → Tous les utilisateurs peuvent utiliser at
4. Si aucun fichier n'existe → Dépend de la distribution

**Format :** Identique à cron (un nom d'utilisateur par ligne)

#### 4. Alternative à at : systemd-run

##### Qu'est-ce que systemd-run ?

**systemd-run** permet de créer des timers transitoires pour exécuter des commandes ponctuelles sans créer de fichiers de service.

```bash
# Exécuter date à une heure précise (root)
systemd-run --on-calendar='2025-10-06 11:30' date

# Exécuter foo.sh dans 2 minutes
systemd-run --on-active="2m" ./foo.sh

# Exécuter avec un utilisateur spécifique
systemd-run --on-calendar='2025-10-06 11:30' --uid=michael date
```

**Options principales :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `--on-calendar` | Timer basé sur le calendrier | `--on-calendar='2025-01-01 10:00'` |
| `--on-active` | Timer monotonique (délai) | `--on-active="10m"` |
| `--uid` | Utilisateur qui exécute | `--uid=michael` |
| `--unit` | Nom de l'unité créée | `--unit=mon-timer` |

💡 **Avantage :** Pas besoin de créer des fichiers de service, tout est géré en ligne de commande.

### 🔑 Commandes Essentielles

#### Tableau récapitulatif des commandes

| Commande | Description | Exemple |
|----------|-------------|---------|
| `crontab -e` | Éditer sa crontab | `crontab -e` |
| `crontab -l` | Lister sa crontab | `crontab -l` |
| `crontab -r` | Supprimer sa crontab | `crontab -r` |
| `crontab -u` | Gérer la crontab d'un autre utilisateur | `crontab -u michael -e` |
| `at` | Planifier une tâche ponctuelle | `at 10:00 tomorrow` |
| `atq` | Lister les tâches at | `atq` |
| `atrm` | Supprimer une tâche at | `atrm 12` |
| `systemctl enable` | Activer un timer | `systemctl enable foobar.timer` |
| `systemctl start` | Démarrer un timer | `systemctl start foobar.timer` |
| `systemctl list-timers` | Lister les timers | `systemctl list-timers` |
| `systemd-run` | Créer un timer transitoire | `systemd-run --on-active="5m" date` |
| `journalctl` | Voir les logs d'un timer/service | `journalctl -u foobar.timer` |

### 💡 Conseils Pratiques

#### Comparaison Cron vs Systemd Timers

| Critère | Cron | Systemd Timers |
|---------|------|----------------|
| **Simplicité** | ✅ Syntaxe simple | ⚠️ Plus complexe |
| **Journalisation** | ⚠️ Par email ou fichier | ✅ Intégré avec journalctl |
| **Gestion** | ⚠️ Fichiers texte | ✅ systemctl |
| **Persistance** | ❌ Tâche manquée = perdue | ✅ Persistent=true |
| **Granularité** | ⚠️ Minimum 1 minute | ✅ À la seconde près |
| **Portabilité** | ✅ Universel | ⚠️ Nécessite systemd |

#### Déboguer les Tâches Cron

```bash
# Vérifier que cron fonctionne
systemctl status cron    # Debian/Ubuntu
systemctl status crond   # RHEL/CentOS

# Voir les logs de cron
grep CRON /var/log/syslog
journalctl -u cron

# Tester une commande avant de la mettre dans cron
bash -c "commande"

# Vérifier les permissions d'exécution
chmod +x /home/frank/script.sh
```

#### Permissions Spéciales

```bash
# Vérifier les permissions de crontab
ls -l /usr/bin/crontab
# -rwxr-sr-x (bit SGID)

# Vérifier les permissions de at
ls -l /usr/bin/at
# -rwsr-sr-x (bits SUID et SGID)
```

💡 **Explication :** Les bits SUID/SGID permettent à ces commandes de s'exécuter avec des privilèges élevés pour accéder aux fichiers de planification.

---

## 107.3 - Paramètres régionaux et langues

### 🎯 Objectifs de cette section

- ✅ Configuration de l'environnement linguistique et des variables d'environnement correspondantes
- ✅ Configuration du fuseau horaire et des variables d'environnement correspondantes
- ✅ Comprendre l'encodage des caractères (UTF-8, ISO-8859, ASCII, Unicode)

### 📚 Concepts Clés

#### 1. Les Fuseaux Horaires

##### Qu'est-ce qu'un Fuseau Horaire ?

Les **fuseaux horaires** sont des zones de la surface terrestre qui partagent la même heure locale. Ils sont définis par rapport au **Temps Universel Coordonné (UTC)**.

**Concepts importants :**

| Terme | Description |
|-------|-------------|
| **UTC** | Temps Universel Coordonné (référence mondiale) |
| **GMT** | Greenwich Mean Time (synonyme d'UTC dans les noms de fuseaux) |
| **Décalage** | Différence avec UTC (ex: GMT-5, GMT+3) |
| **Nom descriptif** | Basé sur une localité (ex: Europe/Paris, America/New_York) |

**Exemples de décalages :**

```
GMT-5  → 5 heures de retard sur UTC (ex: New York en hiver)
GMT+0  → Heure UTC (ex: Londres, Lisbonne)
GMT+1  → 1 heure d'avance sur UTC (ex: Paris en hiver)
GMT+3  → 3 heures d'avance sur UTC (ex: Moscou)
```

##### Afficher la Date et l'Heure

**Avec la commande date :**

```bash
# Afficher la date et l'heure actuelles
date

# Exemple de sortie
Mon Oct 21 10:45:21 -03 2019
```

**Décryptage :** `-03` indique un décalage de -3 heures par rapport à UTC (fuseau GMT-3).

**Avec la commande timedatectl (systemd) :**

```bash
# Afficher des informations détaillées
timedatectl

# Exemple de sortie
               Local time: Sat 2019-10-19 17:53:18 -03
           Universal time: Sat 2019-10-19 20:53:18 UTC
                 RTC time: Sat 2019-10-19 20:53:18
                Time zone: America/Sao_Paulo (-03, -0300)
System clock synchronized: yes
NTP service: active
    RTC in local TZ: no
```

**Informations fournies :**

| Champ | Description |
|-------|-------------|
| `Local time` | Heure locale du système |
| `Universal time` | Heure UTC |
| `RTC time` | Heure de l'horloge matérielle (Real-Time Clock) |
| `Time zone` | Fuseau horaire actuel |
| `System clock synchronized` | Synchronisation avec NTP |
| `NTP service` | État du service de synchronisation |
| `RTC in local TZ` | Horloge matérielle en heure locale ou UTC |

##### Configuration du Fuseau Horaire

**Fichiers de configuration :**

| Fichier | Description |
|---------|-------------|
| `/etc/timezone` | Définit le fuseau horaire par défaut du système |
| `/etc/localtime` | Lien symbolique vers le fichier de fuseau horaire |
| `/usr/share/zoneinfo/` | Répertoire contenant tous les fuseaux horaires |

**Voir le fuseau horaire configuré :**

```bash
# Méthode 1 : Lire /etc/timezone
cat /etc/timezone
# Sortie: America/Sao_Paulo

# Méthode 2 : Vérifier le lien symbolique
ls -l /etc/localtime
# lrwxrwxrwx 1 root root 36 Oct 19 /etc/localtime -> /usr/share/zoneinfo/America/Sao_Paulo
```

**Changer le fuseau horaire (méthode manuelle) :**

```bash
# Créer un lien symbolique vers le nouveau fuseau
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime

# Mettre à jour /etc/timezone
echo "Europe/Paris" > /etc/timezone
```

**Changer le fuseau horaire (méthode timedatectl) :**

```bash
# Lister tous les fuseaux horaires disponibles
timedatectl list-timezones

# Définir un nouveau fuseau horaire
timedatectl set-timezone Europe/Paris

# Vérifier le changement
timedatectl
```

##### Sélection Interactive : tzselect

La commande `tzselect` guide l'utilisateur de manière interactive pour trouver le bon fuseau horaire :

```bash
# Lancer tzselect
tzselect
```

**Exemple d'utilisation :**

```
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the time zone using the Posix TZ format.
#? 7

Please select a country whose clocks agree with yours.
 1) Åland Islands   18) Greece          35) Norway
 2) Albania         19) Guernsey        36) Poland
 3) Andorra         20) Hungary         37) Portugal
 4) Austria         21) Ireland         38) Romania
 5) Belarus         22) Isle of Man     39) Russia
 6) Belgium         23) Italy           40) San Marino
 7) Bosnia & Herzegovina  24) Jersey    41) Serbia
 8) Britain (UK)    25) Latvia          42) Slovakia
 9) Bulgaria        26) Liechtenstein   43) Slovenia
10) Croatia         27) Lithuania       44) Spain
11) Czech Republic  28) Luxembourg      45) Svalbard & Jan Mayen
12) Denmark         29) Macedonia       46) Sweden
13) Estonia         30) Malta           47) Switzerland
14) Finland         31) Moldova         48) Turkey
15) France          32) Monaco          49) Ukraine
16) Germany         33) Montenegro      50) Vatican City
17) Gibraltar       34) Netherlands
#? 15

The following information has been given:
        France
Therefore TZ='Europe/Paris' will be used.
Selected time is now:   Sat Oct 19 22:53:18 CEST 2019.
Universal Time is now:  Sat Oct 19 20:53:18 UTC 2019.
Is the above information OK?
1) Yes
2) No
#? 1

You can make this change permanent for yourself by appending the line
        TZ='Europe/Paris'; export TZ
to the file '.profile' in your home directory; then log out and log in again.
```

💡 **Résultat :** `tzselect` affiche le nom du fuseau horaire (ex: `Europe/Paris`) que vous pouvez utiliser dans `/etc/timezone` ou dans la variable `TZ`.

##### Variable d'Environnement TZ

La variable `TZ` permet de définir le fuseau horaire pour une session ou un utilisateur :

```bash
# Définir TZ pour la session actuelle
export TZ='Europe/Paris'
date

# Définir TZ temporairement pour une commande
env TZ='America/New_York' date

# Rendre le changement permanent pour un utilisateur
echo "TZ='Europe/Paris'; export TZ" >> ~/.profile
```

**Priorité :** La variable `TZ` a la priorité sur `/etc/timezone` pour la session en cours.

##### Heure d'Été (Daylight Saving Time)

De nombreux pays adoptent l'heure d'été, où les horloges sont avancées d'une heure pendant une partie de l'année.

💡 **Gestion automatique :** Les fichiers de fuseaux horaires dans `/usr/share/zoneinfo/` contiennent les règles d'heure d'été. Le système ajuste automatiquement l'heure si le fuseau horaire est correctement configuré.

**Vérification :**

```bash
# Voir les transitions d'heure d'été
zdump -v Europe/Paris | grep 2025
```

#### 2. Paramètres Régionaux (Locales)

##### Qu'est-ce qu'un Locale ?

Un **locale** définit les conventions culturelles et linguistiques d'une région :

- 🌍 Langue de l'interface
- 📅 Format de date et heure
- 💰 Format de devise
- 🔢 Format de nombres
- 📏 Unités de mesure
- ✉️ Encodage des caractères

**Format d'un locale :**

```
langue_PAYS.encodage
```

**Exemples :**

```
fr_FR.UTF-8      → Français (France), UTF-8
en_US.UTF-8      → Anglais (États-Unis), UTF-8
de_DE.UTF-8      → Allemand (Allemagne), UTF-8
pt_BR.UTF-8      → Portugais (Brésil), UTF-8
ja_JP.UTF-8      → Japonais (Japon), UTF-8
```

##### Variables d'Environnement Locales

**Variables LC_* :**

| Variable | Description | Exemple |
|----------|-------------|---------|
| `LANG` | Locale par défaut pour toutes les catégories | `fr_FR.UTF-8` |
| `LC_COLLATE` | Ordre de tri des chaînes | `fr_FR.UTF-8` |
| `LC_CTYPE` | Classification et conversion des caractères | `fr_FR.UTF-8` |
| `LC_MESSAGES` | Langue des messages du système | `fr_FR.UTF-8` |
| `LC_MONETARY` | Format de devise | `fr_FR.UTF-8` |
| `LC_NUMERIC` | Format de nombres | `fr_FR.UTF-8` |
| `LC_TIME` | Format de date et heure | `fr_FR.UTF-8` |
| `LC_PAPER` | Format de papier | `fr_FR.UTF-8` |
| `LC_ALL` | Écrase toutes les autres variables LC_* | `fr_FR.UTF-8` |

**Hiérarchie des variables :**

1. `LC_ALL` (priorité absolue, écrase tout)
2. Variables `LC_*` individuelles
3. `LANG` (valeur par défaut)

💡 **Conseil :** Évitez d'utiliser `LC_ALL` sauf pour des tests temporaires. Préférez `LANG` et les variables `LC_*` individuelles.

##### Afficher les Locales Actuels

**Avec la commande locale :**

```bash
# Afficher tous les paramètres régionaux actuels
locale

# Exemple de sortie
LANG=fr_FR.UTF-8
LANGUAGE=
LC_CTYPE="fr_FR.UTF-8"
LC_NUMERIC="fr_FR.UTF-8"
LC_TIME="fr_FR.UTF-8"
LC_COLLATE="fr_FR.UTF-8"
LC_MONETARY="fr_FR.UTF-8"
LC_MESSAGES="fr_FR.UTF-8"
LC_PAPER="fr_FR.UTF-8"
LC_NAME="fr_FR.UTF-8"
LC_ADDRESS="fr_FR.UTF-8"
LC_TELEPHONE="fr_FR.UTF-8"
LC_MEASUREMENT="fr_FR.UTF-8"
LC_IDENTIFICATION="fr_FR.UTF-8"
LC_ALL=

# Lister tous les locales disponibles
locale -a

# Afficher les informations sur un locale spécifique
locale -ck LC_TIME
```

##### Configurer les Locales

**Méthode 1 : Variables d'environnement temporaires**

```bash
# Définir pour la session actuelle
export LANG=fr_FR.UTF-8
export LC_TIME=en_US.UTF-8

# Vérifier
locale
```

**Méthode 2 : Configuration permanente (fichiers utilisateur)**

```bash
# Ajouter au fichier ~/.bashrc ou ~/.profile
echo 'export LANG=fr_FR.UTF-8' >> ~/.bashrc
echo 'export LC_TIME=en_US.UTF-8' >> ~/.bashrc

# Recharger la configuration
source ~/.bashrc
```

**Méthode 3 : Configuration système (systemd)**

```bash
# Utiliser localectl pour définir le locale système
localectl set-locale LANG=fr_FR.UTF-8

# Vérifier la configuration
localectl status

# Définir plusieurs variables
localectl set-locale LANG=fr_FR.UTF-8 LC_TIME=en_US.UTF-8
```

**Fichiers de configuration système :**

| Fichier | Description |
|---------|-------------|
| `/etc/locale.conf` | Configuration des locales système (systemd) |
| `/etc/default/locale` | Configuration des locales système (Debian/Ubuntu) |

##### Générer de Nouveaux Locales

Certaines distributions nécessitent de générer les locales avant de les utiliser :

```bash
# Debian/Ubuntu : Éditer /etc/locale.gen
sudo nano /etc/locale.gen
# Décommenter les locales souhaités (ex: fr_FR.UTF-8 UTF-8)

# Générer les locales
sudo locale-gen

# Ou directement générer un locale spécifique
sudo locale-gen fr_FR.UTF-8

# Mettre à jour les locales
sudo update-locale LANG=fr_FR.UTF-8
```

**Red Hat/CentOS :**

```bash
# Installer le paquet de langue
sudo yum install glibc-langpack-fr

# Configurer avec localectl
sudo localectl set-locale LANG=fr_FR.UTF-8
```

#### 3. Encodage des Caractères

##### Qu'est-ce qu'un Encodage de Caractères ?

Un **encodage de caractères** définit comment les caractères de texte sont représentés en nombres (bytes) dans l'ordinateur.

**Principaux encodages :**

| Encodage | Description | Caractéristiques |
|----------|-------------|------------------|
| **ASCII** | American Standard Code for Information Interchange | 7 bits, 128 caractères (0-127) |
| **ISO-8859-1** (Latin-1) | Extension d'ASCII pour les langues européennes occidentales | 8 bits, 256 caractères |
| **ISO-8859-15** (Latin-9) | Variante d'ISO-8859-1 avec € et autres | 8 bits, 256 caractères |
| **UTF-8** | Unicode Transformation Format - 8 bits | Longueur variable (1-4 bytes), compatible ASCII |
| **UTF-16** | Unicode Transformation Format - 16 bits | Longueur variable (2 ou 4 bytes) |
| **UTF-32** | Unicode Transformation Format - 32 bits | Longueur fixe (4 bytes) |

##### ASCII

- **Taille :** 7 bits (valeurs 0-127)
- **Caractères :** Alphabet anglais, chiffres, ponctuation, caractères de contrôle
- **Limites :** Pas de caractères accentués (é, à, ö, ñ, etc.)

**Exemple :**

```
A = 65 (décimal) = 01000001 (binaire)
a = 97 (décimal) = 01100001 (binaire)
0 = 48 (décimal) = 00110000 (binaire)
```

##### ISO-8859 (Latin)

**Famille d'encodages 8 bits :**

| Encodage | Description |
|----------|-------------|
| ISO-8859-1 (Latin-1) | Europe occidentale (français, allemand, espagnol, etc.) |
| ISO-8859-2 (Latin-2) | Europe centrale et orientale |
| ISO-8859-5 | Cyrillique (russe, bulgare, etc.) |
| ISO-8859-15 (Latin-9) | Variante de Latin-1 avec € et Œ, œ |

**Caractéristiques :**
- ✅ Compatible ASCII (premiers 128 caractères identiques)
- ✅ 256 caractères au total
- ⚠️ Limité à une région linguistique
- ⚠️ Incompatible entre variantes (Latin-1 ≠ Latin-2)

##### Unicode et UTF-8

**Unicode :** Norme universelle qui assigne un numéro unique (point de code) à chaque caractère de toutes les langues du monde.

**UTF-8 :** Encodage à longueur variable pour représenter Unicode :

**Avantages de UTF-8 :**
- ✅ Compatible ASCII (caractères ASCII = 1 byte)
- ✅ Supporte toutes les langues du monde
- ✅ Longueur variable (1-4 bytes) → Efficace pour textes principalement ASCII
- ✅ Standard moderne recommandé pour Linux

**Longueur des caractères UTF-8 :**

| Plage Unicode | Bytes UTF-8 | Exemple |
|---------------|-------------|---------|
| U+0000 - U+007F | 1 byte | A, 0, ! |
| U+0080 - U+07FF | 2 bytes | é, ñ, ö |
| U+0800 - U+FFFF | 3 bytes | 中, 日, 本 |
| U+10000 - U+10FFFF | 4 bytes | 😀, 🚀, 🎉 |

**Exemple :**

```
Caractère  Unicode    UTF-8 (hex)
A          U+0041     41
é          U+00E9     C3 A9
中         U+4E2D     E4 B8 AD
😀         U+1F600    F0 9F 98 80
```

💡 **Recommandation :** Utilisez **UTF-8** pour tous les nouveaux systèmes et fichiers.

##### Conversion d'Encodage : iconv

La commande `iconv` permet de convertir des fichiers entre différents encodages :

```bash
# Convertir de ISO-8859-1 vers UTF-8
iconv -f ISO-8859-1 -t UTF-8 fichier_latin1.txt > fichier_utf8.txt

# Lister tous les encodages disponibles
iconv -l

# Convertir en remplaçant le fichier original
iconv -f ISO-8859-15 -t UTF-8 fichier.txt -o fichier.txt
```

**Options de iconv :**

| Option | Description | Exemple |
|--------|-------------|---------|
| `-f` | Encodage source (from) | `-f ISO-8859-1` |
| `-t` | Encodage cible (to) | `-t UTF-8` |
| `-o` | Fichier de sortie | `-o output.txt` |
| `-l` | Lister les encodages | `iconv -l` |
| `-c` | Ignorer les caractères invalides | `-c` |

**Exemples pratiques :**

```bash
# Convertir un fichier Windows-1252 vers UTF-8
iconv -f WINDOWS-1252 -t UTF-8 document.txt > document_utf8.txt

# Convertir plusieurs fichiers
for file in *.txt; do
    iconv -f ISO-8859-1 -t UTF-8 "$file" -o "utf8_$file"
done

# Vérifier l'encodage d'un fichier (avec file)
file -i fichier.txt
# fichier.txt: text/plain; charset=utf-8
```

### 🔑 Commandes Essentielles

#### Tableau récapitulatif des commandes

| Commande | Description | Exemple |
|----------|-------------|---------|
| `date` | Afficher la date et l'heure | `date` |
| `timedatectl` | Gérer date, heure et fuseau horaire (systemd) | `timedatectl set-timezone Europe/Paris` |
| `tzselect` | Sélectionner un fuseau horaire interactivement | `tzselect` |
| `locale` | Afficher les paramètres régionaux | `locale` |
| `locale -a` | Lister les locales disponibles | `locale -a` |
| `localectl` | Gérer les locales système (systemd) | `localectl set-locale LANG=fr_FR.UTF-8` |
| `locale-gen` | Générer les locales (Debian/Ubuntu) | `locale-gen fr_FR.UTF-8` |
| `iconv` | Convertir l'encodage de fichiers | `iconv -f ISO-8859-1 -t UTF-8 file.txt` |
| `file -i` | Détecter l'encodage d'un fichier | `file -i document.txt` |

### 💡 Conseils Pratiques

#### Vérifier l'Encodage d'un Fichier

```bash
# Méthode 1 : file
file -i fichier.txt
# fichier.txt: text/plain; charset=utf-8

# Méthode 2 : file (sans -i)
file fichier.txt
# fichier.txt: UTF-8 Unicode text

# Méthode 3 : chardet (Python)
chardet fichier.txt
# fichier.txt: ISO-8859-1 with confidence 0.73
```

#### Problèmes Courants

**Caractères mal affichés (mojibake) :**

```bash
# Exemple : "café" affiché comme "cafÃ©"
# Cause : Fichier UTF-8 lu comme ISO-8859-1

# Solution : Convertir en UTF-8
iconv -f ISO-8859-1 -t UTF-8 fichier.txt > fichier_corrige.txt
```

**Locale non installé :**

```bash
# Erreur
locale: Cannot set LC_ALL to default locale: No such file or directory

# Solution
sudo locale-gen fr_FR.UTF-8
sudo update-locale LANG=fr_FR.UTF-8
```

#### Configuration Recommandée

**Pour un système moderne :**

```bash
# Fuseau horaire
timedatectl set-timezone Europe/Paris

# Locale
localectl set-locale LANG=fr_FR.UTF-8

# Vérification
timedatectl
localectl status
```

**Pour un utilisateur :**

```bash
# Ajouter au ~/.bashrc
export LANG=fr_FR.UTF-8
export LC_TIME=en_US.UTF-8
export TZ='Europe/Paris'
```

---

## 🏋️ Exercices Pratiques

### Exercice 1 : Gestion des Utilisateurs et Groupes

**Objectif :** Créer et gérer des utilisateurs et des groupes.

```bash
# 1. Créer les groupes administrators et developers
groupadd administrators
groupadd developers

# 2. Créer l'utilisateur kevin avec ces groupes secondaires
useradd -G administrators,developers kevin

# 3. Créer le groupe web-designers et l'ajouter aux groupes de kevin
groupadd web-designers
usermod -a -G web-designers kevin

# 4. Vérifier les groupes de kevin
id kevin
groups kevin

# 5. Supprimer le groupe developers des groupes de kevin
usermod -G administrators,web-designers kevin

# 6. Définir le mot de passe de kevin
passwd kevin

# 7. Définir l'expiration du compte au 31 décembre 2025
chage -E 2025-12-31 kevin

# 8. Créer emma avec UID 1050 et groupes spécifiques
useradd -u 1050 -g administrators -G developers,web-designers emma

# 9. Changer le shell de emma
usermod -s /bin/sh emma

# 10. Supprimer tous les comptes et groupes
userdel -r emma
userdel -r kevin
groupdel administrators
groupdel developers
groupdel web-designers
```

### Exercice 2 : Fichiers de Bases de Données

**Objectif :** Interroger et comprendre les fichiers système.

```bash
# 1. Afficher les informations de l'utilisateur michael
getent passwd michael
grep michael /etc/passwd

# 2. Vérifier le groupe primaire de michael
id -gn michael

# 3. Lister tous les membres du groupe developers
getent group developers

# 4. Vérifier les informations d'expiration de mot de passe
chage -l michael

# 5. Vérifier si un compte est verrouillé
grep michael /etc/shadow | cut -d: -f2
# Si commence par !, le compte est verrouillé
```

### Exercice 3 : Planification avec Cron

**Objectif :** Créer et gérer des tâches cron.

```bash
# 1. Éditer sa crontab
crontab -e

# 2. Ajouter une tâche qui s'exécute tous les vendredi à 13h00
0 13 * * 5 date

# 3. Ajouter une tâche qui s'exécute toutes les minutes
*/1 * * * * ./foobar.sh >> /home/user/output.log

# 4. Désactiver la première tâche (commenter la ligne)
# 0 13 * * 5 date

# 5. Lister sa crontab
crontab -l

# 6. Définir MAILTO pour éviter les emails
# Ajouter en haut de la crontab :
MAILTO=""

# 7. Créer une tâche système dans /etc/cron.d/
sudo nano /etc/cron.d/backup
# Ajouter :
30 2 * * * root /usr/local/bin/backup.sh >> /var/log/backup.log 2>&1
```

### Exercice 4 : Planification avec at

**Objectif :** Utiliser at pour des tâches ponctuelles.

```bash
# 1. Planifier une tâche dans 5 minutes
at now +5 minutes
at> echo "Tâche exécutée" > /tmp/test.txt
at> Ctrl+D

# 2. Planifier une tâche à une date précise
at 10:30 AM October 31
at> ./script.sh
at> Ctrl+D

# 3. Lister les tâches en attente
atq

# 4. Afficher les détails d'une tâche (ID 12)
at -c 12

# 5. Supprimer une tâche
atrm 12

# 6. Planifier une tâche demain
at 10:00 tomorrow
at> ./cleanup.sh
at> Ctrl+D
```

### Exercice 5 : Systemd Timers

**Objectif :** Créer un timer systemd.

```bash
# 1. Créer un service
sudo nano /etc/systemd/system/backup.service

[Unit]
Description=Backup Service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/backup.sh

# 2. Créer un timer
sudo nano /etc/systemd/system/backup.timer

[Unit]
Description=Run backup daily

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target

# 3. Activer et démarrer le timer
sudo systemctl daemon-reload
sudo systemctl enable backup.timer
sudo systemctl start backup.timer

# 4. Vérifier l'état
sudo systemctl status backup.timer
sudo systemctl list-timers

# 5. Voir les logs
journalctl -u backup.service
```

### Exercice 6 : Configuration des Locales

**Objectif :** Configurer les paramètres régionaux et fuseaux horaires.

```bash
# 1. Afficher les locales actuels
locale

# 2. Lister les locales disponibles
locale -a

# 3. Générer un nouveau locale (Debian/Ubuntu)
sudo locale-gen fr_FR.UTF-8

# 4. Définir le locale système
sudo localectl set-locale LANG=fr_FR.UTF-8

# 5. Vérifier la configuration
localectl status

# 6. Définir le fuseau horaire
sudo timedatectl set-timezone Europe/Paris

# 7. Vérifier
timedatectl

# 8. Convertir un fichier ISO-8859-1 en UTF-8
iconv -f ISO-8859-1 -t UTF-8 ancien_fichier.txt > nouveau_fichier.txt
```

---

## ✅ Checklist de Révision

### 107.1 - Gestion des Comptes Utilisateurs et Groupes

- [ ] Je sais créer un utilisateur avec `useradd` et toutes ses options importantes
- [ ] Je sais modifier un utilisateur avec `usermod`
- [ ] Je sais supprimer un utilisateur avec `userdel -r`
- [ ] Je connais la différence entre `-G` et `-a -G` pour les groupes secondaires
- [ ] Je sais créer, modifier et supprimer des groupes
- [ ] Je comprends le rôle du répertoire `/etc/skel`
- [ ] Je connais les directives importantes de `/etc/login.defs`
- [ ] Je sais gérer les mots de passe avec `passwd` et ses options
- [ ] Je sais gérer l'expiration des mots de passe avec `chage`
- [ ] Je connais les équivalences entre `passwd` et `chage`
- [ ] Je comprends la structure de `/etc/passwd` (7 champs)
- [ ] Je comprends la structure de `/etc/group` (4 champs)
- [ ] Je comprends la structure de `/etc/shadow` (9 champs)
- [ ] Je comprends la structure de `/etc/gshadow` (4 champs)
- [ ] Je sais utiliser `getent` pour interroger les bases de données
- [ ] Je sais utiliser `gpasswd` pour gérer les groupes
- [ ] Je sais verrouiller et déverrouiller un compte
- [ ] Je connais les conventions d'ID (root=0, système<1000, utilisateurs≥1000)

### 107.2 - Automatisation des Tâches

- [ ] Je comprends le fonctionnement de cron
- [ ] Je connais la structure d'une crontab utilisateur (6 champs)
- [ ] Je connais la structure d'une crontab système (7 champs)
- [ ] Je sais utiliser les opérateurs cron (*, ,, -, /)
- [ ] Je connais les raccourcis cron (@hourly, @daily, @weekly, @monthly, @yearly)
- [ ] Je sais créer/éditer une crontab avec `crontab -e`
- [ ] Je sais lister et supprimer une crontab
- [ ] Je connais les variables d'environnement crontab (HOME, MAILTO, PATH, SHELL)
- [ ] Je sais rediriger la sortie des tâches cron
- [ ] Je comprends le rôle de `/etc/cron.allow` et `/etc/cron.deny`
- [ ] Je connais les répertoires `/etc/cron.{hourly,daily,weekly,monthly}`
- [ ] Je comprends le fonctionnement des timers systemd
- [ ] Je sais créer un fichier `.timer` et `.service`
- [ ] Je connais la syntaxe `OnCalendar` pour les timers
- [ ] Je sais gérer les timers avec `systemctl`
- [ ] Je sais lister les timers avec `systemctl list-timers`
- [ ] Je sais utiliser `at` pour planifier une tâche ponctuelle
- [ ] Je connais les formats de spécification horaire pour `at`
- [ ] Je sais lister et supprimer des tâches at avec `atq` et `atrm`
- [ ] Je comprends le rôle de `/etc/at.allow` et `/etc/at.deny`
- [ ] Je sais utiliser `systemd-run` pour créer des timers transitoires

### 107.3 - Paramètres Régionaux et Langues

- [ ] Je comprends ce qu'est un fuseau horaire et UTC
- [ ] Je sais afficher la date et l'heure avec `date`
- [ ] Je sais utiliser `timedatectl` pour gérer date/heure/fuseau
- [ ] Je connais le rôle de `/etc/timezone` et `/etc/localtime`
- [ ] Je sais utiliser `tzselect` pour trouver un fuseau horaire
- [ ] Je sais définir le fuseau horaire avec `timedatectl set-timezone`
- [ ] Je comprends l'utilisation de la variable `TZ`
- [ ] Je comprends ce qu'est un locale
- [ ] Je connais le format d'un locale (langue_PAYS.encodage)
- [ ] Je connais les variables `LANG`, `LC_*` et `LC_ALL`
- [ ] Je comprends la hiérarchie des variables locales
- [ ] Je sais afficher les locales avec `locale`
- [ ] Je sais lister les locales disponibles avec `locale -a`
- [ ] Je sais configurer les locales avec `localectl`
- [ ] Je sais générer de nouveaux locales avec `locale-gen`
- [ ] Je comprends la différence entre ASCII, ISO-8859 et UTF-8
- [ ] Je sais que UTF-8 est l'encodage recommandé
- [ ] Je sais utiliser `iconv` pour convertir l'encodage de fichiers
- [ ] Je sais vérifier l'encodage d'un fichier avec `file -i`
- [ ] Je comprends les problèmes de caractères mal affichés (mojibake)

---

## 📚 Ressources Complémentaires

### Documentation Officielle

- [LPI 102-500 Exam Objectives](https://www.lpi.org/our-certifications/exam-102-objectives)
- [Man pages essentielles :]
  - `man useradd`, `man usermod`, `man userdel`
  - `man groupadd`, `man groupmod`, `man groupdel`
  - `man passwd`, `man chage`
  - `man crontab`, `man cron`
  - `man at`, `man atq`, `man atrm`
  - `man systemd.timer`, `man systemctl`
  - `man locale`, `man localectl`
  - `man timedatectl`, `man tzselect`
  - `man iconv`

### Fichiers Importants à Connaître

**Gestion des utilisateurs et groupes :**
- `/etc/passwd` - Base de données des utilisateurs
- `/etc/group` - Base de données des groupes
- `/etc/shadow` - Mots de passe chiffrés des utilisateurs
- `/etc/gshadow` - Mots de passe chiffrés des groupes
- `/etc/skel/` - Répertoire squelette
- `/etc/login.defs` - Configuration de création des utilisateurs
- `/etc/nsswitch.conf` - Configuration NSS

**Planification des tâches :**
- `/etc/crontab` - Crontab système
- `/etc/cron.d/` - Répertoire des crontabs système
- `/etc/cron.{hourly,daily,weekly,monthly}/` - Scripts périodiques
- `/etc/cron.allow` - Utilisateurs autorisés pour cron
- `/etc/cron.deny` - Utilisateurs interdits pour cron
- `/etc/at.allow` - Utilisateurs autorisés pour at
- `/etc/at.deny` - Utilisateurs interdits pour at
- `/var/spool/cron/` - Crontabs utilisateurs
- `/etc/systemd/system/` - Unités systemd (timers et services)

**Locales et fuseaux horaires :**
- `/etc/timezone` - Fuseau horaire système
- `/etc/localtime` - Lien vers le fichier de fuseau horaire
- `/usr/share/zoneinfo/` - Base de données des fuseaux horaires
- `/etc/locale.conf` - Configuration des locales (systemd)
- `/etc/default/locale` - Configuration des locales (Debian/Ubuntu)
- `/etc/locale.gen` - Liste des locales à générer (Debian/Ubuntu)

### Commandes à Maîtriser

**Gestion des utilisateurs :**
- `useradd`, `usermod`, `userdel`
- `groupadd`, `groupmod`, `groupdel`
- `passwd`, `chage`
- `id`, `groups`
- `getent`, `gpasswd`, `newgrp`

**Planification :**
- `crontab`, `at`, `atq`, `atrm`
- `systemctl` (enable, disable, start, stop, status, list-timers)
- `systemd-run`
- `journalctl`

**Locales et temps :**
- `date`, `timedatectl`, `tzselect`
- `locale`, `localectl`, `locale-gen`
- `iconv`, `file`

### Astuces pour l'Examen

1. **Gestion des utilisateurs :**
   - Pensez toujours à vérifier `/etc/login.defs` pour comprendre les valeurs par défaut
   - N'oubliez pas l'option `-a` avec `-G` pour ajouter des groupes secondaires sans écraser les existants
   - Rappelez-vous que `usermod -L` verrouille un compte (ajoute `!` devant le mot de passe dans `/etc/shadow`)

2. **Planification des tâches :**
   - Pour cron, l'ordre des champs est : minute, heure, jour du mois, mois, jour de la semaine, commande
   - Pour les crontabs système, n'oubliez pas le champ utilisateur
   - Redirigez toujours la sortie pour éviter les emails (`> /dev/null 2>&1` pour tout ignorer)
   - Les timers systemd nécessitent deux fichiers : `.timer` et `.service`

3. **Locales et fuseaux horaires :**
   - UTF-8 est toujours le bon choix pour l'encodage
   - Utilisez `timedatectl` et `localectl` sur les systèmes avec systemd
   - La variable `LC_ALL` écrase toutes les autres variables `LC_*`
   - `iconv` est l'outil standard pour convertir l'encodage de fichiers

4. **Sécurité :**
   - Les bits SUID et SGID sur `passwd`, `crontab` et `at` permettent aux utilisateurs ordinaires de les utiliser
   - Les fichiers `/etc/shadow` et `/etc/gshadow` ne sont lisibles que par root
   - Les fichiers `cron.allow` et `at.allow` ont la priorité sur les fichiers `.deny`

---

## 🎓 Points Clés à Retenir

### Gestion des Utilisateurs (107.1)

1. **useradd, usermod, userdel** sont les trois commandes principales
2. **-a -G** pour ajouter des groupes secondaires sans écraser les existants
3. **passwd** et **chage** gèrent l'expiration des mots de passe (équivalences importantes)
4. **/etc/passwd** (7 champs), **/etc/shadow** (9 champs) : structures à connaître
5. **getent** interroge toutes les sources NSS (pas seulement les fichiers locaux)

### Automatisation (107.2)

1. **Cron** : 6 champs pour utilisateurs, 7 pour système (ajout de l'utilisateur)
2. **Opérateurs cron** : `*` (tout), `,` (liste), `-` (plage), `/` (paliers)
3. **Raccourcis** : @hourly, @daily, @weekly, @monthly, @yearly
4. **Systemd timers** : Alternative moderne avec fichiers `.timer` et `.service`
5. **at** : Planification ponctuelle (une seule fois)

### Locales et Temps (107.3)

1. **Fuseaux horaires** : UTC (référence), décalage (GMT-5, GMT+3), noms descriptifs (Europe/Paris)
2. **timedatectl** : Commande systemd pour gérer date/heure/fuseau
3. **Locales** : Format langue_PAYS.encodage (ex: fr_FR.UTF-8)
4. **Variables** : LANG (défaut), LC_* (catégories), LC_ALL (écrase tout)
5. **UTF-8** : Encodage universel recommandé, compatible ASCII

---

**📌 Fin des Notes de Révision - Sujet 107**

💪 Bon courage pour vos révisions !
