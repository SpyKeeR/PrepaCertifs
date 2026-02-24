# 📘 Notes de Révision - Sujet 108 : Services Système Essentiels

## 🎯 Objectifs du Sujet 108 (Poids: 10 points)

Le Sujet 108 couvre les services système essentiels pour l'administration Linux :

- **108.1** Gestion de l'horloge système (Poids: 3)
- **108.2** Journaux systèmes (Poids: 4)  
- **108.3** Bases sur l'agent de transfert de courrier (MTA) (Poids: 3)

---

## 📋 Table des matières

1. [108.1 - Gestion de l'horloge système](#1081---gestion-de-lhorloge-système)
2. [108.2 - Journaux systèmes](#1082---journaux-systèmes)
3. [108.3 - Bases sur l'agent de transfert de courrier](#1083---bases-sur-lagent-de-transfert-de-courrier)
4. [Checklist de révision](#checklist-de-révision)
5. [Exercices pratiques](#exercices-pratiques)
6. [Ressources supplémentaires](#ressources-supplémentaires)

---

# 108.1 - Gestion de l'horloge système

## 🎯 Objectifs clés

- Configuration de la date et de l'heure système
- Configuration de l'horloge matérielle en UTC
- Configuration du fuseau horaire
- Configuration NTP avec `ntpd` et `chrony`
- Connaissance du service pool.ntp.org

## 📚 Concepts fondamentaux

### Horloges système

Linux utilise **deux horloges distinctes** :

| Horloge | Description | Caractéristiques |
|---------|-------------|------------------|
| **Horloge système** | Maintenue par le système d'exploitation | Réglée au démarrage depuis l'horloge matérielle |
| **Horloge matérielle** (RTC) | Horloge en temps réel sur la carte mère | Fonctionne même ordinateur éteint |

### Heure locale et heure UTC

- **UTC** (Temps Universel Coordonné) : Heure à Greenwich (Royaume-Uni)
- **Heure locale** : UTC + décalage du fuseau horaire + heure d'été
- **Recommandation** : Toujours régler l'horloge matérielle en UTC

### Temps Unix (Epoch)

- Nombre de secondes depuis le **1er janvier 1970 à 00:00:00 UTC**
- Format interne utilisé par les systèmes Unix/Linux
- ⚠️ **Problème Y2038** : Sur systèmes 32 bits, dépassement le 19 janvier 2038

## 🔑 Commandes principales

### date - Afficher et modifier l'heure système

```bash
# Afficher l'heure locale
date

# Afficher l'heure UTC
date -u

# Formats standards
date -I                  # Format ISO 8601 (2024-01-15)
date -R                  # Format RFC 5322
date --rfc-3339=seconds  # Format RFC 3339

# Afficher en temps Unix
date +%s                 # 1705334515

# Formater une date spécifique
date --date='@1564013011'

# Régler l'heure système (root requis)
date --set="11 Nov 2024 11:11:11"
date +%Y%m%d -s "20241125"
date +%T -s "13:11:00"

# Déboguer une date
date --debug --date="Fri, 03 Jan 2024 14:00:17 -0500"
```

**Séquences de formatage courantes** :
- `%Y` : Année (2024)
- `%m` : Mois (01-12)
- `%d` : Jour (01-31)
- `%H` : Heure (00-23)
- `%M` : Minutes (00-59)
- `%S` : Secondes (00-59)
- `%s` : Temps Unix
- `%T` : Heure complète (HH:MM:SS)

### hwclock - Gérer l'horloge matérielle

```bash
# Afficher l'heure matérielle (root requis)
sudo hwclock

# Mode verbeux
sudo hwclock --verbose

# Synchroniser horloge matérielle → horloge système
sudo hwclock --hctosys

# Synchroniser horloge système → horloge matérielle
sudo hwclock --systohc

# Régler l'horloge matérielle manuellement
sudo hwclock --set --date "12/04/2024 11:15:19"
```

### timedatectl - Gestion unifiée sur systemd

```bash
# Afficher l'état date/heure
timedatectl

# Régler l'heure (désactive NTP automatiquement)
timedatectl set-time '2024-11-25 14:00:00'
timedatectl set-time '14:30:00'  # Heure seule

# Gestion du fuseau horaire
timedatectl list-timezones        # Lister tous les fuseaux
timedatectl list-timezones | grep Paris
timedatectl set-timezone Europe/Paris

# Gestion de NTP
timedatectl set-ntp yes   # Activer NTP
timedatectl set-ntp no    # Désactiver NTP
```

**Sortie typique de `timedatectl`** :
```
Local time: Thu 2024-12-05 11:08:05 CET
Universal time: Thu 2024-12-05 10:08:05 UTC
RTC time: Thu 2024-12-05 10:08:05
Time zone: Europe/Paris (CET, +0100)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

## 📁 Fichiers de configuration des fuseaux horaires

### /usr/share/zoneinfo/

```bash
# Arborescence des fuseaux horaires
ls /usr/share/zoneinfo/
# Africa/  America/  Antarctica/  Arctic/  Asia/  Atlantic/  
# Australia/  Europe/  Indian/  Pacific/

# Exemple pour la France
ls /usr/share/zoneinfo/Europe/ | grep Paris
# Paris
```

### /etc/localtime

```bash
# Lien symbolique vers le fuseau horaire actuel
ls -l /etc/localtime
# lrwxrwxrwx /etc/localtime -> /usr/share/zoneinfo/Europe/Paris

# Définir le fuseau horaire manuellement
sudo ln -sf /usr/share/zoneinfo/Canada/Eastern /etc/localtime

# Synchroniser l'horloge matérielle après changement
sudo hwclock --systohc
```

### /etc/timezone

```bash
# Représentation textuelle du fuseau horaire (pas toutes les distros)
cat /etc/timezone
# Europe/Paris
```

## 🌐 Network Time Protocol (NTP)

### Concepts NTP

| Concept | Description |
|---------|-------------|
| **Offset** | Différence entre heure système et heure NTP |
| **Step** | Changement brusque si offset > 128 ms |
| **Slew** | Ajustement progressif si offset < 128 ms |
| **Insane Time** | Si offset > 17 minutes, pas de changement automatique |
| **Drift** | Désynchronisation au fil du temps |
| **Jitter** | Dérive depuis la dernière requête NTP |
| **Stratum** | Distance par rapport à l'horloge de référence |

**Hiérarchie NTP** :
- **Stratum 0** : Horloges atomiques (références)
- **Stratum 1** : Serveurs connectés aux horloges de référence (non publics)
- **Stratum 2** : Serveurs accessibles au public
- **Stratum 3+** : Serveurs et clients

### timedatectl avec SNTP

```bash
# Vérifier le statut de synchronisation SNTP
timedatectl show-timesync --all

# Vérifier le service timesyncd
systemctl status systemd-timesyncd
```

### Configuration NTP avec ntpd

#### Fichier /etc/ntp.conf

```bash
# Serveurs NTP par défaut
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

# Syntaxe générale
server 192.168.1.100        # Adresse IP
server ntp.example.com       # URL (nécessite DNS)
pool pool.ntp.org            # Pool de serveurs
```

#### Gestion du service ntpd

```bash
# Vérifier le statut
systemctl status ntpd

# Démarrer et activer ntpd
sudo systemctl enable ntpd
sudo systemctl start ntpd

# Vérifier que le port 123 est en écoute
sudo netstat -nltp | grep 123
# tcp 0 0 0.0.0.0:123 0.0.0.0:* LISTEN 2263/ntpd
```

#### ntpdate - Synchronisation ponctuelle

```bash
# Arrêter ntpd
sudo systemctl stop ntpd

# Synchronisation manuelle (si offset > 17 minutes)
sudo ntpdate pool.ntp.org

# Redémarrer ntpd
sudo systemctl start ntpd
```

#### ntpq - Interroger le statut NTP

```bash
# Afficher les serveurs NTP
ntpq -p

# Sortie typique
#      remote           refid      st t when poll reach   delay   offset  jitter
# ==============================================================================
# +37.44.185.42    91.189.94.4     3 u   86  128  377  126.509  -20.398   6.838
# *inspektor-vlan1 121.131.112.137 2 u   17  128  377  112.878  -23.619   7.959

# Afficher les adresses IP
ntpq -pn

# Mode interactif
ntpq
ntpq> ?     # Liste des commandes
ntpq> peers # Afficher les serveurs
ntpq> quit
```

**Colonnes de `ntpq -p`** :
- `remote` : Nom d'hôte du serveur NTP
- `refid` : ID de référence du serveur
- `st` : Stratum du serveur
- `when` : Secondes depuis la dernière requête
- `poll` : Intervalle entre les requêtes (secondes)
- `reach` : État de connexion (377 = succès)
- `delay` : Délai requête/réponse (ms)
- `offset` : Différence système/NTP (ms)
- `jitter` : Variation lors de la dernière requête (ms)

### Configuration NTP avec chrony

#### Fichier /etc/chrony.conf

```bash
# Activer les serveurs NTP
server 0.arch.pool.ntp.org iburst
server 1.arch.pool.ntp.org iburst
pool 3.arch.pool.ntp.org iburst

# Autoriser ajustements importants
makestep 1.0 3
```

#### Gestion du service chronyd

```bash
# Démarrer et activer chronyd
sudo systemctl enable chronyd
sudo systemctl start chronyd

# Vérifier le statut
systemctl status chronyd
```

#### chronyc - Contrôler chrony

```bash
# Afficher l'état de synchronisation
chronyc tracking

# Sortie typique
# Reference ID    : 3265FB3D (bras-vprn-toroon2638w)
# Stratum         : 3
# System time     : 0.000134029 seconds fast of NTP time
# Last offset     : +0.000166506 seconds
# RMS offset      : 0.000470712 seconds
# Frequency       : 919.818 ppm slow

# Afficher les dernières données NTP
chronyc ntpdata

# Afficher les serveurs NTP
chronyc sources

# Effectuer un ajustement manuel
sudo chronyc makestep
```

### pool.ntp.org

- **Projet open source** de serveurs NTP bénévoles
- **Répartition de charge** entre plusieurs serveurs
- **Adresses régionalisées** : 
  - `0.pool.ntp.org`, `1.pool.ntp.org`, etc.
  - `0.fr.pool.ntp.org` (France)
  - `0.europe.pool.ntp.org` (Europe)

⚠️ **Avertissement** : Pour applications critiques, utiliser des serveurs NTP professionnels !

## 💡 Bonnes pratiques

### Recommandations générales

✅ **À faire** :
- Toujours utiliser UTC pour l'horloge matérielle
- Activer NTP pour la synchronisation automatique
- Synchroniser horloge matérielle après changement de fuseau horaire
- Utiliser `timedatectl` sur systèmes systemd
- Vérifier régulièrement la synchronisation NTP

❌ **À éviter** :
- Modifier l'heure système et matérielle sans NTP
- Utiliser l'heure locale pour l'horloge matérielle
- Oublier de synchroniser après changements manuels
- Exposer serveur NTP sans authentification

### Workflow de configuration

1. **Configuration initiale** :
   ```bash
   # Définir le fuseau horaire
   sudo timedatectl set-timezone Europe/Paris
   
   # Activer NTP
   sudo timedatectl set-ntp yes
   
   # Synchroniser l'horloge matérielle
   sudo hwclock --systohc
   ```

2. **Configuration serveur NTP local** :
   ```bash
   # Installer ntpd
   sudo apt install ntp
   
   # Configurer /etc/ntp.conf
   # server 0.fr.pool.ntp.org iburst
   
   # Démarrer le service
   sudo systemctl enable --now ntpd
   
   # Vérifier
   ntpq -p
   ```

3. **Dépannage** :
   ```bash
   # Vérifier l'heure actuelle
   timedatectl
   
   # Vérifier la dérive
   sudo hwclock --verbose
   
   # Vérifier les serveurs NTP
   ntpq -p  # ou chronyc sources
   
   # Forcer une synchronisation
   sudo systemctl stop ntpd
   sudo ntpdate pool.ntp.org
   sudo systemctl start ntpd
   ```

## 📝 Exemples pratiques

### Scénario 1 : Configuration complète d'un nouveau serveur

```bash
# 1. Vérifier l'état actuel
timedatectl

# 2. Définir le fuseau horaire
sudo timedatectl set-timezone Europe/Paris

# 3. Installer chrony
sudo apt install chrony

# 4. Configurer chrony
sudo nano /etc/chrony/chrony.conf
# Ajouter : server 0.fr.pool.ntp.org iburst

# 5. Redémarrer chrony
sudo systemctl restart chronyd

# 6. Vérifier la synchronisation
chronyc tracking

# 7. Synchroniser l'horloge matérielle
sudo hwclock --systohc
```

### Scénario 2 : Correction d'une heure incorrecte

```bash
# 1. Vérifier l'écart
timedatectl
chronyc tracking

# 2. Si offset > 17 minutes
sudo systemctl stop chronyd
sudo chronyd -q 'server pool.ntp.org iburst'
sudo systemctl start chronyd

# 3. Vérifier la correction
chronyc tracking
```

### Scénario 3 : Configuration d'un serveur NTP local

```bash
# Sur le serveur (192.168.1.100)
# /etc/ntp.conf
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst

# Sur les clients
# /etc/ntp.conf
server 192.168.1.100 iburst

# Redémarrer sur tous les systèmes
sudo systemctl restart ntpd
```

---

# 108.2 - Journaux systèmes

## 🎯 Objectifs clés

- Configuration de base de rsyslog
- Compréhension des ressources (facilities), priorités et actions
- Interrogation et filtrage du journal systemd (journald)
- Configuration du stockage persistant et gestion de la taille
- Interactions entre rsyslog et systemd-journald
- Configuration de logrotate

## 📚 Concepts fondamentaux

### Types de systèmes de journalisation

| Système | Description | Statut |
|---------|-------------|--------|
| **syslog** | Système de journalisation traditionnel | Obsolète |
| **syslog-ng** | Nouvelle génération de syslog | Utilisé |
| **rsyslog** | Système rapide et robuste | **Standard actuel** |
| **systemd-journald** | Journal systemd | **Standard moderne** |

### Fichiers de journalisation système

| Fichier | Contenu |
|---------|---------|
| `/var/log/syslog` | Tous les messages centralisés |
| `/var/log/auth.log` | Authentification (connexions, sudo, etc.) |
| `/var/log/kern.log` | Messages du noyau |
| `/var/log/messages` | Messages informatifs (pas noyau) |
| `/var/log/daemon.log` | Services/démons en arrière-plan |
| `/var/log/mail.log` | Serveur de messagerie |
| `/var/log/debug` | Messages de débogage |
| `/var/log/Xorg.0.log` | Serveur graphique X |
| `/var/run/utmp` | Connexions réussies actuelles |
| `/var/log/wtmp` | Historique connexions réussies |
| `/var/log/btmp` | Tentatives échouées |
| `/var/log/faillog` | Échecs d'authentification |
| `/var/log/lastlog` | Dernières connexions |

### Fichiers de journalisation des services

| Service | Emplacement |
|---------|-------------|
| **Apache** | `/var/log/apache2/` ou `/var/log/httpd/` |
| **MySQL** | `/var/log/mysql/` |
| **CUPS** | `/var/log/cups/` |
| **Samba** | `/var/log/samba/` |

## 🔑 Rsyslog

### Architecture rsyslog

```
Application → /dev/log (socket) → rsyslogd → Fichiers de journalisation
   ↓              ↓
Noyau  → /dev/kmsg (buffer) →
```

### Configuration - /etc/rsyslog.conf

#### Structure du fichier

```bash
#####################
#### MODULES     ####
#####################
module(load="imuxsock")  # Support journalisation locale
module(load="imklog")    # Support journalisation noyau

# Support UDP
#module(load="imudp")
#input(type="imudp" port="514")

# Support TCP
#module(load="imtcp")
#input(type="imtcp" port="514")

###############################
#### GLOBAL DIRECTIVES     ####
###############################
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat
$FileOwner root
$FileGroup adm
$FileCreateMode 0640
$DirCreateMode 0755
$WorkDirectory /var/spool/rsyslog

# Inclure configurations additionnelles
$IncludeConfig /etc/rsyslog.d/*.conf

#####################
#### RULES       ####
#####################
auth,authpriv.*                 /var/log/auth.log
*.*;auth,authpriv.none          -/var/log/syslog
kern.*                          -/var/log/kern.log
mail.*                          -/var/log/mail.log
```

### Ressources (Facilities)

| Numéro | Mot-clé | Description |
|--------|---------|-------------|
| 0 | kern | Messages du noyau Linux |
| 1 | user | Messages au niveau utilisateur |
| 2 | mail | Système de messagerie |
| 3 | daemon | Démons système |
| 4 | auth, authpriv | Sécurité/autorisation |
| 5 | syslog | Messages syslogd internes |
| 6 | lpr | Sous-système d'impression |
| 7 | news | Sous-système de news |
| 8 | uucp | Sous-système UUCP |
| 9 | cron | Démon cron |
| 10 | auth, authpriv | Sécurité/autorisation |
| 11 | ftp | Démon FTP |
| 12 | ntp | Démon NTP |
| 15 | cron | Démon cron |
| 16-23 | local0-local7 | Utilisation locale |

### Priorités (Sévérité)

| Numéro | Mot-clé | Description | Urgence |
|--------|---------|-------------|---------|
| 0 | emerg, panic | Système inutilisable | ⚠️⚠️⚠️ |
| 1 | alert | Action immédiate requise | ⚠️⚠️ |
| 2 | crit | Conditions critiques | ⚠️⚠️ |
| 3 | err, error | Conditions d'erreur | ⚠️ |
| 4 | warn, warning | Avertissements | ⚡ |
| 5 | notice | État normal mais significatif | 📋 |
| 6 | info | Messages informatifs | ℹ️ |
| 7 | debug | Messages de débogage | 🔧 |

**⚠️ Important** : Les priorités sont **hiérarchiquement inclusives**
- `mail.err` = erreur **et plus** (crit, alert, emerg)

### Syntaxe des règles

```bash
# Format général
<ressource>.<priorité> <action>

# Exemples
auth,authpriv.*                /var/log/auth.log
# Toutes (*) les priorités de auth et authpriv

*.*;auth,authpriv.none         -/var/log/syslog
# Tout sauf (.none) auth et authpriv
# Le "-" évite les écritures excessives

mail.err                       /var/log/mail.err
# Mail avec priorité error et plus

*.=debug;auth,authpriv.none    -/var/log/debug
# Uniquement (=) debug, sauf auth/authpriv

# Syntaxe avancée
mail.crit                      /var/log/mail.crit
mail.*                         -/var/log/mail.log
mail.info                      -/var/log/mail.info
kern.*                         /dev/console
*.emerg                        *  # À tous les utilisateurs
```

**Opérateurs** :
- `;` : Sépare plusieurs sélecteurs
- `,` : Combine plusieurs ressources
- `.none` : Exclut une ressource
- `=` : Priorité exacte (pas inclusive)
- `-` : Évite sync immédiat (performance)

## 🔧 Commandes de lecture des journaux

### Outils textuels

```bash
# less/more - Navigation page par page
sudo less /var/log/syslog
sudo more /var/log/auth.log

# tail - Dernières lignes
sudo tail /var/log/syslog          # 10 dernières lignes
sudo tail -n 50 /var/log/syslog    # 50 dernières lignes
sudo tail -f /var/log/syslog       # Suivi en temps réel

# head - Premières lignes
sudo head /var/log/syslog          # 10 premières lignes
sudo head -n 20 /var/log/syslog    # 20 premières lignes

# grep - Filtrage
sudo grep "error" /var/log/syslog
sudo grep "dhclient" /var/log/syslog
sudo grep -i "failed" /var/log/auth.log  # Insensible à la casse

# Journaux compressés
sudo zless /var/log/auth.log.3.gz
sudo zmore /var/log/syslog.2.gz
```

### Fichiers binaires spéciaux

```bash
# /var/log/wtmp - Connexions réussies
who
w
last

# /var/log/btmp - Tentatives échouées
sudo utmpdump /var/log/btmp
sudo last -f /var/log/btmp

# /var/log/faillog - Échecs d'authentification
sudo faillog -a | less

# /var/log/lastlog - Dernières connexions
lastlog | less
lastlog -u carol  # Pour utilisateur spécifique
```

### logger - Entrées manuelles

```bash
# Envoyer un message dans syslog
logger "Ceci est un message de test"

# Vérifier
sudo tail -1 /var/log/syslog
# Jan 17 17:55:33 debian carol: Ceci est un message de test

# Avec options
logger -t MON_APP "Message avec tag"
logger -p user.err "Message d'erreur utilisateur"
logger -i "Message avec PID"
```

## 📡 Rsyslog comme serveur centralisé

### Configuration serveur (192.168.1.6)

```bash
# /etc/rsyslog.d/remote.conf ou /etc/rsyslog.conf

# Activer réception TCP sur port 514
$ModLoad imtcp.so
$InputTCPServerRun 514

# OU réception UDP
#$ModLoad imudp.so
#$UDPServerRun 514

# Redémarrer rsyslog
sudo systemctl restart rsyslog

# Vérifier le port en écoute
sudo netstat -nltp | grep 514
# tcp 0 0 0.0.0.0:514 0.0.0.0:* LISTEN 2263/rsyslogd

# Ouvrir le pare-feu
sudo firewall-cmd --permanent --add-port=514/tcp
sudo firewall-cmd --reload
```

### Modèles et filtres

```bash
# Créer un modèle pour organiser les logs
$template RemoteLogs,"/var/log/remotehosts/%HOSTNAME%/%$NOW%.%syslogseverity-text%.log"

# Filtrer par IP source
if $fromhost-ip=='192.168.1.4' then ?RemoteLogs
& stop

# Résultat : /var/log/remotehosts/client-debian/2024-01-17.info.log
```

### Configuration client (192.168.1.4)

```bash
# /etc/rsyslog.conf

# Envoyer tous les logs au serveur via TCP port 514
*.* @@192.168.1.6:514

# OU via UDP (un seul @)
#*.* @192.168.1.6:514

# Redémarrer rsyslog
sudo systemctl restart rsyslog

# Tester
logger -t CLIENT "Test envoi vers serveur centralisé"
```

**Syntaxe d'envoi distant** :
- `@` : UDP
- `@@` : TCP
- `:514` : Port (optionnel si défaut 514)

## 🔄 Logrotate - Rotation des journaux

### Pourquoi la rotation ?

✅ **Avantages** :
- Empêche saturation du disque
- Facilite consultation des logs
- Améliore les performances
- Archive les anciens logs

### Configuration - /etc/logrotate.conf

```bash
# Options globales
weekly                 # Rotation hebdomadaire
rotate 4              # Conserver 4 semaines
create                # Créer nouveau fichier vide
#compress             # Compresser les anciens logs

# Inclure configurations spécifiques
include /etc/logrotate.d
```

### Configurations spécifiques - /etc/logrotate.d/

```bash
# /etc/logrotate.d/rsyslog
/var/log/syslog
/var/log/mail.log
/var/log/kern.log
{
    rotate 7           # Conserver 7 fichiers
    daily             # Rotation quotidienne
    missingok         # Pas d'erreur si fichier manquant
    notifempty        # Ne pas tourner si vide
    compress          # Compresser avec gzip
    delaycompress     # Reporter compression au prochain cycle
    sharedscripts     # Exécuter scripts une seule fois
    postrotate
        /usr/lib/rsyslog/rsyslog-rotate
    endscript
}
```

### Directives logrotate

| Directive | Description |
|-----------|-------------|
| `daily/weekly/monthly` | Fréquence de rotation |
| `rotate N` | Nombre de fichiers à conserver |
| `size 100M` | Rotation si taille > 100M |
| `compress` | Compression gzip |
| `delaycompress` | Reporter compression au cycle suivant |
| `missingok` | Pas d'erreur si fichier absent |
| `notifempty` | Ne pas tourner si vide |
| `create MODE USER GROUP` | Créer nouveau fichier avec permissions |
| `sharedscripts` | Scripts une seule fois pour plusieurs fichiers |
| `postrotate/endscript` | Script après rotation |
| `prerotate/endscript` | Script avant rotation |
| `copytruncate` | Copier puis tronquer (sans restart service) |

### Exemple de cycle de rotation

```
Avant rotation :
messages        (actuel)
messages.1      (semaine dernière)
messages.2.gz   (il y a 2 semaines)
messages.3.gz   (il y a 3 semaines)
messages.4.gz   (il y a 4 semaines)

Après rotation :
messages        (nouveau, vide)
messages.1      (actuel → semaine dernière)
messages.2.gz   (messages.1 → il y a 2 semaines)
messages.3.gz   (messages.2 → il y a 3 semaines)
messages.4.gz   (messages.3 → il y a 4 semaines)
                (messages.4.gz supprimé)
```

### Commandes logrotate

```bash
# Tester la configuration
sudo logrotate -d /etc/logrotate.conf

# Forcer la rotation
sudo logrotate -f /etc/logrotate.conf

# Rotation avec verbosité
sudo logrotate -v /etc/logrotate.conf

# Exécution automatique
ls /etc/cron.daily/logrotate
```

## 📊 Kernel Ring Buffer (dmesg)

```bash
# Afficher tous les messages du noyau
dmesg

# Filtrer par mot-clé
dmesg | grep usb
dmesg | grep error

# Avec niveaux de priorité lisibles
dmesg -H

# Suivre en temps réel
dmesg -w

# Afficher horodatages lisibles
dmesg -T

# Effacer le buffer (root)
sudo dmesg -C

# Niveau de log du noyau
cat /proc/sys/kernel/printk
# 4 4 1 7
# console_loglevel default_message_loglevel minimum_console_loglevel default_console_loglevel
```

## 🔷 systemd-journald

### Concepts de base

**Journal systemd** :
- Système de journalisation natif de systemd
- Fichiers **binaires** indexés
- **Centralisé** : tous les logs en un endroit
- Pas de rotation nécessaire (gestion automatique)
- Stockage volatile (RAM) ou persistant (disque)

### Configuration - /etc/systemd/journald.conf

```bash
[Journal]
# Emplacement du stockage
Storage=auto          # auto, volatile, persistent, none

# Taille maximale
SystemMaxUse=500M     # Maximum pour /var/log/journal/
RuntimeMaxUse=200M    # Maximum pour /run/log/journal/

# Espace libre à conserver
SystemKeepFree=1G
RuntimeKeepFree=100M

# Taille fichiers individuels
SystemMaxFileSize=100M
RuntimeMaxFileSize=50M

# Nombre de fichiers
SystemMaxFiles=100
RuntimeMaxFiles=100

# Durée de conservation
MaxRetentionSec=1month

# Redirection vers syslog
ForwardToSyslog=yes
ForwardToKMsg=no
ForwardToConsole=no
ForwardToWall=yes

# Compression
Compress=yes

# Niveau de log
MaxLevelStore=debug
MaxLevelSyslog=debug
```

### Modes de stockage

| Mode | Comportement |
|------|-------------|
| `auto` | `/var/log/journal/` si existe, sinon `/run/log/journal/` |
| `volatile` | RAM uniquement (`/run/log/journal/`) - perdu au reboot |
| `persistent` | Disque (`/var/log/journal/`) - crée répertoire si nécessaire |
| `none` | Désactivé (mais forwarding possible) |

### Activer le stockage persistant

```bash
# Méthode 1 : Créer le répertoire
sudo mkdir -p /var/log/journal
sudo systemctl restart systemd-journald

# Méthode 2 : Modifier la configuration
sudo nano /etc/systemd/journald.conf
# Storage=persistent
sudo systemctl restart systemd-journald

# Vérifier
sudo journalctl | grep "Journal started"
# Oct 05 21:33:49 debian systemd-journald[1768]: System journal (/var/log/journal/...) is 8.0M
```

## 🔍 journalctl - Interroger le journal

### Commandes de base

```bash
# Afficher tout le journal
sudo journalctl

# Dernières lignes (par défaut 10)
sudo journalctl -n
sudo journalctl -n 50

# Suivre en temps réel
sudo journalctl -f

# Ordre inverse (récent → ancien)
sudo journalctl -r

# Aller à la fin
sudo journalctl -e

# Messages du noyau (équivalent dmesg)
sudo journalctl -k
sudo journalctl --dmesg
```

### Filtrage par temps

```bash
# Depuis un moment donné
sudo journalctl --since "2024-01-15 10:00:00"
sudo journalctl --since "1 hour ago"
sudo journalctl --since "2 days ago"
sudo journalctl --since yesterday
sudo journalctl --since today

# Jusqu'à un moment donné
sudo journalctl --until "2024-01-15 15:00:00"
sudo journalctl --until "10 minutes ago"

# Intervalle de temps
sudo journalctl --since "2024-01-15 09:00" --until "2024-01-15 17:00"
sudo journalctl --since "1 hour ago" --until "30 minutes ago"

# Aujourd'hui uniquement
sudo journalctl --since today --until tomorrow
```

### Filtrage par boot

```bash
# Lister les boots
sudo journalctl --list-boots
# -2 xxxxxxxxxxx Mon 2024-01-15 08:00 - 09:00
# -1 yyyyyyyyyyy Mon 2024-01-15 09:15 - 10:30
#  0 zzzzzzzzzzz Mon 2024-01-15 10:45 - (en cours)

# Boot actuel
sudo journalctl -b
sudo journalctl -b 0

# Boot précédent
sudo journalctl -b -1

# Boot spécifique par ID
sudo journalctl -b zzzzzzzzzzz
```

### Filtrage par priorité

```bash
# Erreurs et plus grave
sudo journalctl -p err
sudo journalctl -p 3

# Uniquement warnings
sudo journalctl -p warning

# Plage de priorités
sudo journalctl -p warning..err
sudo journalctl -p 4..2

# Priorités disponibles
# emerg (0), alert (1), crit (2), err (3)
# warning (4), notice (5), info (6), debug (7)
```

### Filtrage par unité systemd

```bash
# Logs d'une unité spécifique
sudo journalctl -u ssh.service
sudo journalctl -u nginx.service
sudo journalctl -u systemd-journald.service

# Plusieurs unités
sudo journalctl -u ssh.service -u nginx.service

# Lister toutes les unités
systemctl list-units
systemctl list-unit-files
```

### Filtrage par champs

```bash
# Par PID
sudo journalctl _PID=1
sudo journalctl _PID=1234

# Par UID utilisateur
sudo journalctl _UID=1000
sudo journalctl _UID=0  # root

# Par GID groupe
sudo journalctl _GID=1000

# Par nom d'hôte
sudo journalctl _HOSTNAME=debian

# Par exécutable
sudo journalctl /usr/sbin/sshd
sudo journalctl /usr/bin/sudo

# Par nom de commande
sudo journalctl _COMM=sshd
sudo journalctl _COMM=sudo

# Par priorité (numérique)
sudo journalctl PRIORITY=3  # err
sudo journalctl PRIORITY=0  # emerg

# Par ressource syslog (numérique)
sudo journalctl SYSLOG_FACILITY=0  # kern
sudo journalctl SYSLOG_FACILITY=4  # auth

# Par transport
sudo journalctl _TRANSPORT=kernel
sudo journalctl _TRANSPORT=syslog
sudo journalctl _TRANSPORT=journal
```

### Combiner les filtres

```bash
# ET logique (tous les critères)
sudo journalctl PRIORITY=3 SYSLOG_FACILITY=0
# Priorité err ET ressource kern

# OU logique (+ entre expressions)
sudo journalctl PRIORITY=3 + SYSLOG_FACILITY=0
# Priorité err OU ressource kern

# Plusieurs valeurs pour même champ (OU)
sudo journalctl PRIORITY=1 PRIORITY=2 PRIORITY=3
# Priorités alert OU crit OU err

# Combinaisons complexes
sudo journalctl -u ssh.service -p err --since today
sudo journalctl -b -1 -p warning..err _UID=1000
```

### Formats de sortie

```bash
# Format court (par défaut)
sudo journalctl -o short

# Format verbeux (tous les champs)
sudo journalctl -o verbose

# Format JSON
sudo journalctl -o json
sudo journalctl -o json-pretty

# Format export (binaire)
sudo journalctl -o export

# Format pour suivi (cat)
sudo journalctl -o cat

# Sans pageur (sortie directe)
sudo journalctl --no-pager
```

### Navigation dans le pageur

**Déplacement** :
- `Espace`, `Page Down` : Page suivante
- `b`, `Page Up` : Page précédente
- `↓`, `↑` : Ligne par ligne
- `g` : Début
- `G` : Fin

**Recherche** :
- `/motif` : Rechercher vers le bas
- `?motif` : Rechercher vers le haut
- `n` : Occurrence suivante
- `N` : Occurrence précédente

**Quitter** :
- `q` : Quitter

## ✍️ systemd-cat - Entrées manuelles

```bash
# Entrée standard
systemd-cat
Message dans le journal
^D

# Avec pipe
echo "Message de test" | systemd-cat

# Depuis une commande
systemd-cat echo "Sortie de commande"

# Avec priorité
systemd-cat -p emerg echo "Urgence test"
systemd-cat -p warning echo "Avertissement"

# Avec identifiant
systemd-cat -t MON_APP echo "Message de mon application"

# Vérifier
sudo journalctl -n 5
```

## 🧹 Gestion de la taille du journal

### Vérifier l'utilisation

```bash
# Espace disque utilisé
sudo journalctl --disk-usage
# Archived and active journals take up 256.0M in the filesystem.

# Vérifier les fichiers
ls -lh /var/log/journal/*/
```

### Nettoyage manuel

```bash
# Par âge (supprimer > 2 semaines)
sudo journalctl --vacuum-time=2weeks
sudo journalctl --vacuum-time=1months
sudo journalctl --vacuum-time=1y

# Par taille (réduire à < 500M)
sudo journalctl --vacuum-size=500M
sudo journalctl --vacuum-size=1G

# Par nombre de fichiers (max 10)
sudo journalctl --vacuum-files=10

# Rotation des journaux actifs
sudo journalctl --rotate

# Puis nettoyage
sudo journalctl --rotate --vacuum-time=1s

# Vérifier l'intégrité
sudo journalctl --verify
```

### Configuration automatique

```bash
# /etc/systemd/journald.conf
[Journal]
SystemMaxUse=500M       # Max 500M au total
SystemKeepFree=1G       # Garder 1G libre
SystemMaxFileSize=100M  # Max 100M par fichier
SystemMaxFiles=100      # Max 100 fichiers
MaxRetentionSec=1month  # Conserver 1 mois

# Appliquer
sudo systemctl restart systemd-journald
```

## 💾 Récupération depuis système de secours

```bash
# Monter partition du système défaillant
sudo mount /dev/sda1 /mnt/rescue

# Lire les journaux
sudo journalctl -D /mnt/rescue/var/log/journal/

# OU avec --root
sudo journalctl --root=/mnt/rescue/

# Fusionner tous les journaux disponibles
sudo journalctl -m -D /mnt/rescue/var/log/journal/

# Lire un fichier spécifique
sudo journalctl --file=/mnt/rescue/var/log/journal/.../system.journal
```

## 🔗 Interaction rsyslog ↔ journald

### Configuration du forwarding

```bash
# /etc/systemd/journald.conf
[Journal]
# Envoyer vers syslog (rsyslog)
ForwardToSyslog=yes

# OU : rsyslog lit directement les journaux
Storage=persistent  # ou auto/volatile (pas none)

# Redémarrer
sudo systemctl restart systemd-journald
```

### Socket de communication

```bash
# Journald envoie vers
/run/systemd/journal/syslog

# rsyslog lit depuis ce socket
# /etc/rsyslog.conf
$ModLoad imuxsock
$SystemLogSocketName /run/systemd/journal/syslog
```

## 💡 Bonnes pratiques journalisation

### Recommandations

✅ **À faire** :
- Activer stockage persistant pour diagnostic post-crash
- Configurer rotation automatique
- Centraliser les logs sur serveur dédié
- Surveiller l'espace disque
- Sauvegarder les logs critiques
- Filtrer par priorité pour débogage ciblé
- Utiliser `journalctl -f` pour suivi en temps réel
- Vérifier régulièrement l'intégrité (`--verify`)

❌ **À éviter** :
- Stocker trop de logs sans rotation
- Négliger les logs d'erreur
- Supprimer manuellement des fichiers de log
- Désactiver la journalisation sur serveurs
- Ignorer les messages d'avertissement
- Oublier de synchroniser l'heure (logs incorrects)

---

# 108.3 - Bases sur l'agent de transfert de courrier

## 🎯 Objectifs clés

- Création des alias de courriel
- Transfert de courriel (forward)
- Connaissance des principaux serveurs SMTP (postfix, sendmail, exim)
- Utilisation de la couche d'émulation sendmail

## 📚 Concepts fondamentaux

### Architecture du courrier électronique

```
Utilisateur → MUA → MTA local → SMTP → MTA distant → Boîte de réception
                 (Mail User      (Mail Transfer
                  Agent)          Agent)
```

**Composants** :
- **MUA** (Mail User Agent) : Client de messagerie (Thunderbird, mail, mutt)
- **MTA** (Mail Transfer Agent) : Serveur de messagerie (sendmail, postfix, exim)
- **MDA** (Mail Delivery Agent) : Livraison locale (procmail, dovecot)
- **SMTP** : Simple Mail Transfer Protocol (port 25)
- **POP3** : Post Office Protocol v3 (port 110) - récupération
- **IMAP** : Internet Message Access Protocol (port 143) - synchronisation

### Protocoles

| Protocole | Port | Usage | Description |
|-----------|------|-------|-------------|
| **SMTP** | 25 | Envoi | Transfert entre MTA |
| **SMTP+Auth** | 587 | Envoi | Avec authentification (soumission) |
| **SMTPS** | 465 | Envoi | SMTP sur SSL/TLS |
| **POP3** | 110 | Réception | Téléchargement des messages |
| **POP3S** | 995 | Réception | POP3 sur SSL/TLS |
| **IMAP** | 143 | Réception | Synchronisation des messages |
| **IMAPS** | 993 | Réception | IMAP sur SSL/TLS |

### MTA disponibles pour Linux

| MTA | Caractéristiques | Usage |
|-----|------------------|-------|
| **Sendmail** | Traditionnel, très flexible, complexe | Systèmes legacy |
| **Postfix** | Moderne, performant, sécurisé | **Recommandé** |
| **Exim** | Flexible, utilisé par Debian | Distributions Debian |
| **qmail** | Sécurisé, modulaire | Niche |

## 📁 Structure des boîtes aux lettres

### Boîte de réception locale

```bash
# Format mbox (fichier unique)
/var/mail/carol
/var/spool/mail/carol

# Format Maildir (un fichier par message)
~/Maildir/
  ├── cur/     # Messages lus
  ├── new/     # Nouveaux messages
  └── tmp/     # Temporaires

# Vérifier le format
ls -la /var/mail/
ls -la /var/spool/mail/
```

### Format d'un message

```
From emma@lab1.campus Sat Nov 16 00:19:13 2024
Return-Path: <emma@lab1.campus>
Received: from lab1.campus (lab1.campus [10.0.3.134])
    by lab2.campus (8.15.2/8.15.2) with SMTP id xAG0G7Y0000595
    for dave@lab2.campus; Sat, 16 Nov 2024 00:17:06 GMT
Date: Sat, 16 Nov 2024 00:16:07 GMT
From: emma@lab1.campus
To: dave@lab2.campus
Subject: Test Message
Message-Id: <201911160017.xAG0G7Y0000595@lab2.campus>

Hi Dave, this is a test message.
```

## 🔑 Commandes principales

### sendmail - Envoyer du courrier

```bash
# Envoyer un message
sendmail dave@lab2.campus
From: emma@lab1.campus
To: dave@lab2.campus
Subject: Test

Bonjour Dave,
Ceci est un message de test.
.
(Ctrl+D ou . seul sur une ligne pour terminer)

# Avec redirection
echo "Corps du message" | sendmail -t destinataire@example.com

# Voir les messages en attente
sudo sendmail -bp
sudo mailq

# Forcer envoi de la file d'attente
sudo sendmail -q

# Initialiser base de données alias
sudo sendmail -bi
sudo sendmail -I
sudo newaliases
```

**Options sendmail** :
- `-bp` : Afficher la file d'attente (= mailq)
- `-q` : Traiter la file d'attente
- `-bi` : Initialiser base alias
- `-v` : Mode verbeux
- `-t` : Extraire destinataires des en-têtes

### mail (mailx) - Client de messagerie

#### Mode lecture

```bash
# Lire les messages
mail

# Commandes interactives
mail> ?              # Aide
mail> 1              # Lire message 1
mail> p 1            # Print message 1
mail> d 1            # Delete message 1
mail> r 1            # Reply to message 1
mail> h              # Liste des en-têtes
mail> q              # Quitter (sauvegarde changements)
mail> x              # Quitter (annule changements)
```

#### Mode envoi

```bash
# Envoi simple
mail dave@lab2.campus
Subject: Test
Corps du message
.
(Ctrl+D pour terminer)

# Avec sujet en ligne de commande
mail -s "Sujet du message" dave@lab2.campus
Corps du message
^D

# Avec fichier comme corps
mail -s "Logs du système" admin@example.com < /var/log/syslog

# Avec redirection Hereline
mail -s "Alerte" admin@example.com <<< "Le service a redémarré à $(date)"

# Avec pièce jointe (mailx)
uname -a | mail -s "Info système" -a /var/log/syslog admin@example.com
mail -s "Rapport" -a rapport.pdf admin@example.com < message.txt

# Envoi automatisé depuis script
{
    echo "Statut : OK"
    echo "Date : $(date)"
    echo ""
    df -h
} | mail -s "Rapport quotidien" admin@example.com
```

### mailq - File d'attente

```bash
# Afficher la file d'attente
mailq
sudo mailq

# Exemple de sortie
/var/spool/mqueue (1 request)
-----Q-ID----- --Size-- -----Q-Time----- ------------Sender/Recipient-----------
xAIK3D9S000453 36 Mon Nov 18 20:03 <emma@lab1.campus>
(Deferred: Connection refused by lab2.campus.)
<dave@lab2.campus>

Total requests: 1

# Équivalent
sendmail -bp
```

## 📋 Alias de messagerie

### /etc/aliases - Alias système

```bash
# Format : alias: destination
# /etc/aliases

# Redirection vers utilisateur local
postmaster: root
webmaster: carol

# Redirection vers adresse externe
admin: administrateur@example.com

# Multiple destinations (liste)
support: carol,dave,emma

# Fichier d'inclusion
team: :include:/etc/mail/team-list.txt

# Redirection vers fichier
logs: /var/log/mail-archive.log

# Redirection vers programme
subscribe: |/usr/local/bin/subscribe.sh
alerts: |"/usr/local/bin/process-alert.sh"

# Combinaisons
all: carol, dave, :include:/etc/mail/users.txt
```

**Activer les alias** :
```bash
# Après modification de /etc/aliases
sudo newaliases

# OU
sudo sendmail -bi
sudo sendmail -I

# Vérifier la base générée
ls -l /etc/aliases.db
```

### ~/.forward - Alias utilisateur

```bash
# Redirection personnelle
# ~/forward (utilisateur carol)

# Vers adresse externe
emma@lab1.campus

# Vers plusieurs destinations
dave@lab2.campus
emma@lab1.campus

# Vers fichier
/home/carol/mail-archive.txt

# Vers programme
|/home/carol/bin/filter-mail.sh

# Garder copie locale ET transférer
\carol
emma@lab1.campus
```

**Important** :
- Pas besoin de `newaliases` pour `.forward`
- Doit être lisible uniquement par le propriétaire :
  ```bash
  chmod 644 ~/.forward  # Lisible par tous
  # OU
  chmod 600 ~/.forward  # Recommandé
  ```

## 🌐 SMTP - Commandes de base

### Communication SMTP manuelle

```bash
# Se connecter au MTA avec nc (netcat)
nc lab2.campus 25

# Ou telnet
telnet lab2.campus 25

# Session SMTP
220 lab2.campus ESMTP Sendmail ready
HELO lab1.campus
250 lab2.campus Hello lab1.campus [10.0.3.134]
MAIL FROM: <emma@lab1.campus>
250 2.1.0 Sender ok
RCPT TO: <dave@lab2.campus>
250 2.1.5 Recipient ok
DATA
354 Enter mail, end with "." on a line by itself
Subject: Test SMTP

Ceci est un test SMTP direct.
.
250 2.0.0 Message accepted for delivery
QUIT
221 2.0.0 Closing connection
```

**Commandes SMTP** :
- `HELO hostname` : Identification (SMTP basique)
- `EHLO hostname` : Identification (SMTP étendu)
- `MAIL FROM:<email>` : Expéditeur
- `RCPT TO:<email>` : Destinataire
- `DATA` : Corps du message (terminer par `.` seul)
- `RSET` : Réinitialiser la session
- `VRFY user` : Vérifier existence utilisateur
- `NOOP` : Pas d'opération (keep-alive)
- `QUIT` : Fermer connexion

**Codes de réponse** :
- `2xx` : Succès
- `3xx` : Information supplémentaire requise
- `4xx` : Erreur temporaire
- `5xx` : Erreur permanente

### Exemples de codes

```
220 Service ready
250 Requested action completed
354 Start mail input
421 Service not available
450 Requested action not taken (mailbox busy)
451 Requested action aborted (error in processing)
500 Syntax error
550 Requested action not taken (mailbox unavailable)
551 User not local
552 Requested action aborted (exceeded storage)
```

## 📧 Postfix (recommandé)

### Installation

```bash
# Debian/Ubuntu
sudo apt install postfix

# Configuration interactive
sudo dpkg-reconfigure postfix

# Fedora/CentOS
sudo dnf install postfix

# Démarrer le service
sudo systemctl enable --now postfix
```

### Fichiers de configuration

```bash
# Configuration principale
/etc/postfix/main.cf

# Exemples de paramètres
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain
inet_interfaces = all
mydestination = $myhostname, localhost.$mydomain, $mydomain
mynetworks = 127.0.0.0/8, 192.168.1.0/24

# Alias
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases

# Appliquer les changements
sudo postfix reload
sudo systemctl reload postfix
```

### Commandes Postfix

```bash
# Vérifier la configuration
sudo postfix check

# Recharger la configuration
sudo postfix reload

# Voir la file d'attente
postqueue -p
mailq

# Vider la file d'attente
sudo postqueue -f

# Supprimer un message
sudo postsuper -d MESSAGE_ID

# Supprimer tous les messages
sudo postsuper -d ALL

# Logs
sudo tail -f /var/log/mail.log
```

## 🔒 Sécurité MTA

### Problèmes courants

⚠️ **Open Relay** : MTA qui relaie tous les messages sans restriction
- **Risque** : Spam, blacklisting IP
- **Solution** : Restreindre les connexions autorisées

### Protection

```bash
# Postfix - Restreindre relais
# /etc/postfix/main.cf
smtpd_relay_restrictions = permit_mynetworks, reject_unauth_destination
mynetworks = 127.0.0.0/8, 192.168.1.0/24

# Sendmail - Restreindre connexions
# /etc/mail/sendmail.mc
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl

# Régénérer sendmail.cf
cd /etc/mail
sudo m4 sendmail.mc > sendmail.cf
sudo systemctl restart sendmail
```

### DNS MX Records

```bash
# Vérifier les enregistrements MX
dig example.com MX
nslookup -type=MX example.com
host -t MX example.com

# Exemple de sortie
example.com.    3600    IN  MX  10 mail1.example.com.
example.com.    3600    IN  MX  20 mail2.example.com.

# Priorité : plus petit nombre = priorité plus haute
```

## 🔧 Dépannage

### Vérifications de base

```bash
# 1. Service en cours d'exécution
sudo systemctl status postfix
sudo systemctl status sendmail

# 2. Port SMTP en écoute
sudo netstat -tlnp | grep :25
sudo ss -tlnp | grep :25

# 3. Logs en temps réel
sudo tail -f /var/log/mail.log
sudo tail -f /var/log/maillog

# 4. File d'attente
mailq

# 5. Tester envoi local
echo "Test" | mail -s "Test local" $USER

# 6. Tester envoi SMTP
nc localhost 25
# HELO localhost
# MAIL FROM:<test@localhost>
# RCPT TO:<user@localhost>
# DATA
# Test
# .
# QUIT
```

### Problèmes fréquents

| Problème | Cause possible | Solution |
|----------|----------------|----------|
| Messages en queue | MTA distant injoignable | Vérifier DNS, réseau |
| Permission denied | Mauvaises permissions /var/mail | `chmod 1777 /var/mail` |
| Relaying denied | Restriction relay | Configurer mynetworks |
| Connection refused | Service arrêté / pare-feu | Démarrer service, ouvrir port 25 |
| User unknown | Utilisateur inexistant | Vérifier alias |

## 💡 Bonnes pratiques

### Recommandations

✅ **À faire** :
- Utiliser Postfix pour nouveaux déploiements
- Configurer DNS MX correctement
- Restreindre le relais aux réseaux autorisés
- Implémenter SPF, DKIM, DMARC pour production
- Surveiller les logs régulièrement
- Chiffrer les communications (TLS/SSL)
- Maintenir les alias à jour

❌ **À éviter** :
- Laisser un open relay
- Exposer MTA sans authentification
- Ignorer les messages en queue
- Négliger les mises à jour de sécurité
- Utiliser des mots de passe faibles

### Configuration minimale sécurisée

```bash
# Postfix - /etc/postfix/main.cf
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain

# Écouter uniquement sur localhost
inet_interfaces = localhost

# Restreindre destinations
mydestination = $myhostname, localhost

# Restreindre relais
mynetworks = 127.0.0.0/8
smtpd_relay_restrictions = permit_mynetworks, reject

# TLS (optionnel mais recommandé)
smtpd_tls_cert_file = /etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file = /etc/ssl/private/ssl-cert-snakeoil.key
smtpd_tls_security_level = may
```

## 📝 Exemples pratiques

### Scénario 1 : Redirection de tous les e-mails root

```bash
# /etc/aliases
root: admin@example.com

# Appliquer
sudo newaliases

# Tester
echo "Test admin" | sudo mail -s "Test root" root
```

### Scénario 2 : Liste de diffusion

```bash
# Créer fichier de liste
sudo nano /etc/mail/equipe.txt
carol@example.com
dave@example.com
emma@example.com

# /etc/aliases
equipe: :include:/etc/mail/equipe.txt

# Appliquer
sudo newaliases

# Tester
echo "Message à l'équipe" | mail -s "Info équipe" equipe
```

### Scénario 3 : Archivage automatique

```bash
# /etc/aliases
archive: /var/mail/archive.mbox

# Créer fichier avec bonnes permissions
sudo touch /var/mail/archive.mbox
sudo chown mail:mail /var/mail/archive.mbox
sudo chmod 660 /var/mail/archive.mbox

# Appliquer
sudo newaliases
```

### Scénario 4 : Traitement par script

```bash
# Script de traitement
sudo nano /usr/local/bin/process-mail.sh

#!/bin/bash
# Lire depuis stdin
cat >> /var/log/processed-mail.log
# Envoyer notification
echo "Mail traité à $(date)" | mail -s "Notification" admin@localhost

# Permissions
sudo chmod +x /usr/local/bin/process-mail.sh

# Si sendmail en mode restricted shell
sudo ln -s /usr/local/bin/process-mail.sh /etc/smrsh/

# /etc/aliases
processed: |/usr/local/bin/process-mail.sh

# Appliquer
sudo newaliases
```

---

# 📋 Checklist de révision

## 108.1 - Gestion de l'horloge système

- [ ] Comprendre la différence entre horloge système et horloge matérielle
- [ ] Utiliser `date` pour afficher et modifier l'heure
- [ ] Utiliser `hwclock` pour gérer l'horloge matérielle
- [ ] Maîtriser `timedatectl` sur systèmes systemd
- [ ] Configurer un fuseau horaire avec `/etc/localtime`
- [ ] Comprendre les concepts NTP (offset, drift, stratum, jitter)
- [ ] Configurer `ntpd` avec `/etc/ntp.conf`
- [ ] Configurer `chrony` avec `/etc/chrony.conf`
- [ ] Utiliser `ntpq` et `chronyc` pour diagnostiquer NTP
- [ ] Connaître pool.ntp.org et son utilisation
- [ ] Synchroniser horloge système ↔ horloge matérielle
- [ ] Comprendre le temps Unix et le problème Y2038

## 108.2 - Journaux systèmes

- [ ] Comprendre l'architecture de rsyslog
- [ ] Connaître les fichiers de journalisation dans `/var/log/`
- [ ] Maîtriser les ressources (facilities) syslog
- [ ] Maîtriser les priorités (sévérité) syslog
- [ ] Écrire des règles rsyslog dans `/etc/rsyslog.conf`
- [ ] Utiliser `logger` pour entrées manuelles
- [ ] Configurer rsyslog comme serveur centralisé
- [ ] Créer des modèles et filtres rsyslog
- [ ] Comprendre et configurer logrotate
- [ ] Lire `/etc/logrotate.conf` et `/etc/logrotate.d/`
- [ ] Utiliser `dmesg` pour le kernel ring buffer
- [ ] Comprendre systemd-journald et son stockage
- [ ] Maîtriser `journalctl` et ses options de filtrage
- [ ] Configurer le stockage persistant du journal
- [ ] Gérer la taille du journal avec vacuum
- [ ] Utiliser `systemd-cat` pour entrées manuelles
- [ ] Comprendre l'interaction rsyslog ↔ journald

## 108.3 - Agent de transfert de courrier

- [ ] Comprendre l'architecture MUA/MTA/MDA
- [ ] Connaître les protocoles SMTP, POP3, IMAP
- [ ] Connaître les MTA : sendmail, postfix, exim, qmail
- [ ] Utiliser `sendmail` pour envoyer du courrier
- [ ] Utiliser la commande `mail` (mailx)
- [ ] Utiliser `mailq` pour voir la file d'attente
- [ ] Créer des alias dans `/etc/aliases`
- [ ] Utiliser `newaliases` pour mettre à jour la base
- [ ] Créer des alias personnels avec `~/.forward`
- [ ] Comprendre les commandes SMTP de base
- [ ] Connaître les codes de réponse SMTP
- [ ] Comprendre les enregistrements DNS MX
- [ ] Identifier et éviter les open relays
- [ ] Dépanner les problèmes de livraison de courrier

---

# 🏋️ Exercices pratiques

## Exercice 1 : Configuration complète de l'heure

**Objectif** : Configurer correctement l'heure sur un nouveau serveur.

```bash
# 1. Vérifier l'état actuel
timedatectl

# 2. Lister les fuseaux horaires disponibles
timedatectl list-timezones | grep Paris

# 3. Définir le fuseau horaire
sudo timedatectl set-timezone Europe/Paris

# 4. Vérifier la synchronisation NTP
systemctl status systemd-timesyncd

# 5. Activer NTP si désactivé
sudo timedatectl set-ntp yes

# 6. Vérifier la synchronisation
timedatectl show-timesync --all

# 7. Synchroniser l'horloge matérielle
sudo hwclock --systohc

# 8. Vérifier le résultat
timedatectl
sudo hwclock --verbose
```

## Exercice 2 : Configuration serveur NTP avec chrony

**Objectif** : Mettre en place un serveur NTP local.

```bash
# 1. Installer chrony
sudo apt install chrony

# 2. Configurer /etc/chrony/chrony.conf
sudo nano /etc/chrony/chrony.conf

# Ajouter :
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

# Autoriser le réseau local
allow 192.168.1.0/24

makestep 1.0 3

# 3. Redémarrer chrony
sudo systemctl restart chronyd

# 4. Vérifier le statut
chronyc tracking
chronyc sources

# 5. Ouvrir le pare-feu (si nécessaire)
sudo firewall-cmd --permanent --add-service=ntp
sudo firewall-cmd --reload

# 6. Tester depuis un client
# Sur le client : /etc/chrony/chrony.conf
# server 192.168.1.100 iburst
```

## Exercice 3 : Analyse des journaux avec rsyslog

**Objectif** : Configurer et analyser la journalisation système.

```bash
# 1. Examiner la configuration rsyslog
sudo less /etc/rsyslog.conf

# 2. Créer une règle personnalisée
sudo nano /etc/rsyslog.d/50-custom.conf

# Ajouter :
# Tous les messages d'erreur dans un fichier séparé
*.err     /var/log/errors.log

# Messages kern dans un fichier dédié
kern.*    /var/log/kernel.log

# 3. Redémarrer rsyslog
sudo systemctl restart rsyslog

# 4. Envoyer des messages de test
logger -p user.err "Erreur de test utilisateur"
logger -p kern.info "Message noyau de test"

# 5. Vérifier les logs
sudo tail /var/log/errors.log
sudo tail /var/log/kernel.log
sudo grep "test" /var/log/syslog

# 6. Analyser les tentatives de connexion échouées
sudo grep "Failed password" /var/log/auth.log

# 7. Voir les dernières connexions réussies
last -10
```

## Exercice 4 : Configuration serveur de logs centralisé

**Objectif** : Mettre en place un serveur de logs centralisé avec rsyslog.

**Serveur (192.168.1.10)** :
```bash
# 1. Configuration TCP
sudo nano /etc/rsyslog.d/remote.conf

# Ajouter :
module(load="imtcp")
input(type="imtcp" port="514")

# Modèle pour logs distants
$template RemoteLogs,"/var/log/remote/%HOSTNAME%/%$NOW%.log"

# Filtrer par IP
if $fromhost-ip=='192.168.1.20' then ?RemoteLogs
& stop

# 2. Redémarrer
sudo systemctl restart rsyslog

# 3. Vérifier le port
sudo netstat -tlnp | grep 514

# 4. Pare-feu
sudo firewall-cmd --permanent --add-port=514/tcp
sudo firewall-cmd --reload
```

**Client (192.168.1.20)** :
```bash
# Configuration
sudo nano /etc/rsyslog.conf

# Ajouter à la fin :
*.* @@192.168.1.10:514

# Redémarrer
sudo systemctl restart rsyslog

# Tester
logger -t CLIENT-TEST "Message depuis le client"

# Vérifier sur le serveur
# sudo tail /var/log/remote/client-hostname/...
```

## Exercice 5 : Maîtriser journalctl

**Objectif** : Utiliser journalctl pour diagnostiquer des problèmes.

```bash
# 1. Afficher les erreurs du boot actuel
sudo journalctl -b -p err

# 2. Voir les logs SSH des dernières 24h
sudo journalctl -u ssh.service --since "24 hours ago"

# 3. Suivre les logs en temps réel
sudo journalctl -f

# 4. Afficher les logs d'un utilisateur spécifique
sudo journalctl _UID=1000

# 5. Chercher des patterns spécifiques
sudo journalctl | grep -i "failed"

# 6. Exporter en JSON
sudo journalctl -u nginx.service -o json-pretty > nginx.json

# 7. Vérifier l'espace disque
sudo journalctl --disk-usage

# 8. Nettoyer les vieux logs (> 2 semaines)
sudo journalctl --vacuum-time=2weeks

# 9. Voir les boots disponibles
sudo journalctl --list-boots

# 10. Analyser un boot spécifique
sudo journalctl -b -1 -p warning
```

## Exercice 6 : Configuration logrotate personnalisée

**Objectif** : Configurer la rotation pour un log applicatif.

```bash
# 1. Créer configuration
sudo nano /etc/logrotate.d/monapp

/var/log/monapp/*.log {
    daily                # Rotation quotidienne
    rotate 14            # Conserver 14 jours
    compress             # Compresser
    delaycompress        # Compression différée
    missingok            # Pas d'erreur si manquant
    notifempty           # Ne pas tourner si vide
    create 0640 www-data adm  # Nouvelles permissions
    sharedscripts
    postrotate
        systemctl reload monapp > /dev/null 2>&1 || true
    endscript
}

# 2. Tester la configuration
sudo logrotate -d /etc/logrotate.d/monapp

# 3. Forcer une rotation
sudo logrotate -f /etc/logrotate.d/monapp

# 4. Vérifier le résultat
ls -lh /var/log/monapp/
```

## Exercice 7 : Configuration MTA avec Postfix

**Objectif** : Installer et configurer Postfix pour courrier local.

```bash
# 1. Installer Postfix
sudo apt install postfix

# 2. Configuration de base
sudo nano /etc/postfix/main.cf

# Paramètres essentiels :
myhostname = server.example.local
mydomain = example.local
myorigin = $mydomain
mydestination = $myhostname, localhost.$mydomain, localhost
inet_interfaces = loopback-only
mynetworks = 127.0.0.0/8

# 3. Redémarrer Postfix
sudo systemctl restart postfix

# 4. Vérifier la configuration
sudo postfix check

# 5. Tester envoi local
echo "Test Postfix" | mail -s "Test local" $USER

# 6. Vérifier réception
mail

# 7. Voir la file d'attente
mailq

# 8. Surveiller les logs
sudo tail -f /var/log/mail.log
```

## Exercice 8 : Configuration des alias

**Objectif** : Mettre en place un système d'alias complet.

```bash
# 1. Créer liste d'équipe
sudo nano /etc/mail/equipe.txt

alice@example.com
bob@example.com
carol@example.com

# 2. Configurer /etc/aliases
sudo nano /etc/aliases

# Ajouter :
# Redirections individuelles
postmaster: root
webmaster: alice
hostmaster: bob

# Liste de diffusion
equipe: :include:/etc/mail/equipe.txt

# Redirection externe
backup: sauvegarde@external.com

# Archive
archive: /var/mail/archive.mbox

# 3. Créer fichier archive
sudo touch /var/mail/archive.mbox
sudo chown mail:mail /var/mail/archive.mbox
sudo chmod 660 /var/mail/archive.mbox

# 4. Appliquer
sudo newaliases

# 5. Tester
echo "Test alias equipe" | mail -s "Test" equipe
echo "Test archive" | mail -s "Archive" archive

# 6. Vérifier
sudo tail /var/mail/archive.mbox
```

## Exercice 9 : Transfert utilisateur avec ~/.forward

**Objectif** : Configurer le transfert personnel de courrier.

```bash
# 1. Créer ~/.forward
nano ~/.forward

# Ajouter :
# Garder copie locale
\$USER
# Transférer vers externe
mon.email.perso@gmail.com
# Transférer vers autre serveur
utilisateur@autre-serveur.com

# 2. Permissions correctes
chmod 644 ~/.forward

# 3. Tester
echo "Test forward" | mail -s "Test" $USER

# 4. Vérifier :
# - Copie locale dans /var/mail/$USER
# - Email reçu sur adresses externes
```

## Exercice 10 : Dépannage complet

**Scénario** : Les e-mails ne sont pas livrés.

```bash
# 1. Vérifier le service MTA
sudo systemctl status postfix
sudo systemctl status sendmail

# 2. Vérifier le port SMTP
sudo netstat -tlnp | grep :25
sudo ss -tlnp | grep :25

# 3. Examiner la file d'attente
mailq

# 4. Analyser les logs
sudo tail -50 /var/log/mail.log
sudo grep "error" /var/log/mail.log
sudo grep "warning" /var/log/mail.log

# 5. Tester SMTP localement
nc localhost 25
HELO localhost
MAIL FROM:<test@localhost>
RCPT TO:<$USER@localhost>
DATA
Subject: Test

Test message
.
QUIT

# 6. Vérifier DNS MX
dig example.com MX
host -t MX example.com

# 7. Vérifier les alias
sudo cat /etc/aliases | grep -v "^#"
ls -l /etc/aliases.db

# 8. Vérifier permissions
ls -ld /var/mail
ls -l /var/mail/$USER

# 9. Forcer traitement file d'attente
sudo postfix flush
sudo sendmail -q

# 10. Tester avec verbosité
echo "Test verbose" | sendmail -v $USER@localhost
```

---

# 📚 Ressources supplémentaires

## Documentation officielle

### Gestion du temps
- `man date` - Commande date
- `man hwclock` - Horloge matérielle
- `man timedatectl` - Gestion systemd du temps
- `man ntpd` - Démon NTP
- `man ntp.conf` - Configuration NTP
- `man chrony` - Démon chrony
- `man chrony.conf` - Configuration chrony
- `man chronyd` - Démon chronyd
- `man chronyc` - Commande chronyc

### Journalisation
- `man rsyslogd` - Démon rsyslog
- `man rsyslog.conf` - Configuration rsyslog
- `man logger` - Commande logger
- `man logrotate` - Rotation des logs
- `man logrotate.conf` - Configuration logrotate
- `man dmesg` - Buffer du noyau
- `man systemd-journald` - Démon journal systemd
- `man journald.conf` - Configuration journald
- `man journalctl` - Commande journalctl
- `man systemd-cat` - Entrées journal
- `man systemd.journal-fields` - Champs du journal

### Courrier électronique
- `man sendmail` - Commande sendmail
- `man mail` - Client mail
- `man mailx` - Client mailx étendu
- `man mailq` - File d'attente
- `man aliases` - Format aliases
- `man newaliases` - Mise à jour alias
- `man postfix` - MTA Postfix
- `man postconf` - Configuration Postfix
- `man postqueue` - File Postfix
- `man postsuper` - Administration Postfix

## Sites web utiles

- [NTP Pool Project](https://www.ntppool.org/) - Serveurs NTP publics
- [Rsyslog Documentation](https://www.rsyslog.com/doc/) - Doc officielle rsyslog
- [Systemd Journal](https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html) - Doc journald
- [Postfix Documentation](http://www.postfix.org/documentation.html) - Doc officielle Postfix
- [RFC 5322](https://tools.ietf.org/html/rfc5322) - Format messages Internet

## Commandes de référence rapide

### Temps
```bash
date                           # Heure actuelle
timedatectl                    # État complet
hwclock --systohc              # Sync système → matériel
ntpq -p                        # État NTP
chronyc tracking               # État chrony
```

### Logs
```bash
sudo tail -f /var/log/syslog   # Suivi temps réel
logger "message"               # Entrée manuelle
sudo journalctl -f             # Suivi journal systemd
sudo journalctl -xe            # Dernières entrées avec explications
mailq                          # File d'attente mail
```

### Mail
```bash
mail                           # Lire courrier
echo "msg" | mail user         # Envoyer message
sudo newaliases                # MAJ alias
mailq                          # File d'attente
```

---

**🎯 Bon courage pour votre révision du Sujet 108 !**

*Ce document couvre l'ensemble des objectifs du Sujet 108 pour l'examen LPIC-1 102-500.*
