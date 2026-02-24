# 🎯 QCM - Sujet 103 : Commandes GNU et Unix

> **Poids du sujet :** 16 points (~40% de l'examen) - **LE PLUS IMPORTANT !**  
> **Questions :** 50 au total  
> **Objectif :** 38/50 minimum (75%) - Viser 42+ (85%)  
> **Temps estimé :** 50-60 minutes

---

## 📋 Instructions

- Lisez attentivement chaque question
- Une ou plusieurs réponses peuvent être correctes (indiqué)
- Notez vos réponses et vérifiez avec les explications
- Calculez votre score final

---

## 📝 Questions

#### Question 1
Quelle commande affiche TOUTES les variables d'environnement du système ?

- [ ] A) `set`  
- [ ] B) `env`  
- [ ] C) `export`  
- [ ] D) `echo $VAR`

---

#### Question 2
Comment ajouter `/opt/myapp/bin` au PATH de manière PERMANENTE pour l'utilisateur ?

- [ ] A) `export PATH=/opt/myapp/bin`  
- [ ] B) `echo 'export PATH=$PATH:/opt/myapp/bin' >> ~/.bashrc`  
- [ ] C) `PATH=$PATH:/opt/myapp/bin`  
- [ ] D) `set PATH=/opt/myapp/bin`

---

#### Question 3
Quelle variable contient le **code de retour** de la dernière commande exécutée ?

- [ ] A) `$!`  
- [ ] B) `$?`  
- [ ] C) `$$`  
- [ ] D) `$_`

---

#### Question 4
Comment créer un **alias permanent** qui exécute `ls -lah` quand on tape `ll` ?

- [ ] A) `alias ll='ls -lah'`  
- [ ] B) `echo "alias ll='ls -lah'" >> ~/.bashrc && source ~/.bashrc`  
- [ ] C) `ln -s ls ll`  
- [ ] D) `export ll='ls -lah'`

---

#### Question 5
Quelle commande permet de **rechercher dans l'historique** des commandes de manière interactive ?

- [ ] A) `history | grep pattern`  
- [ ] B) Appuyer sur `Ctrl+R`  
- [ ] C) `!!`  
- [ ] D) `!ssh`

---

#### Question 6
Quelle commande affiche le **chemin complet** d'un exécutable dans le PATH ?

- [ ] A) `whereis`  
- [ ] B) `which`  
- [ ] C) `find`  
- [ ] D) `locate`

---

#### Question 7
Comment exécuter **deux commandes séquentiellement** où la **deuxième ne s'exécute QUE si la première réussit** ?

- [ ] A) `command1 ; command2`  
- [ ] B) `command1 && command2`  
- [ ] C) `command1 || command2`  
- [ ] D) `command1 | command2`

---

#### Question 8
Quelle variable spéciale contient le **nombre d'arguments** passés à un script ?

- [ ] A) `$@`  
- [ ] B) `$#`  
- [ ] C) `$*`  
- [ ] D) `$0`

---

#### Question 9
Comment afficher les **10 dernières commandes** de l'historique ?

- [ ] A) `history 10`  
- [ ] B) `history | tail -10`  
- [ ] C) `!-10`  
- [ ] D) Les deux A et B

---

#### Question 10
Quel fichier contient l'**historique des commandes** Bash par défaut ?

- [ ] A) `~/.bash_profile`  
- [ ] B) `~/.bash_history`  
- [ ] C) `~/.bashrc`  
- [ ] D) `/var/log/bash.log`

---

#### Question 11
Quelle commande affiche les **15 premières lignes** d'un fichier ?

- [ ] A) `head -15 file.txt`  
- [ ] B) `tail -15 file.txt`  
- [ ] C) `cat -n 15 file.txt`  
- [ ] D) `less +15 file.txt`

---

#### Question 12
Comment **compter le nombre de lignes** dans un fichier ?

- [ ] A) `wc -l file.txt`  
- [ ] B) `wc -w file.txt`  
- [ ] C) `cat file.txt | count`  
- [ ] D) `lines file.txt`

---

#### Question 13
Quelle commande **extrait les colonnes 1 et 3** d'un fichier CSV (délimiteur virgule) ?

- [ ] A) `cut -d ',' -f 1,3 file.csv`  
- [ ] B) `awk -F',' '{print $1,$3}' file.csv`  
- [ ] C) `grep -E '^[^,]+,[^,]+' file.csv`  
- [ ] D) Les deux A et B

---

#### Question 14
Comment **trier un fichier numériquement** par la **3ème colonne** ?

- [ ] A) `sort -k 3 file.txt`  
- [ ] B) `sort -k 3 -n file.txt`  
- [ ] C) `sort -t ' ' -k 3 -n file.txt`  
- [ ] D) Les deux B et C (si délimiteur espace)

---

#### Question 15
Quelle commande **compte les occurrences** de chaque ligne dupliquée dans un fichier ?

- [ ] A) `uniq file.txt`  
- [ ] B) `sort file.txt | uniq -c`  
- [ ] C) `count file.txt`  
- [ ] D) `grep -c file.txt`

---

#### Question 16
Comment **supprimer toutes les lignes vides** d'un fichier ?

- [ ] A) `grep -v '^$' file.txt`  
- [ ] B) `sed '/^$/d' file.txt`  
- [ ] C) `awk 'NF' file.txt`  
- [ ] D) Toutes les réponses

---

#### Question 17
Comment **copier récursivement** un répertoire avec tous ses fichiers et sous-répertoires ?

- [ ] A) `cp dir1 dir2`  
- [ ] B) `cp -r dir1 dir2`  
- [ ] C) `cp -R dir1 dir2`  
- [ ] D) Les deux B et C

---

#### Question 18
Quelle différence entre **lien symbolique** et **lien dur** ? (Plusieurs réponses possibles)

- [ ] A) Lien symbolique peut pointer vers autre partition  
- [ ] B) Lien dur partage même inode que fichier original  
- [ ] C) Supprimer original casse lien symbolique mais pas lien dur  
- [ ] D) Toutes les réponses

---

#### Question 19
Comment **déplacer tous les fichiers .txt** d'un répertoire vers un autre ?

- [ ] A) `mv *.txt /dest/`  
- [ ] B) `mv /source/*.txt /dest/`  
- [ ] C) `find /source -name "*.txt" -exec mv {} /dest/ \;`  
- [ ] D) Toutes les réponses

---

#### Question 20
Comment créer un **fichier de 100 Mo** rempli de zéros ?

- [ ] A) `dd if=/dev/zero of=file.bin bs=1M count=100`  
- [ ] B) `fallocate -l 100M file.bin`  
- [ ] C) `truncate -s 100M file.bin`  
- [ ] D) Toutes les réponses

---

#### Question 21
Quelle commande affiche le **type** d'un fichier (texte, binaire, etc.) ?

- [ ] A) `type file.txt`  
- [ ] B) `file file.txt`  
- [ ] C) `ls -l file.txt`  
- [ ] D) `stat file.txt`

---

#### Question 22
Comment **renommer massivement** tous les fichiers `.txt` en `.bak` dans le répertoire courant ?

- [ ] A) `rename 's/\.txt$/\.bak/' *.txt`  
- [ ] B) `for f in *.txt; do mv "$f" "${f%.txt}.bak"; done`  
- [ ] C) `mv *.txt *.bak`  
- [ ] D) Les deux A et B

---

#### Question 23
Comment **rediriger STDOUT et STDERR** vers le **même fichier** ?

- [ ] A) `command > output.txt 2>&1`  
- [ ] B) `command &> output.txt`  
- [ ] C) `command > output.txt 2> output.txt`  
- [ ] D) Les deux A et B

---

#### Question 24
Quelle commande permet d'**afficher ET sauvegarder** la sortie d'une commande simultanément ?

- [ ] A) `command | tee output.txt`  
- [ ] B) `command > output.txt`  
- [ ] C) `command >> output.txt`  
- [ ] D) `command | cat > output.txt`

---

#### Question 25
Que fait la commande `command 2> /dev/null` ?

- [ ] A) Redirige STDOUT vers /dev/null  
- [ ] B) Redirige STDERR vers /dev/null (supprime erreurs)  
- [ ] C) Redirige STDOUT et STDERR vers /dev/null  
- [ ] D) Supprime le fichier /dev/null

---

#### Question 26 (Suite des questions 103.4)

Comment **chaîner 3 commandes** où chacune traite la sortie de la précédente ?

- [ ] A) `cmd1 ; cmd2 ; cmd3`  
- [ ] B) `cmd1 && cmd2 && cmd3`  
- [ ] C) `cmd1 | cmd2 | cmd3`  
- [ ] D) `cmd1 > cmd2 > cmd3`

---

#### Question 27
Comment **créer un mot de passe aléatoire** de 16 caractères depuis la ligne de commande ?

- [ ] A) `tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 16`  
- [ ] B) `openssl rand -base64 16`  
- [ ] C) `cat /dev/random | head -c 16`  
- [ ] D) Les deux A et B

---

#### Question 28
Que fait la commande `xargs` ?

- [ ] A) Compresse des fichiers  
- [ ] B) Construit et exécute commandes depuis stdin  
- [ ] C) Cherche fichiers par nom  
- [ ] D) Trie des lignes

---

#### Question 29
Quelle commande affiche **tous les processus** de tous les utilisateurs en format détaillé ?

- [ ] A) `ps`  
- [ ] B) `ps aux`  
- [ ] C) `ps -ef`  
- [ ] D) Les deux B et C

---

#### Question 30
Comment **tuer proprement** un processus (lui laisser le temps de nettoyer) ?

- [ ] A) `kill -9 PID`  
- [ ] B) `kill PID` ou `kill -15 PID`  
- [ ] C) `killall -9 processname`  
- [ ] D) `pkill -KILL processname`

---

#### Question 31
Comment **lister les processus en arrière-plan** (jobs) du shell actuel ?

- [ ] A) `ps`  
- [ ] B) `jobs`  
- [ ] C) `bg`  
- [ ] D) `top`

---

#### Question 32
Quelle commande affiche les processus en **temps réel** avec rafraîchissement automatique ?

- [ ] A) `ps aux`  
- [ ] B) `top`  
- [ ] C) `htop`  
- [ ] D) Les deux B et C

---

#### Question 33
Comment **détacher un processus** du terminal pour qu'il continue après déconnexion ?

- [ ] A) `command &`  
- [ ] B) `nohup command &`  
- [ ] C) `disown`  
- [ ] D) Les deux B et C

---

#### Question 34
Quelle colonne de `ps aux` indique l'**état** du processus (running, sleeping, zombie, etc.) ?

- [ ] A) %CPU  
- [ ] B) STAT  
- [ ] C) TTY  
- [ ] D) TIME

---

#### Question 35
Comment **envoyer le signal SIGHUP** à un processus (souvent pour reload config) ?

- [ ] A) `kill -1 PID`  
- [ ] B) `kill -HUP PID`  
- [ ] C) `pkill -HUP processname`  
- [ ] D) Toutes les réponses

---

#### Question 36
Comment surveiller l'**utilisation mémoire** en temps réel ?

- [ ] A) `free -h`  
- [ ] B) `top`  
- [ ] C) `vmstat 2`  
- [ ] D) Les deux B et C (temps réel)

---

#### Question 37
Quelle est la **plage de valeurs nice** pour les processus ?

- [ ] A) 0 à 19  
- [ ] B) -20 à +19  
- [ ] C) -10 à +10  
- [ ] D) 1 à 100

---

#### Question 38
Comment **modifier la priorité** d'un processus **déjà en cours** ?

- [ ] A) `nice -n 5 PID`  
- [ ] B) `renice -n 5 PID`  
- [ ] C) `renice -n 5 -p PID`  
- [ ] D) Les deux B et C

---

#### Question 39
Comment **lancer un processus** avec la priorité **la plus basse** possible (utilisateur normal) ?

- [ ] A) `nice command`  
- [ ] B) `nice -n 10 command`  
- [ ] C) `nice -n 19 command`  
- [ ] D) `nice -n 20 command`

---

#### Question 40
Un utilisateur **normal** peut-il utiliser `renice` pour **augmenter la priorité** (diminuer nice) de son processus ?

- [ ] A) Oui, toujours  
- [ ] B) Oui, mais seulement jusqu'à nice 0  
- [ ] C) Non, jamais (seulement diminuer priorité = augmenter nice)  

---

#### Question 41
Comment chercher un mot en **ignorant la casse** (majuscules/minuscules) avec grep ?

- [ ] A) `grep word file.txt`  
- [ ] B) `grep -i word file.txt`  
- [ ] C) `grep -v word file.txt`  
- [ ] D) `grep -c word file.txt`

---

#### Question 42
Quelle regex grep trouve les lignes commençant par "Error" ?

- [ ] A) `grep "Error" file`  
- [ ] B) `grep "^Error" file`  
- [ ] C) `grep "$Error" file`  
- [ ] D) `grep "Error$" file`

---

#### Question 43
Comment chercher des lignes contenant "error" **OU** "warning" avec grep ?

- [ ] A) `grep "error warning" file`  
- [ ] B) `grep -E "error|warning" file`  
- [ ] C) `egrep "error|warning" file`  
- [ ] D) Les deux B et C

---

#### Question 44
Quelle commande utilise `sed` pour **remplacer** "old" par "new" dans un fichier ?

- [ ] A) `sed 's/old/new/' file`  
- [ ] B) `sed 's/old/new/g' file`  
- [ ] C) `sed -i 's/old/new/g' file`  
- [ ] D) Les trois (avec nuances)

---

#### Question 45
Quelle regex trouve les **adresses IPv4** (format 192.168.1.1) ?

- [ ] A) `grep "[0-9]\.[0-9]\.[0-9]\.[0-9]" file`  
- [ ] B) `grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" file`  
- [ ] C) `grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" file`  
- [ ] D) Les deux B et C (C plus précis)

---

#### Question 46
Quelle regex grep trouve les **mots entiers** "test" (pas "testing", "attest", etc.) ?

- [ ] A) `grep "test" file`  
- [ ] B) `grep "\btest\b" file`  
- [ ] C) `grep -w "test" file`  
- [ ] D) Les deux B et C

---

#### Question 47
Comment **compter le nombre de lignes** contenant "error" dans un fichier ?

- [ ] A) `grep "error" file | wc -l`  
- [ ] B) `grep -c "error" file`  
- [ ] C) `wc -l error file`  
- [ ] D) Les deux A et B

---

#### Question 48
Quelle option grep affiche les lignes **NE contenant PAS** le pattern ?

- [ ] A) `grep -n pattern file`  
- [ ] B) `grep -v pattern file`  
- [ ] C) `grep -c pattern file`  
- [ ] D) `grep -i pattern file`

---

#### Question 49
Dans vi, quelle commande **sauvegarde et quitte** ?

- [ ] A) `:q`  
- [ ] B) `:w`  
- [ ] C) `:wq` ou `:x` ou `ZZ`  
- [ ] D) `:q!`

---

#### Question 50
Dans vi, comment **passer en mode Insert** pour commencer à taper du texte ?

- [ ] A) `a` ou `i` ou `o`  
- [ ] B) `Esc`  
- [ ] C) `:i`  
- [ ] D) `Ctrl+I`

---


---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

### Question 1
**Réponse correcte : B**

**Explication détaillée :**

`env` (ou `printenv`) affiche toutes les variables d'environnement :
```bash
env
# HOME=/home/user
# PATH=/usr/local/bin:/usr/bin:/bin
# USER=john
# SHELL=/bin/bash
# etc.
```

**Pourquoi les autres sont incorrectes :**

- **A) `set`** : Affiche TOUTES les variables (environnement + shell locales) et fonctions. Plus verbeux que `env`.
- **C) `export`** : Utilisé pour DÉFINIR ou afficher variables exportées. `export VAR=value` exporte, `export -p` liste (verbeux).
- **D) `echo $VAR`** : Affiche UNE variable spécifique, pas toutes.

**Équivalences :**
```bash
env           # Toutes env vars
printenv      # Identique à env
export -p     # Liste exportées (format export VAR=value)
set           # Tout (env + locales + fonctions)
```

**En pratique :**
```bash
# Liste propre
env | sort

# Variable spécifique
printenv HOME
echo $HOME

# Différence
VAR=local     # Locale (pas exportée)
set | grep VAR=local      # Visible
env | grep VAR=local      # Pas visible

export VAR=exported
env | grep VAR=exported   # Maintenant visible
```

---

### Question 2
**Réponse correcte : B**

**Explication détaillée :**

Pour rendre un changement de PATH **permanent**, il faut l'ajouter au fichier de configuration du shell (`~/.bashrc` pour Bash) :

```bash
echo 'export PATH=$PATH:/opt/myapp/bin' >> ~/.bashrc
source ~/.bashrc    # Recharger ou relancer shell
```

Le `>>` **ajoute** à la fin du fichier (append) sans écraser.

**Pourquoi les autres sont incorrectes :**

- **A) `export PATH=/opt/myapp/bin`** : **ÉCRASE** tout le PATH ! Plus de `/usr/bin`, `/bin`, etc. = système cassé. Et seulement **temporaire** (session courante).
- **C) `PATH=$PATH:/opt/myapp/bin`** : Correct pour **temporaire** (session courante), mais PAS permanent (perdu au logout).
- **D) `set PATH=/opt/myapp/bin`** : Syntaxe invalide. `set` ne fonctionne pas comme ça.

**Bonne pratique :**
```bash
# Ajouter à la fin (priorité normale)
export PATH=$PATH:/opt/myapp/bin

# Ajouter au début (priorité haute)
export PATH=/opt/myapp/bin:$PATH

# Vérifier
echo $PATH
which mycommand
```

**Fichiers de configuration Bash :**
- `~/.bashrc` : Login interactif non-login (terminal)
- `~/.profile` ou `~/.bash_profile` : Login shell
- `/etc/environment` : Système-wide (format `VAR=value`)
- `/etc/profile` : Système-wide (login shells)

**Test :**
```bash
# Ajouter
echo 'export PATH=$PATH:/opt/bin' >> ~/.bashrc

# Vérifier (nouvelle session)
exit
# Nouvelle connexion
echo $PATH | grep /opt/bin    # Doit apparaître
```

---

### Question 3
**Réponse correcte : B**

**Explication détaillée :**

`$?` contient l'**exit code** de la dernière commande :
- **0** = Succès
- **Non-zéro** = Erreur (1-255)

```bash
ls /tmp
echo $?     # 0 (succès)

ls /nonexistent
echo $?     # 2 (erreur)

grep "pattern" file.txt
echo $?     # 0 si trouvé, 1 si pas trouvé, 2 si erreur

# Utilisation dans scripts
if command; then
    echo "Success"
fi

# Ou
command
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Failed with code $?"
fi
```

**Pourquoi les autres sont incorrectes :**

- **A) `$!`** : PID du **dernier processus background**
  ```bash
  sleep 100 &
  echo $!    # PID du sleep (ex: 12345)
  kill $!    # Kill le processus background
  ```

- **C) `$$`** : PID du **shell actuel**
  ```bash
  echo $$    # PID du bash courant (ex: 1234)
  ps -p $$   # Infos sur shell actuel
  ```

- **D) `$_`** : **Dernier argument** de la commande précédente
  ```bash
  ls /var/log
  cd $_      # cd /var/log
  ```

**Codes retour courants :**
- **0** : Succès
- **1** : Erreur générale
- **2** : Usage incorrect commande
- **126** : Commande non exécutable
- **127** : Commande introuvable
- **128+N** : Signal N (ex: 130 = Ctrl+C)

**En pratique :**
```bash
# Vérifier succès
make && make install

# Vérifier échec
command || echo "Failed"

# Combinaison
command && echo "OK" || echo "Failed"

# Log avec code
./script.sh
echo "Exit code: $?"
```

---

### Question 4
**Réponse correcte : B**

**Explication détaillée :**

Pour rendre un alias **permanent**, il faut :
1. L'ajouter à `~/.bashrc`
2. Recharger le fichier avec `source` (ou redémarrer shell)

```bash
echo "alias ll='ls -lah'" >> ~/.bashrc
source ~/.bashrc    # Ou: . ~/.bashrc

# Vérifier
alias ll
# alias ll='ls -lah'

ll    # Exécute ls -lah
```

**Pourquoi les autres sont incorrectes :**

- **A) `alias ll='ls -lah'`** : Crée alias **temporaire** (session courante uniquement). Perdu au logout/redémarrage shell.

- **C) `ln -s ls ll`** : Tente de créer un **lien symbolique** (pas un alias). Incorrect conceptuellement et syntaxe invalide.

- **D) `export ll='ls -lah'`** : Crée une **variable d'environnement** (pas un alias). `ll` contiendra le string "ls -lah" mais ne s'exécutera pas.

**Gestion alias :**
```bash
# Créer temporaire
alias gs='git status'
alias ..='cd ..'

# Lister tous les alias
alias

# Supprimer alias
unalias ll

# Utiliser commande originale (bypass alias)
\ls         # Exécute ls sans alias
command ls  # Idem
```

**Alias utiles courants :**
```bash
# Dans ~/.bashrc
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias grep='grep --color=auto'
alias df='df -h'
alias free='free -h'
alias mkdir='mkdir -pv'
alias ..='cd ..'
alias ...='cd ../..'
alias update='sudo apt update && sudo apt upgrade'
alias ports='netstat -tulanp'
```

**Différence alias vs fonction :**
```bash
# Alias (simple)
alias ll='ls -lah'

# Fonction (avec paramètres)
mkcd() {
    mkdir -p "$1" && cd "$1"
}
mkcd project/src    # Crée et va dans project/src
```

---

### Question 5
**Réponse correcte : B**

**Explication détaillée :**

**Ctrl+R** lance la **recherche inversée interactive** dans l'historique :

```bash
# Appuyer sur Ctrl+R
(reverse-i-search)`': 

# Taper 'ssh'
(reverse-i-search)`ssh': ssh user@server.com

# Appuyer Enter pour exécuter
# Ou Ctrl+R à nouveau pour occurence précédente
# Ou Esc pour éditer sans exécuter
```

C'est la méthode **la plus efficace** pour retrouver rapidement une commande.

**Pourquoi les autres sont incorrectes :**

- **A) `history | grep pattern`** : Fonctionne pour chercher, mais **pas interactif**. Affiche liste, nécessite ensuite `!N` pour exécuter.
  ```bash
  history | grep ssh
  # 42  ssh user@server1.com
  # 87  ssh root@server2.com
  !42    # Exécuter commande #42
  ```

- **C) `!!`** : Répète **dernière commande** (pas une recherche).
  ```bash
  ls -l
  !!       # Exécute: ls -l
  sudo !!  # Exécute: sudo ls -l
  ```

- **D) `!ssh`** : Exécute **dernière commande commençant par** "ssh" (pas interactif, exécution directe).
  ```bash
  !ssh    # Exécute dernière commande ssh*
  # Attention: exécution IMMÉDIATE sans confirmation !
  ```

**Raccourcis historique Bash :**
```bash
# Navigation
Ctrl+R      # Recherche inversée (interactive)
Ctrl+S      # Recherche avant (nécessite: stty -ixon)
Ctrl+P      # Commande précédente (= flèche haut)
Ctrl+N      # Commande suivante (= flèche bas)

# Expansion
!!          # Dernière commande
!N          # Commande numéro N
!-2         # Avant-dernière commande
!ssh        # Dernière commande commençant par 'ssh'
!?pattern   # Dernière commande contenant 'pattern'

# Arguments
!$          # Dernier argument précédente commande
!^          # Premier argument précédente commande
!*          # Tous arguments précédente commande
!:2         # 2ème argument

# Modification
^old^new    # Remplace 'old' par 'new' dans dernière commande
```

**Exemples pratiques :**
```bash
# Recherche interactive
Ctrl+R puis 'docker run'    # Trouve commande docker

# Réutiliser argument
cd /var/log/apache2
ls !$    # ls /var/log/apache2

# Répéter avec sudo
apt update    # Erreur: permission denied
sudo !!       # sudo apt update

# Chercher et exécuter
history | grep scp
!123    # Exécute commande #123
```

**Configuration historique (~/.bashrc) :**
```bash
HISTSIZE=10000              # Taille en mémoire
HISTFILESIZE=20000          # Taille sur disque
HISTCONTROL=ignoredups      # Ignorer doublons
HISTTIMEFORMAT="%F %T "     # Timestamp
```

---

### Question 6
**Réponse correcte : B**

**Explication détaillée :**

`which` cherche une commande dans le **$PATH** et affiche le **premier** exécutable trouvé (celui qui sera exécuté) :

```bash
which python3
# /usr/bin/python3

which ls
# /usr/bin/ls

which nonexistent
# (rien ou erreur)

# Plusieurs emplacements
which -a python3
# /usr/bin/python3
# /usr/local/bin/python3
```

**Pourquoi les autres sont incorrectes :**

- **A) `whereis`** : Cherche **binaires, sources ET man pages** (pas seulement PATH). Plus large que `which`.
  ```bash
  whereis python3
  # python3: /usr/bin/python3 /usr/lib/python3 /usr/share/man/man1/python3.1.gz
  #          └─ binaire      └─ librairies  └─ man page
  ```

