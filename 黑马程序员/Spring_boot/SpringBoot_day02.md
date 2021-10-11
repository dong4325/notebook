---
title: SpringBoot_day02
date: 2021-08-01 21:55:34
tags: 黑马程序员 springboot
---

## SpringBoot 原理分析

### SpringBoot自动配置

#### Condition

是在 Spring 4.0 增加的条件判断功能，通过这个可以功能可以实现选择性的创建 Bean 操作。

SpringBoot是如何知道要创建哪个 Bean 的？比如 SpringBoot 是如何知道要创建 RedisTemplate 的？

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
```

```java
@SpringBootApplication
public class Test1Application {
    public static void main(String[] args) {
        //启动SpringBoot的应用，返回Spring的IOC容器
        ConfigurableApplicationContext context = SpringApplication.run(Test1Application.class, args);
        //获取Bean，redisTemplate
        Object redisTemplate = context.getBean("redisTemplate");
        System.out.println(redisTemplate);
    }
}
```

Spring会根据Condition判断有没有redis对应的字节码文件，有就创建Bean。



**案例**：需求
在Spring 的 IOC 容器中有一个 User 的 Bean ，现要求

1. 导入 Jedis 坐标后，加载该 Bean ，没导入，则不加载。
2. 将类的判断定义为动态的。判断哪个字节码文件存在可以动态指定。

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>
```

```java
//注意实现的是spirngframework.context.annotation包下的条件接口
public class ClassCondition implements Condition {
    @Override
    public boolean matches(ConditionContext conditionContext, AnnotatedTypeMetadata annotatedTypeMetadata) {
        //导入 Jedis 坐标后，加载该 Bean，否则不会创建该bean，并会抛出异常
        //判断：redis.clients.jedis.Jedis文件是否存在
        try {
            Class<?> aClass = Class.forName("redis.clients.jedis.Jedis");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            return false;
        }
        return true;
    }
}
```

```java
@Configuration
public class UserConfig {
    @Bean
    @Conditional(ClassCondition.class)
    public User user(){
        return new User();
    }
}
```

```java
@SpringBootApplication
public class Test1Application {

    public static void main(String[] args) {
        //启动SpringBoot的应用，返回Spring的IOC容器
        ConfigurableApplicationContext context = SpringApplication.run(Test1Application.class, args);
        Object user = context.getBean("user");
        System.out.println(user);
    }
}
```

2. 将类的判断设置为动态的

```java
//注意实现的是spirngframework.context.annotation包下的条件接口
public class ClassCondition implements Condition {
    /**
     *
     * @param conditionContext 上下文对象。用于获取环境，IOC容器，ClassLoader对象
     * @param annotatedTypeMetadata 注解元对象。可以用于获取注解定义的属性值。
     * @return
     */
    @Override
    public boolean matches(ConditionContext conditionContext, AnnotatedTypeMetadata annotatedTypeMetadata) {
        //导入 Jedis 坐标后，加载该 Bean
        //判断：redis.clients.jedis.Jedis文件是否存在
        Map<String, Object> map = annotatedTypeMetadata.getAnnotationAttributes(ConditionOnClass.class.getName());
        String[] value = (String[])map.get("value");
        try {
            for(String className : value){
                Class<?> aClass = Class.forName(className);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            return false;
        }
        return true;
    }
}
```

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional(ClassCondition.class)
public @interface ConditionOnClass {
    String[] value();
}
```

```java
@Configuration
public class UserConfig {
    @Bean
//    @Conditional(ClassCondition.class)
    @ConditionOnClass("redis.clients.jedis.Jedis")
    public User user(){
        return new User();
    }

    @Bean
    @ConditionalOnProperty(name = "itcast",havingValue = "itheima")
    public User user2(){
        return new User();
    }
}
```

```properties
#application.properties
itcast=itheima
```

```java
@SpringBootApplication
public class Test1Application {

