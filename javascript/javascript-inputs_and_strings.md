Strings

There are three ways to create strings using "string literals":

1. 'string' - single quotes
2. "strings" - double quotes
3. `strings`- back ticks or template literals

*In general there is no preference for single or double quotes.

Strings can be chained together using the + operator. This is called a string concatenation:

const name = "Alex";
const stringConcatenation = "Hello " + name + ", good to see you!";

Template Literals

The third method to write strings, has the useful property that you can insert variables into the string by wrapping placeholders with a dollar sign and curly brackets ${}. This is also called string interpolation.

This way you don't have to concat multiple strings if you want to use a variable in string:

const stringConcatenation = "Hello " + name + ", good to see you!";

const withTemplateString = `Hello ${name}, good to see you!`;

Any expression can be placed into these placeholders:

const greeting = `Hello ${
  name !== null ? name : "mysterious person"
}, good to see you!`;

With template literals you can also write multi-line strings:

`Hello,
this is in a new line.
Good bye!`;

String Properties and Methods

Strings in JavaScript have some build-in properties and functionalities called methods. You can call them with the dot notation followed by the name of the property/method.

"A normal string".length; 
// evaluates to 15
"A normal string".toUpperCase(); 
// evaluates to "A NORMAL STRING"

.length - returns the number of characters in a string.
.toUpperCase() - returns an all uppercase version of the string
.toLowerCase() - returns an all lowercase version of the string
.trim() - returns a string with all whitespace removed from the beginning and end
.replaceAll(oldString,newString) - replaces all occurrences of oldString with the newString
.startsWith(subString) - returns true if the string starts with subString.
.endsWith(subString) - returns true if the string ends with subString.
.includes(subString) - returns true if the string contains the subString.

Input Fields

Every INPUT field in HTML holds a value in form of a string. You can access the calue by using .value on the input Element:

<form>
  <input data-js="textInput" type="text" value="test 123" />
  <input data-js="numberInput" type="number" value="42" />
</form>

const textInput = document.querySelector('[data-js="textInput"]');
const numberInput = document.querySelector('[data-js="numberInput"]');

textInput.value; 
// evaluates to 'test 123'
numberInput.value; 
// evaluates to '42' (still a string!)

You can change the value of the input by assigning a new value to this input property:

textInput.value = "changed value!";

This change is immediately visible on the website.

For example, you can enforce all uppercase letter in a form by combining this functionality with an input event listerner on the input:

// transform on every change the input value to uppercase letters
textInput.addEventListener("input", () => {
  const oldValue = textInput.value;
  const newValue = oldValue.toUpperCase();
  textInput.value = newValue;
});