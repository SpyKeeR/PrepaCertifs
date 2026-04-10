# Module 14 - Protocoles de Transport (TCP/UDP)

**Date :** 27 février 2026  
**Cours :** CCNA ITN (Introduction to Networks)  
**Sujet :** Protocoles de la couche Transport (Layer 4)

---

## 1. Introduction à la couche Transport

### Rôle de la couche 4

La **couche Transport** (Layer 4 du modèle OSI) est responsable de :
- **Segmentation** : découper les données en segments/datagrammes
- **Multiplexage** : permettre plusieurs applications simultanées via les ports
- **Contrôle de flux** : éviter la surcharge du récepteur
- **Fiabilité** (TCP uniquement) : garantir la livraison des données
- **Réassemblage** : reconstituer les données dans l'ordre

### Les deux protocoles principaux

| Protocole | Type | Fiabilité | Connexion | Overhead | Cas d'usage |
|-----------|------|-----------|-----------|----------|-------------|
| **TCP** (Transmission Control Protocol) | Orienté connexion | Fiable | Établissement connexion (3-way handshake) | Élevé | HTTP, HTTPS, FTP, SSH, SMTP |
| **UDP** (User Datagram Protocol) | Sans connexion | Non fiable (best effort) | Aucune connexion | Faible | DNS, DHCP, TFTP, VoIP, streaming |

---

## 2. TCP (Transmission Control Protocol)

### 2.1 Caractéristiques de TCP

TCP est un protocole **orienté connexion** et **fiable** :
- ✅ **Établissement de connexion** : 3-way handshake (SYN, SYN-ACK, ACK)
- ✅ **Fiabilité** : accusé de réception (ACK), retransmission si perte
- ✅ **Contrôle de flux** : fenêtre glissante (sliding window)
- ✅ **Contrôle de congestion** : adaptation au trafic réseau
- ✅ **Ordre des données** : numéros de séquence (SEQ)
- ✅ **Full-duplex** : communication bidirectionnelle simultanée

### 2.2 En-tête TCP (Détails complets)

L'en-tête TCP fait **20 octets minimum** (peut atteindre 60 octets avec options) :

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
| Offset|Rsvd |N|C|E|U|A|P|R|S|F|           Window Size         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options (0-40 bytes)                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

#### 📋 Détails des champs de l'en-tête TCP

| Champ | Taille | Rôle |
|-------|--------|------|
| **Source Port** | 16 bits | Port de l'application source (0-65535) |
| **Destination Port** | 16 bits | Port de l'application destination (0-65535) |
| **Sequence Number (SEQ)** | 32 bits | Numéro du premier octet de données dans ce segment. Utilisé pour réordonner les segments et détecter les pertes. |
| **Acknowledgment Number (ACK)** | 32 bits | Numéro du prochain octet attendu (si flag ACK=1). Confirme la réception jusqu'à SEQ-1. |
| **Data Offset (Header Length)** | 4 bits | Longueur de l'en-tête TCP en mots de 32 bits (min: 5 = 20 octets, max: 15 = 60 octets) |
| **Reserved** | 3 bits | Réservé pour usage futur (toujours à 0) |
| **Flags (Control Bits)** | 9 bits | Bits de contrôle : NS, CWR, ECE, URG, ACK, PSH, RST, SYN, FIN |
| **Window Size** | 16 bits | Taille de la fenêtre de réception (contrôle de flux) en octets. Max: 65 535 octets (extensible avec option Window Scale) |
| **Checksum** | 16 bits | Somme de contrôle pour vérifier l'intégrité de l'en-tête + données + pseudo-en-tête IP |
| **Urgent Pointer** | 16 bits | Décalage des données urgentes (si flag URG=1) |
| **Options** | 0-40 octets | Options TCP : MSS, Window Scale, SACK, Timestamps, etc. |

### 2.3 Bits de contrôle (Flags TCP)

Les **6 flags principaux** à connaître pour l'examen CCNA :

