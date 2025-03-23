What is CSS?

Cascading Stylesheets you can add styling to your HTML elements

The term cascading in CSS refers to the algorithm that resolves conflicts when multiple styles are defined for an element.

Specificity - How precisely a selector targets an element.

The Source order - Last in the stylesheet takes precedence.

Inheritance - Children inherit their parent elements styles.

A stylesheet is a collection or rulesets declared using CSS, typically in a .css file.

Linking Stylesheets

Link in the <head> of the HTML file

<head>
  …
  <link rel="stylesheet" href="css/styles.css" />
</head>

CSS Syntax

Selector - h1 {}
Property - color:
Property Value - blue;

h1 {
  color: blue;
  font-size: 3rem;
  text-align: center;
}

Selectors

Type selector - like: article, h1, p, div, a, input, button...

Class selector - .classname, .superpink...

Pseudo-classes - an element in a specific state - :hover, :focus...

Attribute selectors - selects all elements that have a certain attribute - [type]

Attribute value selector - [attribute="value"]

Universal selector - "*" - selects all elements in the document

Combining Selectors

Use commas to apply to any one of the selectors

h1,
h2,
h3 {
  color: hotpink;
}

Descendant Combinator

Effects all .superpink elements that are descendants of article elements.

article .superpink {
  color: hotpink;
}

CSS Properties

Examples include: color, font-size, text-align, background-color, border, padding, margin, width

Inheritance

CSS properties are inherited from the parent element to the child element. If not specified more specifically

body {
  color: hotpink;
}

p {
  /* The color of the paragraph is hotpink because it is inherited from the body */
}

Box Model

All elements of a website are rectangular boxes described by the box model. Each of those boxes has four areas (listed from inside to outside): content, padding, border, margin

You can set width using a content-box (just the width of the content) or border-box (width of border, padding and content together) (preferred)

The browser calculates the size with width and height.

We can set the box sizing of all elements to border box so:

* {
  box-sizing: border-box;
}

Now the width property defines the size of the border box, padding and border width are subtracted to calculate the available space for the content.

Inline and Block Elements

There are two kinds of elements: inline-level and block-level elements.

Inline Elements

Inline elements are as wide as their maximum content width and flow with the text lines.

These include: a, span, strong,  img, input, button...

Block Elements

Block elements take up the full width of their parent elements and always start on a new line.

These include: p, h1 - h6, div, section, article, header, footer, nav ...

You can change the default behaviour of elements by using the CSS display property.

h2 {
  display: inline;
}

or 

a {
  display: block;
}