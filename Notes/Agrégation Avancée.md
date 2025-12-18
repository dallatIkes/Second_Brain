#Motivation Malgré ces avantages, le [[Clustering]] rencontre plusieurs problèmes :
- la **[[Curse of dimensionality|malédiction de la dimensionnalité]]** 
- les données éparses sont difficile à généraliser
- la complexité explose
- les **données complexes** peuvent former des clusters de formes non convexes ou être imbriqués
Pour contourner ces problèmes, il est possible de modifier l'espace en réduisant la dimension des données ([[ACP]], [[t-SNE]], [[UMAP]]), on applique ensuite des méthodes de [[Clustering|clustering]] ([[DBSCAN]], [[K-means]], [[Clustering#Clustering Hiérarchique|méthodes hiérarchiques]], etc...)

Cependant, il existe des approches développées spécifiquement pour ce type de scénarios, permettant de mieux gérer la complexité, l’incertitude ou la structure des données.

---
# Spectral [[Clustering]]

#Principe Modéliser les données comme un **graphe** et trouver une partition qui **minimise la coupure entre les clusters** 

#Objectif **Regrouper** les points **fortement connectés** et **séparer** ceux **faiblement connectés** 

## Concept de base

### Graphe et Matrices

On commence par calculer deux matrices
- la **matrice de degré** : $D_{ii}=\text{ Arité du point i (nombre de voisins)}$ et $0$ partout ailleurs
- la **matrice d'adjacence** : $A_{ij} = 1 \text{ si i et j sont liés, 0 sinon}$ 
Avec ces deux matrices on calcule la **matrice Laplacienne** $L=D-A$ 

#Exemple ![[Pasted image 20251218135413.png]]

Pour mesurer la **similarité** entre deux points, il faut **pondérer le graphe**, pour cela, une formule couramment utilisées et le  [[Kernel Trick#^rbf|RBF]] : ![[Kernel Trick#^rbf]]Plus les données sont proches, plus le poids est proche de 1

D'autres mesures de similarités sont possibles : 
- graphe des $\varepsilon\text{-voisins}$ : les arrêtes existent uniquement si la distance $\lVert x_i-x_j\rVert\lt\varepsilon$ 
- graphe des [[k-NN|k-plus proches voisins]] : une arrête est ajoutée entre $x_i$ et $x_j$ si $x_i$ est l'un des [[k-NN]] de $x_j$ (ou vice-versa)
![[Pasted image 20251218141052.png]]

### Coupe du graphe

Dans un graphe de similarité, la **coupe** entre deux ensembles de sommets $A$ et $B$ est définie par :
$$\mathrm{cut}(A,B)=\sum_{\substack{i\in A\\j\in B}}w_{ij}$$où $w_{ij}$ est le poids (la similarité) de l'arrête entre $i$ et $j$.

Plus la coupe est **grande**, plus les groupes sont **liés**

L'idée est donc de **minimiser la coupe** :
- réduire les liens entre clusters
- maximiser la cohésion interne

## Algorithme

**Entrées :** les données $X$ et le nombre de clusters $K$

1. Construire le graphe ([[k-NN]] ou $\varepsilon\text{-voisins}$)
2. Construire les matrices $A$ et $D$
3. Calculer le Laplacien normalisé $L_{norm}=D^{-1/2}(D-A)D^{-1/2}$ 
4. Calculer les $d$ plus petit vecteurs propres de $L_{norm}$ (notons $V$ la matrice $n\times d$ qui les contient)
5. Calculer la matrice $Y$en normalisant les lignes de $V$ : $y_{ij}=\frac{v_{ij}}{\sqrt{\sum_lv_{il}^2}}$ 
6. Appliquer [[K-means]] sur $Y$

---







