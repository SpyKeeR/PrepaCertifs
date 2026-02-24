# 📝 QCM - Sujet 108 : Services Système Essentiels

## 🎯 Informations sur le QCM

- **Sujet** : 108 - Services Système Essentiels
- **Nombre de questions** : 50
- **Poids du sujet** : 10 points
- **Durée estimée** : 60 minutes

### Répartition des questions

- **108.1** - Gestion de l'horloge système : 20 questions
- **108.2** - Journaux systèmes : 20 questions
- **108.3** - Agent de transfert de courrier : 10 questions

---

## 📋 Questions

### 108.1 - Gestion de l'horloge système (20 questions)

#### Question 1
Quelle est la différence entre l'horloge système et l'horloge matérielle sous Linux ?

- [ ] A) Il n'y a aucune différence, ce sont deux noms pour la même horloge  
- [ ] B) L'horloge système est maintenue par le système d'exploitation, l'horloge matérielle est sur la carte mère  
- [ ] C) L'horloge système est plus précise que l'horloge matérielle  
- [ ] D) L'horloge matérielle ne fonctionne que lorsque l'ordinateur est allumé  

#### Question 2
Quelle commande affiche l'heure UTC actuelle ?

- [ ] A) `date --utc`  
- [ ] B) `date -u`  
- [ ] C) `hwclock --utc`  
- [ ] D) `timedatectl show-utc`  

#### Question 3
Comment régler l'horloge système sur la date "25 décembre 2025 à 14:30:00" avec la commande `date` ?

- [ ] A) `date --set="25/12/2025 14:30:00"`  
- [ ] B) `date -s "Dec 25 2025 14:30:00"`  
- [ ] C) `date --set="2025-12-25 14:30:00"`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 4
Que fait la commande `hwclock --systohc` ?

- [ ] A) Synchronise l'horloge système depuis l'horloge matérielle  
- [ ] B) Synchronise l'horloge matérielle depuis l'horloge système  
- [ ] C) Affiche les deux horloges côte à côte  
- [ ] D) Réinitialise l'horloge matérielle  

#### Question 5
Quel est le rôle du fichier `/etc/localtime` ?

- [ ] A) Stocker l'heure locale actuelle  
- [ ] B) Définir le fuseau horaire du système  
- [ ] C) Configurer le format d'affichage de l'heure  
- [ ] D) Enregistrer l'historique des changements d'heure  

#### Question 6
Comment définir le fuseau horaire sur "Europe/Paris" avec `timedatectl` ?

- [ ] A) `timedatectl set-timezone Europe/Paris`  
- [ ] B) `timedatectl timezone Europe/Paris`  
- [ ] C) `timedatectl --timezone=Europe/Paris`  
- [ ] D) `timedatectl config timezone Europe/Paris`  

#### Question 7
Que signifie "offset" dans le contexte NTP ?

- [ ] A) Le décalage entre l'heure système et l'heure NTP  
- [ ] B) La vitesse de dérive de l'horloge  
- [ ] C) Le numéro de stratum du serveur  
- [ ] D) Le délai de transmission réseau  

#### Question 8
Quelle est la signification d'un stratum 2 dans la hiérarchie NTP ?

- [ ] A) Serveur directement connecté à une horloge de référence  
- [ ] B) Serveur synchronisé avec un serveur stratum 1  
- [ ] C) Serveur de troisième niveau  
- [ ] D) Serveur client uniquement  

#### Question 9
Quel port TCP est utilisé par défaut pour les requêtes NTP ?

- [ ] A) 23  
- [ ] B) 123  
- [ ] C) 323  
- [ ] D) 523  

#### Question 10
Dans le fichier `/etc/ntp.conf`, que signifie l'option `iburst` après un serveur ?

- [ ] A) Envoyer plusieurs requêtes au démarrage pour une synchronisation plus rapide  
- [ ] B) Utiliser le mode rafale pour réduire la bande passante  
- [ ] C) Ignorer les erreurs de connexion  
- [ ] D) Activer le mode burst pour la sécurité  

#### Question 11
Quelle commande affiche l'état de synchronisation NTP avec `ntpd` ?

- [ ] A) `ntp -status`  
- [ ] B) `ntpq -p`  
- [ ] C) `ntpstat`  
- [ ] D) `systemctl status ntpd`  

#### Question 12
Que fait la commande `ntpdate pool.ntp.org` ?

- [ ] A) Démarre le service NTP  
- [ ] B) Configure pool.ntp.org comme serveur NTP  
- [ ] C) Effectue une synchronisation ponctuelle avec pool.ntp.org  
- [ ] D) Teste la connectivité avec pool.ntp.org  

#### Question 13
Dans `chrony`, quelle commande affiche l'état de synchronisation ?

- [ ] A) `chrony status`  
- [ ] B) `chronyc tracking`  
- [ ] C) `chronyc status`  
- [ ] D) `chrony --status`  

#### Question 14
Que signifie "Insane Time" dans le contexte NTP ?

- [ ] A) L'horloge système dérive trop rapidement  
- [ ] B) Le décalage entre l'heure système et NTP est supérieur à 17 minutes  
- [ ] C) Le serveur NTP ne répond pas  
- [ ] D) L'horloge matérielle est défaillante  

