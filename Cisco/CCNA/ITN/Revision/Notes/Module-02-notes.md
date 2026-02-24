# Module 02 : Configuration de base des commutateurs et des terminaux
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module introduit Cisco IOS (Internetwork Operating System) et la configuration de base des commutateurs et routeurs.

**Durée estimée :** 5-6 heures  
**Objectifs :** Maîtriser la navigation dans IOS et configurer les paramètres de base

---

## 2.1 Accès à Cisco IOS

### Cisco IOS
- **Définition** : Système d'exploitation des équipements Cisco (routeurs, commutateurs)
- **Interface** : Ligne de commande (CLI - Command Line Interface)
- **Versions** : IOS, IOS XE, IOS XR, NX-OS (selon l'équipement)

### Méthodes d'accès

**1. Accès Console (hors bande - Out-of-Band)**
- Câble console (RJ-45 vers DB-9 ou USB)
- Accès physique direct à l'équipement
- Utilisé pour configuration initiale ou récupération
- Paramètres série : 9600 bauds, 8 bits de données, pas de parité, 1 bit

 d'arrêt (9600 8N1)
- **Logiciels** : PuTTY, Tera Term, Minicom, Screen

**2. Accès SSH (Secure Shell)**
- Connexion réseau sécurisée et chiffrée
- Remplace Telnet (non sécurisé)
- Nécessite configuration préalable sur l'équipement

**3. Accès Telnet**
- Connexion réseau non chiffrée
- ⚠️ **Déconseillé** : Mots de passe transmis en clair
- Encore utilisé en environnement de lab

**4. Accès par port auxiliaire (AUX)**
- Modem pour accès distant d'urgence
- Rare aujourd'hui

---

## 2.2 Navigation IOS

### Modes de commande

**1. Mode Utilisateur (User EXEC Mode)**
```cisco
Switch>
```
- Invite : `>`
- Accès limité (consultation uniquement)
- Commandes de base : `ping`, `show`, `traceroute`

**2. Mode Privilégié (Privileged EXEC Mode)**
```cisco
Switch> enable
Switch#
```
- Invite : `#`
- Accès à toutes les commandes `show` et `debug`
- Peut redémarrer l'équipement
- Commande pour y accéder : `enable`
- Retour : `disable`

**3. Mode de Configuration Globale**
```cisco
Switch# configure terminal
Switch(config)#
```
- Invite : `(config)#`
- Configuration de l'équipement entier
- Commande : `configure terminal` ou `conf t`
- Retour : `exit` ou `end`

**4. Modes de Configuration Spécifiques**

- **Configuration d'interface :**
```cisco
Switch(config)# interface gigabitEthernet 0/0/0
Switch(config-if)#
```

- **Configuration de ligne (console, VTY) :**
```cisco
Switch(config)# line console 0
Switch(config-line)#

Switch(config)# line vty 0 4
Switch(config-line)#
```

- **Configuration de routage (routeurs) :**
```cisco
Router(config)# router ospf 1
Router(config-router)#
```

### Navigation entre les modes
```cisco
Switch> enable                         # User → Privileged
Switch# configure terminal             # Privileged → Global Config
Switch(config)# interface fa0/1        # Global → Interface
Switch(config-if)# exit                # Retour d'un niveau
Switch(config)# end                    # Retour direct au Privileged
Switch# disable                        # Privileged → User
```

### Raccourcis clavier utiles

| Raccourci | Action |
|-----------|--------|
| `Tab` | Complétion automatique de la commande |
| `Ctrl + A` | Début de la ligne |
| `Ctrl + E` | Fin de la ligne |
| `Ctrl + R` | Réaffiche la ligne |
| `Ctrl + Z` | Quitte le mode de configuration (équivalent à `end`) |
| `Ctrl + C` | Annule la commande en cours |
| `Ctrl + Shift + 6` | Interrompt un processus (ping, traceroute) |
| `↑` / `↓` | Historique des commandes |

---

## 2.3 Structure des commandes

### Syntaxe des commandes IOS

**Format général :**
```
commande [sous-commande] [paramètre] [argument]
```

**Exemples :**
```cisco
show ip interface brief
show running-config
interface gigabitEthernet 0/0/0
ip address 192.168.1.1 255.255.255.0
```

### Aide contextuelle

**1. Aide `?` - Liste des commandes disponibles**
```cisco
Switch# ?                              # Toutes les commandes du mode actuel
Switch# show ?                         # Sous-commandes de "show"
Switch# show ip ?                      # Options après "show ip"
```

**2. Complétion automatique (Tab)**
```cisco
Switch# conf<Tab>                      # Complète en "configure"
Switch# sh<Tab>                        # Complète en "show"
```

**3. Syntaxe de commande**
- **[mot-clé]** : Paramètre optionnel
- **{mot-clé}** : Paramètre obligatoire
- **|** : Choix (l'un ou l'autre)

**Exemple :**
```cisco
show ip interface [type number]
```
- `type` et `number` sont optionnels

### Messages d'erreur

**1. Commande ambiguë**
```cisco
Switch# sh co
% Ambiguous command: "sh co"
```
- La commande est incomplète ou ambiguë
- Utiliser `?` pour voir les options

**2. Commande incomplète**
```cisco
Switch# show
% Incomplete command.
```
- Paramètres manquants

**3. Commande incorrecte**
```cisco
Switch# show xyz
% Invalid input detected at '^' marker.
```
- Commande ou paramètre invalide

---

## 2.4 Configuration de base des périphériques

### Configuration initiale d'un commutateur

**1. Nommer l'équipement (hostname)**
```cisco
Switch# configure terminal
Switch(config)# hostname S1
S1(config)#
```

**2. Sécuriser le mode privilégié (enable secret)**
```cisco
S1(config)# enable secret class
```
- Mot de passe chiffré pour accéder au mode privilégié
- Remplace `enable password` (obsolète, non chiffré)

**3. Sécuriser le port console**
```cisco
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
```
- `login` : Active l'authentification par mot de passe

**4. Sécuriser les lignes VTY (Telnet/SSH)**
```cisco
S1(config)# line vty 0 4
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
```
- `vty 0 4` : 5 lignes VTY (connexions simultanées possibles)

**5. Chiffrer tous les mots de passe en clair**
```cisco
S1(config)# service password-encryption
```
- Chiffre les mots de passe `password` (type 7 - faible)
- N'affecte PAS `enable secret` (déjà chiffré type 5 - MD5)

**6. Bannière de connexion (MOTD - Message Of The Day)**
```cisco
S1(config)# banner motd #Acces interdit aux personnes non autorisees#
```
- `#` est le délimiteur (peut être n'importe quel caractère)
- Affiché avant la connexion

**7. Désactiver la recherche DNS**
```cisco
S1(config)# no ip domain-lookup
```
- Évite les délais quand on tape une commande incorrecte

---

## 2.5 Enregistrement des configurations

### Fichiers de configuration

**1. Running-config (running-configuration)**
- Configuration active en mémoire RAM
- Perdue au redémarrage
- Commande : `show running-config`

**2. Startup-config (startup-configuration)**
- Configuration sauvegardée en NVRAM (Non-Volatile RAM)
- Chargée au démarrage
- Commande : `show startup-config`

### Sauvegarder la configuration

**Copier running-config vers startup-config :**
```cisco
S1# copy running-config startup-config
Destination filename [startup-config]? [Entrée]
Building configuration...
[OK]
```

**Raccourcis :**
```cisco
S1# copy run start        # Abréviation acceptable
S1# wr                    # Ancien raccourci (write)
```

### Effacer la configuration

**Supprimer la startup-config :**
```cisco
S1# erase startup-config
```
ou
```cisco
S1# write erase
```

**Redémarrer l'équipement :**
```cisco
S1# reload
```
- Recharge la startup-config (ou configuration d'usine si effacée)

---

## 2.6 Ports et adresses

### Interfaces réseau

**Types d'interfaces sur un commutateur :**
- **FastEthernet** : 100 Mbps (Fa0/1, Fa0/2, etc.)
- **GigabitEthernet** : 1000 Mbps (Gi0/1, Gi1/0/1, etc.)
- **SFP** : Module enfichable pour fibre optique

**Types d'interfaces sur un routeur :**
- **GigabitEthernet** : Gi0/0/0, Gi0/0/1
- **Serial** : S0/0/0, S0/0/1 (WAN)
- **Management** : G0/0 (gestion à distance)

**Nomenclature :**
```
type slot/sous-slot/port
```
- Exemple : `GigabitEthernet 0/0/1`
  - Type : GigabitEthernet
  - Module/Slot : 0
  - Sous-slot : 0
  - Port : 1

### Adresse MAC (Media Access Control)
- Adresse physique gravée sur la carte réseau (NIC)
- **Format** : 48 bits (6 octets) en hexadécimal
- **Exemple** : `00:1A:2B:3C:4D:5E`
- **Composition** :
  - 3 premiers octets : OUI (Organizationally Unique Identifier) - Fabricant
  - 3 derniers octets : Numéro de série unique
- **Unicité** : Chaque carte réseau a une adresse MAC unique

**Commandes :**
```cisco
Switch# show mac address-table         # Table d'adresses MAC du switch
PC> ipconfig /all                      # Voir adresse MAC sous Windows
PC> ip link show                       # Voir adresse MAC sous Linux
```

---

## 2.7 Configuration de l'adressage IP

### Adresse IP sur un commutateur

Les commutateurs de couche 2 n'ont pas d'adresse IP sur leurs ports physiques. L'adresse IP est configurée sur une **interface VLAN virtuelle (SVI)** pour la gestion à distance.

**Configuration de l'interface VLAN (SVI) :**
```cisco
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.10 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
```

**Définir la passerelle par défaut :**
```cisco
S1(config)# ip default-gateway 192.168.1.1
```
- Nécessaire pour gérer le switch depuis un réseau différent

### Adresse IP sur un routeur

Chaque interface physique d'un routeur peut avoir une adresse IP.

**Configuration d'une interface :**
```cisco
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# description Lien vers LAN
R1(config-if)# no shutdown
R1(config-if)# exit
```

**⚠️ Important :** Les interfaces de routeur sont désactivées par défaut (`shutdown`). Il faut les activer avec `no shutdown`.

**Voir la configuration IP :**
```cisco
R1# show ip interface brief
```

---

## 2.8 Vérification de la connectivité

### Commande `ping`
Test de connectivité réseau (protocole ICMP Echo Request/Reply).

**Syntaxe :**
```cisco
Switch# ping 192.168.1.1
Switch# ping google.com
```

**Résultats :**
- `.` : Timeout (pas de réponse)
- `!` : Réponse reçue (succès)
- `U` : Destination inaccessible

**Exemple :**
```
Switch# ping 192.168.1.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/2/5 ms
```

### Commande `traceroute` / `tracert`
Affiche le chemin emprunté par les paquets vers une destination.

**Sur IOS :**
```cisco
Router# traceroute 8.8.8.8
```

**Sur Windows :**
```cmd
C:\> tracert 8.8.8.8
```

**Sur Linux :**
```bash
$ traceroute 8.8.8.8
```

---

## 💡 Points clés à retenir

1. **Cisco IOS** : Système d'exploitation des équipements Cisco
2. **Modes de commande** : User EXEC (`>`), Privileged EXEC (`#`), Configuration globale (`(config)#`)
3. **Configuration de base** : hostname, enable secret, line console/vty, banner motd, service password-encryption
4. **Fichiers de configuration** : running-config (RAM), startup-config (NVRAM)
5. **Sauvegarder** : `copy running-config startup-config`
6. **Vérification** : `ping`, `traceroute`, `show ip interface brief`

---

## 🔗 Commandes essentielles

### Navigation
```cisco
enable                                 # User → Privileged
configure terminal                     # Privileged → Global Config
exit                                   # Retour d'un niveau
end                                    # Retour au Privileged
```

### Configuration de base
```cisco
hostname S1                            # Nom de l'équipement
enable secret motdepasse               # Mot de passe mode privilégié
line console 0
  password cisco
  login
line vty 0 4
  password cisco
  login
service password-encryption            # Chiffrer les mots de passe
banner motd # Message #                # Bannière de connexion
no ip domain-lookup                    # Désactiver recherche DNS
```

### Sauvegarde et visualisation
```cisco
show running-config                    # Voir config active
show startup-config                    # Voir config sauvegardée
copy running-config startup-config     # Sauvegarder
erase startup-config                   # Effacer la config
reload                                 # Redémarrer
```

### Configuration IP
```cisco
interface vlan 1                       # Interface virtuelle (switch)
  ip address 192.168.1.10 255.255.255.0
  no shutdown
ip default-gateway 192.168.1.1         # Passerelle (switch)

interface gi0/0/0                      # Interface physique (routeur)
  ip address 192.168.1.1 255.255.255.0
  no shutdown
```

### Vérification
```cisco
show ip interface brief                # Résumé des interfaces IP
show running-config                    # Config active
ping 192.168.1.1                       # Test de connectivité
traceroute 8.8.8.8                     # Tracer le chemin
```

---

## 📝 Exercices pratiques

1. **Configuration initiale d'un commutateur** :
   - Nommer "S1"
   - Configurer enable secret "class"
   - Sécuriser console et VTY avec mot de passe "cisco"
   - Ajouter bannière MOTD
   - Sauvegarder

2. **Configuration IP** :
   - Configurer VLAN 1 : 192.168.1.2/24
   - Passerelle par défaut : 192.168.1.1
   - Tester avec `ping`

3. **Packet Tracer** :
   - Créer une topologie simple (PC - Switch - Routeur)
   - Configurer les adresses IP
   - Vérifier la connectivité end-to-end

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
