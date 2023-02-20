---
description: Steps to install KEYCLOAK on Ubuntu 22.04
---

# 🔐 KEYCLOAK

Make sure java and JDK are installede

```
apt-get install default-jdk -y
```

Download the latest version of Keycloak from offical website

```
wget https://github.com/keycloak/keycloak/releases/download/20.0.3/keycloak-20.0.3.tar.gz
```

Extract the archive

```sh
tar -xvzf keycloak-20.0.3.tar.gz
```

Move the keyloack extracted folder to the opt directory&#x20;

```
mv keycloak-20.0.3 /opt/keycloak
```

Add the user group keycloak without login ablility and make sure that it has the correct ownership rules,&#x20;

```sh
groupadd keycloak
useradd -r -g keycloak -d /opt/keycloak -s /sbin/nologin keycloak
```

```sh
chown -R keycloak: /opt/keycloak
chmod o+x /opt/keycloak/bin/
```

```sh
chown keycloak: /opt/keycloak/bin/launch.sh
```

```sh
sudo vim /etc/systemd/system/keycloak.servicel
```

Make sure the service file look like this:

```systemd
[Unit]
Description=Keycloak
After=network.target

[Service]
Type=idle
User=keycloak
Group=keycloak
ExecStart=!/opt/keycloak/bin/kc.sh start-dev
TimeoutStartSec=600
TimeoutStopSec=600


[Install]
WantedBy=multi-user.target
```

Start and enable the new keylcoak service

```sh
sudo systemctl start keycloak
sudo systemctl enable keycloak
```
