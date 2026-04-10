# QCM Module 13 - ICMP et protocoles de connectivité

**Nombre de questions :** 20
**Durée estimée :** 30 minutes
**Seuil de réussite :** 75%

---

## Question 1
Quelle est la couche OSI à laquelle opère le protocole ICMP ?

- [ ] Couche 2 (Data Link)
- [ ] Couche 3 (Network)
- [ ] Couche 4 (Transport)
- [ ] Couche 7 (Application)

---

## Question 2
Quel message ICMPv4 Type 3 Code 0 signifie-t-il ?

- [ ] Host Unreachable
- [ ] Network Unreachable
- [ ] Port Unreachable
- [ ] Fragmentation Needed

---

## Question 3
Un routeur n'a pas de route vers le réseau de destination. Quel message ICMPv4 envoie-t-il ?

- [ ] Type 3 Code 0 (Network Unreachable)
- [ ] Type 3 Code 1 (Host Unreachable)
- [ ] Type 3 Code 3 (Port Unreachable)
- [ ] Type 11 Code 0 (TTL Exceeded)

---

## Question 4
Quel code ICMPv4 Type 3 est utilisé par traceroute pour détecter la destination finale ?

- [ ] Code 0 (Network Unreachable)
- [ ] Code 1 (Host Unreachable)
- [ ] Code 3 (Port Unreachable)
- [ ] Code 4 (Fragmentation Needed)

---

## Question 5
Qu'indique le message ICMPv4 Type 3 Code 4 ?

- [ ] Le routeur ne connaît pas la destination
- [ ] Le paquet est trop grand pour le MTU et le bit DF=1
- [ ] Le port UDP est fermé
- [ ] L'hôte ne répond pas

---

## Question 6
Quel est le rôle du message ICMPv4 Type 11 Code 0 ?

- [ ] Indiquer qu'un port est fermé
- [ ] Indiquer que le TTL a atteint 0 pendant le transit
- [ ] Indiquer une redirection vers un meilleur chemin
- [ ] Indiquer un problème d'entête IP

---

## Question 7
Comment traceroute utilise-t-il le TTL pour découvrir le chemin réseau ?

- [ ] En envoyant des paquets avec TTL croissant (1, 2, 3...)
- [ ] En envoyant des paquets avec TTL décroissant (255, 254, 253...)
- [ ] En envoyant tous les paquets avec TTL=1
- [ ] En n'utilisant pas le TTL

---

## Question 8
Quels sont les types de messages ICMP utilisés par la commande ping ? **(Sélectionner 2 réponses)**

- [ ] Type 8 (Echo Request)
- [ ] Type 0 (Echo Reply)
- [ ] Type 3 (Destination Unreachable)
- [ ] Type 11 (Time Exceeded)

---

## Question 9
Quel message ICMPv6 Type 1 est l'équivalent de ICMPv4 Type 3 Code 0 et Code 1 ?

- [ ] Type 1 Code 0 (No route to destination)
- [ ] Type 1 Code 1 (Administratively prohibited)
- [ ] Type 1 Code 3 (Address unreachable)
- [ ] Type 1 Code 4 (Port unreachable)

---

## Question 10
Quelle différence majeure existe entre le traitement des paquets trop grands en IPv4 et IPv6 ?

- [ ] IPv4 utilise Type 2, IPv6 utilise Type 3 Code 4
- [ ] IPv4 utilise Type 3 Code 4, IPv6 utilise Type 2 (Packet Too Big)
- [ ] IPv6 ne gère pas les paquets trop grands
- [ ] Il n'y a aucune différence

---

## Question 11
Quel message ICMPv6 est utilisé par traceroute pour détecter les routeurs intermédiaires ?

- [ ] Type 1 Code 4 (Port Unreachable)
- [ ] Type 2 (Packet Too Big)
- [ ] Type 3 Code 0 (Hop Limit Exceeded)
- [ ] Type 4 (Parameter Problem)

---

## Question 12
Quels sont les 5 types de messages NDP ? **(Sélectionner 5 réponses)**

- [ ] Type 133 (Router Solicitation - RS)
- [ ] Type 134 (Router Advertisement - RA)
- [ ] Type 135 (Neighbor Solicitation - NS)
- [ ] Type 136 (Neighbor Advertisement - NA)
- [ ] Type 137 (Redirect)
- [ ] Type 138 (Router Renumbering)

---

