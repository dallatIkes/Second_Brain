**Density Based Spatial [[Clustering]] of Applications with Noise** a été conçu pour détecter des clusters de forme arbitraire, caractérisés par une forte densité locale![[Pasted image 20251219204044.png]]

Chaque objet appartenant doit se situer dans une région dense, pour cela on introduit deux valeurs : 
- **Eps :** rayon choisi pour déterminer le voisinage d'un point![[Pasted image 20251219204354.png]]
- **MinPts :** nombre minimum de voisins que devrait avoir un point pour être considéré dans une région dense

On classe trois types d'objets :
- les **points centraux** : situés au cœur d'une région dense
- les **points de bordure :** voisins d'un point central sans en être un
- les **outliers (ou bruit) :** situés dans une zone de faible densité
![[Pasted image 20251219204645.png]]

