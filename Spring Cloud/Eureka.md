# Eureka

> 服务注册与发现 类似ZooKeeper

## 三大角色

- Eureka Server 提供服务注册与发现 就像ZooKeeper 的客户端
- Service Provide 将自身服务注册到Eureka 
- Service Consumer 服务消费方从Eureka中获取注册服务列表，从而找到消费服务