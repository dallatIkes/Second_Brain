Permet d'approximer une **fonction complexe** près d'un point spécifique $a$ par le **polynôme de Taylor**. 

**Formule générale** pour l'ordre $n$ : $$
\begin{align}
f(x) &\approx \sum_{i=0}^nf^{(i)}(a)\frac{(x-a)^i}{i!} \\
\\
&\approx f(a)+f'(a)(x-a)+f''(a)\frac{(x-a)^2}{2!}+...+f^{(n)}(a)\frac{(x-a)^n}{n!}
\end{align}$$

Exemple de son utilisation à l'ordre 2 de façon vectorielle près du **maximum de vraisemblance** $\Theta^*$
$$\ln p(D\vert\Theta)=\ln p(D\vert\Theta^*)+(\Theta - \Theta^*) \nabla_\Theta\ln p(D\vert\Theta)\vert_{\Theta=\Theta^*}+(\Theta-\Theta^*)^T\nabla_\Theta\nabla_\Theta\ln p(D\vert\Theta)\vert_{\Theta=\Theta^*}(\Theta-\Theta^*)$$
