---
title: Java常用API
author: 闲花
img: "https://files.islu.cn/article/JavaAPI.png"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - JavaAPI概述
  - Java常用API
keywords: "Java,JavaAPI,Java常用API,Scanner,Object,equals,Math,System"
essay: false
summary: Java常用API(Object、System、Scanner、Math)
abbrlink: 32274
date: 2021-03-24 12:39:13
update: 2021-03-24 12:39:13
---

## API 概述

> API(Application Programming Interface) 应用程序编程接口

编写一个机器人程序去控制机器人踢足球，程序就需要向机器人发出向前跑、向后跑、射门、抢球等各种命令，没有编过程序的人很难想象这样的程序如何编写。但是对于有经验的开发人员来说，知道机器人厂商一定会提供一些用于控制机器人的 Java 类，这些类中定义好了操作机器人各种动作的方法。其实，这些 Java 类就是机器人厂商提供给应用程序编程的接口，大家把这些类称为 Xxx Robot API。本章涉及的 Java API 指的就是 JDK 中提供的各种功能的 Java 类。

## 学习汉语和学习编程的异同点

相同点

- 基本语法
- 大量成语
- 写文章的手法和技巧

不同点

- 学习汉语 必须先学后用
- 学习编程 可以现用现学

## Object 类

Object 类是类层次结构的根类，所有类都直接或者间接的继承自该类

### 构造方法

```java
public Object()
```

【注意】Object 只有一个无参构造方法

### toString()

#### 作用

用来返回对象的字符串表示形式

```java
public String toString()
```

返回值为：包名.类名@当前对象在内存空间中的首地址

```java
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

#### 重写 toString()

由于默认情况下的数据对我们来说没有意义，一般会重写该方法用以展示对象的字段信息

```java
public class Student {
    String name;
    int age;

    // 重写 toString 方法
    @Override
    public String toString() {
        return "Student [name=" + name + ", age=" + age + "]";
    }
}
```

测试

```java
public class TestStudent {
    public static void main(String[] args) {
        Student student = new Student("Buffer",23);
        System.out.println(student);
    }
}
```

结果

```shell
Student [name=Buffer, age=23]
```

#### 总结

> toString 方法用来展示一些对象的基本信息：完整的包名.类名@堆内存地址，通常我们用快捷键来重写这个方法来获取我们需要的数据信息

### equals()

#### 作用

用来比较两个对象的地址是否相同

```
public boolean equals(Object obj) {
        return (this == obj);
}
```

如果调用此方法的对象与 obj 的地址相同(即为同一个对象)，返回 true，否则返回 false

#### 重写 equals()思路

一般需要重写 equals() 方法用以判断两个对象的字段是否相同

```shell
1、判断两个对象的地址是否相同
2、判断两个对象的类型是否一致
3、判断两个对象所存储的数据是否相同
```

#### 重写 equals()

```java
public class Student {
    String name;
    int age;

    // 重写 equals 方法
    @Override
    public boolean equals(Object obj) {

        // 判断是否是同一个对象(地址相同)，如果是返回 true
        if (this == obj) {
            return true;
        }

        // 判断数据类型是否一致，如果不一致返回 false
        if (!(obj instanceof Student)) {
            return false;
        }

        // 强制类型转换为当前类对象
        Student student = (Student) obj;

        // 所有字段全部满足时返回 true ，否则返回false
        return this.name.equals(student.name) && this.age == student.age;
    }
}
```

测试

```java
public class TestStudent {
    public static void main(String[] args) {
        Student student1 = new Student("Buffer",23);
        Student student2 = new Student("Banlance",22);
        Student student3 = new Student("Buffer",23);

        System.out.println(student1.equals(student2));
        System.out.println(student1.equals(student3));
    }
}
```

结果

```java
false
true
```

【注意】基本数据类型不能使用 equals() 方法

#### 总结

> 1、equals 方法用来判断两个对象是否相同，默认比较的是两个对象的内存首地址。我们可以通过重写 equals 方法实现对两个对象的比较
>
> 2、注意 equals 方法的调用者，不同的调用者调用方法是不一样的

### hashCode()

#### 作用

返回对象的哈希码值，**具有唯一指向性**

```java
public int hashCode()
```

#### 重写 hashCode()

hashCode 方法要求必须和 equals() 方法的结果是对应的，如果两个对象的 equals 的结果为 true ，那这两个对象的 hashCode 的值一定相同，所以**只要重写了 equals 方法，就必须重写 hashCode 方法**

```java
public class Student {
    String name;
    int age;

