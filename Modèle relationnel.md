Proposé par [Edgar Frak Codd](https://www.wikiwand.com/fr/articles/Edgar_Frank_Codd) en 1970. Fondé sur la notion mathématique de relation.

# Éléments du modèle

- **Domaine :** ensemble de valeurs
- **Attributs :** variable prenant ses valeurs dans un domaine
- **Relation :** une relation sur les attributs $A_1, \ ..., \ A_n$ de domaines respectifs $D_1, \ ..., \ D_n$ est tout sous-ensemble du produit cartésien $D_1\times ... \times D_n$
- **N-uplet (tuple) :** c'est une occurrence particulière appartenant à la relation
- **Degré :** nombre d'attributs d'une relation (nombre de colonnes de la table)
- **Cardinalité :** nombre de n-uplets d'une relation (nombre de lignes de la table)

Conception d'un schéma relationnel : les propriétés souhaitables pour les relations qu'on veut construire sont :
- éviter la redondance d'information
- les mises à jour devant être faciles à réaliser
#Exemple de mauvais schéma : $(cours, étudiant, note, prof)$ 
- redondance : le nom du prof associé à un cours
- risque d'incohérence : pour modifier la valeur de p, il faut modifier n n-uplets
- anomalie d'insertion : si un étudiant n'a pas encore de note, on ne peut l'inscrire à un cours
- anomalie de suppressions : si on efface les inscriptions des étudiants en fin d'année, on perd la trace du fait que p enseigne c.

# Dépendances fonctionnelles et clé

**Dépendance fonctionnelle (DF) :**
Soit $R$ un schéma de relation $A, B, C, ...$ des attributs de $R$ et $X,Y,Z$ des ensembles d'attributs de $R$. On dit que la relation $r$ du schéma $R$ vérifie la DF $X\rightarrow Y$ ssi $\forall t_1, t_2 \in r, \ t_1.X=t_2.X \Rightarrow t_1.Y = t_2.Y$ (lorsque 2 n-uplets ont même valeur sur les attributs de $X$, ils ont la même valeur sur les attributs de $Y$).

**Propriétés des DF (axiomes d'Armstrong) :**
- réflexivité : $R.A_i \rightarrow R.A_i$ 
- décomposition : $((X\rightarrow Y) \ et \ (Z\subseteq Y))\Rightarrow (X \rightarrow Z)$ 
	$X\rightarrow ABC \Rightarrow X \rightarrow A \ et \ X \rightarrow B \ et \ X \rightarrow C$ 
	on peut se ramener à des DF ayant un seul attribut en partie droite
- additivité (ou union) : $((X\rightarrow Y) \ et \ (X\rightarrow Z)) \Rightarrow (X\rightarrow YZ)$ 
- transitivité : $((X\rightarrow Y) \ et \ (Y\rightarrow Z)) \Rightarrow (X\rightarrow Z)$ 
- pseudo-transitivité : $((X\rightarrow Y) \ et \ (WY\rightarrow Z)) \Rightarrow (XW\rightarrow Z)$ 
- augmentation : $\forall z \subseteq R, (X\rightarrow Y) \Rightarrow (XZ \rightarrow YZ)$ 

### Jointure

#Principe concaténer les n-uplets d'une relation r avec ceux d'une relation s sous réserve qu'une certaine condition soit vérifiée.
une jointure = ($\pm$) un produit cartésien suivi d'une sélection

#Remarque On peut faire la jointure d'une relation avec elle-même

#Notation r\[A=B]s (équijointure)  ou $\bowtie$    

#Généralisation A et B peuvent être des ens. d'attributs

#Définition  $[A=B]s = \{(t\bigoplus t') [\bar{B}] | t \in r \ et \ t' \in s \ et \ t.A = t'.B\}$ où $\bar{B}$ = tous les attributs du produit cartésien r$\times$s sauf B

#Exemple F

| f   | nomf    | remise | ville  |
| --- | ------- | ------ | ------ |
| f1  | Dupont  | 5      | Rennes |
| f2  | Durand  | 7      | Lyon   |
| f3  | Martin  | 5      | Rennes |
| f4  | Mercier | 10     | Paris  |
M


| f   | p   | qté |
| --- | --- | --- |
| f1  | p2  | 50  |
| f3  | p4  | 27  |
| f1  | p4  | 12  |
| f4  | p3  | 15  |
F\[f=f]M = F\*M (jointure naturelle - équijointure sur les attributs communs)
Ex de requête PSJ (projection-sélection-jointure)
Donner les n° des fournisseurs qui fournissent au moins un produit de Dijon.
((M\[p=p]p):(origine='Dijon'))\[f] ou (M\[p=p](p:(origine='Dijon')))\[f]

 #### **$\theta$-jointure**
 $\rightarrow$ jointure ou le comparateur utilisé dans al condition de jointure n'est pas l'égalité
 
 #Notation r\[A $\theta$ B]s ou r $\bowtie_{A \theta B}$ s
 
 #Définition  $r[A \theta B]s = \{(t \bigoplus t') | t \in r$ et $t' \in s$ et $t.A \theta t'.B\}$ 
 Représentation graphique

### Division

#Notation r\[A $\div$ B]s
Soit r une relation de schéma R(A, X) et s une relation de schéma S(B, Y).

#Définition $[A \div B]$ = $\{x|\forall a \in s[B], (a,x) \in r\}$  
$\rightarrow$ on cherche les x qui sont associés dans r à au moins tous les "a" présents dans s

#Exemple R = (num_prod, num_client) $\rightarrow$ r    Commandes
S = (num_prod, libellé) $\rightarrow$ s                  Catalogue
Soit la requête: r\[num_prod $\div$ num_prod]s
Elle retourne les n° des clients qui sont associés dans r à tous les n° de produits présents dans s = les n° des clients qui ont commandé tous les produits du catalogue.

#Def_équivalente $r[A \div B]s = \{x|s[B] \subseteq \Omega_r(x)\}$ avec $\Omega_r(x)$ = $\{a|(a,x) \in r\}$ 

#Exemple

r

| num_prod | num_client | qté |
| -------- | ---------- | --- |
| $p_1$    | $c_1$      | 10  |
| $p_1$    | $c_2$      | 20  |
| $p_2$    | $c_1$      | 30  |
| $p_2$    | $c_3$      | 10  |
| $p_3$    | $c_4$      | 15  |
| $p_3$    | $c_1$      | 7   |
| $p_2$    | $c_2$      | 5   |
| $p_4$    | $c_1$      | 1   |
s

| num_prod | libellé |
| -------- | ------- |
| $p_1$    | $L_1$   |
| $p_2$    | $L_2$   |
| $p_3$    | $L_3$   |
| $p_4$    | $L_4$   |


r\[num_prod $\div$ num_prod]s
s\[num_prod] = $\{p_1, p_2, p_3, p_4\}$ 
client c1
$\Omega_r(c_1) = \{p_1, p_2, p_3, p_4\}$ 

#Remarque Il faut faire attention aux attributs du dividende (r)
X = tous les attributs de r sauf A
Avant d'effectuer la division, il faut éliminer dans r les attributs qui pourraient en parasiter le sens.

Avec r attributs qté dans r, le sens de la requête devient : "trouver les clients ayant commandé tous les produits du catalogue en même quantité"
X = (num_client, qté)

#Remarque la division n'est pas un opérateur primitif. On peut le réécrire : 
r\[A $\div$ B]s = r\[X]-(r\[X]$\times$s\[B]-r)\[X]

## Équivalences de requêtes

Une requête algébrique peut être représentée sous la forme d'un [[Arbre binaire]] où les nœuds intérieurs sont des opérateurs et les feuilles sont des relations.
$\exists$ des équivalences entre séquences d'opérateurs
$\rightarrow$ un arbre donnée possède plusieurs arbres équivalents (sémantiquement)

Dans un SGBD, l'optimiseur de requêtes:
- calcul les arbres équivalents à une requête utilisateur donnée
- estime le coût d'évaluation associé à chaque arbre
- évalue l'arbre le moins coûteux

#Idée_clé diminuer le coût des jointures en restreignant la taille de leurs opérandes (en effectuant le plus tôt les sélections et les projections)

## Principales équivalences utilisées

1) $\Pi_X(\Pi_{XY}(r)) = \Pi_X(r)$
2) $\sigma_{\phi_2}(\sigma_{\phi_1}(r)) = \sigma_{\phi_1}(\sigma_{\phi_2}(r)) = \sigma_{\phi_1 et \phi_2}(r)$ 
3) $\sigma_{\phi_1 ou \phi_2}(r) = \sigma_{\phi_1}(r) \cup \sigma_{\phi_2}(r)$ 
4) $\sigma(\Pi_X(r)) = \Pi_X(\sigma_{\phi}(r))$ si $\phi$ ne concerne que $X$ 
5) $\sigma_\phi(r_1\times r_2)=\sigma_{\phi_1 et \phi_2 et \phi_3}(r_1 \times r_2) = \sigma_{\phi_3}(\sigma_{\phi_1}(r_1)\times \sigma_{\phi_2}(r_2))$ où $\phi = \phi_1 et \phi_2 et \phi_3$ avec
	$\phi_1$ qui ne concerne que des attributs de $r_1$ 
	$\phi_2$ qui ne concerne que des attributs de $r_2$ 
	$\phi_3$ qui concerne à la fois des attributs de $r_1$ et $r_2$ 
