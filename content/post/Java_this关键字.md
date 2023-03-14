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