    public static void main(String[] args) {
        //启动SpringBoot的应用，返回Spring的IOC容器
        ConfigurableApplicationContext context = SpringApplication.run(Test1Application.class, args);
        Object user1 = context.getBean("user");
        Object user2 = context.getBean("user2");
        System.out.println(user1);
        System.out.println(user2);
    }
}
```

#### Condition小结

- 自定义条件：

  1. 定义条件类：自定义类实现 Condition 接口，重写 matches 方法，在 matches 方法中进行逻辑判断，返回boolean 值 。  matches 方法两个参数：
     1. context ：上下文对象，可以获取属性值，获取类加载器，获取 BeanFactory 等。
     2. metadata ：元数据对象，用于获取注解属性。

  2. 判断条件： 在初始化 Bean 时，使用 @Conditional 条件类 class 注解
  
- SpringBoot 提供的常用条件注解：
  • ConditionalOnProperty 判断配置文件中是否有对应属性和值才初始化 Bean
  • ConditionalOnClass 判断环境中是否有对应字节码文件才初始化 Bean
  • ConditionalOnMissingBean 判断环境中没有对应 Bean 才初始化 Bean

#### 切换内置web 服务器

SpringBoot的 web 环境中默认使用 tomcat 作为内置服务器，其实 SpringBoot 提供了 4 中内置服务器供我们选择，我们可以很方便的进行切换。Jetty，Netty，Tomcat，Undertow。

引入web环境依赖，会自动加入tomcat服务器。

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
```

更改为使用Jetty服务器。

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <!--排除tomcat依赖-->
            <exclusions>
                <exclusion>
                    <artifactId>spring-boot-starter-tomcat</artifactId>
                    <groupId>org.springframework.boot</groupId>
                </exclusion>
            </exclusions>
        </dependency>

        <!--引入jetty的依赖-->
        <dependency>
            <artifactId>spring-boot-starter-jetty</artifactId>
            <groupId>org.springframework.boot</groupId>
        </dependency>
```

#### @Enable注解

SpringBoot中提供了很多 Enable 开头的注解，这些注解都是用于动态启用某些功能的。而其底层原理是使用 @Import 注解导入一些配置类，实现 Bean 的动态加载。

SpringBoot工程是否可以直接获取 jar 包（第三方）中定义的 Bean?

不可以

other模块中：

```java
package com.itheima.domain;

public class User {
}
```

```java
package com.itheima.config;

import com.itheima.domain.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class UserConfig {

    @Bean
    public User user() {
        return new User();
    }
}
```



Enable模块中内容：

获取另外一模块内容，

```xml
        <dependency>
            <groupId>com.itheima</groupId>
            <artifactId>springboot-enable-other</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
```

```java
package com.itheima.springbootenable;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.Bean;
import redis.clients.jedis.Jedis;

import java.util.Map;

/**
 * @ComponentScan 扫描范围：当前引导类所在包及其子包
 *
 * com.itheima.springbootenable
 * com.itheima.config
 * //1.使用@ComponentScan扫描com.itheima.config包
 * //2.可以使用@Import注解，加载类。这些类都会被Spring创建，并放入IOC容器
 * //3.可以对Import注解进行封装。
 */

@SpringBootApplication
//@ComponentScan("com.itheima.config")
//@Import(UserConfig.class)
@EnableUser
public class SpringbootEnableApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(SpringbootEnableApplication.class, args);

        //获取Bean
        Object user = context.getBean("user");
        System.out.println(user);
    }
}
```

```java
//使用注解需要在other模块下建立此注解。
package com.itheima.config;

import org.springframework.context.annotation.Import;

import java.lang.annotation.*;

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Import(UserConfig.class)
public @interface EnableUser {
}
```

#### @Import注解
@Enable 底层依赖于 @Import 注解导入一些类，使用 @Import 导入的类会被 Spring 加载到 IOC 容器中。而 @Import 提供 4 种用法:

1. 导入 Bean
2. 导入配置类
3. 导入 ImportSelector 实现类。一般用于加载配置文件中的类
4. 导入 ImportBeanDefinitionRegistrar 实现类。

```java
package com.itheima.springbootenable;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.Bean;
import redis.clients.jedis.Jedis;
import java.util.Map;

/**
 * Import4中用法：
 *  1. 导入Bean
 *  2. 导入配置类
 *  3. 导入ImportSelector的实现类。
 *  4. 导入ImportBeanDefinitionRegistrar实现类
 */

//@Import(User.class)
//@Import(UserConfig.class)
//@Import(MyImportSelector.class)
//@Import({MyImportBeanDefinitionRegistrar.class})
@SpringBootApplication
public class SpringbootEnableApplication {
    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(SpringbootEnableApplication.class, args);
        User user = context.getBean(User.class);
        System.out.println(user);
        Role role = context.getBean(Role.class);
        System.out.println(role);
       /* Map<String, User> map = context.getBeansOfType(User.class);
        System.out.println(map);*/
        
      /*  Object user = context.getBean("user");
        System.out.println(user);
        //第四种方法，起的名称叫做user
        */
    }
}
```

```java
package com.itheima.config;

import com.itheima.domain.Role;
import com.itheima.domain.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

