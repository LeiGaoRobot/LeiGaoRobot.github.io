---
title: Java9 版本特性
date: 2018-12-20 14:14:20
categories: java
tags: 
- java9
thumbnail: /img/article/javase.png
---

# 模块系统

## **What is Module system?**

Java 平台模块系统，也就是 Project Jigsaw，把模块化开发实践引入到了 Java 平台中。在引入了模块系统之后，JDK 被重新组织成 94 个模块。Java 应用可以通过新增的 jlink 工具，创建出只包含所依赖的 JDK 模块的自定义运行时镜像。这样可以极大的减少 Java 运行时环境的大小。这对于目前流行的不可变基础设施的实践来说，镜像的大小的减少可以节省很多存储空间和带宽资源 。

模块就是代码和数据的封装体。模块的代码被组织成多个包，每个包中包含Java类和接口；模块的数据则包括资源文件和其他静态信息。

模块化开发的实践在软件开发领域并不是一个新的概念。Java 开发社区已经使用这样的模块化实践有相当长的一段时间。主流的构建工具，包括 Apache Maven 和 Gradle 都支持把一个大的项目划分成若干个子项目。子项目之间通过不同的依赖关系组织在一起。每个子项目在构建之后都会产生对应的 JAR 文件。 在 Java9 中 ，已有的这些项目可以很容易的升级转换为 Java 9 模块 ，并保持原有的组织结构不变。

Java 9 模块的重要特征是在其工件（artifact）的根目录中包含了一个描述模块的 module-info.class 文 件。 工件的格式可以是传统的 JAR 文件或是 Java 9 新增的 JMOD 文件。这个文件由根目录中的源代码文件 module-info.java 编译而来。该模块声明文件可以描述模块的不同特征。模块声明文件中可以包含的内容如下：
+ 模块导出的包 - 使用 exports 可以声明模块对其他模块所导出的包。包中的 public 和 protected 类型，以及这些类型的 public 和 protected 成员可以被其他模块所访问。没有声明为导出的包相当于模块中的私有成员，不能被其他模块使用。
+ 模块的依赖关系 - 使用 requires 可以声明模块对其他模块的依赖关系。使用 requires transitive 可 以把一个模块依赖声明为传递的。传递的模块依赖可以被依赖当前模块的其他模块所读取。 如果一个模块所导出的类型的型构中包含了来自它所依赖的模块的类型，那么对该模块的依赖应该声明为传递的。
+ 服务的提供和使用 - 如果一个模块中包含了可以被 ServiceLocator 发现的服务接口的实现 ，需要使用 provides with 语句来声明具体的实现类 ；如果一个模块需要使用服务接口，可以使用 uses 语句来声明。


## **Usage**

模块声明示例
```
module com.mycompany.sample { 
    exports com.mycompany.sample; 
    requires com.mycompany.common; 
    provides com.mycompany.common.DemoService with
        com.mycompany.sample.DemoServiceImpl; 
}
```
在该声明文件中，模块 com.mycompany.sample 导出了 Java 包 com.mycompany.sample。
该模块依赖于模块 com.mycompany.sample 。
该模块也提供了服务接口 com.mycompany.common.DemoService 的实现类 c om.mycompany.sample.DemoServiceImpl 。

### Create Module Example

step 1

创建文件夹 src ,然后在该目录下再创建与模块名相同的文件夹 com\runoob\greetings

step 2

在src\com\runoob\greetings 目录下创建 module-info.java 文件，代码如下：
```
module com.runoob.greetings { }
```
module-info.java 用于创建模块。这一步我们创建了 com.runoob.greetings 模块

step 3

在模块中添加源代码文件，在目录src\com.runoob.greetings\com\runoob\greetings 中创建文件 Java9Tester.java，代码如下：
```
package com.runoob.greetings;

public class Java9Tester {
   public static void main(String[] args) {
      System.out.println("Hello World!");
   }
}
```

step 4

创建文件夹 mods，然后在该目录下创建 com\runoob\greetings 文件夹，编译模块到这个目录下：
```
$ javac -d mods/com.runoob.greetings 
   src/com.runoob.greetings/module-info.java 
   src/com.runoob.greetings/com/runoob/greetings/Java9Tester.java
```

step 5

执行模块，查看输出结果：
```
$ java --module-path mods -m com.runoob.greetings/com.runoob.greetings.Java9Tester
Hello World!
```
module-path 指定了模块所在的路径。

-m 指定主要模块。

---
# Jshell : REPL

## **What is Jshell?**

REPL(Read Eval Print Loop)意为交互式的编程环境。

jshell 是 Java 9 新增的一个实用工具。jshell 为 Java 增加了类似 NodeJS 和 Python 中的读取-求值-打印循环（ Read-Evaluation-Print Loop ） 。 在 jshell 中 可以直接 输入表达式并查看其执行结果。当需要测试一个方法的运行效果，或是快速的对表达式进行求值时，jshell 都非常实用。只需要通过 jshell 命令启动 jshell，然后直接输入表达式即可。每个表达式的结果会被自动保存下来 ，以数字编号作为引用，类似 $1 和$2 这样的名称 。可以在后续的表达式中引用之前语句的运行结果。 在 jshell 中 ，除了表达式之外，还可以创建 Java 类和方法。jshell 也有基本的代码完成功能。

## **Usage**

### 执行 JSHELL

JShell 允许你无需使用类或者方法包装来执行 Java 语句。它与 Python 的解释器类似，可以直接 输入表达式并查看其执行结果。
```
$ jshell
|  Welcome to JShell -- Version 9-ea
|  For an introduction type: /help intro
jshell>int add(int x, int y) { 
    ...> return x + y; 
    ...> }
 | created method add(int,int)
jshell> add(1, 2) 
$19 ==> 3
```
### 查看 JShell 命令

