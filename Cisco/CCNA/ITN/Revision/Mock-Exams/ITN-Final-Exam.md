# Mock Exam Final - ITN (Introduction to Networks)
**Examen Blanc Final - Cours CCNA 1/3**

---

## 📋 Instructions

### Format de l'examen
- **Nombre de questions :** 50 questions
- **Durée recommandée :** 90 minutes
- **Score minimal :** 75% (38/50)
- **Type :** QCM et questions à choix multiples
- **Couverture :** L'intégralité du cours ITN (Modules 1-17)
- **Difficulté :** Niveau examen final NetAcad

### Conseils
- Cet examen simule l'examen final officiel
- La difficulté est légèrement supérieure au Practice Exam
- Certaines questions nécessitent des calculs
- Gérez votre temps efficacement
- Vérifiez toutes vos réponses

### Conditions d'examen réel
- ⏱️ Chronométrez-vous strictement (90 minutes)
- 📵 Sans aucune aide extérieure
- 🚫 Sans documentation
- 📝 Conditions d'examen simulées

---

## Questions

### Question 1
Un technicien doit diviser le réseau 172.16.0.0/16 en sous-réseaux pouvant accueillir au minimum 500 hôtes chacun. Quel masque de sous-réseau devrait-il utiliser ?

- [ ] A. 255.255.252.0 (/22)
- [ ] B. 255.255.254.0 (/23)
- [ ] C. 255.255.248.0 (/21)
- [ ] D. 255.255.240.0 (/20)

---

### Question 2
Quelles sont les trois caractéristiques du protocole UDP ? (Choisissez trois réponses)

- [ ] A. Sans connexion
- [ ] B. Fiable
- [ ] C. Faible overhead
- [ ] D. Orienté connexion
- [ ] E. Livraison garantie
- [ ] F. Adapté pour les applications temps réel

---

### Question 3
Un administrateur configure SSH sur un routeur. Quelles sont les trois commandes requises pour activer SSH version 2 ? (Choisissez trois réponses)

- [ ] A. `hostname <nom>`
- [ ] B. `enable secret <mot-de-passe>`
- [ ] C. `ip domain-name <domaine>`
- [ ] D. `crypto key generate rsa`
- [ ] E. `transport input ssh`
- [ ] F. `ip ssh version 2`

---

### Question 4
Quelle adresse IPv6 est une adresse de loopback ?

- [ ] A. ::1
- [ ] B. FE80::1
- [ ] C. FF02::1
- [ ] D. 2001::1

---

### Question 5
Dans la table de commutation MAC d'un switch, qu'est-ce qui est mappé ensemble ?

- [ ] A. Adresse MAC et numéro de VLAN
- [ ] B. Adresse MAC et numéro de port
- [ ] C. Adresse IP et adresse MAC
- [ ] D. Numéro de port et adresse IP

---

### Question 6
Quelle est la plage d'adresses link-local IPv4 (APIPA) ?

- [ ] A. 10.0.0.0 à 10.255.255.255
- [ ] B. 169.254.0.0 à 169.254.255.255
- [ ] C. 172.16.0.0 à 172.31.255.255
- [ ] D. 192.168.0.0 à 192.168.255.255

---

### Question 7
Un routeur a reçu un paquet destiné à 192.168.1.50. Il consulte sa table de routage. Quelle affirmation décrit le comportement du routeur si aucune correspondance exacte n'est trouvée ?

- [ ] A. Il utilise la route par défaut si elle existe
- [ ] B. Il broadcast le paquet sur toutes les interfaces
- [ ] C. Il demande une route via ARP
- [ ] D. Il conserve le paquet dans une mémoire tampon

---

### Question 8
Quelle commande affiche uniquement les routes apprises dynamiquement dans la table de routage ?

- [ ] A. `show ip route static`
- [ ] B. `show ip route dynamic`
- [ ] C. `show ip route rip`
- [ ] D. Dépend du protocole de routage utilisé

---

### Question 9
Combien de sous-réseaux utilisables peut-on créer en empruntant 4 bits à la partie hôte d'une adresse réseau ?

- [ ] A. 14
- [ ] B. 16
- [ ] C. 30
- [ ] D. 32

---

### Question 10
Quelle est la différence entre `enable password` et `enable secret` sur un routeur Cisco ?

- [ ] A. `enable password` est chiffré par défaut
- [ ] B. `enable secret` utilise le chiffrement MD5
- [ ] C. Les deux sont identiques
- [ ] D. `enable password` est plus sécurisé

