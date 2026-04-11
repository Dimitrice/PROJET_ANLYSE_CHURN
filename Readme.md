# Analyse Exploratoire du Churn Bancaire
## Customer Churn Analysis — Bank Dataset

---

## Contexte du projet

Ce projet porte sur l'analyse exploratoire (EDA) et la préparation des données
d'un dataset de churn bancaire composé de **10 000 clients** . L'objectif est d’analyser les facteurs expliquant le départ des clients  à partir d’un dataset bancaire. L’analyse vise à identifier les variables les plus discriminantes afin de mieux comprendre le comportement des clients.

> **Note importante** : Les 10 000 observations constituent la **population entière** et non un échantillon. Les analyses réalisées sont donc purement descriptives.
---

---

## Variable cible

| Variable | Type | Description |
|---|---|---|
| `Exited` | Binaire (0/1) | 0 = clients restés \| 1 = clients Partis |

| element |  Valeur  |
|**Taux_clients_partis global :|20.38%** (2 038 clients sur 10 000) (Taux_clients_partis )|


---
## Structure du projet

```
PROJET_ANALYSE_CHURN/
│
├── Data/
│   ├──Data_brut
│   │  ├── Customer-Churn-Records.csv     
│   ├──Data_for_prediction
│   │  ├── Data_Churn_Prediction.csv
├── Notebook/
│   ├── 01_ETL_EDA.ipynb            
│   └── 02_Selection_Var_Prdict.ipynb           
│
├── .gitignore
├── Readme.md
└── requirements.txt
```
---

