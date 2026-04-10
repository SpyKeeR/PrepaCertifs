# QCM - Module 5 : VLAN Trunks & EtherChannel
**CCNP ENCOR v8 - Trunks VLAN et Agrégation de Liens**

---

## 📋 Instructions

- **25 questions à choix multiples**
- **1 seule réponse correcte** par question
- **Durée recommandée** : 30 minutes
- **Seuil de réussite** : 80% (20/25)

---

## 🎯 Questions

### Question 1
Quelle est la valeur du champ TPID (Tag Protocol Identifier) dans une trame 802.1Q ?
- A) 0x8100
- B) 0x0800
- C) 0x0806
- D) 0x86DD

### Question 2
Quel est le Native VLAN par défaut sur un trunk Cisco ?
- A) VLAN 0
- B) VLAN 1
- C) VLAN 999
- D) VLAN 1005

### Question 3
Que se passe-t-il si le Native VLAN est différent sur les deux extrémités d'un trunk ?
- A) Le trunk ne se forme pas
- B) CDP/VTP génèrent des warnings, risque de VLAN hopping
- C) Le switch avec la priorité la plus basse impose son Native VLAN
- D) Les trames sont automatiquement taggées

### Question 4
Quelle commande limite les VLANs 10, 20 et 30 sur un trunk ?
- A) `switchport trunk vlan 10,20,30`
- B) `switchport trunk allowed vlan 10,20,30`
- C) `switchport vlan allowed 10,20,30`
- D) `switchport trunk filter vlan 10,20,30`

### Question 5
Quel protocole Cisco négocie automatiquement la formation de trunks ?
- A) VTP (VLAN Trunking Protocol)
- B) STP (Spanning Tree Protocol)
- C) DTP (Dynamic Trunking Protocol)
- D) CDP (Cisco Discovery Protocol)

### Question 6
Deux switches ont les modes DTP suivants. Quel est le résultat ?
- Switch A : `dynamic auto`
- Switch B : `dynamic auto`
- A) Trunk formé
- B) Access formé (aucun switch n'initie)
- C) Erreur de configuration
- D) Dépend du Native VLAN

### Question 7
Quel mode DTP initie activement la formation d'un trunk ?
- A) dynamic auto
- B) dynamic desirable
- C) access
- D) nonegotiate

### Question 8
Quelle commande désactive DTP sur un port trunk pour améliorer la sécurité ?
- A) `switchport mode trunk static`
- B) `switchport nonegotiate`
- C) `no switchport dtp`
- D) `switchport dtp disable`

### Question 9
Quel est le mode VTP par défaut sur un switch Cisco ?
- A) Client
- B) Server
- C) Transparent
- D) Off

### Question 10
Un switch VTP en mode Client peut-il créer des VLANs localement ?
- A) Oui, mais uniquement des VLANs Extended (1006-4094)
- B) Oui, si le domaine VTP est vide
- C) Non, mode Client est en lecture seule
- D) Oui, mais ils ne sont pas propagés

### Question 11
Qu'est-ce que la Configuration Revision Number en VTP ?
- A) Le nombre de VLANs configurés
- B) Un compteur incrémental indiquant la version de la config VLANs
- C) Le numéro de version VTP (v1, v2, v3)
- D) L'ID du serveur VTP Primary

### Question 12
Quel est le danger d'ajouter un switch VTP Client avec une Configuration Revision élevée ?
- A) Le switch refuse la connexion
- B) Le switch écrase tous les VLANs du domaine
- C) Les VLANs sont dupliqués
- D) VTP passe en mode Transparent

### Question 13
Comment réinitialiser la Configuration Revision VTP à 0 ?
- A) `clear vtp revision`
- B) `vtp mode transparent` puis `vtp mode server`
- C) `reload` suffit
- D) Impossible de réinitialiser

### Question 14
Quelle version de VTP supporte les Extended VLANs (1006-4094) ?
- A) VTP v1
- B) VTP v2
- C) VTP v3
- D) Toutes les versions

### Question 15
Combien de liens physiques peuvent être agrégés dans un EtherChannel ?
- A) 2 à 4 liens
- B) 2 à 8 liens
- C) 2 à 16 liens
- D) 1 à 8 liens

### Question 16
Quel est l'avantage principal d'EtherChannel par rapport à plusieurs liens physiques sans agrégation ?
- A) Meilleure latence
- B) Tous les liens sont actifs, pas de blocage STP
- C) Supporte des vitesses différentes
- D) Configuration plus simple

