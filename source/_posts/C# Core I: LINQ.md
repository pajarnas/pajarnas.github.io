---

title: C# Core LINQ
date: 06/15/2021
updated: 
tags: 
  - notes
  - LINQ
  - Expression Tree
  - Collections
categories: C# Core
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

# Collections

## Standard Collections

## LINQ Collections

IQueryable

The [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable?view=net-5.0) interface is intended for implementation by query providers. It is only supposed to be implemented by providers that also implement [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1?view=net-5.0). If the provider does not also implement [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1?view=net-5.0), the standard query operators cannot be used on the provider's data source.

The [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable?view=net-5.0) interface inherits the [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable?view=net-5.0) interface so that if it represents a query, the results of that query can be enumerated. Enumeration causes the expression tree associated with an [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable?view=net-5.0) object to be executed. The definition of "executing an expression tree" is specific to a query provider. For example, it may involve translating the expression tree to an appropriate query language for the underlying data source. Queries that do not return enumerable results are executed when the [Execute](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryprovider.execute?view=net-5.0) method is called.

# **EXPRESSION TREES**

With LINQ to Objects, **the extension methods require a delegate type as parameter;** <u>this way, a lambda expression can be assigned to the parameter.</u> **Lambda expressions can also be assigned to parameters of type Expression\<T\>**. <u>The C# compiler defines different behavior for lambda expressions depending on the type. If the type is Expression\<T\>, the compiler creates an expression tree from the lambda expression and stores it in the assembly. The expression tree can be analyzed during runtime and optimized for querying against the data source.</u>

1. Example of query expression:

Let's turn to a **query expression** that was used previously:

```
   var brazilRacers = from r in racers
                      where r.Country == "Brazil"
                      orderby r.Wins
                      select r;
```

2. **lambda expression is like an anonymous method**

Extension methods Where, OrderBy, and Select to preceding QE

- Enumberable:

The Enumerable class defines the Where extension method with the delegate type Func<T, bool> as parameter predicate:

```c#
   public static IEnumerable<TSource> Where<TSource>(
     this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

This way, the **lambda expression is assigned to the predicate**. Here, **the lambda expression is like an anonymous method, as explained earlier:**

```
   Func<Racer, bool> predicate = r => r.Country == "Brazil";
```

- Queryable

```c#
   public static IQueryable<TSource> Where<TSource>(
     this IQueryable<TSource> source,
     Expression<Func<TSource, bool>> predicate);
```

3. **lambda expression is assigned to the type Expression\<T\>**

Expression Tree 

Here, the lambda expression is assigned to the type Expression\<T\>, which behaves differently:

```
   Expression<Func<Racer, bool>> predicate = r => r.Country == "Brazil";
