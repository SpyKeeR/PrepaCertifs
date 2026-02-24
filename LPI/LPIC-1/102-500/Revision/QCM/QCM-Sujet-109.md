# 📝 QCM - Sujet 109 : Notions Élémentaires sur les Réseaux

## 🎯 Informations sur le QCM

- **Sujet** : 109 - Notions Élémentaires sur les Réseaux
- **Nombre de questions** : 65
- **Poids du sujet** : 14 points
- **Durée estimée** : 75 minutes

### Répartition des questions

- **109.1** - Protocoles Internet : 20 questions
- **109.2** - Configuration réseau persistante : 20 questions
- **109.3** - Dépannage réseau : 15 questions
- **109.4** - Résolution de noms : 10 questions

---

## 📋 Questions

### 109.1 - Protocoles Internet (20 questions)

#### Question 1
Quelle est la plage d'adresses IP privées pour une classe C ?

- [ ] A) 10.0.0.0 - 10.255.255.255  
- [ ] B) 172.16.0.0 - 172.31.255.255  
- [ ] C) 192.168.0.0 - 192.168.255.255  
- [ ] D) 127.0.0.0 - 127.255.255.255  

#### Question 2
Combien de bits contient une adresse IPv4 ?

- [ ] A) 16 bits  
- [ ] B) 32 bits  
- [ ] C) 64 bits  
- [ ] D) 128 bits  

#### Question 3
Quel masque de sous-réseau correspond à la notation CIDR /24 ?

- [ ] A) 255.0.0.0  
- [ ] B) 255.255.0.0  
- [ ] C) 255.255.255.0  
- [ ] D) 255.255.255.128  

#### Question 4
Combien d'adresses IP sont utilisables dans un réseau /26 ?

- [ ] A) 30  
- [ ] B) 62  
- [ ] C) 126  
- [ ] D) 254  

#### Question 5
Quel port TCP est utilisé par défaut pour le service SSH ?

- [ ] A) 21  
- [ ] B) 22  
- [ ] C) 23  
- [ ] D) 25  

#### Question 6
Quel protocole de transport garantit la livraison ordonnée des paquets ?

- [ ] A) UDP  
- [ ] B) ICMP  
- [ ] C) TCP  
- [ ] D) IP  

#### Question 7
Sur quel port UDP le service NTP fonctionne-t-il par défaut ?

- [ ] A) 53  
- [ ] B) 123  
- [ ] C) 161  
- [ ] D) 514  

#### Question 8
Quelle commande permet de consulter la liste des ports standards sur un système Linux ?

- [ ] A) `more /etc/ports`  
- [ ] B) `cat /etc/services`  
- [ ] C) `less /var/log/ports`  
- [ ] D) `view /etc/protocols`  

#### Question 9
Combien de bits contient une adresse IPv6 ?

- [ ] A) 32 bits  
- [ ] B) 64 bits  
- [ ] C) 128 bits  
- [ ] D) 256 bits  

#### Question 10
Comment écrit-on l'adresse IPv6 `2001:0db8:0000:0000:0000:0000:0000:0001` de manière abrégée ?

- [ ] A) `2001:db8:0:0:0:0:0:1`  
- [ ] B) `2001:db8::1`  
- [ ] C) `2001:0db8::1`  
- [ ] D) Les réponses B et C sont correctes  

#### Question 11
Quelle est l'adresse de loopback en IPv6 ?

- [ ] A) `127.0.0.1`  
- [ ] B) `::1`  
- [ ] C) `fe80::1`  
- [ ] D) `ff02::1`  

#### Question 12
Quel type d'adresse IPv6 remplace le broadcast IPv4 ?

- [ ] A) Unicast  
- [ ] B) Anycast  
- [ ] C) Multicast  
- [ ] D) Broadcast  

#### Question 13
Quelle adresse IPv6 envoie un paquet à tous les hôtes du réseau local ?

- [ ] A) `::1`  
- [ ] B) `fe80::1`  
- [ ] C) `ff02::1`  
- [ ] D) `2001:db8::1`  

#### Question 14
Quelle est la différence principale entre TCP et UDP ?

- [ ] A) TCP est plus rapide que UDP  
- [ ] B) TCP garantit la livraison, UDP non  
- [ ] C) UDP utilise des ports, TCP non  
- [ ] D) TCP est pour IPv4, UDP pour IPv6  

#### Question 15
Quel protocole utilise la commande `ping` ?

- [ ] A) TCP  
- [ ] B) UDP  
- [ ] C) ICMP  
- [ ] D) ARP  

#### Question 16
Quel port utilise le protocole HTTPS ?

- [ ] A) 80  
- [ ] B) 443  
- [ ] C) 8080  
- [ ] D) 8443  

#### Question 17
Dans le réseau 192.168.10.0/24, quelle est l'adresse de broadcast ?

- [ ] A) 192.168.10.0  
- [ ] B) 192.168.10.1  
- [ ] C) 192.168.10.254  
- [ ] D) 192.168.10.255  

#### Question 18
Combien de serveurs DNS maximum peut-on spécifier dans `/etc/resolv.conf` ?

- [ ] A) 1  
- [ ] B) 2  
- [ ] C) 3  
- [ ] D) Illimité  

#### Question 19
Quelle plage de ports est réservée aux services privilégiés nécessitant les droits root ?

- [ ] A) 1-1023  
- [ ] B) 1024-49151  
- [ ] C) 49152-65535  
- [ ] D) 1-65535  

#### Question 20
Pour le réseau 172.16.30.230/27, quelle est l'adresse réseau ?

- [ ] A) 172.16.30.0  
- [ ] B) 172.16.30.192  
- [ ] C) 172.16.30.224  
- [ ] D) 172.16.30.230  

---

### 109.2 - Configuration réseau persistante (20 questions)

#### Question 21
Quelle commande moderne affiche toutes les interfaces réseau ?

- [ ] A) `ifconfig -a`  
- [ ] B) `ip link show`  
- [ ] C) `netstat -i`  
- [ ] D) `route -n`  

#### Question 22
Quel préfixe indique une interface Ethernet selon la convention de nommage moderne ?

- [ ] A) `eth`  
- [ ] B) `en`  
- [ ] C) `wl`  
- [ ] D) `lo`  

