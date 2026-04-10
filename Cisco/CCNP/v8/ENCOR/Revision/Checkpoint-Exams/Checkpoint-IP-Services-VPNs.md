# Checkpoint 6 : IP Services & VPNs
## Examen Complet (50 Questions - 90 minutes)

---

## SECTION 1 : NTP ET REDONDANCE PREMIER SAUT (Q1-Q20)

**Question 1**: Décrire stratum NTP hierarchy. Quels strata représentent source temps absolue ?
- A) Stratum 0 (horloges atomiques, pas appareils physiques WAN)
- B) Stratum 1 (directement atomiques)
- C) Stratum 2 (universellement atomiques)
- D) Stratums 0-5 (tous source absolue)

**Réponse**: A) Stratum 0 ✓

---

**Question 2**: Combien de heures/jours un routeur non-synchronisé NTP prend typiquement converger à précision stable ?
- A) < 5 minutes
- B) 30 minutes - 2 heures
- C) Plusieurs heures à plusieurs jours
- D) Instantané après première sync

**Réponse**: C) Plusieurs heures à plusieurs jours ✓

---

**Question 3**: Configuration NTP routeur : `ntp server 10.1.1.1 prefer` résultat quoi ?
- A) Serveur sélectionné comme première tentative
- B) Serveur marqué préféré, utilisé priorité si accessible
- C) Seul serveur autorisé
- D) Serveur actif seulement après 10 autres échouent

**Réponse**: B) Serveur marqué préféré, utilisé priorité si accessible ✓

---

**Question 4**: Commande configurer NTP source interface sortante :
- A) `ntp interface GigabitEthernet0/0/0`
- B) `ntp source GigabitEthernet0/0/0`
- C) `ntp interface-source 0/0/0`
- D) `interface tunnel 0` puis `ntp bind`

**Réponse**: B) `ntp source GigabitEthernet0/0/0` ✓

---

**Question 5**: Périphérique config `ntp master 5` sans sync externe. Problème :
- A) Stratum 5 trop bas (invalide)
- B) Stratum 5 acceptable mais autres routeurs dépendent horloge faible
- C) Exige serieu interface loopback
- D) Requiert configuration HSRP complémentaire

**Réponse**: B) Stratum 5 acceptable mais autres routeurs dépendent horloge faible ✓

---

**Question 6**: FHRP problème fondamental résolu :
- A) Améliorer vitesse routeur
- B) Aider clients trouver passerelle passante si hardware défaille
- C) Chiffrer trafic
- D) Augmenter bande passante interface

**Réponse**: B) Aider clients trouver passerelle passante si hardware défaille ✓

---

**Question 7**: Trois FHRP options standards. Lequel SEUL offre load-balancing trafic outbound ?
- A) HSRP
- B) VRRP
- C) GLBP
- D) Aucun standard ne load-balance

**Réponse**: C) GLBP ✓

---

**Question 8**: Election HSRP groupée : deux routeurs priorité identique (100). Tiebreaker ?
- A) Interface physique MAC le plus haut
- B) Adresse IP interface HSRP plus haute
- C) Ordre apparition dans config
- D) Dernier routeur rebooté

**Réponse**: B) Adresse IP interface HSRP plus haute ✓

---

**Question 9**: HSRP non-preemptive (defaut) signifie :
- A) Routeur priorité basse jamais devient actif
- B) Routeur actuellement actif reste actif même si priorité inférieure à nouveau boot
- C) Préemption sécurisée par encryption
- D) Désactive groupes HSRP multiples

**Réponse**: B) Routeur actuellement actif reste actif même si priorité inférieure à nouveau boot ✓

---

**Question 10**: Commande HSRP basic : `standby 1 ip 192.168.1.1`. Ceci configure :
- A) IP interface physique
- B) IP virtuelle (VIP) du groupe 1
- C) IP destination next-hop
- D) IP serveur NTP HSRP

**Réponse**: B) IP virtuelle (VIP) du groupe 1 ✓

---

**Question 11**: Object Tracking pour HSRP peut tracker quoi ?
- A) Seulement l'interface physique
- B) Reachability route, interface line-protocol, autre conditions
- C) Pas de condition (HSRP standalone décide)
- D) Interface uniquement, pas routes

**Réponse**: B) Reachability route, interface line-protocol, autre conditions ✓

---

**Question 12**: Configuration Object Tracking : `track 10 ip route 0.0.0.0/0 reachability`. Si route inaccessible, track 10 devient :
- A) Up (routes down usually okay)
- B) Down (route unreachable)
- C) Pending (awaits next poll)
- D) Fluctuating

