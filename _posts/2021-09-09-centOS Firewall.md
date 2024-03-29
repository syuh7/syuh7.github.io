---
layout: post
title: "centOS Firewall"
date: 2021-09-09 16:00:00 +0800
categories: centOS
---

> 记录centOS7中常用的防火墙命令、IP命令、进程命令



### 查看IP

```bash
#本机IP
ifconfig

#公网IP
curl icanhazip.com
```

### centOS7 防火墙

```bash
# 查看防火墙状态
systemctl status firewalld

# 开启防火墙
systemctl start firewalld

# 关闭防火墙
systemctl stop firewalld

# 查看当前firewall状态
firewall-cmd --state

# 重启firewall
firewall-cmd --reload

# 禁止开机启动
systemctl disable firewalld.service 

# 查看已经开放的端口
firewall-cmd --list-ports

# 开启端口
firewall-cmd --zone=public --add-port=80/tcp --permanent

# 命令含义
--zone #作用域
--add-port=80/tcp  #添加端口，格式为：端口/通讯协议
--permanent  #永久生效，没有此参数重启后失效
```

### 其他操作

```shell
# 查看端口占用情况
fuser -n tcp 80

# 查看程序进程
ps axu |grep java

# 根据进程号查看端口占用情况
netstat -nltp | grep pid

# 杀进程
kill -9 pid;   
```























