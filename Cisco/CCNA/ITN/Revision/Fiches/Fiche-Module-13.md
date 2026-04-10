# Fiche de révision CCNA ITN - Module 13
## ICMP et protocoles de connectivité

---

## 🎯 Concepts clés

### ICMP - Rôle
- Protocole **couche 3** (Layer 3)
- **Messages d'erreur** : signaler problèmes de transmission
- **Messages d'information** : diagnostic (ping, traceroute)
- **Contrôle réseau** : redirection, PMTUD
- ❌ **Non fiable** (pas de garantie de livraison)

### Versions
- **ICMPv4** : RFC 792 (avec IPv4)
- **ICMPv6** : RFC 4443 (avec IPv6, intègre NDP)

---

## 📋 ICMPv4 - Messages d'erreur ⚠️ IMPORTANT

### Type 3 - Destination Unreachable (4 codes essentiels)

| Code | Nom | Description | Généré par | Utilisation |
|------|-----|-------------|------------|-------------|
| **0** | Network Unreachable | Pas de route vers réseau | Routeur | Routage |
| **1** | Host Unreachable | Hôte inaccessible | Routeur | ARP échoue |
| **3** | Port Unreachable | Port UDP fermé | Hôte | **Traceroute** |
| **4** | Fragmentation Needed (DF) | Paquet trop grand, DF=1 | Routeur | **PMTUD** |

**Autres codes utiles** :
- **Code 2** : Protocol Unreachable
- **Code 13** : Administratively Prohibited (ACL/firewall)

### Type 11 - Time Exceeded ⚠️ CRUCIAL

| Code | Nom | Description | Utilisation |
|------|-----|-------------|-------------|
| **0** | TTL Exceeded in Transit | TTL = 0 pendant transit | **Traceroute** |
| **1** | Fragment Reassembly Time Exceeded | Réassemblage échoué | Rare |

**Fonctionnement traceroute** :
```
TTL=1 → Routeur 1 → ICMP Type 11 Code 0
TTL=2 → Routeur 2 → ICMP Type 11 Code 0
TTL=3 → Routeur 3 → ICMP Type 11 Code 0
...
TTL=N → Destination → ICMP Type 3 Code 3 (Port Unreachable)
```

### Autres types d'erreur
- **Type 5** : Redirect (meilleur chemin disponible)
- **Type 12** : Parameter Problem (entête malformé)

---

## 📋 ICMPv4 - Messages d'information

| Type | Code | Nom | Description |
|------|------|-----|-------------|
| **8** | 0 | Echo Request | Ping (demande) |
| **0** | 0 | Echo Reply | Pong (réponse) |

---

## 📋 ICMPv6 - Messages d'erreur ⚠️ IMPORTANT

### Type 1 - Destination Unreachable (5 codes essentiels)

| Code | Nom | Description | Équivalent IPv4 |
|------|-----|-------------|-----------------|
| **0** | No route to destination | Pas de route | Type 3 Code 0/1 |
| **1** | Administratively prohibited | ACL/firewall | Type 3 Code 13 |
| **3** | Address unreachable | NDP échoue | Type 3 Code 1 |
| **4** | Port unreachable | Port UDP fermé | Type 3 Code 3 |

**Autres codes** :
- **Code 2** : Beyond scope of source address
- **Code 5** : Source address failed policy
- **Code 6** : Reject route

### Type 2 - Packet Too Big ⚠️ CRUCIAL

| Code | Description | Utilisation |
|------|-------------|-------------|
| **0** | Paquet trop grand pour MTU | **PMTUD obligatoire** en IPv6 |

⚠️ **IPv6 ne fragmente pas en transit** (contrairement IPv4)

### Type 3 - Time Exceeded

| Code | Nom | Description | Utilisation |
|------|-----|-------------|-------------|
| **0** | Hop Limit Exceeded | Hop Limit = 0 | **Traceroute IPv6** |
| **1** | Fragment Reassembly Time Exceeded | Réassemblage échoué | Rare |

### Autres types d'erreur
- **Type 4** : Parameter Problem (entête malformé)

---

## 📋 ICMPv6 - Messages d'information

| Type | Code | Nom | Description |
|------|------|-----|-------------|
| **128** | 0 | Echo Request | Ping IPv6 (demande) |
| **129** | 0 | Echo Reply | Pong IPv6 (réponse) |

---

## 📋 NDP - 5 types de messages ICMPv6 ⚠️ ESSENTIEL

### Messages NDP

