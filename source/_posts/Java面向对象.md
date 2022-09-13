---
title: Java面向对象
categories:
  - Java

  - null
tags:
  - Java
  - null
copyright: true
date: 2022-03-07 10:57:21
permalink:
description:
image:
---



**前言**

**Java 面向对象编程 笔记**

<https://www.liaoxuefeng.com/wiki/1252599548343744/1260451488854880>
<https://www.cnblogs.com/hellojava/archive/2013/02/27/2935450.html>
<https://www.runoob.com/java/java-tutorial.html>

<!-- more -->

# 类的声明

{% codeblock   %}
[public | protected | private ][abstract|final] class className [extends superclassName] [implements interfaceNameList]{……}
{% endcodeblock %}

其中，修饰符public,abstract,final 说明了类的属性，
className为类名，
superclassName为类的父类的名字，用于继承
interfaceNameList为类所实现的接口列表。

## abstract 抽象类

如果一个class定义了方法，但没有具体执行代码，这个方法就是抽象方法
抽象类除了**不能实例化对象**之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。
可以用于继承，即定义新的类父类是一个抽象类

# 成员变量和成员方法

{% codeblock  %}
class className{
    [public | protected | private ] [static] [final] [transient] [volatile] type variableName;//成员变量
    [public | protected | private ] [static] [final | abstract] [native] [synchronized] returnType methodName([paramList]) [throws exceptionList]{
        statements
    }//成员方法
}
{% endcodeblock %}

**成员变量限定词的含义：**

static: 静态变量（类变量）
final: 常量；
transient: 暂时性变量，用于对象存档，用于对象的串行化
volatile: 贡献变量，用于并发线程的共享

方法的实现也包括两部分内容：方法声明和方法体。

方法声明

**方法声明中的限定词的含义：**

static: 类方法，可通过类名直接调用
abstract: 抽象方法，没有方法体
final: 方法不能被重写、继承
native: 集成其它语言的代码
synchronized: 控制多个并发线程的访问

## abstract 抽象方法

如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法

## 构造方法

**this代表本类的对象**

没有在构造方法中初始化字段时，引用类型的字段默认是null，数值类型的字段用默认值，int类型默认值是0，布尔类型默认值是false

可以定义多个构造方法

{% codeblock  %}
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Xiao Ming", 15); // 既可以调用带参数的构造方法
        Person p2 = new Person(); // 也可以调用无参数构造方法
    }
}

class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name) {
        this.name = name;
        this.age = 12;
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
{% endcodeblock %}

# 面向对象的基本特征

## 封装

在面向对象程式设计方法中，封装（英语：Encapsulation）是指一种将抽象性函式接口的实现细节部分包装、隐藏起来的方法。
封装可以被认为是一个保护屏障，防止该类的代码和数据被外部类定义的代码随机访问。
要访问该类的代码和数据，必须通过严格的接口控制。
封装最主要的功能在于我们能修改自己的实现代码，而不用修改那些调用我们代码的程序片段。
适当的封装可以让程式码更容易理解与维护，也加强了程式码的安全性。

<https://www.runoob.com/java/java-encapsulation.html>

private：类中限定为private的成员，只能被这个类本身访问。如果一个类的构造方法声明为private,则其它类不能生成该类的一个实例。
default：类中不加任何访问权限限定的成员属于缺省的（default）访问状态，可以被这个类本身和同一个包中的类所访问。
protected：类中限定为protected的成员，可以被这个类本身、它的子类（包括同一个包中以及不同包中的子类）和同一个包中的所有其他的类访问。
public：类中限定为public的成员，可以被所有的类访问。
<a href="https://sm.ms/image/TKfdORlCGaQgJVD" target="_blank"><img src="https://s2.loli.net/2022/03/08/TKfdORlCGaQgJVD.jpg" ></a>

## 继承

解决代码重复和便于维护

### 继承格式

{% codeblock  %}

class 父类 {
}

class 子类 extends 父类 {

}
{% endcodeblock %}

### 特性

子类拥有父类 **非 private** 的属性、方法。

子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。

子类可以用自己的方式实现父类的方法。

**Java支持多重继承，不支持多继承**
<a href="https://sm.ms/image/lNnouWEYDSv2U13" target="_blank"><img src="https://s2.loli.net/2022/03/08/lNnouWEYDSv2U13.jpg" ></a>

### super关键字

我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类

{% codeblock   %}
class Animal {
  void eat() {
    System.out.println("animal : eat");
  }
}

class Dog extends Animal {
  void eat() {
    System.out.println("dog : eat");
  }
  void eatTest() {
    this.eat();   // this 调用自己的方法
    super.eat();  // super 调用父类方法
  }
}
{% endcodeblock %}

子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表

{% codeblock   %}
class SuperClass {
  private int n;
  SuperClass(){
    System.out.println("SuperClass()");
  }
  SuperClass(int n) {
    System.out.println("SuperClass(int n)");
    this.n = n;
  }
}
// SubClass 类继承
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){ // 自动调用父类的无参数构造器
    System.out.println("SubClass");
  }  
  
  public SubClass(int n){
    super(300);  // 调用父类中带有参数的构造器
    System.out.println("SubClass(int n):"+n);
    this.n = n;
  }
}

