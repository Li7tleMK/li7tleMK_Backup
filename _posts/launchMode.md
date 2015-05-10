title: "launchMode详细理解"
date: 2015-05-01
comments: true	
categories:
  - Android基础
tags:
  - Android
  
---
###standard
这种模式下的Activity可以被多次实例化，即在同一个Task上可以用多个Activity实例。如当前A已经启动，再运行如下代码：

		startActivity(new Intent(this,A.class));

目前栈中的状态是A->A。

<!--more-->

###singleTop
当前示例如果在栈顶，就不会新建实例，而是重用原来的实例并调用其OnNewIntent。如：

		startActivity(new Intent(this, A.class));

启动A时不会创建新的实例。
但是如果这个A不在栈顶而是在其他Task中，那么他的行为和standard是一样的，即：创建新的实例。

### singleTask
google文档原文：

> The system creates the activity at the root of a new task and routes the intent to it. However, if an instance of the activity already exists, the system routes the intent to existing instance through a call to its onNewIntent() method, rather than creating a new one.

简单的来说有2点：

1. 当系统第一次启动这个Activity时（之前系统不存在这个Activity），系统便会把这个Activity实例放入新创建Task栈的底部。
2. 如果这个Activity的实例已经存在，就会调用这个Activity的OnNewIntent成员方法而不是新建一个Activity实例。

如果要满足第1点需要有点前提：在新建Activity实例的时候系统会去检查taskAffinity这个属性，如果系统中已经存在这个属性的Task（比如Activity的taskAffinity:“me.bo1.launcher”，系统中有个Task也是”me.bo1.launcher”），那么系统不会新建一个Task，而是在已存在的Task中启动。
关于第2点，如果taskAffinity相同的Task已经存在，那么也会有2种情况：
	1. 在这个Task中已经有Activity实例，那么直接启动并且把位于这个Activity上面的其他Activity全部移除，即最终这个Activity实例会位于Tas栈顶端中。
	2. 如果在这个Task中不存在，那么会直接新建taskAffinity:“me.bo1.launcher”的Task，并新建Activity放入到这个Task中。

### singleInstance
和singleTask有点类似，会新建一个Task，但是该Task中只有这个Activity唯一一个实例。不会出现singleTask的第二种情况。

