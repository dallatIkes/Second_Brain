Un processus ou une [[Time series|série de données]] est dit **stationnaire** lorsque ses **propriétés statistiques** (espérance, variance, ...) sont **constantes dans le temps**

## Stationnarité forte

$[Y_{t_1},...,Y_{t_m}]$ et $[Y_{t_1+\tau},...,Y_{t_m+\tau}]$ suivent la même distribution avec $\tau=\pm1, \pm2,...$ 

## Stationnarité faible

C'est la plus utilisée : les **moments d'ordre 1 et 2** existent et ne dépendent pas du temps :
-  **moyenne constante :** $\mathrm{E}(Y_t)=\mu\lt\infty$
- **Covariance ne dépend que du lag k :** $\mathrm{E}[(T_t-\mu)(Y_{t-k}-\mu)]=C(k)\lt\infty$

---

# Propriété importante 

Pour une série stationnaire, l'autocorrélation **tend vers 0** quand le lag k augmente

**Exemple :** $Y_t=aY_{t-1}+e_t$
$\rho(k)=a^{\lvert k\rvert}$
$\lvert a\rvert\lt1\implies\rho(k)\xrightarrow[k\rightarrow\infty]{}0$

---

# Exemples

**Série stationnaire :** $Y_t=\mu+\varepsilon_t \text{ où } \varepsilon_t\sim\mathcal{N}(0,\sigma^2)$
- $\mathrm{E}(Y_t)=\mu \text{ (constante)}$
- $\mathrm{Cov}(Y_t,Y_{t-k})=\sigma^2 \text{ si } k=0,\text{ sinon }0$

**Série non-stationnaire :** $Y_t=\mu t+\varepsilon_t$
- $\mathrm{E}(Y_t)=\mu t\text{ (dépendant du temps)}$
