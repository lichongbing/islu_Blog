---
title: JavaScript基础
author: 闲花
img: "https://files.islu.cn/article/JavaScript.jfif"
top: false
toc: true
mathjax: true
summary: JavaScript基础笔记
categories: JavaScript
tags:
  - JavaScript
abbrlink: 53226
keywords: js,JS,JavaScript,JS基础笔记,JavaScript笔记,JavaScript特点
date: 2020-09-18 09:25:00
update: 2020-09-18 09:25:00
---

# JavaScript 基础

## JavaScript 特点

1. 用于完成 html 网页交互
2. 脚本语言
3. 弱类型的
4. 客户端的脚本
5. 解释性的，边解释边执行
6. 区分大小写

## JavaScript 组成

ECMAScript、浏览器对象模型(BOM)、文档对象模型(DOM)

## 网页上引入 js 脚本三种形式

#### 1. 网页内部使用

`<script>`标签添加---->`<body></body>`后面

```html
<script>
	//js代码
<script>
```

#### 2. 引入外部 js 脚本

1.  添加 JavaScript 文件，在里面编写代码
2.  在 html 页面中添加标签,引入外部文件
    `<script type="text/javascript" src="要引入文件的相对路径" ></script>`

#### 3. 在网页标签元素的属性中添加

`<input type="button" name="btn" value="请点击" onclick="alert('hello world!!!')"/>`

#### 三种引入 JavaScript 脚本的方式分别适合在什么时候用呢？

- 如果在标签属性中添加，只能作用于本标签，不能实现效果的重用
- 如果在页面内部通过 Script 标签引入，可以实现本页面的效果共享
- 引入外部 js 文件，可以实现页面间的代码共享，保证网页结构代码和效果代码相分离

## 标识符

变量名，函数名，属性以及函数中的参数都属于标识符

### 命名规则

1. 只能包含数字，字母，下划线和$ ，但是不能以数字开头
2. 不能包含其他符号
3. 不能和 js 中关键字，保留字冲突

## JavaScript 注释

- 单行  //
  `//注释内容`
- 多行注释  /\_ \_/
  `/*注释内容*/`

## 系统弹框

1.  `alert("");`   警示框
2.  `confirm("");`   确认框,包含确认,取消按钮

```javascript
var n = confirm("-----？"); //得到的值是布尔类型的
if (n) {
  //点击了确定
} else {
  //点击了取消
}
```

3.  可以让用户输入的提示框

```javascript
var 变量名 = prompt("提示给用户的信息", "默认值");
```

- 用户点击确定，能够返回用户输入的值
- 用户点击取消，返回的值是 null

## JavaScript 下载解析

- head:   先下载 js 脚本，再显示页面----》当网络不好时，用户只能看到空白页面并且一直等待网页显示
- body: 先显示网页内容，然后遇到 js 脚本时再下载解析---》当网络不好时，用户可以先看到没有效果的页面
- body 后面  html2.0 不支持
  为了优化加载速度大多使用异步加载(放在 body 后面)，先加载页面后实现效果

## 变量与数据类型

- console.log("");   向控制台输出一句话（浏览器的控制台，f12 可以打开）多用于程序调试，观察变量的值
- javaScript 是弱类型的，松散型的

### 变量

1.  声明

- var 关键字声明变量
  - 变量声明
    - var 变量名；
    - 同时定义多个变量： var 变量名 1,变量名 2,....;
  - 变量赋值：
    - var 变量名=值；
    - 同时定义多个变量赋值： var 变量名 1=值,变量名 2=值,....;
- let 关键字定义变量
  - let 定义的变量，只能在定义的代码块中使用

```javascript
if (true) {
  let a = 1;
  var b = 2;
  document.write("a=" + a + "<br/>"); //可以输出
}
document.write("a=" + a + "<br/>"); //提示变量尚未定义
document.write("b=" + b); //可以正常输出
```

      -  let不存在变量提升(var存在变量提升)---->必须声明赋值之后才能使用

```javascript
console.log("name" + name); //不会报错
console.log("age" + age); //变量尚未定义
var name = "张三";
let age = 18;
```

      -  let 定义的变量会有暂时性死区

