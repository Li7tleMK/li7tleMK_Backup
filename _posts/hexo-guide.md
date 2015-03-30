title: "hexo的简单使用"
date: 2015-03-08
comments: true	
tags: 
  - hexo
  
---

## 什么是hexo
[hexo](http://hexo.io)是一个基于Node.js的静态博客生成系统，类似Jekyll、Octopress、Pelican，可以方便的托管在github、gitcafe上。该系统的特点是快速、简单、强大的Node.js博客框架。官网原话：
> A fast, simple & powerful blog framework, powered by Node.js.

* 快速：只需几步就能搭建一个博客。
* 简单：从部署、创建、写博客一共只有几条命令。
* 强大：兼容于Windows、Mac、Linux，插件多、主题丰富并可定制。

<!--more-->
<br />
## 怎样搭建一个hexo博客
1. 安装Git
Mac和Windows用户可以直接从[官网](http://git-scm.com/)下载安装。Linux用户请使用apt-get（Ubuntu）或者yum（Centos）。

2. 安装Node.js
也是从[官网](https://nodejs.org/download/)下载安装，Mac是pkg文件，Windows是msi，Linux请使用apt-get(Ubuntu)或yum(Centos) 。在命令行输入`node -v`，查看是否安装成功。

3. 安装hexo
以官网最新版本（3.0.0）为例：

	$ npm install hexo-cli -g
	
在命令行执行`hexo -v`可以查看是否安装成功。

4. 创建hexo目录
安装好Hexo以后，可以在你指定的目录下执行`hexo init blog`（假设你的博客目录是blog），windows用户需右键选择`git bash`，然后执行此命令。成功执行后会看到blog目录下已经有了网站所需的所有文件。

5. 安装依赖包
进入blog目录下，执行`npm install`。

6. 本地查看

## hexo基本命令的使用

* 创建一篇文章

<!--示例代码-->
	$ hexo new title

* 生成静态文件：

<!--示例代码-->
	$ hexo g
	
* 本地查看：

<!--示例代码-->
	$ hexo s
	
浏览器直接打开`http://127.0.0.1:4000/`就可以看到已经部署好的个人博客。更多功能请查看[官网](http://hexo.io/docs/commands.html)。
