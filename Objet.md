Entité atomique que l'on peut piloter non pas par des [[Méthode|méthodes]] mais par un message qu'il peut interpréter. 

Un [[Objet]] est identifié de manière absolue par son OID.

Un [[Objet]] a également un état.

égalité $\implies$ identité  

En [[Java]] toutes les [[Classe|classes]] [[Héritage|héritent]] implicitement de la [[Classe]] Object. 

La comparaison d'[[Objet]] n'est pas possible en [[Java]] avec l'opérateur "\==". Il va donc falloir implémenter les [[Méthode|méthodes]] equals et hashcode:
- la [[Méthode]] equals est :
	- symétrique
	- transitive
	- réflexive
	- consistante : equals $\implies$ même hashcode
- la [[Méthode]] hashcode est :
	- déterministe
	- même hashcode $\centernot\implies$ equals (collision)

```Java
public class Livre{
	private String titre;
	private String auteur;
	private int nbPages;

	public Livre(){
	}

	public String getTitre(){
		return this.titre;
	}
	public String getAuteur(){
		return this.auteur;
	}
	public int getNbPages(){
		return this.nbPages;
	}

	@Override
	public bool equals(Object obj){
		if(this==obj){
			return true;
		}
		if (obj==null){
			return false;
		}
		if(getClass()!=obj.getClass()){
		return false;
		}
		Livre l = (Livre) obj;
		return Objects.equals(this.titre, l.getTitre())&&Object.equals(this.auteur, l.getAuteur());
	}

	@Override
	public int hashCode(){
		int result = 17;
		result = 31*result+Objects.hashCode(auteur);
		result = 31*result+Objects.hashCode(nbPages);
		result = 31*result+Objects.hashCode(titre);
		return result;
	}
}
```

La [[Méthode]] toString est définie dans la [[Classe]] Object et retourne par défaut le nom de la [[Classe]].
