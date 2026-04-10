# Fiche Module 18 : Infrastructure Wireless
## Référence Rapide pour Révision

---

## TABLEAU COMPARATIF TOPOLOGIES WIRELESS

| Aspect | Autonomous | Lightweight Centralisé | Embedded | Mobilité Express |
|--------|-----------|-------|----------|------------------|
| **Déploiement** | Simple, indépendant | Dépend WLC | WLC dans switch | AP+WLC par site |
| **Scalabilité** | < 10 APs max | 1000+ APs par WLC | 100-200 APs | 50-100 APs |
| **WLC** | Aucun | Dédié requis | Embarqué | Embarqué dans AP |
| **Management** | Par-AP config | Centralisé (WLC) | Centralisé | Distribué multi-site |
| **Data Path** | Direct trafic | Tunnelisé CAPWAP | Tunnelisé local | Tunnelisé |
| **Roaming Client** | Re-auth required | Transparent (WLC) | Transparent | Transparent |
| **Latence** | Basse | Modérée (tunnel) | Basse | Basse locale |
| **Coût** | Bas/AP | Haut (WLC) | Modéré | Modéré/site |
| **Cas d'usage** | PME, bureaux fins | Entreprise, campus | Succursales | Multi-site espaces |

---

## TABLEAU COMPARATIF MODES AP

| Mode | Nature | Configuration | Dépendance | Roaming |
|------|--------|---------------|-----------|---------|
| **Autonomous** | Indépendant, auto-suffisant | Locale sur AP | Aucune | Non (re-auth) |
| **Lightweight** | Dépendant WLC | WLC→ centralisé | WLC critique | Oui (transparent) |

---

## MACHINE À ÉTATS AP : PROCESSUS BOOT

```
1. AP BOOT
   └─ Charge IOS de base (~5-10 MB)
      └─ Démarre interfaces réseau
      
2. DHCP / AUTO-CONFIG
   └─ Établit adresse IP (DHCP ou statique)
      └─ Envoie DHCP Option 43 ou DNS
      
3. WLC DISCOVERY
   └─ Cherche WLC préféré (DHCP → DNS → Multicast)
      └─ Identifie adresse IP WLC
      
4. CAPWAP TUNNEL
   └─ Initie connexion UDP vers WLC:5246
      └─ Échange certificats DTLS (encryption)
      └─ Tunnel sécurisé établi
      
5. JOIN REQUEST
   └─ Envoie capacités AP (modèle, radios, etc)
      └─ WLC vérifie et accept/reject
      
6. IMAGE DOWNLOAD (si requis)
   └─ Vérifie version IOS match WLC
      └─ Telecharge image - reboote - retour Étape 3
      
7. CONFIG DOWNLOAD
   └─ WLC envoie bloc configuration
      └─ SSID, sécurité, canaux, puissance
      └─ AP prêt à servir clients
```

---

## CAPWAP TUNNEL OVERVIEW

| Aspect | Détail |
|--------|--------|
| **Fonction** | Sécurisé AP ↔ WLC communication |
| **Couche** | L3 (IP UDP) |
| **Port WLC** | UDP 5246 (Control), 5247 (Data) |
| **Encryption** | DTLS (Datagram TLS) certificats |
| **Trafic** | Control (config) + Data (client) |
| **Direction** | Bidirectional (control), Data AP→WLC |

---

## LATENCE RTT REQUIREMENT

| Métrique | Spécification | Impact |
|----------|---------------|--------|
| **Max RTT** | < 100 ms | Cisco standard |
| **Dépasse 100ms** | ⚠️ Non supporté officially | Roaming+ peuvent échouer |
| **Real-world** | Typique 10-30 ms | Intra-campus |
| **Considération** | Metro area RTT peut être borderline | Plan réseau accordingly |

---

## SÉQUENCE AP BOOT DÉTAIL

**Ordre découverte WLC** (Cisco):
1. DHCP Option 43 (serveur DHCP fournit WLC IP)
2. DNS query `cisco-capwap-controller.local`
3. IP Helper (switch forward broadcast)
4. Multicast 224.0.1.44 (CAPWAP discovery)
5. Configuration manuelle (console ou config file)

---

## CHECKLIST DÉPLOIEMENT LIGHTWEIGHT AP

- [ ] **Réseau Switch**: Port d'accès L2, PoE activé
- [ ] **DHCP Server**: Configuré pour subnet AP  
- [ ] **DHCP Option 43**: Configure (Format Cisco: `F104.WLC.IP.Address`)
- [ ] **DNS**: Configurer `cisco-capwap-controller` record
- [ ] **WLC**: Prêt à accepter APs (licences OK)
- [ ] **Firewall**: UDP 5246/5247 ouvert AP↔WLC
- [ ] **Network Latency**: Vérifier RTT < 100ms
- [ ] **Power**: PoE 30W+ suffisant pour AP
- [ ] **Boot First AP**: Confirmez Discovery/Join
- [ ] **Image Match**: WLC image téléchargement si version dépareillée
- [ ] **Config Received**: AP affiche SSID → clients peuvent connecter

---

## TYPES D'ANTENNES

| Type | Couverture | Distance | Utilisation |
|------|-----------|----------|------------|
| **Omnidirectionnelle** | 360° sphérique | 50-80m (2.4 GHz) | AP plafond couverture générale |
| **Directionnelle (Patch)** | Forcée direction | 100+ m (point-to-pt) | Corridors, longs couloirs |
| **MIMO** | Diversité multiple | Normal | 802.11n/ac/ax clients |

---

## PLANIFICATION DENSITÉ AP

| Bande | Portée Intérieur | Overlap Recommandé | Espacement Approx |
|-------|-----------------|-------------------|-----------------|
| **2.4 GHz** | 50-80m | 20-30% | ~25m |
| **5 GHz** | 30-50m | 20-30% | ~15m |

**Calcul**: Portée avec 20% chevauchement = ~0.8× portée max

---

## POINTS CLÉS POUR EXAMEN

1. **Autonomous**: Indépendant, pas de WLC. Max ~10 APs.

2. **Lightweight + Centralisé**: WLC point unique. Scalable mille+ APs. RTT < 100ms.

3. **Embedded**: WLC dans switch, 100-200 APs. Compromis coût.

4. **Mobilité Express**: Un AP+WLC par site. Permet multi-site sans WLC central.

5. **AP Boot Séquence**: DHCP → Discovery → CAPWAP → Join → Image DL → Config.

6. **CAPWAP**: Tunnel UDP secure (DTLS). Control + Data planes.

7. **Roaming**: Autonomous = non-transparent. Lightweight = transparent (WLC gère).

8. **Antennes**: Omnidirectional (coverage). Directional (distance/point-to-point).

---

## TABLEAU RAPIDE : TOPOLOGIE PAR CONTEXTE

| Contexte | Topologie |
|---------|----------|
| **1-2 petits offices** | Autonomous |
| **1 bâtiment campus** | Centralisé |
| **Succursale unique** | Embedded |
| **Multi-site sans WLC central** | Mobilité Express |
| **Enterprise 1000+ APs** | Centralisé (WLC en haute dispo) |

---

*Fiche de révision rapide - Module 18 CCNP ENCOR*
