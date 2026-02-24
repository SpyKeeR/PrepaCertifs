# QCM - Sujet 106 : Interfaces utilisateur et bureaux

**LPIC-1 Examen 102-500**

---

## Instructions

- Ce QCM contient **40 questions** réparties sur les 3 objectifs du Sujet 106
- Chaque question peut avoir **une ou plusieurs bonnes réponses**
- Les réponses et explications détaillées sont fournies à la fin de chaque section
- Prenez le temps de lire les explications pour comprendre vos erreurs

**Répartition :**
- 106.1 : Installation et configuration de X11 (20 questions)
- 106.2 : Bureaux graphiques (13 questions)
- 106.3 : Accessibilité (7 questions)

---

## 106.1 - Installation et configuration de X11

### Question 1
Dans l'architecture X Window, où se trouve le serveur X ?

- [ ] A. Sur la machine qui exécute l'application graphique
- [ ] B. Sur la machine avec l'écran, le clavier et la souris
- [ ] C. Sur un serveur centralisé dans le réseau
- [ ] D. Le serveur X n'existe plus dans les systèmes modernes

### Question 2
Que signifie le nom d'affichage `:0.1` ?

- [ ] A. Machine distante, premier affichage, deuxième écran
- [ ] B. Machine locale, premier affichage, deuxième écran
- [ ] C. Machine locale, deuxième affichage, premier écran
- [ ] D. Machine locale, zéro affichage, un écran

### Question 3
Quelle variable d'environnement contient le nom d'affichage de la session X ?

- [ ] A. `$XDISPLAY`
- [ ] B. `$DISPLAY`
- [ ] C. `$X11_DISPLAY`
- [ ] D. `$SCREEN`

### Question 4
Quel fichier de configuration X a la plus haute priorité ?

- [ ] A. `/etc/X11/xorg.conf`
- [ ] B. `/usr/share/X11/xorg.conf.d/*`
- [ ] C. `/etc/X11/xorg.conf.d/*`
- [ ] D. `~/.xorg.conf`

### Question 5
Sur les distributions modernes, le fichier `/etc/X11/xorg.conf` est-il obligatoire ?

- [ ] A. Oui, X ne peut pas démarrer sans ce fichier
- [ ] B. Non, X se configure automatiquement au démarrage
- [ ] C. Oui, mais seulement pour les cartes NVIDIA
- [ ] D. Non, il a été remplacé par Wayland

### Question 6
Quelle commande génère un fichier de configuration xorg.conf ?

- [ ] A. `xorg-config`
- [ ] B. `X --configure`
- [ ] C. `Xorg -configure`
- [ ] D. `xorgsetup`

### Question 7
Quelle section du fichier xorg.conf permet de configurer la disposition du clavier ?

- [ ] A. `InputDevice`
- [ ] B. `InputClass`
- [ ] C. `Keyboard`
- [ ] D. `ServerLayout`

### Question 8
Quel fichier contient typiquement la configuration du clavier sur les systèmes modernes ?

- [ ] A. `/etc/X11/xkb.conf`
- [ ] B. `/etc/X11/xorg.conf.d/00-keyboard.conf`
- [ ] C. `/etc/keyboard.conf`
- [ ] D. `~/.keyboard`

### Question 9
Quelle commande permet de changer temporairement la disposition du clavier en français ?

- [ ] A. `setxkbmap -layout fr`
- [ ] B. `xkbmap fr`
- [ ] C. `xorg-keyboard fr`
- [ ] D. `localectl set-layout fr`

### Question 10
Quelle commande crée automatiquement un fichier de configuration clavier permanent ?

- [ ] A. `setxkbmap --permanent`
- [ ] B. `localectl set-x11-keymap`
- [ ] C. `xorg-keyboard --save`
- [ ] D. `update-keyboard`

### Question 11
Quelle commande affiche des informations détaillées sur la session X en cours ?

- [ ] A. `xinfo`
- [ ] B. `xdpyinfo`
- [ ] C. `xorginfo`
- [ ] D. `xinfoquery`

### Question 12
Quel gestionnaire d'affichage est utilisé par défaut avec GNOME ?

- [ ] A. LightDM
- [ ] B. SDDM
- [ ] C. GDM
- [ ] D. XDM

### Question 13
Quelle commande autorise un hôte distant à se connecter au serveur X local ?

- [ ] A. `xhost +192.168.1.10`
- [ ] B. `xaccess 192.168.1.10`
- [ ] C. `xallow 192.168.1.10`
- [ ] D. `xpermit +192.168.1.10`

### Question 14
Quelle méthode de contrôle d'accès X est la plus sécurisée ?

- [ ] A. `xhost`
- [ ] B. `xauth`
- [ ] C. `xaccess`
- [ ] D. Aucun contrôle n'est nécessaire

### Question 15
Où se trouvent les logs du serveur X pour l'affichage :0 ?

- [ ] A. `/var/log/X.0.log`
- [ ] B. `/var/log/Xorg.0.log`
- [ ] C. `~/.xsession-errors`
- [ ] D. `/var/log/xorg/display0.log`

### Question 16
Quelle variable d'environnement indique qu'un système utilise Wayland ?

- [ ] A. `$WAYLAND`
- [ ] B. `$WAYLAND_DISPLAY`
- [ ] C. `$DISPLAY_TYPE`
- [ ] D. `$XDG_SESSION_TYPE`

