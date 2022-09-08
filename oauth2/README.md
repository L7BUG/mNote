### OIDC

**OIDC**是**OAuth2**的一个内建协议，是对**OAuth2**的一个补充，它支持对资源拥有者的认证。

#### OIDC的关键术语

**OIDC**规定了一些术语用来提高我们学习的门槛:

1. `EU`：**End User** 终端用户
2. `RP`：**Relying Party** 即客户端（**client**），授权和认证的最终消费方，我搞不懂为啥要玩多余的概念
3. `OP`：**OpenID Provider**，对**EU**进行认证的服务提供者
4. `ID Token`：**JWT**格式，**EU**的认证通过后生成凭证，供**RP**消费
5. `UserInfo Endpoint`： 通过凭据查询用户基本信息的接口，建议上**HTTPS**。
