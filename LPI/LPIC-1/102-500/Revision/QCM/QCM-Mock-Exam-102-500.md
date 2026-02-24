# 🎓 Mock Exam LPIC-1 102-500 - Examen Blanc Complet

> **Format réel** : 60 questions | 90 minutes | 500/800 minimum (62.5%)  
> **Objectif visé** : 700/800 (87.5%) = 52+ bonnes réponses

---

## 📋 Instructions Examen

### Conditions réelles
- ⏱️ **Temps** : 90 minutes chrono (1h30)
- 📝 **Questions** : 60 au total
- ✅ **Réussite** : 500/800 minimum (38/60 questions)
- 🎯 **Objectif** : 700/800 (52/60 questions)
- 📵 **Sans aide** : Pas de notes, internet, documentation

### Consignes
1. Préparez une feuille pour noter vos réponses (1-60)
2. Démarrez chronomètre 90 minutes
3. Répondez dans l'ordre ou marquez les questions difficiles
4. Une seule réponse correcte par question
5. Pas de pénalité pour mauvaise réponse
6. À la fin : comparez avec grille de correction

### Répartition par sujet
| Sujet | Poids | Questions | % Examen |
|-------|-------|-----------|----------|
| 105 - Shells et Scripts | 11 pts | 11 Q | 18% |
| 106 - Interfaces Utilisateur | 4 pts | 4 Q | 7% |
| 107 - Tâches Administratives | 12 pts | 12 Q | 20% |
| 108 - Services Système | 10 pts | 10 Q | 17% |
| 109 - Notions Réseaux | 8 pts | 8 Q | 13% |
| 110 - Sécurité | 12 pts | 15 Q | 25% |

---

## 📝 EXAMEN - 60 Questions

### Question 1 (Sujet 105)
Quelle commande affiche **toutes les variables d'environnement** ?

- [ ] A) `set`  
- [ ] B) `env`  
- [ ] C) `printenv`  
- [ ] D) Les deux B et C

---

### Question 2 (Sujet 110)
Quelle est la représentation **numérique du bit SUID** ?

- [ ] A) 1000  
- [ ] B) 2000  
- [ ] C) 4000  
- [ ] D) 8000

---

### Question 3 (Sujet 107)
Comment créer un utilisateur avec un **répertoire home** ?

- [ ] A) `useradd user`  
- [ ] B) `useradd -m user`  
- [ ] C) `useradd -h user`  
- [ ] D) `adduser user`

---

### Question 4 (Sujet 109)
Quel est le **réseau privé de classe A** selon RFC 1918 ?

- [ ] A) `192.168.0.0/16`  
- [ ] B) `172.16.0.0/12`  
- [ ] C) `10.0.0.0/8`  
- [ ] D) `127.0.0.0/8`

---

### Question 5 (Sujet 108)
Comment activer la **synchronisation NTP** avec systemd ?

- [ ] A) `ntpd enable`  
- [ ] B) `timedatectl set-ntp true`  
- [ ] C) `systemctl enable ntp`  
- [ ] D) `hwclock --ntp`

---

### Question 6 (Sujet 110)
Quelle commande affiche les **processus utilisant le port 80** ?

- [ ] A) `lsof -i :80`  
- [ ] B) `fuser -vn tcp 80`  
- [ ] C) `ss -tulpn | grep :80`  
- [ ] D) Toutes les réponses

---

### Question 7 (Sujet 105)
Dans un script, que contient la variable **$?** ?

- [ ] A) PID du script  
- [ ] B) Nom du script  
- [ ] C) Code retour de la dernière commande  
- [ ] D) Nombre d'arguments

---

### Question 8 (Sujet 107)
Quel est le **format d'une ligne crontab** ?

- [ ] A) `heure min jour mois jour_semaine commande`  
- [ ] B) `min heure jour mois jour_semaine commande`  
- [ ] C) `jour mois année heure min commande`  
- [ ] D) `commande min heure jour mois`

---

### Question 9 (Sujet 109)
Quelle commande affiche les **routes** avec iproute2 ?

- [ ] A) `route -n`  
- [ ] B) `ip route show`  
- [ ] C) `ip r`  
- [ ] D) Les deux B et C

---

### Question 10 (Sujet 106)
Quelle variable contient l'**affichage X11** actuel ?

- [ ] A) `$XDISPLAY`  
- [ ] B) `$DISPLAY`  
- [ ] C) `$X11`  
- [ ] D) `$SCREEN`

