# Module 15 : Services IP
## Notes Complètes de Révision

---

## 1. SYNCHRONISATION DU TEMPS

### Importance critique de la synchronisation temporelle

La synchronisation du temps est bien plus qu'une commodité dans les réseaux modernes – elle est fondamentale pour la sécurité et la fiabilité. Chaque périphérique réseau dépend d'une compréhension précise du moment actuel pour plusieurs raisons critiques :

**Intervalles de mot de passe et rotation de clés** : Les politiques de sécurité exigent que les mots de passe expirent après une période définie. Si un périphérique ignore que 90 jours se sont écoulés, il ne peut pas appliquer cette politique de manière fiable. De même, les clés cryptographiques doivent être renouvelées selon des calendriers stricts. Sans synchronisation temporelle, ces rotations deviennent impossibles à garantir.

**Validité des certificats** : Les certificats X.509, utilisés dans les VPN, le HTTPS et autres protocoles sécurisés, ont des dates de validité précises (« valide à partir de » et « expire le »). Un périphérique avec une horloge décalée pourrait rejeter un certificat valide ou accepter un certificat expiré, compromettant la sécurité.

**Intégrité du chiffrement** : Certains algorithmes de chiffrement utilisent des timestamps comme parties des nonces ou des données entrantes. Un désalignement temporel peut invalider les opérations cryptographiques.

**Corrélation des événements de sécurité** : Lors d'une enquête sur une violation ou un incident, les analystes examinent les journaux provenant de plusieurs périphériques. Si les horloges ne sont pas synchronisées, il devient impossible de déterminer l'ordre chronologique des événements, rendant l'analyse criminalistique pratiquement impossible.

**Dépannage réseau** : Les administrateurs comparent les timestamps des journaux pour diagnostiquer les problèmes. Des horloges désynchronisées transforment une tâche de diagnostic simple en cauchemar frustrant.

### Network Time Protocol (NTP) - Fondamentaux

Le Network Time Protocol est le protocole standard de l'industrie pour synchroniser les horloges sur les réseaux IP. NTP a été développé pour fonctionner sur des réseaux avec des délais variables et des défaillances matérielles, ce qui le rend extraordinairement robuste.

**Architecture NTP : Modèle Client-Serveur**

NTP fonctionne selon un modèle hiérarchique où :
- Les serveurs NTP primaires se connectent à des sources externes (appelées horloges de référence)
- Les serveurs secondaires se synchronisent auprès des serveurs primaires
- Les clients se synchronisent auprès des serveurs

Un appareil peut jouer plusieurs rôles simultanément – être client pour un serveur supérieur tout en servant de serveur pour les appareils inférieurs.

**Concept hiérarchique : Les strates NTP**

NTP utilise un système de strates pour représenter la distance par rapport à une horloge de référence absolue :

- **Stratum 0** : Horloges atomiques, récepteurs GPS, sources de temps absolues. Aucun appareil NTP n'est un stratum 0 – il s'agit simplement de la source de référence.
- **Stratum 1** : Appareils directement connectés à une horloge stratum 0. Exemples : récepteurs GPS dédiés, serveurs NTP primaires dotés d'une horloge atomique interne.
- **Stratum 2** : Se synchronisent auprès des serveurs stratum 1. Typiquement des serveurs NTP secondaires dans une entreprise.
- **Stratum 3** : Se synchronisent auprès des serveurs stratum 2, et ainsi de suite jusqu'au stratum 15.
- **Stratum 16** : Indique une source non synchronisée ou non fiable. Les appareils au stratum 16 ne sont pas considérés comme synchronisés.

**Préférence des strates et sélection du serveur**

NTP sélectionne automatiquement son serveur de plus haute qualité en considérant :
1. Le stratum du serveur (plus bas = meilleur)
2. La latence réseau vers le serveur
3. La dispersion (variation des délais)
4. L'accessibilité du serveur

