---
title: "Module 26: Network Device Access Control & Infrastructure Security"
module: 26
type: notes
topics: [ACL, Standard, Extended, Named, PACL, VACL, Terminal Lines, AAA, RBAC, ZBFW, CoPP]
difficulty: advanced
updated: 2026-03-18
---

# Module 26: Network Device Access Control & Infrastructure Security

## Vue d'ensemble
Le **Network Device Access Control & Infrastructure Security** (Module 26) couvre les contrôles d'accès au niveau des interfaces, des terminaux et le pare-feu d'infrastructure. Ce module est critique pour sécuriser les équipements Cisco et filtrer le trafic réseau.

---

## 1. Access Control Lists (ACLs): Fondamentaux

### 1.1 Concept Fondamental
**ACL** (Access Control List) = liste hiérarchique d'**Access Control Entries (ACEs)** dictant qui peut communiquer avec qui.

### 1.2 Processing ACLs

Les ACLs s'évaluent **de haut en bas** (first-match):

```
ACE #1 (seq 10) → Match? → Action (permit/deny) + STOP
                   Non ↓
ACE #2 (seq 20) → Match? → Action + STOP
                   Non ↓
ACE #3 (seq 30) → Match? → Action + STOP
                   Non ↓
...
Implicit Deny → STOP (paquet rejeté)
```

**Principal règle**: Premier match gagne, pas d'évaluation suite

### 1.3 Implicit Deny
**Chaque ACL termine par "deny any" implicite**:
- Même si pas écrite, elle existe
- Tous paquets non-matchés = rejetés
- Nécessite "permit any" explicite si accès par défaut

---

## 2. Types d'ACLs (5 variantes)

### 2.1 Numérotation ACLs

| Type | Plage Numéraire | Scope |
|------|-----------------|-------|
| **Standard** | 1-99, 1300-1999 | Source seulement |
| **Extended** | 100-199, 2000-2699 | Source/Dest/Protocol/Port |
| **Named** | nommée (string) | Standard ou Extended |
| **PACL** | named (couche 2) | Ports Layer 2 |
| **VACL** | named (couche 2) | VLANs entières |

### 2.2 ACL Standard: Source Uniquement

Syntaxe numérotée:
```
access-list {1-99|1300-1999} {permit|deny} source [wildcard] [log]
```

Exemple:
```
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny any log
```

Application interface:
```
ip access-group 10 in
```

### 2.3 ACL Extended: Source/Dest/Protocol/Port

Syntaxe numérotée:
```
access-list {100-199|2000-2699} {permit|deny} protocol source wildcard 
            dest wildcard [options] [log|log-input]
```

Exemple:
```
access-list 101 permit tcp 192.168.1.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 80
access-list 101 permit tcp 192.168.1.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 443
access-list 101 deny ip any any log
```

Protocols courants: `ip`, `tcp`, `udp`, `icmp`, `eigrp`, `ospf`

### 2.4 ACL Named: Approche Moderne

Syntaxe:
```
ip access-list standard|extended {name|#}
 [seq] {permit|deny} ...
 [seq] {permit|deny} ...
```

Exemple Standard:
```
ip access-list standard REMOTE_OFFICES
 10 permit 192.168.1.0 0.0.0.255
 20 permit 192.168.2.0 0.0.0.255
 30 deny any
```

Exemple Extended:
```
ip access-list extended WEB_TRAFFIC
 10 permit tcp any any eq 80
 20 permit tcp any any eq 443
 30 deny ip any any log
```

**Avantages Named ACLs**:
- Noms descriptifs (lisibilité)
- Modification facile (insertion/suppression ACEs)
- Réutilisabilité multi-contexte

---

## 3. Wildcard Masks (Masques Génériques)

### 3.1 Calcul Wildcard Mask

**Wildcard = 255.255.255.255 - Subnet Mask**

| Subnet Mask | Wildcard Mask | Réseau /notation |
|-------------|---------------|------------------|
| 255.255.255.0 | 0.0.0.255 | /24 |
| 255.255.255.128 | 0.0.0.127 | /25 |
| 255.255.0.0 | 0.0.255.255 | /16 |
| 255.255.128.0 | 0.0.127.255 | /17 |
| 0.0.0.0 | 255.255.255.255 | (any) |

