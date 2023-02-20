---
description: Steps to instal OPENSSH server on Ubuntu 22.04.
---

# 🔑 OPENSSH

Install th openssh-server from the apt repository.

```sh
sudo apt install openssh-server
```

Enable and start the openssh service

```sh
sudo systemctl enable --now ssh
```
