# 📄 Fiche de Révision Synthétique - Linux Essentials 010-160
## Vue d'ensemble rapide pour révision de dernière minute

---

## ⏰ DATES CLÉS À MÉMORISER

| Année | Événement Important |
|-------|---------------------|
| **1970s** | Unix créé (AT&T Bell Labs) |
| **1985** | FSF fondée par Richard Stallman |
| **1991** | **Linux créé par Linus Torvalds** |
| **1992** | SUSE fondée (Allemagne) |
| **1993** | Debian fondée par Ian Murdock |
| **1994** | Red Hat Linux + SUSE v1 |
| **1998** | OSI (Open Source Initiative) créée |
| **2003** | RHEL renommé + Fedora + Android Inc. |
| **2004** | **Ubuntu (Shuttleworth) + openSUSE** |
| **2005** | Google rachète Android |
| **2007** | GPLv3 publiée |
| **2019** | IBM rachète Red Hat |

---

## 👥 PERSONNES CLÉS

| Personne | Contribution |
|----------|--------------|
| **Linus Torvalds** | Créateur de Linux (1991) |
| **Richard Stallman** | FSF (1985), GPL, mouvement logiciel libre |
| **Ian Murdock** | Fondateur Debian (1993) |
| **Mark Shuttleworth** | Fondateur Ubuntu (2004) |

---

## 🐧 DISTRIBUTIONS LINUX

### Famille Debian
```
┌─ DEBIAN (1993, Ian Murdock)
│  ├─ Gestionnaire: dpkg (bas niveau), APT (haut niveau)
│  ├─ Format: .deb
│  ├─ Philosophie: 100% libre
│  └─ Très stable
│
├─ UBUNTU (2004, Mark Shuttleworth)
│  ├─ Basée sur Debian
│  ├─ Mission: Linux facile pour tous
│  ├─ Release: tous les 6 mois
│  ├─ LTS: tous les 2 ans (avril années paires)
│  └─ Support LTS: 5 ans (ou 10 avec ESM)
│
└─ LINUX MINT
   └─ Basée sur Ubuntu, très conviviale
```

### Famille Red Hat
```
┌─ RED HAT (1994)
│  ├─ RHEL (2003): Entreprise, support payant
│  ├─ Gestionnaire: rpm, YUM (ancien), DNF (nouveau)
│  ├─ Format: .rpm
│  └─ Propriétaire: IBM (depuis 2019)
│
├─ CENTOS
│  ├─ Clone RHEL gratuit
│  └─ Pas de support commercial
│
└─ FEDORA (2003)
   ├─ Desktop, innovante
   ├─ Maintenue par Red Hat
   └─ "Banc d'essai" pour RHEL
```

### Famille SUSE
```
┌─ SUSE (1992, Allemagne)
│  ├─ Outil signature: YaST
│  ├─ Format: .rpm
│  │
│  ├─ SLES: Entreprise commercial
│  └─ openSUSE (2004): Communautaire gratuit
```

### Distributions Spécialisées
- **Kali Linux** : Tests de pénétration, sécurité
- **QubesOS** : Sécurité maximale (isolation)
- **Scientific Linux** : Recherche scientifique
- **Arch Linux** : Rolling release, avancé
- **Raspbian** : Pour Raspberry Pi

---

## 📱 SYSTÈMES EMBARQUÉS

### Android
- Fondation: **2003** (Android Inc., Palo Alto)
- Rachat: **2005** (Google)
- Base: Noyau Linux modifié
- **AOSP**: Android Open Source Project
- Cible: Smartphones, tablettes, TV, montres

### Raspberry Pi
- Ordinateur monocarte éducatif
- **Raspberry Pi Foundation**: Mission éducative
- **Raspbian**: Distribution basée sur Debian
- Usage: Éducation, IoT, prototypage

---

## 📦 GESTION DE PAQUETS

