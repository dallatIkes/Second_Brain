---
aliases:
  - Inférence variationnelle
---
---
# KL divergence-based approach

minimiser la **divergence** (distance non symétrique) entre $q_\theta(z)$ et la véritable distribution à posteriori : $$
\begin{align}
KL(q_\theta(z)||p_\varphi(z\vert x)) &= E_{q(z)}[\ln q_\theta(z)-\ln p_\varphi(z\vert x)]\\
&= E_{q(z)}(\ln\frac{q_\theta(z)}{p_\varphi(z\vert x)}) \\
&= \int q_\theta(z)\ln\frac{q_\theta(z)}{p_\varphi(z\vert x)}dz, \\ 
q=p &\implies KL()=0
\end{align}$$
---
# Evidence Lower Bound (ELBO) based approach

$$
\begin{align}
\ln p_\varphi(x) &= \ln\int_\Omega p_\varphi(x,z)dz \\
&= \ln\int_\Omega q(z)\frac{p_\varphi(x,z)}{q(z)}dz \\
&= \ln E_q(\frac{p_\varphi(x,z)}{q(z)})
\end{align}
$$
$\ln$ est une fonction concave, nous pouvons utiliser l'[[Inégalité de Jensen]] : $$\ln E_q(\frac{p}{q}) \ge E_q(\ln\frac{p}{q})=E_q(\ln p(x,z)-\ln q(z)) \ \ (ELBO)$$

---
# Équivalence des deux approches

$$\ln p_\varphi(x)=ELBO(\theta,\varphi)+KL(q_\theta(z)\vert\vert p_\varphi(z\vert x))$$
$ELBO$ est une borne inférieure de $\ln p_\varphi(x)$. La maximiser revient à minimiser le $KL$
Donc maximiser le $ELBO$ **maximise le data fit** et **minimise la divergence** entre $q$ et $p$

---
# Propriétés

L'[[Variational approximation|Inférence variationnelle]]  convertit l'**intégration** en **optimisation**
Une posterior parfois intractable devient une simple fonction de potentiel
Largement utilisée dans :
- les [[Neural networks|Réseaux de neurones]] Bayésiens
- les Latent Variable models
- les Topic Modeling, Gaussian mixtures, ...

---

# Exemples

$$
\begin{align}
KL(q,p) + E_q(\ln p(x,z)-\ln q) &= E_q(\ln q-\ln p(z|x))+E_q(\ln p(x,z)-\ln q) \\
&= E_q(\cancel{ln q}-\ln p(z|x)+\ln p(x)p(z|x)-\cancel{\ln q}) \\
&= E_q(-\cancel{\ln p(z|x)}+\ln p(x)+\cancel{\ln p(z|x)}) \\
&= E_q(\ln p) \\
&= \int_\Omega\ln p(x)q(z)dz \\
&= \ln p(x)\int_\Omega q(z)dz \\
&= p(x)
\end{align}
$$

$$
\begin{align}
E_q(\ln p(z,x))-E_q(\ln q) &= E_q(\ln p(x)p(z|x))-E_q(\ln\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(z-u)^2}{2\sigma^2}}) \\
&= E_q(\ln p(x))+E_q(\ln p(z|x))-E_q(\ln\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(z-u)^2}{2\sigma^2}}) \\
&= \int_\Omega q(z)\ln p(x)dz+E_q(-z^4+3z^2-2)+E_q(-\ln\sqrt{2\pi\sigma})+E_q(\frac{(z-u)^2}{2\sigma^2}) \\
&= \ln p(x)\int_\Omega q(z)dz+E_q(-z^4+3z^2-2)+E_q(-\ln\sqrt{2\pi\sigma})+E_q(\frac{(z-u)^2}{2\sigma^2}) \\
&= cte+E_q(-z^4+3z^2-2)+\frac{1}{2\sigma^2}\int_\Omega(z-u)^2\frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{(z-u)^2}{2\sigma^2}}dz
\end{align}
$$

#Exemple avec [[Expectation-maximization algorithm|EM]]
$$
\begin{align}
\int_\Omega q(z)\ln\frac{p(x,z|\theta)}{q(z)}-q(z)\ln\frac{p(z|x,\theta)}{q(z)}dz &= \int_\Omega q(z)\ln p(x,z|\theta)-\cancel{q(z)\ln q(z)}-q(z)\ln p(z|x,\theta)+\cancel{q(z)\ln q(z)}dz \\
&= \int_\Omega q(z)[\ln p(x|\theta)p(z|x,\theta)-\ln p(z|x,\theta)]dz \\
&= \int_\Omega q(z)\ln\frac{p(x|\theta)\cancel{p(z|x,\theta)}}{\cancel{p(z|x,\theta)}} \\
&= \ln p(x|\theta)\int_\Omega q(z)dz \\
&= \ln p(x|\theta)
\end{align}
$$

