
# Série 3 : un peu d'ordre dans les résultats

1. Rechercher tous les clients. On affichera le nom et le prénom et les résultats seront donnés par ordre alphabétique 
    croissant sur le nom et par ordre alphabétique décroissant sur le prénom

    _Version: croissant/nom et decroissant/prenom_
   <!-- Pas obliger d'ecrie ASC-->
    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT
    FROM AG_CLIENTS
    ORDER BY NOMCLIENT , PRENOMCLIENT DESC;
    ~~~
   
2. Reprendre les deux solutions de la requête 1 série 2 et trier le résultat par ordre alphabétique 
    sur le nom des clients.
    
    _Version: Sans op ensembliste_
    ~~~sql
    SELECT NOMCLIENT ,PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT ='Bruxelles' OR LOCALITECLIENT='Namur'
    ORDER BY NOMCLIENT ASC;
    ~~~
    _Version: Avec op ensembliste_
   <!-- ORDER BY 1 tri selon le premier element donc nomclient ici-->
    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT = 'Bruxelles'
    UNION
    SELECT NOMCLIENT, PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT = 'Namur'
    ORDER BY NOMCLIENT ASC;
    ~~~
 
3. Reprendre les deux solutions de la requête 9 série 1 et trier le résultat par ordre alphabétique sur le nom et 
    ordre alphabétique inverse sur le prénom

     _Version : 2.Jointure_
   ~~~sql
   SELECT V1.NOMACCOMPAGNATEUR,V1.PRENOMACCOMPAGNATEUR
   FROM AG_ACCOMPAGNATEURS V1
   INNER JOIN AG_ACCOMPAGNATEURS V2 
       ON (V1.PAYSACCOMPAGNATEUR=V2.PAYSACCOMPAGNATEUR)
   WHERE  V1.NOMACCOMPAGNATEUR<>'Perilleux'
   AND V1.PRENOMACCOMPAGNATEUR<>'Daniel'
   AND V2.NOMACCOMPAGNATEUR='Perilleux' 
   AND V2.PRENOMACCOMPAGNATEUR='Daniel'
   ORDER BY NOMACCOMPAGNATEUR,PRENOMACCOMPAGNATEUR DESC;
   ~~~

 
