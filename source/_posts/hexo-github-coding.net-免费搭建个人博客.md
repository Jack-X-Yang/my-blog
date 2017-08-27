title: hexo + github + coding.net 免费搭建个人博客
author: Jack-X-Yang
tags:
  - hexo

categories:
  - hexo

date: 2016-10-15 16:42:00
updated: 2017-8-27 15:02:00

---

# 前言

---
最近发现学习效率比较低，决定搭个个人博客，一方面当作学习笔记，另一方面也对自己起一个监督的作用。

之前用过`jekyll`利用github的pages搭过个人博客，也用过`webpress`和`博客园`，但是都搞到到一半放弃了。`jekyll`是因为自己对`ruby`并不了解。`webpress`和`博客园`是觉得主题太丑，并且自己个性化比较麻烦。由于本人是前端狗，所以看到`hexo`不错，决定折腾一下。

免费主要是通过github和coding.net上面的pages服务实现的。
<!-- more -->

为什么要分别在github和coding.net两个平台部署？
主要是因为github是在国外，国内通过coding.net访问比较快，而github用的人比较多，通过同时部署到两个平台，能够充分利用两者的优点。

主要有配置hexo运行环境、配置hexo发布环境、撰写博客、编译博客和发布博客等几个步骤。

步骤比较笼统，但是都给了相应资料的链接。

# hexo运行环境配置

---

## 安装node
Node.js®是一个基于[Chrome V8 引擎](https://developers.google.com/v8/)的 JavaScript 运行时。hexo需要node作为运行环境，通过node运行hexo代码，从而将我们写的markdown文件，解析并编译成静态的HTML、CSS和javascript文件。而这些文件就是我们博客的源码。

- windows 用户直接[node官网](https://nodejs.org/en/)下载，安装
- linux 用户推荐使用[nvm](https://github.com/creationix/nvm)安装

## 安装git
除了安装上述的node还是不行的，hexo通过node虽然可以生成网页，但是还需要发发布服务器上。github.com和coding.net都提供了免费的个人主页服务，因此我们可以将自己的博客发布到上面。这时候需要借助git将我们生成的博客源码推送到github和coding.net的仓库中，然后利用免费的个人主页服务，就可以免费的将我们的博客发布到网上了。
同时git也是一个版本控制软件，通过使用git可以保存我们的博客历史版本。

- windows用户可以去https://git-scm.com/downloads下载，安装
windows用户git安装时一定要安装bash
- linux用户可以通过自己的自带的包管理器安装，如ubuntu：
```
sudo apt install git
```
## 安装hexo
按照官方的文档安装即可，官方文档写的非常棒。
传送门：
https://hexo.io/zh-cn/docs/index.html

# 初始化博客

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

# 撰写博客

---

- 博客类型简介  
  hexo默认有三种布局（layout），分别是：post、page和draft
  - post就是普通的文章，存储在`source/_posts`文件夹里
  - page依照个人理解应该是页面，比如分类页面，about页面之类的  
  - draft就是草稿，草稿默认不显示，可以使用`publish`命令将草稿从`source/_drafts`移到`source/_posts`

  具体如何创建和撰写博客，参考hexo官网的文档 https://hexo.io/zh-cn/docs/writing.html
- markdown编辑器安利
  - Yu Writer是一个非常棒的markdown编辑器，界面十分的简介，并且还支持hexo博客
  - markdown文本编辑器强烈推荐atom下的[markdown-preview-enhanced](https://atom.io/packages/markdown-preview-enhanced)插件，功能超级强大

- 使用hexo-admin插件
除了使用本地的markdown编辑器之外，使用网页版的也非常不错，hexo-admin就提供这样的功能
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

# 生成静态页面

---

我们写好的markdown文件并不能直接通过浏览器查看，除非你的浏览器装了相应的插件。这时候需要将markdown文件编译成静态网页，就需要执行如下命令。
```shell
$ hexo generate
```
注意： 每次修改文章之后都要运行该命令，重新生成静态页面

如果嫌麻烦，可以使用下列命令来监视文件修改自动生成
```shell
$ hexo generate --watch
```
详情： https://hexo.io/zh-cn/docs/generating.html

# 发布到github和coding.net上

---

- 首先申请账号
分别在github和coding.net上面注册账号，注册完毕之后开通pages功能。
	- github： https://pages.github.com/
	- coding.net：https://coding.net/help/doc/pages/index.html
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
    coding: <repository url>,[branch]
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
  注意： 第一次发布时可能会提示登录，只要根据提示，输入对应的账号秘密即可

# 后记

----

- 如果之后需要发布只需运行：
```shell
$ hexo g -d
```
即可

- 如果不想安装`hexo-cli`，可以在`package.json`文件中添加下列配置：

```json
"scripts": {
    "server": "hexo server",
    "deploy": "hexo d -g"
}
```
然后直接运行

```
$ npm run server
$ npm run deploy
```
 即可


由于本人还是个初学者，水平有限，如果本文中有错误，希望大家能够指出来 。