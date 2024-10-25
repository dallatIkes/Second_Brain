#Introduction Une base de donnée ([[Bases de données|BdD]]) est un [[Ensemble]] structuré de données représentant un sous-ensemble du monde réel (entreprise) pouvant être partagé par plusieurs applications.

#Exemple entreprise = université, données = liste des inscrits; antécédents des étudiants; liste des cours; liste des enseignants; etc... , application: gestion des inscriptions; planning des salles; composition des jurys; etc... Une [[Bases de données|BdD]] contient des informations sur les objets du monde réel et sur les relations entre ces objets.

#Principale_motivation fournir une description unique de toutes les données manipulées par l'entreprise (+ indépendance des données et des applications)

# Modèle de données

#Définition On appelle modèle de données un [[Ensemble]] d'outils conceptuels permettant de représenter et de structurer des données. On en verra deux : 
- [[Modèle entité-association]]
- [[Modèle relationnel]]

#But fournir des outils et un cadre rigoureux pour la gestion des données

#Exemple conception d'une [[Bases de données|BdD]] visant à conserver des descriptions d'articles parus dans les journaux.
**Réel perçu :** un éditeur édite des journaux. IL est caractérisé par un nom et une adresse. Un journal est édité par un éditeur et publie des articles dans des numéros. On conservera le nom du journal et celui de son rédacteur en chef. Un numéro de journal contient une collection d'articles. On veut conserver le titre et un résumé de l'article, ainsi que le nom de l'auteur. Les auteurs sont connus par leur nom, prénom, adresse et date de naissance.
**Démarche :** on est observateur de l'organisation (= '"réel perçu"). On retient de l'observation ce qui nous intéresse pour les applications visées $\rightarrow$ description linguistique. On conçoit un schéma à l'aide d'une modèle. ⚠ Beaucoup de soin doit être accordé à cette étape de modélisation. Des modifications ultérieures pourraient être très coûteuses. 

# Système de gestion de bases de données ([[SGBD]])

**SGBD** : le logiciel qui permet aux utilisateurs d’interagir avec une [[Bases de données|BdD]]. Les "éléments" intervenant dans un [[SGBD]] sont :
- les données qui y sont rangées de manière accessible, intégrée et partageable
- les fonctions disponibles aux utilisateurs : description, protection, interrogation, mise à jour, ...
- le matériel et le système d'exploitation
Les utilisateurs (au sens large) sont rangés en 3 catégories :
- utilisateurs terminaux : non informaticiens, manipulent les informations
- développeurs d'application : informaticiens chargés d'écrire les procédures agissant sur les données
- administrateurs du [[SGBD]] : chargé des problèmes de gestion de la base.

# Principales fonctions d'un SGBD

$\rightarrow$ **Description des données :** elle se fait à 2 niveaux :
- développeur d'application : description logique des objets
- administrateur du SGBD : description physique des données gérées
Un [[LDD]] (Langage de Description de Données) permet la description logique des objets et des liens entre ces objets.
$\rightarrow$ **Utilisation :** doit offrir des outils de recherche, mise à jour (création, suppression, modification) des données par l'intermédiaire d'un langage d'utilisation plus ou moins riche.
$\rightarrow$ **Gestion de l'intégrité :** dans une [[Bases de données|BdD]], on a un grand nombre d'informations manipulées, lesquelles évoluent, ce qui impose une gestion de l'intégrité. Le SGBD doit fournir des possibilités de contrôle qui portent sur le type, la valeur des informations, et sur les contraintes d'intégrité définies sur et entre les informations (propriétés devant toujours être vérifiées par la [[Bases de données|BdD]]. 

# Confidentialité

Plusieurs catégories d'utilisateurs. Certaines informations peuvent être confidentielles $\rightarrow$ gestion des droits d'accès. Limitation de l'accès à des sous-ensembles de la base à des groupes d'utilisateurs autorisés.
$$\{sous-ens. \ de \ la \ base, \ groupe\} \rightarrow \{ens. \ droits \ d'accès\} \subseteq \{lire, \ créer, \ supprimer, \ modifier\}$$

# Concurrence d'accès

Tentatives d'accès simultanées provenant de plusieurs utilisateurs. Nécessité éventuelle d'opérer un ordre de prise en compte des divers accès. Chaque utilisateur doit avoir une version cohérente de la base. Notion de transaction (ensemble de commandes vu comme une seule commande).

# Sécurité de fonctionnement

Possibilité de panne, d'incident. Cette fonction doit assurer :
- la sauvegarde des fichiers lors d'états cohérents de la base
- la reprise après incident