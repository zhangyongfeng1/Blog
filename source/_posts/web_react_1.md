---
title: React 开发环境及工具介绍
date:  2019-05-10 12:00:00
tags: [javascript,react,node,npm]
categories: 张永枫
description: React 开发环境及工具介绍
---

### 基础环境

#### Node.js
React 应用的执行并不依赖Node.js环境，但React 应用开发编译过程中用到的佷多依赖（例如NPM、Webpack等）都是需要Node.js环境的。所以有React应用前，需要先安装Node.js。Node.js的官方下载地址为 https://nodejs.org.

#### NPM
NPM 是一个模块管理工具，用来管理模块的发布、下载及模块之间的依赖关系。开发React应用时，需要依赖很多其他的模块，这些模块就可以通过NPM下载。NPM已经集成到Node.js的安装包中，所以不需要单独安装。另外，Facebook 联合Exponent、Google和Tilde 共同推出了另一个模块管理工具Yarn（https://yarnpkg.com）,可以作为NPM的替代工具。

### 辅助工具

#### Webpack
Webpack是用于现代JavaScript 应用程序的模块打包工具。Webpack会递归地构建一个包含应用程序所需的每个模块的依赖关系图，然后将所有的模块打包到少量文件中。Webpack不仅可以打包JS文件，配合相关插件的使用，它还可以打包图片资源和样式文件，已经具备了一站式的javaScript应用打包能力。Webpack本身就是一个模块，因此可以通过NPM等模块管理工具安装。

#### Babel
React 应用中会使用大量的ES 6 语法，但是目前的济鉴器环境并不完全支持ES 6 语法。Babel 是一个javaScript 编译器，它可以装ES6 及其以后的语法编译成ES 5的语法，从而让我们可以在开发过程中尽情使用最新的JavaScript语法，而不需要担心代码无法在浏器端运行的问题。Babel一般会和Webpack一起使用，在Webpack编译打包阶段，利用Babel插件将ES 6 及其以后的语法编译成ES 5语法。

#### ESLint
ESLint 是一个插件代的JavaScritp代码检测工具，它既可以用于检查常见的JavaScript语法的错误，又可以进行代码风格检查，从而保证团队内不同开发人员编写的代码能遵循统一的代码规范。使用ESlint必须指定一套代码规范，然后ESlint就会根据这套规范对代码进行检查。目前，业内比较好的规范是Airbnb的规范，但这套规范过于严格，并不一定适合所有团队。在实际使用中，可以先继承这套规范，然后在它的基础上根据实际需求对规范进行修改。

#### 代码编辑器

```
    Visuall Studio Code(VS code)
    Subline Text
    Atom 
    WebStorm
```
 
### Create React App （搭建脚手架）
Webpack、Babel等工具是开发React应用所必需的，但这些工具的使用方法比较烦琐，龙其是Webpack 的使用，需要大量篇幅才能介绍清楚。为了避免读者还没开始使用React,就被各种辅助工具的使用搞得“头晕目眩”，这本书借助React 官方提供的脚手架工程Create React App（https://github.com/facebookincubator/create-react-app）创建React应用。Create React App 基于最佳实践，将Webpack、Babel、ESlint等工具的配置做了封装，使用Create React App创建的项目无须进行任何配置工作，从而使开发者可以专注于应用开发。
#### 1、安装
打开命令行终端，依次输入以下命令：
```
    npm install -g create-react-app
```
通过使用 -g 参数，我们将create-react-app 安装到了系统的全局环境，这样就可以在任意中径下使用它了。
```
    sudo npm install -g create-react-app //(使用root权限安装)
```
#### 2、创建应用
使用create-react-app创建一个新应用，在命令行终端执行：
```
create-react-app my_app
```
这时会在当前路径下新建一个名为my_app的文件夹，my_app也就是我们新创建的React应用。

#### 3、运行应用
在命令行终端执行：
```
cd my_app
npm start
```
当应用启动成功后，在浏览器地址输入http://localhost:3000即可访问应用
生成的项目目录如下：

```

node_modules
public
    favicon.ico
    index.html
    manifest.json
src
    App.css
    App.js
    App.test.js
    index.css
    logo.svg
    serviceWorker.js
README.md
package.json
yarn.lock

```    

node_modules 文件夹内是安装的所有依赖模块;

package.json 文件定义了项目的基本信息，如项目名称、版本号、在该项目下可执行的命令以及项目的依赖模块等；

public 文件夹下的index.html是应用的入口页面；

src 文件夹是项目源代码，其中index.js 是代码入口。

index.js 导入了模块的App.js，修改App.js

保存文件后，可以发现浏览器页面实时进行了更新，这是因为Create React App也包含热加载功能，可实时更新代码变化。

---

react 中文官网：https://zh-hans.reactjs.org/

THE END

---