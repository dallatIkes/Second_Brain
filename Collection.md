Les [[Collection]] sont des [[Objet]] qui permettent de gérer des ensembles d'objets appelé éléments. Elles sont utilisées pour stocker, gérer et passer en argument à des méthodes des éléments.

En [[Java]], il y a les List, les Set, etc...

![[Pasted image 20240318105422.png]]

On implémente une collection en [[Java]] de la sorte :
```Java
HashSet<String> col = new HashSet<String>();
// Les éléments doivent être de même type, ici String
```

Il existe des [[Méthode|méthodes]] communes à toutes les [[Collection|collections]] comme
```Java
void remove();
int size();
boolean isEmpty();
void clear();
boolean contains(E e);
Iterator iterator();
```

L'[[Interface]] List sert à implémenter les [[Collection|collections]] dont les éléments sont ordonnés (ordre d'insertion) et qui autorise la répétition. Elle est implémentée en [[Java]] grâce aux 
```Java
ArrayList<E> // Tableau dynamique
Vector<E> // Tableau dynamique
LinkedList<E> // List doublement chaînée
```

```Java
Queue<E> // FIFO
Deque<E> // LIFO
```

L'[[Interface]] Set\<E> sert à implémenter une [[Collection]] de type [[Ensemble]] que l'on peut également ordonné selon une [[Relation d'ordre]] qu'il va peut-être falloir définir à l'aide de la [[Méthode]] compareTo() afin d'implémenter un TreeSet.