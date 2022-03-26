---
title: JavaScript数据类型判断
author: 闲花
img: "https://files.islu.cn/article/JavaScriptIsVar"
top: false
toc: true
mathjax: false
categories: JavaScript
tags:
  - JavaScript
  - JavaScript数据类型判断
keywords: "JavaScript数据类型判断,JavaScript,数据类型判断"
summary: JavaScript数据类型判断
abbrlink: 50959
date: 2021-09-04 13:42:25
update: 2021-09-04 13:42:25
---

# JavaScript 数据类型判断

## 1. typeof

使用 typeof 判断数据类型

```javascript
console.log(typeof 1); //number

console.log(typeof NaN); //number

console.log(typeof "1"); //string

console.log(typeof true); //boolean

let s = Symbol();
console.log(typeof s); //Symbol

console.log(typeof undefined); //undefined

function islu() {
  console.log("this is a function!");
}
console.log(typeof islu); //function

let obj = {
  name: "闲花手札",
};
console.log(typeof obj); //object

console.log(typeof null); //object

let array = [0, 1, 2, 3]; //数组
console.log(typeof array); //object
```

> 1. 使用 typeof 可以检测大部分的基本类型。但无法检测出来 null，会认为是对象。
> 2. NaN 也会认为是 number。
> 3. 可以检测出函数，但是对象数组和对象无法区分。

## 2. instanceof

instanceof 可以用来判断对象是否是某个类的实例。instanceof 的实现原理出门左转查看**手撕 instanceof**

简单说就是左边对象的原型(通过`.__proto__`访问)是否和右边对象的原型相等（通过`.prototype`访问），如果相等则返回 true。

```javascript
var arr = [1, 2, 3];
var date = new Date();
var fn = function () {
  alert(123);
};
console.log(arr instanceof Array);
console.log(date instanceof Date);
console.log(fn instanceof Function);
console.log(Function instanceof Object);
console.log(Object instanceof Function);
```

再来看另外一种情况:

在 a.html 中定义了数组 a:

```html
// a.html
<script>
  var a = [1, 2, 3];
</script>
```

然后通过 iframe 引入 main.html 页面：

```html
// main.html
<iframe src="a.html"></iframe>

<script>
  var frame = window.frames[0];
  var a = frame.a;
  console.log(a instanceof Array); // false
  console.log(a.constructor === Array); //false
  console.log(a instanceof frame.Array); // true
</script>
```

在 main.html 页面通过 iframe 获取到 a 页面的数组检测，发现 a 不是 Array 的实例对象，这是什么原因呢？

其实 iframe 之间不会共享原型链, 因为他们有独立的执行环境, 所以 frame a 中的数组 a 不会是本执行环境的实例对象.

## 3. constructor

使用构造函数判断类型：

```javascript
var bool = true;
var num = 123;
var str = "Davie";
var arr = [1, 2, 3];
var obj = { name: "Davie" };
var fun = function () {};
var sy = Symbol("Davie");

function Person() {}
function Student() {
  Person.call(this);
}
var stu = new Student();

console.log(bool.constructor === Boolean); // true

console.log(num.constructor === Number); // true

console.log(str.constructor === String); // true

console.log(arr.constructor === Array); // true

console.log(obj.constructor === Object); // true

console.log(fun.constructor === Function); // true

console.log(sy.constructor === Symbol); // true

console.log(stu.constructor === Student); // true

console.log(stu.constructor === Person); // false
```

- undefined 和 null 没有 contructor 属性,所以 constructor 不能判断 undefined 和 null
- 使用 constructor 判断类型是不安全的，因为 contructor 的指向是可以改变的

```javascript
arr.constructor = Object;
console.log(arr.constructor === Object); // true
```

## 4. 特性嗅探

或者一些特有的方法，比如数组特有的 sort，slice 等：

```javascript
console.log(typeof arr.sort === "function");
```

但是这种方式也不是特别牢靠，因为很难保证其他对象里面没有这些方法。

## 5. 万能方法

