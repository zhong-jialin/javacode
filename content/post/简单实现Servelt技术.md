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

### HttpServletRequest接口详解
* 一般情况下，浏览器（客户端）通过 HTTP 协议来访问服务器的资源，Servlet 主要用来处理 HTTP 请求。
* Servlet 处理 HTTP 请求的流程如下：
!["Servlet 处理 HTTP 请求的流程"](http://c.biancheng.net/uploads/allimg/210627/1103524464-0.png "流程图")

1. Servlet 容器接收到来自客户端的 HTTP 请求后，容器会针对该请求分别创建一个 HttpServletRequest 对象和 HttpServletReponse 对象。
2. 容器将 HttpServletRequest 对象和 HttpServletReponse 对象以参数的形式传入 service() 方法内，并调用该方法。
3. 在 service() 方法中 Servlet 通过 HttpServletRequest 对象获取客户端信息以及请求的相关信息。
4. 对 HTTP 请求进行处理。
5. 请求处理完成后，将响应信息封装到 HttpServletReponse 对象中。
6. Servlet 容器将响应信息返回给客户端。
7. 当 Servlet 容器将响应信息返回给客户端后，HttpServletRequest 对象和 HttpServletReponse 对象被销毁。

#### HttpServletRequest 接口
* 在 Servlet API 中，定义了一个 HttpServletRequest 接口，它继承自 ServletRequest 接口。HttpServletRequest 对象专门用于封装 HTTP 请求消息，简称 request 对象。

* HTTP 请求消息分为请求行、请求消息头和请求消息体三部分，所以 HttpServletRequest 接口中定义了获取请求行、请求头和请求消息体的相关方法。

* HttpServletRequest接口定义了一系列请求行信息的方法：

|  返回值类型  | 方法声明 |描述 |
| :-------------: | :----------: | :------------: |
|    String |   	getMethod()   | 该方法用于获取 HTTP 请求方式（如 GET、POST 等）。 |
|    String |   	getRequestURI()   | 该方法用于获取请求行中的资源名称部分，即位于 URL 的主机和端口之后，参数部分之前的部分。 |
|    String |   	getQueryString()   | 该方法用于获取请求行中的参数部分，也就是 URL 中“?”以后的所有内容。 |
|    String |   	getContextPath()   | 返回当前 Servlet 所在的应用的名字（上下文）。对于默认（ROOT）上下文中的 Servlet，此方法返回空字符串""。 |
|    String |   	getServletPath()   | 该方法用于获取 Servlet 所映射的路径。 |
|    String |   	getRemoteAddr()   | 该方法用于获取客户端的 IP 地址。 |
|    String |   	getRemoteHost()   | 该方法用于获取客户端的完整主机名，如果无法解析出客户机的完整主机名，则该方法将会返回客户端的 IP 地址。 |



####   Servlet中通过request功能获取请求参数的功能
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


                PrintWriter writer = resp.getWriter();
        writer.println("请求方式:" + req.getMethod() + "<br/>" +
                "客户端的 IP 地址:" + req.getRemoteAddr() + "<br/>" +
                "应用名字（上下文）:" + req.getContextPath() + "<br/>" +
                "URI:" + req.getRequestURI() + "<br/>" +
                "请求字符串:" + req.getQueryString() + "<br/>" +
                "Servlet所映射的路径:" + req.getServletPath() + "<br/>" +
                "客户端的完整主机名:" + req.getRemoteHost() + "<br/>"
        );

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
#### 获取 form 表单的数据
|  返回值类型  | 方法声明   |描述 |
| :-------------: | :----------: | :------------: |
|    String |   	getParameter(String name)   | 返回指定参数名的参数值。 |
|    String[] |   	getParameterValues (String name)   | 以字符串数组的形式返回指定参数名的所有参数值（HTTP 请求中可以有多个相同参数名的参数）。 |
|    Enumeration  |   	getParameterNames()   | 以枚举集合的形式返回请求中所有参数名。 |
|    Map |   	getParameterMap()   | 	用于将请求中的所有参数名和参数值装入一个 Map 对象中返回。 |

#### 获取 form 表单的数据,并显示在网页上。
* 创建RequestParam.java文件
```
package com.tipdm.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Arrays;

@WebServlet("/RequestParam")
public class RequestParam extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //通过HttpServletResponse类的response响应对象调用getWriter()方法，
        // 返回一个PrintWriter类的对象(比如声明为out)，再使用PrintWriter对象调用该类中自带的方法进行输出
        resp.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        //获取内容 存储到write 再用writer自带的方法输出
        String username = req.getParameter("username");//form 里面input的name
        String password = req.getParameter("password");
        String sex = req.getParameter("sex");
        String city = req.getParameter("city");
        //因为是有多个选项所以用字符串数组
        String[] languages = req.getParameterValues("language");
        writer.write("用户名：" + username + "<br/>" + "密码：" + password + "<br/>" + "性别：" + sex + "<br/>" + "城市：" + city
                + "<br/>" + "使用过的语言：" + Arrays.toString(languages) + "<br/>");
        //                                   因为language是字符串数组的方式所以要用Arrays数组的遍历方法输出
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}

/// 网页提交表格
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
</head>
<body>
<form action="/Servlet/RequestParam" method="get">
    <table border="1" width="50%">
        <tr>
            <td colspan="2" align="center">编程帮wwww.biancheng.net</td>
        </tr>
        <tr>
            <td>输入姓名</td>
            <td><input type="text" name="username" /></td>
        </tr>
        <tr>
            <td>输入密码</td>
            <td><input type="password" name="password" /></td>
        </tr>
        <tr>
            <td>选择性别</td>
            <td><input type="radio" name="sex" value="male" />男 <input
                    type="radio" name="sex" value="female" />女</td>
        </tr>
        <tr>
            <td>选择使用的语言</td>
            <td><input type="checkbox" name="language" value="JAVA" />JAVA
                <input type="checkbox" name="language" value="C" />C语言 <input
                        type="checkbox" name="language" value="PHP" />PHP <input
                        type="checkbox" name="language" value="Python" />Python</td>
        </tr>
        <tr>
            <td>选择城市</td>
            <td><select name="city">
                <option value="none">--请选择--</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="guangzhou">广州</option>
            </select></td>
        </tr>
        <tr>
            <td colspan="2"><input type="submit" value="提交" /></td>
        </tr>
    </table>
</form>
</body>
</html>

```
* 实际网页输出界面
![图片](https://img-blog.csdnimg.cn/2121df37834b4fc98d98a66cff781585.png "图片")


1. 简单获取请求参数的方式，只能通过post请求获取
```
public class SerletDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //只能获取post请求的请求参数
        //缓冲区 获取速度快
        BufferedReader reader = req.getReader(); //获取字符输入流
        String line = null;
        //判断是否为空
        while ((line = reader.readLine())!=null){
            System.out.println(line);
            //打印请求参数
        }
    }
}
```
1. get和post都可以获取请求参数的方式
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
        //使用Map集合中的方法keySet()，把Map集合所有的key取出来，存储到一个set集合中
        Set<String> set  = parameterMap.keySet();
        //遍历set集合，获取Map集合中的每一个key
        for (String name : set) {
            String[] values= req.getParameterValues(name);
            //通过set方法获取请求名称
            System.out.println(name);
            for (String value : values) {
                //通过req.getParameterValues获取请求参数
                System.out.println(value);
            }
            System.out.println("-----------------");
        }

    }
}