public class TestSuperSub{
  public static void main (String args[]){
    System.out.println("------SubClass 类继承------");
    SubClass sc1 = new SubClass();
    SubClass sc2 = new SubClass(100);
  }
}
{% endcodeblock %}

输出结果为
------SubClass 类继承------
SuperClass()
SubClass
SuperClass(int n)
SubClass(int n):100

## 多态

### 重载

<a href="https://sm.ms/image/z3q1aP4sbDHMUx8" target="_blank"><img src="https://s2.loli.net/2022/03/08/z3q1aP4sbDHMUx8.jpg" ></a>
方法名相同、参数不同（数量不同、类型不同、顺序不同）、同一作用域。
返回值类型可以相同也可以不相同，无法以返回型别作为重载函数的区分标准。

### 重写

重写是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。**即外壳不变，核心重写！**

**当需要在子类中调用父类的被重写方法时，要使用 super 关键字。**

**重写规则**

1. 参数列表与被重写方法的参数列表必须完全相同。

2. 返回类型与被重写方法的返回类型可以不相同，但是必须是父类返回值的派生类（java5 及更早版本返回类型要一样，java7 及更高版本可以不同）。

3. 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为 public，那么在子类中重写该方法就不能声明为 protected。

4. 父类的成员方法只能被它的子类重写。

5. 声明为 final 的方法不能被重写。

6. 声明为 static 的方法不能被重写，但是能够被再次声明。

7. 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为 private 和 final 的方法。

8. 子类和父类不在同一个包中，那么子类只能够重写父类的声明为 public 和 protected 的非 final 方法。

9. 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。

10. 构造方法不能被重写。

11. 如果不能继承一个类，则不能重写该类的方法。

### 重载重写区别

1. 方法重载是一个类中定义了多个方法名相同,而他们的参数的数量不同或数量相同而类型和次序不同,则称为方法的重载(Overloading)。

2. 方法重写是在子类存在方法与父类的方法的名字相同,而且参数的个数与类型一样,返回值也一样的方法,就称为重写(Overriding)。

3. 方法重载是一个类的多态性表现,而方法重写是子类与父类的一种多态性表现。

<a href="https://sm.ms/image/vecY2Ql85H7sOEk" target="_blank"><img src="https://s2.loli.net/2022/03/08/vecY2Ql85H7sOEk.jpg" ></a>

### 虚函数

虚函数的存在是为了多态。
Java 中其实没有虚函数的概念，它的普通函数就相当于 C++ 的虚函数，动态绑定是Java的默认行为。如果 Java 中不希望某个函数具有虚函数特性，可以加上 final 关键字变成非虚函数。

