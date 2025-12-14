[[Learning Technique|Technique d'apprentissage]] non supervisé qui permet de partitionner notre ensemble de données $X$ en un ensemble $C$ de parties non-vides de taille $K$. N'ayant pas de classes ou étiquettes prédéfinis (contrairement à la [[Classification|classification]], le regroupement de données se fait par la similitudes des attributs des données. 

$C$ peut être représenté par une matrice $U \in \{0,1\}^{n\times K}$ telle que $\forall i,j$ ; 
- $u_{i,k} = 1$ si $x_i\in C_k$ et $u_{i,k}=0$ sinon, on parle alors de **partition dure** (**Hard**)   
- $u_{i,k} \in [0,1]$ appelé **degré d’appartenance**, ainsi un élément peut appartenir à plusieurs classes en même temps (avec un certain degré), on parle alors de **partition floue** (**Fuzzy**) 

Exemple de clustering par partition dure : [[K-means]]