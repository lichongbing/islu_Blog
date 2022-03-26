---
title: Java接口
author: 闲花
img: "https://files.islu.cn/article/JavaPort"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java接口
keywords: "Java,Java接口,接口特点,接口格式,接口的声明和实现,抽象类实现接口,JDK1.8新特性,default接口"
essay: false
summary: Java接口总结
abbrlink: 50457
date: 2021-03-24 12:51:30
update: 2021-03-24 12:51:30
---

## 接口

### 概念

接口是一系列方法的声明，是一些方法特征的集合，**一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的行为（功能）**。

### 格式

interface ：用来声明接口的关键字

```java
声明格式：
    interface 接口名 {
        静态常量;
        抽象方法;
    }

实现格式：
    class 类名 implements 接口名 {

    }
```

### 特点

```java
1、接口中的成员变量只能是静态常量，定义时必须初始化。默认修饰符：public static final
2、接口中没有构造方法，因为接口不能实例化对象
3、接口中的成员方法只能是抽象方法，没有方法体。默认修饰符：public abstract
4、接口的实现类必须重写接口中方法，或者是一个抽象类(可以重写也可以不重写接口中的方法)
```

### 接口的声明和实现

```java
interface play{
    // 常量，缺省修饰符：public static final
    int time = 10;

    // 抽象方法，缺省修饰符：public abstract
    void geme();
}

public class TestInterface3 implements play{

    // 重写接口中的方法
    @Override
    public void geme() {
        System.out.println("玩游戏");
    }

}
```

【注意】接口的实现类必须重写接口中的方法

### 抽象类实现接口

```java
interface servlet {
    void init();

    void service();
}

abstract class BaseServlet implements servlet {
    // 重写init()方法
    @Override
    public void init() {
        System.out.println("初始化");
    }
}

class MyServlet extends BaseServlet {

    @Override
    public void service() {
        System.out.println("服务方法");
    }
}

public class Test {
    public static void main(String[] args) {
        new MyServlet().init();
        new MyServlet().service();
    }
}
```

【注意】抽象类实现接口，可以选择性重写也可以不重写接口中的方法

### 类的接口多实现

```java
interface Play {
    void geme();
}

interface Eat {
    void noodles();
}

public class TestInterface3 implements Play, Eat {

    // 重写Play类中的方法
    @Override
    public void geme() {
        System.out.println("玩游戏");
    }

    // 重写Eat类中的方法
    @Override
    public void noodles() {
        System.out.println("吃面条");
    }

}
```

【注意】接口的实现类必须重写所有接口中的方法

### 接口的继承

```java
interface Eat {
    void noodles();
}

interface Play {
    void happy();
}

// 单继承
interface Person extends Play {

}

// 多继承
interface Animal extends Play, Eat {

}

// 实体类实现Animal接口，重写所有方法
class Biology implements Animal {

    @Override
    public void happy() {
        System.out.println("玩得开心");
    }

    @Override
    public void noodles() {
        System.out.println("面条好吃");
    }

}

public class Test {
    public static void main(String[] args) {
        Biology biology = new Biology();
        biology.happy();    // 玩得开心
        biology.noodles();    // 面条好吃
    }
}
```

【注意】接口之间可以单继承，也可以多继承

### jdk1.8 新特性：default 接口

```java
interface Function {
    void test();

    default void testDefault() {
        System.out.println("default修饰的接口可以有方法体");
    }
}

// default 修饰的接口可以不被重写
class Base implements Function {

    @Override
    public void test() {
        System.out.println("Base类重写Function接口中的方法");
    }
}

// default 修饰的接口也可以重写
class Boost implements Function {

    @Override
    public void test() {
        System.out.println("Boost类重写Function接口中的方法");
    }

    @Override
    public void testDefault() {
        System.out.println("Boost类重写Function接口中的default方法");
    }
}

public class TestInterface2 {
    public static void main(String[] args) {
        Base base = new Base();
        Boost boost = new Boost();

        base.test();        // Base类重写Function接口中的方法
        base.testDefault();    // default修饰的接口可以有方法体
        boost.test();        // Boost类重写Function接口中的方法
        boost.testDefault();// Boost类重写Function接口中的default方法
    }
}
```

【注意】default 修饰的接口可以不被重写

### 总结

```shell
1、接口是对类的扩展，通过接口可以让类拥有更多更强的功能
2、接口中只有全局常量和抽象方法，所以不能实例化
3、接口的实现类必须重写所有方法，或者是个抽象类
4、接口可以多实现
5、接口可以单继承，也可以多继承
```
