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