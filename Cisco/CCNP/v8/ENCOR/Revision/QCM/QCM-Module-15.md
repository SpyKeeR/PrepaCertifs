# QCM Module 15 : Services IP
## 25 Questions - Révision Complète

---

## SECTION 1 : NTP ET STRATUM (5 Questions)

**Question 1**: Quel stratum NTP représente une horloge atomique ou un récepteur GPS ?
- A) Stratum 0
- B) Stratum 1
- C) Stratum 2
- D) Stratum 10

**Réponse**: A) Stratum 0 ✓
**Explication**: Stratum 0 est la source de référence absolue (atomique ou GPS). Aucun périphérique NTP n'est stratum 0 – c'est juste la source externe. Un stratum 1 se connecte directement à une horloge stratum 0.

---

**Question 2**: Un routeur Cisco sans synchronisation NTP announcera quel stratum par défaut s'il est configuré comme serveur NTP ?
- A) Stratum 1
- B) Stratum 8
- C) Stratum 10
- D) Stratum 16

**Réponse**: C) Stratum 10 ✓
**Explication**: Par défaut, un routeur non synchronisé avec `ntp master` utilise stratum 8. Si on veut empêcher explicitement d'autres appareilsdde s'y synchroniser, configurer stratum 10 ou plus est recommandé.

---

**Question 3**: Combien de temps NTP a-t-il généralement besoin pour converger à une précision stable (dizaines de millisecondes) après le démarrage d'un routeur ?
- A) 1-2 minutes
- B) 5-10 minutes
- C) Plusieurs heures à plusieurs jours
- D) NTP atteint la précision immédiatement

**Réponse**: C) Plusieurs heures à plusieurs jours ✓
**Explication**: NTP effectue des ajustements graduels de l'horloge. Un routeur avec une dérive initiale importante peut mettre 24 heures ou plus pour converger. Une convergence rapide (quelques heures) est typique dans de bons conditions.

---

**Question 4**: Quel mot-clé configure un serveur NTP comme le serveur préféré dans un groupe ?
- A) `ntp server 10.1.1.1 priority`
- B) `ntp server 10.1.1.1 prefer`
- C) `ntp server 10.1.1.1 primary`
- D) `ntp server 10.1.1.1 best`

**Réponse**: B) `ntp server 10.1.1.1 prefer` ✓
**Explication**: Le mot-clé `prefer` marque un serveur comme préféré. NTP sélectionnera ce serveur en priorité s'il est accessible.

---

**Question 5**: Quelle commande affiche les associations NTP actuelles incluant le statut de chaque serveur ?
- A) `show ntp servers`
- B) `show ntp status`
- C) `show ntp associations`
- D) `show ntp peers`

**Réponse**: C) `show ntp associations` ✓
**Explication**: `show ntp associations` affiche l'état de chaque serveur/peer avec delay, offset, reach, stratum. `show ntp status` affiche seulement l'état global.

---

## SECTION 2 : PROTOCOLES DE REDONDANCE (8 Questions)

**Question 6**: Quel est le rôle principal d'un protocole de redondance du premier saut (FHRP) ?
- A) Fournir une adresse IP virtuelle partagée entre routeurs
- B) Encrypter le trafic entre routeurs
- C) Équilibrer la charge entre interfaces
- D) Réduire la latence RTT du réseau

**Réponse**: A) Fournir une adresse IP virtuelle partagée entre routeurs ✓
**Explication**: Les FHRP (HSRP, VRRP, GLBP) créent une VIP partagée que les hôtes utilisent comme passerelle par défaut. En cas de défaillance du routeur actif, un routeur standby prend en charge sans interruption pour les hôtes.

---

**Question 7**: Quel FHRP est un standard de l'industrie RFC (non propriétaire Cisco) et fonctionne sur plusieurs fournisseurs ?
- A) HSRP
- B) VRRP
- C) GLBP
- D) RRSP

**Réponse**: B) VRRP ✓
**Explication**: VRRP est défini dans RFC 3768 et fonctionne sur Cisco, Juniper, Mikrotik et autres. HSRP et GLBP sont propriétaires Cisco.

---

**Question 8**: Par défaut, HSRP est-il préemptif ou non-préemptif ?
- A) Préemptif (routeur priorité haute reprend immédiatement après redémarrage)
- B) Non-préemptif (routeur actif conserve son rôle même si priorité inférieure)
- C) Dynamiquement configurable selon un timer
- D) Préemptif uniquement en HSRPv2

**Réponse**: B) Non-préemptif ✓
**Explication**: Par défaut, HSRP ne change pas l'actif une fois établi. Le routeur actuellement actif conserve son rôle même s'il a une priorité inférieure au routeur redémarré. `standby preempt` active la préemption.

---

**Question 9**: Quel est l'intervalle de hello par défaut d'HSRP et le timeout (hold time) par défaut ?
- A) Hello 1s, Hold 3s
- B) Hello 3s, Hold 10s
- C) Hello 5s, Hold 15s
- D) Hello 10s, Hold 30s

