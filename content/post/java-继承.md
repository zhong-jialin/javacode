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
// fu lei
package 继承Demo2;

public class fu {
    public int n1 = 100;
    protected  int n2 = 200;
    int n3 = 300;
    private int n4 = 400;
    public int returnn4(){
        return n4;
    }
//    public fu(){
//        System.out.println("fu()");
//    }
    public fu(String name,int age){
        System.out.println("fu(String name,int age)");
    }
    public void test100(){
        System.out.println("test100");
    }
    protected void test200(){
        System.out.println("test200");
    }
    void test300(){
        System.out.println("test300");
    }
    private void  test400(){
        System.out.println("test400");
    }
    public void calltest400(){
        test400();
    }
}

// son lei
public class son extends fu{
  //当父类没有无参的构造器要手动调用super调用父类的构造器
  //指定使用父类的那个构造器完成对父类的初始化工作
    public son(){
        super("tom",18);
        System.out.println("son");
    }
    public void saook(){
        System.out.println(n1 + n2 + n3);
        test100();
        test200();
        test300();
        System.out.println(returnn4());
        calltest400();
    }
}

```
2. 子类在调用父类是会默认调用父类构造器。默认调用super()方法，如果父类没有无参构造器，必须用子类的构造器中用super去指定使用父类的那个构造器完成对父类的初始化工作，否则编译不会通过。
3. 如果希望指定去调用父类的构造器，要显式的调用一下
4. super使用时，要在放在构造器第一行
5. super() 和 this() 都是放在构造器第一行，但是两个方法不能同时出现。
6. 子类最多只能继承一个父类。
   
### 继承的本质分析
* 子类创建的内存布局
![内存](https://img-blog.csdnimg.cn/f631c64da9904edf809a442528038986.png "继承内存")   
#### 练习
1. 1
```
class  a{
    a(){
        a sout("a");
        a(String name){
            sout("a name)
        }
    }
}
class b extends a{
    b(){
        this("abc");
        sout("b");
    }
    b(String name){
        sout("b name");
    }
}
b b = new b(); 会输出什么
a,b name,b
```
2. 2
![](https://img-blog.csdnimg.cn/37656236ae894068a4b90f0a00bd590c.png "")

3. 编写computer类，包含cpu,内存 硬盘,getDetails方法用于返回Cumputer的详细信息。
   编写pc子类，继承computer类，添加特有属性【品牌brand】
   编写NotePad子类，继承computer类，添加特有属性【演示color】
   编写test类，在main方法中创建pc和notepad对象，分别给对象中特有的属性赋值，以及从computer类继承的属性赋值，并使用方法并打印输出信息。
```
package 继承Demo2;
//computer 类
public class computer {
    private String cpu;
    private int memory;
    private int disk;
    public computer(String cpu, int memory, int disk) {
        this.cpu = cpu;
        this.memory = memory;
        this.disk = disk;}
    public String getDetails(){
        return "cpu= " + cpu + " memory= " + memory +" disk= " + disk;}
    public String getCpu() {return cpu;}
    public void setCpu(String cpu) {this.cpu = cpu;}
    public int getMemory() {return memory;}
    public void setMemory(int memory) {this.memory = memory;}
    public int getDisk() {return disk;}
    public void setDisk(int disk) {this.disk = disk;}
}

//pc类
public class pc extends computer{
    private String brand;
    public pc(String cpu, int memory, int disk,String brand) {
        super(cpu, memory, disk);
        this.brand = brand;
    }
    public String getBrand() {return brand;}
    public void setBrand(String brand) {this.brand = brand;}
    public void printinfo(){
        System.out.println("pc信息 = ");
        System.out.println(getDetails() + "brand= " + brand);
    }
}

// notepad 子类
public class notepad extends computer{
    private String color;
    public notepad(String cpu,int memory,int disk,String color){
        super(cpu,memory,disk);
        this.color = color;
    }
    public String getcolor(){ return color;}
    public void printcolor(){
        System.out.println("yans = ");
        System.out.println(getDetails() + "color=" + color);
    }
}
// test
public class Extendtest2 {
    public static void main(String[] args) {
        pc p = new pc("intel",16,500,"ibm");
        color cp = new color("Amd",16,102400,"white")
        cp.printcolor();
        p.printinfo();
    }
}
```