---

### Question 11
Un technicien utilise la commande `ping` mais ne reçoit pas de réponse. Quelle couche du modèle OSI est probablement en cause ?

- [ ] A. Couche 1, 2 ou 3
- [ ] B. Couche 4
- [ ] C. Couche 7
- [ ] D. Toutes les couches

---

### Question 12
Quelle technologie permet d'attribuer dynamiquement des adresses IPv6 sans serveur DHCPv6 ?

- [ ] A. NDP uniquement
- [ ] B. SLAAC (Stateless Address Autoconfiguration)
- [ ] C. EUI-64 uniquement
- [ ] D. Adresses link-local

---

### Question 13
Dans un réseau 192.168.5.0/28, quelle est la première adresse hôte utilisable ?

- [ ] A. 192.168.5.0
- [ ] B. 192.168.5.1
- [ ] C. 192.168.5.15
- [ ] D. 192.168.5.16

---

### Question 14
Quels sont les deux protocoles qui opèrent sur la couche Application du modèle TCP/IP ? (Choisissez deux réponses)

- [ ] A. ARP
- [ ] B. HTTP
- [ ] C. ICMP
- [ ] D. DNS
- [ ] E. TCP

---

### Question 15
Un switch reçoit une trame avec une adresse MAC de destination inconnue. Que fait-il ?

- [ ] A. Il l'envoie au routeur par défaut
- [ ] B. Il la transfère sur tous les ports sauf le port source (flood)
- [ ] C. Il la supprime
- [ ] D. Il envoie une requête ARP

---

### Question 16
Quelle commande permet de voir l'état et la configuration d'une interface spécifique ?

- [ ] A. `show interface`
- [ ] B. `show ip interface <interface>`
- [ ] C. `show ip interface brief`
- [ ] D. A et B sont correctes

---

### Question 17
Quel est le préfixe d'adresse IPv6 pour les adresses unique locale (ULA) ?

- [ ] A. FE80::/10
- [ ] B. FC00::/7
- [ ] C. FF00::/8
- [ ] D. 2000::/3

---

### Question 18
Quelle méthode de commutation vérifie la trame entière avant de la transmettre ?

- [ ] A. Cut-through
- [ ] B. Fast-forward
- [ ] C. Fragment-free
- [ ] D. Store-and-forward

---

### Question 19
Quelle affirmation concernant la passerelle par défaut est correcte ?

- [ ] A. Elle est obligatoire pour toute communication
- [ ] B. Elle est nécessaire pour communiquer avec des hôtes d'autres réseaux
- [ ] C. Elle doit être configurée sur tous les switches
- [ ] D. Elle remplace le serveur DNS

---

### Question 20
Quel numéro de port UDP utilise le protocole DHCP côté serveur ?

- [ ] A. 67
- [ ] B. 68
- [ ] C. 53
- [ ] D. 69

---

### Question 21
Un administrateur souhaite éviter qu'un utilisateur non autorisé ne modifie la configuration d'un routeur. Quelle commande devrait-il utiliser ?

- [ ] A. `enable password`
- [ ] B. `enable secret`
- [ ] C. `service password-encryption`
- [ ] D. B et C ensemble

---

### Question 22
Quelle est la longueur maximale d'un câble UTP Cat 5e pour maintenir les performances ?

- [ ] A. 100 mètres
- [ ] B. 200 mètres
- [ ] C. 500 mètres
- [ ] D. 1000 mètres

---

### Question 23
Dans une adresse IPv6 2001:0DB8:0000:0000:0000:FF00:0042:8329, quelle est la forme compressée correcte ?

- [ ] A. 2001:DB8::FF00:42:8329
- [ ] B. 2001:DB8:0:0:0:FF00:42:8329
- [ ] C. 2001:DB8::FF:42:8329
- [ ] D. 2001:0DB8::FF00:0042:8329

---

### Question 24
Quelle fonctionnalité d'un ISR (Integrated Services Router) permet de connecter différents types de médias réseau ?

- [ ] A. Pare-feu
- [ ] B. Interfaces modulaires
- [ ] C. Quality of Service
- [ ] D. VPN

---

### Question 25
Quel message ICMP est renvoyé lorsqu'un routeur ne peut pas transmettre un paquet parce que le TTL a expiré ?

- [ ] A. Destination Unreachable
- [ ] B. Time Exceeded
- [ ] C. Echo Reply
- [ ] D. Source Quench

---

### Question 26
Un technicien configure PAT sur un routeur. Quelle commande est typiquement utilisée ?