```
### HttpServletRequest请求转发
* 什么是请求的转发? 
请求转发是指，服务器收到请求后，从一次资源跳转到另一个资源的操作叫请求转发.
1. 通过request对象获取请求转发器对象：RequestDispatcher getRequestDispatcher(String path)
2. 使用RequestDispatcher对象来进行转发：forward(ServletRequest request, ServletResponse response)
3. 由于 forward() 方法会先清空 response 缓冲区，因此只有转发到最后一个 Web 资源时，生成的响应才会被发送到客户端。
4. 请求转发之后，浏览器地址栏中的 URL 不会发生变化，因此浏览器不知道在服务器内部发生了转发行为，更无法得知转发的次数。
5. 请求转发不支持跨域访问，只能跳转到当前应用中的资源。
6. 参与请求转发的 Web 资源之间共享同一 request 对象和 response 对象。
* 请求转发的工作原理
![请求转发](http://c.biancheng.net/uploads/allimg/210627/11105U1R-0.png "请求转发")
#### 实现一个转发和request域对象。
1. 创建ServletDemo5类实现转发服务到ServletDemo6
```
package com.tipdm.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
@WebServlet("/ServletDemo5")
public class ServletDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {


    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("5555555555555");
        //请求转发
        //转发特点：浏览器地址不会变化 不能跨域访问，只能在当前服务器访问
        req.setAttribute("msg","hellow");
        //转发，服务器内部
        req.getRequestDispatcher("/ServletDemo6").forward(req,resp);
        //重定向 //浏览器发出请求，要加虚拟路径 //动态路径
//        resp.sendRedirect(req.getContextPath() + "/ServletDemo6");

        //转发请求

    }
}
------------------------------------------------------
@WebServlet("/ServletDemo6")
public class ServeltDemo6 extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("6666666666");

        ///接受由ServletDemo5转发的数据
        Object msg = req.getAttribute("msg");
        System.out.println(msg);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}
