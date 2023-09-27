# Exercices de révision à propos du LMD

## Série 1 : Les jointures

1. Rechercher, pour chaque départ, sa date, le nombre de places, l'intitulé et la durée du voyage
~~~sql
SELECT DATEDEPART,NBRPLACEDEPART,INTITULEVOYAGE,DUREEVOYAGE 
FROM AG_DEPARTS , AG_VOYAGES;
~~~
 
2. Dans quelles conditions peut-on utiliser une jointure naturelle?
~~~sql

~~~
 
3. Quand on fait une jointure de type INNER JOIN avec un USING, comment peut-on utiliser le(s) champ(s) qui 
    apparai(ssen)t dans le USING (par exemple dans le SELECT ou le WHERE ?
~~~sql

~~~
 
4. Rechercher, en utilisant les jointures, le nom et le prenom des accompagnateurs ainsi que le libellé des différentes 
    langues qu'ils parlent (pour chaque accompagnateur on aura donc autant de lignes que de langues qu'il sait parler)

   <!--INNER JOIN:seules les lignes qui ont des correspondances dans les deux tables sont incluses dans le résultat-->
~~~sql
SELECT AG_ACCOMPAGNATEURS.NOMACCOMPAGNATEUR, AG_ACCOMPAGNATEURS.PRENOMACCOMPAGNATEUR, AG_LANGUES.LIBELLELANGUE
FROM AG_ACCOMPAGNATEURS
INNER JOIN AG_CONNAIT ON AG_ACCOMPAGNATEURS.NUMACCOMPAGNATEUR = AG_CONNAIT.NUMACCOMPAGNATEUR
INNER JOIN AG_LANGUES ON AG_CONNAIT.CODELANGUE = AG_LANGUES.CODELANGUE;
~~~
 
5. Rechercher l'immatriculation, la marque, le nom du concessionnaire et le nombre de places des différents cars disponibles
~~~sql
SELECT NUMIMMATRICULATION, AG_MARQUES.MARQUE, AG_MARQUES.NOMCONCESSIONNAIRE, NBRPLACECAR 
FROM AG_CARS
INNER JOIN AG_MARQUES ON AG_CARS.MARQUE = AG_MARQUES.MARQUE;
~~~
 
6. Rechercher l'ensemble des noms de villes qui constituent l'itinéraire des différents voyages. On affichera l'intitulé
    du voyage et toutes les villes
~~~sql
SELECT INTITULEVOYAGE, AG_VILLES.NOMVILLE 
FROM AG_VOYAGES
INNER JOIN AG_ITINERAIRES ON AG_VOYAGES.NUMVOYAGE = AG_ITINERAIRES.NUMVOYAGE
INNER JOIN AG_VILLES ON AG_ITINERAIRES.NUMVILLE = AG_VILLES.NUMVILLE;
~~~
 
7. Rechercher l'ensemble des noms de villes qui constituent l'itinéraire du voyage dont l'intitulé est "Paris". 
    On affichera l'intitulé du voyage ainsi que toutes les villes concernées
~~~sql
SELECT INTITULEVOYAGE, AG_VILLES.NOMVILLE 
FROM AG_VOYAGES
INNER JOIN AG_ITINERAIRES ON AG_VOYAGES.NUMVOYAGE = AG_ITINERAIRES.NUMVOYAGE
INNER JOIN AG_VILLES ON AG_ITINERAIRES.NUMVILLE = AG_VILLES.NUMVILLE
WHERE AG_VOYAGES.INTITULEVOYAGE = 'Paris';
~~~
 
8. Rechercher le nom et le prénom de tous les clients qui habitent la même ville que Eva Colette 
    (résoudre avec jointure et requêtes imbriquées : 2 solutions différentes)

_Version : 1.Requete imbriqué_
~~~sql
SELECT NOMCLIENT,PRENOMCLIENT
FROM AG_CLIENTS
WHERE LOCALITECLIENT=
      (SELECT LOCALITECLIENT 
       FROM AG_CLIENTS 
       WHERE NOMCLIENT='Colette' 
         AND PRENOMCLIENT='Eva');
~~~
_Version : 2.Jointure_
~~~sql
SELECT V1.NOMCLIENT, V1.PRENOMCLIENT
FROM AG_CLIENTS V1
INNER JOIN AG_CLIENTS V2 
    ON V1.LOCALITECLIENT = V2.LOCALITECLIENT
WHERE V2.NOMCLIENT = 'Colette' 
  AND V2.PRENOMCLIENT = 'Eva';
~~~
 
9. Rechercher le nom et le prénom des tous les accompagnateurs qui habitent le même pays que l'accompagnateur 
    Daniel Perilleux (résoudre avec jointure et requêtes imbriquées)

_Version : 1.Requete imbriqué_
~~~sql
SELECT NOMACCOMPAGNATEUR,PRENOMACCOMPAGNATEUR
FROM AG_ACCOMPAGNATEURS
WHERE PAYSACCOMPAGNATEUR=
      (SELECT PAYSACCOMPAGNATEUR 
       FROM AG_ACCOMPAGNATEURS 
       WHERE NOMACCOMPAGNATEUR='Perilleux' 
         AND PRENOMACCOMPAGNATEUR='Daniel');
~~~
 _Version : 2.Jointure_
~~~sql
SELECT V1.NOMACCOMPAGNATEUR,V1.PRENOMACCOMPAGNATEUR
FROM AG_ACCOMPAGNATEURS V1
INNER JOIN AG_ACCOMPAGNATEURS V2 
    ON V1.PAYSACCOMPAGNATEUR=V2.PAYSACCOMPAGNATEUR
WHERE V2.NOMACCOMPAGNATEUR='Perilleux' 
  AND V2.PRENOMACCOMPAGNATEUR='Daniel';
~~~

10. Rechercher les paires de cars qui possèdent le même nombre de places. On affichera la plaque d'immatriculation de 
    chaque car ainsi que le nombre de places.
<!--WHERE V1.NUMIMMATRICULATION <> V2.NUMIMMATRICULATION : pour ne pas avoir de doublons-->
~~~sql
SELECT DISTINCT V1.NUMIMMATRICULATION, V1.NBRPLACECAR
FROM AG_CARS V1
INNER JOIN AG_CARS V2 ON V1.NBRPLACECAR = V2.NBRPLACECAR
WHERE V1.NUMIMMATRICULATION <> V2.NUMIMMATRICULATION;
~~~
 
11. Rechercher les paires de villes situées dans le même pays.
~~~sql
SELECT DISTINCT V1.NOMVILLE, V1.PAYS, V2.NOMVILLE, V2.PAYS
FROM AG_VILLES V1
INNER JOIN AG_VILLES V2 ON V1.PAYS = V2.PAYS AND V1.NOMVILLE < V2.NOMVILLE;
~~~
 

