**Décomposition en valeurs singulières**
$$R\approx P\Sigma Q^T$$

# Algorithme

1. Décomposer la matrice $R$ en $P\Sigma Q^T$
2. Conserver les $K$ plus grandes valeurs singulières $\sigma_k$ 
3. Représenter chaque utilisateur $U_u$ et chaque item $I_i$ par un vecteur latent
4. Prédire une note par produit scalaire : $\hat{r}_{u,i}=P_u\cdot Q_i$ 

> Les valeurs singulières constituent une généralisation des valeurs propres pour les matrices non carrées

À partir d'une matrice $A$, on calcule $B=A^TA$, elle est symétrique et définie positive on on résout $\det(B-\lambda I)=0$, les solutions sont les valeurs propres, les valeurs singulières sont leurs racines.

# Avantages 

- capture des relations implicites entre user et item
- tolère la sparsité des données
- meilleure généralisation

# Limites

- calculs plus complexes ([[ALS]], [[SGD]])
- nécessite beaucoup de données
- moins interprétable