```javascript
let num1 = 10;
if (true) {
  let num1 = 20;
}
console.log("num1=" + num1); //此处输出10
```

      -  不允许重复的声明变量(在相同作用域中)

```javascript
let a = 1;
let a = 10; //报错
```

2.  赋值
    JavaScript 语言是弱类型的
1.  先声明再赋值
1.  不用声明直接赋值  x=10;//ok
1.  常量
    使用 const 关键字
    语法:`const PI=3.14;`
    注意：

- 常量值是只读的，不能修改
- 和 let 的作用域是一样的

### 数据类型

#### undefined

表示:变量声明了，但是没有初始化

```javascript
var x; //声明但是没有初始化
console.log(x); //undefined
console.log(y); //没有定义   y is not defined
```

注意：变量未初始化和变量没有定义是不同的概念

#### null

表示空的值

跟 undefined 的区别是：undefined 变量定义了 但是跟本就没有赋值

```javascript
如:var x; 此时x的值就是undefined
null，变量定义了，有值，并且是值就是null

如:var z=null;  一般用于对象的初始值
```

#### String 字符串

语法:定义 时可以用“” 或者'  '，但是前后必须匹配

```javascript
var str1 = "bbb";
var str2 = " aaa";
```

注意：

- 字符串的值不能更改
- toString()方法，可以将   数值，对象，布尔，字符串 转换成字符串
  可以使用 String()来进行判断一个变量的值是否为 null 或 undefined

```javascript
var num=100;
console.log(num.toString());//以十进制的形式转换成字符串
console.log(num.toString(2));//以二进制的形式转换成字符串
console.log(num.toString(8));//以八进制的形式转换成字符串
console.log(num.toString(16));//以十六进制的形式转换成字符串
注意：null和undefined 不能调用这个方法,会报错
```

- String（）函数
  可以将任意类型转换成 String 字符串，包括 null 和 undefined

#### number

可以存储任何数字，整型和浮点型

```javascript
var n1 = 100;
var n2 = 90.99;
```

注意:浮点数值的最高精度是 17 位小数，但在进行算数计算时其精确度远远不如整型。

#### 特殊值和方法

- infinity  :当大于或小于某个界限时，该值会被自动转换为特殊值——Infinity。
- isFinite()函数可以判断一个数值是否无穷大。
  - 它会把参数转换为数值，如果得到的结果是 NaN、Infinity 或-Infinity，函数返回 false（假），其他情况返回 true（真）。
- NaN:非数值（Not a Number）
  - 任何涉及 NaN 的操作（例如 NaN/5）都会返回 NaN。
  - NaN 与任何值都不相等，包括 NaN 本身
- isNaN():检测一个值是否为 NaN
  规则:
  - isNaN 方法会把参数转换为数值，若不能转换为数值则函数返回 false。
  - 任何不能被转换为数值的值都会导致这个函数返回 true。
- parseInt()   解析字符串并返回一个整数或 NaN,可以解析二进制，八进制和十六进制的数值.
- parseFloat():解析字符串并返回一个浮点数
  - parseFloat()函数始终都会忽略前导的零，且不具备传入基数的能力

#### Boolean

值: true false

转型函数 Boolean()

规则:

1. String 类型：任何非空字符串转换为 true，空字符串（""）转换为 false；
2. Number 类型：任何非零数值（包括无穷大）转换为 true，0 和 NaN 转换为 false；

#### Object 类型

任何对象转换为 true，null 转换为 false；

注意:当遇到流程控制语句（如 if 语句）也会对数据自动执行相应的 Boolean 转换

#### typeof

来判断一个值或变量究竟属于哪种数据类型。

typeof 操作符返回的数据类型有以下几种：

- undefined
- boolean
- string
- number
- object
- function

## 运算符

表达式:JavaScript 中短语,包括变量,字面量和运算符，简单表达式可以使用运算符组合成复杂表达式

### 一元运算符

只有一个操作数

`如:a++ a-- ++b --b`

**注意:在 javascript 可以对任何值使用, 包括字符串,布尔值,浮点值和对象**

