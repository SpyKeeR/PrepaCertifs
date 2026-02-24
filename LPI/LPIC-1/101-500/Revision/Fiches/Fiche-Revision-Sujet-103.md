# 📄 Fiche Sujet 103 : Commandes GNU et Unix

**Poids : 16 points (40%)** | Révision rapide

---

## 103.1 : Shell et Scripts (4 pts)

### Variables
```bash
# Définition
VAR="value"              # Pas d'espaces autour =
export VAR="value"       # Variable environnement

# Affichage
echo $VAR
echo ${VAR}
printenv VAR
env | grep VAR

# Variables spéciales
$0        # Nom script
$1-$9     # Arguments
$#        # Nombre arguments
$@        # Tous arguments
$?        # Code retour dernière commande
$$        # PID script
$!        # PID dernier background
```

### Structures
```bash
# If
if [ condition ]; then
    commands
elif [ condition ]; then
    commands
else
    commands
fi

# Tests fichiers
[ -e file ]    # Existe
[ -f file ]    # Fichier regular
[ -d dir ]     # Directory
[ -r file ]    # Readable
[ -w file ]    # Writable
[ -x file ]    # Executable
[ -s file ]    # Taille > 0

# Tests chaînes
[ -z "$str" ]  # Vide
[ -n "$str" ]  # Non vide
[ "$a" = "$b" ] # Égalité
[ "$a" != "$b" ] # Différence

# Tests numériques
[ $a -eq $b ]  # Égal
[ $a -ne $b ]  # Différent
[ $a -lt $b ]  # <
[ $a -le $b ]  # ≤
[ $a -gt $b ]  # >
[ $a -ge $b ]  # ≥

# For
for i in list; do
    commands
done

for i in {1..10}; do echo $i; done
for file in *.txt; do echo $file; done

# While
while [ condition ]; do
    commands
done

# Case
case $VAR in
    pattern1) commands ;;
    pattern2) commands ;;
    *) default ;;
esac
```

### Fonctions
```bash
function_name() {
    commands
    return 0
}

# Appel
function_name arg1 arg2

# Arguments fonction
$1, $2, ...    # Arguments fonction
```

### Commandes utiles
```bash
source script.sh         # Exécute dans shell actuel
. script.sh              # Idem
./script.sh              # Exécute dans sous-shell (nécessite +x)

command1 && command2     # ET (cmd2 si cmd1 réussit)
command1 || command2     # OU (cmd2 si cmd1 échoue)

exec command             # Remplace shell actuel
```

---

## 103.2 : Filtres Texte (4 pts)

### cat, head, tail
```bash
cat file                 # Affiche tout
cat -n file              # Numéros lignes
cat file1 file2 > out    # Concaténer

head file                # 10 premières lignes
head -n 20 file          # 20 premières

tail file                # 10 dernières
tail -n 20 file          # 20 dernières
tail -f file             # Suivre (logs)
tail -f /var/log/syslog
```

### cut, paste
```bash
cut -d: -f1 /etc/passwd  # Champ 1, délimiteur :
cut -d: -f1,3 file       # Champs 1 et 3
cut -c1-10 file          # Caractères 1 à 10

paste file1 file2        # Fusionner colonnes
paste -d, file1 file2    # Délimiteur virgule
```

### sort, uniq
```bash
sort file                # Tri alphabétique
sort -n file             # Tri numérique
sort -r file             # Reverse
sort -k2 file            # Tri colonne 2
sort -t: -k3 -n /etc/passwd  # Tri champ 3 numérique

uniq file                # Supprimer doublons consécutifs
sort file | uniq         # Doublons non-consécutifs
uniq -c file             # Compter occurrences
uniq -d file             # Seulement doublons
uniq -u file             # Seulement uniques
```

### wc, nl
```bash
wc file                  # Lignes Mots Caractères
wc -l file               # Lignes seulement
wc -w file               # Mots
wc -c file               # Caractères

nl file                  # Numéroter lignes
nl -ba file              # Toutes lignes (même vides)
```

### tr, expand, unexpand
```bash
tr 'a-z' 'A-Z' < file    # Minuscules → Majuscules
tr -d 'aeiou' < file     # Supprimer voyelles
tr -s ' ' < file         # Squeeze espaces multiples

expand file              # Tabs → espaces
unexpand file            # Espaces → tabs
```

