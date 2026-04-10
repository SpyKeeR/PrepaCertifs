# Fiche de révision CCNA ITN - Module 11
## Adressage IPv4

---

## 🎯 Concepts clés

### Types d'adresses IPv4
- **Unicast** : un-à-un (communication point-à-point)
- **Broadcast** : un-à-tous (tous les hôtes du réseau)
- **Multicast** : un-à-plusieurs (groupe 224.0.0.0/4)

### Structure d'une adresse IPv4
```
[ Partie Réseau ] [ Partie Hôte ]
```
- **Masque de sous-réseau** : sépare réseau/hôte
- **Adresse réseau** : tous les bits hôte = 0 (non assignable)
- **Adresse broadcast** : tous les bits hôte = 1 (non assignable)
- **Formule hôtes utilisables** : `2^n - 2` (n = bits hôte)

---

## 📋 Classes d'adresses (système obsolète mais utile)

| Classe | Premier octet | Masque | Plage | Hôtes/réseau |
|--------|---------------|--------|-------|--------------|
| **A** | 1-126 | /8 | 1.0.0.0 - 126.255.255.255 | 16M |
| **B** | 128-191 | /16 | 128.0.0.0 - 191.255.255.255 | 65K |
| **C** | 192-223 | /24 | 192.0.0.0 - 223.255.255.255 | 254 |
| **D** | 224-239 | N/A | Multicast | N/A |
| **E** | 240-255 | N/A | Expérimental | N/A |

---

## 📋 Adresses privées (RFC 1918)

| Classe | Plage privée | Masque par défaut |
|--------|--------------|-------------------|
| **A** | 10.0.0.0 - 10.255.255.255 | /8 |
| **B** | 172.16.0.0 - 172.31.255.255 | /12 |
| **C** | 192.168.0.0 - 192.168.255.255 | /16 |

**⚠️ Non routables sur Internet** → nécessitent NAT

---

## 📋 Adresses spéciales

| Adresse | Rôle |
|---------|------|
| **127.0.0.0/8** | Loopback (127.0.0.1 = localhost) |
| **169.254.0.0/16** | APIPA (auto-config quand pas de DHCP) |
| **0.0.0.0/0** | Route par défaut (toutes destinations) |
| **255.255.255.255** | Limited broadcast (ne traverse pas routeur) |

---

## 📋 CIDR - Notation et masques courants

| CIDR | Masque | Bits hôte | Hôtes utilisables |
|------|--------|-----------|-------------------|
| /24 | 255.255.255.0 | 8 | 254 |
| /25 | 255.255.255.128 | 7 | 126 |
| /26 | 255.255.255.192 | 6 | 62 |
| /27 | 255.255.255.224 | 5 | 30 |
| /28 | 255.255.255.240 | 4 | 14 |
| /29 | 255.255.255.248 | 3 | 6 |
| /30 | 255.255.255.252 | 2 | 2 (point-à-point) |

---

## ⚡ Formules de calcul essentielles

### Nombre de sous-réseaux
```
2^n    où n = nombre de bits empruntés
```

### Nombre d'hôtes par sous-réseau
```
2^h - 2    où h = nombre de bits hôte restants
-2 : exclut adresse réseau et broadcast
```

### Magic Number (méthode rapide)
```
Magic Number = 256 - valeur de l'octet du masque
```

**Exemple /26** :
- Masque : 255.255.255.**192**
- Magic Number : 256 - 192 = **64**
- Sous-réseaux : 0, 64, 128, 192

**Exemple /27** :
- Masque : 255.255.255.**224**
- Magic Number : 256 - 224 = **32**
- Sous-réseaux : 0, 32, 64, 96, 128, 160, 192, 224

---

## 📋 Tableau de subnetting rapide

| Bits empruntés | Masque (4e octet) | Sous-réseaux | Hôtes/sous-réseau | Magic Number |
|----------------|-------------------|--------------|-------------------|--------------|
| 1 | .128 | 2 | 126 | 128 |
| 2 | .192 | 4 | 62 | 64 |
| 3 | .224 | 8 | 30 | 32 |
| 4 | .240 | 16 | 14 | 16 |
| 5 | .248 | 32 | 6 | 8 |
| 6 | .252 | 64 | 2 | 4 |

