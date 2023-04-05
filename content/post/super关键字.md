---
title: "Super关键字"
date: 2023-04-03T22:44:29+08:00
categories: [
    "Java",
]
---
### super关键字
* 基本介绍
  super代表父类的引用，用于访问弗雷德属性，方法，构造器
1. super不可以访问父类的private属性，和private方法，必须从公共方法访问属性，方法。
2. super在子类的引用必须在子类的构造器的第一行使用。
* 基本使用super   
  
```
  //父类
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
    public fu(){
    }
    public fu(String name){
        System.out.println(name);
    }
    public fu(String name,int age){
        System.out.println("fu(String name,int age)");
    }
    public void cal(){
        System.out.println("fu类的cal方法");
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

//子类
package super关键字;

public class son extends fu{
    public void he(){
        System.out.println(super.n1);
    }
    public void of(){
        super.test100();
        super.test200();
        super.test300();
    }
    public son(){
        super("jack",10);
//        super("jack");
    }
    public void sum(){
        System.out.println("son类方法");
        //调用父类cal方法
        //调用顺序是，本类，父类，父类的父类知道 object类
        // 如果存在cal类但是是父类的private类就会返回错误，public类能够正常访问
        cal(); //查找最近
        super.cal(); //直接查找父类
        this.cal(); //只查找本类
        //在查找属性的时候和类的应用规则是一样的
    }
}
```

* super的便利和使用细节
1. 调用父类的构造器的好处，分工明确，父类属性由父类初始化，子类的属性有子类初始化
2. 当子类中有和父类中的成员，属性，方法重名时，为了访问父类的成员，必须用过super，如果没有重名，使用super，this，直接访问是一样的效果。
3. super的访问不限于父类，父类的父类如果有方法也会访问。super访问遵循就近原则，son》fu>fufu
4. super和this的比较。  
   
![二维数组内存示意图](https://img-blog.csdnimg.cn/becb979b7dc24eff82d83bfc5ce0d44a.png "二维数组内存示意图")

