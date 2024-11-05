# Exercice 1
Soit la relation r suivante :

|       | A     | B     | C     | D     |
| ----- | ----- | ----- | ----- | ----- |
| $t_1$ | $a_1$ | $b_1$ | $c_1$ | $d_1$ |
| $t_2$ | $a_1$ | $b_2$ | $c_1$ | $d_2$ |
| $t_3$ | $a_2$ | $b_2$ | $c_1$ | $d_1$ |
| $t_4$ | $a_2$ | $b_2$ | $c_2$ | $d_2$ |

1) Quelles sont les DF du type $elt_1\rightarrow elt_2$ ?    
Il n'y en a pas.

#Rappel $X\rightarrow Y$ est valide sur r ssi $\forall t_1, t_2 \in r, t_1. X=t_2\cdot X \implies t_1\cdot Y = t_2\cdot Y$  
$A\rightarrow B \ ?$ : non ($t_1$ et $t_2$)  
$A\rightarrow C \ ?$ : non ($t_3$ et $t_4$)  
$A\rightarrow D \ ?$   
$B\rightarrow A \ ?$   
...  
$D\rightarrow C \ ?$  