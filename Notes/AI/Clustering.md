[[Learning Technique|Technique d'apprentissage]] non supervisé qui permet de partitionner notre ensemble de données $X$ en un ensemble $C$ de parties non-vides de taille $K$. N'ayant pas de classes ou étiquettes prédéfinis (contrairement à la [[Classification|classification]], le regroupement de données se fait par la similitudes des attributs des données. 

## Hard vs Fuzzy

$C$ peut être représenté par une matrice $U \in \{0,1\}^{n\times K}$ telle que $\forall i,j$ ; 
- $u_{i,k} = 1$ si $x_i\in C_k$ et $u_{i,k}=0$ sinon, on parle alors de **partition dure** (**Hard**)   
- $u_{i,k} \in [0,1]$ appelé **degré d’appartenance**, ainsi un élément peut appartenir à plusieurs classes en même temps (avec un certain degré), on parle alors de **partition floue** (**Fuzzy**) 

Exemple de clustering par partition dure : [[K-means]]
Exemple de clustering par partition floue : [[Fuzzy C-means]]

# [[Clustering]] Hiérarchique

Une autre méthode est le clustering hiérarchique : on génère une **structure arborescente** de partitions emboîtées représentant différents niveaux de granularité dans l'organisation des données. Il existent deux grandes familles : 
- la méthode agglomérative (**ascendante**) : fusion progressive
- la méthode divisive (**descendante**) : divisions successives

3 **distances** peuvent être utilisées : 
- $dist_{lien\_unique}(C_i,C_j)=min_{x\in C_i, y\in C_j}dist(x,y)$
  ![[Pasted image 20251214220047.png]]
- $dist_{lien\_complet}(C_i,C_j)=max_{x\in C_i, y\in C_j}dist(x,y)$
  ![[Pasted image 20251214220058.png]]
- $dist_{lien\_moyen}(C_i,C_j)=\frac{1}{n_in_j}\sum_{x\in C_i}\sum_{y\in C_j}dist(x,y)$ 
  ![[Pasted image 20251214220108.png]]

Les structures hiérarchiques obtenues peuvent être représentées par des **dendogramme** : 
![[Pasted image 20251214220305.png]]


# [[Clustering]] basé sur la densité

Les méthodes de [[Clustering|clustering]] classiques ne permettent pas d'identifier des clusters de forme non sphérique (structures étirées, linéaires, ...). Il existe une solution : [[DBSCAN]]

![[DBSCAN]]