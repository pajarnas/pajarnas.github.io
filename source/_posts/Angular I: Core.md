---

title: Angular I Core
date: 06/16/2021
updated: 
tags: 
  - notes
  - Angular
  - Angular-Routing
  - Angular-Component
  - Angular-Data-Binding
categories: Angular
keywords: 
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Ng-book
copyright_author_href: 
copyright_url: 
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# Overview

- How to break your app into components
- How to make reusable components using **inputs**
- How to handle user interactions, such as clicking on a component

# Model

## Product Model

One of the key things to realize about Angular is that **it doesn't prescribe a particular model library**.

Angular is flexible enough to **support many different kinds of models (and data architectures)**. However, this means the choice is left to you as the user to determine how to implement these things.

 ```typescript
 /**
  * Provides a `Product` object
  */
 export class Product {
   constructor(
     public sku: string,
     public name: string,
     public imageUrl: string,
     public department: string[],
     public price: number) {
   }
 }
 ```

We're creating a new `Product` class and the `constructor` takes 5 arguments. When we write `public sku: string`, we're saying two things:

- there is a `public` variable on instances of this class called `sku`
- `sku` is of type `string`.

> If you're already familiar with JavaScript, you can quickly catch up on some of the differences, including the `public constructor` shorthand, [here at learnxinyminutes](https://learnxinyminutes.com/docs/typescript/)

This `Product` class doesn't have any dependencies on Angular, it's just a model that we'll use in our app.

# Components 

Each component is composed of three parts:

- Component **Decorator**
- A **View**
- A **Controller**

![Products List Component](https://d2uusema5elisf.cloudfront.net/books/ng-book-2/images/how-angular-works/app-diagram-product-list-focused.png)

# Decorator



```
@Component({
  selector: "inventory-app-root",
  template: `
  <div class="inventory-app">
     (Products will go here soon)
  </div>
  `
})
export class AppComponent {
  // Inventory logic here
}
```

The `@Component` is called a **decorator**. It adds metadata to the class that follows it (`AppComponent`). The `@Component`decorator specifies:

- a `selector`, which tells Angular what element to match
- a `template`, which defines the view

The Component **controller** is defined by a `class`, the `AppComponent` class, in this case.

Component => Services => API (Rest) HTTP Call Ajax Call in Angular HttpClient => API



Async/await and Tasks



Promises



Observiables =>



Observer pattern



Publish/subscribe pattern

