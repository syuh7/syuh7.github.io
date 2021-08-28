---
layout: post
title: "虚拟机安装Linux、GitLab"
date: 2021-06-23 11:50:27 +0800
categories: 其他
---



## 一、安装 Centos7

> 参考\借鉴\转载：
>
> [Mac下使用PD安装配置centOS7&配置静态IP&连接ssh工具](https://blog.csdn.net/m0_45899013/article/details/108337190)
>
> [关于Mac VMFusion Centos7虚拟机网络的配置](https://www.cnblogs.com/terrycode/p/12117248.html)

### 1. 下载镜像

[镜像下载](http://mirrors.aliyun.com/centos/7/isos/x86_64/)

正常选`DVD版`即可

### 2. 安装

上面的链接的教程是用的PD，VM也可以没什么区别，重点是Centos里面的一些配置。

- 前面的直接默认，安装的时候选第一个 `Install Centos 7`
- 语言选中文
- 安装信息摘要，可以什么都不改
- 开始安装以后，修改一下`ROOT密码`
- 重启虚拟机

安装完成。

### 3. 配置

```javascript
cd /etc/sysconfig/network-scripts   
ls
vi ifcfg-eth0
```

做如下修改：

```
BOOTPROTO=static
ONBOOT=yes
```

添加如下内容：

```javascript
IPADDR=IP地址
NETMASK=255.255.255.0
GATEWAY=路由器地址
DNS1=8.8.8.8
DNS2=114.114.114.114
```

注：

mac终端，ifconfig查看IP，找到IP的安全范围：

```bash
示例：
inet6 fe80::1c26:d16b:69cd:b37f%en0 prefixlen 64 secured scopeid 0x9
inet 192.168.2.40 netmask 0xffffff00 broadcast 192.168.2.255
```

打开mac网络设置，子网掩码对应netmask，路由器对应gateway

此时：

```bash
service network restart
ping 114.114.114.114
应该是ping不通的
```

停止防火墙：

```bash
#停止防火墙
systemctl stop firewalld
#禁止防火墙随着系统启动而启动
systemctl disable firewalld
#查看防火墙状态
systemctl status firewalld
```

虚拟机网络连接改为 `Wi-Fi`

```bash
service network restart
```

测试网络连接情况：

```bash
ping 114.114.114.114
ping www.baidu.com
```

都能ping通就完事儿了。



## 二、安装Git

> 参考\借鉴\转载：
>
> [Linux环境下安装、升级Git](https://www.lwhweb.com/posts/45066/)

记录的是源码安装方式

### 1. 准备

git 的工作需要调用 `curl`，`zlib`，`openssl`，`expat`，`libiconv` 等库的代码，所以需要先安装这些依赖工具。

可使用下面的命令安装：

```bash
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
yum install gcc perl-ExtUtils-MakeMaker
yum -y install wget
```

然后，访问git官方站点下载最新版本源码：https://git-scm.com/download/linux

或者直接访问以下地址获取源码包:https://www.kernel.org/pub/software/scm/git/

### 2. 安装

```bash
# 下载
wget https://www.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz

# 解压
tar -zxvf git-2.9.5.tar.gz

# 进入解压后目录
cd git-2.9.5

# 安装
make prefix=/usr/local/git all 
sudo make prefix=/usr/local/git install

# 配置环境变量
echo "export PATH=/usr/local/git/bin:$PATH" >> /etc/profile
source /etc/profile
```

**检查版本:**

```bash
git --version
```



## 三、安装Gitlab

> 参考\借鉴\转载：
>
> [GitLab 详细安装步骤](https://blog.csdn.net/weixin_41981080/article/details/107071905)

- 在[下载地址](https://packages.gitlab.com/gitlab/gitlab-ce/packages/el/7/gitlab-ce-10.8.2-ce.0.el7.x86_64.rpm)下载安装包

- 将安装包上传到centos中，一般在 `/opt`目录下

- 在 `/opt`目录下新建` install.sh`文件，输入以下内容

  ```bash
  sudo rpm -ivh /opt/gitlab-ce-10.8.2-ce.0.el7.x86_64.rpm
  sudo yum install -y curl policycoreutils-python openssh-server cronie
  sudo lokkit -s http -s ssh
  sudo yum install postfix
  sudo service postfix start
  sudo chkconfig postfix on
  curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
  # 下面地址可以不用修改， 等待安装完成， 编译时在修改
  sudo EXTERNAL_URL="http://127.0.0.1" yum -y install gitlab-ce
  ```

- 并赋予 install.sh 可执行权限 执行命令行:    

  ```bash
  chmod 775 install.sh
  ```

- 执行脚本文件 `install.sh`,等待安装完成

  ```bash
  ./install.sh
  ```

- 执行编译,等待编译完成,需要较长时间

  ```bash
  gitlab-ctl reconfigure
  ```

- 重启服务

  ```bash
  gitlab-ctl restart
  ```

输入服务器ip即可正常访问











