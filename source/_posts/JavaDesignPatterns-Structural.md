---
title: Java 设计模式 - Structural
date: 2019-01-15 10:52:18
categories: 
- java
- design patterns
tags: 
- java
- 设计模式
- design patterns
- structural
thumbnail: /img/article/javase.png
---

# Structural Patterns

在软件工程中，结构设计模式是借由一以贯之的方式来了解元件间的关系，以简化设计。

结构模式的示例包括：
+ Adapter pattern (适配器模式) -将一个物件的界面'转接'成当事人预期的样子
    + Adapter pipeline (适配器管道) : 同时使用多个类别的界面的适配器
    + Retroft Interface Pattern (改造接口模式) : 因除错目的而使用多个适配器
+ Aggregate pattern (聚集模式) - 一种组合模式的版本，包含用于聚集子成员的成员函式
+ Bridge pattern (桥接模式) - 将抽象与其实现解耦，这样两者就可以独立地变化
    + Tombstone (墓碑模式) : 一种中介的查询物件，包含物件的实际位址
+ Composite pattern (组合模式) - 对象的树结构，其中每个对象都有相同的接口
+ Decorator pattern (装饰模式) - 对一个执行的类别，若使用继承方式加上新功能可能会新类别的数量呈指数型地增加，可使用此模式来解决
+ Extensibility pattern (扩展模式) - 亦即框架，将复杂的程式码隐藏在简单的界面后
+ Facade pattern (外观模式) - 为现有接口创建简化的接口，以简化对常见任务的使用
+ Flyweight pattern (享元模式) - 大量对象共享一个公共属性对象以节省空间
+ Marker pattern (标记模式)- 将元数据与类关联的空接口。
+ Pipes and filter (导线及过滤器模式) - 一个进程链，其中每个进程的输出是下一个进程的输入
+ Opaque pointer (不透明指针) - 指向未声明或私有类型的指针，以隐藏其实现细节
+ Proxy pattern (代理模式) - 类的作用是作为另一个对象的接口

## External Polymorphism

