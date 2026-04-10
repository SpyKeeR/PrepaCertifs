# Fiche Module 14 - Protocoles de Transport (TCP/UDP)

**Date :** 27 février 2026  
**Cours :** CCNA ITN  
**Sujet :** Protocoles de la couche Transport (Layer 4)

---

## 🎯 Concepts clés

**Rôle de la couche Transport :**
- Segmentation des données
- Multiplexage via numéros de ports
- Contrôle de flux (TCP uniquement)
- Fiabilité et réassemblage (TCP uniquement)

---

## 📋 Tableaux récapitulatifs

### Comparaison TCP vs UDP

| Critère | TCP | UDP |
|---------|-----|-----|
| **Type** | Orienté connexion | Sans connexion |
| **Fiabilité** | Fiable (ACK, retransmission) | Non fiable (best effort) |
| **Ordre** | Garanti (SEQ) | Non garanti |
| **Overhead** | 20-60 octets | 8 octets |
| **Vitesse** | Plus lent | Rapide |
| **Contrôle de flux** | Oui (fenêtre glissante) | Non |
| **Contrôle de congestion** | Oui (Slow Start, Congestion Avoidance) | Non |
| **Connexion** | 3-way handshake | Aucune |
| **Diffusion** | Unicast seulement | Unicast, multicast, broadcast |
| **Applications** | HTTP, HTTPS, FTP, SSH, SMTP | DNS, DHCP, TFTP, VoIP, streaming |

### En-tête TCP (20-60 octets)

| Champ | Taille | Rôle |
|-------|--------|------|
| **Source Port** | 16 bits | Port source (0-65535) |
| **Destination Port** | 16 bits | Port destination (0-65535) |
| **Sequence Number (SEQ)** | 32 bits | Numéro du 1er octet de données |
| **Acknowledgment (ACK)** | 32 bits | Prochain octet attendu (acquittement cumulatif) |
| **Data Offset** | 4 bits | Longueur en-tête en mots de 32 bits (min: 5, max: 15) |
| **Flags (Control Bits)** | 9 bits | SYN, ACK, FIN, RST, PSH, URG, etc. |
| **Window Size** | 16 bits | Taille buffer récepteur (octets) - Contrôle de flux |
| **Checksum** | 16 bits | Intégrité en-tête + données |
| **Urgent Pointer** | 16 bits | Décalage données urgentes (si URG=1) |
| **Options** | 0-40 octets | MSS, Window Scale, SACK, Timestamps |

### Flags TCP (Bits de contrôle)

| Flag | Nom | Rôle | Usage |
|------|-----|------|-------|
| **SYN** | Synchronize | Initialiser connexion | 3-way handshake (étapes 1 et 2) |
| **ACK** | Acknowledgment | Acquitter réception | Présent dans tous les segments après SYN |
| **FIN** | Finish | Terminer connexion proprement | 4-way termination |
| **RST** | Reset | Réinitialiser connexion brutalement | Erreur, port fermé, attaque |
| **PSH** | Push | Envoyer immédiatement à l'application | Données urgentes, pas de buffer |
| **URG** | Urgent | Données urgentes | Rarement utilisé |

### En-tête UDP (8 octets)

| Champ | Taille | Rôle |
|-------|--------|------|
| **Source Port** | 16 bits | Port source (optionnel, peut être 0) |
| **Destination Port** | 16 bits | Port destination (obligatoire) |
| **Length** | 16 bits | Longueur totale (en-tête + données) |
| **Checksum** | 16 bits | Intégrité. **Optionnel IPv4, obligatoire IPv6** |

### Ports courants

#### TCP

| Port | Service | Description |
|------|---------|-------------|
| 20-21 | FTP | File Transfer Protocol (données/contrôle) |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Telnet (non sécurisé) |
| 25 | SMTP | Simple Mail Transfer Protocol |
| 80 | HTTP | HyperText Transfer Protocol |
| 110 | POP3 | Post Office Protocol v3 |
| 143 | IMAP | Internet Message Access Protocol |
| 443 | HTTPS | HTTP Secure (TLS) |
| 445 | SMB | Server Message Block |
| 3389 | RDP | Remote Desktop Protocol |

#### UDP

| Port | Service | Description |
|------|---------|-------------|
| 53 | DNS | Domain Name System |
| 67-68 | DHCP | Dynamic Host Configuration Protocol |
| 69 | TFTP | Trivial File Transfer Protocol |
| 123 | NTP | Network Time Protocol |
| 161-162 | SNMP | Simple Network Management Protocol |
| 514 | Syslog | Logs système |

---

## ⚡ Mécanismes TCP essentiels

### 3-Way Handshake (Établissement connexion)

```
Client                          Serveur
   |                                |
   | SYN (SEQ=1000)                 |
   |------------------------------->|
   |                                |
   | SYN-ACK (SEQ=5000, ACK=1001)   |
   |<-------------------------------|
   |                                |
   | ACK (SEQ=1001, ACK=5001)       |
   |------------------------------->|
   |                                |
   |     Connexion établie          |
```

**Étapes :**
1. Client → Serveur : SYN (SEQ=X)
2. Serveur → Client : SYN-ACK (SEQ=Y, ACK=X+1)
3. Client → Serveur : ACK (SEQ=X+1, ACK=Y+1)