输入 /help 可以查看 JShell相关的命令：
```
jshell> /help
|  Type a Java language expression, statement, or declaration.
|  Or type one of the following commands:
|  /list [<name or id>|-all|-start]
|  list the source you have typed
|  /edit <name or id>
|  edit a source entry referenced by name or id
|  /drop <name or id>
|  delete a source entry referenced by name or id
|  /save [-all|-history|-start] <file>
|  Save snippet source to a file.
|  /open <file>
|  open a file as source input
|  /vars [<name or id>|-all|-start]
|  list the declared variables and their values
|  /methods [<name or id>|-all|-start]
|  list the declared methods and their signatures
|  /types [<name or id>|-all|-start]
|  list the declared types
|  /imports 
|  list the imported items
```
### 执行 JShell 命令

/imports 命令用于查看已导入的包：
```
jshell> /imports
|    import java.io.*
|    import java.math.*
|    import java.net.*
|    import java.nio.file.*
|    import java.util.*
|    import java.util.concurrent.*
|    import java.util.function.*
|    import java.util.prefs.*
|    import java.util.regex.*
|    import java.util.stream.*
jshell>
```

### JShell 执行计算

以下实例执行 JShell 简单计算：
```
jshell> 3+1
$1 ==> 4
jshell> 13%7
$2 ==> 6
jshell> $2
$2 ==> 6
jshell>
```

### JShell 创建与使用函数

创建一个函数 doubled() ，将传入的整型参数乘于 2 后返回：
```
jshell> int doubled(int i){ return i*2;}
|  created method doubled(int)
jshell> doubled(6)
$3 ==> 12
jshell>
```

### 退出 JShell

输入 /exit 命令退出 jshell：
```
jshell> /exit
| Goodbye 
```

---
# 改进的 API 和类

## Stream API

Java 9 改进的 Stream API 添加了一些便利的方法，使流处理更容易，并使用收集器编写复杂的查询。

Java 9 为 Stream 新增了几个方法：dropWhile, takeWhile, ofNullable。还有个 iterate 方法的新重载方法，可以让你提供一个 Predicate (判断条件)来指定什么时候结束迭代：

### takeWhile 方法

定义
```
default Stream<T> takeWhile(Predicate<? super T> predicate)
```

takeWhile() 方法使用一个断言作为参数，返回给定 Stream 的子集直到断言语句第一次返回 false。如果第一个值不满足断言条件，将返回一个空的 Stream。

takeWhile() 方法在有序的 Stream 中，takeWhile 返回从开头开始的尽量多的元素；在无序的 Stream 中，takeWhile 返回从开头开始的符合 Predicate 要求的元素的子集。

示例
```
import java.util.stream.Stream;
 
public class Tester {
   public static void main(String[] args) {
      Stream.of("a","b","c","","e","f").takeWhile(s->!s.isEmpty())
         .forEach(System.out::print);      
   } 
}
```

以上示例 takeWhile 方法在碰到空字符串时停止循环输出，执行输出结果为：

```
abc
```

### dropWhile 方法

定义
```
default Stream<T> dropWhile(Predicate<? super T> predicate)
```

dropWhile 方法和 takeWhile 作用相反的，使用一个断言作为参数，直到断言语句第一次返回 true 才返回给定 Stream 的子集。

示例
```
import java.util.stream.Stream;
 
public class Tester {
   public static void main(String[] args) {
      Stream.of("a","b","c","","e","f").dropWhile(s-> !s.isEmpty())
         .forEach(System.out::print);
   } 
}
```

以上示例 dropWhile 方法在碰到空字符串时开始循环输出，执行输出结果为：

```
ef
```

### iterate 方法

定义
```
static <T> Stream<T> iterate(T seed, Predicate<? super T> hasNext, UnaryOperator<T> next)
```

方法允许使用初始种子值创建顺序（可能是无限）流，并迭代应用指定的下一个方法。 当指定的 hasNext 的 predicate 返回 false 时，迭代停止。

示例
```
java.util.stream.IntStream;
 
public class Tester {
   public static void main(String[] args) {
      IntStream.iterate(3, x -> x < 10, x -> x + 3).forEach(System.out::println);
   } 
}
```

执行输出结果为：

```
3
6
9
```

### ofNullable 方法

定义
```
static <T> Stream<T> ofNullable(T t)
```

ofNullable 方法可以预防 NullPointerExceptions 异常， 可以通过检查流来避免 null 值。

如果指定元素为非 null，则获取一个元素并生成单个元素流，元素为 null 则返回一个空流。

示例
```
import java.util.stream.Stream;
 
public class Tester {
   public static void main(String[] args) {
      long count = Stream.ofNullable(100).count();
      System.out.println(count);
  
      count = Stream.ofNullable(null).count();
      System.out.println(count);
   } 
}
```

执行输出结果为：

```
1
0
```

## Optional 类

Optional 类在 Java 8 中引入，Optional 类的引入很好的解决空指针异常。在 java 9 中, 添加了三个方法来改进它的功能：stream(),ifPresentOrElse()和or()。

### stream() 方法

定义
```
public Stream<T> stream()
```

stream 方法的作用就是将 Optional 转为一个 Stream，如果该 Optional 中包含值，那么就返回包含这个值的 Stream，否则返回一个空的 Stream（Stream.empty()）。

示例
```
import java.util.Arrays;
import java.util.List;
import java.util.Optional;
import java.util.stream.Collectors;
import java.util.stream.Stream;
 
public class Tester {
public static void main(String[] args) {
   List<Optional<String>> list = Arrays.asList (
      Optional.empty(), 
      Optional.of("A"), 
      Optional.empty(), 
      Optional.of("B"));
 
      //filter the list based to print non-empty values
  
      //if optional is non-empty, get the value in stream, otherwise return empty
      List<String> filteredList = list.stream()
         .flatMap(o -> o.isPresent() ? Stream.of(o.get()) : Stream.empty())
         .collect(Collectors.toList());
 
      //Optional::stream method will return a stream of either one 
      //or zero element if data is present or not.
      List<String> filteredListJava9 = list.stream()
         .flatMap(Optional::stream)
         .collect(Collectors.toList());
 
      System.out.println(filteredList);
      System.out.println(filteredListJava9);
   }
}
```