#### Question 15
Quel fichier de configuration est utilisé par `chrony` ?

- [ ] A) `/etc/chrony.conf`  
- [ ] B) `/etc/chronyd.conf`  
- [ ] C) `/etc/ntp/chrony.conf`  
- [ ] D) Le fichier varie selon la distribution  

#### Question 16
Comment forcer `chrony` à effectuer un ajustement immédiat de l'horloge ?

- [ ] A) `chronyc adjust`  
- [ ] B) `chronyc makestep`  
- [ ] C) `chronyc force-sync`  
- [ ] D) `chronyc step-time`  

#### Question 17
Quelle commande liste tous les fuseaux horaires disponibles avec `timedatectl` ?

- [ ] A) `timedatectl timezones`  
- [ ] B) `timedatectl list-timezones`  
- [ ] C) `timedatectl show-timezones`  
- [ ] D) `timedatectl --list-tz`  

#### Question 18
Que représente le temps Unix (Epoch) ?

- [ ] A) Le nombre de jours depuis le 1er janvier 1970  
- [ ] B) Le nombre de secondes depuis le 1er janvier 1970 à 00:00:00 UTC  
- [ ] C) Le nombre d'heures depuis le début du système  
- [ ] D) Le nombre de millisecondes depuis le démarrage  

#### Question 19
Quel problème est connu sous le nom de "problème Y2038" ?

- [ ] A) Dépassement de capacité du temps Unix sur systèmes 32 bits  
- [ ] B) Bug de l'an 2038 dans les systèmes Windows  
- [ ] C) Fin du support de NTP en 2038  
- [ ] D) Obsolescence des horloges matérielles  

#### Question 20
Comment désactiver la synchronisation NTP avec `timedatectl` ?

- [ ] A) `timedatectl disable-ntp`  
- [ ] B) `timedatectl set-ntp no`  
- [ ] C) `timedatectl ntp off`  
- [ ] D) `timedatectl stop-ntp`  

---

### 108.2 - Journaux systèmes (20 questions)

#### Question 21
Quel est le système de journalisation standard moderne sur les distributions utilisant systemd ?

- [ ] A) syslog  
- [ ] B) rsyslog  
- [ ] C) systemd-journald  
- [ ] D) klogd  

#### Question 22
Dans quelle arborescence les fichiers de journalisation sont-ils généralement stockés ?

- [ ] A) `/var/spool/log/`  
- [ ] B) `/var/log/`  
- [ ] C) `/etc/log/`  
- [ ] D) `/usr/log/`  

#### Question 23
Quel fichier contient les tentatives de connexion échouées ?

- [ ] A) `/var/log/auth.log`  
- [ ] B) `/var/log/faillog`  
- [ ] C) `/var/log/btmp`  
- [ ] D) `/var/log/secure`  

#### Question 24
Dans rsyslog, quelle ressource (facility) correspond aux messages du noyau ?

- [ ] A) kernel  
- [ ] B) kern  
- [ ] C) system  
- [ ] D) klog  

#### Question 25
Quelle est la priorité la plus élevée (la plus critique) dans syslog ?

- [ ] A) emerg  
- [ ] B) alert  
- [ ] C) crit  
- [ ] D) error  

#### Question 26
Dans une règle rsyslog, que signifie le point `.` entre la ressource et la priorité ?

- [ ] A) Séparateur obligatoire  
- [ ] B) Indique "et"  
- [ ] C) Indique "ou"  
- [ ] D) Représente un wildcard  

#### Question 27
Que signifie la règle rsyslog suivante : `mail.err /var/log/mail.err` ?

- [ ] A) Tous les messages mail avec priorité err uniquement  
- [ ] B) Tous les messages mail avec priorité err et supérieure  
- [ ] C) Tous les messages mail sauf err  
- [ ] D) Messages d'erreur de tous les services vers mail.err  

#### Question 28
Que fait le symbole `-` devant le chemin dans une règle rsyslog comme `*.*;auth.none -/var/log/syslog` ?

- [ ] A) Désactive la règle  
- [ ] B) Évite la synchronisation immédiate sur disque  
- [ ] C) Indique une négation  
- [ ] D) Crée un lien symbolique  

#### Question 29
Comment envoyer manuellement un message dans syslog ?

- [ ] A) `syslog "message"`  
- [ ] B) `logger "message"`  
- [ ] C) `echo "message" > /var/log/syslog`  
- [ ] D) `log "message"`  

#### Question 30
Quel port TCP est utilisé par défaut pour recevoir des logs distants avec rsyslog ?

- [ ] A) 25  
- [ ] B) 514  
- [ ] C) 5140  
- [ ] D) 6514  

#### Question 31
Dans un fichier de configuration rsyslog, comment envoyer tous les logs vers un serveur distant via TCP ?

- [ ] A) `*.* @192.168.1.100:514`  
- [ ] B) `*.* @@192.168.1.100:514`  
- [ ] C) `*.* tcp://192.168.1.100:514`  
- [ ] D) `*.* >192.168.1.100:514`  

#### Question 32
Quelle est la principale raison d'utiliser `logrotate` ?

