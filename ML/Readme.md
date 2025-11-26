# Rapport d'Analyse - Dataset Wine Quality

## 📊 Vue d'Ensemble

**Source:** UCI Machine Learning Repository  
**ID Dataset:** 186  
**Date de donation:** 6 octobre 2009  
**DOI:** 10.24432/C56S3T  
**Licence:** Creative Commons Attribution 4.0 International (CC BY 4.0)

## 🍷 Description du Dataset

Ce dataset contient deux ensembles de données relatifs aux vins rouge et blanc de la variété **"Vinho Verde"** portugais, provenant du nord du Portugal. L'objectif principal est de modéliser la qualité du vin en fonction de tests physicochimiques.

### Caractéristiques Principales

- **Type de données:** Multivariées
- **Domaine:** Business
- **Tâches associées:** Classification, Régression
- **Type de features:** Réel (valeurs continues)
- **Nombre d'instances:** 4 898
- **Nombre de features:** 11 variables d'entrée + 1 variable cible
- **Valeurs manquantes:** Non

## 📁 Fichiers Disponibles

| Fichier | Taille | Description |
|---------|--------|-------------|
| `winequality-white.csv` | 258.2 KB | Données des vins blancs |
| `winequality-red.csv` | 82.2 KB | Données des vins rouges |
| `winequality.names` | 3.2 KB | Documentation du dataset |
| **Archive complète** | **89.2 KB** | Téléchargement ZIP |

## 🔬 Variables du Dataset

### Variables d'Entrée (Features)

Toutes les variables suivantes sont basées sur des tests physicochimiques :

| # | Variable | Type | Description |
|---|----------|------|-------------|
| 1 | `fixed_acidity` | Continue | Acidité fixe |
| 2 | `volatile_acidity` | Continue | Acidité volatile |
| 3 | `citric_acid` | Continue | Acide citrique |
| 4 | `residual_sugar` | Continue | Sucre résiduel |
| 5 | `chlorides` | Continue | Chlorures |
| 6 | `free_sulfur_dioxide` | Continue | Dioxyde de soufre libre |
| 7 | `total_sulfur_dioxide` | Continue | Dioxyde de soufre total |
| 8 | `density` | Continue | Densité |
| 9 | `pH` | Continue | pH |
| 10 | `sulphates` | Continue | Sulfates |
| 11 | `alcohol` | Continue | Taux d'alcool |

### Variable de Sortie (Target)

| Variable | Type | Description | Échelle |
|----------|------|-------------|---------|
| `quality` | Continue/Ordinale | Score de qualité basé sur des données sensorielles | 0 à 10 |

## 🎯 Objectifs et Applications

### Objectifs Principaux

1. **Prédiction de la qualité:** Modéliser la qualité du vin à partir des propriétés physicochimiques
2. **Classification:** Catégoriser les vins selon leur niveau de qualité
3. **Régression:** Prédire le score exact de qualité

### Cas d'Usage Potentiels

- **Contrôle qualité:** Évaluation rapide de la qualité sans dégustation
- **Optimisation de production:** Identifier les paramètres physicochimiques optimaux
- **Détection d'outliers:** Identifier les vins exceptionnels (excellents ou médiocres)
- **Sélection de features:** Déterminer quelles propriétés sont les plus importantes

## ⚠️ Particularités et Défis

### Caractéristiques Importantes

1. **Classes déséquilibrées:** Il y a beaucoup plus de vins de qualité moyenne que de vins excellents ou médiocres
2. **Classes ordonnées:** Les scores de qualité suivent un ordre naturel (0 < 1 < ... < 10)
3. **Données limitées:** Par souci de confidentialité et de logistique, certaines informations ne sont pas disponibles :
   - Type de cépage
   - Marque du vin
   - Prix de vente
   - Autres données commerciales

### Défis Techniques

- **Déséquilibre des classes:** Nécessite des techniques d'échantillonnage ou de pondération
- **Pertinence des features:** Toutes les variables ne sont peut-être pas pertinentes
- **Détection d'outliers:** Identification des vins exceptionnels dans un dataset déséquilibré

## 📚 Référence Scientifique

**Article fondateur:**  
*"Modeling wine preferences by data mining from physicochemical properties"*

**Auteurs:** P. Cortez, A. Cerdeira, Fernando Almeida, Telmo Matos, J. Reis  
**Publié dans:** Decision Support Systems (2009)  
**Lien:** [Semantic Scholar](https://www.semanticscholar.org/paper/bf15a0ccc14ac1deb5cea570c870389c16be019c)

Pour plus d'informations sur le Vinho Verde : http://www.vinhoverde.pt/en/

## 💻 Utilisation avec Python

### Installation

```bash
pip install ucimlrepo
```

### Code d'Exemple

```python
from ucimlrepo import fetch_ucirepo

# Télécharger le dataset
wine_quality = fetch_ucirepo(id=186)

# Accéder aux données (pandas DataFrames)
X = wine_quality.data.features  # Variables d'entrée
y = wine_quality.data.targets   # Variable cible

# Afficher les métadonnées
print(wine_quality.metadata)

# Afficher les informations sur les variables
print(wine_quality.variables)
```

## 🔍 Créateurs du Dataset

- **Paulo Cortez** (Contact principal)
- **A. Cerdeira**
- **F. Almeida**
- **T. Matos**
- **J. Reis**

**Affiliation:** Université du Minho, Portugal

## 📝 Recommandations pour l'Analyse

1. **Exploration des données:**
   - Analyser la distribution des scores de qualité
   - Visualiser les corrélations entre variables
   - Identifier les outliers

2. **Prétraitement:**
   - Normaliser/standardiser les features
   - Gérer le déséquilibre des classes
   - Séparer les analyses pour vins rouges et blancs

3. **Modélisation:**
   - Tester des approches de classification et régression
   - Comparer les performances sur vins rouges vs blancs
   - Appliquer des techniques de sélection de features

4. **Validation:**
   - Utiliser une validation croisée stratifiée
   - Évaluer avec des métriques adaptées aux classes déséquilibrées
   - Tester la généralisation sur les deux types de vin

---

**Date du rapport:** Novembre 2024  
**Dataset disponible sur:** http://archive.ics.uci.edu/dataset/186/wine+quality
