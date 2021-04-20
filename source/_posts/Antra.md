---
title: Antra Interview Experience
date: 04/20/2021
updated: 
tags: 
  - notes
  - interview
categories: interview
keywords: 
  - java
  - oop
  - leetcode
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

# **Antra Interview Experience**

# **Part I** First Interview





```java
import java.io.*;
import java.util.*;


class MyCode {
    /**
     * 1. Question: Why the amap size is 3? Instead of 4 even though we called put() method 3 times
     *    Answer:
     *  In the main method we only create 3 new objects , even we set a2 = a , they are the same object so the size is 3
     * 2. Fixed the code(Apple class) to let the map treat the apples with the same color as the same key. So the amap size will be 1. Output should be "map size is 1"
     * * DO NOT Change the main method
     */
    public static void main(String[] args){
        Apple a = new Apple("red", 10);
        Apple a1 = new Apple("red", 10);
        Apple a2 = a;
        Apple a3 = new Apple("red", 20);

        Map<Apple, String> amap = new HashMap<>();
        amap.put(a,"one apple");
        amap.put(a1,"two apples");
        amap.put(a2,"three apples");
        amap.put(a3,"four apples");

        System.out.printf("map size is %s \n", amap.size());
    }
}


class Apple {
    private int price;
    private String color;
    HashSet<String> set = new HashSet();
    public Apple(String color,int price) {
        
        this.price = price;
        this.color = color;
        
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        
        this.color = color;
    }
    
    @Override
    public String toString() {
        return "Apple{" +
                "color='" + color + '\'' +
                '}';
    }
}
```

# **Part II** Source from Web

# multithread

# hash table vs hash map

# volatile

# final

# checked exception

# SQL normalization 

# **Part III** Coding Source



# Find top k freq element in a list

# **Part IV** Source from HR



# Usage of Collections in coding: 

## List

## Set

## Map

## minimum ArrayList

## LinkedList

## HashMap (hashCode equals)

  Sorting a List/Array in a given attribute. Like sort a list of students by age or name.

# basic java coding: 

# String

# sub-class

# constructor

# getter/setter

## Leetcode easy level

# Advanced Concepts in Java: 

# OOP

# SOLID

# MVC

# design patterns

# multithreading



# basic network: 

# HTTP

# TCP

# basic DB: 

# SQL

# joins

# index

any thing showing on their resumes.


1. Collections in Java.
2. Multithreading in Java.
3. Lambda and Stream in Java 8.
4. HTTP protocol.
5. Have Any one of : AWS, MongoDB, Angular, React, NodeJS, Algorithms

# 