- **C) `find`** : Cherche fichiers dans **arborescence** (pas spécifique au PATH). Lent et verbeux.
  ```bash
  find /usr -name python3 2>/dev/null
  # Cherche partout dans /usr, pas seulement PATH
  ```

- **D) `locate`** : Cherche via **base de données** indexée (updatedb). Rapide mais pas spécifique au PATH.
  ```bash
  locate python3
  # Des centaines de résultats (scripts, librairies, docs, etc.)
  ```

**Comparaison des commandes :**

| Commande | Fonction | Rapidité | Spécifique PATH |
|----------|----------|----------|----------------|
| `which` | Exécutable dans PATH | Rapide | ✅ Oui |
| `whereis` | Binaire + source + man | Rapide | ❌ Non (plus large) |
| `type` | Type commande (builtin/alias/file) | Rapide | ✅ Oui |
| `find` | Recherche arborescence | Lent | ❌ Non |
| `locate` | Recherche index | Très rapide | ❌ Non |

**Commande `type` (alternative) :**
```bash
type ls
# ls is aliased to `ls --color=auto'

type cd
# cd is a shell builtin

type python3
# python3 is /usr/bin/python3

type -a ls
# ls is aliased to `ls --color=auto'
# ls is /usr/bin/ls

type -t python3
# file (type: file/alias/builtin)
```

**Usage pratique :**
```bash
# Vérifier si commande existe
if which docker &>/dev/null; then
    echo "Docker installed"
fi

# Chemin exact pour script
PYTHON=$(which python3)
$PYTHON script.py

# Comparer versions
which -a python
# /usr/local/bin/python
# /usr/bin/python

# Vérifier priorité PATH
which gcc
# /usr/bin/gcc (si /usr/bin avant /usr/local/bin dans PATH)
```

---

### Question 7
**Réponse correcte : B**

**Explication détaillée :**

L'opérateur `&&` (ET logique) exécute la commande suivante **SEULEMENT si la précédente réussit** (exit code 0) :

```bash
cd /tmp && ls -l
# Si cd réussit (code 0), alors ls s'exécute
# Si cd échoue, ls NE s'exécute PAS

make && make install
# Compile, puis installe SEULEMENT si compilation OK

mkdir project && cd project && touch README.md
# Crée, entre, puis crée fichier (chaîne conditionnelle)
```

**Pourquoi les autres sont incorrectes :**

- **A) `command1 ; command2`** : Exécute **TOUJOURS les deux** séquentiellement, **peu importe** le résultat de la première.
  ```bash
  cd /nonexistent ; ls -l
  # Erreur cd, mais ls s'exécute quand même (dans répertoire actuel)
  ```

- **C) `command1 || command2`** : OU logique - exécute la deuxième **SEULEMENT si la première ÉCHOUE**.
  ```bash
  cd /tmp || echo "Failed"
  # Affiche "Failed" seulement si cd échoue
  
  command || exit 1    # Quitter si échec
  ```

- **D) `command1 | command2`** : **Pipe** - la sortie de command1 devient l'entrée de command2. Les deux s'exécutent **en parallèle**.
  ```bash
  ls | grep txt
  # ls s'exécute, sortie envoyée à grep
  ```

**Tableau récapitulatif :**

| Opérateur | Signification | Exécution command2 |
|-----------|---------------|-------------------|
| `;` | Séquentiel | Toujours |
| `&&` | ET logique | Si command1 réussit (code 0) |
| `\|\|` | OU logique | Si command1 échoue (code ≠ 0) |
| `\|` | Pipe | Parallèle (avec stdin/stdout) |

**Patterns courants :**
```bash
# Installation avec vérification
apt update && apt upgrade

# Backup avec vérification
tar czf backup.tar.gz /data && echo "Backup OK"

# Compilation + installation
./configure && make && sudo make install

# Chaîne conditionnelle
cd project && git pull && npm install && npm start

# Combinaison && et ||
command && echo "Success" || echo "Failed"
# Si command OK → "Success"
# Si command échoue → "Failed"

# Fallback
cd /preferred/path || cd /fallback/path

# Exit si échec
critical_command || exit 1
```

**Groupement de commandes :**
```bash
# Grouper dans sous-shell
(cd /tmp && ls -l)    # cd temporaire
pwd                   # Toujours dans répertoire original

# Grouper dans shell actuel
{ cd /tmp && ls -l; } # cd persistent
pwd                   # Maintenant dans /tmp
```

---

### Question 8
**Réponse correcte : B**

**Explication détaillée :**

`$#` contient le **nombre d'arguments** passés au script (ou fonction) :

```bash
#!/bin/bash
echo "Nombre d'arguments: $#"
echo "Arguments: $@"

# Exécution
./script.sh arg1 arg2 arg3
# Nombre d'arguments: 3
# Arguments: arg1 arg2 arg3

# Validation
if [ $# -lt 2 ]; then
    echo "Usage: $0 <arg1> <arg2>"
    exit 1
fi
```

**Pourquoi les autres sont incorrectes :**

- **A) `$@`** : **Tableau de tous les arguments** (pas le compte). Préserve séparation.
  ```bash
  #!/bin/bash
  for arg in "$@"; do
      echo "Arg: $arg"
  done
  
  # ./script.sh "arg 1" arg2
  # Arg: arg 1
  # Arg: arg2
  ```

- **C) `$*`** : Tous les arguments en **une seule chaîne** (jointure).
  ```bash
  #!/bin/bash
  echo "$*"    # Tous en un string
  echo "$@"    # Array préservé
  
  # ./script.sh arg1 arg2
  # $* = "arg1 arg2" (une chaîne)
  # $@ = ("arg1" "arg2") (array)
  ```

- **D) `$0`** : **Nom du script** (pas les arguments).
  ```bash
  #!/bin/bash
  echo "Script: $0"
  
  # ./test.sh
  # Script: ./test.sh
  ```

**Variables positionnelles complètes :**
```bash
$0     # Nom du script
$1-$9  # Arguments 1 à 9
${10}  # Argument 10+ (accolades requises)
$#     # Nombre d'arguments
$@     # Tous arguments (array)
$*     # Tous arguments (string)
$$     # PID du script
$!     # PID dernier processus background
$?     # Exit code dernière commande
$_     # Dernier argument commande précédente
```

**Exemples pratiques :**
```bash
#!/bin/bash
# backup.sh

# Vérifier nombre args
if [ $# -ne 1 ]; then
    echo "Usage: $0 <directory>"
    exit 1
fi

# Utiliser arg
DIR=$1
tar czf backup_$(date +%Y%m%d).tar.gz "$DIR"
```

```bash
#!/bin/bash
# process_files.sh

# Vérifier minimum 2 args
if [ $# -lt 2 ]; then
    echo "Usage: $0 <command> <file1> [file2...]"
    exit 1
fi

COMMAND=$1
shift    # Décaler arguments ($2 devient $1)

# Traiter fichiers
for file in "$@"; do
    $COMMAND "$file"
done
```

**Différence `$@` vs `$*` :**
```bash
#!/bin/bash
function show_args() {
    echo "Count: $#"
    for arg in "$@"; do
        echo "  - $arg"
    done
}

# Appel
show_args "arg 1" arg2 arg3
# Count: 3
#   - arg 1
#   - arg2
#   - arg3

# Avec $* (incorrect si espaces)
for arg in "$*"; do
    echo "- $arg"
done
# - arg 1 arg2 arg3  (tout en un!)
```

**Shift et manipulation :**
```bash
#!/bin/bash
echo "Premier: $1"
shift
echo "Maintenant premier: $1"

# ./script.sh a b c
# Premier: a
# Maintenant premier: b

# Consommer tous les args
while [ $# -gt 0 ]; do
    echo "Processing: $1"
    shift
done
```

---

### Question 9
**Réponse correcte : D (A et B fonctionnent)**

**Explication détaillée :**

Deux méthodes pour afficher les 10 dernières commandes :

**Méthode A - `history 10` :**
```bash
history 10
# 491  cd /var/log
# 492  tail -f syslog
# 493  grep ERROR syslog
# 494  ps aux
# 495  top
# 496  systemctl status nginx
# 497  ls -la
# 498  pwd
# 499  clear
# 500  history 10
```

**Méthode B - `history | tail -10` :**
```bash
history | tail -10
# (même résultat que ci-dessus)
```

**Les deux sont valides !** `history 10` est plus direct, `history | tail -10` utilise pipeline.

**Pourquoi C est incorrecte :**

- **C) `!-10`** : **EXÉCUTE** la commande qui était 10 commandes avant (pas un affichage).
  ```bash
  !-10    # Exécute commande #490 (si on est à #500)
  # Attention: exécution IMMÉDIATE !
  ```

**Commandes historique utiles :**
```bash
# Afficher tout
history

# Dernières N
history 20
history | tail -20

# Chercher
history | grep ssh

# Numéros de ligne
history -w    # Sauvegarder historique
history -c    # Effacer historique (mémoire)
history -d 42 # Supprimer entrée #42

# Exécuter commande N
!42
!-5       # 5 commandes avant

# Dernière commande
!!

# Dernière commande commençant par...
!ssh

# Éditer et exécuter
fc        # Ouvre dernière commande dans $EDITOR
fc 42     # Édite commande #42
```

**Configuration historique (~/.bashrc) :**
```bash
# Taille
HISTSIZE=10000           # En mémoire
HISTFILESIZE=20000       # Sur disque (~/.bash_history)

# Contrôle
HISTCONTROL=ignoredups:ignorespace
# ignoredups  : Pas de doublons consécutifs
# ignorespace : Ignore commandes commençant par espace
# ignoreboth  : Les deux

# Timestamp
HISTTIMEFORMAT="%F %T "  # Format: 2026-01-28 15:30:00

# Ignorer commandes
HISTIGNORE="ls:ll:cd:pwd:exit:clear"

# Append (pas overwrite)
shopt -s histappend
```

**Exemples pratiques :**
```bash
# Analyse historique
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
# Top 10 commandes utilisées

# Exporter historique
history > my_commands.txt

# Timestamp (si HISTTIMEFORMAT configuré)
history | tail -10
# 491  2026-01-28 15:30:45 cd /var/log
# 492  2026-01-28 15:31:02 tail -f syslog

# Supprimer dernière entrée (erreur)
history -d $(history 1 | awk '{print $1}')
```

**Sécurité :**
```bash
# Ne pas enregistrer commande (espace devant)
 mysql -u root -p    # Pas dans historique (si ignorespace)

# Effacer commande sensible
history | grep password
history -d 123    # Supprimer entrée avec password

# Désactiver historique temporairement
set +o history    # Désactiver
# commandes sensibles
set -o history    # Réactiver
```

---

### Question 10
**Réponse correcte : B**

**Explication détaillée :**

`~/.bash_history` est le fichier qui contient l'historique des commandes Bash :

```bash
# Afficher historique (fichier)
cat ~/.bash_history

# Dernières lignes
tail -20 ~/.bash_history

# Chercher dans historique
grep ssh ~/.bash_history

# Taille du fichier
wc -l ~/.bash_history
```

**Fonctionnement :**
- **En mémoire** pendant session (variable HISTSIZE)
- **Sauvegardé** dans `~/.bash_history` au logout (HISTFILESIZE)
- **Chargé** au login depuis `~/.bash_history`

**Pourquoi les autres sont incorrectes :**

- **A) `~/.bash_profile`** : Fichier de **configuration** (scripts exécutés au login), pas d'historique.
  ```bash
  cat ~/.bash_profile
  # export PATH=$PATH:/opt/bin
  # source ~/.bashrc
  ```

- **C) `~/.bashrc`** : Fichier de **configuration** (alias, fonctions, prompts), pas d'historique.
  ```bash
  cat ~/.bashrc
  # alias ll='ls -lah'
  # export PS1='[\u@\h \W]\$ '
  ```

- **D) `/var/log/bash.log`** : N'existe **pas par défaut**. `/var/log/` contient logs système, pas historique shell utilisateur.

**Configuration historique :**
```bash
# Dans ~/.bashrc
HISTFILE=~/.bash_history      # Fichier (défaut)
HISTSIZE=10000                # Lignes en mémoire
HISTFILESIZE=20000            # Lignes sur disque
HISTCONTROL=ignoredups        # Contrôle
HISTTIMEFORMAT="%F %T "       # Timestamp

# Fichier personnalisé
HISTFILE=~/.my_history
```

**Gestion du fichier :**
```bash
# Sauvegarder manuellement
history -w

# Recharger
history -r

# Effacer (mémoire)
history -c

# Effacer (fichier)
> ~/.bash_history
# ou
rm ~/.bash_history

# Backup
cp ~/.bash_history ~/.bash_history.backup

# Merge historiques (multi-sessions)
shopt -s histappend    # Append au lieu de overwrite
```

**Sécurité et privacy :**
```bash
# Désactiver historique pour session
unset HISTFILE

# Historique dans /dev/null (pas de sauvegarde)
HISTFILE=/dev/null

# Effacer historique sensible
history -c
rm ~/.bash_history

# Lien symbolique vers /dev/null (permanent)
ln -sf /dev/null ~/.bash_history

# Permissions restrictives
chmod 600 ~/.bash_history
```

**Autres shells :**
```bash
# Zsh
~/.zsh_history

# Fish
~/.local/share/fish/fish_history

# Tcsh
~/.history
```

**Analyse historique :**
```bash
# Commandes les plus utilisées
cat ~/.bash_history | sort | uniq -c | sort -rn | head -20

# Recherche pattern
grep -i docker ~/.bash_history

# Compter commandes uniques
cat ~/.bash_history | sort -u | wc -l
```

---

### Question 11
**Réponse correcte : A**

**Explication détaillée :**

`head -15 file.txt` (ou `head -n 15 file.txt`) affiche les **15 premières lignes** :

```bash
head -15 file.txt
head -n 15 file.txt    # Équivalent

# Défaut: 10 lignes
head file.txt

# Premiers 100 bytes
head -c 100 file.txt

# Multiple fichiers
head -n 5 file1.txt file2.txt
```

**Pourquoi les autres sont incorrectes :**

- **B) `tail -15 file.txt`** : Affiche les **15 DERNIÈRES** lignes (pas les premières).
  ```bash
  tail -15 file.txt        # 15 dernières
  tail -n 15 file.txt      # Équivalent
  tail -f file.txt         # Suivre en temps réel
  ```

- **C) `cat -n 15 file.txt`** : `-n` numérote **toutes les lignes** (pas limite à 15). Syntaxe invalide pour limiter.
  ```bash
  cat -n file.txt          # Numérote toutes les lignes
  # 1  ligne 1
  # 2  ligne 2
  # ...
  ```

- **D) `less +15 file.txt`** : Ouvre `less` **à partir de la ligne 15** (pas affichage des 15 premières).
  ```bash
  less +15 file.txt        # Ouvre à ligne 15 (interactive)
  less +G file.txt         # Ouvre à la fin
  ```

**Combinaisons head et tail :**
```bash
# Lignes 11 à 20
head -20 file.txt | tail -10

# Ligne exacte (ex: ligne 15)
head -15 file.txt | tail -1
sed -n '15p' file.txt        # Plus direct

# Plage
sed -n '10,20p' file.txt
awk 'NR>=10 && NR<=20' file.txt
```

**Exemples pratiques :**
```bash
# Aperçu fichier CSV
head -5 data.csv

# Première ligne (header)
head -1 data.csv

# Log récents
tail -50 /var/log/syslog

# Suivre log en temps réel
tail -f /var/log/apache2/access.log

# Premières lignes de tous les .txt
head -n 3 *.txt

# Depuis ligne N jusqu'à la fin
tail -n +10 file.txt    # Depuis ligne 10
```

**Options head/tail :**
```bash
# head
-n N    # N lignes
-c N    # N bytes
-q      # Quiet (pas de header si multiples fichiers)
-v      # Verbose (avec header même un fichier)

# tail
-n N    # N lignes
-n +N   # Depuis ligne N
-c N    # N bytes
-f      # Follow (temps réel)
-F      # Follow avec retry (si fichier recréé)
-s N    # Sleep N secondes entre lectures (avec -f)
```

---

### Question 12
**Réponse correcte : A**

**Explication détaillée :**

`wc -l file.txt` compte le nombre de **lignes** (line count) :

```bash
wc -l file.txt
# 250 file.txt

# Sans nom fichier (via pipe)
cat file.txt | wc -l
# 250

# Multiple fichiers
wc -l file1.txt file2.txt
# 100 file1.txt
# 150 file2.txt
# 250 total
```

**Pourquoi les autres sont incorrectes :**

- **B) `wc -w file.txt`** : Compte les **mots** (words), pas les lignes.
  ```bash
  wc -w file.txt
  # 1234 file.txt  (1234 mots)
  ```

- **C) `cat file.txt | count`** : Commande `count` **n'existe pas** en Linux standard.

- **D) `lines file.txt`** : Commande `lines` **n'existe pas** en Linux standard.

**Options wc :**
```bash
wc file.txt
# 10  50  300 file.txt
# │   │   │
# │   │   └─ bytes
# │   └───── mots
# └───────── lignes

# Options
-l    # Lignes
-w    # Mots
-c    # Bytes
-m    # Caractères (UTF-8)
-L    # Longueur ligne la plus longue

# Exemples
wc -l file.txt          # 10
wc -w file.txt          # 50
wc -c file.txt          # 300
wc -m unicode.txt       # 280 (si caractères multi-bytes)
wc -L file.txt          # 85 (ligne plus longue)
```

**Exemples pratiques :**
```bash
# Compter fichiers dans répertoire
ls -1 | wc -l
find . -type f | wc -l

# Compter utilisateurs connectés
who | wc -l

# Compter lignes non vides
grep -v '^$' file.txt | wc -l

# Compter lignes de code Python
find . -name "*.py" | xargs wc -l

# Total lignes projet
wc -l **/*.{py,js,html}

# Lignes avec pattern
grep "ERROR" /var/log/syslog | wc -l

# Comparer tailles fichiers
wc -l *.log | sort -n
```

**Différence bytes vs caractères :**
```bash
# Fichier ASCII
echo "hello" > ascii.txt
wc -c ascii.txt    # 6 bytes (h e l l o \n)
wc -m ascii.txt    # 6 caractères

# Fichier UTF-8 (caractères multi-bytes)
echo "héllo" > utf8.txt
wc -c utf8.txt     # 7 bytes (é = 2 bytes)
wc -m utf8.txt     # 6 caractères

# Émojis
echo "Hello 👋" > emoji.txt
wc -c emoji.txt    # 11 bytes
wc -m emoji.txt    # 8 caractères
```

**Compter avec conditions :**
```bash
# Lignes commençant par #
grep -c '^#' file.txt

# Lignes contenant pattern
grep -c "ERROR" log.txt

# Lignes NE contenant PAS
grep -vc "DEBUG" log.txt

# Avec awk
awk 'END {print NR}' file.txt        # Total lignes
awk '/ERROR/ {count++} END {print count}' log.txt
```

---

### Question 13
**Réponse correcte : D (A et B fonctionnent)**

**Explication détaillée :**

**Méthode A - `cut` :**
```bash
cut -d ',' -f 1,3 file.csv
# -d ','  : Délimiteur virgule
# -f 1,3  : Champs (fields) 1 et 3

# Exemple fichier:
# John,Doe,30,Engineer
# Jane,Smith,25,Designer

# Résultat:
# John,30
# Jane,25
```

**Méthode B - `awk` :**
```bash
awk -F',' '{print $1,$3}' file.csv
# -F','  : Délimiteur virgule
# $1,$3  : Colonnes 1 et 3

# Résultat (avec espace comme séparateur de sortie):
# John 30
# Jane 25

# Avec virgule en sortie
awk -F',' '{print $1","$3}' file.csv
# John,30
# Jane,25

# Ou avec OFS (Output Field Separator)
awk -F',' -v OFS=',' '{print $1,$3}' file.csv
```

**Les deux sont valides !** `cut` est plus simple pour colonnes fixes, `awk` plus flexible.

**Pourquoi C est incorrecte :**

- **C) `grep -E '^[^,]+,[^,]+' file.csv`** : **Filtre lignes** ayant au moins 2 champs, mais **n'extrait pas** colonnes spécifiques.

**Comparaison cut vs awk :**

| Aspect | cut | awk |
|--------|-----|-----|
| Simplicité | ✅ Simple | Plus complexe |
| Flexibilité | Limitée | ✅ Très flexible |
| Colonnes | Fixes | Variables, calculs |
| Traitement | Basique | ✅ Puissant |
| Vitesse | ✅ Rapide | Légèrement plus lent |

**Exemples cut :**
```bash
# Champs 1 et 3
cut -d ',' -f 1,3 file.csv

# Plage (1 à 3)
cut -d ',' -f 1-3 file.csv

# À partir de 2
cut -d ',' -f 2- file.csv

# Jusqu'à 4
cut -d ',' -f -4 file.csv

# Tous sauf 2
cut -d ',' -f 1,3- file.csv --complement

# Délimiteur tab (défaut)
cut -f 1,3 file.tsv

# Caractères (pas champs)
cut -c 1-10 file.txt        # Caractères 1 à 10

# Exemples pratiques
# Usernames depuis /etc/passwd
cut -d ':' -f 1 /etc/passwd

# UID et home
cut -d ':' -f 3,6 /etc/passwd

# Première colonne access log
cut -d ' ' -f 1 access.log | sort -u
```

**Exemples awk :**
```bash
# Colonnes 1 et 3
awk -F',' '{print $1,$3}' file.csv

# Avec header personnalisé
awk -F',' 'BEGIN {print "Name,Age"} {print $1","$3}' file.csv

# Calculs
awk -F',' '{sum+=$3} END {print sum}' numbers.csv

# Conditions
awk -F',' '$3 > 25 {print $1,$3}' file.csv

# Formattage
awk -F',' '{printf "%-10s %d\n", $1, $3}' file.csv

# Exemples pratiques
# Total colonne 3
awk -F',' '{sum+=$3} END {print sum}' data.csv

# Moyenne
awk -F',' '{sum+=$3; count++} END {print sum/count}' data.csv

# Filtrer et extraire
awk -F',' '$3 > 30 {print $1,$3}' file.csv

# NF (nombre de champs)
awk -F',' 'NF==4 {print $1,$3}' file.csv    # Seulement lignes avec 4 champs
```

**Gestion cas complexes :**
```bash
# CSV avec quotes
# "John,Jr",Doe,30

# awk avancé
awk -F',' '{gsub(/"/, "", $1); print $1,$3}' file.csv

# Espaces dans champs
# John Doe,30,Engineer

cut -d ',' -f 1,3    # OK
# John Doe,Engineer

# Multiple délimiteurs (awk)
awk -F'[,;:]' '{print $1,$3}' file.txt
```

---

### Question 14
**Réponse correcte : D (B et C pour délimiteur espace)**

**Explication détaillée :**

Pour tri **numérique** par colonne 3 :

**Méthode B (délimiteur espace/tab par défaut) :**
```bash
sort -k 3 -n file.txt
# -k 3  : Tri par colonne 3
# -n    : Tri numérique (pas alphabétique)

# Fichier exemple:
# Alice 25 1000
# Bob 30 500
# Charlie 28 2000

# Résultat (tri par colonne 3 numérique):
# Bob 30 500
# Alice 25 1000
# Charlie 28 2000
```

**Méthode C (délimiteur espace explicite) :**
```bash
sort -t ' ' -k 3 -n file.txt
# -t ' '  : Délimiteur espace
# Même résultat que B
```

**Pourquoi A est incorrecte :**

- **A) `sort -k 3 file.txt`** : Tri **alphabétique** (pas numérique). Problème avec nombres :
  ```bash
  # Sans -n (alphabétique)
  sort -k 3 file.txt
  # 1000
  # 2000
  # 500     ← Incorrect ! (5 > 2 alphabétiquement)
  
  # Avec -n (numérique)
  sort -k 3 -n file.txt
  # 500
  # 1000
  # 2000    ← Correct !
  ```

**Options sort avancées :**
```bash
# Tri numérique colonne 3
sort -k 3 -n file.txt
sort -k3n file.txt          # Forme compacte

# Tri inverse
sort -k 3 -nr file.txt

# Tri par plusieurs colonnes
sort -k 3 -n -k 1 file.txt  # Colonne 3 puis 1

# Délimiteur personnalisé
sort -t ':' -k 3 -n /etc/passwd    # Tri par UID

# Seulement colonne 3 (pas au-delà)
sort -k 3,3 -n file.txt

# Plage de colonnes
sort -k 2,4 -n file.txt     # Tri colonnes 2 à 4

# Tri humain (1K, 2M, 3G)
du -h | sort -h
du -h | sort -k 1 -h

# Tri par mois
sort -k 2 -M file.txt       # Jan, Feb, Mar...

# Tri par version
sort -V versions.txt        # 1.1, 1.2, 1.10, 2.0
```

**Exemples pratiques :**
```bash
# Top processus par CPU (colonne 3 de ps aux)
ps aux --sort=-%cpu | head -10
ps aux | sort -k 3 -nr | head -10

# Tri /etc/passwd par UID (colonne 3)
sort -t ':' -k 3 -n /etc/passwd

# Tri fichiers par taille (colonne 5 de ls -l)
ls -l | sort -k 5 -n

# Avec du
du -h /var/log/* | sort -h

# Tri CSV par prix (colonne 4)
sort -t ',' -k 4 -n products.csv

# Tri inverse (plus grand d'abord)
sort -t ',' -k 4 -nr products.csv

# Top 10 plus gros fichiers
du -h | sort -rh | head -10
```

