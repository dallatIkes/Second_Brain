Un ensemble est une collection d'objets **distincts** de même type.

Ex:  Type ens    -- type d'intérêt
utilise entier, boolean    -- en supposant boolean défini
opérations
	eVide  : $\to$ ens    -- constructeur
	eAjout : ens x entier $\to$ ens    -- constructeur
	eSupp : ens x entier $\to$ ens
	eApp : ens x entier $\to$ boolean
	eEstVide : ens $\to$ boolean

eVide $\to \emptyset$ 

eAjout(eVide, 5) $\to$ {5}
eAjout(eAjout(eVide, 5), 5) $\to$ {5}

eApp eVide x $\to$ F
eApp eAjout(E, y) x $\to$ (x=\=y) OU eApp E x

eSupp eVide x $\to$ eVide
eSupp eAjout(E, y) x $\to$ si (x=\=y) alors E sinon eAjout(eSupp(E, x), y)

Différentes mises en œuvre des ensembles : 

| **Structure simple** | **Cté en temps recherche** | **Cté en temp ajout** | **Cté en temp suppression** |
| ---- | ---- | ---- | ---- |
| tableau trié (recherche dicho ) | O($\log_2(n)$) | O(n) | O(n) |
| liste chaînée (ajout en tête) | O(n) | O(1) | O(n) |
| tableau de boolééns | O(1) | O(1) | O(1) |
| [[ABR]] |   |  |  |


