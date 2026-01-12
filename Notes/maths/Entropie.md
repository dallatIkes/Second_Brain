permet de mesurer le chaos d'un fichier
va de 0 à 8
plus l'[[Entropie]] est grande plus le fichier est chiffré, packé, etc...
ex : fichier C -> ~3-4 et code héxa d'une fichier chiffré -> ~7-8

---

# Théorie de l'information

En théorie de l'information, l'entropie de Shannon est une mesure mathématique de l'incertitude, de la surprise ou du « manque d'information » moyen contenu dans une source de données ou une variable aléatoire
$$H(X)=-\sum_{i=1}^nP(x_i)\log P(x_i)$$
Elle mesure le **nombre de bits** nécessaires pour encoder l'information ou aussi le **degré d'impureté** d'une nœud 

On peut l'utiliser pour calculer le **gain d'information** de nos données $D$ par rapport à un attribut $a_j$ : $$Gain(D,a_j)=H(D)-\sum_{v\in val(a_j)}\frac{\lvert D_{a_j=v}\rvert}{\lvert D\rvert}H(D_{a_j=v})$$