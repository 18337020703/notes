## cache笔记

### spring默认缓存  

**simpleCacheConfiguration  储存在JavaJVM中**

#### javaCaching

+ JavaCaching定义了五个核心接口分别是
  1. CachingProvider 定义了创建，配置，获取，管理和控制多个CacheManager，一个应用运行期间可以访问多个CachingProvider
  2. CacheManger 定义了创建，配置，获取，管理和控制多个Cache，这些Cache存放在CacheManager的上下文中，CacheManager仅被一个CacheingProvider拥有
  3. Cache是一个类似于Map的数据结构，临时储存以key为索引的值，一个Cache仅被一个CacheManager所拥有
  4. Entry 是一个储存在Cache中的 key - value 对
  5. Expiry 每一个储存在Cache中的条目有一个定义的有效期，一旦超过这个时间，条目为过期的状态，条目将不可被访问，更新和删除，缓存有效期可以用ExpiryPolicy设置

![缓存关系图](C:\Users\Administrator\Desktop\markdown\img\2020-04-06_155613.png)



+++



#### 源码分析

源码分析

+ 自动配置类  CacheAutoConfiguration

+ 缓存的配置类

  *开启缓存，自动配置类依次加载缓存的配置类*

  ```java
  0 = "org.springframework.boot.autoconfigure.cache.GenericCacheConfiguration"
  1 = "org.springframework.boot.autoconfigure.cache.JCacheCacheConfiguration"
  2 = "org.springframework.boot.autoconfigure.cache.EhCacheCacheConfiguration"
  3 = "org.springframework.boot.autoconfigure.cache.HazelcastCacheConfiguration"
  4 = "org.springframework.boot.autoconfigure.cache.InfinispanCacheConfiguration"
  5 = "org.springframework.boot.autoconfigure.cache.CouchbaseCacheConfiguration"
  6 = "org.springframework.boot.autoconfigure.cache.RedisCacheConfiguration"
  7 = "org.springframework.boot.autoconfigure.cache.CaffeineCacheConfiguration"
  8 = "org.springframework.boot.autoconfigure.cache.SimpleCacheConfiguration"
  9 = "org.springframework.boot.autoconfigure.cache.NoOpCacheConfiguration"
  ```

+ 默认生效的缓存配置类

  *springboot 默认加载simpleCacheConfiguration配置类*

  ```java
  8 = "org.springframework.boot.autoconfigure.cache.SimpleCacheConfiguration"
  ```

+ 给容器中注册了一个CacheManager，ConcurrentMapCacheManager

+ 获取ConcurrentMapCache类型的缓存组件，按照CacheNames指定的名字获取

  + 运行流程

    1.  @Cacheable  方法执行之前，先去查询Cache(**缓存组件**) 用CacheNames指定的名字获取，(CacheManager先获取相应的缓存)，第一次获取缓存如果没有就会自动创建

    2. 去Cache去查找内容，key是方法的参数，key是按照某种策略生成的

       + 如果没有参数 

         `key = new SimpleKey()`

       + 如果有参数

         `key = 参数的值`

       + 如果有多个参数

         `key = new SimpleKey(params)`

    3. 没有查到缓存，就调用目标方法

    4. 将目标返回结果，放到Cache中



#### springboot操作默认缓存

+ 开启基于注解的缓存

  ``````java
  @SpringBootApplication
  @MapperScan("com.wang.dao")
  @EnableCaching //开启缓存
  public class Springbootdemo3Application {
      public static void main(String[] args) {
          SpringApplication.run(Springbootdemo3Application.class, args);
      }
  }
  ``````

