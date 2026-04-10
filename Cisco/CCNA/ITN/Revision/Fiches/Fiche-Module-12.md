# Fiche de révision CCNA ITN - Module 12
## Adressage IPv6

---

## 🎯 Concepts clés

### Structure IPv6
- **128 bits** (vs 32 bits IPv4)
- **8 groupes** de 16 bits (4 chiffres hexadécimaux)
- Séparés par `:`
- **Exemple** : `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Compression des adresses ⚠️ IMPORTANT
**Règle 1** : Supprimer les zéros de tête
```
2001:0db8:0000:0042 → 2001:db8:0:42
```

**Règle 2** : Remplacer une séquence de zéros par `::`
```
2001:0db8:0000:0000:0000:0000:0000:0001 → 2001:db8::1
```
⚠️ **Une seule fois** par adresse (sinon ambiguïté)

### Types d'adresses
- **Unicast** : un-à-un
- **Multicast** : un-à-plusieurs (FF00::/8)
- **Anycast** : un-au-plus-proche
- ❌ **Pas de broadcast** en IPv6

---

## 📋 Types d'adresses unicast

| Type | Plage | Routabilité | Utilisation |
|------|-------|-------------|-------------|
| **GUA** | 2000::/3 | ✅ Routable Internet | Adresses publiques globales |
| **LLA** | FE80::/10 | ❌ Non routable | Communication lien local, passerelle |
| **ULA** | FC00::/7 (FD00::/8) | ❌ Non routable Internet | Privé interne (= RFC 1918) |
| **Loopback** | ::1/128 | Local | Test local (= 127.0.0.1) |
| **Unspecified** | ::/128 | N/A | Absence d'adresse |

---

## 🎯 GUA - Global Unicast Address

### Structure (notation /48 → /64)
```
|    48 bits     | 16 bits  |      64 bits       |
+----------------+----------+--------------------+
| Global Prefix  | Subnet   |   Interface ID     |
|  (ISP/RIR)     | ID       | (hôte)             |
+----------------+----------+--------------------+
```

### Allocation typique
```
ISP alloue → Organisation : 2001:db8:acad::/48

Sous-réseaux /64 :
  2001:db8:acad:0001::/64    ← VLAN 1
  2001:db8:acad:0002::/64    ← VLAN 2
  2001:db8:acad:0003::/64    ← VLAN 3
  ...
  2001:db8:acad:ffff::/64    ← VLAN 65535
```

**Capacité** : /48 → 65 536 sous-réseaux /64

---

## 🎯 LLA - Link-Local Address ⚠️ ESSENTIEL

### Caractéristiques
- **Plage** : `FE80::/10` (en pratique toutes commencent par `FE80::`)
- **Obligatoire** sur chaque interface IPv6
- **Non routable** (ne traverse jamais un routeur)
- **Auto-générée** (EUI-64) ou configurée manuellement

### Génération EUI-64
```
MAC : 00:1A:2B:3C:4D:5E

1. Diviser : 00:1A:2B | 3C:4D:5E
2. Insérer FFFE : 00:1A:2B:FF:FE:3C:4D:5E
3. Inverser 7e bit :
   00 (hex) = 0000 0000 (bin) → 0000 0010 (bin) = 02 (hex)
4. Interface ID : 021A:2BFF:FE3C:4D5E

