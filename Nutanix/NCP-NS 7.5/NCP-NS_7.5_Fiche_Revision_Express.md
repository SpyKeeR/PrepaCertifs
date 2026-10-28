# 🎯 NCP-NS 7.5 : Fiche de révision express (Nutanix Flow)

> Objectif : comprendre la techno et le **contexte des questions** en ~45 min de lecture.
> Ton atout : tu fais déjà du BGP/OSPF en prod chez un opérateur. 70% de Flow, c'est du SDN overlay + du firewall distribué. Le vrai travail ici, c'est de **mapper tes réflexes réseau sur le vocabulaire Nutanix**.

---

## 📋 Le cadre de l'examen (blueprint officiel)

| Paramètre | Valeur |
|---|---|
| Questions | 75 (choix multiple + réponses multiples) |
| Durée | 120 minutes |
| Score de passage | 3000 (échelle scaled de 1000 à 6000) |
| Langues | Anglais, Japonais |
| Versions testées | **Flow Virtual Networking 6.0**, **Flow Network Security 5.2**, **Prism Central 7.3** |

Les 5 sections du blueprint :

1. Configure Flow Virtual Networking (FVN)
2. Configure Flow Network Security (FNS)
3. Troubleshoot FVN
4. Troubleshoot FNS
5. Deploy & Upgrade

💡 **Retiens les numéros de version.** L'examen aime les questions du type "quelle version minimale pour la feature X".

---

## 🧠 La grande image : Flow = 2 produits distincts

C'est LE point à ancrer en premier, parce que la moitié des questions jouent sur la confusion entre les deux.

### FVN (Flow Virtual Networking) = le réseau
SDN overlay sur AHV. Il crée des **VPC** (réseaux virtuels isolés) avec leurs propres subnets, routage, gateways, NAT, VPN, BGP. C'est ton monde d'opérateur, transposé en logiciel.

### FNS (Flow Network Security) = le firewall
Micro-segmentation. Firewall distribué **stateful** qui filtre le trafic entre VM (East-West surtout) selon des **catégories**, pas des adresses IP.

⚠️ **Piège récurrent : deux notions de "policy" qui n'ont rien à voir.**

| | Network Policy (FVN) | Security Policy (FNS) |
|---|---|---|
| Nature | **Stateless** | **Stateful** |
| Où | Au niveau du virtual router du VPC | Distribué sur chaque hôte AHV |
| Rôle | PBR, permit/deny/reroute inter-subnet | Micro-segmentation applicative |
| Priorité | Valeurs **10 à 1000** (plus haut = prioritaire) | Ordre fixe par type (voir plus bas) |

### L'architecture en 3 plans (à connaître par coeur)

```
Management plane  →  Prism Central (config des policies, visibilité globale)
Control plane     →  Network Controller (conteneurisé, distribue les flow rules,
                     provisionne les subnets en OVN logical switches)
Data plane        →  Open vSwitch (OVS) sur chaque hôte AHV (forwarding réel)
```

Encapsulation overlay : **Geneve** (transport inter-hôtes sans toucher les VLAN physiques).

Les bridges OVS (utile pour le troubleshooting) :
- 🔧 `br0` : réseau VLAN classique, porte les uplinks physiques
- 🔧 `brAtlas` : subnets FVN (overlay + controller-managed VLAN), gérés en OVN
- 🔧 `br.microseg` : enforcement FNS (les règles de firewall sont programmées ici)
- 🔧 `virbr0` : réseau interne AOS

### 📌 À retenir
- **FVN = réseau, FNS = sécurité.** Deux produits, deux versions, deux logiques.
- Network Policy (FVN) = stateless / Security Policy (FNS) = stateful. Ne pas confondre.
- 3 plans : Prism Central (mgmt) / Network Controller (control) / OVS (data).
- Overlay via Geneve. Enforcement FNS sur `br.microseg`, subnets FVN sur `brAtlas`.
- Versions clés : FVN 6.0, FNS 5.2, PC 7.3.

---

## 🌐 Section 1 : Configurer Flow Virtual Networking

### VPC : tenant vs transit

Un **VPC** = ton réseau virtuel isolé, avec un espace d'adressage à lui (les VPC peuvent avoir des IP qui se chevauchent, c'est le principe du multi-tenant).

