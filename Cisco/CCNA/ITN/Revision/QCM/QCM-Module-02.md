# QCM - Module 02 : Configuration de base des commutateurs et des terminaux
**ITN - Introduction to Networks**

---

## Instructions
- Ce QCM contient **20 questions**
- Chaque question peut avoir une ou plusieurs bonnes réponses
- Cochez la ou les bonnes réponses avec `- [x]`
- Les réponses et explications sont à la fin

---

## Questions

### Question 1
Quel est le symbole d'invite affiché lorsqu'un utilisateur est en mode privilégié sur un équipement Cisco ?

- [ ] A. `>`
- [ ] B. `#`
- [ ] C. `(config)#`
- [ ] D. `(config-if)#`

### Question 2
Quelles méthodes peuvent être utilisées pour accéder à la CLI d'un équipement Cisco ?

- [ ] A. Port console avec câble série
- [ ] B. SSH (Secure Shell)
- [ ] C. HTTP via navigateur web
- [ ] D. Telnet

### Question 3
Quelle commande permet de passer du mode utilisateur au mode privilégié ?

- [ ] A. `configure terminal`
- [ ] B. `enable`
- [ ] C. `login`
- [ ] D. `exit`

### Question 4
Quel raccourci clavier permet de compléter automatiquement une commande dans l'IOS Cisco ?

- [ ] A. Ctrl + C
- [ ] B. Ctrl + Z
- [ ] C. Tab
- [ ] D. Entrée

### Question 5
Quelle commande permet d'entrer en mode de configuration globale depuis le mode privilégié ?

- [ ] A. `config`
- [ ] B. `configure terminal`
- [ ] C. `conf t`
- [ ] D. `configuration`

### Question 6
Quels types de lignes VTY permettent l'accès distant à un commutateur Cisco ?

- [ ] A. SSH
- [ ] B. Telnet
- [ ] C. Console
- [ ] D. HTTP

### Question 7
Quelle commande permet de sauvegarder la configuration en cours (running-config) dans la NVRAM ?

- [ ] A. `save running-config`
- [ ] B. `copy running-config startup-config`
- [ ] C. `write memory`
- [ ] D. `backup config`

### Question 8
Quelle commande chiffre tous les mots de passe en clair dans la configuration ?

- [ ] A. `enable secret`
- [ ] B. `password encryption`
- [ ] C. `service password-encryption`
- [ ] D. `encrypt passwords`

### Question 9
Où est stockée la configuration active d'un équipement Cisco ?

- [ ] A. NVRAM
- [ ] B. Flash
- [ ] C. RAM
- [ ] D. ROM

### Question 10
Où est stockée la configuration de démarrage (startup-config) ?

- [ ] A. NVRAM
- [ ] B. Flash
- [ ] C. RAM
- [ ] D. ROM

### Question 11
Quelle commande permet de configurer le nom d'hôte d'un commutateur ?

- [ ] A. `name S1`
- [ ] B. `hostname S1`
- [ ] C. `set hostname S1`
- [ ] D. `switch-name S1`

### Question 12
Dans la nomenclature des interfaces Cisco, que signifie `GigabitEthernet 0/0/1` ?

- [ ] A. Interface Fast Ethernet, module 0, port 1
- [ ] B. Interface Gigabit Ethernet, slot 0, sous-slot 0, port 1
- [ ] C. Interface 10 Gigabit Ethernet, port 1
- [ ] D. Interface série, port 0/0/1

### Question 13
Quelle commande affiche la configuration active en mémoire RAM ?

- [ ] A. `show startup-config`
- [ ] B. `show running-config`
- [ ] C. `show config`
- [ ] D. `display configuration`

### Question 14
Combien de lignes VTY sont généralement disponibles sur un commutateur Cisco pour les connexions simultanées ?

- [ ] A. 1 (ligne 0)
- [ ] B. 5 (lignes 0 à 4)
- [ ] C. 10 (lignes 0 à 9)
- [ ] D. 16 (lignes 0 à 15)