---

### Question 11 (Sujet 110)
Comment **verrouiller le compte** d'un utilisateur avec passwd ?

- [ ] A) `passwd -l user`  
- [ ] B) `passwd -L user`  
- [ ] C) `passwd --lock user`  
- [ ] D) Les réponses A et C

---

### Question 12 (Sujet 108)
Quel fichier contient les **serveurs DNS** ?

- [ ] A) `/etc/hosts`  
- [ ] B) `/etc/resolv.conf`  
- [ ] C) `/etc/dns.conf`  
- [ ] D) `/etc/network/dns`

---

### Question 13 (Sujet 105)
Quelle commande SQL **supprime des données** d'une table ?

- [ ] A) `REMOVE FROM table WHERE condition`  
- [ ] B) `DELETE FROM table WHERE condition`  
- [ ] C) `DROP FROM table WHERE condition`  
- [ ] D) `TRUNCATE table WHERE condition`

---

### Question 14 (Sujet 107)
Comment ajouter un utilisateur au groupe **sudo** (en préservant les autres groupes) ?

- [ ] A) `usermod -G sudo user`  
- [ ] B) `usermod -aG sudo user`  
- [ ] C) `usermod -a sudo user`  
- [ ] D) `groupadd user sudo`

---

### Question 15 (Sujet 109)
Quel **port utilise HTTPS** ?

- [ ] A) 80  
- [ ] B) 443  
- [ ] C) 8080  
- [ ] D) 8443

---

### Question 16 (Sujet 110)
Quelle commande génère une **paire de clés SSH Ed25519** ?

- [ ] A) `ssh-keygen`  
- [ ] B) `ssh-keygen -t ed25519`  
- [ ] C) `ssh-keygen -t rsa -b 25519`  
- [ ] D) `ssh-add -t ed25519`

---

### Question 17 (Sujet 108)
Comment afficher les **logs du service SSH** avec journalctl ?

- [ ] A) `journalctl ssh`  
- [ ] B) `journalctl -u ssh`  
- [ ] C) `journalctl -u sshd`  
- [ ] D) Les deux B et C

---

### Question 18 (Sujet 105)
Quel fichier est exécuté lors d'un **login shell bash** (premier appelé env. utilisateur) ?

- [ ] A) `~/.bashrc`  
- [ ] B) `~/.bash_profile`  
- [ ] C) `/etc/profile`  
- [ ] D) `~/.bash_login`

---

### Question 19 (Sujet 110)
Comment copier votre **clé publique SSH** sur un serveur distant ?

- [ ] A) `ssh-copy-id user@host`  
- [ ] B) `scp ~/.ssh/id_rsa.pub user@host:~/.ssh/authorized_keys`  
- [ ] C) `cat ~/.ssh/id_rsa.pub | ssh user@host 'cat >> .ssh/authorized_keys'`  
- [ ] D) Toutes les réponses

---

### Question 20 (Sujet 107)
Quelle entrée cron exécute un script **tous les lundis à 8h30** ?

- [ ] A) `30 8 * * 1 /script.sh`  
- [ ] B) `8 30 * * 1 /script.sh`  
- [ ] C) `30 8 1 * * /script.sh`  
- [ ] D) `* * * * 1 /script.sh`

---

### Question 21 (Sujet 109)
Comment ajouter une **route par défaut** avec ip ?

- [ ] A) `ip route default 192.168.1.1`  
- [ ] B) `ip route add default via 192.168.1.1`  
- [ ] C) `ip route set default 192.168.1.1`  
- [ ] D) `route add default gw 192.168.1.1`

---

### Question 22 (Sujet 106)
Quel est le **display manager** utilisé par GNOME ?

- [ ] A) `lightdm`  
- [ ] B) `gdm3`  
- [ ] C) `sddm`  
- [ ] D) `xdm`

---

### Question 23 (Sujet 110)
Quelle commande affiche les **informations d'expiration** du mot de passe d'un utilisateur ?

- [ ] A) `passwd -l user`  
- [ ] B) `chage -l user`  
- [ ] C) `usermod -e user`  
- [ ] D) `getent shadow user`

---

### Question 24 (Sujet 108)
Comment synchroniser l'**horloge système vers l'horloge matérielle** ?

- [ ] A) `hwclock --systohc`  
- [ ] B) `hwclock --hctosys`  
- [ ] C) `timedatectl set-time`  
- [ ] D) `date --sync`

