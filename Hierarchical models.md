Accounts for the nested structure of the data

Example : Estimate how study hours affect grades without considering the
school or class context.
- level 1 : individual students
- level 2 : the class where the students are grouped
- level 3 : the departments where the classes are grouped

## Sélection de modèle

**Critères :** 
- Ajuster au mieux les données (max de vraisemblance)
- Réduire au minimum le nombre de paramètres (complexité du modèle)

ex: meilleur modèle s'ajustant au données $= \sum f_{données}$ ajustement parfait mais modèle très complexe.   

**ANTAGONISME** $\rightarrow$ compromis !

meilleur algorithme de sélection de modèle : [[AIC]]
pire algorithme : MDL 

## Simulation de modèle

**Méthode :** [[Markov chain Monte Carlo|MCMC]]  
