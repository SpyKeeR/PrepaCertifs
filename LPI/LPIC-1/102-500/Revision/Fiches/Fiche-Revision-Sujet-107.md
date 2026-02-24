# 📄 Fiche Sujet 107 : Tâches Administratives

**Poids : 12 points (20%)** | Révision rapide

---

## 107.1 : Gestion comptes utilisateurs (5 pts)

### Création utilisateurs/groupes
```bash
# Utilisateurs
useradd user                  # Créer utilisateur
useradd -m user               # + répertoire home
useradd -m -s /bin/bash user  # + shell
useradd -u 1500 user          # UID spécifique
useradd -g group user         # Groupe primaire
useradd -G gr1,gr2 user       # Groupes secondaires
useradd -c "Nom Complet" user # Commentaire
usermod -aG sudo user         # Ajouter à groupe (append!)
usermod -s /bin/zsh user      # Changer shell
usermod -L user               # Verrouiller
usermod -U user               # Déverrouiller
userdel user                  # Supprimer
userdel -r user               # + supprimer home

# Groupes
groupadd groupe               # Créer groupe
groupadd -g 1000 groupe       # GID spécifique
groupmod -n nouveau ancien    # Renommer
groupdel groupe               # Supprimer

# Infos
id user                       # UID, GID, groupes
groups user                   # Groupes uniquement
whoami                        # Utilisateur actuel
who                           # Utilisateurs connectés
w                             # Utilisateurs + activité
last                          # Historique connexions
```

### Fichiers utilisateurs
```bash
# Fichiers principaux
/etc/passwd                   # Users (7 champs)
/etc/shadow                   # Mots de passe
/etc/group                    # Groupes
/etc/gshadow                  # Mots de passe groupes
/etc/skel/                    # Squelette home

# /etc/passwd format
login:x:UID:GID:GECOS:home:shell
# Exemple: john:x:1001:1001:John Doe:/home/john:/bin/bash

# /etc/shadow format
login:hash:lastchange:min:max:warn:inactive:expire
```

### Environnement utilisateur
```bash
# Squelette
/etc/skel/                    # Copié vers nouveau home
~/.bash_profile               # Login shell
~/.bashrc                     # Non-login shell
~/.bash_logout                # Déconnexion

# Limites
/etc/security/limits.conf     # Limites ressources
ulimit -a                     # Afficher limites
```

---

## 107.2 : Automatisation avec cron (4 pts)

### Crontab
```bash
# Gestion
crontab -e                    # Éditer crontab user
crontab -l                    # Lister
crontab -r                    # Supprimer
crontab -u user -e            # Éditer pour autre user (root)

# Format crontab
# min heure jour mois jour_semaine commande
# *   *     *    *    *            /script.sh

# Exemples
0 2 * * *           /backup.sh       # Tous les jours 2h00
*/15 * * * *        /check.sh        # Toutes les 15 min
0 0 * * 1           /weekly.sh       # Lundi 00h00
0 0 1 * *           /monthly.sh      # 1er du mois
0 0 1 1 *           /yearly.sh       # 1er janvier
@reboot             /startup.sh      # Au démarrage
@daily              /daily.sh        # Tous les jours minuit
@weekly             /weekly.sh       # Chaque semaine
@monthly            /monthly.sh      # Chaque mois

# Cron système
/etc/crontab                  # Crontab système (+ user)
/etc/cron.d/                  # Tâches système
/etc/cron.daily/              # Scripts quotidiens
/etc/cron.weekly/             # Scripts hebdomadaires
/etc/cron.monthly/            # Scripts mensuels
/etc/cron.allow               # Users autorisés
/etc/cron.deny                # Users interdits
```

### Anacron
```bash
# Pour machines non 24/7
/etc/anacrontab               # Config anacron
anacron -n                    # Exécuter maintenant
anacron -T                    # Tester config

# Format anacrontab
# jours délai identifiant commande
1  5    cron.daily    /script.sh
```