执行输出结果为：
```
[A, B]
[A, B]
```

### ifPresentOrElse() 方法

定义
```
public void ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction)
```

ifPresentOrElse 方法的改进就是有了 else，接受两个参数 Consumer 和 Runnable。

ifPresentOrElse 方法的用途是，如果一个 Optional 包含值，则对其包含的值调用函数 action，即 action.accept(value)，这与 ifPresent 一致；与 ifPresent 方法的区别在于，ifPresentOrElse 还有第二个参数 emptyAction —— 如果 Optional 不包含值，那么 ifPresentOrElse 便会调用 emptyAction，即 emptyAction.run()。

示例
```
import java.util.Optional;
 
public class Tester {
   public static void main(String[] args) {
      Optional<Integer> optional = Optional.of(1);
 
      optional.ifPresentOrElse( x -> System.out.println("Value: " + x),() -> 
         System.out.println("Not Present."));
 
      optional = Optional.empty();
 
      optional.ifPresentOrElse( x -> System.out.println("Value: " + x),() -> 
         System.out.println("Not Present."));
   }  
}
```

执行输出结果为：
```
Value: 1
Not Present.
```

### or() 方法

定义
```
public Optional<T> or(Supplier<? extends Optional<? extends T>> supplier)
```

如果值存在，返回 Optional 指定的值，否则返回一个预设的值。

示例
```
import java.util.Optional;
import java.util.function.Supplier;
 
public class Tester {
   public static void main(String[] args) {
      Optional<String> optional1 = Optional.of("Mahesh");
      Supplier<Optional<String>> supplierString = () -> Optional.of("Not Present");
      optional1 = optional1.or( supplierString);
      optional1.ifPresent( x -> System.out.println("Value: " + x));
      optional1 = Optional.empty();    
      optional1 = optional1.or( supplierString);
      optional1.ifPresent( x -> System.out.println("Value: " + x));  
   }  
}
```

执行输出结果为：
```
Value: Mahesh
Value: Not Present
```

## 集合

在集合上，Java 9 增加 了 List.of()、Set.of()、Map.of() 和 M ap.ofEntries()等工厂方法来创建不可变集合。

除了更短和更好阅读之外，这些方法也可以避免您选择特定的集合实现。 事实上，从工厂方法返回已放入数个元素的集合实现是高度优化的。这是可能的，因为它们是不可变的：在创建后，继续添加元素到这些集合会导致 “UnsupportedOperationException” 。

示例
```
    List.of(); 
    List.of("Hello", "World"); 
    List.of(1, 2, 3);
    Set.of(); 
    Set.of("Hello", "World"); 
    Set.of(1, 2, 3);
    Map.of();
    Map.of("Hello", 1, "World", 2);
```

## 进程 API

Java 9 增加了 ProcessHandle 接口，可以对原生进程进行管理，尤其适合于管理长时间运行的进程。在使用 ProcessBuilder 来启动一个进程之后，可以通过 Process.toHandle()方法来得到一个 ProcessHandle 对象的实例。通过 ProcessHandle 可以获取到由 ProcessHandle.Info 表 示的进程的基本信息，如命令行参数、可执行文件路径和启动时间等。ProcessHandle 的 onExit()方法返回一个 CompletableFuture<ProcessHandle>对象，可以在进程结束时执行自定义的动作。

示例
```
    final ProcessBuilder processBuilder = new ProcessBuilder("top") 
        .inheritIO(); 
    final ProcessHandle processHandle = processBuilder.start().toHandle(); 
    processHandle.onExit().whenCompleteAsync((handle, throwable) -> { 
        if (throwable == null) { 
            System.out.println(handle.pid()); 
        } else { 
            throwable.printStackTrace(); 
        } 
    });
```

## I/O 流新特性

类 java.io.InputStream 中增加了新的方法来读取和复制 InputStream 中包含的数据。
+ readAllBytes - 读取 InputStream 中的所有剩余字节。
+ readNBytes - 从 InputStream 中读取指定数量的字节到数组中。
+ transferTo - 读取 InputStream 中的全部字节并写入到指定的 OutputStream 中 。

示例
```
public class TestInputStream {
    private InputStream inputStream; 
    private static final String CONTENT = "Hello World"; 
    @Before 
    public void setUp() throws Exception { 
        this.inputStream = 
            TestInputStream.class.getResourceAsStream("/input.txt"); 
    }
    @Test 
    public void testReadAllBytes() throws Exception { 
        final String content = new String(this.inputStream.readAllBytes()); 
        assertEquals(CONTENT, content); 
    } 
    @Test 
    public void testReadNBytes() throws Exception { 
        final byte[] data = new byte[5]; 
        this.inputStream.readNBytes(data, 0, 5); 
        assertEquals("Hello", new String(data)); 
    } 
    @Test 
    public void testTransferTo() throws Exception { 
        final ByteArrayOutputStream outputStream = new ByteArrayOutputStream(); 
        this.inputStream.transferTo(outputStream); 
        assertEquals(CONTENT, outputStream.toString()); 
    } 
}
```
ObjectInputFilter 可以对 ObjectInputStream 中 包含的内容进行检查，来确保其中包含的数据是合法的。可以使用 ObjectInputStream 的方法 setObjectInputFilter 来设置。ObjectInputFilter 在 进行检查时，可以检查如对象图的最大深度、对象引用的最大数量、输入流中的最大字节数和数组的最大长度等限制，也可以对包含的类的名称进行限制。

## 平台日志 API 和 服务

