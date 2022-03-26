---
title: Java关键词总结
author: 闲花
img: "https://files.islu.cn/article/JavaKeyword.jpg"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java关键词总结
keywords: "Java关键词总结,this,super,final,static，abstract,java关键词"
summary: Java关键词总结
abbrlink: 53229
date: 2021-03-15 14:35:33
update: 2021-03-15 14:35:33
---

# Java 关键字

## this 关键字

### 概述

this 代表所在类的对象引用，即当前对象

> new 创建出来的对象
>
> 调用方法的对象

### 作用

1、调用本类中的属性和方法（区别成员变量和局部变量）

2、调用本类中的其他构造方法：this

```shell
格式：
    this([参数...]);

会根据参数列表调用对应的构造方法
public Rabbit(String color) {
    // 调用本来中的属性
    this.color = color;
}

public Rabbit(String color, int age, double weight) {
    // 调用本类中的其他构造方法
    this(color);

    this.age = age;
    this.weight = weight;
}
```

【注意】

```shell
1、this()只能在构造方法中使用
2、this()只能在第一行
3、构造方法中不能同时出现两个this()，因为2
4、不能自己调用自己，不能相互调用
```

### 规范化 this

```java
class Son {
    String name;
    int age;
    float salary;

    public Son() {
    }

    public Son(String name) {
        // 调用Son(String name, int age, float salary)
        this(name, 0, 0.0F);
    }

    public Son(String name, int age) {
        // 调用Son(String name, int age, float salary)
        this(name, age, 0.0F);
    }

    public Son(String name, int age, float salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }
}
```

### 总结

> - this 表示的是当前对象
> - this 可以调用本类中的属性和方法，最常用与区分成员变量和局部变量
> - this 还可以调用本类中的构造方法，但是要注意有坑

## super 关键字

### 概述

> super 指父类对象，用来区分父类和子类，用于调用父类的属性和方法
>
> 用法和 this 非常类似：this 指当前对象，super 指父类对象

### 调用父类的属性和方法

```java
public class Father {
    public int age = 60;

    public void play() {
        System.out.println("下象棋");
    }
}

public class Son extends Father {
    public int age = 16;

    @Override
    public void play() {
        System.out.println("玩游戏");
    }

    public void showAge() {
        int age = 20;
        System.out.println("局部变量：" + age);
        System.out.println("当前对象成员变量：" + this.age);
        System.out.println("父类对象成员变量：" + super.age);
    }

    public void callPlay() {
        // 调用当前对象的方法
        this.play();
        // 调用父类对象的方法
        super.play();
    }
}

public class Demo {
    public static void main(String[] args) {
        Son son = new Son();

        son.showAge();

        son.callPlay();
    }
}
```

### 调用父类的构造方法

默认调用父类的无参构造，且必须在代码的第一行

```java
class Father {
    private String name;

    public Father() {
        System.out.println("Father's Constrator be performed");
    }

    public Father(String name) {
        System.out.println("Father's Constrator be performed with name");
    }
}

class Son extends Father {
    private int age;

    public Son() {
        super();
        System.out.println("Son's Constrator be performed");
    }

    public Son(String name, int age) {
        super(name);
        this.age = age;
        System.out.println("Son's Constrator be performed with name and age");
    }
}

public class TestSon {
    public static void main(String[] args) {
        Son son = new Son();
    }
}
```

> 注意：`super()` 和`this()` 代码不能共存都必须在首行都必须在首行，但是实际效果其实是可以的，如果不写 super 也会自动调用

### 总结

> 1. super 指父类对象，对比 this 关键字，使用方法都一样
> 2. super 和 this 代码不能共存都必须在首行都必须在首行，但是实际效果其实是可以的，如果不写 super 也会自动调用
> 3. 父类的属性要交给父类的构造方法去操作，没什么事就不要去使用 super 来调用父类的构造方法了

## final 关键字

### 概述

final 表示最终的，用来修饰变量，方法和类

```shell
1、final 修饰的局部变量只能被赋值一次
2、final 修饰的成员变量只能被赋值一次，并且必须在声明时就赋值
3、final 修饰的基本类型变量是一个常量(只能被赋值一次)，引用类型变量不可修改地址，如对象
4、final 修饰的方法不能被重写
5、final 修饰的类不能被继承
package com.fc.j._final;
/*
 * final修饰的局部变量
 */
public class FinalDemo1 {
    public static void main(String[] args) {
        // 测试final修饰的修饰的变量
        final int num;

        num = 10;

        System.out.println(num);

        /*
         * 被final修饰的变量只能赋值一次
         *
         * The final local variable num may already have been assigned
         *
         * 被final修饰的局部变量num可能已经被赋值
         */
        // num = 20;
    }
}

// final修饰的类不能被继承，断子绝孙
class Father {
    /*
     * final 修饰的成员变量必须在声明时就赋值
     *
     * The blank final field age may not have been initialized
     * 空白的final成员变量可能未被初始化
     */
     // final int age;
    final int age = 16;

    public final void play() {
        System.out.println("下棋");
    }
}

class Son extends Father {
    /*
     *  Cannot override the final method from Father
     *  无法重写被final修饰的方法
     */
//    @Override
//    public final void play() {
//
//    }
}
```

### 特点

final 修饰可以保证安全性，比如数组的长度属性，String 类，这些都是 final 修饰的，保证不可变

