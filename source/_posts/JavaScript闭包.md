---
title: JavaScript闭包
author: 闲花
img: "https://files.islu.cn/article/JavaScript%E9%97%AD%E5%8C%85"
top: false
toc: true
mathjax: false
essay: true
categories: JavaScript
tags:
  - JavaScript
  - JavaScript闭包
keywords: "JavaScript,闭包,JavaScript闭包"
summary: JavaScript闭包，词法作用域及性能问题
abbrlink: 58738
date: 2021-11-14 16:02:19
update: 2021-11-14 16:02:19
---

​

# 闭包

​

## 1. 什么是闭包

​

先来说下概念：
​

> 一个函数和对其周围状态（**lexical environment，词法环境**）的引用捆绑在一起（或者说函数被引用包围），这样的组合就是**闭包**（**closure**）。也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用域。在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。
> ​

​

​

## 2. 词法作用域

​

说到闭包，必须要说下作用域，看下面代码 👇：
​

```javascript
function init() {
  var name = "Davie"; // name 是一个被 init 创建的局部变量
  function displayName() {
    // displayName() 是内部函数，一个闭包
    alert(name); // 使用了父函数中声明的变量
  }
  displayName();
}
init();
```

​

`init()` 创建了一个局部变量 `name` 和一个名为 `displayName()` 的函数。`displayName()` 是定义在 `init()` 里的内部函数，并且仅在 `init()` 函数体内可用。`displayName()` 没有自己的局部变量。然而，因为它可以访问到外部函数的变量，所以 `displayName()` 可以使用父函数 `init()` 中声明的变量 `name` 。
​

运行该代码后发现， `displayName()` 函数内的 `alert()` 语句成功显示出了变量 `name` 的值（该变量在其父函数中声明）。词法（lexical）一词指的是，**词法作用域根据源代码中声明变量的位置来确定该变量在何处可用**。嵌套函数可访问声明于它们外部作用域的变量。
​

重要的话说三遍：
​

**词法作用域根据源代码中声明变量的位置来确定该变量在何处可用**
​

**词法作用域根据源代码中声明变量的位置来确定该变量在何处可用**
​

**词法作用域根据源代码中声明变量的位置来确定该变量在何处可用**
​

一定是声明变量的位置，而不是调用的位置。
​

## 3. 闭包

​

再来看一段代码：
​

```javascript
function makeFunc() {
    var name = "Davie";
    function displayName() {
        alert(name);
    }
    return displayName;
}
var name = "大卫"
var myFunc = makeFunc();
​

myFunc();
```

​

代码运行结果是 “Davie”，`displayName`函数形成一个闭包，如果没有`displayName`函数，`makeFunc`函数执行完之后，name 属性就不能再被访问。而由于`displayName`的存在，维持了对`name`的引用，因此，当 `myFunc` 被调用时，变量 `name` 仍然可用。
​

另一个有趣的代码：
​

```javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}
​

var add5 = makeAdder(5);
var add10 = makeAdder(10);
​

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

​

`makeAdder`函数在执行完毕之后，参数`x`仍然存在，保留在内存中，当在此执行内部的闭包函数时，就可以被内部函数访问到。
​

​

​

## 4. 使用闭包实现模块化

​

在一些编程语言，比如 Java 中，是支持将方法声明为私有的，即它们只能被同一个类中的其它方法所调用。
​

而 JavaScript 没有这种原生支持（TypeScript 已经支持），但我们可以使用闭包来模拟私有方法。私有方法不仅仅有利于限制对代码的访问：还提供了管理全局命名空间的强大能力，避免非核心的方法弄乱了代码的公共接口部分。
​

下面的示例展现了如何使用闭包来定义公共函数，并令其可以访问私有函数和变量。这个方式也称为**模块模式**：
​

```javascript
var Counter = (function() {
  var _privateCounter = 0;
  function changeBy(val) {
    _privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return _privateCounter;
    }
  }
})();
​

console.log(Counter.value()); /* logs 0 */
Counter.increment();
Counter.increment();
console.log(Counter.value()); /* logs 2 */
Counter.decrement();
console.log(Counter.value()); /* logs 1 */
```

​

通过立即执行函数创建了一个模块。模块内部的两个变量`privateCounter`和`changeBy`都不能再外部访问到，于是提供了三个函数用于在外部访问。这三个公共函数是共享同一个环境的闭包。多亏 JavaScript 的词法作用域，它们都可以访问 `privateCounter` 变量和 `changeBy` 函数。
​

把上面的代码稍加改造，变成有名函数，通过执行这个函数得到多个计数器：
​

```JavaScript
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }
};
​