Java 9 允许为 JDK 和应用配置同样的日志实现。新增的 System.LoggerFinder 用来管理 JDK 使 用的日志记录器实现。JVM 在运行时只有一个系统范围的 LoggerFinder 实例。LoggerFinder 通 过服务查找机制来加载日志记录器实现。默认情况下，JDK 使用 java.logging 模块中的 java.util.logging 实现。通过 LoggerFinder 的 getLogger()方法就可以获取到表示日志记录器的 System.Logger 实现。应用同样可以使用 System.Logger 来记录日志。这样就保证了 JDK 和应用使用同样的日志实现。我们也可以通过添加自己的 System.LoggerFinder 实现来让 JDK 和应用使用 SLF4J 等其他日志记录框架。 代码清单 9 中给出了平台日志 API 的使用示例。

示例
```
public class Main { 
    private static final System.Logger LOGGER = System.getLogger("Main"); 

    public static void main(final String[] args) { 
        LOGGER.log(Level.INFO, "Run!");
    } 
}
```

## 改进应用安全性能

Java 9 新增了 4 个 SHA- 3 哈希算法，SHA3-224、SHA3-256、SHA3-384 和 S HA3-512。另外也增加了通过 java.security.SecureRandom 生成使用 DRBG 算法的强随机数。

示例
```
import org.apache.commons.codec.binary.Hex; 
public class SHA3 { 
    public static void main(final String[] args) throws NoSuchAlgorithmException { 
        final MessageDigest instance = MessageDigest.getInstance("SHA3-224"); 
        final byte[] digest = instance.digest("".getBytes()); 
        System.out.println(Hex.encodeHexString(digest)); 
    } 
}
```

## 改进的 try-with-resources

try-with-resources 是 JDK 7 中一个新的异常处理机制，它能够很容易地关闭在 try-catch 语句块中使用的资源。所谓的资源（resource）是指在程序完成后，必须关闭的对象。try-with-resources 语句确保了每个资源在语句结束时关闭。所有实现了 java.lang.AutoCloseable 接口（其中，它包括实现了 java.io.Closeable 的所有对象），可以使用作为资源。

try-with-resources 声明在 JDK 9 已得到改进。如果你已经有一个资源是 final 或等效于 final 变量,您可以在 try-with-resources 语句中使用该变量，而无需在 try-with-resources 语句中声明一个新变量。

java 7 示例
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.Reader;
import java.io.StringReader;
 
public class Tester {
   public static void main(String[] args) throws IOException {
      System.out.println(readData("test"));
   } 
   static String readData(String message) throws IOException {
      Reader inputString = new StringReader(message);
      BufferedReader br = new BufferedReader(inputString);
      try (BufferedReader br1 = br) {
         return br1.readLine();
      }
   }
}
```
以上实例中我们需要在 try 语句块中声明资源 br1，然后才能使用它。

在 Java 9 中，我们不需要声明资源 br1 就可以使用它，并得到相同的结果。
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.Reader;
import java.io.StringReader;
 
public class Tester {
   public static void main(String[] args) throws IOException {
      System.out.println(readData("test"));
   } 
   static String readData(String message) throws IOException {
      Reader inputString = new StringReader(message);
      BufferedReader br = new BufferedReader(inputString);
      try (br) {
         return br.readLine();
      }
   }
}
```
在处理必须关闭的资源时，使用try-with-resources语句替代try-finally语句。 生成的代码更简洁，更清晰，并且生成的异常更有用。 try-with-resources语句在编写必须关闭资源的代码时会更容易，也不会出错，而使用try-finally语句实际上是不可能的。

## 私有接口方法

在 Java 8之前，接口可以有常量变量和抽象方法。

我们不能在接口中提供方法实现。如果我们要提供抽象方法和非抽象方法（方法与实现）的组合，那么我们就得使用抽象类。

在 Java 8 接口引入了一些新功能——默认方法和静态方法。我们可以在Java SE 8的接口中编写方法实现，仅仅需要使用 default 关键字来定义它们。

在 Java 8 中，一个接口中能定义如下几种变量/方法：
+ 常量
+ 抽象方法
+ 默认方法
+ 静态方法

Java 9 不仅像 Java 8 一样支持接口默认方法，同时还支持私有方法。

在 Java 9 中，一个接口中能定义如下几种变量/方法：
+ 常量
+ 抽象方法
+ 默认方法
+ 静态方法
+ 私有方法
+ 私有静态方法

示例

java 7
```
interface Logging {
   String ORACLE = "Oracle_Database";
   String MYSQL = "MySql_Database";

   void logInfo(String message);

   void getConnection();
   void closeConnection();
}
final class LogMySql implements Logging {
   @Override
   public void logInfo(String message) {
      getConnection();
      System.out.println("Log Message : " + "INFO");
      closeConnection();
   }
   @Override
   public void getConnection() {
      System.out.println("Open Database connection");
   }
   @Override
   public void closeConnection() {
      System.out.println("Close Database connection");
   }
}
final class LogOracle implements Logging {
   @Override
   public void logInfo(String message) {
      getConnection();
      System.out.println("Log Message : " + "INFO");
      closeConnection();
   }
   @Override
   public void getConnection() {
      System.out.println("Open Database connection");
   }
   @Override
   public void closeConnection() {
      System.out.println("Close Database connection");
   }
}
```

java 8
```
interface Logging {
   String ORACLE = "Oracle_Database";
   String MYSQL = "MySql_Database";
 
   default void logInfo(String message) {
      getConnection();
      System.out.println("Log Message : " + "INFO");
      closeConnection();
   }
   default void logWarn(String message) {
      getConnection();
      System.out.println("Log Message : " + "WARN");
      closeConnection();
   }
   default void logError(String message) {
      getConnection();
      System.out.println("Log Message : " + "ERROR");
      closeConnection();
   }
   default void logFatal(String message) {
      getConnection();
      System.out.println("Log Message : " + "FATAL");
      closeConnection();
   }

   static void getConnection() {
      System.out.println("Open Database connection");
   }
   static void closeConnection() {
      System.out.println("Close Database connection");
   }
}
final class LogOracle implements Logging { }
final class LogMySql implements Logging { }
```

