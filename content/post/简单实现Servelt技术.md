---
title: "简单实现Servelt技术"
date: 2023-04-21T20:39:02+08:00
categories: [
    "Java",
]
---
## 图面无法在转markdown打开，用链接替代。
### 项目目录
![这是图片](https://img-blog.csdnimg.cn/db30087542d54bb79e3356068e5e67d0.png "Magic Gardens")
## 什么是Servelt技术
1. servlet是JavaEE规范之一，规范就是接口。
2. Servelt就是javaWeb三大组件之一，分别是Servelt程序,Filter过滤器，Listener监听器。
3. Servlet是运行在服务器上的一个java程序，它可以接受客户端发送过来的请求，并相应数据给客户端。

### 创建Servlet程序
1. 打开IDea新建项目：
![这是图片](https://img-blog.csdnimg.cn/678ea88e077045018df3f5ff7e94056f.png "Magic Gardens")
https://img-blog.csdnimg.cn/678ea88e077045018df3f5ff7e94056f.png 
2. 打开目录pom.xml文件，打开https://mvnrepository.com/artifact/org.apache.tomcat.maven/tomcat7-maven-plugin/2.2 maven网站。
![这是图片](https://img-blog.csdnimg.cn/e3dba81ecdc14d10ad78c50d39b7ded8.png "Magic Gardens")
https://img-blog.csdnimg.cn/e3dba81ecdc14d10ad78c50d39b7ded8.png
3. 在pom.xml导入maven包。然后按下右上角蓝色m字母导入包。导入javax.servlet-api包.
快捷键 alt+ins->插件模板。
![这是图片](https://img-blog.csdnimg.cn/55d352964c9a4de3b0d489a1787ba4d2.png "Magic Gardens")
https://img-blog.csdnimg.cn/55d352964c9a4de3b0d489a1787ba4d2.png
完整代码:
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.example</groupId>
  <artifactId>Servlet</artifactId>
  <version>1.0-SNAPSHOT</version>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
      </plugin>
    </plugins>
  </build>

  <properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <!--
      1.jar java项目
      2.war web项目
  -->
  <packaging>war</packaging>
  <dependencies>
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>

  </dependencies>

</project>

```
4. 在main文件夹创建java文件。
5.  在webapp创建index.HTML文件。
6. 创建编辑配置运行tomcat文件。
![这是图片](https://img-blog.csdnimg.cn/e6fd839bd9404c0dbfca5b8fc9f35742.png "Magic Gardens")
https://img-blog.csdnimg.cn/e6fd839bd9404c0dbfca5b8fc9f35742.png
7. 显示下面内容说明导入包并且成功运行tomcat成功。访问http://localhost:8080/Servlet/index.html 可以访问地址就是配置成功了。
```
[INFO] 
[INFO] --- tomcat7-maven-plugin:2.2:run (default-cli) @ Servlet ---
[INFO] Running war on http://localhost:8080/Servlet
[INFO] Using existing Tomcat server configuration at C:\Users\33993\Desktop\server\remake\target\tomcat
[INFO] create webapp with contextPath: /Servlet
四月 21, 2023 9:10:14 下午 org.apache.coyote.AbstractProtocol init
信息: Initializing ProtocolHandler ["http-bio-8080"]
四月 21, 2023 9:10:14 下午 org.apache.catalina.core.StandardService startInternal
信息: Starting service Tomcat
四月 21, 2023 9:10:14 下午 org.apache.catalina.core.StandardEngine startInternal
信息: Starting Servlet Engine: Apache Tomcat/7.0.47
四月 21, 2023 9:10:15 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["http-bio-8080"]
```
8. 打开web.xml文件，设置打开本地端口地址默认显示index.html。
```
<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <welcome-file-list>
    <welcome-file></welcome-file>
  </welcome-file-list>
</web-app>
```
9. 编写一个类去实现Servlet接口。实现service方法，处理请求，并相应数据。
```


import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;
////访问路径 相当于vue的路由 //在网页中用
@WebServlet("/TestServlet")
public class TestServlet implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        //初始化方法只调用一次 默认访问servlet资源调用一次
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hellow servlet");
        //访问此接口会触发service方法 idea控制台会输出语句
        //service方法不能和doget,dopost方法一起使用，会覆盖其他两个方法。
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {
        System.out.println("destray销毁调用");
    }
}
```
### Servlet的生命周期
    - 加载和实例化 (默认情况下，当servlet第一次被访问的时候,由容器创建Servlet对象)
    - 执行 init 初始化方法 (实例化之后,容器将调用Servlet的init()方法初始化这个对象
完成一些加载配置文件,创建连接等初始化的工作,该方法只调用一次)
第一、二步，是在第一次访问，的时候创建 Servlet 程序会调用。
    - 执行 service 方法
第三步，每次访问都会调用。
    - 执行 destroy 销毁方方法
第四步，在 web 工程停止的时候调用
```
@WebServlet(urlPatterns = "/demo",loadOnStartup = 1) 
尾数为 -1 时：第一次被访问时创建Servlet对象
0或正整数：服务器启动时创建Servlet对象，数字越小优先级越高。
```
### Servlet类的继承体系
* interface Servlet    : 只负责servlet程序访问规范，servlet体系的根接口
* class genericServlet : 实现servlet接口，是抽象类
* Class HTTP Servlet ： 抽取实现server()方法，并实现了请求分发处理。
Httpservlet 是对http协议封装的Servlet实现类
* 自定义servlet程序 : 重写doGet()方法和doPost()方法
#### 通过继承HttpsServlet实现Servlet程序
1. 编写一个类去继承 HttpServlet 类，根据业务需要重写 doGet 或 doPost 方法
```
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
@WebServlet("/demo3")
public class TestServlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("usessss get");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("usesss post");
    }
}

```
2. 建立一个HTML文件去访问类，判断使用的是post还是get方法。一样使用http://localhost:8080/Servlet/request.html访问
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<form action="/Servlet/demo3" method="post">
  <input name="username" type="text">
  <input type="submit">
</form>
</body>
</html>
```
#### 通过引用servlet接口实现HttpServlet的判断是post还是get获取值的类。
1. 编写test Server类
```
package com.tipdm.servlet;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

public class TestServlet3 implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        //强制转换类型 为什么要转忘了
        String method = request.getMethod();
        if ("GET".equals(method)){
            //执行doget（） 代码
            doget();
        } else if ("POST".equals(method)) {
            dopost();
        }
    }

    protected void dopost() {
        System.out.println("dopost方法");
    }

    protected void doget() {
        System.out.println("doget方法");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}

```
3. 用myheepsServerlet实现。
```


import javax.servlet.annotation.WebServlet;

@WebServlet("/demo2")
public class MyHttpsServlet extends TestServlet3{
    @Override
    protected void doget() {
        System.out.println("myhttpsssssssssss doget");
    }

    @Override
    protected void dopost() {
        System.out.println("myhttpssssssssssss dopost");
    }
}
```
4. 吧request.html的提交路径改为MyHttpServlet的路由。idea控制台返回myhttpsssssssssss doget就是成功了。


### Servlet中通过request功能获取请求参数的功能
1. 获取请求消息数据
```
package com.tipdm.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
@WebServlet("/servletdemo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求时方式
        String method = req.getMethod();
        System.out.println(method);
        //获取虚拟目录
        String contextPath = req.getContextPath();
        System.out.println(contextPath);
        //获取servlet路径
        String servletPath = req.getServletPath();
        System.out.println(servletPath);
        // 获取get请求参数
        String queryget = req.getQueryString();
        System.out.println(queryget + "use dopost");
        //获取客户端ip地址
        String remoteaddre = req.getRemoteAddr();
        System.out.println(remoteaddre);

    }
}


```
2. 获取浏览器请求头数据
```
package com.tipdm.servlet;

import jdk.nashorn.internal.runtime.regexp.joni.ast.StringNode;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Enumeration;
@WebServlet("/ServletDemo1")
public class ServletDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       this.doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求头数据
        String header = req.getHeader("User-Agent");
        System.out.println(header);
        System.out.println("===========================");
        //获取所有请求头数据
        Enumeration<String> headerNames = req.getHeaderNames();
        while (headerNames.hasMoreElements()){
                String name = headerNames.nextElement();
                String value = req.getHeader(name);
            System.out.println(name + "==============>" + value);
        }
    }
}

```
3. get和post都可以获取请求参数的方式
```
package com.tipdm.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;
import java.util.Enumeration;
import java.util.Map;

@WebServlet("/ServletDemo3")
public class ServletDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
        System.out.println("get");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //get和post都可以获取请求参数的方式
        //第一种
        String username = req.getParameter("username");
        System.out.println(username);
        String password = req.getParameter("password");
        System.out.println(password);
        System.out.println("post");


        System.out.println("=================================");

        //第二种
        //根据参数名称获取参数数值的数组 返回String类型数组
        String[] hobbies = req.getParameterValues("hobby");
        System.out.println(Arrays.toString(hobbies));


        System.out.println("===================================");

        //第三种
        //获取所有请求的参数名称
        Enumeration<String> parameterNames = req.getParameterNames();
        while(parameterNames.hasMoreElements()){
            //获取参数名称
           String name =  parameterNames.nextElement();
           //获取请求参数
           String value = req.getParameter(name);
            //弊端：只能获取一个参数
            System.out.println(name + "==========>" + value);
        }

        System.out.println("===========================");
        //第四种
        //获取所有参数的map参数集合
        ////参数     值
        Map<String, String[]> parameterMap = req.getParameterMap();
        //便利map集合
        parameterMap.forEach((k,v)->{
            //                                     Arrays.toString(v)     参看数组v的内容
            System.out.println(k + "=============>" + Arrays.toString(v));
        });

        ///map 另一种map方式
        Set<String> set  = parameterMap.keySet();
        for (String name : set) {
            String[] values= req.getParameterValues(name);
            System.out.println(name);
            for (String value : values) {
                System.out.println(value);
            }
            System.out.println("-----------------");
        }

    }
}

```




