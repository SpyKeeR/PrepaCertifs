# QCM Module 17 : Signaux Wireless
## 25 Questions - Révision Complète

---

**Question 1**: Quelle est la plage exacte de fréquence de la bande 2.4 GHz pour Wi-Fi ?
- A) 2.4 - 2.5 GHz (complète)
- B) 2.400 - 2.4835 GHz
- C) 2.412 - 2.484 GHz
- D) 2.0 - 2.7 GHz

**Réponse**: B) 2.400 - 2.4835 GHz ✓
**Explication**: Pas la bande complète 2.4-2.5 GHz, mais seulement 2.400-2.4835 GHz pour Wi-Fi.

---

**Question 2**: Combien de canaux non-overlappants peut-on utiliser simultanément en 2.4 GHz ?
- A) 2
- B) 3
- C) 6
- D) 11

**Réponse**: B) 3 ✓
**Explication**: Seulement canaux 1, 6, 11 ne se chevauchent pas (25 MHz spacing).

---

**Question 3**: Quels sont les trois canaux 2.4 GHz recommandés pour déploiement multi-AP ?
- A) 1, 5, 9
- B) 1, 6, 11
- C) 2, 7, 12
- D) 1, 7, 13

**Réponse**: B) 1, 6, 11 ✓
**Explication**: Spacing de 5 MHz × 5 (25 MHz total) entre 1-6 et 6-11 evite overlap.

---

**Question 4**: La bande 5 GHz n'est pas continue - combien de brèches (gaps) existent ?
- A) Aucune (bande continue)
- B) 1 brèche
- C) 2 brèches
- D) 3+ brèches

**Réponse**: C) 2 brèches ✓
**Explication**: 5.250-5.350 GHz et 5.350-5.470 GHz sont non-usables pour Wi-Fi.

---

**Question 5**: Laquelle des bandes 5 GHz suivantes est la plus restrictive en puissance radiée (radar weather) ?
- A) 5.150-5.250 GHz
- B) 5.250-5.350 GHz
- C) 5.470-5.725 GHz
- D) 5.725-5.825 GHz

**Réponse**: C) 5.470-5.725 GHz ✓
**Explication**: UNII-3 (canaux 100-144) demande DFS/TPC pour coexister avec radars météo.

---

**Question 6**: Largeur de bande signal typique pour 802.11b à 11 Mbps ?
- A) 5 MHz
- B) 10 MHz
- C) ~22 MHz
- D) 33 MHz

**Réponse**: C) ~22 MHz ✓
**Explication**: 802.11b DSSS occupe environ 22 MHz bande passante.

---

**Question 7**: Calculez la longueur d'onde (λ) pour Wi-Fi 5 GHz (c = 3×10^8 m/s) :
- A) 3 cm
- B) 6 cm
- C) 12.5 cm
- D) 25 cm

**Réponse**: B) 6 cm ✓
**Explication**: λ = c/f = (3×10^8) / (5×10^9) = 0.06 m = 6 cm

---

**Question 8**: Quelle est la relation décibel pour doubler la puissance ?
- A) 0 dB
- B) +1 dB
- C) +3 dB
- D) +6 dB

**Réponse**: C) +3 dB ✓
**Explication**: dB = 10 × log₁₀(2) ≈ 3 dB pour ratio 2:1

---

**Question 9**: Comparaison : 100 mW réduit à 25 mW = combien de dB ?
- A) -6 dB
- B) -4 dB
- C) -12 dB
- D) -3 dB

**Réponse**: A) -6 dB ✓
**Explication**: dB = 10 × log₁₀(25/100) = 10 × log₁₀(0.25) = 10 × (-0.602) ≈ -6 dB

---

**Question 10**: Quel standard 802.11 introduit la technologie MIMO (Multiple-Input Multiple-Output) ?
- A) 802.11a
- B) 802.11g
- C) 802.11n
- D) 802.11ac

**Réponse**: C) 802.11n ✓
**Explication**: 802.11n d'abord utilise MIMO antenne multiples. AC etendant ceci avec MU-MIMO.

---

**Question 11**: Débit maximum théorique de 802.11ac sur un canal 80 MHz avec MU-MIMO ?
- A) 300 Mbps
- B) 600 Mbps
- C) 1 Gbps+
- D) 600 Mbps (même ac)

**Réponse**: C) 1 Gbps+ ✓
**Explication**: 802.11ac atteint 1.3 Gbps avec 80 MHz bande passante et mode MU-MIMO optimal.

---

**Question 12**: Quel standard peut utiliser la bande 6 GHz (spectre récemment ouvert) ?
- A) 802.11n
- B) 802.11ac
- C) 802.11ax
- D) 802.11af

**Réponse**: C) 802.11ax ✓
**Explication**: Wi-Fi 6 (802.11ax) premier à supp 6 GHz. Nouveaux AP Wi-Fi 6E support 6 GHz.

---

**Question 13**: Phase de 180° entre deux signaux de même fréquence résulte en :
- A) Constructive addition (amplitude double)
- B) Destructive cancellation (s'annulent)
- C) Pas d'effet
- D) Déphasage gradient

