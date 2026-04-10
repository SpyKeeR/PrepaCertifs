# QCM Module 10 : OSPFv3

## Questions

### Question 1
**Enoncé** : Quel est le format du Router ID dans OSPFv3 ?

A) IPv6 128-bits  
B) IPv4 32-bits  
C) MAC address 48-bits  
D) Anycast IPv6

**Réponse** : B) IPv4 32-bits

**Explication** : Router ID OSPFv3 est **format IPv4 (32-bits)** même pour routage IPv6. Ceci assure compatibilité avec OSPFv2 et identifiants RID uniques.

---

### Question 2
**Enoncé** : Laquelle de ces adresses IPv6 est OBLIGATOIRE pour adjacence OSPFv3 ?

A) Global Unicast Address (GUA)  
B) Link-Local Address (LLA)  
C) Unique-Local Address (ULA)  
D) Site-Local Address (SLA)

**Réponse** : B) Link-Local Address (LLA)

**Explication** : Link-Local (fe80::/10) est **OBLIGATOIRE** pour adjacence OSPFv3. Tous les paquets OSPF (Hello, DD, LSU, etc.) utilisent LLA comme source. Sans LLA, voisinage ne se forme.

---

### Question 3
**Enoncé** : Quelle adresse est utilisée comme next-hop dans les routes OSPFv3 ?

A) Global Unicast Address (GUA) du voisin  
B) Link-Local Address (LLA) du voisin  
C) Loopback IPv6 du voisin  
D) Anycast address du voisin

**Réponse** : B) Link-Local Address (LLA) du voisin

**Explication** : Routes OSPFv3 pointent vers **LLA du voisin** (pas GUA). Ceci est efficient pour lien-local hops et minimize routing entries (toujours via LLA).

---

### Question 4
**Enoncé** : Quelle commande active OSPFv3 sur une interface pour Area 0 ?

A) `ip ospf 100 area 0`  
B) `ipv6 ospf 100 area 0`  
C) `router ospf 100` network statement  
D) `ospfv3 100`

**Réponse** : B) `ipv6 ospf 100 area 0`

**Explication** : Configuration OSPFv3 utilise `ipv6 ospf [number] area [id]` par interface (pas network statement global par défaut).

---

### Question 5
**Enoncé** : Quel est le multicast address IPv6 utilisé pour flooder Hello OSPF ?

A) FF02::1 (tous nœuds)  
B) FF02::5 (OSPFv3)  
C) FF02::6 (OSPFv3 DR/BDR)  
D) FF05::5 (site-scoped)

**Réponse** : B) FF02::5 (OSPFv3)

**Explication** : OSPFv3 utilise FF02::5 pour Hello floodings (équivalent 224.0.0.5 en OSPFv2). FF02::6 pour DR/BDR communication.

---

### Question 6
**Enoncé** : Quel LSA Type est NOUVEAU en OSPFv3 (n'existe pas en OSPFv2) ?

A) Type 3 (Network Summary)  
B) Type 5 (AS External)  
C) Type 8 (Link Prefix)  
D) Type 7 (NSSA)

**Réponse** : C) Type 8 (Link Prefix)

**Explication** : Type 8 (Link Prefix LSA) est **nouveau en OSPFv3**. Scope = single link (vs AS-wide). Utilisé pour annoncer IPv6 prefixes efficiently.

---

### Question 7
**Enoncé** : Deux interfaces : GUA 2001:db8:1::1/64 et LLA fe80::1. OSPFv3 utilisera quelle source pour Hello ?

A) GUA 2001:db8:1::1  
B) LLA fe80::1  
C) Loopback IPv6  
D) Combinaison des deux

**Réponse** : B) LLA fe80::1

**Explication** : OSPFv3 toujours utilise **LLA comme source** pour tous paquets OSPF (Hello, DD, LSU, etc.). GUA utilisée pour routage vers destinations distantes, pas pour OSPF protocole himself.

---

### Question 8
**Enoncé** : Configuration multicast hello adresse en OSPFv3 versus OSPFv2 ?

A) Identique (224.0.0.5 vs FF02::5 format)  
B) Différente (FF02::5 vs 224.0.0.5)  
C) OSPFv3 unicast, OSPFv2 multicast  
D) Identique (défaut non-configurable)

**Réponse** : B) Différente (FF02::5 vs 224.0.0.5)

**Explication** :
- **OSPFv2** : 224.0.0.5 (IPv4 multicast)
- **OSPFv3** : FF02::5 (IPv6 multicast)
Les addresses sont différentes format (IPv6 vs IPv4) mais rôle identique.

---

### Question 9
**Enoncé** : Quelle méthode authentication OSPFv3 utilise par défaut ?

A) MD5 (comme OSPFv2)  
B) Cleartext  
C) IPsec  
D) None (optionnel)

**Réponse** : C) IPsec

**Explication** : OSPFv3 utilise **IPsec standard** pour authentication (vs MD5 propriétaire OSPFv2). Donner meilleure security et compatibilité.

---

### Question 10
**Enoncé** : Address Family en OSPFv3 permet support simultané de :

