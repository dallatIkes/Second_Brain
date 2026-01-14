# Exercice 1
Soit la relation r suivante :

|       | A     | B     | C     | D     |
| ----- | ----- | ----- | ----- | ----- |
| $t_1$ | $a_1$ | $b_1$ | $c_1$ | $d_1$ |
| $t_2$ | $a_1$ | $b_2$ | $c_1$ | $d_2$ |
| $t_3$ | $a_2$ | $b_2$ | $c_1$ | $d_1$ |
| $t_4$ | $a_2$ | $b_2$ | $c_2$ | $d_2$ |

1) Quelles sont les DF du type $elt_1\rightarrow elt_2 : \emptyset$ ?    
Il n'y en a pas.

#Rappel $X\rightarrow Y$ est valide sur r ssi $\forall t_1, t_2 \in r, t_1. X=t_2\cdot X \implies t_1\cdot Y = t_2\cdot Y$  
$A\rightarrow B \ ?$ : non ($t_1$ et $t_2$)  
$A\rightarrow C \ ?$ : non ($t_3$ et $t_4$)  
$A\rightarrow D \ ?$   
$B\rightarrow A \ ?$   
...  
$D\rightarrow C \ ?$  

2) Quelles sont les DF du type $elt_1elt_2\rightarrow elt_3$ ?
Il y en a 2 :
$AD\rightarrow B$
$AD\rightarrow C$

# Exercice 2

Démontrer les propriétés suivantes dur les DF
1) transitivité : $X\xrightarrow{(1)} Y$ et $Y\xrightarrow{(2)} Z \implies X\rightarrow Z$ 
2) augmentation : $X\xrightarrow{(1)} Y$ et $Z\overset{(2)}{\subseteq}W \implies XW\rightarrow YZ$ 
3) pseudo-transitivité : $X\rightarrow Y$ et $YW\rightarrow Z \implies XW\rightarrow Z$ 

1) Supposons (1) et (2) vraies, $\forall t_1, t_2 \in r, \ t_1\cdot X=t_2\cdot X \implies t_1\cdot Y = t_2\cdot Y$ (grâce à (1)) $\implies t_1\cdot Z=t_2\cdot Z$ (grâce à (2))
2) sûrement des trucs
3) tout pareil

# Exercice 3

Soit une relation $R(vol, type\_avion, pilote, jour)$. Modéliser les contraintes suivantes à l'aide de DF :
1) un vol est effectué par un type d'avion donné
2) un jour donné, un type d'avion donné est affecté à un pilote donné
3) un pilote ne pilote que certains jours
4) le dimanche, il n'y a aucun vol

1) $vol\rightarrow type\_avion$ 
2) $jour, type\_avion\rightarrow pilote$ 
3) CE N'EST PAS UNE DF!
4) PAREIL, CE N'EST PAS UNE DF! (TIÉ BÊTE OU QUOI?)

# Exercice 4 

Soit une relation de schéma $(A, B, C, D)$ sur laquelle on trouve trois DFE valides avec deux attributs en partie gauche : $AD\rightarrow B, \ AD\rightarrow C, \ BC\rightarrow A$ 

#Rappel DFE : 
- un seul attribut à droite (a)
- partie gauche minimale (b)

Justifier qu'il n'y a pas de DFE ayant trois attributs en partie gauche

Compte tenu de (b), la seule DFE candidate est : $ABC\rightarrow D$ 
Pourquoi n'est-elle pas valide ?
On a $BC\rightarrow A$ 
Si on avait $ABC\rightarrow D$, on aurait aussi $BC\rightarrow D$
Or, on ne l'a pas. Donc on n'a pas $ABC\rightarrow D$

# Exercice 5

