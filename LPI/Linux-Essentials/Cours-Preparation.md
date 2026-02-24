# Linux Essentials - Cours de Préparation

## Guide d'utilisation

### Méthode d'apprentissage recommandée

1. **Identifier les faiblesses**
   - Repérer les sujets qui ne sont pas bien assimilés
   - Pratiquer avec les questions par sujet

2. **Comprendre les commandes**
   - L'examen évalue la compréhension des données obtenues d'une commande, pas la mémorisation
   - Connaître la syntaxe ne suffit pas : il faut comprendre quelles données sont disponibles sous chaque commande ou flag
   - Observer les en-têtes pour saisir les informations utiles

3. **Réviser de multiples façons**
   - Simplement regarder les commandes ne suffit pas à les comprendre
   - Travailler directement avec Linux pour mieux assimiler

4. **Ne pas se fier uniquement aux examens blancs**
   - Les examens Cisco et Udemy ne couvrent pas tout
   - Udemy est trop facile comparé à l'examen réel
   - Cisco est difficile, mais ne garantit pas la réussite seul

5. **Prendre son temps**
   - Ne pas se comparer à ceux qui prétendent finir rapidement
   - Comprendre l'OS prend du temps (450 pages de matériel)

---

## Sujets couverts

- **Sujet 1** : La communauté Linux et carrière dans l'Open Source
- **Sujet 2** : Navigation dans un système Linux
- **Sujet 3** : Puissance de la ligne de commande
- **Sujet 4** : Le système d'exploitation Linux
- **Sujet 5** : Sécurité et permissions de fichiers

---

## Questions d'étude

### Section 1 : La communauté Linux et carrière dans l'Open Source

**Questions 1-10**

1. **Qui a développé Linux en 1991 ?**
   - A. Ken Thompson
   - B. Linus Torvalds ✓
   - C. Dennis Ritchie
   - D. Richard Stallman

2. **Quel est l'outil principal de gestion de paquets pour les distributions basées sur Debian ?**
   - A. YUM
   - B. RPM
   - C. APT ✓
   - D. GNOME Software

3. **Quelle distribution Linux est connue pour être un environnement de bureau sécurisé ?**
   - A. Ubuntu
   - B. Fedora
   - C. QubesOS ✓
   - D. Kali Linux

4. **Quel est l'objectif principal du projet GNU fondé par Richard Stallman ?**
   - A. Créer un OS Unix commercial
   - B. Créer un OS libre compatible avec Unix ✓
   - C. Développer des logiciels propriétaires
   - D. Remplacer les distributions Linux

5. **Laquelle des licences suivantes est permissive ?**
   - A. AGPL
   - B. BSD ✓
   - C. AGPL
   - D. LGPL

6. **Quel est l'avantage principal d'Android comme OS pour systèmes embarqués ?**
   - A. Frais de licence élevés
   - B. Compatibilité limitée
   - C. Interface graphique intuitive pour la technologie tactile ✓
   - D. Composants uniquement propriétaires

7. **Que signifie le terme "fork" dans le logiciel open source ?**
   - A. Un type de licence
   - B. Créer une nouvelle version d'un logiciel à partir du code existant ✓
   - C. Fusionner deux projets logiciels
   - D. Payer pour des mises à jour logicielles

8. **Quelle organisation valide les licences open source ?**
   - A. Projet GNU
   - B. Free Software Foundation
   - C. Open Source Initiative ✓
   - D. Linux Professional Institute

9. **Quel est un exemple de licence Creative Commons ?**
   - A. CC BY-SA ✓
   - B. GPLv3
   - C. LGPL
   - D. BSD

10. **Quel est l'objectif de la Raspberry Pi Foundation ?**
    - A. Construire des serveurs d'entreprise
    - B. Enseigner la programmation et les fondamentaux informatiques aux jeunes ✓
    - C. Développer des plateformes cloud
    - D. Créer des logiciels propriétaires

**Réponses : 1-B, 2-C, 3-C, 4-B, 5-B, 6-C, 7-B, 8-C, 9-A, 10-B**

---

### Section 2 : Navigation dans un système Linux

**Questions 11-20**

1. **Quelle commande affiche le répertoire de travail actuel ?**
   - A. cd
   - B. pwd ✓
   - C. ls
   - D. echo

2. **Quel est l'objectif du fichier `/etc/passwd` ?**
   - A. Stocker les informations de compte utilisateur ✓
   - B. Stocker les informations de groupe
   - C. Stocker la configuration du noyau
   - D. Stocker les détails des pilotes de périphérique

3. **Quelle commande est utilisée pour rechercher des fichiers dans le système de fichiers ?**
   - A. locate ✓
   - B. grep
   - C. cat
   - D. echo

4. **Que fait la commande `man` ?**
   - A. Affiche un manuel pour les commandes Linux ✓
   - B. Affiche les processus actuels
   - C. Modifie les permissions de fichier
   - D. Bascule vers le superutilisateur

5. **Que représente le symbole tilde `~` dans le système de fichiers Linux ?**
   - A. Répertoire racine
   - B. Répertoire actuel
   - C. Répertoire personnel de l'utilisateur ✓
   - D. Répertoire temporaire

6. **Quel shell est le plus couramment utilisé sur les systèmes Linux ?**
   - A. C shell
   - B. Korn shell
   - C. Z shell
   - D. Bourne-again shell (Bash) ✓

7. **Quel est l'objectif de la commande `echo` ?**
   - A. Afficher du texte ou des variables ✓
   - B. Créer des fichiers
   - C. Supprimer des répertoires
   - D. Copier des fichiers

8. **Quelle commande est utilisée pour modifier les permissions d'un fichier ?**
   - A. chmod ✓
   - B. chown
   - C. ls
   - D. mkdir

9. **Quel fichier contient la liste des répertoires où le shell recherche les fichiers exécutables ?**
   - A. /etc/shells
   - B. /etc/passwd
   - C. PATH ✓
   - D. /bin

10. **Que fait le symbole `>` dans la ligne de commande ?**
    - A. Redirige l'entrée
    - B. Redirige la sortie ✓
    - C. Redirige les données entre commandes
    - D. Ajoute des données à un fichier

**Réponses : 11-B, 12-A, 13-A, 14-A, 15-C, 16-D, 17-A, 18-A, 19-C, 20-B**

---

### Section 3 : Puissance de la ligne de commande

**Questions 21-30**

1. **Que spécifie l'option `-z` dans la commande `tar` ?**
   - A. Utiliser la compression bzip2
   - B. Utiliser la compression gzip ✓
   - C. Utiliser la compression xz
   - D. Aucune compression

2. **Quel algorithme de compression offre le niveau de compression le plus élevé ?**
   - A. gzip
   - B. bzip2
   - C. xz ✓
   - D. zip

3. **Quelle est la fonction de la commande `grep` ?**
   - A. Copier des fichiers
   - B. Rechercher des motifs dans le texte ✓
   - C. Lister le contenu des répertoires
   - D. Modifier les permissions de fichiers

4. **Que fait la commande `head` ?**
   - A. Afficher les 10 premières lignes d'un fichier ✓
   - B. Afficher les 10 dernières lignes d'un fichier
   - C. Afficher toutes les lignes contenant un motif spécifique
   - D. Trier les lignes d'un fichier

5. **Quel est l'objectif de `chmod +x` ?**
   - A. Définir les permissions d'exécution pour un fichier ✓
   - B. Définir les permissions de lecture pour un fichier
   - C. Définir les permissions d'écriture pour un fichier
   - D. Supprimer les permissions d'exécution d'un fichier

6. **Que fait l'opérateur `|` (pipe) dans Linux ?**
   - A. Redirige l'entrée vers un fichier
   - B. Combine deux fichiers
   - C. Redirige la sortie d'une commande vers une autre ✓
   - D. Ajoute des données à un fichier existant

7. **Quelle est la commande par défaut pour éditer du texte dans Linux ?**
   - A. nano ✓
   - B. vim
   - C. emacs
   - D. gedit

8. **Quel paramètre spécial contient le nombre d'arguments passés à un script ?**
   - A. $!
   - B. $# ✓
   - C. $@
   - D. $*

9. **Que signifie un code de sortie de 0 dans un script ?**
   - A. Le script a rencontré une erreur
   - B. Le script s'est terminé avec succès ✓
   - C. Le script est en pause
   - D. Le script est prêt à s'exécuter

