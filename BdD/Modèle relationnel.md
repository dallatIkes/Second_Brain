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

#Définition\[A=B]s = {(t$\bigoplus$t') \[$\bar{B}$] | t $\in$ r et t' $\in$ s et t.A = t'.B} où $\bar{B}$ = tous les attributs du produit cartésien r$\times$s sauf B

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


$r[num\_prod \div num\_prod]s$
$s[num\_prod] = \{p_1, p_2, p_3, p_4\}$ 
client $c_1$
$\Omega_r(c_1) = \{p_1, p_2, p_3, p_4\}$ 

#Remarque Il faut faire attention aux attributs du dividende ($r$)
X = tous les attributs de $r$ sauf $A$
Avant d'effectuer la division, il faut éliminer dans r les attributs qui pourraient en parasiter le sens.

Avec r attributs qté dans r, le sens de la requête devient : "trouver les clients ayant commandé tous les produits du catalogue en même quantité"
$X = (num\_client, qté)$

#Remarque la division n'est pas un opérateur primitif. On peut le réécrire : 
$r[A \div B]s = r[X]-(r[X]\times s[B]-r)[X]$ 

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

**--> Test de non vacuité**
```SQL
WHERE [NOT] EXISTS
```

```SQL
-- Liste des numéros et noms des étudiant inscrits à au moins un cours
SELECT e, nom FROM E WHERE EXISTS (SELECT * FROM N WHERE e = E.e);

-- Liste des numéros et noms des modules auxquels n'est inscrit aucun étudiant d'INFO
SELECT m, nom FROM M WHERE NOT EXISTS (SELECT * FROM N,E WHERE N.e = E.e AND E.spécialité = 'INFO' AND N.m = M.m);
-- variante
SELECT m, nom FROM M WHERE NOT EXISTS (SELECT * FROM N WHERE N.m = M.m AND e IN (SELECT e FROM E WHERE spécialité = 'INFO'));
```

**--> Fonctions d'agrégation**
Prennent des valeurs qui dépendent du groupe de n-uplets retournées par la clause ``WHERE`` 
- ``COUNT(*)`` : nombre de n-uplets
- ``COUNT(nom_col)``: nombre de valeurs $\neq$ ``NULL`` pour l'attribut ``nom_col``
- ``COUNT(DISTINCT nom_col)`` : nombre de valeurs distinctes $\neq$ ``NULL`` pour l'attribut ``nom_col`` 
- ``SUM(nom_col)`` : somme des valeurs
- ``AVG(nom_col)`` : moyenne des valeurs
- ``MAX(nom_col)`` : maximum des valeurs
- ``MIN(nom_col)`` : minimum des valeurs
- ``VARIANCE(nom_col)`` : variance des valeurs
- ``STDDEV(nom_col)`` : écart-type des valeurs

#Remarque les valeurs ``NULL`` sont ignorées
#Remarque ⚠ Les fonctions d'agrégations ne peuvent apparaître que dans une clause ``SELECT`` (ou ``HAVING``) mais **PAS** dans une clause ``WHERE``

#Exemple 
```SQL
-- Nombre d'étudiants inscrits au module 5
SELECT COUNT(*) FROM N WHERE m = 5;

-- Nombre d'étudiants ayant obtenu une note dans le module 5
SELECT COUNT(note) FROM N WHERE m = 5;

-- Durée totale des modules enseignés par Martin
SELECT SUM(durée) FROM M WHERE ens = 'Martin';

-- Note maximale obtenue par un étudiant dans le module de Japonais
SELECT MAX(note) FROM N,M WHERE N.m = M.m AND nom = 'Japonais';
```

[[BdD - TD4]]

**--> Requêtes faisant intervenir un partitionnement de relation**

Clause ``GROUP BY`` : produit un partition, càd un [[Ensemble]] de groupes de n-uplets qui ont les mêmes valeurs pour chacun des attributs spécifiés
```SQL
GROUP BY liste_att;
```

Restriction : dans la clause ``SELECT`` ne peuvent figurer que :
- des fonction aggregation
- des 

#Exemple Nombre de modules où est inscrit chaque étudiant
```SQL
SELECT e, COUNT(*) FROM N GROUP BY e;
```

## Retour sur les [[Modèle relationnel#Éléments du modèle###division|divisions]]

