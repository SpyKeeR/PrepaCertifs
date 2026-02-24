# QCM - Sujet 105 : Shells et Scripts Shell

**LPIC-1 Examen 102-500**

---

## Instructions

- Ce QCM contient **50 questions** réparties sur les 3 objectifs du Sujet 105
- Chaque question peut avoir **une ou plusieurs bonnes réponses**
- Les réponses et explications détaillées sont fournies à la fin de chaque section
- Prenez le temps de lire les explications pour comprendre vos erreurs

**Répartition :**
- 105.1 : Environnement shell (20 questions)
- 105.2 : Scripts shell (20 questions)
- 105.3 : SQL (10 questions)

---

## 105.1 - Personnalisation et utilisation de l'environnement du shell
### Question 1
Quel fichier est exécuté en premier lors de la connexion d'un utilisateur dans un shell Bash de connexion ?

- [ ] A. `~/.bashrc`
- [ ] B. `/etc/bash.bashrc`
- [ ] C. `/etc/profile`
- [ ] D. `~/.bash_profile`

### Question 2
Quels fichiers de configuration utilisateur peuvent être exécutés lors d'un shell de connexion ? (Sélectionnez toutes les réponses correctes)

- [ ] A. `~/.bash_profile`
- [ ] B. `~/.bash_login`
- [ ] C. `~/.profile`
- [ ] D. `~/.bashrc`

### Question 3
Quelle commande permet de vérifier si vous êtes dans un shell de connexion ?

- [ ] A. `echo $0`
- [ ] B. `shopt -q login_shell && echo "Connexion"`
- [ ] C. `test -login`
- [ ] D. `bash --status`

### Question 4
Comment ajouter `/opt/bin` au début de votre PATH de manière permanente ?

- [ ] A. Ajouter `PATH=/opt/bin:$PATH` dans `~/.bashrc`
- [ ] B. Ajouter `export PATH=/opt/bin` dans `~/.bashrc`
- [ ] C. Ajouter `export PATH=/opt/bin:$PATH` dans `~/.bashrc`
- [ ] D. Exécuter `set PATH=/opt/bin:$PATH`

### Question 5
Quelle est la différence entre `source ~/.bashrc` et `./~/.bashrc` ?

- [ ] A. Aucune différence
- [ ] B. `source` exécute dans le shell actuel, `./` dans un sous-shell
- [ ] C. `source` nécessite les droits d'exécution, `./` non
- [ ] D. `./` est plus rapide que `source`

### Question 6
Quel fichier contient les fichiers par défaut pour les nouveaux utilisateurs ?

- [ ] A. `/etc/default`
- [ ] B. `/etc/skel`
- [ ] C. `/home/template`
- [ ] D. `/usr/share/skel`

### Question 7
Quelle commande affiche uniquement les variables d'environnement (exportées) ?

- [ ] A. `set`
- [ ] B. `env`
- [ ] C. `export`
- [ ] D. `printenv`

### Question 8
Comment créer un alias permanent pour `ll` qui exécute `ls -lah` ?

- [ ] A. `alias ll='ls -lah'` dans le terminal
- [ ] B. Ajouter `alias ll='ls -lah'` dans `~/.bashrc`
- [ ] C. Exécuter `export alias ll='ls -lah'`
- [ ] D. Créer un script `/bin/ll` contenant `ls -lah`

### Question 9
Quelle variable d'environnement définit le répertoire personnel de l'utilisateur ?

- [ ] A. `$PWD`
- [ ] B. `$USER_HOME`
- [ ] C. `$HOME`
- [ ] D. `$HOMEDIR`

### Question 10
Comment supprimer la variable d'environnement `MY_VAR` ?

- [ ] A. `export MY_VAR=`
- [ ] B. `unset MY_VAR`
- [ ] C. `MY_VAR=null`
- [ ] D. `delete MY_VAR`

### Question 11
Quelle séquence d'échappement affiche le nom d'utilisateur dans le prompt PS1 ?

- [ ] A. `\u`
- [ ] B. `\U`
- [ ] C. `$USER`
- [ ] D. `\user`

