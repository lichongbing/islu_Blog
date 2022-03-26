---
title: Java面向对象
author: 闲花
img: "https://files.islu.cn/article/JavaObject"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java面向对象
keywords: "Java面向对象概念和特征,java面向对象,java基础,java特征"
summary: Java面向对象概念和特征
abbrlink: 28848
date: 2021-03-15 14:47:42
update: 2021-03-15 14:47:42
---

# Java 面向对象

## 面向对象概念

### 什么是 Object 对象对象

相当于中文语义”东西”。Object 是指一个具体事物实例，比如飞机、狗、运气、哲学等等看得见的，看不见的，有形的，无形的，具体的，抽象的都是对象，总之“一切皆 object”。

### 面向对象 ObjectOriented

面向对象是指面向客观事物之间的关系。人类日常的思维方式是面向对象的，自然界事物之间的关系是对象与对象之间的关系。

**优点**

- 直观，高效，与人类的思维习惯一致
- 信息隐藏，提高了程序的可维护性和安全性
- 提高了程序的可重用性

### 面向对象定义

首先根据客户需求抽象出业务对象；

然后对需求进行合理分层，构建相对独立的业务模块；

之后设计业务逻辑，利用多态、继承、封装、抽象的编程思想，实现业务需求

最后通过整合各模块，达到高类聚、低耦合的效果，从而满足客户要求

### 面向对象分析 OOAOOA/面向对象设计 OODOOD

OOADObjectOrientAnalysisDesign 面向对象分析和设计，面向对象分析不设计 ObjectOrientAnalysisDesign 面向对象分析和设计，面向对象分析不设计是现在软件企业广为采用的一项有效技术。OOAD 方法要求在设计中要映射现实世界中指定问题域中的对象和实体，例如：顾客、汽车和销售人员等。这就需要设计要尽可能低接近现实世界，即以最自然的方式表述实体。

> **优点：**为能够构建与现实世界相对应的问题模型，并保持他们的结构、关系和行为模式

### 面向对象概念

```shell
1、类型(类)指一个名词概念，如：客人、菜品、厨师

2、引用(变量)指引用具体概念实例的代词，如：某人、特价菜

3、对象(东西)指具体概念的个体实例，如：张三丰是个人、一盘大盘鸡
    如上三者关系之间的关系可以体现为：“今天的特价菜是一盘大盘鸡”
4、行为(方法)

5、多态 行为或引用，在具体情形下会发生变化的现象。
    如：“一只动物”可以是“一匹马”、“一头驴”、“一只猴子”，多态的
6、封装 任何对象实例都是尽可能封装，减少暴露，它的实现细节对你是透明的(看不到的)。比如：只能看到汽车的壳子、轮胎等，看不到发动机

7、继承 概念的继承关系
```

### 面向对象思想

```shell
1、面向对象是基于面向过程的编程思想

2、万物皆对象

3、对象具有唯一性

4、任何对象都具有一定的特征和行为；特征是事物的基本描述，行为是事物的功能

5、类是一组相关的属性和方法的集合，是一个抽象的概念

6、对象是类的具体存在

7、在一组相同或相似的对象中，抽取出共性的特征和行为，保留所关注的部分就是类的抽取

8、类是模板、图纸，通过类创造的对象就是实体
```

## 面向对象特征

面向对象的编程语言有封装、继承、抽象、多态等四个主要的特征

### 封装

#### 概述

是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。核心是归纳总结

封装是保证软件部件具有优良的模块性的基础。

封装的目标：实现软件部件的“高内聚、低耦合”，防止程序相互依赖性而带来的变动影响。

面向对象的封装就是把描述一个对象的属性和行为的代码封装在一个“模块”中，也就是一个类中，属性用变量定义，行为用方法进行定义，方法可以直接访问同一个对象中的属性。通常情况下，只要记住让变量和访问这个变量的方法放在一起，将一个类中的成员变量全部定义成私有的，只有这个类自己的方法可以访问到这些成员的变量，这就基本实现了对象的封装，就很容易找到分配到这些类的方法了，就基本上算是会面向对象的编程了。

> 把对同一事物进行操作的方法和相关的方法放在同一个类中，把方法和它操作的数据放在同一个类中。

#### 特点

> 提高代码的复用度、安全性，不必关心具体细节，便于开发

#### JavaBean 规范化封装

