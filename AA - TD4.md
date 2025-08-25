# Exercice 1 

On considère un jeu où on dispose de 2 piles de pièces $P$ et $Q$ contenant respectivement $p$ et $q$ pièces $(p,q>1)$

**But :** atteindre l'une des 2 situations $\begin{cases} p=0,q=1 \\ p=1,q=0\end{cases}$ 

Transitions autorisées : $(p,q)\begin{cases}(p-2,q+1)\\(p+1,q-2)\end{cases}$ 

On veut établir par programmation dynamique le nombre de façons différentes $N[p,q]$ permettant d'atteindre l'un des deux états terminaux à partir de l'état $(p,q)$

1) Donner la formule de récurrence exprimant $N[p,q]$ 

$\begin{cases}N[0,1]=1; \ N[1,0]=1; \ N[1,1]=0 \\ \forall q \ge 2 : N[0,q]=N[1,q-2];N[1,q]=N[2,q-2] \\ \forall p \ge 2 : N[p,0]=N[p-2,1]; N[p,1]=N[p-2,2] \\ \forall p,q \ge : N[p,q] = N[p+1, q-2]+N[p-2,q+1]\end{cases}$

On initialise les cases $[0,1], \ [1,0], \ [1,1]$ grâce à (1) puis on remplit les diagonales par numéro croissant en commençant par le numéro 2. Pour une diagonale donnée : on initialise ses 4 cases extrêmes grâce à (2), puis on décale les autres

# Exercice 2

# Exercice 3

Soit un escalier de $m$ marches que l'ont veut gravir par des sauts de $a_1, \ ..., \ a_p$ marches. On veut calculer le nombre $N(s,m)$ de façons différentes de gravie $m$ marches en $s$ sauts.

<u>exemple :</u> $m=12$, 
$a_1=2, \ a_2=3, \ a_3=5$ 
On peut envisager les enchaînements suivants :
$2,\ 2,\ 2,\ 2,\ 2,\ 2$ 
$3, \ 3, \ 3, \ 3$ 
$3, \ 2, \ 5, \ 2$ 
$2, \ 3, \ 2, \ 3, \ 2$ 
$2, \ 2, \ 3, \ 5$ 

1) Donner la formule de récurrence complète exprimant $N(s,m)$

$N(1,m) = \begin{cases}1 \ si \ \exists i \ tq \ a_i=m \\ 0 \ sinon\end{cases}$                 $(1)$

$N(s,m) = \begin{cases}0 \ si \ m \le min(a_i) \\ \sum_{i=1}^{p}{N(s-1, m-a_i)}\end{cases}$        $(2)$


|       |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  | 11  | 12  |
| :---: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **1** |  0  |  1  |  1  |  0  |  1  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
| **2** |  0  |  0  |  0  |  1  |  2  |  1  |  2  |  2  |  0  |  1  |  0  |  0  |
| **3** |  0  |  0  |  0  |  0  |  0  |  1  |  3  |  3  |  4  |  6  |  3  |  3  |
| **4** |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  1  |  4  |  6  |  8  | 13  |
| **5** |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  1  |  5  | 10  |
| **6** |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  1  |

2) un truc
3) Calculer les valeurs de $N(s,m)$ pour $m\le 12$ et  