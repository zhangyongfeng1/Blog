---
title: javaScript_ES 6 简介
date:  2019-05-09 12:00:00
tags: [javascript,ES6]
categories: 张永枫
description: javaScript_ES 6 简介
---

    ES 6 是JavaScript语言的新一代标准，加入了很多新的功能和语法。React 的项目一般都是用ES 6 语法来写的，这也是是Facebook官方推荐的方式。

#### 1. let、const
    
let 和 const 是ES6 中新增的两个关键字，用来声明变量，let 和 const都是块级作用域。let声明的变量只在let命令所在的代码块内有效。const声明一个只读的常量，一量声明，常量的值就不能改变。例如：
    
```
// let 示例
{
    var a = 1;
    let b = 2;
}
console.log(a);//1
console.log(b);//ReferenceError: b is not defined.

//const 示例
const c = 3;
c = 4;//TypeError:Assignment to constant variable.
```
#### 2. 箭头函数
ES 6允许使用“箭头”（=>）定义函数。这种方式创建的函数不需要function 关键字，并且还可以省略return 关键字。同时，箭头函数内的this 指向函数定义所在的上下文对象，而不是函数执行时的上下文对象，例如：

```
var f = a => a + 1;
//等价于
var f = function(a){
    return a + 1;
}

function foo(){
    this.bar = 1;
    this.f = (a) => a + this.bar;
}

//等价于
function foo(){
    this.bar = 1;
    this.f = (function(a){
        return a + this.bar
    }).bind(this);
}
```
如果箭头函数的参数多于1个或者不需要参数，就需要使用一个圆括号代表参数部分。例如：

```
var f = () =>1;
vaf f= (a, b) => a + b;
```
如果函数体内包含的语句多于一条，就需要使用大括号将函数括起来，使用return语名返回。例如：
```
var f = (x,y) =>{
    x++;
    y--;
    return x + y;
}
```
#### 3. 模板字符串
模板字符串是增强版的字符串，用反引号(`)标识字符串。除了可以当作普通字符串使用外，它还可以用来定义多行字符串，以及在字符串中嵌入变量，功能很强大。例如：
```
//普通字符串
`React is wonderful !`

//多行字符串
`JS is wonderful 1
React is wonderful!`

//字符串中嵌入变量
var name = "React";
`Hello, ${name} !`;
```
#### 4. 解构赋值
ES 6 允许按照一定模式从数组和对象中提取，对变量进行赋值，这被称为解构。例如：
```
//数组解构
let [a,b,c] = [1,2,3];
a //1
b //2
c //3

//对象解构
let name = 'Lily';
let age = 4;
let person = {name, age};
console.log(person);//Object {name: "Lily", age: 4}

//对象解构的另一种形式
let person = {name: "Lily",age: 4};
let {name,age} = person;
console.log(name);//"Lily"
console.log(age);//4

函数的参数也可以使用解构赋值。例如:

//数组参数解构
function sum ([x, y]){
    return x + y;
}
sum([1, 2]);//3

//对象参数解构
function sum ({x, y}){
    return x + y;
}
sum({x:1,y:2});//3

//解构同样适用于嵌套结构的数组或对象。例如：
//嵌套结构的数组解构

let [a, [b], c] = [1, [2], 3];
a; //1
b; //2
c; //3

//嵌套结构的对象解构
let {person:{name, age}, foo} = {person:{name:'Lily',age: 4},foo:"foo"}
console.log(name);
console.log(4);
console.log(foo);
```
#### 5. rest参数
ES 6 引入rest（形式为...变量名）用于获取函数的多余参数，以代替argments 对象的使用。rest参数是一个数组，数组中的元素是多余的参数。注意，rest 参数之后不能再有其他参数 例如：
```
function languages(lang, ...types){
    console.log(types);
}
languages("js","java","python");//['java','python']
```
#### 6. 扩展运算符
扩展运算符是三个点(...),它将一个数组转为用逗号分隔的参数序列，类似于rest参数的逆运算。例如：
```
function sum(a, b, c){
    return a + b + c;
}
let numbers = [1, 2, 3];
sum(...numbers);//6

扩展运算符还常用于合并数组以及与解构赋值结合使用，例如：
//合并数组
let arr1 = ['a'];
let arr2 = ['b', 'c'];
let arr3 = ['d', 'e'];

[...arr1, ...arr2, ...arr3];

//与解构赋值结合
let [a, ...rest] = ['a', 'b', 'c'];
rest //['b', 'c']
扩展运算符还可以用于取出参数对象的所有可遍历属性，复制到当前对象之中。例如：
let bar = {a: 1, b: 2};
let foo = {...bar};
foo //Object {a: 1, b: 2};
foo === bar //false
```
#### 7. class
ES 6 引入了class(类)这个概念，新的class写法让对象原型的写法更加清晰，也更像传统的面向对象编程语言的写法。例如:
```
//定义一个类
class Person {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
    
    getName(){
        return this.name;
    }
    
    getAge(){
        return this.age;
    }
}
//根据类创建对象
let person = new('Lily', 4);
//class 之间可以通过extends关键字实现继承，例如：
class Man extends Person {
    constructor(name, age){
        super(name, age);
    }
    
    getGender(){
        return 'male';
    }
}
let man = new Man('Jack', 20);

```
#### 8. import、export
ES 6 实现了自已的模块化标准，ES 6 模块功能主要由两个关键字构成：export 和import。export 用于规定模块对外暴露的接口，import用于引入其他模块提供的接口。例如：
```
// a.js 导出默认接口和普通接口
const foo = () => "foo";
const bar = () => "bar";

export default foo //导出默认接口
export {bar} //导出普通接口

//b.js（与a.js 在同一目录下），导入a.js中的接口
//注意默认接口和普通接口导入写法的区别
import foo, {bar} from './a';
foo(); //"foo"
bar(); //"bar"
```
---
参考文献：《React 进阶之路》 

THE END

---