10. **Quel est l'objectif du shebang `#!/bin/bash` dans un script ?**
    - A. Exécuter le script
    - B. Indiquer que le script est un script shell ✓
    - C. Définir les permissions de fichier
    - D. Ajouter des commentaires au script

**Réponses : 21-B, 22-C, 23-B, 24-A, 25-A, 26-C, 27-A, 28-B, 29-B, 30-B**

---

### Section 4 : Le système d'exploitation Linux

**Questions 31-40**

1. **Quel répertoire contient les binaires utilisateur ?**
   - A. /bin
   - B. /sbin
   - C. /usr/bin ✓
   - D. /usr/local/sbin

2. **Quel est l'objectif principal du répertoire `/proc` ?**
   - A. Stocker les données utilisateur
   - B. Stocker les informations sur les processus et le noyau ✓
   - C. Stocker les fichiers exécutables
   - D. Stocker les données temporaires

3. **Que fait la commande `lsblk` ?**
   - A. Créer des périphériques en mode bloc
   - B. Afficher des informations sur les périphériques en mode bloc ✓
   - C. Monter des périphériques en mode bloc
   - D. Démonter des périphériques en mode bloc

4. **Quelle est la signification du répertoire `/etc` ?**
   - A. Contient les répertoires personnels des utilisateurs
   - B. Contient les fichiers de configuration ✓
   - C. Contient les fichiers de périphériques
   - D. Contient les fichiers temporaires

5. **Lequel des éléments suivants est un système de fichiers virtuel ou pseudo dans Linux ?**
   - A. /root
   - B. /usr
   - C. /proc ✓
   - D. /var

6. **Qu'affiche la commande `free` ?**
   - A. Permissions de fichiers
   - B. Utilisation de la mémoire ✓
   - C. Utilisation du disque
   - D. Utilisation du CPU

7. **Quel fichier liste les appartenances de groupe sur le système ?**
   - A. /etc/passwd
   - B. /etc/group ✓
   - C. /etc/shadow
   - D. /etc/gshadow

8. **Quel est le rôle du noyau Linux ?**
   - A. Gérer les permissions utilisateur
   - B. Gérer le matériel et les ressources ✓
   - C. Stocker les fichiers de configuration
   - D. Surveiller les fichiers journaux

9. **Quel répertoire est utilisé pour stocker les fichiers temporaires qui persistent entre les redémarrages ?**
   - A. /tmp
   - B. /var/tmp ✓
   - C. /run
   - D. /etc/tmp

10. **Que fait `/dev/null` ?**
    - A. Redirige les données vers un fichier
    - B. Rejette toutes les données envoyées ✓
    - C. Stocke les données temporaires
    - D. Crypte les données

**Réponses : 31-C, 32-B, 33-B, 34-B, 35-C, 36-B, 37-B, 38-B, 39-B, 40-B**

---

### Section 5 : Sécurité et permissions de fichiers

**Questions 41-50**

1. **Quel est l'objectif du fichier `/etc/shadow` ?**
   - A. Stocker les informations d'appartenance de groupe
   - B. Stocker les mots de passe utilisateur sous forme hachée ✓
   - C. Stocker la configuration du noyau
   - D. Stocker les noms d'utilisateur des comptes

2. **Que fait la commande `chmod` ?**
   - A. Modifier les permissions de fichier ✓
   - B. Modifier la propriété du fichier
   - C. Modifier le type de fichier
   - D. Modifier l'emplacement du fichier

3. **Quelle permission est représentée par la valeur octale 4 ?**
   - A. Exécution
   - B. Écriture
   - C. Lecture ✓
   - D. Suppression

4. **Que fait le flag `-R` lorsqu'il est utilisé avec `chmod` ?**
   - A. Appliquer récursivement les permissions aux répertoires et fichiers ✓
   - B. Supprimer les permissions d'un fichier
   - C. Réinitialiser les permissions par défaut
   - D. Afficher les permissions d'un répertoire

5. **Que fait un sticky bit ?**
   - A. Empêcher les utilisateurs non autorisés de supprimer un fichier ✓
   - B. Permettre aux membres du groupe de modifier un fichier
   - C. Exécuter automatiquement un fichier à la connexion
   - D. Changer le propriétaire d'un fichier

6. **Quelle est la représentation d'un lien symbolique dans la sortie de `ls -l` ?**
   - A. Un `l` initial ✓
   - B. Un `d` initial
   - C. Un `s` initial
   - D. Un `b` initial

7. **Que fait la commande `chown` ?**
   - A. Modifier les permissions de fichier
   - B. Modifier la propriété du fichier ✓
   - C. Modifier le type de fichier
   - D. Modifier l'emplacement du fichier

8. **Quelle est la valeur octale pour les permissions `rwx` ?**
   - A. 4
   - B. 6
   - C. 7 ✓
   - D. 5

9. **Quelle commande liste tous les utilisateurs actuellement connectés au système ?**
   - A. who ✓
   - B. id
   - C. groups
   - D. sudo

10. **Quel est l'objectif du fichier `/etc/sudoers` ?**
    - A. Stocker les mots de passe des comptes utilisateur
    - B. Définir qui peut utiliser la commande `sudo` ✓
    - C. Stocker les appartenances de groupe système
    - D. Définir les paramètres du noyau

**Réponses : 41-B, 42-A, 43-C, 44-A, 45-A, 46-A, 47-B, 48-C, 49-A, 50-B**

---

## Flashcards de révision

### Flashcards 1-10 : Communauté Linux et Open Source

1. **Qui a développé Linux en 1991 ?** → Linus Torvalds
2. **Outil principal de gestion de paquets pour Debian ?** → APT
3. **Distribution Linux connue pour sécurité de bureau ?** → QubesOS
4. **Objectif du projet GNU ?** → Créer un OS libre compatible Unix
5. **Licence permissive ?** → BSD
6. **Avantage d'Android pour systèmes embarqués ?** → Interface tactile intuitive
7. **Signification de "fork" ?** → Créer une nouvelle version à partir du code existant
8. **Organisation validant licences open source ?** → Open Source Initiative
9. **Exemple de licence Creative Commons ?** → CC BY-SA
10. **Objectif Raspberry Pi Foundation ?** → Enseigner programmation aux jeunes

### Flashcards 11-20 : Navigation système Linux

1. **Commande pour afficher répertoire actuel ?** → pwd
2. **Objectif de `/etc/passwd` ?** → Stocker informations compte utilisateur
3. **Commande de recherche de fichiers ?** → locate
4. **Fonction de `man` ?** → Afficher manuel des commandes Linux
5. **Symbole `~` représente ?** → Répertoire personnel utilisateur
6. **Shell le plus utilisé ?** → Bash (Bourne-again shell)
7. **Objectif de `echo` ?** → Afficher texte ou variables
8. **Commande pour modifier permissions ?** → chmod
9. **Fichier listant répertoires exécutables ?** → PATH
10. **Symbole `>` fait quoi ?** → Redirige la sortie

### Flashcards 21-30 : Ligne de commande

1. **Option `-z` dans `tar` ?** → Compression gzip
2. **Meilleure compression ?** → xz
3. **Fonction de `grep` ?** → Rechercher motifs dans texte
4. **Fonction de `head` ?** → Afficher 10 premières lignes
5. **Objectif `chmod +x` ?** → Définir permission exécution
6. **Opérateur `|` (pipe) ?** → Rediriger sortie vers autre commande
7. **Éditeur texte par défaut ?** → nano
8. **Paramètre pour nombre d'arguments ?** → $#
9. **Code sortie 0 signifie ?** → Script terminé avec succès
10. **Objectif du shebang ?** → Indiquer script shell

### Flashcards 31-40 : Système d'exploitation

1. **Répertoire binaires utilisateur ?** → /usr/bin
2. **Objectif de `/proc` ?** → Stocker infos processus et noyau
3. **Fonction `lsblk` ?** → Afficher infos périphériques bloc
4. **Signification `/etc` ?** → Contient fichiers configuration
5. **Système fichiers virtuel ?** → /proc
6. **Commande `free` affiche ?** → Utilisation mémoire
7. **Fichier listant groupes ?** → /etc/group
8. **Rôle noyau Linux ?** → Gérer matériel et ressources
9. **Répertoire fichiers temporaires persistants ?** → /var/tmp
10. **Fonction `/dev/null` ?** → Rejeter toutes données

