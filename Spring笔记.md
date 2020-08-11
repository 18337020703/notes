# Spring 框架知识总结

## Spring介绍

### 什么是spring

> Spring是一个开源框架，Spring是于2003 年兴起的一个轻量级的Java 开发框架，由Rod Johnson 在其著作Expert One-On-One J2EE Development and Design中阐述的部分理念和原型衍生而来。它是为了解决企业应用开发的复杂性而创建的。框架的主要优势之一就是其分层架构，分层架构允许使用者选择使用哪一个组件，同时为 J2EE 应用程序开发提供集成的框架。Spring使用基本的JavaBean来完成以前只可能由EJB完成的事情。然而，Spring的用途不仅限于服务器端的开发。从简单性、可测试性和松耦合的角度而言，任何Java应用都可以从Spring中受益。Spring的核心是控制反转（IoC）和面向切面（AOP）。简单来说，Spring是一个分层的JavaSE/EE full-stack(一站式) 轻量级开源框架。

### spring核心

> spring的核心理念，IOC 和 AOP

### Spring体系结构图

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-16_131428.png)

### spring优点

+ **方便解耦，简化开发 （高内聚低耦合）**

  Spring就是一个大工厂（容器），可以将所有对象创建和依赖关系维护，交给Spring管理
  spring工厂是用于生成bean

+ **AOP编程的支持**

  Spring提供切面编程，可以方便的实现对程序进行权限拦截，运用监控等

+ **方便程序的测试**

  spring对Junit支持，可以通过注解测试Spring程序

+ **声明式事务的支持**

  只需要通过配置就可以完成对事务的管理，而无需手动编程

+ **方便集成各种优秀的框架**

  内部提供了很多优秀的框架（如：Struts、Hibernate、MyBatis、Quartz等）的直接支持

+ 降低API的使用难度

  Spring 对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低

### 高内聚低耦合

> 高内聚就是把操作数据库的dao层，操作业务逻辑的service层，都分在一层，这是高内聚
>
> 低耦合就是，能不调用其他层，尽量不调用。做到不调用可以以用。

## IOC-控制反转

+ **控制反转就是把bean的控制，反转给spring来控制。**

+ 目标类

  提供UserService接口和实现类，获得UserService实现类的实例。之前开发中，直接new一个对象即可。学习spring之后，将由Spring创建对象实例–> IoC 控制反转，之后需要实例对象时，从spring工厂（容器）中获得，需要将实现类的全限定名称配置到xml文件中。

  ```javascript
  //写一个接口和一个实现类，交给spring管理
  public interface UserService {
      public void addUser();
  }
  public class UserServiceImpl implements UserService {
      @Override
      public void addUser() {
          System.out.println("a_ico add user");
      }
  }
  ```