//@Configuration
//使用import导入类，可以省略该注解
public class UserConfig {
    @Bean
    public User user() {
        return new User();
    }
    @Bean
    public Role role() {
        return new Role();
    }//role和user一样，就是个domain包下的类
}
```

第三种方式：other模块中

```java
package com.itheima.config;

import org.springframework.context.annotation.ImportSelector;
import org.springframework.core.type.AnnotationMetadata;

public class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata importingClassMetadata) {
        return new String[]{"com.itheima.domain.User", "com.itheima.domain.Role"};
        //字符串可以从配置文件中获取。
    }
}
```

第四种方式：other模块中

```java
package com.itheima.config;

import com.itheima.domain.User;
import org.springframework.beans.factory.support.AbstractBeanDefinition;
import org.springframework.beans.factory.support.BeanDefinitionBuilder;
import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.context.annotation.ImportBeanDefinitionRegistrar;
import org.springframework.core.type.AnnotationMetadata;

public class MyImportBeanDefinitionRegistrar implements ImportBeanDefinitionRegistrar {
    @Override
    public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
        AbstractBeanDefinition beanDefinition = BeanDefinitionBuilder.rootBeanDefinition(User.class).getBeanDefinition();
        registry.registerBeanDefinition("user", beanDefinition);
    }
}
```

#### @EnableAutoConfiguration注解

- @EnableAutoConfiguration（位于@SpringApplicaton中） 注解内部使用 @Import(AutoConfigurationImportSelector.class) 来加载配置类。
- 配置文件位置： `META INF/spring.factories` ，该配置文件中定义了大量的配置类，当 SpringBoot 应用启动时，会自动加载这些配置类，初始化 Bean
- 并不是所有的 Bean 都会被初始化，在配置类中使用 Condition 来加载满足条件的 Bean

> 依赖可以在mvnrepository.com网站搜索如使用mybatis 可以搜索 mybatis spring-boot。

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.2</version>
</dependency>
<!--第三方提供的依赖会把名字放前面-->
```

案例：需求

自定义redis starter 。要求当导入 redis 坐标时， SpringBoot 自动创建 Jedis 的 Bean

案例：实现步骤

1. 创建 redis spring boot autoconfigure 模块
2. 创建 redis spring boot starter 模块 依赖 redis springboot autoconfigure 的模块
3. 在 redis spring boot autoconfigure 模块中初始化 Jedis 的Bean 。并定义 META INF/ spring.factories 文件
4. 在测试模块中引入自定义的 redis starter 依赖，测试获取Jedis 的 Bean ，操作 redis 。

**创建redis-spring-boot-autoconfigure模块（包名为configure）**

引入jedis依赖

```xml
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>
```

新建核心配置类

```java
package com.itheima.redis.config;

import org.springframework.boot.autoconfigure.condition.ConditionalOnClass;
import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import redis.clients.jedis.Jedis;

@Configuration
@EnableConfigurationProperties(RedisProperties.class)//使RedisProperties类被spring识别
@ConditionalOnClass(Jedis.class)//Jedis在的时候才会加载Bean
public class RedisAutoConfiguration {

    /**
     * 提供Jedis的bean
     */
    @Bean
    @ConditionalOnMissingBean(name = "jedis")//如果没有叫做jedis的Bean才会加载
    public Jedis jedis(RedisProperties redisProperties) {
        System.out.println("RedisAutoConfiguration....");
        return new Jedis(redisProperties.getHost(), redisProperties.getPort());
    }
}
```

新建实体类 将实体类于配置文件相绑定

```java
package com.itheima.redis.config;

import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties(prefix = "redis")
public class RedisProperties {
    private String host = "localhost";
    private int port = 6379;
	//getter setter方法
}
```

在resources目录下新建`META-INF/spring.factories`文件

```properties
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  com.itheima.redis.config.RedisAutoConfiguration
```



**创建redis-spring-boot-starter模块（包名为redis）**

引入依赖

```xml
        <!--引入configure-->
        <dependency>
            <groupId>com.itheima</groupId>
            <artifactId>redis-spring-boot-autoconfigure</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
```



**使用enable模块**

引入自定义的模块依赖

```xml
        <!--自定义的redis的starter-->
        <dependency>
            <groupId>com.itheima</groupId>
            <artifactId>redis-spring-boot-starter</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
```

