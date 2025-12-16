---
aliases:
  - série chronologique
  - TS
---
---
# Temporal phenomena

phénomène aléatoire dans le temps $\rightarrow$ [[Loi de Poisson ]]
granularité/chaîne/résolution $\rightarrow$ mesure d'une valeur qui évolue dans le temps

Problème en [[Data Science|science des données]]

---

# Types de [[Time series|séries chronologiques]]

 - **Univariate :** une seule variable observée
 - **Stationary :** propriétés statistiques constantes dans le temps
 - **Linear :** relation linéaire entre les observations

# Composantes des [[Time series|séries chronologiques]]

- effet saisonnier $(S)$
- tendance (locale ou globale) $(Z)$
- fluctuation aléatoire $(\epsilon)$
- composition de ces dernières $(S+Z+\epsilon), (S\times Z\times\epsilon), ...$ 

![[Pasted image 20251216070123.png]]

# Étude des [[Time series|séries chronologiques]]

- **Nettoyer les données** :
	- Traiter le cas des données manquantes
	- Faire en sorte que les données soient séparées d'un intervalle régulier
	- Transformer les données pour devenir stationnaire (ou retirer les effets saisonniers)
- **Identifier les composantes de la [[Time series|TS]]**
- **Étudier la composante aléatoire :**
	- isoler
	- modéliser
	- injecter dans la prédiction

# Statistiques des [[Time series|séries chronologiques]]

## Espérance
$$\mu_t=\mathrm{E}(Y_t)=\int_\Omega y_tf(y_t)dy_t$$
## Covariance 
$$C_Y(t,r)=\mathrm{Cov}(Y_t,Y_r)=\mathrm{E}[(Y_t-\mu_t)(Y_r-\mu_r)]$$
Propriétés de la Covariance : 
- **symétrie :** $C_Y(t,r)=C_Y(r,t)$
- **variance :** $C_Y(t,t)=\mathrm{Var}(Y_t)$
- **matrice :** décrit comment le processus co-varie en fonction du décalage temporel (lag)

## Autocorrélation
$$R_Y(t,r)=\frac{C_Y(t,r)}{\sqrt{C_Y(t,t)C_Y(r,r)}}=\frac{C_Y(t,r)}{\sqrt{\mathrm{Var}(Y_t)\mathrm{Var}(Y_r)}}$$

Le **corrélogramme** est le représentation graphique des coefficient d'autocorrélation en fonction du lag
![[Pasted image 20251216105427.png]]

# [[Stationnarité]]

![[Stationnarité]]

# [[Ergodicité]]

![[Ergodicité]]

# Estimation des moyens pour séries [[Stationnarité|stationnaires]]

On observe $[y_1,...,y_N]$
- **Moyenne :** $\hat{\mu}=\frac{1}{N}\sum_{t=1}^Ny_t$
- **Covariance :** On crée les paires : $(y_1,y_{1+k}),...,(y_n,y_{n+k})$
  $C_Y(k)=\mathrm{E}[(y_t-\mu)(y_{t-k}-\mu)]=\frac{1}{n}\sum_{t=k+1}^n(y_t-\mu)(y_{t-k}-\mu)$ 

# [[Time series|Séries chronologiques]] de base

## Bruit blanc (White Noise)

$Y_t=e_t$ où :
- les $e_t$ sont indépendants
- $\mathrm{E}(e_t)=0$
- $\mathrm{Cov}(e_t, e_{t-\tau})=\sigma^2\text{ si }\tau=0\text{, sinon }0$
- $e_t\sim\mathcal{N}(0,\sigma^2)$

## Marche aléatoire (Random Walk)

$Y_t=Y_{t-1}+e_t$ où :
- $e_t\sim\mathcal{N}(0,\sigma^2)$
- $\mathrm{Var}(Y_t)=\mathrm{Var}(Y_0)+t\sigma^2\text{ (variance croissante)}$
- Non [[Stationnarité|stationnaire]]
- $e_t=Y_t-Y_{t-1}\text{ est stationnaire}$ 

---

# Modèle autorégressif






---

# [[Variogram]] 

# [[Kriging]]


