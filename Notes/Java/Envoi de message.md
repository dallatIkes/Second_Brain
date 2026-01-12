Mécanisme qui permet de déclenchement d'un comportement pour un [[Objet]].

```Java
Voiture voit = new Voiture()
voit.affiche()
// voit n'apelle pas une méthode mais reçoit le message "affiche" pour ensuite chercher dans sa classe (et puis éventuellement dans sa classe parent) la méthode affiche
```