### Question 15
Quelle commande permet de retourner directement au mode privilégié depuis n'importe quel sous-mode de configuration ?

- [ ] A. `exit`
- [ ] B. `quit`
- [ ] C. `end`
- [ ] D. Ctrl + Z

### Question 16
Quel type de chiffrement utilise la commande `enable secret` pour protéger le mot de passe ?

- [ ] A. Type 0 (aucun chiffrement)
- [ ] B. Type 5 (MD5)
- [ ] C. Type 7 (Vigenère - faible)
- [ ] D. Type 9 (SCRYPT)

### Question 17
Pour configurer une bannière de connexion (MOTD), quelle commande est utilisée ?

- [ ] A. `banner login`
- [ ] B. `banner motd`
- [ ] C. `message-of-the-day`
- [ ] D. `set banner`

### Question 18
Quelle commande permet de désactiver la recherche DNS pour éviter les délais lors de fautes de frappe ?

- [ ] A. `no dns lookup`
- [ ] B. `disable dns`
- [ ] C. `no ip domain-lookup`
- [ ] D. `dns off`

### Question 19
Quelle est la commande pour effacer complètement la configuration de démarrage ?

- [ ] A. `delete startup-config`
- [ ] B. `erase startup-config`
- [ ] C. `clear startup-config`
- [ ] D. `remove startup-config`

### Question 20
Après avoir effacé la startup-config, quelle commande redémarre l'équipement ?

- [ ] A. `reboot`
- [ ] B. `restart`
- [ ] C. `reload`
- [ ] D. `reset`

---

# ✅ RÉPONSES ET EXPLICATIONS DÉTAILLÉES

## Question 1
**Réponse correcte : B**

**Explication :**
Le symbole `#` indique que l'utilisateur est en mode privilégié (Privileged EXEC Mode). Le symbole `>` indique le mode utilisateur, `(config)#` le mode de configuration globale, et `(config-if)#` le mode de configuration d'interface.

**💡 Point clé :** Le mode privilégié donne accès à toutes les commandes de consultation et de diagnostic, mais ne permet pas de modifier la configuration (il faut passer en mode configuration pour cela).

---

## Question 2
**Réponses correctes : A, B, D**

**Explication :**
Les méthodes d'accès à la CLI Cisco incluent :
- **Port console (A)** : Accès direct avec câble série (configuration initiale)
- **SSH (B)** : Accès distant sécurisé et chiffré (recommandé)
- **Telnet (D)** : Accès distant non chiffré (déconseillé)

HTTP (C) donne accès à une interface web graphique, pas à la CLI.

**💡 Point clé :** SSH est la méthode recommandée pour l'accès distant car elle chiffre toutes les communications, contrairement à Telnet qui transmet les mots de passe en clair.

---

## Question 3
**Réponse correcte : B**

**Explication :**
La commande `enable` permet de passer du mode utilisateur (`Switch>`) au mode privilégié (`Switch#`). La commande `configure terminal` permet d'entrer en mode configuration, et `exit` retourne au mode précédent.

**💡 Point clé :** Si un mot de passe `enable secret` est configuré, il faudra le saisir après avoir tapé `enable`. Pour revenir au mode utilisateur, utilisez `disable`.

---

## Question 4
**Réponse correcte : C**

**Explication :**
La touche **Tab** permet de compléter automatiquement une commande. Ctrl + C annule une commande, Ctrl + Z quitte le mode de configuration, et Entrée exécute la commande.

**💡 Point clé :** Si plusieurs commandes commencent par les mêmes lettres, Tab ne complétera que la partie commune. Utilisez `?` après pour voir les options disponibles.

---

## Question 5
**Réponses correctes : B, C**

**Explication :**
Les commandes `configure terminal` (forme complète) et `conf t` (abréviation) permettent d'entrer en mode de configuration globale depuis le mode privilégié. L'IOS Cisco accepte les abréviations non ambiguës.