```java
package com.itheima.springbootenable;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.Bean;
import redis.clients.jedis.Jedis;
import java.util.Map;

@SpringBootApplication
public class SpringbootEnableApplication {
    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(SpringbootEnableApplication.class, args);

        Jedis jedis = context.getBean(Jedis.class);
        System.out.println(jedis);

        jedis.set("name","itcast");
        String name = jedis.get("name");
        System.out.println(name);
    }//会打印RedisAutoConfiguration....

    @Bean
    public Jedis jedis(){
        return  new  Jedis("localhost",6379);
    }//不会打印RedisAutoConfiguration.... ，证明ConditionalOnMissingBean生效
}
```

新建application.properties

```properties
redis.port=6666
#链接会失败，证明生效
```

### SpringBoot监听机制

#### Java的监听机制

SpringBoot监听机制，其实是对 Java 提供的事件监听机制的封装。
Java中的事件监听机制定义了以下几个角色：

1. 事件： Event ，继承 java.util.EventObject 类的对象
2. 事件源： Source ，任意对象 Object
3. 监听器： Listener ，实现 java.util.EventListener 接口 的对象

#### SpringBoot监听机制

SpringBoot在项目启动时，会对几个监听器进行回调，我们可以实现这些监听器接口，在项目启动时完成一些操作。
ApplicationContextInitializer、 SpringApplicationRunListener 、 CommandLineRunner 、ApplicationRunner

前两个类想要生效需要先配置`META-INF/spring.factories`文件

```factories
org.springframework.context.ApplicationContextInitializer=com.itheima.springbootlistener.listener.MyApplicationContextInitializer

org.springframework.boot.SpringApplicationRunListener=com.itheima.springbootlistener.listener.MySpringApplicationRunListener
```

新建MyApplicationContextInitializer类

```java
package com.itheima.springbootlistener.listener;

import org.springframework.context.ApplicationContextInitializer;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.stereotype.Component;

@Component
public class MyApplicationContextInitializer implements ApplicationContextInitializer {
    @Override
    public void initialize(ConfigurableApplicationContext applicationContext) {
        System.out.println("ApplicationContextInitializer....initialize");
        //可以用于项目还没有准备IOC容器之前检测一些资源是否存在。
    }
}
```

新建MySpringApplicationRunListener类

```java
package com.itheima.springbootlistener.listener;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.SpringApplicationRunListener;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.core.env.ConfigurableEnvironment;
import org.springframework.stereotype.Component;

public class MySpringApplicationRunListener implements SpringApplicationRunListener {
    
    //SpringApplication 为项目启动时 事件源，可以产生很多生命周期事件 该构造不能省略
    public MySpringApplicationRunListener(SpringApplication application, String[] args) {
    }

    @Override
    public void starting() {
        System.out.println("starting...项目启动中");
    }

    @Override
    public void environmentPrepared(ConfigurableEnvironment environment) {
        System.out.println("environmentPrepared...环境对象开始准备");
    }

    @Override
    public void contextPrepared(ConfigurableApplicationContext context) {
        System.out.println("contextPrepared...上下文对象开始准备");
    }

    @Override
    public void contextLoaded(ConfigurableApplicationContext context) {
        System.out.println("contextLoaded...上下文对象开始加载");
    }

    @Override
    public void started(ConfigurableApplicationContext context) {
        System.out.println("started...上下文对象加载完成");
    }

    @Override
    public void running(ConfigurableApplicationContext context) {
        System.out.println("running...项目启动完成，开始运行");
    }

    @Override
    public void failed(ConfigurableApplicationContext context, Throwable exception) {
        System.out.println("failed...项目启动失败");
    }
}
```

新建MyCommandLineRunner类

```java
package com.itheima.springbootlistener.listener;

import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

import java.util.Arrays;

@Component
public class MyCommandLineRunner implements CommandLineRunner {
    //与下面那种用法基本相同
    @Override
    public void run(String... args) throws Exception {
        System.out.println("CommandLineRunner...run");
        System.out.println(Arrays.asList(args));
    }
}
```

新建MyApplicationRunner类

```java
package com.itheima.springbootlistener.listener;

import org.springframework.boot.ApplicationArguments;
import org.springframework.boot.ApplicationRunner;
import org.springframework.stereotype.Component;

import java.util.Arrays;

/**
 * 当项目启动后执行run方法。可以执行缓存预热，如让redis在项目启动时把数据库信息提前加载到缓存，
 * 防止第一个人查询时缓存里没有数据
 */
@Component
public class MyApplicationRunner implements ApplicationRunner {
    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println("ApplicationRunner...run");
        System.out.println(Arrays.asList(args.getSourceArgs()));
    }
}
```

### SpringBoot 启动流程分析

#### 启动流程

![SpringBoot启动流程](SpringBoot_day02.assets/SpringBoot启动流程.png)

