# LDAP server
## @edt ASIX M06-ASO Curs 2023-2024

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona


### Ldap servers:

 * **edtasixm06/ldap23:acl** Imatge per a fer proves de modificació de les acls usant
  fitxers de modificació. S'ha incorporat la BD cn=config per a l'administració
  del servidor dinàmicament.

Detach:
```
docker run --rm --name ldap.edt.org -h ldap.edt.org --net 2hisx -p 389:389 -d edtasixm06/ldap23:acl
```

Exemples:
```
  access to * by * read
  access to * by * write
  access to * by self write by * read
  access to * by self write by * read
```

Exemples de modificació dinàmica: fitxer de modificació entry.ldif
```
dn: olcDatabase={1}mdb,cn=config
changetype: modify
replace: olcAccess
olcAccess: to attrs=UserPassword by self write by * auth
olcAccess: to * by * read


#olcAccess: to * attrs=homePhone by dn.exact="cn=Marta Mas,ou=usuaris,dc=edt,dc=org" write by users write
#olcAccess:  to attrs=homePhone by * read
#olcAccess: to * by * write
```

Modificar amb ldapmodify
```
ldapmodify -x -h localhost -D ‘cn=Sysadmin,cn=config’ -w syskey -f entry.ldif
```

---

```
ldapsearch -x -LLL -D 'cn=Sysadmin,cn=config' -w syskey -b 'olcDatabase={1}mdb,cn=config' 

ldapsearch -x -LLL -D 'cn=Sysadmin,cn=config' -w syskey -b 'olcDatabase={1}mdb,cn=config' olcAccess

# ldapmodify -vx -D 'cn=Sysadmin,cn=config' -w syskey -f acl1.ldif 


```



 