- **Tenant VPC** (ou "user"/"regular") : héberge tes workloads.
- **Transit VPC** : un VPC **hub** en architecture hub-and-spoke. Il centralise le routage North-South pour beaucoup de VPC et permet de router entre VPC **via IP privées (ERP), sans passer par l'infra physique**.

⚠️ Piège transit VPC : le BGP Gateway du transit VPC **ne dessert que le transit VPC**. Pour qu'il annonce les préfixes des VPC réguliers connectés, tu dois **ajouter les ERP des VPC réguliers dans la liste d'ERP du transit VPC**. Sinon, pas d'annonce (et Prism Central lève l'alerte **802007**).

### ERP : le concept central à comprendre

**ERP = Externally Routable Prefix.** C'est une **liste de préfixes que tu choisis d'exposer** hors du VPC.

- Un subnet du VPC **ajouté à l'ERP** devient **routable** (joignable de l'extérieur, annoncé en BGP).
- Un subnet **hors ERP** reste **privé** (communique en interne au VPC, sort via NAT si besoin).

C'est exactement une logique de **redistribution/route-map sélective** que tu connais : tu décides quel préfixe fuit vers le monde extérieur.

### External Networks : NAT vs No-NAT

C'est la question de design qui revient tout le temps.

| | NAT External Network | No-NAT External Network |
|---|---|---|
| Translation | Oui. Egress via une **SNAT IP** prise dans le subnet externe | **Aucune** translation |
| Exposition | IP du VPC cachées. Inbound 1:1 via **Floating IP** | IP du VPC **exposées telles quelles** (via ERP + BGP) |
| Overlap IP | Toléré (isolé) | **Interdit** (l'espace n'est plus isolé) |
| Cas d'usage | Isolation, multi-tenant | Intégration au routage d'entreprise, hybrid cloud |

💡 Un VPC peut avoir **max 1 NAT + 1 No-NAT** simultanément. Dans ce cas, l'un des deux porte la **default route** (0.0.0.0/0), l'autre reçoit des routes plus spécifiques.

### Floating IP
IP publique/externe mappée **1:1** vers une VM (NAT statique) quand tu es en connectivité NAT. C'est ton "static one-to-one NAT" habituel.

⚠️ **Gros piège d'examen** : une **Floating IP contourne les Isolation policies** de FNS (FNS ne tient pas compte des floating IP dans le calcul de destination). À manier avec précaution.

### BGP dans Flow (la zone la plus dure d'après les retours)

Le **BGP Gateway** fonctionne comme un **route server** :
- Il **annonce les ERP** vers l'infra physique (les routeurs ToR).
- Il **apprend** les routes externes et les distribue dans les VPC.
- ⚠️ Il est en **control plane uniquement, PAS dans le data path**. Le forwarding réel reste distribué sur les hôtes AHV. C'est le piège classique : "le gateway BGP transporte-t-il le trafic ?" → **non**.

Ce que Flow te donne (et que tu connais déjà) :
- **Priorité de session BGP** : nombre plus élevé = plus prioritaire.
- **AS-Path Prepend** : pour l'actif/backup multi-AZ. L'AZ de secours prepend son ASN pour rendre son chemin moins préférable. Failover automatique en cas de panne du primaire. Configurable **par session**.
- **ERP filtering (session-scoped)** : annoncer un sous-ensemble d'ERP différent par voisin (ex : préfixes complets vers "Corporate", préfixes restreints vers "DMZ").
- **Add-Path (RFC 7911)** : annoncer plusieurs chemins pour un même préfixe (ECMP, fast reroute), utile en scale-out gateway. Capability code **69**.

### Les autres gateways
- **VPN Gateway** : tunnels **IPsec** entre clusters ou vers un site externe. Policy-based ou route-based.
- **VTEP Gateway** : **extension L2** d'un subnet overlay entre sites/AZ (VXLAN). Utile pour garder les IP lors d'une migration (L2 adjacency).

### Network Load Balancer
Répartit le trafic applicatif sur un **target group de VM**. Question type : "créer un LB avec un groupe cible".

