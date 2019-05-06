---
title:  Android_Activity_3-Intent和数据传递
date:  2018-04-1 16:25:25
tags: [android,Activity]
categories: 张永枫
description: 本文是以Android Studio为开发工具，<<第一行代码Anroid第2版>> 为学习指导书籍的学习记录
---

<!-- TOC -->

- [1、写在前面](#1写在前面)
- [2、介绍](#2介绍)
- [3、使用显示intent](#3使用显示intent)
- [4、使用隐式Intent](#4使用隐式intent)
- [5、更多隐式Intent用法](#5更多隐式intent用法)
- [7、返回数据给上一个活动](#7返回数据给上一个活动)

<!-- /TOC -->

## 1、写在前面

本文是以Android Studio为开发工具，
<<第一行代码Anroid第2版>> 为学习指导书籍
> [电子书pdf百度云下载地址:](https://pan.baidu.com/s/1GP4sv4NLIvTo8gECTkOxQg) 
密码:rx3g
[Android Studio运行的测试代码下载地址:](https://zhangyongfeng1.github.io/dowland/MyApplication1.zip)


## 2、介绍
功能：从启动器的主活动进入其他的活动,

Inten 分为显示Intent 和隐式 Intent

Intent 是android 程序中各组件的交互方式，

1、可以指明当前组件想要执行的动作
2、要不同组件之间传递数据
3、可被用于启动活动、启动服务，以及发送广播等（下面以启动活动为例）


## 3、使用显示intent

1、新建一个activity
```
新建一个空的活动Activity,命名SecondActivity,并勾选Generate Layout File,

自动创建布局文件，给布局文件命名second_layout

```
2、 编辑second_layout.xml,使用linearLayout,改成如下内容：
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <Button
        android:id="@+id/button_3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button 3"
        />
</LinearLayout>
```
3、 在页面定义一个Button 3按钮

4、查看 AndroidMainifest.xml 中活动的注册情况，Android Studio 会自动完成

5、启动第二个活动
```
Intent 有多个构造函数的重载
其中Intent(Context packageContext, Class<?>cls )
第一个参数Context 要求提供一个启动活动的上下文
第二个参数class 则是指定想要启动的目标活动
Activity类 中有个启动活动的方法，这个方法接收一个Intent 参数。
6、点击一个按钮，跳转到下一个活动页面
```
代码如下：
```
Button button3  = (Button) findViewById(R.id.button_3);
button3.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivity(intent);
    }
});
```
## 4、使用隐式Intent

不明确指出想要启动那个活动
指定一系列抽象的action、category 信息
交由系统去分析这个Intent.找出合适的活动去启动

运行隐式Intent示例：
1、为SecondActivity活动指定action /category
```
<activity android:name=".SecondActivity">
    <intent-filter>
        <action android:name="com.example.activitytext.ACTION_START"/>
        <category android:name="android.intent.category.DEFAULT"/>
    </intent-filter>
</activity>
```
action： 表示当前活动可以响应com.example.activitytext.ACTION_START 这个action
category： 包括一些附加信息

2、在first_layout.xml添加一个按钮
```
<Button
    android:id="@+id/button_4"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="用隐式intent跳转到下一个活动页面"
    />
```
3、在MainActivity.java 添加按钮对应监听方法
```
Button button4  = (Button) findViewById(R.id.button_4);
button4.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        Intent intent = new Intent("android.intent.action.ACTION_START");
        startActivity(intent);
    }
});
```
4、运行代码
category 这里是用的默认有name，所以可以不用指category 就能启动

注：一个intent 可以指定多个category

运行指定多个category示例：
1、修改AndroidMainfest.xml文件
```
<activity android:name=".SecondActivity">
    <intent-filter>
        <action android:name="android.intent.action.ACTION_START"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <category android:name="android.intent.category.MY_CATEGORY"/>
    </intent-filter>
</activity>
```
2.修改MainActivity.java文件
```
Button button4  = (Button) findViewById(R.id.button_4);
button4.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        Intent intent = new Intent("android.intent.action.ACTION_START");
        intent.addCategory("android.intent.category.MY_CATEGORY");
        startActivity(intent);
    }
});
```

## 5、更多隐式Intent用法
 ```