Un périphérique peut être configuré pour peer avec plusieurs serveurs NTP. NTP teste périodiquement chaque serveur et choisit dynamiquement le meilleur pour une synchronisation continue.

**Précision NTP et convergence**

Une idée fausse courante est que NTP atteint instantanément une haute précision. En réalité :
- La précision typique est dans la **plage de dizaines de millisecondes** (10-100 ms)
- Atteindre cette précision nécessite **plusieurs heures à plusieurs jours de convergence** après qu'un périphérique démarre ou se reconnecte
- Les périphériques avec une dérive d'horloge initiale importante (plusieurs secondes) peuvent mettre plus longtemps à converger
- Une fois convergé, NTP maintient la synchronisation en effectuant des ajustements petits et continus de l'horloge système

### Configuration NTP sur Cisco IOS

**Configuration basique du client NTP**

```
Router(config)# ntp server 10.1.1.100
Router(config)# ntp server 10.1.1.101
Router(config)# ntp server 10.1.1.102 prefer
```

La commande `ntp server <adresse-ip>` configure le routeur pour synchroniser son horloge auprès du serveur NTP spécifié. Le mot-clé optionnel `prefer` désigne un serveur comme le serveur préféré – NTP sélectionnera ce serveur en priorité si accessible.

**Spécification de l'interface source**

```
Router(config)# ntp source GigabitEthernet0/0/0
```

Dans les réseaux complexes, un routeur peut avoir plusieurs interfaces avec différentes adresses IP. Par défaut, NTP sélectionne l'adresse source en fonction de l'interface de sortie vers le serveur NTP. Le mot-clé `source` force l'utilisation d'une interface spécifique pour tous les paquets NTP sortants.

**Configuration du serveur NTP**

```
Router(config)# ntp master 2
```

Cette commande transforme le routeur en serveur NTP autonome qui publicise sa propre horloge système. Le paramètre (2 dans cet exemple) spécifie le stratum que le routeur prétendra avoir. Un routeur non synchronisé avec horloge uniquement système ne devrait utiliser que stratum 10 ou supérieur pour éviter qu'un autre équipement ne s'y synchronise accidentellement.

**Configuration des peers NTP (synchronisation bidirectionnelle)**

```
Router(config)# ntp peer 10.1.1.100
Router(config)# ntp peer 10.1.1.101
```

Le mode peer configure une relation bidirectionnelle où les deux routeurs se synchronisent mutuellement. Ceci est plus robuste que client-serveur pour les appareils de même stratum, car si le serveur primaire demeure indisponible, les peers peuvent continuer à fonctionner ensemble.

### Vérification NTP

```
Router# show ntp status
```

Cette commande affiche :
- **Clock offset** : Différence entre l'horloge du routeur et le serveur référence (en millisecondes)
- **Frequency adjustment** : Quantité d'ajustement appliquée pour corriger la dérive
- **System peer** : Adresse IP du serveur NTP actuellement utilisé pour la synchronisation
- **Reference ID** : L'horloge de référence de stratum supérieur sur laquelle repose le système

```
Router# show ntp associations
```

Affiche les associations actuelles avec les serveurs/peers NTP :
- **address** : Adresse IP du serveur NTP
- **ref clock** : Identifiant du serveur de référence
- **st** : Stratum du serveur
- **when** : Temps écoulé depuis la dernière synchronisation (en secondes)
- **poll** : Intervalle de polling en secondes
- **reach** : Masque d'accessibilité (255 = tous les 8 derniers polls ont réussi)
- **delay** : Latence réseau aller-retour vers le serveur
- **offset** : Différence horaire entre ce routeur et le serveur
- **disp** : Dispersion (variation estimée)

---

## 2. PROTOCOLES DE REDONDANCE DU PREMIER SAUT

### Importance de la résilience réseau

La redondance à la couche 3 est critique pour la disponibilité continue des services réseau. Un seul point de défaillance au niveau des passerelles peut mettre toute une DMZ, un VLAN ou un segment hors ligne – un risque commercial inacceptable.