**💡 Point clé :** L'invite passe de `Switch#` à `Switch(config)#` une fois en mode de configuration globale. C'est dans ce mode qu'on configure le hostname, les mots de passe, et qu'on entre dans les sous-modes de configuration.

---

## Question 6
**Réponses correctes : A, B**

**Explication :**
Les lignes VTY (Virtual TeletYpe) permettent l'accès distant via SSH (A) et Telnet (B). Le port console (C) est un accès physique local, et HTTP (D) n'utilise pas les lignes VTY traditionnelles.

**💡 Point clé :** Par défaut, les commutateurs Cisco ont 16 lignes VTY (0 à 15), mais on configure généralement les 5 premières (0 à 4) avec `line vty 0 4`. SSH nécessite une configuration supplémentaire (domaine, clés RSA).

---

## Question 7
**Réponses correctes : B, C**

**Explication :**
Les commandes `copy running-config startup-config` (forme standard) et `write memory` ou `wr` (ancien raccourci) sauvegardent la configuration active vers la NVRAM.

**💡 Point clé :** Si vous ne sauvegardez pas, toutes les modifications seront perdues au redémarrage ! La running-config est en RAM (volatile), la startup-config est en NVRAM (non-volatile).

---

## Question 8
**Réponse correcte : C**

**Explication :**
La commande `service password-encryption` chiffre tous les mots de passe en clair (type `password`) dans la configuration. Le chiffrement utilisé est de type 7 (Vigenère), qui est faible mais mieux que rien.

**💡 Point clé :** Cette commande n'affecte PAS le mot de passe `enable secret` qui est déjà chiffré en MD5 (type 5). Le chiffrement type 7 est réversible et peut être décrypté facilement, il protège surtout contre la lecture accidentelle.

---

## Question 9
**Réponse correcte : C**

**Explication :**
La configuration active (running-config) est stockée dans la **RAM**, qui est une mémoire volatile. Elle est perdue au redémarrage si elle n'est pas sauvegardée dans la NVRAM.

**💡 Point clé :** RAM = mémoire volatile = configuration active en cours d'exécution. C'est cette configuration qui est modifiée lorsque vous changez des paramètres.

---

## Question 10
**Réponse correcte : A**

**Explication :**
La configuration de démarrage (startup-config) est stockée dans la **NVRAM** (Non-Volatile RAM), qui conserve les données même après extinction. La Flash contient l'IOS, la ROM contient le bootstrap et le mini-IOS.

**💡 Point clé :** NVRAM = mémoire non-volatile = configuration qui sera chargée au démarrage. Au démarrage, l'équipement copie la startup-config de la NVRAM vers la RAM pour en faire la running-config.

---

## Question 11
**Réponse correcte : B**

**Explication :**
La commande `hostname S1` (en mode de configuration globale) permet de définir le nom d'hôte de l'équipement. Le nom apparaîtra ensuite dans l'invite de commande.

**💡 Point clé :** Le hostname est case-sensitive et peut contenir jusqu'à 63 caractères. Il est important de donner des noms descriptifs pour faciliter l'identification des équipements.

---

## Question 12
**Réponse correcte : B**

**Explication :**
La nomenclature `GigabitEthernet 0/0/1` signifie : Interface Gigabit Ethernet, slot 0, sous-slot 0, port 1. Le format général est `type slot/sous-slot/port`.

**💡 Point clé :** Sur les switches modulaires, le premier chiffre indique le module, le second le sous-module, et le troisième le port. Sur les switches fixes, on peut voir `Gi0/1` (pas de sous-slot).

---

## Question 13
**Réponse correcte : B**

**Explication :**
La commande `show running-config` (ou `sh run`) affiche la configuration active en RAM. La commande `show startup-config` affiche la configuration sauvegardée en NVRAM.

**💡 Point clé :** Cette commande est essentielle pour vérifier la configuration actuelle. Elle peut être longue, utilisez la barre d'espace pour défiler page par page, ou Entrée pour ligne par ligne.