**Réponse**: B) Destructive cancellation (s'annulent) ✓
**Explication**: 0° phase = constructive (s'additionne). 180° = destructive (s'annule).

---

**Question 14**: Pour un signal 2.4 GHz ~22 MHz largeur, quelle est la problème principal en déploiement multi-AP ?
- A) Interférence avec satellites
- B) Seulement 3 canaux sans overlap possible
- C) Trop d'énergie radiée
- D) Incompatibilité avec 5 GHz

**Réponse**: B) Seulement 3 canaux sans overlap possible ✓
**Explication**: 22 MHz largeur signal sur canaux 5 MHz espacement = seulement 1, 6, 11 sans chevauchement.

---

**Question 15**: Bande passante totale utilisable dans UNII-1 (5.150-5.250 GHz) pour canaux 4× 20 MHz ?
- A) 20 MHz
- B) 80 MHz (4 canaux × 20 MHz)
- C) 100 MHz
- D) 150 MHz

**Réponse**: B) 80 MHz (4 canaux × 20 MHz) ✓
**Explication**: UNII-1 = 100 MHz total, 4 canaux de 20 MHz chacun = 80 MHz utilisé (avec spacing).

---

**Question 16**: Quel est l'amplitude dans la formule de calcul décibels ?
- A) Puissance seulement
- B) Tension et puissance
- C) Fréquence
- D) Phase

**Réponse**: A) Puissance seulement ✓
**Explication**: dB = 10 × log₁₀(P2/P1). Basé sur ratio de puissances.

---

**Question 17**: Modulation utilisée par 802.11b ?
- A) OFDM
- B) DSSS
- C) QAM
- D) PSK

**Réponse**: B) DSSS ✓
**Explication**: Spread Spectrum Direct Sequence (DSSS) pour 802.11b 2.4 GHz.

---

**Question 18**: Quel est le principal avantage de la bande 5 GHz par rapport à 2.4 GHz ?
- A) Portée plus grande
- B) Moins de congestion spectre, nombreux canaux
- C) Meilleure pénétration mur
- D) Moins cher à implémenter

**Réponse**: B) Moins de congestion spectre, nombreux canaux ✓
**Explication**: 5 GHz offre beaucoup plus canals non-overlappants que 2.4 GHz congestionné.

---

**Question 19**: Fréquence centrale officiel pour canal Wi-Fi 6 (2.4 GHz) ?
- A) 2.412 GHz
- B) 2.437 GHz
- C) 2.462 GHz
- D) 2.484 GHz

**Réponse**: C) 2.462 GHz ✓
**Explication**: Canal 11 = 2.462 GHz. Canal 1 = 2.412. Canal 6 = 2.437.

---

**Question 20**: MIMO dans 802.11n peuvent se combiner canaux pour doubler bande passante. Largeur combinée ?
- A) 20 MHz
- B) 40 MHz
- C) 60 MHz
- D) 80 MHz

**Réponse**: B) 40 MHz ✓
**Explication**: 802.11n peut combiner deux 20 MHz canals = 40 MHz (doubleant le débit théorique).

---

**Question 21**: Quelle fréquence est considérée comme "haute fréquence" dans le spectre RF ?
- A) 100 kHz
- B) 100 MHz
- C) 1 GHz
- D) Toutes > 100 MHz

**Réponse**: C) 1 GHz ✓
**Explication**: Ondes centimétriques (GHz range) sont "RF haute fréquence".

---

**Question 22**: Phase 90° entre deux signaux identiques signifie :
- A) Signaux en phase (s'ajoutent)
- B) Déphasés (s'annulent)
- C) Partiellement déphasés (s'ajoutent faiblement)
- D) Pas de relation phase

**Réponse**: C) Partiellement déphasés (s'ajoutent faiblement) ✓
**Explication**: 90° = 1/4 cycle décalage = constructive partiel.

---

**Question 23**: Si signal A = 50 mW et signal B = 200 mW, ratio dB (B relative A) ?
- A) -6 dB
- B) 0 dB
- C) +6 dB
- D) +12 dB

**Réponse**: C) +6 dB ✓
**Explication**: dB = 10 × log₁₀(200/50) = 10 × log₁₀(4) ≈ 6dB

---

**Question 24**: Limitation principale du standard 802.11g sur 2.4 GHz ?
- A) Lenteur historique (54 Mbps max)
- B) Backward compat avec 802.11b ralentit trafic
- C) Incompatible avec antennes MIMO
- D) Bande trop étroite pour multiple canals

**Réponse**: B) Backward compat avec 802.11b ralentit trafic ✓
**Explication**: Si clients legacy 802.11b présents, AP ralentit à 802.11b ou modes mixtes = moins performance.

---

**Question 25**: Antenne dipôle Wi-Fi 2.4 GHz efficace est approximativement quelle longueur ?
- A) 3 cm
- B) 6.25 cm
- C) 12.5 cm
- D) 25 cm

**Réponse**: B) 6.25 cm ✓
**Explication**: Dipôle = λ/2. λ 2.4 GHz = 12.5 cm. Dipôle = 6.25 cm.

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. B | 2. B | 3. B | 4. C | 5. C
6. C | 7. B | 8. C | 9. A | 10. C
11. C | 12. C | 13. B | 14. B | 15. B
16. A | 17. B | 18. B | 19. C | 20. B
21. C | 22. C | 23. C | 24. B | 25. B

---

*QCM Révision Module 17 - CCNP ENCOR v8*
