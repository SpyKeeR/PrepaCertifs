# Fiche Révision Module 8 : OSPF

## 1. Architecture OSPF Fondamentale

```
OSPF DOMAIN
├── Area 0 (Backbone - OBLIGATOIRE)
│   ├── Core Routers
│   └── ABRs
├── Area 1
│   ├── Internal Routers
│   └── ABR → Area 0
├── Area 2
│   ├── Internal Routers
│   └── ABR → Area 0
└── ASBR (Any Area)
    └── Routes Externes (Type 5 LSA)
```

## 2. Router ID (RID) et Sélection

### Sélection Automatique (Ordre)
1. RID configuré explicitement
2. Adresse IP loopback la plus élevée
3. Adresse IP physique la plus élevée

### Configuration
```
router ospf 100
 router-id 1.1.1.1                              ! Recommandé
```

## 3. États du Voisinage OSPF

```
Down → Init → 2-Way → ExStart → Exchange → Loading → Full
       ↑━━━━━━━↑  Élection DR/BDR ici
```

| État | Signification |
|---|---|
| **Down** | Pas de Hello reçu |
| **Init** | Hello reçu MAI sans RID local |
| **2-Way** | Hello reçu AVEC RID local, DR/BDR élu |
| **ExStart** | Master/Slave élu |
| **Exchange** | Échange DD (Database Description) |
| **Loading** | LSR/LSU (demande/réception LSAs) |
| **Full** | LSDB sync, adjacency établie |

## 4. Élection DR/BDR - Processus

### Critères d'Élection (Par Ordre)
1. **Priorité Interface** (0-255, défaut 1)
   - 0 = Jamais élu
   - Plus haut = Plus de chance
2. Si égalité → **RID la plus élevée**

### Configuration
```
interface Gi0/0
 ip ospf priority 100  ! Élève priorité (défaut 1)
```

### Rôles
| Rôle | Adjacencies | Rôle |
|---|---|---|
| **DR** | Full avec tous | Floode LSA centralisé |
| **BDR** | Full avec tous | Backup si DR défaille |
| **DROther** | Full seulement avec DR+BDR | Routeur normal |

**Exemple Topologie** :
```
3 Routeurs sur Ethernet
├─ R1 (Priority 100) = DR
├─ R2 (Priority 50) = BDR
└─ R3 (Priority 1) = DROther (2 adjacencies)

Sans DR/BDR : 3 routeurs = 3 adjacencies = 3 inondations
Avec DR/BDR : 3 routeurs = 2 adjacencies = 1 inondation centralisée
```

## 5. Network Statements et Wildcards

### Format
```
network <réseau> <masque-wildcard> area <area-id>
```

### Wildcard Mask (Inverse)
| CIDR | Masque Standard | Wildcard |
|---|---|---|
| /32 | 255.255.255.255 | 0.0.0.0 |
| /24 | 255.255.255.0 | 0.0.0.255 |
| /16 | 255.255.0.0 | 0.0.255.255 |
| /8 | 255.0.0.0 | 0.255.255.255 |
| /0 | 0.0.0.0 | 255.255.255.255 |

### Exemples Configuration
```
network 192.168.1.0 0.0.0.255 area 0        ! /24 précis
network 192.168.0.0 0.0.255.255 area 0      ! /16
network 0.0.0.0 255.255.255.255 area 0      ! Catchall (passif)
```

## 6. Timers OSPF - Par Défaut

| Type d'Interface | Hello | Dead (Total) | Ratio |
|---|---|---|---|
| **Ethernet/Point-to-Point** | 10 sec | 40 sec | 1:4 |
| **Point-to-Multipoint** | 30 sec | 120 sec | 1:4 |
| **NBMA (Non-Broadcast Multi-Access)** | 30 sec | 120 sec | 1:4 |

### Configuration Interface
```
interface Gi0/0
 ip ospf hello-interval 10    ! 10 secondes
 ip ospf dead-interval 40     ! 40 secondes
```

### Detection Rapide (Failover < 1 sec)
```
interface Gi0/0
 ip ospf dead-interval minimal hello-multiplier 5
 ! Dead = Hello × 5 (ex: 1 sec × 5 = 5 sec)
```

## 7. Métrique/Coût OSPF

### Formule
$$Coût = \frac{100,000,000}{Bande \, passante \, (bps)}$$

### Valeurs Typiques
```
1 Gbps (1,000,000,000 bps)    → Coût = 1
100 Mbps (100,000,000 bps)    → Coût = 10
10 Mbps (10,000,000 bps)      → Coût = 100
1 Mbps (1,000,000 bps)        → Coût = 100
```

### Override Coût
```
interface Gi0/0
 ip ospf cost 25    ! Force coût 25 (ignore BW)
```

## 8. Types d'LSA (Link State Advertisements)

### Table de Référence

