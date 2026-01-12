
Langage intermédiaire : [[Compilation|compilé]] en un langage non compréhensible par la machine ([[Byte Code|bytecode]]) qui sera interprété par une [[Java Virtual Machine|JVM]].

[[Programmation Orientée Objet]] $\to$ pas fonctions mais des [[Méthode|méthodes]]

En [[Java]] pas de pointeur mais des références.

Pas de gestion de la mémoire non plus : ramasse-miette ([[Garbage collector]]) de la [[Java Virtual Machine|JVM]] permet de libérer tout seul la mémoire pour les références qui ne servent plus.

Plus haut niveau que le langage [[C]].

variable en [[C]] $\iff$ attribut en [[Java]].
l'attribut est soit primitif (int, bool, etc...) ou non (classe).

```Java
public class DeclarationInitialisation{
	public static void main(String args[]){
		// Déclarer un attribut de type entier
		int monentier;
		// Initialiser l'attribut de type entier à 2
		monentier=2;
		// Déclarer un attribut de type float et l'initialiser à 5.0
		float monfloat = 5.0f
		// Déclarer et initialiser une constante de type long et une autre de type Chaine de caractère (String)
		final long monlong = 123456789L;
		final String s = "mon String!";
	}
}
```


opérateur paresseux en [[C]] $\iff$ opérateur avec court-circuitage en [[Java]].

The main difference between the two is that ``print()`` retains the cursor in the same line after printing the argument, while ``println()`` moves the cursor to the next line.

```Java
public class Tableau{
	public static void main(String args[]){
		int[] tab = new int[5];
		tab[0] = 1;
		tab[1] = 4;
		for(int i=0; i<tab.length; i++)
		{
			System.out.print(tab[i]);
		}
		tab[tab.length-1] = tab[0]+tab[1];
		for(int i=0; i<tab.length; i++)
		{
			System.out.print(tab[i]);
		}
	}
}
```

```Java
public class Matrice{
	public static void main(String args[]){
		int [][] mat = new int[3][];
		
		mat[0] = new int[3];
		mat[0][0] = 10;
		mat[0][1] = 11;
		mat[0][2] = 22;

		mat[1] = new int[2];
		mat[1][0] = ...
	}
}
```

