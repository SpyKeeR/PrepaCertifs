# 📝 Fiche de Révision - Module 10 : Configuration routeur

## 🎯 Concepts clés

### Rôle du routeur
- Périphérique de **couche 3** (Network Layer)
- **Interconnecte différents réseaux** (LAN, WAN, Internet)
- **Route les paquets** en consultant la table de routage
- **Segmente les domaines de broadcast** (chaque interface = réseau différent)

### Composants mémoire

| Mémoire | Contenu | Volatile ? |
|---------|---------|-----------|
| **RAM** | Running-config, tables de routage, cache ARP/ND | Oui |
| **NVRAM** | Startup-config | Non |
| **Flash** | Image IOS | Non |
| **ROM** | Bootstrap, POST, IOS de secours | Non |

### Types d'interfaces
- **LAN** : FastEthernet (100 Mbps), GigabitEthernet (1 Gbps)
- **WAN** : Serial, DSL, Câble, Fibre

---

## 📋 Tableaux récapitulatifs

### États des interfaces

| État | Signification |
|------|---------------|
| **up / up** | Interface opérationnelle (physique + protocole OK) |
| **down / down** | Interface physiquement inactive (câble débranché) |
| **up / down** | Interface active mais protocole inactif (problème Layer 2) |
| **administratively down / down** | Interface désactivée avec `shutdown` |

### Modes de configuration

| Mode | Prompt | Description |
|------|--------|-------------|
| **User EXEC** | `Router>` | Mode limité (consultation) |
| **Privileged EXEC** | `Router#` | Accès complet (show, debug, etc.) |
| **Global Config** | `Router(config)#` | Configuration globale |
| **Interface Config** | `Router(config-if)#` | Configuration d'interface |
| **Line Config** | `Router(config-line)#` | Configuration console/VTY |

### Adresses IPv6 Link-Local ⚠️ **POINT CRUCIAL**

**Plage** : `FE80::/10` (FE80, FE90, FEA0, FEB0)

**Caractéristiques** :
- **Non routable** (valide uniquement sur le lien local)
- **Auto-générée** avec EUI-64 à partir de la MAC
- Utilisée pour :
  - **Passerelle par défaut** pour les hôtes IPv6
  - Communication entre voisins (NDP)
  - Protocoles de routage (OSPF, EIGRP)

**Génération automatique** :
- Format : `FE80::<Interface-ID>/10`
- Interface ID = MAC avec EUI-64
- Exemple : `FE80::2E0:F7FF:FE12:3456`

**Configuration manuelle recommandée** ⚠️ :
```
Router(config-if)# ipv6 address fe80::1 link-local
```

**Avantages de la configuration manuelle** :
- ✅ Adresses **simples et mémorisables** : `FE80::1`, `FE80::2`
- ✅ **Cohérence** sur toutes les interfaces
- ✅ Facilite **identification** et **dépannage**
- ✅ Utilisée comme passerelle par défaut (prévisible)

**Exemple complet** :
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64       # Adresse globale
R1(config-if)# ipv6 address fe80::1 link-local          # Link-local manuelle
R1(config-if)# no shutdown
```

**Résultat** : 2 adresses sur l'interface
- Unicast globale : `2001:db8:acad:1::1/64`
- Link-local : `FE80::1`

---

## ⚡ Commandes IOS essentielles

### Configuration de base du routeur

#### 1. Configuration initiale
```
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# banner motd # Accès non autorisé interdit #
R1(config)# enable secret Cisco123!
R1(config)# service password-encryption
```

#### 2. Sécurisation console
```
R1(config)# line console 0
R1(config-line)# password ConsolePass123
R1(config-line)# login
R1(config-line)# logging synchronous
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
```

#### 3. Sécurisation VTY (Telnet/SSH)
```
R1(config)# line vty 0 4
R1(config-line)# password VtyPass123
R1(config-line)# login
R1(config-line)# transport input ssh
R1(config-line)# exec-timeout 10 0
R1(config-line)# exit
```

#### 4. Configuration SSH ⚠️ **IMPORTANT**
```
# Étape 1 : Domaine
R1(config)# ip domain-name example.com

