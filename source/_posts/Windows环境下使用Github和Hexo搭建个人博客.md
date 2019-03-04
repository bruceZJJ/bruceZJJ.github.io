---
title: Windows环境下使用Github和Hexo搭建个人博客
date: 2018-06-08 17:44:03
tags: [GitHub,Hexo,个人博客搭建]
---
## 安装Hexo
前提条件：已安装git、node.js
在你喜欢的位置创建一个新的文件夹建立网站，打开新建文件夹
在文件夹内右键选择“Git Bash Here”打开windows下的命令行工具
输入如下命令在当前文件夹中建立一个新的网站，等待克隆文件下载

``` bash
$ hexo init
```

<!--more-->

安装完成后，使用如下命令生成静态文档

``` bash
$ hexo g
```

使用如下命令将网站部署到本地服务器上，默认端口是4000
可以通过[http://localhost:4000](http://localhost:4000/)访问
这样我们可以在部署到GitHub之前在本地服务器进行预览

``` bash
$ hexo s
```

如果提示端口被占用，则可以使用如下命令来自定义端口

``` bash
$ hexo -p xxxx
```

## 创建repository

在部署之前，我们先要在GitHub上面创建一个repository,点击左上角的小猫图标进入主页,再点击“New repository”
![](/img/New repository.png)
Repository name为：yourname.github.io,Description自定义，点击“Create repository”即可
![](/img/New repository details.png)

## 配置Github SSH
创建完repository之后，配置GitHub SSH
在桌面上右键选择“Git Bash Here”打开windows下的命令行工具，输入如下命令

```bash
$ ssh-keygen -t rsa -C "your's emaill address"
```

回车，提示你文件保存路径，再按回车
下面接着提示你输入(passphrase)密码，输入你要设置的密码(passphrase)
建议不要设置，即密码为空，这样以后更新部署的时候就不需要输入密码
注意这个密码你是看不到的，不管你输入是什么，显示的都是空，回车后输入确认密码

在之前文件保存的路径里可以看到两个文件id_rsah和id_rsa.pub，用文本编辑器打开id_rsa.pub，将其中的内容复制下来
在GitHub主页点击头像，选择setting选项
![](/img/Settings.png)
进入setting选项，进入选择“SSH and GPG keys”,选择New SSH key
![](/img/New SSH Key.png)
Title自定义，将复制的内容粘到Key里面，点击Add SSH key
![](/img/New SSH Key Details.png)

## 部署到GitHub上
为了部署到GitHub上面，我们还需要安装hexo-deployer-git
使用npm（node package manager，node包管理工具）来安装
输入如下命令

```bash
$ npm install hexo-deployer-git --save
```

此时会提示 This package is no longer maintained，稍等片刻就会安装好

之后我们还需要配置一下_config.yml
使用文本编辑器打开_config.yml，在文件最后找到deploy设置，
配置如下信息：
![](/img/deploy.png)
repo：你创建的github仓库的网址
branch：分支的名称
message：提交信息
可以同时又多个deployer，hexo会依照顺序执行每个deployer。

依次输入如下命令

```bash
$ hexo g
```
```bash
$ hexo d
```

输入之前设置的密码(之前未设置密码则不需要输入，直接部署)
就可以部署到github上面了
输入youname.github.io就可以访问了