+ 配置文件

  位置：任意，开发中一般在classpath下（src）

  任意，开发中常用applicationContext.xml

  添加schema约束

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans 
                             http://www.springframework.org/schema/beans/spring-beans.xsd">
      <!-- 配置service 
          <bean> 配置需要创建的对象
              id ：用于之后从spring容器获得实例时使用的
              class ：需要创建实例的全限定类名
      -->
      <bean id="userServiceId" class="com.itheima.a_ioc.UserServiceImpl"></bean>
  </beans>
  ```

+ 测试

  ```java
   @Test
      public void demo02(){
          //从spring容器获得
          //1 获得容器
          String xmlPath = "com/itheima/a_ioc/beans.xml";
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext(xmlPath);
          //2获得内容 --不需要自己new，都是从spring容器获得
          UserService userService = (UserService) applicationContext.getBean("userServiceId");
          userService.addUser();  
  ```

  
## DI-依赖注入

+ 例如

  ```java
  class BookServiceImpl{
      //之前开发：接口 = 实现类  （service和dao耦合）
      //private BookDao bookDao = new BookDaoImpl();
      //spring之后 （解耦：service实现类使用dao接口，不知道具体的实现类）
      private BookDao bookDao;
      setter方法
  }
  模拟spring执行过程
  创建service实例：BookService bookService = new BookServiceImpl()     -->IoC  <bean>
  创建dao实例：BookDao bookDao = new BookDaoImple()                -->IoC
  将dao设置给service：bookService.setBookDao(bookDao);             -->DI   <property>
  ```

+ #####  目标类

  - 创建BookService接口和实现类

  - 创建BookDao接口和实现类

  - 将dao和service配置 xml文件

  - 使用api测试

+ ##### dao

  ```java
  public interface BookDao {
      public void save();
  }
  public class BookDaoImpl implements BookDao {
  
      @Override
      public void save() {
          System.out.println("di  add book");
      }
  }
  ```

+ service

  ```java
  public interface BookService {
  
      public abstract void addBook();
  
  }
  public class BookServiceImpl implements BookService {
  
      // 方式1：之前，接口=实现类
  //  private BookDao bookDao = new BookDaoImpl();
      
      // 方式2：接口 + setter
      private BookDao bookDao;
      public void setBookDao(BookDao bookDao) {
          this.bookDao = bookDao;
      }
  
      @Override
      public void addBook(){
          this.bookDao.save();
      }
  }
  
  ```

+ 配置文件

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans 
                             http://www.springframework.org/schema/beans/spring-beans.xsd">
      <!-- 
      模拟spring执行过程
          创建service实例：BookService bookService = new BookServiceImpl() IoC  <bean>
          创建dao实例：BookDao bookDao = new BookDaoImpl()         IoC
          将dao设置给service：bookService.setBookDao(bookDao);     DI   <property>
  
          <property> 用于进行属性注入
              name： bean的属性名，通过setter方法获得
                  setBookDao ##> BookDao  ##> bookDao
              ref ：另一个bean的id值的引用
       -->
  
      <!-- 创建service -->
      <bean id="bookServiceId" class="com.itheima.b_di.BookServiceImpl">
          <property name="bookDao" ref="bookDaoId"></property>
      </bean>
  
      <!-- 创建dao实例 -->
      <bean id="bookDaoId" class="com.itheima.b_di.BookDaoImpl"></bean>
  
  
  </beans>
  ```

  

+ 测试

  ```java
   @Test
      public void demo01(){
          //从spring容器获得
          String xmlPath = "com/itheima/b_di/beans.xml";
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext(xmlPath);
          BookService bookService = (BookService) applicationContext.getBean("bookServiceId");    
          bookService.addBook();
      }
  ```

## 核心API

+ BeanFactory   

  > 这是一个工厂，用来生成任意bean
  >
  > 采用延迟加载，第一次getBean时才会初始化bean

  

+ ApplicationContext

  > 是BeanFactory 的子接口，功能更强大，比如国际化处理，事件传递，自动装配等
  >
  > 配置文件 一加载，对象就实例化
  >
  > ClassPathXmlApplicationContext,加载类路径下的xml
  >
  > FileSystemXmlApplicationContext,加载指定盘符下的xml    // .getRealPath()

## 装配Bean基于XML

### 实例化方式

#### 默认构造

`<bean id="" class=""></bean>` 默认使用默认构造

#### 静态工厂

+ 常用于Spring整合其他框架/工具

+ 静态工厂：用于生成实例对象，所有方法必须是static

  + 把bean放到静态工厂

  ```java
  package com.wang.beans;
   
  public class Bean1 {
      public void add(){
          System.out.println("bean1 ........");
      }
  }
  
  
    package com.wang.beans;
   
  public class Bean1_factory {
      public static Bean1 getBean(){
          return new Bean1();
      }
  }
  ```

  + 把工厂装配到Spring

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans 
                             http://www.springframework.org/schema/beans/spring-beans.xsd">
      
      <!-- 使用静态工厂创建对象 -->
      <bean id="bean1" class="cn.jz.beans.Bean1_factory" 
          factory-method="getBean">
      </bean>
   </bean>
  ```

#### 实例工厂

+ 实例工厂方法都是非静态的

  + 把bean放到实例工厂

  ```java
  package com.wang.beans;
   
  public class Bean2 {
      public void add(){
          System.out.println("bean2 ........");
      }
  }
  
  
    package com.wang.beans;
   
   public class Bean2_factory {
      public Bean2 getBean(){
          return new Bean2();
      }
  }
  ```
  
  + 把工厂装配到Spring
  
  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans 
                             http://www.springframework.org/schema/beans/spring-beans.xsd">
      
      <!-- 使用实例工厂创建对象 -->
      <bean id="bean2_fcty" class="cn.jz.beans.Bean2_factory"> </bean>
      <bean id="bean2" factory-bean="bean2_fcty" factory-method="getBean"> </bean>
  </bean>
   
  ```
  
  

### Bean的种类

#### 普通bean

+ 之前的操作都是普通bean。`<bean id="" class="A"></bean>`

#### 工厂bean

+ FactoryBean接口提供getObject()方法获得bean的实例，此bean实例不是由spring容器提供，而是工厂自己提供

  + 是一个特殊的bean，具有工厂生成对象能力，只能生成特定的对象

  + bean必须使用Factory接口，此接口提供getObject()方法，用于获得特定bean

  + 先创建FactoryBean实例，使用getObject()方法，返回方法的返回值

    `<bean id="" class="FactoryBean"></bean>`

    `FactoryBean factoryBean = new FactoryBean();`

    `return factoryBean.getObject();`
  + FactoryBean 和 BeanFactory的区别
    + FactoryBean：特殊Bean，用于生成另一个特定的bean(代理Bean)，例如ProxyFactoryBean
    + BeanFactory：工厂，用于生成任意Bean
  + Spring的框架内部，AOP相关功能及事务处理中，很多地方使用到了工厂bean
  + BeanFactory作用是实例化，定位，配置应用程序中的对象及建立这些对象的依赖。

### Bean的作用域

+ 作用域：用于确定spring创建bean实例的个数

  | 类别          | 说明                                                         |
  | ------------- | ------------------------------------------------------------ |
  | singleton     | 在Spring Ioc容器中仅存在一个Bean实例，Bean以单例的方式存在，默认单例 |
  | prototype     | 每次从容器中调用Bean的时候，都返回一个新的实例，即每次都调用getBean的时候，相当于 new XxxBean() |
  | request       | 每次HTTP请求都会创建一个新的Bean，该作用域仅适用于WebAppLicationContext环境 |
  | session       | 同一个HTTP Session共享一个Bean，不同Session使用不同Bean，仅适用于WebAppLicationContext环境 |
  | globalSession | 一般用于Portlet应用环境，该作用域仅适用于WebAppLicationContext环境 |

  

+ 配置信息

  + 单例

    `<bean id="" class="com.wang.userImpl"  ></bean>`

    调用两次Bean实例，一样
  
    com.wang.userImpl@a09316
  
    com.wang.userImpl@a09316
  
  + 多例
  
    `<bean id="" class="A" scope="prototype"></bean>`
  
    调用两次Bean实例，不一样
  
    com.wang.userImpl@5d9072
  
    com.wang.userImpl@b66600
  

### Bean的生命周期

#### 初始化销毁方法

+ init-method：用于配置初始化方法，用来**准备数据**等等

+ destory-method：用于配置销毁方法，用来**清理资源**

```xml
<bean id="" class="com.wang.userImpl" init-method="myInit" destory-method="myDestory"></bean>
```

```java
package com.wang.userImpl;

public void myInit(){
    system.out.printl("初始化")
}
public void myDestory(){
    system.out.printl("销毁")
}
```

+ 测试

```java
@Test
public void demo() throw Exception{
	String xmlPath = "com.wang.beans.xml";
	ApplicationContext applicationContext = new ClassPathXmlApplicationContext(xmlPath);
	UserService userService = (userService) applicationContext.getBean("userServiceId")
	userService.addUser;
	//1 容器必须close掉，销毁方法才会执行
    //2 必须是单例模式
	applicationContext.close();
}
```


#### 后处理Bean

+ spring提供一种机制，只要实现此接口BeanPostProcessor，并将实现类提供给Spring容器，容器将自动执行，在初始化方法之前执行before()方法，在初始化方法之后执行after()方法

+ Factory  hook that allows for custom modification of a new bean instances ,e g checking for marker interfaces or wrapping them with proxies

+ spring 提供工厂钩子，用于修改实例对象，可以生成代理对象，是AOP底层。

+ 模拟流程

  ```java
  A  a = new A();
  a = B.before(a);  // 把a传到before()方法，再return回来  a 变成了代理对象
  a.init();
  a = B.after(a);
  a.addUser();
  a.destory();
  ```

  

##### BeanPostProcessor简介

> BeanPostProcessor是Spring IOC容器给我们提供的一个扩展接口

```java
public interface BeanPostProcessor {
    //bean初始化方法调用前被调用
    Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException;
    //bean初始化方法调用后被调用
    Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;
}
```

运行顺序

1. Spring IOC容器实例化Bean
2. 调用BeanPostProcessor的postProcessBeforeInitialization方法
3. 调用bean实例的初始化方法
4. 调用BeanPostProcessor的postProcessAfterInitialization方法

##### BeanPostProcessor实例

```java
/**
 * 后置处理器：初始化前后进行处理工作
 * 将后置处理器加入到容器中
 */
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessBeforeInitialization..."+beanName+"=>"+bean);
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessAfterInitialization..."+beanName+"=>"+bean);
        return bean;
    }

}
```

##### 将后处理Bean的实现类注册给Spring

> Spring容器加入 MyBeanPostProcessor之后，针对容器中所有创建的Bean都会回调postProcessBeforeInitialization和postProcessAfterInitialization方法

```xml
<!--将后处理Bean的实现类注册给Spring-->
<bean id="" class="com.wang.MyBeanPostProcessor"></bean>
```
**配置完后处理Bean默认所有创建Bean都生效，如果想要在一个Bean里生效，可以在后处理Bean的方法中，通过BeanName用进行字符串判定,来决定加载哪一个Bean**

```java
//过滤掉bean实例ID为userService的bean，直接return 回去  
if ("userService".equals(beanName)) {
            return bean;
  }
```



##### 返回一个jdk动态代理对象

###### jdk动态代理简介

> JDK动态代理技术是在运行时直接生成类的字节码，并载入到虚拟机执行的。
>
> JDK动态代理技术必须面向接口
>
> JDK动态代理的实现是在运行时，根据一组接口定义，使用Proxy、InvocationHandler等工具类去生成一个代理类和代理类实例。
>
> Proxy是个工具类，有了它就可以为接口生成动态代理类了。如果需要进一步生成代理类实例，需要注入InvocationHandler实例。这点我们上面解释过，因为代理类最终逻辑的实现是分派给InvocationHandler实例的invoke方法的。
>
> Proxy.newProxyInstance方法创建一个动态代理类实例，这个方法需要传入三个参数，第一个参数是类加载器，用于加载这个代理类。第二个参数是Class数组，里面存放的是待实现的接口信息。第三个参数是InvocationHandler实例。
>
> newProxyInstance 它就是使用反射机制调用动态代理类的构造函数生成一个代理类实例的过程。
>
> InvocationHandler接口只有一个待实现的invoke方法。这个方法有三个参数，proxy表示动态代理类实例，method表示调用的方法，args表示调用方法的参数。在实际应用中，invoke方法就是我们实现业务逻辑的入口。
###### 动态代理实例

```java
// 每次生成动态代理类对象时,实现了InvocationHandler接口的调用处理器对象 
public class InvocationHandlerImpl implements InvocationHandler {
    private Object target;// 这其实业务实现类对象，用来调用具体的业务方法
    // 通过构造函数传入目标对象
    public InvocationHandlerImpl(Object target) {
        this.target = target;
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        Object result = null;
        System.out.println("调用开始处理");
        result = method.invoke(target, args);
        System.out.println("调用结束处理");
        return result;
    }
    public static void main(String[] args) throws NoSuchMethodException, SecurityException, InstantiationException,
            IllegalAccessException, IllegalArgumentException, InvocationTargetException {
        // 被代理对象
        IUserDao userDao = new UserDao();
        InvocationHandlerImpl invocationHandlerImpl = new InvocationHandlerImpl(userDao);
        ClassLoader loader = userDao.getClass().getClassLoader();
        Class<?>[] interfaces = userDao.getClass().getInterfaces();
        // 主要装载器、一组接口及调用处理动态代理实例
        IUserDao newProxyInstance = (IUserDao) Proxy.newProxyInstance(loader, interfaces, invocationHandlerImpl);
        newProxyInstance.save();
    }
}
```

###### CGLIB动态代理

+ 使用cglib[Code Generation Library]实现动态代理，并不要求委托类必须实现接口，底层采用asm字节码生成框架生成代理类的字节码

```java
public class CglibProxy implements MethodInterceptor {
    private Object targetObject;
    // 这里的目标类型为Object，则可以接受任意一种参数作为被代理类，实现了动态代理
    public Object getInstance(Object target) {
        // 设置需要创建子类的类
        this.targetObject = target;
        Enhancer enhancer = new Enhancer();
        enhancer.setSuperclass(target.getClass());
        enhancer.setCallback(this);
        return enhancer.create();
    }
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("开启事物");
        Object result = proxy.invoke(targetObject, args);
        System.out.println("关闭事物");
        // 返回代理对象
        return result;
    }
    public static void main(String[] args) {
        CglibProxy cglibProxy = new CglibProxy();
        UserDao userDao = (UserDao) cglibProxy.getInstance(new UserDao());
        userDao.save();
    }
}
```

###### CGLIB动态代理与JDK动态区别

+ java动态代理是利用反射机制生成一个实现代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理。

  而cglib动态代理是利用asm开源包，对代理对象类的class文件加载进来，通过修改其字节码生成子类来处理。

  Spring中。

  1. 如果目标对象实现了接口，默认情况下会采用JDK的动态代理实现AOP
  2. 如果目标对象实现了接口，可以强制使用CGLIB实现AOP
  3. 如果目标对象没有实现了接口，必须采用CGLIB库，spring会自动在JDK动态代理和CGLIB之间转换
  4. JDK动态代理只能对实现了接口的类生成代理，而不能针对类 。 CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法 。 因为是继承，所以该类或方法最好不要声明成final ，final可以阻止继承和多态。

###### 返回代理对象
```java
/**
 * 后置处理器：初始化前后进行处理工作
 * 将后置处理器加入到容器中
 * 返回一个代理对象
 */
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessBeforeInitialization..."+beanName+"=>"+bean);
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(final Object bean, String beanName) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("postProcessAfterInitialization..."+beanName+"=>"+bean);
        return Proxy.newProxyInstance(
        MyBeanPostProcessor.class.getClassLoader(),
            bean.getClass().getInterfaces(),
            new InvocationHandler(){
                @Override
                public Object invoke(Object proxy,Method method,Object[] args) throws Throwable{
                    //执行目标方法之前
                    system.out.println("----开启事务---")
                    
                    //执行目标方法
                    Object obj = method.invoke(bean,args);
                    
                    system.out.println("----提交事务---")
                    return obj;
                }
            }
         );
    }
}
```

+ 执行顺序为

```markdown
	1. 前方法    // postProcessBeforeInitialization
	2. 初始化    // myInit()
	3. 后方法    // postProcessAfterInitialization   return Proxy.newProxyInstance()
	4. ----开启事务---
	5. 目标方法  // Object obj = method.invoke(bean,args);
	6. ----提交事务---
	7. 销毁      // myDestory()
```

### 属性依赖注入

+ 依赖注入方式：手动装配和自动装配
  + 手动装配：一般进行配置信息都采用手动。基于xml装配：构造方法、setter方法
  + 基于注解装配

#### 构造方法

+ 目标类

```java
public class User {

    private Integer uid;
    private String username;
    private Integer age;

    public User(Integer uid, String username) {
        super();
        this.uid = uid;
        this.username = username;
    }

    public User(String username, Integer age) {
        super();
        this.username = username;
        this.age = age;
    }

```

+ spring 配置

```xml
<!-- 构造方法注入 
        * <constructor-arg> 用于配置构造方法一个参数argument
            name ：参数的名称
            value：设置普通数据
            ref：引用数据，一般是另一个bean id值

            index ：参数的索引号，从0开始 。如果只有索引，匹配到了多个构造方法时，默认使用第一个。
            type ：确定参数类型
        例如：使用名称name
            <constructor-arg name="username" value="jack"></constructor-arg>
            <constructor-arg name="age" value="18"></constructor-arg>
        例如2：【类型type 和  索引 index】
            <constructor-arg index="0" type="java.lang.String" value="1"></constructor-arg>
            <constructor-arg index="1" type="java.lang.Integer" value="2"></constructor-arg>
    -->
    <bean id="userId" class="com.itheima.f_xml.a_constructor.User" >
        <constructor-arg index="0" type="java.lang.String" value="1"></constructor-arg>
        <constructor-arg index="1" type="java.lang.Integer" value="2"></constructor-arg>
    </bean>
```

#### setter方法

```xml
<!-- setter方法注入 
        * 普通数据 
            <property name="" value="值">
            等效
            <property name="">
                <value>值
        * 引用数据
            <property name="" ref="另一个bean">
            等效
            <property name="">
                <ref bean="另一个bean"/>
    -->
    <bean id="personId" class="com.itheima.f_xml.b_setter.Person">
        <property name="pname" value="阳志"></property>
        <property name="age">
            <value>1234</value>
        </property>

        <property name="homeAddr" ref="homeAddrId"></property>
        <property name="companyAddr">
            <ref bean="companyAddrId"/>
        </property>
    </bean>

    <bean id="homeAddrId" class="com.itheima.f_xml.b_setter.Address">
        <property name="addr" value="阜南"></property>
        <property name="tel" value="911"></property>
    </bean>
    <bean id="companyAddrId" class="com.itheima.f_xml.b_setter.Address">
        <property name="addr" value="北京八宝山"></property>
        <property name="tel" value="120"></property>
    </bean>
```

#### 集合注入

```xml
<!-- 
        集合的注入都是给<property>添加子标签
            数组：<array>
            List：<list>
            Set：<set>
            Map：<map> ，map存放k/v 键值对，使用<entry>描述
            Properties：<props>  <prop key=""></prop>  【】

        普通数据：<value>
        引用数据：<ref>
    -->
    <bean id="collDataId" class="com.itheima.f_xml.e_coll.CollData" >
        <property name="arrayData">
            <array>
                <value>DS</value>
                <value>DZD</value>
                <value>屌丝</value>
                <value>屌中屌</value>
            </array>
        </property>

        <property name="listData">
            <list>
                <value>于嵩楠</value>
                <value>曾卫</value>
                <value>杨煜</value>
                <value>曾小贤</value>
            </list>
        </property>

        <property name="setData">
            <set>
                <value>停封</value>
                <value>薄纸</value>
                <value>关系</value>
            </set>
        </property>

        <property name="mapData">
            <map>
                <entry key="jack" value="杰克"></entry>
                <entry>
                    <key><value>rose</value></key>
                    <value>肉丝</value>
                </entry>
            </map>
        </property>

        <property name="propsData">
            <props>
                <prop key="高富帅">嫐</prop>
                <prop key="白富美">嬲</prop>
                <prop key="男屌丝">挊</prop>
            </props>
        </property>
    </bean>
```

## 基于注解装备Bean

+ 注解：就是一个类, 使用@注解名称

+ 开发中：使用注解 取代 xml配置文件。

  1.  @Component取代 `<bean class="">`
  2.  @Component("id") 取代 `<bean id="" class="">`
  3.  web开发，提供3个@Component注解衍生注解（功能一样）取代
      + @Repository ：dao层
      + @Service：service层
      + @Controller：web层
  4.  依赖注入，给私有字段设值，也可以给setter方法设值
      + 普通值：@Value(" ")
      + 引用值
        1. 方式1：按照【类型】注入@Autowired
        2. @Autowired   @Qualifier("名称")
        3. 方式3：按照【名称】注入2    @Resource("名称")
        4. 生命周期 
           + 初始化：@PostConstruct
           + 销毁：@PreDestroy
        5. 作用域  @Scope("prototype") 多例
           + 注解使用前提，添加命名空间，让spring扫描含有注解类
  

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:context="http://www.springframework.org/schema/context"
   xsi:schemaLocation="http://www.springframework.org/schema/beans 
                       http://www.springframework.org/schema/beans/spring-beans.xsd
                       http://www.springframework.org/schema/context 
                       http://www.springframework.org/schema/context/spring-context.xsd">
<!-- 组件扫描，扫描含有注解的类 -->
<context:component-scan base-package="com.itheima.g_annotation.a_ioc"></context:component-scan>
</beans>
```

## AOP面向切面编程

### 什么是AOP

+ 在软件业，AOP为Aspect Oriented Programming的缩写，意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP（面向对象编程）的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。
+ AOP采取横向抽取机制，取代了传统纵向继承体系重复性代码
+ 经典应用：事务管理、性能监视、安全检查、缓存 、日志等
+ Spring AOP使用纯Java实现，不需要专门的编译过程和类加载器，在运行期通过代理方式向目标类织入增强代码
+ AspectJ是一个基于Java语言的AOP框架，Spring2.0开始，Spring AOP引入对Aspect的支持，AspectJ扩展了Java语言，提供了一个专门的编译器，在编译时提供横向代码的织入

### AOP实现原理

+ aop底层将采用代理机制进行实现；
+ 接口 + 实现类 ：spring采用 jdk 的动态代理Proxy。
+ 实现类：spring 采用 cglib字节码增强。

### AOP术语

1. target：目标类，需要被代理的类。例如：UserService

2. Joinpoint(连接点):所谓连接点是指那些可能被拦截到的方法。例如：所有的方法

3. PointCut 切入点：已经被增强的连接点。例如：addUser()

4. advice 通知/增强，增强代码。例如：after、before

5. Weaving(织入):是指把增强advice应用到目标对象target来创建新的代理对象proxy的过程.

6. proxy 代理类

7. Aspect(切面): 是切入点pointcut和通知advice的结合

   一个线是一个特殊的面。
   一个切入点和一个通知，组成成一个特殊的面。

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-17_214615.png)

### AOP实现方式

#### 手动方式

##### 静态代理

+ 由程序员创建或工具生成代理类的源码，再编译代理类。所谓静态也就是在程序运行前就已经存在代理类的字节码文件，代理类和委托类的关系在运行前就确定了。

  ```java
  public interface IUserDao {
      void save();
  }
  public class UserDao implements IUserDao {
      public void save() {
          System.out.println("已经保存数据...");
      }
  }
  代理类
  public class UserDaoProxy implements IUserDao {
      private IUserDao target;
      public UserDaoProxy(IUserDao iuserDao) {
          this.target = iuserDao;
      }
      public void save() {
          System.out.println("开启事物...");
          target.save();
          System.out.println("关闭事物...");
      }
  }
  
  ```

  

##### jdk动态代理

> JDK动态代理 对“装饰者”设计模式 简化。使用前提：必须有接口

+ 目标类：接口 + 实现类

  ```java
  public interface UserService {
      public void addUser();
      public void updateUser();
      public void deleteUser();
  }
  ```

+ 切面类：用于存通知 MyAspect

  ```java
  public class MyAspect { 
      public void before(){
          System.out.println("鸡首");
      }   
      public void after(){
          System.out.println("牛后");
      }
  }
  ```

+ 工厂类：编写工厂生成代理

  ```java
  public class MyBeanFactory {
  
      public static UserService createService(){
          //1 目标类
          final UserService userService = new UserServiceImpl();
          //2切面类
          final MyAspect myAspect = new MyAspect();
          /* 3 代理类：将目标类（切入点）和 切面类（通知） 结合 --> 切面
           *  Proxy.newProxyInstance
           *      参数1：loader ，类加载器，动态代理类 运行时创建，任何类都需要类加载器将其加载到内存。
           *          一般情况：当前类.class.getClassLoader();
           *                  目标类实例.getClass().get...
           *      参数2：Class[] interfaces 代理类需要实现的所有接口
           *          方式1：目标类实例.getClass().getInterfaces()  ;注意：只能获得自己接口，不能获得父元素接口
           *          方式2：new Class[]{UserService.class}   
           *          例如：jdbc 驱动  --> DriverManager  获得接口 Connection
           *      参数3：InvocationHandler  处理类，接口，必须进行实现类，一般采用匿名内部
           *          提供 invoke 方法，代理类的每一个方法执行时，都将调用一次invoke
           *              参数31：Object proxy ：代理对象
           *              参数32：Method method : 代理对象当前执行的方法的描述对象（反射）
           *                  执行方法名：method.getName()
           *                  执行方法：method.invoke(对象，实际参数)
           *              参数33：Object[] args :方法实际参数
           * 
           */
          UserService proxService = (UserService)Proxy.newProxyInstance(
                                  MyBeanFactory.class.getClassLoader(), 
                                  userService.getClass().getInterfaces(), 
                                  new InvocationHandler() {
  
                                      @Override
                                      public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
  
                                          //前执行
                                          myAspect.before();
  
                                          //执行目标类的方法
                                          Object obj = method.invoke(userService, args);
  
                                          //后执行
                                          myAspect.after();
  
                                          return obj;
                                      }
                                  });
  
          return proxService;
      }
  
  }
  ```

+ 测试

  ```java
  @Test
      public void demo01(){
          UserService userService = MyBeanFactory.createService();
          userService.addUser();
          userService.updateUser();
          userService.deleteUser();
      }
  ```


##### 字节码增强

> 没有接口，只有实现类。采用字节码增强框架 cglib，在运行时 创建目标类的子类，从而对目标类进行增强。
+ 工厂类

  ```java
  public class MyBeanFactory {
  
      public static UserServiceImpl createService(){
          //1 目标类
          final UserServiceImpl userService = new UserServiceImpl();
          //2切面类
          final MyAspect myAspect = new MyAspect();
          // 3.代理类 ，采用cglib，底层创建目标类的子类
          //3.1 核心类
          Enhancer enhancer = new Enhancer();
          //3.2 确定父类
          enhancer.setSuperclass(userService.getClass());
          /* 3.3 设置回调函数 , MethodInterceptor接口 等效 jdk InvocationHandler接口
           *  intercept() 等效 jdk  invoke()
           *      参数1、参数2、参数3：以invoke一样
           *      参数4：methodProxy 方法的代理
           */
          enhancer.setCallback(new MethodInterceptor(){
              @Override
              public Object intercept(Object proxy, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {
                  //前
                  myAspect.before();
                  //执行目标类的方法
                  Object obj = method.invoke(userService, args);
                  // * 执行代理类的父类 ，执行目标类 （目标类和代理类 父子关系）
                  methodProxy.invokeSuper(proxy, args);
                  //后
                  myAspect.after();
                  return obj;
              }
          });
          //3.4 创建代理
          UserServiceImpl proxService = (UserServiceImpl) enhancer.create();
          return proxService;
      }
  
  }
  ```

  
#### 半自动

> 让spring 创建代理对象，从spring容器中手动的获取代理对象
+ 目标类

  ```java
  public interface UserService {
      public void addUser();
      public void updateUser();
      public void deleteUser();
  }
  ```

+ 切面类

  ```java
  /**
   * 切面类中确定通知，需要实现不同接口，接口就是规范，从而就确定方法名称。
   * * 采用“环绕通知” MethodInterceptor
   *
   */
  public class MyAspect implements MethodInterceptor {
  
      @Override
      public Object invoke(MethodInvocation mi) throws Throwable {
  
          System.out.println("前3");
  
          //手动执行目标方法
          Object obj = mi.proceed();
  
          System.out.println("后3");
          return obj;
      }
  }
  ```

+ spring配置

  ```xml
  <!-- 1 创建目标类 -->
      <bean id="userServiceId" class="com.itheima.b_factory_bean.UserServiceImpl"></bean>
      <!-- 2 创建切面类 -->
      <bean id="myAspectId" class="com.itheima.b_factory_bean.MyAspect"></bean>
  
      <!-- 3 创建代理类 
          * 使用工厂bean FactoryBean ，底层调用 getObject() 返回特殊bean
          * ProxyFactoryBean 用于创建代理工厂bean，生成特殊代理对象
              interfaces : 确定接口们
                  通过<array>可以设置多个值
                  只有一个值时，value=""
              target : 确定目标类
              interceptorNames : 通知 切面类的名称，类型String[]，如果设置一个值 value=""
              optimize :强制使用cglib
                  <property name="optimize" value="true"></property>
          底层机制
              如果目标类有接口，采用jdk动态代理
              如果没有接口，采用cglib 字节码增强
              如果声明 optimize = true ，无论是否有接口，都采用cglib
      -->
      <bean id="proxyServiceId" class="org.springframework.aop.framework.ProxyFactoryBean">
          <property name="interfaces" value="com.itheima.b_factory_bean.UserService"></property>
          <property name="target" ref="userServiceId"></property>
          <property name="interceptorNames" value="myAspectId"></property>
      </bean>
  ```

+ 测试

  ```java
  @Test
      public void demo01(){
          String xmlPath = "com/itheima/b_factory_bean/beans.xml";
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext(xmlPath);
  
          //获得代理类
          UserService userService = (UserService) applicationContext.getBean("proxyServiceId");
          userService.addUser();
          userService.updateUser();
          userService.deleteUser();
      }
  ```
#### 全自动

> 从spring容器获得目标类，如果配置aop，spring将自动生成代理

+ Spring配置

  ```java
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans 
                             http://www.springframework.org/schema/beans/spring-beans.xsd
                             http://www.springframework.org/schema/aop 
                             http://www.springframework.org/schema/aop/spring-aop.xsd">
      <!-- 1 创建目标类 -->
      <bean id="userServiceId" class="com.itheima.c_spring_aop.UserServiceImpl"></bean>
      <!-- 2 创建切面类（通知） -->
      <bean id="myAspectId" class="com.itheima.c_spring_aop.MyAspect"></bean>
      <!-- 3 aop编程 
          3.1 导入命名空间
          3.2 使用 <aop:config>进行配置
                  proxy-target-class="true" 声明时使用cglib代理
              <aop:pointcut> 切入点 ，从目标对象获得具体方法
              <aop:advisor> 特殊的切面，只有一个通知 和 一个切入点
                  advice-ref 通知引用
                  pointcut-ref 切入点引用
          3.3 切入点表达式
              execution(* com.itheima.c_spring_aop.*.*(..))
              选择方法         返回值任意   包             类名任意   方法名任意   参数任意
  
      -->
      <aop:config proxy-target-class="true">
          <aop:pointcut expression="execution(* com.itheima.c_spring_aop.*.*(..))" id="myPointCut"/>
          <aop:advisor advice-ref="myAspectId" pointcut-ref="myPointCut"/>
      </aop:config>
  </beans>
  ```

+ 测试

  ```java
  @Test
      public void demo01(){
          String xmlPath = "com/itheima/c_spring_aop/beans.xml";
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext(xmlPath);
  
          //获得目标类
          UserService userService = (UserService) applicationContext.getBean("userServiceId");
          userService.addUser();
          userService.updateUser();
          userService.deleteUser();
      }
  
  ```

  

## Aspect
### 切入点表达式

+ execution()用于描述方法
  + 语法：execution(修饰符 返回值 包 类 方法(参数) throw 异常)
    + 修饰符，一般省略，public 公共方法，*****任意
    + 返回值，void 返回没有值，String 返回字符串， ***** 任意
    + 包(省略)
      + com.wang.user                   固定包
      + com.wang.user.*.service    user包下面子包任意(例如：com.wang.user.student.service)
      + com.wang.user..                 user包下面的所有子包
      + com.wang.user.*.service..  user包下面任意子包，固定目录service，service目录任意包
    + 类(省略)
      + UserServiceImpl     制定类
      + Impl                        以Impl结尾
      + User*                      以User开头
      + 只有*                      表示任意
    + 方法名：(不能省略)
      + addUser                 固定方法
      + add*                       以add开头
      + *Do                        以Do结尾
    + 参数
      + ()                          无参
      + (int)                      一个整型
      + (int,int)                两个整型
      + (..)                       任意参数

    + throw，可省略，一般不写

+ 综合表达式，示例

  返回值任意，固定包，任意子包，service层下的任意接口以及实现类，任意方法名，任意参数

  `execution(*com.wang.*.service..*.*(..))`

### 通知类型

+ aop联盟定义通知类型，具有特性接口，必须实现，从而确定方法名称

+ aspectj通知类型，只定义类型名称，已经方法格式。

+ 通知类型如下5种，**around**必须掌握，其他稍作了解。

  1. before前置通知(应用，各种校验)

     + 在方法执行前执行，如果抛出异常，通知无法执行
  2. afterRrturning后置通知(应用常规数据处理)
  
     + 方法正常返回后执行，如果方法抛出异常，通知无法执行
  
     + 必须在方法执行后执行，所以可以获取方法的返回值
  3. **around** **环绕通知(应用十分强大，可以做任何事)**
     + 方法执行前后分别抛出异常，可以阻止方法的执行
     + 必须手动执行目标方法
  4. afterThrowing 抛出异常通知(应用 包装异常信息)
     + 方法执行完毕后执行，如果方法没有抛出异常，则无法执行
  5. after最终通知(应用 清理现场)
     + 方法执行完毕后执行，无论方法中是否出现异常

### AOP编程

#### 注解版使用AOP

```java
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>  开启事物注解权限
@Aspect                         指定一个类为切面类       
@Pointcut("execution(* com.service.UserService.add(..))")  指定切入点表达式
@Before("pointCut_()")              前置通知: 目标方法之前执行
@After("pointCut_()")               后置通知：目标方法之后执行（始终执行）
@AfterReturning("pointCut_()")       返回后通知： 执行方法结束前执行(异常不执行)
@AfterThrowing("pointCut_()")           异常通知:  出现异常时候执行
@Around("pointCut_()")              环绕通知： 环绕目标方法执行

@Component
@Aspect
public class AopLog {
    // 前置通知
    @Before("execution(* com.service.UserService.add(..))")
    public void begin() {
        System.out.println("前置通知");
    }
    // 后置通知
    @After("execution(* com.service.UserService.add(..))")
    public void commit() {
        System.out.println("后置通知");
    }
    // 运行通知
    @AfterReturning("execution(* com.service.UserService.add(..))")
    public void returning() {
        System.out.println("运行通知");
    }
    // 异常通知
    @AfterThrowing("execution(* com.service.UserService.add(..))")
    public void afterThrowing() {
        System.out.println("异常通知");
    }
    // 环绕通知
    @Around("execution(* com.service.UserService.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕通知开始");
        proceedingJoinPoint.proceed();
        System.out.println("环绕通知结束");
    }
}
```

#### XML使用AOP

> Xml实现aop编程：
>     1） 引入jar文件  【aop 相关jar， 4个】
>     2） 引入aop名称空间
>     3）aop 配置
>         * 配置切面类 （重复执行代码形成的类）
>                 * aop配置
>             拦截哪些方法 / 拦截到方法后应用通知代码

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- dao 实例 -->

    <bean id="userService" class="com.service.UserService"></bean>
    <!-- 切面类 -->
    <bean id="aop" class="com.aop2.AopLog2"></bean>
    <!-- Aop配置 -->
    <aop:config>
        <!-- 定义一个切入点表达式： 拦截哪些方法 -->
        <aop:pointcut expression="execution(* com.service.UserService.*(..))"
            id="pt" />
        <!-- 切面 -->
        <aop:aspect ref="aop">
            <!-- 环绕通知 -->
            <aop:around method="around" pointcut-ref="pt" />
            <!-- 前置通知： 在目标方法调用前执行 -->
            <aop:before method="begin" pointcut-ref="pt" />
            <!-- 后置通知： -->
            <aop:after method="after" pointcut-ref="pt" />
            <!-- 返回后通知 -->
            <aop:after-returning method="afterReturning"
                pointcut-ref="pt" />
            <!-- 异常通知 -->
            <aop:after-throwing method="afterThrowing"
                pointcut-ref="pt" />
        </aop:aspect>
    </aop:config>

</beans>

```

