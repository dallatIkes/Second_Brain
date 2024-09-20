En [[Java]] les flux sont unidirectionnels.

[[Java]].io possède 3 fonctionnalités :
- Manipulation de fichier : grâce à la [[Classe]] File (représentation abstraite des fichiers physiques)
- Flux binaires : manipulation des flux entrant et sortant à l'aide des [[Classe abstraite|classes abstraites]] InputStream et OutputStream

```mermaid
flowchart TB

A[InputStream]---B(FileInputStream)
A---C(FilterInputStream)
C---D(DataInputStream)

E[OutputStream]---F(FileOutputStream)
E---G(FilterOutputStream)
G---H(DataOutputStream)
```

- Sérialisation : écrire un objet ainsi que tous les objets qu'il référence dans un flux binaire (le procédé inverse est la désérialisation) $\to$ implémentation de l'[[Interface]] Serializable (sérialisation à l'aide de ObjectOutputStream et désérialisation à l'aide de ObjectInputStream).