| Type | Nom | Destination | Rôle |
|------|-----|-------------|------|
| **133** | Router Solicitation (RS) | FF02::2 (all routers) | Demander annonce routeurs |
| **134** | Router Advertisement (RA) | FF02::1 (all nodes) | Annoncer routeur + config |
| **135** | Neighbor Solicitation (NS) | Solicited-node | Résolution adresse, DAD |
| **136** | Neighbor Advertisement (NA) | Unicast | Réponse à NS |
| **137** | Redirect | Unicast | Meilleur chemin disponible |

---

## 🎯 Router Advertisement (RA) - Flags ⚠️ TRÈS IMPORTANT

### Flags dans les messages RA

| Flag | Nom | Signification |
|------|-----|---------------|
| **M** | Managed Address Config | 1 = utiliser DHCPv6 stateful pour adresse |
| **O** | Other Configuration | 1 = utiliser DHCPv6 stateless pour DNS/autres |
| **A** | Autonomous Address Config | 1 = utiliser SLAAC (généralement activé) |

---

## 📋 3 méthodes d'allocation IPv6 ⚠️ CRUCIAL POUR L'EXAMEN

### Méthode 1 : SLAAC Only (M=0, O=0)

```
Router(config-if)# no ipv6 nd managed-config-flag
Router(config-if)# no ipv6 nd other-config-flag
```

| Aspect | Valeur |
|--------|--------|
| **Adresse** | Auto-générée (SLAAC) |
| **DNS** | ❌ Non fourni |
| **Serveur DHCPv6** | ❌ Non requis |
| **Contrôle** | Faible |

**Utilisation** : petits réseaux sans DNS automatique

---

### Méthode 2 : SLAAC + DHCPv6 Stateless (M=0, O=1) ⚠️ RECOMMANDÉE

```
Router(config-if)# no ipv6 nd managed-config-flag
Router(config-if)# ipv6 nd other-config-flag
```

| Aspect | Valeur |
|--------|--------|
| **Adresse** | Auto-générée (SLAAC) |
| **DNS** | ✅ Fourni par DHCPv6 |
| **Serveur DHCPv6** | ✅ Requis (stateless) |
| **Contrôle** | Partiel |

**Processus** :
1. Hôte génère adresse via SLAAC (préfixe du RA)
2. Hôte contacte serveur DHCPv6 pour DNS/domaine/NTP
3. Serveur DHCPv6 **ne gère pas les adresses** (stateless)

**Utilisation** : réseaux d'entreprise (méthode la plus courante)

---

### Méthode 3 : DHCPv6 Stateful (M=1)

```
Router(config-if)# ipv6 nd managed-config-flag
Router(config-if)# ipv6 nd other-config-flag  # (optionnel)
```

| Aspect | Valeur |
|--------|--------|
| **Adresse** | Fournie par DHCPv6 |
| **DNS** | ✅ Fourni par DHCPv6 |
| **Serveur DHCPv6** | ✅ Requis (stateful) |
| **Contrôle** | Total |

**Processus** :
1. Hôte reçoit RA avec M=1
2. Hôte **ne génère PAS** d'adresse via SLAAC
3. Hôte contacte serveur DHCPv6 pour adresse + config complète
4. Serveur DHCPv6 **maintient état** des adresses (logs)

**Utilisation** : contrôle strict, traçabilité requise

---

## 📋 Comparaison des 3 méthodes

| Méthode | M | O | Adresse | DNS | Serveur DHCPv6 | Contrôle |
|---------|---|---|---------|-----|----------------|----------|
| **SLAAC Only** | 0 | 0 | SLAAC | ❌ | ❌ Non requis | ❌ Faible |
| **SLAAC + DHCPv6 Stateless** | 0 | 1 | SLAAC | ✅ | ✅ Requis | ⚠️ Partiel |
| **DHCPv6 Stateful** | 1 | x | DHCPv6 | ✅ | ✅ Requis | ✅ Total |

---

## 🎯 SLAAC - Processus complet

### Étapes de configuration automatique

```
1. Génération Link-Local (FE80::)
   ↓
2. Router Solicitation (RS) → FF02::2
   ↓
3. Router Advertisement (RA) ← Routeur
   (Préfixe : 2001:db8:acad:1::/64, M=0, O=0/1)
   ↓
4. Génération Interface ID (EUI-64 ou aléatoire)
   ↓
5. DAD (Duplicate Address Detection) avec NS
   ↓
6. Configuration complète
   Adresse : 2001:db8:acad:1:[Interface ID]/64
   Passerelle : FE80::1 (LLA du routeur)
```

---

## ⚡ Commandes de diagnostic

### Ping

**IPv4** :
```
C:\> ping 8.8.8.8
Router# ping 8.8.8.8
```