### Question 17
Quel protocole EtherChannel est un standard IEEE et donc interopérable multi-vendor ?
- A) PAgP
- B) LACP
- C) EtherChannel On
- D) HSRP

### Question 18
Quels sont les modes de négociation LACP ?
- A) on, off
- B) desirable, auto
- C) active, passive
- D) enable, disable

### Question 19
Deux switches forment un EtherChannel avec LACP. Quel est le résultat ?
- Switch A : `channel-group 1 mode passive`
- Switch B : `channel-group 1 mode passive`
- A) EtherChannel formé
- B) EtherChannel ne se forme pas (aucun switch n'initie)
- C) Erreur err-disabled
- D) Formation après 30 secondes

### Question 20
Quel algorithme de load-balancing EtherChannel est recommandé pour des switches Layer 3 ?
- A) src-mac
- B) dst-mac
- C) src-dst-mac
- D) src-dst-ip

### Question 21
Quelle commande configure le load-balancing EtherChannel basé sur IP source et destination ?
- A) `etherchannel load-balance src-dst-ip`
- B) `port-channel load-balance src-dst-ip`
- C) `load-balance etherchannel src-dst-ip`
- D) `channel-group load-balance src-dst-ip`

### Question 22
Dans la sortie `show etherchannel summary`, que signifie le code "(SU)" ?
- A) Suspended
- B) Switched + Up (EtherChannel fonctionnel)
- C) Stand-alone + Unused
- D) Secure + Untagged

### Question 23
Quel est le prérequis critique pour que les liens physiques forment un EtherChannel ?
- A) Tous les liens doivent avoir le même speed, duplex, VLANs, mode
- B) Au moins 4 liens doivent être disponibles
- C) Les liens doivent être sur des modules différents
- D) LACP doit être désactivé

### Question 24
Un EtherChannel trunk ne se forme pas. Quelle est la cause probable ?
- A) Les Allowed VLANs sont différents sur les liens physiques
- B) Le nombre de liens dépasse 8
- C) LACP n'est pas supporté
- D) VTP est en mode Transparent

### Question 25
Quelle commande affiche les voisins LACP pour un EtherChannel ?
- A) `show etherchannel neighbors`
- B) `show lacp neighbor`
- C) `show channel-group lacp`
- D) `show interfaces lacp`

---

## ✅ Grille de réponses

| Question | Réponse | Question | Réponse | Question | Réponse |
|----------|---------|----------|---------|----------|---------|
| 1        | ⬜ A ⬜ B ⬜ C ⬜ D | 10 | ⬜ A ⬜ B ⬜ C ⬜ D | 19 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 2        | ⬜ A ⬜ B ⬜ C ⬜ D | 11 | ⬜ A ⬜ B ⬜ C ⬜ D | 20 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 3        | ⬜ A ⬜ B ⬜ C ⬜ D | 12 | ⬜ A ⬜ B ⬜ C ⬜ D | 21 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 4        | ⬜ A ⬜ B ⬜ C ⬜ D | 13 | ⬜ A ⬜ B ⬜ C ⬜ D | 22 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 5        | ⬜ A ⬜ B ⬜ C ⬜ D | 14 | ⬜ A ⬜ B ⬜ C ⬜ D | 23 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 6        | ⬜ A ⬜ B ⬜ C ⬜ D | 15 | ⬜ A ⬜ B ⬜ C ⬜ D | 24 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 7        | ⬜ A ⬜ B ⬜ C ⬜ D | 16 | ⬜ A ⬜ B ⬜ C ⬜ D | 25 | ⬜ A ⬜ B ⬜ C ⬜ D |
| 8        | ⬜ A ⬜ B ⬜ C ⬜ D | 17 | ⬜ A ⬜ B ⬜ C ⬜ D |    |         |
| 9        | ⬜ A ⬜ B ⬜ C ⬜ D | 18 | ⬜ A ⬜ B ⬜ C ⬜ D |    |         |

---

## 📖 Corrigé détaillé

### Question 1 - Réponse : A
**A) 0x8100**

**Explication :**
- **TPID (Tag Protocol Identifier)** = `0x8100`
- Identifie une trame 802.1Q taggée
- 2 bytes au début du tag 802.1Q
- Permet aux switches de reconnaître une trame VLAN

**Structure 802.1Q Tag :**
```
┌────────────────────┐
│ TPID │ TCI        │ 4 bytes
│0x8100│ PRI│CFI│VID│
└──────┴────────────┘
```