### split, join
```bash
split -l 1000 file part_ # Découper 1000 lignes/fichier
split -b 10M file part_  # Découper 10MB/fichier

join file1 file2         # Jointure champ commun
```

---

## 103.3 : Gestion Fichiers (4 pts)

### ls
```bash
ls -l                    # Long format
ls -a                    # Fichiers cachés
ls -la                   # Combiné
ls -lh                   # Human-readable sizes
ls -lt                   # Tri par date modification
ls -ltr                  # Tri date (reverse = ancien d'abord)
ls -R                    # Récursif
ls -i                    # Inode numbers
ls -d */                 # Seulement répertoires
```

### cp, mv, rm
```bash
cp source dest           # Copier
cp -r dir dest           # Copier récursif (dirs)
cp -a dir dest           # Archive (preserve attrs)
cp -p file dest          # Preserve permissions/dates
cp -i file dest          # Interactif (demande confirmation)
cp -u file dest          # Update (seulement si plus récent)

mv source dest           # Déplacer/renommer
mv -i file dest          # Interactif
mv -u file dest          # Update

rm file                  # Supprimer
rm -r dir                # Récursif
rm -f file               # Force (pas de confirmation)
rm -rf dir               # Force récursif (⚠️)
rm -i file               # Interactif
```

### mkdir, rmdir, touch
```bash
mkdir dir                # Créer répertoire
mkdir -p path/to/dir     # Parents si nécessaire
mkdir -m 755 dir         # Avec permissions

rmdir dir                # Supprimer répertoire vide
rm -r dir                # Supprimer non-vide

touch file               # Créer/MAJ timestamp
touch -t 202601281200 file  # Timestamp spécifique
```

### file, dd
```bash
file fichier             # Type fichier
file -b fichier          # Sans nom fichier
file -i fichier          # MIME type

dd if=/dev/sda of=backup.img  # Clone disque
dd if=/dev/zero of=file bs=1M count=100  # Créer fichier 100MB
dd if=file of=/dev/sdb bs=4M status=progress  # Avec progress
```

### Globbing (wildcards)
```bash
*                        # N'importe quoi
?                        # Un caractère
[abc]                    # a ou b ou c
[a-z]                    # a à z
[!abc]                   # Pas a, b, c
{txt,pdf}                # txt ou pdf

# Exemples
ls *.txt                 # Tous .txt
ls file?.txt             # file1.txt, fileA.txt
ls [A-Z]*                # Commence par majuscule
ls *.{jpg,png}           # Images
```

---

## 103.4 : Streams, Pipes, Redirections (4 pts)

### Redirections
```bash
cmd > file               # Stdout → file (écrase)
cmd >> file              # Stdout → file (append)
cmd 2> file              # Stderr → file
cmd &> file              # Stdout + Stderr → file
cmd > file 2>&1          # Idem (ancienne syntaxe)
cmd < file               # Stdin ← file
cmd << EOF               # Here document
cmd <<< "string"         # Here string

# Exemples
ls -la > listing.txt
grep error log 2> errors.txt
find / -name file 2>/dev/null  # Ignorer erreurs
```

### Pipes
```bash
cmd1 | cmd2              # Stdout cmd1 → Stdin cmd2
cmd1 | tee file | cmd2   # Pipe + sauvegarde fichier

# Exemples
ps aux | grep apache
cat file | sort | uniq -c
dmesg | grep -i error | less
```

### xargs
```bash
find . -name "*.tmp" | xargs rm      # Supprimer résultats find
find . -type f | xargs grep "pattern"  # Grep dans résultats
echo "file1 file2" | xargs touch     # Créer fichiers
ls | xargs -I {} cp {} {}.bak        # Backup avec {}
```

---

## 103.5 : Gestion Processus (4 pts)

### ps
```bash
ps                       # Processus user actuel
ps aux                   # Tous processus (BSD style)
ps -ef                   # Tous processus (System V)
ps -u username           # Processus user spécifique
ps -C processname        # Par nom
ps --forest              # Tree view
ps -eo pid,cmd,%cpu,%mem # Colonnes custom
```

