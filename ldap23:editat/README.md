# LDAP server
## @edt ASIX M06-ASO Curs 2023-2023

Podeu trobar les imatges docker al Dockehub de [edtasixm06](https://hub.docker.com/u/edtasixm06/)

Podeu trobar la documentació del mòdul a [ASIX-M06](https://sites.google.com/site/asixm06edt/)

ASIX M06-ASO Escola del treball de barcelona


### Ldap servers:

 * **edtasixm06/ldap22:editat** 
   * generar un sol fitxer ldif anomenat edt.org.ldif
   * afegir en el fitxer dos usuaris i una ou nova inventada i posar-los dins aquesta ou.
   * modificar el fitxer edt.org.ldif  modificant dn dels usuaris utilitzant en lloc del cn el uid per identificar-los. 
   * configurar el password de Manager que sigui ‘secret’ però encriptat (posar-hi un comentari per indicar quin és de cara a estudiar).
   * propagar el port amb -p -P
   * editar els dos README, en el general afegir que tenim una nova imatge. En el de la imatge ldap21:editat descriure els canvis i les ordres per posar-lo en marxa.
   * [posteriorment] vam afegir el requeriment de que tingui cn=config]



#### Generar passwd
```
$ docker run --rm --name ldap.edt.org -h ldap.edt.org --net 2hisx -p 389:389 -d edtasixm06/ldap22:config
d17420f8f77b266c1be84599dea12cb630ad77180776bb06b48257c2790cf1e7

$ docker exec -it ldap.edt.org slappasswd
New password: 
Re-enter new password: 
{SSHA}oAtPEpCsAdk6SLqmqv+6fkqm2EHELq32
```

#### Verificar config

```
$ docker build -t edtasixm06/ldap22:editat .

$ docker run --rm --name ldap.edt.org -h ldap.edt.org --net 2hisx -p 389:389 -d edtasixm06/ldap22:editat

$ ldapsearch -x -LLL -b 'dc=edt,dc=org' | grep dn
dn: dc=edt,dc=org
dn: ou=maquines,dc=edt,dc=org
dn: ou=clients,dc=edt,dc=org
dn: ou=productes,dc=edt,dc=org
dn: ou=usuaris,dc=edt,dc=org
dn: cn=Pau Pou,ou=usuaris,dc=edt,dc=org
dn: cn=Pere Pou,ou=usuaris,dc=edt,dc=org
dn: cn=Anna Pou,ou=usuaris,dc=edt,dc=org
dn: cn=Marta Mas,ou=usuaris,dc=edt,dc=org
dn: cn=Jordi Mas,ou=usuaris,dc=edt,dc=org
dn: cn=Admin System,ou=usuaris,dc=edt,dc=org
```
```
$ ldapwhoami -x -D 'cn=Manager,dc=edt,dc=org' -w secret 
dn:cn=Manager,dc=edt,dc=org

$ docker exec -it ldap.edt.org slapcat -n0 

$ ldapsearch -x -LLL -D 'cn=Sysadmin,cn=config' -w syskey -b 'olcDatabase={1}mdb,cn=config'
dn: olcDatabase={1}mdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcMdbConfig
olcDatabase: {1}mdb
olcDbDirectory: /var/lib/ldap
olcSuffix: dc=edt,dc=org
olcAccess: {0}to *  by self write  by * read
olcAddContentAcl: FALSE
olcLastMod: TRUE
olcMaxDerefDepth: 15
olcReadOnly: FALSE
olcRootDN: cn=Manager,dc=edt,dc=org
olcRootPW: {SSHA}oAtPEpCsAdk6SLqmqv+6fkqm2EHELq32
olcSyncUseSubentry: FALSE
olcMonitoring: TRUE
olcDbNoSync: FALSE
olcDbIndex: objectClass pres,eq
olcDbMaxReaders: 0
olcDbMaxSize: 10485760
olcDbMode: 0600
olcDbSearchStack: 16
olcDbRtxnSize: 10000
```

#### Nou format de DN dels usuaris

```
dn: uid=pau,ou=usuaris,dc=edt,dc=org
objectclass: posixAccount
objectclass: inetOrgPerson
cn: Pau Pou
cn: Pauet Pou
sn: Pou
homephone: 555-222-2220
mail: pau@edt.org
description: Watch out for this guy
ou: Profes
uid: pau
uidNumber: 5000
gidNumber: 100
homeDirectory: /tmp/home/pau
userPassword: {SSHA}NDkipesNQqTFDgGJfyraLz/csZAIlk2/
```

#### Entrades noves fetes

```
dn: ou=cfgs,dc=edt,dc=org
ou: cfgs
description: cicle informatica grau superior
objectclass: organizationalunit

dn: cn=cicle01,ou=cfgs,dc=edt,dc=org
objectclass: inetOrgPerson
cn: cicle01
sn: 01
homephone: 555-222-2220
mail: cicle01@edt.org
description: Watch out for this guy
```


#### Exemple-1

```
$ cat acl-e1.ldif 
dn: olcDatabase={1}mdb,cn=config
changetype: modify
delete: olcAccess
-
add: olcAccess
olcAccess: to * by * read
```

```
$ ldapmodify -vx -D 'cn=sysadmin,cn=config' -w syskey -f acl-e1.ldif 
ldap_initialize( <DEFAULT> )
delete olcAccess:
add olcAccess:
	to * by * read
modifying entry "olcDatabase={1}mdb,cn=config"
modify complete
```

```
$ ldapsearch -x -LLL -D 'cn=sysadmin,cn=config' -w syskey -b 'olcDatabase={1}mdb,cn=config' olcAccess
dn: olcDatabase={1}mdb,cn=config
olcAccess: {0}to * by * read
```

```
$ ldapmodify -cvx -D 'uid=pere,ou=usuaris,dc=edt,dc=org' -w pere -f mod1.ldif 
```

