---
title: Java方法
author: 闲花
img: "https://files.islu.cn/article/JavaVoid"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java方法
keywords: "Java方法的声明及使用,java引用传递,java值传递,java方法"
summary: Java方法的声明及使用
abbrlink: 16735
date: 2021-03-15 14:43:29
update: 2021-03-15 14:43:29
---

# Java 方法

## 为什么要使用方法

### 生活中的方法（工具）

螺丝刀，锤子，扳手

> 1、提高复用度，可重复使用
>
> 2、提高效率

开发中使用方法来实现同样的效果，为了解决复用和效率的问题

## 概念

实现特定功能的一段代码，可以被反复使用

## 方法的构成

```shell
固定格式：
    public static
返回值类型：
    表示方法执行完成后返回的数据类型
    如果没有返回值类型就用 void ，如果有就使用对应的返回值类型
方法名：
    小驼峰命名，见名知意，动宾结构
形参列表：
    用来接收用户传入的数据，可以是基本数据类型或者引用数据类型，需要声明局部变量。
    如果不需要形参就写 ()，如果有多个就写多个
方法体：
    {}
```

> 注意：

> 1. 固定的格式（public static）不要问，因为不影响我们写代码，后期会讲！！！
> 2. 方法要写上文档注释，为了更方便地阅读代码

## 方法声明格式

```java
public static returnType methodName(dataType FormerParameter) {
    method body;
}

public static 返回值类型 方法名(数据类型 形参名) {
    方法体;
}
```

## 声明位置

定义在类中，与其他方法（main 方法）并列

## 无返回值方法调用

```java
mothodName(actualParameter);
方法名(实参);
```

> 注意：

> 方法和变量最大的区别就是方法后面有小括号，即便没有参数也有小括号
>
> 小驼峰

### 无参无返回值调用

```java
class TestMethod1 {
    public static void main(String[] args) {
        printHelloWorld();
    }

    /**
    * 打印Hello World
    */
    public static void printHelloWorld() {
        System.out.println("Hello World");
    }
}
```

> 注意
>
> 1. main 方法是程序的入口，所有的代码和方法都需要在 main 方法中被完成和调用
> 2. 方法名的后面一定要跟
> 3. 方法和其他方法的关系是并列关系

### 有参无返回值调用

```java
import java.util.Scanner;

class TestMethod3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入一个数：");
        int num = scanner.nextInt();

        printIntNum(num);
    }

    /**
    * 展示用户传入的int类型数据
    *
    * @param num 这里需要传入一个int类型的数据
    */
    public static void printIntNum(int num) {
        System.out.println("您输入的数为：" + num);
    }
}
```

> 注意：
>
> 1. 如果方法声明时带有形式参数，那么方法调用时就必须携带实际参数 1
> 2. 如果方法声明时没有形式参数，方法调用时就不能有实参
> 3. 声明时有几个形式参数，调用时就传入几个实际参数，形参实参个数不一样编译会报错
> 4. 实参与形参的数据类型不一样，编译器会报错
> 5. 实参与形参的顺序不一样，编译器会报错

## 形参与实参

> 形参：用来接收调用该方法时传递的参数。只有在被调用的时候才分配内存空间，一旦调用结束，就释放内存空间。因此仅仅在方法内有效。
> 实参：方法调用时用于传入的数据，用来给形参赋值，数据类型要求一致

### 形参举例

```java
  public void swap(int a, int b) {
         int temp = a;
         a = b;
         b = temp;
         System.out.println("a:" + a + " b:" + b);
     }
 这里边的a,b就是形参，temp是一个局部变量，方法结束，在栈空间中就会被销毁
```

### 实参举例

```java
 调用上面的方法
 swap(1,2);
 其中1和2就是实际的参数值，就叫实参
```

## 返回值

方法中的返回值有两种情况，即有返回值和无返回值，如果定义方法时有返回值类型，就需要返回相对应的数据类型

```java
基本数据类型
    值传递，不改变自身
引用数据类型
    引用传递，改变自身
void
    无返回值
1、一个方法只能有一个返回值
2、分支结构的每一个分支都需要正确的返回值
3、返回值可以接收也可以不接收
```

### return 关键字

#### 作用

结束当前方法，返回至调用方法处，如果定义了返回值类型就返回对应类型的数据

