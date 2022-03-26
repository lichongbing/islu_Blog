---
title: Java集合
author: 闲花
img: "https://files.islu.cn/article/JavaList"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - Java
  - Java集合
keywords: "Java集合知识点,Java,Java集合,List,Collection,Map,Set"
essay: false
summary: List、Collection、Map、Set 集合知识点
abbrlink: 21079
date: 2021-03-24 12:55:51
update: 2021-03-24 12:55:51
---

## List

### 概述

有序的 Collection ，可以根据索引操作元素，数据可重复

> ArrayList
>
> 可变长数组
>
> LinkedList
>
> 双向链表
>
> Vector
>
> 线程安全的可变长数组

### 增加方法

```java
boolean add(E e);
    List接口继承Collection接口 add方法，使用操作和Collection一致，并且这里采用的添加方式是【尾插法】

boolean add(int index, E e);
    List接口【特有方法】，在指定位置，添加指定元素

boolean addAll(Collection<? extends E> c);
    List接口继承Collection接口 addAll方法，使用操作和Collection一致，并且这里采用的添加方式是【尾插法】

boolean addAll(int index, Collection<? extends E> c);
    List接口【特有方法】，在指定下标位置，添加另一个集合中所有内容
public class Test {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<String>();

        arrayList.add("Hello");
        arrayList.add("World");
        arrayList.add("Android");

        arrayList.add(0, "Java");
        System.out.println(arrayList);

        List<String> al = new ArrayList<String>();

        al.add("ArrayList是线程不安全的可变长数组");
        al.add("LinkedList是双向链表：增删快，查询慢");

        al.addAll(arrayList);

        System.out.println(al);

        arrayList.addAll(0, al);

        System.out.println(arrayList);
    }
}
```

### 删除方法

```java
E remove(int index);
    List接口【特有方法】，获取指定下标位置的元素并删除

boolean remove(Object obj);
    List接口继承Collection接口方法。删除集合中的指定元素

boolean removeAll(Collection<?> c);
    List接口继承Collection接口方法。删除当前集合中和参数集合重复元素

boolean retainAll(Collection<?> c);
    List接口继承Collection接口方法。保留当前集合中和参数集合重复元素

clear();
    List接口继承Collection接口方法。清空整个集合中的所有元素
public class TestRemove {
    public static void main(String[] args) {
        List<Integer> al = new ArrayList<Integer>();

        al.add(1);
        al.add(2);
        al.add(3);
        al.add(4);

        System.out.println("删除指定下标位置为0的元素： " + al.remove(0));

        System.out.println("al : " + al);

        List<Integer> al1 = new ArrayList<Integer>();

        al1.add(4);
        al1.add(5);
        al1.add(6);

        System.out.println("al.removeAll(al1) : " + al.removeAll(al1));
        System.out.println("al : " + al);

        List<Integer> al2 = new ArrayList<Integer>();

        al2.add(5);
        al2.add(7);
        al2.add(6);

        System.out.println("al1.reatinAll(al2) : " + al1.retainAll(al2));

        System.out.println("al1 ： " + al1);

        al2.clear();

        System.out.println("al2.clear() ： " + al2);
    }
}
```

### 修改方法

```java
E set(int index, E e);
    List接口【特有方法】，使用指定元素替代指定下标的元素，返回值是被替换的元素
public class TestModify {
    public static void main(String[] args) {
        List<Character> al = new ArrayList<Character>();

        al.add('A');
        al.add('B');
        al.add('C');

        al.set(0, 'M');

        System.out.println(al); // [M, B, C]
    }
}
```

#### 查询方法

