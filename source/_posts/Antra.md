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

### 1) What is multithreading?

Multithreading is a process of executing multiple threads simultaneously. Multithreading is used to obtain the multitasking. It consumes less memory and gives the fast and efficient performance. Its main advantages are:

- Threads share the same address space.
- The thread is lightweight.
- The cost of communication between the processes is low.

[More details.](https://www.javatpoint.com/multithreading)

------

### 2) What is the thread?

A thread is a lightweight subprocess. It is a separate path of execution because each thread runs in a different stack frame. A process may contain multiple threads. Threads share the process resources, but still, they execute independently.

# hash table vs hash map

**1. Synchronization or Thread Safe :** This is the most important difference between two . HashMap is non synchronized and not thread safe.On the other hand, Hashtable is thread safe and synchronized.

**2. Null keys and null values :** HashMap allows one null key and any number of null values, while Hashtable do not allow null keys and null values in the Hashtable object.

**3. Iterating the values:** HashMap object values are iterated by using iterator .Hashtable is the only class other than vector which uses enumerator to iterate the values of Hashtable object.

**4. Fail-fast iterator** : The iterator in HashMap is fail-fast iterator while the enumerator for Hashtable is not.

**5. Performance :** HashMap is much faster and uses less memory than Hashtable as former is unsynchronized . Unsynchronized objects are often much better in performance in compare to synchronized object like Hashtable in single threaded environment.

# volatile

volatile keyword.

volatile keyword indicates that a variable's value will be modified by different threads.

When a java variable is declared volatile,

- The value of that varilable will not be cached thread-locally, all read/write will be directed to the "main memory".
- Access to the variable is synchronized on itself.

Difference between synchronized and volatile:



| synchronized/ˈsiNGkrəˌnīz/                                   | volatile/ˈvälədl/                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Synchronized block applies only to object.                   | volatile keyword can be applied to Object or primitive types. |
| Synchronized block does not work on null. Attempting to synchronize on a null object will throw a NullPointerException. | volatile variables can be null.                              |
| synchronized blocks other threads while one thread is accessing the block. | volatile does not block any threads.                         |
| synchronization occurs when you enter a synchronized block.  | synchronization occurs when a volatile variable is accessed. |

# final

The final keyword can be used with a class, method, and variables. 

- If it is used with class then it prevents inheritance by not allowing you to create subclasses. 
- If it is used with methods then it prevents overriding, you cannot override a final method in Java. 
- If it is used with variables then they are treated as constant because you cannot change their value once assigned.
- The final variable can only be assigned during the class instantiate cycl

# checked exception

# SQL normalization 

Database Normalization is a set of rules that are applied to a database, such that the schema of the database ensures that all the rules are being followed. These rules are also known as Normal Forms and are widely used while designing database solutions.

### First Normal Form (1NF)

- Data is stored in tables with rows that can be uniquely identified by a Primary Key.
- Data within each table is stored in individual columns in its most reduced form.
- There are no repeating groups.

### Second Normal Form (2NF)

- All the rules from 1NF must be satisfied.
- Only those data that relates to a table’s primary key is stored in each table.

### Third Normal Form (3NF)

- All the rules from 2NF must be satisfied.
- There should be no intra-table dependencies between the columns in each table.

# **Part III** Coding Source



# Find top k freq element in a list

# **Part IV** Source from HR



# Usage of Collections in coding: 

## List 

**List** in Java provides the facility to maintain the ***ordered collection***. It is a ***interface***. 

The List interface is found in the ```java.util``` package and inherits the Collection interface. 

```List``` is an interface whereas ```ArrayList``` is the implementation class of List.

### How to create List

The ArrayList and LinkedList classes provide the implementation of List interface. Let's see the examples to create the List:

 ```java
    //Creating a List of type String using ArrayList 
    List<String> list=new ArrayList<String>(); 
    
   //Creating a List of type Integer using ArrayList 
   List<Integer> list=new ArrayList<Integer>(); 
    
   //Creating a List of type Book using ArrayList 
   List<Book> list= new ArrayList<Book>();   
   
   //Creating a List of type String using LinkedList 
   List<String> list=new LinkedList<String>(); 
 ```

   

In short, you can create the List of any type. The ```ArrayList<T>``` and ```LinkedList<T>``` classes are used to specify the type. Here, ```T``` denotes the type.

Example:

```java
import java.util.*;  
public class ListExample1{  
	public static void main(String args[]){  
         //Creating a List  
         List<String> list=new ArrayList<String>();  
         //Adding elements in the List  
         list.add("Mango");  
         list.add("Apple");  
         list.add("Banana");  
         list.add("Grapes");  
         //Iterating the List element using for-each loop  
         for(String fruit:list)  
          System.out.println(fruit);  

    }  
}  
```

```java
//How to convert Array to List
import java.util.*;  
public class ArrayToListExample{  
    public static void main(String args[]){  
    	//Creating Array  
        String[] array={"Java","Python","PHP","C++"};  
        System.out.println("Printing Array: "+Arrays.toString(array));  
        //Converting Array to List  
        List<String> list=new ArrayList<String>();  
        for(String lang:array){  
            list.add(lang);  
        }  
        System.out.println("Printing List: "+list);  

    }  
}  
/*
output
Printing Array: [Java, Python, PHP, C++]
Printing List: [Java, Python, PHP, C++]
*/
```

```java
import java.util.*;  
public class ListToArrayExample{  
    public static void main(String args[]){  
         List<String> fruitList = new ArrayList<>();    
         fruitList.add("Mango");    
         fruitList.add("Banana");    
         fruitList.add("Apple");    
         fruitList.add("Strawberry");    
         //Converting ArrayList to Array  
         String[] array = fruitList.toArray(new String[fruitList.size()]);    
         System.out.println("Printing Array: "+Arrays.toString(array));  
         System.out.println("Printing List: "+fruitList);  	
    }  
}  
```

## LinkedList

```java
import java.util.*;  
public class LinkedList1{  
 public static void main(String args[]){  
  
  LinkedList<String> al=new LinkedList<String>();  
  al.add("Ravi");  
  al.add("Vijay");  
  al.add("Ravi");  
  al.add("Ajay");  
  
  Iterator<String> itr=al.iterator();  
  while(itr.hasNext()){  
   System.out.println(itr.next());  
  }  
 }  
}  
```

| ArrayList                                                    | LinkedList                                                   |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1) ArrayList internally uses a **dynamic array** to store the elements. | LinkedList internally uses a **doubly linked list** to store the elements. |
| 2) Manipulation with ArrayList is **slow** because it internally uses an array. If any element is removed from the array, all the bits are shifted in memory. | Manipulation with LinkedList is **faster** than ArrayList because it uses a doubly linked list, so no bit shifting is required in memory. |
| 3) An ArrayList class can **act as a list** only because it implements List only. | LinkedList class can **act as a list and queue** both because it implements List and Deque interfaces. |
| 4) ArrayList is **better for storing and accessing** data.   | LinkedList is **better for manipulating** data.              |

