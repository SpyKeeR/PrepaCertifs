# QCM Module 12 : Advanced BGP

## Questions 1-10

### Q1 : Quel est le type de multihoming RECOMMANDÉ pour une entreprise ?
**A)** Connexion sans ASN propre  
**B)** Connexion avec ASN unique propre à plusieurs ISP  
**C)** Connexion avec plusieurs ASN (un par ISP)  
**D)** Aucun multihoming n'est recommandé  

**Réponse : B** - **Multihoming avec ASN unique propre** donne le contrôle maximal des politiques de routage et est recommandé.

---

### Q2 : Quel est le rôle principal de l'ORF (Outbound Route Filtering) ?
**A)** Filtrer les routes annoncées sortantes  
**B)** Communiquer au voisin quels préfixes on désire recevoir  
**C)** Filtrer le trafic en temps réel  
**D)** Augmenter le weight des routes  

**Réponse : B** - **ORF** permet à un routeur de signaler aux voisins les préfixes qu'il désire recevoir, évitant le transit involontaire.

---

### Q3 : Quelle est la MEILLEURE pratique pour filtrer les préfixes BGP ?
**A)** Access lists standard  
**B)** Access lists étendues  
**C)** Prefix lists  
**D)** Community lists seulement  

**Réponse : C** - **Prefix lists** sont la meilleure pratique BGP car elles supportent ge/le pour plages de longueur.

---

### Q4 : Quel symbole regex BGP représente le début d'un AS_Path ?
**A)** `*`  
**B)** `^`  
**C)** `$`  
**D)** `_`  

**Réponse : B** - **`^`** représente le début du chemin (AS adjacent).

---

### Q5 : Dans une route map BGP, que fait `match ip address prefix-list` ?
**A)** Match la source uniquement  
**B)** Match le préfixe de destination announcé  
**C)** Match l'adresse du voisin  
**D)** Match le Next Hop  

**Réponse : B** - **`match ip address prefix-list`** teste le préfixe announcé contre la prefix-list.

---

### Q6 : Quel parameter de prefix-list filtre les routes de /25 à /32 ?
**A)** `ge 25 le 32`  
**B)** `ge 25`  
**C)** `le 32`  
**D)** `range 25-32`  

**Réponse : A** - **`ge 25 le 32`** accepte les préfixes avec longueur 25-32 bits.

---

### Q7 : Quel attribut BGP tagge les routes pour les politiques groupées ?
**A)** Tag  
**B)** Community  
**C)** Policy  
**D)** Label  

**Réponse : B** - **Community** est l'attribut pour tagger les routes de façon réutilisable.

---

### Q8 : Quel est le format standard d'une BGP Community ?
**A)** ASN-VALUE  
**B)** VALUE-VALUE  
**C)** ASN:VALUE  
**D)** PREFIX:VALUE  

**Réponse : C** - Le format est **ASN:VALUE**, exemple : `100:1` ou `65001:100`.

---

### Q9 : Que signifie la well-known community `no-export` ?
**A)** Ne pas annoncer cette route du tout  
**B)** Ne pas exporter hors de l'AS  
**C)** Ne pas accepter depuis cet AS  
**D)** Ne pas importer cette route  

**Réponse : B** - **`no-export` (65535:65281)** signifie ne pas exporter la route hors de l'AS.

---

### Q10 : Quel attribut manipulation peut allonger un AS_Path pour déprioritiser une route ?
**A)** `set metric prepend`  
**B)** `set as-path prepend`  
**C)** `set local-preference`  
**D)** `set weight prepend`  

**Réponse : B** - **`set as-path prepend`** ajoute le propre ASN plusieurs fois au chemin pour le faire paraître plus long.

---

## Questions 11-20

### Q11 : Quel attribut contrôle la SÉLECTION des routes **SORTANTES** (iBGP) ?
**A)** MED  
**B)** Local Preference  
**C)** Weight  
**D)** Both B et C  

**Réponse : D** - **Local Preference** (iBGP) et **Weight** (Cisco) contrôlent les routes sortantes.

---

### Q12 : Quel attribut recommande une route aux AS PAIRS (routes rentrantes) ?
**A)** Local Preference  
**B)** MED (Multi-Exit Discriminator)  
**C)** Weight  
**D)** Community  

**Réponse : B** - **MED** est une recommandation au peering AS pour les routes **rentrantes**.

---

### Q13 : Quel est l'ordre de priorité entre Weight et Local Preference dans Best Path ?
**A)** Local Preference > Weight  
**B)** Weight > Local Preference  
**C)** Égalité  
**D)** Dépend du routeur  