### Question 17
Quelle est la principale différence architecturale entre X11 et Wayland ?

- [ ] A. Wayland n'a pas de compositeur
- [ ] B. Wayland élimine le serveur X intermédiaire
- [ ] C. X11 est plus léger que Wayland
- [ ] D. Wayland ne supporte pas les applications graphiques

### Question 18
Quel composant permet d'exécuter des applications X11 anciennes sous Wayland ?

- [ ] A. XServer
- [ ] B. XWayland
- [ ] C. WaylandX
- [ ] D. X11-compat

### Question 19
Quelle combinaison de touches permet de basculer vers une console virtuelle ?

- [ ] A. `Alt + F1`
- [ ] B. `Ctrl + Alt + F1`
- [ ] C. `Super + F1`
- [ ] D. `Shift + Alt + F1`

### Question 20
Quelle extension X gère les configurations multi-écrans ?

- [ ] A. `XMultiScreen`
- [ ] B. `XRandR`
- [ ] C. `XINERAMA`
- [ ] D. `XScreens`

---

## 106.2 - Bureaux graphiques

### Question 21
Quelle boîte à outils de widgets utilise GNOME ?

- [ ] A. Qt
- [ ] B. GTK+
- [ ] C. wxWidgets
- [ ] D. FLTK

### Question 22
Quel environnement de bureau est recommandé pour les machines à faibles ressources ?

- [ ] A. KDE Plasma
- [ ] B. GNOME
- [ ] C. Xfce
- [ ] D. Cinnamon

### Question 23
Quel est le gestionnaire de fichiers par défaut de KDE ?

- [ ] A. Nautilus
- [ ] B. Thunar
- [ ] C. Dolphin
- [ ] D. Konqueror

### Question 24
Où sont situés les fichiers .desktop pour les applications système ?

- [ ] A. `/usr/local/applications/`
- [ ] B. `/usr/share/applications/`
- [ ] C. `/etc/applications/`
- [ ] D. `/opt/applications/`

### Question 25
Quel champ dans un fichier .desktop spécifie la commande à exécuter ?

- [ ] A. `Command=`
- [ ] B. `Run=`
- [ ] C. `Exec=`
- [ ] D. `Launch=`

### Question 26
Quel protocole d'accès distant est natif au système X Window ?

- [ ] A. VNC
- [ ] B. RDP
- [ ] C. XDMCP
- [ ] D. Spice

### Question 27
Sur quel port TCP par défaut écoute le premier serveur VNC ?

- [ ] A. 5800
- [ ] B. 5900
- [ ] C. 6000
- [ ] D. 3389

### Question 28
Quel fichier script est exécuté au démarrage d'un serveur VNC ?

- [ ] A. `~/.vncrc`
- [ ] B. `~/.vnc/startup`
- [ ] C. `~/.vnc/xstartup`
- [ ] D. `~/.vncserver`

### Question 29
Quel protocole utilise le port TCP 3389 ?

- [ ] A. VNC
- [ ] B. XDMCP
- [ ] C. RDP
- [ ] D. Spice

### Question 30
Pourquoi VNC doit-il être utilisé avec SSH ou VPN ?

- [ ] A. Pour améliorer les performances
- [ ] B. Car VNC n'est pas chiffré par défaut
- [ ] C. Car VNC ne fonctionne que localement
- [ ] D. Pour réduire la bande passante

### Question 31
Quel protocole est principalement utilisé pour accéder à des bureaux de machines virtuelles ?

- [ ] A. XDMCP
- [ ] B. VNC
- [ ] C. RDP
- [ ] D. Spice

### Question 32
Quelle commande lance l'émulateur de terminal par défaut dans KDE ?

- [ ] A. `terminal`
- [ ] B. `gnome-terminal`
- [ ] C. `konsole`
- [ ] D. `xterm`

### Question 33
Quel raccourci clavier est couramment utilisé pour verrouiller l'écran ?

- [ ] A. `Ctrl + L`
- [ ] B. `Alt + L`
- [ ] C. `Super + L`
- [ ] D. `Ctrl + Alt + L`

---

## 106.3 - Accessibilité

### Question 34
Quelle fonction d'accessibilité permet de taper Ctrl + C en deux étapes ?

- [ ] A. Touches lentes
- [ ] B. Touches rémanentes
- [ ] C. Rebonds de touches
- [ ] D. Navigation au clavier

### Question 35
Quel est le geste d'activation pour les Touches rémanentes ?

- [ ] A. Appuyer 3 fois sur Ctrl
- [ ] B. Appuyer 5 fois sur Majuscule
- [ ] C. Maintenir Majuscule 8 secondes
- [ ] D. Appuyer 5 fois sur Alt

### Question 36
Quelle fonction évite les frappes involontaires en instaurant un délai entre les touches ?

- [ ] A. Touches lentes
- [ ] B. Touches rémanentes
- [ ] C. Rebonds de touches
- [ ] D. Touches filtrées

### Question 37
Quel lecteur d'écran est principalement utilisé sous Linux ?

- [ ] A. JAWS
- [ ] B. NVDA
- [ ] C. Orca
- [ ] D. VoiceOver

### Question 38
Quelle application KDE aide les personnes ayant des difficultés à cliquer ?

- [ ] A. KClick
- [ ] B. KMouseTool
- [ ] C. KAccessibility
- [ ] D. KHelper

