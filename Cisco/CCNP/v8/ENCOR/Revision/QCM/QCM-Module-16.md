# QCM Module 16 : Tunnels Overlay
## 25 Questions - Révision Complète

---

## SECTION 1 : TUNNELS GRE (10 Questions)

**Question 1**: Quel est le protocole IP number utilisé par GRE pour encapsuler le trafic ?
- A) 6 (TCP)
- B) 17 (UDP)
- C) 47 (GRE)
- D) 50 (ESP)

**Réponse**: C) 47 (GRE) ✓
**Explication**: GRE utilise le protocole IP 47. Les paquets encapsulés GRE sont identifiables par ce numéro dans l'en-tête IP externe.

---

**Question 2**: Quel est le cas d'usage principal d'un tunnel GRE ?
- A) Chiffrer le trafic pour la sécurité
- B) Encapsuler des protocoles non-IP (AppleTalk, IPX) dans IP
- C) Uniquement pour la redondance
- D) Réduire la latence réseau

**Réponse**: B) Encapsuler des protocoles non-IP (AppleTalk, IPX) dans IP ✓
**Explication**: GRE est Protocol-Agnostic – il peut tunneliser IPv4, IPv6, AppleTalk, IPX et autres. La sécurité vient d'IPsec, pas GRE seul.

---

**Question 3**: Lorsque vous configurez `tunnel source GigabitEthernet0/0/0` sans adresse IP spécifique, quel IP prend GRE comme source ?
- A) N'importe quel IP de l'interface
- B) L'adresse IP primaire de l'interface
- C) L'adresse IP secondaire
- D) La configuration échoue

**Réponse**: B) L'adresse IP primaire de l'interface ✓
**Explication**: Si vous spécifiez une interface (pas une IP), GRE utilise l'adresse IP primaire de cette interface comme source tunnel.

---

**Question 4**: Quel MTU tunnel minimal est-il recommandé pour éviter la fragmentation exessive ?
- A) 512
- B) 1000
- C) 1400
- D) 1500

**Réponse**: C) 1400 ✓
**Explication**: L'interface physique est généralement 1500 (Ethernet MTU). GRE ajoute ~24 octets. Configurer tunnel MTU = 1400 pour sûreté (100 octets buffer).

---

**Question 5**: Quel est le problème appelé « routage récursif » dans les tunnels GRE ?
- A) Le tunnel cause boucles depuis traffic de l'interface
- B) La destination tunnel est accessible via le tunnel lui-même
- C) L'horloge du routeur ne synchronise pas
- D) La sélection de l'interface de sortie est aléatoire

**Réponse**: B) La destination tunnel est accessible via le tunnel lui-même ✓
**Explication**: Si le routeur envoie des paquets destinés au tunnel via le tunnel, cela crée une boucle infinie. Mitigation: route statique pour dest tunnel via interface physique.

---

**Question 6**: Quel timeout (en utilisant keepalive par défaut) avant qu'une interface tunnel ne passe à down ?
- A) 3 secondes
- B) 10 secondes
- C) 30 secondes
- D) 180 secondes (3 minutes)

**Réponse**: C) 30 secondes ✓
**Explication**: Défaut keepalive: 10 secondes entre essais, 3 tentatives = 30 secondes total avant timeout. `keepalive 10 3` est configurable.

---

**Question 7**: GRE peut encapsuler à la fois IPv4 (underlay) et IPv6 (overlay) ou vice-versa. Quel est un scénario pratique pour cela ?
- A) Aucun routeur ne supporte vraiment cette combinaison
- B) Transition IPv6 : transport IPv4 existant, forward IPv6
- C) Uniquement pour tests, pas utilisé en production
- D) Performance – IPv4/IPv6 mixing accélère tunnels

**Réponse**: B) Transition IPv6 : transport IPv4 existant, forward IPv6 ✓
**Explication**: Lors de migration IPv6, la nouvelle infrastructure IPv6 peut être tunnelisée via l'infrastructure IPv4 existante. Cela permet co-existence graduelle.

---

**Question 8**: À quelle commande montre-t-on que le tunnel est up et collecte l'état MTU, les stats paquets ?
- A) `show tunnel 0`
- B) `show interface tunnel 0`
- C) `show tunnel status`
- D) `debug tunnel packets`

**Réponse**: B) `show interface tunnel 0` ✓
**Explication**: `show interface` affiche état physique/protocol, MTU, paquets envoyés/reçus, erreurs. Cette commande est identique pour toutes les interfaces.

---

**Question 9**: Une interface tunnel GRE est configured avec une bande passante 512 kbps. Quelle est la purpose de configurer cela ?
- A) Limiter le throughput réel du tunnel
- B) Influencer les métriques de routage dynamique (OSPF, EIGRP)
- C) Augmenter la priorité QoS
- D) Détecter les défaillances plus rapidement