### Flashcards 41-50 : Sécurité et permissions

1. **Objectif `/etc/shadow` ?** → Stocker mots de passe hachés
2. **Fonction `chmod` ?** → Modifier permissions fichier
3. **Valeur octale 4 ?** → Lecture
4. **Flag `-R` avec `chmod` ?** → Appliquer récursivement permissions
5. **Fonction sticky bit ?** → Empêcher suppression non autorisée
6. **Représentation lien symbolique ?** → `l` initial
7. **Fonction `chown` ?** → Modifier propriété fichier
8. **Valeur octale `rwx` ?** → 7
9. **Commande liste utilisateurs connectés ?** → who
10. **Objectif `/etc/sudoers` ?** → Définir qui peut utiliser sudo

### Flashcards 51-60 : Réseau et système

1. **Fonction `locate` ?** → Rechercher fichiers dans base de données
2. **Objectif `find` ?** → Rechercher système fichiers selon critères
3. **Fonction `/etc/hosts` ?** → Mapper noms d'hôtes vers IP
4. **Commande `ping` teste ?** → Connectivité entre périphériques
5. **Fonction `dig` ?** → Interroger informations DNS
6. **Commande `ip addr` affiche ?** → Liste interfaces réseau
7. **Équivalent IPv6 de `ping` ?** → ping6
8. **NAT fait quoi ?** → Mapper adresses internes vers IP externe unique
9. **Commande `ss` affiche ?** → Informations sur sockets
10. **Objectif `/etc/resolv.conf` ?** → Configurer paramètres DNS

### Flashcards 61-70 : Fichiers système

1. **Objectif `/tmp` ?** → Fichiers temporaires effacés au boot
2. **Commande `ln` ?** → Créer liens vers fichiers
3. **Différence hard link / soft link ?** → Hard pointe inode, soft pointe chemin
4. **Objectif `/proc/cpuinfo` ?** → Infos processeur système
5. **Commande `id` affiche ?** → UID, GID utilisateur
6. **Fonction `/etc/group` ?** → Stocker infos groupes système
7. **Commande `last` montre ?** → Infos dernière connexion utilisateurs
8. **Objectif `/etc/shadow` ?** → Stocker mots de passe hachés
9. **Mode symbolique `chmod` ?** → Utiliser u, g, o, a
10. **Flag `-R` fait quoi ?** → Application récursive

### Flashcards 71-80 : Permissions avancées

1. **Fonction sticky bit ?** → Empêcher suppression non autorisée dans répertoire
2. **Valeur octale sticky bit ?** → 1
3. **SGID fait quoi ?** → Hériter groupe du répertoire parent
4. **Valeur octale SGID ?** → 2
5. **SUID fait quoi ?** → Exécuter avec privilèges propriétaire
6. **Valeur octale SUID ?** → 4
7. **Différence `/bin` et `/sbin` ?** → bin=tous utilisateurs, sbin=administrateurs
8. **Commande `touch` ?** → Créer fichier vide
9. **Objectif `/etc/fstab` ?** → Définir montage partitions disque
10. **Commande `cp -r` ?** → Copier fichiers et répertoires récursivement

### Flashcards 81-90 : Répertoires système

1. **Utilisation `/var/tmp` ?** → Fichiers temporaires persistant entre boots
2. **Objectif `/boot` ?** → Contient noyau Linux et chargeur démarrage
3. **Fonction `/dev/null` ?** → Rejeter toutes entrées
4. **Objectif `/etc/sudoers.d` ?** → Stocker configs sudo supplémentaires
5. **Commande `mv` ?** → Déplacer ou renommer fichiers
6. **Commande `ls -l` affiche ?** → Infos détaillées fichiers et répertoires
7. **Objectif `/usr/local` ?** → Stocker programmes installés localement
8. **Commande `cat` ?** → Afficher contenu fichier
9. **Objectif `/etc/bash.bashrc` ?** → Config système bash
10. **Commande `pwd` affiche ?** → Répertoire travail actuel

### Flashcards 91-100 : Gestion utilisateurs

1. **Objectif `/etc/skel` ?** → Fichiers par défaut nouveaux répertoires utilisateur
2. **Commande `groupadd` ?** → Ajouter nouveau groupe
3. **Commande `passwd` ?** → Changer mot de passe utilisateur
4. **Objectif `/etc/gshadow` ?** → Stocker mots de passe groupe hachés
5. **`chmod 777` fait quoi ?** → Toutes permissions pour tous
6. **Commande `whoami` affiche ?** → Utilisateur actuel
7. **Objectif `/etc/hostname` ?** → Stocker nom d'hôte système
8. **Commande `rm -rf` ?** → Supprimer répertoires et contenu récursivement
9. **Fonction `/etc/crontab` ?** → Gérer tâches planifiées système
10. **Objectif `/var/log` ?** → Stocker journaux système et applications

---

## Notes de cours détaillées

### Leçon 1.1 : Évolution de Linux et systèmes d'exploitation populaires

#### Histoire de Linux

- **1991** : Linus Torvalds développe Linux, inspiré par Unix (créé dans les années 1970 par AT&T Laboratories)
- Unix n'était pas relativement disponible pour les ordinateurs de bureau
- **Distribution Linux** : consiste en un noyau Linux et une sélection d'applications maintenues par une entreprise ou communauté

#### Familles de distributions

**Famille Debian**
- Basée sur le gestionnaire de paquets APT
- Exemples : Debian, Ubuntu, Linux Mint

**Famille Red Hat**
- Basée sur les gestionnaires RPM/YUM/DNF
- Exemples : Red Hat Enterprise Linux, CentOS, Fedora

#### Distributions spécialisées

- **QubesOS** : Environnement de bureau sécurisé
- **Kali Linux** : Environnement pour exploiter les vulnérabilités logicielles, principalement pour les testeurs de pénétration

#### SUSE

- **1992** : Fondée en Allemagne comme fournisseur de services Unix
- Dérivée de Slackware
- Connue pour son outil de configuration **YaST**
  - Outil d'administration
  - Installation et configuration logiciels/matériel
  - Configuration serveurs et réseaux
- **SUSE Enterprise** : Édition commerciale avec packages pour serveurs ou bureaux
- **openSUSE** : Version gratuite, environnement de test pour développeurs

#### Systèmes embarqués

Matériel et logiciel conçus pour une fonction spécifique dans un système plus large :
- Automobile (tableaux de bord)
- Équipements médicaux
- Militaire

**Avantages de Linux :**
- Compatibilité multiplateforme
- Développement actif
- Support communautaire
- Pas de frais de licence

#### Cycles de version

- **Release cycle** : Mises à jour OS et logiciels sur base régulière
- **Maintenance cycle / Life cycle** : Période pendant laquelle les fournisseurs supportent les anciennes versions

#### Linux et le Cloud

Absence de licence requise → forte demande pour Linux dans l'Infrastructure as a Service (IaaS) pour machines virtuelles

---

### Leçon 1.2 : Applications Open Source majeures

#### Gestion de paquets

**Distributions basées Debian :**
```bash
apt search package_name      # Rechercher paquet
apt install package_name     # Installer paquet
apt remove package_name      # Supprimer paquet
```

**Distributions basées Red Hat :**
```bash
yum search package_name      # Rechercher paquet
dnf search package_name      # Rechercher paquet (nouveau)
yum install package_name     # Installer paquet
yum remove package_name      # Supprimer paquet
```

> **Note :** `sudo` est nécessaire pour installer/supprimer

#### Applications bureautiques

**OpenOffice**
- Créé par Sun Microsystems (acquis par Oracle)
- Version open source de StarOffice
- Licence : Apache License 2.0

**LibreOffice**
- Publié par Document Foundation
- Utilise le même code source qu'OpenOffice
- Licence : LGPLv3

#### Navigateurs et multimédia

**Navigateurs**
- Chrome et Firefox : plus courants sur Linux
- Chromium : navigateur open source dont Chrome est dérivé

**Application email**
- Thunderbird : application email dédiée la plus courante

**Applications multimédia**

| Application | Fonction | Équivalent |
|-------------|----------|------------|
| Blender | Rendu 3D et animations | - |
| GIMP | Éditeur d'images | Adobe Photoshop |
| Inkscape | Éditeur graphiques vectoriels | Corel Draw, Adobe Illustrator |
| Audacity | Éditeur audio | - |
| ImageMagick | Conversion et édition images | - |

