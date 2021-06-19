---

title: Angular Routing
date: 06/16/2021
updated: 
tags: 
  - notes
  - Angular
  - Angular-Property-Binding
  - Angular-Event-Binding
  - Angular-Two-Way-Binding
categories: Angular
keywords: 
  - Angular-Property-Binding
  - Angular-Event-Binding
  - Angular-Two-Way-Binding
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Angular
copyright_author_href: 
copyright_url: 
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# Property Binding

Property binding moves a value in one direction, from a component's property into a target element property.

## Binding to a property

To bind to an element's property, enclose it in square brackets, `[]`, which identifies the property as a target property. A target property is the DOM property to which you want to assign a value. For example, the target property in the following code is the image element's `src` property.

## Setting an element property to a component property value 

To bind the `src` property of an `<img>` element to a component's property, place the target, `src`, in square brackets followed by an equal sign and then the property. The property here is `itemImageUrl`.

```
<img [src]="itemImageUrl">
```

Declare the `itemImageUrl` property in the class, in this case `AppComponent`.

```
itemImageUrl = '../assets/phone.png';
```

## Setting a directive property

To set a property of a directive, **place the directive within square brackets , such as `[ngClass]`, followed by an equal sign and the property.** Here, the property is `classes`.

## Bind values between components

```
<p><img src="{{itemImageUrl}}"> is the <i>interpolated</i> image.</p> <p><img [src]="itemImageUrl"> is the <i>property bound</i> image.</p>
```



## interpolated

## Displaying values with interpolation

Interpolation refers to embedding expressions into marked up text. By default, interpolation uses the double curly braces `{{` and `}}` as delimiters.

To illustrate how interpolation works, consider an Angular component that contains a `currentCustomer`variable:

## Template expressions

A template **expression** produces a value and appears within double curly braces, `{{ }}`. Angular resolves the expression and assigns it to a property of a binding target. The target could be an HTML element, a component, or a directive.

### Resolving expressions with interpolation

More generally, the text between the braces is a template expression that Angular first evaluates and then converts to a string. The following interpolation illustrates the point by adding two numbers:

src/app/app.component.html

```html
content_copy<!-- "The sum of 1 + 1 is 2" -->
<p>The sum of 1 + 1 is {{1 + 1}}.</p>
```

### Syntax

Template expressions are similar to JavaScript. Many JavaScript expressions are legal template expressions, with the following exceptions.

You can't use JavaScript expressions that have or promote side effects, including:

- Assignments (`=`, `+=`, `-=`, `...`)
- Operators such as `new`, `typeof`, or `instanceof`
- Chaining expressions with `;` or `,`
- The increment and decrement operators `++` and `--`
- Some of the ES2015+ operators

Other notable differences from JavaScript syntax include:

