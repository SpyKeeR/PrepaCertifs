# 📘 Notes de Révision - Sujet 109 : Notions Élémentaires sur les Réseaux

## 🎯 Informations sur le sujet

- **Poids** : 8 points
- **Objectifs** :
  - 109.1 : Notions élémentaires sur les protocoles Internet (4 points)
  - 109.2 : Configuration réseau persistante (4 points)
  - 109.3 : Résolution de problèmes réseaux simples (4 points)
  - 109.4 : Configuration de la résolution de noms (2 points)

---

## 📚 Table des matières

1. [109.1 - Protocoles Internet](#1091---protocoles-internet)
2. [109.2 - Configuration réseau persistante](#1092---configuration-réseau-persistante)
3. [109.3 - Dépannage réseau](#1093---dépannage-réseau)
4. [109.4 - Résolution de noms](#1094---résolution-de-noms)
5. [Checklist de révision](#checklist-de-révision)
6. [Exercices pratiques](#exercices-pratiques)
7. [Ressources complémentaires](#ressources-complémentaires)

---

## 109.1 - Protocoles Internet

### 🔑 Concepts clés

#### Protocole IPv4

**Format d'adresse** :
- 32 bits divisés en 4 octets (notation décimale pointée)
- Exemple : `192.168.10.20` = `11000000.10101000.00001010.00010100`
- Chaque octet : 0-255 (8 bits = 00000000 à 11111111)

**Classes d'adresses IPv4** :

| Classe | Premier octet | Plage | Masque par défaut | Exemple |
|--------|---------------|-------|-------------------|---------|
| A | 1-126 | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 (/8) | 10.25.13.10 |
| B | 128-191 | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 (/16) | 141.150.200.1 |
| C | 192-223 | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 (/24) | 200.178.12.242 |

**Plages IP privées** :

| Classe | Plage privée |
|--------|--------------|
| A | 10.0.0.0 – 10.255.255.255 |
| B | 172.16.0.0 – 172.31.255.255 |
| C | 192.168.0.0 – 192.168.255.255 |

#### Masque de sous-réseau

**Notation CIDR** :
- Indique le nombre de bits pour la partie réseau
- Exemples :
  - `/8` = 255.0.0.0
  - `/16` = 255.255.0.0
  - `/24` = 255.255.255.0
  - `/26` = 255.255.255.192

**Calcul des adresses** :
```
192.168.8.12/24
├─ Plage : 192.168.8.0 - 192.168.8.255
├─ Adresse réseau : 192.168.8.0
├─ Adresse de diffusion : 192.168.8.255
└─ Hôtes utilisables : 192.168.8.1 - 192.168.8.254
```

#### Ports et protocoles de transport

**Ports courants à connaître** :

| Port | Service | Protocole |
|------|---------|-----------|
| 20/21 | FTP (données/contrôle) | TCP |
| 22 | SSH | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | TCP/UDP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |
| 123 | NTP | UDP |
| 139 | NetBIOS | TCP/UDP |
| 143 | IMAP | TCP |
| 161/162 | SNMP/SNMPTRAP | UDP |
| 389 | LDAP | TCP |
| 443 | HTTPS | TCP |
| 465 | SMTPS | TCP |
| 514 | RSH/Syslog | TCP/UDP |
| 636 | LDAPS | TCP |
| 993 | IMAPS | TCP |
| 995 | POP3S | TCP |

**Fichier de référence** :
```bash
cat /etc/services     # Liste des ports standards
```

#### TCP vs UDP vs ICMP

**TCP (Transmission Control Protocol)** :
- ✅ Orienté connexion
- ✅ Fiable : contrôle d'intégrité, ordre, retransmission
- ❌ Plus lent
- Utilisé pour : HTTP, SMTP, FTP, SSH

**UDP (User Datagram Protocol)** :
- ❌ Sans connexion
- ❌ Non fiable : pas de contrôle
- ✅ Plus rapide
- Utilisé pour : DNS, NTP, streaming vidéo

**ICMP (Internet Control Message Protocol)** :
- Protocole de contrôle et diagnostic
- Utilisé pour : ping, traceroute, notifications d'erreurs

#### Protocole IPv6

**Format d'adresse** :
- 128 bits divisés en 8 groupes de 16 bits
- Notation hexadécimale
- Exemple : `2001:0db8:85a3:08d3:1319:8a2e:0370:7344`

**Abréviations IPv6** :
```bash
# Réduire les 0 :
2001:0db8:85a3:0000:0000:0000:0000:7344
→ 2001:0db8:85a3:0:0:0:0:7344

# Omettre les groupes de 0 (une seule fois) :
→ 2001:0db8:85a3::7344
```

**Types d'adresses IPv6** :
- **Unicast** : Une interface (64 bits réseau + 64 bits interface)
- **Multicast** : Groupe d'interfaces (remplacement du broadcast)
- **Anycast** : Groupe mais livraison à une seule interface

**Adresses spéciales** :
- `::1` : Loopback (équivalent de 127.0.0.1)
- `fe80::/10` : Link-local (auto-configuration)
- `ff02::1` : Tous les hôtes du réseau local

**Différences IPv4 vs IPv6** :
```bash
# Notation IP:port
IPv4: 200.216.10.15:443
IPv6: [2001:0db8:85a3::7344]:443

# Broadcast
IPv4: 192.168.1.255
IPv6: ff02::1 (multicast)
```

---

## 109.2 - Configuration réseau persistante

### 🔑 Interfaces réseau

#### Conventions de nommage

**Préfixes modernes (systemd)** :

| Préfixe | Type d'interface |
|---------|------------------|
| `en` | Ethernet |
| `ib` | InfiniBand |
| `sl` | IP série (slip) |
| `wl` | WLAN (sans fil) |
| `ww` | WWAN (cellulaire) |

**Méthodes de nommage (par ordre de priorité)** :
1. Index BIOS/firmware : `eno1`
2. Index PCI Express : `ens1`
3. Adresse bus : `enp3s5`
4. Adresse MAC : `enx78e7d1ea46da`
5. Ancienne convention : `eth0`

#### Visualiser les interfaces

```bash
# Méthode moderne (recommandée)
ip link show                  # Toutes les interfaces
ip link show dev enp0s3       # Interface spécifique

# Autre méthode
nmcli device                  # Via NetworkManager

# Anciennes méthodes (obsolètes)
ifconfig -a                   # Toutes les interfaces
ls /sys/class/net            # Via sysfs
```

#### Configuration manuelle avec ifconfig (obsolète)

```bash
# Configurer IPv4
ifconfig enp0s8 192.168.50.50/24
ifconfig enp0s8 192.168.50.50 netmask 255.255.255.0

# Configurer IPv6 (nécessite 'add')
ifconfig enp0s8 add 2001:db8::10/64

# Activer/désactiver
ifconfig enp0s8 up
ifconfig enp0s8 down

# Modifier MTU
ifconfig enp0s3 mtu 1500
```

#### Configuration moderne avec ip

```bash
# Configurer adresse (IPv4/IPv6)
ip addr add 192.168.5.5/24 dev enp0s8
ip addr add 2001:db8::10/64 dev enp0s8

# Activer/désactiver
ip link set dev enp0s8 up
ip link set dev enp0s8 down

# Modifier MTU
ip link set enp0s8 mtu 2000

# Afficher configuration
ip addr show
ip addr show dev enp0s8
```

### 🔑 Configuration persistante

#### Fichier /etc/network/interfaces (Debian/Ubuntu)

**Format** :
```bash
# Interface de bouclage
auto lo
iface lo inet loopback

# Interface avec DHCP
auto enp3s5
iface enp3s5 inet dhcp

# Interface statique
auto enp0s8
iface enp0s8 inet static
    address 192.168.1.2/24
    gateway 192.168.1.1
```

**Commandes** :
```bash
# Activer/désactiver interface
ifup enp3s5
ifdown enp3s5
```

⚠️ **ATTENTION** : Sur CentOS/Red Hat, la configuration est dans `/etc/sysconfig/network-scripts/`

#### Configuration des noms d'hôtes

**Fichier /etc/hostname** :
```bash
# Voir le nom d'hôte
cat /etc/hostname

# Modifier directement
echo "storage" > /etc/hostname
```

**Commande hostnamectl** :
```bash
# Afficher toutes les infos
hostnamectl
hostnamectl status

# Définir nom d'hôte statique
hostnamectl set-hostname storage

# Définir nom d'hôte amélioré (pretty)
hostnamectl --pretty set-hostname "LAN Shared Storage"

# Définir nom d'hôte transitoire
hostnamectl --transient set-hostname generic-host
```

**Types de noms d'hôtes** :
- **Statique** : Stocké dans `/etc/hostname`, utilisé au boot
- **Amélioré** : Nom descriptif avec caractères spéciaux
- **Transitoire** : Temporaire, défini dynamiquement

#### Résolution de noms locale

**Fichier /etc/hosts** :
```bash
# Format : IP    nom_complet    alias(s)
127.0.0.1       localhost
127.0.1.1       proxy

::1             localhost ip6-localhost ip6-loopback

10.0.0.1        gateway.lpi.org gateway gw
fd00:ffff::1    gateway.lpi.org gateway gw
```

**Règles** :
- IP en premier, puis noms (séparés par espaces/tabulations)
- `#` pour les commentaires
- Noms : alphanumériques, `-`, `.`
- Support IPv4 et IPv6

#### Résolution DNS

**Fichier /etc/resolv.conf** :
```bash
# Domaine de recherche
search lpi.org

# Serveurs DNS (max 3)
nameserver 10.0.0.53
nameserver fd00:ffff::2:53

# Domaine local
domain lpi.org

# Options
options timeout:3
```

**Options courantes** :
- `nameserver` : Serveur DNS (max 3)
- `search` : Domaines de recherche (max 6) pour noms courts
- `domain` : Domaine local (exclusif avec search)
- `options` : timeout, attempts, etc.

**Fichier /etc/nsswitch.conf** :
```bash
# Ordre de résolution
hosts:    files dns

# Autres bases de données
passwd:   compat
group:    compat
```

### 🔑 NetworkManager

#### Commandes nmcli essentielles

**État général** :
```bash
# État de connectivité
nmcli general status
nmcli general          # Équivalent

# Afficher connexions
nmcli connection show
nmcli con show         # Abréviation
```

**Gestion Wi-Fi** :
```bash
# Scanner réseaux disponibles
nmcli device wifi list

# Se connecter
nmcli device wifi connect SSID
nmcli device wifi connect SSID password MOT_DE_PASSE
nmcli device wifi connect SSID password MOT_DE_PASSE hidden yes

# Spécifier interface
nmcli device wifi connect SSID password PASS ifname wlo1
```

**Gestion des connexions** :
```bash
# Activer/désactiver connexion
nmcli connection up Hypnotoad
nmcli connection down Hypnotoad

# Activer/désactiver périphérique
nmcli device connect wlo1
nmcli device disconnect wlo1

# Activer/désactiver Wi-Fi
nmcli radio wifi on
nmcli radio wifi off
```

### 🔑 systemd-networkd

#### Fichiers de configuration

**Emplacements (par ordre de priorité)** :
1. `/etc/systemd/network/` (priorité haute)
2. `/run/systemd/network/` (priorité moyenne)
3. `/lib/systemd/network/` (priorité basse)

**Types de fichiers** :
- `.network` : Configuration IP et routes
- `.netdev` : Périphériques virtuels (bridge, tun)
- `.link` : Configuration bas niveau

**Exemple : /etc/systemd/network/30-lan.network** :
```ini
[Match]
Name=enp3s5
# OU
MACAddress=00:16:3e:8d:2b:5b

[Network]
# Configuration statique
Address=192.168.0.100/24
Gateway=192.168.0.1

# OU DHCP
DHCP=yes        # IPv4 + IPv6
DHCP=ipv4       # IPv4 seulement
DHCP=ipv6       # IPv6 seulement
```

#### Configuration Wi-Fi avec WPA

```bash
# Créer fichier de mot de passe
wpa_passphrase MyWifi > /etc/wpa_supplicant/wpa_supplicant-wlo1.conf
# Saisir le mot de passe

# Activer service
systemctl start wpa_supplicant@wlo1.service
systemctl enable wpa_supplicant@wlo1.service

# Créer fichier .network correspondant dans /etc/systemd/network/
```

---

## 109.3 - Dépannage réseau

### 🔑 Configuration manuelle avancée

#### Gestion des routes

**Afficher la table de routage** :
```bash
# Méthodes modernes
ip route                    # IPv4
ip -6 route                 # IPv6

# Méthodes obsolètes
route
netstat -r
route -6                    # IPv6
```

**Ajouter/supprimer routes** :
```bash
# Avec ip route (moderne)
ip route add 2001:db8:1::/64 via 2001:db8::3
ip route del 2001:db8:1::/64 via 2001:db8::3

# Avec route (obsolète)
route -6 add 2001:db8:1::/64 gw 2001:db8::3
route -6 del 2001:db8:1::/64 gw 2001:db8::3

# Route par défaut
ip route add default via 192.168.1.1
route add default gw 192.168.1.1
```

### 🔑 Outils de diagnostic

#### ping / ping6

**Test de connectivité ICMP** :
```bash
# IPv4
ping -c 3 192.168.50.2        # 3 paquets
ping google.com               # Jusqu'à Ctrl+C

# IPv6
ping6 -c 3 2001:db8::10
```

**Limitations** :
- Peut être bloqué par pare-feu
- Pas de réponse ≠ hôte inaccessible

#### traceroute / traceroute6

**Tracer le chemin vers destination** :
```bash
# UDP (par défaut)
traceroute 192.168.1.20
traceroute6 2001:db8::11

# ICMP (nécessite root)
traceroute -I learning.lpi.org

# TCP (nécessite root)
traceroute -T -p 80 learning.lpi.org

# Options utiles
traceroute -m 60          # Max 60 sauts
```

**Fonctionnement** :
- Incrémente le TTL à chaque paquet
- Chaque routeur répond avec ICMP TTL exceeded
- `*` = Pas de réponse pour ce saut

#### tracepath / tracepath6

**Trouver les MTU** :
```bash
tracepath 192.168.1.20
tracepath6 2001:db8::11
```

**Affichage** :
- Affiche le chemin + MTU de chaque lien
- Résume le PMTU (Path MTU) à la fin

#### netcat (nc)

**Connexions arbitraires TCP/UDP** :
```bash
# Écouter (serveur)
nc -l 1234                    # TCP
nc -u -l 1234                 # UDP

# Se connecter (client)
nc net2.example.net 1234
nc -u net2.example.net 1234   # UDP

# Shell distant (ATTENTION : DANGEREUX)
nc -u -e /bin/bash -l 1234
```

**Utilisation** :
- Tester connectivité
- Transfert de fichiers
- Debug de services réseau

#### ss / netstat

**Afficher connexions et sockets** :

| Option | Description |
|--------|-------------|
| `-a` | Toutes les sockets |
| `-l` | Sockets en écoute |
| `-p` | Processus associé (nécessite root) |
| `-n` | Numérique (pas de résolution) |
| `-t` | Connexions TCP |
| `-u` | Connexions UDP |

```bash
# Moderne (ss - recommandé)
ss -tulnp                     # Très utilisé
ss -ta                        # Toutes connexions TCP

# Obsolète (netstat)
netstat -tulnp
netstat -ta
```

**Exemples pratiques** :
```bash
# Ports en écoute
ss -tuln

# Qui écoute sur port 80 ?
ss -tulnp | grep :80
netstat -tulnp | grep :80

# Connexions établies
ss -tun
```

### 🔑 Autres outils réseau

#### lsof (List Open Files)

**Fichiers réseau** :
```bash
# Tous les fichiers réseau Internet
lsof -i

# Par adresse IP
lsof -i@192.168.1.7

# Par port
lsof -i :22
lsof -i :80,443
lsof -i :1-1024              # Plage

# IPv4 ou IPv6 uniquement
lsof -i4
lsof -i6
```

#### fuser (File User)

**Processus utilisant fichiers/ports** :
```bash
# Répertoire actuel
fuser .
fuser -v .                    # Verbose

# Port réseau
fuser -vn tcp 80
fuser -vn udp 53

# Tuer processus
fuser -k 80/tcp
```

**Types d'accès** :
- `c` : Répertoire actuel
- `e` : Exécutable
- `f` : Fichier ouvert
- `F` : Fichier ouvert en écriture
- `r` : Répertoire racine
- `m` : Fichier mmap

#### nmap (Network Mapper)

**Scanner de ports** :
```bash
# Scanner un hôte
nmap localhost
nmap 192.168.1.10

# Plusieurs hôtes
nmap 192.168.1.3-20           # Plage
nmap 192.168.1.*              # Wildcard
nmap 192.168.1.0/24           # CIDR

# Exclure
nmap 192.168.1.0/24 --exclude 192.168.1.7

# Scanner ports spécifiques
nmap -p 22 localhost
nmap -p ssh,80 localhost
nmap -p 22-80 localhost

# Options utiles
nmap -F localhost             # Scan rapide (100 ports)
nmap -v learning.lpi.org      # Verbose
```

---

## 109.4 - Résolution de noms

### 🔑 Processus de résolution

**Ordre standard** :
1. Application appelle fonction C (gethostbyname)
2. Lecture de `/etc/nsswitch.conf`
3. Consultation des sources dans l'ordre spécifié
4. Retour du résultat

### 🔑 Configuration NSSwitch

**Fichier /etc/nsswitch.conf** :
```bash
# Syntaxe : base_données: source [action] source ...
hosts:    files dns
passwd:   compat
group:    compat
```

**Actions conditionnelles** :
```bash
# Syntaxe
[RÉSULTAT=action]
[!RÉSULTAT=action]

# Exemples
hosts: dns [!UNAVAIL=return] files
# Si DNS pas indisponible, ne pas essayer files

hosts: files [SUCCESS=continue] dns
# Si trouvé dans files, continuer quand même avec dns
```

**Résultats possibles** :
- `SUCCESS` : Trouvé
- `NOTFOUND` : Pas trouvé mais source accessible
- `UNAVAIL` : Source indisponible
- `TRYAGAIN` : Erreur temporaire

**Actions possibles** :
- `return` : Arrêter la recherche
- `continue` : Continuer avec la source suivante

### 🔑 Outils de résolution

#### getent

**Interroger bases de données NSS** :
```bash
# Afficher toutes les entrées
getent hosts
getent passwd
getent group

# Recherche spécifique
getent hosts learning.lpi.org
getent passwd carol

# Spécifier source (glibc >= 2.2.5)
getent -s files hosts learning.lpi.org
getent -s dns hosts learning.lpi.org
```

**Avantage** : Utilise le processus de résolution complet du système

#### host

**Requêtes DNS simples** :
```bash
# Recherche standard (A, AAAA, MX)
host wikipedia.org

# Recherche inverse
host 208.80.154.224

# Type d'enregistrement spécifique
host -t NS lpi.org
host -t SOA lpi.org
host -t MX lpi.org

# Serveur DNS spécifique
host -t MX lpi.org dns1.easydns.com
```

**Types d'enregistrements courants** :
- `A` : Adresse IPv4
- `AAAA` : Adresse IPv6
- `MX` : Mail Exchange
- `NS` : Name Server
- `SOA` : Start of Authority
- `PTR` : Pointeur (reverse lookup)
- `CNAME` : Alias

#### dig

**Requêtes DNS avancées** :
```bash
# Recherche simple
dig learning.lpi.org

# Type spécifique
dig -t SOA lpi.org
dig -t MX lpi.org

# Serveur DNS spécifique
dig @8.8.8.8 learning.lpi.org

# Affichage court
dig +short lpi.org
dig +short -t MX lpi.org

# Options multiples
dig +noall +answer +question lpi.org
dig +nocookie -t MX lpi.org
```

**Sections du résultat** :
1. En-tête : version, requête, options
2. Question : requête envoyée
3. Réponse : résultat de la requête
4. Authority : serveurs NS du domaine
5. Additional : A/AAAA des serveurs NS
6. Statistiques : temps, serveur utilisé

**Configuration personnalisée** :
```bash
# Créer ~/.digrc
cat > ~/.digrc << EOF
+short
+noall +answer
EOF
```

### 🔑 systemd-resolved

**Service de résolution systemd** :
```bash
# Écoute sur 127.0.0.53
# Interroge /etc/systemd/resolv.conf ou /etc/resolv.conf
# Fournit : DNS, mDNS, LLMNR

# Activation dans /etc/nsswitch.conf
hosts: files resolve dns
```

**Fonctionnalités** :
- Cache DNS local
- mDNS (Multicast DNS)
- LLMNR (Link-Local Multicast Name Resolution)
- Intégration avec systemd-networkd

---

## 📝 Checklist de révision

### IPv4 et adressage
- [ ] Comprendre format IPv4 (32 bits, 4 octets)
- [ ] Connaître classes A, B, C et plages
- [ ] Identifier plages IP privées
- [ ] Calculer masque de sous-réseau et CIDR
- [ ] Déterminer adresse réseau et broadcast
- [ ] Calculer nombre d'hôtes utilisables
- [ ] Convertir binaire ↔ décimal

### IPv6 et protocoles
- [ ] Comprendre format IPv6 (128 bits, 8 groupes)
- [ ] Maîtriser abréviations IPv6
- [ ] Différencier unicast, multicast, anycast
- [ ] Connaître 20 ports courants minimum
- [ ] Différencier TCP, UDP, ICMP
- [ ] Comprendre notion de stratum NTP

### Configuration réseau
- [ ] Lister interfaces avec `ip link`
- [ ] Comprendre noms d'interfaces modernes
- [ ] Configurer IP avec `ip addr add`
- [ ] Activer/désactiver interface
- [ ] Modifier MTU
- [ ] Gérer routes avec `ip route`
- [ ] Configurer `/etc/network/interfaces`
- [ ] Utiliser `ifup`/`ifdown`

### NetworkManager
- [ ] Vérifier état avec `nmcli general`
- [ ] Scanner Wi-Fi avec `nmcli device wifi list`
- [ ] Se connecter avec `nmcli device wifi connect`
- [ ] Gérer connexions (up/down)
- [ ] Activer/désactiver radio Wi-Fi

### systemd-networkd
- [ ] Connaître emplacements fichiers (.network)
- [ ] Créer section [Match]
- [ ] Configurer section [Network]
- [ ] Utiliser WPA pour Wi-Fi

### Résolution de noms
- [ ] Configurer `/etc/hosts`
- [ ] Éditer `/etc/resolv.conf`
- [ ] Comprendre `/etc/nsswitch.conf`
- [ ] Utiliser `getent hosts`
- [ ] Effectuer requêtes DNS avec `host`
- [ ] Maîtriser `dig` et options (+short, -t)

### Nom d'hôte
- [ ] Modifier `/etc/hostname`
- [ ] Utiliser `hostnamectl set-hostname`
- [ ] Différencier statique/pretty/transitoire

### Diagnostic réseau
- [ ] Tester connectivité avec `ping`/`ping6`
- [ ] Tracer route avec `traceroute`
- [ ] Trouver MTU avec `tracepath`
- [ ] Utiliser `netcat` pour tests
- [ ] Afficher sockets avec `ss -tulnp`
- [ ] Scanner ports avec `nmap`
- [ ] Identifier processus avec `lsof -i`
- [ ] Utiliser `fuser -vn tcp`

---

## 💡 Exercices pratiques

### Exercice 1 : Calcul de sous-réseaux

**Objectif** : Maîtriser le calcul de sous-réseaux IPv4.

**Scénario** : Vous gérez le réseau 172.16.30.230/27.

**Questions** :
1. Quelle est l'adresse réseau ?
2. Quelle est l'adresse de broadcast ?
3. Combien d'hôtes utilisables ?
4. Quelle est la plage d'IP utilisables ?

**Méthode** :
```
/27 = 255.255.255.224 = 11111111.11111111.11111111.11100000

172.16.30.230 = 10101100.00010000.00011110.11100110
Masque        = 11111111.11111111.11111111.11100000
Réseau        = 10101100.00010000.00011110.11100000 = 172.16.30.224

Broadcast : mettre tous les bits hôte à 1
            = 10101100.00010000.00011110.11111111 = 172.16.30.255

Hôtes utilisables : 2^5 - 2 = 32 - 2 = 30
Plage : 172.16.30.225 - 172.16.30.254
```

**Réponses** :
1. Adresse réseau : `172.16.30.224`
2. Broadcast : `172.16.30.255`
3. Hôtes : `30`
4. Plage : `172.16.30.225 - 172.16.30.254`

---

### Exercice 2 : Configuration réseau statique

**Objectif** : Configurer une interface avec IP statique.

**Scénario** : Configurer `enp0s8` avec :
- IP : 192.168.100.50/24
- Passerelle : 192.168.100.1
- DNS : 8.8.8.8 et 8.8.4.4

**Méthode 1 : ip command (temporaire)** :
```bash
# Configurer IP
sudo ip addr add 192.168.100.50/24 dev enp0s8
sudo ip link set enp0s8 up

# Ajouter route par défaut
sudo ip route add default via 192.168.100.1

# Configurer DNS
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
echo "nameserver 8.8.4.4" | sudo tee -a /etc/resolv.conf

# Vérifier
ip addr show dev enp0s8
ip route
cat /etc/resolv.conf
```

**Méthode 2 : /etc/network/interfaces (persistant)** :
```bash
sudo nano /etc/network/interfaces

# Ajouter :
auto enp0s8
iface enp0s8 inet static
    address 192.168.100.50/24
    gateway 192.168.100.1
    dns-nameservers 8.8.8.8 8.8.4.4

# Appliquer
sudo ifdown enp0s8
sudo ifup enp0s8
```

**Méthode 3 : systemd-networkd** :
```bash
sudo nano /etc/systemd/network/20-wired.network

# Contenu :
[Match]
Name=enp0s8

[Network]
Address=192.168.100.50/24
Gateway=192.168.100.1
DNS=8.8.8.8
DNS=8.8.4.4

# Redémarrer service
sudo systemctl restart systemd-networkd
```

---

### Exercice 3 : Diagnostic de connectivité

**Objectif** : Diagnostiquer problème de connexion.

**Scénario** : Impossible d'accéder à `learning.lpi.org`.

**Étapes de diagnostic** :

1. **Vérifier interface locale** :
```bash
ip addr show
# L'interface est-elle UP ? A-t-elle une IP ?
```

2. **Tester boucle locale** :
```bash
ping -c 3 127.0.0.1
# La pile TCP/IP fonctionne-t-elle ?
```

3. **Tester passerelle** :
```bash
ip route                    # Trouver passerelle
ping -c 3 192.168.1.1       # Tester
# Le routeur local est-il accessible ?
```

4. **Tester DNS** :
```bash
cat /etc/resolv.conf        # Serveurs DNS ?
ping -c 3 8.8.8.8          # DNS Google accessible ?
# Le DNS est-il joignable ?
```

5. **Tester résolution de noms** :
```bash
host learning.lpi.org
dig learning.lpi.org
# La résolution fonctionne-t-elle ?
```

6. **Tester connectivité finale** :
```bash
ping -c 3 learning.lpi.org
traceroute learning.lpi.org
# Où est le blocage ?
```

7. **Tester service** :
```bash
nc -vz learning.lpi.org 80
# Le port est-il ouvert ?
```

**Causes possibles** :
- Interface down → `ip link set dev enp0s8 up`
- Pas d'IP → Vérifier DHCP ou config statique
- Passerelle inaccessible → Problème réseau local
- DNS ne résout pas → Vérifier `/etc/resolv.conf`
- Pare-feu bloque → Vérifier iptables/firewalld

---

### Exercice 4 : Scanner réseau avec nmap

**Objectif** : Découvrir services sur réseau local.

**Scénario** : Scanner le sous-réseau 192.168.1.0/24.

```bash
# Scanner tout le sous-réseau (scan ping)
sudo nmap -sn 192.168.1.0/24

# Scanner hôtes actifs avec ports courants
nmap -F 192.168.1.0/24

# Scanner ports spécifiques sur un hôte
nmap -p 22,80,443,3306 192.168.1.10

# Scan détaillé avec détection OS et services
sudo nmap -A 192.168.1.10

# Scanner plage de ports
nmap -p 1-1024 192.168.1.10

# Identifier services
nmap -sV 192.168.1.10
```

**Interpréter résultats** :
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2
80/tcp   open  http    Apache httpd 2.4.41
443/tcp  open  https   
3306/tcp open  mysql   MySQL 5.7.30
```

---

### Exercice 5 : Configuration NetworkManager en ligne de commande

**Objectif** : Gérer connexions Wi-Fi avec nmcli.

**Tâches** :

1. **Lister périphériques** :
```bash
nmcli device
```

2. **Scanner réseaux Wi-Fi** :
```bash
nmcli device wifi list
```

3. **Se connecter** :
```bash
nmcli device wifi connect "MonWiFi" password "MonMotDePasse"
```

4. **Vérifier connexions** :
```bash
nmcli connection show
```

5. **Déconnecter** :
```bash
nmcli connection down "MonWiFi"
```

6. **Reconnecter** :
```bash
nmcli connection up "MonWiFi"
```

7. **Configurer connexion statique** :
```bash
nmcli con mod "MonWiFi" ipv4.addresses 192.168.1.100/24
nmcli con mod "MonWiFi" ipv4.gateway 192.168.1.1
nmcli con mod "MonWiFi" ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con mod "MonWiFi" ipv4.method manual
nmcli con up "MonWiFi"
```

8. **Revenir à DHCP** :
```bash
nmcli con mod "MonWiFi" ipv4.method auto
nmcli con up "MonWiFi"
```

---

## 📚 Ressources complémentaires

### Documentation officielle

**Pages de manuel essentielles** :
```bash
man ip
man ip-address
man ip-link
man ip-route

man nmcli
man nmcli-examples

man interfaces      # /etc/network/interfaces
man resolv.conf
man nsswitch.conf
man hosts

man ping
man traceroute
man tracepath
man dig
man host
man ss
man netstat
man nmap
```

### Commandes de référence rapide

```bash
# === CONFIGURATION IP ===
ip addr show                # Afficher IP
ip addr add IP/MASK dev IF  # Ajouter IP
ip link set IF up/down      # Activer/désactiver

# === ROUTES ===
ip route                    # Afficher routes
ip route add ... via ...    # Ajouter route

# === NETWORKMANAGER ===
nmcli general               # État
nmcli device wifi list      # Scanner Wi-Fi
nmcli con show              # Connexions

# === DIAGNOSTIC ===
ping -c 4 HOST              # Test ICMP
traceroute HOST             # Tracer route
dig HOST                    # Requête DNS
ss -tulnp                   # Sockets

# === RÉSOLUTION NOMS ===
getent hosts HOSTNAME       # Via NSS
host HOSTNAME               # DNS simple
dig +short HOSTNAME         # DNS rapide
```

### Fichiers de configuration importants

```bash
/etc/hostname               # Nom d'hôte
/etc/hosts                  # Résolution locale
/etc/resolv.conf            # Configuration DNS
/etc/nsswitch.conf          # Ordre résolution
/etc/network/interfaces     # Config interfaces (Debian)
/etc/systemd/network/       # systemd-networkd
/etc/services               # Ports standards
```

---

## 🎯 Points clés pour l'examen

### À retenir absolument

**Adressage** :
- ✅ Classes A, B, C et plages privées
- ✅ Calcul masque et nombre d'hôtes
- ✅ 20 ports courants minimum

**Configuration** :
- ✅ `ip addr`, `ip link`, `ip route`
- ✅ `nmcli` pour NetworkManager
- ✅ `/etc/network/interfaces`

**Diagnostic** :
- ✅ `ping`, `traceroute`, `tracepath`
- ✅ `ss -tulnp` ou `netstat -tulnp`
- ✅ `nmap` pour scanner

**Résolution** :
- ✅ `/etc/hosts`, `/etc/resolv.conf`, `/etc/nsswitch.conf`
- ✅ `getent`, `host`, `dig`
- ✅ `hostnamectl`

### Pièges courants

❌ Confondre `ifconfig` (obsolète) et `ip` (moderne)  
❌ Oublier `add` pour IPv6 avec `ifconfig`  
❌ Confondre adresse réseau et première IP utilisable  
❌ Oublier `-6` pour IPv6 avec `route`, `traceroute`  
❌ Ignorer que `ping` peut être bloqué  

### Astuces examen

⏱️ **Temps recommandé** : 15-20 minutes
✍️ **Calculs** : Pratiquer conversions binaire/décimal
📝 **Commandes** : Connaître syntaxe `ip` par cœur
🔍 **Diagnostic** : Approche méthodique (local → distant)

---

**Bon courage pour votre préparation ! 🎓**
