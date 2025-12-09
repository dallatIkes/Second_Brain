Le [[Kriging|krigeage]] est, en géostatistique, une famille de méthodes d’estimation linéaires garantissant le minimum de variance sous certaines hypothèses. Le [[Kriging|krigeage]] réalise l'interpolation spatiale d'une variable régionalisée par calcul de l'espérance mathématique d'une variable aléatoire, utilisant l'interprétation et la modélisation du [[Variogram|variogramme]] expérimental. Il tient compte non seulement de la distance entre les données et le point d'estimation, mais également des distances entre les données deux à deux

Prédiction linéaire

Deuxième approche : au lieu d'utiliser la matrice des poids, on utilise la matrice des [[Variogram|variogrammes]]
(même résultat : juste remplacer $C_{kj}$ par $\gamma_{kj}$)

On a $\hat{z}_0=\sum_iw_iz_i$, $\sum_iw_i=1$
$$
\begin{align}
Cov(\hat{z}_0, z_0) &= E[(\hat{z}_0-E(\hat{z}_0))(z_0-E(z_0))] \\
&= E[(\sum_iw_iz_i-E(\sum_iw_iz_i))(z_0-E(z_0))] \\
&= E[(\sum_iw_iz_i-\sum_iw_iE(z_i))(z_0-u)] \\
&= E[(\sum_iw_iz_i-u\sum_iw_i)(z_0-u)] \\
&= E[(\sum_iw_iz_i-u)(z_0-u)] \\
&= E[\sum_iw_iz_iz_0-u\sum_iw_iz_i-uz_0+u^2] \\
&= \sum_iw_iE(z_iz_0)-u\sum_iw_iE(z_i)-uE(z_0)+u^2 \\
&= \sum_iw_iE(z_iz_0)-u^2\sum_iw_i-\cancel{u^2}+\cancel{u^2} \\
&= \sum_iw_iE(z_iz_0)-u^2 \\
&= \sum_iw_i[Cov(z_i,z_0)+u^2]-u^2 \\
&= \sum_iw_iCov(z_i,z_0)+\cancel{u^2}\sum_iw_i-\cancel{u^2} \\
&= \sum_iw_iCov(z_i,z_0)
\end{align}
$$

#Exercice $F=\sum_i\sum_jw_iw_jC_{ij}$  avec  $C_{ij}=Cov(z_i, z_j)$
$$
\begin{align}
F &= w_kw_kC_{kk} + \sum_{i\ne k}w_iw_kC_{ik} + \sum_{j\ne k}w_kw_jC_{kj} + reste
\end{align}
$$
$$
\begin{align}
\frac{\partial F}{\partial w_k} &= 2w_kC_{kk}+\sum_{i\ne k}w_iC_{ik}+\sum_{j\ne k}w_jC{kj}+0 \\
&= 2w_kC_{kk}+2\sum_{i\ne k}w_iC_{ik} \\
&= 2\sum_iw_iC_{ik}
\end{align}
$$