```

The compiler emits an expression tree to the assembly Instead of using delegates. 

The expression tree can be read during runtime. 

Expression trees are built from classes derived from the abstract base class Expression. 

The Expression class is not the same as Expression\<T\>. 

Some of the expression classes that inherit from Expression: 

- BinaryExpression, 
- ConstantExpression, 
- InvocationExpression, 
- LambdaExpression, 
- NewExpression, 
- NewArrayExpression, 
- TernaryExpression, 
- UnaryExpression. 

The compiler creates an expression tree resulting from the lambda expression.

For example, the lambda expression ```r.Country == "Brazil"``` makes use of *ParameterExpression*, *MemberExpression*, *ConstantExpression*, and *MethodCallExpression* to **create** a **tree** and **store** the **tree** in the **assembly**. This tree is then used during **runtime** to create an **optimized query** to the underlying **data source**.

With the sample application, the method DisplayTree is implemented to display an expression tree graphically on the console. In the following example, an Expression object can be passed, and depending on the expression type some information about the expression is written to the console. Depending on the type of the expression, DisplayTree is called recursively (code file ExpressionTreeSample/Program.cs):

``` c#
   static void DisplayTree(int indent, string message,
     Expression expression)
   {
     string output = $"{string.Empty.PadLeft(indent, '>')}
   {message} " +
       $"! NodeType: {expression.NodeType}; Expr: {expression}";
       indent++;

     switch (expression.NodeType)
     {
       case ExpressionType.Lambda:
         Console.WriteLine(output);
         LambdaExpression lambdaExpr =
   (LambdaExpression)expression;
         foreach (var parameter in lambdaExpr.Parameters)
         {
           DisplayTree(indent, "Parameter", parameter);
         }
         DisplayTree(indent, "Body", lambdaExpr.Body);
         break;
       case ExpressionType.Constant:
         ConstantExpression constExpr =
  (ConstantExpression)expression;
        Console.WriteLine($"{output} Const Value:
  {constExpr.Value}");
        break;
      case ExpressionType.Parameter:
        ParameterExpression paramExpr =
  (ParameterExpression)expression;
        Console.WriteLine($"{output} Param Type:
  {paramExpr.Type.Name}");
        break;
      case ExpressionType.Equal:
      case ExpressionType.AndAlso:
      case ExpressionType.GreaterThan:
        BinaryExpression binExpr =
  (BinaryExpression)expression;
        if (binExpr.Method != null)
        {
          Console.WriteLine($"{output} Method:
  {binExpr.Method.Name}");


} else {


          Console.WriteLine(output);
        }
        DisplayTree(indent, "Left", binExpr.Left);
        DisplayTree(indent, "Right", binExpr.Right);
        break;
      case ExpressionType.MemberAccess:
        MemberExpression memberExpr =
  (MemberExpression)expression;
        Console.WriteLine($"{output} Member Name:
  {memberExpr.Member.Name}, " +
          " Type: {memberExpr.Expression}");
        DisplayTree(indent, "Member Expr",
  memberExpr.Expression);
        break;
      default:
        Console.WriteLine();
        Console.WriteLine($"{expression.NodeType}
  {expression.Type.Name}");


break; }

}
```

**NOTE**

*The method* DisplayTree *does not deal with all expression types— only the types that are used with the following example expression.*

The expression that is used for showing the tree is already well known. It’s a lambda expression with a Racer parameter, and the body of the expression takes racers from Brazil only if they have won more than six races:

```
   Expression<Func<Racer, bool>> expression =
     r => r.Country == "Brazil" && r.Wins > 6;
```

Looking at the tree result, you can see from the output that the lambda expression consists of a Parameter and an AndAlso node type. The AndAlso node type has an Equal node type to the left and a GreaterThan node type to the right. The Equal node type to the left of the AndAlso node type has a MemberAccess node type to the left and a Constant node type to the right, and so on:

```
   Lambda! NodeType: Lambda; Expr: r => ((r.Country == "Brazil")
   AndAlso (r.Wins > 6))
   > Parameter! NodeType: Parameter; Expr: r Param Type: Racer
   > Body! NodeType: AndAlso; Expr: ((r.Country == "Brazil")
   AndAlso (r.Wins > 6))
   >> Left! NodeType: Equal; Expr: (r.Country == "Brazil")
   Method: op_Equality
   >>> Left! NodeType: MemberAccess; Expr: r.Country Member
   Name: Country, Type: String
   >>>> Member Expr! NodeType: Parameter; Expr: r Param Type:
   Racer
   >>> Right! NodeType: Constant; Expr: "Brazil" Const Value:
   Brazil
   >> Right! NodeType: GreaterThan; Expr: (r.Wins > 6)
   >>> Left! NodeType: MemberAccess; Expr: r.Wins Member Name:
   Wins, Type: Int32
   >>>> Member Expr! NodeType: Parameter; Expr: r Param Type:
   Racer
   >>> Right! NodeType: Constant; Expr: 6 Const Value: 6
```

Examples where the Expression<T> type is used are with the Entity Framework Core and the client provider for WCF Data Services. These technologies define methods with Expression<T> parameters. This way the LINQ provider accessing the database can create a runtime- optimized query by reading the expressions to get the data from the database.

# Client-side Javascript

Client-side JavaScript is the most common form of the language. The script should be included in or referenced by an HTML document for the code to be interpreted by the browser.

It means that a web page need **not be a static HTML**, but can include programs that **interact with the user,** **control the browser,** and **dynamically create HTML content**.

The JavaScript client-side mechanism provides **many advantages over traditional CGI server-side scripts**. For example, you might use JavaScript to check if the user has entered a valid e-mail address in a form field.

The JavaScript code is executed when the user submits the form, and only if all the entries are valid, they would be submitted to the Web Server.

JavaScript can be used to **trap user-initiated events** such as button clicks, link navigation, and other actions that the user initiates explicitly or implicitly.



# Benefits

The merits of using JavaScript are −

**Less server interaction** − We can validate user input before sending the page off to the server. This saves server traffic, which means less load on your server.

**Immediate feedback to the visitors** − They don't have to wait for a page reload to see if they have forgotten to enter something.

**Increased interactivity** − We can create interfaces that react when the user hovers over them with a mouse or activates them via the keyboard.

**Richer interfaces** − We can use JavaScript to include such items as drag-and-drop components and sliders to give a Rich Interface to your site visitors.

# Limitation

We cannot treat JavaScript as a full-fledged programming language. It lacks the following important features −

- Client-side JavaScript does not allow the reading or writing of files. This has been kept for security reason.

- JavaScript cannot be used for networking applications because there is no such support available.

- JavaScript doesn't have any multithreading or multiprocessor capabilities.

# Syntax

JavaScript can be implemented using JavaScript statements that are placed within the **<script>... </script>** HTML tags in a web page.

You can place the **<script>** tags, containing your JavaScript, anywhere within your web page, but it is normally recommended that you should keep it within the **<head>** tags.

The <script> tag alerts the browser program to start interpreting all the text between these tags as a script. A simple syntax of your JavaScript will appear as follows.



# Event



# Javascript Standard built-in objects

## Global Objects

1. [parseFloat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)



## String

1. [String.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)
2. [String.prototype.split()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)

## JSON

JSON objects are surrounded by curly braces {}.

JSON objects are written in key/value pairs.

Keys must be strings, and values must be a valid JSON data type (string, number, object, array, boolean or null).

Keys and values are separated by a colon.

Each key/value pair is separated by a comma.

## RegExp

   ```
   const re = /[a-zA-Z0-9.]*@[a-zA-Z0-9]*\.[a-zA-Z0-9]*/is
   
   console.log(re.test("adad2123.213.132ads@gmailco.m"));
   ```

## Expressions and operators

1. [Remainder (%)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder)

   ```javascript
   console.log(12 % 5);
   // expected output: 2
   
   console.log(-12 % 5);
   // expected output: -2
   
   console.log(4 % 2);
   // expected output: 0
   
   console.log(-4 % 2);
   // expected output: -0
   ```

   

## Object

1. Object to an array

   1. Object.entries()
   2. Object.keys()
   3. Object.values()

2. Objecy copy

   ```javascript
      const person = {
          firstName: 'John',
          lastName: 'Doe'
      };
      
      
      // using spread ...
      let p1 = {
          ...person
      };
      
      // using  Object.assign() method
      let p2 = Object.assign({}, person);
      
      // using JSON
      let p3 = JSON.parse(JSON.stringify(person));
   ```




# Javascript Statements and Declaration

1. [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

 ```
   const object = { 2: 'wa', b: 2, c: 3 };
   
   for (const property in object) {
     console.log(`${property}: ${object[property]}`);
   }
   
   // "2: wa"
   // "b: 2"
   // "c: 3"
   
 ```

2. let vs [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) vs var

 ```javascript
   /* Constants are block-scoped, much like variables declared using the let keyword. The value of a constant can't be changed through reassignment, and it can't be redeclared.*/
    const number = 42;
 
 try {
   number = 99;
 } catch (err) {
   console.log(err);
   // expected output: TypeError: invalid assignment to const `number'
   // Note - error messages will vary depending on browser
 }
 
 console.log(number);
 // expected output: 42
 
 //The var statement declares a function-scoped or globally-scoped variable, optionally initializing it to a value.
 
 var x = 1;
 
 if (x === 1) {
   var x = 2;
 
   console.log(x);
   // expected output: 2
 }
 
 console.log(x);
 // expected output: 2
 
 //The let statement declares a block-scoped local variable, optionally initializing it to a value.
 
 let x = 1;
 
 if (x === 1) {
   let x = 2;
 
   console.log(x);
   // expected output: 2
 }
 
 console.log(x);
 // expected output: 1
 
 ```

3. [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
4. [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

**JS is not strong type**



Local scope : use let keyword to create a variable(ES 6), a local scope variable can be accessed online inside its scope. it means only inside the {} brackets where the variable is created



Functional scope: use var keyword to create a variable. it can be created and accessed anywhere inside a function 

press table twice auto generate for loop 



Global scope





Js 

a=10

b="10"

a == b True

a === b False

1==true true

'' == null false

On the console

\> 10 + 20 

\< 30



DOM 

Document Object Model

# \`  diff  "

```javascript
console.log(`The students is ${students}`)

Array Three constructor

array

let a=new Array(5) // the size will be adjusted if you push one more element to the array

let b = new Array("IT","HR")

let c = ["MS","FB","TW",""]

let d = [];

d.push("China"); //add an element at the end of an array
d.unshift("Antra")// add an element at the start of an array
// pop remove the element at the end
// shift remove the element at the front
```

# callback

pass a function to another function as a parameter

=> arrow operator 

// callback hell

//promises

```javascript
let p = new Promise(function (resolve, reject) {
    
    resolve("This promise is resolved");
    //reject("Some error has occured");

});
p.then(function (data) {
    console.log(data);
}).catch(function (e) {
    console.log(e);
})


```

Javascript.info for javascript learning

https://javascript.info/async
promise vs Observable

Modules

Export/Import