    // 重写 equals 方法
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }

        if (!(obj instanceof Student)) {
            return false;
        }

        Student student = (Student) obj;

        return this.name.equals(student.name) && this.age == student.age;
    }

    // 重写 hashCode 方法
    @Override
    public int hashCode() {
        // 调用 Objects 工具类的 hash 方法，根据传入的参数生成一个指定的 hashCode 值
        return Objects.hash(name, age);
    }
}
```

测试

```java
public class TestStudent {
    public static void main(String[] args) {
        Student student1 = new Student("Buffer",23);
        Student student2 = new Student("Banlance",22);
        Student student3 = new Student("Buffer",23);

        System.out.println(student1.equals(student2));
        System.out.println(student1.equals(student3));

        System.out.println(student1.hashCode());
        System.out.println(student2.hashCode());
        System.out.println(student3.hashCode());
    }
}
```

结果

```shell
false
true
1892650872
247063595
1892650872
```

student1 和 student3 的 equals 方法返回值是 true ，所以他们的 hashCode 值相同

#### 总结

> 1、hashCode()用来获取当前对象的哈希值，表示对象的唯一标识。如果重写 equals()则必须重写 hashCode()方法
>
> 2、equals 相同 hashCode 一定相同，hashCode 相同 equals 不一定相同

### getClass()

获取当前对象的 Class 对象（字节码对象），直接打印会显示包含完整的包名,类名的信息

```java
public final native Class<?> getClass();
class Cat {}

public class GetClassDemo {
    public static void main(String[] args) {
        Cat cat = new Cat();
        System.out.println(cat.getClass());
    }
}
```

### finalize()

```java
protected void finalize()
```

当垃圾回收器确定不存在对该对象的更多引用时，由对象的垃圾回收器调用此方法。

### 总结

> Object 类是所有类的基类，提供了一个无参的构造方法和一些公共方法
>
> 通过重写 toString 方法来获取对象中的数据
>
> 通过重写 equals 方法和 hashCode 方法来判断两个对象是否相同，这两个方法必须同时重写
>
> getClass 用来获取 Class 对象
>
> finalize 方法用于垃圾回收，不可控

## System 类

`System` 类包含一些有用的类字段和方法。它不能被实例化。

在 `System` 类提供的设施中，有标准输入、标准输出和错误输出流；对外部定义的属性和环境变量的访问；加载文件和库的方法；还有快速复制数组的一部分的实用方法。

### 成员变量

```java
// 标准输入流，常用于键盘录入
public final static InputStream in = null

// 标准输出流，常用于打印信息
public final static PrintStream out = null;

// 标准错误输出流，常用于打印错误信息
public final static PrintStream err = null;
public class SystemFieldDemo {
    public static void main(String[] args) {
        // 通过Scanner测试标准输入
        Scanner sc = new Scanner(System.in);

        String next = sc.next();

        // 通过System.out.print测试标准输出流
        System.out.println(next);

        sc.close();

        // 通过System.err.print测试标准输出流
        System.err.println("打印错误报告");
    }
}
```

### 构造方法

构造方法私有化，无法创建对象

```java
/** Don't let anyone instantiate this class */
private System() {
}
```

### arraycopy()

这个方法表示复制数组，从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束。

```java
public static native void arraycopy(Object src,  int  srcPos,
                                        Object dest, int destPos,
                                        int length);
```

参数解释

> src - 源数组。
> srcPos - 源数组中的起始位置。
> dest - 目标数组。
> destPos - 目标数据中的起始位置。
> length - 要复制的数组元素的数量。

```java
public class ArraycopyDemo {
    public static void main(String[] args) {
        // 创建一个长度为5的int类型数组arr
        int[] arr = new int[5];

        // 为数组arr赋值
        for (int i = 0; i < arr.length; i++) {
            arr[i] = i;
        }

        // 遍历数组arr
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }

        System.out.println("------------------");

        // 创建一个新的长度为5的int类型数组newArr
        int[] newArr = new int[5];

        // 调用System的arraycopy方法，分别传入对应的参数
        System.arraycopy(arr, 0, newArr, 0, 5);

