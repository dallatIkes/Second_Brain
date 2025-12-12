La déclaration d'une [[Classe paramétrée]] comprend un type paramétré. (Ex: ArrayList déjà implémenté en [[Java]]).

On peut également définir notre propre [[Classe paramétrée]] :
```Java
class Couple<T>{
	private T x, y;
	
	public Couple(T p1, T p2){
		x = p1;
		y = p2;
	}
	
	T getX(){
		return(x);
	}
}
```

Limites : 
- On ne peut pas instancier un type paramétré dans un autre type paramétré (Ex: pas d'ArrayList de Couple)
- Pas de tableau de type paramétré non plus