### Question 39
Quelle touche du pavé numérique génère un clic gauche en mode Navigation au clavier ?

- [ ] A. 0
- [ ] B. 5
- [ ] C. Enter
- [ ] D. +

### Question 40
Quel type de thème aide les personnes ayant une déficience visuelle ?

- [ ] A. Thème sombre
- [ ] B. Thème coloré
- [ ] C. Thème à fort contraste
- [ ] D. Thème minimaliste

---


---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Réponses et explications - 106.1

### Question 1
**Réponse correcte : B**

**Explication :**
Dans l'architecture X Window, le serveur X se trouve sur la machine qui possède les périphériques physiques d'affichage et d'entrée :
- Écran (moniteur)
- Clavier
- Souris/pavé tactile

Le client X est l'application graphique, qui peut être locale ou distante.

**Architecture :**
```
Client X (Firefox) → Serveur X (Xorg sur machine locale) → Écran physique
```

**💡 Point clé :** C'est contre-intuitif ! Le "serveur" est côté utilisateur, le "client" est l'application.

---


### Question 2
**Réponse correcte : B. Machine locale, premier affichage, deuxième écran**

**Explication :**
Format du nom d'affichage : `hostname:displaynumber.screennumber`

Pour `:0.1` :
- Pas de hostname = machine locale
- `:0` = premier affichage (numérotation commence à 0)
- `.1` = deuxième écran (numérotation commence à 0)

**Autres exemples :**
- `:0` = local, premier affichage, écran unique
- `lab01:0` = machine lab01, premier affichage
- `192.168.1.10:1.0` = IP distante, deuxième affichage, premier écran

**💡 Point clé :** La numérotation commence à 0 pour display et screen.

---


### Question 3
**Réponse correcte : B. `$DISPLAY`**

**Explication :**
La variable `$DISPLAY` contient le nom d'affichage de la session X actuelle :
```bash
echo $DISPLAY
# Affiche: :0 (ou hostname:0)

# Lancer application sur affichage spécifique
DISPLAY=:0.1 firefox &
```

Cette variable indique aux applications graphiques où elles doivent s'afficher.

**💡 Point clé :** Sans `$DISPLAY`, les applications graphiques ne savent pas où s'afficher.

---


### Question 4
**Réponse correcte : C. `/etc/X11/xorg.conf.d/*`**

**Explication :**
Ordre de priorité des fichiers de configuration X :
1. `/etc/X11/xorg.conf.d/*` - Configurations utilisateur (priorité haute)
2. `/etc/X11/xorg.conf` - Configuration principale monolithique
3. `/usr/share/X11/xorg.conf.d/*` - Configurations distribution (priorité basse)

**Avantages de xorg.conf.d/ :**
- Modularité (un fichier par composant)
- Facilite la maintenance
- Mises à jour système n'écrasent pas configuration utilisateur

**💡 Point clé :** Préférer des fichiers dans `xorg.conf.d/` au monolithique `xorg.conf`.

---


### Question 5
**Réponse correcte : B. Non, X se configure automatiquement au démarrage**

**Explication :**
Sur les distributions Linux modernes :
- X détecte automatiquement le matériel au démarrage
- Génère une configuration en mémoire
- Le fichier `xorg.conf` est optionnel
- Utilisé seulement pour configurations spécifiques non détectables

**Cas d'usage de xorg.conf :**
- Multi-GPU complexe
- Configuration clavier spéciale
- Multi-écrans avancé
- Pilotes propriétaires (NVIDIA)

**💡 Point clé :** L'absence de `xorg.conf` est normale sur systèmes modernes.

---


### Question 6
**Réponse correcte : C. `Xorg -configure`**

**Explication :**
Pour générer un fichier de configuration :
```bash
# Méthode 1
sudo Xorg -configure
# Crée: xorg.conf.new dans répertoire actuel

# Si session X déjà active
sudo Xorg :1 -configure

# Déplacer vers /etc/X11/
sudo mv xorg.conf.new /etc/X11/xorg.conf
```

**Alternative :**
```bash
# X est souvent un lien vers Xorg
sudo X -configure
```

**💡 Point clé :** Le fichier est créé dans le répertoire actuel, pas directement dans `/etc/X11/`.

---


### Question 7
**Réponses correctes : A, B**

**Explication :**
Deux sections pour configurer le clavier :

**InputDevice (ancienne méthode) :**
```conf
Section "InputDevice"
    Identifier "Keyboard0"
    Driver "kbd"
    Option "XkbLayout" "fr"
EndSection
```

**InputClass (méthode moderne) :**
```conf
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "fr"
    Option "XkbModel" "pc105"
EndSection
```

**💡 Point clé :** `InputClass` est préférée car elle configure par classe de périphériques, pas par périphérique spécifique.

---


### Question 8
**Réponse correcte : B. `/etc/X11/xorg.conf.d/00-keyboard.conf`**

**Explication :**
Sur les systèmes modernes, la configuration clavier se trouve dans :
- `/etc/X11/xorg.conf.d/00-keyboard.conf` (créé par `localectl`)

**Contenu typique :**
```conf
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "fr"
    Option "XkbModel" "pc105"
EndSection
```

**Préfixe numérique :**
- `00-` assure que ce fichier est lu en premier
- Ordre alphabétique détermine priorité

