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
copyright_author_href: 
copyright_url: 
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# Built-in directives



**Directives are classes that add additional behavior to elements in your Angular applications. With Angular's built-in directives, you can manage forms, lists, styles, and what users see.**

The different types of Angular directives are as follows:

1. [Components](https://angular.io/guide/component-overview)—directives with a template. This type of directive is the most common directive type.
2. [Attribute directives](https://angular.io/guide/built-in-directives#built-in-attribute-directives)—directives that change the appearance or behavior of an element, component, or another directive.
3. [Structural directives](https://angular.io/guide/built-in-directives#built-in-structural-directives)—directives that change the DOM layout by adding and removing DOM elements.

This guide covers built-in [attribute directives](https://angular.io/guide/built-in-directives#built-in-attribute-directives) and [structural directives](https://angular.io/guide/built-in-directives#built-in-structural-directives).



## Built-in attribute directives

**Attribute directives listen to and modify the behavior of other HTML elements, attributes, properties, and components.**

Many NgModules such as the [`RouterModule`](https://angular.io/guide/router) and the [`FormsModule`](https://angular.io/guide/forms) define their own attribute directives. The most common attribute directives are as follows:

- [`NgClass`](https://angular.io/guide/built-in-directives#ngClass)—adds and removes a set of CSS classes.
- [`NgStyle`](https://angular.io/guide/built-in-directives#ngstyle)—adds and removes a set of HTML styles.
- [`NgModel`](https://angular.io/guide/built-in-directives#ngModel)—adds two-way data binding to an HTML form element.

Built-in directives use only public APIs. They do not have special access to any private APIs that other directives can't access.



## Adding and removing classes with `NgClass`

You can add or remove multiple CSS classes simultaneously with `ngClass`.

To add or remove a *single* class, use [class binding](https://angular.io/guide/attribute-binding#class-binding) rather than `NgClass`.

### Using `NgClass` with an expression

On the element you'd like to style, add `[ngClass]` and set it equal to an expression. In this case, `isSpecial` is a boolean set to `true` in `app.component.ts`. Because `isSpecial` is true, `ngClass` applies the class of `special` to the `<div>`.

src/app/app.component.html

```html
content_copy<!-- toggle the "special" class on/off with a property -->
<div [ngClass]="isSpecial ? 'special' : ''">This div is special</div>
```

### Using `NgClass` with a method

1. To use `NgClass` with a method, add the method to the component class. In the following example, `setCurrentClasses()` sets the property `currentClasses` with an object that adds or removes three classes based on the `true` or `false` state of three other component properties.

   Each key of the object is a CSS class name. If a key is `true`, `ngClass` adds the class. If a key is `false`, `ngClass` removes the class.

   src/app/app.component.ts

   ```
   content_copycurrentClasses: Record<string, boolean> = {};
   /* . . . */
     setCurrentClasses() {
       // CSS classes: added/removed per current state of component properties
       this.currentClasses =  {
         saveable: this.canSave,
         modified: !this.isUnchanged,
         special:  this.isSpecial
       };
     }
   ```

2. In the template, add the `ngClass` property binding to `currentClasses` to set the element's classes:

   src/app/app.component.html

   ```
   content_copy<div [ngClass]="currentClasses">This div is initially saveable, unchanged, and special.</div>
   ```

For this use case, Angular applies the classes on initialization and in case of changes. The full example calls `setCurrentClasses()` initially with `ngOnInit()` and when the dependent properties change through a button click. These steps are not necessary to implement `ngClass`. For more information, see the [live example](https://angular.io/generated/live-examples/built-in-directives/stackblitz.html) / [download example](https://angular.io/generated/zips/built-in-directives/built-in-directives.zip) `app.component.ts` and `app.component.html`.



## Setting inline styles with `NgStyle`

You can use `NgStyle` to set multiple inline styles simultaneously, based on the state of the component.

1. To use `NgStyle`, add a method to the component class.

   In the following example, `setCurrentStyles()` sets the property `currentStyles` with an object that defines three styles, based on the state of three other component properties.

   src/app/app.component.ts

   ```
   content_copycurrentStyles: Record<string, string> = {};
   /* . . . */
     setCurrentStyles() {
       // CSS styles: set per current state of component properties
       this.currentStyles = {
         'font-style':  this.canSave      ? 'italic' : 'normal',
         'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
         'font-size':   this.isSpecial    ? '24px'   : '12px'
       };
     }
   ```

2. To set the element's styles, add an `ngStyle` property binding to `currentStyles`.

   src/app/app.component.html

   ```
   content_copy<div [ngStyle]="currentStyles">
     This div is initially italic, normal weight, and extra large (24px).
   </div>
   ```

For this use case, Angular applies the styles upon initialization and in case of changes. To do this, the full example calls `setCurrentStyles()` initially with `ngOnInit()` and when the dependent properties change through a button click. However, these steps are not necessary to implement `ngStyle` on its own. See the [live example](https://angular.io/generated/live-examples/built-in-directives/stackblitz.html) / [download example](https://angular.io/generated/zips/built-in-directives/built-in-directives.zip) `app.component.ts` and `app.component.html` for this optional implementation.



## Displaying and updating properties with `ngModel`

You can use the `NgModel` directive to display a data property and update that property when the user makes changes.

1. Import `FormsModule` and add it to the NgModule's `imports` list.

   src/app/app.module.ts (FormsModule import)

   ```
   content_copyimport { FormsModule } from '@angular/forms'; // <--- JavaScript import from Angular
   /* . . . */
   @NgModule({
   /* . . . */
   
     imports: [
       BrowserModule,
       FormsModule // <--- import into the NgModule
     ],
   /* . . . */
   })
   export class AppModule { }
   ```

2. Add an `[(ngModel)]` binding on an HTML `<form>` element and set it equal to the property, here `name`.

   src/app/app.component.html (NgModel example)

   ```
   content_copy<label for="example-ngModel">[(ngModel)]:</label>
   <input [(ngModel)]="currentItem.name" id="example-ngModel">
   ```

   This `[(ngModel)]` syntax can only set a data-bound property.

To customize your configuration, you can write the expanded form, which separates the property and event binding. Use [property binding](https://angular.io/guide/property-binding) to set the property and [event binding](https://angular.io/guide/event-binding) to respond to changes. The following example changes the `<input>` value to uppercase:

src/app/app.component.html

```
content_copy<input [ngModel]="currentItem.name" (ngModelChange)="setUppercaseName($event)" id="example-uppercase">
```

Here are all variations in action, including the uppercase version:

![NgModel variations](https://angular.io/generated/images/guide/built-in-directives/ng-model-anim.gif)

### `NgModel` and value accessors

The `NgModel` directive works for an element supported by a [ControlValueAccessor](https://angular.io/api/forms/ControlValueAccessor). Angular provides *value accessors* for all of the basic HTML form elements. For more information, see [Forms](https://angular.io/guide/forms).

To apply `[(ngModel)]` to a non-form native element or a third-party custom component, you have to write a value accessor. For more information, see the API documentation on [DefaultValueAccessor](https://angular.io/api/forms/DefaultValueAccessor).

When you write an Angular component, you don't need a value accessor or `NgModel` if you name the value and event properties according to Angular's [two-way binding syntax](https://angular.io/guide/two-way-binding#how-two-way-binding-works).



## Built-in structural directives

Structural directives are responsible for HTML layout. They shape or reshape the DOM's structure, typically by adding, removing, and manipulating the host elements to which they are attached.

This section introduces the most common built-in structural directives:

- [`NgIf`](https://angular.io/guide/built-in-directives#ngIf)—conditionally creates or disposes of subviews from the template.
- [`NgFor`](https://angular.io/guide/built-in-directives#ngFor)—repeat a node for each item in a list.
- [`NgSwitch`](https://angular.io/guide/built-in-directives#ngSwitch)—a set of directives that switch among alternative views.

For more information, see [Structural Directives](https://angular.io/guide/structural-directives).



## Adding or removing an element with `NgIf`

You can add or remove an element by applying an `NgIf` directive to a host element.

When `NgIf` is `false`, Angular removes an element and its descendants from the DOM. Angular then disposes of their components, which frees up memory and resources.

To add or remove an element, bind `*ngIf` to a condition expression such as `isActive` in the following example.

src/app/app.component.html

```
content_copy<app-item-detail *ngIf="isActive" [item]="item"></app-item-detail>
```

When the `isActive` expression returns a truthy value, `NgIf` adds the `ItemDetailComponent` to the DOM. When the expression is falsy, `NgIf` removes the `ItemDetailComponent` from the DOM and disposes of the component and all of its sub-components.

For more information on `NgIf` and `NgIfElse`, see the [NgIf API documentation](https://angular.io/api/common/NgIf).

### Guarding against `null`

By default, `NgIf` prevents display of an element bound to a null value.

To use `NgIf` to guard a `<div>`, add `*ngIf="yourProperty"` to the `<div>`. In the following example, the `currentCustomer` name appears because there is a `currentCustomer`.

src/app/app.component.html

```
content_copy<div *ngIf="currentCustomer">Hello, {{currentCustomer.name}}</div>
```

However, if the property is `null`, Angular does not display the `<div>`. In this example, Angular does not display the `nullCustomer` because it is `null`.

src/app/app.component.html

```
content_copy<div *ngIf="nullCustomer">Hello, <span>{{nullCustomer}}</span></div>
```



## Listing items with `NgFor`

You can use the `NgFor` directive to present a list of items.

1. Define a block of HTML that determines how Angular renders a single item.
2. To list your items, assign the short hand `let item of items` to `*ngFor`.

src/app/app.component.html

```
content_copy<div *ngFor="let item of items">{{item.name}}</div>
```

The string `"let item of items"` instructs Angular to do the following:

- Store each item in the `items` array in the local `item` looping variable
- Make each item available to the templated HTML for each iteration
- Translate `"let item of items"` into an `<ng-template>` around the host element
- Repeat the `<ng-template>` for each `item` in the list

For more information see the [Structural directive shorthand](https://angular.io/guide/structural-directives#shorthand) section of [Structural directives](https://angular.io/guide/structural-directives).

### Repeating a component view

To repeat a component element, apply `*ngFor` to the selector. In the following example, the selector is `<app-item-detail>`.

src/app/app.component.html

```
content_copy<app-item-detail *ngFor="let item of items" [item]="item"></app-item-detail>
```

You can reference a template input variable, such as `item`, in the following locations:

- within the `ngFor` host element
- within the host element descendants to access the item's properties

The following example references `item` first in an interpolation and then passes in a binding to the `item`property of the `<app-item-detail>` component.

src/app/app.component.html

```
content_copy<div *ngFor="let item of items">{{item.name}}</div>
<!-- . . . -->
  <app-item-detail *ngFor="let item of items" [item]="item"></app-item-detail>
```

For more information about template input variables, see [Structural directive shorthand](https://angular.io/guide/structural-directives#shorthand).

### Getting the `index` of `*ngFor`

You can get the `index` of `*ngFor` in a template input variable and use it in the template.

In the `*ngFor`, add a semicolon and `let i=index` to the short hand. The following example gets the `index` in a variable named `i` and displays it with the item name.

src/app/app.component.html

```
content_copy<div *ngFor="let item of items; let i=index">{{i + 1}} - {{item.name}}</div>
```

The index property of the `NgFor` directive context returns the zero-based index of the item in each iteration.

Angular translates this instruction into an `<ng-template>` around the host element, then uses this template repeatedly to create a new set of elements and bindings for each `item` in the list. For more information about shorthand, see the [Structural Directives](https://angular.io/guide/structural-directives#shorthand) guide.



## Repeating elements when a condition is true

To repeat a block of HTML when a particular condition is true, put the `*ngIf` on a container element that wraps an `*ngFor` element. One or both elements can be an `<ng-container>` so you don't have to introduce extra levels of HTML.

Because structural directives add and remove nodes from the DOM, apply only one structural directive per element.

For more information about `NgFor` see the [NgForOf API reference](https://angular.io/api/common/NgForOf).



### Tracking items with `*ngFor` `trackBy`

By tracking changes to an item list, you can reduce the number of calls your application makes to the server. With the `*ngFor` `trackBy` property, Angular can change and re-render only those items that have changed, rather than reloading the entire list of items.

1. Add a method to the component that returns the value `NgFor` should track. In this example, the value to track is the item's `id`. If the browser has already rendered `id`, Angular keeps track of it and doesn't re-query the server for the same `id`.

   src/app/app.component.ts

   ```
   content_copytrackByItems(index: number, item: Item): number { return item.id; }
   ```

2. In the short hand expression, set `trackBy` to the `trackByItems()` method.

   src/app/app.component.html

   ```
   content_copy<div *ngFor="let item of items; trackBy: trackByItems">
     ({{item.id}}) {{item.name}}
   </div>
   ```

**Change ids** creates new items with new `item.id`s. In the following illustration of the `trackBy` effect, **Reset items** creates new items with the same `item.id`s.

- With no `trackBy`, both buttons trigger complete DOM element replacement.
- With `trackBy`, only changing the `id` triggers element replacement.

![Animation of trackBy](https://angular.io/generated/images/guide/built-in-directives/ngfor-trackby.gif)



## Hosting a directive without a DOM element

The Angular `<ng-container>` is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM.

You can use `<ng-container>` when there's no single element to host the directive.

Here's a conditional paragraph using `<ng-container>`.

src/app/app.component.html (ngif-ngcontainer)

```
content_copy<p>
  I turned the corner
  <ng-container *ngIf="hero">
    and saw {{hero.name}}. I waved
  </ng-container>
  and continued on my way.
</p>
```

![ngcontainer paragraph with proper style](https://angular.io/generated/images/guide/structural-directives/good-paragraph.png)

1. Import the `ngModel` directive from `FormsModule`.

2. Add `FormsModule` to the imports section of the relevant Angular module.

3. To conditionally exclude an `<option>`, wrap the `<option>` in an `<ng-container>`.

   src/app/app.component.html (select-ngcontainer)

   ```
   content_copy<div>
     Pick your favorite hero
     (<label><input type="checkbox" checked (change)="showSad = !showSad">show sad</label>)
   </div>
   <select [(ngModel)]="hero">
     <ng-container *ngFor="let h of heroes">
       <ng-container *ngIf="showSad || h.emotion !== 'sad'">
         <option [ngValue]="h">{{h.name}} ({{h.emotion}})</option>
       </ng-container>
     </ng-container>
   </select>
   ```

   ![ngcontainer options work properly](https://angular.io/generated/images/guide/structural-directives/select-ngcontainer-anim.gif)



## Switching cases with `NgSwitch`

Like the JavaScript `switch` statement, `NgSwitch` displays one element from among several possible elements, based on a switch condition. Angular puts only the selected element into the DOM.

`NgSwitch` is a set of three directives:

- `NgSwitch`—an attribute directive that changes the behavior of its companion directives.
- `NgSwitchCase`—structural directive that adds its element to the DOM when its bound value equals the switch value and removes its bound value when it doesn't equal the switch value.
- `NgSwitchDefault`—structural directive that adds its element to the DOM when there is no selected `NgSwitchCase`.

1. On an element, such as a `<div>`, add `[ngSwitch]` bound to an expression that returns the switch value, such as `feature`. Though the `feature` value in this example is a string, the switch value can be of any type.

2. Bind to `*ngSwitchCase` and `*ngSwitchDefault` on the elements for the cases.

   src/app/app.component.html

   ```
   content_copy<div [ngSwitch]="currentItem.feature">
     <app-stout-item    *ngSwitchCase="'stout'"    [item]="currentItem"></app-stout-item>
     <app-device-item   *ngSwitchCase="'slim'"     [item]="currentItem"></app-device-item>
     <app-lost-item     *ngSwitchCase="'vintage'"  [item]="currentItem"></app-lost-item>
     <app-best-item     *ngSwitchCase="'bright'"   [item]="currentItem"></app-best-item>
   <!-- . . . -->
     <app-unknown-item  *ngSwitchDefault           [item]="currentItem"></app-unknown-item>
   </div>
   ```

3. In the parent component, define `currentItem` so you can use it in the `[ngSwitch]` expression.

   src/app/app.component.ts

   ```
   content_copycurrentItem!: Item;
   ```

4. In each child component, add an `item` [input property](https://angular.io/guide/inputs-outputs#input) which is bound to the `currentItem` of the parent component. The following two snippets show the parent component and one of the child components. The other child components are identical to `StoutItemComponent`.

   In each child component, here StoutItemComponent

   ```
   content_copyexport class StoutItemComponent {
     @Input() item!: Item;
   }
   ```

   ![Animation of NgSwitch](https://angular.io/generated/images/guide/built-in-directives/ngswitch.gif)

Switch directives also work with native HTML elements and web components. For example, you could replace the `<app-best-item>` switch case with a `<div>` as follows.

src/app/app.component.html

```
content_copy<div *ngSwitchCase="'bright'"> Are you as bright as {{currentItem.name}}?</div>
```