### top, htop
```bash
top                      # Monitoring temps réel
  M        # Tri par RAM
  P        # Tri par CPU
  k        # Kill process
  r        # Renice
  q        # Quit

htop                     # Top amélioré (si installé)
```

### Gestion jobs
```bash
command &                # Background
jobs                     # Liste jobs
fg %1                    # Foreground job 1
bg %1                    # Background job 1
Ctrl+Z                   # Suspend job actuel
Ctrl+C                   # Kill job actuel

# Exemples
sleep 100 &
jobs
fg %1
```

### kill, killall, pkill
```bash
kill PID                 # Envoyer SIGTERM
kill -15 PID             # SIGTERM (défaut)
kill -9 PID              # SIGKILL (force)
kill -KILL PID           # Idem
kill -HUP PID            # SIGHUP (reload config)
kill -STOP PID           # Pause
kill -CONT PID           # Reprendre

killall processname      # Tuer par nom
pkill -u username        # Tuer tous processus user
pkill -9 processname     # Kill -9 par nom

# Signaux courants
1  HUP     # Hangup (reload config)
2  INT     # Interrupt (Ctrl+C)
9  KILL    # Force kill (non-catchable)
15 TERM    # Terminate (propre, défaut)
18 CONT    # Continue
19 STOP    # Stop
```

### pgrep, pidof
```bash
pgrep processname        # PID par nom
pgrep -u username        # PIDs user
pidof processname        # PIDs process exact
```

### nice, renice
```bash
nice -n 10 command       # Lancer avec priorité +10
nice -n -5 command       # Priorité -5 (root seulement)

renice 15 -p PID         # Changer priorité process
renice -5 -u username    # Tous processus user

# Priorités: -20 (max) à +19 (min)
# Défaut = 0
```

### nohup, screen, tmux
```bash
nohup command &          # Continuer après logout
nohup ./script.sh > output.log 2>&1 &

screen                   # Session persistante
  Ctrl+A D     # Detach
screen -ls               # Liste sessions
screen -r session        # Reattach

tmux                     # Terminal multiplexer
  Ctrl+B D     # Detach
tmux ls
tmux attach
```

---

## 103.6 : Priorités Processus (2 pts)

### Valeurs nice
```bash
# -20 = Priorité maximale (réservé root)
#   0 = Priorité normale (défaut)
# +19 = Priorité minimale

# Lancer avec priorité
nice -n 10 tar -czf backup.tar.gz /data

# Modifier priorité
renice 10 -p 1234
renice -5 -u alice
```

### top - colonnes priorité
```
NI   # Nice value (-20 à +19)
PR   # Priority (20 + NI pour user processes)
```

---

## 103.7 : Regex (2 pts)

### Caractères de base
```bash
.        # N'importe quel caractère
^        # Début ligne
$        # Fin ligne
*        # 0 ou + du précédent
+        # 1 ou + du précédent (grep -E)
?        # 0 ou 1 du précédent (grep -E)
[]       # Classe caractères
[^]      # Négation classe
|        # OU (grep -E)
()       # Groupement (grep -E)

# Exemples
^root        # Lignes commençant par "root"
bash$        # Lignes finissant par "bash"
^$           # Lignes vides
[0-9]        # Chiffre
[a-zA-Z]     # Lettre
[^0-9]       # Pas chiffre
a*           # 0+ "a"
a+           # 1+ "a" (grep -E)
a?           # 0 ou 1 "a" (grep -E)
(ab)+        # ab, abab, ababab... (grep -E)
cat|dog      # cat ou dog (grep -E)
```

### grep
```bash
grep pattern file        # Chercher
grep -i pattern file     # Insensible casse
grep -v pattern file     # Inverser (pas pattern)
grep -r pattern dir      # Récursif
grep -n pattern file     # Numéros lignes
grep -c pattern file     # Compter
grep -l pattern files    # Seulement noms fichiers
grep -w pattern file     # Mot entier
grep -E "regex" file     # Extended regex (ERE)
grep -A 3 pattern file   # 3 lignes après
grep -B 3 pattern file   # 3 lignes avant
grep -C 3 pattern file   # 3 lignes avant+après

# Exemples
grep '^root' /etc/passwd
grep -E 'error|warning' /var/log/syslog
grep -r "TODO" /project/
ps aux | grep apache | grep -v grep
```