```shell
1. 要求Java中的所有实体类成员变量全部私有化，最少提供一个无参数构造方法，对应成员变量实现setter和getter方法
2. JavaBean规范，是为了后期开发汇总更好的代码适配度，提高代码运行的统一性，能够满足框架的使用
3. JavaBean规范只是一个规范，而且是作为一个基础规范，操作都是可以使用快捷键来完成的！！！
class Person {
    private String name;
    private int age;
    private char sex;
    private boolean alive;

    public Person() {}

    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }

    public char getSex() {
        return this.sex;
    }

    public boolean isAlive() {
        return alive;
    }

    public void setAlive(boolean alive) {
        this.alive = alive;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }
}
```

### 继承

#### 概念

把多个类中相同的成员给提取出来定义到一个独立的类中。然后让这多个类和该独立的类产生一个关系，这多个类就具备了这些内容。这个关系叫继承。

```java
关键字：extends

格式:
    class Son extends Father {

    }

//一个孩子只能有一个父亲
//一个父亲可以有多个孩子
```

#### 特点

> 1. Java 为单继承，一个类只能有一个直接父类，但可以多级继承，属性和方法逐级叠加
> 2. 构造方法只可服务于本类，不可继承，子类执行构造方法前会默认调用父类的无参构造方法。可以通过 super 去访问父类的构造方法
> 3. private 修饰的属性和方法不能被继承

#### extends

```java
public class Demo {
    public static void main(String[] args) {
        // 创建一个父类对象
        Father father = new Father();

        // 父类调用父类的属性和方法
        father.name = "父";
        System.out.println(father.name);
        father.game();

        System.out.println("-------------");

        // 创建一歌子类对象
        Son son = new Son();

        // 子类调用子类的属性和方法
        son.age = 16;
        System.out.println(son.age);
        son.study();

        // 子类调用父类的属性和方法(public修饰)
        son.name = "子";
        System.out.println(son.name);
        son.game();


        /*
         * 子类调用父类private修饰的属性和方法
         *
         * 报错
         * The field Father.suffer is not visible
         * The method cook() from the type Father is not visible
         *
         * 由此可知子类不能调用父类私有化的属性和方法
         */
//        son.suffer = 10;
//        son.cook();
    }
}

public class Father {
    public String name;

    private int suffer;

    public void game() {
        System.out.println("下棋");
    }

    private void cook() {
        System.out.println("做饭");
    }
}

public class Son extends Father{
    public int age;

    public void study() {
        System.out.println("子类 -- 学习");
    }
}
```

#### 优点

> 1. 提高了代码的复用性
> 2. 提高了代码的维护性
> 3. 让类与类之间产生了一个关系，是多态的前提

#### 缺点

> 1. 让类的耦合性增强。这样某个类的改变，就会影响到其他和该类相关的类
> 2. 打破了封装性

#### 总结

> 1. Java 中只有单继承
> 2. 子类可以继承父类的非私有属性和方法（非 private 修饰的）
> 3. 执行子类的构造方法前会默认执行父类的无参构造方法

### 抽象

不能实例化的类就是抽象类，用 abstract 修饰

##### 构成

```java
abstract class 类名 {
    成员变量
    构造方法
    成员方法
        非抽象方法
        抽象方法
}
```

##### 要求

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

### 多态

**二者具有直接或间接的继承关系时，父类引用指向子类对象，从而产生多种形态；接口的引用指向实现接口的类对象也是多态**

#### 特点

多态场景下，父类引用调用方法，如果被子类重写过，优先执行子类重写过后的方法

```java
public class testCar{
    public static void main(String[] args) {
        // 父类引用指向子类对象
        Vehicle vehicle = new Car();

        // 优先执行子类重写过的方法
        vehicle.run();    // Car run！！！
    }
}
class Vehicle {
    public void run() {
        System.out.println("Vehicle run！！！");
    }
}
class Car extends Vehicle {
    @Override
    public void run() {
        System.out.println("Car run！！！");
    }
}
```

#### 应用场景一

使用父类作为方法形参实现多态，使方法参数的类型更为宽泛

