# Exercice 1 - Pavage d'un carré

Soit un échiquier carré de côté $n=2^m$ avec $m\ge0$ 

On veut recouvrir intégralement l'échiquier à l'exception d'une case spéciale donnée $(x, y)$ 
Chaque case doit être recouverte par un seul motif

1) Donner le principe d'une solution de type DpR (et le modèle de division)

$\begin{cases} \mbox{Recouvre}(2^n)\rightarrow 4\mbox{Recouvre}(2^{m-1})+\mbox{pose d'un motif} \\ \mbox{Reouvre}(2^1) \rightarrow \mbox{pose d'un motif} \end{cases}$ 

2) Déterminer la complexité temporelle exacte de la procédure associée avec opération élémentaire = la pose d'un motif

$\begin{cases} \mbox{Nbm}(m) = 4\mbox{Nbm}(m-1)+1=\sum_{i=0}^{n-1}4^i=\frac{4^m-4^0}{4-1}=\frac{(2^m)^2-1}{3}=\frac{n^2-1}{3} \\ \mbox{Nbm}(1)=1 \end{cases}$ 

3) Donner une condition nécessaire (relative à n) pour que le problème posé ait une solution (indépendamment de la façon de le résoudre). 

On doit avoir : $(n^2-1) =$ multiple de 3 

Quand cette condition est satisfaite, peut-on appliquer la méthode DpR proposée au ?paravent ?

Pas forcément : Encore faut-il qu'elle soit satisfaite par chaque sous-problème engendré (on peut montrer que c'est le cas pour un carré de côté $n=2^m$) 

# Exercice 2 - Dessin "en triangles"

Problème d'ordre $n=6$ 

Empilement de lignes composées de triangles isocèles élémentaires

1) Pour un dessin d'ordre $n$, quel est le nombre de triangles élémentaires à tracer ?

Donner le principe et le modèle de division puis écrire l'algo (on supposera disponible une procédure tracer $(x,y)$ qui trace le segment du point courant au point $(x,y)$ (sans modifier $x$ et $y$))

$\begin{cases} \mbox{Triangles}(n) \rightarrow 2\mbox{Triangles}(n-1) + \mbox{tracé d'un triangle élémentaire} \\ \mbox{Triangles}(1) \rightarrow \mbox{tracé d'un triangle élémentaire (ou Triangles}(0) \rightarrow \emptyset\mbox{)} \end{cases}$ 

```
procédure dessin_en_triangles(ent n, réel x, réel y)
	debut
		si n > 0 alors :
			tracer(x-d, y+d);
			dessin_en_triangles(n-1, x-d, y+d);
			tracer(x+d, y+d);
			dessin_en_triangles(n-1, x+d, y+d);
			tracer(x,y);
		finSi
	fin
```

3) Combien de triangles élémentaires sont tracés par cette méthode ?

$\begin{cases} \mbox{Nbtr}(n) = 2\mbox{Nbtr}(n-1)+1 \\ \mbox{Nbtr}(1)=1 \end{cases}$ 

4) On envisage maintenant d'utiliser de façon conjointe deux procédés de type DpR
```
procédure triangles(ent a, réel x, réel y);
début
	si n > 0 alors :
		tracer(x-d, y+d);
		triangles(n-1, x-d, y+d);
fin
```

# Exercice 3 - Le dessin en doubles carrés imbriqués

On veut tracer cette figure avec les contraintes suivantes :
- à la fin du tracé, la plume est revenue au point de départ
- la plume ne doit jamais être levée, ni un trait tracé plusieurs fois

1) Dire pourquoi une stratégie DpR du type :
$Pb(n)\rightarrow TE; \ Pb(n-1)$, où $TE =$ tracé externe
ne peut pas marcher

Quel que soit le point de départ du premier tracé, il ne pourra servir de point de départ au tracé suivant or on n'a pas le droit de lever la plume. 

Quel genre de schéma de division doit-on plutôt considérer ?
$Pb(n)\rightarrow Début\_TE; \ Pb(n-1); \ Fin\_TE;$ 

2) Mettre en évidence (graphiquement) une solution possible instanciant le modèle précédent

3) Déterminer la longueur du tracé en fonction de n et de h $lgtracé(n,h)=$
