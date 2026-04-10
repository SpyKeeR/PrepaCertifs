# QCM Checkpoint - Modules 8-10 : Communication entre les réseaux

## Informations générales

**Modules couverts :**
- Module 8 : Couche Réseau (Network Layer)
- Module 9 : Résolution d'adresse (ARP et NDP)
- Module 10 : Configuration de base d'un routeur

**Nombre de questions :** 30
**Durée estimée :** 45 minutes
**Seuil de réussite :** 75% (23/30 questions correctes)
**Format :** Choix unique et choix multiples

---

## Instructions

- Certaines questions ont **une seule réponse correcte**
- D'autres ont **plusieurs réponses correctes** (indiqué dans l'énoncé)
- Prenez le temps de bien lire chaque question
- Les réponses et explications sont à la fin du document

---

## Question 1
Lors du routage d'un paquet entre deux réseaux distants, que se passe-t-il avec les adresses IP et MAC à chaque saut ?

- [ ] Les adresses IP et MAC restent identiques
- [ ] Les adresses IP et MAC changent à chaque saut
- [ ] Les adresses IP restent identiques, les adresses MAC changent
- [ ] Les adresses MAC restent identiques, les adresses IP changent

---

## Question 2 ⚠️ **NDP - PRIORITÉ**
Un hôte IPv6 vient de se connecter au réseau et souhaite obtenir automatiquement sa configuration réseau. Quel message ICMPv6 NDP va-t-il envoyer en premier ?

- [ ] Type 134 - Router Advertisement (RA)
- [ ] Type 133 - Router Solicitation (RS)
- [ ] Type 135 - Neighbor Solicitation (NS)
- [ ] Type 136 - Neighbor Advertisement (NA)

---

## Question 3
**Sélectionnez DEUX réponses correctes.**

Dans une table de routage Cisco, quels codes indiquent des routes configurées manuellement par l'administrateur ou apprises dynamiquement ?

