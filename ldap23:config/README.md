# LDAP server
## @edt ASIX M06-ASO Curs 2023-2024

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona


 * **edtasixm06/ldap23:config** Configuració dinàmica del servidor.
   Definir un compte d’administració per a cn=config. Consultes amb ldapsearch de cn=config.
   Modificacions de la configuració amb ldapmodify usant l’usuari i 
   passwd de l’administrador de cn=config.
   Slapd.conf → slaptest → /etc/openldap/slapd.d → fitxers ldif.
   cn=config. Exemple mod1.ldif (posar atenció a no deixar espis al final dels ldif)

#### Desplegament

```
# Atenció no deixar espais als finals de linia
dn: olcDatabase={1}mdb,cn=config
changetype: modify
replace: olcRootPW
olcRootPw: jupiter
-
delete: olcAccess
-
add: olcAccess
olcAccess: to * by * write
```

```
$ ldapmodify -vx -D 'cn=Sysadmin,cn=config' -w syskey -f mod2.ldif

$ ldapwhoami -x -D 'cn=Manager,dc=edt,dc=org' -w jupiter

$ ldapmodify -x -D 'cn=Anna Pou,ou=usuaris,dc=edt,dc=org' -w anna -f mod.ldif

$ ldapmodify -x -D 'cn=Pere Pou,ou=usuaris,dc=edt,dc=org' -w pere -f mod.ldif
```

```
$ ldapsearch -x -LLL -D 'cn=Sysadmin,cn=config' -w syskey -b 'cn=config'

$ ldapsearch -x -LLL -D 'cn=Sysadmin,cn=config' -w syskey -b 'olcDatabase={1}mdb,cn=config'
```


