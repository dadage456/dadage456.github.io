---
title: 一、Hexo搭建博客： 快速搭建
categories:
- Hexo博客
---

## Hexo是怎么生成博客的

主要是2个目录：

* `source/_posts/`: 存放markdown文件

* `public/`: hexo生成的html文件

部署网站其实就是把`public/`文件夹中的内容部署到服务器上.



## 快速创建博客

```bash
# !bin/bash
$ npm install hexo-cli -g

$ hexo init blog

$ cd blog

$ npm install

$ hexo server
```
<!-- more -->



## Hexo常用命令简介

| 命令                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `$ hexo init [folder]` | 新建一个网站                                                 |
| `$ hexo new page XXX`  | 会创建一个 `source/XXX/index.md` 文件                        |
| `$ hexo generate `     | 生成静态文件。存放在/public文件夹下，**部署静态网站也是public中的内容** |
| `$ hexo generate -d`   | 生成静态文件, 立即部署网站                                   |
| `$ hexo server`        | 启动服务器。默认情况下，访问网址为： `http://localhost:4000/` |
| `$ hexo deploy`        | 部署之前预先生成静态文件                                     |
| `$ hexo clean`         | 清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。     |



## Hexo博客配置

通过修改`_config.yml`, 配置博客

### 基本信息配置

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



### 配置博客Next主题

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
