---
title: erlang-实战-对文件内容进行处理
date:  2018-06-26 14:27:25
tags: [erlang]
categories: 张永枫
description: 对文件进行处理,将 xml报文格式的报文转为lua 去取值
---

示例为：对文件进行处理
将 xml报文格式的报文转为lua 去取值
如由 

```
<khxm><name>姓名</name><value>123</value></khxm>
```
 转为 
 
```
this.hqzhxx_ccsz_name = body['hqzhxx']["ccsz"]['name']  or "";--持仓市值
```
txt1.txt文件内容如下：

```
<cpgg><name>产品规格</name><value>123克</value></cpgg>
<gmsl><name>购买数量</name><value>234个</value></gmsl>
<gmfe><name>购买份额</name><value>345克</value></gmfe>
```
转换后要的效果如下：

```
this.cpgg_name = body['cpgg']['name'] or '';--产品规格
this.cpgg_value = body['cpgg']['value'] or '';--产品规格
this.gmsl_name = body['gmsl']['name'] or '';--购买数量
this.gmsl_value = body['gmsl']['value'] or '';--购买数量
this.gmfe_name = body['gmfe']['name'] or '';--购买份额
this.gmfe_value = body['gmfe']['value'] or '';--购买份额
```

erl处理文件(file_change.erl)代码如下：

```
-module(file_change).
-export([process/2]).

%对文件进行处理
%将 xml报文格式的报文转为lua 去取值
%如由 <khxm><name>姓名</name><value>123</value></khxm> 转为 
%this.hqzhxx_ccsz_name = body['hqzhxx']["ccsz"]['name']  or "";--持仓市值

process(FileIn, FileOut)->
	{Status,Value} = file:open(FileIn,read),
	if Status =:= ok ->
			io:format("==== open successed ====!~n"),
			Tokens = readFile(Value),%%读取文件并处理
			io:format("file_value------~p ~n",[Tokens]),
			file:write_file("./"++FileOut,[Tokens]),%%写文件
			io:format("==== end ===!~n");
	   	Status =/= ok ->
			io:format("open file error!")
	end.
	
readFile(Value) ->
	readFile(Value,[]).

readFile(Value,ReturnList) ->
	OneLine = io:get_line(Value,""),%一行一行读取文件
	if 
		OneLine =:= eof -> %文件末尾标记 文件结束,关闭文件
			io:format("acrss the file end! ~n"),
			file:close(Value),
			ReturnList;
		OneLine =/= eof ->
			Tokens = string:tokens(OneLine,"< > /> \n"),% 使用多个分隔符把字符串分割

			Len = string:len(Tokens),%获取一个字符长度
			if  Len =:= 0 ->
					io:format(" end to read ~n"),
					file:close(Value),
					ReturnList;
				Len =/= 0 ->
					%对一行的数据进行处理
					io:format(" the line Value ~p~n",[OneLine]),
					%<khxm><name>姓名</name><value>123</value></khxm>
					%this.hqzhxx_ccsz_name = body['hqzhxx']["ccsz"]['name']  or "";--持仓市值
					%%取出列表对应个数的值
					Tokens_1 = lists:nth(1,Tokens),%
					Tokens_2 = lists:nth(2,Tokens),%name
					Tokens_3 = lists:nth(3,Tokens),%注解
					Tokens_5 = lists:nth(5,Tokens),%value

					%对字符串进行拼接
					BB = "this." ++ Tokens_1 ++ "_" ++ Tokens_2,
					BB2 = "this." ++ Tokens_1 ++ "_" ++ Tokens_5,
					CC  = "body['" ++ Tokens_1 ++"']['" ++Tokens_2++ "']",
					CC2  = "body['" ++ Tokens_1 ++"']['" ++Tokens_5++ "']",
					DD = " or '';--" ++Tokens_3,
					EE = BB ++ " = " ++ CC ++ DD ++ "\n",
					EE2 = BB2 ++ " = " ++ CC2 ++ DD ++ "\n",

					GG =string:concat(EE,EE2),%将两个字符串列表拼接

					% io:format(" the line Value BB ~p~n",[BB]),
					% io:format(" the line Value BB2 ~p~n",[BB2]),
					% io:format(" the line Value CC ~p~n",[CC]),
					% io:format(" the line Value CC2 ~p~n",[CC2]),
					% io:format(" the line Value DD ~p~n",[DD]),
					% io:format(" the line Value EE ~p~n",[EE]),
					% io:format(" the line Value EE2 ~p~n",[EE2]),
					NewDic = string:concat(ReturnList,GG),
					readFile(Value,NewDic)
			end
	end.

```

