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

## Property binding and security

Property binding can help keep content secure. For example, consider the following malicious content.

src/app/app.component.ts

```
content_copyevilTitle = 'Template <script>alert("evil never sleeps")</script> Syntax';
```

The component template interpolates the content as follows:

src/app/app.component.html

```
content_copy<p><span>"{{evilTitle}}" is the <i>interpolated</i> evil title.</span></p>
```

The browser doesn't process the HTML and instead displays it raw, as follows.

```bash
content_copy"Template <script>alert("evil never sleeps")</script> Syntax" is the interpolated evil title.
```

Angular does not allow HTML with `<script>` tags, neither with [interpolation](https://angular.io/guide/interpolation) nor property binding, which prevents the JavaScript from running.

In the following example, however, Angular [sanitizes](https://angular.io/guide/security#sanitization-and-security-contexts) the values before displaying them.

src/app/app.component.html

```
content_copy<!--
 Angular generates a warning for the following line as it sanitizes them
 WARNING: sanitizing HTML stripped some content (see https://g.co/ng/security#xss).
-->
 <p>"<span [innerHTML]="evilTitle"></span>" is the <i>property bound</i> evil title.</p>
```

Interpolation handles the `<script>` tags differently than property binding, but both approaches render the content harmlessly. The following is the browser output of the sanitized `evilTitle` example.

```bash
content_copy"Template Syntax" is the property bound evil title.
```

```
content_copy<div *ngSwitchCase="'bright'"> Are you as bright as {{currentItem.name}}?</div>
```