6) $\sigma_\phi(r_1 \cup r_2)=\sigma_\phi(r_1)\cup\sigma_\phi(r_2)$
7) $\sigma(r_1\cap r_2)=\sigma_\phi(r_1)\cap\sigma_\phi(r_2)=\sigma_\phi(r_1)\cap r_2=r_1\cap \sigma_\phi(r_2)$
8) $\sigma_\phi(r_1-r_2)=\sigma(r_1)-\sigma_\phi(r_2)=\sigma_\phi(r_1)-r_2$
9) $\Pi_X(r_1\cup r_2)=\Pi_X(r_1)\cup \Pi_X(r_2)$
10) $\Pi_Z(r_1\times r_2)=\Pi_X(r_1)\times\Pi_Y(r_2)$ avec $X$ (resp. $Y$) = le sous-ensemble de $Z$ présent dans $r_1$ (resp. $r_2$)

[[BdD - TD3]] 

# Bloc de base [[SQL]]

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

[[BdD - TD4]]

## Requêtes imbriquées

Dans une commande ``SELECT``, la condition de recherche peut aussi :
- comparer une expression au résultat d'une autre commande ``SELECT``
- tester si une expression est comprise dans le résultat d'une autre commande ``SELECT`` 
- tester si le résultat d'une autre commande ``SELECT`` est non vide

