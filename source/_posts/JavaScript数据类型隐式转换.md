---
title: JavaScript数据类型隐式转换
author: 闲花
img: "https://files.islu.cn/article/JavaScriptShowAndHidden"
top: false
toc: true
mathjax: false
categories: JavaScript
tags:
  - JavaScript数据类型隐式转换
keywords: "JavaScript数据类型隐式转换,JavaScript,数据类型隐式转换"
summary: JavaScript数据类型隐式转换
abbrlink: 33904
date: 2021-09-05 21:23:09
update: 2021-09-05 21:23:09
---

# JavaScript 数据类型隐式转换

## 1. 面试题

在讲 JavaScript 的数据类型隐式转换前，我们先看道面试题：

```javascript
console.log(new String("abc") == true);

console.log({} == true);

console.log([] == ![]);
```

结果是什么呢？

先把结果写下来，放在一边，然后继续看

## 2. 字面量形式、包装器方式，new 方式的区别

创建字符串的三种方式：

```javascript
var a = "Davie"; //申明的是一个string类型，它是一个基本类型
var a = String("Davie"); // String()是一个包装类，用于将参数转换成string类型
var a = new String("Davie"); //采用new方式时创建了一个object类型
```

使用 typeof 验证上面的结论

```javascript
var a = "Davie";
console.log(typeof a); //string
console.log(typeof String(a)); //string
console.log(typeof new String(a)); //object
```

## 3. JavaScript 的数据类型

