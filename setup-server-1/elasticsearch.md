---
description: Steps to install ElasticSearch on Ubuntu 22.04
---

# 🔍 Elasticsearch

Import the Elasticsearch public GPG keys to Ubuntu APT

```sh
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg
```

Add Elasticsearch to the sources.list

```sh
echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```

Next we update the Ubuntu apt and refresh the sources.list

```sh
sudo apt update && sudo apt install elasticsearch
```

Next we configure Elascticsearch for our needs:

```sh
sudo nano /etc/elasticsearch/elasticsearch.yml
```

If we are not using an ngnix router or any external router for our machine we must set the host to 0.0.0.0 to allow external traffic.

```yaml
netwrok.host: 0.0.0.0
network.bind_host: 0.0.0.0
network.publish_host: 0.0.0.0
discovery.seed_host: ["0.0.0.0", "[::0]"]
```

Enable the traffic to 9200 port which is the default port.

```sh
sudo ufw allow 9200
```

Next start the elastic search service and enable it to start automaticaly on system boot.

```sh
sudo systemctl start elasticsearch l
sudo systemctl enable elasticsearch
```
