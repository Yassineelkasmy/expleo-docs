---
description: Steps to install KIBANA on Ubuntu 22.04
---

# 📶 KIBANA

```sh
sudo apt install kibana
```

```sh
sudo systemctl daemon-reload
```

Make sure to change the server host to **192.168.100.87** or the desired port , (dont put 127.0.0.1 or localhost) because it is not gonna be accessible from the external network.

```sh
sudo vim /etc/nginx/sites-available/kibana.conf
```

```sh
sudo systemctl enable kibana
sudo systemctl start kibana
```

```sh
sudo systemctl status kibana
```