| Famille | Bas Niveau | Haut Niveau | Format |
|---------|------------|-------------|--------|
| **Debian/Ubuntu** | dpkg | APT, apt-get | .deb |
| **Red Hat/Fedora** | rpm | YUM, DNF | .rpm |
| **SUSE** | rpm | YaST, Zypper | .rpm |

**Différence bas/haut niveau :**
- **Bas niveau** (dpkg, rpm) : Installe paquet seul
- **Haut niveau** (APT, YUM) : Gère dépendances automatiquement

---

## 💻 APPLICATIONS LIBRES MAJEURES

### Bureautique
- **LibreOffice** : Suite complète (fork OpenOffice)
  - Writer, Calc, Impress, Draw, Base, Math
- **OpenOffice** : Prédécesseur, moins actif

### Navigateurs & Email
- **Firefox** : Mozilla, open source, vie privée
- **Chromium** : Base de Chrome, Brave, Edge
- **Thunderbird** : Client email Mozilla

### Multimédia
- **GIMP** : Édition images (vs Photoshop)
- **Audacity** : Édition audio
- **VLC** : Lecteur multimédia universel
- **Blender** : 3D/Animation

### Serveurs Web
- **Apache HTTPD** : Historique, modulaire, configurable
- **NGINX** : Moderne, performant, léger, reverse proxy

### Bases de Données
- **MySQL** : Populaire, propriété Oracle
- **MariaDB** : Fork MySQL, 100% compatible, open source
- **PostgreSQL** : Avancé, standards SQL stricts

### Cloud & Partage
- **Nextcloud** / **ownCloud** : Cloud personnel auto-hébergé
- **Samba** : Partage fichiers Windows (SMB/CIFS) sur Linux
- **NFS** : Partage fichiers Unix/Linux standard

### Langages Programmation
- **C** : Système, noyau Linux
- **Python** : Polyvalent, populaire, data science
- **PHP** : Web serveur (WordPress)
- **JavaScript** : Web client/serveur (Node.js)
- **Java** : Multi-plateforme (JVM), entreprise
- **Perl** : Scripts, traitement texte
- **Bash** : Shell scripting

---

## 📜 LICENCES LOGICIELLES

### Philosophies
**Free Software (FSF - 1985)**
- Focus: **Libertés utilisateur** (philosophique)
- 4 Libertés: 0-Exécuter, 1-Étudier, 2-Redistribuer, 3-Distribuer modifié
- "Free" = **Freedom** (liberté), pas gratuit

**Open Source (OSI - 1998)**
- Focus: **Aspects pratiques** (technique)
- 10 critères OSI
- Moins idéologique

**Acronymes**
- **FOSS** : Free and Open Source Software
- **FLOSS** : Free/Libre and Open Source Software

### Types de Licences

#### Copyleft (Restrictives)
**Modifications doivent rester libres**

| Licence | Caractéristiques |
|---------|------------------|
| **GPL** | La plus utilisée, copyleft fort, exemples: Linux, GIMP |
| **GPLv3** | Version actuelle (2007) |
| **LGPL** | Moins stricte, permet liaison code propriétaire |
| **AGPL** | Plus stricte, ferme faille SaaS (services web) |

#### Permissives
**Peu de restrictions, peuvent devenir propriétaires**

| Licence | Caractéristiques |
|---------|------------------|
| **BSD** | Très permissive, variantes: 2-clause, 3-clause |
| **MIT** | Très simple, très populaire |
| **Apache 2.0** | Permissive + protection brevets |

### Creative Commons
- **Usage**: Contenu créatif (PAS logiciel)
- **Composants**:
  - BY : Attribution
  - SA : Share-Alike (copyleft)
  - NC : Non-Commercial
  - ND : No Derivatives
- **Exemples**: CC BY, CC BY-SA, CC BY-NC, CC0 (domaine public)

### Modèles Économiques Open Source
1. **Support/Services** : Red Hat, Canonical
2. **Double Licence** : MySQL (GPL + commerciale)
3. **Open Core** : GitLab (CE gratuit, EE payant)
4. **SaaS** : WordPress.com vs .org
5. **Dons/Crowdfunding** : Fondations
6. **Vente Matériel** : Raspberry Pi

