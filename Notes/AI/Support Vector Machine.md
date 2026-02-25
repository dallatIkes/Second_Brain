---
aliases:
  - SVM
---
---

# Modèle linéaire pour la [[Classification]]

- Une **fonction discriminante** a le rôle de prendre une entrée $x$ et de lui assigner une classe parmi $K$ classes existantes
- Un **classificateur linéaire** utilise une **frontière de décision linéaire** pour assigner les classes aux données

Pour des données en 2d, la frontière est un plan :
![[Pasted image 20251211170136.png]]

En 3d, c'est un plan :
![[Pasted image 20251211170159.png]]

en 4d, un hyperplan, etc...

![[Pasted image 20251211170422.png]]

La **meilleur fonction discriminante** est celle qui **généralise la [[Classification|classification]]** et elle est **stable** par rapport aux nouvelles données

La solution offrant le **maximum de marge** d’erreur peut être une bonne alternative pour une meilleure **généralisation**

Fonction de coût : [[Hinge Loss]]

![[Pasted image 20251211170501.png]]

---

# [[Support Vector Machine|Machine à Support de Vecteurs]]

Il s'agit d'une [[Learning Technique|technique d'apprentissage]] qui permet de trouver la **meilleure frontière de décision**

![[Pasted image 20251211170800.png]]

![[Pasted image 20251211173524.png]]

Avec [[Support Vector Machine|SVM]] on cherche donc : $$\arg\max_w\frac{2}{\lVert w \rVert}$$
ce qui peut être reformulé en $$\arg\min_w\frac{1}{2}\lVert w\rVert^2$$
Mais on ne peut pas juste dériver et trouver la valeur optimale car il y a une contrainte à notre $w$ :
$$(w^Tx^{(i)}+w_0)y^{(i)}\gt1$$

Il faut donc introduire les **multiplicateurs de Lagrange** et notre nouvelle fonction à optimiser devient : $$Q=\frac{1}{2}\lVert w\rVert^2-\sum_{i=1}^n\alpha_i[y^{(i)}(w^Tx^{(i)}+w_0)-1]$$Il n'existe **pas de solution analytique** à ce problème, on le résout donc **numériquement**

L'ensemble des données $x^{(i)}$ pour lesquels $\alpha_i\gt0$ sont appelés **vecteurs de support**

Le vecteur $w$ est réécrit comme une somme pondérée des **vecteurs de supports**. Ces vecteurs se trouvent sur la **marge** et donc satisfont l’équation : $(w^Tx^{(i)}+w_0)y^{(i)}=1$ 

On peut donc retrouver la valeur de $w_0=y^{(i)}-w^Tx^{(i)}$ et faire la **moyenne** pour en obtenir une valeur robuste 

Les données loin de la marge ne fournissent pas d'information sur la solution ($\alpha_i$ nul)

---
# Cas non séparable de [[Support Vector Machine|SVM]] 

Parfois les classes de sont pas **linéairement séparables** :
![[Pasted image 20251211182843.png]]

Dans ce cas l'algo [[Support Vector Machine|SVM]] ne fonctionne pas directement, mais on peu le forcer à **tolérer des erreurs** de [[Classification|classification]]

Pour chaque $x^{(i)}$ on intègre une variable $\xi_i\ge0$ qui mesure la **déviation** par rapport à la marge :
- $0\le\xi_i\le\frac{1}{\lVert w\rVert}$ (entre la frontière et la marge) : **violation de marge**
- $\xi_i\gt\frac{1}{\lVert w\rVert}$ : **point mal classé**
![[Pasted image 20251211183416.png]]

On adapte la contrainte qui devient : $$(w^Tx^{(i)}+w_0)y^{(i)}\ge1-\xi_i$$L'erreur de [[Classification|classification]] globale est défini par : $$\sum_{i=1}^N\xi_i$$On ajoute cette erreur comme pénalité à notre fonction à optimiser :$$Q=\frac{1}{2}\lVert w\rVert^2+C\sum_{i=1}^N\xi_i-\sum_{i=1}^N\alpha_i[(w^Tx^{(i)}+w_0)y^{(i)}-1+\xi_i]-\sum_{i=1}^N\tau_i\xi_i$$avec $\tau_i$ les multiplicateurs de Lagrange et $C$ une constante

On a toujours les **vecteurs à support** avec $\alpha_i\gt0$ 
De plus, les **vecteurs à support** avec $\alpha_i\lt C$ seront sur la **marge** et auront $\xi_i=0$ 
Les vecteur **à l'intérieur de la marge** ou **mal classés** auront $\alpha_i=C$ 

Plus $C$ est petit et plus la **marge** est grande (on peut se permettre d'ignorer la contrainte)
![[Pasted image 20251211184957.png]]

---

# [[Support Vector Machine|SVM]] et frontières de décision non-linéaires

Les performances du [[Support Vector Machine|SVM]] se **détériorent** lorsque les classes des données ne sont **pas linéairement séparables**. Si on veut tout de même l'utiliser, il faut transformer l'espace d'entrée $X$ en un autre espace $X'$ où les classes deviennent **linéairement séparables**. Ce nouvel espace est généralement de **plus grande dimension** et s'appelle l'**espace des caractéristiques**.

![[Pasted image 20251211185410.png]]
![[Pasted image 20251211185448.png]]

On évite de faire **explicitement la transformation** de $\mathbb{R}^D$ vers $\mathbb{R}^M$, on remplace la **produit scalaire** par le **[[Kernel Trick|noyau]] k**

Exemple avec le [[Kernel Trick|noyau Gaussien]] :
![[Pasted image 20251211190001.png]]

---

# Forces et Faiblesses

**Forces :**
- Base **théorique rigoureuse**
- [[Classification]] **efficace**, surtout pour les données de **grande dimension**
- Peut être appliqué aux problèmes **non linéaires** grâce à l'[[Kernel Trick|astuce du noyau]] 
**Faiblesses :**
- Fonctionne uniquement dans un **espace réel** (il faut convertir les valeurs discrètes en valeurs numériques)
- Ne fait que la **[[Classification|classification]] binaire** (on peut toujours faire du One-vs-Rest)
- L'hyperplan obtenu est **difficilement compréhensible** par les humains