- [ ] A) Compresser tous les fichiers de log  
- [ ] B) Éviter la saturation du disque et faciliter la consultation  
- [ ] C) Chiffrer les logs pour la sécurité  
- [ ] D) Synchroniser les logs avec un serveur distant  

#### Question 33
Dans un fichier de configuration logrotate, que fait la directive `rotate 7` ?

- [ ] A) Effectuer une rotation tous les 7 jours  
- [ ] B) Conserver 7 copies des fichiers de log  
- [ ] C) Tourner le fichier à 7h du matin  
- [ ] D) Compresser après 7 rotations  

#### Question 34
Que fait la directive `delaycompress` dans logrotate ?

- [ ] A) Compresse immédiatement après rotation  
- [ ] B) Reporte la compression au prochain cycle  
- [ ] C) Désactive la compression  
- [ ] D) Compresse uniquement les fichiers de plus de 7 jours  

#### Question 35
Quelle commande affiche les messages du kernel ring buffer ?

- [ ] A) `klog`  
- [ ] B) `kernlog`  
- [ ] C) `dmesg`  
- [ ] D) `syslog -k`  

#### Question 36
Avec `journalctl`, comment afficher uniquement les messages du boot actuel ?

- [ ] A) `journalctl --this-boot`  
- [ ] B) `journalctl -b`  
- [ ] C) `journalctl --current-boot`  
- [ ] D) `journalctl -b 0`  

#### Question 37
Comment suivre en temps réel le journal systemd ?

- [ ] A) `journalctl --follow`  
- [ ] B) `journalctl -f`  
- [ ] C) `journalctl --tail`  
- [ ] D) `journalctl --live`  

#### Question 38
Quelle commande affiche les messages du journal systemd avec priorité "error" et supérieure ?

- [ ] A) `journalctl -p err`  
- [ ] B) `journalctl --priority=error`  
- [ ] C) `journalctl -p 3`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 39
Comment activer le stockage persistant du journal systemd ?

- [ ] A) Modifier `/etc/systemd/journald.conf` avec `Storage=persistent`  
- [ ] B) Créer le répertoire `/var/log/journal/`  
- [ ] C) Les deux méthodes A et B  
- [ ] D) Exécuter `journalctl --make-persistent`  

#### Question 40
Quelle commande nettoie les journaux systemd de plus de 2 semaines ?

- [ ] A) `journalctl --vacuum-time=2weeks`  
- [ ] B) `journalctl --clean-old=2w`  
- [ ] C) `journalctl --delete-older=2weeks`  
- [ ] D) `journalctl --purge=2weeks`  

---

### 108.3 - Agent de transfert de courrier (10 questions)

#### Question 41
Que signifie l'acronyme MTA ?

- [ ] A) Mail Transfer Application  
- [ ] B) Mail Transport Agent  
- [ ] C) Mail Transfer Agent  
- [ ] D) Message Transfer Application  

#### Question 42
Quel port TCP est utilisé par défaut pour SMTP ?

- [ ] A) 23  
- [ ] B) 25  
- [ ] C) 110  
- [ ] D) 143  

#### Question 43
Quel MTA est considéré comme le plus moderne et sécurisé pour Linux ?

- [ ] A) Sendmail  
- [ ] B) Postfix  
- [ ] C) Exim  
- [ ] D) qmail  

#### Question 44
Où sont stockées les boîtes de réception locales par défaut ?

- [ ] A) `/home/user/mail/`  
- [ ] B) `/var/mail/user` ou `/var/spool/mail/user`  
- [ ] C) `/etc/mail/user/`  
- [ ] D) `/usr/mail/user/`  

#### Question 45
Quelle commande affiche la file d'attente des messages non délivrés ?

- [ ] A) `sendmail -q`  
- [ ] B) `mailq`  
- [ ] C) `mail --queue`  
- [ ] D) `postfix queue`  

#### Question 46
Quel fichier contient les alias de messagerie au niveau système ?

- [ ] A) `/etc/mail/aliases`  
- [ ] B) `/etc/aliases`  
- [ ] C) `/var/mail/aliases`  
- [ ] D) `/etc/postfix/aliases`  

#### Question 47
Après avoir modifié `/etc/aliases`, quelle commande faut-il exécuter ?

- [ ] A) `reloadalias`  
- [ ] B) `newaliases`  
- [ ] C) `sendmail -restart`  
- [ ] D) `updatedb`  

#### Question 48
Comment un utilisateur peut-il rediriger automatiquement tous ses e-mails vers une adresse externe ?

- [ ] A) Modifier `/etc/aliases`  
- [ ] B) Créer un fichier `~/.forward` contenant l'adresse  
- [ ] C) Utiliser la commande `mailforward`  
- [ ] D) Configurer `/etc/mail/redirect`  

#### Question 49
Que signifie "open relay" dans le contexte d'un MTA ?

- [ ] A) Un serveur SMTP qui accepte les connexions de n'importe qui  
- [ ] B) Un serveur qui relaie les messages sans restriction  
- [ ] C) Un serveur avec le port 25 ouvert  
- [ ] D) Un serveur de messagerie public  

#### Question 50
Dans le fichier `/etc/aliases`, que fait la syntaxe suivante : `support: :include:/etc/mail/team.txt` ?

