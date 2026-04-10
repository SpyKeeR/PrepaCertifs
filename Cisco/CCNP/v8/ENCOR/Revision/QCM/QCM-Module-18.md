# QCM Module 18 : Infrastructure Wireless
## 25 Questions - Révision Complète

---

**Question 1**: Quel est le mode d'AP pour un petit bureaux avec 2-3 APs indépendants ?
- A) Lightweight mode
- B) Autonomous mode
- C) Embedded mode
- D) Centralisé mode

**Réponse**: B) Autonomous mode ✓
**Explication**: Autonomous = indépendant, pas de WLC. Chaque AP config seul. Idéal petit.

---

**Question 2**: Dans mode Lightweight, le routeur de trafic client entre l'AP et le cliente se fait via :
- A) Direct (AP → switch → client)
- B) Tunnel CAPWAP vers WLC
- C) GRE tunnel
- D) IPsec tunnel

**Réponse**: B) Tunnel CAPWAP vers WLC ✓
**Explication**: Lightweight = tout trafic (control + data) via tunnel CAPWAP à WLC.

---

**Question 3**: Combien d'APs peut supporter généralement un WLC central Cisco ?
- A) 100-200
- B) 500-1000
- C) 1000+ (jusqu'à 6000)
- D) 10,000+

**Réponse**: C) 1000+ (jusqu'à 6000) ✓
**Explication**: Catalyst 9800 ou 3504 peuvent supporter 4000-6000 APs par controleur.

---

**Question 4**: Pour topologie Embedded WLC, le WLC se situe :
- A) Dans un bâtiment central separate
- B) Dans un AP
- C) Embarqué dans un commutateur d'accès
- D) Dans le cloud

**Réponse**: C) Embarqué dans un commutateur d'accès ✓
**Explication**: Embedded = WLC physiquement dans Catalyst 3850, 9300, ou Nexus switch.

---

**Question 5**: Quel est l'exigence RTT maximale pour APs communiquant avec un WLC centralisé ?
- A) < 50 ms
- B) < 100 ms
- C) < 200 ms
- D) < 500 ms

**Réponse**: B) < 100 ms ✓
**Explication**: Cisco spécifique < 100 ms RTT pour roaming + fiabilité.

---

**Question 6**: Lors du boot d'un AP, quel est le premier essai pour découvrir une WLC ?
- A) Multicast 224.0.1.44
- B) DNS query cisco-capwap-controller
- C) DHCP Option 43
- D) Configuration console manuelle

**Réponse**: C) DHCP Option 43 ✓
**Explication**: Ordre découverte: DHCP Opt43 → DNS → IP Helper → Multicast → Console.

---

**Question 7**: Le tunnel CAPWAP entre AP et WLC utilise quel port UDP sur WLC ?
- A) 22 (SSH)
- B) 443 (HTTPS)
- C) 5246/5247
- D) 8000

**Réponse**: C) 5246/5247 ✓
**Explication**: 5246 = control, 5247 = data (ou unified) CAPWAP.

---

**Question 8**: Si image AP ne correspond pas à version WLC, qu'arrive-t-il ?
- A) AP rest en mode limited
- B) WLC rejette AP immédiatement
- C) WLC télécharge nouvelle image à AP, AP redémarre
- D) AP ignore et fonctionne quand même

**Réponse**: C) WLC télécharge nouvelle image à AP, AP redémarre ✓
**Explication**: Processus boot étape 6 : Image version mismatch → Download → Reboot → Retry Discovery.

---

**Question 9**: Architecture CAPWAP split-MAC divise fonctions 802.11 où ?
- A) AP gère tout (pas split)
- B) WLC gère real-time, AP gère management
- C) AP gère real-time 802.11, WLC gère management
- D) Partagé 50/50

**Réponse**: C) AP gère real-time 802.11, WLC gère management ✓
**Explication**: Split-MAC : AP = PHY/MAC timing critique. WLC = security, NAS, policies.

---

**Question 10**: Quel mode AP ne supporte PAS le roaming transparent de client ?
- A) Autonomous
- B) Lightweight
- C) Centralisé
- D) Tous supportent roaming

**Réponse**: A) Autonomous ✓
**Explication**: Autonomous pas de gestion roaming – cliente re-authenticate quand change d'AP.

---

**Question 11**: Grande avantage de topologie Lightweight (WLC centralisé) est :
- A) Latence basse (no tunnel)
- B) Mobilité transparente + config centralisée
- C) Coût bas
- D) Compatibilité legacy

**Réponse**: B) Mobilité transparente + config centralisée ✓
**Explication**: WLC gère roaming + applique politiques center → haute scalabilité.

---

**Question 12**: Topologie Embedded est surtout recommandée pour :
- A) Grands campus (1000+ APs)
- B) Petits succursales (< 200 APs, pas WLC center)
- C) Points de vente unique
- D) Cloud deployments

**Réponse**: B) Petits succursales (< 200 APs, pas WLC center) ✓
**Explication**: Embedded = WLC dans switch = ideal succursal sanWLC dédié.

---

**Question 13**: Mobilité Express mode supporte typiquement combien d'APs ?
- A) 10-20
- B) 50-100
- C) 500+
- D) 4000+

**Réponse**: B) 50-100 ✓
**Explication**: Mobilité Express = AP+WLC embedded dans AP = petit, local. ~100 APs max.