| Flag | Nom | Rôle | Usage typique |
|------|-----|------|---------------|
| **SYN** | Synchronize | Initialiser une connexion | 3-way handshake (étape 1 et 2) |
| **ACK** | Acknowledgment | Acquitter la réception de données | Présent dans presque tous les segments après connexion |
| **FIN** | Finish | Terminer proprement une connexion | 4-way termination (étape 1 et 3) |
| **RST** | Reset | Réinitialiser brutalement une connexion | Erreur, port fermé, attaque |
| **PSH** | Push | Envoyer immédiatement au processus applicatif | Données urgentes à traiter sans buffer |
| **URG** | Urgent | Données urgentes présentes | Rarement utilisé, données prioritaires |

**Flags additionnels** (moins courants) :
- **NS** (ECN-nonce) : Protection contre dissimulation de congestion
- **CWR** (Congestion Window Reduced) : Réponse à notification ECE
- **ECE** (ECN-Echo) : Notification de congestion réseau

### 2.4 Numéros de séquence (SEQ) et d'acquittement (ACK)

#### Principe

- **SEQ** : Numéro du **premier octet** de données dans le segment
- **ACK** : Numéro du **prochain octet attendu** (acquittement cumulatif)

#### Exemple de communication TCP

```
Client → Serveur : SEQ=1000, 100 octets de données
Serveur → Client : ACK=1100 (j'attends l'octet 1100, donc j'ai bien reçu jusqu'à 1099)

Client → Serveur : SEQ=1100, 50 octets de données
Serveur → Client : ACK=1150
```

#### 3-Way Handshake (Établissement de connexion)

```
Client                          Serveur
   |                                |
   |  SYN (SEQ=1000)                |
   |------------------------------->|
   |                                |
   |  SYN-ACK (SEQ=5000, ACK=1001)  |
   |<-------------------------------|
   |                                |
   |  ACK (SEQ=1001, ACK=5001)      |
   |------------------------------->|
   |                                |
   |     Connexion établie          |
```

**Détails :**
1. **Client → Serveur** : SYN (SEQ=1000, ACK=0, flag SYN=1)
   - Le client choisit un numéro de séquence initial (ISN) aléatoire : 1000
2. **Serveur → Client** : SYN-ACK (SEQ=5000, ACK=1001, flags SYN=1, ACK=1)
   - Le serveur choisit son propre ISN : 5000
   - Il acquitte le SYN du client : ACK=1001 (prochain octet attendu)
3. **Client → Serveur** : ACK (SEQ=1001, ACK=5001, flag ACK=1)
   - Le client acquitte le SYN du serveur : ACK=5001

#### 4-Way Termination (Fermeture de connexion)

```
Client                          Serveur
   |                                |
   |  FIN (SEQ=1500, ACK=6000)      |
   |------------------------------->|
   |                                |
   |  ACK (SEQ=6000, ACK=1501)      |
   |<-------------------------------|
   |                                |
   |  FIN (SEQ=6000, ACK=1501)      |
   |<-------------------------------|
   |                                |
   |  ACK (SEQ=1501, ACK=6001)      |
   |------------------------------->|
   |                                |
   |     Connexion fermée           |
```

