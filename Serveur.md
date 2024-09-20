Le [[Serveur]] est le fournisseur de service qui attend les connexions de la part des [[Client|clients]] et traite les requêtes en même temps.

![[Pasted image 20240312145911.png]]

Le [[Serveur]] peut spécifier une taille de file d'attente où seront stockées toutes les demandes de connexions qui seront ensuite retirée une fois la [[Socket]] créée.

```Java
// création de la socket et association au port 7777 et déclaration de la taille de sa file d'attente
ServerSocket servSocket = new ServerSocket(7777,tailleFileAttente);

// attribut de type socket pour permettre au serveur de prendre connaissance d'une nouvelle connexion afin de discuter avec le client
Socket sock; 
sock = servSocket.accept();
```