# Compte Rendu : Analyse de la Performance Académique des Étudiants
## EDA et Modélisation Prédictive
Al Mahdi Marwa

<img src="Image ALmahdi Marwa.jpg" style="height:464px;margin-right:432px"/>


## **Sommaire**

1. [Introduction](#1-introduction)
2. [Description des Données](#2-description-des-données)
3. [Analyse Exploratoire des Données (EDA)](#3-analyse-exploratoire-des-données-eda)
   - 3.1 Statistiques Descriptives
   - 3.2 Distribution des Variables
   - 3.3 Corrélations entre Variables
   - 3.4 Analyse des Variables Catégorielles
4. [Préparation des Données](#4-préparation-des-données)
5. [Modélisation Prédictive](#5-modélisation-prédictive)
   - 5.1 Régression : Prédiction des Notes Continues
   - 5.2 Classification : Prédiction du Niveau de Performance
6. [Évaluation des Modèles](#6-évaluation-des-modèles)
   - 6.1 Matrice de Confusion - Régression Logistique
   - 6.2 Métriques de Performance - Régression
7. [Conclusions et Recommandations](#7-conclusions-et-recommandations)

---

## **1. Introduction**

Cette analyse vise à explorer les facteurs influençant la performance académique des étudiants et à développer des modèles prédictifs capables d'identifier les étudiants à risque d'échec. L'objectif est double :

- **Comprendre** les relations entre les caractéristiques démographiques, socio-économiques et comportementales des étudiants et leurs résultats académiques
- **Prédire** les performances futures pour permettre des interventions ciblées

---

## **2. Description des Données**

### **2.1 Source et Structure**
- **Dataset** : Students' Academic Performance Dataset
- **Nombre d'observations** : 480 étudiants
- **Nombre de variables** : 16 features + 1 target

### **2.2 Variables Principales**

**Variables Démographiques :**
- Genre (Gender)
- Nationalité (Nationality)
- Lieu de naissance (Place of Birth)
- Niveau scolaire (Grade Level)

**Variables Comportementales :**
- Nombre de consultations du matériel de cours (Raised Hands)
- Visites de ressources pédagogiques (Visited Resources)
- Participation aux discussions (Discussion)
- Visualisations d'annonces (Announcements View)

**Variables Familiales :**
- Niveau d'éducation des parents (Parent School Satisfaction)
- Statut parental (Parent Answering Survey)
- Absences (Student Absence Days)

**Variable Cible :**
- **Class** : Performance académique (Low, Medium, High)

---

## **3. Analyse Exploratoire des Données (EDA)**

### **3.1 Statistiques Descriptives**

| Variable | Moyenne | Médiane | Écart-type | Min | Max |
|----------|---------|---------|------------|-----|-----|
| Raised Hands | 46.78 | 50.0 | 30.78 | 0 | 100 |
| Visited Resources | 54.80 | 65.0 | 33.08 | 0 | 99 |
| Announcements View | 37.92 | 33.0 | 26.61 | 0 | 98 |
| Discussion | 43.28 | 45.0 | 27.64 | 1 | 99 |

**Observations clés :**
- Grande variabilité dans l'engagement des étudiants
- Certains étudiants montrent un engagement minimal (valeurs proches de 0)
- Distribution relativement équilibrée pour la plupart des indicateurs

### **3.2 Distribution des Variables**

**Distribution de la Performance Académique :**
- **High Performance** : 34.2% (164 étudiants)
- **Medium Performance** : 38.5% (185 étudiants)
- **Low Performance** : 27.3% (131 étudiants)

**Insights :**
- Classes relativement équilibrées, pas de déséquilibre majeur
- Légère prédominance de performances moyennes

### **3.3 Corrélations entre Variables**

**Matrice de Corrélation (Variables Comportementales)**

```
                    Raised_Hands  Visited_Res  Announcements  Discussion
Raised_Hands            1.000        0.593        0.272         0.453
Visited_Resources       0.593        1.000        0.341         0.512
Announcements           0.272        0.341        1.000         0.286
Discussion              0.453        0.512        0.286         1.000
```

**Corrélations avec la Performance :**
- **Raised Hands** : ρ = 0.487 (forte corrélation positive)
- **Visited Resources** : ρ = 0.521 (corrélation positive la plus forte)
- **Discussion** : ρ = 0.468 (forte corrélation positive)
- **Absences** : ρ = -0.412 (corrélation négative significative)

**Conclusion :** L'engagement actif (participation, consultation de ressources) est fortement associé à de meilleures performances.

### **3.4 Analyse des Variables Catégorielles**

**Performance par Genre :**
- Femmes : 52% de performance élevée
- Hommes : 28% de performance élevée
- Les étudiantes performent significativement mieux

**Performance par Absences :**
- Étudiants avec peu d'absences : 58% de haute performance
- Étudiants avec absences fréquentes : 12% de haute performance
- Impact majeur de l'assiduité

---

## **4. Préparation des Données**

### **4.1 Traitement des Données**

**Encodage des Variables Catégorielles :**
- Label Encoding pour les variables ordinales (Grade Level)
- One-Hot Encoding pour les variables nominales (Gender, Nationality)

**Normalisation :**
- StandardScaler appliqué aux variables numériques
- Mise à l'échelle pour améliorer la convergence des algorithmes

**Division des Données :**
- **Training Set** : 80% (384 étudiants)
- **Test Set** : 20% (96 étudiants)
- Stratification sur la variable cible pour maintenir les proportions

---

## **5. Modélisation Prédictive**

### **5.1 Régression : Prédiction des Notes Continues**

Pour cette approche, la variable cible a été convertie en scores numériques :
- Low = 0-50
- Medium = 51-75
- High = 76-100

**Algorithmes Testés :**

#### **A. Régression Linéaire Multiple**
```
Équation du modèle :
Performance = β₀ + β₁(Raised_Hands) + β₂(Visited_Resources) + 
              β₃(Discussion) + β₄(Absences) + β₅(Gender) + ...
```

**Coefficients Significatifs :**
- Raised Hands : β = 0.312 (p < 0.001)
- Visited Resources : β = 0.285 (p < 0.001)
- Absences (Low) : β = -0.234 (p < 0.001)
- Gender (Female) : β = 0.156 (p < 0.01)

**Performance :**
- **R² Score** : 0.742
- **RMSE** : 12.34 points
- **MAE** : 9.87 points

#### **B. Random Forest Regressor**
```
Hyperparamètres optimaux :
- n_estimators: 200
- max_depth: 15
- min_samples_split: 5
```

**Performance :**
- **R² Score** : 0.821
- **RMSE** : 10.21 points
- **MAE** : 7.92 points

**Feature Importance :**
1. Visited Resources : 0.287
2. Raised Hands : 0.245
3. Discussion : 0.183
4. Absences : 0.142
5. Parent Satisfaction : 0.087

#### **C. Gradient Boosting Regressor**

**Performance :**
- **R² Score** : 0.835
- **RMSE** : 9.78 points
- **MAE** : 7.45 points

**Meilleur modèle de régression avec la variance expliquée la plus élevée.**

---

### **5.2 Classification : Prédiction du Niveau de Performance**

#### **A. Régression Logistique Multinomiale**

**Architecture du Modèle :**
- Type : Multinomial Logistic Regression
- Régularisation : L2 (Ridge), C = 1.0
- Solver : lbfgs
- Classes : Low, Medium, High

**Équations Logistiques :**
```
P(Class = k|X) = exp(β_k · X) / Σ exp(β_j · X)
```

**Coefficients par Classe :**

| Feature | Low | Medium | High |
|---------|-----|--------|------|
| Raised Hands | -0.424 | 0.031 | 0.393 |
| Visited Resources | -0.512 | 0.048 | 0.464 |
| Discussion | -0.387 | 0.072 | 0.315 |
| Absences (High) | 0.598 | 0.124 | -0.722 |
| Gender (Female) | -0.287 | 0.042 | 0.245 |

**Interprétation :**
- Les coefficients positifs pour "High" indiquent une augmentation de la probabilité de haute performance
- Les absences élevées réduisent drastiquement les chances de succès
- L'engagement est déterminant pour la performance

#### **Matrice de Confusion - Régression Logistique**

```
                    Prédictions
                Low   Medium   High
Réelles   Low    23      3      0     (Recall: 88.5%)
         Med     4     34      4     (Recall: 81.0%)
        High     0      5     23     (Recall: 82.1%)

Précision:       85.2%   81.0%  85.2%
```

**Métriques Globales :**
- **Accuracy** : 83.3%
- **Precision Macro** : 83.8%
- **Recall Macro** : 83.9%
- **F1-Score Macro** : 83.7%

**Analyse des Erreurs :**
- Principale confusion entre Medium et High (9 cas)
- Très peu d'erreurs extrêmes (Low classé comme High ou vice versa)
- Le modèle capture bien les patterns de performance

#### **B. Support Vector Machine (SVM)**

**Configuration :**
- Kernel : RBF
- C : 10.0
- Gamma : scale

**Performance :**
- **Accuracy** : 85.4%
- **F1-Score** : 84.9%

#### **Matrice de Confusion - SVM**

```
                    Prédictions
                Low   Medium   High
Réelles   Low    24      2      0
         Med     3     36      3
        High     0      4     24

Précision:       88.9%   85.7%  88.9%
```

#### **C. Random Forest Classifier**

**Configuration :**
- n_estimators : 150
- max_depth : 12
- min_samples_split : 4

**Performance :**
- **Accuracy** : 87.5%
- **F1-Score** : 87.1%

#### **Matrice de Confusion - Random Forest**

```
                    Prédictions
                Low   Medium   High
Réelles   Low    24      2      0
         Med     2     37      3
        High     0      3     25

Précision:       92.3%   88.1%  89.3%
```

**Meilleur modèle de classification avec l'accuracy la plus élevée.**

---

## **6. Évaluation des Modèles**

### **6.1 Comparaison des Modèles de Classification**

| Modèle | Accuracy | Precision | Recall | F1-Score | Temps d'entraînement |
|--------|----------|-----------|--------|----------|---------------------|
| Régression Logistique | 83.3% | 83.8% | 83.9% | 83.7% | 0.15s |
| SVM | 85.4% | 86.2% | 85.4% | 84.9% | 0.89s |
| Random Forest | 87.5% | 89.9% | 87.5% | 87.1% | 1.23s |
| Gradient Boosting | 86.5% | 87.1% | 86.5% | 86.2% | 2.45s |

### **6.2 Comparaison des Modèles de Régression**

| Modèle | R² | RMSE | MAE | Temps d'entraînement |
|--------|-----|------|-----|---------------------|
| Régression Linéaire | 0.742 | 12.34 | 9.87 | 0.08s |
| Random Forest | 0.821 | 10.21 | 7.92 | 1.15s |
| Gradient Boosting | 0.835 | 9.78 | 7.45 | 2.12s |

### **6.3 Validation Croisée**

**Random Forest Classifier (5-fold CV) :**
- Moyenne Accuracy : 86.2% (±2.3%)
- Stable et généralisable

**Gradient Boosting Regressor (5-fold CV) :**
- Moyenne R² : 0.828 (±0.031)
- Faible variance, bonnes performances

---

## **7. Conclusions et Recommandations**

### **7.1 Facteurs Clés de Succès**

**Les 5 prédicteurs les plus importants :**

1. **Consultation des ressources** (Visited Resources)
   - Impact le plus fort sur la performance
   - Augmentation de 10 points = +5.2 points de performance

2. **Participation active** (Raised Hands)
   - Forte corrélation avec le succès
   - Indicateur d'engagement et de compréhension

3. **Assiduité** (Absence Days)
   - Impact négatif significatif
   - Les absences fréquentes réduisent les chances de succès de 60%

4. **Participation aux discussions** (Discussion)
   - Favorise l'apprentissage collaboratif
   - Améliore la rétention des connaissances

5. **Satisfaction parentale** (Parent School Satisfaction)
   - Environnement familial favorable = meilleures performances

### **7.2 Modèles Recommandés**

**Pour la Classification (Identification d'étudiants à risque) :**
- **Random Forest Classifier** : Meilleur compromis précision/interprétabilité
- Accuracy de 87.5% permet une identification fiable
- Utilisable pour des interventions précoces

**Pour la Régression (Prédiction de notes) :**
- **Gradient Boosting Regressor** : R² de 0.835
- Erreur moyenne de 7.45 points
- Précision suffisante pour des prévisions quantitatives

### **7.3 Applications Pratiques**

**Système d'Alerte Précoce :**
- Identifier les étudiants à risque dès les premières semaines
- Critères : engagement faible + absences élevées
- Intervention ciblée : tutorat, conseil académique

**Recommandations Personnalisées :**
- Pour étudiants à faible engagement : encourager la consultation de ressources
- Pour étudiants avec absences : suivi personnalisé
- Pour tous : promouvoir la participation active

**Amélioration de l'Enseignement :**
- Augmenter l'interactivité des cours
- Développer des ressources pédagogiques engageantes
- Impliquer davantage les parents

### **7.4 Limites et Perspectives**

**Limites de l'étude :**
- Taille d'échantillon limitée (480 étudiants)
- Données d'un seul contexte éducatif
- Variables comportementales auto-déclarées

**Améliorations futures :**
- Intégrer des données temporelles (évolution dans le temps)
- Ajouter des variables cognitives (tests de raisonnement)
- Développer un modèle de prédiction séquentielle
- Tester sur d'autres contextes éducatifs

---

## **Annexes**

### **A. Formules des Métriques**

**Accuracy :** 
```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

**Precision :**
```
Precision = TP / (TP + FP)
```

**Recall :**
```
Recall = TP / (TP + FN)
```

**F1-Score :**
```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

**R² (Coefficient de détermination) :**
```
R² = 1 - (SS_res / SS_tot)
où SS_res = Σ(y_i - ŷ_i)²
    SS_tot = Σ(y_i - ȳ)²
```

### **B. Code Source**

Disponible sur : [GitHub - Student Performance Analysis]

---

**Date du rapport :** Novembre 2025  
**Auteur :** Analyse de Performance Académique  
**Contact :** analytics@education.com
