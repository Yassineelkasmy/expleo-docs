---
description: Steps to install Apache KAFKA on Ubuntu 22.04
---

# ⚡ Apache KAFKA & ZOOKEEPER

```sh
sudo apt update  
sudo apt install default-jdk
```

Here in date of 2023/02/10 i have installed this version , you can check the link of the latest kafka version available to download.

```sh
wget https://downloads.apache.org/kafka/3.4.0/kafka_2.12-3.4.0.tgz
```

Extract the archive and move it to the shared apps folder, we will go with the manual installation method.

```sh
tar xzf kafka_2.13-3.2.0.tgz 
sudo mv kafka_2.13-3.2.0 /usr/local/kafka
```

We will create first the system service file for zookeeper to be recognized by the systemd, we will do the same for creating the kafka service, you can change the folders of the config as you like , just make sure the are correct in the system services files : **zookeeper.service** and **kafka.service**

```sh
sudo nano /etc/systemd/system/zookeeper.service 
```

```systemd
[Unit]
Description=Apache Zookeeper server
Documentation=http://zookeeper.apache.org
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=simple
ExecStart=/usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties
ExecStop=/usr/local/kafka/bin/zookeeper-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

```sh
sudo nano /etc/systemd/system/kafka.service 
```

```systemd
[Unit]
Description=Apache Kafka Server
Documentation=http://kafka.apache.org/documentation.html
Requires=zookeeper.service

[Service]of
Type=simple
Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64"
ExecStart=/usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/server.properties
ExecStop=/usr/local/kafka/bin/kafka-server-stop.sh

[Install]
WantedBy=multi-user.target
```

Reload the systemctl so the systemd recognize the new services files.

```sh
sudo systemctl daemon-reload 
```

Try these commands first to test if the configuration files are valid and can start the deamons.

```sh
sudo systemctl start zookeeper 
sudo systemctl start kafka 
```

Then enable the services so they start automaticaly when the server boots up.

```sh
sudo systemctl status zookeeper 
sudo systemctl status kafka 
```