【注意】[数据类型一致化](https://localhost:63342/ialoe.github.io-master/posts/35.html?_ijt=bqlst5qgc5f4q088n5220dj5j)

#### 格式

```java
return 需要返回的数据;
```

### 注意

```shell
1、单一职能原则，一个方法只做一件事
2、注意形参和实参数据类型一致化
3、返回值类型和参数没有关系
4、方法名要符合小驼峰命名规则
5、return的下一行代码不会执行
```

## 有返回值方法调用

### 无参有返回值的方法：give me five

```java
class TestMethod1 {
    public static void main(String[] args) {
        System.out.println(giveMeFive());
    }

    /**
    * 返回一个整数 5
    *
    * @return 5 int类型
    */
    public static int giveMeFive() {
        return 5;
    }
}
```

### 有参有返回值的方法：两个数求和

```java
public class MethodDemo6 {
    public static void main(String[] args) {
        /*
         * 调用自定义getSumOfTwoNumber方法，需要两个int类型的参数，并得到一个int类型的返回值
         *
         * 参数列表一定要和方法声明上的参数类型完全一致
         */
        int total = getSumOfTwoNumber(1, 2);

        System.out.println(total);
    }

    /**
     * 两个整数进行求和
     *
     * @param num1 求和的第一个数
     * @param num2 求和的第二个数
     * @return 返回两个参数的和，int类型
     */
    public static int getSumOfTwoNumber(int num1, int num2){
        return num1 + num2;
    }
}
```

> 注意:调用带有多参数的方法，要求传入的参数数据类型，个数和顺序还有数据类型必须和方法声明一致

### 规范化 return

在一个方法中，return 出现的次数要尽可能得少，为了提高阅读性和逻辑性

```java
class TestMethod4 {
    public static void main(String[] args) {
        System.out.println(getCompare(3,2));
    }

    /**
    * 比较大小，返回较大的那个数
    *
    * @param num1 int类型
    * @param num2 int类型
    * @return int类型的结果
    */
    public static int getCompare(int num1, int num2) {
        return num1 > num2 ? num1 : num2;
    }
}
```

### 总结

```shell
1、break 是退出当前循环结构，return 是退出当前方法

2、如果返回值类型是 void ，可以返回 null 或者不返回或者 return;

3、一个方法可以有多个 return，但只能有一个返回值

4、返回值可以接收也可以不接收，由调用者决定如何调用

5、分支结构里的每一个分支都需要有正确的返回值

6、对返回值的处理方式因情况而定，可以打印、参与运算或者当做其他方法的实参

7、调用带有多参数的方法，要求传入的参数数据类型，个数和顺序和类型必须和方法声明一致
```

> 注意:方法具有单一职能原则，一个函数只做一件事

## 方法重载【Overload】

### 概念

一个类或者接口中定义多个相同名称的方法

### 要求

```shell
1、必须在同一个类中
2、方法名必须一致
3、参数必须不一致(个数，顺序，类型)
4、与访问修饰符、返回值类型无关
public class MethodDemo9 {
    public static void main(String[] args) {
        // 调用同名方法，传入不同的参数列表，即可实现方法的重载
        play();
        play("英雄联盟");
        play("红色警戒", 2);
        play(1, "DNF");
    }

    public static void play() {
        System.out.println("玩王者荣耀");
    }

    public static void play(String gameName) {
        System.out.println("玩" + gameName);
    }

    public static void play(String gameName, int time) {
        System.out.println("玩" + gameName + time + "小时");
    }

    public static void play(int time, String gameName) {
        System.out.println("玩" + gameName + time + "小时");
    }

    /*
     * Duplicate method play(String, int) in type MethodDemo9
     *
     * 跟返回值类型无关，只关注方法名和参数类型
     */
//    public static String play(String gameName, int time) {
//        return "玩" + gameName + time + "小时";
//    }
}
```

### 优点

满足需求多样化，屏蔽使用差异，灵活、方便

### 总结

> 方法的重载我们只关注方法名和参数类型，要求方法名必须一致，参数列表必须不一致（个数，顺序，类型）

## 局部变量

### 概念

在方法内部或者形参列表上定义的变量（包括 main 方法）

### 作用域

从定义局部变量的那一行到所在的代码块结束

```java
for (int i = 1; i <= 10; i++) {

}

for (int i = 1; i <= 10; i++) {

}
```

【注意】两个 for 循环中，i 循环变量分别属于不同的大括号以内，不同的作用域空间，并不冲突

### 生存期

从方法被调用的时刻算起到函数返回调用处的时刻结束

```java
for (int i = 1; i <= 10; i++) {

}

System.out.println(i); // 报错，找不到符号
```

【注意】for 循环结束时局部变量 i 的生存期结束，在 for 循环外无法使用 i

### 单一性，不能重名

```java
// 报错！
for (int i = 1; i <= 10; i++) {
    for (int i = 1; i <= 10; i++) {

    }
}
```

【注意】在一个方法内局部变量不能多次定义

### 值传递

```java
class Test {
    public static void main(String[] args) {
        int num = 5;
        test(num);

        System.out.println(num);    // 5
    }

    public static void test(int num) {
        num = 10;
    }
}
```

【注意】基本数据类型作为参数传递给局部变量时，传递的是值，局部变量的更改不影响实参本身

| ![](https://files.islu.cn/medias/reward/loading.gif#id=x2spE&originalType=binary&ratio=1&status=done&style=none) |
| ---------------------------------------------------------------------------------------------------------------- |
| ![](https://files.islu.cn/medias/reward/loading.gif#id=IS8Ok&originalType=binary&ratio=1&status=done&style=none) |

### 引用传递

```java
public class MethodDemoC {
    public static void main(String[] args) {
        int[] arr = new int[5];

        System.out.println("调用方法前：" + arr[0]);

        test(arr);

        System.out.println("调用方法后：" + arr[0]);
    }

    public static void test(int[] arr) {
        arr[0] = 1;
    }
}
```

【注意】引用数据类型传递时传递的是地址，局部变量直接作用于实参本身

| 引用传递分析图                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------- |
| More Actions![](https://files.islu.cn/medias/reward/loading.gif#id=Zpdob&originalType=binary&ratio=1&status=done&style=none) |

### 总结

1. 局部变量声明在函数中，从定义的那一行开始到函数结束时被销毁
2. 局部变量必须先赋值再使用
3. 局部变量不能重复定义
4. 值传递：基本数据类型的传递不改变实参
5. 引用传递：引用数据类型的传递会改变实参
6. Java 中只有值传递，引用传递传递的是地址值

## 构造方法

### 引言

> 构造方法很重要，但是比较鸡肋

### 定义

构造方法（`Constructor`）的名称和类名相同，没有返回值类型。

### 作用

类中的特殊方法，用于创建对象，在创建对象的时候会执行一些初始化操作，如给成员属性赋初值

### 格式

```java
格式：
    类名([参数...]){}
    Student(){}
```

注意：格式问题

> 1、构造方法的方法名与类名完全相同
>
> 2、构造方法没有返回值类型
>
> 3、创建对象时，触发构造方法的调用，不可手动调用
>
> 4、如果没有声明构造方法，编译器默认生成无参构造方法
>
> 5、如果定义了有参构造方法，编译器就不会创建无参构造方法
>
> 【强制要求】

```shell
无论什么时候，都要加上一个无参构造方法！！！
```

### 构造方法的使用

```java
// 自定义有参构造方法，并给name属性赋值
Dog(String n) {
    name = n;
}

// 自定义无参构造方法
Dog(){}
```

### 构造方法的重载

```java
public Dog(String n){
    name = n;
}

public Dog(String n, int i){
    name = n;
    age = i;
}
```

### 总结

> 1. 构造方法是用来创建对象，在创建对象的过程中会进行初始化操作（为对象赋值）
> 2. 构造方法也是方法，除了没有返回值，其他的都跟方法一样

> 按照方法参数列表的类型、个数、顺序去匹配，如果没有找到对应的就会报错
>
> 1. 无论什么时候，都一定要给一个无参构造方法

### 扩展：反编译

```shell
javap -c -l -private 类名.class
```

### 扩展：对象的创建过程

```shell
1、类加载
2、内存中开辟对象空间
3、为各个属性赋予初始值
4、执行构造方法中的代码
5、将对象的地址赋值给变量
```

## 方法重写【@Override】

开发中父类的方法不一定适用于子类，因为父类方法不能更改，在子类中新增方法会造成代码的冗余，而且不符合逻辑

### 要求

> 1. 应用于继承和实现接口
> 2. 方法的返回值类型，方法名，形参列表与父类一致
> 3. 使用`@Override`注解来标识
> 4. 重写方法的访问修饰符权限不能低于父类
>    private < 默认什么都不写什么都不写 < protected < public

```java
/*
 *十二生肖类的继承+方法重写
 */
class rat {
    private String name;// 名字
    private int ranking;// 排名

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getRanking() {
        return ranking;
    }

    public void setRanking(int ranking) {
        this.ranking = ranking;
    }

    public void skill() {
        System.out.print("打洞");
    }

    public void print() {
        System.out.print(name + "\t" + ranking + "\t");
        skill();
        System.out.println();
    }
}

class cow extends rat {
    public void skill() {
        System.out.print("耕田");
    }
}

class tiger extends rat {
    public void skill() {
        System.out.print("打斗");
    }
}

class rabbit extends rat {
    public void skill() {
        System.out.print("躲避");
    }
}

class dragon extends rat {
    public void skill() {
        System.out.print("呼风唤雨");
    }
}

class snake extends rat {
    public void skill() {
        System.out.print("游走");
    }
}

class horse extends rat {
    public void skill() {
        System.out.print("飞奔");
    }
}

class sheep extends rat {
    public void skill() {
        System.out.print("吃草");
    }
}

class monkey extends rat {
    public void skill() {
        System.out.print("模仿");
    }
}

class chicken extends rat {
    public void skill() {
        System.out.print("啄食");
    }
}

class dog extends rat {
    public void skill() {
        System.out.print("游泳");
    }
}

class pig extends rat {
    public void skill() {
        System.out.print("吃");
    }
}
```

### 优点

既沿袭了父类的方法名，又实现了子类的扩展

### 总结

> 1. 方法的重写能够在不新增方法的情况下实现子类的扩展
> 2. 方法重写要求方法声明格式和父类完全一致（访问修饰符不能小于父类）
> 3. `@Overrid`关键字用来开启格式检测，如果不一致就会报错
