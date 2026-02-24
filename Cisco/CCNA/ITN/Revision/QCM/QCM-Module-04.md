# QCM - Module 04 : Couche physique
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **17 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Quelle couche du modèle OSI est responsable de la transmission des bits sur le média physique ?

- [ ] A. Couche 1 - Physique
- [ ] B. Couche 2 - Liaison de données
- [ ] C. Couche 3 - Réseau
- [ ] D. Couche 4 - Transport

### Question 2
Quels sont les types d'interférences qui peuvent affecter les câbles en cuivre ?

- [ ] A. EMI (Electromagnetic Interference)
- [ ] B. RFI (Radio Frequency Interference)
- [ ] C. Diaphonie (Crosstalk)
- [ ] D. Atténuation lumineuse

### Question 3
Quel est le type de câble réseau le plus couramment utilisé dans les LAN modernes ?

- [ ] A. Câble coaxial
- [ ] B. UTP (Unshielded Twisted Pair)
- [ ] C. STP (Shielded Twisted Pair)
- [ ] D. Fibre optique multimode

### Question 4
Quelle est la distance maximale recommandée pour un câble UTP Ethernet entre deux équipements actifs ?

- [ ] A. 50 mètres
- [ ] B. 100 mètres
- [ ] C. 185 mètres
- [ ] D. 500 mètres

### Question 5
Quelle catégorie de câble UTP est recommandée pour Gigabit Ethernet (1000BASE-T) ?

- [ ] A. Cat 3
- [ ] B. Cat 5
- [ ] C. Cat 5e
- [ ] D. Cat 6

### Question 6
Quel type de câble Ethernet est utilisé pour connecter directement deux PC entre eux ?

- [ ] A. Câble droit (Straight-through)
- [ ] B. Câble croisé (Crossover)
- [ ] C. Câble console
- [ ] D. Câble rollover

### Question 7
Quel connecteur est utilisé pour les câbles Ethernet UTP ?

- [ ] A. RJ-11
- [ ] B. RJ-45
- [ ] C. DB-9
- [ ] D. LC

### Question 8
Combien de paires de fils torsadés contient un câble Ethernet UTP standard ?

- [ ] A. 2 paires
- [ ] B. 4 paires
- [ ] C. 6 paires
- [ ] D. 8 paires

### Question 9
Dans un câble droit (straight-through), quels standards de câblage sont utilisés ?

- [ ] A. T568A des deux côtés
- [ ] B. T568B des deux côtés
- [ ] C. T568A d'un côté, T568B de l'autre
- [ ] D. Aucune norme spécifique

### Question 10
Quels avantages offre la fibre optique par rapport au câble cuivre ?

- [ ] A. Immunité aux interférences électromagnétiques
- [ ] B. Plus grande bande passante
- [ ] C. Distance de transmission plus longue
- [ ] D. Coût inférieur

### Question 11
Quelle est la différence entre la bande passante et le débit (throughput) ?

- [ ] A. La bande passante est la capacité théorique, le débit est la mesure réelle
- [ ] B. Ils sont identiques
- [ ] C. Le débit est toujours supérieur à la bande passante
- [ ] D. La bande passante concerne seulement la fibre optique

### Question 12
Quel type de fibre optique est utilisé pour les longues distances (plusieurs kilomètres) ?

- [ ] A. Fibre multimode
- [ ] B. Fibre monomode
- [ ] C. Fibre Cat 6
- [ ] D. Fibre UTP

### Question 13
Quelle caractéristique du câble Cat 6a lui permet de supporter 10 Gigabit Ethernet sur 100 mètres ?

- [ ] A. Plus de blindage et meilleure torsade des paires
- [ ] B. Utilisation de cuivre pur
- [ ] C. Connecteurs dorés
- [ ] D. Isolation en téflon

### Question 14
Qu'est-ce que l'atténuation dans un câble réseau ?

- [ ] A. L'augmentation du signal sur la distance
- [ ] B. La perte de signal sur la distance
- [ ] C. Le chiffrement du signal
- [ ] D. La compression des données

### Question 15
Quelle technologie moderne permet aux équipements réseau de détecter automatiquement s'ils ont besoin d'un câble droit ou croisé ?

- [ ] A. QoS (Quality of Service)
- [ ] B. Auto-MDIX
- [ ] C. PoE (Power over Ethernet)
- [ ] D. VLAN

### Question 16
Dans un câble croisé (crossover), quelles broches sont inversées ?

- [ ] A. 1-2 avec 3-6
- [ ] B. 1-3 avec 2-6
- [ ] C. Toutes les broches
- [ ] D. Aucune broche

### Question 17
Quelle unité mesure la bande passante d'un réseau ?

