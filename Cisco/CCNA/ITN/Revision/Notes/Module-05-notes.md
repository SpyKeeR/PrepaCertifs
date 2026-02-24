# Module 05 : Systèmes numériques
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module couvre les systèmes de numération utilisés en réseau : binaire et hexadécimal.

**Durée estimée :** 3-4 heures  
**Objectifs :** Maîtriser la conversion binaire, décimal et hexadécimal

---

## 5.1 Système binaire

### Base 2 (Binaire)
- **Système binaire** : Utilise seulement deux chiffres (**0** et **1**)
- **Bit** : Binary Digit (unité de base)
- **Octet (Byte)** : 8 bits

### Représentation décimale vs binaire

Un nombre décimal peut être représenté comme une somme de puissances de 10 :
```
1234 = (1 × 10³) + (2 × 10²) + (3 × 10¹) + (4 × 10⁰)
     = 1000 + 200 + 30 + 4
```

Un nombre binaire est une somme de puissances de 2 :
```
1011 = (1 × 2³) + (0 × 2²) + (1 × 2¹) + (1 × 2⁰)
     = 8 + 0 + 2 + 1
     = 11 (décimal)
```

### Puissances de 2

| Puissance | Valeur | Mémoire |
|-----------|--------|---------|
| 2⁰ | 1 | |
| 2¹ | 2 | |
| 2² | 4 | |
| 2³ | 8 | |
| 2⁴ | 16 | |
| 2⁵ | 32 | |
| 2⁶ | 64 | |
| 2⁷ | 128 | |
| 2⁸ | 256 | Important pour les octets (1 octet = 2⁸ valeurs) |
| 2¹⁰ | 1024 | 1 Ko (Kilooctet) |
| 2¹⁶ | 65536 | 64 Ko |
| 2²⁰ | 1048576 | 1 Mo (Mégaoctet) |
| 2³⁰ | 1073741824 | 1 Go (Gigaoctet) |

**⚠️ Retenir pour CCNA :**
- **2⁸ = 256** : Nombre de valeurs dans un octet (0-255)
- **2¹⁰ = 1024** : 1 Kilooctet

### Conversion binaire → décimal

**Méthode des positions :**

Un octet a 8 bits avec ces valeurs de position :

| Position | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|----------|---|---|---|---|---|---|---|---|
| Valeur | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

**Exemple 1 :** Convertir **11010110** en décimal
```
  1    1    0    1    0    1    1    0
128 + 64 + 0 + 16 + 0 + 4 + 2 + 0 = 214
```

**Exemple 2 :** Convertir **10101010** en décimal
```
  1    0    1    0    1    0    1    0
128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170
```

**Exemple 3 :** Convertir **11111111** en décimal
```
128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255
```
(C'est la valeur maximale d'un octet)

### Conversion décimal → binaire

**Méthode de soustraction :**

Pour convertir 172 en binaire :

| Position | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|----------|-----|----|----|----|----|---|---|---|
| **Bit** | **1** | **0** | **1** | **0** | **1** | **1** | **0** | **0** |

**Étapes :**
1. 172 ≥ 128 ? Oui → Bit = 1, reste = 172 - 128 = 44
2. 44 ≥ 64 ? Non → Bit = 0
3. 44 ≥ 32 ? Oui → Bit = 1, reste = 44 - 32 = 12
4. 12 ≥ 16 ? Non → Bit = 0
5. 12 ≥ 8 ? Oui → Bit = 1, reste = 12 - 8 = 4
6. 4 ≥ 4 ? Oui → Bit = 1, reste = 4 - 4 = 0
7. 0 ≥ 2 ? Non → Bit = 0
8. 0 ≥ 1 ? Non → Bit = 0

**Résultat : 172 = 10101100**

**Autre méthode : Division par 2**
```
172 ÷ 2 = 86 reste 0
86 ÷ 2 = 43 reste 0
43 ÷ 2 = 21 reste 1
21 ÷ 2 = 10 reste 1
10 ÷ 2 = 5 reste 0
5 ÷ 2 = 2 reste 1
2 ÷ 2 = 1 reste 0
1 ÷ 2 = 0 reste 1

Lire de bas en haut : 10101100
```

### Adresse IPv4 en binaire

Une adresse IPv4 est composée de **4 octets** (32 bits).

**Exemple :** 192.168.1.10

| Décimal | 192 | 168 | 1 | 10 |
|---------|-----|-----|----|-----|
| **Binaire** | **11000000** | **10101000** | **00000001** | **00001010** |

**Notation complète :**
```
192.168.1.10 = 11000000.10101000.00000001.00001010
```

**⚠️ Importance :** Conversion binaire essentielle pour :
- Calculs de sous-réseaux (subnetting)
- Masques de sous-réseau
- Wildcard masks (ACL)

---

## 5.2 Système hexadécimal

### Base 16 (Hexadécimal)
- **Système hexadécimal** : Utilise 16 symboles (0-9 et A-F)
- **Préfixe** : 0x (exemple : 0x1A)
- **Usage** : Adresses MAC, IPv6, représentation compacte de binaire

### Correspondance