--> Requêtes imbriquées : (autre commande ``SELECT`` = sous-interrogation)
Une sous-interrogation peut être subordonnée au n-uplet en cours alors que celui-ci est évalué par la commande ``SELECT`` externe --> <u>sous-interrogation en corrélation</u> 
```SQL
WHERE expr {=|!=|<|<=|>|>=} {ALL|ANY} (commande SELECT);
```

**ALL :** vrai si la comparaison est vraie pour chacune des valeurs retournées par le ``SELECT`` interne.
#Exemple Liste des numéros et noms des modules ayant la durée maximale
```SQL
SELECT m, nom FROM M WHERE durée >= ALL (SELECT durée FROM M);
```

**ANY :** vrai si la comparaison est vraie pour au moins l'une des valeurs retournées par le ``SELECT`` interne.
#Exemple Liste des numéros des étudiants inscrit à au moins un module où est inscrit l'étudiant 17
```SQL
SELECT e FROM N WHERE m = ANY (SELECT m FROM N WHERE e = 17);
```
#Remarque On pouvait aussi l'écrire de la façon suivante (auto-jointure) :
```SQL
SELECT N1.e FROM NN1,NN2 WHERE N1.m = N2.m AND N2.e = 17;
```

#Remarque Si le ``SELECT`` interne rend une seule valeur, il n'est pas nécessaire de préciser ``ANY`` ou ``ALL``
#Exemple Liste des numéros et noms des étudiants appartenant à la même spécialité que l'étudiant 17
```SQL
SELECT e, nom FROM E WHERE spécialité = (SELECT spécialité FROM E WHERE e = 17);
```

#Remarque On peut faire une comparaison multi-attribut
#Exemple Liste des numéros et noms des étudiants appartenant au même groupe (spécialité et année) que l'étudiant 17
```SQL
SELECT e, nom FROM E WHERE (spécialité, année) = (SELECT spécialité, année FROM E WHERE e = 17);
```

--> **Appartenance ensembliste** 
```SQL
WHERE expr [NOT] IN (commande SELECT)
```
Vrai si ``expr`` appartient au résultat de la sous-interrogation
Faux sinon
#Exemple Liste des numéros et noms des étudiants inscrits à au moins un module optionnel
```SQL
SELECT e, nom FROM E WHERE e IN (SELECT e FROM N);
```

#Remarque ``IN`` est équivalent à ``= ANY`` et ``NOT IN`` est équivalent à ``!= ALL``

#Exemple Liste des numéros et noms des étudiants qui en sont pas inscrits au module 3
```SQL
SELECT e, nom FROM E WHERE e NOT IN (SELECT e FROM N WHERE m = 3);
```

#Remarque On peut généraliser au cas multi-attribut
#Exemple Liste des numéros et noms des étudiants appartenant au même groupe (spécialité, année) qu'un étudiant inscrit au module de Japonais
```SQL
SELECT e, nom FROM E WHERE (spécialité, année) IN (SELECT spécialité, année FROM E,M,N WHERE E.e = N.e AND N.m = M.m AND M.nom = 'Japonais');
```