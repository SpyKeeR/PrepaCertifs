# Module 06 : Couche de liaison de données
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module couvre la couche 2 du modèle OSI : rôle, services, topologies et structure des trames.

**Durée estimée :** 4-5 heures  
**Objectifs :** Comprendre la couche liaison de données et son rôle dans la transmission

---

## 6.1 Rôle de la couche liaison de données

### Couche 2 du modèle OSI

**Responsabilités principales :**
1. **Accès au média** : Contrôle qui peut émettre sur le média
2. **Encadrement (Framing)** : Encapsulation des paquets réseau en trames
3. **Adressage physique** : Adresses MAC source et destination
4. **Détection d'erreurs** : Vérification de l'intégrité des trames (CRC/FCS)

**PDU de la couche 2 : Trame (Frame)**

### Services de la couche liaison de données

**1. Adressage**
- Identifie les périphériques sur le média local
- Utilise les adresses MAC (48 bits)

**2. Délimitation des trames**
- Indique le début et la fin d'une trame
- Champs d'en-tête et de fin (trailer)

**3. Contrôle d'accès au média**
- Détermine quand un périphérique peut transmettre
- Gère les collisions (Ethernet : CSMA/CD)

**4. Détection d'erreurs**
- Identifie les trames corrompues
- FCS (Frame Check Sequence) : CRC-32
- Ne corrige PAS les erreurs, juste les détecte et rejette

### Sous-couches de la couche liaison de données

La couche liaison est divisée en deux sous-couches IEEE :

**1. LLC (Logical Link Control) - 802.2**
- Interface avec la couche réseau
- Identification du protocole de couche 3 (IP, IPX, etc.)
- Ajout d'informations de contrôle
- Moins utilisée aujourd'hui (rôle limité avec TCP/IP)

**2. MAC (Media Access Control)**
- Interaction avec le matériel physique
- Gestion des adresses MAC
- Encapsulation et délimitation des trames
- Accès au média et gestion des collisions
- Spécifique à chaque technologie (Ethernet, Wi-Fi, PPP, etc.)

**Schéma :**
```
┌─────────────────────┐
│   Couche Réseau     │ (Couche 3 - Paquet)
└─────────────────────┘
          ↕
┌─────────────────────┐
│  LLC (802.2)        │ (Interface protocoles)
├─────────────────────┤
│  MAC                │ (Trames, adresses MAC)
└─────────────────────┘
          ↕
┌─────────────────────┐
│  Couche Physique    │ (Couche 1 - Bits)
└─────────────────────┘
```

---

## 6.2 Topologies

### Topologies physiques vs logiques

**Topologie physique :**
- Disposition physique réelle des câbles et équipements
- Vue "câblage"

**Topologie logique :**
- Chemin logique des données à travers le réseau
- Vue du flux de données

### Topologies WAN courantes

**1. Point-à-point (Point-to-Point)**
- Connexion directe entre deux nœuds
- Lien dédié permanent
- Exemples : Liaison série entre routeurs, HDLC, PPP
- Pas de contrôle d'accès au média nécessaire (un seul émetteur/récepteur)

**Caractéristiques :**
- Full-duplex (communication bidirectionnelle simultanée)
- Bande passante dédiée
- Pas de collisions

**2. Hub-and-Spoke (Étoile)**
- Un point central connecté à plusieurs sites distants
- Hub central : Point de concentration
- Spokes : Sites périphériques
- Utilisé dans les WAN (MPLS, Frame Relay legacy)

**3. Mesh (Maillé)**
- **Full mesh** : Chaque nœud connecté à tous les autres
- **Partial mesh** : Certains nœuds interconnectés
- Haute redondance
- Coûteux (nombre de liens = n(n-1)/2 pour full mesh)

### Topologies LAN courantes

**1. Bus (Obsolète)**
- Tous les périphériques sur un seul câble linéaire
- Coaxial, terminaisons aux extrémités
- 10BASE2, 10BASE5 (Ethernet ancien)
- **Inconvénients** :
  - Point de défaillance unique
  - Collisions
  - Difficile à dépanner

**2. Étoile (Star) - Topologie LAN moderne**
- Tous les périphériques connectés à un commutateur central
- Ethernet moderne avec commutateurs
- **Avantages** :
  - Facile à installer et dépanner
  - Défaillance isolée (un câble ne coupe pas tout le réseau)
  - Évolutif
- **Inconvénient** :
  - Point de défaillance : le commutateur central

**Topologie logique Ethernet :**
- Même si physiquement en étoile, Ethernet agit logiquement comme un bus (domaine de diffusion partagé sans commutation)

**3. Étoile étendue (Extended Star)**
- Hiérarchie de commutateurs en étoile
- Commutateurs de cœur, distribution, accès
- Topologie d'entreprise courante

