# 🎯 LPIC-1 Exam 102-500 - Plan de Révision Complet

> **Objectif :** Obtenir la certification LPIC-1 (Exam 102-500) d'ici **fin mars 2026**
> **Durée :** 4-5 semaines intensives (après réussite du 101-500)
> **Méthodologie éprouvée :** Continuité de la préparation LPIC-1 101-500 ✅

---

## 📊 Vue d'ensemble de l'examen

### Informations clés
- **Code exam :** 102-500
- **Durée :** 90 minutes
- **Questions :** 60 questions
- **Score minimum :** 500/800 (62.5%)
- **Objectif visé :** 700/800 (87.5%)
- **Type :** QCM + questions à trous
- **Langue :** Français
- **Format :** En ligne (Pearson VUE)

### Structure de l'examen (6 sujets)

| Sujet | Nom | Poids | % Exam |
|-------|-----|-------|---------|
| **105** | Shells, scripts et gestion des données | 11 | ~18% |
| **106** | Interfaces utilisateur et bureaux | 4 | ~7% |
| **107** | Tâches administratives | 12 | ~20% |
| **108** | Services système essentiels | 10 | ~17% |
| **109** | Notions réseau de base | 8 | ~13% |
| **110** | Sécurité | 12 | ~25% |
| **TOTAL** | | **57** | **100%** |

---

## 🗂️ Organisation du matériel de révision

```
102-500/Revision/
├── README.md (ce fichier)
├── DEMARRAGE-RAPIDE.md
├── Notes/
│   ├── Notes-Revision-Sujet-105.md (Shells et Scripts)
│   ├── Notes-Revision-Sujet-106.md (Interfaces Utilisateur)
│   ├── Notes-Revision-Sujet-107.md (Tâches Administratives)
│   ├── Notes-Revision-Sujet-108.md (Services Système)
│   ├── Notes-Revision-Sujet-109.md (Notions Réseaux)
│   └── Notes-Revision-Sujet-110.md (Sécurité)
├── QCM/
│   ├── QCM-Sujet-105.md (60 questions + explications)
│   ├── QCM-Sujet-106.md (30 questions + explications)
│   ├── QCM-Sujet-107.md (65 questions + explications)
│   ├── QCM-Sujet-108.md (60 questions + explications)
│   ├── QCM-Sujet-109.md (55 questions + explications)
│   ├── QCM-Sujet-110.md (70 questions + explications)
│   └── QCM-Mock-Exam-102-500.md (60 questions - simulation complète)
└── Fiches/
    ├── Fiche-Revision-Sujet-105.md
    ├── Fiche-Revision-Sujet-106.md
    ├── Fiche-Revision-Sujet-107.md
    ├── Fiche-Revision-Sujet-108.md
    ├── Fiche-Revision-Sujet-109.md
    ├── Fiche-Revision-Sujet-110.md
    └── Fiche-Commandes-Essentielles.md (cheatsheet 102-500)
```

---

## 📅 Plan de révision sur 5 semaines

### 🔵 Semaine 1 : Sujet 105 + Sujet 106 (1-7 mars)
**Focus :** Shells, scripts, SQL + Interfaces graphiques

#### Jour 1-3 (1-3 mars) - Sujet 105 : Shells et Scripts
- [ ] 📖 Lire [Notes-Revision-Sujet-105.md](Notes/Notes-Revision-Sujet-105.md)
- [ ] 🎥 Suivre cours Sujet 105 (KodeKloud/ressources)
- [ ] 🃏 Réviser 120 cartes Anki (Sujet 105)
- [ ] ✅ Compléter [QCM-Sujet-105.md](QCM/QCM-Sujet-105.md) (60 questions)
- [ ] 🔬 **LAB :** 
  - Variables bash (`export`, `$PATH`, `$HOME`)
  - Scripts avec `$@`, `$?`, tests `[ ]`, boucles `for/while`
  - SQL : `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`