```javascript
var a = "89";
a++; //90，数值字符串自动转换成数值
var b = "ab";
b++; //NaN，字符串包含非数值转成NaN
var c = false;
c++; //1，false转成数值是0，累加就是1
var d = 2.3;
d++; //3.3，直接加1
```

执行顺序

- ++i:先自增再运算
  - i=i+1
  - 其他
- i++;先运算再自增
  - 其他运算
  - i=i+1

### 算术运算符

1.  加法
    运算:
1.  求和
1.  连接(跟字符串运算)
1.  注意:NAN 和任何类型运算都是 NAN

```javascript
var result1 = 1 + 2; //3
var result2 = 1 + NaN; //NaN												var result3 = 100 + "100";  //100100
var result4 = "10+20=" + 10 + 20; //10+20=1020
var result5 = "10+20=" + (10 + 20); //10+20=30
var result6 = 10 + 20 + "=10+20"; //30=10+20
```

2.  减法
    求差时遇到字符串,布尔类型,NAN,null 等非数字类型时,先按规则转换成数字,再进行减法运算

```javascript
var result1 = 5 - true; //4,因为true被转换成了1
var result2 = NaN - 1; //NaN
var result3 = 5 - 3; //2
var result4 = 5 - ""; //5,因为""被转换成了0
var result5 = 5 - "2"; //3,因为"2"被转换成了2
var result6 = 5 - null; //5,因为null被转换成了0
```

3.  乘法
    求积时遇到字符串,布尔类型,NAN,null 等非数字类型时,先按规则转换成数字,再进行减法运算

```javascript
var result1 = 100 * 70; //7000
var result2 = 100 * NaN; //NaN,只要有一个操作数为NaN即为NaN
var result3 = 100 * true; //100,因为true被转换成了1
var result4 = 100 * ""; //0,因为""被转换成了0
var result5 = 100 * "70"; //7000,因为"70"被转换成了70
var result6 = 100 * null; //0,因为null被转换成了0
var result7 = 100 * "hello"; //NaN,因为"hello"被转换成了NaN
```

4.  除法
    运算符由斜杠符号（/）表示,遇到非数字类型时先转换为数字再运算

```javascript
var result1 = 100 / 50; // 2
var result2 = 100 / NaN; //NaN,只要有一个操作数为NaN即为NaN
var result3 = 100 / true; //100,因为true被转换成了1
var result4 = 100 / ""; //Infinity,因为""被转换成了0
var result5 = 100 / "50"; //2,因为"50"被转换成了50
var result6 = 100 / null; //Infinity,因为null被转换成了0
var result7 = 100 / "hello"; //NaN,因为"hello"被转换成了NaN
```

5.  取模(求余)
    %--à 求余数

### 关系运算符

`相等（==）、不相等（!=）、全等（===）和不全等（!==）`

- == 和 === 的区别
  - ==会进行类型转换
  - ===不会转换类型
- 运算规则
  - 如果操作数都是数值，则按照数值比较
  - 如果两个操作数都是字符串，则比较两个字符对应的字符编码值
  - 如果一个操作数是数值，则将另一个操作数转换为数值，然后进行数值比较
  - 如果一个操作数是一个布尔值，则先将其转换为数值，然后再执行比较

### 逻辑运算符

1.  &&(并且)
    两边不全是 boolean 类型
1.  第一个表达式转换为 false,最终的结果为第一个操作数
1.  第一个表达式转换为 true,最终的结果为第二个操作数
1.  || (或者)

两边不全是 boolean 类型

1. 第一个表达式转换为 false,最终的结果为第二个操作数
2. 第一个表达式转换为 true,最终的结果为第一个操作数

```javascript
console.log(Boolean("1234")); //true 非空字符串
console.log(Boolean("")); //false  空字符串

console.log(Boolean(0)); // false  0
console.log(Boolean(8888)); //true  非0

console.log(Boolean(null)); // false 对象是null
console.log(Boolean(new Date())); //  true 对象不是空

console.log(Boolean(NaN)); //false

console.log(Boolean(undefined)); //false
```

### 赋值运算符