---

**Question 14**: Format Cisco DHCP Option 43 pour WLC IP address :
- A) Simple IP list
- B) Vendor-specific encoding (F1 + IP bins)
- C) DNS CNAME pointer
- D) XML block

**Réponse**: B) Vendor-specific encoding (F1 + IP bins) ✓
**Explication**: Cisco Option 43 format: F104.a.b.c.d (F1=Cisco, 04=length, IP quartet).

---

**Question 15**: AP dans Autonomous mode nécessite quel type de lien commutateur ?
- A) Trunk (véhicule multiples VLANs)
- B) Accès (un VLAN)
- C) Routed port (L3)
- D) Port channel

**Réponse**: B) Accès (un VLAN) ✓
**Explication**: Autonomous AP sur un VLAN, cliente sur même VLAN ou routé normalement.

---

**Question 16**: AP Lightweight sur accès port change quelle(s) VLAN(s) ?
- A) Reste sur VLAN d'accès, tout trafic tunnelisé
- B) Multiple VLANs possibles sur trunk
- C) Clients VLANs décidés par WLC
- D) Pas de VLAN (tout IP)

**Réponse**: A) Reste sur VLAN d'accès, tout trafic tunnelisé ✓
**Explication**: AP lightweight pas trunk – tout tunnel CAPWAP homogène. VLAN existe au WLC.

---

**Question 17**: Processus AP boot étape 4 (CAPWAP tunnel) utilise quel encryptage ?
- A) AES-128 (IPsec style)
- B) DTLS (Datagram TLS)
- C) DES (legacy)
- D) Pas encryptage

**Réponse**: B) DTLS (Datagram TLS) ✓
**Explication**: CAPWAP tunnel = DTLS secured certificats digital exchange.

---

**Question 18**: Type d'antenne recommandée pour AP au plafond couvrant tout étage :
- A) Directionnelle (Patch)
- B) Omnidirectionnelle (Dipôle)
- C) Yagi (longue distance)
- D) Parabolic

**Réponse**: B) Omnidirectionnelle (Dipôle) ✓
**Explication**: Omnidirectionnelle = 360° horizontal coverage – idéal plafond central.

---

**Question 19**: Pour roaming client transparent sans rupture de session, nécessité minimum :
- A) Autonomous mode sufficient
- B) Lightweight + WLC maintains association
- C) Embedded topology seul
- D) VRRP pour gateway redondance

**Réponse**: B) Lightweight + WLC maintains association ✓
**Explication**: WLC tracking l'association client → roaming seamless.

---

**Question 20**: Espacement recommandé entre APs 2.4 GHz pour 20-30% chevauchement :
- A) 10 mètres
- B) 25 mètres
- C) 50 mètres
- D) 100+ mètres

**Réponse**: B) 25 mètres ✓
**Explication**: 2.4 GHz ~50-80m portée. 20% overlap = ~25m spacing.

---

**Question 21**: WLC point unique de failure dans topologie quoi :
- A) Autonomous (aucun WLC)
- B) Lightweight Centralisé
- C) Embedded (chaque switch son WLC)
- D) Toutes ont point unique failure

**Réponse**: B) Lightweight Centralisé ✓
**Explication**: Un WLC = tous APs dépendants. Failure = tous APs down. (Mitigation : haute disponibilité WLC)

---

**Question 22**: Lors Image Download durant boot AP, quel étape suit APRÈS reboots ?
- A) Étape 7 (Config Download)
- B) Étape 3 (Discovery)
- C) Étape 1 (Boot)
- D) Étape finale

**Réponse**: B) Étape 3 (Discovery) ✓
**Explication**: Image téléchargement → Reboots → Recommence discovery processs.

---

**Question 23**: Avantage Embedded vs Centralisé topologie ?
- A) Plus APs supporté
- B) Moins latence (WLC local)
- C) Meilleur roaming
- D) Coûts licences plus bas

**Réponse**: B) Moins latence (WLC local) ✓
**Explication**: Embedded = WLC dans switch local = RTT très faible. Centralisé = tunnel lointain.

---

**Question 24**: IP Helper command routeur switch configure pour AP discovery :
- A) Pas configuré (APs trouvent via DHCP)
- B) Relaye broadcast CAPWAP Multicast
- C) Redirect DNS queries
- D) Proxy DHCP

**Réponse**: B) Relaye broadcast CAPWAP Multicast ✓
**Explication**: IP Helper relaye 224.0.1.44 multicast AP → WLC discorvery fallback.

---

**Question 25**: Licence impact Lightweight mode :
- A) APs gratuit, WLC payant (par AP)
- B) Chaque AP nécessite licence
- C) Total throughput max = licence
- D) Aucune licence pour discovery

**Réponse**: B) Chaque AP nécessite licence ✓
**Explication**: WLC centralisé = licences per-AP (varie par model WLC).

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. B | 2. B | 3. C | 4. C | 5. B
6. C | 7. C | 8. C | 9. C | 10. A
11. B | 12. B | 13. B | 14. B | 15. B
16. A | 17. B | 18. B | 19. B | 20. B
21. B | 22. B | 23. B | 24. B | 25. B

---

*QCM Révision Module 18 - CCNP ENCOR v8*
