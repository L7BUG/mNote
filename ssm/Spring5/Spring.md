> # Spring
---
1. # IOC
    * alias 标签可以设置别名
    * `name` 属性可以设置多个别名
    * `import` 标签可以导入多个配置文件(冲突的话后面会覆盖前面的)
    * bean 作用域
        1. 单例&多例
    * ## 自动装配
        1. xml `bean` 标签中有一个 autowire 属性
            1. byName
            2. byType
2. # ioc(注解)
    1. ## @Autowired
        > `required` 默认为 true 如果设置为 false 说明这个对象可以null, 并且不抛出异常
        > `@Qualifier("???")` 配合Autowired 根据id找
    3. ## @Nullable 说明这个字段可以未空
    2. ## 使用注解开发
        > 使用注解开发 需要 aop
        
        * Component
        * Repository
        * Service
        * Controller
        
        > 作用域
        - Scope

    3. ## 使用Java 配置spring
        > 完全不使用xml spring配置

3. # AOP
    1. ## 动态代理
        > JDK 动态代理
        - `Proxy` 代理类
        - `InvocationHandler`  处理代理结果
    2. Spring AOP
        > **动态代理生成的 bean 必须是接口 否则会报错**
        1. 使用 Spring 的API接口
            1. 实现 `org.springframework.aop.*Advice` 各接口
            2. >`<aop:config>`
                >> `<aop:pointcut>` 切入点
                >> `<aop:advisor advice-ref="实现接口" pointcut-ref="切面"/>`
        2. 自定义类实现AOP
            1. 自定义类
            2. >`<aop:config>`
                >> `<aop:aspect ref="自定义类">` 定义切面
                >>>  `<aop:pointcut />` 切入点
                >>> `<aop:`通知类型` method `类中的方法`  pointcut `切入点`/>` 通知...
        3. 使用注解实现
            > `<aop:aspectj-autoproxy/>` 需要导入支持
            1. 在自定义类上加上`Aspect` 表示 这是一个切面
            2. 定义切入点方法
            3. 定义通知方法
                > 方法
                
                >环绕通知 `@Around` `ProceedingJoinPoint 连接点参数`   **需要返回值**
                >进入环绕通知
                >> 调用 `joinPoint.proceed()` 方法 
                >> 前置通知 `@Before`
                >> 出现异常回到异常通知(如果有的话) `@AfterThrowing`
                >> 后置通知 `@AfterReturning`
                >>最终通知 `@After`

                >环绕结束
4. # [MyBatis-Spring](http://mybatis.org/spring/zh/index.html)
    1. > `DriverManagerDataSource`
        > > `SqlSessionFactoryBean`
        > >> `SqlSessionTemplate`
        > >>> `MyMapper`
5. # 事务
    > ACID 原则
    * 原子性
    * 一致性
    * 隔离性
        * 多个业务操作同一个资源， 防止数据损坏
    * 持久性
        * 事务一旦提交， 无论系统发生什么问题， 结果都不会再被影响， 被持久化的写到存储器中

    * # 声明式事务
        > 和AOP 差不多 需要配置一个 事务管理器 `DataSourceTransactionManager`
        1. >`<tx:advice>` //配置事务通知
        2. >> `<tx:attributes>` //配置事务传播特性
        3. >>> `<tx:method name>`...
        
        然后配置AOP
        >`<aop:config>`
        >> 切入点 和 aop:advisor 引用上方的事务通知