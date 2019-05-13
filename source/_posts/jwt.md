---
title: jwt
date: 2019-04-09 10:06:15
tags:
---

# What is JSON Web Token?

JSON Web Token（JWT）是一个开放标准（[RFC 7519](https://tools.ietf.org/html/rfc7519)），它定义了一种简洁且独立的方式，用于在各方之间作为JSON对象安全地传输信息。此信息可以通过数字签名进行验证和信任。JWT可以使用安全算法（使用HMAC算法）或使用RSA或ECDSA的公钥/私钥对进行签名。

虽然JWT可以加密以在各方之间提供保密，但我们将专注于签名令牌。签名令牌可以验证其中包含的声明的完整性，而加密令牌则隐藏其他方的声明。当使用公钥/私钥对签名令牌时，签名还证明只有持有私钥的一方是签署它的一方。

**JWT特点**

+ 简洁(Compact): 可以通过URL，POST参数或者在HTTP header发送，因为数据量小，传输速度也很快
+ 自包含(Self-contained)：负载中包含了所有用户所需要的信息，避免了多次查询数据库


# When should you use JSON Web Tokens?

以下是JSON Web令牌有用的一些场景：

+ 授权(Authorization)：这是使用JWT的最常见方案。一旦用户登录，每个后续请求都将包括JWT，允许用户访问该令牌允许的路由，服务和资源。Single Sign On(单点登录)是一种现在广泛使用JWT的功能，因为它的开销很小，并且能够在不同的域中轻松使用。
+ 信息交换(Infomation Exchange)：JSON Web令牌是在各方之间安全传输信息的好方法。因为JWT可以签名 - 例如，使用公钥/私钥对 - 您可以确定发件人是他们所说的人。此外，由于使用标头和有效负载计算签名，您还可以验证内容是否未被篡改。

# What is the JSON Web Token structure?

在简洁的形式中，JSON Web Tokens由英语句号（.）分隔的三个部分组成，它们是：

+ Header
+ Payload
+ Signature

因此，JWT通常如下所示。
```
xxxxx.yyyyy.zzzzz
```

让我们分解不同的部分。

## Head

标头(Head)通常由两部分组成：令牌的类型，即JWT，以及正在使用的签名算法，例如HMAC SHA256或RSA。

例如：
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
经过Base64编码后
```
ewogICJhbGciOiAiSFMyNTYiLAogICJ0eXAiOiAiSldUIgp9ICA=
```

## Payload

token(令牌)的第二部分是Payload，其中包含claims(声明)。Claims是关于实体（通常是用户）和其他数据的声明。Claims有三种类型：Registered，public和private claims。

+ Registered Claims: 这些是一组预定义声明，不是强制性的，但建议使用，以提供一组有用的，可互操作的声明。其中一些是： 
  + iss（issuer） - 该JWT的签发者
  + exp（expiration time） - 什么时候过期，这里是一个Unix时间戳
  + sub（subject） - 该JWT所面向的用户
  + aud（audience） - 接收该JWT的一方
  + iat(issued at) - 在什么时候签发的
  + ...

Notice that the claim names are only three characters long as JWT is meant to be compact

+ Public Claims: 这些可以由使用JWT的人随意定义。但为避免冲突，应在 [IANA JSON Web Token Registy](https://www.iana.org/assignments/jwt/jwt.xhtml) 中定义它们，或者将其定义为包含防冲突命名空间的URI。
+ Private Claims: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

An example payload could be:
```
{
    "iss": "Lefto.com",
    "iat": 1500218077,
    "exp": 1500218077,
    "aud": "www.leftso.com",
    "sub": "leftso@qq.com",
    "user_id": "dc2c4eefe2d141490b6ca612e252f92e",
    "user_token": "09f7f25cdb003699cee05759e7934fb2"
}
```

然后，Payload经过Base64编码，形成JSON Web token的第二部分。
```
ewogICAgImlzcyI6ICJMZWZ0by5jb20iLAogICAgImlhdCI6IDE1MDAyMTgwNzcsCiAgICAiZXhwIjogMTUwMDIxODA3NywKICAgICJhdWQiOiAid3d3LmxlZnRzby5jb20iLAogICAgInN1YiI6ICJsZWZ0c29AcXEuY29tIiwKICAgICJ1c2VyX2lkIjogImRjMmM0ZWVmZTJkMTQxNDkwYjZjYTYxMmUyNTJmOTJlIiwKICAgICJ1c2VyX3Rva2VuIjogIjA5ZjdmMjVjZGIwMDM2OTljZWUwNTc1OWU3OTM0ZmIyIgp9
```

请注意，对于 signed tokens(签名令牌) ，此信息虽然可以防止被篡改，但任何人都可以读取。除非加密，否则不要将秘密信息放在 JWT 的 Payload 或 Head 中。

## Signature

签名其实是对JWT的头部和负载整合的一个签名验证
首先需要将头部和负载通过.链接起来就像这样:header.Payload,上述的例子链接起来之后就是这样的:
```
ewogICJhbGciOiAiSFMyNTYiLAogICJ0eXAiOiAiSldUIgp9ICA=.ewogICAgImlzcyI6ICJMZWZ0by5jb20iLAogICAgImlhdCI6IDE1MDAyMTgwNzcsCiAgICAiZXhwIjogMTUwMDIxODA3NywKICAgICJhdWQiOiAid3d3LmxlZnRzby5jb20iLAogICAgInN1YiI6ICJsZWZ0c29AcXEuY29tIiwKICAgICJ1c2VyX2lkIjogImRjMmM0ZWVmZTJkMTQxNDkwYjZjYTYxMmUyNTJmOTJlIiwKICAgICJ1c2VyX3Rva2VuIjogIjA5ZjdmMjVjZGIwMDM2OTljZWUwNTc1OWU3OTM0ZmIyIgp9
```

例如，如果要使用HMAC SHA256算法，将按以下方式创建签名：
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

由于HMAC SHA256加密算法需要一个key,我们这里key暂时用leftso吧,加密后的内容：
```
686855c578362e762248f22e2cc1213dc7a6aff8ebda52247780eb6b5ae91877
```

其实加密的内容也就是JWT的签名,类似我们对某个文件进行MD5加密然后接收到文件进行md5对比一样.只是这里的HMAC SHA256算法需要一个key,当然这个key应该是使用者和接收者都知道的。

对上面的签名内容进行base64编码得到最终的签名
```
Njg2ODU1YzU3ODM2MmU3NjIyNDhmMjJlMmNjMTIxM2RjN2E2YWZmOGViZGE1MjI0Nzc4MGViNmI1YWU5MTg3Nw==
```

签名用于验证消息在此过程中未被更改，并且，在使用私钥签名的token的情况下，它还可以验证JWT的发行人是否是它所声称的人。

## Putting all together

输出是三个由点分隔的Base64-URL字符串，可以在HTML和HTTP环境中轻松传递，而与基于XML的标准（如SAML）相比更加简洁。

下面显示了一个JWT,它具有先前的 header 和 payload encoded, 并使用加密签名. 

![gcheap](/img/jwt/encoded-jwt3.png)

根据上面例子最终整合在一起的jwt:
```
ewogICJhbGciOiAiSFMyNTYiLAogICJ0eXAiOiAiSldUIgp9ICA=.ewogICAgImlzcyI6ICJMZWZ0by5jb20iLAogICAgImlhdCI6IDE1MDAyMTgwNzcsCiAgICAiZXhwIjogMTUwMDIxODA3NywKICAgICJhdWQiOiAid3d3LmxlZnRzby5jb20iLAogICAgInN1YiI6ICJsZWZ0c29AcXEuY29tIiwKICAgICJ1c2VyX2lkIjogImRjMmM0ZWVmZTJkMTQxNDkwYjZjYTYxMmUyNTJmOTJlIiwKICAgICJ1c2VyX3Rva2VuIjogIjA5ZjdmMjVjZGIwMDM2OTljZWUwNTc1OWU3OTM0ZmIyIgp9.
Njg2ODU1YzU3ODM2MmU3NjIyNDhmMjJlMmNjMTIxM2RjN2E2YWZmOGViZGE1MjI0Nzc4MGViNmI1YWU5MTg3Nw==
```

如果您想使用JWT并将这些概念付诸实践，您可以使用 [jwt.io Debugger](https://jwt.io/) 来解码，验证和生成JWT。

# How do JSON Web Tokens work?

在身份验证中，当用户使用其凭据成功登录时，将返回 JSON Web token 。由于 token 是 credentials(凭证) ，因此必须非常小心以防止出现安全问题。一般情况下，您不应该将 token 保留的时间超过要求。

当用户希望访问受保护的路由或资源时，用户代理应该发送JWT，通常在 Authorization header（授权头） 中使用 Bearer 模式。标题的内容应该如下:
```
Authorization: Bearer <token>
```

在某些情况下，这可能是一种无状态授权机制。服务器的受保护路由将在授权头中检查有效的JWT，如果它存在，则允许用户访问受保护的资源。如果JWT包含必要的数据，就可以减少对数据库查询某些操作的需求，尽管情况并非总是如此。

如果令牌是在授权头中发送的，那么跨源资源共享(Cross-Origin Resource Sharing, CORS)就不是问题，因为它不使用cookie。

下图显示了JWT是如何获得并用于访问api或资源的:

![gcheap](/img/jwt/client-credentials-grant.png)

1. 应用程序或客户端向授权服务器请求授权。这是通过不同的授权流之一执行的。例如，一个典型的符合[OpenID Connect](https://openid.net/connect/)的web应用程序将使用 [authorization code flow](https://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth) 通过/oauth/authorize端点。
2. 当 authorization(授权) 被 grant(授予) 时，授权服务器将向应用程序返回一个access token(访问令牌)。
3. 应用程序使用访问令牌访问受保护的资源(如API)。

请注意，对于已签名的令牌，令牌中包含的所有信息都公开给用户或其他方，即使他们无法更改这些信息。这意味着您不应该将机密信息放在令牌中。

# Why should we use JSON Web Tokens?

让我们讨论一下与 Simple Web Tokens(SWT)和 Security Assertion Markup Language Tokens(SAML)相比，JSON Web Tokens(JWT)的好处。

由于JSON比XML更简洁，当它被编码时，它的大小也更小，这使得JWT比SAML更简洁。这使得JWT成为在HTML和HTTP环境中传递消息的一个很好的选择。

在安全方面，SWT只能由使用HMAC算法的共享秘密对称签名。但是，JWT和SAML令牌可以使用X.509证书形式的公钥/私钥对进行签名。与JSON签名的简单性相比，使用XML数字签名签名而不引入模糊的安全漏洞是非常困难的。

JSON解析器在大多数编程语言中都很常见，因为它们直接映射到对象。相反，XML没有一个自然的文档到对象的映射。这使得使用JWT比使用SAML assertions更容易。

在使用方面，JWT 用于互联网规模。这突出了 JSON Web token 在多个平台(尤其是移动平台)上的客户端处理的易用性。

如果您想了解更多关于JSON Web令牌的信息，甚至开始使用它们在您自己的应用程序中执行身份验证，请浏览到 [JSON Web Token landing page](https://auth0.com/learn/json-web-tokens/) 查看 Auth0。
