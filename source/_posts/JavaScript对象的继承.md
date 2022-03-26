---
title: JavaScript对象的继承
date: 2021-11-16 16:02:19
update: 2021-11-16 16:02:19
author: 闲花
img: "https://files.islu.cn/article/JavaScriptObject.webp"
top: false
toc: true
mathjax: false
essay: false
summary: JavaScript对象的继承关系
categories: JavaScript
tags:
  - JavaScript
  - JavaScript对象的继承
keywords: JavaScript对象的继承,对象的继承,JavaScript对象
abbrlink: 958434
---

# JavaScript 对象的继承

### 1. 原型链继承

基于原型链，即把一个对象的原型设置为另一个对象的实例，那么这个对象实例也就拥有了另一个对象上的属性。

````JavaScript
function Father(){
  this.nationality = "中国🇨🇳"
}
Father.prototype.getNational = function(){
  console.log('中国🇨🇳')
}

function Son(){ }

Son.prototype = new Father()

var s = new Son()

s.getNational() _//中国🇨🇳_
_```_
原型和实例的关系
```JavaScript
s instanceof Son _//true_
s instanceof Father _//true_
_```_
子类也可以继续添加其他的方法，但是需要注意，子类添加方法的代码要写在替换原型的代码之后
```JavaScript
function Father(){
  this.nationality = "中国🇨🇳"
}
Father.prototype.getNational = function(){
  console.log('中国🇨🇳')
}

function Son(){ }

Son.prototype = new Father()

_// 子类添加其他方法_
Son.prototype.learn = function(){
  console.log('好好学习天天向上')
}
````

### 2. 借用构造函数

使用父类的实例设置为子类的原型，也就意味着父类的属性变成了子类原型上共享的属性了。我们在之前将面向对象时，说过，对象的属性最好定义在构造函数中，需要共享的引用类型的属性再定义在原型上。为了解决这个问题，我们可以在子类的构造函数中调用父类的构造函数，这样父类的属性就会变成子类构造函数上的属性，子类的实例对象也就有了独立的属性：

```JavaScript
function Father() {
  this.nationality = "中国🇨🇳"
}

function Son() {
  _// 在子类的构造函数中调用父类构造函数_
  Father.call(this)
}
传递参数：
function Father(name) {
  this.name = name;
  this.nationality = "中国🇨🇳"
}

function Son(name) {
  // 在子类的构造函数中调用父类构造函数
  Father.call(this,name)
}
```

### 3. 组合继承模式

结合原型链和构造函数，原型链实现对原型属性和方法的基础，构造函数实现实例方法的继承：

```JavaScript
function Father(name) {
  this.name = name;
  this.nationality = "中国🇨🇳"
}

Father.prototype.getNational = function () {
  console.log('中国🇨🇳')
}

function Son(name) {
  _// 在子类的构造函数中调用父类构造函数_
  Father.call(this,name)
}

Son.prototype = new Father()

Son.prototype.constructor = Son;
```

**这种方法也是推荐的实现继承的方式**

### 4. 寄生式继承

```JavaScript
function createPerson(origin) {
  var clone = Object(origin)
  clone.sayHello = function () {
    console.log('hello')
  }
  return clone;
}

var person = {
  name: "davie",
  age: 20
}

var p2 = createPerson(person)
p2.sayHello()
```

createPerson 方法返回了一个新的对象，具有 person 的属性，而且还有自己的方法。
当继承的父对象不是自定义类型和构造函数的情况下，可以采用寄生继承模式。

### 5. 寄生组合式继承

组合继承模式是最常用的模式，但也不是完美的。组合继承会执行两次父类构造函数。一次是在子类构造函数中，一次在创建子类原型的时候。结合寄生模式，可以进一步优化：

```JavaScript
function _inherit(subClass,supClass){
  var prototype = Object(supClass.prototype)
  prototype.constructor = subClass
  subClass.prototype = prototype
}

function Father(name){
  this.name = name;
}
Father.prototype.sayHi = function(){
  console.log(this.name)
}

function Son(name,age){
  Father.call(this.name)
  this.age = age;
}

_inherit(Son,Father)
```

这种方法的高效之处体现在只调用了一次父类构造函数。因此避免了在子类的原型上添加不必要的、多余的属性。同时原型链还能保持不变，因此可以正常使用 instanceof 判断类型。

### 6. ES6 中类的继承

在 es6 中，有了 class(JavaScript 的 class 只是一种语法糖，覆盖在基于构造函数和原型的模式上)，我们就可以使用 extends 来实现类的继承了：

```JavaScript
class Father {
   constructor(name) {
     this.name = name
   }

   sayHi() {
     console.log(this.name)
   }
 }

class Son extends Father {
  constructor(name) {
    // 在子类中通过super函数调用父类构造函数
    super(name)
  }

  learn() {
    console.log('好好学习天天向上')
  }
}

var s = new Son("Davie")
s.sayHi()
s.sayHi()
```

子类的构造函数可以不写。但是如果要写的话，一定要记得执行 super 函数。super 函数用来调用父类的构造函数。否则会报错：

![error](https://files.islu.cn/article/202111161448.jpg)
