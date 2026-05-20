# Projet 3 : Identifier les facteurs qui influencent les performances commerciales

**Auteur** : LDA Advisory  
**Source** : 12 Projets pour devenir Data Analyst  
**Dataset** : Sample Superstore  
**Langage** : Python 3  
**Livrables** : Notebook Jupyter · Dashboard HTML interactif

---

## Contexte métier

Une entreprise souhaite comprendre les interactions entre ses produits, ses performances régionales et ses marges afin d'optimiser sa stratégie commerciale.

L'analyse repose sur le dataset Superstore, qui recense 9 994 lignes de commandes couvrant la période 2014 à 2017 sur quatre régions des États-Unis.

---

## Objectifs analytiques

Ce projet vise à :

- Analyser les relations entre variables qualitatives (catégorie, région, segment)
- Comparer les distributions de ventes et de profit selon les groupes
- Mesurer les corrélations entre variables quantitatives (ventes, profit, remise, quantité)
- Identifier les sous-catégories déficitaires et les leviers de rentabilité
- Produire des visualisations claires et des recommandations actionnables

---

## Structure du projet

```
projet3/
├── README.md
├── Sample_-_Superstore.csv
├── projet3_analyse_bivariee.ipynb
└── dashboard_corporate.html
```

---

## Dataset

**Source** : Sample Superstore Dataset (Tableau Public)  
**Fichier** : `Sample_-_Superstore.csv`  
**Encodage** : latin-1  
**Dimensions** : 9 994 lignes × 21 colonnes  
**Période** : janvier 2014 à décembre 2017

### Variables utilisées

| Variable | Type | Description |
|---|---|---|
| Sales | Quantitative | Chiffre d'affaires par ligne de commande |
| Profit | Quantitative | Profit net par ligne de commande |
| Discount | Quantitative | Taux de remise appliqué (0 à 0.80) |
| Quantity | Quantitative | Nombre d'unités commandées |
| Category | Qualitative | Furniture, Office Supplies, Technology |
| Sub-Category | Qualitative | 17 sous-catégories de produits |
| Region | Qualitative | Central, East, South, West |
| Segment | Qualitative | Consumer, Corporate, Home Office |
| Ship Mode | Qualitative | Mode de livraison choisi |
| Order Date | Temporelle | Date de la commande |

---

## Environnement et dépendances

### Prérequis

Python 3.8 ou supérieur est requis.

### Installation

```bash
pip install pandas numpy matplotlib seaborn scipy notebook
```

### Versions utilisées

| Bibliothèque | Rôle |
|---|---|
| pandas | Manipulation et agrégation des données |
| numpy | Calculs numériques |
| matplotlib | Visualisation de base |
| seaborn | Visualisations statistiques avancées |
| scipy | Tests statistiques (Pearson, Spearman) |

---

## Lancement du notebook

```bash
# Cloner ou télécharger le projet
# Placer le fichier CSV dans le même dossier que le notebook

# Lancer Jupyter
jupyter notebook projet3_analyse_bivariee.ipynb
```

Le notebook s'exécute de haut en bas sans modification. Toutes les cellules sont autonomes.

---

## Contenu du notebook

Le notebook est structuré en cinq sections.

### Section 1 : Chargement et exploration des données

Chargement du CSV avec gestion de l'encodage latin-1 et parsing des dates. Vérification de la qualité des données : dimensions, valeurs manquantes, doublons, aperçu des modalités qualitatives, statistiques descriptives des variables numériques.

### Section 2 : Analyse Quali-Quali

Étude des relations entre deux variables catégorielles.

**Analyses réalisées :**

- Répartition des commandes par Catégorie et Région via tableaux croisés et heatmap
- Répartition du mode de livraison par Segment client via bar chart empilé horizontal

**Outils** : `pd.crosstab`, `sns.heatmap`, bar charts empilés

### Section 3 : Analyse Quali-Quanti

Comparaison de distributions numériques entre groupes catégoriels.

**Analyses réalisées :**

- Profit moyen et total par Région : boxplot et bar chart avec ligne de référence à zéro
- Ventes, Profit et Marge nette par Catégorie : boxplots et calcul du ratio profit/ventes
- Profit total par Sous-Catégorie : bar chart horizontal coloré (profitable vs déficitaire)
- Impact des tranches de remise sur le profit moyen par Catégorie

**Outils** : `groupby`, `sns.boxplot`, bar charts colorés conditionnellement

### Section 4 : Analyse Quanti-Quanti

Mesure et visualisation des relations entre variables numériques.

**Analyses réalisées :**

- Matrice de corrélation de Pearson (triangle inférieur masqué)
- Scatter plots Sales vs Profit, Discount vs Profit, Quantity vs Profit avec droite de régression et coefficient r
- Tests de corrélation Pearson et Spearman pour chaque paire avec p-values
- Pairplot global coloré par Catégorie (échantillon 1 000 lignes)

**Outils** : `df.corr()`, `scipy.stats.pearsonr`, `scipy.stats.spearmanr`, `sns.pairplot`

