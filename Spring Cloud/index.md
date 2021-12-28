# 微服务架构的4个主要问题

1. 服务很多，客户端怎么访问？
2. 这么多服务，服务间如何通讯?
3. 这么多服务，如何治理?
4. 服务挂了这么办?

---

相关技术：

1. **网关** :kong,soul；
2. **分布式调用链**： SkyWalking、Zipkin
3. **日志系统：** Kibana
4. ......

Spring Cloud 相关：

1. [Eureka](./Eureka.md)：服务注册与发现；
2. Ribbon：负载均衡；
3. Hytrix ：熔断；
4. Zuul ：网关；
5. Spring Cloud Config：配置中心；

Spring Cloud Alibaba也是很值得学习的：

1. **[Sentinel](https://github.com/alibaba/Sentinel "Sentinel")** ：A lightweight powerful flow control component enabling reliability and monitoring for microservices. (轻量级的流量控制、熔断降级 Java 库)。
2. **[dubbo](https://github.com/apache/dubbo "dubbo")** ：Apache Dubbo 是一个基于 Java 的高性能开源 RPC 框架。
3. **[nacos](https://github.com/alibaba/nacos "nacos")** ：Nacos 致力于帮助您发现、配置和管理微服务。Nacos 提供了一组简单易用的特性集，帮助您快速实现动态服务发现、服务配置、服务元数据及流量管理。Nacos 可以作为 Dubbo 的注册中心来使用。
4. **[seata](https://github.com/seata/seata "seata")** : Seata 是一种易于使用，高性能，基于 Java 的开源分布式事务解决方案。
5. **[RocketMQ](https://github.com/apache/rocketmq "RocketMQ")** ：阿里巴巴开源的一款高性能、高吞吐量的分布式消息中间件。