**Réponse**: B) Hello 3s, Hold 10s ✓
**Explication**: Les timers par défaut HSRP sont 3 secondes pour les hellos multicast et 10 secondes pour le hold time (délai d'attente avant basculement).

---

**Question 10**: Deux routeurs HSRP ont la même priorité (100). Comment l'élection du routeur actif est-elle tranchée ?
- A) Interface avec MAC le plus élevé gagne
- B) Interface avec adresse IP la plus élevée du groupe gagne
- C) Ordre de configuration dans la commande
- D) Appareil qui démarre en premier gagne

**Réponse**: B) Interface avec adresse IP la plus élevée du groupe gagne ✓
**Explication**: Quand les priorités sont égales, HSRP utilise l'adresse IP de l'interface comme tiebreaker. L'adresse IP la plus élevée gagne.

---

**Question 11**: Object Tracking dans HSRP permet de faire quoi ?
- A) Seulement afficher l'état des interfaces
- B) Tracker des conditions réseau spécifiques et ajuster la priorité HSRP
- C) Encrypter les messages HSRP
- D) Augmenter automatiquement la bande passante

**Réponse**: B) Tracker des conditions réseau spécifiques et ajuster la priorité HSRP ✓
**Explication**: Object Tracking lie les décisions HSRP à des conditions. Par exemple, si une route BGP se baisse, réduire la priorité automatiquement. Configuration: `track 10 ip route X.X.X.X reachability` puis `standby 1 track 10 decrement 30`.

---

**Question 13**: GLBP se différencie de HSRP et VRRP principalement par :
- A) Supp IPv6 uniquement
- B) Mécanisme de détection défaillance unique
- C) Capacité à équilibrer la charge entre plusieurs routeurs actifs
- D) Utilisation d'une MAC virtuelle propriétaire

**Réponse**: C) Capacité à équilibrer la charge entre plusieurs routeurs actifs ✓
**Explication**: GLBP (Gateway Load Balancing Protocol) est unique car il permet plusieurs routeurs actifs simultanément, distribuant le trafic vers la VIP parmi eux. HSRP et VRRP ne ont qu'un seul actif.

---

## SECTION 3 : NAT (6 Questions)

**Question 14**: Quel type de NAT crée une cartographie permanente 1:1 d'une adresse privée à une adresse publique ?
- A) NAT dynamique
- B) NAT statique
- C) PAT
- D) NAT bidirectionnel

**Réponse**: B) NAT statique ✓
**Explication**: NAT statique: une adresse interne = toujours la même adresse externe. Idéal pour serveurs Web ou FTP qui doivent rester accessibles par une adresse fixe.

---

**Question 15**: Quel est le terme pour la traduction NAT "many-to-one" où plusieurs adresses privées partagent une seule adresse publique en variant les ports ?
- A) NAT statique
- B) NAT dynamique
- C) PAT (Port Address Translation)
- D) Static NAT avec pool

**Réponse**: C) PAT (Port Address Translation) ✓
**Explication**: PAT permet à 65535 connexions simultanées de partager une seule IP publique en utilisant des variantes de ports. Configuration: `ip nat inside source list <ACL> interface <interface> overload`.

---

**Question 16**: Qu'est-ce que l'adresse "inside global" dans la terminologie NAT ?
- A) Véritable adresse IP d'un serveur interne
- B) Adresse IP en laquelle un client interne est traduit côté réseau externe
- C) Adresse IP d'un hôte externe
- D) MAC adresse de l'interface inside

**Réponse**: B) Adresse IP en laquelle un client interne est traduit côté réseau externe ✓
**Explication**: Inside global = adresse NAT publique vue par le réseau externe. Par exemple, client interne 192.168.1.50 (inside local) traduit à 203.0.113.50 (inside global).

---

**Question 17**: Quelle commande enverrouille les interfaces d'un routeur comme "inside" (privée) pour NAT ?
- A) `interface ip nat private`
- B) `ip nat specify inside`
- C) `ip nat inside`
- D) `nat set interface inside`

**Réponse**: C) `ip nat inside` ✓
**Explication**: La commande `ip nat inside` est configurée sous une interface pour indiquer qu'elle est côté réseau privé. L'interface opposée recevrait `ip nat outside`.

---

**Question 19**: Pourquoi un administrateur pourrait-il choisir NAT statique plutôt que PAT pour un serveur Web public ?
- A) NAT statique est plus rapide
- B) NAT statique permet une adresse fixe connue pour l'accès externe stable
- C) PAT ne supporte pas les connexions entrantes
- D) NAT statique utilise moins de ressources

**Réponse**: B) NAT statique permet une adresse fixe connue pour l'accès externe stable ✓
**Explication**: Les serveurs publics (Web, DNS, SMTP) nécessitent une adresse IP stable pour que les clients externes puissent s'y connecter de manière prévisible. NAT statique garantit cette stabilité.

---

## SECTION 4 : DÉPANNAGE ET SCÉNARIOS (6 Questions)

