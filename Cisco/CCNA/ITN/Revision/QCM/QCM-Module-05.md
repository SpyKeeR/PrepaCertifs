# QCM - Module 05 : Systèmes numériques
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **20 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Combien de valeurs différentes peut contenir un octet (8 bits) ?

- [ ] A. 128
- [ ] B. 255
- [ ] C. 256
- [ ] D. 512

### Question 2
Quelle est la valeur de 2⁸ (utilisée fréquemment en réseau) ?

- [ ] A. 128
- [ ] B. 256
- [ ] C. 512
- [ ] D. 1024

### Question 3
Convertir le nombre binaire 11111111 en décimal.

- [ ] A. 127
- [ ] B. 255
- [ ] C. 256
- [ ] D. 511

### Question 4
Convertir le nombre décimal 192 en binaire.

- [ ] A. 11000000
- [ ] B. 10100000
- [ ] C. 11110000
- [ ] D. 10101100

### Question 5
Dans un nombre binaire à 8 bits (octet), quelle est la valeur de position du bit de poids fort (le plus à gauche) ?

- [ ] A. 64
- [ ] B. 128
- [ ] C. 256
- [ ] D. 512

### Question 6
Convertir le nombre décimal 254 en binaire.

- [ ] A. 11111110
- [ ] B. 11111111
- [ ] C. 11111100
- [ ] D. 11110000

### Question 7
Convertir le nombre binaire 10101010 en décimal.

- [ ] A. 85
- [ ] B. 170
- [ ] C. 171
- [ ] D. 255

### Question 8
Quelle base numérique utilise le système hexadécimal ?

- [ ] A. Base 2
- [ ] B. Base 8
- [ ] C. Base 10
- [ ] D. Base 16

### Question 9
Combien de bits représente un chiffre hexadécimal ?

- [ ] A. 2 bits
- [ ] B. 4 bits (1 nibble)
- [ ] C. 8 bits (1 octet)
- [ ] D. 16 bits

### Question 10
Convertir le nombre hexadécimal 0xFF en décimal.

- [ ] A. 15
- [ ] B. 127
- [ ] C. 255
- [ ] D. 256

### Question 11
Convertir le nombre hexadécimal 0xC0 en décimal.

- [ ] A. 128
- [ ] B. 192
- [ ] C. 200
- [ ] D. 255

### Question 12
Quelle est la représentation hexadécimale du nombre décimal 10 ?

- [ ] A. 0x0A
- [ ] B. 0x10
- [ ] C. 0xA0
- [ ] D. 0x10A

### Question 13
Convertir le nombre binaire 11010110 en hexadécimal.

- [ ] A. 0xD6
- [ ] B. 0x6D
- [ ] C. 0xDB
- [ ] D. 0xC6

### Question 14
Dans une adresse IPv4, combien d'octets sont utilisés ?

- [ ] A. 2 octets (16 bits)
- [ ] B. 4 octets (32 bits)
- [ ] C. 6 octets (48 bits)
- [ ] D. 8 octets (64 bits)

### Question 15
Convertir l'adresse IP 192.168.1.1 en binaire (premier octet seulement : 192).

- [ ] A. 10000000
- [ ] B. 11000000
- [ ] C. 11100000
- [ ] D. 11110000

### Question 16
Quelle est la valeur maximale qu'un octet peut contenir ?

- [ ] A. 127
- [ ] B. 128
- [ ] C. 255
- [ ] D. 256

### Question 17
Combien de chiffres hexadécimaux sont nécessaires pour représenter une adresse MAC (48 bits) ?

- [ ] A. 6 chiffres
- [ ] B. 8 chiffres
- [ ] C. 12 chiffres
- [ ] D. 16 chiffres

### Question 18
Convertir le nombre binaire 11111000 en décimal.

- [ ] A. 240
- [ ] B. 248
- [ ] C. 252
- [ ] D. 254

### Question 19
Dans le système hexadécimal, que représente la lettre "F" ?

- [ ] A. 10
- [ ] B. 12
- [ ] C. 14
- [ ] D. 15

### Question 20
Convertir le nombre décimal 172 en binaire.

