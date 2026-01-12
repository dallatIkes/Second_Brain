---
aliases:
  - FCM
---
---

# Principe

Utilise la même stratégie que [[K-means]] mais génère une partition floue, càd que les points ont un degré d'appartenance  à chaque cluster

[[Fuzzy C-means|FCM]] minimise la fonction suivante : $$J_m(U,\mu)=\sum_{i=1}^n\sum_{k=1}^Ku_{i,k}^m\lVert x_i-\mu_k\rVert^2$$où $m$ est le coefficient flou (généralement $m=2$) 

# Algorithme

1. Initialiser aléatoirement les centres de clusters $\mu_k^{(t)}$ et la matrice $U\in\{0\}^{n\times K}$ 
2. Mise à jour de la matrice $U$ : $$u_{i,k}=\begin{cases}[\sum_{l=1}^K(\frac{\mathrm{dist}(x_i,\mu_k^{(t)})}{\mathrm{dist}(x_i,\mu_l^{(t)})})^{\frac{2}{m-1}}]^{-1}\text{ si }\forall l,\mathrm{dist}(x_i,\mu_l^{(t)})\gt0 \\ 1\text{ si }\mathrm{dist}(x_i,\mu_k^{(t)})=0 \\ 0\text{ si }\exists l, l\ne k,\mathrm{dist}(x_i,\mu_l^{(t)})=0\end{cases}$$
3. Mise à jour des centre des clusters : $\mu_k^{(t+1)}=\frac{\sum_{i=1}^n(u_{i,k})^mx_i}{\sum_{i=1}^n(u_{i,k})^m}$ 
4. Convergence : on réitère jusqu'à ce que $\mathrm{dist}(\mu_k^{(t)},\mu_k^{(t+1)})\lt\varepsilon,\forall k$  