```java
int size();
    List接口继承Collection接口方法。获取集合中有效元素个数

boolean isEmpty();
    List接口继承Collection接口方法。判断当前集合是否为空

boolean contains(Object obj);
    List接口继承Collection接口方法。判断指定元素是否包含在当前集合中

boolean containsAll(Collection<?> c);
    List接口继承Collection接口方法。判断参数集合是不是当前集合在子集合

Object[] toArray();
    List接口继承Collection接口方法。获取当前集合中所有元素Object数组

E get(int index);
    List接口【特有方法】。获取指定下标对应的元素

List<E> subList(int fromIndex, int toIndex);
    List接口【特有方法】。获取当前集合指定子集合，从fromIndex开始，到toIndex结束。fromIndex <= 范围 < toIndex [)

int indexOf(Object obj);
    List接口【特有方法】。获取指定元素在集合中第一次出现位置

int lastIndexOf(Object o);
    List接口【特有方法】。获取指定元素在集合中最后一次出现的位置
public class TestGet {
    public static void main(String[] args) {
        List<String> al = new ArrayList<String>();
        al.add("Hello");
        al.add("World");
        al.add("Java");
        al.add("Android");
        al.add("Hello");

        List<String> al2 = new ArrayList<>();
        al2.add("Java");
        al2.add("Hello");

        System.out.println(al.size()); // 4
        System.out.println(al.isEmpty()); // false
        System.out.println(al.contains("Java")); // true
        System.out.println(al.containsAll(al2)); // true

        Object[] array = al.toArray();
        for (Object str : array) {
            System.out.println(str);
        }

        System.out.println(al.indexOf("World")); // 1
        System.out.println(al.lastIndexOf("Hello")); // 4

        System.out.println(al.get(0)); // Hello

        System.out.println(al.subList(1, 3)); // [World, Java]
    }
}
```

### LinkedList

#### 概述

> 底层数据结构是一个双向链表，查询慢，增删快

#### 方法

LinkedList 使用的方法都是从 List 接口实现而来的方法，需要了解的是 LinkedList 特有方法：

```java
void addFirst(E e);
    在当前链表开始位置加元素

void addLast(E e);
    在当前链表末尾添加元素

E getFirst();
    获取第一个Node节点元素数据

E getLast();
    获取末尾Node节点元素数据

E removeFirst();
    删除头节点

E removeLast();
    删除末尾节点
public class Test {
    public static void main(String[] args) {
        LinkedList<String> linkedList = new LinkedList<String>();

        linkedList.add("Buffer");
        linkedList.add("Balance");
        linkedList.add("Wizard");
        linkedList.add("Blanche");
        linkedList.add("Eve");

        linkedList.addFirst("Hello");
        linkedList.addLast("World");

        System.out.println(linkedList.getFirst());    // Buffer
        System.out.println(linkedList.getLast());    // Eve

        System.out.println(linkedList);    // [Hello, Buffer, Balance, Wizard, Blanche, Eve, World]

        System.out.println("移除头元素" + linkedList.removeFirst());    // 移除头元素Hello
        System.out.println("移除尾元素" + linkedList.removeLast());    // 移除尾元素World

        System.out.println(linkedList);    // [Buffer, Balance, Wizard, Blanche, Eve]
    }
}
```

### ArrayList

#### 概述

```java
List 接口的大小可变数组的实现。实现了所有可选列表操作，并允许包括 null 在内的所有元素。除了实现 List 接口外，此类还提供一些方法来操作内部用来存储列表的数组的大小。（此类大致上等同于 Vector 类，除了此类是不同步的。）
```

#### 特有方法

```java
void ensureCapacity(int minCapacity);
    如有必要，增加此 ArrayList 实例的容量，以确保它至少能够容纳最小容量参数所指定的元素数。

trimToSize();
    将此 ArrayList 实例的容量调整为列表的当前大小。节省空间
```

#### 效率

> 增删慢，查询快

```
增删慢
    增加慢
        1、数组当前容量无法满足添加操作，需要进行grow扩容方法执行，在扩容方法中，存在数组创建，数组数据拷贝。非常浪费时间，而且浪费内存。
        2、数组在添加数据的过程中，存在在指定位置添加元素，从指定位置开始，之后的元素整体向后移动。

    删除慢
        1、删除数据之后，从删除位置开始，之后的元素整体向前移动，移动过程非常浪费时间
        2、删除操作会导致数据空间的浪费，内存的浪费

    查询快
        ArrayList 底层是一个数组结构，在查询操作的过程中，是按照数组+下标的方式来操作对应的元素，数组+下标方式可以直接获取对应的空间首地址，CPU访问效率极高。
```

