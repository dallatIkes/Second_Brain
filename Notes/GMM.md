---
aliases:
  - Mélange Gaussien
---
---

# Concept de base

Le [[GMM]] est un modèle probabiliste qui représente la **densité de probabilité des données** comme la **somme pondérée de $K$ distributions Gaussiennes** $\mathcal{N}(\mu_k,\Sigma_k)$ correspondant chacune à un [[Clustering|cluster]].

$$p(x\vert\theta)=\sum_{k=1}^K\phi_k\mathcal{N}(x\vert\mu_k,\Sigma_k)$$avec : 
- $\phi_k$ : poids de la composante $k$ (on a $\sum_k\phi_k=1$)
- $\mu_k$ : moyenne du cluster $k$
- $\Sigma_k$ : matrice de covariance du cluster $k$
- $\theta=\{\phi_k, \mu_k, \Sigma_k\}_{k=1}^K$ : les paramètres du modèle

# Apprentissage

L'estimation des paramètres $\theta$ se fait généralement par l'[[Expectation-maximization algorithm|algorithme EM]]

1. **Initialisation :** choix initial de $K$ et des paramètres $\theta$
2. **Étape E :** calcul de la probabilité d'appartenance (responsabilité) $r_{ik}$ du point $x_i$ à chaque composante $k$ $$r_{ik}=\frac{\phi_k\mathcal{N}(x_i\vert\mu_k,\Sigma_k)}{\sum_{j=1}^K\phi_j\mathcal{N}(x_i\vert\mu_j,\Sigma_j)}$$
3. **Étape M :** mise à jour des paramètres $\theta$ pour maximiser la vraisemblance en utilisant les $r_{ik}$
4. **Convergence :** Répéter les étapes E et M jusqu'à la convergence des paramètres ou de la vraisemblance

# Détection d'anomalies

Les anomalies sont les points situés dans les régions de faible densité. On calcule souvent le **score d'anomalie** d'un nouveau point $x$ par l'inverse de sa vraisemblance ou bien l'opposé de sa log-vraisemblance :
$$\mathrm{score}(x)=\frac{1}{p(x\vert\theta)}\text{ ou }\mathrm{score}(x)=-\log p(x\vert\theta)$$si $\mathrm{score}(x)\gt\varepsilon$ alors $x$ est classé comme anomalie

# Avantages

- nature probabiliste
- modélisation flexible
- non supervisé

# Limites

- sensibilité à $K$
- coût de calcul ([[Expectation-maximization algorithm|Algorithme EM]], [[Curse of dimensionality|Malédiction de la dimensionnalité]]) - une solution serait d'appliquer [[ACP]] ou [[UMAP]] avant d'appliquer [[GMM]]
- hypothèse de normalité