---
title: Java基础笔记
author: 闲花
img: "https://files.islu.cn/article/JavaBasics.jpg"
top: false
toc: true
mathjax: true
summary: Java基础学习笔记
categories: Java
tags:
  - Java
abbrlink: 44149
keywords: Java,Java基础,java语言特点,java开发环境,java基本类型
date: 2020-09-23 00:00:00
update: 2020-09-23 00:00:00
---

# Java 基础

## Java 语言特点

1. 跨平台( 一次开发，到处运行)
2. 面向对象(万物皆对象)

## Java 开发运行环境

JDK:Java 开发工具集(开发人员需要安装)[window 配置 JDK](https://ialoe.top/posts/57766.html)

JVM:java 虚拟机

JRE:java 运行环境（运行 java 程序必须安装）

注:java 程序最终是运行在 jvm 虚拟机上的，不同的操作系统上可以安装其对应版本的 jvm，这样就实现了跨平台

## java 程序开发的步骤

1.  编写源代码 (后缀.java)

```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World！");
    }
}
```

2.  编译                 (后缀.class)
    `javac 文件名.java`
3.  运行
    `java 文件名`

## java 类的结构

```java
public 	class 类名{
    public static void main(String[] args){

    }
}
```

main 方法是 Java 程序的入口

## 语法规则

### 输出语句

```java
System.out.println("输出内容");		//输出完后自动换行--》System.out.print("\n");
System.out.print("输出内容");		//输出完后不自动换行
```

### 转义字符

```
\n		换行符
\t		大空格(Tab键)
```

### 注释

```
//		单行注释

/*
 *		多行注释
 */
```

### 变量

内存中一块储存空间的表示

#### 变量的数据类型

1.  基本类型(8 种)

- byte  1 个字节
- char          2 个字节
- short         2 个字节
- int             4 个字节
- long          8 个字节
- float          4 个字节
- double      8 个字节
- boolean    1 个字节

自动     小——》大
强制     大——》小
大小是根据占用字节判断
byte—》short—》int—》long—》float—》double
char——》int 自动
float——》int 强制 (int)12.3f

2.  引用类型
    String 数组 对象 除了八种基本类型之外的都属于引用数据类型

- 比较相等
  - Java 基本数据类型(8 种)
    - 相等 ==
    - 不相等    !=
  - String
    - 相同 `字符串1.equals(字符串2)`
      - true
    - 不相同    `!字符串1.equals(字符串2)`
      - false

#### 变量的声明和使用

1. 先声明后赋值
   1. 声明变量 数据类型 变量名；
   1. 变量名 = 变量值；
   1. 使用
2. 声明并赋值
   1. 声明变量 数据类型 变量名 = 变量值；
   1. 使用

#### 变量的命名规则

1. 字母,数字,下划线,$,但是不能以数字开头
2. 不能与关键词重名
3. 见名知义
4. 多个单词组成时，第一个单词小写其余单词开头首字母大写。 如:myScore

#### 键盘接收

1.  初始化 Scanner 对象
    `Scanner input=new Scanner(System.in);`
2.  在程序中导入 Scanner 类
    在类的外面写`import java.util.Scanner;`
3.  从键盘接收数据赋值给变量

```java
String name=input.next();//接收到String类型值
int age=input.nextInt();//接收到int类型的值
double score=input.nextDouble();//接收到double类型的值
```

### 数组

#### 声明和使用步骤

1. 声明
2. 分配空间
3. 赋值
4. 使用
5. 注意
   - 声明同时分配空间：`数据类型 [] 数组名=new 数据类型[数组长度];
   - 数组下标从 0 开始         数组元素最大下标值是 `length-1`
   - 声明的时候赋值
     - 数据类型 [] 数组名 = new 数据类型[]{值 1,值 2,...}//后面的括号中不能写长度
     - 数据类型 [] 数组名 = {值 1,值 2,...}//不可拆分

#### 遍历数组元素

```java
for(int i=0;i<数组名.length;i++){
	System.out.println(数组名[下标]);
}
```

#### 数组的应用

1.  数组排序
    使用 Arrays 类 sort 方法排序,默认升序排序

- 步骤
  1. Arrays 类导入 `import java.util.Arrays`
  1. `Arrays.sort(要排序的数组);`

2.  求最大值(打擂台思想)

- 思想
  1. 设置数组第一个元素为默认最大值

2.  循环数组依次与最大值比较

- 关键代码

```java
int max=数组[0];
for(int i=0;i<数组名.length;i++){
	if(数组名[i]>max){
		max=数组名[i];
	}
}
```

3.  向数组中添加元素
    实现思路
1.  找到待插入元素的下标
    - 循环数组,当满足   待插入元素大于当前数组元素的时候,终止循环,并用变量保存当前下标
1.  给待插入元素腾位置
    - 从后往前移动元素   否则会元素覆盖,丢失  i=length-1;i>找到的下标值;i--前一个元素的值   赋值给   后一个
1.  插入元素
    - 数组名[下标]=元素值;

### 运算符

#### 赋值运算符

符号:  =

把等号右边的值赋给左边

> sum+=i;//sum=sum+i;

#### 算数运算符

> \ + - \* /(求商)  %(求余数)  ++(自增)  --(自减)

#### 关系运算符

> <,> ,>=,<=,  == (比较两个数是否相等)  !=（比较两数是否不等）

#### 逻辑运算符

> ||或 &&与 !非

#### 优先级

> ！＞算术运算符＞关系运算符＞＆＆＞｜｜
>
>     	最高小括号,最低赋值运算符

### 流程控制语句

##### 流程图

表示程序的运行流程

- ◇ (菱形)表示判断
- 矩形 表示代码块
- 平行四边形   输出语句
- 圆角矩形   开始或者结束

### 选择结构

1.  简单的 if 选择结构
    语法结构：

```java
if( boolean类型的值 ){
	//代码块
}
```

2.  if-else 选择结构-----用于两种分支判断的情形
    语法结构：

```java
if(){
	//代码块1
}else{
	//代码块2
}
```

3.  多重 if 语句 :用于区间连续情形
    语法结构：

```java
if(){
	//代码块1
}else if(){
	//代码块2
	}else{
		//代码块3
		}
```

4.  嵌套 if 语句 :一个完整的 里面嵌套另一个完整的结构
    语法结构：

```java
if(){
	if(){
		//代码块1
	}else{
		//代码块2
	}
}else{
	if(){
		//代码块3
	}else{
		//代码块4
	}
}
```

5.  switch 选择结构----用于等值判断
    语法结构：

```java
switch(变量){
	case 常量1:
		//代码块1
	break;
	case 常量2:
		//代码块2
	break;
	default:
		//代码块3
	break;
}
```

- switch 小括号里的变量  --->整型和字符型,jdk 版本 1.7 以上 支持 String
- break 可以省略,但是省略之后 case 之间会贯穿执行,直到遇到 break 才结束
- 各个 case 之间常量值不能重复的
- default 总是在最后执行的,当前面所有的 case 都匹配不上时,位置不固定

### 循环结构

1.  while 循环-----先判断再执行

```java
//初始化循环变量
while(判断条件){
				//循环操作
				更新循环变量
			}
```

2.  do-while---先执行再判断

```java
//定义循环变量
do{
	//循环体
	//循环变量的更新
}while(判断条件);
```

3.  for 循环---用于固定循环次数
    执行顺序:同 while  1.变量初始化  2 条件判断  3 循环体  4 变量更新
    for 循环中 3 个表达式均可省略,但是一般不要省略

```java
for(循环变量初始化;条件判断;循环变量更新){
				//循环体
	      		}
```

4.  三种循环比较
    顺序：

- 先判断后执行：while for
- 先执行后判断：do-while
- for 循环主要用于循环次数固定
- 在循环条件不成立的时候，do-while 至少执行一次

5.  二重循环
    一个完整的循环结构   再嵌套另一个
    外层循环变化一次,内层循环变化一遍

```java
for(){
	   //循环体
	 for(){
	 	//循环体
	 	}
	}
```

### 流程控制语句

- break
  - 单层循环中: 终止循环，执行循环外的语句
  - 二重循环中:用在内层循环中,只能结束内层循环,执行外层剩下的代码
- continue
  - 单层循环:跳过本次循环，执行下一次循环
  - 结束本层的本次循环 执行本层下一次

### 解决代码中的异常

- 常见的错误信息
  - The local(局部的) variable(变量) num may not have been(可能还没有被) initialized(初始化)===>变量尚未赋值就已经使用
  - num cannot be resolved to a variable===>变量没有声明
  - java.util.InputMismatchException  ===>输入类型不匹配
  - 数组下标越界  java.lang.ArrayIndexOutOfBoundsException   当访问超出了数组下标范围
    - Array 数组
    - index 下标
    - outof 超出了
    - bounds 边界
    - Exception 异常
- 简单的异常处理
  - input.hasNextInt()   判断用户输入的内容是否是合法整数,合法为 true, 否则为 false
    - 要在变量赋值之前判断
- 程序调试
  程序在我们的控制下一步一步执行
  - 调试代码之前,要先分析可能出错的位置
  - 在可能出错的地方   打断点---代码执行到断点处会暂停   行号前双击
  - 以 debug 模式启动程序  debug as---java application
  - 单步执行,查找错误(F6) {程序运行到断点处才会启动调试模式}
  - 找到错误,修改代码
