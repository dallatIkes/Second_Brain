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

# Projected [[Clustering]]

## Concept de base

#Contexte Données de très grande dimension $m$ où seulement un sous-ensemble de dimensions $d\ll m$ est pertinent pour un cluster donné

#Principe Trouver simultanément : 
- le cluster $C_k$
- le sous-espace de caractéristiques $S_k$ qui définit $C_k$
Dans un espace où notre cluster est compact dans seulement seulement $d$ des $m$ dimensions, les $(m-d)$ autres dimensions sont du bruit que le [[Clustering|clustering]] projeté ignore.

On introduit le concept de **médoïde** qui est **le point le plus central du cluster** (i.e. celui qui minimise la dissimilarité moyenne). Contrairement à un **centroïde**, le **médoïde** est toujours un point réel du jeu de données.

## PROCLUS

Plusieurs approches sont possibles (CLIQUE basée sur les hyper-rectangles, approche par hyper-graphe), mais celle qui nous intéresse le plus par son efficacité est **PROCLUS** :

**Entrées :** 
- ensemble de données $X\in\mathbb{R}^{n\times m}$ 
- nombre de cluster $K$
- nombre moyen de dimensions pertinentes par cluster $d$
**Sortie :** Partition des données en $K$ clusters, chacun défini dans un sous-espace propre
**Limitations :** forte dépendances à $d$ et difficile à appliquer sur des données de très grande dimension

### Algorithme

1. **Sélection des médoïdes candidats :** on choisit aléatoirement les centres initiaux
2. **Choix des médoïdes :** on sélectionne les $K$ médoïdes qui maximisent une heuristique de dispersion (on veut qu'ils soient les plus éloignés possible)
3. **Détermination des sous-espaces :** pour chaque médoïde $m_k$ on identifie les dimensions pertinentes :
	- On un cluster provisoire formé des points qui lui sont proches (distance sous un seuil)
	- On calcule la variance par dimension de ces points
	- On retient au maximum $d$ dimensions où la variance est faible (donc pertinentes pour ce cluster), ce sous-espace de dimensions de $m_k$ est noté $S_k$ 
4. **Affectation des points :** pour chaque point $x_i$, on calcule sa distance projetée avec $m_k$ et lui assigne le cluster le plus proche (selon l'implémentation il est possible de le laisser non affecté si la distance avec tous les $m_k$ dépasse un seuil)
5. **Raffinement itératif :** en recherche de stabilité, on recalcule pour chaque cluster un nouveau médoïde qui minimise la dissimilarité globale et on recalcule les dimensions pertinentes pour ensuite réaffecter les points selon les distances projetées dans ces nouveaux sous-espaces

### Métriques

- **Distance Manhattan :** pour calculer la distance séparant $x_i$ de $m_k$ dans $S_k$ $$\mathrm{dist}(x_i,m_k)=\sum_{j\in S_k}\lvert x_{ij}-m_{kj}\rvert$$
- **Variance par dimension :** pour chaque médoïde $m_k$ et ses voisins $\mathcal{N}_k$ $$\mathrm{Var}_j(m_k)=\frac{1}{\lvert\mathcal{N}_k\rvert}\sum_{x_i\in\mathcal{N}_k}(x_i-\mu_k^{(k)})^2$$avec $\mu_k^{(k)}$ la moyenne des valeurs sur la dimension $j$ pour $x_i\in\mathcal{N}_k$ 
- **Score de qualité (optionnel) :** pour évaluer la compacité des clusters $$\mathrm{score}(m_k)=\frac{1}{\lvert\mathcal{N}_k\rvert}\sum_{x_i\in\mathcal{N}_k}\mathrm{dist}(x_i, m_k)$$
---