### Problème : Comment les hôtes trouvent-ils la passerelle préféée ?

Les hôtes dans un sous-réseau (par exemple, 192.168.1.0/24) doivent router le trafic vers le reste du réseau. Mais à quel routeur ou commutateur (la passerelle par défaut) un appareil se fie-t-il ?

Traditionnellement, les administrateurs configurent manuellement une passerelle par défaut statique sur chaque hôte. Mais que se passe-t-il lorsque cette passerelle s'arrête ? L'hôte ne détecte pas automatiquement la panne et continue à envoyer du trafic vers une passerelle morte. Il n'y a pas de basculement automatique.

**Solution : Les protocoles de redondance du premier saut (FHRP)**

Les FHRP résolvent ce problème en créant une **adresse IP virtuelle (VIP)** partagée entre plusieurs appareils physiques à la couche 3 (routeurs ou commutateurs de couche 3). Les hôtes configurent cette VIP partagée comme leur passerelle par défaut. Lorsque le routeur actuel cesse de fonctionner, un routeur secondaire prend rapidement en charge, et le trafic des hôtes continue sans interruption majeure.

### Trois options FHRP

**HSRP (Hot Standby Routing Protocol)** : Protocole propriétaire Cisco développé dans les années 1990. Nécessite au moins 2 routeurs (un actif + un standby). Domine l'infrastructure existante de Cisco.

**VRRP (Virtual Router Redundancy Protocol)** : Défini dans RFC 3768, c'est un standard de l'industrie. Fonctionne sur Cisco, Juniper, Mikrotik et autres. Plus moderne que HSRP mais moins riche en fonctionnalités.

**GLBP (Gateway Load Balancing Protocol)** : Protocole Cisco propriétaire qui combine redondance ET équilibrage de charge à la couche 3. Permet de partager le trafic entre plusieurs routeurs actifs au lieu d'avoir un routeur actif passif et un routeur en attente.

### Object Tracking : Flexibilité véritable pour FHRP

Object Tracking est un mécanisme flexible pour lier les décisions FHRP à des conditions réseau très spécifiques. Au lieu de basculer uniquement en fonction de la perte de lien local, un FHRP peut suivre :

**Suivi des routes**

```
Router(config)# track 10 ip route 0.0.0.0/0 reachability
Router(config-if)# standby 1 track 10 decrement 30
```

Le numéro de track (10) suit la reachabilité d'une route spécifique. Si la route 0.0.0.0/0 devient inaccessible (par exemple, le lien WAN sort, rendant la route par défaut inaccessible), le track 10 devient « down ». La commande `standby track` abaisse la priorité du routeur de 30 points. Si ce routeur avait une priorité de 100, il tomberait à 70, cédant le rôle actif à un routeur par défaut avec priorité 100.

**Suivi du protocole de ligne d'interface**

```
Router(config)# track 20 interface GigabitEthernet0/0/1 line-protocol
Router(config-if)# standby 1 track 20 decrement 15
```

Suit l'état du protocole de ligne d'une interface physique. Si l'interface passe à « down », le statut du track change. C'est utile pour le basculement rapide si une interface directe d'accès perd sa connexion.

```
Router# show track [20]
```

Affiche le statut actuel de tous les tracks ou d'un track spécifique, y compris son statut (up/down), ses raisons de changement d'état, etc.

### HSRP: Hot Standby Routing Protocol

**Architecture : Actif + Standby**