---

## Question 14
**Réponse correcte : B**

**Explication :**
Par défaut, les commutateurs Cisco ont 5 lignes VTY (lignes 0 à 4) configurables avec `line vty 0 4`. Certains équipements plus récents peuvent avoir 16 lignes (0 à 15).

**💡 Point clé :** Chaque ligne VTY permet une connexion simultanée. Si les 5 lignes sont utilisées, les utilisateurs supplémentaires ne pourront pas se connecter. Pour plus de connexions, configurez `line vty 0 15`.

---

## Question 15
**Réponses correctes : C, D**

**Explication :**
La commande `end` et le raccourci **Ctrl + Z** permettent de retourner directement au mode privilégié depuis n'importe quel sous-mode de configuration. La commande `exit` ne remonte que d'un niveau à la fois.

**💡 Point clé :** Si vous êtes en mode `(config-if)#`, `exit` vous ramène en `(config)#`, puis un autre `exit` vous ramène en mode privilégié `#`. Avec `end` ou Ctrl+Z, vous revenez directement en mode privilégié.

---

## Question 16
**Réponse correcte : B**

**Explication :**
La commande `enable secret` utilise le chiffrement MD5 (type 5). C'est beaucoup plus sûr que le chiffrement type 7 utilisé par `enable password` (désormais obsolète).

**💡 Point clé :** Si `enable secret` et `enable password` sont tous deux configurés, c'est toujours `enable secret` qui est utilisé. Dans la config, le type 5 est visible : `enable secret 5 $1$mERr$hx...`

---

## Question 17
**Réponse correcte : B**

**Explication :**
La commande `banner motd # message #` permet de configurer une bannière (Message Of The Day) affichée avant la connexion. Le `#` est un délimiteur (peut être remplacé par un autre caractère).

**💡 Point clé :** La bannière peut avoir une utilité légale en avertissant que l'accès est réservé au personnel autorisé. Exemple :
```
banner motd #
**********************************************
* ACCES RESERVE AU PERSONNEL AUTORISE UNIQUEMENT *
* Les connexions sont surveillées et enregistrées *
**********************************************
#
```

---

## Question 18
**Réponse correcte : C**

**Explication :**
La commande `no ip domain-lookup` désactive la résolution DNS pour éviter que l'IOS n'essaie de résoudre chaque commande incorrecte comme un nom d'hôte, ce qui cause des délais frustrants.

**💡 Point clé :** Sans cette commande, si vous tapez une commande incorrecte comme "sho", l'IOS va essayer de résoudre "sho" comme un nom d'hôte, ce qui prend plusieurs secondes avant d'afficher une erreur.

---

## Question 19
**Réponse correcte : B**

**Explication :**
La commande `erase startup-config` (ou `write erase`) efface complètement la configuration de démarrage stockée en NVRAM. Après un redémarrage, l'équipement démarrera avec la configuration d'usine.

**💡 Point clé :** Cette commande est souvent utilisée en laboratoire pour réinitialiser un équipement. Attention : elle n'efface PAS la running-config ! Pour revenir à une config vierge, il faut aussi redémarrer avec `reload`.

---

## Question 20
**Réponse correcte : C**

**Explication :**
La commande `reload` redémarre l'équipement Cisco. Si la startup-config a été effacée, l'équipement démarrera en mode de configuration initiale (setup mode).

**💡 Point clé :** Après avoir tapé `reload`, l'IOS demande confirmation : "System configuration has been modified. Save? [yes/no]:" - répondez `no` si vous voulez charger la startup-config non modifiée. Puis "Proceed with reload? [confirm]" - appuyez sur Entrée.

---

**Score recommandé pour valider le module : 16/20 minimum (80%)**

**Révision conseillée si score < 16/20 :**
- Section 2.2 (Navigation IOS et modes de commande)
- Section 2.4 (Configuration de base)
- Section 2.5 (Enregistrement des configurations)
- Pratiquer dans Packet Tracer !