# 接口

<https://www.liaoxuefeng.com/wiki/1252599548343744/1260456790454816>

如果一个抽象类没有字段，所有方法全部都是抽象方法，就可以把该抽象类改写为接口：**interface**

所谓interface，就是比抽象类还要抽象的纯抽象接口，因为它连字段都不能有。因为接口定义的所有方法默认都是**public abstract**的，所以这两个修饰符不需要写出来（写不写效果都一样）

## 接口声明和实现

Interface关键字用来声明一个接口。

类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。
当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。

类在重写方法时要保持一致的方法名，并且应该保持相同或者相兼容的返回值类型。

{% codeblock  %}
interface Person {
    void run();
    String getName();
}

class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        System.out.println(this.name + " run");
    }

    @Override
    public String getName() {
        return this.name;
    }
}
{% endcodeblock %}

## 接口特性

1. 接口文件保存在 .java 结尾的文件中，文件名使用接口名

2. 当一个具体的class去实现一个interface时，需要使用**implements**关键字

3. **一个类可以实现多个interface**

4. 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

5. 接口中每一个方法也是隐式抽象

6. 接口中可以含有变量，但是接口中的变量会被隐式的指定为 public static final 变量（并且只能是 public，用 private 修饰会报编译错误）

7. 一个接口能继承另一个接口，这和类之间的继承比较相似。接口的继承使用extends关键字 **并且接口允许多继承**
eg: public interface int extends int1, int2

# 内部类

## Inner Class

如果一个类定义在另一个类的内部，这个类就是Inner Class
Inner Class 不能单独存在，必须依附于一个实例

{% codeblock  %}
public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer("Nested"); // 实例化一个Outer
        Outer.Inner inner = outer.new Inner(); // 实例化一个Inner
        inner.hello();
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    class Inner {
        void hello() {
            System.out.println("Hello, " + Outer.this.name);
        }
    }
}

{% endcodeblock %}

## Anonymous Class

在方法内部，通过匿名类（Anonymous Class）来定义Inner Class

Runnable本身是接口，接口是不能实例化的，所以这里实际上是定义了一个实现了Runnable接口的匿名类，并且通过new实例化该匿名类，然后转型为Runnable

不关心类名，简化代码

{% codeblock  %}
public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer("Nested");
        outer.asyncHello();
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    void asyncHello() {
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("Hello, " + Outer.this.name);
            }
        };
        new Thread(r).start();
    }
}
{% endcodeblock %}

## Static Nested Class

使用static修饰，静态内部类

用static修饰的内部类不再依附于Outer的实例，而是一个完全独立的类，因此无法引用Outer.this，但它可以访问Outer的private静态字段和静态方法。
**用途，可以访问private的方法和变量**

{% codeblock  %}
public class Main {
    public static void main(String[] args) {
        Outer.StaticNested sn = new Outer.StaticNested();
        sn.hello();
    }
}

class Outer {
    private static String NAME = "OUTER";

    private String name;

    Outer(String name) {
        this.name = name;
    }

    static class StaticNested {
        void hello() {
            System.out.println("Hello, " + Outer.NAME);
        }
    }
}
{% endcodeblock %}

# 包+

<https://www.liaoxuefeng.com/wiki/1252599548343744/1260467032946976>

将功能相似或相关的类或者接口组织在同一个包中，方便查找和使用。
防止命名冲突

## 实现

{% codeblock  %}
packsge package_name // 申明包名

public cless Cless_name{

}
{% endcodeblock %}

## 导入

{% codeblock  %}
// 导入包
package ming;

// 导入完整类名:
import mr.jun.Arrays;

// 导入mr.jun包的所有class
import mr.jun.*;

public class Person {
    public void run() {
        Arrays arrays = new Arrays();
    }
}
{% endcodeblock %}

<hr />
版权信息
