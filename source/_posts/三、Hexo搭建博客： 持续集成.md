---
title: 三、Hexo搭建Next主题的博客： 持续集成
categories:
- Hexo博客
---

## 创建持续集成的git分支

* 注册[Travis CI](https://travis-ci.org/) 账号，绑定github

* 在github的仓库：`xxx.github.io`，上新建一个分支`hexo`。

  ```
  # 克隆项目到本地
  git clone https://github.com/xxx/xxx.github.io.git
  # 创建并切换到 hexo 分支
  git checkout -b hexo
  ```

* 在 `hexo` 分支保存博客项目的源代码

  * 将 `hexo` 分支下的文件除 `.git` 目录外全部删除
  * 将博客源码文件拷贝到该目录下，并提交 Commit 到 `hexo` 分支.

* 将本地 `hexo` 分支内容提交到 GitHub 远程仓库

  ```bash
  # 提交本地 hexo 分支到远程仓库的 hexo 分支
  git push origin hexo:hexo
  ```



经过这样的配置，我们博客仓库项目文件应该是这样的：

- 在 `hexo` 分支保存博客项目的源代码
- 在 `master` 分支保持项目的静态文件（即 `public` 文件夹下的内容）

<!-- more -->

## 配置持续集成文件

> `.travis.yml` 是 Travis CI 的部署配置文件，Travis CI 部署时会自动读取我们每次 Commit 中是否包含 `.travis.yml` ，有此文件才会开始部署。
>
> 在博客项目源代码分支下（ `hexo` 分支）创建文件 `.travis.yml`

```
language: node_js # 编译语言、环境

sudo: required # 需要管理员权限

dist: xenial # 指定 CI 系统版本为 Ubuntu16.04 LTS

node_js: stable #Node.js 版本

branches:
  only:
    - hexo # 只有 hexo 分支检出更改才触发 CI

before_install: 
  - export TZ='Asia/Shanghai' #配置时区为东八区 UTC+8
  - npm install hexo-cli # 安装 hexo
#  - sudo apt-get install libpng16-dev # 安装 libpng16-dev CI 编译出现相关报错时请取消注释

install:
  - npm install # 安装依赖

script: # 执行脚本，清除缓存，生成静态文件
  - hexo clean
  - hexo generate

deploy:
  provider: pages
  skip_cleanup: true # 跳过清理
  local_dir: public # 需要推送到 GitHub 的静态文件目录 
  name: $GIT_NAME # 用户名变量
  email: $GIT_EMAIL # 用户邮箱变量
  github_token: $GITHUB_TOKEN # GitHub Token 变量
  keep-history: true # 保持推送记录，以增量提交的方式
  target-branch: master # 推送的目标分支 local_dir->>master 分支
  on:
    branch: hexo # 工作分支
```



## 自动部署

经过以上步骤的配置，发布博客的命令就变更为：

```bash
# 切换到 hexo 分支
git checkout hexo

# 提交新博文
git add .
git commit -m "Publish new post."

# 推送到远程仓库
git push
```





参考网站：

* [Easy Hexo](https://easyhexo.com/1-Hexo-install-and-config/1-3-config-hexo.html)