### 3.2 Interprétation Wildcard

**0 (zéro) = must match exactement**
**1 (un) = don't care (ignore)**

Exemple: `192.168.1.0 0.0.0.255`
```
192.168.1.X (X peut être 0-255, tous matchent)
```

Keywords simplifiés:
- `any` = 0.0.0.0 255.255.255.255 (tous)
- `host` = adresse spécifique + 0.0.0.0 wildcard

---

## 4. Application ACLs: Interfaces et Directions

### 4.1 Syntaxe d'Application

```
interface GigabitEthernet0/0
 ip access-group {ACL#|name} {in|out}
```

### 4.2 Restrictions d'Application

- **Max 1 ACL inbound** par interface
- **Max 1 ACL outbound** par interface
- S'applique au trafic **entrant (in)** ou **sortant (out)**

```
Trafic entrant → [ACL Inbound] → Interface → Routage
                                     ↓
                               [ACL Outbound] → Sortie
```

### 4.3 Directions Logiques

| Direction | Scope | Cas d'usage |
|-----------|-------|-----------|
| **in** | Avant routage | Bloquer source malveillant |
| **out** | Après routage | Bloquer destination non-autorisée |

---

## 5. Port ACLs (PACLs): Filtrage Couche 2

### 5.1 Concept PACL
**PACL** (Port ACL) applique filtrage standards/extended IPv4 ou MAC au niveau port switch.

### 5.2 Syntaxe PACLs

```
ip access-list standard|extended {name|#}
 {permit|deny} ...

interface GigabitEthernet0/1
 ip access-group {name|#} in    ← Inbound only
```

### 5.3 Restrictions PACLs Critiques

**Les PACLs ont limitations significatives**:

1. **Inbound uniquement**: pas d'ACL outbound couche 2
2. **Pas de L2 Control**: ne filtre pas CDP, VTP, DTP, PAgP, UDLD, STP
   - Ces protocoles dépassent les PACLs
3. **Hardware-only**: pas de traitement CPU, table CAM
4. **Pas IPv6/ARP**: PACLs IPv4 seulement (ACLs IPv6 distinctes pour IPv6)
5. **Pas MPLS**: ignoré si Label Switch Path présent

### 5.4 Cas d'usage PACL

```
Attaque Layer 2 depuis port spécifique
                 ↓
          [PACL appliqué port]
                 ↓
     Trafic malveillant bloqué
     Protocoles L2 control non-affectés
```

---

## 6. VLAN ACLs (VACLs): Filtrage Couche 2 Inter-VLAN

### 6.1 Concept VACL
**VACL** (VLAN ACL) filtre trafic **au sein d'une VLAN entière** (forwarding, pas routage).

### 6.2 Création VACLs

**Étape 1**: Créer access-list standard/extended pour matching

```
ip access-list standard VOICE_DEVICES
 permit 10.0.1.0 0.0.0.255
```

**Étape 2**: Créer vlan access-map (action = permit/drop)

```
vlan access-map VOICE_POLICY 10
 match ip address VOICE_DEVICES
 action forward
 
vlan access-map VOICE_POLICY 20
 match ip address any
 action drop log
```

**Étape 3**: Appliquer à VLAN

```
vlan filter VOICE_POLICY vlan-list 100-105
```

### 6.3 Syntaxe Complète VACLs

```
vlan access-map {map-name} {seq-num}
 match {ip address {acl-name|number}|mac address acl-name}
 action {forward|drop} [log]

vlan filter {map-name} vlan-list {vlan-range}
```

### 6.4 Différences VACL vs ACLs standard

| Aspect | VACL | Standard ACL |
|--------|------|-------------|
| **Scope** | VLAN entière | Interface/direction |
| **Direction** | In+Out (bridged) | In ou Out |
| **L2 Filtering** | Oui | Non |
| **Action** | forward/drop | permit/deny |
| **Routage** | **Bridged uniquement** | Routed aussi |

---

## 7. Processing ACLs: Bridged vs Routed

### 7.1 Trafic Bridged (Même VLAN, pas routage)

```
Paquet → [PACL Inbound] → [VACL Inbound] → Forward → [VACL Outbound]
```

### 7.2 Trafic Routed (Inter-VLAN, routeur)

