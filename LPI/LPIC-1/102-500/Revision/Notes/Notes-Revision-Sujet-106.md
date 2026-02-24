# Notes de révision - Sujet 106 : Interfaces utilisateur et bureaux

**LPIC-1 Examen 102-500**

---

## 📋 Vue d'ensemble

**Pondération totale du sujet : 4 points**

| Objectif | Description | Pondération |
|----------|-------------|-------------|
| 106.1 | Installation et configuration de X11 | 2 |
| 106.2 | Bureaux graphiques | 1 |
| 106.3 | Accessibilité | 1 |

---

## Table des matières

1. [106.1 - Installation et configuration de X11](#1061---installation-et-configuration-de-x11)
2. [106.2 - Bureaux graphiques](#1062---bureaux-graphiques)
3. [106.3 - Accessibilité](#1063---accessibilité)

---

## 106.1 - Installation et configuration de X11

🎯 **Objectif :** Installer et configurer X11  
📊 **Pondération :** 2 points

### 🔑 Concepts fondamentaux

#### Architecture du système X Window

Le système X Window (X11) est une pile logicielle qui gère l'affichage graphique sur Linux. Il utilise une architecture **client-serveur** :

| Composant | Rôle |
|-----------|------|
| **Serveur X** | Gère l'affichage, clavier, souris sur la machine locale |
| **Client X** | Application graphique (Firefox, terminal, etc.) |
| **Protocole X** | Communication entre client et serveur |

```
┌─────────────┐         Protocole X         ┌─────────────┐
│  Client X   │ ◄────────────────────────► │  Serveur X  │
│ (Firefox)   │                              │  (Xorg)     │
└─────────────┘                              └──────┬──────┘
                                                    │
                                            ┌───────▼───────┐
                                            │  Écran        │
                                            │  Clavier      │
                                            │  Souris       │
                                            └───────────────┘
```

**💡 Point clé :** Le serveur X est sur la machine avec l'écran, pas sur la machine qui exécute l'application !

#### Nom d'affichage (Display name)

Format : `hostname:displaynumber.screennumber`

**Exemples :**
- `:0` → Affichage local, première session, écran unique
- `:0.1` → Affichage local, première session, deuxième écran
- `lab01:0.2` → Machine lab01, première session, troisième écran
- `192.168.1.10:1` → IP distante, deuxième session

**Variable d'environnement :**
```bash
echo $DISPLAY
# Affiche: :0 (affichage local par défaut)
```

#### Extensions X

X11 est modulaire et extensible via des bibliothèques :

| Extension | Fonction |
|-----------|----------|
| **XRandR** | Gestion multi-écrans, résolutions |
| **XKB** | Configuration clavier avancée |
| **GLX** | Support OpenGL pour 3D |
| **Composite** | Effets de transparence, ombres |
| **XINERAMA** | Multi-écrans (ancienne méthode) |

### 📂 Fichiers de configuration

#### Structure des fichiers Xorg

| Fichier/Dossier | Usage | Priorité |
|-----------------|-------|----------|
| `/etc/X11/xorg.conf.d/` | Configurations utilisateur (snippets) | 1 (haute) |
| `/etc/X11/xorg.conf` | Configuration principale (optionnel) | 2 |
| `/usr/share/X11/xorg.conf.d/` | Configurations par défaut de la distribution | 3 (basse) |

**💡 Point clé :** Sur les distributions modernes, X se configure automatiquement au démarrage. Le fichier `xorg.conf` peut ne pas exister.

#### Sections du fichier xorg.conf

```conf
Section "InputDevice"
    # Configuration souris/clavier spécifique
    Identifier "Keyboard0"
    Driver "kbd"
EndSection

Section "InputClass"
    # Configuration par classe de périphériques (moderne)
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "fr"
    Option "XkbModel" "pc105"
EndSection

Section "Monitor"
    # Configuration moniteur physique
    Identifier "DP2"
    Option "Primary" "true"
EndSection

Section "Device"
    # Configuration carte graphique
    Identifier "Device0"
    Driver "i915"        # Pilote Intel
    BusID "PCI:0:2:0"
EndSection

Section "Screen"
    # Association Monitor + Device
    Identifier "Screen0"
    Device "Device0"
    Monitor "DP2"
EndSection

Section "ServerLayout"
    # Regroupement de tous les composants
    Identifier "Layout-1"
    Screen "Screen0" 0 0
    InputDevice "Keyboard0" "CoreKeyboard"
EndSection
```

### 🔧 Configuration du clavier

#### Fichier de configuration clavier

**Fichier :** `/etc/X11/xorg.conf.d/00-keyboard.conf`

```conf
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "fr"              # Disposition française
    Option "XkbModel" "pc105"            # Type de clavier
    Option "XkbVariant" "azerty"         # Variante
    Option "XkbOptions" "compose:ralt"   # Touche compose
EndSection
```

#### Dispositions courantes

| Layout | Description |
|--------|-------------|
| `us` | QWERTY américain |
| `fr` | AZERTY français |
| `de` | QWERTZ allemand |
| `gb` | QWERTY britannique |
| `gr(polytonic)` | Grec polytonique |

#### Modèles de clavier courants

| Model | Description |
|-------|-------------|
| `pc105` | Clavier PC 105 touches (Europe) |
| `pc104` | Clavier PC 104 touches (US) |
| `chromebook` | Chromebook |
| `latitude` | Dell Latitude |

### 🔑 Commandes essentielles

#### Générer un fichier xorg.conf

```bash
# Depuis un terminal (sans session X active)
sudo Xorg -configure
# Crée: xorg.conf.new

# Si session X déjà active
sudo Xorg :1 -configure

# Déplacer vers /etc/X11/
sudo mv xorg.conf.new /etc/X11/xorg.conf
```

#### Modifier la disposition du clavier

**Méthode 1 : setxkbmap (temporaire)**
```bash
# Changer en français
setxkbmap -layout fr

# Avec modèle spécifique
setxkbmap -model chromebook -layout "gr(polytonic)"

# Avec variante
setxkbmap -layout fr -variant azerty

# Lister les dispositions disponibles
localectl list-x11-keymap-layouts
localectl list-x11-keymap-models
```

**Méthode 2 : localectl (permanent)**
```bash
# Définir disposition française
localectl set-x11-keymap fr pc105

# Avec variante et options
localectl set-x11-keymap fr pc105 azerty compose:ralt

# Sans modifier la console
localectl --no-convert set-x11-keymap fr pc105

# Afficher configuration actuelle
localectl status
```

**💡 Point clé :** `localectl` crée automatiquement `/etc/X11/xorg.conf.d/00-keyboard.conf`

#### Informations sur le serveur X

```bash
# Informations détaillées sur session X
xdpyinfo
# Affiche: version, extensions, résolution, etc.

# Filtrer pour extensions
xdpyinfo | grep -A 30 "number of extensions"

# Vérifier affichage actuel
echo $DISPLAY

# Tester variables d'environnement
env | grep DISPLAY
```

**Exemple de sortie xdpyinfo :**
```
name of display: :0
version number: 11.0
vendor string: The X.Org Foundation
vendor release number: 12004000
X.Org version: 1.20.4
number of extensions: 25
    BIG-REQUESTS
    GLX
    RANDR
    XKEYBOARD
    ...
screen #0:
  dimensions: 1920x1080 pixels (508x286 millimeters)
  resolution: 96x96 dots per inch
```

### 🖥️ Gestionnaires d'affichage

Le gestionnaire d'affichage (Display Manager) fournit l'écran de connexion graphique et lance la session X.

| Gestionnaire | Environnement | Description |
|--------------|---------------|-------------|
| **GDM** | GNOME | GNOME Display Manager |
| **SDDM** | KDE | Simple Desktop Display Manager |
| **LightDM** | Multi | Léger, multi-environnements |
| **XDM** | Basique | X Display Manager classique |
| **LXDM** | LXDE | LXDE Display Manager |

**Démarrage automatique :**
```bash
# Vérifier gestionnaire actuel
systemctl status display-manager

# GDM
systemctl enable gdm
systemctl start gdm

# SDDM
systemctl enable sddm
systemctl start sddm

# LightDM
systemctl enable lightdm
systemctl start lightdm
```

### 🌐 Accès X distant

#### Variable DISPLAY pour affichage distant

```bash
# Sur la machine locale (avec écran)
xhost +192.168.1.10  # Autoriser machine distante

# Sur la machine distante
export DISPLAY=192.168.1.5:0  # IP de la machine avec écran
firefox &  # Firefox s'affichera sur 192.168.1.5
```

#### xhost et xauth

**xhost :** Contrôle d'accès basé sur l'hôte (moins sécurisé)
```bash
# Autoriser un hôte
xhost +192.168.1.10

# Autoriser tout le monde (DANGEREUX)
xhost +

# Révoquer un hôte
xhost -192.168.1.10

# Désactiver tous les accès
xhost -

# Lister les hôtes autorisés
xhost
```

**xauth :** Contrôle d'accès basé sur cookie (plus sécurisé)
```bash
# Extraire cookie pour affichage :0
xauth extract cookie.txt :0

# Sur machine distante, importer cookie
xauth merge cookie.txt

# Lister cookies
xauth list

# Générer nouveau cookie
xauth generate :0 .
```

### 🎨 Wayland (nouveau protocole)

Wayland est le remplaçant moderne de X Window.

| Caractéristique | X11 | Wayland |
|-----------------|-----|---------|
| **Architecture** | Client-Serveur | Compositeur direct |
| **Performance** | Bonne | Meilleure |
| **Sécurité** | Moyenne | Élevée |
| **Compatibilité** | Excellente | En progression |
| **Ressources** | Plus lourdes | Plus légères |

**Variable d'environnement Wayland :**
```bash
echo $WAYLAND_DISPLAY
# Affiche: wayland-0 (si Wayland actif)
```

**Différences architecturales :**

**X11 :**
```
Application → Serveur X → Compositeur → Noyau → Matériel
```

**Wayland :**
```
Application → Compositeur Wayland → Noyau → Matériel
```

**XWayland :** Serveur X intégré dans Wayland pour compatibilité avec applications X11 anciennes.

### 📝 Fichiers de journalisation

| Fichier | Contenu |
|---------|---------|
| `/var/log/Xorg.0.log` | Logs du serveur X (affichage :0) |
| `~/.xsession-errors` | Erreurs de session utilisateur |
| `/var/log/Xorg.1.log` | Logs du deuxième serveur X (affichage :1) |

**Consulter les erreurs X :**
```bash
# Logs serveur X
less /var/log/Xorg.0.log
grep EE /var/log/Xorg.0.log  # Erreurs

# Logs session utilisateur
less ~/.xsession-errors
```

### 💡 Astuces et commandes utiles

```bash
# Redémarrer le serveur X (attention, ferme tout!)
sudo systemctl restart display-manager

# Passer en console virtuelle (hors X)
Ctrl + Alt + F1 à F6

# Retourner à X
Ctrl + Alt + F7 (ou F1 sur certains systèmes)

# Vérifier pilote graphique utilisé
lspci -k | grep -A 3 VGA

# Tester nouvelle configuration X sans redémarrer
Xorg -config /etc/X11/xorg.conf.new :1

# Afficher résolutions disponibles
xrandr
xrandr --query

# Changer résolution temporairement
xrandr --output HDMI-1 --mode 1920x1080

# Lister périphériques d'entrée X
xinput list

# Obtenir propriétés d'un périphérique
xinput list-props 12  # 12 = ID du périphérique
```

### ✅ Checklist de vérification X11

- [ ] Comprendre architecture client-serveur de X
- [ ] Savoir lire et interpréter `$DISPLAY`
- [ ] Connaître structure des fichiers de configuration
- [ ] Maîtriser `setxkbmap` et `localectl`
- [ ] Savoir générer `xorg.conf` avec `Xorg -configure`
- [ ] Comprendre sections InputClass, Monitor, Device, Screen
- [ ] Connaître principaux gestionnaires d'affichage
- [ ] Différencier xhost et xauth
- [ ] Connaître différences X11 vs Wayland
- [ ] Savoir utiliser `xdpyinfo` pour diagnostics

---

## 106.2 - Bureaux graphiques

🎯 **Objectif :** Connaître les principaux environnements de bureau et protocoles d'accès distant  
📊 **Pondération :** 1 point

### 🖥️ Environnements de bureau majeurs

#### Composants d'un environnement de bureau

| Composant | Fonction |
|-----------|----------|
| **Gestionnaire de fenêtres** | Gère placement, décoration, redimensionnement fenêtres |
| **Gestionnaire d'affichage** | Écran de connexion graphique |
| **Boîte à outils de widgets** | GTK+, Qt - éléments visuels (boutons, menus) |
| **Applications de bureau** | Terminal, gestionnaire fichiers, éditeur texte |
| **Compositeur** | Effets visuels (transparence, animations) |

#### GNOME

**Caractéristiques :**
- Boîte à outils : **GTK+**
- Interface : GNOME Shell (depuis version 3)
- Philosophie : Minimaliste, moderne
- Distributions : Fedora, Ubuntu, Debian, RHEL/CentOS

**Applications phares :**
- Terminal : GNOME Terminal
- Fichiers : Nautilus
- Éditeur : gedit
- Navigateur : GNOME Web (Epiphany)

**GNOME Classic :** Version avec apparence traditionnelle (comme GNOME 2)

```bash
# Installer GNOME
sudo apt install gnome-core  # Debian/Ubuntu
sudo dnf install @gnome-desktop  # Fedora

# Applications essentielles
sudo apt install gnome-terminal nautilus gedit
```

#### KDE Plasma

**Caractéristiques :**
- Boîte à outils : **Qt**
- Interface : KDE Plasma Desktop
- Philosophie : Personnalisable, riche en fonctionnalités
- Distributions : openSUSE, Kubuntu, Manjaro KDE

**Applications phares :**
- Terminal : Konsole
- Fichiers : Dolphin
- Éditeur : Kate
- Suite bureautique : Calligra

```bash
# Installer KDE Plasma
sudo apt install kde-plasma-desktop  # Debian/Ubuntu
sudo dnf install @kde-desktop  # Fedora

# Applications essentielles
sudo apt install konsole dolphin kate
```

#### Xfce

**Caractéristiques :**
- Boîte à outils : **GTK+**
- Philosophie : Léger, rapide, modulaire
- Idéal pour : Machines anciennes, ressources limitées
- Distributions : Xubuntu, Manjaro Xfce

**Applications phares :**
- Terminal : Xfce Terminal
- Fichiers : Thunar
- Éditeur : Mousepad

```bash
# Installer Xfce
sudo apt install xfce4  # Debian/Ubuntu
sudo dnf install @xfce-desktop  # Fedora
```

#### Autres environnements

| Environnement | Base | Caractéristiques |
|---------------|------|------------------|
| **Cinnamon** | GNOME 3 fork | Linux Mint, look traditionnel |
| **MATE** | GNOME 2 fork | Léger, traditionnel |
| **LXDE** | GTK+ | Très léger, ressources minimales |
| **LXQt** | Qt | Version Qt de LXDE |
| **Budgie** | GNOME | Moderne, élégant |
| **Deepin DE** | Qt | Magnifique, inspiré macOS |

### 🔄 Interopérabilité freedesktop.org

#### Spécifications communes

| Spécification | Fonction |
|---------------|----------|
| **Desktop Entry** | Fichiers `.desktop` pour lanceur applications |
| **XDG Base Directory** | Emplacements standardisés (`~/.config`, `~/.local`) |
| **Autostart** | Applications au démarrage automatique |
| **Drag and Drop** | Glisser-déposer entre applications |
| **Trash** | Corbeille standardisée |
| **Icon Theme** | Thèmes d'icônes interchangeables |

#### Fichiers .desktop

**Emplacement :**
- `/usr/share/applications/` - Applications système
- `~/.local/share/applications/` - Applications utilisateur

**Exemple de fichier .desktop :**
```ini
[Desktop Entry]
Type=Application
Name=Mon Application
Comment=Description de l'application
Exec=/usr/bin/mon-app --option
Icon=mon-icone
Terminal=false
Categories=Utility;Development;
```

**Champs importants :**
- `Exec` : Commande à exécuter
- `Terminal` : true/false - lancer dans terminal
- `Categories` : Catégorie dans le menu
- `Icon` : Icône à afficher

### 🌐 Accès à distance aux environnements graphiques

#### XDMCP (X Display Manager Control Protocol)

**Caractéristiques :**
- Protocole natif de X11
- Port : UDP 177
- ⚠️ Non chiffré, non sécurisé
- Rarement utilisé aujourd'hui

**Limitations :**
- Haute bande passante requise
- Problèmes de sécurité
- Requiert X des deux côtés

#### VNC (Virtual Network Computing)

**Protocole :** Remote Frame Buffer (RFB)  
**Ports :** TCP 5900, 5901, 5902... (un par serveur VNC)

**Avantages :**
- Indépendant de la plateforme
- Léger côté client
- Pas besoin de privilèges root

**Inconvénients :**
- ⚠️ Non chiffré par défaut
- Doit être tunnelisé via SSH/VPN

**Serveurs VNC courants :**
| Serveur | Description |
|---------|-------------|
| **TigerVNC** | Fork performant de TightVNC |
| **TightVNC** | Compression optimisée |
| **x11vnc** | Partage session X existante |
| **Vino** | Serveur GNOME intégré |

**Utilisation basique :**
```bash
# Installer serveur VNC
sudo apt install tigervnc-standalone-server

# Premier démarrage (définir mot de passe)
vncserver
# Crée: ~/.vnc/passwd

# Démarrer serveur VNC
vncserver :1  # Démarre sur port 5901
vncserver :2  # Démarre sur port 5902

# Lister serveurs VNC actifs
vncserver -list

# Arrêter serveur VNC
vncserver -kill :1

# Fichier de configuration
~/.vnc/xstartup
```

**Exemple ~/.vnc/xstartup :**
```bash
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec startxfce4  # Ou: gnome-session, startkde
```

**Client VNC :**
```bash
# Installer client
sudo apt install tigervnc-viewer

# Se connecter
vncviewer 192.168.1.10:5901  # IP:port
vncviewer 192.168.1.10:1     # IP:display

# Via tunnel SSH (sécurisé)
ssh -L 5901:localhost:5901 user@192.168.1.10
vncviewer localhost:5901
```

#### RDP (Remote Desktop Protocol)

**Caractéristiques :**
- Protocole Microsoft
- Port : TCP 3389
- Natif sur Windows
- Client Linux : **Remmina**, **xfreerdp**

**Utilisation :**
```bash
# Installer client RDP
sudo apt install remmina remmina-plugin-rdp

# Ou en ligne de commande
sudo apt install freerdp2-x11

# Se connecter
xfreerdp /v:192.168.1.10 /u:utilisateur /p:motdepasse
xfreerdp /v:192.168.1.10 /u:utilisateur /size:1920x1080 /f  # Plein écran
```

**Serveur RDP Linux :**
```bash
# XRDP - serveur RDP pour Linux
sudo apt install xrdp
sudo systemctl enable xrdp
sudo systemctl start xrdp

# Configuration
/etc/xrdp/xrdp.ini
```

#### Spice (Simple Protocol for Independent Computing Environments)

**Caractéristiques :**
- Conçu pour machines virtuelles
- Intégration USB, audio, partage fichiers
- Utilisé par : QEMU/KVM, oVirt, Proxmox
- Port : 5900 (par défaut)

**Avantages :**
- Haute performance
- Support multi-moniteurs
- Intégration périphériques locaux
- Qualité audio/vidéo

**Client Spice :**
```bash
# Installer client
sudo apt install virt-viewer

# Se connecter
remote-viewer spice://192.168.1.10:5900
```

#### Comparaison des protocoles

| Protocole | Bande passante | Sécurité | Usage typique |
|-----------|----------------|----------|---------------|
| **XDMCP** | Très élevée | ⚠️ Faible | Obsolète |
| **VNC** | Moyenne | ⚠️ Faible (SSH requis) | Accès simple, multi-OS |
| **RDP** | Basse | ✅ Bonne | Windows principalement |
| **Spice** | Basse | ✅ Bonne | Virtualisation |

### 🎹 Raccourcis clavier courants

| Raccourci | Fonction | Environnements |
|-----------|----------|----------------|
| `Alt + Tab` | Basculer entre fenêtres | Tous |
| `Alt + F2` | Exécuter une commande | Tous |
| `Alt + F4` | Fermer fenêtre | Tous |
| `Ctrl + Alt + T` | Ouvrir terminal | GNOME, MATE |
| `Ctrl + Alt + Del` | Gestionnaire tâches / Déconnexion | Variable |
| `Super + L` | Verrouiller écran | Tous |
| `Ctrl + Alt + F1-F6` | Consoles virtuelles | Tous |
| `Ctrl + Alt + F7` | Retour à X | Tous |

**💡 Note :** `Super` = Touche Windows

### 🔧 Outils d'administration

```bash
# Changer environnement de bureau par défaut
sudo update-alternatives --config x-session-manager

# Voir gestionnaire d'affichage actif
cat /etc/X11/default-display-manager

# Lancer session spécifique manuellement
startx  # Démarre X avec ~/.xinitrc
startxfce4  # Démarre Xfce
gnome-session  # Démarre GNOME
startkde  # Démarre KDE

# Redémarrer gestionnaire d'affichage
sudo systemctl restart gdm
sudo systemctl restart sddm
sudo systemctl restart lightdm
```

### ✅ Checklist de vérification Bureaux

- [ ] Connaître GNOME, KDE, Xfce et leurs différences
- [ ] Savoir quelle boîte à outils utilise chaque bureau (GTK+ vs Qt)
- [ ] Comprendre fichiers .desktop et leur emplacement
- [ ] Connaître VNC, RDP, Spice et leurs cas d'usage
- [ ] Savoir sécuriser VNC avec SSH
- [ ] Connaître ports par défaut (VNC 5900, RDP 3389)
- [ ] Comprendre limitations XDMCP
- [ ] Savoir installer et démarrer serveur VNC

---

## 106.3 - Accessibilité

🎯 **Objectif :** Connaître les technologies d'assistance pour personnes handicapées  
📊 **Pondération :** 1 point

### ♿ Paramètres d'accessibilité

#### Emplacement dans les environnements

| Environnement | Emplacement paramètres |
|---------------|------------------------|
| **GNOME** | Paramètres → Accès universel |
| **KDE** | Paramètres du système → Personnalisation → Accessibilité |
| **Xfce** | Gestionnaire de paramètres → Accessibilité |

#### Menu d'accès rapide

**GNOME :** Menu Accès universel (coin supérieur droit)
- Activation permanente disponible
- Accès rapide aux fonctions principales

### ⌨️ Assistance clavier

#### Touches rémanentes (Sticky Keys)

**Fonction :** Permet de taper les raccourcis clavier une touche à la fois

**Cas d'usage :** 
- Impossibilité d'appuyer sur plusieurs touches simultanément
- Mobilité réduite des mains

**Utilisation :**
```
Au lieu de : Ctrl + C (simultané)
Faire :      Ctrl (appuyer/relâcher) puis C (appuyer/relâcher)
```

**Geste d'activation :** Appuyer 5 fois sur `Majuscule`

**GNOME :** Accès universel → Saisie → Touches rémanentes  
**KDE :** Accessibilité → Touches de modification

#### Touches lentes (Slow Keys)

**Fonction :** La touche doit être maintenue enfoncée un certain temps pour être acceptée

**Cas d'usage :**
- Éviter frappes accidentelles
- Tremblements involontaires

**Geste d'activation :** Maintenir `Majuscule` enfoncée 8 secondes

**GNOME :** Accès universel → Saisie → Touches lentes  
**KDE :** Accessibilité → Filtres de clavier → Touches lentes

#### Rebonds de touches (Bounce Keys)

**Fonction :** Délai minimum entre deux pressions de touche

**Cas d'usage :**
- Tremblements de la main
- Éviter répétitions involontaires

**Fonctionnement :**
- GNOME : Délai uniquement pour répétition de la même touche
- KDE : Délai pour toutes les touches

**KDE :** Accessibilité → Filtres de clavier → Rebonds de touches

#### Récapitulatif des gestes d'activation

| Fonction | Geste |
|----------|-------|
| **Touches rémanentes** | Appuyer 5× sur `Majuscule` |
| **Touches lentes** | Maintenir `Majuscule` 8 secondes |

**Activation des gestes :**
- **GNOME :** Accès universel → Assistance frappe → Activer par le clavier
- **KDE :** Accessibilité → Utiliser les gestes pour activer...

### 🖱️ Assistance souris

#### Navigation au clavier (Mouse Keys)

**Fonction :** Contrôler le pointeur souris avec le pavé numérique

**Touches du pavé numérique :**
| Touche | Action |
|--------|--------|
| `8` | Haut |
| `2` | Bas |
| `4` | Gauche |
| `6` | Droite |
| `7` | Haut-gauche |
| `9` | Haut-droite |
| `1` | Bas-gauche |
| `3` | Bas-droite |
| `5` | Clic gauche |
| `0` | Maintenir bouton |
| `.` | Relâcher bouton |
| `/` | Sélection bouton gauche |
| `*` | Sélection bouton droit |
| `-` | Sélection double-clic |

**Configuration :**
- **GNOME :** Accès universel → Pointage et clic → Touches de la souris
- **KDE :** Paramètres système → Souris → Navigation au clavier

**Options personnalisables (KDE) :**
- Vitesse de déplacement
- Accélération
- Délai avant accélération

#### Clavier à l'écran (On-Screen Keyboard)

**Fonction :** Clavier virtuel pour saisie à la souris/écran tactile

**GNOME :** Accès universel → Saisie → Clavier à l'écran  
**Application externe :** `onboard`

```bash
# Installer Onboard
sudo apt install onboard

# Lancer
onboard
```

**Caractéristiques :**
- Apparaît automatiquement dans champs texte
- Utilisable avec souris ou écran tactile
- Compatible tous environnements de bureau

#### Assistant de clic

**Fonction :** Générer des clics sans appuyer sur bouton souris

**GNOME : Simulation du clic secondaire**
- Maintenir bouton gauche enfoncé → génère clic droit
- Accès universel → Pointage et clic → Simulation clic secondaire

**GNOME : Clic par survol**
- Immobiliser curseur → génère clic
- Délai configurable
- Accès universel → Pointage et clic → Clic par survol

**KDE : KMouseTool**
- Application dédiée
- Fonctions similaires à GNOME
- Lancement via menu applications

#### Réglage double-clic

**Fonction :** Augmenter le délai entre deux clics pour qu'ils comptent comme double-clic

**Emplacement :**
- Préférences de la souris
- Réglage du délai de double-clic

**Cas d'usage :** Difficultés à cliquer rapidement

### 👁️ Assistance visuelle

#### Thèmes et apparence

| Paramètre | Fonction | Cas d'usage |
|-----------|----------|-------------|
| **Contraste élevé** | Couleurs vives, contours marqués | Faible vision, daltonisme |
| **Grand texte** | Agrandir police système | Presbytie, basse vision |
| **Taille du curseur** | Curseur souris plus grand | Difficultés à localiser curseur |

**GNOME :**
- Accès universel → Vision → Contraste élevé
- Accès universel → Vision → Grand texte
- Accès universel → Vision → Taille du curseur

**Autres environnements :**
- Paramètres → Apparence → Thème
- Choix de thèmes à fort contraste disponibles

#### Loupe d'écran (Screen Magnifier)

**Fonction :** Zoomer sur portions de l'écran

**GNOME :** Accès universel → Vision → Zoom
- Taux d'agrandissement configurable
- Position de la loupe
- Ajustements de couleur

**KDE :** Application **KMagnifier**
- Disponible via lanceur d'applications
- Modes de zoom variés

**Xfce :** Zoom intégré
- `Alt` + molette souris pour zoomer

**Applications externes :**
```bash
# Autres loupes disponibles
sudo apt install magnifier  # Loupe simple
```

#### Lecteur d'écran (Screen Reader)

**Orca :** Lecteur d'écran principal pour Linux

**Fonctions :**
- Synthèse vocale
- Lecture texte sous curseur
- Annonce événements à l'écran
- Support afficheurs braille

```bash
# Installer Orca
sudo apt install orca

# Lancer
orca

# Configuration
orca --setup
```

**Activation :**
- **GNOME :** Accès universel → Vision → Lecteur d'écran
- **Autre :** Lancer via menu applications

**Compatibilité :**
- Fonctionnement optimal avec applications GTK+
- Support variable selon applications

#### Afficheur braille (Braille Display)

**Fonction :** Périphérique matériel affichant caractères braille tactiles

**Configuration :**
- Via Orca
- Détection automatique du périphérique
- Support de nombreux modèles

**Avantages :**
- Lecture tactile pour aveugles complets
- Complément au lecteur d'écran

### 🔊 Assistance auditive

#### Alerte visuelle (Visual Bell)

**Fonction :** Remplacer bip sonore par flash visuel

**Cas d'usage :** Malentendants, environnements silencieux

**Configuration :**
- **GNOME :** Accès universel → Menu permanent → Alerte visuelle
- **KDE :** Accessibilité → Cloche visuelle (visual bell)

**Effets possibles :**
- Flash de la fenêtre
- Flash de l'écran entier
- Flash de couleur spécifique

### 🛠️ Outils en ligne de commande

#### AccessX (Extensions clavier X)

**Commande :** `xkbset`

```bash
# Installer xkbset (si disponible)
sudo apt install xkbset

# Activer touches rémanentes
xkbset sticky -twokey -latchlock

# Activer touches lentes
xkbset slowkeys 500  # Délai en ms

# Activer rebonds de touches
xkbset bouncekeys 500  # Délai en ms

# Désactiver
xkbset -sticky
xkbset -slowkeys
xkbset -bouncekeys

# Afficher état actuel
xkbset q
```

**💡 Note :** `xkbset` configure AccessX, les extensions d'accessibilité de X Window System

### 📋 Récapitulatif des technologies d'assistance

#### Par catégorie de handicap

**Mobilité réduite - Clavier :**
- ✅ Touches rémanentes
- ✅ Touches lentes
- ✅ Rebonds de touches
- ✅ Clavier à l'écran

**Mobilité réduite - Souris :**
- ✅ Navigation au clavier (pavé numérique)
- ✅ Clic par survol
- ✅ Simulation clic secondaire
- ✅ Délai double-clic augmenté

**Basse vision :**
- ✅ Grand texte
- ✅ Contraste élevé
- ✅ Taille curseur agrandie
- ✅ Loupe d'écran

**Cécité :**
- ✅ Lecteur d'écran (Orca)
- ✅ Afficheur braille
- ✅ Synthèse vocale

**Malentendants :**
- ✅ Alerte visuelle
- ✅ Sous-titres (applications vidéo)

### ✅ Checklist de vérification Accessibilité

- [ ] Comprendre différence touches rémanentes, lentes, rebonds
- [ ] Connaître gestes d'activation (5× Maj, 8s Maj)
- [ ] Savoir configurer navigation au clavier (touches souris)
- [ ] Connaître Orca comme lecteur d'écran principal
- [ ] Comprendre utilité des thèmes à fort contraste
- [ ] Savoir qu'Onboard est le clavier à l'écran
- [ ] Connaître KMagnifier (KDE) et zoom GNOME
- [ ] Différencier clic par survol et simulation clic secondaire
- [ ] Connaître alerte visuelle pour malentendants
- [ ] Savoir qu'AccessX est l'extension X pour accessibilité

---

## 📚 Ressources complémentaires

### Documentation officielle

- [X.Org Documentation](https://www.x.org/wiki/)
- [GNOME Accessibility](https://help.gnome.org/users/gnome-help/stable/a11y.html)
- [KDE Accessibility](https://kde.org/accessibility/)
- [freedesktop.org Specifications](https://www.freedesktop.org/wiki/Specifications/)

### Pages de manuel essentielles

```bash
man Xorg
man xorg.conf
man setxkbmap
man localectl
man xdpyinfo
man xhost
man xauth
man vncserver
```

### Commandes d'aide rapide

```bash
# Aide X.Org
Xorg -help
Xorg -version

# Aide localectl
localectl --help
localectl list-x11-keymap-layouts

# Aide setxkbmap
setxkbmap -help
setxkbmap -print

# Aide VNC
vncserver -help
vncviewer -help
```

---

## 🎯 Points clés à retenir

### 106.1 - X11

1. **Architecture client-serveur** : Serveur X sur machine avec écran
2. **Format DISPLAY** : `hostname:displaynumber.screennumber`
3. **Configuration moderne** : Fichiers dans `/etc/X11/xorg.conf.d/`
4. **Clavier** : `setxkbmap` (temporaire), `localectl` (permanent)
5. **Génération config** : `Xorg -configure`
6. **Wayland** : Nouveau protocole remplaçant X

### 106.2 - Bureaux

1. **GNOME** : GTK+, GNOME Shell, moderne
2. **KDE** : Qt, hautement personnalisable
3. **Xfce** : GTK+, léger et rapide
4. **VNC** : Port 5900+, à sécuriser avec SSH
5. **RDP** : Port 3389, natif Windows
6. **Spice** : Pour virtualisation, haute performance

### 106.3 - Accessibilité

1. **Touches rémanentes** : Raccourcis une touche à la fois
2. **Touches lentes** : Maintenir touche pour accepter
3. **Rebonds** : Délai entre frappes
4. **Navigation clavier** : Pavé numérique contrôle souris
5. **Orca** : Lecteur d'écran principal
6. **Contraste élevé** : Thème pour basse vision

---

**Date de création :** 28 janvier 2026  
**Dernière mise à jour :** 28 janvier 2026  
**Version :** 1.0
