
Révision pour l'intra de [[Data Science|Science de données]]

---
## Concepts de base

### Exercice 1 - Robustesse Statistique
**Quelle mesure de tendance centrale est la plus robuste face à la présence de valeurs aberrantes (outliers) ?**  
- La Médiane

### Exercice 2 - Techniques d'Imputation et Données Manquantes
**Indiquez les bonnes propositions sur les techniques d'imputations :**
- L'imputation hot-deck consiste à remplacer  une valeur manquante par une valeur existante provenant d'un enregistrement "donneur" du même jeu de données
- L'imputation cold-deck consiste à remplacer une valeur manquante par une valeur existante provenant d'une enregistrement "donneur" d'une autre jeu de données (historique ou externe)

### Exercice 3 - Visualisation pour Variables Quantitatives
**Quel graphique est le plus approprié pour visualiser la relation (corrélation) entre deux variables quantitatives continues**
- Le Nuage de points (Scatter Plot)

### Exercice 4 - Définition de l'IQR
**Quelle est la définition précise de l'IQR (Intervalle Interquartile) ?**
- La différence entre le troisième quartile ($Q_3$) et le premier quartile ($Q_1$)

### Exercice 5 - Statistiques Descriptives - Propriétés
**Si l'IQR d'une série de données est élevé, cela signifie que :**
- Le 50% central des données présente une grandes dispersion

### Exercice 6 - Représentation des Proportions
**Quel type de graphique est le plus adapté pour représenter la répartition en pourcentage des dépenses totales d'un ménage par catégorie ?**
- Le Diagramme circulaire

---
## Analyse d'association et de séquences

### Exercice 7 - Règle d'Association des Propositions
**On considère que la séquence de règles d'association composite suivante est fréquente :**

$<(A,B) \rightarrow (C,D) \rightarrow E \rightarrow F>$

### Exercice 8 - Parallélisme d'Items dans une Base Transactionnelle
**Dans le cadre de l'analyse temporelle des transactions, que signifie que deux items sont considérés comme parallèles ?**
- Leur écart temporel se situe dans une fenêtre temporelle prédéfinie

