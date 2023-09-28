
# Série 2 : les opérateurs ensemblistes

1. Rechercher les clients bruxellois et namurois. On écrira une requête ensembliste ainsi qu'une requête
    sans opérateur ensembliste.
    
    _Version: Sans op ensembliste_
    ~~~sql
    SELECT NOMCLIENT ,PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT ='Bruxelles' OR LOCALITECLIENT='Namur';
    ~~~
    _Version: Avec op ensembliste_
    <!-- pour les op ensembl il faut que tout soit compatibles donc avoir les mme select -->

    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT = 'Bruxelles'
    UNION
    SELECT NOMCLIENT, PRENOMCLIENT, LOCALITECLIENT
    FROM AG_CLIENTS
    WHERE LOCALITECLIENT = 'Namur';
    ~~~

2. Rechercher les clients qui possèdent à la fois un numéro de téléphone et un numéro de fax. On écrira 
    une requête ensembliste ainsi qu'une requête sans opérateur ensembliste.
    
    _Version: Sans op ensembliste_
    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT, TELCLIENT,FAXCLIENT
    FROM AG_CLIENTS
    WHERE TELCLIENT IS NOT NULL AND FAXCLIENT IS NOT NULL;
    ~~~
     _Version: Avec op ensembliste_
   ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT, TELCLIENT,FAXCLIENT
    FROM AG_CLIENTS
    MINUS
    SELECT NOMCLIENT, PRENOMCLIENT, TELCLIENT,FAXCLIENT
    FROM AG_CLIENTS
    WHERE TELCLIENT IS  NULL OR FAXCLIENT IS  NULL;
   ~~~
   
3. Rechercher tous les clients qui ne possèdent pas de numéro de téléphone. On écrira une requête 
    ensembliste ainsi qu'une requête sans opérateur ensembliste.

     _Version: Sans op ensembliste_
    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT
    FROM AG_CLIENTS
    WHERE TELCLIENT IS NULL ;
    ~~~
    _Version: Avec op ensembliste_
    ~~~sql
    SELECT NOMCLIENT, PRENOMCLIENT
    FROM AG_CLIENTS
    MINUS
    SELECT NOMCLIENT, PRENOMCLIENT
    FROM AG_CLIENTS
    WHERE TELCLIENT IS NOT NULL ;
    ~~~
   
4. Rechercher toutes les activités dont la durée est supérieure à 2. On écrira une requête ensembliste
    ainsi qu'une requête sans opérateur ensembliste.

     _Version: Sans op ensembliste_
    ~~~sql
    SELECT INTITULEACTIVITE ,DUREEACTIVITE
    FROM AG_ACTIVITES
    WHERE DUREEACTIVITE>2;
    ~~~
     _Version: Avec op ensembliste_
   ~~~sql
    SELECT INTITULEACTIVITE ,DUREEACTIVITE
    FROM AG_ACTIVITES
    MINUS
    SELECT INTITULEACTIVITE,DUREEACTIVITE
    FROM AG_ACTIVITES
    WHERE DUREEACTIVITE<=2;
   ~~~   
   
5. Rechercher toutes les informations sur les cars de marque Opel ou Mercedes. On écrira une requête ensembliste 
    ainsi qu'une requête sans opérateur ensembliste.
    
     _Version: Sans op ensembliste_
    ~~~sql
    SELECT NUMIMMATRICULATION,MARQUE,NBRPLACECAR,TV,VIDEO,DVD 
    FROM AG_CARS
    WHERE MARQUE='Opel' OR MARQUE='Mercedes';
   ~~~
      _Version: Avec op ensembliste_
    ~~~sql
    SELECT NUMIMMATRICULATION,MARQUE,NBRPLACECAR,TV,VIDEO,DVD 
    FROM AG_CARS
    MINUS
    SELECT NUMIMMATRICULATION,MARQUE,NBRPLACECAR,TV,VIDEO,DVD 
    FROM AG_CARS
    WHERE MARQUE<>'Opel' AND MARQUE<>'Mercedes';
    ~~~
   
6. Rechercher l'intitulé de tous les voyages dont le prix est inférieur à 1000€ et la durée supérieure à 4. 
    On écrira une requête ensembliste ainsi qu'une requête sans opérateur ensembliste.
    
     _Version: Sans op ensembliste_
    ~~~sql
    SELECT INTITULEVOYAGE,PRIXHTVOYAGE,DUREEVOYAGE
    FROM AG_VOYAGES
    WHERE PRIXHTVOYAGE <1000 AND DUREEVOYAGE>4;
    ~~~
    _Version: Avec op ensembliste_
    ~~~sql
    SELECT INTITULEVOYAGE,PRIXHTVOYAGE,DUREEVOYAGE
    FROM AG_VOYAGES
    MINUS
    SELECT INTITULEVOYAGE,PRIXHTVOYAGE,DUREEVOYAGE
    FROM AG_VOYAGES
    WHERE PRIXHTVOYAGE >= 1000 OR DUREEVOYAGE <= 4;
    ~~~   