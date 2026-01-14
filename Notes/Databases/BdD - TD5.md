# Exercice 1 : [[Bases de données|BdD]] bibliographique

$AUTEUR(\underline{a}, nom)$                      ex : $<a_{12}, \ 'Sowa'>$ 
$PUBLI(\underline{t}, titre)$                          ex : $<t_4, \ 'Conceptuel \ Structures'>$
$MOTCLÉ(\underline{m}, mot)$                      ex :  $<m_5, \ 'IA'>$
$ÉCRITPAR(\underline{t}, \underline{a})$                        ex : $<t_4, \ a_{12}>$
$PARLEDE(\underline{t}, \underline{m})$                        ex : $<t_4, \ m_5>$

Hypothèse : Tout auteur répertorié est associé à au moins une publication

```SQL
-- (9) Numéros et noms des auteurs qui ont cosigné toutes les publications de Ullman (division)
-- 2 expressions
-- double imbrication : tout auteur tel qu'il n'existe pas de publication de Ullman que cet auteur n'a pas cosigné
SELECT * FROM AA1 WHERE NOT EXISTS (SELECT * FROM E,A WHERE E.a = A.a AND nom = 'Ullman' AND t NOT IN (SELECT t FROM E WHERE a = A1.a));
-- comparaison de cardinalité
-- tout auteur tel que le nombre de publications que cet auteur a cosignées avec Ullman est égal au nombre total de publications de Ullman
SELECT * FROM A WHERE a in (SELECT a FROM E WHERE t IN (SELECT t FROM E,A WHERE E.a = A.a AND nom = 'Ullman') GROUP BY a HAVING COUNT(*) = (SELECT COUNT(*) FROM E,A WHERE E.a = A.a AND nom = 'Ullman'));

-- (10) Numéros et noms des auteurs qui ont écrit toutes leurs publications seuls
-- double imbrication
SELECT * FROM AA1 WHERE NOT EXISTS (SELECT * FROM E WHERE E.a = A1.a AND IN (SELECT t FROM E WHERE A1.a != E.a));
-- différence : tous les auteurs - ceux qui ont cosigné
SELECT * FROM A WHERE a NOT IN (SELECT E1.a FROM EE1,EE2 WHERE E.t = E2.t AND E1.a != E2.a);
```

# Exercice 2 : [[Bases de données]] ornithologique

Une association ornithologique se dote d'une [[Bases de données|BdD]] pour stocker ses observations.
$Familles(\underline{f}, nom\_f)$                           ex : $<5, Limicoles>$
$Espèces(\underline{e}, nom\_e, f)$                          ex : $<12, gravelot, 5>$
$Type\_de\_site(\underline{t}, nom\_t)$                      ex : $<16, dunnes>$
$Observations(\underline{e}, \underline{t}, \underline{période})$                 ex : $<12, 16, m>$

$dom(période)=\{m, s, n\} \ (pour \ matin, \ soir \ et  \ nuit)$ 

Hypothèse : La relation $E$ contient toutes les espèces susceptibles d'être observées dans la région

```SQL
-- (1) Trouver le nom de tout type de site où ont été vues autant d'espèces qu'il y en a dans la famille des limicoles
SELECT nom_t FROM T GROUP BY t HAVING COUNT(DISTINCT e) = (SELECT COUNT(*) FROM E,F WHERE E.f = F.f AND nom_f = 'Limicoles');

-- (2) Exprimer en français la signifaction de la requête suivante :
SELECT e, nom_e FROM E WHERE e in (SELECT e FROM O GROUP BY e,t HAVING COUNT(*) = 3);
-- Numéros et noms de toutes les espèces que l'on a pu observer à n'importe quel moment sur un site donné

-- (3) Soit la requête  : "Trouver le numéro de toute espèce ayant été vue le matin sur au plus 2 types de site"
-- On envisage la requête SQL :
SELECT e FROM O WHERE période = 'm' GROUP BY e HAVING COUNT(*) <= 2;
-- Est-elle appropriée ?
-- Non! On rate les espèces qui n'ont j'amais été observées le matin (ou jamais observées du tout). La bonne requête serait :
SELECT e FROM E WHERE NOT IN (SELECT e FROM O WHERE période = 'm' GROUP BY e HAVING COUNT(*) > 2);
```