- [ ] A. `ip nat inside source list 1 interface g0/0 overload`
- [ ] B. `ip nat static 192.168.1.10 203.0.113.5`
- [ ] C. `ip nat pool PUBLIC 203.0.113.1 203.0.113.10`
- [ ] D. `ip nat enable`

---

### Question 27
Quelle est la fonction principale du protocole NDP dans IPv6 ?

- [ ] A. Attribuer des adresses IP
- [ ] B. Découvrir les voisins sur le lien local
- [ ] C. Router les paquets
- [ ] D. Chiffrer les communications

---

### Question 28
Lors de la méthode de dépannage "Divide and Conquer", par quelle couche commence-t-on généralement ?

- [ ] A. Couche 1 (Physique)
- [ ] B. Couche 3 (Réseau)
- [ ] C. Couche 7 (Application)
- [ ] D. Dépend du symptôme observé

---

### Question 29
Quelle commande affiche la configuration active mais non sauvegardée d'un routeur ?

- [ ] A. `show startup-config`
- [ ] B. `show running-config`
- [ ] C. `show configuration`
- [ ] D. `display config`

---

### Question 30
Un réseau utilise l'adresse 10.0.0.0 avec un masque 255.255.0.0. Combien d'adresses hôtes sont disponibles ?

- [ ] A. 65,534
- [ ] B. 65,535
- [ ] C. 65,536
- [ ] D. 32,768

---

### Question 31
Quel type de trame Ethernet est utilisé pour des communications un-à-plusieurs ?

- [ ] A. Unicast
- [ ] B. Broadcast
- [ ] C. Multicast
- [ ] D. Anycast

---

### Question 32
Quelle commande permet d'activer une interface de routeur qui est administrativement désactivée ?

- [ ] A. `enable`
- [ ] B. `no shutdown`
- [ ] C. `up`
- [ ] D. `interface enable`

---

### Question 33
Quel protocole de routage est considéré comme un protocole à vecteur de distance ?

- [ ] A. OSPF
- [ ] B. IS-IS
- [ ] C. RIP
- [ ] D. BGP

---

### Question 34
Un utilisateur ne peut pas accéder à Internet. La commande `ipconfig` montre une adresse IP 169.254.x.x. Quelle est la cause probable ?

- [ ] A. Configuration IP statique incorrecte
- [ ] B. Pas de réponse du serveur DHCP
- [ ] C. Problème DNS
- [ ] D. Routeur par défaut incorrect

---

### Question 35
Quelle caractéristique du protocole TCP garantit la livraison fiable des données ?

- [ ] A. Contrôle de flux
- [ ] B. Numéros de séquence et accusés de réception
- [ ] C. Connexion three-way handshake
- [ ] D. Fenêtre glissante

---

### Question 36
Quelle commande IOS permet d'afficher la table MAC d'un switch ?

- [ ] A. `show mac table`
- [ ] B. `show mac-address-table`
- [ ] C. `show arp`
- [ ] D. `show cam table`

---

### Question 37
Dans un scénario de dépannage, un utilisateur peut utiliser `ping` pour atteindre le serveur par adresse IP, mais pas par nom. Quel est le problème probable ?

- [ ] A. Problème de câblage
- [ ] B. Problème DNS
- [ ] C. Problème de passerelle
- [ ] D. Problème DHCP

---

### Question 38
Quel est l'avantage principal de l'utilisation d'une hiérarchie à 2 couches dans un petit réseau ?

- [ ] A. Coût réduit et complexité moindre
- [ ] B. Performances maximales
- [ ] C. Sécurité maximale
- [ ] D. Évolutivité illimitée

---

### Question 39
Quelle plage d'adresses IPv4 est réservée aux adresses de classe D (multicast) ?

- [ ] A. 192.0.0.0 à 223.255.255.255
- [ ] B. 224.0.0.0 à 239.255.255.255
- [ ] C. 240.0.0.0 à 255.255.255.255
- [ ] D. 172.16.0.0 à 172.31.255.255

---

### Question 40
Quelle commande affiche les connexions TCP actives sur un hôte Windows ?

- [ ] A. `ipconfig /all`
- [ ] B. `netstat -a`
- [ ] C. `netstat -r`
- [ ] D. `nbtstat -a`

---

### Question 41
Un technicien doit configurer le logging sur un routeur pour capturer les messages de niveau Warning et supérieur. Quel niveau devrait-il configurer ?

