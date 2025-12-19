---
aliases:
  - science des données
---
# Thème 1 - Concepts de base en [[Data Science|Science des Données]]

## 1. Introduction
- **Définition** : domaine interdisciplinaire (maths, stats, informatique, domaine d’application) visant à extraire de l’information utile de grandes masses de données (*big data*).  
- **Composantes clés** : collecte → nettoyage → analyse → visualisation → modélisation → interprétation/communication.  
- **Applications** : tendances commerciales, prévision, détection de fraude/pannes, médecine personnalisée, etc.  

![[Pasted image 20250821131955.png]]
### Lien avec l’[[AI|IA]]
- **[[Machine Learning]] (ML)** : apprentissage à partir de données, sans programmation spécifique.
- **Supervisé** : labels connus, tâches de [[Classification|classification]]/[[Regression|régression]] ([[Support Vector Machine|SVM]], Random Forest, Deep Learning).
- **Non-supervisé** : pas de labels, découverte de structures ([[Clustering]], [[ACP]], [[t-SNE]], règles d’association).
- **Semi-supervisé** : peu de données annotées + beaucoup de non annotées (pseudo-labeling).
- **Renforcement** : agent ↔ environnement, politique pour maximiser récompense (Q-learning, PPO).
- **Auto-supervisé** : prétextes sur données non étiquetées (BERT, SimCLR) pour apprendre des représentations transférables.  

### Problèmes fréquents
- **Overfitting** : trop de complexité → apprend le bruit.  
  *Solutions* : régularisation, dropout, early stopping, data augmentation.  
- **Underfitting** : modèle trop simple → n’apprend pas assez.  
  *Solutions* : complexifier modèle, ajouter features.  
- **Biais-Variance** : compromis entre sous-apprentissage et surapprentissage.  
- **Types de biais** : sélection, mesure, échantillonnage, confirmation, algorithmique.  

---

## 2. Prétraitement des données
- **Objets** = lignes/instances ; **Attributs** = colonnes/features.  
- **Variables** :
  - **Qualitatives** : nominales (sexe, couleur), ordinales (éducation, classe sociale).  
  - **Quantitatives** : discrètes (N), continues (R).  
- **Types de données** : tabulaires, séquentielles (temps), images, textes, graphes, spatiales/3D.  

### Mesures descriptives
- **Tendance centrale** : moyenne, médiane, mode.  
- **Dispersion** : variance, écart-type, IQR.  
- **Détection d’anomalies** : via IQR ou Z-score.  

### Nettoyage
- Données réelles = souvent incomplètes, bruitées, incohérentes.  
- **Données manquantes** :
  - Ignorer (perte d’info).
  - Imputation : déductive, hot-deck (valeurs similaires), cold-deck (autre dataset), constante (moyenne/0), K-NN.  
- **Données bruitées** : détectées via clustering, IQR ou Z-score.  
- **Intégration** : fusion de sources (unités, redondances).  
- **Transformation** : normalisation (min-max, Z-score).  

---

## 3. Numérisation des données
- **Textes** :
  - Bag of Words (comptage d’occurrences).
  - TF-IDF (poids selon rareté).  
  - Word2Vec / Doc2Vec (vecteurs denses, capture sémantique).  
- **Variables catégorielles** :
  - One-hot encoding.  
  - Label encoding (risque d’ordre implicite).  

---

## 4. Réduction de dimension
- **Objectifs** : améliorer performance, réduire bruit, visualiser, éviter la malédiction de la dimension.  
- **Méthodes** :
  - Sélection d’attributs (supprimer redondants/peu informatifs).  
  - Projection (transformer dans sous-espace plus petit).  

### Techniques
- **[[ACP]] (PCA)** : projection linéaire maximisant la variance (compression/visualisation).  
- **[[t-SNE]]** : projection non linéaire, conserve voisinage local (NLP, images).  
- **[[UMAP]]** : rapide, scalable, conserve structure globale et locale (bioinformatique).  

---

## 5. Mesures de similarité
- **Numériques** :
  - [[Euclidean distance|Euclidienne]], [[Taxicab distance|Manhattan]], Minkowski, Mahalanobis (prend en compte corrélation).  
- **Binaires** :
  - SMC (similarité simple), Jaccard (ignore N00).  
- **Autres** :
  - [[Cosine similarity|Cosinus]] (angle entre vecteurs).  
  - Corrélation de Pearson (mesure linéaire, ∈ \[−1, 1\]).  

---

## 6. Visualisation des données
- **Rôle** : rendre l’analyse compréhensible, détecter tendances/anomalies, storytelling (communication).  
- **Exploration (EDA)** : comprendre variables, corrélations, anomalies.  
- **Types** :
  - Box plots (outliers).
  - Histogrammes, barres, camemberts.
  - Scatter plots, line plots, matrices de nuages.
  - Heatmaps, bubble charts.  
