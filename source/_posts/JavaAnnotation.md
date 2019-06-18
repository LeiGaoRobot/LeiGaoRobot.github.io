---
title: Java Annotation
date: 2019-04-11 09:51:41
categories: Java
tags:
- java annotation
- java
---
# Native

## @Resource

### Introduce

### Source Code

### Usage

## [@Transactional]((https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html))

### Introduce

javax.transaction.Transactional 注解提供了应用程序以声明式的方式控制事务的边界。此注解可以应用于Java EE规范定义为托管bean（包括CDI托管bean）的任何类。

javax.transaction.Transactional注释为应用程序提供了声明性地控制CDI托管bean上的事务边界的能力，以及Java EE规范定义为托管bean的类，在类和方法级别，方法级别注释覆盖了班级。

有关将@Transactional与EJB一起使用的限制，请参阅EJB规范。

这种支持是通过执行必要的挂起，恢复等的CDI拦截器实现的。事务拦截器仅插入业务方法调用而不插入生命周期事件。生命周期方法在未指定的事务上下文中调用。

如果尝试从使用@Transactional和NOT_SUPPORTED或NEVER以外的Transactional.TxType注释的bean或方法范​​围内调用UserTransaction接口的任何方法，则必须抛出IllegalStateException。在生命周期事件中允许使用UserTransaction。无论是否有任何@Transactional注释，都允许使用TransactionSynchronizationRegistry。

Transactional拦截器的优先级必须为Interceptor.Priority.PLATFORM_BEFORE + 200。有关更多详细信息，请参阅Interceptor规范。

注释的TxType元素指示是否要在事务上下文中执行bean方法。TxType.REQUIRED是默认值。

默认情况下，检查的异常不会导致事务拦截器标记事务以进行回滚以及RuntimeException及其子类的实例。可以通过指定导致拦截器标记事务以进行回滚的异常和/或不会导致回滚的异常来修改此默认行为。

可以设置rollbackOn元素以指示必须使拦截器将事务标记为回滚的异常。

相反，可以设置dontRollbackOn元素以指示异常，这些异常不得导致拦截器将事务标记为回滚。

为这些元素中的任何一个指定类时，指定的行为也适用于该类的子类。如果指定了两个元素，则dontRollbackOn优先。

### Source Code

### Usage

# Spring

## Spring Bean

### @Autowired

#### Introduce

#### Source Code

```
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
    boolean required() default true;
}
```

#### Usage

**Enabling @Autowired Annotations**

如果您在应用程序中使用基于Java的配置，则可以通过使用AnnotationConfigApplicationContext加载Spring Configuration来启用注解驱动的注入，如下所示：
```
@Configuration
@ComponentScan("com.baeldung.autowire.sample")
public class AppConfig {}
```

Spring XML中，则可以通过在Spring XML文件中声明它来启用它：<context：annotation-config />

**Using @Autowired**

启用注释注入后，可以在属性，setter和构造函数上使用自动装配。

**@Autowired on Properties**

注释可以直接用于属性，因此不需要getter和setter：

```
@Component("fooFormatter")
public class FooFormatter {
 
    public String format() {
        return "foo";
    }
}

@Component
public class FooService {
     
    @Autowired
    private FooFormatter fooFormatter;
 
}
```

在上面的例子中，春季查找并注入fooFormatter时FooService接口被创建。

**@Autowired on Setters**

该@Autowired注解可以在setter方法中使用。在下面的示例中，当在setter方法上使用注释时，在创建FooService时使用FooFormatter实例调用setter方法：

```
public class FooService {
 
    private FooFormatter fooFormatter;
 
    @Autowired
    public void setFooFormatter(FooFormatter fooFormatter) {
            this.fooFormatter = fooFormatter;
    }
}
```

**@Autowired on Constructors**

该@Autowired注释也可以在构造函数中使用。在下面的示例中，当注释上的构造使用时，实例FooFormatter注入作为参数给构造时FooService接口创建：

```
public class FooService {
 
    private FooFormatter fooFormatter;
 
    @Autowired
    public FooService(FooFormatter fooFormatter) {
        this.fooFormatter = fooFormatter;
    }
}
```

