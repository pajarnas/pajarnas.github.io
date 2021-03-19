---
title: Beaconfire Interview Experience
date: 03/19/2021
updated: 
tags: notes, leetcode, interview
categories: interview
keywords: java, oop, leetcode
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

# **Beaconfire Interview Experience**

# **Part I**

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

# final modifier

The final keyword can be used with a class, method, and variables. 

- If it is used with class then it prevents inheritance by not allowing you to create subclasses. 
- If it is used with methods then it prevents overriding, you cannot override a final method in Java. 
- If it is used with variables then they are treated as constant because you cannot change their value once assigned.
- The final variable can only be assigned during the class instantiate cycle. 

# Overloading and overriding

**Overloading** : If two or more methods have same name, but different argument then it is called method overloading.

| **Number of Arguments** | Overloaded method can have different number of arguments     |
| ----------------------- | ------------------------------------------------------------ |
| **Date type**           | Overload method can have different data type for argument    |
| **Return type**         | Return type can be changed but either number of argument or data type of argument should also be changed. |
| **Order of arguments**  | If you change sequence of arguments then it is also valid method overloading provided you have different data types arguments. |
| **Constructor**         | Can be overloaded                                            |

**Overriding**: 

- If subclass is having same method as base class then it is known as method overriding Or in another words.

- If subclass provides specific implementation to any method which is present in its one of parents classes then it is known as method overriding.

| **Arguments**       | Must not change                                              |
| ------------------- | ------------------------------------------------------------ |
| **Return type**     | Can’t change except for covariant (subtype) returns          |
| **Access Modifier** | Must not be more restrictive. Can be less restrictive.       |
| **Exceptions**      | Can reduce or eliminate but must not throw new/broader checked exceptions |
| **Constructor**     | Can not be overridden                                        |
| **Static method**   | Can not be overridden                                        |
| **final method**    | Can not be overridden                                        |

# array list vs linked list

**Linked List** are linear data structures where the elements are **not** stored in **contiguous** locations and every element is a separate object with a data part and address part. 

- The elements are linked using pointers and addresses. 

- Each element is known as a **node**. 

- Due to the dynamicity and ease of insertions and deletions, they are preferred over the arrays. 

**Array List** is a part of the **collection framework**. 

- It is present in the **java.util** package and provides us dynamic arrays in Java. 

- Though, it may be slower than standard arrays but can be helpful in programs where lots of manipulation in the array is needed. 

- We can dynamically add and remove items. It automatically resizes itself. 

## Difference 

