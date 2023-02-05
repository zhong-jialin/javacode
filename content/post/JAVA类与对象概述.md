---
title: "JAVA类与对象概述"
date: 2023-02-02T19:30:43+08:00

categories: [
    "Java"
]
---
# 面向对象编程（基础部分）
* 类与对象
* 成员方法
* 成员方法传参机制
* 重载（overload）
* 可变参数
* 作用域
* 构造器
* this指向

## 类与对象案例
  * 有两只猫，{'小白','3岁','白色'}{'小花','100岁','花色'}，用户输入小猫名字显示信息，输入错误则显示没有这只猫。    
  * 案例中类与对象的关系示意图    
  ![类与对象关系](https://img-blog.csdnimg.cn/1c22bba349d74979b2f57fed04ae7e6b.png "类与对象关系")

  ```
  public class 对象创建及使用 {
    public static void main(String[] args) {
        //类实例化一只猫对象
        //cat1对象名  
        //new Cat()创建的空间是真正的对象
        Cat cat1 = new Cat();
        cat1.name = "小白";
        cat1.age = 3;
        cat1.color = "白色";

        Cat cat2 = new Cat();
        cat2.name = "小花";
        cat2.age = 100;
        cat2.color = "花色";
    }
}
//创建类
class Cat {
  //属性
    String name;
    int age;
    String color;
}
```   
  * 类和对象的区别和联系
1. 类是抽象的，代表一类事物，比如人，猫类，即它是数据类型
2. 对象是具体的，实际的，代表一个具体事务，是实例
3. 类是对象的模板，对象是类的一个个体，对应一个实例

  * 对象在内存中的存在形式    
  ![图片](https://img-blog.csdnimg.cn/5c8ee5a1156f4002b21fdcb2f071ee2f.png "对象在内存中的存在形式")    

## 属性/成员变量
1. 从概念或叫法上看： 成员变量 = 属性 = field(字段) (即 成员变量是用来表示属性的)
2. 属性是类的一个组成部分,一般是基本数据类型,也可以是引用类型(对象，数组)，在上一个案例中猫类的 int age 就是属性。
3. 属性的定义语法同变量：访问修饰符 属性类型 属性名
   public proctected 默认 private
4. 属性的定义类型可以为任意类型，包含基本类型或引用类型
5. 属性如果不赋值，有默认值，规则和数组一致。

## 类和对象
 * 类和对象的内存分配机制*
  ```
Person p1 = new Person();
p1.age=10;
p1.name = "13";
Person p2 = p1;
sout(p2.age)
问：p2.age = ? 及画出内存图。
  ```
![图片](https://img-blog.csdnimg.cn/d9d0d2b12e1448229475584d9839314a.png "对象内存图")
 * 2
  ```
    public static void main(String[] args) {
        Person a = new Person();
        a.age = 10;
        a.name = "110";
        Person b;
        b = a;
        System.out.println(b.name);
        b.age = 200;
        b = null;
        //b = null 时 b失去对象，无法获取a的对象属性 就会出错
        System.out.println(a.age);
        System.out.println(b.age);
    }
  ```