## Collection 接口

> Collection   层次结构中的根接口。Collection 表示一组对象，这些对象也称为 collection 的元素。一些 collection   允许有重复的元素，而另一些则不允许。一些 collection 是有序的，而另一些则是无序的。JDK 不提供此接口的任何*直接* 实现：它提供更具体的子接口（如 `Set` 和 `List`）实现。此接口通常用来传递 collection，并在需要最大普遍性的地方操作这些 collection。

### 增加方法

```java
boolean add(E e);
    添加当前集合约束的指定数据类型到当前集合中

boolean addAll(Collection<? extends E> c);
    添加另一个集合到当前集合中，要求添加集合中保存的元素必须是当前集合中保存元素本身或者其子类对象 【泛型的上限】
    class Dog extends Animal
    class Cat extends Animal
    class Tiger extends Animal
```

案例代码

```java
public class Test {
    public static void main(String[] args) {
        Collection<String> collection1 = new ArrayList<String>();
        Collection<String> collection2 = new ArrayList<String>();

        collection1.add("Java");
        collection1.add("Hello");

        collection2.add("Java");
        collection2.add("Hello");
        collection2.add("World");

        System.out.println(collection1);    // [Java, Hello]

        collection1.addAll(collection2);
        System.out.println(collection1);    // [Java, Hello, Java, Hello, World]
    }
}
```

### 删除方法

```java
boolean remove(Object obj);
    删除集合中的指定元素，删除成功返回true,未找到指定元素，无法删除返回
    false，并且在多个元素的情况下，删除找到的第一个元素。

boolean removeAll(Collection<?> c);
    在当前集合中删除两个集合的交集

boolean retainAll(Collection<?> c);
    在当前集合中保留两个集合的交集

void clear();
    清空整个集合中的所有元素
```

案例代码

```java
public class TestRemove {
    public static void main(String[] args) {
        Collection<String> collection1 = new ArrayList<String>();
        Collection<String> collection2 = new ArrayList<String>();

        collection1.add("Java");
        collection1.add("Hello");

        collection2.add("Java");
        collection2.add("Hello");
        collection2.add("World");

        collection1.remove("Hello");
        System.out.println(collection1);    // [Java]

        collection2.removeAll(collection1);
        System.out.println(collection2);    // [Hello, World]

        collection1.add("Hello");

        collection1.containsAll(collection2);
        System.out.println(collection1);    // [Java, Hello]
    }
}
```

### 查询方法

```java
int size();
    有效元素个数

boolean isEmpty();
    判断当前集合是否为空，是否存在有效元素

boolean contains(Object obj);
    判断指定元素是否在当前集合中存在

boolean containsAll(Collection<?> c);
    判断传入的参数集合是不是当前集合的子集合

Object[] toArray();
    返回集合中所有保存元素的Object类型数组
```

案例代码

```java
public class TestGet {
    public static void main(String[] args) {
        Collection<String> collection1 = new ArrayList<String>();
        Collection<String> collection2 = new ArrayList<String>();

        collection1.add("Java");
        collection1.add("Hello");

        collection2.add("Java");
        collection2.add("Hello");
        collection2.add("World");

        System.out.println(collection1.size());    // 2

        System.out.println(collection1.isEmpty());    // fasle

        System.out.println(collection1.contains("Java"));    //true

        System.out.println(collection2.containsAll(collection1));    // true

        Object[] array = collection1.toArray();
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}
```

### 迭代器

是用来获取集合中元素的另一种方式（遍历），依赖于集合存在

#### 获取迭代器的方法

