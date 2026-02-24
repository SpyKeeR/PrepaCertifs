# Module 01 : Les réseaux aujourd'hui
**ITN - Introduction to Networks**

---

## 📋 Vue d'ensemble du module

Ce module introduit les concepts fondamentaux des réseaux informatiques modernes et leur impact sur notre vie quotidienne.

**Durée estimée :** 4-5 heures  
**Objectifs :** Comprendre les bases des réseaux, leurs composants et leur importance

---

## 1.1 Les réseaux affectent nos vies

### Impact des réseaux
Les réseaux informatiques ont transformé notre société :
- **Communication** : Email, messagerie instantanée, visioconfér

ence
- **Collaboration** : Partage de documents, travail à distance
- **Mobilité** : Accès aux ressources depuis n'importe où
- **Commerce** : Commerce électronique, transactions bancaires
- **Éducation** : Apprentissage en ligne, cours à distance
- **Divertissement** : Streaming, jeux en ligne, réseaux sociaux

### Types de réseaux dans notre vie
- **Réseaux personnels** : Smartphones, tablettes, ordinateurs personnels
- **Réseaux domestiques** : Wi-Fi, équipements connectés (IoT)
- **Réseaux d'entreprise** : Accès aux ressources professionnelles
- **Internet** : Le réseau global connectant tous les autres réseaux

---

## 1.2 Composants réseau

### Périphériques finaux (End Devices)
Appareils qui sont la source ou la destination des données :
- **Ordinateurs** : PC, laptops, workstations
- **Serveurs** : Hébergement d'applications et de données
- **Smartphones et tablettes**
- **Périphériques réseau** : Imprimantes réseau, caméras IP, téléphones VoIP
- **Appareils IoT** : Capteurs, domotique, wearables

**Rôle** : Génèrent ou consomment du trafic réseau (hôtes/hosts)

### Périphériques intermédiaires
Périphériques qui connectent les hôtes et acheminent les données :
- **Commutateurs (Switches)** : Connexion des périphériques dans un réseau local (LAN)
- **Routeurs (Routers)** : Interconnexion de réseaux différents (LAN vers WAN)
- **Points d'accès sans fil (Wireless Access Points)** : Connexion sans fil des périphériques
- **Pare-feu (Firewalls)** : Sécurité réseau, filtrage du trafic
- **Modems** : Conversion de signaux pour l'accès Internet

**Fonctions principales** :
- Régénération et retransmission des signaux
- Choix du meilleur chemin (routage)
- Classification et direction du trafic
- Sécurisation et filtrage

### Supports réseau (Network Media)
Les câbles ou médias qui transportent les données :

**1. Câbles cuivre**
- Câble Ethernet (paires torsadées)
- Types : UTP (Unshielded Twisted Pair), STP (Shielded Twisted Pair)
- Standards : Cat 5e, Cat 6, Cat 6a
- Distance max : ~100 mètres

**2. Câbles à fibre optique**
- Transmission par impulsions lumineuses
- Types : Monomode (longue distance), multimode (courte distance)
- Avantages : Grande bande passante, immunité aux interférences
- Distance : Plusieurs kilomètres

**3. Sans fil (Wireless)**
- Wi-Fi (802.11)
- Bluetooth
- Transmission par ondes radio
- Sensible aux interférences et obstacles

---

## 1.3 Topologies et représentations du réseau

### Diagrammes réseau
Deux types de représentations :

**1. Diagramme physique**
- Montre l'emplacement physique réel des périphériques
- Indique les salles, bâtiments, emplacements géographiques
- Utile pour la maintenance et le dépannage physique

**2. Diagramme logique**
- Montre les connexions logiques entre périphériques
- Indique les adresses IP, interfaces, protocoles
- Masque les détails physiques
- Utile pour comprendre le flux de données

### Topologies réseau

**Topologies physiques communes :**

**1. Topologie en bus**
- Tous les périphériques sur un câble unique
- Obsolète aujourd'hui

**2. Topologie en étoile**
- Tous les périphériques connectés à un point central (switch)
- Topologie LAN la plus courante
- Avantage : Panne isolée à un périphérique

**3. Topologie en étoile étendue**
- Plusieurs étoiles interconnectées
- Topologie d'entreprise courante

**4. Topologie maillée (Mesh)**
- Chaque périphérique connecté à tous les autres (maillage complet)
- Ou connexions partielles (maillage partiel)
- Redondance élevée
- Utilisée dans les WAN et les réseaux sans fil modernes

---

## 1.4 Types courants de réseaux

### Selon la taille et la portée

**LAN (Local Area Network)**
- Réseau local
- Couvre une zone géographique limitée (bureau, bâtiment, campus)
- Haute vitesse (1 Gbps, 10 Gbps, 100 Gbps)
- Propriété et gestion privées
- Exemples : Réseau d'entreprise, réseau domestique

