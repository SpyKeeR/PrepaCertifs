# QCM Module 13 : Multicast

## Questions 1-10

### Q1 : Quelle est la plage d'adresses IPv4 réservée au multicast ?
**A)** 192.168.0.0/16  
**B)** 224.0.0.0/4  
**C)** 240.0.0.0/4  
**D)** 255.255.255.255/32  

**Réponse : B** - **Classe D : 224.0.0.0 à 239.255.255.255** est réservée au multicast.

---

### Q2 : Quel est le préfixe MAC multicast Layer 2 ?
**A)** `FF:FF:FF:FF:FF:FF`  
**B)** `01:00:5E:xx:xx:xx`  
**C)** `00:00:5E:00:53:00`  
**D)** `01:00:00:xx:xx:xx`  

**Réponse : B** - Le préfixe MAC multicast est **`01:00:5E`** suivi des 23 bits bas de l'IP multicast.

---

### Q3 : Quel protocole gère l'adhésion des hôtes aux groupes multicast ?
**A)** DHCP  
**B)** ARP  
**C)** IGMP (Internet Group Management Protocol)  
**D)** DNS  

**Réponse : C** - **IGMP** est le protocole permettant hôtes de rejoindre/quitter les groupes multicast.

---

### Q4 : Quelle est la version IGMP recommandée pour les déploiements modernes ?
**A)** IGMPv1  
**B)** IGMPv2  
**C)** IGMPv3  
**D)** IGMPv4  

**Réponse : C** - **IGMPv3** est la version moderne avec support Source-Specific Multicast (SSM).

---

### Q5 : Quel est le rôle principal de l'IGMP Snooping sur un switch ?
**A)** Router le trafic multicast en Layer 3  
**B)** Écouter les messages IGMP et limiter le flood multicast  
**C)** Convertir multicast en unicast  
**D)** Réduire l'AS_Path en multicast  

**Réponse : B** - **IGMP Snooping** écoute les messages IGMP (Layer 2) pour limiter le flood multicast aux ports intéressés seulement.

---

### Q6 : Quel est le délai par défaut pour l'intervalle de query IGMP ?
**A)** 30 secondes  
**B)** 60 secondes  
**C)** 125 secondes  
**D)** 260 secondes  

**Réponse : C** - L'intervalle de query IGMP par défaut est **125 secondes**.

---

### Q7 : Quel timeout IGMP est utilisé avant de supprimer un groupe sans réponse ?
**A)** 60 secondes  
**B)** 125 secondes  
**C)** 130 secondes  
**D)** 260 secondes  

**Réponse : D** - Le **Group Membership Interval par défaut est 260 secondes** (3.5 × Query Interval).

---

### Q8 : Quel mode PIM utilise l'approche Flood & Prune ?
**A)** PIM Dense Mode (DM)  
**B)** PIM Sparse Mode (SM)  
**C)** PIM Hybrid Mode  
**D)** PIM Bidirectional  

**Réponse : A** - **PIM Dense Mode** utilise la stratégie **Flood & Prune** : inonde partout, puis prune les branches non intéressées.

---

### Q9 : Quel mode PIM est recommandé pour les réseaux de grande taille ?
**A)** PIM Dense Mode  
**B)** PIM Sparse Mode  
**C)** PIM Source Specific Mode  
**D)** PIM Reverse Route Forwarding  

**Réponse : B** - **PIM Sparse Mode** est recommandé pour les grands réseaux avec scalabilité meilleure.

---

### Q10 : Quel est le rôle principal du Rendezvous Point (RP) en PIM Sparse Mode ?
**A)** Router tous les paquets multicast  
**B)** Élire le routeur avec le meilleur BGP path  
**C)** Négocie entre sources et receveurs multicast  
**D)** Compter les sauts multicast  

**Réponse : C** - Le **RP** négocie et pivot les flux entre sources multicast et récepteurs.

---

## Questions 11-20

### Q11 : Comment est calculée l'adresse MAC multicast pour 224.10.20.30 ?
**A)** 01:00:5E:10:14:1E  
**B)** 01:00:5E:0A:14:1E  
**C)** 01:00:5E:E0:14:1E  
**D)** 01:00:5E:FF:14:1E  

**Réponse : B** - 224.10.20.30 → bits bas {0A:14:1E} → MAC **01:00:5E:0A:14:1E**

---

### Q12 : Quelle est la plage de priorité d'un RP en PIM ?
**A)** 0-16  
**B)** 0-128  
**C)** 0-255  
**D)** Sans limite  

**Réponse : C** - La plage de priorité RP est **0-255**, plus bas = meilleur (défaut 0).

---

### Q13 : Quel message utilise un hôte pour quitter un groupe multicast en IGMPv2 ?
**A)** MEMBERSHIP REPORT  
**B)** MEMBERSHIP QUERY  
**C)** LEAVE MESSAGE  
**D)** ADDRESS CHANGE  

