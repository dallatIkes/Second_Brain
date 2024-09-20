Algorithme de [[Cryptographie]] asymétrique décrit par Ronald Rivest, Adi Shamir et Leonard Adleman.

Utilisation d'une clé privée et d'une clé publique générées à l'aide de nombres premiers très grands.

Plusieurs attaques sont possibles :
- Factorisation de n avec $\phi$ 
- Attaque de Wiener qui permet de récupérer la clé privée à partir de la clé publique
- Attaque des fractions continues
- Attaque de Håstad

L'algorithme étant déterministe, il n'est pas sémantiquement sûr. Il pourrait donc être judicieux d'ajouter de l'aléatoire par la biais d'une schéma de remplissage. Dans ce cas, il faut commencer par encoder le message avant de le chiffrer.