| ArrayList                                                    | LinkedList                                                   |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| This class uses a dynamic array to store the elements in it. With the introduction of [generics](https://www.geeksforgeeks.org/generics-in-java/), this class supports the storage of all types of objects. | This class uses a [doubly linked list](https://www.geeksforgeeks.org/doubly-linked-list/) to store the elements in it. Similar to the ArrayList, this class also supports the storage of all types of objects. |
| Manipulating ArrayList takes more time due to the internal implementation. Whenever we remove an element, internally, the array is traversed and the memory bits are shifted. | Manipulating LinkedList takes less time compared to ArrayList because, in a doubly-linked list, there is no concept of shifting the memory bits. The list is traversed and the reference link is changed. |
| This class implements a [List interface](https://www.geeksforgeeks.org/list-interface-java-examples/). Therefore, this acts as a list. | This class implements both the [List interface](https://www.geeksforgeeks.org/list-interface-java-examples/) and the [Deque interface](https://www.geeksforgeeks.org/deque-interface-java-example/). Therefore, it can act as a list and a deque. |
| This class works better when the application demands storing the data and accessing it. | This class works better when the application demands manipulation of the stored data. |

# array vs array list

An array is a collection of items stored at contiguous memory locations. 

- The idea is to store multiple items of the same type together. 
- However, the limitation of the array is that the size of the array is predefined and fixed.

## Difference

- An array is basic functionality provided by Java. ArrayList is part of collection framework in Java. Therefore array members are accessed using [], while ArrayList has a set of methods to access elements and modify them.
- Array is a fixed size data structure while ArrayList is not. One need not to mention the size of Arraylist while creating its object. Even if we specify some initial capacity, we can add more elements.
- Array can contain both primitive data types as well as objects of a class depending on the definition of the array. However, ArrayList only supports object entries, not the primitive data types.
  Note: When we do arraylist.add(1); : it converts the primitive int data type into an Integer object. 
- Since ArrayList can’t be created for primitive data types, members of ArrayList are always references to objects at different memory locations (See [this](https://www.geeksforgeeks.org/g-fact-46/) for details). Therefore in ArrayList, the actual objects are never stored at contiguous locations. References of the actual objects are stored at contiguous locations.
  In array, it depends whether the arrays is of primitive type or object type. In case of primitive types, actual values are contiguous locations, but in case of objects, allocation is similar to ArrayList.
- Java ArrayList supports many additional operations like [indexOf()](http://java.util.arraylist.indexof() in java/), [remove()](https://www.geeksforgeeks.org/arraylist-linkedlist-remove-methods-java-examples/), etc. These functions are not supported by Arrays.

# HashMap

 It provides the basic implementation of the Map interface of Java. It stores the data in **(Key, Value) pairs**, and you can access them by an index of another type (e.g. an Integer). One object is used as a key (index) to another object (value). If you try to insert the duplicate key, it will replace the element of the corresponding key.

## Implement 

handle collisions 

- closed addressing(open hashing)

  In Open Hashing each cell in the array points to a list containg the collisions. The hashing has produced the same index for all items in the linked list.

- open addressing(close hashing)

  In Closed Hashing you use only one array for everything. You store the collisions in the same array. The trick is to use some smart way to jump from collision to collision until you find what you want. And do this in a reproducible / deterministic way.

```java
public class MyHashMap {
    // for better re-sizing is taken as 2^4
    private static final int SIZE = 16;

    private Entry table[] = new Entry[SIZE];

    /**
       * To store the Map data in key and value pair.
       * Used linked list approach to avoid the collisions
       */
    class Entry {
        final String key;
        String value;
        Entry next;

        Entry(String k, String v) {
            key = k;
            value = v;
        }

        public String getValue() {
            return value;
        }

        public void setValue(String value) {
            this.value = value;
        }

        public String getKey() {
            return key;
        }
    }

    /**
       * Returns the entry mapped to key in the HashMap.
       */
    public Entry get(String k) {
        int hash = k.hashCode() % SIZE;
        Entry e = table[hash];

        // Bucket is identified by hashCode and traversed the bucket
        // till element is not found.
        while(e != null) {
            if(e.key.equals(k)) {
                return e;
            }
            e = e.next;
        }
        return null;
    }

    /**
       * If the map previously contained a mapping for the key, the old
       * value is replaced.
       */
    public void put(String k, String v) {
        int hash = k.hashCode() % SIZE;
        Entry e = table[hash];

        if(e != null) {
            // If we will insert duplicate key-value pair,
            // Old value will be replaced by new one.
            if(e.key.equals(k)) {
                e.value = v;
            } else {
                // Collision: insert new element at the end of list
                // in the same bucket
                while(e.next != null) {
                    e = e.next;
                }
                Entry entryInOldBucket = new Entry(k, v);
                e.next = entryInOldBucket;
            }
        } else {
            // create new bucket for new element in the map.
            Entry entryInNewBucket = new Entry(k, v);
            table[hash] = entryInNewBucket;
        }
    }

    public static void main(String[] args) {
        MyHashMap myHashMap = new MyHashMap();

        myHashMap.put("Awadh", "SSE");
        myHashMap.put("Rahul", "SSE");
        myHashMap.put("Sattu", "SE");
        myHashMap.put("Gaurav", "SE");

        Entry e = myHashMap.get("Awadh");
        System.out.println(""+e.getValue());
    }
}
```

# **Part II**

Destination City

Next Greater Element I

Number of Longest Increasing Subsequence