在任何值上调用 Object 原生的 toString() 方法，都会返回一个 [object NativeConstructorName] 格式的字符串。
**需要注意的是，它不能检测非原生构造函数的构造函数名。**

```javascript
function foo() {}
var div = document.createElement("div");

Object.prototype.toString.call(1);
("[object Number]");

Object.prototype.toString.call(NaN);
("[object Number]");

Object.prototype.toString.call("1");
("[object String]");

Object.prototype.toString.call(true);
("[object Boolean]");

Object.prototype.toString.call(undefined);
("[object Undefined]");

Object.prototype.toString.call(null);
("[object Null]");

Object.prototype.toString.call(Symbol());
("[object Symbol]");

Object.prototype.toString.call(foo);
("[object Function]");

Object.prototype.toString.call([1, 2, 3]);
("[object Array]");

Object.prototype.toString.call({});
("[object Object]");

Object.prototype.toString.call(/\d+/);
("[object RegExp]");

Object.prototype.toString.call(div);
("[object HTMLDivElement]");

Object.prototype.toString.call(
  (function () {
    return arguments;
  })()
);
("[object Arguments]");

Object.prototype.toString.call(new Error()); // => "[object Error]"

Object.prototype.toString.call(new Date()); // => "[object Date]"
```

从上面的例子可以看到，Object.prototype.toString 方法能有效弥补 typeof 不能很好区分**数组**、**对象**和**函数**的短板。

每个类在内部都有一个 [[Class]] 属性，这个属性中就指定了上述字符串中的构造函数名。

Object.prototype.toString 的原理是当调用的时候, 就取值内部的 [[Class]] 属性值, 然后拼接成 '[object ' + [[Class]] + ']' 这样的字符串并返回. 然后我们使用 call 方法来获取任何值的数据类型。

## 6. 检测函数

**Array.isArray()**

用于确定传递的值是否是一个 Array。如果对象是 Array，则返回 true，否则为 false。

```javascript
Array.isArray([1, 2, 3]);
```

**判断是否是 DOM 元素**

在实际项目里面, 有时或许我们需要判断是否是 DOM 元素对象, 那么在判断的时候利用的是 DOM 对象特有的 nodeType 属性:

```javascript
isElement: function(obj){  return !!(obj && obj.nodeType === 1);}
```

**判断是否是对象**

```javascript
isObject: function(obj){  var type = typeof obj;  return type === 'function' || typeof === 'object' && obj !== null;}
```

这里的对象是狭义的, 是通常所指的 key-value 型的集合, 或者是 function 函数并且不为 null.

**判断是否是 arguments 对象**

判断一个对象是不是 arguments 对象可以通过 Object.prototype.toString 来判断, 但是低版本的浏览器不支持, 他们返回的是 [object Object], 所以需要兼容:

```javascript
isArguments: function(obj){  return Object.prototype.toString.call(obj) === '[object Arguments]' || (obj != null && Object.hasOwnProperty.call(obj, 'callee'));}
```

兼容做法原理是通过对象的 hasOwnProperty 方法来判断对象是否拥有 callee 属性从而判断是不是 arguments 对象.

**isNaN()和 Number.isNaN**

isNaN 函数可以检测某个值是否是 NaN：

```javascript
isNaN(NaN); // true
```

但是：

```javascript
isNaN(undefined); // trueisNaN({}); // trueisNaN([]); // false
```

只要传入的参数不是数字，都会返回 true,但是数组会返回 false，所以任然无法很好进行区分。

ES6 为了修正这个 BUG，引入了 Number.isNaN()

```javascript
Number.isNaN(NaN); // true

Number.isNaN("A String"); // false

Number.isNaN(undefined); // false

Number.isNaN({}); // false

Number.isNaN(1); // false

Number.isNaN([]); // false
```

没有 ES6 的情况下，可以采用以下 polyfill

```javascript
if (!Number.isNaN) {
  Number.isNaN = function (n) {
    return typeof n === "number" && window.isNaN(n);
  };
}
```