### Question 12
Quel fichier est exécuté lors de la fermeture d'un shell de connexion ?

- [ ] A. `~/.bash_exit`
- [ ] B. `~/.bash_logout`
- [ ] C. `~/.logout`
- [ ] D. `/etc/bash.logout`

### Question 13
Comment exécuter une commande sans utiliser un alias défini ?

- [ ] A. `\commande`
- [ ] B. `/commande`
- [ ] C. `unalias commande && commande`
- [ ] D. `--no-alias commande`

### Question 14
Quelle commande affiche toutes les fonctions définies dans le shell actuel ?

- [ ] A. `list functions`
- [ ] B. `declare -F`
- [ ] C. `function --list`
- [ ] D. `show functions`

### Question 15
Comment définir une variable disponible pour tous les processus enfants ?

- [ ] A. `VAR=valeur`
- [ ] B. `export VAR=valeur`
- [ ] C. `set VAR=valeur`
- [ ] D. `declare VAR=valeur`

### Question 16
Quel fichier Debian/Ubuntu source généralement `~/.bashrc` dans un shell de connexion ?

- [ ] A. `/etc/profile`
- [ ] B. `~/.bash_profile`
- [ ] C. `~/.profile`
- [ ] D. `/etc/bash.bashrc`

### Question 17
Comment lister tous les alias définis dans le shell actuel ?

- [ ] A. `alias -l`
- [ ] B. `alias`
- [ ] C. `list alias`
- [ ] D. `show alias`

### Question 18
Quelle commande permet de sourcer un fichier (méthode POSIX) ?

- [ ] A. `source fichier`
- [ ] B. `. fichier`
- [ ] C. `load fichier`
- [ ] D. `exec fichier`

### Question 19
Quelle variable contient le répertoire de travail précédent ?

- [ ] A. `$PREVIOUS`
- [ ] B. `$LASTDIR`
- [ ] C. `$OLDPWD`
- [ ] D. `$PREVPWD`

### Question 20
Comment créer une fonction Bash qui affiche "Bonjour" ?

- [ ] A. `function hello { echo "Bonjour"; }`
- [ ] B. `hello() { echo "Bonjour"; }`
- [ ] C. `def hello { echo "Bonjour"; }`
- [ ] D. `create function hello { echo "Bonjour"; }`

---

## Réponses et explications - 105.1

## 105.2 - Personnalisation ou écriture de scripts simples
### Question 21
Quelle ligne doit être la première dans un script Bash ?

- [ ] A. `#!/bin/sh`
- [ ] B. `#!/bin/bash`
- [ ] C. `# Script Bash`
- [ ] D. Aucune ligne spéciale n'est requise

### Question 22
Que contient la variable `$#` dans un script ?

- [ ] A. Le PID du script
- [ ] B. Le nombre d'arguments passés au script
- [ ] C. Le code de retour de la dernière commande
- [ ] D. Tous les arguments sous forme de chaîne

### Question 23
Quelle est la différence entre `$@` et `$*` ?

- [ ] A. Aucune différence
- [ ] B. `$@` préserve les espaces dans les arguments, `$*` non
- [ ] C. `$*` est obsolète
- [ ] D. `$@` contient le premier argument seulement

### Question 24
Comment tester si un fichier existe et est un fichier régulier ?

- [ ] A. `[ -e fichier ]`
- [ ] B. `[ -f fichier ]`
- [ ] C. `test -file fichier`
- [ ] D. `[[ -exists fichier ]]`

### Question 25
Quelle commande teste si une chaîne est vide ?

- [ ] A. `[ -z "$str" ]`
- [ ] B. `[ -empty "$str" ]`
- [ ] C. `[ "$str" == "" ]`
- [ ] D. `test -null "$str"`

### Question 26
Comment comparer deux nombres dans un test ?

- [ ] A. `[ $a = $b ]`
- [ ] B. `[ $a -eq $b ]`
- [ ] C. `[ $a == $b ]`
- [ ] D. `test $a equals $b`

### Question 27
Quelle syntaxe est correcte pour une boucle for sur une liste ?