```java
Iterator<E> iterator();
    获取迭代器对象，泛型对应的具体数据类型和集合中约束的泛型具体数据类型一致。
```

#### 其他方法

```java
boolean hasNext();
    判断当前集合中是否可以继续得到元素，(是否可以继续遍历)

E next();
    1. 获取迭代器当前指向的元素
    2. 将迭代器指向下一个元素

void remove();
    删除通过next方法获取到元素
        【注意】
        1、remove方法只能删除next方法获取到元素
        2、remove方法只能在next方法之后执行，且不能跨过一个next执行
        3、没有next不能使用remove
```

案例代码

```java
public class Test {
    public static void main(String[] args) {
        Collection<String> c = new ArrayList<String>();

        c.add("雪花纯生");
        c.add("修道院啤酒");
        c.add("1664");
        c.add("泰山精酿");
        c.add("时光精酿");

        /*
         * 根据当前集合，获取对应的迭代器对象
         *
         * 得到的迭代器对象会依据，当前集合中的所有元素进行一个规划操作。
         * 迭代器对于整个集合中的元素都是存在预期。
         */
        Iterator<String> iterator = c.iterator();

        /*
         * 迭代器遍历，利用迭代器的特征进行遍历操作
         */
        while (iterator.hasNext()) {
            // 获取每一个迭代器指向元素，并且展示
            String string = iterator.next();
            System.out.println(string);

            /*
             * 通过集合对象本身删除1664，对于迭代器而言，一脸懵逼，原本的规划
             * 没有了！！！并且集合没有告知迭代器数据发生了改变，迭代器继续按照
             * 原本的规划路径操作，保存！！！
             *
             * 对于集合在内存中占用的空间而言
             *     1. 集合对应的引用数据类型变量可以操作对应空间
             *     2. 迭代器可以操作对应的空间
             *
             * 对于集合和迭代器而言，【集合在内存中占用的空间】共享资源，在操作
             * 共享资源过程中，我们要多多考虑共享资源的冲突问题。
             * 后面课程中会讲到【多线程】
             */
            c.remove("1664");
        }

        /*
         Exception in thread "main" java.util.ConcurrentModificationException
                at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:909)
                at java.util.ArrayList$Itr.next(ArrayList.java:859)
                at com.qfedu.b_iterator.Demo3.main(Demo3.java:30)
         */
    }
}
```

## Map

> Map 接口允许以键集、值集或键-值映射关系集的形式查看某个映射的内容。映射顺序 定义为迭代器在映射的 collection 视图上返回其元素的顺序。某些映射实现可明确保证其顺序，如 TreeMap 类；另一些映射实现则不保证顺序，如 HashMap 类。
>
> 【重点】将键映射到值的对象。一个映射不能包含重复的键；每个键最多只能映射到一个值。

```java
public interface Map<K,V>
```

```java
interface Map<K, V>
--| class HashMap<K, V>
    重点！！！底层是哈希表
--| class TreeMap<K, V>
    底层是红黑树
```

### 增加方法

```java
V put(K key, V value);
    添加符合Map要求的键值对存入到双边队列中

void putAll(Map<? extends K, ? extends V> map)
    添加另一个Map到当前Map中，要求K是当前Map本身对应的K，或者其子类，V是当前Map本身对应的V，或者其子类
```

### 删除方法

```java
V remove(Object key);
    删除对应Key键值对
```

### 修改方法

```java
V put(K key, V value);
    使用value修改已存在的key对应的值
```

### 查询方法

```java
int size();
    Map双边队列个数
boolean isEmpty();
    判断当前Map双边队列中是否为空
boolean containsKey(Object key);
    判断指定Key是否存在
boolean containsValue(Object value);
    判断指定Value是否存在
Set<K> keySet();
    返回Map双边队列中所有Key对应的Set集合
Collection<V> values();
    返回Map双边队列中所有value对应Collection集合
```

### Map 中的 Entry

