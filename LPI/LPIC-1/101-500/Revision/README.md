# 🎯 LPIC-1 Exam 101-500 - Plan de Révision Complet

> **Objectif :** Obtenir la certification LPIC-1 (Exam 101-500) d'ici **fin février 2026**
> **Durée :** 4 semaines intensives (28 janvier - 28 février 2026)
> **Méthodologie éprouvée :** Inspirée de la réussite Linux Essentials (800/800 points) ✅

---

## 📊 Vue d'ensemble de l'examen

### Informations clés
- **Code exam :** 101-500
- **Durée :** 90 minutes
- **Questions :** 60 questions
- **Score minimum :** 500/800
- **Type :** QCM + questions à trous
- **Langue :** Français
- **Format :** En ligne (Pearson VUE)

### Structure de l'examen (4 sujets)

| Sujet | Nom | Poids | % Exam |
|-------|-----|-------|---------|
| **101** | Architecture système | 8 | ~20% |
| **102** | Installation Linux et gestion des paquets | 10 | ~25% |
| **103** | Commandes GNU et Unix | 16 | ~40% |
| **104** | Périphériques, systèmes de fichiers, FHS | 6 | ~15% |
| **TOTAL** | | **40** | **100%** |

---

## 🗂️ Organisation du matériel de révision

```
Revision/
├── README.md (ce fichier)
├── DEMARRAGE-RAPIDE.md
├── Notes/
│   ├── Notes-Revision-Sujet-101.md (Architecture Système)
│   ├── Notes-Revision-Sujet-102.md (Installation Linux)
│   ├── Notes-Revision-Sujet-103.md (Commandes GNU/Unix)
│   └── Notes-Revision-Sujet-104.md (Filesystems & FHS)
├── QCM/
│   ├── QCM-Sujet-101.md (30 questions + explications)
│   ├── QCM-Sujet-102.md (40 questions + explications)
│   ├── QCM-Sujet-103.md (50 questions + explications)
│   ├── QCM-Sujet-104.md (25 questions + explications)
│   └── QCM-Mock-Exam.md (60 questions - simulation complète)
└── Fiches/
    ├── Fiche-Revision-Sujet-101.md
    ├── Fiche-Revision-Sujet-102.md
    ├── Fiche-Revision-Sujet-103.md
    ├── Fiche-Revision-Sujet-104.md
    └── Fiche-Commandes-Essentielles.md (cheatsheet)
```

---

## 📅 Plan de révision sur 4 semaines

### 🔵 Semaine 1 : Sujet 101 + Sujet 102 (28 jan - 3 fév)
**Focus :** Architecture système + Installation Linux

#### Jour 1-2 (28-29 janvier) - Sujet 101 : Architecture Système
- [ ] 📖 Lire [Notes-Revision-Sujet-101.md](Notes/Notes-Revision-Sujet-101.md)
- [ ] 🎥 Suivre cours KodeKloud Sujet 101
- [ ] 🃏 Réviser 100 cartes Anki (Sujet 101)
- [ ] ✅ Compléter [QCM-Sujet-101.md](QCM/QCM-Sujet-101.md) (30 questions)
- [ ] 📝 Créer notes personnelles sur points difficiles
- [ ] 🔬 **LAB :** Manipuler `/proc`, `/sys`, `lspci`, `lsusb`, `lsmod`

#### Jour 3-5 (30 jan - 1 fév) - Sujet 102 : Installation Linux
- [ ] 📖 Lire [Notes-Revision-Sujet-102.md](Notes/Notes-Revision-Sujet-102.md)
- [ ] 🎥 Suivre cours KodeKloud Sujet 102
- [ ] 🃏 Réviser 150 cartes Anki (Sujet 102)
- [ ] ✅ Compléter [QCM-Sujet-102.md](QCM/QCM-Sujet-102.md) (40 questions)
- [ ] 🔬 **LAB :** GRUB config, partitionnement, apt/yum/rpm, LVM, RAID

