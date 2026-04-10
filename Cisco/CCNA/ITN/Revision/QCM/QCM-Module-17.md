# QCM - Module 17 : Conception d'un réseau de petite taille
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **18 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Quelles fonctions sont typiquement intégrées dans un routeur ISR (Integrated Services Router) pour petit réseau ? (Choisissez trois réponses)

- [ ] A. Routage
- [ ] B. NAT/PAT
- [ ] C. Serveur DHCP
- [ ] D. Contrôleur de domaine Active Directory
- [ ] E. Base de données SQL

### Question 2
Dans un réseau hiérarchique à 3 couches, quelle couche est responsable de la commutation haute vitesse sans manipulation de paquets ?

- [ ] A. Couche Accès
- [ ] B. Couche Distribution
- [ ] C. Couche Cœur (Core)
- [ ] D. Couche Bordure (Edge)

### Question 3
Combien de couches hiérarchiques sont généralement suffisantes pour un réseau de petite taille ?

- [ ] A. 1 couche (Core seulement)
- [ ] B. 2 couches (Distribution + Accès)
- [ ] C. 3 couches (Core + Distribution + Accès)
- [ ] D. 4 couches

### Question 4
Quelle commande Windows permet de renouveler une adresse IP obtenue via DHCP ?

- [ ] A. `ipconfig /refresh`
- [ ] B. `ipconfig /renew`
- [ ] C. `ipconfig /update`
- [ ] D. `dhcp renew`

### Question 5
Quelle méthodologie de dépannage commence par la couche physique du modèle OSI et remonte vers la couche application ?

- [ ] A. Top-Down
- [ ] B. Bottom-Up
- [ ] C. Divide and Conquer
- [ ] D. Spot the Differences

### Question 6
Un utilisateur peut pinger l'adresse IP 8.8.8.8 avec succès, mais ne peut pas accéder à www.google.com. Quel est le problème le plus probable ?

- [ ] A. Câble réseau défectueux
- [ ] B. Problème de routage
- [ ] C. Problème DNS
- [ ] D. Interface réseau désactivée

### Question 7
Quelle commande Cisco affiche un résumé rapide de toutes les interfaces avec leur adresse IP et leur statut ?

- [ ] A. `show interfaces`
- [ ] B. `show ip interface`
- [ ] C. `show ip interface brief`
- [ ] D. `show ip summary`

### Question 8
Dans la méthodologie de dépannage en 7 étapes, quelle est la dernière étape critique ?

- [ ] A. Tester la solution
- [ ] B. Implémenter la solution
- [ ] C. Vérifier la fonctionnalité complète
- [ ] D. Documenter le problème et la solution

### Question 9
Quel outil permet de tracer le chemin qu'emprunte un paquet pour atteindre sa destination ?

- [ ] A. ping
- [ ] B. traceroute/tracert
- [ ] C. ipconfig
- [ ] D. nslookup

### Question 10
Un technicien constate que PC1 fonctionne correctement mais PC2 (dans le même VLAN) ne peut pas accéder au réseau. Quelle devrait être la première vérification ?

- [ ] A. Configuration DNS sur PC2
- [ ] B. Table de routage du routeur
- [ ] C. Câbles et connectivité physique de PC2
- [ ] D. Configuration du serveur DHCP

### Question 11
Quelle approche de dépannage est généralement considérée comme la plus efficace ?

- [ ] A. Bottom-Up (bas vers haut)
- [ ] B. Top-Down (haut vers bas)
- [ ] C. Divide and Conquer (diviser pour régner)
- [ ] D. Trial and Error (essai-erreur)

### Question 12
Quel numéro de port utilise le protocole DNS ?

- [ ] A. 25
- [ ] B. 53
- [ ] C. 80
- [ ] D. 443

### Question 13
Un réseau subit une connectivité intermittente avec de nombreuses collisions. Quelle est la cause la plus probable ?

- [ ] A. Câble trop long (>100m)
- [ ] B. Duplex mismatch
- [ ] C. VLAN mal configuré
- [ ] D. Adresse IP dupliquée

### Question 14
Quelles commandes Windows permettent de vider le cache DNS ? (Choisissez deux réponses)

