---
aliases:
  - auto-encodeurs
---
---

# Concept de base

Les [[Autoencoder|auto-encodeurs]] sont une famille de [[Neural networks|réseaux de neurones]] conçus pour apprendre une représentation compacte et informative des données.

## Applications

- réduction de dimension (alternative à [[ACP]], [[UMAP]] et [[t-SNE]])
- détection d'anomalie
- génération de données

![[Pasted image 20251218204924.png]]

**Les [[Autoencoder|auto-encodeurs]] sont robustes à la [[Curse of dimensionality|malédiction de la dimensionnalité]] car ils apprennent à projeter les données dans un espace latent de faible dimension tout en conservant les structures essentielles.**

# Détection d'anomalie

Le [[Neural networks|réseau de neurones]] apprend à reproduire ses entrées en deux étapes :
- **encodeur :** il compresse les données en une représentation latente
- **décodeur :** il reconstruit les données à partir de la compression
L'[[Autoencoder|auto-encodeur]] reconstruit bien ce qu'il connait et mal le reste, ce qui veut dire qu'un écart entre l'entrée et la sortie dépassant un seuil de détection $\eta$ indiquerait une anomalie
![[Pasted image 20251218211959.png]]

## Algorithme

1. Normaliser les données
2. Entraîner l'[[Autoencoder|auto-encodeur]] sur des données normale
3. Calculer l'erreur de reconstruction (par ex: [[MSE]])
4. Définir un seuil de détection
5. Classer les points avec erreurs élevée comme anomalies

# Avantages

- capte les relations non-linéaires
- s'adapte aux données multidimensionnelles
- modèle flexible et généralisable
- détection efficace même en l'absence de labels

---

# Variantes

- Classique
- Denoising
- Sparse
- Variational
- Contractive
- Convolutional
- Seq2Seq
- Masked
- Monte Carlo Dropout