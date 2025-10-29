## KL divergence-based approach

minimiser la divergence (distance non symétrique) entre $q_\theta(z)$ et la véritable distribution à posteriori :$$KL(q||p)=E_{q(z)}(\ln\frac{q_\theta(z)}{p_\phi(z|x)})=\int q_\theta(z)\ln\frac{q_\theta(z)}{p_\phi(z|x)}dz, \ \ q=p \implies KL()=0$$
## Evidence Lower Bound (ELBO) based approach

$$
\begin{align}
\ln p(x) &= \ln\int_\Omega p(x,z)dz \\
&= \ln\int_\Omega q(z)\frac{p(x,z)}{q(z)}dz \\
&= \ln E_q(\frac{p(x,z)}{q(z)})
\end{align}
$$
$ln$ est une fonction concave, nous pouvons utiliser l'[[Inégalité de Jensen]] : $$\ln E_q(\frac{p}{q}) \ge E_q(\ln\frac{p}{q})=E_q(\ln p(x,z)-\ln q(z)) \ \ (ELBO)$$

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

