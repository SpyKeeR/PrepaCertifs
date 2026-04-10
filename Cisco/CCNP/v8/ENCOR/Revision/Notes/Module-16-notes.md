# Module 16 : Tunnels Overlay
## Notes Complètes de Révision

---

## 1. TUNNELS GRE (Generic Routing Encapsulation)

### Objectifs et Cas d'Usage

GRE est un protocole de tunneling qui encapsule n'importe quel protocole de couche réseau (IPv4, IPv6, AppleTalk, IPX) dans des paquets IP pour transmission à travers une infrastructure IP existante. Contrairement à IPsec qui ajoute du chiffrement, GRE ne chiffre rien – il encapsule simplement.

**Cas d'usage courants:**
- Connecter deux réseaux privés discontiguous à travers Internet ou un réseau tiers
- Tunnel à travers firewall ou ACL restrictive (GRE peut se glisser là où d'autres protocoles échouent)
- Créer des liaisons VPN simples lorsque le chiffrement n'est pas critique
- Transporter du trafic multicast (GPE et IPsec n'en supportent pas)
- Création de topologies virtual mesh pour le routage dynamique

### Processus d'encapsulation et décapsulation GRE

Un paquet original (IPv4, IPv6, ou autre) entre dans une interface tunnel. Le routeur d'encapsulation :

1. **Sauvegarder le paquet original** (paquet interne)
2. **Ajouter l'en-tête GRE** (4 octets minimum, jusqu'à 24 avec options)
3. **Ajouter un nouvel en-tête IP** avec source = adresse source tunnel et destination = adresse destination tunnel
4. **Transmettre** le paquet encapsulé résultant sur le chemin normal de routage

Au point de décapsulation, le routeur distant :

1. **Reçoit** le paquet tunnel IP
2. **Reconnait** le protocole GRE (IP protocol 47)
3. **Extrait l'en-tête GRE** et le paquet interne
4. **Traite** le paquet interne selon son type (IPv4, IPv6, etc.)
5. **Route** le paquet décapsulé normalement

### Supp IPv4 et IPv6 dans les tunnels GRE

GRE est Protocol-Agnostic – le protocole interne (overlay) et externe (underlay) peuvent être n'importe quelle combinaison :

| Underlay (Transport) | Overlay (Payload) | Cas d'usage |
|---------------------|------------------|-----------|
| IPv4 | IPv4 | Classique: IPv4 sur IPv4 |
| IPv4 | IPv6 | Transition IPv6: transport IPv4 existant |
| IPv6 | IPv4 | Infrastructure IPv6 native, clients IPv4 |
| IPv6 | IPv6 | IPv6 sur infrastructure IPv6 |
| IPv4 | Autre (AppleTalk, IPX) | Héritage |

Cette flexibilité rend GRE précieux lors de transitions vers IPv6 – l'infrastructure IPv6 peut être déployée graduellement.

### Configuration GRE étape par étape

**Étape 1 : Créer l'interface tunnel**

```
Router(config)# interface tunnel 0
```

Cela crée une interface de tunnel numérotée 0. Vous pouvez avoir plusieurs tunnels sur un routeur (tunnel 0, 1, 2, etc.).

**Étape 2 : Configurer la source du tunnel**

```
Router(config-if)# tunnel source 10.1.1.1
```

ou

```
Router(config-if)# tunnel source GigabitEthernet0/0/0
```

Soit une adresse IP statique, soit une interface. Si une interface est spécifiée, l'adresse IP primaire de cette interface devient la source tunnel.

**Étape 3 : Configurer la destination du tunnel**

```
Router(config-if)# tunnel destination 10.2.2.2
```

Adresse IP de l'autre extrémité du tunnel où l'authentification se fait.

**Étape 4 : Attribuer une adresse IP à l'interface tunnel**

```
Router(config-if)# ip address 192.168.100.1 255.255.255.0
```

L'interface tunnel elle-même reçoit une adresse IP. Cette adresse est généralement dans un sous-réseau distinkt qui connecte les deux extrémités du tunnel. Les deux côtés doivent être sur le même sous-réseau logique tunnel.

**Étape 5 (Optionnelle) : Configurer ou modifier la bande passante pour les métriques de routage**

```
Router(config-if)# bandwidth 1000
```

La bande passante est en kbps. Les protocoles de routage (OSPF, EIGRP) utilisent cela pour calculer les métriques. Sans configuration, GRE hérite de la bande passante de l'interface physique de sortie. Configurer à basse bande passante rend les routes tunnel moins préférées.

**Étape 6 (Optionnelle) : Configurer les keepalives**

```
Router(config-if)# keepalive 10 3
```

Par défaut: 10 secondes, 3 retries. Si 3 keepalives consécutifs échouent, l'interface tunnel passe à down. C'est plus rapide que d'attendre 180 secondes pour un timeout de protocole de routage.

**Étape 7 (Optionnelle) : Configurer le MTU du tunnel**

```
Router(config-if)# ip mtu 1400
```

Par défaut, l'interface tunnel hérite du MTU de l'interface physique (typiquement 1500 octets). Comme GRE ajoute 24 octets d'en-tête (dans le pior cas avec IP + GRE), des paquets de 1500 octets fragmentés en tunnel pourraient devenir 1524 octets – trop grands pour le lien physique. Configurer MTU tunnel à 1400 ou moins joue par sécurité.

### Configuration GRE Exemple complet

```
Router-A(config)# interface tunnel 0
Router-A(config-if)# tunnel source 203.0.113.10
Router-A(config-if)# tunnel destination 203.0.113.20
Router-A(config-if)# ip address 192.168.100.1 255.255.255.0
Router-A(config-if)# bandwidth 512
Router-A(config-if)# keepalive 10 3
Router-A(config-if)# ip mtu 1400
Router-A(config-if)# exit

Router-B(config)# interface tunnel 0
Router-B(config-if)# tunnel source 203.0.113.20
Router-B(config-if)# tunnel destination 203.0.113.10
Router-B(config-if)# ip address 192.168.100.2 255.255.255.0
Router-B(config-if)# bandwidth 512
Router-B(config-if)# exit
```

### Vérification des tunnels GRE

**Avant de vérifier, deux choses doivent être vraies:**
1. La source et la destination tunnel doivent être routables (ping doit fonctionner)
2. Les deux extrémités doivent avoir une configuration compatible

```
Router# show interface tunnel 0
```

Affiche l'état de l'interface :
- Statut physique (up/down)
- MTU configuré
- Statistiques de paquet (entrée/sortie)
- Erreurs potentielles

```
Router# show ip route
```

Vérifier que les tunnels et les routes qui les utilisent sont présentes. Les routes apprises ou statiquement configurées utilisant la destination tunnel doivent être visibles avec l'interface tunnel comme sortie.

**Tracer et vérifier la connectivité à travers le tunnel:**

```
Router# ping 192.168.100.2
```

Si le tunnel fonctionne (et la configuration de l'autre côté est correcte), le ping de l'adresse tunnel IP de l'autre côté doit réussir.

```
Router# traceroute 192.168.1.0
```

Traceroute à travers le tunnel montrera d'abord les hops vers la destination tunnel (à travers Internet public ou WAN), puis le tunnel comme un « hop » logique unique, puis finalement le réseau cible au-delà du tunnel distant.

### Problèmes courants avec les réseaux overlay

**Routage récursif**

C'est le problème classique et déroutant avec les tunnels. Exemple :

- Tunnel source = 10.1.1.1
- Tunnel destination = 10.2.2.2 (dans le sous-réseau 10.2.2.0/24)
- Routeur envoie le trafic du tunnel à travers le tunnel lui-même pour atteindre la destination tunnel

Cela crée une boucle infinie de paquet tunnelisés.

**Mitigation**: Assurez-vous que la route vers la destination tunnel utilise une interface différente que l'interface tunnel elle-même. Typiquement, il faut une route statique pour la destination tunnel via l'interface WAN réelle :

```
Router(config)# ip route 10.2.2.0 255.255.255.0 <next-hop-via-physical-interface>
```

**Sélection d'interface de sortie incorrecte**

Si le routeur a plusieurs chemins vers la destination tunnel, il doit sélectionner correctement lequel utiliser pour les paquets du tunnel.

**Problèmes d'encapsulation BTW:**

Parfois les deux extrémités ne s'entendent pas sur le protocole ou les paramètres du tunnel. Les symptômes incluent :
- "Interface protocol down" bien que physiquement up
- Paquets tunnelisés qui n'arrivent jamais
- Asymétrie (tunnel fonctionne dans un sens seulement)

**Vérification:** `show ip route summary`, `debug tunnel` pour identifier les probèmes.

---

## 2. FONDAMENTAUX IPSEC

### IPsec comme cadre de sécurité standard ouvert

IPsec est un ensemble de protocoles et standards pour sécuriser les communications IP. Ce n'est pas un produit propriétaire – c'est une suite d'RFC (2401, 2402, 2406, 3686, etc.) implémentée par Cisco, Juniper, Fortinet, pfSense, OpenBSD, Linux et pratiquement tous les fournisseurs de réseau.

### Services de sécurité IPsec : 4 piliers

**1. Authentification des pairs**

Avant de créer un tunnel IPsec, les deux extrémités doivent prouver leur identité. Deux méthodes principales:

- **RSA Signatures** : Utiliser des certificats X.509 et la cryptographie à clé publique pour prouver l'identité
- **Pre-Shared Key (PSK)** : Partager une clé secrète configurable localement (plus simple, moins sécurisé à grande échelle)

Sans authentification mutuelle, un acteur malveillant sur le chemin réseau peut se faire passer pour un endpoint le gitime.

**2. Confidentialité des données (chiffrement)**

Le trafic doit être incompréhensible pour quiconque l'intercepte. IPsec utilise la cryptographie symétrique pour le chiffrement en masse des données. Les algorithmes courants:

- **DES (56-bit)** : **OBSOLÈTE** et **NON RECOMMANDÉ** – trop faible pour les menaces modernes
- **3DES (168-bit effectif)**: Triple DES, meilleur que DES seul mais pas recommandé pour les nouveaux déploiements
- **AES (128/192/256-bit)** : **RECOMMANDÉ** et **Standard FIPS 197**. Le standard, moderne, sécurisé pour la plupart des cas

**3. Intégrité des données**

Même si encrypted, le trafic doit être certifié comme non-modifié en transit. Ceci utilise des fonctions de hachage (Message Authentication Code + HMAC):

- **MD5 (128-bit)** : **ÉVITER** – collisions cryptographiques connues depuis des années
- **SHA-1 (160-bit)** : Plus sécurisé que MD5, mais considéré comme faible maintenant
- **SHA-256/384/512** : Recommandé pour la cohérence avec AES puissant

**4. Détection de rejeu**

Si un attaquant capture un paquet IPsec, peut-il le renvoyer ultérieurement pour étrange le pare-feu ou nuire au service ? IPsec utilise des numéros de séquence croissants pour rejeter les paquets dupliqués ou hors séquence.

### En-tête d'authentification (AH) vs Encapsulating Security Payload (ESP)

**Authentication Header (AH):**

- **Fonction**: Authentifiaction + intégrité (pas de confidentialité)
- **Couverture**: En-tête IP extérieur (partiellement) + toutes les données
- **Raison uncommon**: Ajoute un en-tête supplémentaire sans chiffrement; putas pas cher que ESP et c'est donc rarement utilisé isolé
- **Historique**: Original dans IPsec RFC 2402, maintenant souvent couplé avec ESP

**Encapsulating Security Payload (ESP):**

- **Fonction**: Confidentialité (chiffrement) + intégrité (hachage HMAC)
- **Couverture**: Paquet original complet, puis hachage périphérique calculé
- **Standard**: RFC 2406 (après 3686 pour les IV explicites)
- **Utilisation**: Le cœur de la plupart des VPN IPsec modernes

**Combinaisons valides:**
- AH seul : Intégrité seulement
- ESP seul : Chiffrement + intégrité
- AH + ESP : Double protection (rarement utilisé car ESP seul suffira couvrir tous les chiffrement + intégrité)

### Modes d'opération IPsec : Tunnel vs Transport

**Mode Transport:**

```
Original IP Header | Original Data
        ↓
[Modify Original Header] | ESP Encrypted Original Data | ESP Auth
```

- L'en-tête IP original reste visible (mais Payload chiffré)
- Seul le payload est chiffré et authentifié
- Les réseaux intermédiaires voient source/destination originales
- **Non utilisé** pour les VPN site-to-site (le mode tunnel est standard)
- Utilisation: Host-to-host VPN (client SSH IPsec, application IPsec)

**Mode Tunnel:**

```
Original Source/Dest IP Header | Original Data
        ↓
New IP Header (tunnel) | ESP Encrypted (Original IP + Data) | ESP Auth
```

- L'en-tête IP original est complètement encapsulé (chiffré)
- Un nouvel en-tête IP pour tunnel source/dest est ajouté
- **Standard pour VPN site-to-site**, les passerelles ne voient que le tunnel, pas le trafic interne
- De meilleure sécurité car les politiques d'IP interne ne sont pas visibles au-delà du tunnel

---

## 3. CRYPTOGRAPHIE IPSEC

### Algorithmes de chiffrement

**DES (Data Encryption Standard):**
- Clé: 56 bits
- **NE PAS UTILISER** – trop court pour brute force modern
- Historique uniquement

**3DES (Triple DES):**
- Clé: 3× 56-bit = 168-bit long logement
- Applique DES trois fois avec trois clés différentes
- "Keying option 1": les 3 clés sont indépendantes
- Meilleur que DES, mais :
  - Lent (3× la complexité du DES)
  - Pas recommandé pour les nouveaux déploiements
  - Phase out progressif

**AES (Advanced Encryption Standard, Rijndael):**
- Clés: 128-bit, 192-bit, ou 256-bit
- Dernier standard FIPS 197
- **STANDARD RECOMMANDÉ** pour tous les nouveaux déploiements IPsec
- Extrêmement rapide en hardware moderne
- Sécurisé contre les menaces actuelles et anticipées

### Algorithmes de hachage pour HMAC

**MD5:**
- Sortie: 128-bit
- **OBSOLÈTE** – collisions connues, éviter pour la sécurité
- Peut rester dans les configs historiques

**SHA-1:**
- Sortie: 160-bit
- Plus robuste que MD5, mais pas idéal
- Phase-out progressif de beaucoup d'organisations
- NIST recommander de passer à SHA-256/512 pour la cryptographie

**SHA-256 (SHA-2):**
- Sortie: 256-bit
- **RECOMMANDÉ** – sécurité moderne, fonctionne avec AES
- Bonne future-proofing

### Échange de clés : Diffie-Hellman vs RSA vs Pre-Shared Key

**Diffie-Hellman (DH):**

Protocole asymétrique permettant deux parties générant une clé secrète partagée sur un canal non sécurisé. Étapes simplifiées:

1. Alice et Bob publientliquement : g (générateur) et p (grand nombre premier)
2. Alice génère a privé, calcule A = g^a mod p, envoie A
3. Bob génère b privé, calcule B = g^b mod p, envoie B
4. Alice calcule secrète partagée = B^a mod p
5. Bob calcule la même partagée = A^b mod p
6. Mathématiquement, B^a = A^b, donnant la clé partagée

Un tiers qui voit A et B ne peut pas facilement calculer la clé partagée (problème DH discrete log). Utilisé dans IKE Phase 1 pour établir la clé session.

**Variantes DH:**
- DH Group 1 (768-bit) : Faible maintenant
- DH Group 2 (1024-bit) : Plus sûr
- DH Group 14-19 : 2048-bit+, recommandé modern

**RSA Signatures:**

- Suite de certificats X.509 incluant la clé publique
- Chaque partie signe les données avec sa clé privée
- L'autre partie vérifie la signature avec la clé publique reçue
- Prouve l'identité et non-répudiation (quiconque envoyé les données)
- Plus lent que PSK, mais plus secure car chaque endpoint a une identité unique

**Pre-Shared Key (PSK):**

- Chaîne de secrets configurable localement
- Simple, pas de gestion de certificats
- **Limitations**: Les deux points de terminaison doivent connaissance la clé secrète; un seul PSK partagé entre 10 VPN signifie un compromission = tous les 10 VPN compromis
- Utilisé généralement dans des petits déploiements

---

## 4. TRANSFORM SETS ET NÉGOCIATION SA

### Concept de Transform Set

Une `transform set` est une combinaison d'algorithmes de sécurité acceptables pour un VPN donné. Rather que d'autoriser ANY combo (dont celles faibles), un administrateur définit précisément les protos + algos acceptables.

**Exemple transform set:**

```
Router(config)# crypto ipsec transform-set TS-AES-SHA255-TUNNEL 
 esp-aes 256 esp-sha256-hmac
 mode tunnel
```

Cela dit:
- Utiliser ESP (pas AH seul)
- Algosym chiffrement: AES avec clé 256-bit
- Algo d'authentification: SHA-256 HMAC
- Mode: Tunnel (pas host transport)

Les pairs durant la négociation échangent listes de transform sets acceptables. Si une correspondance existe, l'SA utilise cet ensemble.

### Internet Key Exchange (IKE)

IKE est le protocole de négociation pour establir les associations de sécurité IPsec. Deux versions:

**IKEv1:**
- RFC originale 2409
- Complexe, moins efficace
- Deux phases:
  - **Phase 1**: Les deux extrémités s'authentifient mutuellement (RSA, PSK, etc meth), établir une clé session
  - **Phase 2**: Négocier les transform sets pour l'IPsec
- Toujours supporté

**IKEv2:**
- RFC 7296 (2010)
- Simplifié, plus efficace, fusionné les phases
- Meilleur support de mobilité client (MOBIKE)
- Recommandé pour les nouveaux déploiements

### Asociation de Sécurité (SA) IPsec

Chaque tunnel IPsec est formé par une ou deux SAs (unidirectionnel par). Une SA stocke:
- Transform set négocié
- Clés de chiffrement dérivées
- Numéro de séquence
- Dates d'expiration SA
- Adresses tunnel endpoints

Les deux peers créent des SAs bidirectionnels – trafic sortant utilise une, entrant usesé l'autre.

---

## 5. LISP & VXLAN : TECHNOLOGIES OVERLAY AUTRES

### LISP (Locator/ID Separation Protocol)

LISP est un protocole overlay qui sépare l'identifiant d'un hôte de son locateur réseau actuel. Un appareil garde le même "ID" (adresse immuable) tandis que son "Locateur" (IP de routage actuelle) change lors des changements de réseau.

- **Cas d'usage**: Mobilité site-to-site, DC migration, réduction annnonces de routage
- **Différence de GRE/IPsec**: Plus avancé, nécessite infrastructure LISP (Map-Servers, ETRs, ITRs)
- Pas aussi adopté que GRE/IPsec

### VXLAN (Virtual Extensible LAN)

VXLAN encapsule les trames Ethernet L2 en paquets UDP L4 pour transmission à travers une infrastructure IP.

- **Cas d'usage**: Datacenter overlay, extension VLAN sur L3, cloud multi-tenant
- **Avantage**: Transparent à L3, utilise UDP port 4789
- **Différence de GRE**: VXLAN spécifiquement pour L2 overlay, GRE est agnostique sur le protocole
- Supporté par Cisco Catalyst, Nexus, beaucoup de switches physiques/virtuels

---

## Résumé et Points clés

1. **GRE**: Protocol tunneling simple, sans chiffrement. IPv4/IPv6 flexible overlay/underlay.

2. **IPsec Cadre**: Authentification + Confidentialité + Intégrité + Rejeu en 4 services.

3. **AH vs ESP**: AH = intégrité seulement (rarement seul). ESP = chiffrement + intégrité (standard).

4. **Modes**: Tunnel = VPN site-to-site standard. Transport = host encrypt.

5. **Crypto Algos**: AES-256 recommandé pour chiffrement. SHA-256 pour hachage. DES/3DES/MD5 obsolète.

6. **Transform Sets**: Combos d'algorithmes approuvées pour un VPN. Négociées via IKE.

7. **IKE**: Protocole key exchange. IKEv1 (2 phases) et IKEv2 (fusionné, meilleur).

---

*Dernière révision : 18 mars 2026*
*Révision CCNP ENCOR Module 16*
