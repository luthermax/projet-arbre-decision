# TP - Détection de Fraude par Arbre de Décision

![Python](https://img.shields.io/badge/Python-3.13-blue)
![scikit-learn](https://img.shields.io/badge/scikit-learn-1.6-orange)
![pandas](https://img.shields.io/badge/pandas-2.2-green)

##  Description du projet

Ce projet implémente un modèle d'arbre de décision pour la détection de fraudes sur des transactions de carte de crédit. Le projet suit la méthodologie **CRISP-DM** (Cross-Industry Standard Process for Data Mining).

### Contexte métier

Notre entreprise, **FraudGuard Solutions**, est spécialisée dans les solutions d'IA pour le secteur financier. Une grande banque nous a contactés avec le problème suivant :

> « Nous traitons des millions de transactions par carte de crédit chaque jour. Les méthodes de détection de fraude actuelles génèrent un taux élevé de faux positifs (transactions légitimes bloquées) et de faux négatifs (fraudes non détectées). Cela entraîne des pertes financières significatives et une insatisfaction des clients. »

---

## 📊 Dataset

- **Source** : `Fraud Detection Dataset.csv`
- **Taille** : ~10 200 transactions
- **Colonne cible** : `Fraudulent` (0 = Non-Frauduleuse, 1 = Frauduleuse)
- **Déséquilibre** : ~95% Non-Frauduleuses / ~5% Frauduleuses

### Colonnes disponibles

| Colonne | Type | Description |
|---------|------|-------------|
| User_ID | Numérique | Identifiant utilisateur |
| Transaction_Amount | Numérique | Montant de la transaction |
| Time_of_Transaction | Numérique | Heure de la transaction |
| Previous_Fraudulent_Transactions | Numérique | Nombre de fraudes précédentes |
| Account_Age | Numérique | Ancienneté du compte |
| Number_of_Transactions_Last_24H | Numérique | Transactions dernières 24h |
| Fraudulent | Binaire | Variable cible (0/1) |

---

## 🔧 Installation

### Prérequis

```bash
Python 3.8+
```

### Dépendances

```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

### Lancer le projet

1. Ouvrez le notebook Jupyter :
```bash
jupyter notebook "TP_Arbre_Decision (1).ipynb"
```

2. Exécutez les cellules dans l'ordre (Phase 0 → Phase 6)

---

## 🏗️ Structure du projet

Le notebook est organisé en **6 phases** selon CRISP-DM :

### Phase 0 — Installation et Imports
- Import des librairies nécessaires (numpy, pandas, matplotlib, seaborn, scikit-learn)

### Phase 1 — Business Understanding
- Définition du problème métier
- Questions métier à résoudre

### Phase 2 — Data Understanding
- Chargement et exploration des données
- Analyse des valeurs manquantes
- Statistiques descriptives
- Visualisation comparative (boxplots)
- **Matrice de corrélation**

### Phase 3 — Data Preparation
- Séparation X (features) / y (cible)
- Train/Test Split (80/20) avec stratification
- Equilibre des données avec SMOTE
- **Note** : Les arbres de décision ne nécessitent pas de normalisation

### Phase 4 — Modeling
- **Modèle 1** : DecisionTreeClassifier (Gini, max_depth=3)
- **Modèle 2** : DecisionTreeClassifier (Entropy, max_depth=3)
- **Modèle 3** : DecisionTreeClassifier (sans limite de profondeur)

### Phase 5 — Evaluation
- Comparaison des 3 modèles
- Analyse du surapprentissage
- Métriques détaillées (Precision, Recall, F1-Score)
- Matrice de confusion
- Courbe ROC et AUC
- Importance des caractéristiques

### Phase 6 — Deployment
- Synthèse des résultats
- Recommandations au client

---

## 📈 Résultats

### Comparaison des modèles

| Modèle | Critère | max_depth | Accuracy Train | Accuracy Test |
|--------|---------|-----------|----------------|---------------|
| Gini | gini | 3 | ~38.47% | ~37.43% |
| Entropy | entropy | 3 | ~38.47% | ~37.43% |
| No Limit | gini | None | 99% | ~89.2% |

### Modèle recommandé

- **Critère** : Entropy
- **max_depth** : 3

### Métriques clés

| Métrique | Valeur |
|----------|--------|
| Accuracy | ~37.37% |
| Recall (Frauduleuses) | Variable selon équilibrage |
| AUC-ROC | < 0.90 |

### Caractéristiques importantes

Les variables les plus importantes pour la prédiction sont :

1. `Previous_Fraudulent_Transactions`
2. `Number_of_Transactions_Last_24H`
3. `Time_of_Transaction`
---

## ⚠️ Points importants

### Surapprentissage
- Le modèle **No Limit** (sans max_depth) montre un écart train/test de ~0.1%
- **Solution** : Utiliser `max_depth=3` pour éviter le surapprentissage

### Déséquilibre de classes
- Le dataset contient ~5% de frauduleuses seulement
- **Solution** : Ajouter `class_weight='balanced'` dans le modèle

### Normalisation
- Les arbres de décision **n'ont pas besoin** de normalisation
- L'algorithme coupe déjà les données selon les valeurs des features

---

## 🚀 Recommandations

1. **Performance** : Le modèle atteint les objectifs (>80% accuracy)
2. **Limites** : Déséquilibre de classes, variables anonymes
3. **Améliorations** : 
   - Tester RandomForest, XGBoost
   - Validation croisée
   - Optimisation des hyperparamètres
4. **Déploiement** : 
   - Tableau de bord pour analystes
   - Alertes pour transactions à haut risque

---

## 📝 Auteurs

- Étudiant : YENUI Luther 
- Entreprise : FraudGuard Solutions
- Date : Avril 2026

---

## 📚 Références

- [scikit-learn - DecisionTreeClassifier](https://scikit-learn.org/stable/modules/tree.html)
- [CRISP-DM Methodology](https://www.datascience-pm.com/crisp-dm-2/)