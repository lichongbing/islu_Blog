---
title: Java代码块
author: 闲花
img: "https://files.islu.cn/article/java{}"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java代码块
keywords: "Java代码块,Java,代码块,构造代码块,静态代码块,代码块相关执行顺序,面试题"
essay: false
summary: Java代码块及相关面试题
abbrlink: 18904
date: 2021-03-24 12:44:01
update: 2021-03-24 12:44:01
---

## 代码块

在 Java 中，使用{}括起来的代码被称为代码块，根据其位置和声明的不同，可以分为局部代码块，构造代码块，静态代码块，同步代码块(多线程)

### 构造代码块

```java
格式：
    {

    }
```

#### 注意

```shell
1、用于给对象初始化，多个构造方法中相同的代码存放到一起，每次调用构造方法都会执行，并且在构造方法前执行
2、只有创建对象时调用，类不能调用
3、构造代码块可以有多个，建议只写一个
class Person {
    {
        System.out.println("Person构造代码块执行");
    }

    public Person() {
        System.out.println("Person构造方法执行");
    }
}

public class TestPerson {
    public static void main(String[] args) {
        System.out.println("main方法");
        new Person();
        new Person();
    }
}
```

### 静态代码块

```java
格式：
    static {

    }
```

#### 注意

```shell
1、用于给类进行初始化，在加载的时候就执行，并且只执行一次
2、优先级高于主函数
3、静态代码块可以有多个，顺序执行，建议只写一个
class Person {
    static {
        System.out.println("Person静态代码块执行");
    }

    public Person() {
        System.out.println("Person构造方法执行");
    }
}

public class TestPerson {
    static {
        System.out.println("静态代码块1执行");
    }

    public static void main(String[] args) {
        System.out.println("main方法");
        new Person();
        new Person();
    }

    static {
        System.out.println("静态代码块2执行");
    }
}
```

结果

```shell
静态代码块1执行
静态代码块2执行
main方法
Person静态代码块执行
Person构造方法执行
Person构造方法执行
```

### 代码块相关执行顺序

```java
public class Father {
    public Father() {
        System.out.println("父类构造方法执行~~~");
    }

    {
        System.out.println("父类构造代码块执行~~~");
    }

    static {
        System.out.println("父类静态代码块执行~~~");
    }

    public static void function() {
        System.out.println("父类静态成员方法执行~~~");
    }
}

public class Son extends Father{
    public Son() {
        System.out.println("子类构造方法执行~~~");
    }

    {
        System.out.println("子类构造代码块执行~~~");
    }

    static {
        System.out.println("子类静态代码块执行~~~");
    }

    public static void function() {
        System.out.println("子类静态成员方法执行~~~");
    }

    public static void main(String[] args) {
        System.out.println("main方法执行~~~");
        new Son();
    }
}
```

结果

```shell
父类静态代码块执行~~~
子类静态代码块执行~~~
main方法执行~~~
父类构造代码块执行~~~
父类构造方法执行~~~
子类构造代码块执行~~~
子类构造方法执行~~~
```

### 面试题

执行顺序

```java
public class Test {
    static Test test1 = new Test();
    static Test test2 = new Test();

    static {
        System.out.println("静态代码块");
    }

    {
        System.out.println("构造代码块");
    }

    public Test() {
        System.out.println("构造方法");
    }

    public static void main(String[] args) {
        System.out.println("main方法");
        new Test();
    }
}
```

结果

```shell
构造代码块
构造方法
构造代码块
构造方法
静态代码块
main方法
构造代码块
构造方法
```

### 总结

> 1、构造代码块用于给对象初始化，每次创建对象都会调用构造代码块，并且执行顺序在构造方法之前
>
> 2、静态代码块用于给类初始化，当类被加载的时候就会调用静态代码块（只执行一次），执行顺序在 main 方法之前
