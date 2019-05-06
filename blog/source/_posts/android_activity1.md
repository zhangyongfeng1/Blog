---
title:  Android_Activity_1--活动入门
date: 2018-03-26 16:25:25
tags: [android,Activity]
categories: 张永枫
description: 本文是以Android Studio为开发工具，<<第一行代码Anroid第2版>> 为学习指导书籍的学习记录
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [1、写在前面](#1%E5%86%99%E5%9C%A8%E5%89%8D%E9%9D%A2)
- [2、介绍](#2%E4%BB%8B%E7%BB%8D)
- [3、手动创建活动](#3%E6%89%8B%E5%8A%A8%E5%88%9B%E5%BB%BA%E6%B4%BB%E5%8A%A8)
- [4、创建和加载布局](#4%E5%88%9B%E5%BB%BA%E5%92%8C%E5%8A%A0%E8%BD%BD%E5%B8%83%E5%B1%80)
  - [4.1、 Android 设计原则：](#41-android-%E8%AE%BE%E8%AE%A1%E5%8E%9F%E5%88%99)
  - [4.2、 创建一个布局](#42-%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%B8%83%E5%B1%80)
  - [4.3、 可视化布局编辑器](#43-%E5%8F%AF%E8%A7%86%E5%8C%96%E5%B8%83%E5%B1%80%E7%BC%96%E8%BE%91%E5%99%A8)
  - [4.4、 在布局中添加一个按扭](#44-%E5%9C%A8%E5%B8%83%E5%B1%80%E4%B8%AD%E6%B7%BB%E5%8A%A0%E4%B8%80%E4%B8%AA%E6%8C%89%E6%89%AD)
  - [4.5、 在一个活动（Activity）中加载一个布局(Layout)](#45-%E5%9C%A8%E4%B8%80%E4%B8%AA%E6%B4%BB%E5%8A%A8activity%E4%B8%AD%E5%8A%A0%E8%BD%BD%E4%B8%80%E4%B8%AA%E5%B8%83%E5%B1%80layout)
  - [4.6、 关于R文件](#46-%E5%85%B3%E4%BA%8Er%E6%96%87%E4%BB%B6)
  - [4.7、 在AndroidManifest文件中注册](#47-%E5%9C%A8androidmanifest%E6%96%87%E4%BB%B6%E4%B8%AD%E6%B3%A8%E5%86%8C)
  - [4.8、 设置主活动的方法](#48-%E8%AE%BE%E7%BD%AE%E4%B8%BB%E6%B4%BB%E5%8A%A8%E7%9A%84%E6%96%B9%E6%B3%95)
  - [4.9、 启动器的标题](#49-%E5%90%AF%E5%8A%A8%E5%99%A8%E7%9A%84%E6%A0%87%E9%A2%98)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->



## 1、写在前面

本文是以Android Studio为开发工具，
<<第一行代码Anroid第2版>> 为学习指导书籍
> [电子书pdf百度云下载地址:](https://pan.baidu.com/s/1GP4sv4NLIvTo8gECTkOxQg)
密码:rx3g
[Android Studio运行的测试代码下载地址:](https://zhangyongfeng1.github.io/dowland/MyApplication1.zip)


## 2、介绍

Activity 是一种可以包括界面的组件，主要用于和用户的交互，
一个应用程序可以有0个或多个活动。

## 3、手动创建活动

使项目在Project模式下面，
1. 选中在app/src/main/java/下面的包中右键点击；
2. 再选择New->Activity->Empty Activity 创建一个活动的对话框 会有以下选项：
Generate Layout File 表示会自动为创建的活动生成一个对应的layout布局文件（可不选）；
Launcher Activity 表示会自动将当前创建的活动设置为当前项目的主活动 （有主活动时不选）；
Backwards Compatibility 表示为项目启用向下兼容的模式（这个要选）；
3. 点击finish 之后会自动生成一个java文件（会自动继承AppCompatActivity这个类，并且重写 onCrate()方法）。


## 4、创建和加载布局


### 4.1、 Android 设计原则：

逻辑和视图分离，最好一个活动都能对应一个布局；

（Activity 是处理逻辑用javap实现，layout 负责显示内容用xmL实现）。

### 4.2、 创建一个布局

使项目在Project模式下面：

1. 选中在app/src/main/res/layout目录下面的包中右键点击，

2. 再选择New->Layout resource file 创建一个布局文件

3. 在弹出框有中两个选项：

Flie name : 这个自已命名就可以了

Boot element: 根元素（先默认选择LinerLayout）

4. 点击完成，会自动生成一个xml文件

### 4.3、 可视化布局编辑器

屏幕中央区域显示预览的效果；

最下方有两个切换的选项：

* Design:     显示当前的可视化布局

* Text:    是显示xml文件的内容

### 4.4、 在布局中添加一个按扭

添加的button元素中中添加了几个属性

* android:id (定义一个唯一个标识符）；

* android:layout_width(指定当前的宽度，使用match_parent表示和当前父元素一样宽）；

* android:layout_height(指定当前的高度，使用wrap_content表示适应控件里的内容)；

* android:text(指定元素中显示的内容)；

### 4.5、 在一个活动（Activity）中加载一个布局(Layout)

在onCreate()方法中添加
```
setContentView(R.layout.frist_layout);
```

### 4.6、 关于R文件


项目中任何添加任何资源都会在R文件中生成一个相应的资源id

(因此可以直接使用setContentView()方法加载R.layout.frist_layout)


### 4.7、 在AndroidManifest文件中注册

所有的活动activity,要在AndroidMainifest.xml中进行注册才会生效；

AndroidMainifest.xml文件在项目中的位app/src/main/AndroidManifest.xml；

<activity>标签中使用android:name来表示指定具体注册那个活动；

注：不过要是只有一个活动，而没有配置主活动的话，代码在android studio 中是跑不起来的，会抛弃出一串异常的代码
```
org.gradle.api.tasks.TaskExecutionException: Execution failed for task …

```
### 4.8、 设置主活动的方法


在<activity>标签内部加入<intent-filter>标签，并在标签中添加

```
<action android:name=“android.intent.action.MAIN”/>
```
和
```
<category android:name=“android.intent.category.LAUNCHER”/>
```
这两名声明即可。


### 4.9、 启动器的标题


除此之外如果给主活动指定一个label的话，你会发现标题栏中的内容也变成了启动器中的应用程序显示的名称。

如果应用程序没有声明任何一个活动作为主活动，这个程序仍然可以正常安装，可是你无法在启动器中看到或者打开这个程序，这类程序一般都是作为第三方服务供其他应用内部调用，如支付宝快捷支付服务。
