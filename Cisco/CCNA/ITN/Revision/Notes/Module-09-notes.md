# Module 9 - Résolution d'adresse (Address Resolution)

## Table des matières
1. [Introduction à la résolution d'adresse](#introduction)
2. [Adresses MAC et IP](#mac-ip)
3. [ARP - Address Resolution Protocol](#arp)
4. [Fonctionnement d'ARP](#arp-fonctionnement)
5. [Table ARP](#table-arp)
6. [Problèmes ARP](#problèmes-arp)
7. [IPv6 Neighbor Discovery Protocol (NDP)](#ndp)
8. [Messages ICMPv6 de NDP](#messages-ndp)
9. [Comparaison ARP vs NDP](#arp-vs-ndp)
10. [Commandes IOS utiles](#commandes)

---

## 1. Introduction à la résolution d'adresse {#introduction}

### Problématique
Pour communiquer sur un réseau local (LAN), les périphériques ont besoin de **deux types d'adresses** :
- **Adresse IP (Layer 3)** : identifie logiquement l'hôte sur le réseau
- **Adresse MAC (Layer 2)** : identifie physiquement la carte réseau

**Question** : Comment un périphérique connaît-il l'adresse MAC correspondant à une adresse IP ?

**Réponse** : Grâce aux **protocoles de résolution d'adresse** :
- **ARP** pour IPv4
- **NDP** pour IPv6

### Scénarios de communication

#### 1. Communication sur le même réseau local
- L'hôte source doit connaître l'**adresse MAC de destination**
- Utilisation d'**ARP (IPv4)** ou **NDP (IPv6)** pour résoudre l'adresse

#### 2. Communication vers un réseau distant
- L'hôte source doit connaître l'**adresse MAC de la passerelle par défaut**
- Le paquet est envoyé au routeur avec l'IP de destination finale
- Mais l'adresse MAC de destination = MAC de la passerelle

---

## 2. Adresses MAC et IP {#mac-ip}

### Rappel : Adresse MAC
- **48 bits** (6 octets) : `00:1A:2B:3C:4D:5E`
- Notation hexadécimale
- Gravée sur la carte réseau (NIC)
- Composée de :
  - **OUI (24 bits)** : identifiant du fabricant
  - **Device ID (24 bits)** : identifiant unique

### Rappel : Adresse IP
- **IPv4** : 32 bits (ex: 192.168.1.10)
- **IPv6** : 128 bits (ex: 2001:db8::1)
- Attribuée par configuration (statique ou DHCP)

### Pourquoi deux types d'adresses ?
- **Adresse IP** : routage sur Internet (Layer 3)
- **Adresse MAC** : livraison locale sur le LAN (Layer 2)
- Les routeurs changent les adresses MAC à chaque saut
- Les adresses IP restent identiques de bout en bout

---

## 3. ARP - Address Resolution Protocol {#arp}

### Rôle d'ARP
**ARP** résout les adresses **IPv4** en adresses **MAC** sur un réseau local.

### Caractéristiques d'ARP
- Protocole de **couche 2** (Data Link)
- Utilisé uniquement pour **IPv4**
- Fonctionne par **requête/réponse** (Request/Reply)
- Utilise la **diffusion (broadcast)** pour les requêtes
- Maintient une **table ARP** (cache) pour éviter les requêtes répétées

### Encapsulation ARP
Un message ARP est **encapsulé directement** dans une trame Ethernet :
- **Type Ethernet** : `0x0806` (ARP)
- Pas d'entête IP (ARP opère au niveau Layer 2)

---

## 4. Fonctionnement d'ARP {#arp-fonctionnement}

### Scénario : PC1 (192.168.1.10) veut communiquer avec PC2 (192.168.1.20)

#### Étape 1 : Vérification de la table ARP
PC1 consulte sa **table ARP** pour voir si l'adresse MAC de 192.168.1.20 est déjà connue :
```
C:\> arp -a
```
- Si l'entrée existe → utiliser l'adresse MAC du cache
- Si l'entrée n'existe pas → envoyer une requête ARP

#### Étape 2 : Requête ARP (ARP Request) - BROADCAST
PC1 envoie une **requête ARP en broadcast** :

**Informations de la trame** :
- **MAC source** : `AA:AA:AA:AA:AA:AA` (MAC de PC1)
- **MAC destination** : `FF:FF:FF:FF:FF:FF` (broadcast)
- **Type** : 0x0806 (ARP)

**Contenu du message ARP** :
- **Opcode** : 1 (Request)
- **Sender MAC** : `AA:AA:AA:AA:AA:AA` (MAC de PC1)
- **Sender IP** : `192.168.1.10`
- **Target MAC** : `00:00:00:00:00:00` (inconnu)
- **Target IP** : `192.168.1.20` (adresse recherchée)

**Question posée** : *"Qui a l'adresse IP 192.168.1.20 ? Merci de répondre à AA:AA:AA:AA:AA:AA."*

#### Étape 3 : Réception par tous les hôtes du LAN
- Le **switch** reçoit la trame en **broadcast**
- Il la **transmet sur tous les ports** (sauf le port source)
- **Tous les hôtes** du réseau local reçoivent la requête

#### Étape 4 : Traitement de la requête ARP
Chaque hôte examine le champ **Target IP** :
- Si Target IP ≠ mon IP → **ignorer** la requête
- Si Target IP = mon IP → **répondre** avec une ARP Reply

#### Étape 5 : Réponse ARP (ARP Reply) - UNICAST
PC2 (192.168.1.20) envoie une **réponse ARP en unicast** :

**Informations de la trame** :
- **MAC source** : `BB:BB:BB:BB:BB:BB` (MAC de PC2)
- **MAC destination** : `AA:AA:AA:AA:AA:AA` (MAC de PC1, unicast)
- **Type** : 0x0806 (ARP)

**Contenu du message ARP** :
- **Opcode** : 2 (Reply)
- **Sender MAC** : `BB:BB:BB:BB:BB:BB` (MAC de PC2)
- **Sender IP** : `192.168.1.20`
- **Target MAC** : `AA:AA:AA:AA:AA:AA` (MAC de PC1)
- **Target IP** : `192.168.1.10`

**Réponse** : *"Je suis 192.168.1.20 et mon adresse MAC est BB:BB:BB:BB:BB:BB."*

#### Étape 6 : Mise à jour de la table ARP
PC1 reçoit la réponse et **enregistre** l'information dans sa table ARP :
```
Internet Address      Physical Address      Type
192.168.1.20          BB-BB-BB-BB-BB-BB     dynamic
```

#### Étape 7 : Communication
Maintenant, PC1 peut **encapsuler les paquets IP** dans des trames Ethernet avec :
- **MAC destination** : `BB:BB:BB:BB:BB:BB`
- **IP destination** : `192.168.1.20`

---

## 5. Table ARP {#table-arp}

### Fonction du cache ARP
La **table ARP** stocke les correspondances **IP ↔ MAC** pour éviter de répéter les requêtes ARP à chaque envoi de paquet.

### Caractéristiques
- **Mémoire volatile** : les entrées sont perdues au redémarrage
- **Entrées temporaires** : expiration après un certain temps (timeout)
- **Durée de vie typique** :
  - Windows : 2 minutes (si inutilisé) à 10 minutes (si utilisé)
  - Linux/Cisco : 4 heures par défaut

### Types d'entrées ARP

| Type | Description |
|------|-------------|
| **Static** | Ajoutée manuellement, permanente jusqu'à suppression |
| **Dynamic** | Ajoutée automatiquement, expire après timeout |

### Affichage de la table ARP

**Windows** :
```
C:\> arp -a
```

**Linux** :
```
$ arp -n
$ ip neighbor show
```

**Cisco IOS** :
```
Router# show ip arp
Router# show arp
```

### Exemple de table ARP

```
Internet Address      Physical Address      Type
192.168.1.1           00-1A-2B-3C-4D-5E     dynamic
192.168.1.20          AA-BB-CC-DD-EE-FF     dynamic
192.168.1.100         11-22-33-44-55-66     static
```

### Gestion de la table ARP

**Windows** :
```
C:\> arp -a                          # Afficher la table ARP
C:\> arp -d                          # Supprimer toutes les entrées
C:\> arp -d 192.168.1.20             # Supprimer une entrée spécifique
C:\> arp -s 192.168.1.50 AA-BB-CC-DD-EE-FF   # Ajouter une entrée statique
```

**Linux** :
```
$ arp -n                             # Afficher la table ARP
$ sudo arp -d 192.168.1.20           # Supprimer une entrée
$ sudo arp -s 192.168.1.50 AA:BB:CC:DD:EE:FF  # Ajouter une entrée statique
```

**Cisco IOS** :
```
Router# clear ip arp                 # Effacer toutes les entrées dynamiques
Router# clear arp-cache              # Effacer le cache ARP
Router(config)# arp 192.168.1.50 AABB.CCDD.EEFF ARPA   # Entrée statique
```

---

## 6. Problèmes ARP {#problèmes-arp}

### ARP Spoofing (Empoisonnement ARP)
**Attaque** : un attaquant envoie de fausses réponses ARP pour **détourner le trafic**

**Principe** :
1. L'attaquant envoie des ARP Reply non sollicitées
2. Il associe **son adresse MAC** à l'IP de la passerelle ou d'un autre hôte
3. Les victimes mettent à jour leur table ARP avec la fausse information
4. Le trafic est redirigé vers l'attaquant (**Man-in-the-Middle**)

**Conséquences** :
- Interception du trafic
- Vol de données sensibles
- Déni de service (DoS)

**Protections** :
- **DAI (Dynamic ARP Inspection)** : validation des messages ARP sur les switchs Cisco
- **Port Security** : limiter les adresses MAC par port
- **Entrées ARP statiques** : pour les serveurs critiques
- **Outils de détection** : arpwatch, XArp

### Problèmes de connectivité liés à ARP

#### Entrée ARP incorrecte
**Symptôme** : impossible de joindre un hôte spécifique
**Cause** : entrée ARP corrompue ou obsolète
**Solution** :
```
C:\> arp -d [ip-address]    # Supprimer l'entrée
C:\> ping [ip-address]       # Régénérer l'entrée
```

#### Table ARP pleine
**Symptôme** : nouvelles connexions échouent
**Cause** : trop d'entrées ARP (attaque ou réseau surchargé)
**Solution** : augmenter le timeout ARP ou utiliser VLANs

---

## 7. IPv6 Neighbor Discovery Protocol (NDP) {#ndp}

### Introduction à NDP
**NDP** remplace plusieurs protocoles IPv4 :
- **ARP** : résolution d'adresse
- **ICMP Router Discovery** : découverte des routeurs
- **ICMP Redirect** : redirection

### Caractéristiques de NDP
- Protocole de **couche 3** (basé sur ICMPv6)
- Utilise des messages **ICMPv6** (type 133-137)
- Utilise le **multicast** au lieu du broadcast
- Plus efficace et sécurisé qu'ARP

### Avantages de NDP sur ARP
- ✅ **Multicast** : moins de perturbations réseau (vs broadcast)
- ✅ **Auto-configuration (SLAAC)** : adressage sans serveur DHCP
- ✅ **Détection de doublons (DAD)** : évite les conflits d'adresse
- ✅ **Détection d'inaccessibilité** : vérification périodique des voisins
- ✅ **Support de la mobilité** : changement de réseau facilité

---

## 8. Messages ICMPv6 de NDP {#messages-ndp}

### Types de messages NDP ⚠️ **SECTION IMPORTANTE**

| Type ICMPv6 | Nom | Description |
|-------------|-----|-------------|
| **133** | **RS** - Router Solicitation | Demande d'information aux routeurs |
| **134** | **RA** - Router Advertisement | Annonce des routeurs (préfixe, passerelle) |
| **135** | **NS** - Neighbor Solicitation | Recherche d'un voisin (= ARP Request) |
| **136** | **NA** - Neighbor Advertisement | Réponse du voisin (= ARP Reply) |
| **137** | **Redirect** | Redirection vers un meilleur routeur |

### 1. Router Solicitation (RS) - Type 133

**Rôle** : demander aux routeurs de s'annoncer

**Envoyé par** : hôtes (au démarrage ou lors de la connexion au réseau)

**Destination** : 
- **Adresse multicast** : `FF02::2` (tous les routeurs sur le lien local)

**Contenu** :
- Demande aux routeurs d'envoyer immédiatement un RA (sans attendre la période d'annonce)

**Scénario** :
```
Hôte → FF02::2 (tous les routeurs)
"Y a-t-il des routeurs sur ce réseau ? Merci de vous annoncer."
```

---

### 2. Router Advertisement (RA) - Type 134

**Rôle** : annoncer la présence d'un routeur et fournir des informations de configuration

**Envoyé par** : routeurs IPv6

**Destination** :
- **Réponse à RS** : unicast vers l'hôte qui a demandé
- **Annonce périodique** : multicast `FF02::1` (tous les nœuds)

**Informations fournies** :
- **Préfixe IPv6** du réseau (ex: 2001:db8:acad:1::/64)
- **Longueur du préfixe** (ex: /64)
- **Adresse de la passerelle par défaut** (adresse link-local du routeur)
- **Durée de vie du préfixe**
- **Flags** :
  - **M (Managed)** : si 1 → utiliser DHCPv6 pour obtenir l'adresse
  - **O (Other)** : si 1 → utiliser DHCPv6 pour d'autres infos (DNS, domaine)
- **Intervalle de retransmission**

**Scénario** :
```
Routeur → FF02::1 (tous les nœuds)
"Je suis un routeur. Voici le préfixe : 2001:db8:acad:1::/64
Mon adresse link-local (passerelle) : FE80::1"
```

**Auto-configuration SLAAC** :
Grâce aux RA, un hôte peut :
1. Générer automatiquement son **adresse IPv6** (préfixe + Interface ID)
2. Configurer sa **passerelle par défaut** (adresse link-local du routeur)

---

### 3. Neighbor Solicitation (NS) - Type 135

**Rôle** : découvrir l'adresse MAC d'un voisin IPv6 (équivalent ARP Request)

**Envoyé par** : hôte ou routeur

**Destination** :
- **Adresse multicast "solicited-node"** : `FF02::1:FF__:____` (3 derniers octets de l'IPv6 cible)
- Plus efficace que le broadcast (seulement les hôtes concernés traitent le message)

**Utilisations** :
1. **Résolution d'adresse** : trouver l'adresse MAC d'un voisin
2. **DAD (Duplicate Address Detection)** : vérifier qu'une adresse n'est pas déjà utilisée
3. **NUD (Neighbor Unreachability Detection)** : vérifier qu'un voisin est toujours joignable

**Exemple de résolution d'adresse** :
```
PC1 veut envoyer un paquet à 2001:db8:acad:1::20

PC1 → FF02::1:FF00:0020 (solicited-node multicast)
"Qui a l'adresse 2001:db8:acad:1::20 ? Merci de répondre."
```

**Exemple DAD (Duplicate Address Detection)** :
Avant d'utiliser une nouvelle adresse, l'hôte vérifie qu'elle n'est pas déjà prise :
```
PC1 → FF02::1:FF00:0010 (solicited-node de sa propre adresse)
"Quelqu'un utilise-t-il 2001:db8:acad:1::10 ?"
Si aucune réponse → adresse disponible
Si réponse → conflit détecté → ne pas utiliser cette adresse
```

---

### 4. Neighbor Advertisement (NA) - Type 136

**Rôle** : répondre à un NS ou annoncer un changement d'adresse MAC (équivalent ARP Reply)

**Envoyé par** : hôte ou routeur qui possède l'adresse recherchée

**Destination** :
- **Réponse à un NS** : unicast vers l'émetteur du NS
- **Annonce spontanée** : multicast `FF02::1` (tous les nœuds)

**Flags** :
- **R (Router)** : si 1 → l'émetteur est un routeur
- **S (Solicited)** : si 1 → réponse à un NS
- **O (Override)** : si 1 → mettre à jour le cache même si une entrée existe

**Exemple** :
```
PC2 → PC1 (unicast)
"Oui, je suis 2001:db8:acad:1::20 et mon adresse MAC est BB:BB:BB:BB:BB:BB."
```

---

### 5. Redirect - Type 137

**Rôle** : informer un hôte qu'un meilleur chemin existe vers une destination

**Envoyé par** : routeur

**Destination** : unicast vers l'hôte concerné

**Scénario** :
1. Un hôte envoie un paquet à sa passerelle par défaut (Routeur 1)
2. Routeur 1 détermine que Routeur 2 est sur le même lien et constitue un meilleur chemin
3. Routeur 1 transmet le paquet ET envoie un Redirect à l'hôte
4. L'hôte met à jour sa table et envoie les prochains paquets directement à Routeur 2

---

## 9. Comparaison ARP vs NDP {#arp-vs-ndp}

| Critère | ARP (IPv4) | NDP (IPv6) |
|---------|-----------|-----------|
| **Couche** | Layer 2 | Layer 3 (ICMPv6) |
| **Encapsulation** | Directement dans trame Ethernet | Dans paquet IPv6 |
| **Type Ethernet** | 0x0806 | 0x86DD (IPv6) |
| **Requête** | Broadcast (FF:FF:FF:FF:FF:FF) | Multicast solicited-node (FF02::1:FF__:____) |
| **Réponse** | Unicast | Unicast |
| **Messages** | Request, Reply | NS, NA, RS, RA, Redirect |
| **Auto-configuration** | Non (nécessite DHCP) | Oui (SLAAC via RA) |
| **Détection de doublons** | Non | Oui (DAD avec NS) |
| **Découverte routeur** | Non (ICMP séparé) | Oui (RS/RA) |
| **Sécurité** | Vulnérable (spoofing) | Meilleure (SEcure ND - SEND possible) |
| **Impact réseau** | Broadcast = beaucoup de trafic | Multicast = trafic ciblé |

---

## 10. Commandes IOS utiles {#commandes}

### Affichage des voisins IPv6 (NDP)

```
Router# show ipv6 neighbors
```

**Exemple de sortie** :
```
IPv6 Address                              Age Link-layer Addr State Interface
2001:DB8:ACAD:1::10                       0   0030.a3e8.1234 REACH Gi0/0
FE80::A8BB:CCFF:FE00:6700                 1   aabb.cc00.6700 STALE Gi0/1
```

**Colonnes** :
- **IPv6 Address** : adresse IPv6 du voisin
- **Age** : temps (en minutes) depuis la dernière confirmation
- **Link-layer Addr** : adresse MAC du voisin
- **State** : état de la découverte (voir ci-dessous)
- **Interface** : interface du routeur connectée au voisin

### États de la découverte de voisins (Neighbor Discovery States)

| État | Description |
|------|-------------|
| **INCMP** (Incomplete) | Résolution en cours, NS envoyé, en attente de NA |
| **REACH** (Reachable) | Voisin joignable, communication récente confirmée |
| **STALE** (Périmé) | Entrée expirée, aucune communication récente |
| **DELAY** | En attente de confirmation de joignabilité |
| **PROBE** | Envoi de NS pour vérifier la joignabilité |

### Effacer le cache des voisins IPv6

```
Router# clear ipv6 neighbors
Router# clear ipv6 neighbors [ipv6-address]
```

### Affichage de la table ARP (IPv4)

```
Router# show ip arp
Router# show arp
```

**Exemple de sortie** :
```
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  192.168.1.10           5    aabb.cc00.1000  ARPA   GigabitEthernet0/0
Internet  192.168.1.20           2    aabb.cc00.2000  ARPA   GigabitEthernet0/0
```

### Effacer le cache ARP

```
Router# clear ip arp
Router# clear arp-cache
```

### Vérification de la résolution d'adresse

**IPv4** :
```
Router# ping 192.168.1.10
Router# show ip arp | include 192.168.1.10
```

**IPv6** :
```
Router# ping ipv6 2001:db8:acad:1::10
Router# show ipv6 neighbors | include 2001:db8:acad:1::10
```

### Debug des messages NDP

```
Router# debug ipv6 nd
```

**Affiche** :
- RS (Router Solicitation)
- RA (Router Advertisement)
- NS (Neighbor Solicitation)
- NA (Neighbor Advertisement)
- Redirect

**⚠️ Désactiver après utilisation** :
```
Router# no debug ipv6 nd
Router# undebug all
```

---

## Résumé des points clés 🎯

### ARP (IPv4)
- ✅ Résout **IPv4 → MAC**
- ✅ Utilise le **broadcast** (FF:FF:FF:FF:FF:FF)
- ✅ Messages : **ARP Request** (broadcast) et **ARP Reply** (unicast)
- ✅ Table ARP : cache temporaire (expire après timeout)
- ⚠️ Vulnérable aux attaques de **spoofing**

### NDP (IPv6)
- ✅ Remplace ARP, ICMP Router Discovery, ICMP Redirect
- ✅ Utilise le **multicast solicited-node** (plus efficace que broadcast)
- ✅ **5 types de messages ICMPv6** :
  - **RS (133)** : demande d'annonce aux routeurs
  - **RA (134)** : annonce du routeur (SLAAC)
  - **NS (135)** : recherche d'un voisin (= ARP Request)
  - **NA (136)** : réponse du voisin (= ARP Reply)
  - **Redirect (137)** : meilleur chemin disponible
- ✅ **DAD** : détection des doublons d'adresse
- ✅ **SLAAC** : auto-configuration sans DHCP

### Commandes clés
- `show ip arp` : afficher la table ARP (IPv4)
- `show ipv6 neighbors` : afficher les voisins IPv6
- `clear ip arp` : effacer le cache ARP
- `clear ipv6 neighbors` : effacer le cache NDP
- `debug ipv6 nd` : surveiller les messages NDP (attention à désactiver après)

---

**Prochaine étape** : Module 10 - Configuration de base d'un routeur
