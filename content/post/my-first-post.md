---
title: "Enable TCP port 2375 for external connection to Docker"
description: 在修改Docker配置hosts时，发现服务启动失败：Conflict between default -H fd:// systemd config and daemon.json hosts config
date: 2024-10-22T17:19:16+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---

1. Create daemon.json file in /etc/docker:
```
{"hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]}
```

2. Add /etc/systemd/system/docker.service.d/override.conf

```
 [Service]
 ExecStart=
 ExecStart=/usr/bin/dockerd
```
3. Reload the systemd daemon:
```bash
 systemctl daemon-reload
```
4. Restart docker:
```bash
 systemctl restart docker.service
```
