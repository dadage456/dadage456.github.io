---
title: 四、Hexo搭建博客： 标签、分类、菜单配置
categories:
- Hexo博客
---


> 默认生成的博客的标签页和分类页不能访问。这里介绍如何配置标签页、分类页，以及文档中设置标签与分类。

<!-- more -->

#### 配置标签页面、分类页面

* 创建新页面

  ```bash
  $ hexo new page "categories"
  
  $ hexo new page "tags"
  ```

* 修改新建的页面/source/tags/index.md文件。头部追加

  ```
  ---
  title: 标签
  date: 2016-10-21 11:59:10
  type: "tags"
  comments: false
  ---
  ```

* 修改新建的页面/source/categories/index.md文件。头部追加

  ```markdown
  ---
  title: 分类
  date: 2016-10-21 11:59:10
  type: "categories"
  comments: false
  ---
  ```

* 修改主题的配置文件 _config.yml (next主题的配置路径：/themes/next/)

  ```yaml
  menu:
    home: /
    archives: /archives
    categories: /categories
    tags: /tags
  ```



#### 文档中使用标签与分类

在文档的顶部写入一下内容

```yaml
---
title: 文档标题
categories:
- [分类, 子分类]
- 分类
tags:
- [标签1,标签2]
---
```



#### 配置自定义菜单

> 文档中配置一个【每日学习】的分类，如何把这个分类直接配置到菜单上显示，可以便捷快速的访问该分类下的文章。

* 修改主题的配置文件 _config.yml (next主题的配置路径：/themes/next/)

  ```yaml
  menu:
    home: /
    archives: /archives
    categories: /categories
    tags: /tags
    study: /categories/每日学习
  ```

* 找到主题文件夹下的languages文件夹，找到对应的语言配置文件。这里我们修改zh-CN.yml

  ```yaml
  menu:
    home: 首页
    archives: 归档
    categories: 分类
    tags: 标签
    study: 每日学习
  ```



#### next主题设置阅读全文按钮

> next主题的主页面显示文章的全部内容。希望显示文章的一部分，点击“阅读全文”查看文章

* 在文章中使用 `<!-- more -->` 手动进行截断，Hexo 提供的方式 推荐
* 在文章的 [front-matter](https://hexo.io/docs/front-matter.html) 中添加 `description`，并提供文章摘录



参考网站：

* [Easy Hexo](https://easyhexo.com/1-Hexo-install-and-config/)
