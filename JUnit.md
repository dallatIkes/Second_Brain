Environnement de [[Test]] en [[Java]] qui permet la construction de [[Classe|classes]] de [[Test]] selon 4 phases :
- Initialisation (setUp): permet de définir l'environnement de test reproductible. 
- Exercice: exécution du test 
- Vérification (assert): utilisation des méthodes d'assertions, on compare le résultat obtenu avec le résultat défini. Défini le succès ou l'échec du test.  
- Désactivation (tearDown): permet de retrouver l'état initial du système pour ne pas compromettre les tests suivants