- [ ] A. 10101100
- [ ] B. 10101010
- [ ] C. 11010100
- [ ] D. 10110100

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : C**

**Explication :**
Un octet (8 bits) peut contenir **256 valeurs différentes** (de 0 à 255). Le calcul est 2⁸ = 256.

**💡 Point clé :** Les valeurs vont de 0 (00000000) à 255 (11111111), soit 256 valeurs au total. C'est pourquoi chaque octet d'une adresse IPv4 peut aller de 0 à 255.

---

## Question 2
**Réponse correcte : B**

**Explication :**
2⁸ = 256. Cette valeur est fondamentale en réseautique car elle représente le nombre de valeurs dans un octet.

**💡 Point clé :** Valeurs importantes à mémoriser :
- 2⁸ = 256 (octet)
- 2¹⁰ = 1024 (kilo)
- 2¹⁶ = 65536 (16 bits)
- 2³² = 4,3 milliards (adresses IPv4)

---

## Question 3
**Réponse correcte : B**

**Explication :**
```
11111111 = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255
```
C'est la valeur maximale d'un octet.

**💡 Point clé :** 11111111 (tous les bits à 1) = 255. Cette valeur apparaît fréquemment dans les masques de sous-réseau et les adresses broadcast.

---

## Question 4
**Réponse correcte : A**

**Explication :**
```
192 en binaire :
192 ≥ 128 ? Oui → 1, reste = 64
64 ≥ 64 ? Oui → 1, reste = 0
Tous les autres bits = 0
Résultat : 11000000
```

**💡 Point clé :** 192 (11000000) est très courant en réseau, notamment dans les masques de sous-réseau de classe C (255.255.255.0) et les adresses privées (192.168.x.x).

---

## Question 5
**Réponse correcte : B**

**Explication :**
Dans un octet (8 bits), le bit de poids fort (Most Significant Bit - MSB) est en position 7, avec une valeur de 2⁷ = **128**.

**💡 Point clé :** Positions des bits dans un octet (de gauche à droite) :
```
Bit :    7   6   5   4   3   2   1   0
Valeur: 128  64  32  16  8   4   2   1
```

---

## Question 6
**Réponse correcte : A**

**Explication :**
```
254 en binaire :
254 = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 0
    = 11111110
```
Tous les bits à 1 sauf le dernier.

**💡 Point clé :** 254 (11111110) est utilisé dans les masques de sous-réseau pour créer des réseaux de 2 hôtes. Il apparaît aussi souvent comme adresse de passerelle par défaut.

---

## Question 7
**Réponse correcte : B**

**Explication :**
```
10101010 = 128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170
```

**💡 Point clé :** 10101010 (170) est un pattern de bits alternés, facile à reconnaître. Il correspond à 0xAA en hexadécimal.

---

## Question 8
**Réponse correcte : D**

**Explication :**
Le système hexadécimal utilise la **base 16**, avec 16 symboles : 0-9 et A-F (où A=10, B=11, C=12, D=13, E=14, F=15).

**💡 Point clé :** Le préfixe commun pour indiquer un nombre hexadécimal est "0x". Exemple : 0xFF, 0x1A2B.

---

## Question 9
**Réponse correcte : B**

**Explication :**
Un chiffre hexadécimal représente **4 bits** (appelé aussi un "nibble" ou "quartet"). Puisque 2⁴ = 16, un chiffre hexa peut représenter 16 valeurs (0-F).

**💡 Point clé :** Cette correspondance 1:4 (1 chiffre hexa = 4 bits) est très pratique :
- 2 chiffres hexa = 1 octet (8 bits)
- 12 chiffres hexa = adresse MAC (48 bits)
- 32 chiffres hexa = adresse IPv6 (128 bits)

---

## Question 10
**Réponse correcte : C**

**Explication :**
```
0xFF = (F × 16¹) + (F × 16⁰)
     = (15 × 16) + (15 × 1)
     = 240 + 15
     = 255
```

**💡 Point clé :** 0xFF (255) est la valeur maximale d'un octet. En binaire : 11111111. Très utilisé dans les masques de sous-réseau et les adresses broadcast.

---

## Question 11
**Réponse correcte : B**

