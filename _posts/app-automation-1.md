title: "移动App自动化测试（一）"
date: 2015-03-12
comments: true
categories:
  - 自动化测试
tags: 
  - 移动App自动化测试
  
---

## 移动App自动化测试简介
目前移动App的自动化测试框架比较多，比如：Robotium、Expresso等，很多大公司甚至都会有自己的一套自动化测试框架。这篇文章简单Android自动化测试框架，iOS自动化测试框架也会少量提到。

1. Monkey是Android SDK自带的测试工具，在测试过程中会向系统发送伪随机的用户事件流，如按键输入、触摸屏输入、手势输入等)，实现对正在开发的应用程序进行压力测试，也有日志输出。实际上该工具只能对程序做一些压力测试，由于测试事件和数据都是随机的，不能自定义，所以有很大的局限性。<!--more-->

2. MonkeyRunner也是Android SDK提供的测试工具。严格意义上来说MonkeyRunner其实是一个Api工具包，比Monkey强大，可以编写测试脚本来自定义数据、事件。缺点是脚本用Python来写，对测试人员来说要求较高，有比较大的学习成本。

3. Instrumentation是早期Google提供的Android自动化测试工具类，虽然在那时候JUnit也可以对Android进行测试，但是Instrumentation允许你对应用程序做更为复杂的测试，甚至是框架层面的。通过Instrumentation你可以模拟按键按下、抬起、屏幕点击、滚动等事件。Instrumentation是通过将主程序和测试程序运行在同一个进程来实现这些功能，你可以把Instrumentation看成一个类似Activity或者Service并且不带界面的组件，在程序运行期间监控你的主程序。缺点是对测试人员来说编写代码能力要求较高，需要对Android相关知识有一定了解，还需要配置AndroidManifest.xml文件，不能跨多个App。

4. UiAutomator也是Android提供的自动化测试框架，基本上支持所有的Android事件操作，对比Instrumentation它不需要测试人员了解代码实现细节（可以用UiAutomatorviewer抓去App页面上的控件属性而不看源码）。基于Java，测试代码结构简单、编写容易、学习成本，一次编译，所有设备或模拟器都能运行测试，能跨App（比如：很多App有选择相册、打开相机拍照，这就是跨App测试）。缺点是只支持SDK 16（Android 4.1）及以上，不支持Hybird App、WebApp。

5. Espresso是Google的开源自动化测试框架。相对于Robotium和UIAutomator，它的特点是规模更小、更简洁，API更加精确，编写测试代码简单，容易快速上手。因为是基于Instrumentation的，所以不能跨App。[配合Android Studio来编写测试的简单例子](https://medium.com/@marta/ui-tests-with-espresso-android-studio-c476d3b5ba45)

6. Selendroid：也是基于Instrumentation的测试框架，可以测试Native App、Hybird App、Web App，但是网上资料较少，社区活跃度也不大。

7. Robotium也是基于Instrumentation的测试框架，目前国内外用的比较多，资料比较多，社区也比较活跃。缺点是对测试人员来说要有一定的Java基础，了解Android基本组件，不能跨App。

8. Athrun是淘宝出的一个移动测试框架/平台，同时支持iOS和Android。Android部分也是基于Instrumentation，在Android原有的ActivityInstrumentationTestCase2类基础上进行了扩展，提供一整套面向对象的API。[这里](http://code.taobao.org/p/athrun/wiki/index/)有详细介绍。

9. UIAutomation是iOS平台下的测试框架，目前用的比较多的框架。

10. Appium是最近比较热门的框架，社区也很活跃。后一章我会重点介绍这个自动化测试框架。

## 目前常用移动自动化测试框架的综合对比

||**UiAutomator**|**Espresso**|**Robotium**|**Selendroid**|**Athrun**|**Appium**|
| :--: |:------:|:------:|:------:|:------:|:------:|:------:|
|**支持Andorid**|Yes|Yes|Yes|Yes|Yes|Yes|
|**支持iOS**|No|No|No|No|Yes|Yes|
|**Web App**|No|No|Yes(4.0以上)|Yes|Yes|Yes|
|**测试脚本语言**|Java|Java|Java|Java|Java|Almost Any|
|**Android SDK**|大于16|8,10,15-19|All|All|All|All|
|**社区/资料**|一般/多|一般/一般|活跃/多|一般/一般|很少/较少|活跃/较多|


