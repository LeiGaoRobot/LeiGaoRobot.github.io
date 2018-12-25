---
title: Java10 版本特性
date: 2018-12-25 15:37:37
categories: java
tags:
- java10
---

作为当今使用最广泛的编程语言之一的 Java 在 2018 年 3 月 21 日发布了第十个大版本。为了更快地迭代、更好地跟进社区反馈，Java 语言版本发布周期调整为每隔 6 个月发布一次。Java 10 是这一新规则之后，采用新发布周期的第一个大版本。

# 长期支持模型

从2017年开始，甲骨文和Java社区宣布将向Java推出新的6个月节奏。它转向了Oracle Java SE产品的长期支持（LTS）模型。

LTS版本的产品将提供Oracle的主要和持续支持，并将每3年定位一次。

## Oracle JDK vs Open JDK

为了更加开发人员友好，Oracle和Java社区现在将OpenJDK二进制文件作为主要JDK推进。从早期开始，这是一个很大的缓解，其中JDK二进制文件是适当的并且由Oracle授权，Oracle在重新分发方面有各种限制。然而，Oracle将继续生产他们的JDK，但仅限于长期支持版本。这是一个向更多云和容器友好的方向，因为开放的JDK二进制文件可以作为容器的一部分进行分发。

Open JDK二进制文件将每6个月发布一次，而Oracle JDK二进制文件将每3年发布一次（LTS版本）。

Java 9和10是非LTS版本。将于2018年9月发布的Java 11将是LTS版本。

## JCP

JCP（Java Community Process）成立于1998年，是使有兴趣的各方参与定义Java的特征和未来版本的正式过程。

JCP使用JSR（Java规范请求，Java Specification Requests）作为正式规范文档，描述被提议加入到Java体系中的的规范和技术。

JSR变为final状态前需要正式的公开审查，并由JCP Executive Committee投票决定。最终的JSR会提供一个参考实现，它是免费而且公开源代码的；还有一个验证是否符合API规范的Technology Compatibility Kit。

