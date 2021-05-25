---

title: Front-End I CSS, Bootstrap
date: 05/11/2021
updated: 05/12/2021
tags: 
  - notes
  - HTML
  - Bootstrap
  - front-End
categories: Front-End
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

# Cascading Style Sheet (CSS)

- Styles define how to display HTML elements

- Styles are normally stored in Style Sheets

- Styles were added to HTML 4.0 to solve a problem

- External style sheets can save a lot of work

- External style sheets are stored in CSS files

- Multiple style definitions will cascade into one

## Benefit

- Separates structure from presentation

- Provides advanced control of presentation

- Easy maintenance of multiple pages

- Faster page loading

- Better accessibility for disabled users

- Easy to learn

## HTML and CSS 

work together to produce beautiful and functional Web sites

HTML = structure

CSS = *style*

Bootstrap



  <p>Custom file:</p>
```html
<!-- bootstrap file upload: custom-file -->
<div class="custom-file mb-3">
  <input type="file" class="custom-file-input" id="customFile" name="filename">
  <label class="custom-file-label" for="customFile">Choose file</label>
</div>

<p>Default file:</p>
<input type="file" id="myFile" name="filename2">
```

# Z-index

The `z-index` property specifies the stack order of an element.



# Align

```html
<div class="container py-3 mt-3">
    <h5>Float</h5>
    <div class="row">
        <div class="col-6">left</div>
        <div class="col-6"><span class="float-right">right</span></div>
    </div>
    <hr>
    <h5>Responsive Floats</h5>
    <div class="row">
        <div class="col-md-6 text-center">
            <span class="float-md-left">left on md</span>
        </div>
        <div class="col-md-6 text-center">
            <span class="float-md-right">right on md</span>
        </div>
    </div>
    <hr>
    <h5>Responsive Text Align</h5>
    <div class="row">
        <div class="col-md-12 text-md-right">
            text-md-right
        </div>
        <div class="col-md-12 text-md-center">
            text-md-center
        </div>
    </div>
    <hr>
    <h5>Flexbox Align</h5>
    <div class="d-flex justify-content-between">
        <div>
            left
        </div>
        <div>
            right
        </div>
    </div>
</div>
```

