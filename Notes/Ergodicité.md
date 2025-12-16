Lorsque qu'un processus est ergodique, les estimateurs trouvés lors d'une observation, sont les mêmes que pour plusieurs observations.

#Exemple une personne mesure 1000 fois un phénomène et en déduit des estimateurs de ses paramètres. 1000 personnes mesurent chacun 1000 fois le même phénomène et on en déduit les mêmes estimateurs.

---

Une [[Time series|série chronologique]] [[Stationnarité|stationnaire]] est dite [[Ergodicité|ergodique]] si ses moments statistiques peuvent être estimés de manière cohérente à partir d'une seule réalisation suffisamment longue : $$\mathrm{E}(Y_t)=\lim_{T\rightarrow\infty}\sum_{t=1}^T \frac{y_t}{T}$$
#Contre-exemple $Y_t=\begin{cases}\mu_1+\varepsilon_t \text{ si } z=0 \\ \mu_2+\varepsilon_t\text{ si }z=1\end{cases}$
La moyenne converge vers $\mu_1$ ou $\mu_2$ mais jamais vers $\mathrm{E}(Y_t)=\mu_1\mathbb{P}(z=0)+\mu_2\mathbb{P}(z=1)$