### Section 5 : Synthèse et recommandations métier

Tableau récapitulatif des KPIs agrégés par Région et Catégorie. Présentation structurée des insights en trois axes : facteurs négatifs, opportunités de croissance, relations statistiques validées.

---

## Dashboard interactif

Le fichier `dashboard_corporate.html` est un dashboard standalone qui ne nécessite aucune installation. Il s'ouvre directement dans un navigateur web moderne.

### Contenu du dashboard

**KPIs en en-tête :**

- Ventes totales
- Profit net avec marge en pourcentage
- Nombre de commandes uniques
- Remise moyenne

**Visualisations :**

- Évolution mensuelle des ventes et du profit (2014 à 2017)
- Tableau de performance par Région avec marge nette
- Ventes, Profit et Marge par Catégorie (double axe)
- Profit par Sous-Catégorie (horizontal, rouge/bleu selon signe)
- Impact des remises sur le profit moyen par tranche
- Ventes et Profit par Segment client
- Matrice de corrélation de Pearson avec valeurs affichées

**Filtres interactifs :**

- Filtre par Région (West, East, South, Central)
- Filtre par Catégorie (Technology, Office Supplies, Furniture)
- Les deux filtres sont combinables
- Bouton de réinitialisation

---

## Résultats et insights clés

### Facteurs qui dégradent la rentabilité

**Les remises supérieures à 20% sont systématiquement destructrices de marge.**  
Le profit moyen bascule en territoire négatif dès que la remise dépasse ce seuil. La corrélation Discount/Profit est négative et statistiquement significative (Pearson r = -0.22, p < 0.001).

**Tables et Bookcases affichent un profit net négatif.**  
Malgré des ventes significatives, ces deux sous-catégories du segment Furniture détruisent de la valeur. Tables : -17 725 dollars de profit total. Bookcases : -3 472 dollars.

**La région Central est la moins rentable.**  
Marge nette de 7.9% contre 14.9% pour West. Les pratiques commerciales et la politique de remises dans cette région méritent une analyse approfondie.

### Opportunités identifiées

**Technology est la catégorie la plus rentable.**  
Marge nette de 17.4%, soit sept fois celle de Furniture (2.5%). Amplifier la part des ventes Technology dans le mix produit est le levier de croissance le plus direct.

**La région West concentre le profit.**  
108 418 dollars de profit total, soit 37.8% du profit global pour 31.6% des ventes. Identifier et répliquer les pratiques commerciales de cette région dans Central et South est une priorité stratégique.

**Copiers est la sous-catégorie la plus profitable.**  
55 618 dollars de profit total. Phones et Accessories suivent avec respectivement 44 516 et 41 937 dollars. Ces références méritent d'être davantage promues.

### Relations statistiques validées

| Paire | Pearson r | Spearman r | Significatif |
|---|---|---|---|
| Sales / Profit | 0.479 | 0.511 | Oui |
| Discount / Profit | -0.221 | -0.244 | Oui |
| Quantity / Profit | 0.066 | 0.049 | Oui |
| Discount / Sales | -0.028 | -0.031 | Non |

La corrélation Sales/Profit est positive mais modérée : le volume ne garantit pas la rentabilité. La corrélation Discount/Sales est non significative, ce qui signifie que les remises ne stimulent pas les volumes.

---

## Recommandations métier

**Priorité 1 : Plafonner les remises à 20% dans toutes les catégories.**  
C'est la mesure à impact immédiat le plus élevé sur la marge nette.

**Priorité 2 : Réviser la politique tarifaire sur Tables et Bookcases.**  
Ces produits sont vendus à perte. Une hausse des prix, une réduction des coûts ou un arrêt de gamme doit être évalué.

**Priorité 3 : Auditer la région Central.**  
Comprendre pourquoi la marge est deux fois inférieure à West permettrait d'aligner les pratiques commerciales.

**Priorité 4 : Renforcer les ventes Technology.**  
Cette catégorie offre la meilleure rentabilité et un potentiel de montée en puissance dans toutes les régions.

---

## Compétences développées

- Statistiques descriptives : moyenne, médiane, quartiles, corrélations
- Analyse bivariée : quali-quali, quali-quanti, quanti-quanti
- Visualisation : heatmaps, boxplots, scatter plots, bar charts conditionnels, pairplot
- Tests statistiques : Pearson, Spearman, p-values
- Communication : synthèse des résultats en recommandations actionnables
- Dashboard interactif : HTML/CSS/JS avec Chart.js

---

## Références

- Dataset : [Superstore Sales Dataset, Tableau Public](https://www.tableau.com/learn/articles/free-public-data-sets)
- Documentation pandas : https://pandas.pydata.org/docs/
- Documentation seaborn : https://seaborn.pydata.org/
- Documentation scipy.stats : https://docs.scipy.org/doc/scipy/reference/stats.html
- Source pédagogique : LDA Advisory, 12 Projets pour devenir Data Analyst, Natacha Njongwa Yepnga
