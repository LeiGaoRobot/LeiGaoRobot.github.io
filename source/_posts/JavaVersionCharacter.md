---
title: Java8 版本特性
date: 2018-12-17 10:20:40
categories: java
tags: 
- java8
- lambda
- functional interface
---
# Java8特性
## 函数式接口

>函数式接口（functional interface）就是只定义一个抽象方法的接口，比如 Java API 中的 Predicate、Comparator 和 Runnable 等。Lambda 表达式允许你直接以内联的形式为函数式接口的抽象方法提供实现，并把整个表达式作为函数式接口的实例（具体说来，是函数式接口一个具体实现的实例）。

Java 8 引入的一个核心概念是函数式接口（Functional Interfaces）。通过在接口里面添加一个抽象方法，这些方法可以直接从接口中运行。如果一个接口定义个唯一一个抽象方法，那么这个接口就成为函数式接口。同时，引入了一个新的注解：@FunctionalInterface。可以把他它放在一个接口前，表示这个接口是一个函数式接口。这个注解是非必须的，只要接口只包含一个方法的接口，虚拟机会自动判断，不过最好在接口上使用注解 @FunctionalInterface 进行声明。在接口中添加了 @FunctionalInterface 的接口，只允许有一个抽象方法，否则编译器也会报错。

java.lang.Runnable 就是一个函数式接口。
``` java
@FunctionalInterface
public interface Runnable {
   public abstract void run();
}
```

---
## Lambda表达式
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

**Syntax**

Lambda 表达式由参数列表、箭头和 Lambda 主体组成。

`parameter -> expression body`

**example**

>函数式编程（functional programming）或称函数程序设计，又称泛函编程，是一种编程典范，它将计算机运算视为数学上的函数计算，并且避免使用程序状态以及易变对象。函数编程语言最重要的基础是λ演算（lambda calculus）。而且λ演算的函数可以接受函数当作输入（引数）和输出（传出值）。[Wiki](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B8%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80)


lambda演算可比拟是最根本的编程语言，它包括了一条变换规则（变量替换）和一条将函数抽象化定义的方式。因此普遍公认是一种更接近软件而非硬件的方式。对函数式编程语言造成很大影响，比如Lisp、ML语言和Haskell语言。在1936年邱奇利用λ演算给出了对于判定性问题（Entscheidungsproblem）的否定：关于两个lambda表达式是否等价的命题，无法由一个“通用的算法”判断，这是不可判定性能够证明的头一个问题，甚至还在停机问题之先。

``` java
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

**注意事项**

使用lambda表达式，您可以引用任何最终变量或有效的最终变量（仅分配一次）。如果第二次为变量赋值，则Lambda表达式会抛出编译错误。

---
## 方法引用

方法引用有助于通过名称指向方法，可以使语言的构造更紧凑简洁，减少冗余代码。使用“::”符号描述方法引用。方法引用可用于指出以下类型的方法
+ 静态方法
+ 实例方法
+ 使用new运算符的构造函数（TreeSet :: new）

**Syntax**

+ 构造器引用：它的语法是Class::new，或者更一般的Class< T >::new实例如下：
```java
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
```java
cars.forEach( Car::collide );
```
+ 特定类的任意对象的方法引用：它的语法是Class::method实例如下：
```java
cars.forEach( Car::repair );
```
+ MathOperation
```java
final Car police = Car.create( Car::new );
cars.forEach( police::follow );
```
---
## 接口的增强

Java 8 对接口做了进一步的增强。在接口中可以添加使用 default 关键字修饰的非抽象方法。还可以在接口中定义静态方法。如今，接口看上去与抽象类的功能越来越类似了。

### **默认方法**

Java 8在接口中引入了默认方法实现的新概念。添加此功能是为了向后兼容，以便可以使用旧接口来利用Java 8的lambda表达式功能。给接口添加一个非抽象的方法实现，只需要使用 default 关键字即可，这个特征又叫做扩展方法。在实现该接口时，该默认扩展方法在子类上可以直接使用，它的使用方式类似于抽象类中非抽象成员方法。但扩展方法不能够重载 Object 中的方法。例如：toString、equals、 hashCode 不能在接口中被重载。

**Syntax**

Default：

``` java
public interface vehicle {

   default void print() {
      System.out.println("I am a vehicle!");
   }
}
```

Mutiple Defaults：

一个接口有默认方法，考虑这样的情况，一个类实现了多个接口，且这些接口有相同的默认方法，以下实例说明了这种情况的解决方法：

``` java
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
```java
public class interface Car implements Vehicle, fourWheeler{

   default void print(){
      System.out.println("I am a four wheeler car vehicle!");
   }
}
```

第二种解决方案，使用super调用指定接口的默认方法
```java
public class Car implements Vehicle, FourWheeler {

   public void print(){
      Vehicle.super.print();
   }
}
```

Static Default Methods：

在接口中，还允许定义静态的方法，可以声明（并且可以提供实现）的静态方法。接口中的静态方法可以直接用接口来调用。
```java
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