A) Seulement IPv6 (OSPFv3 = IPv6)  
B) IPv4 et IPv6 avec topologies séparées  
C) IPv4 et IPv6 avec LSDB partagée  
D) Seulement statique IPs

**Réponse** : B) IPv4 et IPv6 avec topologies séparées

**Explication** : **Address Families** en OSPFv3 permettent :
- IPv4 AF : Topology/LSDB/SPF séparée
- IPv6 AF : Topology/LSDB/SPF séparée
- Chaque AF converge indépendamment

---

### Question 11
**Enoncé** : Configuration IPv4 dans OSPFv3 utilise quel format d'area ID ?

A) IPv4 dotted-decimal (ex: 192.168.1.0)  
B) Numéric ID (ex: area 1)  
C) IPv6 address (ex: 2001:db8::)  
D) Format est identique OSPFv2

**Réponse** : D) Format est identique OSPFv2

**Explication** : Area IDs en OSPFv3 sont **numéric** (0, 1, 2, etc.) même en IPv4 AF. Identique OSPFv2 format. Ex: `area 0 range 192.168.0.0 255.255.0.0`.

---

### Question 12
**Enoncé** : Quelle est la sélection automatique Router ID en OSPFv3 si pas configuré ?

A) Plus haut IPv6 GUA  
B) Plus haut IPv4 address (loopback d'abord)  
C) MAC address (Cisco)  
D) Random (unique garantie)

**Réponse** : B) Plus haut IPv4 address (loopback d'abord)

**Explication** : Router ID sélection OSPFv3 (identique OSPFv2) :
1. Configured `router-id`
2. Highest IPv4 loopback
3. Highest physical IPv4

RID est toujours IPv4 format, pas IPv6.

---

### Question 13
**Enoncé** : Quel Hello Interval par défaut en OSPFv3 sur Gigabit Ethernet ?

A) 5 secondes  
B) 10 secondes  
C) 30 secondes  
D) 60 secondes

**Réponse** : B) 10 secondes

**Explication** : Hello default en OSPFv3 = **10 secondes** (même OSPFv2 Ethernet). Dead Interval = 40 sec (4× Hello).

---

### Question 14
**Enoncé** : Stub Area dans OSPFv3 rejette quels LSA types ?

A) Type 4, 5  
B) Type 3, 4, 5  
C) Type 1, 2  
D) Identique OSPFv2 (Type 4, 5)

**Réponse** : D) Identique OSPFv2 (Type 4, 5)

**Explication** : Stub Area en OSPFv3 a **même comportement OSPFv2** :
- Rejette Type 4, 5 LSAs
- Accepte Type 1, 2, 3
- Reçoit défaut 0::/0

---

### Question 15
**Enoncé** : Comment configurer Cost/Métrique sur interface OSPFv3 ?

A) `ipv6 ospf metric 50`  
B) `ipv6 ospf cost 50`  
C) `ip ospf cost 50`  
D) `ospf metric 50`

**Réponse** : B) `ipv6 ospf cost 50`

**Explication** : Configuration coût interface OSPFv3 utilise `ipv6 ospf cost [value]` (préfixe `ipv6` vs `ip` pour OSPFv2).

---

### Question 16 (Avancée)
**Enoncé** : Deux OSPFv3 voisins : R1 (IPv6 2001:db8:1::1) et R2 (LLA fe80::2). Comment R1 atteint R2 pour next-hop ?

A) Via GUA 2001:db8:1::1  
B) Via LLA fe80::2  
C) Via défaut fe80::/10  
D) Pas de routage (lien-direct)

**Réponse** : B) Via LLA fe80::2

**Explication** : Toutes routes installées dans RIB OSPFv3 utilisent **LLA comme next-hop**. R1 atteint R2 traffic via fe80::2 (link-local R2), pas GUA.

---

### Question 17 (Avancée)
**Enoncé** : OSPFv3 Address Family IPv4 configuration. Quel est l'impact sur OSPFv2 process existant ?

A) Aucun (indépendant)  
B) Remplace OSPFv2 (incompatible)  
C) Fusionne LSDB  
D) Crée conflit processus

**Réponse** : A) Aucun (indépendant)

**Explication** : OSPFv3 (même avec AF IPv4) est **processus séparé** d'OSPFv2. Peuvent coexister :
- OSPFv2 process 100 (IPv4)
- OSPFv3 process 200 (IPv4+IPv6 AF)
Complètement indépendant, LSDB séparé, RIB merge possibility.

---

### Question 18 (Avancée)
**Enoncé** : NSSA en OSPFv3 genère Type 7 LSAs. Via ABR, Type 7 est traduit vers :

A) Type 5 (AS-wide)  
B) Type 3 (Inter-area)  
C) Type 8 (Link Prefix)  
D) Aucun (reste Type 7)

**Réponse** : A) Type 5 (AS-wide)

**Explication** : NSSA Translation (identique OSPFv2) :
- Type 7 généré dans NSSA
- ABR traduit Type 7 → **Type 5** flooded vers autres areas
- Résultat : Routes NSSA connues AS-wide

---

