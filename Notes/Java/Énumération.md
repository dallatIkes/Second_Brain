En [[Java]] une [[Énumération]] se déclare comme une [[Classe]] mais en utilisant le mot clé :
```Java
public class Jour{
	public enum WE {samedi, dimanche};
	private WE jourRepos;
	jourRepos = WE.samedi;
}
```

Une [[Énumération]] peut également avoir des attributs, des [[Méthode|méthodes]] et des [[Constructeur|constructeurs]] (cf. enum Animal dans le cours).

Pratique à utiliser dans un switch (comme le type action dans le projet Bomberman en [[C]] qui n'est rien d'autre qu'un type énuméré : BOMBING, NORTH, EAST, WEST, SOUTH).