- [ ] A. `ipconfig /flushdns`
- [ ] B. `ipconfig /cleardns`
- [ ] C. `nslookup /flush`
- [ ] D. `ipconfig /displaydns` puis suppression manuelle

### Question 15
Dans un petit réseau, quelle segmentation est recommandée pour améliorer la sécurité et les performances ?

- [ ] A. Aucune segmentation nécessaire
- [ ] B. Segmentation par VLANs (départements, invités, voix/données)
- [ ] C. Segmentation physique uniquement
- [ ] D. Segmentation par protocoles uniquement

### Question 16
Quel protocole assure la synchronisation de l'heure entre les équipements réseau ?

- [ ] A. SNMP
- [ ] B. Syslog
- [ ] C. NTP
- [ ] D. CDP

### Question 17
Lors du dépannage d'un problème DHCP, un administrateur souhaite voir les adresses IP attribuées par le serveur DHCP Cisco. Quelle commande doit-il utiliser ?

- [ ] A. `show dhcp leases`
- [ ] B. `show ip dhcp binding`
- [ ] C. `show dhcp pool`
- [ ] D. `show ip dhcp addresses`

### Question 18
Quelle est la longueur maximale recommandée pour un câble Ethernet UTP entre deux équipements actifs ?

- [ ] A. 50 mètres
- [ ] B. 100 mètres
- [ ] C. 185 mètres
- [ ] D. 500 mètres

---

## Réponses et Explications

### Question 1
**Réponses correctes : A, B, C**

**Explication :**
Un routeur ISR (Integrated Services Router) pour petit réseau intègre typiquement :
- **Routage** : Fonction principale, routage entre réseaux
- **NAT/PAT** : Traduction d'adresses privées vers publique
- **Serveur DHCP** : Attribution automatique d'adresses IP aux clients

**Fonctions additionnelles possibles :**
- Pare-feu (ACL)
- VPN
- Switch intégré (4-24 ports)
- Point d'accès Wi-Fi

**💡 Point clé :** "Integrated Services" signifie que plusieurs services réseau sont intégrés dans un seul boîtier, réduisant le nombre d'équipements nécessaires pour un petit réseau.

---

### Question 2
**Réponse correcte : C**

**Explication :**
Dans un réseau hiérarchique à 3 couches :

| Couche | Fonction | Caractéristiques |
|--------|----------|------------------|
| **Core** | Commutation haute vitesse | Pas de manipulation de paquets, redondance max |
| **Distribution** | Routage inter-VLAN, agrégation | ACL, QoS, politiques |
| **Accès** | Connexion périphériques finaux | Port security, VLANs, PoE |

**💡 Point clé :** La couche Core ne fait QUE de la commutation rapide. Toute manipulation (routage, ACL, QoS) ralentirait le Core et est faite à la couche Distribution.

---

### Question 3
**Réponse correcte : B**

**Explication :**
Un réseau de petite taille nécessite généralement **2 couches** :
- **Couche Distribution** : Routage inter-VLAN, connexion Internet
- **Couche Accès** : Connexion des périphériques finaux

**Pourquoi pas de couche Core ?**
Un petit réseau n'a pas assez de trafic pour justifier une couche Core séparée. Les fonctions de core sont intégrées dans la couche distribution.

**💡 Point clé :** Core layer = uniquement pour grands réseaux (campus, entreprise multi-sites).

---

### Question 4
**Réponse correcte : B**

**Explication :**
Commandes DHCP Windows :

```cmd
ipconfig /release    # Libérer l'adresse IP actuelle
ipconfig /renew      # Demander une nouvelle adresse au serveur DHCP
ipconfig /all        # Afficher configuration détaillée
```

**Séquence typique de dépannage DHCP :**
1. `ipconfig /release`
2. `ipconfig /renew`
3. Si échec, vérifier connectivité serveur DHCP

**💡 Point clé :** `/release` libère l'adresse, `/renew` en demande une nouvelle. Souvent utilisés ensemble lors du dépannage.

---

### Question 5
**Réponse correcte : B**

**Explication :**
Trois approches principales de dépannage OSI :

