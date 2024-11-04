# Exercice 1
$R(Nom\_F, Adresse\_F, Produit, Prix)$ et $F=\{Nom\_F\rightarrow Adresse\_F, (Nom\_F, Produit)\rightarrow Prix\}$  
Décomposition : $R_1(Nom\_F, Adresse\_F)$ et $R_2(Nom\_F, Produit, Prix)$ STB ?  
$F[R_1] = \{Nom\_F\rightarrow Adresse\_F\}$ et $F[R_2] = \{(Nom\_F, Produit)\rightarrow Prix\}$  
$\bigcup\limits_i F[R_i] = F$ donc $(\bigcup\limits_i F[R_i])^+=F^+$  

# Exercice 2
$R(Etudiant, Examen, Heure, Date)$ la décomposition est SPD  
$F=\{(Etudiant, Examen)\rightarrow (Heure, Date), (Etudiant, Heure, Date)\rightarrow Examen\}$   
Décomposition : $R_1(Etudiant, Examen)$ et $R_2(Etudiant, Heure, Date)$ SPD?  
$\begin{cases} {F[R_1]=\empty} \\  F[R_2]=\empty\end{cases} \implies (\bigcup\limits_i F[R_i])^+=\empty$  
la décomposition n'est pas SPD (on a perdu les 2 DF)  

# Exercice 3
$R(Num\_Vol, Date, Prte, Heure, Dest)$ et $F=\{(Num\_Vol, Date)\xrightarrow{(1)} Porte, Num\_Vol\xrightarrow{(2)} (Dest, Heure), (Date, Porte, Heure)\xrightarrow{(3)} Num\_Vol\}$   
Décomposition : $R_1(Num\_Vol, Dest, Heure)$ et $R_2(Num\_Vol, Porte, Date)$  
$F[R_1] = \{Num_Vol\rightarrow (Dest, Heure)\}$ et $F[R_2]=\{Num\_Vol, Date)\rightarrow Porte\}$  
Il semble qu'on ait perdu la DF (3) : la DF (3) $\notin (\bigcup\limits_i F[R_i])^+$  
Vérifions-le en calculant $(Date, Porte, Heure)^+$ selon $\bigcup\limits_i F[R_i]$ et en montrant qu'on n'obtient pas $Num\_Vol$  
$(Date, Porte, Heure)^+_{\bigcup\limits_i F[R_i]} = \{Date, Porte, Heure\}$ ne contient pas $Num\_Vol  
La décomposition n'est pas SPD