- [ ] A. Level 3
- [ ] B. Level 4
- [ ] C. Level 5
- [ ] D. Level 6

---

### Question 42
Quelle est la fonction du champ "Sequence Number" dans l'en-tête TCP ?

- [ ] A. Identifier l'application source
- [ ] B. Ordonner les segments pour le réassemblage
- [ ] C. Contrôler le flux de données
- [ ] D. Détecter les erreurs

---

### Question 43
Quel type d'attaque réseau implique l'envoi massif de requêtes pour saturer une ressource ?

- [ ] A. Man-in-the-Middle
- [ ] B. Phishing
- [ ] C. DoS (Denial of Service)
- [ ] D. Social Engineering

---

### Question 44
Dans le contexte AAA, que signifie "Authorization" ?

- [ ] A. Vérifier l'identité de l'utilisateur
- [ ] B. Déterminer ce que l'utilisateur est autorisé à faire
- [ ] C. Enregistrer les actions de l'utilisateur
- [ ] D. Chiffrer les communications

---

### Question 45
Un réseau /25 contient combien d'adresses hôtes utilisables ?

- [ ] A. 62
- [ ] B. 126
- [ ] C. 128
- [ ] D. 254

---

### Question 46
Quelle topologie logique est utilisée par Ethernet moderne avec des switches ?

- [ ] A. Bus
- [ ] B. Anneau
- [ ] C. Étoile étendue
- [ ] D. Maillée

---

### Question 47
Quel protocole IPv6 remplace les fonctions d'ARP, IGMP et ICMP redirect d'IPv4 ?

- [ ] A. DHCPv6
- [ ] B. ICMPv6
- [ ] C. NDP (Neighbor Discovery Protocol)
- [ ] D. SLAAC

---

### Question 48
Un switch reçoit une trame sur le port 1. L'adresse MAC source n'est pas dans sa table MAC. Que fait le switch ?

- [ ] A. Il supprime la trame
- [ ] B. Il ajoute l'adresse MAC et le port 1 à sa table
- [ ] C. Il envoie une requête ARP
- [ ] D. Il redémarre

---

### Question 49
Quelle commande permet de sécuriser les lignes VTY pour n'accepter que SSH ?

- [ ] A. `transport input telnet`
- [ ] B. `transport input ssh`
- [ ] C. `transport input all`
- [ ] D. `login local`

---

### Question 50
Dans la méthode de dépannage "Bottom-Up", par quelle couche commence-t-on ?

- [ ] A. Couche Physique (Couche 1)
- [ ] B. Couche Liaison de données (Couche 2)
- [ ] C. Couche Réseau (Couche 3)
- [ ] D. Couche Application (Couche 7)

---

## Grille de réponses

| Q | Rép | Q | Rép | Q | Rép | Q | Rép | Q | Rép |
|---|-----|---|-----|---|-----|---|-----|---|-----|
| 1 | | 11 | | 21 | | 31 | | 41 | |
| 2 | | 12 | | 22 | | 32 | | 42 | |
| 3 | | 13 | | 23 | | 33 | | 43 | |
| 4 | | 14 | | 24 | | 34 | | 44 | |
| 5 | | 15 | | 25 | | 35 | | 45 | |
| 6 | | 16 | | 26 | | 36 | | 46 | |
| 7 | | 17 | | 27 | | 37 | | 47 | |
| 8 | | 18 | | 28 | | 38 | | 48 | |
| 9 | | 19 | | 29 | | 39 | | 49 | |
| 10 | | 20 | | 30 | | 40 | | 50 | |

---

## Corrigé des réponses

### Réponses