**Réponse**: B) Down (route unreachable) ✓

---

**Question 13**: `standby 1 track 10 decrement 30`. Si track 10 down, HSRP priorité diminue :
- A) À zéro (immédiat failover)
- B) De 30 points (priorité 100 → 70)
- C) À 10% valeur original
- D) Jusqu'à stratum NTP change

**Réponse**: B) De 30 points (priorité 100 → 70) ✓

---

**Question 14**: Vérification HSRP status via :
- A) `show hsrp`
- B) `show standby brief`
- C) `show hsrp interface GigabitEthernet0/0/0`
- D) Tous ci-dessus affichent données útiles

**Réponse**: D) Tous ci-dessus affichent données útiles ✓

---

**Question 15**: NAT Static mapping :
- A) Crée pool d'addresses publiques pour clients internes
- B) 1:1 permanente de adresse privée unique → publique
- C) Many-to-one partageant port variation
- D) Trafic bidirectionnel illimité

**Réponse**: B) 1:1 permanente de adresse privée unique → publique ✓

---

**Question 16**: PAT (Port Address Translation) dans NAT utile pour :
- A) Un seule adresse publique servir centaines clients internes
- B) Augmenter sécurité encryption
- C) Réduire latence réseau
- D) Améliorer qualité voix

**Réponse**: A) Un seule adresse publique servir centaines clients internes ✓

---

**Question 17**: Configuration NAT : designate `inside` interface vs `outside`. Raison ?
- A) Seulement pour documentation
- B) Dire NAT quelle direction traduire (inside→outside)
- C) Appliquer ACLs différentes
- D) Optimiser MTU

**Réponse**: B) Dire NAT quelle direction traduire (inside→outside) ✓

---

**Question 18**: Dépannage HSRP : deux APs HSRP. Aucun n'affiche état « Active ». Probable cause :
- A) NTP non-synchronisé
- B) Priorité identiques + non-preempt = Standby seulement (pas Active jamais élu)
- C) Interface MTU trop petit
- D) OSPF metric incompatible

**Réponse**: B) Priorité identiques + non-preempt = Standby seulement (pas Active jamais élu) ✓

---

**Question 19**: NTP paquet timeout/reliability sans SNMP. Check quoi pour vérifier ?
- A) `debug ntp` (verbeux)
- B) `show ntp status` + `show ntp associations`
- C) `show ip route ntp`
- D) Interrogation RADIUS  

**Réponse**: B) `show ntp status` + `show ntp associations` ✓

---

**Question 20**: Routeur HSRP préemption désactivé. Routeur actuel crash, reboots. Quoi se passe ?
- A) Automatique prend rôle actif (si priorité haute)
- B) Reste passif bien que haute priorité (preempt off)
- C) Entrer loop instabilité
- D) Attend manuel admin restart

**Réponse**: A) Automatique prend rôle actif (si priorité haute) ✓

---

## SECTION 2 : TUNNELS GRE & IPSEC (Q21-Q50)

**Question 21**: GRE tunnel protocole IP number :
- A) 6 (TCP)
- B) 17 (UDP)
- C) 47 (GRE)
- D) 50 (ESP)

**Réponse**: C) 47 (GRE) ✓

---

**Question 22**: GRE tunnel encapsule quel protocole(s) ?
- A) Uniquement IPv4
- B) Uniquement IPv6
- C) N'importe quel protocole couche réseau (IPv4, IPv6, AppleTalk, etc)
- D) Uniquement protocoles routés

**Réponse**: C) N'importe quel protocole couche réseau ✓

---

**Question 23**: Configuration tunnel GRE étapes obligatoires. Laquelle est FAUSSE ?
- A) `interface tunnel 0`
- B) `tunnel source <IP>`
- C) `tunnel destination <IP>`
- D) `bandwidth 1000000` (obligatoire pour vit normal)

**Réponse**: D) `bandwidth 1000000` (obligatoire pour vit normal) ✓

---

**Question 24**: Problème « routage récursif » dans GRE signifie :
- A) Tunnel packet destination également accessible via tunnel
- B) Tunnel crée boucles physiques multiples
- C) Trafic fragmente infiniment
- D) Keepalive échoue

**Réponse**: A) Tunnel packet destination également accessible via tunnel ✓

---

**Question 25**: Mitigation routage récursif GRE :
- A) Augmenter keepalive timer
- B) Route statique dest tunnel via interface physique (pas tunnel)
- C) Réduire MTU tunnel
- D) Activation encryption IPsec

**Réponse**: B) Route statique dest tunnel via interface physique (pas tunnel) ✓

