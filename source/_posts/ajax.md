---
title: ajax小记
date: 2023-01-16 12:12:12
tags: [ajax,记录]
categories: [张永枫]
description: ajax
---
	
#	1.url
url是（ Uniform Resource Locator ）统一资源定位符的缩写。

## 完整格式&语法
```
scheme:[//[user[:password]@]host[:port]][/path][?query][#fragment]
```

    scheme：传送协议。 层级URL标记符号(为[//],固定不变) 访问资源需要的凭证信息（可省略）
    host：服务器。（通常为域名，有时为IP地址）
    port：端口号。（以数字方式表示，若为HTTP的默认值“:80”可省略）
    path：路径。（以“/”字符区别路径中的每一个目录名称）
    query：查询。（GET模式的窗体参数，以“?”字符为起点，每个参数以“&”隔开，再以“=”分fragment：开参数名称与数据，通常以UTF8的URL编码，避开字符冲突的问题）
    ?a=1&b=2; 参数
    fragment:锚点/片段。以“#”字符为起点

## 常见协议

    ftp 21 文件
    ssh 22
    telnet 23
    smtp 25 邮件
    dns 53
    http 80

# 2.DNS运行原理

## http协议

###    1、作用 
        规范数据打包，传递方式
        http/1.1 web 

###    2、Message 消息 / 报文
在http和服务器之间传递的数据块
分类：

```
    1、Request Message :客户端请求的消息
    2、Response Message :服务器根据客户端请求返回的消息
    src 
    sprict
```

###    3、请求消息（request message）
#### 1、请求起始行
1、请求方法
* 1、GET 客户端获取服务器上的资源

        特点：
        1、无请求主体
        2.依靠地址栏传递数据组服务器
* 2、POST

        表示客户端想传递数据给服务器
        特点：
            1、有请求主体
* 3、PUT(禁用)

        客户端想把文件放到服务器上
        特点：
            1、有请求主体
* 4、DELETE(禁用)

        客户端想把服务器上的文件删除
* 5、HEAD

        表示只想获取指定的响应头
* 6、CONNECT

        测试连接
* 7、TRACE

        追踪请示路径
* 8、OPTIONS

    选项，保留以后使用

#### 2、请求的url== 
    3、协议 和 版本号
        http 1.1

        2、请求头
            1、host:localhost

            2、Connection:keep-alive
                持久的连接
            3、User-Agent
                浏览器的类型
            4、Cache-Control:mac-age=0
                缓存信息 max-age不缓存
            5、Accept-Language:zh-CN
                服务器能接收的自然语言
            6、Accept-Encoding:gzip
                告诉服务器自已可以压缩的类型
            7、Referer:url
                告诉服务器请求来自于那个页面
        3、请求主体(Request Message）
            Form Date 
        注意
            Query String:不算作请求主体，是属于URl的一部分
        4、响应消息（Response Message）
            1、响应起始行
                1、版本号
                    http 1.1
                2、响应状态码
                    1、1XX
                        提示信息	
                    2、2XX
                        200：服务器端成功响应所有的信息ok
                    3、3XX
                        需要客户端进行重定向
                        301：永久性重定向
                        302：临时重定向
                        304：Not Modified
                    4、4XX
                        客户端请示错误
                        404： Not Found 请求资源不存在
                        403： Forbidden 没有访问权限
                        405:  Method Not Allowed 请求方法不被允许
                    5、5XX
                        服务器运行错误
                        500：服务器内部错误
                        501：没有实现
                3、原因短句
                    对状态码的简单解释
                    200：ok
                    404: Not Found
                    ......
            2、响应消息头
                1、Content-type
                    响应的主体类型，告诉浏览器，响应数以后有时的格式和类型
                    取值
                    1、text/plain 纯文本
                    2、text/html 文本与网页
                    3、text/css css解析
                    4、application/javascript JS代码片段，按JS的方式运行数据
                    5、application/xml
                        按xml的方式解析
                    6、application/json
                        按json的方式解析
                2、Date
                    日期
            3、响应主体
                Preview Response
                由服务器响应回来的数据
## 缓存
		1、缓存的工作原理
			客户端可以自动保存已访问过的文档的副本
			当客户端再向同一url发送请求时，可以直接从缓存中取出来，不有再重新发送请求
		2、优点
			1、节省流理
			2、节省更多带宽
			3、服务资源利用
			4、降低加载延迟
		3、与缓存相关的消息头
			1、cache-control
				作用：从服务器将文档传来时认为新鲜的秒数
				取值： 秒数 60、3600 
				0/on-cache 每次都要重新刷新
			2、Expires 指定缓存过期的时间，取值是格林尼冶标准时间（GMT）
			Expries:
			Expires:0 不需要缓存
		4、如何在网页中设置消息头
			http-equiv:消息头名称
			content：消息头内容
			<meta http-equiv="Content-Type" content="text/html">
			设置文本为html格式
			<meta http-equiv="Cache-Control" content="on-cache">
			设置是否缓存
	3、DOM操作
		Document Object Model 文档对象模型 操作页面的元素
		1、使用JS获取页面上的某个元素
			1、为元素增加ID属性
				<div id="d1" >hello world</div>xfxw
			2、在JS中，允许通过元素的ID获取页面元素

            ```js
				document.getElementById("元素ID");

				function printDiv(){
					//1、获取元素
					var elem = document.getElementById("d1");
					console.log(elem);
				}
            ```

				elem 就是指定ID值的元素在JS中的表现形式
		2、修改/获取标记内的内容
			属性：innerHTML
				赋值：为某元素的innerHTM属性赋值
				取值；获取某元素的innerHTML属性
				ex:
					elem.innerHTML ="hello world";
					console.log(elem.innerHTML);
				练习:
```html
<div id="d1">hello world</div>
<button onclick="getid()" >显示元素id内容</button>
<button onclick="setid()" >设置元素id内容</button>
```
```js
function getid(){
    //   var elem = document.getElementById('d1');
    // console.log(elem.innerHTML);
    //简写
    document.getElementById('d1').innerHTML;
}
function setid(){
        // var elem = document.getElementById('d1');
    //  elem.innerHTML="<h1>alkdlfl</h1>";
    // console.log(elem.innerHTML);
    //简写
    document.getElementById('d1').innerHTML="<h1>alkdlfl</h1>";
```
		3、获取、设置 表单控件的数据
			文本框,密码框...通过value 属性来获取或设置控件的值
			ex:
```html
<input type="text" id="uname">
<button onclick='showinput()'>显示输入的内容</button>
<button onclick='setinput()'>改变输入的内容</button>
```
```js
function showinput(){
    var ele = document.getElementById('uname');
    console.log(ele.value);
}

function setinput(){
    var ele = document.getElementById('uname');
    ele.value="111";
}
```
练习:
```html
<input type="text" id='input1'>
<div id="show">1</div>
<button onclick="showname()">显示</button>
```
```js
function showname(){
    var input_value = document.getElementById('input1').value;
    document.getElementById("show").innerHTML="<h1>"+input_value+"</h1>";
}
```

		4、简化document.getElementById()
			//作用 根据指定的ID值，获取对应的HTML元素
			//参数 id :要获取元素的id值
			//返回值: 要获取对应的HTML元素
```js
function $(id){
    return document.getElementById(id);
}
<div id='d2'>hello world</div>
<button onclick="showText2()">d2 的值</button>
<button onclick="setText2()">set d2 的值</button>

function showText2(){
    var elem2 = $('d2');
    console.log(elem2.innerHTML);
}
function setText2(){
    $('d2').innerHTML ="ssss";
}
```
		5、HTML 元素的事件
			事件：在某些特殊情况下，可以被激发的事件
				onclick 
			1、文本框、密码框的事件 onblur
				onblur 事件，鼠标离开时触发的事件
```js
function onblur_t1(){
    $('onblur_s1').innerHTML = $("onblur_uname").value;
}
```
```html
<div id="onblur_s1"></div>
<input type='text' id="onblur_uname" onblur="onblur_t1()">
```
			2、onfocus 获取焦点时要执行的操作
			练习:
				1、文本框失去焦点时，判断文本框中的数据是否为空，如果为空，在span 中提示用户名不能为空，否则提示通过
```html           
<input type='text' onblur='span_show1()' id="input_v1">
<span id='span_tip'></span>
```
```js
function span_show1(){
    if($('input_v1').value==""){
        $("span_tip").innerHTML="用户名不能为空";
    }else{
        $("span_tip").innerHTML="输入正确";

    }
}
```
			3、body 的事件 -- onload
				在网页加载时要执行的操作，可以封装在onload 中
				<input type="text" id="onload_uname">
				//加载时初始化
				function body_onload(){
					$("onload_uname").value="请输入您的用户名称"
				}

				作业：显示数据
				tbody
				编号 书名 作者 操作（修改 删除）
				1 西游记 吴恩
				2 水浒传 施耐庵
```vue
<button onclick="show_table()">显示数据</button>
<table border="1" width='400px'>
    <thead>
        <tr>
            <td>编号</td>
            <td>书名</td>
            <td>作者</td>
            <td>操作</td>
        </tr>
    </thead>
    <tbody id ="tbody">
    </tbody>
</table>

function show_table(){
    var html ="";
    html += "<tr>";
        html += "<td>1</td>";
        html += "<td>西游记</td>";
        html += "<td>吴承恩</td>";
        html += "<td>";
            html += "<button>修改</button>";
            html += "<button>删除</button>";
        html += "</td>";
    html += "</tr>";
    $("tbody").innerHTML=html;
}
```
# 3、DOM	
## 事件
    onchange 选项发生改变的时候

```vue
<select id='selProvince' onchange="changeProvince()">
    <option value="-1">=请选择=</option>
    <option value="0">黑龙江</option>
    <option value="1">吉林</option>
    <option value="2">辽宁</option>
</select>

function changeProvince(){
    var val = $("selProvince").value;
    console.log('您选中的值:' + val);
}

//创建一个二维数组
var city = [
    ['哈尔滨','heb'],
    ['长春','cc'],
    ['沈阳','sy']
];

```


    练习1:=========
```js
<select id='selProvince' onchange="changeProvince()">
    <option value="-1">=请选择=</option>
    <option value="0">黑龙江</option>
    <option value="1">吉林</option>
    <option value="2">辽宁</option>
</select>
<select id='selCity'>
    <option value='-1'>=请先选择省份=</option>
</select>
function changeProvince(){
    var val = $("selProvince").value;
    console.log('您选中的值:' + val);
    if(val == -1){
        var html ="<option>请先选择省份</option>";
        $("selCity").innerHTML = html;
    }else{
        var html = "";
        console.log(city[val]);
        for(var i = 0;i<city[val].length;i++){
            html += "<option value='"+i+"'>"+ city[val][i]+"</option>";
        }
        console.log(html);
        $("selCity").innerHTML = html;
    }
}
```

    练习2:=========
```js
<form action="02_checkname.php">
    用户名:
    <input type="text" name="uname">
    <span id='uname_show'>*</span>
    <input type="submit" value="验证用户名">
</form>
```

    =php=02_checkname.php
```php
<?php
    $uname = $_REQUEST['uname'];
    if($uname == "admin"){
        echo "用户名称已存在"
    }else{
        echo "用户名称不存在"
    }
?>
```
## AJAX
1、名词解释
    1、同步
        客户端只能等待服务器的响应
        ex:
            1、输入网址访问页面
            2、a标记的默认跳转
            3、submit 按钮的表单提交
    2、异步
        在一段时间内，可以做多件事情
        ex:
            1、用户名的重复性验证
            2、聊天室
            3、股票图
            4、搜索建议
2、ajax 
    asynchronous javascript and xml
    本质：使用js提供的XMLHttpRequest对象，	异步的向服务器发送请求，并接受响应数据（格式为xml[过时]）

    返回部分数据，可以以无刷新的效果来更改页面中的局部内容
3、获取 AJAX核心对象 - XMLHttpRequest	
    标准创建：var xhr = new XMLHttpRequest();
    IE8 以下：
```js
var xhr = new ActiveXObject("Microsoft.XMLHttp");

允许通过 window.XMLHttpRequest判断浏览器是否支持XMLHttpRequest()
返回值为:null时,说明不支持;

var xhr;
//判断浏览器是否支持XMLHttpRequest
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest();
}else{
    xhr = new ActiveXObject("Microsoft.XMLHttp");
};
console.log(xhr);

function createXhr(){
    var xhr;
    //1、声明一个xhr对象，用于保存不同浏览器中创建出来的AJAX核心对象
    //2、判断浏览器是否支持XMLHttpRequest
    if(window.XMLHttpRequest){
        xhr = new XMLHttpRequest();
    }else{
        xhr = new ActiveXObject("Microsoft.XMLHttp");
    }
    return xhr;
}
```
4、XHR的常用属性和方法（难点）
    1、open()方法
        作用：创建请求
        语法：open(method,url,isAsyn)
        1、method
            string 类型
            请求方式；get post
        2、url
            string 
            请求地址
        3、isAsyn
            boolean 类型
            指定采用同步（false）还是异步（true）的方式发送请求 
    2、readyState -xhr的属性
        作用：表示xhr 对象的请求状态
        值：由0-5表示5 个状态
        0: 请求尚未初始化
        1: 已经打开开web的连接，正在向服务器发送请求
        2、请求完成
        3、正在接收服务器端的响应
        4、接收响应数据成功
        注意:当readyState 的值为4的时候，表示所有的响应都已经接收完毕
    3、status - 属性
        作用： 服务器的响应状态码
        为200是表示服务器已经正确响应
    4、onreadstatechange - 事件
        作用：当xhr的readyState 属性值发生改变的时候，要自运激发的操作。
        语法：
```js
xhr.onreadystatechange = function(){
    //当xhr的readyState 属性值发生改变的时候要执行的操作

    //判断xhr.readyState 为4的时候，并且xhr.status为200的时候，才能获取正常的响应数据

    if(xhr.readyState ==4 && xhr.status == 200){
        //可以接收响应回来的数据
        //responseText属性，表示服务器响应回来的文本
        var resText = xhr.responseText;
    }
}
```
    5、send -方法
        作用：发送\提交请求
        语法：send(body)
            body:是请求主体
            没有请求主体的提交方式，body位置处，要写null
            有的话写主体的数据
5、发送异步请求的步骤
    1、创建/获取xhr对象
    2、创建请求，xhr.open()
    3、设置xhr的onreadystatechange 事件
```js
xhr.onreadystatechange=function(){
    if(xhr.readyState == 4 && xhr.statue ==200){
        xhr.responseText;
    }
};
```
    4、发送请求
        xhr.send();

    05_textajax.php
        <?php
            echo "oneoneone 这是php回显的数据";
        ?>
    long.html
```html
function getInfo(){
    //1 创建 
    var xhr = createXhr();
    //2 创建请求
    xhr.open('get',"05_textajax.php",true);
    //3 设置 onreadystatechange（回调函数）
    xhr.onreadystatechange=function(){
        if(xhr.readyState== 4 && xhr.status ==200){
            //接收响应数据
            var text = xhr.responseText
            console.log(text);
            $("msg-show").innerHTML = text;
        }
    }
    //4 发送请求
    xhr.send(null);
};

<div id='msg-show'></div>
<button onclick="getInfo()">发送异步请求</button>
```

## 作业:
    1、创建htm1.html 页面，用php查询数据库，验证用户密码是否正确。
    查询数据库
    ajax异步请求 get

    ==00_con_mysql.php
    <?php
        /*
        连接数据库
        ip地址
        用户
        密码
        数据库
        */
        $conn = mysqli_connect("localhost","root","a3c2218636677573","bplan_top");
        
        $sql = "SET NAMES UTF8";
        mysqli_query($conn,$sql);
    ?>
    ==00_checkUname.php
    <?php
        #1、数据库连接
        require("00_con_mysql.php");
        #2、接收前端传递过来的数据
        $uname = $_REQUEST["uname"];
        #3、到数据库中验证用户名称是否存在
        $sql = "select * from xuezi where uname = '$uname'";
        $result = mysqli_query($conn,$sql);
        $row = mysqli_fetch_row($result);
        if($row == null){
            echo "通过";
        }else{
            echo "用户名称已存在";
        }
        #ALTER TABLE  `xuezi` ADD pwd VARCHAR( 20 ) NULL DEFAULT  '' COMMENT  '用户名'
    ?>
    ==html----------
    //查询数据库校验用户名和密码  ---start
    function check_uname(){
        console.log('11111');

        var xhr = createXhr();
        var uname = $('check_uname').value;
        console.log(uname);
        var url = '00_checkUname.php?uname='+uname;
        xhr.open("get",url,true);
        xhr.onreadystatechange=function(){
            if(xhr.readyState==4 && xhr.status==200){
                $('check_uname_show').innerHTML = xhr.responseText;
            }
        };
        xhr.send(null);
    }
    //查询数据库校验用户名和密码  ---end

    <!-- 查询数据库校验用户名和密码 start -->
    <fieldset>
        <legend>查询数据库校验用户名和密码</legend>
            用户名：<input type ='text' id='check_uname' onblur="check_uname()" >
            <span id='check_uname_show'></span><br/>
            密码：<input type ='password' name="check_rpwd">
        </form>
    </fieldset>
    <!-- 查询数据库校验用户名和密码 end -->

# 使用post方式提交请求 
		1、提交的请求数据
			提交的请求数据需要按照指定的格式拼好，放在send()中传递
			xhr.send("name1=value1&name2=value2");
		2、设置一个请求消息头
			POST 提交方式
			将Content-type 的请求消息头改为application/x-www/form-urlencoded
			在发送请求之前(post)
			xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
```js
<?php
    /*
    连接数据库
    ip地址
    用户
    密码
    数据库
    */
    $conn = mysqli_connect("localhost","root","a3c2218636677573","bplan_top");
    
    $sql = "SET NAMES UTF8";
    mysqli_query($conn,$sql);
?>

<?php
    #1、数据库连接
        require("00_con_mysql.php");
    #2、接收前端传递过来的数据
        $uname = $_REQUEST["uname"];
        $upwd = $_REQUEST["upwd"];
    #3、到数据库中验证用户名和密码是否存在
        $sql = "select * from xuezi where uname = '$uname' and pwd= '$upwd'";
        $result = mysqli_query($conn,$sql);
        $row = mysqli_fetch_row($result);
        if($row == null){
            echo "用户或密码不正确";
        }else{
            echo "登录成功";
        }
?>

//校验用户名和密码
function check_uname_post(){
    var xhr = createXhr();
    var uname = $('check_uname').value;
    var upwd = $('check_upwd').value;
    var url = '00_checkUnameandpwd_post.php'
    xhr.open("post",url,true);
    xhr.onreadystatechange=function(){
        if(xhr.readyState==4 && xhr.status==200){
            $('check_unameandpwd_show').innerHTML = xhr.responseText;
        }
    };
    xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");

    xhr.send("uname=" + uname + "&upwd=" + upwd);
}
```
## 练习 省市级联
### 1、00_province.php 生成列表中的数据
```
<option value=0>helongjian</option>
<option value=1>jilings</option>
```
			1、在00_provice.html中，网页加载时，异步的向00_province.php发送请求，并将响应的数据填充在<select>中

			<?php 
				#1 声明一个数组并且初始化三个省份的信息
				$array = ["heilongjiang","jiling","liaoning"];
				#2 循环遍历数组，取出每个省份的信息，拼成一个字符串
				$opts="";
				for($i=0;$i<count($array);$i++){
					$opts.="<option value='$i' >$array[$i]</option>";
				}
				#3 将生成的字符串响应给客户端
				echo $opts;
			?>
```js
<body onload="loadProvince()"> 
        <select id='selProvince' onchange="showcity()">
        </select>
        <select id="selCity">
        </select>
</body>

function loadProvince(){
    //1、获取xhr
    var xhr = createXhr();
    //2、创建请求
    xhr.open('get','00_province.php',true);
    //3、设置回调
    xhr.onreadystatechange = function(){
        if(xhr.readyState==4 && xhr.status==200){
            $('selProvince').innerHTML = xhr.responseText;
        }
    }
    //4、发送请求
    xhr.send(null);
}
```
			2、在00_province2.php中创建一个二维数组，保存省份对应城市的信息
			3、根据传递过来的value值，取出对应的城市信息，拼成<option>响应回去并显示在下拉选项框中 
```js
<?php 
    $array =[
        ["h1","h2",'h3'],
        ['j1','j2','j3'],
        ['L1','L2',"l3"]
    ];
    $Province_value=$_REQUEST('Province_value');
    $opts='';
    for($i=0;$i<count($array);$i++){
        $opts .= "<option value='$i'>$array[$i]</option>"
    }
    echo $opts;
?>

function showcity(){
    //1、获取xhr
    var xhr = createXhr();
    //2、创建请求
    var Province_value = $("selProvince").value;
    xhr.open('get','00_province2.php?Province_value='+Province_value,true);
    //3、设置回调
    xhr.onreadystatechange = function(){
        if(xhr.readyState==4 && xhr.status==200){
            $('selCity').innerHTML = xhr.responseText;
        }
    }
    //4、发送请求
    xhr.send(null);
}
```
### 2、JSON 	
		1、什么是JSON 
			javaScript Object Notation js对象表示法以js对象的方法来表示字符串 字符串
		2、js对象
			用{}来表示对象
```js
			var fbb = [];
			fbb[0] = 121;
			fbb[1] = 73;
			fbb[2] = 116;

			fbb['yuwen'] = 121;
			fbb['shuxue'] = 73;
			fbb['yingyu'] = 116;

			var fbb_obj = {
				yuwen:121,
				shuxue:73,
				yingyu:116
			};

			function showObject(){
				//1、创建一个对象，名称为fbb,包含三个属性
				var fbb = {
					height:121,
					weight:73,
					gender:'女'
				};

				//2、打印对应属性的值
				console.log(fbb.yuwen);
				console.log(fbb.shuxue);
				console.log(fbb.yingyu);

				//创建一个新的对象
				var ym ={ 
					height:165,
					weight:50,
					gender:"女"
				};
				//3、声明一个数组，保存fbb 和 ym
				var star = [fbb,ym];
				console.log(star);
				//循环打印数组
				for(var i=0;i<star.length;i++){
					var s = star[i]; 
					console.log(s.height,s.weight,s.gender);
				}
			}

			//数组对象 明星数组
			var star = [
				{
					height:121,
					weight:73,
					gender:'女'
				},
				{ 
					height:165,
					weight:50,
					gender:"女"
				},
				{ 
					height:160,
					weight:49,
					gender:"女"
				}
			];

			//循环打印数组
			for(var i=0;i<star.length;i++){
				var s = star[i]; 
				console.log(s.height,s.weight,s.gender);
			}
```
		3、JSON
			1、JSON对象
				语法：
					1、用一对{}来表示一个对象
					2、对象的属性名称，必须用“”引起来，值如果也是字符串，也必须用“”引起来
					3、属性 与 值，用:连接
					4、多对属性 与 值之间，用，分开
				ex:
					var ym = '{"height":174,"weight":50}';
			2、JSON数组
				1、普通数组表现：'['ym','fbb','fj']';
				2、对象的数组：
```js
				'[
					{
						"height":170,
						"weight":55,
						"geight":女
					},
					{
						"height":160,
						"weight":49,
						"geight":女
					}
				]'
```
			3、JOSN文件
				创建一个文件，以 ***.json 作为后缀
				该文件中的数据必须是json 格式的字符串
				04_Pesion.json
```js
					[
						{
							"name":"fbb",
							"age":"40",
							"gender":"女"
						},
						{
							"name":"lic",
							"age":"41",
							"gender":"男"
						},
						{
							"name":"ym",
							"age":"31",
							"gender":"女"
						}
					]
```
				04_getjson.html
				<!-- http://bplan.top/ajax_t/04_getjson.html 外网地址 -->
					
			4、将JOSN字符串转成JS对象/数组
				var p = '{"name":"sf.z","age":25}';
				1、使用eval()
					var obj = eval("("+p+")");
				2、使用JSON.parse()来解析JSON字符串得到JS对象
					var obj = JSON.parse(p);
				练习：
					1、创建一个05_user.json的文件，里面包含一个数组，数组中有3个对象，每个对象包含uname,upwd,gender 属性
```js
					[
						{
							"uname":'1',
							"upwd":"123",
							"gender":"女"
						},
						{
							"uname":'2',
							"upwd":"123",
							"gender":"女"
						},
						{
							"uname":'3',
							"upwd":"123",
							"gender":"男"
						}
					]
```
					2、创建一个05_getusers.html，使用异步的方式向user.json发送一个请求，并按以下格式打印输出数据
					<!-- http://bplan.top/ajax_t/05_getusers.html 外网地址 -->
			5、在php中，可以直接将数组（）转换成JSON可笑式的字符串
				php中通过： json_encode()将数组转换为JSON字符串
				语法： 
					￥str = json_encode($array);
				注意：如果服务器端响应回来的数据时JSON格式时，需要增加响应消息头
				header("Content-Type:application/json");

				#http://bplan.top/ajax_t/06_city.php
				#http://bplan.top/ajax_t/07_textJSON.php
```php
				<?php
					#1、增加响应消息头
					header("Content-Type:application/json");
					#2、声明一个普通数组，并且以 JSON 格式进行响应
					$province = ["heilongjiang",'jilin',liaoning];
					#3、将数组转为json格式的字符
					$str = json_encode($province);
					#4、响应给客户端
					echo $str;
				?>
```
			作业：
			unmae 用户名  email 邮件   操作
			
			网页加载数据库内容

			并转换为关联数组 mysqli_fetch_all($result,MYSLQi_ASSOC)

			转换为json,响应组客户端

			在前端拼接好数据

# 1、XML
## 1、什么是xml 
			eXtensible Markup Language 
			可扩展的    标记	   语言
			xml的标记没有被预定义，需要自行定义
			xml的宗旨是做数据传递，而非数据显示
## 2、xml的语法规范
			xml可以独立的保存成为 **.xml 文件，也可以以字符串的形式出现(服务器端生成)
			1、xml的最顶端是xml的声明
				<?xml version="1.0" encoding='uft-8' ?>
			练习：
				创建一个student.xml文件，并添加xml声明

				<?xml version='1.0' encoding="utf-8" ?>
			2、xml标记的语法
				1、XML标记是成对出现，所有的标记必须要显示的结果
					<person /> 错误
					<person>aa    错误
					<person>bb</person>  正确
				2、XML标记是严格区分大小写,开始和结束必须一致
					<person><Person> 错误
					<Person></Person> 正确
					<perSon></perSon> 正确
				3、标记允许嵌套，注意嵌套顺序即可（与HTML一致）
					<person>
						<name>fbb</name>
						<age>11</age>
					</person>
				4、每个标记都允许自定义属性，格式等同于HTML，但属性值，必须使用引号括起来
					<person id="1001" gender="male"></person>
				5、每个xml文档中，有且只有一个根元素

				练习：
					1、在student.xml基础中完成
						1、创建一对根元素 studentList
						2、在studentList 根元素中，使用一对student 元素来表示一名学员的信息
						3、在student 中，再分别使用三个元素来表示姓名(name),性别(gender),年龄(age),并将值写在标记中
						4、创建3个学员的信息
## 3、使用 AJAX 请求 XML 文档			
				1、要遵循AJAX的请求步骤
					1、创建，获取 xhr
					2、创建请求
					3、设置回调
					4、发送请求
				使用 xhr.responseXML 来获取响应的数据,返回的是XML文档对象
			练习：
				在student.xml基础上，使用AJAX向student.xml发送请求，并将响应结果(responseXML)打印在控制台上
				<!-- http://bplan.top/ajax_t/00_10_student.xml-->
				<!-- http://bplan.top/ajax_t/00_10_student.html-->
## 4、解析xml文档内容
				1、核心
					elem.getElementByTagName("标签名")；
					elem: 表示获取范围
					返回值：返回一个包含指定元素的“类数组”:
```js
					var xmlDoc = xhr.responseXML;
					xmlDoc.getElementsByTagName("student");

					var studnetList = xmlDoc.getElementsByTagName("studentList");
```
				2、获取元素中的文本
					elem.innerHTML
## 5、在PHP中返回xml格式的字符串
				1、必须增加响应消息头
					header("Content-Type:application/xml");
				2、按照xml的语法结构，拼xml的字符串,再响应给客户端
```js
					$xml = "<?xml version='1.0' encoding='utf-8' ?>";
					$xml .="<studentList>";
					$xml .="</studentList>";
```
				练习:1、在03_php_xml.php中响应报文
					2、在03_php_xml.html使用AJAX响应数据










		