**IPv6** :
```
C:\> ping 2001:4860:4860::8888
Router# ping ipv6 2001:4860:4860::8888
```

### Traceroute

**IPv4** :
```
C:\> tracert 8.8.8.8
Router# traceroute 8.8.8.8
```

**IPv6** :
```
C:\> tracert 2001:4860:4860::8888
Router# traceroute ipv6 2001:4860:4860::8888
```

### Vérification NDP

```
Router# show ipv6 neighbors
Router# show ipv6 routers
Router# show ipv6 interface g0/0
Router# debug ipv6 nd  (à désactiver après : undebug all)
```

---

## 💡 Points importants pour l'examen CCNA

### ICMPv4 - À mémoriser
✅ **Type 3 Code 0** : Network Unreachable  
✅ **Type 3 Code 1** : Host Unreachable  
✅ **Type 3 Code 3** : Port Unreachable (traceroute)  
✅ **Type 3 Code 4** : Fragmentation Needed (PMTUD)  
✅ **Type 11 Code 0** : TTL Exceeded (traceroute)  
✅ **Type 8** : Echo Request (ping)  
✅ **Type 0** : Echo Reply (pong)

### ICMPv6 - À mémoriser
✅ **Type 1 Code 0** : No route to destination  
✅ **Type 1 Code 3** : Address unreachable  
✅ **Type 1 Code 4** : Port unreachable  
✅ **Type 2** : Packet Too Big (PMTUD obligatoire IPv6)  
✅ **Type 3 Code 0** : Hop Limit Exceeded (traceroute)  
✅ **Type 128** : Echo Request (ping)  
✅ **Type 129** : Echo Reply (pong)

### NDP - 5 types à connaître
✅ **Type 133 (RS)** : Router Solicitation → FF02::2  
✅ **Type 134 (RA)** : Router Advertisement → FF02::1 (flags M, O)  
✅ **Type 135 (NS)** : Neighbor Solicitation → solicited-node (résolution, DAD)  
✅ **Type 136 (NA)** : Neighbor Advertisement → unicast  
✅ **Type 137** : Redirect

### 3 méthodes d'allocation IPv6 ⚠️ QUESTION FRÉQUENTE
✅ **M=0, O=0** : SLAAC Only (pas de DNS)  
✅ **M=0, O=1** : SLAAC + DHCPv6 Stateless (recommandée, DNS fourni)  
✅ **M=1** : DHCPv6 Stateful (contrôle total)

### Pièges à éviter
⚠️ **Traceroute** utilise **Type 11 Code 0** (TTL Exceeded) puis **Type 3 Code 3** (Port Unreachable)  
⚠️ **PMTUD** : Type 3 Code 4 (IPv4) vs **Type 2** (IPv6)  
⚠️ **IPv6 PMTUD obligatoire** (pas de fragmentation en transit)  
⚠️ **NDP utilise solicited-node** (FF02::1:FF[24 derniers bits]), pas FF02::1  
⚠️ **LLA du routeur** utilisée comme passerelle (pas la GUA)  
⚠️ **M=0, O=1 = méthode recommandée** (SLAAC + DNS via DHCPv6)

### Processus SLAAC
✅ RS → FF02::2  
✅ RA ← FE80::1 (préfixe + flags M, O)  
✅ Génération Interface ID (EUI-64 ou aléatoire)  
✅ DAD avec NS vers solicited-node  
✅ Configuration finale (GUA + passerelle LLA)

### Compétences pratiques
✅ Identifier le type/code ICMP à partir d'une capture Wireshark  
✅ Comprendre le fonctionnement de traceroute (TTL/Hop Limit)  
✅ Configurer les flags M et O sur un routeur  
✅ Choisir la méthode d'allocation selon le scénario  
✅ Diagnostiquer avec ping et traceroute (IPv4/IPv6)  
✅ Interpréter la sortie de `show ipv6 neighbors`

---

## 🔑 Checklist de révision

- [ ] Je connais les codes ICMP Type 3 essentiels (0, 1, 3, 4)
- [ ] Je comprends le fonctionnement de traceroute (Type 11 Code 0)
- [ ] Je connais les 5 types de messages NDP (133, 134, 135, 136, 137)
- [ ] Je maîtrise les 3 méthodes d'allocation IPv6 (M, O flags)
- [ ] Je sais quelle méthode est recommandée (M=0, O=1)
- [ ] Je comprends le processus SLAAC complet
- [ ] Je connais la différence entre DHCPv6 stateful et stateless
- [ ] Je sais utiliser ping et traceroute (IPv4/IPv6)

---

**Durée de révision recommandée** : 30-45 minutes  
**Prochaine étape** : Module 14 - Couche Transport