#### Jour 4-5 (4-5 mars) - Sujet 106 : Interfaces Utilisateur
- [ ] 📖 Lire [Notes-Revision-Sujet-106.md](Notes/Notes-Revision-Sujet-106.md)
- [ ] 🎥 Suivre cours Sujet 106
- [ ] 🃏 Réviser 70 cartes Anki (Sujet 106)
- [ ] ✅ Compléter [QCM-Sujet-106.md](QCM/QCM-Sujet-106.md) (30 questions)
- [ ] 🔬 **LAB :**
  - `$DISPLAY`, `xhost`, `xrandr`
  - Tester GNOME, KDE, XFCE (VMs)
  - Accessibilité : orca, onboard

#### Jour 6-7 (6-7 mars) - Consolidation Semaine 1
- [ ] 📚 Relire fiches [Fiche-Revision-Sujet-105.md](Fiches/Fiche-Revision-Sujet-105.md)
- [ ] 📚 Relire fiches [Fiche-Revision-Sujet-106.md](Fiches/Fiche-Revision-Sujet-106.md)
- [ ] 🃏 Réviser TOUTES les cartes Anki Sujet 105+106 (erreurs)
- [ ] ✅ Refaire QCM avec erreurs
- [ ] 🔬 **LAB :** Créer scripts bash complexes avec bases de données

---

### 🟢 Semaine 2 : Sujet 107 (8-14 mars)
**Focus :** Tâches administratives (users, cron, locale)

#### Jour 8-10 (8-10 mars) - Gestion utilisateurs
- [ ] 📖 Lire Notes 107.1 (Gestion comptes)
- [ ] 🎥 Suivre cours 107.1
- [ ] 🃏 Réviser 80 cartes Anki (107.1)
- [ ] ✅ QCM 107.1 (25 questions)
- [ ] 🔬 **LAB :**
  - `useradd -m`, `usermod -aG`, `userdel -r`
  - `passwd -l/-u/-e`, `chage -M/-W/-I/-E/-d`
  - `/etc/passwd`, `/etc/shadow`, `/etc/group`
  - `id`, `groups`, `last`, `w`

#### Jour 11-12 (11-12 mars) - Automatisation cron/at
- [ ] 📖 Lire Notes 107.2 (Automatisation)
- [ ] 🎥 Suivre cours 107.2
- [ ] 🃏 Réviser 70 cartes Anki (107.2)
- [ ] ✅ QCM 107.2 (25 questions)
- [ ] 🔬 **LAB :**
  - `crontab -e/-l`, format `min heure jour mois jour_sem`
  - `*/15 * * * *`, `@daily`, `@weekly`, `@reboot`
  - `/etc/cron.d/`, `/etc/cron.daily/`
  - `at now + 2 hours`, `atq`, `atrm`
  - `anacron` pour machines non 24/7

#### Jour 13-14 (13-14 mars) - Localisation
- [ ] 📖 Lire Notes 107.3 (Locale & i18n)
- [ ] 🎥 Suivre cours 107.3
- [ ] 🃏 Réviser 50 cartes Anki (107.3)
- [ ] ✅ QCM 107.3 (15 questions)
- [ ] 🔬 **LAB :**
  - `locale`, `locale -a`, `localectl`
  - `export LANG=fr_FR.UTF-8`
  - `timedatectl set-timezone Europe/Paris`
  - `timedatectl set-ntp true`
  - `iconv -f ISO-8859-1 -t UTF-8`

---

### 🟡 Semaine 3 : Sujet 108 (15-21 mars)
**Focus :** Services système (time, logs, mail)

#### Jour 15-16 (15-16 mars) - Horloge système
- [ ] 📖 Lire Notes 108.1 (Horloge)
- [ ] 🎥 Suivre cours 108.1
- [ ] 🃏 Réviser 60 cartes Anki (108.1)
- [ ] ✅ QCM 108.1 (20 questions)
- [ ] 🔬 **LAB :**
  - `date`, `date +%Y-%m-%d`
  - `hwclock`, `hwclock --hctosys`, `hwclock --systohc`
  - `timedatectl`, `timedatectl set-time`
  - `systemctl status systemd-timesyncd`
  - `ntpq -p`, `chronyc sources`

