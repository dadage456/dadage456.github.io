---
title: 一、Hexo搭建博客： 快速搭建
categories:
- Hexo博客
---


### Hexo生成博客原理

> Hexo生成的静态网站，主要是把.md文件生成.html文件。生成html文件放在**public/**文件夹下。
>
> 部署网站是把**public/**里面的内容部署到网站上。



### 快速创建博客

```bash
# !bin/bash
$ npm install hexo-cli -g

$ hexo init blog

$ cd blog

$ npm install

$ hexo server
```
<!-- more -->


### Hexo常用命令简介

| 命令                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `$ hexo init [folder]` | 新建一个网站                                                 |
| `$ hexo new page XXX`  | 会创建一个 `source/XXX/index.md` 文件                        |
| `$ hexo generate `     | 生成静态文件。存放在/public文件夹下，**部署静态网站也是public中的内容** |
| `$ hexo generate -d`   | 生成静态文件, 立即部署网站                                   |
| `$ hexo server`        | 启动服务器。默认情况下，访问网址为： `http://localhost:4000/` |
| `$ hexo deploy`        | 部署之前预先生成静态文件                                     |
| `$ hexo clean`         | 清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。     |



### Hexo博客配置

> 通过**_config.yml**，修改博客的配置

* 基本信息

  ```yaml
  # Site
  title: 网站名称
  subtitle: '网站副标题'
  description: '网站描述'
  keywords: '网站的关键词。使用半角逗号 , 分隔多个关键词。'
  author: 您的名字
  language: 'zh-CN'						# 网站使用的语言。，zh-CN【中文简体】
  timezone: 'Asia/Shanghai'		# 网站时区
  
  # URL
  url: http://yoursite.com   	#网站host
  
  # 如果你的博客地址是'http://yoursite.com/child' 需要设置 root: '/child/'
  root: /									
  
  # 文章的链接格式：http://yoursite.com/title/
  permalink: :post_title/		
  ```

  

* 配置博客Next主题

  执行以下命令，将next主题下载到theme文件夹中。

  ```bash
  # !bin/bash
  $ cd blog
  $ git clone https://github.com/theme-next/hexo-theme-next /theme/next
  ```

  修改**_config.yml**文件中`theme: next`配置完毕！
  
  执行 `hexo server`本机查看配置效果。



参考网站：

* [Easy Hexo](https://easyhexo.com/1-Hexo-install-and-config/1-3-config-hexo.html)
