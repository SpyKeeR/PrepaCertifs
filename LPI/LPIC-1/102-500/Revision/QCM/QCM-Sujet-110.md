# 📝 QCM - Sujet 110 : Sécurité

## 🎯 Informations sur le QCM

- **Sujet** : 110 - Sécurité
- **Nombre de questions** : 70
- **Poids du sujet** : 12 points
- **Durée estimée** : 85 minutes

### Répartition des questions

- **110.1** - Tâches d'administration de sécurité : 25 questions
- **110.2** - Configuration de la sécurité du système : 20 questions
- **110.3** - Sécurisation des données avec le chiffrement : 25 questions

---

## 📋 Questions

### 110.1 - Tâches d'administration de sécurité (25 questions)

#### Question 1
Quelle est la représentation numérique du bit SUID ?

- [ ] A) 1000  
- [ ] B) 2000  
- [ ] C) 4000  
- [ ] D) 8000  

#### Question 2
Quelle commande trouve tous les fichiers avec le bit SUID dans /usr/bin (+ autres permissions) ?

- [ ] A) `find /usr/bin -perm 4000`  
- [ ] B) `find /usr/bin -perm -4000`  
- [ ] C) `find /usr/bin -perm /4000`  
- [ ] D) `find /usr/bin -perm +4000`  

#### Question 3
Comment apparaît le bit SUID dans les permissions symboliques avec droit d'exécution ?

- [ ] A) S (majuscule)  
- [ ] B) s (minuscule)  
- [ ] C) x  
- [ ] D) t  

#### Question 4
Quelle commande définit le bit SGID sur un répertoire shared_dir ?

- [ ] A) `chmod 1755 shared_dir`  
- [ ] B) `chmod 2755 shared_dir`  
- [ ] C) `chmod 4755 shared_dir`  
- [ ] D) `chmod 6755 shared_dir`  

#### Question 5
Quelle option de `find -perm` recherche des fichiers avec SUID OU SGID ?

- [ ] A) `find -perm 6000`  
- [ ] B) `find -perm -6000`  
- [ ] C) `find -perm /6000`  
- [ ] D) `find -perm +6000`  

#### Question 6
Dans le résultat de `passwd -S carol`, que signifie le statut "L" ?

- [ ] A) Logged in (connecté)  
- [ ] B) Locked (verrouillé)  
- [ ] C) Login required (connexion requise)  
- [ ] D) Limited (limité)  

#### Question 7
Quelle commande force l'utilisatrice emma à changer son mot de passe au prochain login ?

- [ ] A) `passwd -e emma`  
- [ ] B) `chage -d 0 emma`  
- [ ] C) Les deux commandes A et B  
- [ ] D) `usermod -f 0 emma`  

#### Question 8
Quelle commande affiche les informations d'expiration du mot de passe de l'utilisateur john ?

- [ ] A) `passwd -l john`  
- [ ] B) `chage -l john`  
- [ ] C) `usermod -l john`  
- [ ] D) `getent shadow john`  

#### Question 9
Comment définir la durée maximale de validité d'un mot de passe à 90 jours avec chage ?

- [ ] A) `chage -m 90 utilisateur`  
- [ ] B) `chage -M 90 utilisateur`  
- [ ] C) `chage -d 90 utilisateur`  
- [ ] D) `chage -W 90 utilisateur`  

#### Question 10
Quelle valeur utiliser avec `chage -M` pour désactiver l'expiration du mot de passe ?

- [ ] A) 0  
- [ ] B) -1  
- [ ] C) 99999  
- [ ] D) unlimited  

#### Question 11
Quelle commande affiche tous les fichiers réseau Internet avec lsof ?

- [ ] A) `lsof -i`  
- [ ] B) `lsof -n`  
- [ ] C) `lsof -p`  
- [ ] D) `lsof -u`  

#### Question 12
Comment afficher les processus utilisant le port 80 avec fuser ?

- [ ] A) `fuser 80`  
- [ ] B) `fuser -n tcp 80`  
- [ ] C) `fuser -p 80`  
- [ ] D) `fuser -i 80`  

#### Question 13
Quelle commande netstat affiche tous les ports TCP en écoute en format numérique ?

- [ ] A) `netstat -tln`  
- [ ] B) `netstat -uln`  
- [ ] C) `netstat -tan`  
- [ ] D) `netstat -rn`  

#### Question 14
Quelle est la commande moderne équivalente à netstat ?

- [ ] A) `nc`  
- [ ] B) `ss`  
- [ ] C) `nmap`  
- [ ] D) `lsof`  

#### Question 15
Quelle option de nmap effectue un scan rapide des 100 ports les plus courants ?

- [ ] A) `-f`  
- [ ] B) `-F`  
- [ ] C) `-fast`  
- [ ] D) `-quick`  

#### Question 16
Comment scanner les ports 22, 80 et 443 sur localhost avec nmap ?

- [ ] A) `nmap -p 22 80 443 localhost`  
- [ ] B) `nmap -p 22-443 localhost`  
- [ ] C) `nmap -p 22,80,443 localhost`  
- [ ] D) `nmap -ports 22,80,443 localhost`  

#### Question 17
Quelle commande affiche toutes les limites soft de l'utilisateur actuel ?

- [ ] A) `ulimit`  
- [ ] B) `ulimit -a`  
- [ ] C) `ulimit -H`  
- [ ] D) `ulimit -S`  

#### Question 18
Comment afficher le nombre maximum de processus (limite hard) ?

- [ ] A) `ulimit -u`  
- [ ] B) `ulimit -Su`  
- [ ] C) `ulimit -Hu`  
- [ ] D) `ulimit -p`  

#### Question 19
Quelle est la différence entre soft limit et hard limit ?

- [ ] A) Soft peut être augmentée par utilisateur normal, hard seulement par root  
- [ ] B) Hard peut être augmentée par utilisateur normal, soft seulement par root  
- [ ] C) Aucune différence  
- [ ] D) Soft est temporaire, hard est permanente  

#### Question 20
Dans quel fichier les limites persistantes sont-elles configurées ?

