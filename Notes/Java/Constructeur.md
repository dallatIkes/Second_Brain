Permet d'instancier les objets, si aucun n'est déclaré, la [[Java Virtual Machine|JVM]] va en créer un par défaut. Mécanisme aussi appelé : instanciation.

```Java
public class Constructeur1{
	private int i;
	public Constructeur1(int j){
		i=j;
	}
}
```

Le nom d'un [[Constructeur]] est le même nom que celui de la [[Classe]] en [[Java]].
Une [[Classe]] peut avoir plusieurs [[Constructeur|constructeurs]].

```Java
public class LivreExo1{
	// donnees membres
	private String titre;
	private String auteur;
	private int nbPages;

	// Constructeurs
	public LivreExo1(){}

	public LivreExo1(String auteurParam, String titreParam){
		auteur = auteurParam;
		titre = titreParam;
	}

	public LivreExo1(String auteurParam, String titreParam, int nbPagesParam){
		auteur = auteurParam;
		titre = titreParam;
		nbPages = nbPagesParam;
	}
}
```

En ajoutant des getters (accesseurs) et setters (modificateurs) on a :

```Java
public class LivreExo1{
	// donnees membres
	private String titre;
	private String auteur;
	private int nbPages;

	// Constructeurs
	public LivreExo1(){}

	public LivreExo1(String auteurParam, String titreParam){
		auteur = auteurParam;
		titre = titreParam;
	}

	public LivreExo1(String auteurParam, String titreParam, int nbPagesParam){
		auteur = auteurParam;
		titre = titreParam;
		nbPages = nbPagesParam;
	}
	
	// getters
	public String getAuteur(){
		return auteur;
	}

	public String getTitre(){
		return titre;
	}

	public String getNbPages(){
		return nbPages;
	}

	// setters
	public setAuteur(String auteurParam){
		auteur = auteurParam;
	}

	public setTitre(String titreParam){
		titre = titreParam;
	}

	public setNbPages(String nbPagesParam){
		nbPages = nbPagesParam;
	}
}
```
