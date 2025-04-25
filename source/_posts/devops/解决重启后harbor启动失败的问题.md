---
title: 解决重启后harbor启动失败的问题
date: 2025-04-24 18:43:39
tags: [ 'harbor' ]
categories: [ 'devops' ]
---

创建`/etc/systemd/system/harbor.service`，内容如下：

```
[Unit]
Description=harbor
After=docker.service systemd-networkd.service systemd-resolved.service
Requires=docker.service
Documentation=http://github.com/vmware/harbor
[Service]
Type=simple
Restart=on-failure
RestartSec=5
ExecStart=/usr/bin/docker-compose -f /data/dockers/devops/harbor/docker-compose.yml up
ExecStop=/usr/bin/docker-compose -f /data/dockers/devops/harbor/docker-compose.yml down
[Install]
WantedBy=multi-user.target
```

然后执行命令开启开机自启：

```shell
systemctl enable harbor.service
```