#### Jour 6-7 (2-3 février) - Consolidation Semaine 1
- [ ] 📚 Relire fiches [Fiche-Revision-Sujet-101.md](Fiches/Fiche-Revision-Sujet-101.md)
- [ ] 📚 Relire fiches [Fiche-Revision-Sujet-102.md](Fiches/Fiche-Revision-Sujet-102.md)
- [ ] 🃏 Réviser TOUTES les cartes Anki Sujet 101+102 (erreurs uniquement)
- [ ] ✅ Refaire les QCM avec erreurs
- [ ] 🔬 **LAB :** Projet intégrateur (installer système complet)

---

### 🟢 Semaine 2 : Sujet 103 Partie 1 (4-10 février)
**Focus :** Commandes GNU/Unix (Shell, texte, redirections)

#### Jour 8-9 (4-5 février) - Shell & Variables
- [ ] 📖 Lire Notes 103.1 et 103.2 (Shell, processus texte)
- [ ] 🎥 Suivre cours KodeKloud 103.1-103.2
- [ ] 🃏 Réviser 80 cartes Anki (103.1-103.2)
- [ ] ✅ QCM 103.1-103.2 (20 questions)
- [ ] 🔬 **LAB :** Pratiquer `grep`, `sed`, `awk`, `cut`, pipes

#### Jour 10-11 (6-7 février) - Gestion fichiers & Redirections
- [ ] 📖 Lire Notes 103.3 et 103.4 (Fichiers, streams, redirections)
- [ ] 🎥 Suivre cours KodeKloud 103.3-103.4
- [ ] 🃏 Réviser 80 cartes Anki (103.3-103.4)
- [ ] ✅ QCM 103.3-103.4 (20 questions)
- [ ] 🔬 **LAB :** `find`, `tar`, `cpio`, redirections complexes

#### Jour 12-14 (8-10 février) - Processus & Regex
- [ ] 📖 Lire Notes 103.5-103.8 (Processus, priorités, regex, vi)
- [ ] 🎥 Suivre cours KodeKloud 103.5-103.8
- [ ] 🃏 Réviser 100 cartes Anki (103.5-103.8)
- [ ] ✅ QCM 103.5-103.8 (30 questions)
- [ ] 🔬 **LAB :** `ps`, `top`, `nice`, `screen`, `tmux`, regex avancées

---

### 🟡 Semaine 3 : Sujet 104 + Révisions globales (11-17 février)
**Focus :** Filesystems + Révisions intensives

#### Jour 15-16 (11-12 février) - Sujet 104 Partie 1
- [ ] 📖 Lire Notes 104.1-104.3 (Partitions, filesystems, montage)
- [ ] 🎥 Suivre cours KodeKloud 104.1-104.3
- [ ] 🃏 Réviser 80 cartes Anki (104.1-104.3)
- [ ] ✅ QCM 104.1-104.3 (20 questions)
- [ ] 🔬 **LAB :** `fdisk`, `mkfs`, `mount`, `/etc/fstab`, UUID

#### Jour 17-18 (13-14 février) - Sujet 104 Partie 2
- [ ] 📖 Lire Notes 104.4-104.7 (Permissions, quotas, liens, FHS)
- [ ] 🎥 Suivre cours KodeKloud 104.4-104.7
- [ ] 🃏 Réviser 70 cartes Anki (104.4-104.7)
- [ ] ✅ QCM 104.4-104.7 (20 questions)
- [ ] 🔬 **LAB :** `chmod`, `chown`, `ln`, `find`, `locate`, FHS

#### Jour 19-21 (15-17 février) - Révisions Globales
- [ ] 📚 Relire TOUTES les fiches de révision
- [ ] 🃏 Session Anki massive (réviser TOUTES les cartes)
- [ ] ✅ Refaire TOUS les QCM avec erreurs
- [ ] 📝 Identifier les 10 points faibles principaux
- [ ] 🔬 **LAB :** Renforcer les points faibles identifiés

