# Module 1 : Packet Forwarding
**CCNP ENCOR v8 - Acheminement des paquets**

---

## 📋 Vue d'ensemble du module

### Objectifs du module
Ce module couvre les fondamentaux de l'acheminement des paquets dans les réseaux d'entreprise, tant au niveau de la couche 2 (commutation) qu'au niveau de la couche 3 (routage). Il s'agit de la base essentielle pour comprendre comment les données transitent dans un réseau.

### Thèmes principaux
1. **Communication des périphériques réseau**
   - Acheminement au niveau Layer 2 (Switches)
   - Acheminement au niveau Layer 3 (Routers)
   - Domaines de collision et de broadcast
   
2. **Architectures d'acheminement**
   - Mécanismes de transfert des routeurs et switches
   - Tables CAM, TCAM, FIB
   - Process switching vs Fast switching vs CEF

---

## 🔌 Communication des périphériques réseau

### Fonction primaire d'un réseau

Le rôle principal d'un réseau est de **fournir de la connectivité entre les périphériques**.

**Protocoles dominants :**
- Aujourd'hui, pratiquement tout est basé sur **TCP/IP** (Transmission Control Protocol/Internet Protocol)
- TCP/IP s'appuie sur le modèle **OSI** (Open Systems Interconnection) à 7 couches

### Modèle OSI - Rappel

| Couche | Nom | Fonction principale | Protocoles/Technologies |
|--------|-----|---------------------|------------------------|
| 7 | Application | Interface utilisateur | HTTP, FTP, DNS, SMTP |
| 6 | Présentation | Format et chiffrement | SSL/TLS, JPEG, ASCII |
| 5 | Session | Gestion des sessions | NetBIOS, RPC |
| 4 | Transport | Segmentation et fiabilité | TCP, UDP |
| 3 | Réseau | Routage et adressage logique | IP, ICMP, OSPF, BGP |
| 2 | Liaison de données | Adressage physique, trames | Ethernet, PPP, STP |
| 1 | Physique | Transmission de bits | Câbles, connecteurs, signaux |

**💡 Point clé :** Le modèle OSI fournit une référence pour comprendre comment les données sont traitées à chaque niveau du réseau.

---

## 🔄 Acheminement de couche 2 (Layer 2 Forwarding)

### Rôle de la couche liaison de données

La couche liaison de données gère **l'adressage sous la pile de protocoles IP** pour que la communication soit dirigée entre les hôtes.

**Technologies de couche 2 :**
- **Ethernet** : Utilise les adresses MAC (Media Access Control)
- **Frame Relay** : Utilise des DLCI (Data Link Connection Identifier)
- **PPP** : Point-to-Point Protocol
- **HDLC** : High-Level Data Link Control

**Focus du cours :** Ethernet et adresses MAC

### Adresses MAC (Media Access Control)

**Structure :**
- Longueur : **48 bits** (6 octets)
- Format : `XX:XX:XX:XX:XX:XX` (hexadécimal)
- Première moitié (24 bits) : **OUI** (Organizationally Unique Identifier) - Identifie le fabricant
- Deuxième moitié (24 bits) : Identifiant unique attribué par le fabricant

**Exemple :**
```
00:1A:2B:3C:4D:5E
^^^^^^^  ^^^^^^^^
  OUI      Device Unique ID
```

**Types d'adresses MAC :**
- **Unicast** : Adresse d'un seul périphérique (bit I/G = 0)
- **Multicast** : Groupe de périphériques (bit I/G = 1)
- **Broadcast** : Tous les périphériques du segment (`FF:FF:FF:FF:FF:FF`)

### Domaines de collision (Collision Domains)

**Définition :** Zone du réseau où les collisions de paquets peuvent se produire.

#### CSMA/CD (Carrier Sense Multiple Access/Collision Detect)

Les périphériques Ethernet utilisent CSMA/CD pour garantir qu'**un seul périphérique parle à la fois** dans un domaine de collision.

**Fonctionnement :**
1. **Carrier Sense** : Écouter le support avant de transmettre
2. **Multiple Access** : Plusieurs périphériques peuvent accéder au support
3. **Collision Detect** : Détection de collision et retransmission

**Limitations :**
- Les périphériques ne peuvent que **transmettre OU recevoir** (half-duplex)
- Plus il y a de périphériques, plus il y a de collisions
- Réduction des performances

#### Hub vs Switch - Impact sur les domaines de collision

**Hub (Répéteur multiport) :**
- Crée un **seul grand domaine de collision**
- Tous les ports partagent la même bande passante
- Fonctionne en **half-duplex**
- 🚫 Obsolète aujourd'hui

