---
title: Web_Development
categories:
  - Web开发
  - 前端
  - null
tags:
  - 前端
  - HTML
  - CSS
  - Web开发
  
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
arrange data into rows and columns
```HTML
<table style="width:100%">  
  <caption>Monthly savings</caption>
  <colgroup>  
    <col span="2" style="background-color: #D6EEEE">  
  </colgroup>
  <tr>  
    <th style="width:70%">Firstname</th>  
    <th>Lastname</th>  
    <th>Age</th>  
  </tr>  
  <tr style="height:200px">  
    <td>Jill</td>  
    <td>Smith</td>  
    <td>50</td>  
  </tr>  
  <tr>  
    <td>Eve</td>  
    <td>Jackson</td>  
    <td>94</td>  
  </tr>  
</table>
```

`<td>`  table cell
`<tr>` table rows
`<th>` table headers
Use the `style` attribute with the `width` or `height` properties to specify the size of a table, row or column
The `<colgroup>` element should be used as a container for the column specifications.


you can use CSS border property on `table`, `th`, and `td`
`border-collapse` avoid having double borders
`border-style` 
`padding` add padding on table cells
`border-spacing` change the space between table cell
if you use `(odd)` instead of `(even)`, the styling will occur on row 1,3,5 etc. instead of 2,4,6 etc.
```CSS
table, th(even), td(odd) {  
	border: 1px solid black;  
	border-collapse: collapse;
	background-color: rgba(150, 212, 212, 0.4);
	border-radius: 10px;
	border-style:hidden;
	border-color: #96D4D4;
	padding-top: 10px;  
    padding-bottom: 20px;  
    padding-left: 30px;  
    padding-right: 40px;
    border-spacing: 30px;
}
 
```


## Lists
- `ul` unordered list
- `ol` ordered list
- each list with the `li` tag
-   Use the CSS `list-style-type` property to define the list item marker
	- disc/cricle/square/none
- HTML lists can be styled in many different ways with CSS.

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<style>  
ul {  list-style-type: none;  
  margin: 0;  
  padding: 0;  
  overflow: hidden;  
  background-color: #333333;}  
  
li {  float: left;}  
  
li a {  display: block;  
  color: white;  
  text-align: center;  
  padding: 16px;  
  text-decoration: none;}  
  
li a:hover {  background-color: #111111;}  
</style>  
</head>  
<body>  
  
<ul>  
  <li><a href="#home">Home</a></li>  
  <li><a href="#news">News</a></li>  
  <li><a href="#contact">Contact</a></li>  
  <li><a href="#about">About</a></li>  
</ul>  
  
</body>  
</html>

```

## Block-level/Inline Elements

### A block-level element always starts on a new line, and the browsers automatically add some space (a margin) before and after the element.

The `<p>` element defines a paragraph in an HTML document.

The `<div>` element defines a division or a section in an HTML document.

### An inline element does not start on a new line.

The `<span>` element is an inline container used to mark up a part of a text, or a part of a document.

## Class/Id

### The HTML `class` attribute is used to specify a class for an HTML element.
To create a class; write a period (.) character, followed by a class name. Then, define the CSS properties within curly braces {}:

### The `id` attribute specifies a unique id for an HTML element. The value of the `id` attribute must be unique within the HTML document.

The syntax for id is: write a hash character (#), followed by an id name. Then, define the CSS properties within curly braces {}.

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<style>  

#myHeader {  background-color: lightblue;  
  color: black;  
  padding: 40px;  
  text-align: center;}
  
.city {  background-color: tomato;  
  color: white;  
  padding: 10px;} 
   
.main {
  text-align: center;}
</style>  
</head>  
<body>  

<h1 id="myHeader">My Cities</h1>
  
<h2 class="city main">London</h2>  
<p>London is the capital of England.</p>  
  
<h2 class="city">Paris</h2>  
<p>Paris is the capital of France.</p>  
  
<h2 class="city">Tokyo</h2>  
<p>Tokyo is the capital of Japan.</p>  
  
</body>  
</html>
```

## Form
### `<form>`
a containter for different types of input elements
### `<input>`

| Type     | Description |
| -------- | ----------- |
| text     | **single-line text input field**           |
| submit   | defines a button for **submitting** form data to a **form-handler**            |
| reset    | defines a **reset button** that will reset all form values to their default values           |
| radio    | defines a **radio button**            |
| checkbox | defines a **checkbox**            |
| button   | defines a **button**            |

```html
<form>  
  <label for="fname">First name:</label><br>  
  <input type="text" id="fname" name="fname"><br>  
  <label for="lname">Last name:</label><br>  
  <input type="text" id="lname" name="lname">  
</form>
```

```ad-note
** `<lable>` defines a lable for elements**
```


##
# Attributes

## style
`<_tagname_ style="_property_:_value;_">`

The _**property**_ is a CSS property. The _**value**_ is a CSS value.


# CSS
https://www.w3schools.com/cssref/css4_pr_accent-color.asp
## using CSS

CSS can be added to HTML documents in 3 ways:

-   **Inline** - by using the `style` attribute inside HTML elements
```HTML
<h1 style="color:blue;">A Blue Heading</h1>
```
-   **Internal** - by using a `<style>` element in the `<head>` section
```HTML
<!DOCTYPE html>  
<html>  
<head>  
<style>  
h1 {  color: blue;  
  font-family: verdana;  
  font-size: 300%;}  
p {  color: red;  
  font-family: courier;  
  font-size: 160%;}
</style>  
</head>  
<body>  
  
<h1>This is a heading</h1>  
<p>This is a paragraph.</p>  
  
</body>  
</html>
```
-   **External** - by using a `<link>` element to link to an external CSS file
```HTML
<!DOCTYPE html>  
<html>  
<head>  
  <link rel="stylesheet" href="styles.css">  
</head>  
<body>  
  
<h1>This is a heading</h1>  
<p>This is a paragraph.</p>  
  
</body>  
</html>

```

styles.css
```CSS
body {  background-color: powderblue;}  
h1 {  color: blue;}  
p {  color: red;}
```

## Property
- `color` property defines the text color to be used.
- `accent-color` property defines the accent color for differents user-interface controls

 - `font-family` property defines the font to be used.

-  `font-size` property defines the text size to be used.

-  `border` property defines a border around an HTML element.
-  `padding` property defines a padding (space) between the text and the border.
-  `margin` property defines a margin (space) outside the border.
```CSS
p {  
	border: 2px solid powderblue;
	padding: 30px;
	margin: 50px;
}
```



# xx2x

# xx3x

<hr />
版权信息