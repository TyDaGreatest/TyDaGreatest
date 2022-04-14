# Variables

Think of variables as a way to store information that you want to reuse throughout your stylesheet. You can store things like colors, font stacks, or any CSS value you think you'll want to reuse. Sass uses the $ symbol to make something a variable. Here's an example:

## SASS Example

$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
font: 100% $font-stack;
color: $primary-color;
}

## CSS Example

body {
font: 100% Helvetica, sans-serif;
color: #333;
}

---

# Nesting

Sass will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. Be aware that overly nested rules will result in over-qualified CSS that could prove hard to maintain and is generally considered bad practice.

## SASS Example

nav {
ul {
margin: 0;
padding: 0;
list-style: none;
}

li { display: inline-block;
}

a {
display: block;
padding: 6px 12px;
text-decoration: none;
}
}

## CSS Example

nav ul {
margin: 0;
padding: 0;
list-style: none;
}

nav li {
display: inline-block;
}

nav a {
display: block;
padding: 6px 12px;
text-decoration: none;
}

---

# Modules

You don't have to write all your Sass in a single file. You can split it up however you want with the @use rule. This rule loads another Sass file as a module, which means you can refer to its variables, mixins, and functions in your Sass file with a namespace based on the filename. Using a file will also include the CSS it generates in your compiled output!

## SASS Example

'\' is not included with the code only include // and understore. =)

//\_base.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
font: 100% $font-stack;
color: $primary-color;
}

// styles.scss
@use 'base';

.inverse {
background-color: base.$primary-color;
color: white;
}

---

# Mixins

Some things in CSS are a bit tedious to write, especially with CSS3 and the many vendor prefixes that exist. A mixin lets you make groups of CSS declarations that you want to reuse throughout your site. It helps keep your Sass very DRY.

## SASS Example

@mixin theme($theme: DarkGray) {
  background: $theme;
  box-shadow: 0 0 1px rgba($theme, .25);
color: #fff;
}

.info {
@include theme;
}
.alert {
@include theme($theme: DarkRed);
}
.success {
  @include theme($theme: DarkGreen);
}

## CSS Example

.info {
background: DarkGray;
box-shadow: 0 0 1px rgba(169, 169, 169, 0.25);
color: #fff;
}

.alert {
background: DarkRed;
box-shadow: 0 0 1px rgba(139, 0, 0, 0.25);
color: #fff;
}

.success {
background: DarkGreen;
box-shadow: 0 0 1px rgba(0, 100, 0, 0.25);
color: #fff;

---

# Extend/Inheritance

Using @extend lets you share a set of CSS properties from one selector to another. In our example we're going to create a simple series of messaging for errors, warnings and successes using another feature which goes hand in hand with extend, placeholder classes. A placeholder class is a special type of class that only prints when it is extended, and can help keep your compiled CSS neat and clean.

/_ This CSS will print because %message-shared is extended. _/ ----> This line is a comment!

## SASS Example

%message-shared {
border: 1px solid #ccc;
padding: 10px;
color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
display: flex;
flex-wrap: wrap;
}

.message {
@extend %message-shared;
}

.success {
@extend %message-shared;
border-color: green;
}

.error {
@extend %message-shared;
border-color: red;
}

.warning {
@extend %message-shared;
border-color: yellow;
}

## CSS Example

/_ This CSS will print because %message-shared is extended. _/ --> This is a comment

.message, .success, .error, .warning {
border: 1px solid #ccc;
padding: 10px;
color: #333;
}

.success {
border-color: green;
}

.error {
border-color: red;
}

.warning {
border-color: yellow;
}

---

# Operators

Doing math in your CSS is very helpful. Sass has a handful of standard math operators like +, -, \*, math.div(), and %. In our example we're going to do some simple math to calculate widths for an article and aside.

## SASS Example

@use "sass:math";

.container {
display: flex;
}

article[role="main"] {
width: math.div(600px, 960px) \* 100%;
}

aside[role="complementary"] {
width: math.div(300px, 960px) \* 100%;
margin-left: auto;
}

## CSS Example

.container {
display: flex;
}

article[role="main"] {
width: 62.5%;
}

aside[role="complementary"] {
width: 31.25%;
margin-left: auto;
}
