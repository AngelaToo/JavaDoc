##### SpringBoot整合shiro

1. **Authentication  认证 ---用户登录**
2. **Authorization 授权 --- 用户具有哪些权限**
3. Cryptography 安全数据加密
4. Session Management 会话管理
5. Web Integration Web 系统集成
6. Interations 集成其他应用，spring、缓存框架

##### 核心API

subject:用户主体（操作交给SecurityManager）

securityManager:安全管理器（关联Realm)

realm:shiro连接数据的桥梁



- pom 导入shiro 依赖

  ```
  <dependency>
      <groupId>org.apache.shiro</groupId>
      <artifactId>shiro-spring</artifactId>
      <version>1.3.2</version>
  </dependency>
  ```

- 自定义realm类

  ```java
  public class UserRealm extends AuthorizingRealm {
  
      /**
       *  执行授权逻辑
       * @param principalCollection
       * @return
       */
      @Override
      protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
          return null;
      }
  
      /**
       *  执行认证逻辑
       * @param authenticationToken
       * @return
       * @throws AuthenticationException
       */
      @Override
      protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
          return null;
      }
  }
  ```

- 编写shiro配置类

  ```java
  @Configuration
  public class ShiroConfig {
  
  
     /**
       *  创建ShiroFilterFactoryBean
       */
      @Bean
      public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("securityManager") DefaultWebSecurityManager securityManager){
          ShiroFilterFactoryBean shiroFilterFactoryBean = new ShiroFilterFactoryBean();
  
          //设置安全管理器
          shiroFilterFactoryBean.setSecurityManager(securityManager);
  
          //添加内置过滤器
          /**
           *  Shiro内置过滤器，实现权限相关的拦截器
           *      常用过滤器
           *      anon:无需认证（登录）可以访问
           *      authc:必须认证才可以访问
           *      user：如果使用rememberMe的功能可以直接访问
           *      perms:该资源必须授权才可以访问
           *      role：该资源必须得到角色权限才可以访问
           */
          Map<String, String> filterMap = new LinkedHashMap<>();
  //        filterMap.put("/add","authc");
  //        filterMap.put("/update","authc");
  
          filterMap.put("/test","anon");
          filterMap.put("/login","anon");
          filterMap.put("/*","authc");
  
          //授权过滤器
          //注意：当授权拦截后，shiro会自动跳转到未授权页面
          filterMap.put("/add","Perms[user:add]");
  
          //设置跳转登录页面
          shiroFilterFactoryBean.setLoginUrl("/toLogin");
  
          //设置未授权提示页面
          shiroFilterFactoryBean.setUnauthorizedUrl("/noAuth");
  
          shiroFilterFactoryBean.setFilterChainDefinitionMap(filterMap);
  
          return shiroFilterFactoryBean;
      }
  
      /**
       *  创建DefaultWebSecurityManager
       */
      @Bean(name="securityManager")
      public DefaultWebSecurityManager getDefaultWebSecurityManager(@Qualifier("userRealm")UserRealm userRealm){
          DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
         // 关联realm
          securityManager.setRealm(userRealm);
          return securityManager;
      }
  
      /**
       *  创建Realm
       */
      @Bean(name="userRealm")
      public UserRealm getRealm(){
          return new UserRealm();
      }
  }
  ```

- 使用shiro内置过滤器进行拦截

- 

##### 登录功能