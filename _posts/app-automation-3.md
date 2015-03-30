title: "移动App自动化测试（三）"
date: 2015-03-16
comments: true
categories:
  - 自动化测试
tags:
  - 移动App自动化测试
  
---

## Appium Server端的简单安装

Appium是支持Mac、Windows和Linux的。

1. 安装Node.js：Mac推荐使用[Homebrew](http://brew.sh/)，Windows可以直接[官网](https://nodejs.org/)下载；如果是Windows用户，把你的安装路径添加到环境变量方便使用（默认是在C:\Program Files\Nodejs\）npm。

2. 安装Git。

3. 安装JDK，并设置JAVA_HOME环境变量。

4. 安装Android SDK，并设置ANDROID_HOME环境变量；把sdk下的tools和platform-tools也设置环境变量。
<!--more-->

安装好以上所有依赖，就可以安装Appium Server了。Windows和Mac下都有2种使用安装方式：

* 使用命令行安装：

<!--code-->
	$ npm install -g appium
	$ appium &
	
* 或者直接[下载GUI](http://appium.io/slate/en/master/?ruby#appium-gui)桌面应用。

## Appium Server配置和使用

以下步骤以Mac下的Appium GUI为例（Windows下的Appium GUI使用可以参考[官网文档](http://appium.io/slate/en/master/?ruby#a-windows-gui-for-appium)）：

* 打开Appium，点击Doctor按钮。可以检测上面安装依赖项是否成功安装

<img style="clear:both;display:block;margin:auto;width:500px;height:100px" src="http://ww4.sinaimg.cn/mw690/6bdb10c1gw1eq9qfkeaehj20i403mdgv.jpg" alt="" />

* 然后点击Android图标的配置，选择你要测试的Apk包。一旦选择好APK包，这里的Package和Launch Activity直接会在下拉框显示出来，个人觉得这是Appium框架的非常大的优点，无需APK源码，减少与开发人员的沟通成本。

<img style="clear:both;display:block;margin:auto;width:500px;height:530px" src="http://ww2.sinaimg.cn/mw690/6bdb10c1gw1eq9qmsh1qrj20hc0juwh7.jpg" alt="" />

* 然后配置Advanced中的SDK路径和签名keystore信息（其实可以不配置签名这一项也可以测试APK包，但是签名项验证测试也还是非常重要的）。

<img style="clear:both;display:block;margin:auto;width:500px;height:250px" src="http://ww2.sinaimg.cn/mw690/6bdb10c1gw1eq9qquze6oj20h908vgmn.jpg" alt="" />

其他设置可以暂时都默认，然后直接运行Launch。运行的相关信息和错误日志都会直接显示在这里：

<img style="clear:both;display:block;margin:auto;width:500px;height:365px" src="http://ww1.sinaimg.cn/mw690/6bdb10c1gw1eq9quz8fmaj20ii0ek42g.jpg" alt="" />

到这一步为止Appium Server已经成功启动了。

## Appium Client的配置

Appium Client的安装可以用Maven来构建：

* Maven配置代码：

<!--code-->
	<dependency>
	    <groupId>io.appium</groupId>
	    <artifactId>java-client</artifactId>
	    <version>2.1.0</version>
	</dependency>

* 或者直接下载[jar](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22io.appium%22%20AND%20a%3A%22java-client%22)包，添加到测试项目中。

## 利用UiAutomatorviewer来获取控件的信息
编写测试用例需要模拟各种按键点击、滚动、输入文字等信息，前面已经提到使用Appium的测试框架可以脱离源代码，那么是如何获取Apk上的控件信息呢？这里介绍UiAutomatorviewer这个Android SDK自带的工具。

1. 如果Android SDK下的tools路径有添加到环境变量，直接可以在命令行输入：

<!--code-->
	$ uiautomatorviewer
	
没有添加环境变量，直接在SDK目录tools/下面有个uiautomatorviewer，双击打开。

2. 把要测试的Apk安装到模拟器或者手机设备中，如果是手机设备用USB连接到PC。

3. 然后使用uiautomatorviewer查看控件信息，用我自己的Demo为例：

<img style="clear:both;display:block;margin:auto;width:500px;height:340px" src="http://7xi85h.com1.z0.glb.clouddn.com/uiauto_guide.gif" alt="" />

从右下控件属性框可以看到控件的任何属性。

