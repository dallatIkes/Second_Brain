# Exercice 1

a) Après avoir fermé une commande, le processus s’arrête.
```plantuml
: Fermer commande;
stop
```

b) Le processus commence par la réception d’une commande (il est en attente de la
commande).
```plantuml
start
:Réception commande;
```

c) On vérifie la transaction financière puis on envoie la commande.
```plantuml
:Vérifier la transaction;
:Envoyer la commande;
```

d) Le service commande vérifie la transaction financière puis le service de livraison
envoie la commande.
```plantuml
start
:Réception commande;
if() then (acceptée)
	:Livrer la commande;
else (refusée)
	:Annuler;
endif
stop
```

e) Après réception d’une demande de commande, soit la commande est acceptée et
elle est livrée, soit elle est rejetée et fermée.
```plantuml
start
:Réception d'une commande;
if() then (refusée)
	:Annuler;
else (acceptée)
	:Livrer la commande;
endif
stop
```

f) Après avoir accepté une commande, on envoie la commande et la facture.
```plantuml
start
:Accepter la commande;
fork
	:Envoyer la commande;
fork again
	:Envoyer la facture;
endfork
stop
```

# Exercice 2

Modélisation d'un retrait au DAB

```plantuml
start
:Insérer carte bancaire;
:Taper le code;
if () then (Code bon)
	:Retirer tout l'argent de la banque;
else (Code mauvais)
	:Avaler la carte;
	:Appeler la police;
	stop
endif
stop
```

# Exercice 5

```plantuml
start
fork
	:Casser le chocolat;
	: Faire fondre le chocolat;
fork again
	:Casser les oeufs;
	:Jaune]
end fork
```