```java
public class AopLog2 {

    // 前置通知
    public void begin() {
        System.out.println("前置通知");
    }

    //
    // 后置通知
    public void commit() {
        System.out.println("后置通知");
    }

    // 运行通知
    public void returning() {
        System.out.println("运行通知");

    // 异常通知
    public void afterThrowing() {
        System.out.println("异常通知");
    }

    // 环绕通知
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕通知开始");
        proceedingJoinPoint.proceed();
        System.out.println("环绕通知结束");
    }


```

## 事务管理

> 事务：一组业务操作ABCD，要么全部成功，要么全部不成功

### jdbc事务管理

#### 事务的原理

> Spring事务的本质其实就是数据库对事务的支持，使用JDBC的事务管理机制,就是利用java.sql.Connection对象完成对事务的提交，那在没有Spring帮我们管理事务之前，我们要怎么做

```java
Connection conn = DriverManager.getConnection();
try {  
    conn.setAutoCommit(false);  //将自动提交设置为false                         
    执行CRUD操作 
    conn.commit();      //当两个操作成功后手动提交  
} catch (Exception e) {  
    conn.rollback();    //一旦其中一个操作出错都将回滚，所有操作都不成功
    e.printStackTrace();  
} finally {
    conn.colse();
}
```

​         **事务是一系列的动作，一旦其中有一个动作出现错误，必须全部回滚，系统将事务中对数据库的所有已完成的操作全部撤消，滚回到事务开始的状态，避免出现由于数据不一致而导致的接下来一系列的错误。事务的出现是为了确保数据的完整性和一致性，在目前企业级应用开发中，事务管理是必不可少的。**