---

## 🖥️ CHOIX SYSTÈME D'EXPLOITATION

### Composants OS
- **Noyau (Kernel)** : Gestion ressources
- **Shell** : Interface utilisateur
- **Utilitaires système**
- **Bibliothèques**

### Linux vs Windows vs macOS

| Aspect | Linux | Windows | macOS |
|--------|-------|---------|-------|
| **Base** | Noyau Linux | NT Kernel | Unix (BSD) |
| **Licence** | Open Source | Propriétaire | Propriétaire |
| **Code** | Accessible | Fermé | Fermé |
| **Coût** | Gratuit | Payant | Inclus matériel |
| **Interface** | CLI + GUI variées | Principalement GUI | GUI (Aqua) |
| **Fichiers** | ext4, btrfs, xfs | NTFS, FAT32 | APFS, HFS+ |
| **Philosophie** | Tout est fichier | Registre + fichiers | Unix-like |
| **Matériel** | Universel | PC x86/ARM | Apple uniquement |
| **Virus** | Peu sensible | Plus vulnérable | Moyennement |
| **Root/Admin** | Séparé (sudo) | Souvent admin | Séparé |

### Cycles de Vie

**Version Stable**
- Testée, fiable
- Pour production
- Ex: Debian Stable, RHEL

**Version Développement**
- Nouvelles fonctionnalités
- Tests, peut être instable
- Ex: Debian Testing, Fedora Rawhide

**LTS (Long Term Support)**
- Support prolongé (5+ ans)
- Stabilité maximale
- Ex: Ubuntu LTS (tous les 2 ans)

**Rolling Release**
- Mises à jour continues
- Pas de versions majeures
- Ex: Arch, openSUSE Tumbleweed

**EOL (End of Life)**
- Fin du support
- Plus de mises à jour

### Choisir une Distribution

| Besoin | Distributions |
|--------|---------------|
| **Débutants** | Ubuntu, Mint, elementary OS |
| **Serveurs** | Ubuntu Server, RHEL, Debian |
| **Développeurs** | Fedora, Ubuntu, Arch |
| **Sécurité** | Kali, Parrot, QubesOS |
| **Ancien matériel** | Lubuntu, Puppy Linux |

### GUI vs CLI

**GUI (Graphical User Interface)**
- Plus facile débutants
- Consomme plus ressources
- Environnements: GNOME, KDE, XFCE

**CLI (Command Line Interface)**
- Plus puissante et flexible
- Moins de ressources
- Essentielle serveurs
- Automatisation facile

---

## 🔑 POINTS ESSENTIELS À RETENIR

### Règle des "Tout"
- **Linux** : Tout est fichier
- **4 Libertés** : 0-3 (Exécuter, Étudier, Redistribuer, Distribuer modifié)
- **Répondre** : Toutes les questions à l'examen (pas de pénalité)

### Mnémotechniques

**GPL vs BSD**
```
GPL = "Give back Please" (Copyleft - rendre à la communauté)
BSD = "Be free, Do anything" (Permissive - faire ce qu'on veut)
```

**Familles Distributions**
```
D-Debian → D-dpkg → D-deb
R-Red Hat → R-RPM → R-rpm
```

**Ubuntu LTS**
```
Années PAIRES + AVRIL
20.04, 22.04, 24.04, 26.04...
```

**4 Libertés (ordre 0-3)**
```
E.É.R.D.
Exécuter - Étudier - Redistribuer - Distribuer modifié
```

### Associations Rapides

**Outils Caractéristiques**
- Debian → APT
- Red Hat → YUM/DNF
- SUSE → **YaST** ⭐

**Forks Célèbres**
- Ubuntu ← Debian
- LibreOffice ← OpenOffice
- MariaDB ← MySQL
- Nextcloud ← ownCloud
- Fedora → RHEL (sens inverse: testbed)

**Projets & Fondateurs**
- Linux → Linus Torvalds
- FSF/GPL → Richard Stallman
- Debian → Ian Murdock
- Ubuntu → Mark Shuttleworth

