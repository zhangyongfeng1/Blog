---
title:  Android_Activity_3-活动括展
date: 2018-03-27 15:25:25
tags: [android,Activity]
categories: 张永枫
description: 本文是以Android Studio为开发工具，<<第一行代码Anroid第2版>> 为学习指导书籍的学习记录
---

<!-- TOC -->

- [1、写在前面](#1写在前面)
- [2、在活动中使用Toast（android 友好提醒方式）](#2在活动中使用toastandroid-友好提醒方式)
- [3、在活动中使用Menu(菜单)](#3在活动中使用menu菜单)
- [4、销毁一个活动](#4销毁一个活动)

<!-- /TOC -->

## 1、写在前面

本文是以Android Studio为开发工具，
<<第一行代码Anroid第2版>> 为学习指导书籍
> [电子书pdf百度云下载地址:](https://pan.baidu.com/s/1GP4sv4NLIvTo8gECTkOxQg) 
密码:rx3g
[Android Studio运行的测试代码下载地址:](https://zhangyongfeng1.github.io/dowland/MyApplication1.zip)


## 2、在活动中使用Toast（android 友好提醒方式）

在程序中可以使用它将一些短小的信息通知给用户，这些信息在一段时间后会自动消失。
示例：
需要定义一个弹出Toast的触发点，在一个页面上定义一个按钮，点击这个按钮提示一个Tast


在onCreate()方法中添加如下代码：
```
package com.bignerdranch.android.myapplication1;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
//        setContentView(R.layout.activity_main);
//        日志打印
        setContentView(R.layout.first_layout);//先布局后面才可以签听对象

        Log.v("MainActivity1","zyf_@@@@@@@@@@@@--verbose");
        Log.d("MainActivity2","zyf_@@@@@@@@@@@@--debug");
        Log.i("MainActivity3","zyf_@@@@@@@@@@@@--info");
        Log.w("MainActivity4","zyf_@@@@@@@@@@@@--warn");
        Log.e("MainActivity5","zyf_@@@@@@@@@@@@--error");
        Button button1  = (Button) findViewById(R.id.button_1);
        button1.setOnClickListener(new View.OnClickListener() {
                   public void onClick(View v) {
                       Toast.makeText(MainActivity.this, "you clicked Button 1", Toast.LENGTH_SHORT).show();
                    }
                                   });
    }
}
```

注：要记得引入button 类
1. 在活动中通过调用方法 findViewById()方法获取到布局文件中定义的元素（
示例中我们传入R.id.button_1 （这个值是在layout 文件中通过android:id 来得到）按扭的实例。
2. findViewById()返回的是一个View对象，要向下转型将它转成Button对象
3. 拿到Button对象之后，可以通过调用setOnClickListenter()方法为按钮注册一个监听器。点击按钮之后就会执行监听器中的onClick()方法，在onClick()方法中调用Toast
4. Toast的用法 通过静态方法makeText()创建出一个Toast对象，然后调用show()将Toast 显示出来就可以了
makeText()方法定义中要传入的三个参数
第一个参数是Context,Toast上下文，由于活动本身就是一个Context对象，因此这里直接传入MainActivity.this
就可以了
第二个参数是显示文本的内容
第三个参数是Toast显示的时长，这里内置了两个常量
Toast.LENGTH_SHORT
Toast.LENGTH_LONG

## 3、在活动中使用Menu(菜单)

添加一个菜单
1、在res目录下面新建一个menu文件夹，
2、然后再menu下面再新建一个名收main的菜单文件（右击menu文件—>new —>Menu resourse file）生成一个main.xml文件

输入内容如下：

```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/add_item"
        android:title="Add"/>
    <item
        android:id="@+id/remove_item"
        android:title="Remove"/>
</menu>
```

其中 <item>标签下面 
android:id 表示给这个菜单定义一个唯一的标识符
android:title 表示给这个菜音定一个名称

然后回到主活动MainActivity.java中重写如下方法

```
//重写方法
public boolean onCreateOptionsMenu(Menu menu){
    getMenuInflater().inflate(R.menu.main,menu);
    return true;
}
```


1、通过getMenuInflater()方法能得到MenuInflater 对象，

2、再调用inflate() 方法可以组给当前活动创建菜单，

3、inflate()方法上送两个参数

第一个是指定通过资源文件创建menu菜单 （菜单R地址）

第二个指定要添加的对象（方法传入的menu 对象）

4、onCreateOptionsMenu() 返回true表示显示菜单

再重写方法加入弹框提示

```
//重写方法 弹框提示
public boolean onOptionsItemSelected(MenuItem item){
    switch (item.getItemId()){
        case R.id.add_item:
            Toast.makeText(this,"you clicked add",Toast.LENGTH_SHORT);
            break;
        case R.id.remove_item:
            Toast.makeText(this,"you clicked remove",Toast.LENGTH_SHORT);
            break;
        default:
    }
    return true;
}
```

通过item.getItemId()
来判断点击了那个菜单

## 4、销毁一个活动

一般按一下返加按钮（back）键就可以销毁当前的活动

也可以通过Activity类的 finish()方法调用来销毁当前的活动