使用隐式intent，不仅可以启动自已的程序内活动，还可以启动其他程序的活动，这使行Adnroid多个应用程序之间功能共享成功了可能，
```
示例：
在应用程中展示一个网页，调用系统浏览器来打开网页
1、新添加一个按钮
```
<Button
    android:id="@+id/button_5"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="用隐式intent调用系统浏览器来打开网页"
    />
```
2、添加这个按钮的监听事件
```
Button button5  = (Button) findViewById(R.id.button_5);
button5.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("http://www.baidu.com"));
        startActivity(intent);
    }
});
```
> 可以通过在注册表中组给活动的<date>标签 添加android:scheme 数据协议为http 协议 这样ThridActivity 就可以响应一个网页。？

示例：
添加一个按钮，跳转调用系统打电话的页面
1、在layout文件中添加一个按钮
```
<Button
    android:id="@+id/button_6"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="用隐式intent调用系统打电话功能"
    />
```
2、在java中添加响应事件
```
Button button6  = (Button) findViewById(R.id.button_6);
button6.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        Intent intent = new Intent(Intent.ACTION_DIAL);
        //Intent.ACTION_DIAL为 android 的内置活动
        intent.setData(Uri.parse("tel:10086"));
        startActivity(intent);
    }
});
```

## 6、向下一个活动传递数据
 > 启动活动数据传递思路
运用Intent 中putExtra()方法的重载，可以将数据暂存在Intent中，启动另一个活动后，只需要把这些数据再从Intent 中取出就可以了。

示例：
在MainActivity 中的一个字符串，想把这个字符串传递到SecondActivity 中去
1、MainActivityk中修改代码如下：
 ````
Button button3  = (Button) findViewById(R.id.button_3);
button3.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        //设置一个变量
        String data = "Hello SecondActivity";
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        intent.putExtra("data_name ",data);
        startActivity(intent);
    }
});
```
2、在第二个活动中将数据取出并打印出来；

```
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.second_layout);
    Intent intent = getIntent();
    String data1 = intent.getStringExtra("data_name");
    Log.d("SecondActivity", data1);
}
```

## 7、返回数据给上一个活动

> Activity 还有一个startActivtyForResult() 也用于启动活动的方法，在活动销毁的时候返回一个结果给上一个活动
startActivityForResult()方法接收两个参数
第一个参数是：Intent 
第二个参数是：请求码

1、在MainActivity活动中设定一个监听跳到secondActivity
```
 Button button3  = (Button) findViewById(R.id.button_3);
        button3.setOnClickListener(new View.OnClickListener(){
            public void onClick(View v){
                //设置一个变量
                String data = "Hello SecondActivity";
                Intent intent = new Intent(MainActivity.this,SecondActivity.class);
                intent.putExtra("data_name11", data);
//                 startActivity(intent);
                startActivityForResult(intent,1);
                //用startActivityForResult，启动secondActivity活动，在活动销毁的时候返回一个结果给上一个活动
            }
        });
```
2、在secondActivity，新增一个按钮，并定义一个监听的方法
```
<Button
    android:id="@+id/button_2"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="返回上一页面，并返回第二个页面的参数"
    />
```
```
//      点击返回上一个活动页面，并返回数据
        Button button2 = (Button)  findViewById(R.id.button_2);
        button2.setOnClickListener(new View.OnClickListener(){
            public void onClick(View v){
            Intent intent = new Intent();
            intent.putExtra("date_return","Hello fristActivity");
            setResult(RESULT_OK,intent);

            String data2 = intent.getStringExtra("date_return");
            Log.i("SecondActivity_back", data2);

            finish();
            }
        });
```
3、在MainActivity，重写onActivityResult（）方法，接收secondActivity返回的参数
```
//重写方法，secondActivity 活动关闭后会调用
protected void onActivityResult(int requestCode,int resultCode,Intent data){
    switch (requestCode){
        case 1:
            if (resultCode == RESULT_OK){
                String returnedData = data.getStringExtra("date_return");
                Log.i("MainActivity",returnedData);
            }
            break;
        default:
    }
}
```

设置back()返回事件

> 重写onBackPressed()

 ```
//重写返回的方法
public void onBackPressed(){
    Intent intent = new Intent();
    intent.putExtra("data_return","Hello back FirstActivity");
    setResult(RESULT_OK,intent);
    finish();
}
```












