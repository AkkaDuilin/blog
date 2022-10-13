---
title: Web_Development
categories:
  - Web
  - 前端
  - null
tags:
  - 前端
  - HTML
  
copyright: true
date: 2022-09-20 09:15:28
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

HTML / Web开发前端笔记
https://www.w3schools.com/html/default.asp

HTML is the standard markup language for Web pages.

With HTML you can create your own Website.


<!-- more -->

# Elements

## `<html>`

The `<html>` element is the root element and it defines the whole HTML document.

It has a start tag `<html>` and an end tag `</html>`.

## `<body>`

Then, inside the `<html>` element there is a `<body>` element:

The `<body>` element defines the document's body.

It has a start tag `<body>` and an end tag `</body>`.

## `<h>`

The `<h1>` to `<h6>` lement defines a heading.
These elements decrease in size as the number increases

It has a start tag `<h1>` and an end tag `</h1>`:

## `<p>`

The `<p>` element defines a paragraph.

It has a start tag `<p>` and an end tag `</p>`:

A paragraph always starts on a new line, and browsers automatically add some white space (a margin) before and after a paragraph.

## Links

### `<a>`
The HTML `<a>` tag defines a hyperlink.
`<a href="_url_">_link text_</a>`


The `target` attribute specifies where to open the linked document.

The `target` attribute can have one of the following values:

-   `_self` - Default. Opens the document in the same window/tab as it was clicked
-   `_blank` - Opens the document in a new window or tab
-   `_parent` - Opens the document in the parent frame
-   `_top` - Opens the document in the full body of the window

### others
Use Image / Botton as a link

``` HTML

<a href="default.asp">  
<img src="smiley.gif" alt="HTML tutorial" style="width:42px;height:42px;">  
</a>

<button onclick="document.location='default.asp'">HTML Tutorial</button>
```

Link to an Email Address
`<a href="mailto:someone@example.com">Send email</a>`

### bookmark

First, use the `id` attribute to create a bookmark:
Then, add a link to the bookmark ("Jump to Chapter 4"), from within the same page:
You can also add a link to a bookmark on another page:
``` HTML
<h2 id="C4">Chapter 4</h2>


<a href="#C4">Jump to Chapter 4</a>
<a href="html_demo.html#C4">Jump to Chapter 4</a>

```

## Images

### `<img>`

The `<img>` tag has some required attributes:

-   src - Specifies the path to the image
-   alt - Specifies an alternate text for the image

-   Use the HTML `width` and `height` attributes or the CSS `width` and `height` properties to define the size of the image
-   Use the CSS `float` property to let the image float to the left or to the right

```HTML
<img src="html5.gif" alt="HTML5 Icon" width="128" height="128">  
  
<img src="html5.gif" alt="HTML5 Icon" style="width:128px;height:128px;">
```

### `<map>`
https://www.w3schools.com/html/html_images_imagemap.asp 

```HTML
<img src="workplace.jpg" alt="Workplace" usemap="#workmap">  
  
<map name="workmap">  
  <area shape="rect" coords="34,44,270,350" alt="Computer" href="computer.htm">  
  <area shape="rect" coords="290,172,333,250" alt="Phone" href="phone.htm">  
  <area shape="circle" coords="337,300,44" alt="Coffee" href="coffee.htm">  
</map>
```

Shape
-   `rect` - defines a rectangular region
-   `circle` - defines a circular region
-   `poly` - defines a polygonal region
-   `default` - defines the entire region

### `<picture>`

The `<picture>` element contains one or more `<source>` elements, each referring to different images through the `srcset` attribute. This way the browser can choose the image that best fits the current view and/or device.

Each `<source>` element has a `media` attribute that defines when the image is the most suitable.

```HTML
<picture>  
  <source media="(min-width: 650px)" srcset="img_food.jpg">  
  <source media="(min-width: 465px)" srcset="img_car.jpg">  
  <img src="img_girl.jpg">  
</picture>
```


## Formatting Elements

-   `<b>` - Bold text
-   `<strong>` - Important text
-   `<i>` - Italic text
-   `<em>` - Emphasized text
-   `<mark>` - Marked text
-   `<small>` - Smaller text
-   `<del>` - Deleted text
-   `<ins>` - Inserted text
-   `<sub>` - Subscript text
-   `<sup>` - Superscript text

## Quotation and Citation
 - `<blockquote>` - Quotation
- `<q>`  -  short quotation
- `<abbr>`  - Abbreviations
- `<address>` - Contact Information
-  `<cite>` for Work Title

## Comments

`<!-- Write your comments here -->`


 
## Tables
## Lists


# Attributes

## style
`<_tagname_ style="_property_:_value;_">`

The _**property**_ is a CSS property. The _**value**_ is a CSS value.


# CSS


# xx2x

# xx3x

<hr />
版权信息