- [ ] A) `/etc/limits`  
- [ ] B) `/etc/security/limits`  
- [ ] C) `/etc/security/limits.conf`  
- [ ] D) `/etc/ulimit.conf`  

#### Question 21
Quelle commande affiche les derniers utilisateurs connectés ?

- [ ] A) `who`  
- [ ] B) `w`  
- [ ] C) `last`  
- [ ] D) `users`  

#### Question 22
Quel fichier log est utilisé par la commande `last` ?

- [ ] A) `/var/log/auth.log`  
- [ ] B) `/var/log/wtmp`  
- [ ] C) `/var/log/lastlog`  
- [ ] D) `/var/log/secure`  

#### Question 23
Quelle différence entre `su` et `su -` ?

- [ ] A) `su -` charge l'environnement de l'utilisateur cible  
- [ ] B) `su` charge l'environnement de l'utilisateur cible  
- [ ] C) Aucune différence  
- [ ] D) `su -` nécessite le mot de passe root  

#### Question 24
Quelle commande doit toujours être utilisée pour éditer /etc/sudoers ?

- [ ] A) `nano /etc/sudoers`  
- [ ] B) `vi /etc/sudoers`  
- [ ] C) `visudo`  
- [ ] D) `sudo edit`  

#### Question 25
Dans /etc/sudoers, que signifie la directive `NOPASSWD:` ?

- [ ] A) L'utilisateur n'a pas de mot de passe  
- [ ] B) Pas de mot de passe requis pour exécuter la commande  
- [ ] C) Le mot de passe est désactivé  
- [ ] D) Le mot de passe expire immédiatement  

---

### 110.2 - Configuration de la sécurité du système (20 questions)

#### Question 26
Combien de champs contient une ligne du fichier /etc/passwd ?

- [ ] A) 5  
- [ ] B) 7  
- [ ] C) 9  
- [ ] D) 10  

#### Question 27
Dans /etc/passwd, que signifie le "x" dans le deuxième champ ?

- [ ] A) Le compte est désactivé  
- [ ] B) Le mot de passe est dans /etc/shadow  
- [ ] C) Aucun mot de passe n'est défini  
- [ ] D) Le compte est verrouillé  

#### Question 28
Comment empêcher temporairement tous les utilisateurs (sauf root) de se connecter ?

- [ ] A) Créer le fichier `/etc/nologin`  
- [ ] B) Exécuter `systemctl stop login`  
- [ ] C) Modifier `/etc/passwd`  
- [ ] D) Créer `/etc/no-login`  

#### Question 29
Comment empêcher définitivement l'utilisateur emma de se connecter ?

- [ ] A) `passwd -l emma`  
- [ ] B) `usermod -s /sbin/nologin emma`  
- [ ] C) `chage -E -1 emma`  
- [ ] D) Créer `/home/emma/nologin`  

#### Question 30
Quel est le rôle principal de xinetd ?

- [ ] A) Gérer les services réseau à la demande  
- [ ] B) Configurer le pare-feu  
- [ ] C) Chiffrer les connexions  
- [ ] D) Gérer les utilisateurs  

#### Question 31
Quel est le fichier de configuration principal de xinetd ?

- [ ] A) `/etc/xinetd.d/xinetd.conf`  
- [ ] B) `/etc/xinetd.conf`  
- [ ] C) `/etc/inet.conf`  
- [ ] D) `/etc/services.conf`  

#### Question 32
Dans une configuration xinetd, que signifie `socket_type = stream` ?

- [ ] A) Socket UDP  
- [ ] B) Socket TCP  
- [ ] C) Socket ICMP  
- [ ] D) Socket RAW  

#### Question 33
Quelle directive xinetd active ou désactive un service ?

- [ ] A) `enabled`  
- [ ] B) `active`  
- [ ] C) `disable`  
- [ ] D) `start`  

#### Question 34
Quelle commande démarre une unité socket SSH avec systemd ?

- [ ] A) `systemctl start ssh`  
- [ ] B) `systemctl start ssh.socket`  
- [ ] C) `systemctl start sshd.socket`  
- [ ] D) Les réponses B et C sont correctes  

#### Question 35
Sur un système SysV-init (Debian), comment désactiver un service au démarrage ?

- [ ] A) `service SERVICE stop`  
- [ ] B) `update-rc.d SERVICE remove`  
- [ ] C) `chkconfig SERVICE off`  
- [ ] D) `systemctl disable SERVICE`  

#### Question 36
Quelle commande liste tous les services actifs sur systemd ?

- [ ] A) `systemctl list-services`  
- [ ] B) `systemctl list-units --type service --state active`  
- [ ] C) `systemctl status --all`  
- [ ] D) `service --status-all`  

#### Question 37
Comment désactiver définitivement le service cups avec systemd ?

- [ ] A) `systemctl stop cups`  
- [ ] B) `systemctl disable cups`  
- [ ] C) `systemctl disable cups --now`  
- [ ] D) `systemctl remove cups`  

#### Question 38
Quelle commande vérifie si un démon supporte les TCP wrappers ?

- [ ] A) `ldd /usr/sbin/sshd | grep wrapper`  
- [ ] B) `ldd /usr/sbin/sshd | grep libwrap`  
- [ ] C) `tcpwrap --check sshd`  
- [ ] D) `which tcpwrap`  

#### Question 39
Quel fichier contient les règles de blocage pour les TCP wrappers ?

- [ ] A) `/etc/hosts.allow`  
- [ ] B) `/etc/hosts.deny`  
- [ ] C) `/etc/tcpwrappers.deny`  
- [ ] D) `/etc/deny.conf`  

#### Question 40
Dans quel ordre les TCP wrappers évaluent-ils les fichiers ?

- [ ] A) deny puis allow  
- [ ] B) allow puis deny  
- [ ] C) allow uniquement  
- [ ] D) deny uniquement  

#### Question 41
Quelle syntaxe dans /etc/hosts.deny bloque SSH pour tous sauf le réseau local ?

- [ ] A) `sshd: ALL EXCEPT LOCAL`  
- [ ] B) `sshd: ALL`  
- [ ] C) `sshd: !LOCAL`  
- [ ] D) `ALL: sshd`  

