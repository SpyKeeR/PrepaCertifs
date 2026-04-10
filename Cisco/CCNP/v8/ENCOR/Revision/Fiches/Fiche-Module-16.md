# Fiche Module 16 : Tunnels Overlay
## Référence Rapide pour Révision

---

## TABLEAU COMPARATIF : GRE vs IPsec vs LISP vs VXLAN

| Aspect | GRE | IPsec | LISP | VXLAN |
|--------|-----|-------|------|-------|
| **Chiffrement** | Non | Oui | Non | Non |
| **Protocole interne** | Tout (IPv4/IPv6/autre) | IPv4/IPv6 | IPv4/IPv6 | Ethernet (L2) |
| **Complexité** | Simple | Haute (crypto) | Complexe | Modérée |
| **Cas d'usage** | Tunnel simple, multicast | VPN sécurisé, site-to-site | Mobilité, DC cloud | DC overlay, VLAN étendu |
| **Overhead** | ~24 octets | ~50-70 octets | Variable | 8 octets (UDP) |
| **Performance** | Haute (pas crypto) | Modérée (crypto intensive) | Haute | Modérée |
| **Fabrique unique** | Non (standard) | Non (RFC) | Cisco | Multi-fournisseur |

---

## CHECKLIST CONFIGURATION GRE

### Étapes obligatoires:
- [ ] **Étape 1**: `interface tunnel <number>` - créer interface
- [ ] **Étape 2**: `tunnel source {<IP> | <interface>}` - source du tunnel
- [ ] **Étape 3**: `tunnel destination <IP-distante>` - destination tunnel
- [ ] **Étape 4**: `ip address <IP-tunnel> <netmask>` - adresse tunnel

### Étapes optionnelles mais recommandées:
- [ ] **Étape 5**: `bandwidth <kbps>` - métrique routage (défaut hérite physique)
- [ ] **Étape 6**: `keepalive <seconds> <retries>` - défaillance rapide (défaut 10s, 3 retries)
- [ ] **Étape 7**: `ip mtu <mtu>` - prévenir fragmentation (1400 sûr)

### Dépannage:
- [ ] Vérifier source/dest tunnel routables: `ping` vers IP tunnel
- [ ] Vérifier interface up: `show interface tunnel <num>`
- [ ] Vérifier routes utilisent tunnel: `show ip route`
- [ ] Vérifier packet flow: `traceroute` à travers tunnel

---

## TÂCHES VÉRIFICATION GRE ET COMMANDES

| Tâche | Commande | Affiche |
|------|----------|---------|
| État tunnel | `show interface tunnel 0` | Statut physical/protocol, MTU, stats |
| Routes avec tunnel | `show ip route` | Routes avec tunnel comme interface sortie |
| Associated tunnel config | `show run interface tunnel 0` | Configuration tunnel complète |
| Conectivité tunnel | `ping 192.168.100.2` (autre côté) | Tunnel fonctionne si succès |
| Tracing packet path | `traceroute 192.168.1.0` | Montre hops vers dest tunnel + réseau cible |
| Debug tunnel packets | `debug tunnel` | Paquets tunnelisés détails (verbeux) |
| Problèmes récursion | `show ip route <dest-tunnel>` | Route ne doit pas utiliser tunnel lui-même |

---

## MATRICE SERVICES SÉCURITÉ IPSEC

| Service | AH | ESP | ESP+INT | Description |
|---------|----|----|---------|------------|
| **Authentification** | ✓ | ✗ | ✓ | Prouver identité pair |
| **Confidentialité** | ✗ | ✓ | ✓ | Chiffrer données |
| **Intégrité** | ✓ | ✗* | ✓ | Détect modification transit |
| **Anti-rejeu** | ✓ | ✓ | ✓ | Éviter duplication paquet |

*ESP sans HMAC n'offre pas authentification native, AH requiert pour ça.

---

## COMPARAISON ALGORITHMES DE CHIFFREMENT

| Algo | Taille Clé | Status | Recommandation | Raison |
|------|-----------|--------|-----------------|--------|
| **DES** | 56-bit | ❌ OBSOLÈTE | ÉVITER | Trop faible, cassable en heures |
| **3DES** | 168-bit | ⚠️ FAIBLE | TRANSITION | Lent, considéré faible maintenant |
| **AES-128** | 128-bit | ✅ ACCEPTABLE | POSSIBLE | Sûr pour beaucoup d'usages |
| **AES-256** | 256-bit | ✅✅ EXCELLENT | **RECOMMANDÉ** | Fort, future-proof, FIPS 197 |

**Choix pratique**: AES-256 pour tous les nouveaux déploiements.

---

## COMPARAISON ALGORITHMES DE HACHAGE

