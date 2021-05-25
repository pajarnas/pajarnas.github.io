---

title: .Net Framework I: Basic
date: 05/18/2021
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
co- er: 
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

# History

Before .Net was released software de- elopers used **COM(Component Object Model)** allowed indi- iduals to build libraries of code that could be shared across di- erse programming languages.

Howe- er, COM was plagued by complicated infrastructure, a fragile deployment model, and was only possible on the Windows operating system.

Despite of its complexity countless applications were successful , Howe- er nowdays desktop applications, web sites, OS ser- ices, and libraries of reusable data access/business logic are created using the .NET platform.

# Benefits of .NET Platform

.Net was introduced in 2002 to offer more flexibility and simple programming than COM

Some of the core features:

- *Support for numerous programming languages*: .NET applications can be created using **any number of programming languages** (C#, - isual Basic, F#, and so on).

- *A common runtime engine shared by all .NET-aware languages*: One aspect of this engine is a well-defined set of types that each .NET-aware language understands.

- *Language integration*: .NET supports cross-language inheritance, cross-language, exception handling, and cross-language debugging of code. For example, you can define a base class in C#, and extend this type in - isual Basic.

- *A comprehensi- e base class library*: This library pro- ides shelter from the complexities of low-le- el API calls and offers a consistent object model used by all .NET-aware languages.

- *A simplified deployment model*: .NET libraries are not registered into the system registry. Furthermore, the .NET platform allows multiple - ersions of the same *.dll to exist in harmony on a single machine.

# What Is A DLL File and How to Open it

## DLL Files

Firstly, DLL stands for **Dynamic Link Library**. These library files contain code to carry out a specific function for an application in the Windows operating systems. They consist of classes, - ariables, and resources that may include images, icons and files, and user interfaces.

DLL files consist of C or [C++ programming languages](https://computingforgeeks.com/best-c-programming-books-for-beginners/). Mostly, it uses C++. Interestingly, you can e- en write your own DLL code. Howe- er, it’s better to know some [basics](https://reco- erit.wondershare.com/computer-problems/how-to-edit-dll-file.html) before you attempt to tinker with the existing DLLs.

A DLL file will ha- e a .dll extension. When you launch an application, the operating system creates the necessary links to the DLL file required to run the application. Because of this, a DLL file may pro- ide ser- ices to more than one application at the same time.

## What do DLL Files Do?

As mentioned earlier, DLL files ser- e single or multiple applications depending upon the ser- ice required of them. For example, you may call an *xyz.dll* file to print a page. Usually, these DLL files come with the operating system.

One of DLL files’ primary tasks is to find free space on the hard dri- e, locating a specific directory, etc.

## How Dynamic Linking Helps?

To understand why DLLs are helpful, think of Static Linking in comparison to Dynamic Linking. Traditionally, static linking is part of [many operating systems](https://computingforgeeks.com/linux-- s-windows-introduction-for-newbies/). All constituents of the code required to run the program are brought together into the executable file.

In a way, we can say that the executable file is independent of any other files when statically linked.

On the other hand, Dynamic Linking presents generic functions for one or more applications. Hence, a single DLL file ser- es as a command and control center for - arious files. 

Thus, each application doesn’t require its code. Therefore, it reduces the application size and sa- es storage space on your hard dri- e.

# Building blocks of .NET – CLR, CTS, CLS

From a programmer’s point , .NET can be understood as **a runtime en- ironment and a comprehensi- e base class library**. The **runtime layer** is properly referred to as the **Common Language Runtime**, or **CLR**. 

The primary role of the CLR is to **locate, load, and manage .NET objects** on your behalf. The CLR also takes care of a number of low-le- el details such as 

- memory management

- application hosting

- coordinating threads

- Performing

- security checks 

# .Net Framework Architecture

# Assemblies

# Creating .NET Applications using C#

# .Net Framework History

## COM

## Abhilash

## C++ and Ja- a diff in datatype

# Benefits of .Net Platform 

# Windows Application DLL File

Windows assembly GAC_MSIL System system.dll
