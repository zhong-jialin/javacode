---
title: "Mybatis的使用"
date: 2023-05-24T21:06:54+08:00
categories: [
    "Mybatis",
]
---
#### 准备工作
1. 创建springboot工程，数据库表user，实体类User
!["创建文件"](https://img-blog.csdnimg.cn/7f8b8043784d4ffd936052ba78f537be.png "创建文件")
!["创建文件"](https://img-blog.csdnimg.cn/de38cf400b7847cd8a352f237f6a1a6e.png "创建文件")
    - 创建实体类
   !["创建文件"](https://img-blog.csdnimg.cn/08d209f83aaf4c5c9b22196a26828db3.png "创建文件")
    - 声明实体类的数据类型，要和数据库的表相同名字。
    ```
        package com.zhong.pojo;

        public class User {
            private Integer id;
            private String username;
            private Short age;
            private Short gender;
            private String phone;

            public User() {
            }

            public User(Integer id, String username, Short age, Short gender, String phone) {
                this.id = id;
                this.username = username;
                this.age = age;
                this.gender = gender;
                this.phone = phone;
            }

            @Override
            public String toString() {
                return "User{" +
                        "id=" + id +
                        ", username='" + username + '\'' +
                        ", age=" + age +
                        ", gender=" + gender +
                        ", phone='" + phone + '\'' +
                        '}';
            }

            public Integer getId() {
                return id;
            }

            public void setId(Integer id) {
                this.id = id;
            }

            public String getUsername() {
                return username;
            }

            public void setUsername(String username) {
                this.username = username;
            }

            public Short getAge() {
                return age;
            }

            public void setAge(Short age) {
                this.age = age;
            }

            public Short getGender() {
                return gender;
            }

            public void setGender(Short gender) {
                this.gender = gender;
            }

            public String getPhone() {
                return phone;
            }

            public void setPhone(String phone) {
                this.phone = phone;
            }
        }
    ```
2. 引入Mybatis的相关依赖，配置Mybatis(数据库连接信息)
    * 在resource的application...的文件中写入连接数据库的信息
    ```
    spring.datasource.driver-class-name=com.mysql.jdbc.Driver
    spring.datasource.url=jdbc:mysql://localhost:3306/mybatis
    spring.datasource.username=root
    spring.datasource.password=root
    #配置mybatis日志
    mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
    ```
    * 编写sql语句的接口
    ```
    @Mapper //运行时，会自动生成该接口的实现类对象（代理对象），并将开对象交给IOC容器管理

    public interface UserMapper {
        //查询全部用户信息
        @Select("select * from user")
        public List<User> list();
    }
    ```
    - 用测试类测试接口
    ```
    @SpringBootTest
        class DemoMybatisApplicationTests {

            //声明接口 自动代理生成接口
            @Autowired
            private UserMapper userMapper;
            @Test

            public void testListUser(){
                List<User> userList = userMapper.list();
                //用集合的方法遍历
                userList.forEach(System.out::println);
            }

        }

    //控制台输出以下结果说明测试成功
    User{id=47, username='admin', age=12, gender=1, phone='123'}
    User{id=48, username='123', age=12, gender=2, phone='123'}
    User{id=51, username='root', age=12, gender=1, phone='123'}
    User{id=54, username='zhong', age=12, gender=2, phone='123'}
    ```
#### lompok工具包
* lombpk是一个实用的java类库，能通过注解的形式自动生成构造器，并可以自动化生成日志变量，简化Java开发。
1. 在pom文件引入lambok
```
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
```
2. 修改数据库的实体类pojo.User
```
package com.zhong.pojo;

import lombok.*;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class User {
    private Integer id;
    private String username;
    private Short age;
    private Short gender;
    private String phone;

}
```
#### 在sprint boot项目中使用mybatis，lombok进行增删改查
* 删除操作
1. 用之前创建的项目目录。在pojo软件包创建emp文件，使用Lombok工具包
```
package com.zhong.pojo;
import lombok.*;

        import java.time.LocalDate;
        import java.time.LocalDateTime;
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Emp {
    private Integer id;
    private String username;
    private String password;
    private String name;
    private Short gender;
    protected String image;
    private Short job;
    private LocalDate entrydate;
    private Integer deptId;
    private LocalDateTime createTime;
    private LocalDateTime updateTime;
}

```
2. 创建EmpMapper接口
```
package com.zhong.mapper;

import org.apache.ibatis.annotations.Delete;
import org.apache.ibatis.annotations.Mapper;

@Mapper
public interface EmpMapper {

    //根据id删除数据
    //注解
    @Delete("delete from emp where id = #{id}")
    public void delete(Integer id);
}
```
3. 在测试类中测试
```
@SpringBootTest
class DemoMybatisApplicationTests {

    //声明接口 自动代理生成接口
    @Autowired
    private EmpMapper empMapper;
    @Test

    public void testDelete(){
        empMapper.delete(17);
    }

}
```
* 增加操作
1. 新增接口方法

```
    //插入之后，返回主键id的值
    @Options(useGeneratedKeys = true,keyProperty = "id")
    @Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time)"
            + " values(#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")
    public void insert(Emp emp);

    Emp是pojo的引入实体类Emp
```
2. 测试类
```
    public void testInsert(){
        Emp emp = new Emp();
        emp.setUsername("tom");
        emp.setName("tom");
        emp.setImage("tom.jpg");
        emp.setGender((short)1);
        emp.setJob((short)1);
        emp.setEntrydate(LocalDate.of(2000,1,1));
        emp.setCreateTime(LocalDateTime.now());
        emp.setUpdateTime(LocalDateTime.now());
        emp.setDeptId(1);

        //执行动作
        empMapper.insert(emp);
                System.out.println(emp.getId());
    }
```
* 更新操作
```
EmpMapper
    @Update("update emp set username=#{username},name=#{name},gender=#{gender},image=#{image},job=#{job}" +
            ",entrydate=#{entrydate},dept_id=#{deptId},update_time=#{updateTime} where id= #{id}")
    public void updadate(Emp emp);

//test
        public void updadate(){
        Emp emp = new Emp();
        emp.setId(18);
        emp.setUsername("jerr");
        emp.setName("jerr");
        emp.setImage("jerr.jpg");
        emp.setGender((short)2);
        emp.setJob((short)2);
        emp.setEntrydate(LocalDate.of(2000,1,1));
        emp.setUpdateTime(LocalDateTime.now());
        emp.setDeptId(1);

        //执行动作
        empMapper.updadate(emp);
        System.out.println(emp.getId());
    }
```
* 查询操作
```
EmpMapper

    //查询员工
    //不显示日期
    //方法一
    @Select("select id, username, password, name, gender, image, job, entrydate, dept_id deptId, create_time createTime, update_time updateTime " +
            "from emp where id = #{id}")
    public Emp getById(Integer id);

    第二种
    @Results( {
            @Result(column = "dept_id", property = "deptId"),
            @Result(column = "create_time", property = "createTime"),
            @Result(column = "update_time", property = "updateTime")
    })

    @Select("select * from emp where id = #{id}")
    public Emp getById(Integer id);

    //第三总驼峰自动映射
    //在数据库配置文件配置mybatis.configuration.map-underscore-to-camel-case=true
    @Select("select * from emp where id = #{id}")
    public Emp getById(Integer id);

test
    public void testselect(){
        Emp emp = empMapper.getById(18);
        System.out.println(emp);
    }
```
* 条件查询
```
    //条件查询员工
    //方法1  '%${name}%' 性能低 不安全 存在sql注入问题
    //''内想要读取字符要改成${}
    //使用mysql的拼接语法
    @Select("select * from emp where name like concat('%',#{name},'%') and gender = #{gender}" +
            " and entrydate between #{begin} and #{end} order by update_time desc")
    public List<Emp> list(String name, Short gender, LocalDate begin,LocalDate end);

test
    //查询条件
    public void testList(){
        List<Emp> empList = empMapper.list("张", (short) 1, LocalDate.of(2010, 1, 1), LocalDate.of(2020, 1, 1));
        System.out.println(empList);
    }

```
* XML映射文件   
所有的SQL语句都必须在XML文件中配置。而从MyBatis 3开始，开始支持接口映射器，其底层利用的是接口绑定技术。另外，接口映射器允许通过注解定义SQL语句，用以替代XML文件配置SQL。
1. XML映射文件的名称与Mapper接口名称一致，并且XML文件和Mapper接口放置在相同包下
2. XML映射文件的namespace属性为Mapper接口全限定名一致
3. XML映射文件中sql语句的id与mapper接口中的方法名一致，并且返回类型一致
* 吧sql语句放进xml文件执行
```
EmpMapper接口配置
    //使用xml实现
    public List<Emp> list(String name, Short gender, LocalDate begin,LocalDate end);

xml文件配置
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zhong.mapper.EmpMapper">
<!--    id对应EmpMapper的接口名称-->
<!--    resultType单条记录返回类型-->
    <select id="list" resultType="com.zhong.pojo.Emp">
        select * from emp where name like concat('%',#{name},'%') and gender = #{gender} and
        entrydate between #{begin} and #{end} order by update_time desc
    </select>
</mapper>

```
* XML动态SQL
```
<mapper namespace="com.zhong.mapper.EmpMapper">
<!--    id对应EmpMapper的接口名称-->
<!--    resultType单条记录返回类型-->
    <select id="list" resultType="com.zhong.pojo.Emp">
        select * from emp
        <where>
        <if test="name != null">
            name like concat('%',#{name},'%')
        </if>
        <if test="gender != null">
            and gender = #{gender}
        </if>
        <if test="begin != null">
            and entrydate between #{begin} and #{end}
        </if>
        </where>
        order by update_time desc
    </select>
</mapper>
```