- [ ] A. `for i in 1 2 3; do echo $i; done`
- [ ] B. `for (i in 1 2 3) { echo $i }`
- [ ] C. `for i = 1 to 3; echo $i`
- [ ] D. `foreach i in 1 2 3 do echo $i`

### Question 28
Comment lire un fichier ligne par ligne dans un script ?

- [ ] A. `while read line; do echo $line; done < fichier`
- [ ] B. `for line in $(cat fichier); do echo $line; done`
- [ ] C. `read -file fichier`
- [ ] D. `cat fichier | foreach line`

### Question 29
Quelle est la syntaxe correcte pour la substitution de commande (moderne) ?

- [ ] A. `` `commande` ``
- [ ] B. `$(commande)`
- [ ] C. `${commande}`
- [ ] D. `&(commande)`

### Question 30
Que signifie un code de retour de 0 ?

- [ ] A. Erreur
- [ ] B. Succès
- [ ] C. Avertissement
- [ ] D. Commande non trouvée

### Question 31
Comment vérifier le code de retour de la dernière commande ?

- [ ] A. `echo $?`
- [ ] B. `echo $EXIT`
- [ ] C. `echo $RETVAL`
- [ ] D. `status`

### Question 32
Quelle option active le mode de débogage dans un script ?

- [ ] A. `set -d`
- [ ] B. `set -x`
- [ ] C. `bash -debug script.sh`
- [ ] D. `debug=true`

### Question 33
Comment lire l'entrée utilisateur de manière silencieuse (masquer ce qui est tapé) ?

- [ ] A. `read -s password`
- [ ] B. `read -silent password`
- [ ] C. `read -hide password`
- [ ] D. `read -p password`

### Question 34
Quelle structure permet de tester plusieurs conditions mutuellement exclusives ?

- [ ] A. `if/elif/else`
- [ ] B. `case`
- [ ] C. `switch`
- [ ] D. `select`

### Question 35
Comment envoyer un email simple depuis un script ?

- [ ] A. `echo "message" | mail -s "sujet" user@example.com`
- [ ] B. `sendmail "message" user@example.com`
- [ ] C. `email -to user@example.com -body "message"`
- [ ] D. `smtp send "message" user@example.com`

### Question 36
Que fait `set -e` dans un script ?

- [ ] A. Active le mode écho
- [ ] B. Arrête le script en cas d'erreur
- [ ] C. Exporte toutes les variables
- [ ] D. Active le mode interactif

### Question 37
Comment obtenir le nom du script en cours d'exécution ?

- [ ] A. `$SCRIPT`
- [ ] B. `$0`
- [ ] C. `$NAME`
- [ ] D. `basename`

### Question 38
Quelle commande affiche "Succès" si la commande précédente a réussi ?

- [ ] A. `commande && echo "Succès"`
- [ ] B. `commande || echo "Succès"`
- [ ] C. `commande ; echo "Succès"`
- [ ] D. `if commande; echo "Succès"`

### Question 39
Comment créer une boucle infinie ?

- [ ] A. `while true; do ... done`
- [ ] B. `for (;;); do ... done`
- [ ] C. `loop; do ... done`
- [ ] D. `repeat; do ... done`

### Question 40
Quelle commande termine une fonction et retourne un code de retour ?

- [ ] A. `exit 0`
- [ ] B. `return 0`
- [ ] C. `break`
- [ ] D. `quit 0`

---

## Réponses et explications - 105.2


---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Réponses et explications - 105.1

### Question 1

**Réponse correcte : C. `/etc/profile`**

**Explication :**
Lors d'un shell de connexion Bash, l'ordre d'exécution est :
1. `/etc/profile` (fichier système)
2. `/etc/profile.d/*` (scripts système)
3. Puis un seul de ces fichiers utilisateur (premier trouvé) :
   - `~/.bash_profile`
   - `~/.bash_login`
   - `~/.profile`

`~/.bashrc` et `/etc/bash.bashrc` sont pour les shells interactifs non-login.

**💡 Point clé :** `/etc/profile` est toujours le premier fichier exécuté dans un shell de connexion.