#### Question 42
Comment autoriser SSH uniquement depuis 192.168.1.0/24 avec TCP wrappers ?

- [ ] A) Dans /etc/hosts.allow : `sshd: 192.168.1.`  
- [ ] B) Dans /etc/hosts.deny : `sshd: ALL EXCEPT 192.168.1.0/24`  
- [ ] C) Les deux (deny ALL, allow 192.168.1.)  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 43
Dans /etc/shadow, que signifie un "!" dans le champ du mot de passe ?

- [ ] A) Mot de passe expiré  
- [ ] B) Compte verrouillé  
- [ ] C) Pas de mot de passe  
- [ ] D) Mot de passe temporaire  

#### Question 44
Quelle commande affiche les services réseau en écoute (moderne, non obsolète) ?

- [ ] A) `netstat -ltu`  
- [ ] B) `ss -ltu`  
- [ ] C) `lsof -i`  
- [ ] D) Les réponses B et C  

#### Question 45
Sur Red Hat, comment désactiver un service au démarrage (SysV-init) ?

- [ ] A) `service SERVICE off`  
- [ ] B) `update-rc.d SERVICE remove`  
- [ ] C) `chkconfig SERVICE off`  
- [ ] D) `rc.d SERVICE off`  

---

### 110.3 - Sécurisation des données avec le chiffrement (25 questions)

#### Question 46
Quelle commande se connecte en SSH à l'hôte 192.168.1.10 en tant qu'utilisateur bob ?

- [ ] A) `ssh bob 192.168.1.10`  
- [ ] B) `ssh 192.168.1.10 bob`  
- [ ] C) `ssh bob@192.168.1.10`  
- [ ] D) `ssh -u bob 192.168.1.10`  

#### Question 47
Quelle commande génère une paire de clés Ed25519 ?

- [ ] A) `ssh-keygen -t ed25519`  
- [ ] B) `ssh-keygen -t ecdsa -b 25519`  
- [ ] C) `ssh-keygen -e ed25519`  
- [ ] D) `ssh-keygen --ed25519`  

#### Question 48
Parmi ces algorithmes SSH, lequel est considéré comme le plus sûr ?

- [ ] A) RSA 4096  
- [ ] B) DSA  
- [ ] C) ECDSA 521  
- [ ] D) Ed25519  

#### Question 49
Quel algorithme SSH est déprécié depuis OpenSSH 7.0 ?

- [ ] A) RSA  
- [ ] B) DSA  
- [ ] C) ECDSA  
- [ ] D) Ed25519  

#### Question 50
Quelle commande copie automatiquement votre clé publique SSH sur un serveur distant ?

- [ ] A) `ssh-copy user@host`  
- [ ] B) `ssh-copy-id user@host`  
- [ ] C) `scp ~/.ssh/id_rsa.pub user@host`  
- [ ] D) `ssh-keygen --copy user@host`  

#### Question 51
Dans quel fichier sur le serveur sont stockées les clés publiques autorisées ?

- [ ] A) `~/.ssh/authorized_keys`  
- [ ] B) `~/.ssh/known_hosts`  
- [ ] C) `~/.ssh/id_rsa.pub`  
- [ ] D) `/etc/ssh/authorized_keys`  

#### Question 52
Dans quel fichier sur le client sont stockées les empreintes des hôtes connus ?

- [ ] A) `~/.ssh/authorized_keys`  
- [ ] B) `~/.ssh/known_hosts`  
- [ ] C) `~/.ssh/config`  
- [ ] D) `/etc/ssh/known_hosts`  

#### Question 53
Comment supprimer l'empreinte de l'hôte 192.168.1.10 du fichier known_hosts ?

- [ ] A) `ssh-keygen -R 192.168.1.10`  
- [ ] B) `ssh-keygen -D 192.168.1.10`  
- [ ] C) `ssh-remove 192.168.1.10`  
- [ ] D) `ssh-keygen --remove 192.168.1.10`  

#### Question 54
Quelle commande lance l'agent d'authentification SSH dans un nouveau shell ?

- [ ] A) `ssh-agent`  
- [ ] B) `ssh-agent bash`  
- [ ] C) `ssh-agent /bin/bash`  
- [ ] D) `eval $(ssh-agent)`  

#### Question 55
Quelle commande ajoute votre clé privée à l'agent SSH ?

- [ ] A) `ssh-add`  
- [ ] B) `ssh-agent --add`  
- [ ] C) `ssh-key-add`  
- [ ] D) `ssh load-key`  

#### Question 56
Où sont stockées les clés d'hôte du serveur SSH ?

- [ ] A) `~/.ssh/`  
- [ ] B) `/etc/ssh/`  
- [ ] C) `/var/lib/ssh/`  
- [ ] D) `/usr/share/ssh/`  

#### Question 57
Quelles sont les permissions correctes pour une clé privée SSH ?

- [ ] A) 644 (-rw-r--r--)  
- [ ] B) 600 (-rw-------)  
- [ ] C) 700 (drwx------)  
- [ ] D) 400 (-r--------)  

#### Question 58
Quelle option SSH crée un tunnel de port local ?

- [ ] A) `-L`  
- [ ] B) `-R`  
- [ ] C) `-D`  
- [ ] D) `-T`  

#### Question 59
Quelle commande crée un tunnel local du port 8080 vers www.example.com:80 via serveur ?

- [ ] A) `ssh -L 8080:www.example.com:80 serveur`  
- [ ] B) `ssh -R 8080:www.example.com:80 serveur`  
- [ ] C) `ssh -T 8080:www.example.com:80 serveur`  
- [ ] D) `ssh -D 8080 serveur`  

#### Question 60
Quelle option SSH crée un tunnel de port distant ?

- [ ] A) `-L`  
- [ ] B) `-R`  
- [ ] C) `-D`  
- [ ] D) `-T`  

#### Question 61
Quelle option SSH permet de ne pas ouvrir de shell interactif (tunneling uniquement) ?

