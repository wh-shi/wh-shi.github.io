---
title: Mac下Hexo+GitHub搭建个人博客
tags:
  - Hexo
  - GitHub
date: 2017-04-03 18:39:50
categories: GitHub
---

近来无意间发现了可通过GitHub来免费搭建自己的博客，无需申请域名，无需蛋疼的备案，无需购买主机，简直不能太兴奋了，于是这俩天研究了下，现在把搭建过程记录下来。

# 1 安装Hexo

## 1.1 安装前提

Hexo运行前需先安装[Node.js](https://nodejs.org)和[Git](https://git-scm.com/)
Node.js安装好后，执行`node -v`验证成功与否

``` bash
shiwenhuandeMacBook-Pro:~ shiwenhuan$ node -v
v7.7.4
```

Git安装好后，执行`git --version`验证成功与否

``` bash
shiwenhuandeMacBook-Pro:~ shiwenhuan$ git --version
git version 2.10.1
```

## 1.2 使用npm安装Hexo

Node.js的安装已经包含了[npm](https://docs.npmjs.com/)的安装，现在执行`npm install -g hexo-cli`安装Hexo，完成后再执行`hexo -v`验证成功与否

``` bash
shiwenhuandeMacBook-Pro:node-js-example shiwenhuan$ hexo -v
hexo-cli: 1.0.2
os: Darwin 16.5.0 darwin x64
http_parser: 2.7.0
node: 7.7.4
v8: 5.5.372.42
uv: 1.11.0
zlib: 1.2.11
ares: 1.10.1-DEV
modules: 51
openssl: 1.0.2k
icu: 58.2
unicode: 9.0
cldr: 30.0.3
tz: 2016j
```

# 2 使用Hexo建站

## 2.1 初始化

``` bash
hexo init example
cd example
npm install
```

其中**example**为网站代码所在的目录

``` bash
shiwenhuandeMacBook-Pro:wh-shi.github.io shiwenhuan$ pwd
/Users/shiwenhuan/GitHub/wh-shi.github.io
shiwenhuandeMacBook-Pro:wh-shi.github.io shiwenhuan$ ll
total 24
drwxr-xr-x    9 shiwenhuan  staff   306  4  3 23:41 ./
drwxr-xr-x    7 shiwenhuan  staff   238  4  3 23:41 ../
-rw-r--r--    1 shiwenhuan  staff    65  4  3 23:41 .gitignore
-rw-r--r--    1 shiwenhuan  staff  1483  4  3 23:41 _config.yml
drwxr-xr-x  286 shiwenhuan  staff  9724  4  3 23:42 node_modules/
-rw-r--r--    1 shiwenhuan  staff   443  4  3 23:41 package.json
drwxr-xr-x    5 shiwenhuan  staff   170  4  3 23:41 scaffolds/
drwxr-xr-x    3 shiwenhuan  staff   102  4  3 23:41 source/
drwxr-xr-x    3 shiwenhuan  staff   102  4  3 23:41 themes/
shiwenhuandeMacBook-Pro:wh-shi.github.io shiwenhuan$
```
## 2.2 代码编译

``` bash
hexo generate
hexo server
```
现在访问http://localhost:4000
{% asset_img image/localhost_4000_init.png example localhost page %}

## 2.3 Hexo详解

更多Hexo资料请参考[Hexo官网文档](https://hexo.io/zh-cn/docs/)

# 3 使用GitHub发布网站

## 步骤

1. 注册[GitHub](https://github.com)账户

2. 在GitHub上新建一个远程仓库，仓库名为`wh-shi.github.io`，`wh-shi`必须为你GitHub的用户名

3. 在本地网站代码所在的目录example下，执行`git flow init`，不懂[git-flow](https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow)的自行Google

4. 关联远程仓库`wh-shi.github.io`
  ``` bash
   ## 若未设置，请先设置
   # git config --global user.name "******"
   # git config --global user.email "******"
   git remote add origin git@github.com:wh-shi/wh-shi.github.io.git
  ```
5. 修改_config.yml文件，通过git提交网站代码到远程仓库的master分支

6. 执行hexo deploy即可将代码push到远程仓库master分支中
  ``` bash
  # Deployment
  ## Docs: https://hexo.io/docs/deployment.html
  deploy:
  type: git
  repo: git@github.com:wh-shi/wh-shi.github.io.git
  ## https://wh-shi.github.io 访问的将是master分支的内容；网站其它内容的代码则放在默认的develop分支
  branch: master
  ```

7. 访问https://wh-shi.github.io

8. 执行一下命令即可将代码改动提交到远程仓库的develop分支中
  ``` bash
  git add .
  git commit -m "*****"
  git push origin develop
  ```
