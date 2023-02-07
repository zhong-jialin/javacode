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
## 成员方法
在某些情况下，我们要需要定义成员方法，比如人类：除了有一些特定的属性外，还有一些行为比如：说话、跑步、通过学习..、做计算题等。这时候需要用成员方法才能完成。现在要求对Person类完善。
 * 成员方法快速入门   
  1. 添加speak成员方法，输入我是人。
  2. 添加cal01成员方法，计算出1+..+1000的结果。
  3. 添加cal02成员方法，接受一个n 计算从1-n的和。
  4. 添加getSum成员方法，计算两个数的和。
```
public class Method1 {
    public static void main(String[] args) {
        Person p1 = new Person();
        p1.speak();
        p1.cal01();
        p1.cal02(10);
        int returnsum = p1.getSum(10,20);
        System.out.println(returnsum);
    }
}
class Person{
    String name;
    int age;
    //1. public 公开方法  void方法没有返回值 speak方法名 （）里面为空：没有传入的参数
    public void speak(){
        System.out.println("我是人");
    }
    public void cal01(){
        int res = 0;
        for (int i = 1; i <= 1000; i++) {
            res +=i;
        }
        System.out.println(res);
    }
    public void cal02(int n){
        int res = 0;
        for (int i = 1; i <= n ; i++) {
            res += i;
        }
        System.out.println(res);
    }
    public int getSum(int a,int b){
        int sum = a+b;
        return sum;
    }
}
```

* 方法调用机制原理（cal02）
  ![原理](https://img-blog.csdnimg.cn/ab53e0b014f64b788ae19e338036df46.png "方法调用机制原理（cal02）")

* 用成员方法遍历一个数组，输出数组的元素值。
```
      public static void main(String[] args) {
        int[][] map = {{0,1,2},{3,4,5},{6,7,8}};
        method m1 = new method();
        m1.traverse(map);
    }

    class method{
      public void traverse(int[][] map){
        for (int[] ints : map) {
            for (int anInt : ints) {
                System.out.print(anInt + "\t");
            }
            System.out.println(" ");
        }
    }
 ```
* 跨类方法调用
```
  public class MethodDetail01 {
    public static void main(String[] args) {
        a a = new a();a.sayOk();a.m1();}}
class a{
    public void print(int n){
        System.out.println("print use"+ n);}
    public void sayOk(){
        print(10);System.out.println("sayOk use");}
    //跨类调用方法
    public void m1(){b b = new b();b.hi();}
}
class b{
    public void hi(){System.out.println("b 类调用12");}
}
```
* 成员方法穿参机制    
  1. 基本数据类型的传参机制
```public class 基本数据传参机制 {
    public static void main(String[] args) {
        swap sw = new swap();
        int a = 10;
        int b = 20;
        //值传递
        sw.swap1(a,b);
        System.out.println("a=" + a + "; b=" + b);

        //地址传递
        int[] arr = {1,3,4};
        sw.adress(arr);
        System.out.println(arr[0]);
    }
  class swap{
    public void swap1(int a,int b){
        int temp = a;
        a = b;
        b = temp;
    }
        public void adress(int[] arr){
        arr[0] = 200;
        System.out.println(arr[0]);

    }
  }
  ```
  