- [ ] A) Inclut le fichier team.txt dans le message  
- [ ] B) Redirige vers les adresses listées dans team.txt  
- [ ] C) Crée un lien symbolique  
- [ ] D) Archive les messages dans team.txt  

---

## ✅ Réponses et explications

### 108.1 - Gestion de l'horloge système

#### Réponse 1 : B
**Explication** : L'horloge système est maintenue par le système d'exploitation en mémoire vive et démarre à partir de l'horloge matérielle au boot. L'horloge matérielle (RTC - Real-Time Clock) est un composant physique sur la carte mère qui continue de fonctionner même lorsque l'ordinateur est éteint grâce à une pile.

#### Réponse 2 : B
**Explication** : La commande `date -u` affiche l'heure UTC. L'option longue `--utc` n'existe pas pour la commande date. `hwclock --utc` affiche l'horloge matérielle en UTC, pas l'heure système.

#### Réponse 3 : C
**Explication** : La syntaxe correcte est `date --set="YYYY-MM-DD HH:MM:SS"`. Bien que `date` soit flexible dans l'analyse des dates, le format ISO 8601 (C) est le plus standard et fiable. Les formats A et B peuvent fonctionner selon la locale mais ne sont pas universels.

#### Réponse 4 : B
**Explication** : `hwclock --systohc` signifie "system clock to hardware clock", donc synchronise l'horloge matérielle depuis l'horloge système. L'inverse est `--hctosys` (hardware clock to system clock).

#### Réponse 5 : B
**Explication** : `/etc/localtime` est généralement un lien symbolique vers un fichier de fuseau horaire dans `/usr/share/zoneinfo/`. Il définit le fuseau horaire utilisé par le système pour calculer l'heure locale à partir de l'heure UTC.

#### Réponse 6 : A
**Explication** : La commande correcte est `timedatectl set-timezone Europe/Paris`. Cette commande crée/modifie le lien symbolique `/etc/localtime`.

#### Réponse 7 : A
**Explication** : L'offset (décalage) est la différence absolue entre l'heure système et l'heure fournie par le serveur NTP. Si l'horloge système indique 12:00:02 et l'heure NTP 11:59:58, l'offset est de 4 secondes.

#### Réponse 8 : B
**Explication** : Dans la hiérarchie NTP :
- Stratum 0 : Horloges de référence (atomiques)
- Stratum 1 : Serveurs directement connectés aux horloges de référence
- Stratum 2 : Serveurs synchronisés avec stratum 1
- Et ainsi de suite...

#### Réponse 9 : B
**Explication** : NTP utilise le port **UDP 123** (pas TCP). C'est le port standard pour les requêtes et réponses NTP.

#### Réponse 10 : A
**Explication** : L'option `iburst` envoie une rafale de plusieurs requêtes au démarrage pour obtenir une synchronisation plus rapide, puis passe au mode normal. C'est différent de `burst` qui envoie plusieurs requêtes à chaque intervalle.

#### Réponse 11 : B
**Explication** : `ntpq -p` (print peers) affiche l'état des serveurs NTP configurés avec leurs statistiques (offset, jitter, delay, etc.). L'option `-n` affiche les adresses IP au lieu des noms d'hôtes.

#### Réponse 12 : C
**Explication** : `ntpdate` effectue une synchronisation ponctuelle (one-shot) avec le serveur spécifié. Cette commande est obsolète mais encore utilisée pour des ajustements initiaux quand le démon NTP n'est pas actif.

#### Réponse 13 : B
**Explication** : `chronyc tracking` affiche l'état détaillé de la synchronisation avec chrony, incluant le stratum, l'offset, le drift, etc. `chronyc` est l'outil en ligne de commande pour interroger `chronyd`.

#### Réponse 14 : B
**Explication** : Si le décalage entre l'heure système et l'heure NTP est supérieur à 17 minutes, l'heure système est considérée comme "insane" (insensée) et le démon NTP ne modifiera pas automatiquement l'heure. Une intervention manuelle est nécessaire (ntpdate ou chronyc makestep).

#### Réponse 15 : D
**Explication** : Le chemin varie selon la distribution :
- Debian/Ubuntu : `/etc/chrony/chrony.conf`
- Red Hat/CentOS/Fedora : `/etc/chrony.conf`
- Arch : `/etc/chrony.conf`

#### Réponse 16 : B
**Explication** : `chronyc makestep` force un ajustement immédiat de l'horloge système, même si le décalage est important. Cela équivaut à un "step" au lieu du "slew" habituel.

#### Réponse 17 : B
**Explication** : `timedatectl list-timezones` liste tous les fuseaux horaires disponibles. La sortie peut être filtrée avec `grep` : `timedatectl list-timezones | grep Paris`.

#### Réponse 18 : B
**Explication** : Le temps Unix (Epoch) est le nombre de secondes écoulées depuis le 1er janvier 1970 à 00:00:00 UTC. Il est utilisé en interne par les systèmes Unix/Linux pour stocker les horodatages.