---

## 🎯 Subnetting - Exemple complet

**Réseau** : 192.168.10.0/24 → Créer 4 sous-réseaux

**Solution** :
- Bits empruntés : 2 (car 2² = 4)
- Nouveau masque : /26 (255.255.255.192)
- Hôtes/sous-réseau : 2⁶ - 2 = 62

| Sous-réseau | Réseau | Première IP | Dernière IP | Broadcast |
|-------------|--------|-------------|-------------|-----------|
| 1 | .0/26 | .1 | .62 | .63 |
| 2 | .64/26 | .65 | .126 | .127 |
| 3 | .128/26 | .129 | .190 | .191 |
| 4 | .192/26 | .193 | .254 | .255 |

---

## 🎯 VLSM - Variable Length Subnet Masking

### Principe
Utiliser **différents masques** dans un même réseau pour optimiser l'allocation.

### Méthodologie
1. **Lister les besoins** (nombre d'hôtes par segment)
2. **Trier du plus grand au plus petit**
3. **Allouer séquentiellement** avec masques adaptés

### Exemple VLSM
**Réseau** : 192.168.1.0/24

| Segment | Besoin | Masque | Réseau alloué | Hôtes dispo |
|---------|--------|--------|---------------|-------------|
| A | 100 | /25 | 192.168.1.0/25 | 126 |
| B | 50 | /26 | 192.168.1.128/26 | 62 |
| C | 25 | /27 | 192.168.1.192/27 | 30 |
| Lien 1 | 2 | /30 | 192.168.1.224/30 | 2 |
| Lien 2 | 2 | /30 | 192.168.1.228/30 | 2 |

---

## 📋 Agrégation de routes (Route Summarization)

**Objectif** : Regrouper plusieurs réseaux en une seule route

**Exemple** :
```
Réseaux :
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24

→ Route agrégée : 192.168.0.0/22
```

---

## 💡 Points importants pour l'examen CCNA

### À mémoriser absolument
✅ **Formule hôtes** : 2^n - 2  
✅ **Adresses privées RFC 1918** : 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16  
✅ **Loopback** : 127.0.0.1  
✅ **APIPA** : 169.254.0.0/16  
✅ **Magic Number** : 256 - valeur masque  
✅ **Classes** : A (1-126), B (128-191), C (192-223), D (multicast), E (expérimental)

### Pièges à éviter
⚠️ Ne pas oublier le **-2** dans les calculs d'hôtes (réseau + broadcast exclus)  
⚠️ Vérifier que la plage d'adresses est **cohérente** avec le masque  
⚠️ VLSM : toujours **trier par taille décroissante** avant allocation  
⚠️ **0.0.0.0** = route par défaut (pas d'hôte)  
⚠️ Multicast = plage **224.0.0.0 à 239.255.255.255**

### Protocoles de routage supportant VLSM
✅ RIPv2, OSPF, EIGRP, IS-IS, BGP  
❌ RIPv1 (ne supporte pas VLSM)

### Compétences pratiques
✅ Calculer rapidement le nombre de sous-réseaux et d'hôtes  
✅ Identifier la classe d'une adresse  
✅ Déterminer si une adresse est publique ou privée  
✅ Appliquer VLSM selon les besoins réels  
✅ Créer un plan d'adressage structuré et évolutif

---

## 🔑 Checklist de révision

- [ ] Je connais les 3 types d'adresses IPv4 (unicast, broadcast, multicast)
- [ ] Je sais calculer le nombre d'hôtes avec 2^n - 2
- [ ] Je connais les plages d'adresses privées RFC 1918
- [ ] Je maîtrise le calcul avec le Magic Number
- [ ] Je sais créer un plan VLSM optimisé
- [ ] Je connais les adresses spéciales (loopback, APIPA, broadcast)
- [ ] Je sais identifier la classe d'une adresse
- [ ] Je comprends le principe d'agrégation de routes

---

**Durée de révision recommandée** : 30-45 minutes  
**Prochaine étape** : Module 12 - Adressage IPv6
