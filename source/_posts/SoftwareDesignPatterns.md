---
title: 软件设计模式
date: 2019-01-09 10:45:03
categories: design patterns
tags: design patterns
---
# What is Design Pattern?

在软件工程中，设计模式（design pattern）是对软件设计中普遍存在（反复出现）的各种问题，所提出的解决方案。这个术语是由埃里希·伽玛（Erich Gamma）等人在1990年代从建筑设计领域引入到计算机科学的。

设计模式并不直接用来完成代码的编写，而是描述在各种不同情况下，要怎么解决问题的一种方案。面向对象设计模式通常以类别或对象来描述其中的关系和相互作用，但不涉及用来完成应用程序的特定类别或对象。设计模式能使不稳定依赖于相对稳定、具体依赖于相对抽象，避免会引起麻烦的紧耦合，以增强软件设计面对并适应变化的能力。

并非所有的软件模式都是设计模式，设计模式特指软件“设计”层次上的问题。还有其他非设计模式的模式，如架构模式。同时，算法不能算是一种设计模式，因为算法主要是用来解决计算上的问题，而非设计上的问题。

随着软件开发社群对设计模式的兴趣日益增长，已经出版了一些相关的专著，定期召开相应的研讨会，而且沃德·坎宁安（Ward Cunningham）为此发明了WikiWiki用来交流设计模式的经验。
[more](https://en.wikipedia.org/wiki/Software_design_pattern)

# History

设计模式最初是Christopher Alexander(1977/78)提出的一个架构概念。1987年，Kent Beck和Ward Cunningham开始尝试将模式应用于编程——特别是模式语言——并在那年的OOPSLA会议上展示了他们的成果。在接下来的几年里，Beck, Cunningham等人对这项工作进行了跟进。

1994年，所谓的“四人帮”(Gamma et al.)出版了《设计模式：可复用面向对象软件的基础》(Design Patterns: Elements of Reusable Object-Oriented Software)一书，该书经常缩写为“GoF”，此后，设计模式在计算机科学中变得流行起来。同年，举行了第一次编程模式语言会议，并于次年建立了 Portland Pattern Repository ，用于记录设计模式。这个术语的范围仍有争议。值得注意的设计模式类书籍包括:

+ Gamma, Erich; Helm, Richard; Johnson, Ralph; Vlissides, John (1995). *Design Patterns: Elements of Reusable Object-Oriented Software(设计模式：可复用面向对象软件的基础)*. ISBN 0-201-63361-2.
+ Brinch Hansen, Per (1995). *Studies in Computational Science: Parallel Programming Paradigms*. ISBN 0-13-439324-4.
+ Buschmann, Frank; Meunier, Regine; Rohnert, Hans; Sommerlad, Peter (1996). *Pattern-Oriented Software Architecture, Volume 1: A System of Patterns(面向模式的软件体系结构(卷1))*. ISBN 0-471-95869-7.
+ Beck, Kent (1997). *Smalltalk Best Practice Patterns*. ISBN 978-0134769042.
+ Schmidt, Douglas C.; Stal, Michael; Rohnert, Hans; Buschmann, Frank (2000). *Pattern-Oriented Software Architecture, Volume 2: Patterns for Concurrent and Networked Objects(面向模式的软件体系结构(卷2))*. ISBN 0-471-60695-2.
+ Fowler, Martin (2002). *Patterns of Enterprise Application Architecture(企业应用架构模式)*. ISBN 978-0-321-12742-6.
+ Hohpe, Gregor; Woolf, Bobby (2003). *Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions(企业集成模式)*. ISBN 0-321-20068-3.
+ Freeman, Eric T; Robson, Elisabeth; Bates, Bert; Sierra, Kathy (2004). *Head First Design Patterns(深入浅出设计模式)*. ISBN 0-596-00712-4.

# Classification

设计模式最初被分为三类:创建模式、结构模式和行为模式，并使用委托、聚合和协商的概念进行描述。有关面向对象设计的进一步背景，请参见耦合和内聚、继承、接口和多态性。另一个分类还引入了架构设计模式的概念，该概念可以应用于软件的架构级别，例如模型-视图-控制器模式(Model–view–controller，MVC)。

> 耦合性（英语：Coupling，dependency，或称耦合力或耦合度）是一种软件度量，是指一程序中，模块及模块之间信息或参数依赖的程度。[more](https://en.wikipedia.org/wiki/Coupling_(computer_programming))

> 内聚性（Cohesion）也称为内聚力，是一软件度量，是指机能相关的程序组合成一模块的程度，或是各机能凝聚的状态或程度。是结构化分析的重要概念之一。量测内聚性的方式很多，有些方法是由分析源代码，得到非量化的结果，有些方法则是检查源代码的文本特征，以得到内聚性的量化分数。内聚性是属于顺序式的量测量，一般会以“高内聚性”或“低内聚性”来表示。一般会希望程序的模块有高内聚性，因为高内聚性一般和许多理想的软件特性有关，包括鲁棒性、可靠度、可复用性及易懂性（understandability）等特性，而低内聚性一般也代表不易维护、不易测试、不易复用以及难以理解。[more](https://en.wikipedia.org/wiki/Cohesion_(computer_science))

>>耦合性和内聚性是一个相对的概念。一般而言高内聚性代表低耦合性，反之亦然。内聚性是由赖瑞·康斯坦丁所提出，是以实务上可减少维护及修改的“良好”软件的特性为基础。

> 继承（英语：inheritance）是面向对象软件技术当中的一个概念。如果一个类别B“继承自”另一个类别A，就把这个B称为“A的子类”，而把A称为“B的父类别”也可以称“A是B的超类”。继承可以使得子类具有父类别的各种属性和方法，而不需要再次编写相同的代码。在令子类别继承父类别的同时，可以重新定义某些属性，并重写某些方法，即覆盖父类别的原有属性和方法，使其获得与父类别不同的功能。另外，为子类追加新的属性和方法也是常见的做法。 一般静态的面向对象编程语言，继承属于静态的，意即在子类的行为在编译期就已经决定，无法在运行期扩展。[more](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))

> 接口（英语：interface），台湾译为介面，中介之面的意思；大陆译作界面，也译作接口，但“port”大陆也是译作接口。接口泛指实体把自己提供给外界的一种抽象化物（可以为另一实体），用以由内部操作分离出外部沟通方法，使其能被修改内部而不影响外界其他实体与其交互的方式，就如面向对象编程提供的多重抽象化。接口可能也提供某种意义上的在讲不同语言的实体之间的翻译，诸如人类与计算机之间。因为接口是一种间接手段，所以相比起直接沟通，会引致些额外负担。[more](https://en.wikipedia.org/wiki/Interface_(computing))

> 多态（英语：polymorphism）指为不同数据类型的实体提供统一的接口。 多态类型（英语：polymorphic type）可以将自身所支持的操作套用到其它类型的值上。计算机程序运行时，相同的消息可能会送给多个不同的类别之对象，而系统可依据对象所属类别，引发对应类别的方法，而有不同的行为。简单来说，所谓多态意指相同的消息给予不同的对象会引发不同的动作。多态也可定义为“一种将不同的特殊行为和单个泛化记号相关联的能力”。[more](https://en.wikipedia.org/wiki/Polymorphism_(computer_science))

> MVC模式（Model–view–controller）是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）。MVC模式最早由Trygve Reenskaug在1978年提出，是施乐帕罗奥多研究中心（Xerox PARC）在20世纪80年代为程序语言Smalltalk发明的一种软件架构。MVC模式的目的是实现一种动态的程序设计，使后续对程序的修改和扩展简化，并且使程序某一部分的重复利用成为可能。除此之外，此模式通过对复杂度的简化，使程序结构更加直观。软件系统通过对自身基本部分分离的同时也赋予了各个基本部分应有的功能。专业人员可以通过自身的专长分组：
> + 控制器（Controller）- 负责转发请求，对请求进行处理。
> + 视图（View） - 界面设计人员进行图形界面设计。
> + 模型（Model） - 程序员编写程序应有的功能（实现算法等等）、数据库专家进行数据管理和数据库设计(可以实现具体的功能)。
> [more](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)

### Creational patterns(创建模式)

Name | Description
--|:--|
Abstract Factory<br/>抽象工厂 | Provide an interface for creating families of related or dependent objects without specifying their concrete classes.<br/>为一个产品族提供了统一的创建接口。当需要这个产品族的某一系列的时候，可以从抽象工厂中选出相应的系列创建一个具体的工厂类。
Builder<br/>生成器 | Separate the construction of a complex object from its representation, allowing the same construction process to create various representations.<br/>将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。
Dependency Injection<br/>依赖注入 | A class accepts the objects it requires from an injector instead of creating the objects directly.<br/> 类从注入器接受它需要的对象，而不是直接创建对象。
Factory Method<br/>工厂方法 | Define an interface for creating a single object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.<br/>定义用于创建单个对象的接口，但让子类决定实例化哪个类。 工厂方法把一个类的实例化下放到子类。
Lazy initialization<br/>延迟初始化 | Tactic of delaying the creation of an object, the calculation of a value, or some other expensive process until the first time it is needed. This pattern appears in the GoF catalog as "virtual proxy", an implementation strategy for the Proxy pattern.<br/>将对象的创建、值的计算或其他一些开销很大的过程延迟到第一次需要它的时候。这种模式出现在GoF目录中,作为“虚拟代理”,是代理模式的实现策略。
Multiton<br/>多例 | Ensure a class has only named instances, and provide a global point of access to them.<br/>确保一个类只有命名的实例，并提供对这些实例的全局访问。
Object pool<br/>对象池 | Avoid expensive acquisition and release of resources by recycling objects that are no longer in use. Can be considered a generalisation of connection pool and thread pool patterns.<br/>通过回收不再使用的对象，避免昂贵的资源获取和释放。可以认为是连接池和线程池模式的一般化。
Prototype<br/>原型 | Specify the kinds of objects to create using a prototypical instance, and create new objects from the 'skeleton' of an existing object, thus boosting performance and keeping memory footprints to a minimum.<br/>指定使用原型实例创建的对象类型，并从现有对象的“骨架”创建新对象，从而提高性能并将内存占用降到最低。
Resource acquisition is initialization<br/>资源获取为初始化 | Ensure that resources are properly released by tying them to the lifespan of suitable objects.<br/> 确保通过将资源绑定到合适对象的生命周期来正确释放资源。
Singleton<br/>单例 | Ensure a class has only one instance, and provide a global point of access to it.确保一个类只有一个实例，并提供对这些实例的全局访问。

### Structural patterns(结构模式)

Name | Description
--|:--|
Adapter, Wrapper or Translator<br/>适配器，包装器或转换器 | Convert the interface of a class into another interface clients expect. An adapter lets classes work together that could not otherwise because of incompatible interfaces. The enterprise integration pattern equivalent is the translator.<br/>将类的接口转换为客户期望的另一个接口。适配器允许类一起工作，否则由于不兼容的接口。企业集成模式等同于翻译。
Bridge<br/>桥接 | Decouple an abstraction from its implementation allowing the two to vary independently.<br/>将抽象与其实现分离，允许两者独立变化。
Composite<br/>组合 | Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.<br/>将对象组合成树结构以表示部分整体层次结构。 Composite允许客户端统一处理单个对象和对象组合。
Decorator<br/>修饰 | Attach additional responsibilities to an object dynamically keeping the same interface. Decorators provide a flexible alternative to subclassing for extending functionality.<br/>动态地将额外的职责附加到保持相同接口的对象上。装饰器为扩展功能提供了子类化的灵活选择。
Extension object<br/>拓展对象 | Adding functionality to a hierarchy without changing the hierarchy.<br/>在不更改层次结构的情况下向层次结构添加功能。
Facade<br/>外观 | Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.<br/>为子系统中的一组接口提供统一的接口。Facade定义了一个更高级的接口，使子系统更容易使用。
Flyweight<br/>享元 | Use sharing to support large numbers of similar objects efficiently.<br/>通过共享以便有效的支持大量小颗粒对象。
Front controller<br/>前控制器 | The pattern relates to the design of Web applications. It provides a centralized entry point for handling requests.<br/>该模式与Web应用程序的设计有关。它为处理请求提供了一个集中入口点。
Marker<br/>标记 | Empty interface to associate metadata with a class.<br/>空接口，用于将元数据与类关联。
Module<br/>模块 | Group several related elements, such as classes, singletons, methods, globally used, into a single conceptual entity.<br/>将多个相关元素(如类、单例、全局使用的方法)分组到单个概念实体中。
Proxy<br/>代理 | Provide a surrogate or placeholder for another object to control access to it.<br/>为另一个对象提供代理或占位符来控制对它的访问。
Twin<br/>孪生 | 	Twin allows modeling of multiple inheritance in programming languages that do not support this feature.<br/>Twin标准允许在不支持此特性的编程语言中对多重继承进行建模。

### Behavioral patterns(行为模式)

Name | Description
--|:--|
Blackboard<br/>黑板 | Artificial intelligence pattern for combining disparate sources of data (see [blackboard system](https://en.wikipedia.org/wiki/Blackboard_system))<br/>用于组合不同数据源的人工智能模式(参见黑板系统)
Chain of responsibility<br/>责任链 | Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.<br/>通过给多个对象处理请求的机会，避免将请求的发送方与其接收方耦合。将接收对象链接起来，并沿着链传递请求，直到对象处理它。
Command<br/>命令 | Encapsulate a request as an object, thereby allowing for the parameterization of clients with different requests, and the queuing or logging of requests. It also allows for the support of undoable operations.<br/>将请求封装为一个对象，从而允许使用不同请求的客户端参数化，以及请求的排队或日志记录。它还支持可撤消的操作。
Interpreter<br/>解释器 | Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.<br/>给定一种语言，定义其语法的表示，以及使用该表示来解释该语言中的句子的解释器。
Iterator<br/>迭代器 | Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.<br/>提供一种按顺序访问聚合对象的元素而不暴露其底层表示的方法。
Mediator<br/>中介者 | Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it allows their interaction to vary independently.<br/>定义封装一组对象如何交互的对象。中介器通过防止对象显式地相互引用来促进松耦合，并且允许它们的交互独立地变化。
Memento<br/>备忘录 | Without violating encapsulation, capture and externalize an object's internal state allowing the object to be restored to this state later.<br/>在不违反封装的情况下，捕获并外部化对象的内部状态，以便稍后将对象恢复到该状态。
Null object<br/>空对象 | Avoid null references by providing a default object.<br/>通过提供默认对象来避免空引用。
Observer or Publish/subscribe<br/>观察者 | Define a one-to-many dependency between objects where a state change in one object results in all its dependents being notified and updated automatically.<br/>定义对象之间的一对多依赖关系，其中一个对象中的状态更改将导致所有依赖关系被自动通知和更新。
Servant<br/>助手 | Define common functionality for a group of classes. The servant pattern is also frequently called helper class or utility class implementation for a given set of classes. The helper classes generally have no objects hence they have all static methods that act upon different kinds of class objects.<br/>为一组类定义公共功能。对于给定的一组类，服务模式也经常被称为助手类或实用程序类实现。helper类通常没有对象，因此它们具有所有作用于不同类型的类对象的静态方法。
Specification<br/>规格 | Recombinable business logic in a Boolean fashion.<br/>以布尔方式重组业务逻辑。
State<br/>状态 | Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.<br/>允许对象在其内部状态发生变化时改变其行为。对象将显示更改其类。
Strategy<br/>策略 | Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.<br/>定义一系列算法，封装每个算法，并使它们可互换。策略允许算法独立于使用它的客户机变化。
Template method<br/>模板方法 | Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.<br/>在操作中定义算法的框架，将一些步骤推迟到子类。模板方法允许子类在不改变算法结构的情况下重新定义算法的某些步骤。
Visitor<br/>访问者 | Represent an operation to be performed on the elements of an object structure. Visitor lets a new operation be defined without changing the classes of the elements on which it operates.<br/>表示要对对象结构的元素执行的操作。Visitor允许定义一个新操作，而无需更改它所操作的元素的类。

### Concurrency patterns(并发模式)

Name | Description
--|:--|
Active Object<br/>主动对象 | Decouples method execution from method invocation that reside in their own thread of control. The goal is to introduce concurrency, by using asynchronous method invocation and a scheduler for handling requests.<br/>将方法执行与驻留在它们自己的控制线程中的方法调用解耦。目标是通过使用异步方法调用和用于处理请求的调度器引入并发性。
Balking<br/>阻碍 | Only execute an action on an object when the object is in a particular state.<br/>只有当对象处于特定状态时，才对该对象执行操作。
Binding properties<br/>绑定属性 | Combining multiple observers to force properties in different objects to be synchronized or coordinated in some way.<br/>组合多个观察者以强制以某种方式同步或协调不同对象中的属性。
Compute kernel<br/>计算内核 | The same calculation many times in parallel, differing by integer parameters used with non-branching pointer math into shared arrays, such as GPU-optimized Matrix multiplication or Convolutional neural network.<br/>相同的计算并行多次，不同于非分支指针数学用于共享数组的整数参数，例如GPU优化的矩阵乘法或卷积神经网络。
Double-checked locking<br/>双重检查锁定 | Reduce the overhead of acquiring a lock by first testing the locking criterion (the 'lock hint') in an unsafe manner; only if that succeeds does the actual locking logic proceed.Can be unsafe when implemented in some language/hardware combinations. It can therefore sometimes be considered an anti-pattern.<br/>首先以不安全的方式测试锁标准(“锁提示”)，从而减少获取锁的开销;只有成功了，实际的锁定逻辑才会继续。在某些语言/硬件组合中实现可能不安全。因此，有时可以认为它是一个反模式。
Event-based asynchronous<br/>基于事件的异步 | Addresses problems with the asynchronous pattern that occur in multithreaded programs.<br/>处理多线程程序中出现的异步模式的问题。
Guarded suspension<br/>守卫 | Manages operations that require both a lock to be acquired and a precondition to be satisfied before the operation can be executed.<br/>管理既需要获取锁又需要在执行操作之前满足先决条件的操作。
Join<br/>连接 | Join-pattern provides a way to write concurrent, parallel and distributed programs by message passing. Compared to the use of threads and locks, this is a high-level programming model.<br/>Join-pattern提供了一种通过消息传递编写并发、并行和分布式程序的方法。与线程和锁的使用相比，这是一个高级编程模型。
Lock<br/>锁 | One thread puts a "lock" on a resource, preventing other threads from accessing or modifying it.<br/>一个线程对资源进行“锁定”，防止其他线程访问或修改资源。
Messaging design pattern (MDP)<br/>消息传递设计模式 | Allows the interchange of information (i.e. messages) between components and applications.<br/>允许在组件和应用程序之间交换信息（即消息）。
Monitor object<br/>监控对象 | An object whose methods are subject to mutual exclusion, thus preventing multiple objects from erroneously trying to use it at the same time.<br/>一种对象，其方法可以互斥，从而防止多个对象同时错误地尝试使用它。
Reactor<br/>反应器 | A reactor object provides an asynchronous interface to resources that must be handled synchronously.<br/>反应器对象提供了必须同步处理的资源的异步接口。
Read-write lock<br/>迭代器 | Allows concurrent read access to an object, but requires exclusive access for write operations.<br/>允许对对象进行并发读访问，但需要对写操作进行独占访问。
Scheduler<br/>调度 | Explicitly control when threads may execute single-threaded code.<br/>明确控制线程何时可以执行单线程代码。
Thread pool<br/>线程池 | A number of threads are created to perform a number of tasks, which are usually organized in a queue. Typically, there are many more tasks than threads. Can be considered a special case of the object pool pattern.<br/>创建了许多线程来执行许多任务，这些任务通常组织在队列中。通常，除了线程之外还有许多任务。可以认为是对象池模式的特例。
Thread-specific storage<br/>特定于线程的存储 | Static or "global" memory local to a thread.<br/>线程本地的静态或“全局”内存。
