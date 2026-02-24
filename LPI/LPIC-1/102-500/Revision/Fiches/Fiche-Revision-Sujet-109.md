# 📄 Fiche Sujet 109 : Notions Réseaux

**Poids : 8 points (13%)** | Révision rapide

---

## 109.1 : Protocoles Internet (4 pts)

### Adressage IPv4
```bash
# Classes
Classe A: 1-126     /8    255.0.0.0       16M hôtes
Classe B: 128-191   /16   255.255.0.0     65K hôtes
Classe C: 192-223   /24   255.255.255.0   254 hôtes

# Réseaux privés (RFC 1918)
10.0.0.0/8          # Classe A
172.16.0.0/12       # 16 réseaux classe B
192.168.0.0/16      # 256 réseaux classe C

# Réseaux spéciaux
127.0.0.0/8         # Loopback
169.254.0.0/16      # Link-local (APIPA)
0.0.0.0/8           # Réseau actuel

# CIDR
/24 = 255.255.255.0     256 IPs (254 hôtes)
/25 = 255.255.255.128   128 IPs (126 hôtes)
/26 = 255.255.255.192   64 IPs (62 hôtes)
/27 = 255.255.255.224   32 IPs (30 hôtes)
/28 = 255.255.255.240   16 IPs (14 hôtes)
/30 = 255.255.255.252   4 IPs (2 hôtes, P2P)
```

### IPv6
```bash
# Format
2001:0db8:0000:0000:0000:0000:0000:0001
2001:db8::1                  # Compressé

# Types adresses
::1/128                      # Loopback
fe80::/10                    # Link-local
fc00::/7                     # Unique local (privé)
2000::/3                     # Global unicast
ff00::/8                     # Multicast

# Commandes
ip -6 addr                   # Adresses IPv6
ip -6 route                  # Routes IPv6
ping6 fe80::1%eth0           # Ping IPv6 link-local
```

### Ports et protocoles
```bash
# Ports bien connus (<1024)
20/21   FTP (data/control)
22      SSH
23      Telnet
25      SMTP
53      DNS
67/68   DHCP (server/client)
80      HTTP
110     POP3
143     IMAP
443     HTTPS
465/587 SMTPS/Submission
993     IMAPS
995     POP3S
3306    MySQL
5432    PostgreSQL

# Fichier services
/etc/services               # Port → service mapping
grep ssh /etc/services
```

### Protocoles TCP/IP
```bash
# Couche Transport
TCP     # Connecté, fiable, ordre garanti
UDP     # Non connecté, rapide, pas de garantie

# Couche Internet
IP      # Routage paquets
ICMP    # Ping, traceroute, erreurs

# Couche Application
HTTP, FTP, SSH, DNS, SMTP, etc.
```

---

## 109.2 : Configuration réseau persistante (4 pts)

### NetworkManager
```bash
# CLI
nmcli                                    # Infos générales
nmcli device status                      # État interfaces
nmcli connection show                    # Connexions
nmcli connection show "Wired connection 1"
nmcli device show eth0

# Connexion Ethernet statique
nmcli con add type ethernet ifname eth0 \
  con-name eth0-static \
  ip4 192.168.1.100/24 \
  gw4 192.168.1.1 \
  ipv4.dns "8.8.8.8 8.8.4.4"

# DHCP
nmcli con add type ethernet ifname eth0 \
  con-name eth0-dhcp

# Activation/désactivation
nmcli con up eth0-static
nmcli con down eth0-static
nmcli device disconnect eth0
nmcli device connect eth0

# Modification
nmcli con mod eth0-static ipv4.addresses 192.168.1.200/24
nmcli con mod eth0-static ipv4.gateway 192.168.1.254
nmcli con mod eth0-static ipv4.dns "1.1.1.1"

# TUI
nmtui                                    # Interface texte
```

### ip (iproute2)
```bash
# Adresses
ip addr show                             # Toutes interfaces
ip addr show eth0                        # Interface spécifique
ip a                                     # Abrégé
ip addr add 192.168.1.100/24 dev eth0    # Ajouter IP
ip addr del 192.168.1.100/24 dev eth0    # Supprimer IP

# Interfaces
ip link show                             # État interfaces
ip link set eth0 up                      # Activer
ip link set eth0 down                    # Désactiver
ip link set eth0 mtu 9000                # MTU

# Routes
ip route show                            # Table routage
ip r                                     # Abrégé
ip route add default via 192.168.1.1     # Route défaut
ip route add 10.0.0.0/8 via 192.168.1.254
ip route del default                     # Supprimer route
ip route get 8.8.8.8                     # Route vers IP
```