#### Réponse 19 : A
**Explication** : Le problème Y2038 survient le 19 janvier 2038 à 03:14:07 UTC lorsque le temps Unix stocké sur 32 bits signés atteindra sa valeur maximale (2^31 - 1 = 2 147 483 647) et débordera. Les systèmes 64 bits ne sont pas affectés.

#### Réponse 20 : B
**Explication** : `timedatectl set-ntp no` désactive la synchronisation NTP. Pour réactiver : `timedatectl set-ntp yes`.

### 108.2 - Journaux systèmes

#### Réponse 21 : C
**Explication** : `systemd-journald` est le système de journalisation natif de systemd, devenu standard sur la plupart des distributions modernes. Il coexiste souvent avec rsyslog qui peut lire ses journaux.

#### Réponse 22 : B
**Explication** : `/var/log/` est l'emplacement standard pour tous les fichiers de journalisation système sous Linux. Les données variables comme les logs sont dans `/var/` (variable data).

#### Réponse 23 : C
**Explication** : `/var/log/btmp` enregistre les tentatives de connexion échouées (bad logins). Il se lit avec `last -f /var/log/btmp` ou `utmpdump /var/log/btmp`. `/var/log/auth.log` contient aussi des échecs mais dans un format différent.

#### Réponse 24 : B
**Explication** : La ressource `kern` correspond aux messages du noyau Linux. Le démon `klogd` (ou le module `imklog` dans rsyslog) récupère ces messages depuis `/dev/kmsg`.

#### Réponse 25 : A
**Explication** : La priorité `emerg` (ou `panic`, numéro 0) est la plus critique. Hiérarchie :
0=emerg, 1=alert, 2=crit, 3=err, 4=warn, 5=notice, 6=info, 7=debug

#### Réponse 26 : A
**Explication** : Le point `.` est simplement le séparateur obligatoire entre la ressource (facility) et la priorité dans une règle rsyslog : `ressource.priorité action`.

#### Réponse 27 : B
**Explication** : Les priorités sont hiérarchiquement inclusives. `mail.err` signifie tous les messages de la ressource `mail` avec priorité `err` **et supérieure** (err, crit, alert, emerg). Pour une priorité exacte, utiliser `=` : `mail.=err`.

#### Réponse 28 : B
**Explication** : Le tiret `-` devant le chemin désactive la synchronisation immédiate sur disque (fsync), améliorant les performances. Les messages sont bufferisés en mémoire avant écriture. Risque : perte en cas de crash.

#### Réponse 29 : B
**Explication** : `logger` est la commande pour envoyer manuellement des messages à syslog. Exemples :
- `logger "message simple"`
- `logger -p user.err "message d'erreur"`
- `logger -t MON_APP "message avec tag"`

#### Réponse 30 : B
**Explication** : Le port **514** est le port standard pour syslog, utilisable en TCP ou UDP. Pour rsyslog :
- UDP : `$ModLoad imudp` + `$UDPServerRun 514`
- TCP : `$ModLoad imtcp` + `$InputTCPServerRun 514`

#### Réponse 31 : B
**Explication** : Dans rsyslog :
- `@` = UDP
- `@@` = TCP
Donc `*.* @@192.168.1.100:514` envoie tous les logs via TCP au serveur 192.168.1.100 sur le port 514.

#### Réponse 32 : B
**Explication** : `logrotate` effectue la rotation des logs pour :
1. Éviter la saturation du disque (les logs peuvent devenir très volumineux)
2. Faciliter la consultation (fichiers plus petits)
3. Archiver et éventuellement compresser les anciens logs

#### Réponse 33 : B
**Explication** : `rotate 7` signifie conserver 7 copies rotées. Exemple : si rotation hebdomadaire, on garde les logs des 7 dernières semaines. Au 8ème cycle, le plus ancien est supprimé.

#### Réponse 34 : B
**Explication** : `delaycompress` reporte la compression au prochain cycle de rotation. Utile si un service continue d'écrire dans l'ancien fichier après rotation. Le fichier `.1` reste non compressé, `.2` et suivants sont compressés.

#### Réponse 35 : C
**Explication** : `dmesg` affiche le kernel ring buffer, une mémoire tampon circulaire contenant les messages du noyau depuis le démarrage. Équivalent : `journalctl -k` ou `journalctl --dmesg`.

#### Réponse 36 : B et D
**Explication** : `journalctl -b` affiche les messages du boot actuel (0). `-b 0` est équivalent. `-b -1` = boot précédent, `-b -2` = avant-dernier boot, etc. `--list-boots` liste tous les boots disponibles.

#### Réponse 37 : B
**Explication** : `journalctl -f` (follow) suit le journal en temps réel, comme `tail -f`. Affiche les nouvelles entrées au fur et à mesure. `--follow` est l'option longue équivalente.

#### Réponse 38 : D
**Explication** : Trois syntaxes équivalentes :
- `journalctl -p err` (mot-clé)
- `journalctl --priority=error` (option longue)
- `journalctl -p 3` (numérique)
Toutes affichent err et supérieur (err, crit, alert, emerg).

#### Réponse 39 : C
**Explication** : Deux méthodes pour activer le stockage persistant :
1. Créer `/var/log/journal/` : systemd détecte et active automatiquement
2. Modifier `/etc/systemd/journald.conf` : `Storage=persistent`
Dans les deux cas, redémarrer `systemd-journald`.

