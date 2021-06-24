---

title: Angular References
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

@Injectable({

  providedIn: 'root'

})

# Command Lines

1. Angular CLI

The *Angular CLI* is a command-line interface tool that you use to initialize, develop, scaffold, and maintain Angular applications directly from a command shell.



# Template statements



**Template statements are methods or properties that you can use in your HTML to respond to user events.** With template statements, your application can engage users through actions such as displaying dynamic content or submitting forms.

See the [Template syntax](https://angular.io/generated/live-examples/template-syntax/stackblitz.html) / [download example](https://angular.io/generated/zips/template-syntax/template-syntax.zip) for the syntax and code snippets in this guide.

In the following example, the template statement `deleteHero()` appears in quotes to the right of the `=` symbol as in `(event)="statement"`.

src/app/app.component.html

```
content_copy<button (click)="deleteHero()">Delete hero</button>
```

When the user clicks the **Delete hero** button, Angular calls the `deleteHero()` method in the component class.

You can use template statements with elements, components, or directives in response to events.

# NgModules



**NgModules** configure the injector and the compiler and help organize related things together.

An NgModule is a class marked by the `@NgModule` decorator. `@NgModule` takes a metadata object that describes how to compile a component's template and how to create an injector at runtime. It identifies the module's own components, directives, and pipes, making some of them public, through the `exports` property, so that external components can use them. `@NgModule` can also add service providers to the application dependency injectors.

For an example application showcasing all the techniques that NgModules related pages cover, see the [live example](https://angular.io/generated/live-examples/ngmodules/stackblitz.html) / [download example](https://angular.io/generated/zips/ngmodules/ngmodules.zip). For explanations on the individual techniques, visit the relevant NgModule pages under the NgModules section.

## @angular/forms

`FormsModule` gives us *template driven* directives such as:

- `ngModel` and
- `NgForm`

Whereas `ReactiveFormsModule` gives us *reactive driven* directives like

- `formControl` and
- `ngFormGroup`

## directive

**A class that can modify the structure of the DOM or modify attributes in the DOM and component data model.** A directive class definition is immediately preceded by a `@Directive()` [decorator](https://angular.io/guide/glossary#decorator) that supplies metadata.

A directive class is usually associated with an HTML element or attribute, and that element or attribute is often referred to as the directive itself. When Angular finds a directive in an HTML [template](https://angular.io/guide/glossary#template), it creates the matching directive class instance and gives the instance control over that portion of the browser DOM.

There are three categories of directive:

- [Components](https://angular.io/guide/glossary#component) use `@Component()` (an extension of `@Directive()`) to associate a template with a class.
- [Attribute directives](https://angular.io/guide/glossary#attribute-directive) modify behavior and appearance of page elements.
- [Structural directives](https://angular.io/guide/glossary#structural-directive) modify the structure of the DOM.

## built-in directives

**Angular supplies a number of built-in directives that begin with the `ng` prefix.** 

## User-defined directives

You can also create new directives to implement your own functionality. You associate a *selector* (an HTML tag such as `<my-directive>`) with a custom directive; this extends the [template syntax](https://angular.io/guide/template-syntax) that you can use in your applications.

**UpperCamelCase**, such as `NgIf`, refers to a directive class. You can use **UpperCamelCase** when describing properties and directive behavior.

**lowerCamelCase**, such as `ngIf` refers to a directive's attribute name. You can use **lowerCamelCase** when describing how to apply the directive to an element in the HTML template.

## template

**Code that defines how to render a component's [view](https://angular.io/guide/glossary#view).**

A template combines straight HTML with Angular [data-binding](https://angular.io/guide/glossary#data-binding) syntax, [directives](https://angular.io/guide/glossary#directive), and [template expressions](https://angular.io/guide/glossary#template-expression)(logical constructs). The Angular elements insert or calculate values that modify the HTML elements before the page is displayed. Learn more about Angular template language in the [Template Syntax](https://angular.io/guide/template-syntax) guide.

A template is associated with a [component class](https://angular.io/guide/glossary#component) through the `@Component()` [decorator](https://angular.io/guide/glossary#decorator). The template code can be provided inline, as the value of the `template` property, or in a separate HTML file linked through the `templateUrl` property.

Additional templates, represented by `TemplateRef` objects, can define alternative or *embedded* views, which can be referenced from multiple components.

