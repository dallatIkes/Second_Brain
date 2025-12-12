## Principe de base

Partitionne l’ensemble $X$ de données en $K$ clusters avec $K$ un hyperparamètre.

**Principe :** On cherche à minimiser la fonction suivante : $$E=\sum_{k=1}^K\sum_{x_i\in C_k}\lVert x_i-\mu_k\rVert^2$$où $\mu_k$ représente le centre du cluster $C_k$

---

## Algorithme

- **Étape 1 :** Initialiser **aléatoirement** les centres de clusters $u_k^{(0)}$ et la matrice $U$
- **Étape 2 :** On met tous les points dans le clusters qui minimise sa distance avec le centre, 
  i.e. Soit $j=\arg\min_{k\in⟦1,K⟧}dist(x_i,\mu_k^{(t)})$, $\hspace{3pt}u_{i,j} \leftarrow 1$ et  $\forall k\ne j, u_{i,k} \leftarrow 0$         
- **Étape 3 :** Mise à jour des centres des clusters qui deviennent la moyenne des coordonnées des points qu'ils contiennent : $\mu_k^{(t)}=\frac{\sum_{i=1}^nu_{i,k}x_i}{\sum_{i=1}^nu_{i,k}}$ 
- **Étape 4 :** On recommence à partir de l'étape 2 jusqu'à convergence : $\forall k,\lVert\mu_k^{(t)}-\mu_k^{(t+1)}\rVert\lt\epsilon$ 

Exemples d'exécution de l'algorithme :
![[Pasted image 20251212164224.png]]
![[Pasted image 20251212164937.png]]

---

## Propriétés

- **Forces :**
	- converge en général
	- efficace : complexité en $O(KTn)$ avec $T$ le nombre d'itérations
- **Faiblesses :**
	- besoin de spécifier $K$ à l'avance
	- ne gère pas le bruit
	- ne trouve que des clusters de forme sphérique
	- sensible à l'initialisation des centres de clusters

![[Pasted image 20251212164559.png]]
