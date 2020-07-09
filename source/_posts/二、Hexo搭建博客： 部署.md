---
title: 二、Hexo搭建Next主题的博客： 部署
categories:
- Hexo博客
---


### 前言

> Hexo可以直接部署到github上，通过 **https://用户名.github.io** 访问博客。
>
> 也可以部署到云服务器上，通过Nginx搭建静态站点访问博客。
>
> 持续集成：修改文件提交到git上，自动实现部署。

<!-- more -->

### 部署到github上

* 配置ssh公钥到github。使用ssh访问github.

* github创建一个公共仓库。仓库名: 用户名.github.io

* 配置博客的_config.yml文件

  ```yaml
  deploy:
    type: 'git'
    repo:
      github: git@github.com:用户名/用户名.github.io.git
    branch: master
  ```

* 执行部署命令 `hexo g -d`，使用https://用户名.github.io访问博客。

  

### 部署到云服务上

* 配置ssh公钥到云服务。可以使用ssh访问云服务。

* 创建blog.git

  ```bash
  # !bin/bash
  $ mkdir -p /var/repo    //新建 var/repo 目录
  $ cd /var/repo          //进入该目录
  $ git init --bare blog.git   //新建一个裸仓库
  $ chown -R git:git blog.git
  ```

* 配置 Git Hooks

  使用 vim 命令在 `/var/repo/blog.git/hooks` 目录下创建 `post-receive` 文件

  ```bash
  vim /var/repo/blog.git/hooks/post-receive
  ```

  并且在 `post-receive` 文件中写入以下内容

  ```bash
  #!/bin/sh
  git --work-tree=/home/www/hexo --git-dir=/var/repo/blog.git checkout -f
  ```

  提升 `post-receive` 的可执行权限

  ```bash
  chmod +x /var/repo/blog.git/hooks/post-receive
  ```

  创建目录

  ```
  mkdir -p /home/www/hexo      //创建目录
  chown -R root:root /home/www/hexo   //更改目录所有者
  ```

* 安装Nginx，配置静态目录

  ```bash
  $ yun install -y nginx
  
  $ vi /etc/nginx/nginx.conf
  
  # nginx.conf 修改内容
  server {
          listen       80 default_server;
          listen       [::]:80 default_server;
          server_name  _;
  -       root         /data/www;
  +       root         /home/www/hexo;
   }
  
  ```

* 配置_config.yml

  ```
  deploy:
    type: 'git'
    repo:
      cent: root@服务器host:/var/repo/blog.git
    branch: master
  ```

* 执行部署命令`hexo g -d`



> 注意：
>
> 这里使用root访问服务器上的blog.git。
>
> 安全起见应该创建一个git用户访问blog.git。git用户取消登录shell的权限。



参考网站：

* [Easy Hexo](https://easyhexo.com/1-Hexo-install-and-config/1-3-config-hexo.html)
