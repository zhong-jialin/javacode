---
title: "Java 继承"
date: 2023-03-31T22:06:29+08:00
categories: [
    "Java",
]
---
### 面向对象编程-继承
* 继承基本介绍和示意图    
  继承可以解决代码复用，当多个类存在相同的属性和方法是，可以从这些类中抽象出父类，在父类中定义这些相同的属性和方法，子类不需要重新定义这些属性和方法，只需要通过extends来生命继承父类即可。
* 继承的基本语法    
  class son extend father{}
  1. 子类就会自动拥有父类定义的属性和方法
  2. 父类又叫超类，基类
  3. 子类又叫派生类

* 简单继承类
1. 目录 extendDemo ->Deom fu son
```
//DEMO 调用类
public class Demo {
    public static void main(String[] args) {
        son s = new son();
        s.method();
    }
}
// fu 父类
public class fu {
    public int age = 120;
    public void show(){
        System.out.println("use fu");
    }
}
//son 子类
public class son extends fu {
    public int height = 75;
    public int age = 12;
    public void method(){
        int age = 1;
        System.out.println(age); //age 调用最近的age变量
        System.out.println(this.age); //this.age 调用类的age变量
        System.out.println(super.age); //super.age 调用父类的age变量

    }
}
输出
1
12
120

进程已结束,退出代码0
```
* 继承的深入讨论
1. 子类继承的父类所有的方法和属性，但是父类的私有属性和方法子类无法访问，需要公共的方法访问。
```

```

