# Spring Security安全管理

> Java开发常见的安全框架有`Spring Security` 和 `shiro` ,`shiro`是一个轻量级的安全管理框架，`SpringSecurity`是一个相对复杂的安全管理框架，功能比`shiro`更强大，权限控制细颗粒度更高。对`OAuth2`更加友好

### 基于内存的认证

#### 导入依赖

```xml
         <!--spring-security安全框架-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
```

​                                        **只要项目添加了此依赖，项目中所有的资源都会被保护起来**

+ 配置文件里自定义账号密码

  ```yaml
  security:
      user:
        name: wang
        password: 123
  ```

#### 内存认证

+ 基于内存的认证-自定义类继承`webSecurityConfigurerAdapter`，进而实现对`SpringSecurity`更多的自定义配置

  ```java
  @Configurtion
  public class MyWebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Bean
      PasswordEncoder passwordEncoder(){
          //不对密码进行MD5加密处理
          Return NoOPpasswordEncoder.getInstance();
      }
      @Override
      protected void configure(AuthenticationManagerBuilder auth) throws Exception{
          auth.inMemoryAuthentication()
              .withUser("wang").password("123").roles("ADMIN","USER")
              //在内存中定义了一个用户名为wang密码为123角色为 ADMIN 和 USER 的用户
      }
  }
  ```

  > ​      上面只是实现了认证功能，但是对资源进行了全部的拦截，一般情况下，我们都需要要根据实际对部分资源来进行拦截，这是我们就需要对`WebSecurityConfigurerAdapter`进行重写。

#### 重写方法

+ 重写`WebSecurityConfigurerAdapte`中的`configure()`方法

```java
 @Override
    protected void configure(HttpSecurity httpSecurity) throws Exception{
    httpSecurity.authorizeRequests()
     /**
     *    以下代码定义了某一个URL只能有某一个权限的用户进行访问
     */
                .antMatchers("/admin/**")
        	    .hasRole("ADMIN")
        	    .antMatchers("/user/**")
        	    .assess("hasAnyRole('ADMIN','USER')")
        	    .anyRequest()
        	    .anthenticated()  //后面两行为除了定义过的url，访问其他必须认证以后访问
     
    /**
     *   以下代码定义了替换SpringSecurity的默认登陆页面，而且登陆页面表单里的字段name必须为username和password
     */
                .and()
                .formLogin()
                .loginPage("/User/login_page")
                .loginProcessingUrl("/login")     //方便AJAX或者移动端调用登录接口
                .usernameParameter("username")
                .passwordParameter("password")
               /**
                *以下代码为登陆成功以后需要处理的业务逻辑
                */
                .successHandler(new AuthenticationSuccessHandler() {
                    @Override
                    public void onAuthenticationSuccess(HttpServletRequest httpServletRequest,
                                                        HttpServletResponse httpServletResponse,
                                                        Authentication authentication) throws IOException, ServletException {
                        httpServletResponse.sendRedirect("index.html");//重定向到主页
                        Object principal = authentication.getPrincipal();
                        httpServletResponse.setContentType("application/json;charset=utf-8");
                        PrintWriter out = httpServletResponse.getWriter();
                        httpServletResponse.setStatus(200);
                        Map<String,Object> map = new HashMap<>();
                        map.put("status",200);
                        map.put("msg",principal);
                        ObjectMapper om = new ObjectMapper();
                        out.write(om.writeValueAsString(map));
                        out.flush();
                        out.close();
                    }
                })
         /**
          *     以上代码为登录失败以后返回的信息(Json格式)
          */
                .failureHandler(new AuthenticationFailureHandler() {
                    @Override
                    public void onAuthenticationFailure(HttpServletRequest httpServletRequest,
                                                        HttpServletResponse httpServletResponse,
                                                        AuthenticationException e) throws IOException, ServletException {
                        httpServletResponse.setContentType("application/json;charset=utf-8");
                        PrintWriter out = httpServletResponse.getWriter();
                        httpServletResponse.setStatus(401);
                        Map<String,Object> map = new HashMap<>();
                        map.put("status",401);
                        if(e instanceof LockedException){
                            map.put("msg","账户被锁定，请重新登录呐");
                        }else if (e instanceof BadCredentialsException){
                            map.put("msg","账户或密码错误，请重新登录呐");
                        }else if (e instanceof DisabledException){
                            map.put("msg","账户被禁用，登录失败呐");
                        }else if (e instanceof AccountExpiredException){
                            map.put("msg","账户已过期，登录失败呐");
                        }else if (e instanceof CredentialsExpiredException){
                            map.put("msg","密码已过期，登录失败呐");
                        }else{
                            map.put("msg","登录失败呐");
                        }
                        ObjectMapper om = new ObjectMapper();
                        out.write(om.writeValueAsString(map));
                        out.flush();
                        out.close();
                    }
                })
                .permitAll()//表示和登录相关的接口都不需要认证即可访问
                .and()
        /**
         *  注销接口，以及注销以后的业务处理
         */
                .logout()
                .logoutUrl("/logout")
                .logoutSuccessUrl("/public/login.html") //注销成功访问
                .clearAuthentication(true)     //注销以后清除用户信息
                .invalidateHttpSession(true)  //注销以后删除session
                .addLogoutHandler(new LogoutHandler() {
                    @Override
                    public void logout(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Authentication authentication) {
                    }
                })
                .logoutSuccessHandler(new LogoutSuccessHandler() {  //注销成功处理业务逻辑
                    @Override
                    public void onLogoutSuccess(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Authentication authentication) throws IOException, ServletException {
                        //重定向到一个页面
                        httpServletResponse.sendRedirect("/school/public/login.html");
                
                    }
                })
                .and()
                .headers().frameOptions().disable()//放行iframe 解决 X-Frame-Options 设为“DENY”，不允许载入任何框架
                .and()
                .csrf().disable(); //关闭csrf
    }

```

