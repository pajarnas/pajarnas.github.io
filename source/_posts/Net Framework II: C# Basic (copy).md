---

title: .Net Framework II: C# Ba
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

JSON Config file

Schemea will auto downloaded from json.schemastore.org, so the name is important, appsetting.json

Object name should be the same as Class but with a carmel style. 

# Fundamentals ->Type System

## Namespace

1. declaring your own namespaces can help you control the scope of class and method names in larger programming projects. Use the [namespace](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/namespace) keyword to declare a namespace, as in the following example:
2. .NET uses namespaces to organize its many classes

# Types -> Value Types

## Real literals

The type of a real literal is determined by its suffix as follows:

- The literal without suffix or with the `d` or `D` suffix is of type `double`
- The literal with the `f` or `F` suffix is of type `float`
- The literal with the `m` or `M` suffix is of type `decimal`

```c#
Console.WriteLine($"Multiplication = {multiply}")
double x = 23.13d;
float y = 12.13f; 
```

# Factory Design pattern

A factory is used to implement factory design pattern which means it is responsible to return the object of the base type using derived type constructor or concreate derived object. 