**Réponse : B** - **Weight > Local Preference** (Weight est premie, en Cisco).

---

### Q14 : Que se passe-t-il si une route n'a pas de match dans une route map ?
**A)** Elle est acceptée par défaut  
**B)** Elle est rejetée par défaut  
**C)** Elle est ignorée (no action)  
**D)** Elle est dupliquée  

**Réponse : B** - Les clauses route-map finales sont **implicitement deny**, donc sans match = **REJECT**.

---

### Q15 : Quel est le délai en secondes pour basculer depuis route primaire vers route secondaire en BGP ?
**A)** < 1 seconde  
**B)** 10-20 secondes  
**C)** 60-180 secondes (Hold Time)  
**D)** Immédiat  

**Réponse : C** - Le **Hold Time par défaut (180 sec)** gouverne la détection de route morte et le basculement.

---

### Q16 : Quelle route map clause rejette tout trafic ne matchant pas les critères précédents ?
**A)** `route-map X permit 100` sans match  
**B)** `route-map X deny 100` sans match  
**C)** Clause implicite final (implicit deny)  
**D)** Aucun, tout est accepté par défaut  

**Réponse : C** - **Clause implicite final dans route-map = deny everything**. Toujours ajouter un permit explicite final.

---

### Q17 : Quel commande Cisco configure les communities envoyées au voisin BGP ?
**A)** `send-community`  
**B)** `neighbor send-community`  
**C)** `community-list send`  
**D)** `advertise-community`  

**Réponse : B** - **`neighbor X send-community`** envoie les communities aux voisins.

---

### Q18 : Quel est l'impact de `set as-path prepend 65001 65001 65001` sur la longueur du AS_Path ?
**A)** Réduit de 3  
**B)** Ajoute 3 au chemin  
**C)** Multiplie par 3  
**D)** Efface le chemin  

**Réponse : B** - **Prepend** ajoute 3 copies de l'ASN, donc **+3 au AS_Path length**.

---

### Q19 : Quel est le MEILLEUR scénario pour utiliser ORF (Outbound Route Filtering) ?
**A)** Toutes les sessions BGP  
**B)** Seulement iBGP  
**C)** Utilisateur a multihoming avec ISPs multiples  
**D)** Jamais utile en production  

**Réponse : C** - **ORF est utile en multihoming** pour éviter le transit involontaire vers les ISP.

---

### Q20 : Quel well-known community empêche la route de sortir l'AS COMPLÈTEMENT ?
**A)** `no-export`  
**B)** `no-advertise`  
**C)** `local-preference`  
**D)** `internet`  

**Réponse : B** - **`no-advertise` (65535:65282)** signifie la route ne doit PAS être annoncée (complètement supprimée).

---

## Questions 21-25

### Q21 : Quel prefix-list syntax accepte TOUS les préfixes IPv4 sans restriction ?
**A)** `permit 0.0.0.0/0`  
**B)** `permit any`  
**C)** `permit 0.0.0.0/0 le 32`  
**D)** `permit *`  

**Réponse : C** - **`permit 0.0.0.0/0 le 32`** accepte tous les préfixes IPv4/0-32 bits.

---

### Q22 : Quel paramètre de "match" en route-map teste l'origin attribute ?
**A)** `match origin`  
**B)** `match as-path`  
**C)** `match origin-type`  
**D)** `match source`  

**Réponse : A** - **`match origin`** teste l'attribut Origin (IGP/EGP/Incomplete).

---

### Q23 : En quelle cas la Local Preference n'a-t-elle AUCUN effet ?
**A)** Entre routeurs eBGP  
**B)** Avec un seul voisin iBGP  
**C)** Quand Weight est configuré  
**D)** Aucune de ces - Local Preference fonctionne toujours  

**Réponse : A** - **Local Preference ne s'échange QUE en iBGP**, donc pas d'effet en eBGP.

---

### Q24 : Quel est l'impact principal du multihoming sur la disponibilité ?
**A)** Réduit la latence de 50%  
**B)** Double la bande passante  
**C)** Fournit une redondance en cas de panne ISP  
**D)** Élimine les pertes de paquets  

**Réponse : C** - **Multihoming = redondance ISP**, assurant la disponibilité en cas de défaillance d'un ISP.

---

### Q25 : Quel est le vrai bénéfice de Community tags vs ACLs pour les politiques BGP ?
**A)** Les Communities sont plus rapides  
**B)** Les ACLs ne peuvent pas filtrer  
**C)** Les Communities sont réutilisables entre multiples voisins  
**D)** Les Communities ne consomment pas de mémoire  

**Réponse : C** - **Communities = tags réutilisables** qui simplifient la gestion des politiques multiples.

