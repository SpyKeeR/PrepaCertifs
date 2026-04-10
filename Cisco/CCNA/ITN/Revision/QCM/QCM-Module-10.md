# QCM Module 10 - Configuration de base d'un routeur

**Nombre de questions :** 20
**Durée estimée :** 30 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quelle commande configure le nom d'hôte d'un routeur Cisco ?

- [ ] Router(config)# name R1
- [ ] Router(config)# set hostname R1
- [ ] Router(config)# hostname R1
- [ ] Router# hostname R1

---

## Question 2
Quelle commande sécurise l'accès au mode privilégié avec un mot de passe chiffré ?

- [ ] Router(config)# enable password Cisco123
- [ ] Router(config)# enable secret Cisco123
- [ ] Router(config)# password enable Cisco123
- [ ] Router(config)# secret Cisco123

---

## Question 3
**Sélectionnez TROIS réponses correctes.**

Quelles commandes sont nécessaires pour configurer SSH sur un routeur Cisco ?

- [ ] ip domain-name example.com
- [ ] crypto key generate rsa
- [ ] ip ssh version 2
- [ ] ssh enable
- [ ] enable ssh-server

---

## Question 4
Quel mode IOS est représenté par l'invite "Router(config-if)#" ?

- [ ] Mode User EXEC
- [ ] Mode Privileged EXEC
- [ ] Mode de configuration globale
- [ ] Mode de configuration d'interface

---

## Question 5
Quelle commande active une interface de routeur désactivée ?

- [ ] Router(config-if)# enable
- [ ] Router(config-if)# no shutdown
- [ ] Router(config-if)# up
- [ ] Router(config-if)# interface enable

---

## Question 6
Que signifie l'état d'interface "administratively down / down" ?

- [ ] Câble débranché
- [ ] Problème de couche 2
- [ ] Interface désactivée avec la commande shutdown
- [ ] Interface en cours de démarrage

---

## Question 7
**Sélectionnez DEUX réponses correctes.**

Quels états d'interface indiquent que l'interface est opérationnelle ?

- [ ] up / up
- [ ] down / down
- [ ] up / down
- [ ] administratively down / down

---

## Question 8
Quelle commande configure une adresse IPv4 sur une interface ?

- [ ] Router(config-if)# ipv4 address 192.168.1.1 255.255.255.0
- [ ] Router(config-if)# ip address 192.168.1.1 /24
- [ ] Router(config-if)# ip address 192.168.1.1 255.255.255.0
- [ ] Router(config-if)# address 192.168.1.1 255.255.255.0

---

## Question 9 ⚠️ **IMPORTANT**
Quelle commande **OBLIGATOIRE** doit être exécutée avant de configurer IPv6 sur un routeur ?

- [ ] Router(config)# ipv6 enable
- [ ] Router(config)# ipv6 routing
- [ ] Router(config)# ipv6 unicast-routing
- [ ] Router(config)# enable ipv6

---

## Question 10
Quelle commande configure une adresse IPv6 avec auto-génération EUI-64 ?