### Exercice 9 - [[FP-Growth Algorithm|FP-Growth]] vs Apriori
**Expliquez en trois points clés l'efficacité supérieure de l'algorithme [[FP-Growth Algorithm|FP-Growth]] par rapport à [[Apriori Algorithm|Apriori]] lors du traitement de bases de données massives (décrivez l'avantage structurel de [[FP-Growth Algorithm|FP-Growth]])**
- nombre limité de parcours de la base de données
- Utilise la structure d'arbre
- Ne considère pas tous les candidats

### Exercice 10 - Algorithme [[FP-Growth Algorithm|FP-Growth]]
**Étant donné un ensemble d'items {a,b,c,d,e,f,g,h} et un ensemble de transactions $T$ donné par le tableau suivant, construisez l'arbre FP-Tree et utilisez l'algorithme [[FP-Growth Algorithm|FP-Growth]] pour calculer tous les itemsets fréquents pour un support minimal $\lambda_{min} = 3/8$**
- 

### Exercice 11 - Concepts de Fouille de Séquences
**Cochez les affirmations vraies concernant les concepts de fouille de motifs fréquents et de séquences :**
- Le support séquentiel d'une séquence $S$ est toujours inférieur ou égal au support d'association de l'itemset correspondant aux items de $S$
- [[FP-Growth Algorithm|FP-Growth]] évite la génération de candidats explicites
- SPADE (Sequential Pattern Discovery using Equivalence classes) repose sur une représentation verticale des séquences

### Exercice 12 - Mesures d'Évaluation des Associations
**Cochez les affirmations correctes :**
- Le support d'un itemset est toujours compris dans l'intervalle \[0, 1\]

### Exercice 13 - Avantage Clé de [[FP-Growth Algorithm|FP-Growth]]
**Quel est l'avantage structurel fondamental qui rend l'algorithme [[FP-Growth Algorithm|FP-Growth]] généralement plus rapide que Apriori**
- Il évite les multiples balayages de la base de données en compressant les données dans une structure d'arbre

### Exercice 14 - Contraintes en Fouille de Séquences
**Laquelle des affirmations suivantes est vraie concernant la contrainte temporelle dans l'analyse de données séquentielles ?**
- Elle est essentielle et obligatoire dans l'analyse de séquences

---
## Inférence statistique

### Exercice 15 - Estimation par Maximum de Vraisemblance (MV)
**Considérons un échantillon aléatoire i.i.d. $X_1, ..., X_n$ issu d'une variable aléatoire suivant la loi exponentielle $Exp(\lambda)$, dont la densité de probabilité est donnée par $f(x,\lambda) = \lambda e^{-\lambda x}$ pour $x\le 0$ et $\lambda \gt 0$. Dérivez et estimez le paramètre $\lambda$ par la méthode du Maximum de Vraisemblance.**
$$\hat{\lambda} = \frac{n}{\sum_{i=0}^{n}{X_i}}$$


### Exercice 16 - Intervalle de confiance
**L'interprétation correcte d'un intervalle de confiance à 95% construit pour la moyenne $\mu$ est :**
- Si l'on répète l'expérience un grand nombre de fois, l'intervalle construit conviendra la vraie valeur du paramètre $\mu$ dans 95% des cas

### Exercice 17 - Tests d'Hypothèses et Erreurs
**Lors d'un test d'hypothèse statistique, si l'on rejette l'hypothèse nulle ($H_0$) alors qu'en réalité vraie, on commet :
- Un erreur de Type

### Exercice 18 - Évaluation de la Durée de Vie d'un Composant
**Une entreprise fabrique des composants électroniques. Un ingénieur suppose que la durée de vie de ces composants suit une loi exponentielle de paramètres $\lambda$ inconnu. À partir d'un échantillon, l'ingénieur obtient une moyenne $\bar{X} = 1500$ heures et construits un intervalle de confiance à 95% pour la vraie durée de vie moyenne $\mu$ :\[1450 heures, 1550 heures\]. Parmi les assertions suivantes, cochez celles qui décrivent correctement la méthode utilisée :
- 

### Exercice 19 - Comparaison de deux groupes - test t et taille d'effet
**Deux groupes d'étudiants ont suivi deux méthodes d'apprentissage différentes. On mesure leur score à un test final (sur 20).**
- **Groupe A (méthode active) : 16, 15, 17, 14, 16, 18, 15, 17, 16, 16**
- **Groupe B (méthode classique) : 12, 14, 13, 15, 11, 13, 14, 12, 13, 13**
**Pour test t, on a :**
$$t=\frac{\hat{\mu}_A-\hat{\mu}_B}{\sqrt{\frac{\partial^2A}{n_A}+\frac{\partial^2B}{n_B}}}$$
**le degré de liberté $ddl=n_A+n_B-2$, $\hat{\mu_X}$ et $\hat{\sigma}_X^2$ représentent la moyenne et la variance de l'échantillon $X$ respectivement. Pour la taille d'effet,**
$$d=\frac{\hat{\mu}_A-\hat{\mu}_B}{\hat{\sigma}}$$
**on prendra $\hat{\sigma}=2$** 

-  Il existe une différence statistiquement significative entre les deux groupes
- La différence est forte et d'ampleur pertinente sur le plan pédagogique

---
## Clustering

### Exercice 20 - Algorithmes de segmentation
**On vous présente un dataset à segmenter, mais vous n'avez aucune information sur :**
- **la présence de bruit**
- **le nombre de clusters**
- **la structure des clusters**
**Parmi les assertions suivantes, lesquelles sont vraies ?**
- DBSCAN est robuste au bruit et n'exige pas la connaissance du nombre de clusters, donc bon choix
- DBSCAN est favorable pour des clusters de structures complexes
- KMeans et CMeans exigent la connaissance du nombre de clusters

### Exercice 21 - Prétraitement, Nettoyage et Normalisation des Données
**Soit le jeu de données incomplet et non normalisé suivant :**

| ID  | Âge |   Sexe   | Nb Enfants | Université |   Ville    | Éducation | Revenu (k$) | Classe Cible |
| :-: | :-: | :------: | :--------: | :--------: | :--------: | :-------: | :---------: | :----------: |
|  1  | 65  | Féminin  |     7      |    UdeS    |     -      | Maîtrise  |     4.1     |      ?       |
|  2  | 60  | Masculin |     7      |    UdeS    | Sherbrooke | Licenciée |     3.2     |      ?       |
|  3  | 40  | Féminin  |     1      |    UdeS    |     -      | Licenciée |     2.5     |      ?       |
|  4  |  -  | Masculin |     3      |    UdeS    | Sherbrooke | Licenciée |     1.2     |      ?       |
|  5  | 30  | Masculin |     2      |    UdeS    | Sherbrooke | Licenciée |     2.0     |      ?       |
|  6  | 40  | Féminin  |     -      |    UdeS    | Sherbrooke | Licenciée |     2.5     |      ?       |
|  7  | 18  |    -     |     1      |    UdeS    | Sherbrooke | Licenciée |     1.1     |      ?       |
|  8  | 20  | Masculin |     0      |    UdeS    | Sherbrooke | Licenciée |     0.8     |      ?       |
- **Visualisation : Tracer le diagramme en barres pour la distribution de l'attribut Éducation. Tracer le diagramme circulaire (ou en secteurs) pour représenter la proportion de l'attribut Sexe (Féminin vs Masculin). Indiquez clairement les pourcentages sur le graphique.**
- **Imputation :  Compléter les valeurs manquantes (représentées par un espace vide) du jeu des données ci-haut (décrire et motiver l'approche utilisée pour chaque colonne).**
- **Analyse des Variables : Intuitivement, compléter la colonne Class Cible du jeu de données ci -haut en prenant comme nombre de classes K = 2. Justifiez brièvement votre regroupement.**
- **Réduction de Dimension : Si possible et avec justification, supprimer les colonnes non pertinentes ou redondantes du jeu de données.**
- **Encodage : Numériser le jeu de données résultant, en précisant le type d'encodage utilisé pour chaque variable catégorielle (ex: one-hot encoding, ordinal).** 


### Exercice 22 - Distance Inter-Clusters
**On considère deux clusters dans un espace 2D :**
- **Cluster A : $P_1(1,1),P_2(2,1),P_3(1,2)$**
- **Cluster B : $P_4(5,5),P_5(6,5),P_6(5,6)$**
**Calculez les distances inter-clusters en utilisant la distance euclidienne qui donnée par (avec $p_i=(x_i,y_i)$) :**
$$d(P_i,P_j)=\sqrt{(x_i-x_j)^2+(y_i-y_j)^2}$$
**Choisissez la correspondance correcte :**
- Lien unique = 5.00, lien complet = $\sqrt{41}$
