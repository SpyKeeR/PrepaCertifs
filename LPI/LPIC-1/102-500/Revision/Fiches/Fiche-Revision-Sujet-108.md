# 📄 Fiche Sujet 108 : Services Système

**Poids : 10 points (17%)** | Révision rapide

---

## 108.1 : Horloge système (3 pts)

### Date et heure
```bash
# Affichage
date                          # Date/heure système
date +%Y-%m-%d                # Format personnalisé
date +"%d/%m/%Y %H:%M:%S"     # Français
hwclock                       # Horloge matérielle (RTC)

# Définir date/heure
date -s "2026-01-28 14:30:00" # Manuelle (déconseillé)
date --set="14:30:00"         # Heure seulement
timedatectl set-time "2026-01-28 14:30:00"
timedatectl set-time "14:30:00"

# Horloge matérielle
hwclock --show                # Lire RTC
hwclock --hctosys             # RTC → système
hwclock --systohc             # Système → RTC
hwclock --set --date="2026-01-28 14:30"
```

### NTP (Network Time Protocol)
```bash
# systemd-timesyncd (moderne)
timedatectl set-ntp true      # Activer NTP
timedatectl                   # Voir statut
systemctl status systemd-timesyncd

# ntpd (traditionnel)
systemctl status ntpd
ntpq -p                       # Serveurs NTP
ntpdate pool.ntp.org          # Sync manuelle (obsolète)

# chronyd (alternatif moderne)
systemctl status chronyd
chronyc sources               # Serveurs
chronyc tracking              # Statut sync

# Config
/etc/systemd/timesyncd.conf   # systemd-timesyncd
/etc/ntp.conf                 # ntpd
/etc/chrony/chrony.conf       # chronyd
```

### Timezone
```bash
timedatectl list-timezones    # Lister
timedatectl set-timezone Europe/Paris
ls -l /etc/localtime          # Lien vers timezone actuelle
```

---

## 108.2 : Logs système (4 pts)

### rsyslog
```bash
# Service
systemctl status rsyslog
systemctl restart rsyslog

# Config
/etc/rsyslog.conf             # Config principale
/etc/rsyslog.d/*.conf         # Configs additionnelles

# Format règle
facility.priority    action
# Exemples:
mail.*              /var/log/mail.log
*.emerg             *
authpriv.notice     /var/log/auth.log

# Facilities
kern, user, mail, daemon, auth, authpriv, syslog, 
lpr, news, uucp, cron, local0-local7

# Priorities (ordre croissant)
debug < info < notice < warning < err < crit < alert < emerg

# Sélecteurs
*.info              # Toutes facilities, info et +
mail.err            # Mail, err et +
*.=warn             # Exactement warn
*.!err              # Tout sauf err et +
```

### Fichiers logs
```bash
/var/log/syslog               # Général (Debian)
/var/log/messages             # Général (Red Hat)
/var/log/auth.log             # Authentification (Debian)
/var/log/secure               # Authentification (Red Hat)
/var/log/kern.log             # Kernel
/var/log/dmesg                # Boot kernel
/var/log/mail.log             # Mail
/var/log/apache2/             # Apache
/var/log/nginx/               # Nginx

# Lecture
tail -f /var/log/syslog       # Suivi temps réel
tail -n 100 /var/log/auth.log # 100 dernières lignes
grep "error" /var/log/syslog
```

### journalctl (systemd)
```bash
# Affichage
journalctl                    # Tous logs
journalctl -f                 # Suivi temps réel (follow)
journalctl -n 50              # 50 dernières entrées
journalctl -p err             # Priorité err et +
journalctl -p 3               # Idem (err=3)

# Filtres
journalctl -u service         # Service spécifique
journalctl -k                 # Kernel uniquement
journalctl -b                 # Boot actuel
journalctl -b -1              # Boot précédent
journalctl --list-boots       # Lister boots
journalctl --since "1 hour ago"
journalctl --since "2026-01-28 10:00"
journalctl --until "2026-01-28 12:00"
journalctl _PID=1234          # Process ID

# Sortie
journalctl -o json            # Format JSON
journalctl -o verbose         # Détaillé
journalctl --no-pager         # Sans pager

# Persistance
/etc/systemd/journald.conf
# Storage=auto|persistent|volatile|none
mkdir -p /var/log/journal     # Rendre persistent
systemctl restart systemd-journald
```

