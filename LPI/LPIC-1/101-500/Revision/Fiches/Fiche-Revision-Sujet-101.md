# 📄 Fiche Sujet 101 : Architecture Système

**Poids : 8 points (20%)** | Révision rapide

---

## 101.1 : Matériel et Paramètres (2 pts)

### Commandes principales
```bash
lspci               # Liste périphériques PCI
lspci -v            # Détails
lspci -k            # Modules kernel
lsusb               # Périphériques USB
lsusb -v            # Détails USB

dmesg               # Messages kernel boot
dmesg | grep -i usb # Filtrer USB
journalctl -k       # Kernel logs systemd

lsmod               # Modules chargés
modprobe module     # Charger module
modprobe -r module  # Décharger
modinfo module      # Infos module

/proc/cpuinfo       # CPU
/proc/meminfo       # RAM
/proc/interrupts    # IRQ
/proc/ioports       # I/O
/proc/dma           # DMA
/sys/               # Sysfs tree
```

### Ressources système
| Ressource | Utilisation |
|-----------|-------------|
| **IRQ** | Interruptions (souris=12, USB souvent 16+) |
| **I/O** | Adresses ports (0x3F8=COM1, 0x378=LPT1) |
| **DMA** | Accès direct mémoire |
| **/dev** | Fichiers devices |

---

## 101.2 : Boot Système (3 pts)

### Processus boot BIOS/MBR
```
1. BIOS → POST tests
2. MBR (512 bytes) → GRUB stage 1
3. GRUB stage 2 → Menu boot
4. Kernel chargement (vmlinuz)
5. initrd/initramfs → drivers
6. /sbin/init ou systemd
```

### Processus boot UEFI/GPT
```
1. UEFI firmware
2. ESP (EFI System Partition)
3. Bootloader (/EFI/ubuntu/grubx64.efi)
4. Kernel → initrd → systemd
```

### Messages boot
```bash
dmesg                      # Messages kernel
dmesg -T                   # Timestamps
dmesg -l err,warn          # Seulement erreurs/warnings
journalctl -b              # Boot actuel
journalctl -b -1           # Boot précédent
journalctl -k              # Kernel uniquement
journalctl --list-boots    # Liste boots
```

---

## 101.3 : Runlevels / Targets systemd (3 pts)

### SysVinit Runlevels (ancien)
| Runlevel | Mode | Équivalent systemd |
|----------|------|-------------------|
| **0** | Halt | poweroff.target |
| **1, S** | Single-user | rescue.target |
| **2** | Multi-user sans réseau | |
| **3** | Multi-user CLI | multi-user.target |
| **5** | Multi-user GUI | graphical.target |
| **6** | Reboot | reboot.target |

### Commandes SysVinit
```bash
runlevel            # Affiche runlevel actuel
telinit 3           # Passer runlevel 3
init 6              # Reboot
```

### Systemd Targets
```bash
# Affichage
systemctl get-default                  # Target par défaut
systemctl list-units --type=target     # Liste targets

# Changer target
systemctl isolate multi-user.target    # Immédiat
systemctl isolate graphical.target
systemctl isolate rescue.target

# Définir défaut
systemctl set-default multi-user.target
systemctl set-default graphical.target

# Boot/Halt
systemctl reboot
systemctl poweroff
systemctl suspend
systemctl hibernate
```

### Services systemd
```bash
systemctl start service       # Démarrer
systemctl stop service        # Arrêter
systemctl restart service     # Redémarrer
systemctl reload service      # Recharger config
systemctl status service      # État
systemctl enable service      # Activer au boot
systemctl disable service     # Désactiver boot
systemctl is-enabled service  # Vérifie si activé
systemctl is-active service   # Vérifie si actif

systemctl list-units --type=service      # Liste services
systemctl list-unit-files --type=service # Tous + état enabled
```

### Units systemd
```bash
# Localisation units
/usr/lib/systemd/system/      # Système (défaut)
/etc/systemd/system/          # Admin (priorité)
/run/systemd/system/          # Runtime

# Commandes
systemctl daemon-reload       # Recharger config
systemctl edit service        # Override config
systemctl cat service         # Voir unit file
journalctl -u service         # Logs service
```

---

## 🎯 Points clés examen

1. **lspci/lsusb** : Identifier hardware
2. **dmesg** : Messages kernel/boot
3. **/proc et /sys** : Infos système runtime
4. **Boot BIOS** : MBR → GRUB → Kernel → init
5. **Boot UEFI** : ESP → Bootloader EFI → Kernel
6. **Runlevel 1/S** = rescue.target (single-user)
7. **Runlevel 3** = multi-user.target (CLI)
8. **Runlevel 5** = graphical.target (GUI)
9. **systemctl isolate** : Changer target immédiatement
10. **systemctl set-default** : Target par défaut au boot
11. **journalctl -b** : Logs boot actuel
12. **/etc/systemd/system/** prioritaire sur /usr/lib/systemd/

---

## 📋 Checklist révision

- [ ] Différence lspci vs lsusb
- [ ] Lire /proc/cpuinfo et /proc/meminfo
- [ ] Processus boot BIOS/MBR (6 étapes)
- [ ] Différence initrd vs initramfs
- [ ] Commandes dmesg (filtres, timestamps)
- [ ] Runlevels 0,1,3,5,6 + équivalents systemd
- [ ] systemctl : start/stop/enable/disable
- [ ] systemctl isolate vs set-default
- [ ] Localisation units systemd (/etc prioritaire)
- [ ] journalctl : -b, -u, -k