- [ ] A) `-N`  
- [ ] B) `-n`  
- [ ] C) `-T`  
- [ ] D) `-t`  

#### Question 62
Comment activer le X11 forwarding avec SSH ?

- [ ] A) `ssh -x user@host`  
- [ ] B) `ssh -X user@host`  
- [ ] C) `ssh --x11 user@host`  
- [ ] D) `ssh -F user@host`  

#### Question 63
Quelle directive dans sshd_config autorise le X11 forwarding ?

- [ ] A) `X11Forward yes`  
- [ ] B) `X11Forwarding yes`  
- [ ] C) `ForwardX11 yes`  
- [ ] D) `AllowX11 yes`  

#### Question 64
Quelle commande génère une paire de clés GPG ?

- [ ] A) `gpg --generate-key`  
- [ ] B) `gpg --gen-key`  
- [ ] C) `gpg --create-key`  
- [ ] D) `gpg --new-key`  

#### Question 65
Quelle commande liste toutes vos clés publiques GPG ?

- [ ] A) `gpg --list-keys`  
- [ ] B) `gpg --list-public-keys`  
- [ ] C) `gpg -k`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 66
Comment exporter votre clé publique GPG en format ASCII ?

- [ ] A) `gpg --export --armor utilisateur > cle.asc`  
- [ ] B) `gpg -a --export utilisateur > cle.asc`  
- [ ] C) `gpg --armor-export utilisateur > cle.asc`  
- [ ] D) Les réponses A et B sont correctes  

#### Question 67
Quelle commande chiffre le fichier message.txt pour l'utilisateur bob ?

- [ ] A) `gpg --encrypt --recipient bob message.txt`  
- [ ] B) `gpg -e -r bob message.txt`  
- [ ] C) `gpg --recipient bob --encrypt message.txt`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 68
Quelle commande déchiffre le fichier encrypted.gpg ?

- [ ] A) `gpg --decrypt encrypted.gpg`  
- [ ] B) `gpg -d encrypted.gpg`  
- [ ] C) `gpg --output message.txt --decrypt encrypted.gpg`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 69
Quelle commande signe le fichier document.txt ?

- [ ] A) `gpg --sign document.txt`  
- [ ] B) `gpg -s document.txt`  
- [ ] C) `gpg --output document.sig --sign document.txt`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 70
Comment vérifier la signature d'un fichier document.txt.sig ?

- [ ] A) `gpg --verify document.txt.sig`  
- [ ] B) `gpg --check document.txt.sig`  
- [ ] C) `gpg -v document.txt.sig`  
- [ ] D) `gpg --validate document.txt.sig`  

---

## ✅ Réponses et explications

### 110.1 - Tâches d'administration de sécurité

#### Réponse 1 : C
**Explication** : Le bit SUID est représenté par **4000** en notation numérique. SGID = 2000, Sticky = 1000. Pour l'appliquer : `chmod 4755 fichier`.

#### Réponse 2 : B
**Explication** : **find /usr/bin -perm -4000** trouve les fichiers avec SUID + autres permissions possibles. Sans le tiret (`-4000`), cela chercherait uniquement SUID sans aucune autre permission.

#### Réponse 3 : B
**Explication** : Le **s minuscule** (rws) indique SUID + permission d'exécution. S majuscule (rwS) = SUID sans exécution sous-jacente.

#### Réponse 4 : B
**Explication** : **chmod 2755** définit le SGID (2000) + permissions 755. Sur un répertoire, SGID fait hériter le groupe propriétaire aux nouveaux fichiers créés.

#### Réponse 5 : C
**Explication** : **find -perm /6000** cherche fichiers avec SUID (4000) OU SGID (2000). Le `/` signifie "au moins une des permissions".

#### Réponse 6 : B
**Explication** : Dans `passwd -S`, **L** signifie "Locked" (verrouillé). P = password valide, NP = no password. Pour verrouiller : `passwd -l utilisateur`.

#### Réponse 7 : C
**Explication** : **Les deux commandes fonctionnent** : `passwd -e` expire le mot de passe, `chage -d 0` met la date du dernier changement à 0 (époque), forçant le changement au login.

#### Réponse 8 : B
**Explication** : **chage -l utilisateur** affiche les informations d'expiration du mot de passe (last change, expiration, warning, etc.). `passwd -l` verrouille le compte.

#### Réponse 9 : B
**Explication** : **chage -M 90** définit le nombre MAXimal de jours de validité. `-m` = minimum (jours entre changements), `-W` = warning (avertissement).

#### Réponse 10 : C
**Explication** : **99999** est la valeur conventionnelle pour désactiver l'expiration. `chage -M 99999 utilisateur`. La valeur -1 pour `-E` désactive l'expiration du compte.

#### Réponse 11 : A
**Explication** : **lsof -i** affiche tous les fichiers réseau Internet (sockets, connexions). `-i :PORT` filtre par port, `-i@IP` par hôte, `-i4/-i6` par protocole IP.

#### Réponse 12 : B
**Explication** : **fuser -n tcp 80** affiche les processus utilisant le port TCP 80. `-n` = namespace (tcp/udp), `-v` = verbose pour plus de détails.

#### Réponse 13 : A
**Explication** : **netstat -tln** : `-t` = TCP, `-l` = listening (écoute), `-n` = numérique (pas de résolution DNS). `-u` serait pour UDP.

#### Réponse 14 : B
**Explication** : **ss** (socket statistics) est l'équivalent moderne de netstat. Syntaxe identique : `ss -tulnp`. Plus rapide et mieux maintenu.

#### Réponse 15 : B
**Explication** : **nmap -F** (majuscule) effectue un Fast scan des 100 ports les plus courants au lieu des 1000 par défaut. Plus rapide pour découverte.

#### Réponse 16 : C
**Explication** : **nmap -p 22,80,443** scanne les ports spécifiés séparés par des virgules. `-p 22-80` scanne une plage, `-p-` scanne tous les ports.

#### Réponse 17 : B
**Explication** : **ulimit -a** affiche toutes les limites soft (par défaut). `-Ha` afficherait les limites hard. Sans option, `ulimit` affiche seulement les blocs fichiers.