**Pourquoi les autres réponses sont fausses :**
- B) 0x0800 = IPv4 EtherType
- C) 0x0806 = ARP EtherType
- D) 0x86DD = IPv6 EtherType

---

### Question 2 - Réponse : B
**B) VLAN 1**

**Explication :**
- Native VLAN par défaut : **VLAN 1**
- Trafic Native VLAN non taggé sur trunk
- Best practice : **Changer pour autre VLAN** (ex: 999)
- Motif sécurité : Éviter VLAN hopping

**Configuration changement :**
```cisco
switchport trunk native vlan 999
```

**Pourquoi les autres réponses sont fausses :**
- A) VLAN 0 n'existe pas
- C) VLAN 999 est une bonne pratique mais pas le défaut
- D) VLAN 1005 est un VLAN réservé

---

### Question 3 - Réponse : B
**B) CDP/VTP génèrent des warnings, risque de VLAN hopping**

**Explication :**
- **Mismatch Native VLAN** :
  - CDP détecte l'incohérence → Warning
  - VTP peut générer des alertes
  - **Risque sécurité** : VLAN hopping attack
  - Trafic peut être routé vers mauvais VLAN
- Le trunk **fonctionne toujours** mais vulnérable

**Exemple warning :**
```
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on GigabitEthernet0/1 (999), with Switch neighbor port GigabitEthernet0/1 (1).
```

**Pourquoi les autres réponses sont fausses :**
- A) Le trunk se forme malgré mismatch
- C) Aucun mécanisme d'imposition automatique
- D) Native VLAN reste non taggé

---

### Question 4 - Réponse : B
**B) `switchport trunk allowed vlan 10,20,30`**

**Explication :**
- Syntaxe : `switchport trunk allowed vlan <list>`
- Liste : VLANs séparés par virgules ou plages
- Exemples :
  - `switchport trunk allowed vlan 10,20,30`
  - `switchport trunk allowed vlan 10-30`
  - `switchport trunk allowed vlan add 40` (ajout)
  - `switchport trunk allowed vlan remove 20` (suppression)

**Pourquoi les autres réponses sont fausses :**
- A) Syntaxe incorrecte (manque `allowed`)
- C) Syntaxe incorrecte (manque `trunk`)
- D) `filter` n'existe pas

---

### Question 5 - Réponse : C
**C) DTP (Dynamic Trunking Protocol)**

**Explication :**
- **DTP (Dynamic Trunking Protocol)** : Cisco proprietary
- Négocie automatiquement trunks entre switches
- Modes : trunk, access, dynamic desirable, dynamic auto
- **Risque sécurité** : VLAN hopping (DTP enabled par défaut)
- Best practice : Désactiver avec `switchport nonegotiate`

**Pourquoi les autres réponses sont fausses :**
- A) VTP synchronise VLANs, pas négociation trunks
- B) STP prévient boucles, pas négociation trunks
- D) CDP découvre voisins, pas négociation trunks

---

### Question 6 - Réponse : B
**B) Access formé (aucun switch n'initie)**

**Explication :**
- **dynamic auto** = Mode passif (attend négociation)
- Switch A : auto (attend)
- Switch B : auto (attend)
- **Résultat** : Aucun switch n'initie → **Access formé**

**Tableau négociation DTP :**
| Switch A | Switch B | Résultat |
|----------|----------|----------|
| desirable | desirable | ✅ Trunk |
| desirable | auto | ✅ Trunk |
| **auto** | **auto** | ❌ **Access** |

**Pourquoi les autres réponses sont fausses :**
- A) Trunk nécessite au moins 1 switch actif
- C) Pas d'erreur, juste access formé
- D) Native VLAN n'influence pas DTP

---

### Question 7 - Réponse : B
**B) dynamic desirable**

**Explication :**
- **dynamic desirable** : Mode actif DTP
- Envoie paquets DTP pour négocier trunk
- Répond aussi aux demandes DTP
- **dynamic auto** : Mode passif (attend, ne initie pas)

**Modes DTP :**
| Mode | Initie | Répond |
|------|--------|--------|
| trunk | ✅ | ✅ |
| **dynamic desirable** | ✅ | ✅ |
| dynamic auto | ❌ | ✅ |
| access | ❌ | ❌ |

**Pourquoi les autres réponses sont fausses :**
- A) dynamic auto est passif
- C) access force mode access (pas trunk)
- D) nonegotiate désactive DTP

---

### Question 8 - Réponse : B
**B) `switchport nonegotiate`**

