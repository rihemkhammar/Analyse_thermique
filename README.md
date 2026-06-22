# 🌡️ Analyse Thermique — Grille 8×5×3

Modélisation et prédiction de la distribution de température dans une grille 3D de capteurs thermocouple, avec machine learning (XGBoost) et visualisation interactive (Plotly).

---

## 📁 Structure du projet

```
.
├── NOTEBOOK_THERMIQUE_8_5_3_final.ipynb   # Notebook principal (pipeline complet)
├── ThermoCouple.csv                        # Données brutes — 120 capteurs thermocouple
├── temperature.csv   # Données brutes — 254 capteurs tension
└── README.md
```

---

## 🧱 Description

Le projet analyse la distribution thermique d'un espace physique via une **grille 8 colonnes × 5 rangées × 3 hauteurs** (120 capteurs actifs), en combinant :

- **Parsing robuste** des positions capteurs avec regex + fallback automatique
- **Nettoyage des données** : suppression des valeurs physiquement impossibles (< -50°C ou > 200°C)
- **Feature engineering CVC** : distances aux bouches de chauffage et climatisation
- **Modèle XGBoost** pour la prédiction de température en tout point de la grille
- **Visualisation 3D interactive** avec Plotly

---

## 📊 Données

| Fichier | Capteurs | Colonnes | Type |
|--------|----------|----------|------|
| `ThermoCouple.csv` | 120 | 122 (Row, Time + 120 temp.) | Thermocouple (°C) |
| `temperature.csv` | 254 | 256 (Row, Time + 254 temp.) | Tension (Voltage) |

---

## ⚙️ Pipeline (étapes du notebook)

| Étape | Description |
|-------|-------------|
| 0 | Installation des dépendances |
| 1 | Upload & chargement des CSVs |
| 2 | Parsing des positions (regex + fallback) |
| 3 | Nettoyage : valeurs hors limites physiques |
| 4 | Feature engineering (grille + distances CVC) |
| 5 | Entraînement XGBoost |
| 6 | Évaluation du modèle (RMSE, MAE, R²) |
| 7 | Visualisation 3D Plotly (heatmap volumique) |

---

## 🚀 Lancement

### Option A — Google Colab (recommandé)

1. Ouvrir `NOTEBOOK_THERMIQUE_8_5_3_final.ipynb` dans [Google Colab](https://colab.research.google.com/)
2. Uploader les deux fichiers CSV via la cellule d'upload (Étape 1)
3. Exécuter toutes les cellules (`Runtime > Run all`)

### Option B — Environnement local

```bash
# Cloner le repo
git clone https://github.com/<votre-username>/<votre-repo>.git](https://github.com/rihemkhammar/Analyse_thermique.git
cd Analyse_thermique

# Installer les dépendances
pip install xgboost scikit-learn pandas numpy matplotlib seaborn plotly scipy

# Lancer Jupyter
jupyter notebook NOTEBOOK_THERMIQUE_8_5_3_final.ipynb
```

> ⚠️ Commenter la cellule `from google.colab import files` avant de lancer en local.

---

## 🔧 Paramètres configurables

Dans la cellule **Paramétrage du système** :

```python
LARGEUR  = 8    # colonnes A–H
LONGUEUR = 5    # rangées 0–4
HAUTEUR  = 3    # niveaux H1–H3

T_MIN_PHYSIQUE = -50    # seuil bas de validité (°C)
T_MAX_PHYSIQUE = 200    # seuil haut de validité (°C)

SOURCES_FROID = [(0, 0), (7, 4)]   # bouches climatisation (x, y)
SOURCES_CHAUD = [(3, 2), (4, 2)]   # bouches chauffage (x, y)
```

---

## 📦 Dépendances

```
pandas
numpy
matplotlib
seaborn
plotly
scikit-learn
xgboost
scipy
```

---

## 📝 Notes

- La grille utilise **120 capteurs sur 254 disponibles** — les capteurs hors limites physiques sont automatiquement exclus.
- Le parser de position gère les lignes mal alignées dans le CSV via un fallback regex.
- Les visualisations 3D sont interactives (rotation, zoom) grâce à Plotly.