**Réponse**: B) Influencer les métriques de routage dynamique (OSPF, EIGRP) ✓
**Explication**: Les protocoles de routage utilisent la bande passante pour calculer les métriques. 512 kbps = coût élevé, tunnel moins préféré. C'est logique, pas une vraie limitation.

---

**Question 10**: Deux routeurs avec tunnels GRE entre eux : Router-A destination = 10.2.2.2, Router-B destination = 10.1.1.1. De plus, chaque routeur n'a qu'un seul chemin vers l'autre routeur, qui utilise une route par défaut via Internet. Quel est le risque principal ?
- A) Les deux tunnels vont flood le lien WAN
- B) Les deux tunnels vont fonctionner normalement
- C) L'un des deux tunnels va entrer en boucle récursive
- D) Un tunnel va down toutes les heures

**Réponse**: C) L'un des deux tunnels va entrer en boucle récursive ✓
**Explication**: Si Router-A envoie trafic au tunnel destination (10.2.2.2) via le tunnel lui-même (boucle), routage récursif résulte. Besoin de route statique pour dest tunnel hors du tunnel.

---

## SECTION 2 : IPSEC FONDAMENTAUX (8 Questions)

**Question 11**: Lequel des 4 services de sécurité IPsec est fourni par Authentication Header (AH) seul ?
- A) Confidentiality (chiffrement)
- B) Integrity (intégrité) and Anti-replay
- C) Confidentiality + Integrity
- D) Aucun – AH est un protocole d'honneur

**Réponse**: B) Integrity (intégrité) and Anti-replay ✓
**Explication**: AH fornit souvent l'authentification Et l'intégrité des données, avec détection de rejeu. Pas de chiffrement.

---

**Question 12**: RFC numéro pour le protocole Encapsulating Security Payload (ESP) ?
- A) RFC 2402
- B) RFC 2406
- C) RFC 3686
- D) RFC 2409

**Réponse**: B) RFC 2406 ✓
**Explication**: RFC 2406 définit ESP. RFC 2402 = AH. RFC 2409 = IKEv1. RFC 3686 = IV explicite pour AES.

---

**Question 13**: Mode IPsec où l'en-tête IP original est entièrement encapsulé et chiffré ?
- A) Transport mode
- B) Tunnel mode
- C) Encapsulation mode
- D) Header security mode

**Réponse**: B) Tunnel mode ✓
**Explication**: Tunnel mode = tout paquet original (IP + payload) encapsulé/chiffré. Standard VPN site-to-site. Transport = paquet original IP visible, payload seulement chiffré.

---

**Question 14**: Quel algorithme de chiffrement est recommandé NIST FIPS 197 et devrait être utilisé pour tous les nouveaux déploiements ?
- A) DES
- B) 3DES
- C) AES
- D) IDEA

**Réponse**: C) AES ✓
**Explication**: AES (Rijndael) est le standard moderne FIPS 197 recommandé. DES/3DES obsolètes. IDEA peu commun.

---

**Question 15**: Quel est le problème avec MD5 comme algorithme de hachage pour IPsec ?
- A) Trop rapide, soupconne de faiblesse
- B) Collisions cryptographiques connues et démontrées
- C) Seule 56-bit de sécurité
- D) Pas de support multi-fournisseur

**Réponse**: B) Collisions cryptographiques connues et démontrées ✓
**Explication**: MD5 a des collisions documentées depuis des années. SHA-1 ou mieux requis pour sécurité moderne.

---

**Question 16**: Protocole asymétrique pour l'échange de clés permettant deux parties de générer une clé secrète partagée sur un canal non-sécurisé ?
- A) RSA
- B) Diffie-Hellman
- C) HMAC
- D) Pre-Shared Key

**Réponse**: B) Diffie-Hellman ✓
**Explication**: Diffie-Hellman permet établissement de clé secrète partagée sans que le secret soit jamais transmis. RSA = signatures. PSK = password partagé.

---

**Question 17**: IKEv1 négociation se déroule en combien de phases ?
- A) 1 phase
- B) 2 phases
- C) 3 phases
- D) Continu sans phases

**Réponse**: B) 2 phases ✓
**Explication**: Phase 1 = authentification + établir clé session. Phase 2 = négocier transform sets pour IPsec.

---

**Question 18**: Quel est l'avantage principal d'IKEv2 par rapport à IKEv1 ?
- A) IKEv2 supporte plus d'algorithmes de chiffrement
- B) IKEv2 phases soient fusionnées, plus efficace (+ meilleure mobilité)
- C) IKEv2 utilise moins de bande passante
- D) IKEv1 est plus moderne

**Réponse**: B) IKEv2 phases soient fusionnées, plus efficace (+ meilleure mobilité) ✓
**Explication**: IKEv2 (RFC 7296) combine et simplifie les phases, plus efficace. Meilleur MOBIKE support pour roaming.

---

