---

title: Angular Routing
date: 06/16/2021
updated: 
tags: 
  - notes
  - Angular
  - Angular-Routing
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
copyright_author_href:https://www.newline.co/books/ng-book-2/
copyright_url:https://www.newline.co/books/ng-book-2/
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# Routing

## How client-side routing works

Perhaps you've written server-side routing code before (though, it isn't necessary to complete this chapter). Generally with server-side routing, the HTTP request comes in and the server will render a different controller depending on the incoming URL.

### The beginning: using anchor tags

Client-side routing started out with a clever hack: Instead of using a normal server-side URL for a page in our SPA, we use the *anchor tag* as the client-side URL.

As you may already know, anchor tags were traditionally used to link directly to a place *within* the webpage and make the browser scroll all the way to where that anchor was defined. For instance, if we define an anchor tag in an HTML page:

**And we visited the URL `http://something/#about`, the browser would jump straight to that H1 tag that identified by the `about` anchor.**

The clever move for client-side frameworks used for SPAs was to take the anchor tags and use them represent the routes within the app by formatting them as paths.

For example, the `about` route for an SPA would be something like `http://something/#/about`. This is what is known as **hash-based routing**.

What's neat about this trick is that it looks like a "normal" URL because we're starting our anchor with a slash (`/about`).



## Components of Angular routing

There are **three main components** that we use to configure routing in Angular:

- `Routes` describes the routes our application supports
- `RouterOutlet` is a "placeholder" component that shows Angular where to put the content of each route
- `RouterLink` directive is used to link to routes

### Imports

In order to use the router in Angular, we import constants from the `@angular/router` package:

Now we can define our router configuration.

```typescript
// src/app/app.module.ts
import {
  RouterModule,
  Routes
} from '@angular/router';
```



### `RouterOutlet` using `<router-outlet>`

```<router-outlet>``` in Angular works as a placeholder which **is used to load the different components dynamically based on the activated component or current route state.** 

When we change routes, we want to keep our outer "layout" template and only substitute the "inner section" of the page with the route's component.

In order to describe to Angular where in our page we want to render the contents for each route, we use the `RouterOutlet`directive.

Our component `@Component` has a `template` which specifies some `div` structure, a section for `Navigation`, and a directive called `router-outlet`.

**The `router-outlet` element indicates where the contents of each route component will be rendered.**

> We are are able to use the `router-outlet` directive in our template because we imported the `RouterModule`in our `NgModule`.

Here's the component and template for the navigation wrapper of our app:

```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  constructor(private router: Router) {
  };
}
```



and the template:

```html
<div class="page-header">
  <div class="container">
    <h1>Router Sample</h1>
    <div class="navLinks">
      <a [routerLink]="['/home']">Home</a>
      <a [routerLink]="['/about']">About Us</a>
      <a [routerLink]="['/contact']">Contact Us</a>
      |
      <a [routerLink]="['/products']">Products</a>
      <a [routerLink]="['/login']">Login</a>
      <a [routerLink]="['/protected']">Protected</a>
    </div>
  </div>
</div>

<div id="content">
  <div class="container">
    <router-outlet></router-outlet>
  </div>
</div>
```



If we look at the template above, you will note the `router-outlet` element right below the navigation menu. When we visit `/home`, that's where `HomeComponent` template will be rendered. The same happens for the other components.

### `RouterLink` using `[routerLink]`

Now that we know where route templates will be rendered, how do we tell Angular to navigate to a given route?

We might try linking to the routes directly using pure HTML:

Home

But if we do this, we'll notice that clicking the link triggers a page reload and that's definitely not what we want when programming single page apps.

To solve this problem, Angular provides a solution that can be used to link to routes **with no page reload**: the `RouterLink` directive.

This directive allows you to write links using a special syntax:

```html
    <h1>Router Sample</h1>
    <div class="navLinks">
      <a [routerLink]="['/home']">Home</a>
      <a [routerLink]="['/about']">About Us</a>
      <a [routerLink]="['/contact']">Contact Us</a>
      
```



We can see on the left-hand side the `[routerLink]` that applies the directive to the current element (in our case `a` tags).

Now, on the right-hand side we have an array with the route path as the first element, like `"['/home']"` or `"['/about']"`that will indicate which route to navigate to when we click the element.

It might seem a little odd that the value of `routerLink` is a string with an array containing a string (`"['/home']"`, for example). This is because there are more things you can provide when linking to routes, but we'll look at this into more detail when we talk about child routes and route parameters.

For now, we're only using routes names from the root app component.

# 
