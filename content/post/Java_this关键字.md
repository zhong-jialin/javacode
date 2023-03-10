---
title: "Java_this关键字"
date: 2023-03-14T20:44:34+08:00
categories: [
    "Java",
]
---
## this关键字
1. 什么是this
   在Javajvm 中Java会给每个对象分配一个this 代表当前对象
   例基本使用this 那个对象调用，this就代表那个对象
```
public class demo1 {
    public static void main(String[] args) {
        Test t1 = new Test("niubi",18);
        t1.getTest();

    }
}
class Test{
    private String name;
    private int age;
    public Test(String name,int age){
        this.name = name;
        this.age = age;
    }
    public void getTest(){
        System.out.println(name + ":" + age);
    }
}
```
2. jvm在内存中的this指向
![this指向](https://img-blog.csdnimg.cn/7d164c0141f84048b44eac34fb486e75.png "this在jvm的内存指向")

## this的注意事项和使用细节
1. 可以用来访问本类的属性，方法，构造器
2. 用于区分当前类的属性和局部变量
3. 访问成员的语法：this.方法名
4. 访问构造器语法：只能在构造器内部使用
5. 不能在类定义类的外部使用，只能在类定义的方法中使用
   
##### 访问成员的语法：this.方法名
```
public class 访问成员语法 {
    public static void main(String[] args) {
        T t1 = new T();
        t1.f2();
    }
}
class T{
    private String name = "niub";
    private int age;
    public T(){
        //在一个构造器中访问另一个构造器 必须放在第一行
        this("niui",18);
        System.out.println("T 构造器");
    }
    public T(String name,int age){
        System.out.println("T(canshu) 构造器");
    }
    public void f1(){
        String name =  "list";
        //在方法中不使用this默认使用最近的值
        System.out.println("normle"+ name);
        System.out.println("this name"+ this.name);
    }
    public void f2(){
        //第一种方法
        f1();
        //第二种方法
        this.f1();
    }
}
```