**Bottom-Up (B) :**
- Commence **Couche 1 (Physique)** → Monte vers **Couche 7 (Application)**
- Vérifier câbles → VLANs → IP → Transport → Application
- Approche la plus courante et systématique

**Top-Down (A) :**
- Commence **Couche 7 (Application)** → Descend vers **Couche 1 (Physique)**
- Utile pour problèmes applicatifs spécifiques

**Divide and Conquer (C) :**
- Commence au **milieu (Couche 3-4)**
- Si OK → problème couches supérieures
- Si KO → problème couches inférieures
- **Approche la plus efficace**

**💡 Point clé :** Bottom-Up est la plus courante car les problèmes réseau commencent souvent à la couche physique (câbles, interfaces).

---

### Question 6
**Réponse correcte : C**

**Explication :**
**Analyse du symptôme :**
- `ping 8.8.8.8` : **FONCTIONNE** → Connectivité IP OK (couches 1-3 OK)
- `ping www.google.com` : **ÉCHOUE** → Problème de résolution de nom

**Diagnostic :**
Le problème est la **résolution DNS**. Le PC ne peut pas convertir "www.google.com" en adresse IP.

**Dépannage :**
```cmd
ipconfig /all              # Vérifier serveur DNS configuré
nslookup www.google.com    # Tester résolution DNS
ipconfig /flushdns         # Vider cache DNS
```

**💡 Point clé :** "Ping IP fonctionne, ping nom échoue" = Toujours un problème DNS.

---

### Question 7
**Réponse correcte : C**

**Explication :**
`show ip interface brief` est LA commande la plus utilisée pour avoir une vue d'ensemble rapide :

```cisco
Router# show ip interface brief
Interface         IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0 192.168.1.1    YES manual up                    up
GigabitEthernet0/1 10.0.0.1       YES manual up                    up
Serial0/0/0        209.165.200.1  YES manual up                    up
```

**Informations affichées :**
- Nom de l'interface
- Adresse IP
- Statut administratif (up/down)
- Protocole (up/down)

**Comparaison :**
- `show interfaces` : Détails TRÈS verbeux (plusieurs pages)
- `show ip interface brief` : Résumé sur une page
- `show ip interface` : Détails couche 3 uniquement

**💡 Point clé :** C'est généralement la PREMIÈRE commande à utiliser lors du dépannage pour avoir une vue d'ensemble rapide.

---

### Question 8
**Réponse correcte : D**

**Explication :**
Les 7 étapes de dépannage :

1. Identifier le problème
2. Établir une théorie
3. Tester la théorie
4. Établir un plan d'action
5. Implémenter la solution
6. Vérifier la fonctionnalité complète
7. **Documenter** ✅

**Pourquoi documenter est critique :**
- Base de connaissances pour futurs problèmes similaires
- Traçabilité des changements
- Formation des nouveaux techniciens
- Conformité et audit
- Éviter répétition des mêmes erreurs

**💡 Point clé :** Beaucoup de techniciens oublient cette étape, mais c'est celle qui apporte le plus de valeur à long terme pour l'équipe et l'organisation.

---

### Question 9
**Réponse correcte : B**

**Explication :**
**traceroute/tracert** trace le chemin complet qu'emprunte un paquet :

```cmd
# Windows
C:\> tracert 8.8.8.8

# Linux/Mac/Cisco
$ traceroute 8.8.8.8
Router# traceroute 8.8.8.8
```

**Fonctionnement :**
- Envoie paquets avec TTL croissant (1, 2, 3...)
- Chaque routeur décrémente TTL et répond quand TTL=0
- Permet de voir chaque saut (hop) jusqu'à destination

**Différence avec ping :**
- **ping** : Test de connectivité simple (destination atteignable ?)
- **traceroute** : Chemin complet avec tous les sauts intermédiaires

**💡 Point clé :** Utiliser traceroute quand ping échoue pour identifier OÙ le trafic s'arrête.

---

### Question 10
**Réponse correcte : C**

**Explication :**
Approche de dépannage **Bottom-Up** : commencer par les couches basses.