#### Réponse 40 : A
**Explication** : `journalctl --vacuum-time=2weeks` supprime les journaux archivés de plus de 2 semaines. Autres options :
- `--vacuum-size=500M` : limiter à 500M
- `--vacuum-files=10` : max 10 fichiers
- `--rotate` : rotation manuelle

### 108.3 - Agent de transfert de courrier

#### Réponse 41 : C
**Explication** : MTA = **Mail Transfer Agent** (Agent de Transfert de Courrier). C'est le serveur qui transfère les e-mails entre expéditeur et destinataire en utilisant SMTP. Exemples : Sendmail, Postfix, Exim.

#### Réponse 42 : B
**Explication** : Le port **25** est le port standard SMTP pour le transfert de courrier entre serveurs. Autres ports :
- 587 : Soumission SMTP (avec authentification)
- 110 : POP3
- 143 : IMAP
- 465 : SMTPS (obsolète, remplacé par STARTTLS sur 587)

#### Réponse 43 : B
**Explication** : **Postfix** est considéré comme le MTA le plus moderne, sécurisé et performant. Avantages :
- Architecture modulaire et sécurisée
- Configuration plus simple que Sendmail
- Performances élevées
- Bonne documentation

#### Réponse 44 : B
**Explication** : Les boîtes de réception locales sont dans `/var/mail/username` ou `/var/spool/mail/username` (souvent un lien symbolique l'un vers l'autre). Format généralement **mbox** (un fichier par utilisateur) ou **Maildir** (un fichier par message).

#### Réponse 45 : B
**Explication** : `mailq` affiche la file d'attente des messages en attente de livraison. Équivalent à `sendmail -bp`. Pour Postfix : `postqueue -p` fait la même chose.

#### Réponse 46 : B
**Explication** : `/etc/aliases` contient les alias de messagerie système. Format : `alias: destination`. Après modification, exécuter `newaliases` pour régénérer la base de données `/etc/aliases.db`.

#### Réponse 47 : B
**Explication** : `newaliases` régénère la base de données des alias à partir de `/etc/aliases`. Équivalent à `sendmail -bi` ou `sendmail -I`. Nécessaire pour que les modifications soient prises en compte.

#### Réponse 48 : B
**Explication** : Un utilisateur crée `~/.forward` dans son répertoire personnel contenant l'adresse de redirection. Exemples :
```
emma@example.com
```
Pour garder une copie locale ET rediriger :
```
\username
emma@example.com
```

#### Réponse 49 : B
**Explication** : Un **open relay** est un serveur SMTP qui relaie les e-mails sans vérifier l'expéditeur ou le destinataire. Problème : peut être exploité pour envoyer du spam. Solution : configurer `mynetworks` et `relay_restrictions` pour limiter les relais autorisés.

#### Réponse 50 : B
**Explication** : `:include:/chemin/fichier` dans `/etc/aliases` inclut une liste d'adresses depuis un fichier externe. Chaque ligne du fichier = une adresse de destination. Utile pour listes de diffusion.

Exemple `/etc/mail/team.txt` :
```
alice@example.com
bob@example.com
carol@example.com
```

---

## 🎓 Barème et évaluation

### Score total : /50

- **45-50 points** : Excellente maîtrise ! 🏆
- **40-44 points** : Très bonne compréhension 👏
- **35-39 points** : Bonne base, à consolider 👍
- **30-34 points** : Révision nécessaire 📚
- **< 30 points** : Revoir le sujet en profondeur 🔄

### Points par objectif

