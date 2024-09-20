Les [[Socket|sockets]] sont des points d'entrée entre 2 applications du réseau en mode [[Client]]/[[Serveur]]. Ils fournissent une interface pour utiliser les protocoles de transport [[TCP]] et [[UDP]]. Elles permettent l'échange de données à l'aide de mécanismes d[[IO]]. On associe une socket à un [[Port]].

- Stream [[Socket]] en mode [[TCP]]
	- Communication en mode connecté
	- Si la connexion est terminée alors les applications sont informées
- Datagram [[Socket]] en mode [[UDP]]
	- Communication en mode non connecté
	- Données envoyées en paquets indépendants de la connexion

Une fois la connexion établie, on peut créer des flux de communications :
- 2 flux côté [[Client]]:
	- 1 en sortie pour envoyer des données
	- 1 en entrée pour lire des données en provenance du [[Serveur]]
- 2 flux côté [[Serveur]]:
	- 1 en entrée pour recevoir des données du [[Client]]
	- 1 en sortie pour envoyer des données au [[Client]]

![[Pasted image 20240312151438.png]]



