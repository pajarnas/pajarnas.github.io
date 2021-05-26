---

title: .Net Framework II C# OOP
date: 05/19/2021
updated: 
tags: 
  - notes
  - C#
  - .Net
categories: .Net Framework
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

# Var keyword 

Anonymous type properties are read only and they cannot be set. It just stored the information.

# Method Extension

An Extension Method is:

1. It is a **static method.**
2. It must be located in a **static class**.
3. It uses the "**this**" keyword as the **first parameter with a type in** .Net and this method will called by a given type instance on the client side.
4. The first parameter should be the **same type** as the class type your are expending to. 
5. It also shown by VS intellisense. When we press the dot (.) after a type instance then it comes in VS intellisense.
6. An Extension Method should be in the same namespace as it is used or you need to import the namespace of the class by a using statement.
7. You can give any name of for the class that has an Extension Method but the class should be static.
8. If you want to add new methods to a type and you don't have the source code for it then the solution is to use and implement Extension Methods of that type.
9. If you create Extension Methods that have the same signature methods as the type you are extending then the Extension Methods will never be called. 

# Difference between Abstract Class and Interface in C# Program

As we all know that C# is an object oriented programming provides full support for object-oriented concepts that are Encapsulation, Abstraction, Inheritance, and Polymorphism. In contrast to Abstraction both Abstract class and Interface are coming out in picture as both of these provides abstraction in C# program.

In **an abstract class**, we can create the functionality and that needs to be implemented by the derived class. The interface allows us to define the functionality or functions but cannot implement that. The derived class extend the interface and implement those functions.

Following are the important differences between Abstract Class and Interface.

| Sr. No. |      Key       |                        Abstract Class                        |                          Interface                           |
| ------- | :------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 1       |   Definition   | In terms of standard definition an Abstract class is, conceptually, a class that cannot be instantiated and is usually implemented as a class that has one or more pure virtual (abstract) functions. | On other hand an Interface is a description of what member functions must a class, which inherits this interface, implement. In other words, an interface describes behaviour of the class. |
| 2       | Implementation | As like of other general class design in C# Abstract class also have its own implementation along with its declaration. | On other hand an Interface can only have a signature, not the implementation. While its implementation is being provided by the class which implements it. |
| 3       |  Inheritance   | As per specification in C# a class can extends only one other class hence multiple inheritance is not achieved by abstract class. | On other hand in case of Interface a class can implements multiple interfaces and hence multiple inheritance is achieved by interface. |
| 4       |  Constructor   | Like other classes in C# for instantiation abstract class also have constructor which provide an instance of abstract class to access its non-static methods. | On other hand Interface do not have constructor so we can't instantiate an interface directly although its method could get accessed by creating instance of class which implementing it. |
| 5       |   Modifiers    | As abstract class is most like of other ordinary class in C# so it can contain different types of access modifiers like public, private, protected etc. | On other hand as Interface needs to be get implemented in order to provide its methods implementation by other class so can only contains public access modifier. |
| 6       |  Performance   | As abstract class have its method as well as their implementations also for its abstract methods implementation it have reference for its implementing class so performance is comparatively faster as compare to that of Interface. | On other hand the performance of interface is slow because it requires time to search actual method in the corresponding class. |

# Anonymous

In the previous code, the names of the anonymous type members (CustomerName, City, Stores, and CustomerID) are explicitly specified. It is also possible to omit the names, in which case, the names of the generated members are the same as the members used to initialize them. This is called a *projection initializer*