java 9
```
interface Logging {
   String ORACLE = "Oracle_Database";
   String MYSQL = "MySql_Database";
 
   private void log(String message, String prefix) {
      getConnection();
      System.out.println("Log Message : " + prefix);
      closeConnection();
   }
   default void logInfo(String message) {
      log(message, "INFO");
   }
   default void logWarn(String message) {
      log(message, "WARN");
   }
   default void logError(String message) {
      log(message, "ERROR");
   }
   default void logFatal(String message) {
      log(message, "FATAL");
   }
   
   private static void getConnection() {
      System.out.println("Open Database connection");
   }
   private static void closeConnection() {
      System.out.println("Close Database connection");
   }
}
final class LogOracle implements Logging { }
final class LogMySql implements Logging { }
```

## 改进的 @Deprecated 注解

在 Java SE 8 和更早版本上，@Deprecated 注解只是一个没有任何方法的标记类接口。它的作用是标记一个 Java API，可以是 calss，field，method，interface，constructor 等。

在 Java SE 9 中，Oracle 公司强化了 @Deprecated 注解，来提供更多有关废弃 API 的介绍信息，同时也提供一个工具来分析项目中的废弃 API 的静态使用情况。

注解 @Deprecated 可以标记 Java API 状态，可以是以下几种：
+ 使用它存在风险，可能导致错误
+ 可能在未来版本中不兼容
+ 可能在未来版本中删除
+ 一个更好和更高效的方案已经取代它。

Java 9 中注解增加了两个新元素：since 和 forRemoval。

+ since: 元素指定已注解的API元素已被弃用的版本。
+ forRemoval: 元素表示注解的 API 元素在将来的版本中被删除，应该迁移 API。

## Diamond Operator for Anonymous Inner Class

在Java7之前每次声明泛型变量的时必须左右两边都同时声明泛型：

在Java7中，对这一点进行了改进，就不必两边都要声明泛型，这种只适用<>标记的操作，称之为钻石操作符Diamond Operator。

但是Java7中钻石操作符不允许在匿名类上使用：

在 Java 8 中，Oracle 公司发现在 Diamond 操作器和匿名内部类的使用中存在一些局限性，后来修复了这些问题并准备将其作为 Java 9 的一部分发布出去。在 java 9 中， 它可以与匿名的内部类一起使用，从而提高代码的可读性。

 Java 7 之前的代码：
 ```
   List<String> list = new ArrayList<String>();
   Set<String> set = new HashSet<String>();
   Map<String, List<String>> map = new HashMap<String, List<String>>();
 ```

 Java 9 之前的代码：
 ```
   List<String> list = new ArrayList<>();
   Set<String> set = new HashSet<>();
   Map<String, List<String>> map = new HashMap<>();
 ```

 在 Java 9 中，我们可以在匿名类中使用 <> 操作符，如下所示：
 ```
List<String> list = new ArrayList<>() {
    @Override
    public int size() {
        return super.size();
    }

    @Override
    public String toString() {
        return super.toString();
    }
};
        
Set<String> set = new HashSet<>() {
    @Override
    public int size() {
        return super.size();
    }
    
    @Override
    public String toString() {
        return super.toString();
    }
};

Map<String, List<String>> map = new HashMap<>() {
    @Override
    public int size() {
        return super.size();
    }

    @Override
    public String toString() {
        return super.toString();
    }
};
 ```

## 多分辨率图像 API

在 Java 9 中，Oracle 公司将引入一个新的 Мulti-Resolution Image API。这个 API 中比较重要的接口是 MultiResolutionImage，在 java.awt.image 包下可获取到。

MultiResolutionImage 封装不同高度和宽度图片（不同解决方案）到一个集合中，并允许我们按需查询使用。

以下是MultiResolutionImage的主要操作方法：
+ Image getResolutionVariant(double destImageWidth, double destImageHeight) − 获取特定分辨率的图像变体-表示一张已知分辨率单位为DPI的特定尺寸大小的逻辑图像，并且这张图像是最佳的变体。
+ List<Image> getResolutionVariants() − 返回可读的分辨率的图像变体列表。

示例
```
import java.io.IOException;
import java.net.URL;
import java.net.MalformedURLException;
import java.util.ArrayList;
import java.util.List;
import java.awt.Image;
import java.awt.image.MultiResolutionImage;
import java.awt.image.BaseMultiResolutionImage;
 
import javax.imageio.ImageIO;
 
public class Tester {
   public static void main(String[] args) throws IOException, MalformedURLException {
 
      List<String> imgUrls = List.of("http://www.runoob.com/wp-content/themes/runoob/assets/img/runoob-logo@2x.png",
         "http://www.runoob.com/wp-content/themes/runoob/assets/img/runoob-logo.png",
         "http://www.runoob.com/wp-content/themes/runoob/assets/images/qrcode.png");
 
      List<Image> images = new ArrayList<>();
 
      for (String url : imgUrls) {
         images.add(ImageIO.read(new URL(url)));
      }
 
      // 读取所有图片
      MultiResolutionImage multiResolutionImage = 
         new BaseMultiResolutionImage(images.toArray(new Image[0]));
 
      // 获取图片的所有分辨率
      List<Image> variants = multiResolutionImage.getResolutionVariants();
 
      System.out.println("Total number of images: " + variants.size());
 
      for (Image img : variants) {
         System.out.println(img);
      }
 
      // 根据不同尺寸获取对应的图像分辨率
      Image variant1 = multiResolutionImage.getResolutionVariant(156, 45);
      System.out.printf("\nImage for destination[%d,%d]: [%d,%d]", 
         156, 45, variant1.getWidth(null), variant1.getHeight(null));
 
      Image variant2 = multiResolutionImage.getResolutionVariant(311, 89);
      System.out.printf("\nImage for destination[%d,%d]: [%d,%d]", 311, 89, 
         variant2.getWidth(null), variant2.getHeight(null));
 
      Image variant3 = multiResolutionImage.getResolutionVariant(622, 178);
      System.out.printf("\nImage for destination[%d,%d]: [%d,%d]", 622, 178, 
         variant3.getWidth(null), variant3.getHeight(null));
 
      Image variant4 = multiResolutionImage.getResolutionVariant(300, 300);
      System.out.printf("\nImage for destination[%d,%d]: [%d,%d]", 300, 300, 
         variant4.getWidth(null), variant4.getHeight(null));
   }  
}
```