### Question 19 (Avancée)
**Enoncé** : Interface OSPFv3 sans `ipv6 address fe80::...` configurée. Quel adresse LLA est utilisée ?

A) Pas de LLA (erreur adjacency)  
B) Générée automatiquement (EUI-64)  
C) Défaut fe80::1  
D) Aucune ne peut être générée

**Réponse** : B) Générée automatiquement (EUI-64)

**Explication** : Si LLA pas configurée, **Cisco génère automatiquement** LLA via EUI-64 (desde MAC address). Pas besoin configuration explicite, mais recommandé pour clarté.

---

### Question 20 (Avancée)
**Enoncé** : Adjacency OSPFv3 stuck dans ExStart state. Cause probable ?

A) RID identiques  
B) Timers Hello/Dead mismatch  
C) Master/Slave election problème  
D) LLA non-directional

**Réponse** : C) Master/Slave election problème

**Explication** : ExStart state = Master/Slave élection (RID supérieur = Master). Si stuck ici :
- Possible asymétrie RID (conflict)
- Database exchange failure
- Network issue entre voisins

---

### Question 21 (Avancée)
**Enoncé** : `router ospfv3 100` configuration pour IPv4 via Address Family. Quelle est priorité d'installation RIB vs OSPFv2 process ?

A) OSPFv3 AF IPv4 (plus haut priorité)  
B) OSPFv2 (plus haut priorité)  
C) Basé sur AD (90 vs 110 défaults)  
D) Alternance (change)

**Réponse** : C) Basé sur AD (90 vs 110 défaults)

**Explication** : Si OSPFv2 et OSPFv3 AF IPv4 sont actifs avec **même destination** :
- OSPFv2 = AD 110 (défaut)
- OSPFv3 = AD 110 (défaut, si OSPF)
- Equal AD → première apprise gagne (plus haut RID ou timing)

---

### Question 22 (Avancée)
**Enoncé** : Type 8 LSA (Link Prefix) en OSPFv3. Quel est l'avantage vs Type 1/2 ?

A) Scope plus grand (AS-wide)  
B) Scope plus petit (single link) = moins flooding  
C) Métrique meilleur  
D) Support multicast

**Réponse** : B) Scope plus petit (single link) = moins flooding

**Explication** : Type 8 (Link Prefix) scope = **single link** (vs Type 1 = area, Type 5 = AS). Avantages :
- Réduit flooding pour prefix changes
- Efficient IPv6 manage per-link
- Less disruption réseau

---

### Question 23 (Avancée)
**Enoncé** : OSPFv3 IPsec authentication configuration. Quel paramètre détermine la clé chiffrée ?

A) SPI (Security Parameter Index) seulement  
B) SPI + algorithm + clé  
C) Algorithm seulement  
D) Clé seulement

**Réponse** : B) SPI + algorithm + clé

**Explication** : Configuration IPsec OSPFv3 :
```
ip ospf authentication ipsec spi <SPI> <algorithm> <key>
```
- **SPI** : Index unique (ex: 256)
- **Algorithm** : MD5, SHA, etc.
- **Key** : Clé chiffrement hex

Tous trois nécessaires.

---

### Question 24 (Avancée)
**Enoncé** : OSPFv3 interface sans Global Unicast Address (GUA), seulement LLA fe80::1. Adjacency ?

A) Adjacency établie (LLA suffisant)  
B) Adjacency failure (GUA obligatoire)  
C) Adjacency établie mais routes bizarres  
D) Dépend type interface

**Réponse** : A) Adjacency établie (LLA suffisant)

**Explication** : **LLA SEUL suffit** pour adjacency OSPFv3. GUA est pour **routage vers destinations** externes. Avec LLA seulement :
- Adjacency OK
- Voisins appris
- Mais routes nulles (pas de GUA pour prefix)

---

### Question 25 (Avancée)
**Enoncé** : OSPFv3 process 100 avec AF IPv4 et AF IPv6. Deux voisins établissent adjacency. Combien d'adjacencies complètes ?

A) 1 (partagée)  
B) 2 (une par AF)  
C) 0 (pas possible)  
D) Dépend BW interface

**Réponse** : A) 1 (partagée)

**Explication** : **Une adjacency per voisin**, peu importe AF. Mais :
- LSDB séparé (IPv4 vs IPv6)
- SPF calcul séparé
- Topologie indépendante

Adjacency = point-to-point link, partagée par AFs.

---

## Résumé des Réponses

| Q | Rép | Q | Rép |
|---|-----|---|-----|
| 1 | B | 13 | B |
| 2 | B | 14 | D |
| 3 | B | 15 | B |
| 4 | B | 16 | B |
| 5 | B | 17 | A |
| 6 | C | 18 | A |
| 7 | B | 19 | B |
| 8 | B | 20 | C |
| 9 | C | 21 | C |
| 10 | B | 22 | B |
| 11 | D | 23 | B |
| 12 | B | 24 | A |

---
**Durée estimée** : 60-75 minutes  
**Difficulté** : Basique (Q1-12), Intermédiaire (Q13-18), Avancée (Q19-25)