---

### Question 25 (Sujet 105)
Comment tester si un **fichier existe** dans un script bash ?

- [ ] A) `[ -e fichier ]`  
- [ ] B) `[ -f fichier ]`  
- [ ] C) `[ -d fichier ]`  
- [ ] D) Les deux A et B

---

### Question 26 (Sujet 107)
Combien de champs contient le fichier **/etc/passwd** ?

- [ ] A) 5  
- [ ] B) 7  
- [ ] C) 9  
- [ ] D) 10

---

### Question 27 (Sujet 109)
Quelle commande affiche les **connexions réseau actives** (moderne, non obsolète) ?

- [ ] A) `netstat -tunap`  
- [ ] B) `ss -tunap`  
- [ ] C) `lsof -i`  
- [ ] D) Les deux B et C

---

### Question 28 (Sujet 110)
Quel algorithme SSH est **recommandé** pour la meilleure sécurité ?

- [ ] A) RSA 2048  
- [ ] B) DSA  
- [ ] C) ECDSA 521  
- [ ] D) Ed25519

---

### Question 29 (Sujet 108)
Dans rsyslog, quelle **priority** est la plus élevée (critique) ?

- [ ] A) `debug`  
- [ ] B) `info`  
- [ ] C) `err`  
- [ ] D) `emerg`

---

### Question 30 (Sujet 105)
Comment créer une **boucle for** de 1 à 10 en bash ?

- [ ] A) `for i in (1..10); do echo $i; done`  
- [ ] B) `for i in {1..10}; do echo $i; done`  
- [ ] C) `for i from 1 to 10; do echo $i; done`  

---

### Question 31 (Sujet 107)
Que signifie **@reboot** dans une crontab ?

- [ ] A) Exécuter toutes les heures  
- [ ] B) Exécuter au démarrage du système  
- [ ] C) Exécuter tous les jours  
- [ ] D) Redémarrer le système

---

### Question 32 (Sujet 110)
Comment forcer un utilisateur à **changer son mot de passe** au prochain login ?

- [ ] A) `passwd -e user`  
- [ ] B) `chage -d 0 user`  
- [ ] C) `usermod -e 0 user`  
- [ ] D) Les deux A et B

---

### Question 33 (Sujet 109)
Combien d'**adresses IP utilisables** dans un réseau /26 ?

- [ ] A) 64  
- [ ] B) 62  
- [ ] C) 128  
- [ ] D) 126

---

### Question 34 (Sujet 108)
Quelle commande affiche les **logs du boot actuel** avec journalctl ?

- [ ] A) `journalctl -b`  
- [ ] B) `journalctl --boot`  
- [ ] C) `journalctl -k`  
- [ ] D) Les deux A et B

---

### Question 35 (Sujet 106)
Quel composant remplace progressivement **X11** ?

- [ ] A) X12  
- [ ] B) Wayland  
- [ ] C) Mir  
- [ ] D) XWayland

---

### Question 36 (Sujet 110)
Quel fichier doit TOUJOURS être édité avec **visudo** ?

- [ ] A) `/etc/passwd`  
- [ ] B) `/etc/shadow`  
- [ ] C) `/etc/sudoers`  
- [ ] D) `/etc/sudo.conf`

---

### Question 37 (Sujet 105)
Dans un test bash, que signifie **-z "$var"** ?

- [ ] A) Variable non vide  
- [ ] B) Variable vide  
- [ ] C) Variable égale à zéro  
- [ ] D) Variable numérique

---

### Question 38 (Sujet 107)
Quelle commande planifie une **tâche unique** dans 2 heures ?

- [ ] A) `crontab -e`  
- [ ] B) `at now + 2 hours`  
- [ ] C) `batch +2h`  
- [ ] D) `schedule 2h`

---

### Question 39 (Sujet 109)
Comment définir une **adresse IP statique** avec NetworkManager en CLI ?

- [ ] A) `nmcli con add type ethernet ifname eth0 ip4 192.168.1.100/24`  
- [ ] B) `ip addr add 192.168.1.100/24 dev eth0`  
- [ ] C) `ifconfig eth0 192.168.1.100 netmask 255.255.255.0`  
- [ ] D) Les deux A et B

---

### Question 40 (Sujet 110)
Comment chiffrer un fichier avec **GPG** pour l'utilisateur alice ?

