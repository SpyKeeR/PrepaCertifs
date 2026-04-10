# QCM Module 11 : BGP Fundamentals

## Questions 1-10

### Q1 : Quel attribut BGP prévient les boucles de routage ?
**A)** Local Preference  
**B)** AS_Path  
**C)** MED  
**D)** Weight  

**Réponse : B** - L'attribut **AS_Path** contient la liste des AS traversés. Si un routeur voit son propre ASN dans le chemin, il rejette la route.

---

### Q2 : Quelle est la distance administrative de eBGP ?
**A)** 90  
**B)** 110  
**C)** 20  
**D)** 200  

**Réponse : C** - **eBGP a une AD de 20**, la plus faible (donc la plus préférée). iBGP a une AD de 200.

---

### Q3 : Quel port utilise BGP pour établir les sessions ?
**A)** 180  
**B)** 179  
**C)** 178  
**D)** 175  

**Réponse : B** - BGP utilise **TCP port 179** pour établir les connexions.

---

### Q4 : Quelle plage d'ASN est réservée pour les réseaux privés (16-bit) ?
**A)** 0-1000  
**B)** 1000-20000  
**C)** 64512-65535  
**D)** 100000-200000  

**Réponse : C** - Les ASN privés 16-bit sont **64512-65535**. La plage 32-bit privée est 4200000000-4294967294.

---

### Q5 : Quel est le keepalive par défaut en BGP ?
**A)** 10 secondes  
**B)** 30 secondes  
**C)** 60 secondes  
**D)** 90 secondes  

**Réponse : C** - Le **keepalive par défaut est 60 secondes**, et le Hold Time est 180 secondes (3× le keepalive).

---

### Q6 : Dans le Best Path Algorithm BGP, quel est l'ordre de priorité (1er au 3e) ?
**A)** Weight, Local Preference, AS_Path length  
**B)** Local Preference, Weight, AS_Path length  
**C)** AS_Path length, Weight, Local Preference  
**D)** Weight, AS_Path length, Local Preference  

**Réponse : A** - L'ordre est : **1) Weight (Cisco proprietary)** → **2) Local Preference** → **3) Locally originated** → **4) AS_Path length**

---

### Q7 : Qu'est-ce que MP-BGP (Multiprotocol BGP) ?
**A)** BGP avec plusieurs systèmes autonomes simultanément  
**B)** BGP supportant plusieurs familles d'adresses sur une seule session  
**C)** BGP avec multiple redundancy  
**D)** BGP multicast uniquement  

**Réponse : B** - **MP-BGP** permet une seule session BGP de supporter IPv4, IPv6, et d'autres familles d'adresses (AFI/SAFI).

---

### Q8 : Quel attribut BGP indique comment la route a été originaire ?
**A)** Origin  
**B)** Source  
**C)** Generator  
**D)** Type  

**Réponse : A** - L'attribut **Origin** indique IGP (i), EGP (e), ou Incomplete (?).

---

### Q9 : Qu'est-ce which change lors d'une annonce eBGP ?
**A)** Le Next Hop reste identique  
**B)** Le Next Hop change en adresse du voisin eBGP  
**C)** Le Local Preference est modifié  
**D)** Le poids (weight) est remis à zéro  

**Réponse : B** - Lors d'une annonce **eBGP**, le **Next Hop est changé** à l'adresse de l'interface sortante du routeur annonçant (ou de la voisin en direction inverse).

---

### Q10 : Quel est le rôle principal du BGP Router ID ?
**A)** Identifier la source de la mise à jour BGP  
**B)** Servir de Next Hop pour toutes les routes  
**C)** Identifier le routeur dans l'AS  
**D)** Contrôler la bande passante BGP  

**Réponse : C** - Le **BGP Router ID** est un identifiant 32-bit unique pour chaque routeur BGP dans l'AS.

---

## Questions 11-20

### Q11 : Un routeur eBGP reçoit la même route de 2 voisins avec des AS_Path de longueurs différentes (3 AS vs 5 AS). Quelle route est préférée ?
**A)** Celle avec 5 AS (plus long chemin)  
**B)** Celle avec 3 AS (chemin plus court)  
**C)** Les deux ont la même préférence  
**D)** Dépend du MED  

**Réponse : B** - Dans le Best Path Algorithm, **AS_Path length** est un critère : **AS_Path plus court = meilleur**. Donc 3 AS < 5 AS.

---

### Q12 : Quel est l'attribut utilisé pour signaler les routes supprimées en BGP ?
**A)** Withdrawn Routes  
**B)** Unfeasible Routes  
**C)** Les deux sont corrects  
**D)** Aucun, BGP n'utilise que UPDATE  

**Réponse : C** - Les routes retirées sont signalées par **Withdrawn Routes** dans les **UPDATE messages**, aussi appelées **Unfeasible Routes**.

---

