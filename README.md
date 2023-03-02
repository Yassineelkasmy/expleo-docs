---
description: >-
  This page provides a summary about the documentation written for all the CI/CD
  pipeline made
---

# ⚒ DET-PFE CI/CD Documentation

## **CI/CD setup we have:**

### Server 1 : 192.168.1.87 (Ubuntu 22.04)

* OPEN\_LDAP - port : 389
* APACHE\_KAFKA - port: 9092
* ZOOKEEPER - port: 2181
* ELASTICSEARCH - port : 9200
* FILEBEAT
* LOGSTASH
* KIBANA - port : 5601
* GITLAB - port : 443 (HTTPS) with Let's Encrypt certificate
* OPENSSH

### Server 2 : 192.168.1.86 (Ubuntu 22.04)

* KEYKLOACL - port : 8080
* ORACLE\_DB: 1539
* ORACLE\_WEB\_INTERFACE\_MONITOR: 5500
* OPENSSH
* NEXUS REPOSITORY MANAGER - port : 8081

### Server 3 : 192.168.1.85 (6.1.11-arch1-1)

* JENKINS - port : 8090
* OPENSSH
