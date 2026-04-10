# Module 10 - Configuration de base d'un routeur

## Table des matières
1. [Introduction aux routeurs](#introduction)
2. [Configuration initiale d'un routeur](#configuration-initiale)
3. [Configuration des interfaces](#interfaces)
4. [Configuration IPv4 sur les interfaces](#ipv4-config)
5. [Configuration IPv6 sur les interfaces](#ipv6-config)
6. [Adresses IPv6 Link-Local](#link-local)
7. [Vérification de la configuration](#verification)
8. [Routes statiques](#routes-statiques)
9. [Sauvegarde et restauration](#sauvegarde)
10. [Commandes de dépannage](#depannage)

---

## 1. Introduction aux routeurs {#introduction}

### Rôle du routeur
Un **routeur** est un périphérique de **couche 3** (Network Layer) qui :
- **Interconnecte différents réseaux** (LAN avec LAN, LAN avec WAN, LAN avec Internet)
- **Route les paquets** entre réseaux en consultant sa table de routage
- **Prend des décisions** basées sur les adresses IP de destination
- **Segmente les domaines de broadcast** (chaque interface = un réseau différent)

### Composants d'un routeur
- **CPU** : exécute les instructions du système d'exploitation (IOS)
- **RAM** : 
  - Stocke les tables de routage
  - Cache ARP / ND
  - Fichier de configuration en cours (running-config)
  - Paquets en attente de traitement
- **NVRAM** : 
  - Stocke le fichier de configuration de démarrage (startup-config)
  - Mémoire non volatile (conservée après redémarrage)
- **Flash** :
  - Stocke l'image de l'IOS (système d'exploitation Cisco)
  - Mémoire non volatile
- **ROM** :
  - Programme de démarrage (bootstrap)
  - Diagnostic POST (Power-On Self Test)
  - IOS de secours (version réduite)

### Types d'interfaces sur un routeur

#### Interfaces LAN
- **FastEthernet** (100 Mbps) : `FastEthernet0/0` ou `Fa0/0`
- **GigabitEthernet** (1 Gbps) : `GigabitEthernet0/0` ou `Gi0/0` ou `G0/0`
- **10 GigabitEthernet** (10 Gbps) : `TenGigabitEthernet0/0` ou `Te0/0`

#### Interfaces WAN
- **Serial** : connexions point-à-point (PPP, HDLC, Frame Relay)
- **DSL** : connexion ADSL via modem
- **Câble** : connexion via câble coaxial
- **Fibre** : connexions longue distance haut débit

---

## 2. Configuration initiale d'un routeur {#configuration-initiale}

### Accès au routeur
**Connexion console** (câble série) :
1. Connecter le câble console (RJ-45 vers USB ou DB-9)
2. Ouvrir un logiciel de terminal (PuTTY, Tera Term, minicom)
3. Paramètres :
   - **Baud rate** : 9600
   - **Data bits** : 8
   - **Parity** : None
   - **Stop bits** : 1
   - **Flow control** : None

### Modes de configuration

```
Router>                                    # Mode User EXEC
Router> enable
Router#                                    # Mode Privileged EXEC
Router# configure terminal
Router(config)#                            # Mode de configuration globale
Router(config)# interface g0/0
Router(config-if)#                         # Mode de configuration d'interface
Router(config-if)# exit
Router(config)# line console 0
Router(config-line)#                       # Mode de configuration de ligne
Router(config-line)# exit
Router(config)# router ospf 1
Router(config-router)#                     # Mode de configuration du routage
```

### Configuration de base

#### 1. Nom d'hôte (Hostname)
```
Router(config)# hostname R1
R1(config)#
```

#### 2. Bannière de connexion (MOTD)
```
R1(config)# banner motd #
Enter TEXT message. End with the character '#'.
*********************************************
* Unauthorized access is strictly prohibited *
* All activities are logged and monitored    *
*********************************************
#
R1(config)#
```

#### 3. Sécurisation du mode privilégié
```
R1(config)# enable secret Cisco123!
```
- Mot de passe **chiffré** avec MD5
- Remplace `enable password` (moins sécurisé)

#### 4. Sécurisation de la console
```
R1(config)# line console 0
R1(config-line)# password ConsolePass123
R1(config-line)# login
R1(config-line)# logging synchronous
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
```
- `logging synchronous` : empêche les messages système d'interrompre la saisie
- `exec-timeout 5 0` : déconnexion automatique après 5 minutes d'inactivité

#### 5. Sécurisation du VTY (Telnet/SSH)
```
R1(config)# line vty 0 4
R1(config-line)# password VtyPass123
R1(config-line)# login
R1(config-line)# transport input ssh
R1(config-line)# exec-timeout 10 0
R1(config-line)# exit
```
- `transport input ssh` : autoriser seulement SSH (plus sécurisé que Telnet)
- `line vty 0 4` : configuration des 5 lignes VTY (0 à 4)

#### 6. Chiffrement des mots de passe en clair
```
R1(config)# service password-encryption
```
- Chiffre les mots de passe configurés en texte clair (type 7)
- ⚠️ Chiffrement faible, préférer `enable secret` et des mots de passe locaux avec `username ... secret`

#### 7. Configuration d'un utilisateur local
```
R1(config)# username admin privilege 15 secret AdminPass123
```
- Crée un compte utilisateur avec accès au mode privilégié (niveau 15)
- `secret` : mot de passe chiffré avec un algorithme fort

#### 8. Configuration SSH

**Étape 1 : Définir le domaine**
```
R1(config)# ip domain-name example.com
```

**Étape 2 : Générer les clés RSA**
```
R1(config)# crypto key generate rsa
How many bits in the modulus [512]: 2048
```
- Recommandation : **2048 bits minimum** pour une bonne sécurité

**Étape 3 : Configurer SSH version 2**
```
R1(config)# ip ssh version 2
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 3
```

**Étape 4 : Configurer les lignes VTY pour SSH uniquement**
```
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit
```
- `login local` : utiliser la base de données locale des utilisateurs

---

## 3. Configuration des interfaces {#interfaces}

### Affichage des interfaces
```
R1# show ip interface brief
R1# show ipv6 interface brief
R1# show interfaces
R1# show interfaces g0/0
R1# show interfaces description
```

### États des interfaces

| État | Signification |
|------|---------------|
| **up / up** | Interface physiquement active et protocole actif (opérationnelle) |
| **down / down** | Interface physiquement inactive (câble débranché, interface éteinte) |
| **up / down** | Interface active mais protocole inactif (problème de couche 2) |
| **administratively down / down** | Interface désactivée avec `shutdown` |

### Commandes de base sur les interfaces

#### Accéder à une interface
```
R1(config)# interface gigabitEthernet 0/0
R1(config-if)#
```

Notations équivalentes :
- `interface gigabitEthernet 0/0`
- `interface GigabitEthernet0/0`
- `interface g0/0`
- `interface Gi0/0`

#### Activer une interface
```
R1(config-if)# no shutdown
```
- Par défaut, les interfaces sont **désactivées** (`shutdown`)
- **TOUJOURS** exécuter `no shutdown` pour activer une interface

#### Désactiver une interface
```
R1(config-if)# shutdown
```

#### Ajouter une description
```
R1(config-if)# description Connexion vers Switch1 - VLAN 10
```

---

## 4. Configuration IPv4 sur les interfaces {#ipv4-config}

### Assigner une adresse IPv4
```
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

### Exemple de configuration complète IPv4
```
R1(config)# interface g0/0
R1(config-if)# description LAN Administratif
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface g0/1
R1(config-if)# description Connexion vers ISP
R1(config-if)# ip address 203.0.113.1 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
```

### Vérification IPv4
```
R1# show ip interface brief
R1# show ip interface g0/0
R1# show ip route
R1# show ip route connected
```

---

## 5. Configuration IPv6 sur les interfaces {#ipv6-config}

### Activer le routage IPv6 ⚠️ **ÉTAPE OBLIGATOIRE**
```
R1(config)# ipv6 unicast-routing
```
- **IMPORTANT** : cette commande active le routage IPv6 sur le routeur
- Sans elle, le routeur ne routera pas les paquets IPv6
- Permet également au routeur d'envoyer des **Router Advertisements (RA)**

### Assigner une adresse IPv6
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
```

### Auto-configuration avec EUI-64
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
R1(config-if)# no shutdown
R1(config-if)# exit
```
- L'**Interface ID** (64 bits de poids faible) est généré automatiquement à partir de l'adresse MAC
- Format : adresse MAC (48 bits) → insertion de `FFFE` au milieu → inversion du 7e bit

**Exemple** :
- MAC : `00:1A:2B:3C:4D:5E`
- EUI-64 : `021A:2BFF:FE3C:4D5E`
- Adresse complète : `2001:db8:acad:1:021A:2BFF:FE3C:4D5E`

---

## 6. Adresses IPv6 Link-Local {#link-local}

### Qu'est-ce qu'une adresse Link-Local ?
- Plage : **FE80::/10** (commence par FE80, FE90, FEA0, FEB0)
- Valide **uniquement sur le lien local** (un seul segment réseau)
- **Non routable** (ne traverse pas les routeurs)
- Utilisée pour :
  - Communication entre voisins sur le même lien
  - **Passerelle par défaut** pour les hôtes IPv6
  - Protocoles de routage (OSPF, EIGRP)
  - NDP (Neighbor Discovery Protocol)

### Génération automatique
Quand une interface IPv6 est configurée, une **adresse link-local est automatiquement générée** :
- **Format** : `FE80::<Interface-ID>/10`
- Interface ID généré avec **EUI-64** à partir de la MAC

**Exemple** :
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
```

**Résultat** : 2 adresses sur l'interface :
- **Unicast globale** : `2001:db8:acad:1::1/64`
- **Link-local** : `FE80::2E0:F7FF:FE12:3456/10` (générée automatiquement)

### Configuration manuelle d'une adresse Link-Local ⚠️ **POINT IMPORTANT**

**Pourquoi configurer manuellement ?**
- Adresses EUI-64 difficiles à mémoriser
- Simplifier la gestion du réseau
- Utiliser des adresses prévisibles et logiques

**Commande** :
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# exit
```

**Exemple complet** :
```
R1(config)# interface g0/0
R1(config-if)# description LAN Administratif
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface g0/1
R1(config-if)# description Connexion vers R2
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
R1(config-if)# exit
```

**Avantages** :
- ✅ Adresses **simples et mémorisables** : `FE80::1`, `FE80::2`, etc.
- ✅ **Cohérence** : même adresse link-local sur toutes les interfaces d'un routeur
- ✅ Facilite l'**identification** et le **dépannage**
- ✅ Utilisée comme **passerelle par défaut** pour les clients

**Commandes de vérification** :
```
R1# show ipv6 interface brief
R1# show ipv6 interface g0/0
```

**Exemple de sortie** :
```
GigabitEthernet0/0         [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
```

---

## 7. Vérification de la configuration {#verification}

### Vérification globale

#### Afficher les interfaces et leurs adresses IPv4
```
R1# show ip interface brief
```

**Exemple de sortie** :
```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     192.168.2.1     YES manual up                    up
Serial0/0/0            10.1.1.1        YES manual up                    up
Serial0/0/1            unassigned      YES unset  administratively down down
```

#### Afficher les interfaces et leurs adresses IPv6
```
R1# show ipv6 interface brief
```

**Exemple de sortie** :
```
GigabitEthernet0/0     [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
GigabitEthernet0/1     [up/up]
    FE80::1
    2001:DB8:ACAD:2::1
```

### Vérification détaillée d'une interface

#### IPv4
```
R1# show ip interface g0/0
```

Informations affichées :
- État de l'interface (up/down)
- Adresse IP et masque
- Méthode d'assignation (manual, DHCP)
- MTU
- Broadcast address
- État du proxy ARP

#### IPv6
```
R1# show ipv6 interface g0/0
```

Informations affichées :
- Adresse IPv6 unicast globale
- Adresse link-local
- Groupes multicast rejoints
- ND (Neighbor Discovery) DAD (statut de détection de doublons)
- ICMP redirects activés/désactivés

### Vérification de la configuration complète

#### Configuration en cours (RAM)
```
R1# show running-config
```

#### Configuration sauvegardée (NVRAM)
```
R1# show startup-config
```

#### Afficher seulement les interfaces
```
R1# show running-config | section interface
R1# show running-config | include interface
```

### Vérification de la table de routage

#### IPv4
```
R1# show ip route
```

**Codes des routes** :
- **C** : réseau directement connecté
- **L** : adresse locale (IP de l'interface)
- **S** : route statique
- **D** : route EIGRP
- **O** : route OSPF

#### IPv6
```
R1# show ipv6 route
```

**Codes similaires** : C, L, S, D, O

### Vérification de la connectivité

#### Ping IPv4
```
R1# ping 192.168.1.10
```

#### Ping IPv6
```
R1# ping ipv6 2001:db8:acad:1::10
```

#### Traceroute IPv4
```
R1# traceroute 8.8.8.8
```

#### Traceroute IPv6
```
R1# traceroute ipv6 2001:4860:4860::8888
```

---

## 8. Routes statiques {#routes-statiques}

### Route statique IPv4

**Syntaxe** :
```
Router(config)# ip route [réseau-destination] [masque] [next-hop-ip | exit-interface]
```

**Exemple 1 : avec next-hop IP**
```
R1(config)# ip route 192.168.3.0 255.255.255.0 10.1.1.2
```
- Pour atteindre le réseau `192.168.3.0/24`, envoyer les paquets à `10.1.1.2`

**Exemple 2 : avec interface de sortie**
```
R1(config)# ip route 192.168.3.0 255.255.255.0 serial 0/0/0
```

**Exemple 3 : route par défaut**
```
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2
```
- Envoie tout le trafic non spécifié vers `203.0.113.2` (ISP)

### Route statique IPv6

**Syntaxe** :
```
Router(config)# ipv6 route [préfixe/longueur] [next-hop-ipv6 | exit-interface]
```

**Exemple 1 : avec next-hop IPv6**
```
R1(config)# ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2
```

**Exemple 2 : avec interface de sortie**
```
R1(config)# ipv6 route 2001:db8:acad:3::/64 serial 0/0/0
```

**Exemple 3 : route par défaut IPv6**
```
R1(config)# ipv6 route ::/0 2001:db8:acad:2::2
```

**Exemple 4 : avec next-hop link-local (nécessite interface de sortie)**
```
R1(config)# ipv6 route 2001:db8:acad:3::/64 serial 0/0/0 fe80::2
```
- ⚠️ Quand on utilise une adresse link-local comme next-hop, **on doit spécifier l'interface de sortie**

### Vérification des routes statiques
```
R1# show ip route static
R1# show ipv6 route static
R1# show ip route
R1# show ipv6 route
```

---

## 9. Sauvegarde et restauration {#sauvegarde}

### Sauvegarde de la configuration

#### Sauvegarder running-config → startup-config
```
R1# copy running-config startup-config
Destination filename [startup-config]? [Entrée]
Building configuration...
[OK]
```

**Raccourcis** :
```
R1# copy run start
R1# write
R1# write memory
```

#### Sauvegarder vers un serveur TFTP
```
R1# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [R1-confg]? R1-backup-2026-02-24
```

### Restauration de la configuration

#### Restaurer startup-config → running-config
```
R1# copy startup-config running-config
```
- ⚠️ Attention : **fusionne** les configurations (ne remplace pas)

#### Restaurer depuis un serveur TFTP
```
R1# copy tftp: running-config
Address or name of remote host []? 192.168.1.100
Source filename []? R1-backup-2026-02-24
```

#### Restaurer et redémarrer
```
R1# copy tftp: startup-config
Address or name of remote host []? 192.168.1.100
Source filename []? R1-backup-2026-02-24
R1# reload
```

### Suppression de la configuration

#### Effacer startup-config
```
R1# erase startup-config
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
```

**Raccourcis** :
```
R1# write erase
```

#### Effacer les clés SSH (avant réinitialisation complète)
```
R1(config)# crypto key zeroize rsa
```

#### Redémarrage du routeur
```
R1# reload
System configuration has been modified. Save? [yes/no]: no
Proceed with reload? [confirm] [Entrée]
```

---

## 10. Commandes de dépannage {#depannage}

### Diagnostic des interfaces

```
R1# show interfaces g0/0
R1# show ip interface g0/0
R1# show ipv6 interface g0/0
R1# show interfaces status
R1# show interfaces description
```

### Diagnostic de la connectivité

#### Ping étendu (Extended Ping) - IPv4
```
R1# ping
Protocol [ip]: 
Target IP address: 192.168.3.10
Repeat count [5]: 100
Datagram size [100]: 
Timeout in seconds [2]: 
Extended commands [n]: y
Source address or interface: 192.168.1.1
Type of service [0]: 
Set DF bit in IP header? [no]: 
Validate reply data? [no]: 
Data pattern [0xABCD]: 
Loose, Strict, Record, Timestamp, Verbose[none]: 
Sweep range of sizes [n]: 
```

#### Traceroute
```
R1# traceroute 8.8.8.8
R1# traceroute ipv6 2001:4860:4860::8888
```

### Diagnostic du routage

```
R1# show ip route
R1# show ipv6 route
R1# show ip protocols
R1# show ipv6 protocols
```

### Diagnostic des protocoles de routage

```
R1# show ip ospf neighbor
R1# show ip eigrp neighbors
R1# show ip bgp summary
R1# show ipv6 ospf neighbor
```

### Debug (attention : peut surcharger le processeur)

```
R1# debug ip routing
R1# debug ipv6 routing
R1# debug ip icmp
R1# debug ipv6 nd
```

**⚠️ Désactiver après utilisation** :
```
R1# undebug all
R1# no debug all
```

### Vérification du matériel

```
R1# show version
R1# show flash
R1# show processes
R1# show memory
R1# show interfaces counters errors
```

---

## Résumé des points clés 🎯

### Configuration initiale
- ✅ **Hostname**, **bannière MOTD**, **mot de passe enable secret**
- ✅ Sécuriser **console**, **VTY**, **chiffrement des mots de passe**
- ✅ Configurer **SSH** (domaine, clés RSA, version 2)
- ✅ Créer des **utilisateurs locaux** avec `username ... secret`

### Configuration des interfaces
- ✅ **Toujours** exécuter `no shutdown` pour activer une interface
- ✅ Ajouter une **description** pour documenter la fonction
- ✅ IPv4 : `ip address [IP] [masque]`
- ✅ IPv6 : `ipv6 address [IPv6/préfixe]`
- ✅ **Activer le routage IPv6** : `ipv6 unicast-routing` (obligatoire)

### Adresses Link-Local IPv6 ⚠️ **IMPORTANT**
- ✅ Automatiquement générées (FE80::/10) avec EUI-64
- ✅ **Configuration manuelle recommandée** : `ipv6 address fe80::1 link-local`
- ✅ Utilisée comme **passerelle par défaut** pour les clients
- ✅ Simplifie la gestion et permet des adresses **mémorisables**

### Routes statiques
- ✅ IPv4 : `ip route [réseau] [masque] [next-hop]`
- ✅ IPv6 : `ipv6 route [préfixe/longueur] [next-hop]`
- ✅ Route par défaut : `0.0.0.0/0` (IPv4) ou `::/0` (IPv6)
- ✅ Si next-hop link-local → **spécifier l'interface de sortie**

### Vérification et sauvegarde
- ✅ `show ip interface brief` / `show ipv6 interface brief`
- ✅ `show running-config` / `show startup-config`
- ✅ `show ip route` / `show ipv6 route`
- ✅ **Sauvegarder** : `copy running-config startup-config` (ou `write`)

### Diagnostic
- ✅ `ping`, `traceroute` (ajouter `ipv6` pour IPv6)
- ✅ `show interfaces` pour l'état des interfaces
- ✅ `debug` pour surveillance en temps réel (⚠️ désactiver après)

---

**Prochaine étape** : Module 11 - Adressage IPv4 et Sous-réseaux
