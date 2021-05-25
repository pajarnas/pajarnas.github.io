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

