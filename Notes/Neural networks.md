---
aliases:
  - Réseau de neurones
---
---

# Concepts de base

L'élément de traitement de base d'un [[Neural networks|réseau de neurones]] est appelé : **perceptron**

Il possède un **vecteur d'entrée** de réels $x=(x_1,x_2,...,x_D)$ qui peut provenir de l'**environnement (entrée)** ou d'un **autre perceptron**

Pour chaque entrée $x_d$ on associe un **poids (synaptique)** $w_d$ 

La sortie $\hat{y}$ est une **somme pondérée des entrées** : $$\hat{y}=f(x)=w_0+\sum_{d=1}^Dw_dx_d$$$w_0$ est appelé **intercept** :
![[Notes/Regression#^372119]]

![[Screenshot from 2025-12-12 12-00-30.png]]

---

# Perceptron et [[Regression|régression]]

Une fois notre réseau en place, il faut estimer **vecteur des poids** $w$, pour ce faire, il y a : 
- la méthode **hors ligne** : on fournit l'ensemble $D$ de données d'un coup
- la méthode **en ligne** : on fournit $D$, donnée par donnée (dans ce cas, la fonction d'erreur peut être définie pour une **donnée à la fois**)

On définit l'**erreur de sortie** produite par un ensemble d'entrainement $(x^{(i)},y{(i)})$ par : $$E^{(i)}(w)=\frac{1}{2}(y^{(i)}-f(x^{(i)}))^2$$Par **montée de gradient**, on recalcule les poids : $$\Delta w_d=\alpha(y^{(i)}-f(x^{(i)})x_d^{(i)}$$En d'autres termes : $$\text{mise à jour}=\text{facteur d'entrainement}\times(\text{sortie désirée}-\text{sortie calculée})\times\text{donnée}$$Et on répète la mise à jour jusqu'à convergence

---

# Perceptron et [[Classification|classification]] binaire

Le **perceptron** définit un **hyperplan** qui divise l'espace des données en deux classes ($C_1$ et $C_2$)
La probabilité à posteriori de la classe $C_1$ est donné par $$g(x)=\frac{1}{1+\exp(-w^Tx)}$$

---

# Perceptron et [[Classification|classification]] multiple

Pour un nombre de classe $K\gt2$, on définit $K$ perceptrons et on utilise la fonction **Softmax**:
![[Pasted image 20251212123041.png]]

---

# Perceptron multi-couches

Le problème avec les perceptrons uni-couche est qu'il ne peuvent approximer que les **fonctions linéaires**. Cependant, en utilisant des **couches intermédiaires** en plus (aussi appelées **cachées**), on peut faire de la **[[Regression|régression]]** et de la **[[Classification|classification]]** **non-linéaire**

![[Pasted image 20251212123401.png]]

Chaque couche cachée a également son **intercept** et prend en entrée la sortie de la **couche précédente**

La mise à jour des poids se fait par le **règle de chaîne (backpropagation)**  (en utilisant la méthode [[SGD]] par exemple) : $$
\begin{align}
\Delta w_{ld} &= \alpha\frac{\partial E^{(i)}}{\partial w_{ld}} \\
&= \alpha \frac{\partial E^{(i)}}{\partial h}\times\frac{\partial h^{(i)}}{\partial f_l}\times\frac{\partial f_l^{(i)}}{\partial w_{ld}} \\
&= \alpha(y^{(i)}-h^{(i)})\times v_l\times f_l^{(i)}(1-f_l^{(i)})x_d^{(i)}
\end{align}$$Preuve :
![[Pasted image 20251212124152.png]]

---

# Fonction d'activation

Ce sont les fonctions d'activation qui permettent l'introduction de la non-linéarité dans les [[Neural networks#Perceptron multi-couches|couches cachées]]. Elle transforment la sortie d'un perceptron en une valeur activée permettant l'apprentissage de frontières de décision non linéaires.

**Exemples :** 
- **sigmoïde :** $\phi(z_k)=\frac{1}{1+e^{-z_k}}$ 
- **tanh :** $\phi(z_k)=\tanh(z_k)$
- **ReLU :** $\phi(z_k)=\max(0,z_k)$
![[Pasted image 20251218210207.png]]
