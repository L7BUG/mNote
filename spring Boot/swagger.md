# [swagger](https://swagger.io/)
---
- # 依赖
    -  springfox-swagger2
    -  springfox-swagger-ui
    - spring fox
    ```
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
    ```
1. # 配置docket
    ```
                return new Docket(DocumentationType.OAS_30)
                    .apiInfo(apiInfo())
                    .select()
    //                扫描什么路径
                    .apis(RequestHandlerSelectors.basePackage("com.l.controller"))
    //                过滤什么路径
                    .paths(PathSelectors.ant("/l/**"))
                    .build();
    ```