## Set

```java
import java.util.*;  
class HashSet2{  
 public static void main(String args[]){  
  //Creating HashSet and adding elements  
  HashSet<String> set=new HashSet<String>();  
  set.add("Ravi");  
  set.add("Vijay");  
  set.add("Ravi");  
  set.add("Ajay");  
  //Traversing elements  
  Iterator<String> itr=set.iterator();  
  while(itr.hasNext()){  
   System.out.println(itr.next());  
  }  
 }  
}  
```



## Map



## HashMap (hashCode equals)

  Sorting a List/Array in a given attribute. Like sort a list of students by age or name.

**two objects, which are not equal to equals() method can still return same hashCode.**

Hashcode is a fundamental method in every Java.Lang.Object.  The hashCode method is an inbuilt method that returns the integer hashed value of the input value. Here are a few key concepts to remember: 

Multiple invocations of the hashCode must return the same integer value within the execution of a program unless the Object used within the equals method changes. 

The integer value need not be the same for the next implementation. If two or more objects are equal according to the equals method, then their hashes should be equal too. If two or more objects are not equal according to the equals method, then their hashes can be equal or unequal.

# basic java coding: 

# Primitive Data Types

![](E:\github_repos\pajarnas.github.io\themes\butterfly\source\img\Java_Primitive_Data_Types_Interview_Questions.png)

