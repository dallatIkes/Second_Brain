---
aliases:
  - Arbre de décision
---
---

# Concept de base

Manière d'organiser nos données sous forme d'arbre avec : 
- **Nœud :** test sur la valeur d'un ou plusieurs attributs
- **Branche :** une ou plusieurs valeurs de ce test
- **Feuille :** valeur de l'attribut cible

Exemple où les données sont des jours avec comme attributs leur propriétés météorologique
![[Pasted image 20251212181702.png]]
![[Pasted image 20251212181729.png]]

---

# Choix de l'attribut de décision

On comprend assez bien, qu'un algorithme efficace de création d'[[Decision Tree|Arbre de décision]]
va minimiser la profondeur de l'arbre, et pour cela il faut choisir les bons attributs, on peut se baser sur l'**homogénéité de la valeur cible** ou encore sur le **gain d'information** 

![[Entropie#Théorie de l'information]]

Le principe de l'algorithme **ID3** est d'itérer **récursivement** sur l'ensemble des nœuds et de toujours choisir en **racine** celui qui **maximise le gain**

En appliquant **ID3** à notre exemple précédent, on obtient finalement un arbre optimal :
![[Pasted image 20251212183630.png]]

---

# Classification par [[Decision Tree|Arbre de décision]]

On commence à la racine et on suit simplement la branche avec la valeur de l'attribut correspondant jusqu'à arriver à une feuille et on renvoi son étiquette

---

# C4.5

Dans cette amélioration de l'algorithme ID3, on peut traiter le cas des **attributs numériques** ou de **grande arité**. Il faut définir des **seuils** qui maximise le **rapport de gain** :$$Rapport \ gain(D,a)=\frac{Gain(D,a)}{DivisionInf(D,a)}$$avec $$DivInf(D,a)=\sum_{v\in val(a)}\frac{\lvert D_{a=v}\rvert}{\lvert D\rvert}\log_2(\frac{\lvert D_{a=v}\rvert}{\lvert D\rvert})$$
Exemple :
![[Pasted image 20251212190928.png]]
![[Pasted image 20251212190939.png]]

---

D'autres problèmes peuvent persister, comme le manque de données (dans ce cas, plusieurs options : ignorer cet attribut, calculer la probabilité à partir des données...)