### Q13 : Selon RFC 5398, quelle est la plage d'ASN 32-bit publique ?
**A)** 1-65535  
**B)** 65536-4199999999  
**C)** 4200000000-4294967295  
**D)** 4294967295 onwards  

**Réponse : C** - La plage **4200000000-4294967294** (et 4294967295 réservé).

---

### Q14 : Quel est le délai par défaut avant de considérer une session BGP comme morte ?
**A)** 60 secondes  
**B)** 90 secondes  
**C)** 180 secondes  
**D)** 3 minutes  

**Réponse : C** - Le **Hold Time par défaut est 180 secondes** (3 minutes).

---

### Q15 : Dans l'établissement d'une session BGP, quel message est échangé pour synchroniser après OPEN ?
**A)** UPDATE  
**B)** NOTIFICATION  
**C)** KEEPALIVE  
**D)** REFRESH  

**Réponse : C** - Après OPEN, les routeurs échangent des **KEEPALIVE** pour établir l'état ESTABLISHED.

---

### Q16 : Quel AFI/SAFI est utilisé pour le routage IPv4 standard (unicast) ?
**A)** AFI 1, SAFI 1  
**B)** AFI 2, SAFI 1  
**C)** AFI 1, SAFI 2  
**D)** AFI 2, SAFI 2  

**Réponse : A** - **AFI 1 (IPv4), SAFI 1 (Unicast)** est le standard pour IPv4 unicast.

---

### Q17 : Lors d'une annonce de route en iBGP, que se passe-t-il avec le Next Hop ?
**A)** Le Next Hop est remplacé par l'adresse du voisin iBGP  
**B)** Le Next Hop reste identique (contrainte iBGP)  
**C)** Le Next Hop est ajouté à une liste  
**D)** Le Next Hop est remis à 0.0.0.0  

**Réponse : B** - En **iBGP**, le **Next Hop est préservé** (IBGP Next Hop constraint), ce qui est crucial pour le design de topologie.

---

### Q18 : Quel attribut BGP est le plus spécifique pour les politiques de routage ?
**A)** MED  
**B)** Local Preference  
**C)** Community  
**D)** Préférence d'origine  

**Réponse : C** - **Community** est l'attribut le plus flexible et réutilisable pour les politiques de routage.

---

### Q19 : Si un routeur iBGP annonce une route externe (reçue de eBGP) à un autre routeur iBGP, quelle conséquence sur AD ?
**A)** L'AD reste 20 (eBGP)  
**B)** L'AD devient 200 (iBGP)  
**C)** L'AD devient 110 (IGP)  
**D)** L'AD reste la même que la source originale  

**Réponse : B** - Quand une route eBGP (AD 20) est reannoncée via **iBGP**, **l'AD devient 200**.

---

### Q20 : Quel message BGP est utilisé pour signaler une erreur ou terminer une session ?
**A)** NOTIFICATION  
**B)** RESET  
**C)** ALERT  
**D)** CLOSE  

**Réponse : A** - Le message **NOTIFICATION** est utilisé pour signaler une erreur et terminer la session.

---

## Questions 21-25

### Q21 : Quel est le Weight par défaut (Cisco) pour les routes reçues de voisins iBGP ?
**A)** 0  
**B)** 32768  
**C)** 65535  
**D)** 100  

**Réponse : A** - Le **Weight par défaut est 0** pour les routes reçues, et **32768 pour les routes générées localement**.

---

### Q22 : En BGP, quel est le critrère pour départager deux routes avec le même AS_Path length ?
**A)** Origin attribute  
**B)** MED attribute  
**C)** Peer IP address  
**D)** BGP Router ID  

**Réponse : A** - Après AS_Path length égale, on utilise **Origin** : IGP > EGP > Incomplete (?).

---

### Q23 : Quelle est la relation entre les Keepalive et Hold Time ?
**A)** Hold Time = Keepalive  
**B)** Hold Time = 3 × Keepalive (défaut)  
**C)** Hold Time = Keepalive / 3  
**D)** Aucune relation directe  

**Réponse : B** - **Hold Time = 3 × Keepalive** par défaut (donc 180 = 3 × 60 secondes).

---

### Q24 : Quel est le mecanisme primaire pour éviter les boucles de routage en BGP ?
**A)** Hold down timers  
**B)** Administrative Distance hiérarchique  
**C)** Inspection de l'AS_Path  
**D)** Split Horizon  

**Réponse : C** - Le **AS_Path** est inspecté; si l'ASN du routeur y figure, la route est rejetée.

---

### Q25 : À quoi sert l'attribut BGP "Next Hop" ?
**A)** À identifier le routeur suivant dans le chemin complet  
**B)** À indiquer l'adresse IP du prochain routeur à atteindre la destination  
**C)** À compter le nombre de sauts  
**D)** À limiter le TTL de la route  

**Réponse : B** - **Next Hop** indique l'adresse IP du prochain routeur pour atteindre la destination annoncée.