### 4-Way Termination (Fermeture connexion)

```
Client                          Serveur
   |                                |
   | FIN (SEQ=1500, ACK=6000)       |
   |------------------------------->|
   |                                |
   | ACK (SEQ=6000, ACK=1501)       |
   |<-------------------------------|
   |                                |
   | FIN (SEQ=6000, ACK=1501)       |
   |<-------------------------------|
   |                                |
   | ACK (SEQ=1501, ACK=6001)       |
   |------------------------------->|
   |                                |
   |     Connexion fermée           |
```

**Étapes :**
1. Client → Serveur : FIN
2. Serveur → Client : ACK
3. Serveur → Client : FIN
4. Client → Serveur : ACK

### Fenêtre glissante (Sliding Window)

**Contrôle de flux pour protéger le récepteur**

- **Window Size** : Taille du buffer récepteur (en octets)
- Permet d'envoyer **plusieurs segments sans attendre ACK**
- Adaptation dynamique : Window Size = 0 → arrêt émission

**Formule :** 
```
Nombre de segments = Window Size / MSS
```

**Exemple :**
- Window Size = 6000 octets
- MSS = 1500 octets
- Nb segments envoyés : 6000 / 1500 = 4 segments

**Window Scaling (RFC 1323) :**
- Multiplie Window Size par $2^n$ (n jusqu'à 14)
- Max : 65 535 × $2^{14}$ = **1 Go**

### Contrôle de congestion

**Protéger le réseau (routeurs surchargés)**

#### 1. Slow Start (Démarrage lent)

- CWND (Congestion Window) = 1 MSS au début
- **Croissance exponentielle** : CWND double à chaque ACK
- Progression : 1 → 2 → 4 → 8 → 16 MSS

#### 2. Congestion Avoidance (Évitement congestion)

- Quand CWND atteint **ssthresh** (slow start threshold)
- **Croissance linéaire** : +1 MSS par RTT
- Plus prudent pour éviter saturation réseau

#### 3. Réaction à la perte

**Perte détectée** (timeout ou 3 ACK dupliqués) :
- ssthresh = CWND / 2
- CWND = 1 MSS (recommence Slow Start)

**Algorithmes courants :**
- TCP Reno : Fast Retransmit + Fast Recovery
- TCP CUBIC : Croissance cubique (Linux moderne)
- TCP BBR : Base sur bande passante et RTT (Google)

### Numéros SEQ et ACK

**Exemple :**
```
Client → Serveur : SEQ=1000, 100 octets de données
Serveur → Client : ACK=1100 (j'attends octet 1100, donc reçu jusqu'à 1099)

Client → Serveur : SEQ=1100, 50 octets de données
Serveur → Client : ACK=1150
```

- **SEQ** : Numéro du **premier octet** de données
- **ACK** : Numéro du **prochain octet attendu** (acquittement cumulatif)

### MSS (Maximum Segment Size)

**Calcul :**
```
MSS = MTU - IP Header - TCP Header
MSS = 1500 - 20 - 20 = 1460 octets (typique)
```

---

## 💡 Points examen

**TCP :**
- ✅ En-tête 20-60 octets (vs UDP 8 octets)
- ✅ SEQ = numéro 1er octet, ACK = prochain octet attendu
- ✅ Flags : SYN (connexion), ACK (acquittement), FIN (fermeture), RST (reset)
- ✅ 3-way handshake : SYN → SYN-ACK → ACK
- ✅ 4-way termination : FIN → ACK → FIN → ACK
- ✅ Window Size : contrôle de flux (octets)
- ✅ Slow Start : croissance exponentielle (double à chaque ACK)
- ✅ Congestion Avoidance : croissance linéaire (+1 MSS/RTT)

**UDP :**
- ✅ En-tête 8 octets seulement
- ✅ Checksum **optionnel IPv4**, **obligatoire IPv6**
- ✅ Source Port optionnel (peut être 0)
- ✅ Pas de connexion, pas d'ACK, pas de retransmission
- ✅ Applications temps réel : VoIP, streaming, jeux

**Ports :**
- ✅ 0-1023 : Well-known (réservés)
- ✅ 1024-49151 : Registered
- ✅ 49152-65535 : Dynamic/Private (éphémères)

**Commandes diagnostic :**
```powershell
# Windows
netstat -an        # Liste connexions actives
netstat -anb       # Avec processus

# Linux
ss -tunap          # Connexions TCP/UDP
netstat -tunap     # Connexions (ancien)
```

---

## ⚡ Révision rapide

1. **TCP** = fiable, connexion, overhead élevé (20-60 octets) | **UDP** = rapide, sans connexion, léger (8 octets)
2. **3-way handshake** : SYN → SYN-ACK → ACK | **4-way termination** : FIN → ACK → FIN → ACK
3. **Flags TCP** : SYN (connexion), ACK (acquit), FIN (fermeture), RST (reset), PSH (push), URG (urgent)
4. **Window Size** : contrôle de flux (buffer récepteur) | **Slow Start** : CWND × 2 | **Congestion Avoidance** : CWND +1/RTT
5. **UDP Checksum** : optionnel IPv4, **obligatoire IPv6** | MSS = MTU - IP hdr - TCP hdr = 1460 octets
