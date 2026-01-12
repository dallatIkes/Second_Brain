# Exercice 1 - Les dominos

$x_1, \ ..., \ x_n = n$ dominos composées de syllabes 
assemblage $<x_i, x_j>$ ssi deuxième syllabe de $x_i \bigoplus$ première syllabe de $x_j$ = mot de la langue française

Graphe

<u>Analyse</u> 

$X :$  vecteur d'entiers de taille n 
$S_i : \{1, \ ..., \ n\}$   
$satisfaisant(x_i) :$ il doit exister un arc entre $X[i-1]$ et $x_i$, et $x_i$ n'a pas déjà été pris (il n'est pas dans $X[1 \ .. \ i-1]$)
$enregistrer(x_i) :$ $x_ix est pris (il n'est plus libre). $X[i]\leftarrow x_i$ 
$soltrouvée : i=n$ 
$défaire(x_i) :$ on libère $x_i$ 

# Exercice 2

# Exercice 3

# Exercice 4 - Crypto-arithmétique

On considère une opération arithmétique sur des lettres

Exemple : 
```
  N E U F
+     U N
+     U N
---------
  O N Z E
```

But : affecter un chiffre (0 à 9) à une lettre sous la condition que le même chiffre ne soit pas affecté à 2 lettres et qu'une lettre vaille toujours le même chiffre. Le résultat de cette opération doit fournir une opération arithmétiquement correcte en base 10.

Exemple de solution :
```
N = 1, E = 9, U = 8, F = 7, O = 2, Z = 4
1987 + 81 + 81 = 2149
```

On supposera disponible une fonction ``calculExact`` qui appelée pour une certaine affectation, rend vrai sir l'opération est correcte et faux sinon.

Soit T un tableau contenant les lettres présentes dans le problème

| N   | E   | U   | F   | O   | Z   |
| --- | --- | --- | --- | --- | --- |

| 1   | 9   | 8   | 7   | 2   | 4   |
| --- | --- | --- | --- | --- | --- |

<u>Analyse</u> : 

$X =$ vecteur de chiffres (tous différents) de taille n
$S_i = \{0, \ ..., \ 9\}$  
satisfaisant$(x_i)$ : le chiffre $x_i$ n'a pas déjà été pris
enregistrer$(x_i)$ : $X[i] \leftarrow x_i; \ x_i \ \mbox{est pris}$ 

```
proédure crypto(ent i);
var ent x_i;
début
	pour x_i allant de 0 à 9 faire:
		si non_pris[x_i] alors:
			X[i] <- x_i;
			pris[x_i] <- vrai;
			si i = ne t calculExact alors
				écrireSol;
			sinon:
				si i < n alors:
					crypto(i+1);
				finSi;
			finSi;
		finSi;
	finPour;
fin;
```
