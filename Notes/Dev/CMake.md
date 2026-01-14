Pas un système de [[Compilation]] mais un générateur de script de build ([[Makefile]], Ninja, VS Code, etc...). Concurrent taux autotools. 

Surtout utilisé dans de gros projets qui utilisent beaucoup de bibliothèques qui elles-mêmes utilisent beaucoup de bibliothèques.  (Overkill sinon..)

## Création d'un exécutable
```cmake
add_executable (Demo ${CMAKE_CURRENT_SOURCE_DIR})
```

## Bonnes pratiques
- Compiler dans un répertoire de build
	Ne pas appeler les fonction de [[CMake]] dans le répertoire courant à cause de la création de fichiers (question d'organisation).
- Utiliser les target le plus possible