# Étape 2 : Générer clés RSA (2048 bits minimum)
R1(config)# crypto key generate rsa
How many bits in the modulus [512]: 2048

# Étape 3 : Configurer SSH version 2
R1(config)# ip ssh version 2
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 3

# Étape 4 : VTY pour SSH uniquement
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit
```

#### 5. Créer utilisateur local
```
R1(config)# username admin privilege 15 secret AdminPass123
```

---

### Configuration des interfaces

#### Activation interface ⚠️ **TOUJOURS NÉCESSAIRE**
```
R1(config)# interface g0/0
R1(config-if)# no shutdown          # OBLIGATOIRE pour activer
R1(config-if)# description Connexion vers Switch1
```

#### Configuration IPv4
```
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# description LAN Administratif
R1(config-if)# no shutdown
R1(config-if)# exit
```

#### Configuration IPv6 ⚠️ **ACTIVER LE ROUTAGE IPv6 D'ABORD**
```
# Étape 1 : Activer routage IPv6 (OBLIGATOIRE)
R1(config)# ipv6 unicast-routing

# Étape 2 : Configurer les interfaces
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local         # Recommandé
R1(config-if)# no shutdown
R1(config-if)# exit
```

#### Auto-configuration avec EUI-64
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
R1(config-if)# no shutdown
```

---

### Routes statiques

#### IPv4
```
# Route normale
R1(config)# ip route 192.168.3.0 255.255.255.0 10.1.1.2

# Route par défaut
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1

# Avec interface de sortie
R1(config)# ip route 192.168.3.0 255.255.255.0 serial 0/0/0
```

#### IPv6
```
# Route normale
R1(config)# ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2

# Route par défaut
R1(config)# ipv6 route ::/0 2001:db8:acad:2::1

# Avec next-hop link-local (nécessite interface)
R1(config)# ipv6 route 2001:db8:acad:3::/64 serial 0/0/0 fe80::2
```

---

### Vérification

#### Interfaces
```
R1# show ip interface brief                # Résumé IPv4
R1# show ipv6 interface brief              # Résumé IPv6
R1# show interfaces g0/0                   # Détails interface
R1# show interfaces description            # Descriptions
```

**Exemple de sortie `show ip interface brief`** :
```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     192.168.2.1     YES manual up                    up
Serial0/0/0            unassigned      YES unset  administratively down down
```

**Exemple de sortie `show ipv6 interface brief`** :
```
GigabitEthernet0/0     [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
```

#### Tables de routage
```
R1# show ip route                          # Table IPv4
R1# show ipv6 route                        # Table IPv6
R1# show ip route connected                # Routes connectées
R1# show ip route static                   # Routes statiques
```

#### Configuration
```
R1# show running-config                    # Config active (RAM)
R1# show startup-config                    # Config sauvegardée (NVRAM)
R1# show running-config | section interface
```

#### Connectivité
```
R1# ping 192.168.1.10                      # Ping IPv4
R1# ping ipv6 2001:db8:acad:1::10          # Ping IPv6
R1# traceroute 8.8.8.8                     # Traceroute IPv4
R1# traceroute ipv6 2001:4860:4860::8888   # Traceroute IPv6
```

---

### Sauvegarde et restauration

#### Sauvegarder configuration
```
R1# copy running-config startup-config     # Sauvegarder
R1# copy run start                         # Raccourci
R1# write                                  # Raccourci
R1# write memory                           # Raccourci
```

#### Sauvegarder vers TFTP
```
R1# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [R1-confg]? R1-backup-2026-02-24
```

#### Restaurer depuis TFTP
```
R1# copy tftp: running-config              # Vers RAM (fusion)
R1# copy tftp: startup-config              # Vers NVRAM
```

#### Effacer configuration
```
R1# erase startup-config                   # Effacer NVRAM
R1# write erase                            # Raccourci
R1# reload                                 # Redémarrer
```

#### Effacer clés SSH
```
R1(config)# crypto key zeroize rsa
```

---

## 💡 Points importants pour l'examen

### ⚠️ À retenir absolument