**Tri multiple colonnes :**
```bash
# Tri par colonne 3 puis 1 (si égalité)
sort -k 3 -n -k 1 file.txt

# Tri colonne 2 inverse, puis colonne 3 normal
sort -k 2 -nr -k 3 -n file.txt

# Différents types par colonne
sort -k 1 -k 3n file.txt    # Col 1 alpha, col 3 numérique
```

**Supprimer doublons après tri :**
```bash
sort -u file.txt            # Tri + uniques
sort -k 3 -n -u file.txt    # Par col 3, uniques

# Avec uniq (nécessite tri avant)
sort file.txt | uniq
sort file.txt | uniq -c     # Avec compteur
```

**Cas particuliers :**
```bash
# Ignorer casse
sort -f file.txt
sort -k 2 -f file.txt

# Tri stable (préserve ordre original si égalité)
sort -s -k 3 file.txt

# Vérifier si trié
sort -c file.txt            # Erreur si pas trié
sort -C file.txt            # Idem sans message
```

---

### Question 15
**Réponse correcte : B**

**Explication détaillée :**

`sort file.txt | uniq -c` tri le fichier puis compte les occurrences :

```bash
# Fichier exemple
# apple
# banana
# apple
# cherry
# banana
# apple

sort file.txt | uniq -c
#   3 apple
#   2 banana
#   1 cherry

# Tri par occurrences (plus fréquent d'abord)
sort file.txt | uniq -c | sort -rn
#   3 apple
#   2 banana
#   1 cherry
```

**Pourquoi sort est NÉCESSAIRE avant uniq :**
`uniq` compare seulement lignes **consécutives**. Sans `sort`, doublons non-adjacents ne sont pas détectés :

```bash
# Sans sort (INCORRECT)
uniq -c file.txt
#   1 apple
#   1 banana
#   1 apple    ← Pas fusionné !
#   1 cherry
#   1 banana   ← Pas fusionné !
#   1 apple    ← Pas fusionné !

# Avec sort (CORRECT)
sort file.txt | uniq -c
#   3 apple
#   2 banana
#   1 cherry
```

**Pourquoi les autres sont incorrectes :**

- **A) `uniq file.txt`** : Supprime **seulement doublons consécutifs**, ne compte pas. Nécessite `sort` avant.
  ```bash
  uniq file.txt          # Juste suppression
  sort file.txt | uniq   # Suppression correcte
  ```

- **C) `count file.txt`** : Commande **n'existe pas** en Linux standard.

- **D) `grep -c file.txt`** : Syntaxe invalide. `grep -c` compte lignes **matchant un pattern** (nécessite pattern).
  ```bash
  grep -c "apple" file.txt    # Compte lignes avec "apple"
  # 3
  ```

**Options uniq :**
```bash
# Supprimer doublons consécutifs
uniq file.txt

# Compter occurrences
uniq -c file.txt

# Afficher seulement doublons
uniq -d file.txt

# Afficher seulement uniques
uniq -u file.txt

# Ignorer N premiers caractères
uniq -s 5 file.txt

# Ignorer N premiers champs
uniq -f 2 file.txt

# Ignorer casse
uniq -i file.txt
```

**Exemples pratiques :**
```bash
# Top 10 commandes historique
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10

# IPs uniques dans access log
cut -d ' ' -f 1 access.log | sort -u | wc -l

# Top 10 IPs avec compteur
cut -d ' ' -f 1 access.log | sort | uniq -c | sort -rn | head -10

# Mots les plus fréquents
tr -cs 'A-Za-z' '\n' < file.txt | tr '[:upper:]' '[:lower:]' | \
    sort | uniq -c | sort -rn | head -20

# Lignes dupliquées seulement
sort file.txt | uniq -d

# Lignes apparaissant exactement 1 fois
sort file.txt | uniq -u

# Compter lignes uniques
sort file.txt | uniq | wc -l
sort -u file.txt | wc -l    # Équivalent
```

**Différence `uniq` vs `sort -u` :**
```bash
# uniq (après sort)
sort file.txt | uniq        # Supprime doublons

# sort -u (tri + uniques en une commande)
sort -u file.txt            # Plus rapide

# Mais uniq offre plus d'options
sort file.txt | uniq -c     # Compter
sort file.txt | uniq -d     # Doublons seulement
```

**Avec awk (alternative) :**
```bash
# Compter occurrences (pas besoin de sort)
awk '{count[$0]++} END {for (word in count) print count[word], word}' file.txt | \
    sort -rn

# Plus simple pour compter
awk '{count[$0]++} END {for (word in count) print word, count[word]}' file.txt
```

---

### Question 16
**Réponse correcte : D (Toutes fonctionnent !)**

**Explication détaillée :**

Trois méthodes pour supprimer lignes vides :

**Méthode A - grep :**
```bash
grep -v '^$' file.txt
# -v   : Inverse match (lignes NE matchant PAS)
# ^$   : Regex ligne vide (^ = début, $ = fin)

# Fichier exemple:
# line 1
# 
# line 3
# 
# line 5

# Résultat:
# line 1
# line 3
# line 5
```

**Méthode B - sed :**
```bash
sed '/^$/d' file.txt
# /^$/  : Pattern ligne vide
# d     : Delete

# In-place (modifier fichier)
sed -i '/^$/d' file.txt

# Backup avant modification
sed -i.bak '/^$/d' file.txt
```

**Méthode C - awk :**
```bash
awk 'NF' file.txt
# NF  : Number of Fields (nombre de champs)
# Si NF > 0 (ligne non vide), imprime

# Ou explicite
awk 'NF > 0' file.txt
awk 'length > 0' file.txt    # Par longueur
```

**Toutes sont équivalentes !** Choix selon préférence/contexte.

**Lignes vides vs blanches :**
```bash
# Ligne vide : rien
# Ligne blanche : espaces/tabs seulement

# Supprimer lignes vides uniquement
grep -v '^$' file.txt

# Supprimer lignes vides ET blanches (espaces/tabs)
grep -v '^[[:space:]]*$' file.txt
sed '/^[[:space:]]*$/d' file.txt
awk 'NF' file.txt          # Supprime blanches aussi
awk '/\S/' file.txt        # Lignes avec au moins 1 non-blanc
```

**Exemples pratiques :**
```bash
# Config sans commentaires ni lignes vides
grep -Ev '^#|^$' /etc/ssh/sshd_config

# Nettoyer CSV
sed '/^$/d' data.csv > clean.csv

# Compter lignes non vides
grep -cv '^$' file.txt
awk 'NF' file.txt | wc -l

# Supprimer lignes vides multiples (garder 1)
cat -s file.txt             # Squeeze
sed '/^$/N;/^\n$/D' file.txt

# Avec awk (traitement avancé)
awk 'NF {print; next} !NF {if (!blank) print} {blank=!NF}' file.txt
```

**Modification in-place :**
```bash
# sed
sed -i '/^$/d' file.txt

# grep (via fichier temporaire)
grep -v '^$' file.txt > temp && mv temp file.txt

# awk
awk 'NF' file.txt > temp && mv temp file.txt

# Perl (in-place natif)
perl -i -ne 'print if /\S/' file.txt
```

**Variations complexes :**
```bash
# Supprimer lignes contenant seulement espaces
sed 's/^[[:space:]]*$//' file.txt | sed '/^$/d'
awk '{gsub(/^[[:space:]]+$/, "")}; NF' file.txt

# Réduire multiples lignes vides en une
cat -s file.txt
sed '/^$/N;/^\n$/D' file.txt

# Supprimer début et fin vides
sed -e '/./,$!d' -e :a -e '/^\n*$/{$d;N;ba' -e '}' file.txt
```

**Performances :**
```bash
# Sur gros fichiers, comparer:
time grep -v '^$' huge.txt > /dev/null
time sed '/^$/d' huge.txt > /dev/null
time awk 'NF' huge.txt > /dev/null

# Généralement:
# awk ≈ sed (légèrement plus rapide)
# grep : très rapide aussi
```

---

### Question 17
**Réponse correcte : D (B et C fonctionnent)**

**Explication détaillée :**

`-r` et `-R` sont **synonymes** pour copie récursive :

```bash
cp -r source/ dest/
cp -R source/ dest/    # Identique

# Copie répertoire complet avec contenu
# source/
#   file1.txt
#   subdir/
#     file2.txt

# → dest/
#     file1.txt
#     subdir/
#       file2.txt
```

**Pourquoi A est incorrecte :**

- **A) `cp dir1 dir2`** : Sans `-r`, **erreur** pour répertoires.
  ```bash
  cp mydir newdir
  # cp: -r not specified; omitting directory 'mydir'
  ```

**Options cp avancées :**
```bash
# Récursif avec préservation attributs
cp -a source/ dest/
# -a = --archive = -dR --preserve=all
# Préserve permissions, ownership, timestamps, links

# Préserver seulement certains attributs
cp -p source dest
# -p = --preserve=mode,ownership,timestamps

# Interactif (confirmer écrasement)
cp -ri source/ dest/

# Verbose
cp -rv source/ dest/

# Mise à jour (copier si plus récent)
cp -ru source/ dest/

# Créer liens durs au lieu de copier
cp -rl source/ dest/

# Suivre liens symboliques
cp -L source/ dest/    # Copier cible du lien
cp -P source/ dest/    # Copier lien lui-même (défaut)
```

**Exemples pratiques :**
```bash
# Backup complet avec attributs
cp -a /home/user/ /backup/home_user/

# Sync répertoires (mise à jour)
cp -ru /source/ /dest/

# Copie avec progression (via rsync)
rsync -av --progress source/ dest/

# Copie seulement fichiers modifiés aujourd'hui
find source/ -type f -mtime 0 -exec cp --parents {} dest/ \;

# Copie excluant certains fichiers
rsync -av --exclude='*.log' source/ dest/

# Copie structure (pas fichiers)
find source/ -type d -exec mkdir -p dest/{} \;
```

**Différence trailing slash :**
```bash
# Avec slash final
cp -r source/ dest/
# Si dest existe: copie CONTENU dans dest/
# Si dest n'existe pas: crée dest avec contenu de source

# Sans slash
cp -r source dest/
# Si dest existe: crée dest/source avec contenu
# Si dest n'existe pas: crée dest avec contenu de source

# Exemple
cp -r /var/log/ /backup/    → /backup/syslog, /backup/auth.log...
cp -r /var/log /backup/     → /backup/log/syslog, /backup/log/auth.log...
```

**Sauvegardes avec date :**
```bash
# Backup avec timestamp
cp -a /data/ /backup/data_$(date +%Y%m%d)/

# Rotation backups
for i in {5..1}; do
    [ -d /backup/data.$i ] && mv /backup/data.$i /backup/data.$((i+1))
done
cp -a /data/ /backup/data.1/
```

**Comparaison cp vs rsync :**

| Aspect | cp | rsync |
|--------|----|----|
| Vitesse | Rapide | Plus lent (mais optimisé) |
| Réseau | Non | ✅ Oui |
| Reprise | Non | ✅ Oui |
| Différentiel | Limité (-u) | ✅ Excellent |
| Exclusions | Non | ✅ Oui |
| Progrès | Non (natif) | ✅ Oui |
| Bande passante | N/A | ✅ Limitible |

```bash
# rsync pour backups
rsync -av --delete source/ dest/    # Mirror exact
rsync -av --progress source/ dest/  # Avec progression
rsync -avz source/ user@host:dest/  # Via réseau (compressé)
```

---

### Question 18
**Réponse correcte : D (Toutes correctes !)**

**Explication détaillée :**

**A) Lien symbolique peut pointer vers autre partition :**
✅ **VRAI**

```bash
# Lien symbolique cross-partition
ln -s /mnt/external/file.txt /home/user/link
# OK - pointe vers chemin (texte)

# Lien dur cross-partition
ln /mnt/external/file.txt /home/user/hardlink
# ERREUR - impossible (différentes partitions)
# ln: failed to create hard link: Invalid cross-device link
```

**B) Lien dur partage même inode que fichier original :**
✅ **VRAI**

```bash
# Créer lien dur
echo "data" > original.txt
ln original.txt hardlink.txt

# Vérifier inode (identique)
ls -li
# 12345 -rw-r--r-- 2 ... original.txt
# 12345 -rw-r--r-- 2 ... hardlink.txt
#  └─ même inode

# Même fichier physiquement
stat original.txt hardlink.txt
# Inode: 12345 (les deux)

# Modification dans un affecte l'autre
echo "modified" >> hardlink.txt
cat original.txt
# data
# modified
```

**C) Supprimer original casse lien symbolique mais pas lien dur :**
✅ **VRAI**

```bash
# Lien symbolique
ln -s original.txt symlink.txt
rm original.txt
ls -l symlink.txt
# lrwxrwxrwx ... symlink.txt -> original.txt (en rouge, cassé)
cat symlink.txt
# cat: symlink.txt: No such file or directory

# Lien dur
echo "data" > original.txt
ln original.txt hardlink.txt
rm original.txt
cat hardlink.txt
# data    ← Toujours accessible !
# Le fichier existe tant qu'au moins 1 lien existe
```

**Tableau comparatif complet :**

| Aspect | Lien symbolique | Lien dur |
|--------|----------------|----------|
| **Création** | `ln -s target link` | `ln target link` |
| **Pointeur** | Chemin (texte) | Inode (physique) |
| **Cross-partition** | ✅ Oui | ❌ Non |
| **Répertoires** | ✅ Oui | ❌ Non (sauf root) |
| **Original supprimé** | ❌ Lien cassé | ✅ Fichier reste |
| **Espace disque** | ~Négligeable | Partagé (0 extra) |
| **Identification** | `ls -l` (→) | Même inode |
| **Permissions** | Du fichier cible | Propres (mais partagées) |
| **Utilité** | Raccourcis, compatibility | Backups, sécurité données |

**Créer les liens :**
```bash
# Lien symbolique
ln -s /path/to/original /path/to/link
ln -s original.txt symlink.txt        # Relatif
ln -s /abs/path/file.txt link.txt     # Absolu

# Forcer (écraser si existe)
ln -sf original.txt link.txt

# Lien dur
ln original.txt hardlink.txt

# Vérifier type
ls -l link.txt
# lrwxrwxrwx ... link.txt -> original.txt    (symlink)
# -rw-r--r-- 2 ... hardlink.txt              (hard, "2" = link count)

# Destination d'un symlink
readlink link.txt
readlink -f link.txt    # Résoudre chemin absolu
```

**Nombre de liens durs (compteur) :**
```bash
# Colonne 2 de ls -l = nombre de liens durs
ls -l original.txt
# -rw-r--r-- 3 user group 100 Jan 28 15:00 original.txt
#            └─ 3 liens durs pointent vers ce fichier

# Créer 2 liens durs
ln original.txt link1.txt
ln original.txt link2.txt

ls -l original.txt
# -rw-r--r-- 3 ...    (original + link1 + link2 = 3)

# Supprimer un lien
rm link1.txt

ls -l original.txt
# -rw-r--r-- 2 ...    (original + link2 = 2)

# Fichier supprimé quand compteur = 0
rm original.txt
rm link2.txt    # Maintenant supprimé du disque
```

**Trouver liens :**
```bash
# Trouver destination symlink
readlink symlink.txt

# Trouver tous symlinks cassés
find / -xtype l 2>/dev/null

# Trouver tous les liens durs d'un fichier (par inode)
find / -inum 12345 2>/dev/null
find / -samefile original.txt 2>/dev/null

# Lister liens durs d'un fichier
ls -li original.txt    # Noter inode
find . -inum <inode>
```

**Cas d'usage :**
```bash
# Symlink: compatibilité versions
ln -s /usr/bin/python3.11 /usr/bin/python3

# Hard link: backup incrémental (rsync --link-dest)
cp -al /backup/full/ /backup/incremental/
# Liens durs = pas de duplication espace

# Symlink: /var/www/current → /var/www/release-1.2.3
ln -sf /var/www/release-1.2.3 /var/www/current
# Facile de changer version (atomique)

# Hard link: sécurité (pas de suppression accidentelle)
ln important.txt backup_hardlink.txt
```

---

### Question 19
**Réponse correcte : D (Toutes fonctionnent !)**

**Explication détaillée :**

**Méthode A - Glob simple (répertoire courant) :**
```bash
cd /source
mv *.txt /dest/

# Déplace tous les .txt du répertoire courant
```

**Méthode B - Glob avec chemin :**
```bash
mv /source/*.txt /dest/

# Déplace tous les .txt de /source vers /dest
# Note: ne fonctionne que pour /source (pas récursif)
```

**Méthode C - find (récursif) :**
```bash
find /source -name "*.txt" -exec mv {} /dest/ \;

# Trouve TOUS les .txt (récursivement) et déplace
# Attention: écrase structure (tous dans /dest root)

# Pour préserver structure
find /source -name "*.txt" -exec mv --backup=t {} /dest/ \;
```

**Toutes valides !** Choix selon besoin (récursif ou non).

**Différences importantes :**
```bash
# A et B: seulement fichiers directs (pas subdirs)
# C: récursif (tous niveaux)

# Structure:
# /source/
#   file1.txt
#   file2.txt
#   subdir/
#     file3.txt

# mv *.txt /dest/
# → déplace file1.txt, file2.txt (pas file3.txt)

# find ... -exec mv
# → déplace file1.txt, file2.txt, file3.txt
# Attention: file3.txt va dans /dest (pas /dest/subdir)
```

**Options mv avancées :**
```bash
# Interactif (confirmer écrasement)
mv -i *.txt /dest/

# Forcer (pas de confirmation)
mv -f *.txt /dest/

# Ne pas écraser
mv -n *.txt /dest/

# Backup si fichier existe
mv -b *.txt /dest/          # .txt.~ suffix
mv --backup=numbered *.txt /dest/    # .txt.~1~

# Verbose
mv -v *.txt /dest/

# Mise à jour (si plus récent)
mv -u *.txt /dest/
```

**Exemples pratiques :**
```bash
# Déplacer fichiers modifiés aujourd'hui
find /source -name "*.txt" -mtime 0 -exec mv {} /dest/ \;

# Déplacer avec préservation structure (rsync + delete)
rsync -av --remove-source-files /source/*.txt /dest/

# Déplacer puis vérifier
mv *.txt /dest/ && echo "Moved $(ls /dest/*.txt | wc -l) files"

# Déplacer avec renommage
for f in *.txt; do
    mv "$f" "/dest/${f%.txt}_backup.txt"
done

# Déplacer fichiers > 1MB
find . -name "*.txt" -size +1M -exec mv {} /dest/ \;
```

**Déplacer avec préservation structure :**
```bash
# Problème: find écrase structure
find /source -name "*.txt" -exec mv {} /dest/ \;
# /source/sub/file.txt → /dest/file.txt (perd "sub")

# Solution 1: rsync
rsync -av --remove-source-files --include='*.txt' --include='*/' \
    --exclude='*' /source/ /dest/
# Préserve structure

# Solution 2: cpio
cd /source
find . -name "*.txt" | cpio -pdm /dest/
rm -f $(find . -name "*.txt")

# Solution 3: tar
cd /source
tar cf - --files-from=<(find . -name "*.txt") | \
    (cd /dest && tar xf -)
find . -name "*.txt" -delete
```

**Gestion espaces dans noms :**
```bash
# Glob: OK (bash quote automatiquement)
mv *.txt /dest/

# find: utiliser -exec avec {}
find . -name "*.txt" -exec mv {} /dest/ \;

# Ou avec xargs (null-terminated)
find . -name "*.txt" -print0 | xargs -0 mv -t /dest/

# Boucle shell (quote variables)
for f in *.txt; do
    mv "$f" "/dest/"    # Guillemets importants !
done
```

**Vérifications avant déplacement :**
```bash
# Compter fichiers
ls -1 *.txt | wc -l

# Lister fichiers qui seront déplacés
find /source -name "*.txt"

# Dry-run (simulation)
find /source -name "*.txt" -exec echo mv {} /dest/ \;

# Vérifier espace disque destination
df -h /dest

# Test avec un fichier
mv test.txt /dest/ && echo "OK" || echo "Failed"
```

---

### Question 20
**Réponse correcte : D (Toutes créent fichier 100 Mo !)**

**Explication détaillée :**

**Méthode A - dd (classique, écrit réellement) :**
```bash
dd if=/dev/zero of=file.bin bs=1M count=100
# if=/dev/zero  : Source (octets à zéro)
# of=file.bin   : Destination
# bs=1M         : Block size 1 MégaOctet
# count=100     : 100 blocs → 100 Mo

# Résultat:
# 100+0 records in
# 100+0 records out
# 104857600 bytes (105 MB, 100 MiB) copied

# Fichier RÉELLEMENT rempli de zéros (espace alloué)
```

**Méthode B - fallocate (moderne, rapide) :**
```bash
fallocate -l 100M file.bin
# -l 100M : Taille

# Très rapide (allocation espace seulement)
# Fichier sparse possible (selon filesystem)

# Vérifier
ls -lh file.bin
# -rw-r--r-- ... 100M ... file.bin
```

**Méthode C - truncate (ultra-rapide, sparse) :**
```bash
truncate -s 100M file.bin
# -s 100M : Size

# Instantané (ne réserve pas espace physique)
# Fichier sparse (trous)
# ls montre 100M, mais du montre 0

ls -lh file.bin
# -rw-r--r-- ... 100M ... file.bin

du -h file.bin
# 0       file.bin    ← Pas d'espace réel !
```

**Toutes créent fichier 100 Mo**, mais différences importantes :

| Méthode | Vitesse | Espace alloué | Sparse | Usage |
|---------|---------|---------------|--------|-------|
| `dd` | ⭐ Lent | ✅ Oui | ❌ Non | Test I/O, création réelle |
| `fallocate` | ⭐⭐⭐ Très rapide | ✅ Oui | Possible | Allocation rapide |
| `truncate` | ⭐⭐⭐⭐ Instantané | ❌ Non | ✅ Oui | Placeholder, logs |

**Fichiers sparse (trous) :**
```bash
# truncate crée fichier sparse
truncate -s 1G file.bin

# Taille apparente vs réelle
ls -lh file.bin
# -rw-r--r-- ... 1.0G ... file.bin    (apparent)

du -h file.bin
# 0       file.bin                     (réel)

# Écriture rend non-sparse
dd if=/dev/zero of=file.bin bs=1M count=100 conv=notrunc
du -h file.bin
# 100M    file.bin                     (maintenant alloué)
```

**Exemples pratiques :**
```bash
# Benchmark disque (dd)
dd if=/dev/zero of=testfile bs=1G count=1 oflag=direct
# Mesure vitesse écriture réelle

# Fichier swap (fallocate)
fallocate -l 2G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile

# Placeholder log (truncate)
truncate -s 0 /var/log/app.log    # Vider log (taille 0)
truncate -s 1G /var/log/huge.log  # Créer grand fichier

# Remplir partition (test)
dd if=/dev/zero of=/mnt/fillfile bs=1M
# Écrit jusqu'à plein (attention!)

# Fichier aléatoire (pas zéros)
dd if=/dev/urandom of=random.bin bs=1M count=10

# Créer image disque (sparse)
truncate -s 10G disk.img
mkfs.ext4 disk.img
mount -o loop disk.img /mnt
```

**Performances comparées :**
```bash
# Test vitesse (1 Go)
time dd if=/dev/zero of=file1.bin bs=1M count=1024
# real 0m2.5s (écrit réellement)

time fallocate -l 1G file2.bin
# real 0m0.02s (allocation rapide)

time truncate -s 1G file3.bin
# real 0m0.001s (instantané)
```

**Options dd avancées :**
```bash
# Block size optimal (4K)
dd if=/dev/zero of=file.bin bs=4K count=25600

# Avec progression (status=progress)
dd if=/dev/zero of=file.bin bs=1M count=100 status=progress

# Direct I/O (bypass cache)
dd if=/dev/zero of=file.bin bs=1G count=1 oflag=direct

# Conversion
dd if=input.img of=output.img bs=1M conv=sync,noerror
# sync: pad blocks
# noerror: continue sur erreurs
```

**Vérifier contenu :**
```bash
# Hexdump (premiers bytes)
hexdump -C file.bin | head
# 00000000  00 00 00 00 00 00 00 00  |........|
# (tout à zéro)

# Vérifier si fichier est sparse
filefrag -v file.bin
# Montre extents (zones allouées)

# Comparer tailles
ls -lh file.bin     # Taille apparente
du -h file.bin      # Taille réelle
stat file.bin       # Détails complets
```

---

### Question 21
**Réponse correcte : B**

**Explication détaillée :**

`file` détermine le **type de contenu** d'un fichier en analysant ses données :

```bash
file document.pdf
# document.pdf: PDF document, version 1.4

file script.sh
# script.sh: Bash script, ASCII text executable

file image.jpg
# image.jpg: JPEG image data, JFIF standard 1.01

file /bin/ls
# /bin/ls: ELF 64-bit LSB executable, x86-64

file data.tar.gz
# data.tar.gz: gzip compressed data

file empty.txt
# empty.txt: empty

file /dev/sda
# /dev/sda: block special (8/0)
```