- **Bonnes pratiques** :
  1. Clarté et simplicité.  
  2. Choix adapté du type de graphique.  
  3. Titres et étiquettes explicites.  
  4. Utilisation judicieuse des couleurs.  
  5. Cohérence.  
  6. Éviter les distorsions.  
  7. Fournir le contexte.  

---

## 7. Résumé final
- La science des données = découverte de **relations et patterns cachés** dans les grandes bases.  
- **Étapes d’un projet** :
  1. Identifier besoins.  
  2. Obtenir données représentatives.  
  3. Choisir algorithme adapté.  
  4. Appliquer sur données prétraitées.  
  5. Visualiser, évaluer, interpréter.  
- **Objectif** = assister la prise de décision (ne remplace pas l’expert, mais l’aide).  

---

# Thème 2 - Analyse d'association et de séquence

## Introduction
- Applications concrètes :
  - **Netflix** : recommandations personnalisées (historique, notes, genres, horaires).
  - **Amazon** : recommandations produits (achats, consultations, wishlist).
  - **Spotify** : playlists adaptées (écoutes, morceaux aimés, artistes).
  - **YouTube** : vidéos recommandées selon comportements de visionnage.
  - **LinkedIn** : suggestions d’emplois, articles, contacts.
  - **Boutique** : bundling stratégique (pantalon + ceinture, brosse + dentifrice).
- **Objectifs** :
  - Identifier relations entre items dans des transactions.
  - Comprendre les mesures : support, confiance, lift.
  - Appliquer des algorithmes ([[Apriori Algorithm|Apriori]], [[FP-Growth Algorithm|FP-Growth]]).
  - Découvrir motifs séquentiels ([[SPADE Algorithm|SPADE]], [[EMMA Algorithm|EMMA]]).
  - Applications : recommandation, analyse comportementale, détection de patterns.

---

## Analyse d’association
- **Définition** : identifier des relations fréquentes entre éléments (ex. panier d’achat).
- **Concepts clés** :
  - *Itemset* : groupe d’items.
  - *Support* : fréquence d’un itemset.  
    $$
    support(A) = \frac{\text{transactions contenant A}}{\text{total transactions}}
    $$
  - *Confiance* : probabilité que B soit présent si A est présent.  
    $$
    confiance(A → B) = \frac{support(A∪B)}{support(A)}
    $$
  - *Lift* : force de l’association.  
    $$
    lift(A → B) = \frac{confiance(A→B)}{support(B)}
    $$
  - **Interprétation** :
    - lift > 1 → corrélation positive (achetés ensemble plus souvent que par hasard).
    - lift ≈ 1 → indépendants.
    - lift < 1 → corrélation négative.
- **Algorithmes principaux** :
  - **[[Apriori Algorithm|Apriori]]** : génération de candidats + propriété d’anti-monotonie (tout sous-ensemble d’un itemset fréquent est fréquent).
  - **[[FP-Growth Algorithm|FP-Growth]]** : utilise un FP-Tree pour compresser et extraire efficacement.
  - **Eclat** : approche verticale basée sur intersections de tidsets.


---

## Analyse des séquences
- **Différence avec association** : l’ordre des événements est essentiel.  
  - Exemple : {visite page} → {ajout panier} → {achat}
- **Mesures** :
  - Support séquentiel : proportion de séquences contenant un motif.
  - Confiance séquentielle : probabilité qu’un événement suive une séquence.
- **Algorithmes** :
  - **[[PrefixSpan Algorithm|PrefixSpan]]** : projection par préfixe, rapide et efficace.
  - **[[SPADE Algorithm|SPADE]]** : représentation verticale, expansion par jointures.
  - **[[EMMA Algorithm|EMMA]]** : motifs séquentiels avec contraintes temporelles.

---

# Thème 3 - Inférence statistique

## Estimation

## Test d'hypothèse

Hypothèse à accepter ou rejeter

### Types d'erreurs

**Erreur de type 1 :**

**Erreur de type 2 :** 

### Test Binomial

### Test Chi-Carré

### Test de Student

### Taille d'effet

### Analyse de la variance (ANOVA)

### A/B testing 

........

---

# Thème 4 - [[Clustering]]

![[Clustering]]

---

# Thème 5 - [[Agrégation Avancée]]

![[Agrégation Avancée]]

---

# Thème 6 - [[Recommendation system|Système de recommendation]]

![[Recommendation system]]

---
# Thème 7 - [[Web Exploration|Exploration du Web]]

![[Web Exploration]]