### Policy-Based Routing (PBR)
Redirige des flux spécifiques (ex : vers une appliance de sécurité pour inspection). Rappel : c'est une **network policy stateless** au niveau du virtual router (priorité 10-1000).

### Nutanix IPAM (DHCP)
- **Optionnel** pour les VLAN-backed subnets.
- **Obligatoire** pour les Overlay subnets.
- Permet réservations DHCP (assignation statique garantie).

### 📌 À retenir
- **ERP = ce que tu exposes.** Subnet dans l'ERP = routable/annoncé ; hors ERP = privé.
- **NAT** (SNAT + Floating IP, overlap OK) vs **No-NAT** (exposition directe via BGP, overlap interdit).
- **BGP Gateway = route server, pas dans le data path.** Le forwarding reste sur les AHV.
- **Transit VPC** = hub-and-spoke ; ses ERP doivent inclure ceux des VPC réguliers (sinon alerte 802007).
- **Floating IP contourne les Isolation policies** (piège majeur).
- Gateways : BGP (route server), VPN (IPsec), VTEP (extension L2).

---

## 🔒 Section 2 : Configurer Flow Network Security

### Le modèle : catégories, pas adresses IP

FNS applique des policies à des **catégories** = paires clé-valeur (`Environment:Production`, `AppType:Web`, `AppTier:DB`). Une VM hérite de la policy **selon ses catégories, indépendamment de son IP**. C'est ça la puissance : la sécurité suit la VM.

