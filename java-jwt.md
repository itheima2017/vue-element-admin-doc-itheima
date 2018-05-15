# JWT 令牌

JWT是为了在网络应用环境间传递声明而执行的一种基于JSON的开放标准（[(RFC 7519](https://tools.ietf.org/html/rfc7519)).该token被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源，也可以增加一些额外的其它业务逻辑所必须的声明信息，该token也可直接被用于认证，也可被加密。

##### JWT的构成

- Header

  通常由两部分组成：token的类型，即JWT和正在使用的散列算法，如HMAC SHA256或RSA。

  ```json
  {
    "alg": "HS256",
    "typ": "JWT"
  }
  ```

  然后，这个JSON被Base64Url编码，形成JWT的第一部分。

- Payload

  令牌的第二部分是包含声明的有效负载。 声明是关于实体（通常是用户）和其他元数据的声明。 有三种类型的声明：注册，公共声明和私有声明。

  - 注册

    这些是一组预先定义的声明，它们不是强制性的，但推荐使用，以提供一组有用的，可互操作的声明。 其中一些是：iss（发行者），exp（到期时间），sub（主题），aud（受众）等。

  - 公共声明

    这些可以由使用JWT的人员随意定义。 但为避免冲突，应在IANA JSON Web令牌注册表中定义它们，或将其定义为包含防冲突命名空间的URI。该部分信息可以在客户端解密，因此不建议添加敏感信息。

  - 私有声明

    由提供者和消费者共同定义，因为这部分采用的是对称加密，也就意味着这部分信息是明文信息，因此不建议存放敏感信息。

    ```json
    //Payload示例
    {
      "sub": "1234567890",
      "name": "John Doe",
      "admin": true
    }
    ```

- Signature

  要创建签名部分，必须采用编码头，编码有效载荷，秘钥，header指定的算法并签名。

  例如，如果你想使用HMAC SHA256算法，签名将按照以下方式创建：

  ```
  HMACSHA256(
    base64UrlEncode(header) + "." +
    base64UrlEncode(payload),
    secret)
  ```

  将这三部分，连接成一个完整的字符串，构成一个最终的JWT:

  ```
  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
  ```

  秘钥是保存在服务器的，因此JWT的签发也是在服务器上完成的。在任何时候，都不要将秘钥泄露出去，否则你的验证机制将没有任何意义。

##### 如何应用

```java
//token签发
String username = String.valueOf(authentication.getPrincipal());
String token = Jwts.builder()
      .setSubject(username)
      .setExpiration(new Date(System.currentTimeMillis() + 24 * 60 * 60 * 1000))
      .signWith(SignatureAlgorithm.HS256, JWTConstants.SECRET)
      .compact();

//token验证
String token = request.getHeader(JWTConstants.AUTHORIZATION_HEADER);
        if (token != null) {
            String user = Jwts.parser()
                    .setSigningKey(JWTConstants.SECRET)
                    .parseClaimsJws(token.replace(JWTConstants.AUTHORIZATION_PRE, ""))
                    .getBody()
                    .getSubject();
            if (user != null) {
                UserDetails userDetails = userDetailsService.loadUserByUsername(user);
                return new UsernamePasswordAuthenticationToken(userDetails.getUsername(), null, userDetails.getAuthorities());
            }
        }
```

上述代码，即JWT在Java中应用的方式之一。从代码中我们可以看出，当前签发的token使用HS256加密，在token中存放了username，用于验证时，通过username从上下文中获取当前用户的相关信息，从而完成token的校验操作。

##### 总结

因为json的通用，所以JWT可以进行跨语言支持。在payload中可以保存一些信息，因此可用于存放也一些业务相关的必要的非敏感信息。由于它不需要在后端保存会话信息，因此它易于扩展。但是在使用过程中，需要注意保护好秘钥信息，避免泄露。同时由于payload在客户端是可以解密的，因此请不要在payload中存放敏感信息，避免重要信息泄露。