**Détails :**
1. **Client → Serveur** : FIN (je n'ai plus de données à envoyer)
2. **Serveur → Client** : ACK (j'ai reçu ton FIN)
3. **Serveur → Client** : FIN (je termine aussi)
4. **Client → Serveur** : ACK (j'ai reçu ton FIN)

### 2.5 Fenêtre glissante (Sliding Window)

#### Principe du contrôle de flux

La **fenêtre glissante** est un mécanisme de **contrôle de flux** qui permet :
- D'envoyer plusieurs segments **sans attendre un ACK pour chaque segment**
- D'ajuster le débit en fonction de la capacité du récepteur
- D'éviter la **surcharge du buffer** du récepteur

#### Fonctionnement

Le champ **Window Size** (16 bits) indique la quantité de données (en octets) que le récepteur peut accepter **sans acquittement**.

**Exemple :**
```
Récepteur annonce : Window Size = 6000 octets

Émetteur peut envoyer :
- Segment 1 : 1500 octets (SEQ=1000)
- Segment 2 : 1500 octets (SEQ=2500)
- Segment 3 : 1500 octets (SEQ=4000)
- Segment 4 : 1500 octets (SEQ=5500)

Total : 6000 octets envoyés SANS attendre d'ACK

Émetteur doit maintenant attendre un ACK avant d'envoyer plus de données.
```

#### Adaptation dynamique

Le récepteur peut **ajuster la taille de la fenêtre** :
- **Buffer plein** → Window Size = 0 (stop l'émission)
- **Buffer vide** → Window Size augmente (reprise de l'émission)

**Exemple :**
```
Récepteur : Window Size = 6000
Émetteur envoie 6000 octets

Récepteur traite 3000 octets, renvoie : ACK + Window Size = 3000
Émetteur peut envoyer 3000 octets supplémentaires

Récepteur traite tout, renvoie : ACK + Window Size = 6000
Émetteur peut à nouveau envoyer 6000 octets
```

#### Window Scaling (Option TCP)

Pour les réseaux à haute capacité, le champ Window Size (16 bits = max 65 535) est trop petit.

**Solution** : Option **Window Scale** (RFC 1323)
- Multiplie Window Size par 2^n (n jusqu'à 14)
- Window Size effective max : 65 535 × 2^14 = **1 Go**

### 2.6 Contrôle de congestion (Congestion Control)

#### Différence avec le contrôle de flux

| Type | Objectif | Régulé par |
|------|----------|------------|
| **Contrôle de flux** (Flow Control) | Protéger le **récepteur** (buffer plein) | Window Size du récepteur |
| **Contrôle de congestion** (Congestion Control) | Protéger le **réseau** (routeurs surchargés) | Émetteur détecte pertes et adapte |

#### Mécanismes de contrôle de congestion

##### 1. Slow Start (Démarrage lent)

Au **début de la connexion**, l'émetteur ne connaît pas la capacité du réseau.

**Principe :**
- L'émetteur commence avec une petite **fenêtre de congestion** (CWND) : 1 MSS (Maximum Segment Size, typiquement 1460 octets)
- À chaque ACK reçu, CWND **double** : 1 → 2 → 4 → 8 → 16 MSS
- Croissance **exponentielle** rapide

**Exemple :**
```
CWND = 1 MSS   → Envoie 1 segment
ACK reçu       → CWND = 2 MSS
                → Envoie 2 segments
ACK reçu (×2)  → CWND = 4 MSS
                → Envoie 4 segments
ACK reçu (×4)  → CWND = 8 MSS
```

##### 2. Congestion Avoidance (Évitement de congestion)

Quand CWND atteint un **seuil** (ssthresh = slow start threshold) :
- Passage en mode **Congestion Avoidance**
- Croissance **linéaire** : +1 MSS par RTT (Round-Trip Time)
- Plus prudent pour ne pas saturer le réseau

**Exemple :**
```
CWND = 16 MSS (atteint ssthresh)
RTT 1 → CWND = 17 MSS
RTT 2 → CWND = 18 MSS
RTT 3 → CWND = 19 MSS
```

##### 3. Réaction à la perte (Congestion Detected)

**Perte détectée** : timeout ou 3 ACK dupliqués

**Actions :**
- **ssthresh = CWND / 2** (réduit le seuil)
- **CWND = 1 MSS** (recommence Slow Start)
- Adaptation : le réseau était congestionné

**Exemple :**
```
CWND = 32 MSS
Perte détectée (timeout)
→ ssthresh = 32 / 2 = 16 MSS
→ CWND = 1 MSS (reprendre Slow Start)
→ Croissance exponentielle jusqu'à 16 MSS
→ Puis croissance linéaire
```

##### 4. Fast Retransmit et Fast Recovery

**Fast Retransmit** :
- Si **3 ACK dupliqués** reçus (même numéro ACK) → retransmission immédiate sans attendre le timeout
- Plus rapide que d'attendre le timer

**Fast Recovery** :
- Après Fast Retransmit, ne revient pas à CWND=1
- **CWND = ssthresh + 3 MSS** (plus doux)
- Reste en Congestion Avoidance

#### Algorithmes de congestion

| Algorithme | Variante | Caractéristique |
|------------|----------|-----------------|
| **TCP Reno** | Classique | Fast Retransmit + Fast Recovery |
| **TCP Tahoe** | Ancien | Retour à CWND=1 sur perte |
| **TCP New Reno** | Amélioration | Gestion multiple pertes |
| **TCP CUBIC** | Moderne (Linux) | Croissance cubique, meilleure performance LFN |
| **TCP BBR** | Google | Base sur bande passante et RTT, pas sur pertes |

### 2.7 Numérotation des ports TCP

| Plage | Type | Utilisation |
|-------|------|-------------|
| **0-1023** | **Well-known ports** | Ports réservés pour services standards (HTTP, FTP, SSH, etc.) |
| **1024-49151** | **Registered ports** | Ports enregistrés par l'IANA pour applications spécifiques |
| **49152-65535** | **Dynamic/Private ports** | Ports éphémères pour connexions clientes |

#### Ports TCP courants

| Port | Service | Protocole |
|------|---------|-----------|
| 20 | FTP Data | File Transfer Protocol (données) |
| 21 | FTP Control | File Transfer Protocol (contrôle) |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Telnet (non sécurisé) |
| 25 | SMTP | Simple Mail Transfer Protocol (envoi email) |
| 53 | DNS | Domain Name System (peut aussi utiliser UDP) |
| 80 | HTTP | HyperText Transfer Protocol |
| 110 | POP3 | Post Office Protocol v3 (réception email) |
| 143 | IMAP | Internet Message Access Protocol (email) |
| 443 | HTTPS | HTTP Secure (SSL/TLS) |
| 3389 | RDP | Remote Desktop Protocol |
| 445 | SMB | Server Message Block (partage fichiers) |

### 2.8 Fiabilité TCP

#### Mécanismes de fiabilité

1. **Numérotation des segments** : Réordonnancement via SEQ
2. **Accusés de réception (ACK)** : Confirmation de réception
3. **Retransmission** : Renvoi des segments perdus après timeout
4. **Checksum** : Détection d'erreurs dans l'en-tête et les données
5. **Contrôle de flux** : Fenêtre glissante pour éviter surcharge récepteur
6. **Contrôle de congestion** : Adaptation au trafic réseau

#### Retransmission Timeout (RTO)

Quand l'émetteur n'a pas reçu d'ACK dans un **délai** (Retransmission Timeout) :
- **Retransmission** du segment
- **RTO dynamique** : calculé en fonction du RTT (Round-Trip Time)
- Formule : RTO ≈ RTT + 4 × RTT_deviation

---

## 3. UDP (User Datagram Protocol)

### 3.1 Caractéristiques d'UDP

UDP est un protocole **sans connexion** et **non fiable** (best effort) :
- ❌ **Pas d'établissement de connexion** : envoi direct
- ❌ **Pas de fiabilité** : pas d'ACK, pas de retransmission
- ❌ **Pas de contrôle de flux** : pas de fenêtre glissante
- ❌ **Pas de contrôle de congestion** : pas d'adaptation au réseau
- ❌ **Pas d'ordre garanti** : les datagrammes peuvent arriver dans le désordre
- ✅ **Léger et rapide** : overhead minimal (8 octets d'en-tête)
- ✅ **Multicast/Broadcast** : supporte la diffusion
- ✅ **Applications temps réel** : VoIP, streaming vidéo, jeux en ligne

### 3.2 En-tête UDP (Détails complets)

L'en-tête UDP fait **seulement 8 octets** :

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Length             |           Checksum            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

#### 📋 Détails des champs de l'en-tête UDP

| Champ | Taille | Rôle |
|-------|--------|------|
| **Source Port** | 16 bits | Port de l'application source (0-65535). **Optionnel**, peut être 0 si pas de réponse attendue. |
| **Destination Port** | 16 bits | Port de l'application destination (0-65535). **Obligatoire**. |
| **Length** | 16 bits | Longueur totale du datagramme UDP (en-tête 8 octets + données). Min: 8 octets, Max: 65 535 octets. |
| **Checksum** | 16 bits | Somme de contrôle pour vérifier l'intégrité de l'en-tête + données + pseudo-en-tête IP. **Optionnel en IPv4** (peut être 0), **obligatoire en IPv6**. |

#### Importance du Checksum UDP

Contrairement à une idée reçue, **UDP possède bien un checksum** :
- **IPv4** : Checksum **optionnel** (peut être mis à 0 si non calculé)
- **IPv6** : Checksum **obligatoire** (RFC 2460)

**Rôle du checksum** :
- Détecte les erreurs de transmission (bits flippés, corruption)
- Vérifie l'intégrité de l'**en-tête UDP + données + pseudo-en-tête IP**
- Si checksum incorrect → datagramme **éliminé silencieusement**

**Pseudo-en-tête IP** (utilisé dans le calcul du checksum) :
```
+--------+--------+--------+--------+
|     Source IP Address (32 bits)  |
+--------+--------+--------+--------+
|  Destination IP Address (32 bits)|
+--------+--------+--------+--------+
|  Zero  |Protocol|   UDP Length    |
+--------+--------+--------+--------+

Protocol = 17 (UDP)
UDP Length = longueur en-tête + données
```

### 3.3 Numérotation des ports UDP

Même système que TCP :

| Plage | Type | Utilisation |
|-------|------|-------------|
| **0-1023** | **Well-known ports** | Ports réservés pour services standards |
| **1024-49151** | **Registered ports** | Ports enregistrés IANA |
| **49152-65535** | **Dynamic/Private ports** | Ports éphémères |

#### Ports UDP courants

| Port | Service | Protocole |
|------|---------|-----------|
| 53 | DNS | Domain Name System (requêtes/réponses DNS) |
| 67 | DHCP Server | Dynamic Host Configuration Protocol (serveur) |
| 68 | DHCP Client | Dynamic Host Configuration Protocol (client) |
| 69 | TFTP | Trivial File Transfer Protocol |
| 123 | NTP | Network Time Protocol (synchronisation horloge) |
| 161 | SNMP | Simple Network Management Protocol |
| 162 | SNMP Trap | SNMP Trap (notifications) |
| 514 | Syslog | Syslog (logs système) |
| 520 | RIP | Routing Information Protocol |
| 5060 | SIP | Session Initiation Protocol (VoIP) |
| 5353 | mDNS | Multicast DNS |

---

## 4. Comparaison TCP vs UDP

### 4.1 Tableau récapitulatif

| Critère | TCP | UDP |
|---------|-----|-----|
| **Type** | Orienté connexion | Sans connexion |
| **Fiabilité** | Fiable (ACK, retransmission) | Non fiable (best effort) |
| **Ordre** | Ordre garanti (SEQ) | Pas d'ordre garanti |
| **Overhead** | Élevé (20-60 octets en-tête) | Faible (8 octets en-tête) |
| **Vitesse** | Plus lent (établissement, contrôle) | Rapide |
| **Contrôle de flux** | Oui (fenêtre glissante) | Non |
| **Contrôle de congestion** | Oui (Slow Start, Congestion Avoidance) | Non |
| **Connexion** | 3-way handshake (SYN, SYN-ACK, ACK) | Aucune |
| **Fermeture** | 4-way termination (FIN, ACK, FIN, ACK) | Aucune |
| **Checksum** | Obligatoire | Optionnel IPv4, obligatoire IPv6 |
| **Diffusion** | Unicast seulement | Unicast, multicast, broadcast |
| **Applications** | HTTP, HTTPS, FTP, SSH, SMTP, POP, IMAP, Telnet | DNS, DHCP, TFTP, NTP, SNMP, VoIP, streaming |

### 4.2 Quand utiliser TCP ou UDP ?

#### Utiliser TCP quand :
- ✅ **Fiabilité critique** : transfert de fichiers, emails, pages web
- ✅ **Ordre important** : données séquentielles
- ✅ **Intégrité des données** : aucune perte acceptable
- ✅ **Sessions longues** : connexions persistantes

**Exemples :** HTTP/HTTPS, FTP, SSH, SMTP, POP, IMAP, Telnet, bases de données

#### Utiliser UDP quand :
- ✅ **Vitesse prioritaire** : applications temps réel
- ✅ **Perte acceptable** : quelques paquets perdus = OK
- ✅ **Overhead minimal** : pas de surcharge protocole
- ✅ **Broadcast/Multicast** : diffusion vers plusieurs destinataires
- ✅ **Requêtes simples** : question/réponse rapide

**Exemples :** VoIP, streaming vidéo/audio, jeux en ligne, DNS, DHCP, TFTP, NTP, SNMP

### 4.3 Applications hybrides

Certaines applications utilisent **les deux protocoles** :

| Application | TCP | UDP |
|-------------|-----|-----|
| **DNS** | Transferts de zones (AXFR) > 512 octets | Requêtes/réponses < 512 octets |
| **DHCP** | - | Allocation d'adresses (broadcast) |
| **RTP/RTCP** | - | RTP (média), RTCP (contrôle) |
| **QUIC** | - | UDP + fiabilité applicative (HTTP/3) |

---

## 5. Multiplexage et Démultiplexage

### 5.1 Principe

Le **multiplexage** permet à plusieurs applications d'utiliser le réseau simultanément via les **numéros de ports**.

**Multiplexage (émission)** :
- Plusieurs applications envoient des données
- Chaque application utilise un port unique
- La couche Transport ajoute le numéro de port dans l'en-tête

**Démultiplexage (réception)** :
- La couche Transport reçoit des segments
- Elle lit le **Destination Port** dans l'en-tête
- Elle envoie les données à l'application correspondante

### 5.2 Identification d'une session TCP

Une session TCP est identifiée par un **tuple à 5 éléments** :
1. **Adresse IP source**
2. **Port source**
3. **Adresse IP destination**
4. **Port destination**
5. **Protocole** (TCP = 6)

**Exemple :**
```
Session 1 : 192.168.1.10:54321 → 93.184.216.34:80 (TCP)
Session 2 : 192.168.1.10:54322 → 93.184.216.34:80 (TCP)

Ces deux sessions sont DISTINCTES (ports sources différents)
```

### 5.3 Sockets

Un **socket** est un point de terminaison de communication :
- **Format** : IP:Port
- **Exemple** : 192.168.1.10:80

**Types de sockets** :
- **Socket TCP** : connexion orientée (stream socket)
- **Socket UDP** : sans connexion (datagram socket)

---

## 6. Maximum Segment Size (MSS)

### Définition

Le **MSS (Maximum Segment Size)** est la **taille maximale des données** dans un segment TCP (sans compter l'en-tête TCP/IP).

**Calcul :**
```
MSS = MTU - IP Header - TCP Header
MSS = 1500 - 20 - 20 = 1460 octets (typique)
```

- **MTU (Maximum Transmission Unit)** : 1500 octets (Ethernet)
- **En-tête IP** : 20 octets (sans options)
- **En-tête TCP** : 20 octets (minimum)

### Négociation du MSS

Le MSS est **négocié lors du 3-way handshake** :
- Chaque partie annonce son MSS dans **l'option TCP MSS**
- Le MSS effectif = **minimum des deux MSS**

**Exemple :**
```
Client → Serveur : SYN + MSS=1460
Serveur → Client : SYN-ACK + MSS=1400
→ MSS effectif = 1400 octets
```

### Path MTU Discovery (PMTUD)

**Problème** : Le chemin réseau peut avoir un MTU plus petit que 1500 octets.

**Solution** : **PMTUD (Path MTU Discovery)**
1. L'émetteur envoie des paquets avec **DF=1** (Don't Fragment)
2. Si un routeur doit fragmenter → **ICMP Type 3 Code 4** (Fragmentation Needed)
3. L'émetteur **réduit le MSS** et réessaie
4. Répète jusqu'à trouver le MTU optimal

---

## 7. États TCP (TCP State Machine)

Une connexion TCP passe par plusieurs **états** :

### États principaux

| État | Description |
|------|-------------|
| **CLOSED** | Aucune connexion |
| **LISTEN** | Serveur attend des connexions (port ouvert) |
| **SYN-SENT** | Client a envoyé SYN, attend SYN-ACK |
| **SYN-RECEIVED** | Serveur a reçu SYN, a envoyé SYN-ACK, attend ACK |
| **ESTABLISHED** | Connexion établie, transfert de données |
| **FIN-WAIT-1** | Application a fermé, FIN envoyé, attend ACK |
| **FIN-WAIT-2** | ACK reçu, attend FIN de l'autre côté |
| **CLOSE-WAIT** | FIN reçu, attend que l'application locale ferme |
| **CLOSING** | Les deux côtés ferment simultanément |
| **LAST-ACK** | FIN envoyé, attend dernier ACK |
| **TIME-WAIT** | Attente 2×MSL (Maximum Segment Lifetime) avant fermeture complète |

### Commande de diagnostic

**Afficher les connexions TCP actives** :
```bash
# Windows
netstat -an

# Linux
ss -tunap
netstat -tunap
```

**Exemple de sortie** :
```
Proto  Local Address    Foreign Address  State
TCP    0.0.0.0:22       0.0.0.0:0        LISTEN
TCP    192.168.1.10:54321  93.184.216.34:80  ESTABLISHED
TCP    192.168.1.10:54322  93.184.216.34:443 TIME-WAIT
```

---

## 8. Segmentation et Réassemblage

### Processus d'envoi (Émetteur)

1. **Application** envoie des données (ex: 10 000 octets)
2. **Couche Transport** segmente en plusieurs segments :
   - Segment 1 : SEQ=1, 1460 octets de données
   - Segment 2 : SEQ=1461, 1460 octets de données
   - Segment 3 : SEQ=2921, 1460 octets de données
   - Segment 4 : SEQ=4381, 1460 octets de données
   - Segment 5 : SEQ=5841, 1460 octets de données
   - Segment 6 : SEQ=7301, 1460 octets de données
   - Segment 7 : SEQ=8761, 1240 octets de données
3. **Couche IP** encapsule chaque segment dans un paquet IP
4. **Couche Liaison** encapsule dans une trame Ethernet

### Processus de réception (Récepteur)

1. **Couche Liaison** décapsule la trame
2. **Couche IP** décapsule le paquet
3. **Couche Transport** lit le port destination, réordonne les segments via SEQ
4. **Application** reçoit les données complètes (10 000 octets)

---

## 9. Commandes de diagnostic TCP/UDP

### Commandes Windows

```powershell
# Afficher toutes les connexions TCP/UDP
netstat -an

# Afficher les connexions avec les programmes
netstat -anb

# Afficher les statistiques TCP/UDP
netstat -s

# Afficher les connexions en écoute
netstat -an | findstr LISTENING

# Tester une connexion TCP (telnet)
telnet google.com 80
Test-NetConnection -ComputerName google.com -Port 443
```

### Commandes Linux

```bash
# Afficher les connexions TCP/UDP (moderne)
ss -tunap

# Afficher les connexions TCP/UDP (ancien)
netstat -tunap

# Afficher les statistiques
ss -s
netstat -s

# Tester une connexion TCP
telnet google.com 80
nc -zv google.com 443
```

### Commandes Cisco IOS

```cisco
! Afficher les connexions TCP actives
show tcp brief

! Statistiques TCP
show ip tcp statistics

! Statistiques UDP
show ip udp statistics
```

---

## 10. Points clés pour l'examen CCNA

### TCP - Points essentiels

✅ **En-tête TCP** : 20 octets minimum, champs Source Port, Destination Port, SEQ, ACK, Flags, Window Size, Checksum
✅ **Flags** : SYN (connexion), ACK (acquittement), FIN (fermeture), RST (reset), PSH (push), URG (urgent)
✅ **3-way handshake** : SYN → SYN-ACK → ACK
✅ **4-way termination** : FIN → ACK → FIN → ACK
✅ **Fenêtre glissante** : Contrôle de flux, Window Size, ajustement dynamique
✅ **Contrôle de congestion** : Slow Start (croissance exponentielle), Congestion Avoidance (croissance linéaire)
✅ **SEQ/ACK** : Numérotation des octets, réordonnancement, fiabilité
✅ **MSS** : 1460 octets typique (MTU 1500 - IP 20 - TCP 20)
✅ **Ports** : 0-1023 (well-known), 1024-49151 (registered), 49152-65535 (dynamic)

### UDP - Points essentiels

✅ **En-tête UDP** : 8 octets, champs Source Port, Destination Port, Length, Checksum
✅ **Checksum** : Optionnel IPv4, obligatoire IPv6, vérifie intégrité
✅ **Sans connexion** : Pas de handshake, pas de fiabilité, best effort
✅ **Applications** : DNS, DHCP, TFTP, NTP, SNMP, VoIP, streaming
✅ **Rapide et léger** : Overhead minimal, adapté temps réel

### Comparaison TCP vs UDP

✅ **TCP** : Fiable, orienté connexion, contrôle de flux/congestion, ordre garanti
✅ **UDP** : Non fiable, sans connexion, rapide, multicast/broadcast
✅ **Choix** : TCP pour fiabilité, UDP pour vitesse et temps réel

---

## 11. Scénarios pratiques

### Scénario 1 : Fenêtre glissante

**Contexte :**
- Récepteur annonce Window Size = 5000 octets
- MSS = 1000 octets

**Question :** Combien de segments l'émetteur peut-il envoyer sans attendre d'ACK ?

**Réponse :**
```
Window Size = 5000 octets
MSS = 1000 octets
Nombre de segments = 5000 / 1000 = 5 segments
```

L'émetteur peut envoyer **5 segments** avant d'attendre un ACK.

### Scénario 2 : 3-way handshake

**Contexte :**
- Un client veut se connecter à un serveur web (port 80)

**Question :** Décrivez les 3 étapes du handshake avec les flags et SEQ/ACK.

**Réponse :**
```
1. Client → Serveur : SYN (SEQ=X, flag SYN=1)
   "Je veux établir une connexion, mon ISN est X"

2. Serveur → Client : SYN-ACK (SEQ=Y, ACK=X+1, flags SYN=1, ACK=1)
   "OK, mon ISN est Y, j'ai bien reçu ton SYN"

3. Client → Serveur : ACK (SEQ=X+1, ACK=Y+1, flag ACK=1)
   "J'ai bien reçu ton SYN, connexion établie"
```

### Scénario 3 : Choix TCP vs UDP

**Question :** Quelle protocole choisir pour ces applications ?

| Application | Protocole | Justification |
|-------------|-----------|---------------|
| Transfert de fichier | **TCP** | Fiabilité critique, ordre important |
| VoIP | **UDP** | Temps réel, quelques pertes acceptables |
| Navigation web | **TCP** | Intégrité des pages HTML |
| Streaming vidéo en direct | **UDP** | Temps réel, vitesse prioritaire |
| Requête DNS | **UDP** | Simple requête/réponse, rapide |
| Email | **TCP** | Fiabilité critique |

### Scénario 4 : Détection de perte

**Contexte :**
- Émetteur envoie segments SEQ=1000, 2000, 3000, 4000
- Segment SEQ=2000 est perdu

**Question :** Que se passe-t-il ?

**Réponse :**
```
Segment SEQ=1000 → Récepteur envoie ACK=2000
Segment SEQ=2000 → PERDU
Segment SEQ=3000 → Récepteur envoie ACK=2000 (ACK dupliqué, attend toujours 2000)
Segment SEQ=4000 → Récepteur envoie ACK=2000 (2e ACK dupliqué)

Émetteur reçoit 3 ACK=2000 (dupliqués)
→ Fast Retransmit : retransmission de SEQ=2000 immédiatement
```

---

## 12. Résumé

### TCP (Transmission Control Protocol)

- **Orienté connexion** : 3-way handshake (SYN, SYN-ACK, ACK)
- **Fiable** : ACK, retransmission, SEQ/ACK pour ordre et fiabilité
- **Contrôle de flux** : Fenêtre glissante (Window Size), adaptation capacité récepteur
- **Contrôle de congestion** : Slow Start, Congestion Avoidance, réaction aux pertes
- **En-tête** : 20-60 octets, champs importants (ports, SEQ, ACK, flags, window, checksum)
- **Flags** : SYN, ACK, FIN, RST, PSH, URG
- **Applications** : HTTP, HTTPS, FTP, SSH, SMTP, POP, IMAP

### UDP (User Datagram Protocol)

- **Sans connexion** : Pas de handshake, envoi direct
- **Non fiable** : Pas d'ACK, pas de retransmission, best effort
- **Léger** : 8 octets d'en-tête, overhead minimal
- **Rapide** : Pas de contrôle de flux/congestion
- **Checksum** : Optionnel IPv4, obligatoire IPv6, vérifie intégrité
- **Applications** : DNS, DHCP, TFTP, NTP, SNMP, VoIP, streaming

### Choix TCP vs UDP

- **TCP** : Fiabilité, intégrité, ordre → applications critiques
- **UDP** : Vitesse, temps réel, multicast → applications rapides

---

**Fin du Module 14 - Protocoles de Transport (TCP/UDP)**