```java
public class TestCar {
    public static void main(String[] args) {
        Vehicle vehicle = new Car();
        vehicle.type = "小汽车";

        Bike bike = new Bike();
        bike.type = "自行车";

        Bus bus = new Bus();
        bus.type = "公交车";

        Employee employee = new Employee("你的迪丽热巴");
        employee.goHome(vehicle);
        employee.goHome(bus);
    }
}

class Employee {
    String name;

    public Employee() {
    }

    public Employee(String name) {
        this.name = name;
    }

    public void goHome(Vehicle vehicle) {
        System.out.println(this.name + "乘坐" + vehicle.type + "交通工具回家");
    }
}

class Vehicle {
    String type;

    public void run() {
        System.out.println("Vehicle run！！！");
    }
}

class Bus extends Vehicle {
    @Override
    public void run() {
        System.out.println("Bus run！！！");
    }
}

class Car extends Vehicle {
    @Override
    public void run() {
        System.out.println("Car run！！！");
    }
}

class Bike extends Vehicle {
    @Override
    public void run() {
        System.out.println("Bike run！！！");
    }
}
```

#### 应用场景二

使用父类作为方法返回值实现多态，使方法可以返回不同子类对象

```java
public Vehicle buyVehicle(int money) {
        Vehicle vehicle = null;

        if (money >= 100) {
            Bus bus = new Bus();
            bus.speed = 60;
            bus.price = 1230000.0;
            bus.seatNum = 16;
            bus.type = "公交车";
            vehicle = bus;

        } else if (money >= 30) {
            Car car = new Car();
            car.price = 310000.0;
            car.speed = 90;
            car.type = "小汽车";
            car.brand = "BMW";
            vehicle = car;

        } else if (money >= 1) {
            Bike bike = new Bike();
            bike.type = "捷安特自行车";
            bike.speed = 40;
            bike.price = 2000.0;
            bike.color = "红色";
            vehicle = bike;
        }

        return vehicle;
    }
```

#### 向上装箱与向下拆箱

```java
class Animal{}

class Cat extends Animal{}

class Dog extends Animal{}

class Fish extends Animal {}

public class Test {
    public static void main(String[] args) {
        showAnimal(new Animal());    // code.polymorphic.animal.Animal@7852e922
        // 向上转型
        showAnimal(new Cat());    // code.polymorphic.animal.Cat@4e25154f
        // 向上转型
        showAnimal(new Dog());    // code.polymorphic.animal.Dog@70dea4e
        // 向上转型
        showAnimal(new Fish());    // code.polymorphic.animal.Fish@5c647e05

        System.out.println("----------------------");

        Animal animal = getAnimal();
        // 向下转型
        Cat cat = (Cat) getCat();
        // 向下转型
        Dog dog = (Dog) getDog();
        // 向下转型
        Fish fish = (Fish) getFish();

        System.out.println(animal);    // code.polymorphic.animal.Animal@33909752
        System.out.println(cat);    // code.polymorphic.animal.Cat@55f96302
        System.out.println(dog);    // code.polymorphic.animal.Dog@3d4eac69
        System.out.println(fish);    // code.polymorphic.animal.Fish@42a57993
    }

    /**
     * 展示动物
     * @param animal
     */
    public static void showAnimal(Animal animal) {
        System.out.println(animal);
    }

    /**
     * 得到动物
     * @return 返回一个Animal对象
     */
    public static Animal getAnimal() {
        return new Animal();
    }

    /**
     * 得到猫
     * @return 返回一个Cat对象
     */
    public static Animal getCat() {
        return new Cat();
    }

    /**
     * 得到狗
     * @return 返回一个Dog对象
     */
    public static Animal getDog() {
        return new Dog();
    }

    /**
     * 得到鱼
     * @return 返回一个Fish对象
     */
    public static Animal getFish() {
        return new Fish();
    }
}
```

#### instanceof 关键字

用于判断当前对象是否是某个类，或者其子类、实现类的实例。如果是返回 true，否则返回 false。

```
/**
 * 动物类
 */
class Animal {
}

/**
 * 老虎类
 */
class Tiger extends Animal {

}

/**
 * 熊猫类
 */
class Panda extends Animal {

}

/**
 * 猴子类
 */
class Monkey extends Animal {

}

public class AnimalDemo {
    public static void main(String[] args) {
        Animal ani = getAnimal();

        if (ani instanceof Panda) {
            // ani一定是panda对象或子类对象
            Panda panda2 = (Panda) ani;
            System.out.println("这是熊猫：" + panda2);
            showPanda(panda2);
        } else {
            System.out.println("这是动物：" + ani);
        }
    }

    // 获取动物，返回一个Panda对象
    public static Animal getAnimal() {
        return new Panda();
    }

    // 展示熊猫对象
    public static void showPanda(Panda panda) {
        System.out.println(panda);
    }
}
```

