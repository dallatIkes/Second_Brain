Une interface est une [[Classe abstraite]] dont toutes les [[Méthode|méthodes]] sont abstraites et ne possède aucune attributs si ce n'est des constantes. il s'agit d'un contrat de service. Contrairement à une [[Classe abstraite]], on n'utilise pas le mécanisme d'[[Héritage]] mais plutôt d'implémentation. Une [[Classe]] peut implémenter plusieurs [[Interface|interfaces]] alors que l'[[Héritage]] multiple n'existe pas en [[Java]].

mot clé utilisé :
```java
public class C1 implements I{}
```

```Java
// Le mot clé abstract n'est pas obligatoire car les méthodes sont abstraites de base dans une interface
public interface Animal{
	public abstract void crier();
}

public class Chat implements Animal{
	public abstract void crier(){
		System.out.println("Miaou!");
	}
}

public class Chien implements Animal{
	public abstract void crier(){
		System.out.println("Wouaf!");
	}
}

public class Lapin{
}

public class Test{
	public void Test(){
		// Lapin ne peut pas être dans mon tableau car il n'implémente pas Animal
		Animal[] farm = {new Chat(), new Chien()};
		for(int i=.; i<farm.length(); i++){
			farm[i].crier();
		}
	}
}
```

```Java
public interface Geometrie{
	public float calcSurf();
	public float calcPeri();
	public void translate(float x, float y);
}

// Implémenter une classe abstraite Figure qui implémente Geometrie pour ensuite en faire hériter Cercle et Rectangle vu qu'ils ont des attributs en commun. Ces classes héritant d'une classe qui implémente Geometrie, elles l'implémentent aussi.

public class Cercle implements Geometrie{
	private float rayon;
	private float x;
	private float y;

	public void Cercle(float x, floaty, float r){
		this.rayon = r;
	}

	public float calcSurf(){
		return Math.PI*this.rayon*this.rayon;
	}

	public float calcPeri(){
		return 2*Math.PI*this.rayon;
	}

	public void translate(float x, float y){
		this.x += x;
		this.y += y;
	}
}

public class Rectangle implements Geometrie{
	private float longueur;
	private float largeur;
	private float x;
	private float y;

	public void Rectangle(float x, float y, float longueur, float largeur){
		this.x = x;
		this.y = y;
	
		this.longueur = longueur;
		this.largeur = largeur;
	}

	public float calcSurf(){
		return this.longueur*this.largeur;
	}

	public float calcPeri(){
		return 2*(this.longueur+this.largeur);
	}

	public void translate(float x, float y){
		this.x += x;
		this.y += y;
	}
}
```