**@Autowired和Optional Dependencies**

Spring期望在构造依赖bean时可以使用@Autowired依赖项。如果框架无法解析bean进行连接，它将抛出下面引用的异常并阻止Spring容器成功启动：

> Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException:   
> No qualifying bean of type [com.autowire.sample.FooDAO] found for dependency:   
> expected at least 1 bean which qualifies as autowire candidate for this dependency.   
> Dependency annotations:   
> {@org.springframework.beans.factory.annotation.Autowired(required=true)}

为了避免这种情况发生，可以选择如下指定bean：

```
public class FooService {
 
    @Autowired(required = false)
    private FooDAO dataAccessor; 
     
}
```

**自动消除歧义**

默认情况下，Spring 按类型解析@Autowired条目。如果容器中有多个相同类型的bean，框架将抛出​​一个致命异常，表明有多个bean可用于自动装配。

**@Qualifier自动装配**

该@Qualifier注解可用于在暗示和缩小所需的bean：

```
@Component("fooFormatter")
public class FooFormatter implements Formatter {
 
    public String format() {
        return "foo";
    }
}

@Component("barFormatter")
public class BarFormatter implements Formatter {
 
    public String format() {
        return "bar";
    }
}

public class FooService {
     
    @Autowired
    private Formatter formatter;
 
}
```

由于可以为Spring容器注入两个具体的Formatter实现，因此Spring 在构造FooService时会抛出NoUniqueBeanDefinitionException异常：

> Caused by: org.springframework.beans.factory.NoUniqueBeanDefinitionException:   
> No qualifying bean of type [com.autowire.sample.Formatter] is defined:   
> expected single matching bean but found 2: barFormatter,fooFormatter  

通过使用@Qualifier注释缩小实现可以避免这种情况：

```
public class FooService {
     
    @Autowired
    @Qualifier("fooFormatter")
    private Formatter formatter;
 
}
```

通过使用特定实现的名称指定@Qualifier，在本例中为fooFormatter，当Spring找到多个相同类型的bean时，我们可以避免歧义。

请注意，价值@Qualifier注解与声明的名称相匹配@Component我们的注解FooFormatter实施。

**自定义限定符自动装配**

Spring允许我们创建自己的@Qualifier注释。要创建自定义限定符，请定义注释并在定义中提供@Qualifier注释，如下所示：

```
@Qualifier
@Target({
  ElementType.FIELD, ElementType.METHOD, ElementType.TYPE, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
public @interface FormatterType {
     
    String value();
 
}
```

一旦定义，FormatterType可以在各种实现中用于指定自定义值：

```
@FormatterType("Foo")
@Component
public class FooFormatter implements Formatter {
 
    public String format() {
        return "foo";
    }
}

@FormatterType("Bar")
@Component
public class BarFormatter implements Formatter {
 
    public String format() {
        return "bar";
    }
}
```

注释实现后，可以使用自定义限定符注释，如下所示：

```
@Component
public class FooService {
     
    @Autowired
    @FormatterType("Foo")
    private Formatter formatter;
     
}
```

@Target注释中指定的值限制限定符可用于标记注入点的位置。

在上面的代码片段中，限定符可用于消除Spring可以将bean注入字段，方法，类型和参数的点的歧义。

**按名称自动装配**

作为回退，Spring使用bean名称作为默认限定符值。

因此，通过定义bean属性的名称，在这种情况下fooFormatter，spring 匹配的FooFormatter执行以及何时注入的具体实施FooService接口的构造：

```
public class FooService {
     
    @Autowired
    private Formatter fooFormatter;
     
}
```

**结论**

尽管@Qualifier和bean名称后备匹配都可以用于缩小到特定的bean，但是自动装配实际上是关于按类型注入的，这就是使用此容器功能的最佳方式。


## Spring Boot

### @ConditionalOnProperty

*Spring Boot 2.1.4 API : https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnProperty.html*

#### Introduce

> Spring Boot通过@ConditionalOnProperty来控制Configuration是否生效

#### Source Code