- [ ] C = Connected (réseau directement connecté)
- [ ] S = Static (route statique)
- [ ] L = Local (adresse locale de l'interface)
- [ ] O = OSPF (route apprise via OSPF)
- [ ] D = EIGRP (route apprise via EIGRP)

---

## Question 4
Un routeur Cisco IPv6 a été configuré avec une adresse globale sur l'interface G0/0, mais les clients du réseau ne peuvent pas envoyer de paquets vers Internet. Quelle est la cause la plus probable ?

- [ ] L'interface n'a pas de commande "no shutdown"
- [ ] La commande "ipv6 unicast-routing" n'a pas été configurée
- [ ] L'adresse link-local n'a pas été configurée manuellement
- [ ] Le routeur ne supporte pas IPv6

---

## Question 5 ⚠️ **LINK-LOCAL - FOCUS**
**Sélectionnez TROIS réponses correctes.**

Quelles affirmations concernant les adresses IPv6 link-local sont vraies ?

- [ ] Elles commencent par FE80::/10
- [ ] Elles sont routables sur Internet
- [ ] Elles sont utilisées comme passerelle par défaut
- [ ] Elles sont générées automatiquement avec EUI-64
- [ ] Elles sont uniquement valides sur le lien local

---

## Question 6
Quel est le champ de l'entête IPv4 qui indique le protocole de couche supérieure encapsulé (ex: TCP, UDP, ICMP) ?

- [ ] Type of Service (ToS)
- [ ] Protocol
- [ ] Next Header
- [ ] IHL (Internet Header Length)

---

## Question 7 ⚠️ **NDP - PRIORITÉ**
Un hôte IPv6 souhaite vérifier si l'adresse qu'il vient de générer n'est pas déjà utilisée sur le réseau (DAD - Duplicate Address Detection). Quel type de message NDP va-t-il utiliser ?

- [ ] Type 133 - Router Solicitation (RS)
- [ ] Type 134 - Router Advertisement (RA)
- [ ] Type 135 - Neighbor Solicitation (NS)
- [ ] Type 137 - Redirect

---

## Question 8
**Sélectionnez DEUX réponses correctes.**

Quelles commandes permettent de sauvegarder la configuration en cours (running-config) vers la configuration de démarrage (startup-config) ?

- [ ] copy running-config startup-config
- [ ] save configuration
- [ ] write memory
- [ ] copy run start
- [ ] save run start

---

## Question 9
Analysez cette entrée de table de routage :
```
O    10.5.5.0/24 [110/65] via 192.168.1.2, 00:10:23, GigabitEthernet0/1
```
Que signifie la valeur **110** entre crochets ?

- [ ] La métrique de la route (coût)
- [ ] La distance administrative d'OSPF
- [ ] Le temps en secondes depuis l'apprentissage
- [ ] Le nombre de sauts jusqu'au réseau

---

## Question 10
Comparez la taille des entêtes IPv4 et IPv6. Quelle affirmation est correcte ?

- [ ] IPv4 : 20 octets fixes, IPv6 : 40 octets fixes
- [ ] IPv4 : 20-60 octets variables, IPv6 : 40 octets fixes
- [ ] IPv4 : 40 octets fixes, IPv6 : 20-60 octets variables
- [ ] Les deux ont une taille variable selon les options

---

## Question 11 ⚠️ **LINK-LOCAL - FOCUS**
Un administrateur configure une interface de routeur avec les commandes suivantes :
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# no shutdown
```
Pourquoi est-il recommandé de configurer manuellement l'adresse link-local ?

- [ ] C'est obligatoire, sinon l'interface ne fonctionnera pas
- [ ] Pour avoir une adresse simple et mémorisable (FE80::1)
- [ ] Pour éviter les conflits d'adresses sur le réseau
- [ ] L'adresse link-local n'est pas auto-générée sur les routeurs

---

## Question 12 ⚠️ **NDP - PRIORITÉ**
**Sélectionnez DEUX réponses correctes.**

Quels types de messages ICMPv6 NDP sont envoyés par les routeurs IPv6 ?

- [ ] Type 133 - Router Solicitation (RS)
- [ ] Type 134 - Router Advertisement (RA)
- [ ] Type 135 - Neighbor Solicitation (NS)
- [ ] Type 136 - Neighbor Advertisement (NA)
- [ ] Type 137 - Redirect

---

## Question 13
Lors d'une requête ARP, quel est l'opcode utilisé et quelle est l'adresse MAC de destination ?

- [ ] Opcode 1, MAC destination = FF:FF:FF:FF:FF:FF
- [ ] Opcode 2, MAC destination = FF:FF:FF:FF:FF:FF
- [ ] Opcode 1, MAC destination = 00:00:00:00:00:00
- [ ] Opcode 2, MAC destination = adresse MAC du destinataire

---

## Question 14
**Sélectionnez TROIS réponses correctes.**

Quelles valeurs du champ "Protocol" dans l'entête IPv4 sont correctes ?

- [ ] 1 = ICMP
- [ ] 6 = TCP
- [ ] 17 = UDP
- [ ] 58 = ICMPv6
- [ ] 89 = OSPF

---

## Question 15
Un paquet IPv4 avec un champ TTL initial de 128 traverse 15 routeurs. Quelle sera la valeur finale du TTL lorsque le paquet atteint sa destination ?

- [ ] 128
- [ ] 113
- [ ] 15
- [ ] 0

---

## Question 16
Quel est l'avantage principal d'utiliser le multicast au lieu du broadcast pour la résolution d'adresse en IPv6 (NDP) ?

- [ ] Le multicast est plus sécurisé
- [ ] Le multicast réduit la charge réseau en ciblant uniquement les hôtes concernés
- [ ] Le multicast permet de traverser les routeurs
- [ ] Le multicast est plus rapide que le broadcast

---

## Question 17
**Sélectionnez TROIS réponses correctes.**

Quelles étapes sont nécessaires pour configurer SSH sur un routeur Cisco ?

- [ ] Router(config)# ip domain-name example.com
- [ ] Router(config)# crypto key generate rsa modulus 2048
- [ ] Router(config)# ip ssh version 2
- [ ] Router(config)# enable ssh
- [ ] Router(config)# line vty 0 4, puis transport input ssh

---

## Question 18
Quelle est l'adresse IPv6 multicast "solicited-node" utilisée pour résoudre l'adresse 2001:DB8:ACAD:1::A5B3 ?

- [ ] FF02::1:FFA5:B3
- [ ] FF02::1:FF00:A5B3
- [ ] FF02::1:FFAD:A5B3
- [ ] FF02::A5B3

---

## Question 19
Dans une table de routage, quelle distance administrative (AD) est associée aux routes directement connectées ?

- [ ] 0
- [ ] 1
- [ ] 90
- [ ] 110

---

## Question 20
**Sélectionnez DEUX réponses correctes.**

Quelles commandes permettent d'afficher les adresses IPv6 configurées sur les interfaces d'un routeur Cisco ?

- [ ] show ipv6 interface brief
- [ ] show ip interface brief
- [ ] show ipv6 interface g0/0
- [ ] show interface ipv6
- [ ] ipconfig /all

---

## Question 21
Quel champ de l'entête IPv6 est l'équivalent du champ "Protocol" d'IPv4 ?

- [ ] Traffic Class
- [ ] Flow Label
- [ ] Next Header
- [ ] Hop Limit

---

## Question 22
Un hôte IPv6 a reçu un Router Advertisement (RA) avec le flag M=0 et O=0. Quelle méthode d'auto-configuration va-t-il utiliser ?

- [ ] DHCPv6 Stateful (obtenir adresse + options via DHCPv6)
- [ ] DHCPv6 Stateless (obtenir seulement les options via DHCPv6)
- [ ] SLAAC (auto-configuration complète sans DHCPv6)
- [ ] Configuration manuelle uniquement

---

## Question 23
**Sélectionnez DEUX réponses correctes.**

Quelles commandes Cisco IOS permettent d'effacer la table ARP ?

- [ ] clear ip arp
- [ ] clear arp-cache
- [ ] delete arp
- [ ] erase arp
- [ ] no ip arp

---

## Question 24 - SCÉNARIO DE TROUBLESHOOTING
Un administrateur configure une interface de routeur avec les commandes suivantes :
```
R1(config)# interface g0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# description LAN Administratif
```
Après la configuration, la commande `show ip interface brief` affiche :
```
GigabitEthernet0/0  192.168.10.1  YES manual  administratively down  down
```
Quelle est la cause du problème et quelle commande permet de le résoudre ?

- [ ] Problème : câble débranché | Solution : reconnecter le câble
- [ ] Problème : interface désactivée | Solution : no shutdown
- [ ] Problème : mauvaise adresse IP | Solution : changer l'adresse IP
- [ ] Problème : interface non configurée | Solution : interface enable

---

## Question 25
Classez les distances administratives suivantes par ordre croissant (plus fiable → moins fiable) :

Distances à classer : OSPF (110), Static (1), EIGRP (90), RIP (120), Connected (0)

- [ ] Connected (0), Static (1), EIGRP (90), OSPF (110), RIP (120)
- [ ] Static (1), Connected (0), EIGRP (90), OSPF (110), RIP (120)
- [ ] Connected (0), EIGRP (90), Static (1), OSPF (110), RIP (120)
- [ ] RIP (120), OSPF (110), EIGRP (90), Static (1), Connected (0)

---

## Question 26
**Sélectionnez TROIS réponses correctes.**

Quelles valeurs du champ "Next Header" dans l'entête IPv6 sont correctes ?

- [ ] 6 = TCP
- [ ] 17 = UDP
- [ ] 43 = Routing Header
- [ ] 58 = ICMPv6
- [ ] 89 = OSPF

---

## Question 27 - ANALYSE DE SORTIE DE COMMANDE
Analysez cette sortie de la commande `show ipv6 neighbors` sur un routeur Cisco :
```
IPv6 Address                    Age  Link-layer Addr  State     Interface
2001:DB8:ACAD:1::10             0    0050.7966.6801   REACH     GigabitEthernet0/0
FE80::250:79FF:FE66:6802        5    0050.7966.6802   STALE     GigabitEthernet0/0
2001:DB8:ACAD:1::25             -    0050.7966.6803   INCMP     GigabitEthernet0/0
```
Quelle interprétation est correcte ?

- [ ] Tous les voisins sont inaccessibles
- [ ] Le voisin ::10 est confirmé joignable, ::25 est incomplet
- [ ] Les trois voisins sont en état opérationnel normal
- [ ] La table des voisins est corrompue, il faut la vider

---

## Question 28
Quelle commande configure une adresse IPv6 sur une interface en utilisant la méthode EUI-64 ?

- [ ] R1(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
- [ ] R1(config-if)# ipv6 address 2001:db8:acad:1::1/64 auto
- [ ] R1(config-if)# ipv6 address 2001:db8:acad:1::/64 auto-config
- [ ] R1(config-if)# ipv6 address eui-64 2001:db8:acad:1::/64

---

## Question 29 - QUESTION DE SYNTHÈSE
Un administrateur doit configurer un routeur R1 pour permettre à un réseau IPv6 2001:DB8:ACAD:1::/64 d'utiliser SLAAC pour l'auto-configuration. Quelles sont les étapes minimales nécessaires ?

**Sélectionnez TROIS réponses correctes.**

- [ ] Activer le routage IPv6 : ipv6 unicast-routing
- [ ] Configurer une adresse IPv6 globale sur l'interface : ipv6 address 2001:db8:acad:1::1/64
- [ ] Configurer DHCPv6 : ipv6 dhcp pool
- [ ] Activer l'interface : no shutdown
- [ ] Configurer une route statique par défaut

---

## Question 30 - SCÉNARIO AVANCÉ
Un hôte avec l'adresse IPv6 2001:DB8:ACAD:1::50 souhaite envoyer un paquet à un serveur distant 2001:DB8:ACAD:5::100. L'hôte ne connaît pas l'adresse MAC de sa passerelle par défaut (FE80::1). Décrivez la séquence correcte des événements.

**Sélectionnez l'ordre correct des étapes :**

- [ ] A) L'hôte envoie NS vers FF02::1:FF00:0001 → B) Le routeur répond avec NA → C) L'hôte encapsule le paquet avec MAC destination = MAC du routeur → D) Le paquet est routé vers le serveur
- [ ] A) L'hôte envoie RS vers FF02::2 → B) Le routeur répond avec RA → C) L'hôte envoie le paquet directement au serveur
- [ ] A) L'hôte envoie ARP Request → B) Le routeur répond avec ARP Reply → C) Le paquet est envoyé
- [ ] A) L'hôte envoie le paquet en broadcast → B) Tous les routeurs reçoivent le paquet → C) Le meilleur routeur le transmet

---

---

# Réponses et explications

---

## Question 1
**Réponse correcte :** C - Les adresses IP restent identiques, les adresses MAC changent

**Explication :**
Lors du routage entre réseaux :
- Les **adresses IP source et destination** restent **identiques** de bout en bout (c'est le principe de la couche 3)
- Les **adresses MAC changent à chaque saut** car elles servent uniquement à la livraison locale (couche 2)
- À chaque routeur, la trame Layer 2 est décapsulée, puis réencapsulée avec de nouvelles adresses MAC (source = MAC de l'interface de sortie du routeur, destination = MAC du prochain saut)

---

## Question 2 ⚠️ **NDP**
**Réponse correcte :** B - Type 133 - Router Solicitation (RS)

**Explication :**
Quand un hôte IPv6 se connecte à un réseau :
1. Il envoie un **Router Solicitation (RS) - Type 133** en multicast vers **FF02::2** (tous les routeurs)
2. Les routeurs répondent avec un **Router Advertisement (RA) - Type 134** contenant :
   - Le préfixe du réseau
   - L'adresse de la passerelle par défaut (link-local du routeur)
   - Les flags M et O pour la configuration DHCPv6
3. L'hôte utilise ces informations pour s'auto-configurer (SLAAC)

**Message RS** : *"Y a-t-il des routeurs sur ce réseau ? Merci de vous annoncer."*

---

## Question 3
**Réponses correctes :** B (S = Static), D (O = OSPF)

**Explication :**
Les codes de table de routage indiquent la source de la route :
- **C (Connected)** : réseau directement connecté (interface active avec une IP)
- **L (Local)** : adresse locale de l'interface elle-même
- **S (Static)** : route **configurée manuellement** par l'administrateur
- **D (EIGRP)** : route apprise via le protocole EIGRP
- **O (OSPF)** : route **apprise dynamiquement** via le protocole OSPF

Les routes configurées manuellement = **S (Static)**
Les routes apprises dynamiquement = **D, O, R** (protocoles de routage)

---

## Question 4
**Réponse correcte :** B - La commande "ipv6 unicast-routing" n'a pas été configurée

**Explication :**
La commande **`ipv6 unicast-routing`** est **OBLIGATOIRE** pour :
- **Activer le routage IPv6** sur le routeur
- Permettre au routeur de **router les paquets IPv6** entre interfaces
- Permettre au routeur d'**envoyer des Router Advertisements (RA)**

Sans cette commande :
- Le routeur ne routera pas les paquets IPv6
- Les clients ne recevront pas de RA pour leur auto-configuration
- Le trafic IPv6 ne passera pas vers Internet

**Configuration correcte :**
```
R1(config)# ipv6 unicast-routing
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
```

---

## Question 5 ⚠️ **LINK-LOCAL**
**Réponses correctes :** A (FE80::/10), C (passerelle par défaut), E (valides sur le lien local)

**Explication :**
Les adresses IPv6 link-local :
- ✅ **Commencent par FE80::/10** (FE80, FE90, FEA0, FEB0)
- ❌ **Ne sont PAS routables** sur Internet (uniquement lien local)
- ✅ **Utilisées comme passerelle par défaut** pour les hôtes IPv6
- ✅ **Générées automatiquement** avec EUI-64 (mais configuration manuelle recommandée)
- ✅ **Valides uniquement sur le lien local** (un seul segment réseau)

**Utilisations :**
- Passerelle par défaut pour les clients
- Communication entre voisins sur le même lien
- Protocoles de routage (OSPF, EIGRP)
- NDP (Neighbor Discovery Protocol)

---

## Question 6
**Réponse correcte :** B - Protocol

**Explication :**
Le champ **Protocol (8 bits)** dans l'entête IPv4 identifie le protocole de couche supérieure (Layer 4) :
- **1** = ICMP
- **6** = TCP
- **17** = UDP
- **89** = OSPF
- **88** = EIGRP

Ce champ permet au système de destination de savoir quel protocole doit traiter les données encapsulées dans le paquet IP.

**Équivalent IPv6** : champ **Next Header**

---

## Question 7 ⚠️ **NDP**
**Réponse correcte :** C - Type 135 - Neighbor Solicitation (NS)

**Explication :**
**DAD (Duplicate Address Detection)** permet à un hôte de vérifier qu'une adresse IPv6 n'est pas déjà utilisée avant de l'activer.

**Processus DAD :**
1. L'hôte génère une nouvelle adresse IPv6
2. Il envoie un **Neighbor Solicitation (NS) - Type 135** vers l'adresse multicast solicited-node correspondante (FF02::1:FF__:____)
3. Il attend une réponse (**Neighbor Advertisement - NA**)
4. **Si aucune réponse** → adresse disponible, l'hôte peut l'utiliser
5. **Si réponse reçue** → conflit détecté, l'hôte ne doit PAS utiliser cette adresse

**Message NS pour DAD** : *"Quelqu'un utilise-t-il l'adresse 2001:DB8:ACAD:1::10 ?"*

---

## Question 8
**Réponses correctes :** A (copy running-config startup-config), D (copy run start)

**Explication :**
Pour sauvegarder la configuration en cours (RAM) vers la configuration de démarrage (NVRAM) :

**Commandes complètes :**
- `copy running-config startup-config`
- `copy run start` (abrégé)

**Commande obsolète (anciennes versions IOS) :**
- `write memory` ou `write` (équivalent, mais moins utilisé maintenant)

**Attention :**
- `save configuration` n'existe pas dans Cisco IOS
- `save run start` n'existe pas
- Sans sauvegarde, la configuration sera **perdue au redémarrage**

---

## Question 9
**Réponse correcte :** B - La distance administrative d'OSPF

**Explication :**
Format d'une entrée de table de routage :
```
O    10.5.5.0/24 [110/65] via 192.168.1.2, 00:10:23, GigabitEthernet0/1
```

Décomposition :
- **O** = route apprise via OSPF
- **10.5.5.0/24** = réseau de destination
- **[110/65]** :
  - **110** = **Distance Administrative (AD)** d'OSPF
  - **65** = Métrique (coût de la route)
- **via 192.168.1.2** = adresse du prochain saut (next-hop)
- **00:10:23** = temps écoulé depuis l'apprentissage (10 minutes 23 secondes)
- **GigabitEthernet0/1** = interface de sortie

**Distance Administrative :** mesure de **fiabilité** de la source de la route (plus faible = plus fiable)

---

## Question 10
**Réponse correcte :** B - IPv4 : 20-60 octets variables, IPv6 : 40 octets fixes

**Explication :**
Comparaison des entêtes :

**IPv4 :**
- Taille **variable** : **20 à 60 octets**
- 20 octets minimum (sans options)
- Jusqu'à 60 octets (avec options)
- Champ IHL indique la taille de l'entête

**IPv6 :**
- Taille **fixe** : **40 octets**
- Simplifie le traitement par les routeurs
- Les fonctionnalités optionnelles sont gérées par des **entêtes d'extension** chainés

**Avantage IPv6 :** traitement plus rapide par les routeurs (entête fixe, pas de checksum)

---

## Question 11 ⚠️ **LINK-LOCAL**
**Réponse correcte :** B - Pour avoir une adresse simple et mémorisable (FE80::1)

**Explication :**
**Configuration manuelle de l'adresse link-local :**

**Avantages :**
- ✅ Adresses **simples et mémorisables** : FE80::1, FE80::2, etc.
- ✅ **Cohérence** : même adresse link-local sur toutes les interfaces d'un routeur (facilite la gestion)
- ✅ Facilite l'**identification** et le **dépannage**
- ✅ Utilisée comme **passerelle par défaut prévisible** pour les clients

**Adresse auto-générée (EUI-64) :**
- Difficile à mémoriser : FE80::2E0:F7FF:FE12:3456
- Varie selon l'interface (basée sur la MAC)

**Note :** L'adresse link-local est TOUJOURS auto-générée si non configurée manuellement. La configuration manuelle n'est pas obligatoire, mais **fortement recommandée**.

---

## Question 12 ⚠️ **NDP**
**Réponses correctes :** B (Type 134 - RA), E (Type 137 - Redirect)

**Explication :**
**Messages NDP envoyés par les routeurs :**

1. **Type 134 - Router Advertisement (RA)** :
   - Annonce périodique de la présence du routeur
   - Fournit le préfixe du réseau, la passerelle, les flags M/O
   - Permet aux hôtes de s'auto-configurer (SLAAC)

2. **Type 137 - Redirect** :
   - Informe un hôte qu'il existe un meilleur chemin pour atteindre une destination
   - Optimise le routage local

**Messages envoyés par les hôtes :**
- **Type 133 - Router Solicitation (RS)** : demande aux routeurs de s'annoncer
- **Type 135 - Neighbor Solicitation (NS)** : recherche d'un voisin, DAD
- **Type 136 - Neighbor Advertisement (NA)** : réponse à un NS

---

## Question 13
**Réponse correcte :** A - Opcode 1, MAC destination = FF:FF:FF:FF:FF:FF

**Explication :**
**ARP Request (requête ARP) :**
- **Opcode** : **1** (Request)
- **MAC destination** : **FF:FF:FF:FF:FF:FF** (broadcast Ethernet)
- **Target MAC** dans le message ARP : 00:00:00:00:00:00 (inconnu)

**Message** : *"Qui a l'adresse IP 192.168.1.20 ? Merci de répondre à AA:AA:AA:AA:AA:AA."*

**ARP Reply (réponse ARP) :**
- **Opcode** : **2** (Reply)
- **MAC destination** : adresse MAC de l'émetteur de la requête (unicast)

**Note :** La requête est en broadcast pour atteindre tous les hôtes du LAN, seul l'hôte possédant l'IP recherchée répond en unicast.

---

## Question 14
**Réponses correctes :** A (1 = ICMP), B (6 = TCP), C (17 = UDP)

**Explication :**
Le champ **Protocol (8 bits)** dans l'entête IPv4 identifie le protocole de couche supérieure :

**Valeurs correctes :**
- **1** = **ICMP** (Internet Control Message Protocol)
- **6** = **TCP** (Transmission Control Protocol)
- **17** = **UDP** (User Datagram Protocol)
- **89** = **OSPF** (Open Shortest Path First)
- **88** = EIGRP

**Valeurs incorrectes :**
- ❌ **58** = ICMPv6 (utilisé dans l'entête **IPv6**, PAS IPv4)

---

## Question 15
**Réponse correcte :** B - 113

**Explication :**
Le champ **TTL (Time to Live)** :
- **Décrémenté de 1** à chaque passage par un routeur
- Si TTL = 0 → paquet détruit, message ICMP "Time Exceeded" envoyé

**Calcul :**
- TTL initial : **128**
- Nombre de routeurs traversés : **15**
- TTL final : 128 - 15 = **113**

**Utilité du TTL :**
- Empêche les **boucles de routage infinies**
- Les paquets ne restent pas indéfiniment dans le réseau

---

## Question 16
**Réponse correcte :** B - Le multicast réduit la charge réseau en ciblant uniquement les hôtes concernés

**Explication :**
**Différence Broadcast (ARP IPv4) vs Multicast (NDP IPv6) :**

**Broadcast (IPv4 - ARP) :**
- Adresse MAC : FF:FF:FF:FF:FF:FF
- **Tous les hôtes** du LAN doivent traiter la trame (même ceux non concernés)
- Charge réseau élevée sur les réseaux avec beaucoup d'hôtes

**Multicast (IPv6 - NDP) :**
- Adresse multicast solicited-node : FF02::1:FF__:____ (3 derniers octets de l'IP cible)
- Seuls les hôtes ayant rejoint ce groupe multicast traitent le message
- **Réduit considérablement la charge** sur les hôtes non concernés

**Avantage principal :** efficacité et réduction de la charge réseau

---

## Question 17
**Réponses correctes :** A (ip domain-name), B (crypto key generate rsa), E (transport input ssh)

**Explication :**
**Configuration SSH sur un routeur Cisco - étapes minimales :**

1. **Définir le domaine** (obligatoire pour générer les clés) :
   ```
   R1(config)# ip domain-name example.com
   ```

2. **Générer les clés RSA** (minimum 2048 bits recommandé) :
   ```
   R1(config)# crypto key generate rsa modulus 2048
   ```

3. **Configurer les lignes VTY pour SSH uniquement** :
   ```
   R1(config)# line vty 0 4
   R1(config-line)# transport input ssh
   R1(config-line)# login local
   ```

**Optionnel mais recommandé :**
```
R1(config)# ip ssh version 2
R1(config)# username admin privilege 15 secret AdminPass123
```

**Note :** `ip ssh version 2` n'est pas dans les commandes proposées, mais c'est une bonne pratique.

---

## Question 18
**Réponse correcte :** B - FF02::1:FF00:A5B3

**Explication :**
**Adresse multicast solicited-node :**
- Format : **FF02::1:FF + 3 derniers octets de l'adresse IPv6 cible**

**Calcul pour 2001:DB8:ACAD:1::A5B3 :**
- Adresse complète : 2001:0DB8:ACAD:0001:0000:0000:0000:A5B3
- **3 derniers octets (24 bits)** : 00:A5:B3
- Adresse solicited-node : **FF02::1:FF00:A5B3**

**Utilisation :**
- Les **Neighbor Solicitation (NS)** sont envoyés à cette adresse multicast
- Plus efficace que le broadcast (seuls les hôtes concernés traitent le message)

---

## Question 19
**Réponse correcte :** A - 0

**Explication :**
**Distance Administrative (AD)** des différentes sources de routes (ordre croissant = plus fiable) :

- **0** = **Connected** (réseau directement connecté) ← **Plus fiable**
- **1** = **Static** (route statique)
- **90** = **EIGRP** (Cisco propriétaire)
- **110** = **OSPF** (Open Shortest Path First)
- **120** = **RIP** (Routing Information Protocol)

**Logique :**
Les réseaux directement connectés ont la **distance administrative la plus faible (0)** car ils sont les plus fiables : le routeur sait avec certitude que ces réseaux sont joignables via ses interfaces.

---

## Question 20
**Réponses correctes :** A (show ipv6 interface brief), C (show ipv6 interface g0/0)

**Explication :**
**Commandes de vérification IPv6 sur Cisco IOS :**

1. **`show ipv6 interface brief`** :
   - Affiche toutes les interfaces avec leurs adresses IPv6 (globale + link-local)
   - État up/up ou down/down

2. **`show ipv6 interface g0/0`** :
   - Affiche les détails d'une interface spécifique
   - Adresses IPv6, groupes multicast, état NDP, etc.

**Commandes incorrectes :**
- ❌ `show ip interface brief` : pour **IPv4** uniquement
- ❌ `show interface ipv6` : n'existe pas
- ❌ `ipconfig /all` : commande **Windows**, pas Cisco IOS

---

## Question 21
**Réponse correcte :** C - Next Header

**Explication :**
**Correspondance des champs IPv4 ↔ IPv6 :**

| IPv4 | IPv6 | Description |
|------|------|-------------|
| **Protocol** | **Next Header** | Protocole de couche supérieure |
| TTL | Hop Limit | Nombre de sauts maximum |
| Type of Service (ToS) | Traffic Class | Qualité de service (QoS) |

**Valeurs du champ Next Header :**
- **6** = TCP
- **17** = UDP
- **58** = ICMPv6
- **43** = Routing Header (extension)
- **44** = Fragment Header (extension)

---

## Question 22
**Réponse correcte :** C - SLAAC (auto-configuration complète sans DHCPv6)

**Explication :**
**Flags dans les Router Advertisements (RA) :**

| Flag M | Flag O | Méthode d'auto-configuration |
|--------|--------|------------------------------|
| **0** | **0** | **SLAAC** (auto-configuration complète, pas de DHCPv6) |
| **1** | X | **DHCPv6 Stateful** (adresse + options via DHCPv6) |
| **0** | **1** | **SLAAC + DHCPv6 Stateless** (adresse via SLAAC, options via DHCPv6) |

**SLAAC (M=0, O=0) :**
- L'hôte génère son adresse IPv6 automatiquement :
  - Préfixe fourni par RA
  - Interface ID généré avec EUI-64 ou aléatoire
- Passerelle par défaut = adresse link-local du routeur
- **Aucun serveur DHCPv6 nécessaire**

---

## Question 23
**Réponses correctes :** A (clear ip arp), B (clear arp-cache)

**Explication :**
**Commandes Cisco IOS pour effacer la table ARP :**

1. **`clear ip arp`** :
   - Efface toutes les entrées dynamiques de la table ARP
   - Commande principale

2. **`clear arp-cache`** :
   - Équivalent à `clear ip arp`
   - Commande alternative

**Commandes incorrectes :**
- ❌ `delete arp` : n'existe pas
- ❌ `erase arp` : n'existe pas
- ❌ `no ip arp` : désactive ARP sur une interface, ne vide pas la table

**Note :** Les entrées statiques ne sont pas supprimées avec ces commandes.

---

## Question 24
**Réponse correcte :** B - Problème : interface désactivée | Solution : no shutdown

**Explication :**
**Analyse de la sortie :**
```
GigabitEthernet0/0  192.168.10.1  YES manual  administratively down  down
```

**État "administratively down / down" :**
- Signifie que l'interface a été **désactivée manuellement** avec la commande `shutdown`
- Par défaut, toutes les interfaces de routeur sont **désactivées** (`shutdown`)

**Solution :**
```
R1(config)# interface g0/0
R1(config-if)# no shutdown
```

**Après la commande `no shutdown` :**
```
GigabitEthernet0/0  192.168.10.1  YES manual  up  up
```

**Erreurs courantes :**
- Oublier `no shutdown` après la configuration de l'interface
- Penser que l'interface est active par défaut (contrairement aux switchs)

---

## Question 25
**Réponse correcte :** A - Connected (0), Static (1), EIGRP (90), OSPF (110), RIP (120)

**Explication :**
**Distance Administrative (AD) - ordre croissant (plus fiable → moins fiable) :**

1. **Connected (0)** : réseaux directement connectés (plus fiable)
2. **Static (1)** : routes statiques configurées manuellement
3. **EIGRP (90)** : protocole Cisco propriétaire
4. **OSPF (110)** : protocole à état de lien
5. **RIP (120)** : protocole à vecteur de distance (ancien, moins fiable)

**Principe :**
- **Plus l'AD est faible**, plus la route est **fiable**
- Si plusieurs routes vers la même destination avec des AD différentes → le routeur choisit celle avec l'AD la plus faible

---

## Question 26
**Réponses correctes :** A (6 = TCP), B (17 = UDP), D (58 = ICMPv6)

**Explication :**
Le champ **Next Header (8 bits)** dans l'entête IPv6 identifie le prochain entête (protocole de couche supérieure ou entête d'extension) :

**Valeurs correctes :**
- **6** = **TCP** (Transmission Control Protocol)
- **17** = **UDP** (User Datagram Protocol)
- **58** = **ICMPv6** (Internet Control Message Protocol version 6)
- ✅ **43** = Routing Header (entête d'extension, correct)

**Valeurs incorrectes :**
- ❌ **89** = OSPF (protocole de routage, mais s'exécute sur **IP**, donc valeur possible mais non demandée ici)

**Note :** 43 est une entête d'extension IPv6, pas un protocole de couche 4, mais c'est une valeur valide du champ Next Header.

**Correction :** La question demande les valeurs correctes. Dans ce contexte, les trois réponses principales sont 6, 17 et 58. La valeur 43 est également valide techniquement.

---

## Question 27
**Réponse correcte :** B - Le voisin ::10 est confirmé joignable, ::25 est incomplet

**Explication :**
**États de la table des voisins IPv6 (NDP) :**

1. **REACH (Reachable)** :
   - Voisin **confirmé joignable** récemment
   - Age = 0 : vient d'être vérifié
   - État opérationnel normal

2. **STALE (Périmé)** :
   - Entrée **pas vérifiée récemment** mais toujours utilisable
   - Age = 5 : dernière vérification il y a 5 secondes
   - Sera re-vérifiée à la prochaine utilisation
   - État normal

3. **INCMP (Incomplete)** :
   - Résolution d'adresse **en cours**
   - Age = "-" : en cours de traitement
   - NS envoyé, en attente de NA
   - Peut indiquer un problème si statut persiste

**Analyse :**
- **::10** : REACH → voisin joignable ✅
- **FE80::...:6802** : STALE → voisin probablement joignable (normal) ✅
- **::25** : INCMP → résolution incomplète (peut indiquer un problème) ⚠️

---

## Question 28
**Réponse correcte :** A - R1(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64

**Explication :**
**Configuration IPv6 avec EUI-64 :**

**Syntaxe correcte :**
```
R1(config-if)# ipv6 address <préfixe>/64 eui-64
```

**Exemple :**
```
R1(config-if)# ipv6 address 2001:db8:acad:1::/64 eui-64
```

**Résultat :**
- Le préfixe est fourni : 2001:DB8:ACAD:1::/64
- L'**Interface ID (64 bits de poids faible)** est généré automatiquement à partir de l'adresse MAC :
  - Insertion de FFFE au milieu de la MAC
  - Inversion du 7e bit
- Adresse complète : 2001:DB8:ACAD:1:021A:2BFF:FE3C:4D5E/64

**Commandes incorrectes :**
- ❌ `ipv6 address ... auto` : n'existe pas
- ❌ `ipv6 address ... auto-config` : n'existe pas
- ❌ `ipv6 address eui-64 ...` : ordre incorrect

---

## Question 29
**Réponses correctes :** A (ipv6 unicast-routing), B (ipv6 address ...), D (no shutdown)

**Explication :**
**Configuration minimale pour SLAAC sur un routeur :**

**Étape 1 : Activer le routage IPv6 (OBLIGATOIRE)**
```
R1(config)# ipv6 unicast-routing
```
- Permet au routeur de router les paquets IPv6
- Permet au routeur d'envoyer des Router Advertisements (RA)

**Étape 2 : Configurer une adresse IPv6 globale sur l'interface**
```
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
```
- Le routeur utilise cette adresse pour envoyer les RA
- Les clients utiliseront le préfixe 2001:db8:acad:1::/64 pour s'auto-configurer

**Étape 3 : Activer l'interface**
```
R1(config-if)# no shutdown
```

**Pas nécessaire pour SLAAC :**
- ❌ DHCPv6 : SLAAC fonctionne sans serveur DHCP
- ❌ Route statique par défaut : pour le routage sortant du routeur, pas pour SLAAC des clients

---

## Question 30
**Réponse correcte :** A - L'hôte envoie NS vers FF02::1:FF00:0001 → Le routeur répond avec NA → L'hôte encapsule le paquet avec MAC destination = MAC du routeur → Le paquet est routé vers le serveur

**Explication :**
**Séquence complète de communication IPv6 vers réseau distant :**

**Étape 1 : Résolution de l'adresse link-local de la passerelle (FE80::1)**
- L'hôte détermine que 2001:DB8:ACAD:5::100 est sur un **réseau distant**
- Il doit envoyer le paquet à sa **passerelle par défaut (FE80::1)**
- Il ne connaît pas l'**adresse MAC de FE80::1**
- Il envoie un **Neighbor Solicitation (NS) - Type 135** vers l'adresse multicast solicited-node :
  - **FF02::1:FF00:0001** (3 derniers octets de FE80::1)

**Étape 2 : Réponse du routeur**
- Le routeur répond avec un **Neighbor Advertisement (NA) - Type 136** contenant son adresse MAC
- L'hôte enregistre l'association FE80::1 ↔ MAC du routeur dans sa table des voisins

**Étape 3 : Encapsulation et envoi**
- L'hôte encapsule le paquet IPv6 dans une trame Ethernet :
  - **IP source** : 2001:DB8:ACAD:1::50
  - **IP destination** : 2001:DB8:ACAD:5::100
  - **MAC source** : MAC de l'hôte
  - **MAC destination** : **MAC du routeur** (passerelle)

**Étape 4 : Routage**
- Le routeur reçoit la trame, décapsule le paquet
- Consulte sa table de routage pour 2001:DB8:ACAD:5::/64
- Route le paquet vers le serveur (potentiellement via d'autres routeurs)

**Point clé :** Les adresses IP restent identiques de bout en bout, mais les adresses MAC changent à chaque saut.

---