- [ ] A) `gpg -e file alice`  
- [ ] B) `gpg -e -r alice file`  
- [ ] C) `gpg --encrypt --recipient alice file`  
- [ ] D) Les deux B et C

---

### Question 41 (Sujet 108)
Où sont stockés les **scripts de rotation quotidiens** des logs ?

- [ ] A) `/etc/cron.daily/`  
- [ ] B) `/etc/logrotate.d/`  
- [ ] C) `/var/log/rotate/`  
- [ ] D) `/etc/log.d/`

---

### Question 42 (Sujet 105)
Quelle est la différence entre `$@` et `$*` dans un script ?

- [ ] A) Aucune différence  
- [ ] B) `$@` préserve les arguments séparés entre guillemets  
- [ ] C) `$*` préserve les arguments séparés entre guillemets  
- [ ] D) `$@` contient le nombre d'arguments

---

### Question 43 (Sujet 107)
Comment définir la **timezone Paris** avec systemd ?

- [ ] A) `timedatectl set-timezone Europe/Paris`  
- [ ] B) `ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime`  
- [ ] C) `export TZ=Europe/Paris`  
- [ ] D) Les deux A et B

---

### Question 44 (Sujet 110)
Quelle commande trouve tous les fichiers avec le **bit SGID** ?

- [ ] A) `find / -perm 2000`  
- [ ] B) `find / -perm -2000`  
- [ ] C) `find / -perm /2000`  
- [ ] D) Les réponses B et C

---

### Question 45 (Sujet 109)
Quel port utilise le service **DNS** ?

- [ ] A) 25  
- [ ] B) 53  
- [ ] C) 80  
- [ ] D) 110

---

### Question 46 (Sujet 106)
Quel outil d'**accessibilité** est un lecteur d'écran pour GNOME ?

- [ ] A) `onboard`  
- [ ] B) `orca`  
- [ ] C) `kmag`  
- [ ] D) `florence`

---

### Question 47 (Sujet 108)
Comment afficher les **10 dernières lignes** du syslog en temps réel ?

- [ ] A) `tail /var/log/syslog`  
- [ ] B) `tail -f /var/log/syslog`  
- [ ] C) `journalctl -f -n 10`  
- [ ] D) Les deux B et C

---

### Question 48 (Sujet 110)
Quelle option SSH crée un **tunnel de port local** ?

- [ ] A) `-L`  
- [ ] B) `-R`  
- [ ] C) `-D`  
- [ ] D) `-T`

---

### Question 49 (Sujet 105)
Quelle commande SQL compte le **nombre de lignes** dans une table ?

- [ ] A) `SELECT COUNT(*) FROM table;`  
- [ ] B) `SELECT SUM(*) FROM table;`  
- [ ] C) `SELECT LINES(*) FROM table;`  
- [ ] D) `SELECT TOTAL(*) FROM table;`

---

### Question 50 (Sujet 107)
Dans `/etc/shadow`, combien de champs sont présents par ligne ?

- [ ] A) 7  
- [ ] B) 8  
- [ ] C) 9  
- [ ] D) 10

---

### Question 51 (Sujet 109)
Comment résoudre un nom de domaine en utilisant un **serveur DNS spécifique** ?

- [ ] A) `dig google.com`  
- [ ] B) `dig @8.8.8.8 google.com`  
- [ ] C) `host google.com 8.8.8.8`  

---

### Question 52 (Sujet 110)
Quelle est la limite par défaut qu'un **utilisateur normal peut modifier** pour ulimit ?

- [ ] A) Hard limit (augmenter)  
- [ ] B) Soft limit (augmenter jusqu'à hard)  
- [ ] C) Toutes les limites  
- [ ] D) Aucune limite

---

### Question 53 (Sujet 108)
Comment envoyer un message dans **syslog** depuis la ligne de commande ?

- [ ] A) `syslog "message"`  
- [ ] B) `logger "message"`  
- [ ] C) `log "message"`  
- [ ] D) `echo "message" > /var/log/syslog`

---

### Question 54 (Sujet 105)
Quel fichier est chargé pour un **shell non-login** bash ?

- [ ] A) `~/.bash_profile`  
- [ ] B) `~/.bashrc`  
- [ ] C) `/etc/profile`  
- [ ] D) `~/.profile`

---

### Question 55 (Sujet 107)
Quelle commande affiche les **groupes** d'un utilisateur ?

- [ ] A) `id user`  
- [ ] B) `groups user`  
- [ ] C) `getent group user`  
- [ ] D) Les deux A et B

