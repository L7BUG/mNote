# `org.springframework.boot.autoconfigure.security.oauth2.client.OAuth2ClientProperties` 配置类

## 配置 信息

### 配置文件

```yaml
      client:
        registration:
          gitee:  # registrationId
            client-id: 246dc3e8acf8582256d0932e4e2bf2c5a5f64c0dba864d8183e0dec56a71a1ea
            client-secret: baeb04a9855ae4d2f77154d16d8996653c344ed1f80cee7f884e3ac3bf77d56f
            authorization-grant-type: authorization_code
            redirect-uri: '{baseUrl}/{action}/oauth2/code/{registrationId}'
            client-authentication-method: POST
            scope: user_info
        provider:
          # providerId
          gitee:
            authorization-uri: https://gitee.com/oauth/authorize
            token-uri: https://gitee.com/oauth/token
            user-info-uri: https://gitee.com/api/v5/user
            user-name-attribute: name
```

### 配置类

```java
/**
 * OAuth provider details. 服务提供者 key -> id
 */
private final Map<String, Provider> provider = new HashMap<>();

/**
 * OAuth client registrations. 客户端 key -> id
 */
private final Map<String, Registration> registration = new HashMap<>();
```

客户端信息

```java
public static class Registration {

		/**
		 * Reference to the OAuth 2.0 provider to use. May reference an element from the
		 * 'provider' property or used one of the commonly used providers (google, github,
		 * facebook, okta).
		 */
		private String provider;// 授权服务器的id 可不填 不填为key

		/**
		 * Client ID for the registration.
		 */
		private String clientId;// 授权服务器提供的客户端标识，需要向授权服务器申请。

		/**
		 * Client secret of the registration.
		 */
		private String clientSecret;// 授权服务器提供的客户端秘钥。

		/**
		 * Client authentication method. May be left blank when using a pre-defined
		 * provider.
		 */
		private String clientAuthenticationMethod;// 客户端认证方法

		/**
		 * Authorization grant type. May be left blank when using a pre-defined provider.
		 */
		private String authorizationGrantType;// 授权类型参考 OAuth2协议中的授权模式。 配置文件中是授权码类型

		/**
		 * Redirect URI. May be left blank when using a pre-defined provider.
		 */
		private String redirectUri;// 302认证重定向uri

		/**
		 * Authorization scopes. When left blank the provider's default scopes, if any,
		 * will be used.
		 */
		private Set<String> scope;// 授权范围

		/**
		 * Client name. May be left blank when using a pre-defined provider.
		 */
		private String clientName; // 客户端名称
}
```

授权服务器配置

```java
public static class Provider {

		/**
		 * Authorization URI for the provider.
		 */
		private String authorizationUri;// 客户端授权请求地址

		/**
		 * Token URI for the provider.
		 */
		private String tokenUri;// token地址

		/**
		 * User info URI for the provider.
		 */
		private String userInfoUri;// 用户信息地址

		/**
		 * User info authentication method for the provider.
		 */
		private String userInfoAuthenticationMethod;// 请求方法

		/**
		 * Name of the attribute that will be used to extract the username from the call
		 * to 'userInfoUri'.
		 */
		private String userNameAttribute;// 用户名key

		/**
		 * JWK set URI for the provider.
		 */
		private String jwkSetUri;// 是jwkSet的请求端点，获取授权服务器提供的公钥信息。

		/**
		 * URI that can either be an OpenID Connect discovery endpoint or an OAuth 2.0
		 * Authorization Server Metadata endpoint defined by RFC 8414.
		 */
		private String issuerUri;// 是授权服务器提供的元信息端点服务，如果授权服务器提供了该端点前面的Provider配置项不需要配置，都可以从该端点读取。
	}
```
