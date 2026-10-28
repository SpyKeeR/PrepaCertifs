# NCA 7.5 — Fiche de révision express

> Objectif : tout ce qui tombe le plus souvent, lisible en 30-40 min. Lis d'abord le **Top 30**, puis les sections où tu hésites, puis enchaîne sur le QCM.

## L'examen en 20 secondes

- 50 questions (choix unique **et** choix multiples), 90 min, score ≥ 3000 sur une échelle 1000-6000.
- Versions testées : **AOS 7.5 · AHV 11.0 · Prism Central pc.7.5**.
- Niveau attendu : reconnaître les produits/outils et leur cas d'usage, naviguer dans Prism (Element et Central), lire des infos dans l'UI, faire des opérations de base.
- Réflexe examen : la réponse « la plus Nutanix » et la plus simple est souvent la bonne. Si une question parle de plusieurs clusters, catégories, Flow, DR, templates, playbooks → c'est **Prism Central**.

## Top 30 des faits à connaître par cœur

1. **CVM** (Controller VM) = une VM par nœud qui exécute AOS et gère le stockage ; le stockage est distribué (DSF / AOS Storage), pas de SAN.
2. **Prism Element** = gère **un** cluster, tourne sur les CVM (VIP du cluster). **Prism Central** = VM(s) dédiée(s), gère **plusieurs** clusters + fonctions avancées (catégories, Flow, DR, templates, NCM, playbooks, rapports, LCM de PC…).
3. Port de Prism (PE et PC) : **9440** (HTTPS). NGT : **2074**. iSCSI Volumes : **3260** via la **Data Services IP**. SSH : 22.
4. **RF2** = 2 copies, tolère **1** panne, cluster **3 nœuds mini**. **RF3** = 3 copies, tolère **2** pannes, **5 nœuds mini**. RF1 = aucune redondance.
5. **FT1** = RF2 données + 3 copies de métadonnées. **FT2** = RF3 + 5 copies de métadonnées. On passe un cluster de RF2 à RF3 (Settings › Redundancy State), jamais l'inverse.
6. **1 nœud** : RF2 entre disques, pas de Witness, pas d'extension possible. **2 nœuds** : Witness VM obligatoire sur un 3e site. **3 nœuds** : minimum standard, RF2 seulement, pas de N+1 pendant une maintenance.
7. **Witness VM** sert à : clusters 2 nœuds, Metro Availability (ESXi), réplication synchrone. Communique en **9440**.
8. **Erasure Coding (EC-X)** : réduit le surcoût de stockage des données **froides** (write-cold). Minimum **4 nœuds en RF2**, **6 nœuds en RF3**. Licence NCI **Pro** mini.
9. **Compression** : inline (délai 0, défaut) ou post-process (délai en minutes). **Dédup** : post-process, idéale VDI/clones complets, mauvaise pour bases de données/données chiffrées.
10. Hiérarchie stockage : **Storage Pool** (tous les disques, 1 par cluster) › **Storage Container** (logique, porte RF/compression/dédup/EC) › **vDisk**. **Volume Group** = disques partagés / iSCSI.
11. **Oplog** (SSD) = tampon d'écriture. **Extent Store** = stockage persistant. **Unified Cache** = cache de lecture (RAM + SSD). **ILM** déplace le froid SSD → HDD. **Data locality** = les données d'une VM restent sur son nœud.
12. Services clés : **Stargate** (I/O), **Cassandra/Medusa** (métadonnées), **Zookeeper/Zeus** (config cluster), **Curator** (tâches de fond MapReduce : scrub, rebuild, ILM, équilibrage), **Acropolis** (gestion AHV/VM), **Genesis** (services), **Cerebro** (réplication/DR), **Prism** (UI/API).
13. **AHV** est basé sur **KVM/QEMU** + **Open vSwitch**. Inclus avec AOS, aucune licence hyperviseur.
14. Hyperviseurs supportés NCI : **AHV, VMware ESXi, Microsoft Hyper-V** (pas Xen, pas Proxmox). Toutes les fonctions ne sont pas disponibles sur tous les hyperviseurs (matrice « Supportability by Hypervisor »).
15. **Bonds AHV** : **active-backup** (défaut, aucune config switch), **balance-slb** (répartition par MAC source, sans LACP), **balance-tcp** (nécessite **LACP** sur le switch, meilleur débit).
16. Sous-réseau **managé** = Nutanix IPAM distribue les IP (pool) ; **non managé** = DHCP externe ou IP statique dans l'invité. Types de réseau : **VLAN** et **Overlay (VPC, Flow Virtual Networking)**.
17. **Catégories** = paires clé:valeur définies dans **PC**, utilisées par Flow, DR, Self-Service, playbooks, rapports, RBAC.
18. **Templates de VM** : Prism Central uniquement, AHV uniquement. **Snapshot** (PE) ↔ **Recovery Point** (PC).
19. Hot-plug AHV : **augmenter** vCPU et mémoire à chaud = OK ; diminuer = VM éteinte. Windows sur AHV = pilotes **VirtIO**.
20. **NGT** apporte : VirtIO, snapshots cohérents applicatifs (**VSS**), **Self-Service Restore**, mobilité de VM, communication VM ↔ cluster (port 2074).
21. **LCM** = inventaire + mises à jour firmware et logiciels (AOS, AHV, NCC, Foundation, PC, Files…). **Dark site** = pas d'internet → bundle sur serveur web local ou **Direct Upload**. Ordre conseillé : **PC d'abord**, puis NCC → Foundation → AOS → AHV → firmware.
22. **NCC** = Nutanix Cluster Check : `ncc health_checks run_all` ou Health › Actions › Run NCC Checks. Résultats **PASS / INFO / WARN / FAIL / ERR**. Fréquence : toutes les 4 h, quotidien ou hebdo.
23. **Logbay** = collecte de logs (Health › Actions › Collect Logs ou `logbay collect`), envoi possible vers le support avec le numéro de cas.
24. **Metric chart** = **une métrique**, plusieurs entités. **Entity chart** = **une entité**, plusieurs métriques. (Page Analysis.)
25. **Pulse** = télémétrie envoyée à Nutanix (Insights) : support proactif, Discoveries, cas automatiques. Activé par défaut, vérifiable dans Settings › Pulse.
26. Sévérités d'alerte : **Critical, Warning, Info**. Types d'impact : Availability, Capacity, Configuration, Performance, System Indicator. Une alerte fournit **Cause + Résolution + KB**.
27. **CPU Ready** = temps pendant lequel une vCPU attend un cœur physique → signe de **sur-allocation CPU** ; > 5 % = problème. **Memory Overcommit** AHV = activable par VM dans PC, pour VMs non critiques.
28. **Licences** : NCI/NCM au **cœur CPU**, NUS au **TiB**. NCI **Starter** (≤ 12 nœuds, RF2), **Pro** (RF3, EC-X, block/rack awareness, multi-site DR), **Ultimate** (Sync/NearSync/Metro, chiffrement + KMS, microsegmentation Flow). NCM Pro = Intelligent Ops ; NCM Ultimate = Self-Service, Cost Governance, Security Central.
29. Licence **seamless** = cluster connecté au portail, application automatique. **Manuelle** = télécharger le **CSF** (Cluster Summary File) depuis Prism → portail (License Manager) → récupérer le **LSF** (License Summary File) → l'uploader dans Prism. **Reclaim/Unlicense** avant de détruire un cluster.
30. Gratuits / sans licence : NCC, LCM, Foundation, Move, X-Ray, Collector, NGT, Witness VM, Community Edition, Prism Element (Starter).