#### Question 23
Comment activer l'interface `enp3s5` avec la commande moderne ?

- [ ] A) `ifconfig enp3s5 up`  
- [ ] B) `ip link set dev enp3s5 up`  
- [ ] C) `ifup enp3s5`  
- [ ] D) Les réponses B et C sont correctes  

#### Question 24
Quelle commande configure l'adresse IP 192.168.1.100/24 sur l'interface enp0s8 ?

- [ ] A) `ip addr add 192.168.1.100/24 dev enp0s8`  
- [ ] B) `ip address add 192.168.1.100/24 enp0s8`  
- [ ] C) `ifconfig enp0s8 192.168.1.100/24`  
- [ ] D) Les réponses A et C sont correctes  

#### Question 25
Dans quel fichier configure-t-on les interfaces réseau de manière persistante sur Debian ?

- [ ] A) `/etc/network/config`  
- [ ] B) `/etc/network/interfaces`  
- [ ] C) `/etc/sysconfig/network-scripts/ifcfg-eth0`  
- [ ] D) `/etc/netplan/01-netcfg.yaml`  

#### Question 26
Quelle directive dans `/etc/network/interfaces` active une interface au démarrage ?

- [ ] A) `start`  
- [ ] B) `auto`  
- [ ] C) `enable`  
- [ ] D) `boot`  

#### Question 27
Comment définir le nom d'hôte statique à "webserver" avec `hostnamectl` ?

- [ ] A) `hostnamectl set-hostname webserver`  
- [ ] B) `hostnamectl --static set-hostname webserver`  
- [ ] C) Les deux commandes A et B fonctionnent  
- [ ] D) `hostnamectl hostname webserver`  

#### Question 28
Dans quel fichier est stocké le nom d'hôte statique ?

- [ ] A) `/etc/hostname`  
- [ ] B) `/etc/hosts`  
- [ ] C) `/etc/sysconfig/network`  
- [ ] D) `/etc/hostnamectl.conf`  

#### Question 29
Quelle commande NetworkManager liste les réseaux Wi-Fi disponibles ?

- [ ] A) `nmcli wifi list`  
- [ ] B) `nmcli device wifi list`  
- [ ] C) `nmcli connection show`  
- [ ] D) `nmcli radio wifi`  

#### Question 30
Comment se connecter au réseau Wi-Fi "MonWiFi" avec le mot de passe "Secret123" via nmcli ?

- [ ] A) `nmcli wifi connect MonWiFi password Secret123`  
- [ ] B) `nmcli device wifi connect MonWiFi password Secret123`  
- [ ] C) `nmcli connection add wifi MonWiFi password Secret123`  
- [ ] D) `nmcli radio wifi connect MonWiFi Secret123`  

#### Question 31
Comment désactiver le Wi-Fi avec NetworkManager ?

- [ ] A) `nmcli wifi off`  
- [ ] B) `nmcli radio wifi off`  
- [ ] C) `nmcli device wifi off`  
- [ ] D) `nmcli connection wifi off`  

#### Question 32
Dans quel répertoire place-t-on les fichiers de configuration réseau pour systemd-networkd ?

- [ ] A) `/etc/network/`  
- [ ] B) `/etc/systemd/network/`  
- [ ] C) `/lib/systemd/network/`  
- [ ] D) Les réponses B et C sont correctes (B prioritaire)  

#### Question 33
Quel suffixe de fichier est utilisé pour configurer les adresses IP avec systemd-networkd ?

- [ ] A) `.link`  
- [ ] B) `.netdev`  
- [ ] C) `.network`  
- [ ] D) `.conf`  

#### Question 34
Dans un fichier `.network` systemd-networkd, quelle section contient le nom de l'interface ?

- [ ] A) `[Network]`  
- [ ] B) `[Match]`  
- [ ] C) `[Link]`  
- [ ] D) `[Interface]`  

#### Question 35
Comment configurer DHCP IPv4 uniquement dans un fichier `.network` systemd-networkd ?

- [ ] A) `DHCP=yes`  
- [ ] B) `DHCP=ipv4`  
- [ ] C) `DHCP=on`  
- [ ] D) `DHCPv4=true`  

#### Question 36
Quel fichier contient les associations statiques entre noms d'hôtes et adresses IP ?

- [ ] A) `/etc/hostname`  
- [ ] B) `/etc/hosts`  
- [ ] C) `/etc/resolv.conf`  
- [ ] D) `/etc/nsswitch.conf`  

#### Question 37
Dans `/etc/hosts`, quelle est la syntaxe correcte pour associer 10.0.0.1 au nom "gateway" ?

- [ ] A) `gateway 10.0.0.1`  
- [ ] B) `10.0.0.1 gateway`  
- [ ] C) `gateway=10.0.0.1`  
- [ ] D) `10.0.0.1:gateway`  

#### Question 38
Quelle directive dans `/etc/resolv.conf` spécifie un serveur DNS ?

- [ ] A) `dns`  
- [ ] B) `server`  
- [ ] C) `nameserver`  
- [ ] D) `resolver`  

#### Question 39
Quelle option dans `/etc/resolv.conf` permet d'ajouter automatiquement un domaine aux noms courts ?

- [ ] A) `domain`  
- [ ] B) `search`  
- [ ] C) Les deux A et B  
- [ ] D) `suffix`  

#### Question 40
Comment modifier le MTU de l'interface enp0s3 à 9000 avec la commande `ip` ?

- [ ] A) `ip link set enp0s3 mtu 9000`  
- [ ] B) `ip addr set enp0s3 mtu 9000`  
- [ ] C) `ip mtu set enp0s3 9000`  
- [ ] D) `ifconfig enp0s3 mtu 9000`  

---

### 109.3 - Dépannage réseau (15 questions)

#### Question 41
Quelle commande affiche la table de routage IPv4 avec la méthode moderne ?

- [ ] A) `route`  
- [ ] B) `netstat -r`  
- [ ] C) `ip route`  
- [ ] D) Toutes les réponses ci-dessus  

#### Question 42
Comment ajouter une route par défaut vers 192.168.1.1 avec `ip` ?

