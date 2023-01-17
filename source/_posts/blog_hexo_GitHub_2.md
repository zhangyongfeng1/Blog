---
title: 利用hexo和GitHub搭建属于自己的个人静态网站
date: 2023-01-12 10:05:00
tags: [hexo,GitHub]
categories: [张永枫]
description: 搭建静态网站参考教程
---

## 一.Hexo简介

[hexo](https://github.com/hexojs/hexo) 是一款基于Node.js的静态博客框架，依赖少，易于安装使用，可以方便的生成静态网页托管在GitHub上，是搭建博额的首选框架。
这个是 [Hexo官网 https://hexo.io/zh-cn](https://hexo.io/zh-cn)

## 二.准备工作--hexo框架的搭建
### 需要的东西
- 1.要有一个github账号
- 2.要安装node.js,npm 依赖
- 3.安装git工具

### 安装git
[git 官网 https://gitforwindows.org](https://gitforwindows.org)

### 安装nodejs
[nodejs官网 https://nodejs.org/en/download/](https://nodejs.org/en/download/)


``` bash
node -v // 检查node版本
npm -v  // 检查npm版本
```

## 三.安装 hexo 环境。

安装好 Nodejs 后，就可以安装 hexo 框架了。

- 1.首先新建一个文件夹（涉及到代码的文件夹，请大家务必不要用中文），用于存放 hexo 框架，我这边以 `D:\work\hexo` 为例。

- 2.打开 CMD 命令窗口，cd 进入 `hexo` 文件夹，输入以下命令安装 hexo ：

``` bash
npm install hexo-cli -g
```

- 3.安装完成后，输入以下命令生成博客工程（文件夹），这边工程先命名为 `blog` ：

``` bash
hexo init blog
```

- 4.进入工程 `blog` 文件夹：

``` bash
cd blog
```

## 四.初始化

安装完成后，可以看到 `blog` 目录下有一堆文件和文件夹，

![项目目录结构](/img/zyf_img/blog2.png)

其中：

- node_modules 依赖包
- public 文件夹中存放自动生成的网站代码
- scaffolds 生成文章的一些模板
- source 用于放 MarkDown 写的文章文档；
- themes 是存放博客主题的文件夹；
- _config.yml 博客的配置文件

知道这些就可以开始写博客了，可以看到 `\source\_posts` 下有一个默认的文档 helloworld ，就是一篇默认的博客。

- 1.新建一篇博客，在 `D:\work\hexo\blog` 目录下，输入以下命令会在 `D:\work\hexo\blog\source\_posts` 中生成一个 .md 后缀的 MarkDown 文件：

``` bash
hexo new "文章标题"
```

格式
```
- title: postName #文章页面上的显示名称，一般是中文
- date: 2019-08-14 22:30:16 #文章生成时间，一般不改，当然也可以任意修改
- categories: 默认分类 #分类
- tags: [tag1, tag2, tag3] #文章标签，可空，多标签请用格式，注意逗号后面有个空格
- description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面 
```
- 2.在生成的文件中写博客，一般的文本编辑器都可以编写 MarkDown 文档；
- 3.写完博客后，输入以下命令就可以在 `public` 目录下，自动生成静态的博客网站代码：

``` bash
hexo generate
或
hexo g
```
- 4.这时候启动本地服务，就可以预览网站（ http://localhost:4000/ ）效果了，启动服务命令：

``` bash
hexo server
或
hexo s
```
## 五 生成SSH添加到GitHub
```
git config --global user.name 'yourname'

git config --global user.email 'youremail'
```
这里的yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱。这样GitHub才能知道你是不
是对应它的账户。

检查
```
git config user.name
git confit user.email
```

![git配置](/img/zyf_img/blog3.png)

### 创建SSH
生成公私钥
```
ssh-keygen -t res -C "503977995@qq.com"
```
进入.ssh文件夹

```
cd /Users/Macx/.ssh
```

ssh，简单来讲，就是一个秘钥，其中，id_rsa是你这台电脑的私人秘钥，不能给别人看的，id_rsa.pub是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。

而后在GitHub的setting中，找到SSH keys的设置选项，点击New SSH key
把你的id_rsa.pub里面的信息复制进去。
![git配置](/img/zyf_img/blog4.png)


## 六.将hexo部署到GitHub

现在，我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 _config.yml，翻到最后，修改为
```
deploy:  

    type: git  

    repo: https://github.com/YourgithubName/YourgithubName.github.io.git  

    branch: master
```
YourgithubName就是你的GitHub账户

这个时候需要先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。
```
npm install hexo-deployer-git --save 然后执行命令

hexo clean

hexo generate

hexo deploy
```
其中 hexo clean清除了你之前生成的东西，也可以不加。

hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写

hexo deploy 部署文章，可以用hexo d缩写

注意deploy时可能要你输入username和password



## 写在后面
引用网络博客内容：
https://www.bilibili.com/read/cv14867895    