---

## 1. Architecture NCI

**Nutanix Cloud Infrastructure (NCI)** = AOS (stockage distribué) + AHV (hyperviseur) + Prism (gestion) + réseau/sécurité (Flow) + DR.

| Composant | Rôle | À retenir |
|---|---|---|
| CVM | Exécute AOS sur chaque nœud, gère les I/O locaux | Une par nœud, passthrough des disques |
| Stargate | Chemin de données (lectures/écritures) | Port 2009 |
| Cassandra / Medusa | Base de métadonnées distribuée | 3 copies (FT1) ou 5 (FT2) |
| Zookeeper / Zeus | Configuration du cluster | Nombre impair de nœuds ZK |
| Curator | Tâches de fond (scrubbing, rebuild, ILM, équilibrage, dédup post-process) | Style MapReduce |
| Acropolis | Gestion AHV : scheduling (ADS), HA, migration | Un leader élu |
| Genesis | Démarrage/gestion des services sur chaque CVM | `genesis status` |
| Cerebro | Réplication, snapshots, DR | Port 2020 |
| Prism | UI + API (v3/v4) | Port 9440 |

- **Scénarios de déploiement** : cluster standard 3+ nœuds ; 1 nœud (ROBO/edge) ; 2 nœuds + Witness ; hybride (SSD+HDD) ou all-flash/NVMe ; nœuds **storage-only** (tournent toujours sous AHV, pas de VM utilisateur, ajoutables même à un cluster ESXi) ; nœuds **compute-only** (AHV sans CVM, sans stockage local, nécessitent des nœuds HCI) ; **NC2** dans AWS/Azure ; DR multi-sites.
- **AHV** : live migration, VM HA (**Best effort** par défaut, **Guarantee** avec réservation), **ADS** (rééquilibrage automatique selon contention CPU/stockage), affinité VM-hôte et anti-affinité VM-VM, vGPU, UEFI/Secure Boot/vTPM, memory overcommit, templates.
- **Nouveautés 7.5 à connaître de nom** : VM Startup Policies (ordre de démarrage lors d'un HA ou redémarrage), Guest Customization Profiles réutilisables, NTP authentifié, AES (Autonomous Extent Store) par défaut en all-flash, Elastic VM Storage (une VM consomme le stockage d'un autre cluster du même domaine PC), vTPM + KMS externe, **CVM Secure Access** (désactivation du SSH sur CVM/AHV — casse la migration inter-clusters CCLM), NCC exécutable **depuis PC**, installeur AHV pour nœuds compute-only sans Foundation, AHV téléchargé séparément d'AOS.
- Depuis AOS 7.0 : fin du modèle LTS/STS → modèle de release unifié (15 mois de correctifs + 9 mois sécurité).