**Type MIME :**
```bash
file -i document.pdf
# document.pdf: application/pdf; charset=binary

file -i script.sh
# script.sh: text/x-shellscript; charset=us-ascii

file -i image.jpg
# image.jpg: image/jpeg; charset=binary

# Utile pour serveurs web (Content-Type)
```

**Pourquoi les autres sont incorrectes :**

- **A) `type file.txt`** : Commande **shell builtin** qui montre type de **commande** (pas de fichier).
  ```bash
  type ls
  # ls is aliased to `ls --color=auto'
  
  type cd
  # cd is a shell builtin
  
  type python3
  # python3 is /usr/bin/python3
  ```

- **C) `ls -l file.txt`** : Affiche **métadonnées** (permissions, taille, date), pas type de contenu.
  ```bash
  ls -l file.txt
  # -rw-r--r-- 1 user group 1234 Jan 28 15:00 file.txt
  #  └─ type: - (fichier régulier), pas contenu
  ```

- **D) `stat file.txt`** : Affiche **attributs système** (inode, dates, etc.), pas type de contenu.
  ```bash
  stat file.txt
  # File: file.txt
  # Size: 1234    Blocks: 8    IO Block: 4096   regular file
  # Device: 8,1   Inode: 12345  Links: 1
  # Access: 2026-01-28 15:00:00
  # (infos système, pas analyse contenu)
  ```

**Options file :**
```bash
# Type MIME
file -i file.txt
file --mime-type file.txt

# Brief (sans nom fichier)
file -b script.sh
# Bash script, ASCII text executable

# Tous les fichiers d'un répertoire
file *

# Keep going (continue sur erreurs)
file -k binary.exe

# Suivre symlinks (analyser cible)
file -L symlink.txt

# Ne pas suivre symlinks
file -h symlink.txt
# symlink.txt: symbolic link to original.txt
```

**Exemples pratiques :**
```bash
# Trouver tous les scripts
file * | grep script

# Trouver tous les binaires
file * | grep ELF

# Vérifier images
file *.jpg *.png | grep -v image
# (trouver fichiers mal nommés)

# Type MIME pour upload
MIME=$(file -b --mime-type upload.dat)
echo $MIME    # application/octet-stream

# Détecter encodage
file -i text.txt
# text/plain; charset=utf-8

# Vérifier si exécutable
file /bin/bash | grep executable

# Analyser fichiers inconnus
find /data -type f -exec file {} \; | grep -i "text"
```

**Types communs retournés :**
```bash
# Texte
ASCII text
UTF-8 Unicode text
HTML document
JSON data
XML document

# Scripts
Bash script
Python script
Perl script
Shell script

# Binaires
ELF 64-bit executable
PE32 executable (Windows)
Mach-O executable (macOS)

# Archives
gzip compressed data
Zip archive data
tar archive
bzip2 compressed data

# Images
JPEG image data
PNG image data
GIF image data

# Documents
PDF document
Microsoft Word document
OpenDocument Text

# Spéciaux
symbolic link to ...
directory
block special
character special
empty
```

**Détecter fichiers corrompus :**
```bash
# Vérifier images
for img in *.jpg; do
    file "$img" | grep -q JPEG || echo "Corrupt: $img"
done

# Vérifier archives
file backup.tar.gz | grep -q gzip || echo "Not a valid gzip"

# Vérifier scripts
if file script.sh | grep -q "shell script"; then
    bash -n script.sh    # Syntax check
fi
```

---

### Question 22
**Réponse correcte : D (A et B fonctionnent !)**

**Explication détaillée :**

**Méthode A - rename (Perl-based, si disponible) :**
```bash
rename 's/\.txt$/\.bak/' *.txt
# s/pattern/replacement/  : Substitution Perl regex
# \.txt$                  : .txt à la fin
# \.bak                   : Remplacer par .bak

# Fichiers:
# file1.txt → file1.bak
# file2.txt → file2.bak
# file3.txt → file3.bak
```

**Méthode B - Boucle shell (portable) :**
```bash
for f in *.txt; do
    mv "$f" "${f%.txt}.bak"
done

# ${f%.txt}  : Supprimer .txt à la fin
# .bak       : Ajouter .bak

# Guillemets "$f" importants (gère espaces)
```

**Pourquoi C est incorrecte :**

- **C) `mv *.txt *.bak`** : Syntaxe **invalide**. `mv` ne peut pas remplacer extension comme ça.
  ```bash
  mv *.txt *.bak
  # mv: target '*.bak' is not a directory
  ```

**Variations rename :**
```bash
# Attention: 2 versions de rename !

# Version Perl (Debian/Ubuntu)
rename 's/\.txt$/\.bak/' *.txt
rename 's/ /_/g' *                # Espaces → underscores
rename 'y/A-Z/a-z/' *             # Minuscules

# Version util-linux (RedHat/CentOS)
rename .txt .bak *.txt            # Syntaxe différente !

# Vérifier version
rename --version
# perl-rename (Debian) ou rename from util-linux (RedHat)

# Test sans exécution (dry-run)
rename -n 's/\.txt$/\.bak/' *.txt
```

**Exemples boucle shell :**
```bash
# Ajouter préfixe
for f in *.txt; do
    mv "$f" "backup_$f"
done

# Ajouter suffixe date
for f in *.txt; do
    mv "$f" "${f%.txt}_$(date +%Y%m%d).txt"
done

# Remplacer espaces
for f in *; do
    mv "$f" "${f// /_}"    # Remplace espaces par _
done

# Minuscules
for f in *; do
    mv "$f" "$(echo $f | tr '[:upper:]' '[:lower:]')"
done

# Numéroter fichiers
count=1
for f in *.jpg; do
    mv "$f" "$(printf 'image_%03d.jpg' $count)"
    ((count++))
done
```

**Exemples rename avancés :**
```bash
# Minuscules (Perl rename)
rename 'y/A-Z/a-z/' *

# Supprimer espaces
rename 's/ //g' *

# Préfixe numérique
rename 's/^/0/' [1-9].txt        # 1.txt → 01.txt

# Remplacement complexe
rename 's/(\d+)/sprintf("%03d",$1)/e' *.txt

# Regex complexe
rename 's/file_(\d+)_old\.txt$/document_$1.bak/' *

# Interactif
rename -i 's/\.txt$/\.bak/' *.txt
```

**Sécurité et vérifications :**
```bash
# Dry-run avant exécution
for f in *.txt; do
    echo mv "$f" "${f%.txt}.bak"    # Affiche sans exécuter
done

# Ou avec rename
rename -n 's/\.txt$/\.bak/' *.txt

# Backup avant renommage
for f in *.txt; do
    cp "$f" "$f.backup"
    mv "$f" "${f%.txt}.bak"
done

# Vérifier nombre de fichiers
echo "Will rename $(ls *.txt | wc -l) files"
read -p "Continue? (y/n) " -n 1 -r
if [[ $REPLY =~ ^[Yy]$ ]]; then
    for f in *.txt; do mv "$f" "${f%.txt}.bak"; done
fi
```

**Cas complexes :**
```bash
# Fichiers avec espaces
for f in *.txt; do
    mv "$f" "${f%.txt}.bak"    # Guillemets essentiels !
done

# Préserver chemins
find /data -name "*.txt" -exec bash -c \
    'mv "$0" "${0%.txt}.bak"' {} \;

# Multiple extensions
for ext in txt log tmp; do
    for f in *.$ext; do
        [ -f "$f" ] && mv "$f" "$f.bak"
    done
done

# Avec confirmation
for f in *.txt; do
    read -p "Rename $f to ${f%.txt}.bak? (y/n) " -n 1 -r
    echo
    [[ $REPLY =~ ^[Yy]$ ]] && mv "$f" "${f%.txt}.bak"
done
```

**Alternative : mmv (mass move, si installé) :**
```bash
# Installation
sudo apt install mmv    # Debian/Ubuntu

# Usage
mmv "*.txt" "#1.bak"
# * capture dans #1

mmv "*-old.txt" "#1-new.bak"
mmv "file*.txt" "document#1.bak"
```

---

### Question 23
**Réponse correcte : D (A et B fonctionnent !)**

**Explication détaillée :**

**Méthode A - Classique (portable) :**
```bash
command > output.txt 2>&1
# >          : Redirige STDOUT (fd 1) vers output.txt
# 2>&1       : Redirige STDERR (fd 2) vers où pointe STDOUT (output.txt)

# Ordre important !
# 2>&1 DOIT être APRÈS >

# Exemple
ls /tmp /nonexistent > output.txt 2>&1
cat output.txt
# /tmp:              ← STDOUT
# file1
# file2
# ls: cannot access '/nonexistent': No such file or directory  ← STDERR
```

**Méthode B - Moderne (Bash 4+) :**
```bash
command &> output.txt
# &>         : Redirige STDOUT ET STDERR vers output.txt
# Équivalent à > output.txt 2>&1

ls /tmp /nonexistent &> output.txt
# Même résultat que méthode A
```

**Pourquoi C est problématique :**

- **C) `command > output.txt 2> output.txt`** : **Fonctionne** mais **déconseillé** !
  ```bash
  # Ouvre output.txt DEUX FOIS (deux file descriptors)
  # Possible corruption si écritures simultanées
  # Ordre non garanti
  
  # Mieux utiliser 2>&1 ou &>
  ```

**File descriptors :**
- **0** = STDIN (entrée standard)
- **1** = STDOUT (sortie standard)
- **2** = STDERR (erreur standard)

**Redirections complètes :**
```bash
# STDOUT seulement
command > output.txt
command 1> output.txt    # Explicite

# STDERR seulement
command 2> error.txt

# STDOUT et STDERR ensemble
command > all.txt 2>&1        # Classique
command &> all.txt            # Moderne

# STDOUT et STDERR séparés
command > output.txt 2> error.txt

# Append (ajouter)
command >> output.txt 2>&1
command &>> all.txt           # Moderne

# STDERR vers STDOUT (puis pipe)
command 2>&1 | grep pattern

# Tout vers /dev/null (silence)
command > /dev/null 2>&1
command &> /dev/null

# STDIN depuis fichier, STDOUT vers autre
command < input.txt > output.txt

# Combiner
command < input.txt > output.txt 2> error.txt
```

**Exemples pratiques :**
```bash
# Installation silencieuse
sudo apt install package &> /dev/null

# Log complet (succès + erreurs)
./backup.sh &> backup_$(date +%Y%m%d).log

# Log séparé succès/erreurs
./script.sh > success.log 2> error.log

# Afficher STDOUT, log STDERR
command 2> error.log

# Log STDERR, afficher STDOUT
command 2> error.log

# Dupliquer STDOUT et log
command | tee output.log

# Dupliquer STDERR et log
command 2>&1 | tee all.log

# Vérifier si erreurs
./script.sh &> /tmp/log
if grep -q ERROR /tmp/log; then
    echo "Errors found"
fi
```

**Ordre d'exécution (IMPORTANT) :**
```bash
# CORRECT
command > file.txt 2>&1
# 1. STDOUT → file.txt
# 2. STDERR → où pointe STDOUT (file.txt) ✓

# INCORRECT
command 2>&1 > file.txt
# 1. STDERR → où pointe STDOUT (terminal actuellement)
# 2. STDOUT → file.txt
# Résultat: STDERR va au terminal, STDOUT dans fichier ✗

# Démonstration
ls /tmp /nonexistent 2>&1 > output.txt
# Erreurs à l'écran, pas dans fichier !
```

**Redirections avancées :**
```bash
# Swapper STDOUT et STDERR
command 3>&1 1>&2 2>&3
# 3 = backup STDOUT
# 1 → STDERR
# 2 → backup (original STDOUT)

# Rediriger vers multiples fichiers
command > >(tee stdout.log) 2> >(tee stderr.log >&2)

# Supprimer STDERR, garder STDOUT
command 2> /dev/null

# Supprimer STDOUT, garder STDERR
command > /dev/null

# Here document
command << EOF > output.txt
line 1
line 2
EOF

# Here string
command <<< "input text" > output.txt
```

**Gestion logs :**
```bash
# Rotation log automatique
./long_running.sh &>> /var/log/app.log

# Log avec timestamp
exec > >(ts '[%Y-%m-%d %H:%M:%S]' | tee -a /var/log/script.log)
exec 2>&1

# Log seulement si erreurs
./script.sh &> /tmp/log.$$ || cat /tmp/log.$$
```

---

### Question 24
**Réponse correcte : A**

**Explication détaillée :**

`tee` lit STDIN et écrit vers **STDOUT ET fichier(s)** simultanément :

```bash
command | tee output.txt
# Affiche à l'écran ET sauvegarde dans output.txt

# Exemple
ls -l | tee files.txt
# Affiche listing à l'écran
# ET sauvegarde dans files.txt

# Vérifier
cat files.txt    # Même contenu affiché
```

**Schéma :**
```
command → | → tee → → → → fichier
                 ↓
                STDOUT (écran)
```

**Pourquoi les autres sont incorrectes :**

- **B) `command > output.txt`** : Redirige **seulement vers fichier**, rien à l'écran.
  ```bash
  ls -l > files.txt    # Pas d'affichage
  ```

- **C) `command >> output.txt`** : Idem que B, mais **append** (ajoute) au lieu d'écraser.

- **D) `command | cat > output.txt`** : Équivalent à `>` (seulement fichier, pas d'affichage).
  ```bash
  ls -l | cat > files.txt    # Pas d'affichage
  ```

**Options tee :**
```bash
# Append (ajouter)
command | tee -a output.txt

# Ignorer interruptions (SIGINT)
command | tee -i output.txt

# Multiple fichiers
command | tee file1.txt file2.txt file3.txt

# Combiner avec redirections
command 2>&1 | tee all.log    # STDOUT + STDERR
```

**Exemples pratiques :**
```bash
# Installation avec log
sudo apt update | tee install.log

# Compilation avec log
make 2>&1 | tee build.log

# Long processus avec log
./long_script.sh | tee -a process.log

# Pipeline avec logs intermédiaires
command1 | tee step1.log | \
    command2 | tee step2.log | \
    command3 | tee step3.log

# Multiples destinations
ps aux | tee processes.txt | grep apache | tee apache.txt

# Avec date dans fichier
date | tee -a logfile.txt
command | tee -a logfile.txt
```

**tee pour STDERR :**
```bash
# STDERR aussi
command 2>&1 | tee output.log

# Séparer STDOUT et STDERR
command > >(tee stdout.log) 2> >(tee stderr.log >&2)

# Ou plus simple
command 2>&1 | tee all.log
```

**Cas d'usage :**
```bash
# Monitoring avec log
top -b -n 1 | tee system_state.txt

# Backup avec confirmation visuelle
tar czf backup.tar.gz /data | tee backup.log

# Tests avec log
pytest 2>&1 | tee test_results.txt

# Debugging script
bash -x script.sh 2>&1 | tee debug.log

# Analyse performance
time ./benchmark.sh 2>&1 | tee perf.log
```

**Append vs overwrite :**
```bash
# Overwrite (défaut)
command | tee file.txt
# Écrase file.txt

# Append
command | tee -a file.txt
# Ajoute à file.txt

# Log avec date
echo "=== $(date) ===" | tee -a daily.log
command | tee -a daily.log
```

**Multiple fichiers :**
```bash
# Écrire dans 3 fichiers + afficher
command | tee log1.txt log2.txt log3.txt

# Avec chemins
command | tee /var/log/app.log ~/backup.log

# Condition
if [ "$DEBUG" = "1" ]; then
    command | tee debug.log
else
    command
fi
```

**Combiner avec autres commandes :**
```bash
# tee + grep (filtrer et sauver)
dmesg | tee dmesg.log | grep -i error

# tee + wc (compter et sauver)
cat file.txt | tee backup.txt | wc -l

# tee multiple + traitement
command | tee >(process1) >(process2) >(process3) > final.txt
```

---

### Question 25
**Réponse correcte : B**

**Explication détaillée :**

`2> /dev/null` redirige **STDERR (fd 2)** vers `/dev/null` (trou noir) :

```bash
command 2> /dev/null
# 2>         : Redirige file descriptor 2 (STDERR)
# /dev/null  : Périphérique qui ignore tout

# Résultat: Messages d'erreur supprimés
# STDOUT (fd 1) reste affiché
```

**Exemple :**
```bash
# Sans redirection
ls /tmp /nonexistent
# /tmp:              ← STDOUT
# file1
# file2
# ls: cannot access '/nonexistent': No such file or directory  ← STDERR (rouge)

# Avec 2> /dev/null
ls /tmp /nonexistent 2> /dev/null
# /tmp:              ← STDOUT affiché
# file1
# file2
# (erreur supprimée)
```

**Pourquoi les autres sont incorrectes :**

- **A) Redirige STDOUT vers /dev/null** : Faux. Ce serait `> /dev/null` ou `1> /dev/null`.
  ```bash
  command > /dev/null    # Supprime STDOUT
  ```

- **C) STDOUT et STDERR vers /dev/null** : Faux. Ce serait `&> /dev/null` ou `> /dev/null 2>&1`.
  ```bash
  command &> /dev/null   # Tout supprimer
  ```

- **D) Supprime fichier /dev/null** : **Impossible**. `/dev/null` est un périphérique système spécial (pas un fichier normal).

**File descriptors :**
```bash
0  STDIN   (entrée)
1  STDOUT  (sortie)
2  STDERR  (erreur)

# Redirections
command > file      # 1> (STDOUT)
command 2> file     # STDERR
command < file      # 0< (STDIN)
```

**Usages de /dev/null :**
```bash
# Supprimer STDERR
find / -name "*.txt" 2> /dev/null
# Pas de "Permission denied"

# Supprimer STDOUT
command > /dev/null
# Seulement erreurs visibles

# Tout supprimer
command > /dev/null 2>&1
command &> /dev/null

# Test existence (ignore sortie)
if command &> /dev/null; then
    echo "Command succeeded"
fi

# Vider fichier
> file.txt
cat /dev/null > file.txt
```

**Exemples pratiques :**
```bash
# find sans "Permission denied"
find / -name "*.log" 2> /dev/null

# grep silencieux (juste exit code)
if grep -q "pattern" file.txt 2> /dev/null; then
    echo "Found"
fi

# Commande silencieuse complète
apt update &> /dev/null && echo "Updated"

# ping sans output (juste test)
ping -c 1 google.com > /dev/null 2>&1 && echo "Online"

# Vérifier commande existe
if which docker &> /dev/null; then
    echo "Docker installed"
fi

# Cron job silencieux
0 2 * * * /path/script.sh > /dev/null 2>&1
```

**Périphériques spéciaux :**
```bash
/dev/null      # Trou noir (ignore tout)
/dev/zero      # Source de zéros
/dev/random    # Source aléatoire (bloque si entropy basse)
/dev/urandom   # Source aléatoire (non-bloquant)
/dev/stdin     # Lien vers fd 0
/dev/stdout    # Lien vers fd 1
/dev/stderr    # Lien vers fd 2
```

**Combiner redirections :**
```bash
# STDOUT vers fichier, STDERR vers null
command > output.txt 2> /dev/null

# STDERR vers fichier, STDOUT vers null
command > /dev/null 2> error.log

# STDOUT+STDERR vers null (2 syntaxes)
command > /dev/null 2>&1
command &> /dev/null

# Inverser (afficher STDERR, cacher STDOUT)
command 2>&1 > /dev/null | grep ERROR
```

**Test avec /dev/null :**
```bash
# Écriture (rien ne se passe)
echo "test" > /dev/null

# Lecture (EOF immédiat)
cat /dev/null
# (vide)

# Taille toujours 0
ls -l /dev/null
# crw-rw-rw- 1 root root 1, 3 Jan 28 15:00 /dev/null
#  └─ c = character device

# Écrire beaucoup (pas de problème)
dd if=/dev/zero of=/dev/null bs=1G count=100
# (instantané, rien ne stocke)
```

---

### Question 26
**Réponse correcte : C**

**Explication détaillée :**

Le **pipe `|`** envoie STDOUT d'une commande comme STDIN de la suivante :

```bash
cmd1 | cmd2 | cmd3
# STDOUT de cmd1 → STDIN de cmd2
# STDOUT de cmd2 → STDIN de cmd3
# STDOUT de cmd3 → écran (ou redirection)

# Exemple
cat file.txt | grep ERROR | wc -l
# cat     : Lit fichier
# grep    : Filtre lignes avec ERROR
# wc -l   : Compte lignes
# Résultat: Nombre d'erreurs
```

**Pipeline classique :**
```bash
ps aux | grep apache | grep -v grep | wc -l
# 1. Liste processus
# 2. Filtre apache
# 3. Supprime ligne "grep" elle-même
# 4. Compte résultats
```

**Pourquoi les autres sont incorrectes :**

- **A) `cmd1 ; cmd2 ; cmd3`** : Exécute **séquentiellement** (pas de traitement de sortie).
  ```bash
  ls ; pwd ; date
  # Exécute les 3, MAIS pas de connexion entre elles
  # (ls ne passe rien à pwd)
  ```

- **B) `cmd1 && cmd2 && cmd3`** : Exécute **si précédente réussit** (pas de pipe).
  ```bash
  make && make install && echo "Done"
  # Install si make réussit
  # Mais pas de traitement de sortie
  ```

- **D) `cmd1 > cmd2 > cmd3`** : Syntaxe **invalide**. `>` redirige vers **fichier** (pas commande).
  ```bash
  ls > grep txt    # Crée fichier nommé "grep" !
  ```

**Exemples pipelines :**
```bash
# Top 10 processus CPU
ps aux --sort=-%cpu | head -10

# Top 10 IPs dans logs
cut -d ' ' -f 1 access.log | sort | uniq -c | sort -rn | head -10

# Statistiques lignes de code
find . -name "*.py" | xargs wc -l | sort -n | tail -20

# Utilisateurs avec shell Bash
cat /etc/passwd | cut -d: -f1,7 | grep bash | cut -d: -f1

# Mots les plus fréquents
cat book.txt | tr -cs 'A-Za-z' '\n' | tr '[:upper:]' '[:lower:]' | \
    sort | uniq -c | sort -rn | head -20

# Répertoires les plus volumineux
du -h | sort -rh | head -10

# Processus zombie
ps aux | awk '$8 ~ /Z/ {print}'

# Monitoring temps réel
tail -f /var/log/syslog | grep --line-buffered ERROR | \
    while read line; do echo "[ALERT] $line"; done
```

**Pipes avec STDERR :**
```bash
# STDERR ne passe PAS par pipe (seulement STDOUT)
command1 | command2
# STDOUT de cmd1 → cmd2
# STDERR de cmd1 → écran

# Passer STDERR aussi
command1 2>&1 | command2
# STDOUT + STDERR → cmd2

# Exemple
find / -name "*.txt" 2>&1 | grep -v "Permission denied"
# Filtre erreurs du find
```

**Pipes multiples niveaux :**
```bash
# 5 étapes
cat data.csv | \
    cut -d, -f2,3 | \
    grep -v '^#' | \
    sort -t, -k2 -n | \
    head -100 | \
    tee top100.csv

# Avec filtrage progressif
cat /var/log/syslog | \
    grep "Jan 28" | \
    grep ERROR | \
    awk '{print $5, $6, $7}' | \
    sort | \
    uniq -c | \
    sort -rn
```

**xargs (construire commandes depuis pipe) :**
```bash
# Liste → arguments
find . -name "*.tmp" | xargs rm

# Avec placeholder
find . -name "*.txt" | xargs -I {} cp {} /backup/

# Parallèle
find . -name "*.jpg" | xargs -P 4 -n 1 convert -resize 800x600

# Null-terminated (espaces dans noms)
find . -name "*.txt" -print0 | xargs -0 rm
```

**Process substitution (avancé) :**
```bash
# Comparer sorties de 2 commandes
diff <(ls dir1) <(ls dir2)

# Multiple inputs
paste <(cut -d: -f1 /etc/passwd) <(cut -d: -f3 /etc/passwd)

# Combiner
cat file1.txt <(echo "===") file2.txt
```

---

### Question 27
**Réponse correcte : D (A et B fonctionnent !)**

**Explication détaillée :**

**Méthode A - /dev/urandom avec tr :**
```bash
tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 16
# tr -dc          : Delete complement (garde seulement chars spécifiés)
# 'A-Za-z0-9'     : Lettres et chiffres
# /dev/urandom    : Source aléatoire
# head -c 16      : 16 caractères

# Exemple sortie:
# Kj8mN2pQ9rXt4vZa
```

**Méthode B - openssl :**
```bash
openssl rand -base64 16
# rand            : Génère aléatoire
# -base64         : Encodage base64
# 16              : 16 bytes (→ ~21 chars base64)

# Exemple sortie:
# 3kJ9mN2pQ8rXt4vZ+a==

# Pour exactement 16 chars
openssl rand -base64 12 | cut -c1-16
```

**Les deux sont valides !** `tr+urandom` plus personnalisable, `openssl` plus standard.

**Pourquoi C est problématique :**

- **C) `cat /dev/random | head -c 16`** : Utilise `/dev/random` qui **bloque** si entropy faible. Peut être **très lent**.
  ```bash
  # /dev/random bloque si pas assez d'entropy
  cat /dev/random | head -c 16
  # (peut prendre plusieurs minutes si entropy basse)
  
  # /dev/urandom ne bloque jamais (préféré)
  cat /dev/urandom | head -c 16
  ```

**Sources aléatoires :**
```bash
/dev/random      # "True" random, bloque si entropy basse
/dev/urandom     # Pseudo-random, ne bloque jamais (recommandé)
```

**Variations mot de passe :**
```bash
# Alphanumériques seulement
tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 16

