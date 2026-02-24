# Notes de Révision - Linux Essentials 010-160
## Objectifs Ciblés pour Mémorisation (Sujets 1.1, 1.2, 1.3 et 4.1)

---

## 📌 Sujet 1.1 : Évolution de Linux et systèmes d'exploitation populaires

### Historique de Linux
- **1991** : Linux créé par **Linus Torvalds**
- **1970s** : Unix développé par **AT&T Labs** (Bell Labs)
- Linux inspiré d'Unix mais code indépendant
- Projet communautaire international (pas une seule entreprise)

### Distributions Majeures - Famille Debian
**Debian GNU/Linux**
- Fondateur : **Ian Murdock (1993)**
- Gestionnaire de paquets : **dpkg**
- Format de paquet : **.deb**
- Philosophie : Logiciel 100% libre
- Des milliers de contributeurs bénévoles
- Très stable et fiable

**Ubuntu**
- Fondateur : **Mark Shuttleworth (2004)**
- Basée sur Debian
- Mission : Linux facile à utiliser pour tous
- Cycle de sortie : **tous les 6 mois**
- **LTS (Long Term Support)** : tous les **2 ans**
- Versions : Desktop, Server, Cloud

**Linux Mint**
- Basée sur Ubuntu/Debian
- Focus : Environnement de bureau convivial
- Très populaire pour débutants

### Distributions Majeures - Famille Red Hat
**Red Hat Enterprise Linux (RHEL)**
- Première version : **1994** (Red Hat Linux)
- Renommé **RHEL en 2003**
- Propriétaire : **IBM** (rachat en 2019)
- Format de paquet : **.rpm**
- Cible : Environnements d'entreprise
- Support commercial payant

**CentOS**
- Basée sur code source RHEL
- **Gratuite** et **sans support commercial**
- Identique à RHEL techniquement
- Utilise aussi format **.rpm**

