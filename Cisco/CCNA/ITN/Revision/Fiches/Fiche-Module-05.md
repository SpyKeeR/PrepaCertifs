# Fiche Module 05 : Systèmes numériques
**ITN - Introduction to Networks**

---

## 📋 Points clés

### Systèmes de numération en réseau
- **Binaire (Base 2)** : Représentation interne des données (0, 1)
- **Décimal (Base 10)** : Représentation humaine (0-9)
- **Hexadécimal (Base 16)** : Représentation compacte (0-9, A-F)

**Usages :**
- **Binaire** : Adresses IP, masques de sous-réseau, calculs réseau
- **Hexadécimal** : Adresses MAC, IPv6, couleurs RGB

---

## 📊 Système binaire (Base 2)

### Puissances de 2 (À mémoriser)

| Puissance | Valeur | Usage réseau |
|-----------|--------|--------------|
| 2⁰ | 1 | |
| 2¹ | 2 | |
| 2² | 4 | |
| 2³ | 8 | Nombre de valeurs (3 bits) |
| 2⁴ | 16 | |
| 2⁵ | 32 | CIDR /27 |
| 2⁶ | 64 | CIDR /26 |
| 2⁷ | 128 | CIDR /25 |
| **2⁸** | **256** | **Valeurs d'un octet (0-255)** |
| **2¹⁰** | **1024** | **1 Ko (Kilooctet)** |
| 2¹⁶ | 65536 | 64 Ko, plage de ports |
| 2²⁰ | 1048576 | 1 Mo (Mégaoctet) |
| 2³⁰ | 1073741824 | 1 Go (Gigaoctet) |

**⚠️ Essentiel pour CCNA :**
- **2⁸ = 256** : Nombre de valeurs dans un octet (0-255)
- **2¹⁰ = 1024** : 1 Kilooctet

---

## 📊 Conversion binaire → décimal

### Positions des bits dans un octet

| Position | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|----------|---|---|---|---|---|---|---|---|
| **Valeur** | **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |

**Méthode :** Additionner les valeurs des bits à 1

**Exemples :**

```
11010110 = 128 + 64 + 0 + 16 + 0 + 4 + 2 + 0 = 214

10101010 = 128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170

11111111 = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255 (valeur max)

00000000 = 0 (valeur min)
```

---

## 📊 Conversion décimal → binaire

### Méthode de soustraction

**Exemple : Convertir 172 en binaire**

| Position | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|----------|-----|----|----|----|----|---|---|---|
| **Bit** | **1** | **0** | **1** | **0** | **1** | **1** | **0** | **0** |

**Étapes :**
1. 172 ≥ 128 ? Oui → Bit = 1, reste = 44
2. 44 ≥ 64 ? Non → Bit = 0
3. 44 ≥ 32 ? Oui → Bit = 1, reste = 12
4. 12 ≥ 16 ? Non → Bit = 0
5. 12 ≥ 8 ? Oui → Bit = 1, reste = 4
6. 4 ≥ 4 ? Oui → Bit = 1, reste = 0
7. Reste = 0 → Bits restants = 0

**Résultat : 172 = 10101100**

---

## 📊 Adresses IPv4 en binaire

### Structure
- **4 octets** (32 bits au total)
- Chaque octet = 0 à 255 en décimal

**Exemple : 192.168.1.10**

| Décimal | 192 | 168 | 1 | 10 |
|---------|-----|-----|----|-----|
| **Binaire** | **11000000** | **10101000** | **00000001** | **00001010** |

**Notation complète :**
```
192.168.1.10 = 11000000.10101000.00000001.00001010
```

**Usage :** Calculs de sous-réseaux (subnetting), masques, wildcard masks (ACL)

---

## 📊 Système hexadécimal (Base 16)

### Table de conversion Hex ↔ Décimal ↔ Binaire

| Hex | Décimal | Binaire (4 bits) |
|-----|---------|------------------|
| **0** | 0 | 0000 |
| **1** | 1 | 0001 |
| **2** | 2 | 0010 |
| **3** | 3 | 0011 |
| **4** | 4 | 0100 |
| **5** | 5 | 0101 |
| **6** | 6 | 0110 |
| **7** | 7 | 0111 |
| **8** | 8 | 1000 |
| **9** | 9 | 1001 |
| **A** | 10 | 1010 |
| **B** | 11 | 1011 |
| **C** | 12 | 1100 |
| **D** | 13 | 1101 |
| **E** | 14 | 1110 |
| **F** | 15 | 1111 |

**Préfixe hexadécimal :** 0x (exemple : 0x1A)

---

## 📊 Conversions hexadécimales

### Hexadécimal → Décimal

**Exemple : 0x2F**
```
2F (hex) = (2 × 16¹) + (15 × 16⁰)
         = 32 + 15
         = 47 (décimal)
```

**Exemple : 0xA5**
```
A5 (hex) = (10 × 16¹) + (5 × 16⁰)
         = 160 + 5
         = 165 (décimal)
```

### Hexadécimal → Binaire

**Méthode :** Convertir chaque chiffre hex en 4 bits binaires

**Exemple : 0x3C**
```
3 (hex) = 0011 (binaire)
C (hex) = 1100 (binaire)

0x3C = 00111100 (binaire)
```

### Binaire → Hexadécimal

**Méthode :** Regrouper par 4 bits, convertir chaque groupe en hex

**Exemple : 10101110**
```
1010 = A (hex)
1110 = E (hex)

10101110 = 0xAE
```

---

## 📊 Adresses MAC en hexadécimal

**Format :** 48 bits (6 octets) en hexadécimal

**Exemple : 00:1A:2B:3C:4D:5E**

**Conversion en binaire :**
```
00 = 00000000
1A = 00011010
2B = 00101011
3C = 00111100
4D = 01001101
5E = 01011110

00:1A:2B:3C:4D:5E = 000000000001101000101011001111000100110101011110
```

---

## 💡 À retenir absolument

✅ **1 octet = 8 bits** = 256 valeurs possibles (0-255)  
✅ **2⁸ = 256** (valeur max d'un octet + 1)  
✅ **2¹⁰ = 1024** (1 Ko)  
✅ **Positions binaires** : 128, 64, 32, 16, 8, 4, 2, 1  
✅ **Adresse IPv4** = 4 octets (32 bits)  
✅ **Hexadécimal** : 0-9, A-F (A=10, B=11, C=12, D=13, E=14, F=15)  
✅ **1 chiffre hex** = 4 bits binaires  
✅ **Adresse MAC** = 6 octets (48 bits) en hexadécimal  
✅ **0xFF = 255** (tous les bits à 1 dans un octet)  
✅ **0x00 = 0** (tous les bits à 0)  

**Astuce de conversion rapide binaire → décimal :**  
Mémoriser : **128, 64, 32, 16, 8, 4, 2, 1**  
Additionner les valeurs correspondant aux bits à 1.
