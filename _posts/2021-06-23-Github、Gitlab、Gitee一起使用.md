---
layout: post
title: "Github、Gitlab、Gitee等仓库一起使用"
date: 2021-06-23 11:50:27 +0800
categories: git
---



## `Github`、`Gitlab`、`Gitee`等仓库一起使用

### 1. 生成对应的仓库密钥

```bash
ssh-keygen -t rsa -C "XXX的邮箱" -f ~/.ssh/密钥名
```

```bash
ssh-keygen -t rsa -C "github邮箱" -f ~/.ssh/github_id-rsa
ssh-keygen -t rsa -C "gitlab邮箱" -f ~/.ssh/gitlab_id-rsa
ssh-keygen -t rsa -C "gitee邮箱" -f ~/.ssh/gitee_id-rsa
```

### 2. 将公钥添加到仓库中

```
cat github_id-rsa
```

结果应是以仓库邮箱名结尾，将密钥复制后添加到仓库中。

### 3. 添加配置文件

在`~/.ssh`路径下添加配置文件`config`

```bash
Host github
    Port 22
    User git
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_id-rsa
Host gitlab
    Port 22
    User git
    HostName gitlab.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gitlab_id-rsa
Host gitee.com     # 这边如果只写gitee，会出现匹配不到的情况
    Port 22
    User git
    HostName gitee.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gitee_id-rsa
```

配置文件解释：

```bash
Host
    它涵盖了下面一个段的配置，我们可以通过他来替代将要连接的服务器地址。
    这里可以使用任意字段或通配符。
    当ssh的时候如果服务器地址能匹配上这里Host指定的值，则Host下面指定的HostName将被作为最终的服务器地址使用，并且将使用该Host字段下面配置的所有自定义配置来覆盖默认的`/etc/ssh/ssh_config`配置信息。
Port
    自定义的端口。默认为22，可不配置
User
    自定义的用户名，默认为git，可不配置
HostName
    真正连接的服务器地址
PreferredAuthentications
    指定优先使用哪种方式验证，支持密码和秘钥验证方式
IdentityFile
    指定本次连接使用的密钥文件
```

### 4. 配置仓库

```bash
github工作仓库:~/workspace/github
gitlab工作仓库:~/workspace/gitlab
gitee工作仓库：~/workspace/gitee
```

操作如下：

```
global 全局的
local  本地的

#gitlab
cd ~/workspace/gitlab
git init
git config --global user.name 'xxxx'
git config --global user.email 'xxxx@xxx.com'

#github
cd ~/workspace/github
git init
git config --local user.name 'xxxx'
git config --local user.email 'xxxx@xxx.com'
```

### 5. 测试

```bash
ssh -T git@github.com
ssh -T git@gitlab.com
ssh -T git@gitee.com
```

注⚠️：如果要看匹配SSH的时候，具体的操作，可以加上`-V`

```bash
ssh -T -v git@github.com
```



> 参考/转载自：
>
> [github和gitlab仓库一起使用](https://www.cnblogs.com/bdhk/p/7423329.html)

---

## 操作

### 1. 查看公钥信息

```bash
cd ~/.ssh
ls
```

目录下的文件

```bash
config
gitee_id-rsa.pub	
github_id-rsa.pub	
gitlab_id-rsa.pub	
id_rsa.pub		
known_hosts
gitee_id-rsa	
github_id-rsa		
gitlab_id-rsa		
id_rsa
```

需要哪个就`cat`哪个

```bash
cat id_rsa.pub
```

### 2. 删除公钥

```bash
mkdir key_backup
cp id_rsa* key_backup
rm id_rsa*
```

### 3. 生成公钥

```bash
ssh-keygen -t rsa -C "你的邮箱"
```