# Avec symboles
tr -dc 'A-Za-z0-9!@#$%^&*' < /dev/urandom | head -c 20

# Seulement minuscules et chiffres
tr -dc 'a-z0-9' < /dev/urandom | head -c 12

# Hexadécimal
openssl rand -hex 8        # 16 chars hex

# Base64
openssl rand -base64 12    # ~16 chars

# Avec date (seed)
date +%s | sha256sum | base64 | head -c 16

# Multiple mots de passe
for i in {1..5}; do
    tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 16
    echo
done
```

**Exemples pratiques :**
```bash
# Mot de passe fort (20 chars avec symboles)
PASSWORD=$(tr -dc 'A-Za-z0-9!@#$%^&*()-_=+' < /dev/urandom | head -c 20)
echo $PASSWORD

# Hash pour token
openssl rand -hex 32

# UUID
cat /proc/sys/kernel/random/uuid
uuidgen    # Si disponible

# API key (32 chars alphanumériques)
tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 32

# PIN code (6 chiffres)
tr -dc '0-9' < /dev/urandom | head -c 6

# Passphrase (mots lisibles)
shuf -n 4 /usr/share/dict/words | tr '\n' '-' | sed 's/-$//'
```

**Vérifier qualité :**
```bash
# Tester caractères présents
PASSWORD=$(tr -dc 'A-Za-z0-9!@#' < /dev/urandom | head -c 20)
echo $PASSWORD | grep -E '[A-Z]' && echo "Has uppercase"
echo $PASSWORD | grep -E '[a-z]' && echo "Has lowercase"
echo $PASSWORD | grep -E '[0-9]' && echo "Has digit"
echo $PASSWORD | grep -E '[!@#]' && echo "Has symbol"

# Longueur
echo $PASSWORD | wc -c
```

**Sécurité :**
```bash
# Ne PAS utiliser (faible)
date +%s    # Timestamp prévisible
$RANDOM     # Pseudo-random simple (16-bit)

# UTILISER (fort)
/dev/urandom
openssl rand
```

---

### Question 28
**Réponse correcte : B**

**Explication détaillée :**

`xargs` lit stdin et construit des commandes en utilisant cette entrée comme **arguments** :

```bash
# Principe
echo "file1 file2 file3" | xargs rm
# xargs construit: rm file1 file2 file3

# Équivalent à
rm file1 file2 file3

# Exemple pratique
find . -name "*.tmp" | xargs rm
# Trouve *.tmp puis les supprime
```

**Sans xargs (ne fonctionne pas) :**
```bash
# Ceci NE fonctionne PAS
find . -name "*.tmp" | rm
# rm attend arguments, pas stdin

# xargs résout ce problème
find . -name "*.tmp" | xargs rm
```

**Options xargs essentielles :**
```bash
# -n : N arguments par commande
echo "1 2 3 4 5" | xargs -n 2 echo
# echo 1 2
# echo 3 4
# echo 5

# -I : Placeholder
find . -name "*.txt" | xargs -I {} cp {} /backup/
# {} remplacé par chaque ligne

# -P : Parallèle
find . -name "*.jpg" | xargs -P 4 -n 1 convert -resize 800x600
# 4 processus parallèles

# -p : Interactif (confirmer)
find . -name "*.log" | xargs -p rm

# -t : Trace (afficher commande)
echo "a b c" | xargs -t rm
# rm a b c (affiché)

# -0 : Null-terminated (avec find -print0)
find . -name "*.txt" -print0 | xargs -0 rm
# Gère espaces dans noms
```

**Pourquoi les autres sont incorrectes :**

- **A) Compresse des fichiers** : Faux. C'est `gzip`, `tar`, `zip`, etc.
  
- **C) Cherche fichiers par nom** : Faux. C'est `find`, `locate`.

- **D) Trie des lignes** : Faux. C'est `sort`.

**Exemples pratiques :**
```bash
# Supprimer fichiers trouvés
find . -name "*.tmp" | xargs rm

# Grep dans plusieurs fichiers
find . -name "*.log" | xargs grep "ERROR"

# Chmod multiple
find . -type f -name "*.sh" | xargs chmod +x

# Télécharger URLs
cat urls.txt | xargs -n 1 wget

# Traitement parallèle
cat files.txt | xargs -P 8 -n 1 process_file.sh

# Copier avec structure
find /source -name "*.pdf" | xargs -I {} cp {} /dest/

# Déplacer fichiers modifiés aujourd'hui
find . -type f -mtime 0 | xargs -I {} mv {} /backup/

# Créer archives par lot
ls *.txt | xargs -n 10 tar czf batch.tar.gz
```

**Gestion espaces dans noms :**
```bash
# PROBLÈME: fichiers avec espaces
find . -name "*.txt" | xargs rm
# Si "my file.txt" existe, xargs voit "my" et "file.txt" (2 fichiers)

# SOLUTION: -print0 et -0
find . -name "*.txt" -print0 | xargs -0 rm
# Utilise null (\0) comme séparateur
```

**Limiter arguments (éviter "Argument list too long") :**
```bash
# Erreur sans xargs
rm $(find . -name "*.tmp")
# bash: /bin/rm: Argument list too long (si beaucoup de fichiers)

# OK avec xargs (batch automatique)
find . -name "*.tmp" | xargs rm
# xargs découpe en multiples appels si nécessaire
```

**Placeholder avancé :**
```bash
# -I avec multiple usages
find . -name "*.txt" | xargs -I {} sh -c 'echo {}; wc -l {}'

# Renommer avec pattern
ls *.txt | xargs -I {} sh -c 'mv {} $(basename {} .txt).bak'

# Backup avec date
find . -name "*.conf" | xargs -I {} cp {} {}.$(date +%Y%m%d)
```

**Alternatives :**
```bash
# find -exec (intégré)
find . -name "*.tmp" -exec rm {} \;
find . -name "*.tmp" -delete    # Plus direct

# Mais xargs souvent plus rapide (moins d'appels)
find . -name "*.tmp" | xargs rm    # Un appel avec N args
find . -name "*.tmp" -exec rm {} \;   # N appels avec 1 arg

# -exec {} + (batch comme xargs)
find . -name "*.tmp" -exec rm {} +    # Similaire à xargs
```

**Parallélisation :**
```bash
# Séquentiel (lent)
for file in *.jpg; do
    convert $file -resize 800x600 resized/$file
done

# Parallèle avec xargs (rapide)
ls *.jpg | xargs -P 4 -I {} convert {} -resize 800x600 resized/{}
# 4 conversions simultanées
```

---

### Question 29
**Réponse correcte : D (B et C fonctionnent !)**

**Explication détaillée :**

Deux syntaxes pour afficher tous les processus :

**Méthode B - BSD style :**
```bash
ps aux
# a = tous les utilisateurs
# u = format utilisateur (USER, PID, %CPU, %MEM, etc.)
# x = inclus processus sans terminal

# Sortie:
# USER  PID %CPU %MEM    VSZ   RSS TTY   STAT START   TIME COMMAND
# root    1  0.0  0.1 168888  9876 ?     Ss   15:00   0:02 /sbin/init
# www   123  0.5  2.3 456789 12345 ?     S    15:10   1:23 apache2
```

**Méthode C - UNIX style :**
```bash
ps -ef
# -e = tous les processus
# -f = full format (UID, PID, PPID, C, STIME, TTY, TIME, CMD)

# Sortie:
# UID   PID  PPID  C STIME TTY      TIME CMD
# root    1     0  0 15:00 ?     00:00:02 /sbin/init
# www   123     1  0 15:10 ?     00:01:23 apache2
```

**Les deux montrent tous les processus !** Différence : format de sortie.

**Pourquoi A est incorrecte :**

- **A) `ps`** : Sans options, affiche **seulement processus de l'utilisateur courant dans le terminal actuel**.
  ```bash
  ps
  #   PID TTY          TIME CMD
  #  1234 pts/0    00:00:00 bash
  #  5678 pts/0    00:00:00 ps
  ```

**Comparaison formats :**

| Option | Style | Affichage | Colonnes clés |
|--------|-------|-----------|---------------|
| `ps` | Minimal | Utilisateur courant | PID, TTY, TIME, CMD |
| `ps aux` | BSD | Tous + détails | USER, %CPU, %MEM, VSZ, RSS |
| `ps -ef` | UNIX | Tous + full | UID, PID, PPID, STIME |
| `ps -ely` | UNIX | Très détaillé | F, S, UID, PID, PPID, PRI, NI |

**Options ps courantes :**
```bash
# Tous processus (2 syntaxes)
ps aux
ps -ef

# Format personnalisé
ps -eo pid,user,cmd,%cpu,%mem
ps aux --sort=-%cpu    # Tri par CPU décroissant

# Processus d'un utilisateur
ps -u username
ps aux | grep ^username

# Hiérarchie (arbre)
ps auxf        # BSD avec tree
ps -ejH        # UNIX hierarchical
pstree -p      # Arbre dédié

# Processus spécifique
ps -C apache2
ps aux | grep apache2

# Avec threads
ps -eLf
ps auxm
```

**Colonnes importantes ps aux :**
```bash
# USER      : Propriétaire processus
# PID       : Process ID
# %CPU      : Utilisation CPU
# %MEM      : Utilisation mémoire
# VSZ       : Virtual memory (KB)
# RSS       : Resident memory (KB)
# TTY       : Terminal (? = pas de terminal)
# STAT      : État processus
# START     : Heure démarrage
# TIME      : Temps CPU cumulé
# COMMAND   : Commande complète
```

**États processus (STAT) :**
```bash
R    Running (en cours)
S    Sleeping (interruptible)
D    Sleeping (uninterruptible, I/O wait)
T    Stopped (Ctrl+Z)
Z    Zombie (terminé mais pas nettoyé)
<    High priority
N    Low priority
L    Pages locked in memory
s    Session leader
l    Multi-threaded
+    Foreground process group
```

**Exemples pratiques :**
```bash
# Top 10 processus CPU
ps aux --sort=-%cpu | head -11

# Top 10 processus mémoire
ps aux --sort=-%mem | head -11

# Processus zombies
ps aux | awk '$8 ~ /Z/ {print}'

# Processus depuis plus de 10 jours
ps -eo pid,etime,cmd | grep -E '[0-9]{2,}-'

# Arborescence depuis PID 1
ps -p 1 --forest

# Processus avec chemin complet
ps auxww

# Format custom
ps -eo pid,user,args,pcpu,pmem --sort=-pcpu | head -20

# Tous les Apache
ps aux | grep '[a]pache'    # [a] évite grep lui-même
```

**ps vs top :**
```bash
# ps : Snapshot statique
ps aux    # Un instant T

# top : Temps réel dynamique
top       # Rafraîchit toutes les secondes
```

**ps vs pgrep :**
```bash
# ps + grep
ps aux | grep apache2

# pgrep (plus direct)
pgrep apache2        # Juste PIDs
pgrep -a apache2     # Avec commande
pgrep -l apache2     # Avec nom
```

---

### Question 30
**Réponse correcte : B**

**Explication détaillée :**

`kill PID` (ou `kill -15 PID`) envoie **SIGTERM** (signal 15) qui permet au processus de :
- Sauvegarder son état
- Libérer ressources
- Fermer fichiers proprement
- Terminer élégamment

```bash
kill 1234
kill -15 1234    # Explicite (SIGTERM)
kill -TERM 1234  # Par nom

# Processus reçoit signal et peut:
# - Finir tâches en cours
# - Flush buffers
# - Cleanup fichiers temporaires
# - Exit proprement
```

**Pourquoi les autres sont incorrectes :**

- **A) `kill -9 PID`** : Envoie **SIGKILL** (force). Processus **ne peut PAS** l'intercepter. Terminaison **immédiate brutale**.
  ```bash
  kill -9 1234
  # SIGKILL = terminaison forcée
  # Pas de cleanup possible
  # Peut laisser:
  #   - Fichiers corrompus
  #   - Ressources non libérées
  #   - Verrous actifs
  #   - Données non sauvegardées
  
  # À utiliser EN DERNIER RECOURS seulement !
  ```

- **C) `killall -9 processname`** : Idem SIGKILL (brutal) mais par nom.

- **D) `pkill -KILL processname`** : Idem SIGKILL par nom.

**Signaux importants :**
```bash
# Liste signaux
kill -l

# Signaux courants:
1  SIGHUP    Hangup (reload config)
2  SIGINT    Interrupt (Ctrl+C)
9  SIGKILL   Kill (force, NON capturable)
15 SIGTERM   Terminate (propre, capturable) ← DÉFAUT
18 SIGCONT   Continue
19 SIGSTOP   Stop (pause, NON capturable)
20 SIGTSTP   Stop (Ctrl+Z, capturable)
```

**Processus de kill propre :**
```bash
# 1. Essayer SIGTERM (propre)
kill 1234
sleep 5

# 2. Vérifier si toujours actif
if ps -p 1234 > /dev/null; then
    # 3. Force si nécessaire
    kill -9 1234
fi

# Ou avec timeout
timeout 10 kill 1234 || kill -9 1234
```

**Script kill gracieux :**
```bash
#!/bin/bash
PID=$1
kill $PID

# Attendre max 10 secondes
for i in {1..10}; do
    # kill -0 teste si processus existe (pas de kill)
    kill -0 $PID 2>/dev/null || exit 0
    sleep 1
done

# Force si toujours là
echo "Forcing kill..."
kill -9 $PID
```

**Exemples pratiques :**
```bash
# Kill propre
kill 1234

# Kill par nom (propre)
pkill apache2
killall apache2

# Reload config (SIGHUP)
kill -HUP $(cat /var/run/nginx.pid)
pkill -HUP nginx
systemctl reload nginx    # Préféré

# Pause processus
kill -STOP 1234

# Reprendre
kill -CONT 1234

# Interrupt (comme Ctrl+C)
kill -INT 1234

# Liste processus puis kill
ps aux | grep myapp
kill 1234 5678 9012    # Multiple PIDs
```

**killall et pkill :**
```bash
# killall (par nom exact)
killall apache2           # SIGTERM
killall -9 apache2        # SIGKILL (éviter)
killall -HUP nginx        # SIGHUP
killall -i apache2        # Interactif
killall -u username       # Par utilisateur

# pkill (par pattern)
pkill apache              # Match "apache"
pkill -9 firefox          # SIGKILL (éviter)
pkill -HUP nginx
pkill -u www-data         # Par utilisateur
pgrep -a apache | pkill   # Via pgrep
```

**Vérifier kill réussi :**
```bash
# Tester existence
kill -0 1234 && echo "Still running" || echo "Terminated"

# Attendre terminaison
while kill -0 1234 2>/dev/null; do
    sleep 1
done
echo "Process terminated"

# Avec ps
ps -p 1234 > /dev/null && echo "Running" || echo "Dead"
```

**Services systemd (préféré) :**
```bash
# Plutôt que kill manuel
systemctl stop apache2     # Propre
systemctl kill apache2     # SIGTERM
systemctl kill -s SIGKILL apache2  # Force

# Reload sans redémarrer
systemctl reload nginx
systemctl reload-or-restart nginx
```

**Cas particuliers :**
```bash
# Processus bloqué en I/O (état D)
ps aux | awk '$8 ~ /D/ {print $2, $11}'
# SIGKILL ne fonctionne pas toujours
# Attendre fin I/O ou reboot

# Zombies (état Z)
ps aux | awk '$8 ~ /Z/ {print $2, $11}'
# Déjà mort, attend parent
# Kill parent ou attendre

# Init (PID 1)
kill 1    # Interdit (reboot sinon)
# systemd/init ne peut être tué
```

---

### Question 31
**Réponse correcte : B**

**Explication détaillée :**

`jobs` affiche les **jobs (tâches)** du shell actuel :

```bash
# Lancer processus en background
sleep 100 &
[1] 12345

vim file.txt
# Ctrl+Z (suspend)
[2]+ Stopped    vim file.txt

# Lister jobs
jobs
# [1]- Running    sleep 100 &
# [2]+ Stopped    vim file.txt
#  │   └─ état    └─ commande
#  └─ numéro job
```

**Symboles jobs :**
```bash
+    Job par défaut (utilisé si pas de numéro spécifié)
-    Job suivant
     (vide) = autre job
```

**Options jobs :**
```bash
# Liste basique
jobs

# Avec PIDs
jobs -l
# [1]  12345 Running    sleep 100 &
# [2]+ 12346 Stopped    vim file.txt

# PIDs seulement
jobs -p
# 12345
# 12346

# Running seulement
jobs -r

# Stopped seulement
jobs -s
```

**Pourquoi les autres sont incorrectes :**

- **A) `ps`** : Affiche **tous processus système** (pas limité aux jobs du shell).
  ```bash
  ps    # Tous processus, pas jobs concept
  ```

- **C) `bg`** : **Reprend** job en background (ne liste pas).
  ```bash
  bg %1    # Reprend job 1 en background
  ```

- **D) `top`** : Monitoring **temps réel** tous processus (pas jobs spécifiquement).

**Gestion jobs :**
```bash
# Lancer en background
sleep 100 &
command &

# Suspendre (Ctrl+Z)
# En cours d'exécution, appuyer Ctrl+Z

# Reprendre en background
bg
bg %1
bg %2

# Reprendre en foreground
fg
fg %1
fg %2

# Tuer job
kill %1
kill %2

# Attendre job
wait %1
wait        # Attendre tous jobs
```

**Exemples pratiques :**
```bash
# Multiple jobs
sleep 100 &
sleep 200 &
sleep 300 &

jobs
# [1]  Running    sleep 100 &
# [2]- Running    sleep 200 &
# [3]+ Running    sleep 300 &

# Reprendre job 2 en foreground
fg %2

# Background tous jobs stoppés
for job in $(jobs -p); do bg $job; done

# Kill tous jobs
for job in $(jobs -p); do kill $job; done
```

**États jobs :**
```bash
Running      En cours (background)
Stopped      Suspendu (Ctrl+Z)
Done         Terminé avec succès
Exit N       Terminé avec code N
Terminated   Tué par signal
```

**Job control complet :**
```bash
# 1. Lancer
./long_script.sh

# 2. Suspendre (Ctrl+Z)
^Z
[1]+ Stopped    ./long_script.sh

# 3. Background
bg %1
[1]+ ./long_script.sh &

# 4. Foreground
fg %1

# 5. Détacher complètement
disown %1    # Shell n'attend plus le job
# Ou relancer avec nohup
nohup ./long_script.sh &
```

**Référencer jobs :**
```bash
%1       Job numéro 1
%2       Job numéro 2
%+       Job courant (le plus récent)
%-       Job précédent
%        Job courant (= %+)
%string  Job commençant par "string"
%?string Job contenant "string"

# Exemples
fg %1
kill %2
bg %-
fg %vim      # Job commençant par vim
kill %?sleep # Job contenant sleep
```

**Jobs vs processus :**
```bash
# Jobs = shell-specific
jobs         # Seulement jobs du shell actuel
# Nouveau terminal → pas de jobs

# Processus = système-wide
ps aux       # Tous processus tous utilisateurs

# Lien: jobs -l montre PID
jobs -l
# [1]+ 12345 Running    sleep 100 &

ps -p 12345
# Même processus
```

**Persister jobs après déconnexion :**
```bash
# nohup (no hangup)
nohup long_command &
# Continue après logout
# Output dans nohup.out

# disown
long_command &
disown       # Détache du shell

# screen/tmux (préféré)
screen
# Lancer commandes
# Ctrl+A D (detach)
# Relancer: screen -r
```

---

### Question 32
**Réponse correcte : D (B et C en temps réel !)**

**Explication détaillée :**

**Méthode B - top (standard) :**
```bash
top
# Rafraîchit toutes les 3s (défaut)
# Interface interactive
# Affiche:
#   - Uptime, load average
#   - Tâches (running, sleeping, stopped, zombie)
#   - CPU usage (%us, %sy, %ni, %id, %wa)
#   - Mémoire (total, free, used, buff/cache)
#   - Liste processus triés

# Commandes interactives:
# q     Quitter
# k     Kill processus
# r     Renice processus
# M     Tri par mémoire
# P     Tri par CPU (défaut)
# 1     Toggle CPUs individuels
# u     Filtrer utilisateur
# c     Toggle commande complète
# V     Arbre processus
```

**Méthode C - htop (amélioré, si installé) :**
```bash
htop
# Plus moderne que top
# Fonctionnalités:
#   - Couleurs
#   - Support souris
#   - Barres visuelles CPU/mémoire
#   - Arbre processus natif
#   - Recherche interactive
#   - Setup menu (F2)

# Installation
sudo apt install htop    # Debian/Ubuntu
sudo yum install htop    # RHEL/CentOS
```

**Pourquoi A est incorrecte :**

- **A) `ps aux`** : **Snapshot statique** (un instant T, pas de rafraîchissement).
  ```bash
  ps aux    # Affiche une fois puis termine
  
  # Pour simuler rafraîchissement
  watch -n 1 'ps aux'    # Mais pas interactif
  ```

**Comparaison :**

| Aspect | ps aux | top | htop |
|--------|--------|-----|------|
| Rafraîchissement | ❌ Non | ✅ Oui (3s) | ✅ Oui (1s) |
| Interactif | ❌ Non | ✅ Oui | ✅ Oui |
| Couleurs | ❌ Non | Limité | ✅ Complet |
| Souris | ❌ Non | ❌ Non | ✅ Oui |
| Arbre | Avec -f | V key | ✅ Natif |
| Installation | ✅ Natif | ✅ Natif | Parfois requis |

**Options top :**
```bash
# Lancer top
top

# Refresh custom (2s)
top -d 2

# Batch mode (non-interactif, 1 fois)
top -b -n 1

# Utilisateur spécifique
top -u www-data

# PID spécifique
top -p 1234
top -p 1234,5678,9012    # Multiple PIDs

# Tri par mémoire au démarrage
top -o %MEM

# Log top dans fichier
top -b -n 1 > top_snapshot.txt
```

**Commandes interactives top :**
```bash
# Dans top:
h ou ?   Aide
q        Quitter
k        Kill processus (demande PID)
r        Renice (demande PID et nice value)
M        Tri par %MEM
P        Tri par %CPU
T        Tri par TIME+
u        Filtrer utilisateur
c        Toggle args complets
V        Arbre (forest mode)
1        Toggle CPUs individuels
d        Change delay (refresh)
W        Save config (~/.toprc)
```

**Ligne de statut top :**
```bash
top - 15:30:00 up 10 days,  5:23,  2 users,  load average: 0.50, 0.30, 0.20
Tasks: 180 total,   1 running, 179 sleeping,   0 stopped,   0 zombie
%Cpu(s): 10.5 us,  2.3 sy,  0.0 ni, 86.5 id,  0.5 wa,  0.0 hi,  0.2 si,  0.0 st
MiB Mem :  7842.1 total,  1234.5 free,  4567.8 used,  2039.8 buff/cache
MiB Swap:  2048.0 total,  2048.0 free,     0.0 used.  2876.3 avail Mem

# us: user space
# sy: system (kernel)
# ni: nice (low priority)
# id: idle
# wa: I/O wait
# hi: hardware interrupts
# si: software interrupts
# st: steal (virtual)
```

**htop avantages :**
```bash
# Barres visuelles
# [|||||||||||||||25.3%]  CPU 1
# [|||||          10.1%]  CPU 2

# [||||||||||||||||||||||||||3.2G/7.7G]  Memory

# Couleurs par type processus
# Vert  = user
# Rouge = kernel
# Bleu  = low priority

# Navigation souris
# Clic sur processus pour sélectionner
# Scroll wheel

# F-keys
# F1: Aide
# F2: Setup
# F3: Recherche
# F4: Filtrer
# F5: Arbre
# F6: Tri
# F9: Kill
# F10: Quit
```

**Alternatives :**
```bash
# atop (logging + replay)
atop
atop -r /var/log/atop/atop_20260128    # Replay log

# glances (Python, cross-platform)
glances

# nmon (performance)
nmon

# iotop (I/O monitoring)
iotop

# nethogs (network per-process)
nethogs
```

**Monitoring scriptable :**
```bash
# top batch pour scripts
top -b -n 1 | head -20

# Extraire données
top -b -n 1 | grep '%Cpu'
top -b -n 1 | awk 'NR>7 {print $1, $9, $12}'

# Watch custom command
watch -n 1 'ps aux --sort=-%cpu | head -10'
```

---

### Question 33
**Réponse correcte : D (B et C détachent !)**

**Explication détaillée :**

**Méthode B - nohup (no hangup) :**
```bash
nohup long_command &
# nohup: Ignore signal HUP (hangup)
# &: Background
# Output → nohup.out (défaut)

# Processus continue après:
# - Fermeture terminal
# - Déconnexion SSH
# - Logout

# Vérifier
tail -f nohup.out

# Custom output
nohup command > output.log 2>&1 &
```

**Méthode C - disown :**
```bash
# Lancer normalement
long_command &
[1] 12345

