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

创建设计模式的一些示例包括：

+ Factory Mothed pattern(工厂方法模式) - 允许一个类的实例化推迟到子类中进行。
+ Abstract Factory pattern(抽象工厂模式) - 提供一个创建相关或依赖对象的接口，而不指定对象的具体类。
+ Singleton pattern(单例模式) - 保证一个类只有一个实例，并且提供对这个实例的全局访问方式。
+ Builder pattern(生成器模式) - 将一个复杂对象的创建与它的表示分离，使同样的创建过程可以创建不同的表示。
+ Lazy Initialization pattern(延迟初始化模式) - 将对象的创建，某个值的计算，或者其他代价较高的过程推迟到它第一次需要时进行。
+ Object Pool pattern(对象池模式) - 通过回收不再使用的对象，避免创建和销毁对象时代价高昂的获取和释放资源的过程。
+ Prototype pattern(原型模式) - 使用原型实例指定要创建的对象类型，通过复制原型创建新的对象。


# Factory Design Pattern in Java

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



