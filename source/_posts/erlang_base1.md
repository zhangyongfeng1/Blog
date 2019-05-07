
---
title: erlang-基本语法_1、io:format输出、基本数据类型
date:  2018-06-11 13:27:25
tags: [erlang]
categories: 张永枫
description:
---
<!-- TOC -->

- [写在前面](#写在前面)
- [介绍](#介绍)
    - [.为什么要用到erlang？](#为什么要用到erlang)
    - [.什么时候要用到erlang？](#什么时候要用到erlang)
    - [.erlang可以用来干什么？](#erlang可以用来干什么)
- [安装（网上有教程这里先不说明）](#安装网上有教程这里先不说明)
- [基本语法](#基本语法)
    - [注释](#注释)
    - [入门语法示例:](#入门语法示例)
- [.基本数据类型](#基本数据类型)
    - [.1、Numbers数字运算法则](#1numbers数字运算法则)
    - [.2、Boolean布尔数据类型（与或非）](#2boolean布尔数据类型与或非)
    - [.3、比较](#3比较)
- [写在后面](#写在后面)

<!-- /TOC -->
## 写在前面
本文主要是以一个erlang的学习记录，有错误的地方欢迎指正。

## 介绍
![自已梳理erlang学习脑图](https://upload-images.jianshu.io/upload_images/6841945-2243e6e21b9b06d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### .为什么要用到erlang？
高并发（）
高容错（）
软实时（修改一个erl文件时，不需要全部文件重新编译，只需要编译修改的那个文件即可）

### .什么时候要用到erlang？
高并发请求的服务可以用到。

### .erlang可以用来干什么？
可以搭建成一个web的服务器。

## 安装（网上有教程这里先不说明）

## 基本语法
### 注释
（用％来注释）
### 入门语法示例:
```
➜ ~ erl Erlang/OTP 20 [erts-9.3] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:10] [hipe] [kernel-poll:false] [dtrace] Eshell V9.3 (abort with ^G)
 1> io:format("hello world!~n").
 hello world! 
ok 
2> 1 + 1.
2 
3> q(). 
ok 
➜ ~
```
第一个是io:format("hello world!~n").表示输出一串hello world的字符串，
其中的~n表示的是换行处理，
输出的ok，是函数的返回值。

第二个是一个加法的运算;

第三个是退出当前erlang的shell命令窗口;也可以在erlang shell（erlang交互命令行） 中执行halt().来退出命令窗口。

```
9> halt().
➜  erlang 
```

## .基本数据类型
### .1、Numbers数字运算法则
```
1> 2 + 15. ％加法
17 
2> 49 * 100. ％乘法
4900 
3> 1892 - 1472. ％减法
420 
4> 5 / 2. %% 最常用的浮点数除法 
2.5 
5> 5 div 2. %% div 是整除 
2 
6> 5 rem 2. %% rem 是取余运算 
1
 %% 数字前面可以用 ‘#’ 来标注其 ‘Base’
 %% 语法：Base#Value %% 默认的 Base 10 … 
％％从其他进制转为十进制
10> 2#101010. %% 2 进制的 101010 
42 
11> 8#0677. %% 8 进制的 0677 
447 
12> 16#AE. %% 16 进制的 AE 
174
```
### .2、Boolean布尔数据类型（与或非）

atom 类型的 true 和 false 两个值，被用作布尔处理。
```
1> true and false. %% 逻辑 并 
false 
2> false or true. %% 逻辑 或 
true 
3> true xor false. %% 逻辑 异或 
true 
4> not false. %% 逻辑 非 
true 
5> not (true and true). 
false 
```
还有两个与 and 和 or 类似的操作：andalso和 orelse。区别是 and 和 or 不论左边的运算结果是真还是假，都会执行右边的操作。而 andalso 和 orelse是短路的，意味着右边的运算不一定会执行。

来看一下比较：
### .3、比较
```
6> 5 =:= 5. %% =:= 是"严格相等"运算符，== "是大概相等" 
true 
7> 1 =:= 0. 
false 
8> 1 =/= 0. %% =/= 是"严格不等"运算符，/= "是相差很多" 
true 
9> 5 =:= 5.0. 
false 
10> 5 == 5.0. 
true 
11> 5 /= 5.0. 
false 
```
一般如果懒得纠结太多，用 =:= 和 =/= 就可以了。

```
12> 1 < 2. 
true 
13> 1 < 1. 
false 
14> 1 >= 1. %% 大于等于 
true 
15> 1 =< 1. %% 注意这个 "小于等于" 的写法，= 在前面。因为 => 还有其他的用处。。 
true 
17> 0 == false. %% 数字和 atom 类型是不相等的 
false 
18> 1 < false. 
true 
```

虽然不同的类型之间可以比较，也有个对应的顺序，但一般情况用不到的:
number < atom < reference < fun < port < pid < tuple < list < bit string


## 写在后面
引用网络博客内容：
https://www.jianshu.com/p/b45eb9314d1e        （30 分钟学 Erlang (一)）
https://www.w3cschool.cn/erlang/tohb1p5z.html      （w3cschool erlang教程）


