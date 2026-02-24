# SRWE - Switching, Routing, and Wireless Essentials
## Révisions Cisco CCNA - Cours 2/3

---

## 📚 Description du cours

**Switching, Routing, and Wireless Essentials (SRWE)** est le deuxième des trois cours de formation Cisco NetAcad pour la certification CCNA. Ce cours approfondit la commutation, le routage et les réseaux sans fil.

**Durée estimée :** ~70 heures  
**Modules :** 16 modules + examens

---

## 🎯 Objectifs d'apprentissage

Ce cours couvre :
- Configuration avancée des commutateurs
- VLANs et routage inter-VLAN
- Spanning Tree Protocol (STP)
- EtherChannel
- DHCP (v4 et v6)
- FHRP (First Hop Redundancy Protocols)
- Sécurité de couche 2
- Réseaux sans fil (WLAN)
- Concepts de routage avancés
- Routage statique

---

## 📂 Structure des révisions

### Notes de cours
Dossier `Notes/` - Notes détaillées par module

### Fiches de révision
Dossier `Fiches/` - Fiches synthétiques par module

### QCM
Dossier `QCM/` - Questions à choix multiples par module et checkpoint

### Mock Exams
Dossier `Mock-Exams/` - Examens blancs finaux

---

## 📊 Répartition des modules

### Bloc 1 : Configuration de base (Modules 1-4)
- Configuration des périphériques
- Concepts de commutation
- VLANs
- Routage inter-VLAN
- **Checkpoint 1** ⬜

### Bloc 2 : Réseaux redondants (Modules 5-6)
- Spanning Tree Protocol (STP)
- EtherChannel
- **Checkpoint 2** ⬜

### Bloc 3 : Réseaux disponibles (Modules 7-9)
- DHCPv4
- SLAAC et DHCPv6
- FHRP
- **Checkpoint 3** ⬜

### Bloc 4 : Sécurité L2 et WLAN (Modules 10-13)
- Sécurité du réseau local
- Configuration de la sécurité
- Concepts WLAN
- Configuration WLAN
- **Checkpoint 4** ⬜

### Bloc 5 : Routage (Modules 14-16)
- Concepts de routage
- Routage statique IP
- Dépannage des routes statiques
- **Checkpoint 5** ⬜

---

## 🎓 Progression

| Module | Titre | Status | Notes | Fiche | QCM |
|--------|-------|--------|-------|-------|-----|
| 01 | Configuration de base | ⬜ | ⬜ | ⬜ | ⬜ |
| 02 | Concepts de commutation | ⬜ | ⬜ | ⬜ | ⬜ |
| 03 | VLANs | ⬜ | ⬜ | ⬜ | ⬜ |
| 04 | Routage Inter-VLAN | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP1** | **Checkpoint Modules 1-4** | ⬜ | - | - | ⬜ |
| 05 | Concepts du STP | ⬜ | ⬜ | ⬜ | ⬜ |
| 06 | EtherChannel | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP2** | **Checkpoint Modules 5-6** | ⬜ | - | - | ⬜ |
| 07 | DHCPv4 | ⬜ | ⬜ | ⬜ | ⬜ |
| 08 | SLAAC et DHCPv6 | ⬜ | ⬜ | ⬜ | ⬜ |
| 09 | Concepts du FHRP | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP3** | **Checkpoint Modules 7-9** | ⬜ | - | - | ⬜ |
| 10 | Sécurité réseau local | ⬜ | ⬜ | ⬜ | ⬜ |
| 11 | Configuration sécurité | ⬜ | ⬜ | ⬜ | ⬜ |
| 12 | Concepts WLAN | ⬜ | ⬜ | ⬜ | ⬜ |
| 13 | Configuration WLAN | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP4** | **Checkpoint Modules 10-13** | ⬜ | - | - | ⬜ |
| 14 | Concepts de routage | ⬜ | ⬜ | ⬜ | ⬜ |
| 15 | Routage statique IP | ⬜ | ⬜ | ⬜ | ⬜ |
| 16 | Dépannage routes | ⬜ | ⬜ | ⬜ | ⬜ |
| **CP5** | **Checkpoint Modules 14-16** | ⬜ | - | - | ⬜ |
| **Final** | **Examen blanc final** | ⬜ | - | - | ⬜ |

---

## 📖 Ressources complémentaires

### Cours NetAcad
- Plateforme NetAcad : Cours SRWE complet
- Labs Packet Tracer avancés

### Jeremy's IT Lab
- Modules correspondants du cours CCNA

### Livres
- CCNA 200-301 Official Cert Guide (Volume 1)
- Switching, Routing, and Wireless Essentials Companion Guide

---

## ⚡ Commandes IOS essentielles

### VLANs
```cisco
vlan 10
 name SALES
interface range fa0/1-10
 switchport mode access
 switchport access vlan 10
```

### Trunks
```cisco
interface gi0/1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30
```

### STP
```cisco
spanning-tree mode rapid-pvst
spanning-tree vlan 1 root primary
spanning-tree portfast
spanning-tree bpduguard enable
```

---

**Dernière mise à jour :** 23 février 2026  
**Status du cours :** À commencer ⬜