- [ ] A) `ip route add default via 192.168.1.1`  
- [ ] B) `ip route add 0.0.0.0/0 via 192.168.1.1`  
- [ ] C) Les deux commandes A et B fonctionnent  
- [ ] D) `ip route default 192.168.1.1`  

#### Question 43
Quelle commande envoie 5 paquets ICMP à google.com ?

- [ ] A) `ping google.com -c 5`  
- [ ] B) `ping -c 5 google.com`  
- [ ] C) `ping -n 5 google.com`  
- [ ] D) Les réponses A et B sont correctes  

#### Question 44
Quelle commande trace le chemin réseau vers une destination en affichant les MTU ?

- [ ] A) `traceroute --mtu destination`  
- [ ] B) `tracepath destination`  
- [ ] C) `ping -M do destination`  
- [ ] D) `mtr destination`  

#### Question 45
Quelle option de `traceroute` force l'utilisation d'ICMP au lieu d'UDP (nécessite root) ?

- [ ] A) `-i`  
- [ ] B) `-I`  
- [ ] C) `-T`  
- [ ] D) `-U`  

#### Question 46
Quelle commande affiche tous les ports TCP en écoute avec les numéros (pas de résolution DNS) ?

- [ ] A) `ss -tln`  
- [ ] B) `netstat -tln`  
- [ ] C) Les deux réponses A et B  
- [ ] D) `lsof -i tcp -n`  

#### Question 47
Avec `netcat`, comment créer un listener TCP sur le port 1234 ?

- [ ] A) `nc -l 1234`  
- [ ] B) `nc listen 1234`  
- [ ] C) `nc -p 1234`  
- [ ] D) `nc --listen 1234`  

#### Question 48
Quelle commande `lsof` affiche tous les processus utilisant le port 80 ?

- [ ] A) `lsof -i :80`  
- [ ] B) `lsof -p 80`  
- [ ] C) `lsof tcp:80`  
- [ ] D) `lsof --port 80`  

#### Question 49
Comment utiliser `fuser` pour identifier les processus utilisant le port TCP 22 ?

- [ ] A) `fuser 22/tcp`  
- [ ] B) `fuser -n tcp 22`  
- [ ] C) `fuser -vn tcp 22`  
- [ ] D) Les réponses B et C sont correctes  

#### Question 50
Quelle commande `nmap` effectue un scan rapide des 100 ports les plus courants ?

- [ ] A) `nmap -f localhost`  
- [ ] B) `nmap -F localhost`  
- [ ] C) `nmap --fast localhost`  
- [ ] D) `nmap -quick localhost`  

#### Question 51
Comment scanner les ports 22, 80 et 443 sur l'hôte 192.168.1.10 avec nmap ?

- [ ] A) `nmap -p 22,80,443 192.168.1.10`  
- [ ] B) `nmap -p ssh,http,https 192.168.1.10`  
- [ ] C) Les deux réponses A et B fonctionnent  
- [ ] D) `nmap --ports 22,80,443 192.168.1.10`  

#### Question 52
Quelle commande affiche les connexions réseau établies (sans les listeners) ?

- [ ] A) `ss -t`  
- [ ] B) `ss -ta`  
- [ ] C) `ss -tl`  
- [ ] D) `netstat -tan`  

#### Question 53
Dans le résultat de `ss`, que signifie l'état "ESTAB" ?

- [ ] A) La connexion est en cours d'établissement  
- [ ] B) La connexion est établie  
- [ ] C) La connexion est terminée  
- [ ] D) La connexion est en attente  

#### Question 54
Quelle commande teste si le port 80 est ouvert sur example.com avec netcat ?

- [ ] A) `nc -vz example.com 80`  
- [ ] B) `nc -t example.com 80`  
- [ ] C) `nc --test example.com 80`  
- [ ] D) `nc -p 80 example.com`  

#### Question 55
Comment forcer `ping` à utiliser IPv6 pour tester localhost ?

- [ ] A) `ping -6 localhost`  
- [ ] B) `ping6 localhost`  
- [ ] C) `ping ::1`  
- [ ] D) Les réponses B et C sont correctes  

---

### 109.4 - Résolution de noms (10 questions)

#### Question 56
Quel fichier définit l'ordre de résolution des noms d'hôtes ?

- [ ] A) `/etc/hosts`  
- [ ] B) `/etc/resolv.conf`  
- [ ] C) `/etc/nsswitch.conf`  
- [ ] D) `/etc/hostname`  

#### Question 57
Quelle ligne dans `/etc/nsswitch.conf` consulte d'abord `/etc/hosts` puis DNS ?

- [ ] A) `hosts: dns files`  
- [ ] B) `hosts: files dns`  
- [ ] C) `hosts: local dns`  
- [ ] D) `hosts: files resolve`  

#### Question 58
Quelle commande utilise les bibliothèques système pour résoudre "learning.lpi.org" ?

- [ ] A) `host learning.lpi.org`  
- [ ] B) `dig learning.lpi.org`  
- [ ] C) `getent hosts learning.lpi.org`  
- [ ] D) `nslookup learning.lpi.org`  

#### Question 59
Comment forcer `getent` à utiliser uniquement le fichier `/etc/hosts` ?

- [ ] A) `getent -s files hosts learning.lpi.org`  
- [ ] B) `getent --source=files hosts learning.lpi.org`  
- [ ] C) `getent hosts -f learning.lpi.org`  
- [ ] D) `getent --files hosts learning.lpi.org`  

#### Question 60
Quelle commande DNS affiche uniquement l'adresse IP de lpi.org (format court) ?

- [ ] A) `host lpi.org`  
- [ ] B) `dig lpi.org`  
- [ ] C) `dig +short lpi.org`  
- [ ] D) `host -s lpi.org`  

#### Question 61
Comment interroger les enregistrements MX de lpi.org avec `host` ?

- [ ] A) `host lpi.org mx`  
- [ ] B) `host -t MX lpi.org`  
- [ ] C) `host --type=MX lpi.org`  
- [ ] D) Les réponses B et C sont correctes  

#### Question 62
Quelle commande `dig` interroge le serveur DNS 8.8.8.8 pour résoudre example.com ?

