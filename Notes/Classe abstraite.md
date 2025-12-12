Une [[Classe abstraite]] est non instanciable.

Une [[Classe]] héritant d'une [[Classe]] abstraite ne peut être concrète que si elle définit toutes les [[Méthode|méthodes]] de sa classe mère.

Dans l'exemple des Mammifères dans [[Polymorphisme]], si on veut forcer le développeur à définir la [[Méthode]] seDeplacer pour la [[Classe]] Chien, il faut la rendre abstraite dans la [[Classe]] Mammifère :
```Java
public abstract void seDeplacer();
```

```Java
public class Figure{
	private String nom;
	
	public Figure(String nom){
		this.nom = nom;
	}
	public float calcSurf() {}
}

public class Cercle extends Figure{
	private float rayon;
	
	public Cercle(float rayon){
		super("Cercle");
		this.rayon = rayon;
	}
	public float calcSurf(){
		return Math.PI*this.rayon*this.rayon;
	}
}

public class Rectangle extends Figure{
	private float longueur;
	private float largeur;

	public Rectangle(float longueur, float largeur){
		super("Rectangle");
		this.longueur = longueur;
		this.largeur = largeur;
	}
	public float calcSurf(){
		return this.longueur*this.largeur;
	}
}

public class Cylindre extends Figure{
	private float rayon;
	private float hauteur;

	public Cylindre(float rayon, float hauteur){
		super("Cylindre");
		this.rayon = rayon;
		this.hauteur = hauteur;
	}
	public float calcSurf(){
		return (2*Math.PI*this.rayon*this.rayon)+(this.hauteur*2*Math.PI*this.rayon);
	}
}
```
