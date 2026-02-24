# Fiche Module 03 : Modèles et protocoles
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Protocoles réseau
Un **protocole** = Ensemble de règles régissant la communication réseau

**Fonctions des protocoles :**
- **Adressage** : Identification émetteur/destinataire (IP, MAC)
- **Fiabilité** : Garantie de livraison, ACK, retransmission
- **Contrôle de flux** : Régulation de la vitesse de transmission
- **Séquencement** : Ordre de reconstruction des données
- **Détection d'erreurs** : Intégrité des données (checksum, CRC)

### Suite de protocoles TCP/IP
- **TCP** : Fiable, orienté connexion
- **IP** : Acheminement des paquets (routage)
- **HTTP/HTTPS** : Navigation web
- **FTP** : Transfert de fichiers
- **SMTP** : Envoi d'emails
- **DNS** : Résolution de noms de domaine
- **DHCP** : Attribution automatique d'adresses IP

---

## 📊 Modèle OSI (7 couches)

| Couche | Nom | Rôle | PDU | Protocoles/Exemples |
|--------|-----|------|-----|---------------------|
| **7** | **Application** | Interface utilisateur | Données | HTTP, FTP, SMTP, DNS, Telnet, SSH |
| **6** | **Présentation** | Format, chiffrement, compression | Données | SSL/TLS, JPEG, ASCII, MPEG |
| **5** | **Session** | Gestion des sessions | Données | NetBIOS, RPC, SIP |
| **4** | **Transport** | Livraison fiable (segment), ports | Segment | TCP, UDP |
| **3** | **Réseau** | Routage logique (adresses IP) | Paquet | IP, ICMP, ARP, OSPF, EIGRP |
| **2** | **Liaison de données** | Adressage physique (MAC), trames | Trame | Ethernet, PPP, HDLC, Wi-Fi (802.11) |
| **1** | **Physique** | Transmission des bits | Bits | Câbles (UTP, fibre), Wi-Fi, signaux |

**Moyen mnémotechnique (de haut en bas) :** *A* *P*ersonne *S*age *T*rouve *R*apidemment *L*es *P*roblèmes

---

## 📊 Modèle TCP/IP (4 couches)

| Couche TCP/IP | Couches OSI équivalentes | Fonction | Protocoles |
|---------------|--------------------------|----------|------------|
| **Application** | 7, 6, 5 (Application, Présentation, Session) | Services réseau aux applications | HTTP, FTP, SMTP, DNS, DHCP, Telnet, SSH |
| **Transport** | 4 (Transport) | Communication bout-en-bout, ports | TCP, UDP |
| **Internet** | 3 (Réseau) | Adressage logique IP, routage | IP, ICMP, ARP, OSPF, EIGRP |
| **Accès réseau** | 2, 1 (Liaison de données, Physique) | Accès au média physique, adresses MAC | Ethernet, Wi-Fi, PPP, câbles |

---

## 📊 Encapsulation des données

**Flux descendant (émission) :**

```
Application      →  Données
Transport        →  Segment (TCP/UDP) + Port source/destination
Réseau           →  Paquet (IP) + Adresse IP source/destination
Liaison données  →  Trame (Ethernet) + Adresse MAC source/destination
Physique         →  Bits (signaux électriques, lumière, ondes)
```

**Flux ascendant (réception) : Désencapsulation** (processus inverse)

**PDU (Protocol Data Unit) selon la couche :**
| Couche | PDU |
|--------|-----|
| Application, Présentation, Session | **Données** |
| Transport | **Segment** (TCP) ou **Datagramme** (UDP) |
| Réseau | **Paquet** |
| Liaison de données | **Trame** |
| Physique | **Bits** |

---

## 📊 Protocoles ouverts vs propriétaires

| Type | Caractéristiques | Exemples |
|------|------------------|----------|
| **Protocoles ouverts** | Standards publics, interopérabilité, gérés par organismes (IETF, IEEE) | TCP/IP, HTTP, SMTP, Ethernet (802.3), Wi-Fi (802.11) |
| **Protocoles propriétaires** | Développés par une entreprise, contrôle exclusif | Cisco EIGRP (historiquement), AppleTalk |

---

## 📊 Organismes de normalisation

| Organisme | Rôle | Standards clés |
|-----------|------|----------------|
| **IETF** | Standards Internet, RFC | TCP/IP, HTTP, FTP, SMTP |
| **IEEE** | Standards réseaux locaux | 802.3 (Ethernet), 802.11 (Wi-Fi), 802.1Q (VLANs) |
| **ISO** | Standards internationaux | Modèle OSI |
| **ITU** | Télécommunications | DSL, vidéo compression |
| **ICANN** | Noms de domaine, adresses IP | Coordination DNS, allocation IP |
| **IANA** | Allocation adresses IP, ports | Gérée par ICANN |

---

## 💡 À retenir absolument

✅ **Modèle OSI** = 7 couches (Application → Physique)  
✅ **Modèle TCP/IP** = 4 couches (Application → Accès réseau)  
✅ **PDU** : Données → Segment → Paquet → Trame → Bits  
✅ **Encapsulation** = Ajout d'en-têtes à chaque couche (descendant)  
✅ **Désencapsulation** = Retrait d'en-têtes (ascendant)  
✅ **Couche 3** = Adresses IP (logique), routage  
✅ **Couche 2** = Adresses MAC (physique), commutation  
✅ **TCP** = Fiable, orienté connexion (accusés de réception)  
✅ **UDP** = Non fiable, sans connexion (rapide, pas d'ACK)  
✅ **Protocoles applicatifs** : HTTP (web), FTP (fichiers), SMTP (email), DNS (noms → IP)  
✅ **IEEE 802.3** = Ethernet, **IEEE 802.11** = Wi-Fi  
