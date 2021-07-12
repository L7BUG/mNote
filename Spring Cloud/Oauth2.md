# Spring Oauth2

> 结合Oauth2可以实现单点登录、令牌中继、令牌交换等功能

## OAuth2 相关名词解释

- Resource owner（资源拥有者）：拥有该资源的最终用户，他有访问资源的账号密码；
- Resource server（资源服务器）：拥有受保护资源的服务器，如果请求包含正确的访问令牌，可以访问资源；
- Client（客户端）：访问资源的客户端，会使用访问令牌去获取资源服务器的资源，可以是浏览器、移动设备或者服务器；
- Authorization server（认证服务器）：用于认证用户的服务器，如果客户端认证通过，发放访问资源服务器的令牌。

## [四种授权模式](http://www.macrozheng.com/#/cloud/oauth2?id=四种授权模式)

- Authorization Code（授权码模式）：正宗的OAuth2的授权模式，客户端先将用户导向认证服务器，登录后获取授权码，然后进行授权，最后根据授权码获取访问令牌；
- Implicit（简化模式）：和授权码模式相比，取消了获取授权码的过程，直接获取访问令牌；
- Resource Owner Password Credentials（密码模式）：客户端直接向用户获取用户名和密码，之后向认证服务器获取访问令牌；
- Client Credentials（客户端模式）：客户端直接通过客户端认证（比如client_id和client_secret）从认证服务器获取访问令牌。

> 说明： 以上来源于 mall项目文档

