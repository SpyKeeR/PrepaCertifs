# 📄 Fiche Sujet 106 : Interfaces Utilisateur

**Poids : 4 points (7%)** | Révision rapide

---

## 106.1 : Installation et configuration de X11 (2 pts)

### Serveur X
```bash
# Variables clés
$DISPLAY               # :0 (local), hostname:0 (distant)
echo $DISPLAY

# Autorisation affichage
xhost +hostname        # Autoriser hôte
xhost -hostname        # Refuser hôte
xhost +                # Autoriser tous (DANGEREUX)
xauth                  # Gestion authentification

# Démarrage X
startx                 # Démarrer X (script)
xinit                  # Démarrer X (direct)
X -configure           # Générer config

# Fichiers config
/etc/X11/xorg.conf             # Config principale (optionnel moderne)
/etc/X11/xorg.conf.d/*.conf    # Snippets config
~/.xsession                    # Session utilisateur
~/.xinitrc                     # Initialisation X

# Infos
xdpyinfo               # Infos display
xrandr                 # Config écrans/résolutions
xwininfo               # Infos fenêtres
```

### Display managers
```bash
# Principaux
gdm3                   # GNOME Display Manager
lightdm                # Léger, universel
sddm                   # KDE Plasma
xdm                    # Basique

# Services systemd
systemctl status gdm3
systemctl start lightdm
systemctl enable sddm
```

### Desktop environments
| Environnement | Caractéristiques |
|---------------|------------------|
| **GNOME** | Moderne, complet, lourd |
| **KDE Plasma** | Riche, personnalisable |
| **XFCE** | Léger, traditionnel |
| **LXDE/LXQt** | Très léger |
| **MATE** | Fork GNOME 2 |
| **Cinnamon** | Fork GNOME 3 |

---

## 106.2 : Bureaux graphiques (1 pt)

### Window managers
```bash
# Standalone WM
openbox                # Léger, configurable
fluxbox                # Minimaliste
i3                     # Tiling
awesome                # Tiling + Lua
```

### Protocoles
```bash
# X11 (traditionnel)
- Client-serveur
- Réseau transparent
- Lourd

# Wayland (moderne)
- Direct compositeur
- Plus léger, sécurisé
- Remplace X11 progressivement
```

---

## 106.3 : Accessibilité (1 pt)

### Outils d'accessibilité
```bash
# Lecteurs d'écran
orca                   # Lecteur GNOME

# Clavier visuel
onboard                # Clavier à l'écran
florence               # Alternative

# Loupe
gnome-magnifier        # Loupe GNOME
kmag                   # Loupe KDE

# Thèmes haute visibilité
# Paramètres → Accessibilité
- Fort contraste
- Grande police
- Thèmes sombres
```

### Sticky keys / Slow keys
```bash
# Sticky keys : touches modificatrices persistent
# Slow keys : délai avant acceptation touche
# Bounce keys : ignore répétitions rapides
# Mouse keys : déplacer souris au clavier

# Configuration
gsettings              # GNOME
systemsettings5        # KDE
```

---

## 🎯 Points clés examen

### Must know
- ✅ Variable `$DISPLAY` (format `:0`, `hostname:0`)
- ✅ `xhost` pour autorisation affichage
- ✅ Display managers : gdm3, lightdm, sddm, xdm
- ✅ Desktop environments : GNOME, KDE, XFCE, LXDE
- ✅ Différence X11 vs Wayland
- ✅ Outils accessibilité : orca, onboard, magnifier
- ✅ `/etc/X11/xorg.conf.d/` pour config X

### Pièges
- ❌ Confondre X server et X client
- ❌ Oublier export `DISPLAY` pour apps distantes
- ❌ `xhost +` sans restriction (sécurité)

### Astuces rapides
```bash
# Exécuter app graphique distante
export DISPLAY=:0
ssh -X user@host firefox    # X11 forwarding

# Changer résolution
xrandr                      # Lister
xrandr --output HDMI-1 --mode 1920x1080

# Tester affichage
xclock                      # Horloge simple
xeyes                       # Yeux qui suivent souris

# Redémarrer display manager
systemctl restart gdm3
systemctl restart lightdm
```

---

**💡 Conseil :** Ce sujet est léger (4 pts). Connaître les bases suffit : `$DISPLAY`, display managers, et accessibilité.
