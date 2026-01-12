# Concept

**Hypertext Induced Topix Search :** méthode d'analyse de lien qui évalue l'importance des pages web en se basant sur une requête spécifique.

Il attribut à chaque page deux rôles : 
- **autorité :** page reconnue pour sa pertinence sur un sujet précis
  score d'autorité à l'instant $t$ : $a_i^{(t)}=\sum_{j\rightarrow i}h_j^{(t-1)}$ 
- **hub :** centres de ressources pointant vers des autorités
  score de hub à l'instant $t$ : $h_i^{(t)}=\sum_{i\rightarrow j}a_j^{(t)}$ 

> On fixe un seuil de tolérance $\varepsilon$ et on réitère jusqu'à convergence

# Détection de communautés

Il est important de détecter les communautés ou [[Clustering|clusters]] du réseau : 
- comprendre la structure
- identifier les groupes
- analyser les dynamiques
- optimiser des processus
- [[Agrégation Avancée#Détection d'anomalie|détecter des anomalies]]

Une méthode populaire dans les grands réseaux est l'[[Algorithme de Louvain]]



