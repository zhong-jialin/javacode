---
title: "Java作用域"
date: 2023-02-28T23:17:12+08:00
categories: [
    "Java",
]
---

1. 在Java中，主要的变量就是属性，和局部变量
2. 局部变量一般是指在成员方法中定义的变量
3. Java中的作用域分类：
   全局变量：就是属性，作用域为整个类体Cat类：cry eat 等方法使用属性
   局部变量：就是除属性外的其他变量，作用域为定义它的代码块中
4. 全局变量可以不赋值，直接使用，应为有默认值，局部变量必须赋值后，才能使用因此没有默认值