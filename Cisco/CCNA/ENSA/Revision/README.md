# ENSA - Enterprise Networking, Security, and Automation
## Révisions Cisco CCNA - Cours 3/3

---

## 📚 Description du cours

**Enterprise Networking, Security, and Automation (ENSA)** est le troisième et dernier cours de formation Cisco NetAcad pour la certification CCNA. Ce cours couvre OSPF, la sécurité avancée, les WAN, la QoS et l'automatisation.

**Durée estimée :** ~70 heures  
**Modules :** 14 modules + examens

---

## 🎯 Objectifs d'apprentissage

Ce cours couvre :
- OSPF (Open Shortest Path First)
- Sécurité réseau avancée
- ACL (Access Control Lists)
- NAT/PAT
- Concepts WAN
- VPN et IPsec
- QoS (Quality of Service)
- Gestion réseau (SNMP, Syslog, NTP)
- Conception réseau d'entreprise
- Virtualisation et cloud
- Automatisation réseau (API, REST, Ansible)

---

## 📂 Structure des révisions

### Notes de cours
Dossier `Notes/` - Notes détaillées par module

### Fiches de révision
Dossier `Fiches/` - Fiches synthétiques par module

### QCM
Dossier `QCM/` - Questions à choix multiples par module et checkpoint

### Mock Exams
Dossier `Mock-Exams/` - Examens blancs finaux + examen blanc CCNA complet

---

## 📊 Répartition des modules

### Bloc 1 : OSPF (Modules 1-2)
- Concepts OSPF à zone unique
- Configuration OSPFv2
- **Checkpoint 1** ⬜

### Bloc 2 : Sécurité réseau (Modules 3-5)
- Concepts de sécurité
- Concepts ACL
- Configuration ACL IPv4
- **Checkpoint 2** ⬜

### Bloc 3 : WAN (Modules 6-8)
- NAT pour IPv4
- Concepts WAN
- VPN et IPsec
- **Checkpoint 3** ⬜

### Bloc 4 : Gestion et conception (Modules 9-12)
- Concepts QoS
- Gestion réseau
- Conception réseau
- Dépannage réseau
- **Checkpoint 4** ⬜

### Bloc 5 : Technologies émergentes (Modules 13-14)
- Virtualisation du réseau
- Automatisation des réseaux
- **Checkpoint 5** ⬜

---

## 🎓 Progression

| Module | Titre | Status | Notes | Fiche | QCM |
|--------|-------|--------|-------|-------|-----|
| 01 | Concepts OSPF | ⬜ | ⬜ | ⬜ | ⬜ |
| 02 | Configuration OSPFv2 | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP1** | **Checkpoint Modules 1-2** | ⬜ | - | - | ⬜ |
| 03 | Concepts de sécurité | ⬜ | ⬜ | ⬜ | ⬜ |
| 04 | Concepts ACL | ⬜ | ⬜ | ⬜ | ⬜ |
| 05 | Configuration ACL IPv4 | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP2** | **Checkpoint Modules 3-5** | ⬜ | - | - | ⬜ |
| 06 | NAT pour IPv4 | ⬜ | ⬜ | ⬜ | ⬜ |
| 07 | Concepts WAN | ⬜ | ⬜ | ⬜ | ⬜ |
| 08 | VPN et IPsec | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP3** | **Checkpoint Modules 6-8** | ⬜ | - | - | ⬜ |
| 09 | Concepts QoS | ⬜ | ⬜ | ⬜ | ⬜ |
| 10 | Gestion réseau | ⬜ | ⬜ | ⬜ | ⬜ |
| 11 | Conception réseau | ⬜ | ⬜ | ⬜ | ⬜ |
| 12 | Dépannage réseau | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP4** | **Checkpoint Modules 9-12** | ⬜ | - | - | ⬜ |
| 13 | Virtualisation réseau | ⬜ | ⬜ | ⬜ | ⬜ |
| 14 | Automatisation réseaux | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP5** | **Checkpoint Modules 13-14** | ⬜ | - | - | ⬜ |
| **Final** | **Examen blanc CCNA complet** | ⬜ | - | - | ⬜ |

---

## 📖 Ressources complémentaires

### Cours NetAcad
- Plateforme NetAcad : Cours ENSA complet
- Labs Packet Tracer avancés

### Jeremy's IT Lab
- Modules correspondants du cours CCNA

### Livres
- CCNA 200-301 Official Cert Guide (Volume 2)
- Enterprise Networking, Security, and Automation Companion Guide

---

## ⚡ Commandes IOS essentielles

### OSPF
```cisco
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 passive-interface gi0/0
interface gi0/1
 ip ospf 1 area 0
```

### ACL standard
```cisco
access-list 10 permit 192.168.1.0 0.0.0.255
interface gi0/0
 ip access-group 10 out
```

### ACL étendue
```cisco
ip access-list extended BLOCK_TELNET
 deny tcp any any eq 23
 permit ip any any
interface gi0/0
 ip access-group BLOCK_TELNET in
```

### NAT/PAT
```cisco
ip nat inside source list 1 interface gi0/1 overload
interface gi0/0
 ip nat inside
interface gi0/1
 ip nat outside
```

---

**Dernière mise à jour :** 23 février 2026  
**Status du cours :** À commencer ⬜