JavaScript 的数据类型之前已经讲过了，忘记的小伙伴出门左转，查看[**搞懂 JavaScript 的数据类型**](#)

## 4. 各种类型隐式转换到布尔类型对照表

| 数据类型  | 转换为 true 的值 | 转换为 false 的值 |
| --------- | ---------------- | ----------------- |
| Boolean   | true             | false             |
| String    | 任何非空字符串   | "" 空字符串       |
| Number    | 任何非零数字     | 0 和 NaN          |
| Object    | 任何对象         | null              |
| Undefined | 不适用           | undefined         |

## 5. `!`转换规则

`!`会将后面的数据先转成布尔值，然后取反。例如：

```
var a;
var r = !!a;
console.log(r) //false

!!{} // true
!!undefined // false
!!nul // false
!!NaN //fales
```

## 6. `==`比较

> 比较操作符会为两个不同类型的操作数转换类型，然后进行严格比较。当两个操作数都是对象时，JavaScript 会比较其内部引用，当且仅当他们的引用指向内存中的相同对象（区域）时才相等，即他们在栈内存中的引用地址相同。  ---- [引用自 MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)

#### 1. 类型相同的情况

- 如果比较的是两个对象，则比较两个对象的指针是否指向同一个对象，例如：

```
var a = {}
var b = {}
a==b //false
```

很明显，`a`和`b`在堆内存中是两个对象。二另一种情况：

```
var a = {}
var b = a;
a==b //true
```

这时，`a`和`b`就指向了同一个对象，所以相等。

- 其它的基本类型，如果是相同类型，则直接进行严格比较就好，没什么好说的。

#### 2. 类型不同的情况

如果两边类型不同，则两边都**尝试转成 number 类型**。对于引用类型，先调用`valueOf()`,如果能转成数字，则进行比较。不能转成数字就调用`toString()`方法转成字符串。

```javascript
var a = "123";
console.log(a == false); //false,'123'转成数字是123,右侧转成数字是0,最终比较123==0
console.log(a == 123); //true,右边是数字，把左 边转成数字123
```

如果有一边是 object 类型：

```javascript
var a = new String(123);
console.log(a == 123); //true,a.valueOf()结果就是数字123，最终比较的是123==123
```

再看一个：

```javascript
var a = {} console.log(a == 1)
//上面a==1在js解释引擎中的执行过程如下:
// a.valueOf()获取到的不是基本类型，调用a.toString()得到'[object Object]''[object Object]'==1;
// 两边类型不致，左侧转成数字NaN==1;
// false,NaN跟任何类型比较都为false
```

#### 3. null、NaN、undefined

null、NaN、undefined 和 string、number、boolean、object 类型比较时，都不做隐式转换，比较的结果直接为 false。但是需要注意以下几个规则：

```javascript
console.log(NaN == NaN); //false
console.log(undefined == null); //true
console.log(null == null); //true
console.log(null == undefined); //true
undefined == undefined; //true
```

#### 4. 面试题解析

搞清楚规则后，开头的面试题就很容易了：

第一题：

```javascript
//问题1：
console.log(new String("abc") == true);
// step1:右侧转成数字1,变成：new String('abc')==1
// step2 new String('abc').valueOf()不是数字也不是字符串，再调用toString()'[object Object]' == 1
// step3:字符串转数字NaN == 1
// false,NaN和任何类型比较都为false
```

第二题：

```javascript
//问题2：
console.log({} == true);
//step1:右侧转成数字{} == 1
// step2 {}.valueOf()不是数字也不是字符串，再调用toString()'[object Object]' ==1
// step3:字符串转数字NaN == 1
// false,NaN和任何类型比较都为false
```

第三题：

```javascript
//问题3:
console.log([] == ![]);
//step1:!优先级比==高，先转右边,[]是对象类型，转成布尔值为true,!true就是false[]==false
// step2:右侧转成数字为0[]==0
// step3:左侧是一个对象，valueOf()转出来不是字符也不是字符串，调用toString()，得到空字符串'' == 0
// step4:字符串转成数字0 == 0 //true
```

#### 5. 总结

- 类型相同
  - 基本类型，直接比较值
  - 引用类型比较指针
- 类型不同，尝试转成 number 类型，
  - 先调用`valueOf()`转成`number`
  - 不行就再用`toString()`方法转成`string`
- null、NaN、undefined 单独一套规则

## 7. 比较运算符 `>` `<`

来，在来看一道题：

```
console.log('666' < '7')
```

正确答案是 `true`

这是因为**字符串类型比较大小时，不进行类型转换，而是逐位比较 ascii 码，第 1 位不同则返回结果，否则继续比较第 2 位，直到某一位不同为止**。

在比如使用数组的 sort 方法排序：

```javascript
var a = [1, 10, 6, 100].sort();
```

结果是：

```javascript
[1, 10, 100, 6];
```

原因是 sort()方法默认的比较规则会先把每个元素转成字符串，然后比较字符串的 ascii 码来确定先后顺序。

## 8. 加号`+`

`+`运算符即可以对两个数相加，也可以连接字符串，那如果是[1,2,3]+4 这种情况下又会发生什么呢？这就需要我们了解相应的规则，为了方便描述，我们把+号左侧的值叫做 A，右侧的叫做 B：
第一步：如果 A 和 B 都是 number 类型，直接相加；
第二步：接下来看 A 或 B 中是否有一个是否为 string 类型，如果有，则将另一个也转成字符串，然后连接；
第三步：既不是 number,也不是 string,则按如下规则转换：

1.  能转换成数字，返回之
2.  否则调用 valueOf()，如果执行结果是基本类型，返回之；
3.  否则调用 toString()，如果执行结果是基础类型，返回之；
4.  无法得到原始值，抛异常。

**调用 valueOf()返回的结果：**

![](https://files.islu.cn/article/ValueOfResult#id=X1AFB&originHeight=339&originWidth=640&originalType=binary&ratio=1&status=done&style=none)

**调用 toString()返回的结果：**

![](https://files.islu.cn/article/ToStringResult#id=FdwIG&originHeight=339&originWidth=640&originalType=binary&ratio=1&status=done&style=none)

## 9. 减号`-`

除了加号外，减号也很神奇。

使用减号在做非数字类型的运算时，也会发生隐式类型转换.来看下面几个例子：

1. true 会转换成 1

```javascript
5 - true; // 4
```

2. ''空字符串、null 转成 0

```
5 - '' //55 - null //5
```

3. undefined 和非空字符串转成 NaN

```
5 - undefined // NaN5 - 'a' // NaN
```

4. 可以转成数字的字符串转成数字

```
5 - '1'  //4
```
