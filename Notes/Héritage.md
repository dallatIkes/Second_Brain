Une [[Classe]] dérive d'une autre $\to$ bénéficie des mêmes attributs et [[Méthode|méthodes]] + d'autres plus spécifiques.

ex: la [[Classe]] Chien dérive de la [[Classe]] Animal et en hérite les attributs, [[Méthode|méthodes]] et [[Association|associations]]. 

Si C2 hérite de C1, alors C2 possède tous les attributs et [[Méthode|méthodes]] de C1. Dans ce cas, toute instance de C2 est une instance de C1 ([[Principe de substitution]]).

Même si une [[Classe]] hérite d'une autre, elle ne peut pas accéder à ses attributs privés sans getter. Une solution pour ça est de changer les 
```Java
private double x;
```
en
```Java
protected double x;
```

On peut modifier les attributs. Pareil pour les [[Méthode|méthodes]] : [[Surcharge]] ou [[Redéfinition]].

même chose que super() en [[Python]]

mot clé utilisé : 
```Java 
public class SecondClass extends FirstClass{ 
}
``` 

En [[Java]] l'[[Héritage]] multiple n'existe pas.

Si au moins une méthode d'une classe n'est pas spécifiée (juste la signature) alors il s'agit d'une [[Classe abstraite]].
ex: la méthode manger() de la [[Classe]] Animal n'est pas spécifiée car un Humain et un Lion ne mange pas de la même façon, on laisse donc aux [[Classe|classes]] enfants concrètes de cette [[Classe]] parent abstraite la spécification des différents comportements.

```Java
import java.util.Calendar;

public class Train extends Vehicule{
	private int numero;
	private Calendar depart;
	private Calendar arrivee;

	public Train(float vitesseMaxParam, int nbPlaceParam, String immatriculationParam, Calendar derniereRevisionParam, Calendar anneeMiseEnCirculationParam, Calendar departParam, Calendar arrivee Param){
		super(vitesseMaxParam, nbPlaceParam, immatriculationParam, derniereRevisionParam, anneeMiseEnCirculationParam);
		this.depart = departParam;
		this.arrivee = arriveeParam;
	}
}
```