# Détacher du shell
disown %1
# Ou
disown    # Dernier job

# Maintenant, processus continue après logout
# Mais: pas de nohup.out (output perdu si pas redirigé)
```

**Pourquoi A est incorrecte seule :**

- **A) `command &`** : Lance en **background** mais **toujours attaché** au terminal.
  ```bash
  long_command &
  # Si terminal ferme → SIGHUP envoyé → processus tué
  
  # Vérifier
  jobs
  # [1]+ Running    long_command &
  
  # Exit → processus tué
  ```

**Comparaison méthodes :**

| Méthode | Survit logout | Output | Syntaxe |
|---------|---------------|--------|---------|
| `&` seul | ❌ Non | Terminal | Simple |
| `nohup &` | ✅ Oui | nohup.out | Avant lancement |
| `disown` | ✅ Oui | Perdu si non redirigé | Après lancement |
| `screen/tmux` | ✅ Oui | Dans session | Session persistante |

**nohup complet :**
```bash
# Syntaxe complète
nohup command > output.log 2>&1 &

# Exemples
nohup ./backup.sh &
nohup python3 server.py > server.log 2>&1 &
nohup make > build.log 2>&1 &

# Vérifier processus
ps aux | grep command

# Lire output temps réel
tail -f nohup.out
```

**disown complet :**
```bash
# Déjà lancé en background
long_command &
[1] 12345

# Détacher
disown %1
# Ou tous jobs
disown -a

# Vérifier (plus dans jobs)
jobs
# (vide)

# Mais toujours dans ps
ps -p 12345
```

**Workflow typique :**
```bash
# Si oublié nohup
command &    # Oops, pas de nohup

# Ctrl+Z (suspend)
^Z
[1]+ Stopped

# Background
bg %1

# Détacher
disown %1

# Maintenant OK pour logout
```

**screen et tmux (préférés) :**
```bash
# screen (session persistante)
screen
# Lancer commandes
long_command

# Détacher: Ctrl+A puis D
# Logout OK

# Reconnecter
screen -r

# tmux (moderne)
tmux
# Lancer commandes
long_command

# Détacher: Ctrl+B puis D
# Reconnecter
tmux attach
```

**Exemples pratiques :**
```bash
# Serveur web dév
nohup python3 -m http.server 8080 > server.log 2>&1 &

# Backup longue durée
nohup tar czf backup.tar.gz /data > backup.log 2>&1 &

# Compilation
nohup make -j8 > build.log 2>&1 &

# Script maintenance
nohup ./maintenance.sh > /var/log/maint.log 2>&1 &

# Monitoring continu
nohup watch -n 60 'df -h' > disk_monitor.log &
```

**Cron (alternative) :**
```bash
# Pour tâches récurrentes
# Détaché par nature
crontab -e
0 2 * * * /path/to/backup.sh

# One-shot avec at
echo "long_command" | at now + 1 minute
```

**Vérifier processus détachés :**
```bash
# Par utilisateur
ps -u $USER

# Sans terminal (TTY = ?)
ps aux | awk '$7 == "?"'

# Processus avec nohup dans nom
ps aux | grep nohup

# Tous background (STAT sans +)
ps aux | awk '$8 !~ /\+/'
```

**Systemd (services permanents) :**
```bash
# Pour vrais daemons
sudo systemctl start myapp
sudo systemctl enable myapp

# Créer unit file
cat > /etc/systemd/system/myapp.service << EOF
[Unit]
Description=My Application

[Service]
ExecStart=/path/to/myapp
Restart=always

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl start myapp
```

---

### Question 34
**Réponse correcte : B**

**Explication détaillée :**

La colonne **STAT** (status) indique l'état du processus :

```bash
ps aux
# USER  PID %CPU %MEM  VSZ  RSS TTY  STAT START  TIME COMMAND
# root    1  0.0  0.1 168888 9876 ?   Ss   15:00  0:02 /sbin/init
# www   123  0.5  2.3 456789 12345 ?  S    15:10  1:23 apache2
# user  456  1.2  0.5  12345  6789 pts R+   15:20  0:05 python
#                                     ││
#                                     │└─ modificateurs
#                                     └─ état principal
```

**États principaux :**
```bash
R    Running (en cours d'exécution)
S    Sleeping (interruptible) - en attente
D    Sleeping (uninterruptible) - I/O wait
T    Stopped (Ctrl+Z ou debugger)
Z    Zombie (terminé, attend parent)
I    Idle (kernel threads)
```

**Modificateurs :**
```bash
<    High priority (nice < 0)
N    Low priority (nice > 0)
L    Pages locked in memory
s    Session leader
l    Multi-threaded (has threads)
+    Foreground process group
```

**Exemples combinés :**
```bash
Ss    Sleeping, session leader (souvent init/systemd)
R+    Running, foreground
S<    Sleeping, high priority
Sl    Sleeping, multi-threaded
Z     Zombie
D     Uninterruptible sleep (I/O)
T     Stopped
```

**Pourquoi les autres sont incorrectes :**

- **A) %CPU** : **Pourcentage CPU** utilisé (pas état).
  ```bash
  %CPU
  0.5    Utilise 0.5% CPU
  100.0  Utilise 100% d'un core
  ```

- **C) TTY** : **Terminal** associé (pas état).
  ```bash
  TTY
  pts/0  Pseudo-terminal 0
  tty1   Console virtuelle 1
  ?      Pas de terminal (daemon)
  ```

- **D) TIME** : **Temps CPU cumulé** (pas état).
  ```bash
  TIME
  00:00:05  5 secondes CPU
  01:23:45  1h23m45s CPU
  ```

**Filtrer par état :**
```bash
# Running seulement
ps aux | awk '$8 ~ /R/'

# Sleeping
ps aux | awk '$8 ~ /S/'

# Zombies
ps aux | awk '$8 ~ /Z/'
ps aux | grep ' Z '

# Stopped
ps aux | awk '$8 ~ /T/'

# Uninterruptible sleep (I/O wait)
ps aux | awk '$8 ~ /D/'

# High priority
ps aux | awk '$8 ~ /</'

# Multi-threaded
ps aux | awk '$8 ~ /l/'
```

**Exemples pratiques :**
```bash
# Compter par état
echo "Running:"; ps aux | grep -c ' R'
echo "Sleeping:"; ps aux | grep -c ' S'
echo "Zombies:"; ps aux | grep -c ' Z'

# Processus problématiques
# Zombies (parent mort)
ps aux | awk '$8 ~ /Z/ {print $2, $11}'

# I/O wait (disque lent)
ps aux | awk '$8 ~ /D/ {print $2, $11}'

# Stopped (oubliés en Ctrl+Z)
ps aux | awk '$8 ~ /T/ {print $2, $11}'

# High priority (vérifier nice)
ps aux | awk '$8 ~ /</ {print $2, $18, $11}'
```

**États détaillés (man ps) :**
```bash
# man ps | grep -A 20 "PROCESS STATE CODES"

PROCESS STATE CODES
R  running or runnable (on run queue)
D  uninterruptible sleep (usually IO)
S  interruptible sleep (waiting for event)
T  stopped by job control signal
t  stopped by debugger during trace
Z  defunct ("zombie") process
X  dead (should never be seen)

<  high-priority (not nice)
N  low-priority (nice)
L  has pages locked into memory
s  is a session leader
l  is multi-threaded
+  is in the foreground process group
```

**Différence D vs S :**
```bash
# S (interruptible sleep)
# - Peut être interrompu par signal
# - Attente événement (réseau, timer, etc.)
# - Normal

# D (uninterruptible sleep)
# - NE peut PAS être interrompu
# - Attente I/O critique (disque, NFS)
# - Si bloqué longtemps = problème I/O
# - SIGKILL n'a pas d'effet !

# Vérifier
ps aux | awk '$8 ~ /D/ {print}'
# Si beaucoup en D → problème disque/NFS
```

**Zombies explication :**
```bash
# Processus zombie (Z):
# - Terminé mais pas nettoyé
# - Attend que parent lise exit status
# - Prend peu de ressources
# - Disparaît quand parent lit status

# Trouver zombies
ps aux | grep ' Z '

# Parent des zombies
ps -o pid,ppid,stat,cmd | grep Z

# Résoudre: tuer parent (ou attendre)
kill <PPID>
```

---

### Question 35
**Réponse correcte : D (Toutes fonctionnent !)**

**Explication détaillée :**

**Trois méthodes équivalentes pour SIGHUP :**

**Méthode A - Par numéro :**
```bash
kill -1 PID
# -1 = SIGHUP (signal numéro 1)

# Exemple
kill -1 1234
```

**Méthode B - Par nom :**
```bash
kill -HUP PID
kill -SIGHUP PID    # Aussi valide

# Exemple
kill -HUP 1234
```

**Méthode C - Par nom de processus :**
```bash
pkill -HUP processname

# Exemple
pkill -HUP nginx
pkill -HUP apache2
```

**Toutes équivalentes !** Choix selon contexte.

**SIGHUP (Hangup) - Usages :**
```bash
# 1. Reload configuration (sans redémarrer)
kill -HUP $(cat /var/run/nginx.pid)
pkill -HUP nginx
systemctl reload nginx    # Préféré

# 2. Forcer relecture fichiers
kill -HUP syslog_pid

# 3. Terminer sessions (origine: raccrochage terminal)
```

**Liste signaux :**
```bash
kill -l
# 1) SIGHUP       2) SIGINT       3) SIGQUIT
# 9) SIGKILL     15) SIGTERM     18) SIGCONT
# 19) SIGSTOP    20) SIGTSTP

# Ou
kill -L    # Format différent
```

**Signaux courants et usages :**
```bash
# HUP (1) - Hangup / Reload
kill -HUP nginx_pid
# → Nginx relit nginx.conf

# INT (2) - Interrupt (Ctrl+C)
kill -INT script_pid
# → Comme Ctrl+C

# QUIT (3) - Quit (Ctrl+\)
kill -QUIT process_pid
# → Terminer avec core dump

# KILL (9) - Force kill (NON capturable)
kill -9 stuck_pid
# → Terminaison immédiate brutale

# TERM (15) - Terminate (défaut)
kill process_pid
kill -15 process_pid
# → Terminaison propre

# STOP (19) - Pause (NON capturable)
kill -STOP process_pid
# → Fige processus

# CONT (18) - Continue
kill -CONT process_pid
# → Reprend après STOP

# TSTP (20) - Terminal Stop (Ctrl+Z, capturable)
kill -TSTP process_pid
# → Comme Ctrl+Z

# USR1 (10), USR2 (12) - User-defined
kill -USR1 process_pid
# → Défini par application
```

**Exemples services courants :**
```bash
# Nginx - reload config
pkill -HUP nginx
systemctl reload nginx
nginx -s reload

# Apache - reload
pkill -HUP apache2
systemctl reload apache2
apachectl graceful

# Syslog - rotate logs
pkill -HUP rsyslogd

# SSH - reload sshd_config
pkill -HUP sshd
systemctl reload sshd

# Postfix
postfix reload
pkill -HUP master
```

**Vérifier signal supporté :**
```bash
# Vérifier comportement dans man page
man nginx
# Chercher: "SIGNALS"

# Nginx signals:
# TERM, INT - fast shutdown
# QUIT - graceful shutdown
# HUP - reload configuration
# USR1 - reopen log files
# USR2 - upgrade executable
# WINCH - graceful shutdown of workers
```

**kill vs pkill vs killall :**
```bash
# kill - par PID
kill -HUP 1234

# pkill - par pattern de nom
pkill -HUP nginx
pkill -HUP -u www-data apache

# killall - par nom exact
killall -HUP nginx
killall -HUP -u username process
```

**Exemples pratiques :**
```bash
# Reload après changement config
vim /etc/nginx/nginx.conf
nginx -t    # Test config
pkill -HUP nginx

# Rotate logs (reopen)
mv /var/log/app.log /var/log/app.log.1
kill -HUP $(cat /var/run/app.pid)

# Reload multiple processus
for pid in $(pgrep worker); do
    kill -HUP $pid
done

# Avec vérification
if nginx -t; then
    pkill -HUP nginx && echo "Reloaded"
else
    echo "Config error"
fi
```

**Signal depuis systemd :**
```bash
# Reload (envoie SIGHUP)
systemctl reload nginx

# Kill custom signal
systemctl kill -s SIGUSR1 myapp

# Kill tous processus du service
systemctl kill myapp
```

**Capture signaux (script) :**
```bash
#!/bin/bash
# Intercepter SIGHUP

function reload_config() {
    echo "SIGHUP received, reloading..."
    # Code reload config
}

trap reload_config SIGHUP

while true; do
    # Main loop
    sleep 1
done

# Test:
# ./script.sh &
# kill -HUP $!
```

---

### Question 36
**Réponse correcte : D (B et C en temps réel !)**

**Explication détaillée :**

**Méthode B - top (interactif) :**
```bash
top
# Rafraîchit toutes les 3s (défaut)
# Ligne mémoire:
# MiB Mem :  7842.1 total,  1234.5 free,  4567.8 used,  2039.8 buff/cache
# MiB Swap:  2048.0 total,  2048.0 free,     0.0 used.  2876.3 avail Mem

# Tri par mémoire: touche M
# Processus par %MEM

# Options lancement
top -o %MEM    # Tri par mémoire
```

**Méthode C - vmstat (statistiques) :**
```bash
vmstat 2
# Rafraîchit toutes les 2s
# Colonnes mémoire:
# procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
#  r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
#  1  0      0 1234567 123456 234567   0    0     5    10  100  200  5  2 92  1  0

# swpd: swap used
# free: RAM libre
# buff: buffers
# cache: cache
# si: swap in (KB/s)
# so: swap out (KB/s)

# N mesures
vmstat 2 10    # 10 fois toutes les 2s
```

**Pourquoi A seule est incorrecte :**

- **A) `free -h`** : **Snapshot statique** (pas de rafraîchissement automatique).
  ```bash
  free -h
  #               total   used    free    shared  buff/cache  available
  # Mem:          7.7Gi   4.5Gi   1.2Gi   100Mi   2.0Gi       2.8Gi
  # Swap:         2.0Gi   0B      2.0Gi
  
  # Une mesure puis termine
  
  # Simuler rafraîchissement
  watch -n 1 'free -h'    # Mais pas vraiment "temps réel"
  free -s 2               # Rafraîchit toutes les 2s (option moins connue)
  ```

**Comparaison :**

| Commande | Temps réel | Interactif | Détail processus | Statistiques |
|----------|------------|------------|------------------|--------------|
| `free -h` | ❌ Non | ❌ Non | ❌ Non | ✅ Global |
| `top` | ✅ Oui | ✅ Oui | ✅ Oui | ✅ Par processus |
| `vmstat` | ✅ Oui | ❌ Non | ❌ Non | ✅ Système |
| `htop` | ✅ Oui | ✅ Oui | ✅ Oui | ✅ Visuel |

**free détails :**
```bash
# Format humain
free -h

# En MB
free -m

# En GB
free -g

# Avec total
free -h -t

# Wide (nombre au lieu de human)
free -w

# Rafraîchir (peu connu)
free -s 2    # Toutes les 2s

# Compter iterations
free -s 2 -c 10    # 10 fois toutes les 2s
```

**Colonnes free :**
```bash
#               total   used    free    shared  buff/cache  available
# total:       RAM installée
# used:        RAM utilisée (apps)
# free:        RAM complètement libre
# shared:      RAM partagée (tmpfs, etc.)
# buff/cache:  Buffers + cache disque
# available:   RAM disponible pour nouvelles apps (≠ free!)
#              = free + récupérable de cache

# IMPORTANT: available > free
# Cache peut être libéré si besoin
```

**vmstat détails :**
```bash
# Syntaxe
vmstat [delay] [count]

# Exemples
vmstat 1        # Toutes les secondes
vmstat 2 10     # 10 fois toutes les 2s
vmstat -a       # Active/inactive memory
vmstat -s       # Statistiques complètes
vmstat -d       # Disk statistics
vmstat -p sda1  # Partition statistics

# Colonnes importantes
# swpd:  Swap utilisé
# free:  RAM libre
# si:    Swap in (pages/s)
# so:    Swap out (pages/s)
# bi:    Blocks in (lecture disque)
# bo:    Blocks out (écriture disque)
```

**Monitoring mémoire complet :**
```bash
# Snapshot global
free -h

# Temps réel interactif (processus)
top
htop

# Temps réel statistiques
vmstat 2

# Détails mémoire
cat /proc/meminfo
# MemTotal:        8058880 kB
# MemFree:         1234567 kB
# MemAvailable:    3456789 kB
# Buffers:          123456 kB
# Cached:          2345678 kB
# SwapTotal:       2097148 kB
# SwapFree:        2097148 kB

# Par processus
ps aux --sort=-%mem | head -10
ps -eo pid,user,%mem,rss,cmd --sort=-%mem | head -10

# smem (si installé - mémoire proportionnelle)
smem -r
smem -u    # Par utilisateur
```

**Exemples pratiques :**
```bash
# Top 10 processus mémoire
ps aux --sort=-%mem | head -11

# Memory leak detection
watch -n 1 'ps aux --sort=-%mem | head -5'

# Swap usage par processus
for file in /proc/*/status; do
    awk '/^Name|VmSwap/{printf $2" "$3}END{print ""}' $file
done | grep -v " 0 kB" | sort -k 2 -n -r

# Vérifier si swap actif
free -h | grep Swap

# Clear cache (root)
sync
echo 3 > /proc/sys/vm/drop_caches
```

**Alertes mémoire :**
```bash
# Script monitoring
#!/bin/bash
THRESHOLD=80

while true; do
    MEM_USAGE=$(free | grep Mem | awk '{print int($3/$2 * 100)}')
    
    if [ $MEM_USAGE -gt $THRESHOLD ]; then
        echo "WARNING: Memory usage ${MEM_USAGE}%"
        # Alert action
    fi
    
    sleep 60
done

# Avec vmstat
vmstat 5 | awk '$5 < 102400 {print "Low memory:", $5}'
```

**Outils avancés :**
```bash
# sar (sysstat package)
sar -r 2 10    # Mémoire toutes les 2s, 10 fois

# dstat (combine vmstat/iostat/netstat)
dstat -m       # Memory only
dstat -tm      # Time + memory

# nmon (performance)
nmon
# Touche m pour memory
```

---

### Question 37
**Réponse correcte : B**

**Explication détaillée :**

La plage nice va de **-20 à +19** :

```bash
# Plage complète
-20  = Priorité MAXIMALE (le plus de CPU)
  0  = Priorité par défaut
+19  = Priorité MINIMALE (le moins de CPU)

# Règle inverse: Plus bas = Plus prioritaire
nice -20  → très prioritaire (beaucoup de CPU)
nice +19  → très peu prioritaire (peu de CPU)
```

**Permissions :**
```bash
# Utilisateur normal:
# - Peut SEULEMENT augmenter nice (0 à 19)
# - NE peut PAS diminuer (rendre plus prioritaire)

nice -n 5 command      # OK (user)
nice -n 10 command     # OK (user)

nice -n -5 command     # ERREUR (user)
# nice: cannot set niceness: Permission denied

# Root:
# - Peut utiliser TOUTE la plage (-20 à 19)
sudo nice -n -10 command    # OK (root)
sudo nice -n -20 command    # OK (root)
```

**Pourquoi les autres sont incorrectes :**

- **A) 0 à 19** : Plage **utilisateur normal** seulement (pas complète).

- **C) -10 à +10** : Plage incorrecte (trop limitée).

- **D) 1 à 100** : Confond avec **priorité (PRI)** de kernel (différent de nice).
  ```bash
  ps -eo pid,ni,pri,cmd
  # PID  NI PRI CMD
  # 1234  0  20 process
  #       └─ nice
  #          └─ priority (calculée: 20 + nice)
  ```

**Relation nice et priorité :**
```bash
# PRI (priority) = 20 + nice

nice -20 → PRI = 0   (max priorité)
nice   0 → PRI = 20  (défaut)
nice +19 → PRI = 39  (min priorité)

# Scheduler utilise PRI, pas nice
# Plus bas PRI = plus de CPU
```

**Vérifier nice :**
```bash
# Avec ps
ps -eo pid,ni,cmd
ps -l         # Inclut NI column
ps aux        # NI pas affiché par défaut

# Avec top
top
# Colonne NI

# Avec stat
stat /proc/PID/stat
```

**Exemples :**
```bash
# Lancer avec nice élevé (faible priorité)
nice -n 19 tar czf backup.tar.gz /data
# Minimal CPU (background task)

# Lancer avec nice bas (haute priorité - root)
sudo nice -n -10 important_task
# Maximum CPU

# Défaut (nice 0)
command
# Priorité normale

# Vérifier nice d'un processus
ps -o pid,ni,cmd -p 1234
```

---

### Question 38
**Réponse correcte : D (B et C fonctionnent !)**

**Explication détaillée :**

**renice** modifie nice d'un processus **existant** :

**Méthode B (syntaxe courte) :**
```bash
renice -n 5 PID
renice 5 PID    # -n optionnel

# Exemples
renice -n 10 1234
renice 15 5678
```

**Méthode C (syntaxe explicite) :**
```bash
renice -n 5 -p PID
# -p = process (explicite)

# Exemple
renice -n 10 -p 1234
```

**Les deux sont valides !** `-p` est optionnel mais plus clair.

**Pourquoi A est incorrecte :**

- **A) `nice -n 5 PID`** : **nice** lance NOUVEAU processus (pas modification existant).
  ```bash
  nice -n 5 command    # Lancer nouveau
  # PAS: nice -n 5 1234 (syntaxe invalide)
  ```

**Options renice :**
```bash
# Par PID
renice -n 10 -p 1234
renice 10 1234

# Par utilisateur (tous ses processus)
renice -n 5 -u username
renice 5 -u www-data

# Par groupe de processus
renice -n 10 -g 5678

# Multiple PIDs
renice -n 5 -p 1234 5678 9012

# Vérifier après
ps -o pid,ni,cmd -p 1234
```

**Permissions :**
```bash
# Utilisateur normal:
# - Peut SEULEMENT augmenter nice (rendre MOINS prioritaire)
# - Ses propres processus seulement

renice 10 1234    # OK si nice actuel < 10
renice 5 1234     # ERREUR si nice actuel > 5
# Permission denied

# Root:
# - Peut modifier n'importe quel processus
# - Peut augmenter OU diminuer nice

sudo renice -5 1234     # OK
sudo renice -20 5678    # OK (max priorité)
```

**Exemples pratiques :**
```bash
# Réduire priorité processus gourmand
renice 15 $(pgrep firefox)
renice 19 $(pgrep chrome)    # Minimal CPU

# Augmenter priorité processus important (root)
sudo renice -10 $(pgrep mysql)
sudo renice -15 $(pgrep nginx)

# Tous processus d'un utilisateur
renice 10 -u apache
sudo renice 5 -u www-data

# Dans top (interactif)
top
# Touche 'r'
# PID to renice: 1234
# Renice PID 1234 to value: 10
```

**Workflow typique :**
```bash
# 1. Identifier processus gourmand
top
ps aux --sort=-%cpu | head -10

# 2. Noter PID
PID=1234

# 3. Réduire priorité
renice 15 $PID

# 4. Vérifier
ps -o pid,ni,%cpu,cmd -p $PID
```

**Script renice automatique :**
```bash
#!/bin/bash
# Renice processus utilisant >50% CPU

ps aux | awk '$3 > 50 {print $2}' | while read pid; do
    echo "Renicing PID $pid"
    renice 10 $pid
done
```

**Différence nice vs renice :**

| Aspect | nice | renice |
|--------|------|--------|
| Usage | **Lancer** nouveau processus | **Modifier** processus existant |
| Syntaxe | `nice -n X command` | `renice -n X PID` |
| Cible | Commande à exécuter | PID existant |
| Exemple | `nice -n 10 tar czf...` | `renice 10 1234` |

**Avec top/htop :**
```bash
# top
top
# Touche 'r' (renice)
# Entrer PID
# Entrer nice value

# htop
htop
# F7/F8: Augmenter/Diminuer nice
# Ou sélectionner processus puis 'r'
```

**Renice récursif (tous enfants) :**
```bash
# Parent + enfants
pstree -p 1234 | grep -oP '\(\K[0-9]+' | xargs -I {} renice 10 {}

# Fonction
renice_tree() {
    local parent=$1
    local nice_val=$2
    
    for pid in $(pgrep -P $parent); do
        renice $nice_val $pid
        renice_tree $pid $nice_val
    done
    renice $nice_val $parent
}

renice_tree 1234 10
```

---

### Question 39
**Réponse correcte : C**

**Explication détaillée :**

Pour utilisateur normal, **nice maximum = +19** :

```bash
nice -n 19 command
# +19 = priorité MINIMALE
# Processus utilise le MOINS de CPU possible
# Idéal pour tâches background non urgentes

# Exemples
nice -n 19 tar czf backup.tar.gz /data
nice -n 19 find / -name "*.tmp" -delete
nice -n 19 ./long_computation.sh
```

**Pourquoi les autres sont incorrectes :**

- **A) `nice command`** : Nice **par défaut = +10** (pas maximum).
  ```bash
  nice command
  # Équivalent à: nice -n 10 command
  # Priorité réduite mais pas minimale
  ```

- **B) `nice -n 10 command`** : Nice 10 (moyen, pas maximum).

- **D) `nice -n 20 command`** : **Invalide** (max = 19, pas 20).
  ```bash
  nice -n 20 command
  # Erreur: nice: invalid adjustment '20'
  # Plage: -20 à +19
  ```

**Plage nice complète :**
```bash
# Utilisateur normal
nice -n 0  command     # Défaut (même que sans nice)
nice -n 5  command     # Légèrement réduit
nice -n 10 command     # Défaut de 'nice' seul
nice -n 15 command     # Très réduit
nice -n 19 command     # MINIMAL (le plus bas possible)

nice -n -5 command     # ERREUR (permission denied)

# Root
sudo nice -n -20 command    # MAXIMAL (le plus haut possible)
sudo nice -n -10 command    # Très haute priorité
sudo nice -n 0   command    # Défaut
sudo nice -n 19  command    # Minimal
```

**Cas d'usage nice 19 :**
```bash
# Backup (pas urgent)
nice -n 19 tar czf /backup/full-$(date +%Y%m%d).tar.gz /data

# Indexation (background)
nice -n 19 updatedb

# Compression massive
nice -n 19 find /data -name "*.log" -exec gzip {} \;

# Calculs scientifiques (batch)
nice -n 19 ./simulation --iterations 1000000

# Scan antivirus
nice -n 19 clamscan -r /home

# Nettoyage fichiers temp
nice -n 19 find /tmp -mtime +7 -delete
```

**Vérifier nice appliqué :**
```bash
# Lancer
nice -n 19 sleep 1000 &
[1] 12345

# Vérifier
ps -o pid,ni,cmd -p 12345
#   PID  NI CMD
# 12345  19 sleep 1000

# Avec ps aux
ps aux | grep sleep
# user 12345 ... 19 ... sleep 1000
```

**Impact nice sur CPU :**
```bash
# Sans nice (priorité normale)
./cpu_intensive &
# Utilise ~100% CPU si disponible

# Avec nice 19 (priorité minimale)
nice -n 19 ./cpu_intensive &
# Utilise CPU seulement si personne d'autre n'en a besoin
# Si autre processus veut CPU, il est prioritaire
```

**Exemples pratiques :**
```bash
# Compilation non urgente
nice -n 19 make -j$(nproc)

# Encodage vidéo (long)
nice -n 19 ffmpeg -i input.mp4 -c:v h264 output.mp4

# Download + compression
nice -n 19 wget https://example.com/bigfile.tar.gz
nice -n 19 tar xzf bigfile.tar.gz

# Script maintenance
nice -n 19 ./cleanup_old_logs.sh

# Génération rapports
nice -n 19 ./generate_monthly_report.sh
```

**Nice avec ionice (I/O priority) :**
```bash
# CPU + I/O low priority
nice -n 19 ionice -c 3 tar czf backup.tar.gz /data

# ionice classes:
# -c 1: Realtime (root only)
# -c 2: Best-effort (défaut)
# -c 3: Idle (I/O seulement si disque inactif)
```

**Comparaison valeurs nice :**

| Nice | Priorité | Usage | Permissions |
|------|----------|-------|-------------|
| -20 | Maximale | Processus critiques | Root seulement |
| -10 | Très haute | Services importants | Root seulement |
| 0 | Normale | Défaut | Tous |
| 10 | Réduite | Défaut `nice` | Tous |
| 19 | **Minimale** | **Background tasks** | **Tous** |

**Forcer nice minimum (cron) :**
```bash
# Crontab
0 2 * * * nice -n 19 /backup/script.sh

# Systemd service
[Service]
ExecStart=/usr/bin/backup
Nice=19
```

**Modifier nice après lancement :**
```bash
# Lancer sans nice (oops)
./long_process &
[1] 12345

# Réduire priorité après
renice 19 12345

# Vérifier
ps -o pid,ni,cmd -p 12345
```

---

### Question 40
**Réponse correcte : C**

**Explication détaillée :**

Utilisateur normal **NE PEUT JAMAIS** augmenter priorité (diminuer nice) :

```bash
# Scénario
nice -n 10 sleep 1000 &
[1] 12345

# Essayer augmenter priorité (diminuer nice à 5)
renice 5 12345
# renice: failed to set priority for 12345 (process ID): Permission denied

# Raison: sécurité
# Empêcher utilisateur d'accaparer CPU
```

**Règle utilisateur normal :**
```bash
# AUTORISÉ: Augmenter nice (diminuer priorité)
nice 10 → renice 15    ✅ OK
nice 10 → renice 19    ✅ OK

# INTERDIT: Diminuer nice (augmenter priorité)
nice 10 → renice 5     ❌ Permission denied
nice 10 → renice 0     ❌ Permission denied
nice 10 → renice -5    ❌ Permission denied
```

**Pourquoi C est correcte :**

Utilisateur peut **seulement** rendre ses processus **MOINS prioritaires** :
- Empêche accaparement ressources
- Sécurité multi-utilisateurs
- Fair scheduling

**Pourquoi les autres sont incorrectes :**

- **A) Oui, toujours** : Faux, jamais pour utilisateur normal.

- **B) Oui, mais seulement jusqu'à nice 0** : Faux, aucune augmentation possible.

**Tableau permissions :**

| Action | User Normal | Root |
|--------|-------------|------|
| Augmenter nice (diminuer priorité) | ✅ Oui | ✅ Oui |
| Diminuer nice (augmenter priorité) | ❌ Non | ✅ Oui |
| Nice négatif | ❌ Non | ✅ Oui |
| Processus d'autres users | ❌ Non | ✅ Oui |

**Exemples concrets :**
```bash
# Utilisateur lance processus
nice -n 5 ./myapp &
[1] 12345

# Peut réduire priorité (augmenter nice)
renice 10 12345    ✅ OK
renice 15 12345    ✅ OK
renice 19 12345    ✅ OK

# NE peut PAS augmenter priorité (diminuer nice)
renice 0 12345     ❌ Permission denied
renice -5 12345    ❌ Permission denied

# Root peut tout
sudo renice -10 12345    ✅ OK
sudo renice 0 12345      ✅ OK
```

**Vérifier limites :**
```bash
# Limite nice utilisateur
ulimit -e
# Affiche nice limit (souvent 0)

# /etc/security/limits.conf
cat /etc/security/limits.conf
# username  hard  nice  0
# username  soft  nice  0
```

**Workflow utilisateur :**
```bash
# 1. Lancer processus (oublié nice)
./long_task &
[1] 12345

# 2. Réaliser qu'il consomme trop
top    # 95% CPU !

# 3. Réduire priorité (OK)
renice 15 12345    ✅ Fonctionne

# 4. Trop réduit, vouloir augmenter
renice 10 12345    ❌ Permission denied

# 5. Solution: relancer avec bon nice
kill 12345
nice -n 10 ./long_task &
```

**Cas root :**
```bash
# Root peut tout modifier
sudo renice -20 1234    # Max priorité
sudo renice -10 5678    # Haute priorité
sudo renice 0 9012      # Normale
sudo renice 19 1111     # Min priorité

# Root peut modifier processus de n'importe qui
sudo renice 10 -u www-data    # Tous processus www-data
```

**Raison sécurité :**
```bash
# Sans restriction:
# Utilisateur malveillant pourrait:
# 1. Lancer processus nice 19 (minimal)
# 2. Puis renice à -20 (maximal)
# → Accaparer tout le CPU
# → Déni de service

# Avec restriction actuelle:
# Utilisateur peut seulement RÉDUIRE impact
# → Sécurité préservée
```

**Alternative: limites PAM :**
```bash
# /etc/security/limits.conf
# Autoriser certains users à nice négatif

@admins  hard  nice  -10
@admins  soft  nice  -10

# Groupe admins peut alors:
renice -5 processus    # OK pour membres @admins
```

**Systemd (root équivalent) :**
```bash
# Service avec haute priorité
[Service]
ExecStart=/usr/bin/myapp
Nice=-10    # Haute priorité (root via systemd)

# User service (user permissions)
systemctl --user start myapp
# → soumis aux mêmes restrictions nice
```

---

### Question 41
**Réponse correcte : B**

**Explication détaillée :**

`grep -i` (insensitive) ignore la casse :

```bash
grep -i "error" file.log
# Trouve: error, Error, ERROR, ErRoR, etc.

# Sans -i (sensible casse)
grep "error" file.log
# Trouve seulement: error

# Exemple fichier
cat file.txt
# Error in line 1
# error in line 2
# ERROR in line 3
# ErRoR in line 4

grep -i "error" file.txt
# (Toutes les 4 lignes)

grep "error" file.txt
# error in line 2 (seulement)
```

**Pourquoi les autres sont incorrectes :**

- **A) `grep word file.txt`** : Recherche **sensible casse** (défaut).

- **C) `grep -v word file.txt`** : **Inverse** (lignes NE contenant PAS "word").
  ```bash
  grep -v "error" file.log
  # Lignes SANS "error"
  ```

- **D) `grep -c word file.txt`** : **Compte** lignes contenant "word".
  ```bash
  grep -c "error" file.log
  # 42 (nombre de lignes, pas les lignes elles-mêmes)
  ```

**Options grep courantes :**
```bash
# Ignorer casse
grep -i "pattern" file

# Inverser (lignes sans pattern)
grep -v "pattern" file

# Compter lignes
grep -c "pattern" file

# Numéros de lignes
grep -n "pattern" file

# Fichiers contenant pattern
grep -l "pattern" *.txt

# Récursif
grep -r "pattern" /path

# Extended regex
grep -E "pattern1|pattern2" file

# Mot entier
grep -w "word" file

# Ligne exacte
grep -x "exact line" file

# Contexte (lignes avant/après)
grep -A 3 "pattern" file    # 3 lignes après
grep -B 2 "pattern" file    # 2 lignes avant
grep -C 2 "pattern" file    # 2 lignes avant ET après
```

**Exemples pratiques -i :**
```bash
# Logs (ERROR, error, Error)
grep -i "error" /var/log/syslog

# Recherche utilisateur
grep -i "john" /etc/passwd

# Recherche extension (case-insensitive)
grep -i ".pdf" file_list.txt
# Trouve: .pdf, .PDF, .Pdf

# Multiple mots
grep -i -E "error|warning|critical" app.log

# Avec contexte
grep -i -A 5 "exception" app.log
# Exception + 5 lignes suivantes
```

**Combiner options :**
```bash
# Insensitive + numéros lignes
grep -in "error" file.log

# Insensitive + compte
grep -ic "error" file.log

# Insensitive + récursif
grep -ir "todo" /project/src

# Insensitive + fichiers seulement
grep -il "copyright" *.txt

# Insensitive + inverser
grep -iv "debug" app.log    # Lignes sans debug (casse ignorée)

# Insensitive + mot entier
grep -iw "error" file.log   # Pas "errors", "erreur"

# Insensitive + contexte
grep -i -C 3 "critical" syslog
```

**Regex avec -i :**
```bash
# Classes caractères
grep -i "[a-z]" file    # a-z ET A-Z

# Pattern complexe
grep -i -E "^(error|warning)" log
# ^ERROR, ^error, ^Warning, etc.

# IP addresses (insensible nombres)
grep -i "[0-9]{1,3}\.[0-9]{1,3}" file
```

**Performance :**
```bash
# -i légèrement plus lent
time grep "error" huge.log
# 0.5s

time grep -i "error" huge.log
# 0.6s (comparaison supplémentaire)

# Négligeable sauf fichiers énormes
```

**Alternatives :**
```bash
# awk (case-insensitive)
awk 'tolower($0) ~ /error/' file

# sed
sed -n '/error/Ip' file    # Imprimer lignes (case-insensitive)

# grep avec pattern
grep -E "[Ee][Rr][Rr][Oo][Rr]" file
# Équivalent mais lourd
```

**Scripts :**
```bash
# Fonction recherche flexible
search() {
    local pattern="$1"
    local file="$2"
    
    grep -in "$pattern" "$file"
}

search "error" /var/log/syslog

# Recherche multiple fichiers
for file in *.log; do
    echo "=== $file ==="
    grep -i "error" "$file"
done
```

---

### Question 42
**Réponse correcte : B**

**Explication détaillée :**

`^` (caret) = **ancre début de ligne** :

```bash
grep "^Error" file.log
# Trouve lignes COMMENÇANT par "Error"

# Exemple fichier
cat file.txt
# Error: Something failed
# Warning: Error detected
# Error in module X
# No problems here

grep "^Error" file.txt
# Error: Something failed
# Error in module X
# (seulement lignes COMMENÇANT par Error)

grep "Error" file.txt
# Error: Something failed
# Warning: Error detected    ← aussi (Error au milieu)
# Error in module X
```

**Pourquoi les autres sont incorrectes :**

- **A) `grep "Error" file`** : Trouve Error **n'importe où** dans la ligne.

- **C) `grep "$Error" file`** : **Invalide**. `$` seul = fin de ligne (pas préfixe variable).
  ```bash
  grep "$Error" file
  # Cherche chaîne littérale "$Error" (probablement rien)
  ```

- **D) `grep "Error$" file`** : Trouve lignes **FINISSANT** par "Error".
  ```bash
  grep "Error$" file
  # Something failed: Error
  # Critical Error
  # (lignes se terminant par Error)
  ```

**Ancres importantes :**
```bash
^     Début de ligne
$     Fin de ligne
\b    Bordure de mot (word boundary)
\B    Pas bordure de mot

# Exemples
grep "^Error"     # Commence par Error
grep "Error$"     # Finit par Error
grep "^Error$"    # Ligne exacte "Error"
grep "\bError\b"  # "Error" comme mot entier
```

**Exemples pratiques :**
```bash
# Logs commençant par timestamp
grep "^2026-01-" app.log

# Commentaires (commencent par #)
grep "^#" script.sh

# Lignes vides
grep "^$" file.txt

# Lignes NON vides
grep -v "^$" file.txt

# Commandes bash (commencent par $)
grep "^$ " history.txt

# Erreurs en début de ligne
grep -E "^(ERROR|CRITICAL)" syslog
```

**Combinaisons :**
```bash
# Commence par Error ou Warning
grep -E "^(Error|Warning)" log

# Commence par nombre
grep "^[0-9]" file

# Commence par lettre majuscule
grep "^[A-Z]" file

# Ne commence PAS par #
grep -v "^#" config

# Commence par au moins 3 espaces (indentation)
grep "^   " code.py

# Ligne exacte
grep "^exact line$" file
```

**Différences début vs n'importe où :**
```bash
# Fichier exemple
cat log.txt
# 2026-01-28 10:00 ERROR: Failed
# ERROR: Database connection lost
# Warning: ERROR in module
# System is OK

# N'importe où (4 lignes)
grep "ERROR" log.txt
# (toutes les 4)

# Début seulement (2 lignes)
grep "^ERROR" log.txt
# ERROR: Database connection lost
# (seulement ligne commençant par ERROR)

# Début avec timestamp
grep "^2026.*ERROR" log.txt
# 2026-01-28 10:00 ERROR: Failed
```

**Ancres multiples :**
```bash
# Ligne exacte "ERROR"
grep "^ERROR$" file

# Mot Error en début
grep "^Error\b" file

# Pattern au début ET à la fin
grep "^Error.*failed$" log
# Error: operation failed
```

**Négation :**
```bash
# Lignes NE commençant PAS par #
grep -v "^#" script.sh

# Lignes NE finissant PAS par ;
grep -v ";$" code.js

# Lignes non vides (NE commence PAS immédiatement par fin)
grep -v "^$" file
```

**sed avec ancres :**
```bash
# Supprimer lignes commençant par #
sed '/^#/d' file

# Ajouter # en début de ligne
sed 's/^/# /' file

# Supprimer espaces en début de ligne
sed 's/^ *//' file
```

**awk avec ancres :**
```bash
# Lignes commençant par Error
awk '/^Error/' file

# Lignes finissant par Error
awk '/Error$/' file

# Pattern début
awk '/^[0-9]/{print "Starts with digit: " $0}' file
```

---

### Question 43
**Réponse correcte : D (B et C fonctionnent !)**

**Explication détaillée :**

**Méthode B - grep -E (extended regex) :**
```bash
grep -E "error|warning" file.log
# | = OU (alternation)
# Trouve lignes avec "error" OU "warning"

# Exemple
cat file.txt
# Error detected
# Warning: low memory
# Info: system OK
# Critical error
# Warning level high

grep -E "error|warning" file.txt
# Error detected
# Warning: low memory
# Critical error
# Warning level high
# (4 lignes)
```

**Méthode C - egrep (équivalent) :**
```bash
egrep "error|warning" file.log
# egrep = grep -E (alias)
# Même résultat

# Note: egrep deprecated (utiliser grep -E)
```

**Pourquoi A est incorrecte :**

- **A) `grep "error warning" file`** : Cherche chaîne **littérale** "error warning" (les deux mots ensemble, pas OU).
  ```bash
  grep "error warning" file
  # Trouve seulement: "error warning" (exact)
  # Pas "error" seul ou "warning" seul
  ```

**Basic vs Extended regex :**
```bash
# Basic regex (grep défaut)
grep "error"          # Littéral
grep "error\|warning" # OU (| doit être échappé)

# Extended regex (grep -E ou egrep)
grep -E "error|warning"    # OU (| pas échappé)
grep -E "(error|warning)"  # Groupé

# Extended préféré pour lisibilité
```

**Alternation multiple :**
```bash
# 3 patterns
grep -E "error|warning|critical" file

# Avec insensitive
grep -Ei "error|warning|critical" file

# Avec ancres
grep -E "^(error|warning)" file    # Début ligne

# Avec contexte
grep -E -A 3 "error|warning" file  # + 3 lignes après
```

**Exemples pratiques :**
```bash
# Logs multiples niveaux
grep -Ei "error|warning|critical|fatal" /var/log/syslog

# Extensions fichiers
grep -E "\.(jpg|png|gif)$" filelist.txt

# Protocoles
grep -E "http|https|ftp" urls.txt

# Status codes
grep -E "(200|404|500)" access.log

# Adresses emails domaines
grep -E "@(gmail|yahoo|hotmail)\.com" users.txt
```

**Groupes et alternation :**
```bash
# Grouper pattern
grep -E "(error|warning): [0-9]+" log
# error: 123
# warning: 456

# Préfixe commun
grep -E "server (start|stop|restart)" log

# Suffixe commun
grep -E "(before|after) backup" log
```

**Négation avec alternation :**
```bash
# Lignes SANS error OU warning
grep -vE "error|warning" file

# NI error NI warning
grep -vE "error|warning|critical" log
```

**Alternatives méthodes :**
```bash
# grep basique (échapper |)
grep "error\|warning" file

# Multiple grep (pipe)
grep "error" file | grep -v "debug"
grep -E "error|warning" file | grep -v "debug"

# awk
awk '/error|warning/' file

# sed
sed -n '/error\|warning/p' file
```

**Performances :**
```bash
# grep -E optimisé
time grep -E "error|warning" huge.log

# Multiple grep (moins efficace)
time grep -e error -e warning huge.log

# Différence négligeable fichiers moyens
```

**Regex complexe :**
```bash
# IP OU hostname
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}|[a-z]+\.com" file

