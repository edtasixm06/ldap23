# LDAP Server
## @edt ASIX M06-ASO Curs 2023 - 2024
### Servidor LDAP

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona

Imatge:

* **edtasixm06/ldap23:phpldapadmin** Imatge amb un servidor phpldapadmin. Connecta a al servidor ldap
  anomenat *ldap.edt.org* per accedir a les bases de dades *dc=edt,dc=org* i *cn=config*. Aquesta imatge
  està basada en fedora:27 per evitar el canvi de sintaxis de PHP 7.4.


Detach:
```
$ docker run --rm  --name phpldapadmin.edt.org -h phpldapadmin.edt.org --net 2hisx -p 80:80 -d edtasixm06/ldap23:phpldapadmin 
```