---

### Question 56 (Sujet 110)
Comment **déchiffrer** un fichier GPG ?

- [ ] A) `gpg -d file.gpg`  
- [ ] B) `gpg --decrypt file.gpg`  
- [ ] C) `gpg -o output.txt -d file.gpg`  
- [ ] D) Toutes les réponses

---

### Question 57 (Sujet 109)
Quelle commande affiche la **table ARP** (moderne) ?

- [ ] A) `arp -a`  
- [ ] B) `ip neigh`  
- [ ] C) `ip arp`  
- [ ] D) `arp show`

---

### Question 58 (Sujet 108)
Dans `/etc/rsyslog.conf`, que signifie `mail.*` ?

- [ ] A) Facility mail, toutes priorities  
- [ ] B) Toutes facilities, priority mail  
- [ ] C) Mail uniquement priority info  
- [ ] D) Wildcard pour tous fichiers mail

---

### Question 59 (Sujet 110)
Quelle commande ajoute votre **clé privée à ssh-agent** ?

- [ ] A) `ssh-agent -add`  
- [ ] B) `ssh-add`  
- [ ] C) `ssh-agent load`  
- [ ] D) `ssh-keygen -add`

---

### Question 60 (Sujet 109)
Comment tester la **connectivité vers le port 80** d'un serveur avec netcat ?

- [ ] A) `nc -z host 80`  
- [ ] B) `nc -zv host 80`  
- [ ] C) `nc host 80`  
- [ ] D) Les réponses A et B

---

## ✅ GRILLE DE CORRECTION

### Réponses
```
1.D   2.C   3.B   4.C   5.B   6.D   7.C   8.B   9.D   10.B
11.D  12.B  13.B  14.B  15.B  16.B  17.D  18.B  19.D  20.A
21.B  22.B  23.B  24.A  25.D  26.B  27.D  28.D  29.D  30.B
31.B  32.D  33.B  34.D  35.B  36.C  37.B  38.B  39.A  40.D
41.A  42.B  43.D  44.D  45.B  46.B  47.D  48.A  49.A  50.C
51.B  52.B  53.B  54.B  55.D  56.D  57.B  58.A  59.B  60.D
```

### Explications détaillées

**Q1 (D)** : `env` et `printenv` affichent les variables d'environnement. `set` affiche aussi les variables locales et fonctions.

**Q2 (C)** : SUID = 4000, SGID = 2000, Sticky = 1000.

**Q3 (B)** : `useradd -m` crée le répertoire home. Sans `-m`, pas de home créé.

**Q4 (C)** : RFC 1918 : `10.0.0.0/8` (classe A), `172.16.0.0/12` (16 réseaux B), `192.168.0.0/16` (256 réseaux C).

**Q5 (B)** : `timedatectl set-ntp true` active la synchronisation NTP avec systemd-timesyncd.

**Q6 (D)** : Toutes ces commandes affichent les processus utilisant le port 80.

**Q7 (C)** : `$?` contient le code retour (exit status) de la dernière commande. 0 = succès, non-zéro = erreur.

**Q8 (B)** : Format crontab : `min heure jour mois jour_semaine commande`.

**Q9 (D)** : `ip route show` (ou `ip r`) affiche les routes. `route -n` est obsolète.

**Q10 (B)** : `$DISPLAY` contient l'affichage X11 (ex: `:0`, `hostname:0`).

**Q11 (D)** : `passwd -l user` ou `passwd --lock user` verrouillent le compte. `-L` est pour `usermod`.

**Q12 (B)** : `/etc/resolv.conf` contient les serveurs DNS (`nameserver 8.8.8.8`).

**Q13 (B)** : `DELETE FROM table WHERE condition` supprime des données. `DROP` supprime la table, `TRUNCATE` vide la table.

**Q14 (B)** : `usermod -aG sudo user` ajoute au groupe sudo EN PRÉSERVANT les autres groupes. `-G` seul écrase.

**Q15 (B)** : HTTPS utilise le port 443. HTTP = 80, HTTP alternatif = 8080.

**Q16 (B)** : `ssh-keygen -t ed25519` génère une paire Ed25519 (recommandé, 256 bits).

**Q17 (D)** : `journalctl -u ssh` ou `journalctl -u sshd` (selon distribution). `-u` = unit.

**Q18 (B)** : Login shell bash : `/etc/profile` → `~/.bash_profile` → `~/.bash_login` → `~/.profile`.

