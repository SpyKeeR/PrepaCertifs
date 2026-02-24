# Fiche Module 01 : Les réseaux aujourd'hui
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Impact des réseaux
- Communication (email, visio), Collaboration (cloud, partage)
- Mobilité (accès n'importe où), Commerce électronique
- Éducation en ligne, Divertissement (streaming, jeux)

### Types de réseaux
- **Réseaux personnels** : Smartphones, tablettes, PC
- **Réseaux domestiques** : Wi-Fi, IoT
- **Réseaux d'entreprise** : Ressources professionnelles
- **Internet** : Réseau global interconnectant tous les réseaux

---

## 📊 Composants réseau

| Composant | Type | Rôle | Exemples |
|-----------|------|------|----------|
| **Périphériques finaux** | Hôtes | Génèrent/consomment du trafic | PC, serveurs, smartphones, imprimantes IP, IoT |
| **Périphériques intermédiaires** | Équipements réseau | Acheminent les données | Switches, routeurs, firewalls, WAP, modems |
| **Supports réseau** | Médias | Transportent les données | Cuivre (UTP), fibre optique, sans fil (Wi-Fi) |

### Caractéristiques des supports

**Câbles cuivre (UTP/STP)**
- Distance max : ~100 m
- Standards : Cat 5e (1 Gbps), Cat 6 (10 Gbps)

**Fibre optique**
- Longue distance (plusieurs km)
- Grande bande passante, immunité aux interférences
- Types : Monomode (longue distance), Multimode (courte distance)

**Sans fil (Wi-Fi)**
- 802.11 (Wi-Fi), Bluetooth
- Sensible aux interférences et obstacles

---

## 📊 Types de réseaux selon la taille

| Type | Nom | Portée | Caractéristiques | Exemples |
|------|-----|--------|------------------|----------|
| **LAN** | Local Area Network | Zone limitée (bureau, bâtiment, campus) | Haute vitesse (1-100 Gbps), propriété privée | Réseau d'entreprise, réseau domestique |
| **WAN** | Wide Area Network | Grande zone géographique (pays, continent) | Vitesse variable, utilise des ISP | Internet, réseau inter-sites |
| **MAN** | Metropolitan Area Network | Ville ou région | Entre LAN et WAN | Réseau métropolitain |

**Autres types :**
- **PAN** (Personal Area Network) : Bluetooth, portée personnelle
- **WLAN** (Wireless LAN) : LAN sans fil (Wi-Fi)

---

## 📊 Topologies réseau

| Topologie | Description | Avantages | Inconvénients |
|-----------|-------------|-----------|---------------|
| **Étoile** | Tous les périphériques connectés à un switch central | Facile à dépanner, panne isolée | Point de défaillance unique (le switch) |
| **Étoile étendue** | Plusieurs étoiles interconnectées | Évolutif, utilisé en entreprise | Complexité accrue |
| **Maillée (Mesh)** | Chaque périphérique connecté aux autres (complet ou partiel) | Haute redondance | Coûteux, complexe |
| **Bus** | Tous sur un câble unique | Simple | Obsolète, point de défaillance unique |

---

## 💡 À retenir absolument

✅ **Périphériques finaux** = Hôtes (source/destination du trafic)  
✅ **Périphériques intermédiaires** = Routent et gèrent le trafic  
✅ **LAN** = Réseau local, haute vitesse, propriété privée  
✅ **WAN** = Réseau étendu, grande distance, utilise des ISP  
✅ **Internet** = Le plus grand WAN du monde  
✅ **Topologie en étoile** = Topologie LAN moderne la plus courante  
✅ **Distance maximale UTP** : 100 mètres  
✅ **Fibre optique** = Longue distance, immunité aux interférences  

---

**Diagrammes réseau :**
- **Physique** : Emplacements réels, salles, bâtiments
- **Logique** : Connexions logiques, adresses IP, protocoles