**💡 Point clé :** Le nom exact peut varier (`10-keyboard.conf`, etc.) selon distribution.

---


### Question 9
**Réponse correcte : A. `setxkbmap -layout fr`**

**Explication :**
`setxkbmap` modifie la disposition du clavier pour la session en cours :
```bash
# Disposition française
setxkbmap -layout fr

# QWERTY américain
setxkbmap -layout us

# Avec modèle spécifique
setxkbmap -model pc105 -layout fr

# Avec variante
setxkbmap -layout fr -variant azerty

# Grec polytonique sur Chromebook
setxkbmap -model chromebook -layout "gr(polytonic)"
```

**Limitation :** Change uniquement la session actuelle, pas permanent.

**💡 Point clé :** Utiliser `localectl` pour changement permanent.

---


### Question 10
**Réponse correcte : B. `localectl set-x11-keymap`**

**Explication :**
`localectl` crée automatiquement le fichier de configuration :
```bash
# Syntaxe de base
localectl set-x11-keymap LAYOUT [MODEL [VARIANT [OPTIONS]]]

# Exemples
localectl set-x11-keymap fr
localectl set-x11-keymap fr pc105
localectl set-x11-keymap fr pc105 azerty
localectl set-x11-keymap fr pc105 azerty compose:ralt

# Sans modifier console
localectl --no-convert set-x11-keymap fr pc105

# Vérifier
localectl status
```

**Fichier créé :** `/etc/X11/xorg.conf.d/00-keyboard.conf`

**💡 Point clé :** `localectl` est la méthode systemd moderne et recommandée.

---


### Question 11
**Réponse correcte : B. `xdpyinfo`**

**Explication :**
`xdpyinfo` affiche des informations complètes sur la session X :
```bash
xdpyinfo

# Filtrer extensions
xdpyinfo | grep -A 30 "number of extensions"

# Filtrer résolution
xdpyinfo | grep dimensions
```

**Informations fournies :**
- Nom de l'affichage
- Version X.Org
- Extensions disponibles
- Nombre d'écrans
- Résolution et DPI
- Profondeur de couleur

**💡 Point clé :** Outil de diagnostic essentiel pour problèmes X.

---


### Question 12
**Réponse correcte : C. GDM**

**Explication :**
Gestionnaires d'affichage par environnement :
- **GDM** (GNOME Display Manager) → GNOME
- **SDDM** (Simple Desktop Display Manager) → KDE
- **LightDM** → Xfce, MATE, multi-environnements
- **XDM** → Basique X Window
- **LXDM** → LXDE

**Gestion systemd :**
```bash
systemctl status display-manager
systemctl enable gdm
systemctl start gdm
```

**💡 Point clé :** Le gestionnaire d'affichage fournit l'écran de connexion graphique.

---


### Question 13
**Réponse correcte : A. `xhost +192.168.1.10`**

**Explication :**
`xhost` contrôle quels hôtes peuvent se connecter au serveur X :
```bash
# Autoriser un hôte spécifique
xhost +192.168.1.10

# Autoriser TOUS les hôtes (DANGEREUX)
xhost +

# Révoquer un hôte
xhost -192.168.1.10

# Révoquer tous
xhost -

# Lister hôtes autorisés
xhost
```

**⚠️ Sécurité :** `xhost` est basé sur IP, peu sécurisé. Préférer `xauth`.

**💡 Point clé :** Ne jamais utiliser `xhost +` en production !

---


### Question 14
**Réponse correcte : B. `xauth`**

**Explication :**
`xauth` utilise des cookies d'authentification (plus sécurisé que `xhost`) :
```bash
# Sur machine locale
xauth extract cookie.txt $DISPLAY
scp cookie.txt user@remote:~/

# Sur machine distante
xauth merge ~/cookie.txt

# Vérifier cookies
xauth list

# Générer nouveau cookie
xauth generate $DISPLAY .

# Supprimer cookie
xauth remove $DISPLAY
```

**Avantage :** Authentification par cookie, pas juste par IP.

**💡 Point clé :** `xauth` est la méthode recommandée pour accès X distant.

---


### Question 15
**Réponse correcte : B. `/var/log/Xorg.0.log`**

**Explication :**
Fichiers de logs X :
- `/var/log/Xorg.0.log` - Logs serveur X affichage :0
- `/var/log/Xorg.1.log` - Logs serveur X affichage :1
- `~/.xsession-errors` - Logs erreurs session utilisateur

**Utilisation :**
```bash
# Voir logs
less /var/log/Xorg.0.log

# Chercher erreurs
grep EE /var/log/Xorg.0.log

# Chercher warnings
grep WW /var/log/Xorg.0.log

# Logs session utilisateur
tail -f ~/.xsession-errors
```

**💡 Point clé :** `Xorg.X.log` correspond au numéro d'affichage (display number).

---


### Question 16
**Réponses correctes : B, D**

**Explication :**
Deux variables indiquent Wayland :

**WAYLAND_DISPLAY :**
```bash
echo $WAYLAND_DISPLAY
# Affiche: wayland-0 (si Wayland)
# Vide si X11
```

**XDG_SESSION_TYPE :**
```bash
echo $XDG_SESSION_TYPE
# Affiche: wayland ou x11
```

**Distinction :**
- Sous X11 : `$DISPLAY` est défini, `$WAYLAND_DISPLAY` vide
- Sous Wayland : `$WAYLAND_DISPLAY` défini, `$DISPLAY` peut être défini (XWayland)