## Technologies utilisées
- Langage : **Python (pandas, numpy, seaborn, matplotlib, skalearn, statsmodels, scipy )**
- Document interactif : **Notebook Python**
- Editeur de code: **VScode** 
- Dataset:Customer-Churn-Records.csv (https://www.kaggle.com)

---
---

## Description des variables
- **RowNumber** : correspond au numéro de l’enregistrement (ligne) et n’a aucun effet sur la sortie.
- **CustomerId** : contient des valeurs aléatoires et n’a aucun effet sur le départ du client de la banque.
- **Surname** :  le nom de famille d’un client n’a aucun impact sur sa décision de quitter la banque.
- **CreditScore** : peut avoir un impact sur le churn, car un client ayant un score de crédit plus élevé est moins susceptible de quitter la banque.
- **Geography** :  la localisation d’un client peut influencer sa décision de quitter la banque.
- **Gender** :  il est intéressant d’explorer si le genre joue un rôle dans le départ d’un client de la banque.
- **Age** : cela est certainement pertinent, car les clients plus âgés sont moins susceptibles de quitter leur banque que les plus jeunes.
- **Tenure** : fait référence au nombre d’années pendant lesquelles le client est client de la banque. Normalement, les clients plus âgés sont plus fidèles et moins susceptibles de quitter une banque.
- **Balance** : également un très bon indicateur du churn des clients, car les personnes ayant un solde plus élevé sur leurs comptes sont moins susceptibles de quitter la banque comparées à celles avec des soldes plus bas.
- **NumOfProducts** : fait référence au nombre de produits qu’un client a achetés via la banque.
- **HasCrCard** :  indique si un client possède ou non une carte de crédit. Cette chronique est également pertinente, car les personnes possédant une carte de crédit sont moins susceptibles de quitter la banque.
- **IsActiveMember** : les clients actifs sont moins susceptibles de quitter la banque.
- **EstimatedSalary** : Comme pour l’équilibre, les personnes avec des salaires plus bas sont plus susceptibles de quitter la banque que celles avec des salaires plus élevés.
- **Exited** : que le client ait quitté la banque ou non
- **Complain** :  le client a ou non une plainte.
- **Satisfaction Score** :  Score fourni par le client pour la résolution de sa plainte.
- **Card Type** : type de détention de carte par le client.
- **Points Earned** : les points gagnés par le client en utilisant une carte de crédit.

---


---

## Plan d'analyse
### Tâche 01 Réalisation du processus ETL ()
- Importation des librairies de python et des données 
- Interrogation de la base, analyse de base (analyse des doublons, valeurs incohérentes, des valeurs manquantes)
- Analyse graphique des valeurs abérantes

###  Tâche 02- Analyse Univariée

####  02.1 — Analyse univariée : variables numériques
- Statistiques descriptives (moyenne, médiane, écart-type, min, max)
- Détection des valeurs extrêmes (méthode IQR)
- analyse graphique afin d'identifier la forme de la distribution de chaque variable quantitative
- analyse du coefficient d'asymetrie 

####  02.2 — Analyse univariée : variables qualitatives
- Fréquences absolues 
- Poportion en pourcentage de chaque groupe modalité de la variable cible

###  Tâche 03- Analyse Bivariée

### Tâche 03.1 — Analyse bivariée : variables quantitatives vs Exited
- Moyennes réelles par groupe (Restés vs Resté)
- Écart absolu 
- Analyse de l'intensité de l'association entre les variables quantitatives et la variable cible (Exited)
- Analyse Graphique

#### Tâche 03.2 — Analyse bivariée : variables qualitatives vs Exited
- Tableau de contingence
- Taux de départ réel par modalité
- Écart au taux global (en points de pourcentage)
- V de Cramér (force de l'association, une mesure descriptive)
- Odds Ratio descriptif



### Tâche 04 — Analyse multivariée : interactions entre variables
- Feature Engineering
- Suppression des variables non Associées à Exited 
- Feature Engineering
- Normalisation de la var (balance et Age) 
- Analyse de la multicolinéarité des variables explicatives 
- suppression des la variables explicatives correlés 

---

## Résultats clés

### analyse  Bivariée des variables quantitative 

#### analyse des écarts entre le groupe des clients qui partent  et qui restent

| Variable | Moyen restés | Moyen Partis  | Ecarts | Ecarts (%) | 
|---|---|---|---|---|
| CreditScore |  651.84  |  645.41  |  -6.42  | -1.0% | 
| Age   |   37.41  |  44.84|   +7.43    | +19.9% | 
| Tenure |   5.03 |   4.93  |  -0.10  | -1.9% | 
| Balance | 72742.75  |   91109.48 |  +18366.73  | +25.2% | 
|  EstimatedSalary |  99726.85  |   101509.91  |   +1783.06   |  +1.8%  | 
| Satisfaction Score   |   3.02  |   3.00   |   -0.02  | -0.7% | 
| Point Earned  |   607.04  |  604.45  |  -2.60 |  -0.4%  | 
| NumOfProducts  |   1.54   | 1.48  |  -0.07|   -4.5%  | 

#### Variables quantitatives retenues

| Designation | Valeur |
|---|---|
| Nombre de clients | 10000 |
| proportion des clients partis | 20.38% |

| Variable | Type | Mesure | Valeur | Pvalue | Valeur | Décision |
|---|---|---|---|---|---|---|
| `NumOfProducts` | Discrète | V Cramér | 0.387 | p_(chi2) | 0.000000 | Association statistiquement significative |
| `Age`  | Continue | corr bisériale |   0.2853 | p_(t-student) | 0.000000 | Association statistiquement significative|
| `Balance`  | Continue | corr bisériale |   0.1186 | p_(t-student) | 0.000000 | Association statistiquement significative|
| `IsActiveMember` | binaire |  phi |  0.1561 | p_(Fisher exact) |  0.000000 | Association statistiquement significative |


#### Variables quantitatives exclues

| Variable | Raison |
|---|---|
| `Complain` |  phi = 0.996 (0.000000), extrèmement associée avec Exited (Data leakage)  |
| `CreditScore` | corr_bisériale = -0.0268 ( 0.007422), statistiquement significatif mais quasiment non associée  |
| `HasCrCard` | Phi = 0.0067 (0.496018), Non associée |
| `EstimatedSalary` | corr_biseriale =  0.0125(0.211715),  Non associée |
| `Satisfaction Score` | V cramèr =  0.0195(0.433365),  Non associée |
| `Point Earned` | corr_bisériale =  -0.0046(0.643535),  Non associée|
| `Tenure` | corr_bisériale = -0.0137(0.172104),  Non associée|

### Bivariée des variables qualitatives 
#### Analyse de l'association des variables qualitatives avec la variable cible
| Variable | V cramèr | Force de la mesure | 
|---|---|---|
| Geography  | 0.1734  |  Modéré | 
| Gender  |  0.1063  |  Modéré |  
| Card Type  | 0.0225 | Faible |  

#### analyse de la proportion des clients partis par modalité

| Geography |Fréquences Absolue | Nombre de clients Restés | Nombre de clients Partis | Taux_clients partdis |  Odds Ratio |
|---|---|---|---|---|---|
| France |  5014  |  4203  |  811  |  16.2%  | 0.59  | 
| Germany  |   2509  |  1695  |   814    |   32.4%   |  2.46 | 
| Spain  |  2477  |    2064   |  413 |  16.7%  |  0.73 | 

| Gender |Fréquences Absolue | Nombre de clients Restés | Nombre de clients Partis | Taux_clients partdis |  Odds Ratio |
|---|---|---|---|---|---|
| Female  | 4543 | 3404 | 1139 | 21.1% |  1.70 | 
| GOLD   | 5457 | 4558 | 899 | 16.5% |  0.59 | 


| Card Type |Fréquences Absolue | Nombre de clients Restés | Nombre de clients Partis | Taux_clients partdis |  Odds Ratio |
|---|---|---|---|---|---|
| DIAMOND |  2507  |  1961  |  546  |     21.8%  |  1.12 | 
| GOLD   |   2502  |  2020  |    482     |   19.3%   |  1.00 | 
| PLATINUM  |  2495  |    1987  |  508 |  20.4%  |  0.91 | 
| SILVER  |   2496  |   1994  |  502|  20.1%  |  0.98 | 

---

## pipline de préparation de données

### nouvelles variables créées à partir des interactions détectées

- Risque_Nbproduit : les clients qui achète [3 - 4 ]produits représentes 83% des clients qui quittent la banque
- Client_Allemangne : les clients en provenance d'Allemagne qui partent représentent presque le double des clients qui partent dans d'autres aire Geographique 
- Solde_Positif : les clients ayant un compte positif voit bien founir sont enclins à quitter la banque 
- Client_Senior : les clients de 50ans et plus  sont plus enclins à quitter la banque 
- Clt_Inact_Monopdt : elle combine  les clients inactifs et ayant acheté qu'un seul produit via la banque 

### feature engineering

-  Recodage Variable NumOfProducts, en une variables categorielle (appréciation_Nbproduit) avec  3 modalités (risque, fidele, critique) 
- suppression des variables non retenues avec la variables cible:(Complain, CreditScore, HasCrCard, EstimatedSalary, Satisfaction Score, Point Earned, Tenure, Card Type )
- Encodage de la variable  Geography, appréciation_Nbproduit avec le one hot encoding et la variable Gender avec le label encoding
- Normalisation des variables Age et Balance afin de mettre toutes les features sur une échelle comparable

## Analyse de la multicolinéarité : variables explicatives retenues après analyse uniquement
| Variable | Vif | decision seuil (vif < 5 :Acceptable, vif =[5-10] : seuil modéré, vif >10 : seuil élevé ) | 
|---|---|---|
|  Age  | 2.361039 | variable retenue | 
|  Gender  |  1.003918 | variable retenue | 
| IsActiveMember | 1.659190 | variable retenue | 
| Risque_Nbproduit | 1.041420 | variable retenue | 
| Client_Allemangne | 1.373007 | variable retenue | 
| Solde_Positif | 1.331117 | variable retenue | 
| Client_Senior | 2.361340 | variable retenue | 
|  Clt_Inact_Monopdt | 1.739201 | variable retenue | 
| Geography_Spain | 1.125292 | variable retenue | 
## Insights
1- Les clients présentant le plus fort risque de churn sont généralement plus âgés, avec un âge moyen d’environ 45 ans contre 37 ans pour les clients fidèles. Ils disposent également d’un solde bancaire moyen supérieur, avec un écart d’environ +18 000,  et montrent un faible niveau d’engagement dans leur relation avec la banque (inactif).
2- On observe une augmentation significative du taux de churn à mesure que le nombre de produits détenus augmente.
 Alors que le churn reste limité pour les clients ayant deux produits (7,6 %), il devient très élevé pour ceux en possédant trois (82,7 %) et atteint 100 % pour quatre produits. Cette tendance indique que les clients multi-équipés présentent un risque de départ nettement plus élevé.
3- On n’observe pas de différence significative entre la proportion de clients ayant quitté la banque et ceux étant restés après la résolution de leur problème (19,6 % contre 21,8 %). Deux hypothèses peuvent expliquer ce résultat : soit les clients quittent la banque sans exprimer leur insatisfaction, soit la mesure de la satisfaction n’est pas suffisamment pertinente ou correctement formulée pour capturer le ressenti réel des clients.
4- Les clients basés en Allemagne affichent un taux de churn significativement plus élevé, environ deux fois supérieur à celui observé en France et en Espagne. Cette différence suggère soit une pression concurrentielle plus forte sur ce marché, soit des attentes client différentes, potentiellement moins bien couvertes par l’offre de la banque. 
5- les femmes ont 70% plus de chance de quitter la banque par rapport aux hommes. Cela suggère que la banque ne répond pas certainement aux besoins spécifiques d'une partie importante de sa clientèle féminine.
6- les client inactif on deux plus de chance de quitter la banque par rapport au autres actif 
### Resumé des Insights :
La banque perd principalement des clients matures et aisés non pas parce qu'ils sont insatisfaits au sens déclaratif, mais parce qu'ils ne se sentent pas suffisamment bien servis pour leur profil — ce qui se traduit par une inactivité croissante puis un départ, surtout en Allemagne et chez les femmes.
## Auteur
Dimitrice Wabo