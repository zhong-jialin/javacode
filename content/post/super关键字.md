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
}
```

