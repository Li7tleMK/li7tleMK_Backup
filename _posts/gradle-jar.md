title: "使用gradle打包jar"
date: 2015-04-15
comments: true	
categories:
  - Android相关
tags: 
  - gradle
  
---

使用eclipse把Library打包成jar很简单，菜单中export选择需要打包的项目，直接下一步就可以了。

但是Android Studio使用的是gradle自动化构建工具，相比eclipse稍微有点麻烦。
我目前更新了Android Studio 1.1，gradle版本是1.1，gradle在更新到1.0以后，gradle的部分语法有变化。

<!--more-->

##打包一个普通的Java Library
如果你的Library中没有引用到Android相关的库，那么就是一个普通的Java Library：

1. 新建一个Module，选择 `Java Library`，给Module个命名，直接下一步即可。
<img style="clear:both;display:block;margin:auto;width:600px;height:360px" src="http://7xi85h.com1.z0.glb.clouddn.com/1.png" alt="" />

2. 新建好以后已经可以在Projects下看到了（注意有个咖啡的Logo），

<img style="clear:both;display:block;margin:auto;width:150px;height:25px" src="http://7xi85h.com1.z0.glb.clouddn.com/2.png" alt="" />
然后打开IDE最右边的Gradle标签，
<img style="clear:both;display:block;margin:auto;width:320px;height:300px" src="http://7xi85h.com1.z0.glb.clouddn.com/3.png" alt="" />

3.双击`jar`，就会自动把你的Library打包成jar（第一次打包可能会下载一些依赖）。然后就会在你的library_name/build/libs/下看到library_name.jar

## 打包一个Android Library

1. 修改gradle配置文件：新建好一个Module以后，在Library项目下有个build.gradle文件，打开以后替换和增加一些代码，

<!--code-->
	buildscript {
	    repositories {
	        jcenter()  //Maven仓库地址，如果你下载有些慢，可以把这句代码替换成国内的仓库：maven{ url 'http://maven.oschina.net/content/groups/public/'}
	    }
	    dependencies {
	        classpath 'com.android.tools.build:gradle:1.1.0'  //gradle版本
	    }
	}

	apply plugin: 'com.android.library' //表明是Android Library
	
	android {
	    compileSdkVersion 21
	    buildToolsVersion '21.1.1'
	}

2. 这时候你会发现你的Library项目的图片已经变成了柱形图（还是4本书？），
<img style="clear:both;display:block;margin:auto;width:150px;height:25px" src="http://7xi85h.com1.z0.glb.clouddn.com/4.png" alt="" />
如果你再去根据上面第3步方式去生成jar，这时你已经找不到jar这个task选项了。其中一个办法就是你可以gradle命令行执行，在你的Library项目目录下执行`gradle build`命令（确认gradle已经添加到环境变量）。如果成功执行在你的build/intermediates/classes/release/下已经生成了.class文件
3. 把.class文件打包成jar：在命令行下执行jar cvf CommonUtils.jar -C build/intermediates/classes/release/ .

最后你就会看到CommonUtils.jar已经在生成在你的Library项目下了。

