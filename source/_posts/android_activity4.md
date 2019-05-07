---
title:  Android_Activity_4-活动的生命周期探究
date:  2018-04-10 16:25:25
tags: [android,Activity]
categories: 张永枫
description: 本文是以Android Studi为开发工具，<<第一行代码Anroid第2版>> 为学习指导书籍的学习记录
---
1、介绍

Android的活动是可以层叠的，我们每启动一个新的活动，就会覆盖有原活动之上，点击Back键之后会销毁最上面的活动，下面的一个活动就会重新显示出来。
2、 返回栈

Android使用（Task）来管理活动；
一个任务就是一组存放在栈里的的活动集合，这个栈也称之为返回栈（back Stack）;
栈是一种先进先出的数据结构；
工作流程：
    在默认情况下，
    每当启动了一个新的活动，它会在返回栈中入栈，并处于栈顶的位置，
    每当我们按下Back键或调用finish()方法去销毁一个活动时，处于栈顶的位置的活动就会出栈，这时前一个入栈的活动就会重新处于栈顶的位置，系统就会是显示处于栈顶的活动给用。
3、活动状态（每个活动其生命周期最多可能会有4种状态）

3.1、运行状态

当一个活动位于返回栈的栈顶时，活动就处于运行状态。
3.2、暂停状态

当一个活动不再处于栈顶位置，但仍然可见时，活动就进入了暂停状态。
示例：并不是每一个活动都会占满整个屏幕，比如对话框形式的活动就只会占用屏幕中间的部分区域，你仍然可以看到后面的活动；
处于暂停状态的活动仍然是完全存活着的；
只有在内存极低的情况下才会考虑回收这种活动；
3.3、停止状态

当一个活动不再处于栈顶位置，并且完成不可见的时候，就进入了停止状态。系统会为这种活动保存相应的状态和成员变量（但是当其他地方需要内存时，处于停止活动下的活动有可能会被系统回收。）
3.4、销毁状态

当一个活动从返回栈中移除后变成了销毁状态。系统会倾向回收这种状态的活动，以保证手机内存的充足。
4、活动的生存期

Activity中定义了7个回调方法，覆盖了生命周期的每一个环节；
onCreate()

每个活动基本都会重写这个方法，它会在活动第一次创建的时候调用；这个方法会完成活动的初始化操作，比如:加载布局、绑定事件；
onStart()

这个方法在活动由不可见变为可见的时候调用；
onResume()

这个方法在活动准备好和用户进行交互的时候调用，此时的活动一定位于返回栈的栈顶，并且处于运行状态；
onPause()

这个方法在系统准备去启动或者恢复另一个活动的时候调用；
（通常会在这个方法中将一）
onStop()

这个方法在活动完全不可见的时候调用；
onDestroy()

在活动被销毁之前调用，之后活动的状态变为销毁状态；
onRestart()

这个方法在活动由停止状态变为运行状态之前调用，就是活动被重新启动的时候调用；
5、体验活动的生命周期

准备工作
*  新建一个项目，允许自动创建活动和布局，并设置主活动；
*  再分别创建两人子活动NormalActivity(布局命名：normal_layout)和DialogActivity(布局命名：dialog_layout)；
*  normal_layout.xml 修改成内容如下：
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="this is a mormal activity"
        />

</LinearLayout>
```
*  dialog_layout.xml 修改成内容如下：
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              >
    <TextView
        android:layout_height="match_parent"
        android:layout_width="wrap_content"
        android:text="This is a dialog activity"
        />
</LinearLayout>
```
修改注册表AndroidManifest.xml如下：
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.bignerdranch.android.activity_text">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        <activity android:name=".NormalActivity">
        </activity>
        <activity android:name=".DialoActivity"
            android:theme="@andrid:style/Theme.Dialog">
        </activity>
    </application>

</manifest>
```
添加两个按钮，一个用于启动活动NormalActivity，一个用于启动DialogActivity
主活动的布局如下:
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <Button
        android:id="@+id/start_normal_activity"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Start normal activity"/>

    <Button
        android:id="@+id/start_dialog_activity"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Start dialog activity"
        />
</LinearLayout>
```
活动修改代码如下:
```
import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    public static final String TAG = "MainActivity";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        Log.w(TAG,"onCreate");
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button startNormalActivity = (Button) findViewById(R.id.start_normal_activity);
        Button startDialogActivity = (Button) findViewById(R.id.start_dialog_activity);

        //设置按钮的签听事件
        startNormalActivity.setOnClickListener(new View.OnClickListener(){
            public void onClick(View v){
                Intent intent = new Intent(MainActivity.this,NormalActivity.class);
                startActivity(intent);
            }
        });

        //设置按钮的签听事件
        startDialogActivity.setOnClickListener(new View.OnClickListener(){
            public void onClick(View v){
                Intent intent = new Intent(MainActivity.this,DialoActivity.class);
                startActivity(intent);
            }
        });

        }
    protected void onStart(){
        super.onStart();
        Log.w(TAG,"onStart");
    }

    protected  void onResume(){
        super.onResume();
        Log.w(TAG,"Onresume");
    }

    protected  void onPause(){
        super.onPause();
        Log.w(TAG,"onpause");
    }

    protected  void onStop(){
        super.onStop();
        Log.w(TAG,"onstop");
    }

    protected void onDestroy(){
        super.onDestroy();
        Log.w(TAG,"onDestroy");
    }

    protected void onRestart(){
        super.onRestart();
        Log.w(TAG,"onRestart");
    }
}
```
进入时打印如下：
```
04-10 01:18:06.875 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动第一次创建的时候调用>> onCreate
04-10 01:18:06.908 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动由不可见变为可见的时候调用>> onStart
04-10 01:18:06.911 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动准备好和用户进行交互的时候调用>> Onresume
```
点击START NOTMAL ACTIVITY 按钮时会打印 如下：
```
04-10 01:18:27.265 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 系统准备去启动或者恢复另一个活动的时候调用>> onpause
04-10 01:18:27.589 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动完全不可见的时候调用>> onstop
```
再点击返回主活动页面时打印 如下：
```
04-10 01:18:46.132 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动由停止状态变为运行状态之前调用>> onRestart
04-10 01:18:46.133 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动由不可见变为可见的时候调用>> onStart
04-10 01:18:46.134 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动准备好和用户进行交互的时候调用>> Onresume
```
点击Start dialog activity 按钮进打印如下：
```
04-10 17:22:18.739 3798-3798/com.bignerdranch.android.activity_text W/MainActivity: 系统准备去启动或者恢复另一个活动的时候调用>> onpause
```
再点击返回主活动页面时打印 如下：
```
04-10 17:22:46.798 3798-3798/com.bignerdranch.android.activity_text W/MainActivity: 活动准备好和用户进行交互的时候调用>> Onresume
```
再点击返回退出app时打印
```
04-10 01:20:35.510 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 系统准备去启动或者恢复另一个活动的时候调用>> onpause
04-10 01:20:36.031 21015-21015/com.bignerdranch.android.activity_text W/MainActivity: 活动完全不可见的时候调用>> onstop
    活动被销毁之前调用>> onDestroy
```
遇到的问题
在运行过程中点击Start dialog activity 按钮弹出框的时候，会发生闪退
分析出原因为类继承的问题，修改方法如下；
修改DialoActivity.class中DialoActivity为继承Activity类，代码如下：
```
package com.bignerdranch.android.activity_text;

import android.app.Activity;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class DialoActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.dialog_layout);
    }
}
```