## 2. Résilience & tolérance de panne

- **Data Resiliency Status** (widget accueil PE) : OK / Critical, indique combien de pannes chaque composant tolère.
- **RF vs FT** : RF = nombre de copies des données ; FT = pannes simultanées tolérées par le cluster (FT1 ↔ RF2, FT2 ↔ RF3). Un container RF3 exige un cluster en redondance 3.
- **Block awareness** : copies réparties entre blocs (châssis) ; automatique si ≥ 3 blocs (RF2). **Rack awareness** : configuration manuelle (Settings › Rack Configuration, on assigne les blocs aux racks) ; ≥ 3 racks en RF2, ≥ 5 en RF3.
- **Rebuild Capacity Reservation** : réserve l'espace nécessaire pour reconstruire après perte d'un nœud (N+1). Activable dans PE › Settings.
- **Panne de disque** : Stargate marque le disque hors ligne, **Hades** lance les diagnostics ; si défaillant, Curator reconstruit les copies automatiquement (self-healing). Remplacer : Hardware › Diagram › disque › **Remove Disk** (attendre la migration des données) → remplacer → **Repartition and Add** si nécessaire.
- **Panne de nœud** : VMs redémarrées ailleurs (HA), données reconstruites sur les nœuds restants. Sur 3 nœuds, les métadonnées ne retrouvent 3 copies qu'au retour du nœud.
- **Recycle Bin** : vDisks supprimés conservés **24 h** par défaut (récupération par nCLI/support), désactivable.

## 3. Stockage

- **Optimisations** (par container) : compression inline/post-process (LZ4, LZ4HC pour le froid), dédup (empreintes SHA-1, post-process, capacité), EC-X (données froides, strip ex. 4/1 en RF2, 4/2 en RF3). Le widget **Data Efficiency / Storage savings** affiche le ratio d'économie.
- **RF1** : une seule copie, pour données temporaires ou apps qui répliquent elles-mêmes ; la panne d'un nœud rend les données indisponibles.
- **Types de stockage** : SSD/NVMe (tier chaud : Oplog, métadonnées, extent store chaud), HDD (tier froid). Hybride vs all-flash. **Volumes** (bloc iSCSI) ; **Files** (SMB/NFS) et **Objects** (S3) sont dans NUS.
- **Volume Group** : créé dans PE (Storage › Table › Volume Group) ou PC ; attaché directement à des VM AHV ou exposé en iSCSI (IQN, CHAP optionnel) via la Data Services IP ; permet les disques partagés (clusters Windows, Oracle RAC).
- **Storage Container** : réservation, **advertised capacity** (quota), whitelist NFS pour ESXi ; impossible de supprimer un container non vide.
- **vDisk placement** : migration **à chaud** d'un vDisk vers un autre container (VM allumée), depuis PE ou PC.
- Alertes d'espace par défaut : **75 %** = warning, **90 %** = critique.