---
# 响应式流 （ Reactive Streams ）


## **What is Reactive Streams?**

>流是由生产者生产并由一个或多个消费者消费的元素（item）的序列。 这种生产者——消费者模型也被称为source/sink模型或发布者——订阅者（publisher-subscriber ）模型。 在本章中，将其称为发布者订阅者模型。<br/>有几种流处理机制，其中pull模型和push模型是最常见的。 在push模型中，发布者将元素推送给订阅者。 在pull模式中，订阅者将元素推送给发布者。 发布者和订阅者都以同样的速率工作，这是一个理想的情况，这些模式非常有效。 我们会考虑一些情况，如果他们不按同样的速率工作，这种情况下涉及的问题以及对应的解决办法。<br/>当发布者比订阅者快的时候，后者必须有一个无边界缓冲区来保存快速传入的元素，或者它必须丢弃它无法处理的元素。另一个解决方案是使用一种称为背压（backpressure）的策略，其中订阅者告诉发布者减慢速率并保持元素，直到订阅者准备好处理更多的元素。 使用背压可确保更快的发布者不会压制较慢的订阅者。 使用背压可能要求发布者拥有无限制的缓冲区，如果它要一直生成和保存元素。 发布者可以实现有界缓冲区来保存有限数量的元素，如果缓冲区已满，可以选择放弃它们。 可以使用另一策略，其中发布者将发布元素重新发送到订阅者，这些元素发布时订阅者不能接受。<br/>订阅者在请求发布者的元素并且元素不可用时，该做什么？ 在同步请求中订阅者户必须等待，无限期地，直到有元素可用。 如果发布者同步地向订阅者发送元素，并且订阅者同步处理它们，则发布者必须阻塞直到数据处理完成。 解决方案是在两端进行异步处理，订阅者可以在从发布者请求元素之后继续处理其他任务。 当更多的元素准备就绪时，发布者将它们异步发送给订阅者。

响应式流从2013年开始，作为提供非阻塞背压的异步流处理标准的倡议。 它旨在解决处理元素流的问题——如何将元素流从发布者传递到订阅者，而不需要发布者阻塞，或订阅者有无限制的缓冲区或丢弃。

响应式流模型非常简单——订阅者向发布者发送多个元素的异步请求。 发布者向订阅者异步发送多个或稍少的元素。

响应式编程的思想最近得到了广泛的流行。 在 Java 平台上有流行的响应式库 RxJava 和 Reactor。响应式流规范的出发点是提供一个带非阻塞负压（ non-blocking backpressure ） 的异步流处理规范。响应式流规范的核心接口已经添加到了 Java9 中的 java.util.concurrent.Flow 类中。

Flow 中包含了 Flow.Publisher、Flow.Subscriber、Flow.Subscription 和 Flow.Processor 等 4 个核心接口。Java 9 还提供了 SubmissionPublisher 作为 Flow.Publisher 的一个实现。RxJava 2 和 Reactor 都可以很方便的 与 Flow 类的核心接口进行互操作。

有关响应式流的更多信息，请访问<a>http://www.reactive-streams.org/</a>。 

---
# 句柄

## 变量句柄

变量句柄是一个变量或一组变量的引用，包括静态域，非静态域，数组元素和堆外数据结构中的组成部分等。变量句柄的含义类似于已有的方法句柄。变量句柄只是对创建的变量的类型引用，以便在不同的访问模式下提供对变量的读写访问。

变量句柄由 Java 类 java.lang.invoke.VarHandle 来表示。可以使用类 java.lang.invoke.MethodHandles.Lookup 中的静态工厂方法来创建 VarHandle 对象。varHandle由两个重要部分组成 - 变量类型和坐标列表。变量类型表示varHandle给出内存引用的变量类型，而坐标列表有助于定位其引用由varHandle给出的变量。通过变量句柄，可以在变量上进行各种操作。这些操作称为访问模式。不同的访问模式尤其在内存排序上的不同语义。目前一共有 31 种 访问模式，而每种访问模式都 在 VarHandle 中 有对应的方法。这些方法可以对变量进行读取、写入、原子更新、数值原子更新和按位原子操作等。VarHandle 还可以用来访问数组中的单个元素，以及把 byte[]数组 和 ByteBuffer 当成是不同原始类型的数组来访问。从本质上讲，VarHandle对象一旦创建就无法修改。

Variable Handle的方法分为五种访问模式：
+ 读访问模式 - 这可用于获取变量的值。get()，getVolatile()，getAcquire()和getOpaque()是一些支持读访问的方法。
+ 写访问模式 - 这可用于设置变量的值。set()，setVolatile()，setRelease()和setOpaque()是一些支持写访问的方法。
+ 原子更新加速模式 - 这可用于在比较当前值和新值之后以原子方式更改变量的值。属于此类访问模式的一些方法是：compareAndSet，compareAndExchangeAcquire，compareAndExchange，compareAndExchangeRelease，getAndSet，getAndSetAcquire，getAndSetRelease等。
+ 数值原子更新访问模式 - 这可以用于我们想要通过添加原子设置值的情况。getAndAdd，getAndAddAcquire，getAndAddRelease等方法属于此类别。
+ 按位原子更新访问模式 - 这可用于在设置值之前检索并执行按位OR，AND或XOR。属于此类别的一些方法是：getAndBitwiseOr，getAndBitwiseOrAcquire，getAndBitwiseOrRelease，getAndBitwiseAnd，getAndBitwiseAndAcquire，getAndBitwiseAndRelease，getAndBitwiseXor，getAndBitwiseXorAcquire，getAndBitwiseXorRelease等。