- [ ] A. Hertz (Hz)
- [ ] B. Bits par seconde (bps)
- [ ] C. Ohms (Ω)
- [ ] D. Décibels (dB)

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : A**

**Explication :**
La **Couche 1 - Physique** est responsable de la transmission des bits (0 et 1) sur le média physique. Elle définit les spécifications électriques, mécaniques et procédurales pour la transmission des signaux.

**💡 Point clé :** La couche Physique convertit les trames numériques de la couche 2 en signaux physiques (tension électrique, lumière, ondes radio) adaptés au média utilisé.

---

## Question 2
**Réponses correctes : A, B, C**

**Explication :**
Les câbles en cuivre sont sensibles à :
- **EMI (A)** : Interférences électromagnétiques (moteurs, lignes électriques)
- **RFI (B)** : Interférences radio (émetteurs, micro-ondes)
- **Diaphonie (C)** : Interférences entre fils voisins dans le même câble

L'atténuation lumineuse (D) concerne la fibre optique, pas le cuivre.

**💡 Point clé :** Pour réduire ces interférences : utiliser des paires torsadées (annule les interférences), du blindage (STP), respecter les distances maximales, éviter le passage près de sources électriques.

---

## Question 3
**Réponse correcte : B**

**Explication :**
Le câble **UTP (Unshielded Twisted Pair)** est le plus couramment utilisé dans les LAN modernes (Cat 5e, Cat 6). Il offre un bon rapport coût/performance et est facile à installer.

**💡 Point clé :** Le câble UTP utilise des paires de fils torsadés pour annuler les interférences externes. Plus la catégorie est élevée, plus les torsades sont serrées et meilleures sont les performances.

---

## Question 4
**Réponse correcte : B**

**Explication :**
La distance maximale pour un câble UTP Ethernet est de **100 mètres** entre deux équipements actifs (ex: PC vers switch, switch vers switch). Au-delà, l'atténuation du signal devient trop importante.

**💡 Point clé :** Cette limite de 100m est valable pour les standards Ethernet sur cuivre (10/100/1000BASE-T). Pour dépasser cette distance, utilisez de la fibre optique, des répéteurs, ou des switches intermédiaires.

---

## Question 5
**Réponses correctes : C, D**

**Explication :**
Pour Gigabit Ethernet (1000BASE-T), on recommande au minimum du **Cat 5e** (C) ou mieux, du **Cat 6** (D). Le Cat 3 et Cat 5 ne supportent que 10/100 Mbps.

**💡 Point clé :** 
- Cat 5e : 1 Gbps sur 100m
- Cat 6 : 10 Gbps sur 55m, 1 Gbps sur 100m
- Cat 6a : 10 Gbps sur 100m

---

## Question 6
**Réponse correcte : B**

**Explication :**
Un **câble croisé (Crossover)** est utilisé pour connecter deux équipements identiques : PC vers PC, switch vers switch, routeur vers routeur. Le câble droit connecte deux équipements différents.

**💡 Point clé :** Dans un câble croisé, les paires TX (transmission) et RX (réception) sont inversées : ce qui transmet d'un côté reçoit de l'autre. Avec Auto-MDIX moderne, les équipements détectent automatiquement et s'adaptent.

---

## Question 7
**Réponse correcte : B**

**Explication :**
Le connecteur **RJ-45** (8 broches) est utilisé pour les câbles Ethernet UTP. RJ-11 est pour le téléphone (4-6 broches), DB-9 pour le port série/console, et LC pour la fibre optique.

**💡 Point clé :** RJ signifie "Registered Jack". Le RJ-45 ressemble à un RJ-11 de téléphone mais est plus large. Ne forcez jamais un RJ-11 dans un port RJ-45 !

---

## Question 8
**Réponse correcte : B**

**Explication :**
Un câble Ethernet UTP standard contient **4 paires** de fils torsadés, soit 8 fils au total. Les paires sont de couleurs différentes : orange, vert, bleu, brun (+ blanc-rayé).

**💡 Point clé :** Pour 100BASE-TX (Fast Ethernet), seules 2 paires sont utilisées (orange et vert). Pour 1000BASE-T (Gigabit), les 4 paires sont utilisées simultanément pour augmenter le débit.

---

## Question 9
**Réponses correctes : A, B**

**Explication :**
Dans un câble droit, on utilise le **même standard des deux côtés** : soit T568A des deux côtés (A), soit T568B des deux côtés (B). Le standard T568B est plus courant en Amérique du Nord.

**💡 Point clé :** T568A d'un côté et T568B de l'autre (C) définit un câble croisé, pas un câble droit. Les deux standards diffèrent par l'ordre des paires orange et verte.