**Switch :**
- Crée un **domaine de collision par port**
- Chaque port a sa propre bande passante dédiée
- Fonctionne en **full-duplex** (transmission et réception simultanées)
- ✅ Standard actuel

```
Hub :                          Switch :
[PC1]--\                      [PC1]---- [Switch] ----[PC2]
[PC2]---|[HUB]|                 |                      |
[PC3]--/                      Domaine 1           Domaine 2
   |
Un seul domaine de collision
```

**💡 Point clé :** Les switches augmentent considérablement les performances en créant des domaines de collision individuels et en permettant le full-duplex.

---

## 📡 Domaines de broadcast (Broadcast Domains)

### Trafic de broadcast

**Définition :** Trafic réseau destiné à **tous les hôtes** du réseau local (LAN).

**Caractéristiques :**
- Adresse MAC de destination : `FF:FF:FF:FF:FF:FF`
- Adresse IP de broadcast : Dernière adresse du sous-réseau (ex: `192.168.1.255/24`)
- Transféré sur **tous les ports du switch**

### Unknown Unicast Flooding

Lorsqu'un switch reçoit une trame avec une **adresse MAC de destination inconnue** (pas dans sa table MAC), il effectue un **flooding** :
- La trame est envoyée sur **tous les ports** (sauf le port source)
- Comportement similaire au broadcast
- Le switch apprend l'adresse MAC source

### Limites des broadcasts

**Problème :** Dans un grand LAN, trop de broadcasts peuvent :
- Consommer de la bande passante
- Surcharger les CPUs des hôtes
- Créer des "broadcast storms"

**Solution :** Segmenter le réseau avec des **routeurs** ou **VLANs**

