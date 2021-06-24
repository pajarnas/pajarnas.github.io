---
``
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

Security of your Application - We have used JWT (JSON Web Token) in our Project.

- First User will register in our application where we store the hashed password with Salt
- Next when user login in to the web site ,  Angular will send un/pw to the API, here API will validate un/pw and if valid it will  Yes….generate the JWT token and send it to the Client (Angular App)
-  Usually our Token is valid for 20 minutes and if the token is expired or not present in the local storage then user will be redirected to the Login Page. 
-  Next, the Angular app will store the token in local storage of the browser, when user is requesting a secure page on angular app which will communicate with Secure API on the backend then Angular will check for JWT token from local storage and see if it is valid and then if it is valid we let user go the secure page which will call secure API with Token in the header.
-  To guard against the Angular URL( i.e. secure page) we use Angular Guards, where we created Authentication Guards, Guards job is to check whether the token in local storage is Valid, if valid then let user to go that secure page
-  API will check for valid token in the header and if valid it will return the Json data to the Angular App.

最大的挑战， 全新的， 不熟悉的， 和自己的经验不一样的知识，或者技术。 超出了自己认知范围的，比较需要花更多的时间去钻研。 掌握， 并且熟练运用。

发现问题，解决问题其实不难，最大的挑战是发现不了问题。 比如某个缺陷，自己并没有注意。

代码架构的问题，不知道什么样的代码是最优架构，经常花很多时间去重构代码。代码的重构并没有一个标准。是以可读性，复用性为标准，还是性能为标准。

