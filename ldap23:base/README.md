# LDAP server
## @edt ASIX M06-ASO Curs 2023-2024

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona


### Ldap servers:

 * **edtasixm06/ldap23:base** Server bàsic ldap, amb base de dades edt.org.
   Aquesta imatge engega amb CMD un script anomenat startup.sh que fa el següent:
   * Esborrar els directoris de configuració i de dades
   * Generar el directori de configuració dinàmica slapd.d a partir del fitxer de configuració slapd.conf
   * Injectar a baix nivell les dades de la BD 'populate' de l'organització dc=edt,dc=org
   * Assignar la propietat i grup del directori de ddaes i de configuració a l'usuari *openldap*
   * Engegar el servei slapd amb el paràmetre que fa debug per mantenir-lo engegat en foreground

#### Desplegament
```
docker build -t edtasixm06/ldap23:base .
```

```
docker network create 2hisx
docker network inspect 2hisx
```
```
docker run --rm --name ldap.edt.org -h ldap.edt.org --net 2hisx -p 389:389 -d edtasixm06/ldap23:base

docker ps
```

```
nmap <ip-container ldap>
ldapsearch -x -LLL -b 'dc=edt,dc=org'
ldapsearch -x -LLL -H ldap://<ip-container> -b 'dc=edt,dc=org'
docker exec -it ldap.edt.org ps ax
```