```
Paquet → [PACL Inbound] → [VACL Inbound] 
         → [SVI Inbound ACL] → Routage 
         → [SVI Outbound ACL] → [VACL Outbound]
```

Où **SVI** = Switch Virtual Interface (VLAN interface routeur)

---

## 8. Terminal Line Security: Console & Telnet/SSH

### 8.1 Authentification Terminale

Deux lignes désactives par défaut:

```
line console 0
 login
 password CISCO123

line vty 0 4
 login
 password REMOTE_ACCESS
```

### 8.2 Configuration Locale vs AAA

**Local (simple)**:
```
username admin privilege 15 secret $crypt_password
username user1 privilege 1 secret $crypt_password

line console 0
 login local

line vty 0 4
 login local
```

**AAA (enterprise)**:
```
aaa new-model
aaa authentication login default group tacacs+ local
aaa authorization commands 15 default group tacacs+ local

line vty 0 4
 access-class ADMIN_IPS in
```

---

## 9. Privilege Levels: Contrôle de Commandes

### 9.1 Niveaux Prédéfinis

| Niveau | Description | Accès |
|--------|-------------|-------|
| **0** | Disable | Désactivation seulement |
| **1** | User (default) | show, ping, trace (read-only) |
| **15** | Enable | Full admin access |
| **2-14** | Custom | Granularité fine |

### 9.2 Assignment des Custom Levels

```
privilege mode {level} {command}

Example:
privilege exec 5 show running-config
privilege interface 7 ip address
privilege configure 10 router eigrp
```

### 9.3 Assignment Utilisateurs

```
username admin privilege 15 ...
username readonly privilege 1 ...
username manager privilege 5 ...

line vty 0 4
 privilege level 1    ← niveau par défaut (peut override)
```

---

## 10. RBAC (Role-Based Access Control)

### 10.1 Concept
**RBAC** classe utilisateurs par **rôles** avec permissions pré-définies.

Rôle = ensemble privilege levels + commandes associées

### 10.2 Implémentation Cisco

```
Example Roles:
- Administrator: privilege 15
- Manager: privilege 7 (show, reload)
- Operator: privilege 5 (show, clear counters)
- Guest: privilege 1 (show only)

username alice privilege 15 group administrator
username bob privilege 7 group manager
```

---

## 11. AAA (Authentication, Authorization, Accounting)

### 11.1 Les 3 A

| A | Définition | Exemple |
|---|-----------|---------|
| **Auth** | Qui es-tu? | Vérifier username/password |
| **Authz** | Que peux-tu faire? | Niveau privilege assigné |
| **Acct** | Quoi as-tu fait? | Logging actions, syslog |

### 11.2 TACACS+ (Terminal Access Controller Access-Control System Plus)

**TACACS+** = serveur AAA centralisé, protocole propriétaire Cisco.

Syntaxe configuration:
```
aaa new-model
tacacs server TACACS_SERVER1
 address ipv4 10.0.0.1
 key TacacsSecret123

aaa authentication login default group tacacs+ local
aaa authorization commands 15 default group tacacs+ local
aaa accounting commands 15 default start-stop group tacacs+
```

### 11.3 Method Lists

```
aaa authentication login {list-name} method1 method2 fallback
```

Méthodes: `group tacacs+`, `local`, `enable`, `line`

Ordre évaluation:
1. Méthode 1 (TACACS+): disponible?
2. Sinon, Méthode 2 (local): credentials local?
3. Sinon, Fallback

---

## 12. Zone-Based Firewall (ZBFW)

### 12.1 Concept ZBFW
**ZBFW** (Zone-Based Firewall) = pare-feu stateful **par zones** sur routeurs, pas par interfaces.

### 12.2 Zones de Sécurité

```
┌──────────────────────────────────┐
│         INTERNET ZONE            │
│       [Untrusted, No rules]      │
└────────────────┬─────────────────┘
                 │
          [Zone-pair policies]
                 ↓
┌──────────────────────────────────┐
│       INSIDE ZONE                │
│   [Internal users, trusted]      │
└──────────────────────────────────┘
```

Zones typiques: `inside`, `outside`, `dmz`, `guest`, etc.

### 12.3 Configuration ZBFW: 5 Étapes

**Étape 1**: Définir zones
```
zone security INSIDE
zone security OUTSIDE
zone security DMZ
```