| Décimal | Binaire | Hexadécimal |
|---------|---------|-------------|
| 0 | 0000 | 0 |
| 1 | 0001 | 1 |
| 2 | 0010 | 2 |
| 3 | 0011 | 3 |
| 4 | 0100 | 4 |
| 5 | 0101 | 5 |
| 6 | 0110 | 6 |
| 7 | 0111 | 7 |
| 8 | 1000 | 8 |
| 9 | 1001 | 9 |
| 10 | 1010 | A |
| 11 | 1011 | B |
| 12 | 1100 | C |
| 13 | 1101 | D |
| 14 | 1110 | E |
| 15 | 1111 | F |

**⚠️ Point clé :** 1 chiffre hexadécimal = 4 bits (nibble)

### Conversion hexadécimal → décimal

**Exemple :** Convertir 0x2A en décimal
```
2A (hex) = (2 × 16¹) + (10 × 16⁰)
         = 32 + 10
         = 42 (décimal)
```

**Exemple :** Convertir 0xFF en décimal
```
FF (hex) = (15 × 16¹) + (15 × 16⁰)
         = 240 + 15
         = 255 (décimal)
```

### Conversion décimal → hexadécimal

**Exemple :** Convertir 172 en hexadécimal

**Méthode division par 16 :**
```
172 ÷ 16 = 10 reste 12
10 ÷ 16 = 0 reste 10

Reste 10 = A (hex)
Reste 12 = C (hex)

Lire de bas en haut : AC
```

**Résultat : 172 = 0xAC**

### Conversion binaire ↔ hexadécimal

**Binaire → Hexadécimal :**

Grouper les bits par 4 et convertir chaque groupe.

**Exemple :** 11010110
```
Grouper : 1101 | 0110
Convertir : D  |  6
Résultat : 0xD6
```

**Exemple :** 10101100 (172 en binaire)
```
Grouper : 1010 | 1100
Convertir :  A  |  C
Résultat : 0xAC
```

**Hexadécimal → Binaire :**

Convertir chaque chiffre hexa en 4 bits.

**Exemple :** 0x2F
```
2 = 0010
F = 1111
Résultat : 00101111
```

### Adresses MAC en hexadécimal

Une adresse MAC est représentée en **hexadécimal** (48 bits = 12 chiffres hex).

**Format :** XX:XX:XX:XX:XX:XX ou XX-XX-XX-XX-XX-XX

**Exemple :** `00:1A:2B:3C:4D:5E`

**En binaire :**
```
00000000:00011010:00101011:00111100:01001101:01011110
```

### Adresses IPv6 en hexadécimal

IPv6 utilise des adresses de **128 bits** représentées en hexadécimal.

**Format :** 8 groupes de 4 chiffres hexadécimaux séparés par `:`

**Exemple :** `2001:0DB8:85A3:0000:0000:8A2E:0370:7334`

**Simplification :**
- Zéros de tête omis : `2001:DB8:85A3:0:0:8A2E:370:7334`
- Séquence de zéros remplacée par `::` (une seule fois) : `2001:DB8:85A3::8A2E:370:7334`

---

## 💡 Points clés à retenir

### Conversions importantes

| Décimal | Binaire | Hexadécimal |
|---------|---------|-------------|
| 0 | 00000000 | 0x00 |
| 128 | 10000000 | 0x80 |
| 192 | 11000000 | 0xC0 |
| 224 | 11100000 | 0xE0 |
| 240 | 11110000 | 0xF0 |
| 248 | 11111000 | 0xF8 |
| 252 | 11111100 | 0xFC |
| 254 | 11111110 | 0xFE |
| 255 | 11111111 | 0xFF |

**⚠️ Valeurs à mémoriser (masques de sous-réseau) :**
- **255** = 11111111 = 0xFF
- **254** = 11111110 = 0xFE
- **252** = 11111100 = 0xFC
- **248** = 11111000 = 0xF8
- **240** = 11110000 = 0xF0
- **224** = 11100000 = 0xE0
- **192** = 11000000 = 0xC0
- **128** = 10000000 = 0x80
- **0** = 00000000 = 0x00

### Usages en réseau

1. **Binaire** :
   - Calculs de sous-réseaux
   - Masques de sous-réseau
   - Adresses IP
   - ACL (wildcard masks)

2. **Hexadécimal** :
   - Adresses MAC
   - Adresses IPv6
   - Représentation compacte

---

## 📝 Exercices pratiques

### Conversions binaire → décimal
1. 11000000 = ?
2. 10101010 = ?
3. 11111000 = ?

**Réponses :**
1. 192
2. 170
3. 248

### Conversions décimal → binaire
1. 224 = ?
2. 254 = ?
3. 168 = ?

**Réponses :**
1. 11100000
2. 11111110
3. 10101000

### Conversions hexadécimal → décimal
1. 0xFF = ?
2. 0xC0 = ?
3. 0x10 = ?

**Réponses :**
1. 255
2. 192
3. 16

### Adresse IPv4 en binaire
Convertir 172.16.30.1 en binaire

**Réponse :**
```
172 = 10101100
16  = 00010000
30  = 00011110
1   = 00000001

Résultat : 10101100.00010000.00011110.00000001
```

---

## 🔗 Outils en ligne

Calcul

ateurs de conversion :
- [Rapid Tables](https://www.rapidtables.com/convert/number/binary-to-decimal.html)
- [Binary Hex Converter](https://www.binaryhexconverter.com/)
- Calculatrices Windows, macOS (mode programmeur)

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
