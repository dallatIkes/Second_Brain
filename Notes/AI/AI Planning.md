---
aliases:
  - Planification d'IA
  - Automated planning
---
---

A field in [[AI]] that creates action sequences for agents to reach goals

Formalisme : ex : logique du premier ordre (prédicats) -> pas très appropriée 
un mauvais formalisme peut entraîner une contre performance d'un algorithme normalement efficace

chaînage avant : estimations -> heuristiques (heuristique < coût réel : heuristique admissible) (pas bcp de règles + conditions initiales bien formulées)
chaînage arrière : du but à l'état initial (besoin de bcp de règles + but précis)
chaînage mixte possible

algo utilisant une heuristique admissible -> garantit de trouver une solution optimale si elle existe
ex: A* -> Best-First-Search 

ex: Théorie des jeux : jeu des 7 allumettes : MINMAX + $\alpha \beta$ 

---

# [[MDP|Markov Decision Process]]

![[MDP]]

---

# [[RL|Apprentissage par renforcement]]

![[RL]]
