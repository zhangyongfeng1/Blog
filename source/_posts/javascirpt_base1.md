---
title: javaScript_基础1
date:  2018-06-26 14:27:25
tags: [javascript]
categories: 张永枫
description: javaScript基础示例
---

<!-- TOC -->

- [1. javaScript简介](#1-javascript简介)
    - [1.1. javaScript简单示列：textdemo.html](#11-javascript简单示列textdemohtml)
    - [1.2. 以引入文件形式调用javaScript文件示例：](#12-以引入文件形式调用javascript文件示例)
    - [1.3. 后台调试日志打卬和页面输出示例：](#13-后台调试日志打卬和页面输出示例)
    - [1.4. 定义变量，获取变量类型，判断变量否有赋值](#14-定义变量获取变量类型判断变量否有赋值)
    - [1.5. 拆分一个变量，转换为对象打印出来](#15-拆分一个变量转换为对象打印出来)
    - [1.6. 字符串比较方式：==](#16-字符串比较方式)
    - [1.7. 打印出99乘法表](#17-打印出99乘法表)
    - [1.8. 数组JavaScript](#18-数组javascript)

<!-- /TOC -->
# 1. javaScript简介

## 1.1. javaScript简单示列：textdemo.html

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<script type="text/javascript">
		alert("text");
	</script>
</head>
<body>

</body>
</html>
```

## 1.2. 以引入文件形式调用javaScript文件示例：
在textdemo.html目录下再新建一个文件夹命名为js,再新建一个文件命名为demo.js
demo.js 内容如下：

```
alert("text");
```

textdemo.html

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<script type="text/javascript" src="./js/demo.js">
	</script>
</head>
<body>

</body>
</html>
```

## 1.3. 后台调试日志打卬和页面输出示例：
textdemo.html

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" >
		document.write("<h1>hello world</h1>");
		//通过javascript向页面输出HTML代码
		//输出document.write为不可控
  		console.log("这是后台输出！");
  		//后台调轼通用
	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
```
## 1.4. 定义变量，获取变量类型，判断变量否有赋值

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" > 
		var num = 10;// 定义变量类型 number
		var aa ;// 定义没值的变量类型 undefined
		var bolue = false;
		var string1 = "string"; 
		
		console.log(typeof num);
		console.log(typeof aa);
		console.log(typeof bolue);
		console.log(typeof string1);

		document.write("<h1>" + (typeof num) + "</h1>");
		document.write("<h1>" + (typeof aa) + "</h1>");
		
		//判断变量是否undefined
		if (aa == undefined){
			alert("num 的变量类型没有内容！undefined");
		}

		//判断变量是否false 变量没有值同为underfined 和 布尔类型的false
		if (!aa){
			alert("num 的变量类型没有内容！false");
		}else{
			alert("num 的变量类型有内容！true");
		}

	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
```

## 1.5. 拆分一个变量，转换为对象打印出来
 
 ```
 <!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" > 
		var num = "hello world ni hao";//定义变量
		var result = num.split(" ");//根据空格拆分变量，新生成的为一个对象；
	   //var num = "192.168.1.1";//定义变量
		//var result = num.split(".");
	   document.write("<h1>result变量的类型：" + (typeof result) + "</h1>");
		//打卬对result 的类型
		console.log(result);
		//在后台打卬result的内容

		for (var x = 0 ; x < result.length ; x ++ ){
			document.write("<h1>" + result[x] + "</h1>");
		}

	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
 ```

## 1.6. 字符串比较方式：==

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" > 
		var stra = 'hello';
		var strb = "hello";

		alert(stra == strb);

	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
```

## 1.7. 打印出99乘法表

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" > 
		document.write("<table border='1'>");
		for(var x =1;x <=9 ;x++){
			document.write("<tr>");
			for (var y =1 ;y <= x ;y++){
				document.write("<td>" + x + "*" + y + "=" +(x*y) +"</td>");
			}
			for (var y =1 ;y <=9-x;y++){
				document.write("<td>&nbsp;</td>")
			}	
			document.write("</tr>");
		}
		document.write("</table>");
	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
```

## 1.8. 数组JavaScript
数组JavaScript为数组提供一个length属性来得到数组的长度
定义语法：
     
```
var arr1=[2,5,6]; //定义时直接给数组元素赋值
var arr2=[]; //定义一个空数组
var arr3=new Array(); //定义一个空数组并通过索引来赋值
arr3[0]=1;
arr3[3]="abc";
```

数组特点：
1.数组长度可变，总长度='数组的最大索引值'+1；
2.同一数组中的元素类型可互不相同；
3.当访问未赋值的数组元素时，该元素值为undefined，不会数组越界。
数据创建示列：

```
<!DOCTYPE html>
<html>
<head>
	<title>javascript text</title>
	<meta charset="utf-8">
	<!-- 设置编码为UTF-8 -->
	<script type="text/javascript" > 
		//动态数组
		var result = new Array();
		result[0] = "hello";
		result[1] = 100;
		result[2] = true;

		console.log(result);

		for (var x = 0 ; x < result.length; x++){
			document.write("<h1>" + result[x] +"-->" + (typeof result[x]) +"</h1> ");
		}

		//初始代数据为string类型并打印
		var result1 = new Array('hello',"world","!");

		console.log(result1);

		for (var x = 0 ; x < result1.length; x++){
			document.write("<h1>" + result1[x] +"-->" + (typeof result1[x]) +"</h1> ");
		}
	</script>
</head>
<body>
	<div>你好，世界！</div>
</body>
</html>
```

注：在定义javascript变量时不使用var进行定义时，为全局变量（几乎是不用的）

