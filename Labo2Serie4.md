# Série 4 : les groupements

1. Rechercher le nombre de cars de chaque marque. On affichera la marque ainsi que le nombre de véhicules correspondants.
    <!--Si champs , count => il faut faire un group by sinon ca ne fonctionne pas-->
    ~~~sql
    SELECT MARQUE,COUNT(NUMIMMATRICULATION) AS "Nombre de vehicules"
    FROM AG_CARS
    GROUP BY MARQUE;
    ~~~
 
2. Rechercher le nombre de langues parlées par les différents accompagnateurs. On affichera le nom, le prénom,
    le pays de l'accompagnateur ainsi que le nombre de langues qu'il maîtrise.
    ~~~sql
    SELECT AG_ACCOMPAGNATEURS.NOMACCOMPAGNATEUR,AG_ACCOMPAGNATEURS.PRENOMACCOMPAGNATEUR,AG_ACCOMPAGNATEURS.PAYSACCOMPAGNATEUR,COUNT(CODELANGUE) AS "Nombre de langues parlees"
    FROM AG_ACCOMPAGNATEURS
    INNER JOIN AG_CONNAIT ON AG_ACCOMPAGNATEURS.NUMACCOMPAGNATEUR=AG_CONNAIT.NUMACCOMPAGNATEUR
    GROUP BY AG_ACCOMPAGNATEURS.NUMACCOMPAGNATEUR ,AG_ACCOMPAGNATEURS.NOMACCOMPAGNATEUR,AG_ACCOMPAGNATEURS.PRENOMACCOMPAGNATEUR,AG_ACCOMPAGNATEURS.PAYSACCOMPAGNATEUR;
    ~~~
   
3. Reprendre la requête précédente et afficher, en plus, le nombre total de places dans les cars, toujours par marque.
    <!--FAUX-->
    ~~~sql
    SELECT MARQUE,COUNT(NUMIMMATRICULATION) AS "Nombre de vehicules",SUM(NBRPLACECAR) AS "Nombre de places "
    FROM AG_CARS
    GROUP BY MARQUE;
    ~~~
 
4. Rechercher le nombre de villes traversées par chaque voyage. On affichera l'intitulé du voyage ainsi que le nombre 
    de villes visitées.
    ~~~sql
    SELECT INTITULEVOYAGE, COUNT(NUMVILLE) AS "Nombre de villes visitees"
    FROM AG_VOYAGES
    INNER JOIN AG_ITINERAIRES ON AG_VOYAGES.NUMVOYAGE = AG_ITINERAIRES.NUMVOYAGE
    GROUP BY AG_VOYAGES.NUMVOYAGE, INTITULEVOYAGE;
    ~~~
 
5. Rechercher le nombre d'activités pour chaque voyage. On affichera l'intitulé du voyage ainsi le nombre d'activités
    correspondantes.
    ~~~sql
    SELECT INTITULEVOYAGE, COUNT(*) AS "Nombre d'activites"
    FROM AG_VOYAGES
    INNER JOIN AG_ESTPROPOSEE ON AG_VOYAGES.NUMVOYAGE = AG_ESTPROPOSEE.NUMVOYAGE
    GROUP BY INTITULEVOYAGE,AG_VOYAGES.NUMVOYAGE;
    ~~~
 
6. Compéter la requête précédente en affichant également le nombre maximum de places par activité ainsi que le prix 
    total de toutes les activités de chaque voyage.
    ~~~sql
    SELECT INTITULEVOYAGE, COUNT(*) AS "Nombre d'activites",MAX(NBRPLACEACTIVITE),SUM(PRIXACTIVITE)
    FROM AG_VOYAGES
    INNER JOIN AG_ESTPROPOSEE ON AG_VOYAGES.NUMVOYAGE = AG_ESTPROPOSEE.NUMVOYAGE
    INNER JOIN AG_ACTIVITES AA on AG_ESTPROPOSEE.NUMACTIVITE = AA.NUMACTIVITE
    GROUP BY INTITULEVOYAGE,AG_VOYAGES.NUMVOYAGE;
    ~~~
 