示例
```
public class HandleTarget { 
    public int count = 1; 
} 
public class VarHandleTest {
    private HandleTarget handleTarget = new HandleTarget(); 
    private VarHandle varHandle; 
    @Before 
    public void setUp() throws Exception { 
        this.handleTarget = new HandleTarget(); 
        this.varHandle = MethodHandles 
            .lookup() 
            .findVarHandle(HandleTarget.class, "count", int.class); 
    } 
    @Test 
    public void testGet() throws Exception { 
        assertEquals(1, this.varHandle.get(this.handleTarget)); 
        assertEquals(1, this.varHandle.getVolatile(this.handleTarget)); 
        assertEquals(1, this.varHandle.getOpaque(this.handleTarget)); 
        assertEquals(1, this.varHandle.getAcquire(this.handleTarget)); 
    } 
}
```

## 改进方法句柄

类 java.lang.invoke.MethodHandles 增加了更多的静态方法来创建不同类型的方法句柄。

+ arrayConstructor - 创建指定类型的数组。
+ arrayLength - 获取指定类型的数组的大小。
+ varHandleInvoker 和 varHandleExactInvoker - 调用 VarHandle 中的访问模式方法。
+ zero - 返回一个类型的默认值。
+ empty - 返回 MethodType 的返回值类型的默认值。
+ loop、countedLoop、iteratedLoop、whileLoop 和 doWhileLoop - 创建不同类型的循环，包括 for 循环、while 循环 和 do-while 循环。
+ tryFinally - 把对方法句柄的调用封装在 try-finally 语句中。

示例
```
public class IteratedLoopTest { 
    static int body(final int sum, final String value) { 
        return sum + value.length(); 
    } 
    @Test 
    public void testIteratedLoop() throws Throwable { 
        final MethodHandle iterator = MethodHandles.constant( 
            Iterator.class, 
            List.of("a", "bc", "def").iterator()); 
        final MethodHandle init = MethodHandles.zero(int.class); 
        final MethodHandle body = MethodHandles 
            .lookup() 
            .findStatic( 
                IteratedLoopTest.class, 
                "body", 
                MethodType.methodType( 
                    int.class, 
                    int.class, 
                    String.class)); 
        final MethodHandle iteratedLoop = MethodHandles 
            .iteratedLoop(iterator, init, body); 
        assertEquals(6, iteratedLoop.invoke()); 
    } 
}
```

---
# 并发的改进

Java 8 引入了 CompletableFuture<T> 类，可能是 java.util.concurrent.Future<T> 明确的完成版（设置了它的值和状态），也可能被用作java.util.concurrent.CompleteStage 。支持 future 完成时触发一些依赖的函数和动作。Java 9 引入了一些CompletableFuture 的改进，增加了几个新的方法。

对原 CompletableFuture 做了改进：
+ 支持 delays 和 timeouts
+ 提升了对子类化的支持
+ 新的工厂方法

增加的方法：
+ completeAsync 使用一个异步任务来获取结果并完成该 CompletableFuture。
+ orTimeout 在 CompletableFuture 没有在给定的超时时间之前完成，使用 TimeoutException 异常来完成 CompletableFuture。
+ completeOnTimeout 与 orTimeout 类似，只不过它在超时时使用给定的值来完成 CompletableFuture。
+ 新的 Thread.onSpinWait 方法在当前线程需要使用忙循环来等待时，可以提高等待的效率。


## 支持 delays 和 timeouts

定义

```
public CompletableFuture<T> orTimeout(long timeout, TimeUnit unit)
```

如果没有在给定的 timeout 内完成，就以 java.util.concurrent.TimeoutException 完成这个 CompletableFutrue，并返回这个 CompletableFutrue。

定义

```
public CompletableFuture<T> completeOnTimeout(T value, long timeout, TimeUnit unit)
```

在 timeout（单位在 java.util.concurrent.Timeunits units 中，比如 MILLISECONDS ）前以给定的 value 完成这个 CompletableFutrue。返回这个 CompletableFutrue。

## 增强了对子类化的支持

做了许多改进使得 CompletableFuture 可以被更简单的继承。比如，你也许想重写新的 public Executor defaultExecutor() 方法来代替默认的 executor。

另一个新的使子类化更容易的方法是：

```
public <U> CompletableFuture<U> newIncompleteFuture()
```

## 新的工厂方法

ava 8引入了 \<U> CompletableFuture\<U> completedFuture(U value) 工厂方法来返回一个已经以给定 value 完成了的 CompletableFuture。Java 9以一个新的 \<U> CompletableFuture\<U> failedFuture(Throwable ex) 来补充了这个方法，可以返回一个以给定异常完成的 CompletableFuture。

除此以外，Java 9 引入了下面这对 stage-oriented 工厂方法，返回完成的或异常完成的 completion stages:
+ \<U> CompletionStage\<U> completedStage(U value): 返回一个新的以指定 value 完成的CompletionStage ，并且只支持 CompletionStage 里的接口。
+ \<U> CompletionStage\<U> failedStage(Throwable ex): 返回一个新的以指定异常完成的CompletionStage ，并且只支持 CompletionStage 里的接口。

--- 
# 多版本兼容 jar 包

多版本兼容 JAR 功能能让你创建仅在特定版本的 Java 环境中运行库程序时选择使用的 class 版本。

通过 --release 参数指定编译版本。

具体的变化就是 META-INF 目录下 MANIFEST.MF 文件新增了一个属性：*Multi-Release: true*

META-INF 目录下还新增了一个 versions 目录，如果是要支持 java9，则在 versions 目录下有 9 的目录。
```
multirelease.jar
├── META-INF
│   └── versions
│       └── 9
│           └── multirelease
│               └── Helper.class
├── multirelease
    ├── Helper.class
    └── Main.class
```
---
# Javadoc

javadoc 工具可以生成 Java 文档， Java 9 的 javadoc 的输出现在符合兼容 HTML5 标准。

