# shiro
---

# javaSE
1. 读取配置文件
```
        Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");
        SecurityManager securityManager = factory.getInstance();
        SecurityUtils.setSecurityManager(securityManager);
```
2.  subject
```
//        获取当前用户 Subject对象
        Subject currentUser = SecurityUtils.getSubject();
//        通过当前用户拿到session(shiro的session)
        Session session = currentUser.getSession();
        session.setAttribute("someKey", "aValue");
//        判断当前用户是否被认证
        currentUser.isAuthenticated()
//        设置令牌
        UsernamePasswordToken token = new UsernamePasswordToken("lonestarr", "vespa");
//        登陆操作
        token.login()
//        判断用户是否为该角色
        currentUser.hasRole("schwartz")
//        判断权限
        currentUser.isPermitted("")
```

# spring boot
---
1. ## 	创建 自定义 Realm 对象 `extends AuthorizingRealm`
    > 用于认证和授权
2. ## DefaultWebSecurityManager
    >安全管理器
    >关联自定义 realm 对象 
    `securityManager.setRealm(userRealm);`
3. ## ShiroFilterFactoryBean
    ```
    //        设置安全管理器
            bean.setSecurityManager(defaultWebSecurityManager);
            /*
                添加 shiro 内置过滤器
                anon: 无需认证
                authc: 必须认证才能访问
                user: 必须拥有记住我才能访问
                perms: 拥有对某个资源的权限才能访问
                role: 拥有某个角色权限才能访问
             */
            Map<String, String> filterMap = new LinkedHashMap<>();
    ////        拦截
    //        filterMap.put("/user/**", "authc");
    //        授权 没有授权页面会跳转到未授权的页面
            filterMap.put("/user/add", "perms[user:add]");
            filterMap.put("/user/update", "perms[user:update]");
            filterMap.put("/user/*", "authc");
            bean.setFilterChainDefinitionMap(filterMap);
    //        设置登陆页面
            bean.setLoginUrl("/toLogin");
    //        设置未授权的页面
            bean.setUnauthorizedUrl("/noauth");
        ```
- realm 用于认证和 授权 
    >new UsernamePasswordToken().login()登陆操作
    >>登陆后 回到 自定义 Realm doGetAuthenticationInfo()

    >doGetAuthorizationInfo()授权方法
    >返回值为 new SimpleAuthorizationInfo();
    >info.addStringPermission()添加权限 该方法可以拿到 doGetAuthenticationInfo 返回对象中的 principal 可以是认证环节中获取的user对象
- ShiroFilterFactoryBean 用于配置信息