---
title: Java10 版本特性
date: 2018-12-25 15:37:37
categories: Java
tags:
- java10
- java
thumbnail: /img/article/javase.png
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

详细相关JEP

[JEP 286](http://openjdk.java.net/jeps/286)

## **Usage**

示例
```
    var numbers = List.of(1, 2, 3, 4, 5); // inferred value ArrayList<String>
    // Index of Enhanced For Loop
    for (var number  - numbers) {
        System.out.println(number);
    }
    // Local variable declared in a loop
    for (var i = 0; i < numbers.size(); i++) {
        System.out.println(numbers.get(i));
    }
    var stream = numbers.stream();// Stream<int>
```

具体用法实例

[Java 10 - Local Variable Type Inference](https://www.journaldev.com/19871/java-10-local-variable-type-inference)

# 整合 JDK 代码仓库(JEP 296)

## **What is Consolidate the JDK Forest into a Single Repository?**

为了简化开发流程，Java 10 中会将多个代码库合并到一个代码仓库中。

在已发布的 Java 版本中，JDK 的整套代码根据不同功能已被分别存储在多个 Mercurial 存储库，这八个 Mercurial 存储库分别是：root、corba、hotspot、jaxp、jaxws、jdk、langtools、nashorn。

虽然以上八个存储库之间相互独立以保持各组件代码清晰分离，但同时管理这些存储库存在许多缺点，并且无法进行相关联源代码的管理操作。其中最重要的一点是，涉及多个存储库的变更集无法进行原子提交 （atomic commit）。例如，如果一个 bug 修复时需要对独立存储两个不同代码库的代码进行更改，那么必须创建两个提交：每个存储库中各一个。这种不连续性很容易降低项目和源代码管理工具的可跟踪性和加大复杂性。特别是，不可能跨越相互依赖的变更集的存储库执行原子提交这种多次跨仓库的变化是常见现象。

为了解决这个问题，JDK 10 中将所有现有存储库合并到一个 Mercurial 存储库中。这种合并的一个次生效应是，单一的 Mercurial 存储库比现有的八个存储库要更容易地被镜像(作为一个 Git 存储库)，并且使得跨越相互依赖的变更集的存储库运行原子提交成为可能，从而简化开发和管理过程。虽然在整合过程中，外部开发人员有一些阻力，但是 JDK 开发团队已经使这一更改成为 JDK 10 的一部分。

详细相关JEP

[JEP 296](http://openjdk.java.net/jeps/296)

# 统一的垃圾回收接口(JEP 304)

## **What is Garbage Collector Interface?**

在当前的 Java 结构中，组成垃圾回收器（GC）实现的组件分散在代码库的各个部分。尽管这些惯例对于使用 GC 计划的 JDK 开发者来说比较熟悉，但对新的开发人员来说，对于在哪里查找特定 GC 的源代码，或者实现一个新的垃圾收集器常常会感到困惑。更重要的是，随着 Java modules 的出现，我们希望在构建过程中排除不需要的 GC，但是当前 GC 接口的横向结构会给排除、定位问题带来困难。

为解决此问题，需要整合并清理 GC 接口，以便更容易地实现新的 GC，并更好地维护现有的 GC。Java 10 中，hotspot/gc 代码实现方面，引入一个干净的 GC 接口，改进不同 GC 源代码的隔离性，多个 GC 之间共享的实现细节代码应该存在于辅助类中。这种方式提供了足够的灵活性来实现全新 GC 接口，同时允许以混合搭配方式重复使用现有代码，并且能够保持代码更加干净、整洁，便于排查收集器问题。

此更改为内部GC代码提供了更好的模块化。它将来有助于在不更改现有代码库的情况下添加新GC，也有助于删除或管理以前的GC。

详细相关JEP

[JEP 304](http://openjdk.java.net/jeps/304)

# 并行全垃圾回收器 G1(JEP 307)

## **What is Parallel Full GC for G1?**

G1 是设计来作为一种低延时的垃圾回收器（但是如果它跟不上旧的堆碎片产生的提升速率的话，将仍然采用完整压缩集合）。在 JDK9 之前，默认的收集器是并行，吞吐，收集器。为了减少在使用默认的收集器的应用性能配置文件的差异，G1 现在有一个并行完整收集机制。

大家如果接触过 Java 性能调优工作，应该会知道，调优的最终目标是通过参数设置来达到快速、低延时的内存垃圾回收以提高应用吞吐量，尽可能的避免因内存回收不及时而触发的完整 GC（Full GC 会带来应用出现卡顿）。

G1 垃圾回收器是 Java 9 中 Hotspot 的默认垃圾回收器，是以一种低延时的垃圾回收器来设计的，旨在避免进行 Full GC，但是当并发收集无法快速回收内存时，会触发垃圾回收器回退进行 Full GC。之前 Java 版本中的 G1 垃圾回收器执行 GC 时采用的是基于单线程标记扫描压缩算法（mark-sweep-compact）。为了最大限度地减少 Full GC 造成的应用停顿的影响，Java 10 中将为 G1 引入多线程并行 GC，同时会使用与年轻代回收和混合回收相同的并行工作线程数量，从而减少了 Full GC 的发生，以带来更好的性能提升、更大的吞吐量。

Java 10 中将采用并行化 mark-sweep-compact 算法，并使用与年轻代回收和混合回收相同数量的线程。具体并行 GC 线程数量可以通过：-XX：ParallelGCThreads 参数来调节，但这也会影响用于年轻代和混合收集的工作线程数。

详细相关JEP

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

详细相关JEP

[JEP 310](http://openjdk.java.net/jeps/310)

# 线程-局部管控(JEP 312)

## **What is Thread-Local Handshakes?**

在已有的 Java 版本中，JVM 线程只能全部启用或者停止，没法做到对单独某个线程的操作。为了能够对单独的某个线程进行操作，Java 10 中线程管控引入 JVM 安全点的概念，将允许在不运行全局 JVM 安全点的情况下实现线程回调，由线程本身或者 JVM 线程来执行，同时保持线程处于阻塞状态，这种方式使得停止单个线程变成可能，而不是只能启用或停止所有线程。通过这种方式显著地提高了现有 JVM 功能的性能开销，并且改变了到达 JVM 全局安全点的现有时间语义。

增加的参数为：-XX:ThreadLocalHandshakes (默认为开启)，将允许用户在支持的平台上选择安全点。

详细相关JEP

[JEP 312](http://openjdk.java.net/jeps/312)

# 移除 Native-Header 自动生成工具(JEP 313)

## **Why Remove the Native-Header Generation Tool?**

自 Java 9 以来便开始了一些对 JDK 的调整，用户每次调用 javah 工具时会被警告该工具在未来的版本中将会执行的删除操作。当编译 JNI 代码时，已不再需要单独的 Native-Header 工具来生成头文件，因为这可以通过 Java 8（JDK-7150368）中添加的 javac 来完成。在未来的某一时刻，JNI 将会被 Panama 项目的结果取代，但是何时发生还没有具体时间表。

详细相关JEP

[JEP 313](http://openjdk.java.net/jeps/313)

# 额外的 Unicode 语言标签扩展(JEP 314)

## **What is Additional Unicode Language-Tag Extensions?**

自 Java 7 开始支持 BCP 47 语言标记以来， JDK 中便增加了与日历和数字相关的 Unicode 区域设置扩展，在 Java 9 中，新增支持 ca 和 nu 两种语言标签扩展。而在 Java 10 中将继续增加 Unicode 语言标签扩展，具体为：增强 java.util.Locale 类及其相关的 API，以更方便的获得所需要的语言地域环境信息。同时在这次升级中还带来了如下扩展支持：
+ cu - 货币类型
+ fw - 一周的第一天
+ rg - 区域覆盖
+ tz - 时区

为了支持这些附加扩展，对各种API进行了更改，以便根据Unicode或其他扩展提供信息。

```
java.text.DateFormat::get*Instance
java.text.DateFormatSymbols::getInstance
java.text.DecimalFormatSymbols::getInstance
java.text.NumberFormat::get*Instance
java.time.format.DateTimeFormatter::localizedBy
java.time.format.DateTimeFormatterBuilder::getLocalizedDateTimePattern
java.time.format.DecimalStyle::of
java.time.temporal.WeekFields::of
java.util.Calendar::{getFirstDayOfWeek,getMinimalDaysInWeek}
java.util.Currency::getInstance
java.util.Locale::getDisplayName
java.util.spi.LocaleNameProvider
```

详细相关JEP

[JEP 314](http://openjdk.java.net/jeps/314)

# 备用存储装置上的堆分配(JEP 316)

## **What is Heap Allocation on Alternative Memory Devices?**

随着便宜的NV-DIMM内存的普及，未来的系统可能配备异构内存架构。这种技术的一个例子是英特尔的3D XPoint。除DRAM之外，这样的架构将具有一种或多种具有不同特性的非DRAM存储器。这个JEP针对与DRAM具有相同语义的替代存储器设备，包括原子操作的语义，因此可以代替DRAM用于对象堆而不改变现有的应用程序代码。所有其他的内存结构，如代码堆，元代码空间，线程堆栈等，都将继续驻留在DRAM中。

一些操作系统中已经通过文件系统提供了使用非 DRAM 内存的方法。例如：NTFS DAX 模式和 ext4 DAX。这些文件系统中的内存映射文件可绕过页面缓存并提供虚拟内存与设备物理内存的相互映射。与 DRAM 相比，NV-DIMM 可能具有更高的访问延迟，低优先级进程可以为堆使用 NV-DIMM 内存，允许高优先级进程使用更多 DRAM。

在多JVM部署中，一些JVM（如守护进程，服务等）的优先级低于其他JVM。与DRAM相比，NV-DIMM可能具有更高的访问延迟。低优先级进程可以使用NV-DIMM内存作为堆，允许高优先级进程使用更多的DRAM。

大数据和内存数据库等应用程序对内存的需求不断增加。这种应用可以使用NV-DIMM作为堆，因为与DRAM相比，NV-DIMM有更大的容量，成本更低。

要在这样的备用设备上进行堆分配，可以使用堆分配参数 -XX：AllocateHeapAt = <path>，这个参数将指向文件系统的文件并使用内存映射来达到在备用存储设备上进行堆分配的预期结果。

详细相关JEP

[JEP 316](http://openjdk.java.net/jeps/316)

# 基于 Java 的 实验性 JIT 编译器（试验版本）(JEP 317)

## **What is Experimental Java-Based JIT Compiler?**

Java 10 中开启了基于 Java 的 JIT 编译器 Graal，并将其用作 Linux/x64 平台上的实验性 JIT 编译器开始进行测试和调试工作，另外 Graal 将使用 Java 9 中引入的 JVM 编译器接口（JVMCI）,基于Java的JIT编译器Graal是JDK 9中引入的实验性AOT（Ahead-of-Time）编译器的基础。

Graal 是一个以 Java 为主要编程语言、面向 Java bytecode 的编译器。与用 C++实现的 C1 及 C2 相比，它的模块化更加明显，也更加容易维护。Graal 既可以作为动态编译器，在运行时编译热点方法；亦可以作为静态编译器，实现 AOT 编译。在 Java 10 中，Graal 作为试验性 JIT 编译器一同发布（JEP 317）。将 Graal 编译器研究项目引入到 Java 中，或许能够为 JVM 性能与当前 C++ 所写版本匹敌（或有幸超越）提供基础。

Java 10 中默认情况下 HotSpot 仍使用的是 C2 编译器，要启用 Graal 作为 JIT 编译器，请在 Java 命令行上使用以下参数：

`-XX：+ UnlockExperimentalVMOptions -XX：+ UseJVMCICompiler`

详细相关JEP

[JEP 317](http://openjdk.java.net/jeps/317)

# 根证书认证(JEP 319)

## **What is Root Certificates?**

自 Java 9 起在 keytool 中加入参数 -cacerts，可以查看当前 JDK 管理的根证书。而 Java 9 中 cacerts 目录为空，这样就会给开发者带来很多不便。从 Java 10 开始，将会在 JDK 中提供一套默认的 CA 根证书。

作为 JDK 一部分的 cacerts 密钥库旨在包含一组能够用于在各种安全协议的证书链中建立信任的根证书。但是，JDK 源代码中的 cacerts 密钥库至目前为止一直是空的。因此，在 JDK 构建中，默认情况下，关键安全组件（如 TLS）是不起作用的。要解决此问题，用户必须使用一组根证书配置和 cacerts 密钥库下的 CA 根证书。

在 JDK 中将提供一套默认的 CA 根证书。关键的安全部件，如 TLS ，在 OpenJDK 构建中将默认有效。这是 Oracle 正在努力确保 OpenJDK 二进制和 Oracle JDK 二进制功能上一样的工作的一部分，是一项有用的补充内容。

详细相关JEP

[JEP 319](http://openjdk.java.net/jeps/319)

# 基于时间的版本发布模式

虽然 JEP 223中引入的版本字符串方案较以往有了显著的改进。但是，该方案并不适合以后严格按照六个月的节奏来发布 Java 新版本的这种情况。

按照 JEP 223 的语义中，每个基于 JDK 构建或使用组件的开发者（包括 JDK 的发布者）都必须提前敲定版本号，然后切换过去。开发人员则必须在代码中修改检查版本号的相关代码，这对所有参与者来说都很尴尬和混乱。

Java 10 中将重新编写之前 JDK 版本中引入的版本号方案，将使用基于时间模型定义的版本号格式来定义新版本。保留与 JEP 223 版本字符串方案的兼容性，同时也允许除当前模型以外的基于时间的发布模型。使开发人员或终端用户能够轻松找出版本的发布时间，以便开发人员能够判断是否将其升级到具有最新安全修补程序或可能的附加功能的新版本。

Oracle Java 平台组的首席架构师 Mark Reinhold 在博客上介绍了有关 Java 未来版本的一些想法（你能接受 Java 9 的下一个版本是 Java 18.3 吗？）。他提到，Java 计划按照时间来发布，每半年一个版本，而不是像之前那样按照重要特性来确定大版本，如果某个大的特性因故延期，这个版本可能一拖再拖。

当时，Mark 也提出来一种基于时间命名版本号的机制，比如下一个将于 2018 年 3 月发布的版本，就是 18.3，再下一个版本是 18.9，以后版本依此类推。

不过经过讨论，考虑和之前版本号的兼容等问题，最终选择的命名机制是：

$FEATURE.$INTERIM.$UPDATE.$PATCH

$FEATURE，每次版本发布加 1，不考虑具体的版本内容。2018 年 3 月的版本是 JDK 10，9 月的版本是 JDK 11，依此类推。

$INTERIM，中间版本号，在大版本中间发布的，包含问题修复和增强的版本，不会引入非兼容性修改。

“Feature releases” 版本将包含新特性，“Update releases” 版本仅修复 Bug

添加了新的API以编程方式获取这些版本：
```
Version version = Runtime.version();
version.feature();
version.interim();
version.update();
version.patch();
```

# 新 API

有 73 项新增内容添加到了标准类库中：

+ java.awt.Toolkit int getMenuShortcutKeyMaskEx() - 确定哪个扩展修饰符键是菜单快捷键的适当加速键。
+ java.awt.geom.Path2D:void trimToSize() - 将此 Path2D 实例的容量计算到它当前的大小。应用可使用此操作将路径的存储空间最小化。这个方法也被添加到 Path2D.Double 和 Path2D.Float 类。
+ java.io.ByteArrayOutputStream:String toString(Charset) - 重载 toString()，通过使用指定的字符集解码字节，将缓冲区的内容转换为字符串。
+ java.io.PrintStream:lang.io.PrintWriter - 这两个类都有三个新的构造函数，它们需要额外的 Charset 参数。
+ java.io.Reader:long transferTo(Writer) - 从这个 Reader 中读取所有字符，并按照所读的顺序将字符写入给定的 Writer 。
+ java.lang.Runtime.Version - 有四种新方法返回新（JEP 322）版本字符串字段的整数值 - feature()、interim()、patch() 和 update() 。
+ java.lang.StackWalker.StackFrame:String getDescriptor() - 按照 JVM 标准返回此堆栈帧所代表的方法的描述符。
+ String getMethodType():返回此堆栈帧所代表的方法类型，描述参数类型和返回值类型。
+ java.lang.invoke.MethodType:Class<?> lastParameterType() - 返回这个方法类型的最后一个参数类型。如果这个方法类型没有参数，则返回空类型作为岗哨值（Sentinel Value）。
+ java.lang.management.RuntimeMXBean:long getPid() - 返回正在运行的 JVM 的进程 ID 。
+ java.lang.management.ThreadMXBean:ThreadInfo[] dumpAllThreads(boolean, boolean, int) - 返回所有活动线程的线程信息，其中有指定的最大元素数量和同步信息的堆栈跟踪。
+ ThreadInfo[] getThreadInfo(long[], boolean, boolean, int) - 返回每个线程的线程信息，这些线程的标识位于输入数组中，其中有指定的最大元素数量和同步信息的堆栈跟踪。
+ java.lang.reflect.MalformedParameterizedTypeException - 添加了一个新的构造函数，它以字符串的形式作为参数来获取详细信息。
+ java.net.URLDecoder:java.net.URLEncoder - 这两个类都有新的重载的解码和编码方法，将 charset 作为附加参数。
+ java.nio.channels.Channels - 两个新的静态重载方法，允许使用 Charset 的 newReader（ReadByteChannel，Charset）和newWriter（WriteByteChannel，Charset）。
+ java.nio.file.FileStore:long getBlockSize() - 在这个文件存储中返回每个块的字节数。
+ java.time.chrono - 这个包里有三个类，HijrahEra、MiinguoEra 和 ThaiBuddhistEra ，都有同样的方法。
+ String getDisplayName(TextStyle, Locale) - 这将返回用于识别 era 的文本名称，适合于向用户展示。
+ java.time.format.DateTimeFormatter:localizedBy(Locale) - 返回指定格式器的一个副本，其中包含地区、日历、区域、小数和/或时区的本地化值，这将取代该格式器中的值。
+ java.util - DoubleSummaryStatistics、IntSummaryStatistics 和 LongSummaryStatistics 都有一个新的构造函数，它包含 4 个数值。它使用指定的计数、最小值、最大值和总和构造一个非空实例。
+ java.util.List:java.util.Map:java.util.Set - 这些接口中的每一个都增加了一个新的静态方法，copyOf(Collection）。这些函数按照其迭代顺序返回一个不可修改的列表、映射或包含给定集合的元素的集合。
+ java.util.Optional:java.util.OptionalDouble:java.util.OptionalInt:java.util.OptionalLong - 每一个类都有一个新的方法，orElseThrow() ，它本质上和 get() 一样，也就是说，如果 Optional 有值则返回。否则，将抛出 NoSuchElementException 。
+ java.util.Formatter:java.util.Scanner - 这两个类都有三个新的构造函数，除了其他参数之外，它们都带有一个 charset 参数。
+ java.util.Properties - 这有一个新的构造函数，它接受一个 int 参数。这将创建一个没有默认值的空属性列表，并且指定初始大小以容纳指定的元素数量，而无需动态调整大小。还有一个新的重载的 replace 方法，接受三个 Object 参数并返回一个布尔值。只有在当前映射到指定值时，才会替换指定键的条目。
+ java.SplittableRandom:void nextBytes(byte[]) - 用生成的伪随机字节填充一个用户提供的字节数组。
+ java.util.concurrent.FutureTask - 添加了 toString() 方法，该方法返回一个标识 FutureTask 的字符串，以及它的完成状态。在括号中，状态包含如下字符串中的一个，“Completed Normally” 、“Completed Exceptionally”、 “Cancelled” 或者 “Not completed”。
+ java.util.concurrent.locks.StampedLock:boolean isLockStamp(long) - 返回一个标记戳表示是否持有一个锁。
+ boolean isOptimisticReadStamp(long) - 返回一个标记戳代表是否成功的进行了乐观读（optimistic read）。
+ boolean isReadLockStamp(long) - 返回一个标记戳表示是否持有一个非独占锁（即 read lock ）。
+ boolean isWriteLockStamp(long) - 返回一个标记戳表示是否持有一个独占锁（即 write lock ）。
+ java.jar.JarEntry:String getRealName() - 返回这个 JarEntry 的真实名称。如果这个 JarEntry 是一个多版本 jar 文件的入口，它被配置为这样处理，这个方法返回的名字是 JarEntry 所代表的版本条目的入口，而不是 ZipEntry.getName（） 返回的基本条目的路径名。如果 JarEntry 不代表一个多版本 jar 文件的版本化条目或者 jar 文件没有被配置为作为一个多版本 jar 文件进行处理，这个方法将返回与 ZipEntry.getName（） 返回的相同名称。
+ java.util.jar.JarFile:Stream<JarEntry> versionedStream() - 返回 jar 文件中指定版本的入口对应 Stream 。与 JarEntry 的 getRealName 方法类似，这与多版本 jar 文件有关。
+ java.util.spi.LocaleNameProvider:getDisplayUnicodeExtensionKey(String, Locale) - 为给定的 Unicode 扩展键返回一个本地化名称。
+ getDisplayUnicodeExtensionType(String, String, Locale) - 为给定的 Unicode 扩展键返回一个本地化名称。
+ java.util.stream.Collectors:toUnmodifiableList():toUnmodifiableSet():toUnmodifiableMap(Function, Function) - toUnmodifiableMap(Function, Function, BinaryOperator) - 这四个新方法都返回 Collectors ，将输入元素聚集到适当的不可修改的集合中。
+ java.lang.model.SourceVersion - 现在有了一个字段，它代表了 JDK 10 的版本。
+ java.lang.model.util.TypeKindVisitor6:javax.lang.model.util.TypeKindVisitor9:（我必须承认，我从来没听说过这些类）RevisitNoTypeAsModule(NoType, P) - 访问一个 MODULE 的 pseudo-type 。我不确定为什么只有这两个类得到这个方法，因为还有 Visitor7 和 Visitor8 变量。
+ javax.remote.management.rmi.RMIConnectorServer - 这个类已经添加了两个字段： CREDENTIALS_FILTER_PATTERN 和 SERIAL_FILTER_PATTERN 。
+ javax.ButtonModel - 看，Swing 还在更新！
+ ButtonGroup getGroup() - 返回按钮所属的组。通常用于单选按钮，它们在组中是互斥的。
+ javax.plaf.basic.BasicMenuUI:Dimension getMinimumSize(JComponent) - 返回指定组件适合观感的最小大小。

# JVM 规范改动

这些改动相当小：
+ 4.6节：类文件格式（第99页）。在方法访问标志方面有小的改动。
+ 4.7节：模块属性（第169页）。如果模块不是 java.base ，则 JDK 10 不再允许设置 ACC_TRANSITIVE 或 ACC_STATIC_PHASE 。
+ 4.10节：类文件的校验（第252页）。dup2 指令已改变了 typesafe form 1 的定义，颠倒了 canSafleyPushList 一节中类型的顺序（你需要仔细查看才能发现它）。
+ 5.2节：Java 虚拟机启动（第350页）。该描述添加了在创建初始类或接口时可使用用户定义的类加载器（ bootstrap 类加载器除外）。

# 对 Java 语言规范的更改

这里还有一些更改，但主要是为了支持局部变量类型推断。

+ 第3.8节：标识符（第23页）。在忽略了可忽略的字符之后，标识符的等价性现在被考虑了。这似乎是合乎逻辑的。
+ （第24页）一个新的 Token，TypeIdentifier，它支持对局部变量类型推断的新用法，而 var 的使用不是关键字，而是一个具有特殊含义的标识符，作为局部变量声明的类型。
+ 第4.10.5节：类型预测（第76页）。这是一个相当复杂的部分，它涉及到捕获变量、嵌套类以及如何使用局部变量类型推断。我建议你阅读规范中的这一部分，而不是试图解释它。
+ 第6.1节：声明（第134页）。一个反映使用 TypeIdentifier 来支持局部变量类型的推断的小改动。
+ 第6.5节：确定名字的含义（第153页，第158页和第159页）。根据类型标识符的使用而更改类类型。
+ 第6.5.4.1:简单的 PackageOrTypeNames（第160页）
+ 第6.5.4.2节：合规的 PackageOrTypeNames（第160页）。这两种方式都与使用 TypeIdentifier 有细微的变化。
+ 第7.5.3:单静态导入声明（第191页）。这改变了导入具有相同名称的静态类型的规则。除非类型是相同的，否则这将成为一个错误，在这种情况下，重复被忽略。
+ 第7.7.1:依赖（第198页）。如果你明确声明一个模块需要 java.base ，那在必要的关键字之后，你就不能再使用修饰符（例如静态）了。
+ 第8部分：正式参数（第244页）。接收者参数可能只出现在一个实例方法的 formalparameters 列表，或者是一个内部类的构造函数中，其中内部类没有在静态上下文中声明。
+ 第9.7.4节：注释可能出现的地方（第335页）。有一个与局部变量类型推断相关的变更。
+ 第14.4部分：局部变量声明语句（第433页）。实现局部变量类型推断所需的大量更改。
+ 第14节：增强的 for 语句（第455页）。这个结构已经更新，包括对局部变量类型推断的支持。
+ 第14.20.3节:try-with-resources（474页）。这个结构已经更新，包括对局部变量类型推断的支持。

最后，第 19 章有多处语法更新，反映了应更多使用 TypeIdentifier 类型标识符，而不仅仅是 Identifier 标识符，以支持局部变量类型推断。

# 杂项

+ 如果 Kerberos 的配置文件 krb5.conf 包含一个 INCLUDEDIR 选项，那么在 INCLUDEDIR 这个目录下所有以 .conf 结尾的文件都会被默认加载进来。
+ 以前版本中已经过期的 Java 的启动选项 -d32 和 –d64 在当前版本已经被移除。如果你在新的版本里仍然使用了这两个选项，JVM 将无法正常启动。
+ JDK10 支持 JDK9 中的新版本 Doclet，JDK6、JDK7、JDK8 中的 Doclet 版本都不再支持。
+ JDK10 重新启用了在 JDK9 中被不当过时的 newFactory() 方法。
+ JDK10 引入了一个新的 Javadoc 标签： {@summary…}，解决了以前版本无法生成 API 摘要的问题。
+ JDK10 去掉了 BiasedLockingStartupDelay 的 4 秒启动延时。
+ 以下在 com.sun.security.auth 包中的过时的类在新版本中都已经被移除：
+ +  PolicyFile
+ + SolarisNumericGroupPrincipal
+ + SolarisNumericUserPrincipal
+ + X500Principal
+ + SolarisLoginModule
+ + SolarisSystem
+ 在 java.lang.SecurityManager 类中的以下属性和方法（从 JDK 1.2 就已经过时）终于被移除了：
+ + inCheck (属性)
+ + getInCheck
+ + classDepth
+ + classLoaderDepth
+ + currentClassLoader
+ + currentLoadedClass
+ + inClass
+ + inClassLoader
+ 以下 java.lang.Runtime 类中已经被废弃的国际化方法在新版本被移除：
+ + getLocalizedInputStream
+ + getLocalizedOutputStream
+ 以下废弃的 Hotspot –X 选项在新版本中被移除：-Xoss, -Xsqnopause, -Xoptimize, -Xboundthreads and –Xusealtsigs.
+ policytool 在新版本中被移除。
+ javadoc 工具在新版本中可以通过 –add-stylesheets 命令选项支持多个 stylesheets 。
+ 新版本的 JVM 能够根据系统分配给当前 Docker 容器的 CPU 数和内存来配置线程池和 GC 机制，而不再是直接使用系统的 CPU 和内存。并且增加了三个更强大的命令选项：-XX:InitialRAMPercentage、-XX:MaxRAMPercentage 和 -XX:MinRAMPercentage 。
+ 新版本增加了一个新的系统属性：jdk.disableLastUsageTracking。这个新增的属性就像它的名字一样，会禁用 JRE 的上一次使用跟踪。

# 主要参考资源

## [openjdk](http://openjdk.java.net/projects/jdk/10/)

## [ibm-developerworks](https://www.ibm.com/developerworks/cn/java/the-new-features-of-Java-10/index.html)

## [journaldev](https://www.journaldev.com/20395/java-10-features)

## [Java 10 docs](https://docs.oracle.com/javase/10/)

## [Java 10 docs api](https://docs.oracle.com/javase/10/docs/api/overview-summary.html)

## [oschina](https://www.oschina.net/translate/109-new-features-in-jdk-10?lang=chs&p=1)