#### 事务的四大特性

1. 原子性：整体
   + 由一系列动作组成。事务的原子性确保动作要么全部完成，要么完全不起作用。
2. 一致性：完成
   + 事务在完成时，必须是所有的数据都保持一致状态。
3. 隔离性：并发
   + 并发事务执行之间无影响，在一个事务内部的操作对其他事务是不产生影响，这需要事务隔离级别来指定隔离性。
4. 持久性：结果
   + 一旦事务完成，数据库的改变必须是持久化的。

#### 隔离问题

1. 脏读

   一个事务读到另外一个事务没有提交的数据

2. 不可重复读

   一个事务读到另一个已提交的数据(update)

3. 虚读/幻读

   一个事务读到另一个已提交的数据(insert)

#### 隔离级别

   

| 级别             | 解释                                           |
| ---------------- | ---------------------------------------------- |
| read uncommitted | 读未提交，存在三个问题                         |
| read committed   | 读已提交，解决脏读，存在两个问题               |
| repeatable read  | 可重复读，解决：脏读，不可重复度，存在一个问题 |
| serializable     | 串行化。都解决了，单事务                       |

+ 我们可以在java.sql.Connection中看到JDBC定义了五种事务隔离级别来解决这些并发导致的问题：

```java
/**
 * A constant indicating that transactions are not supported. 驱动不支持事务
 */
int TRANSACTION_NONE         = 0;   

/**
 * A constant indicating that                                 允许脏读、不可重复读和幻读。
 * dirty reads, non-repeatable reads and phantom reads can occur.
 * This level allows a row changed by one transaction to be read
 * by another transaction before any changes in that row have been
 * committed (a "dirty read").  If any of the changes are rolled back, 
 * the second transaction will have retrieved an invalid row.
 */
int TRANSACTION_READ_UNCOMMITTED = 1;

/**
 * A constant indicating that                                 禁止脏读，但允许不可重复读和幻读。
 * dirty reads are prevented; non-repeatable reads and phantom
 * reads can occur.  This level only prohibits a transaction
 * from reading a row with uncommitted changes in it.
 */
int TRANSACTION_READ_COMMITTED   = 2;

/**
 * A constant indicating that                               禁止脏读和不可重复读，单运行幻读。
 * dirty reads and non-repeatable reads are prevented; phantom
 * reads can occur.  This level prohibits a transaction from
 * reading a row with uncommitted changes in it, and it also
 * prohibits the situation where one transaction reads a row,
 * a second transaction alters the row, and the first transaction
 * rereads the row, getting different values the second time
 * (a "non-repeatable read").
 */
int TRANSACTION_REPEATABLE_READ  = 4;

/**
 * A constant indicating that                                   禁止脏读、不可重复读和幻读。
 * dirty reads, non-repeatable reads and phantom reads are prevented.
 * This level includes the prohibitions in
 * <code>TRANSACTION_REPEATABLE_READ</code> and further prohibits the 
 * situation where one transaction reads all rows that satisfy
 * a <code>WHERE</code> condition, a second transaction inserts a row that
 * satisfies that <code>WHERE</code> condition, and the first transaction
 * rereads for the same condition, retrieving the additional
 * "phantom" row in the second read.
 */
int TRANSACTION_SERIALIZABLE     = 8;
```

