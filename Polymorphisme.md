Revoir l'exemple du lion avec la [[Surcharge]] de la [[Méthode]] afficher()

Capacité pour une entité de prendre plusieurs formes. Méthode de conception consistant à ajouter de l'abstraction par rapport au type des données manipulées.
Possible grâce au [[Lien dynamique]] et au [[Surclassement]].

```Java
public class Mammifere{
	private int nbPates;
	
	public Mammifere(int nbPates){
		this.nbPates = nbPates
	}
	public void seDeplacer(){
		System.out.println("Je me déplace");
	}
}

public class Baleine extends Mammifere{
	public Baleine(int NbPates){
		super(nbPates);
	}
	@Override
	public void seDeplacer(){
		System.out.println("Je nage!");
	}
}

public class Humain extends Mammifere{
	private age;
	public Humain(int nbPates, int age){
		super(nbPates);
		this.age = age;
	}
	@Override
	public void seDeplacer(){
		System.out.println("Je marche");
	}
}

public class Chien extends Mammifere{
	public Chien(){}
}

public class Test{
	public void main()
	{
		Mammifere[] tab = new Mammifere[4];
		tab[0] = new Mammifere(4);
		tab[1] = new Baleine(0);
		tab[2] = new Humain(2);
		tab[3] = new Chien;
		for(int i=0: i<tab.length; i++){
			tab[i].seDeplacer();
		}
	}
}
```
