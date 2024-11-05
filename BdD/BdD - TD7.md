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