- L'enforcement se fait **sur l'IP détectée** (Acropolis intercepte DHCP/ARP pour connaître l'IP). Les **Isolation policies** filtrent sur **IP + MAC**.
- Firewall **distribué et stateful**, programmé dans `br.microseg` sur chaque hôte via OVS/OpenFlow.

### Les 4 types de policy et leur ORDRE d'évaluation

⚠️ **C'est LA table à mémoriser.** Évaluation en **first-match**, dans cet ordre précis (FNS 5.2) :

| Priorité | Type | Rôle |
|---|---|---|
| 1 (max) | **Quarantine** | Isoler une VM compromise |
| 2 | **Shared Services** | 🆕 nouveau en 5.2. Services communs (DNS, monitoring, AD) accessibles à tous |
| 3 | **Isolation** | Bloquer tout trafic entre 2+ catégories |
| 4 | **Application** | "Ring-fencing" : définir explicitement inbound/outbound autorisés (implicit deny) |

Dans **Application**, on trouve les **VDI policies** (basées sur l'identité AD).

💡 Détails Quarantine :
- **Strict** : bloque TOUT (inbound + outbound).
- **Forensic** : bloque tout SAUF le trafic vers des outils de sécurité définis (pour que l'équipe SOC puisse analyser la VM).
- Quarantine peut être déclenchée manuellement OU par API (ex : un EDR détecte une menace et appelle Prism Central).

⚠️ **Quarantine > Isolation** : si une VM est dans les deux (enforced), la Quarantine gagne.

### Les modes de policy (le workflow le plus testé)

| Mode | Comportement |
|---|---|
| **Save** | Brouillon. Créée mais pas appliquée. |
| **Monitor** (Apply/Monitor) | Laisse **tout passer** mais **visualise ce qui SERAIT bloqué**. Sert à découvrir les flux légitimes. |
| **Enforce** (Apply/Enforce) | Applique : autorise les flux définis, **droppe tout le reste** (implicit deny). |

🎯 **Le workflow Monitor → Enforce est le scénario le plus testé de l'examen.** La logique Nutanix :
1. Tu appliques en **Monitor**.
2. Tu **observes les flux réels** dans la visualisation.
3. Tu valides que tu comprends qui parle à qui, tu ajoutes les exceptions manquantes.
4. **Ensuite seulement** tu passes en **Enforce**.

La raison (comprends le "pourquoi", pas juste le "quoi") : enforcer sans passer par Monitor **bloque du trafic légitime** en production. L'examen teste ce raisonnement.

⚠️ Piège Monitor : si un flux matche une policy **en Monitor**, l'action est "forward + log comme autorisé", et **l'évaluation s'arrête là** (first-match). Même si une policy plus bas (Enforce) l'aurait bloqué, elle n'est jamais atteinte.

### Visualisation vs Hit Logs (piège des 24h)
- **Visualisation** (Prism Central) : montre les flux **< 24h**. Pour construire les policies.
- **Policy Hit Logs** : trace allow/deny par flux, **exportables en syslog** pour analyser les flux **> 24h** et l'audit.

### Intégration Active Directory (VDI / Identity-based)
- **VDI policies** : appliquent une catégorie à une VM VDI **selon les groupes AD de l'utilisateur connecté** (firewall basé sur l'identité).
- Nécessite : AD configuré (URL, compte de service, credentials), **ID-Based Security** activé, groupes AD référencés.
- 💡 Bonne pratique : appliquer une **policy de base par défaut** aux VM VDI **avant** le login (sécurisées dès l'allumage).

### Syslog / Service Insertion
- **Syslog** : expédier les logs de policy vers un collecteur externe (analyse, audit, rétention > 24h).
- **Service Insertion** : voir Section 4 (feature testée à part).

### Constructs réutilisables
- **Services** : combinaisons protocole/port réutilisables.
- **Address Groups** : IP/subnets réutilisables.
- **Entity Groups** (🆕 5.2) : groupes dynamiques basés sur une **combinaison de catégories** (ex : `App:PubSite` + `Env:Prod` + `AppTier:Web`).

### Limites Isolation policy (chiffres testables)
- Min **2**, max **32** entités par policy.
- Max **10** catégories par entité.
- Fait de l'**isolation L2** (broadcast, unknown-unicast, multicast droppés ; IPv6 bloqué par défaut).

### 📌 À retenir
- FNS filtre par **catégories** (clé-valeur), pas par IP. La sécurité suit la VM.
- Ordre d'évaluation (first-match) : **Quarantine > Shared Services > Isolation > Application**.
- Quarantine **Strict** (tout bloqué) vs **Forensic** (accès outils SOC autorisé).
- Workflow **Monitor → Enforce** = LE scénario clé. Monitor observe, Enforce bloque.
- **Visualisation < 24h ; Hit logs (syslog) pour > 24h.**
- VDI = identity-based via groupes AD. Shared Services et Entity Groups sont nouveaux en 5.2.

---

## 🔧 Section 3 : Troubleshoot Flow Virtual Networking

Approche : diagnostic **de bas en haut** (VM → subnet → routeur VPC → gateway → infra).

### Scénarios de connectivité classiques

- **VM ne joint pas Internet** : vérifier default route du VPC, external network attaché (NAT/No-NAT), SNAT IP, santé du gateway.
- **2 VM du même VPC ne se parlent pas** : souvent une **Security policy FNS** (Isolation/Application) qui bloque, pas un problème réseau. Vérifier les catégories et les hit logs.
- **VM ne joint pas l'external network** : subnet dans l'ERP ? route présente ? gateway healthy ?
- **Le voisin BGP ne reçoit pas les routes attendues** : le subnet est-il **dans l'ERP** ? (cause n°1). Pour un transit VPC : les ERP des VPC réguliers sont-ils bien dans l'ERP du transit ?

### Santé des Gateway VM
Vérifier qu'une Gateway VM (**VTEP, VPN ou BGP**) est healthy. Un gateway down casse la connectivité correspondante (extension L2, tunnel IPsec, annonces BGP).

### Subnet extension (VTEP)
Vérifier que l'extension L2 est **active et healthy**. Elle augmente la complexité opérationnelle (spanning L2), donc à utiliser avec parcimonie.

### Network Controller
- 🔧 C'est le control plane. Vérifier sa **santé** (health check attributes) et sa **version**.
- ⚠️ **Ne jamais désactiver le Network Controller si des features FVN tournent.**
- Quand il est unhealthy, certaines actions sont impossibles (création/modif de subnets overlay, etc.).

### Alertes et logs
- **Diagnostiquer l'état BGP** via les session logs (Established ? advertised/received routes ?).
- **Savoir qui a fait quel changement et quand** (audit).
- **IPFIX** : export de flow data (façon NetFlow). Sert à **analyser les patterns de trafic** et **diagnostiquer un problème de routing ou de perf**. Question type : "que montre IPFIX / comment configurer une cible d'export IPFIX / comment l'utiliser pour diagnostiquer".

### 📌 À retenir
- BGP ne reçoit pas les routes → **vérifier l'ERP en premier**.
- 2 VM même VPC muettes → suspecter une **Security policy FNS**, pas le réseau.
- Gateway VM (VTEP/VPN/BGP) et Network Controller : vérifier **santé + version**.
- **Ne jamais désactiver le Network Controller** avec FVN actif.
- **IPFIX** = analyse de flux pour diagnostiquer routing/perf.

---

## 🛡️ Section 4 : Troubleshoot Flow Network Security

### Séquence de diagnostic d'une policy (à connaître dans l'ordre)
Quand un trafic ne se comporte pas comme prévu :
1. Vérifier les **catégories assignées** à la VM.
2. Vérifier les **règles de la policy** pour cette catégorie.
3. Vérifier la **direction** (inbound vs outbound).
4. Vérifier l'exactitude de la **définition du service** (protocole/port).

L'examen teste **la séquence**, pas juste les étapes isolées.

### Outils
- **Security Policy Hit Logs** : identifier le trafic **allowed vs denied**. Le point de départ de tout troubleshooting FNS.
- **Vérifier l'appartenance** d'une VM à un composant de policy (target group, source, destination).
- **Conflits de priorité** : rappel de l'ordre Quarantine > Shared Services > Isolation > Application. Attention aussi à la priorité intra-tier vs inbound/outbound.

### Service Insertion (feature testée, souvent peu couverte ailleurs)
Redirige des flux **à travers une VM de fonction réseau tierce** (FortiGate, Palo Alto VM-Series, IDS/IPS, capture de paquets) **avant** d'atteindre la destination. Permet d'intégrer tes investissements sécu existants au lieu de les remplacer.

- Dispo **FNS 5.2+**.
- Cas typique : filtrage web, DPI, inspection inline.
- 🔧 **Healthcheck** : FNS ping la NIC inbound et attend de voir le ping ressortir sur la NIC outbound de la Service VM. Utilise le subnet **169.254.100.0/24**. (Détail très "Nutanix-specific", possible en QCM.)
- ⚠️ Cause fréquente de packet loss quand service insertion est en jeu : la Service VM ne laisse pas passer le trafic (virtual wire mal configuré, healthcheck qui échoue).

### Le piège MTU (North/South cassé alors que les routes existent)
⚠️ Scénario classique : **les routes sont présentes mais le trafic North/South ne passe pas → c'est le MTU.**
L'overlay (Geneve) ajoute de l'encapsulation. Si le MTU du virtual switch / réseau physique n'est pas assez grand (jumbo frames), les gros paquets sont droppés. Symptôme trompeur : ping OK (petits paquets) mais transferts qui cassent.

### Logs FNS
- Piper les **FNS Security Hit logs** vers un syslog externe.
- Vérifier l'état de la table **conntrack** via les **NCC healthchecks**.
- Interpréter les **audit logs** FNS.

### 📌 À retenir
- Séquence FNS : **catégorie → règle → direction → service**. Dans cet ordre.
- **Hit Logs** = point de départ (allow/deny).
- **Service Insertion** = redirection vers appliance tierce (5.2+), healthcheck sur 169.254.100.0/24.
- **Routes OK mais N/S cassé = MTU** (jumbo frames pour l'overlay Geneve).
- Conntrack via NCC healthchecks.

---

## 🚀 Section 5 : Déployer et Upgrader un environnement Flow

### Activer FNS
1. Activer la **Microsegmentation** depuis Prism Central.
2. **Créer les catégories** et les associer aux VM.
3. Confirmer que les **versions sont supportées et à jour** avant activation.
4. Identifier les **ressources** nécessaires sur les noeuds et Prism Central.

### Activer FVN
1. Confirmer que le **Network Controller est activé** et à la bonne version.
2. S'assurer que **tous les clusters sont compatibles** avant d'activer FVN.
3. **Régler le MTU** sur le virtual switch (indispensable pour subnet extension et overlay).
4. Confirmer que **Prism Central a les ressources** adéquates.

### MTU et Virtual Switches
- Augmenter le MTU pour permettre la **subnet extension** et les autres features overlay (jumbo frames).
- **Ségréguer les trafics** : East-West vs North-South ; UVM vs Management vs réplication (virtual switches séparés).

### Ordre des upgrades
- Identifier et traiter les **clusters incompatibles**.
- Déterminer si le **Network Controller** peut être mis à jour + ses dépendances.
- Déterminer si la version **FNS** peut être upgradée + ses dépendances.
- Ordre logique : Prism Central → Network Controller → Network Gateways.

### RBAC (deux univers séparés)

**Côté FVN :**
- Reconnaître quels **rôles peuvent/ne peuvent pas créer un VPC**.
- Créer un **rôle custom**.
- Limiter un **Custom-Admin à des VPC spécifiques**.

**Côté FNS :**
- Rôles système : **Flow Admin**, **Flow Policy Author**, **Flow Viewer**.
- Créer une **Authorization policy** FNS.
- Créer un **rôle custom FNS** avec permissions granulaires.
- 💡 Exemple typique : autoriser un user à créer une policy **en Monitor** mais **pas à l'Enforce**.

### 📌 À retenir
- FNS : activer microseg → catégories → versions → ressources.
- FVN : Network Controller activé/à jour → clusters compatibles → **MTU** → ressources PC.
- Upgrade : **PC → Network Controller → Gateways**, en vérifiant compatibilité et dépendances.
- RBAC FVN (qui crée un VPC ?) et RBAC FNS (**Flow Admin / Policy Author / Viewer**) sont deux systèmes distincts.

---

## ⚠️ Les 12 pièges qui rapportent des points

1. **Network Policy (FVN, stateless)** ≠ **Security Policy (FNS, stateful)**.
2. **BGP Gateway = route server**, PAS dans le data path (forwarding sur les AHV).
3. **Subnet dans l'ERP = routable ; hors ERP = privé.** Cause n°1 des routes BGP manquantes.
4. **Floating IP contourne les Isolation policies.**
5. Ordre policies FNS : **Quarantine > Shared Services > Isolation > Application** (first-match).
6. **Quarantine > Isolation** si conflit. Strict = tout bloqué, Forensic = outils SOC OK.
7. **Monitor observe, Enforce bloque.** Un match en Monitor stoppe l'évaluation.
8. **Visualisation < 24h, Hit logs (syslog) > 24h.**
9. **Routes OK mais North/South cassé = MTU** (overlay Geneve, jumbo frames).
10. **Transit VPC** : ses ERP doivent inclure les ERP des VPC réguliers (sinon alerte 802007).
11. **Ne jamais désactiver le Network Controller** avec FVN actif.
12. Service Insertion : **FNS 5.2+**, healthcheck sur **169.254.100.0/24**.

---

## ⏱️ Stratégie pour la dernière ligne droite

**Si tu as 30 min avant l'exam :**
1. Relis les **12 pièges** ci-dessus (5 min). Ce sont des points quasi garantis.
2. Mémorise **l'ordre des policies FNS** et le **workflow Monitor → Enforce** (5 min).
3. Ancre **NAT vs No-NAT** et **le rôle de l'ERP** (5 min).
4. Relis les 3 plans + les gateways (BGP/VPN/VTEP) (5 min).
5. Survole les sections Troubleshooting (séquence FNS, IPFIX, MTU) (10 min).

**Pendant l'exam :**
- Questions à **réponses multiples** : lis bien "select TWO/THREE". Tu perds des points bêtement sinon.
- Sur une question scénario réseau, demande-toi : "est-ce FVN (réseau) ou FNS (sécurité) ?" Ça élimine souvent la moitié des réponses.
- Doute entre deux réponses BGP : rappelle-toi que le gateway **annonce** mais **ne route pas** le trafic.
- Score 3000/6000 requis : tu peux te tromper sur pas mal de questions. Vise la compréhension, pas la perfection.

💡 Tu connais déjà le BGP mieux que le candidat moyen visé par cette certif. Ton point faible sera le **vocabulaire propriétaire** (ERP, catégories, ordre des policies, noms des bridges). C'est exactement ce que cette fiche verrouille.

Bonne chance. 🎯