---

### Question 2

**Réponses correctes : A, B, C**

**Explication :**
Un shell de connexion cherche et exécute le premier fichier trouvé parmi :
- `~/.bash_profile` (priorité 1)
- `~/.bash_login` (priorité 2)
- `~/.profile` (priorité 3)

Une fois qu'un fichier est trouvé et exécuté, les autres sont ignorés. Cependant, ces fichiers peuvent eux-mêmes sourcer `~/.bashrc`.

**💡 Point clé :** Un seul de ces trois fichiers est exécuté, mais tous peuvent potentiellement l'être selon la configuration.

---

### Question 3

**Réponses correctes : A, B**

**Explication :**
Deux méthodes fonctionnent :

1. `echo $0` affiche :
   - `-bash` ou `-su` pour un shell de connexion
   - `bash` ou `/bin/bash` pour un shell simple

2. `shopt -q login_shell && echo "Connexion"` teste directement l'option `login_shell`

**💡 Point clé :** `shopt -q login_shell` est la méthode la plus fiable en script.

---

### Question 4

**Réponse correcte : C. `export PATH=/opt/bin:$PATH` dans `~/.bashrc`**

**Explication :**
- `export` est nécessaire pour que la variable soit disponible aux processus enfants
- `/opt/bin:$PATH` ajoute le nouveau chemin AU DÉBUT (prioritaire)
- `$PATH` doit être inclus pour conserver les chemins existants
- `~/.bashrc` assure que c'est appliqué à chaque nouveau shell

**❌ Erreurs courantes :**
- B. Oublie `$PATH`, écrase complètement le PATH existant
- A. Sans `export`, la variable ne sera pas héritée par les sous-processus

**💡 Point clé :** Toujours inclure `$PATH` lors de la modification du PATH.

---

### Question 5

**Réponse correcte : B**

**Explication :**
- `source ~/.bashrc` (ou `. ~/.bashrc`) : exécute le script dans le shell actuel
  - Les modifications de variables affectent le shell actuel
  - Pas besoin de permissions d'exécution
  
- `./~/.bashrc` : exécute dans un sous-shell (nouveau processus)
  - Les modifications ne persistent pas dans le shell parent
  - Nécessite les permissions d'exécution (chmod +x)

**💡 Point clé :** Utilisez `source` ou `.` pour charger des fichiers de configuration.

---

### Question 6

**Réponse correcte : B. `/etc/skel`**

**Explication :**
`/etc/skel` (skeleton) contient les fichiers modèles copiés automatiquement dans le répertoire personnel de chaque nouvel utilisateur créé avec `useradd -m`.

Contenu typique :
- `.bashrc`
- `.profile`
- `.bash_logout`

**💡 Point clé :** Modifiez `/etc/skel` pour standardiser l'environnement des nouveaux utilisateurs.

---

### Question 7

**Réponses correctes : B, D**

**Explication :**
- `env` et `printenv` : affichent uniquement les variables d'environnement (exportées)
- `set` : affiche toutes les variables (shell + environnement) et fonctions
- `export` sans argument : affiche les variables exportées avec `declare -x`

**💡 Point clé :** `env` et `printenv` sont équivalents et préférables pour lister uniquement l'environnement.

---

### Question 8

**Réponse correcte : B**

**Explication :**
Pour qu'un alias soit permanent, il doit être défini dans un fichier de configuration :
- `~/.bashrc` pour les shells interactifs
- Ou `~/.bash_aliases` (sourcé par `~/.bashrc`)

Exécuter `alias ll='ls -lah'` directement dans le terminal ne le rend disponible que pour la session en cours.

**💡 Point clé :** Les alias doivent être dans `~/.bashrc` ou `~/.bash_aliases` pour être permanents.

---

### Question 9

**Réponse correcte : C. `$HOME`**

**Explication :**
Variables importantes :
- `$HOME` : répertoire personnel (`/home/username`)
- `$PWD` : répertoire de travail actuel
- `$USER` : nom d'utilisateur
- `$OLDPWD` : répertoire de travail précédent