## 4. VMs & réseau AHV

**VM (PE : VM › Create VM ; PC : Compute & Storage › VMs)** : vCPU, cœurs/vCPU, mémoire, disques (bus **SCSI** recommandé, IDE pour CD-ROM), NIC → sous-réseau, boot **Legacy BIOS / UEFI** (Secure Boot et vTPM exigent UEFI), guest customization (**Cloud-init** Linux, **Sysprep** Windows), NGT, catégories (PC), **APC** (Advanced Processor Compatibility : masque les fonctions CPU pour migrer entre générations de CPU différentes, activé par VM dans PC, redémarrage requis), GPU passthrough/vGPU.
Snapshot manuel PE : VM › **Take Snapshot** (crash-consistent sauf VSS via NGT) ; suppression dans l'onglet VM Snapshots. Un snapshot n'est pas une sauvegarde.

**Réseau** :
- **Open vSwitch** sur chaque hôte : bridge **br0** ↔ virtual switch **vs0** (défaut), bond **br0-up**. Le virtual switch se gère dans PE (Settings › Network Configuration › Virtual Switch) ; **multicluster virtual switch** depuis PC.
- Créer un sous-réseau : PE Network Configuration › Subnets ou PC Network & Security › Subnets : nom, VLAN ID (0 = natif), virtual switch, IPAM (pool, DNS, domaine).
- **Network Segmentation** : isole le trafic **backplane** (CVM ↔ CVM, stockage) sur un VLAN/interface dédié (eth2 de la CVM) ; aussi segmentation par service (Volumes, DR).
- **Network Visualizer** (PE › Network) : topologie hôtes / VMs / vSwitch / ports physiques. Prérequis : **LLDP** sur les switchs + **SNMP** (Settings › Network Switch) pour les stats des ports.
- **Traffic mirroring** (SPAN) sur hôtes AHV pour outils d'analyse. **Network Gateways** (Flow VN) : VPN IPsec, VTEP (extension L2), BGP.
- Prérequis réseau : CVM et hôte sur le même VLAN de management, IPMI joignable, IPv6 link-local pour la découverte des nœuds (expand cluster / Foundation).

## 5. Portfolio produits (Objectifs 1.1 – 1.3)

