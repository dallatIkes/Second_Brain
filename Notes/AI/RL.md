---
aliases:
  - Apprentissage par renforcement
  - Reinforcement learning
---
---

L'[[RL|Apprentissage par renforcement]] fait référence au cas où l'[[agent]] doit apprendre à agir <u><strong>seulement à partir des récompenses</strong></u> : il agit, reçois un rétro-action (le renforcement) et son but est de maximiser les récompenses.

# Apprentissage passif

L'[[agent]] a une **politique fixe** et **essaie d'apprendre l'utilité des états** sans connaître $P(s'\vert s,a)$.
Puisqu'on ne connais pas les probabilités, il faut les apprendre par essais successifs, pour ce faire, 3 approches sont possibles 

## Estimation directe

Calculer la moyenne de ce qui est observé dans les essais : pour un état donné, on calcule la somme de toutes les récompenses obtenues à partir de lui et on fait la moyenne sur tous les essais réalisés. Cette moyenne représente une estimation de l'utilité de cet état. (S, lors d'un même essai, on visite plusieurs fois l'état dont on veut estimer l'utilité, on calcule une somme différente à partir de chaque visite).
## Programmation dynamique adaptative

On n'apprend pas directement $U(s)$ mais on cherche plutôt à apprendre le modèle transitionnel $P(s'\vert s, a)$ que l'on utilise pour ensuite calculer l'utilité. Pour cela, on utilise les fréquences des transitions observées : $$P(s'\vert s, a)=\frac{\underset{essais}{\sum}N_{s'\vert sa}}{\underset{essais}{\sum}N_{sa}}=\frac{\text{nombre de transitions de (s,a,s') dans touys les esssais}}{\text{nombre de fois que l'action a est choisie dans tous les essais}}$$
## Différence temporelle

On met à jour l'utilité d'un état à chaque essaie en fonction de l'essaie précédent (initialisée à 0 lors de la première visite de l'état): $$U(s)\leftarrow U(s)+\alpha[R+\gamma U(s')-U(s)]$$avec $\alpha$ le taux d'apprentissage entre $0$ et $1$ et $R$ la récompense $R(s,a,s')$ 

# Apprentissage actif

L'[[agent]] essaie de **trouver une bonne politique** en agissant (similaire à résoudre un [[MDP]]).
Ici, il doit donc décider quelle action effectuer.

## PDA vorace

Une approche est la programmation dynamique adaptative en utilisant un [[Algorithme Glouton]]

## Différence temporelle

L'approche par différence temporelle est également possible

## Q-learning

Le but est d'apprendre la fonction de qualité action-valeur $Q(s,a)$ 