```
@Retention(RetentionPolicy.RUNTIME)
@Target({ ElementType.TYPE, ElementType.METHOD })
@Documented
@Conditional(OnPropertyCondition.class)
public @interface ConditionalOnProperty {

    String[] value() default {}; //数组，获取对应property名称的值，与name不可同时使用  
  
    String prefix() default "";//property名称的前缀，可有可无  
  
    String[] name() default {};//数组，property完整名称或部分名称（可与prefix组合使用，组成完整的property名称），与value不可同时使用  
  
    String havingValue() default "";//可与name组合使用，比较获取到的属性值与havingValue给定的值是否相同，相同才加载配置  
  
    boolean matchIfMissing() default false;//缺少该property时是否可以加载。如果为true，没有该property也会正常加载；反之报错  
  
    boolean relaxedNames() default true;//是否可以松散匹配，至今不知道怎么使用的  
} 
```

#### Usage

> 通过其两个属性name以及havingValue来实现的，其中name用来从application.properties中读取某个属性值。  
> 如果该值为空，则返回false;  
> 如果值不为空，则将该值与havingValue指定的值进行比较，如果一样则返回true;否则返回false。  
> 如果返回值为false，则该configuration不生效；为true则生效。

```
@Configuration
//在application.properties配置"mf.assert"，对应的值为true, 也可以不写prefix，全写在name里(name="mf.assert")
@ConditionalOnProperty(prefix="mf",name = "assert", havingValue = "true")
public class AssertConfig {
    @Autowired
    private HelloServiceProperties helloServiceProperties;
    @Bean
    public HelloService helloService(){
        HelloService helloService = new HelloService();
        helloService.setMsg(helloServiceProperties.getMsg());
        return helloService;
    }
}
```

## Spring Cloud

### @EnableEurekaServer

#### Introduce

标明该类是Eureka服务注册中心。

### @EnableEurekaClient

#### Introduce

表明该服务Eureka的一个服务提供方。

### @EnableDiscoverClient

#### Introduce

声明该服务为Eureka中服务消费方

### @EnableFeignClients

#### Introduce

开启Feign声明式服务间通信（配合@FeignClient注解使用）。

> Feign是一个声明式的HTTP客户端，仅需要一个@FeignClient注解就能实现远程调用。Feign默认集成了Ribbon，并和Eureka结合，默认实现了负载均衡的效果。

### @FeignClient

#### Introduce

实现远程调用,需要填写**value**值，value属性值必须等于一个已在Eureka中注册的服务名称。

#### Source Code

```
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface FeignClient {
    @AliasFor("name")
    String value() default "";

    /** @deprecated */
    @Deprecated
    String serviceId() default "";

    String contextId() default "";

    @AliasFor("value")
    String name() default "";

    String qualifier() default "";

    String url() default "";

    boolean decode404() default false;

    Class<?>[] configuration() default {};

    Class<?> fallback() default void.class;

    Class<?> fallbackFactory() default void.class;

    String path() default "";

    boolean primary() default true;
}
```

@Target(ElementType.TYPE)修饰，表示FeignClient的作用目标在接口上。
@Retention(RetentionPolicy.RUNTIME)注解表明该注解会在Class字节码中存在，在运行时可以通过反射获取到。
@Documented表明该注解被包含在javadoc中。

@FeignClient用于创建声明是API接口，该接口是RESTful风格的。Feign被设计成插拔式的，可注入其他组件和Feign一起使用。最典型的是如果Ribbon可用，Feign会和Ribbon相结合进行负载均衡。

在代码中，value()和name()一样，是被调用的服务的ServiceId。url()直接填写硬编码URL地址。decode404（）即404是被解码，还是抛异常。configuration（）指明FeignClient的配置类，默认的配置类为FeignClientsConfiguration类，在缺省情况下，这个类注入了默认的Decoder、Encoder和Constant等配置的bean。fallback()为配置熔断器的处理类。

### @EnableHystrixDashboard

#### Introduce

开启对熔断器Hystrix的实时监控仪表盘

### @EnableZuulProxy

#### Introduce

开启Zuul网关的支持。

### @EnableConfigServer

#### Introduce

开启配置文件服务支持

