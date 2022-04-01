---
title: Centos创建服务
date: 2022-03-07 22:01:18
tags: Linux Centos
---

Centos7中的用户服务文件在`/usr/lib/systemd/system`中，以`.service`结尾，下面是nginx.service的内容

```shell
[Unit]
# 服务名称
Description=nginx - high performance web server         
# 文档
Documentation=http://nginx.org/en/docs/
# 服务的依赖	
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
# Nginx will fail to start if /run/nginx.pid already exists but has the wrong
# SELinux context. This might happen when running `nginx -t` from the cmdline.
ExecStartPre=/usr/bin/rm -f /run/nginx.pid
# 服务预启动、启动、重启、停止
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
PrivateTmp=true

[Install]
WantedBy=multi-user.target                               
```



从上面nginx.service的内容可以看出，一个service的内容包含三部分`[Unit]`,`[Service]`,`[Install]`