- No support for the bitwise operators such as `|` and `&`
- New [template expression operators](https://angular.io/guide/template-expression-operators), such as `|`, `?.` and 

## Expression context

Interpolated expressions have a context—a particular part of the application to which the expression belongs. Typically, this context is the component instance.



# Event binding



Event binding allows you to listen for and respond to user actions such as keystrokes, mouse movements, clicks, and touches.

## Binding to events

To bind to an event you use the Angular event binding syntax. This syntax consists of a target event name within parentheses to the left of an equal sign, and a quoted template statement to the right. In the following example, the target event name is `click` and the template statement is `onSave()`.

Event binding syntax

```html
<div class="group">
  <h3>Target event</h3>
  <button (click)="onSave($event)">Save</button>

  <button on-click="onSave($event)">on-click Save</button>

  <h4>myClick is an event on the custom ClickDirective:</h4>
  <button (myClick)="clickMessage=$event" clickable>click with myClick</button>
  {{clickMessage}}

</div>
```

The event binding listens for the button's click events and calls the component's `onSave()` method whenever a click occurs.

```
onSave(event?: MouseEvent) {
    const evtMsg = event ? ' Event target is ' + (event.target as HTMLElement).textContent : '';
    alert('Saved.' + evtMsg);
    if (event) { event.stopPropagation(); }
  }
```



![Syntax diagram](https://angular.io/generated/images/guide/template-syntax/syntax-diagram.svg)

## Custom events with `EventEmitter`

[Directives](https://angular.io/guide/built-in-directives) typically raise custom events with an Angular [EventEmitter](https://angular.io/api/core/EventEmitter) as follows.

1. The directive creates an `EventEmitter` and exposes it as a property.
2. The directive then calls `EventEmitter.emit(data)` to emit an event, passing in message data, which can be anything.
3. Parent directives listen for the event by binding to this property and accessing the data through the `$event`object.

Consider an `ItemDetailComponent` that presents item information and responds to user actions. Although the `ItemDetailComponent` has a delete button, it doesn't contain the functionality to delete the hero. It can only raise an event reporting the user's delete request.

src/app/item-detail/item-detail.component.html (template)

```
content_copy<img src="{{itemImageUrl}}" [style.display]="displayNone">
<span [style.text-decoration]="lineThrough">{{ item.name }}
</span>
<button (click)="delete()">Delete</button>
```

The component defines a `deleteRequest` property that returns an `EventEmitter`. When the user clicks **Delete**, the component invokes the `delete()` method, telling the `EventEmitter` to emit an `Item` object.

src/app/item-detail/item-detail.component.ts (deleteRequest)

```
content_copy// This component makes a request but it can't actually delete a hero.
@Output() deleteRequest = new EventEmitter<Item>();

delete() {
  this.deleteRequest.emit(this.item);
  this.displayNone = this.displayNone ? '' : 'none';
  this.lineThrough = this.lineThrough ? '' : 'line-through';
}
```

The hosting parent component binds to the `deleteRequest` event of the `ItemDetailComponent` as follows.

src/app/app.component.html (event-binding-to-component)

```
content_copy<app-item-detail (deleteRequest)="deleteItem($event)" [item]="currentItem"></app-item-detail>
```

When the `deleteRequest` event fires, Angular calls the parent component's `deleteItem()` method with the item.

### Determining an event target

To determine an event target, Angular checks if the name of the target event matches an event property of a known directive. In the following example, Angular checks to see if `myClick` is an event on the custom `ClickDirective`.

src/app/app.component.html

```
content_copy<h4>myClick is an event on the custom ClickDirective:</h4>
<button (myClick)="clickMessage=$event" clickable>click with myClick</button>
{{clickMessage}}
```

If the target event name, `myClick` fails to match an element event or an output property of `ClickDirective`, Angular reports an "unknown directive" error.

## Sharing data between child and parent directives and components

## Sending data to a child component[*link*](https://angular.io/guide/inputs-outputs#sending-data-to-a-child-component)

The `@Input()` decorator in a child component or directive **signifies that the property can receive its value from its parent component**



![Input data flow diagram of data flowing from parent to child](https://angular.io/generated/images/guide/inputs-outputs/input.svg)

To use `@Input()`, **you must configure the parent and child.**

### Configuring the child component

To use the **`@Input()` decorator** in a child component class, **first import `Input` and then decorate the property with `@Input()`**, as in the following example.

src/app/item-detail/item-detail.component.ts

```typescript
content_copyimport { Component, Input } from '@angular/core'; // First, import Input
export class ItemDetailComponent {
  @Input() item = ''; // decorate the property with @Input()
}
```

In this case, `@Input()` decorates the property `item`, which has a type of `string`, however, `@Input()`properties can have any type, such as `number`, `string`, `boolean`, or `object`. The value for `item` comes from the parent component.

**Next, in the child component template, add the following:**

src/app/item-detail/item-detail.component.html

```
content_copy<p>
  Today's item: {{item}}
</p>
```

### Configuring the parent component

**The next step is to bind the property in the parent component's template.** In this example, the parent component template is `app.component.html`.

1. Use the child's selector, here `<app-item-detail>`, as a directive within the parent component template.
2. Use [property binding](https://angular.io/guide/property-binding) **to bind the `item` property in the child to the `currentItem` property of the parent.**

src/app/app.component.html

```
 <app-item-detail [item]="currentItem"></app-item-detail>
```

1. In the parent component class, designate a value for `currentItem`:

src/app/app.component.ts

```
 export class AppComponent {
  currentItem = 'Television';
}
```

With `@Input()`, Angular passes the value for `currentItem` to the child so that `item` renders as `Television`.

The following diagram shows this structure:

![Property binding diagram of the target, item, in square brackets set to the source, currentItem, on the right of an equal sign](https://angular.io/generated/images/guide/inputs-outputs/input-diagram-target-source.svg)

The target in the square brackets, `[]`, is the property you decorate with `@Input()` in the child component. The binding source, the part to the right of the equal sign, is the data that the parent component passes to the nested component.

### Watching for `@Input()` changes

To watch for changes on an `@Input()` property, you can use `OnChanges`, one of Angular's [lifecycle hooks](https://angular.io/guide/lifecycle-hooks). See the [`OnChanges`](https://angular.io/guide/lifecycle-hooks#onchanges) section of the [Lifecycle Hooks](https://angular.io/guide/lifecycle-hooks) guide for more details and examples.



## Sending data to a parent component

The `@Output()` decorator in a child component or directive allows data to flow from the child to the parent.

![Output diagram of the data flow going from child to parent](https://angular.io/generated/images/guide/inputs-outputs/output.svg)

`@Output()` marks a property in a child component as a doorway through which data can travel from the child to the parent.

**The child component uses the `@Output()` property to raise an event to notify the parent of the change. To raise an event, an `@Output()` must have the type of `EventEmitter`, which is a class in `@angular/core` that you use to emit custom events.**

The following example shows how to set up an `@Output()` in a child component that pushes data from an HTML `<input>` to an array in the parent component.

To use `@Output()`, you must configure the parent and child.

### Configuring the child component

The following example features an `<input>` where a user can enter a value and click a `<button>` that raises an event. The `EventEmitter` then relays the data to the parent component.

1. Import `Output` and `EventEmitter` in the child component class:

   ```js
    import { Output, EventEmitter } from '@angular/core';
   ```

2. In the component class, decorate a property with `@Output()`. The following example `newItemEvent``@Output()` has a type of `EventEmitter`, which means it's an event.

   src/app/item-output/item-output.component.ts

   ```typescript
    @Output() newItemEvent = new EventEmitter<string>();
   ```

   The different parts of the above declaration are as follows:

   - `@Output()`—a decorator function marking the property as a way for data to go from the child to the parent
   - `newItemEvent`—the name of the `@Output()`
   - `EventEmitter<string>`—the `@Output()`'s type
   - `new EventEmitter<string>()`—tells Angular to create a new event emitter and that the data it emits is of type string.

   For more information on `EventEmitter`, see the [EventEmitter API documentation](https://angular.io/api/core/EventEmitter).

3. Create an `addNewItem()` method in the same component class:

   src/app/item-output/item-output.component.ts

   ```
   content_copyexport class ItemOutputComponent {
   
     @Output() newItemEvent = new EventEmitter<string>();
   
     addNewItem(value: string) {
       this.newItemEvent.emit(value);
     }
   }
   ```

   **The `addNewItem()` function uses the `@Output()`, `newItemEvent`, to raise an event with the value the user types into the `<input>`.**

### Configuring the child's template

The child's template has two controls. The first is an HTML `<input>` with a [template reference variable](https://angular.io/guide/template-reference-variables) , `#newItem`, where the user types in an item name. The `value` property of the `#newItem` variable stores what the user types into the `<input>`.

src/app/item-output/item-output.component.html

```
content_copy<label for="item-input">Add an item:</label>
<input type="text" id="item-input" #newItem>
<button (click)="addNewItem(newItem.value)">Add to parent's list</button>
```

The second element is a `<button>` with a `click` [event binding](https://angular.io/guide/event-binding).

The `(click)` event is bound to the `addNewItem()` method in the child component class. The `addNewItem()`method takes as its argument the value of the `#newItem.value` property.

### Configuring the parent component

The `AppComponent` in this example features a list of `items` in an array and a method for adding more items to the array.

src/app/app.component.ts

```
content_copyexport class AppComponent {
  items = ['item1', 'item2', 'item3', 'item4'];

  addItem(newItem: string) {
    this.items.push(newItem);
  }
}
```

The `addItem()` method takes an argument in the form of a string and then adds that string to the `items` array.

### Configuring the parent's template

1. In the parent's template, bind the parent's method to the child's event.

2. Put the child selector, here `<app-item-output>`, within the parent component's template, `app.component.html`.

   src/app/app.component.html

   ```
   content_copy<app-item-output (newItemEvent)="addItem($event)"></app-item-output>
   ```

   The event binding, `(newItemEvent)='addItem($event)'`, connects the event in the child, `newItemEvent`, to the method in the parent, `addItem()`.

   The `$event` contains the data that the user types into the `<input>` in the child template UI.

   To see the `@Output()` working, you can add the following to the parent's template:

   ```html
   content_copy<ul>
     <li *ngFor="let item of items">{{item}}</li>
   </ul>
   ```

   The `*ngFor` iterates over the items in the `items` array. When you enter a value in the child's `<input>` and click the button, the child emits the event and the parent's `addItem()` method pushes the value to the `items` array and new item renders in the list.

## Using `@Input()` and `@Output()` together

You can use `@Input()` and `@Output()` on the same child component as follows:

src/app/app.component.html

```
content_copy<app-input-output [item]="currentItem" (deleteRequest)="crossOffItem($event)"></app-input-output>
```

The target, `item`, which is an `@Input()` property in the child component class, receives its value from the parent's property, `currentItem`. When you click delete, the child component raises an event, `deleteRequest`, which is the argument for the parent's `crossOffItem()` method.

The following diagram shows the different parts of the `@Input()` and `@Output()` on the `<app-input-output>`child component.

![Diagram of an input target and an output target each bound to a source.](https://angular.io/generated/images/guide/inputs-outputs/input-output-diagram.svg)

The child selector is `<app-input-output>` with `item` and `deleteRequest` being `@Input()` and `@Output()`properties in the child component class. The property `currentItem` and the method `crossOffItem()` are both in the parent component class.

To combine property and event bindings using the banana-in-a-box syntax, `[()]`, see [Two-way Binding](https://angular.io/guide/two-way-binding).

# Two way data binding

To get the most out of two-way binding, you should have a basic understanding of the following concepts:

- [Property binding](https://angular.io/guide/property-binding) : Property binding in Angular helps you **set** **values for properties of HTML elements or directives**. With property binding, you can do things such as **toggle button functionality**, **set paths programmatically**, and **share values between components**.
- [Event binding](https://angular.io/guide/event-binding) : Event binding allows you to **listen for and respond to user actions** such as keystrokes, **mouse movements**, **clicks**, and touches.
- [Inputs and Outputs](https://angular.io/guide/inputs-outputs) : Sharing data between child and parent directives and components. A common pattern in Angular is sharing data between a parent component and one or more child components. You can implement this pattern by using the `@Input()` and `@Output()` directives.

------

Two-way binding combines property binding with event binding:

- [Property binding](https://angular.io/guide/property-binding) sets a specific element property.
- [Event binding](https://angular.io/guide/event-binding) listens for an element change event.

## Adding two-way data binding

**Angular's two-way binding syntax is a combination of square brackets and parentheses, `[()]`. The `[()]` syntax combines the brackets of property binding, `[]`, with the parentheses of event binding, `()`, as follows.**

src/app/app.component.html

```
content_copy<app-sizer [(size)]="fontSizePx"></app-sizer>
```

## How two-way binding works

For two-way data binding to work, the **`@Output()` property must use the pattern, `inputChange`**, where `input` is the name of the `@Input()` property. For example, if the `@Input()` property is `size`, the `@Output()` property must be `sizeChange`.

The following `sizerComponent` has a `size` value property and a `sizeChange` event. The `size` property is an `@Input()`, so data can flow into the `sizerComponent`. The `sizeChange` event is an `@Output()`, which allows data to flow out of the `sizerComponent` to the parent component.

Next, there are two methods, `dec()` to decrease the font size and `inc()` to increase the font size. These two methods use `resize()` to change the value of the `size` property within min/max value constraints, and to emit an event that conveys the new `size` value.

src/app/sizer.component.ts

```
content_copyexport class SizerComponent {

  @Input()  size!: number | string;
  @Output() sizeChange = new EventEmitter<number>();

  dec() { this.resize(-1); }
  inc() { this.resize(+1); }

  resize(delta: number) {
    this.size = Math.min(40, Math.max(8, +this.size + delta));
    this.sizeChange.emit(this.size);
  }
}
```

The `sizerComponent` template has two buttons that each bind the click event to the `inc()` and `dec()`methods. When the user clicks one of the buttons, the `sizerComponent` calls the corresponding method. Both methods, `inc()` and `dec()`, call the `resize()` method with a `+1` or `-1`, which in turn raises the `sizeChange`event with the new size value.

src/app/sizer.component.html

```
<div>
  <button (click)="dec()" title="smaller">-</button>
  <button (click)="inc()" title="bigger">+</button>
  <label [style.font-size.px]="size">FontSize: {{size}}px</label>
</div>
```

In the `AppComponent` template, `fontSizePx` is two-way bound to the `SizerComponent`.

src/app/app.component.html

```
content_copy<app-sizer [(size)]="fontSizePx"></app-sizer>
<div [style.font-size.px]="fontSizePx">Resizable Text</div>
```

In the `AppComponent`, `fontSizePx` establishes the initial `SizerComponent.size` value by setting the value to `16`.

src/app/app.component.ts

```
content_copyfontSizePx = 16;
```

Clicking the buttons updates the `AppComponent.fontSizePx`. The revised `AppComponent.fontSizePx` value updates the style binding, which makes the displayed text bigger or smaller.

The two-way binding syntax is shorthand for a combination of property binding and event binding. The `SizerComponent` binding as separate property binding and event binding is as follows.

src/app/app.component.html (expanded)

```
content_copy<app-sizer [size]="fontSizePx" (sizeChange)="fontSizePx=$event"></app-sizer>
```

The `$event` variable contains the data of the `SizerComponent.sizeChange` event. Angular assigns the `$event`value to the `AppComponent.fontSizePx` when the user clicks the buttons.

TWO-WAY BINDING IN FORMS

Because no native HTML element follows the `x` value and `xChange` event pattern, two-way binding with form elements requires `NgModel`. For more information on how to use two-way binding in forms, see Angular [NgModel](https://angular.io/guide/built-in-directives#ngModel).

## A Word on Data Architecture

You might be wondering at this point how we would manage the data flow if we started adding more functionality to this app.

For instance, say we wanted to add a shopping cart view and then we would add items to our cart. How could we implement this?

The only tools we've talked about are emitting output events. When we click add-to-cart do we simply bubble up an `addedToCart` event and handle at the root component? That feels a bit awkward.

Data architecture is a large topic with many opinions. Thankfully, Angular is flexible enough to handle a wide variety of data architectures, but that means that you have to decide for yourself which to use.

In Angular 1, the default option was two-way data binding. Two-way data binding is super easy to get started: your controllers have data, your forms manipulate that data directly, and your views show the data.

The problem with two-way data binding is that it often causes cascading effects throughout your application and makes it really difficult to trace data flow as your project grows.

Another problem with two-way data binding is that because you're passing data down through components it often forces your "data layout tree" to match your "dom view tree". In practice, these two things should really be separate.

One way you might handle this scenario would be to create a `ShoppingCartService`, which would be a singleton that would hold the list of the current items in the cart. This service could notify any interested objects when an item in the cart changes.

The idea is easy enough, but in practice there are a lot of details to be worked out.

The recommended way in Angular, and in many modern web frameworks (such as React), is to adopt a pattern of **one-way data binding**. That is, your data flows only **down** through components. If you need to make changes, you emit events that cause changes to happen "at the top" which then trickle down.

# Sharing data between unrelated components

**User Subjects, BehaviorSubject in Rxjs**

Login Componet => data => AuthService => BehaviorSubject(observable)

​																		headerComponet

​																		Component 3

​																		Component 4	

Component can push the data to the behaviorSubject, so if the unrelated component subscribed the Subject, it will receive the data. 