---

### 🔴 Semaine 4 : Entraînement intensif + Mock Exams (18-28 février)
**Focus :** Simulations d'examen + Optimisation du score

#### Jour 22-23 (18-19 février) - Mock Exam 1
- [ ] ⏱️ **MOCK EXAM 1** : [QCM-Mock-Exam.md](QCM/QCM-Mock-Exam.md) (60 questions, 90 min)
- [ ] 📊 Analyser score et erreurs
- [ ] 📝 Créer plan de renforcement personnalisé
- [ ] 🔬 **LAB :** Travailler uniquement sur faiblesses identifiées

#### Jour 24-25 (20-21 février) - Renforcement ciblé
- [ ] 📖 Relire sections problématiques dans notes
- [ ] 🃏 Réviser 200 cartes Anki (zones d'erreurs)
- [ ] ✅ Refaire QCM des sujets avec erreurs
- [ ] 🔬 **LAB :** Pratique intensive des commandes faibles

#### Jour 26 (22 février) - Mock Exam 2
- [ ] ⏱️ **MOCK EXAM 2** : Nouvelle simulation complète (60 questions, 90 min)
- [ ] 📊 Comparer scores Mock 1 vs Mock 2
- [ ] 📝 Ajuster stratégie de révision finale

#### Jour 27-28 (23-24 février) - Optimisation finale
- [ ] 📚 Relire fiches de révision (focus sur commandes)
- [ ] 🃏 Session Anki légère (éviter surcharge)
- [ ] ✅ QCM légers (seulement 20-30 questions)
- [ ] 🔬 **LAB :** Pratiquer commandes les plus courantes

#### Jour 29-30 (25-26 février) - Repos stratégique
- [ ] 📚 Lecture passive des fiches (pas d'étude intensive)
- [ ] 🃏 Anki léger (10-15 min max)
- [ ] 🧘 Repos mental et confiance
- [ ] 🎯 Visualisation de réussite

#### Jour 31 (27 février) - Veille d'examen
- [ ] 📚 Lecture rapide [Fiche-Commandes-Essentielles.md](Fiches/Fiche-Commandes-Essentielles.md)
- [ ] 🧘 Repos complet (pas de révision intensive)
- [ ] ✅ Vérifier matériel exam (ID, connexion internet)
- [ ] 💤 Bonne nuit de sommeil

#### 🎯 Jour 32 (28 février) - JOUR D'EXAMEN
- [ ] ☕ Petit-déjeuner léger
- [ ] 🧘 10 min de méditation/respiration
- [ ] 📋 Relecture ultra-rapide fiche commandes (5 min)
- [ ] 🎯 **PASSER L'EXAMEN LPIC-1 101-500**
- [ ] 🎉 **CÉLÉBRER LA RÉUSSITE !**

---

## 🎯 Objectifs de performance par étape

### Semaine 1 (Sujets 101+102)
- ✅ Minimum 70% de réussite aux QCM
- ✅ Réviser 250+ cartes Anki
- ✅ Compléter 3+ labs pratiques

### Semaine 2 (Sujet 103)
- ✅ Minimum 75% de réussite aux QCM
- ✅ Réviser 260+ cartes Anki
- ✅ Maîtriser regex et processus

### Semaine 3 (Sujet 104 + Révisions)
- ✅ Minimum 80% de réussite aux QCM
- ✅ Réviser TOUTES les cartes Anki (1501)
- ✅ Score > 500/800 sur révisions globales

### Semaine 4 (Mock Exams)
- ✅ Mock Exam 1 : > 550/800
- ✅ Mock Exam 2 : > 650/800
- ✅ **OBJECTIF FINAL : > 700/800**

---

## 📚 Ressources disponibles

### Cartes Anki
- **1501 cartes** réparties sur tous les sujets :
  - 1171 cartes Noji (commandes)
  - 330 cartes traduites de l'allemand (concepts)
- **Import :** Utiliser les fichiers CSV dans `/AnkiCards/`

### Notes de cours
- LPI Learning Material (officiel) ✅
- Notes KodeKloud (extraites) ✅
- Notes personnelles à créer pendant révisions

### Pratique
- KodeKloud Labs (cours actuel)
- Environnement Linux personnel (VM recommandée)
- SadServers (challenges pratiques)

---

## 🛠️ Configuration recommandée

### Environnement de lab
```bash
# Option 1 : VM Linux locale
- VirtualBox/VMware avec Ubuntu 24.04 LTS ou Debian 12
- 2 GB RAM minimum, 20 GB disque
- Snapshots avant chaque lab

# Option 2 : Container Docker
docker run -it --name lpic1-lab ubuntu:24.04 bash

# Option 3 : KodeKloud Labs (inclus dans cours)
```

### Outils essentiels à installer
```bash
sudo apt update && sudo apt install -y \
  vim nano \
  systemd \
  lvm2 mdadm \
  net-tools iproute2 \
  tree htop \
  man-db manpages-dev
```

---

## 📈 Suivi de progression

### Tableau de bord hebdomadaire

| Semaine | Cartes Anki | QCM Score | Labs | Status |
|---------|-------------|-----------|------|--------|
| S1 (101+102) | 250+ | 70%+ | 3+ | ⏳ |
| S2 (103) | 260+ | 75%+ | 4+ | ⏳ |
| S3 (104+Rev) | 1501 | 80%+ | 5+ | ⏳ |
| S4 (Mocks) | 200+ | 85%+ | 2+ | ⏳ |

### Indicateurs de réussite
- ✅ **QCM moyens > 80%** sur tous les sujets
- ✅ **Cartes Anki matures** (intervalle > 7 jours)
- ✅ **Mock Exams > 650/800**
- ✅ **Confiance subjective** : 8/10 minimum

---

## 🎓 Conseils stratégiques

### Pendant les révisions
1. **Pratiquer > Théorie** : 60% pratique, 40% théorie
2. **Espacer les révisions** : Ne pas tout faire en une fois
3. **Labs quotidiens** : Au moins 30 min de pratique/jour
4. **Anki régulier** : 50-100 cartes/jour minimum
5. **Ne pas négliger le sommeil** : 7-8h/nuit

### Pendant l'examen
1. **Gestion du temps** : 90 min = 1,5 min/question
2. **Questions faciles d'abord** : Marquer les difficiles
3. **Élimination** : Éliminer réponses absurdes
4. **Pas de panique** : Respirer, rester calme
5. **Vérifier** : Si temps restant, relire réponses

### Après l'examen
1. **Célébrer** : Peu importe le résultat, vous avez travaillé !
2. **Analyser** : Noter les sujets difficiles pour 102-500
3. **Partager** : Publier sur LinkedIn votre réussite
4. **Continuer** : Préparer 102-500 avec même méthodologie

---

## 🚀 Pour commencer

1. **📖 Lire :** [DEMARRAGE-RAPIDE.md](DEMARRAGE-RAPIDE.md)
2. **🃏 Importer :** Cartes Anki dans votre deck
3. **📝 Commencer :** Semaine 1, Jour 1 - Sujet 101
4. **💪 S'engager :** Dédier 100% du temps disponible

---

## 📞 Support et questions

- **Documentation :** Relire ce README en cas de doute
- **Notes :** Créer fichier `Notes-Personnelles.md` pour vos réflexions
- **Blocage :** Consulter LPI Learning Material ou forums LPI

---

> **« Le succès, c'est d'aller d'échec en échec sans perdre son enthousiasme. »**  
> – Winston Churchill

**Vous avez obtenu 800/800 sur Linux Essentials. Le 101-500 n'est que la prochaine étape !** 🎯

*Bon courage, et surtout... PRATIQUE, PRATIQUE, PRATIQUE !* 🚀