### 总结

> 1、final 表示最终的，可以修饰变量，属性和方法
>
> 2、final 修饰的基本数据类型的成员变量只能被赋值一次
>
> 3、final 修饰的引用数据类型的成员变量地址不可变，但不影响地址所指向的对象的操作
>
> 4、final 修饰的方法不能被重写
>
> 5、final 修饰的类不能被继承

## static 关键字

### 概述

static 关键字方便在**没有创建对象的情况下来进行调用方法和变量**优先级高于对象优先级高于对象，可以用来修饰类的成员方法、类的成员变量，另外可以编写 static 代码块来优化程序性能

### static 变量

static 变量也称作静态变量，静态变量和非静态变量的区别是：静态变量被所有的对象所共享，在内存中只有一个副本，它当且仅当在类初次加载时会被初始化。

```java
public class PersonDemo {
    public static void main(String[] args) {
        Person person1 = new Person("张三", 16);
        Person person2 = new Person("李四", 17);
        Person person3 = new Person("王五", 18);
        Person person4 = new Person("赵六", 19);

        /*
         * The static field Person.address should be accessed in a static way
         * 静态成员变量应该通过静态的方式访问（注意这里是应该，不是必须）
         *
         * Change access to static using 'Person' (declaring type)
         * 使用Person声明类型来更改对静态的访问
         * 通过类名来操作成员变量：Person.address
         */
        System.out.println("姓名：" + person1.name + " 年龄：" + person1.age + " 地址：" + Person.address);
        System.out.println("姓名：" + person2.name + " 年龄：" + person2.age + " 地址：" + Person.address);
        System.out.println("姓名：" + person3.name + " 年龄：" + person3.age + " 地址：" + Person.address);
        System.out.println("姓名：" + person4.name + " 年龄：" + person4.age + " 地址：" + Person.address);

        // 通过类名直接调用static修饰的成员变量，此时是没有对象的
        System.out.println("没有对象：" + Person.address);

        /*
         *  Cannot make a static reference to the non-static field Person.name
         *
         *  将name添加static后没有报错
         */
//        System.out.println("没有对象：" + Person.name);

        /*
         * 通过对象调用statice修饰的成员方法
         *
         * The static method test() from the type Person should be accessed in a static way
         */
        // person1.testStatic();

        // 通过类名直接调用静态方法
        Person.testStatic();
    }
}
```

#### 总结

```shell
1、通过类名调用静态成员变量，因为静态变量与对象无关
2、静态变量被所有对象共享，一处更改处处更改
```

### static 方法

static 方法一般称作静态方法，由于静态方法不依赖于任何对象就可以进行访问，因此对于静态方法来说，是没有 this 的，因为它不依附于任何对象，既然都没有对象，就谈不上 this 了。并且由于这个特性，在静态方法中不能访问类的非静态成员变量和非静态成员方法，因为非静态成员方法/变量都是必须依赖具体的对象才能够被调用。

```java
public class Person {
    public String name = "张三";
    public int age;
    public static String address = "郑州";

    public Person() {
        super();
    }

    public Person(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }

    // 自定义static修饰的成员方法
    public static void testStatic() {
        /*
         * 静态方法不能调用非静态方法
         * Cannot make a static reference to the non-static method test() from the type Person
         */
        // test();
        System.out.println("static mothed");

        /*
         * 不能再静态方法中使用this关键字
         *
         * Cannot use this in a static context
         */
        // this.name;
    }

    public void test() {
        System.out.println("method");
    }
}
```

#### 总结

```shell
1. static修饰的方法不能访问本类中的非静态变量和方法，不能使用this和super
2. 通过类名来调用静态成员方法，工具类的应用很广泛
```

### 总结

> 1. static 修饰的成员变量和方法都是对象所共享的资源，对其进行的操作回作用于所有对象。
> 2. static 修饰的成员变量和方法依赖于类不依赖于对象，即没有对象
> 3. static 修饰的成员变量和成员方法都可以通过类名调用，没有对象
> 4. 静态不能调用费静态，不能使用 this 关键字，没有对象
> 5. 静态变量常和 final 关键字搭配作为常量使用，静态方法常用于工具类

## abstract 关键字

不能实例化的类就是抽象类，用 abstract 修饰

### 构成

```java
abstract class 类名 {
    成员变量
    构造方法
    成员方法
        非抽象方法
        抽象方法
}
```

### 要求

```shell
1、抽象类和抽象方法必须用关键字 abstract 修饰
2、抽象类中不一定有抽象方法，但是有抽象方法的类一定是抽象类
3、abstract 修饰的方法没有方法体，且子类必须重写
4、抽象类不能实例化，因为 abstract 类中有 abstract 方法
5、抽象类的子类
        也可以是一个抽象类，可以重写也可以不重写父类的抽象方法。
        可以是一个具体类。这个类必须重写抽象类中的所有抽象方法。(可以实例化)
public class TestSon {
    public static void main(String[] args) {
        Son son = new Son();
        son.play();
    }
}

// 抽象类
abstract class Father {
    String name;
    int age;

    public Father() {
    }

    public void eat() {
        System.out.println("吃饭");
    }

    // 抽象方法
    abstract public void play();
}

class Son extends Father {
    // 抽象方法的重写
    @Override
    public void play() {
        System.out.println("玩游戏");
    }
}
```