右边赋值给左边`+= -= *= /= %=`

## 函数

### 定义调用

- 方式一

```javascript
定义:
	function 函数名(形参1,形参2,形参3,...){

	}
调用:
	函数名(实参1,实参2,实参3,...);//通过函数名调用
```

- 方式二

```javascript
定义:
	函数定义表达式:(定义的函数是匿名函数,赋值给了一个变量)
	var 变量名=function (形参1,形参2,形参3,...){
调用: 	  			 }
   	变量名(实参1,实参2,实参3,...);//通过变量名调用
```

### 函数的参数

1. 定义函数是传入的参数是形参
2. 调用函数时传入的参数是实参
3. 形参和实参没有必然联系,形参只是占位符,并且方便函数内使用
4. javaScript 中,形参和实参的个数可以不一致,但是注意 java 中必须保持一致
5. 获取参数的方式:argument 对象
   - argument[0]:获得调用函数时传入的第一个实参
   - argument[1]:获得调用函数时传入的第二个实参...以此类推
   - argument.length 属性可以获得实参个数

例子:求最大值

```javascript
function getMax() {
  var max = arguments[0];
  for (let i = 0; i < arguments.length; i++) {
    if (max < arguments[i]) {
      max = arguments[i];
    }
  }
  alert("最大值是" + max);
}
getMax(10, 20, 40, 50, 60, 90, 200, 23);
```

### 函数返回值

```javascript
function 函数名(形参) {
  return 返回值;
}
var 变量 = 函数名(实参); //调用函数之后,返回值保存在变量里面
//可以返回任何类型的值,包括函数
```

### 变量作用域

- 全局作用域
- 局部作用域
  如:在函数中定义的变量局部作用域
- 注意:如果在函数内部定义变量没有用 var 声明,直接赋值,那么将是一个全局变量
  - 全局变量声明了之后,在程序的各个部分都可以使用,包括在函数里面
  - 但是在函数内定义的局部变量,只能在函数内部使用

### 作用域链

在函数内部没有定义,就会在上一级作用域里面找

由内向外的作用域中寻找变量，直到找到为止

如果找到全局作用域也没找到，那么该变量的值为 undefined

### 闭包

可以读取一个函数内部变量函数

因为变量作用域的关系，导致内部可以读取全局变量，但是外部却不能访问内部变量

- 如何能从外部读取内部变量？
  可以在函数内部再定义一个函数

```javascript
function f1() {
  var n = 999;
  function f2() {
    alert(n); //99	在f2函数里面访问了f1内部的局部变量
  }
  return f2; //JavaScript返回值可以返回任何数据类型，包括函数
}
var rel = f1(); //调用f1并接收返回值
rel(); //做到了在函数外部访问内部的局部变量
```

- 作用
  - 读取到函数内部的变量
  - 函数内部变量的作用范围扩大，常驻内存不会被回收

不用太纠结到底怎样才算闭包，其实我们每一个写的函数都是一个简单的闭包

### 立即执行函数

把函数的定义和调用合在一起

```javascript
(function () {
  alert("a");
})();
```

### 块级作用域与函数的声明

ES6 之前 函数不能声明在块级作用域里的，函数的声明是会全部提升至顶部

ES6 块级作用域里可以声明函数，但是函数声明的行为类似于 let，在块级外部是不能访问的

```javascript
if(){

}
```

现如今:

1. 允许在块级中声明函数】
2. 函数的生命类似于 var,会有提升
3. 函数的生命是会提升至头部

### 函数参数的默认值

在 ES6 之后，允许为参数指定默认值

```javascript
function f1(x, y = 18) {
  console.log(x, y);
}
```

1.  不允许有同名参数

```javascript
function f2(x, x, y = 18) {
  //报错
  console.log(x, x, y);
}
```

2.  参数默认值是不能传值，每次都重新计算表达式默认的值，惰性求值
3.  参数默认值的位置

- 一般来说，定义了默认值的参数，应该是尾参数，如果为非尾参数设置默认值，实际上并没有办法省略
- 如果不是尾参数，可以显示输入 undefined 但是 null 不行