**WAN (Wide Area Network)**
- Réseau étendu
- Couvre une grande zone géographique (ville, pays, continent)
- Interconnecte plusieurs LAN
- Utilise des fournisseurs de services (ISP, opérateurs télécoms)
- Vitesses variables (souvent plus lentes que LAN)
- Exemple : Internet (le plus grand WAN)

**MAN (Metropolitan Area Network)**
- Réseau métropolitain
- Couvre une ville ou une région
- Entre LAN et WAN en termes de taille

### Autres types de réseaux

**WLAN (Wireless LAN)**
- LAN sans fil utilisant Wi-Fi
- Norme 802.11 (802.11a/b/g/n/ac/ax)
- Mobilité et flexibilité

**PAN (Personal Area Network)**
- Réseau personnel
- Très courte portée (quelques mètres)
- Technologies : Bluetooth, USB, NFC
- Exemples : Connexion casque Bluetooth, montre connectée

**SAN (Storage Area Network)**
- Réseau dédié au stockage
- Accès aux systèmes de stockage centralisés
- Haute performance pour les serveurs

---

## 1.5 Connexions Internet

### Types d'accès Internet résidentiel

**1. DSL (Digital Subscriber Line)**
- Utilise les lignes téléphoniques existantes
- ADSL : Asymétrique (téléchargement > envoi)
- Vitesses : 1-100 Mbps

**2. Câble**
- Utilise le réseau de télévision par câble coaxial
- Partagé dans le quartier (bande passante variable)
- Vitesses : 10-1000 Mbps

**3. Fibre optique (FTTH - Fiber To The Home)**
- Fibre jusqu'au domicile
- Très haute vitesse : 100 Mbps - 10 Gbps
- Faible latence
- Plus cher mais meilleures performances

**4. Sans fil**
- **Cellulaire** : 3G, 4G, 5G
- **Satellite** : Couverture zones reculées, latence élevée
- **WiMAX** : Moins courant

**5. Ligne louée dédiée**
- Pour les entreprises
- Connexion dédiée garantie
- Coût élevé

### Types d'accès Internet entreprise

**1. Ligne louée (Leased Line)**
- Connexion point-à-point dédiée
- Bande passante garantie
- SLA (Service Level Agreement)
- Coûteux

**2. Metro Ethernet**
- Extension du LAN via réseau métropolitain
- Haute vitesse

**3. DSL/Câble professionnel**
- Version business avec SLA

**4. Connexions WAN traditionnelles**
- Frame Relay (obsolète)
- ATM (obsolète)
- MPLS (toujours utilisé)

---

## 1.6 Réseaux fiables

Un réseau fiable doit avoir quatre caractéristiques principales :

### 1. Tolérance aux pannes (Fault Tolerance)
- **Définition** : Capacité du réseau à continuer de fonctionner malgré la panne d'un composant
- **Méthodes** :
  - Redondance des chemins
  - Équipements en double
  - Routage dynamique pour contourner les pannes
- **Technologies** : STP, FHRP, routage redondant

### 2. Évolutivité (Scalability)
- **Définition** : Capacité à s'agrandir pour supporter plus d'utilisateurs et de services
- **Conception modulaire** : Ajout de modules sans refonte complète
- **Standards** : Utilisation de protocoles et équipements standards

### 3. Qualité de service (QoS - Quality of Service)
- **Définition** : Priorisation du trafic selon son importance
- **Nécessité** : Bande passante limitée, types de trafic variés
- **Exemples** :
  - Priorité haute : VoIP, visioconférence (sensible aux délais)
  - Priorité moyenne : Navigation web, email
  - Priorité basse : Téléchargements massifs, backups
- **Métriques** :
  - Bande passante (bandwidth)
  - Délai (latency)
  - Gigue (jitter) - variation du délai
  - Perte de paquets

### 4. Sécurité (Security)
- **Protection contre** :
  - Accès non autorisé
  - Vol de données
  - Attaques malveillantes (DDoS, virus, malware)
