# Spring Boot 微框架



## 1. springboot的引言

> Spring Boot是由`Pivotal团队提供的全新框架`，其设计目的是用来`简化Spring应用的 初始搭建以及开发过程`。该框架使用了`特定的方式来进行配置`，从而使开发人员不 再需要定义样板化的配置。通过这种方式，Spring Boot致力于在蓬勃发展的快速应 用开发领域(rapid application development)成为领导者。
>
> `springboot(微框架) = springmvc(控制器) + spring(项目管理)`

---

## 2. springboot的特点

1. `创建独立的Spring应用程序  `

2. `嵌入的Tomcat，无需部署WAR文件`

3. `简化Maven配置`

4. `自动配置Spring`

5. `没有XML配置`

   ---


## 3. springboot的环境搭建

> 环境要求:
>
> > 1. MAVEN 3.x+
> > 2. Spring FrameWork 4.x+
> > 3. JDK7.x +
> > 	. Spring Boot 1.5.x+	

##### 	3.1 项目中引入依赖

```xml
    <!--继承springboot的父项目-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.7.RELEASE</version>
    </parent>

    <dependencies>
        <!--引入springboot的web支持-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

##### 	3.2 引入配置文件

​		`项目中src/main/resources/application.yml`

##### 	3.3 建包并创建控制器

```java
//在项目中创建指定的包结构
/*
	 com
	    +| baizhi
	    		+| controller */ 
                	@Controller
                    @RequestMapping("/hello")
                    public class HelloController {
                        @RequestMapping("/hello")
                        @ResponseBody
                        public String hello(){
                            System.out.println("======hello world=======");
                            return "hello";
                        }
                    }
               	    		  		
```

##### 	3.4 编写入口类

```java
//在项目中如下的包结构中创建入口类 Application
/*
	com
		+| baizhi                  */
            @SpringBootApplication
            public class Application {
                public static void main(String[] args) {
                    SpringApplication.run(Application.class,args);
                }
            }
```

##### 	3.5 运行main启动项目

```java
o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8989 (http)
com.baizhi.Application : Started Application in 2.152 seconds (JVM running for 2.611)

//说明:  出现以上日志说明启动成功
```

##### 	3.6 访问项目 

```java
//注意: springboot的项目默认没有项目名
//访问路径:  http://localhost:8080/hello/hello
```

---

## 4. 启动tomcat端口占用问题

```yaml
server:
  port: 8989                 #用来指定内嵌服务器端口号
  context-path: /springboot  #用来指定项目的访问路径
```

---

## 5. springboot相关注解说明

```markdown

# Spring boot通常有一个名为 xxxApplication的类,入口类中有一个main方法, 在main方法中使用SpringApplication.run(xxxApplication.class,args)启动springboot应用的项目。

# @RestController: 就是@Controller+@ResponseBody组合，支持RESTful访问方 式，返回结果都是json字符串。

# @SpringBootApplication 注解等价于: 
	@SpringBootConfiguration           标识注解,标识这是一个springboot的配置类
	@EnableAutoConfiguration           自动与项目中集成的第三方技术进行集成
	@ComponentScan			 			扫描入口类所在子包以及子包后代包中注解	
   
```

---

## 6. springboot中配置文件的拆分

```yaml
#说明: 在实际开发过程中生产环境和测试环境有可能是不一样的 因此将生产中的配置和测试中的配置拆分开,是非常必要的在springboot中也提供了配置文件拆分的方式. 这里以生产中项名名称不一致为例:
	
	生产中项目名为: cmfz
	测试中项目名为: springboot
	端口同时为:   8080

拆分如下:
	#主配置文件:
			application.yml	#用来书写相同的的配置
				server:
					port: 8080 #生产和测试为同一个端口
                   
    #生产配置文件:
    	  application-pord.yml
    			server:
    				context-path: /cmfz
    #测试配置文件:
    		application-dev.yml
    			server:
    				context-path: /springboot

```

---

## 7.springboot中创建自定义简单对象

### 7.1 管理单个对象

> 在springboot中可以管理自定义的`简单组件`对象的创建可以直接使用注解形式创建。

```markdown
# 1.使用 @Repository  @Service @Controller 以及@Component管理不同简单对象
	如: 比如要通过工厂创建自定义User对象:
```

```java
@Component
@Data
public class User {
  private String id;
  private String name;
  ......
}	
```

``` markdown
# 2.通过工厂创建之后可以在使用处任意注入该对象
	如:在控制器中使用自定义简单对象创建
```

```java
@Controller
@RequestMapping("hello")
public class HelloController {
    @Autowired
    private User user;
  	......
}
```

### 7.2 管理多个对象

> 在springboot中如果要管理`复杂对象`必须使用`@Configuration + @Bean`注解进行管理

```markdown
# 1.管理复杂对象的创建
```

```java
@Configuration(推荐)|@Component(不推荐)
public class Beans {
    @Bean
    public Calendar getCalendar(){
        return Calendar.getInstance();
    }
}
```

```markdown
# 2.使用复杂对象
```

```java
@Controller
@RequestMapping("hello")
public class HelloController {
    @Autowired
    private Calendar calendar;
    ......
}
```

```markdown
# 注意: 
			  1.@Configuration 配置注解主要用来生产多个组件交给工厂管理  (注册形式)
			  2.@Component     用来管理单个组件                      (包扫描形式)
```

------

## 8.springboot中注入

> ​	springboot中提供了三种注入方式: `注入基本属性`,`对象注入`

##### 8.1 基本属性注入

```markdown
# 1.@Value 属性注入   [重点]
```

```java
@Controller
@RequestMapping("hello")
public class HelloController {
  
    @Value("${name}")
    private String name;
    
    @Value("#{'${lists}'.spilt(",")}")
    private List<String> lists;
    