#### Jour 17-19 (17-19 mars) - Logs système
- [ ] 📖 Lire Notes 108.2 (Logs)
- [ ] 🎥 Suivre cours 108.2
- [ ] 🃏 Réviser 80 cartes Anki (108.2)
- [ ] ✅ QCM 108.2 (30 questions)
- [ ] 🔬 **LAB :**
  - `/etc/rsyslog.conf`, `facility.priority action`
  - Priorities : debug < info < notice < warn < err < crit < alert < emerg
  - `journalctl`, `journalctl -u service`, `journalctl -f`
  - `journalctl -b`, `journalctl -k`, `journalctl -p err`
  - `logger "message"`, `logger -p user.warn`
  - `/etc/logrotate.conf`, `logrotate -f`

#### Jour 20-21 (20-21 mars) - MTA (Mail)
- [ ] 📖 Lire Notes 108.3 (MTA)
- [ ] 🎥 Suivre cours 108.3
- [ ] 🃏 Réviser 60 cartes Anki (108.3)
- [ ] ✅ QCM 108.3 (10 questions)
- [ ] 🔬 **LAB :**
  - `systemctl status postfix`
  - `mailq`, `postqueue -f`, `postsuper -d ALL`
  - `/etc/aliases`, `newaliases`
  - `~/.forward`

---

### 🟠 Semaine 4 : Sujet 109 + Sujet 110 (22-28 mars)
**Focus :** Réseaux + Sécurité (SUJETS CRITIQUES)

#### Jour 22-24 (22-24 mars) - Sujet 109 : Réseaux
- [ ] 📖 Lire [Notes-Revision-Sujet-109.md](Notes/Notes-Revision-Sujet-109.md)
- [ ] 🎥 Suivre cours Sujet 109
- [ ] 🃏 Réviser 110 cartes Anki (Sujet 109)
- [ ] ✅ Compléter [QCM-Sujet-109.md](QCM/QCM-Sujet-109.md) (55 questions)
- [ ] 🔬 **LAB :**
  - IPv4 : classes, CIDR, réseaux privés (10/8, 172.16/12, 192.168/16)
  - IPv6 : `::1`, `fe80::/10`, `fc00::/7`
  - Ports : 22 SSH, 25 SMTP, 53 DNS, 80 HTTP, 443 HTTPS
  - `nmcli con show/up/down`, `nmcli con add`
  - `ip addr`, `ip route`, `ip link`
  - `ping`, `traceroute`, `mtr`, `dig`, `host`, `nslookup`
  - `ss -tulpn`, `nc -zv host 80`
  - `/etc/resolv.conf`, `/etc/hosts`, `/etc/nsswitch.conf`
  - `hostnamectl set-hostname`