+ 标注缓存注释

  + CaCheable

    + CacheNames    缓存的名称

    + key   缓存中数据的key，默认是方法中的参数

    + keyGenerator    key的生成器

    + cacheManager  指定缓存管理器

    + condition    判断条件 指定符合条件的情况下，才会缓存

    + unless   指定符合条件的情况下，不会被缓存

    + sync    是否使用异步模式

      ```java
       @Override
          @Cacheable(cacheNames = "user",key = "#root.methodName+'['+#id+']'")
          public User findById(Integer id) {
              return  userMapper.findById(id);
          }
      ```
      
  
    *自定义keyGenerator*
  
    ```java
      import org.springframework.cache.interceptor.KeyGenerator;
    import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
    import java.lang.reflect.Method;
      import java.util.Arrays;
    @Configuration
      public class MyCacheConfig {
          @Bean("keyGenerator")
          public KeyGenerator keyGenerator(){
              return new KeyGenerator(){
              @Override
              public Object generate(Object o, Method method, Object... objects) {
                  return method.getName()+"["+ Arrays.asList(objects).toString() +"]";
              }
          };
      }}
    ```
  
      *使用自定义key*
  
      ```java
       @Override
          @Cacheable(cacheNames = "user",keyGenerator = "keyGenerator")
          public User findById(Integer id) {
              return  userMapper.findById(id);
         }
      ```
  
      *自定义管理器*
  
      ```
      
      ```
  
      条件缓存
  
      *id>1才会进行缓存*
  
      ```java
       @Override
          @Cacheable(cacheNames = "user",condition = "#id>1")
          public User findById(Integer id) {
              return  userMapper.findById(id);
         }
      ```
  
      *id>1不会进行缓存*
  
      ``````java
       @Override
          @Cacheable(cacheNames = "user",unless = "#id>1")
          public User findById(Integer id) {
              return  userMapper.findById(id);
         }
      ``````
  
  + CachePut
  
    + 既调用方法，又更新缓存
  
      ```java
         @CachePut(value = "user",key = "#user.id") //key与查询方法key要对应
          public User UpdateUserById(User user) {
              userMapper.UpdateUserById(user);
              return user;
          }
      ```
  
      
  
  + CacheEvict
  
    + 清除单个缓存
  
      ```java
      @CacheEvict(value = "user",key = "#id")
          public void DeleteUserById(Integer id) {
              userMapper.DeleteUserById(id);
          }
      ```
  
    + 清除全部缓存
  
      ```java
      @CacheEvict(value = "user",allEntries = true)
          public void DeleteUserById(Integer id) {
              userMapper.DeleteUserById(id);
          }
      ```
  
      
  
    + 缓存的清除是否在方法执行前执行 默认beforeInvocation = false
  
      ```java
      //即使方法出错，缓存依然会被清除
      @CacheEvict(value = "user",allEntries = true,beforeInvocation = true)
          public void DeleteUserById(Integer id) {
              userMapper.DeleteUserById(id);
          }
      ```
  
      
  
  + Caching
  
    + 组合注解，一般用于复杂的缓存规则
  
      ```java
      //缓存可以key id中拿 也可以从 key name中拿   
      @Caching(
                  cacheable = {@Cacheable(value = "user",key = "#id")},
                  put = {@CachePut(value = "user",key = "#result.name")}
          )
           public User findById(Integer id) {
              return  userMapper.findById(id);
          }
      ```
  
  + CacheConfig
  
    + 公共配置
    
      ```java
      //配置在类上，其他的缓存注解都不用写CacheNames或者value
      @CacheConfig(cacheNames = "user")
      public class userService {}
      ```
    
    

+++

### Redis 缓存

#### 配置redis环境

+ pom依赖

  ```xml
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-data-redis</artifactId>
          </dependency>
  ```

+ properties配置

  ```properties
  spring.redis.database=1
  spring.redis.password=root
  spring.redis.host=49.234.18.34
  spring.redis.port=1996
  ```

#### redisTemplate序列化机制

+ `StringRedisTemplate`

  ```java
  StringRedisTemplate.opsForValue() //字符串
  StringRedisTemplate.opsForList() //列表
  StringRedisTemplate.opsForSet() //集合
  StringRedisTemplate.opsForHash() //散列
  StringRedisTemplate.opsForZset() //有序集合
  ```

+ `RedisTemplate`  同上

+ 序列化机制

  + 默认使用jdk序列化机制 `JdkSerializationRedisSerializer`

#### 自定义CacheManager

+ 自定义**基于代码**操作缓存`Jackson2JsonRedisSerializer`序列化机制的`RedisTemplate`

  ```java
  @Configuration
  public class MyRedisConfig {
      @Bean
      public RedisTemplate<Object, User> userRedisTemplate(RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {
          RedisTemplate<Object, User> template = new RedisTemplate();
          template.setConnectionFactory(redisConnectionFactory);
          Jackson2JsonRedisSerializer<User> jsonRedisSerializer = new Jackson2JsonRedisSerializer<User>(User.class);
          template.setDefaultSerializer(jsonRedisSerializer);
          return template;
      }
  }
  ```

  ```java
    @Autowired
      RedisTemplate<Object,User> userRedisTemplate;
  	...
      userRedisTemplate.opsForValue().set("user",user);
  ```

  

