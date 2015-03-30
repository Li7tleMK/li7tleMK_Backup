title: "移动App自动化测试（二）"
date: 2015-03-14
comments: true
categories:
  - 自动化测试
tags: 
  - 移动App自动化测试
  
---

**什么是Appium？**

Appium是[Sauce Labs](https://saucelabs.com/)公司的一个移动测试框架，该公司专注于Web、Mobile和桌面应用的自动化测试，为企业开发者提供Web应用测试平台。

**它的优点：**

* 开源；
* 支持Native App、Hybird App、Web App；
* 支持Android、iOS、Firefox OS；
* Server也是跨平台的，你可以使用Mac OS X、Windows或者Linux；
<!--more-->

**它的哲理是：**

* 用Appium自动化测试不需要重新编译App；
* 支持很多语言来编写测试脚本，Java、Javascript、PHP、Python、C#、Ruby等主流语言；
* 不需要为了自动化测试来重造轮子，因为扩展了WebDriver。（WebDriver是测试WebApps的一种简单、快速的自动化测试框架，所以有Web自动化测试经验的测试人员可以直接上手）；
* 移动端自动化测试应该是开源的；

**它的设计理念：**

* Client/Server架构，运行的时候Server端会监听Client端发过来的命令，翻译这些命令发送给移动设备或模拟器，然后移动设备或模拟器做出响应的反应。正是因为这种架构，所以Client可以使用[Appium client libraries](http://appium.io/downloads)多种语言的测试脚本，而且Server端完全可以部署在服务器上，甚至云服务器。
* Session，每个Client连接到Server以后都会有一个Session ID，而且Client发送命令到Server端都需要这个Session ID，因为这个seesion id代表了你所打开的浏览器或者是移动设备的模拟器。所以你甚至可以打开N个Session，同时测试不同的设备或模拟器。
* Desired Capabilities，其实就是一个键值对，设置一些测试的相关信息来告诉Server端，我们需要测试iOS、还是Android，或者换是WebApp等信息。
* Appium Server，使用Node.js写的，所以可以直接用NPM来进行安装。
* Appium Client，可以使用Java、PHP、Python、Javascript、C#、Ruby等主流语言来编写测试用例。

**相关限制：**

* 如果你在Windows使用Appium，你没法使用预编译专用于OS X的.app文件，因为Appium依赖OS X专用的库来支持iOS测试，所以在Windows平台你不能测试iOS Apps。这意味着你只能通过在Mac上来运行iOS测试。

**总结：**

* 在iOS部分是封装了UIAutomation；Android 4.2以上是用UiAutomator，Android 2.3 ~ 4.1用的是 Instrumentation，也就说Appium同时封装了UiAutomator和Instrumentation。所以Appium拥有了以上几大框架的所有优点：能跨App，支持Native App、Hybird App、Web App的测试；不仅支持N种语言来编写你的测试脚本，而且可以让开发人员完全脱离源代码来编写。

___
部分内容参考 [乙醇的cnblog](http://www.cnblogs.com/nbkhic/p/3803804.html)