**Raisonnement :**
- PC1 fonctionne → Infrastructure réseau globale OK
- PC2 ne fonctionne pas (même VLAN) → Problème spécifique à PC2
- **TOUJOURS vérifier les basiques en premier** : Couche 1 (Physique)

**Vérifications Couche 1 :**
- Câble branché correctement ?
- Câble endommagé ?
- Voyant d'interface allumé ?
- Port switch activé ?

**Commande switch :**
```cisco
Switch# show interfaces FastEthernet0/5
! Vérifier status (up/down), erreurs, collisions
```

**💡 Point clé :** Règle d'or du dépannage : "Vérifier les basiques d'abord". La plupart des problèmes sont physiques (câbles déconnectés, ports shutdown).

---

### Question 11
**Réponse correcte : C**

**Explication :**
**Divide and Conquer (Diviser pour régner)** est généralement la plus efficace :

**Principe :**
1. Tester **couche médiane (3 ou 4)**
2. Si **OK** → Problème dans couches **supérieures (4-7)**
3. Si **KO** → Problème dans couches **inférieures (1-3)**
4. Diviser à nouveau la section problématique

**Avantage :**
- Élimine rapidement la moitié des possibilités
- Plus rapide que Bottom-Up ou Top-Down
- Approche efficace pour techniciens expérimentés

**Comparaison :**
- **Bottom-Up** : Systématique mais peut être long
- **Top-Down** : Bien pour problèmes applicatifs spécifiques
- **Divide and Conquer** : **Le plus efficace**, nécessite expérience

**💡 Point clé :** Testez la connectivité IP (couche 3). Si OK, problème est probablement logiciel/applicatif. Si KO, problème est physique/liaison.

---

### Question 12
**Réponse correcte : B**

**Explication :**
**DNS (Domain Name System)** utilise le **port 53**.

**Protocoles :**
- **UDP 53** : Requêtes DNS standard (la plupart)
- **TCP 53** : Transferts de zone, réponses > 512 bytes

**Ports communs à connaître :**
| Service | Port | Protocole |
|---------|------|-----------|
| DNS | **53** | UDP/TCP |
| DHCP | 67-68 | UDP |
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| SSH | 22 | TCP |
| Telnet | 23 | TCP |
| FTP | 20-21 | TCP |
| SMTP | 25 | TCP |

**💡 Point clé :** DNS = Port 53. Si pare-feu bloque UDP 53, résolution de noms impossible.

---

### Question 13
**Réponse correcte : B**

**Explication :**
**Duplex mismatch** est une cause très fréquente de connectivité intermittente avec collisions.

**Qu'est-ce qu'un duplex mismatch ?**
- Un côté configuré en **Full-duplex**
- Autre côté configuré en **Half-duplex**
- Ou un côté en auto-négociation, l'autre en mode fixe

**Symptômes typiques :**
- Connectivité intermittente
- Performances très dégradées
- Nombreuses collisions
- Erreurs CRC
- Retransmissions

**Vérification :**
```cisco
Switch# show interfaces GigabitEthernet0/1 | include duplex
  Full-duplex, 1000Mb/s    ✅ OK

Switch# show interfaces status
Port      Name          Status    Vlan  Duplex  Speed Type
Gi0/1     to Server     connected 1     a-full  a-1000 10/100/1000BaseTX
```

**Correction :**
```cisco
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# duplex auto
! Ou forcer même valeur des deux côtés
Switch(config-if)# duplex full
Switch(config-if)# speed 1000
```

**💡 Point clé :** Toujours vérifier duplex/speed lors de problèmes de performance ou de connectivité intermittente.

---

### Question 14
**Réponse correcte : A**

**Explication :**
La commande pour vider le cache DNS sous Windows est :

```cmd
ipconfig /flushdns
```

**Résultat :**
```cmd
C:\> ipconfig /flushdns
Successfully flushed the DNS Resolver Cache.
```

**Autres commandes DNS utiles :**
```cmd
ipconfig /displaydns       # Afficher le cache DNS
nslookup <hostname>        # Résoudre un nom manuellement
```

**Quand vider le cache DNS ?**
- Résolution DNS incorrecte (ancienne adresse IP)
- Après modification DNS sur serveur
- Dépannage de problèmes de connectivité web

