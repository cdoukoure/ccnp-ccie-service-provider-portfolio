# Backbone IP – Operator Network Fundamentals

## 🎯 Objectif du projet

Ce projet démontre une **maîtrise solide des fondamentaux réseaux opérateur** requis pour les certifications **CCNP Service Provider** et **CCIE Service Provider**. Il couvre les protocoles de base, leur rôle en environnement ISP, et leur mise en œuvre pratique dans un lab reproductible, servant de base aux architectures MPLS et EVPN.

---

## 🧠 Compétences démontrées

* Architecture réseau opérateur (ISP / Backbone)
* Compréhension L2/L3 avancée
* IGP (OSPF, IS-IS) niveau opérateur
* MPLS fundamentals
* Haute disponibilité & résilience
* Méthodologie CCIE (design → config → validation)

---

## 🗺️ Architecture du lab

### Topologie logique

```
CE1 ---- PE1 ---- P1 ---- PE2 ---- CE2
           |       |
           |       +---- P2
           |
           +---- RR (Route Reflector)
```

### Rôles des équipements

| Équipement | Rôle                   |
| ---------- | ---------------------- |
| CE         | Customer Edge (client) |
| PE         | Provider Edge          |
| P          | Provider Core          |
| RR         | Route Reflector        |

---

## 📦 Technologies couvertes

### 1️⃣ IPv4 / IPv6

* Plan d’adressage hiérarchique
* Loopbacks pour le control-plane
* Dual-stack ready

### 2️⃣ OSPF vs IS-IS (niveau opérateur)

| Critère       | OSPF  | IS-IS      |
| ------------- | ----- | ---------- |
| Usage ISP     | Moyen | ⭐⭐⭐⭐⭐      |
| Scalabilité   | Bonne | Excellente |
| MPLS-friendly | Oui   | ⭐⭐⭐⭐⭐      |

➡️ **Choix du lab : IS-IS (Level-2 only)**

### 3️⃣ BGP Fundamentals

* eBGP CE–PE
* iBGP PE–PE
* Route Reflector
* Attributs clés :

  * Local-Preference
  * MED
  * Communities

### 4️⃣ MPLS – Bases opérateur

* MPLS Label Imposition
* LDP vs RSVP (introduction)
* PHP (Penultimate Hop Popping)

### 5️⃣ Haute disponibilité

* ECMP
* Fast Reroute (concept)
* IGP convergence

---

## ⚙️ Configurations clés (extraits)

### IS-IS – Core Provider

```cisco
router isis CORE
 is-type level-2-only
 net 49.0001.0000.0000.0001.00
 metric-style wide
 passive-interface Loopback0
 mpls ldp autoconfig
```

### MPLS Global

```cisco
mpls label protocol ldp
mpls ldp router-id Loopback0 force
```

### BGP – PE

```cisco
router bgp 65000
 bgp log-neighbor-changes
 neighbor 10.0.0.2 remote-as 65000
 neighbor 10.0.0.2 update-source Loopback0
 address-family ipv4
  neighbor 10.0.0.2 activate
```

---

## 🧪 Scénarios de tests

### Test 1 – Convergence IGP

* Shutdown lien P–PE
* Mesure convergence IS-IS

### Test 2 – MPLS Forwarding

```bash
show mpls forwarding-table
```

### Test 3 – BGP Path Selection

* Modification Local-Pref
* Vérification best-path

---

## 📊 Résultats attendus

* Ping CE1 ↔ CE2 via MPLS
* Labels visibles dans le core
* Aucun route client dans le core (clean core)

---

## 🧱 Bonnes pratiques opérateur

* Loopbacks systématiques
* Core sans routes client
* IGP minimaliste
* BGP pour la politique

---

## 📁 Structure du dossier

```
01-operator-fundamentals/
├── diagrams/
├── configs/
│   ├── PE1.cfg
│   ├── PE2.cfg
│   ├── P1.cfg
│   └── RR.cfg
├── tests/
│   └── validation.md
└── README.md
```

---

## 🚀 Niveau CCIE – Ce que ce projet prouve

✅ Vision opérateur
✅ Séparation control / data plane
✅ MPLS-ready mindset
✅ Méthode de troubleshooting

---

## 🔜 Évolution du portfolio

➡️ Projet 02 : **MPLS L3VPN avancé**
➡️ Projet 03 : **Segment Routing MPLS**
➡️ Projet 04 : **EVPN MPLS & VXLAN**