## Spring Boot 监控

#### SpringBoot监控概述
SpringBoot自带监控功能 Actuator ，可以帮助实现对程序内部运行情况监控，比如监控状况、 Bean 加载情况、配置属性、日志信息等。

#### SpringBoot监控使用
使用步骤

1. 导入依赖坐标

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-actuator</artifactId>
   </dependency>
   <!--在Ops中可以直接勾选-->
   ```

2. 访问 http://localhost:8080/acruator

| **路径**        | **描述**                                                     |
| --------------- | ------------------------------------------------------------ |
| /beans          | 描述应用程序上下文里全部的Bean，以及它们的关系               |
| /env            | 获取全部环境属性                                             |
| /env/{name}     | 根据名称获取特定的环境属性值                                 |
| /health         | 报告应用程序的健康指标，这些值由HealthIndicator的实现类提供  |
| /info           | 获取应用程序的定制信息，这些信息由info打头的属性提供（配置文件中） |
| /mappings       | 描述全部的URI路径，以及它们和控制器(包含Actuator端点)的映射关系 |
| /metrics        | 报告各种应用程序度量信息，比如内存用量和HTTP请求计数         |
| /metrics/{name} | 报告指定名称的应用程序度量值                                 |
| /trace          | 提供基本的HTTP请求跟踪信息(时间戳、HTTP头等)                 |

application.properties

```properties
info.name=zhangsan
info.age=22

#开启健康检查的完整信息，为了安全默认为关闭，有up和 down两种状态
management.endpoint.health.show-details=always

#将web的所有的监控endpoint暴露出来
management.endpoints.web.exposure.include=*
```

#### SpringBoot监控 Spring Boot Admin

- Spring Boot Admin 是一个开源社区项目，用于管理和监控 SpringBoot 应用程序。
- Spring Boot Admin 有两个角色，客户端 ( 和服务端 ）。
- 应用程序作为 Spring Boot Admin Client 向为 Spring Boot Admin Server 注册
- Spring Boot Admin Server 的 UI 界面将 Spring Boot Admin Client 的 Actuator Endpoint 上的一些监控信息。

使用步骤

admin-server（可以监控多个client模块）

1. 创建 admin server 模块

2. 导入依赖坐标`spring-boot-admin-starter-server` 和web模块

3. 在引导类上启用监控功能 EnableAdminServer

   ```java
   @EnableAdminServer
   @SpringBootApplication
   public class SpringbootAdminServerApplication {
   
       public static void main(String[] args) {
           SpringApplication.run(SpringbootAdminServerApplication.class, args);
       }
   }
   ```

   两个项目在一个地址，端口都是8080会重复，为方便，更改下端口

   新建application.properties文件

   ```properties
   server.port=9000
   ```

admin-client

1. 创建 admin client 模块

2. 导入依赖坐标`spring-boot-admin-starter-client` 和web模块

3. 配置相关信息： server 地址等

   application.properties文件

   ```properties
   # 执行admin.server地址
   spring.boot.admin.client.url=http://localhost:9000
   management.endpoint.health.show-details=always
   management.endpoints.web.exposure.include=*
   ```

4. 启动 server 和 client 服务，访问 server（localhost:9000）

## SpringBoot 项目部署

#### SpringBoot项目部署
SpringBoot项目开发完毕后，支持两种方式部署到服务器：

1. jar 包 官方推荐

   创建deploy模块，导入web依赖，新建一个Controller类

   ```java
   @RequestMapping("/user")
   @RestController
   public class UserController {
       @RequestMapping("/findAll")
       public String findAll(){
           return "succcess";
       }
   }
   ```

   使用在Maven Project中点击package打为jar包（默认极为打为jar包）

   将jar包放在服务器 执行`java -jar .\*.jar`即可

2. war 包

   更改项目中的pom文件`<packaging>war</packaging>` 

   更改引导类继承SpringBootServletInitializer类，重写configure方法。

   ```java
   @SpringBootApplication
   public class SpringbootDeployApplication extends SpringBootServletInitializer {
       public static void main(String[] args) {
           SpringApplication.run(SpringbootDeployApplication.class, args);
       }
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
           return builder.sources(SpringbootDeployApplication.class);
       }
   }
   ```

   将war包放在tomcat的webapps目录下，启动Tomcat即可。

   访问地址为`localhost:8080/springboot/user/findAll`,spirngboot为war包名称，也是在tomcat中的虚拟目录。

   内置更改的端口号也不会生效，这时更改端口号需要在Tomcat的外置配置文件中更改。