**Q19 (D)** : Toutes ces méthodes copient la clé publique. `ssh-copy-id` est la plus simple.

**Q20 (A)** : `30 8 * * 1` = 8h30, tous les lundis (0 et 7 = dimanche).

**Q21 (B)** : `ip route add default via 192.168.1.1`. `route add default gw` est obsolète.

**Q22 (B)** : `gdm3` (GNOME Display Manager). KDE = `sddm`, universel = `lightdm`.

**Q23 (B)** : `chage -l user` liste toutes les infos d'expiration du mot de passe.

**Q24 (A)** : `hwclock --systohc` synchronise système → matérielle. `--hctosys` fait l'inverse.

**Q25 (D)** : `-e` teste l'existence (fichier ou dossier), `-f` teste fichier régulier. Les deux marchent pour fichiers.

**Q26 (B)** : `/etc/passwd` contient 7 champs : login, x, UID, GID, GECOS, home, shell.

**Q27 (D)** : `ss -tunap` (moderne) ou `lsof -i`. `netstat` est obsolète (paquet net-tools).

**Q28 (D)** : Ed25519 est le plus sûr (256 bits, courbe 25519). DSA est déprécié.

**Q29 (D)** : Priorities (ordre croissant) : debug < info < notice < warn < err < crit < alert < `emerg`.

**Q30 (B)** : `for i in {1..10}; do echo $i; done`. Accolades `{}` pour expansion brace.

**Q31 (B)** : `@reboot` exécute au démarrage. `@daily` = minuit, `@weekly` = dimanche, `@monthly` = 1er.

**Q32 (D)** : `passwd -e user` ou `chage -d 0 user` forcent le changement au prochain login.

**Q33 (B)** : /26 = 64 IPs totales - 2 (réseau + broadcast) = 62 utilisables.

**Q34 (D)** : `journalctl -b` ou `journalctl --boot` affichent le boot actuel. `-k` = kernel seulement.

**Q35 (B)** : Wayland remplace progressivement X11 (plus moderne, sécurisé, performant).

**Q36 (C)** : `/etc/sudoers` doit TOUJOURS être édité avec `visudo` (vérifie syntaxe avant sauvegarde).

**Q37 (B)** : `-z "$var"` teste si variable est vide. `-n "$var"` teste si non vide.

**Q38 (B)** : `at now + 2 hours` planifie une tâche unique. `cron` est pour tâches répétitives.

**Q39 (A)** : `nmcli con add type ethernet ifname eth0 ip4 192.168.1.100/24` crée connexion NetworkManager statique.

**Q40 (D)** : `gpg -e -r alice file` ou `gpg --encrypt --recipient alice file`. `-e` = encrypt, `-r` = recipient.

**Q41 (A)** : `/etc/cron.daily/` contient scripts quotidiens (dont logrotate). `/etc/logrotate.d/` = configs rotation.

**Q42 (B)** : Entre guillemets, `"$@"` préserve chaque argument séparé, `"$*"` les joint en une chaîne.

**Q43 (D)** : `timedatectl set-timezone Europe/Paris` (recommandé) ou lien symbolique `/etc/localtime`.

**Q44 (D)** : `find / -perm -2000` (SGID + autres) ou `find / -perm /2000` (SGID OU autres). Sans `-` ou `/` = exact.

**Q45 (B)** : DNS utilise le port 53 (TCP et UDP). SMTP = 25, HTTP = 80, POP3 = 110.

**Q46 (B)** : `orca` est le lecteur d'écran GNOME. `onboard` = clavier virtuel, `kmag` = loupe KDE.

**Q47 (D)** : `tail -f /var/log/syslog` ou `journalctl -f -n 10` suivent logs en temps réel.

**Q48 (A)** : `-L` = tunnel local (port local → destination via intermédiaire). `-R` = tunnel distant.

**Q49 (A)** : `SELECT COUNT(*) FROM table;` compte les lignes. `SUM()` = somme, `AVG()` = moyenne.

**Q50 (C)** : `/etc/shadow` contient 9 champs (nom, hash, lastchange, min, max, warn, inactive, expire, reserved).

**Q51 (B)** : `dig @8.8.8.8 google.com` utilise serveur DNS spécifique (8.8.8.8).

**Q52 (B)** : Utilisateurs peuvent augmenter soft limit jusqu'à hard, et réduire hard. Seul root augmente hard.