var Counter1 = makeCounter();
var Counter2 = makeCounter();
console.log(Counter1.value()); /* logs 0 */
Counter1.increment();
Counter1.increment();
console.log(Counter1.value()); /* logs 2 */
Counter1.decrement();
console.log(Counter1.value()); /* logs 1 */
console.log(Counter2.value()); /* logs 0 */
```

​

两个计数器 `Counter1` 和 `Counter2` 是如何维护它们各自的独立性的。每个闭包都是引用自己词法作用域内的变量 `privateCounter` 。
​

每次调用其中一个计数器时，通过改变这个变量的值，会改变这个闭包的词法环境。然而在一个闭包内对变量的修改，不会影响到另外一个闭包中的变量。
​

> 通过这种方式可以实现很多与面向对象编程相关的好处 —— 特别是数据隐藏和封装。
> ​

​

​

## 5. 一个常见错误

​

我们在开发中，经常会遇到一个问题就是通过循环的方式给元素添加事件：
​

```html
<p id="html">HTML</p>
<p id="css">CSS</p>
<p id="js">JavaScript</p>
```

​

需求是给每一个`p`标添加点击事件，当点击`p`标签时，使用`alert`弹出里面的文字内容：
​

通过 for 循环添加：
​

```javascript
 var list = document.getElementsByTagName('p')
​

 for(var i = 0;i < list.length;i++){
   var item = list[i]
   item.onclick = function(){
        alert(item.innerText)
    }
 }
```

​

如果这样写的话，执行代码会发现不管点击那个元素，弹出的始终是"JavaScript"。
​

原因是赋值给 onclick 的是闭包。这三个闭包在循环中被创建，但他们共享了同一个词法作用域，在这个作用域中存在一个变量 item。变量 item 使用 var 进行声明，由于变量提升，所以具有函数作用域。由于循环在事件触发之前早已执行完毕，变量对象`item`（被三个闭包所共享）的值已经变成了最后一个`p`。
​

解决这个问题的办法是使用工厂模式：
​

```javascript
 function showText(item){
   return function(){
     alert(item.innerText)
   }
 }
​

var list = document.getElementsByTagName('p')
​

for(var i = 0;i < list.length;i++){
  var item = list[i]
  item.onclick = showText(item)
}
```

​

所有的回调不再共享同一个环境， showText 函数为每一个回调创建一个新的词法环境。三个闭包中，三个 item 会被单独保存下来。
​

当然使用匿名函数也可以：
​

```javascript
var list = document.getElementsByTagName('p')
​

 for(var i = 0; i < list.length;i++){
   (function(){
     var item = list[i]
     item.onclick = function(){
       alert(item.innerText)
     }
   })()
 }
```

​

当然，使用 ES6 的 let 关键字就单间多了：
​

```javascript
for (var i = 0; i < list.length; i++) {
  let item = list[i];
  item.onclick = function () {
    alert(item.innerText);
  };
}
```

​

使用 let 定义 item，每个闭包都绑定了块作用域的变量，这意味着不再需要额外的闭包。
​

另外还有一种方法是使用 forEach 函数：
​

```javascript
// 使用forEach方法
new Array().forEach.call(list, (item) => {
  item.onclick = function () {
    alert(item.innerText);
  };
});
```

​

​

​

​

## 6. 性能问题

​

闭包虽然有很多好处，然而也要谨慎使用，由于闭包会保存变量，不会立即被垃圾回收机制处理，所以创建过多的闭包可能会造成内存泄漏。
​

例如，在创建新的对象或者类时，方法通常应该关联于对象的原型，而不是定义到对象的构造器中。原因是这将导致每次构造器被调用时，方法都会被重新赋值一次（也就是说，对于每个对象的创建，方法都会被重新赋值）。
​

```javascript
function Person(name, message) {
  this.name = name.toString();
  this.message = message.toString();

  this.getName = function() {
    return this.name;
  };
​

  this.getMessage = function() {
    return this.message;
  };
}
```

​

上面的代码中，我们并没有利用到闭包的好处，因此可以避免使用闭包。修改成如下：
​

```javascript
function Person(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
​

MyObject.prototype.getName = function() {
  return this.name;
};
​

MyObject.prototype.getMessage = function() {
  return this.message;
};
```

​

1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在 IE 中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
2. 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。
   ​

​

​

## 7. 总结

​

闭包是能够读取另一个函数作用域的变量的函数。
​

闭包具有：封闭性、持久性的有点。
​

同时又由于持久性，处理不当易造成内存泄漏。
​
