# 📝 Fiche de Révision - Module 9 : Résolution d'adresse

## 🎯 Concepts clés

### Problématique
- Pour communiquer sur un LAN, deux adresses nécessaires :
  - **Adresse IP (Layer 3)** : identifie logiquement l'hôte
  - **Adresse MAC (Layer 2)** : identifie physiquement la carte réseau
- **Question** : Comment connaître l'adresse MAC correspondant à une IP ?
- **Réponse** : **ARP** (IPv4) ou **NDP** (IPv6)

### ARP - Address Resolution Protocol (IPv4)
- Résout les adresses **IPv4 en MAC** sur un réseau local
- Fonctionne par **requête/réponse** (Request/Reply)
- **Requête** : broadcast (`FF:FF:FF:FF:FF:FF`)
- **Réponse** : unicast
- Maintient une **table ARP** (cache) pour éviter les requêtes répétées

### NDP - Neighbor Discovery Protocol (IPv6)
- Remplace **ARP, ICMP Router Discovery, ICMP Redirect**
- Basé sur **messages ICMPv6** (types 133-137)
- Utilise le **multicast** au lieu du broadcast (plus efficace)
- Supporte **auto-configuration (SLAAC)**, **DAD**, **détection d'inaccessibilité**

---

## 📋 Tableaux récapitulatifs

### Fonctionnement d'ARP - Requête/Réponse

#### Requête ARP (ARP Request) - BROADCAST

| Élément | Valeur |
|---------|--------|
| **MAC source** | MAC de l'émetteur (ex: AA:AA:AA:AA:AA:AA) |
| **MAC destination** | `FF:FF:FF:FF:FF:FF` (broadcast) |
| **Type Ethernet** | 0x0806 (ARP) |
| **Opcode** | 1 (Request) |
| **Sender MAC** | MAC de l'émetteur |
| **Sender IP** | IP de l'émetteur (ex: 192.168.1.10) |
| **Target MAC** | `00:00:00:00:00:00` (inconnu) |
| **Target IP** | IP recherchée (ex: 192.168.1.20) |

**Question** : *"Qui a l'adresse IP 192.168.1.20 ?"*

#### Réponse ARP (ARP Reply) - UNICAST

| Élément | Valeur |
|---------|--------|
| **MAC source** | MAC du répondant (ex: BB:BB:BB:BB:BB:BB) |
| **MAC destination** | MAC de l'émetteur (unicast) |
| **Type Ethernet** | 0x0806 (ARP) |
| **Opcode** | 2 (Reply) |
| **Sender MAC** | MAC du répondant |
| **Sender IP** | IP du répondant (ex: 192.168.1.20) |
| **Target MAC** | MAC de l'émetteur |
| **Target IP** | IP de l'émetteur |

**Réponse** : *"Je suis 192.168.1.20 et mon MAC est BB:BB:BB:BB:BB:BB"*

---

### Types d'entrées ARP

| Type | Description | Durée de vie |
|------|-------------|--------------|
| **Dynamic** | Ajoutée automatiquement | 2-10 min (Windows), 4h (Linux/Cisco) |
| **Static** | Ajoutée manuellement | Permanente jusqu'à suppression |

---

### Les 5 messages NDP (ICMPv6) ⚠️ **SECTION CRUCIALE**

| Type | Code | Nom | Rôle | Envoyé par | Destination |
|------|------|-----|------|------------|-------------|
| **133** | RS | **Router Solicitation** | Demander info aux routeurs | Hôte | `FF02::2` (all-routers) |
| **134** | RA | **Router Advertisement** | Annoncer présence routeur + config | Routeur | `FF02::1` (all-nodes) ou unicast |
| **135** | NS | **Neighbor Solicitation** | Rechercher un voisin (= ARP Request) | Hôte/Routeur | Multicast solicited-node |
| **136** | NA | **Neighbor Advertisement** | Répondre (= ARP Reply) | Hôte/Routeur | Unicast ou `FF02::1` |
| **137** | Redirect | **Redirect** | Indiquer meilleur chemin | Routeur | Unicast |

### Détails des messages NDP

#### 1. Router Solicitation (RS) - Type 133
- **Rôle** : demander aux routeurs de s'annoncer
- **Scénario** : hôte se connecte au réseau
- **Destination** : `FF02::2` (tous les routeurs)
- **Message** : *"Y a-t-il des routeurs sur ce réseau ?"*