1. **A** - /22 (1022 hôtes utilisables par sous-réseau)
2. **A, C, F** - Sans connexion, Faible overhead, Temps réel
3. **A, C, D** - hostname, ip domain-name, crypto key
4. **A** - ::1
5. **B** - MAC et numéro de port
6. **B** - 169.254.0.0/16
7. **A** - Route par défaut si disponible
8. **D** - Dépend du protocole (ex: `show ip route rip`)
9. **B** - 16 sous-réseaux (2^4)
10. **B** - enable secret utilise MD5
11. **A** - Couches 1, 2 ou 3
12. **B** - SLAAC
13. **B** - 192.168.5.1
14. **B, D** - HTTP et DNS
15. **B** - Flood sur tous les ports sauf source
16. **D** - Les deux commandes
17. **B** - FC00::/7
18. **D** - Store-and-forward
19. **B** - Nécessaire pour communication inter-réseaux
20. **A** - Port 67 (serveur), 68 (client)
21. **D** - enable secret + service password-encryption
22. **A** - 100 mètres
23. **A** - 2001:DB8::FF00:42:8329
24. **B** - Interfaces modulaires
25. **B** - Time Exceeded
26. **A** - ip nat inside source avec overload
27. **B** - Découvrir les voisins
28. **D** - Dépend du symptôme (couche médiane)
29. **B** - show running-config
30. **A** - 65,534 (2^16 - 2)
31. **C** - Multicast
32. **B** - no shutdown
33. **C** - RIP
34. **B** - Pas de serveur DHCP accessible (APIPA)
35. **B** - Numéros de séquence et ACK
36. **B** - show mac-address-table
37. **B** - Problème DNS
38. **A** - Coût réduit et simplicité
39. **B** - 224.0.0.0 à 239.255.255.255
40. **B** - netstat -a
41. **B** - Level 4 (Warning)
42. **B** - Ordonner les segments
43. **C** - DoS
44. **B** - Déterminer les autorisations
45. **B** - 126 (2^7 - 2)
46. **C** - Étoile étendue
47. **C** - NDP
48. **B** - Ajoute MAC et port à la table
49. **B** - transport input ssh
50. **A** - Couche 1 (Physique)

---

## Explications détaillées

### Question 1 - Calcul de sous-réseau
**Réponse : A (/22)**

**Explication :**
Pour accueillir 500 hôtes, on doit avoir au moins 500 adresses utilisables.
- Formule : 2^n - 2 ≥ 500 (où n = nombre de bits hôte)
- 2^9 - 2 = 510 ✅
- Donc besoin de 9 bits pour les hôtes
- Masque : 32 - 9 = /23... Non ! 2^9 - 2 = 510, mais seulement à partir de /23
- Vérification /22 : 32 - 22 = 10 bits hôtes → 2^10 - 2 = 1022 hôtes ✅
- Vérification /23 : 32 - 23 = 9 bits hôtes → 2^9 - 2 = 510 hôtes ✅

Mais le /22 offre plus de marge, ce qui est préférable pour la croissance.

💡 **Point clé :** Pour calculer le nombre d'hôtes, utilisez 2^(32-préfixe) - 2.

---

### Question 2 - Caractéristiques UDP
**Réponse : A, C, F**