**Explication :**
```
0xC0 = (C × 16¹) + (0 × 16⁰)
     = (12 × 16) + 0
     = 192
```

**💡 Point clé :** C en hexadécimal = 12 en décimal. 0xC0 = 192, une valeur courante dans les adresses privées de classe C (192.168.x.x).

---

## Question 12
**Réponse correcte : A**

**Explication :**
Le nombre décimal 10 correspond à la lettre A en hexadécimal, d'où **0x0A** (ou simplement 0xA).

**💡 Point clé :** En hexadécimal :
- A = 10
- B = 11
- C = 12
- D = 13
- E = 14
- F = 15

---

## Question 13
**Réponse correcte : A**

**Explication :**
```
Grouper par 4 bits : 1101 | 0110
Convertir en hexa : D | 6
Résultat : 0xD6
```

**💡 Point clé :** Pour convertir binaire → hexa : grouper par 4 bits et convertir chaque groupe. Pour hexa → binaire : convertir chaque chiffre hexa en 4 bits.

---

## Question 14
**Réponse correcte : B**

**Explication :**
Une adresse IPv4 utilise **4 octets (32 bits)**, d'où le format X.X.X.X où chaque X va de 0 à 255.

**💡 Point clé :** 32 bits = 2³² ≈ 4,3 milliards d'adresses possibles. C'est insuffisant pour les besoins actuels, d'où la transition vers IPv6 (128 bits).

---

## Question 15
**Réponse correcte : B**

**Explication :**
```
192 = 128 + 64 + 0 + 0 + 0 + 0 + 0 + 0
    = 11000000
```

**💡 Point clé :** L'adresse complète 192.168.1.1 en binaire :
```
192.168.1.1 = 11000000.10101000.00000001.00000001
```

---

## Question 16
**Réponse correcte : C**

**Explication :**
La valeur maximale d'un octet est **255** (tous les bits à 1 : 11111111). Les valeurs vont de 0 à 255, soit 256 valeurs différentes.

**💡 Point clé :** Ne confondez pas :
- Valeur maximale : **255**
- Nombre de valeurs : **256** (de 0 à 255)

---

## Question 17
**Réponse correcte : C**

**Explication :**
Une adresse MAC a 48 bits. Puisque 1 chiffre hexa = 4 bits, il faut 48 ÷ 4 = **12 chiffres hexadécimaux**.

**💡 Point clé :** Format d'adresse MAC : XX:XX:XX:XX:XX:XX
- 6 groupes de 2 chiffres hexa
- Total : 12 chiffres hexa
- Exemple : 00:1A:2B:3C:4D:5E

---

## Question 18
**Réponse correcte : B**

**Explication :**
```
11111000 = 128 + 64 + 32 + 16 + 8 + 0 + 0 + 0 = 248
```

**💡 Point clé :** 248 (11111000) est un masque de sous-réseau courant. Il laisse 3 bits d'hôte (2³ - 2 = 6 hôtes utilisables).

---

## Question 19
**Réponse correcte : D**

**Explication :**
En hexadécimal, la lettre **F** représente la valeur décimale **15**. En binaire : 1111 (4 bits à 1).

**💡 Point clé :** Correspondances hexa-décimal à mémoriser :
- A = 10, B = 11, C = 12, D = 13, E = 14, F = 15

---

## Question 20
**Réponse correcte : A**

**Explication :**
```
172 en binaire :
172 = 128 + 44
44 = 32 + 12
12 = 8 + 4
Résultat : 10101100
```

**💡 Point clé :** 172 (10101100) est l'octet de départ des adresses privées de classe B (172.16.0.0 à 172.31.255.255). En hexadécimal : 0xAC.

---

**Score recommandé pour valider le module : 16/20 minimum (80%)**

**Révision conseillée si score < 16/20 :**
- Section 5.1 (Système binaire et conversions)
- Section 5.2 (Système hexadécimal)
- Pratiquer les conversions avec un calculateur
- Mémoriser les valeurs courantes (128, 192, 224, 240, 248, 252, 254, 255)

**💡 Astuce pratique :** Créez des flashcards (papier ou Anki) avec les conversions courantes pour les mémoriser.
