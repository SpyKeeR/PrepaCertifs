# Module 13 - ICMP et protocoles de connectivité

## Table des matières
1. [Introduction à ICMP](#introduction)
2. [Messages ICMP IPv4](#icmpv4)
3. [Messages ICMPv4 d'erreur](#icmpv4-erreur)
4. [Messages ICMPv4 d'information](#icmpv4-info)
5. [Messages ICMP IPv6](#icmpv6)
6. [Messages ICMPv6 d'erreur](#icmpv6-erreur)
7. [Messages ICMPv6 d'information](#icmpv6-info)
8. [ICMPv6 et NDP](#icmpv6-ndp)
9. [SLAAC - Stateless Address Autoconfiguration](#slaac)
10. [DHCPv6](#dhcpv6)
11. [Méthodes d'allocation IPv6](#methodes-allocation)
12. [Commandes de diagnostic](#diagnostic)

---

## 1. Introduction à ICMP {#introduction}

### Définition
Le **ICMP (Internet Control Message Protocol)** est un protocole de **couche 3** utilisé pour :
- **Signaler des erreurs** de transmission (destination inaccessible, TTL expiré, etc.)
- **Fournir des informations** de diagnostic (ping, traceroute)
- **Contrôler le réseau** (redirection, messages de contrôle)

### Caractéristiques
- Protocole de **support** pour IP (ne transporte pas de données utilisateur)
- Utilisé par **IPv4** (ICMPv4) et **IPv6** (ICMPv6)
- **Non fiable** : pas de garantie de livraison
- Les messages ICMP sont **encapsulés dans des paquets IP**

### Versions
- **ICMPv4** : RFC 792, utilisé avec IPv4
- **ICMPv6** : RFC 4443, utilisé avec IPv6
  - Plus de fonctionnalités (intègre **NDP**)
  - Remplace plusieurs protocoles IPv4 (ARP, IGMP)

---

## 2. Messages ICMP IPv4 {#icmpv4}

### Structure d'un message ICMPv4

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Type      |     Code      |          Checksum             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        (Variables selon Type/Code)             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Données (optionnel)                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### Champs principaux
- **Type (8 bits)** : type de message ICMP
- **Code (8 bits)** : sous-type ou détails du message
- **Checksum (16 bits)** : vérification d'intégrité
- **Données** : informations complémentaires selon le type

### Catégories de messages ICMPv4
- **Messages d'erreur** : signalent des problèmes (Type 3, 5, 11, 12)
- **Messages d'information** : diagnostics et requêtes (Type 0, 8)

---

## 3. Messages ICMPv4 d'erreur {#icmpv4-erreur}

### Type 3 - Destination Unreachable ⚠️ **TRÈS IMPORTANT**

**Rôle** : Signaler qu'une destination est **inaccessible**.

#### Codes de Type 3 (sous-types)

| Code | Nom | Description | Généré par |
|------|-----|-------------|------------|
| **0** | Network Unreachable | Réseau de destination inaccessible | Routeur |
| **1** | Host Unreachable | Hôte de destination inaccessible | Routeur |
| **2** | Protocol Unreachable | Protocole de couche supérieure non supporté | Hôte destination |
| **3** | Port Unreachable | Port de destination fermé ou inaccessible | Hôte destination |
| **4** | Fragmentation Needed (DF set) | Fragmentation nécessaire mais DF=1 (Don't Fragment) | Routeur |
| **5** | Source Route Failed | Échec du routage par la source | Routeur |
| **6** | Destination Network Unknown | Réseau de destination inconnu | Routeur |
| **7** | Destination Host Unknown | Hôte de destination inconnu | Routeur |
| **13** | Communication Administratively Prohibited | Communication bloquée (ACL, firewall) | Routeur/Firewall |

**Scénarios courants** :

**Code 0 - Network Unreachable** :
- Le routeur n'a **pas de route** vers le réseau de destination
- Exemple : ping 10.1.1.10, mais le routeur n'a pas de route vers 10.1.1.0/24

**Code 1 - Host Unreachable** :
- Le routeur a une route vers le réseau, mais l'hôte **ne répond pas**
- L'hôte est éteint, déconnecté, ou n'a pas l'adresse IP
- Exemple : ping 192.168.1.50, le routeur envoie des ARP Request, mais aucune réponse

**Code 3 - Port Unreachable** :
- L'hôte est joignable, mais le **port UDP** spécifié n'est pas ouvert
- Exemple : envoi d'un paquet UDP vers un port non écouté
- Utilisé par **traceroute** (envoie des paquets UDP vers des ports élevés)

**Code 4 - Fragmentation Needed (DF set)** :
- Le paquet est trop grand pour le MTU du lien suivant
- Le bit **DF (Don't Fragment)** est positionné à 1
- Le routeur **ne peut pas fragmenter** et envoie ce message
- Utilisé pour **Path MTU Discovery** (PMTUD)

**Code 13 - Communication Administratively Prohibited** :
- La communication est **bloquée par une ACL** ou un firewall
- Exemple : accès refusé par une règle de sécurité

---

### Type 5 - Redirect

**Rôle** : Informer un hôte qu'un **meilleur chemin** existe vers une destination.

**Scénario** :
1. Un hôte envoie un paquet à sa passerelle par défaut (Routeur 1)
2. Routeur 1 détermine que Routeur 2 (sur le même segment) est un meilleur chemin
3. Routeur 1 transmet le paquet ET envoie un **ICMP Redirect** à l'hôte
4. L'hôte met à jour sa table de routage locale

**Code** :
- **0** : Redirect for Network
- **1** : Redirect for Host

---

### Type 11 - Time Exceeded ⚠️ **TRÈS IMPORTANT**

**Rôle** : Signaler qu'un paquet a été **rejeté** en raison de l'expiration d'un compteur.

#### Codes de Type 11

| Code | Nom | Description |
|------|-----|-------------|
| **0** | TTL Exceeded in Transit | TTL a atteint 0 pendant le transit (hop par hop) |
| **1** | Fragment Reassembly Time Exceeded | Temps de réassemblage des fragments dépassé |

**Code 0 - TTL Exceeded in Transit** :
- Le **TTL (Time To Live)** d'un paquet IPv4 atteint **0**
- Le routeur **rejette le paquet** et envoie ce message à la source
- Empêche les **boucles de routage infinies**
- **Utilisé par traceroute** pour découvrir le chemin réseau

**Fonctionnement de traceroute avec ICMP Type 11** :
```
1. Client envoie paquet avec TTL=1 → Routeur 1 répond ICMP Type 11 Code 0
2. Client envoie paquet avec TTL=2 → Routeur 2 répond ICMP Type 11 Code 0
3. Client envoie paquet avec TTL=3 → Routeur 3 répond ICMP Type 11 Code 0
...
N. Client envoie paquet avec TTL=N → Destination répond ICMP Type 3 Code 3 (Port Unreachable)
```

**Code 1 - Fragment Reassembly Time Exceeded** :
- L'hôte de destination n'a pas reçu **tous les fragments** dans le délai imparti
- Les fragments reçus sont **rejetés**
- Rare en pratique

---

### Type 12 - Parameter Problem

**Rôle** : Signaler un **problème dans l'entête IP**.

**Code** :
- **0** : Pointer indicates error (pointeur vers le champ erroné)
- **1** : Required Option is Missing

**Utilisation** :
- Entête IPv4 malformé ou incorrect
- Option obligatoire manquante
- Le routeur ou l'hôte **rejette le paquet**

---

## 4. Messages ICMPv4 d'information {#icmpv4-info}

### Type 8 - Echo Request (Ping)

**Rôle** : Demander une **réponse** pour tester la connectivité.

**Utilisation** :
```
C:\> ping 8.8.8.8
```

**Processus** :
1. Client envoie **ICMP Echo Request (Type 8)**
2. Destination répond **ICMP Echo Reply (Type 0)**
3. Client mesure le **temps de réponse (RTT)**

**Structure** :
- **Type** : 8
- **Code** : 0
- **Identifier** : ID de la session ping
- **Sequence Number** : numéro du paquet (incrémenté)
- **Data** : données aléatoires (généralement 32 octets)

---

### Type 0 - Echo Reply (Pong)

**Rôle** : Répondre à un **Echo Request**.

**Processus** :
- La destination reçoit l'**Echo Request**
- Elle envoie un **Echo Reply** avec les **mêmes données**
- Le client vérifie que les données correspondent

**Structure** :
- **Type** : 0
- **Code** : 0
- **Identifier** : même que la requête
- **Sequence Number** : même que la requête
- **Data** : mêmes données que la requête

---

## 5. Messages ICMP IPv6 {#icmpv6}

### Introduction
**ICMPv6** (RFC 4443) est une **évolution majeure** par rapport à ICMPv4 :
- Intègre les fonctionnalités de **NDP** (Neighbor Discovery Protocol)
- Remplace **ARP** (résolution d'adresse)
- Remplace **IGMP** (gestion des groupes multicast)
- Intègre **Path MTU Discovery**

### Structure d'un message ICMPv6

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Type      |     Code      |          Checksum             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Message Body (variable)                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### Catégories de messages ICMPv6
- **Messages d'erreur** : Type 0-127 (bit de poids fort = 0)
- **Messages d'information** : Type 128-255 (bit de poids fort = 1)

---

## 6. Messages ICMPv6 d'erreur {#icmpv6-erreur}

### Type 1 - Destination Unreachable ⚠️ **TRÈS IMPORTANT**

**Rôle** : Signaler qu'une destination est **inaccessible**.

#### Codes de Type 1 (sous-types)

| Code | Nom | Description | Généré par |
|------|-----|-------------|------------|
| **0** | No route to destination | Aucune route vers la destination | Routeur |
| **1** | Communication with destination administratively prohibited | Communication bloquée (ACL, firewall) | Routeur/Firewall |
| **2** | Beyond scope of source address | Destination hors de la portée de l'adresse source | Routeur |
| **3** | Address unreachable | Adresse inaccessible (résolution d'adresse échoue) | Routeur |
| **4** | Port unreachable | Port de destination fermé ou inaccessible | Hôte destination |
| **5** | Source address failed ingress/egress policy | Adresse source bloquée par politique | Routeur |
| **6** | Reject route to destination | Route rejetée vers la destination | Routeur |

**Différence avec ICMPv4 Type 3** :
- ICMPv6 Type 1 **regroupe** plusieurs erreurs (network/host unreachable)
- Code 0 = équivalent Code 0 et Code 1 d'ICMPv4 Type 3
- Code 4 = équivalent Code 3 d'ICMPv4 Type 3 (Port Unreachable)

**Scénarios courants** :

**Code 0 - No route to destination** :
- Le routeur n'a **aucune route** vers la destination
- Équivalent de ICMPv4 Type 3 Code 0/1

**Code 3 - Address unreachable** :
- La résolution d'adresse **NDP** a échoué
- Équivalent de ARP échoué en IPv4

**Code 4 - Port unreachable** :
- Port UDP de destination **fermé**
- Utilisé par **traceroute IPv6**

---

### Type 2 - Packet Too Big

**Rôle** : Signaler qu'un paquet est **trop grand** pour être transmis sur le lien suivant.

**Différence avec IPv4** :
- IPv4 : utilise Type 3 Code 4 (Fragmentation Needed, DF set)
- IPv6 : message dédié (Type 2)

**Fonctionnement** :
1. Un paquet IPv6 dépasse le **MTU** du lien
2. Le routeur **rejette le paquet** (IPv6 ne fragmente pas les paquets en transit)
3. Le routeur envoie **ICMPv6 Type 2** avec le MTU du lien
4. La source **réajuste** la taille de ses paquets

**Utilisation** : **Path MTU Discovery (PMTUD)** obligatoire en IPv6

**Code** : 0 (pas de sous-types)

**Contenu** :
- **MTU** : taille maximale supportée par le lien

---

### Type 3 - Time Exceeded ⚠️ **TRÈS IMPORTANT**

**Rôle** : Signaler qu'un paquet a été **rejeté** en raison de l'expiration d'un compteur.

#### Codes de Type 3

| Code | Nom | Description |
|------|-----|-------------|
| **0** | Hop Limit Exceeded in Transit | Hop Limit a atteint 0 pendant le transit |
| **1** | Fragment Reassembly Time Exceeded | Temps de réassemblage des fragments dépassé |

**Code 0 - Hop Limit Exceeded in Transit** :
- Le **Hop Limit** d'un paquet IPv6 atteint **0**
- Équivalent du **TTL** en IPv4
- Le routeur **rejette le paquet** et envoie ce message
- **Utilisé par traceroute IPv6**

**Fonctionnement de traceroute IPv6** :
```
1. Client envoie paquet avec Hop Limit=1 → Routeur 1 répond ICMPv6 Type 3 Code 0
2. Client envoie paquet avec Hop Limit=2 → Routeur 2 répond ICMPv6 Type 3 Code 0
3. Client envoie paquet avec Hop Limit=3 → Routeur 3 répond ICMPv6 Type 3 Code 0
...
N. Client envoie paquet avec Hop Limit=N → Destination répond ICMPv6 Type 1 Code 4 (Port Unreachable)
```

**Code 1 - Fragment Reassembly Time Exceeded** :
- Similaire à ICMPv4 Type 11 Code 1
- Rare en IPv6 (fragmentation seulement par la source)

---

### Type 4 - Parameter Problem

**Rôle** : Signaler un **problème dans l'entête IPv6** ou une extension.

**Codes** :
- **0** : Erroneous header field encountered (champ d'entête erroné)
- **1** : Unrecognized Next Header type (Next Header non reconnu)
- **2** : Unrecognized IPv6 option (option IPv6 non reconnue)

**Utilisation** :
- Entête IPv6 malformé
- Extension non supportée
- Option inconnue

---

## 7. Messages ICMPv6 d'information {#icmpv6-info}

### Type 128 - Echo Request (Ping)

**Rôle** : Demander une **réponse** pour tester la connectivité IPv6.

**Utilisation** :
```
C:\> ping 2001:db8::1
Router# ping ipv6 2001:db8::1
```

**Code** : 0

**Structure** : Identique à ICMPv4 Type 8 (Identifier, Sequence Number, Data)

---

### Type 129 - Echo Reply (Pong)

**Rôle** : Répondre à un **Echo Request IPv6**.

**Code** : 0

**Structure** : Identique à ICMPv4 Type 0

---

## 8. ICMPv6 et NDP {#icmpv6-ndp}

### Intégration de NDP dans ICMPv6

**NDP (Neighbor Discovery Protocol)** utilise **5 types de messages ICMPv6** pour remplacer ARP, ICMP Router Discovery, et ICMP Redirect d'IPv4.

| Type ICMPv6 | Nom | Rôle |
|-------------|-----|------|
| **133** | Router Solicitation (RS) | Demander aux routeurs de s'annoncer |
| **134** | Router Advertisement (RA) | Annoncer la présence d'un routeur, fournir infos réseau |
| **135** | Neighbor Solicitation (NS) | Résoudre une adresse IPv6 en MAC (= ARP Request) |
| **136** | Neighbor Advertisement (NA) | Répondre à un NS (= ARP Reply) |
| **137** | Redirect | Informer d'un meilleur chemin |

### Type 133 - Router Solicitation (RS)

**Rôle** : Un hôte demande aux routeurs de **s'annoncer immédiatement**.

**Envoyé par** : Hôtes (au démarrage ou à la connexion)

**Destination** : `FF02::2` (multicast : tous les routeurs du lien local)

**Contenu** :
- Adresse source : link-local de l'hôte ou `::` (si pas encore d'adresse)

**Processus** :
```
Hôte → FF02::2
"Y a-t-il des routeurs sur ce réseau ? Merci de vous annoncer."
```

---

### Type 134 - Router Advertisement (RA) ⚠️ **ESSENTIEL POUR SLAAC**

**Rôle** : Un routeur **annonce sa présence** et fournit des **informations de configuration réseau**.

**Envoyé par** : Routeurs IPv6

**Destination** :
- **Réponse à RS** : unicast vers l'hôte
- **Annonce périodique** : `FF02::1` (multicast : tous les nœuds)

**Informations fournies** :
- **Préfixe IPv6** du réseau (ex: 2001:db8:acad:1::/64)
- **Longueur du préfixe** (typiquement /64)
- **Adresse link-local du routeur** (utilisée comme passerelle par défaut)
- **Durée de vie du préfixe**
- **Flags M et O** (voir section DHCPv6)
- **MTU du lien**

**Flags du message RA** :

| Flag | Nom | Signification |
|------|-----|---------------|
| **M** | Managed Address Configuration | Si 1 : utiliser **DHCPv6 stateful** pour obtenir l'adresse |
| **O** | Other Configuration | Si 1 : utiliser **DHCPv6 stateless** pour d'autres infos (DNS, domaine) |
| **A** | Autonomous Address Configuration | Si 1 : utiliser **SLAAC** (généralement sur le préfixe) |

**Scénarios selon les flags** :
- **M=0, O=0** : SLAAC uniquement (pas de DHCPv6)
- **M=0, O=1** : SLAAC + DHCPv6 stateless (pour DNS)
- **M=1, O=x** : DHCPv6 stateful (l'hôte doit contacter un serveur DHCPv6)

---

### Type 135 - Neighbor Solicitation (NS)

**Rôle** : Résoudre une adresse IPv6 en adresse MAC (équivalent d'ARP Request).

**Envoyé par** : Hôte ou routeur

**Destination** : Adresse multicast **solicited-node** (`FF02::1:FF[24 derniers bits]`)

**Utilisations** :
1. **Résolution d'adresse** : trouver la MAC d'un voisin
2. **DAD (Duplicate Address Detection)** : vérifier qu'une adresse n'est pas déjà utilisée
3. **NUD (Neighbor Unreachability Detection)** : vérifier qu'un voisin est toujours joignable

**Exemple de résolution d'adresse** :
```
PC1 veut communiquer avec 2001:db8:acad:1::20

1. PC1 calcule solicited-node : FF02::1:FF00:0020
2. PC1 envoie NS à FF02::1:FF00:0020
   "Qui a l'adresse 2001:db8:acad:1::20 ? Quelle est votre MAC ?"
3. PC2 (qui a cette adresse) répond avec NA
```

**Exemple de DAD** :
```
PC1 veut utiliser 2001:db8:acad:1::10

1. PC1 envoie NS à FF02::1:FF00:0010 (solicited-node)
   "Quelqu'un utilise-t-il 2001:db8:acad:1::10 ?"
2. Si aucune réponse → adresse disponible
3. Si réponse (NA) → conflit d'adresse détecté
```

---

### Type 136 - Neighbor Advertisement (NA)

**Rôle** : Répondre à un NS ou annoncer un changement d'adresse MAC.

**Envoyé par** : Hôte ou routeur qui possède l'adresse recherchée

**Destination** :
- **Réponse à NS** : unicast vers l'émetteur du NS
- **Annonce spontanée** : `FF02::1` (tous les nœuds)

**Flags** :
- **R (Router)** : l'émetteur est un routeur
- **S (Solicited)** : réponse à un NS
- **O (Override)** : mettre à jour le cache même si une entrée existe

**Exemple** :
```
PC2 → PC1 (unicast)
"Oui, je suis 2001:db8:acad:1::20 et mon adresse MAC est AA:BB:CC:DD:EE:FF."
```

---

### Type 137 - Redirect

**Rôle** : Informer un hôte qu'un **meilleur chemin** existe vers une destination.

**Envoyé par** : Routeur

**Destination** : Unicast vers l'hôte concerné

**Scénario** :
1. Un hôte envoie un paquet à sa passerelle (Routeur 1)
2. Routeur 1 détermine que Routeur 2 (sur le même lien) est un meilleur chemin
3. Routeur 1 transmet le paquet ET envoie un **Redirect** à l'hôte
4. L'hôte met à jour sa table de routage

---

## 9. SLAAC - Stateless Address Autoconfiguration {#slaac}

### Définition
**SLAAC** permet à un hôte IPv6 de **générer automatiquement** son adresse IPv6 **globale** sans serveur DHCP.

### Principe
1. L'hôte génère une **link-local** (FE80::/10)
2. L'hôte envoie un **Router Solicitation (RS)** (Type 133)
3. Le routeur répond avec un **Router Advertisement (RA)** (Type 134) contenant :
   - **Préfixe** (ex: 2001:db8:acad:1::/64)
   - **Longueur du préfixe** (/64)
4. L'hôte génère son **Interface ID** (64 bits) :
   - **EUI-64** (dérivé de la MAC)
   - **Aléatoire** (privacy extensions, RFC 4941)
5. L'hôte effectue **DAD** (Duplicate Address Detection) avec NS
6. Si pas de conflit, l'hôte configure l'adresse IPv6 complète

### Étapes détaillées

#### Étape 1 : Génération de la Link-Local
```
MAC : 00:1A:2B:3C:4D:5E
EUI-64 : 021A:2BFF:FE3C:4D5E
Link-Local : FE80::021A:2BFF:FE3C:4D5E
```

#### Étape 2 : Router Solicitation (RS)
```
Source : FE80::021A:2BFF:FE3C:4D5E
Destination : FF02::2 (tous les routeurs)
Type ICMPv6 : 133 (RS)
Message : "Y a-t-il des routeurs sur ce lien ?"
```

#### Étape 3 : Router Advertisement (RA)
```
Source : FE80::1 (routeur)
Destination : FF02::1 (tous les nœuds) ou unicast
Type ICMPv6 : 134 (RA)
Contenu :
  - Préfixe : 2001:db8:acad:1::/64
  - Flags : M=0, O=0, A=1
  - Passerelle : FE80::1
```

#### Étape 4 : Génération de l'adresse globale
```
Préfixe (64 bits) : 2001:0db8:acad:0001
Interface ID (64 bits) : 021A:2BFF:FE3C:4D5E

Adresse complète : 2001:db8:acad:1:021A:2BFF:FE3C:4D5E/64
```

#### Étape 5 : DAD (Duplicate Address Detection)
```
Source : :: (adresse non spécifiée)
Destination : FF02::1:FF3C:4D5E (solicited-node)
Type ICMPv6 : 135 (NS)
Message : "Quelqu'un utilise-t-il 2001:db8:acad:1:021A:2BFF:FE3C:4D5E ?"

Si aucune réponse → adresse valide
Si NA reçue → conflit, générer une nouvelle adresse
```

#### Étape 6 : Configuration finale
```
Adresse IPv6 : 2001:db8:acad:1:021A:2BFF:FE3C:4D5E/64
Passerelle par défaut : FE80::1
```

### Avantages de SLAAC
- ✅ **Aucun serveur DHCP nécessaire**
- ✅ **Auto-configuration simple**
- ✅ **Pas d'état côté serveur** (stateless)
- ✅ **Rapidité** de configuration

### Inconvénients de SLAAC
- ❌ **Pas d'informations DNS** (nécessite O=1 pour DHCPv6 stateless)
- ❌ **Adresses prévisibles** avec EUI-64 (problème de confidentialité)
- ❌ **Pas de contrôle centralisé** des adresses

---

## 10. DHCPv6 {#dhcpv6}

### Introduction
**DHCPv6** est le protocole DHCP pour IPv6, permettant d'attribuer des adresses et des paramètres de configuration.

### Différences avec DHCP IPv4
- Utilise le **multicast** au lieu du broadcast
- Deux modes : **stateful** et **stateless**
- Fonctionne avec ou **sans SLAAC**

### Adresses multicast DHCPv6
- **Serveurs/Relais DHCPv6** : `FF02::1:2` (link-local)
- **Serveurs DHCPv6** : `FF05::1:3` (site-local)

### Processus DHCPv6 (4 étapes)

#### 1. SOLICIT
- **Client → FF02::1:2** (multicast)
- "Je cherche un serveur DHCPv6"

#### 2. ADVERTISE
- **Serveur → Client** (unicast)
- "Je suis un serveur DHCPv6, voici mes paramètres"

#### 3. REQUEST
- **Client → Serveur** (unicast)
- "J'accepte, envoyez-moi la configuration"

#### 4. REPLY
- **Serveur → Client** (unicast)
- "Voici votre adresse IPv6 et la configuration"

---

## 11. Méthodes d'allocation IPv6 {#methodes-allocation}

### Trois méthodes principales ⚠️ **IMPORTANT**

#### Méthode 1 : SLAAC Only (M=0, O=0)

**Configuration** :
```
Router(config-if)# no ipv6 nd managed-config-flag
Router(config-if)# no ipv6 nd other-config-flag
```

**Processus** :
- Hôte utilise **SLAAC** pour générer son adresse
- **Aucun serveur DHCPv6** nécessaire
- **Pas d'informations DNS** automatiques

**Utilisation** :
- Réseaux simples sans besoin de DNS automatique
- Petits réseaux domestiques

---

#### Méthode 2 : SLAAC + DHCPv6 Stateless (M=0, O=1)

**Configuration** :
```
Router(config-if)# no ipv6 nd managed-config-flag
Router(config-if)# ipv6 nd other-config-flag
```

**Processus** :
1. Hôte utilise **SLAAC** pour générer son adresse (préfixe du RA)
2. Hôte contacte un **serveur DHCPv6** pour obtenir :
   - **Adresses DNS**
   - **Nom de domaine**
   - **Autres paramètres** (NTP, etc.)

**Caractéristiques** :
- DHCPv6 = **stateless** (ne gère pas les adresses)
- Serveur DHCPv6 **ne maintient pas d'état** des adresses allouées
- Hôte génère lui-même son adresse

**Utilisation** :
- Réseaux d'entreprise nécessitant DNS automatique
- **Méthode recommandée** pour la plupart des cas

---

#### Méthode 3 : DHCPv6 Stateful (M=1, O=x)

**Configuration** :
```
Router(config-if)# ipv6 nd managed-config-flag
Router(config-if)# ipv6 nd other-config-flag  # (optionnel)
```

**Processus** :
1. Hôte reçoit le **RA** avec M=1
2. Hôte **NE GÉNÈRE PAS** d'adresse via SLAAC
3. Hôte contacte un **serveur DHCPv6** pour obtenir :
   - **Adresse IPv6 complète**
   - **Passerelle par défaut** (optionnel, généralement LLA du routeur)
   - **DNS, domaine, autres paramètres**

**Caractéristiques** :
- DHCPv6 = **stateful** (gère les adresses)
- Serveur DHCPv6 **maintient un état** des adresses allouées
- **Contrôle centralisé** des adresses
- Similaire à DHCP IPv4

**Utilisation** :
- Réseaux nécessitant un **contrôle strict** des adresses
- Environnements avec **politiques d'adressage** spécifiques
- Traçabilité des adresses (logs serveur DHCPv6)

---

### Comparaison des méthodes

| Méthode | M | O | Adresse | DNS | Serveur DHCPv6 | Contrôle |
|---------|---|---|---------|-----|----------------|----------|
| **SLAAC Only** | 0 | 0 | SLAAC | ❌ Non | ❌ Non requis | ❌ Faible |
| **SLAAC + DHCPv6 Stateless** | 0 | 1 | SLAAC | ✅ Oui | ✅ Requis (stateless) | ⚠️ Partiel |
| **DHCPv6 Stateful** | 1 | x | DHCPv6 | ✅ Oui | ✅ Requis (stateful) | ✅ Total |

---

## 12. Commandes de diagnostic {#diagnostic}

### Commandes ping

**IPv4** :
```
C:\> ping 8.8.8.8
Router# ping 8.8.8.8
```

**IPv6** :
```
C:\> ping 2001:4860:4860::8888
Router# ping ipv6 2001:4860:4860::8888
```

**Options utiles** :
```
ping -t [ip]                    # Ping continu (Windows)
ping -c 10 [ip]                 # 10 pings (Linux)
ping -n 100 [ip]                # 100 pings (Windows)
ping -s 1472 [ip]               # Taille de paquet spécifique (Linux)
ping -l 1472 [ip]               # Taille de paquet spécifique (Windows)
```

### Commandes traceroute

**IPv4** :
```
C:\> tracert 8.8.8.8           # Windows
$ traceroute 8.8.8.8           # Linux
Router# traceroute 8.8.8.8     # Cisco
```

**IPv6** :
```
C:\> tracert 2001:4860:4860::8888      # Windows
$ traceroute6 2001:4860:4860::8888     # Linux
Router# traceroute ipv6 2001:4860:4860::8888  # Cisco
```

### Commandes de vérification ICMPv6 / NDP

**Afficher les voisins IPv6 (cache NDP)** :
```
Router# show ipv6 neighbors
```

**Afficher les messages RA reçus** :
```
Router# show ipv6 routers
```

**Afficher les préfixes annoncés** :
```
Router# show ipv6 interface [interface]
```

**Debug des messages NDP** :
```
Router# debug ipv6 nd
Router# undebug all  # À désactiver après utilisation
```

### Analyse de paquets ICMP

**Wireshark** :
- Filtre ICMPv4 : `icmp`
- Filtre ICMPv6 : `icmpv6`
- Filtre NDP : `icmpv6.type >= 133 && icmpv6.type <= 137`
- Filtre Echo Request/Reply : `icmp.type == 8 || icmp.type == 0`

---

## Résumé des points clés 🎯

### ICMP - Rôles principaux
- ✅ **Messages d'erreur** : signaler problèmes de transmission
- ✅ **Messages d'information** : ping, diagnostic
- ✅ **Contrôle réseau** : redirection, MTU discovery

### ICMPv4 - Messages d'erreur importants
- ✅ **Type 3** : Destination Unreachable (Codes 0-13, **4 codes essentiels**)
  - **Code 0** : Network Unreachable
  - **Code 1** : Host Unreachable
  - **Code 3** : Port Unreachable (traceroute)
  - **Code 4** : Fragmentation Needed (PMTUD)
- ✅ **Type 5** : Redirect
- ✅ **Type 11 Code 0** : TTL Exceeded (traceroute)
- ✅ **Type 12** : Parameter Problem

### ICMPv6 - Messages d'erreur importants
- ✅ **Type 1** : Destination Unreachable (Codes 0-6, **5 codes essentiels**)
  - **Code 0** : No route to destination
  - **Code 1** : Administratively prohibited
  - **Code 3** : Address unreachable
  - **Code 4** : Port unreachable
- ✅ **Type 2** : Packet Too Big (PMTUD obligatoire)
- ✅ **Type 3 Code 0** : Hop Limit Exceeded (traceroute IPv6)
- ✅ **Type 4** : Parameter Problem

### NDP - 5 types de messages
- ✅ **Type 133 (RS)** : Router Solicitation
- ✅ **Type 134 (RA)** : Router Advertisement (flags M, O)
- ✅ **Type 135 (NS)** : Neighbor Solicitation (résolution, DAD)
- ✅ **Type 136 (NA)** : Neighbor Advertisement
- ✅ **Type 137** : Redirect

### Méthodes d'allocation IPv6 ⚠️ **IMPORTANT**
- ✅ **SLAAC Only** (M=0, O=0) : auto-config, pas de DNS
- ✅ **SLAAC + DHCPv6 Stateless** (M=0, O=1) : auto-config + DNS
- ✅ **DHCPv6 Stateful** (M=1) : serveur gère tout

### Diagnostic
- ✅ **ping** : Echo Request (Type 8/128), Echo Reply (Type 0/129)
- ✅ **traceroute** : TTL/Hop Limit Exceeded (Type 11/Type 3)
- ✅ **show ipv6 neighbors** : cache NDP

---

**Prochaine étape** : Module 14 - Couche Transport