**Étape 2**: Assigner interfaces à zones
```
interface GigabitEthernet0/0
 zone-member security INSIDE

interface GigabitEthernet0/1
 zone-member security OUTSIDE

interface GigabitEthernet0/2
 zone-member security DMZ
```

**Étape 3**: Créer classe maps (trafic match)
```
class-map type inspect match-any HTTP_TRAFFIC
 match protocol http
 match protocol https
```

**Étape 4**: Créer policy maps (actions)
```
policy-map type inspect INSIDE_TO_OUTSIDE
 class type inspect HTTP_TRAFFIC
  inspect
 class class-default
  drop
```

**Étape 5**: Appliquer zone-pairs
```
zone-pair security INSIDE-OUTSIDE source INSIDE destination OUTSIDE
 service-policy type inspect INSIDE_TO_OUTSIDE
```

### 12.4 Avantages ZBFW

- **Stateful inspection**: suivre connexions
- **Easy policies**: logique intuitive zone-pair
- **Granular control**: par classe trafic

---

## 13. Control Plane Policing (CoPP)

### 13.1 Concept CoPP
**CoPP** (Control Plane Policing) protège la **Route Processor (RP)** du routeur contre DoS/flooding.

### 13.2 Problématique

```
Attaque DoS:
 Flood paquets → CPU routeur surchargé → Routes instables
                  (BGP adjacencies down, EIGRP hello missed)
                  
CoPP solution:
 → Rate-limit paquets destiné CPU
 → Priorisé OSPF/BGP/SSH
 → Rejeté excédent silencieusement
```

### 13.3 Configuration CoPP: 4 Étapes

**Étape 1**: Créer ACL(s) classifier paquets
```
access-list 101 permit tcp any any eq 22  ← SSH
access-list 102 permit ospf any any       ← OSPF
access-list 103 permit icmp any any       ← PING
access-list 199 permit ip any any         ← Default
```

**Étape 2**: Créer class-maps
```
class-map MANAGEMENT
 match access-group 101

class-map ROUTING
 match access-group 102
```

**Étape 3**: Créer policy-map (rate-limits)
```
policy-map CONTROL_PLANE_POLICY
 class MANAGEMENT
  police 8000 1500 conform-action transmit exceed-action drop
 class ROUTING
  police 4000 1500 conform-action transmit exceed-action drop
 class class-default
  police 1000 1500 conform-action transmit exceed-action drop
```

**Étape 4**: Appliquer à control-plane
```
control-plane
 service-policy input CONTROL_PLANE_POLICY
```

---

## 14. Résumé Hiérarchie Sécurité Couche 3/2

```
┌─────────────────────────────────────────┐
│         Terminal Line Security          │
│  (Console/Telnet/SSH authentication)    │
├─────────────────────────────────────────┤
│       Device/Infrastructure Security    │
│  (Privilege levels, RBAC, AAA, CoPP)    │
├─────────────────────────────────────────┤
│          Zone-Based Firewall            │
│  (Zone policies, stateful inspection)   │
├─────────────────────────────────────────┤
│        Interface/VLAN ACLs              │
│  (PACLs, VACLs, named/numbered ACLs)    │
└─────────────────────────────────────────┘
```

---

## 15. Points d'Examen Clés

✓ **ACL Standard**: 1-99/1300-1999, source seulement  
✓ **ACL Extended**: 100-199/2000-2699, source/dest/protocol/port  
✓ **Named ACLs**: approche moderne, manipulation facile  
✓ **Wildcard Mask**: calcul (255.255.255.255 - subnet)  
✓ **PACL**: inbound-only, pas L2 control, hardware  
✓ **VACL**: vlan access-map, match + action (forward/drop)  
✓ **Processing**: PACL → VACL in → SVI in → SVI out → VACL out (routed)  
✓ **Terminal Lines**: console 0, vty 0 4, password/local/aaa  
✓ **Privilege Levels**: 0-15, custom 2-14, privilege level # command  
✓ **RBAC**: rôles utilisateurs, assignments privilege  
✓ **AAA**: TACACS+, évaluation sequentielle, method-lists  
✓ **ZBFW**: zones, zone-pairs, class-map/policy-map, zone-member  
✓ **CoPP**: rate-limit control-plane, protection DoS CPU
