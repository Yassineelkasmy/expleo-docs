---
description: Install Nexus repository manager on Ubuntu 22.04
---

# Nexus Repository Manager

```
sudo apt install openjdk-8-jre-headless
```

```
cd /opt
sudo wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
tar -zxvf latest-unix.tar.gz
```

```
sudo mv /opt/nexus-3.47.01 /opt/nexus
```

```
sudo adduser nexus
```

```
sudo visudo
```

Add this to file being edited

```
nexus ALL=(ALL) NOPASSWD: ALL
```

```
sudo chown -R nexus:nexus /opt/nexus
```

```
sudo chown -R nexus:nexus /opt/sonatype-work
```

```
sudo vim /opt/nexus/bin/nexus.rc
```

Add this to the file being edited

```
run_as_user="nexus"
```

Also add this configuration below, this will increase the nexus JVM heap size

```systemd
-Xms1024m
-Xmx1024m
-XX:MaxDirectMemorySize=1024m

-XX:LogFile=./sonatype-work/nexus3/log/jvm.log
-XX:-OmitStackTraceInFastThrow
-Djava.net.preferIPv4Stack=true
-Dkaraf.home=.
-Dkaraf.base=.
-Dkaraf.etc=etc/karaf
-Djava.util.logging.config.file=/etc/karaf/java.util.logging.properties
-Dkaraf.data=./sonatype-work/nexus3
-Dkaraf.log=./sonatype-work/nexus3/log
-Djava.io.tmpdir=./sonatype-work/nexus3/tmp
```

```
sudo vim /etc/systemd/system/nexus.service
```

```systemd
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
```



```sh
sudo systemctl start nexus
sudo systemctl enable nexus
```
