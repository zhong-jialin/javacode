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
   
#### 访问成员的语法：this.方法名
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
####  Java——this 练习
1. 定义Person类，有name,age属性，冰提供compareTo比较方法，用于判断是否和另一个人相等，提供测试类TestPersion 用于测试，名字和年龄完全一样，就返回ture 否则返回false

```
public class Demo2 {
    public static void main(String[] args) {
        Person p1 = new Person("tom",15);
        Person p2 = new Person("jerry" ,16);
        System.out.println("p1比较p2" + p1.TestPersion(p2));
        // 使用p1时 tom 和 15 先传值给 方法定义的name和age
        // 在p1对象中把p2的值传给p1类对象的TestPerson方法
        //
    }
}
class Person{
    private String name; //tom
    private int age; //15
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    public boolean TestPersion(Person p){ //p.name = jerry age = 16
       return this.name.equals(p.name) && this.age == p.age;
    }
}
```
2. 定义方法max，实现求某个double数组的最大值，并返回。
```
public class MaxArray {
    public static void main(String[] args) {
        A01 max = new A01();
        double[] arr = {1.0,4.8,0,9.5,9.8};
        System.out.println(max.max(arr));
    }
}
class A01{
    public  double max(double[] arr){
        double max = arr[0];
        for (int i = 0; i < arr.length; i++) {
            if (max < arr[i]){
                max = arr[i];
            }
        }
        return max;
    }

}
```
3. 定义方法find，实现查找某字符串数组中的元素查找，并返回索引，如果找不到返回-1
```
public class FindArray {
    public static void main(String[] args) {
        String[] fstr = {"ff","gg","ee"};
        findf find = new findf();

        System.out.println("index = " + find.find("ee",fstr));
    }
}
class findf{
    public int find(String n,String[] arr){
        for (int i = 0; i < arr.length; i++) {
            if (n.equals(arr[i])){
                return i;
            }
        }
        return -1;
    }
}

```

4. 编写book，定义方法updatePrice，实现更改某本书的价格，如果价格>150，则改为150，如果价格>100,更改为100，否则不变。
```
public class bookUpPrice {
    public static void main(String[] args) {
        book bo = new book();
        bo.book("niubi",151);
        bo.info();
        bo.updatePrice();
        bo.info();
    }
}
class book{
    String name;
    double price;
    public void book(String name,double price){
        this.name = name;
        this.price = price;
    }
    public void updatePrice(){
        if (price>150){
            price = 150;
        }else if (price>100){
            price = 100;
        }
    }
    public void info(){
        System.out.println("书名1" + name + "价格" + price);
    }
}
```