### sed (simple)
```bash
sed 's/old/new/' file        # Remplacer 1ère occurrence
sed 's/old/new/g' file       # Toutes occurrences
sed -i 's/old/new/g' file    # Modifier fichier
sed '/pattern/d' file        # Supprimer lignes
sed -n '10,20p' file         # Afficher lignes 10-20
sed '5d' file                # Supprimer ligne 5
```

---

## 103.8 : vi/vim (4 pts)

### Modes
```
ESC           # Mode commande
i             # Insert avant curseur
a             # Insert après curseur
I             # Insert début ligne
A             # Insert fin ligne
o             # Nouvelle ligne dessous
O             # Nouvelle ligne dessus
R             # Replace mode
v             # Visual mode
```

### Déplacements
```
h j k l       # ← ↓ ↑ →
w             # Mot suivant
b             # Mot précédent
0             # Début ligne
^             # Premier caractère non-blanc
$             # Fin ligne
gg            # Début fichier
G             # Fin fichier
:n            # Ligne n
Ctrl+F        # Page down
Ctrl+B        # Page up
```

### Édition
```
x             # Supprimer caractère
dd            # Supprimer ligne
D             # Supprimer jusqu'à fin ligne
dw            # Supprimer mot
d$            # Supprimer jusqu'à fin ligne
yy            # Copier ligne
yw            # Copier mot
p             # Coller après
P             # Coller avant
u             # Undo
Ctrl+R        # Redo
.             # Répéter dernière commande
```

### Recherche/Remplacement
```
/pattern      # Chercher avant
?pattern      # Chercher arrière
n             # Résultat suivant
N             # Résultat précédent

:s/old/new/           # Remplacer ligne actuelle
:s/old/new/g          # Ligne actuelle (toutes occur.)
:%s/old/new/g         # Tout fichier
:%s/old/new/gc        # Avec confirmation
:10,20s/old/new/g     # Lignes 10-20
```

### Fichiers
```
:w            # Sauvegarder
:w file       # Sauvegarder sous
:q            # Quitter
:q!           # Quitter sans sauvegarder
:wq           # Sauvegarder et quitter
:x            # Idem
ZZ            # Idem
:e file       # Ouvrir fichier
:r file       # Insérer fichier
```

### Autres
```
:set number   # Numéros lignes
:set nonumber # Pas numéros
:set ai       # Auto-indent
:syntax on    # Coloration syntaxe
:help         # Aide
```

---

## 🎯 Points clés examen

1. **Variables** : Pas d'espaces autour =
2. **$?** : Code retour dernière commande (0=succès)
3. **[ -f file ]** : Test fichier regular
4. **sort | uniq** : Supprimer doublons non-consécutifs
5. **tr 'a-z' 'A-Z'** : Transformer casse
6. **cmd 2>/dev/null** : Ignorer erreurs
7. **cmd1 | tee file | cmd2** : Pipe + sauvegarde
8. **ps aux** vs **ps -ef** : Même résultat, syntaxes différentes
9. **kill -9** : SIGKILL (force, non-catchable)
10. **nice -20 à +19** : -20=max priorité (root), +19=min
11. **^** : Début ligne, **$** : Fin ligne
12. **grep -E** : Extended regex (|, +, ?)
13. **vi modes** : ESC (commande), i (insert)
14. **:wq** : Sauvegarder et quitter vi
15. **dd** : Supprimer ligne vi

---

## 📋 Checklist révision

- [ ] Variables shell ($0, $1, $?, $$)
- [ ] Tests [ -f ], [ -d ], [ -z ]
- [ ] Boucles for, while, case
- [ ] cat, head, tail -f
- [ ] cut -d: -f1, paste
- [ ] sort -n, uniq -c
- [ ] tr, wc -l
- [ ] ls -la, cp -r, rm -rf
- [ ] Redirections >, >>, 2>, &>
- [ ] Pipes |, xargs
- [ ] ps aux, top
- [ ] kill -15 vs kill -9
- [ ] nice, renice
- [ ] Regex ^, $, ., *, +, []
- [ ] grep -r, grep -E
- [ ] vi modes, :wq, dd, yy, p