#### Réponse 18 : C
**Explication** : **ulimit -Hu** affiche la limite Hard (-H) sur le nombre de processUs (-u). `-Su` serait la limite soft.

#### Réponse 19 : A
**Explication** : Les utilisateurs normaux peuvent **augmenter soft limits** (jusqu'à hard) et **réduire hard limits**. Seul **root peut augmenter hard limits**.

#### Réponse 20 : C
**Explication** : **/etc/security/limits.conf** contient les limites persistantes. Format : `utilisateur type ressource valeur`. Type = soft/hard/-.

#### Réponse 21 : C
**Explication** : **last** affiche l'historique des connexions depuis `/var/log/wtmp`. `who` = actuellement connectés, `w` = connectés + activité.

#### Réponse 22 : B
**Explication** : **last** lit `/var/log/wtmp`. `/var/log/lastlog` contient la dernière connexion par utilisateur. `/var/log/auth.log` contient les tentatives d'authentification.

#### Réponse 23 : A
**Explication** : **su -** (avec tiret) charge l'environnement complet de l'utilisateur cible (comme un vrai login). Sans tiret, l'environnement actuel est conservé.

#### Réponse 24 : C
**Explication** : **visudo** doit TOUJOURS être utilisé pour éditer /etc/sudoers. Il vérifie la syntaxe avant de sauvegarder, évitant de casser sudo.

#### Réponse 25 : B
**Explication** : **NOPASSWD:** indique qu'aucun mot de passe n'est requis pour exécuter la commande. Exemple : `carol ALL=(ALL) NOPASSWD: /usr/bin/systemctl status apache2`.

### 110.2 - Configuration de la sécurité du système

#### Réponse 26 : B
**Explication** : **/etc/passwd contient 7 champs** : login, password placeholder (x), UID, GID, GECOS, home dir, shell. Séparés par `:`.

#### Réponse 27 : B
**Explication** : Le **x** dans le 2e champ signifie que le mot de passe haché est dans `/etc/shadow` (shadow password). Vide = pas de mot de passe, ! = verrouillé.

#### Réponse 28 : A
**Explication** : Créer **/etc/nologin** bloque temporairement toutes les connexions sauf root. Le contenu du fichier s'affiche aux utilisateurs. `rm /etc/nologin` pour réactiver.

#### Réponse 29 : B
**Explication** : **usermod -s /sbin/nologin emma** définit le shell nologin, empêchant définitivement la connexion. `/bin/false` fonctionne aussi. `passwd -l` verrouille temporairement.

#### Réponse 30 : A
**Explication** : **xinetd** est un super-démon qui **surveille les ports et démarre services à la demande**, économisant les ressources. Alternative moderne : systemd.socket.

#### Réponse 31 : B
**Explication** : **/etc/xinetd.conf** est le fichier principal. Il contient les defaults et `includedir /etc/xinetd.d/` pour charger les configs par service.

#### Réponse 32 : B
**Explication** : **socket_type = stream** indique un socket TCP. `dgram` = UDP. D'autres valeurs existent (raw, seqpacket) mais moins courantes.

#### Réponse 33 : C
**Explication** : **disable = no/yes** active ou désactive un service dans xinetd. `disable = no` active, `disable = yes` désactive.

#### Réponse 34 : D
**Explication** : **Les deux commandes fonctionnent** selon la distribution : `systemctl start ssh.socket` (Debian) ou `systemctl start sshd.socket` (Red Hat).

#### Réponse 35 : B
**Explication** : Sur Debian SysV-init, **update-rc.d SERVICE remove** désactive un service au démarrage. `chkconfig` est pour Red Hat.

#### Réponse 36 : B
**Explication** : **systemctl list-units --type service --state active** liste les services actifs. `systemctl list-units --type service` liste tous les services (actifs + inactifs).

#### Réponse 37 : C
**Explication** : **systemctl disable cups --now** désactive ET arrête immédiatement le service. `disable` seul désactive au démarrage mais ne l'arrête pas maintenant.

#### Réponse 38 : B
**Explication** : **ldd /usr/sbin/sshd | grep libwrap** vérifie si le démon est lié à la bibliothèque libwrap (support TCP wrappers). Si résultat vide, pas de support.

#### Réponse 39 : B
**Explication** : **/etc/hosts.deny** contient les règles de blocage. `/etc/hosts.allow` contient les autorisations. Ordre d'évaluation : allow → deny.

#### Réponse 40 : B
**Explication** : Ordre d'évaluation : **allow puis deny**. Si une règle allow correspond, accès autorisé (deny ignoré). Sinon, vérification deny.

#### Réponse 41 : A
**Explication** : Dans `/etc/hosts.deny` : **sshd: ALL EXCEPT LOCAL** bloque tout le monde sauf le réseau local. `sshd: ALL` bloque tout le monde, `sshd: !LOCAL` n'est pas une syntaxe valide.

#### Réponse 42 : C
**Explication** : **Les deux méthodes fonctionnent** : deny ALL dans hosts.deny, puis allow 192.168.1. dans hosts.allow. Syntaxe : `192.168.1.` (avec point final) ou `192.168.1.0/255.255.255.0`.

#### Réponse 43 : B
**Explication** : Un **!** au début du champ mot de passe dans /etc/shadow signifie **compte verrouillé**. `!!` = jamais de mot de passe défini, vide = pas de mot de passe.

#### Réponse 44 : D
**Explication** : **ss -ltu** (moderne) et **lsof -i** affichent les services en écoute. `netstat -ltu` fonctionne mais est obsolète (paquet net-tools).

#### Réponse 45 : C
**Explication** : Sur Red Hat SysV-init, **chkconfig SERVICE off** désactive au démarrage. `update-rc.d` est pour Debian. Sur systemd : `systemctl disable`.

### 110.3 - Sécurisation des données avec le chiffrement

#### Réponse 46 : C
**Explication** : **ssh bob@192.168.1.10** est la syntaxe correcte. Format : `ssh [user@]host [commande]`. Si user non spécifié, utilise le nom local.

#### Réponse 47 : A
**Explication** : **ssh-keygen -t ed25519** génère une paire Ed25519. `-t` = type (rsa, dsa, ecdsa, ed25519). Ed25519 a toujours 256 bits (pas besoin de `-b`).

#### Réponse 48 : D
**Explication** : **Ed25519** est considéré comme le plus sûr : courbe 25519 robuste, 256 bits, rapide. ECDSA 521 est aussi très bon, RSA 4096 est sûr mais plus lent.

#### Réponse 49 : B
**Explication** : **DSA** est déprécié depuis OpenSSH 7.0 (vulnérabilités). Limité à 1024 bits. À éviter absolument. Préférer Ed25519, ECDSA ou RSA ≥ 2048.

#### Réponse 50 : B
**Explication** : **ssh-copy-id user@host** copie automatiquement votre clé publique dans `~/.ssh/authorized_keys` du serveur. Méthode recommandée et simple.

#### Réponse 51 : A
**Explication** : **~/.ssh/authorized_keys** sur le serveur contient les clés publiques autorisées à se connecter. Permissions : 600 ou 644. Répertoire ~/.ssh : 700.

#### Réponse 52 : B
**Explication** : **~/.ssh/known_hosts** sur le client stocke les empreintes des clés d'hôtes connus. Vérifie l'identité du serveur à chaque connexion (prévient MITM).

#### Réponse 53 : A
**Explication** : **ssh-keygen -R 192.168.1.10** supprime l'empreinte de l'hôte de known_hosts. Utile après changement de clé serveur ou réinstallation.

#### Réponse 54 : C
**Explication** : **ssh-agent /bin/bash** lance l'agent dans un nouveau shell bash. Alternative : `eval $(ssh-agent)` dans le shell actuel.

#### Réponse 55 : A
**Explication** : **ssh-add** ajoute la clé privée par défaut (~/.ssh/id_*) à l'agent. `ssh-add chemin/cle` pour une clé spécifique. Demande la phrase de passe une seule fois.

#### Réponse 56 : B
**Explication** : Les clés d'hôte du serveur sont dans **/etc/ssh/** : ssh_host_rsa_key, ssh_host_ecdsa_key, ssh_host_ed25519_key (+ .pub pour publiques).

#### Réponse 57 : B
**Explication** : Les clés privées SSH doivent avoir permissions **600** (-rw-------) : lisible/modifiable uniquement par propriétaire. Sinon SSH refuse de les utiliser.

#### Réponse 58 : A
**Explication** : **-L** crée un tunnel Local (port forwarding local). Syntaxe : `ssh -L port_local:destination:port_dest intermédiaire`.

#### Réponse 59 : A
**Explication** : **ssh -L 8080:www.example.com:80 serveur** crée un tunnel : localhost:8080 → serveur → www.example.com:80. Tout trafic chiffré via SSH.

#### Réponse 60 : B
**Explication** : **-R** crée un tunnel Remote (port forwarding distant/inversé). Syntaxe : `ssh -R port_distant:destination:port_dest serveur_distant`.

#### Réponse 61 : A
**Explication** : **-N** indique "pas de commande distante" (No remote command), utile pour tunnels uniquement. `-f` = arrière-plan. Combo : `ssh -L 8080:dest:80 -Nf host`.

#### Réponse 62 : B
**Explication** : **ssh -X user@host** active le X11 forwarding (X majuscule). Les applications graphiques distantes s'affichent localement. `-x` désactive X11.

#### Réponse 63 : B
**Explication** : **X11Forwarding yes** dans /etc/ssh/sshd_config autorise le serveur à faire du X11 forwarding. Redémarrer sshd après modification.

#### Réponse 64 : B
**Explication** : **gpg --gen-key** génère une paire de clés avec options simplifiées. `gpg --full-generate-key` offre plus d'options (taille clé, expiration, etc.).

#### Réponse 65 : D
**Explication** : **Toutes ces commandes fonctionnent** : `gpg --list-keys`, `gpg --list-public-keys`, `gpg -k`. Pour clés privées : `gpg --list-secret-keys` ou `gpg -K`.

#### Réponse 66 : D
**Explication** : **Les deux syntaxes sont correctes** : `gpg --export --armor` ou `gpg -a --export`. `-a` = `--armor` (format ASCII). Sans `-a`, format binaire.

#### Réponse 67 : D
**Explication** : **Toutes les syntaxes fonctionnent** : ordre des options flexible. `-e` = `--encrypt`, `-r` = `--recipient`. Résultat : message.txt.gpg (binaire) ou .asc (avec `-a`).

#### Réponse 68 : D
**Explication** : **Toutes fonctionnent** : `gpg -d file.gpg` affiche à l'écran, `gpg --decrypt file.gpg` idem, `gpg -o output.txt -d file.gpg` sauvegarde dans fichier.

#### Réponse 69 : D
**Explication** : **Toutes fonctionnent** : `-s` = `--sign`. Résultat : document.txt.gpg (binaire compressé + signé). `--armor` pour ASCII, `--clearsign` pour texte lisible + signature.

#### Réponse 70 : A
**Explication** : **gpg --verify fichier.sig** vérifie la signature. Pour signature détachée : `gpg --verify signature.sig fichier_original`. Affiche "Good signature" si valide.

---

## 🎓 Barème et évaluation

### Score total : /70

- **63-70 points** : Excellente maîtrise ! 🏆
- **56-62 points** : Très bonne compréhension 👏
- **49-55 points** : Bonne base, à consolider 👍
- **42-48 points** : Révision nécessaire 📚
- **< 42 points** : Revoir le sujet en profondeur 🔄

### Points par objectif

- **110.1 (Administration sécurité)** : /25 → Pondération : 25% du sujet
- **110.2 (Configuration sécurité)** : /20 → Pondération : 25% du sujet
- **110.3 (Chiffrement données)** : /25 → Pondération : 50% du sujet

---

## 💡 Exercices pratiques

### Exercice 1 : Lab sécurité complet

**Objectif** : Mettre en pratique tous les concepts de sécurité.

**Scénario** : Vous êtes administrateur système d'une petite entreprise. Sécurisez un nouveau serveur.

```bash
# === Phase 1 : Audit initial ===

# 1. Identifier fichiers SUID/SGID suspects
sudo find / -perm /6000 -type f 2>/dev/null > suid_sgid_audit.txt
# Analyser la liste, vérifier légitimité

# 2. Lister services actifs
systemctl list-units --type service --state running > services_actifs.txt

# 3. Scanner ports ouverts
sudo nmap -sV localhost > ports_ouverts.txt
sudo ss -tulnp > sockets_ecoute.txt

# === Phase 2 : Politique mots de passe ===

# 4. Créer utilisateurs test
sudo useradd -m alice -s /bin/bash
sudo useradd -m bob -s /bin/bash
sudo useradd -m charlie -s /bin/bash

# 5. Configurer politique stricte pour alice
sudo passwd alice
sudo chage -m 1 alice        # Min 1 jour entre changements
sudo chage -M 90 alice       # Validité 90 jours
sudo chage -W 14 alice       # Avertissement 14 jours
sudo chage -I 7 alice        # Inactivité 7 jours

# 6. Bob : forcer changement au login
sudo passwd bob
sudo chage -d 0 bob

# 7. Charlie : compte temporaire (expire dans 30 jours)
sudo passwd charlie
sudo chage -E $(date -d "+30 days" +%Y-%m-%d) charlie

# === Phase 3 : Configuration sudo ===

# 8. Créer groupe admins
sudo groupadd admins
sudo usermod -aG admins alice

# 9. Configurer sudoers
sudo visudo
# Ajouter :
# Cmnd_Alias MONITORING = /usr/bin/systemctl status *, /usr/bin/journalctl
# %admins ALL=(ALL) NOPASSWD: MONITORING
# alice ALL=(ALL) ALL

# === Phase 4 : Sécurisation SSH ===

# 10. Générer clé pour alice
su - alice
ssh-keygen -t ed25519 -C "alice@entreprise.com"

# 11. Configurer serveur SSH (en tant que root)
sudo nano /etc/ssh/sshd_config
# Modifications :
# PermitRootLogin no
# PasswordAuthentication no
# PubkeyAuthentication yes
# X11Forwarding no
# AllowUsers alice bob

sudo systemctl restart sshd

# === Phase 5 : Services et pare-feu ===

# 12. Désactiver services inutiles
sudo systemctl disable --now cups
sudo systemctl disable --now bluetooth

# 13. Configurer TCP wrappers (si supporté)
sudo sh -c 'echo "sshd: ALL" >> /etc/hosts.deny'
sudo sh -c 'echo "sshd: 192.168.1.0/24" >> /etc/hosts.allow'

# === Phase 6 : Surveillance ===

# 14. Configurer surveillance connexions
sudo tail -f /var/log/auth.log | grep "ssh\|sudo"

# 15. Créer script de monitoring quotidien
cat > ~/security_check.sh << 'EOF'
#!/bin/bash
echo "=== Rapport Sécurité $(date) ===" > /tmp/security_report.txt
echo "" >> /tmp/security_report.txt
echo "Connexions récentes :" >> /tmp/security_report.txt
last -n 20 >> /tmp/security_report.txt
echo "" >> /tmp/security_report.txt
echo "Services en écoute :" >> /tmp/security_report.txt
sudo ss -tulnp >> /tmp/security_report.txt
echo "" >> /tmp/security_report.txt
echo "Fichiers SUID modifiés (24h) :" >> /tmp/security_report.txt
sudo find / -perm /4000 -mtime -1 2>/dev/null >> /tmp/security_report.txt
EOF

chmod +x ~/security_check.sh

# === Phase 7 : Tests ===

# 16. Tester connexion SSH avec clé
ssh-copy-id alice@localhost
ssh alice@localhost

# 17. Vérifier politique sudo
sudo systemctl status sshd    # OK sans mot de passe
sudo systemctl stop sshd      # Demande mot de passe

# 18. Tester expiration mots de passe
sudo chage -l alice
sudo chage -l bob
sudo chage -l charlie
```

---

### Exercice 2 : Infrastructure PKI avec GPG

**Objectif** : Créer une mini-PKI d'entreprise avec GPG.

```bash
# === Création des identités ===

# 1. Générer paire de clés pour 3 employés
# Alice (Admin)
gpg --quick-generate-key "Alice Admin <alice@corp.com>" rsa4096

# Bob (Dev)
gpg --quick-generate-key "Bob Developer <bob@corp.com>" rsa4096

# Charlie (Manager)
gpg --quick-generate-key "Charlie Manager <charlie@corp.com>" rsa4096

# 2. Lister toutes les clés
gpg --list-keys
gpg --list-secret-keys

# === Export et distribution ===

# 3. Exporter clés publiques
mkdir ~/gpg_keys
gpg --armor --export alice@corp.com > ~/gpg_keys/alice_pub.asc
gpg --armor --export bob@corp.com > ~/gpg_keys/bob_pub.asc
gpg --armor --export charlie@corp.com > ~/gpg_keys/charlie_pub.asc

# 4. Simuler échange de clés (normalement via email/serveur)
# Alice importe clés de Bob et Charlie
gpg --import ~/gpg_keys/bob_pub.asc
gpg --import ~/gpg_keys/charlie_pub.asc

# Bob importe clés d'Alice et Charlie
gpg --import ~/gpg_keys/alice_pub.asc
gpg --import ~/gpg_keys/charlie_pub.asc

# === Confiance (Web of Trust) ===

# 5. Alice signe les clés de Bob et Charlie
gpg --sign-key bob@corp.com
gpg --sign-key charlie@corp.com

# 6. Définir niveau de confiance
gpg --edit-key bob@corp.com
# gpg> trust
# → 5 (ultimate)
# gpg> save

# === Utilisation pratique ===

# 7. Créer document confidentiel
cat > ~/confidential_report.txt << EOF
CONFIDENTIEL - RAPPORT TRIMESTRIEL
Revenus: 1.5M€
Effectif: 25 employés
Projets en cours: 3
EOF

# 8. Chiffrer pour Bob et Charlie
gpg --armor --encrypt --recipient bob@corp.com \
    --recipient charlie@corp.com confidential_report.txt
# → Crée confidential_report.txt.asc

# 9. Signer document (Alice)
cat > ~/company_policy.txt << EOF
Politique de sécurité de l'entreprise
Version 2.0 - 2026
...
EOF

gpg --clearsign company_policy.txt
# → Crée company_policy.txt.asc (texte + signature)

# 10. Vérifier signature (Bob)
gpg --verify company_policy.txt.asc
# → Good signature from "Alice Admin <alice@corp.com>"

# === Gestion des clés ===

# 11. Générer certificat de révocation (Alice, au cas où)
gpg --output ~/alice_revoke.asc --gen-revoke alice@corp.com
# Stocker en lieu sûr !

# 12. Publier clés sur serveur
gpg --keyserver keyserver.ubuntu.com --send-keys $(gpg --list-keys alice@corp.com | grep pub | awk '{print $2}' | cut -d'/' -f2)

# === Scénario de compromission ===

# 13. Simuler vol de laptop de Bob
# Révoquer clé immédiatement
gpg --import ~/bob_revoke.asc
gpg --keyserver keyserver.ubuntu.com --send-keys BOB_KEY_ID

# 14. Générer nouvelle paire pour Bob
gpg --quick-generate-key "Bob Developer <bob@corp.com>" rsa4096

# === Backup sécurisé ===

# 15. Exporter clés privées (backup chiffré)
gpg --armor --export-secret-keys alice@corp.com > alice_private_BACKUP.asc
# Chiffrer le backup lui-même
gpg --symmetric --armor alice_private_BACKUP.asc
# → Demande phrase de passe pour chiffrement symétrique
# Stocker alice_private_BACKUP.asc.asc en lieu sûr

# === Automatisation ===

# 16. Script pour chiffrement automatique des backups
cat > ~/encrypt_backup.sh << 'EOF'
#!/bin/bash
BACKUP_DIR="/var/backups"
ENCRYPTED_DIR="/var/backups/encrypted"
RECIPIENTS="alice@corp.com bob@corp.com charlie@corp.com"

mkdir -p "$ENCRYPTED_DIR"

for file in "$BACKUP_DIR"/*.tar.gz; do
    if [ -f "$file" ]; then
        basename=$(basename "$file")
        gpg --armor --encrypt \
            $(for r in $RECIPIENTS; do echo "--recipient $r"; done) \
            --output "$ENCRYPTED_DIR/${basename}.asc" \
            "$file"
        echo "Chiffré : $basename"
    fi
done
EOF

chmod +x ~/encrypt_backup.sh
```

---

## 📚 Ressources complémentaires

### Pages de manuel essentielles

```bash
# Permissions et sécurité
man 1 find
man 1 chmod
man 1 passwd
man 1 chage
man 8 usermod
man 5 shadow

# Surveillance réseau
man 8 lsof
man 1 fuser
man 8 netstat
man 8 ss
man 1 nmap

# Limites et utilisateurs
man 1 ulimit
man 5 limits.conf
man 1 last
man 1 who
man 1 w

# Sudo
man 8 sudo
man 5 sudoers
man 8 visudo
man 1 su

# Configuration système
man 8 xinetd
man 5 xinetd.conf
man 5 hosts.allow
man 5 hosts.deny
man 5 nologin

# SSH
man 1 ssh
man 1 ssh-keygen
man 1 ssh-agent
man 1 ssh-add
man 1 ssh-copy-id
man 5 ssh_config
man 5 sshd_config

# GPG
man 1 gpg
man 1 gpg-agent
```

### Fichiers de configuration clés

```bash
# Sécurité système
/etc/passwd
/etc/shadow
/etc/group
/etc/sudoers
/etc/sudoers.d/*
/etc/security/limits.conf
/etc/nologin
/etc/login.defs

# Services
/etc/xinetd.conf
/etc/xinetd.d/*
/etc/hosts.allow
/etc/hosts.deny
/etc/services

# SSH
~/.ssh/config
~/.ssh/id_rsa, ~/.ssh/id_ecdsa, ~/.ssh/id_ed25519
~/.ssh/authorized_keys
~/.ssh/known_hosts
/etc/ssh/sshd_config
/etc/ssh/ssh_host_*_key

# GPG
~/.gnupg/gpg.conf
~/.gnupg/pubring.kbx
~/.gnupg/trustdb.gpg
~/.gnupg/private-keys-v1.d/

# Logs
/var/log/auth.log (Debian)
/var/log/secure (Red Hat)
/var/log/wtmp
```

---

## 🎯 Points clés pour l'examen

### Commandes à connaître par cœur

```bash
# PERMISSIONS SPÉCIALES
find / -perm /6000          # SUID ou SGID
chmod 4755 file             # SUID
chmod 2755 dir              # SGID

# MOTS DE PASSE
passwd -l user              # Verrouiller
chage -l user               # Infos expiration
chage -M 90 user            # Validité 90j
chage -d 0 user             # Forcer changement

# PORTS
lsof -i :PORT
fuser -vn tcp PORT
netstat -tulnp
ss -tulnp
nmap -F host

# SUDO
visudo
sudo -u user cmd

# SSH
ssh-keygen -t ed25519
ssh-copy-id user@host
ssh -L 8080:dest:80 host
ssh -R 8080:dest:80 host

# GPG
gpg --gen-key
gpg -e -r user file
gpg -d file.gpg
gpg -s file
gpg --verify file.sig
```

### Pièges à éviter

❌ Confondre `find -perm 4000` (exact) et `-perm -4000` (+ autres)  
❌ Éditer `/etc/sudoers` sans `visudo`  
❌ Oublier `-` dans `su -`  
❌ Permissions clés SSH incorrectes (600 obligatoire pour privées)  
❌ Confondre tunnel local (`-L`) et distant (`-R`)  
❌ Oublier `--armor` pour GPG ASCII  

---

**Bon courage pour votre préparation ! 🔐**

*La sécurité est un processus, pas un produit. Pratiquez régulièrement !*