#### 2. Router Advertisement (RA) - Type 134
- **Rôle** : annoncer la présence d'un routeur et fournir la configuration
- **Informations fournies** :
  - Préfixe IPv6 du réseau (ex: `2001:db8:acad:1::/64`)
  - Adresse link-local du routeur (passerelle par défaut)
  - Flags M/O (DHCPv6 ou non)
  - Durée de vie du préfixe
- **Auto-configuration SLAAC** : l'hôte génère son adresse avec préfixe + Interface ID
- **Destination** : `FF02::1` (all-nodes) ou unicast en réponse à RS

#### 3. Neighbor Solicitation (NS) - Type 135
- **Rôle** : découvrir l'adresse MAC d'un voisin IPv6
- **Destination** : multicast **solicited-node** `FF02::1:FF__:____` (3 derniers octets de l'IPv6 cible)
- **Utilisations** :
  1. **Résolution d'adresse** (= ARP Request)
  2. **DAD (Duplicate Address Detection)** : vérifier qu'une adresse n'est pas déjà utilisée
  3. **NUD (Neighbor Unreachability Detection)** : vérifier qu'un voisin est joignable
- **Message** : *"Qui a l'adresse 2001:db8:acad:1::20 ?"*

#### 4. Neighbor Advertisement (NA) - Type 136
- **Rôle** : répondre à un NS ou annoncer un changement
- **Destination** : unicast (réponse) ou `FF02::1` (annonce spontanée)
- **Flags** :
  - **R (Router)** : émetteur est un routeur
  - **S (Solicited)** : réponse à un NS
  - **O (Override)** : mettre à jour le cache
- **Message** : *"Je suis 2001:db8:acad:1::20 et mon MAC est BB:BB:BB:BB:BB:BB"*

#### 5. Redirect - Type 137
- **Rôle** : informer qu'un meilleur chemin existe
- **Scénario** : routeur informe l'hôte qu'un autre routeur sur le même lien est plus proche
- **Destination** : unicast vers l'hôte concerné

---

### Comparaison ARP vs NDP

| Critère | ARP (IPv4) | NDP (IPv6) |
|---------|-----------|-----------|
| **Couche** | Layer 2 | Layer 3 (ICMPv6) |
| **Type Ethernet** | 0x0806 | 0x86DD (IPv6) |
| **Requête** | Broadcast `FF:FF:FF:FF:FF:FF` | Multicast solicited-node |
| **Réponse** | Unicast | Unicast |
| **Messages** | Request, Reply (2) | RS, RA, NS, NA, Redirect (5) |
| **Auto-configuration** | Non (nécessite DHCP) | Oui (SLAAC) |
| **Détection de doublons** | Non | Oui (DAD) |
| **Découverte routeur** | Non | Oui (RS/RA) |
| **Impact réseau** | Broadcast = beaucoup de trafic | Multicast = trafic ciblé |
| **Sécurité** | Vulnérable (ARP spoofing) | Meilleure (SEcure ND possible) |

---

## ⚡ Commandes IOS essentielles

### Commandes ARP (IPv4)

#### Windows
```
C:\> arp -a                          # Afficher table ARP
C:\> arp -d                          # Supprimer toutes les entrées
C:\> arp -d 192.168.1.20             # Supprimer une entrée
C:\> arp -s 192.168.1.50 AA-BB-CC-DD-EE-FF   # Ajouter entrée statique
```

#### Linux
```
$ arp -n                             # Afficher table ARP
$ ip neighbor show                   # Afficher table ARP (nouvelle syntaxe)
$ sudo arp -d 192.168.1.20           # Supprimer entrée
$ sudo arp -s 192.168.1.50 AA:BB:CC:DD:EE:FF  # Ajouter statique
```

#### Cisco IOS
```
Router# show ip arp                  # Afficher table ARP
Router# show arp                     # Afficher table ARP
Router# clear ip arp                 # Effacer entrées dynamiques
Router# clear arp-cache              # Effacer cache ARP
Router(config)# arp 192.168.1.50 AABB.CCDD.EEFF ARPA   # Entrée statique
```

### Commandes NDP (IPv6)

#### Cisco IOS
```
Router# show ipv6 neighbors          # Afficher table des voisins IPv6
Router# clear ipv6 neighbors         # Effacer cache des voisins
Router# clear ipv6 neighbors 2001:db8:acad:1::10   # Effacer un voisin
```

#### Exemple de sortie `show ipv6 neighbors`
```
IPv6 Address                          Age  Link-layer Addr  State    Interface
2001:DB8:ACAD:1::10                   0    0030.a3e8.1234   REACH    Gi0/0
FE80::A8BB:CCFF:FE00:6700             1    aabb.cc00.6700   STALE    Gi0/1
```

### États de la découverte de voisins (NDP States)

| État | Description |
|------|-------------|
| **INCMP** (Incomplete) | Résolution en cours, NS envoyé, en attente de NA |
| **REACH** (Reachable) | Voisin joignable, communication récente confirmée |
| **STALE** (Périmé) | Entrée expirée, aucune communication récente |
| **DELAY** | En attente de confirmation de joignabilité |
| **PROBE** | Envoi de NS pour vérifier la joignabilité |

---

## 💡 Points importants pour l'examen

### ⚠️ À retenir absolument

1. **ARP : Broadcast Request → Unicast Reply**
   - Request : `FF:FF:FF:FF:FF:FF` (tous les hôtes du LAN reçoivent)
   - Reply : unicast vers l'émetteur uniquement

2. **Les 5 types de messages NDP (ICMPv6)** :
   - **133 = RS** (Router Solicitation)
   - **134 = RA** (Router Advertisement)
   - **135 = NS** (Neighbor Solicitation) = ARP Request
   - **136 = NA** (Neighbor Advertisement) = ARP Reply
   - **137 = Redirect**

3. **NS utilise multicast solicited-node** (pas broadcast)
   - Format : `FF02::1:FF__:____` (3 derniers octets de l'IPv6 cible)
   - Plus efficace que broadcast (seulement hôtes concernés)

4. **DAD (Duplicate Address Detection)** :
   - Avant d'utiliser une adresse IPv6, l'hôte envoie un NS
   - Si réponse (NA) → conflit détecté → ne pas utiliser cette adresse
   - Si pas de réponse → adresse disponible

5. **SLAAC (Stateless Address Autoconfiguration)** :
   - Grâce aux RA, l'hôte configure automatiquement :
     - Son adresse IPv6 (préfixe + Interface ID)
     - Sa passerelle par défaut (link-local du routeur)
   - Pas besoin de serveur DHCP

6. **Table ARP : durée de vie limitée**
   - Windows : 2-10 minutes
   - Linux/Cisco : 4 heures
   - Évite les requêtes répétées

7. **ARP Spoofing (attaque)** :
   - Attaquant envoie de fausses ARP Reply
   - Détourne le trafic (Man-in-the-Middle)
   - **Protection** : DAI (Dynamic ARP Inspection), Port Security

8. **NDP vs ARP** :
   - NDP = Layer 3 (ICMPv6), ARP = Layer 2
   - NDP = multicast, ARP = broadcast
   - NDP supporte auto-configuration, pas ARP

### Adresse multicast solicited-node

**Format** : `FF02::1:FF` + **3 derniers octets de l'IPv6 cible**

**Exemple** :
- IPv6 cible : `2001:db8:acad:1::0020`
- Solicited-node : `FF02::1:FF00:0020`

**Avantage** : Seulement les hôtes ayant une adresse finissant par `00:0020` traitent le message (vs tous avec broadcast).

### Scénarios d'utilisation

#### Communication sur le même LAN (IPv4)
1. Vérifier table ARP
2. Si entrée absente → envoyer ARP Request (broadcast)
3. Recevoir ARP Reply (unicast)
4. Mettre à jour table ARP
5. Encapsuler paquet avec MAC destination

#### Communication vers réseau distant (IPv4)
1. Déterminer que destination est distante (IP & masque)
2. Résoudre adresse MAC de la **passerelle par défaut** (ARP)
3. Envoyer paquet avec :
   - **IP destination** : hôte final
   - **MAC destination** : passerelle

#### Communication IPv6
- Même processus mais avec **NS/NA** au lieu d'ARP Request/Reply
- Utilise multicast solicited-node (plus efficace)

---

**🎓 Conseils pour l'examen** :
- Mémoriser les 5 types de messages NDP et leurs codes (133-137)
- Comprendre la différence entre broadcast (ARP) et multicast solicited-node (NDP)
- Savoir que NS peut servir à la résolution d'adresse ET au DAD
- Connaître les états de découverte (REACH, STALE, INCMP)
- Comprendre SLAAC et le rôle des RA