- **108.1 (Gestion de l'horloge)** : /20 → Pondération réelle : 30% du sujet
- **108.2 (Journaux systèmes)** : /20 → Pondération réelle : 40% du sujet
- **108.3 (MTA)** : /10 → Pondération réelle : 30% du sujet

---

## 💡 Exercices pratiques

### Exercice 1 : Configuration NTP complète

**Objectif** : Mettre en place une synchronisation NTP fiable.

**Scénario** : Vous administrez un serveur dont l'horloge dérive de plusieurs minutes. Vous devez configurer chrony pour synchroniser avec pool.ntp.org.

**Étapes** :

1. Installer chrony :
```bash
sudo apt install chrony
```

2. Éditer `/etc/chrony/chrony.conf` :
```bash
sudo nano /etc/chrony/chrony.conf

# Ajouter/vérifier :
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

# Autoriser ajustements importants
makestep 1.0 3
```

3. Redémarrer chrony :
```bash
sudo systemctl restart chronyd
```

4. Vérifier la synchronisation :
```bash
chronyc tracking
chronyc sources -v
```

5. Forcer un ajustement si nécessaire :
```bash
sudo chronyc makestep
```

6. Synchroniser l'horloge matérielle :
```bash
sudo hwclock --systohc
```

**Questions** :
1. Quelle est la différence entre `server` et `pool` dans chrony.conf ?
2. Pourquoi utiliser `iburst` ?
3. Que fait `makestep 1.0 3` ?

**Réponses** :
1. `server` = un serveur spécifique ; `pool` = groupe de serveurs (rotation)
2. `iburst` envoie plusieurs requêtes au démarrage pour sync plus rapide
3. Permet ajustement immédiat si offset < 1s lors des 3 premières mises à jour

---

### Exercice 2 : Configuration serveur de logs centralisé

**Objectif** : Centraliser les logs de plusieurs serveurs.

**Scénario** : Vous gérez 3 serveurs web. Vous voulez centraliser tous leurs logs sur un serveur dédié.

**Serveur de logs (192.168.1.10)** :

1. Configurer rsyslog pour recevoir TCP :
```bash
sudo nano /etc/rsyslog.d/remote.conf

# Activer module TCP
module(load="imtcp")
input(type="imtcp" port="514")

# Créer template pour organiser par hôte
$template RemoteLogs,"/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log"

# Appliquer template aux logs distants
*.* ?RemoteLogs
& stop
```

2. Redémarrer rsyslog :
```bash
sudo systemctl restart rsyslog
```

3. Vérifier le port en écoute :
```bash
sudo netstat -tlnp | grep 514
```

4. Ouvrir le pare-feu :
```bash
sudo firewall-cmd --permanent --add-port=514/tcp
sudo firewall-cmd --reload
```

**Clients web (192.168.1.11, .12, .13)** :

1. Configurer envoi vers serveur central :
```bash
sudo nano /etc/rsyslog.conf

# Ajouter à la fin
*.* @@192.168.1.10:514
```

2. Redémarrer rsyslog :
```bash
sudo systemctl restart rsyslog
```

3. Tester :
```bash
logger -t WEB-TEST "Message de test depuis $(hostname)"
```

**Vérification sur serveur central** :
```bash
sudo ls -R /var/log/remote/
sudo tail /var/log/remote/web-01/WEB-TEST.log
```

**Questions** :
1. Quelle est la différence entre `@` et `@@` ?
2. Pourquoi utiliser `& stop` dans le template ?
3. Comment filtrer uniquement les logs d'un client spécifique ?

**Réponses** :
1. `@` = UDP (rapide mais non fiable), `@@` = TCP (fiable mais plus lent)
2. `& stop` évite que les logs distants soient aussi écrits dans les fichiers locaux
3. Utiliser `if $fromhost-ip=='192.168.1.11' then ?RemoteLogs`

---

### Exercice 3 : Analyse avancée avec journalctl

**Objectif** : Maîtriser le filtrage et l'analyse des logs systemd.

**Scénarios** :

**1. Trouver toutes les erreurs SSH des dernières 24h :**
```bash
sudo journalctl -u ssh.service -p err --since "24 hours ago"
```

**2. Voir les connexions utilisateur "carol" :**
```bash
sudo journalctl _UID=$(id -u carol) --since today
```

**3. Analyser le démarrage précédent :**
```bash
sudo journalctl -b -1 -p warning
```

**4. Rechercher des patterns spécifiques :**
```bash
# Chercher "failed" dans les logs
sudo journalctl | grep -i "failed"

# OU utiliser filtres journalctl
sudo journalctl SYSLOG_IDENTIFIER=sshd | grep "Failed password"
```

**5. Exporter pour analyse externe :**
```bash
# Format JSON
sudo journalctl -u nginx --since today -o json-pretty > nginx-logs.json

# Format court pour scripts
sudo journalctl -u apache2 --since "1 hour ago" -o cat > apache-errors.txt
```

**6. Surveiller en temps réel avec filtres :**
```bash
# Suivre uniquement les erreurs
sudo journalctl -f -p err

# Suivre une unité spécifique
sudo journalctl -f -u mysql.service

# Combiner plusieurs filtres
sudo journalctl -f -p warning --since "now" _SYSTEMD_UNIT=nginx.service
```

**Questions pratiques** :

1. **Combien de boots sont disponibles ?**
```bash
sudo journalctl --list-boots | wc -l
```

2. **Quel est l'espace disque utilisé par les journaux ?**
```bash
sudo journalctl --disk-usage
```

3. **Nettoyer pour ne garder que 500M :**
```bash
sudo journalctl --vacuum-size=500M
```

4. **Voir tous les messages du processus avec PID 1 (systemd) :**
```bash
sudo journalctl _PID=1 --since today
```

5. **Afficher les messages kernel uniquement :**
```bash
sudo journalctl -k
# OU
sudo journalctl _TRANSPORT=kernel
```

---

### Exercice 4 : Configuration Postfix et alias

**Objectif** : Mettre en place un système de messagerie local avec redirections.

**Installation et configuration de base** :

1. Installer Postfix :
```bash
sudo apt install postfix
# Choisir "Internet Site" ou "Local only" selon besoin
```

2. Configuration minimale `/etc/postfix/main.cf` :
```bash
sudo nano /etc/postfix/main.cf

# Configuration pour usage local uniquement
myhostname = server.example.local
mydomain = example.local
myorigin = $mydomain
inet_interfaces = loopback-only
mydestination = $myhostname, localhost.$mydomain, localhost
mynetworks = 127.0.0.0/8
```

3. Redémarrer Postfix :
```bash
sudo systemctl restart postfix
sudo postfix check  # Vérifier config
```

**Configuration des alias** :

1. Créer fichier de liste d'équipe :
```bash
sudo nano /etc/mail/equipe-dev.txt

alice@example.com
bob@example.com
carol@example.local
```

2. Éditer `/etc/aliases` :
```bash
sudo nano /etc/aliases

# Redirections administrateur
root: admin@example.com
postmaster: root

# Équipes
dev: :include:/etc/mail/equipe-dev.txt
support: alice, bob

# Archive
logs: /var/mail/archive-logs.mbox

# Script de traitement
alerts: |/usr/local/bin/process-alert.sh
```

3. Appliquer les alias :
```bash
sudo newaliases
# Vérifier
ls -l /etc/aliases.db
```

**Tests** :

1. Envoyer à un utilisateur :
```bash
echo "Test message" | mail -s "Test" carol
```

2. Envoyer à une liste :
```bash
echo "Message à l'équipe dev" | mail -s "Info Dev" dev
```

3. Vérifier la réception :
```bash
mail
# OU
sudo cat /var/mail/carol
```

4. Voir la file d'attente :
```bash
mailq
# Si messages bloqués
sudo postqueue -f  # Forcer envoi
```

**Redirection utilisateur** :

En tant qu'utilisateur carol :
```bash
nano ~/.forward

# Rediriger tout vers adresse externe
carol.externe@gmail.com

# OU garder copie locale + rediriger
\carol
carol.externe@gmail.com
```

**Monitoring** :
```bash
# Logs en temps réel
sudo tail -f /var/log/mail.log

# Analyser les erreurs
sudo grep "error" /var/log/mail.log
sudo grep "deferred" /var/log/mail.log
```

**Questions** :
1. Comment envoyer un message avec pièce jointe ?
2. Que se passe-t-il si l'adresse externe est indisponible ?
3. Comment déboguer un problème de livraison ?

**Réponses** :
1. `mail -s "Sujet" -a /chemin/fichier.pdf destinataire@example.com < message.txt`
2. Le message reste dans la queue (`mailq`) et Postfix réessaie périodiquement
3. Vérifier : 1) service actif, 2) DNS/réseau, 3) logs `/var/log/mail.log`, 4) queue `mailq`