**💡 Point clé :** `~` est un raccourci pour `$HOME`.

---

### Question 10

**Réponse correcte : B. `unset MY_VAR`**

**Explication :**
`unset` supprime complètement une variable :
```bash
MY_VAR="valeur"
echo $MY_VAR  # affiche: valeur
unset MY_VAR
echo $MY_VAR  # n'affiche rien
```

**❌ Erreurs courantes :**
- `MY_VAR=` : définit la variable comme vide mais elle existe toujours
- `export MY_VAR=` : pareil, mais exportée

**💡 Point clé :** `unset` supprime, `VAR=` vide seulement.

---

### Question 11

**Réponse correcte : A. `\u`**

**Explication :**
Séquences d'échappement courantes pour PS1 :
- `\u` : nom d'utilisateur
- `\h` : nom d'hôte (court)
- `\w` : chemin complet du répertoire de travail
- `\W` : nom du répertoire de travail seulement
- `\$` : `#` si root, `$` sinon

Exemple :
```bash
PS1='\u@\h:\w\$ '
# Résultat: maxime@debian:/home/maxime$
```

**💡 Point clé :** Minuscules pour la plupart des séquences PS1.

---

### Question 12

**Réponse correcte : B. `~/.bash_logout`**

**Explication :**
`~/.bash_logout` est exécuté automatiquement lors de la fermeture d'un shell de connexion. Utilisations courantes :
- Nettoyer les fichiers temporaires
- Effacer l'écran
- Enregistrer l'historique

Exemple :
```bash
# ~/.bash_logout
clear
echo "Au revoir, $USER"
```

**💡 Point clé :** Uniquement pour les shells de connexion, pas pour les shells simples.

---

### Question 13

**Réponse correcte : A. `\commande`**

**Explication :**
Le backslash `\` devant une commande empêche l'expansion d'alias :
```bash
alias ls='ls --color=auto'
ls        # utilise l'alias
\ls       # utilise la commande originale
```

Alternative : `command ls` ou `/bin/ls` (chemin complet)

**💡 Point clé :** `\` est la méthode la plus simple pour contourner un alias.

---

### Question 14

**Réponse correcte : B. `declare -F`**

**Explication :**
Commandes pour gérer les fonctions :
- `declare -F` : liste les noms de toutes les fonctions
- `declare -f` : affiche toutes les fonctions avec leur corps
- `declare -f nom_fonction` : affiche une fonction spécifique
- `unset -f nom_fonction` : supprime une fonction

**💡 Point clé :** `declare` gère à la fois les variables et les fonctions selon l'option.

---

### Question 15

**Réponse correcte : B. `export VAR=valeur`**

**Explication :**
Différence fondamentale :
- `VAR=valeur` : variable locale au shell actuel
- `export VAR=valeur` : variable d'environnement héritée par les processus enfants

```bash
# Sans export
VAR="test"
bash -c 'echo $VAR'  # n'affiche rien

# Avec export
export VAR="test"
bash -c 'echo $VAR'  # affiche: test
```

**💡 Point clé :** `export` rend la variable disponible à tous les sous-processus.

---

### Question 16

**Réponse correcte : C. `~/.profile`**

**Explication :**
Dans Debian/Ubuntu, `~/.profile` contient généralement :
```bash
# ~/.profile
if [ -n "$BASH_VERSION" ]; then
    if [ -f "$HOME/.bashrc" ]; then
        . "$HOME/.bashrc"
    fi
