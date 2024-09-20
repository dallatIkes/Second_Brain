Le [[Client]] est l'utilisateur du service. Une fois la connexion établie, il effectue une demande de traitement, d'information, … à l'aide d'une requête auprès du [[Serveur]].

Le [[Client]] contact un [[Serveur]] à une [[Adresse IP]] et un [[Port]] spécifiques.

```Java 
// création de socket et envoi de demande de connexion vers la socket du serveur
Socket socket = new Socket();
InetSocketAddress server = new InetSocketAddress(adrServeur, 7777);
socket.connect(server);
```
