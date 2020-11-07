# Spring MVC
---
 
 - # RestFul 风格  
     ```
        @RequestMapping("/add/{a}/{b}")
        public String test(@PathVariable int a, @PathVariable String b, Model model)
        // URL: localhost/add/1/231ads
        
     ```
- # `return String`
    - `Redirect` 重定向
    - `forward` 转发
    - `字符串` 视图解析器
- # JSON
    - jackson
        ```
            <dependency>
                <groupId>com.fasterxml.jackson.core</groupId>
                <artifactId>jackson-databind</artifactId>
                <version>2.11.3</version>
            </dependency>
        ```
        通过ObjectMapper对象的writeValueAsString方法 将对象转换成JSON字符串
        > **乱码问题**
        ```
            <mvc:annotation-driven>
            <mvc:message-converters register-defaults="true">
                <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                    <constructor-arg value="UTF-8"/>
                </bean>
                <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                    <property name="objectMapper">
                        <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                            <property name="failOnEmptyBeans" value="false"/>
                        </bean>
                    </property>
                </bean>
            </mvc:message-converters>
        </mvc:annotation-driven>
        ```