#### Jour 25-28 (25-28 mars) - Sujet 110 : Sécurité 🔐
**⚠️ SUJET LE PLUS IMPORTANT (12 points, 25% de l'examen)**

- [ ] 📖 Lire [Notes-Revision-Sujet-110.md](Notes/Notes-Revision-Sujet-110.md)
- [ ] 🎥 Suivre cours Sujet 110
- [ ] 🃏 Réviser 150 cartes Anki (Sujet 110)
- [ ] ✅ Compléter [QCM-Sujet-110.md](QCM/QCM-Sujet-110.md) (70 questions)
- [ ] 🔬 **LAB Sécurité (INTENSIF) :**

**110.1 - Administration sécurité**
  - Permissions : `chmod 4755` (SUID), `chmod 2755` (SGID), `chmod 1777` (sticky)
  - `find / -perm -4000`, `find / -perm /6000`
  - `passwd -l/-u/-e/-S`, `chage -l/-M/-W/-I/-E/-d`
  - `usermod -L/-U/-f/-e`
  - `lsof -i :80`, `fuser -vn tcp 80`, `ss -tulpn`, `nmap -F host`
  - `ulimit -a/-Ha`, `/etc/security/limits.conf`
  - `last`, `who`, `w`, `lastb`
  - `su -` vs `su`, `sudo -u user`, `visudo`
  - `/etc/sudoers` : `user ALL=(ALL) NOPASSWD: /cmd`

**110.2 - Configuration sécurité système**
  - `/etc/passwd` (7 champs), `/etc/shadow` (9 champs)
  - `/etc/nologin`, `usermod -s /sbin/nologin user`
  - `/etc/xinetd.conf`, `/etc/xinetd.d/*`
  - `systemctl start ssh.socket`
  - `systemctl list-units --type service --state active`
  - `systemctl disable service --now`
  - `/etc/hosts.allow`, `/etc/hosts.deny`
  - `ldd /usr/sbin/sshd | grep libwrap`

**110.3 - Chiffrement SSH et GPG** 🔑
  - SSH : `ssh user@host`, `ssh -p 2222 user@host`
  - `ssh-keygen -t ed25519` (RECOMMANDÉ)
  - `ssh-keygen -t rsa -b 4096`
  - Algorithmes : Ed25519 > ECDSA > RSA > DSA (déprécié)
  - `ssh-copy-id user@host`
  - `~/.ssh/authorized_keys`, `~/.ssh/known_hosts`
  - `ssh-keygen -R hostname`
  - `ssh-agent /bin/bash`, `ssh-add`, `ssh-add -l/-D`
  - `/etc/ssh/ssh_host_*_key` (privées 600, publiques 644)
  - `ssh-keygen -l -f key.pub`
  - Tunnels : `ssh -L 8080:dest:80 bastion` (local)
  - `ssh -R 8080:localhost:80 remote` (distant)
  - `ssh -X user@host` (X11 forwarding)
  - GPG : `gpg --gen-key`, `gpg --full-generate-key`
  - `gpg --list-keys`, `gpg --list-secret-keys`
  - `gpg --fingerprint user`
  - `gpg -a --export user > pub.asc`
  - `gpg --import key.asc`
  - `gpg --keyserver keyserver.ubuntu.com --send-keys KEY-ID`
  - `gpg -e -r alice file`, `gpg -d file.gpg`
  - `gpg -s file`, `gpg --verify file.sig`
  - `gpg -a -e -s -r alice file` (encrypt + sign)
  - `gpg --gen-revoke user`

---

### 🔴 Semaine 5 : Entraînement intensif + Mock Exams (29 mars - 4 avril)
**Focus :** Simulations d'examen + Optimisation du score

#### Jour 29-30 (29-30 mars) - Mock Exam 1
- [ ] ⏱️ **MOCK EXAM 1** : [QCM-Mock-Exam-102-500.md](QCM/QCM-Mock-Exam-102-500.md) (60 Q, 90 min)
- [ ] 📊 Analyser score et erreurs par sujet
- [ ] 📝 Créer plan de renforcement personnalisé
- [ ] 🔬 **LAB :** Travailler uniquement sur faiblesses identifiées

#### Jour 31-32 (31 mars - 1 avril) - Renforcement ciblé
- [ ] 📖 Relire sections problématiques dans notes
- [ ] 🃏 Session Anki ciblée (cartes en erreur uniquement)
- [ ] ✅ Refaire QCM des sujets faibles (erreurs)
- [ ] 🔬 **LAB :** Pratiquer intensivement zones faibles

#### Jour 33 (2 avril) - Mock Exam 2
- [ ] ⏱️ **MOCK EXAM 2** : Refaire Mock Exam ou créer variantes
- [ ] 📊 Comparer scores Mock 1 vs Mock 2
- [ ] ✅ Objectif : ≥ 700/800 (52+ bonnes réponses)
- [ ] 📝 Noter les 5 pièges récurrents

#### Jour 34-35 (3-4 avril) - Révision finale
- [ ] 📚 Relire [Fiche-Commandes-Essentielles.md](Fiches/Fiche-Commandes-Essentielles.md)
- [ ] 📚 Relire TOUTES les fiches de révision (survol rapide)
- [ ] 🃏 Dernière session Anki (nouvelles cartes désactivées)
- [ ] ✅ Questions pièges notées lors des mocks
- [ ] 🧘 **Repos mental** : pas de marathon la veille !

---

## 🎯 Stratégies d'examen

### Gestion du temps (90 minutes / 60 questions)
- **1,5 min par question** en moyenne
- **Premier passage (60 min)** : répondre aux questions faciles/moyennes
- **Marquer les difficiles** : les sauter temporairement
- **Deuxième passage (25 min)** : traiter questions difficiles
- **Vérification (5 min)** : relire réponses si temps restant

### Priorisation par poids
1. **Sujet 110 (Sécurité)** : 12 points → ~15 questions → **25% de l'examen** 🔥
2. **Sujet 107 (Admin)** : 12 points → ~12 questions → **20% de l'examen**
3. **Sujet 105 (Shells)** : 11 points → ~11 questions → **18% de l'examen**
4. **Sujet 108 (Services)** : 10 points → ~10 questions → **17% de l'examen**
5. **Sujet 109 (Réseaux)** : 8 points → ~8 questions → **13% de l'examen**
6. **Sujet 106 (UI)** : 4 points → ~4 questions → **7% de l'examen**

### Questions pièges fréquents
❌ `usermod -G` écrase groupes → **utiliser `-aG`**
❌ Oublier masque dans `ip addr add` → **`/24` obligatoire**
❌ `find -perm 4000` (exact) vs **`-perm -4000`** (inclusif)
❌ Confondre `hwclock --hctosys` et **`--systohc`**
❌ Éditer `/etc/sudoers` sans **`visudo`** → JAMAIS !
❌ DSA déprécié → **utiliser Ed25519**
❌ Oublier `-a` pour export GPG → binaire au lieu ASCII

---

## 📚 Ressources complémentaires

### Cartes Anki
- **Total :** 752 cartes traduites en français
- **Répartition :**
  - Sujet 105 : 120 cartes
  - Sujet 106 : 70 cartes
  - Sujet 107 : 120 cartes
  - Sujet 108 : 100 cartes
  - Sujet 109 : 110 cartes
  - Sujet 110 : 132 cartes

### Cours vidéo (optionnels)
- KodeKloud LPIC-1 Course
- Linux Academy
- Udemy : LPIC-1 Exam Prep

### Documentation officielle
- LPI Learning Materials : https://learning.lpi.org/
- Man pages : `man command`
- Info pages : `info command`

---

## ✅ Checklist finale (48h avant l'examen)

### J-2 (Veille de la veille)
- [ ] Mock Exam final : score ≥ 700/800
- [ ] Révision fiches master
- [ ] Session Anki légère (30 min max)
- [ ] Repos mental : arrêter à 18h !

### J-1 (Veille)
- [ ] Relecture rapide Fiche-Commandes-Essentielles.md (30 min)
- [ ] Réviser uniquement les 20 commandes top fréquentes
- [ ] **PAS** de nouveau contenu
- [ ] Coucher tôt, bien dormir

### Jour J (Examen)
- [ ] Petit-déjeuner léger
- [ ] Arriver 15 min en avance (si centre)
- [ ] Vérifier connexion internet stable (si online)
- [ ] Papier brouillon + stylo prêts
- [ ] **Respirer** : vous êtes prêt ! 💪

---

## 🏆 Objectif final

**Score minimum :** 500/800 (38/60 questions correctes)
**Score visé :** 700/800 (52/60 questions correctes)
**Score excellent :** 750+/800 (56+/60 questions correctes)

---

## 📞 Support et questions

Pour toute question sur cette préparation :
- Relire les Notes de révision
- Consulter les QCM avec explications
- Tester sur votre lab Linux
- Réviser les cartes Anki correspondantes

**Vous avez tout le matériel nécessaire pour réussir ! 🚀**

Bon courage ! 💪
