---
aliases:
  - Astuce du noyau
---
Tous les problèmes ne peuvent pas être résolus avec un modèle linéaire. Par contre, on peut obtenir des modèles non-linéaires à l'aide de fonctions non-linéaires. 

Exemple :
![[Pasted image 20251212095218.png]]
![[Pasted image 20251212095248.png]]

Pour rappel, notre **problème de régression** (maximum à posteriori) est : $$w=\arg\min_w\sum_{i=1}^N(w^T\Phi(x_i)-y_i)^2+\lambda\lVert w\rVert^2$$(poids qui minimisent l'écart avec la cible en prenant en compte le biais)

Si on **fixe le gradient** par rapport à $w$ à $0$, on obtient : $$w=\Phi^ta$$Si on reprend notre **fonction objectif de la régression ridge** : $$J(w)=\sum_{i=1}^N(w^T\Phi(x_i)-y_i)^2+\lambda\lVert w\rVert^2$$en remplaçant $w$ par $\Phi^ta$, on obtient : $$J(a)=a^T\phi\phi^T\phi\phi^Ta-a^T\phi\phi^Ty+y^Ty+\lambda a^T\phi\phi^Ta$$c'est la **représentation duale** de $J(w)$
On peut noter $\phi\phi^T = K$ où $K_{nm}=k(x_n,x_m)=\phi(x_n)^T\phi(x_m)$ 
$K$ est la **[[Matrice de Gram]]** et $k(x_n,x_m)$ le **noyau**

Ainsi, on a $$J(a)=a^TKKa-a^TKy+y^Ty+\lambda a^TKa$$et en fixant $\nabla J(a)=0$, on obtient : $$\boxed{a=(K+\lambda I_n)^{-1}y}$$
Ainsi une fois $a$ calculé, on peut **prédire une nouvelle donnée $x$**: $$
\begin{align}
y(x) &= w^T\Phi(x) \\
&= a^T\Phi(x)^T\Phi(x) \\
&= [(K+\lambda I_n)^{-1}y]^T\Phi(x)^T\Phi(x) \\
&= [(K+\lambda I_n)^{-1}y]^Tk(x)
\end{align}$$
L'[[Kernel Trick|Astuce du noyau]] permet de **calculer $K$** sans avoir à **calculer $\Phi(x_n)$**
Exemple avec $x^T=(x_1,x_2)$ et $\Phi(x)=(x_1^2, \sqrt{2}x_1x_2, x_2^2)$ :
$$
\begin{align}
k(x,x') &= \Phi(x)^T\Phi(x)\hspace{150pt}\text{(10 multiplications et 2 additions)} \\
&= (x_1^2,\sqrt{2}x_1x_2,x_2^2)^T(x_1'^2,\sqrt{2}x_1'x_2',x_2'^2) \\
&= x_1^2x_1'^2+2x_1x_1'x_2x_2'+x_2^2x_2'^2 \\
&= (x_1x_1'+x_2x_2')^2 \\
&= (x^Tx')^2\hspace{165pt}\text{(3 multiplications et 1 addition)}
\end{align}$$


## Règles de construction

![[Pasted image 20251212103836.png]]

Montrant par exemple que $k(x,x')=\exp(-\frac{\lVert x-x'\rVert^2}{2\sigma^2})$ est un noyau valide :
![[Pasted image 20251212104114.png]]
![[Pasted image 20251212104124.png]]
![[Pasted image 20251212104133.png]]
![[Pasted image 20251212104140.png]]

## Noyaux Classiques

- **Noyau polynomial :** $$k(x,x')=(x^Tx'+C)^M  \hspace{20pt}\text{(plus $M$ est grand, plus le noyau a de la capacité)}$$
- **Noyau gaussien :** $$k(x,x')=\exp(-\frac{\lVert x-x'\rVert^2}{2\sigma^2}) \hspace{20pt}\text{(plus $\sigma^2$ est petit, plus le noyau a de la capacité)}$$
## Résumé

![[Pasted image 20251212104657.png]]
