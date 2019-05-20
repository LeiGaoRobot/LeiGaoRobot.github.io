---
title: Spring Security
date: 2019-05-14 17:14:39
categories: Java
tags:
- java
- spring
- security
- spring security
---

# What is Spring Security?

Spring Security是一个 Java/Java EE 框架，为企业应用程序提供身份验证，授权和其他安全功能。该项目于2003年底开始作为'Acegi Security'（发音为Ah-see-gee，其字母为英文字母中的第1,3,5,7和9个字符，以防止名称冲突） Alex，于2004年3月在Apache License下公开发布。随后，Acegi被纳入Spring组合作为Spring Security，一个官方的Spring子项目。新名称下的第一个公开发布是2008年4月的Spring Security 2.0.0，SpringSource提供了商业支持和培训。

> Spring Security是一个功能强大且可高度自定义的身份验证和访问控制框架。它是保护基于Spring的应用程序的事实标准。  
> Spring Security是一个专注于为Java应用程序提供身份验证和授权的框架。与所有Spring项目一样，Spring Security的真正强大之处在于它可以轻松扩展以满足自定义要求

## Features

+ 对身份验证和授权的全面和可扩展的支持
+ 防止会话固定，点击劫持，跨站点请求伪造等攻击
+ Servlet API集成
+ 可选与Spring Web MVC集成

### Key authentication features

+ LDAP（使用基于绑定和密码比较策略）用于集中身份验证信息。
+ 使用流行的中央身份验证服务的单点登录功能。
+ Java身份验证和授权服务（JAAS）LoginModule，一种在Java中使用的基于标准的身份验证方法。请注意，此功能仅是对JAAS Loginmodule的委派。
+ 通过 IETF Request for Comments 1945 标准定义的基本访问认证。
+ 通过 IETF Request for Comments 2617 和 RFC 2069 标准定义的摘要访问认证。
+ 通过 Secure Sockets Layer(SSL,又叫Transport Layer Security,TLS) 标准的 X.509 客户端证书表示。
+ CA，Inc SiteMinder用于身份验证（一种流行的商业访问管理产品）。
+ 类似于Su（Unix）支持通过HTTP或HTTPS连接切换主体身份。
+ Run-as replacement，使操作能够采用不同的安全标识。
+ 匿名身份验证，这意味着即使是未经身份验证的主体也会分配安全身份。
+ 容器适配器（自定义领域）支持Apache Tomcat，Resin，JBoss和Jetty（Web服务器）。
+ Windows NTLM启用浏览器集成（实验性）。
+ Web表单身份验证，类似于Servlet容器规范。
+ 通过HTTP Cookie “Remember-me”支持。
+ 并发会话支持，限制委托人允许的同时登录次数。
+ 完全支持自定义和插入自定义身份验证实现。

### Instance-based security features

+ AspectJ方法调用授权。
+ 使用Apache Ant路径或正则表达式选择Web请求URL的HTTP授权。

### Other features 

+ 软件本地化，因此用户界面消息可以使用任何语言。
+ 通道安全性，在满足特定规则时自动在HTTP和HTTPS之间切换。
+ 在框架的所有数据库触摸区域中进行缓存。
+ 发布消息以促进事件驱动的编程。
+ 支持通过JUnit执行集成测试。
+ Spring Security本身具有全面的JUnit隔离测试。
+ 几个示例应用程序，详细的JavaDocs和参考指南。
+ Web框架独立性。

# Registration

## Basic Registration Process