#### 密码加密

```java
    /**
     * 输入密码进行MD5加密
     * @return
     */
    @Bean
    PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder(10);  //默认为10，取值在4-31之间，越大越安全
    }
     /**
     * 给数据库密码加密
     * @return
     */
	  BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();
      String encodePassword = encoder.encode(user.getPassword());
	  user.setPassword(encodePassword);
```

#### 方法安全

```java
      /**
     * 基于注解的方法安全
     * @return
     */
	public Class userService(){
        //该方法需要ROLE_ADMIN权限
        @Secured("ROLE_ADMIN")
        public String admin(){
            return "hello";
        }
        //该方法需要同时有ADMIN和USER两种权限
        @PreAuthorize("hasRole('ADMIN') and hasRole('USER')")
        public String adminAndUser(){
            return "hello";
        }
        //该方法需要有ADMIN,DBA,USER任意一种即可
        @PreAuthorize("hasAnyRole('ADMIN','DBA','USER')")
        public String admin(){
            return "hello";
        }
    }
```

### 基于数据库的动态认证

#### 建表

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-13_210616.png)

#### 编写实体类

```java
public class User implements UserDetails{
    private String id;
    private String username;
    private String password;
    private Boolean enabled;
    private Boolean locked;
    private List<Role> roles;
    //UserDetails方法的实现
    
    //账户未过期
    @Override
    public boolean isAccountNonExpired() {
        return true;
    }
    //账户未锁定
    @Override
    public boolean isAccountNonLocked() {
        return !locked;
    }
	//凭证未过期
    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }
	//已启用
    @Override
    public boolean isEnabled() {
        return enabled;
    }
	//遍历用户拥有的权限return
    @Override
    public Collection<? extends GrantedAuthority> getAuthorities(){
        List<SimpleGrantedAuthority> authorities = new ArrayList<>();
        for (Role role : roles){
            authorities.add(new SimpleGrantedAuthority(role.getName()));
        }
        System.out.println("entity_user_getAuthorities——————>"+authorities);
        return authorities;
    }

}

public class Role{
    private Integer id;
    private String name;
    private String nameZh;
      //省去get set 方法...
}
public class Menu {
    private Integer id;
    private String pattern;
    private List<Role> roles;
      //省去get set 方法...
}
```

#### 创建`UserService`

> 用户登录首先会进入这里,查找用户并为其装配属性，然后再由系统提供的`DaoAuthenticationProvider`对比密码

```java
@Service
public class UserSecurity implements UserDetailsService {
    @Autowired
    UserMapper userMapper;
    /**
     * 根据前端传入的用户名去数据库查找其权限并附上
     */
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        if (username == null){
            throw new UsernameNotFoundException("账户不存在");
        }
        User user = userMapper.loadUserByUsername(username); //查找用户的相关信息
        if ( user == null){
            /**
             *  这是我加的一个方法，实现两个表复用一个登录模块
             */
            User merchants = userMapper.loadMerchantsByUsername(username);
            merchants.setRoles(userMapper.getUserRolesByUid(merchants.getId()));
            return merchants;
        }else {
            user.setRoles(userMapper.getUserRolesByUid(user.getId()));//为当前用户装配权限
            return user;
        }
        //System.out.println("给用户装配从数据库获取的权限——————>"+user.getRoles());
    }
}
```

