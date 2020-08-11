## SpringBoot综合

### test测试

+ pom文件依赖

  

  ```xml
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
      </dependency>
  ```

+ 引入类

  

  ```java
  import org.junit.Test;
  import org.junit.runner.RunWith;
  import org.springframework.boot.test.context.SpringBootTest;
  import org.springframework.test.context.junit4.SpringRunner;
  ```

+ 类必须是public的，否则报错 例如

```java
@SpringBootTest(classes = Springbootdemo3Application.class)
@RunWith(SpringRunner.class)
public class Springbootdemo3ApplicationTests {
    @Autowired
    userService userService;
    @Test
    public void contextLoads() {
        userService.findById(1);
    }
}
```

### mysql数据库

+ pom依赖

  + mysql依赖

    

    ```xml
             <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
            </dependency>
    ```

  + druiid依赖

    ``````      xml
             <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>1.1.12</version>
                <scope>compile</scope>
            </dependency>
    ``````

+ application.properties/yml 配置文件

  ``````properties
  spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
  #spring.datasource.driver-class-name=com.mysql.jdbc.Driver //可以不写
  spring.datasource.url=jdbc:mysql://49.234.18.34:3306/wang?characterEncoding=UTF-8
  spring.datasource.username=root
  spring.datasource.password=root
  ``````

### mybatis框架

+ pom依赖

  ``````xml
          <dependency>
              <groupId>org.mybatis.spring.boot</groupId>
              <artifactId>mybatis-spring-boot-starter</artifactId>
              <version>2.1.2</version>
          </dependency>
  ``````

+ 配置文件

  ``````yaml
  mybatis:
    mapper-locations: classpath:com/wang/mapper/*.xml
    type-aliases-package: com.wang.entiy
  ``````

+ 查询方式

  + xml文件

    ``````xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
    <mapper namespace="com.wang.dao.LoveDao">
        <select id="findAll" resultType="com.wang.entity.Love">
          ...
        </select>
        <insert id="save" parameterType="com.wang.entity.Love">
         ...
        </insert>
    </mapper>
    ``````

  + 注解查询

    ``````java
        @Select("select id,name from t_user where id = #{id}")
        public User findById(Integer id);
        @Update("update t_user set name = #{name} WHERE id = #{id}")
        public void UpdateUserById(User user);
        @Delete("DELETE from t_user WHERE id = #{id}")
        public void DeleteUserById(Integer id);
        @Insert("insert into t_user values(#{id},#{name})")
        public User saveUser(User user);
    ``````

+ mapper 自动转换驼峰命名法配置

  > 比如数据库中的字段 student_id 转化为 studentId 和java中的实体类相对应

  

  ```properties
  mybatis.configuration.map-underscore-to-camel-case=true
  ```

