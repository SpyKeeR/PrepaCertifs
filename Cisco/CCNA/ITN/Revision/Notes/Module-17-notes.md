# Module 17 : Conception d'un réseau de petite taille
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module final d'ITN consolide tous les concepts appris en les appliquant à la conception, la configuration et le dépannage d'un réseau de petite taille.

**Durée estimée :** 5-6 heures  
**Objectifs :** Concevoir, implémenter et dépanner un réseau de petite entreprise complet

---

## 17.1 Périphériques d'un petit réseau

### Équipements typiques d'un petit réseau

**Infrastructure de base :**
- **Routeur intégré** : Routage, switch intégré, pare-feu, NAT/PAT, DHCP, DNS
- **Switch(es)** : Commutation L2, parfois L3
- **Point(s) d'accès sans fil** : Connectivité Wi-Fi
- **Serveur(s)** : Fichiers, email, applications (physiques ou cloud)
- **Périphériques finaux** : PC, laptops, smartphones, imprimantes, IoT

**Routeur intégré (ISR - Integrated Services Router)**

Fonctions typiques d'un ISR petit réseau :
- Routage vers Internet (passerelle par défaut)
- NAT/PAT (traduction d'adresses)
- Pare-feu de base (ACL)
- Serveur DHCP interne
- Relais DHCP (si serveur externe)
- VPN (accès distant sécurisé)
- Switch intégré (4-24 ports)
- Point d'accès Wi-Fi intégré (optionnel)

**Exemple de topologie petit réseau :**
```
[Internet] ─── [Modem] ─── [Routeur ISR]
                              │
                    ┌─────────┴─────────┐
                    │                   │
              [Switch 24 ports]    [Point d'accès Wi-Fi]
                    │                   │
         ┌──────────┼──────────┐       │
         │          │          │       │
      [PC]  [Imprimante]  [Serveur] [Clients Wi-Fi]
```

### Topologies courantes

**Topologie étoile étendue**
- Un ou plusieurs switches centraux
- Switches de distribution pour différents départements
- Évolutive et facile à maintenir

**Topologie sans fil**
- Point d'accès central ou multiples
- SSID unique ou multiples (invités, employés)
- Authentification WPA3
- VLANs pour segmentation

---

## 17.2 Applications et protocoles des réseaux de petite taille

### Applications courantes

**Productivité :**
- Suite bureautique (Microsoft 365, Google Workspace)
- Email (Exchange, Gmail)
- Stockage cloud (OneDrive, Dropbox)
- Visioconférence (Teams, Zoom)

**Opérationnel :**
- ERP/CRM (gestion entreprise)
- Comptabilité
- Point de vente (POS)
- Gestion de stock

**Collaboration :**
- Messagerie instantanée (Slack, Teams)
- Partage de fichiers (SharePoint, NAS)
- Gestion de projets (Trello, Jira)

### Protocoles réseau essentiels

**Couche Application (7) :**
- **HTTP/HTTPS** : Web (80/443)
- **DNS** : Résolution de noms (53)
- **SMTP/POP3/IMAP** : Email (25/110/143)
- **FTP/SFTP** : Transfert de fichiers (20-21/22)
- **DHCP** : Attribution IP automatique (67-68)
- **NTP** : Synchronisation horaire (123)
- **SNMP** : Gestion réseau (161-162)

**Couche Transport (4) :**
- **TCP** : Fiable, avec connexion
- **UDP** : Non fiable, sans connexion

**Couche Réseau (3) :**
- **IPv4/IPv6** : Adressage et routage
- **ICMP** : Messages de contrôle (ping, traceroute)
- **ARP** : Résolution MAC (IPv4)
- **NDP** : Découverte de voisins (IPv6)

**Couche Liaison de données (2) :**
- **Ethernet** : Standard LAN câblé
- **Wi-Fi (802.11)** : Standard LAN sans fil

### Services réseau communs

**DHCP (Dynamic Host Configuration Protocol)**
- Attribution automatique d'adresses IP
- Masque de sous-réseau, passerelle, DNS
- Gestion centralisée des adresses
- Réservations pour équipements critiques

**DNS (Domain Name System)**
- Résolution noms de domaine → adresses IP
- DNS interne pour serveurs locaux
- Forwarders vers DNS FAI ou public (8.8.8.8)

**NAT/PAT (Network Address Translation)**
- Traduction adresses privées → publique
- Conservation d'adresses IPv4
- Sécurité par masquage réseau interne

**NTP (Network Time Protocol)**
- Synchronisation horaire des équipements
- Essentiel pour logs, authentification, certificats

---

## 17.3 Évolution vers de plus grands réseaux

### Principes de conception évolutive

**Hiérarchie réseau à 3 couches :**

**1. Couche Cœur (Core)**
- Commutation haute vitesse
- Pas de manipulation de paquets
- Redondance maximale
- Uniquement dans grands réseaux

**2. Couche Distribution**
- Routage entre VLANs
- Agrégation des switches d'accès
- Politiques de sécurité (ACL)
- QoS

**3. Couche Accès**
- Connexion des périphériques finaux
- Port security
- VLANs
- PoE (Power over Ethernet)

**Petit réseau = Distribution + Accès** (couche cœur non nécessaire)

### Conception modulaire

**Modules fonctionnels :**

**Module Entreprise Campus**
- Couches Core, Distribution, Accès
- Infrastructure principale

**Module Bordure Entreprise (Edge)**
- Connexion Internet
- VPN, pare-feu
- DMZ

**Module Télétravail**
- VPN site-à-site
- VPN client-à-site
- Accès distant sécurisé

**Module Centre de données**
- Serveurs
- Stockage (SAN)
- Haute disponibilité

### Évolutivité

**Facteurs à considérer :**

**Bande passante :**
- Liens 1 Gbps minimum accès
- 10 Gbps distribution/core
- Agrégation de liens (EtherChannel)

**Redondance :**
- Double ISP (multi-homing)
- Switches redondants
- Liens redondants
- Alimentations redondantes

**Croissance :**
- Plan d'adressage IP flexible (VLSM)
- Capacité de ports disponibles
- VLANs extensibles
- Architecture modulaire

---

## 17.4 Vérification de la connectivité

### Commandes de base

**Ping - Test de connectivité**
```cisco
! Ping simple
C:\> ping 192.168.1.1

! Ping étendu (Cisco)
Router# ping
Protocol [ip]:
Target IP address: 192.168.1.1
Repeat count [5]: 100
Datagram size [100]:
Timeout in seconds [2]:
Extended commands [n]: n
```

**Interprétation des résultats ping :**
- `.` = Timeout (pas de réponse)
- `!` = Succès
- `U` = Destination unreachable
- `Q` = Source quench (congestion)

**Traceroute - Traçage du chemin**
```cisco
! Windows
C:\> tracert 8.8.8.8

! Linux/Mac
$ traceroute 8.8.8.8

! Cisco
Router# traceroute 8.8.8.8
```

**Utilise :**
- ICMP sous Linux/Cisco
- ICMP ou UDP selon OS

---

## 17.5 Commandes d'hôte et IOS

### Commandes hôte Windows

**Configuration réseau :**
```cmd
ipconfig                  # Config IP basique
ipconfig /all            # Config détaillée
ipconfig /release        # Libérer IP DHCP
ipconfig /renew          # Renouveler IP DHCP
ipconfig /displaydns     # Afficher cache DNS
ipconfig /flushdns       # Vider cache DNS
```

**Tests de connectivité :**
```cmd
ping <IP/hostname>       # Test connectivité
tracert <IP/hostname>    # Tracer route
pathping <IP>            # Combinaison ping+tracert
```

**Affichage :**
```cmd
arp -a                   # Table ARP
netstat -ano             # Connexions actives + ports
nslookup <hostname>      # Requête DNS
route print              # Table de routage
```

### Commandes hôte Linux

**Configuration réseau :**
```bash
ip addr show             # Afficher adresses IP
ip route show            # Table de routage
ifconfig                 # Config interfaces (ancien)
```

**Tests :**
```bash
ping <IP/hostname>       # Test connectivité
traceroute <IP>          # Tracer route
dig <hostname>           # Requête DNS détaillée
nslookup <hostname>      # Requête DNS simple
```

**Outils avancés :**
```bash
ss -tuln                 # Sockets et ports (moderne)
netstat -tuln            # Connexions réseau (ancien)
ip neigh show            # Table ARP/NDP
```

### Commandes IOS essentielles

**Verification de base :**
```cisco
! Interfaces
show ip interface brief
show interfaces
show interfaces status

! Routage
show ip route
show ipv6 route

! Connectivité
ping <IP>
traceroute <IP>

! ARP
show arp
show ip arp

! MAC
show mac address-table

! Configuration
show running-config
show startup-config

! Système
show version
show processes cpu
show memory
```

---

## 17.6 Méthodologies de dépannage

### Approche structurée

**Étapes du dépannage :**

**1. Identifier le problème**
- Collecter informations auprès de l'utilisateur
- Reproduire le problème
- Définir la portée (un utilisateur, un réseau, etc.)

**2. Établir une théorie**
- Liste des causes probables
- Commencer par le plus simple
- Tester théories une par une

**3. Tester la théorie**
- Confirmer ou infirmer
- Si confirmée : passer à la résolution
- Si infirmée : théorie suivante

**4. Établir un plan d'action**
- Définir les étapes de résolution
- Identifier impact potentiel
- Planifier la mise en œuvre

**5. Implémenter la solution**
- Appliquer les changements
- Documenter les actions

**6. Vérifier la solution**
- Tester fonctionnalité complète
- Confirmer avec l'utilisateur
- Vérifier absence d'effets secondaires

**7. Documenter**
- Problème rencontré
- Cause identifiée
- Solution appliquée
- Base de connaissances

### Modèle OSI pour le dépannage

**Approche Bottom-Up (bas vers haut)**

**Couche 1 - Physique :**
- Câbles connectés ?
- Voyants d'interface allumés ?
- Câble endommagé ?
- Port défectueux ?

**Commandes :**
```cisco
show interfaces <interface>
show controllers <interface>
```

**Couche 2 - Liaison de données :**
- VLAN correct ?
- Trunkink configuré ?
- Encapsulation correcte ?
- Erreurs de trame ?

**Commandes :**
```cisco
show interfaces trunk
show vlan brief
show mac address-table
```

**Couche 3 - Réseau :**
- Adresse IP correcte ?
- Masque de sous-réseau correct ?
- Passerelle par défaut ?
- Routage fonctionnel ?

**Commandes :**
```cisco
show ip interface brief
show ip route
ping <gateway>
```

**Couche 4 - Transport :**
- Port correct ?
- Service actif ?
- Pare-feu bloque ?

**Commandes :**
```cisco
Windows: netstat -ano
Linux: ss -tuln
Cisco: show ip ports all
```

**Approche Top-Down (haut vers bas)**

Commencer par couche Application, descendre vers Physique :
- Utile si problème applicatif spécifique
- Exemple : Email fonctionne, Web non → problème HTTP/DNS

**Approche Divide and Conquer (diviser pour régner)**

Commencer par couche médiane (3 ou 4) :
- Si couche 3 OK → problème couches supérieures
- Si couche 3 KO → problème couches inférieures
- Approche la plus efficace

### Outils de dépannage

**Tests de connectivité :**
- `ping` : Test couche 3 (IP, ICMP)
- `traceroute/tracert` : Identification du point de défaillance

**Analyseurs de protocoles :**
- **Wireshark** : Capture et analyse de paquets
- Voir paquets en détail
- Identifier anomalies, retransmissions

**Outils logiciels :**
- Moniteurs réseau (PRTG, Nagios)
- Analyseurs de bande passante
- Scanners réseau (Nmap)

---

## 17.7 Scénarios de dépannage

### Scénario 1 : Pas de connectivité Internet

**Symptômes :**
- PC ne peut pas accéder à Internet
- Ping passerelle locale : OK
- Ping 8.8.8.8 : ÉCHEC

**Dépannage Bottom-Up :**

```cisco
! 1. Vérifier couche 1-2 (OK si ping gateway marche)

! 2. Vérifier couche 3 - Routage
PC> ipconfig
! Vérifier passerelle par défaut

! 3. Sur routeur
Router# show ip route
! Vérifier route par défaut (0.0.0.0/0)

Router# show ip interface brief
! Vérifier interface WAN UP

! 4. Tester connectivité FAI
Router# ping 8.8.8.8
! Si échec : problème liaison FAI ou routage
```

**Causes possibles :**
- Route par défaut manquante sur PC
- Route par défaut manquante sur routeur
- Interface WAN down
- Problème FAI
- NAT mal configuré

### Scénario 2 : DNS ne fonctionne pas

**Symptômes :**
- `ping 8.8.8.8` : OK
- `ping google.com` : ÉCHEC "Unable to resolve"

**Dépannage :**

```cmd
! Windows
ipconfig /all
! Vérifier serveurs DNS configurés

ipconfig /flushdns
! Vider cache DNS

nslookup google.com
! Test résolution manuelle

nslookup google.com 8.8.8.8
! Test avec DNS spécifique
```

**Causes possibles :**
- Pas de serveur DNS configuré
- Serveur DNS incorrect
- Serveur DNS inaccessible
- Pare-feu bloque port 53 UDP

### Scénario 3 : Certains hôtes fonctionnent, pas d'autres

**Symptômes :**
- PC1 : OK
- PC2 : Pas d'accès réseau
- Même VLAN, même subnet

**Dépannage Bottom-Up :**

```cisco
! 1. Couche 1 - Physique
show interfaces <PC2-port>
! Vérifier status up/down, erreurs

! 2. Couche 2 - VLAN
show vlan brief
! Vérifier PC2 dans bon VLAN

show mac address-table | include <PC2-MAC>
! Vérifier apprentissage MAC

! 3. Couche 3 - IP
Sur PC2:
ipconfig /all
! Vérifier config IP (adresse, masque, gateway, DNS)

! Tester DHCP si nécessaire
ipconfig /release
ipconfig /renew
```

**Causes possibles :**
- Câble défectueux ou déconnecté
- Port shutdown
- VLAN incorrect
- Duplex mismatch
- Port security bloque MAC
- Configuration IP statique incorrecte
- Pas d'adresse DHCP disponible

### Scénario 4 : Connectivité intermittente

**Symptômes :**
- Connexions coupées aléatoirement
- Ping avec pertes de paquets
- Applications lentes

**Dépannage :**

```cisco
! 1. Vérifier utilisation bande passante
Router# show interfaces <interface>
! Regarder collisions, erreurs CRC, runts

! 2. Vérifier duplex
show interfaces <port> | include duplex
! Rechercher duplex mismatch

! 3. Vérifier câblage
! Tester avec câble de rechange
! Vérifier longueur < 100m (UTP)

! 4. Vérifier ressources
show processes cpu
show memory
```

**Causes possibles :**
- Duplex mismatch (Half/Full)
- Câble défectueux
- Interférences (EMI)
- Câble trop long (> 100m UTP)
- Problème QoS
- Surcharge réseau
- Boucle réseau (spanning-tree)

---

## 💡 Bonnes pratiques de conception et dépannage

### Conception

✅ **Plan d'adressage IP cohérent**
- Documentation complète
- VLSM pour optimiser
- Réservations pour équipements critiques

✅ **Segmentation réseau**
- VLANs par département/fonction
- VLAN séparé pour invités
- Séparation voix/données

✅ **Redondance des liens critiques**
- Double uplink vers distribution
- EtherChannel
- Spanning-tree configuré

✅ **Sécurité dès la conception**
- ACL sur périphérie
- Port security sur accès
- DHCP snooping
- Private VLANs si nécessaire

✅ **Documentation**
- Diagrammes physiques et logiques
- Plan d'adressage IP
- Configurations standardisées
- Procédures d'intervention

### Dépannage

✅ **Approche méthodique**
- Suivre une méthodologie (Bottom-Up, Top-Down, Divide-and-Conquer)
- Ne pas sauter d'étapes
- Documenter les tests

✅ **Isoler le problème**
- Limiter la portée (un user, un service, tout le réseau)
- Diviser pour régner

✅ **Un changement à la fois**
- Tester l'impact
- Pouvoir revenir en arrière
- Documenter chaque action

✅ **Utiliser les bons outils**
- `ping` et `traceroute` pour connectivité
- `show` commands pour état équipements
- Wireshark pour analyse fine

✅ **Vérifier les basiques**
- Câbles branchés
- Interfaces up
- Pas d'erreurs évidentes dans logs

---

## 📊 Checklist de vérification réseau petit taille

### Couche 1-2 (Physique/Liaison)
- [ ] Tous les câbles connectés et fonctionnels
- [ ] Voyants d'interface verts/actifs
- [ ] Pas de duplex mismatch
- [ ] VLANs correctement configurés
- [ ] Trunking fonctionnel entre switches

### Couche 3 (Réseau)
- [ ] Adressage IP cohérent et documenté
- [ ] Passerelles par défaut configurées
- [ ] Routage inter-VLAN fonctionnel
- [ ] Route par défaut vers Internet
- [ ] NAT/PAT configuré sur routeur bordure

### Services
- [ ] DHCP fonctionnel (pools, exclusions, options)
- [ ] DNS fonctionnel (résolution interne et externe)
- [ ] NTP configuré sur équipements
- [ ] Syslog centralisé

### Sécurité
- [ ] SSH configuré, Telnet désactivé
- [ ] Mots de passe forts sur tous les équipements
- [ ] ACL sur interfaces externes
- [ ] Port security sur interfaces accès
- [ ] DHCP snooping activé
- [ ] Bannières configurées

### Documentation
- [ ] Diagramme physique à jour
- [ ] Diagramme logique à jour
- [ ] Plan d'adressage documenté
- [ ] Configurations sauvegardées
- [ ] Procédures de dépannage disponibles

---

## 🎯 Points clés à retenir

1. **Petit réseau = Simple mais complet** : Tous les services nécessaires dans un design compact
2. **Hiérarchie 2 couches** : Distribution + Accès (pas de Core nécessaire)
3. **ISR = Router tout-en-un** : Routage, switching, firewall, NAT, DHCP, VPN
4. **Méthodologie de dépannage** : Approche structurée en 7 étapes
5. **Modèle OSI** : Outil puissant pour dépannage systématique
6. **Bottom-Up** : De la couche physique vers application (approche courante)
7. **Top-Down** : De l'application vers physique (problèmes applicatifs spécifiques)
8. **Divide and Conquer** : Commencer au milieu, la plus efficace
9. **Documentation** : Essentielle pour maintenance et dépannage
10. **Évolutivité** : Concevoir pour croissance future (bande passante, adressage, redondance)

---

**Félicitations ! Vous avez complété le cours ITN (Introduction to Networks) !**

**Prochaine étape :** [SRWE - Switching, Routing, and Wireless Essentials](../../SRWE/Revision/README.md)
