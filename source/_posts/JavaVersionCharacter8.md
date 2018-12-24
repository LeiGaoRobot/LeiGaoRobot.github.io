---
title: Java8 版本特性
date: 2018-12-17 10:20:40
categories: java
tags: 
- java8
- lambda
---

# 函数式接口

## **What is functional interface?**

>函数式接口（functional interface）就是只定义一个抽象方法的接口，比如 Java API 中的 Predicate、Comparator 和 Runnable 等。Lambda 表达式允许你直接以内联的形式为函数式接口的抽象方法提供实现，并把整个表达式作为函数式接口的实例（具体说来，是函数式接口一个具体实现的实例）。

Java 8 引入的一个核心概念是函数式接口（Functional Interfaces）。通过在接口里面添加一个抽象方法，这些方法可以直接从接口中运行。如果一个接口定义个唯一一个抽象方法，那么这个接口就成为函数式接口。同时，引入了一个新的注解：@FunctionalInterface。可以把他它放在一个接口前，表示这个接口是一个函数式接口。这个注解是非必须的，只要接口只包含一个方法的接口，虚拟机会自动判断，不过最好在接口上使用注解 @FunctionalInterface 进行声明。在接口中添加了 @FunctionalInterface 的接口，只允许有一个抽象方法，否则编译器也会报错。

java.lang.Runnable 就是一个函数式接口。
```
@FunctionalInterface
public interface Runnable {
   public abstract void run();
}
```

---
# Lambda表达式

## **What is lambda expression?**

