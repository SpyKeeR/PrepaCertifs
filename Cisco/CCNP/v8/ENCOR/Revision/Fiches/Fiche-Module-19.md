# Fiche Module 19 : Roaming et Services de Localisation
## Référence Rapide pour Révision

---

## SÉQUENCE PROCESSUS ROAMING

```
1. CLIENT SCAN
   └─ Probe requests envoyés sur canaux
      └─ APs répondent avec RSSI

2. SÉLECTION AP
   └─ Client sélectionne meilleur RSSI (générally)
      └─ Peut avoir préférence SSID/Band

3. TENTATIVE RÉASSOCIATION
   └─ Client envoie reassociation request
      └─ Nouvel AP envoie réponse confirm

4. AUTHENTIFICATION
   └─ 802.1x EAP (peut être lent, 500ms-2s)
      └─ Optimisation techniques peuvent accélérer

5. MAINTENANCE RÉSEAU
   └─ WLC met à jour association client
      └─ Trafic rerouter au nouvel AP

6. CONCLUSION ROAMING
   └─ Client maintenant sur nouveau AP
      └─ Brief déconnexion totale : ~100-500 ms
```

---

## TABLEAU COMPARATIF TECHNIQUES ROAMING

| Technique | Vitesse | Technologie | Client Support | Impact |
|-----------|---------|------------|-----------------|--------|
| **Standard (aucune)** | 1-2 sec | Full RADIUS | Tous | Possible rupture voice |
| **Key Caching** | 200-500 ms | 802.11i cached PMK | 802.11i-capable | Modéré |
| **CCKM** | 50-100 ms | Clés interne WLC | CCX clients seulement | Excellent |
| **802.11r (FT)** | < 100 ms | FT protocol | 802.11r-capable | Très bon, standard |

**Recommandation**: 802.11r moderne, CCKM legacy Cisco.

---

## ROAMING COUCHE 2 vs COUCHE 3

| Aspect | Layer 2 Roam | Layer 3 Roam |
|--------|-------------|------------|
| **VLAN** | Même (1 subnet) | Différent (2 subnets) |
| **IP Client** | Reste inchangé | Anchor gère original |
| **Tunnel** | Non requis | Tunnel WLC à WLC |
| **DHCP Renew** | Non | Possible besoin |
| **Vitesse** | Rapide | Légèrement plus lent |

---

## ANCHOR VS FOREIGN CONTROLLER

| Rôle | Fonction | Contexte |
|-----|----------|---------|
| **Anchor (original)** | Maintient client contexte original (VLAN, IP, clés) | WLC où client initial associé |
| **Foreign (new)** | Accepte client, crée tunnel à Anchor | WLC où client roame maintenant |

Analogie: Anchor = "home" WLC, Foreign = "visit" WLC

---

## MOBILITY GROUPS CONCEPT

```
MÊME MOBILITY GROUP (Trusted Peers)
  ├─ WLC1 ←→ WLC2 ←→ WLC3
  │  Dépêche rapide (< 100 ms possible)
  │  Info client partagée immédiatement
  │
  └─ Client roamant entre 1 ↔ 2 ↔ 3 = rapide

DIFFÉRENTS MOBILITY GROUPS (Non-Trusted)
  └─ WLC1 (groupe "campus") ←→ WLC4 (groupe "partner")
     Clients roamant entre groupes = slow (1-2 sec, full re-auth)
```

---

## SERVICES DE LOCALISATION OVERVIEW

| Service | Technologie | Précision | Utilisation |
|---------|-------------|-----------|-----------|
| **RSS Single AP** | Distance estimation | ±10-20m | Rough location |
| **Trilatération 3+ APs** | RSS intersection | ±2-5m | Location exacte |
| **DNA Spaces Visuel** | Floor plan mapping | ±1-2m | Client tracking |
| **Rogue AP+Interference** | Energy detection | Variable | Interference source |

---

## TRILATÉRATION RSS MULTI-AP

**Concept simplifiée:**

```
       AP1 (RSSI -50dBm)
       └─ Rayon 5m
       
AP2    └─┬─────→ Client est ici?
(RSSI   │ Rayon (intersection de 3 cercles)
-65dBm) │
        │
    AP3 (RSSI -45dBm)
        └─ Rayon 8m
```

**Minimum APs**: 3 pour trilatération exacte. 4+ pour meilleure précision.

---

## UTILISATION RFID ACTIVE

- **Tag Attache**: Objet/personne avec petit tag Wi-Fi
- **Émission Périodique**: Tag wake, envoie probe request
- **Network Détecte**: APs reçoivent via RSS
- **Localisation**: Trilatération place tag
- **Suivi Temps Réel**: Mouvement tag suivi en continu

---

## INTERFÉRENCE NON-802.11 DETECTION

**Sources Courant:**
- Four micro-ondes (2.4 GHz, non-Wi-Fi waves)
- Téléphone sans fil legacy
- Caméra vidéo propriétaire
- Équipements industriel

**Localisation:**
- Network détecte energy dans bande 2.4/5 GHz
- RSS trilatération même protocole Wi-Fi
- Locate source précisément
- Éliminer source

---

## POINTS CLÉS POUR EXAMEN

1. **Roaming Decision**: Client décide (pas AP/WLC). Basé sur RSS + préférence.

2. **Roaming Time**: Standard 1-2s (RADIUS). Optimisé techniques : < 100ms possible.

3. **Même WLC Roam**: Transparent, assoc update. Pas tunnel.

4. **Intercontroller Roam**: Anchor/Foreign pattern. Tunnel si VLAN different.

5. **Mobility Groups**: Même groupe = fast (< 100ms), Crosse-groupe = slow (re-auth).

6. **DHCP/802.1x**: Peuvent être slow durant roaming. Optimisation techniques bypass RADIUS.

7. **RSS Location**: 1 AP = distance. 3+ APs = trilatération location exacte.

8. **DNA Spaces**: Visual floor plan, track client, rogue detection.

---

## TABLEAU RAPIDE ROAMING LATENCY

| Scenario | Latency Typique |
|----------|-----------------|
| **Standard roaming** | 1-2 secondes |
| **Key Caching pre-cached** | 200-500 ms |
| **CCKM optimisé** | 50-100 ms |
| **802.11r FastRoaming** | < 100 ms |
| **VoIP acceptable max** | < 150 ms (sinon rupture audible) |

---

## VOCABULARY CLEF

- **BSS**: Basic Service Set (un AP + ses clients)
- **RSSI**: Received Signal Strength Indicator (puissance signal)
- **Anchor Controller**: WLC original client
- **Foreign Controller**: Nouvel WLC durant roaming
- **Mobility List**: Liste MAC trusted WLCs
- **DHCP Snooping** (mitigation attack): Monitor DHCP packets
- **802.11r**: Fast BSS Transition (fast roaming standard)
- **DNA Spaces**: Cisco location services platform

---

*Fiche de révision rapide - Module 19 CCNP ENCOR*
