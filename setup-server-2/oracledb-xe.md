---
description: Steps to install Oracle XE on Ubnuntu 22.04
---

# OracleDB XE

First we begin by installing the alien package from apt, this will help us install any RPM package in our ubuntu server

```sh
sudp apt install alien
```

Download the latest oracle xe RPM package from oracle linux downloads page

```sh
wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.ol8.x86_64.rpm
```

Install the RPM package using alien like this:

```sh
sudo alien -i oracle-database-xe-21c-1.0-1.ol8.x86_64.rpm
```

Configure the oracle xe, make sure you remember the password u entered

```sh
sudo /etc/init.d/oracle-xe configure
```

Next start the oracle databse service,&#x20;

```sh
sudo /etc/init.d/oracle-xe start
```

You can access the oracle database web inteface in the following port : 5500, and the oracle database instance port 1539

First connect using sys or system users from the sqldeveloper applocation in your local machine.
