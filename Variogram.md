mesure de similarité, prise en compte de la distance (et de l'orientation si [[Isotrope vs Anisotrope|anisotrope]])
variance négative possible dans le cas spatial

#Notation $z(s_i) = z_i$, $z(s_j)=z_j$
$$
\begin{align}
Cov(z_i,z_j) &= E[(z_i-E(z_i))(z_j-E(z_j))] \\
&= E(z_iz_j)-E(z_i)(z_j)-\cancel{E(z_i)E(z_j)}+\cancel{E(z_j)E(z_i)} \\
\end{align}
$$
$z$ est un **Random Process** d'ordre 2
$$E(z_iz_j)-u^2=Cov(z_i,z_j)$$
$$\boxed{E(z_iz_j)=Cov(z_i,z_j)+u^2}$$
$Y=\sum_iw_iz_i$, $\sum_iw_i=0$ 
$$
\begin{align}
Var(Y) &= \sum_i\sum_jw_iw_jCov(z_i,z_j) \\
&= E(Y^2)-E^2(Y) \\
&= E[(\sum_iw_iz_i)^2]-[E(\sum_iw_iz_i)]^2 \\
\text{or } (\sum_iw_iz_i)^2 &=\sum_i\sum_jw_iw_jz_iz_j \\
\text{d'où } Var(Y) &= \sum_i\sum_jw_iw_jE(z_iz_j)-[\sum_iw_iE(z_i)]^2 \\
&= \sum_i\sum_jw_iw_jCov(z_i,z_j)
\end{align}
$$
$$
\begin{align}
\gamma(h_{ij}) &= Var(z_j-z_i) \\
&= E[(z_j-z_i)^2]-[E(z_j-z_i)]^2 \\
&= [z_j^2+z_i^2-2z_iz_j]-\cancel{[E(z_j)-E(z_i)]^2}
\end{align}
$$
Dans le cas stationnaire, $E(z_i)=E(z_j)=u$ donc
$$
\begin{align}
\gamma(h_{ij}) &= E(z_j^2)+E(z_i^2)-2E(z_iz_j) \\
&= 2\sigma^2-2C_{ij}
\end{align}
$$
$$
\begin{align}
\frac{1}{2}\sum_i\sum_jw_iw_j\gamma(h_{ij}) &= \cancel{\frac{1}{2}}\sum_i\sum_jw_iw_j[\cancel{2}\sigma^2-\cancel{2}C_{ij}] \\
&= \sigma^2\sum_i\sum_jw_iw_j-\sum_i\sum_jw_iw_jC_{ij} \\
\end{align}
$$
$\text{Or, } -\sum_i\sum_jw_iw_jC_{ij}=_Var(Y), \text{d'où}$ 
$$
\boxed{\frac{1}{2}\sum_i\sum_jw_iw_j\gamma(h_{ij})\le0}
$$

## Parameters

![[Pasted image 20251125094610.png]]

Intrinsèquement stationnaire $\supset$ stationnaire (2ème ordre) $\supset$ fortement stationnaire
et on ne traite que ce qui est [[Ergodicité|ergodique]] 

le maximum d'un [[Variogram|variogramme]] est la variance