Soit la relation de schéma $R(A,B,C,D,E)$ dotée des DF : $A\xrightarrow{(1)} C, \ CD\xrightarrow{(2)} E, \ D\xrightarrow{(3)} B$ 
Montrer qu'elle possède $AD$ comme clé en utilisant les axiomes d'Armstrong
Il faut montrer que : 
- $AD\xrightarrow{(4)} B, \ AD\xrightarrow{(5)} C, \ AD\rightarrow E$ (on a évidemment $AD\rightarrow AD$ par réflexivité)
- $AD$ est minimal ($A$ n'est pas clé, ni $D$) 

On a $D\rightarrow B \ (3)$ donc par augmentation : $AD\rightarrow B$ 
On a $A\rightarrow C (1)$ donc par augmentation : $AD\rightarrow C$ 
On a $\begin{cases} AD\rightarrow C \ (5) \\ AD\rightarrow D \ (réflexivité) \end{cases} \implies \begin{cases} AD\rightarrow CD \ (transitivité) \\ CD\rightarrow E \ \ \ \ (2) \end{cases} \implies AD\rightarrow E \ (transitivité)$  

# Exercice 6

Soit l'[[Ensemble]] de DF $\mathcal{F}=\{AB\xrightarrow{(1)} C, \ C\xrightarrow{(2)}A, \ BC\xrightarrow{(3)} D, ACD\xrightarrow{(4)} B, \ D\xrightarrow{(5)} EG, \ BE\xrightarrow{(6)} C, \ CG\xrightarrow{(7)} BD, \ CE\xrightarrow{(8)} AG\}$ 
Calculer $BD^+$ en déroulant l'algo de calcul de $X^+$ 

| $X^+_{ancien}$ | DF utilisables ou non encore utilisées | $X^+_{nouveau}$ |
| -------------- | -------------------------------------- | --------------- |
| $BD$           | 5                                      | $BDEG$          |
| $BDEG$         | 6                                      | $BDEGC$         |
| $BDEQGC$       | 2, 3, 7, 8                             | $BDEGCA$        |
| $ABCDEG$       | 1, 4                                   | $ABCDEG$        |
#Rappel Étape 1: éclatement des parties droites
Étape 2 : supprimer les DF redondantes (Attention : on ne peut plus utiliser celles qu'on a supprimées)
Étape 3 : réduction des parties gauches

Étape 1 : $\mathcal{F}=\{AB\xrightarrow{(1)} C, \ C\xrightarrow{(2)}A, \ BC\xrightarrow{(3)} D, ACD\xrightarrow{(4)} B, \ D\xrightarrow{(5)} E, \ D\xrightarrow{(6)} G, \ BE\xrightarrow{(7)} C, \ CG\xrightarrow{(8)} B, \ CG\xrightarrow{(9)} D, \ CE\xrightarrow{(10)} A, \ CE\xrightarrow{(11)} G\}$ Étape 2: 
- $AB\rightarrow C$ est-elle redondante? non $AB^+_{\mathcal{F}-\{AB\rightarrow C\}} = AB$ ne contient pas $C$
- $C\rightarrow A \ ?$ Non car $C^+_{\mathcal{F}-\{C\rightarrow A\}}=C$ ne contient pas $A$ 
- $BC\rightarrow D \ ?$ Non car $BC^+_{\mathcal{F}-\{BC\rightarrow D\}}=BCA$ ne contient pas $D$

# Exercice 7

Soit l'[[Ensemble]] de DF $\mathcal{F}=\{AB\xrightarrow{(1)} C, \ C\xrightarrow{(2)}A, \ BC\xrightarrow{(3)} D, ACD\xrightarrow{(4)} B, \ D\xrightarrow{(5)} EG, \ BE\xrightarrow{(6)} C, \ CG\xrightarrow{(7)} BD, \ CE\xrightarrow{(8)} AG\}$ 
Calculer une couverture minimale de $F$
- $ACD\rightarrow B \ ?$ Oui car $ACD^+_{\mathcal{F}-\{ACD\rightarrow D\}} = ACDEGBF$ contient $B$
Posons $F'=F-\{ACD\rightarrow B\}$ 
- $D\rightarrow E \ ?$ Non car $D^+_{\mathcal{F}'-\{D\rightarrow E\}} = DG$ ne contient pas $E$
- $D\rightarrow G \ ?$ Non car $D^+_{\mathcal{F}'-\{D\rightarrow G\}} = DE$ ne contient pas $G$
- $BE\rightarrow C \ ?$ Non car $BE^+_{\mathcal{F}'-\{BE\rightarrow C\}} = BE$ ne contient pas $C$
- $CG\rightarrow B \ ?$ Non car $CG^+_{\mathcal{F}'-\{CG\rightarrow B\}} = CG$ ne contient pas $B$
- $CG\rightarrow D \ ?$ Oui car $CG^+_{\mathcal{F}'-\{CG\rightarrow D\}} = CGAPD$ contient $D$
Posons $\mathcal{F}''=\mathcal{F}'-\{CG\rightarrow D\}$ 
- $CE\rightarrow A \ ?$ Oui car $CE^+_{\mathcal{F}''-\{CE\rightarrow A\}} = CEA$ contient $A$
Posons $\mathcal{F}'''=\mathcal{F}''-\{CE\rightarrow A\}$ 
-  $CE\rightarrow G \ ?$ Non car $CE^+_{\mathcal{F}'''-\{CE\rightarrow G\}} = CEA$ ne contient pas $G$

Étape 1 : $\mathcal{F}'''=\{AB\xrightarrow{(1)} C, \ BC\xrightarrow{(2)} A, \ BC \xrightarrow{(3)} D, \ D\xrightarrow{(4)} E, \ D\xrightarrow{(5)} G, \ BE\xrightarrow{(6)} C, \ CG\xrightarrow{(7)} B, \ CE\xrightarrow{(8)} G\}$ 

Étape 3 :
Réduction des parties gauches

$BC \longrightarrow D$ : Non : $B \longrightarrow D$ non et $B \longrightarrow D$ non.

$B^+_{\mathcal F'''} = B$ et $C^+_{\mathcal F'''} = CA$

De même pour les autres.

Conclusion : $\mathcal F'''$ est une couverture minimale de $\mathcal F$.

# Exercice 8

Soit $\mathcal{F}=\{A\rightarrow C, \ BC\rightarrow D,  \ ABD\rightarrow E\}$ un [[Ensemble]] de DF définies sur $R(A,B,C,D,E)$.
Montrer que $\mathcal{F}$ n'est pas une couverture minimale.

Étape 1 : OK
Étape 2 : Pas de DF redondantes (elles ont des attributs différentes en partie droite)
Étape 3 : $BC\rightarrow D \ ?$ non
	$B^+_\mathcal{F} = B$
	$C^+_\mathcal{F}  = C$ 
	$ABD\rightarrow E \ ?$
	$AB^+_\mathcal{F} = ABCD\underline{\underline{E}}$
	peut être remplacée par $AB\rightarrow E$ 

# Exercice 9

Soit $R(B,D,I,O,Q,S)$ munie des DF $\mathcal{F}=\{S\rightarrow D, \ I\rightarrow B, \ IS\rightarrow Q, \ B\rightarrow O\}$  
1) Quelles sont les clés de R ?
2) $\mathcal{F}$ est-il une couverture minimale ?

3) #Remarque les attributs qui n'apparaissent en partie droite d'aucune DF sont $I$ et $S$ $\implies$ $I$ et $S$ appartiennent à toute clé
   $IS^+ = ISDBQO \ =$ tous les attributs $\implies$ $IS$ est clé et c'est la seule
2) Étape 1 : OK
   Étape 2 : pas de DF redondantes (attributs différents en partie droite)
   Étape 3 : $IS\rightarrow Q \ ?$ non réductible
		$I^+_\mathcal{F} = ISO$ 
		$S^+_\mathcal{F} = SD$ 

# Exercice 10

Démontrer le théorème de décomposition
#Rappel Soit $r$ une relation de schéma $R(X,Y,Z)$ munie de la DF $X\rightarrow Y$ (ou $X\rightarrow Z$) alors $r = \Pi_{XY}(r)*\Pi_{XZ}(r)$ 
On montre l'inclusion dans les deux sens
1) $r\subseteq \Pi_{XY}(r)*\Pi_{XZ}(r)$ (cf. TD sur l'algèbre relationnelle)
2) $\Pi_{XY}(r)*\Pi_{XZ}(r) \subseteq r$ 
   Soit $t=xyz \in \Pi_{XY}(r)*\Pi_{XZ}(r)$ 
   $\implies xy\in \Pi_{XY}(r)$ et $xz\in \Pi_{XZ}(r)$ (par définition de la jointure)
   $\implies \exists$ un n-uplet $xyz'$ dans $r$ et $\exists$ un n-uplet $xy'z$ dans $r$ (par définition de la projection)
   Or, on a $X\rightarrow Y$ donc $y=y'$ donc $xyz \in r$ 

# Exercice 11

Soit $U=\{C,B,I,A,Q,D\}$ et $\mathcal{F} = \{A\xrightarrow{(1)} D, \ I\xrightarrow{(2)} C, \ IA\xrightarrow{(3)} Q, \ C\xrightarrow{(4)} D\}$  
La décomposition $(AD), \ (IC), \ (IAQ), \ (CB)$ est-elle valide (SPI) ?
-> algo du tableau

|           | $C$      | $B$      | $I$      | $A$      | $Q$      | $D$      |
| --------- | -------- | -------- | -------- | -------- | -------- | -------- |
| **$AD$**  | $b_{11}$ | $b_{12}$ | $b_{13}$ | $a_{4}$  | $b_{15}$ | $a_{6}$  |
| **$IC$**  | $a_{21}$ | $b_{22}$ | $a_{3}$  | $b_{24}$ | $b_{25}$ | $b_{26}$ |
| **$IAQ$** | $b_{31}$ | $b_{32}$ | $a_{3}$  | $a_{4}$  | $a_{5}$  | $b_{36}$ |
| **$CB$**  | $a_{1}$  | $a_{2}$  | $b_{43}$ | $b_{44}$ | $b_{45}$ | $b_{46}$ |
Grâce à la DF (1)

|           | $C$      | $B$      | $I$      | $A$      | $Q$      | $D$         |
| --------- | -------- | -------- | -------- | -------- | -------- | ----------- |
| **$AD$**  | $b_{11}$ | $b_{12}$ | $b_{13}$ | $a_{4}$  | $b_{15}$ | $a_{6}$     |
| **$IC$**  | $a_{21}$ | $b_{22}$ | $a_{3}$  | $b_{24}$ | $b_{25}$ | $b_{26}$    |
| **$IAQ$** | $b_{31}$ | $b_{32}$ | $a_{3}$  | $a_{4}$  | $a_{5}$  | ==$a_{6}$== |
| **$CB$**  | $a_{1}$  | $a_{2}$  | $b_{43}$ | $b_{44}$ | $b_{45}$ | $b_{46}$    |
Grâce à la DF 3

|           | $C$         | $B$      | $I$      | $A$      | $Q$      | $D$      |
| --------- | ----------- | -------- | -------- | -------- | -------- | -------- |
| **$AD$**  | $b_{11}$    | $b_{12}$ | $b_{13}$ | $a_{4}$  | $b_{15}$ | $a_{6}$  |
| **$IC$**  | $a_{21}$    | $b_{22}$ | $a_{3}$  | $b_{24}$ | $b_{25}$ | $b_{26}$ |
| **$IAQ$** | ==$a_{1}$== | $b_{32}$ | $a_{3}$  | $a_{4}$  | $a_{5}$  | $a_{6}$  |
| **$CB$**  | $a_{1}$     | $a_{2}$  | $b_{43}$ | $b_{44}$ | $b_{45}$ | $b_{46}$ |
Grâce à la DF 

|           | $C$      | $B$         | $I$      | $A$      | $Q$      | $D$      |
| --------- | -------- | ----------- | -------- | -------- | -------- | -------- |
| **$AD$**  | $b_{11}$ | $b_{12}$    | $b_{13}$ | $a_{4}$  | $b_{15}$ | $a_{6}$  |
| **$IC$**  | $a_{21}$ | ==$a_{2}$== | $a_{3}$  | $b_{24}$ | $b_{25}$ | $b_{26}$ |
| **$IAQ$** | $a_{1}$  | ==$a_{2}$== | $a_{3}$  | $a_{4}$  | $a_{5}$  | $a_{6}$  |
| **$CB$**  | $a_{1}$  | $a_{2}$     | $b_{43}$ | $b_{44}$ | $b_{45}$ | $b_{46}$ |
On a une ligne de "a" $\implies$ la décomposition est SPI (valide)

Préserve-t-elle les DF ?
$(\bigcup\limits_i \mathcal{F}[R_i])^+=\mathcal{F}^+ \ ?$ 

#Rappel $\mathcal{F}[R_i] =$ l'[[Ensemble]] des DF de $\underline{\underline{\underline{\mathcal{F}^+}}}$ qui ne font intervenir que des attributs de $R_i$ 

$\mathcal{F}[R_1] = \{A\rightarrow D\}$ 
$\mathcal{F}[R_2] = \{I\rightarrow C\}$ 
$\mathcal{F}[R_3] = \{IA\rightarrow Q\}$ 
$\mathcal{F}[R_4] = \{C\rightarrow B\}$ 
$\bigcup\limits_i\mathcal{F}[R_i]=\mathcal{F}$ donc $(\bigcup\limits_i\mathcal{F}[R_i])^+ = \mathcal{F}^+$ donc la décomposition est SPD

Que peut-on dire de la décomposition : $(IAQ), \ (IC), \ (AD), \ (IAB) \ ?$ (SPI? SPD?)


|       | $C$       | $B$       | $I$       | $A$       | $Q$       | $D$       |
| ----- | --------- | --------- | --------- | --------- | --------- | --------- |
| $IAQ$ | ==$a_1$== | ==$a_2$== | $a_3$     | $a_4$     | $a_5$     | ==$a_6$== |
| $IC$  | $a_1$     | ==$a_2$== | $a_3$     |           |           |           |
| $AD$  |           |           |           | $a_4$<br> |           | $a_6$<br> |
| $IAB$ | ==$a_1$== | $a_2$     | $a_3$<br> | $a_4$<br> | ==$a_5$== | ==$a_6$== |
On a une ligne de "a" $\implies$ la décomposition est SPI

$\mathcal{F}[R_1] = \{IA\rightarrow Q\}$ 
$\mathcal{F}[R_2] = \{I\rightarrow C\}$ 
$\mathcal{F}[R_3] = \{A\rightarrow D\}$ 
$\mathcal{F}[R_4] = \{I\rightarrow B\}$ 
Il semble qu'on est perdu $C\rightarrow B$ 
$C^+_{\bigcup\limits_i\mathcal{F}[R_i]}=C$ ne contient pas $B$. On a perdu $C\rightarrow B$ $\implies$ la décomposition n'est pas SPD

# Exercice 13

Énoncé sur papier

On note : 
- $E$ : Emploi
- $Q$ : Qualificatif
- $N$ : Niveau d'études
- $S$ : Salaire
$U=\{E, \ Q, \ N, \ S\}$
On a les DF suivantes : 
- $Q\rightarrow N \ (I_2+R_3)$ 
- $E\rightarrow N \ (I_4+R_5)$ 
- $E\rightarrow Q \ (I_5+R_6)$ 
- $EN\rightarrow S \ (R7)$ 

Soit la relation universelle de schéma $R(E,Q,N,S)$ 
clé(s) de $R$
$R$ est-elle en 2NF? en 3NF?

Il y a une unique clé : $E$
$R$ est en 2NF car la clé est réduite à un attribut
$R$ n'est pas en 3NF car $E\xrightarrow{\nearrow Q\searrow}N$ n'est pas directe, il faut décomposer

Couverture minimale de $\mathcal{F}$ 
Proposer un schéma décomposé 3NF SPI et SPD

Étape 1 : OK
Étape 2 : une DF redondante $E\rightarrow N$ 
Étape 3 : $EN\rightarrow S$ peut être réduite en $E\rightarrow S$ 
$\mathcal{F}'=\{Q\rightarrow N, \ E\rightarrow Q, \ E\rightarrow S\}$ 
Avec l'algo du cours, on obtient : $R_1(\underline{E}, Q, S)$ et $R_2(\underline{Q}, N)$ 

