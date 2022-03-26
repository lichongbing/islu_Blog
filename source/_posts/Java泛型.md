---
title: Java泛型
author: 闲花
img: "https://files.islu.cn/article/JavaT.jpg"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java泛型
keywords: "Java,Java泛型,泛型概述,泛型优缺点,泛型格式,泛型方法,泛型推断,泛型知识点总结"
essay: false
summary: Java泛型知识点总结
abbrlink: 42613
date: 2021-03-24 12:47:38
update: 2021-03-24 12:47:38
---

## 泛型

### 概述

Java 泛型是 JavaSE1.5 中引入的一个新特性，其本质是参数化类型，也就是说所操作的数据类型被指定为一个参数（type  parameter）这种参数类型在定义的时候是宽泛的，而在使用的时候是确定的。可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。

### 泛型的优点

```shell
1、提高了程序的安全性(类型安全)
2、提高了程序的可扩展性、可重用性
3、将运行期遇到的问题转移到了编译期
4、省去了类型强转的麻烦(Object类对象)
```

### 泛型格式

```java
泛型标识符：<自定义无意义英文大写单字母占位符>
    常用格式：
        <T> Type
        <E> Element
        <K> Key
        <V> Value

泛型类：把泛型定义在类上
    格式:class 类名<泛型类型1,…>
        【注意】泛型类型必须是引用类型

泛型方法：把泛型定义在方法上
    格式:public <泛型类型> 返回类型 方法名(泛型类型 .)

泛型接口：把泛型定义在接口上
    格式:public  interface 接口名<泛型类型1…>
```

### 泛型方法

案例代码 1

```java
public class GenericityMethodDemo {
    public static void main(String[] args) {
        System.out.println(getData(100));
        System.out.println(getData("Java"));
        System.out.println(getData('A'));
        System.out.println(getData(false));
    }

    /**
     * 泛型方法
     * 格式：
     *         泛型限定符 返回值类型 方法名(泛型类型 参数名) {}
     *
     * @param <T> 泛型限定符
     * @param t 任意类型的参数
     * @return 返回任意类型参数
     */
    public static <T> T getData(T t) {
        return t;
    }
}
```

案例代码 2

```java
public class GenericityMethodDemo2 {
    public static void main(String[] args) {
        Integer[] intArr = {1, 2, 3};
        String[] stringArr = {"4", "5", "6"};

        // 自定义学生类，其中包含name和age两个成员变量
        Student[] students = {new Student("张三", 1), new Student("李四", 2), new Student("王五", 3)};

        printArray(intArr);
        printArray(stringArr);
        printArray(students);
    }

    /**
     * 遍历任意类型的数组
     *
     * @param <T> 泛型限定符
     * @param t 任意类型的数组
     */
    public static <T> void printArray(T[] t) {
        for (int i = 0; i < t.length; i++) {
            System.out.println(t[i]);
        }
    }
}
```

【注意】

```shell
1、要求形式参数列表中必须有一个参数是当前自定义泛型，因为需要通过参数来约束当前方法运行过程中泛型对应的具体数据类型是哪一个

2、返回值类型可以使用自定义泛型，而且是被形式参数列表中传入的泛型对应具体的数据类型控制

3、方法体内也可以使用自定义泛型，同时也是被参数当中泛型对应具体数据类型约束监控
```

### 泛型类

```java
public class GenericityClassDemo {
    public static void main(String[] args) {
        Number<Integer> num1 = new Number<Integer>(100);
        Number<String> num2 = new Number<String>("100");
        System.out.println(num1.getT());
        System.out.println(num2.getT());
    }
}

/**
 * 泛型类，把泛型定义到类上，整个类内都可以使用。是对泛型方法的封装
 * @param <T> 泛型标识符
 */
class Number<T> {
    private T t;

    // Constrator、setters、getters
}
```

【注意】

```shell
1、类内可以直接使用对应的类名声明泛型
2、类内使用的泛型具体数据类型是在创建当前类对象时约束
3、在创建当前类对象时没有约束泛型对应的具体数据类型，那么所有使用到泛型的位置都是Object类型，有悖于泛型使用原则
4、如果类声明过了泛型，那么类中所有使用此泛型的方法都同时被声明，即无法使用其他类型
5、泛型类中定义的静态方法不能直接使用类声明的泛型，因为泛型需要在创建对象时声明，而静态方法在类加载时就加载完成，此时泛型还没有声明。如果静态方法想要使用泛型，只能自己声明自己使用
```

泛型接口

案例代码 1

```java
interface USB {}

class Mouse implements USB {}

class Keyboard implements USB {}

interface PC<T> {
    // 接口中的常量不能使用泛型

    T use(T t);
}

/*
 *  实现类实现接口时不指定泛型类型,
 *  需要在创建对象时明确
 */
class MyPC<T> implements PC<T> {
    @Override
    public T use(T t) {
        return t;
    }
}

/*
 * 实现类实现接口时，接口中泛型的类型已经明确，
 * 实现的方法也是明确的
 */
class YourPC implements PC<Mouse> {
    @Override
    public Mouse use(Mouse t) {
        return t;
    }
}

public class GenericityInterfaceDemo {
    public static void main(String[] args) {
        // 创建对象时明确泛型的类型
        MyPC<Keyboard> myPC = new MyPC<Keyboard>();

        Keyboard keyboard = myPC.use(new Keyboard());

        System.out.println(keyboard);

        System.out.println("-----------------");

        // 声明类时已经明确泛型的类型，所以这里的类型已经是明确的
        YourPC yourPC = new YourPC();

        Mouse mouse = yourPC.use(new Mouse());

        System.out.println(mouse);
    }
}
```