        // 遍历newArr数组
        for (int i = 0; i < newArr.length; i++) {
            System.out.println(newArr[i]);
        }
    }
}
```

### currentTimeMillis()

返回以毫秒为单位的当前时间。

```java
public static native long currentTimeMillis();
```

【注意】

> 1、这个方法的返回值是 long 类型
>
> 2、当前时间与协调世界时 1970 年 1 月 1 日午夜之间的时间差（以毫秒为单位测量）

```java
public class CurrentTimeMillsDemo {
    public static void main(String[] args) {

        long currentTimeMillis = System.currentTimeMillis();

        System.out.println("毫秒：" + currentTimeMillis);
        System.out.println("年：" + currentTimeMillis/1000/60/60/24/365);

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

        String date = sdf.format(currentTimeMillis);

        System.out.println(date); // 2020-10-06 17:53:02
    }
}
```

### gc()

运行垃圾回收器。在此之前会调用 Object 的 finalize()

```java
public static void gc()
```

> System.gc()可用于垃圾回收。当使用 System.gc()回收某个对象所占用的内存之前，通过要求程序调用适当的方法来清理资源。在没有明确指定资源清理的情况下，Java 提高了默认机制来清理该对象的资源，就是调用 Object 类的 finalize()方法。finalize()方法的作用是释放一个对象占用的内存空间时，会被 JVM 调用。而子类重写该方法，就可以清理对象占用的资源，该方法有没有链式调用，所以必须手动实现。

```java
class Person {
    private String name;
    private int age;

    // 构造方法，getter、setter方法、toString方法

    /*
     * 通过重写finalize方法验证调用gc会执行此方法
     */
    @Override
    protected void finalize() throws Throwable {
        System.out.println("执行finalize方法回收垃圾：" + this);
        super.finalize();
    }
}

public class GcDemo {
    public static void main(String[] args) {
        System.out.println(new Person("张三", 16));
        System.gc();
    }
}
```

> 从程序的运行结果可以发现，执行 System.gc()前，系统会自动调用 finalize()方法清除对象占有的资源，通过 super.finalize()方式可以实现从下到上的 finalize()方法的调用，即先释放自己的资源，再去释放父类的资源。
>
> 但是，不要在程序中频繁的调用垃圾回收，因为每一次执行垃圾回收，jvm 都会强制启动垃圾回收器运行，这会耗费更多的系统资源，会与正常的 Java 程序运行争抢资源，只有在执行大量的对象的释放，才调用垃圾回收最好

### exit()

终止当前正在运行的 Java 虚拟机。参数用作状态码；根据惯例，非 0 的状态码表示异常终止。

```java
public static void exit(int status)
public class ExitDemo {
    public static void main(String[] args) {
        System.out.println("程序执行开始");
        // 执行此方法后关闭虚拟机，程序不会再向下执行
        System.exit(0);
        System.out.println("程序执行结束");
    }
}
```

### 总结

> System 类提供了一些和系统相关的类字段和方法，便于我们和底层进行交互。
>
> 比较常用的就是 arraycopy()和 currentTimeMills()，其他不需要关注

## Scanner 类

一个可以使用正则表达式来解析基本类型和字符串的简单文本扫描器。

### 类声明

```java
public final class Scanner implements Iterator<String>, Closeable {}
```

> 这里我们需要关注三个点：
>
> 1、final 修饰，不能被继承
>
> 2、实现了 Iterator 接口(迭代器接口)，主要使用其中的 hasNext 方法和 next 方法
>
> 3、实现了 Closeable 接口，主要使用其中的 close 方法

```java
// 用来判断是否还有下一个元素录入
public boolean hasNext()

// 用来接收录入的数据
public String next()

