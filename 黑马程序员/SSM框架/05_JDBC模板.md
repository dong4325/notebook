---
title: 05_JDBC模板
date: 2021-07-28 10:34:00
tags: 黑马程序员 SSM
---

### 1. Spring JdbcTemplate基本使用

#### 1.1 JdbcTemplate概述

它是spring框架中提供的一个对象，是对原始繁琐的**JdbcAPI**对象的简单封装。spring框架为我们提供了很多的操作模板类。例如：操作关系型数据的**JdbcTemplate**和**HibernateTemplate**，操作**nosql**数据库的**RedisTemplate**，操作消息队列的**JmsTemplat**e等等。

#### 1.2 JdbcTemplate开发步骤

①导入spring-jdbc和spring-tx坐标
②创建数据库表和实体
③创建JdbcTemplate对象
④执行数据库操作

#### 1.3 JdbcTemplate快速入门

①导入坐标

```xml
<!--springcontext依赖 c3p0 commosio mysql-connector-java等也需要自己导入，具体参考案例-->
<!--导入spring的jdbc坐标-->
<dependency
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<!--导入spring的tx坐标-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

②创建accout表和Accout实体

![9965b02155fad198f80dd07fb0c0e921.png](en-resource://database/1979:1)

```java
public class Account {
    private String name;
    private double money;
    //省略get和set方法
}
```

③创建JdbcTemplate对象
④执行数据库操作

```java
//1、创建数据源对象
ComboPooledDataSource dataSource= new ComboPooledDataSource();
dataSource.setDriverClass("com.mysql.jdbc.Driver");
dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/test");
dataSource.setUser("root");
dataSource.setPassword("root");
//2、创建JdbcTemplate对象J
JdbcTemplate jdbcTemplate= new JdbcTemplate();
//3、设置数据源给JdbcTemplate
jdbcTemplate.setDataSource(dataSource);
//4、执行操作
jdbcTemplate.update("insert into account values(?,?)","tom",5000);
```

#### 1.4 Spring产生JdbcTemplate对象

我们可以将JdbcTemplate的创建权交给Spring，将数据源DataSource的创建权也交给Spring，在Spring容器内部将数据源DataSource注入到JdbcTemplate模版对象中，配置如下：

```xml
<!--数据源DataSource-->
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
    <property name="jdbcUrl" value="jdbc:mysql:///test"></property>
    <property name="user" value="root"></property>
    <property name="password" value="root"></property>
</bean>
<!--JdbcTemplate-->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

从容器中获得JdbcTemplate进行添加操作

```java
@Test
public void testSpringJdbcTemplate() throws PropertyVetoException{
    ApplicationContext applicationContext= new ClassPathXmlApplicationContext("applicationContext.xml");
    JdbcTemplate jdbcTemplate= applicationContext.getBean(JdbcTemplate.class);
    jdbcTemplate.update("insert into account values(?,?)","lucy",5000);
}
```

数据库配置一般与spirng的xml文件分开，使用jdbc.properties文件存储
```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=root
```

修改xml文件（熟记）
```xml
<!--添加命名空间-->
xmlns:context="http://www.springframework.org/schema/context"
xsi:schemaLocation="http://www.springframework.org/schema/context   http://www.springframework.org/schema/context/spring-context.xsd

    <!--加载jdbc.properties-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--数据源对象-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="user" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>    
    <!--JdbcTemplate-->
    <bean id="jdbcTemplate"     class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
```



### 1.5 JdbcTemplate的常用操作

修改操作

```java
//需要导入相关依赖
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class JdbcTemplateCRUDTest{
    @Autowired
    private JdbcTemplate jdbcTemplate;
    @Test
    //测试修改操作
    public void testUpdate(){
        jdbcTemplate.update("update account set money=? where name=?",1000,"tom");
    }
}
```

删除和查询全部操作

```java
@Test
public void testDelete(){
    jdbcTemplate.update("delete from account where name=?","tom");
}
@Test
public void testQueryAll(){
    List<Account> accounts = jdbcTemplate.query("select *from account", new BeanPropertyRowMapper<Account>(Account.class));
    for (Account account: accounts) {
        System.out.println(account.getName());
    }
}
```

查询单个数据操作操作

```java
@Test
//测试查询单个对象操作
public void testQueryOne(){
    Account account= jdbcTemplate.queryForObject("select *from account where name=?", new BeanPropertyRowMapper<Account>(Account.class), 
"tom");
    System.out.println(account.getName());
}

@Test
//测试查询单个简单数据操作(聚合查询)
public void testQueryCount(){
    Long aLong= jdbcTemplate.queryForObject("select count(*) from account", Long.class);
    System.out.println(aLong);
}
```

#### 1.6 知识要点

①导入spring-jdbc和spring-tx坐标
②创建数据库表和实体
③创建JdbcTemplate对象

```java
JdbcTemplatejdbcTemplate= new JdbcTemplate();
jdbcTemplate.setDataSource(dataSource);
```

④执行数据库操作

- 更新操作：
`jdbcTemplate.update(sql,params)`

- 查询操作：

```java
jdbcTemplate.query(sql,Mapper,params)
jdbcTemplate.queryForObject(sql,Mapper,params)
```