### logger
```bash
# Écrire dans syslog
logger "Message de test"
logger -p user.warn "Attention!"
logger -t monscript "Démarrage"
logger -f fichier.txt
```

### logrotate
```bash
# Config
/etc/logrotate.conf           # Config principale
/etc/logrotate.d/             # Configs par service

# Exemple config
/var/log/apache2/*.log {
    daily                     # Rotation quotidienne
    rotate 14                 # Garder 14 fichiers
    compress                  # Compresser
    delaycompress             # Compress J-1
    missingok                 # OK si absent
    notifempty                # Pas si vide
    create 0640 www-data adm  # Permissions nouveau
    sharedscripts
    postrotate
        systemctl reload apache2
    endscript
}

# Fréquences
daily, weekly, monthly

# Test
logrotate -d /etc/logrotate.conf  # Dry run
logrotate -f /etc/logrotate.conf  # Forcer
```

---

## 108.3 : MTA (Mail Transfer Agent) (3 pts)

### Configuration mail
```bash
# Principaux MTA
sendmail                      # Historique
postfix                       # Moderne, sécurisé
exim4                         # Debian
qmail                         # Alternatif

# Postfix
systemctl status postfix
/etc/postfix/main.cf          # Config principale
/etc/postfix/master.cf        # Services
postconf                      # Afficher config
postconf -e 'param=valeur'    # Modifier param
postfix reload                # Recharger config

# Queue mails
mailq                         # Voir queue
postqueue -p                  # Idem
postqueue -f                  # Forcer envoi
postsuper -d queue_id         # Supprimer mail
postsuper -d ALL              # Vider queue
```

### Aliases
```bash
/etc/aliases                  # Aliases mail système
# Format:
# alias: destination
root: admin@example.com
postmaster: root
abuse: postmaster

newaliases                    # Régénérer DB après modif
```

### Forward utilisateur
```bash
~/.forward                    # Redirection user
# Contenu:
user@example.com
|/home/user/script.sh
```

### Mail en ligne de commande
```bash
# Envoi
mail -s "Sujet" dest@example.com < fichier.txt
echo "Corps" | mail -s "Sujet" dest@example.com

# Lecture (mail local)
mail                          # Lire mailbox
```

---

## 🎯 Points clés examen

### Must know
- ✅ `timedatectl` pour date/heure/timezone
- ✅ `hwclock --hctosys` (RTC→sys), `--systohc` (sys→RTC)
- ✅ `systemd-timesyncd` pour NTP moderne
- ✅ rsyslog : `facility.priority action`
- ✅ Priorities : debug < info < notice < warn < err < crit < alert < emerg
- ✅ `journalctl -u service`, `-f`, `-b`, `-k`
- ✅ `/var/log/syslog` (Debian), `/var/log/messages` (Red Hat)
- ✅ `logger` pour écrire logs
- ✅ `logrotate` : daily/weekly/monthly, compress, rotate
- ✅ `mailq`, `newaliases`, `/etc/aliases`

### Pièges
- ❌ Confondre `hwclock --hctosys` et `--systohc`
- ❌ Oublier `newaliases` après modif `/etc/aliases`
- ❌ Confondre priorities rsyslog (err vs error)
- ❌ `journalctl -b` vs `-b -1` (boot actuel vs précédent)

### Astuces rapides
```bash
# Sync heure NTP
timedatectl set-ntp true

# Voir logs erreurs dernière heure
journalctl -p err --since "1 hour ago"

# Logs service SSH temps réel
journalctl -u sshd -f

# Tester config rsyslog
rsyslogd -N1

# Voir queue mails Postfix
mailq

# Forcer envoi queue
postqueue -f

# Vider queue complètement
postsuper -d ALL

# Rotation immédiate
logrotate -f /etc/logrotate.conf

# Écrire log custom
logger -p user.notice "Script terminé avec succès"
```

---

**💡 Conseil :** Maîtrisez `journalctl` (très fréquent !) et rsyslog (facility.priority). NTP avec `timedatectl set-ntp true` est simple.
