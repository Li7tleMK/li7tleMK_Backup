title: "Mac下使用Charles实现对Android手机进行抓包"
date: 2015-04-01
comments: true
categories:
  - Android开发
tags:
  - Android抓包
  
---

以前在Windows下开发Android的时候有强大的Fiddler这个抓包工具，用起来很爽。但是换到Mac环境以后发现Mac下也有Fiddler，但是得先安装[Mono运行时](http://www.mono-project.com/download/)，比较折腾（关键是我有轻微洁癖，不想装一大堆东西而且平时不怎么用的Mono）。经过一番搜索发现Mac下有Charles这个强大的抓包工具，发现用起来还是很简单的，虽然没有Windows下的Fiddler那么功能强大，但是也基本够用。

#### Charles基本设置

* 端口设置：在菜单上选择`Proxy`->`Proxy Settings...`，然后配置端口，默认：8888

<!--more-->

<img style="clear:both;display:block;margin:auto;width:500px;height:400px" src="http://7xi85h.com1.z0.glb.clouddn.com/charles-proxy-setting.png" alt="" />
	
* 流量控制：在菜单上选择`Proxy`->`Throttling Settings...`，勾选`Enable Throttling`以后选择限制的流量，也可以手动输入上行、下行大小。
	
<img style="clear:both;display:block;margin:auto;width:500px;height:480px" src="http://7xi85h.com1.z0.glb.clouddn.com/Throttling-settings.png" alt="" />
	
#### Android设备端或模拟器设置代理

* 首先确认你的Android设备或模拟器和Mac在同一局域网下。比如你的Mac地址是`192.168.111.126`
* 配置你的Android设备或者模拟器代理地址为`192.168.111.126`，端口号：`8888`（默认）。这里我使用模拟器，如果手机配置原理是一样的。

<img style="clear:both;display:block;margin:auto;width:384px;height:640px" src="http://7xi85h.com1.z0.glb.clouddn.com/out.gif" alt="" />

* 配置好以后在你在Android端发起的任何http请求都会被Charles捕获到。
<img style="clear:both;display:block;margin:auto;width:600px;height:420px" src="http://7xi85h.com1.z0.glb.clouddn.com/catch.gif" alt="" />
	
	
	