**💡 Point clé :** `$XDG_SESSION_TYPE` est plus fiable pour distinguer X11/Wayland.

---


### Question 17
**Réponse correcte : B. Wayland élimine le serveur X intermédiaire**

**Explication :**
Différence architecturale fondamentale :

**X11 :**
```
Application → Serveur X → Compositeur → Noyau → GPU
```

**Wayland :**
```
Application → Compositeur Wayland → Noyau → GPU
```

**Avantages Wayland :**
- Moins de couches = meilleure performance
- Sécurité accrue (isolation applications)
- Moins de ressources système
- Code plus simple et moderne

**💡 Point clé :** Wayland fusionne serveur X et compositeur en un seul composant.

---


### Question 18
**Réponse correcte : B. XWayland**

**Explication :**
**XWayland** est un serveur X complet qui s'exécute comme client Wayland :
```
Application X11 → XWayland → Compositeur Wayland
```

**Fonction :**
- Permet d'exécuter applications X11 sous Wayland
- Compatibilité rétroactive
- Transparent pour l'utilisateur

**Vérification :**
```bash
# Vérifier si XWayland est actif
ps aux | grep Xwayland
```

**💡 Point clé :** XWayland assure la transition X11 → Wayland sans casser compatibilité.

---


### Question 19
**Réponse correcte : B. `Ctrl + Alt + F1`**

**Explication :**
Consoles virtuelles (TTY) :
- `Ctrl + Alt + F1` à `F6` : Consoles texte (tty1-tty6)
- `Ctrl + Alt + F7` : Retour à X (ou F1 sur certains systèmes)

**Distribution moderne :**
- Parfois F1 = interface graphique
- F2-F6 = consoles texte

**Utilité :**
- Dépannage si X plante
- Tâches administratives
- Redémarrage services

**💡 Point clé :** Ces raccourcis fonctionnent même si X est planté.

---


### Question 20
**Réponses correctes : B, C**

**Explication :**
Deux extensions pour multi-écrans :

**XRandR (moderne, recommandée) :**
- Rotation, Resize and Reflection
- Configuration dynamique
- `xrandr` pour configuration
```bash
xrandr --output HDMI-1 --mode 1920x1080
xrandr --output DP-1 --right-of HDMI-1
```

**XINERAMA (ancienne) :**
- Multi-écrans classique
- Moins flexible que XRandR
- Toujours supportée

**💡 Point clé :** XRandR a remplacé XINERAMA sur systèmes modernes.

---


---

## Réponses et explications - 106.2

### Question 21
**Réponse correcte : B. GTK+**

**Explication :**
Boîtes à outils par environnement :
- **GNOME** → GTK+
- **KDE** → Qt
- **Xfce** → GTK+
- **LXDE** → GTK+
- **LXQt** → Qt

**GTK+ :**
- GIMP Toolkit
- Langage C
- Bibliothèque open source

**Applications GTK+ :**
- GIMP
- Firefox
- Inkscape

**💡 Point clé :** GTK+ vs Qt est la principale distinction entre environnements de bureau.

---


### Question 22
**Réponse correcte : C. Xfce**

**Explication :**
Environnements par consommation de ressources :

**Légers :**
- **Xfce** - Bon compromis fonctionnalités/ressources
- **LXDE** - Très léger
- **LXQt** - Version Qt de LXDE
- **MATE** - Fork GNOME 2, léger

**Moyens :**
- **Cinnamon**
- **Budgie**

**Lourds :**
- **GNOME** - Riche en fonctionnalités
- **KDE Plasma** - Très personnalisable mais plus lourd

**💡 Point clé :** Xfce = équilibre entre légèreté et fonctionnalités complètes.

---


### Question 23
**Réponse correcte : C. Dolphin**

**Explication :**
Gestionnaires de fichiers par environnement :
- **GNOME** → Nautilus (Files)
- **KDE** → Dolphin
- **Xfce** → Thunar
- **MATE** → Caja
- **Cinnamon** → Nemo

**Dolphin :**
- Riche en fonctionnalités
- Panneaux d'informations
- Prévisualisation fichiers
- Onglets et vues divisées

**💡 Point clé :** Chaque environnement a son gestionnaire de fichiers dédié.

---


### Question 24
**Réponse correcte : B. `/usr/share/applications/`**

**Explication :**
Emplacements des fichiers .desktop :
- `/usr/share/applications/` - Applications système (tous utilisateurs)
- `~/.local/share/applications/` - Applications utilisateur
- `/usr/local/share/applications/` - Applications installées localement

**Ordre de priorité :**
1. `~/.local/share/applications/` (haute)
2. `/usr/local/share/applications/`
3. `/usr/share/applications/` (basse)

**💡 Point clé :** Les fichiers utilisateur dans `~/.local/` écrasent ceux du système.

---


### Question 25
**Réponse correcte : C. `Exec=`**

**Explication :**
Champs importants d'un fichier .desktop :
```ini
[Desktop Entry]
Type=Application
Name=Mon Application
Comment=Description
Exec=/usr/bin/mon-app --option    # Commande à exécuter
Icon=mon-icone
Terminal=false
Categories=Utility;Development;
```