**Explication :**
- `switchport nonegotiate` : Désactive DTP complètement
- Pas d'envoi de paquets DTP
- Améliore sécurité (prévient VLAN hopping)
- Utilisé avec `switchport mode trunk` ou `access`

**Configuration sécurisée :**
```cisco
interface GigabitEthernet0/1
 switchport mode trunk
 switchport nonegotiate  ← Pas DTP
exit
```

**Pourquoi les autres réponses sont fausses :**
- A) `static` n'existe pas
- C) `no switchport dtp` syntaxe incorrecte
- D) `dtp disable` syntaxe incorrecte

---

### Question 9 - Réponse : B
**B) Server**

**Explication :**
- Mode VTP par défaut : **Server**
- ⚠️ **Danger** : Server peut modifier/supprimer VLANs
- Risque si switch avec révision élevée ajouté
- Best practice : Mode **Transparent** ou **Off** (v3)

**Modes VTP :**
| Mode | Crée VLANs | Modif | Propage |
|------|------------|-------|---------|
| **Server** (défaut) | ✅ | ✅ | ✅ |
| Client | ❌ | ❌ | ✅ |
| Transparent | ✅ Local | ✅ Local | Relaie |
| Off (v3) | ✅ | ✅ | ❌ |

**Pourquoi les autres réponses sont fausses :**
- A) Client n'est pas le défaut
- C) Transparent doit être configuré
- D) Off existe seulement en VTPv3

---

### Question 10 - Réponse : C
**C) Non, mode Client est en lecture seule**

**Explication :**
- Mode **VTP Client** : **Lecture seule**
- Capacités :
  - ❌ Créer VLANs
  - ❌ Modifier VLANs
  - ❌ Supprimer VLANs
  - ✅ Recevoir updates VTP
  - ✅ Propager updates
  - ❌ Stocker config en NVRAM
- Configuration VLANs refusée :
```cisco
vlan 100
% VTP VLAN configuration not allowed when device is in CLIENT mode.
```

**Pourquoi les autres réponses sont fausses :**
- A) Client ne peut créer aucun VLAN
- B) Domaine vide ne change rien
- D) Client ne peut créer aucun VLAN

---

### Question 11 - Réponse : B
**B) Un compteur incrémental indiquant la version de la config VLANs**

**Explication :**
- **Configuration Revision** : Compteur 0-4,294,967,295
- Incrémenté à chaque modification VLANs
- Client compare révisions :
  - Révision reçue > locale → Synchronise
  - Révision reçue < locale → Ignore
- ⚠️ **Danger** : Switch avec révision élevée écrase VLANs

**Vérification :**
```cisco
show vtp status
Configuration Revision          : 42
```

**Pourquoi les autres réponses sont fausses :**
- A) Nombre de VLANs est séparé
- C) Version VTP (v1/v2/v3) est différente
- D) Primary Server est un concept VTPv3

---

### Question 12 - Réponse : B
**B) Le switch écrase tous les VLANs du domaine**

**Explication :**
- **Scénario catastrophe** :
  1. Switch retiré du réseau (révision élevée)
  2. VLANs modifiés/supprimés sur ce switch
  3. Switch reconnecté
  4. Switch propage config → **Écrase tous les VLANs !**
- Clients reçoivent révision > → Synchronisent
- VLANs supprimés → Ports access orphelins

**Solution :**
```cisco
! Réinitialiser révision AVANT connexion
vtp mode transparent
vtp mode server
```

**Pourquoi les autres réponses sont fausses :**
- A) Switch accepte la connexion
- C) VLANs ne sont pas dupliqués, remplacés
- D) Mode ne change pas automatiquement

---

### Question 13 - Réponse : B
**B) `vtp mode transparent` puis `vtp mode server`**

**Explication :**
- Méthode 1 : Mode Transparent temporaire
```cisco
vtp mode transparent
vtp mode server
! Révision réinitialisée à 0
```

- Méthode 2 : Changer domaine
```cisco
vtp domain TEMP
vtp domain PROD
```

- Méthode 3 : Supprimer vlan.dat
```cisco
delete flash:vlan.dat
reload
```

**Pourquoi les autres réponses sont fausses :**
- A) Commande n'existe pas
- C) `reload` seul ne réinitialise pas
- D) Réinitialisation possible

---

### Question 14 - Réponse : C
**C) VTP v3**

**Explication :**
- **VTPv1** : VLANs 1-1005 uniquement
- **VTPv2** : VLANs 1-1005 uniquement
- **VTPv3** : ✅ VLANs 1-4094 (Extended VLANs support)