---

**Question 26**: MTU recommandé tunnel GRE pour évitter fragmentation :
- A) 512 octets
- B) 1000 octets
- C) 1400 octets
- D) 1500 octets

**Réponse**: C) 1400 octets ✓

---

**Question 27**: Vérification tunnel GRE :
- A) `show tunnel` (pas correct syntax)
- B) `show interface tunnel 0`
- C) `show gre tunnels`
- D) `show ip gre`

**Réponse**: B) `show interface tunnel 0` ✓

---

**Question 28**: IPsec 4 services sécurité incluent :
- A) Authentification peer, Confidentiality, Integrity, Anti-replay
- B) Juste chiffrement
- C) Authentification seulement
- D) Compression données

**Réponse**: A) Authentification peer, Confidentiality, Integrity, Anti-replay ✓

---

**Question 29**: AH (Authentication Header) fournit :
- A) Chiffrement uniquement
- B) Intégrité + Anti-replay (pas confidentiality)
- C) Confidentiality + Integrity
- D) Non-répudiation

**Réponse**: B) Intégrité + Anti-replay (pas confidentiality) ✓

---

**Question 30**: ESP (Encapsulating Security Payload) dans IPsec offre :
- A) Authentification seulement
- B) Chiffrement seulement
- C) Confidentiality + Intégrité (si HMAC ajouté)
- D) Aucune sécurité (data plane seulement)

**Réponse**: C) Confidentiality + Intégrité (si HMAC ajouté) ✓

---

**Question 31**: Mode IPsec où paquet IP original entièrement encapsulé et chiffré :
- A) Transport mode
- B) Tunnel mode
- C) Encapsulation mode
- D) Hybrid mode

**Réponse**: B) Tunnel mode ✓

---

**Question 32**: Algorithme chiffrement recommandé NIST FIPS 197 pour IPsec :
- A) DES (56-bit)
- B) 3DES (168-bit)
- C) AES (128/192/256-bit)
- D) IDEA

**Réponse**: C) AES (128/192/256-bit) ✓

---

**Question 33**: MD5 problème comme algorithme hash IPsec :
- A) Trop rapide (sécurité faible)
- B) Collisions cryptographiques connues
- C) Format incompatible HMAC
- D) Compatible seulement 32-bit systems

**Réponse**: B) Collisions cryptographiques connues ✓

---

**Question 34**: Diffie-Hellman dans IPsec utile pour :
- A) Chiffrer données client
- B) Establir clé secrète partagée sur canal non-sécurisé
- C) Authentification peer
- D) Hacher données pour integrity

**Réponse**: B) Establir clé secrète partagée sur canal non-sécurisé ✓

---

**Question 35**: Pre-Shared Key (PSK) dans IPsec :
- A) Clé générée dynamiquement per session
- B) Clé secrète manuellement configurée partagée entre peers
- C) Public key dans X.509 certificate
- D) Une des 5 clés simultanés per SA

**Réponse**: B) Clé secrète manuellement configurée partagée entre peers ✓

---

**Question 36**: IKEv1 phases IPsec SA negotiation :
- A) 1 phase (unified)
- B) 2 phases (Phase 1 auth, Phase 2 crypto negotiate)
- C) 3 phases
- D) Continu sans phases

**Réponse**: B) 2 phases (Phase 1 auth, Phase 2 crypto negotiate) ✓

---

**Question 37**: IKEv2 améliorat principal comparé IKEv1 :
- A) Plus d'algorithmes supportés
- B) Phases fusionnées, plus efficace + meilleur mobilité support
- C) Plus puissant encryption
- D) Utilise moins bande passante pour header

**Réponse**: B) Phases fusionnées, plus efficace + meilleur mobilité support ✓

---

**Question 38**: Transform set IPsec combine :
- A) Juste chiffrement
- B) Juste authentification
- C) Algorithmes sécurité (proto + algo) approuvés pour VPN
- D) Paramètres QoS tunneling

**Réponse**: C) Algorithmes sécurité (proto + algo) approuvés pour VPN ✓

---

**Question 39**: Combo transform set valide :
- A) AES-256 + SHA-256 ESP mode tunnel
- B) DES seul (legacy acceptable)
- C) 3DES + MD5 (modern)
- D) AH seulement sans espacement

**Réponse**: A) AES-256 + SHA-256 ESP mode tunnel ✓

---

**Question 40**: Security Association (SA) IPsec :
- A) Connectement seulement une direction (bidirectionnel = 2 SAs)
- B) Toujours bidirectionnel (une SA sert 2 directions)
- C) 3per tunnel
- D) Illimité par session