    @Value("#{${maps}}")
    private Map<String,String> maps;
}
```

```markdown
# 2.在配置文件中注入
```

```yaml
name: xiaohei
lists: xiaohei,xiaoming,xiaowang
maps: "{key:'value',key1:'value1'}"
```

##### 8.2 对象方式注入

```markdown
# 1. @ConfigurationProperties(prefix="前缀")
```

```java
@Component
@Data
@ConfigurationProperties(prefix = "user")
public class User {
    private String id;
    private String name;
    private Integer age;
    private String  bir;
    .....
}
```

```markdown
# 2. 编写配置文件
```

```yaml
user:
  id: 24
  name: xiaohei
  age: 23
  bir: 2012/12/12
```

```markdown
# 3. 引入依赖构建自定义注入元数据
```

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-configuration-processor</artifactId>
  <optional>true</optional>
</dependency>
```

------

## 9. springboot中集成jsp展示

##### 	9.1 引入jsp的集成jar包

```xml
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
</dependency>

<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
</dependency>
```

##### 	9.2 引入jsp运行插件

```xml
<build>
    <finalName>springboot_day1</finalName>
    <!--引入jsp运行插件-->
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

##### 	9.3 配置视图解析器

```yaml
#在配置文件中引入视图解析器
spring:
  mvc:
    view:
      prefix: /   	# /代表访问项目中webapp中页面
      suffix: .jsp 
```

##### 	9.4 启动访问jsp页面

```http
http://localhost:8989/cmfz/index.jsp
```

---

## 10. springboot集成mybatis

##### 	10.1 引入依赖

```markdown
<!--整合mybatis-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.3</version>
</dependency>

<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>druid</artifactId>
	<version>1.1.12</version>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.38</version>
</dependency>

>说明:由于springboot整合mybatis版本中默认依赖mybatis 因此不需要额外引入mybati版本,否则会出现冲突
```

##### 	10.2 配置配置文件

```yaml
spring:
  mvc:
    view:
      prefix: /
      suffix: .jsp
  datasource:
    type: org.apache.commons.dbcp.BasicDataSource   #指定连接池类型
    driver-class-name: com.mysql.jdbc.Driver        #指定驱动
    url: jdbc:mysql://localhost:3306/cmfz           #指定url
    username: root									#指定用户名
    password: root								 	#指定密码
```

##### 	10.3 加入mybatis配置

```yaml
#配置文件中加入如下配置:

