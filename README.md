# 100 SQL Queries



![GitHub](https://img.shields.io/github/license/kebiri-isam-dine/UniversityProjects?color=g&style=for-the-badge)
![GitHub last commit](https://img.shields.io/github/last-commit/kebiri-isam-dine/UniversityProjects?color=red&style=for-the-badge)
![GitHub contributors](https://img.shields.io/github/contributors/kebiri-isam-dine/UniversityProjects?color=yellow&style=for-the-badge)


![GitHub dev_language](https://img.shields.io/badge/MySQL-brown?style=flat&logo=MySQL&logoColor=white)
![GitHub dev_language](https://img.shields.io/badge/phpMyAdmin-pink?style=flat&logo=phpMyAdmin&logoColor=white)
![GitHub dev_language](https://img.shields.io/badge/SQL-005C84?style=flat&logo=maas&logoColor=white)

![GitHub Org's stars](https://img.shields.io/github/stars/kebiri-isam-dine?style=social)
![GitHub followers](https://img.shields.io/github/followers/kebiri-isam-dine?style=social)




## About The Project
CHALLENGE : 100 requêtes SQL sur un Dataset de jeu, on utilisera ``XAMPP v3.3.0`` serveur Web, une distribution Apache open source contenant ``MySQL`` et ``PHP``







## Dataset
Base de données d'un jeu rpg qui contient des personnages et des armes, lancer le script [DataBrutes.sql](/DataBrutes.sql) pour importer les tables dans ``phpMyAdmin``


[Data.sql](Data.sql) représente la base de données après les modifications      


Le MDP (Modèle Physique de Données) : 
<img src="/Captures/MDP.png">    

Le MDP après les modifications :
<img src="/Captures/MDP2.png">

## Queries

#### SELECT

1. Récupérer tous les personnages

``` sql
SELECT * 
FROM personnage;
```

2. Afficher seulement le nom et les "levelMin" de toutes les armes

``` sql
SELECT nom, levelMin 
FROM arme;
```

3. Afficher le nom, le surnom et le level de tous les personnages

``` sql
SELECT nom, surnom, level 
FROM personnage;
```

4. Afficher le nom et le level de tous les personnages en modifiant les titres des colonnes en "Pseudo" et "Niveau"

``` sql
SELECT nom as Pseudo, level as Niveau
FROM personnage;
```

5. Afficher le types des armes en renommant le type en "Types d'armes de jeu"

``` sql
SELECT libelle as "Types d'armes de jeu"
FROM typearme;
```

#### Fonctions calculs : COUNT, SUM, AVG, MIN, MAX

6. Récupérer le nombre d'armes existantes
``` sql
SELECT count(*) as "Nombre d'armes"
FROM arme;
```

7. Afficher le nombre de personnages du jeu
``` sql
SELECT count(*) as "Nombre de personnages"
FROM personnage;
```

8. Récupérer la moyenne des niveaux des personnages du jeu
``` sql
SELECT AVG(LEVEL) as "Moyenne des niveaux des personnages"
FROM personnage;
```

9. Récupérer la somme des points de force, d'agilité et d'intelligence de toutes les classes

``` sql
SELECT SUM(baseAgi) as "Moyenne d'agilité", SUM(baseIntel) as "Moyenne d'intelligence", SUM(baseForce) as "Moyenne de force"
FROM classe;
```
10. Récupérer le level min et max des armes de jeu
``` sql
SELECT MIN(levelMin) as "level min", MAX(levelMin) as "level max"
FROM arme;
```

11. Additionner le nombre de points de caractéristique de toutes les classes
``` sql
SELECT nom, baseForce + baseIntel + baseAgi as "nombre de points de caractéristique"
FROM classe;
```

#### String : CONCAT, SUBSTRING, LEFT

12. Afficher le nom et le surnom des personnages dans une seule colonne (concaténation)
``` sql
SELECT CONCAT(nom, " ",surnom) as "Personnage"
FROM personnage;
```

13. Afficher les noms des classes avec les points de caractéristique dans une seule colonne
``` sql
SELECT CONCAT(nom, ": ","A = ",baseAgi,", I = ",baseIntel,", F = ",baseForce) as "Classe"
FROM classe;
```

14. Afficher les 6 premières lettres des noms des personnages
``` sql
SELECT SUBSTRING(nom,1,6) 
FROM personnage;
```

15. Afficher les 5 premières lettres des classes concaténées au 20 premières lettres de la description
``` sql
SELECT CONCAT(SUBSTRING(nom,1,5)," : ", SUBSTRING(description,1,20)) as "Description des classe"
FROM classe;
```

#### WHERE

16. Récupérer toutes les armes dont le levelMin est >5
``` sql
SELECT * 
FROM arme 
WHERE levelMin >5
```

17. Récupérer toutes les armes ayant un nombre de dégats < à 25
``` sql
SELECT * 
FROM arme 
WHERE degat <25
```

18. Récupérer toutes les personnages ayant le level 10 et n'afficher que leur nom et leur surnom

``` sql
SELECT nom, surnom
FROM personnage
WHERE level =10
```

19. Récupérer tous les armes à distance
``` sql
SELECT *
FROM typearme
WHERE estDistance = true
```

#### Les Opérateurs : AND, OR, BETWEEN

20. Récupérer tous les armes ayant un level min compris entre 4 et 8 inclus
``` sql
SELECT *
FROM arme
WHERE levelMin BETWEEN 4 and 8
-- BETWEEN is inclusive by default
```

21. Récupérer tous les personnages ayant un identifiant <= à 3 et un level = à 10
``` sql
SELECT *
FROM personnage
WHERE idPersonnage <=3 and level =10
```

#### JOIN

22. Récupérer tous les personnages et leur classe
``` sql
SELECT * 
FROM personnage
INNER JOIN classe ON personnage.idClasse = classe.idClasse;
```

23. Récupérer toutes les armes et leurs type, et afficher que le nom, levelMin, libelle et estDistance
``` sql
SELECT nom, levelMin, libelle, estDistance 
FROM arme
INNER JOIN typearme ON arme.idTypeArme = typearme.idTypeArme;
```

24. Récupérer le nom des personnages et le nom de leur classe
``` sql
SELECT personnage.nom as "Nom personnage", classe.nom as "Nom classe"
FROM personnage
INNER JOIN classe ON personnage.idClasse = classe.idClasse;
```

25. Récupérer l'arme qui est utilisée par chaque personnage
``` sql
SELECT personnage.nom as "Nom personnage", arme.nom as "Nom arme"
FROM personnage
INNER JOIN arme ON personnage.idArmeUtilise = arme.idArme;
```

26. Récupérer l'arme qui est utilisée par chaque personnage et le type d'arme

``` sql
SELECT personnage.nom as "Nom personnage", arme.nom as "Nom arme", typearme.libelle as "Type d'arme"
FROM personnage
INNER JOIN arme ON personnage.idArmeUtilise = arme.idArme
INNER JOIN typearme ON arme.idTypeArme = typearme.idTypeArme;
```

27. Récupérer toutes les armes de tous les personnages
``` sql
SELECT personnage.nom as "Nom personnage", arme.nom as "Nom arme"
from personnage
INNER JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
INNER JOIN arme ON arme.idArme = dispose.idArme;
```

28. Récupérer toutes les armes qui ne sont pas à distance
``` sql
SELECT arme.nom as "Nom arme", levelMin, degat, typearme.libelle as "Type"
from arme
INNER JOIN typearme ON arme.idTypeArme = typearme.idTypeArme
WHERE estDistance = False;
```

29. Récupérer l'arme utilisée par chaque guerrier
``` sql
SELECT personnage.nom as "Nom personnage", arme.nom as "Nom arme", typearme.libelle as "Type d'arme" 
from personnage
INNER JOIN arme ON arme.idArme = personnage.idArmeUtilise
INNER JOIN typearme ON typearme.idTypeArme = arme.idTypeArme
INNER JOIN classe ON personnage.idClasse = classe.idClasse
WHERE classe.nom = 'Guerrier'
```

30. Récupérer toutes les armes dont disposent les joueurs ayant le level 10
``` sql
SELECT personnage.nom as "Nom personnage", arme.nom as "Nom arme", level
from personnage
INNER JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
INNER JOIN arme ON arme.idArme = dispose.idArme
WHERE personnage.level = 10
```

31. memes requete que 30. mais triées par idPersonnage
``` sql
SELECT personnage.idPersonnage, personnage.nom as "Nom personnage", arme.nom as "Nom arme", level
from personnage
INNER JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
INNER JOIN arme ON arme.idArme = dispose.idArme
WHERE personnage.level = 10
ORDER BY personnage.idPersonnage;
-- ASC ou DESC
```

32. Récupérer la moyenne des dégats des armes à distance
``` sql
SELECT AVG(degat) as "la moyenne des dégats des armes à distance"
FROM arme
INNER JOIN typearme ON arme.idTypeArme = arme.idTypeArme
WHERE typearme.estDistance = True;
```

33. Récupérer tous les personnages disposant d'une arme d'un type commençant par "a"
``` sql
SELECT DISTINCT(personnage.nom) as "Nom personnage"
from personnage
INNER JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
INNER JOIN arme ON arme.idArme = dispose.idArme
INNER JOIN typearme ON arme.idTypeArme = arme.idTypeArme
WHERE typearme.libelle LIKE "A%";
```

34. Récupérer tous les types d'armes, et afficher les armes pour chaque type (meme les types qui n'ont pas d'arme)
``` sql
SELECT arme.nom, typearme.libelle as "type"
FROM arme
RIGHT JOIN typearme ON arme.idTypeArme = typearme.idTypeArme;
-- jointure externe poir avoir toutes les types d'armes meme les types d'armes NULL
```

35. Récupérer toutes les armes et afficher le personnage qui les utilis, ordonnées par levelMin
``` sql
SELECT arme.nom, personnage.nom as "Nom personnage", arme.levelMin
FROM arme
Left JOIN personnage ON arme.idArme = personnage.idArmeUtilise
ORDER BY levelMin;
```

##### Regroupement : GROUP BY, HAVING

36. Afficher le nombre d'arme par type d'arme
``` sql
SELECT typearme.libelle AS "Type d'arme", COUNT(*) AS "Nombre d'arme"
FROM arme
INNER JOIN typearme ON arme.idTypeArme = typearme.idTypeArme
GROUP BY typearme.libelle
ORDER BY COUNT(*) DESC;
```

37. Afficher le nombre de personnage par classe
``` sql
SELECT classe.nom AS "Type de classe", COUNT(*) AS "Nombre de personnage"
FROM personnage
INNER JOIN classe ON personnage.idClasse = classe.idClasse
GROUP BY classe.nom
ORDER BY COUNT(*) DESC;
```

38. Afficher le nombre d'armes dont dispose chaque personnage 
``` sql
SELECT personnage.nom AS "Personnage", COUNT(*) AS "Nombre d'arme"
FROM arme
INNER JOIN dispose ON dispose.idArme = arme.idArme
INNER JOIN personnage ON personnage.idPersonnage = dispose.idPersonnage
GROUP BY personnage.nom
ORDER BY COUNT(*) DESC;
-- l'odre des jointures est IMPORTANT
```

39. Afficher le nombre d'armes dont dispose chaque personnage mais seulement les guerriers
``` sql
SELECT personnage.nom AS "Personnage", COUNT(*) AS "Nombre d'arme"
FROM arme
INNER JOIN dispose ON dispose.idArme = arme.idArme
INNER JOIN personnage ON personnage.idPersonnage = dispose.idPersonnage
INNER JOIN classe ON personnage.idClasse = classe.idClasse
WHERE classe.nom = 'Guerrier'
GROUP BY personnage.nom
ORDER BY COUNT(*) DESC;
```

40. Afficher le nombre de personnages par arme
``` sql
SELECT arme.nom AS "Arme", COUNT(personnage.idPersonnage) AS "Nombre de personnages"
FROM personnage
RIGHT JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
RIGHT JOIN arme ON dispose.idArme = arme.idArme
GROUP BY arme.nom
ORDER BY COUNT(*) DESC;
-- eviter de faire des COUNT(*), pour récuérer le nombre réel réaliser des COUNT() sur les colonnes
```

41. Afficher le niveau moyen de chaque classe
``` sql
SELECT classe.nom AS "Classe", AVG(personnage.level) AS "Niveau moyen"
FROM classe
INNER JOIN personnage ON personnage.idClasse = classe.idClasse
GROUP BY classe.nom
ORDER BY COUNT(*) ASC;
```

42. Afficher le niveau moyen de chaque classe et ne récupérer que les classes ayant un niveau min de 9

``` sql
SELECT classe.nom AS "Classe", AVG(personnage.level) AS "Niveau moyen"
FROM classe
INNER JOIN personnage ON personnage.idClasse = classe.idClasse
GROUP BY classe.nom
HAVING AVG(personnage.level)>9
ORDER BY COUNT(*) ASC;
-- HAVING pour filtrer sur les fonctions de calculs AVG, COUNT, SUM, MIN, MAX
```

43. Afficher le nombre de personnages par arme et ne garder que les armes ayant entre 1 et 2 utilisateurs (table dispose) 
``` sql
SELECT arme.nom AS "Arme", COUNT(personnage.idPersonnage) AS "Nombre de personnages"
FROM personnage
RIGHT JOIN dispose ON personnage.idPersonnage = dispose.idPersonnage
RIGHT JOIN arme ON dispose.idArme = arme.idArme
GROUP BY arme.nom
HAVING COUNT(personnage.idPersonnage) BETWEEN 1 AND 2
ORDER BY COUNT(*) DESC;
```

44. Afficher le nombre d'arme par type d'arme mais ne prendre que les armes de corps à corps présentes au max 1 fois
``` sql
SELECT typearme.libelle AS "Type d'arme", COUNT(arme.idArme) AS "Nombre d'armes"
FROM arme
RIGHT JOIN typearme ON arme.idTypeArme = typearme.idTypeArme
WHERE typearme.estDistance = False
GROUP BY typearme.libelle
HAVING COUNT(arme.idArme) <= 1
ORDER BY COUNT(*) DESC;
-- jointure externe TRES IMPORTANTE
-- on peut avoir WHERE et HAVING dans une seule requete
```

#### Requetes imbriquées (Sous-Requetes) : ALL, IN

45. Récupérer les armes ayant un nombre de dégats > à la moyenne du nombre de dégats de toutes les armes
``` sql
SELECT arme.nom, arme.degat
FROM arme
WHERE arme.degat >
    (SELECT AVG(arme.degat)
     FROM arme)
ORDER BY arme.degat DESC;
```

46. Récupérer les personnages ayant un level < à la moyenne
``` sql
SELECT personnage.nom, personnage.level
FROM personnage
WHERE personnage.level <
    (SELECT AVG(personnage.level)
     FROM personnage)
ORDER BY personnage.level DESC;
```

47. Récupérer les personnages ayant un level > à la moyenne des archers

``` sql
SELECT personnage.nom, personnage.level
from personnage
WHERE personnage.level >
 (SELECT AVG(personnage.level)
    FROM personnage
    INNER JOIN classe ON personnage.idClasse = classe.idClasse
    WHERE classe.nom = 'Archer')
ORDER BY personnage.level DESC;
-- attention au double jointure (pas la peine)
```

48. Pour les armes à distance, récupérer le nombre max d'occurence du type arme

``` sql
SELECT MAX(NombreDarmes) as "le nombre max d'occurence du type arme"
FROM
(SELECT typearme.libelle, COUNT(*) AS "NombreDarmes"
FROM arme
INNER JOIN typearme ON typearme.idTypeArme = arme.idTypeArme
WHERE typearme.estDistance = True
GROUP BY typearme.libelle) TableDynamique
-- TableDynamique : il est nécessaire de nommer la table dynamique qu'on vient de créer
```

49. Récupérer les types d'armes ayant le nombre égale d'occurrence de la précédente reuquete

``` sql
SELECT typearme.libelle AS "Type d'arme", COUNT(*) AS "Nombre d'armes"
FROM typearme
INNER JOIN arme ON typearme.idTypeArme = arme.idTypeArme
GROUP BY typearme.libelle
HAVING COUNT(*) = 
(SELECT MAX(NombreDarmes) as "le nombre max d'occurence du type arme"
FROM
(SELECT typearme.libelle, COUNT(*) AS "NombreDarmes"
FROM arme
INNER JOIN typearme ON typearme.idTypeArme = arme.idTypeArme
WHERE typearme.estDistance = True
GROUP BY typearme.libelle) TableDynamique)
-- l'astuce est de séparer et traiter chaque requête à part pour pouvoir après les imbriquer correctement
```

50. Récupérer les armes ayant un nombre de dégats > au nombre de dégats des arcs
``` sql
SELECT *
FROM arme
WHERE arme.degat > ALL(
 SELECT arme.degat
    FROM arme
    RIGHT JOIN typearme ON arme.idTypeArme = typearme.idTypeArme
    WHERE typearme.libelle = 'Arc') 
-- quand on compare à un SRING, faut vraiment bien vérifier l'orthographe de ce STRING
```

51. Récupérer les armes de corp à corp sans utiliser de jointure
``` sql
SELECT *
FROM arme
WHERE arme.idTypeArme IN(
    SELECT typearme.idTypeArme
    FROM typearme
    WHERE typearme.estDistance = False) 
```

52. Requete précédente avec jointure
``` sql
SELECT * 
FROM arme
INNER JOIN typearme ON arme.idTypeArme = typearme.idTypearme
WHERE typearme.estDistance = False;
```

#### Gestion CRUD (gestion des tables et des données)

53. Créer la table attaque
``` sql
CREATE TABLE attaque
(
    idAttaque INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    nom VARCHAR(60)
)
```

54. Modifier la table pour ajouter deux champs
``` sql
ALTER TABLE attaque
ADD baseDegat INT,
ADD test TINYINT;
```

55. Modifier le champs test en le passant à varchar(50)
``` sql
ALTER TABLE attaque
MODIFY test VARCHAR(50);
```

56. Renommer le champs test en toto
``` sql
ALTER TABLE attaque
CHANGE test toto INT;
```

57. Supprimer le champs test (toto)
``` sql
ALTER TABLE attaque
DROP toto;
-- la BD MySQL demande confirmation avant de supprimer
```

58. Créer la table "utilise" contenant l'id d'un personnage et l'id d'une attaque, et le level d'une attaque
``` sql
CREATE TABLE utilise 
(
    idAttaque INT NOT NULL,
    idPersonnage INT NOT NULL,
    levelAttaque INT,
    PRIMARY KEY (idAttaque, idPersonnage),
    CONSTRAINT FK_ATTAQUE_UTILISE FOREIGN KEY (idAttaque) REFERENCES attaque(idAttaque),
    CONSTRAINT FK_PERSONNAGE_UTILISE FOREIGN KEY (idPersonnage) REFERENCES personnage(idPersonnage)
);
```

59. Ajouter des lignes dans la table 'attaque'
``` sql
INSERT INTO attaque (nom, baseDegat) VALUES ('attaque1', 5);
INSERT INTO attaque (nom, baseDegat) VALUES ('attaque2', 10);
INSERT INTO attaque (nom, baseDegat) VALUES ('attaque3', 15);
INSERT INTO attaque (nom, baseDegat) VALUES ('attaque4', 20);
```

60. Ajouter des lignes dans la table 'utilise'
``` sql
INSERT INTO utilise (idAttaque, idPersonnage, levelAttaque) VALUES (1,1,2), (2,1,2), (2,2,1), (4,3,2), (1,4,3), (4,5,3);
```

61. Modifier l'attaque de toutes les lignes pour que les dégats soient égaux à 10
``` sql
UPDATE attaque
SET baseDegat = 10;
```

62. Modifier les attaques avec les identifiants 2 et 3 pour qu'elles disposent de 50 dégats
``` sql
UPDATE attaque
SET baseDegat = 50
WHERE idAttaque = 2 OR idAttaque = 3;
```

63. Supprimer l'attaque avec l'ID 4
``` sql
DELETE FROM attaque
WHERE idAttaque = 4;
-- impossible, car y a des ligne dans la table 'utilise' avec cet id. Et donc faut d'abord le supprimer de cette table
```

64. Supprimer la table 'utilise', la recréer avec la propriété ON DELETE CASCADE et replacer toutes les lignes dedans. Pour faire ensuite la suppression dans 'attaque'
``` sql
DROP TABLE utilise;
CREATE TABLE utilise 
(
    idAttaque INT NOT NULL,
    idPersonnage INT NOT NULL,
    levelAttaque INT,
    PRIMARY KEY (idAttaque, idPersonnage),
    CONSTRAINT FK_ATTAQUE_UTILISE FOREIGN KEY (idAttaque) REFERENCES attaque(idAttaque) ON DELETE CASCADE,
    CONSTRAINT FK_PERSONNAGE_UTILISE FOREIGN KEY (idPersonnage) REFERENCES personnage(idPersonnage) ON DELETE CASCADE
);
INSERT INTO utilise (idAttaque, idPersonnage, levelAttaque) VALUES (1,1,2), (2,1,2), (2,2,1), (4,3,2), (1,4,3), (4,5,3);
DELETE FROM attaque
WHERE idAttaque = 4;
```

65. Modifier la table personnage pour rajouter une date de naissance, définir ensuite une valeur pour chaque personnage
``` sql
ALTER TABLE personnage
ADD dateNaissance DATE;
UPDATE personnage SET dateNaissance = '2000-01-01' WHERE idPersonnage=1;
UPDATE personnage SET dateNaissance = '2001-02-01' WHERE idPersonnage=2;
UPDATE personnage SET dateNaissance = '2002-03-01' WHERE idPersonnage=3;
UPDATE personnage SET dateNaissance = '2003-06-01' WHERE idPersonnage=4;
UPDATE personnage SET dateNaissance = '2001-04-01' WHERE idPersonnage=5;
UPDATE personnage SET dateNaissance = '2007-02-01' WHERE idPersonnage=6;
UPDATE personnage SET dateNaissance = '2003-05-01' WHERE idPersonnage=7;
```

#### DATE

66. Récupérer les personnages nés après 2002
``` sql
SELECT *
FROM personnage
WHERE personnage.dateNaissance > '2002-01-01'
```

67. Récupérer l'année de naissance de tous les personnages
``` sql
SELECT personnage.nom, YEAR(personnage.dateNaissance) as 'Année de naissance'
FROM personnage;
```

68. Récupérer le jour de la semaine de naissance de tous les personnages

``` sql
SELECT personnage.nom, DAYOFWEEK(personnage.dateNaissance) as 'Jour de naissance'
FROM personnage;
-- 1 : Dimanche / 2 : Lundi / 3 : Mardi / 4 : Mercredi / 5 : Jeudi / 6 : Vendredi / 7 : Samedi
```

69. Récupérer l'age de chaque personnage
``` sql
SELECT personnage.nom, DATEDIFF(NOW(), personnage.dateNaissance)/365 as 'Age'
FROM personnage;
```

70. Requête précédente mais avec un résultat arrondi (age exact)

``` sql
SELECT personnage.nom, CONVERT(DATEDIFF(NOW(), personnage.dateNaissance)/365,INT) as 'Age'
FROM personnage
ORDER BY Age DESC;
```

71. Calculer la moyenne d'age des personnages
``` sql
SELECT AVG(CONVERT(DATEDIFF(NOW(), personnage.dateNaissance)/365,INT)) as 'Moyenne dage'
FROM personnage;
```

72. Calculer la moyenne d'age des personnages avec une deuxième méthode

``` sql
SELECT AVG(TableDynamique1.age) AS 'Moyenne dage'
FROM
(SELECT personnage.nom, DATEDIFF(NOW(), personnage.dateNaissance)/365 AS age
FROM personnage) TableDynamique1
```

73. Récupérer les personnages ayant plus de 15ans
``` sql
SELECT personnage.nom, CONVERT(DATEDIFF(NOW(), personnage.dateNaissance)/365,INT) AS age
FROM personnage
WHERE CONVERT(DATEDIFF(NOW(), personnage.dateNaissance)/365,INT) > 15;
```

74. 
``` sql
SELECT * FROM ;
```

75. 
``` sql
SELECT * FROM ;
```

76. 
``` sql
SELECT * FROM ;
```

77. 
``` sql
SELECT * FROM ;
```

78. 
``` sql
SELECT * FROM ;
```

79. 
``` sql
SELECT * FROM ;
```

80. 
``` sql
SELECT * FROM ;
```

81. 
``` sql
SELECT * FROM ;
```

82. 
``` sql
SELECT * FROM ;
```

83. 
``` sql
SELECT * FROM ;
```

84. 
``` sql
SELECT * FROM ;
```

85. 
``` sql
SELECT * FROM ;
```

86. 
``` sql
SELECT * FROM ;
```

87. 
``` sql
SELECT * FROM ;
```

88. 
``` sql
SELECT * FROM ;
```

89. 
``` sql
SELECT * FROM ;
```

90. 
``` sql
SELECT * FROM ;
```

91. 
``` sql
SELECT * FROM ;
```

92. 
``` sql
SELECT * FROM ;
```

93. 
``` sql
SELECT * FROM ;
```

94. 
``` sql
SELECT * FROM ;
```

95. 
``` sql
SELECT * FROM ;
```

96. 
``` sql
SELECT * FROM ;
```

97. 
``` sql
SELECT * FROM ;
```

98. 
``` sql
SELECT * FROM ;
```

99. 
``` sql
SELECT * FROM ;
```

100. 
``` sql
SELECT * FROM ;
```




## License

[GPL-3.0](https://choosealicense.com/licenses/gpl-3.0/)


## Contact

📫 How to reach me: kebiri.isam.dine@gmail.com

🌐 My Portfolio: <https://kebiri-isam-dine.github.io/>

🔗 Project Link: <https://github.com/kebiri-isam-dine/100_SQL_Queries>