- [ ] A) `dig @8.8.8.8 example.com`  
- [ ] B) `dig -s 8.8.8.8 example.com`  
- [ ] C) `dig --server 8.8.8.8 example.com`  
- [ ] D) `dig example.com @8.8.8.8`  

#### Question 63
Quel type d'enregistrement DNS permet la résolution inverse (IP vers nom) ?

- [ ] A) A  
- [ ] B) AAAA  
- [ ] C) PTR  
- [ ] D) CNAME  

#### Question 64
Dans `/etc/nsswitch.conf`, que signifie `hosts: files [!UNAVAIL=return] dns` ?

- [ ] A) Si files échoue, utiliser DNS  
- [ ] B) Si files n'est pas indisponible, ne pas essayer DNS  
- [ ] C) Toujours utiliser files puis DNS  
- [ ] D) Si DNS échoue, utiliser files  

#### Question 65
Quel service systemd fournit la résolution DNS locale sur 127.0.0.53 ?

- [ ] A) systemd-networkd  
- [ ] B) systemd-resolved  
- [ ] C) systemd-dns  
- [ ] D) systemd-hostnamed  

---

## ✅ Réponses et explications

### 109.1 - Protocoles Internet

#### Réponse 1 : C
**Explication** : La plage IP privée de classe C est **192.168.0.0 - 192.168.255.255**. La classe A est 10.0.0.0/8, la classe B est 172.16.0.0/12. 127.0.0.0/8 est réservé pour le loopback.

#### Réponse 2 : B
**Explication** : Une adresse IPv4 contient **32 bits** divisés en 4 octets (4 × 8 bits). Exemple : 192.168.1.1 = 11000000.10101000.00000001.00000001. IPv6 utilise 128 bits.

#### Réponse 3 : C
**Explication** : /24 signifie 24 bits à 1 pour la partie réseau : **255.255.255.0** = 11111111.11111111.11111111.00000000. Cela laisse 8 bits (256 adresses) pour les hôtes.

#### Réponse 4 : B
**Explication** : /26 = 26 bits réseau, donc 6 bits hôtes (2^6 = 64 adresses). On soustrait 2 (réseau + broadcast) : **64 - 2 = 62 adresses utilisables**.

#### Réponse 5 : B
**Explication** : SSH (Secure Shell) utilise le port TCP **22**. Port 21 = FTP, 23 = Telnet, 25 = SMTP.

#### Réponse 6 : C
**Explication** : **TCP** (Transmission Control Protocol) garantit la livraison fiable et ordonnée des paquets avec contrôle d'erreurs et retransmission. UDP est sans connexion et ne garantit rien.

#### Réponse 7 : B
**Explication** : NTP (Network Time Protocol) utilise le port UDP **123**. Port 53 = DNS, 161 = SNMP, 514 = Syslog.

#### Réponse 8 : B
**Explication** : Le fichier **/etc/services** contient la liste des ports standards et services associés. Format : `service port/protocole # commentaire`.

#### Réponse 9 : C
**Explication** : Une adresse IPv6 contient **128 bits** divisés en 8 groupes de 16 bits (notation hexadécimale). C'est 4 fois plus qu'IPv4 (32 bits).

#### Réponse 10 : D
**Explication** : On peut omettre les zéros de tête : `2001:db8::1`. Les deux notations **B et C sont correctes**. L'omission des groupes de zéros avec `::` ne peut être faite qu'une seule fois.

#### Réponse 11 : B
**Explication** : L'adresse de loopback IPv6 est **::1** (équivalent de 127.0.0.1 en IPv4). fe80::/10 = link-local, ff02::1 = multicast tous hôtes.

#### Réponse 12 : C
**Explication** : IPv6 utilise **multicast** au lieu du broadcast. Par exemple, ff02::1 envoie à tous les hôtes du lien local (équivalent du broadcast).

#### Réponse 13 : C
**Explication** : **ff02::1** est l'adresse multicast qui atteint tous les hôtes du réseau local (all-nodes). ::1 = loopback, fe80::1 = link-local.

#### Réponse 14 : B
**Explication** : **TCP garantit la livraison fiable** des paquets (contrôle, ordre, retransmission), UDP non. TCP est plus lent mais fiable, UDP est rapide mais non fiable.

#### Réponse 15 : C
**Explication** : `ping` utilise le protocole **ICMP** (Internet Control Message Protocol) pour envoyer des requêtes echo et recevoir des réponses echo.

#### Réponse 16 : B
**Explication** : HTTPS (HTTP Secure) utilise le port TCP **443**. Port 80 = HTTP non chiffré, 8080 et 8443 sont des ports alternatifs non standards.

#### Réponse 17 : D
**Explication** : Dans un réseau /24, la dernière adresse est le broadcast : **192.168.10.255**. L'adresse réseau est .0, les hôtes vont de .1 à .254.

#### Réponse 18 : C
**Explication** : On peut spécifier jusqu'à **3 serveurs DNS** avec `nameserver` dans `/etc/resolv.conf`. Les serveurs suivants servent de secours.

#### Réponse 19 : A
**Explication** : Les ports **1-1023** sont privilégiés et nécessitent root. Les ports 1024-49151 sont enregistrés, 49152-65535 sont dynamiques/privés.

#### Réponse 20 : C
**Explication** : /27 = 27 bits réseau. 
```
172.16.30.230 = 10101100.00010000.00011110.11100110
Masque /27    = 11111111.11111111.11111111.11100000
Réseau        = 10101100.00010000.00011110.11100000 = 172.16.30.224
```

### 109.2 - Configuration réseau persistante

#### Réponse 21 : B
**Explication** : La commande moderne est **ip link show** (ou `ip link`). `ifconfig -a` est obsolète mais fonctionne encore. `netstat -i` affiche les statistiques.

#### Réponse 22 : B
**Explication** : Le préfixe **en** indique une interface Ethernet (enp3s5, eno1, etc.). wl = WLAN (Wi-Fi), ww = WWAN (cellulaire), lo = loopback.

#### Réponse 23 : D
**Explication** : **Les deux commandes fonctionnent** : `ip link set dev enp3s5 up` (moderne) et `ifup enp3s5` (utilise /etc/network/interfaces). `ifconfig enp3s5 up` est obsolète.