- [ ] Router(config-if)# ipv6 address 2001:db8:acad:1::1/64
- [ ] Router(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
- [ ] Router(config-if)# ipv6 address auto
- [ ] Router(config-if)# ipv6 enable eui-64

---

## Question 11 ⚠️ **IMPORTANT**
Quelle est la plage d'adresses IPv6 Link-Local ?

- [ ] FC00::/7
- [ ] FE80::/10
- [ ] FF00::/8
- [ ] 2001::/32

---

## Question 12 ⚠️ **IMPORTANT**
Quelle commande configure **manuellement** une adresse IPv6 Link-Local sur une interface ?

- [ ] Router(config-if)# ipv6 address fe80::1
- [ ] Router(config-if)# ipv6 address fe80::1 link-local
- [ ] Router(config-if)# ipv6 link-local fe80::1
- [ ] Router(config-if)# ipv6 address fe80::1/10

---

## Question 13 ⚠️ **IMPORTANT**
**Sélectionnez TROIS utilisations correctes des adresses IPv6 Link-Local.**

- [ ] Utilisée comme passerelle par défaut pour les clients
- [ ] Utilisée pour la communication entre voisins sur le même lien
- [ ] Routable à travers Internet
- [ ] Utilisée par les protocoles de routage (OSPF, EIGRP)
- [ ] Remplace les adresses IPv6 globales

---

## Question 14
Dans l'algorithme EUI-64, que se passe-t-il avec l'adresse MAC pour générer l'Interface ID ?

- [ ] On inverse le premier bit
- [ ] On insère FFFE au milieu et on inverse le 7e bit
- [ ] On double l'adresse MAC
- [ ] On applique un hash SHA-256

---

## Question 15
Quelle commande affiche un résumé des interfaces avec leurs adresses IPv4 ?

- [ ] Router# show interfaces summary
- [ ] Router# show ip interface brief
- [ ] Router# show ip interfaces
- [ ] Router# show running-config

---

## Question 16
Quelle commande affiche les adresses IPv6 de toutes les interfaces ?

- [ ] Router# show ipv6 address
- [ ] Router# show ipv6 interface brief
- [ ] Router# show interfaces ipv6
- [ ] Router# show ipv6 route

---

## Question 17
Quelle commande configure une route statique IPv4 par défaut ?

- [ ] Router(config)# ip route 0.0.0.0 0.0.0.0 [next-hop]
- [ ] Router(config)# ip route default [next-hop]
- [ ] Router(config)# ip default-route [next-hop]
- [ ] Router(config)# default-gateway [next-hop]

---

## Question 18 ⚠️ **IMPORTANT**
Lors de la configuration d'une route statique IPv6 avec un next-hop link-local, que faut-il **obligatoirement** spécifier ?

- [ ] Le masque de sous-réseau
- [ ] L'interface de sortie
- [ ] Le protocole de routage
- [ ] La distance administrative

---

## Question 19
**Sélectionnez TROIS commandes correctes pour sauvegarder la configuration.**

- [ ] copy running-config startup-config
- [ ] copy run start
- [ ] write
- [ ] save config
- [ ] write memory

---

## Question 20
Quelle commande efface complètement la configuration sauvegardée en NVRAM ?

- [ ] Router# clear startup-config
- [ ] Router# erase startup-config
- [ ] Router# delete startup-config
- [ ] Router# remove startup-config

---

## Réponses et explications

### Question 1
**Réponse correcte :** Router(config)# hostname R1

**Explication :**
La commande `hostname` s'exécute en **mode de configuration globale** (config)#. Elle change l'invite de commande pour refléter le nouveau nom. Après exécution, l'invite devient `R1(config)#`.

---

### Question 2
**Réponse correcte :** Router(config)# enable secret Cisco123

**Explication :**
- `enable secret` : mot de passe **chiffré avec MD5** (fort) ✅
- `enable password` : mot de passe en **clair** ou chiffrement faible (type 7) ❌

Si les deux sont configurés, `enable secret` est prioritaire. Toujours utiliser `enable secret` pour la sécurité.

---

### Question 3
**Réponses correctes :** ip domain-name example.com, crypto key generate rsa, ip ssh version 2

**Explication :**
**Configuration SSH complète** :

1. Définir le domaine :
   ```
   Router(config)# ip domain-name example.com
   ```

2. Générer les clés RSA (2048 bits minimum) :
   ```
   Router(config)# crypto key generate rsa
   How many bits in the modulus [512]: 2048
   ```

3. Configurer SSH version 2 :
   ```
   Router(config)# ip ssh version 2
   ```

4. Configurer les lignes VTY :
   ```
   Router(config)# line vty 0 4
   Router(config-line)# transport input ssh
   Router(config-line)# login local
   ```

5. Créer un utilisateur :
   ```
   Router(config)# username admin privilege 15 secret AdminPass123
   ```

---

### Question 4
**Réponse correcte :** Mode de configuration d'interface

**Explication :**
**Hiérarchie des modes IOS** :

| Mode | Invite | Accès |
|------|--------|-------|
| **User EXEC** | `Router>` | Commandes limitées |
| **Privileged EXEC** | `Router#` | `enable` |
| **Configuration globale** | `Router(config)#` | `configure terminal` |
| **Configuration d'interface** | `Router(config-if)#` | `interface g0/0` |
| **Configuration de ligne** | `Router(config-line)#` | `line console 0` |
| **Configuration de routage** | `Router(config-router)#` | `router ospf 1` |

---

### Question 5
**Réponse correcte :** Router(config-if)# no shutdown

**Explication :**
Par défaut, les interfaces de routeur sont **désactivées** (état `shutdown`). La commande `no shutdown` (abrégée `no shut`) active l'interface. 

**⚠️ Point crucial** : Toujours exécuter `no shutdown` après avoir configuré une interface, sinon elle restera "administratively down".

---

### Question 6
**Réponse correcte :** Interface désactivée avec la commande shutdown

**Explication :**
**États des interfaces** :

| État | Signification |
|------|---------------|
| **up / up** | Interface opérationnelle ✅ |
| **down / down** | Câble débranché, interface éteinte |
| **up / down** | Problème Layer 2 (encapsulation, protocole) |
| **administratively down / down** | Interface désactivée avec `shutdown` |

---

### Question 7
**Réponses correctes :** up / up

**Explication :**
Seul l'état **up / up** indique une interface pleinement opérationnelle :
- **Premier "up"** : état physique (Layer 1) = câble connecté, signal présent
- **Deuxième "up"** : état du protocole (Layer 2) = protocole de liaison actif

Tous les autres états indiquent des problèmes.

---

### Question 8
**Réponse correcte :** Router(config-if)# ip address 192.168.1.1 255.255.255.0

**Explication :**
**Syntaxe correcte IPv4** :
```
Router(config)# interface g0/0
Router(config-if)# ip address [adresse-IP] [masque]
Router(config-if)# no shutdown
```

**Exemple** :
```
Router(config-if)# ip address 192.168.1.1 255.255.255.0
```

⚠️ Le masque est en **notation décimale**, pas en notation CIDR (/24).

---

### Question 9 ⚠️ **IMPORTANT**
**Réponse correcte :** Router(config)# ipv6 unicast-routing

**Explication :**
La commande `ipv6 unicast-routing` est **OBLIGATOIRE** pour :
- ✅ Activer le **routage IPv6** sur le routeur
- ✅ Permettre au routeur de **router les paquets IPv6**
- ✅ Activer l'envoi des **Router Advertisements (RA)**

**Sans cette commande, le routeur ne routera pas IPv6**, même si les interfaces ont des adresses IPv6 configurées.

```
Router(config)# ipv6 unicast-routing
Router(config)# interface g0/0
Router(config-if)# ipv6 address 2001:db8:acad:1::1/64
Router(config-if)# no shutdown
```

---

### Question 10
**Réponse correcte :** Router(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64

**Explication :**
**Auto-configuration avec EUI-64** :

```
Router(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
```

L'**Interface ID** (64 bits de poids faible) est généré automatiquement :
1. Prendre l'adresse MAC (48 bits) : `00:1A:2B:3C:4D:5E`
2. Insérer `FFFE` au milieu : `00:1A:2B:FF:FE:3C:4D:5E`
3. Inverser le 7e bit : `02:1A:2B:FF:FE:3C:4D:5E`
4. Adresse complète : `2001:db8:acad:1:021A:2BFF:FE3C:4D5E`

---

### Question 11 ⚠️ **IMPORTANT**
**Réponse correcte :** FE80::/10

**Explication :**
**Plages d'adresses IPv6** :

| Plage | Type |
|-------|------|
| **FE80::/10** | **Link-Local** (commence par FE80, FE90, FEA0, FEB0) |
| **FC00::/7** | Unique Local (privées) |
| **FF00::/8** | Multicast |
| **2000::/3** | Global Unicast (Internet) |
| **::1/128** | Loopback |

**Point clé** : Les adresses link-local commencent toujours par **FE80** en pratique.

---

### Question 12 ⚠️ **IMPORTANT**
**Réponse correcte :** Router(config-if)# ipv6 address fe80::1 link-local

**Explication :**
**Configuration manuelle d'une adresse link-local** :

```
Router(config)# interface g0/0
Router(config-if)# ipv6 address 2001:db8:acad:1::1/64
Router(config-if)# ipv6 address fe80::1 link-local
Router(config-if)# no shutdown
```

**Avantages** :
- ✅ Adresses **simples et mémorisables** : `fe80::1`, `fe80::2`, `fe80::3`
- ✅ **Cohérence** sur toutes les interfaces
- ✅ Facilite le **dépannage** et la **documentation**
- ✅ Utilisée comme **passerelle par défaut** des clients

**⚠️ Important** : Le mot-clé `link-local` est **obligatoire** pour une configuration manuelle.

---

### Question 13 ⚠️ **IMPORTANT**
**Réponses correctes :** Utilisée comme passerelle par défaut pour les clients, Utilisée pour la communication entre voisins sur le même lien, Utilisée par les protocoles de routage (OSPF, EIGRP)

**Explication :**
**Utilisations des adresses IPv6 Link-Local** :

✅ **Passerelle par défaut** : les clients utilisent l'adresse link-local du routeur
```
PC> ipconfig
Default Gateway: fe80::1
```

✅ **Communication locale** : entre périphériques sur le même segment réseau

✅ **Protocoles de routage** : OSPF, EIGRP utilisent les link-local pour les voisinages

❌ **NON routable** : les adresses link-local ne traversent **jamais** les routeurs

❌ **Ne remplacent PAS** : les adresses globales sont toujours nécessaires pour Internet

---

### Question 14
**Réponse correcte :** On insère FFFE au milieu et on inverse le 7e bit

**Explication :**
**Processus EUI-64** :

1. **Adresse MAC** (48 bits) : `00:1A:2B:3C:4D:5E`

2. **Séparer en deux** : `00:1A:2B` | `3C:4D:5E`

3. **Insérer FFFE** : `00:1A:2B:FF:FE:3C:4D:5E`

4. **Inverser le 7e bit** (bit U/L) :
   - `00` en binaire = `00000000`
   - Inverser le 7e bit = `00000010`
   - `02` en hexa
   - Résultat : `02:1A:2B:FF:FE:3C:4D:5E`

5. **Interface ID** : `021A:2BFF:FE3C:4D5E`

**Objectif** : créer un identifiant unique de 64 bits à partir de l'adresse MAC.

---

### Question 15
**Réponse correcte :** Router# show ip interface brief

**Explication :**
**Commandes de vérification IPv4** :

```
Router# show ip interface brief
```

**Sortie** :
```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     192.168.2.1     YES manual up                    up
Serial0/0/0            10.1.1.1        YES manual up                    up
```

Autres commandes utiles :
- `show ip interface g0/0` : détails d'une interface
- `show running-config` : configuration complète
- `show interfaces` : détails physiques

---

### Question 16
**Réponse correcte :** Router# show ipv6 interface brief

**Explication :**
**Commandes de vérification IPv6** :

```
Router# show ipv6 interface brief
```

**Sortie** :
```
GigabitEthernet0/0     [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
GigabitEthernet0/1     [up/up]
    FE80::1
    2001:DB8:ACAD:2::1
```

Autres commandes :
- `show ipv6 interface g0/0` : détails complets
- `show ipv6 route` : table de routage IPv6
- `show ipv6 neighbors` : cache NDP

---

### Question 17
**Réponse correcte :** Router(config)# ip route 0.0.0.0 0.0.0.0 [next-hop]

**Explication :**
**Route statique par défaut IPv4** :

```
Router(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

- **0.0.0.0** : réseau de destination (tous)
- **0.0.0.0** : masque (tous)
- **203.0.113.2** : next-hop (généralement l'ISP)

**IPv6** :
```
Router(config)# ipv6 route ::/0 2001:db8:acad:2::2
```

---

### Question 18 ⚠️ **IMPORTANT**
**Réponse correcte :** L'interface de sortie

**Explication :**
Quand on utilise une **adresse link-local** comme next-hop en IPv6, il **faut spécifier l'interface de sortie** :

```
Router(config)# ipv6 route 2001:db8:acad:3::/64 serial 0/0/0 fe80::2
```

**Pourquoi ?**
Les adresses link-local ne sont valides que sur **un seul lien**. Le routeur a besoin de savoir **quelle interface** utiliser car la même adresse link-local peut exister sur plusieurs liens différents.

**Syntaxe correcte** :
```
Router(config)# ipv6 route [réseau] [interface-sortie] [next-hop-link-local]
```

**Avec adresse globale** (interface optionnelle) :
```
Router(config)# ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2
```

---

### Question 19
**Réponses correctes :** copy running-config startup-config, copy run start, write

**Explication :**
**Commandes de sauvegarde** (toutes équivalentes) :

```
Router# copy running-config startup-config
Router# copy run start
Router# write
Router# write memory
```

Ces commandes copient la configuration en RAM (running-config) vers la NVRAM (startup-config). Sans sauvegarde, les modifications sont perdues au redémarrage.

---

### Question 20
**Réponse correcte :** Router# erase startup-config

**Explication :**
**Effacer la configuration** :

```
Router# erase startup-config
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
```

**Équivalent** :
```
Router# write erase
```

**Après effacement** :
```
Router# reload
System configuration has been modified. Save? [yes/no]: no
```

Le routeur redémarre avec la configuration par défaut (vierge).