mybatis:
  mapper-locations: classpath:com/baizhi/mapper/*.xml  #指定mapper配置文件位置
  type-aliases-package: com.baizhi.entity              #指定起别名来的类
```

```java
//入口类中加入如下配置:
@SpringBootApplication
@MapperScan("com.baizhi.dao")   //必须在入口类中加入这个配置
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class,args);
    }
}
```



##### 	10.4 建表

```sql
CREATE TABLE `t_clazz` (
  `id` varchar(40) NOT NULL,
  `name` varchar(80) DEFAULT NULL,
  `no` varchar(90) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

##### 	10.5 开发实体类

```java
public class Clazz {
    private String id;
    private String name;
    private String no;
    //get set 方法省略....
}
```

##### 	10.6 开发DAO接口以及Mapper

```java
public interface ClazzDAO {
    List<Clazz> findAll();
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.baizhi.dao.ClazzDAO">
    <select id="findAll" resultType="Clazz">
        select * from t_clazz 
    </select>
</mapper>
```

##### 	10.7 开发Service以及实现

```java
//接口
public interface ClazzService {
    List<Clazz> findAll();
}
//实现
@Service
@Transactional
public class ClazzServiceImpl implements  ClazzService {
    @Autowired
    private ClazzDAO clazzDAO;
    
    @Transactional(propagation = Propagation.SUPPORTS)
    @Override
    public List<Clazz> findAll() {
        return clazzDAO.findAll();
    }
}
```

##### 	10.8 引入测试依赖

```xml
 <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
     <scope>test</scope>
</dependency>
```

##### 	10.9 编写测试类

```java
@RunWith(SpringRunner.class)
@SpringBootTest(classes = Application.class)
public class TestClazzService {

    @Autowired
    private ClazzService clazzService;

    @Test
    public void test(){
        List<Clazz> all = clazzService.findAll();
        for (Clazz clazz : all) {
            System.out.println(clazz);
        }

    }
}
```

## 11.开启jsp页面热部署

##### 11.1 引言

> `在springboot中默认对jsp运行为生产模式,不允许修改内容保存后立即生效,因此在开发过程需要调试jsp页面每次需要重新启动服务器这样极大影响了我们的效率,为此springboot中提供了可以将默认的生产模式修改为调试模式,改为调试模式后就可以保存立即生效,如何配置为测试模式需要在配置文件中加入如下配置即可修改为开发模式。`

##### 11.2 配置开启测试模式

```yml
server:
  port: 8989
  jsp-servlet:
    init-parameters:
      development: true  #开启jsp页面的调试模式
```

----

## 12.springboot中devtools热部署

##### 12.1  引言

> ​	`为了进一步提高开发效率,springboot为我们提供了全局项目热部署,日后在开发过程中修改了部分代码以及相关配置文件后,不需要每次重启使修改生效,在项目中开启了springboot全局热部署之后只需要在修改之后等待几秒即可使修改生效。`

##### 12.2 开启热部署

###### 	12.2.1 项目中引入依赖

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <optional>true</optional>
</dependency>
```

###### 	12.2.2 设置idea中支持自动编译

```markdown
# 1.开启自动编译

	Preferences | Build, Execution, Deployment | Compiler -> 勾选上 Build project automatically 这个选项

# 2.开启允许在运行过程中修改文件
	ctrl + alt + shift + / ---->选择1.Registry ---> 勾选 compiler.automake.allow.when.app.running 这个选项
```

###### 12.2.3 启动项目检测热部署是否生效

```markdown
# 1.启动出现如下日志代表生效
```

```verilog
2019-07-17 21:23:17.566  INFO 4496 --- [  restartedMain] com.baizhi.InitApplication               : Starting InitApplication on chenyannandeMacBook-Pro.local with PID 4496 (/Users/chenyannan/IdeaProjects/ideacode/springboot_day1/target/classes started by chenyannan in /Users/chenyannan/IdeaProjects/ideacode/springboot_day1)
2019-07-17 21:23:17.567  INFO 4496 --- [  restartedMain] com.baizhi.InitApplication               : The following profiles are active: dev
2019-07-17 21:23:17.612  INFO 4496 --- [  restartedMain] ationConfigEmbeddedWebApplicationContext : Refreshing org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@66d799c5: startup date [Wed Jul 17 21:23:17 CST 2019]; root of context hierarchy
2019-07-17 21:23:18.782  INFO 4496 --- [  restartedMain] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat initialized with port(s): 8989 (http)
2019-07-17 21:23:18.796  INFO 4496 --- [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-07-17 21:23:18.797  INFO 4496 --- [  restartedMain] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/8.5.20

```

> `注意:日志出现restartedMain代表已经生效,在使用热部署时如果遇到修改之后不能生效,请重试重启项目在试`

##  12. logback日志的集成

##### 	12.1 logback简介

> Logback是由[log4j](https://baike.baidu.com/item/log4j/480673)创始人设计的又一个开源日志组件。目前，logback分为三个模块：logback-core，logback-classic和logback-access。是对log4j日志展示进一步改进

##### 	12.2 日志的级别

	> DEBUG < INFO < WARN < ERROR   
	>
	> 日志级别由低到高:  日志级别越高输出的日志信息越少

##### 	12.3 项目中日志分类

	> 日志分为两类
	>
	>  一种是rootLogger :  用来监听项目中所有的运行日志 包括引入依赖jar中的日志 
	>
	>  一种是logger :         用来监听项目中指定包中的日志信息

##### 	12.4 java项目中使用

###### 12.4.1 logback配置文件

		> logback的配置文件必须放在项目根目录中 且名字必须为logback.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<configuration>
    <!--定义项目中日志输出位置-->
    <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <!--定义项目的日志输出格式-->
        <!--定义项目的日志输出格式-->
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern> [%p] %d{yyyy-MM-dd HH:mm:ss} %m %n</pattern>
        </layout>
    </appender>

    <!--项目中跟日志控制-->
    <root level="INFO">
        <appender-ref ref="stdout"/>
    </root>
    <!--项目中指定包日志控制-->
    <logger name="com.baizhi.dao" level="DEBUG"/>

</configuration>
```

###### 		12.4.2 具体类中使用日志

```java
@Controller
@RequestMapping("/hello")
public class HelloController {
    //声明日志成员
    private static org.apache.log4j.Logger logger = org.apache.log4j.Logger.getLogger(HelloController.class);
    @RequestMapping("/hello")
    @ResponseBody
    public String hello(){
        System.out.println("======hello world=======");
        logger.debug("DEBUG");
        logger.info("INFO");
        logger.warn("WARN");
        logger.error("ERROR");
        return "hello";
    }
}
```

###### 12.4.3 使用默认日志配置

```yml
logging:
  level:
    root: debug
    com.baizhi.dao: debug
  path: /Users/chenyannan/aa.log
  file: bbb.log
```



---

## 12. 切面编程

##### 	12.1 引言

> springboot是对原有项目中spring框架和springmvc的进一步封装,因此在springboot中同样支持spring框架中AOP切面编程,不过在springboot中为了快速开发仅仅提供了注解方式的切面编程.

##### 	12.2 使用

###### 		12.2.1 引入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

###### 		12.2.2 相关注解

```java
/**
    @Aspect 用来类上,代表这个类是一个切面
    @Before 用在方法上代表这个方法是一个前置通知方法 
    @After 用在方法上代表这个方法是一个后置通知方法 @Around 用在方法上代表这个方法是一个环绕的方法
    @Around 用在方法上代表这个方法是一个环绕的方法
**/
```

###### 		12.2.3 前置切面

```java
@Aspect
@Component
public class MyAspect {
    @Before("execution(* com.baizhi.service.*.*(..))")
    public void before(JoinPoint joinPoint){
        System.out.println("前置通知");
        joinPoint.getTarget();//目标对象
        joinPoint.getSignature();//方法签名
        joinPoint.getArgs();//方法参数
    }
}
```

###### 		12.2.4 后置切面

```java
@Aspect
@Component
public class MyAspect {
    @After("execution(* com.baizhi.service.*.*(..))")
    public void before(JoinPoint joinPoint){
        System.out.println("后置通知");
        joinPoint.getTarget();//目标对象
        joinPoint.getSignature();//方法签名
        joinPoint.getArgs();//方法参数
    }
}
```

	> **注意: 前置通知和后置通知都没有返回值,方法参数都为joinpoint**

###### 	12.2.5 环绕切面

```java
@Aspect
@Component
public class MyAspect {
    @Around("execution(* com.baizhi.service.*.*(..))")
    public Object before(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("进入环绕通知");
        proceedingJoinPoint.getTarget();//目标对象
        proceedingJoinPoint.getSignature();//方法签名
        proceedingJoinPoint.getArgs();//方法参数
        Object proceed = proceedingJoinPoint.proceed();//放行执行目标方法
        System.out.println("目标方法执行之后回到环绕通知");
        return proceed;//返回目标方法返回值
    }
}
```

> **`注意: 环绕通知存在返回值,参数为ProceedingJoinPoint,如果执行放行,不会执行目标方法,一旦放行必须将目标方法的返回值返回,否则调用者无法接受返回数据`**

##### 12.3 AOP编程

示例

+ controller

```java
package com.wang.aop;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

/**
 * Created by lmb on 2018/9/5.
 */
@RestController
@RequestMapping("/aopController")
public class AopController {

    @RequestMapping(value = "/sayHello",method = RequestMethod.GET)
    public String sayHello(String name){
        return "hello " + name;
    }
}
```

+ 切面类

```java
package com.wang.aop;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;
import javax.servlet.http.HttpServletRequest;
import java.util.Arrays;
import java.util.Date;

@Aspect
@Component
public class WebLogAcpect {

    private Logger logger = (Logger) LoggerFactory.getLogger(WebLogAcpect.class);

