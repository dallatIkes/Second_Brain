# INTRODUCTION 

```SELECT``` $X_1, \ ..., \ X_p$
``FROM`` $R_1, \ ..., \ R_n$ 
``WHERE`` $C$ 

$X_i$ : expressions qui peuvent faire intervenir :
- des attributs
- des fonctions
- des constants
qui peuvent être reliés par des opérations arithmétiques

On peut également utiliser :
- des opérations maniant les chaînes de caractères (exemple : || concaténation)
- des opérations maniant les dates (exemple : - nombre de jours entre deux dates)
```SQL
SELECT e, note*1.5 FROM N;
```

# CLAUSES

## Clause ``SELECT``

--> Le mot clé ``DISTINCT`` permet d'éliminer les doubles
```SQL
SELECT DISTINCT durée FROM M;
```

--> ``SELECT *`` permet de récupérer tous les attributs

--> Pour éviter les ambiguïtés sur les noms d'attribut, on préfixe par le nom de la table
#Exemple On cherche e, nom étudiant, n° module, note
```SQL
SELECT E.e, nom, m, note FROM E,N WHERE E.e = N.e;
```

## Clause ``FROM``

On peut associer un synonyme à un nom de table
```SQL
FROM tabe_1[synonyme_1], ... table_n[synonyme_n]
```

--> Nécessaire notamment quand on fait des auto-jointures
```SQL
FROM NN1, NN2 WHERE N1.e = N2.e AND N1.m != N2.m;
```
La clause ``FROM`` construit un produit cartésien. Pour faire une jointure, il faut préciser la condition de jointure dans la clause ``WHERE``

## Clause ``WHERE``

Peur prendre différentes formes :
- sélection simple : Dans l'expression logique (prédicat) C, on peut utiliser :
	- des opérateurs de comparaison (``=``, ``!=``, ``<``, ``<=``, ``>``, ``>=``)
	- des connecteurs logiques (``AND``, ``OR``, ``NOT``)
		```SQL
		SELECT e FROM E WHERE spécialité = 'INFO' AND année = 2;
```
	- les opérations de test suivants :
		```SQL
		expr [NOT] BETWEEN expr1 AND expr2
```
		```SQL
		SELECT nom FROM M WHERE durée BETWEEN 20 AND 40;
		SELECT e FROM E WHERE nom BETWEEN 'Dupont' AND 'Martin';
```
		```SQL
		expr [NOT] IN (liste_val) 
```
		```SQL
		SELECT nom FROM M WHERE ens IN ('Colbert', 'Durand');
```
		```SQL 
		expr_1 [NOT] LIKE expr_2
		/* Teste l'égalité de deux chaînes (en tenant compte des caractères                 joker dans expr2
		   - % remplace n'importe quelle chaîne
		   - _ remplace n'importe quel caractère */
```
		```SQL
		SELECT * FROM E WHERE nom LIKE 'B%';
```
		```SQL
		nom_colonne IS [NOT] NULL  --valeur inconnue
```
		```SQL
		SELECT e FROM N WHERE note IS NULL;
```

--> On peut exprimer dans la cause ``WHERE`` les conditions de jointure
```SQL
SELECT E.e, nom, m, note FROM E,N WHERE E.e = N.e
```
Variante syntaxique
```SQL
SELECT E.e, nom, m, note, FROM E JOIN N ON E.e = N.e
```

[[BdD - TD4#Exercice 1]]

## Clause ``HAVING`` 

permet de spécifier une condition de recherche au niveau des groupes (complément d'une clause ``GROUP BY``)

#Syntaxe ``HAVING`` condition : la condition peut
- comparer une fonction agrégation à une constante
- comparer une fonction d'agrégation à une autre fonction d'agrégation

## Clause ``ORDER BY``

Permet de trier le résultat sur 1 ou plusieurs attributs
#Remarque ces attributs doivent apparaître dans la clause ``SELECT`` 
#Exemple 
```SQL
SELECT * FROM E ORDER BY nom; -- ordre croissant
SELECT * FROM E ORDER BY nom DESC; -- ordre décroissant
SELECT * FROM N ORDER BY e,m; -- tri imbriqué
```
#Exemple Moyenne des notes de tout étudiant inscrit à plus de 2 modules
```SQL
SELECT e, AVG(note) FROM N GROUP BY e HAVING COUNT(*) > 2;
```

[[BdD - TD4#Exercice 3]]