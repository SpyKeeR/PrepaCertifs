# Module 03 : Modèles et protocoles
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module présente les modèles de référence réseau (OSI et TCP/IP), les protocoles et l'encapsulation des données.

**Durée estimée :** 5-6 heures  
**Objectifs :** Comprendre les modèles en couches, les protocoles et l'encapsulation

---

## 3.1 Les règles

### Communication réseau
Toute communication nécessite des règles (protocoles) définissant :
- **Format du message** : Structure et organisation
- **Taille du message** : Segmentation si nécessaire
- **Timing** : Contrôle du flux, délais d'attente
- **Encodage** : Conversion en signaux (bits)
- **Encapsulation** : Format du paquet
- **Métohde de livraison** : Unicast, multicast, broadcast

### Analogie : Communication humaine
- **Langue commune** : Protocole partagé
- **Ton et volume** : Présentation du message
- **Tour de parole** : Gestion du timing

---

## 3.2 Protocoles

### Définition
Un **protocole** est un ensemble de règles qui régissent la communication réseau.

### Fonction des protocoles

**1. Adressage**
- Identification de l'émetteur et du destinataire
- Adresses IP, adresses MAC

**2. Fiabilité**
- Garantie de livraison
- Accusés de réception (ACK)
- Retransmission si perte

**3. Contrôle de flux**
- Régulation de la vitesse de transmission
- Évite la surcharge du récepteur

**4. Séquencement**
- Ordre de reconstruction des données
- Numéros de séquence

**5. Détection d'erreurs**
- Vérification de l'intégrité des données
- Checksum, CRC

**6. Interface applicative**
- Communication entre applications et réseau

---

## 3.3 Suites de protocoles

### Suite de protocoles TCP/IP
Ensemble de protocoles utilisés sur Internet.

**Protocoles majeurs :**
- **TCP** (Transmission Control Protocol) : Fiable, orienté connexion
- **IP** (Internet Protocol) : Acheminement des paquets
- **HTTP/HTTPS** : Navigation web
- **FTP** : Transfert de fichiers
- **SMTP** : Envoi d'email
- **DNS** : Résolution de noms
- **DHCP** : Attribution automatique d'adresses IP

### Protocoles ouverts vs propriétaires

**Protocoles ouverts** :
- Standards publics
- Interopérabilité entre fabricants
- Exemples : TCP/IP, HTTP, SMTP
- Gérés par des organismes (IETF, IEEE)

**Protocoles propriétaires** :
- Développés par une entreprise
- Contrôle exclusif
- Exemples : Cisco EIGRP (bien que ouvert depuis), AppleTalk

---

## 3.4 Organismes de normalisation

### Organismes internationaux

**1. IETF (Internet Engineering Task Force)**
- Développe et maintient les standards Internet
- Documents : RFC (Request For Comments)
- Exemples : TCP/IP, HTTP, FTP

**2. IEEE (Institute of Electrical and Electronics Engineers)**
- Standards réseaux locaux
- Exemples :
  - **802.3** : Ethernet
  - **802.11** : Wi-Fi
  - **802.1Q** : VLANs

**3. ISO (International Organization for Standardization)**
- Modèle OSI (Open Systems Interconnection)
- Standards internationaux

**4. ITU (International Telecommunication Union)**
- Standards télécommunications
- Exemples : vidéo compression, DSL

**5. ICANN (Internet Corporation for Assigned Names and Numbers)**
- Gestion des noms de domaine et adresses IP
- Coordination de l'espace d'adressage

**6. IANA (Internet Assigned Numbers Authority)**
- Allocation des adresses IP, numéros de port
- Gérée par ICANN

---

## 3.5 Modèles de référence

### Pourquoi des modèles en couches ?

**Avantages** :
- **Modularité** : Chaque couche a un rôle spécifique
- **Interopérabilité** : Standards communs
- **Facilité de conception** : Développement par couche
- **Evolut

ivité** : Modifications sans affecter les autres couches
- **Dépannage** : Isolation des problèmes par couche

### Modèle OSI (Open Systems Interconnection)

**7 couches** (de haut en bas) :