**Réponse**: A) Connectement seulement une direction (bidirectionnel = 2 SAs) ✓

---

**Question 41**: GRE vs IPsec choix : GRE seulement (pas IPsec) acceptable si :
- A) Jamais acceptable (toujours IPsec required)
- B) Transport sur LAN privé (no confidentiality need)
- C) Trafic chiffré par application (IPsec redundant)
- D) Réponses B et C

**Réponse**: D) Réponses B et C ✓

---

**Question 42**: VXLAN est overlay protocol pour :
- A) L3 IP (comme GRE)
- B) L2 Ethernet frames (datacenter)
- C) Seulement IPv6
- D) Wireless networks

**Réponse**: B) L2 Ethernet frames (datacenter) ✓

---

**Question 43**: Tunnel GRE configuration minimal fonctionnel :
- A) Source + Destination tunelabel addresses required
- B) Source, Destination, interface IP address required
- C) Plus 7 étapes optionnelles
- D) Juste `interface tunnel 0`

**Réponse**: B) Source, Destination, interface IP address required ✓

---

**Question 44**: GRE tunnel "up" status dépend :
- A) Source/Destination routables + bidirectionnel ping
- B) Seulement source reachable
- C) Cloud provider connectivity
- D) NTP time sync

**Réponse**: A) Source/Destination routables + bidirectionnel ping ✓

---

**Question 45**: Sélection d'algorithme chiffrement pour nouvel IPsec VPN :
- A) DES (fastest)
- B) 3DES (balance)
- C) AES-256 (recommandé modern)
- D) IDEA (propriétaire Cisco)

**Réponse**: C) AES-256 (recommandé modern) ✓

---

**Question 46**: Combination transform set ESP seul :
- A) Invalide, AH required toujours
- B) Valide, ESP fourni entrambi chiffrement et integrity
- C) Valide seulement pour client host
- D) Dépend mode tunnel/transport

**Réponse**: B) Valide, ESP fourni entrambi chiffrement et integrity ✓

---

**Question 47**: IPv4 tunnel transport (underlay) avec IPv6 payload (overlay) cas d'usage :
- A) Impossible
- B) Transition IPv6: nouveau services IPv6 sur infrastructure IPv4 existante
- C) Performance boost
- D) Réduire fragmentationfragmentation

**Réponse**: B) Transition IPv6: nouveau services IPv6 sur infrastructure IPv4 existante ✓

---

**Question 48**: LISP vs GRE principales differences :
- A) GRE = simplifié, LISP = architecture separating ID/Location
- B) GRE = chiffrement, LISP = pas chiffrement
- C) Identiques functionality
- D) LISP = legacy, GRE = modern

**Réponse**: A) GRE = simplifié, LISP = architecture separating ID/Location ✓

---

**Question 49**: Tunnel GRE responsabilité de chiffrement :
- A) GRE seul chiffre
- B) GRE ne chiffre pas (IPsec requise pour confidentiality)
- C) Optional basé sur vendor
- D) Client negotiate avec GRE

**Réponse**: B) GRE ne chiffre pas (IPsec requise pour confidentiality) ✓

---

**Question 50**: Récommandation sécurité : pour productio VPN site-to-site sensible données :
- A) GRE seul suffisant
- B) GRE + IPsec (overlay + encryption)
- C) IPsec uniquement (sans GRE)
- D) PAT uniquement sur firewall

**Réponse**: B) GRE + IPsec (overlay + encryption) ✓

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. A | 2. C | 3. B | 4. B | 5. B
6. B | 7. C | 8. B | 9. B | 10. B
11. B | 12. B | 13. B | 14. D | 15. B
16. A | 17. B | 18. B | 19. B | 20. A
21. C | 22. C | 23. D | 24. A | 25. B
26. C | 27. B | 28. A | 29. B | 30. C
31. B | 32. C | 33. B | 34. B | 35. B
36. B | 37. B | 38. C | 39. A | 40. A
41. D | 42. B | 43. B | 44. A | 45. C
46. B | 47. B | 48. A | 49. B | 50. B

---

## GUIDE ÉVALUATION

| Score | Interprétation |
|-------|-----------------|
| **45-50** (90-100%) | Excellent - PASS examen |
| **40-44** (80-89%) | Bon - PASS, révision avant test |
| **35-39** (70-79%) | Acceptable - PASS marginale, étude supplémentaire |
| **< 35** (< 70%) | Fail - Répétition requise, étude approfondie |

---

*Checkpoint 6 Examen Complet - CCNP ENCOR Modules 15-16*
