---
description: Steps to install GitLab on Ubuntu (22.04)
---

# 👨💻 GitLab

```sh
sudo apt install tzdata curl ca-certificates openssh-server
```

<pre class="language-sh"><code class="lang-sh"><strong>gpg_key_url="https://packages.gitlab.com/gitlab/gitlab-ce/gpgkey" curl -fsSL $gpg_key_url| sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/gitlab.gpg
</strong></code></pre>

```sh
sudo tee /etc/apt/sources.list.d/gitlab_gitlab-ce.list<<EOF
deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ focal main
deb-src https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ focal main
EOF
```

```sh
sudo apt update
```

```sh
sudo apt install gitlab-ce
```

Test if GitlLab can start with the default configuration , most of times it will only fail if the port 80 is already taken and https cerficates are not configured, **Let\`s encrypt** will automaticaly issue a certficate.

```sh
sudo gitlab-ctl reconfigure
```

```sh
sudo gitlab-rake gitlab:env:info
```

Enable https traffic from outside the network, port (443)

```sh
sudo ufw allow https
```

```sh
sudo gitlab-ctl start
```

```sh
sudo gitlab-ctl status
```

This is the configuration file, for now we dont need to change anything , but later we will modfiy it because we need to set custom SSL cerficates on each server. You can use the server for now and configure ssh keys and users/groups.\
We need self signed cerficates to use the server from external network services , like Jenkins and Nexus repository manager.&#x20;

```sh
sudo vim /etc/gitlab/gitlab.rb
```