---

## 📊 INFOS EXAMEN

### Format
- **40 questions** en **60 minutes**
- **Aucune pénalité** pour mauvaise réponse → **Tout répondre !**
- Temps par question : ~1.5 minute
- Passing score: Variable (généralement ~50-60%)

### Sujets Prioritaires (selon vos besoins)
✅ **Sujet 1.1** (valeur 2) : Évolution Linux, distributions
✅ **Sujet 1.2** (valeur 2) : Applications libres
✅ **Sujet 1.3** (valeur 1) : Licences open source
✅ **Sujet 4.1** (valeur 1) : Choix OS

**Total ciblé : 6 points sur ~40**

### Focus Révision
1. **Dates et personnes** (1985, 1991, 1993, 2003, 2004...)
2. **Différences distributions** (Debian vs Red Hat vs SUSE)
3. **Types licences** (GPL vs BSD vs LGPL vs AGPL)
4. **Applications majeures** (LibreOffice, Firefox, Apache, MySQL/MariaDB)
5. **Gestionnaires paquets** (dpkg/APT vs rpm/YUM)
6. **Cycles de vie** (LTS, Rolling, Stable vs Dev)

### Stratégie Examen
1. Lire question **entièrement**
2. Éliminer réponses évidemment fausses
3. Si hésitation, marquer et revenir après
4. Gestion temps: Max 1.5 min/question
5. Vérifier toutes les questions répondues

---

## 🎯 CHECKLIST FINALE

**Avant l'examen, je maîtrise :**
- [ ] Dates clés (1985, 1991, 1993, 2003, 2004, 2019)
- [ ] Personnes (Torvalds, Stallman, Murdock, Shuttleworth)
- [ ] Distributions (Debian, Ubuntu, RHEL, Fedora, SUSE)
- [ ] Gestionnaires paquets (dpkg/APT, rpm/YUM/DNF)
- [ ] 4 Libertés logiciel libre (0-3)
- [ ] Types licences (GPL, LGPL, AGPL, BSD, MIT)
- [ ] Applications (LibreOffice, Firefox, Apache, NGINX, MariaDB)
- [ ] Différences OS (Linux vs Windows vs macOS)
- [ ] Cycles vie (LTS, Rolling, EOL)
- [ ] Systèmes embarqués (Android, Raspberry Pi)

**Score QCM cible : > 85% (34/40)**

---

## ⚡ ULTRA-CONDENSÉ (1 Page)

### DATES
- 1985: FSF (Stallman) | 1991: Linux (Torvalds) | 1993: Debian (Murdock) | 2004: Ubuntu (Shuttleworth) | 2019: IBM→Red Hat

### DISTRIBUTIONS
- **Debian** (.deb, dpkg/APT) → Ubuntu (LTS 2 ans, release 6 mois)
- **Red Hat** (.rpm, rpm/YUM/DNF) → RHEL (IBM), CentOS (gratuit), Fedora (desktop)
- **SUSE** (.rpm, YaST) → SLES (commercial), openSUSE (gratuit)

### LICENCES
- **Copyleft**: GPL (standard), LGPL (liaison OK), AGPL (SaaS)
- **Permissives**: BSD, MIT, Apache
- **4 Libertés**: 0-Exécuter, 1-Étudier, 2-Redistribuer, 3-Distribuer modifié

### APPLICATIONS
- **Bureau**: LibreOffice, Firefox, Thunderbird, GIMP
- **Serveur**: Apache/NGINX, MySQL/MariaDB, Samba, NFS
- **Cloud**: Nextcloud/ownCloud

### OS
- **Linux**: Gratuit, open source, ext4, "tout=fichier", sudo
- **LTS**: Long Term Support (5+ ans)
- **Rolling**: Mises à jour continues (Arch)

### EXAMEN
- 40Q / 60min / Pas pénalité → Tout répondre !

---

**Dernière révision : 26 janvier 2026**

🐧 **Bonne chance pour votre certification Linux Essentials !** 🎉