[详情](https://zh.wikipedia.org/wiki/JCP)

## JEP

JEP(JDK Enhancement Proposal，改善提议) 是JDK发布项目及相关工作的长期路线图。

[详情](http://openjdk.java.net/jeps/1)

# 局部变量类型推断(JEP 286)

## **What is Local-Variable Type Inference?**

局部变量类型推断(Local-Variable Type Inference)是 Java 10 中最值得开发人员注意的新特性，这是 Java 语言开发人员为了简化 Java 应用程序的编写而进行的又一重要改进。

这一新功能将为 Java 增加一些新语法，允许开发人员省略通常不必要的局部变量类型初始化声明。新的语法将减少 Java 代码的冗长度，同时保持对静态类型安全性的承诺。局部变量类型推断主要是向 Java 语法中引入在其他语言（比如 C#、JavaScript）中很常见的保留类型名称 var。但需要特别注意的是：var 不是一个关键字，而是一个保留字。只要编译器可以推断此种类型，开发人员不再需要专门声明一个局部变量的类型，也就是可以随意定义变量而不必指定变量的类型。这种改进对于链式表达式来说，也会很方便。

虽然变量类型的推断在 Java 中不是一个崭新的概念，但在局部变量中确是很大的一个改进。说到变量类型推断，从 Java 5 中引进泛型，到 Java 7 的 <> 操作符允许不绑定类型而初始化 List，再到 Java 8 中的 Lambda 表达式，再到现在 Java 10 中引入的局部变量类型推断，Java 类型推断正大刀阔斧地向前进步、发展。

但这种 var 变量类型推断的使用也有局限性，仅局限于具有初始化器的局部变量、增强型 for 循环中的索引变量以及在传统 for 循环中声明的局部变量，而不能用于推断方法的参数类型，不能用于构造函数参数类型推断，不能用于推断方法返回类型，也不能用于字段类型推断，同时还不能用于捕获表达式（或任何其他类型的变量声明）。

不过对于开发者而言，变量类型显式声明会提供更加全面的程序语言信息，对于理解和维护代码有很大的帮助。Java 10 中新引入的局部变量类型推断能够帮助我们快速编写更加简洁的代码，但是局部变量类型推断的保留字 var 的使用势必会引起变量类型可视化缺失，并不是任何时候使用 var 都能容易、清晰的分辨出变量的类型。一旦 var 被广泛运用，开发者在没有 IDE 的支持下阅读代码，势必会对理解程序的执行流程带来一定的困难。所以还是建议尽量显式定义变量类型，在保持代码简洁的同时，也需要兼顾程序的易读性、可维护性。

局部变量类型推断只能在以下场景中使用：
+ 仅限于具有初始化程序的本地变量
+ 增强的for循环或索引的索引
+ 本地声明为for循环

详细请看相关JEP

[JEP 286](http://openjdk.java.net/jeps/286)

## **Usage**

示例
```
    var numbers = List.of(1, 2, 3, 4, 5); // inferred value ArrayList<String>
    // Index of Enhanced For Loop
    for (var number : numbers) {
        System.out.println(number);
    }
    // Local variable declared in a loop
    for (var i = 0; i < numbers.size(); i++) {
        System.out.println(numbers.get(i));
    }
    var stream = numbers.stream();// Stream<int>
```

具体用法实例

[Java 10: Local Variable Type Inference](https://www.journaldev.com/19871/java-10-local-variable-type-inference)

# 整合 JDK 代码仓库(JEP 296)

## **What is Consolidate the JDK Forest into a Single Repository?**

为了简化开发流程，Java 10 中会将多个代码库合并到一个代码仓库中。

在已发布的 Java 版本中，JDK 的整套代码根据不同功能已被分别存储在多个 Mercurial 存储库，这八个 Mercurial 存储库分别是：root、corba、hotspot、jaxp、jaxws、jdk、langtools、nashorn。

虽然以上八个存储库之间相互独立以保持各组件代码清晰分离，但同时管理这些存储库存在许多缺点，并且无法进行相关联源代码的管理操作。其中最重要的一点是，涉及多个存储库的变更集无法进行原子提交 （atomic commit）。例如，如果一个 bug 修复时需要对独立存储两个不同代码库的代码进行更改，那么必须创建两个提交：每个存储库中各一个。这种不连续性很容易降低项目和源代码管理工具的可跟踪性和加大复杂性。特别是，不可能跨越相互依赖的变更集的存储库执行原子提交这种多次跨仓库的变化是常见现象。

为了解决这个问题，JDK 10 中将所有现有存储库合并到一个 Mercurial 存储库中。这种合并的一个次生效应是，单一的 Mercurial 存储库比现有的八个存储库要更容易地被镜像(作为一个 Git 存储库)，并且使得跨越相互依赖的变更集的存储库运行原子提交成为可能，从而简化开发和管理过程。虽然在整合过程中，外部开发人员有一些阻力，但是 JDK 开发团队已经使这一更改成为 JDK 10 的一部分。

详细请看相关JEP

[JEP 296](http://openjdk.java.net/jeps/296)

# 统一的垃圾回收接口(JEP 304)

## **What is Garbage Collector Interface?**

在当前的 Java 结构中，组成垃圾回收器（GC）实现的组件分散在代码库的各个部分。尽管这些惯例对于使用 GC 计划的 JDK 开发者来说比较熟悉，但对新的开发人员来说，对于在哪里查找特定 GC 的源代码，或者实现一个新的垃圾收集器常常会感到困惑。更重要的是，随着 Java modules 的出现，我们希望在构建过程中排除不需要的 GC，但是当前 GC 接口的横向结构会给排除、定位问题带来困难。

为解决此问题，需要整合并清理 GC 接口，以便更容易地实现新的 GC，并更好地维护现有的 GC。Java 10 中，hotspot/gc 代码实现方面，引入一个干净的 GC 接口，改进不同 GC 源代码的隔离性，多个 GC 之间共享的实现细节代码应该存在于辅助类中。这种方式提供了足够的灵活性来实现全新 GC 接口，同时允许以混合搭配方式重复使用现有代码，并且能够保持代码更加干净、整洁，便于排查收集器问题。

此更改为内部GC代码提供了更好的模块化。它将来有助于在不更改现有代码库的情况下添加新GC，也有助于删除或管理以前的GC。

详细请看相关JEP

[JEP 304](http://openjdk.java.net/jeps/304)

# 并行全垃圾回收器 G1(JEP 307)

## **What is Parallel Full GC for G1?**

G1 是设计来作为一种低延时的垃圾回收器（但是如果它跟不上旧的堆碎片产生的提升速率的话，将仍然采用完整压缩集合）。在 JDK9 之前，默认的收集器是并行，吞吐，收集器。为了减少在使用默认的收集器的应用性能配置文件的差异，G1 现在有一个并行完整收集机制。

大家如果接触过 Java 性能调优工作，应该会知道，调优的最终目标是通过参数设置来达到快速、低延时的内存垃圾回收以提高应用吞吐量，尽可能的避免因内存回收不及时而触发的完整 GC（Full GC 会带来应用出现卡顿）。

G1 垃圾回收器是 Java 9 中 Hotspot 的默认垃圾回收器，是以一种低延时的垃圾回收器来设计的，旨在避免进行 Full GC，但是当并发收集无法快速回收内存时，会触发垃圾回收器回退进行 Full GC。之前 Java 版本中的 G1 垃圾回收器执行 GC 时采用的是基于单线程标记扫描压缩算法（mark-sweep-compact）。为了最大限度地减少 Full GC 造成的应用停顿的影响，Java 10 中将为 G1 引入多线程并行 GC，同时会使用与年轻代回收和混合回收相同的并行工作线程数量，从而减少了 Full GC 的发生，以带来更好的性能提升、更大的吞吐量。

Java 10 中将采用并行化 mark-sweep-compact 算法，并使用与年轻代回收和混合回收相同数量的线程。具体并行 GC 线程数量可以通过：-XX：ParallelGCThreads 参数来调节，但这也会影响用于年轻代和混合收集的工作线程数。

详细请看相关JEP

[JEP 307](http://openjdk.java.net/jeps/307)

# 应用程序类数据共享(JEP 310)

## **What is Application Class-Data Sharing?**

在 Java 5 中就已经引入了类数据共享机制 (Class Data Sharing，简称 CDS)，允许将一组类预处理为共享归档文件，以便在运行时能够进行内存映射以减少 Java 程序的启动时间，当多个 Java 虚拟机（JVM）共享相同的归档文件时，还可以减少动态内存的占用量，同时减少多个虚拟机在同一个物理或虚拟的机器上运行时的资源占用。简单来说，Java 安装程序会把 rt.jar 中的核心类提前转化成内部表示，转储到一个共享存档（shared archive）中。多个 Java 进程（或者说 JVM 实例）可以共享这部分数据。为改善启动和占用空间，Java 10 在现有的 CDS 功能基础上再次拓展，以允许应用类放置在共享存档中。

CDS 特性在原来的 bootstrap 类基础之上，扩展加入了应用类的 CDS (Application Class-Data Sharing) 支持。

其原理为：在启动时记录加载类的过程，写入到文本文件中，再次启动时直接读取此启动文本并加载。设想如果应用环境没有大的变化，启动速度就会得到提升。

可以想像为类似于操作系统的休眠过程，合上电脑时把当前应用环境写入磁盘，再次使用时就可以快速恢复环境。

对大型企业应用程序的内存使用情况的分析表明，此类应用程序通常会将数以万计的类加载到应用程序类加载器中，如果能够将 AppCDS 应用于这些应用，将为每个 JVM 进程节省数十乃至数百兆字节的内存。另外对于云平台上的微服务分析表明，许多服务器在启动时会加载数千个应用程序类，AppCDS 可以让这些服务快速启动并改善整个系统响应时间。

简单来说：应用程序数据共享，事通过跨进程共享通用类的元数据，减少空间占用及启动时长。

应用程序数据共享主要是为4个目的：
+ 通过在不同的Java进程间共享公共类元数据来减少占用空间。
+ 改善启动时间。
+ 扩展CDS以允许来自JDK运行时映像文件（比如，$JAVA_HOME/lib/modules）的归档类（archived classes）和应用程序class path加载到内置平台和系统类加载器（system class loader）中。
+ 扩展CDS以允许将打包的classes加载到自定义class loader中。

详细请看相关JEP

[JEP 310](http://openjdk.java.net/jeps/310)

# 线程-局部管控(JEP 312)

## **What is Thread-Local Handshakes?**

在已有的 Java 版本中，JVM 线程只能全部启用或者停止，没法做到对单独某个线程的操作。为了能够对单独的某个线程进行操作，Java 10 中线程管控引入 JVM 安全点的概念，将允许在不运行全局 JVM 安全点的情况下实现线程回调，由线程本身或者 JVM 线程来执行，同时保持线程处于阻塞状态，这种方式使得停止单个线程变成可能，而不是只能启用或停止所有线程。通过这种方式显著地提高了现有 JVM 功能的性能开销，并且改变了到达 JVM 全局安全点的现有时间语义。

增加的参数为：-XX:ThreadLocalHandshakes (默认为开启)，将允许用户在支持的平台上选择安全点。

详细请看相关JEP

[JEP 312](http://openjdk.java.net/jeps/312)