```markdown
	翻译过来这几个常量就是
	TRANSACTION_NONE JDBC 驱动不支持事务
	TRANSACTION_READ_UNCOMMITTED 允许脏读、不可重复读和幻读。
	TRANSACTION_READ_COMMITTED 禁止脏读，但允许不可重复读和幻读。
	TRANSACTION_REPEATABLE_READ 禁止脏读和不可重复读，单运行幻读。
	TRANSACTION_SERIALIZABLE 禁止脏读、不可重复读和幻读。

	隔离级别越高，意味着数据库事务并发执行性能越差，能处理的操作就越少。你可以通过conn.setTransactionLevel去设置你需要的隔离级别。
	JDBC规范虽然定义了事务的以上支持行为，但是各个JDBC驱动，数据库厂商对事务的支持程度可能各不相同。
	出于性能的考虑我们一般设置TRANSACTION_READ_COMMITTED就差不多了，剩下的通过使用数据库的锁来帮我们处理别的，关于数据库的锁这个之后再说。

	了解了基本的JDBC事务，那有了Spring，在事务管理上会有什么新的改变呢？
	有了Spring，我们再也无需要去处理获得连接、关闭连接、事务提交和回滚等这些操作，使得我们把更多的精力放在处理业务上。事实上Spring并不直接管理事务，而是提供了多种事务管理器。他们将事务管理的职责委托给Hibernate或者JTA等持久化机制所提供的相关平台框架的事务来实现。
```