【注意】**使用 instanceof 关键字做判断时， instanceof 操作符的左操作数必须和右操作数存在继承或实现关系**

#### 总结

> 1. 父类引用指向子类对象，接口引用指向实现类对象
> 2. instanceof 用以比较对象是否是类或父类的实例，接口的实现类

## 访问权限权限修饰符

### Java 中的访问修饰符

|           | 类内部 | 同包下 | 子类中 | 非同包 |
| --------- | ------ | ------ | ------ | ------ |
| public    | √      | √      | √      | √      |
| protected | √      | √      | √      | ×      |
| 默认不写  | √      | √      | ×      | ×      |
| private   | √      | ×      | ×      | ×      |

### public 公共的公共的关键字

### protected 受保护的受保护的关键字

### private 私有的私有的关键字

```java
1、可以修饰成员变量和成员方法

2、被private修饰的变量和方法仅本类中可用

3、被private修饰的变量需要提供get、set方法供类外调用使用

4、boolean类型的 get 方法比较特殊：

    public boolean isName(String name){
        return name;
    }
```

> 在使用 Eclipse 写 Java 程序同时按住 shift+Alt+s 选择“Generate Getters and Setters”可以自动写出 set、get 的方法

```java
public class Dog {
    private String name;
    int age;
    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    private void function() {
        System.out.println("method be execute!");
    }

    public void executeFunction() {
        this.function();
    }
}
```

### 总结

> 1. 般我们最常用的就是 private 和 public，建议任何情况下都使用访问修饰符对变量和方法进行限制
> 2. public 权限最高，整个项目中都可以访问（同一个项目），private 权限最小，只能在本类中使用
> 3. 被 private 修饰的变量和方法可以通过提供公共的方法对其进行访问

## 匿名对象

### 概述

没有名字的对象，是对象的一种简化表示形式

### 特性

一次性，每次使用都是一个新的对象

### 使用情景

> 1、对象调用方法仅使用一次，然后等待销毁
>
> 2、作为实际参数传递

```java
public class TestDog{
    public static void main(String[] args) {
        // 对象调用方法仅使用一次
        new Dog().sleep();

        // 作为实际参数传递
        useDog(new Dog());
    }

    public static void useDog(Dog dog) {
        dog.sleep();
    }
}

class Dog {
    String name;
    int age;

    public void sleep() {
        System.out.println("小狗睡觉.....");
    }
}
```

### 优点

提高开发效率，简化代码结构

## 类和对象

### 类

类是对某一类事物的描述，是抽象的、概念上的定义。**类是模板，包含了一类事物所共有的特征属性属性和行为方法方法**

> 属性描述：学号、姓名、性别、年龄、身高、体重、地址、电话、微信、QQ…
>
> 行为描述：吃饭、睡觉、上班、学习、娱乐…

### 对象

**对象是类的具体体现（**[**属性和方法**](https://localhost:63342/ialoe.github.io-master/posts/36.html?_ijt=4djrf4sgdibf0v57aogg3jvm4k)**），是具体的、独一无二的个体。**

以班长为例：

> 属性描述：班长的学号、班长的姓名、班长的身高…
>
> 行为描述：班长吃饭、班长睡觉、班长学习…

### 类和对象的关系

类是对象的抽象，对象是类的具体实现

### 类的定义

类是一种自定义的数据类型

```java
格式：
    class 类名 {
        成员变量;// Fieldi

        成员方法;// Method
    }

class：
    定义类的关键字

类名：
    大驼峰命名，首字母大写，见名知意
    类名就是一种数据类型（自定义引用的数据类型），就是模板的名字

成员变量（属性/特征描述）：
    定义在类中，方法外的变量，用来描述类的特征

成员方法（行为描述）：
    定义在类中，用来描述类的功能
```

### 总结

> Java 中的类和对象
>
> - 类是对象的抽象，具有公共的特征和行为，对象是类的具体实现，具有唯一的特征和行为

> 基础数据类型与类和对象
>
> - 类就是一种自定义的数据类型，由类名，属性和方法构成
> - 对象就是一种数据类型的数据，由对象名，属性和方法构成

> 类和对象的定义和使用
>
> - 格式和规范，一定要按照标准

> **注意**

```shell
大写开头的都是类
小写开头的都是变量
带()的都是方法
```