    /**
     * 定义切入点，切入点为com.example.aop下的所有函数
     */
    @Pointcut("execution(public * com.wang.aop..*.*(..))")
    public void webLog(){}

    /**
     * 前置通知：在连接点之前执行的通知
     * @param joinPoint
     * @throws Throwable
     */
    @Before("webLog()")
    public void doBefore(JoinPoint joinPoint) throws Throwable {
        // 接收到请求，记录请求内容
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        HttpServletRequest request = attributes.getRequest();

        // 记录下请求内容
        logger.info("URL : " + request.getRequestURL().toString());
        logger.info("HTTP_METHOD : " + request.getMethod());
        logger.info("IP : " + request.getRemoteAddr());
        logger.info("CLASS_METHOD : " + joinPoint.getSignature().getDeclaringTypeName() + "." + joinPoint.getSignature().getName());
        logger.info("ARGS : " + Arrays.toString(joinPoint.getArgs()));
    }
    @Around("execution(public * com.wang.aop..*.*(..))")
    public Object before(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        logger.info("进入环绕通知"+new Date());
        logger.info("目标对象"+proceedingJoinPoint.getTarget());
        logger.info("方法签名"+proceedingJoinPoint.getSignature());
        logger.info("方法参数"+proceedingJoinPoint.getArgs());
        Object proceed = proceedingJoinPoint.proceed();//放行执行目标方法
        logger.info("目标方法执行之后回到环绕通知"+new Date());
        return proceed;//返回目标方法返回值
    }

    @AfterReturning(returning = "ret",pointcut = "webLog()")
    public void doAfterReturning(Object ret) throws Throwable {
        // 处理完请求，返回内容
        logger.info("RESPONSE : " + ret);
    }

}

```

##### 12.4 AOP通知类型

+ 前置@before

  + 注意：这里用到了JoinPoint和RequestContextHolder。
    1. 通过JoinPoint可以获得通知的签名信息，如目标方法名、目标方法参数信息等；
    2. 通过RequestContextHolder来获取请求信息，Session信息；

  ```java
  /** 
   * 前置通知，方法调用前被调用 
   * @param joinPoint/null
   */  
  @Before(value = POINT_CUT)
  public void before(JoinPoint joinPoint){
      logger.info("前置通知");
      //获取目标方法的参数信息  
      Object[] obj = joinPoint.getArgs();  
      //AOP代理类的信息  
      joinPoint.getThis();  
      //代理的目标对象  
      joinPoint.getTarget();  
      //用的最多 通知的签名  
      Signature signature = joinPoint.getSignature();  
      //代理的是哪一个方法  
      logger.info("代理的是哪一个方法"+signature.getName());  
      //AOP代理类的名字  
      logger.info("AOP代理类的名字"+signature.getDeclaringTypeName());  
      //AOP代理类的类（class）信息  
      signature.getDeclaringType();  
      //获取RequestAttributes  
      RequestAttributes requestAttributes = RequestContextHolder.getRequestAttributes();  
      //从获取RequestAttributes中获取HttpServletRequest的信息  
      HttpServletRequest request = (HttpServletRequest) requestAttributes.resolveReference(RequestAttributes.REFERENCE_REQUEST);  
      //如果要获取Session信息的话，可以这样写：  
      //HttpSession session = (HttpSession) requestAttributes.resolveReference(RequestAttributes.REFERENCE_SESSION);  
      //获取请求参数
      Enumeration<String> enumeration = request.getParameterNames();  
      Map<String,String> parameterMap = Maps.newHashMap();  
      while (enumeration.hasMoreElements()){  
          String parameter = enumeration.nextElement();  
          parameterMap.put(parameter,request.getParameter(parameter));  
      }  
      String str = JSON.toJSONString(parameterMap);  
      if(obj.length > 0) {  
          logger.info("请求的参数信息为："+str);
      }  
  }
  ```

  + 后置通知@AfterReturning

    + 在某连接点之后执行的通知，通常在一个匹配的方法返回的时候执行（可以在后置通知中绑定返回值）

  ```java
  /** 
   * 后置返回通知 
   * 这里需要注意的是: 
   *      如果参数中的第一个参数为JoinPoint，则第二个参数为返回值的信息 
   *      如果参数中的第一个参数不为JoinPoint，则第一个参数为returning中对应的参数 
   *       returning：限定了只有目标方法返回值与通知方法相应参数类型时才能执行后置返回通知，否则不执行，
   *       对于returning对应的通知方法参数为Object类型将匹配任何目标返回值 
   * @param joinPoint 
   * @param keys 
   */  
  @AfterReturning(value = POINT_CUT,returning = "keys")  
  public void doAfterReturningAdvice1(JoinPoint joinPoint,Object keys){  
      logger.info("第一个后置返回通知的返回值："+keys);  
  }  
  
  @AfterReturning(value = POINT_CUT,returning = "keys",argNames = "keys")  
  public void doAfterReturningAdvice2(String keys){  
      logger.info("第二个后置返回通知的返回值："+keys);  
  }
  ```
  
  + 后置异常通知@AfterThrowing：在方法抛出异常退出时执行的通知。
  
  ```java
  /** 
   * 后置异常通知 
   *  定义一个名字，该名字用于匹配通知实现方法的一个参数名，当目标方法抛出异常返回后，将把目标方法抛出的异常传给通知方法； 
   *  throwing:限定了只有目标方法抛出的异常与通知方法相应参数异常类型时才能执行后置异常通知，否则不执行， 
   *           对于throwing对应的通知方法参数为Throwable类型将匹配任何异常。 
   * @param joinPoint 
   * @param exception 
   */  
  @AfterThrowing(value = POINT_CUT,throwing = "exception")  
  public void doAfterThrowingAdvice(JoinPoint joinPoint,Throwable exception){  
      //目标方法名：  
      logger.info(joinPoint.getSignature().getName());  
      if(exception instanceof NullPointerException){  
          logger.info("发生了空指针异常!!!!!");  
      }  
  }  
  ```
  
  + 后置最终通知@After：当某连接点退出时执行的通知（不论是正常返回还是异常退出）。
  
  ```java
  /** 
   * 后置最终通知（目标方法只要执行完了就会执行后置通知方法） 
   * @param joinPoint 
   */  
  @After(value = POINT_CUT)  
  public void doAfterAdvice(JoinPoint joinPoint){ 
      logger.info("后置最终通知执行了!!!!");  
  }  
  ```
  
  + 环绕通知@Around：包围一个连接点的通知，如方法调用等。这是最强大的一种通知类型。环绕通知可以在方法调用前后完成自定义的行为，它也会选择是否继续执行连接点或者直接返回它自己的返回值或抛出异常来结束执行。
  
    环绕通知最强大，也最麻烦，是一个对方法的环绕，具体方法会通过代理传递到切面中去，切面中可选择执行方法与否，执行几次方法等。环绕通知使用一个代理ProceedingJoinPoint类型的对象来管理目标对象，所以此通知的第一个参数必须是ProceedingJoinPoint类型。在通知体内调用ProceedingJoinPoint的proceed()方法会导致后台的连接点方法执行。proceed()方法也可能会被调用并且传入一个Object[]对象，该数组中的值将被作为方法执行时的入参。
  
   ```java
