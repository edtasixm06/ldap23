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

 * **edtasixm06/ldap22:config** Exemples de configuració i configuració
   dinàmica del servidor.

 * **acls** Imatge per a fer proves de modificació de les acls usant
   fitxers de modificació. S'ha incorporat la BD cn=config per a l'administració
   del servidor dinàmicament.

 
