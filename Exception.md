En [[Java]], lorsqu'une anomalie se produit on appelle une [[Exception]] grâce aux mots clés :
```Java
try{
	// code susceptible de générer une exception
}
catch(ExceptionType name){
	// code exécuté si une exception est détéctée
	name.printStackTrace(); // permet d'afficher cette dernière
}
finally{
	// code toujours exécuté
}
```

On peut également écrire nos propres [[Exception|exceptions]] et les faire renvoyer par des [[Méthode|méthodes]] à l'aide du mot clé:
```Java
static void testMethod() throws Exception{ 
	String test = null; 
	test.toString(); 
}
```

Le système parcours la pile d'appel dans l'ordre inverse. La recherche commence par la [[Méthode]] qui a provoqué l'erreur. Si elle n'a pas de gestionnaire d'[[Exception]], on remonte à la [[Méthode]] qui l'a appelée et ainsi de suite (le parcours de la pile se fait comme dans [[Debugger|gdb]]).

```Java
public class ExoCM{
	private int[] tab = {1, 4, 15, 5};
	public int diviser(int indice, int diviseur)
	{
		return tab[indice]/diviseur;
		// ici trois exceptions sont possibles :
		//    - diviseur = 0
		//    - indice sort de la limite du tableau
		//    - l'utilisateur peut entrer des paramètres du mauvais type
		// Remarque : en dev, on ne fait jamais confiance à l'utilisateur !
	}

	// Dans le main, on ajoutera un try englobant l'appel de la méthode diviser pour ensuite appeler trois catch consécutifs traitant le cas des trois exceptions possibles.
}
```




