# Fiche Module 15 : Services IP
## Référence Rapide pour Révision

---

## TABLEAU RÉFÉRENCE RAPIDE NTP

| Commande | Objectif | Paramètres |
|----------|----------|-----------|
| `ntp server <IP>` | Configurer client NTP | IP serveur NTP |
| `ntp server <IP> prefer` | Serveur préféré | IP avec priorité |
| `ntp source <interface>` | Source NTP explicite | Interface physique/logique |
| `ntp master <stratum>` | Serveur NTP autonome | Stratum 2-15 (défaut 8) |
| `ntp peer <IP>` | Sync bidirectionnelle | IP du peer |
| `show ntp status` | État synchronisation | Affiche peer système, offset |
| `show ntp associations` | Associations actives | Détails delay, offset, reach |

---

## HIÉRARCHIE STRATUM NTP

```
STRATUM 0: Horloge Atomique / GPS (externe)
    ↓
STRATUM 1: Routeur avec source stratum 0
    ↓
STRATUM 2: Clients du routeur stratum 1
    ↓
STRATUM 3+: Chaînes de clients suivantes
    ↓
STRATUM 16: Non synchronisé / Inaccessible
```

**Caractéristiques clés:**
- Plus bas = plus précis et plus proche de la source atomique
- Stratum 1 = directement attaché à stratum 0
- Stratum 2+ = clients de niveaux inférieurs
- Convergence NTP: typiquement plusieurs **heures** pour atteindre précision
- Précision typique: **dizaines de millisecondes** (10-100 ms)

---

## TABLEAU COMPARATIF : HSRP vs VRRP vs GLBP

| Aspect | HSRP | VRRP | GLBP |
|--------|------|------|------|
| **Standard** | Propriétaire Cisco | RFC 3768 (Standard) | Propriétaire Cisco |
| **Fabricants** | Cisco uniquement | Multi-fournisseur | Cisco uniquement |
| **Architecture** | 1 Actif + Standby | 1 Master + Backup | 1 AVG + AVF (Multi-actif) |
| **Équilibrage** | Non (passif) | Non (passif) | **Oui (actif)** |
| **Groupes** | 0-255 (v1), 0-4095 (v2) | 1-255 | 1-255 |
| **MAC Virtuelle** | 0000.0c07.acXX | 0000.5e00.01XX | 0000.07acXX |
| **Détection défaillance** | Hellos multidiffusion | Hellos multidiffusion | Hellos multidiffusion |
| **Préemption** | Désactivée par défaut | Activée par défaut | Option configurable |

**Sélection:**
- **HSRP**: Infrastructure Cisco existante, besoin simple redondance
- **VRRP**: Environnement multi-fournisseur, standard requis
- **GLBP**: Besoin équilibrage charge + redondance simultanées

---

## EXAMPLES SYNTAXE OBJECT TRACKING

**Suivi de route:**
```
Router(config)# track 10 ip route 0.0.0.0/0 reachability
Router(config-if)# standby 1 track 10 decrement 30
```
→ Si route par défaut non accessible, abaisser priorité HSRP de 30 pts

**Suivi protocole ligne interface:**
```
Router(config)# track 20 interface GigabitEthernet0/0/1 line-protocol
Router(config-if)# standby 1 track 20 decrement 15
```
→ Si interface physique « down », abaisser priorité de 15 pts

**Vérification track:**
```
Router# show track 10
Track 10
  IP route 0.0.0.0/0 reachability
  Reachability is Up (connected via 192.168.1.1)
  1 change, last change 00:05:23
```

---

## CHECKLIST CONFIGURATION HSRP

- [ ] Définir interface physique avec IP propre
- [ ] Configurer groupe HSRP avec VIP: `standby <group> ip <VIP>`
- [ ] Définir priorité (> 100 si doit être actif): `standby <group> priority <value>`
- [ ] Activer préemption si failback automatique requis: `standby <group> preempt`
- [ ] Configurer timers si défaillance rapide requise: `standby <group> timers <hello> <hold>`
- [ ] Ajouter authentification si sécurité requise: `standby <group> authentication md5 key-string <password>`
- [ ] Configurer tracking si basculement sur conditions externes: `standby <group> track <object-num> decrement <value>`
- [ ] Vérifier synchronisation: `show standby brief`
- [ ] Tester basculement avec `int <iface>` puis `shutdown`

---

## DÉPANNAGE COURANT NTP/HSRP

| Problème | Cause Probable | Solution |
|---------|-----------------|----------|
| Appareil ne synchronise pas NTP | Serveur NTP inaccessible | Vérifier `ping` vers serveur NTP, `show ip route` |
| Offset NTP très grand (> 1s) | Horloge système très décalée | `debug ntp packet`, augmenter timeout |
| Basculement HSRP très lent (>30s) | Timers par défaut trop longs | Diminuer `hello time` et `hold time` |
| Les deux routeurs HSRP sont actifs | Priorité/adresse IP identiques | `show standby`, différencier priorités |
| HSRP ne bascule pas à redémarrage | Préemption désactivée | Ajouter `standby <group> preempt` |
| Clients ne rejoignent pas via VIP | Mauvaise VIP configurée | Vérifier `show standby`, confirmer VIP ≠ IP physique |

---

## CONFIGURATION NAT RAPIDE

**Configuration basique PAT (cas courant):**
```
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip nat inside

Router(config)# interface GigabitEthernet0/0/1
Router(config-if)# ip nat outside

Router(config)# ip access-list extended INTERNAL
Router(config-ext-nacl)# permit ip 192.168.1.0 0.0.0.255 any

Router(config)# ip nat inside source list INTERNAL interface GigabitEthernet0/0/1 overload
```

**Vérification:**
```
Router# show ip nat translations
Router# show ip nat statistics
Router# debug ip nat
```

---

## POINTS CLÉS POUR EXAMEN

1. **NTP Stratum**: Stratum 1 = directement atomique. Stratum 0 n'est pas un appareil physique.

2. **Convergence NTP**: Prend **heures/jours**, pas minutes. Précision = dizaines de ms.

3. **HSRP - Rôles**: 
   - Actif = transmet trafic VIP
   - Standby = écoute hellos, prêt à basculer
   - Utilisé par clients comme passerelle par défaut

4. **HSRP - Élection**: Priorité d'abord (défaut 100), adresse IP en tiebreaker

5. **Object Tracking**: Permet lier HSRP à conditions réseau externes (routes, interfaces)

6. **NAT Terminologie**:
   - Inside local = adresse privée réelle
   - Inside global = adresse publique traduite
   - PAT = partage une seule adresse publique avec port variation

7. **Timers HSRP** (défaut):
   - Hello: 3 secondes
   - Hold: 10 secondes (timeout)
   - Basculement typique: ~10 secondes

---

## TABLEAUX RAPIDES

**Adresses Multicast HSRP:**
- Groupe: 224.0.0.102
- Port: 1985/UDP

**Formats Adresse MAC Virtuelle:**
- HSRPv1: 0000.0c07.ac00-0000.0c07.acff
- HSRPv2: 0000.0c9f.f000-0000.0c9f.ffff

**Plages Stratum NTP:**
- 0: Atomique (source externe)
- 1-15: Valides pour synchronisation
- 16: Non synchronisé

---

*Fiche de révision rapide - Module 15 CCNP ENCOR*