#Exemple Étudiants (n°) inscrits à tous les modules d'au moins 30h
Diviseur = M : durée >= 30
Dividende = $N[E,m]$ 
Requête : $(N[e,m])[m]\div m](M: durée >= 30)$ 
En [[SQL]]: pas d'opération de division --> on reformule la requête : 2 façons de faire :
- double imbrication : tout étudiant tel qu'il n'existe pas de module d'au moins 30h auquel cet étudiant n'est pas inscrit
	```SQL
	SELECT e FROM E WHERE NOT EXISTS (SELECT * FROM M WHERE durée >= 30 AND m NOT IN (SELECT m FROM N WHERE e = E.e));
	```

- comparaison de cardinalité : tout étudiant tel que le nombre de modules d'au moins 30h auxquels il est inscrit est égal au nombre total de modules d'au moins 30h
	```SQL
	SELECT e FROM N WHERE m in (SELECT m FROM M WHERE durée >= 30) GROUP BY e HAVING COUNT(*) = (SELECT COUNT(*) FROM M WHERE durée >= 30);
	-- variante
	SELECT e FROM E WHERE (SELECT COUNT(*) FROM N WHERE e = E.e AND m IN (SELECT m FROM M WHERE durée >= 30)) = (SELECT COUNT(*) FROM M WHERE durée >= 30);
	```

## Fonctions

Pas standardisé (dépend des [[SGBD]])
- Fonctions arithmétiques
	- ABS(n)
	- MOD($n_1$, $n_2$)
	- POWER(n, e)
	- SQRT(n)
	- ...
- Fonctions sur les chaînes
	- LENGTH(ch)
	- SUBSTR(ch, position\[, longueur])
	- UPPER(ch)
	- LOWER(ch)
	- ...
- Fonctions sur les dates
	- ROUND(date, précision)
	- TRUNK(date, précision)
	- SYSDATE()
	- ...
- Nom de l'utilisateur
	- USER()
	- ...

## Opérations ensemblistes