| Type | Nom | Scope | Fonction |
|---|---|---|---|
| **1** | Router LSA | Intra-area | Liens du routeur |
| **2** | Network LSA | Intra-area | Réseau multi-accès (DR) |
| **3** | Network Summary | Inter-area | Routes résumées (ABR) |
| **4** | ASBR Summary | Inter-area | Annonce ASBR (ABR) |
| **5** | AS External | AS-wide | Routes externes |
| **7** | NSSA External | Area only | Routes NSSA |

### Exemple LSDB
```
show ip ospf database

           Router Link States (Area 0)
Link ID    ADV Router  Age  Seq  Checksum
1.1.1.1    1.1.1.1     145  0x80000003  0xF2EF  [Type 1]
2.2.2.2    2.2.2.2     156  0x80000002  0x5C1A  [Type 1]

           Network Link States (Area 0)
Link ID    ADV Router  Age  Seq  Checksum
192.168.1.1 2.2.2.2    156  0x80000001  0xABCD [Type 2]

           Net Summary Link States (Area 0)
Link ID    ADV Router  Age  Seq  Checksum
10.0.0.0   3.3.3.3     200  0x80000001  0xDEF0  [Type 3]
```

## 9. Types de Routes OSPF dans RIB

| Notation | Type | Scope | Exemple |
|---|---|---|---|
| **O** | Intra-area | Routeur même area | O 192.168.1.0/24 [110/10] |
| **O IA** | Inter-area | Via ABR | O IA 10.0.0.0/24 [110/20] |
| **O E1** | External Type 1 | Externe (métrique cumulée) | O E1 172.16.0.0/16 [110/30] |
| **O E2** | External Type 2 | Externe (métrique fixe) | O E2 172.16.0.0/16 [110/20] |

## 10. Types de Routeurs

```
Internal Router (IR)
├── Toutes interfaces = Même area
└── Exemple : Area 1 only

Area Border Router (ABR)
├── Interfaces = Area 0 + Autres areas
├── Génère Type 3 LSA
└── Résume routes inter-area

AS Boundary Router (ASBR)
├── Injecte routes externes (redistribution)
├── Génère Type 5 LSA
└── Peut être dans area quelconque

Backbone Router
├── Au moins une interface dans Area 0
└── Participe au routing hierarchy

Virtual Link Router
├── Connecte areas discontigues
└── À travers transit area
```

## 11. Configuration OSPF Minimum

```bash
router ospf 100
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0

interface Gi0/0
 ip ospf 100 area 0              ! Alternative network statement
```

## 12. Commandes Essentielles

### Configuration
```bash
router ospf <process-id>
 router-id <IP>
 network <net> <wildcard> area <id>
 default-information originate always [metric <cost>]

interface <int>
 ip ospf <process-id> area <id>
 ip ospf cost <value>
 ip ospf priority <0-255>
 ip ospf hello-interval <sec>
 ip ospf dead-interval <sec>
```

### Vérification
```bash
show ip ospf                      ! État général
show ip ospf neighbor             ! Voisins
show ip ospf neighbor detail      ! Détails voisins
show ip ospf interface            ! Interfaces OSPF
show ip ospf database             ! LSDB complète
show ip ospf database router      ! Type 1 LSAs
show ip ospf database network     ! Type 2 LSAs
show ip ospf database summary     ! Type 3 LSAs
show ip ospf database external    ! Type 5 LSAs
show ip route ospf                ! Routes OSPF
```

### Dépannage
```bash
debug ip ospf adjacency           ! Adjacency debug
debug ip ospf hello               ! Hello packets
debug ip ospf spf                 ! SPF calculations
clear ip ospf process             ! Restart OSPF (change RID)
clear ip ospf neighbor            ! Force recalcul adjacencies
```

## 13. Checklist Configuration

- [ ] RID configuré explicitement
- [ ] Network statements précis (wildcard OK)
- [ ] Area 0 présente
- [ ] Voisins détectés (show ip ospf neighbors)
- [ ] États Full (pas stuck en ExStart/Exchange)
- [ ] Timers Hello/Dead correct
- [ ] DR/BDR élus correctement
- [ ] LSDB synchronisé (show ip ospf database)
- [ ] Routes dans RIB (show ip route ospf)
- [ ] Coûts calculés correctement

## 14. Pièges Courants

❌ Wildcard mask inversé (0.0.0.255 vs 255.255.255.0 standard)  
❌ RID non configuré (slow selection, changements imprévisibles)  
❌ Protocoles différents dans même area (timers, format LSA)  
❌ Priority pas assez élevée pour DR (par défaut 1, trop bas)  
❌ Hello/Dead non synchronisés entre voisins  
❌ Area structure discontigus sans transit areas  
❌ Oublier Area 0 (obligatoire pour hierarchie)

---
**Temps révision** : 45 min | **Niveau** : Basique-Intermédiaire
