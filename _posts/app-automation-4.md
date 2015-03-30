title: "移动App自动化测试（四）"
date: 2015-03-18
comments: true
categories:
  - 自动化测试
tags:
  - 移动App自动化测试
  
---

我用Java写了3个测试脚本，分别测试Native App、Hybird App、Web App。用TestNG单元测试框架。

## 测试Native App
一个TestNG测试脚本需要3个必要的部分：
* 1个setup()，用于测试前初始化工作：
<!--more-->

<!--code-->
	@BeforeClass
	public void setup() throws Exception {
		//你要测试的APK
		File appDir = new File("Apk");
		File app = new File(appDir, "Kuozhiv2.apk"); 
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "");
		//测试平台
		capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME,"Android"); 
		capabilities.setCapability(MobileCapabilityType.DEVICE_NAME,"Google_Nexus_4"); 
		//Android版本
		capabilities.setCapability(MobileCapabilityType.PLATFORM_VERSION, "4.4");
		//Package name
		capabilities.setCapability(MobileCapabilityType.APP_PACKAGE,"com.edusoho.kuozhi");
		//Launch Activity
		capabilities.setCapability(MobileCapabilityType.APP_ACTIVITY,".KuozhiActivity");
		capabilities.setCapability(MobileCapabilityType.APP,app.getAbsolutePath());
		driver = new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"),capabilities);
		driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
		System.out.print("App is launched!");
	}

* 1个tearDown()，用于测试完毕清理工作：

<!--code-->
	@AfterClass
	public void tearDown() throws Exception {
		driver.quit();
	}


* 至少1个test()测试用例：

<!--code-->
	@Test
	public void splashTest() throws Exception {

		Thread.sleep(2000);
		int Y = driver.manage().window().getSize().getHeight();
		int X = driver.manage().window().getSize().getWidth();

		int sX = (int) (X * 0.8);
		int sY = (int) (Y * 0.5);
		int eX = (int) (X * 0.2);
		int eY = sY;
		int duration = 600;

		//第一个模拟滑动
		driver.swipe(sX, sY, eX, eY, duration);
		//第二个模拟滑动
		driver.swipe(sX, sY, eX, eY, duration);

		WebElement enterMainActivityElement = driver.findElement(By
				.id("com.edusoho.kuozhi:id/splash_ok_btn"));
		enterMainActivityElement.click();

		WebElement enterSchoolElement = driver.findElement(By
				.id("com.edusoho.kuozhi:id/qr_other_btn"));
		enterSchoolElement.click();
	}
	
这个测试NativeApp的脚本比较简单：滑动2次Splash，点击进入，登录等事件。**注：抓取控件可以根据ID，如果控件没有ID还可以用XPath**。

测试效果：

<video src="http://7xi85h.com1.z0.glb.clouddn.com/native_test.mp4" style="clear:both;display:block;margin:auto;width:320px;height:533px" controls="controls" >
此浏览器不支持此标签
</video>

## 测试Hybird App
在测试Hybird App的时候，有一点需要注意：
>只有测试设备或者模拟器版本是Android 4.4（API 19）及以上，Appium才能探测到一个Activity中的WebView控件，如果低于Android 4.4（API 19），那么改用Selendroid模式。因为在4.4上WebView是Chromium内核，之前都是Webkit内核。

### 如何定位WebView中页面的元素？
UiAutomatorViewer只能定位Activity中的UI元素，WebView已经是最小单元UI，不能解析WebView中页面元素。这里我使用Chrome DevTools中的inspect来解析WebView中的UI元素。

<img src="http://7xi85h.com1.z0.glb.clouddn.com/chrome_inspect.gif" style="clear:both;display:block;margin:auto;width:620px;height:360px;" alt="图片名称" />

* setup()初始化部分代码：

<!--code-->
	@BeforeClass
	public void setup() throws Exception {
		//other code ...
		//如果你测试的设备的Android版本低于4.4，那么Automation Name要改成"Selendroid"，Appium Server端也要改成"Selendroid"
		capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME,"Appium"); 
		//other code ...
	}
	
* test()测试用例部分代码：

<!--code-->
	@Test
	public void webViewLogin() throws Exception {
		//other code ...
		Set<String> contextNames = driver.getContextHandles();
		for (String contextName : contextNames) {
			System.out.println("--->" + contextName);
			if (contextName.contains("NATIVE_APP")) {
				srtActivityContextString = contextName;
			}
			if (contextName.contains("WEBVIEW")) {
				strWebViewContext = contextName;
			}
		}
		driver.context(strWebViewContext);//把driver切换到WebView的context，再抓取WebView内页面的UI元素
		//other code ...
	}

测试效果：

<video src="http://7xi85h.com1.z0.glb.clouddn.com/hybird_test.mp4" style="clear:both;display:block;margin:auto;width:320px;height:533px"  controls="controls" >
此浏览器不支持此标签
</video>

## 测试Web App
用Appiumku框架测试WebApp的时候有以下几点需要注意：

* 目前Appium的WebApp测试只支持Chrome浏览器。
* Chrome在x86模拟器上除非自己编译，否则是装不上或者存在各种问题的。请用ARM模拟器或真机，或者直接使用selenium测试框架直接对Web进行测试。因为我用的Genymotion模拟器，是x86的，所以发现了这个坑。可以在[官网文档](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/mobile-web.md)看到这个说明。

* setup()测试初始化之前，需要指定浏览器名称，如下代码：

<!--code-->
	@BeforeClass
	public void setup() throws Exception {
		//other code ...
		capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "chrome");
		//other code ...
	}

* driver需要指定webview的url，如下代码：

<!--code-->
	@Test
	public void registerTest() throws Exception {
		//other code ...
		driver.get(web_app_url;
	}
	
测试效果：

<video src="http://7xi85h.com1.z0.glb.clouddn.com/webapp_test.mp4" style="clear:both;display:block;margin:auto;width:320px;height:533px" controls="controls" >
此浏览器不支持此标签
</video>