fi
```

Cela permet d'avoir les configurations de `~/.bashrc` même dans un shell de connexion.

**💡 Point clé :** `~/.profile` fait le lien entre shell de connexion et configurations interactives.

---

### Question 17

**Réponse correcte : B. `alias`**

**Explication :**
Sans argument, `alias` affiche tous les alias définis :
```bash
$ alias
alias ll='ls -lah'
alias grep='grep --color=auto'
alias ..='cd ..'
```

Pour supprimer : `unalias nom_alias` ou `unalias -a` (tous)

**💡 Point clé :** Commande simple sans option nécessaire.

---

### Question 18

**Réponse correcte : B. `. fichier`**

**Explication :**
Deux méthodes pour sourcer :
- `. fichier` : méthode POSIX (compatible sh)
- `source fichier` : spécifique à Bash

Les deux exécutent le fichier dans le shell actuel (pas de sous-shell).

**💡 Point clé :** Utilisez `.` pour compatibilité maximale, `source` est plus lisible.

---

### Question 19

**Réponse correcte : C. `$OLDPWD`**

**Explication :**
Variables de répertoire :
- `$PWD` : répertoire actuel (Present Working Directory)
- `$OLDPWD` : répertoire précédent
- `cd -` : retourne à `$OLDPWD`

```bash
cd /tmp
cd /home
echo $PWD      # /home
echo $OLDPWD   # /tmp
cd -           # retourne à /tmp
```

**💡 Point clé :** `cd -` est un raccourci pour `cd $OLDPWD`.

---

### Question 20

**Réponses correctes : A, B**

**Explication :**
Deux syntaxes valides pour déclarer une fonction Bash :

```bash
# Syntaxe 1
function hello {
    echo "Bonjour"
}

# Syntaxe 2 (préférée, POSIX)
hello() {
    echo "Bonjour"
}
```

Les deux sont équivalentes. La syntaxe 2 est préférable car compatible POSIX.

**💡 Point clé :** La syntaxe avec `()` est plus portable et recommandée.

---

## Réponses et explications - 105.2

### Question 21

**Réponse correcte : B. `#!/bin/bash`**

**Explication :**
Le shebang indique quel interpréteur utiliser :
- `#!/bin/bash` : utilise Bash (fonctionnalités étendues)
- `#!/bin/sh` : utilise sh (POSIX, plus portable)
- `#!/usr/bin/env bash` : trouve bash via PATH (plus portable)