Java 9 之前的旧版本文档
```
/**
  * @author MahKumar
  * @version 0.1
*/
public class Tester {
   /**
      * Default method to be run to print 
      * <p>Hello world</p>
      * @param args command line arguments
   */
   public static void main(String []args) {
      System.out.println("Hello World");
   }
}
```

使用 jdk 7 的 javadoc 生成文档：
```
$ javadoc -d C:/JAVA Tester.java
Loading source file tester.java...
Constructing Javadoc information...
Standard Doclet version 1.7.0_21
Building tree for all the packages and classes...
Generating C:\JAVA\Tester.html...
Generating C:\JAVA\package-frame.html...
Generating C:\JAVA\package-summary.html...
Generating C:\JAVA\package-tree.html...
Generating C:\JAVA\constant-values.html...
Building index for all the packages and classes...
Generating C:\JAVA\overview-tree.html...
Generating C:\JAVA\index-all.html...
Generating C:\JAVA\deprecated-list.html...
Building index for all classes...
Generating C:\JAVA\allclasses-frame.html...
Generating C:\JAVA\allclasses-noframe.html...
Generating C:\JAVA\index.html...
Generating C:\JAVA\help-doc.html...
```

**Java 9 生成的文档兼容 HTML5 标准**

使用 jdk 9 javadoc 命令中的 -html5 参数可以让生成的文档支持 HTML5 标准：
```
C:\JAVA> javadoc -d C:/JAVA -html5 Tester.java
Loading source file Tester.java...
Constructing Javadoc information...
Standard Doclet version 9.0.1
Building tree for all the packages and classes...
Generating C:\JAVA\Tester.html...
Generating C:\JAVA\package-frame.html...
Generating C:\JAVA\package-summary.html...
Generating C:\JAVA\package-tree.html...
Generating C:\JAVA\constant-values.html...
Building index for all the packages and classes...
Generating C:\JAVA\overview-tree.html...
Generating C:\JAVA\index-all.html...
Generating C:\JAVA\deprecated-list.html...
Building index for all classes...
Generating C:\JAVA\allclasses-frame.html...
Generating C:\JAVA\allclasses-frame.html...
Generating C:\JAVA\allclasses-noframe.html...
Generating C:\JAVA\allclasses-noframe.html...
Generating C:\JAVA\index.html...
Generating C:\JAVA\help-doc.html...
```

---
# HTTP/2 Client

## **What is HTTP/2?**
>HTTP/2（超文本传输协议第2版，最初命名为HTTP 2.0），简称为h2（基于TLS/1.2或以上版本的加密连接）或h2c（非加密连接），是HTTP协议的的第二个主要版本，使用于万维网。<br/>
>HTTP/2是HTTP协议自1999年HTTP 1.1发布后的首个更新，主要基于SPDY协议。它由互联网工程任务组（IETF）的Hypertext Transfer Protocol Bis（httpbis）工作小组进行开发。该组织于2014年12月将HTTP/2标准提议递交至IESG进行讨论，于2015年2月17日被批准。<br/>
>HTTP/2标准于2015年5月以RFC 7540正式发表。HTTP/2的标准化工作由Chrome、Opera、Firefox、Internet Explorer 11、Safari、Amazon Silk及Edge等浏览器提供支持。<br/>
>多数主流浏览器已经在2015年底支持了该协议。此外，根据W3Techs的数据，在2017年5月，在排名前一千万的网站中，有13.7%支持了HTTP/2。[Wiki](https://zh.wikipedia.org/wiki/HTTP/2)

在 Java 9 中，Oracle 公司将发布新的 HTTP 2 Client API 来支持 HTTP/2 协议和 WebSocket 特性。现有的 HTTP Client API 存在很多问题（如支持 HTTP/1.1 协议但是不支持 HTTP/2 协议和 WebSocket，仅仅作用在 Blocking 模式中，并存在大量性能问题），他们正在被使用新的 HTTP 客户端的 HttpURLConnection API 所替代。

Oracle 公司准备在 “java.net.http” 包下引入新的 HTTP 2 Client API。它将同时支持 HTTP/1.1 和 HTTP/2 协议，也同时支持同步（Blocking Mode）和异步模式，支持 WebSocket API 使用中的异步模式。

## **Usage**

注意：新的 HttpClient API 在 Java 9 中以所谓的孵化器模块交付。也就是说，这套 API 不能保证 100% 完成。不过你可以在 Java 9 中开始使用这套 API：
```
   HttpClient client = HttpClient.newHttpClient();
   HttpRequest req =
      HttpRequest.newBuilder(URI.create("http://www.google.com"))
               .header("User-Agent","Java")
               .GET()
               .build();
   HttpResponse<String> resp = client.send(req, HttpResponse.BodyHandler.asString());
```

HttpResponse<String> resp = client.send(req, HttpResponse.BodyHandler.asString());
除了这个简单的请求/响应模型之外，HttpClient 还提供了新的 API 来处理 HTTP/2 的特性，比如流和服务端推送。

# 统一 JVM 日志

Java 9 中 ，JVM 有了统一的日志记录系统，可以使用新的命令行选项-Xlog 来控制 JVM 上 所有组件的日志记录。该日志记录系统可以设置输出的日志消息的标签、级别、修饰符和输出目标等。Java 9 移除了在 Java 8 中 被废弃的垃圾回收器配置组合，同时 把 G1 设为默认的垃圾回收器实现。另外，CMS 垃圾回收器已经被声明为废弃。Java 9 也增加了很多可以通过 jcmd 调用的诊断命令。

# 主要参考资源

## [tutorialspoint](https://www.tutorialspoint.com/java9/index.htm)

## [ibm-developerworks](https://www.ibm.com/developerworks/cn/java/the-new-features-of-Java-9/index.html)

## [journaldev](https://www.journaldev.com/13121/java-9-features-with-examples)

## [Java 9 docs](https://docs.oracle.com/javase/9/)

## [Java 9 docs api](https://docs.oracle.com/javase/9/docs/api/overview-summary.html)