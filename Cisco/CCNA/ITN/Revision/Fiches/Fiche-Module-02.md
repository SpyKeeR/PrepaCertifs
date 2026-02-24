# Fiche Module 02 : Configuration de base IOS
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Cisco IOS
- **Système d'exploitation** des équipements Cisco (routeurs, switches)
- **Interface** : CLI (Command Line Interface)
- **Versions** : IOS, IOS XE, IOS XR, NX-OS

### Méthodes d'accès
- **Console** : Câble physique, configuration initiale (9600 8N1)
- **SSH** : Connexion réseau sécurisée (chiffrée) ✅ Recommandé
- **Telnet** : Non chiffré ⚠️ Déconseillé (mots de passe en clair)
- **AUX** : Modem (rare aujourd'hui)

---

## 🔧 Modes de commande IOS

| Mode | Invite | Accès | Commandes typiques |
|------|--------|-------|-------------------|
| **User EXEC** | `Switch>` | Accès initial | `ping`, `show version`, `traceroute` (consultation limitée) |
| **Privileged EXEC** | `Switch#` | Après `enable` | Toutes commandes `show`, `debug`, `reload`, `copy` |
| **Configuration globale** | `Switch(config)#` | Après `configure terminal` | `hostname`, `interface`, `line`, `no`, `ip route` |
| **Configuration interface** | `Switch(config-if)#` | Après `interface <type> <num>` | `ip address`, `no shutdown`, `description` |
| **Configuration ligne** | `Switch(config-line)#` | Après `line console 0` ou `line vty 0 4` | `password`, `login`, `transport input ssh` |

---

## 🔧 Commandes IOS essentielles

### Navigation entre les modes
```cisco
Switch> enable                         # User → Privileged
Switch# configure terminal             # Privileged → Config Globale
Switch(config)# interface fa0/1        # Config → Interface
Switch(config-if)# exit                # Retour d'un niveau
Switch(config)# end                    # Retour direct au Privileged
Switch# disable                        # Privileged → User
```

### Raccourcis clavier
| Raccourci | Action |
|-----------|--------|
| `Tab` | Complétion automatique |
| `Ctrl + A` | Début de ligne |
| `Ctrl + E` | Fin de ligne |
| `Ctrl + R` | Réaffiche la ligne |
| `Ctrl + Z` | Quitte la config (= `end`) |
| `Ctrl + C` | Annule la commande |
| `Ctrl + Shift + 6` | Interrompt processus (ping) |
| `↑` / `↓` | Historique des commandes |

### Aide contextuelle
```cisco
Switch# ?                              # Liste des commandes disponibles
Switch# show ?                         # Options de la commande show
Switch# sh                             # Commande incomplète → aide
```

---

## 🔧 Configuration de base d'un switch

```cisco
# Accès au mode privilégié
Switch> enable

# Mode de configuration globale
Switch# configure terminal

# Nom de l'équipement
Switch(config)# hostname SW1

# Désactivation de la résolution DNS
SW1(config)# no ip domain-lookup

# Bannière MOTD (Message of the Day)
SW1(config)# banner motd # Accès réservé #

# Mot de passe mode privilégié (chiffré)
SW1(config)# enable secret Cisco123!

# Configuration console
SW1(config)# line console 0
SW1(config-line)# password Console123
SW1(config-line)# login
SW1(config-line)# logging synchronous
SW1(config-line)# exit

# Configuration VTY (SSH/Telnet)
SW1(config)# line vty 0 15
SW1(config-line)# password VTY123
SW1(config-line)# login
SW1(config-line)# transport input ssh   # SSH uniquement
SW1(config-line)# exit

# Configuration interface VLAN 1 (gestion)
SW1(config)# interface vlan 1
SW1(config-if)# ip address 192.168.1.10 255.255.255.0
SW1(config-if)# no shutdown
SW1(config-if)# exit

# Passerelle par défaut
SW1(config)# ip default-gateway 192.168.1.1

# Sauvegarde de la configuration
SW1# copy running-config startup-config
# ou
SW1# write memory
```

---

## 🔧 Commandes de vérification

```cisco
show running-config              # Config active (RAM)
show startup-config              # Config sauvegardée (NVRAM)
show version                     # Version IOS, uptime, modèle
show ip interface brief          # Résumé des interfaces IP
show interfaces                  # Détails interfaces
show mac address-table           # Table MAC du switch
show history                     # Historique des commandes
```

---

## 📊 Types de mémoires

| Mémoire | Type | Contenu | Volatilité |
|---------|------|---------|------------|
| **RAM** | Volatile | Running-config, table MAC, table ARP | Perdue au redémarrage |
| **NVRAM** | Non-volatile | Startup-config | Conservée |
| **Flash** | Non-volatile | IOS (système d'exploitation) | Conservée |
| **ROM** | Non-volatile | Bootloader, POST, ROM Monitor | Conservée |

---

## 💡 À retenir absolument

✅ **`enable`** = Passe en mode privilégié (#)  
✅ **`configure terminal`** = Passe en mode de configuration globale  
✅ **`enable secret`** = Mot de passe chiffré (prioritaire sur `enable password`)  
✅ **`no shutdown`** = Active une interface  
✅ **`copy run start`** = Sauvegarde la configuration ⚠️ Important !  
✅ **`show running-config`** = Config actuelle (RAM)  
✅ **`show startup-config`** = Config sauvegardée (NVRAM)  
✅ **SSH** = Sécurisé (chiffré), **Telnet** = Non sécurisé ❌  
✅ **`?`** = Aide contextuelle indispensable  
✅ **Tab** = Complétion automatique des commandes  