#### Réponse 24 : D
**Explication** : **Les deux syntaxes fonctionnent** : `ip addr add 192.168.1.100/24 dev enp0s8` (moderne) et `ifconfig enp0s8 192.168.1.100/24` (obsolète).

#### Réponse 25 : B
**Explication** : Sur Debian/Ubuntu, c'est **/etc/network/interfaces**. Red Hat utilise /etc/sysconfig/network-scripts/. Ubuntu moderne peut utiliser Netplan.

#### Réponse 26 : B
**Explication** : La directive **auto** active l'interface au démarrage. Exemple : `auto enp3s5` suivi de `iface enp3s5 inet dhcp`.

#### Réponse 27 : C
**Explication** : **Les deux commandes fonctionnent**. Sans option, `hostnamectl set-hostname` définit tous les types de noms (statique, pretty, transitoire). Avec `--static`, uniquement le nom statique.

#### Réponse 28 : A
**Explication** : Le nom d'hôte statique est stocké dans **/etc/hostname**. `/etc/hosts` contient les associations IP-noms. `/etc/sysconfig/network` existe sur Red Hat.

#### Réponse 29 : B
**Explication** : **nmcli device wifi list** liste les réseaux Wi-Fi disponibles. `nmcli connection show` liste les connexions configurées, pas les réseaux scannés.

#### Réponse 30 : B
**Explication** : La syntaxe correcte est **nmcli device wifi connect MonWiFi password Secret123**. On peut ajouter `hidden yes` pour les SSID cachés.

