---
description: Steps to install OpenLDAP server on Ubuntu 22.04
---

# 🔓 OpenLDAP

```sh
sudo apt update
```

```sh
sudo apt install slapd ldap-utils
```

After this command you will get a prompt to enter the password for the admin entry, this password will be used in further commands to setup the Ldap directory structure and members.

```sh
sudo dpkg-reconfigure slapd
```

After this command you will get multiple prompts; for the first question make sure you choose the no so the OpenLDAP setup a new configuration and database for you.\
For the second promt i entered this domain : **ma.expleo.com**\
****For **** the organization name simply put : expleo.com

Note : for the last quesion always choose **yes** so the installation purge and replace the old if configuration if it exists!sudo nano /etc/ldap/ldap.conf

```sh
sudo nano /etc/ldap/ldap.conf
```

Uncomment the line "BASE" and "URI" and input the domain name and change to this:

BASE dc=ma,dc=expleo,dc=com \
URI ldap://ldap01.ma.expleo.com:389

```sh
sudo systemctl restart slapd
sudo systemctl status slapdll
```

Now we have to setup some base groups , like personnel, hr, apps

```sh
sudo vim base-groups.ldif
```

Add the following configuration to the file:

```systemd
dn: ou=apps,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou: apps



dn: ou=personnel,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou: personnel


dn: ou=hr,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou
```

Next make a new file yelkasmy.ldif for example and user informations , this user will be added to the personnel entry:

```sh
sudo vim yelkasmy1.ldif
```

```systemd
dn: cn=Yassine ELKasmy,ou=personnel,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Yassine ElKasmy
givenName: Yassine
sn: Elkasmy
uid: yelkasmy1
mail: yassine.elkasmy-ext@expleogroup.com
userPassword: expleo2022
```

```sh
sudo ldapadd -W root -x -D "dc=ma,dc=expleo,dc=com"  -f base-groups.ldif  
```

```sh
sudo ldapadd -W root -x -D "dc=ma,dc=expleo,dc=com" -f yelksamy1.ldif
```

Finally to check that everything wokrs fine , type the following command:

```sh
sudo slapcat
```

I got this follwing output, ( i already added Mr. Merouane to the users) :

```systemd
dn: dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: dcObject
objectClass: organization
o: expleo
dc: ma
structuralObjectClass: organization
entryUUID: 268e0526-3cbf-103d-8934-ad89610666b2
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209121513Z
entryCSN: 20230209121513.761142Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209121513Z

dn: ou=apps,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou: apps
structuralObjectClass: organizationalUnit
entryUUID: a3afdb9a-3cc6-103d-8528-e75751dcfc71
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209130850Z
entryCSN: 20230209130850.175220Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209130850Z

dn: ou=personnel,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou: personnel
structuralObjectClass: organizationalUnit
entryUUID: a3b026f4-3cc6-103d-8529-e75751dcfc71
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209130850Z
entryCSN: 20230209130850.177166Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209130850Z

dn: ou=hr,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: organizationalUnit
ou: hr
structuralObjectClass: organizationalUnit
entryUUID: a3b06650-3cc6-103d-852a-e75751dcfc71
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209130850Z
entryCSN: 20230209130850.178789Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209130850Z

dn: cn=Yassine ELKasmy,ou=personnel,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Yassine ElKasmy
givenName: Yassine
sn: Elkasmy
uid: yelkasmy1
mail: yassine.elkasmy-ext@expleogroup.com
userPassword:: ZXhwbGVvMjAyMg==
structuralObjectClass: inetOrgPerson
entryUUID: 70406512-3cc7-103d-852d-e75751dcfc71
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209131433Z
entryCSN: 20230209131433.377680Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209131433Z

dn: cn=Merouane Guellil,ou=personnel,dc=ma,dc=expleo,dc=com
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Merouane Guellil
givenName: Merouane
sn: Guellil
uid: mguellil1
mail: merouane.guellil@expleogroup.com
userPassword:: ZXhwbGVvMjAyMg==
structuralObjectClass: inetOrgPerson
entryUUID: e8720b94-3cc7-103d-852e-e75751dcfc71
creatorsName: cn=admin,dc=ma,dc=expleo,dc=com
createTimestamp: 20230209131755Z
entryCSN: 20230209131755.029660Z#000000#000#000000
modifiersName: cn=admin,dc=ma,dc=expleo,dc=com
modifyTimestamp: 20230209131755Z
```