/** 
   * 环绕通知： 
   *   环绕通知非常强大，可以决定目标方法是否执行，什么时候执行，执行时是否需要替换方法参数，执行完毕是否需要替换返回值。 
   *   环绕通知第一个参数必须是org.aspectj.lang.ProceedingJoinPoint类型 
   */  
  @Around(value = POINT_CUT)  
  public Object doAroundAdvice(ProceedingJoinPoint proceedingJoinPoint){  
      logger.info("环绕通知的目标方法名："+proceedingJoinPoint.getSignature().getName());  
      try {  
          Object obj = proceedingJoinPoint.proceed();  
          return obj;  
      } catch (Throwable throwable) {  
          throwable.printStackTrace();  
      }  
      return null;  
  }  
   ```
  
  + 有时候我们定义切面的时候，切面中需要使用到目标对象的某个参数，如何使切面能得到目标对象的参数呢？可以使用args来绑定。如果在一个args表达式中应该使用类型名字的地方使用一个参数名字，那么当通知执行的时候对象的参数值将会被传递进来。
  + 注意：任何通知方法都可以将第一个参数定义为org.aspectj.lang.JoinPoint类型（环绕通知需要定义第一个参数为ProceedingJoinPoint类型，它是 JoinPoint 的一个子类）。JoinPoint接口提供了一系列有用的方法，比如 getArgs()（返回方法参数）、getThis()（返回代理对象）、getTarget()（返回目标）、getSignature()（返回正在被通知的方法相关信息）和 toString()（打印出正在被通知的方法的有用信息）。
  ```java
  @Before("execution(* findById*(..)) &&" + "args(id,..)")
      public void twiceAsOld1(Long id){
          System.err.println ("切面before执行了。。。。id==" + id);
  
      }
  ```

##### 12.5 切入点表达式

+ 定义切入点的时候需要一个包含名字和任意参数的签名，还有一个切入点表达式，如execution(public * com.example.aop..*.*(..))

+ 切入点表达式的格式：execution([可见性]返回类型[声明类型].方法名(参数)[异常])
  其中[]内的是可选的，其它的还支持通配符的使用：

  1.  * ：匹配所有字符

  2.  ..：一般用于匹配多个包，多个参数

  3. +：表示类及其子类

  4. 运算符有：&&,||,!

+ 切入点表达式关键词用例：

  1. ```java
     //execution：用于匹配子表达式。
     //匹配com.cjm.model包及其子包中所有类中的所有方法，返回类型任意，方法参数任意
     @Pointcut(“execution(* com.cjm.model...(..))”)
     public void before(){}
     ```
   ```
  
  2. ```java
     //within：用于匹配连接点所在的Java类或者包。
     //匹配Person类中的所有方法
     @Pointcut(“within(com.cjm.model.Person)”)
     public void before(){}
     //匹配com.cjm包及其子包中所有类中的所有方法
     @Pointcut(“within(com.cjm..*)”)
     public void before(){}
   ```
  
  3. ```java
     //this：用于向通知方法中传入代理对象的引用。
     @Before(“before() && this(proxy)”)
     public void beforeAdvide(JoinPoint point, Object proxy){
     //处理逻辑
     }
     ```
  
  4. ```java
     //target：用于向通知方法中传入目标对象的引用。
     @Before(“before() && target(target)
     public void beforeAdvide(JoinPoint point, Object proxy){
     //处理逻辑
     }
     ```
  
  5. ```java
     //args：用于将参数传入到通知方法中。
     @Before(“before() && args(age,username)”)
     public void beforeAdvide(JoinPoint point, int age, String username){
     //处理逻辑
     }
     ```
  
  6. ```java
     //@within ：用于匹配在类一级使用了参数确定的注解的类，其所有方法都将被匹配。
     @Pointcut(“@within(com.cjm.annotation.AdviceAnnotation)”)
     － 所有被@AdviceAnnotation标注的类都将匹配
     public void before(){}
     ```
  
  7. ```java
     //@target ：和@within的功能类似，但必须要指定注解接口的保留策略为RUNTIME。
     @Pointcut(“@target(com.cjm.annotation.AdviceAnnotation)”)
     public void before(){}
     ```
  
  8. ```java
     //@args ：传入连接点的对象对应的Java类必须被@args指定的Annotation注解标注。
     @Before(“@args(com.cjm.annotation.AdviceAnnotation)”)
     public void beforeAdvide(JoinPoint point){
     //处理逻辑
     }
     
     ```
  
  9. ```java
     //@annotation ：匹配连接点被它参数指定的Annotation注解的方法。也就是说，所有被指定注解标注的方法都将匹配。
     @Pointcut(“@annotation(com.cjm.annotation.AdviceAnnotation)”)
     public void before(){}
     ```
  
  10. ```java
      //bean：通过受管Bean的名字来限定连接点所在的Bean。该关键词是Spring2.5新增的。
      @Pointcut(“bean(person)”)
      public void before(){}
      ```

