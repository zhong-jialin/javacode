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