```
#### 从form表单获取请求值，并且吧DispatcherServlet类的信息转发给DoServlet，并输出在网页上。
1. DispatcherServlet类和DoServlet类，复用之前的form表单
```
package com.tipdm.servlet.lianxi;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/DispatcherServlet")
public class DispatcherServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 设置向页面输出内容格式
        resp.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        // 尝试在请求转发前向response缓冲区写入内容，最后在页面查看是否展示
        writer.write("<h1>转发在响应前的信息</h1>");
        // 向reuqest域对象中添加属性，传递给下一个web资源
        req.setAttribute("webName","转发信息11111");
        //转发                      转发资源的路由名称
        req.getRequestDispatcher("/DoServlet").forward(req,resp);
    }
}

----------------------------------------------
@WebServlet("/DoServlet")
public class DoServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        String webName = (String) req.getAttribute("webName");
        String url = (String) req.getAttribute("url");
        String welcome = (String) req.getAttribute("welcome");
        if (webName != null) {
            writer.write("<h3>" + webName + "</h3>");
        }
        if (url != null) {
            writer.write("<h3>" + url + "</h3>");
        }
        if (welcome != null) {
            writer.write("<h3>" + welcome + "</h3>");
        }
        String username = req.getParameter("username");
        // 获取密码
        String password = req.getParameter("password");
        // 获取性别
        String sex = req.getParameter("sex");
        // 获取城市
        String city = req.getParameter("city");
        // 获取使用语言返回是String数组
        String[] languages = req.getParameterValues("language");
        writer.write("用户名：" + username + "<br/>" + "密码：" + password + "<br/>" + "性别：" + sex + "<br/>" + "城市：" + city
                + "<br/>" + "使用过的语言：" + Arrays.toString(languages) + "<br/>"
        );

    }
}
```
#### Servlet服务中使用jsp
1. 导入jsp依赖包
```
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.1</version>
      <scope>provided</scope>
    </dependency>
```
2. 编写jsp文件并用tomcat服务运行jsp文件。
```
<%@page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>title</title>
</head>
<body>
<h2>Hello jsp!</h2>
<%--//这里可以直接写Java语句--%>
<%
        System.out.println("hellow jsp");
        int i = 3;
        %>
<%=i%>
<%!
    String name;
    void show(){}
%>
</body>
</html>
```
![tupain](https://img-blog.csdnimg.cn/10c248a311ee4a91916a8bc09beda723.png "tomcat配置")

####  在jsp获取来自HTML提交的请求或者调用Java类的方法。
* ELb表达式
1. EL（全称Expression Language ）表达式语言，用于简化 JSP 页面内的 Java 代码。
2. EL 表达式的主要作用是 获取数据。其实就是从域对象中获取数据，然后将数据展示在页面上。
3. 而 EL 表达式的语法也比较简单，${expression} 。例如：${name} 就是获取域中存储的 key 为 name 的数据。
4. Java Web中的四大域对象：
    - 1.page：当前页面有效。
    - 2.request:当前请求有效。
    - 3.session：当前会话有效。
    - 4.application:当前应用有效。
*  EL表达式获取值
1. el表达式只能从域对象中获取值
2. 语法： ${域名称.键名}：从指定域中获取指定键的值
* 域名称：
1. pageScope --> pageContext
2. requestScope --> request
3. sessionScope --> session
4. applicationScope --> application（ServletContext）
* 举例：在request域中存储了name=张三
* 获取：${requestScope.name}
2. ${键名} 表示依次从最小的域中查找是否有该键对应的值，直到找到为止。

* EL表达式获取值
获取对象、List集合、Map集合的值
1. 对象：${域名称.键名.属性名}
   * 本质上会去调用对象的getter方法
2. List集合：${域名称.键名[索引]}
3. Map集合：
   * ${域名称.键名.key名称}
   * ${域名称.键名["key名称"]}

* 代码示例
```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page import="com.tipdom.Bean" %>
<%@ page import="java.util.*" %><%--
  Created by IntelliJ IDEA.
  User: 33993
  Date: 2023/4/24
  Time: 11:17
  To change this template use File | Settings | File Templates.

--%>
<%--//--%>
<%--// isELIgnored="false" 解决无法解析“$.{}”内容  有时候 jsp 默认会无视EL 表达式--%>
<%@ page isELIgnored="false" contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%


//    获取对象，list集合，map集合的值
    List list = new ArrayList();
//    在list对象添加值
    Collections.addAll(list,"zs",1,2.0);
//    吧list集合添加到作用域
    request.setAttribute("list",list);


    Bean zs = new Bean("zs", "1234");
    request.setAttribute("bean",zs);

    //    存储bean对象  吧b对象添加到beanlist集合里面
    List<Bean> beanList = new ArrayList<>();
    beanList.add(zs);
    request.setAttribute("beanList",beanList);