**Question 20**: Un routeur devient un serveur NTP avec `ntp master 5`. Aucun autre routeur ne se synchronise avec lui. Quel est le problème probable ?
- A) Stratum 5 n'est pas valide (maximum stratum 3)
- B) Le port 123 UDP doit être autorisé dans les ACL
- C) Les autres routeurs ne peuvent pas le atteindre (ACL ou routage)
- D) `ntp source` n'a pas été configuré

**Réponse**: C) Les autres routeurs ne peuvent pas le atteindre (ACL ou routage) ✓
**Explication**: Stratum 5 est valide. La cause usuelle est une ACL bloquant port 123 UDP ou un problème de routage empêchant la connectivité vers le serveur NTP.

---

**Question 21**: Vous configurez HSRP avec priorité 110 sur Router-A et 100 sur Router-B. Après démarrage, Router-B devient actif. Pourquoi ?
- A) Vous avez d'abord configuré Router-B
- B) Router-A n'a pas terminé la convergence NTP
- C) Router-B redémarre généralement en premier après une panne
- D) Vous avez oublié d'activer `standby preempt` sur Router-A

**Réponse**: D) Vous avez oublié d'activer `standby preempt` sur Router-A ✓
**Explication**: Sans préemption, HSRP non-préemptif fait que Router-B reste actif s'il l'était avant. Ajouter `standby preempt` fait que Router-A reprend son rôle d'actif après redémarrage.

---

**Question 22**: Un client sur VLAN 100 configure passerelle par défaut VIP 192.168.1.1. Les routeurs HSRP sont configurés mais le client ne peut pas envoyer d'ARP pour la VIP. Quel est le problème probable ?
- A) La VIP doit être sur un sous-réseau différent du client
- B) La VIP n'est pas configurée sur les routeurs ou ne correspond pas à celle du client
- C) HSRP utilise toujours 224.0.0.102 pour les hellos
- D) Le client doit être sur le même VLAN que la MAC virtuelle

**Réponse**: B) La VIP n'est pas configurée sur les routeurs ou ne correspond pas à celle du client ✓
**Explication**: Si la VIP client ne correspond pas à `standby X ip`, les routeurs ne répondront jamais aux ARP pour cette adresse. Double-vérifier: `show standby` doit afficher la VIP correcte.

---

**Question 23**: Vous déployez NAT PAT sur un routeur. Les clients internes (192.168.1.0/24) accèdent Internet, mais un serveur interne (192.168.1.50) arrête de répondre aux connexions entrantes. Pourquoi ?
- A) PAT ne supporte pas les adresses de serveur
- B) Les connexions entrantes doivent être statiquement mappées ou traduites par une règle distincte
- C) Le serveur a besoin de sa propre adresse publique
- D) La VIP HSRP interfère

**Réponse**: B) Les connexions entrantes doivent être statiquement mappées ou traduites par une règle distincte ✓
**Explication**: PAT outbound traduit les connexions sortantes. Les connexions entrantes doivent utiliser NAT statique séparé. Configuration: `ip nat inside source static 192.168.1.50 203.0.113.50`.

---

**Question 24**: Object Tracking configure `track 10 ip route 192.168.0.0 255.255.0.0 reachability`. Si la route BGP devient inaccessible, le tracking devient "down". Mais le routeur HSRP ne bascule pas. Quel élément de config manque ?
- A) `show track 10` pour vérifier l'état
- B) Commande `standby <group> track <num> decrement <priority-value>`
- C) Configuration d'une ACL
- D) Augmenter le hold timer

**Réponse**: B) Commande `standby <group> track <num> decrement <priority-value>` ✓
**Explication**: Créer un track est seulement la première moitié. Il faut le lier à HSRP avec `standby 1 track 10 decrement 30` pour réduire la priorité quand le track échoue.

---

**Question 25**: Un administrateur doit assurer que deux routeurs HSRP (priorité 100 respectivement sur chaque) se partagent équitablement le trafic. Quel protocole FHRP ferait cela sans configurations complexes ?
- A) HSRP avec deux groupes
- B) VRRP avec priorité égale
- C) GLBP avec deux routeurs comme AVG/AVF
- D) PAT avec répartition de charge

**Réponse**: C) GLBP avec deux routeurs comme AVG/AVF ✓
**Explication**: GLBP (Gateway Load Balancing Protocol) distribue le trafic VIP entre plusieurs routeurs actifs simultanément. HSRP et VRRP n'ont qu'un seul actif par groupe.

---

## CLÉS DE RÉPONSE RÉSUMÉ

1. A | 2. C | 3. C | 4. B | 5. C
6. A | 7. B | 8. B | 9. B | 10. B
11. B | 12. C | 13. C | 14. B | 15. C
16. B | 17. C | 18. B | 19. C | 20. C
21. D | 22. B | 23. B | 24. B | 25. C

---

## GUIDE D'ÉVALUATION

- **20-25 correctes** (80-100%): Excellent - Maîtrise du Module 15
- **16-19 correctes** (64-76%): Bon - Domaines à consolider
- **12-15 correctes** (48-60%): Moyen - Révision requise sur NTP/FHRP/NAT
- **< 12 correctes** (< 48%): Faible - Étude approfondie recommandée

---

*QCM Révision Module 15 - CCNP ENCOR v8*