**Champs clés :**
- `Exec=` - Commande à lancer
- `Terminal=` - true/false, lancer dans terminal
- `Icon=` - Icône à afficher
- `Categories=` - Catégorie menu
- `Name=` - Nom affiché

**💡 Point clé :** `Exec=` peut contenir arguments et variables (`%f` pour fichier, etc.).

---


### Question 26
**Réponse correcte : C. XDMCP**

**Explication :**
**XDMCP** (X Display Manager Control Protocol) est le protocole natif de X11 pour sessions distantes.

**Caractéristiques :**
- Port UDP 177
- Intégré au système X Window
- ⚠️ Non chiffré
- Haute bande passante requise

**Limitations :**
- Problèmes de sécurité
- Performance médiocre sur réseaux lents
- Rarement utilisé aujourd'hui

**💡 Point clé :** XDMCP est obsolète, préférer VNC ou Spice avec chiffrement.

---


### Question 27
**Réponse correcte : B. 5900**

**Explication :**
Ports VNC par défaut :
- Premier serveur (`:0` ou `:1`) → TCP 5900
- Deuxième serveur (`:1` ou `:2`) → TCP 5901
- Troisième serveur (`:2` ou `:3`) → TCP 5902
- etc.

**Formule :** Port = 5900 + numéro d'affichage

**Exemple :**
```bash
vncserver :1  # Port 5901
vncserver :5  # Port 5905
```

**Connexion client :**
```bash
vncviewer 192.168.1.10:5901
vncviewer 192.168.1.10:1  # Équivalent
```

**💡 Point clé :** Le numéro après `:` peut être le display ou le port - 5900.

---


### Question 28
**Réponse correcte : C. `~/.vnc/xstartup`**

**Explication :**
Le fichier `~/.vnc/xstartup` est un script shell exécuté au démarrage du serveur VNC.

**Exemple pour Xfce :**
```bash
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec startxfce4
```

**Exemple pour GNOME :**
```bash
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec gnome-session
```

**Exemple pour KDE :**
```bash
#!/bin/sh
exec startkde
```

**💡 Point clé :** Ce fichier détermine quel environnement de bureau VNC lance.

---


### Question 29
**Réponse correcte : C. RDP**

**Explication :**
Ports par protocole :
- **RDP** → TCP 3389
- **VNC** → TCP 5900+
- **Spice** → TCP 5900 (par défaut, configurable)
- **XDMCP** → UDP 177
- **SSH** → TCP 22

**RDP (Remote Desktop Protocol) :**
- Protocole Microsoft
- Natif sur Windows
- Client Linux : Remmina, xfreerdp

**💡 Point clé :** 3389 = RDP, mémorisé par "3389" ≈ "Windows".

---


### Question 30
**Réponse correcte : B. Car VNC n'est pas chiffré par défaut**

**Explication :**
VNC utilise le protocole RFB (Remote Frame Buffer) qui n'est **pas chiffré** nativement.

**Risques :**
- Mot de passe transmis en clair (ou faiblement chiffré)
- Données écran non chiffrées
- Susceptible aux attaques man-in-the-middle

**Solutions :**

**Tunnel SSH (recommandé) :**
```bash
# Sur machine locale
ssh -L 5901:localhost:5901 user@serveur
vncviewer localhost:5901
```

**VPN :**
- Établir VPN entre machines
- Puis VNC via tunnel VPN

**💡 Point clé :** TOUJOURS tunneliser VNC via SSH ou VPN en production.

---


### Question 31
**Réponse correcte : D. Spice**

**Explication :**
**Spice** (Simple Protocol for Independent Computing Environments) est conçu pour la virtualisation.

**Avantages :**
- Optimisé pour KVM/QEMU
- Support audio bidirectionnel
- Partage USB
- Partage presse-papier
- Partage fichiers
- Multi-moniteurs

**Utilisation :**
- oVirt
- Proxmox
- Red Hat Virtualization
- virt-manager

**Client :**
```bash
sudo apt install virt-viewer
remote-viewer spice://192.168.1.10:5900
```

**💡 Point clé :** Spice offre bien plus qu'un simple affichage distant pour VMs.

---


### Question 32
**Réponse correcte : C. `konsole`**

**Explication :**
Émulateurs de terminal par environnement :
- **KDE** → Konsole
- **GNOME** → GNOME Terminal (gnome-terminal)
- **Xfce** → Xfce Terminal
- **MATE** → MATE Terminal
- **Universel** → xterm, urxvt

**Commandes génériques :**
```bash
# Marche souvent
terminal
x-terminal-emulator  # Debian/Ubuntu

# Spécifiques
konsole     # KDE
gnome-terminal  # GNOME
xfce4-terminal  # Xfce
```

**💡 Point clé :** Dans KDE, `konsole` est la commande native, mais `terminal` fonctionne souvent.

---


### Question 33
**Réponse correcte : C. `Super + L`**

**Explication :**
Raccourcis communs de verrouillage :
- **GNOME** → `Super + L`
- **KDE** → `Super + L` ou `Ctrl + Alt + L`
- **Xfce** → `Ctrl + Alt + L`
- **MATE** → `Ctrl + Alt + L`

**Autre raccourci :**
- `Ctrl + Alt + Del` → Déconnexion/Arrêt (selon config)

**Note :** `Super` = Touche Windows

**💡 Point clé :** `Super + L` est le plus universel sur environnements modernes.

---


---

