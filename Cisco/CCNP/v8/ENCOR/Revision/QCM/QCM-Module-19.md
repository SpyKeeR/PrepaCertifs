# QCM Module 19 : Roaming et Services de Localisation
## 25 Questions - Révision Complète

---

**Question 1**: Qui décide quand un client roamer vers un nouvel AP ?
- A) Le réseau (AP/WLC)
- B) Le serveur RADIUS
- C) Le client lui-même (basé sur RSS)
- D) WLC based on client utilization

**Réponse**: C) Le client lui-même (basé sur RSS) ✓
**Explication**: Client décide basé sur RSS mesuré, signal degradation. Propriétaire algo chaque OS.

---

**Question 2**: Durée typique totale déconnexion client durant roaming standard :
- A) < 50 ms
- B) 100-500 ms
- C) 1-2 secondes
- D) 5+ secondes

**Réponse**: B) 100-500 ms ✓
**Explication**: Réassociation rapide (~100 ms), mais si 802.1x RADIUS alors 1-2 sec possibles.

---

**Question 3**: Format Mobility List sur WLC :
- A) Liste IP de WLCs trusted
- B) MACs des WLCs avec mobility group names
- C) Canals à utiliser pour roaming
- D) List client MAC à autoriser

**Réponse**: B) MACs des WLCs avec mobility group names ✓
**Explication**: WLC stocke MAC address carte + mobility group assigné (local/peer/etc).

---

**Question 4**: Roaming client entre deux APs sur MÊME WLC :
- A) Transparentissé, WLC update assoc
- B) Tunnel créé entre APs
- C) Client DHCP release obligatoire
- D) Full re-authentication requis

**Réponse**: A) Transparentissé, WLC update assoc ✓
**Explication**: Même WLC = WLC know client = rapide assoc update, pas tunnel.

---

**Question 5**: Client roame de WLC1 (VLAN 100) → WLC2 (VLAN 200). Quelle est le pattern d'échangé ?
- A) Direct roaming, client change IP
- B) Anchor/Foreign, tunnel entre WLCs
- C) Client lost, re-connect required
- D) Tunnel seulement si VLAN match

**Réponse**: B) Anchor/Foreign, tunnel entre WLCs ✓
**Explication**: Clients roamant VLANs différents = Anchor (WLC1) + Foreign (WLC2) tunnel.

---

**Question 6**: Une Mobility Group configuration ferait QUOI ?
- A) Marquer WLCs comme trusted peers
- B) Limit clients par WLC
- C) Encryption channel entre APs
- D) Configure DHCP pools

**Réponse**: A) Marquer WLCs comme trusted peers ✓
**Explication**: Mobility Group = WLCs dans même groupe share client info, fast roaming.

---

**Question 7**: Quel est l'avantage CCKM roaming optimization ?
- A) Augmenter puissance AP
- B) Bypass RADIUS, pre-cache clés sur multiples WLCs
- C) Augmenter SSID broadcast
- D) Augmenter channel width

**Réponse**: B) Bypass RADIUS, pre-cache clés sur multiples WLCs ✓
**Explication**: CCKM = clés pré-partagée entre WLCs = roaming 50-100 ms possibles.

---

**Question 8**: Support Client pour CCKM :
- A) Tous les clients supportent
- B) Seulement Cisco devices
- C) Seulement CCX-certifié clients
- D) Seulement devices 802.11ax

**Réponse**: C) Seulement CCX-certifié clients ✓
**Explication**: CCKM = Cisco Centralized Key Mgt, requiert Cisco CCX client support.

---

**Question 9**: Technique roaming 802.11r (Fast BSS Transition) fait quoi ?
- A) Augmenter signal transmit power
- B) Client pre-position auth key derivative, local roaming (< 100ms)
- C) Forcer client skip authentication
- D) Augmenter AP density automatiquement

**Réponse**: B) Client pre-position auth key derivative, local roaming (< 100ms) ✓
**Explication**: 802.11r = FT protocol. Client + AP cache clé, RADIUS bypass possible. < 100ms typique.

---

**Question 10**: Key Caching dans 802.11i stocke combien de (AP, clé) paires ?
- A) 1
- B) 4
- C) 8
- D) Illimité

**Réponse**: C) 8 ✓
**Explication**: 802.11i Key Caching = jusqu'à 8 paired APs cached. Rapide re-assoc si APs mémorisé.

---

**Question 11**: Trilatération RSS require minimum combien d'APs ?
- A) 1 (distance seulement)
- B) 2 (distance + une direction)
- C) 3 (intersection cercles)
- D) 4+ (seulement pour haute précision)

**Réponse**: C) 3 (intersection cercles) ✓
**Explication**: 3 cercles (AP1, AP2, AP3 RSS radii) = intersection = exact location point.

---

**Question 12**: Cisco DNA Spaces utilisé pour quoi principalement ?
- A) Blockchain security
- B) Floor plan visual + real-time client tracking
- C) Data encryption
- D) VPN tunneling

**Réponse**: B) Floor plan visual + real-time client tracking ✓
**Explication**: DNA Spaces = location services. Import floor plan, place APs, visualize clients.

---

**Question 13**: Interférence non-802.11 (ex: microwave) peut être localisée via :
- A) Pas possible, doit stopper source manuellement
- B) RSS trilatération multi-AP (energy detection)
- C) Seulement via AP reset
- D) Requires external RF analyzer

**Réponse**: B) RSS trilatération multi-AP (energy detection) ✓
**Explication**: Non-802.11 energy visible dans bande 2.4/5 GHz. RSS triangulation locate source.

