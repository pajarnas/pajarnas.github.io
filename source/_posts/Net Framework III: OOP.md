---

title: .Net Framework II C# Ba
date: 05/19/2021
updated: 
tags: 
  - notes
  - HTML
  - front-End
categories: Front-End
keywords: 
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Shiqi Zhang
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

C# 2.0 introduced **Anonymous** methods, which allow code blocks to be written “inline” where **delegate** values are expected. For example, in the following statement, the **FindAll** method requires a delegate parameter:

```c#
var innerPoints = points.FindAll(delegate(Point p) { return (p.X > 0 && p.Y > 0); });
```

In this case, the delegate determines if both the x and y coordinates are positive

C# 3.0 introduces ***lambda expressions***, which provide a **more concise**, functional programming syntax for writing **anonymous methods**. In this case, you replace a method invocation which currently takes an anonymous method with a lambda expression. 

To show this, the example above can be written as:

```c#
var innerPoints = points.FindAll(p => p.X > 0 && p.Y > 0);
```



A lambda expression is written as a parameter list, followed by the => token, and then an expression or statement. For example: 

```c#
(int x) => { return x + 1; }  // parameter list, statement
```

The parameters of a lambda expression can be explicitly or implicitly typed. 

```c#
(int x) => x + 1;        // explicit parameter list, expression
```

In an implicitly typed parameter list, the types of the parameters are inferred from the context in which the lambda expression is used. In addition, if a lambda expression has a single, implicitly typed parameter, the parentheses may be omitted from the parameter list:

```c#
x => x + 1;           // implicit parameter list, expression
```

```c#
(x,y) => x * y;         // implicit parameter list, expression
```

# Delegate

Delegate is a pointer of function. 

首先，写一行int a；我们能知道什么？我们能知道int是个数据类型，a是变量，a能存放int类型的数据，其它的我们这里不用关注，非常的直截了当，那这跟委托有什么关系么？其实没有关系，我只是类比，实际上委托就是一种数据类型，跟int是一样的，只不过这种数据类型指向的是一个函数的入口，它存放的是一个函数入口地址，通俗点讲就是委托类型的变量只能接受函数的赋值，比如xxx d；此时你只能将一个函数赋值给d，函数类型是什么样的呢？（形参个数及形参类型，有无返回值等）这个就得看委托是如何声明的，所以，站在如何使用委托的角度上看，委托就是种数据类型，可以用委托来定义变量，然后使用该变量。这是站在如何使用委托的角度上而言；

​          其次，在代码结构的设计上使用委托可以降低类与类之间的耦合性。我直接用代码举个例子

```csharp
public class AClass
{
      public void AFunc()
     {
//当某个条件满足时
         if(xxxxx)
         {

         }
     }
}

public class BClass
{
 public void BFunc()
     {
     }
}

public class Client
{
AClass aobj = new AClass();
void Main()
{
aobj.AFunc();
}
}
```

可以看到上边代码中有三个类，AClass、BClas和Client类，Client类时驱动执行的类，我们不用管它，在这里，当A类中的某个条件满足时要需要执行到B类中的方法，最最最最简单的做法就是在A类中去引用B类，类似下边的代码。

```text
public class AClass
{
      BClass bobj = new BClass();
      public void AFunc()
     {
//当某个条件满足时
         if(xxxxx)
         {
            bobj.BFunc();
         }
     }
}

public class BClass
{
 public void BFunc()
     {
     }
}

public class Client
{
AClass aobj = new AClass();
void Main()
{
aobj.AFunc();
}
}
```

这样的写法使得A类和B类之间的关系为强耦合的关系，B的变化会在很大的几率上影响到A，我们将这样的关系称之为不稳定的关系，这是面向对象编程设计所不提倡的，那么如何将不稳定的关系变为稳定的关系呢？方法有多种，委托的应用就是其中一种。同还用代码举例，如下

```text
//声明一个委托类型、
//它能接受的函数类型是没有返回也没有参数
public delegate void MyDelegate();
public class AClass
{
      //定义一个委托类型的变量 
//变量名字为 mydelagate
      public MyDelegate mydelagate = null;
      public void AFunc()
     {
//当某个条件满足时
         if(xxxxx)
         {
             if(mydelagate != null)
             {
               mydelagate();
               }
         }
     }
}

public class BClass
{
 public void BFunc()
     {
     }
}

public class Client
{
AClass aobj = new AClass();
BClass bobj = new BClass();
void Main()
{
a.mydelagate = bobj.BFunc();
aobj.AFunc();
}
}
```

可以看到，客户端只需要将B类中的方法通过公开的委托注册到A对象内部去执行，这样就避免了A类和B类之间的相互引用，提高了A、B关系之间的稳定性。