**💡 Point clé :** Le cache DNS stocke les résolutions récentes pour accélérer les requêtes futures. Le vider force une nouvelle résolution auprès du serveur DNS.

---

### Question 15
**Réponse correcte : B**

**Explication :**
La segmentation par **VLANs** est la méthode recommandée pour petit réseau.

**VLANs typiques :**
- **VLAN Employés** : Utilisateurs internes
- **VLAN Invités** : Visiteurs (accès Internet seulement)
- **VLAN Serveurs** : Serveurs d'entreprise
- **VLAN VoIP** : Téléphones IP (QoS prioritaire)
- **VLAN Management** : Administration des équipements

**Avantages :**
- **Sécurité** : Isolation du trafic entre groupes
- **Performance** : Réduction des domaines de broadcast
- **Flexibilité** : Changement facile sans recâblage
- **QoS** : Priorité pour VoIP/vidéo

**💡 Point clé :** Les VLANs permettent une segmentation logique sur un switch physique unique, idéal pour petit réseau avec budget limité.

---

### Question 16
**Réponse correcte : C**

**Explication :**
**NTP (Network Time Protocol)** synchronise l'heure entre les équipements.

**Pourquoi c'est important ?**
- **Logs corrélés** : Identifier séquence d'événements
- **Authentification** : Kerberos, certificats (sensibles à l'heure)
- **Conformité** : Audit et réglementations
- **Débogage** : Comprendre chronologie des problèmes

**Configuration Cisco :**
```cisco
Router(config)# ntp server 132.163.96.1
! NTP serveur du NIST (États-Unis)

Router(config)# ntp server pool.ntp.org
! Pool public de serveurs NTP

! Vérification
Router# show ntp status
Router# show ntp associations
```

**Port :** UDP 123

**💡 Point clé :** Sans synchronisation NTP, impossible de corréler les logs de plusieurs équipements lors du dépannage d'incidents.

---

### Question 17
**Réponse correcte : B**

**Explication :**
`show ip dhcp binding` affiche les "baux" (leases) DHCP actifs :

```cisco
Router# show ip dhcp binding
IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.1.10     0100.1122.3344.55      Mar 03 2026 12:00 PM    Automatic
192.168.1.11     0100.5566.7788.99      Mar 03 2026 01:30 PM    Automatic
```

**Informations affichées :**
- Adresse IP attribuée
- Adresse MAC du client
- Date d'expiration du bail
- Type (Automatic, Manual)

**Autres commandes DHCP utiles :**
```cisco
show ip dhcp pool              # Configuration des pools
show ip dhcp conflict          # Conflits d'adresses
show ip dhcp server statistics # Statistiques serveur
```

**💡 Point clé :** Utiliser cette commande pour vérifier qu'un client a bien reçu une adresse DHCP, et quelle adresse.

---

### Question 18
**Réponse correcte : B**

**Explication :**
La longueur maximale pour un câble **Ethernet UTP** est **100 mètres** entre deux équipements actifs.

**Pourquoi 100m ?**
- Atténuation du signal sur le cuivre
- Standards Ethernet (10/100/1000Base-T)
- Au-delà : Erreurs, perte de paquets, perte de liaison

**Si > 100m nécessaire :**
- **Utiliser switch intermédiaire** : Régénère le signal
- **Utiliser fibre optique** : Distances beaucoup plus longues (km)

**Distances maximales selon le média :**
| Média | Distance max |
|-------|--------------|
| UTP Cat5e/6 | 100 m |
| Fibre multimode | 2-550 m (selon type) |
| Fibre monomode | 10-40 km+ |

**💡 Point clé :** Si problème de connectivité, toujours vérifier longueur de câble UTP < 100m. Un câble trop long = symptômes intermittents.

---

**Score recommandé pour valider le module : 14/18 minimum (78%)**

**Révision conseillée si score < 14/18 :**
- Section 17.6 (Méthodologies de dépannage)
- Section 17.5 (Commandes hôte et IOS)
- Scénarios de dépannage pratiques

**Félicitations pour avoir complété le cours ITN !**