**Lecteurs audio**
- Audacious
- Banshee
- Amarok

**Lecteurs vidéo**
- VLC
- SMPlayer

#### Programmes serveur

**Serveurs HTTP**
- Apache
- Nginx
- lighttpd

**Bases de données relationnelles open source**
- MariaDB
- PostgreSQL

#### Partage de données

**NFS (Network File System)**
- Partage de répertoires : `/etc/exports`
- Montage dans système de fichiers local
- Contrôle d'accès : règles basées sur hôte (adresse IP)
- Basé sur modèle permissions Linux/Unix
- Utilisé pour clients légers (thin clients)

**Samba**
- Partages définis dans `/etc/samba/smb.conf`
- Contrôle d'accès style Windows
- Chemin réseau : `\\serveur\partage`
- Nécessaire pour partage Linux ↔ Windows
- Protocole SMB/CIFS
- Permet partage périphériques et imprimantes
- Autorisation via contrôleur de domaine (Active Directory)
- Association avec contrôleur : Samba ou SSSD

#### Partage cloud

**ownCloud / Nextcloud**
- Partage fichiers et synchronisation
- Nextcloud : conférence audio/vidéo privée

**Caractéristiques**
- Installation serveur privé gratuite
- Versions payantes avec fonctionnalités supplémentaires

#### Administration réseau

**DHCP (Dynamic Host Configuration Protocol)**
- Attribue adresse IP automatiquement lors de connexion réseau
- Configuration manuelle possible mais impratique

**DNS (Domain Name System)**
- Traduit noms de domaine en adresses IP
- Système distribué

#### Langages de programmation

**Langages compilés**
- Nécessitent étape de compilation
- Exécution plus rapide (précompilé)
- Erreurs détectées lors compilation
- Compilateur convertit code source → fichier binaire
- Exemples : C, C++

**Langages interprétés**
- Interpréteur lit et exécute ligne par ligne
- Exécution plus lente (interprétation à l'exécution)
- Code source utilisé directement
- Portables
- Utilisés pour scripting, automatisation
- Exemples : Python, JavaScript, Ruby, Perl, Bash

---

### Leçon 1.3 : Logiciels Open Source et licences

#### Définition du logiciel libre et open source

**1985 : Projet GNU** fondé par Richard Stallman

**Quatre libertés essentielles :**
0. Liberté d'exécuter le programme comme vous le souhaitez
1. Liberté d'étudier le fonctionnement du programme et de le modifier
2. Liberté de redistribuer des copies
3. Liberté de distribuer des copies de vos versions modifiées

**Note importante :** Linux est techniquement le noyau. L'OS complet est GNU/Linux (GNU is Not Unix).

#### Catégories de licences

```
Permissive ← → Copyleft ← → Proprietary
(Moins restrictif)     (Plus restrictif)
```

**Terminologie**
- **FOSS** : Free and Open Source Software
- **FLOSS** : Free/Libre and Open Source Software

#### Licences GNU (GPL)

**GPL (General Public License)**
- Licence la plus importante pour logiciels libres
- Utilisée par le noyau Linux

**LGPL (Lesser GPL)**
- Logiciel libre
- Modifications du code source n'ont pas besoin d'être publiées

**AGPL (Affero GPL)**
- Pour vente d'accès à logiciel hébergé

**FDL (Free Documentation License)**
- Principes de liberté étendus à la documentation

#### FSF (Free Software Foundation)

**Rôles :**
- Recommandations pour/contre licences tierces
- **GPLViolations.org** : Enquête violations licences libres
- **Copyleft** : Principe de transfert des principes libres aussi librement que possible

**Limitation :** Logiciels de différentes licences Copyleft ne peuvent être combinés

#### Open Source Initiative (OSI)

**1998** : Fondée par Eric Raymond et Bruce Perens
- **Open Source Definition** : Procédure standardisation vérification conformité licences
- Environ 80 licences open source validées

#### Licence BSD

**BSD (Berkeley Software Distribution)** : Variante d'Unix
- Dérivés : NetBSD, FreeBSD, OpenBSD
- Liberté maximale de distribution
- Permet décision éditeurs (source fermée ou commercial)

**Conditions de redistribution :**
1. Le code source doit conserver notice copyright, conditions et disclaimer
2. Forme binaire doit reproduire notice copyright dans documentation
3. Nom détenteur copyright ne peut être utilisé pour promouvoir produits dérivés sans permission

#### Creative Commons

Organisation mondiale à but non lucratif pour partage créativité et connaissance.

**Focus :** Œuvres d'art et travaux scientifiques (droits d'auteur)

**Licences Creative Commons :**

| Licence | Description |
|---------|-------------|
| CC BY | Attribution - Libre avec mention auteur |
| CC BY-SA | Attribution - ShareAlike - Même licence pour modifications |
| CC BY-ND | Attribution - NoDerivs - Pas de modifications |
| CC BY-NC | Attribution - NonCommercial - Usage non commercial |
| CC BY-NC-SA | NonCommercial + ShareAlike |
| CC BY-NC-ND | NonCommercial + NoDerivs |

**Principe :** Plus de fonctionnalités = Plus restrictif

#### Modèles économiques FLOSS

**1993 : Red Hat** fondée (3 milliards USD ventes annuelles en 2018)

**Méthodes de monétisation :**
1. Financement participatif (Kickstarter)
2. Double licence (édition business propriétaire)
3. Monétisation périphérique (merchandising, support, certificats, formation)
4. Modèle SaaS (accès payant à applications installées)
5. Fonctionnalités supplémentaires payantes

---

### Leçon 1.4 : Communauté Linux et carrière dans l'Open Source

#### Environnements de bureau

**GNOME**
- Principe KISS (Keep It Simple, Stupid)
- Applications épurées et propres
- Basé sur GTK Toolkit (écrit en C)
- Terminal : Gnome Terminal

**KDE**
- Large sélection d'applications
- Interface similaire à Windows
- Bibliothèque Qt (écrite en C++)
- Terminal : Konsole ou Xterm

#### TTY (TeleTYpewriter)

Simulations de terminal physique basé texte
- Permettent sessions multiples
- Accès via `Ctrl+Alt+F1` (F2 pour session suivante, etc.)

#### Utilisations professionnelles

**Présentations**
- **Beamer** : Classe LaTeX pour présentations
  - Gère équations mathématiques complexes
- **Reveal.js** : Paquet NPM pour présentations web
  - Utilise HTML/CSS/JavaScript

**Gestion de projet**
- GanttProject
- ProjectLibre
- Remplacement pour Microsoft Project

**Cloud et virtualisation**

**Hyperviseurs open source :**
- Xen
- KVM (sponsorisé par Red Hat)
- VirtualBox (Oracle - usage utilisateur final)

**Plateformes cloud :**
- **Heroku** : PaaS - Exécute code sans gérer conteneurs/VMs
- **OpenStack** : Logiciel open source pour environnement IaaS complet sur site

#### Sécurité et confidentialité

**Cookies**
- Petits fichiers sauvegardés par sites web
- Stockent/récupèrent informations navigation
- Publicités utilisent cookies pour monétisation
- Tiers peuvent être désactivés (certaines fonctionnalités perdues)

**DNT (Do Not Track)**
- Indique au site que vous ne voulez pas être suivi
- Respect non garanti

**Navigation privée**
- Ne laisse pas de traces sur l'ordinateur après fermeture session
- N'empêche pas le suivi en ligne
- Attention aux lieux publics

#### Bonnes pratiques mots de passe

- Alphanumériques
- Longueur suffisante
- Caractères spéciaux
- Non devinables
- Pas de réutilisation
- Changement régulier

**Gestionnaires de mots de passe :**
- KeePass
- BitWarden

#### Sécurité réseau

**TLS (Transport Layer Security)**
- Sécurité connexions réseau via cryptographie
- Successeur de SSL
- Version actuelle : 1.3
- Cryptographie symétrique et à clé publique
- Utilisé avec HTTP → HTTPS

#### Chiffrement

**GnuPG (GNU Privacy Guard)**
- Implémentation open source d'OpenPGP
- Signer, chiffrer, déchiffrer : textes, emails, fichiers, répertoires, partitions
- Clés publique et privée
  - Clé privée : signature numérique validation
  - Clé publique : vérification correspondance