>“Lambda 表达式”(lambda expression)是一个匿名函数，Lambda表达式基于数学中的λ演算得名，直接对应于其中的lambda抽象(lambda abstraction)，是一个匿名函数，即没有函数名的函数。Lambda表达式可以表示闭包（注意和数学传统意义上的不同）。[百度百科](https://baike.baidu.com/item/Lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F)
>>匿名函数,在计算机编程中，匿名函数（英语：anonymous function）是指一类无需定义标识符（函数名）的函数或子程序，普遍存在于多种编程语言中。1958年LISP首先采用匿名函数，自此之后，越来越多编程语言陆续采用，主流的编程语言如PHP和C++也在不久前采用。[Wiki](https://zh.wikipedia.org/wiki/%E5%8C%BF%E5%90%8D%E5%87%BD%E6%95%B0)

>>λ演算（英语：lambda calculus，λ-calculus）是一套从数学逻辑中发展，以变量绑定和替换的规则，来研究函数如何抽象化定义、函数如何被应用以及递归的形式系统。它由数学家阿隆佐·邱奇在20世纪30年代首次发表。lambda演算作为一种广泛用途的计算模型，可以清晰地定义什么是一个可计算函数，而任何可计算函数都能以这种形式表达和求值，它能模拟单一磁带图灵机的计算过程；尽管如此，lambda演算强调的是变换规则的运用，而非实现它们的具体机器。[Wiki](https://zh.wikipedia.org/wiki/%CE%9B%E6%BC%94%E7%AE%97)

Lambda 表达式可以理解为简洁地表示可传递的匿名函数的一种方式：它没有名称，但它有参数列表、函数主体、返回类型，可能还有一个可以抛出的异常列表。它的核心思想是将面向对象中的传递数据变成传递行为。

重要特征
+ **可选类型声明** - 无需声明参数类型。编译器可以从参数的值推断出相同的值
+ **参数的可选括号** - 无需在括号中声明单个参数。对于多个参数，需要括号
+ **可选的花括号** - 如果主体包含单个语句，则无需在表达式主体中使用花括号
+ **可选的return关键字** - 如果正文具有单个表达式以返回值，则编译器会自动返回该值。需要使用大括号来表示表达式返回一个值

重要特点
+ **匿名** - 它不像普通方法那样有一个明确的名称
+ **函数** - Lambda 表达式是函数是因为它不像方法那样属于某个特定的类，但和方法一样，Lambda 有参数列表、函数主体、返回类型，还可能有可以抛出的异常列表
+ **传递** - Lambda 表达式可以作为参数传递给方法或存储在变量中
+ **简洁** - 无需像匿名类那样写很多模板代码

Lambda表达式在Java 8中引入.Lambda表达式有助于函数式编程，并简化了很多开发。

## **Syntax**

Lambda 表达式由参数列表、箭头和 Lambda 主体组成。

`parameter -> expression body`

## **Example**

>函数式编程（functional programming）或称函数程序设计，又称泛函编程，是一种编程典范，它将计算机运算视为数学上的函数计算，并且避免使用程序状态以及易变对象。函数编程语言最重要的基础是λ演算（lambda calculus）。而且λ演算的函数可以接受函数当作输入（引数）和输出（传出值）。[Wiki](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B8%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80)
>>lambda演算可比拟是最根本的编程语言，它包括了一条变换规则（变量替换）和一条将函数抽象化定义的方式。因此普遍公认是一种更接近软件而非硬件的方式。对函数式编程语言造成很大影响，比如Lisp、ML语言和Haskell语言。在1936年邱奇利用λ演算给出了对于判定性问题（Entscheidungsproblem）的否定：关于两个lambda表达式是否等价的命题，无法由一个“通用的算法”判断，这是不可判定性能够证明的头一个问题，甚至还在停机问题之先。

```
public class Java8Tester {

   public static void main(String args[]) {
      Java8Tester tester = new Java8Tester();
		
      //with type declaration
      MathOperation addition = (int a, int b) -> a + b;
		
      //with out type declaration
      MathOperation subtraction = (a, b) -> a - b;
		
      //with return statement along with curly braces
      MathOperation multiplication = (int a, int b) -> { return a * b; };
		
      //without return statement and without curly braces
      MathOperation division = (int a, int b) -> a / b;
		
      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));
		
      //without parenthesis
      GreetingService greetService1 = message -> System.out.println("Hello " + message);
		
      //with parenthesis
      GreetingService greetService2 = (message) -> System.out.println("Hello " + message);
		
      greetService1.sayMessage("Mahesh");
      greetService2.sayMessage("Suresh");
   }
	
   @FunctionalInterface
   interface MathOperation {
      int operation(int a, int b);
   }
	
   @FunctionalInterface
   interface GreetingService {
      void sayMessage(String message);
   }
	
   private int operate(int a, int b, MathOperation mathOperation) {
      return mathOperation.operation(a, b);
   }
}
```

以下是对使用上述例子认为是重要的观点:
- Lambda表达式主要用于定义功能接口的内联实现，即仅具有单个方法的接口。在上面的例子中，我们使用了各种类型的lambda表达式来定义MathOperation接口的操作方法。然后我们定义了GreetingService的sayMessage的实现。
- Lambda表达式消除了对匿名类的需求，并为Java提供了非常简单但功能强大的函数编程功能。


使用案例 | Lambda案例
--|:--|
布尔表达式|`(List<String> list) -> list.isEmpty()`
创建对象|`() -> new Object()`
打印信息|`(String str) -> System.out.println(str)`
遍历集合|`Arrays.asList( "a", "b", "d" ).forEach(e -> System.out.println( e ))`
排序比较|`Arrays.asList( "a", "b", "d" ).sort(( e1, e2 ) -> e1.compareTo( e2 ))`

## **Tips**

使用lambda表达式，您可以引用任何最终变量或有效的最终变量（仅分配一次）。如果第二次为变量赋值，则Lambda表达式会抛出编译错误。

---
# 方法引用

## **What is method references**

方法引用有助于通过名称指向方法，可以使语言的构造更紧凑简洁，减少冗余代码。使用“::”符号描述方法引用。方法引用可用于指出以下类型的方法
+ 静态方法
+ 实例方法
+ 使用new运算符的构造函数（TreeSet :: new）

## **Syntax**

+ 构造器引用：它的语法是Class::new，或者更一般的Class< T >::new实例如下：
```
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
class Car {
    public static Car create(final Supplier<Car> supplier) {
        return supplier.get();
    }
 
    public static void collide(final Car car) {
        System.out.println("Collided " + car.toString());
    }
 
    public void follow(final Car another) {
        System.out.println("Following the " + another.toString());
    }
 
    public void repair() {
        System.out.println("Repaired " + this.toString());
    }
}
class Main {
   public static void main(String[] args) {
      final Car car = Car.create( Car::new );
      final List< Car > cars = Arrays.asList( car );
    }
}
```
+ 静态方法引用：它的语法是Class::static_method，实例如下：
```
cars.forEach( Car::collide );
```
+ 特定类的任意对象的方法引用：它的语法是Class::method实例如下：
```
cars.forEach( Car::repair );
```
+ 特定对象的方法引用：它的语法是instance::method实例如下
```
final Car police = Car.create( Car::new );
cars.forEach( police::follow );
```
---
# 默认方法和静态方法

## **What is default method and static method?**

Java 8 对接口做了进一步的增强。在接口中可以添加使用 default 关键字修饰的非抽象方法。还可以在接口中定义静态方法。如今，接口看上去与抽象类的功能越来越类似了。

Java 8在接口中引入了默认方法实现的新概念。添加此功能是为了向后兼容，以便可以使用旧接口来利用Java 8的lambda表达式功能。给接口添加一个非抽象的方法实现，只需要使用 default 关键字即可，这个特征又叫做扩展方法。在实现该接口时，该默认扩展方法在子类上可以直接使用，它的使用方式类似于抽象类中非抽象成员方法。但扩展方法不能够重载 Object 中的方法。例如：toString、equals、 hashCode 不能在接口中被重载。

在接口中，还允许定义静态的方法。接口中的静态方法可以直接用接口来调用。

## **Syntax**

Default：

```
public interface vehicle {

   default void print() {
      System.out.println("I am a vehicle!");
   }
}
```

Mutiple Defaults：

一个接口有默认方法，考虑这样的情况，一个类实现了多个接口，且这些接口有相同的默认方法，以下实例说明了这种情况的解决方法：

```
public interface vehicle {

   default void print() {
      System.out.println("I am a vehicle!");
   }
}

public interface fourWheeler {

   default void print() {
      System.out.println("I am a four wheeler!");
   }
}
```

第一种解决方案，创建自己的默认方法来重写接口的默认方法
```
public class interface Car implements Vehicle, fourWheeler{

   default void print(){
      System.out.println("I am a four wheeler car vehicle!");
   }
}
```

第二种解决方案，使用super调用指定接口的默认方法
```
public class Car implements Vehicle, FourWheeler {

   public void print(){
      Vehicle.super.print();
   }
}
```

Static Default Methods：

在接口中，还允许定义静态的方法，可以声明（并且可以提供实现）的静态方法。接口中的静态方法可以直接用接口来调用。
```
public interface vehicle {
	
   static void blowHorn() {
      System.out.println("Blowing horn!!!");
   }
}
public class TestStaticFun {

   public static void main(String[] args){
      vehicle.blowHorn();
   }  
}
```

---
# Streams

## **What is Stream?**

Java 8 引入了流式操作（Stream），通过该操作可以实现对集合（Collection）的并行处理和函数式操作。根据操作返回的结果不同，流式操作分为中间操作和最终操作两种。最终操作返回一特定类型的结果，而中间操作返回流本身，这样就可以将多个操作依次串联起来。根据流的并发性，流又可以分为串行和并行两种。流式操作实现了集合的过滤、排序、映射等功能。

Stream 和 Collection 集合的区别：Collection 是一种静态的内存数据结构，而 Stream 是有关计算的。前者是主要面向内存，存储在内存中，后者主要是面向 CPU，通过 CPU 实现计算。

Stream 使用一种类似用 SQL 语句从数据库查询数据的直观方式来提供一种对 Java 集合运算和表达的高阶抽象。以下是流的特征
+ 元素序列 - 流以顺序方式提供特定类型的一组元素。流按需获取/计算元素。它从不存储元素。
+ Source - Stream将集合，数组，I/O channel，产生器generator等作为输入源。
+ 聚合操作 - Stream支持聚合操作，如过滤，映射，限制，缩减，查找，匹配等。
+ 中间操作 - 中间操作都会返回流对象本身。 这样多个操作可以串联成一个管道， 如同流式风格（fluent style）。 这样做可以对操作进行优化， 比如延迟执行(laziness)和短路( short-circuiting)。
+ 内部迭代 - 以前对集合遍历都是通过Iterator或者For-Each的方式, 显式的在集合外部进行迭代， 这叫做外部迭代。 Stream提供了内部迭代的方式， 通过访问者模式(Visitor)实现。



## **Syntax**

### 生成流

流有串行和并行两种, 集合接口有两个方法来生成流：

+ stream() − 为集合创建串行流。
```
   List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
   strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.toList()).forEach(System.out::println);
```
+ stream.sequential() − 返回串行的流。
```
   List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
   strings.stream().sequential().filter(string -> !string.isEmpty()).collect(Collectors.toList()).forEach(System.out::println);
```
+ parallelStream() − 为集合创建并行流。
```
   List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
   // 获取空字符串的数量
   long count = strings.parallelStream().filter(string -> string.isEmpty()).count();
```
+ stream.parallel() − 返回并行的流。
```
   List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
   // 获取空字符串的数量
   long count = strings.stream().parallel().filter(string -> string.isEmpty()).count();
```

串行流上的操作是在一个线程中依次完成，而并行流则是在多个线程上同时执行。并行与串行的流可以相互切换。相比较串行的流，并行的流可以很大程度上提高程序的执行效率。

### 中间操作

该操作会保持 stream 处于中间状态，允许做进一步的操作。它返回的还是的 Stream，允许更多的链式操作。常见的中间操作有：
+ filter() - 对元素进行过滤,用于通过设置的条件过滤出元素
```
List<String>strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
// 获取空字符串的数量
int count = strings.stream().filter(string -> string.isEmpty()).count();
```
+ sorted() - 对元素排序,用于对流进行排序
```
Random random = new Random();
random.ints().limit(10).sorted().forEach(System.out::println);
```
+ map() - 元素的映射,用于映射每个元素到对应的结果
```
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
// 获取对应的平方数
List<Integer> squaresList = numbers.stream().map( i -> i*i).distinct().collect(Collectors.toList());
```
+ distinct() - 去除重复元素,去除流中重复的元素
```
Stream<String> stream = Stream.of("a", "a", "b", "c");
stream.distinct().forEach(System.out::println);
```
+ subStream() - 获取子 Stream 等
+ [more](https://www.geeksforgeeks.org/java-8-stream/)

### 终止操作

该操作必须是流的最后一个操作，一旦被调用，Stream 就到了一个终止状态，而且不能再使用了。常见的终止操作有：
+ forEach() - 对每个元素做处理,迭代流中的每个数据
```
Random random = new Random();
random.ints().limit(10).forEach(System.out::println);
```
+ toArray() - 把元素导出到数组
+ findFirst() - 返回第一个匹配的元素
+ anyMatch() - 是否有匹配的元素等
+ collect() - Collectors 类实现了很多归约操作,例如将流转换成集合和聚合元素。Collectors 可用于返回列表或字符串
```
   List<String>strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
   List<String> filtered = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.toList());
   System.out.println("筛选列表: " + filtered);
   String mergedString = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.joining(", "));
   System.out.println("合并字符串: " + mergedString);
```
+ [more](https://www.geeksforgeeks.org/java-8-stream/)

---
# Optional Class

## **What is Optional Class?**

Optional 类是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。

Optional 是个容器：它可以保存类型T的值，或者仅仅保存null。Optional提供很多有用的方法，这样我们就不用显式进行空值检测。

Optional 类的引入很好的解决空指针异常。

[官方文档](https://docs.oracle.com/javase/8/docs/api/)

### 类声明

java.util.Optional<T> 类的声明：
```
public final class Optional<T> {
   ...
}
```

### 类方法

Modifier and Type | Method | Description
--|:--|:--|
static\<T>Optional\<T> | empty() | 返回空的 Optional 实例
boolean | equals(Object obj) | 判断其他对象是否等于 Optional
Optional\<T> | filter(Predicate<? super \<T> predicate) | 如果值存在，并且这个值匹配给定的 predicate，返回一个Optional用以描述这个值，否则返回一个空的Optional
\<U> Optional\<U> | flatMap(Function<?superT,Optional\<U>>mapper) | 如果值存在，返回基于Optional包含的映射方法的值，否则返回一个空的Optional
T | get() | 如果在这个Optional中包含这个值，返回值，否则抛出异常NoSuchElementException
int | hashCode() | 返回存在值的哈希码，如果值不存在 返回 0
void | ifPresent(Consumer<? super T> consumer) | 如果值存在则使用该值调用 consumer , 否则不做任何事情
boolean | isPresent() | 如果值存在则方法会返回true，否则返回 false
\<U>Optional\<U> | map(Function<? super T,? extends U> mapper) | 如果有值，则对其执行调用映射函数得到返回值。如果返回值不为 null，则创建包含映射返回值的Optional作为map方法返回值，否则返回空Optional
static <T> Optional<T> | of(T value) | 返回一个指定非null值的Optional
static <T> Optional<T> | ofNullable(T value) | 如果为非空，返回 Optional 描述的指定值，否则返回空的 Optional
T | orElse(T other) | 如果存在该值，返回值， 否则返回 other
T | orElseGet(Supplier<? extends T> other) | 如果存在该值，返回值， 否则触发 other，并返回 other 调用的结果
<X extends Throwable> T | orElseThrow(Supplier<? extends X> exceptionSupplier) | 如果存在该值，返回包含的值，否则抛出由 Supplier 继承的异常
String | toString() | 返回一个Optional的非空字符串，用来调试

注意： 这些方法是从 java.lang.Object 类继承来的。


## **Example**

解决空指针异常,可能为空的值或者某个类型的值：
```
private String getUserName(User user) {
    Optional<User> userOptional = Optional.ofNullable(user);
    return userOptional.map(User::getUserName).orElse(null);
}
```

Usage Demo：
```
import java.util.Optional;
 
public class Java8Tester {
   public static void main(String args[]){
   
      Java8Tester java8Tester = new Java8Tester();
      Integer value1 = null;
      Integer value2 = new Integer(10);
        
      // Optional.ofNullable - 允许传递为 null 参数
      Optional<Integer> a = Optional.ofNullable(value1);
        
      // Optional.of - 如果传递的参数是 null，抛出异常 NullPointerException
      Optional<Integer> b = Optional.of(value2);
      System.out.println(java8Tester.sum(a,b));
   }
    
   public Integer sum(Optional<Integer> a, Optional<Integer> b){
    
      // Optional.isPresent - 判断值是否存在
        
      System.out.println("第一个参数值存在: " + a.isPresent());
      System.out.println("第二个参数值存在: " + b.isPresent());
        
      // Optional.orElse - 如果值存在，返回它，否则返回默认值
      Integer value1 = a.orElse(new Integer(0));
        
      //Optional.get - 获取值，值需要存在
      Integer value2 = b.get();
      return value1 + value2;
   }
}
```

---
# 安全性

## 安全性增强

现今，互联网环境中存在各种各种潜在的威胁，对于 Java 平台来说，安全显得特别重要。为了保证新版本具有更高的安全性，Java 8 在安全性上对许多方面进行了增强，也为此推迟了它的发布日期。下面例举其中几个关于安全性的更新：

支持更强的基于密码的加密算法。基于 AES 的加密算法，例如 PBEWithSHA256AndAES_128 和 PBEWithSHA512AndAES_256，已经被加入进来。

在客户端，TLS1.1 和 TLS1.2 被设为默认启动。并且可以通过新的系统属性包 jdk.tls.client.protocols 来对它进行配置。

Keystore 的增强，包含新的 Keystore 类型 java.security.DomainLoadStoreParameter 和为 Keytool 这个安全钥匙和证书的管理工具添加新的命令行选项-importpassword。同时，添加和更新了一些关于安全性的 API 来支持 KeyStore 的更新。

支持安全的随机数发生器。如果随机数来源于随机性不高的种子，那么那些用随机数来产生密钥或者散列敏感信息的系统就更易受攻击。SecureRandom 这个类的 getInstanceStrong 方法如今可以获取各个平台最强的随机数对象实例，通过这个实例生成像 RSA 私钥和公钥这样具有较高熵的随机数。

JSSE（Java(TM) Secure Socket Extension）服务器端开始支持 SSL/TLS 服务器名字识别 SNI（Server Name Indication）扩展。SNI 扩展目的是 SSL/TLS 协议可以通过 SNI 扩展来识别客户端试图通过握手协议连接的服务器名字。在 Java 7 中只在客户端默认启动 SNI 扩展。如今，在 JSSE 服务器端也开始支持 SNI 扩展了。

安全性比较差的加密方法被默认禁用。默认不支持 DES 相关的 Kerberos 5 加密方法。如果一定要使用这类弱加密方法需要在 krb5.conf 文件中添加 allow_weak_crypto=true。考虑到这类加密方法安全性极差，开发者应该尽量避免使用它。

## Java8 Base64

在Java 8中，Base64编码已经成为Java类库的标准。
Java 8 内置了 Base64 编码的编码器和解码器。
Base64工具类提供了一套静态方法获取下面三种BASE64编解码器：
+ 基本 - 输出被映射到一组字符A-Za-z0-9+/，编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/。
+ URL - 输出映射到一组字符A-Za-z0-9+_，输出是URL和文件。
+ MIME - 输出隐射到MIME友好格式。输出每行不超过76字符，并且使用'\r'并跟随'\n'作为分割。编码输出最后没有行分割。

### 内嵌类
内嵌类 | 描述
--|:--|
static class Base64.Decoder | 该类实现一个解码器用于，使用 Base64 编码来解码字节数据。
static class Base64.Encoder | 该类实现一个编码器，使用 Base64 编码来编码字节数据。

### 方法
方法名 | 描述
--|:--|
static Base64.Decoder getDecoder() | 返回一个 Base64.Decoder ，解码使用基本型 base64 编码方案。
static Base64.Encoder getEncoder() | 返回一个 Base64.Encoder ，编码使用基本型 base64 编码方案。
static Base64.Decoder getMimeDecoder() | 返回一个 Base64.Decoder ，解码使用 MIME 型 base64 编码方案。
static Base64.Encoder getMimeEncoder() | 返回一个 Base64.Encoder ，编码使用 MIME 型 base64 编码方案。
static Base64.Encoder getMimeEncoder(int lineLength, byte[] lineSeparator) | 返回一个 Base64.Encoder ，编码使用 MIME 型 base64 编码方案，可以通过参数指定每行的长度及行的分隔符。
static Base64.Decoder getUrlDecoder() | 返回一个 Base64.Decoder ，解码使用 URL 和文件名安全型 base64 编码方案。
static Base64.Encoder getUrlEncoder() | 返回一个 Base64.Encoder ，编码使用 URL 和文件名安全型 base64 编码方案。

注意：Base64 类的很多方法从 java.lang.Object 类继承。

### **Example**
```
import java.util.Base64;
import java.util.UUID;
import java.io.UnsupportedEncodingException;
 
public class Java8Tester {
   public static void main(String args[]){
      try {
        
         // 使用基本编码
         String base64encodedString = Base64.getEncoder().encodeToString("runoob?java8".getBytes("utf-8"));
         System.out.println("Base64 编码字符串 (基本) :" + base64encodedString);
        
         // 解码
         byte[] base64decodedBytes = Base64.getDecoder().decode(base64encodedString);
        
         System.out.println("原始字符串: " + new String(base64decodedBytes, "utf-8"));
         base64encodedString = Base64.getUrlEncoder().encodeToString("TutorialsPoint?java8".getBytes("utf-8"));
         System.out.println("Base64 编码字符串 (URL) :" + base64encodedString);
        
         StringBuilder stringBuilder = new StringBuilder();
        
         for (int i = 0; i < 10; ++i) {
            stringBuilder.append(UUID.randomUUID().toString());
         }
        
         byte[] mimeBytes = stringBuilder.toString().getBytes("utf-8");
         String mimeEncodedString = Base64.getMimeEncoder().encodeToString(mimeBytes);
         System.out.println("Base64 编码字符串 (MIME) :" + mimeEncodedString);
         
      }catch(UnsupportedEncodingException e){
         System.out.println("Error :" + e.getMessage());
      }
   }
}
```
---
# 日期时间 API

## Date/time API的改进

Java 8通过发布新的Date-Time API (JSR 310)来进一步加强对日期与时间的处理，支持新的 Unicode 6.2.0 标准。

在旧版的 Java 中，日期时间 API 存在诸多问题，其中有：

+ 非线程安全 − java.util.Date 是非线程安全的，所有的日期类都是可变的，这是Java日期类最大的问题之一。
+ 设计很差 − Java的日期/时间类的定义并不一致，在java.util和java.sql的包中都有日期类，此外用于格式化和解析的类在java.text包中定义。java.util.Date同时包含日期和时间，而java.sql.Date仅包含日期，将其纳入java.sql包并不合理。另外这两个类都有相同的名字，这本身就是一个非常糟糕的设计。
+ 时区处理麻烦 − 日期类并不提供国际化，没有时区支持，因此Java引入了java.util.Calendar和java.util.TimeZone类，但他们同样存在上述所有的问题。

Java 8 在 java.time 包下提供了很多新的 API。常用的几个类有：
+ Clock - 使用时区来返回当前的纳秒时间和日期
+ Instant - 一个instant对象表示时间轴上的一个时间点，Instant.now()方法会返回当前的瞬时点（格林威治时间）
+ Duration - 用于表示两个瞬时点相差的时间量
+ LocalDate − 个带有年份，月份和天数的日期，可以使用静态方法now或者of方法进行创建
+ LocalTime − 表示一天中的某个时间，同样可以使用now和of进行创建
+ LocalDateTime - 兼有日期和时间
+ ZonedDateTime - 通过设置时间的id来创建一个带时区的时间
+ DateTimeFormatter - 日期格式化类，提供了多种预定义的标准格式

新的java.time包涵盖了所有处理日期，时间，日期/时间，时区，时刻（instants），过程（during）与时钟（clock）的操作。

## **Example**

```
public class TimeTest {
    public static void main(String[] args) {
      Clock clock = Clock.systemUTC();
      Instant instant = clock.instant();
      System.out.println(instant.toString());

      // Get duration between two dates
      final LocalDateTime from = LocalDateTime.of( 2014, Month.APRIL, 16, 0, 0, 0 );
      final LocalDateTime to = LocalDateTime.of( 2015, Month.APRIL, 16, 23, 59, 59 );
      final Duration duration = Duration.between( from, to );
      System.out.println( "Duration in days: " + duration.toDays() );
      System.out.println( "Duration in hours: " + duration.toHours() );

      LocalDate localDate = LocalDate.now();
      System.out.println(localDate.toString());

      LocalTime localTime = LocalTime.now();
      System.out.println(localTime.toString());

      LocalDateTime localDateTime = LocalDateTime.now();
      System.out.println(localDateTime.toString());

      ZonedDateTime zonedDateTime = ZonedDateTime.now(ZoneId.of("Asia/Shanghai"));
      System.out.println(zonedDateTime.toString());

      System.out.println(DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL).format(LocalDateTime.now()));
    }
}
```

---
# 注解

## 注解的更新

对于注解，Java 8 主要有两点改进：类型注解和重复注解。

Java 8 的类型注解扩展了注解使用的范围。在该版本之前，注解只能是在声明的地方使用。现在几乎可以为任何东西添加注解：局部变量、类与接口，就连方法的异常也能添加注解。新增的两个注释的程序元素类型 ElementType.TYPE_USE 和 ElementType.TYPE_PARAMETER 用来描述注解的新场合。ElementType.TYPE_PARAMETER 表示该注解能写在类型变量的声明语句中。而 ElementType.TYPE_USE 表示该注解能写在使用类型的任何语句中（例如声明语句、泛型和强制转换语句中的类型）。

对类型注解的支持，增强了通过静态分析工具发现错误的能力。原先只能在运行时发现的问题可以提前在编译的时候被排查出来。Java 8 本身虽然没有自带类型检测的框架，但可以通过使用 Checker Framework 这样的第三方工具，自动检查和确认软件的缺陷，提高生产效率。

例如，下面的代码可以通过编译，但是运行时会报 NullPointerException 的异常。
```
public class TestAnno {
   public static void main(String[] args) {
      Object obj = null;
      obj.toString();
   }
}
```

为了能在编译期间就自动检查出这类异常，可以通过类型注解结合 Checker Framework 提前排查出来：
```
import org.checkerframework.checker.nullness.qual.NonNull;
public class TestAnno {
   public static void main(String[] args) {
      @NonNull Object obj = null;
      obj.toString();
   }
}
```

编译时自动检测结果如下：
```
C:\workspace\TestJava8\src\TestAnno.java:4: Warning:
  (assignment.type.incompatible) $$ 2 $$ null $$ @UnknownInitialization @NonNull Object $$ ( 152, 156 )
  $$ incompatible types in assignment.
@NonNull Object obj = null;
 ^
 found : null
 required: @UnknownInitialization @NonNull Object
```

另外，在该版本之前使用注解的一个限制是相同的注解在同一位置只能声明一次，不能声明多次。Java 8 引入了重复注解机制，这样相同的注解可以在同一地方声明多次。重复注解机制本身必须用 @Repeatable 注解。

例如，下面就是用 @Repeatable 重复注解的例子：
```
@Retention(RetentionPolicy.RUNTIME) \\该注解存在于类文件中并在运行时可以通过反射获取
@interface Annots {
   Annot[] value();
}

@Retention(RetentionPolicy.RUNTIME) \\该注解存在于类文件中并在运行时可以通过反射获取
@Repeatable(Annots.class)
@interface Annot {
   String value();
}

@Annot("a1")
@Annot("a2")
public class Test {
   public static void main(String[] args) {
      Annots annots1 = Test.class.getAnnotation(Annots.class);
      System.out.println(annots1.value()[0]+","+annots1.value()[1]); 
      // 输出: @Annot(value=a1),@Annot(value=a2)
      Annot[] annots2 = Test.class.getAnnotationsByType(Annot.class);
      System.out.println(annots2[0]+","+annots2[1]); 
      // 输出: @Annot(value=a1),@Annot(value=a2)
   }
}
```

注释 Annot 被 @Repeatable( Annots.class ) 注解。Annots 只是一个容器，它包含 Annot 数组, 编译器尽力向程序员隐藏它的存在。通过这样的方式，Test 类可以被 Annot 注解两次。重复注释的类型可以通过 getAnnotationsByType() 方法来返回。

---
# IO/NIO

## IO/NIO 的改进

Java 8 对 IO/NIO 也做了一些改进。主要包括：改进了 java.nio.charset.Charset 的实现，使编码和解码的效率得以提升，也精简了 jre/lib/charsets.jar 包；优化了 String(byte[],*) 构造方法和 String.getBytes() 方法的性能；还增加了一些新的 IO/NIO 方法，使用这些方法可以从文件或者输入流中获取流（java.util.stream.Stream），通过对流的操作，可以简化文本行处理、目录遍历和文件查找。

新增的 API 如下：
+ BufferedReader.line() - 返回文本行的流 Stream<String>
+ File.lines(Path, Charset) - 返回文本行的流 Stream<String>
+ File.list(Path) - 遍历当前目录下的文件和目录
+ File.walk(Path, int, FileVisitOption) - 遍历某一个目录下的所有文件和指定深度的子目录
+ File.find(Path, int, BiPredicate, FileVisitOption... ) - 查找相应的文件

## **Example**

下面就是用流式操作列出当前目录下的所有文件和目录：
```
   Files.list(new File(".").toPath()).forEach(System.out::println);
```

---
# Nashorn JavaScript

## **What is Nashorn JavaScript?**

[Nashorn JavaScript引擎](https://www.javacodegeeks.com/2014/02/java-8-compiling-lambda-expressions-in-the-new-nashorn-js-engine.html) 

从JDK 1.8开始，Nashorn取代Rhino(JDK 1.6, JDK1.7)成为Java的嵌入式JavaScript引擎。Nashorn完全支持ECMAScript 5.1规范以及一些扩展。它使用基于JSR 292的新语言特性，其中包含在JDK 7中引入的 invokedynamic，将JavaScript编译成Java字节码。

与先前的Rhino实现相比，这带来了2到10倍的性能提升。

## **Usage**

### jjs

jjs是个基于Nashorn引擎的命令行工具。它接受一些JavaScript源代码为参数，并且执行这些源代码。

例如，我们创建一个具有如下内容的sample.js文件：
```
   print('Hello World!');
```

打开控制台，输入以下命令并输出：
```
   $ jjs sample.js
   $ Hello World!
```

### Java 中调用 JavaScript

使用 ScriptEngineManager, JavaScript 代码可以在 Java 中执行，实例如下：
```
import javax.script.ScriptEngineManager;
import javax.script.ScriptEngine;
import javax.script.ScriptException;
 
public class Java8Tester {
   public static void main(String args[]){
   
      ScriptEngineManager scriptEngineManager = new ScriptEngineManager();
      ScriptEngine nashorn = scriptEngineManager.getEngineByName("nashorn");
        
      String name = "Runoob";
      Integer result = null;
      
      try {
         nashorn.eval("print('" + name + "')");
         result = (Integer) nashorn.eval("10 + 2");
         
      }catch(ScriptException e){
         System.out.println("执行脚本错误: "+ e.getMessage());
      }
      
      System.out.println(result.toString());
   }
}
```

执行以上脚本，输出结果为：
```
$ javac Java8Tester.java 
$ java Java8Tester
Runoob
12
```

### JavaScript 中调用 Java

以下实例演示了如何在 JavaScript 中引用 Java 类：
```
var BigDecimal = Java.type('java.math.BigDecimal');

function calculate(amount, percentage) {

   var result = new BigDecimal(amount).multiply(
   new BigDecimal(percentage)).divide(new BigDecimal("100"), 2, BigDecimal.ROUND_HALF_EVEN);
   
   return result.toPlainString();
}

var result = calculate(568000000000000000023,13.9);
print(result);
```

我们使用 jjs 命令执行以上脚本，输出结果如下：
```
$ jjs sample.js
78952000000000002017.94
```
---
# 主要参考资源

## [tutorialspoint](https://www.tutorialspoint.com/java8/index.htm)

## [geeksforgeeks](https://www.geeksforgeeks.org/java-8-stream/)

## [ibm-developerworks](https://www.ibm.com/developerworks/cn/java/j-lo-jdk8newfeature/index.html)

## [Javacodegeeks](https://www.javacodegeeks.com/2014/05/java-8-features-tutorial.html)

## [Java 8 docs](https://docs.oracle.com/javase/8/)

## [Java 8 docs api](https://docs.oracle.com/javase/8/docs/api/overview-summary.html)