在erlang shell 输入如下：

```
7> c(file_change).                              
{ok,file_change}
8> file_change:process("./txt1.txt","txt3.txt").
==== open successed ====!
 the line Value [60,99,112,103,103,62,60,110,97,109,101,62,228,186,167,229,
                 147,129,232,167,132,230,160,188,60,47,110,97,109,101,62,60,
                 118,97,108,117,101,62,49,50,51,229,133,139,60,47,118,97,108,
                 117,101,62,60,47,99,112,103,103,62,10]
 the line Value [60,103,109,115,108,62,60,110,97,109,101,62,232,180,173,228,
                 185,176,230,149,176,233,135,143,60,47,110,97,109,101,62,60,
                 118,97,108,117,101,62,50,51,52,228,184,170,60,47,118,97,108,
                 117,101,62,60,47,103,109,115,108,62,10]
 the line Value [60,103,109,102,101,62,60,110,97,109,101,62,232,180,173,228,
                 185,176,228,187,189,233,162,157,60,47,110,97,109,101,62,60,
                 118,97,108,117,101,62,51,52,53,229,133,139,60,47,118,97,108,
                 117,101,62,60,47,103,109,102,101,62]
acrss the file end! 
file_value------[116,104,105,115,46,99,112,103,103,95,110,97,109,101,32,61,32,
                 98,111,100,121,91,39,99,112,103,103,39,93,91,39,110,97,109,
                 101,39,93,32,111,114,32,39,39,59,45,45,228,186,167,229,147,
                 129,232,167,132,230,160,188,10,116,104,105,115,46,99,112,103,
                 103,95,118,97,108,117,101,32,61,32,98,111,100,121,91,39,99,
                 112,103,103,39,93,91,39,118,97,108,117,101,39,93,32,111,114,
                 32,39,39,59,45,45,228,186,167,229,147,129,232,167,132,230,
                 160,188,10,116,104,105,115,46,103,109,115,108,95,110,97,109,
                 101,32,61,32,98,111,100,121,91,39,103,109,115,108,39,93,91,
                 39,110,97,109,101,39,93,32,111,114,32,39,39,59,45,45,232,180,
                 173,228,185,176,230,149,176,233,135,143,10,116,104,105,115,
                 46,103,109,115,108,95,118,97,108,117,101,32,61,32,98,111,100,
                 121,91,39,103,109,115,108,39,93,91,39,118,97,108,117,101,39,
                 93,32,111,114,32,39,39,59,45,45,232,180,173,228,185,176,230,
                 149,176,233,135,143,10,116,104,105,115,46,103,109,102,101,95,
                 110,97,109,101,32,61,32,98,111,100,121,91,39,103,109,102,101,
                 39,93,91,39,110,97,109,101,39,93,32,111,114,32,39,39,59,45,
                 45,232,180,173,228,185,176,228,187,189,233,162,157,10,116,
                 104,105,115,46,103,109,102,101,95,118,97,108,117,101,32,61,
                 32,98,111,100,121,91,39,103,109,102,101,39,93,91,39,118,97,
                 108,117,101,39,93,32,111,114,32,39,39,59,45,45,232,180,173,
                 228,185,176,228,187,189,233,162,157,10] 
==== end ===!
ok
9> 
```

注：本示例txt1.txt 和txt3.txt 都在file_change.erl同级目录