**Q53 (B)** : `logger "message"` écrit dans syslog. `logger -p user.warn "message"` pour priority spécifique.

**Q54 (B)** : Shell non-login : `/etc/bash.bashrc` → `~/.bashrc`.

**Q55 (D)** : `id user` affiche UID, GID, groupes. `groups user` affiche seulement groupes.

**Q56 (D)** : `gpg -d file.gpg` (affiche), `gpg --decrypt file.gpg`, `gpg -o output.txt -d file.gpg` (vers fichier).

**Q57 (B)** : `ip neigh` affiche table ARP (moderne). `arp -a` est obsolète.

**Q58 (A)** : `mail.*` = facility mail, toutes priorities (* = wildcard priorities).

**Q59 (B)** : `ssh-add` ajoute clé privée à ssh-agent. Demande passphrase une fois.

**Q60 (D)** : `nc -z host 80` (silencieux) ou `nc -zv host 80` (verbose) testent connectivité port.

---

## 📊 Grille d'évaluation

### Score par sujet
- **Sujet 105 (Q1,7,13,18,25,30,37,42,49,54)** : /11 questions
- **Sujet 106 (Q10,22,35,46)** : /4 questions  
- **Sujet 107 (Q3,8,14,20,26,31,38,43,50,55)** : /12 questions
- **Sujet 108 (Q5,12,17,24,29,34,41,47,53,58)** : /10 questions
- **Sujet 109 (Q4,9,15,21,27,33,39,45,51,57,60)** : /8 questions
- **Sujet 110 (Q2,6,11,16,19,23,28,32,36,40,44,48,52,56,59)** : /15 questions

### Barème final
| Score | Niveau | Statut |
|-------|--------|--------|
| **52-60** | 700-800 pts | 🏆 Excellent - Prêt pour l'examen |
| **45-51** | 600-699 pts | ✅ Très bien - Presque prêt |
| **38-44** | 500-599 pts | ⚠️ Passable - Réviser zones faibles |
| **30-37** | 400-499 pts | 📚 Insuffisant - Révisions approfondies |
| **< 30** | < 400 pts | 🔄 Revoir tout le programme |

---

## 💡 Conseils post-examen

### Si score < 500 pts (38/60)
1. Identifiez vos sujets faibles
2. Relisez les Notes de révision correspondantes
3. Refaites les QCM par sujet
4. Pratiquez sur machine virtuelle
5. Retentez le Mock Exam dans 1 semaine

### Si score 500-699 pts (38-51/60)
1. Analysez vos erreurs par sujet
2. Révisez les fiches des sujets faibles
3. Pratiquez les commandes problématiques
4. Refaites ce Mock Exam demain
5. Vous êtes proche du succès !

### Si score ≥ 700 pts (52+/60)
1. Félicitations ! Vous êtes prêt 🎉
2. Révisez les fiches 1-2 jours avant l'examen
3. Concentrez-vous sur les sujets 110 (12 pts) et 107 (12 pts)
4. Restez confiant et détendu
5. Inscrivez-vous à l'examen officiel !

---

## 🎯 Points clés à maîtriser absolument

### Top 20 commandes fréquentes
```bash
# User management
useradd -m, usermod -aG, passwd -l, chage -M/-d, id, groups

# Cron
crontab -e/-l, */15 * * * *, @daily, @reboot

# Networking
ip addr, ip route, nmcli con, dig, ss -tulpn, ping

# Security
find -perm -4000, ssh-keygen -t ed25519, ssh-copy-id
gpg -e -r, gpg -d, visudo, lsof -i

# Logs & Time
journalctl -u/-f/-b, timedatectl set-ntp/set-timezone
hwclock --systohc, logger

# Scripts
$?, $@, [ -f ], for i in {1..10}
```

### Pièges fréquents
❌ `usermod -G` écrase groupes → utiliser `-aG`  
❌ Oublier `/24` dans `ip addr add`  
❌ `find -perm 4000` (exact) vs `-perm -4000` (inclusif)  
❌ Confondre `hwclock --hctosys` et `--systohc`  
❌ Éditer `/etc/sudoers` sans `visudo`  
❌ DSA est déprécié, utiliser Ed25519  

---

**Bonne chance pour votre certification LPIC-1 102-500 ! 🎓🔐**

*N'oubliez pas : la pratique est essentielle. Testez toutes ces commandes sur une machine virtuelle !*