案例代码 2

```java
/**
 * 自定义一个比较器接口
 * @param <T> 泛型
 */
interface Comparable<T> {
    /**
     * 这是一个比较方法，实现类应该实现这个方法以达到比较的目的
     *
     * @param t 传入被比较的对象
     * @return 负整数、零或正整数，根据此对象是小于、等于还是大于指定对象。
     */
    public abstract int compareTo(T t);
}
/**
 * 自定义父类，实现比较器接口
 */
class Father implements Comparable<Father>{
    private String name;
    private int age;

    // Constrator、setters、getters

    @Override
    public int compareTo(Father f) {
        return this.age - f.age;
    }
}

public class GenericityInterfaceDemo {
    public static void main(String[] args) {
        Father father1 = new Father("小明父亲", 30);
        Father father2 = new Father("小红父亲", 29);

        if (father1.compareTo(father2) < 0) {
            System.out.println("小红父亲年长：" + father2.getAge());
        } else {
            System.out.println("小明父亲年长：" + father1.getAge());
        }
    }
}
```

【注意】

```shell
1、接口中的成员变量不能使用泛型，因为static、final
2、泛型接口的实现类可以指定泛型的类型，也可以不指定，如果在实现类中明确了数据类型，创建对象时就不需要再进行明确
```

### 泛型通配符

> 在泛型中，？ 表示未知类型，被称为通配符。通配符可以在各种情况下使用：可以作为形式参数、成员变量、局部变量的类型，也可以作为返回值类型。但是，通配符不能用于泛型方法调用、泛型类实例创建对象或者父类的类型实际参数

表示全部类型，类似 Object。区别于 T，T 只是占位符，而 ？是数据类型

```java
<?>
```

【使用场景】

```shell
1、当一个方法可以用Object类提供的功能来实现时，泛型通配符是使用的

2、若代码使用了泛型类中的方法，而这些方法又是不依赖于参数化类型的，可以使用泛型通配符
```

案例代码

```java
class Grade<T> {
    private T t;

    // Constructor、setter and getter、toString

    public void show() {
        System.out.println("show" + this);
    }
}

class School {
    // 这里使用泛型通配符，表示可以传入任意类型
    public void showGrade(Grade<?> grade) {
        grade.show();
    }
}

public class GenericityWildCardDemo {
    public static void main(String[] args) {
        School school = new School();

        school.showGrade(new Grade<Student>(new Student()));
        school.showGrade(new Grade<Teacher>(new Teacher()));
    }
}
```

#### 泛型上限

表示以 T 为父类的所有子类（包括父类）

```java
<? extends T>
```

#### 泛型下限

表示以 E 为子类的所有父类（包括子类）

```java
<? super E>
```

案例代码

```java
class School {
    public void showGrade(Grade<?> grade) {
        grade.show();
    }

    // 泛型上限，Person类本身及其子类都可以使用
    public void showExtends(Grade<? extends Person> grade) {
        System.out.println(grade);
    }

    // 泛型下限，Person类本身及其父类都可以使用
    public void showSuper(Grade<? super Person> grade) {
        System.out.println(grade);
    }
}

public class GenericityWildCardDemo {
    public static void main(String[] args) {
        School school = new School();

        school.showGrade(new Grade<Student>(new Student()));
        school.showGrade(new Grade<Teacher>(new Teacher()));

        // 泛型上限，可以声明子类的类型
        school.showExtends(new Grade<Student>());
        // 泛型下限，可以声明父类的类型
        school.showSuper(new Grade<Object>());
    }
}
```

### 泛型推断

> JDK1.7 新特性，可以省略实例化对象时尖括号内的类型

案例代码

```java
public class GenericityInferDemo {
    public static void main(String[] args) {
        // 泛型推断
        Grade<Student> grade = new Grade<>();

        // 得到对应的类型
        Student student = grade.getT();
    }
}
```

### 总结

> 1、泛型就是泛化的类型，本质是参数化类型，是 jdk1.5 引入的新特性，用在类、接口和方法上，即泛型类，泛型接口和泛型方法
>
> 2、为了解决利用继承 Object 来实现通用性导致的强制类型转换和可能发生的类型转换异常的问题。
>
> 3、泛型的好处是确保了编译时期的类型安全，和避免了强制类型转换的麻烦
>
> 4、缺陷是因为泛型使用了类型擦除机制，jvm 运行之前会将泛型信息擦除掉，这样做是为了兼容 jdk1.5 之前的代码，但是也会导致通过反射可以跳过泛型的问题，因为运行期间并没有泛型的限制
>
> 5、泛型通配符？代表任意类型，泛型上限<? extends T>，泛型下限<? super T>
>
> 6、jdk1.7 新特性泛型推断，声明变量时定义过泛型得话，在实例化对象时可以省略类型，但是还要加<>，否则还是原类型
