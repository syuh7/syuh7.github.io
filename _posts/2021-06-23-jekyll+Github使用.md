---
layout: post
title:  "jekyll+Github使用"
date:   2021-06-23 11:50:27 +0800
categories: jekyll update
---

# jekyll+Github使用

## 安装

> macO环境下安装：[官方教程](https://www.jekyll.com.cn/docs/installation/macos/)



## 使用

文章都放在_posts目录下面，按照格式年-月-日-文章名.markdown

在_posts下建立文件:



- title: 文章标题
- date: 显示日期
- categories: 标签分类 
   文章完整内容如下:







运行

```bash
bundle exec jekyll serve --trace
```



## jekyll主题

[几个简约Jekyll主题推荐](https://blog.csdn.net/chen_z_p/article/details/103132625)

[Mac下使用Jekyll和github搭建个人博客](https://blog.csdn.net/alex_my/article/details/56481922)

[NexT](theme-next.simpleyyt.com/getting-started.html)

```
gem install bundler
```





## 参考

[参考1](https://blog.csdn.net/weixin_34203832/article/details/89621853)

[参考2](https://www.jekyll.com.cn/docs/installation/macos/)

[参考3](https://www.jekyll.com.cn/docs/installation/macos/)







## 安装`Ruby`

```bash
==> ruby
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/2.6.0/bin

You may want to add this to your PATH.

ruby is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have ruby first in your PATH run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile

For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"

For pkg-config to find ruby you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/ruby/lib/pkgconfig"

kai-Pro:~ kangkai$
```





## HomeBrew

```bash
# 安装一个包
brew install <package_name>

# 更新 Homebrew 在服务器端上的包目录
brew update

# 查看是否需要更新
brew outdated

# 更新包
brew upgrade <package_name>

# 查看安装过的包列表（包括版本号）
brew list --versions

# 清理旧版本的包缓存
brew cleanup
```







## 配置文件

> `.bash_profile`一般在用户目录下，是隐藏文件
>
> `Command + Shift + .` 显示/隐藏文件

修改`.bash_profile`后，在其所在目录下执行以下命令使其生效

```bash
source .bash_profile
```







## Github + jekyll 搭建