# Email OU URL
grep -E "[a-z]+@[a-z]+\.[a-z]+|https?://[^ ]+" file

# Multiple conditions
grep -E "^(ERROR|WARN).*database.*connection" log
```

**Scripts :**
```bash
#!/bin/bash
# Chercher patterns multiples

PATTERNS="error|warning|critical"
LOG_FILE="/var/log/app.log"

grep -Ei "$PATTERNS" "$LOG_FILE" | while read line; do
    echo "[ALERT] $line"
done

# Compter par type
echo "Errors: $(grep -ci "error" "$LOG_FILE")"
echo "Warnings: $(grep -ci "warning" "$LOG_FILE")"
```

---

### Question 44
**Réponse correcte : D (Toutes fonctionnent avec différences !)**

**Explication détaillée :**

**Méthode A - Première occurrence par ligne :**
```bash
sed 's/old/new/' file
# s/old/new/ = substitute
# Remplace PREMIÈRE occurrence par ligne
# Affiche résultat (fichier inchangé)

# Exemple
echo "old text old" | sed 's/old/new/'
# new text old (première seulement)
```

**Méthode B - Toutes occurrences :**
```bash
sed 's/old/new/g' file
# g = global (toutes occurrences)
# Remplace TOUTES occurrences par ligne
# Affiche résultat (fichier inchangé)

# Exemple
echo "old text old" | sed 's/old/new/g'
# new text new (toutes)
```

**Méthode C - Modification en place :**
```bash
sed -i 's/old/new/g' file
# -i = in-place (modifie fichier directement)
# Toutes occurrences
# FICHIER MODIFIÉ

# Avec backup
sed -i.bak 's/old/new/g' file
# Crée file.bak (original)
# file modifié
```

**Différences résumées :**

| Commande | Occurrences | Modifie fichier | Affiche |
|----------|-------------|-----------------|---------|
| `sed 's/old/new/' file` | 1ère par ligne | ❌ Non | ✅ Oui |
| `sed 's/old/new/g' file` | Toutes | ❌ Non | ✅ Oui |
| `sed -i 's/old/new/g' file` | Toutes | ✅ **Oui** | ❌ Non |

**Exemples pratiques :**
```bash
# Fichier test
cat file.txt
# The old old house
# old car old bike

# Première occurrence
sed 's/old/new/' file.txt
# The new old house
# new car old bike

# Toutes occurrences
sed 's/old/new/g' file.txt
# The new new house
# new car new bike

# Modifier fichier
sed -i 's/old/new/g' file.txt
cat file.txt
# The new new house
# new car new bike
```

**Options sed courantes :**
```bash
# Backup avant modif
sed -i.bak 's/old/new/g' file
ls
# file file.bak

# Afficher seulement lignes modifiées
sed -n 's/old/new/gp' file

# Case-insensitive
sed 's/old/new/gi' file

# Seulement ligne N
sed '5s/old/new/' file

# Lignes N à M
sed '10,20s/old/new/g' file

# Lignes avec pattern
sed '/error/s/old/new/g' file

# Multiples substitutions
sed -e 's/old/new/g' -e 's/foo/bar/g' file
sed 's/old/new/g; s/foo/bar/g' file
```

**Caractères spéciaux :**
```bash
# Échapper / (utiliser autre délimiteur)
sed 's/\/usr\/local/\/opt/g' file
# Ou
sed 's|/usr/local|/opt|g' file    # | comme délimiteur

# Échapper .
sed 's/file\.txt/file.log/g' file

# Variable
OLD="text"
NEW="replacement"
sed "s/$OLD/$NEW/g" file    # Double quotes !
```

**Référence arrière :**
```bash
# Capturer groupe ()
sed 's/\(.*\)@.*/\1/' emails.txt
# user@domain.com → user

# Multiples groupes
sed 's/\([0-9]*\)-\([0-9]*\)/\2-\1/' file
# 123-456 → 456-123

# Regex étendue
sed -E 's/([0-9]+)-([0-9]+)/\2-\1/' file
```

**Exemples fichiers config :**
```bash
# Changer port
sed -i 's/port = 8080/port = 9000/g' config.ini

# Activer option (décommenter)
sed -i 's/^# *\(option.*\)/\1/' config.conf

# Désactiver (commenter)
sed -i 's/^option/# option/' config.conf

# Changer IP
sed -i 's/192\.168\.1\.1/10.0.0.1/g' network.conf

# Variables environnement
sed -i 's/^DB_HOST=.*/DB_HOST=localhost/' .env
```

**Suppression (bonus) :**
```bash
# Supprimer lignes
sed '/pattern/d' file    # Lignes avec pattern
sed '5d' file            # Ligne 5
sed '10,20d' file        # Lignes 10-20
sed '/^$/d' file         # Lignes vides
sed '/^#/d' file         # Commentaires
```

**Scripts avancés :**
```bash
#!/bin/bash
# Remplacements multiples

sed -i \
  -e 's/old1/new1/g' \
  -e 's/old2/new2/g' \
  -e 's/old3/new3/g' \
  file.txt

# Avec vérification
if sed -i.bak 's/old/new/g' file.txt; then
    echo "Remplacement réussi"
    diff file.txt.bak file.txt
else
    echo "Erreur"
    mv file.txt.bak file.txt  # Restaurer
fi
```

---

### Question 45
**Réponse correcte : D (B et C fonctionnent, C meilleur !)**

**Explication détaillée :**

**Méthode B - Pattern basique :**
```bash
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" file

# Décomposition:
# [0-9]{1,3}  : 1 à 3 chiffres
# \.          : Point littéral (échappé)
# {3}         : Répéter 3 fois le groupe
# [0-9]{1,3}  : Dernier octet

# Trouve:
# 192.168.1.1     ✓
# 10.0.0.255      ✓
# 999.999.999.999 ✓ (invalide mais trouvé)
```

**Méthode C - Avec word boundaries (meilleur) :**
```bash
grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" file

# \b = word boundary
# Évite matchs partiels

# Trouve:
# 192.168.1.1     ✓
# 10.0.0.255      ✓