### Spring事务管理

+ Spring事务管理的核心接口是PlatformTransactionManager

  ![](C:\Users\Administrator\Desktop\markdown\images\2020-04-19_232545.png)

+ 事务管理器接口通过getTransaction(TransactionDefinition definition)方法根据指定的传播行为返回当前活动的事务或创建一个新的事务，这个方法里面的参数是TransactionDefinition类，这个类就定义了一些基本的事务属性。
  在TransactionDefinition接口中定义了它自己的传播行为和隔离级别

  ![](C:\Users\Administrator\Desktop\markdown\images\2020-04-19_232751.png)

  ### Spring事务的传播属性

  + 由上图可知，Spring定义了7个以PROPAGATION_开头的常量表示它的传播属性。

    | 名称                      | 值   | 解释                                                         |
    | ------------------------- | ---- | ------------------------------------------------------------ |
    | PROPAGATION_REQUIRED      | 0    | 支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择，也是Spring默认的事务的传播。 |
    | PROPAGATION_SUPPORTS      | 1    | 支持当前事务，如果当前没有事务，就以非事务方式执行。         |
    | PROPAGATION_MANDATORY     | 2    | 支持当前事务，如果当前没有事务，就抛出异常。                 |
    | PROPAGATION_REQUIRES_NEW  | 3    | 新建事务，如果当前存在事务，把当前事务挂起。                 |
    | PROPAGATION_NOT_SUPPORTED | 4    | 以非事务方式执行操作，如果当前存在事务，就把当前事务挂起     |
    | PROPAGATION_NEVER         | 5    | 以非事务方式执行，如果当前存在事务，则抛出异常               |
    | PROPAGATION_NESTED        | 6    | 如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则进行与PROPAGATION_REQUIRED类似的操作 |

