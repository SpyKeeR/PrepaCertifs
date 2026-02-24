# 📘 Notes de Révision - Sujet 103 : Commandes GNU et Unix

> **Poids du sujet :** 16 points (~40% de l'examen) - **LE PLUS IMPORTANT !**  
> **Temps de lecture estimé :** 4-6 heures  
> **Niveau :** Fondamental - Compétences ESSENTIELLES administrateur Linux !

---

## 📋 Table des matières

- [103.1 - Travail en ligne de commande (Poids: 4)](#1031---travail-en-ligne-de-commande)
- [103.2 - Traitement de flux texte avec filtres (Poids: 2)](#1032---traitement-de-flux-texte-avec-filtres)
- [103.3 - Gestion de base des fichiers (Poids: 4)](#1033---gestion-de-base-des-fichiers)
- [103.4 - Flux, pipes et redirections (Poids: 4)](#1034---flux-pipes-et-redirections)
- [103.5 - Création, surveillance et terminaison de processus (Poids: 4)](#1035---création-surveillance-et-terminaison-de-processus)
- [103.6 - Modification des priorités d'exécution (Poids: 2)](#1036---modification-des-priorités-dexécution)
- [103.7 - Recherche avec expressions régulières (Poids: 3)](#1037---recherche-avec-expressions-régulières)
- [103.8 - Édition basique de fichiers (Poids: 3)](#1038---édition-basique-de-fichiers)

---

## 103.1 - Travail en ligne de commande

### 🎯 Objectifs clés
- Maîtriser le shell Bash
- Utiliser variables d'environnement
- Comprendre l'historique des commandes
- Gérer les commandes et leur exécution

### 🐚 Shell Bash - Concepts fondamentaux

#### Variables Bash

**Définir et utiliser variables :**
```bash
# Définir variable (pas d'espaces autour du =)
NAME="John"
AGE=30

# Utiliser variable
echo $NAME
echo ${NAME}    # Recommandé (évite ambiguïtés)

# Concaténation
FULL="Mr. ${NAME}"
echo $FULL

# Commande dans variable
DATE=$(date +%Y%m%d)
FILES=`ls -1 | wc -l`    # Ancienne syntaxe (backticks)
echo "Today: $DATE, Files: $FILES"
```

**Variables d'environnement :**
```bash
# Afficher toutes les variables d'environnement
env
printenv

# Afficher variable spécifique
echo $HOME
echo $PATH
printenv USER

# Variables importantes :
$HOME      # Répertoire utilisateur (/home/user)
$USER      # Nom utilisateur
$PATH      # Chemins de recherche commandes
$SHELL     # Shell actuel (/bin/bash)
$PWD       # Répertoire courant
$OLDPWD    # Répertoire précédent
$LANG      # Langue système
$HOSTNAME  # Nom machine
$UID       # User ID
$EUID      # Effective User ID

# Exporter variable (disponible pour processus fils)
export MY_VAR="value"

# Variable temporaire (une commande)
MY_VAR="test" command

# Supprimer variable
unset MY_VAR
```

**Variables spéciales :**
```bash
$0    # Nom du script
$1-$9 # Arguments 1 à 9
${10} # Argument 10+ (accolades requises)
$#    # Nombre d'arguments
$@    # Tous les arguments (array)
$*    # Tous les arguments (string)
$$    # PID du shell actuel
$!    # PID dernier processus background
$?    # Code retour dernière commande (0=succès)
$_    # Dernier argument de la commande précédente
```

**Exemple script :**
```bash
#!/bin/bash
echo "Script: $0"
echo "User: $USER"
echo "Args: $#"
echo "First arg: $1"
echo "All args: $@"
echo "PID: $$"
```

#### PATH et recherche de commandes

**Variable PATH :**
```bash
# Afficher PATH
echo $PATH
# /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

# Ordre de recherche (premier trouvé = exécuté)
# Chemins séparés par :

# Ajouter répertoire au PATH (temporaire)
export PATH=$PATH:/opt/bin

# Ajouter en début de PATH (prioritaire)
export PATH=/opt/bin:$PATH

# PATH permanent (~/.bashrc ou ~/.profile)
echo 'export PATH=$PATH:/opt/myapp/bin' >> ~/.bashrc
source ~/.bashrc
```

**Chercher commandes :**
```bash
# Trouver chemin d'une commande
which python3
# /usr/bin/python3

# Chercher plusieurs emplacements
which -a python3
# /usr/bin/python3
# /usr/local/bin/python3

# Type de commande (builtin, alias, file)
type ls
# ls is aliased to `ls --color=auto'

type cd
# cd is a shell builtin

type python3
# python3 is /usr/bin/python3

# Tous les emplacements
type -a ls

# Chercher dans PATH
whereis python3
# python3: /usr/bin/python3 /usr/lib/python3 /usr/share/man/man1/python3.1.gz

# Localiser fichier (base de données)
locate python3
# (nécessite updatedb)
```

#### Commandes intégrées (builtins)

**Liste des builtins importants :**
```bash
# Afficher tous les builtins
help
compgen -b

# Builtins courants :
cd          # Changer répertoire
pwd         # Afficher répertoire
echo        # Afficher texte
read        # Lire entrée
set         # Définir options shell
unset       # Supprimer variable
export      # Exporter variable
alias       # Créer alias
unalias     # Supprimer alias
history     # Historique commandes
source      # Exécuter script dans shell actuel
.           # Alias de source
exit        # Quitter shell
logout      # Déconnecter
exec        # Remplacer shell par commande
```

**Aide sur builtins :**
```bash
# Aide builtin
help cd
help echo

# Man pages (commandes externes)
man ls
man grep
```

#### Alias

**Créer et gérer alias :**
```bash
# Créer alias
alias ll='ls -lah'
alias gs='git status'
alias ..='cd ..'
alias ...='cd ../..'

# Lister alias
alias

# Supprimer alias
unalias ll

# Utiliser commande sans alias (bypass)
\ls         # Exécute ls, ignore alias
command ls  # Idem

# Alias permanents (~/.bashrc)
echo "alias ll='ls -lah'" >> ~/.bashrc
source ~/.bashrc
```

**Alias utiles courants :**
```bash
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias mkdir='mkdir -pv'
alias ports='netstat -tulanp'
alias update='sudo apt update && sudo apt upgrade'
```

#### Historique des commandes

**Commande `history` :**
```bash
# Afficher historique
history

# Dernières N commandes
history 20

# Exécuter commande N
!42

# Dernière commande
!!

# Dernière commande commençant par 'ssh'
!ssh

# Dernier argument commande précédente
cd /var/log
ls -l !$    # !$ = /var/log

# Tous les arguments précédents
command !*

# Recherche interactive (Ctrl+R)
# Ctrl+R puis taper début commande

# Effacer historique
history -c
history -w    # Sauvegarder

# Supprimer entrée N
history -d 42
```

**Configuration historique (~/.bashrc) :**
```bash
# Taille historique
HISTSIZE=10000         # En mémoire
HISTFILESIZE=20000     # Sur disque

# Fichier historique
HISTFILE=~/.bash_history

# Contrôle
HISTCONTROL=ignoredups:ignorespace
# ignoredups  : Ignorer doublons consécutifs
# ignorespace : Ignorer commandes commençant par espace
# ignoreboth  : Les deux

# Format timestamp
HISTTIMEFORMAT="%F %T "

# Ne pas enregistrer certaines commandes
HISTIGNORE="ls:ll:cd:pwd:exit:clear:history"
```

**Recherche historique :**
```bash
# Recherche inversée (Ctrl+R)
# Ctrl+R puis taper texte

# Recherche avant (Ctrl+S)
# (peut nécessiter stty -ixon)

# Éditer dernière commande
fc

# Éditer et exécuter commande N
fc 42

# Liste commandes récentes
fc -l

# Rechercher dans historique
history | grep ssh
```

#### Exécution de commandes

**Séquencement :**
```bash
# Commandes séquentielles (;)
cd /tmp; ls -l; pwd

# ET logique (&&) - exécute si précédente réussie
make && make install

# OU logique (||) - exécute si précédente échoue
cd /nonexistent || echo "Failed"

# Combinaisons
command1 && command2 || command3

# Grouper commandes
(cd /tmp && ls)    # Sous-shell
{ cd /tmp; ls; }   # Shell actuel (attention aux ;)
```

**Background et foreground :**
```bash
# Lancer en arrière-plan (&)
sleep 60 &

# Suspendre commande (Ctrl+Z)
# Met en pause

# Lister jobs
jobs
# [1]+ Running    sleep 60 &

# Reprendre en background
bg %1

# Reprendre en foreground
fg %1

# Tuer job
kill %1

# Détacher processus (nohup)
nohup long_command &
# Continue après déconnexion
# Sortie dans nohup.out
```

**Commandes conditionnelles :**
```bash
# Tester succès
command && echo "Success"

# Tester échec
command || echo "Failed"

# If complet
if command; then
    echo "Success"
else
    echo "Failed"
fi

# Test code retour
command
if [ $? -eq 0 ]; then
    echo "Success"
fi
```

#### Expansion et substitution

**Expansion de paramètres :**
```bash
# Valeur par défaut
echo ${VAR:-default}      # Si VAR vide, affiche "default"
echo ${VAR:=default}      # Idem + assigne default à VAR

# Erreur si vide
echo ${VAR:?error message}

# Longueur
NAME="John"
echo ${#NAME}    # 4

# Substitution
FILE="document.txt"
echo ${FILE%.txt}        # document (supprime .txt)
echo ${FILE%.*}          # document (supprime extension)
echo ${FILE#*.}          # txt (supprime avant .)
echo ${FILE/doc/file}    # filement.txt (remplace)
```

**Expansion de chemins (globbing) :**
```bash
# * = n'importe quels caractères
ls *.txt
ls file*

# ? = un caractère
ls file?.txt

# [] = plage de caractères
ls file[123].txt
ls [a-z]*.txt

# {} = liste
ls {file1,file2,file3}.txt
echo {1..10}
echo {a..z}

# ** = récursif (bash 4+, avec globstar)
shopt -s globstar
ls **/*.txt
```

**Substitution de commandes :**
```bash
# Moderne $()
DATE=$(date +%Y%m%d)
FILES=$(ls -1 | wc -l)

# Ancienne `backticks`
DATE=`date +%Y%m%d`

# Imbrication (plus lisible avec $())
RESULT=$(echo $(date +%Y) is the year)

# Exemples pratiques
echo "Uptime: $(uptime)"
echo "Users: $(who | wc -l)"
find $(pwd) -name "*.log"
```

**Expansion arithmétique :**
```bash
# $(( expression ))
echo $((2 + 3))        # 5
echo $((10 * 5))       # 50

# Avec variables
A=5
B=3
echo $((A + B))        # 8
echo $((A * B))        # 15

# Incrément
COUNT=0
((COUNT++))
echo $COUNT            # 1

# Dans boucles
for ((i=0; i<10; i++)); do
    echo $i
done
```

#### Caractères spéciaux et échappement

**Quotes :**
```bash
# Simples quotes ' ' - littéral
echo 'Hello $USER'     # Hello $USER

# Doubles quotes " " - expansion
echo "Hello $USER"     # Hello john

# Sans quotes - expansion + split
VAR="a b c"
echo $VAR              # a b c (split)
echo "$VAR"            # a b c (préservé)

# Backslash \ - échappe un caractère
echo \$HOME            # $HOME
echo "Price: \$5"      # Price: $5
```

**Caractères spéciaux :**
```bash
#  Commentaire
;  Séparateur commandes
&  Arrière-plan
|  Pipe
>  Redirection sortie
<  Redirection entrée
*  Wildcard (tous caractères)
?  Wildcard (un caractère)
[] Classe de caractères
{} Expansion liste
() Sous-shell
$  Variable
\  Échappement
'  Quote simple (littéral)
"  Quote double (expansion)
`  Substitution (ancien)
!  Historique
~  Home directory
```

---

## 103.2 - Traitement de flux texte avec filtres

### 🎯 Objectifs clés
- Filtrer et transformer texte avec commandes standard
- Chaîner commandes avec pipes
- Manipuler colonnes et champs

### 📝 Commandes de filtrage texte

#### `cat` - Concatenate

```bash
# Afficher fichier
cat file.txt

# Plusieurs fichiers
cat file1.txt file2.txt

# Numéroter lignes
cat -n file.txt

# Numéroter lignes non vides
cat -b file.txt

# Afficher caractères non imprimables
cat -A file.txt
# $ = fin de ligne
# ^I = tab

# Supprimer lignes vides multiples
cat -s file.txt

# Créer fichier (EOF = End Of File)
cat > file.txt << EOF
Line 1
Line 2
EOF

# Ajouter à fichier
cat >> file.txt << EOF
Line 3
EOF
```

#### `tac` - Reverse cat

```bash
# Afficher fichier à l'envers (dernière ligne en premier)
tac file.txt

# Utile pour logs (récent d'abord)
tac /var/log/syslog | head -20
```

#### `head` et `tail`

```bash
# Premières 10 lignes (défaut)
head file.txt

# Premières N lignes
head -n 20 file.txt
head -20 file.txt

# Premières N bytes
head -c 100 file.txt

# Dernières 10 lignes
tail file.txt

# Dernières N lignes
tail -n 50 file.txt
tail -50 file.txt

# Depuis ligne N
tail -n +10 file.txt    # Depuis ligne 10

# Suivre fichier en temps réel (logs)
tail -f /var/log/syslog
tail -f /var/log/apache2/access.log

# Suivre avec retry (fichier recréé)
tail -F /var/log/syslog

# Combiner head et tail
head -100 file.txt | tail -20    # Lignes 81-100
```

#### `cut` - Extraire colonnes

```bash
# Par caractères
cut -c 1-5 file.txt          # Caractères 1 à 5
cut -c 1,5,10 file.txt       # Caractères 1, 5 et 10

# Par champs (délimiteur tab par défaut)
cut -f 1,3 file.txt          # Champs 1 et 3

# Délimiteur personnalisé
cut -d ':' -f 1 /etc/passwd  # Premier champ (username)
cut -d ':' -f 1,3,6 /etc/passwd  # Username, UID, home

# Complémentaire (tous sauf)
cut -d ':' -f 1 --complement /etc/passwd

# Exemples pratiques
# Extraire IPs
cut -d ' ' -f 1 access.log

# Extraire usernames
cut -d ':' -f 1 /etc/passwd | sort
```

#### `paste` - Fusionner lignes

```bash
# Fusionner fichiers côte à côte
paste file1.txt file2.txt
# file1-line1    file2-line1
# file1-line2    file2-line2

# Délimiteur personnalisé
paste -d ',' file1.txt file2.txt
# file1-line1,file2-line1

# Transposer lignes en colonnes
paste -s file.txt
# line1    line2    line3

# Exemple : combiner noms et âges
paste names.txt ages.txt
```

#### `tr` - Translate/Replace caractères

```bash
# Remplacer caractères
echo "hello" | tr 'a-z' 'A-Z'    # HELLO
echo "HELLO" | tr 'A-Z' 'a-z'    # hello

# Supprimer caractères
echo "hello123" | tr -d '0-9'    # hello

# Compresser répétitions
echo "hello    world" | tr -s ' '    # hello world

# Supprimer newlines
cat file.txt | tr -d '\n'

# ROT13 (chiffrement simple)
echo "Hello" | tr 'A-Za-z' 'N-ZA-Mn-za-m'

# Exemples pratiques
# Convertir Windows (CRLF) vers Unix (LF)
tr -d '\r' < windows.txt > unix.txt

# Remplacer espaces par underscores
echo "hello world" | tr ' ' '_'    # hello_world

# Supprimer ponctuation
cat file.txt | tr -d '[:punct:]'
```

#### `wc` - Word Count

```bash
# Compter lignes, mots, bytes
wc file.txt
# 10  50  300 file.txt
# lignes mots bytes

# Lignes seulement
wc -l file.txt

# Mots seulement
wc -w file.txt

# Bytes
wc -c file.txt

# Caractères (UTF-8)
wc -m file.txt

# Exemples pratiques
# Compter fichiers dans répertoire
ls -1 | wc -l

# Compter utilisateurs connectés
who | wc -l

# Compter lignes non vides
grep -v '^$' file.txt | wc -l

# Plus long fichier
wc -l *.txt | sort -n | tail -1
```

#### `sort` - Trier lignes

```bash
# Tri alphabétique
sort file.txt

# Tri numérique
sort -n numbers.txt

# Tri inverse
sort -r file.txt

# Tri par colonne (champ)
sort -k 2 file.txt              # 2ème colonne
sort -k 2,2 file.txt            # Seulement 2ème colonne

# Tri numérique par colonne
sort -k 3 -n file.txt

# Délimiteur personnalisé
sort -t ':' -k 3 -n /etc/passwd # Tri par UID

# Supprimer doublons
sort -u file.txt

# Ignorer casse
sort -f file.txt

# Tri humain (1K, 2M, 3G)
du -h | sort -h

# Exemples pratiques
# Top 10 IPs dans logs
cut -d ' ' -f 1 access.log | sort | uniq -c | sort -rn | head -10

# Trier fichiers par taille
ls -lh | sort -k 5 -h

# Trier /etc/passwd par UID
sort -t ':' -k 3 -n /etc/passwd
```

#### `uniq` - Supprimer/compter doublons

```bash
# Supprimer doublons consécutifs (nécessite sort avant)
sort file.txt | uniq

# Compter occurrences
sort file.txt | uniq -c

# Afficher seulement doublons
sort file.txt | uniq -d

# Afficher seulement uniques
sort file.txt | uniq -u

# Ignorer N premiers caractères
uniq -s 5 file.txt

# Ignorer N premiers champs
uniq -f 2 file.txt

# Exemples pratiques
# Top 10 commandes utilisées
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10

# IPs uniques dans logs
cut -d ' ' -f 1 access.log | sort | uniq

# Lignes dupliquées
sort file.txt | uniq -d
```

#### `split` - Diviser fichiers

```bash
# Diviser en fichiers de 1000 lignes
split -l 1000 largefile.txt part_

# Diviser par taille (bytes)
split -b 100M largefile.iso part_

# Taille humaine
split -b 10M largefile.txt part_

# Préfixe et suffixe personnalisés
split -l 1000 file.txt output_ --additional-suffix=.txt

# Suffixe numérique
split -l 1000 -d file.txt part_
# part_00, part_01, part_02...

# Exemples pratiques
# Diviser CSV en chunks
split -l 10000 data.csv chunk_

# Reconstituer
cat chunk_* > data_restored.csv
```

#### `nl` - Numéroter lignes

```bash
# Numérotation simple
nl file.txt

# Format personnalisé
nl -w 4 -s ': ' file.txt
# 0001: ligne 1
# 0002: ligne 2

# Ne pas numéroter lignes vides
nl -b a file.txt    # Tout
nl -b t file.txt    # Seulement non-vides
```

#### `od` - Octal Dump

```bash
# Affichage octal
od file.bin

# Hexadécimal
od -x file.bin

# Décimal
od -d file.bin

# ASCII
od -c file.bin

# Examiner binaire
od -A x -t x1z -v binary_file
```

---

## 103.3 - Gestion de base des fichiers

### 🎯 Objectifs clés
- Créer, copier, déplacer, supprimer fichiers
- Gérer liens symboliques et durs
- Utiliser globbing et patterns

### 📁 Commandes de gestion fichiers

#### `ls` - Lister fichiers

```bash
# Liste simple
ls

# Liste détaillée
ls -l

# Tout (inclus cachés)
ls -a
ls -A    # Sauf . et ..

# Combiné
ls -la

# Taille humaine
ls -lh

# Tri par date (récent d'abord)
ls -lt

# Tri par taille
ls -lS

# Tri inverse
ls -lr

# Récursif
ls -R

# Un fichier par ligne
ls -1

# Afficher inode
ls -i

# Type de fichier
ls -F
# / = répertoire
# * = exécutable
# @ = lien symbolique
# | = pipe
# = = socket

# Couleurs
ls --color=auto

# Exemples pratiques
# Fichiers récents
ls -lt | head -10

# Plus gros fichiers
ls -lhS | head -10

# Fichiers modifiés aujourd'hui
ls -la --time-style=+%Y-%m-%d | grep $(date +%Y-%m-%d)
```

#### `cp` - Copier

```bash
# Copier fichier
cp source.txt dest.txt

# Copier dans répertoire
cp file.txt /tmp/

# Copier plusieurs fichiers
cp file1.txt file2.txt /tmp/

# Copier répertoire (récursif)
cp -r dir1/ dir2/

# Préserver attributs (permissions, timestamps)
cp -p file.txt backup.txt

# Archive (= -dR --preserve=all)
cp -a dir1/ backup/

# Interactif (demander confirmation)
cp -i file.txt existing.txt

# Verbose
cp -v file.txt /tmp/

# Mise à jour (copie seulement si plus récent)
cp -u source/* dest/

# Créer lien dur au lieu de copier
cp -l file.txt hardlink.txt

# Lien symbolique
cp -s file.txt symlink.txt

# Exemples pratiques
# Backup avec date
cp -p file.txt file.txt.$(date +%Y%m%d)

# Copier préservant structure
cp --parents dir1/dir2/file.txt /backup/

# Copier seulement si absent
cp -n source.txt dest.txt
```

#### `mv` - Déplacer/Renommer

```bash
# Renommer fichier
mv old.txt new.txt

# Déplacer fichier
mv file.txt /tmp/

# Déplacer plusieurs fichiers
mv file1.txt file2.txt /tmp/

# Déplacer répertoire
mv dir1/ /tmp/

# Interactif
mv -i file.txt existing.txt

# Forcer (pas de confirmation)
mv -f file.txt existing.txt

# Ne pas écraser
mv -n file.txt existing.txt

# Verbose
mv -v file.txt /tmp/

# Mise à jour (seulement si plus récent)
mv -u source.txt dest.txt

# Exemples pratiques
# Renommer en masse avec boucle
for f in *.txt; do
    mv "$f" "${f%.txt}.bak"
done

# Renommer avec date
mv file.txt file_$(date +%Y%m%d).txt

# Déplacer fichiers modifiés dernières 24h
find . -mtime -1 -type f -exec mv {} /backup/ \;
```

#### `rm` - Supprimer

```bash
# Supprimer fichier
rm file.txt

# Plusieurs fichiers
rm file1.txt file2.txt

# Interactif (demander confirmation)
rm -i file.txt

# Forcer (pas d'erreur si absent)
rm -f file.txt

# Répertoire (récursif)
rm -r dir/

# Forcer répertoire
rm -rf dir/

# Verbose
rm -v file.txt

# ⚠️ DANGER
rm -rf /     # NE JAMAIS FAIRE !
# (moderne : --no-preserve-root requis)

# Exemples pratiques
# Supprimer fichiers vieux de 30 jours
find /tmp -mtime +30 -type f -delete

# Supprimer fichiers .tmp
rm *.tmp

# Supprimer répertoires vides
find . -type d -empty -delete

# Confirmation pour fichiers importants
rm -i *.conf

# Supprimer en mode verbose
rm -rfv old_project/
```

#### `mkdir` - Créer répertoires

```bash
# Créer répertoire
mkdir mydir

# Créer plusieurs
mkdir dir1 dir2 dir3

# Créer parents (récursif)
mkdir -p path/to/deep/dir

# Avec permissions
mkdir -m 755 mydir
mkdir -m 700 private_dir

# Verbose
mkdir -v mydir

# Exemples pratiques
# Structure projet
mkdir -p project/{src,lib,bin,doc}

# Créer avec date
mkdir backup_$(date +%Y%m%d)

# Arborescence complète
mkdir -p app/{controllers,models,views}/{admin,public}
```

#### `rmdir` - Supprimer répertoires vides

```bash
# Supprimer répertoire vide
rmdir emptydir

# Supprimer parents vides
rmdir -p path/to/empty/dir

# Ignorer erreur si non vide
rmdir --ignore-fail-on-non-empty dir

# Note : utiliser rm -r pour répertoires non vides
```

#### `touch` - Créer fichiers / modifier timestamps

```bash
# Créer fichier vide
touch file.txt

# Créer plusieurs
touch file1.txt file2.txt

# Mettre à jour timestamp (access + modification)
touch existing.txt

# Timestamp spécifique
touch -t 202601281200 file.txt    # YYYYMMDDhhmm

# Copier timestamp d'un autre fichier
touch -r reference.txt target.txt

# Seulement access time
touch -a file.txt

# Seulement modification time
touch -m file.txt

# Ne pas créer si absent
touch -c file.txt

# Exemples pratiques
# Créer fichiers de test
touch test{1..10}.txt

# Marquer fichiers traités
find . -name "*.log" -exec touch -c {} \;
```

#### `file` - Déterminer type de fichier

```bash
# Type de fichier
file document.pdf
# document.pdf: PDF document, version 1.4

file script.sh
# script.sh: Bash script, ASCII text executable

file image.jpg
# image.jpg: JPEG image data, JFIF standard

# Type MIME
file -i document.pdf
# document.pdf: application/pdf; charset=binary

# Brief (court)
file -b image.jpg
# JPEG image data

# Exemples pratiques
# Vérifier type de tous les fichiers
file *

# Trouver tous les scripts
file * | grep script
```

#### Liens symboliques et durs

**Liens symboliques (symlink) :**
```bash
# Créer lien symbolique
ln -s /path/to/original /path/to/link

# Exemple
ln -s /usr/share/doc/myapp ~/myapp-doc

# Lien relatif
ln -s ../config.txt link.txt

# Forcer (écraser si existe)
ln -sf /path/to/original /path/to/link

# Vérifier liens
ls -l link.txt
# lrwxrwxrwx ... link.txt -> original.txt

# Trouver destination
readlink link.txt
readlink -f link.txt    # Chemin absolu résolu

# Lister liens cassés
find . -type l ! -exec test -e {} \; -print
```

**Liens durs (hard link) :**
```bash
# Créer lien dur
ln original.txt hardlink.txt

# Vérifier (même inode)
ls -li original.txt hardlink.txt
# 12345 -rw-r--r-- 2 ... original.txt
# 12345 -rw-r--r-- 2 ... hardlink.txt
#       └─ même inode

# Nombre de liens durs (colonne 2 de ls -l)
ls -l file.txt
# -rw-r--r-- 3 ...
#            └─ 3 liens durs vers ce fichier

# Trouver tous les liens durs d'un fichier
find / -inum 12345

# Différences symlink vs hardlink
```

**Comparaison liens :**

| Aspect | Lien symbolique | Lien dur |
|--------|----------------|----------|
| Pointeur | Chemin (texte) | Inode |
| Partitions | Oui (cross-filesystem) | Non (même partition) |
| Répertoires | Oui | Non (sauf root) |
| Original supprimé | Lien cassé | Fichier reste |
| Espace | Négligeable | Partagé |
| Identification | `ls -l` (->...) | Même inode |

---

## 103.4 - Flux, pipes et redirections

### 🎯 Objectifs clés
- Rediriger entrée/sortie standard
- Utiliser pipes pour chaîner commandes
- Comprendre stdin, stdout, stderr
- Gérer /dev/null et /dev/zero

### 📤 Redirections standard

**File descriptors :**
- **0** : stdin (entrée standard)
- **1** : stdout (sortie standard)
- **2** : stderr (erreur standard)

#### Redirection sortie (stdout)

```bash
# Rediriger vers fichier (écrase)
command > file.txt
command 1> file.txt    # Explicite

# Ajouter à fichier (append)
command >> file.txt

# Exemples
ls > files.txt
echo "Hello" >> log.txt
date > timestamp.txt
ps aux > processes.txt
```

#### Redirection erreur (stderr)

```bash
# Rediriger stderr vers fichier
command 2> error.txt

# Ajouter stderr
command 2>> error.txt

# Exemples
ls /nonexistent 2> error.log
find / -name "*.txt" 2> /dev/null
```

#### Redirections combinées

```bash
# stdout et stderr vers même fichier
command > output.txt 2>&1
command &> output.txt        # Bash 4+ (équivalent)

# stdout et stderr séparés
command > output.txt 2> error.txt

# stdout vers fichier, stderr vers /dev/null
command > output.txt 2> /dev/null

# Tout vers /dev/null (silence complet)
command > /dev/null 2>&1
command &> /dev/null

# stderr vers stdout (puis pipe)
command 2>&1 | grep pattern

# Exemples pratiques
# Installation silencieuse
apt install package > /dev/null 2>&1

# Log complet (output + errors)
./script.sh &> logfile.txt

# Séparer succès et erreurs
./backup.sh > success.log 2> error.log
```

#### Redirection entrée (stdin)

```bash
# Rediriger depuis fichier
command < input.txt

# Here document (EOF)
cat << EOF > file.txt
Line 1
Line 2
Line 3
EOF

# Here string
grep "pattern" <<< "text to search"

# Exemples
wc -l < file.txt
mysql -u root -p < database.sql

# Mail avec contenu
mail -s "Subject" user@example.com < message.txt

# Tee (écrire fichier ET afficher)
command | tee output.txt
command | tee -a output.txt    # Append

# Multiples tee
command | tee file1.txt | grep pattern | tee file2.txt
```

### 🔗 Pipes (|)

**Principe :** Sortie d'une commande → Entrée de la suivante

```bash
# Pipe simple
command1 | command2

# Chaîne de pipes
command1 | command2 | command3 | command4

# Exemples classiques
ls -l | grep "\.txt"
ps aux | grep apache
cat file.txt | sort | uniq | wc -l

# Filtrage progressif
cat /var/log/syslog | grep ERROR | tail -50 | less

# Statistiques
du -h | sort -rh | head -10    # Top 10 plus gros
ps aux | sort -k 3 -rn | head -5    # Top 5 CPU

# Recherche et traitement
find . -name "*.log" | xargs grep -l "ERROR"
```

**Exemples avancés :**
```bash
# Top 10 IPs dans access log
cut -d ' ' -f 1 /var/log/apache2/access.log | \
    sort | uniq -c | sort -rn | head -10

# Top commandes historique
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10

# Utilisateurs avec shell valide
grep -v '^#' /etc/passwd | cut -d: -f1,7 | \
    grep -E '/bin/(bash|sh)$' | cut -d: -f1

# Monitoring bande passante
watch 'ifconfig eth0 | grep "RX bytes"'

# Process tree
ps aux | awk '{print $11}' | sort | uniq -c | sort -rn
```

### 🔄 xargs - Construire commandes

```bash
# Simple
echo "file1 file2 file3" | xargs rm

# Depuis find
find . -name "*.tmp" | xargs rm

# Un argument par commande (-n1)
cat files.txt | xargs -n1 cp -t /backup/

# Parallèle (-P)
find . -name "*.jpg" | xargs -P 4 -n1 convert -resize 800x600

# Interactif (-p)
find . -name "*.log" | xargs -p rm

# Placeholder (-I)
find . -name "*.txt" | xargs -I {} cp {} {}.backup

# Gérer espaces dans noms (avec find -print0)
find . -name "*.txt" -print0 | xargs -0 rm

# Exemples pratiques
# Déplacer fichiers trouvés
find /source -name "*.pdf" | xargs -I {} mv {} /dest/

# Chercher pattern dans fichiers
find . -name "*.log" | xargs grep "ERROR"

# Télécharger URLs depuis fichier
cat urls.txt | xargs -n1 wget

# Chmod sur fichiers trouvés
find . -type f -name "*.sh" | xargs chmod +x
```

### 🕳️ Fichiers spéciaux

#### `/dev/null` - Trou noir

```bash
# Supprimer sortie
command > /dev/null

# Supprimer erreurs
command 2> /dev/null

# Tout supprimer
command &> /dev/null

# Tester commande (ignorer sortie)
if command > /dev/null 2>&1; then
    echo "Success"
fi

# Vider fichier
> file.txt
cat /dev/null > file.txt
```

#### `/dev/zero` - Source de zéros

```bash
# Créer fichier de zéros
dd if=/dev/zero of=file.bin bs=1M count=100

# Remplir partition (test)
dd if=/dev/zero of=/mnt/bigfile bs=1M

# Benchmark disque
dd if=/dev/zero of=testfile bs=1G count=1 oflag=direct
```

#### `/dev/random` et `/dev/urandom`

```bash
# Données aléatoires
dd if=/dev/urandom of=random.bin bs=1M count=1

# Mot de passe aléatoire
tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 16

# Fichier aléatoire
head -c 1M /dev/urandom > random_file.bin
```

#### `/dev/stdin`, `/dev/stdout`, `/dev/stderr`

```bash
# Liens symboliques vers /proc/self/fd/
ls -l /dev/std*
# lrwxrwxrwx /dev/stdin -> /proc/self/fd/0
# lrwxrwxrwx /dev/stdout -> /proc/self/fd/1
# lrwxrwxrwx /dev/stderr -> /proc/self/fd/2

# Usage
cat < /dev/stdin > /dev/stdout
```

---

## 103.5 - Création, surveillance et terminaison de processus

### 🎯 Objectifs clés
- Gérer processus (foreground, background)
- Surveiller processus actifs
- Envoyer signaux aux processus
- Comprendre jobs et sessions

### 🔍 Surveillance de processus

#### `ps` - Process Status

```bash
# Processus utilisateur courant
ps

# Tous les processus (BSD style)
ps aux
# a = tous les utilisateurs
# u = format utilisateur
# x = inclus processus sans terminal

# Tous les processus (UNIX style)
ps -ef
# -e = tous
# -f = full format

# Format personnalisé
ps -eo pid,user,cmd,%cpu,%mem
ps aux --sort=-%cpu | head -10    # Top 10 CPU

# Hiérarchie (tree)
ps auxf
ps -ejH
ps axjf

# Filtrer par utilisateur
ps -u username
ps -U root

# Filtrer par processus
ps -C apache2
ps aux | grep nginx

# Format complet
ps -F
ps -ely

# Exemples pratiques
# Trouver PID
ps aux | grep apache2
pgrep apache2

# Processus zombies
ps aux | grep Z

# Top processus mémoire
ps aux --sort=-%mem | head -10

# Threads
ps -eLf
```

**Colonnes importantes ps aux :**
- **USER** : Propriétaire
- **PID** : Process ID
- **%CPU** : Utilisation CPU
- **%MEM** : Utilisation mémoire
- **VSZ** : Virtual memory (KB)
- **RSS** : Resident memory (KB)
- **TTY** : Terminal (? = pas de terminal)
- **STAT** : État (R=running, S=sleeping, Z=zombie, T=stopped)
- **START** : Heure démarrage
- **TIME** : Temps CPU
- **COMMAND** : Commande

#### `pgrep` et `pkill` - Recherche/kill par nom

```bash
# Trouver PID par nom
pgrep apache2
pgrep -u www-data apache2

# Avec détails
pgrep -a apache2
pgrep -l nginx

# Plus récent/ancien
pgrep -n apache2    # Newest
pgrep -o apache2    # Oldest

# Compter
pgrep -c apache2

# Kill par nom
pkill apache2
pkill -u username process

# Signal spécifique
pkill -9 process    # SIGKILL
pkill -HUP nginx    # SIGHUP (reload config)

# Exemples pratiques
# Tuer tous les processus utilisateur
pkill -u username

# Restart service (reload config)
pkill -HUP nginx

# Kill zombies
pkill -9 -u username
```

#### `pstree` - Arbre des processus

```bash
# Arbre complet
pstree

# Avec PIDs
pstree -p

# Avec arguments
pstree -a

# Utilisateur spécifique
pstree username

# Depuis processus
pstree -p 1234

# Compact (grouper threads)
pstree -c

# Exemple
pstree -p | grep apache2
```

#### `top` - Monitoring temps réel

```bash
# Lancer top
top

# Commandes interactives top :
h ou ?  # Aide
q       # Quitter
k       # Kill processus
r       # Renice processus
M       # Tri par mémoire
P       # Tri par CPU
T       # Tri par temps
u       # Filtrer utilisateur
1       # Toggle CPUs individuels
c       # Commande complète
V       # Arbre processus

# Options lancement
top -d 2        # Refresh toutes les 2s
top -u www-data # Utilisateur spécifique
top -p 1234     # PID spécifique
top -b -n 1     # Batch mode (une fois)

# Exemple: log top dans fichier
top -b -n 1 > top_snapshot.txt
```

**Ligne de statut top :**
```
top - 15:30:00 up 10 days, 5:23, 2 users, load average: 0.50, 0.30, 0.20
Tasks: 180 total, 1 running, 179 sleeping, 0 stopped, 0 zombie
%Cpu(s): 10.5 us, 2.3 sy, 0.0 ni, 86.5 id, 0.5 wa, 0.0 hi, 0.2 si
MiB Mem : 7842.1 total, 1234.5 free, 4567.8 used, 2039.8 buff/cache
MiB Swap: 2048.0 total, 2048.0 free,    0.0 used. 2876.3 avail Mem
```

#### `htop` - Top amélioré (si installé)

```bash
# Lancer htop
htop

# Fonctionnalités :
# - Couleurs
# - Souris support
# - Barre visuelle CPU/Mem
# - Arbre processus
# - Recherche interactive

# Installation
sudo apt install htop    # Debian/Ubuntu
sudo yum install htop    # RHEL/CentOS
```

#### `uptime` - Charge système

```bash
# Uptime et load average
uptime
# 15:30:00 up 10 days, 5:23, 2 users, load average: 0.50, 0.30, 0.20

# Load average : 1 min, 5 min, 15 min
# < nombre de CPUs = OK
# > nombre de CPUs = surchargé
```

#### `free` - Mémoire

```bash
# Mémoire disponible
free

# Format humain
free -h

# En MB
free -m

# Refresh continu
free -s 2    # Toutes les 2s

# Total seulement
free -t

# Exemple
free -h
#               total   used    free    shared  buff/cache  available
# Mem:          7.7Gi   4.5Gi   1.2Gi   100Mi   2.0Gi       2.8Gi
# Swap:         2.0Gi   0B      2.0Gi
```

#### `vmstat` - Statistiques système

```bash
# Statistiques virtuelles memory
vmstat

# Refresh continu
vmstat 2        # Toutes les 2s
vmstat 2 10     # 10 fois toutes les 2s

# Format lisible
vmstat -S M     # En MB

# Exemple
vmstat 1 5
# procs -----memory------ ---swap-- -----io---- -system-- ------cpu-----
#  r  b  swpd   free  buff cache  si  so   bi   bo   in   cs  us sy id wa st
```

### ⚙️ Gestion de processus

#### Jobs (tâches shell)

```bash
# Lancer en background
sleep 100 &
[1] 12345    # [job number] PID

# Lister jobs
jobs
# [1]+ Running    sleep 100 &
# [2]- Stopped    vim file.txt

# Suspendre processus (Ctrl+Z)
# Met en pause

# Reprendre en background
bg %1
bg           # Dernier job

# Reprendre en foreground
fg %1
fg

# Tuer job
kill %1

# Détails jobs
jobs -l      # Avec PIDs
jobs -p      # PIDs seulement

# Exemples pratiques
# Lancer plusieurs tâches
sleep 100 & sleep 200 & sleep 300 &

# Gérer
jobs
fg %2    # Reprendre tâche 2 en foreground
Ctrl+Z   # Suspendre
bg       # Continuer en background
```

#### `nohup` - Processus persistant

```bash
# Lancer avec nohup (survit déconnexion)
nohup long_command &

# Sortie dans nohup.out (défaut)
nohup command &

# Redirection personnalisée
nohup command > output.log 2>&1 &

# Exemples pratiques
# Script long
nohup ./backup.sh > backup.log 2>&1 &

# Processus serveur
nohup python3 server.py &

# Vérifier processus nohup
ps aux | grep nohup
```

#### Signaux

**Signaux principaux :**
```bash
# Liste des signaux
kill -l

# Signaux importants :
1  SIGHUP   # Hangup (reload config)
2  SIGINT   # Interrupt (Ctrl+C)
3  SIGQUIT  # Quit (Ctrl+\)
9  SIGKILL  # Kill (force, non capturable)
15 SIGTERM  # Terminate (propre, par défaut)
18 SIGCONT  # Continue (après STOP)
19 SIGSTOP  # Stop (pause, non capturable)
20 SIGTSTP  # Stop (Ctrl+Z, capturable)
```

#### `kill` - Envoyer signaux

```bash
# Kill par défaut (SIGTERM)
kill 1234

# Signal spécifique
kill -9 1234      # SIGKILL (force)
kill -15 1234     # SIGTERM (propre)
kill -HUP 1234    # SIGHUP (reload)
kill -STOP 1234   # Pause
kill -CONT 1234   # Reprendre

# Par nom de signal
kill -SIGKILL 1234
kill -SIGTERM 1234

# Tous les processus d'un utilisateur
killall -u username

# Par nom de processus
killall apache2
killall -9 firefox

# Exemples pratiques
# Reload config nginx
kill -HUP $(cat /var/run/nginx.pid)
pkill -HUP nginx

# Kill gracieux puis force
kill 1234
sleep 5
kill -9 1234

# Script kill gracieux
kill $PID
for i in {1..10}; do
    kill -0 $PID 2>/dev/null || break
    sleep 1
done
kill -9 $PID 2>/dev/null
```

#### `killall` - Kill par nom

```bash
# Kill tous les processus
killall firefox

# Signal spécifique
killall -9 chrome
killall -HUP nginx

# Interactif
killall -i apache2

# Verbose
killall -v process

# Par utilisateur
killall -u username

# Plus vieux que X
killall -o 1h process

# Plus récent que X
killall -y 10m process
```

#### Sessions et process groups

```bash
# Démarrer nouvelle session
setsid command

# Process group ID
ps -eo pid,pgid,cmd

# Session ID
ps -eo pid,sid,cmd

# Kill tout le group
kill -TERM -1234    # -PID = process group
```

---

## 103.6 - Modification des priorités d'exécution

### 🎯 Objectifs clés
- Comprendre nice et renice
- Ajuster priorités processus
- Gérer charge CPU

### ⚖️ Priorités et nice values

**Nice values :**
- Plage : **-20 à +19**
- **-20** = Priorité MAXIMALE
- **0** = Priorité par défaut
- **+19** = Priorité MINIMALE

**Règles :**
- Utilisateur normal : 0 à 19 seulement
- Root : -20 à 19
- Plus bas = plus de CPU

#### `nice` - Lancer avec priorité

```bash
# Nice par défaut (10)
nice command

# Nice spécifique
nice -n 10 command
nice --10 command    # = nice -n 10

# Priorité haute (root requis)
sudo nice -n -10 command

# Priorité basse
nice -n 19 backup.sh

# Exemples pratiques
# Backup avec faible priorité
nice -n 15 tar czf backup.tar.gz /data/

# Compilation prioritaire
sudo nice -n -5 make -j8

# Script batch
nice -n 10 ./process_data.sh

# Vérifier nice d'un processus
ps -l
# NI colonne = nice value
```

#### `renice` - Changer priorité existant

```bash
# Par PID
renice -n 5 -p 1234

# Par utilisateur
renice -n 10 -u username

# Par process group
renice -n 5 -g 1234

# Exemples pratiques
# Réduire priorité processus gourmand
renice -n 15 -p $(pgrep firefox)

# Augmenter priorité (root)
sudo renice -n -5 -p 1234

# Tous les processus utilisateur
renice -n 10 -u www-data

# Dans top (commande 'r')
# top → r → PID → nice value
```

**Afficher nice values :**
```bash
# ps
ps -eo pid,ni,comm

# top
top    # Colonne NI

# htop
htop   # Colonne NI

# Exemples
ps aux | awk '{print $2, $18, $11}' | head
# PID NI COMMAND
```

---

## 103.7 - Recherche avec expressions régulières

### 🎯 Objectifs clés
- Maîtriser regex basiques et étendues
- Utiliser grep efficacement
- Comprendre métacaractères

### 🔍 Expressions régulières (regex)

#### Métacaractères de base

```bash
.      # N'importe quel caractère (sauf newline)
^      # Début de ligne
$      # Fin de ligne
*      # 0 ou plus répétitions
[]     # Classe de caractères
[^]    # Classe négative
\      # Échappement

# Exemples
grep 'a.c' file      # abc, aac, a5c, etc.
grep '^Hello' file   # Lignes commençant par Hello
grep 'world$' file   # Lignes finissant par world
grep 'a*' file       # '', a, aa, aaa, etc.
grep '[abc]' file    # a ou b ou c
grep '[^abc]' file   # Tout sauf a, b, c
```

#### Classes de caractères

```bash
[abc]       # a ou b ou c
[a-z]       # Minuscules
[A-Z]       # Majuscules
[0-9]       # Chiffres
[a-zA-Z]    # Lettres
[a-zA-Z0-9] # Alphanumériques

# Classes POSIX
[:alnum:]   # Alphanumériques
[:alpha:]   # Lettres
[:digit:]   # Chiffres
[:lower:]   # Minuscules
[:upper:]   # Majuscules
[:space:]   # Espaces blancs
[:punct:]   # Ponctuation

# Exemples
grep '[0-9]' file           # Lignes avec chiffres
grep '^[A-Z]' file          # Commence par majuscule
grep '[[:digit:]]' file     # Chiffres (POSIX)
```

#### Quantificateurs (regex étendues -E)

```bash
?      # 0 ou 1 (optionnel)
+      # 1 ou plus
{n}    # Exactement n
{n,}   # n ou plus
{n,m}  # Entre n et m

# Exemples (grep -E ou egrep)
grep -E 'colou?r' file      # color ou colour
grep -E 'a+' file           # a, aa, aaa, etc. (au moins 1)
grep -E 'a{3}' file         # Exactement aaa
grep -E 'a{2,}' file        # aa, aaa, aaaa, etc.
grep -E 'a{2,4}' file       # aa, aaa, aaaa
```

#### Groupes et alternatives

```bash
()     # Groupe
|      # OU (alternative)

# Exemples
grep -E '(abc)+' file       # abc, abcabc, abcabcabc
grep -E 'cat|dog' file      # cat ou dog
grep -E '^(http|https)://' file  # URLs
grep -E '(error|warning)' log    # error ou warning
```

#### Ancres

```bash
^      # Début de ligne
$      # Fin de ligne
\b     # Limite de mot (word boundary)
\B     # Pas limite de mot

# Exemples
grep '^#' file              # Commentaires
grep '^$' file              # Lignes vides
grep -E '\bcat\b' file      # Mot "cat" complet
grep -E '^[A-Z].*\.$' file  # Commence majuscule, finit par point
```

### 🔎 Commande `grep`

#### Options grep basiques

```bash
# Recherche simple
grep "pattern" file.txt

# Insensible casse (-i)
grep -i "error" log.txt

# Inverser match (-v)
grep -v "^#" config.txt    # Lignes non-commentaires

# Compter occurrences (-c)
grep -c "ERROR" log.txt

# Numéros de lignes (-n)
grep -n "TODO" code.py

# Fichiers seulement (-l)
grep -l "error" *.log

# Contexte (-A, -B, -C)
grep -A 3 "ERROR" log.txt    # 3 lignes après
grep -B 2 "ERROR" log.txt    # 2 lignes avant
grep -C 2 "ERROR" log.txt    # 2 lignes avant et après

# Récursif (-r)
grep -r "TODO" /project/

# Regex étendue (-E)
grep -E "error|warning" log.txt

# Mot complet (-w)
grep -w "cat" file.txt       # Pas "category"

# Ligne entière (-x)
grep -x "exact line" file.txt

# Multiple patterns (-e)
grep -e "error" -e "warning" log.txt

# Pattern depuis fichier (-f)
grep -f patterns.txt file.txt

# Quiet (juste exit code, -q)
if grep -q "error" log.txt; then
    echo "Errors found"
fi
```

#### grep avec regex avancées

```bash
# Adresses IP
grep -E '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' file

# Adresses email
grep -E '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b' file

# URLs
grep -E 'https?://[^\s]+' file

# Numéros téléphone
grep -E '\b[0-9]{2,3}[-. ]?[0-9]{2,3}[-. ]?[0-9]{2,3}[-. ]?[0-9]{2,3}\b' file

# Dates (YYYY-MM-DD)
grep -E '\b[0-9]{4}-[0-9]{2}-[0-9]{2}\b' file

# Heures (HH:MM:SS)
grep -E '\b[0-9]{2}:[0-9]{2}:[0-9]{2}\b' file
```

#### Exemples pratiques grep

```bash
# Erreurs dans logs
grep -i "error\|warning\|critical" /var/log/syslog

# IPs uniques dans access log
grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' access.log | sort -u

# Lignes non vides, non commentées
grep -v '^$' file.conf | grep -v '^#'

# TODO dans code source
grep -rn "TODO\|FIXME\|XXX" /project/src/

# Failed logins
grep "Failed password" /var/log/auth.log | tail -20

# Processus Apache
ps aux | grep apache2 | grep -v grep

# Config active (sans commentaires ni vides)
grep -Ev '^#|^$' /etc/nginx/nginx.conf

# Top 10 IPs dans logs
grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' access.log | \
    sort | uniq -c | sort -rn | head -10
```

### 🔍 Autres commandes de recherche

#### `egrep` et `fgrep`

```bash
# egrep = grep -E (regex étendues)
egrep 'error|warning' log.txt
grep -E 'error|warning' log.txt    # Équivalent

# fgrep = grep -F (fixed strings, pas regex)
fgrep 'log[1].txt' file            # Cherche littéralement
grep -F 'log[1].txt' file          # Équivalent
```

#### `sed` - Stream Editor (recherche/remplace)

```bash
# Remplacer (1ère occurrence)
sed 's/old/new/' file.txt

# Remplacer (toutes occurrences)
sed 's/old/new/g' file.txt

# Insensible casse
sed 's/old/new/gi' file.txt

# Supprimer lignes
sed '/pattern/d' file.txt

# Lignes spécifiques
sed -n '10,20p' file.txt       # Lignes 10-20
sed '5d' file.txt              # Supprimer ligne 5

# In-place (modifier fichier)
sed -i 's/old/new/g' file.txt

# Backup avant modification
sed -i.bak 's/old/new/g' file.txt

# Exemples pratiques
# Supprimer commentaires
sed '/^#/d' config.txt

# Supprimer lignes vides
sed '/^$/d' file.txt

# Remplacer IPs
sed 's/192\.168\.1\./10.0.0./g' config.txt

# Ajouter texte en début
sed '1i\# Configuration file' config.txt

# Ajouter texte en fin
sed '$a\# End of file' config.txt
```

---

## 103.8 - Édition basique de fichiers

### 🎯 Objectifs clés
- Utiliser vi/vim efficacement
- Modes vi (normal, insert, command)
- Commandes d'édition basiques

### ✏️ Éditeur Vi/Vim

**Modes vi :**
1. **Mode Normal** (commandes)
2. **Mode Insert** (édition)
3. **Mode Visual** (sélection)
4. **Mode Command** (ex commandes)

#### Démarrage vi

```bash
# Ouvrir fichier
vi file.txt
vim file.txt

# Créer nouveau fichier
vi newfile.txt

# Ouvrir à ligne N
vi +10 file.txt

# Ouvrir à pattern
vi +/pattern file.txt

# Ouvrir en lecture seule
vi -R file.txt
view file.txt
```

#### Mode Normal → Insert

```bash
i    # Insert avant curseur
I    # Insert début de ligne
a    # Append après curseur
A    # Append fin de ligne
o    # Open ligne dessous
O    # Open ligne dessus
s    # Substitute caractère
S    # Substitute ligne
c    # Change (avec mouvement)

# Retour mode Normal: Esc
```

#### Mouvements (Mode Normal)

```bash
# Caractères
h    # Gauche
j    # Bas
k    # Haut
l    # Droite

# Mots
w    # Mot suivant
b    # Mot précédent
e    # Fin mot

# Ligne
0    # Début ligne
^    # Premier caractère non-blanc
$    # Fin ligne

# Fichier
gg   # Début fichier
G    # Fin fichier
10G  # Ligne 10
:10  # Ligne 10

# Écran
H    # Haut écran
M    # Milieu écran
L    # Bas écran
Ctrl+F # Page suivante
Ctrl+B # Page précédente
Ctrl+D # Demi-page bas
Ctrl+U # Demi-page haut
```

#### Édition (Mode Normal)

```bash
# Supprimer
x    # Caractère
dd   # Ligne
dw   # Mot
d$   # Jusqu'à fin ligne
d0   # Jusqu'à début ligne
5dd  # 5 lignes

# Copier (yank)
yy   # Ligne
yw   # Mot
y$   # Jusqu'à fin ligne
5yy  # 5 lignes

# Coller
p    # Après curseur
P    # Avant curseur

# Annuler/Refaire
u       # Undo
Ctrl+R  # Redo
.       # Répéter dernière commande

# Remplacer
r    # Remplacer caractère
R    # Mode replace
~    # Changer casse

# Joindre lignes
J    # Joindre avec ligne suivante
```

#### Recherche (Mode Normal)

```bash
# Rechercher
/pattern    # Recherche avant
?pattern    # Recherche arrière
n           # Occurrence suivante
N           # Occurrence précédente
*           # Chercher mot sous curseur (avant)
#           # Chercher mot sous curseur (arrière)

# Exemples
/error      # Cherche "error"
n           # Suivant
N           # Précédent
```

#### Mode Command (:)

```bash
# Sauvegarder/Quitter
:w          # Sauvegarder
:q          # Quitter
:wq         # Sauvegarder et quitter
:q!         # Quitter sans sauvegarder
:x          # Sauvegarder et quitter (si modifié)
ZZ          # Idem (mode Normal)

# Fichier
:w file.txt     # Sauvegarder comme
:r file.txt     # Lire fichier
:e file.txt     # Ouvrir fichier
:e!             # Recharger fichier

# Navigation
:10         # Ligne 10
:$          # Dernière ligne

# Rechercher/Remplacer
:s/old/new/         # Remplacer (ligne courante)
:s/old/new/g        # Remplacer (toute ligne)
:%s/old/new/g       # Remplacer (tout fichier)
:%s/old/new/gc      # Remplacer (confirmer)
:10,20s/old/new/g   # Lignes 10-20

# Supprimer
:d          # Ligne courante
:10,20d     # Lignes 10-20
:%d         # Tout

# Shell
:!command   # Exécuter commande shell
:r !command # Insérer sortie commande
:sh         # Shell temporaire (exit pour revenir)

# Options
:set number     # Numéros lignes
:set nonumber   # Masquer numéros
:set list       # Afficher caractères spéciaux
:set hlsearch   # Highlight recherche
:syntax on      # Coloration syntaxe
```

#### Mode Visual

```bash
# Entrer mode Visual
v    # Visual (caractères)
V    # Visual Line (lignes)
Ctrl+V # Visual Block (bloc)

# Sélectionner puis:
d    # Supprimer
y    # Copier
c    # Changer
>    # Indenter droite
<    # Indenter gauche
```

#### Configuration vi (~/.vimrc)

```bash
# Fichier ~/.vimrc
set number          " Numéros lignes
set relativenumber  " Numéros relatifs
set tabstop=4       " Largeur tab
set shiftwidth=4    " Largeur indentation
set expandtab       " Tab → espaces
set autoindent      " Auto-indentation
set smartindent     " Indentation intelligente
syntax on           " Coloration syntaxe
set hlsearch        " Highlight recherche
set incsearch       " Recherche incrémentale
set ignorecase      " Ignorer casse recherche
set smartcase       " Casse si majuscule
set cursorline      " Highlight ligne courante
set showmatch       " Montrer parenthèses
set mouse=a         " Support souris
```

#### Aide vi/vim

```bash
# Dans vim
:help
:help dd
:help search

# Tutoriel
vimtutor

# Version et features
vim --version
```

---

## 📝 Résumé et points clés à retenir

### Commandes essentielles par catégorie

#### Shell et environnement
```bash
echo, export, set, unset, env
alias, unalias
history, !, !!, !$
which, type, whereis
```

#### Filtres texte
```bash
cat, tac, head, tail
cut, paste, tr
wc, sort, uniq
grep, egrep, sed
```

#### Gestion fichiers
```bash
ls, cp, mv, rm
mkdir, rmdir, touch
ln, file
find, locate
```

#### Redirections et pipes
```bash
>, >>, <, 2>, 2>&1, &>
|, tee
xargs
/dev/null, /dev/zero
```

#### Processus
```bash
ps, top, pgrep, pstree
kill, killall, pkill
jobs, fg, bg, nohup
nice, renice
```

#### Regex et recherche
```bash
grep, egrep, fgrep
sed
^, $, ., *, [], [^]
+, ?, {n}, {n,m}
```

#### Éditeur
```bash
vi, vim
i, a, o, Esc
:w, :q, :wq, :q!
dd, yy, p
/pattern, n
```

### Patterns courants

#### Top 10 commandes les plus utilisées
```bash
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
```

#### Chercher et remplacer récursivement
```bash
find . -name "*.txt" -exec sed -i 's/old/new/g' {} \;
```

#### Monitoring en temps réel
```bash
watch 'ps aux | grep apache'
tail -f /var/log/syslog | grep ERROR
```

#### Pipeline de traitement
```bash
cat data.txt | grep -v '^#' | sort | uniq -c | sort -rn | head -20
```

### Checklist avant examen

- [ ] Je maîtrise variables d'environnement ($PATH, $HOME, etc.)
- [ ] Je connais l'historique des commandes (!, !!, Ctrl+R)
- [ ] Je sais utiliser redirections (>, 2>, &>, |)
- [ ] Je maîtrise grep avec regex basiques et étendues
- [ ] Je peux utiliser sed pour recherche/remplacement
- [ ] Je connais filtres texte (cut, sort, uniq, tr, wc)
- [ ] Je maîtrise gestion processus (ps, top, kill, nice)
- [ ] Je sais utiliser vi/vim (modes, commandes basiques)
- [ ] Je comprends pipes et xargs
- [ ] Je connais différences links symboliques/durs

---

## 🔬 Labs pratiques recommandés

### Lab 1 : Shell et variables
```bash
# 1. Variables
NAME="John"
echo "Hello $NAME"
export PATH=$PATH:/opt/bin

# 2. Historique
history | tail -20
!!
!-2

# 3. Alias
alias ll='ls -lah'
alias gs='git status'

# 4. Functions
myfunction() {
    echo "Args: $@"
    echo "First: $1"
}
myfunction test 123
```

### Lab 2 : Filtres et pipes
```bash
# 1. Top 10 plus gros fichiers
du -ah /var/log | sort -rh | head -10

# 2. Statistiques lignes de code
find . -name "*.py" | xargs wc -l | sort -rn

# 3. IPs uniques
cut -d ' ' -f 1 access.log | sort -u | wc -l

# 4. Nettoyer CSV
cat data.csv | tr -d '\r' | cut -d ',' -f 1,3 > clean.csv
```

### Lab 3 : Gestion processus
```bash
# 1. Lancer background
sleep 100 &
jobs

# 2. Monitoring
ps aux --sort=-%cpu | head -10
top -b -n 1 | head -20

# 3. Kill graceful
kill $(pgrep firefox)
pkill -HUP nginx

# 4. Nice
nice -n 10 tar czf backup.tar.gz /data/
renice -n 5 -p $(pgrep backup)
```

### Lab 4 : Regex et grep
```bash
# 1. Recherches basiques
grep -i "error" /var/log/syslog
grep -v "^#" /etc/ssh/sshd_config

# 2. Regex avancées
grep -E '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' file.txt
grep -E '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}' file.txt

# 3. sed
sed 's/192\.168\.1\./10.0.0./g' config.txt
sed -i.bak '/^$/d' file.txt
```

### Lab 5 : Vi/Vim
```bash
# 1. Ouvrir et éditer
vi test.txt
i (insert mode)
# Taper texte
Esc
:wq

# 2. Commandes
dd (supprimer ligne)
yy (copier ligne)
p (coller)
u (undo)

# 3. Recherche/Remplace
/pattern
:%s/old/new/g
```

---

## 📖 Ressources complémentaires

- **Man pages :** `man bash`, `man grep`, `man sed`, `man vim`
- **Tutoriels :** `vimtutor`, `man regex`
- **Documentation LPI :** LPI-Learning-Material-101-500-fr.md
- **Cours KodeKloud :** Modules Sujet 103
- **Anki :** 125 cartes Sujet 103

---

**🎯 Objectif : Maîtriser le Sujet 103 à 100% - C'est le CŒUR de l'examen !**

*Prochaine étape : [QCM-Sujet-103.md](../QCM/QCM-Sujet-103.md) avec 50 questions !*

**⚠️ IMPORTANT :** Le Sujet 103 représente 40% de l'examen. Consacrez-lui le temps nécessaire !
