---
aliases:
  - système de recommendation
---
---

# Introduction

Un [[Recommendation system|système de recommendation]] et un ensemble de programmes de [[Machine Learning]] conçus pour aider l'utilisateur à effectuer un choix parmi diverses propositions![[Pasted image 20251218220047.png]]

- **[[Data Science#Analyse d’association|Analyse d'associations]] :** On utilise des algorithmes comme [[Apriori Algorithm|Apriori]] ou [[FP-Growth Algorithm|FP-Growth]] pour trouver des co-occurrences fréquentes dans les transactions  
- **[[Data Science#Analyse des séquences|Analyse de séquences]] :** On étudient l'ordre des actions et événements pour pouvoir prédire les prochains
- **[[Recommendation system|Système de recommendation]] :** utilise les deux analyses précédentes pour pouvoir prédire le comportement futur d'un utilisateur + filtrage collaboratif (générer les recommendations basées sur la similarité entre utilisateurs)

---

# Représentation matricielle des données

## Matrice User-Item

Il s'agit de la matrice des $r_{i,j}$ qui représentent le **rating** donné par le **user $i$** à l'**item $j$** ![[Pasted image 20251219104235.png]]

## Matrice des caractéristiques

Il s'agit de la matrice des $x_{i,\tau}$ qui indiquent si **l'item $i$** possède la caractéristique $\tau$![[Pasted image 20251219104729.png]]

---

# Filtrage basé sur le contenu

On analyse l'historique d'un utilisateur afin de construire un profil de préférence et ensuite recommander un produit similaire![[Pasted image 20251219101657.png]]

Le moteur de recommendation compare essentiellement le **profil de l'item** (caractéristiques et métadonnées) au **profil de l'utilisateur** (historique, évaluations, requêtes)

## Concept 

À partir des représentations matricielles, on peut construire pour chaque user $U_u$ un profil $$P_U=\frac{\sum_{I_i\in I_u}r_{u,i}x_i}{\sum_{I_i\in I_u}r_{u,i}}$$où $r_{u,i}$ désigne le rating donné par le user $U_u$ à l'item $I_i$

Ainsi la recommendation du prochain basé sera basée sur la **similarité** des $x_i$ en utilisant différentes métrique comme la [[Euclidean distance|distance euclidienne]] ou la [[Cosine similarity|similarité cosinus]]

Les deux techniques de recherche sur le contenu les plus utilisées sont : 
- La **[[Cosine similarity|similarité cosinus]] :** on mesure la proximité entre le vecteur $x_i$ et le profil $P_u$ $$\mathrm{recommend}(I_i\vert P_u)=\begin{cases}1\text{ si }1-\cos(x_i,P_u)\le\delta\\0\text{ sinon}\end{cases}$$avec $\delta$ le seuil de tolérance du système (plus il est petit plus la tolérance est stricte)
- L'**[[Bayesian inference|approche bayésienne]] :** on estime la probabilité que l'utilisateur $u$ attribue la note de $r_{u,i}$ à l'item $I_i$ $$\mathrm{P_r}(r_{u,i}\vert P_u)=\mathrm{P_r}(r_{u,i})\prod\mathrm{P_r}(x_{i,j}\vert r_{u,i})$$
## Avantages

- Indépendance de l'utilisateur
- Transparence
- Indépendance d'évaluation

## Limites

- difficile de produire un recommendation pertinente en cas de manque d'information sur un item
- le contenu doit être encodé sous forme de caractéristiques significatives

---

# Filtrage collaboratif

On analyse les préférences d'utilisateurs ayant les mêmes goûts et on propose un nouvel item

## Étapes

1. Collecte des informations sur les utilisateurs
2. Construction de la matrice d'association
3. Génération des recommendations

## Approches

Il existe deux approches principales : 
- **user-user :** recherche d'autres utilisateurs avec des vecteurs de notes similaires
	  - Exemple : les clients $A$ et $B$ aiment tous les deux $x$, ils sont dont similaires, $A$ a également aimé $y$, on recommande donc $y$ à $B$
	  - Limite : peu stable et vulnérable au shilling attack (push attack, nuke attack)
- **item-item :** recherche des items similaires à ceux que le user a bien noté
  Exemple : il semble qu'une grande parties des users ayant aimé $x$, on aimé $y$, $A$ a aimé $x$, on lui recommande donc $y$ 

**Mesures de similarité courantes :** [[Cosine similarity|similarité cosinus]], corrélation de Pearson, Jaccard

Dans l'approche moderne du filtrage collaboratif, on essaie d'extraire des relations complexes en extrayant des facteurs latents grâce à la décomposition matricielle ([[SVD]]), au [[Deep Learning]] ([[Autoencoder|auto-encodeurs]], embedding), à l'approximation de la matrice user-item... mais cela reste plus complexe et nécessite une puissance de calcul et une quantité de données plus conséquente

Des optimisations sont possibles avec [[ALS]], [[SGD]]


---

# Mesures d'évaluation

Il est important de savoir si un [[Recommendation system|système de recommendation]] effectue de bonnes recommendations, pour cela il faut l'évaluer, et plusieurs méthodes sont possibles :
- **évaluation hors-ligne :** mesures statistiques sur les données historiques
- **évaluation en ligne :** tests avec utilisateurs réels
- **[[Tests utilisateurs|étude utilisateurs]] :** retours qualitatifs

---

# Résumé

![[Pasted image 20251218233616.png]]