1. **Toujours exécuter `no shutdown` sur les interfaces**
   - Par défaut, interfaces désactivées (`shutdown`)
   - Sans `no shutdown`, interface reste `administratively down`

2. **IPv6 : activer le routage avec `ipv6 unicast-routing`**
   - **OBLIGATOIRE** pour router les paquets IPv6
   - Permet au routeur d'envoyer des Router Advertisements (RA)
   - Sans cette commande, IPv6 ne fonctionne pas

3. **Adresses IPv6 Link-Local (FE80::/10)**
   - Auto-générées avec EUI-64
   - **Configuration manuelle recommandée** : `ipv6 address fe80::1 link-local`
   - Utilisées comme **passerelle par défaut** pour les clients
   - Simplifient la gestion (adresses prévisibles)

4. **Configuration SSH nécessite 4 étapes** :
   - Domaine : `ip domain-name`
   - Clés RSA : `crypto key generate rsa` (2048 bits minimum)
   - Version 2 : `ip ssh version 2`
   - VTY : `transport input ssh` + `login local`

5. **Sauvegarde configuration : `copy run start`**
   - Running-config = RAM (volatile)
   - Startup-config = NVRAM (persistante)
   - Sans sauvegarde, config perdue au redémarrage

6. **Routes statiques** :
   - IPv4 : `ip route [réseau] [masque] [next-hop]`
   - IPv6 : `ipv6 route [préfixe/longueur] [next-hop]`
   - Route par défaut : `0.0.0.0/0` (IPv4) ou `::/0` (IPv6)
   - Si next-hop link-local → **spécifier l'interface de sortie**

7. **Modes de configuration** :
   - `>` → User EXEC (limité)
   - `#` → Privileged EXEC (`enable`)
   - `(config)#` → Global Config (`configure terminal`)
   - `(config-if)#` → Interface Config (`interface g0/0`)

8. **Sécurisation** :
   - `enable secret` : mot de passe privilégié (MD5)
   - `service password-encryption` : chiffre mots de passe en clair (type 7)
   - `username ... secret` : utilisateur avec chiffrement fort
   - SSH préféré à Telnet (chiffré)

### Différences running-config vs startup-config

| Fichier | Emplacement | Volatilité | Commande |
|---------|-------------|-----------|----------|
| **Running-config** | RAM | Volatile (perdu au redémarrage) | `show running-config` |
| **Startup-config** | NVRAM | Persistante | `show startup-config` |

**Sauvegarde** : `copy running-config startup-config`

### Configuration complète minimale

```
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# enable secret Cisco123!
R1(config)# banner motd # Accès interdit #

R1(config)# line console 0
R1(config-line)# password ConsolePass
R1(config-line)# login
R1(config-line)# exit

R1(config)# line vty 0 4
R1(config-line)# password VtyPass
R1(config-line)# login
R1(config-line)# exit

R1(config)# interface g0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# exit
R1# copy running-config startup-config
```

### Dépannage typique

**Problème : interface down/down**
- Vérifier câble, connexion physique
- Vérifier `no shutdown` exécuté

**Problème : interface administratively down**
- Exécuter `no shutdown` sur l'interface

**Problème : impossible de pinguer**
- Vérifier adresses IP (même réseau ?)
- Vérifier table de routage (`show ip route`)
- Vérifier interface active (`show ip interface brief`)

**Problème : IPv6 ne fonctionne pas**
- Vérifier `ipv6 unicast-routing` activé
- Vérifier adresse IPv6 configurée
- Vérifier `no shutdown` sur interface

**Problème : SSH ne fonctionne pas**
- Vérifier domaine configuré
- Vérifier clés RSA générées
- Vérifier `transport input ssh` sur VTY
- Vérifier utilisateur créé avec `username ... secret`

---

**🎓 Conseils pour l'examen** :
- Connaître les étapes de configuration SSH
- Mémoriser `ipv6 unicast-routing` (obligatoire pour IPv6)
- Savoir configurer adresse link-local manuelle
- Comprendre différence running-config / startup-config
- Connaître états interfaces (up/up, down/down, admin down)
- Maîtriser routes statiques IPv4 et IPv6
- Savoir que `no shutdown` est toujours nécessaire
