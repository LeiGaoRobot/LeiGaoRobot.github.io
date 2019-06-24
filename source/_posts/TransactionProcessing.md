---
title: Transaction
date: 2019-05-21 11:47:51
categories: 
- [Transaction]
- [DatabaseTransaction]
tags:
- Transaction
- DatabaseTransaction
- Database
---

# Transaction Processing

## What is Transaction Processing?

事务处理是计算机科学中的信息处理，它被分成称为事务的单个不可分割的操作。每笔交易必须作为一个完整的单位成功或失败;它永远不会只是部分完成。

事务处理是一种计算方式，通常由大型服务器计算机执行，支持交互式应用程序。在事务处理中，工作分为单个的，不可分割的操作，称为事务。相比之下，批处理是一种计算方式，其中一个或多个程序处理一系列记录（批处理），用户或操作员很少或没有动作。

详情：

+ [Wikipedia - Transaction Processing](https://en.wikipedia.org/wiki/Transaction_processing)
+ [IBM Knowledge Center - Transaction Processing](https://www.ibm.com/support/knowledgecenter/en/SSGMCP_5.2.0/com.ibm.cics.ts.productoverview.doc/concepts/TransactionProcessing.html)

## Methodlogy

所有 Transaction processing system 的基本原理都是相同的。但是，术语可能因交易处理系统而异，下面使用的术语不一定是通用的。

### Rollback

_Main article: [Rollback (data management)](https://en.wikipedia.org/wiki/Rollback_(data_management))_

事务处理系统在修改数据库时记录数据库的中间状态，然后在无法提交事务时使用这些记录将数据库恢复到已知状态，从而确保数据库的完整性。例如，在事务进行任何修改之前，数据库上的信息的副本将由系统在事务进行任何修改之前保留(有时称为before image)。如果事务的任何部分在提交之前失败，则使用这些副本将数据库恢复到事务开始之前的状态。

### Rollforward

对数据库管理系统的所有修改都可以单独保存日志。(有时称为 after image)。这对于回滚失败的事务不是必需的，但是对于在数据库发生故障时更新数据库管理系统是有用的，因此一些事务处理系统提供了它。如果数据库管理系统完全失败，则必须从最近的备份中恢复它。备份将不反映自备份以来所提交的事务。但是，数据库管理系统一旦恢复，就可以将 after image 日志应用到数据库中(前滚)，使数据库管理系统保持最新。然后可以回滚发生故障时正在进行的任何事务。结果是一个处于一致的、已知状态的数据库，其中包括在失败之前提交的所有事务的结果。

### Deadlocks

_Main article: [Deadlock](https://en.wikipedia.org/wiki/Deadlock)_

在某些情况下，两个事务在处理过程中可能试图同时访问数据库的同一部分，从而阻止它们继续处理。例如，事务A可以访问数据库的X部分，事务B也可以访问数据库的Y部分。如果此时，事务A试图访问数据库的Y部分，同时事务B也试图访问X部分，则会发生死锁，并且两个事务都不能继续往下处理。事务处理系统的设计目的是在这些死锁发生时检测它们。通常这两个事务都将被取消和回滚，然后它们将以不同的顺序自动重新启动，这样死锁就不会再次发生。有时，只有一个死锁事务将被取消、回滚，并在短暂延迟后自动重新启动。

三个或更多事务之间也可能发生死锁。涉及的事务越多，它们检测的难度就越大，以至于事务处理系统发现它们可以检测到的死锁存在实际限制。

### Compensating transaction

在提交和回滚机制不可用或没有预期处理的系统中，补偿事务通常用于撤消失败的事务并将系统恢复到先前的状态。

## ACID criteria

_Main article: [ACID](https://en.wikipedia.org/wiki/ACID_(computer_science))_

Jim Gray在20世纪70年代后期以ACID（atomicity，consistency，isolation 和 durability）的首字母缩写定义了可靠的 transaction system 的属性。

### Atomicity (原子性)

_Main article: [Atomicity (database systems)](https://en.wikipedia.org/wiki/Atomicity_(database_systems))_

事务对状态的更改是原子的：要么全部发生，要么都不发生。这些更改包括数据库更改，消息和传感器上的操作。...

### Consistency (一致性)

一致性:事务是状态的正确转换。作为一个组所采取的操作不违反与状态相关的任何完整性约束。

### Isolation (隔离性)

即使事务并发执行，在其中一个事务T看起来，其他事务在T之前或T之后执行，但不是两者都执行。

### Durability (持久性)

一旦事务成功完成（提交），它对数据库的更改将在失败后继续存在并保留其更改。

## Implements

标准事务处理软件，例如IBM的信息管理系统，最初是在20世纪60年代开发的，并且常常与特定的数据库管理系统紧密耦合。客户机-服务器计算在上世纪80年代实现了类似的原则，但成败参半。然而，近年来，分布式 客户端-服务器模型的维护变得相当困难。由于响应各种在线服务(特别是 Web )的事务数量不断增加，因此单一的分布式数据库并不是一个实用的解决方案。此外，大多数在线系统由一组共同运行的程序组成，而不是严格的客户端-服务器模型，在这种模型中，单个服务器可以处理事务处理。今天，有许多事务处理系统可以在程序间级别工作，并且可以扩展到大型系统，包括大型机。

其中一项工作是 [X/Open 分布式事务处理（Distributed Transaction Processing）](https://en.wikipedia.org/wiki/X/Open_XA)（另请参阅Java Transaction API（JTA）。但是，专有的事务处理环境，例如IBM的CICS仍然非常受欢迎，虽然CICS已经发展到包括开放行业标准也是如此。

术语极端事务处理（XTP）用于描述具有非常具有挑战性的要求的事务处理系统，特别是吞吐量要求（每秒事务数）。可以通过分布式或集群式架构来实现这样的系统。

# Transaction Processing System

事务处理系统是一组信息，其处理在监视数据库系统中的数据事务处理的事务的程序。当通过互联网销售某些东西时，该系统很有用。它允许在物品被销售到实际销售之间的时间延迟。一个例子是体育赛事门票。客户填写他们的信息以购买座位票; 交易处理系统持有票证，以便另一个客户也不能购买它。它允许不向两个不同的客户出售机票。

事务处理是一种计算方式，它将工作划分为单独的，不可分割的操作，称为事务。事务处理系统（TPS）是一种软件系统，或软件/硬件结合，支持事务处理。

事务处理系统（TPS）是一种软件系统，或软件/硬件结合，支持事务处理。

第一个事务处理系统是SABRE，由IBM为美国航空公司制造，于1970年投入运营。该系统设计为每天处理多达83,000个事务，系统运行在两台IBM 7090计算机上。SABER 于1972 年迁移到IBM System/360 计算机，并首先成为IBM产品，作为航空公司控制计划（Airline Control Program），后来成为事务处理设施（Transaction Processing Facility）。除航空公司外，大型银行，信用卡公司和连锁酒店也使用TPF。

惠普 的NonStop系统（前身为 Tandem 的 NonStop）是一个硬件和软件系统，设计用于联机事务处理（OnLine Transaction Processing）在1976年引入的系统被设计用于处理事务和提供的可用性和数据完整性的极端水平。

[more info about transaction processing systems](https://en.wikipedia.org/wiki/Transaction_processing_system)

## Processing types

事务处理不同于其他计算机处理模型 - batch processing(批处理), time-sharing(分时), and real-time processing(实时处理).

### Batch processing

_Main article: [Batch processing](https://en.wikipedia.org/wiki/Batch_processing)_

批处理是在计算机上执行一系列程序(作业)，不需要人工干预。同时收集和处理几个称为批处理的事务。当输入事务时，每个事务的结果不是立即可用的;存在一定时间延迟。

最早的计算机是极其昂贵的设备，与后来的型号相比速度很慢。机器通常用于一组特定的任务，由控制面板操作，操作员通过开关手动输入小程序，以便加载和运行一系列程序。这些程序可能需要数小时，甚至数周才能运行。随着计算机速度的增长，运行时间下降，很快启动下一个程序所需的时间就成为一个问题。批处理方法通过对程序进行排队来减少这些“死周期”，以便一旦一个程序完成，下一个程序就会启动。

为了支持批处理操作，程序员使用一些相对便宜的卡片穿孔机或纸带写入器来“脱机”编写程序。当输入(或打孔)完成后，程序被提交给操作团队，操作团队计划运行这些程序。重要项目快速启动;在不那么重要的项目开始之前多久是不可预测的。当程序运行最终完成时，输出(通常打印)返回给程序员。整个过程可能需要几天的时间，在此期间程序员可能永远看不到计算机。

允许用户直接操作计算机的另一种选择通常过于昂贵，难以考虑。这是因为当计算机处于空闲状态时，用户可能需要很长时间输入代码。这种情况将交互开发限制在那些能够负担得起浪费计算周期的组织中:大部分是大型大学。大学里的程序员们谴责批处理强加给他们的行为，以至于斯坦福大学的学生拍了一部短片，幽默地批评了这种行为。他们试验了与计算机直接交互的新方法，这个领域今天被称为human-computer interaction(人机交互)。

拓展阅读:

+ [Wikipedia - Human-computer interaction](https://en.wikipedia.org/wiki/Human%E2%80%93computer_interaction)

### Real-time processing

_Main article: [Real-time processing](https://en.wikipedia.org/wiki/Real-time_computing)_

“实时系统试图确保对 stimulus 或请求的适当响应足够快，足以影响引发 stimulus 的条件。”实时处理中的每个事务都是唯一的;它不是一组事务的一部分。

### Time-sharing

_Main article: [Time-sharing](https://en.wikipedia.org/wiki/Time-sharing)_

分时（time-sharing）是对计算机资源的一种共享方式，利用多道程序与多任务处理使多个用户可以同时使用一台计算机。

一般来说，计算机用户（可以是多个）通过特定的端口向计算机发送指令，计算机完成相应任务后再将结果通过端口反馈给用户。

在早期的计算机系统中，计算机处理多个用户发送出的指令的时候，处理的方案即为分时，即计算机把它的运行时间分为多个时间段，并且将这些时间段平均分配给用户们指定的任务。轮流地为每一个任务运行一定的时间，如此循环，直至完成所有任务。

### Transaction processing

_Main article: [Transaction processing](#Transaction-Processing)_

事务处理系统（TPS）是一种收集，存储，修改和检索企业数据事务的信息系统。事务处理系统还尝试为请求提供可预测的响应时间，尽管这不像实时系统那样重要。事务处理不允许用户作为时间共享运行任意程序，而是仅允许预定义的结构化事务。每笔交易通常是短期的，并且每笔交易的处理活动都是预先编制的。


## Features

在评估事务处理系统时，以下功能被认为是重要的

### Performance (性能)

事务处理系统（TPS）的响应时间非常重要，因为企业在进行交易之前无法让客户等待很长一段时间。事务处理系统通常通过在给定时间段内可以处理的事务数量来衡量其性能。

### Continuous availability (连续可用性)

良好的TPS必须非常可靠，因为如果要分解，企业可能会失去很大一部分收入，因为客户无法购买他们的产品。系统必须在用户输入事务的时间段内可用。系统必须能够在不破坏数据的情况下处理硬件或软件问题。

### Data integrity (数据完整性)

必须保护多个用户不尝试同时更改相同的数据块，例如两个运营商不能在飞机上出售相同的座位。

### Ease of use (便于使用)

TPS必须能够允许授权员工随时访问它。通常，事务处理系统的用户是临时用户。系统应该易于理解，尽可能地保护它们免受数据输入错误的影响，并允许它们轻松纠正错误。

### Modular growth (模块化增长)

该系统应能够以增量成本增长，而不是需要完全替代。应该可以在不关闭系统的情况下添加，替换或更新硬件和软件组件。

## Types

### Processing in a batch (批量处理)

同时处理多个事务，并带有时间延迟。

可以在批处理中收集和处理事务。事务将被收集并随后在批处理时方便或便捷地进行处理。从历史上看，这是最常用的方法，因为当时还没有允许实时处理的信息技术。

### Processing in a real-time (实时处理)

一次处理一个事务，没有时间延迟。

这是对数据的即时处理。它提供对事务的即时确认。它可能涉及同时执行更改数据的事务的大量用户。由于技术的进步(如数据传输速度的提高和更大的带宽)，实时更新是可能的。

## Database for transaction processing

_Main article: [Database](https://en.wikipedia.org/wiki/Database)_

数据库是有组织的数据集合。与典型的事务处理应用程序一样，数据库为非结构化的请求提供快速检索时间。 可以使用分层，网络或关系结构来构造用于事务处理的数据库。

+ Hierachical structure(分层结构)：以一系列级别组织数据。它的从上到下的结构由节点和分支组成; 每个子节点都有分支，并且只链接到一个更高级别的父节点。
+ Network structure(网络结构)：网络结构还使用节点和分支来组织数据。但是，与分层结构不同，每个子节点都可以链接到多个更高的父节点。
+ Relational structure(关系结构)：关系数据库在一系列相关表中组织其数据。这提供了灵活性，因为构建表之间的关系。

![gcheap](/img/TransactionProcessing/Hierachical-Diagram.png)
![gcheap](/img/TransactionProcessing/Network-Diagram.png)
![gcheap](/img/TransactionProcessing/Relational-Diagram.png)


在事务处理系统中使用的数据库系统中需要以下功能：

+ 良好的数据放置：数据库应设计为访问来自许多同时用户的数据模式。
+ 短事务：短事务可以快速处理。这避免了并发性并使系统步调。
+ 实时备份：应在低活动时间之间安排备份，以防止服务器滞后。
+ 高规范化：这会降低冗余信息以提高速度并提高并发性，这也可以改善备份。
+ 归档历史数据：将不常用的数据移动到其他数据库或备份表中。这样可以保持较小的表，还可以缩短备份时间
+ 良好的硬件配置：硬件必须能够处理许多用户并提供快速响应时间。

## Backup procedures
_Main article: [Backup](https://en.wikipedia.org/wiki/Backup)_

由于业务组织已经非常依赖于事务处理，故障可能会破坏业务的常规例程并在一定时间内停止其运行。为了防止数据丢失并最大限度地减少中断，必须有精心设计的备份和恢复程序。恢复过程可以在系统停机时重建系统。

### Recovery process

TPS可能由于多种原因而失败，例如系统故障，人为错误，硬件故障，数据不正确或无效，计算机病毒，软件应用程序错误或自然灾害或人为灾难。由于无法防止所有故障，因此TPS必须能够在发生错误时检测并纠正错误并应对故障。TPS将通过恢复数据库，可能涉及备份，日志，检查点和恢复管理器：

+ Journal： Journal 维护着交易和数据库变更的审计线索。使用事务日志和数据库更改日志，事务日志记录每个事务的所有基本数据，包括数据值，事务时间和终端号。数据库更改日志包含已由事务修改的记录副本之前和之后。
+ Checkpoint： Checkpoint 的目的是提供数据库中数据的快照。通常， checkpoint 是标识某个时间点的数据库状态的任何标识符或其他引用。对数据库页面的修改在内存中执行，并且不必在每次更新后写入磁盘。因此，数据库系统必须定期执行检 checkpoint，将保存在内存中的这些更新写入存储磁盘。将这些更新写入存储磁盘会创建一个时间点，在该时间点，数据库系统可以在数据库系统意外关闭或崩溃后的恢复期间应用事务日志中包含的更改。如果 checkpoint 中断并且需要恢复，则数据库系统必须从先前成功的 checkpoint 开始恢复。 checkpoint 可以是事务一致的或非事务一致的（也称为 fuzzy checkpoint）。事务一致性的 checkpoint 生成一个持久数据库映像，该映像足以将数据库恢复到开始 checkpoint 时外部感知的状态。非事务一致的 checkpoint 导致持久数据库映像不足以执行数据库状态的恢复。要执行数据库恢复，需要其他信息，通常包含在事务日志中。事务一致性 checkpoint 是指一致的数据库，它不一定包括所有最新提交的事务，但是在启动 checkpoint 创建时提交的事务所做的所有修改都完全存在。不一致的事务是指一个 checkpoint ，它不一定是一致的数据库，如果没有为 checkpoint 中包含的打开事务生成的所有日志记录，则无法恢复到该 checkpoint 。取决于实现的数据库管理系统的类型 checkpoint 可以包含索引或存储页面（用户数据），索引和存储页面。如果 checkpoint 中未包含任何索引，则必须在从 checkpoint 映像还原数据库时创建索引。
+ Recovery Manager： Recovery Manager 是一个将数据库恢复到正确状态的程序，该状态允许重新启动事务处理。


根据系统的失败方式，可以使用两种不同的恢复过程。通常，这些过程涉及恢复从备份设备收集的数据，然后再次运行事务处理。两种类型的恢复是向后恢复和向前恢复：

+ Backward recovery：用于撤消对数据库的不必要更改。它将反转已中止的交易所做的更改。
+ Forward recovery：它从数据库的备份副本开始。然后，事务将根据在进行备份和当前时间之间发生的事务日志进行重新处理。

另请参阅：[Checkpoint restart](https://en.wikipedia.org/wiki/Checkpoint_restart)

### Types of back-up procedures

主要有两种类型的备份程序：grandfather-father-son 和 partial backups：

#### Grandfather - father - son

此过程涉及定期对所有数据进行完整备份 - 每天，每周，每月或任何适当的数据。保留了多代备份，通常是三代，这就产生了名称。最近的备份是 son ，前一个 father ，最老的备份是 grandfather 。该方法通常用于具有磁带的批量交易处理系统。如果在批处理运行期间系统出现故障，则通过还原子备份然后重新启动批处理来重新创建主文件。但是，如果子备份失败，被破坏或被破坏，则使用上一代备份（father）。同样，如果失败，则需要在father（即grandfather）之前生成备份。当然，这一代人越老，数据就越过时。仅组织已更改的记录。例如，可以每周执行完整备份，并在每晚执行部分备份。使用此方案进行恢复涉及还原上次完整备份，然后还原所有部分备份以生成最新数据库。此过程比仅进行完整备份更快，但代价是恢复时间更长。

#### Backup plus journal

此技术还与常规完整备份结合使用。主文件定期备份。自上次备份以来完成的事务将单独存储，称为日志或日志文件。可以通过还原上一个完整备份然后从日志文件重新处理事务来重新创建主文件。这将生成最新的数据库副本，但由于处理大量日志记录所需的时间，恢复可能需要更长时间。


# Java Transaction API

Java Transaction API，通常称为JTA，是用于管理 Java 中的事务的API 。它允许我们以资源无关的方式启动，提交和回滚事务。

JTA的真正强大之处在于它能够在单个事务中管理多个资源（即数据库，消息传递服务）。

在Java Transaction API（JTA），在一个Java企业版（Java EE的）的API，能使分布式事务跨多个进行的 X/Open XA的资源的Java环境。JTA是在Java Community Process下开发的JSR 907 规范.JTA规定：

+ 事务边界的划分
+ X/Open XA API允许资源参与事务。

JTA提供了对业务代码的事务控制(开始，提交和回滚)的抽象。

如果没有这种抽象，我们必须处理每种资源类型的各个API。

例如，我们需要像这样处理JDBC资源。同样，JMS资源可能具有类似但不兼容的模型。

通过JTA，我们可以以一致和协调的方式管理不同类型的多种资源。

作为API，JTA定义了由事务管理器实现的接口和语义。

JTA的实现：

+ [Bitronix](https://github.com/bitronix/btm)
+ [Narayana](http://narayana.io/)

## What is X/Open XA architecture？

在 X/Open XA 体系结构中，事务管理器或事务处理监视器（TP监视器）协调跨多个资源（例如数据库和消息队列）的事务。每个资源都有自己的资源管理器。资源管理器通常有自己的API来操作资源，例如JDBC API用于处理关系数据库。此外，资源管理器允许TP监视器协调其自身和其他资源管理器之间的分布式事务。最后，有一个应用程序以开始与TP监视器通信，提交或回滚事务。应用程序还使用自己的API与各个资源进行通信以修改资源。

## JTA Implements of the X/Open XA architecture？

JTA API由两个Java包中的类组成：

+ javax.transaction
+ javax.transaction.xa

JTA以 X/Open XA 架构为模型，但它定义了两个不同的API来划分事务边界。它区分应用程序服务器（如EJB服务器）和应用程序组件。它提供了一个接口，javax.transaction.TransactionManager ,应用程序服务器本身使用该接口来开始，提交和回滚事务。它提供了一个不同的接口，javax.transaction.UserTransaction由一般客户端代码（如servlet或EJB）用来管理事务。

JTA体系结构要求每个资源管理器必须实现该 javax.transaction.xa.XAResource 接口才能由TP监视器进行管理。如前所述，每个资源都有自己的特定API，例如：

+ 关系数据库使用JDBC
+ 消息传递服务使用JMS
+ 广义EIS（企业信息系统）资源使用Java EE Con​​nector API。

## Java Transaction API (J2EE)

Java Transaction API由三个元素组成：高级应用程序事务划分接口，用于应用程序服务器的高级事务管理器接口，以及用于事务资源管理器的 X/Open XA协议的标准Java映射。

### UserTransaction 接口

javax.transaction.UserTransaction 接口为应用程序提供了以编程方式控制事务边界的能力。Java客户端程序或EJB bean可以使用此接口。

UserTransaction.begin()方法启动全局事务并将事务与调用线程相关联。事务管理器透明地管理事务到线程关联。

不需要支持嵌套事务。当调用线程已与事务关联且事务管理器的实现不支持嵌套事务时，UserTransaction.begin方法抛出NotSupportedException。

应用程序之间的事务上下文传播由客户端和服务器计算机上的基础事务管理器实现提供。用于传播的事务上下文格式取决于协议，必须在客户端和服务器主机之间协商。例如，如果事务管理器是JTS规范的实现，它将使用CORBA OTS 1.1规范中指定的事务上下文传播格式。事务传播对应用程序是透明的。

### [@Transactional](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html)

[javax.transaction.Transactional](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html) 注解提供了应用程序以声明式的方式控制事务的边界。此注解可以应用于Java EE规范定义为托管bean（包括CDI托管bean）的任何类。

下面的代码示例说明了在请求范围的CDI托管bean中[@Transactional](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html)的用法：

```
@RequestScoped
public class ExampleBean {

    @Transactional
    public void foo() { // A transaction is active here
        
        // Do work

    } // After the method returns transaction is committed or rolled back
}
```
可以通过注释上的属性配置事务行为。可用选项与EJB规范的选项非常相似。

### @TransactionScoped

javax.transaction.TransactionScoped 注解使应用程序能够声明bean所处的作用域与给定事务的活动时间相关联。

下面的代码示例说明了在请求范围的CDI托管bean中@TransactionScoped的用法：

```
@TransactionScoped
public class TxScopedBean {
    public int number;

    public int getNumber() {return number;}
    public void setNumber(int number) {this.number = number;}
}

@RequestScoped
public class ExampleBean {

    @Inject
    private TxScopedBean txScopedBean;

    @Transactional
    public void foo() {
        txScopedBean.setNumber(1);
    }

    @Transactional
    public void bar() {
        System.out.print(tXscopedBean.getNumber());
    }
}
```

如果首先在ExampleBean的托管实例上调用foo()方法，然后调用方法bar()，那么输出的数字将是0而不是1。这是因为每个方法都有自己的事务，因此也有自己的TxScopedBean实例。因此，在调用foo()期间设置的数字1将不会在调用bar()期间显示。

## EJB服务器中的UserTransaction支持

EJB服务器需要支持UserTransaction接口，以便EJB BEAN使用javax.ejb中的BEAN值。TransactionManagement 注解(称为bean管理的事务或BMT)。UserTransaction接口通过使用getUserTransaction方法的EJBContext接口公开给EJB组件，或者直接通过使用通用 @Resource 注解的注入公开给EJB组件。因此，EJB应用程序不直接与事务管理器接口进行事务界定;相反，EJB bean依赖EJB服务器为其在Enterprise javabean规范中定义的所有事务工作提供支持。(EJB服务器和TM之间的底层交互对应用程序是透明的;实现事务管理的重担落在EJB容器和服务器提供者身上。

面的代码示例说明了EJB会话bean中通过bean管理的事务对UserTransaction的使用：

```
@Stateless
@TransactionManagement(BEAN)
public class ExampleBean {

    @Resource
    private UserTransaction utx;

    public void foo() {
        // start a transaction
        utx.begin();

        // Do work

        // Commit it
        utx.commit();
    }
}
```

或者，可以从SessionContext获取UserTransaction：

```
@Stateless
@TransactionManagement(BEAN)
public class ExampleBean {

    @Resource
    private SessionContext ctx;

    public void foo() {
        UserTransaction utx = ctx.getUserTransaction();

        // start a transaction
        utx.begin();

        // Do work

        // Commit it
        utx.commit();
    }
}
```

请注意，在上面的示例中，如果省略了@TransactionManagement(BEAN)注释，则无论何时调用foo()都会自动启动JTA事务，并且在foo()退出时自动提交或回滚JTA事务。因此，在EJB编程中不需要使用UserTransaction，但是对于非常特殊的代码可能需要。

> Java Transaction Service，简称JTS,Java事务服务是构建事务管理器的规范，将事务管理器映射到对象管理组织 (OMG)的基于CORBA体系架构的对象事务服务（OTS）上， 它使用IIOP在在多个JTS事务管理器之间传播事务。

## Example

示例应用程序是银行应用程序的一个非常简单的后端服务。我们有两个服务，BankAccountService 和  AuditService 使用两个不同的数据库。这些独立的数据库需要在事务开始，提交或回滚时进行协调。

首先，使用Spring Boot来简化配置：

```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.4.RELEASE</version>
</parent>
 
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jta-bitronix</artifactId>
</dependency>
```

在每个测试方法之前，我们用空数据初始化AUDIT_LOG， 用2行初始化数据库 ACCOUNT：

```
+-----------+----------------+
| ID        |  BALANCE       |
+-----------+----------------+
| a0000001  |  1000          |
| a0000002  |  2000          |
+-----------+----------------+
```

### Declarative Transaction Demarcation

在JTA中处理事务的第一种方法是使用 [@Transactional](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html) 注释。有关更详细的说明和配置，请参阅此[文章](https://www.baeldung.com/transaction-configuration-with-jpa-and-spring)。

用@Transactional注释facade服务方法 executeTranser()。这指示事务管理器开始事务：

```
@Transactional
public void executeTransfer(String fromAccontId, String toAccountId, BigDecimal amount) {
    bankAccountService.transfer(fromAccontId, toAccountId, amount);
    auditService.log(fromAccontId, toAccountId, amount);
    ...
}
```

这里方法executeTranser()调用2个不同的服务，AccountService和AuditService。这些服务使用2个不同的数据库

当 executeTransfer() 返回时，事务管理器认识到这是事务的结束，并将提交给两个数据库:

```
tellerService.executeTransfer("a0000001", "a0000002", BigDecimal.valueOf(500));
assertThat(accountService.balanceOf("a0000001")).isEqualByComparingTo(BigDecimal.valueOf(500));        
assertThat(accountService.balanceOf("a0000002")).isEqualByComparingTo(BigDecimal.valueOf(2500));

TransferLog lastTransferLog = auditService.lastTransferLog();
assertThat(lastTransferLog).isNotNull();        
assertThat(lastTransferLog.getFromAccountId()).isEqualTo("a0000001");
assertThat(lastTransferLog.getToAccountId()).isEqualTo("a0000002"); 
assertThat(lastTransferLog.getAmount()).isEqualByComparingTo(BigDecimal.valueOf(500));
```

### Rolling back in Declarative Demarcation

在方法的执行结束时，executeTransfer()检查帐户余额，如果源资金不足，则抛出RuntimeException:

```
@Transactional
public void executeTransfer(String fromAccontId, String toAccountId, BigDecimal amount) {
    bankAccountService.transfer(fromAccontId, toAccountId, amount);
    auditService.log(fromAccontId, toAccountId, amount);
    BigDecimal balance = bankAccountService.balanceOf(fromAccontId);
    if(balance.compareTo(BigDecimal.ZERO) < 0) {
        throw new RuntimeException("Insufficient fund.");
    }
}
```

超过第一个@Transactional的未处理的RuntimeException将事务回滚到两个数据库。实际上，执行金额大于余额的转移将导致回滚：

```
assertThatThrownBy(() -> {
    tellerService.executeTransfer("a0000002", "a0000001", BigDecimal.valueOf(10000));
}).hasMessage("Insufficient fund.");
 
assertThat(accountService.balanceOf("a0000001")).isEqualByComparingTo(BigDecimal.valueOf(1000));
assertThat(accountService.balanceOf("a0000002")).isEqualByComparingTo(BigDecimal.valueOf(2000));
assertThat(auditServie.lastTransferLog()).isNull();
```

### Programmatic Transaction Demarcation

另一种控制JTA事务的方法是通过UserTransaction以编程方式  。

现在让我们修改 executeTransfer() 来手动处理事务：

```
userTransaction.begin();

bankAccountService.transfer(fromAccontId, toAccountId, amount);
auditService.log(fromAccontId, toAccountId, amount);
BigDecimal balance = bankAccountService.balanceOf(fromAccontId);
if(balance.compareTo(BigDecimal.ZERO) < 0) {
    userTransaction.rollback();
    throw new RuntimeException("Insufficient fund.");
} else {
    userTransaction.commit();
}
```

在我们的示例中，begin() 方法启动一个新事务。如果余额验证失败，我们调用rollback()，它将回滚两个数据库。否则，对commit()的调用会将更改提交给两个数据库。

重要的是要注意 commit()和  rollback() 都会结束当前事务。

最终，使用程序化划分为我们提供了细粒度事务控制的灵活性。

## Distributed Transaction JTA with Spring

### Distributed Transaction With JTA

Spring Boot通过使用[Atomikos](#Java-Transaction-API)或[Bitronix](#Java-Transaction-API) 嵌入式事务管理器支持跨多个 [XA](#What-is-X/Open-XA-architecture) 资源的分布式JTA事务。部署到合适的Java EE Application Server时，也支持JTA事务。

检测到JTA环境时，Spring JtaTransactionManager 用于管理事务。自动配置的JMS，DataSource 和JPA bean 已升级为支持 [XA](#What-is-X/Open-XA-architecture) 事务。您可以使用标准的Spring注解，例如 @Transactional，参与分布式事务。如果您在 JTA 环境中并仍希望使用本地事务，则可以将该 spring.jta.enabled 属性设置 false 为禁用 JTA 自动配置。

#### Using an Atomikos Transaction Manager

Atomikos是一个流行的开源事务管理器，可以嵌入到Spring Boot应用程序中。您可以使用 spring-boot-starter-jta-atomikosStarter 引入相应的Atomikos库。Spring Boot自动配置Atomikos并确保将适当的 depends-on 设置应用于Spring bean以 正确启动和关闭顺序。

默认情况下，Atomikos 事务日志将写入transaction-logs应用程序主目录（应用程序jar文件所在的目录）中的目录。您可以通过spring.jta.log-dir在application.properties文件中设置属性来自定义此目录的位置 。以...开头的属性spring.jta.atomikos.properties也可用于自定义Atomikos UserTransactionServiceImp。

有关完整的详细信息，请参阅 [Atomikos Javadoc](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/api/org/springframework/boot/jta/atomikos/AtomikosProperties.html)。

> 为确保多个事务管理器可以安全地协调相同的资源管理器，必须使用唯一ID配置每个Atomikos实例。默认情况下，此ID是运行Atomikos的计算机的IP地址。要确保生产中的唯一性，应spring.jta.transaction-manager-id 为应用程序的每个实例配置具有不同值的属性。

#### Using a Bitronix Transaction Manager

Bitronix是一种流行的开源JTA事务管理器实现。您可以使用spring-boot-starter-jta-bitronixstarter将适当的Bitronix依赖项添加到项目中。与Atomikos一样，Spring Boot会自动配置Bitronix并对bean进行后处理，以确保启动和关闭顺序正确。

默认情况下，Bitronix事务日志文件（part1.btm和part2.btm）将写入transaction-logs应用程序主目录中的目录。您可以通过设置spring.jta.log-dir属性来自定义此目录的位置。以...开头的属性spring.jta.bitronix.properties也绑定到 bitronix.tm.Configurationbean，允许完全自定义。

有关详细信息，请参阅 [Bitronix Documentation](https://github.com/bitronix/btm/wiki/Transaction-manager-configuration)。

> 为确保多个事务管理器可以安全地协调相同的资源管理器，必须为每个Bitronix实例配置唯一ID。默认情况下，此ID是运行Bitronix的计算机的IP地址。要确保生产中的唯一性，应spring.jta.transaction-manager-id 为应用程序的每个实例配置具有不同值的属性。

#### Using a Java EE Managed Transaction Manager

如果将Spring Boot应用程序打包为一个war或一个ear文件并将其部署到Java EE应用程序服务器，则可以使用应用程序服务器的内置事务管理器。Spring Boot尝试通过查看常见的JNDI位置（java:comp/UserTransaction，java:comp/TransactionManager等等）来自动配置事务管理器。如果使用应用程序服务器提供的事务服务，通常还需要确保所有资源都由服务器管理并通过JNDI公开。Spring Boot尝试通过查找ConnectionFactoryJNDI路径（java:/JmsXA或java:/XAConnectionFactory）来自动配置JMS ，您可以使用该 [spring.datasource.jndi-name](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-sql.html#boot-features-connecting-to-a-jndi-datasource) 属性 来配置您的DataSource。

#### Mixing XA and Non-XA JMS Connections

使用JTA时，主JMS ConnectionFactorybean可识别XA并参与分布式事务。在某些情况下，您可能希望使用非XA处理某些JMS消息ConnectionFactory。例如，您的JMS处理逻辑可能需要比XA超时更长的时间。

如果要使用非XA ConnectionFactory，可以注入 nonXaJmsConnectionFactorybean而不是@Primary jmsConnectionFactorybean。为了保持一致性，jmsConnectionFactory还使用bean别名提供bean xaJmsConnectionFactory。

以下示例显示了如何注入ConnectionFactory实例：

```
// Inject the primary (XA aware) ConnectionFactory
@Autowired
private ConnectionFactory defaultConnectionFactory;

// Inject the XA aware ConnectionFactory (uses the alias and injects the same as above)
@Autowired
@Qualifier("xaJmsConnectionFactory")
private ConnectionFactory xaConnectionFactory;

// Inject the non-XA aware ConnectionFactory
@Autowired
@Qualifier("nonXaJmsConnectionFactory")
private ConnectionFactory nonXaConnectionFactory;
```

#### Supporting an Alternative Embedded Transaction Manager

XAConnectionFactoryWrapper 和 [XADataSourceWrapper](https://github.com/spring-projects/spring-boot/tree/v2.1.5.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jdbc/XADataSourceWrapper.java) 接口可用于支持替代嵌入式事务经理。接口负责包装XAConnectionFactory和XADataSourcebean，并将它们作为常规ConnectionFactory和DataSourcebean 公开，它们透明地注册到分布式事务中。DataSource和JMS自动配置使用JTA变体，前提是您有一个JtaTransactionManagerbean和在您的域中注册的相应XA包装bean ApplicationContext。

[BitronixXAConnectionFactoryWrapper](https://github.com/spring-projects/spring-boot/tree/v2.1.5.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXAConnectionFactoryWrapper.java) 和 [BitronixXADataSourceWrapper](https://github.com/spring-projects/spring-boot/blob/v2.1.5.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXADataSourceWrapper.java) 提供了如何编写XA包装很好的例子。


# 原文资料

+ Wikipedia - Transaction Processing : https://en.wikipedia.org/wiki/Transaction_processing
+ Wikipedia - Transaction Processing System : https://en.wikipedia.org/wiki/Transaction_processing_system
+ Wikipedia - Java Transaction API : https://en.wikipedia.org/wiki/Java_Transaction_API
+ baeldung - Guide to Java EE JTA : https://www.baeldung.com/jee-jta
+ spring.io - Distributed Transactions with JTA : https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-jta.html
+ IBM Knowledge Center - Transaction Processing : https://www.ibm.com/support/knowledgecenter/en/SSGMCP_5.2.0/com.ibm.cics.ts.productoverview.doc/concepts/TransactionProcessing.html
+ computerbusinessresearch - Transaction processing system : http://www.computerbusinessresearch.com/Home/decision-making/transaction-processing-system
