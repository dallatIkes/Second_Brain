Fonction de coût principalement utilisée pour la [[Classification]] binaire (notamment avec les [[Support Vector Machine|SVM]]).

Formule : 
# $$E_D(W)=\frac{1}{N}\sum_{n=1}^N\max(0,1-t_nW^Tx)$$ Avec $t_n$ : la vraie classe et $w^Tx=y(x)$ : le score du modèle (pas une prédiction) 


Gradient : 
# $$\nabla E_D(W)=\frac{1}{N}\sum_{x_n\in M}-t_nx_n$$

> On ne veut pas seulement que la prédiction soit correcte, on voit qu'elle soit correcte avec une marge suffisante. 