**4. Anneau (Ring - Obsolète côté LAN)**
- Token Ring (IEEE 802.5) - obsolète
- FDDI - fibres optiques (obsolète)
- Encore utilisé dans certains réseaux métropolitains (SONET/SDH)

---

## 6.3 Trame liaison de données

### Structure générale d'une trame

Toute trame de couche 2 contient :

```
┌────────┬────────┬─────────┬─────────┬────────┐
│ Header │  Data  │ Trailer │         │        │
└────────┴────────┴─────────┴─────────┴────────┘
```

**Composants :**

**1. En-tête (Header)**
- **Adresse de destination** : À qui est destinée la trame
- **Adresse source** : De qui provient la trame
- **Type/Longueur** : Protocole de couche supérieure ou taille des données
- **Contrôle** : Informations de contrôle (selon le protocole)

**2. Données (Data/Payload)**
- Paquet de couche 3 (IP) encapsulé
- Taille variable selon le protocole
- **MTU** (Maximum Transmission Unit) : Taille maximale des données
  - Ethernet : 1500 octets (MTU)

**3. Trailer (Queue)**
- **FCS** (Frame Check Sequence) : Détection d'erreurs (CRC)
- Utilisé pour vérifier l'intégrité de la trame

### Champs de trame variables selon le média

Les trames diffèrent selon la technologie :
- **Ethernet** : Trame Ethernet (802.3)
- **Wi-Fi** : Trame 802.11
- **PPP** : Trame PPP (liens série WAN)
- **HDLC** : Trame HDLC (Cisco, liens série)

### Types d'adresses de couche 2

**1. Unicast**
- Communication un-à-un
- Adresse MAC de destination unique
- Exemple : PC1 → PC2

**2. Broadcast**
- Communication un-vers-tous
- Adresse MAC de destination : `FF:FF:FF:FF:FF:FF`
- Tous les périphériques du réseau local reçoivent
- Exemples : ARP requests, DHCP Discover

**3. Multicast**
- Communication un-vers-plusieurs (groupe)
- Adresses MAC spéciales commençant par `01:00:5E` (IPv4) ou `33:33` (IPv6)
- Seuls les périphériques intéressés traitent
- Exemples : Streaming vidéo, protocoles de routage

---

## 💡 Points clés à retenir

1. **Couche 2 (Liaison)** : Encadre les paquets en trames, adresse MAC, détection d'erreurs
2. **Sous-couches** : LLC (interface protocoles) et MAC (accès média)
3. **Topologies** :
   - LAN : Étoile (physique et logique moderne)
   - WAN : Point-à-point, hub-and-spoke, mesh
4. **Trame** : En-tête + Données + Trailer (FCS)
5. **Adresses** : Unicast, Broadcast (FF:FF:FF:FF:FF:FF), Multicast
6. **Détection d'erreurs** : FCS (CRC-32), ne corrige pas les erreurs

---

## 🔗 Commandes IOS

```cisco
show interfaces                        # Détails de toutes les interfaces
show interfaces gi0/1                  # Détails d'une interface spécifique
show interfaces status                 # État rapide des interfaces
show mac address-table                 # Table d'adresses MAC (switch)
```

**Interpréter la sortie :**
```cisco
Switch# show interfaces gigabitEthernet 0/1
GigabitEthernet0/1 is up, line protocol is up
  Hardware is Gigabit Ethernet, address is 0cd9.96e8.8a01 (bia 0cd9.96e8.8a01)
  MTU 1500 bytes, BW 1000000 Kbit/sec
  ...
  Encapsulation ARPA, loopback not set
  Full-duplex, 1000Mb/s, media type is RJ45
  ...
  30 seconds input rate 1000 bits/sec, 2 packets/sec
  30 seconds output rate 2000 bits/sec, 3 packets/sec
  ...
  0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
  0 output errors, 0 collisions, 0 interface resets
```

**Statuts importants :**
- **up/up** : Interface activée et fonctionelle (couche 1 et 2 OK)
- **down/down** : Interface désactivée ou câble déconnecté
- **up/down** : Couche physique OK mais problème de couche 2 (protocole)
- **administratively down** : Interface désactivée volontairement (`shutdown`)

**Erreurs courantes :**
- **CRC errors** : Trames corrompues (problème câblage, interférences)
- **Collisions** : Nombreuses en half-duplex (normales), anormales en full-duplex
- **Runts** : Trames trop petites (< 64 octets)
- **Giants** : Trames trop grandes (> 1518 octets)

---

## 📝 Exercices pratiques

1. **Identifier** la topologie physique et logique d'un réseau donné

2. **Packet Tracer** :
   - Mode simulation
   - Envoyer un ping et observer la trame de couche 2
   - Observer les adresses MAC source/destination à chaque saut

3. **Comparer** les structures de trames :
   - Ethernet
   - PPP
   - 802.11 (Wi-Fi)

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