External Polymorphism (外部多态性)，用于实现多态性的任何机制，该多态性在显示多态行为的对象的定义之外。基于类型代码的switch语句可能是最简单的这种机制。[more](http://wiki.c2.com/?ExternalPolymorphism)

# Adapter Pattern in Java

## What is Adapter Pattern?

在软件工程中，适配器模式是一种软件设计模式(也称为包装器，与装饰器模式共享的另一种命名)，它允许将现有类的接口用作另一个接口。它通常用于使现有的类在不修改源代码的情况下与其他类一起工作。

适配器设计模式是23种著名的GoF设计模式之一，这些设计模式描述了如何解决重复出现的设计问题，从而设计灵活且可重用的面向对象软件，即更容易实现、更改、测试和重用的对象。

适配器设计模式解决了以下问题:
+ 如何重用不具有客户端所需接口的类？
+ 具有不兼容接口的类如何协同工作？
+ 如何为类提供替代接口？

通常一个(已经存在的)类不能被重用，仅仅因为它的接口不符合客户端需要的接口。

适配器设计模式描述了如何解决这些问题:
+ 定义一个单独的适配器类，将类(adaptee)的(不兼容的)接口转换为另一个客户端所需的接口(目标)。
+ 通过适配器处理(重用)不具有所需接口的类。

这种模式的关键思想是通过一个单独的适配器来适应（已经存在的）类的接口而不改变它。

客户端不知道它们是直接使用目标类，还是通过具有没有目标接口的类的适配器使用。

适配器允许两个不兼容的接口一起工作。这是适配器的真实定义。接口可能不兼容，但内部功能应该满足需求。适配器设计模式允许不兼容的类通过将一个类的接口转换为客户机期望的接口一起工作。[more](https://en.wikipedia.org/wiki/Adapter_pattern)

### Adapter pipeline

从结构上讲，适配器模式是通过(一个小的转换)委托给另一个类来实现接口的类。但是，这个类结构不仅适用于将两个稍微不兼容的接口连接在一起。

适配器管道有时是分解计算的一种很好的方法。例如，它是编译器的合理设计。

这种模式有利于可测试性。在单元测试中，可以单独测试管道的每个部分。在调试集成问题时，可以通过为边界的接口编写修饰符来监听任何边界。如果某些接口是相同的，则可能允许以不同的顺序排列管道的各个部分。

### Retoft Interface Pattern

如果使用的是Java。如果有两个类不是你的的(因此不能修改它们)。你希望编写一些可以交替使用它们的客户端代码。如何指定它们的类型?你不能指定类;不止一个。不能指定它们的公共超类;它太通用了(可能是java.lang.Object)。不能指定它们的公共接口;要么没有，要么太笼统了。

因此，应用适配器模式的公共专门化。实现客户端需要的接口。对于您尝试使用的每个第三方类，创建一个适配器类。适配器应该实现接口;编写每个接口消息的代码，以便将其委托给第三方类中的适当消息。客户端应该引用接口。当客户端需要使用第三方类的实例时，用对应适配器类的实例包装它，并通过接口使用该实例。适配器允许客户端通过同构接口交换使用异构类，而无需修改原始类。

但，这是一种模式？，还是某种运行时类型更改模式语言中的适配器?

它是GangOfFour设计模式书中AdapterPattern的变体。

在这本书中假设您控制了感兴趣的类之一，并试图使某些不兼容的类保持一致。以上的思想概括了AdapterPattern的思想。


## Advantages

+ 有助于实现可重用性和灵活性。
+ 由于必须使用不同的接口，所以Client类并不复杂，并且可以使用多态性在适配器的不同实现之间进行交换。

Disadvantages

+ 所有请求都被转发，因此开销略有增加。
+ 有时需要沿着适配器链进行许多调整才能达到所需的类型。

## Usage

适配器模式很容易理解，因为现实世界中到处都是适配器。例如，考虑一个USB到以太网适配器。当我们在一端有以太网接口，另一端有USB接口时，我们需要这个。因为它们彼此不相容。我们使用一个适配器将一个转换为另一个。这个示例非常类似于面向对象适配器。在设计中，当我们有一个类(客户机)期望某种类型的对象，并且我们有一个对象(Adaptee)提供相同的特性，但公开不同的接口时，就会使用适配器。

使用适配器模式：
 + 客户端通过使用目标接口调用适配器上的方法向适配器发出请求
 + 适配器使用adaptee接口在adaptee上转换该请求。
 + 客户端接收调用的结果，并且不知道适配器的存在。

适配器设计模式的另一个很好的现实例子是移动充电器。移动电池需要3伏的电压来充电，但普通插座可以产生120V(美国)或240V(印度)。因此，移动充电器作为移动充电插座和壁挂式插座之间的适配器。

 首先我们将有两类-Volt(测量伏特)和Socket(产生恒定电压120V)。
 ```
 package com.journaldev.design.adapter;

public class Volt {

	private int volts;
	
	public Volt(int v){
		this.volts=v;
	}

	public int getVolts() {
		return volts;
	}

	public void setVolts(int volts) {
		this.volts = volts;
	}
	
}
```

```
package com.journaldev.design.adapter;

public class Socket {

	public Volt getVolt(){
		return new Volt(120);
	}
}
```

现在我们想建立一个适配器，可以产生3伏，12伏和默认120伏。首先，我们将使用这些方法创建适配器接口。

```
package com.journaldev.design.adapter;

public interface SocketAdapter {

	public Volt get120Volt();
		
	public Volt get12Volt();
	
	public Volt get3Volt();
}
```

### Two Way Adapter Pattern

在实现适配器模式时，有两种方法——类适配器和对象适配器——但是这两种方法产生相同的结果。
+ Class Adapter (类适配器) —— 使用 java继承 方式扩展源接口，在示例中是Socket类。
+ Object Adapter (对象适配器) —— 使用 Java组合，适配器包含源对象。

#### Class Adapter

```
package com.journaldev.design.adapter;

//Using inheritance for adapter pattern
public class SocketClassAdapterImpl extends Socket implements SocketAdapter{

	@Override
	public Volt get120Volt() {
		return getVolt();
	}

	@Override
	public Volt get12Volt() {
		Volt v= getVolt();
		return convertVolt(v,10);
	}

	@Override
	public Volt get3Volt() {
		Volt v= getVolt();
		return convertVolt(v,40);
	}
	
	private Volt convertVolt(Volt v, int i) {
		return new Volt(v.getVolts()/i);
	}

}
```

#### Object Adapter

```
package com.journaldev.design.adapter;

public class SocketObjectAdapterImpl implements SocketAdapter{

	//Using Composition for adapter pattern
	private Socket sock = new Socket();
	
	@Override
	public Volt get120Volt() {
		return sock.getVolt();
	}

	@Override
	public Volt get12Volt() {
		Volt v= sock.getVolt();
		return convertVolt(v,10);
	}

	@Override
	public Volt get3Volt() {
		Volt v= sock.getVolt();
		return convertVolt(v,40);
	}
	
	private Volt convertVolt(Volt v, int i) {
		return new Volt(v.getVolts()/i);
	}
}
```

注意，这两个适配器实现几乎是相同的，它们实现SocketAdapter接口。适配器接口也可以是一个抽象类。

实际调用
```
package com.journaldev.design.test;

import com.journaldev.design.adapter.SocketAdapter;
import com.journaldev.design.adapter.SocketClassAdapterImpl;
import com.journaldev.design.adapter.SocketObjectAdapterImpl;
import com.journaldev.design.adapter.Volt;

public class AdapterPatternTest {

	public static void main(String[] args) {
		
		testClassAdapter();
		testObjectAdapter();
	}

	private static void testObjectAdapter() {
		SocketAdapter sockAdapter = new SocketObjectAdapterImpl();
		Volt v3 = getVolt(sockAdapter,3);
		Volt v12 = getVolt(sockAdapter,12);
		Volt v120 = getVolt(sockAdapter,120);
		System.out.println("v3 volts using Object Adapter="+v3.getVolts());
		System.out.println("v12 volts using Object Adapter="+v12.getVolts());
		System.out.println("v120 volts using Object Adapter="+v120.getVolts());
	}

	private static void testClassAdapter() {
		SocketAdapter sockAdapter = new SocketClassAdapterImpl();
		Volt v3 = getVolt(sockAdapter,3);
		Volt v12 = getVolt(sockAdapter,12);
		Volt v120 = getVolt(sockAdapter,120);
		System.out.println("v3 volts using Class Adapter="+v3.getVolts());
		System.out.println("v12 volts using Class Adapter="+v12.getVolts());
		System.out.println("v120 volts using Class Adapter="+v120.getVolts());
	}
	
	private static Volt getVolt(SocketAdapter sockAdapter, int i) {
		switch (i){
		case 3: return sockAdapter.get3Volt();
		case 12: return sockAdapter.get12Volt();
		case 120: return sockAdapter.get120Volt();
		default: return sockAdapter.get120Volt();
		}
	}
}
```

### Adapter Design Pattern Example in JDK

+ java.util.Arrays#asList()
+ java.io.InputStreamReader(InputStream) (returns a Reader)
+ java.io.OutputStreamWriter(OutputStream) (returns a Writer)

# Aggregate Pattern in Java

## What is Aggregate Pattern?

聚合模式可以引用统计或计算机编程中的概念。这两种用法都将大小写看作是由更小、更简单的部分组成的。

聚合模式是一个重要的统计概念，在许多领域中，它依赖于统计数据来预测大型组的行为，其基础是子组以某种方式一致行为的趋势。它在社会学、经济学、心理学和犯罪学中尤其有用。[more](https://en.wikipedia.org/wiki/Aggregate_pattern)

聚合模式在JAVA中使用：
+ 当没有is-a关系时，通过聚合也可以最好地实现代码重用。
+ 只有在关系为a的关系在涉及的对象的整个生命周期中都得到维护时，才应该使用继承;否则，聚合是最好的选择。

## Usage


如果类有实体引用，则称为聚合。聚合表示HAS-A关系。

Employee对象包含许多信息，如id、name、emailId等。它还包含一个名为address的对象，该对象包含它自己的信息，如城市、州、国家、邮政编码等，如下所示。
```
class Employee{  
	int id;  
	String name;  
	Address address;//Address is a class  
	...  
}  
```

在这种情况下，Employee有一个实体引用地址,他们之间的关系就是Employee有一个Address。

Employee有一个Address对象，Address对象包含它自己的信息，比如city、state、country等等。在这种情况下，关系就是Employee有一个Address。
```
public class Address {  
	String city,state,country;  
	
	public Address(String city, String state, String country) {  
		this.city = city;  
		this.state = state;  
		this.country = country;  
	}  
}  
```

```
public class Emp {  
	int id;  
	String name;  
	Address address;  
  
	public Emp(int id, String name,Address address) {  
		this.id = id;  
		this.name = name;  
		this.address=address;  
	}  
	
	void display(){  
		System.out.println(id+" "+name);  
		System.out.println(address.city+" "+address.state+" "+address.country);  
	}  
	
	public static void main(String[] args) {  
		Address address1=new Address("gzb","UP","india");  
		Address address2=new Address("gno","UP","india");  
		
		Emp e=new Emp(111,"varun",address1);  
		Emp e2=new Emp(112,"arun",address2);  
			
		e.display();  
		e2.display();  
	}

}  
```

# Bridge Pattern in Java

## What is Brige Pattern?

桥接模式是软件工程中使用的一种设计模式，其目的是“将抽象与其实现解耦，以便两者可以独立地变化”，由“Gang of Four”引入。桥接使用封装、聚合，并可以使用继承将职责分离到不同的类中。

当一个类经常变化时,面向对象编程的特性变得非常有用,因为对于程序的代码的更改可以很容易地对程序的先验知识进行。当课堂和它经常发生的变化时,桥的模式是有用的。类本身可以被认为是抽象,以及类可以作为实现的内容。桥梁模式也可以被认为是两层抽象。

桥接模式经常与适配器模式混淆，通常使用对象适配器模式来实现。

变体:通过将实现延迟到使用抽象的点，可以进一步解耦实现。[more](https://en.wikipedia.org/wiki/Bridge_pattern)

## Usage

桥接模式的概念:将抽象与其实现分离，以便两者可以独立变化

桥接设计模式的实现遵循组合优于继承的思想

如果我们以实例来研究桥接设计模式，就会很容易理解。假设我们在接口和实现中都有一个接口层次结构。

```
package com.journaldev.design.bridge;

public interface Color {

	public void applyColor();
}
```

```
package com.journaldev.design.bridge;

public abstract class Shape {
	//Composition - implementor
	protected Color color;
	
	//constructor with implementor as input argument
	public Shape(Color c){
		this.color=c;
	}
	
	abstract public void applyColor();
}
```

我们有如下所示的三角形和五边形实现类。

```
package com.journaldev.design.bridge;

public class Triangle extends Shape{

	public Triangle(Color c) {
		super(c);
	}

	@Override
	public void applyColor() {
		System.out.print("Triangle filled with color ");
		color.applyColor();
	} 

}
```

```
package com.journaldev.design.bridge;

public class Pentagon extends Shape{

	public Pentagon(Color c) {
		super(c);
	}

	@Override
	public void applyColor() {
		System.out.print("Pentagon filled with color ");
		color.applyColor();
	} 

}
```

红颜色和绿颜色的实现类。
```
package com.journaldev.design.bridge;

public class RedColor implements Color{

	public void applyColor(){
		System.out.println("red.");
	}
}
```

```
package com.journaldev.design.bridge;

public class GreenColor implements Color{

	public void applyColor(){
		System.out.println("green.");
	}
}
```

测试程序测试桥接模式实现。

```
package com.journaldev.design.test;

import com.journaldev.design.bridge.GreenColor;
import com.journaldev.design.bridge.Pentagon;
import com.journaldev.design.bridge.RedColor;
import com.journaldev.design.bridge.Shape;
import com.journaldev.design.bridge.Triangle;

public class BridgePatternTest {

	public static void main(String[] args) {
		Shape tri = new Triangle(new RedColor());
		tri.applyColor();
		
		Shape pent = new Pentagon(new GreenColor());
		pent.applyColor();
	}

}
```

当抽象和实现各自具有不同的层次结构，并且我们希望向客户机应用程序隐藏实现时，可以使用桥接设计模式。


# Composite Pattern in Java

## What is Composite Pattern?

在软件工程中，组合模式是一种分区设计模式。复合模式描述一组对象，这些对象以相同的方式作为同一类型对象的单个实例进行处理。组合的目的是将对象“组合”到树结构中，以表示部分-整体层次结构。实现复合模式可以让客户端统一地处理单个对象和组合。

组合设计模式是23种著名的GoF设计模式之一，这些设计模式描述如何解决重复出现的设计问题，从而设计灵活且可重用的面向对象软件，即更容易实现、更改、测试和重用的对象。

组合设计模式可以解决哪些问题?
+ 应该表示部分-整体层次结构，以便客户端能够统一地对待部分和整体对象。
+ 部分-整体层次结构应该表示为树结构。

当定义部分对象和作为部分对象容器的整个对象时，客户端必须分别对待它们，这使得客户端代码变得复杂。

组合设计模式描述了什么解决方案?
+ 为部分 (Leaf)对象和整体 (Composite)对象定义统一的组件接口。
+ 单个 Leaf 对象直接实现组件接口，Composite 对象将请求转发给其子组件。

这使得客户端能够通过组件接口统一地处理 Leaf 和 Composite 对象: Leaf 对象直接执行请求，Composite 对象递归地将请求转发到树结构的子组件。这使得客户端类更容易实现、更改、测试和重用。

在处理树状结构的数据时，程序员经常不得不区分叶节点和分支节点。这使得代码更复杂，因此更容易出错。解决方案是一个允许统一处理复杂和原始对象的接口。在面向对象编程中，组合是设计为一个或多个相似对象的组合的对象，这些对象都具有相似的功能。这被称为对象之间的“has-a”关系。关键的概念是，您可以像操作一组对象一样操作对象的单个实例。

## Usage

当我们必须表示部分-整体层次结构时，应当使用组合设计模式。当我们需要以必须以相同方式处理结构中的对象的方式创建结构时，我们可以应用组合设计模式。

让我们通过一个真实的例子来理解它——一个图是一个由物体组成的结构，比如圆、线、三角形等。这里的图是由不同的部分组成，它们都有相同的操作。

组合模式由以下对象组成：
+ Base Component (基组件) - 基组件是组合中所有对象的接口，客户端程序使用基组件来处理组合中的对象。它可以是一个接口，也可以是一个抽象类，其中包含所有对象共有的一些方法。
+ Leaf (叶) - 定义组合中的元素的行为。它是组合和实现基本组件的构建块。它没有对其他组件的引用。
+ Composite (组合) - 它由叶元素组成，并在基组件中实现操作。