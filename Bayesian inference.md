**Goal :** learn from data (usually generated from an unknown distribution)
By analyzing data, we want to : 
- Learn about the distribution
- Predict future data
- Make decisions

**Parametric approach :** we assume the distribution family and we estimate the parameters

[[Bayesian inference]] uses three key distributions :
- **Prior :** what we believe before seeing the data
- **Likelihood :** information from the observed data
- **Posterior :** updated belief after combining prior and likelihood

$$
\begin{align}
min_{\theta} \int_{\Omega}{(\theta - \hat{\theta})^2p(\theta|D)d\theta} &= min_{\theta} \int_{\Omega}{l(\hat{\Theta}, \Theta)p(\Theta|D)d\Theta} \\
\end{align}
$$