https://www.interviewgrid.com/interview_questions/java/java_data_types

# String

## immutable

Strings in Java programming language are immutable, i.e. once a string object is created its value cannot be changed. When you change the value of a string reference variable, internally the java virtual machine creates a new string in memory and returns that value. The old string still exists in memory but is not being referenced.

https://www.interviewgrid.com/intervie![](E:\github_repos\pajarnas.github.io\themes\butterfly\source\img\Java_String_Immutability_Interview_Questions.png)

## String constant pool

Strings literals in Java programming language are immutable. Once a string is created in memory it cannot be changed. If a string literal has to be changed, the Java virtual machine creates the new string literal in memory and returns it.

To make it more memory efficient, the Java virtual machine has a special area of memory called the String constant pool. When a new string is required, the Java virtual machine first checks if the string literal exists in the string constant pool. If it exists then the string reference variable will refer to this string literal, a new literal in not created in memory. If the string literal does not exists in memory then a new string literal is created in the string constant pool.



![](E:\github_repos\pajarnas.github.io\themes\butterfly\source\img\Java_String_Constant_Pool_Interview_Questions.png)

## String-builder String-Buffer

String objects are immutable. Once a string object is created then its value cannot change. Every time you want to get a modified string value, the Java virtual machine will create a new string object. So if you modify a string 100 times, 100 string objects are created in memory. 

Unlike string objects, StringBuilder objects are mutable. You can change the value of a string builder object without creating a new object. So you can modify a StringBuilder object many times, but only a single instance of the StringBuilder object is created. 

StringBuilder is not thread safe, i.e it's methods are not synchronized; whereas StringBuffer is thread safe, i.e it's methods are synchronized. Since the methods of StringBuilder are not synchronized, it is faster than StringBuffer. If thread safety is not a requirement, you should use StringBuilder instead of StringBuffer.

## key methods in String class

**toCharArray()** - Returns an array of the string's characters

**equals()** - Returns true if this string matches the text of another string object.

**equalsIgnoreCase()** - Returns true if this string matches the text of another string object ignoring the case.

**length()** - Returns the length of the string.

**subString()** - Returns part of the string. You have to specify the start index and end index.

```java
str = str.substring(1);
```

**concat()** - Appends another string to this string.

```java
String str = "123";
String str2 = "456";
String arrOfStr = str.concat(str2);
System.out.println(arrOfStr);
```

**split()** - Splits the string based on a delimiter. returns a string array

```java
String str = "geekss@for@geekss";
String[] arrOfStr = str.split(",", 2);

for (String a : arrOfStr)
    System.out.println(a);
```

## key methods in String-builder

**append()** - Appends another string to this string.

**insert()** - Inserts another string into this string. You have to specify the index at which the string has to be included.

**delete()** - Deletes part of the string.

**reverse()** - Reverses the characters of a string.

**toString()** - Returns a string representation of the StringBuffer or StringBuilder.

## char Array 

### **Declaring Char Array**

Declaration of a char array can be done by using square brackets:

```java
char[] JavaCharArray;
```

The square brackets can be placed at the end as well.

```java
char JavaCharArray[];
```

The next step is to initialize these arrays

#### **Initializing Char Array**

A char array can be initialized by conferring to it a default size.

```java
char[] JavaCharArray = new char[4];
```

This assigns to it an instance with size 4.

We use the following code to assign values to our char array:

```java
char[] JavaCharArray = new char[5];
JavaCharArray[0] = 'r';
JavaCharArray[1] = 's';
JavaCharArray[2] = 't';
JavaCharArray[3] = 'u';
```

Loops play a very important role when it comes to avoiding repetitive code, this is the next bit of this Char Array in Java article,

