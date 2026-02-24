# 📄 Fiche Sujet 105 : Shells et Scripts

**Poids : 11 points (18%)** | Révision rapide

---

## 105.1 : Environnement du shell (4 pts)

### Variables d'environnement
```bash
# Affichage
env                    # Variables environnement
printenv               # Idem
set                    # Variables + fonctions
echo $VARIABLE

# Principales variables
$PATH                  # Chemins exécutables
$HOME                  # Répertoire personnel
$USER, $LOGNAME        # Nom utilisateur
$SHELL                 # Shell par défaut
$HOSTNAME              # Nom machine
$PWD                   # Répertoire actuel
$OLDPWD                # Répertoire précédent
$PS1                   # Prompt
$LANG, $LC_ALL         # Locale

# Définition
export VAR=valeur      # Variable d'environnement
VAR=valeur             # Variable locale (shell actuel)
unset VAR              # Supprimer variable
```

### Fichiers de configuration
```bash
# Login shells (ordre)
/etc/profile           # Système (tous users)
~/.bash_profile        # User (prioritaire)
~/.bash_login          # Si pas .bash_profile
~/.profile             # Si pas les 2 premiers

# Non-login shells
/etc/bash.bashrc       # Système
~/.bashrc              # User

# Logout
~/.bash_logout         # Exécuté à la déconnexion

# Fonctions shell
function nom() {
    commandes
}
# ou
nom() {
    commandes
}
```

### Alias
```bash
alias ll='ls -la'
alias rm='rm -i'
unalias ll
alias                  # Liste tous alias
```

---

## 105.2 : Scripts shell (4 pts)

### Bases script
```bash
#!/bin/bash            # Shebang

# Variables
VAR="valeur"
echo "$VAR"            # Avec expansion
echo '$VAR'            # Littéral

# Arguments
$0                     # Nom script
$1, $2, ...            # Arguments 1, 2...
$#                     # Nombre d'arguments
$@, $*                 # Tous arguments
$?                     # Code retour dernière commande
$$                     # PID script
```

### Structures conditionnelles
```bash
# if
if [ condition ]; then
    commandes
elif [ condition2 ]; then
    commandes
else
    commandes
fi

# Tests fichiers
-e fichier             # Existe
-f fichier             # Fichier régulier
-d répertoire          # Répertoire
-r fichier             # Lisible
-w fichier             # Modifiable
-x fichier             # Exécutable
-s fichier             # Non vide

# Tests chaînes
-z "$str"              # Chaîne vide
-n "$str"              # Chaîne non vide
"$a" = "$b"            # Égales
"$a" != "$b"           # Différentes

# Tests numériques
$a -eq $b              # Égal
$a -ne $b              # Différent
$a -lt $b              # Inférieur <
$a -le $b              # Inférieur ou égal ≤
$a -gt $b              # Supérieur >
$a -ge $b              # Supérieur ou égal ≥

# Opérateurs logiques
[ cond1 ] && [ cond2 ] # ET
[ cond1 ] || [ cond2 ] # OU
! [ cond ]             # NON
```

### Boucles
```bash
# for
for var in liste; do
    commandes
done

for i in {1..10}; do
    echo $i
done

for file in *.txt; do
    echo $file
done

# while
while [ condition ]; do
    commandes
done

# until
until [ condition ]; do
    commandes
done

# Contrôle boucles
break                  # Sortir boucle
continue               # Itération suivante
```

### Fonctions
```bash
fonction() {
    local var=valeur   # Variable locale
    echo "$1"          # Premier paramètre
    return 0           # Code retour
}

fonction arg1 arg2
resultat=$?            # Récupérer code retour
```

---

## 🎯 Points clés examen

### Must know
- ✅ Différence login shell vs non-login shell
- ✅ Ordre fichiers config (`/etc/profile` → `~/.bash_profile` → `~/.bashrc`)
- ✅ `export` pour variables d'environnement
- ✅ Variables spéciales : `$0`, `$1-$9`, `$#`, `$?`, `$$`, `$@`
- ✅ Tests avec `[ ]` : `-f`, `-d`, `-e`, `-r`, `-w`, `-x`
- ✅ Tests numériques : `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`
- ✅ Boucles `for`, `while`, `until`
- ✅ `if-then-else-fi` et `case-esac`

### Pièges
- ❌ Oublier `export` pour variables globales
- ❌ Confondre `$*` et `$@` (entre guillemets)
- ❌ Utiliser `=` au lieu de `-eq` pour nombres
- ❌ Oublier espaces dans `[ condition ]`
- ❌ Ne pas quoter variables : `"$var"` vs `$var`

### Astuces rapides
```bash
# Tester existence fichier avant traitement
[ -f "$file" ] && cat "$file"

# Boucle sur arguments
for arg in "$@"; do
    echo "$arg"
done

# Lecture fichier ligne par ligne
while IFS= read -r line; do
    echo "$line"
done < fichier.txt

# Fonction avec retour
addition() {
    echo $(( $1 + $2 ))
}
result=$(addition 5 3)

```

---

**💡 Conseil :** Pratiquez en créant de vrais scripts ! Les structures conditionnelles et boucles sont très fréquentes à l'examen.