# Ne trouve PAS:
# abc192.168.1.1xyz  ✗ (entouré de lettres)
# 1192.168.1.1       ✗ (chiffre avant)
```

**Pourquoi A est insuffisante :**

- **A) `grep "[0-9]\.[0-9]\.[0-9]\.[0-9]" file`** : Trouve **1 seul chiffre** par octet.
  ```bash
  # Trouve:
  # 1.2.3.4  ✓
  
  # Ne trouve PAS:
  # 192.168.1.1  ✗ (> 1 chiffre par octet)
  # 10.0.0.255   ✗
  ```

**Validation complète (ranges 0-255) :**
```bash
# Regex complexe (valide vraiment)
grep -E "\b(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\b" file

# Décomposition par octet:
# 25[0-5]          : 250-255
# 2[0-4][0-9]      : 200-249
# [01]?[0-9][0-9]? : 0-199

# Valide:
# 192.168.1.1    ✓
# 255.255.255.0  ✓
# 10.0.0.1       ✓

# Invalide (pas trouvé):
# 256.1.1.1      ✗
# 999.999.999.999 ✗
```

**Exemples pratiques :**
```bash
# Simple (exam LPIC-1)
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" network.conf

# Avec boundaries
grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" file

# Extraire IPs d'un log
grep -Eo "([0-9]{1,3}\.){3}[0-9]{1,3}" access.log
# -o: seulement match (pas ligne entière)

# IPs uniques
grep -Eo "([0-9]{1,3}\.){3}[0-9]{1,3}" log | sort -u

# Compter occurrences
grep -Eo "([0-9]{1,3}\.){3}[0-9]{1,3}" log | sort | uniq -c
```

**Fichier exemple :**
```bash
cat network.txt
# Server IP: 192.168.1.100
# Gateway: 10.0.0.1
# DNS1: 8.8.8.8
# DNS2: 8.8.4.4
# Invalid: 999.999.999.999
# Port: 8080 (not IP)

grep -Eo "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" network.txt
# 192.168.1.100
# 10.0.0.1
# 8.8.8.8
# 8.8.4.4
# 999.999.999.999 (invalide mais trouvé)
```

**Autres patterns réseau :**
```bash
# IPv6 (simplifié)
grep -E "([0-9a-f]{1,4}:){7}[0-9a-f]{1,4}" file

# MAC address
grep -E "([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}" file

# CIDR notation
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}/[0-9]{1,2}" file
# 192.168.1.0/24

# Port avec IP
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}:[0-9]{1,5}" file
# 192.168.1.1:8080
```

**sed/awk avec IP :**
```bash
# Remplacer IPs
sed -E 's/([0-9]{1,3}\.){3}[0-9]{1,3}/X.X.X.X/g' log

# Extraire avec awk
awk 'match($0, /([0-9]{1,3}\.){3}[0-9]{1,3}/) {print substr($0, RSTART, RLENGTH)}' file
```

**Script validation :**
```bash
#!/bin/bash
# Valider IP (avec ranges)

validate_ip() {
    local ip=$1
    
    # Regex complète
    if echo "$ip" | grep -qE "^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$"; then
        echo "Valid IP: $ip"
    else
        echo "Invalid IP: $ip"
    fi
}

validate_ip "192.168.1.1"    # Valid
validate_ip "256.1.1.1"      # Invalid
validate_ip "10.0.0.999"     # Invalid
```

---

### Question 46
**Réponse correcte : D (B et C fonctionnent !)**

**Explication détaillée :**

**Méthode B - Word boundaries \b :**
```bash
grep "\btest\b" file
# \b = word boundary (limite de mot)
# Trouve "test" comme mot complet

# Trouve:
# test            ✓
# test.           ✓
# (test)          ✓
# "test"          ✓

# Ne trouve PAS:
# testing         ✗
# attest          ✗
# latest          ✗
```

**Méthode C - Option -w (word) :**
```bash
grep -w "test" file
# -w = whole word
# Équivalent à \b...\b

# Même comportement que B
```

**Pourquoi A est incorrecte :**

- **A) `grep "test" file`** : Trouve "test" **n'importe où** (même dans d'autres mots).
  ```bash
  grep "test" file
  # Trouve:
  # test       ✓
  # testing    ✓ (contient "test")
  # attest     ✓ (contient "test")
  # latest     ✓ (contient "test")
  ```

**Exemples fichier :**
```bash
cat file.txt
# This is a test
# testing phase
# attest the results
# latest version
# re-test tomorrow

# N'importe où
grep "test" file.txt
# (toutes les 5 lignes)

# Mot entier (-w)
grep -w "test" file.txt
# This is a test
# re-test tomorrow
# (2 lignes seulement)

# Mot entier (\b)
grep "\btest\b" file.txt
# This is a test
# re-test tomorrow
# (2 lignes)
```

**Word boundary expliqué :**
```bash
# \b = transition entre:
#   - \w (word char: [a-zA-Z0-9_])
#   - \W (non-word char: espaces, ponctuation)

# Exemples boundaries:
" test "    \b avant et après
"test."     \b avant et après
"(test)"    \b avant et après
"re-test"   \b avant "test" (- est non-word)
"test123"   PAS de \b après (3 est word char)
```

**Cas particuliers :**
```bash
# Tiret crée boundary
echo "re-test" | grep -w "test"
# re-test (trouvé)

# Underscore PAS boundary (word char)
echo "test_case" | grep -w "test"
# (pas trouvé, test_case est UN mot)

# Chiffres = word chars
echo "test123" | grep -w "test"
# (pas trouvé, test123 est UN mot)

echo "test 123" | grep -w "test"
# test 123 (trouvé, espace fait boundary)
```

**Exemples pratiques :**
```bash
# Chercher variable "id" (pas "void", "uid", etc.)
grep -w "id" code.js

# Chercher commande "cp" (pas "scp", "cpuinfo")
ps aux | grep -w "cp"

# Chercher mot "error" exact
grep -w -i "error" log
# Pas "errors", "error_code", etc.

# Multiple mots entiers
grep -wE "error|warning|critical" log

# Mot entier au début ligne
grep "^\btest\b" file
grep -w "^test" file
```

**Différence avec regex :**
```bash
# Avec boundaries explicites
grep "^test$" file          # Ligne EXACTE "test"
grep "\btest\b" file        # Mot "test" (n'importe où ligne)
grep "^test\b" file         # Mot "test" début ligne
grep "\btest$" file         # Mot "test" fin ligne

# -w équivalent \b
grep -w "test" file
# = grep "\btest\b" file
```

**sed et awk :**
```bash
# sed avec word boundaries
sed 's/\btest\b/exam/g' file

# awk
awk '/\btest\b/' file

# awk with -W (GNU awk)
awk '$0 ~ /\<test\>/' file
# \< \> = word boundaries (alternative)
```

**Négation :**
```bash
# Lignes SANS mot "test"
grep -vw "test" file

# Lignes avec "test" mais pas comme mot entier
grep "test" file | grep -vw "test"
```

**Performances :**
```bash
# -w plus rapide que \b
time grep -w "test" huge.log
# 0.5s

time grep "\btest\b" huge.log
# 0.5s (similaire)

# Différence négligeable
```

**Cas complexes :**
```bash
# Mots avec apostrophes
echo "don't test" | grep -w "test"
# don't test (trouvé, ' est non-word)

# CamelCase
echo "testCase" | grep -w "test"
# (pas trouvé, testCase est UN mot)

# Accents (dépend locale)
echo "testé" | grep -w "test"
# (dépend si é est word char)
```

---

### Question 47
**Réponse correcte : D (A et B fonctionnent !)**

**Explication détaillée :**

**Méthode A - grep + wc :**
```bash
grep "error" file.log | wc -l
# grep trouve lignes avec "error"
# wc -l compte lignes

# Exemple
cat file.txt
# line 1
# error line 2
# line 3
# error line 4
# error line 5

grep "error" file.txt | wc -l
# 3
```

**Méthode B - grep -c (count) :**
```bash
grep -c "error" file.log
# -c = count
# Affiche nombre de lignes directement

# Même exemple
grep -c "error" file.txt
# 3

# Plus court et direct !
```

**Pourquoi C est incorrecte :**

- **C) `wc -l error file`** : **Mauvaise syntaxe**. Compte lignes dans fichiers "error" et "file" (2 fichiers).
  ```bash
  wc -l error file
  # Essaie d'ouvrir fichiers nommés "error" et "file"
  # Pas de recherche du mot "error"
  ```

**Différence subtile A vs B :**
```bash
# Fichier avec plusieurs "error" sur UNE ligne
cat file.txt
# line 1
# error and error again
# line 3

# Méthode A et B
grep "error" file.txt | wc -l
# 1 (une ligne)

grep -c "error" file.txt
# 1 (une ligne)

# IDENTIQUE (compte lignes, pas occurrences)
```

**Compter occurrences (pas lignes) :**
```bash
# Pour compter TOUTES les occurrences
grep -o "error" file.txt | wc -l

# Exemple
cat file.txt
# error and error again

grep -c "error" file.txt
# 1 (une ligne)

grep -o "error" file.txt | wc -l
# 2 (deux occurrences)
# error
# error
```

**Options grep -c :**
```bash
# Compter lignes
grep -c "pattern" file

# Insensitive count
grep -ic "error" file

# Inverser count (lignes SANS pattern)
grep -vc "error" file

# Multiple fichiers
grep -c "error" file1.txt file2.txt
# file1.txt:5
# file2.txt:3

# Récursif avec count
grep -rc "error" /logs
```

**Exemples pratiques :**
```bash
# Compter erreurs dans log
grep -c "ERROR" /var/log/syslog

# Compter warnings
grep -ci "warning" app.log

# Compter lignes code (non vides, non commentaires)
grep -vc "^$\|^#" script.sh

# Multiple patterns
grep -cE "error|warning|critical" log

# Par utilisateur
grep -c "^username" /etc/passwd
```

**Multiple fichiers :**
```bash
# grep -c sur plusieurs fichiers
grep -c "error" *.log
# access.log:42
# error.log:156
# system.log:23

# Total toutes fichiers
grep -h "error" *.log | wc -l
# 221

# Ou avec awk
grep -c "error" *.log | awk -F: '{sum+=$2} END {print sum}'
```

**Comparaison complète :**

| Commande | Compte | Affichage | Notes |
|----------|--------|-----------|-------|
| `grep "error" file \| wc -l` | Lignes | Nombre | Pipe traditionnel |
| `grep -c "error" file` | Lignes | Nombre | Plus direct |
| `grep -o "error" file \| wc -l` | Occurrences | Nombre | Toutes occurrences |
| `wc -l file` | Lignes total | Nombre | Sans filtre |

**awk alternative :**
```bash
# Compter avec awk
awk '/error/{count++} END {print count}' file

# Avec condition
awk '$3 > 100 && /error/{count++} END {print count}' file
```

**Scripts :**
```bash
#!/bin/bash
# Compter patterns dans logs

LOG_FILE="/var/log/app.log"

ERRORS=$(grep -c "ERROR" "$LOG_FILE")
WARNINGS=$(grep -c "WARNING" "$LOG_FILE")
CRITICAL=$(grep -c "CRITICAL" "$LOG_FILE")

echo "Statistiques:"
echo "  Errors:   $ERRORS"
echo "  Warnings: $WARNINGS"
echo "  Critical: $CRITICAL"
echo "  Total:    $((ERRORS + WARNINGS + CRITICAL))"
```

**Différence lignes vs occurrences :**
```bash
# Fichier
cat file.txt
# error
# error error
# line
# error error error

# Lignes avec error
grep -c "error" file.txt
# 3 lignes

# Occurrences totales
grep -o "error" file.txt | wc -l
# 6 occurrences
```

**Performances :**
```bash
# grep -c optimisé (arrête de lire après match)
time grep -c "error" huge.log
# 0.3s

# grep | wc peut être légèrement plus lent
time grep "error" huge.log | wc -l
# 0.4s

# Différence minime en pratique
```

---

### Question 48
**Réponse correcte : B**

**Explication détaillée :**

`grep -v` (invert) inverse la recherche :

```bash
grep -v "pattern" file
# -v = invert match
# Affiche lignes NE contenant PAS "pattern"

# Exemple
cat file.txt
# line 1
# error line 2
# line 3
# error line 4
# line 5

grep -v "error" file.txt
# line 1
# line 3
# line 5
# (lignes SANS "error")
```

**Pourquoi les autres sont incorrectes :**

- **A) `grep -n pattern file`** : Affiche **numéros de lignes** (pas inversion).
  ```bash
  grep -n "error" file.txt
  # 2:error line 2
  # 4:error line 4
  # (avec numéros)
  ```

- **C) `grep -c pattern file`** : **Compte** lignes (pas affichage inversé).
  ```bash
  grep -c "error" file.txt
  # 2
  # (juste le nombre)
  ```

- **D) `grep -i pattern file`** : **Ignore casse** (pas inversion).
  ```bash
  grep -i "error" file.txt
  # error line 2
  # ERROR line X
  # (casse ignorée)
  ```

**Exemples pratiques -v :**
```bash
# Supprimer commentaires
grep -v "^#" config.conf
# Lignes ne commençant pas par #

# Supprimer lignes vides
grep -v "^$" file.txt

# Supprimer commentaires ET lignes vides
grep -vE "^$|^#" file.txt

# Logs sans "debug"
grep -v "debug" app.log

# Processus sans grep lui-même
ps aux | grep "apache" | grep -v "grep"
# Ou: ps aux | grep "[a]pache"

# Fichiers sauf .txt
ls | grep -v "\.txt$"
```

**Combiner avec autres options :**
```bash
# Inverser + ignorer casse
grep -vi "error" file

# Inverser + compter
grep -vc "error" file
# Compte lignes SANS "error"

# Inverser + numéros lignes
grep -vn "error" file
# 1:line 1
# 3:line 3
# 5:line 5

# Inverser + contexte
grep -v -A 2 "error" file
# Lignes sans error + 2 lignes après

# Inverser + multiple patterns
grep -vE "error|warning" file
```

**Nettoyage fichiers :**
```bash
# Supprimer commentaires Python
grep -v "^#" script.py

# Supprimer commentaires + lignes vides
grep -vE "^#|^$" script.py > clean.py

# Supprimer lignes debug
grep -v "DEBUG" app.log > production.log

# Garder seulement erreurs (supprimer info)
grep -v "INFO" log | grep -v "DEBUG"
# Ou
grep -vE "INFO|DEBUG" log
```

**Différence -v vs autres :**

| Option | Action | Exemple résultat |
|--------|--------|------------------|
| `grep "error" file` | Trouve pattern | Lignes avec "error" |
| `grep -v "error" file` | **Inverse** | Lignes **SANS** "error" |
| `grep -n "error" file` | Avec numéros | 2:error line... |
| `grep -c "error" file` | Compte | 5 |
| `grep -i "error" file` | Ignore casse | error, Error, ERROR |

**Multiple exclusions :**
```bash
# Exclure plusieurs patterns
grep -v "error" file | grep -v "warning"

# Plus efficace avec -E
grep -vE "error|warning" file

# Exclure patterns complexes
grep -vE "^(#|$|DEBUG|INFO)" file
# Lignes sans: # début, vides, DEBUG, INFO
```

**Scripts de nettoyage :**
```bash
#!/bin/bash
# Nettoyer log

INPUT="app.log"
OUTPUT="clean.log"

# Supprimer debug et info
grep -vE "DEBUG|INFO" "$INPUT" > "$OUTPUT"

echo "Avant: $(wc -l < $INPUT) lignes"
echo "Après: $(wc -l < $OUTPUT) lignes"
```

**sed équivalent :**
```bash
# sed (delete pattern)
sed '/error/d' file
# = grep -v "error" file

# Supprimer commentaires
sed '/^#/d' file
# = grep -v "^#" file
```

**awk équivalent :**
```bash
# awk (inverse)
awk '!/error/' file
# = grep -v "error" file

# Complexe
awk '!/error/ && !/warning/' file
# = grep -vE "error|warning" file
```

**Cas pratiques :**
```bash
# Processus sauf sh/bash
ps aux | grep -vE "sh$|bash$"

# Fichiers sauf cachés
ls -a | grep -v "^\."

# IPs sauf localhost
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" file | grep -v "127.0.0.1"

# Users sauf système (UID < 1000)
awk -F: '$3 >= 1000 {print}' /etc/passwd
# Ou filtrer par shell
grep -v "/nologin$\|/false$" /etc/passwd
```

**Performance :**
```bash
# -v généralement rapide
# Arrête dès que trouve NON-match

# Multiple greps séquentiels (moins efficace)
grep -v "a" file | grep -v "b" | grep -v "c"

# Un seul grep -E (plus efficace)
grep -vE "a|b|c" file
```

---

### Question 49
**Réponse correcte : C (Trois méthodes !)**

**Explication détaillée :**

**Trois commandes pour sauvegarder + quitter :**

**Méthode 1 - :wq :**
```bash
:wq
# :w  = write (sauvegarder)
# :q  = quit (quitter)
# Combiné: write + quit
```

**Méthode 2 - :x :**
```bash
:x
# Sauvegarder + quitter
# Plus court que :wq
# Équivalent exact
```

**Méthode 3 - ZZ (mode Normal) :**
```bash
ZZ
# Shift+Z deux fois
# Pas besoin de : (mode Normal directement)
# Sauvegarde + quitte
```

**Pourquoi les autres sont incorrectes :**

- **A) `:q`** : **Quitte sans sauvegarder** (erreur si modifications non sauvegardées).
  ```bash
  :q
  # E37: No write since last change (use ! to override)
  ```

- **B) `:w`** : **Sauvegarde sans quitter** (reste dans vi).
  ```bash
  :w
  # File saved (but still in vi)
  ```

- **D) `:q!`** : **Quitte sans sauvegarder** (force, abandonne modifications).
  ```bash
  :q!
  # Quit without saving (changes lost)
  ```

**Tableau commandes vi quitter :**

| Commande | Sauvegarde | Quitte | Force | Notes |
|----------|------------|--------|-------|-------|
| `:q` | ❌ Non | ✅ Oui | ❌ Non | Erreur si modifié |
| `:q!` | ❌ Non | ✅ Oui | ✅ Oui | Abandonne modifs |
| `:w` | ✅ Oui | ❌ Non | - | Reste dans vi |
| `:wq` | ✅ Oui | ✅ Oui | - | Standard |
| `:x` | ✅ Oui | ✅ Oui | - | Équivalent :wq |
| `ZZ` | ✅ Oui | ✅ Oui | - | Mode Normal |
| `:wq!` | ✅ Oui | ✅ Oui | ✅ Oui | Force même readonly |

**Commandes sauvegardes :**
```bash
# Sauvegarder fichier actuel
:w

# Sauvegarder sous nouveau nom
:w newfile.txt

# Sauvegarder + quitter
:wq
:x
ZZ

# Sauvegarder ligne N à M
:10,20w partial.txt

# Append à fichier existant
:w >> existing.txt

# Force save (readonly)
:w!

# Save + quit (force)
:wq!
```

**Workflow typique :**
```bash
# 1. Ouvrir fichier
vi file.txt

# 2. Mode Insert (i)
i
# Éditer...

# 3. Mode Normal (Esc)
Esc

# 4. Sauvegarder + quitter
:wq
# Ou
:x
# Ou
ZZ
```

**Cas d'erreur :**
```bash
# Fichier modifié, :q sans save
vi file.txt
# (modify)
:q
# E37: No write since last change

# Solutions:
:wq      # Sauvegarder puis quitter
:q!      # Quitter sans sauvegarder (abandonner)

# Fichier readonly
vi /etc/hosts
# (modify)
:wq
# E45: 'readonly' option is set

# Solutions:
:wq!     # Force (si permissions OK)
:w /tmp/hosts  # Sauvegarder ailleurs
```

**Modes vi rappel :**
```bash
# Mode Normal (par défaut)
# - Navigation (hjkl)
# - Commandes (dd, yy, p)
# - ZZ (save+quit)

# Mode Insert (édition)
# i, I, a, A, o, O
# Esc pour revenir Normal

# Mode Command (commandes :)
# :w, :q, :wq, :x
# Enter pour exécuter
```

**Exemples pratiques :**
```bash
# Éditer fichier config
vi /etc/nginx/nginx.conf
# (modify)
:wq

# Créer nouveau fichier
vi newfile.txt
i
# Type content
Esc
:wq

# Éditer multiple fichiers
vi file1.txt file2.txt
# (edit file1)
:wq
# (passe à file2, edit)
:wq

# Sauvegarder puis continuer éditer
:w
# (continue editing)
```

**Aliases communs (vimrc) :**
```vim
" ~/.vimrc
" Fast save
nnoremap <leader>w :w<CR>

" Fast quit
nnoremap <leader>q :q<CR>

" Fast save+quit
nnoremap <leader>x :x<CR>
```

**Différence :x vs :wq :**
```bash
# :wq - TOUJOURS écrit fichier
:wq
# Timestamp modifié même si aucun changement

# :x - Écrit SEULEMENT si modifié
:x
# Timestamp inchangé si pas de modifs
# Légèrement plus efficace
```

---

### Question 50
**Réponse correcte : A**

**Explication détaillée :**

**Plusieurs commandes pour mode Insert :**

```bash
# Mode Normal → Mode Insert

i    Insert AVANT curseur
I    Insert DÉBUT de ligne

a    Append APRÈS curseur
A    Append FIN de ligne

o    Open line BELOW (nouvelle ligne dessous)
O    Open line ABOVE (nouvelle ligne dessus)

s    Substitute caractère (supprime + insert)
S    Substitute ligne entière

c<motion>  Change (supprime motion + insert)
# cw = change word
# c$ = change jusqu'à fin ligne
```

**Exemples visuels :**
```bash
# Fichier: "Hello world"
#          ^curseur sur 'H'

i → |Hello world      (insert avant H)
I → |Hello world      (insert début ligne)
a → H|ello world      (append après H)
A → Hello world|      (append fin ligne)
o → Hello world
    |                 (nouvelle ligne dessous)
O → |
    Hello world       (nouvelle ligne dessus)
```

**Pourquoi les autres sont incorrectes :**

- **B) `Esc`** : **Quitte** mode Insert (retour mode Normal).
  ```bash
  # En mode Insert
  Esc    → Mode Normal
  ```

- **C) `:i`** : **Commande invalide** (`:` pour mode Command, pas Insert).
  ```bash
  :i
  # E492: Not an editor command: i
  ```

- **D) `Ctrl+I`** : **Pas utilisé** pour Insert (c'est Tab).

**Tableau modes Insert :**

| Touche | Action | Position curseur |
|--------|--------|------------------|
| `i` | Insert | Avant curseur |
| `I` | Insert | **Début de ligne** |
| `a` | Append | Après curseur |
| `A` | Append | **Fin de ligne** |
| `o` | Open below | **Nouvelle ligne dessous** |
| `O` | Open above | **Nouvelle ligne dessus** |
| `s` | Substitute char | Remplace caractère |
| `S` | Substitute line | Remplace ligne |
| `cw` | Change word | Change mot |
| `cc` | Change line | Change ligne |

**Workflow édition :**
```bash
# 1. Ouvrir fichier (mode Normal)
vi file.txt

# 2. Se positionner
# hjkl pour naviguer

# 3. Mode Insert
i    # ou a, o, etc.

# 4. Taper texte
This is new text

# 5. Mode Normal (Esc)
Esc

# 6. Sauvegarder
:w
```

**Exemples pratiques :**
```bash
# Ajouter en fin de ligne
A
# Type text
Esc

# Nouvelle ligne dessous
o
# Type new line
Esc

# Remplacer mot
cw
# Type new word
Esc

# Insérer au début
I
# Type prefix
Esc

# Remplacer ligne entière
S
# Type new line content
Esc
```

**Indicateur mode (vim) :**
```bash
# vim (pas vi original)
# Bas de l'écran affiche mode

-- INSERT --         (mode Insert)
-- VISUAL --         (mode Visual)
(rien)               (mode Normal)
```

**Change avec motions :**
```bash
# Change = delete + insert
cw     Change jusqu'à fin mot
c$     Change jusqu'à fin ligne
c0     Change jusqu'à début ligne
cc     Change ligne entière
C      Change jusqu'à fin ligne (=c$)
ciw    Change inner word (mot entier)
ci"    Change inside quotes
```

**Erreurs courantes débutants :**
```bash
# Erreur: Taper en mode Normal
# → Commandes exécutées par accident
# → Utiliser 'u' (undo) puis 'i'

# Erreur: Plusieurs Esc
# → Beep (déjà en mode Normal)

# Erreur: Oublier Esc avant :wq
# → :wq tapé comme texte
# → Appuyer Esc puis :wq
```

**Modes vi résumé :**
```bash
# 3 modes principaux

1. Normal (défaut)
   - Navigation: hjkl, w, b, $, 0, G
   - Commandes: dd, yy, p, u, .
   - Passer en Insert: i, a, o
   - Passer en Command: :
   - Passer en Visual: v

2. Insert
   - Édition texte
   - Esc → Normal

3. Command
   - :w, :q, :wq
   - Enter → exécute
```

**Replace mode (bonus) :**
```bash
# R (mode Replace)
R
# Tape texte, remplace caractères existants
# Comme Insert mais écrase

# r (replace single char)
r + character
# Remplace UN caractère, retour Normal
```

---
