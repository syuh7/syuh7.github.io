---
layout: post
title: "BasicIPv6ValidationError解决办法"
date: 2021-08-02 20:30:00 +0800
categories: macOS
---



### BasicIPv6ValidationError解决办法

1.列出你的网卡

```bash
networksetup -listallnetworkservices
```

2.关闭ipv6

```bash
networksetup -setv6off "你网卡名字"

USB 10/100/1000 LAN
networksetup -setv6off "USB 10/100/1000 LAN"
```

3.设置ip地址

```bash
networksetup -setmanual "网卡名字" 192.168.31.2 255.255.255.0 192.168.1.1

networksetup -setmanual "USB 10/100/1000 LAN" 2.32.213.57 255.255.255.192 2.32.213.62
```

