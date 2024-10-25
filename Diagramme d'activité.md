Les [[Diagramme d'activité|DAC]] permettent de représenter graphiquement le déroulement d'un cas d'utilisation

# Activité

Une **activité** représente une exécution d'un mécanisme selon un déroulement d'étapes séquentielles. C'est le plus petit traitement exprimé en [[UML - Unified Modeling Language|UML]] et peut être rapproché de la notion d'instruction élémentaire. Il est possible de fournir des paramètres en entrée d'une **activité**.

Une **activité** est composée :
- d'actions
- de nœuds de contrôle (fork, merge, decision, join)
- de transition

# Transition

Le passage d'une **activité** vers une autre est matérialisé par une **transition**.

## Transition automatique
```plantuml
:Préparer la commande;
:Envoyer la commande;
```

## Transition conditionnelle
```plantuml
repeat
	:Saisir le code;
	:Vérifier le code;
	repeat while () is (ko) not (ok)
	:Valider paiment;
```

## Nœud de fusion
Nœud de contrôle rassemblant plusieurs flots alternatifs entrants et un flot sortant (ici Envoi 24H et Envoi normal). ⚠ N'est pas utilisé pour la synchronisation!
```plantuml
split
	-[hidden]->
	:Enovyer la commande;
	if () then (envoyer prioritaire) 
		:Envoi 24H;
	else ()
		:Envoi normal;
	endif
split again
	-[hidden]->
	:Recevoir paiement;
end split
:Clôturer commande;
```

## Synchronisation
Aussi appelé nœud d'union, utilisé lorsque plusieurs transitions doivent être terminées avant l'exécution de l'activité  suivante (ici Recevoir paiement et la sortie du nœud de fusion)
```plantuml
split
	-[hidden]->
	:Enovyer la commande;
	if () then (envoyer prioritaire) 
		:Envoi 24H;
	else ()
		:Envoi normal;
	endif
split again
	-[hidden]->
	:Recevoir paiement;
end split
:Clôturer commande;
```

## Parallélisation
```plantuml
:Accepter devis;
split
	:Préparer commande;
split again
	:Établir facture;
end split
stop
```

[[Modélisation - TD DAC]]