**Réponse : C** - **LEAVE MESSAGE** est utilisé en IGMPv2 pour quitter explicitement un groupe.

---

### Q14 : Quel arbre multicast offre la meilleure latence source-récepteur ?
**A)** RPT (RP Tree)  
**B)** SPT (Shortest Path Tree)  
**C)** CST (Core Shortest Tree)  
**D)** IDF (Intermediate Distribution Frame)  

**Réponse : B** - **SPT (Shortest Path Tree)** offre le meilleur chemin source-récepteur et la latence minimale.

---

### Q15 : En PIM Sparse Mode, quel est le premier arbre utilisé lors du join multicast ?
**A)** SPT (RP direct)  
**B)** RPT via RP  
**C)** Hybrid Tree  
**D)** Source-specific Tree  

**Réponse : B** - En PIM SM, le récepteur rejoint d'abord le **RPT via RP**, puis peut switcher vers SPT.

---

### Q16 : Quel est le concept d'IPv6 multicast correspondant à la plage "239.0.0.0/8" en IPv4 ?
**A)** ff00::/8  
**B)** fe80::/10  
**C)** ff3x::/16 (où x = scope)  
**D)** Aucun groupe réservé en IPv6  

**Réponse : A** - **IPv6 multicast plage : ff00::/8**, équivalent à la plage IPv4.

---

### Q17 : Quel est le niveau de scope par défaut du RP discovery en PIM ?
**A)** Lien-local seulement  
**B)** Subnet seulement  
**C)** AS-wide via RP-announce  
**D)** Globe entière  

**Réponse : C** - Par défaut, RP discovery est **AS-wide** via RP-announce messages.

---

### Q18 : Quel IGMP message est envoyé périodiquement par le routeur multicast (querier) ?
**A)** MEMBERSHIP REPORT  
**B)** LEAVE MESSAGE  
**C)** MEMBERSHIP QUERY  
**D)** REGISTER MESSAGE  

**Réponse : C** - Le routeur multicast envoie périodiquement **MEMBERSHIP QUERY** pour découvrir les groupes actifs.

---

### Q19 : Quel est l'avantage principal de GLOP (RFC 3180) pour adressage multicast ?
**A)** Meilleure performance réseau  
**B)** Unicité globale basée sur ASN sans coordination centrale  
**C)** Réduction MTU  
**D)** Support IPv6 natif  

**Réponse : B** - **GLOP (233.ASN.0.0/16)** fournit **unicité garantie globale** sans coordination centrale.

---

### Q20 : Quel groupe d'adresses multicast est réservé à usage administratif local ?
**A)** 224.0.1.1 - 224.0.1.255  
**B)** 224.1.0.0 - 224.251.255.255  
**C)** 239.0.0.0/8  
**D)** 224.0.0.0/24  

**Réponse : C** - **Administratively Scoped : 239.0.0.0/8** est réservée à usage local avec boundaries.

---

## Questions 21-25

### Q21 : Quel attribut PIM détermine ququel arbre (RPT ou SPT) un récepteur rejoint ?
**A)** PIM mode (DM vs SM)  
**B)** IGMP version  
**C)** Préférence administrateur  
**D)** Sault source-RP (tous deux initialement)  

**Réponse : D** - Initialement, récepteur rejoint le **RPT**, puis peut switcher **SPT** bas sur source proximity/latency.

---

### Q22 : Quel commande Cisco active PIM Sparse Mode sur une interface ?
**A)** `ip multicast-routing`  
**B)** `ip pim sparse-mode`  
**C)** `ip multicast-mode sparse`  
**D)** `interface pim sparse`  

**Réponse : B** - **`ip pim sparse-mode`** active PIM SM sur l'interface.

---

### Q23 : Quel est le timeout de réponse maximum (Max Response Time) IGMP par défaut ?
**A)** 5 secondes  
**B)** 10 secondes  
**C)** 30 secondes  
**D)** 60 secondes  

**Réponse : B** - Le **Max Response Time par défaut est 10 secondes**.

---

### Q24 : Quel message PIM est utilisé par une source pour contacter le RP en Sparse Mode ?
**A)** JOIN/PRUNE  
**B)** REGISTER  
**C)** HELLO  
**D)** ASSERT  

**Réponse : B** - **REGISTER message** envoie par source pour annoncer au RP son trafic multicast.

---

### Q25 : Quel paramètre IGMP définit le nombre minimum de reports avant de faire un groupe multicast ?
**A)** Last Member Query Type  
**B)** Membership Threshold  
**C)** Group Creation Delay  
**D)** IGMP ne nécessite pas de minimum (un seul report suffit)  

**Réponse : D** - **Un seul IGMP MEMBERSHIP REPORT suffit** pour activer un groupe multicast.