// 用来关闭资源(输入流)
public void close()
```

### 构造方法

从指定的扫描输入流构造一个 Scanner

```java
public Scanner(InputStream source)
```

案例代码

```java
public class Demo1 {
    public static void main(String[] args) {
        // java.util.Scanner.Scanner(InputStream source)
        // 使用构造方法，传入一个标准输入流，创建一个Scanner对象
        Scanner sc = new Scanner(System.in);
    }
}
```

### next()

```java
// 此方法用于接收从键盘录入的字符串
public String next()
```

案例代码

```java
public class Demo1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 从键盘录入一个字符串
        String str = sc.next();

        System.out.println(str);
    }
}
```

### nextInt()

#### 常用方法

```java
// 此方法用于从键盘获取一个int类型的数据
public int nextInt()
```

案例代码

```java
public class Demo1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 从键盘录入一个字符串
        int num = sc.nextInt();

        System.out.println(num);
    }
}
```

#### 方法的重载：nextInt(int radix)

```java
// 指定进制数从键盘录入一个int类型的数据
public int nextInt(int radix)
```

> int radix 参数表示一个进制数，如果从键盘录入的数据超过了指定的进制数就会报错，默认是 10

案例代码

```java
public class Demo5 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        /*
         * 8表示接收8进制内的数，及0~7
         *
         * 从键盘录入的数据中不能出现8及其以上的数字，如果有会报错：
         * InputMismatchException 输入类型不匹配异常
         */
        int num = sc.nextInt(8);

        System.out.println(num);
    }
}
```

#### 相关方法：用法类似，要求触类旁通

```java
public String nextLine()
public byte nextByte()
public byte nextByte(int radix)
public short nextShort()
public long nextLong()
public float nextFloat()
public double nextDouble()
public BigInteger nextBigInteger()
```

### hasNextInt()

```java
// 如果此扫描器的输入中有另一个标记，则返回 true。在等待要扫描的输入时，此方法可能阻塞。扫描器将不执行任何输入。
public boolean hasNext()
```

> 此方法可用于合法性判断

案例

```java
public class Demo2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (sc.hasNextInt()) {
            System.out.println(sc.nextInt());
        } else {
            System.out.println("输入的数据类型有误");
        }
    }
}
```

其他相关方法

```java
public boolean hasNext()
public boolean hasNextLine()
public boolean hasNextBoolean()
public boolean hasNextByte()
public boolean hasNextShort()
public boolean hasNextLong()
public boolean hasNextFloat()
public boolean hasNextDouble()
```

### 扩展：回车换行问题

```java
public class Demo3 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int num = sc.nextInt();
        String str = sc.nextLine();

        System.out.println("str:" + str + "，num:" + num);
    }
}
```

> 当从键盘录入第一个数字后，敲下的回车键实际是两个字符：\r\n，所以键盘实际是录入了这两个字符并且结束，显示的效果和没有录入字符串相同
>
> 补充：
>
> \r：回车，回到行首
>
> \n：换行
>
> 电脑上的回车键(Enter 键)实际上是回车式换行，会先执行回车，后执行换行

扩展：多行录入

可以通过 hasNext 的重载方法来实现多行录入

```java
// 如果从键盘录入指定的pattern标记，则返回true，否则返回false
public boolean hasNext(String pattern)
```

案例

```java
public class Demo4 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        StringBuffer sb = new StringBuffer();

        // 将#作为结束的标记，当遇到#时结束循环
        while (!sc.hasNext("#")) {
            sb.append(sc.next());
        }

        System.out.println(sb);
    }
}
```

### 总结

> Scanner 通过标准输入流来从键盘输入，后期不会用到，目前常用的方法为 nextXxx()和 hasNextXxx()

## Math 类

Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。

### 成员变量

> 静态常量，全大写，通过类名调用

```java
// 比任何其他值都更接近 e（即自然对数的底数）的 double 值
public static final double E = 2.7182818284590452354;

// 比任何其他值都更接近 pi（即圆的周长与直径之比）的 double 值
public static final double PI = 3.14159265358979323846;
```

### 构造方法

> 构造方法私有化，不能创建对象

```java
private Math() {}
```

### 成员方法

> 所有方法全部都被 static 修饰，可以通过类名直接调用

```java
// 获取绝对值
public static int abs(int a)

// 对数据进行向上取整
public static double ceil(double a)

// 对数据进行向下取整
public static double floor(double a)

// 获取最大值
public static int max(int a,int b)

// 获取最小值
public static int min(int a, int b)

// 获取a的b次幂
public static double pow(double a,double b)

// 随机数，范围：[0.0, 1.0)，注意左闭右开，包含左边不包含右边，
public static double random()

// 四舍五入
public static int round(float a)

// 获取正平方根
public static double sqrt(double a)
```

案例代码

```java
package com.fc.r.math;

public class MathDemo1 {
    public static void main(String[] args) {
        // 自然对数的底
        System.out.println("Math.E:" + Math.E);
        // π
        System.out.println("Math.PI:" + Math.PI);

        System.out.println("-----------------");

        // 绝对值
        System.out.println("abs:" + Math.abs(-1));
        System.out.println("abs:" + Math.abs(1));

        System.out.println("-----------------");

        // 向上取整
        System.out.println("ceil:" + Math.ceil(12.34));
        System.out.println("ceil:" + Math.ceil(12.56));

        System.out.println("-----------------");

        // 向下取整
        System.out.println("floor:" + Math.floor(12.34));
        System.out.println("floor:" + Math.floor(12.56));

        System.out.println("-----------------");

        // 最大最小值
        System.out.println("max:" + Math.max(12.34, 56.78));
        System.out.println("max:" + Math.max(12.34, Math.max(56.78, 100)));
        System.out.println("min:" + Math.min(12.34, 56.78));

        System.out.println("-----------------");

        // a的b次方
        System.out.println("pow:" + Math.pow(2, 10));

        System.out.println("-----------------");

        // 随机数1~10
        System.out.println("random:" + (int) (Math.random() * 10 + 1));

        System.out.println("-----------------");

        // 四舍五入
        System.out.println("round:" + Math.round(12.34));
        System.out.println("round:" + Math.round(12.56));

        System.out.println("-----------------");

        // 获取正平方根
        System.out.println("sqrt:" + Math.sqrt(16));
    }
}
```