| Couche | Nom | Rôle | PDU | Exemples |
|--------|-----|------|-----|----------|
| **7** | **Application** | Interface utilisateur | Données | HTTP, FTP, SMTP, DNS |
| **6** | **Présentation** | Format, chiffrement | Données | SSL/TLS, JPEG, ASCII |
| **5** | **Session** | Gestion des sessions | Données | NetBIOS, RPC |
| **4** | **Transport** | Livraison end-to-end | Segment | TCP, UDP |
| **3** | **Réseau** | Routage, adressage logique | Paquet | IP, ICMP, OSPF |
| **2** | **Liaison de données** | Accès média, adressage physique | Trame | Ethernet, PPP, HDLC, 802.11 |
| **1** | **Physique** | Transmission bits | Bits | Câbles, Wi-Fi, hubs |

**Mnémotechnique (bas vers haut) :**
- "Please Do Not Throw Sausage Pizza Away" (en anglais)
- "Pour Des Nuits TranquillesServez Pas d'Alcool" (en français)

**Mnémotechnique (haut vers bas) :**
- "All People Seem To Need Data Processing" (en anglais)

#### Couche 7 - Application
- Interface entre l'utilisateur et le réseau
- Protocoles : HTTP, FTP, SMTP, DNS, Telnet, SSH

#### Couche 6 - Présentation
- Format des données, encodage
- Compression, chiffrement
- Traduction entre formats

#### Couche 5 - Session
- Établissement, gestion et terminaison des sessions
- Synchronisation
- Moins utilisée aujourd'hui

#### Couche 4 - Transport
- Segmentation et réassemblage
- Fiabilité (TCP) ou rapidité (UDP)
- Numéros de port
- Contrôle de flux

#### Couche 3 - Réseau
- Routage des paquets
- Adressage logique (IP)
- Choix du meilleur chemin
- Protocoles : IP, ICMP, OSPF, EIGRP

#### Couche 2 - Liaison de données
- Accès au média physique
- Adressage physique (MAC)
- Détection d'erreurs (CRC)
- Protocoles : Ethernet, PPP, Framerelay

#### Couche 1 - Physique
- Transmission des bits
- Spécifications électriques, mécaniques
- Médias : câbles, connecteurs, signaux

### Modèle TCP/IP

**4 couches** (modèle pratique utilisé sur Internet) :

| Couche | Nom | Correspond à OSI | Protocoles |
|--------|-----|------------------|------------|
| **4** | **Application** | Couches 5, 6, 7 | HTTP, FTP, SMTP, DNS, Telnet, SSH |
| **3** | **Transport** | Couche 4 | TCP, UDP |
| **2** | **Internet** | Couche 3 | IP, ICMP, ARP, OSPF |
| **1** | **Accès réseau** | Couches 1, 2 | Ethernet, Wi-Fi, PPP |

**Comparaison OSI vs TCP/IP :**
- **OSI** : Modèle théorique, 7 couches
- **TCP/IP** : Modèle pratique, 4 couches
- **TCP/IP** regroupe les couches hautes (5-6-7) et basses (1-2)

---

## 3.6 Encapsulation de données

### Processus d'encapsulation

Lorsqu'un message est envoyé, il traverse les couches du modèle. Chaque couche ajoute ses propres informations (en-têtes).

**Étapes (de haut en bas) :**

1. **Couche Application** :
   - Données utilisateur
   - PDU : **Données**

2. **Couche Transport** :
   - Ajout d'en-tête transport (port source/destination)
   - PDU : **Segment** (TCP) ou **Datagramme** (UDP)

3. **Couche Internet/Réseau** :
   - Ajout d'en-tête IP (adresses IP source/destination)
   - PDU : **Paquet**

4. **Couche Accès réseau/Liaison** :
   - Ajout d'en-tête et de trailer (adresses MAC, FCS)
   - PDU : **Trame**

5. **Couche Physique** :
   - Conversion en bits
   - PDU : **Bits**

**Schéma :**
```
Données
    ↓ (Encapsulation)
Segment/Datagramme (En-tête Transport + Données)
    ↓
Paquet (En-tête IP + Segment)
    ↓
Trame (En-tête Ethernet + Paquet + Trailer)
    ↓
Bits (Signal physique)
```

### PDU (Protocol Data Unit)

**Nom de l'unité de données à chaque couche :**
- **Données** : Couche Application
- **Segment** : Couche Transport (TCP)
- **Datagramme** : Couche Transport (UDP)
- **Paquet** : Couche Réseau
- **Trame** : Couche Liaison de données
- **Bits** : Couche Physique

