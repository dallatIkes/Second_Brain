
# Concept de base

Créer des arbres de décision aléatoires et indépendants et calculer la profondeurs des différents nœuds dans ces arbres. Si une feuille est isolée avec peu de coupe, il s'agit d'une anomalie.

**La performance est dégradée avec la [[Curse of dimensionality|malédiction de la dimensionnalité]]**.

# Algorithme

1. **Construction des arbres** :
	- choix aléatoire d'une feature
	- choix aléatoire d'un seuil entre min et max
	- division des données selon ce seuil
	- répétition jusqu'à l'isolement complet de chaque point
2. **Profondeur d'isolation :**
	- chaque point obtient une profondeur moyenne $E(h(x))$ 
	- les anomalies ont une profondeur faible (isolées rapidement)
3. **Score d'anomalie :**
	- on calcule $s(x,n)=2^{-\frac{E(h(x))}{c(n)}}$
	- $c(n)\approx\log(x)$ est un facteur de normalisation
	- $n$ est le nombre de points utilisés pour construire chaque arbre
	- un score proche de $1$ est très anormal
	- un score proche de $0.5$ est plutôt normal

# Avantages

- Pas besoin de modéliser la distribution des données
- Complexité linéaire (très rapide)
- Efficace sur les données multidimensionnelles
- Gère bien les outliers

# Défis

- rareté des anomalies
- définition de la normalité évolutive
- distinction entre le bruit et les anomalies
- haute dimensionnalité
- interprétabilité


