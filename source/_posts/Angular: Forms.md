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

# Overview

Angular provides two different approaches to handling user input through forms: reactive and template-driven. Both capture user input events from the view, validate the user input, create a form model and data model to update, and provide a way to track changes.

# Form

**Reactive** forms and **template-driven** forms process and manage form data differently. Each approach offers different advantages.

- **Reactive forms** provide direct, explicit access to the underlying forms object model. Compared to template-driven forms, they are more robust: **they're more scalable, reusable, and testable**. If forms are a key part of your application, or you're already using reactive patterns for building your application, use reactive forms.
- **Template-driven forms** rely on directives in the template to create and manipulate the underlying object model. They are useful for adding a **simple** form to an app, such as <u>an email list signup form</u>. They're easy to add to an app, but they don't scale as well as reactive forms. If you have very basic form requirements and logic that can be managed solely in the template, template-driven forms could be a good fit.

### Key differences

The table below summarizes the key differences between reactive and template-driven forms.

|                                                              | REACTIVE                             | TEMPLATE-DRIVEN                 |
| :----------------------------------------------------------- | :----------------------------------- | :------------------------------ |
| [Setup of form model](https://angular.io/guide/forms-overview#setup) | Explicit, created in component class | Implicit, created by directives |
| [Data model](https://angular.io/guide/forms-overview#mutability-of-the-data-model) | Structured and immutable             | Unstructured and mutable        |
| [Data flow](https://angular.io/guide/forms-overview#data-flow-in-forms) | Synchronous                          | Asynchronous                    |
| [Form validation](https://angular.io/guide/forms-overview#validation) | Functions                            | Directives                      |

## Setting up the form model

Both reactive and template-driven forms track value changes between the form input elements that users interact with and the form data in your component model. The two approaches share underlying building blocks, but differ in how you create and manage the common form-control instances.

### Common form foundation classes

Both reactive and template-driven forms are built on the following base classes.

- `FormControl` **tracks the value and validation** status of **an individual form control**.
- `FormGroup` **tracks the same values and status for a collection of form controls**.
- `FormArray` tracks the same values and status for **an array of form controls**.
- `ControlValueAccessor` **creates a bridge between Angular `FormControl` instances and native DOM elements**.

### Setup in reactive forms

With reactive forms, you define the form model directly in the component class. The `[formControl]` directive links the explicitly created `FormControl` instance to a specific form element in the view, using an internal value accessor.

The following component implements an input field for a single control, using reactive forms. In this example, the form model is the `FormControl` instance.

```typescript
content_copyimport { Component } from '@angular/core';
import { FormControl } from '@angular/forms';

@Component({
  selector: 'app-reactive-favorite-color',
  template: `
    Favorite Color: <input type="text" [formControl]="favoriteColorControl">
  `
})
export class FavoriteColorComponent {
  favoriteColorControl = new FormControl('');
}
```

Figure 1 shows how, in reactive forms, the form model is the source of truth; it provides the value and status of the form element at any given point in time, through the `[formControl]` directive on the input element.

Steps 1：import { FormsModule, ReactiveFormsModule } from '@angular/forms'; in app.module

Step 2: Create the required model as we done directly access the FormControl, we use NgModel directive

Stop 3:Create HTML Form

Step 4: Elemenet should have name attribute

Step 5: NgModel
