# Concept

Popularisé par [[Google]], mesure l'influence des nœuds selon leurs voisins
$$r_i=\frac{1-\alpha}N+\alpha\sum_{j\in\mathcal{N}_i}\frac{r_j}{d_j^+}$$avec : 
- $\alpha\in[0,1]$, le facteur d’amortissement (souvent $\alpha=0.85$)
- $\mathcal{N}_i$, l'ensemble des nœuds pointant vers $i$
- $d_j^+$, le nombre de liens sortant de $j$

On attribue ainsi un score d'importance ("pageRank") à chaque page web. Une page est importante si elle est liée à des pages importantes (récursivité)

Il est utilisé dans pleins de domaines comme la bio-informatique, les réseaux sociaux, les [[Recommendation system|systèmes de recommendation]], la détection de fraudes, etc...

# Random surfer

Le principe du [[PageRank]] $r_i$ d'une page $i$ est basé sur le surfeur aléatoire :
Le surfeur commence sur une page aléatoire, à chaque étape, soit il suit un lien sortant aléatoire de la page courante (avec une probabilité de $\alpha$), soit il s’ennuie et passe à une autre page aléatoire du web (avec une probabilité de $1-\alpha$). Le [[PageRank]] d'une page est la probabilité pour le surfeur aléatoire de s'y retrouver après un grand nombre d'étapes (distribution de probabilité [[Stationnarité|stationnaire]] de cette [[Time series#Marche aléatoire (Random Walk)|marche aléatoire]])

On fixe un seuil de tolérance $\varepsilon$ et on réitère jusqu'à convergence ($\lVert r^{(t+1)}-r^{(t)}\rVert\lt\varepsilon$)

On a bien sûr $\sum r_i=1$ 

# Avantages

- pertinence structurelle
- résistance au spam
- calculable efficacement
- robuste aux pièges et puits

# Limites

- ignorance du contenu
- vulnérabilité au "fermes de liens"
- lent à réagir
- non-spécifique aux requêtes
- coûteux en ressources