+ 自定义**基于注解**操控redis缓存的`Jackson2JsonRedisSerializer`序列化的`CacheManager`

  ```java
  @Configuration
  public class MyRedisConfig {
      @Bean
      public CacheManager cacheManager(RedisConnectionFactory factory){
          RedisCacheConfiguration cacheConfiguration = RedisCacheConfiguration.defaultCacheConfig()
          .entryTtl(Duration.ofDays(1))
          .disableCachingNullValues()
          .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(new               GenericJackson2JsonRedisSerializer()));
          return RedisCacheManager.builder(factory).cacheDefaults(cacheConfiguration).build();}
  }
  ```

  + 存入redis中的数据示例

  ```json
    {
    "@class": "com.wang.entity.User",
    "id": 1,
    "name": "wang"
    }
  ```
+++
### mybatis + redis

#### 开启`mybatis`二级缓存

  ```xml
  <cache type="com.wang.cache.RedisCache"/>
  ```

#### 自定义`mybatis-Cache`接口

  ```java
  public class RedisCache implements Cache { //实现mybatis里的Cache接口
  
      private String id;  //mapper中的nameplace
  
      //自定义的构造方法，传入mapper中的nameplace
      public RedisCache(String id){
          this.id = id;
      }
  
      @Override
      public String getId() {
          return id;
      }
  
      /**
       * 放入缓存数据，当一个请求，请求不到redis中缓存数据的时候，便从mysql中查询并且存入redis中，缓存模型是hash模型，又叫分区模型
       * @param key   key是 从mapper传过来的当前的请求的nameplace+sql语句
       * @param value  value是从数据库中查出来的结果
       */
      @Override
      public void putObject(Object key, Object value) {
          System.out.println("在redis中没有获取到数据，开始把数据加入缓存");
          RedisTemplate redisTemplate = (RedisTemplate) ApplicationContextUtils.getBean("redisTemplate");
          redisTemplate.setKeySerializer(new StringRedisSerializer());//字符串序列化Mapper中的key
          redisTemplate.setHashKeySerializer(new StringRedisSerializer());//字符串序列化Mapper中value中的key
          redisTemplate.opsForHash().put(id.toString(),key.toString(),value);//存入缓存
      }
  
      /**
       * 当redis中有数据时，从缓存中通过分区中 id (nameplace) 中的 key 获取 value
       * @param key  同上 key
       * @return
       */
      @Override
      public Object getObject(Object key) {
          System.out.println("从redis中获取到了的value");
          RedisTemplate redisTemplate = (RedisTemplate) ApplicationContextUtils.getBean("redisTemplate");
          redisTemplate.setHashKeySerializer(new StringRedisSerializer());
          return redisTemplate.opsForHash().get(id.toString(),key.toString());
      }
      //删除缓存中数据--未实现
      @Override
      public Object removeObject(Object o) {
          System.out.println("删除缓存数据未实现");
          return null;
      }
  
      /**
       * 当某个请求有增删改的时候，redis会根据分区中 id 对缓存进行清空
       */
      @Override
      public void clear() {
          RedisTemplate redisTemplate = (RedisTemplate) ApplicationContextUtils.getBean("redisTemplate");
          redisTemplate.setKeySerializer(new StringRedisSerializer());
          redisTemplate.delete(id.toString());
          System.out.println("清空缓存"+id.toString());
      }
      //缓存命中率
      @Override
      public int getSize() {
          RedisTemplate redisTemplate = (RedisTemplate) ApplicationContextUtils.getBean("redisTemplate");
          redisTemplate.setKeySerializer(new StringRedisSerializer());
          return redisTemplate.opsForHash().size(id.toString()).intValue();
      }
      //读写锁 读写不互斥 写写互斥 读读不互斥
      @Override
      public ReadWriteLock getReadWriteLock() {
          return null;
      }
  }
  
  ```

  

#### 工具类类获取`javaBean`

  ```java
  @Component
  public class ApplicationContextUtils implements ApplicationContextAware {
      private static ApplicationContext context;
      @Override
      //拿到工厂对象
      public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
          this.context=applicationContext;
      }
      //根据id获取bean
      public static Object getBean(String id){
          return context.getBean(id);
      }
      //根据类型获取bean
      public static Object getBean(Class clazz){
          return context.getBean(clazz);
      }
      //根据id和类型获取bean
      public static Object getBean(String id,Class clazz){
          return context.getBean(id,clazz);
      }
  }
  ```

  