### at / batch
```bash
# Exécution unique
at 14:30                      # Interactif
at> /backup.sh
at> Ctrl+D
at now + 2 hours              # Dans 2h
at 2:00 tomorrow              # Demain 2h
at 10:00 2026-02-15           # Date précise
atq                           # Liste tâches
atrm 5                        # Supprimer tâche #5

# batch : comme at mais quand charge faible
batch
batch> /script.sh
batch> Ctrl+D

# Fichiers
/etc/at.allow                 # Users autorisés
/etc/at.deny                  # Users interdits
```

---

## 107.3 : Localisation et internationalisation (3 pts)

### Locale
```bash
# Affichage
locale                        # Locale actuelle
locale -a                     # Locales disponibles
localectl                     # Infos système (systemd)

# Variables locale
LC_CTYPE                      # Classification caractères
LC_NUMERIC                    # Nombres
LC_TIME                       # Date/heure
LC_COLLATE                    # Tri
LC_MONETARY                   # Monnaie
LC_MESSAGES                   # Messages
LC_ALL                        # Override toutes
LANG                          # Défaut

# Définir locale
export LANG=fr_FR.UTF-8
export LC_ALL=fr_FR.UTF-8
localectl set-locale LANG=fr_FR.UTF-8

# Générer locale
locale-gen fr_FR.UTF-8        # Debian/Ubuntu
dpkg-reconfigure locales      # Debian/Ubuntu
```

### Timezone
```bash
# Affichage
date                          # Date/heure actuelle
timedatectl                   # Infos timezone (systemd)
cat /etc/timezone             # Timezone

# Définir timezone
timedatectl set-timezone Europe/Paris
timedatectl list-timezones    # Lister disponibles
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime

# NTP
timedatectl set-ntp true      # Activer NTP
systemctl status systemd-timesyncd
```

### Encodage
```bash
# UTF-8 (moderne)
iconv -f ISO-8859-1 -t UTF-8 input.txt > output.txt
iconv -l                      # Lister encodages

# Vérifier encodage fichier
file -i fichier.txt
file --mime fichier.txt
```

---

## 🎯 Points clés examen

### Must know
- ✅ `useradd -m` pour créer avec home
- ✅ `usermod -aG` (append!) pour ajouter groupes
- ✅ `-L/-U` pour lock/unlock user
- ✅ `/etc/passwd` : 7 champs, `/etc/shadow` : 9 champs
- ✅ Format crontab : `min heure jour mois jour_semaine commande`
- ✅ `*/15` = toutes les 15 minutes
- ✅ `@daily`, `@weekly`, `@monthly`, `@reboot`
- ✅ `at` pour tâche unique, `cron` pour répétitif
- ✅ `LANG`, `LC_ALL` pour locale
- ✅ `timedatectl` pour timezone

### Pièges
- ❌ `usermod -G` écrase groupes (utiliser `-aG`)
- ❌ Confondre jour mois (3e) et jour semaine (5e)
- ❌ Oublier shebang dans scripts cron
- ❌ Variables environnement limitées dans cron
- ❌ Chemin absolu obligatoire dans crontab

### Astuces rapides
```bash
# Utilisateur avec tous droits sudo
useradd -m -G sudo -s /bin/bash admin

# Cron chaque lundi à 8h30
30 8 * * 1 /script.sh

# Cron tous les 2 jours à 3h15
15 3 */2 * * /script.sh

# Locale française UTF-8
export LANG=fr_FR.UTF-8
export LC_ALL=fr_FR.UTF-8

# Timezone Paris
timedatectl set-timezone Europe/Paris

# Voir dernières connexions
last -10
lastlog

# Expiration compte dans 30 jours
usermod -e $(date -d "+30 days" +%Y-%m-%d) user
```

---

**💡 Conseil :** Sujet important (12 pts) ! Maîtrisez bien cron (format + fichiers) et gestion utilisateurs (`useradd`/`usermod`).
