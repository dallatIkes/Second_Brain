# Concept

[[Algorithme Glouton]] visant à optimiser la [[Modularité|modularité]] d'une partition de réseau 

On calcule le gain de modularité après avoir déplacé $i$ dans $\Omega_k$ 
$$\Delta Q^{\Omega_k}=\frac{d_{i,in}^{\Omega_k}}{m}-\frac{d_i\Sigma_{tot}^{\Omega_k}}{2m^2}$$avec : 
- $m$ le nombre total d'arrête du graphe
- $d_{i,in}^{\Omega_k}$ la somme des poids des arrêtes entre $i$ et $\Omega_k$
- $d_i$ le degré de $i$
- $\Sigma_{tot}^{\Omega_k}$ la somme des degrés des points dans $\Omega_k$ 

# Avantages

- efficacité
- hiérarchique
- optimisation de la modularité

# Limites

- limite de résolution pour les petites communautés
- dépendance à l'ordre des nœuds (car [[Algorithme Glouton]] donc maximum local)