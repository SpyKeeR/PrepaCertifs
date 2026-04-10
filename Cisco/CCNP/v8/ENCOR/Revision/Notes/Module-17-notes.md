# Module 17 : Signaux Wireless et Modulation
## Notes Complètes de Révision

---

## 1. THÉORIE WIRELESS DE BASE

### Signaux RF et Propagation

Les signaux wireless (radiofréquence) sont des ondes électromagnétiques se propageant à travers l'air. Contrairement à la propagation filaire où les électrons circulent physiquement dans un câble, les signaux RF créent des champs électriques ET magnétiques oscillants qui se propagent ensemble dans l'espace.

**La nature des champs RF:**
- Le champ électrique et le champ magnétique sont perpendiculaires l'un à l'autre
- Les deux champs oscillent perpendiculairement à la direction de propagation
- Les ondes se propagent sphériquement en 3 dimensions (pas en lignes droites)
- La vitesse de propagation est approximativement celle de la lumière (~300,000 km/s dans le vide, légèrement moins dans l'air)

### Fréquence et Spectre RF

**Fréquence:** Nombre de oscillations complètes du champ par seconde, mesuré en Hertz (Hz).

**Unités de fréquence:**
- 1 kHz = 1,000 Hz (kilohertz)
- 1 MHz = 1,000,000 Hz (mégahertz) = 1,000 kHz
- 1 GHz = 1,000,000,000 Hz (gigahertz) = 1,000 MHz
- 1 THz = 1,000 GHz (térahertz) – rayons X et gamma

**Spectre électromagnétique complet (0 Hz → 10^22 Hz):**

Le spectre s'étend de très basses fréquences (VLF, quelques Hz) jusqu'aux rayons cosmiques (10^22 Hz +). Certaines bandes importantes:

- **Fréquences audio inaudibles** : 0 Hz - 20 Hz (infrasons)
- **Fréquences audio humaines** : 20 Hz - 20,000 Hz (audible)
- **Radio VLF** : 3 kHz - 30 kHz (radio très longues ondes)
- **Radio LF** : 30 kHz - 300 kHz (radio longues ondes)
- **Radio MF** : 300 kHz - 3 MHz (radio AM 550-1700 kHz)
- **Radio HF** : 3 MHz - 30 MHz (raccourcis radio)
- **Radio VHF** : 30 MHz - 300 MHz (FM 88-108 MHz, TV)
- **Radio UHF** : 300 MHz - 3 GHz (TV UHF, cellulaire 800 MHz - 2 GHz, Wi-Fi)
- **Micro-ondes** : 3 GHz - 300 GHz
- **Rayons infrarouges** : 300 GHz - 430 THz
- **Lumière visible** : 430 THz - 770 THz (rouge à violet)
- **Rayons ultraviolets** : 770 THz - 30 PHz
- **Rayons X** : 30 PHz - 300 EHz
- **Rayons gamma** : 300 EHz + (extrêmement haute énergie)

**RadioFréquence (RF) définie:** 3 kHz - 300 GHz (plage utilisée pour radiocommunications et wireless)

### Bande 2.4 GHz pour Wireless LAN

**Plage**: 2.400 GHz - 2.4835 GHz (pas 2.4 - 2.5 GHz complet)

**Canaux définis**: 14 canaux au total, numérotés 1-14 (régional):
- Canaux 1-11 : Utilisés en Amérique du Nord (FCC)
- Canaux 1-13 : Utilisés en Europe (ETSI)
- Canal 14 : Japon seulement (MKK)

**Espacement des canaux**: 5 MHz entre les fréquences centrales des canaux (canal 1=2.412 GHz central, canal 2=2.417 GHz, etc.)

**Problème d'interférence**: Bien que les canaux soient espacés de 5 MHz, la bande passante d'un signal Wi-Fi est de ~22 MHz (dépend du standard). Cela signifie que les canaux 1, 6 et 11 ne se chevauchent PAS (écarts de 25 MHz), mais canaux 1-2 se chevauchent significativement.

### Bande 5 GHz pour Wireless LAN

**Structure complexe**: 5 GHz n'est pas une bande continue – elle est divisée en 4 bandes distinctes séparées:

**Bande 1: 5.150 - 5.250 GHz** (UNII-1 en FCC)
- 8 canaux: 36, 40, 44, 48 (4 MHz apart)

**Brèche: 5.250 - 5.350 GHz** (réservé, non usable pour Wi-Fi)

**Bande 2: 5.250 - 5.350 GHz** (UNII-2 en FCC) 
- 4 canaux: 52, 56, 60, 64

**Brèche: 5.350 - 5.470 GHz** (réservé, non usable)

**Bande 3: 5.470 - 5.725 GHz** (UNII-3)
- Nombreux canaux pour 144 et supérieur

**Bande 4: 5.725 - 5.825 GHz** (UNII-4)
- Canaux 149-165

**Avantages 5 GHz:**
- Beaucoup plus d'espace spectre → Canaux non-overlapping multiples
- Support de débits plus élevés
- Moins d'interférence de dispositifs micro-ondes/Bluetooth (ceux-ci sont 2.4 GHz)

### Largeur et Interférence de Canal

**Largeur de bande du signal**: La largeur en fréquence que le signal Wi-Fi occupe réellement. Des standards 802.11 définissent ceci:

- **802.11b** (1 Mbps - 11 Mbps) : ~22 MHz de largeur
- **802.11g/a** (6 - 54 Mbps) : ~20 MHz de largeur
- **802.11n** (jusqu'à 600 Mbps) : 20 MHz ou 40 MHz (combining 2 canals)
- **802.11ac** (jusqu'à 1.3 Gbps) : 80 MHz ou 160 MHz

**Mascara spectral**: Officiellement, le signal de Wi-Fi doit conformer à une "mascara spectrale" qui limite l'énergie émise en dehors de la largeur de bande définie. Mais en pratique, un peu d'énergie du signal fuit en canaux adjacents, causant une possible interférence.

**Sélection de canaux non-overlapping:**
- **2.4 GHz** : Seulement 3 canaux sans chevauchement (typique: 1, 6, 11)
- **5 GHz** : Beaucoup plus de possibilités (les 4 bandes offrent doizaines de canaux)

---

## 2. TRANSPORT DE DONNÉES SUR SIGNAUX WIRELESS

### Compréhension de la Phase

La **phase** est une mesure du point dans le cycle d'une onde où vous examinez le signal. Un cycle complet = 360 degrés (ou 2π radians).

- **Phase 0°** : Début du cycle
- **Phase 90°** : 1/4 du chemin à travers le cycle
- **Phase 180°** : Moitié du chemin – opposé au cycle de 0°
- **Phase 270°** : 3/4 du chemin
- **Phase 360°** : Un cycle complet (identique à 0°)

**Signaux en phase vs déphasés:**

Quand deux signaux de même fréquence arrivent à un destinataire :
- **En phase** (0° décalage) : Les crêtes s'alignent, les signaux s'ajoutent constructivement (amplitude double)
- **180° déphasé** : Les crêtes d'un signal correspondent aux creux de l'autre – les signaux **s'annulent** complètement

Ceci est exploité en modulation et détection de signaux.

### Longueur d'onde

La **longueur d'onde** (λ, lambda) est la distance physique qu'une onde parcourt pendant un cycle complet.

**Relation:**
λ = c / f

Où: c = vitesse de la lumière (~3 × 10^8 m/s), f = fréquence Hz

**Exemples:**
- 2.4 GHz Wi-Fi: λ = (3 × 10^8) / (2.4 × 10^9) ≈ 0.125 m (12.5 cm)
- 5 GHz Wi-Fi: λ = (3 × 10^8) / (5 × 10^9) ≈ 0.06 m (6 cm)

**Implication pour antennes:** Les antennes Li-Fi efficaces sont généralement dimensionnées par rapport à la longueur d'onde. Une antenne dipôle typique est λ/2 en longueur. Pour 2.4 GHz, une antenne dipôle effectif = 6.25 cm. Pour 5 GHz = 3 cm.

### Mesure de Puissance RF : Absolue et Décibels

**Puissance absolue**: Énergie émise, mesurée en Watts (W) ou Milliwatts (mW).
- 1 W = 1,000 mW
- Un appareil émettant 100 mW = 0.1 W

**Le problème avec les watts**: Les différences de puissance wireless sont énormes. Un AP à 30 mW vs une station de base cellulaire à 10 Watts = 333× différence. Difficile à comparer visuellement.

**Solution : Décibels (dB)** – Échelle logarithmique

```
dB = 10 × log₁₀(P2 / P1)
```

Comparaison de P2 (puissance de test) à P1 (puissance de référence).

**Interprétation:**
- **dB = 0** : P2 = P1 (puissances égales)
- **dB > 0** : P2 > P1 (P2 plus puissant)
- **dB < 0** : P2 < P1 (P2 plus faible)
- **dB = 3** : P2 = 2 × P1 (doublement)
- **dB = 10** : P2 = 10 × P1
- **dB = -3** : P2 = 0.5 × P1 (moitié)
- **dB = -10** : P2 = 0.1 × P1

**Exemples pratiques**:
- Avant : 100 mW, Après : 50 mW → dB = 10 × log₁₀(50/100) = 10 × log₁₀(0.5) = -3 dB
- Avant : 30 mW, Après : 150 mW → dB = 10 × log₁₀(150/30) = 10 × log₁₀(5) ≈ +7 dB

### Standards 802.11

**802.11a:**
- Fréquence: 5 GHz
- Modulation: OFDM (Orthogonal Frequency-Division Multiplexing)
- Max Débit: 54 Mbps
- État: Historique (remplacé par 802.11ac/ax)

**802.11b:**
- Fréquence: 2.4 GHz
- Modulation: DSSS (Direct Sequence Spread Spectrum)
- Max Débit: 11 Mbps
- État: Très lent, rarement vu aujourd'hui

**802.11g:**
- Fréquence: 2.4 GHz
- Modulation: OFDM (comme 802.11a mais 2.4 GHz)
- Max Débit: 54 Mbps
- Compatibilité: Arrière-compatible avec 802.11b (si 802.11b présent, débit décline)

**802.11n (Wi-Fi 4):**
- Fréquence: 2.4 GHz et/ou 5 GHz (dual-band)
- Modulation: OFDM amélioré
- Technologie clé: **MIMO** (Multiple-Input Multiple-Output) – utilise antennes multiples
- Largeur canal: 20 MHz (défaut) ou 40 MHz (40 MHz = débit double)
- Max Débit: 600 Mbps (4×4 MIMO @ 40 MHz)

**802.11ac (Wi-Fi 5):**
- Fréquence: 5 GHz seulement
- Modulation: OFDM
- Technologie clé: **MU-MIMO** (Multi-User MIMO) – serve plusieurs clients simultanément
- Largeur canal: 80 MHz (défaut) ou 160 MHz double)
- Max Débit: 1+ Gbps (1.3 Gbps possible)

**802.11ax (Wi-Fi 6):**
- Fréquence: 2.4 GHz, 5 GHz, et nouveau 6 GHz band
- Modulation: OFDMA (Orthogonal FDM avec accès multiple)
- Technologie clé: Efficacité spectre supérieur via OFDMA
- Max Débit: Multi-gigabit (9.6+ Gbps théorique)
- Premier standard à utiliser 6 GHz (spectrum nouvelle ouverture 2020+)

---

## Résumé et Points clés

1. **Spectre RF**: 3 kHz - 300 GHz avec Wi-Fi à 2.4 GHz (large bande, beaucoup interférence) et 5 GHz (bande dégroupée, plus efficace).

2. **2.4 GHz**: Seulement 3 canaux sans chevauchement (1, 6, 11). ~22 MHz largeur signal.

3. **5 GHz**: 4 bandes séparées, 2 brèches (5.250-5.350, 5.350-5.470), ~20 MHz largeur signal.

4. **Longueur d'onde**: Plus haute fréquence = longueur d'onde plus courte. 2.4 GHz = 12.5 cm, 5 GHz = 6 cm.

5. **Décibels**: Échelle log, 3 dB = doublement puissance, -3 dB = moitié. Facilite comparaison grandes différences.

6. **Standards modernes**: 802.11n (MIMO), 802.11ac (MU-MIMO, 5 GHz), 802.11ax (OFDMA, 6 GHz).

---

*Dernière révision : 18 mars 2026*
*Révision CCNP ENCOR Module 17*