## Question 13
À quelle adresse multicast un hôte envoie-t-il un Router Solicitation (RS) ?

- [ ] FF02::1 (tous les nœuds)
- [ ] FF02::2 (tous les routeurs)
- [ ] FF02::5 (routeurs OSPF)
- [ ] FF02::1:2 (serveurs DHCPv6)

---

## Question 14
Quelles informations le Router Advertisement (RA) fournit-il ? **(Sélectionner 3 réponses)**

- [ ] Préfixe IPv6 du réseau
- [ ] Flags M et O pour la configuration
- [ ] Adresse Link-Local du routeur (passerelle par défaut)
- [ ] Adresse MAC du routeur

---

## Question 15
Quelles sont les utilisations du Neighbor Solicitation (NS) ? **(Sélectionner 3 réponses)**

- [ ] Résolution d'adresse IPv6 en MAC (équivalent ARP)
- [ ] DAD (Duplicate Address Detection)
- [ ] NUD (Neighbor Unreachability Detection)
- [ ] Annonce de routeur

---

## Question 16
Quelle adresse multicast est utilisée pour envoyer un Neighbor Solicitation ?

- [ ] FF02::1 (tous les nœuds)
- [ ] FF02::2 (tous les routeurs)
- [ ] Adresse solicited-node (FF02::1:FF...)
- [ ] Adresse unicast du destinataire

---

## Question 17
Quelles sont les 3 méthodes d'allocation IPv6 ? **(Sélectionner 3 réponses)**

- [ ] SLAAC Only (M=0, O=0)
- [ ] SLAAC + DHCPv6 Stateless (M=0, O=1)
- [ ] DHCPv6 Stateful (M=1)
- [ ] APIPA IPv6

---

## Question 18
Avec SLAAC Only (M=0, O=0), l'hôte peut-il obtenir automatiquement les adresses DNS ?

- [ ] Oui, via SLAAC
- [ ] Oui, via DHCPv6
- [ ] Non, il faut configurer manuellement ou utiliser O=1
- [ ] Oui, via NDP

---

## Question 19
Quelle méthode est recommandée pour la plupart des déploiements IPv6 en entreprise ?

- [ ] SLAAC Only (M=0, O=0)
- [ ] SLAAC + DHCPv6 Stateless (M=0, O=1)
- [ ] DHCPv6 Stateful (M=1)
- [ ] Configuration manuelle uniquement

---

## Question 20
Dans le processus SLAAC, quelle méthode permet de vérifier qu'une adresse IPv6 n'est pas déjà utilisée ?

- [ ] Router Advertisement (RA)
- [ ] Neighbor Solicitation (NS) - DAD
- [ ] Neighbor Advertisement (NA)
- [ ] Ping vers l'adresse

---

## Réponses et explications

### Question 1
**Réponse correcte :** B (Couche 3 - Network)

**Explication :**
ICMP (Internet Control Message Protocol) est un protocole de **couche 3** (Network Layer). Il est encapsulé directement dans des paquets IP et sert à transporter des messages d'erreur et d'information pour le protocole IP. ICMP ne transporte pas de données utilisateur mais fournit un mécanisme de contrôle et de diagnostic pour les réseaux IP.

---

### Question 2
**Réponse correcte :** B (Network Unreachable)

**Explication :**
ICMPv4 Type 3 Code 0 signifie **Network Unreachable**. Ce message est envoyé par un routeur lorsqu'il n'a **aucune route** vers le réseau de destination dans sa table de routage. C'est l'un des 4 codes essentiels du Type 3 à connaître absolument pour l'examen CCNA.

---

### Question 3
**Réponse correcte :** A (Type 3 Code 0 - Network Unreachable)

**Explication :**
Lorsqu'un routeur n'a pas de route vers le réseau de destination, il envoie un message **ICMPv4 Type 3 Code 0 (Network Unreachable)** à la source. Ce message indique que le routeur ne peut pas transmettre le paquet car il ne connaît pas de chemin vers le réseau demandé. Le paquet est alors abandonné.

---

### Question 4
**Réponse correcte :** C (Code 3 - Port Unreachable)

**Explication :**
Traceroute utilise une technique astucieuse : il envoie des paquets **UDP vers des ports élevés** (non utilisés). Lorsque la destination reçoit le paquet, elle répond avec **ICMPv4 Type 3 Code 3 (Port Unreachable)**, indiquant que le port n'est pas ouvert. C'est ainsi que traceroute sait qu'il a atteint la destination finale.

