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