> Map 双边队列中把 Key 和 Value 进行一个封装操作，完全按照一个数据类型来处理。是 Map 中的一个成员接口，用于获取对应的键和值（参考 Collection 中的迭代器）

```java
interface Map.Entry<K,V>
```

案例代码

```java
Set<Map.Entry<K, V>> entrySet();
    返回值类型是Entry键值对形式数据的Set集合

Set<Map.Entry<K, V>>
    Map.Entry<K, V> Map接口的内部接口Entry，使用的泛型 K,V对应Map创建过程中约束的K,V
    因为返回值是Set集合，集合带有泛型 Set<Map接口中的内部接口Entry>

Entry 对应的方法
    K getKey();
        返回与此项对应的键
    V getValue();
        返回与此项对应的值。
    V setValue(V value);
        用指定的值替换与此项对应的值，返回与此项对应的旧值
public class TestEntry {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<String, Integer>();

        map.put("Buffer", 23);
        map.put("Balance", 23);
        map.put("Amy", 32);

        Set<Entry<String, Integer>> entrySet = map.entrySet();

        for (Entry<String, Integer> entry : entrySet) {
            System.out.println(entry.getKey() + " setVaule: " + entry.setValue(16));
            System.out.println(entry.getKey() + " : " + entry.getValue());
        }
    }
}
```

### HashMap

> 基于哈希表的 Map 接口的实现。此实现提供所有可选的映射操作，并允许使用 null 值和 null 键。（除了非同步和允许使用 null 之外，HashMap 类与 Hashtable 大致相同。）此类不保证映射的顺序

```java
public class HashMap<K,V>
```

案例代码

```java
public class TestHashMap {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<String, Integer>();

        map.put("Buffer", 23);
        map.put("Balance", 23);
        map.put("Amy", 32);

        System.out.println(map);

        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Candy", 33);
        hashMap.put("David", 29);

        hashMap.putAll(map);
        System.out.println(hashMap);

        hashMap.remove("Balance");
        System.out.println(hashMap);

        hashMap.put("Buffer", 16);
        System.out.println(hashMap);

        System.out.println("map.size() :" + map.size());

        System.out.println("map.isEmpty() : " + map.isEmpty());

        System.out.println("have Buffer : " + map.containsKey("Buffer"));

        System.out.println("have Buffer's age : " + hashMap.containsValue(16));

        Set<String> keySet = map.keySet();
        System.out.println(keySet);

        Collection<Integer> values = map.values();
        System.out.println(values);
    }
}
```

> 【注意】HashMap 添加自定义数据类型元素时需要重写其 equals 和 hashCode 方法

学生类

```java
public class Student {
    private String name;
    private int age;
    private char sex;

    // Constructor setter getter toString equals hashCode
}
```

测试类

```java
public class TestMap2 {
    public static void main(String[] args) {
        Map<Student, Integer> hashMap = new HashMap<Student, Integer>();

        hashMap.put(new Student("Buffer", 23, '男'), 1);
        hashMap.put(new Student("Balance", 23, '男'), 2);
        hashMap.put(new Student("Buffer", 22, '男'), 3);
        hashMap.put(new Student("Buffer", 23, '女'), 4);
        hashMap.put(new Student("Buffer", 23, '男'), 5);

        Set<Entry<Student, Integer>> entrySet = hashMap.entrySet();

        for (Entry<Student, Integer> entry : entrySet) {
            System.out.println(entry);
        }
    }
}
```

结果

```java
Student [name=Balance, age=23, sex=男]=2
Student [name=Buffer, age=23, sex=女]=4
Student [name=Buffer, age=22, sex=男]=3
Student [name=Buffer, age=23, sex=男]=5
```

### TreeMap

> 基于红黑树（Red-Black tree）的 NavigableMap 实现。该映射根据其键的自然顺序进行排序，或者根据创建映射时提供的 Comparator 进行排序，具体取决于使用的构造方法。

学生类

```java
public class Student {
    private String name;
    private int age;
    private char sex;

    // Constructor and setter、getter
}
```