---

### Question 5
**Réponse correcte :** B (Le paquet est trop grand pour le MTU et le bit DF=1)

**Explication :**
ICMPv4 Type 3 Code 4 signifie **Fragmentation Needed but DF set**. Ce message est envoyé par un routeur lorsque :
- Le paquet dépasse le MTU du lien suivant
- Le bit **DF (Don't Fragment)** est positionné à 1
- Le routeur ne peut donc pas fragmenter le paquet

Ce mécanisme est utilisé pour **Path MTU Discovery (PMTUD)**.

---

### Question 6
**Réponse correcte :** B (Indiquer que le TTL a atteint 0 pendant le transit)

**Explication :**
ICMPv4 Type 11 Code 0 signifie **TTL Exceeded in Transit**. Lorsque le TTL (Time To Live) d'un paquet atteint 0, le routeur rejette le paquet et envoie ce message à la source. Ce mécanisme :
- Empêche les boucles de routage infinies
- Est utilisé par **traceroute** pour découvrir le chemin réseau

---

### Question 7
**Réponse correcte :** A (En envoyant des paquets avec TTL croissant 1, 2, 3...)

**Explication :**
Traceroute fonctionne ainsi :
1. Envoie un paquet avec TTL=1 → le 1er routeur répond ICMPv4 Type 11 Code 0
2. Envoie un paquet avec TTL=2 → le 2e routeur répond ICMPv4 Type 11 Code 0
3. Continue jusqu'à atteindre la destination → répond ICMPv4 Type 3 Code 3

Chaque routeur révèle ainsi son identité en répondant quand le TTL atteint 0.

---

### Question 8
**Réponses correctes :** A (Type 8 - Echo Request), B (Type 0 - Echo Reply)

**Explication :**
La commande ping utilise deux types de messages ICMP :
- **Type 8** : Echo Request (envoyé par la source)
- **Type 0** : Echo Reply (réponse de la destination)

Le client envoie une requête (Type 8), la destination répond (Type 0) si elle est joignable. Le temps de réponse (RTT) est mesuré pour évaluer la latence.

---

### Question 9
**Réponse correcte :** A (Type 1 Code 0 - No route to destination)

**Explication :**
En **ICMPv6 Type 1 Code 0** signifie **No route to destination** et regroupe les erreurs "Network Unreachable" et "Host Unreachable" de ICMPv4. Cette simplification fait partie des améliorations d'ICMPv6. C'est l'un des 5 codes essentiels du Type 1 ICMPv6 à maîtriser.

---

### Question 10
**Réponse correcte :** B (IPv4 utilise Type 3 Code 4, IPv6 utilise Type 2)

**Explication :**
Différence importante :
- **IPv4** : ICMPv4 Type 3 Code 4 (Fragmentation Needed but DF set)
- **IPv6** : ICMPv6 Type 2 (Packet Too Big) - message dédié

En IPv6, les routeurs **ne peuvent jamais fragmenter** les paquets en transit (seule la source peut fragmenter), donc le PMTUD est **obligatoire**.

---

### Question 11
**Réponse correcte :** C (Type 3 Code 0 - Hop Limit Exceeded)

**Explication :**
Traceroute IPv6 utilise **ICMPv6 Type 3 Code 0 (Hop Limit Exceeded in Transit)**. Le Hop Limit en IPv6 est l'équivalent du TTL en IPv4. Quand il atteint 0, le routeur rejette le paquet et envoie ce message, permettant à traceroute de découvrir le chemin. La destination répond avec Type 1 Code 4 (Port Unreachable).

---

### Question 12
**Réponses correctes :** A (Type 133 - RS), B (Type 134 - RA), C (Type 135 - NS), D (Type 136 - NA), E (Type 137 - Redirect)

**Explication :**
Les **5 types de messages NDP** (Neighbor Discovery Protocol) :
- **Type 133 (RS)** : Router Solicitation - demande aux routeurs de s'annoncer
- **Type 134 (RA)** : Router Advertisement - annonce du routeur avec préfixe
- **Type 135 (NS)** : Neighbor Solicitation - résolution d'adresse, DAD
- **Type 136 (NA)** : Neighbor Advertisement - réponse au NS
- **Type 137** : Redirect - informer d'un meilleur chemin

Type 138 n'est pas un message NDP standard.

---

### Question 13
**Réponse correcte :** B (FF02::2 - tous les routeurs)

**Explication :**
Un hôte envoie un **Router Solicitation (RS)** à l'adresse multicast **FF02::2 (all routers)** pour demander aux routeurs du lien local de s'annoncer immédiatement. Les routeurs répondent avec un Router Advertisement (RA) contenant le préfixe IPv6 et d'autres informations de configuration.

---

### Question 14
**Réponses correctes :** A (Préfixe IPv6), B (Flags M et O), C (Link-Local du routeur)

**Explication :**
Le **Router Advertisement (RA)** fournit des informations essentielles :
- **Préfixe IPv6** du réseau (ex: 2001:db8:acad:1::/64)
- **Flags M et O** : déterminent la méthode d'allocation (SLAAC, DHCPv6)
- **Adresse Link-Local du routeur** : utilisée comme passerelle par défaut
- Durée de vie du préfixe, MTU du lien

L'adresse MAC n'est pas fournie dans le RA.

---

### Question 15
**Réponses correctes :** A (Résolution d'adresse), B (DAD), C (NUD)

**Explication :**
Le **Neighbor Solicitation (NS)** a 3 utilisations principales :
- **Résolution d'adresse** : trouver la MAC d'une adresse IPv6 (équivalent ARP)
- **DAD (Duplicate Address Detection)** : vérifier qu'une adresse n'est pas déjà utilisée
- **NUD (Neighbor Unreachability Detection)** : vérifier qu'un voisin est toujours joignable

C'est un message ICMPv6 Type 135 extrêmement important pour le fonctionnement d'IPv6.

---

### Question 16
**Réponse correcte :** C (Adresse solicited-node FF02::1:FF...)

**Explication :**
Pour la résolution d'adresse et DAD, le **Neighbor Solicitation** est envoyé à l'adresse **solicited-node multicast** (FF02::1:FF + 24 derniers bits de l'unicast). Cela permet de cibler uniquement les hôtes concernés, contrairement au broadcast IPv4 qui touche tous les hôtes du segment. C'est plus efficace et réduit la charge réseau.

---

### Question 17
**Réponses correctes :** A (SLAAC Only), B (SLAAC + DHCPv6 Stateless), C (DHCPv6 Stateful)

**Explication :**
Les **3 méthodes d'allocation IPv6** :
- **SLAAC Only** (M=0, O=0) : auto-configuration complète, pas de serveur
- **SLAAC + DHCPv6 Stateless** (M=0, O=1) : SLAAC pour l'adresse + DHCPv6 pour DNS
- **DHCPv6 Stateful** (M=1) : serveur gère tout (adresses et configuration)

APIPA n'existe pas en IPv6 (les Link-Local remplacent ce besoin).

---

### Question 18
**Réponse correcte :** C (Non, il faut configurer manuellement ou utiliser O=1)

**Explication :**
Avec **SLAAC Only (M=0, O=0)**, l'hôte peut générer automatiquement son adresse IPv6, mais **ne peut PAS obtenir automatiquement les serveurs DNS**. C'est une limitation de SLAAC seul. Solutions :
- Configuration manuelle des DNS
- Utiliser **SLAAC + DHCPv6 Stateless (O=1)** pour obtenir DNS automatiquement (méthode recommandée)

---

### Question 19
**Réponse correcte :** B (SLAAC + DHCPv6 Stateless M=0, O=1)

**Explication :**
La méthode **SLAAC + DHCPv6 Stateless (M=0, O=1)** est recommandée pour la plupart des déploiements car elle combine :
- ✅ Simplicité de SLAAC (auto-configuration des adresses)
- ✅ Configuration automatique DNS via DHCPv6
- ✅ Pas d'état à maintenir côté serveur pour les adresses
- ✅ Flexibilité et évolutivité

C'est le meilleur compromis entre simplicité et fonctionnalité.

---

### Question 20
**Réponse correcte :** B (Neighbor Solicitation - DAD)

**Explication :**
Le **DAD (Duplicate Address Detection)** utilise un **Neighbor Solicitation (NS)** :
1. L'hôte génère une adresse via SLAAC
2. Il envoie un NS à l'adresse solicited-node correspondante
3. Message : "Quelqu'un utilise-t-il cette adresse ?"
4. Si aucune réponse (NA) → adresse valide
5. Si réponse → conflit détecté, générer une nouvelle adresse

C'est une étape cruciale du processus SLAAC pour garantir l'unicité des adresses.