**💡 Point clé :** Les broadcasts **ne traversent PAS** les frontières de couche 3 (d'un sous-réseau à un autre).

---

## 🏢 VLANs (Virtual LANs)

### Concept des VLANs

**Définition :** Les VLANs fournissent une **segmentation logique** en créant plusieurs domaines de broadcast sur le même switch physique.

**Avantages :**
- ✅ Meilleure utilisation des ports
- ✅ Sécurité accrue (isolation du trafic)
- ✅ Réduction du trafic de broadcast
- ✅ Gestion simplifiée
- ✅ Flexibilité (déplacement d'utilisateurs sans recâblage)

### Standard 802.1Q

Les VLANs sont définis dans le standard **IEEE 802.1Q**.

**Tag 802.1Q :** 32 bits ajoutés à la trame Ethernet

| Champ | Taille | Description |
|-------|--------|-------------|
| **TPID** | 16 bits | Tag Protocol Identifier (valeur : 0x8100) |
| **PCP** | 3 bits | Priority Code Point (QoS) |
| **DEI** | 1 bit | Drop Eligible Indicator |
| **VLAN ID** | 12 bits | Identifiant du VLAN (1-4094) |

**Plage de VLANs :**
- **Standard** : 1-1005
- **Extended** : 1006-4094
- **Réservés** : VLAN 1 (natif par défaut), VLAN 1002-1005 (Token Ring, FDDI)

### Configuration des VLANs sur Catalyst

#### Création d'un VLAN

```cisco
! Mode de configuration globale
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name ENGINEERING
Switch(config-vlan)# exit
```

#### Vérification des VLANs

```cisco
Switch# show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- ------------------------
1    default                          active    Gi0/1, Gi0/2, Gi0/3
10   SALES                            active    Gi0/4, Gi0/5
20   ENGINEERING                      active    Gi0/6, Gi0/7
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
```

**Options de la commande `show vlan` :**
- `show vlan brief` : Affiche uniquement les mappings port-VLAN pertinents
- `show vlan summary` : Affiche le nombre de VLANs, VTP, et VLANs étendus
- `show vlan id 10` : Filtre par numéro de VLAN
- `show vlan name SALES` : Filtre par nom de VLAN

**Sortie complète de `show vlan` :**
1. **Section 1** : Mappings VLAN-vers-ports
2. **Section 2** : MTU système
3. **Section 3** : Sessions SPAN
4. **Section 4** : VLANs privés

---

## 🔌 Ports d'accès (Access Ports)

### Caractéristiques

**Définition :** Port assigné à **un seul VLAN**.

**Utilisation typique :**
- Connexion d'hôtes finaux (PCs, imprimantes, téléphones)
- Trafic non-tagué (sans 802.1Q)

### Configuration

```cisco
! Configurer le port en mode access
Switch(config)# interface GigabitEthernet0/4
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# description PC Sales Department
Switch(config-if)# exit
```

**💡 Point clé :** Par défaut, tous les ports des switches Catalyst sont des **ports de couche 2** en mode access dans le VLAN 1.

### Vérification

```cisco
Switch# show interfaces GigabitEthernet0/4 switchport
Name: Gi0/4
Switchport: Enabled
Administrative Mode: access
Operational Mode: access
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
Access Mode VLAN: 10 (SALES)
Trunking Native Mode VLAN: 1 (default)
...
```

---

## 🌉 Ports trunk (Trunk Ports)

### Concept des trunks

**Définition :** Port capable de transporter le trafic de **plusieurs VLANs** simultanément.

**Utilisation typique :**
- Connexion entre switches
- Connexion switch-routeur (router-on-a-stick)
- Connexion switch-firewall
- Connexion switch-serveur (avec NIC supportant 802.1Q)

### Configuration d'un trunk

```cisco
! Configuration d'un trunk statique
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q  ! Sur certains modèles uniquement
Switch(config-if)# description Trunk to Core-Switch
Switch(config-if)# exit
```

**Note :** Sur les switches modernes (Catalyst 2960, 9300, etc.), l'encapsulation 802.1Q est la seule supportée, donc la commande `switchport trunk encapsulation` n'est pas nécessaire.

### VLAN natif (Native VLAN)

**Définition :** VLAN dont le trafic **n'est pas tagué** sur un trunk 802.1Q.

**Caractéristiques :**
- Par défaut : **VLAN 1**
- Permet l'interopérabilité avec des équipements ne supportant pas 802.1Q
- **Doit être identique des deux côtés du trunk** (best practice)

**Configuration :**

```cisco
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport trunk native vlan 99
```

**⚠️ Avertissement :** Un mauvais alignement du VLAN natif peut causer :
- Changement de VLAN involontaire du trafic
- Problèmes de connectivité
- Failles de sécurité

**Best practice :** Utiliser un VLAN natif dédié et non-utilisé (ex: VLAN 999)

### VLANs autorisés sur un trunk

Par défaut, **tous les VLANs** (1-4094) sont autorisés sur un trunk.

**Limiter les VLANs :**

```cisco
! Autoriser seulement certains VLANs
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport trunk allowed vlan 1,10,20,99

! Ajouter des VLANs à la liste existante
Switch(config-if)# switchport trunk allowed vlan add 30,40

! Retirer des VLANs de la liste
Switch(config-if)# switchport trunk allowed vlan remove 1

! Autoriser tous les VLANs
Switch(config-if)# switchport trunk allowed vlan all

! Interdire tous les VLANs
Switch(config-if)# switchport trunk allowed vlan none

! Autoriser tous SAUF certains VLANs
Switch(config-if)# switchport trunk allowed vlan except 1-10
```

**Avantages de limiter les VLANs :**
- Réduit le trafic de broadcast inutile
- Améliore la sécurité
- Simplifie le dépannage

### Vérification des trunks

```cisco
Switch# show interfaces trunk

Port        Mode         Encapsulation  Status        Native vlan
Gi0/1       on           802.1q         trunking      99

Port        Vlans allowed on trunk
Gi0/1       1,10,20,99

Port        Vlans allowed and active in management domain
Gi0/1       1,10,20,99

Port        Vlans in spanning tree forwarding state and not pruned
Gi0/1       1,10,20,99
```

**Sections de la sortie :**
1. **Première section** : Mode, encapsulation, statut, VLAN natif
2. **Deuxième section** : VLANs autorisés sur le trunk
3. **Troisième section** : VLANs autorisés ET actifs sur le switch
4. **Quatrième section** : VLANs en état forwarding (non bloqués par STP)

**💡 Point clé :** Un VLAN doit être présent dans les 4 sections pour que son trafic traverse effectivement le trunk.

---

## 📊 Table d'adresses MAC (MAC Address Table)

### Rôle de la table MAC

La table MAC est responsable d'**identifier les ports et VLANs** associés à chaque adresse MAC.

**Fonctionnement :**
1. Le switch examine l'**adresse MAC source** des trames reçues
2. Il enregistre : `MAC address → Port → VLAN`
3. Cette information est utilisée pour **l'acheminement intelligent** des trames

**Avantages :**
- Réduit les collisions (communication point-à-point)
- Diminue le flooding d'inconnues
- Améliore les performances

### Apprentissage dynamique

```
Trame reçue sur Port Gi0/4 (VLAN 10) :
Source MAC: 0050.7966.6800
Destination MAC: 0050.7966.6801

Switch enregistre:
MAC: 0050.7966.6800 → Port: Gi0/4 → VLAN: 10
```

### Types d'entrées MAC

| Type | Description | Durée de vie |
|------|-------------|--------------|
| **Dynamic** | Apprises automatiquement | 300 secondes (défaut) |
| **Static** | Configurées manuellement | Permanente |
| **Secure** | Configurées via port-security | Selon config |

### Consultation de la table MAC

```cisco
! Afficher toute la table
Switch# show mac address-table

          Mac Address Table
-------------------------------------------
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  10    0050.7966.6800    DYNAMIC     Gi0/4
  10    0050.7966.6801    DYNAMIC     Gi0/5
  20    0050.7966.6802    DYNAMIC     Gi0/6
  All    0100.0ccc.cccc    STATIC      CPU
  All    0100.0ccc.cccd    STATIC      CPU

! Filtrer par adresse MAC
Switch# show mac address-table address 0050.7966.6800

! Filtrer par VLAN
Switch# show mac address-table vlan 10

! Afficher uniquement les entrées dynamiques
Switch# show mac address-table dynamic

! Filtrer par interface
Switch# show mac address-table interface GigabitEthernet0/4
```

### Configuration statique d'une entrée MAC

```cisco
! Associer une MAC à un port
Switch(config)# mac address-table static 0050.7966.6803 vlan 10 interface Gi0/7

! Bloquer une MAC (drop sur réception)
Switch(config)# mac address-table static 0050.7966.6804 vlan 10 drop
```

**Use case :** Sécuriser des ports sensibles en n'autorisant que des MACs spécifiques.

### Effacement de la table MAC

```cisco
! Effacer toutes les entrées dynamiques
Switch# clear mac address-table dynamic

! Effacer par adresse spécifique
Switch# clear mac address-table dynamic address 0050.7966.6800

! Effacer par interface
Switch# clear mac address-table dynamic interface Gi0/4

! Effacer par VLAN
Switch# clear mac address-table dynamic vlan 10
```

### Aging time (durée de vie)

```cisco
! Modifier le délai d'expiration (en secondes)
Switch(config)# mac address-table aging-time 600

! Vérifier le aging time
Switch# show mac address-table aging-time
Global Aging Time:  600
Vlan    Aging Time
----    ----------
  10       600
```

**Valeur par défaut :** 300 secondes (5 minutes)

**💡 Point clé :** Si aucune trame n'est reçue avec une MAC source pendant le `aging-time`, l'entrée est supprimée de la table.

---

## 💾 CAM (Content Addressable Memory)

### Technologie CAM

La table MAC réside dans une mémoire spéciale appelée **CAM** (Content Addressable Memory).

**Caractéristiques :**
- **Recherche ultra-rapide** : Résultat en un seul cycle d'horloge
- **Recherche binaire** : 0 (faux) ou 1 (vrai)
- **Hardware-based** : Recherches effectuées par l'ASIC, pas le CPU

**Fonctionnement :**
- Recherche parallèle sur toute la mémoire
- Comparaison simultanée avec toutes les entrées
- Retour instantané du résultat

**Avantage :** Beaucoup plus rapide que la RAM standard (qui nécessite une recherche séquentielle).

---

## 🔍 Statut des ports de switch

### Commande `show interfaces status`

Fournit une vue **condensée et simplifiée** de tous les ports.

```cisco
Switch# show interfaces status

Port      Name               Status       Vlan       Duplex  Speed Type
Gi0/1     Trunk-to-Core      connected    trunk      a-full  a-1000 10/100/1000BaseTX
Gi0/2                        notconnect   1          auto    auto   10/100/1000BaseTX
Gi0/3                        err-disabled 1          auto    auto   10/100/1000BaseTX
Gi0/4     PC-Sales           connected    10         a-full  a-100  10/100/1000BaseTX
Gi0/5     Phone-Sales        connected    10         a-full  a-1000 10/100/1000BaseTX
```

**Colonnes importantes :**

| Colonne | Description |
|---------|-------------|
| **Port** | Interface ID ou Port-Channel |
| **Name** | Description configurée (`description`) |
| **Status** | `connected`, `notconnect`, `err-disabled`, `monitoring` |
| **VLAN** | Numéro de VLAN (access), `trunk`, `routed` (L3) |
| **Duplex** | `full`, `half`, `auto`, ou `a-full` (auto-négocié) |
| **Speed** | `10`, `100`, `1000`, `10G`, ou préfixé `a-` si auto-négocié |
| **Type** | Type d'interface (RJ-45, SFP, SFP+) |

**États de status :**
- **connected** : Liaison établie avec succès
- **notconnect** : Pas de liaison détectée (câble débranché, hôte éteint)
- **err-disabled** : Erreur détectée, port désactivé automatiquement
- **monitoring** : Port en mode SPAN (miroir)

### Commande `show interfaces switchport`

Fournit des **détails complets** sur la configuration de commutation d'un port.

```cisco
Switch# show interfaces GigabitEthernet0/4 switchport
Name: Gi0/4
Switchport: Enabled
Administrative Mode: access
Operational Mode: access
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
Access Mode VLAN: 10 (SALES)
Trunking Native Mode VLAN: 1 (default)
Administrative Native VLAN tagging: enabled
Voice VLAN: none
Trunking VLANs Enabled: ALL
Pruning VLANs Enabled: 2-1001
...
```

**Informations clés :**
- **Switchport** : Enabled/Disabled (port L2 ou L3)
- **Administrative Mode** : Configuration voulue (access, trunk, dynamic)
- **Operational Mode** : État réel (access, trunk)
- **Access Mode VLAN** : VLAN assigné en mode access
- **Trunking Native VLAN** : VLAN natif du trunk

**💡 Point clé :** La commande `show interfaces switchport` révèle la configuration effective, qui peut différer de celle configurée en raison de priorités ou de protocoles (DTP, VTP).

---

## 🌐 Acheminement de couche 3 (Layer 3 Forwarding)

### Principes de base

Une partie de la logique d'acheminement de couche 3 **précède** l'acheminement de couche 2.

**Deux méthodologies principales :**
1. **Acheminement local** : Communication entre périphériques du **même sous-réseau**
2. **Routage** : Communication entre périphériques de **sous-réseaux différents**

### Acheminement réseau local (Local Network Forwarding)

**Scénario :** PC1 (192.168.10.5/24) veut communiquer avec PC2 (192.168.10.6/24).

**Processus :**
1. PC1 détermine que 192.168.10.6 est sur le **même sous-réseau**
2. PC1 connaît l'adresse IP de destination mais **pas la MAC**
3. PC1 consulte sa **table ARP**
   - Si l'entrée existe : Utiliser la MAC
   - Si l'entrée n'existe pas : Envoyer une **requête ARP**
4. PC1 reçoit une réponse ARP avec la MAC de PC2
5. PC1 encapsule la trame avec :
   - MAC source : MAC de PC1
   - MAC destination : MAC de PC2
   - IP source : 192.168.10.5
   - IP destination : 192.168.10.6

### Protocole ARP (Address Resolution Protocol)

**Fonction :** Mapper les **adresses IP de couche 3** aux **adresses MAC de couche 2**.

**Fonctionnement :**

1. **Requête ARP** (ARP Request) :
   - Type : Broadcast (FF:FF:FF:FF:FF:FF)
   - Message : "Qui a l'adresse IP 192.168.10.6 ? Dites-le à 192.168.10.5"
   
2. **Réponse ARP** (ARP Reply) :
   - Type : Unicast (vers l'adresse MAC du demandeur)
   - Message : "192.168.10.6 est à l'adresse MAC 00:50:79:66:68:01"

**Table ARP :**
```
IP Address       MAC Address       Age (min)   Interface
192.168.10.1     0050.7966.6800    5           Vlan10
192.168.10.6     0050.7966.6801    1           Vlan10
192.168.10.10    0050.7966.6802    3           Vlan10
```

### Consultation de la table ARP sur un routeur

```cisco
Router# show ip arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  192.168.10.1     -          0050.7966.6800  ARPA   GigabitEthernet0/0
Internet  192.168.10.5     5          0050.7966.6801  ARPA   GigabitEthernet0/0
Internet  192.168.10.6     2          0050.7966.6802  ARPA   GigabitEthernet0/0

! Filtrer par adresse MAC
Router# show ip arp 0050.7966.6801

! Filtrer par adresse IP
Router# show ip arp 192.168.10.5

! Filtrer par VLAN
Router# show ip arp vlan 10

! Filtrer par interface
Router# show ip arp GigabitEthernet0/0
```

### Effacement de la table ARP

```cisco
! Effacer toute la table ARP
Router# clear ip arp

! Effacer une entrée spécifique
Router# clear ip arp 192.168.10.5
```

**💡 Point clé :** Contrairement à la table MAC qui est gérée automatiquement, la table ARP peut nécessiter un effacement manuel lors du dépannage.

---

## 🛣️ Routage de paquets (Packet Routing)

### Quand router un paquet ?

Un paquet doit être **routé** lorsque la source et la destination sont sur des **réseaux différents**.

**Exemple :** PC1 (192.168.10.5/24) veut communiquer avec Serveur1 (192.168.20.10/24).

### Processus de routage

**Étape 1 : Détermination de la passerelle (Gateway)**

Le périphérique source détecte que la destination est sur un réseau différent. Il consulte sa **table de routage locale** :
- Route statique configurée
- Route par défaut (default gateway)
- Routes apprises par un protocole de routage (si c'est un routeur)

**Étape 2 : Résolution ARP du next-hop**

Le périphérique connaît l'**adresse IP du prochain saut** (next-hop), mais il a besoin de la **MAC address** pour encapsuler la trame de couche 2.
- Consulte la table ARP pour l'IP du next-hop
- Si absente, envoie une requête ARP pour le next-hop

**Étape 3 : Encapsulation de la trame**

```
Trame Ethernet :
├─ MAC source : MAC de PC1
├─ MAC destination : MAC du routeur (default gateway)
└─ Paquet IP :
   ├─ IP source : 192.168.10.5
   └─ IP destination : 192.168.20.10
```

**💡 Point clé :** Les adresses IP **ne changent pas** lors du routage, mais les adresses MAC **changent à chaque saut**.

### Routage sur le routeur

**Étape 1 : Réception de la trame**

Le routeur reçoit la trame parce que la MAC de destination correspond à son interface.

**Étape 2 : Décapsulation**

Le routeur retire l'en-tête Ethernet et examine le paquet IP.

**Étape 3 : Consultation de la table de routage**

```cisco
Router# show ip route
...
S    192.168.20.0/24 [1/0] via 10.0.0.2
```

Le routeur trouve une correspondance : le réseau 192.168.20.0/24 est accessible via 10.0.0.2 (prochain routeur).

**Étape 4 : TTL (Time To Live)**

Le routeur **décrémente le TTL** de 1.
- Si TTL = 0 : Drop du paquet + envoi d'un message ICMP "Time Exceeded"
- Si TTL > 0 : Continue le routage

**Étape 5 : Résolution ARP du prochain saut**

Le routeur vérifie sa table ARP pour l'adresse IP 10.0.0.2. Si absente, il envoie une requête ARP.

**Étape 6 : Réencapsulation**

```
Nouvelle trame Ethernet :
├─ MAC source : MAC de l'interface de sortie du routeur (Gi0/1)
├─ MAC destination : MAC du routeur suivant (10.0.0.2)
└─ Paquet IP :
   ├─ IP source : 192.168.10.5 (inchangée)
   └─ IP destination : 192.168.20.10 (inchangée)
```

**💡 Point clé :** À chaque saut, les adresses MAC sont modifiées, mais les adresses IP restent identiques.

---

## 🎯 Attribution d'adresses IP

### Interfaces IPv4

Pour qu'un routeur ou switch multicouche puisse router des paquets, il doit avoir une **adresse IP configurée** sur l'interface.

```cisco
! Configuration d'une adresse IP sur une interface
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

**Résultat :**
- Le réseau 192.168.10.0/24 est injecté dans la **table de routage**
- Le routeur peut maintenant router le trafic pour ce réseau
- La route est de type **Connected** avec une distance administrative (AD) de **0**

### Adresses IPv4 secondaires

Il est possible d'attacher **plusieurs réseaux IPv4** à la même interface.

```cisco
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# ip address 192.168.11.1 255.255.255.0 secondary
Router(config-if)# exit
```

**Use case :**
- Migration de réseau (ancien et nouveau sous-réseau coexistent temporairement)
- Pas assez d'interfaces physiques disponibles

**⚠️ Limitation :** Tous les hôtes du même segment peuvent communiquer en couche 2, contournant potentiellement les politiques de sécurité.

### Interfaces IPv6

```cisco
! Configuration d'une adresse IPv6
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ipv6 address 2001:DB8:ACAD:10::1/64
Router(config-if)# no shutdown
Router(config-if)# exit

! Activer le routage IPv6 (obligatoire)
Router(config)# ipv6 unicast-routing
```

**💡 Point clé :** Contrairement à IPv4, IPv6 permet d'avoir **plusieurs adresses sur la même interface** sans le mot-clé `secondary`.

---

## 🔀 Sous-interfaces routées (Routed Subinterfaces)

### Concept de Router-on-a-Stick

**Problème :** Un routeur avec peu d'interfaces physiques doit router entre plusieurs VLANs.

**Solution :** Utiliser des **sous-interfaces logiques** sur une seule interface physique.

### Configuration

```cisco
! Configuration du switch (trunk vers le routeur)
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit

! Configuration du routeur
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config-if)# exit

! Sous-interface pour VLAN 10
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

! Sous-interface pour VLAN 20
Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

! Sous-interface pour VLAN 30
Router(config)# interface GigabitEthernet0/0.30
Router(config-subif)# encapsulation dot1q 30
Router(config-subif)# ip address 192.168.30.1 255.255.255.0
Router(config-subif)# exit
```

**Syntaxe des sous-interfaces :**
- Format : `interface.subinterface-number`
- Exemple : `GigabitEthernet0/0.10`
- Le numéro de sous-interface **devrait correspondre** au numéro de VLAN (best practice, pas obligatoire)

**Commande clé :**
```cisco
encapsulation dot1q vlan-id
```
- Associe la sous-interface à un VLAN spécifique
- Nécessaire pour que le routeur sache quel tag 802.1Q traiter

### Vérification

```cisco
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     unassigned      YES unset  up                    up
GigabitEthernet0/0.10  192.168.10.1    YES manual up                    up
GigabitEthernet0/0.20  192.168.20.1    YES manual up                    up
GigabitEthernet0/0.30  192.168.30.1    YES manual up                    up
```

**💡 Point clé :** L'interface physique doit être en état `up/up` pour que les sous-interfaces fonctionnent.

---

## 🌐 SVIs (Switched Virtual Interfaces)

### Concept de SVI

**Définition :** Interface virtuelle associée à un VLAN sur un switch multicouche.

**Avantages :**
- Router entre VLANs **sans routeur externe**
- Gestion à distance du switch (via IP)
- Performances accrues (routage hardware)

### Configuration d'une SVI

```cisco
! Étape 1 : Créer le VLAN (si pas déjà fait)
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config-vlan)# exit

! Étape 2 : Créer l'interface VLAN (SVI)
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

! Étape 3 : Assigner des ports au VLAN
Switch(config)# interface range GigabitEthernet0/2-10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
```

### Conditions pour qu'une SVI soit `up/up`

1. Le **VLAN doit exister** dans la base VLAN
2. Au moins **une interface physique** doit être :
   - Assignée au VLAN
   - En état `up/up`
3. La SVI doit être configurée avec `no shutdown`

### Exemple avec routage inter-VLAN

```cisco
! VLAN 10 - 192.168.10.0/24
Switch(config)# vlan 10
Switch(config-vlan)# exit
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

! VLAN 20 - 192.168.20.0/24
Switch(config)# vlan 20
Switch(config-vlan)# exit
Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

! Activer le routage IP
Switch(config)# ip routing
```

**Vérification :**

```cisco
Switch# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
Vlan10                 192.168.10.1    YES manual up                    up
Vlan20                 192.168.20.1    YES manual up                    up

Switch# show ip route
...
C    192.168.10.0/24 is directly connected, Vlan10
L    192.168.10.1/32 is directly connected, Vlan10
C    192.168.20.0/24 is directly connected, Vlan20
L    192.168.20.1/32 is directly connected, Vlan20
```

**💡 Point clé :** Les SVIs permettent le routage inter-VLAN **hardware-based**, bien plus rapide que le router-on-a-stick.

---

## 🚀 Architectures d'acheminement (Forwarding Architectures)

### Évolution des méthodes d'acheminement

| Méthode | Description | Performance | Utilisation CPU |
|---------|-------------|-------------|-----------------|
| **Process Switching** | CPU traite chaque paquet | Très lente | Très élevée |
| **Fast Switching** | Cache des décisions de routage | Moyenne | Moyenne |
| **CEF** | Table pré-calculée (hardware) | Très rapide | Très faible |

### Process Switching (Routage par processus)

**Fonctionnement :**
1. Le routeur reçoit un paquet
2. Le CPU examine l'en-tête du paquet
3. Consulte la table de routage
4. Effectue la recherche complète
5. Prend la décision de routage
6. Transfère le paquet

**Problème :** Chaque paquet nécessite une recherche complète dans la table de routage, sollicitant intensivement le CPU.

**💡 Point clé :** Process Switching est obsolète sur les équipements modernes, utilisé uniquement pour des cas spéciaux (premier paquet, paquetsavec options IP).

### Fast Switching (Route Caching)

**Optimisation :** Mettre en cache les décisions de routage précédentes.

**Fonctionnement :**
1. Premier paquet : Process Switching (recherche complète)
2. Décision mise en **cache**
3. Paquets suivants vers la même destination : Utilisation du cache

**Avantages :**
- Réduit la charge CPU
- Améliore les performances

**Limitations :**
- Cache limité en taille
- Peut devenir obsolète (changement de topologie)
- Pas optimal pour les grands réseaux

### CEF (Cisco Express Forwarding)

**Définition :** Architecture de commutation avancée qui utilise des **tables pré-calculées** stockées dans du matériel dédié (ASIC/TCAM).

**Composants de CEF :**

1. **FIB (Forwarding Information Base)** :
   - Copie optimisée de la table de routage IP
   - Contient les next-hops et interfaces de sortie
   - Mise à jour en temps réel quand la RIB change

2. **Adjacency Table** :
   - Informations de couche 2 (adresses MAC)
   - Associe les next-hops IP à leurs adresses MAC
   - Permet la réécriture rapide des en-têtes Ethernet

**Fonctionnement :**
1. Le paquet arrive
2. L'ASIC consulte la **FIB** pour trouver la route
3. L'ASIC consulte l'**Adjacency Table** pour les infos L2
4. L'ASIC réécrit les en-têtes et transfère le paquet
5. **Sans solliciter le CPU**

**Avantages :**
- ✅ Performances maximales (wire-speed)
- ✅ CPU libéré pour les tâches de contrôle
- ✅ Scalabilité élevée
- ✅ Déterministe (latence constante)

### Activation de CEF

```cisco
! CEF activé par défaut sur les équipements modernes
Router# show ip cef
Prefix              Next Hop             Interface
0.0.0.0/0           10.0.0.2             GigabitEthernet0/1
10.0.0.0/24         attached             GigabitEthernet0/1
192.168.10.0/24     attached             GigabitEthernet0/0
192.168.20.0/24     10.0.0.2             GigabitEthernet0/1

! Vérifier que CEF est activé
Router# show cef state
CEF Status: enabled
```

**💡 Point clé :** CEF est l'architecture par défaut sur tous les routeurs et switches Cisco modernes. Il n'est généralement pas nécessaire de le configurer manuellement.

---

## 📚 Résumé des concepts clés

### Couche 2 (Commutation)
- **Adresses MAC** : 48 bits, identifient les périphériques au niveau liaison
- **Switches** : Créent un domaine de collision par port, apprennent les MACs dynamiquement
- **Table CAM** : Mémoire ultra-rapide pour les lookups MAC
- **VLANs** : Segmentation logique, domaines de broadcast séparés
- **Trunks 802.1Q** : Transportent plusieurs VLANs, utilisent le tagging
- **VLAN natif** : Trafic non-tagué sur un trunk

### Couche 3 (Routage)
- **Routage local** : ARP pour mapper IP → MAC sur le même sous-réseau
- **Routage inter-réseau** : Table de routage + ARP pour le next-hop
- **TTL** : Décrémenté à chaque saut, empêche les boucles
- **Sous-interfaces** : Router-on-a-stick pour routage inter-VLAN
- **SVIs** : Interfaces VLAN sur switches multicouches

### Architectures d'acheminement
- **Process Switching** : CPU traite chaque paquet (obsolète)
- **Fast Switching** : Cache des décisions (legacy)
- **CEF** : Tables pré-calculées (FIB + Adjacency), hardware-based (standard actuel)

---

## 🎓 Points à retenir absolument

1. ✅ Un switch crée un domaine de collision par port, un hub crée un seul grand domaine
2. ✅ Les broadcasts ne traversent pas les routeurs (frontières L3)
3. ✅ Les VLANs segmentent logiquement un réseau en domaines de broadcast séparés
4. ✅ Un trunk 802.1Q peut transporter plusieurs VLANs, le VLAN natif n'est pas tagué
5. ✅ La table MAC associe : MAC address → Port → VLAN
6. ✅ ARP mappe les adresses IP aux adresses MAC pour le forwarding local
7. ✅ Les adresses IP restent constantes lors du routage, mais les MACs changent à chaque saut
8. ✅ Les SVIs permettent le routage inter-VLAN sur un switch multicouche
9. ✅ CEF (FIB + Adjacency Table) est l'architecture de forwarding moderne et performante
10. ✅ Le TTL empêche les boucles de routage en limitant le nombre de sauts

---

**Module suivant :** [Module 2 - Spanning Tree Protocol](Module-02-notes.md)