### Fichiers configuration (legacy)
```bash
# Debian/Ubuntu (/etc/network/interfaces)
auto eth0
iface eth0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4

iface eth0 inet dhcp

# Red Hat/CentOS (/etc/sysconfig/network-scripts/ifcfg-eth0)
DEVICE=eth0
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8

BOOTPROTO=dhcp  # Pour DHCP

# Redémarrage réseau
systemctl restart networking              # Debian
systemctl restart NetworkManager          # systemd
ifup eth0 / ifdown eth0                  # Legacy
```

### DNS
```bash
# Fichiers
/etc/resolv.conf                         # Serveurs DNS
# Contenu:
nameserver 8.8.8.8
nameserver 1.1.1.1
search example.com

/etc/hosts                               # Résolution locale
# Format: IP hostname [alias]
127.0.0.1       localhost
192.168.1.10    server1.example.com server1

/etc/nsswitch.conf                       # Ordre résolution
# hosts: files dns
```

### Hostname
```bash
# Affichage
hostname                                 # Nom court
hostname -f                              # FQDN
hostname -i                              # IP
hostnamectl                              # Infos complètes

# Modification
hostname nouveau-nom                     # Temporaire
hostnamectl set-hostname server1.example.com
echo "server1" > /etc/hostname          # Persistant
```

### Diagnostic
```bash
# Connectivité
ping 8.8.8.8                            # Test réseau
ping -c 4 google.com                    # 4 paquets
ping6 2001:4860:4860::8888              # IPv6

# Routage
traceroute google.com                   # Trace route
tracepath google.com                    # Alternatif
mtr google.com                          # Combinaison ping+trace

# DNS
host google.com                         # Résolution simple
dig google.com                          # Détaillé
dig @8.8.8.8 google.com                # Serveur spécifique
nslookup google.com                     # Interactif/direct

# Ports
netstat -tulpn                          # Ports écoute (obsolète)
ss -tulpn                               # Moderne
nc -zv google.com 80                    # Test port (netcat)
telnet google.com 80                    # Test connexion
```

### Utilitaires réseau
```bash
# ARP
ip neigh                                # Table ARP (moderne)
arp -a                                  # Table ARP (legacy)
ip neigh flush all                      # Vider cache

# Interface stats
ip -s link                              # Statistiques interfaces
ifconfig eth0                           # Infos interface (obsolète)
ethtool eth0                            # Détails hardware
```

---

## 🎯 Points clés examen

### Must know
- ✅ Réseaux privés : `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- ✅ CIDR : `/24` = 256 IPs, `/30` = 4 IPs (P2P)
- ✅ Ports : SSH=22, HTTP=80, HTTPS=443, DNS=53, SMTP=25
- ✅ `nmcli con show`, `nmcli con up/down`
- ✅ `ip addr`, `ip route`, `ip link`
- ✅ `ip route add default via GATEWAY`
- ✅ `/etc/resolv.conf` (DNS), `/etc/hosts` (local)
- ✅ `ping`, `traceroute`, `dig`, `host`
- ✅ `ss -tulpn` (ports écoute) vs obsolète `netstat`
- ✅ IPv6 loopback `::1`, link-local `fe80::/10`

### Pièges
- ❌ Oublier `/24` dans `ip addr add` (masque requis)
- ❌ Confondre `nmcli con` et `nmcli device`
- ❌ `ifconfig`/`route` obsolètes (utiliser `ip`)
- ❌ Routes non persistantes avec `ip route` (perdu reboot)
- ❌ Confondre ports client/serveur DHCP (67/68)

### Astuces rapides
```bash
# Config IP statique rapide (non persistant)
ip addr add 192.168.1.100/24 dev eth0
ip link set eth0 up
ip route add default via 192.168.1.1

# Config persistante NetworkManager
nmcli con add type ethernet ifname eth0 con-name static \
  ip4 192.168.1.100/24 gw4 192.168.1.1
nmcli con up static

# Voir route vers IP
ip route get 8.8.8.8

# Calculer IPs dans subnet /26
# 256 - 192 = 64 IPs (62 hôtes utilisables)

# Test DNS
dig +short google.com
host -t MX google.com

# Ports écoute
ss -tulpn | grep :80

# Vider cache DNS
systemd-resolve --flush-caches
resolvectl flush-caches
```

---

**💡 Conseil :** Utilisez `ip` (moderne) au lieu de `ifconfig`/`route` (obsolètes). Maîtrisez `nmcli` pour NetworkManager !