#### Réponse 31 : B
**Explication** : **nmcli radio wifi off** désactive la radio Wi-Fi (économie d'énergie). `nmcli radio wifi on` pour réactiver. L'objet est `radio`, pas `device` ou `connection`.

#### Réponse 32 : D
**Explication** : Les fichiers vont dans `/etc/systemd/network/` (priorité haute) ou `/lib/systemd/network/` (priorité basse). **Les deux sont corrects mais /etc/ est prioritaire** pour les personnalisations.

#### Réponse 33 : C
**Explication** : Les fichiers **.network** configurent les adresses IP et routes. `.netdev` = périphériques virtuels, `.link` = configuration bas niveau.

#### Réponse 34 : B
**Explication** : La section **[Match]** identifie l'interface (par nom, MAC, etc.). La section [Network] contient la configuration IP. Exemple : `[Match]` puis `Name=enp3s5`.

#### Réponse 35 : B
**Explication** : **DHCP=ipv4** active DHCP pour IPv4 uniquement. `DHCP=yes` = IPv4+IPv6, `DHCP=ipv6` = IPv6 uniquement, `DHCP=no` = désactivé.

#### Réponse 36 : B
**Explication** : **/etc/hosts** contient les associations IP-noms statiques. Format : `IP nom_complet alias`. `/etc/hostname` = nom local, `/etc/resolv.conf` = DNS.

#### Réponse 37 : B
**Explication** : La syntaxe correcte est **10.0.0.1 gateway** (IP en premier, puis noms). On peut ajouter des alias : `10.0.0.1 gateway.lpi.org gateway gw`.

#### Réponse 38 : C
**Explication** : **nameserver** spécifie un serveur DNS. Exemple : `nameserver 8.8.8.8`. Maximum 3 serveurs.

#### Réponse 39 : C
**Explication** : **Les deux fonctionnent** : `domain` définit le domaine local, `search` une liste de domaines de recherche. Ils sont mutuellement exclusifs ; le dernier défini gagne.

#### Réponse 40 : A
**Explication** : **ip link set enp0s3 mtu 9000** modifie le MTU. `ip link` gère les paramètres de niveau 2 (MAC, MTU, etc.). `ifconfig enp0s3 mtu 9000` fonctionne aussi (obsolète).

### 109.3 - Dépannage réseau

#### Réponse 41 : C
**Explication** : **Toutes les commandes fonctionnent** : `ip route` (moderne), `route` et `netstat -r` (obsolètes). Mais la plus moderne est `ip route`.

#### Réponse 42 : C
**Explication** : **Les deux syntaxes sont équivalentes** : `default` est un alias pour `0.0.0.0/0`. Syntaxe complète : `ip route add 0.0.0.0/0 via 192.168.1.1`.

#### Réponse 43 : B
**Explication** : La syntaxe correcte est **ping -c 5 google.com** (`-c` pour count). L'option `-n` est pour la résolution numérique sous certains `ping`.

#### Réponse 44 : B
**Explication** : **tracepath** trace le chemin ET affiche les MTU de chaque lien. `traceroute --mtu` n'existe pas (mais `traceroute -I --mtu` avec root).

#### Réponse 45 : B
**Explication** : **-I** (i majuscule) force ICMP echo au lieu d'UDP. `-T` = TCP, `-U` = UDP explicite, `-i` = spécifier interface. Nécessite root.

#### Réponse 46 : C
**Explication** : **Les deux commandes sont équivalentes** : `ss -tln` (moderne) et `netstat -tln` (obsolète). `-t` = TCP, `-l` = listening, `-n` = numérique.

#### Réponse 47 : A
**Explication** : **nc -l 1234** crée un listener. `-l` = listen mode. Pour UDP : `nc -u -l 1234`. Le port est en argument après `-l`.

#### Réponse 48 : A
**Explication** : **lsof -i :80** affiche tous les processus utilisant le port 80. `-i` = fichiers Internet, `:80` = port 80. `-p` est pour process ID.

#### Réponse 49 : D
**Explication** : **Les deux fonctionnent** : `fuser -n tcp 22` (minimal) et `fuser -vn tcp 22` (verbose avec détails). `-n` = namespace réseau, `-v` = verbose.

#### Réponse 50 : B
**Explication** : **nmap -F** (Fast scan) scanne les 100 ports les plus courants au lieu des 1000 par défaut. C'est plus rapide pour un scan de découverte.

#### Réponse 51 : C
**Explication** : **Les deux syntaxes fonctionnent** : numéros de ports (`-p 22,80,443`) ou noms de services (`-p ssh,http,https`). nmap résout les noms via /etc/services.

#### Réponse 52 : A
**Explication** : **ss -t** affiche uniquement les connexions TCP établies (sans listeners). `-ta` = tous états, `-tl` = listeners uniquement. `netstat -tan` inclut aussi les listeners.

#### Réponse 53 : B
**Explication** : **ESTAB** (ou ESTABLISHED) signifie que la connexion TCP est **établie et active**. Autres états : LISTEN, SYN-SENT, CLOSE-WAIT, TIME-WAIT.

#### Réponse 54 : A
**Explication** : **nc -vz example.com 80** teste la connexion sans envoyer de données. `-v` = verbose, `-z` = zero-I/O mode (scan uniquement).

#### Réponse 55 : D
**Explication** : **Les deux fonctionnent** : `ping6 localhost` (commande spécifique IPv6) ou `ping ::1` (adresse IPv6 explicite). `-6` n'existe pas avec `ping` standard.

### 109.4 - Résolution de noms

#### Réponse 56 : C
**Explication** : **/etc/nsswitch.conf** (Name Service Switch) définit l'ordre de résolution. Exemple : `hosts: files dns` consulte d'abord /etc/hosts puis DNS.

#### Réponse 57 : B
**Explication** : **hosts: files dns** consulte d'abord `/etc/hosts` (files) puis le DNS. L'ordre est important : de gauche à droite.

#### Réponse 58 : C
**Explication** : **getent hosts** utilise les bibliothèques NSS du système et respecte /etc/nsswitch.conf. `host` et `dig` interrogent directement le DNS.

#### Réponse 59 : A
**Explication** : **getent -s files hosts learning.lpi.org** force l'utilisation de la source `files` (/etc/hosts). `-s` = source (nécessite glibc >= 2.2.5).

#### Réponse 60 : C
**Explication** : **dig +short lpi.org** affiche uniquement la réponse (adresse IP), sans toutes les informations détaillées. Très utile dans les scripts.

#### Réponse 61 : D
**Explication** : **Les deux syntaxes fonctionnent** : `host -t MX lpi.org` (court) et `host --type=MX lpi.org` (long). Types : A, AAAA, MX, NS, SOA, PTR, CNAME.

#### Réponse 62 : A
**Explication** : **dig @8.8.8.8 example.com** interroge le serveur DNS 8.8.8.8. Le `@` précède toujours le serveur DNS. Utile pour tester des serveurs spécifiques.

#### Réponse 63 : C
**Explication** : **PTR** (Pointer) permet la résolution inverse (IP → nom). Exemple : `host 8.8.8.8` utilise PTR. A/AAAA = direct (nom → IP).

#### Réponse 64 : B
**Explication** : `[!UNAVAIL=return]` signifie : **si la source n'est PAS indisponible, ne pas continuer**. Donc si files est disponible (même si pas trouvé), on arrête sans essayer DNS.

#### Réponse 65 : B
**Explication** : **systemd-resolved** fournit DNS local sur 127.0.0.53. Il interroge les serveurs DNS configurés et fournit aussi mDNS et LLMNR.

---

## 🎓 Barème et évaluation

### Score total : /65

- **58-65 points** : Excellente maîtrise ! 🏆
- **52-57 points** : Très bonne compréhension 👏
- **45-51 points** : Bonne base, à consolider 👍
- **39-44 points** : Révision nécessaire 📚
- **< 39 points** : Revoir le sujet en profondeur 🔄

### Points par objectif

- **109.1 (Protocoles Internet)** : /20 → Pondération : 29% du sujet
- **109.2 (Configuration réseau)** : /20 → Pondération : 29% du sujet
- **109.3 (Dépannage réseau)** : /15 → Pondération : 29% du sujet
- **109.4 (Résolution de noms)** : /10 → Pondération : 14% du sujet

---

## 💡 Exercices pratiques

### Exercice 1 : Configuration réseau complète

**Objectif** : Configurer une interface de A à Z.

**Scénario** : Configurer `enp0s8` avec :
- IP statique : 10.0.50.100/24
- Passerelle : 10.0.50.1
- DNS : 1.1.1.1 et 1.0.0.1
- Nom d'hôte : lab-server

**Solution temporaire (ip + echo)** :
```bash
# 1. Configurer IP
sudo ip addr add 10.0.50.100/24 dev enp0s8
sudo ip link set enp0s8 up

# 2. Ajouter route par défaut
sudo ip route add default via 10.0.50.1

# 3. Configurer DNS
sudo bash -c 'cat > /etc/resolv.conf << EOF
nameserver 1.1.1.1
nameserver 1.0.0.1
search lab.local
EOF'

# 4. Définir nom d'hôte
sudo hostnamectl set-hostname lab-server

# 5. Vérifier
ip addr show dev enp0s8
ip route
cat /etc/resolv.conf
hostnamectl
```

**Solution persistante (/etc/network/interfaces)** :
```bash
sudo nano /etc/network/interfaces

# Ajouter :
auto enp0s8
iface enp0s8 inet static
    address 10.0.50.100/24
    gateway 10.0.50.1
    dns-nameservers 1.1.1.1 1.0.0.1
    dns-search lab.local

# Appliquer
sudo ifdown enp0s8 && sudo ifup enp0s8
```

**Solution systemd-networkd** :
```bash
# 1. Créer fichier .network
sudo nano /etc/systemd/network/20-wired.network

[Match]
Name=enp0s8

[Network]
Address=10.0.50.100/24
Gateway=10.0.50.1
DNS=1.1.1.1
DNS=1.0.0.1

# 2. Redémarrer service
sudo systemctl enable systemd-networkd
sudo systemctl restart systemd-networkd

# 3. Configurer nom d'hôte
sudo hostnamectl set-hostname lab-server
```

---

### Exercice 2 : Diagnostic réseau méthodique

**Objectif** : Diagnostiquer un problème de connexion à google.com.

**Méthodologie en 7 étapes** :

```bash
# Étape 1 : Vérifier interface locale
ip addr show
# Vérifier : interface UP ? IP configurée ?

# Étape 2 : Tester pile TCP/IP
ping -c 3 127.0.0.1
# Si échec : problème système grave

# Étape 3 : Tester réseau local
ip route                    # Trouver gateway
ping -c 3 <GATEWAY_IP>      # Ex: 192.168.1.1
# Si échec : problème réseau local (câble, switch)

# Étape 4 : Tester route Internet
ping -c 3 8.8.8.8           # Google DNS
# Si échec : problème routage ou FAI

# Étape 5 : Tester résolution DNS
cat /etc/resolv.conf        # Serveur DNS configuré ?
host google.com
dig google.com
# Si échec : problème DNS

# Étape 6 : Tester connectivité finale
ping -c 3 google.com
traceroute google.com
# Identifier où le blocage se produit

# Étape 7 : Tester service applicatif
nc -vz google.com 80
curl -I http://google.com
# Vérifier que le service HTTP répond
```

**Problèmes courants et solutions** :

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Interface DOWN | Interface désactivée | `sudo ip link set dev enp0s8 up` |
| Pas d'IP | DHCP échoue ou config statique manquante | Vérifier DHCP client ou configurer statique |
| Gateway inaccessible | Problème réseau local | Vérifier câble, switch, routeur |
| DNS ne résout pas | Mauvais serveur DNS | Modifier `/etc/resolv.conf` |
| Ping bloqué mais service OK | ICMP filtré | Normal, utiliser tests applicatifs |

---

### Exercice 3 : Calculs de sous-réseaux

**Objectif** : Maîtriser les calculs IPv4.

**Exercice A** : Réseau 192.168.100.0/25

**Questions** :
1. Masque de sous-réseau ?
2. Nombre d'hôtes utilisables ?
3. Plage d'IP utilisables ?
4. Adresse de broadcast ?

**Réponses** :
```
/25 = 25 bits réseau, 7 bits hôtes

1. Masque : 255.255.255.128
   (11111111.11111111.11111111.10000000)

2. Hôtes : 2^7 - 2 = 128 - 2 = 126

3. Plage utilisable : 192.168.100.1 - 192.168.100.126

4. Broadcast : 192.168.100.127
   (dernière adresse de la plage)
```

**Exercice B** : IP 10.50.75.130/22

**Questions** :
1. Adresse réseau ?
2. Adresse de broadcast ?
3. Combien d'hôtes ?

**Calcul détaillé** :
```
/22 = 22 bits réseau, 10 bits hôtes

Conversion binaire :
10.50.75.130 = 00001010.00110010.01001011.10000010
Masque /22   = 11111111.11111111.11111100.00000000
               = 255.255.252.0

ET logique :
Réseau       = 00001010.00110010.01001000.00000000
             = 10.50.72.0

Broadcast (bits hôte à 1) :
             = 00001010.00110010.01001011.11111111
             = 10.50.75.255

Hôtes : 2^10 - 2 = 1024 - 2 = 1022

Réponses :
1. Réseau : 10.50.72.0
2. Broadcast : 10.50.75.255
3. Hôtes : 1022
```

---

### Exercice 4 : Scanner et analyser réseau

**Objectif** : Utiliser nmap pour découvrir le réseau.

**Scénario** : Scanner le réseau local 192.168.1.0/24.

```bash
# 1. Découverte d'hôtes (ping scan)
sudo nmap -sn 192.168.1.0/24
# Liste les hôtes actifs sans scanner les ports

# 2. Scan rapide des hôtes actifs
nmap -F 192.168.1.0/24
# 100 ports les plus courants

# 3. Scan détaillé d'un hôte spécifique
nmap -A 192.168.1.10
# -A : OS detection, version detection, script scanning, traceroute

# 4. Scanner ports spécifiques
nmap -p 22,80,443,3306,5432 192.168.1.10
# Services courants : SSH, HTTP, HTTPS, MySQL, PostgreSQL

# 5. Scan de plage de ports
nmap -p 1-1024 192.168.1.10
# Tous les ports privilégiés

# 6. Détection de services et versions
nmap -sV 192.168.1.10
# Identifie versions des services

# 7. Scan avec sortie verbose
nmap -v -A 192.168.1.10
# Détails pendant le scan

# 8. Sauvegarder résultats
nmap -oN scan-results.txt 192.168.1.0/24
# Format normal lisible
nmap -oX scan-results.xml 192.168.1.0/24
# Format XML pour analyse
```

**Interpréter les résultats** :
```
Starting Nmap scan...
Nmap scan report for 192.168.1.10
Host is up (0.0012s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu
80/tcp   open  http    Apache httpd 2.4.41
443/tcp  open  ssl/http Apache httpd 2.4.41
3306/tcp open  mysql   MySQL 5.7.32

Analyse :
- Serveur Ubuntu avec SSH (gestion à distance)
- Serveur web Apache sur HTTP et HTTPS
- Base de données MySQL accessible (ATTENTION : risque sécurité)
```

---

### Exercice 5 : Maîtriser la résolution DNS

**Objectif** : Utiliser les outils DNS efficacement.

**Tâches** :

**1. Vérifier configuration locale**
```bash
# Voir serveurs DNS
cat /etc/resolv.conf

# Voir ordre de résolution
cat /etc/nsswitch.conf | grep hosts

# Tester résolution via NSS
getent hosts learning.lpi.org
getent hosts 8.8.8.8
```

**2. Requêtes DNS simples avec host**
```bash
# Adresse IPv4
host learning.lpi.org

# Adresse IPv6
host -t AAAA learning.lpi.org

# Serveurs mail (MX)
host -t MX lpi.org

# Serveurs de noms (NS)
host -t NS lpi.org

# Enregistrement SOA
host -t SOA lpi.org

# Résolution inverse
host 8.8.8.8
```

**3. Requêtes avancées avec dig**
```bash
# Requête simple
dig learning.lpi.org

# Format court (juste la réponse)
dig +short learning.lpi.org

# Type spécifique
dig -t MX lpi.org
dig -t NS lpi.org
dig -t SOA lpi.org

# Serveur DNS spécifique
dig @8.8.8.8 learning.lpi.org
dig @1.1.1.1 learning.lpi.org

# Résolution inverse
dig -x 8.8.8.8

# Options multiples
dig +noall +answer learning.lpi.org
dig +short +nocookie learning.lpi.org

# Tracer requête DNS
dig +trace learning.lpi.org
```

**4. Tests de performance DNS**
```bash
# Mesurer temps de réponse
time dig learning.lpi.org

# Comparer plusieurs serveurs
for dns in 8.8.8.8 1.1.1.1 9.9.9.9; do
    echo "=== DNS $dns ==="
    time dig @$dns +short learning.lpi.org
done

# Statistiques
dig learning.lpi.org | grep "Query time"
```

**5. Configuration personnalisée**
```bash
# Créer ~/.digrc pour options par défaut
cat > ~/.digrc << 'EOF'
+short
+noall +answer
EOF

# Maintenant dig utilisera ces options automatiquement
dig learning.lpi.org
```

---

## 📚 Ressources complémentaires

### Pages de manuel essentielles

```bash
# Configuration IP et interfaces
man ip
man ip-address
man ip-link
man ip-route
man interfaces       # /etc/network/interfaces
man nmcli
man nmcli-examples

# Résolution de noms
man hosts            # /etc/hosts
man resolv.conf      # /etc/resolv.conf
man nsswitch.conf    # /etc/nsswitch.conf
man getent
man host
man dig

# Diagnostic
man ping
man ping6
man traceroute
man traceroute6
man tracepath
man tracepath6
man ss
man netstat
man nmap
man nc
man lsof
man fuser

# Configuration hostname
man hostname
man hostnamectl
```

### Commandes de référence rapide

```bash
# === CONFIGURATION IP ===
ip addr show                      # Afficher adresses
ip addr add IP/MASK dev INTERFACE # Ajouter IP
ip link set INTERFACE up/down     # Activer/désactiver
ip route show                     # Table routage
ip route add default via GATEWAY  # Route par défaut

# === NETWORKMANAGER ===
nmcli general                     # État général
nmcli device                      # Périphériques
nmcli device wifi list            # Scanner Wi-Fi
nmcli device wifi connect SSID password PASS
nmcli connection show             # Connexions
nmcli connection up/down NAME     # Activer/désactiver
nmcli radio wifi on/off           # Wi-Fi on/off

# === DIAGNOSTIC ===
ping -c 4 HOST                    # Test ICMP
traceroute HOST                   # Tracer route
tracepath HOST                    # Tracer + MTU
ss -tulnp                         # Sockets (moderne)
netstat -tulnp                    # Sockets (obsolète)
nmap -F HOST                      # Scan rapide ports
lsof -i :PORT                     # Processus sur port
fuser -vn tcp PORT                # Idem

# === DNS ===
getent hosts HOSTNAME             # Via NSS
host HOSTNAME                     # DNS simple
host -t TYPE HOSTNAME             # Type spécifique
dig HOSTNAME                      # DNS détaillé
dig +short HOSTNAME               # Court
dig @DNS_SERVER HOSTNAME          # Serveur spécifique
```

### Fichiers de configuration clés

```bash
/etc/hostname                     # Nom d'hôte
/etc/hosts                        # Résolution locale
/etc/resolv.conf                  # Configuration DNS
/etc/nsswitch.conf                # Ordre résolution
/etc/network/interfaces           # Interfaces (Debian)
/etc/sysconfig/network-scripts/   # Interfaces (Red Hat)
/etc/systemd/network/             # systemd-networkd
/etc/services                     # Ports standards
```

---

## 🎯 Points clés pour l'examen

### À maîtriser absolument

**Adressage IPv4** :
- ✅ Classes A, B, C et plages privées
- ✅ Calcul masque de sous-réseau (décimal/CIDR)
- ✅ Calcul nombre d'hôtes : 2^n - 2
- ✅ Identifier réseau et broadcast

**Adressage IPv6** :
- ✅ Format 128 bits (8 groupes × 16 bits)
- ✅ Abréviations (omettre zéros)
- ✅ Loopback ::1, link-local fe80::/10, multicast ff02::1

**Ports courants** :
- ✅ 20 ports minimum : 22(SSH), 23(Telnet), 25(SMTP), 53(DNS), 80(HTTP), 110(POP3), 123(NTP), 143(IMAP), 443(HTTPS), 514(Syslog)

**Configuration** :
- ✅ `ip addr add/show`, `ip link set`, `ip route add/show`
- ✅ `nmcli device`, `nmcli connection`, `nmcli radio`
- ✅ `/etc/network/interfaces`, `/etc/hostname`, `/etc/hosts`

**Diagnostic** :
- ✅ `ping`, `traceroute`, `tracepath`
- ✅ `ss -tulnp`, `nmap -F`
- ✅ `lsof -i`, `fuser -vn tcp`

**DNS** :
- ✅ `/etc/resolv.conf`, `/etc/nsswitch.conf`
- ✅ `getent hosts`, `host`, `dig +short`
- ✅ Types : A, AAAA, MX, NS, PTR, SOA

### Pièges courants à éviter

❌ Confondre `ifconfig` (obsolète) et `ip` (moderne)  
❌ Oublier `dev` dans `ip addr add ... dev enp0s8`  
❌ Confondre adresse réseau (.0) et première IP utilisable (.1)  
❌ Compter adresses sans soustraire réseau et broadcast  
❌ Oublier `-6` pour IPv6 avec `route`, `traceroute`  
❌ Penser que ping bloqué = hôte inaccessible (peut être filtré)  
❌ Confondre `nmcli device` et `nmcli connection`  
❌ Oublier que `ss` est moderne, `netstat` obsolète  

### Astuces pour l'examen

⏱️ **Gestion du temps** : 75 min pour 65 questions = ~1min/question  
🧮 **Calculs** : Pratiquer préalablement conversions binaire/décimal  
📝 **Syntaxe** : Connaître `ip`, `nmcli`, `dig` par cœur  
🔍 **Diagnostic** : Approche méthodique (local → passerelle → Internet → DNS)  
📚 **Révision** : Refaire exercices pratiques plusieurs fois  

### Distribution des points par difficulté

- **Facile (35%)** : Classes IP, ports courants, fichiers de config
- **Moyen (50%)** : Calculs sous-réseaux, syntaxe commandes, diagnostic
- **Difficile (15%)** : IPv6 avancé, options complexes, cas particuliers

---

**Bon courage pour votre préparation ! 🎓**

*N'oubliez pas : la pratique est essentielle pour ce sujet. Configurez un lab virtuel et testez toutes les commandes !*