Dans [[MySQL]], seule l'Union est disponible (c'est le seul indispensable)
Les arguments doivent être compatibles (même nombre d'attributs, domaines 2 à 2 les mêmes)

## Les vues

Une vue est une fenêtre dynamique sur un sous-ensemble de la [[Bases de données|base]] (par exemple : un extrait d'une relation ou d'une jointure). S'utilise exactement comme une relation.
On définit une vue à l'aide d'une expression qui :
- spécifie le critère pour sélectionner les n-uplets de la vue
- nomme les attributs retenus (optionnel)

#Exemple On veut créer une vue qui ne comporte que les étudiants d'INFO2
```SQL
CREATE VIEW INFO2 AS SELECT * FROM E WHERE spécialité = 'info' AND année = 2;
```

#Syntaxe de façon générale :
```SQL
CREATE VIEW nom_vue[(nom_attr, ...)] AS SELECT.expr [WITH CHECK OPTION];
-- WITH CHECK OPTION : vérifie que les modifications effectuées aux tables de base grâce à la vue sont conformes à la définition de la vue
```

#Exemple 
```SQL
INSERT INTO INFO2 VALUES(17, 'Bornibus', PHOT, 1);
SELECT * FROM INFO2; -- on ne voit pas Bornibus

-- On rajoute maintenant l'option WITH CHECK OPTION à la vue
CREATE VIEW INFO2 AS SELECT * FROM E WHERE spécialité = 'info' AND année = 2 WITH CHECK OPTION

INSERT INTO INFO2 VALUES(17, 'Bornibus', PHOT, 1);
SELECT * FROM INFO2; -- l'insertion est refusée
```

# Mise à jour des données

- insertion
```SQL
INSERT INTO nom_table [(liste.col)] {VALUES (liste_val)|cmd_SELECT}
```
```SQL
INSERT INTO M VALUES(36, 'Gestion', 'Henry', 30);
INSERT INTO AnciensÉlèves SELECT * FROM E WHERE année = 3;
```
- modification
```SQL
UPDATE nom_table SET nom_col = expr [, ...] [WHERE condition]
```
```SQL
UPDATE N SET note = note+1 WHERE e = 10 AND m = (SELECT m FROM M WHERE nom = 'Japonais');
```
- suppression
```SQL
DELETE FROM nom_table [WHERE condition]
```
```SQL
DELETE FROM M WHERE nom = 'Gestion';
```
⚠ une seule relation concernée pour chacune de ces commandes

# Commandes relatives à l'accès aux données

``GRANT`` : accorde des droits sur une base, une table, une vue, une colonne
``REVOKE`` : supprime des droits

#Exemple 
```SQL
GRANT SELECT ON M TO PUBLIC; -- tout le monde à la droit de lire M
GRANT SELECT, UPDATE ON N TO scolarité; -- scolarité : groupe d'utilisateur
GRANT SELECT, UPDATE(note) ON N TO prof; -- les profs ne peuvent modifier que la colonne note dans N
GRANT ALL ON E TO scolarité; -- on donne tous les droits
```

# Commandes relatives à l'intégrité des données

Faire en sorte que la [[Bases de données|BdD]] soit toujours dans un état cohérent et que chaque utilisateur en ait une vision cohérente.
#Notion = Transaction (= un groupe d'opérations qu'on veut mener à son terme comme s'il s'agissait d'une operation unique ou ne pas exécuter du tout)

#Exemple Transaction : insertion dans $AnciensÉlèves$ et suppression dans E

``COMMIT`` : valide les changement
``ROLLBACK`` annule les changement

#Remarque Par défaut, [[MySQL]] est lancé en mode ``AUTOCOMMIT`` (chaque modification est répercutée immédiatement sur le disque)
Pour le modifier :
```SQL
SET AUTOCOMMIT = 0;
```

[[BdD - TD5]]

# Normalisation (conception de schéma)

## Fermeture transitive et couverture minimale

### Fermeture transitive

Fermeture transitive d'un [[Ensemble]] d'attributs. La fermeture transitive d'un [[Ensemble]] d'attributs $X$, notée $X^+$, représente l'[[Ensemble]] des attributs de $r$ qui peuvent être déduits de $X$ à partir d'une [[Ensemble]] de DF $F$ en appliquant les axiomes d'Armstrong. Ainsi, $Y$ sera inclus dans $X^+$ ssi $X\rightarrow Y$ 

**Algorithme de calcul de $X^+$** 
(1) initialiser $X^+$ à $X$
(2) trouver une DF de $F$ dont la partie gauche est incluse dans $X^+$ 
(3) ajouter à $X^+$ les attributs en partie droite de cette DF
(4) répéter (2) et (3) jusqu'à ce que $X^+$ n'évolue plus

#Exemple Soit $F=\{A\xrightarrow{(1)}D, \ AB\xrightarrow{(2)}E, \ BI\xrightarrow{(3)}E, \ CD\xrightarrow{(4)}I, \ E\xrightarrow{(5)}C\}$ 
Calculer la fermeture transitive de $AE$

| $X^+_{ancien}$ | DF utilisables et non encore utilisée | $X^+_{nouveau}$ |
| -------------- | ------------------------------------- | --------------- |
| $AE$           | (1), (5)                              | $AEDC$          |
| $AEDC$         | (4)                                   | $AEDCI$         |
| $AEDCI$        | __                                    | $AEDCI$         |
l'algorithme s'arrête, $AE^+ = AEDCI$ 

#Exemple Soit $F=\{AB\xrightarrow{(1)}C, \ B\xrightarrow{(2)}D, \ CD\xrightarrow{(3)}E, \ CE\xrightarrow{(4)}GH, \ G\xrightarrow{(5)}A\}$ 
Montrer que la DF $AB\rightarrow E$ est valide
première possibilité : Calculer $AB^+$ et vérifier que $E \in AB^+$ 
deuxième possibilité : le montrer en appliquant les axiomes d'Armstrong
$B\rightarrow D \implies AB \rightarrow D$ par augmentation
$\begin{cases} AB\rightarrow C \\ AB \rightarrow D \end{cases} \implies AB \rightarrow CD$ par union
$\begin{cases} {AB\rightarrow CD} \\ CD\rightarrow E \end{cases} \implies AB \rightarrow E$ par transitivité

#Définition Deux [[Ensemble|ensembles]] de DF sont équivalents s'ils ont la même fermeture transitive

### Couverture minimale

On peut simplifier $F$ en supprimant les DF redondantes càd celles qui peuvent être déduites à partir d'un [[Ensemble]] minimal $F'$ appelé couverture minimale de $F$.

**Algorithme de calcul d'une couverture minimale**  
(1) écrire toutes les DF de $F$ sous la forme $X \rightarrow A$ où $X$ est un groupe d'attributs et $A$ un attribut élémentaire    
Une DF  du type $X\rightarrow A_1A_2...A_n$ est remplacée par $n$ DF $X\rightarrow A_i$  
(2) supprimer les DF redondantes en utilisant la notion de fermeture transitive d'une [[Ensemble]] d'attributs. Une DF $X\rightarrow A$ est redondante ssi $X^+_{F-\{X\rightarrow A\}}$ contient A  
(3) réduire les parties gauches des DF restantes. Une DF $AB\rightarrow C$ peut être réduite en $A\rightarrow C$ ssi $A^+_F$ contient C.

#Exercice Soit l'[[Ensemble]] d'attributs $U=\{A,B,C,D,E,G\}$ et l'[[Ensemble]] de DF $F=\{A\rightarrow B, BC\rightarrow D, AB\rightarrow G, D\rightarrow E, AC\rightarrow DE\}$   
Trouver une couverture minimale de $F$
#Remarque Il peut exister plusieurs couverture minimales  
**Étape 1 :** éclatement des parties droites $F=\{A\rightarrow B, BC\rightarrow D, AB\rightarrow G, D\rightarrow E, AC\rightarrow D, AC\rightarrow E\}$
**Étape 2 :** élimination des DF redondantes
- $A\rightarrow B$ est-elle redondante? non, $A^+_{F-\{A\rightarrow B\}}=A$ ne contient pas $B$
- $BC\rightarrow D$ ? non, $BC^+_{F-\{BC\rightarrow D\}}=BC$ ne contient pas $D$
- $AB\rightarrow G$ ? non, $AB^+_{F-\{AB\rightarrow G\}}=AB$ ne contient pas $G$
- $D\rightarrow E$ ? non, $D^+_{F-\{D\rightarrow E\}} = D$
- $AC\rightarrow D$ ? oui, elle est redondante : $AC^+_{F-\{AC\rightarrow D\}}=ACB\underline{D}...$ contient $D$  
 $F'=F-\{AC\rightarrow D\}$
- $AC\rightarrow E$ ? oui : $AC_{F'-\{AC\rightarrow E\}}=ACBDG\underline{E}$ contient E  
$F''=F'-\{AC\rightarrow E\}$  
$F'' = \{A\rightarrow B, BC\rightarrow D; AB\rightarrow G, D\rightarrow E\}$  

**Étape 3 :** réduction des aprties gauches  
- $BC\rightarrow D$ ? pas réductible     
A-t-on $B\rightarrow D$ ? non, $B^+_{F''}=B$  
A-t-on $C\rightarrow D$ ? non, $C^+_{F''}=C$    
- $AB\rightarrow G$ ? oui  
$A\rightarrow G$ ? oui, $A

On a trouvé une couverture minimale $\{A\rightarrow B, BC\rightarrow D, A\rightarrow G, D\rightarrow E\}$

## Formes normales 

permet de qualifier al qualité d'un schéma

- Première forme nomale (1NF):  
Une relation est en 1NF ssi:
	- elle possède une clé
	- chacun de ses attributs est atomique (monovalué) et on n'a pas de groupes répétitifs d'attributs

Soit une relation $r$ avec les attibuts $n°$, $nom$, $langues\_parlées$  
|$\underline{n°}$|$nom$|$langues\_parlées$|
|----------------|-----|------------------|
|1|Dupont|{Anglais, Allemand}|
|2|Durand|{Russe, Italien, Anglais}|  

Pas une 1NF à cause de l'attribut $langues\_parlées$ 
|$\underline{n°}$|$nom$|$langue_1$|$langue_2$|$langue_3$|
|----------------|-----|----------|----------|----------|
|1|Dupont|Anglais|Allemand|_|
|2|Durand|Russe|Italien|Anglais|  

Pas une 1NF (groupe répétitif d'attributs)

**Solution :** décomposer le schéma  
$r_1(\underline{n°}, nom)$   
$r_2(\underline{n°}, \underline{langue})$  
|$\underline{n°}$|$nom$|
|----------------|-----|
|1|Dupont|
|2|Durand| 

|$\underline{n°}$|$\underline{langue}$|
|----------------|-----|
|1|Anglais|
|1|Allemand|
|2|Russe|
|2|Italien|
|2|Anglais|

- Deuxième forme normale (2NF)  
Une relation est en 2NF ssi :
	- elle est en 1NF
	- tout attribut n'appartenant pas à une clé ne dépend pas fonctionnellement d'une partie de clé (autrement dit : toute DF entre une clé et un attribut n'appartenant pas à une clé est élémentaire)  
	
#Contre-exemple $R(A, B, C, D)$;  $F=\{AB\rightarrow C, A\rightarrow D\}$  
clé de $R$ : $AB$  
$R$ n'est pas en 2NF car $D$ n'appartient pas à une clé mais dépend fonctionnelemnt d'une partie de clé ($A$)  
OU : la FD $AB\rightarrow D$ n'est pas élémentaire (sa partie gauche n'est pas minimale)  
$AB\rightarrow C$ DFE? oui  
$AB\rightarrow D$ DFE? non

**Solution :** décomposer le schéma  
$R_1(\underline{A}, \underline{B}, C)$  
$R_2(\underline{A}, D)$  
- Troisième forme normale (3NF)  
Une relation est en 3NF ssi :
	- elle est en 2NF
	- tout attribut n'appartenant pas à une clé ne dépend pas fonctionnellement d'un autre attribut non clé   

	(autrement dit : toute DF entre une clé et un attribut n'appartenant pas à une clé est directe)  
(autrement dit : une relation où toute DF $X\rightarrow A$ est telle que soit $X$ est une clé, soit $A$ appartient à une clé)

#Contre-exemple $R(A,B,C)$; $F=\{A\rightarrow B, B\rightarrow C\}$  
#Remarque $R$ est une 2NF (la clé est réduite à 1 attribut)  
Clé(s) de R : $A$  
$R$ n'est pas en 3NF  
**Def 1 :** $C$ n'appartient pas à une clé amis dépend fonctionnellement de $B$ qui n'est pas clé  
**Def 2 :** la DF $A\rightarrow C$ n'est pas directe   
**Def 3 :** On a la DF $B\rightarrow C$ où $B$ n'est pas clé et $C$ n'appartient pas à une clé  

**Solution :** on décompose le schéma  
$R_1(\underline{A}, B)$  
$R_2(\underline{B}, C)$  

### Forme normale de Boyce-Codd (BCNF)
Une relation om toute DF a une clé en partie gauche. 

#Remarque plus le degré de normalité d'un schéma est élevé, plus les anomalies de mise à jour sont réduites  
En pratique, on impose au minimum la 3NF  
#Remarque BCNF $\implies$ 3NF (mais la réciproque n'est pas vraie)  
#Exemple illustrant les avantages de la 3NF  
[[Base de données]] comportant des informations sur des machines et des ateliers. On considère 2 schémas :
- (1) $Matériel(\underline{num\_M}, type\_M, num\_A, nom\_A, nbre\_A, chef\_A)$  
les attributs représentent respectivement : le numéro de machine, le type de machine, le numéro de l'atlier, le nom de l'atlier, le nombre de personnes dans l'atelier et le nom du chef d'atelier.
- (2) $Machine(\underline{num\_M}, type\_M, num\_A)$  et  $Atelier(\underline{num\_A}, nom\_A, nbre\_A, chef\_A)$  
$F=\{num\_M\rightarrow type\_M, num\_M\rightarrow num\_A, num\_A\rightarrow nom\_A, num\_A\rightarrow nbre\_A, num\_A\rightarrow chef\_A\}$  

Le schéma (1) est en 1NF et en 2NF mais pas en 3NF (par exemple : la DF $num\_M\rightarrow nom\_A$ n'est pas directe)  
Le schéma (2) est en 3NF (les 2 relations le sont)  

- Aspect redondance  
Supponsons qu'il y ait 30 ateliers différents et 100 machines en moyenne par atelier  
Schéma (1): nombre de valeurs d'attribut stockés ?    
3000 n-uplets $\times$ 6 attributs = 18000 valeurs  
Schéma (2): nombre de valeurs d'attribut stockés ?  
Machine : 3000 $\times$ 3 = 9000  et  Atelier : 30 $\times$ 4 = 120  
Total : 9120 valeurs (On a presque divisé par 2 !)

- Aspect mise-à-jour  
	- changement du nom d'un chef d'atelier :
		- 1 modification dans le schéma (2)
		- 100 modification en moyenne dans le schéma (1)
	- création d'un nouvel atelier :
		- insertion d'une n-uplet dans Atelier pour le schéma (2)
		- possible que si l'atelier possède une machine pour le schéma (1)
	- suppression d'une machine
		- on supprime un n-uplet dans Machine pour le schéma (2)
		- si l'atelier ne possédait que cette machine, on perd les informations sur l'atelier pour le schéma (1)   

### Décomposition sans perte d'information (SPI)

Soit un schéma de relation $R$ qu'on a décomposé en $T=\{R_1, R_2, ..., R_k\}$ et un [[Ensemble]] $F$ de DF. La décomposition est dite <u>SPI sous F</u> ssi $\forall r$ satisfaisant $F$, $r=\Pi_{R_1}(r)\bowtie \Pi_{R_2}(r)\bowtie ... \bowtie \Pi_{R_k}(r)$

#Théorème de décomposition : Soit $R(X,Y,Z)$ un schéma de relation et $r$ une relation de schéma R. Si la DF $X\rightarrow Y$ (ou $X\rightarrow Z$) est valide sur $r$, alors $r=\Pi_{XY}(r)\bowtie \Pi_{XZ}(r)$  
La "méthode des tableaux" permet de vérifier qu'une décomposition est SPI (algo en 3 phases)
- (1) on construit un tableau avec autant de colonnes que d'attributs et autant de lignes que de relations dans le schéma décomposé
- (2) remplissage initial du tableau à l'intersection de la ligne i et de la colonne j : on met $a_j$ si l'attribut $A_j$ appartient au schéma $R_j$, $b_{ij}$ sinon
- (3) pour chaque DF $X\rightarrow Y$ de $F$ on cherche des lignes du tableau pour lesquelles les élements correspondant à tous les attributs de $X$ sont égaux. Si on en trouve, on égalise les éléments de ces lignes pour les attributs de Y. 
	- si au moins un des éléments correspondant à $Y$ est égal à $a_j$, alors tous les autres sont fixés à $a_j$
	- sinon les élements sont égalisés à $b_{ij}$  

A la fin : si une des lignes est remplie de "a" alors la décomposition est SPI (sinon elle ne l'est pas)

#Exercice Soit le schéma $R(Nom\_F, Adresse\_F, Produit, Prix)$ avec les DF   
$F=\{Nom\_F\rightarrow Adresse\_F, (Nom\_F, Produit)\rightarrow Prix\}$  
On considère la décomposition de $R$ en   
$R_1(Nom\_F, Adresse\_F)$ et $R_2(Nom\_F, Produit, Prix)$ est-elle SPI ?  
|    |$Nom\_F$|$Adresse\_F$|$Produit$|$Prix$|
|----|--------|------------|---------|------|
|$R_1$|$a_1$|$a_2$|$b_{13}$|$b_{14}$|
|$R_2$|$a_1$|$b_{22}$|$a_3$|$a_4$|

ligne de "a" : la décomposition est SPI

|    |$Nom\_F$|$Adresse\_F$|$Produit$|$Prix$|
|----|--------|------------|---------|------|
|$R_1$|$a_1$|$a_2$|$b_{13}$|$b_{14}$|
|$R_2$|$a_1$|$a_{2}$|$a_3$|$a_4$|

#Exercice $R(Etudiant, Heure, Date)$ et $F=\{(Etudiant, Examen)\xrightarrow{(1)} (Heure, Date), (Etudiant, Heure, Date)\xrightarrow{(2)} Examen\}$  
Soit la décomposition de $R$ en $R_1(Etudiant, Examen)$ et $R_2(Etudiant, Heure, Date)$ SPI? 
|    |$Etudiant$|$Examen$|$Heure$|$Date$|
|----|--------|------------|---------|------|
|$R_1$|$a_1$|$a_2$|$b_{13}$|$b_{14}$|
|$R_2$|$a_1$|$b_{22}$|$a_3$|$a_4$|    

DF(1) : on ne peut rien faire  
DF(2) : on ne peut rien faire    
Impossible de construire une ligne de "a" : la décomposition n'est pas SPI  

#Exercice $R(Num\_Vol, Date, Porte, Heure, Destination)$ et $F=\{(Num\_Vol, Date)\xrightarrow{(1)} Porte, Num\_Vol\xrightarrow{(2)}(Destination, Heure), (Date, Porte, Heure)\xrightarrow{(3)}Num\_Vol\}$  
Soit la décomposition en $R_1(Num\_Vol, Destination, Heure)$ et $R_2(Num\_Vol, Porte, Date)$  
|    |$Num\_Vol$|$Date$|$Porte$|$Heure$|$Dest$|
|----|----------|------|-------|-------|------|
|$R_1$|$a_1$|$b_{12}$|$b_{13}$|$a_{4}$|$a_5$|
|$R_2$|$a_1$|$a_{2}$|$a_3$|$b_{24}$|$b_{25}$|  

ligne de "a" : la décomposition est SPI  

|       | $Num\_Vol$ | $Date$   | $Porte$  | $Heure$ | $Dest$  |
| ----- | ---------- | -------- | -------- | ------- | ------- |
| $R_1$ | $a_1$      | $b_{12}$ | $b_{13}$ | $a_{4}$ | $a_5$   |
| $R_2$ | $a_1$      | $a_{2}$  | $a_3$    | $a_{4}$ | $a_{5}$ |

### Décomposition préservant les dépendances (SPD)  
Soit un schéma décomposé $T=\{R_1, \ ...,  \ R_k\}$ et un [[Ensemble]] $F$ de DF  
**Projection d'un ensemble de DF sur un schéma de relation**  
$F[z] =$ l'[[Ensemble]] des DF $X\rightarrow Y$ de $\underline{\underline{\underline{F^+}}}$ telles que $XY \subseteq Z$ (fermeture transitive de $F$).  
On dit que $T$ préserve les DF ssi $F[R_1]\cup...\cup F[R_k]$ est équivalent à $F$, autrement dit, ssi $(\bigcup\limits_i F[R_i])^+=F^+$  

[[BdD - TD6]]

### Algorithme de décomposition 3NF (SPI et SPD)
Soit un schéma $R$ et une couverture minimale $F'$ de DF valides sur $R$  
Une décomposition 3NF SPI et SPD est construite de la façon suivante :
- (1) pour chaque DF $X\rightarrow A$ de $F'$, on crée une relation $R_i(\underline{X}, A)$
- (2) si on a plusieurs DF telles que $X\rightarrow A_1, X\rightarrow A_2, \ ..., \ X\rightarrow A_n$ on fusionne les relations correspondantes en une seule relation $R_j(\underline{X}, A_1, ..., A_n)$  

#Exemple Soit les attributs $F$ : titre d'un film, $G$ : genre d'une film, $S$ : salle de cinéma, $H$ : heure de projection, $T$ : technicien de projection.  
Soit les DF : $F=\{F\xrightarrow{(1)} G, \ GH\xrightarrow{(2)} F, \ HS\xrightarrow{(3)} F, \ FH\xrightarrow{(4)} T\}$  
1) Soit la relation universelle $R(F, G, H, S, T)$, Clés de $R$?
#Remarque $H$ et $S$ n'apparaissent en partie droite d'aucune DF $\implies$ $H$ et $S$ s'appartiennent à toute clé  
$HS^+=HSFGT \implies HS$ est clé et c'est la seule
2) $R$ est-elle 
	- en 1NF : oui  
	- en 2NF : oui
		- $HS\rightarrow F$ élémentaire : oui
		- $HS\rightarrow G$ élémentaire : oui
		- $HS\rightarrow T$ élémentaire : oui
	- en 3NF : non
		$HS\rightarrow F\rightarrow G$ n'est pas directe, il faut décomposer $R$
3) Proposer une décomposition 3NF de $R$  
Couverture minimale de $F$ ?
	- étape 1 : rien à faire
	- étape 2 : pas de DF redondante
	- étape 3 : on ne peut réduire aucune partie gauche 

$\rightarrow F$ est une couverture minimale  
L'algo du cours fournit : $R_1(\underline{F},G), \ R_2(\underline{G}, \underline{H}, F), \ R_3(\underline{H}, \underline{S}, F), \ R_4(\underline{F}, \underline{H}, T)$

[[BdD - TD7]]