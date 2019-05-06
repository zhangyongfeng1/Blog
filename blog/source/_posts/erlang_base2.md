
---
title: erlang-基本语法_2、模块和函数、内置函数、在erlang shell中运行文件
date:  2018-06-12 14:27:25
tags: [erlang]
categories: 张永枫
description:
---
<!-- TOC -->

- [写在前面](#写在前面)
- [模块和函数](#模块和函数)
- [内建函数 BIF](#内建函数-bif)
- [erlang shell中运行文件中的方法](#erlang-shell中运行文件中的方法)
- [写在后面](#写在后面)

<!-- /TOC -->

## 写在前面
本文主要是以一个erlang的学习记录，有错误的地方欢迎指正。

![本人的erlang学习脑图](https://upload-images.jianshu.io/upload_images/6841945-a92401e828dbb1fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 模块和函数
1、Erlang 里代码是用 Module 组织的。一个 Module 包含了一组功能相近的函数。用一个函数的时候，要这么调用：Module:Function(arg1, arg2)。
或者你先 import 某个 Module 里的函数，然后用省略Module名的方式调用：Function(arg1, arg2)。
2、Module 可也提供代码管理的作用，加载一个 Module 到 Erlang VM就加载了那个 Module 里的所有代码，然后你想热更新代码的话，直接更新这个 Module 就行了。
**示例1：** 实现将数值翻倍
以一个目录下面新建一个文件名为tut.erl,输入以下代码

```
-module(tut).
-export([double/1]).

double(X)->
X *2.
```

在命令窗口输入以下代码

```
➜  erlang pwd
/Users/Macx/Public/erlang
➜  erlang c(tut). %要在不是erlang shell下才能去执行c(tut).编译文件会报错
zsh: no matches found: c(tut).
➜  erlang erl  %要在erlang shell下才能去执行c(tut).编译文件
Erlang R15B03 (erts-5.9.3.1) [source] [64-bit] [smp:8:8] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.9.3.1  (abort with ^G)
1> c(tut).
{ok,tut}
2> tut:double(3).
%编译完成之后，可以用module:function 来调用方法
6
3> 
```
**示例2：**计算一个数的阶乘，如：4的阶乘为 4 * 3 * 2 * 2 = 24
新建一个tut1.erl文件，代码如下：

```
-module(tut1).
-export([fac/1]).


fac(1) ->
1;
%以分号结束的，这也就表示后面还有 fac 函数的更多内容

fac(N) ->
N * fac(N -1).
%N 的阶乘为 N 乘以 N-1 的阶乘
```
在命令行中输入如下；

```
➜  erlang erl
Erlang R15B03 (erts-5.9.3.1) [source] [64-bit] [smp:8:8] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.9.3.1  (abort with ^G)
1> c(tut1).
{ok,tut1}
2> 
2> 
2> tut1:fac(4).****
24
```

**对tut1.erl进行扩展**
（Erlang 函数也可以有多个参数，实现一个函数完成两个数相乘）
修改tut1.erl如下：

```
-module(tut1).
-export([fac/1,mult/2]).


fac(1) ->
1;

fac(N) ->
N * fac(N -1).


mult(X,Y) ->
X * Y.
```
在命令窗口输入如下：

```
➜  erlang erl
Erlang R15B03 (erts-5.9.3.1) [source] [64-bit] [smp:8:8] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.9.3.1  (abort with ^G)
1> c(tut1).
{ok,tut1}
2> tut1:m
module_info/0  module_info/1  mult/2         
2> tut1:mult(2,3).
6
3> 
```

## 内建函数 BIF
erlang module 里的函数叫做 BIF.（内建函数）

示例：erlang 自带的Module（BIP）

```
45> erlang:element(2,{a,b,c}).
b
46> element(2,{a,b,c}).
b

48> lists:seq(1,4).
[1,2,3,4]
49> seq(1,4).
** exception error: undefined shell command seq/2
50> %上面的例子里，你能直接用 erlang Module 里的 element/2 函数，是因为 erlang 里的常用函数会被 潜在的 import 过来。其他的 Module 比如 lists 不会.
```

内置函数示例：

```
Erlang R15B03 (erts-5.9.3.1) [source] [64-bit] [smp:8:8] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.9.3.1  (abort with ^G)
1> trunc(5.6).
%就近取整
5
2> round(5.6).
%四舍五入
6
3> length([1,2,3,4]).
%列表长度
4
4> float(5).
%浮点数
5.0
5> is_atom(hello).
%是否为原子
true
6> is_atom("hello").
false
7> is_tuple({pairs,{c,30}}).
%是否为元组
true
8> is_tuple([pairs,{c,30}]).
false
9> 
10> atom_to_list(hello).
%原子转为字符串
"hello"
11> list_to_atom("goodbay").
%字符串转为原子
goodbay
12> integer_to_list(22).
%整型转为列表
"22"
```


## erlang shell中运行文件中的方法
1、Erlang Shell 是一个快速尝试新想法的地方，但我们真正的代码是要写到文件里，然后参与编译的。

在一个目录（我这边为/Users/Macx/Public/erlang这个目录）下面新建一个text.erl的文件
在文件的第一行, 用 -module(text) 来声明你的 module name。注意跟 java 类似，module 名要跟文件名一样。
然后你在你的 module 里写你的函数,text.erl代码如下：

```
-module(text).
-export([add/2,add/3]).
%% export 是导出语法，指定导出 add/2, add/3 函数。没导出的函数在 Module 外是无法访问的。

add(A,B) ->
A + B.

add(A,B,C) ->
A + B + C.
```
在 shell中的操作如下:

```
➜  erlang pwd 
%查看当前的目录路径；
/Users/Macx/Public/erlang
➜  erlang ll    
%查看当前的目录路径下的文件；
-rw-r--r--@ 1 Macx  staff     0B  6 12 10:39 text.erl
➜  erlang mkdir -p ./ebin  
%在当前路径下建一个ebin的文件目录
➜  erlang erlc -o ebin text.erl 
%用erlc编译文件，并把文件放到ebin下面
➜  erlang ll ebin  %查看ebin 下面是否有文件
total 8
-rw-r--r--  1 Macx  staff   580B  6 12 10:42 text.beam
➜  erlang erl -pa ./ebin 
%erl -pa 参数的意思是 Path Add, 添加目录到 erlang 的 beam 文件查找目录列表里。
Erlang R15B03 (erts-5.9.3.1) [source] [64-bit] [smp:8:8] [async-threads:0] [hipe] [kernel-poll:false]

Eshell V5.9.3.1  (abort with ^G)
1> pwd
1> .
pwd
2> text(1,4).
%%直接调用方法会报错找不到方法
** exception error: undefined shell command text/2
3> text:add(1,4).
%添加模块名加方法名后可以正常调到方法
5
4> text:add(1,4,8).
13
5> 

```

## 写在后面
引用网络博客内容：
https://www.jianshu.com/p/b45eb9314d1e        （30 分钟学 Erlang (一)）
https://www.w3cschool.cn/erlang/tohb1p5z.html      （w3cschool erlang教程）

个人博客地址：https://zhangyongfeng1.github.io/
简书地址：https://www.jianshu.com/u/137f325832fb