- **Mesures de sécurité** :
  - Pare-feu (firewalls)
  - Authentification et autorisation
  - Chiffrement des données
  - VPN pour accès distant
  - IDS/IPS (systèmes de détection/prévention d'intrusion)

---

## 1.7 Tendances des réseaux

### Technologies émergentes

**1. BYOD (Bring Your Own Device)**
- Les employés utilisent leurs appareils personnels au travail
- Défis : Sécurité, compatibilité, support

**2. Collaboration en ligne**
- Outils : Webex, Teams, Zoom, Slack
- Travail à distance et télétravail

**3. Cloud Computing**
- Services hébergés sur Internet
- Types :
  - **SaaS** (Software as a Service) : Gmail, Office 365
  - **PaaS** (Platform as a Service) : Azure, Google App Engine
  - **IaaS** (Infrastructure as a Service) : AWS EC2, Azure VMs
- Avantages : Évolutivité, coût réduit, accessibilité

**4. Vidéo**
- Communication vidéo (visioconférence)
- Surveillance vidéo sur IP
- Consomme beaucoup de bande passante

**5. IoT (Internet of Things)**
- Objets connectés : capteurs, domotique, wearables
- Milliards de périphériques
- Défis : Sécurité, gestion, adressage IP

### Technologies réseau modernes

**1. Powerline Networking**
- Utilisation du réseau électrique pour transmission de données
- Utile pour zones difficiles à câbler

**2. Haut débit sans fil**
- WiMAX, LTE, 5G
- Alternative au câble/DSL

**3. Technologies maison intelligente (Smart Home)**
- Domotique, assistants vocaux, automatisation

---

## 1.8 Sécurité du réseau

### Menaces de sécurité

**1. Virus, vers et chevaux de Troie**
- Code malveillant qui se propage ou exécute des actions nuisibles

**2. Spyware et adware**
- Logiciels espions collectant des informations
- Publicités indésirables

**3. Attaques zero-day**
- Exploitation de vulnérabilités inconnues

**4. Attaques par acteurs de menace**
- Hackers, cybercriminels, hacktivistes
- Attaques ciblées

**5. Attaques par déni de service (DoS/DDoS)**
- Saturation du réseau ou des serveurs
- Empêche les utilisateurs légitimes d'accéder

**6. Interception de données et vol d'identité**
- "Man-in-the-middle"
- Écoute du trafic non chiffré

**7. Vol d'identité**
- Usurpation d'identité en ligne

### Solutions de sécurité

**Pour les particuliers :**
- **Antivirus/Antimalware** : Protection en temps réel
- **Pare-feu logiciel** : Filtrage du trafic entrant/sortant
- **Mises à jour** : Correctifs de sécurité
- **Mots de passe forts** : Complexité, renouvellement
- **VPN** : Chiffrement de la connexion

**Pour les entreprises :**
- **Pare-feu matériel dédié** : Protection périmétrique
- **ACL (Access Control Lists)** : Filtrage du trafic
- **IDS/IPS** : Détection et prévention d'intrusions
- **VPN** : Accès distant sécurisé
- **Politiques de sécurité** : Règles et procédures
- **Formation** : Sensibilisation des utilisateurs

---

## 1.9 Professionnel de l'IT

### Rôles dans le réseau

**1. Administrateur réseau (Network Administrator)**
- Gère les réseaux de taille petite à moyenne
- Configuration, maintenance, dépannage

**2. Ingénieur réseau (Network Engineer)**
- Conçoit et planifie les réseaux
- Expertise technique approfondie

**3. Architecte réseau (Network Architect)**
- Conçoit les infrastructures réseau d'entreprise
- Vision stratégique

**4. Spécialiste sécurité réseau (Network Security Specialist)**
- Protège le réseau contre les menaces
- Analyse les vulnérabilités

**5. Analyste SOC (Security Operations Center)**
- Surveillance 24/7 de la sécurité
- Réponse aux incidents

### Certifications IT

**Certifications réseau Cisco :**
- **CCNA** : Cisco Certified Network Associate (niveau associé)
- **CCNP** : Cisco Certified Network Professional (niveau professionnel)
- **CCIE** : Cisco Certified Internetwork Expert (niveau expert)

**Autres certifications :**
- **CompTIA Network+** : Fondamentaux réseau (vendor-neutral)
- **CompTIA Security+** : Sécurité fondamentale
- **Juniper JNCIA** : Alternative Cisco

---

## 💡 Points clés à retenir

1. **Les réseaux** sont essentiels dans notre vie moderne (communication, collaboration, commerce)
2. **Composants réseau** : Périphériques finaux (hôtes), périphériques intermédiaires (switches, routeurs), supports (cuivre, fibre, sans fil)
3. **Types de réseaux** : LAN (local), WAN (étendu), WLAN (sans fil)
4. **Réseau fiable** : Tolérance aux pannes, évolutivité, QoS, sécurité
5. **Tendances** : BYOD, cloud, vidéo, IoT
6. **Sécurité** : Antivirus, pare-feu, VPN, mises à jour, politiques

---

## 🔗 Commandes et outils

Aucune commande IOS spécifique pour ce module.

**Outils de diagramme réseau :**
- Cisco Packet Tracer
- Draw.io / Diagrams.net
- Microsoft Visio
- Lucidchart

---

## 📝 Exercices pratiques

1. Identifier les composants réseau dans votre environnement (domicile, école, entreprise)
2. Dessiner un diagramme physique et logique de votre réseau domestique
3. Rechercher les types de connexion Internet disponibles dans votre région
4. Installer et configurer un antivirus et un pare-feu sur votre ordinateur

---

**Date de création :** 23 février 2026  
**Dernière mise à jour :** 23 février 2026