| Algo | Sortie | Status | Usage | Raison |
|------|--------|--------|-------|--------|
| **MD5** | 128-bit | ❌ OBSOLÈTE | ÉVITER | Collisions cryptographiques connues |
| **SHA-1** | 160-bit | ⚠️ FAIBLE | PHASE-OUT | Graduellement supplanté |
| **SHA-256** | 256-bit | ✅✅ EXCELLENT | **RECOMMANDÉ** | Standard moderne, robuste |
| **SHA-512** | 512-bit | ✅✅ EXCELLENT | OVERKILL | Très fort mais moins courant |

**Choix pratique**: SHA-256 pour aligner avec AES-256.

---

## RÉSUMÉ PHASES IKE

### IKEv1 (2 Phases)

**Phase 1: Authentification & Session Key Établissement**
- Deux pairs s'authentifier (PSK, RSA signatures, etc.)
- Estabelir une clé de session partagée (via Diffie-Hellman)
- Créer un IKE SA bidirectionnel
- Durée: quelques centaines de ms

**Phase 2: Négociation Transform Set**
- Aux pairs conviennent d'algorithms de chiffrement/hash (transform set)
- Créer IPsec SAs (généralement deux: inbound + outbound)
- Durée: quelques ms

### IKEv2 (Fusionné)
- Phases combinées, plus efficace
- Meilleur support mobilité (MOBIKE)
- Recommandé pour nouveaux déploiements

---

## COMBINAISONS TRANSFORM SET VALIDES

| Protocoles | Valid | Raison |
|-----------|-------|--------|
| **AH seul** | ✓ | Intégrité seulement, pas chiffrement |
| **ESP seul** | ✓ | Chiffrement + intégrité (STANDARD) |
| **3DES seulement** | ✓ | Historique, legacy |
| **AES-256 + SHA-256 (ESP)** | ✓ | **RECOMMANDÉ** moderne |
| **AH + ESP** | ✓ | Double protection (rarement utile car ESP=suffisant) |

**Cas courant ENCOR**: AES-256 + SHA-256 ESP Tunnel Mode.

---

## DÉPANNAGE RÉSEAUX OVERLAY

| Problème | Cause Probable | Solution |
|---------|-----------------|----------|
| Tunnel UP mais pas data | Transform set incompatible | Vérifier SAs créés: `show crypto ipsec sa` |
| Routage récursif GRE | Dest tunnel publicisée dans tunnel | Ajouter route statique pour dest via interface physique |
| Tunnel flapping (up/down) | MTU trop grand, paquets fragmentés | Réduire `ip mtu` à 1400 or less |
| IPsec tunnel refusé | IKE phase 1 échoue | Vérifier PSK identiques, algorithmes négociables |
| Latency travers tunnel | Overloaded tunnel, pas de QoS | Configurer `bandwidth` tunnel, appliquer QoS |
| Trafic bypass tunnel | ACL ou routing prioritisant autre chemin | Vérifier routes, ACLs, priorités protocole routage |

---

## MODE TUNNEL VS TRANSPORT

| Aspect | Tunnel Mode | Transport Mode |
|--------|-------------|-----------------|
| **En-tête IP** | Encapsulé & encrypted | Original visible |
| **Cas d'usage** | VPN site-to-site (STANDARD) | Host-to-host VPN |
| **Sécurité intra** | Masquée au réseau externe | Visible |
| **Overhead** | Plus grand (nouvel IP header) | Petit |
| **Déploiement** | Courant en VPN production | Rarement vu |

**Pour ENCOR**: Tunnel mode = standard pour tous les VPN site-to-site.

---

## POINTS CLÉS POUR EXAMEN

1. **GRE Recursion**: Route vers dest tunnel doit utiliser interface physique, pas tunnel lui-même.

2. **Transform Sets**: AES-256 + SHA-256 est le combo recommandé, ESP mode tunnel.

3. **IKE Phases**: IKEv1 = 2 phases (auth, negotiate crypto). IKEv2 = fusionné, meilleur.

4. **IPsec Services**: Auth (identité), Confidentiality (chiffrement), Integrity (hachage), Anti-replay.

5. **Modes**: Tunnel = VPN site-to-site standard. Transport = rarement vu, host-to-host.

6. **Algoritmes Obsolètes**: DES, 3DES, MD5 tous en phase-out ou obsolètes.

7. **GRE Config**: 7 étapes, 4 obligatoires (source, dest, IP, interface).

---

## TABLEAUX RAPIDES

**Configuration GRE Minimale:**
```
interface tunnel 0
 tunnel source 203.0.113.10
 tunnel destination 203.0.113.20
 ip address 192.168.100.1 255.255.255.0
```

**Vérification GRE:**
```
show interface tunnel 0
show ip route
ping 192.168.100.2
```

**IPsec Protocol Numbers:**
- IP Protocol 50 = ESP
- IP Protocol 51 = AH
- UDP Port 500 = IKE
- UDP Port 4500 = IKE (NAT-T)

---

*Fiche de révision rapide - Module 16 CCNP ENCOR*
