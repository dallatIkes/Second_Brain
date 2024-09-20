Permet d'inspecter dynamiquement un programme

# gdb

besoin de [[Compilation|compiler]] avec les symboles de debug:
```bash
$ -g -O0
```

## Commandes

![[Pasted image 20240212104343.png]]![[Pasted image 20240212104418.png]]
Remarque : instruction ici est au sens [[C]] et pas [[Assembleur]].

# Valgrind

Utilisation :
```bash
valgrind ./exec
```
équivalent de ``run`` et ``bt``

- **Memcheck** : utilisation de mémoire non initialisée, lecture/écriture sur mémoire libérée, fuite mémoire, erreur de pointeur, etc...
- **Callgrind** : analyse de la pile, détails sur qui appelle quoi et le temps passé sur chaque fonction (passer le callgrind à KCachegrind pour un GUI)![[Pasted image 20240212114924.png]]
- **Massif** : analyse du tas : consommation de la mémoire au cours du temps, optimisation de la taille des structures allouée dynamiquement, massif-visualizer :![[Pasted image 20240212115547.png]] 