## 事务管理

> 我们在开发企业应用时，对于业务人员的一个操作实际是对数据读写的多步操作的结合。由于数据操作在顺序执行的过程中，任何一步操作都有可能发生异常，异常会导致后续操作无法完成，此时由于业务逻辑并未正确的完成，之前成功操作数据的并不可靠，需要在这种情况下进行回退。
>
> 事务的作用就是为了保证用户的每一个操作都是可靠的，事务中的每一步操作都必须成功执行，只要有发生异常就回退到事务开始未进行操作的状态。
>
> 事务管理是Spring框架中最为常用的功能之一，我们在使用Spring Boot开发应用时，大部分情况下也都需要使用事务。

### 快速入门

> 在Spring Boot中，当我们使用了spring-boot-starter-jdbc或spring-boot-starter-data-jpa依赖的时候，框 架会自动默认分别注入DataSourceTransactionManager或JpaTransactionManager。所以我们不需要任何额外 配置就可以用@Transactional注解进行事务的使用。
>
> 在该样例工程中（若对该数据访问方式不了解，可先阅读该文章），我们引入了spring-data-jpa，并创建了User实体以及对User的数据访 问对象UserRepository，在ApplicationTest类中实现了使用UserRepository进行数据读写的单元测试用例，如下：

```java

@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(Application.class)
public class ApplicationTests {
 
    @Autowired
    private UserRepository userRepository;
 
    @Test
    public void test() throws Exception {
 
        // 创建10条记录
        userRepository.save(new User("AAA", 10));
        userRepository.save(new User("BBB", 20));
        userRepository.save(new User("CCC", 30));
        userRepository.save(new User("DDD", 40));
        userRepository.save(new User("EEE", 50));
        userRepository.save(new User("FFF", 60));
        userRepository.save(new User("GGG", 70));
        userRepository.save(new User("HHH", 80));
        userRepository.save(new User("III", 90));
        userRepository.save(new User("JJJ", 100));
 
        // 省略后续的一些验证操作
    }
}
```

+ 可以看到，在这个单元测试用例中，使用UserRepository对象连续创建了10个User实体到数据库中，下面我们人为的来制造一些异常，看看会发生什么情况。

+ 通过定义User的name属性长度为5，这样通过创建时User实体的name属性超长就可以触发异常产生。

  ```java
  
  @Entity
  public class User {
   
      @Id
      @GeneratedValue
      private Long id;
   
      @Column(nullable = false, length = 5)
      private String name;
   
      @Column(nullable = false)
      private Integer age;
   
      // 省略构造函数、getter和setter
   
  }
  ```

+ 修改测试用例中创建记录的语句，将一条记录的name长度超过5，如下：name为HHHHHHHHH的User对象将会抛出异常。

```java
// 创建10条记录
userRepository.save(new User("AAA", 10));  
userRepository.save(new User("BBB", 20));  
userRepository.save(new User("CCC", 30));  
userRepository.save(new User("DDD", 40));  
userRepository.save(new User("EEE", 50));  
userRepository.save(new User("FFF", 60));  
userRepository.save(new User("GGG", 70));  
userRepository.save(new User("HHHHHHHHHH", 80));  
userRepository.save(new User("III", 90));  
userRepository.save(new User("JJJ", 100));
```

+ 执行测试用例，可以看到控制台中抛出了如下异常，name字段超长：

```shell
2016-05-27 10:30:35.948  WARN 2660 --- [           main] o.h.engine.jdbc.spi.SqlExceptionHelper   : SQL Error: 1406, SQLState: 22001  
2016-05-27 10:30:35.948 ERROR 2660 --- [           main] o.h.engine.jdbc.spi.SqlExceptionHelper   : Data truncation: Data too long for column 'name' at row 1  
2016-05-27 10:30:35.951  WARN 2660 --- [           main] o.h.engine.jdbc.spi.SqlExceptionHelper   : SQL Warning Code: 1406, SQLState: HY000  
2016-05-27 10:30:35.951  WARN 2660 --- [           main] o.h.engine.jdbc.spi.SqlExceptionHelper   : Data too long for column 'name' at row 1
 
org.springframework.dao.DataIntegrityViolationException: could not execute statement; SQL [n/a]; nested exception is org.hibernate.exception.DataException: could not execute statement 
```

+ 此时查数据库中，创建了name从AAA到GGG的记录，没有HHHHHHHHHH、III、JJJ的记录。而若这是一个希望保证完整性操作的情况 下，AAA到GGG的记录希望能在发生异常的时候被回退，这时候就可以使用事务让它实现回退，做法非常简单，我们只需要在test函数上添加 @Transactional 注解即可。

```java
@Test
@Transactional
public void test() throws Exception {
 
    // 省略测试内容
 
}
```

+ 这里主要通过单元测试演示了如何使用 @Transactional 注解来声明一个函数需要被事务管理，通常我们单元测试为了保证每个测试之间的数据独立，会使用 @Rollback 注解让每个单元测试都能在结束时回滚。而真正在开发业务逻辑时，我们通常在service层接口中使用 @Transactional 来对各个业务逻辑进行事务管理的配置，例如：

```java
public interface UserService {
 
    @Transactional
    User login(String name, String password);
 
}
```

### SpringBoot事务的使用

> spring Boot 使用事务非常简单，首先使用注解 @EnableTransactionManagement 开启事务支持后，然后在访问数据库的Service方法上添加注解 @Transactional 便可。
>
> 关于事务管理器，不管是JPA还是JDBC等都实现自接口 PlatformTransactionManager 如果你添加的是 spring-boot-starter-jdbc 依赖，框架会默认注入 DataSourceTransactionManager 实例。如果你添加的是 spring-boot-starter-data-jpa 依赖，框架会默认注入 JpaTransactionManager 实例。

+ 在启动类中添加如下方法，Debug测试，就能知道自动注入的是 PlatformTransactionManager 接口的哪个实现类。