---

## Question 10
**Réponses correctes : A, B, C**

**Explication :**
La fibre optique offre :
- **Immunité aux EMI/RFI (A)** : Utilise la lumière, pas l'électricité
- **Plus grande bande passante (B)** : 10/40/100 Gbps et plus
- **Distance plus longue (C)** : Plusieurs kilomètres sans régénération

Le coût (D) est généralement plus élevé que le cuivre, pas inférieur.

**💡 Point clé :** La fibre est idéale pour les backbones de campus, les liaisons inter-bâtiments, et les datacenters. Le cuivre reste plus économique pour les connexions d'utilisateurs finaux.

---

## Question 11
**Réponse correcte : A**

**Explication :**
La **bande passante** est la capacité théorique maximale du média (ex: 1 Gbps), tandis que le **débit (throughput)** est la bande passante réelle mesurée, généralement inférieure en raison de l'overhead, la congestion, etc.

**💡 Point clé :** Le **goodput** est encore plus précis : c'est le débit utile (données applicatives uniquement, sans les en-têtes des protocoles). Bande passante > Débit > Goodput.

---

## Question 12
**Réponse correcte : B**

**Explication :**
La **fibre monomode** (single-mode) est utilisée pour les longues distances (plusieurs kilomètres à dizaines de kilomètres). Elle a un cœur plus fin et utilise un laser. La fibre multimode (multi-mode) est pour les courtes distances (jusqu'à 550m).

**💡 Point clé :** 
- Monomode : Cœur ~9 µm, laser, longue distance, plus cher
- Multimode : Cœur ~50-62.5 µm, LED, courte distance, moins cher

---

## Question 13
**Réponse correcte : A**

**Explication :**
Le Cat 6a améliore le blindage et la torsade des paires pour réduire la diaphonie et les interférences, permettant ainsi 10 Gigabit Ethernet sur toute la distance de 100 mètres (contrairement au Cat 6 limité à 55m pour 10G).

**💡 Point clé :** Le "a" dans Cat 6a signifie "augmented" (amélioré). Il utilise un blindage supplémentaire et des séparateurs physiques entre les paires pour réduire la diaphonie interne (alien crosstalk).

---

## Question 14
**Réponse correcte : B**

**Explication :**
L'**atténuation** est la perte de signal (affaiblissement) sur la distance. Plus le câble est long, plus l'atténuation est importante, jusqu'à rendre le signal illisible.

**💡 Point clé :** L'atténuation se mesure en décibels (dB). C'est pourquoi il y a des distances maximales pour chaque type de câble : au-delà, l'atténuation est trop forte et il faut régénérer le signal avec un équipement actif.

---

## Question 15
**Réponse correcte : B**

**Explication :**
**Auto-MDIX** (Automatic Medium-Dependent Interface Crossover) permet aux équipements modernes de détecter automatiquement le type de câble (droit ou croisé) et d'ajuster leurs interfaces en conséquence.

**💡 Point clé :** Avec Auto-MDIX, vous pouvez utiliser n'importe quel câble (droit ou croisé) et l'équipement s'adaptera. Cette fonctionnalité est présente sur la plupart des switches et cartes réseau modernes.

---

## Question 16
**Réponse correcte : A**

**Explication :**
Dans un câble croisé, les broches **1-2 sont inversées avec 3-6** :
- Broche 1 ↔ Broche 3
- Broche 2 ↔ Broche 6

Cela permet d'inverser les paires TX et RX.

**💡 Point clé :** Plus précisément, dans un câble croisé standard :
- T568A d'un côté : 1=V/B, 2=V, 3=O/B, 6=O
- T568B de l'autre : 1=O/B, 2=O, 3=V/B, 6=V
(V=Vert, O=Orange, B=Blanc)

---

## Question 17
**Réponse correcte : B**

**Explication :**
La bande passante se mesure en **bits par seconde (bps)** et ses multiples : Kbps, Mbps, Gbps, Tbps. Les Hertz mesurent la fréquence, les Ohms la résistance, et les décibels l'atténuation.

**💡 Point clé :** 
- 1 Kbps = 1 000 bps
- 1 Mbps = 1 000 000 bps
- 1 Gbps = 1 000 000 000 bps

Attention : 1 Mégaoctet (MB) = 8 Mégabits (Mb)

---

**Score recommandé pour valider le module : 13/17 minimum (76%)**

**Révision conseillée si score < 13/17 :**
- Section 4.3 (Câblage en cuivre)
- Section 4.4 (Câblage UTP - catégories et types)
- Section 4.5 (Câblage à fibre optique)
- Manipuler des câbles réels ou dans Packet Tracer