//  在作用域添加信息
    pageContext.setAttribute("msg","hellow");

    request.setAttribute("name","zhangsan");

//    添加map集合并存入数据
    Map<String,Integer> map = new HashMap<>();
    map.put("zs",123);

// 循环
    List<Bean> usertable = new ArrayList<>();
    usertable.add(new Bean("foreach","1234"));
    usertable.add(new Bean("222foreach","1234"));
    request.setAttribute("user",usertable);

%>
<%--隐式对象，动态获取虚拟目录--%>
<%=pageContext.getAttribute("msg")%>
${name}

<%--//通过Bean的getname方法获得--%>
${bean.name}
${bean.password}<br>

${list}<br>
${list[0]}<br>
${list[1]}<br>
${list[2]}<br>

<%--打印存储对象的集合--%>
${beanList[0].name}
${beanList[0].password}

<%--打印map--%>
<%--${map.zs}--%>

<%--用maven跑项目可以用虚拟目录代替目录--%>
${pageContext.request.contextPath}<br>

<c:forEach items="${user}" var="user" varStatus="s">

    ${s.index} ${s.count} ${user.name} ${user.password}<br>

</c:forEach>

</body>
</html>

//页面输出
hellow zhangsan zs 1234
[zs, 1, 2.0]
zs
1
2.0
zs 1234 /Servlet_war
0 1 foreach 1234
1 2 222foreach 1234
```
* 使用java类的对象创建对象，把对象存进数组，放进域里。然后在页面循环结果
```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page import="com.tipdom.Bean" %>
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.Collection" %>
<%@ page import="java.util.Collections" %><%--
  Created by IntelliJ IDEA.
  User: 33993
  Date: 2023/4/24
  Time: 10:00
  To change this template use File | Settings | File Templates.
--%>
<%@ page isELIgnored="false" contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    String username = request.getParameter("username");
    int num = 15;

    Bean bean = new Bean("zs", "123456");
    Bean bean1 = new Bean("zs", "123456");
    Bean bean2 = new Bean("zs", "123456");
    List<Bean> list =new ArrayList<>();
    Collections.addAll(list,bean1,bean2,bean);
    request.setAttribute("list",list);
%>

//根据HTML提交的请求判断，并给出结果
<%--    if (username.equals(bean.getName())){--%>
<%--    %>--%>
<%--    <h1>欢迎你</h1>--%>

<%--<%--%>
<%--    }else {--%>
<%--        %>--%>
<%--    <h1>输入错误</h1>--%>

<%--<%--%>
<%--    }--%>
<%--%>--%>
<table border="1">
    <tr>
        <td>姓名</td>
        <td>密码</td>
    </tr>
    //属于jstl标签
    <c:forEach items="${list}" var="list" varStatus="s">
    <tr>
        <td>${list.name}</td>
        <td>${list.password}</td>
    </tr>
    </c:forEach>
</table>

</body>
</html>
```
### JSTL标签
1. 概念：JavaServer Pages Tag Library JSP标准标签库
2. 是由Apache组织提供的开源的免费的jsp标签
3. 作用：用于简化和替换jsp页面上的java代码
4. 导入JSTL标签
```
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <dependency>
      <groupId>org.apache.taglibs</groupId>
      <artifactId>taglibs-standard-impl</artifactId>
      <version>1.2.3</version>
      <scope>runtime</scope>
    </dependency>
```
* 常见的JSTL标签if
1. if:相当于java代码的if语句
1. 属性：
    * test 必须属性，接受boolean表达式
    * 如果表达式为true，则显示if标签体内容，如果为false，则不显示标签体内容
    * 一般情况下，test属性值会结合el表达式一起使用
2. 注意：
    * c:if标签没有else情况，想要else情况，则可以在定义一个c:if标签

* 常见的JSTL标签choose
choose:相当于java代码的switch语句
1. 使用choose标签声明 相当于switch声明
2. 使用when标签做判断 相当于case
3. 使用otherwise标签做其他情况的声明 相当于default
```
<%
  int number = 1;
  request.setAttribute("number",number);
%>

<c:choose>
  <c:when test="${number == 1}">xinqiyi</c:when>
  <c:when test="${number == 2}">xinqier</c:when>
  <c:when test="${number == 3}">xinqisan</c:when>
  <c:otherwise>input error</c:otherwise>
</c:choose>
```
* 常见的JSTL标签foreach 相当于for语句
1. begin 开始值
2. end结束值
3. var临时变量
4. step 步长
5. var Status 循环状态对象
    - index 容器中元素索引
    - count 循环次数从1开始
6. items 容器对象
7. var容器中元素的临时变量