## Réponses et explications - 106.3

### Question 34
**Réponse correcte : B. Touches rémanentes**

**Explication :**
Les **Touches rémanentes** (Sticky Keys) permettent de taper les raccourcis clavier une touche à la fois.

**Cas d'usage :**
- Impossibilité d'appuyer sur plusieurs touches simultanément
- Mobilité réduite des mains
- Utilisation d'une seule main

**Utilisation :**
```
Au lieu de : Ctrl + C (simultané)
Faire :      Ctrl (appuyer/relâcher)
            C (appuyer/relâcher)
```

**Activation :**
- GNOME : Accès universel → Saisie → Touches rémanentes
- Geste : Appuyer 5× sur `Majuscule`

**💡 Point clé :** "Rémanentes" = les touches "restent" actives après relâchement.

---


### Question 35
**Réponse correcte : B. Appuyer 5 fois sur Majuscule**

**Explication :**
Gestes d'activation d'accessibilité :
- **Touches rémanentes** → Appuyer 5× sur `Majuscule`
- **Touches lentes** → Maintenir `Majuscule` 8 secondes

**Activation des gestes :**
- GNOME : Accès universel → Assistance frappe → Activer par le clavier
- KDE : Accessibilité → Utiliser les gestes pour activer...

**Avantage :**
- Activation sans souris
- Utile si difficulté à accéder aux menus

**💡 Point clé :** 5× Maj = Sticky Keys, 8s Maj = Slow Keys (mémo: 5 doigts, 8 bits).

---


### Question 36
**Réponse correcte : C. Rebonds de touches**

**Explication :**
Les **Rebonds de touches** (Bounce Keys) instaurent un délai minimum entre deux pressions.

**Fonction :**
- Ignorer répétitions rapides involontaires
- Délai configurable entre frappes

**Cas d'usage :**
- Tremblements de la main
- Spasmes musculaires
- Éviter double frappe accidentelle

**Différence selon environnement :**
- **GNOME** : Délai uniquement pour même touche
- **KDE** : Délai pour toutes les touches

**Configuration KDE :** Accessibilité → Filtres de clavier → Rebonds de touches

**💡 Point clé :** "Rebond" = ignorer les frappes qui "rebondissent" trop vite.

---


### Question 37
**Réponse correcte : C. Orca**

**Explication :**
**Orca** est le lecteur d'écran principal pour Linux.

**Fonctions :**
- Synthèse vocale (Text-to-Speech)
- Lecture texte sous curseur
- Annonce événements écran
- Support afficheurs braille

**Installation et utilisation :**
```bash
sudo apt install orca
orca
orca --setup  # Configuration
```

**Activation :**
- GNOME : Accès universel → Vision → Lecteur d'écran
- Autre : Lancer via menu

**Autres lecteurs :**
- **JAWS** → Windows (propriétaire)
- **NVDA** → Windows (gratuit)
- **VoiceOver** → macOS/iOS

**💡 Point clé :** Orca est installé par défaut sur la plupart des distributions.

---


### Question 38
**Réponse correcte : B. KMouseTool**

**Explication :**
**KMouseTool** génère des clics automatiques sous KDE.

**Fonctions :**
- Clic quand curseur s'arrête (Clic par survol)
- Clic maintenu → clic droit (Simulation clic secondaire)
- Délai configurable

**Équivalent GNOME :**
- Accès universel → Pointage et clic → Clic par survol
- Accès universel → Pointage et clic → Simulation clic secondaire

**Cas d'usage :**
- Microtraumatismes répétés
- Douleur au clic
- Impossibilité d'appuyer sur bouton souris

**💡 Point clé :** KMouseTool = K + MouseTool (outil souris KDE).

---


### Question 39
**Réponse correcte : B. 5**

**Explication :**
En mode **Navigation au clavier** (Mouse Keys), le pavé numérique contrôle la souris :

**Déplacement :**
- `8` → Haut
- `2` → Bas
- `4` → Gauche
- `6` → Droite
- `7`, `9`, `1`, `3` → Diagonales

**Clics :**
- **`5`** → Clic gauche
- `/` → Sélection bouton gauche
- `*` → Sélection bouton droit
- `-` → Double-clic
- `0` → Maintenir bouton
- `.` → Relâcher bouton

**Activation :**
- GNOME : Accès universel → Pointage et clic → Touches de la souris
- KDE : Souris → Navigation au clavier

**💡 Point clé :** 5 est au centre du pavé, logique pour "cliquer ici".

---


### Question 40
**Réponse correcte : C. Thème à fort contraste**

**Explication :**
Les **thèmes à fort contraste** aident les personnes avec déficience visuelle.

**Caractéristiques :**
- Couleurs vives et contrastées
- Contours marqués
- Texte bien visible
- Séparation claire éléments UI

**Cas d'usage :**
- Basse vision
- Daltonisme
- Fatigue visuelle
- Éclairage difficile

**Configuration :**
- GNOME : Accès universel → Vision → Contraste élevé
- KDE/Autres : Apparence → Thème → High Contrast

**Autres aides visuelles :**
- Grand texte
- Taille curseur agrandie
- Loupe d'écran

**💡 Point clé :** Contraste élevé ≠ thème sombre (ce sont deux choses différentes).

---


---

## 📊 Score et évaluation

### Calcul du score

**106.1 - X11 (20 questions)**
- Score : ___/20