---

## 📚 Ressources complémentaires

### Documentation officielle

**Gestion du temps** :
- `man timedatectl`
- `man chrony.conf`
- `man ntpd`
- [chrony.tuxfamily.org](https://chrony.tuxfamily.org/)
- [www.ntp.org](https://www.ntp.org/)

**Journalisation** :
- `man rsyslog.conf`
- `man journalctl`
- `man journald.conf`
- `man logrotate.conf`
- [rsyslog.com/doc](https://www.rsyslog.com/doc/)
- [systemd.io](https://systemd.io/)

**Messagerie** :
- `man sendmail`
- `man aliases`
- `man postfix`
- [www.postfix.org](http://www.postfix.org/)

### Commandes de référence rapide

```bash
# === TEMPS ===
timedatectl                    # État complet
date -u                        # Heure UTC
hwclock --systohc              # Sync système → matériel
chronyc tracking               # État NTP (chrony)
ntpq -p                        # État NTP (ntpd)

# === LOGS ===
logger "message"               # Entrée manuelle syslog
sudo tail -f /var/log/syslog   # Suivi temps réel
sudo journalctl -f             # Suivi journal systemd
sudo journalctl -xe            # Dernières erreurs
dmesg                          # Messages noyau

# === MAIL ===
mail                           # Lire courrier
mailq                          # File d'attente
sudo newaliases                # MAJ base alias
echo "msg" | mail -s "test" user   # Envoi rapide
```

---

## 🎯 Conseils pour l'examen

### Points clés à retenir

**108.1 - Gestion du temps** :
- ✅ Connaître la différence horloge système/matérielle
- ✅ Maîtriser timedatectl sur systemd
- ✅ Savoir configurer NTP (ntpd ou chrony)
- ✅ Comprendre les concepts : offset, stratum, drift

**108.2 - Journalisation** :
- ✅ Connaître les ressources et priorités syslog
- ✅ Savoir écrire une règle rsyslog
- ✅ Maîtriser journalctl et ses filtres
- ✅ Comprendre logrotate et ses directives

**108.3 - MTA** :
- ✅ Connaître les protocoles : SMTP, POP3, IMAP
- ✅ Savoir utiliser sendmail et mail
- ✅ Maîtriser les alias (/etc/aliases et ~/.forward)
- ✅ Comprendre les risques (open relay)

### Pièges à éviter

❌ Confondre `hwclock --systohc` et `--hctosys`  
❌ Oublier `newaliases` après modification de `/etc/aliases`  
❌ Confondre `@` (UDP) et `@@` (TCP) dans rsyslog  
❌ Ignorer la hiérarchie des priorités syslog  
❌ Ne pas activer le stockage persistant pour journald  

### Temps de réponse recommandé

- Questions de connaissance : 30-45 secondes
- Questions de commande : 45-60 secondes
- Questions de configuration : 60-90 secondes

**Durée totale recommandée** : 45-60 minutes

---

**Bon courage pour votre préparation ! 🎓**

*N'oubliez pas de pratiquer régulièrement avec les exercices pour consolider vos connaissances.*