Link-Local : FE80::021A:2BFF:FE3C:4D5E
```

### Utilisation de la LLA ⚠️ CRUCIAL
✅ **Passerelle par défaut** : clients utilisent la LLA du routeur  
✅ **Protocoles de routage** : OSPFv3, EIGRP IPv6  
✅ **NDP** : tous les messages (RS, RA, NS, NA)  
✅ **Communication locale** sur le même segment

### Configuration manuelle (recommandée sur routeurs)
```
Router(config-if)# ipv6 address fe80::1 link-local
```

**Avantages** :
- Simple à mémoriser
- Cohérent sur toutes les interfaces
- Facilite l'administration

---

## 📋 Adresses multicast IPv6

### Format
```
FF[Flags][Scope]:[Group ID]
```

### Multicast well-known (permanentes)

| Adresse | Scope | Description |
|---------|-------|-------------|
| **FF02::1** | Link-Local | Tous les nœuds |
| **FF02::2** | Link-Local | Tous les routeurs |
| **FF02::5** | Link-Local | Routeurs OSPFv3 |
| **FF02::A** | Link-Local | Routeurs EIGRP |
| **FF02::1:2** | Link-Local | Serveurs/relais DHCPv6 |

---

## 🎯 Solicited-Node Multicast ⚠️ TRÈS IMPORTANT

### Format
```
FF02::1:FF[24 derniers bits de l'adresse unicast]
```

### Exemples
```
Unicast : 2001:db8:acad:1::10
          └─ Derniers 24 bits : 00:0010
Solicited-node : FF02::1:FF00:0010

Unicast : 2001:db8:acad:1:a8bb:ccff:fe00:6700
          └─ Derniers 24 bits : 00:6700
Solicited-node : FF02::1:FF00:6700
```

### Utilisation
- **NDP - Neighbor Solicitation** : résolution d'adresse (= ARP IPv4)
- **DAD** : Duplicate Address Detection
- Plus efficace que broadcast (seuls les périphériques concernés traitent)

### Adresse MAC multicast correspondante
```
Format : 33:33:[4 derniers octets de l'IPv6 multicast]

IPv6 : FF02::1:FF00:6700
MAC : 33:33:FF:00:67:00
```

---

## 📋 Segmentation IPv6

| Entité | Préfixe typique | Capacité |
|--------|----------------|----------|
| **RIR** | /12 à /23 | Milliards de réseaux |
| **ISP** | /32 | 65 536 organisations (/48) |
| **Organisation** | /48 | 65 536 sous-réseaux (/64) |
| **Sous-réseau** | /64 | 18 trillions d'hôtes |
| **Point-à-point** | /127 | 2 hôtes (RFC 6164) |
| **Loopback** | /128 | 1 adresse |

### Standard /64
✅ Compatible SLAAC  
✅ Compatible EUI-64  
✅ Simplifie la gestion  
✅ Largement suffisant (2⁶⁴ hôtes)

---

## 📋 Plan d'adressage - Exemple

**Préfixe organisation** : 2001:db8:acad::/48

| Segment | Subnet ID | Réseau | Usage |
|---------|-----------|--------|-------|
| VLAN 10 | 0001 | 2001:db8:acad:1::/64 | Utilisateurs |
| VLAN 20 | 0002 | 2001:db8:acad:2::/64 | Serveurs |
| VLAN 30 | 0003 | 2001:db8:acad:3::/64 | Invités |
| DMZ | 0100 | 2001:db8:acad:100::/64 | Serveurs publics |
| Lien WAN | FFF0 | 2001:db8:acad:fff0::/127 | Point-à-point |

---

## ⚡ Commandes de configuration

### Activation du routage IPv6
```
Router(config)# ipv6 unicast-routing
```

### Configuration interface avec GUA et LLA
```
Router(config)# interface g0/0
Router(config-if)# ipv6 address 2001:db8:acad:1::1/64
Router(config-if)# ipv6 address fe80::1 link-local
Router(config-if)# no shutdown
```

### Configuration avec EUI-64
```
Router(config-if)# ipv6 address 2001:db8:acad:2::/64 eui-64
```

### Route statique par défaut
```
Router(config)# ipv6 route ::/0 2001:db8:acad:100::1
```

### Vérification
```
show ipv6 interface brief
show ipv6 interface g0/0
show ipv6 route
show ipv6 neighbors
ping ipv6 2001:db8:acad:1::10
```

---

## 💡 Points importants pour l'examen CCNA

### À mémoriser absolument
✅ **128 bits** : 8 groupes de 16 bits hexa  
✅ **Compression** : zéros de tête + `::` une seule fois  
✅ **GUA** : 2000::/3 (routables)  
✅ **LLA** : FE80::/10 (obligatoires, non routables)  
✅ **Solicited-node** : FF02::1:FF[24 derniers bits]  
✅ **MAC multicast** : 33:33:[4 derniers octets]  
✅ **/48 → /64** : 16 bits Subnet ID = 65 536 sous-réseaux  
✅ **/64 standard** pour un segment  
✅ **FF02::1** = tous les nœuds, **FF02::2** = tous les routeurs

### Pièges à éviter
⚠️ **`::` une seule fois** par adresse (sinon ambiguïté)  
⚠️ **LLA utilisée comme passerelle** (pas la GUA)  
⚠️ **Pas de broadcast** en IPv6 → remplacé par multicast  
⚠️ **EUI-64** : insérer **FFFE** + inverser **7e bit**  
⚠️ **Solicited-node** : FF02::1:FF + **24 derniers bits** (6 chiffres hexa)  
⚠️ **/64 requis pour SLAAC** (ne pas utiliser /128 sur un segment)

### Configuration LLA manuelle
✅ **Toujours recommandée sur routeurs** : `fe80::1`, `fe80::2`, etc.  
✅ Facilite administration et troubleshooting  
✅ Cohérence sur toutes les interfaces  
✅ Clients utilisent cette LLA comme passerelle

### Hiérarchie /48 → /64
✅ Organisation reçoit **/48** (65 536 sous-réseaux possibles)  
✅ Chaque segment = **/64** (18 trillions d'hôtes)  
✅ **16 bits Subnet ID** entre /48 et /64  
✅ Nomenclature logique : 0001 (VLAN 1), 0002 (VLAN 2), etc.

### Compétences pratiques
✅ Compresser/décompresser des adresses IPv6  
✅ Calculer l'adresse solicited-node à partir d'une unicast  
✅ Générer une LLA avec EUI-64  
✅ Créer un plan d'adressage hiérarchique /48 → /64  
✅ Configurer GUA + LLA sur une interface  
✅ Identifier le type d'adresse (GUA, LLA, multicast, anycast)

---

## 🔑 Checklist de révision

- [ ] Je sais compresser une adresse IPv6 (règles 1 et 2)
- [ ] Je connais la différence entre GUA et LLA
- [ ] Je sais calculer une adresse solicited-node
- [ ] Je comprends pourquoi la LLA est utilisée comme passerelle
- [ ] Je sais générer une Interface ID avec EUI-64
- [ ] Je connais FF02::1 (all nodes) et FF02::2 (all routers)
- [ ] Je maîtrise la segmentation /48 → /64 (16 bits Subnet ID)
- [ ] Je sais configurer une interface avec GUA + LLA manuelle

---

**Durée de révision recommandée** : 30-45 minutes  
**Prochaine étape** : Module 13 - ICMP