**106.2 - Bureaux graphiques (13 questions)**
- Score : ___/13

**106.3 - Accessibilité (7 questions)**
- Score : ___/7

**TOTAL : ___/40**

### Interprétation

| Score | Niveau | Recommandation |
|-------|--------|----------------|
| 36-40 | Excellent | Vous maîtrisez le sujet, révision légère suffisante |
| 32-35 | Très bon | Bonne compréhension, réviser les points faibles |
| 28-31 | Bon | Compréhension correcte, approfondir certains aspects |
| 24-27 | Passable | Revoir les concepts fondamentaux |
| < 24 | Insuffisant | Étude approfondie nécessaire |

### Points à revoir selon vos erreurs

**Si erreurs sur 106.1 :**
- [ ] Architecture client-serveur de X Window
- [ ] Format et signification de `$DISPLAY`
- [ ] Hiérarchie des fichiers de configuration
- [ ] Différence `setxkbmap` vs `localectl`
- [ ] Génération de xorg.conf
- [ ] Contrôle d'accès xhost vs xauth
- [ ] Différences X11 vs Wayland

**Si erreurs sur 106.2 :**
- [ ] Environnements de bureau et leurs boîtes à outils
- [ ] Fichiers .desktop et leur structure
- [ ] Protocoles d'accès distant (VNC, RDP, Spice, XDMCP)
- [ ] Ports par défaut des protocoles
- [ ] Sécurisation de VNC avec SSH
- [ ] Applications par environnement

**Si erreurs sur 106.3 :**
- [ ] Touches rémanentes, lentes, rebonds
- [ ] Gestes d'activation d'accessibilité
- [ ] Orca comme lecteur d'écran
- [ ] Navigation au clavier (pavé numérique)
- [ ] Thèmes et paramètres visuels
- [ ] Outils d'assistance par environnement

---

## 🎯 Exercices pratiques recommandés

### Pour 106.1

1. **Explorer la configuration X** :
   - Générer un xorg.conf avec `Xorg -configure`
   - Analyser les sections et leur signification
   - Créer un fichier keyboard.conf personnalisé

2. **Tester dispositions clavier** :
   - Utiliser `setxkbmap` pour changer disposition
   - Rendre permanent avec `localectl`
   - Vérifier avec `localectl status`

3. **Diagnostiquer X** :
   - Utiliser `xdpyinfo` pour voir extensions
   - Consulter `/var/log/Xorg.0.log`
   - Analyser `~/.xsession-errors`

4. **Expérimenter accès distant** :
   - Configurer `xhost` (environnement test)
   - Essayer `xauth` pour authentification
   - Lancer application graphique distante

### Pour 106.2

1. **Tester environnements de bureau** :
   - Installer GNOME, KDE, Xfce (VM recommandée)
   - Comparer ressources utilisées
   - Noter différences ergonomiques

2. **Créer fichier .desktop** :
   - Créer application personnalisée
   - Placer dans `~/.local/share/applications/`
   - Vérifier apparition dans lanceur

3. **Configurer VNC** :
   - Installer et configurer serveur VNC
   - Modifier `~/.vnc/xstartup`
   - Se connecter via client VNC
   - Tunneliser via SSH

4. **Accès RDP** :
   - Installer xfreerdp ou Remmina
   - Se connecter à machine Windows
   - Tester qualités de connexion

### Pour 106.3

1. **Tester fonctions clavier** :
   - Activer Touches rémanentes (5× Maj)
   - Tester raccourcis une touche à la fois
   - Activer Touches lentes (8s Maj)
   - Expérimenter Rebonds de touches

2. **Navigation au clavier** :
   - Activer Touches de la souris
   - Contrôler curseur avec pavé numérique
   - Effectuer clics avec touches

3. **Assistance visuelle** :
   - Activer thème fort contraste
   - Augmenter taille police système
   - Tester loupe d'écran (GNOME Zoom, KMagnifier)

4. **Lecteur d'écran** :
   - Installer et lancer Orca
   - Naviguer dans interface à l'aveugle
   - Tester avec applications diverses

---

## 📚 Ressources pour aller plus loin

### Documentation

- [X.Org Documentation](https://www.x.org/wiki/)
- [Wayland Documentation](https://wayland.freedesktop.org/)
- [GNOME Accessibility Guide](https://help.gnome.org/users/gnome-help/stable/a11y.html)
- [KDE Accessibility](https://kde.org/accessibility/)
- [freedesktop.org Specifications](https://www.freedesktop.org/wiki/Specifications/)

### Outils en ligne

- [xkbset Documentation](https://linux.die.net/man/1/xkbset)
- [VNC Documentation](https://tigervnc.org/)
- [Orca Screen Reader](https://help.gnome.org/users/orca/stable/)

### Commandes d'aide

```bash
# X Window System
man Xorg
man xorg.conf
man setxkbmap
man localectl
man xdpyinfo
man xhost
man xauth

# Bureaux
man gnome-shell
man kwin
man xfce4-session

# VNC
man vncserver
man vncviewer

# Accessibilité
man orca
```

---

**Bonne révision ! 🚀**

*Ce QCM est conçu pour être refait plusieurs fois. Notez vos scores pour suivre votre progression.*

---

**Date de création :** 28 janvier 2026  
**Dernière mise à jour :** 28 janvier 2026  
**Version :** 1.0
