# QCM Module 9 - Résolution d'adresse (Address Resolution)

**Nombre de questions :** 20
**Durée estimée :** 30 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quel est le rôle principal du protocole ARP ?

- [ ] Router les paquets entre réseaux
- [ ] Résoudre les adresses IPv4 en adresses MAC
- [ ] Résoudre les adresses IPv6 en adresses MAC
- [ ] Vérifier la connectivité réseau

---

## Question 2
Lors d'une requête ARP, quelle adresse MAC est utilisée comme destination ?

- [ ] Adresse MAC du destinataire
- [ ] Adresse MAC du routeur
- [ ] FF:FF:FF:FF:FF:FF (broadcast)
- [ ] 00:00:00:00:00:00

---

## Question 3
Dans un message ARP, que représente la valeur "Opcode = 1" ?

- [ ] ARP Reply (réponse)
- [ ] ARP Request (requête)
- [ ] ARP Error
- [ ] ARP Redirect

---

## Question 4
Comment est envoyée une réponse ARP (ARP Reply) ?

- [ ] En broadcast à tous les hôtes
- [ ] En multicast
- [ ] En unicast uniquement à l'émetteur de la requête
- [ ] En anycast

---

## Question 5
Quelle commande Windows affiche la table ARP ?

- [ ] ipconfig /all
- [ ] arp -a
- [ ] show arp
- [ ] netstat -r

---

## Question 6
Quelle commande Cisco IOS efface toutes les entrées dynamiques de la table ARP ?

- [ ] clear ip arp
- [ ] delete arp
- [ ] erase arp-cache
- [ ] no arp

---

## Question 7
Qu'est-ce que l'ARP spoofing (empoisonnement ARP) ?

- [ ] Une technique pour accélérer la résolution ARP
- [ ] Une attaque envoyant de fausses réponses ARP pour détourner le trafic
- [ ] Une méthode de compression des trames Ethernet
- [ ] Un protocole de sécurité pour ARP

---

## Question 8
**Sélectionnez DEUX réponses correctes.**

Quelles protections peuvent être mises en place contre l'ARP spoofing ?

- [ ] DAI (Dynamic ARP Inspection)
- [ ] Port Security
- [ ] DHCP Snooping obligatoire
- [ ] Utiliser uniquement IPv6
- [ ] Désactiver le broadcast

---

## Question 9
Quel protocole remplace ARP pour IPv6 ?

- [ ] ICMPv6
- [ ] NDP (Neighbor Discovery Protocol)
- [ ] DHCPv6
- [ ] ARPv6

---

## Question 10 ⚠️ **IMPORTANT**
Combien de types de messages ICMPv6 NDP existe-t-il principalement ?

- [ ] 3 types
- [ ] 5 types
- [ ] 7 types
- [ ] 10 types

---

## Question 11 ⚠️ **IMPORTANT**
Quel est le type ICMPv6 d'un message **Router Solicitation (RS)** ?

- [ ] Type 133
- [ ] Type 134
- [ ] Type 135
- [ ] Type 136

---

## Question 12 ⚠️ **IMPORTANT**
Quel message NDP un routeur envoie-t-il périodiquement pour annoncer sa présence ?

- [ ] NS (Neighbor Solicitation)
- [ ] NA (Neighbor Advertisement)
- [ ] RA (Router Advertisement) - Type 134
- [ ] RS (Router Solicitation) - Type 133

---

## Question 13 ⚠️ **IMPORTANT**
Quel type de message NDP est utilisé pour résoudre une adresse IPv6 en adresse MAC (équivalent ARP Request) ?

- [ ] Type 133 - RS
- [ ] Type 134 - RA
- [ ] Type 135 - NS (Neighbor Solicitation)
- [ ] Type 136 - NA

---

## Question 14 ⚠️ **IMPORTANT**
Quel est le type ICMPv6 d'un message **Redirect** ?

- [ ] Type 133
- [ ] Type 135
- [ ] Type 136
- [ ] Type 137

---

## Question 15 ⚠️ **IMPORTANT**
**Associez chaque type ICMPv6 NDP à son nom correct. Sélectionnez CINQ réponses.**

