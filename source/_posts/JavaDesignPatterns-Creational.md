---
title: Java 设计模式 - Creational
date: 2018-12-27 17:17:15
categories: 
- java
- design patterns
tags: 
- java
- 设计模式
- design patterns
- creational
thumbnail: /img/article/javase.png
---

# Creational Patterns

在软件工程中，创造型设计模式是处理对象创建机制的设计模式，它试图以适合这种情况的方式创建对象。对象创建的基本形式可能会导致设计问题或增加设计的复杂性。创造型设计模式通过某种方式控制对象的创建来解决这个问题。

创造型设计模式由两个主导思想组成。一是将系统使用的具体类封装起来，二是隐藏这些具体类的实例创建和结合的方式。

创建型模式又分为对象创建型模式和类创建型模式。对象创建型模式处理对象的创建，类创建型模式处理类的创建。详细地说，对象创建型模式把对象创建的一部分推迟到另一个对象中，而类创建型模式将它对象的创建推迟到子类中。

## Definition

创建型模式旨在将系统与它的对象创建、结合、表示的方式分离。这些设计模式在对象创建的类型、主体、方式、时间等方面提高了系统的灵活性。

## Usage

现代软件工程更加依赖对象的组合，而不是类的继承，强调从硬编码的行为转变到定义一组基本行为来组合成复杂的行为。硬编码的行为不够灵活，因为如果想要改变设计的一部分，需要通过重写或者重新实现才能完成。另外，硬编码没有提高重用性，而且难以跟踪错误。由于这些原因，创建型模式比硬编码的行为更有用。创建型模式使设计变得更灵活，提供了不同的方式，从代码中移除了对需要实例化的具体类的引用。换句话说，这些模式增强了对象和类之间的独立性。

在以下情况中，可以考虑应用创建型模式：
+ 一个系统需要和它的对象和产品的创建相互独立。
+ 一组相关的对象被设计为一起使用。
+ 隐藏一个类库的具体实现，仅暴露它们的接口。
+ 创建独立复杂对象的不同表示。
+ 一个类希望它的子类实现它所创建的对象。
+ 类的实例化在运行时才指定。
+ 一个类只能有一个实例，而且这个实例能在任何时候访问到。
+ 实例应该能在不修改的情况下具有可扩展性。

## Examples

创建型设计模式的一些示例包括：

+ Factory Mothed pattern(工厂方法模式) - 允许一个类的实例化推迟到子类中进行。
+ Abstract Factory pattern(抽象工厂模式) - 提供一个创建相关或依赖对象的接口，而不指定对象的具体类。
+ Singleton pattern(单例模式) - 保证一个类只有一个实例，并且提供对这个实例的全局访问方式。
+ Builder pattern(生成器模式) - 将一个复杂对象的创建与它的表示分离，使同样的创建过程可以创建不同的表示。
+ Lazy Initialization pattern(延迟初始化模式) - 将对象的创建，某个值的计算，或者其他代价较高的过程推迟到它第一次需要时进行。
+ Object Pool pattern(对象池模式) - 通过回收不再使用的对象，避免创建和销毁对象时代价高昂的获取和释放资源的过程。
+ Prototype pattern(原型模式) - 使用原型实例指定要创建的对象类型，通过复制原型创建新的对象。


# Factory Pattern in Java

## What is Factory Design Pattern?

工厂方法模式（Factory method pattern）是一种实现了“工厂”概念的面向对象设计模式。是处理在不指定对象具体类型的情况下创建对象的问题。工厂方法模式的实质是“定义一个创建对象的接口，但让实现这个接口的类来决定实例化哪个类。工厂方法让类的实例化推迟到子类中进行。”

创建一个对象常常需要复杂的过程，所以不适合包含在一个复合对象中。创建对象可能会导致大量的重复代码，可能会需要复合对象访问不到的信息，也可能提供不了足够级别的抽象，还可能并不是复合对象概念的一部分。工厂方法模式通过定义一个单独的创建对象的方法来解决这些问题。由子类实现这个方法来创建具体类型的对象。