**Autres améliorations VTPv3 :**
- Mode Off (désactive VTP)
- Primary Server (contrôle strict)
- Protected VLANs
- MST propagation

**Pourquoi les autres réponses sont fausses :**
- A/B) VTPv1/v2 limités à 1-1005
- D) Seul VTPv3 supporte Extended VLANs

---

### Question 15 - Réponse : B
**B) 2 à 8 liens**

**Explication :**
- **EtherChannel** : Agrège **2 à 8 liens physiques**
- Minimum : 2 liens (redondance)
- Maximum : 8 liens (limitation matérielle)
- Tous les liens :
  - ✅ Actifs simultanément
  - ✅ Load-balancing
  - ✅ Pas de blocage STP

**Pourquoi les autres réponses sont fausses :**
- A) Maximum 4 est insuffisant
- C) Maximum 16 dépasse limite
- D) Minimum 2 liens requis

---

### Question 16 - Réponse : B
**B) Tous les liens sont actifs, pas de blocage STP**

**Explication :**
- **Sans EtherChannel** :
  - STP bloque liens redondants → Bande passante perdue
  - 4×1G → Seul 1G utilisé
- **Avec EtherChannel** :
  - STP voit 1 lien logique
  - Tous liens physiques actifs
  - 4×1G → 4G utilisés
  - Load-balancing trafic

**Pourquoi les autres réponses sont fausses :**
- A) Latence n'est pas améliorée
- C) Vitesses doivent être identiques
- D) Configuration peut être complexe

---

### Question 17 - Réponse : B
**B) LACP**

**Explication :**
- **LACP (Link Aggregation Control Protocol)** :
  - Standard **IEEE 802.3ad**
  - ✅ Interopérable multi-vendor
  - Modes : active, passive
  - **Recommandé** pour interopérabilité
- **PAgP (Port Aggregation Protocol)** :
  - Cisco proprietary
  - ❌ Non interopérable
  - Modes : desirable, auto

**Pourquoi les autres réponses sont fausses :**
- A) PAgP est Cisco proprietary
- C) Mode On pas de protocole (fonctionne mais risqué)
- D) HSRP est pour redondance routeurs

---

### Question 18 - Réponse : C
**C) active, passive**

**Explication :**
- **LACP modes** :
  - **active** : Initie LACP (actif)
  - **passive** : Attend LACP (passif)
- Négociation :
  - active + active → ✅ EtherChannel
  - active + passive → ✅ EtherChannel
  - passive + passive → ❌ Échec

**Pourquoi les autres réponses sont fausses :**
- A) on/off ne sont pas modes LACP
- B) desirable/auto sont modes PAgP
- D) enable/disable ne sont pas modes LACP

---

### Question 19 - Réponse : B
**B) EtherChannel ne se forme pas (aucun switch n'initie)**

**Explication :**
- **passive** = Mode passif (attend)
- Switch A : passive (attend)
- Switch B : passive (attend)
- **Résultat** : Aucun n'initie → **Échec**

**Solution :**
```cisco
! Au moins UN switch doit être active
! Switch A
channel-group 1 mode active

! Switch B peut rester passive
channel-group 1 mode passive
```

**Pourquoi les autres réponses sont fausses :**
- A) Au moins 1 switch actif requis
- C) Pas err-disabled, juste pas de formation
- D) Pas de formation même après attente

---

### Question 20 - Réponse : D
**D) src-dst-ip**

**Explication :**
- **Load-balancing Layer 3switches/routers** :
  - **src-dst-ip** : ✅ Recommandé
  - Basé sur IP source + destination
  - Meilleur équilibrage
  - Hash(IP src XOR IP dst) → Modulo nb liens → Lien assigné

**Autres algorithmes :**
- src-mac / dst-mac : Simple mais déséquilibré
- **src-dst-mac** : ✅ Recommandé **Layer 2 switches**
- src-port / dst-port : Layer 4

**Pourquoi les autres réponses sont fausses :**
- A/B) src-mac/dst-mac déséquilibrés
- C) src-dst-mac pour Layer 2, pas Layer 3

---

### Question 21 - Réponse : B
**B) `port-channel load-balance src-dst-ip`**

**Explication :**
- Syntaxe : `port-channel load-balance <algorithm>`
- Configuration globale (tous EtherChannels)
- Algorithmes disponibles :
  - src-ip, dst-ip, **src-dst-ip**
  - src-mac, dst-mac, **src-dst-mac**
  - src-port, dst-port

