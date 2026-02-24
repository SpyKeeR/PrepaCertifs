# Notes de Révision - Sujet 105 : Shells et Scripts Shell

**LPIC-1 Examen 102-500**

**Pondération du sujet : 4 + 4 + 3 = 11 points**

---

## Table des matières

- [105.1 Personnalisation et utilisation de l'environnement du shell (Poids : 4)](#1051-personnalisation-et-utilisation-de-lenvironnement-du-shell)
- [105.2 Personnalisation ou écriture de scripts simples (Poids : 4)](#1052-personnalisation-ou-écriture-de-scripts-simples)
- [105.3 Gestion SQL (Poids : 3)](#1053-gestion-sql)

---

## 105.1 Personnalisation et utilisation de l'environnement du shell

**Poids : 4**

### 🎯 Objectifs clés

- Définir les variables d'environnement (PATH) lors de la connexion ou au lancement d'un shell
- Créer des fonctions Bash pour des séquences de commandes fréquentes
- Mettre à jour les répertoires squelette pour les nouveaux comptes utilisateurs
- Définir correctement la liste des chemins d'accès pour les commandes

### 📚 Concepts fondamentaux

#### Types de shells

**Shell de connexion vs. shell simple (non-login)**

1. **Shell de connexion interactif** :
   - Invoqué lors de la connexion (login) au système
   - Exemples : connexion SSH, `su -`, `bash --login`
   - Fichiers exécutés (dans l'ordre) :
     - `/etc/profile` (système)
     - `~/.bash_profile`, `~/.bash_login` ou `~/.profile` (premier trouvé)
     - `~/.bash_logout` (à la déconnexion)

2. **Shell interactif simple (non-login)** :
   - Ouvert après connexion (nouveau terminal)
   - Exemples : `bash`, nouveau terminal dans GUI
   - Fichiers exécutés :
     - `/etc/bash.bashrc` (système)
     - `~/.bashrc` (utilisateur)

3. **Shell non-interactif** :
   - Scripts shell, tâches automatisées
   - Utilise la variable `BASH_ENV` si définie

**Identifier le type de shell actuel** :
```bash
# Shell de connexion affiche : -bash ou -su
# Shell simple affiche : bash ou /bin/bash
echo $0

# Vérifier si shell interactif
[[ $- == *i* ]] && echo "Interactif" || echo "Non-interactif"

# Vérifier si shell de connexion
shopt -q login_shell && echo "Shell de connexion" || echo "Shell simple"
```

#### Fichiers de configuration essentiels

**Niveau système (global)** :

| Fichier | Shell | Description |
|---------|-------|-------------|
| `/etc/profile` | Connexion | Configuration globale pour shells Bourne compatibles |
| `/etc/profile.d/*` | Connexion | Scripts exécutés par `/etc/profile` |
| `/etc/bash.bashrc` | Interactif | Configuration Bash pour tous les utilisateurs |
| `/etc/bashrc` | Interactif | Alternative RedHat/CentOS |

**Niveau utilisateur** :

| Fichier | Shell | Description |
|---------|-------|-------------|
| `~/.bash_profile` | Connexion | 1ère priorité, spécifique Bash |
| `~/.bash_login` | Connexion | 2ème priorité si `.bash_profile` absent |
| `~/.profile` | Connexion | 3ème priorité, compatible sh |
| `~/.bashrc` | Interactif | Configuration interactive utilisateur |
| `~/.bash_logout` | Déconnexion | Commandes à la fermeture du shell |
| `~/.bash_aliases` | - | Alias personnalisés (sourcé par `.bashrc`) |

**💡 Ordre d'exécution pour shell de connexion** :
1. `/etc/profile` → `/etc/profile.d/*` → `/etc/bash.bashrc`
2. `~/.bash_profile` OU `~/.bash_login` OU `~/.profile`
3. Le fichier utilisateur peut sourcer `~/.bashrc`

#### Variables d'environnement

**Variables shell vs. variables d'environnement** :

```bash
# Variable shell (locale au shell actuel)
MY_VAR="valeur"

# Variable d'environnement (disponible aux processus enfants)
export MY_VAR="valeur"
# ou
MY_VAR="valeur"
export MY_VAR
```

**Variables importantes** :

| Variable | Description | Exemple |
|----------|-------------|---------|
| `PATH` | Chemins de recherche des commandes | `/usr/local/bin:/usr/bin:/bin` |
| `HOME` | Répertoire personnel | `/home/username` |
| `USER` | Nom d'utilisateur | `maxime` |
| `SHELL` | Shell par défaut | `/bin/bash` |
| `PWD` | Répertoire de travail actuel | `/home/maxime/documents` |
| `OLDPWD` | Répertoire précédent | `/home/maxime` |
| `PS1` | Prompt principal | `\u@\h:\w\$ ` |
| `PS2` | Prompt secondaire | `> ` |
| `HISTSIZE` | Taille historique en mémoire | `1000` |
| `HISTFILESIZE` | Taille fichier historique | `2000` |
| `HISTFILE` | Fichier historique | `~/.bash_history` |
| `LANG` | Langue/locale du système | `fr_FR.UTF-8` |
| `EDITOR` | Éditeur par défaut | `vim` |
| `PAGER` | Programme de pagination | `less` |

**Gestion du PATH** :

```bash
# Afficher le PATH
echo $PATH

# Ajouter un répertoire au début
export PATH="/usr/local/bin:$PATH"

# Ajouter un répertoire à la fin
export PATH="$PATH:$HOME/bin"

# Ajouter uniquement si pas déjà présent
[[ ":$PATH:" != *":/opt/bin:"* ]] && export PATH="/opt/bin:$PATH"

# Supprimer un répertoire du PATH
PATH=$(echo "$PATH" | sed 's|:/opt/bin||g')
```

**Commandes de gestion des variables** :

```bash
# Afficher toutes les variables d'environnement
env
printenv

# Afficher une variable spécifique
printenv PATH
echo $PATH

# Afficher toutes les variables (y compris shell)
set

# Définir une variable temporaire pour une commande
LANG=en_US.UTF-8 date

# Supprimer une variable
unset MY_VAR

# Lister les variables exportées
export -p
```

#### Sourcing de fichiers

**Exécuter des fichiers de configuration** :

```bash
# Méthode 1 : commande point (POSIX)
. ~/.bashrc

# Méthode 2 : commande source (Bash)
source ~/.bashrc

# Différence avec exécution directe
./script.sh      # Exécute dans un sous-shell (nouveau processus)
source script.sh # Exécute dans le shell actuel
```

**Exemple de sourcing dans `.profile`** :
```bash
# ~/.profile
if [ -n "$BASH_VERSION" ]; then
    if [ -f "$HOME/.bashrc" ]; then
        . "$HOME/.bashrc"
    fi
fi
```

#### Alias

**Créer et gérer des alias** :

```bash
# Créer un alias
alias ll='ls -lah'
alias update='sudo apt update && sudo apt upgrade'
alias grep='grep --color=auto'

# Lister tous les alias
alias

# Supprimer un alias
unalias ll

# Supprimer tous les alias
unalias -a

# Exécuter la commande sans alias (avec \)
\ls

# Alias permanent : ajouter dans ~/.bashrc ou ~/.bash_aliases
echo "alias ll='ls -lah'" >> ~/.bashrc
```

**💡 Bonnes pratiques** :
- Mettre les alias dans `~/.bash_aliases`
- Source ce fichier depuis `~/.bashrc` :
  ```bash
  if [ -f ~/.bash_aliases ]; then
      . ~/.bash_aliases
  fi
  ```

#### Fonctions

**Créer des fonctions Bash** :

```bash
# Syntaxe 1
function nom_fonction {
    commandes
}

# Syntaxe 2 (préférée)
nom_fonction() {
    commandes
}

# Exemple : créer un répertoire et y entrer
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Exemple : sauvegarde avec timestamp
backup() {
    if [ -f "$1" ]; then
        cp "$1" "$1.$(date +%Y%m%d-%H%M%S).bak"
        echo "Sauvegarde créée : $1.$(date +%Y%m%d-%H%M%S).bak"
    else
        echo "Erreur : fichier $1 introuvable"
        return 1
    fi
}

# Exemple : extraction universelle
extract() {
    if [ -f "$1" ]; then
        case "$1" in
            *.tar.bz2)   tar xjf "$1"    ;;
            *.tar.gz)    tar xzf "$1"    ;;
            *.bz2)       bunzip2 "$1"    ;;
            *.gz)        gunzip "$1"     ;;
            *.tar)       tar xf "$1"     ;;
            *.zip)       unzip "$1"      ;;
            *.Z)         uncompress "$1" ;;
            *)           echo "'$1' ne peut pas être extrait" ;;
        esac
    else
        echo "'$1' n'est pas un fichier valide"
    fi
}
```

**Paramètres de fonction** :
```bash
ma_fonction() {
    echo "Nombre d'arguments : $#"
    echo "Premier argument : $1"
    echo "Deuxième argument : $2"
    echo "Tous les arguments : $@"
    echo "Nom de la fonction : $FUNCNAME"
}
```

**Lister et supprimer des fonctions** :
```bash
# Lister toutes les fonctions
declare -F

# Afficher le corps d'une fonction
declare -f nom_fonction

# Supprimer une fonction
unset -f nom_fonction
```

#### Personnalisation du prompt (PS1)

**Séquences d'échappement courantes** :

| Séquence | Description |
|----------|-------------|
| `\u` | Nom d'utilisateur |
| `\h` | Nom d'hôte (court) |
| `\H` | Nom d'hôte (FQDN) |
| `\w` | Répertoire de travail complet |
| `\W` | Nom du répertoire de travail |
| `\d` | Date (format: Jeu Déc 02) |
| `\t` | Heure (HH:MM:SS) |
| `\@` | Heure (format 12h AM/PM) |
| `\$` | `#` si root, `$` sinon |
| `\n` | Nouvelle ligne |
| `\[` | Début séquence non-imprimable |
| `\]` | Fin séquence non-imprimable |

**Codes couleur ANSI** :

```bash
# Couleurs texte
BLACK='\[\033[0;30m\]'
RED='\[\033[0;31m\]'
GREEN='\[\033[0;32m\]'
YELLOW='\[\033[0;33m\]'
BLUE='\[\033[0;34m\]'
PURPLE='\[\033[0;35m\]'
CYAN='\[\033[0;36m\]'
WHITE='\[\033[0;37m\]'
RESET='\[\033[0m\]'

# Exemple de prompt coloré
PS1="${GREEN}\u@\h${RESET}:${BLUE}\w${RESET}\$ "
```

**Exemples de prompts** :

```bash
# Simple
PS1="\u@\h:\w\$ "
# Résultat : maxime@debian:/home/maxime$

# Avec couleurs et git branch (nécessite git-prompt)
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Prompt sur deux lignes
PS1="\n\[\033[1;34m\][\u@\h:\w]\[\033[0m\]\n\$ "
```

#### Répertoires squelettes (/etc/skel)

**Structure de /etc/skel** :
- Contient les fichiers par défaut pour nouveaux utilisateurs
- Copié automatiquement par `useradd` dans `/home/nouvel_utilisateur/`

```bash
# Contenu typique
ls -la /etc/skel/
# .bash_logout
# .bashrc
# .profile
# .bash_aliases (optionnel)

# Personnaliser pour nouveaux utilisateurs
sudo nano /etc/skel/.bashrc

# Créer un alias par défaut pour tous
echo "alias ll='ls -lah'" | sudo tee -a /etc/skel/.bash_aliases

# Créer un nouveau fichier dans skel
sudo nano /etc/skel/.vimrc
```

**Créer un utilisateur avec skel** :
```bash
# Utilise /etc/skel par défaut
sudo useradd -m -s /bin/bash nouvel_user

# Utiliser un répertoire skel personnalisé
sudo useradd -m -k /path/to/custom/skel nouvel_user
```

### 🔑 Commandes essentielles

| Commande | Description | Exemple |
|----------|-------------|---------|
| `env` | Afficher les variables d'environnement | `env` |
| `export` | Exporter une variable | `export PATH="/usr/local/bin:$PATH"` |
| `set` | Afficher toutes les variables | `set \| less` |
| `unset` | Supprimer une variable | `unset MY_VAR` |
| `source` | Exécuter un script dans le shell actuel | `source ~/.bashrc` |
| `.` | Idem que source (POSIX) | `. ~/.profile` |
| `alias` | Créer/lister des alias | `alias ll='ls -lah'` |
| `unalias` | Supprimer un alias | `unalias ll` |
| `function` | Déclarer une fonction | `function hello { echo "Bonjour"; }` |
| `declare` | Déclarer des variables/fonctions | `declare -f` (lister fonctions) |
| `type` | Afficher le type d'une commande | `type ls` |
| `which` | Localiser une commande | `which python3` |
| `whereis` | Localiser binaires, sources, man | `whereis bash` |

### 💡 Points importants pour l'examen

1. **Ordre de priorité des fichiers de configuration** :
   - Shell de connexion : `/etc/profile` → `~/.bash_profile` OU `~/.bash_login` OU `~/.profile`
   - Shell interactif : `/etc/bash.bashrc` → `~/.bashrc`

2. **Différence entre shell et environnement** :
   - Variable shell : accessible uniquement dans le shell actuel
   - Variable d'environnement : accessible aux processus enfants (après `export`)

3. **Modification du PATH** :
   - Ajouter au début : `export PATH="/nouveau/chemin:$PATH"`
   - Ajouter à la fin : `export PATH="$PATH:/nouveau/chemin"`
   - Toujours inclure `$PATH` pour conserver les chemins existants

4. **Différence entre alias et fonction** :
   - Alias : simple substitution de texte, pas de logique
   - Fonction : peut contenir des conditions, boucles, paramètres

5. **Sourcing vs exécution** :
   - `source script.sh` : exécute dans le shell actuel (modifie l'environnement)
   - `./script.sh` : exécute dans un sous-shell (environnement isolé)

6. **Répertoire skel** :
   - `/etc/skel` : modèle pour nouveaux utilisateurs
   - Modifié par l'administrateur, copié par `useradd -m`

### 📝 Exemples pratiques

**Configuration complète d'un environnement utilisateur** :

```bash
# ~/.bash_profile (shell de connexion)
# Source .bashrc si présent
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi

# Ajouter ~/bin au PATH
if [ -d "$HOME/bin" ]; then
    export PATH="$HOME/bin:$PATH"
fi

# Variables d'environnement
export EDITOR=vim
export VISUAL=vim
export PAGER=less
```

```bash
# ~/.bashrc (shell interactif)
# Si non-interactif, ne rien faire
[[ $- != *i* ]] && return

# Historique
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoreboth:erasedups
shopt -s histappend

# Options shell
shopt -s checkwinsize
shopt -s cdspell

# Alias
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# Fonctions
if [ -f ~/.bash_functions ]; then
    . ~/.bash_functions
fi

# Prompt
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
```

```bash
# ~/.bash_aliases
alias ll='ls -lah'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias ..='cd ..'
alias ...='cd ../..'
alias update='sudo apt update && sudo apt upgrade'
```

---

## 105.2 Personnalisation ou écriture de scripts simples

**Poids : 4**

### 🎯 Objectifs clés

- Écrire et déboguer des scripts shell simples
- Utiliser la boucle `for` standard et les tests de conditions
- Utiliser les commandes de substitution
- Tester les valeurs de retour pour la réussite ou l'échec
- Envoyer des messages à l'utilisateur par email

### 📚 Concepts fondamentaux

#### Structure d'un script shell

**Shebang (#!)** :

```bash
#!/bin/bash
# Script doit commencer par le shebang

#!/bin/sh
# Pour compatibilité POSIX

#!/usr/bin/env bash
# Portable (utilise PATH pour trouver bash)
```

**Structure de base** :

```bash
#!/bin/bash
#
# Nom: mon_script.sh
# Description: Ce script fait quelque chose
# Auteur: Maxime
# Date: 2026-01-28

# Variables globales
VERSION="1.0"
DEBUG=false

# Fonctions
function usage() {
    echo "Usage: $0 [options]"
    echo "  -h    Afficher l'aide"
    echo "  -v    Afficher la version"
}

# Script principal
main() {
    # Logique du script
    echo "Début du script"
    
    # Instructions
    
    echo "Fin du script"
}

# Appel de la fonction principale
main "$@"
```

**Rendre un script exécutable** :
```bash
chmod +x mon_script.sh
chmod 755 mon_script.sh
```

#### Variables dans les scripts

**Variables spéciales** :

| Variable | Description | Exemple |
|----------|-------------|---------|
| `$0` | Nom du script | `./mon_script.sh` |
| `$1`, `$2`, ... | Arguments positionnels | `$1` = premier argument |
| `$#` | Nombre d'arguments | `3` |
| `$@` | Tous les arguments (liste) | `"arg1" "arg2" "arg3"` |
| `$*` | Tous les arguments (chaîne) | `"arg1 arg2 arg3"` |
| `$?` | Code retour dernière commande | `0` (succès), `1-255` (erreur) |
| `$$` | PID du script | `12345` |
| `$!` | PID dernière commande background | `12346` |
| `$_` | Dernier argument de la dernière commande | `fichier.txt` |

**Manipulation de variables** :

```bash
# Déclaration
nom="Maxime"
age=25

# Lecture seule
readonly PI=3.14159
declare -r CONSTANTE="valeur"

# Tableaux
fruits=("pomme" "banane" "orange")
echo ${fruits[0]}      # pomme
echo ${fruits[@]}      # tous les éléments
echo ${#fruits[@]}     # nombre d'éléments

# Longueur d'une chaîne
echo ${#nom}           # 6

# Sous-chaîne
texte="Bonjour le monde"
echo ${texte:0:7}      # Bonjour
echo ${texte:8}        # le monde

# Remplacement
fichier="document.txt"
echo ${fichier%.txt}       # document (supprime .txt)
echo ${fichier/txt/pdf}    # document.pdf (remplace)

# Valeur par défaut
echo ${VAR:-"valeur par défaut"}   # Si VAR vide/non définie
echo ${VAR:="valeur"}              # Assigne si vide/non définie
```

#### Tests et conditions

**Commande test** :

```bash
# Syntaxe 1
test -f fichier.txt

# Syntaxe 2 (équivalent)
[ -f fichier.txt ]

# Syntaxe 3 (Bash étendu)
[[ -f fichier.txt ]]
```

**Tests sur fichiers** :

| Test | Description |
|------|-------------|
| `-e fichier` | Fichier existe |
| `-f fichier` | Fichier régulier existe |
| `-d fichier` | Répertoire existe |
| `-L fichier` | Lien symbolique existe |
| `-r fichier` | Fichier lisible |
| `-w fichier` | Fichier modifiable |
| `-x fichier` | Fichier exécutable |
| `-s fichier` | Fichier non vide |
| `fichier1 -nt fichier2` | fichier1 plus récent que fichier2 |
| `fichier1 -ot fichier2` | fichier1 plus ancien que fichier2 |

**Tests sur chaînes** :

| Test | Description |
|------|-------------|
| `-z "$str"` | Chaîne vide |
| `-n "$str"` | Chaîne non vide |
| `"$str1" = "$str2"` | Chaînes égales |
| `"$str1" != "$str2"` | Chaînes différentes |
| `"$str1" < "$str2"` | str1 avant str2 (ordre alphabétique) |

**Tests numériques** :

| Test | Description |
|------|-------------|
| `$a -eq $b` | Égal (equal) |
| `$a -ne $b` | Différent (not equal) |
| `$a -lt $b` | Inférieur (less than) |
| `$a -le $b` | Inférieur ou égal |
| `$a -gt $b` | Supérieur (greater than) |
| `$a -ge $b` | Supérieur ou égal |

**Opérateurs logiques** :

```bash
# ET logique
[ condition1 ] && [ condition2 ]
[ condition1 -a condition2 ]
[[ condition1 && condition2 ]]

# OU logique
[ condition1 ] || [ condition2 ]
[ condition1 -o condition2 ]
[[ condition1 || condition2 ]]

# Négation
! [ condition ]
[ ! condition ]
```

#### Structures conditionnelles

**if/then/else** :

```bash
# Syntaxe de base
if [ condition ]; then
    commandes
fi

# if/else
if [ condition ]; then
    commandes_si_vrai
else
    commandes_si_faux
fi

# if/elif/else
if [ condition1 ]; then
    commandes1
elif [ condition2 ]; then
    commandes2
else
    commandes3
fi

# Exemple pratique
if [ -f "/etc/passwd" ]; then
    echo "Le fichier existe"
    nb_lignes=$(wc -l < /etc/passwd)
    echo "Il contient $nb_lignes lignes"
else
    echo "Le fichier n'existe pas"
fi
```

**case** :

```bash
case $variable in
    pattern1)
        commandes1
        ;;
    pattern2|pattern3)
        commandes2
        ;;
    *)
        commandes_par_defaut
        ;;
esac

# Exemple : menu
echo "Choisissez une option:"
echo "1) Installer"
echo "2) Désinstaller"
echo "3) Quitter"
read -p "Votre choix: " choix

case $choix in
    1)
        echo "Installation en cours..."
        ;;
    2)
        echo "Désinstallation en cours..."
        ;;
    3)
        echo "Au revoir!"
        exit 0
        ;;
    *)
        echo "Option invalide"
        exit 1
        ;;
esac
```

#### Boucles

**for** :

```bash
# Boucle sur liste
for item in item1 item2 item3; do
    echo $item
done

# Boucle sur fichiers
for fichier in *.txt; do
    echo "Traitement de $fichier"
done

# Boucle style C
for ((i=1; i<=10; i++)); do
    echo "Itération $i"
done

# Boucle sur arguments
for arg in "$@"; do
    echo "Argument: $arg"
done

# Boucle sur sortie de commande
for user in $(cut -d: -f1 /etc/passwd); do
    echo "Utilisateur: $user"
done

# Boucle sur plage
for i in {1..5}; do
    echo $i
done

for lettre in {a..z}; do
    echo $lettre
done
```

**while** :

```bash
# while simple
compteur=1
while [ $compteur -le 5 ]; do
    echo "Compteur: $compteur"
    ((compteur++))
done

# Lecture de fichier ligne par ligne
while IFS= read -r ligne; do
    echo "Ligne: $ligne"
done < fichier.txt

# Boucle infinie
while true; do
    echo "Presse Ctrl+C pour arrêter"
    sleep 1
done
```

**until** :

```bash
# Continue jusqu'à ce que la condition soit vraie
compteur=1
until [ $compteur -gt 5 ]; do
    echo "Compteur: $compteur"
    ((compteur++))
done
```

**Contrôle de boucle** :

```bash
# break : sortir de la boucle
for i in {1..10}; do
    if [ $i -eq 5 ]; then
        break
    fi
    echo $i
done

# continue : passer à l'itération suivante
for i in {1..10}; do
    if [ $i -eq 5 ]; then
        continue
    fi
    echo $i
done
```

#### Substitution de commandes

**Syntaxes** :

```bash
# Ancienne syntaxe (backticks)
resultat=`commande`
date_actuelle=`date +%Y-%m-%d`

# Nouvelle syntaxe (préférée)
resultat=$(commande)
date_actuelle=$(date +%Y-%m-%d)

# Substitution imbriquée
fichiers=$(ls -1 $(pwd))
utilisateurs=$(echo $(cut -d: -f1 /etc/passwd))
```

**Exemples d'utilisation** :

```bash
# Compter les fichiers
nb_fichiers=$(ls -1 | wc -l)
echo "Nombre de fichiers: $nb_fichiers"

# Obtenir le nom d'hôte
hostname=$(hostname)
echo "Hôte: $hostname"

# Traitement de texte
users=$(cut -d: -f1 /etc/passwd | sort)
for user in $users; do
    echo "Utilisateur: $user"
done
```

#### Codes de retour

**Utilisation des codes de retour** :

```bash
# $? contient le code de retour de la dernière commande
ls /tmp
echo $?  # 0 si succès

ls /repertoire_inexistant
echo $?  # 2 si erreur

# Conventions
# 0     : succès
# 1     : erreur générale
# 2     : usage incorrect
# 126   : commande non exécutable
# 127   : commande introuvable
# 128+n : signal n (ex: 130 = Ctrl+C)

# Définir le code de retour du script
exit 0   # succès
exit 1   # erreur

# Test du code de retour
if commande; then
    echo "Commande réussie"
else
    echo "Commande échouée"
fi

# Opérateurs && et ||
commande1 && commande2  # commande2 si commande1 réussit
commande1 || commande2  # commande2 si commande1 échoue

# Exemple pratique
cd /tmp && echo "Changement réussi" || echo "Échec du changement"
```

**Gestion des erreurs** :

```bash
#!/bin/bash
# Arrêter en cas d'erreur
set -e

# Arrêter si variable non définie
set -u

# Afficher les commandes exécutées (debug)
set -x

# Désactiver
set +e
set +u
set +x

# Combinaison
set -euo pipefail  # Mode strict
```

#### Entrées/Sorties et redirection

**Lecture d'entrée utilisateur** :

```bash
# read simple
read variable
read -p "Entrez votre nom: " nom

# Options de read
read -p "Prompt: " var           # Avec prompt
read -s mot_de_passe             # Silencieux (pas d'écho)
read -n 1 touche                 # Limite à 1 caractère
read -t 5 reponse                # Timeout de 5 secondes
read -a tableau                  # Lire dans un tableau
read var1 var2 var3              # Lire plusieurs variables

# Exemple avec valeur par défaut
read -p "Port [8080]: " port
port=${port:-8080}
echo "Port sélectionné: $port"
```

**Redirections** :

```bash
# Redirection de sortie
commande > fichier          # Écrase fichier
commande >> fichier         # Ajoute à fichier

# Redirection d'erreur
commande 2> erreurs.txt     # Erreurs vers fichier
commande 2>&1               # Erreurs vers stdout

# Redirection combinée
commande &> fichier         # stdout et stderr vers fichier
commande > fichier 2>&1     # Idem

# Redirection d'entrée
commande < fichier_entree

# Here document
cat << EOF
Ligne 1
Ligne 2
EOF

# Here string
grep "pattern" <<< "texte à chercher"
```

#### Envoi de mails

**Commande mail** :

```bash
# Installation (si nécessaire)
sudo apt install mailutils

# Envoi simple
echo "Corps du message" | mail -s "Sujet" destinataire@example.com

# Avec fichier
mail -s "Sujet" dest@example.com < fichier.txt

# Pièce jointe
echo "Message" | mail -s "Sujet" -A fichier.pdf dest@example.com

# Avec sendmail
echo -e "Subject: Test\n\nCorps du message" | sendmail dest@example.com
```

**Exemple dans un script** :

```bash
#!/bin/bash
# Script de sauvegarde avec notification

BACKUP_DIR="/backup"
LOG_FILE="/var/log/backup.log"
ADMIN_EMAIL="admin@example.com"

# Effectuer la sauvegarde
tar -czf $BACKUP_DIR/backup-$(date +%Y%m%d).tar.gz /home 2>&1 | tee -a $LOG_FILE

# Vérifier le résultat
if [ ${PIPESTATUS[0]} -eq 0 ]; then
    echo "Sauvegarde réussie le $(date)" | mail -s "Sauvegarde OK" $ADMIN_EMAIL
else
    echo "Échec de la sauvegarde le $(date)" | mail -s "ERREUR Sauvegarde" $ADMIN_EMAIL
fi
```

### 🔑 Commandes essentielles

| Commande | Description | Exemple |
|----------|-------------|---------|
| `test` | Évaluer une expression | `test -f fichier` |
| `[` | Alias pour test | `[ -d /tmp ]` |
| `[[` | Test étendu Bash | `[[ $var =~ regex ]]` |
| `read` | Lire l'entrée utilisateur | `read -p "Nom: " nom` |
| `echo` | Afficher du texte | `echo "Bonjour"` |
| `printf` | Affichage formaté | `printf "%s\n" "texte"` |
| `exit` | Terminer le script | `exit 0` |
| `return` | Retourner d'une fonction | `return 1` |
| `exec` | Remplacer le shell actuel | `exec bash` |
| `mail` | Envoyer un email | `echo "msg" \| mail -s "sujet" user` |
| `seq` | Générer une séquence | `seq 1 10` |
| `basename` | Nom de fichier sans chemin | `basename /path/file.txt` |
| `dirname` | Chemin sans nom de fichier | `dirname /path/file.txt` |

### 💡 Points importants pour l'examen

1. **Shebang** :
   - Toujours commencer par `#!/bin/bash` ou `#!/bin/sh`
   - Différence : bash a plus de fonctionnalités que sh (POSIX)

2. **Tests** :
   - `[ ]` : compatible POSIX, limité
   - `[[ ]]` : Bash uniquement, plus puissant (regex, &&, ||)
   - Toujours entre guillemets : `[ "$var" = "valeur" ]`

3. **Codes de retour** :
   - 0 = succès
   - Non-zéro = échec
   - Accessible via `$?`
   - Permet le chaînage : `cmd1 && cmd2 || cmd3`

4. **Boucles for** :
   - Sur liste : `for i in a b c`
   - Sur fichiers : `for f in *.txt`
   - Style C : `for ((i=0; i<10; i++))`

5. **Substitution** :
   - Préférer `$(commande)` à `` `commande` ``
   - Permet l'imbrication : `$(cmd1 $(cmd2))`

### 📝 Exemples pratiques

**Script complet avec bonnes pratiques** :

```bash
#!/bin/bash
#
# backup.sh - Script de sauvegarde automatique
# Auteur: Maxime
# Date: 2026-01-28

set -euo pipefail  # Mode strict

# Configuration
readonly SCRIPT_NAME=$(basename "$0")
readonly BACKUP_DIR="/backup"
readonly SOURCE_DIR="/home"
readonly LOG_FILE="/var/log/${SCRIPT_NAME}.log"
readonly RETENTION_DAYS=7

# Fonctions
log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

error() {
    log "ERREUR: $*" >&2
    exit 1
}

usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS]

Options:
    -h, --help     Afficher cette aide
    -d DIR         Répertoire source (défaut: $SOURCE_DIR)
    -o DIR         Répertoire de sauvegarde (défaut: $BACKUP_DIR)
    -r DAYS        Rétention en jours (défaut: $RETENTION_DAYS)

Exemples:
    $SCRIPT_NAME
    $SCRIPT_NAME -d /var/www -o /backup/www
EOF
}

cleanup_old_backups() {
    log "Nettoyage des sauvegardes > $RETENTION_DAYS jours"
    find "$BACKUP_DIR" -name "backup-*.tar.gz" -mtime +$RETENTION_DAYS -delete
}

create_backup() {
    local source=$1
    local dest=$2
    local timestamp=$(date +%Y%m%d-%H%M%S)
    local backup_file="$dest/backup-$timestamp.tar.gz"
    
    log "Début de la sauvegarde: $source -> $backup_file"
    
    if tar -czf "$backup_file" "$source" 2>&1 | tee -a "$LOG_FILE"; then
        log "Sauvegarde réussie: $backup_file"
        log "Taille: $(du -h "$backup_file" | cut -f1)"
        return 0
    else
        error "Échec de la sauvegarde"
    fi
}

# Traitement des arguments
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            usage
            exit 0
            ;;
        -d)
            SOURCE_DIR="$2"
            shift 2
            ;;
        -o)
            BACKUP_DIR="$2"
            shift 2
            ;;
        -r)
            RETENTION_DAYS="$2"
            shift 2
            ;;
        *)
            echo "Option inconnue: $1"
            usage
            exit 1
            ;;
    esac
done

# Vérifications préalables
[[ -d "$SOURCE_DIR" ]] || error "Source inexistante: $SOURCE_DIR"
[[ -d "$BACKUP_DIR" ]] || mkdir -p "$BACKUP_DIR"
[[ -w "$BACKUP_DIR" ]] || error "Pas de permission d'écriture: $BACKUP_DIR"

# Exécution
log "=== Démarrage du script de sauvegarde ==="
cleanup_old_backups
create_backup "$SOURCE_DIR" "$BACKUP_DIR"
log "=== Fin du script de sauvegarde ==="
```

---

## 📖 Ressources complémentaires

### Documentation officielle

- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)

### Outils pratiques

- **shellcheck** : vérificateur de syntaxe pour scripts shell
- **explainshell.com** : explique les commandes shell

### Commandes d'aide

```bash
# Aide Bash
man bash
help [commande]
info bash
```

---

## ✅ Checklist de révision

### 105.1 Environnement shell
- [ ] Je comprends la différence entre shell de connexion et shell simple
- [ ] Je connais l'ordre d'exécution des fichiers de configuration
- [ ] Je sais modifier le PATH correctement
- [ ] Je peux créer des alias et des fonctions
- [ ] Je maîtrise le sourcing de fichiers
- [ ] Je connais les variables d'environnement importantes
- [ ] Je sais personnaliser le prompt (PS1)
- [ ] Je comprends le rôle de /etc/skel

### 105.2 Scripts shell
- [ ] Je sais écrire un script avec shebang
- [ ] Je connais les variables spéciales ($0, $1, $#, $@, $?, etc.)
- [ ] Je maîtrise les tests et conditions (if, case)
- [ ] Je sais utiliser les boucles (for, while, until)
- [ ] Je comprends la substitution de commandes
- [ ] Je gère les codes de retour et les erreurs
- [ ] Je sais lire l'entrée utilisateur (read)
- [ ] Je peux envoyer des emails depuis un script

---

**Date de dernière révision :** 28 janvier 2026  
**Sujet suivant :** [Sujet 106 - Interfaces utilisateur et bureaux](#)