**Types de chiffrement :**

**Block-level (niveau bloc)**
- En dessous de la couche système de fichiers
- Tout écrit sur périphérique bloc est chiffré
- Hors ligne : ressemble à données aléatoires
- **dm-crypt** : Standard chiffrement bloc Linux
  - Utilisable avec LUKS (Linux Unified Key Setup)

**Stacked (empilé)**
- Au-dessus de la couche système de fichiers
- Fichiers chiffrés avant stockage
- **EncFS** : Chiffrement empilé sans privilèges root

**Multiplateforme**
- **VeraCrypt** : Chiffre médias et fichiers
  - Fonctionne sur Linux, macOS, Windows

---

### Leçon 2.1 : Bases de la ligne de commande

#### Shells Linux

**Shells couramment utilisés :**
- **Bash (Bourne-again shell)** : Le plus courant
- C shell (csh ou tcsh)
- Korn shell (ksh)
- Z shell (zsh)

#### Anatomie du prompt

```
utilisateur@hôte:~/Téléchargements$
│          │    │                │
│          │    │                └─ Prompt
│          │    └─ Répertoire actuel
│          └─ Nom de l'hôte
└─ Utilisateur actuel
```

- **~** : Répertoire personnel (home)
- **$** : Utilisateur normal
- **#** : Superutilisateur (root)

#### Élévation de privilèges

```bash
sudo commande    # Exécute commande avec privilèges élevés
sudo -i          # Ouvre shell root
su               # Change d'utilisateur
```

#### Structure de commande

```
commande [OPTIONS] [ARGUMENTS]
│        │         │
│        │         └─ Arguments positionnels
│        └─ Options/flags (courtes: -a, longues: --all)
└─ Nom de la commande
```

#### Types de commandes

**Internes**
- Exécutées dans le shell
- Environ 30 commandes
- Exemples : `cd`, `set`, `export`

**Externes**
- Résident dans fichiers
- Shell utilise variable `PATH` pour les trouver
- Exemples : `ls`, `cat`, `grep`

**Vérifier le type :**
```bash
type commande
```

#### Guillemets

**Guillemets simples (`'`)**
- Caractères spéciaux perdent leur signification
- Traités comme texte littéral

**Guillemets doubles (`"`)**
- Variables et caractères spéciaux sont interprétés
- Exemple : `$USER` sera remplacé par nom utilisateur