### Désencapsulation

Processus inverse à la réception :
1. **Bits** → **Trame** (Couche Physique)
2. **Trame** → **Paquet** (Couche Liaison - vérifie adresse MAC)
3. **Paquet** → **Segment** (Couche Réseau - vérifie adresse IP)
4. **Segment** → **Données** (Couche Transport - vérifie port)
5. **Données** livrées à l'application

À chaque étape, la couche retire son en-tête et passe aux couches supérieures.

---

## 3.7 Accès aux données

### Adresses réseau

Deux types d'adresses sont nécessaires pour la communication :

**1. Adresse de couche réseau (Logique)**
- **Adresse IP**
- Identifie l'hôte et le réseau
- Peut changer (DHCP, mobilité)
- Utilisée pour le routage entre réseaux

**2. Adresse de couche liaison de données (Physique)**
- **Adresse MAC**
- Identifie la carte réseau (NIC)
- Gravée en usine (permanente)
- Utilisée pour la communication locale (même réseau)

### Communication même réseau

**Exemple :** PC1 (192.168.1.10) envoie à PC2 (192.168.1.20) sur le même LAN.

**Étapes :**
1. PC1 encapsule les données avec :
   - IP source : 192.168.1.10
   - IP destination : 192.168.1.20
2. PC1 doit trouver l'adresse MAC de PC2 :
   - Utilise **ARP** (Address Resolution Protocol)
   - "Qui a l'IP 192.168.1.20 ?"
3. PC2 répond avec son adresse MAC
4. PC1 encapsule le paquet dans une trame avec :
   - MAC source : MAC de PC1
   - MAC destination : MAC de PC2
5. Le switch transmet la trame à PC2
6. PC2 désencapsule et traite les données

### Communication réseau distant

**Exemple :** PC1 (192.168.1.10) envoie à Serveur Web (8.8.8.8) sur Internet.

**Étapes :**
1. PC1 détermine que la destination est sur un réseau distant
2. PC1 encapsule avec :
   - IP source : 192.168.1.10
   - IP destination : 8.8.8.8
3. PC1 envoie à sa **passerelle par défaut** (routeur)
   - Utilise ARP pour l'adresse MAC du routeur
   - MAC destination : MAC du routeur
4. Le routeur reçoit la trame :
   - Désencapsule (retire en-tête Ethernet)
   - Examine l'IP destination
   - Consulte sa table de routage
   - Détermine l'interface de sortie
5. Le routeur réencapsule dans une nouvelle trame :
   - MAC source : MAC de l'interface sortante du routeur
   - MAC destination : MAC du prochain saut (next-hop)
6. Le processus se répète à chaque routeur jusqu'à destination

**⚠️ Point clé :**
- L'adresse IP **ne change pas** de bout en bout
- L'adresse MAC **change à chaque saut** (seulement locale)

---

## 💡 Points clés à retenir

1. **Protocoles** : Règles de communication réseau
2. **Modèle OSI** : 7 couches (Application, Présentation, Session, Transport, Réseau, Liaison, Physique)
3. **Modèle TCP/IP** : 4 couches (Application, Transport, Internet, Accès réseau)
4. **Encapsulation** : Ajout d'en-têtes à chaque couche
5. **PDU** : Données → Segment → Paquet → Trame → Bits
6. **Adresses** : IP (routage inter-réseaux), MAC (livraison locale)
7. **Communication locale** : Adresse MAC destination = MAC de l'hôte
8. **Communication distante** : Adresse MAC destination = MAC de la passerelle par défaut

---

## 🔗 Commandes

Aucune commande IOS spécifique pour ce module (concepts théoriques).

---

## 📝 Exercices pratiques

1. **Identifier les couches OSI** pour différents protocoles :
   - HTTP : Couche 7
   - TCP : Couche 4
   - IP : Couche 3
   - Ethernet : Couche 2

2. **Schématiser l'encapsulation** d'un email envoyé depuis un PC

3. **Expliquer** pourquoi l'adresse MAC change à chaque saut mais pas l'adresse IP

4. **Packet Tracer** :
   - Mode simulation
   - Observer l'encapsulation/désencapsulation lors d'un ping

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