```java

@EnableTransactionManagement // 启注解事务管理，等同于xml配置方式的 <tx:annotation-driven />
@SpringBootApplication
public class ProfiledemoApplication {
 
    @Bean
    public Object testBean(PlatformTransactionManager platformTransactionManager){
        System.out.println(">>>>>>>>>>" + platformTransactionManager.getClass().getName());
        return new Object();
    }
 
    public static void main(String[] args) {
        SpringApplication.run(ProfiledemoApplication.class, args);
    }
}
```

+ 这些SpringBoot为我们自动做了，这些对我们并不透明，如果你项目做的比较大，添加的持久化依赖比较多，我们还是会选择人为的指定使用哪个事务管理器。 
  代码如下：

```java
@EnableTransactionManagement
@SpringBootApplication
public class ProfiledemoApplication {
 
    // 其中 dataSource 框架会自动为我们注入
    @Bean
    public PlatformTransactionManager txManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
 
    @Bean
    public Object testBean(PlatformTransactionManager platformTransactionManager) {
        System.out.println(">>>>>>>>>>" + platformTransactionManager.getClass().getName());
        return new Object();
    }
 
    public static void main(String[] args) {
        SpringApplication.run(ProfiledemoApplication.class, args);
    }
}
```

+ 在Spring容器中，我们手工注解@Bean 将被优先加载，框架不会重新实例化其他的 PlatformTransactionManager 实现类。然后在Service中，被 @Transactional 注解的方法，将支持事务。如果注解在类上，则整个类的所有方法都默认支持事务。
+ 对于同一个工程中存在多个事务管理器要怎么处理，请看下面的实例，具体说明请看代码中的注释。

```java
@EnableTransactionManagement // 开启注解事务管理，等同于xml配置文件中的 <tx:annotation-driven />
@SpringBootApplication
public class ProfiledemoApplication implements TransactionManagementConfigurer {
 
    @Resource(name="txManager2")
    private PlatformTransactionManager txManager2;
 
    // 创建事务管理器1
    @Bean(name = "txManager1")
    public PlatformTransactionManager txManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
 
    // 创建事务管理器2
    @Bean(name = "txManager2")
    public PlatformTransactionManager txManager2(EntityManagerFactory factory) {
        return new JpaTransactionManager(factory);
    }
 
    // 实现接口 TransactionManagementConfigurer 方法，其返回值代表在拥有多个事务管理器的情况下默认使用的事务管理器
    @Override
    public PlatformTransactionManager annotationDrivenTransactionManager() {
        return txManager2;
    }
 
    public static void main(String[] args) {
        SpringApplication.run(ProfiledemoApplication.class, args);
    }
 
}
```

```java
@Component
public class DevSendMessage implements SendMessage {
 
    // 使用value具体指定使用哪个事务管理器
    @Transactional(value="txManager1")
    @Override
    public void send() {
        System.out.println(">>>>>>>>Dev Send()<<<<<<<<");
        send2();
    }
 
    // 在存在多个事务管理器的情况下，如果使用value具体指定
    // 则默认使用方法 annotationDrivenTransactionManager() 返回的事务管理器
    @Transactional
    public void send2() {
        System.out.println(">>>>>>>>Dev Send2()<<<<<<<<");
    }
 
}
```

+ 如果Spring容器中存在多个 PlatformTransactionManager 实例，并且没有实现接口 TransactionManagementConfigurer 指定默认值，在我们在方法上使用注解 @Transactional 的时候，就必须要用value指定，如果不指定，则会抛出异常。

  对于系统需要提供默认事务管理的情况下，实现接口 TransactionManagementConfigurer 指定。

  对有的系统，为了避免不必要的问题，在业务中必须要明确指定 @Transactional 的 value 值的情况下。不建议实现接口 TransactionManagementConfigurer，这样控制台会明确抛出异常，开发人员就不会忘记主动指定
  

### 事务详情

> 上面的例子中我们使用了默认的事务配置，可以满足一些基本的事务需求，但是当我们项目较大较复杂时（比如，有多个数据源等），这时候需要在声明事务时，指定不同的事务管理器。对于不同数据源的事务管理配置可以见 《Spring Boot多数据源配置与使用》 中的设置。在声明事务时，只需要通过value属性指定配置的事务管理器名即可，例如：@Transactional(value="transactionManagerPrimary") 。
> 

+ 除了指定不同的事务管理器之后，还能对事务进行隔离级别和传播行为的控制，下面分别详细解释：

#### 隔离级别

  隔离级别是指若干个并发的事务之间的隔离程度，与我们开发时候主要相关的场景包括：脏读取、重复读、幻读。

  我们可以看 org.springframework.transaction.annotation.Isolation 枚举类中定义了五个表示隔离级别的值：

  ```java
  public enum Isolation {  
      DEFAULT(-1),
      READ_UNCOMMITTED(1),
      READ_COMMITTED(2),
      REPEATABLE_READ(4),
      SERIALIZABLE(8);
  }
  ```

  + `DEFAULT` ：这是默认值，表示使用底层数据库的默认隔离级别。对大部分数据库而言，通常这值就是： READ_COMMITTED 。
  + `READ_UNCOMMITTED` ：该隔离级别表示一个事务可以读取另一个事务修改但还没有提交的数据。该级别不能防止脏读和不可重复读，因此很少使用该隔离级别。
  + `READ_COMMITTED` ：该隔离级别表示一个事务只能读取另一个事务已经提交的数据。该级别可以防止脏读，这也是大多数情况下的推荐值。
  + `REPEATABLE_READ` ：该隔离级别表示一个事务在整个过程中可以多次重复执行某个查询，并且每次返回的记录都相同。即使在多次查询之间有新增的数据满足该查询，这些新增的记录也会被忽略。该级别可以防止脏读和不可重复读
  + `SERIALIZABLE` ：所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

+ 指定方法：通过使用 `isolation` 属性设置，例如：

  `@Transactional(isolation = Isolation.DEFAULT)`

#### 传播行为

> 所谓事务的传播行为是指，如果在开始当前事务之前，一个事务上下文已经存在，此时有若干选项可以指定一个事务性方法的执行行为。