### 事务的隔离级别

|            名称            | 值   |                             解释                             |
| :------------------------: | ---- | :----------------------------------------------------------: |
|     ISOLATION_DEFAULT      | -1   | 这是一个PlatfromTransactionManager默认的隔离级别，使用数据库默认的事务隔离级别。另外四个与JDBC的隔离级别相对应 |
| ISOLATION_READ_UNCOMMITTED | 1    | 这是事务最低的隔离级别，它充许另外一个事务可以看到这个事务未提交的数据。这种隔离级别会产生脏读，不可重复读和幻读。 |
|  ISOLATION_READ_COMMITTED  | 2    | 保证一个事务修改的数据提交后才能被另外一个事务读取。另外一个事务不能读取该事务未提交的数据。 |
| ISOLATION_REPEATABLE_READ  | 4    | 这种事务隔离级别可以防止脏读，不可重复读。但是可能出现幻读。 |
|   ISOLATION_SERIALIZABLE   | 8    | 这是花费最高代价但是最可靠的事务隔离级别。事务被处理为顺序执行。除了防止脏读，不可重复读外，还避免了幻读。 |

+ 调用PlatformTransactionManager接口的getTransaction()的方法得到的是TransactionStatus接口的一个实现
  TransactionStatus接口

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-19_235531.png)

