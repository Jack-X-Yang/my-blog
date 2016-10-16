title: hexo + github + gitcafe 搭建个人博客
author: Jack-X-Yang
tags:
  - hexo
categories:
  - hexo
date: 2016-10-15 16:42:00
---
### 前言
---
最近发现学习效率比较低，决定搭个个人博客，一方面当作学习笔记，另一方面也对自己起一个监督的作用。

之前用过`jekyll`利用github的pages搭过个人博客，也用过`webpress`和`博客园`，但是都没弄到一半放弃了。`jekyll`是因为自己嫌配置麻烦，`webpress`和`博客园`是觉得主题太丑，并且自己个性化比较麻烦。由于本人是前端狗，所以看到`hexo`不错，决定折腾一下。

步骤比较笼统，但是都给了相应资料的链接。


### 目录
---
<!-- toc -->

- [前言](#前言)
- [目录](#目录)
- [安装node](#安装node)
- [安装git](#安装git)
- [安装hexo](#安装hexo)
- [初始化博客](#初始化博客)
- [撰写博客](#撰写博客)
- [生成静态页面](#生成静态页面)
- [发布到github和gitcafe上](#发布到github和gitcafe上)
- [后记](#后记)

<!-- tocstop -->
### 安装node
---
- windows 用户直接[node官网](https://nodejs.org/en/)下载，安装
- linux 用户推荐使用[nvm](https://github.com/creationix/nvm)安装

### 安装git
---
git下载地址 https://git-scm.com/downloads

注意： windows用户git安装时一定要安装bash

### 安装hexo
---
```shell
$ npm install hexo -g
```

### 初始化博客
---
- 新建文件夹作为博客的目录
- 切换到新建的目录，然后运行
```shell
$ hexo init
```
- 安装依赖，如果hexo已经安装好了则不需要再安装
```shell
$ npm i
```
  或者
	```shell
	$ npm install
	```
- 启动服务器
```shell
$ hexo serve
```
命令行会提示本地服务器访问的链接是http://localhost:4000/
打开链接就可以访问你的博客了

### 撰写博客
---
- 使用hexo命令撰写文章  
  准确的说应该是创建文章  
  hexo默认有三种布局（layout），分别是：post、page和draft
  - post就是普通的文章，存储在`source/_posts`文件夹里
  - page依照个人理解应该是页面，比如分类页面，about页面之类的  
  - draft就是草稿，草稿默认不显示，可以使用`publish`命令将草稿从`source/_drafts`移到`source/_posts`

  创建文章：
  ```shell
  $hexo publish [layout] <title>
  ```

  markdown文本编辑器强烈推荐atom下的[markdown-preview-enhanced](https://atom.io/packages/markdown-preview-enhanced)插件，功能超级强大

  参考hexo官网的文档 https://hexo.io/docs/writing.html
- 使用hexo-admin插件
切换到博客的目录，运行：
  ```shell
  $ npm install hexo-admin --save
  ```
  安装完毕后，运行：
  ```shell
  $ hexo serve
  ```
  打开http://localhost:4000/admin即可在网页中编辑自己的博客
  更加详细用法参照：https://github.com/jaredly/hexo-admin

### 生成静态页面
---
```shell
$ hexo generate
```
注意： 每次修改文章之后都要运行该命令，重新生成静态页面

如果嫌麻烦，可以使用下列命令来监视文件修改自动生成
```shell
$ hexo generate --watch
```

详情： https://hexo.io/zh-cn/docs/generating.html

### 发布到github和gitcafe上
---
- 首先申请账号
- 生成公钥
参考：https://git-scm.com/book/zh/ch4-3.html
- 添加公钥到github和gitcafe 参考：[添加公钥到github账户](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
- 发布到github和gitcafe上需要使用github和gitcafe的pages功能  
详情参考：
	- github： https://pages.github.com/
	- gitcafe：https://coding.net/help/doc/pages/index.html
- 测试github和gitcafe服务是否可用，可能会询问安全问题输入yes
	- github：ssh -T git@github.com
    - gitcafe：ssh -T git@coding.net
- 安装发布插件
```shell
$ npm install hexo-deployer-git --save
```
- 修改`_config.yml`配置文件
```shell
deploy:
  type: git
  message: [message]
  repo:
    github: <repository url>,[branch]
    gitcafe: <repository url>,[branch]
  extend_dirs:
    - [extend directory]
    - [another extend directory]
```
  详情参考： https://github.com/hexojs/hexo-deployer-git
- 部署命令
```shell
$ hexo generate
$ hexo deploy
```
  或者：
  ```shell
  $ hexo g -d
  ```
  注意： 可能会提示登录

### 后记
---
如果之后需要发布只需运行：
```shell
$ hexo g -d
```
即可

由于本人还是个初学者，水平有限，如果本文中有错误，希望大家不吝赐教
