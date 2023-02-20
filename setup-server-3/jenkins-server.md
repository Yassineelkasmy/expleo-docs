---
description: Steps to install the jenkins server on 6.1.11-arch1-1
---

# 🛠 Jenkins Server

```sh
sudo pacman -S jenkins
```

```sh
sudo pacman -S  vim jre17-openjdk
```

```sh
sudo archlinux-java set  java-17-openjdk
```

```sh
sudo vim /etc/conf.d/jenkins
JAVA=/usr/lib/jvm/default/bin/java
```

```sh
sudo systemctl daemon-reload
sudo systemctl restart jenkins
sudo systemctl enable jenkins
```

To find the password of the firslt login of user **admin** run the following command

```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