​            **可以看出返回的结果是一些事务的状态，可用来检索事务的状态信息。**

### 配置事务管理

> 介绍完Spring事务的管理的流程大概是怎么走的。接下来可以动手试试Spring是如何配置事务管理器的
> 例如我在spring-mybatis中配置的:

```xml
<!-- 配置事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource" />
</bean>
```

+ 这配置不是唯一的，可以根据自己项目选择的数据访问框架灵活配置事务管理器

  配置了事务管理器后，事务当然还是得我们自己去操作，Spring提供了两种事务管理的方式：编程式事务管理和声明式事务管理，让我们分别看看它们是怎么做的吧。

### 编程式事务管理

> 编程式事务管理我们可以通过PlatformTransactionManager实现来进行事务管理，同样的Spring也为我们提供了模板类TransactionTemplate进行事务管理，下面主要介绍模板类，我们需要在配置文件中配置

```xml
  <!--配置事务管理的模板-->
    <bean id="transactionTemplate" class="org.springframework.transaction.support.TransactionTemplate">
        <property name="transactionManager" ref="transactionManager"></property>
        <!--定义事务隔离级别,-1表示使用数据库默认级别-->
        <property name="isolationLevelName" value="ISOLATION_DEFAULT"></property>
        <property name="propagationBehaviorName" value="PROPAGATION_REQUIRED"></property>
    </bean>
```

> TransactionTemplate帮我们封装了许多代码，节省了我们的工作。下面我们写个单元测试来测测。
> 为了测试事务回滚，专门建了一张tbl_accont表，用于模拟存钱的一个场景。service层主要代码如下，后面会给出全部代码的github地址，有需要的朋友请移步查看。
> BaseSeviceImpl
+ baseServiceImpl
```java
 //方便测试直接写的sql
    @Override
    public void insert(String sql, boolean flag) throws Exception {
        dao.insertSql(sql);
        // 如果flag 为 true ，抛出异常
        if (flag){
            throw new Exception("has exception!!!");
        }
    }
    //获取总金额
    @Override
    public Integer sum(){
        return dao.sum();
    }
```

+ dao对应的sum方法

```xml
  <select id="sum" resultType="java.lang.Integer">
        SELECT SUM(money) FROM tbl_account;
    </select>
```

+ 测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = {"classpath:spring-test.xml"})
public class TransactionTest{ 
    @Resource
    private TransactionTemplate transactionTemplate;
    @Autowired
    private BaseSevice baseSevice;

    @Test
    public void transTest() {
        System.out.println("before transaction");
        Integer sum1 = baseSevice.sum();
        System.out.println("before transaction sum: "+sum1);
        System.out.println("transaction....");
        transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            @Override
            protected void doInTransactionWithoutResult(TransactionStatus status) {
                try{
                    baseSevice.insert("INSERT INTO tbl_account VALUES (100);",false);
                    baseSevice.insert("INSERT INTO tbl_account VALUES (100);",false);
                } catch (Exception e){
                    //对于抛出Exception类型的异常且需要回滚时,需要捕获异常并通过调用status对象的setRollbackOnly()方法告知事务管理器当前事务需要回滚
                    status.setRollbackOnly();
                    e.printStackTrace();
                }
           }
        });
        System.out.println("after transaction");
        Integer sum2 = baseSevice.sum();
        System.out.println("after transaction sum: "+sum2);
    }
}
```

+ 当baseSevice.insert的第二个参数为false时，我们假设插入数据没有出现任何问题
+ 当第二个参数为true时，insert会抛出一个异常，这是事务就应该回滚，数据前后不应该有变化

### 声明式事务管理

> 声明式事务管理有两种常用的方式，一种是基于tx和aop命名空间的xml配置文件，一种是基于@Transactional注解，随着Spring和Java的版本越来越高，大家越趋向于使用注解的方式，下面我们两个都说。

#### 基于tx和aop命名空间的xml配置文件

+ 配置信息

```xml
   <tx:advice id="advice" transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="insert" propagation="REQUIRED" read-only="false"  rollback-for="Exception"/>
        </tx:attributes>
    </tx:advice>

    <aop:config>
        <aop:pointcut id="pointCut" expression="execution (* com.gray.service.*.*(..))"/>
        <aop:advisor advice-ref="advice" pointcut-ref="pointCut"/>
    </aop:config>
```

+ 测试代码

```java
  @Test
    public void transTest() {
        System.out.println("before transaction");
        Integer sum1 = baseSevice.sum();
        System.out.println("before transaction sum: "+sum1);
        System.out.println("transaction....");
        try{
            baseSevice.insert("INSERT INTO tbl_account VALUES (100);",true);
        } catch (Exception e){
            e.printStackTrace();
        }
        System.out.println("after transaction");
        Integer sum2 = baseSevice.sum();
        System.out.println("after transaction sum: "+sum2);
    }
```

#### 基于@Transactional注解

> 这种方式最简单，也是最为常用的，只需要在配置文件中开启对注解事务管理的支持。

```xml
  <!-- 声明式事务管理 配置事物的注解方式注入-->
    <tx:annotation-driven transaction-manager="transactionManager"/>
```

+ 然后在需要事务管理的地方加上@Transactional注解

```java
@Transactional(rollbackFor=Exception.class)
    public void insert(String sql, boolean flag) throws Exception {
        dao.insertSql(sql);
        // 如果flag 为 true ，抛出异常
        if (flag){
            throw new Exception("has exception!!!");
        }
    }
```

+ rollbackFor属性指定出现Exception异常的时候回滚，遇到检查性的异常需要回滚，默认情况下非检查性异常，包括error也会自动回滚。测试代码和上面那个一样