**Échappement (`\`)**
- Backslash devant caractère spécial → traité comme littéral

**Bonnes pratiques :**
- Éviter caractères spéciaux dans noms de fichiers
- Utiliser underscore (`_`) ou point (`.`) à la place

---

### Leçon 2.2 : Variables et aide en ligne de commande

#### Types de variables

**Variables locales**
- Stockent données (texte ou nombres)
- Non héritées par sous-shells
- Spécifiques au terminal où créées

**Variables d'environnement**
- Disponibles dans session shell et sous-processus
- Généralement en MAJUSCULES
- Exemples importants :
  - **`PATH`** : Liste répertoires contenant exécutables (séparés par `:`)
  - **`DATE`** : Date actuelle
  - **`USER`** : Utilisateur actuel

#### Gestion des variables

**Créer variable locale :**
```bash
NOM_VARIABLE=valeur     # Pas d'espaces autour de =
```

**Créer variable d'environnement :**
```bash
export NOM_VARIABLE=valeur
```

**Appeler une variable :**
```bash
echo $NOM_VARIABLE
```

**Ajouter au PATH :**
```bash
PATH=$PATH:/nouveau/repertoire
```

**Persistance :**
- Variables temporaires : disparaissent à fermeture shell
- Variables permanentes : définir dans fichiers configuration shell

#### Obtenir de l'aide

**Options d'aide :**

```bash
commande --help         # Instructions brèves
man commande            # Manuel complet (digest)
info commande           # Détaillé avec hypertexte
locate fichier          # Recherche dans base de données
find chemin -name nom   # Recherche système fichiers
```

#### Pages man

**Structure des pages man :**

| Section | Description |
|---------|-------------|
| NAME | Nom commande et brève description |
| SYNOPSIS | Syntaxe de la commande |
| DESCRIPTION | Description détaillée |
| OPTIONS | Options disponibles |
| FILES | Fichiers auxiliaires |
| BUGS | Limitations connues |
| EXAMPLES | Exemples d'utilisation |

**Catégories de pages man :**

1. Commandes utilisateur
2. Appels système
3. Fonctions bibliothèque
4. Pilotes et fichiers périphériques
5. Fichiers configuration et formats
6. Jeux
7. Divers
8. Commandes administrateur
9. Fonctions noyau (non standard)

**Navigation :**
```bash
man commande            # Ouvrir page man
/motif                  # Rechercher
n                       # Occurrence suivante
q                       # Quitter
```

**Exemple multi-catégories :**
```bash
man passwd              # Page man catégorie 1 (commande)
man 5 passwd            # Page man catégorie 5 (format fichier)
```

#### Info

Navigation similaire à man, mais avec hypertexte
```bash
info commande
?                       # Aide sur commandes info
```

#### Documentation système

**Emplacement :** `/usr/share/doc`
- Contient répertoires pour paquets installés
- Fichiers README ou readme.txt
- Documentation de base paquets
- Tout en texte brut (lisible tout éditeur)

---

### Leçon 2.3 : Navigation et liste de fichiers

#### Système de fichiers Linux

Structure hiérarchique commençant à la racine `/`

**Différence avec Windows :**
- Extensions n'ont pas de signification spéciale
- `.txt` peut contenir n'importe quel type de données

#### Commandes de navigation

```bash
pwd                     # Affiche répertoire travail actuel
cd repertoire           # Change de répertoire
cd ..                   # Répertoire parent (un niveau au-dessus)
cd ~                    # Répertoire personnel
cd /                    # Répertoire racine
```

**Chemins :**
- **Absolu** : Commence par `/` (ex: `/home/utilisateur/Documents`)
- **Relatif** : Par rapport à position actuelle (ex: `Documents` ou `../autre`)

#### Commande ls (list)

```bash
ls                      # Liste contenu répertoire
ls -a                   # Affiche fichiers cachés (commencent par .)
ls -l                   # Format long (détails)
ls -h                   # Tailles lisibles (Ko, Mo, Go)
ls -d                   # Liste répertoires, pas leur contenu
ls -r                   # Ordre inversé
ls -S                   # Trie par taille
ls -t                   # Trie par date modification
ls -X                   # Trie par extension
```

**Combinaison d'options :**
```bash
ls -lah                 # Long format, tout, lisible
```

---

### Leçon 2.4 : Création, déplacement et suppression

#### Sensibilité à la casse

Linux est sensible à la casse :
- `/ETC` ≠ `/etc` (répertoires différents)

#### Commandes de gestion

```bash
mkdir repertoire        # Créer répertoire
mkdir -p a/b/c          # Créer structure répertoires imbriqués

touch fichier           # Créer fichier vide / mettre à jour horodatage

echo "texte"            # Afficher texte
echo "texte" > fichier  # Écrire texte dans fichier

mv source destination   # Déplacer ou renommer
mv -i source dest       # Demander confirmation si écrasement

cp source destination   # Copier fichiers
cp -r source dest       # Copier répertoires récursivement

rm fichier              # Supprimer fichier
rm -r repertoire        # Supprimer répertoire récursivement
rm -f fichier           # Forcer suppression sans confirmation
rm -rf repertoire       # Supprimer répertoire force (DANGEREUX!)

rmdir repertoire        # Supprimer répertoire vide uniquement
```

#### Globbing (motifs)

Correspondance de motifs pour fichiers :

```bash
*                       # N'importe quel nombre de caractères
?                       # Un seul caractère
[abc]                   # Un des caractères a, b ou c
[a-z]                   # Un caractère de a à z
[!a]                    # Tout sauf a
```

**Exemples :**
```bash
ls *.txt                # Tous fichiers .txt
ls fichier?.txt         # fichier1.txt, fichierA.txt, etc.
ls [A-Z]*               # Fichiers commençant par majuscule
```

---

### Leçon 3.1 : Archivage de fichiers

#### Tar (Tape Archive)

Tar regroupe fichiers en un seul fichier (archive).

**Commandes principales :**
```bash
tar -cf archive.tar fichiers    # Créer archive
tar -xf archive.tar              # Extraire archive
tar -tf archive.tar              # Lister contenu
tar -rf archive.tar fichier      # Ajouter à archive
```

**Options compression :**
```bash
tar -czf archive.tar.gz fichiers # Compression gzip
tar -cjf archive.tar.bz2 fichiers # Compression bzip2
tar -cJf archive.tar.xz fichiers  # Compression xz
```

**Extraction avec compression :**
```bash
tar -xzf archive.tar.gz          # Extraire gzip
tar -xjf archive.tar.bz2         # Extraire bzip2
tar -xJf archive.tar.xz          # Extraire xz
```

#### Types de compression

**Lossy (avec perte)**
- Parties du fichier ne peuvent être récupérées
- Utilisé pour : images, vidéos, audio
- Perte généralement imperceptible pour humains

**Lossless (sans perte)**
- Fichier récupérable dans forme originale
- Utilisé pour : exécutables, fichiers logs, documents

**Niveaux de compression :**
1. **xz** : Meilleure compression (plus lent)
2. **bzip2** : Compression moyenne
3. **gzip** : Compression rapide (moins efficace)

#### Zip

```bash
zip archive.zip fichiers         # Créer archive zip
zip -r archive.zip repertoire    # Inclure répertoires
unzip archive.zip                # Extraire
```

- Disponible sur Windows et Linux
- Compression la plus faible mais plus rapide
- Option `-r` nécessaire pour répertoires

---

### Leçon 3.2 : Recherche et extraction de données

#### Redirections

**Canaux standard :**
- **STDIN** (0) : Entrée standard (clavier)
- **STDOUT** (1) : Sortie standard (écran)
- **STDERR** (2) : Erreurs (écran)

**Opérateurs de redirection :**
```bash
commande > fichier              # Redirige sortie (écrase)
commande >> fichier             # Ajoute à la fin
commande 2> fichier             # Redirige erreurs
commande &> fichier             # Redirige sortie ET erreurs
commande < fichier              # Lit depuis fichier
commande | autre_commande       # Pipe : sortie → entrée
```

**Exemples :**
```bash
ls > liste.txt                  # Liste fichiers dans fichier
cat fichier1 fichier2 > fusion  # Combine fichiers
cat < fichier                   # Affiche contenu
commande > /dev/null            # Rejette sortie
```

#### Commandes de manipulation

```bash
head fichier                    # 10 premières lignes
head -n 5 fichier               # 5 premières lignes

tail fichier                    # 10 dernières lignes
tail -n 20 fichier              # 20 dernières lignes
tail -f fichier                 # Suit fichier en temps réel

wc fichier                      # Compte lignes, mots, octets
wc -l fichier                   # Compte lignes uniquement
wc -w fichier                   # Compte mots
wc -c fichier                   # Compte octets
```

#### Grep (Global Regular Expression Print)

Recherche motifs dans fichiers.

```bash
grep motif fichier              # Recherche motif
grep -i motif fichier           # Insensible à la casse
grep -r motif repertoire        # Récursif
grep -v motif fichier           # Inverse (lignes sans motif)
grep -c motif fichier           # Compte occurrences
grep -n motif fichier           # Affiche numéros lignes
grep -E 'motif1|motif2' fichier # Expressions régulières étendues
```

**Expressions régulières :**
```bash
[abc]                           # Un de a, b ou c
[a-z]                           # Caractère de a à z
^motif                          # Début de ligne
motif$                          # Fin de ligne
.                               # N'importe quel caractère
.*                              # Zéro ou plus caractères
\                               # Échappe caractère spécial
*                               # Zéro ou plus occurrences précédent
[^abc]                          # Tout sauf a, b ou c
```

**Exemples :**
```bash
grep '^root' /etc/passwd        # Lignes commençant par root
grep 'error$' log.txt           # Lignes finissant par error
grep '^[A-Z]' fichier           # Lignes commençant par majuscule
```

---

### Leçon 3.3 : Transformer commandes en scripts

#### Création de scripts

**Scripts Bash :**
- Fichiers exécutables contenant commandes
- Doivent avoir permission d'exécution

**Étapes de création :**
```bash
touch mon_script.sh             # Créer fichier
chmod +x mon_script.sh          # Rendre exécutable
./mon_script.sh                 # Exécuter
```

#### Structure d'un script

```bash
#!/bin/bash                     # Shebang : Indique interpréteur

# Ceci est un commentaire

echo "Hello World"              # Commande
```

**Shebang :**
- Toujours première ligne
- Indique quel shell utiliser
- Format : `#!chemin/vers/interpreteur`

**Commentaires :**
- Commencent par `#`
- Ignorés lors exécution

#### Permissions

```bash
chmod u+x script.sh             # Exécutable pour utilisateur
chmod 755 script.sh             # rwxr-xr-x
ls -l script.sh                 # Vérifier permissions
```

**Format permissions :**
```
rwx | rwx | rwx
│     │     │
│     │     └─ Autres (4+2+1=7)
│     └─ Groupe (4+2+1=7)
└─ Propriétaire (4+2+1=7)
```

#### Variables dans scripts

```bash
#!/bin/bash

nom="Jean"                      # Variable locale
echo "Bonjour $nom"             # Utilisation

export PRENOM="Marie"           # Variable environnement
```

**Variables spéciales :**
```bash
$0                              # Nom du script
$1, $2, ...                     # Arguments positionnels
$#                              # Nombre d'arguments
$@                              # Tous les arguments (séparés)
$*                              # Tous les arguments (chaîne)
$?                              # Code sortie dernière commande
$$                              # PID du script
```

**Note :** Espaces = fin d'argument. Utiliser guillemets pour chaînes avec espaces.

#### Structures conditionnelles

```bash
if [ condition ]; then
    commandes
elif [ autre_condition ]; then
    autres_commandes
else
    commandes_par_defaut
fi
```

**Opérateurs de comparaison numériques :**
```bash
-eq                             # Égal
-ne                             # Différent
-gt                             # Plus grand que
-ge                             # Plus grand ou égal
-lt                             # Plus petit que
-le                             # Plus petit ou égal
```

**Exemples :**
```bash
if [ $# -eq 0 ]; then
    echo "Aucun argument"
fi

if [ -f fichier.txt ]; then
    echo "Fichier existe"
fi
```

#### Boucles

```bash
# Boucle for
for var in liste; do
    echo $var
done

# Exemple numérique
for i in {1..10}; do
    echo "Nombre: $i"
done
```

#### Codes de sortie

```bash
exit 0                          # Succès
exit 1                          # Erreur générique
exit 127                        # Commande non trouvée
```

**Vérifier code sortie :**
```bash
commande
echo $?                         # Affiche code sortie
```

#### Éditeurs de texte

**Vi/Vim**
- Éditeur traditionnel
- Modes : commande et insertion
- Navigation : `H J K L`
- Insertion : `I`
- Sauvegarder et quitter : `:wq`
- Quitter sans sauvegarder : `:q!`

**Nano**
- Éditeur simple et convivial
- Pas de modes séparés
- Raccourcis affichés en bas
- `Ctrl+O` : Sauvegarder
- `Ctrl+X` : Quitter

---

### Leçon 4.1 : Choix d'un système d'exploitation

#### Types de systèmes d'exploitation

**Basés Linux**

**Enterprise (Entreprise)**
- Déployés dans grandes organisations
- Matériel d'entreprise
- Stabilité matérielle/logicielle requise
- Versions anciennes du noyau (fiabilité)
- Support étendu :
  - Red Hat : 10 ans
  - Ubuntu LTS : 5 ans
- Exemples : Red Hat, CentOS, SUSE, Debian GNU/Linux, Ubuntu LTS

**Consumer Grade (Grand public)**
- Petites entreprises, maison, hobbyistes
- Pilotes récents pour nouveau matériel
- Support plus court :
  - Ubuntu non-LTS : 3 versions
- Exemples : Fedora, Ubuntu non-LTS, openSUSE

**Experimental / Hacker**
- Technologie de pointe
- Versions les plus récentes (bugs possibles)
- Modèle rolling release (mises à jour continues)
- Utilisateurs avancés
- Exemples : Arch, Gentoo, Kali

**Basés UNIX**
- Usage commercial généralement
- Exemples : AIX, Solaris, HP-UX
- Dérivés BSD : FreeBSD, NetBSD, OpenBSD
- macOS : Basé sur BSD Unix (Darwin)

**Basés Windows**
- Windows Server
- Windows Desktop
- Pas d'option ligne de commande seule

#### Linux sur serveurs

- Pratique courante grandes entreprises
- Souvent masqué (systèmes embarqués)
- Virtualisation/conteneurisation cache OS
- Client ne voit pas le backend

---

### Leçon 4.2 : Comprendre le matériel

#### Informations processeur

```bash
cat /proc/cpuinfo               # Infos détaillées processeur
lscpu                           # Résumé général CPU
```

#### Informations mémoire

```bash
free                            # Mémoire disponible
free -h                         # Format lisible (Go, Mo)
```

#### Périphériques de stockage

```bash
lsblk                           # Liste périphériques bloc (stockage)
```

**Convention nommage :**
- `/dev/sda` : Premier périphérique stockage entier
- `/dev/sda1` : Première partition du périphérique
- `/dev/sda3` : Troisième partition
- `mmcblk` : Cartes SD (ex: Raspberry Pi)

#### Répertoire /dev

Emplacement des fichiers périphériques :
- Identifient périphériques physiques
- Accès aux périphériques
- Pilotes supportés

---

### Leçon 4.3 : Stockage des données

#### Structure Linux

**Racine : /**
Point de départ structure répertoires Linux

**FHS (Filesystem Hierarchy Standard)**
Établit comment données sont stockées

#### Répertoires principaux

**/bin**
- Binaires pour tous utilisateurs
- Exemples : `ls`, `mv`, `mkdir`

**/sbin**
- Binaires pour administrateurs système
- Exemples : `parted`, `ip`, `deluser`, `groupadd`

**/usr/bin**
- Fichiers exécutables
- Exemples : `free`, `pstree`, `sudo`

**/etc**
Fichiers de configuration système

Fichiers importants :
- `group` : Base de données groupes système
- `hostname` : Nom ordinateur hôte
- `hosts` : Correspondance IP ↔ noms d'hôte
- `passwd` : Base données utilisateurs système
- `profile` : Configuration système pour bash
- `shadow` : Mots de passe utilisateurs chiffrés
- `bash.bashrc` : Configuration shellbash interactifs
- `nanorc` : Initialisation GNU nano
- `sysctl.conf` : Variables système pour noyau

**/etc/skel**
- Répertoire "squelette"
- Fichiers par défaut nouveaux utilisateurs
- Copié lors création compte

**Fichiers cachés répertoire home**
Commencent par `.` (point)

Fichiers configuration utilisateur :
- `.bash_history` : Historique commandes
- `.bash_logout` : Commandes à exécution lors déconnexion
- `.bashrc` : Initialisation Bash (non-login shells)
- `.profile` : Initialisation Bash (login shells)

**/boot**
- Noyau Linux
- Chargeur démarrage
- Sous-répertoire `grub` : Configuration GRUB2

**/proc**
Système fichiers virtuel
- Informations processus en cours
- Configuration noyau
- Matériel système
- Exemples :
  - `/proc/cpuinfo` : Informations processeur

**/dev**
Fichiers périphériques
- `/dev/sda1` : Périphériques bloc
- `/dev/console` : Console clavier/texte
- `/dev/zero` : Caractères null
- `/dev/null` : Corbeille bits (rejette tout)
- `/dev/urandom` : Nombres pseudo-aléatoires

**/sys**
Système fichiers virtuel
- Données organisées par catégories
- Facilite interactions processus ↔ périphériques

**/tmp**
- Fichiers temporaires
- Effacé entre sessions démarrage
- Matériel NON garanti persistant

**/var/tmp**
- Fichiers temporaires
- Persistent entre redémarrages

**/var**
- Données variables (logs, caches)
- `/var/log` : Journaux système

**/home**
- Répertoires personnels utilisateurs
- `/home/utilisateur`

**/root**
- Répertoire personnel root
- Séparé de `/home`

**/usr/local**
- Programmes installés localement
- Non gérés par gestionnaire paquets

#### Swap

Espace d'échange : Mémoire virtuelle sur disque dur quand RAM saturée

#### Processus d'initialisation

**Historique :**
- Ancien : `/sbin/init` (PID 1)
- Moderne : `/lib/systemd/systemd` (PID 1)

PID 1 lance chaîne de processus système

---

### Leçon 4.4 : Réseau

#### Modèle OSI vs TCP/IP

**Modèle OSI (7 couches) :**
1. Physique
2. Liaison de données (Data Link)
3. Réseau (Network)
4. Transport
5. Session
6. Présentation
7. Application

**Modèle TCP/IP (4 couches) :**
1. Accès réseau / Liaison
2. Internet / Réseau
3. Transport
4. Application

#### Encapsulation données

**Frame (Trame)**
- Couche 2 (Liaison)
- Contient adresses MAC
- Vérification erreurs

**Packet (Paquet)**
- Couche 3 (Réseau)
- Contient adresses IP
- Informations protocole
- Données contrôle

**Segment**
- Couche 4 (Transport)
- Ports source/destination
- Numéros séquence
- Somme contrôle (checksum)

#### Adresses réseau

**Adresses MAC**
- Couche liaison
- Unique pour chaque interface réseau

**Adresses IP**
- IPv4 : 32 bits (ex: 192.168.1.1)
- IPv6 : 128 bits (ex: 2001:0db8::1)

#### Commandes réseau

```bash
ip addr                         # Liste interfaces et adresses
ip link                         # Infos interfaces réseau

ping adresse                    # Test connectivité IPv4
ping6 adresse                   # Test connectivité IPv6

dig domaine                     # Requête DNS détaillée
dig -A domaine                  # Enregistrements A (IPv4)

ss                              # Informations sockets
ss -tuln                        # TCP/UDP, numériques, écoute

route                           # Table routage IPv4
ip route                        # Table routage (nouvelle syntaxe)
```

#### NAT (Network Address Translation)

- Mappe adresses internes → adresse IP externe unique
- Masquerading
- Permet périphériques réseau privé accéder Internet

#### DHCP (Dynamic Host Configuration Protocol)

- Attribution automatique adresses IP
- Configuration lors connexion réseau

**Ajout manuel adresse IP :**
```bash
ip addr add 192.168.1.100/24 dev eth0
```

#### DNS (Domain Name System)

- Système distribué
- Traduit noms domaine → adresses IP
- Annuaire téléphonique Internet

**Fichiers configuration :**
- `/etc/resolv.conf` : Configuration DNS
- `/etc/hosts` : Correspondances locales nom ↔ IP

**Résolution :**
1. Vérifier `/etc/hosts`
2. Si absent, requête DNS

#### IPv6

**Structure adresse :**
- 128 bits
- Premiers 64 bits : Préfixe routage (site prefix)
- Bits suivants : ID sous-réseau
- Derniers bits : Identifiant interface

**Adresse link-local :**
- Commence par `fe80::`
- Permet demander adresses supplémentaires
- Neighbor Discovery Protocol

**Configuration automatique :**
- **SLAAC** (Stateless Address Autoconfiguration)
  - Routeur annonce préfixes
  - Périphérique crée propre adresse
- **DHCPv6**
  - Contrôle plus fin
  - Même adresse garantie
  - Options supplémentaires

#### Routage

Processus acheminement paquets réseau source → destination

**Tables de routage :**
- Consultées à chaque transmission
- Déterminent prochain saut (next hop)

#### Sockets

Point de terminaison communication entre deux programmes

**Types :**
- **TCP** : Fiable, ordonné, plus lent
  - Applications : FTP, navigation web, email
- **UDP** : Rapide, non garanti
  - Applications : streaming, jeux, VoIP

**Types de communication :**
- Unicast : Un destinataire
- Multicast : Groupe destinataires
- Broadcast : Tous sur réseau

#### Ports

Numéros identifiant services/applications :
- **0-1023** : Ports bien connus (système)
- **1024-49151** : Ports enregistrés
- **49152-65535** : Ports dynamiques/privés

---

### Leçon 4.5 : Sécurité système

#### Identifiants utilisateur (UID)

**Utilisateurs normaux**
- UID ≥ 1000 (≥ 500 sur systèmes anciens)
- Groupe utilisateur même nom que utilisateur
- Répertoire personnel défini (généralement `/home/utilisateur`)
- Shell de connexion défini

**Utilisateurs système**
- Créés lors installation ou installation service
- Plusieurs types :
  - UID < 100 : Comptes système statiques
  - UID 100-999 : Comptes services
- Pas de répertoire dédié (ou hors `/home`)
- Généralement pas de shell valide

**Utilisateurs services**
- Créés lors installation service
- Ne s'exécutent pas en superutilisateur
- Répertoire hors `/home`

#### Fichiers utilisateurs

**/etc/passwd**
Format: `nom:x:UID:GID:commentaire:home:shell`
- Informations utilisateur de base
- UID, GID, répertoire personnel, shell

**/etc/group**
Format: `nom:x:GID:membres`
- Informations groupes

**/etc/shadow**
- Mots de passe hachés
- Accessible uniquement root
- Format: `nom:hash:...`
- `!` ou `*` : Compte désactivé

**/etc/gshadow**
- Informations détaillées groupes
- Mots de passe groupe hachés
- Permet adhésion temporaire groupe

**/etc/sudoers**
- Contrôle qui peut utiliser `sudo`
- Éditer avec `visudo` (vérifie syntaxe)

**/etc/sudoers.d/**
- Répertoire fichiers config sudo supplémentaires

#### Champ GECOS

Dans `/etc/passwd`, contient :
- Nom complet
- Emplacement
- Contact

**Modifier :**
```bash
chfn utilisateur
```

#### Commandes gestion utilisateurs

```bash
useradd utilisateur             # Ajouter utilisateur
useradd -m utilisateur          # Avec répertoire personnel
useradd -s /bin/bash user       # Avec shell spécifique
useradd -G groupe user          # Avec groupes secondaires
useradd -c "Commentaire" user   # Avec commentaire
useradd -e 2025-12-31 user      # Avec date expiration

userdel utilisateur             # Supprimer utilisateur
userdel -r utilisateur          # Supprimer avec répertoire personnel

passwd utilisateur              # Changer mot de passe
passwd -l utilisateur           # Verrouiller compte (ajoute !)
passwd -u utilisateur           # Déverrouiller compte
passwd -d utilisateur           # Supprimer mot de passe
passwd -e utilisateur           # Forcer changement MDP
passwd -S utilisateur           # Statut mot de passe
```

#### Commandes gestion groupes

```bash
groupadd groupe                 # Créer groupe
groupadd -g 1500 groupe         # Avec GID spécifique

groupdel groupe                 # Supprimer groupe

usermod -G groupe user          # Ajouter utilisateur à groupe
gpasswd -a user groupe          # Ajouter utilisateur à groupe
gpasswd -d user groupe          # Retirer utilisateur de groupe
```

#### Commandes information

```bash
whoami                          # Utilisateur actuel
id                              # UID, GID, groupes utilisateur actuel
id utilisateur                  # Infos utilisateur spécifique

groups                          # Groupes utilisateur actuel
groups utilisateur              # Groupes utilisateur spécifique

who                             # Utilisateurs connectés
w                               # Utilisateurs et activités
last                            # Historique connexions
lastb                           # Historique échecs connexion

uptime                          # Durée fonctionnement système
```

#### Permissions fichiers

**Lecture de permissions :**
```
-rwxrwxr-x
│││││││││└─ Autres : Exécution
│││││││└──  Autres : Écriture (non)
││││││└───  Autres : Lecture
│││││└────  Groupe : Exécution
││││└─────  Groupe : Écriture
│││└──────  Groupe : Lecture
││└───────  Utilisateur : Exécution
│└────────  Utilisateur : Écriture
└─────────  Utilisateur : Lecture
```

**Types de fichiers :**
- `-` : Fichier normal
- `d` : Répertoire
- `l` : Lien symbolique
- `b` : Périphérique bloc
- `c` : Périphérique caractère
- `s` : Socket

**Valeurs octales :**
- `4` : Lecture (r)
- `2` : Écriture (w)
- `1` : Exécution (x)

**Exemples :**
- `7` = rwx (4+2+1)
- `6` = rw- (4+2)
- `5` = r-x (4+1)
- `0` = --- (aucune)

**Permissions sur répertoires :**
- **r** : Lister contenu (pas lire fichiers)
- **w** : Créer/supprimer fichiers, modifier noms/permissions
- **x** : Entrer dans répertoire (cd)

#### Commandes permissions

```bash
chmod 755 fichier               # Mode numérique
chmod u+x fichier               # Mode symbolique (user +exec)
chmod g-w fichier               # Groupe -write
chmod o=r fichier               # Autres =read
chmod a+x fichier               # All +exec
chmod -R 755 repertoire         # Récursif

chown utilisateur fichier       # Changer propriétaire
chown user:group fichier        # Changer proprio et groupe
chown -R user repertoire        # Récursif

chgrp groupe fichier            # Changer groupe
```

**Mode symbolique :**
- **u** : User (propriétaire)
- **g** : Group (groupe)
- **o** : Others (autres)
- **a** : All (tous)
- **+** : Ajouter permission
- **-** : Retirer permission
- **=** : Définir exactement

#### Bits spéciaux

**Sticky Bit**
- Valeur octale : `1`
- Symbole : `t` (remplace x dans autres)
- Application : Répertoires
- Effet : Seul propriétaire peut supprimer/renommer fichier
- Exemple : `chmod 1755 repertoire` → `drwxr-xr-t`

**SGID (Set Group ID)**
- Valeur octale : `2`
- Symbole : `s` (remplace x dans groupe)
- **Sur répertoire** : Fichiers créés héritent groupe du répertoire
- **Sur fichier exécutable** : Exécuté avec permissions du groupe
- Exemple : `chmod 2755 repertoire` → `drwxr-sr-x`

**SUID (Set User ID)**
- Valeur octale : `4`
- Symbole : `s` (remplace x dans utilisateur)
- Application : Fichiers exécutables
- Effet : Processus exécuté avec privilèges propriétaire fichier
- Exemple : `chmod 4755 fichier` → `-rwsr-xr-x`

**Combinaisons :**
- SUID + SGID : `6755` → `-rwsr-sr-x`
- SUID + Sticky : `5755` → `-rwsr-xr-t`
- SGID + Sticky : `3755` → `-rwxr-sr-t`
- Tous : `7755` → `-rwsr-sr-t`

#### Liens (Links)

**Hard Links (Liens durs)**
- Pointent vers inode (structure données fichier)
- Chaque hard link augmente compteur liens
- Ne cassent pas si source déplacée
- Cible doit exister
- Chemin complet si hors répertoire actuel
- Ne fonctionnent pas entre systèmes fichiers

```bash
ln fichier_source lien           # Créer hard link
ls -li                           # Voir inodes et compteur liens
```

**Soft Links / Symbolic Links (Liens symboliques)**
- Pointent vers chemin fichier
- Cassent si source déplacée/supprimée
- Fonctionnent avec répertoires
- Identifiables : `l` au début permissions
- Chemin relatif : relatif à emplacement lien

```bash
ln -s fichier_source lien        # Créer lien symbolique
ls -l                            # Voir liens (affiche ->)
```

**Différences clés :**
| Aspect | Hard Link | Soft Link |
|--------|-----------|-----------|
| Pointe vers | Inode | Chemin |
| Répertoires | Non | Oui |
| Entre systèmes fichiers | Non | Oui |
| Si source supprimée | Fonctionne | Cassé |
| Identifiable ls -l | Non | Oui (l) |

---

## Conclusion

Ce cours couvre les fondamentaux nécessaires pour la certification Linux Essentials LPI. Les sujets incluent :

1. **Communauté et Open Source** : Histoire Linux, distributions, licences
2. **Navigation système** : Ligne de commande, système fichiers, aide
3. **Puissance terminal** : Manipulation fichiers, recherche, scripts
4. **Système d'exploitation** : Architecture, matériel, réseau
5. **Sécurité** : Utilisateurs, groupes, permissions, chiffrement

Pour réussir l'examen :
- Pratiquer régulièrement les commandes
- Comprendre les concepts, pas seulement mémoriser
- Utiliser les flashcards pour révision
- Faire les exercices pratiques
- Travailler sur un système Linux réel

Bonne chance pour votre certification !