---

**Question 14**: Rogue AP detection dans wireless network typically appliqué pour :
- A) Mesurer client throughput
- B) Dureté contre unauthorized AP intrus
- C) Augmenter SSID broadcast
- D) Force client change channels

**Réponse**: B) Dureté contre unauthorized AP intrus ✓
**Explication**: Rogue AP = non-à l'autorité, peut sniffer clients. Detection + location = security.

---

**Question 15**: Client roamant entre Même mobility group WLCs :
- A) Full re-authentication (slow, 1-2s)
- B) Fast roaming possible (< 100ms)
- C) Client must rejoin SSID
- D) Tunnel always created

**Réponse**: B) Fast roaming possible (< 100ms) ✓
**Explication**: Même group = trusted peers = fast info sharing = roaming optimize possible.

---

**Question 16**: Client roamant entre DIFFÉRENTS mobility groups :
- A) Instant seamless (WLCs auto peer)
- B) Slow roaming, full re-auth required (1-2s)
- C) Tunnel always used
- D) Client must manually reconnect

**Réponse**: B) Slow roaming, full re-auth required (1-2s) ✓
**Explication**: Cross-group = unknown client to new WLC = RADIUS re-auth = lent.

---

**Question 17**: "Anchor Controller" dans roaming intercontroller roaming est :
- A) Original WLC où cliente initialement associé
- B) WLC avec meilleur interface
- C) WLC avec plus APs connectés
- D) WLC avec hierhieur stratum

**Réponse**: A) Original WLC où cliente initialement associé ✓
**Explication**: Anchor = « home » WLC. Maintains contexte client original (VLAN, IP clés).

---

**Question 18**: "Foreign Controller" dans roaming pattern est :
- A) WLC appartenant différent organization
- B) New WLC où cliente roame à
- C) WLC dépourvu d'interface Ethernet
- D) WLC derrière un firewall

**Réponse**: B) New WLC où cliente roame à ✓
**Explication**: Foreign = « visit » WLC. Temporaire, tunnel à Anchor pour contexte.

---

**Question 19**: Technique roaming rendant < 100 ms transition SANS nécessiter RADIUS préloaded :
- A) Key Caching
- B) DHCP Renewal
- C) 802.11r FT
- D) Aucune ci-dessus

**Réponse**: C) 802.11r FT ✓
**Explication**: FT = Fast Transition. Pre-position clé derivée = local keying = RADIUS bypass.

---

**Question 20**: DHCP impact durant roaming quand client change VLAN :
- A) Toujours déclenchera DHCP release/renew
- B) Peut nécessiter nouveau lease si subnet different
- C) DHCP pas concerné (trop bas-level)
- D) Ignore DHCP, utiliser link-local

**Réponse**: B) Peut nécessiter nouveau lease si subnet different ✓
**Explication**: Nouveau VLAN = nouveau subnet = possible DHCP renew. Typiquement rapide (< 100ms).

---

**Question 21**: Vitesse roaming avec CCKM optimisé à quoi est comparable ?
- A) Standard roaming (1-2 sec)
- B) Key Caching (200-500ms)
- C) 802.11r FT (< 100ms)
- D) Plus lent que Key Caching

**Réponse**: C) 802.11r FT (< 100ms) ✓
**Explication**: CCKM = 50-100ms. Comparable 802.11r pour vitesse, mieux Key Caching.

---

**Question 22**: Non-associated device (rogue client sans connexion) peut être localisé via :
- A) Pas possible, must associé pour tracking
- B) Probe request RSS détection + trilatération
- C) Seulement si proche d'AP
- D) Impossible, client must authenticate

**Réponse**: B) Probe request RSS détection + trilatération ✓
**Explication**: Non-proprio clients envoient probe requests. RSS détectable et triangularisable.

---

**Question 23**: Avantage Active RFID tag (vs passive) pour asset tracking :
- A) Plus petit taille
- B) Plus marché bon marché
- C) Batterie-powered, envoie signaux périodique
- D) Aucun besoin de lecteur

**Réponse**: C) Batterie-powered, envoie signaux périodique ✓
**Explication**: Active RFID = transceiver intégré. Périodique probe requests = WiFi tracking.

---

**Question 24**: Client sur WLC1 VLAN100 (-IP 192.168.100.50) roame WLC2 VLAN200. IP client post-roaming ?
- A) Change à 192.168.200.X (nouvel DHCP)
- B) Reste 192.168.100.50 (Anchor gère)
- C) Perd connectivité (VLAN conflict)
- D) Dépend configuration client

**Réponse**: B) Reste 192.168.100.50 (Anchor gère) ✓
**Explication**: Anchor pattern = client gardant IP original via tunnel. Pas DHCP release.

---

**Question 25**: Contexte client partagé entre WLCs dans même Mobility Group via :
- A) Broadcast sur LAN
- B) Control plane CAPWAP tunnel entre WLCs
- C) DHCP server central
- D) DNS resolution

**Réponse**: B) Control plane CAPWAP tunnel entre WLCs ✓
**Explication**: WLC-to-WLC communication = CAPWAP control tunnel. Même que AP-WLC protocol.

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. C | 2. B | 3. B | 4. A | 5. B
6. A | 7. B | 8. C | 9. B | 10. C
11. C | 12. B | 13. B | 14. B | 15. B
16. B | 17. A | 18. B | 19. C | 20. B
21. C | 22. B | 23. C | 24. B | 25. B

---

*QCM Révision Module 19 - CCNP ENCOR v8*
