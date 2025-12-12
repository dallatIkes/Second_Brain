Approcher autour d'un point par une gaussienne 

![[Pasted image 20251028084240.png]]

Ici dans le cas de la loi à posteriori, on veut approximer autour du maximum de vraisemblance
En effet : $$p(\Theta|D) \propto p(D|\Theta)p(\Theta)$$Donc si on approxime la vraisemblance $i.e. \ p(D|\Theta)$ on approxime la probabilité à posteriori


Pour ce faire, on utilise la méthode de Taylor :  $$\ln p(D|\Theta)=\ln p(D|\Theta^*)+(\Theta - \Theta^*) \nabla_\Theta\ln p(D|\Theta)|_{\Theta=\Theta^*}+(\Theta-\Theta^*)^T\nabla_\Theta\nabla_\Theta\ln p(D|\Theta)|_{\Theta=\Theta^*}(\Theta-\Theta^*)$$Or ici, $\nabla_\Theta\ln p(D|\Theta)=0$, on peut donc réécrire : $$p(D|\Theta)\approx p(D|\Theta^*)\exp(-(\Theta-\Theta^*)^TM(\Theta-\Theta^*))$$Donc nous pouvons interpréter notre exponentielle comme une Gaussienne et notre matrice $M$ comme une matrice de covariance.

#Exemple $$\begin{align}
p(D) &= \int_\Omega p(D,\Theta)d\Theta \\
&= \int_\Omega p(D|\Theta)p(\Theta)d\Theta \\
&\approx \int_\Omega p(D|\Theta^*)G(\Theta,\Theta^*)p(\Theta^*)d\Theta \\
&= p(D|\Theta^*)p(\Theta^*)\int_\Omega G(\Theta,\Theta^*)d\Theta \\
&= p(D|\Theta^*)p(\Theta^*)(2\pi)^{d/2}\sqrt{|H|}
\end{align}
$$
#Rappel $$\int\int\int\frac{1}{(2\pi)^{d/2}|H]^{1/2}}G(\Theta,\Theta^*)d\Theta=\frac{1}{(2\pi)^{d/2}|H]^{1/2}}\int\int\int G(\Theta,\Theta^*)d\Theta=1$$

#Application $$\ln p(D)=\ln p(D|\Theta^*)+\ln p(\Theta^*)+\frac{1}{2}\ln |H|+\frac{d}{2}\ln2\pi$$

[[Laplace approximation]] est une approximation facile, elle est peut être uniquement utilisée pour des variables continue (à cause de la méthode de Taylor) et ne fonctionne  pas pour des fonctions avec plusieurs maximums.
