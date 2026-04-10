# Fiche Module 17 : Signaux Wireless
## Référence Rapide pour Révision

---

## RÉSUMÉ BANDES DE FRÉQUENCE

| Bande | Plage | Canaux | Largeur signal | Avantages |
|-------|-------|--------|-----------------|-----------|
| **2.4 GHz** | 2.400-2.4835 GHz | 1-14 (régional) | ~22 MHz | Portable, longue portée, compatible |
| **5 GHz** | 5.150-5.825 (4 sous-bandes) | 36-165 | ~20 MHz | Nombreux canaux, moins interférence |
| **6 GHz** | 5.925-7.125 GHz | Nouveau (802.11ax) | Variable | Très large spectre disponible |

**2.4 GHz Canaux Non-overlappants**: 1, 6, 11 (25 MHz spannsion – 5 MHz intercanal + 22 MHz largeur = no overlap)

---

## TABLEAU ASSIGNATION CANAUX 2.4 GHz

| Canal | Fréquence Centrale | Régions |
|-------|-------------------|---------|
| 1 | 2.412 GHz | USA, Europe, Plupart |
| 6 | 2.437 GHz | USA, Europe |
| 11 | 2.462 GHz | USA, Europe |
| 14 | 2.484 GHz | Japon seulement |

Canaux 1-13 pour plupart régions, canal 14 Japon unique.

---

## COMPOSITION BANDE 5 GHz

```
BANDE 1: 5.150-5.250 GHz (UNII-1)
├─ Canaux: 36, 40, 44, 48
├─ Pas de restriction puissance
└─ Utilisation: Intérieur/extérieur

Brèche: 5.250-5.350 GHz NON USABLE

BANDE 2: 5.250-5.350 GHz (UNII-2)  
├─ Canaux: 52-144 (déploiement rare)
└─ Restrictions puissance par région

Brèche: 5.350-5.470 GHz NON USABLE

BANDE 3: 5.470-5.725 GHz (UNII-3)
├─ Canaux: 100-144
└─ Restrictions puissance strictes (radar)

BANDE 4: 5.725-5.825 GHz (UNII-4)
├─ Canaux: 149-165
└─ Non restreinte, usage général
```

---

## TABLEAU COMPARATIF STANDARDS 802.11

| Standard | Fréquence | Modulation | Speed Max | MIMO | Cas d'usage |
|----------|-----------|-----------|-----------|------|-----------|
| **802.11a** | 5 GHz | OFDM | 54 Mbps | Non | Historique |
| **802.11b** | 2.4 GHz | DSSS | 11 Mbps | Non | Très lent, legacy |
| **802.11g** | 2.4 GHz | OFDM | 54 Mbps | Non | Anciens AP |
| **802.11n (Wi-Fi 4)** | 2.4/5 GHz | OFDM | 600 Mbps | **MIMO** | Standard avant AC |
| **802.11ac (Wi-Fi 5)** | 5 GHz | OFDM | 1.3+ Gbps | **MU-MIMO** | Courant aujourd'hui |
| **802.11ax (Wi-Fi 6)** | 2.4/5/6 GHz | OFDMA | 9.6+ Gbps | MU-MIMO | Nouvelle génération |

---

## CALCUL LONGUEUR D'ONDE

**Formule**: λ = c / f

Où c = 3 × 10^8 m/s (vitesse lumière)

| Fréquence | Longueur d'onde | Application |
|-----------|-----------------|-------------|
| 2.4 GHz | 12.5 cm | Wi-Fi 2.4 GHz |
| 5 GHz | 6 cm | Wi-Fi 5 GHz |
| 6 GHz | 5 cm | Wi-Fi 6 futur |
| FM Radio (100 MHz) | 3 m | Références |

**Implication antenne**: Antennes dipôles efficaces = λ/2 longueur. Pour 2.4 GHz = 6.25 cm. Pour 5 GHz = 3 cm.

---

## RÉFÉRENCE RAPIDE DÉCIBELS

**Formule**: dB = 10 × log₁₀(P2 / P1)

| dB Value | Power Ratio | Sens Pratique |
|----------|-------------|---------------|
| 0 | 1× | Égal |
| +3 | 2× | Double |
| +6 | 4× | Quadruple |
| +10 | 10× | 10x plus fort |
| +20 | 100× | 100x plus fort |
| -3 | 0.5× | Moitié |
| -10 | 0.1× | 10x plus faible |

**Exemples pratiques**:
- 100 mW → 50 mW = -3 dB (moitié)
- 20 mW → 200 mW = +10 dB (10x)
- 1 W → 500 mW = -3 dB (moitié)

---

## INTERFÉRENCE ET NON-OVERLAPPING

**2.4 GHz Problème:**
- Seulement ~22 MHz largeur de signal
- 3 canaux sans chevauchement maximum: 1, 6, 11
- Espacement requis: 25 MHz entre centrales canales (5 MHz pas)

**Overlapping Exemple:**
- Canal 1 (2.412 GHz central) occupé ±11 MHz = 2.401-2.423 GHz
- Canal 2 (2.417 GHz central) occupé ±11 MHz = 2.406-2.428 GHz
- **Chevauchement = 2.406-2.423 GHz** → Interférence significative

**5 GHz Avantage:**
- Beaucoup plus d'espace spectre
- UNII-1: 4 canaux (36-48) sans overlap
- UNII-3/4: Douzaines de canaux
- Solution interférence plus facile

---

## RÈGLES SÉLECTION CANAUX

| Contexte | Recommandation |
|---------|-----------------|
| **Un seul AP 2.4 GHz** | N'importe lequel (1, 6, 11 meilleur) |
| **Nombreux APs 2.4 GHz** | Utiliser 1, 6, 11 seulement, espacer APs |
| **Interférence détectée** | Scanner canaux, regarder moins crowdé, changer 1→11 ou similaire |
| **5 GHz déploiement** | Automatique avec beaucoup canaux, peu contrainte |
| **Coexistence 2.4+5 GHz** | OK – différentes bandes, peu interférence cross-band |

---

## POINTS CLÉS POUR EXAMEN

1. **2.4 GHz**: 3 canaux max non-overlapping (1, 6, 11). Spectre plus congestionné.

2. **5 GHz**: 4 bandes séparées + 2 brèches. Beaucoup plus canaux = meilleur pour densité AP.

3. **Largeur Signal**: ~22 MHz (2.4 GHz), ~20 MHz (5 GHz). 802.11n/ac peuvent combiner pour 40/80 MHz.

4. **Longueur d'onde**: 2.4 GHz = 12.5 cm, 5 GHz = 6 cm. Affecte taille antenne.

5. **Décibels**: 3 dB = doublement puissance. -3 dB = moitié. Échelle log.

6. **Phase**: 0° = constructif (s'additionne), 180° = destructif (s'annule).

7. **Standards**: 802.11n (MIMO), 802.11ac (MU-MIMO, 5 GHz uniquement), 802.11ax (OFDMA, 6 GHz).

---

*Fiche de révision rapide - Module 17 CCNP ENCOR*
