JS DOM and Events

"this is where we learn how to connect a JavaScript file with <script>

Connect a JavaScript file

<head>
  ...
  <script src="./index.js" defer></script>
</head>
<body>
  ...
</body>

The script tag has two attributes:

src="./index.js" sets the URL to our JavaScript file

defer tells the browser to delay the loading of the script until all HTML elements are loaded.

You can alternatively add the script tag to the end of the body element, so the defer attribute is not necessary. This is not as modern.

<head>
  ...
</head>
<body>
  ...
  <script src="./index.js"></script>
</body>

The DOM

In order to access and manipulate elements of our web page from inside our JavaScript file we can use the DOM - Document Object Model. It contains every element of our HTML document represented as a JavaScript object. We will learn about objects in a later session.

In a JavaScript file the DOM is stored in a variable called document.

console.log(document);
console.log(document.head);
console.log(document.body);

With the help of this variable we can find, create, and manipulate elements on our web page.

Selectig HTML Elements: .querySelector()

Before we can add interactivity, we need to select the necessary HTML-Elements:

<body>
  <main class="main" id="main" data-js="main">...</main>
</body>

There are multiple ways to select the main section above in JavaScript. A good practice is to use a data-* attribute, such as data-js, as shown in the following example.

const mainElement = document.querySelector('[data-js="main"]');

Other CSS selectors work as well, but the data.* attribute selectors should be preferred.

// tag as identifier
const mainElement = document.querySelector("main");
// class as identifier -> .
const mainElement = document.querySelector(".main");
// id as identifier -> #
const mainElement = document.querySelector("#main");

**We try to separate our concerns: Classes are for CSS and data-* attributes are for JavaScript.**

Add Interaction: .addEventListener()

We can listen to events like clicks on an element and execute code when the event is triggered. The method addEventListener is used to react to events.

<button type="button" data-js="button">Log into console</button>

const button = document.querySelector('[data-js="button"]');
button.addEventListener("click", () => {});

First you specify the type of event (e.g., click), and then you defintie the code to be executed when the event is triggered. This code is written inside the {} brackets, such as a console.log statement.

const button = document.querySelector('[data-js="button"]');
button.addEventListener("click", () => {
  console.log("Yeah");
});

There are different events you can listen to, for example;

button.addEventListener("mouseover", () => {});

button.addEventListener("keydown", () => {});

Add/Remove & Toggle Classes: .classList.

You can add, remove, or toggle classes to change the styling of an element. For example:

<main data-js="main">
  <button type="button" data-js="button">Add a class</button>
</main>

To add the page-primary class to the main section, you can use the classList.add method like this:

const main = document.querySelector('[data-js="main"]');
const button = document.querySelector('[data-js="button"]');

button.addEventListener("click", () => {
  main.classList.add("page--primary");
});

A click on the button adds the class page--primary to the main element:

<main data-js="main" class="page--primary">
  <button type="button" data-js="button">Add a class</button>
</main>

You can also remove or toggle a class in the same way:

main.classList.remove("page--primary");
main.classList.toggle("page--primary");