**Configuration :**
```cisco
! Global
port-channel load-balance src-dst-ip

! Vérification
show etherchannel load-balance
```

**Pourquoi les autres réponses sont fausses :**
- A) `etherchannel` incorrect (c'est `port-channel`)
- C) Ordre mots inversé
- D) `channel-group` est pour config liens physiques

---

### Question 22 - Réponse : B
**B) Switched + Up (EtherChannel fonctionnel)**

**Explication :**
- **Codes flags Summary** :
  - **S** = Layer 2 (Switched)
  - **U** = Up (en service)
  - **P** = Port bundled (dans EtherChannel)
  - **D** = Down
  - **I** = Stand-alone (pas dans bundle)
- **(SU)** = ✅ **EtherChannel fonctionnel**

**Output exemple :**
```cisco
show etherchannel summary

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi0/1(P)    Gi0/2(P)    Gi0/3(P)    Gi0/4(P)
```

**Pourquoi les autres réponses sont fausses :**
- A) Suspended serait code différent
- C) Stand-alone = Code (I)
- D) Secure/Untagged pas liés à ce code

---

### Question 23 - Réponse : A
**A) Tous les liens doivent avoir le même speed, duplex, VLANs, mode**

**Explication :**
- **Prérequis EtherChannel (TOUS identiques)** :
  - ✅ **Speed** : 1G, 10G, etc. (même vitesse)
  - ✅ **Duplex** : full-duplex
  - ✅ **VLANs** :
    - Access : Même VLAN
    - Trunk : Mêmes Allowed VLANs, Native VLAN
  - ✅ **Mode** : Tous trunk OU tous access
  - ✅ **STP** : Même coût, priorité
- **Mismatch → err-disabled**

**Pourquoi les autres réponses sont fausses :**
- B) 2 liens minimum suffisent
- C) Modules identiques/différents OK
- D) LACP peut être activé (recommandé)

---

### Question 24 - Réponse : A
**A) Les Allowed VLANs sont différents sur les liens physiques**

**Explication :**
- **Trunk EtherChannel** : Prérequis
  - Même **Allowed VLANs** sur tous liens
  - Même **Native VLAN**
  - Même **Encapsulation** (dot1q)
- Mismatch → EtherChannel échoue

**Diagnostic :**
```cisco
show interfaces trunk

Port        Vlans allowed on trunk
Gi0/1       10,20,30      ← Cohérent
Gi0/2       10,20,30,40   ← MISMATCH !
```

**Solution :**
```cisco
interface range GigabitEthernet0/1-4
 switchport trunk allowed vlan 10,20,30
exit
```

**Pourquoi les autres réponses sont fausses :**
- B) Maximum 8 liens OK
- C) LACP supporté
- D) VTP mode n'affecte pas EtherChannel

---

### Question 25 - Réponse : B
**B) `show lacp neighbor`**

**Explication :**
- `show lacp neighbor` : Affiche voisins LACP
- Informations :
  - Port ID voisin
  - Device ID
  - Flags (Active/Passive, Slow/Fast)
  - Admin Key, Oper Key
  - Priorité port

**Output exemple :**
```cisco
show lacp neighbor

Flags:  S - Device is requesting Slow LACPDUs
        F - Device is requesting Fast LACPDUs
        A - Device is in Active mode
        P - Device is in Passive mode

Port      Neighbor             Age  Flags   Admin  Oper
          Port ID    Devid              Key    Key
Gi0/1     32769      0ce3.ba10      29s  SA   0x1   0x1
```

**Pourquoi les autres réponses sont fausses :**
- A) `show etherchannel neighbors` n'existe pas
- C) Syntaxe incorrecte
- D) Syntaxe incorrecte

---

## 📊 Tableau de scoring

| Score | Niveau | Appréciation |
|-------|--------|--------------|
| 23-25 | Excellent | Maîtrise parfaite Trunks & EtherChannel |
| 20-22 | Très bien | Bonne compréhension, réviser détails DTP/VTP |
| 17-19 | Bien | Compréhension correcte, approfondir load-balancing |
| 14-16 | Moyen | Réviser VTP revision et LACP modes |
| 11-13 | Insuffisant | Revoir cours complet, focus sur prérequis EtherChannel |
| 0-10 | Très insuffisant | Étude approfondie nécessaire |

---

**🎯 Seuil de réussite CCNP : 20/25 (80%)**

---

**📚 Fin du QCM - Module 5 : VLAN Trunks & EtherChannel**