**Fedora**
- Fondation : **2003**
- Maintenu par Red Hat
- Cible : **Postes de travail/Desktop**
- Très innovante (banc d'essai pour RHEL)
- Adopte rapidement nouvelles technologies

### Distributions Majeures - Famille SUSE
**SUSE Linux**
- Fondation : **1992 en Allemagne**
- Première version : **1994**
- Outil caractéristique : **YaST** (configuration système)
- Format de paquet : **.rpm**

**SUSE Linux Enterprise Server (SLES)**
- Version commerciale avec support
- Pour environnements d'entreprise

**openSUSE**
- Lancé en **2004**
- Version communautaire gratuite
- Disponible en téléchargement libre

### Distributions Spécialisées
**QubesOS**
- Focus : **Sécurité maximale**
- Environnement de bureau sécurisé par isolation

**Kali Linux**
- Focus : **Tests de pénétration et sécurité**
- Outils d'exploitation de vulnérabilités
- Utilisé par testeurs de sécurité

**Scientific Linux**
- Pour recherche scientifique
- Basée sur RHEL

### Systèmes Embarqués
**Caractéristiques**
- Combinaison matériel + logiciel spécialisé
- Fonction spécifique dans système plus large
- Applications : automobile, médical, militaire, IoT

**Android**
- Développeur : **Google**
- Fondation Android Inc. : **2003** à Palo Alto
- Rachat par Google : **2005**
- Basé sur : Noyau Linux modifié
- Cible principale : Appareils tactiles (smartphones, tablettes)
- Autres versions : TV, montres, consoles
- **AOSP** (Android Open Source Project) : version open source
- Avantages : Interface tactile intuitive, écosystème vaste

**Raspberry Pi / Raspbian**
- **Raspberry Pi** : Ordinateur monocarte bon marché
- **Raspbian** : Distribution Linux pour Raspberry Pi
- Basée sur Debian
- Mission : Enseigner programmation aux jeunes
- **Raspberry Pi Foundation** : Organisation éducative
- Applications : Éducation, prototypage, projets IoT

### Linux dans le Cloud
- **Dominance** : Majorité des serveurs cloud utilisent Linux
- **Raisons** :
  - Gratuit (pas de licence)
  - Stable et performant
  - Sécurisé
  - Flexible et personnalisable
  - Support conteneurs (Docker, Kubernetes)
- **Distributions populaires cloud** :
  - Ubuntu Server
  - Amazon Linux
  - CoreOS / Container Linux
  - Alpine Linux (très légère pour conteneurs)

---

## 📌 Sujet 1.2 : Applications libres majeures

### Gestion de Paquets

**Famille Debian**
- **dpkg** : Gestionnaire de paquets bas niveau
- **APT (Advanced Package Tool)** : Interface haut niveau
- Commandes : `apt-get`, `apt`, `aptitude`
- Format : `.deb`

**Famille Red Hat**
- **RPM (Red Hat Package Manager)** : Gestionnaire bas niveau
- **YUM (Yellowdog Updater Modified)** : Interface haut niveau (anciennes versions)
- **DNF** : Remplace YUM (versions récentes Fedora/RHEL)
- Format : `.rpm`

**Interface Graphique**
- **GNOME Software** : Gestionnaire graphique multi-distribution
- **Synaptic** : Gestionnaire graphique pour APT
- **Discover** : Pour KDE

### Applications de Bureautique
**LibreOffice**
- Suite bureautique complète et gratuite
- Fork d'OpenOffice.org
- Composants :
  - **Writer** : Traitement de texte
  - **Calc** : Tableur
  - **Impress** : Présentations
  - **Draw** : Dessin vectoriel
  - **Base** : Base de données
  - **Math** : Éditeur de formules
- Compatible avec formats Microsoft Office

**OpenOffice.org**
- Prédécesseur de LibreOffice
- Moins actif aujourd'hui
- Même structure que LibreOffice

### Navigateurs Web
**Firefox**
- Développé par **Mozilla Foundation**
- Open source
- Multi-plateforme
- Focus : Vie privée et standards web

**Chromium**
- Version open source de Google Chrome
- Base de nombreux navigateurs (Brave, Edge, Opera)

### Client Email
**Thunderbird**
- Développé par Mozilla
- Client email complet
- Support : POP3, IMAP, calendrier
- Multi-plateformes

### Multimédia
**GIMP (GNU Image Manipulation Program)**
- Éditeur d'images avancé
- Alternative à Adobe Photoshop
- Retouche photo, création graphique

**Audacity**
- Éditeur audio multi-piste
- Enregistrement et édition

**VLC Media Player**
- Lecteur multimédia universel
- Lit presque tous les formats

**Blender**
- Modélisation 3D et animation
- Très professionnel

### Serveurs Web
**Apache HTTPD**
- Serveur web le plus utilisé historiquement
- **Apache Software Foundation**
- Très configurable et modulaire
- Configuration : fichiers texte

**NGINX (prononcé "engine-x")**
- Serveur web moderne et performant
- Meilleur pour contenu statique et reverse proxy
- Plus léger qu'Apache
- Très utilisé aujourd'hui

### Bases de Données
**MySQL**
- Système de gestion de base de données relationnelle
- Très populaire
- Propriétaire : Oracle (depuis rachat Sun Microsystems)

**MariaDB**
- Fork de MySQL (créé après rachat par Oracle)
- 100% compatible MySQL
- Communautaire et open source
- Remplace MySQL dans beaucoup de distributions

**PostgreSQL**
- SGBD relationnel avancé
- Standards SQL stricts
- Très robuste

### Partage de Fichiers et Cloud
**Nextcloud**
- Plateforme de cloud personnel
- Partage fichiers, calendriers, contacts
- Alternative à Google Drive/Dropbox
- Auto-hébergeable

**ownCloud**
- Prédécesseur de Nextcloud
- Mêmes fonctionnalités
- Nextcloud est fork d'ownCloud

**Samba**
- Partage de fichiers et imprimantes
- Compatible avec réseaux Windows (protocole SMB/CIFS)
- Permet intégration Linux dans réseaux Windows

**NFS (Network File System)**
- Partage de fichiers sur réseau
- Standard Unix/Linux
- Client-serveur

### Langages de Programmation Majeurs
**C**
- Langage système par excellence
- Noyau Linux écrit en C
- Bas niveau, rapide

**Java**
- Multi-plateforme (JVM)
- Orienté objet
- Très utilisé en entreprise

**JavaScript**
- Langage web principal
- Côté client et serveur (Node.js)
- Très populaire

**Perl**
- Traitement de texte et scripts système
- "Couteau suisse" de la programmation
- Historiquement important

**Python**
- Syntaxe simple et lisible
- Multi-usage : web, data science, IA, scripts
- Très populaire actuellement

**PHP**
- Développement web côté serveur
- Très utilisé (WordPress, etc.)

**Shell (Bash)**
- Scripts système Linux
- Automatisation
- Bash est le shell par défaut

---

## 📌 Sujet 1.3 : Logiciel à code source ouvert et licences

### Philosophies Fondamentales

**Free Software (Logiciel Libre)**
- Fondateur : **Richard Stallman**
- Organisation : **FSF (Free Software Foundation)**
- Créée : **1985**
- "Free" = **Liberté**, pas gratuit
- **4 Libertés essentielles** :
  1. **Liberté 0** : Exécuter le programme
  2. **Liberté 1** : Étudier et modifier le code source
  3. **Liberté 2** : Redistribuer des copies
  4. **Liberté 3** : Distribuer versions modifiées
- Accès au **code source obligatoire**

**Open Source Software**
- Organisation : **OSI (Open Source Initiative)**
- Créée : **1998**
- Focus : Aspects pratiques et techniques
- Moins idéologique que Free Software
- Même principe : code source accessible
- **10 critères OSI** pour licence open source

**Terminologie**
- **FOSS** : Free and Open Source Software
- **FLOSS** : Free/Libre and Open Source Software
- Usage souvent interchangeable

### Types de Licences

**Licences Copyleft (Restrictives)**
Principe : Modifications doivent rester libres

**GPL (GNU General Public License)**
- Auteur : Richard Stallman / FSF
- Version actuelle : **GPLv3** (2007)
- La plus utilisée dans logiciels libres
- **Copyleft fort** : dérivés doivent être GPL
- Exemples : Linux, GIMP, WordPress

**AGPL (Affero GPL)**
- Basée sur GPL
- **Plus stricte** : s'applique aussi aux services web
- Modifications d'un service en ligne doivent être partagées
- Ferme faille "SaaS" de GPL

**LGPL (Lesser GPL)**
- Version "allégée" de GPL
- Permet **liaison avec code propriétaire**
- Utilisée pour bibliothèques
- Moins restrictive que GPL

**Licences Permissives (Permissive Licenses)**
Principe : Peu de restrictions, peut devenir propriétaire

**BSD (Berkeley Software Distribution)**
- Très permissive
- Permet usage commercial et propriétaire
- Plusieurs variantes :
  - **BSD 2-clause** (Simplified)
  - **BSD 3-clause** (Modified)
  - **BSD 4-clause** (Original - obsolète)
- Exemples : FreeBSD, OpenBSD

**MIT License**
- Très simple et permissive
- Similaire à BSD
- Très populaire (Node.js, React, etc.)

**Apache License**
- Version actuelle : **Apache 2.0**
- Permissive
- Inclut clause de protection brevets
- Utilisée par Apache Software Foundation

### Licences Creative Commons
**Usage** : Contenu créatif (pas logiciel)
- Documents, images, musique, vidéos

**Composants** :
- **BY** : Attribution (crédit à l'auteur)
- **SA** : Share-Alike (copyleft)
- **NC** : Non-Commercial
- **ND** : No Derivatives (pas de modification)

**Exemples** :
- **CC BY** : Attribution seule
- **CC BY-SA** : Attribution + partage identique
- **CC BY-NC** : Attribution + non commercial
- **CC0** : Domaine public (aucun droit réservé)

### Modèles Économiques Open Source

**Support et Services**
- Red Hat / IBM : Support RHEL payant
- Canonical : Support Ubuntu payant
- Formation, consulting, maintenance

**Double Licence (Dual Licensing)**
- Version open source gratuite
- Version commerciale avec fonctionnalités supplémentaires
- Exemple : MySQL (GPL + licence commerciale)

**Open Core**
- Noyau open source
- Fonctionnalités avancées propriétaires/payantes
- Exemple : GitLab (CE vs EE)

**SaaS (Software as a Service)**
- Logiciel open source
- Service hébergé payant
- Exemple : WordPress.com vs WordPress.org

**Dons et Crowdfunding**
- Fondations
- Sponsoring
- Contributions volontaires

**Vente de Matériel**
- Logiciel gratuit, matériel vendu
- Exemple : Raspberry Pi

---

## 📌 Sujet 4.1 : Choix d'un système d'exploitation

### Qu'est-ce qu'un Système d'Exploitation ?

**Définition**
- Interface entre matériel et applications
- Gère ressources système (CPU, mémoire, périphériques)
- Fournit services aux programmes

**Composants Principaux**
- **Noyau (Kernel)** : Cœur du système
- **Shell** : Interface utilisateur
- **Utilitaires système**
- **Bibliothèques**

### Différences Linux vs Autres OS

**Linux vs Windows**
| Aspect | Linux | Windows |
|--------|-------|---------|
| **Licence** | Open Source / Gratuit | Propriétaire / Payant |
| **Code source** | Accessible | Fermé |
| **Interface** | CLI + GUI variées | Principalement GUI |
| **Virus** | Peu sensible | Plus vulnérable |
| **Utilisateur root** | Séparé de l'utilisateur | Admin souvent par défaut |
| **Système fichiers** | ext4, btrfs, xfs | NTFS, FAT32 |
| **Philosophie** | "Tout est fichier" | Registre + fichiers |
| **Coût** | Gratuit | Licence payante |

**Linux vs macOS**
| Aspect | Linux | macOS |
|--------|-------|-------|
| **Base** | Noyau Linux | Unix (BSD) |
| **Licence** | Open Source | Propriétaire |
| **Matériel** | Tout matériel x86/ARM | Seulement Apple |
| **Coût OS** | Gratuit | Inclus avec matériel |
| **Personnalisation** | Très élevée | Limitée |
| **Interface** | Multiple choix | Aqua uniquement |

### Cycle de Vie des Distributions

**Versions Stables (Stable/Production)**
- Testées et fiables
- Peu de changements
- Pour production
- Exemple : Debian Stable, RHEL

**Versions de Développement (Development/Testing)**
- Nouvelles fonctionnalités
- Peut être instable
- Pour testeurs
- Exemple : Debian Testing, Fedora Rawhide

**Versions Bêta**
- Avant version stable
- Tests finaux
- Bugs connus

**Rolling Release**
- Mises à jour continues
- Pas de versions majeures
- Toujours à jour
- Exemple : Arch Linux, openSUSE Tumbleweed

**Versions LTS (Long Term Support)**
- **Support prolongé** (5+ ans généralement)
- Stabilité maximale
- Moins de nouvelles fonctionnalités
- Exemple : Ubuntu LTS, RHEL, Debian

**Cycles de Maintenance**
- **Mises à jour de sécurité** : Patches critiques
- **Mises à jour de maintenance** : Corrections bugs
- **EOL (End of Life)** : Fin du support

### Choisir une Distribution

**Pour Débutants**
- Ubuntu
- Linux Mint
- elementary OS
- Zorin OS

**Pour Serveurs**
- Ubuntu Server
- RHEL / CentOS / Rocky Linux
- Debian

**Pour Développeurs**
- Fedora
- Ubuntu
- Arch Linux

**Pour Sécurité**
- Kali Linux (tests)
- Parrot Security
- QubesOS (isolation)

**Pour Ancien Matériel**
- Lubuntu
- Puppy Linux
- antiX

**Interface Graphique vs Ligne de Commande**
- **GUI (Graphical User Interface)** :
  - Plus facile pour débutants
  - Consomme plus de ressources
  - Environnements : GNOME, KDE, XFCE, etc.
  
- **CLI (Command Line Interface)** :
  - Plus puissante et flexible
  - Moins de ressources
  - Essentielle pour serveurs
  - Automatisation facile

### Configuration d'un Poste de Travail

**Considérations**
- **Usage** : Bureau, serveur, développement
- **Matériel** : RAM, CPU, stockage
- **Support** : Communautaire vs commercial
- **Logiciels** : Disponibilité applications requises
- **Compétences** : Niveau technique utilisateur

**Avantages Linux Desktop**
- Gratuit
- Sécurisé
- Personnalisable
- Pas de virus
- Respecte vie privée
- Performances sur vieux matériel

---

## 📝 Points Clés à Mémoriser

### Dates Importantes
- **1970s** : Création Unix (AT&T)
- **1985** : Fondation FSF par Richard Stallman
- **1991** : Linux créé par Linus Torvalds
- **1992** : Fondation SUSE
- **1993** : Debian fondé par Ian Murdock
- **1994** : Red Hat Linux, SUSE Linux première version
- **1998** : Création OSI (Open Source Initiative)
- **2003** : RHEL renommé, Fedora et Android Inc. fondés
- **2004** : Ubuntu créé, openSUSE lancé
- **2005** : Google rachète Android
- **2007** : GPLv3 publiée
- **2019** : IBM rachète Red Hat

### Figures Importantes
- **Linus Torvalds** : Créateur de Linux
- **Richard Stallman** : FSF, GPL, mouvement logiciel libre
- **Ian Murdock** : Fondateur Debian
- **Mark Shuttleworth** : Fondateur Ubuntu

### Acronymes Essentiels
- **FSF** : Free Software Foundation
- **OSI** : Open Source Initiative
- **GPL** : GNU General Public License
- **LGPL** : Lesser GPL
- **AGPL** : Affero GPL
- **FOSS** : Free and Open Source Software
- **FLOSS** : Free/Libre Open Source Software
- **RHEL** : Red Hat Enterprise Linux
- **SLES** : SUSE Linux Enterprise Server
- **LTS** : Long Term Support
- **EOL** : End of Life
- **AOSP** : Android Open Source Project

### Familles de Distributions
- **Debian** : Debian, Ubuntu, Mint → **dpkg, .deb, APT**
- **Red Hat** : RHEL, CentOS, Fedora → **rpm, .rpm, YUM/DNF**
- **SUSE** : SLES, openSUSE → **rpm, .rpm, YaST**

### Commandes Gestionnaires de Paquets
- **Debian/Ubuntu** : `apt-get`, `apt`, `dpkg`
- **Red Hat/Fedora** : `yum`, `dnf`, `rpm`

---

## 🎯 Astuces Mnémotechniques

**Pour les 4 libertés du logiciel libre** :
0. **Exécuter** - Utiliser comme on veut
1. **Étudier** - Lire le code
2. **Redistribuer** - Partager
3. **Distribuer modifié** - Améliorer et partager

**GPL vs BSD** :
- **GPL** = "Give back to community" (Copyleft)
- **BSD** = "Be free, do whatever" (Permissive)

**Familles distributions** :
- **D**ebian utilise **D**eb et **D**pkg
- **R**ed Hat utilise **R**PM