**Explication :**
UDP (User Datagram Protocol) :
- ✅ Sans connexion (connectionless)
- ✅ Faible overhead (peu d'en-têtes)
- ✅ Adapté pour temps réel (VoIP, streaming)
- ❌ Non fiable (pas de garantie de livraison)
- ❌ Pas orienté connexion
- ❌ Pas de livraison garantie

💡 **Point clé :** UDP sacrifie la fiabilité pour la vitesse et l'efficacité.

---

### Question 3 - Configuration SSH
**Réponse : A, C, D**

**Explication :**
Les 3 commandes essentielles pour SSH :
```
Router(config)# hostname MonRouteur
Router(config)# ip domain-name exemple.com
Router(config)# crypto key generate rsa
```

Les autres commandes sont complémentaires mais pas dans les 3 minimales requises.

💡 **Point clé :** SSH nécessite un nom d'hôte, un nom de domaine et une clé RSA.

---

### Question 7 - Route par défaut
**Réponse : A**

**Explication :**
Processus de décision du routeur :
1. Recherche correspondance exacte dans table de routage
2. Si aucune correspondance, utilise route par défaut (0.0.0.0/0)
3. Si pas de route par défaut, envoie ICMP Destination Unreachable

💡 **Point clé :** La route par défaut est la "last resort" du routage.

---

### Question 9 - Calcul de sous-réseaux
**Réponse : B (16)**

**Explication :**
- Emprunter 4 bits crée 2^4 = 16 sous-réseaux possibles
- Anciennement, on utilisait 2^n - 2 (soustraire premier et dernier)
- Aujourd'hui, tous les sous-réseaux sont utilisables = 16

💡 **Point clé :** 2^n bits empruntés = nombre de sous-réseaux.

---

### Question 13 - Première adresse hôte
**Réponse : B (192.168.5.1)**

**Explication :**
Réseau /28 :
- Masque : 255.255.255.240
- Incrément : 16
- Sous-réseau : 192.168.5.0
- Première adresse utilisable : 192.168.5.1
- Dernière adresse utilisable : 192.168.5.14
- Broadcast : 192.168.5.15

💡 **Point clé :** La première adresse hôte est toujours l'adresse réseau + 1.

---

### Question 21 - Sécurité configuration
**Réponse : D (enable secret + service password-encryption)**

**Explication :**
- `enable secret` : Chiffre le mot de passe avec MD5
- `service password-encryption` : Chiffre les autres mots de passe (type 7)
- L'utilisation combinée offre une meilleure sécurité

💡 **Point clé :** Toujours utiliser `enable secret` plutôt que `enable password`.

---

### Question 23 - Compression IPv6
**Réponse : A (2001:DB8::FF00:42:8329)**

**Explication :**
Règles de compression IPv6 :
- Supprimer les zéros de tête dans chaque bloc
- Remplacer une séquence de blocs à zéros par `::`
- Ne peut utiliser `::` qu'une seule fois

Original : 2001:0DB8:0000:0000:0000:FF00:0042:8329
Compressé : 2001:DB8::FF00:42:8329

💡 **Point clé :** Les deux-points doubles (::) ne peuvent apparaître qu'une fois.

---

### Question 28 - Divide and Conquer
**Réponse : D (Dépend du symptôme)**

**Explication :**
La méthode Divide and Conquer :
- Commence par une couche médiane (souvent couche 3)
- Se base sur les symptômes observés
- Divise le problème en deux parties
- Élimine une moitié, teste l'autre

💡 **Point clé :** Cette méthode est la plus efficace car elle cible directement la zone suspecte.

---

### Question 30 - Calcul d'hôtes
**Réponse : A (65,534)**

**Explication :**
- Réseau : 10.0.0.0/16
- Bits hôtes : 32 - 16 = 16 bits
- Nombre d'adresses : 2^16 = 65,536
- Adresses utilisables : 65,536 - 2 = 65,534
- (On soustrait l'adresse réseau et l'adresse broadcast)

💡 **Point clé :** Toujours soustraire 2 (réseau + broadcast).

---

### Question 34 - APIPA
**Réponse : B (Pas de serveur DHCP)**

**Explication :**
Adresse 169.254.x.x = APIPA (Automatic Private IP Addressing)
- Windows attribue automatiquement cette adresse
- Se produit quand pas de réponse DHCP
- Permet communication locale uniquement
- Pas d'accès Internet

💡 **Point clé :** 169.254.x.x indique toujours un problème DHCP.

---

### Question 41 - Logging levels
**Réponse : B (Level 4)**

**Explication :**
Niveaux de logging Cisco (0-7) :
- 0 : Emergencies
- 1 : Alerts
- 2 : Critical
- 3 : Errors
- **4 : Warnings** ✅
- 5 : Notifications
- 6 : Informational
- 7 : Debugging

Configurer niveau 4 capture Warning et tous les niveaux supérieurs (0-4).

💡 **Point clé :** Un niveau capture ce niveau et tous les niveaux plus critiques.

---

### Question 45 - Réseau /25
**Réponse : B (126)**

**Explication :**
- /25 = 32 - 25 = 7 bits pour hôtes
- 2^7 = 128 adresses
- 128 - 2 = 126 adresses utilisables

💡 **Point clé :** /25 divise un réseau /24 en deux sous-réseaux de 126 hôtes chacun.

---

## Tableau de scoring

| Score | Pourcentage | Évaluation |
|-------|-------------|------------|
| 45-50 | 90-100% | 🏆 Excellent - Prêt pour l'examen officiel |
| 40-44 | 80-88% | ✅ Très bien - Quelques révisions ciblées |
| 38-39 | 76-78% | ⚠️ Passable - Révision recommandée |
| 35-37 | 70-74% | 📚 Insuffisant - Révision approfondie nécessaire |
| < 35 | < 70% | ❌ Échec - Revoir l'ensemble du cours |

---

## Recommandations post-examen

### Score ≥ 40/50 (80%+)
- ✅ Prêt pour l'examen officiel NetAcad
- Réviser les questions manquées
- Revoir les concepts faibles identifiés

### Score 38-39/50 (76-78%)
- ⚠️ Révision ciblée recommandée
- Refaire les checkpoints des modules faibles
- Reprendre ce mock exam dans 3-4 jours

### Score < 38/50 (< 76%)
- 📚 Révision approfondie nécessaire
- Relire les notes des modules concernés
- Refaire les QCM de chaque module
- Reprendre le Practice Exam avant ce Final

---

**Prochaine étape :** Selon votre score, soit vous êtes prêt pour l'examen officiel, soit vous devez réviser les domaines identifiés comme faibles.

**Bonne chance ! 🎯**
