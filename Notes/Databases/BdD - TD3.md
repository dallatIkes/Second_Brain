# Exercice 1

Soit la base composée des 3 relations suivantes :
- F(<u>f</u>, nomf, remise, ville)             Fournisseurs
- P(<u>p</u>, nomp, couleurs, origine)   Produits
- M(<u>f, p</u>, qté)                                 Fournitures

Exprimez en AR
1) Le numéro des fournisseurs me fournissant quelque chose
2) Le numéro des fournisseurs ne me fournissant rien
3) Le numéro et le nom des fournisseurs me fournissant quelque chose
4) foo
5) Le numéro des fournisseurs me fournissant au moins un produit vert
6) Le numéro et le nom des fournisseurs de Lannion me fournissant au moins un produit vert en quantité supérieure à 20
7) Le numéro des fournisseurs me fournissant uniquement des produits verts                     $\rightarrow$ différence : (tous les fournisseurs présents dans M) - (ceux qui me fournissent au moins un produit non vert)
8) Le numéro des fournisseurs me fournissant au moins tous les produits verts
9) Le numéro des fournisseurs me fournissant exactement un produit vert
10) Le numéro des fournisseurs qui me fournissent au moins deux produits différents
11) Le numéro des fournisseurs me fournissant au moins k produits verts (k>2)
12) Le numéro de tous les fournisseurs me fournissant au moins 1 produit originaire de sa ville. Proposer 3 expression : 
	- jointure-sélection
	- que des jointures
	- intersection
13) Le numéro des fournisseurs me fournissant à la fois les produits de numéro 6, 9 et 45
14) Le numéro des fournisseurs ne me fournissant aucun produit originaire de Dijon


15) $M[f]$
16) les fournisseurs de F qui ne sont pas dans M $\rightarrow$ différence $F[f]-M[f]$                           ⚠ Ne pas écrire $(F-M)[f]$ 
17) $(F[f=f]M)[f, nomf]$ 
18) Il est impossible d'obtenir les réponses :
	1) {12, 19, 56}
	2) {17, 45, 67, 56}
	car p est clé de P et un même produit ne peut satisfaire 1) et 2) à la fois mais il est possible d'obtenir les réponses :
	3) {chaise, écrou, vis}
	4) {latte}
	car
5) $((P[p=p]M):couleur \ = \ 'vert')[f]$ 
	$((P:couleur='vert')[p][p=p]M[f,p])[f]$ 
6) $(((F:(ville='Lannion'))[f=f]((M:qté>20)[p=p](P:couleur='vert'))))[f, nomf]$ 
	$(((F[f=f]M)[p=p]p):(ville='Lannion' \ et \ qté>20 \ et \ couleur= \ 'vert'))[f, nomf]$ 
7) $M[f]-(M[p=p](p:couleur \ne \ 'vert'))[f]$ 
8) voir TD
9) voir TD
10) voir TD
11) $\rightarrow$ k exemplaires de R
	$R=(M[p=p](p:couleur=\ 'vert'))[f,p]$ 
	$\rightarrow$ $k-1$ jointures
	$\rightarrow$ sélection pour imposer que tous les produits sont différents$$((...\ (R_1[f_1=f_2]R_2)...[f_{k-1}=f_k]R_k):(p_2 \neq p_1 et (p_3 \neq p_1 \ et \ p_3 \neq p_2) et \ ... \ et \ (p_k \neq p_1 \ et \ ... \ et \ p_k \neq p_{k-1}))[f_1]$$
12)  $(((F[f=f]M)[p=p]p):ville \ = \ origine)[f]$ 
	$((F[ville \ = \ origine]P)[\{f,p\}=\{f, p\}]M)[f]$ ou $((F[f=f]M)[{p, ville}={p, origine}]P)[f]$ 
	$((M[p=p]P)[f, origine] \cap F[f, ville])[f]$ 
13) $(((M_1[f_1=f_2]M_2)[f_2=f_3]M_3):p_1=6 \ et \ p_2=9 \ et \ p_3=45)[f_1]$ 