```markdown
我们可以看 org.springframework.transaction.annotation.Propagation 枚举类中定义了6个表示传播行为的枚举值：
```

```java

public enum Propagation {  
    REQUIRED(0),
    SUPPORTS(1),
    MANDATORY(2),
    REQUIRES_NEW(3),
    NOT_SUPPORTED(4),
    NEVER(5),
    NESTED(6);
}
```

+ `REQUIRED` ：如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务

+ `SUPPORTS` ：如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。

+ `MANDATORY` ：如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。

+ `REQUIRES_NEW` ：创建一个新的事务，如果当前存在事务，则把当前事务挂起。

+ `NOT_SUPPORTED` ：以非事务方式运行，如果当前存在事务，则把当前事务挂起。

+ `NEVER` ：以非事务方式运行，如果当前存在事务，则抛出异常。

+ `NESTED` ：如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于 `REQUIRED` 。

+ 指定方法：通过使用 propagation 属性设置，例如：

  `@Transactional(propagation = Propagation.REQUIRED)`

#### @Transactional 事务实现机制

> 在应用系统调用声明了 @Transactional 的目标方法时，Spring Framework 默认使用 AOP 代理，在代码运行时生成一个代理对象，根据 @Transactional 的属性配置信息，这个代理对象决定该声明 @Transactional 的目标方法是否由拦截器 TransactionInterceptor 来使用拦截，在 TransactionInterceptor 拦截时，会在目标方法开始执行之前创建并加入事务，并执行目标方法的逻辑, 最后根据执行情况是否出现异常，利用抽象事务管理器 AbstractPlatformTransactionManager 操作数据源 DataSource 提交或回滚事务。

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-21_111459.png)

## 13. 文件上传下载

##### 13.1 文件上传

###### 	13.1.1 准备上传页面

```html
<form action="路径...." method="post" enctype="multipart/form-data">
        <input type="file" name="aa">
        <input type="submit" value="上传">
</form>
<!--
	1. 表单提交方式必须是post
	2. 表单的enctype属性必须为multipart/form-data
	3. 后台接受变量名字要与文件选择name属性一致
-->
```

###### 	13.1.2 编写控制器

```java
@Controller
@RequestMapping("/file")
public class FileController {
  @RequestMapping("/upload")
  public String upload(MultipartFile aa, HttpServletRequest request) throws IOException {
        String realPath = request.getRealPath("/upload");
        aa.transferTo(new File(realPath,aa.getOriginalFilename()));//文件上传
        return "index";
  }
}
```

###### 	13.1.3 修改文件上传大小

```yml

#上传时出现如下异常:  上传文件的大小超出默认配置  默认10M
nested exception is java.lang.IllegalStateException: org.apache.tomcat.util.http.fileupload.FileUploadBase$SizeLimitExceededException: the request was rejected because its size (38443713) exceeds the configured maximum (10485760)
#修改上传文件大小:
spring:
  http:
    multipart:
       max-request-size: 209715200  #用来控制文件上传大小的限制
       max-file-size: 209715200 #用来指定服务端最大文件大小   
```



##### 	13.2 文件下载

###### 		13.2.1 提供下载文件链接

```html
<a href="../file/download?fileName=corejava.txt">corejava.txt</a>
```

###### 		13.2.2 开发控制器

```java
@RequestMapping("/download")
public void download(String fileName, HttpServletRequest request, HttpServletResponse response) throws Exception {
        String realPath = request.getRealPath("/upload");
        FileInputStream is = new FileInputStream(new File(realPath, fileName));
        ServletOutputStream os = response.getOutputStream();
        response.setHeader("content-disposition","attachment;fileName="+ URLEncoder.encode(fileName,"UTF-8"));
        IOUtils.copy(is,os);
        IOUtils.closeQuietly(is);
        IOUtils.closeQuietly(os);
    }
```

---

## 14. 拦截器

##### 	14.1 开发拦截器

```java
public class MyInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object o) throws Exception {
        System.out.println("======1=====");
        return true;//返回true 放行  返回false阻止
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("=====2=====");
    }
    
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object o, Exception e) throws Exception {
        System.out.println("=====3=====");
    }
}
```

##### 	14.2 配置拦截器

```java
@Component
public class InterceptorConfig extends WebMvcConfigurerAdapter {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //添加拦截器
        registry.addInterceptor(new MyInterceptor())
            .addPathPatterns("/**")//定义拦截路径
            .excludePathPatterns("/hello/**"); //排除拦截路径
    }
}
```

------

## 15. war包部署

##### 	15.1 设置打包方式为war

> ​	`<packaging>war</packaging>`

##### 	15.2 在插件中指定入口类

```xml
<build>
	<plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <!--使用热部署出现中文乱码解决方案-->
        <configuration>
          <fork>true</fork>
          <!--增加jvm参数-->
          <jvmArguments>-Dfile.encoding=UTF-8</jvmArguments>
          <!--指定入口类-->
          <mainClass>com.baizhi.Application</mainClass>
        </configuration>
      </plugin>
    </plugins>
</build>	
```

##### 	15.3 排除内嵌的tomcat

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <scope>provided</scope>   <!--去掉内嵌tomcat-->
</dependency>

<dependency>
  <groupId>org.apache.tomcat.embed</groupId>
  <artifactId>tomcat-embed-jasper</artifactId>
  <scope>provided</scope>  <!--去掉使用内嵌tomcat解析jsp-->
</dependency>
```

##### 	15.4 配置入口类

```java
//1.继承SpringBootServletInitializer
//2.覆盖configure方法
public class Application extends SpringBootServletInitializer{
    public static void main(String[] args) {
        SpringApplication.run(Application.class,args);
    }
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
        return builder.sources(Application.class);
    }
}
```

##### 	15.5 打包测试

```java
/* 一旦使用war包部署注意:
	1. application.yml 中配置port context-path 失效
	2. 访问时使用打成war包的名字和外部tomcat端口号进行访问项目
*/
```




```

```