Le shebang doit être la première ligne (pas d'espace avant `#`).

**💡 Point clé :** Sans shebang, le script s'exécute avec le shell actuel de l'utilisateur.

---

### Question 22

**Réponse correcte : B. Le nombre d'arguments**

**Explication :**
Variables spéciales :
- `$#` : nombre d'arguments
- `$0` : nom du script
- `$1, $2, ...` : arguments positionnels
- `$@` : tous les arguments (liste)
- `$?` : code de retour dernière commande
- `$$` : PID du script

```bash
# script.sh arg1 arg2 arg3
echo $#  # affiche: 3
```

**💡 Point clé :** Utile pour vérifier si le bon nombre d'arguments est fourni.

---

### Question 23

**Réponse correcte : B**

**Explication :**
Différence importante entre guillemets :
```bash
# Avec des arguments contenant des espaces
set -- "arg 1" "arg 2"

"$@"  # → "arg 1" "arg 2" (préserve les espaces)
"$*"  # → "arg 1 arg 2" (chaîne unique)
```

**💡 Point clé :** Toujours utiliser `"$@"` pour préserver l'intégrité des arguments.

---

### Question 24

**Réponse correcte : B. `[ -f fichier ]`**

**Explication :**
Tests de fichiers courants :
- `-e` : fichier existe (n'importe quel type)
- `-f` : fichier régulier existe
- `-d` : répertoire existe
- `-L` : lien symbolique existe
- `-r` : fichier lisible
- `-w` : fichier modifiable
- `-x` : fichier exécutable

**💡 Point clé :** `-f` pour fichier régulier, `-e` pour n'importe quel fichier.

---

### Question 25

**Réponses correctes : A, C**

**Explication :**
Deux méthodes valides :
```bash
# Méthode 1
[ -z "$str" ]  # vrai si chaîne vide

# Méthode 2
[ "$str" == "" ]  # vrai si chaîne vide
[[ "$str" == "" ]]  # Bash étendu

# Inverse
[ -n "$str" ]  # vrai si chaîne NON vide
```

**💡 Point clé :** `-z` (zero length) et `-n` (non-zero length) sont les plus idiomatiques.

---

### Question 26

**Réponse correcte : B. `[ $a -eq $b ]`**

**Explication :**
Opérateurs de comparaison numérique :
- `-eq` : égal (equal)
- `-ne` : différent (not equal)
- `-lt` : inférieur (less than)
- `-le` : inférieur ou égal
- `-gt` : supérieur (greater than)
- `-ge` : supérieur ou égal

**❌ Erreur courante :**
`=` et `==` sont pour les chaînes, pas les nombres !
```bash
[ "10" -gt "9" ]   # correct
[ "10" > "9" ]     # incorrect (compare alphabétiquement)
```

**💡 Point clé :** Toujours utiliser `-eq`, `-lt`, etc. pour les nombres.

---

### Question 27

**Réponse correcte : A**

**Explication :**
Syntaxes de boucle for :
```bash
# Sur liste
for i in 1 2 3; do
    echo $i
done

# Sur plage
for i in {1..10}; do
    echo $i
done

# Sur fichiers
for fichier in *.txt; do
    echo $fichier
done

# Style C
for ((i=0; i<10; i++)); do
    echo $i
done
```

**💡 Point clé :** `for var in liste; do ... done` est la syntaxe de base.

---

### Question 28

**Réponse correcte : A**

**Explication :**
Méthode correcte pour lire un fichier ligne par ligne :
```bash
while IFS= read -r ligne; do
    echo "$ligne"
done < fichier.txt
```

- `IFS=` : préserve les espaces de début
- `-r` : ne traite pas les backslashes
- `< fichier.txt` : redirige l'entrée

**❌ Erreur courante :**
```bash
# NE PAS FAIRE
for ligne in $(cat fichier); do
    # Casse les lignes avec des espaces
done
```

**💡 Point clé :** `while read` est la méthode standard pour lire un fichier ligne par ligne.

---

### Question 29

**Réponse correcte : B. `$(commande)`**

**Explication :**
Deux syntaxes de substitution de commande :
- `` `commande` `` : ancienne syntaxe (backticks)
- `$(commande)` : nouvelle syntaxe (préférée)

Avantages de `$()` :
- Plus lisible
- Permet l'imbrication : `$(cmd1 $(cmd2))`
- Pas de confusion avec les guillemets

```bash
date_actuelle=$(date +%Y-%m-%d)
utilisateurs=$(cut -d: -f1 /etc/passwd)
```

**💡 Point clé :** Toujours préférer `$()` aux backticks.

---

### Question 30

**Réponse correcte : B. Succès**

**Explication :**
Conventions de codes de retour :
- `0` : succès
- `1` : erreur générique
- `2` : usage incorrect
- `126` : commande non exécutable
- `127` : commande non trouvée
- `128+n` : tué par signal n

```bash
ls /tmp
echo $?  # 0 si succès

ls /inexistant
echo $?  # 2 si erreur
```

**💡 Point clé :** 0 = succès, non-zéro = erreur (inverse de la logique booléenne).

---

### Question 31

**Réponse correcte : A. `echo $?`**

**Explication :**
`$?` contient le code de retour de la dernière commande :
```bash
grep "pattern" fichier.txt
if [ $? -eq 0 ]; then
    echo "Trouvé"
else
    echo "Non trouvé"
fi

# Équivalent (plus idiomatique)
if grep "pattern" fichier.txt; then
    echo "Trouvé"
fi
```

**💡 Point clé :** `$?` est écrasé par chaque nouvelle commande.

---

### Question 32

**Réponse correcte : B. `set -x`**

**Explication :**
Options de débogage utiles :
```bash
set -x  # Affiche chaque commande avant exécution
set -e  # Arrête en cas d'erreur
set -u  # Erreur si variable non définie
set -o pipefail  # Code retour du pipe = dernière erreur

# Combinaison (mode strict)
set -euxo pipefail

# Désactiver
set +x
```

**💡 Point clé :** `set -x` est l'outil principal de débogage de scripts.

---

### Question 33

**Réponse correcte : A. `read -s password`**

**Explication :**
Options utiles de `read` :
```bash
read -s password         # silencieux (mot de passe)
read -p "Nom: " nom      # avec prompt
read -n 1 touche         # limite à 1 caractère
read -t 5 reponse        # timeout 5 secondes
read -a tableau          # lire dans un tableau
```

Exemple d'utilisation :
```bash
read -sp "Mot de passe: " mdp
echo  # nouvelle ligne après le mot de passe
```

**💡 Point clé :** `-s` (silent) pour les mots de passe.

---

### Question 34

**Réponses correctes : A, B**

**Explication :**
Deux structures pour conditions multiples :

**if/elif/else** : conditions complexes
```bash
if [ condition1 ]; then
    ...
elif [ condition2 ]; then
    ...
else
    ...
fi
```

**case** : comparaison avec patterns
```bash
case $var in
    pattern1)
        ...
        ;;
    pattern2|pattern3)
        ...
        ;;
    *)
        ...
        ;;
esac
```

**💡 Point clé :** `case` est plus lisible pour tester une variable contre plusieurs valeurs.

---

### Question 35

**Réponse correcte : A**

**Explication :**
Commande `mail` (requiert `mailutils` ou équivalent) :
```bash
# Simple
echo "Message" | mail -s "Sujet" user@example.com

# Avec fichier
mail -s "Sujet" user@example.com < message.txt

# Avec pièce jointe
echo "Message" | mail -s "Sujet" -A fichier.pdf user@example.com

# Plusieurs destinataires
echo "Message" | mail -s "Sujet" user1@ex.com user2@ex.com
```

**💡 Point clé :** `-s` pour le sujet (subject), pipe pour le contenu.

---

### Question 36

**Réponse correcte : B. Arrête le script en cas d'erreur**

**Explication :**
`set -e` (errexit) arrête le script si une commande retourne un code non-zéro :
```bash
#!/bin/bash
set -e

mkdir /tmp/test
cd /repertoire/inexistant  # Script s'arrête ici
echo "Cette ligne ne s'exécutera pas"
```

Désactiver temporairement :
```bash
set +e
commande_peut_échouer
set -e
```

**💡 Point clé :** Utile pour éviter d'exécuter des commandes sur des états invalides.

---

### Question 37

**Réponse correcte : B. `$0`**

**Explication :**
`$0` contient le nom du script :
```bash
#!/bin/bash
echo "Nom du script: $0"
echo "Nom seul: $(basename $0)"
echo "Répertoire: $(dirname $0)"

# Si script = /home/user/scripts/backup.sh
# $0 = /home/user/scripts/backup.sh
# basename $0 = backup.sh
# dirname $0 = /home/user/scripts
```

**💡 Point clé :** Utile pour les messages d'aide et les logs.

---

### Question 38

**Réponse correcte : A. `commande && echo "Succès"`**

**Explication :**
Opérateurs de chaînage :
```bash
cmd1 && cmd2  # cmd2 si cmd1 réussit
cmd1 || cmd2  # cmd2 si cmd1 échoue
cmd1 ; cmd2   # cmd2 toujours exécutée

# Exemples
cd /tmp && echo "Changement réussi"
grep pattern file || echo "Non trouvé"
make && make test && make install
```

**💡 Point clé :** `&&` = ET logique, `||` = OU logique pour le contrôle de flux.

---

### Question 39

**Réponses correctes : A, B**

**Explication :**
Deux syntaxes pour une boucle infinie :
```bash
# Méthode 1 (lisible)
while true; do
    echo "Boucle infinie"
    sleep 1
done

# Méthode 2 (style C)
for (( ; ; )); do
    echo "Boucle infinie"
    sleep 1
done

# Sortir avec break ou Ctrl+C
```

**💡 Point clé :** `while true` est plus idiomatique en Bash.

---

### Question 40

**Réponse correcte : B. `return 0`**

**Explication :**
Différence entre `return` et `exit` :
- `return` : termine une fonction, retourne au script
- `exit` : termine le script entier

```bash
ma_fonction() {
    if [ condition ]; then
        return 0  # Succès
    else
        return 1  # Erreur
    fi
}

ma_fonction
if [ $? -eq 0 ]; then
    echo "Fonction réussie"
fi
```

**💡 Point clé :** `return` pour fonctions, `exit` pour scripts.

---

