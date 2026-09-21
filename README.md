# 📊 Dashboard Eurostat · Distribution des revenus en Europe

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/fr/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/fr/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/fr/docs/Web/JavaScript)
[![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chart.js&logoColor=white)](https://www.chartjs.org/)
[![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=for-the-badge&logo=leaflet&logoColor=white)](https://leafletjs.com/)
[![Eurostat](https://img.shields.io/badge/Source-Eurostat-003399?style=for-the-badge)](https://ec.europa.eu/eurostat)
[![JSON-stat](https://img.shields.io/badge/Format-JSON--stat%202.0-blue?style=for-the-badge)](https://json-stat.org/)
[![License MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Stable-brightgreen?style=for-the-badge)]()
[![No API Key](https://img.shields.io/badge/API%20Key-Not%20Required-success?style=for-the-badge)]()
[![Made in France](https://img.shields.io/badge/Made%20in-France-0055A4?style=for-the-badge)]()

> **Dashboard interactif** exploitant intégralement le dataset Eurostat `ILC_DI01` — distribution des revenus, inégalités et seuils par quantile, dans 30+ pays européens, sur 30 ans (1995–2024).

---

## 📖 Table des matières

- [Aperçu](#-aperçu)
- [Fonctionnalités](#-fonctionnalités)
- [Démarrage rapide](#-démarrage-rapide)
- [Structure des fichiers](#-structure-des-fichiers)
- [Source de données](#-source-de-données)
- [Architecture technique](#-architecture-technique)
- [API console](#-api-console)
- [Indicateurs disponibles](#-indicateurs-disponibles)
- [Robustesse et fallbacks](#-robustesse-et-fallbacks)
- [Compatibilité](#-compatibilité)
- [Feuille de route](#-feuille-de-route)
- [Contribution](#-contribution)
- [Licence](#-licence)
- [Remerciements](#-remerciements)

---

## 🎯 Aperçu

Ce dashboard transforme le fichier brut `estat_ilc_di01_en.json` d'Eurostat (format JSON-stat 2.0, 6 dimensions, plusieurs milliers de points) en **8 vues analytiques interactives**, sans aucune dépendance backend.

**Aucune clé API requise.** Tout fonctionne en local, dans un simple navigateur.

| Caractéristique | Valeur |
|---|---|
| 📁 Fichiers | 2 (`dashboard.html` + `estat_ilc_di01_en.json`) |
| 🔌 Dépendances | Chart.js 4.4, Leaflet 1.9 (CDN) |
| 🌐 Connexion | Uniquement pour les tuiles OpenStreetMap |
| 🎨 Design | Responsive, palette sobre, code couleur sémantique |
| ⚡ Performance | Chargement complet en moins de 2 s |
| 🌍 Langue | Interface en français |

---

## ✨ Fonctionnalités

### 8 onglets analytiques

| Onglet | Description |
|---|---|
| 📊 **Revenus** | Gini, S80/S20, P90/P10, médiane, moyenne — coupe transversale et évolution |
| 💰 **Seuils** | Seuils `TC` Q1–Q4 et D1–D9 en EUR / PPS / NAC |
| 📈 **Distribution** | Courbe de Lorenz, parts par décile, parts cumulées |
| 🗺️ **Carte** | Choroplèthe interactive des indicateurs (sans clé API) |
| 📚 **Catalogue** | Inventaire exhaustif des combinaisons `statinfo × unit × quant_inc` |
| 📉 **Convergence** | Analyse σ-convergence UE27 / UE15 / zone euro sur 30 ans |
| 🏚️ **Pauvreté** | Indicateurs adaptatifs (AROP/AROPE si présents, sinon inégalité) |
| 🔍 **Explorateur** | Requête libre sur n'importe quelle dimension du dataset |

### Capacités analytiques

- ✅ **Décodage complet** des 6 dimensions (`freq`, `unit`, `statinfo`, `quant_inc`, `geo`, `time`)
- ✅ **Fallbacks automatiques** : si un indicateur officiel manque, recalcul depuis `SHARE`
- ✅ **Sources explicites** : chaque KPI indique « Eurostat » ou « recalculé »
- ✅ **σ-convergence** avec trajectoires individuelles normalisées
- ✅ **Trajectoires interactives** de 40+ pays sur 30 ans
- ✅ **Export CSV** du catalogue complet
- ✅ **API console** `window.EXPLORE` pour analyses avancées

---

## 🚀 Démarrage rapide

### Prérequis

- Un navigateur moderne (Chrome 90+, Firefox 88+, Edge 90+, Safari 14+)
- Python, Node.js ou tout autre serveur HTTP local *(le protocole `file://` peut bloquer les fetch)*

### Installation

1. Cloner le dépôt :
   git clone https://github.com/votre-utilisateur/dashboard-eurostat-ilc-di01.git

2. Télécharger le dataset Eurostat :
   curl "https://ec.europa.eu/eurostat/api/dissemination/statistics/1.0/data/ilc_di01?format=JSON&lang=EN" -o estat_ilc_di01_en.json

3. Lancer un serveur local :
   python -m http.server 8000

4. Ouvrir dans le navigateur : http://localhost:8000/dashboard.html

### Ouverture directe

Sans serveur local :

- Linux / macOS : `open dashboard.html`
- Windows : `start dashboard.html`

---

## 📂 Structure des fichiers

dashboard-eurostat-ilc-di01/
├── dashboard.html
├── estat_ilc_di01_en.json
├── README.md
├── LICENSE
└── docs/
    └── screenshots/

Le dashboard est **mono-fichier** : tout le CSS et le JavaScript sont inline. Aucune compilation, aucun bundler.

---

## 📊 Source de données

### Dataset `ILC_DI01`

- **Nom officiel** : Distribution of income by quantiles — EU-SILC and ECHP surveys
- **Producteur** : [Eurostat](https://ec.europa.eu/eurostat)
- **URL** : [https://ec.europa.eu/eurostat/databrowser/view/ilc_di01](https://ec.europa.eu/eurostat/databrowser/view/ilc_di01)
- **Format** : JSON-stat 2.0
- **Période** : 1995 → 2024
- **Couverture** : ~40 entités (pays UE + AELE + candidats + agrégats UE/EA)

### Les 6 dimensions

| Dimension | Codes | Description |
|---|---|---|
| `freq` | `A` | Fréquence (annuelle) |
| `unit` | `EUR`, `NAC`, `PPS`, `PC` | Unité monétaire |
| `statinfo` | `SHARE`, `TC`, `MED_E`, `MEAN_E`, `GINI`, `S80S20`, `P90P10`, … | Type d'indicateur |
| `quant_inc` | `D1`–`D10`, `QU1`–`QU5`, `Q1`–`Q4`, `MED`, `MEAN`, `TOTAL` | Quantile / statistique |
| `geo` | `AT`, `BE`, …, `EU27_2020`, `EA20` | Pays ou agrégat |
| `time` | `1995`–`2024` | Année |

### Téléchargement

curl "https://ec.europa.eu/eurostat/api/dissemination/statistics/1.0/data/ilc_di01?format=JSON&lang=EN" -o estat_ilc_di01_en.json

Ou via le databrowser : [https://ec.europa.eu/eurostat/databrowser/view/ilc_di01/default/table](https://ec.europa.eu/eurostat/databrowser/view/ilc_di01/default/table)

---

## 🏗️ Architecture technique

### Flux de données

estat_ilc_di01_en.json  (JSON-stat 2.0)
          │
          ▼
   Décodage index plat → coordonnées 6D
          │
          ▼
   data[freq][unit][statinfo][quant_inc][geo][time] = value
          │
          ▼
   Helpers robustes (findUnit, getGini, getS80S20, …)
          │
          ▼
   Fallback automatique (officiel > recalculé > null)
          │
          ▼
   8 vues Chart.js / Leaflet

### Stack technique

| Couche | Technologie |
|---|---|
| **UI** | HTML5 + CSS3 (grid, custom properties) |
| **Graphiques** | [Chart.js 4.4](https://www.chartjs.org/) |
| **Cartographie** | [Leaflet 1.9](https://leafletjs.com/) + OpenStreetMap |
| **Données** | JSON-stat 2.0 (fetch natif) |
| **Langage** | JavaScript ES2020 (async/await, optional chaining) |

---

## 🧰 API console

Une fois le dashboard chargé, une API globale `window.EXPLORE` est disponible :

EXPLORE.inventaire()
EXPLORE.getGini("FR", "2022")
EXPLORE.getS80S20("FR", "2022")
EXPLORE.getDeciles("FR", "2022")
EXPLORE.serie("GINI", "TOTAL", "TOTAL", "FR")
EXPLORE.exportCSV(EXPLORE.inventaire(), "inventaire.csv")

---

## 📐 Indicateurs disponibles

### Officiels (dans le dataset)

| Code | Description | Recommandé pour |
|---|---|---|
| `GINI` | Coefficient de Gini | Inégalité globale |
| `S80S20` | Ratio 5ᵉ quintile / 1ᵉʳ quintile | Inégalité extrême |
| `P90P10` | Ratio interdécile | Inégalité extrême |
| `P90P50` | Ratio haut de distribution | Inégalité supérieure |
| `P50P10` | Ratio bas de distribution | Inégalité inférieure |
| `AROP` | Taux de risque de pauvreté | Pauvreté monétaire |
| `MED_E` | Médiane du revenu | Niveau de vie |
| `MEAN_E` | Moyenne du revenu | Niveau de vie moyen |

### Recalculés (fallback depuis `SHARE`)

| Indicateur | Formule |
|---|---|
| Gini | Formule de Brown depuis parts déciles |
| S80/S20 | `SHARE.QU5 / SHARE.QU1` |
| P90/P10 | `SHARE.D9 / SHARE.D1` |
| P90/P50 | `SHARE.D9 / SHARE.D5` |
| P50/P10 | `SHARE.D5 / SHARE.D1` |

---

## 🛡️ Robustesse et fallbacks

| Situation | Comportement |
|---|---|
| `GINI` absent du fichier | Recalcul depuis `SHARE.D1`–`D10` |
| `S80S20` absent | Recalcul depuis `SHARE.QU5 / SHARE.QU1` |
| `P90P10` absent | Recalcul depuis `SHARE.D9 / SHARE.D1` |
| `AROP` absent | Sélecteur bascule sur les indicateurs disponibles |
| `unit:"TOTAL"` inexistant | `findUnit()` parcourt toutes les unités |
| Année manquante pour un pays | Message d'erreur avec années disponibles |
| GeoJSON Europe indisponible | Fallback en cercles proportionnels |
| Tuiles CARTO refusées | Utilisation d'OSM standard |

---

## 💻 Compatibilité

| Navigateur | Version minimale | Statut |
|---|---|---|
| Chrome / Edge | 90+ | ✅ Testé |
| Firefox | 88+ | ✅ Testé |
| Safari | 14+ | ✅ Testé |
| Opera | 76+ | ✅ Compatible |
| IE 11 | — | ❌ Non supporté |

**Prérequis techniques** : ES2020, `fetch`, `async/await`, optional chaining (`?.`), nullish coalescing (`??`), CSS Grid, CSS Custom Properties.

---

## 🗺️ Feuille de route

- [x] Décodage exhaustif du dataset
- [x] 8 vues analytiques
- [x] Fallbacks automatiques
- [x] Carte sans clé API
- [x] API console `window.EXPLORE`
- [x] Export CSV
- [ ] Export PNG des graphiques
- [ ] Comparaison multi-pays côte à côte
- [ ] Heatmap pays × années interactive
- [ ] Intégration d'autres datasets (`ILC_LI02`, `TESPM010`)
- [ ] Internationalisation (EN, ES, DE)
- [ ] Mode impression / PDF
- [ ] Tests unitaires (Vitest)
- [ ] Build PWA (offline)

---

## 🤝 Contribution

Les contributions sont bienvenues !

git checkout -b feature/heatmap-pays-annees
git commit -m "feat: ajout heatmap pays × années"
git push origin feature/heatmap-pays-annees

### Conventions

- **Commits** : [Conventional Commits](https://www.conventionalcommits.org/)
- **Style JS** : 2 espaces, point-virgules, `const`/`let` uniquement
- **Nommage** : camelCase pour les variables, UPPER_SNAKE pour les constantes
- **Commentaires** : en français, avec sections délimitées par `// ===`

---

## 📄 Licence

Ce projet est distribué sous licence **MIT**. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

MIT License

Copyright (c) 2025 [Votre nom]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 🙏 Remerciements

- **[Eurostat](https://ec.europa.eu/eurostat)** pour la mise à disposition ouverte des données `ILC_DI01`
- **[Chart.js](https://www.chartjs.org/)** pour la bibliothèque de graphiques
- **[Leaflet](https://leafletjs.com/)** pour la cartographie interactive
- **[OpenStreetMap](https://www.openstreetmap.org/)** pour les tuiles cartographiques
- **[JSON-stat](https://json-stat.org/)** pour le standard de données statistiques

---

<div align="center">

**⭐ Si ce projet vous est utile, n'hésitez pas à lui donner une étoile !**

[🔝 Retour en haut](#-dashboard-eurostat--distribution-des-revenus-en-europe)

*Dernière mise à jour : 2025*

</div>
