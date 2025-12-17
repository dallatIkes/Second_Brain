counts for the nested structure of the data

Example : Estimate how study hours affect grades without considering the
school or class context.
- level 1 : individual students
- level 2 : the class where the students are grouped
- level 3 : the departments where the classes are grouped

## Sélection de modèle

**Critères :** 
- Ajuster au mieux les données (max de vraisemblance)
- Réduire au minimum le nombre de paramètres (complexité du modèle)

ex: meilleur modèle s'ajustant au données $= \sum f_{données}$ ajustement parfait mais modèle très complexe.   

**ANTAGONISME** $\rightarrow$ compromis !

meilleur algorithme de sélection de modèle : [[AIC]]
pire algorithme : MDL 

## Simulation de modèle

**Méthode :** [[Markov chain Monte Carlo|MCMC]]  

[[Machine Learning]]

[[Bayesian inference]] 

[[Bayesian point estimation methods]]

---

## Approximations

Approcher une fonction par une autre fonction

Le but principale de l'**[[Bayesian inference|Inférence Bayésienne]]** est de spécifier la **posterior** : $p(\Theta\vert X)$. Cela peut être fait avec des **algorithmes exacts**, mais dans la plupart des cas, la **complexité** **spatiale** et **temporelle**, rend leur utilisation non raisonnable. Dans ce cas, nous avons besoin d'approximations.

[[Laplace approximation]]

[[Variational approximation]]

---

## [[Time series]]

![[Time series]]


---

### [[Spatiotemporal Models]]

--- 
#### Exercices de révision

##### Exercice 1

>$\epsilon\sim\mathcal{N}(\epsilon|0, \sigma^2I)$ 
>$Y,X$ des vecteurs
>$A,B$ des matrices
>$BY=AX+\epsilon$ 
>**Calculer la PDF $f_y(y)$**

Supposons $B$ inversible
$B^{-1}BY=IY=Y=B^{-1}(AX+\epsilon)$  

>$f_\epsilon(\epsilon)=\frac{1}{(2\pi\sigma^2)^{d/2}}\exp({\frac{-\epsilon^t\epsilon}{2\sigma^2}})$
>**Calculer $f_y(y)$**

On fait un changement de variable : $\epsilon=BY-AX$ 
Ainsi : $f_y(y)=\frac{\mid\det B\mid}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{(BY-AX)^t(BY-AX)}{2\sigma^2})$ 
$\frac{\partial\epsilon}{\partial Y}=B$ 

##### Exercice 2

> Considérons le modèle :
> $y=\rho wy+XB+\epsilon$, $\epsilon\sim\mathcal{N}(\epsilon|0, \sigma^2I)$, $\rho$ scalaire, $w$ matrice, $B$ vecteur, $X$ matrice
> Écrire la vraisemblance 

$y-\rho wy-XB=\epsilon$
$y(I-\rho W)-XB=\epsilon$
$f_\epsilon(\epsilon)=\frac{1}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{\epsilon^t\epsilon}{2\sigma^2})$ 
$f_y(y)=\frac{\mid\det(I-\rho w)\mid}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{[(I-\rho w)y-XB]^t[(I-\rho w)y-XB]}{2\sigma^2})$ 

##### Exercice 3 

> Donner la moyenne et la covariance de la vraisemblance

Posons $A=I-\rho w$
$f_y(y)=\frac{\mid\det(I-\rho w)\mid}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{(AY-XB)^t(AY-XB)}{2\sigma^2})$
Supposons que $A$ est inversible
$$
\begin{align}
f_y(y) &= \frac{\mid\det(I-\rho w)\mid}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{[A(Y-A^{-1}XB)]^t[A(Y-A^{-1}XB)]}{2\sigma^2}) \\
&= \frac{\mid\det(I-\rho w)\mid}{(2\pi\sigma^2)^{d/2}}\exp(-\frac{(Y-A^{-1}XB)^tA^tA(Y-A^{-1}XB)}{2\sigma^2}) \\
&= \frac{\mid\det(I-\rho w)\mid}{(2\pi\sigma^2)^{d/2}}\exp(-(Y-A^{-1}XB)^t(Y-A^{-1}XB)\frac{A^tA}{2\sigma^2})
\end{align}
$$
$u=A^{-1}\times B$, $\Sigma^{-1}=\frac{A^tA}{\sigma^2}$ 

##### Exercice 4

> Trois sites : $S_1=(0,0), S_2=(1,0), S_3=(0,1)$
> $Z(S_1)=1, Z(S_2)=3, Z(S_3)=2$

> Calculer $\gamma(h_{12})$ 

$\frac{1}{2}(Z(S_1)-Z(S_2))^2=\frac{(1-3)^2}{2}=\frac{4}{2}=2$ 

> Calculer $\gamma(1)$

$\frac{1}{2}(Z(S_1)-Z(S_2))^2=\frac{(1-3)^2}{2}=2$ 
$\frac{1}{2}(Z(S_1)-Z(S_3))^2=\frac{(1-2)^2}{2}=\frac{1}{2}$
$\gamma(1)=2+\frac{1}{2}=\frac{5}{2}$  