- [ ] Type 133 = Router Solicitation (RS)
- [ ] Type 134 = Router Advertisement (RA)
- [ ] Type 135 = Neighbor Solicitation (NS)
- [ ] Type 136 = Neighbor Advertisement (NA)
- [ ] Type 137 = Redirect

---

## Question 16
Quelle est la structure d'une adresse multicast "solicited-node" en IPv6 ?

- [ ] FF02::1
- [ ] FF02::2
- [ ] FF02::1:FF__:____ (3 derniers octets de l'IPv6 cible)
- [ ] FE80::/10

---

## Question 17
Qu'est-ce que le DAD (Duplicate Address Detection) en IPv6 ?

- [ ] Un protocole de routage dynamique
- [ ] Une méthode pour vérifier qu'une adresse IPv6 n'est pas déjà utilisée
- [ ] Un système de chiffrement pour IPv6
- [ ] Un mécanisme de détection d'intrusion

---

## Question 18
**Sélectionnez DEUX réponses correctes.**

Quels sont les flags présents dans un message Router Advertisement (RA) ?

- [ ] M (Managed) - utiliser DHCPv6 pour l'adresse
- [ ] O (Other) - utiliser DHCPv6 pour autres infos (DNS)
- [ ] S (Solicited) - réponse à une sollicitation
- [ ] R (Router) - émetteur est un routeur
- [ ] A (Autonomous) - auto-configuration

---

## Question 19
Quelle commande Cisco IOS affiche la table des voisins IPv6 (cache NDP) ?

- [ ] show ipv6 arp
- [ ] show ipv6 neighbors
- [ ] show ndp cache
- [ ] show ipv6 route

---

## Question 20
**Sélectionnez TROIS différences correctes entre ARP et NDP.**

- [ ] ARP utilise le broadcast, NDP utilise le multicast
- [ ] ARP est Layer 2, NDP est Layer 3 (ICMPv6)
- [ ] ARP supporte l'auto-configuration, NDP non
- [ ] NDP inclut la détection de doublons (DAD), ARP non
- [ ] ARP est plus sécurisé que NDP

---

## Réponses et explications

### Question 1
**Réponse correcte :** Résoudre les adresses IPv4 en adresses MAC

**Explication :**
**ARP (Address Resolution Protocol)** permet de trouver l'adresse MAC correspondant à une adresse IPv4 sur un réseau local. Pour IPv6, on utilise **NDP** (Neighbor Discovery Protocol). ARP ne route pas les paquets et ne vérifie pas directement la connectivité.

---

### Question 2
**Réponse correcte :** FF:FF:FF:FF:FF:FF (broadcast)

**Explication :**
Une **requête ARP** est envoyée en **broadcast** à l'adresse MAC `FF:FF:FF:FF:FF:FF`. Tous les hôtes du réseau local reçoivent la requête, mais seul celui qui possède l'adresse IP cible répond.

---

### Question 3
**Réponse correcte :** ARP Request (requête)

**Explication :**
Le champ "Opcode" dans un message ARP indique le type d'opération :
- **Opcode = 1** : ARP Request (requête)
- **Opcode = 2** : ARP Reply (réponse)

---

### Question 4
**Réponse correcte :** En unicast uniquement à l'émetteur de la requête

**Explication :**
Contrairement à la requête qui est en broadcast, la **réponse ARP** est envoyée en **unicast** directement à l'adresse MAC de l'hôte qui a envoyé la requête. Cela réduit le trafic réseau inutile.

---

### Question 5
**Réponse correcte :** arp -a

**Explication :**
Commandes selon les systèmes :
- **Windows** : `arp -a`
- **Linux** : `arp -n` ou `ip neighbor show`
- **Cisco IOS** : `show ip arp` ou `show arp`

---

### Question 6
**Réponse correcte :** clear ip arp

**Explication :**
Sur Cisco IOS :
- `clear ip arp` : efface toutes les entrées dynamiques
- `clear arp-cache` : alternative
- `clear ip arp [adresse]` : efface une entrée spécifique

---

### Question 7
**Réponse correcte :** Une attaque envoyant de fausses réponses ARP pour détourner le trafic

**Explication :**
L'**ARP spoofing** (empoisonnement ARP) est une attaque où l'attaquant envoie de fausses réponses ARP pour associer son adresse MAC à l'IP d'un autre hôte (souvent la passerelle). Le trafic est alors redirigé vers l'attaquant (**Man-in-the-Middle**), permettant l'interception ou la modification des données.

---

### Question 8
**Réponses correctes :** DAI (Dynamic ARP Inspection), Port Security

**Explication :**
Protections contre l'ARP spoofing :
- **DAI (Dynamic ARP Inspection)** : validation des messages ARP sur les switches Cisco
- **Port Security** : limite les adresses MAC autorisées par port
- **Entrées ARP statiques** : pour serveurs critiques
- **Outils de détection** : arpwatch, XArp

DHCP Snooping aide DAI mais n'est pas une protection directe. IPv6 avec NDP est plus sécurisé mais n'empêche pas tous les problèmes.

---

### Question 9
**Réponse correcte :** NDP (Neighbor Discovery Protocol)

**Explication :**
En IPv6, **NDP (Neighbor Discovery Protocol)** remplace ARP. NDP utilise des messages **ICMPv6** et le **multicast** (au lieu du broadcast). Il offre plus de fonctionnalités : résolution d'adresse, découverte de routeurs, auto-configuration (SLAAC), détection de doublons (DAD).

---

### Question 10 ⚠️ **IMPORTANT**
**Réponse correcte :** 5 types

**Explication :**
Il existe **5 types principaux** de messages ICMPv6 NDP :
1. **Type 133** = Router Solicitation (RS)
2. **Type 134** = Router Advertisement (RA)
3. **Type 135** = Neighbor Solicitation (NS)
4. **Type 136** = Neighbor Advertisement (NA)
5. **Type 137** = Redirect

C'est un point **crucial** à mémoriser pour l'examen CCNA.

---

### Question 11 ⚠️ **IMPORTANT**
**Réponse correcte :** Type 133

**Explication :**
**Router Solicitation (RS) = Type ICMPv6 133**

Un hôte envoie un RS en multicast à `FF02::2` (tous les routeurs) pour demander aux routeurs de s'annoncer immédiatement, sans attendre leur annonce périodique.

---

### Question 12 ⚠️ **IMPORTANT**
**Réponse correcte :** RA (Router Advertisement) - Type 134

**Explication :**
**Router Advertisement (RA) = Type ICMPv6 134**

Les routeurs IPv6 envoient périodiquement des **RA** en multicast à `FF02::1` (tous les nœuds) pour :
- Annoncer leur présence
- Fournir le préfixe du réseau
- Indiquer leur adresse link-local (passerelle par défaut)
- Permettre l'auto-configuration SLAAC

---

### Question 13 ⚠️ **IMPORTANT**
**Réponse correcte :** Type 135 - NS (Neighbor Solicitation)

**Explication :**
**Neighbor Solicitation (NS) = Type ICMPv6 135**

Le NS est l'équivalent de l'ARP Request pour IPv6. Il est utilisé pour :
- **Résoudre une adresse IPv6 en adresse MAC**
- **DAD** (Duplicate Address Detection) : vérifier qu'une adresse n'est pas déjà utilisée
- **NUD** (Neighbor Unreachability Detection) : vérifier qu'un voisin est toujours joignable

Le NS est envoyé à l'adresse multicast "solicited-node" (`FF02::1:FF__:____`), pas en broadcast.

---

### Question 14 ⚠️ **IMPORTANT**
**Réponse correcte :** Type 137

**Explication :**
**Redirect = Type ICMPv6 137**

Un routeur envoie un message Redirect à un hôte pour l'informer qu'un meilleur chemin existe vers une destination. L'hôte met alors à jour sa table de routage pour utiliser le routeur optimal.

---

### Question 15 ⚠️ **IMPORTANT**
**Réponses correctes :** Toutes les 5 réponses sont correctes

**Explication :**
Les **5 types de messages ICMPv6 NDP** à connaître absolument :

| Type | Nom | Rôle |
|------|-----|------|
| **133** | **RS** - Router Solicitation | Demander aux routeurs de s'annoncer |
| **134** | **RA** - Router Advertisement | Annonce des routeurs (préfixe, passerelle) |
| **135** | **NS** - Neighbor Solicitation | Résoudre IPv6 → MAC (= ARP Request) |
| **136** | **NA** - Neighbor Advertisement | Réponse à un NS (= ARP Reply) |
| **137** | **Redirect** | Informer d'un meilleur chemin |

**Astuce mnémotechnique** : 133, 134, 135, 136, 137 sont **consécutifs** !

---

### Question 16
**Réponse correcte :** FF02::1:FF__:____ (3 derniers octets de l'IPv6 cible)

**Explication :**
L'adresse multicast "solicited-node" est construite ainsi :
- Préfixe : `FF02::1:FF`
- Suffixe : **3 derniers octets** (24 bits de poids faible) de l'adresse IPv6 cible

**Exemple** :
- IPv6 cible : `2001:db8:acad:1::20`
- Solicited-node : `FF02::1:FF00:0020`

Cette approche est plus efficace que le broadcast car seuls les hôtes concernés traitent le message.

---

### Question 17
**Réponse correcte :** Une méthode pour vérifier qu'une adresse IPv6 n'est pas déjà utilisée

**Explication :**
**DAD (Duplicate Address Detection)** est un mécanisme IPv6 qui vérifie qu'une adresse n'est pas déjà utilisée avant de l'activer.

**Processus** :
1. L'hôte envoie un **NS** vers sa propre adresse (solicited-node multicast)
2. Si **aucune réponse** → adresse disponible ✅
3. Si **réponse NA** reçue → conflit détecté ❌ → ne pas utiliser cette adresse

DAD utilise les messages **Neighbor Solicitation (Type 135)**.

---

### Question 18
**Réponses correctes :** M (Managed), O (Other)

**Explication :**
Les **flags dans les Router Advertisements (RA)** :

- **M (Managed Address Configuration)** : 
  - Si M=1 → utiliser DHCPv6 pour obtenir l'adresse complète
  - Si M=0 → utiliser SLAAC (auto-configuration)

- **O (Other Configuration)** :
  - Si O=1 → utiliser DHCPv6 pour obtenir d'autres informations (DNS, nom de domaine)
  - Si O=0 → pas besoin de DHCPv6 pour les infos additionnelles

**Flags S, R, A** existent dans d'autres messages NDP (NA), pas dans RA.

---

### Question 19
**Réponse correcte :** show ipv6 neighbors

**Explication :**
Sur Cisco IOS :
- `show ipv6 neighbors` : affiche la table des voisins IPv6 (cache NDP)
- `clear ipv6 neighbors` : efface le cache NDP

**Exemple de sortie** :
```
IPv6 Address                    Age  Link-layer Addr  State    Interface
2001:DB8:ACAD:1::10             0    0030.a3e8.1234   REACH    Gi0/0
FE80::A8BB:CCFF:FE00:6700       1    aabb.cc00.6700   STALE    Gi0/1
```

**États** : INCMP, REACH, STALE, DELAY, PROBE

---

### Question 20
**Réponses correctes :** ARP utilise le broadcast, NDP utilise le multicast / ARP est Layer 2, NDP est Layer 3 (ICMPv6) / NDP inclut la détection de doublons (DAD), ARP non

**Explication :**
**Comparaison ARP vs NDP** :

| Critère | ARP (IPv4) | NDP (IPv6) |
|---------|-----------|-----------|
| **Couche** | Layer 2 | Layer 3 (ICMPv6) ✅ |
| **Requête** | Broadcast (FF:FF:FF:FF:FF:FF) | Multicast solicited-node ✅ |
| **Auto-configuration** | Non (nécessite DHCP) | Oui (SLAAC) |
| **Détection de doublons** | Non | Oui (DAD) ✅ |
| **Sécurité** | Vulnérable (spoofing) | Meilleure (SEND possible) |

**Erreurs** :
- ❌ NDP supporte l'auto-configuration (SLAAC), PAS ARP
- ❌ NDP est considéré plus sécurisé qu'ARP (SEcure ND - SEND disponible)