对象创建中的有些过程包括决定创建哪个对象、管理对象的生命周期，以及管理特定对象的创建和销毁的概念。[more](https://en.wikipedia.org/wiki/Factory_method_pattern)

### Factory

在面向对象程序设计中，工厂通常是一个用来创建其他对象的对象。工厂是构造方法的抽象，用来实现不同的分配方案。

工厂对象通常包含一个或多个方法，用来创建这个工厂所能创建的各种类型的对象。这些方法可能接收参数，用来指定对象创建的方式，最后返回创建的对象。

有时，特定类型对象的控制过程比简单地创建一个对象更复杂。在这种情况下，工厂对象就派上用场了。工厂对象可能会动态地创建产品对象的类，或者从对象池中返回一个对象，或者对所创建的对象进行复杂的配置，或者应用其他的操作。

这些类型的对象很有用。几个不同的设计模式都应用了工厂的概念，并可以使用在很多语言中。例如，在《设计模式》一书中，像工厂方法模式、抽象工厂模式、生成器模式，甚至是单例模式都应用了工厂的概念。

## Usage

当我们有一个具有多个子类的超类，并且基于输入，我们需要返回其中一个子类时，将使用工厂设计模式。这种模式将类的实例化从客户端程序转移到工厂类。

让我们首先学习如何在java中实现工厂设计模式，然后我们将研究工厂模式的优势。我们将在JDK中看到一些工厂设计模式的使用。请注意，此模式也称为工厂方法设计模式。

### Factory Design Pattern Super Class   

工厂设计模式中的超类可以是接口，抽象类或普通的java类。对于我们的工厂设计模式示例，我们使用带有重写的toString()方法的抽象超类进行测试。

```
package com.journaldev.design.model;

public abstract class Computer {
	
	public abstract String getRAM();
	public abstract String getHDD();
	public abstract String getCPU();
	
	@Override
	public String toString(){
		return "RAM= "+this.getRAM()+", HDD="+this.getHDD()+", CPU="+this.getCPU();
	}
}
```

### Factory Design Pattern Sub Classes

假设我们有两个子类PC和Server，具有以下实现。

```
package com.journaldev.design.model;

public class PC extends Computer {

	private String ram;
	private String hdd;
	private String cpu;
	
	public PC(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public String getRAM() {
		return this.ram;
	}

	@Override
	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}

}
```

请注意，这两个类都在扩展计算机超类。

```
package com.journaldev.design.model;

public class Server extends Computer {

	private String ram;
	private String hdd;
	private String cpu;
	
	public Server(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public String getRAM() {
		return this.ram;
	}

	@Override
	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}

}
```

### Factory Class

现在我们已经准备好了超级类和子类，我们可以编写工厂类。这是基本的实现。

```
package com.journaldev.design.factory;

import com.journaldev.design.model.Computer;
import com.journaldev.design.model.PC;
import com.journaldev.design.model.Server;

public class ComputerFactory {

	public static Computer getComputer(String type, String ram, String hdd, String cpu){
		if("PC".equalsIgnoreCase(type)) return new PC(ram, hdd, cpu);
		else if("Server".equalsIgnoreCase(type)) return new Server(ram, hdd, cpu);
		
		return null;
	}
}
```

关于工厂设计模式方法的一些要点是;

+ 我们可以保持工厂类是单例的，也可以保持返回子类的方法是静态的。
+ 注意，基于输入参数，将创建并返回不同的子类。 getComputer是工厂方法。

## Advantages

+ 工厂模式提供了接口而不是实现的代码方法。
+ 工厂模式从客户端代码中移除实际实现类的实例化。工厂模式使我们的代码更健壮，耦合更少，易于扩展。例如，我们可以很容易地更改PC类实现，因为客户机程序不知道这一点。
+ 工厂模式通过继承提供实现和客户端类之间的抽象。

> 代码健壮性是指软件对于规范要求以外的输入情况的处理能力。所谓健壮的系统是指对于规范要求以外的输入能够判断出这个输入不符合规范要求，并能有合理的处理方式。通俗地讲，代码的健壮性越好，系统越不容易崩溃。

## Factory Design Pattern Examples in JDK

+ java.util.Calendar，ResourceBundle和NumberFormat getInstance()方法使用Factory模式。
+ 包装类中的valueOf()方法，如Boolean，Integer等。

# Abstract Factory Design Pattern in Java

## What is Abstract Factory Design Pattern?

抽象工厂模式（Abstract factory pattern）是一种软件开发设计模式，抽象工厂模式提供了一种方式，可以将一组具有同一主题的单独的工厂封装起来，且无需指定它们具体的实现类。在正常使用中，客户端创建抽象工厂的具体实现，然后使用抽象工厂的通用接口创建作为该主题部分的具体对象。该客户端不需要知道（或关心），它从这些内部的工厂方法中获得对象的具体类型，因为客户端程序仅使用这些对象的通用接口。此模式将一组对象的实现细节与其一般用法分开，并依赖于对象组合，因为对象创建是在工厂界面中公开的方法中实现的。

举个例子来说，比如一个抽象工厂类叫做DocumentCreator（文档创建器），此类提供创建若干种产品的接口，包括createLetter()（创建信件）和createResume()（创建简历）。其中，createLetter()返回一个Letter（信件），createResume()返回一个Resume（简历）。系统中还有一些DocumentCreator的具体实现类，包括FancyDocumentCreator和ModernDocumentCreator。这两个类对DocumentCreator的两个方法分别有不同的实现，用来创建不同的“信件”和“简历”（用FancyDocumentCreator的实例可以创建FancyLetter和FancyResume，用ModernDocumentCreator的实例可以创建ModernLetter和ModernResume）。这些具体的“信件”和“简历”类均继承自抽象类，即Letter和Resume类。客户端需要创建“信件”或“简历”时，先要得到一个合适的DocumentCreator实例，然后调用它的方法。一个工厂中创建的每个对象都是同一个主题的（“fancy”或者“modern”）。客户端程序只需要知道得到的对象是“信件”或者“简历”，而不需要知道具体的主题，因此客户端程序从抽象工厂DocumentCreator中得到了Letter或Resume类的引用，而不是具体类的对象引用。

“工厂”是创建产品（对象）的地方，其目的是将产品的创建与产品的使用分离。抽象工厂模式的目的，是将若干抽象产品的接口与不同主题产品的具体实现分离开。这样就能在增加新的具体工厂的时候，不用修改引用抽象工厂的客户端代码。

使用抽象工厂模式，能够在具体工厂变化的时候，不用修改使用工厂的客户端代码，甚至是在运行时。然而，使用这种模式或者相似的设计模式，可能给编写代码带来不必要的复杂性和额外的工作。正确使用设计模式能够抵消这样的“额外工作”。[more](https://en.wikipedia.org/wiki/Abstract_factory_pattern)

## Usage

如果熟悉java中的工厂设计模式，会注意到我们有一个Factory类。此工厂类根据提供的输入返回不同的子类，工厂类使用if-else或switch语句来实现此目的。

在抽象工厂模式中，我们摆脱if-else块并为每个子类设置工厂类。然后是一个Abstract Factory类，它将根据输入工厂类返回子类。起初，它似乎令人困惑但是一旦你看到实现，就很容易理解和理解Factory和Abstract Factory模式之间的细微差别。


### Abstract Factory Design Pattern Super Class and Subclasses

就像工厂模式一样，我们将使用相同的超类和子类。

```
package com.journaldev.design.model;
 
public abstract class Computer {
     
    public abstract String getRAM();
    public abstract String getHDD();
    public abstract String getCPU();
     
    @Override
    public String toString(){
        return "RAM= "+this.getRAM()+", HDD="+this.getHDD()+", CPU="+this.getCPU();
    }
}
```

```
package com.journaldev.design.model;
 
public class PC extends Computer {
 
    private String ram;
    private String hdd;
    private String cpu;
     
    public PC(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
    }
    @Override
    public String getRAM() {
        return this.ram;
    }
 
    @Override
    public String getHDD() {
        return this.hdd;
    }
 
    @Override
    public String getCPU() {
        return this.cpu;
    }
 
}
```

```
package com.journaldev.design.model;
 
 
public class Server extends Computer {
 
    private String ram;
    private String hdd;
    private String cpu;
     
    public Server(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
    }
    @Override
    public String getRAM() {
        return this.ram;
    }
 
    @Override
    public String getHDD() {
        return this.hdd;
    }
 
    @Override
    public String getCPU() {
        return this.cpu;
    }
 
}
```

### Factory Class for Each subclass

首先，我们需要创建一个Abstract Factory接口或抽象类。

```
package com.journaldev.design.abstractfactory;

import com.journaldev.design.model.Computer;

public interface ComputerAbstractFactory {

	public Computer createComputer();

}
```

注意，createComputer()方法正在返回超类计算机的实例。现在我们的工厂类将实现此接口并返回其各自的子类。

```
package com.journaldev.design.abstractfactory;

import com.journaldev.design.model.Computer;
import com.journaldev.design.model.PC;

public class PCFactory implements ComputerAbstractFactory {

	private String ram;
	private String hdd;
	private String cpu;
	
	public PCFactory(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public Computer createComputer() {
		return new PC(ram,hdd,cpu);
	}

}
```

类似地，我们将为服务器子类创建一个工厂类。

```
package com.journaldev.design.abstractfactory;

import com.journaldev.design.model.Computer;
import com.journaldev.design.model.Server;

public class ServerFactory implements ComputerAbstractFactory {

	private String ram;
	private String hdd;
	private String cpu;
	
	public ServerFactory(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	
	@Override
	public Computer createComputer() {
		return new Server(ram,hdd,cpu);
	}

}
```

现在我们将创建一个 consumer 类，它将为客户端类提供创建子类的入口点。

```
package com.journaldev.design.abstractfactory;

import com.journaldev.design.model.Computer;

public class ComputerFactory {

	public static Computer getComputer(ComputerAbstractFactory factory){
		return factory.createComputer();
	}
}
```

请注意，它是一个简单的类和有一个getComputer方法，它接受ComputerAbstractFactory参数并返回Computer对象。此时，方法必须要实现。

让我们编写一个简单的测试方法，看看如何使用抽象工厂来获取子类的实例。

```
package com.journaldev.design.test;

import com.journaldev.design.abstractfactory.PCFactory;
import com.journaldev.design.abstractfactory.ServerFactory;
import com.journaldev.design.factory.ComputerFactory;
import com.journaldev.design.model.Computer;

public class TestDesignPatterns {

	public static void main(String[] args) {
		testAbstractFactory();
	}

	private static void testAbstractFactory() {
		Computer pc = com.journaldev.design.abstractfactory.ComputerFactory.getComputer(new PCFactory("2 GB","500 GB","2.4 GHz"));
		Computer server = com.journaldev.design.abstractfactory.ComputerFactory.getComputer(new ServerFactory("16 GB","1 TB","2.9 GHz"));
		System.out.println("AbstractFactory PC Config::"+pc);
		System.out.println("AbstractFactory Server Config::"+server);
	}
}
```

## Advantages

+ 抽象工厂模式提供了接口而不是实现代码的方法。
+ 抽象工厂模式是“工厂中的工厂”，可以很容易地扩展以适应更多的产品，例如，我们可以添加另一个子类笔记本电脑和一个笔记本电脑工厂。
+ 抽象的工厂模式是健壮的，避免了工厂模式的条件逻辑。

## Abstract Factory Design Pattern Examples in JDK

+ javax.xml.parsers.DocumentBuilderFactory#newInstance()
+ javax.xml.transform.TransformerFactory#newInstance()
+ javax.xml.xpath.XPathFactory#newInstance()

# Singleton Design Pattern in Java

## What is Singleton Design Pattern?

单例模式（Singleton Design Pattern）是一种常用的软件设计模式。在应用这个模式时，单例对象的类必须保证只有一个实例存在。许多时候整个系统只需要拥有一个的全局对象，这样有利于我们协调系统整体的行为。比如在某个服务器程序中，该服务器的配置信息存放在一个文件中，这些配置数据由一个单例对象统一读取，然后服务进程中的其他对象再通过这个单例对象获取这些配置信息。这种方式简化了在复杂环境下的配置管理。

实现单例模式的思路是：一个类能返回对象一个引用(永远是同一个)和一个获得该实例的方法（必须是静态方法，通常使用getInstance这个名称）；当我们调用这个方法时，如果类持有的引用不为空就返回这个引用，如果类保持的引用为空就创建该类的实例并将实例的引用赋予该类保持的引用；同时我们还将该类的构造函数定义为私有方法，这样其他处的代码就无法通过调用该类的构造函数来实例化该类的对象，只有通过该类提供的静态方法来得到该类的唯一实例。

单例模式在多线程的应用场合下必须小心使用。如果当唯一实例尚未创建时，有两个线程同时调用创建方法，那么它们同时没有检测到唯一实例的存在，从而同时各自创建了一个实例，这样就有两个实例被构造出来，从而违反了单例模式中实例唯一的原则。 解决这个问题的办法是为指示类是否已经实例化的变量提供一个互斥锁(虽然这样会降低效率)。[more](https://en.wikipedia.org/wiki/Singleton_pattern)

总结为以下几点：

+ Singleton模式限制类的实例化，并确保java虚拟机中只存在该类的一个实例。
+ 单例类必须提供一个全局访问点来获取类的实例。
+ 单例模式用于日志记录，驱动程序对象，缓存和线程池。
+ Singleton设计模式也用于其他设计模式，如Abstract Factory，Builder，Prototype，Facade等。
+ 例如java.lang.Runtime，单核设计模式也用于核心java类中java.awt.Desktop。


## Usage

为了实现Singleton模式，我们有不同的方法，但它们都有以下常见概念：

+ 私有构造函数，用于限制其他类的实例化。
+ 同一个类的私有静态变量，它是该类的唯一实例。
+ 返回类实例的公共静态方法，这是外部世界获取单例类实例的全局访问点。

Singleton模式有以下实现的不同方法以及设计实现的不同关注点：

+ Eager initialization
+ Static block initialization
+ Lazy Initialization
+ Thread Safe Singleton
+ Bill Pugh Singleton Implementation
+ Using Reflection to destroy Singleton Pattern
+ Enum Singleton
+ Serialization and Singleton

### Eager Initialization

在 Eager Initialization (即时初始化) 中，单例类的实例是在类加载时创建的，这是创建单例类最简单的方法，但它有一个缺点，即使客户端应用程序可能不使用它，也会创建实例。

下面是静态初始化singleton类的实现
```
package com.journaldev.singleton;

public class EagerInitializedSingleton {
    
    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();
    
    //private constructor to avoid client applications to use constructor
    private EagerInitializedSingleton(){}

    public static EagerInitializedSingleton getInstance(){
        return instance;
    }
}
```

如果单例类没有使用很多资源，那么可以使用这种方法。但是在大多数情况下，单例类是为资源(如文件系统、数据库连接等)创建的。我们应该避免实例化，除非客户端调用getInstance方法。此外，此方法不提供任何异常处理选项。

### Static block initialization

Static block initialization (静态块初始化) 实现类似于 Eager Initialization (即时初始化)，除了在静态块中创建类的实例，该静态块提供异常处理选项。

```
package com.journaldev.singleton;

public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;
    
    private StaticBlockSingleton(){}
    
    //static block initialization for exception handling
    static{
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }
    
    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
```

即时初始化和静态块初始化都是在实例被使用之前创建的，这不是最佳实践。因此，在接下来的部分中，我们将学习如何创建一个支持延迟初始化的单例类。

[Static Keyword](https://www.journaldev.com/1365/static-keyword-in-java)

### Lazy Initialization

实现单例模式的 Lazy Initialization (延迟初始化) 在全局访问方法中创建实例。下面是使用这种方法创建单例类的示例代码。

```
package com.journaldev.singleton;

public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;
    
    private LazyInitializedSingleton(){}
    
    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```

上面的实现在单线程环境中工作得很好，但是当涉及到多线程系统时，如果多个线程同时在if条件中，它可能会导致问题。它将破坏单例模式，两个线程都将获得单例类的不同实例。在下一节中，我们将看到创建线程安全的单例类的不同方法。

### Thread Safe Singleton

创建线程安全的单例类的更简单方法是使全局访问方法同步，以便一次只有一个线程可以执行此方法。这种方法的一般实现类似于下面的类。

```
package com.journaldev.singleton;

public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static synchronized ThreadSafeSingleton getInstance(){
        if(instance == null){
            instance = new ThreadSafeSingleton();i
        }
        return instance;
    }
    
}
```

上面的实现工作得很好，并提供了线程安全，但是由于与synchronized方法相关的成本，它降低了性能，尽管我们只需要它来处理可能创建单独实例的前几个线程(即:Java同步)。为了避免每次额外的开销，使用了双重检查锁定原则。在这种方法中，同步块在if条件中使用，并附加一个检查，以确保只创建了一个单例类的实例。

下面的代码片段提供了双重检查的锁定实现。

```
public static ThreadSafeSingleton getInstanceUsingDoubleLocking(){
    if(instance == null){
        synchronized (ThreadSafeSingleton.class) {
            if(instance == null){
                instance = new ThreadSafeSingleton();
            }
        }
    }
    return instance;
}
```

[Thread Safety in Java Singleton](https://www.journaldev.com/1377/java-singleton-design-pattern-best-practices-examples)

### Bill Pugh Singleton Implementation

在Java 5之前，Java内存模型有很多问题，在某些情况下，如果有太多线程试图同时获取Singleton类的实例，那么上面的方法就会失败。因此Bill Pugh提出了一种不同的方法来使用内部静态助手类创建单例类。Bill Pugh单例实现是这样的;

```
package com.journaldev.singleton;

public class BillPughSingleton {

    private BillPughSingleton(){}
    
    private static class SingletonHelper{
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }
    
    public static BillPughSingleton getInstance(){
        return SingletonHelper.INSTANCE;
    }
}
```

请注意包含singleton类实例的私有内部静态类。加载单例类时，SingletonHelper类不会加载到内存中，只有当有人调用getInstance方法时，才会加载此类并创建Singleton类实例。

这是Singleton类最广泛使用的方法，因为它不需要同步。许多项目中使用这种方法，它也很容易理解和实现。

[Java Inner Class](https://www.journaldev.com/996/java-inner-class)

### Using Reflection to destroy Singleton Pattern

反射可用于销毁所有上述单例实现方法。让我们看一下示例类。

```
public class ReflectionSingletonTest {

    public static void main(String[] args) {
        EagerInitializedSingleton instanceOne = EagerInitializedSingleton.getInstance();
        EagerInitializedSingleton instanceTwo = null;
        try {
            Constructor[] constructors = EagerInitializedSingleton.class.getDeclaredConstructors();
            for (Constructor constructor : constructors) {
                //Below code will destroy the singleton pattern
                constructor.setAccessible(true);
                instanceTwo = (EagerInitializedSingleton) constructor.newInstance();
                break;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println(instanceOne.hashCode());
        System.out.println(instanceTwo.hashCode());
    }

}
```

当运行上面的测试类时，会注意到两个实例的hashCode与销毁单例模式的方法不同。反射是非常强大的，并且在很多框架中使用，比如Spring和Hibernate.

[Java Reflection Tutorial](https://www.journaldev.com/1789/java-reflection-example-tutorial)。

### Enum Singleton

Joshua Bloch 在 Effect java 中建议使用Enum来实现Singleton设计模式，因为Java确保任何枚举值只在Java程序中实例化一次。由于Java Enum值是全局可访问的，因此单例也是如此。缺点是枚举类型有些不灵活; 例如，它不允许延迟初始化。

```
package com.journaldev.singleton;

public enum EnumSingleton {

    INSTANCE;
    
    public static void doSomething(){
        //do something
    }
}
```

[Java Enum](https://www.journaldev.com/716/java-enum)

### Serialization and Singleton

有时在分布式系统中，我们需要在Singleton类中实现Serializable接口，以便我们可以将其状态存储在文件系统中并在以后的时间点检索它。这是一个小型单例类，它也实现了Serializable接口。

```
package com.journaldev.singleton;

import java.io.Serializable;

public class SerializedSingleton implements Serializable{

    private static final long serialVersionUID = -7604766932017737115L;

    private SerializedSingleton(){}
    
    private static class SingletonHelper{
        private static final SerializedSingleton instance = new SerializedSingleton();
    }
    
    public static SerializedSingleton getInstance(){
        return SingletonHelper.instance;
    }
    
}
```

序列化单例类的问题在于，每当我们反序列化它时，它将创建该类的新实例。让我们用一个简单的程序来看。

```
package com.journaldev.singleton;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInput;
import java.io.ObjectInputStream;
import java.io.ObjectOutput;
import java.io.ObjectOutputStream;

public class SingletonSerializedTest {

    public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {
        SerializedSingleton instanceOne = SerializedSingleton.getInstance();
        ObjectOutput out = new ObjectOutputStream(new FileOutputStream(
                "filename.ser"));
        out.writeObject(instanceOne);
        out.close();
        
        //deserailize from file to object
        ObjectInput in = new ObjectInputStream(new FileInputStream(
                "filename.ser"));
        SerializedSingleton instanceTwo = (SerializedSingleton) in.readObject();
        in.close();
        
        System.out.println("instanceOne hashCode="+instanceOne.hashCode());
        System.out.println("instanceTwo hashCode="+instanceTwo.hashCode());
        
    }

}
```

上述程序的输出是;
```
instanceOne hashCode=2011117821
instanceTwo hashCode=109647522
```

所以它破坏了单例模式，为了克服这种情况我们需要做的就是提供readResolve()方法的实现。

```
protected Object readResolve() {
    return getInstance();
}
```

在此之后，您会注意到两个实例的hashCode在测试程序中是相同的。

[Java Serialization](https://www.journaldev.com/927/objectoutputstream-java-write-object-file) 和 [Java Deserialization](https://www.journaldev.com/933/objectinputstream-java-read-object-file)

# Multiton Pattern in Java

## What is Multiton Pattern?
。 

在软件工程中，Multiton模式是一种对单例模式进行推广的设计模式。虽然Singleton模式只允许创建类的一个实例，但是Multiton模式允许受控地创建多个实例，它通过使用映射来管理这些实例。

Multiton模式是Singleton模式的扩展和增强版本。正如模式的名称所示，Multiton模式只不过是类的实例集合的预定义“n”，而Singleton类只有一个实例。Multiton模式（类）使用哈希或字典对实例列表进行分组。列表中的每个实例都与相应的密钥配对。通过使用密钥，相应的实例将返回到调用代码

大多数人和教科书都认为这是一种Singleton模式。例如，Multiton并没有显式地出现在备受推崇的面向对象编程教科书《设计模式》(Design Patterns)中(它是一种名为registry of singletons的更灵活的方法)。

虽然看起来多例只不过是一个具有同步访问的简单哈希表，但是有两个重要的区别。首先，Multiton不允许客户机添加映射。其次，多例从不返回空引用或空引用;相反，它使用关联键在第一个请求上创建并存储一个多实例。具有相同键的后续请求将返回原始实例。哈希表只是一个实现细节，而不是唯一可能的方法。该模式简化了应用程序中共享对象的检索。

由于对象池只创建一次，并且是与类(而不是实例)关联的成员，因此,Multiton保留了其扁平的行为，而不是演化为树结构。

Multiton是唯一的，因为它提供了对Multiton的单个目录(即所有键本身都在同一个名称空间中)的集中访问，其中池中的每个Multiton实例可能都有自己的状态。通过这种方式，模式提倡对系统的基本对象(例如LDAP系统提供的对象)进行索引存储。然而，Multiton仅限于单个系统的广泛使用，而不是无数的分布式系统。

Multiton模式的特点:
+ 多例模式可以有多个实例
+ 多例类必须自己创建、管理自己的实例，并向外界提供自己的实例，因此，他的构造函数也是private的，这点跟单例模式是相同的
+ 更具是否有上限分为：有上限多例类和无上限多例类。
+ 多例模式往往具有一个聚集属性，通过向这个聚集属性登记已经创建过的实例达到循环使用实例的目的

Multiton模式的缺陷：
+ 像Singleton模式一样，这种模式使单元测试变得更加困难，因为它将全局状态引入应用程序。
+ 使用垃圾收集语言，它可能成为内存泄漏的来源，因为它引入了对对象的全局强引用。

## Example

```
package at.gridtec.multiton;

import java.util.ArrayList;
import java.util.List;

public class Multiton {

    private static final int NUM_OF_INSTANCES = 5;
    private static final List<Multiton> instanceList = new ArrayList<Multiton>(); 
    private static int instanceCount = 0;
    private int instanceNum;

    private Multiton() {

    }

    public static synchronized Multiton getInstance() {

        Multiton instance = null;

        if (instanceList.size() == NUM_OF_INSTANCES) {
            instance = instanceList.get(instanceCount % NUM_OF_INSTANCES);
        } else {
            instance = new Multiton();
            instance.instanceNum = instanceList.size() + 1;
            instanceList.add(instance);
        }

        instanceCount++;
        return instance;
    }


    public int getInstanceNum() {
        return instanceNum;
    }

    /**
     * for testing purposes
     */
    public String toString() {
        return "Multiton Number: " + getInstanceNum();
    }

}
```

test
```
package at.gridtec.multiton;

public class MutlitonTest {

    public static void main(String args[]) {
        for (int i = 0; i < 25; i++) {
            System.out.println(Multiton.getInstance());
            if (Multiton.getInstance().getInstanceNum() > 5) {
                break;
            }
        }
    }
    
}
```

# Builder Design Pattern in Java

## What is Builder Design Pattern?

Builder设计模式是二十三种着名的GoF设计模式之一，描述了如何解决面向对象软件中的重复设计问题。

当Object包含许多属性时，Factory和Abstract Factory设计模式存在三个主要问题。

+ 从客户端程序传递到Factory类的参数太多，可能容易出错，因为大多数情况下，参数的类型是相同的，而从客户端来说，很难维护参数的顺序。
+ 一些参数可能是可选的，但在Factory模式中，我们被迫发送所有需要发送为NULL的参数和可选参数。
+ 如果对象很重并且它的创建很复杂，那么所有这些复杂性将成为Factory类的一部分，这会令人困惑。

我们可以通过提供具有所需参数的构造函数然后使用不同的setter方法来设置可选参数来解决大量参数的问题。这种方法的问题是，除非明确设置所有属性，否则Object状态将不一致。

Builder模式通过提供逐步构建对象的方法并提供实际返回最终Object的方法，解决了大量可选参数和不一致状态的问题。

Builder设计模式的目的是将复杂 Object 的构造与其表示分开。通过这样做，相同的构造过程可以创建不同的表示。类（相同的构造过程）可以委托给不同的Builder对象来创建复杂对象的不同表示。

## Usage

如何在java中实现构建器设计模式。

+ 首先，需要创建一个静态嵌套类，然后将所有参数从外部类复制到Builder类。我们应该遵循命名约定，如果类名是，Computer那么构建器类应该命名为ComputerBuilder。
+ Java Builder类应该有一个公共构造函数，其中包含所有必需的属性作为参数。
+ Java Builder类应具有设置可选参数的方法，并且应在设置可选属性后返回相同的Builder对象。
+ 最后一步是build()在构建器类中提供一个方法，该方法将返回客户端程序所需的Object。为此，我们需要在Class中使用Builder类作为参数的私有构造函数。

下面是示例构建器模式示例代码，其中我们有一个Computer类和ComputerBuilder类来构建它:
```
package com.journaldev.design.builder;

public class Computer {
	
	//required parameters
	private String HDD;
	private String RAM;
	
	//optional parameters
	private boolean isGraphicsCardEnabled;
	private boolean isBluetoothEnabled;
	

	public String getHDD() {
		return HDD;
	}

	public String getRAM() {
		return RAM;
	}

	public boolean isGraphicsCardEnabled() {
		return isGraphicsCardEnabled;
	}

	public boolean isBluetoothEnabled() {
		return isBluetoothEnabled;
	}
	
	private Computer(ComputerBuilder builder) {
		this.HDD=builder.HDD;
		this.RAM=builder.RAM;
		this.isGraphicsCardEnabled=builder.isGraphicsCardEnabled;
		this.isBluetoothEnabled=builder.isBluetoothEnabled;
	}
	
	//Builder Class
	public static class ComputerBuilder{

		// required parameters
		private String HDD;
		private String RAM;

		// optional parameters
		private boolean isGraphicsCardEnabled;
		private boolean isBluetoothEnabled;
		
		public ComputerBuilder(String hdd, String ram){
			this.HDD=hdd;
			this.RAM=ram;
		}

		public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
			this.isGraphicsCardEnabled = isGraphicsCardEnabled;
			return this;
		}

		public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {s
			this.isBluetoothEnabled = isBluetoothEnabled;
			return this;
		}
		
		public Computer build(){
			return new Computer(this);
		}

	}

}
```

请注意，Computer类只有getter方法，没有公共构造函数。因此，获取Computer对象的唯一方法是通过ComputerBuilder类。

这是一个构建器模式示例测试程序，显示如何使用Builder类来获取对象:

```
package com.journaldev.design.test;

import com.journaldev.design.builder.Computer;

public class TestBuilderPattern {

	public static void main(String[] args) {
		//Using builder to get the object in a single line of code and 
                //without any inconsistent state or arguments management issues		
		Computer comp = new Computer.ComputerBuilder(
				"500 GB", "2 GB").setBluetoothEnabled(true)
				.setGraphicsCardEnabled(true).build();
	}

}
```

# Dependency injection in Java

## What is Dependency Injection?

在软件工程中，依赖注入是一种技术，一个对象（或静态方法）提供另一个对象的依赖性。依赖项是可以使用的对象（服务）。注入是将依赖项传递给将使用它的依赖对象（客户端）。该服务是客户所在的一部分。将服务传递给客户端，而不是允许客户端构建或找到服务，是模式的基本要求。

依赖注入的目的是将对象解耦到不需要更改客户端代码的程度，因为它所依赖的对象需要更改为另一个。这允许遵循开放/封闭原则。

依赖注入是更广泛的控制反转技术的一种形式。与其他形式的控制反转一样，依赖注入支持依赖性反转原则。客户端将其依赖关系的责任委托给外部代码（注入器）。客户端不允许调用注入器代码; 它是构建服务并调用客户端注入它们的注入代码。这意味着客户端代码不需要知道注入代码，如何构建服务，甚至不知道它正在使用哪些实际服务; 客户端只需要知道服务的内在接口，因为它们定义了客户端如何使用服务。这分离了使用和构造的责任。

客户端接受依赖注入有三种常用方法：setter- ，interface- 和 constructor-based injection 。Setter 和 constructor-based injection 主要取决于它们何时可以使用。interface 注入的不同之处在于依赖关系有机会控制其自身的注入。每个都要求单独的构造代码（注入器）负责将客户端及其依赖关系引入彼此。

在Java中依赖注入设计模式允许我们删除硬编码的依赖项，并使我们的应用程序松散耦合，可扩展和可维护。我们可以在java中实现依赖注入，以将依赖项解析从编译时移动到运行时。

## Usage

假设我们有一个EmailService用于发送电子邮件的应用程序。通常我们会像下面这样实现它：
```
package com.journaldev.java.legacy;

public class EmailService {

	public void sendEmail(String message, String receiver){
		//logic to send email
		System.out.println("Email sent to "+receiver+ " with Message="+message);
	}
}
```

EmailService类保存将电子邮件消息发送到收件人电子邮件地址的逻辑。我们的应用程序代码如下所示。

```
package com.journaldev.java.legacy;

public class MyApplication {

	private EmailService email = new EmailService();
	
	public void processMessages(String msg, String rec){
		//do some msg validation, manipulation logic etc
		this.email.sendEmail(msg, rec);
	}
}
```

初看起来，上面的实现似乎没有错。但上面的代码逻辑有一定的局限性。

+ MyApplicationclass负责初始化电子邮件服务，然后使用它。这导致了硬编码的依赖性。如果我们希望将来切换到其他一些高级电子邮件服务，则需要在MyApplication类中进行代码更改。这使我们的应用程序难以扩展，如果在多个类中使用电子邮件服务，那将更加困难。
+ 如果我们想扩展我们的应用程序以提供其他消息传递功能，例如SMS或Facebook消息，那么我们需要为此编写另一个应用程序。这将涉及应用程序类和客户端类中的代码更改。
+ 由于我们的应用程序直接创建电子邮件服务实例，因此测试应用程序将非常困难。我们无法在测试类中模拟这些对象。

有人可能会说，我们可以通过一个构造函数将电子邮件服务作为参数来从MyApplication类中删除电子邮件服务实例的创建。

```
package com.journaldev.java.legacy;

public class MyApplication {

	private EmailService email = null;
	
	public MyApplication(EmailService svc){
		this.email=svc;
	}
	
	public void processMessages(String msg, String rec){
		//do some msg validation, manipulation logic etc
		this.email.sendEmail(msg, rec);
	}
}
```

但在这种情况下，我们要求客户端应用程序或测试类的初始化，这不是一个好的电子邮件服务的设计策略。

现在让我们看看我们如何应用java依赖注入模式来解决上述实现的所有问题。 java中的依赖注入至少需要以下内容：

+ 服务组件应该使用基类或接口进行设计。最好选择定义服务契约的接口或抽象类。
+ 使用者类应该根据服务接口编写。
+ 注入器类，它将初始化服务，然后初始化使用者类。

### Service Components

我们可以使用MessageService来声明服务实现的契约：

```
package com.journaldev.java.dependencyinjection.service;

public interface MessageService {

	void sendMessage(String msg, String rec);
}
```

实现上述接口的电子邮件和SMS服务：

```
package com.journaldev.java.dependencyinjection.service;

public class EmailServiceImpl implements MessageService {

	@Override
	public void sendMessage(String msg, String rec) {
		//logic to send email
		System.out.println("Email sent to "+rec+ " with Message="+msg);
	}

}
```

```
package com.journaldev.java.dependencyinjection.service;

public class SMSServiceImpl implements MessageService {

	@Override
	public void sendMessage(String msg, String rec) {
		//logic to send SMS
		System.out.println("SMS sent to "+rec+ " with Message="+msg);
	}

}
```

### Service Consumer

我们不需要为使用者类提供基接口，但是需要为使用者类提供一个声明契约的使用者接口。

```
package com.journaldev.java.dependencyinjection.consumer;

public interface Consumer {

	void processMessages(String msg, String rec);
}
```

使用者类的实现如下:

```
package com.journaldev.java.dependencyinjection.consumer;

import com.journaldev.java.dependencyinjection.service.MessageService;

public class MyDIApplication implements Consumer{

	private MessageService service;
	
	public MyDIApplication(MessageService svc){
		this.service=svc;
	}
	
	@Override
	public void processMessages(String msg, String rec){
		//do some msg validation, manipulation logic etc
		this.service.sendMessage(msg, rec);
	}

}
```

注意，我们的应用程序类只是在引用服务。它没有初始化导致它成为了一个“关注点分离”的服务。服务接口的使用还允许我们通过模拟MessageService轻松地测试应用程序，并在运行时而不是编译时绑定服务。

> 关注点分离（Separation of concerns，SOC）是对只与“特定概念、目标”（关注点）相关联的软件组成部分进行“标识、封装和操纵”的能力，即标识、封装和操纵关注点的能力。是处理复杂性的一个原则。由于关注点混杂在一起会导致复杂性大大增加，所以能够把不同的关注点分离开来，分别处理就是处理复杂性的一个原则，一种方法。<br/>关注点分离在计算机科学中，是将计算机程序分隔为不同部分的设计原则，是面向对象的程序设计的核心概念。每一部分会有各自的关注焦点。关注焦点是影响计算机程式代码的一组资讯。关注焦点可以像是将代码优化过的硬件细节一般，或者像实例化类别的名称一样具体。展现关注点分离设计的程序被称为模组化程序。模组化程度，也就是区分关注焦点，通过将资讯封装在具有明确界面的程序代码段落中。封装是一种资讯隐藏手段。资讯系统中的分层设计是关注点分离的另一个实施例（例如，表示层，业务逻辑层，数据访问层，维持齐一层）。分离关注点使得解决特定领域问题的代码从业务逻辑中独立出来，业务逻辑的代码中不再含有针对特定领域问题代码的调用（将针对特定领域问题代码抽象化成较少的程式码，例如将代码封装成function或是class），业务逻辑同特定领域问题的关系通过侧面来封装、维护，这样原本分散在整个应用程序中的变动就可以很好的管理起来。

现在，我们准备编写java依赖注入器类，这些类将初始化服务和使用者类。

### Injectors Classes

让我们有一个带有返回使用者类的方法声明的接口MessageServiceInjector。

```
package com.journaldev.java.dependencyinjection.injector;

import com.journaldev.java.dependencyinjection.consumer.Consumer;

public interface MessageServiceInjector {

	public Consumer getConsumer();
}
```

现在，对于每个服务，我们都必须创建下面这样的注入器类。

```
package com.journaldev.java.dependencyinjection.injector;

import com.journaldev.java.dependencyinjection.consumer.Consumer;
import com.journaldev.java.dependencyinjection.consumer.MyDIApplication;
import com.journaldev.java.dependencyinjection.service.EmailServiceImpl;

public class EmailServiceInjector implements MessageServiceInjector {

	@Override
	public Consumer getConsumer() {
		return new MyDIApplication(new EmailServiceImpl());
	}

}
```

```
package com.journaldev.java.dependencyinjection.injector;

import com.journaldev.java.dependencyinjection.consumer.Consumer;
import com.journaldev.java.dependencyinjection.consumer.MyDIApplication;
import com.journaldev.java.dependencyinjection.service.SMSServiceImpl;

public class SMSServiceInjector implements MessageServiceInjector {

	@Override
	public Consumer getConsumer() {
		return new MyDIApplication(new SMSServiceImpl());
	}

}
```

现在让我们看看我们的客户端应用程序将如何在一个简单的程序中使用该应用程序。

```
package com.journaldev.java.dependencyinjection.test;

import com.journaldev.java.dependencyinjection.consumer.Consumer;
import com.journaldev.java.dependencyinjection.injector.EmailServiceInjector;
import com.journaldev.java.dependencyinjection.injector.MessageServiceInjector;
import com.journaldev.java.dependencyinjection.injector.SMSServiceInjector;

public class MyMessageDITest {

	public static void main(String[] args) {
		String msg = "Hi Pankaj";
		String email = "pankaj@abc.com";
		String phone = "4088888888";
		MessageServiceInjector injector = null;
		Consumer app = null;
		
		//Send email
		injector = new EmailServiceInjector();
		app = injector.getConsumer();
		app.processMessages(msg, email);
		
		//Send SMS
		injector = new SMSServiceInjector();
		app = injector.getConsumer();
		app.processMessages(msg, phone);
	}

}
```

如您所见，我们的应用程序类只负责使用服务。服务类是在注入器中创建的。另外，如果我们必须进一步扩展我们的应用程序以允许facebook消息传递，我们将只编写服务类和注入器类。

因此，依赖注入实现解决了硬编码依赖的问题，并帮助我们使应用程序更加灵活和易于扩展。现在让我们看看如何通过模拟注入器和服务类来轻松地测试应用程序类。

### JUnit Test Case with Mock Injector and Service

```
package com.journaldev.java.dependencyinjection.test;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import com.journaldev.java.dependencyinjection.consumer.Consumer;
import com.journaldev.java.dependencyinjection.consumer.MyDIApplication;
import com.journaldev.java.dependencyinjection.injector.MessageServiceInjector;
import com.journaldev.java.dependencyinjection.service.MessageService;

public class MyDIApplicationJUnitTest {

	private MessageServiceInjector injector;
	@Before
	public void setUp(){
		//mock the injector with anonymous class
		injector = new MessageServiceInjector() {
			
			@Override
			public Consumer getConsumer() {
				//mock the message service
				return new MyDIApplication(new MessageService() {
					
					@Override
					public void sendMessage(String msg, String rec) {
						System.out.println("Mock Message Service implementation");
						
					}
				});
			}
		};
	}
	
	@Test
	public void test() {
		Consumer consumer = injector.getConsumer();
		consumer.processMessages("Hi Pankaj", "pankaj@abc.com");
	}
	
	@After
	public void tear(){
		injector = null;
	}

}
```

正如您所看到的，我正在使用匿名类来模拟注入器和服务类，并且我可以轻松地测试我的应用程序方法。

我们已经使用构造函数注入应用程序类中的依赖项，另一种方法是使用setter方法注入应用程序类中的依赖项。对于setter方法依赖注入，我们的应用程序类将实现如下所示。

```
package com.journaldev.java.dependencyinjection.consumer;

import com.journaldev.java.dependencyinjection.service.MessageService;

public class MyDIApplication implements Consumer{

	private MessageService service;
	
	public MyDIApplication(){}

	//setter dependency injection	
	public void setService(MessageService service) {
		this.service = service;
	}

	@Override
	public void processMessages(String msg, String rec){
		//do some msg validation, manipulation logic etc
		this.service.sendMessage(msg, rec);
	}

}
```

```
package com.journaldev.java.dependencyinjection.injector;

import com.journaldev.java.dependencyinjection.consumer.Consumer;
import com.journaldev.java.dependencyinjection.consumer.MyDIApplication;
import com.journaldev.java.dependencyinjection.service.EmailServiceImpl;

public class EmailServiceInjector implements MessageServiceInjector {

	@Override
	public Consumer getConsumer() {
		MyDIApplication app = new MyDIApplication();
		app.setService(new EmailServiceImpl());
		return app;
	}

}
```

setter依赖注入的最佳示例之一是Struts2 Servlet API感知接口。

使用基于构造函数的依赖注入还是基于setter是一个设计决策，这取决于您的需求。例如，如果我的应用程序在没有服务类的情况下无法工作，那么我更喜欢基于构造函数的DI，否则我将使用基于DI的setter方法，只在真正需要时才使用它。

Java中的依赖注入是通过将对象绑定从编译时移动到运行时来实现应用程序中的控制反转(IoC)的一种方法。通过工厂模式、模板方法设计模式、策略模式和服务定位模式来实现IoC。

[Spring依赖项注入](https://www.journaldev.com/2410/spring-dependency-injection)、[谷歌Guice](https://www.journaldev.com/2403/google-guice-dependency-injection-example-tutorial)和Java EE CDI框架通过使用Java反射API和Java注解简化了依赖项注入的过程。我们只需要注解字段、构造函数或setter方法，并在配置xml文件或类中配置它们。

## Advantages

+ Separation of Concerns(关注点分离)
+ 在应用程序类中减少样板代码，因为初始化依赖项的所有工作都由注入器组件处理
+ 可配置组件使应用程序易于扩展
+ 使用模拟对象进行单元测试很容易

## Disadvantages

+ 如果过度使用，可能会导致维护问题，因为更改的效果在运行时是已知的。
+ java中的依赖项注入隐藏了服务类依赖项，这些依赖项可能导致在编译时捕获的运行时错误。

# Lazy Initialization in Java

## What is Lazy Initialization?

在计算机编程中，延迟初始化是一种策略，它将对象的创建、值的计算或其他一些开销很大的进程延迟到第一次需要它的时候。它是一种惰性计算，在引用对象或其他比较大的资源实例化时使用。

延迟初始化通常是通过增加访问器方法(或属性的getter)来完成，检查充当缓存的私有成员是否已经初始化。如果有，则立即返回。如果没有，则创建一个新实例，将其放入成员变量中，并在第一次使用时及时返回给调用者。

如果对象具有很少使用的属性，这可以提高启动速度。这意味着对于平均性能可能稍差的程序,可以大大提高平均响应时间，因为对于对象实例化的影响是随实例化时间扩展（“摊销”）的而不是集中在系统的启动阶段。

在多线程代码中，必须同步对延迟初始化对象/状态的访问以防止竞争条件。

在软件设计模式中，延迟初始化通常与工厂方法模式一起使用。这其中结合了三种设计模式：
+ 使用工厂方法创建类的实例(factory method pattern)
+ 将实例存储在Map中，并将相同的实例返回给具有相同参数的实例的请求(multiton pattern)
+ 在第一次请求对象时使用延迟初始化来实例化它(lazy initialization pattern)

## Usage

延迟初始化的使用主要分为两种：
+ Lazy class loading (延迟类加载)
+ Lazy object creation (延迟对象创建)

### Lazy class loading

Java运行时内置了类的延迟实例化。类只有在第一次引用时才加载到内存中。(它们也可以首先通过HTTP从Web服务器加载。)

延迟类加载是Java运行时环境的一个重要特性，因为它可以在某些情况下减少内存使用。例如，如果一个程序的某个部分从来没有在一个会话期间执行过，那么只在该部分中引用的类将永远不会被加载。

### Lazy object creation

延迟对象创建与延迟类加载紧密耦合。第一次在以前未加载的类类型上使用new关键字时，Java运行时将为您加载它。与延迟类加载相比，延迟对象创建可以在更大程度上减少内存使用。

为了介绍延迟对象创建的概念，让我们看一个简单的代码示例，其中一个框架使用一个MessageBox来显示错误消息:

```
public class MyFrame extends Frame
{
  private MessageBox mb_ = new MessageBox();
  //private helper used by this class
  private void showMessage(String message)
  {
    //set the message text
    mb_.setMessage( message );
    mb_.pack();
    mb_.show();
  }
}
```

在上面的例子中，当创建MyFrame的一个实例时，MessageBox实例mb_也会被创建。递归应用相同的规则。因此，在类MessageBox的构造函数中初始化或分配的任何实例变量也会从堆中分配，等等。如果MyFrame的实例没有用于在会话中显示错误消息，那么我们就是在不必要地浪费内存。

在这个相当简单的例子中，我们不会得到太多。但是，如果您考虑一个更复杂的类，它使用许多其他类，而其他类又递归地使用和实例化更多的对象，那么潜在的内存使用就更明显了。

### 将延迟实例化视为减少资源需求的策略

下面列出了上述示例的惰性方法，其中在第一次调用showMessage()时实例化了对象mb_。(也就是说，直到程序真正需要它的时候。)

```
public final class MyFrame extends Frame
{
  private MessageBox mb_ ; //null, implicit
  //private helper used by this class
  private void showMessage(String message)
  {
    if(mb_==null)//first call to this method
      mb_=new MessageBox();
    //set the message text
    mb_.setMessage( message );
    mb_.pack();
    mb_.show();
  }
}
```

如果仔细查看showMessage()，您将看到我们首先确定实例变量mb_是否等于null。由于我们还没有在声明时初始化mb_，所以Java运行时已经为我们处理了这个问题。因此，我们可以安全地继续创建MessageBox实例。将来对showMessage()的所有调用都将发现mb_不等于null，因此跳过对象的创建并使用现有实例。

## Examples

假设客户机要求我们编写一个系统，该系统将允许用户对文件系统上的图像进行编目，并提供查看缩略图或完整图像的功能。我们的第一个尝试可能是编写一个在构造函数中加载映像的类。

```
public class ImageFile
{
  private String filename_;
  private Image image_;
  public ImageFile(String filename)
  {
    filename_=filename;
    //load the image
  }
  public String getName(){ return filename_;}
  public Image getImage()
  {
    return image_;
  }
}
```

在上面的示例中，ImageFile实现了一种过度热切的方法来实例化Image对象。对它有利的是，这种设计保证了在调用getImage()时可以立即获得图像。然而，这不仅会非常缓慢(对于包含许多映像的目录)，而且这种设计可能会耗尽可用内存。为了避免这些潜在的问题，我们可以用即时访问的性能优势来换取更少的内存使用。正如您可能已经猜到的，我们可以通过使用惰性实例化来实现这一点。

下面是更新后的ImageFile类，使用的方法与MyFrame类处理其MessageBox实例变量的方法相同:
```
public class ImageFile
{
  private String filename_;
  private Image image_; //=null, implicit
  public ImageFile(String filename)
  {
    //only store the filename
    filename_=filename;
  }
  public String getName(){ return filename_;}
  public Image getImage()
  {
    if(image_==null)
    {
      //first call to getImage()
      //load the image...
    }
    return image_;
  }
}
```

在这个版本中，实际的映像只在第一次调用getImage()时加载。总而言之，这里的权衡是为了减少总体内存使用和启动时间，我们要为在第一次请求时加载映像付出代价——在程序执行的那个点引入性能冲击。这是在需要限制内存使用的上下文中反映代理模式的另一种习惯用法。

上面所示的延迟实例化策略对于我们的示例来说很好，但是稍后您将看到设计如何在多线程上下文中进行更改。

### Java中单例模式的延迟实例化

```
public class Singleton
{
  private Singleton() {}
  static private Singleton instance_ = new Singleton();
  static public Singleton instance()
  {
    return instance_;
  }
  //public methods
}
```
在泛型版本中，我们声明并初始化instance_字段如下:
```
static final Singleton instance_ = new Singleton();
```

使用延迟实例化:

```
public static Singleton instance()
{
  if(instance_==null) //Lazy instantiation
    instance_= new Singleton();
  return instance_;
}
```

上面的清单是GoF给出的c++单例的一个直接端口，通常也被吹捧为通用Java版本。如果您已经熟悉这个表单，并且对我们没有像这样列出泛型单例感到惊讶，那么当您了解到在Java中完全没有必要这样做时，您会更加惊讶!这是一个常见的例子，说明如果您将代码从一种语言移植到另一种语言，而不考虑各自的运行时环境，会发生什么情况。

需要说明的是，GoF c++版本的Singleton使用了延迟实例化，因为不能保证在运行时静态初始化对象的顺序。(参见Scott Meyer的Singleton了解c++中的另一种方法)。在Java中，我们不必担心这些问题。

在Java中，由于Java运行时处理类加载和静态实例变量初始化的方式，没有必要使用惰性的方法实例化单例。在前面，我们描述了如何以及何时加载类。只有公共静态方法的类在第一次调用这些方法时由Java运行时加载;单例的情况是什么呢

```
Singleton s=Singleton.instance();
```

程序中对Singleton.instance()的第一个调用强制Java运行时加载单例类。由于字段instance_被声明为静态的，Java运行时将在成功加载该类之后初始化它。因此，确保对Singleton.instance()的调用将返回一个完全初始化的Singleton。

### 延迟实例化：多线程应用程序中存在危险

对于具体的单例，使用延迟实例化不仅在Java中是不必要的，在多线程应用程序的上下文中也是非常危险的。考虑Singleton.instance()方法的延迟版本，其中两个或多个单独的线程试图通过instance()获得对对象的引用。如果一个线程在成功执行If (instance_==null)行之后被抢占，但是在它完成instance_=new Singleton()行之前，另一个线程也可以使用instance_ still ==null()来输入这个方法，这很糟糕!

这个场景的结果是创建一个或多个单例对象的可能性。当单例类连接到数据库或远程服务器时，这是一个令人头痛的问题。解决这个问题的简单方法是使用synchronized关键字来保护方法不被多个线程同时进入:

```
synchronized static public instance() {...}
```

但是，对于广泛使用单例类的大多数多线程应用程序来说，这种方法有些笨拙，因此会阻塞对instance()的并发调用。顺便说一下，调用同步方法总是比调用非同步方法慢得多。所以我们需要的是一种同步策略，它不会导致不必要的阻塞。幸运的是，这样的策略是存在的。它被称为双重检查习语。

### 双重检查语法

使用双重检查习惯用法来保护使用延迟实例化的方法。下面是如何用Java实现它:

```
public static Singleton instance()
{
  if(instance_==null) //don't want to block here
  {
    //two or more threads might be here!!!
    synchronized(Singleton.class)
    {
      //must check again as one of the
      //blocked threads can still enter
      if(instance_==null)
        instance_= new Singleton();//safe
    }
  }
  return instance_;
}
```

只有在构造单例之前多个线程调用instance()时，双重检查用法才会使用同步来提高性能。一旦对象被实例化，instance_就不再是==null，从而允许该方法避免阻塞并发调用者。

在Java中使用多个线程可能非常复杂。事实上，并发性的主题非常广泛，以至于Doug Lea写了一本关于它的书:Concurrent Programming in Java (Java并发编程)。


# Object Pool in Java

## What is Object Pool?

对象池模式是一种软件创建设计模式，用于初始化类实例的成本非常高的情况。基本上，对象池是包含一定数量对象的容器。因此，当从池中取出一个对象时，它将在池中不可用，直到它被放回。

对象池(也称为资源池)用于管理对象缓存。访问对象池的客户机可以通过简单地请求池提供一个已经实例化的对象来避免创建新对象。通常，池将是一个不断增长的池，也就是说，如果池为空，池本身将创建新对象，或者我们可以有一个池，它限制了创建的对象的数量。

最好将当前未使用的所有可重用对象保存在同一个对象池中，以便由一个一致的策略管理它们。为此，可重用池类被设计为单例类。

对象池允许其他人从其池中“check out”对象，当进程不再需要这些对象时，将它们返回到池中以便重用。

但是，我们不希望进程必须等待某个特定的对象被释放，因此对象池也会根据需要实例化新对象，但是还必须实现定期清理未使用对象的功能。

## Usage

连接池模式的一般思想是，如果类的实例可以重用，那么可以通过重用它们来避免创建类的实例。

通常，最好将当前未使用的所有可重用对象保存在同一个对象池中，以便由一个一致的策略管理它们。为了实现这一点，ReusablePool类被设计为一个单例类。它的构造函数是私有的，这迫使其他类调用它的getInstance方法来获取ReusablePool类的一个实例。

客户端对象在需要可重用对象时调用ReusablePool对象的acquirereavailable方法。ReusablePool对象维护可重用对象的集合。它使用可重用对象的集合来包含当前未使用的可重用对象池。

当调用acquirereavailable方法时，如果池中有任何可重用对象，则从池中删除可重用对象并返回它。如果池为空，则acquirereavailable方法将在可能的情况下创建可重用对象。如果acquirereavailable方法不能创建新的可重用对象，那么它将等待，直到将可重用对象返回到集合。

客户端对象在使用完可重用对象后，将可重用对象传递给ReusablePool对象的releasereavailable方法。releasereavailable方法将可重用对象返回给未使用的可重用对象池。

在对象池模式的许多应用程序中，有理由限制可能存在的可重用对象的总数。在这种情况下，创建可重用对象的ReusablePool对象负责创建的可重用对象数量不超过指定的最大数量。如果ReusablePool对象负责限制它们将创建的对象的数量，那么ReusablePool类将有一个方法来指定要创建的对象的最大数量。

## Example

对象池模式类似于办公室仓库。当一个新员工被雇佣时，办公室经理必须为他准备一个工作空间。她想知道办公室仓库里是否有备用设备。如果是，她就用它。如果没有，她就从亚马逊订购新设备。如果一名员工被解雇，他的设备就会被转移到仓库，在需要新的工作地点的时候就可以拿到仓库。

### Check List
+ 创建内部,带有私有对象数组的ObjectPool类
+ 在ObjectPool类中创建获取和释放方法
+ 确保ObjectPool是Singleton

### Rules of thumb
+ 工厂方法模式可用于封装对象的创建逻辑。但是，对象池模式在创建对象之后并不管理它们，而是跟踪它创建的对象。
+ 对象池通常实现为单例。

### Use in Java

ObjectPool Class
```
public abstract class ObjectPool<T> {
  private long expirationTime;

  private Hashtable<T, Long> locked, unlocked;

  public ObjectPool() {
    expirationTime = 30000; // 30 seconds
    locked = new Hashtable<T, Long>();
    unlocked = new Hashtable<T, Long>();
  }

  protected abstract T create();

  public abstract boolean validate(T o);

  public abstract void expire(T o);

  public synchronized T checkOut() {
    long now = System.currentTimeMillis();
    T t;
    if (unlocked.size() > 0) {
      Enumeration<T> e = unlocked.keys();
      while (e.hasMoreElements()) {
        t = e.nextElement();
        if ((now - unlocked.get(t)) > expirationTime) {
          // object has expired
          unlocked.remove(t);
          expire(t);
          t = null;
        } else {
          if (validate(t)) {
            unlocked.remove(t);
            locked.put(t, now);
            return (t);
          } else {
            // object failed validation
            unlocked.remove(t);
            expire(t);
            t = null;
          }
        }
      }
    }
    // no objects available, create a new one
    t = create();
    locked.put(t, now);
    return (t);
  }

  public synchronized void checkIn(T t) {
    locked.remove(t);
    unlocked.put(t, System.currentTimeMillis());
  }
}

//The three remaining methods are abstract 
//and therefore must be implemented by the subclass

public class JDBCConnectionPool extends ObjectPool<Connection> {

  private String dsn, usr, pwd;

  public JDBCConnectionPool(String driver, String dsn, String usr, String pwd) {
    super();
    try {
      Class.forName(driver).newInstance();
    } catch (Exception e) {
      e.printStackTrace();
    }
    this.dsn = dsn;
    this.usr = usr;
    this.pwd = pwd;
  }

  @Override
  protected Connection create() {
    try {
      return (DriverManager.getConnection(dsn, usr, pwd));
    } catch (SQLException e) {
      e.printStackTrace();
      return (null);
    }
  }

  @Override
  public void expire(Connection o) {
    try {
      ((Connection) o).close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  @Override
  public boolean validate(Connection o) {
    try {
      return (!((Connection) o).isClosed());
    } catch (SQLException e) {
      e.printStackTrace();
      return (false);
    }
  }
}
```

JDBCConnectionPool将允许应用程序借用和返回数据库连接:
```
public class Main {
  public static void main(String args[]) {
    // Do something...
    ...

    // Create the ConnectionPool:
    JDBCConnectionPool pool = new JDBCConnectionPool(
      "org.hsqldb.jdbcDriver", "jdbc:hsqldb://localhost/mydb",
      "sa", "secret");

    // Get a connection:
    Connection con = pool.checkOut();

    // Use the connection
    ...

    // Return the connection:
    pool.checkIn(con);
 
  }
}
```

# Prototype Pattern in Java

## What is Prototype Pattern?

原型模式是软件开发中的一种创造性设计模式。当要创建的对象类型由一个原型实例决定时，将使用它，该原型实例被克隆以生成新的对象。此模式用于:
+ 避免在客户端应用程序中使用对象创建者的子类，就像工厂方法模式。
+ 避免以标准方式(例如，使用“new”关键字)创建新对象的固有成本，因为它对于给定的应用程序来说非常昂贵。

要实现此模式，请声明一个抽象基类，该类指定一个pure virtual clone()方法。任何需要“多态构造函数”功能的类都从抽象基类派生自己，并实现clone()操作。

客户端没有编写代码来调用硬编码类名上的“new”操作符，而是在原型上调用clone()方法，使用指定所需的特定具体派生类的参数调用工厂方法，或者通过另一种设计模式提供的某种机制调用clone()方法。

一个细胞的有丝分裂——导致两个相同的细胞——是一个原型的一个例子，它在复制自身中起着积极的作用，因此，展示了原型模式。当一个细胞分裂时，会产生两个基因型相同的细胞。换句话说，细胞克隆自己。

## Example 

Prototype模式提供了一种机制，可以将原始对象复制到新对象，然后根据我们的需要对其进行修改。原型设计模式使用java克隆来复制对象。

通过一个实例，可以很容易地理解原型设计模式。假设我们有一个从数据库加载数据的对象。现在我们需要在程序中多次修改该数据，因此使用new关键字创建对象并再次从数据库加载所有数据不是一个好主意。

更好的方法是将现有对象克隆到一个新对象中，然后进行数据操作。

原型设计模式要求您复制的对象应该提供复制特性。它不应该由任何其他类来完成。然而，是否使用对象属性的浅拷贝或深拷贝取决于需求及其设计决策。

下面是一个示例程序，展示了java中的原型设计模式示例。

```
package com.journaldev.design.prototype;

import java.util.ArrayList;
import java.util.List;

public class Employees implements Cloneable{

	private List<String> empList;
	
	public Employees(){
		empList = new ArrayList<String>();
	}
	
	public Employees(List<String> list){
		this.empList=list;
	}
	public void loadData(){
		//read all employees from database and put into the list
		empList.add("Pankaj");
		empList.add("Raj");
		empList.add("David");
		empList.add("Lisa");
	}
	
	public List<String> getEmpList() {
		return empList;
	}

	@Override
	public Object clone() throws CloneNotSupportedException{
			List<String> temp = new ArrayList<String>();
			for(String s : this.getEmpList()){
				temp.add(s);
			}
			return new Employees(temp);
	}
	
}
```

请注意，重写clone方法以提供员工列表的副本。

下面的原型设计模式示例测试程序将展示原型模式的好处。

```
import com.journaldev.design.prototype.Employees;

public class PrototypePatternTest {

	public static void main(String[] args) throws CloneNotSupportedException {
		Employees emps = new Employees();
		emps.loadData();
		
		//Use the clone method to get the Employee object
		Employees empsNew = (Employees) emps.clone();
		Employees empsNew1 = (Employees) emps.clone();
		List<String> list = empsNew.getEmpList();
		list.add("John");
		List<String> list1 = empsNew1.getEmpList();
		list1.remove("Pankaj");
		
		System.out.println("emps List: "+emps.getEmpList());
		System.out.println("empsNew List: "+list);
		System.out.println("empsNew1 List: "+list1);
	}

}
```

如果没有提供对象克隆，那么每次都必须调用数据库来获取employee列表。然后做一些需要耗费资源和时间的操作。




# 主要参考资源

## [design_patterns](https://sourcemaking.com/design_patterns/)

## [geeksforgeeks](https://www.geeksforgeeks.org/object-pool-design-pattern/)

## [wiki-Software design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)

## [journaldev](https://www.journaldev.com/1827/java-design-patterns-example-tutorial)

## [tutorialspoint](https://www.tutorialspoint.com/design_pattern/index.htm)