HSRP exige au minimum 2 appareils (mais prend en charge jusqu'à 16 par groupe sur IOS classique, 4096 sur IOS-XE) :

- **Routeur actif** : Accepte et transfère le trafic destiné à l'adresse IP virtuelle HSRP. Annonce périodiquement les « hello » multidiffusion.
- **Routeur standby** : Écoute les hello du routeur actif. Si les hello cessent pendant un délai d'attente (defaut 10 secondes), il assume immédiatement le rôle actif.

**Adresse IP virtuelle et adresse MAC virtuelle**

Chaque groupe HSRP possède :
- Une **adresse IP virtuelle** : Par exemple, 192.168.1.1 (partagée par le groupe)
- Une **adresse MAC virtuelle** : 0000.0c07.ac0X (où X = numéro de groupe HSRP)

Les hôtes configurent la VIP comme passerelle par défaut et envoient des ARP pour « 192.168.1.1 ». Le routeur actif répond avec la MAC virtuelle. Après un basculement, le nouveau routeur actif répond aux ARP pour la même adresse avec la même MAC. Aucun hôte ne sait ou ne se soucie qu'un basculement s'est produit.

**Mécanisme de détection des défaillances : Multicast Hello**

```
Router(config)# standby 1 ip 192.168.1.1
```

Cela crée un groupe HSRP nommé 1 avec VIP 192.168.1.1. Les routeurs du groupe multicellent des messages HSRP à 224.0.0.102 :1985 (UDP).

- **Hello par défaut** : 3 secondes
- **Timeout par défaut (hold time)** : 10 secondes

Si le routeur actif n'envoie pas de hello pendant 10 secondes, le standby déclare le routeur actif décédé et prend son rôle. Le délai de basculement typique est donc ~10 secondes.

**Élection : Priorité et adresse IP**

```
Router(config)# standby 1 priority 110
```

Les routeurs élisent le routeur actif en fonction de la priorité (par défaut 100). Le routeur avec la priorité la plus élevée remporte. En cas d'égalité (deux routeurs avec priorité 100), l'adresse IP la plus élevée du groupe gagne. Donc, un routeur avec 192.168.1.254 battrait celui avec 192.168.1.10.

**Préemption : Doit-on reprendre le contrôle ?**

```
Router(config)# standby 1 preempt
```

Par défaut, HSRP est **non-préemptif**. Si le routeur primaire (priorité la plus élevée) redémarre après une panne maténielle, il ne récupère automatiquement pas le rôle actif. Le routeur actuellement actif conserve son rôle, même s'il a une priorité inférieure. Ceci évite une instabilité si le routeur primaire alterne entre panne et récupération.

En activant `preempt`, le routeur reprendra le rôle actif dès qu'il aura une priorité supérieure au routeur actif actuel. Ceci est utile pour les scénarios où un routeur principal est clairement supérieur et doit contrôler le groupe HSRP.

**Versions HSRP : v1 vs v2**

- **HSRPv1** : Format original, groupes 0-255, adresses MAC 0000.0c07.ac00-0000.0c07.acff
- **HSRPv2** : RFC 3768 compatible, groupes 0-4095, adresses MAC 0000.0c9f.f000-0000.0c9f.ffff, support IPv6

La configuration de HSRPv2 est similaire, avec juste :

```
Router(config)# standby version 2
Router(config-if)# standby 1 ip 192.168.1.1
```

**Configuration de base HSRP**

```
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip address 192.168.1.254 255.255.255.0
Router(config-if)# standby 1 ip 192.168.1.1
Router(config-if)# standby 1 priority 110
Router(config-if)# standby 1 preempt
Router(config-if)# standby 1 timers 3 10
Router(config-if)# standby 1 authentication md5 key-string MySecretKey123!
```

---

## 3. TRANSLATION D'ADRESSES RÉSEAU (NAT)

### Concept fondamental

NAT traduit les adresses IP d'un domaine de réseau à un autre. Le cas classique : une entreprise avec des serveurs Web sur un réseau privé (192.168.1.0/24) veut que le public Internet y accède. NAT transforme les adresses sources des paquets sortants du réseau privé en adresses publiques routables, et traduit inversement les réponses entrantes.

### Types de NAT

**NAT statique : Cartographie 1:1**

```
Router(config)# ip nat inside source static 192.168.1.50 203.0.113.50
```

Une adresse privée (192.168.1.50) est toujours traduite vers la même adresse publique (203.0.113.50). Utile pour les serveurs Web, serveurs de messagerie – n'importe quel service qui doit être accessible via une adresse stable de l'extérieur.

**NAT dynamique : Pool d'adresses**

```
Router(config)# ip nat pool OUTSIDE 203.0.113.100 203.0.113.120 netmask 255.255.255.0
Router(config)# ip nat inside source list 1 pool OUTSIDE
```

Les clients privés (définis par ACL 1) reçoivent temporairement une adresse du pool. Lorsque la session se termine, l'adresse retourne au pool. Efficace pour les réseaux où de nombreux clients internes accèdent au réseau externe.

**PAT (Port Address Translation) : Many-to-One**

```
Router(config)# ip nat inside source list 1 interface GigabitEthernet0/0/1 overload
```

Tous les clients internes parttagent une seule adresse publique en variant les ports dans l'en-tête TCP/UDP. Par exemple :
- Client 192.168.1.10:5678 → NAT to 203.0.113.1:6001
- Client 192.168.1.11:5679 → NAT to 203.0.113.1:6002

Le routeur NAT maintient une table de traductions pour démultiplexer les réponses entrantes vers le client correct. C'est l'approche standard pour les petites entreprises et les connexions ISP – une adresse publique sert des centaines de clients internes.

### Terminologie : Inside/Outside, Local/Global

- **Inside local** : Adresse IP utilisée par un hôte sur le réseau interne (par exemple, 192.168.1.50)
- **Inside global** : Adresse NAT assignée à l'hôte interne, vue par le réseau externe (par exemple, 203.0.113.50)
- **Outside local** : Adresse IP d'un hôte externe telle que vue par le réseau interne (typiquement identique à outside global)
- **Outside global** : Véritable adresse de l'hôte externe (par exemple, 8.8.8.8 pour Google DNS)

### Commandes de configuration NAT

```
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip nat inside

Router(config)# interface GigabitEthernet0/0/1
Router(config-if)# ip nat outside
```

D'abord, désigner les interfaces : les interfaces vers le réseau privé sont « inside », celles vers le public sont « outside ».

```
Router(config)# ip access-list extended INTERNAL
Router(config-ext-nacl)# permit ip 192.168.1.0 0.0.0.255 any
```

Définir ce trafic interne doit être traduit.

```
Router(config)# ip nat inside source list INTERNAL pool OUTSIDE
```

Créer la translation en mappant l'ACL aux adresses publiques.

### Vérification NAT

```
Router# show ip nat translations
```

Affiche toutes les traductions NAT actuelles actives – très utile pour vérifier que le trafic se traduit comme prévu.

```
Router# show ip nat statistics
```

Affiche les statistiques NAT : nombre total de traductions, nombre d'adresses dans les pools, etc.

```
Router# debug ip nat
```

Avec cette activation, chaque paquet traduit produit une entrée de débogage détaillée, utile pour le dépannage des problèmes NAT complexes.

---

## Résumé et Points clés

1. **NTP** : Standard de l'industrie pour la synchronisation temporelle précise. Les strates hiérarchiques organisent les serveurs. La convergence prend des heures/jours, pas des minutes.

2. **FHRP** : HSRP/VRRP/GLBP fournissent une passerelle virtuelle partagée. Object Tracking ajoute de la flexibilité en liant les basculements à des conditions spécifiques du réseau.

3. **HSRP** : Propriétaire Cisco, priorité + adresse IP pour l'élection. Non-préemptif par défaut. Détection de défaillance via hellos multidiffusion toutes les 3 secondes.

4. **NAT** : Traduit entre deux domaines d'adresse. Static (1:1), Dynamic (pool), PAT (many-to-one). Étiquetage inside/outside critique pour configuration.

---

*Dernière révision : 18 mars 2026*
*Pour révision CCNP ENCOR Module 15*