#### 创建`UserMapper和UserMapper.xml`

> 一个接口和一个mapper文件，为用户查找信息，供`UserService`使用

```java
@Component
public interface UserMapper {
    User loadUserByUsername(String username);
    User loadMerchantsByUsername(String username);
    List<Role> getUserRolesByUid(String id);
}
```
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.wang.dao.UserMapper">
    <select id="loadUserByUsername" resultType="com.wang.entity.User" parameterType="String">
        select * from student where username = #{username}
    </select>
    <select id="getUserRolesByUid" resultType="com.wang.entity.Role">
        select * from t_role r ,user_role ur where r.id = ur.rid and ur.uid=#{id}
    </select>
    <select id="loadMerchantsByUsername" resultType="com.wang.entity.User" parameterType="String">
        select * from merchants where username = #{username}
    </select>
</mapper>
```

#### 编写`WebSecurityConfig`

```java
@Configuration
@EnableGlobalMethodSecurity(prePostEnabled = true,securedEnabled = true)
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    UserSecurity userSecurity;
    @Autowired
    UserMapper userMapper;
    
    /**
     * 输入密码进行MD5加密
     * @return
     */
    @Bean
    PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }

    /**
     * 将CustomFilterInvocationSecurityMetadataSource()装配Bean
     * @return
     */
    @Bean
    CustomFilterInvocationSecurityMetadataSource cfisms(){
        return new CustomFilterInvocationSecurityMetadataSource();
    }

    /**
     * 将CustomAccessDecisionManager() 装配Bean
     * @return
     */
    @Bean
    CustomAccessDecisionManager cadm(){
        return new CustomAccessDecisionManager();
    }
    /**
     * 替换了.antMatchers("/admin/**").hasRole("ADMIN")这种权限拦截
     * @param auth
     * @throws Exception
     */
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception{
        auth.userDetailsService(userSecurity);
    }

    /**
     * 登录结果以及权限处理
     * @param httpSecurity
     * @throws Exception
     */
    @Override
    protected void configure(HttpSecurity httpSecurity) throws Exception{
        httpSecurity
                .authorizeRequests()
                .withObjectPostProcessor(new ObjectPostProcessor<FilterSecurityInterceptor>() {
                    /**
                     * 将装配好的 cfisms() 和 cadm() 自定义的方法放到securityConfig里
                     * @param o
                     * @param <O>
                     * @return
                     */
                    @Override
                    public <O extends FilterSecurityInterceptor> O postProcess(O o) {
                        o.setSecurityMetadataSource(cfisms());
                        o.setAccessDecisionManager(cadm());
                        return o;
                    }
                })
                .and()
}
```

#### 自定义过滤器调用安全性元数据源`CustomFilterInvocationSecurityMetadataSource`

```java
/**
 * 自定义筛选器调用安全元数据
 */
public class CustomFilterInvocationSecurityMetadataSource implements FilterInvocationSecurityMetadataSource {
    AntPathMatcher antPathMatcher = new AntPathMatcher();
    @Autowired
    MenuMapper menuMapper;

    /**
     * 参数为一个FilterInvocation,可以从中提取出当前请求的url
     * 返回值为 Collection<ConfigAttribute> 表示当前请求当前url所需的角色
     * @param object
     * @return
     * @throws IllegalArgumentException
     */
    @Override
    public Collection<ConfigAttribute> getAttributes(Object object) throws IllegalArgumentException {
        /**
         * 当前请求的url
         */
        String requestUrl = ((FilterInvocation) object).getRequestUrl();
        /**
         * 查询所有的资源信息，menu以及menu相应的role
         */
        List<Menu> allMenus = menuMapper.getAllMenus();
        /**
         * 遍历资源信息，对比当前的请求和资源表，如果不存在则返回ROLE_ANONYMOUS
         */
        for (Menu menu : allMenus){
            if (antPathMatcher.match(menu.getPattern(),requestUrl)){   //ant风格的URL对比，对比成功则遍                                                                          历出访问该url需要的角色 
                List<Role> roles = menu.getRoles();
                String[] roleArr = new String[roles.size()];
                for (int i = 0; i<roleArr.length; i++ ){
                    roleArr[i] = roles.get(i).getName();
                }
                return SecurityConfig.createList(roleArr);//当前url所需的角色
            }
        }
        return SecurityConfig.createList("ROLE_ANONYMOUS");//假设一个登陆后可访问的路径？？？
    }