| Produit | En une phrase | Mots-clés |
|---|---|---|
| **NCI** | HCI : AOS + AHV + Prism | Starter/Pro/Ultimate, par cœur |
| **Flow Network Security** | Microsegmentation par catégories | Politiques Application / Isolation / Quarantine / VDI, mode monitor puis apply |
| **Flow Virtual Networking** | SDN : VPC, overlay, gateways | Geneve, NAT, VPN, BGP |
| **Nutanix Disaster Recovery** | Protection Policies + Recovery Plans dans PC | Async ≥ 1 h, NearSync 20 s–15 min, Sync RPO 0 (latence ≤ 5 ms), Availability Zones |
| **MST** (Multicloud Snapshot Technology) | Envoie les recovery points vers un bucket **S3** (AWS) pour DR vers **NC2** | Pas besoin de cluster cible allumé en permanence |
| **NC2** (Cloud Clusters) | NCI sur bare-metal **AWS / Azure** | Lift-and-shift, DR, burst, même Prism |
| **Nutanix Central** | Console SaaS au-dessus de plusieurs Prism Central | Vue globale de la flotte, licences |
| **Konnector** | Service qui enregistre automatiquement les clusters **NKP** dans PC / Nutanix Central | Visibilité VMs/stockage/réseau des clusters K8s |
| **NUS** (Unified Storage) | **Files** (SMB/NFS, FSVM), **Objects** (S3, WORM, versioning), **Volumes** (iSCSI), Data Lens (analytics/ransomware SaaS) | Licence au TiB |
| **NDB** (Database Service, ex-Era) | DBaaS : provisioning, patching, clonage, **Time Machine** | PostgreSQL, MySQL, MariaDB, Oracle, SQL Server, MongoDB, SAP HANA |
| **NCM Intelligent Operations** | Capacity runway, anomaly detection, VM efficiency, **X-Play playbooks**, rapports | Ex-Prism Pro, licence NCM Pro |
| **NCM Self-Service** (ex-Calm) | Blueprints, Marketplace, projets, orchestration multi-cloud | NCM Ultimate |
| **NCM Cost Governance** (ex-Beam) | Coûts cloud public + TCO on-prem, chargeback | NCM Ultimate |
| **NCM Security Central** | Posture de sécurité, conformité, planification de microsegmentation | SaaS |
| **NKP** (Kubernetes Platform, ex-D2iQ) | Clusters Kubernetes entreprise, Day-2 automatisé | **NDK** = Data Services for Kubernetes (sauvegarde/DR/clones d'apps K8s) |
| **Nutanix Enterprise AI** (NAI) | Déployer et sécuriser des **endpoints d'inférence LLM** sur NKP + GPU | NVIDIA NIM, Hugging Face |
| **EUC / VDI** | Plateforme pour Citrix / Omnissa Horizon | Licence NCI VDI par utilisateur |

**Outils (1.3)** :

| Outil | Cas d'usage | Détails qui tombent |
|---|---|---|
| **Move** | Migrer des VMs vers AHV (ESXi, Hyper-V, AWS, Azure, AHV→AHV, AHV→ESXi) et des partages de fichiers | Appliance VM, migration plans, cutover à faible interruption, injecte VirtIO |
| **NGT** | Agent invité | VSS, SSR, VirtIO, mobilité, port 2074, ISO monté depuis Prism |
| **Foundation** | Imager des nœuds bare-metal (hyperviseur + CVM) et créer le cluster | Foundation VM / portable / sur CVM (expand cluster) |
| **Foundation Central** | Imager des nœuds **distants** depuis PC | Nœuds découverts via **DHCP** (options FC IP + API key) |
| **Witness VM** | Arbitre | 2 nœuds, Metro, Sync ; site tiers |
| **Self-Service Restore** | Restauration **fichier** par l'utilisateur dans l'invité | Nécessite NGT, Windows et Linux |
| **X-Ray** | Benchmark / tests de performance et de résilience HCI | Scénarios, déploie des VMs de test, gratuit |
| **Collector** | Inventaire d'un environnement existant pour dimensionner (**Sizer**) | vCenter, Hyper-V, AHV, AWS, Azure ; gratuit |

## 6. Licences (Objectif 2.4)

- **Voir l'état** : PE Settings › Licensing ; PC Licensing. Starter = défaut, gratuit, sans expiration. Alertes avant expiration ; à l'expiration le cluster continue de fonctionner mais n'est plus conforme.
- **License Manager** sur le portail : assigner / réassigner / **reclaim** / unassign, **License Tags** pour organiser (site, département).
- **Seamless** (connecté, souvent via PC) vs **manuel** (CSF → portail → LSF). Reclaim des licences avant destruction d'un cluster.
- **Bon tier selon le besoin** : RF3, EC-X, rack awareness, DR multi-sites → **Pro** ; Sync/NearSync/Metro, chiffrement au repos, Flow Network Security → **Ultimate** (ou add-ons Advanced Replication / Security sur Pro) ; Files/Objects → **NUS** ; capacity runway / playbooks → **NCM Pro** ; Self-Service / coûts → **NCM Ultimate**.

## 7. Configuration du cluster (Objectif 3.1)

- **DNS** : Settings › Name Servers. **NTP** : Settings › NTP Servers (3 sources externes recommandées ; 7.5 supporte NTP authentifié) ; vérif `ncc health_checks system_checks check_ntp` ; le leader Genesis se synchronise et propage aux autres CVM et hôtes.
- **SMTP** : Settings › SMTP Server (hôte, port, none/STARTTLS/SSL, from) → e-mails d'alertes. **SNMP** : Settings › SNMP (v3, transports, traps, MIB Nutanix). **Syslog** : Settings › Syslog Server (modules + niveau de sévérité, TCP/UDP/RELP). **HTTP proxy**. **Pulse**.
- **Cluster VIP** (accès Prism/NFS), **Data Services IP** (iSCSI). Time zone, nom du cluster.
- **Enregistrer PE dans PC** : PE Settings › Prism Central Registration (un PE est lié à **un seul** PC ; désenregistrement par ligne de commande). Un cluster PE peut **héberger** plusieurs instances PC. PC en **scale-out** = 3 VMs pour la HA ; tailles small/large/x-large.
- **Sécurité** : mots de passe par défaut à changer (Prism admin `Nutanix/4u`, CVM nutanix `nutanix/4u`, AHV root `nutanix/4u`), **Cluster Lockdown** (SSH par clé seulement), authentification AD/LDAP + SAML (PC), rôles PE (Viewer, Cluster Admin, User Admin, Backup Admin), RBAC/IAM dans PC, certificats SSL, chiffrement au repos (natif ou KMS externe KMIP), bannière de connexion, **CVM Secure Access** (7.5).
- Accès CVM : SSH `nutanix@<cvm>` ; commandes : `cluster status`, `ncli`, `acli`, `allssh`, `hostssh`, `ncc`, `logbay`.

## 8. Maintenance matérielle (Objectif 3.2)

- **Mode maintenance** : PE Hardware › hôte › **Enter Maintenance Mode** (ou PC Hardware › Hosts › Actions). Les VMs sont **migrées à chaud** ; celles qui ne peuvent pas l'être (GPU passthrough, affinité stricte, agent VMs) sont éteintes ou bloquent l'opération. Ensuite la CVM est arrêtée. Sortie : **Exit Maintenance Mode**, les VMs peuvent revenir.
- **Arrêt complet d'un cluster AHV** : 1) éteindre les VMs utilisateur → 2) `cluster stop` depuis une CVM → 3) arrêter chaque CVM (`cvm_shutdown -P now`) → 4) arrêter les hôtes. Redémarrage : hôtes → CVM → `cluster start` → `cluster status` → VMs.
- **Expand Cluster** (roue crantée › Expand Cluster) : découverte automatique des nœuds (IPv6 link-local) ou ajout manuel ; le nœud est ré-imagé par Foundation si versions différentes ; même hyperviseur (sauf storage-only) ; IP CVM/hôte/IPMI. Types : **HCI**, **storage-only**, **compute-only**.
- **Extension dans un nœud** : ajout de disques dans les slots libres (détection automatique, « Repartition and Add » pour un disque réutilisé) ; mémoire/NIC = arrêt du nœud.
- **OOB / IPMI (BMC : iDRAC, iLO, XCC, IPMI NX)** : console distante, power on/off, capteurs, média virtuel (Foundation), firmware. Identifiants OOB configurés dans Prism pour LCM sur certaines plateformes. IP IPMI via BIOS ou `ipmitool lan set 1 ipaddr …` depuis l'hôte.
- **Power Monitor** : application déployée depuis le **Marketplace** de PC (Admin Center) pour suivre la consommation électrique des clusters via les identifiants OOB (lecture seule).
- **Bare-metal** : nœuds en mode découverte (Foundation), même L2 que la Foundation VM, IPMI configuré ; à distance → Foundation Central + DHCP.

## 9. Maintenance logicielle (Objectif 3.3)

- **Processus** : NCC complet et résolution des FAIL → LCM **Perform Inventory** → pré-checks LCM → sélection → View plan → **Apply** (rolling, un nœud à la fois, sans coupure VM : AOS redémarre les CVM une par une, AHV met les hôtes en maintenance un par un).
- **Connected site** : LCM télécharge depuis Nutanix. **Dark site** : télécharger le **LCM Dark Site Bundle** + bundles AOS/AHV, les héberger sur un serveur web interne (URL dans LCM Settings) ou **Direct Upload** dans LCM.
- **Compatibilité** : vérifier la **Compatibility & Interoperability Matrix** et **Upgrade Paths** sur le portail ; **PC doit être compatible (≥) avec l'AOS** des clusters → upgrader PC en premier ; chaque AOS a ses AHV compatibles (AOS 7.5 ↔ AHV 11.0 ↔ pc.7.5).
- **NGT** : mise à jour en masse depuis PC (VMs › sélection › Actions › Upgrade NGT) ; NGT est aussi mis à jour avec AOS. Prérequis : NGT installé, VM démarrée, connectivité VIP:2074.
- Ancienne méthode PE : Settings › **Upgrade Software** (1-Click) — LCM est la voie recommandée.

## 10. Santé, alertes, performance (Objectifs 4.1 – 4.4)

- **Health** (PE) : entités (hôtes, VMs, disques, CVM…), statuts Healthy / Warning / Critical / Unknown ; Actions : Run NCC Checks, Set NCC Frequency, Collect Logs, Manage Checks (activer/désactiver, seuils).
- **Statut cluster** : `cluster status` (services UP/DOWN par CVM), Home dashboard, Data Resiliency Status.
- **Logs** : Logbay via Prism (plage horaire, composants, téléchargement ou envoi au support) ou `logbay collect --duration=-4h`. Collecte automatique déclenchée par certaines alertes (**Alert Triggered Log Collection**).
- **Pulse** : Settings › Pulse (PE et PC) ; `ncli pulse-config` en CLI ; peut passer par un proxy ou par PC. Bénéfices : Insights, Discoveries, cas automatiques, recommandations de mise à jour.
- **Custom Alert Policies** (PC) : entité + métrique + seuil + durée + sévérité (ex. VM CPU > 90 % pendant 5 min) ; pour des besoins non couverts par les alertes système / SLA métier.
- **Rapports** (PC › Operations › Reports) : rapports prédéfinis ou personnalisés, planifiés, PDF/CSV, e-mail.
- **Events** = informatifs (audit d'actions) ; **Alerts** = nécessitent une attention (acknowledge / resolve).
- **Performance** : **CPU contention** et **CPU ready** (trop de vCPU par cœur physique → réduire les vCPU, déplacer la VM, ajouter des nœuds) ; **mémoire** (ballooning/swap si overcommit) ; **latence I/O** (les pics de latence à faible IOPS sont souvent un artefact statistique de la moyenne ; regarder IOPS + latence ensemble, chercher un « bully VM », un disque défaillant, l'Oplog saturé). **Behavioral learning** (NCM Intelligent Ops) : bandes d'anomalie, **Capacity Runway**, VM **overprovisioned / inactive / constrained / bully**.

## 11. Support (Objectif 4.3)

- **Créer un cas** : portail Support & Insights (portal.nutanix.com) › Create Case : asset/cluster (serial, cluster ID), versions AOS/AHV/PC, description, priorité **P1 (critique, prod arrêtée) à P4 (faible/question)**, joindre le bundle **Logbay** + sortie **NCC** + alertes/captures. Délais selon contrat (Basic / Production / Mission Critical). Support téléphonique possible pour les P1.
- **Types de documentation** : guides produits (Prism, AHV Admin, Security), **KB** (Knowledge Base), **Release Notes**, **Field/Security Advisories**, **Compatibility & Interoperability Matrix**, **Upgrade Paths**, **EOL/EOS bulletins**, Best Practices, Tech Notes, Reference Architectures, Nutanix Bible.
- **Insights** : plateforme alimentée par Pulse — santé prédictive, Discoveries (bugs connus, EOL, advisories qui vous concernent), recommandations d'upgrade, création automatique de cas (pannes matérielles), Cloud Health Insights pour les environnements cloud/NC2.

## 12. Pièges classiques

- PE vs PC : catégories, templates, Flow, DR (policies/plans), playbooks, rapports, multicluster vSwitch, custom alert policies → **PC**. Health/NCC, Hardware diagram, LCM cluster, Upgrade Software, Network visualizer → **PE** (mais NCC est aussi dans PC depuis 7.5).
- RF (copies) ≠ FT (pannes tolérées). RF3 = 5 nœuds. EC-X = 4 nœuds (RF2). Rack awareness = 3 racks.
- Storage-only node = **toujours AHV**, même dans un cluster ESXi.
- balance-tcp = LACP obligatoire ; active-backup = défaut.
- Un cluster 1 nœud ne s'étend pas ; un cluster 2 nœuds peut passer à 3 (le Witness devient inutile).
- Move ≠ Foundation ≠ Collector : migrer des VMs / imager des nœuds / inventorier pour dimensionner.
- SSR ≠ snapshot VM : SSR = restauration de fichiers dans l'invité via NGT.
- Seamless licensing exige la connectivité ; manuelle = CSF/LSF. Reclaim avant destruction.
- Snapshots locaux = pas une sauvegarde. Recycle Bin = 24 h.
- Metric chart = 1 métrique / N entités ; Entity chart = 1 entité / N métriques.
- PC se met à jour **avant** les clusters ; NCC en premier dans l'ordre LCM.
- Konnector concerne **Kubernetes (NKP)**, pas le réseau. Nutanix Central ≠ Prism Central (SaaS multi-PC vs VM multi-clusters).
