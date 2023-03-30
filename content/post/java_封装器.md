---
title: "Java_封装器"
date: 2023-03-27T23:01:53+08:00
categories: [
    "Java",
]
---
### 封装器
1. 封装就是把抽象出的数据和对数据的操作方法封装在一起，数据被保护在内部，陈旭的其他部分只有通过被授权的操作方法，才能对数据进行操作。
2. 封装的好处 隐藏实现细节，对数据进行验证，保证安全合理。
### 封装的实现的步骤
1. 将属性进行私有化private
2. 提供一个公共的public的set方法，用于对属性判断并赋值（public void setxxx (int n){属性= 参数名}）
3. 提供一个公共的get方法 用于获取属性 (public int getxxx(){ retrun xx;})

### 封装练习
1. Encap.java 不能随便查看人的年龄，工资等隐私，并对设置的年龄进行合理的验证，年龄合理设置，否则给默认，年龄在1-120，工资不能直接查看，name的长度在2-26之间。
```
package 封装器;

public class Encap {
    public static void main(String[] args) {
        Person p = new Person();
        p.setName("jack");
        p.setAge(18);
        p.setSalary(200);
        p.info();}
}
class Person {
    public String name;
    private int age;
    private double salary;
    public String getName() {return name;}
    public void setName(String name) {
        //对数据校验
        if (name.length() >=2 && name.length() <= 6){
            this.name = name;
        }else {
            System.out.println("名字长度不对");
            this.name = "nofont";
        }
        this.name = name;
    }
    public int getAge() {return age;}
    public void setAge(int age) {
        if (age>=1 && age<=120 ){
            this.age = age;
        }else {
            System.out.println("年龄不正确");
            this.age = 18;
        }
    }
    public double getSalary() {
        //增加阅读权限 return salary;}
    public void setSalary(double salary) {
        this.salary = salary;
    }
    public void info(){
        System.out.println("name: " + name + " Salary: " + salary + " age: " + age);
    }
}

```
2. 创建程序，定义两个类 account和accountTest 类
   account类要求有属性：姓名（2-3） 余而（>20） 密码(6wei) 如果不满足提示信息，给默认之
   通过setxxx的方法给account的属性赋值
   通过accounttest测试
```
package 封装器;

public class Account {
    private String name;
    private double balance;
    private String pwd;

    //提供两个构造器


    public Account() {

    }

    public Account(String name, double balance, String pwd) {
        this.setName(name);
        this.setBalance(balance);
        this.setPwd(pwd);
    }

    public void setName(String name) {
        if (name.length() >=2 && name.length() <=4){
            this.name = name;
        }else {
            System.out.println("name error");
            this.name = "no name";
        }
    }
    public String getName(){
        return name;
    }
    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        if (balance >20){
            this.balance = balance;
        }else {
            System.out.println("balence must be 20");
            this.balance = 20;
        }
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        if (pwd.length() >= 6){
            this.pwd = pwd;
        }else {
            System.out.println("pwd error must <6");
            this.pwd = "000000";
        }
    }
    public void info(){
        System.out.println("name: " + name + "balance: "  + balance);
    }

}

package 封装器;

public class TestAccount {
    public static void main(String[] args) {
        Account acc =  new Account();
        acc.setName("tom");
        acc.setBalance(60);
        acc.setPwd("000000");
        acc.info();
    }
}
```