    /**
     * 用来返回所有定义好的权限资源，如果不需要校正返回null即可
     * @return
     */
    @Override
    public Collection<ConfigAttribute> getAllConfigAttributes() {
        return null;
    }

    /**
     * 该方法返回类对象是否需要校验
     * @param clazz
     * @return
     */
    @Override
    public boolean supports(Class<?> clazz) {
        return FilterInvocation.class.isAssignableFrom(clazz);
    }
}
```

#### 定制访问决策管理器`CustomAccessDecisionManager`

```java
public class CustomAccessDecisionManager implements AccessDecisionManager {
    /**
     * 判断当前登录的用户是否具备当前请求URL所需要的角色信息，如果不具备就抛出异常
     * @param authentication   包含当前登录用户的信息
     * @param o                是一个FilterInvocation对象，可以获取当前请求对象
     * @param collection       为FilterInvocationSecuritymetadatasource中的getAttribus方法的返回                                      值 即当前请求所需要的角色
     * @throws AccessDeniedException
     * @throws InsufficientAuthenticationException
     */
    
	//重写decide方法
    @Override
    public void decide(Authentication authentication, Object o, Collection<ConfigAttribute> collection) throws AccessDeniedException, InsufficientAuthenticationException {
        /**
         * 对信息进行比对
         */
        
        //我的角色信息为 auths
        Collection<? extends GrantedAuthority> auths =authentication.getAuthorities();
        //遍历信息：如果当前访问的url所需要的角色都对不不上
        for (ConfigAttribute configAttribute : collection){
            //如果configAttribute表里是ROLE_ANONYMOUS，说明当前url登陆后能访问，并且用户是UsernamePasswordAuthenticationToken的示例【登录了】，则方法结束。
            if ("ROLE_ANONYMOUS".equals(configAttribute) && authentication instanceof UsernamePasswordAuthenticationToken) {
                return;
            }
            for (GrantedAuthority authority : auths){
                //如果当前用户的角色具备当前请求所需要的角色，那么方法结束
                if (configAttribute.getAttribute().equals(authority.getAuthority())){
                    return;
                }
            }
        }
        throw new AccessDeniedException("权限不足");
    }

    @Override
    public boolean supports(ConfigAttribute configAttribute) {
        return true;
    }

    @Override
    public boolean supports(Class<?> aClass) {
        return true;
    }
}

```

#### 创建`MenuMapper 和menuMapper.xml`

```java
@Mapper
@Component
public interface MenuMapper {
    List<Menu> getAllMenus();
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.wang.dao.MenuMapper">
    <resultMap id="BaseResultMap" type="com.wang.entity.Menu">
        <id property="id" column="id"/>
        <result property="pattern" column="pattern"/>
        <collection property="roles" ofType="com.wang.entity.Role">
            <id property="id" column="rid"/>
            <result property="name" column="rname"/>
            <result property="nameZh" column="rnameZh"/>
        </collection>
    </resultMap>

    <cache type="com.wang.cache.RedisCache"/>
<!--    m是路径表  r表示权限表  mr是路径与权限的关系表-->
    <select id="getAllMenus" resultMap="BaseResultMap">
        SELECT m.* ,r.id AS rid ,r.name AS rname , r.nameZh AS rnameZh FROM t_menu m left join menu_role mr
        ON m.id=mr.mid left join t_role r ON mr.rid = r.id
    </select>
</mapper>
```

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-14_000047.png)

#### 静态资源放行

```java
 /**
     * 静态资源的放行
     * @param web
     * @throws Exception
     */
    @Override
    public void configure(WebSecurity web) throws Exception {
        //解决静态资源被拦截的问题
        web.ignoring().antMatchers("/public/**");
        web.ignoring().antMatchers("/res/**");
        web.ignoring().antMatchers("/js/**");
        web.ignoring().antMatchers("/css/**");
        web.ignoring().antMatchers("/img/**");
        web.ignoring().antMatchers("/upload/**");
        web.ignoring().antMatchers("/admin/**");
    }
```

