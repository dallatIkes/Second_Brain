Un [[Thread]] permet l'exécution simultanée de plusieurs processus.

[[Java]] est un langage multi-thread où au moment deux [[Thread|threads]] sont actifs : celui de la [[Java Virtual Machine|JVM]] et celui du [[Garbage collector]]. Or en [[Java]], l'[[Héritage]] multiple n'est pas possible, il faut donc implémenter l'[[Interface]] runnable pour hériter de la [[Classe]] [[Thread]].

Une fois créé, on appelle la [[Méthode]] start qui elle-même va appeler la [[Méthode]] run afin de l'exécuter. On peut également gérer les problèmes d'exclusion mutuelle à l'aide des [[Méthode|méthodes]] wait et sleep qui font office de verrou (cf. [[Sémaphore]]). 

```Java
public class Buffer{
	private int taille;
	
	public Buffer(int taille){
		this.taille = taille;
	}

	public synchronized void enfiler(int message) throws InterruptedException{
		while(buffer.size()==this.taille){
			wait();
		}
		buffer.addLast(message);
		notifyAll();
	}

	public synchronized int defiler() throws InterruptedException{
		while(buffer.size()==0){
			wait();
		}
		notifyAll();
		return buffer.removeFirst();
	}
}
```