```java
char[] JavaCharArray = {'r', 's', 't', 'u', 'v'};
for (char c:JavaCharArray) {
System.out.println(c);
}
```

# Array

```
int intArray[];    //declaring array
intArray = new int[20];  // allocating memory to array
 int[] intArray = new int[]{ 1,2,3,4,5,6,7,8,9,10 }; 
```

# sub-class

# Abstract Class and Interface

Data **abstraction** is the process of hiding certain details and showing only essential information to the user. Abstraction can be achieved with either **abstract classes** or **interfaces**. 

## abstract classes

- **Abstract class:** is a restricted class that cannot be used to create objects (to access it, it must be inherited from another class). 
- It can not be **instantiated** by **keyword** "**new**". The normal class can be **instantiated** by **keyword** "**new**". 
- It would need **constructors** since it requires the memory allocation for the **members** or **properties**.  

- **Abstract method:** can only be used in an abstract class, and it does not have a body. The body is provided by the subclass (inherited from).

An abstract class can have both abstract and regular methods:

```java
// Abstract class
abstract class Animal {
  // Abstract method (does not have a body)
  public abstract void animalSound();
  // Regular method
  public void sleep() {
    System.out.println("Zzz");
  }
}

// Subclass (inherit from Animal)
class Pig extends Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig(); // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

## interfaces

Interface in Java is similar to class but, it contains only abstract methods and fields which are final and static.

- An interface is a **reference type** in Java. It is similar to class. **It is a collection of abstract methods.**
- An interface cannot be  **instantiate**.
- An interface does **not** contain any **constructors**.
- An interface cannot contain **instance fields**. The only **fields** that can appear in an interface must be **declared both static and final**.
- An interface is not extended by a class; it is **implemented** by a class.
- An interface can extend multiple interfaces.

# interface

- It is used to achieve total abstraction.

- Since java does not support multiple inheritance in case of class, but by using interface it can achieve multiple inheritance .

- It is also used to achieve loose coupling.

- Interfaces are used to implement abstraction. So the question arises why use interfaces when we have abstract classes?

# constructor

# getter/setter

## Leetcode easy level

# Advanced Concepts in Java: 

# OOP

# SOLID

| Principle                           | Description                                                  |
| :---------------------------------- | :----------------------------------------------------------- |
| **Single Responsibility Principle** | Each class should be responsible for a single part or functionality of the system. |
| **Open-Closed Principle**           | Software components should be open for extension, but not for modification. |
| **Liskov Substitution Principle**   | Objects of a superclass should be replaceable with objects of its subclasses without breaking the system. |
| **Interface Segregation Principle** | No client should be forced to depend on methods that it does not use. |
| **Dependency Inversion Principle**  | High-level modules should not depend on low-level modules, both should depend on abstractions. |

https://www.educative.io/edpresso/what-are-the-solid-principles-in-java

# MVC

# design patterns

# multithreading

# OOP

There are four main OOP concepts in Java. These are:

- **Abstraction.** Abstraction means using simple things to represent complexity. We all know how to turn the TV on, but we don’t need to know how it works in order to enjoy it. In Java, abstraction means simple things like **objects**, **classes**, and **variables** represent more complex underlying code and data. This is important because it lets avoid repeating the same work multiple times.
- **Encapsulation.** en·cap·su·la·tion. This is the practice of keeping fields within a class private, then providing access to them via public methods. It’s a protective barrier that keeps the data and code safe within the class itself. This way, we can re-use objects like code components or variables without allowing open access to the data system-wide.
- **Inheritance.** /inˈherədəns/This is a special feature of Object Oriented Programming in Java. It lets programmers create new classes that share some of the attributes of existing classes. This lets us build on previous work without reinventing the wheel.
- **Polymorphism.** /ˌpälēˈmôrfizəm/This Java OOP concept lets programmers use the same word to mean different things in different contexts. One form of polymorphism in Java is **method overloading**. That’s when different meanings are implied by the code itself. The other form is **method overriding**. That’s when the different meanings are implied by the values of the supplied variables. See more on this below.

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