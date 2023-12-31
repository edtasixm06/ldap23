# LDAP server
## @edt ASIX M06-ASO Curs 2023-2024

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona


### Ldap servers:

 * **edtasixm06/ldap23:base** Server bàsic ldap, amb base de dades edt.org.

 * **edtasixm06/ldap23:editat** Servidor edt.org amb els usuaris identificats per uid, 
   usuaris típics més usuaris user01-user10, passwd de manager xifrat i activant la base
   de dades cn=config.

 * **edtasixm06/ldap23:config** Exemples de configuració i configuració
   dinàmica del servidor.

 * **edtasixm06/ldap23:acls** Imatge per a fer proves de modificació de les acls usant
   fitxers de modificació. S'ha incorporat la BD cn=config per a l'administració
   del servidor dinàmicament.

 * **edtasixm06/ldap23:phpldapadmin** Imatge amb un servidor phpldapadmin. Connecta a al servidor ldap
   anomenat *ldap.edt.org* per accedir a les bases de dades *dc=edt,dc=org* i *cn=config*. Aquesta imatge
   està basada en fedora:27 per evitar el canvi de sintaxis de PHP 7.4.

   Detach:
   ```
   $ docker run --rm  --name phpldapadmin.edt.org -h phpldapadmin.edt.org --net 2hisx -p 80:80 -d edtasixm06/ldap23:phpldapadmin 
   ```

* **edtasixm06/ldap23:schema** Servidor LDAP amb la base de dades edt.org S'ha fet el següent:

    * *futbolistaA.schema* Derivat de inetorgPerson, structural, 
      injectat dades de dades-futbolA.ldif.

    * *futbolistaB.schema* Structural derivat de TOP.

    * *futbolistaC.schema* Auxiliary.

 * **edtasixm06/ldap23:practica**   Imatge de la pràctica de ldap schema.

 * **edtasixm06/ldap23:grups** 
 * **edtasixm06/ldap23:latest** Imatge final del servei ldap amb usuaris i grups. 