Comparator 接口实现类

```java
public class MyCompare implements Comparator<Student> {

    /**
     * 返回两个学生的年龄差
     */
    @Override
    public int compare(Student o1, Student o2) {
        return o1.getAge() - o2.getAge();
    }

}
```

测试类

```java
public class TestTreeMap {
    public static void main(String[] args) {
        TreeMap<Student, Integer> treeMap = new TreeMap<Student, Integer>(new MyCompare());

        treeMap.put(new Student("Buffer",23,'男'), 1);
        treeMap.put(new Student("Buffer",22,'男'), 1);
        treeMap.put(new Student("Buffer",21,'男'), 1);

        System.out.println(treeMap);
        System.out.println(treeMap.size());
    }
}
```

## Set

### 概述

> 一个不包含重复元素的 Collection。存储元素的顺序无序。（注意区分添加顺序和存储顺序）

### HashSet

#### 概述

> 底层数据结构是哈希表，依赖 equals 方法和 hashCode 方法实现不可重复

学生类：需要重写 equals

和 hashCode

```java
public class Student {
    private String name;
    private int age;

    // Construator setter/getter toString

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + age;
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        Student other = (Student) obj;
        if (age != other.age)
            return false;
        if (name == null) {
            if (other.name != null)
                return false;
        } else if (!name.equals(other.name))
            return false;
        return true;
    }
}
```

测试类

```java
public class Test {
    public static void main(String[] args) {
        Set<Student> hashSet = new HashSet<Student>();

        hashSet.add(new Student("Buffer", 23));
        hashSet.add(new Student("Smoot", 22));
        hashSet.add(new Student("Wizard", 23));
        hashSet.add(new Student("Buffer", 23));
        hashSet.add(new Student("Buffer", 20));
        hashSet.add(new Student("Balance", 21));

        for (Student student : hashSet) {
            System.out.println(student);
        }
    }
}
```

结果

```java
Student [name=Smoot, age=22]
Student [name=Wizard, age=23]
Student [name=Balance, age=21]
Student [name=Buffer, age=23]
Student [name=Buffer, age=20]
```

> hashSet 底层哈希表结构存储元素时，会首先得到当前元素的哈希值，需要执行调用对应的 hashCode 方法，hash 方法中存在一个【移位运算】，一种特殊运算方式，用于根据当前对象的 hashCode 结果，计算该元素在底层哈希表中的存储位置。
>
> 【重点】如果元素 hashCode 值结果一致，那么它们保存对应的位置应该是一致的，会存入同一个空间，但是会进行 equals 比较，对象相同，【无法添加，对象不同，可以添加，但是需要避免】

### TreeSet

#### 概述

> 基于 TreeMap 的 NavigableSet 实现，底层数据结构是平衡二叉树。使用元素的自然顺序对元素进行排序（Comparable），或者根据创建 set 时提供的 Comparator 进行排序，具体取决于使用的构造方法。

Person 类

```java
package code.treeset;

public class Person {
    private String name;
    private int age;

    // Constructor setter/getter toString
}
```

Comparator 接口实现类

```java
public class MyCompare implements Comparator<Person> {

    // 通过年龄判断是否为同一个 Person
    @Override
    public int compare(Person o1, Person o2) {
        return o1.getAge() - o2.getAge();
    }
}
```

测试类

```java
public class TestPerson {
    public static void main(String[] args) {
        // 创建 TreeSet 集合时传入一个 Comparator 接口的实现类
        TreeSet<Person> treeSet = new TreeSet<Person>(new MyCompare());

        treeSet.add(new Person("Smoot", 22));
        treeSet.add(new Person("Buffer", 23));
        treeSet.add(new Person("Wizard", 23));
        treeSet.add(new Person("Balance", 21));

        System.out.println(treeSet);    // [Person [name=Balance, age=21], Person [name=Smoot, age=22], Person [name=Buffer, age=23]]
    }
}
```