## SECTION 3 : TRANSFORM SETS ET NÉGOCIATION (4 Questions)

**Question 19**: Une transform set IPsec spécifie ESP-AES-256 + ESP-SHA256-HMAC mode tunnel. C'est une combinaison :
- A) Invalide
- B) Valide et recommandée (EXCELLENTE)
- C) Valide mais AES + SHA ne vont pas ensemble
- D) Valide mais avec overhead excessif

**Réponse**: B) Valide et recommandée (EXCELLENTE) ✓
**Explication**: ESP (chiffrement + intégrité) + AES-256 (chiffrement) + SHA-256 (hachage) = combo moderne recommandée pour tous les nouveaux VPN.

---

**Question 20**: Vue sûr que cette transform set : AH-MD5 seul (pas ESP). C'est:
- A) Non valide – AH seul ne supporte pas IPsec
- B) Valide mais fourni très faible sécurité (MD5 compromis)
- C) Valide pour confidentiality contrairement aux apparences
- D) Valide but meilleur avec 3DES ajouté

**Réponse**: B) Valide mais fourni très faible sécurité (MD5 compromis) ✓
**Explication**: AH-MD5 seul = intégrité seulement, sans chiffrement. MD5 cassable. Valide techniquement, terrible en pratique. Obsolète.

---

**Question 21**: Une SA IPsec bidirectionnelle se compose de combien de SAs (Security Associations) unidirectionnels ?
- A) 1 (partagée dans les deux sens)
- B) 2 (un pour chaque direction)
- C) 3 (IKE + 2 IPsec)
- D) Dépend si tunnel ou transport

**Réponse**: B) 2 (un pour chaque direction) ✓
**Explication**: Chaque SA est unidirectionnel. Un tunnel bidirectionnnel = 2 SAs (outbound + inbound).

---

**Question 22**: During IKE Phase 1, les deux peers échangent :
- A) Les transform sets pour IPsec
- B) Les certificats ou PSK pour authentification + établir clé session
- C) Les données de trafic encrypté
- D) Les numéros SPI pour IPsec

**Réponse**: B) Les certificats ou PSK pour authentification + établir clé session ✓
**Explication**: Phase 1 = auth peer + établir une clé de session partagée via DH. Phase 2 = négocier algos.

---

## SECTION 4 : SCÉNARIOS COMPLEXES (3 Questions)

**Question 23**: Vous configurez un VPN site-to-site GRE + IPsec. GRE fournit :
- A) Chiffrement du tunnel
- B) Encapsulation (tunnelisation) du trafic
- C) Authentification du peer
- D) Anti-rejeu

**Réponse**: B) Encapsulation (tunnelisation) du trafic ✓
**Explication**: GRE = encapsulation. IPsec fournit = chiffrement + authentification + intégrité + anti-rejeu. Les deux ensembles.

---

**Question 24**: Vous avez deux VPN : Tunnel A avec AES-128 + SHA-1, Tunnel B avec AES-256 + SHA-256. Supposant qu'aucune des deux n'a de failles connues, lequel est le plus robuste contre les menaces futures ?
- A) Tunnel A (plus simple = moins de variables)
- B) Tunnel B (clés plus fortes, hash plus fort)
- C) Egalité de sécurité
- D) Dépend de la bande passante disponible

**Réponse**: B) Tunnel B (clés plus fortes, hash plus fort) ✓
**Explication**: AES-256 > AES-128. SHA-256 > SHA-1. Tunnel B a plus de marge de sécurité future-proof.

---

**Question 25**: Un administrateur doit choisir entre GRE seul (pas IPsec) et IPsec tunnel pour connecter deux datacenters. GRE seul est acceptable si :
- A) Les deux datacenters existent dans le même bâtiment physique
- B) Le lien réseau est déjà sur un réseau LAN privé (pas Internet)
- C) Seule confidentiality vient de l'application (IPsec non requise)
- D) Toutes les réponses ci-dessus

**Réponse**: D) Toutes les réponses ci-dessus ✓
**Explication**: GRE sans chiffrement OK si trafic n'a déjà pas besoin de confidentiality (LAN privé, application chiffre datos). Internet public = IPsec obligatoire.

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. C | 2. B | 3. B | 4. C | 5. B
6. C | 7. B | 8. B | 9. B | 10. C
11. B | 12. B | 13. B | 14. C | 15. B
16. B | 17. B | 18. B | 19. B | 20. B
21. B | 22. B | 23. B | 24. B | 25. D

---

## GUIDE D'ÉVALUATION

- **20-25 correctes** (80-100%): Excellent - Maîtrise des overlays
- **16-19 correctes** (64-76%): Bon - Domaines à consolider
- **12-15 correctes** (48-60%): Moyen - Révision GRE/IPsec requise
- **< 12 correctes** (< 48%): Faible - Étude approfondie recommandée

---

*QCM Révision Module 16 - CCNP ENCOR v8*
