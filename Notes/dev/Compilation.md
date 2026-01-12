Production = transformation d'un code écrit dans un langage de programmation en un programme dit exécutable, stocké sur disque.

### Chaîne de production :
- Compilation
	fichier source $\to$ fichier objet
	- le préprocesseur supprime les commentaire et traite les directives #
	- le compilateur : code source $\to$ code [[Assembleur]]
	- l'assembleur crée les fichiers objets
- Édition de lien
	programmes objets $\to$ programmes exécutables

![[Pasted image 20240131141949.jpg]]

En-tête : inclusion : contrat de mise en œuvre (pour éviter les problèmes d'inclusion on utilise les \#ifndef …)
Les fichiers .o peuvent être rangés quelque part dans le disque pour former une bibliothèque (Library). Elles peuvent être statiques(.a) (code copié dans le binaire) ou dynamique(.so) (code copié dans la mémoire au chargement $\to$ plus de temps de chargement mais négligeable - ex : stdio).

Moteur de production - ex : [[Makefile]] ou [[CMake]].

```bash
$ gcc -c -o build/system_utils.o src/system_utils/system_utils.c -Iinclude
$ ar -cvq lib/libsystem_utils.a build/system_utils.o
$ gcc -Wall -fPIC -c -o build/sort.o src/sort/sort.c -Iinclude
$ gcc -Wall -fPIC -c -o build/demo.o src/sort/demo.c -Iinclude
$ gcc -shared build/sort.o build/demo.o -o lib/libsort.so
$ gcc -c apps/Sort.c -o build/Sort.o -Iinclude
$ gcc -o bin/Sort build/Sort.o -L ./lib libsort.so -Wl,-rpath=./lib -lsort -lsystem_utils
```

