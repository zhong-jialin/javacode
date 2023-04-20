---
title: "Java集合"
date: 2023-04-20T20:44:57+08:00
categories: [
    "Java",
]
---

### 二、集合是什么？

* Java集合类存放在java.util包中，是一个用来存放对象的容器。

1. 集合只能存放**对象**。比如你存入一个int型数据66放入集合中，其实它是**自动转换成Integer类**后存入的，Java中每一种基本数据类型都有对应的引用类型。
2. 集合存放的都是**对象的引用**，而非对象本身。所以我们称**集合中的对象就是集合中对象的引用**。对象本身还是放在堆内存中。
3. 集合可以**存放不同类型，不限数量的数据类型**。

### 三、集合和数组的区别

1. 长度区别： 数组固定，集合可变
2. 内容区别： 数组可以是基本类型,也可以是引用类型,集合只能是引用类型
   * 基本数据类型：Boolean float char byte short int long  double
   * 引用类型： 类，接口类型，数组类型，枚举类型，字符串类型。
3. 元素内容： 数组只能存储同一种类型，集合可以存储不同类型。

### 四、集合框架

<https://img2018.cnblogs.com/blog/1175569/201908/1175569-20190813185822827-390071136.png>
上述所有的集合类，除了map系列的集合，即左边的集合都实现了Iterator接口。
Iterator是一个用来遍历集合中元素的接口，主要有hashNext()，next()，remove()三种方法。
它的子接口ListIterator在它的基础上又添加了三种方法，分别是add()，previous()，hasPrevious()。

1. 集合主要分为Collection和Map两个接口。
2. Collection又分别被LIst和set继承。
3. List被AbstractList实现，然后分为3个子类，ArrayList，LinkList和VectorList。
4. Set被AbstractSet实现，又分为2个子类，HashSet和TreeSet。
5. Map被AbstractMap实现，又分为2个子类，HashMap和TreeMap。
6. Map被Hashtable实现。

### 五、Collection集合的方法

```
package 集合;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;
import java.util.Iterator;

public class CollectionDemo {
    public static void main(String[] args) {
        Collection<String> array = new ArrayList<>();
        Collection<String> array1 = new ArrayList<>();
        array.add("a");
        array.add("b");
        array1.add("a");
        array1.add("b");
        //在集合末尾添加元素 conlog:a,b
        array.remove("a");
        //清楚在集合中与a相同的元素。
        System.out.println(array.contains("b"));
        //判断集合中是否有和b相同的元素 conlog：true
        System.out.println(array.isEmpty());
        //判断本类集合是否为空
        System.out.println(array.size());
        //返回集合元素个数
        array.addAll(array1);
        //吧array1集合中所有元素添加到array集合中
        System.out.println(Arrays.toString(array.toArray()));
        System.out.println("------------------------------");
        //吧本类集合所有元素返回为数组

        //集合专用迭代器
        Iterator<String>iterator = array.iterator();
        //hasNext()判断是否有下一个元素 next指针下移
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }

        System.out.println("------------------------------");
//        array.clear();
        //清楚本类所有元素
        for (String s : array) {
            System.out.println(s);
        }

    }
}
```

常用集合的分类：
Collection 接口的接口 对象的集合（单列集合）

* List 接口：元素按进入先后有序保存，可重复
  * LinkedList 接口实现类， 链表， 插入删除， 没有同步， 线程不安全
  * ArrayList 接口实现类， 数组， 随机访问， 没有同步， 线程不安全
  * Vector 接口实现类 数组， 同步， 线程安全
    * Stack 是Vector类的实现类
* Set 接口： 仅接收一次，不可重复，并做内部排序
  * HashSet 使用hash表（数组）存储元素
  * LinkedHashSet 链表维护元素的插入次序
  * TreeSet 底层实现为二叉树，元素排好序

Map 接口 键值对的集合 （双列集合）

* Hashtable 接口实现类， 同步， 线程安全
* HashMap 接口实现类 ，没有同步， 线程不安全-
  * LinkedHashMap 双向链表和哈希表实现
  * WeakHashMap
* TreeMap 红黑树对所有的key进行排序
* IdentifyHashMap
