$E(\underline{e}, nom, spécialité, année)$
$M(\underline{m}, nom, ens, durée)$
$N(\underline{e}, \underline{m}, note)$ 

# Exercice 1
```SQL
-- (1) Numéro et nom des étudiants de SNUM
SELECT e, nom FROM E WHERE spécialité = 'SNUM';

-- (2) Numéro des étudiant inscrits à au moins un module optionnel
SELECT DISTINCT e FROM N;

-- (3) Numéro et nom des étudiants inscrits à au moins un module optionnel
SELECT DISTINCT E.e, nom FROM E,N WHERE E.e = N.e;

-- (4) Numéro des étudiants inscrits au module 1 ou au module 3
SELECT DISTINCT e FROM N WHERE m = 1 OR m = 3;

-- (5) Numéro des étudiants inscrits au module 1 et au module 3
SELECT N1.e FROM NN1, NN2 WHERE N1.e = N2.e AND N1.m = 1 AND N2.m = 3; 

-- (6) Numéro et nom des modules auxquels est inscrit au moins un étudiant d'INFO2
SELECT DISTINCT M.m, M.nom FROM M,N,E WHERE M.m = N.M AND N.e = E.e AND E.spécialité = 'INFO' AND E.année = 2; 

-- (7) Numéro , nom, spécialité et année des étudiants ayant obtenu une note dans un module enseigné par Martin
SELECT DISTINCT E.e, E.nom, spécialité, année FROM E,M,N WHERE E.e = N.e AND M.m = N.m AND ens = 'Martin' AND note IS NOT NULL
```

# Exercice 2
```SQL
-- (1) Numéro des étudiants qui ont eu une note supérieure 11 dans le module 3 et une note supérieure 13 dans le module 7
SELECT e FROM N WHERE m = 3 AND note > 11 AND e IN (SELECT e FROM N WHERE m = 7 AND note > 13);

-- (2) Numéro et noms des modules qui ont une durée supérieure à la moyenne
SELECT m, nom FROM M WHERE durée > (SELECT AVG(durée) FROM M);

-- (3) Numéro des étudiants ayant obtenu dans le module 3 une note supérieure à celle de l'étudiant Bornibus
SELECT e FROM N WHERE m = 3 AND note > (SELECT note FROM N,E WHERE N.e = E.e AND m = 3 AND nom = 'Bornibus');

-- (4) Numéro des étudiants qui ne sont inscrits à aucune module enseigné par Dupont
SELECT e FROM E WHERE e NOT IN (SELECT e FROM N,M WHERE N.m = M.m AND ens = 'Dupont');
-- variante
SELECT e FROM E WHERE NOT EXISTS (SELECT * FROM N,M WHERE N.m = M.m AND ens = 'Dupont' AND N.e = E.e);

-- (5) Noms des enseignants qui n'interviennent que dans des modules de moins de 30h
SELECT M1.nom FROM MM1,MM2 WHERE M1.nom = M2.nom AND MAX(M2.durée) = 30;

--  (6) Numéro des étudiants inscrits à tous les modules enseignés par Martin (division)
SELECT 
```

# Exercice 3
```SQL
-- (1) Noms des enseignants qui assurent plus de 200h de cours
SELECT ens FROM M GROUP BY ens HAVING SUM(durée) > 200;

-- (2) Numéros et noms des étudiants ayant au moins 11 de moyenne
SELECT e, nom FROM E,N WHERE E.e = N.e GROUP BY N.e, nom HAVING AVG(note) >= 11;

-- (3) Numéros des étudiants inscrits à 2 modules exactement et ayant obtenu la même note dans chacun de ces modules
SELECT e FROM N GROUP BY HAVING COUNT(*) = 2 AND MIN(note) = MAX(note);

-- (4) Numéros des modules où sont inscrits des étudiants provenant de deux spécialités exactement
SELECT m FROM N,E  WHERE N.e = E.e GROUP BY m HAVING COUNT(DISTINCT spécialité) = 2;

-- (5) Pour chaque étudiant (n°), moyenne des notes obtenues dans les modules enseignés par Martin
SELECT e, AVG(note) FROM N WHERE m IN (SELECT m FROM M WHERE ens = 'Martin') GROUP BY e;
```

