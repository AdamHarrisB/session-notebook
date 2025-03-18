Functions Purpose

Functions are a fundamental concept in programming that help us avoid repetition and make our code more organised.

Instead of writing the same code repeatedly, you can write it once inside a function and call that function whenever needed.

Function Declarations

You can define a function using a function declaration, which consists of:

The keyword function
A function name
A single parameter or a list of parameters in parentheses ().
A function body, which contains the JavaScript code, between the curly braces {}.

function functionName() {
  // Function body
}

function bakeCake() {
  console.log("Mix the ingredients.");
  console.log("Pour the batter into a pan.");
  console.log("Bake at 180°C for 30 minutes.");
}

*Defining a function doesn't execute its code; you have to call the function to run the code.

*A function should only do what its name suggests. Separate independent actions into different functions.

Function Calls

Functions can be called by their names, followed by parentheses (), to execute the code inside the function body.

Functions can be called as many times as needed.
This highlights of the main purposes of functions: to avoid code duplication.

*We already have built-in browser functions (or methods which are associated with objects) like console.log and addEventListener().

Function Parameters

A function that always shows the same message isn't very useful. 
Adding parameters makes a function more flexible by allowing different inputs. 
Functions use parameters like predefined variables inside the function body.
You can name parameters freely, except for reserved words (break, class, delete, default...)
When defining a function, these variables are called parameters.
When calling a function, the values passed are called arguments.
When the function is called, the given values become local variables that the function uses.

//           parameter ↓
function printLetter(name) {
  console.log("Hi " + name + ", hope you are fine. Your Mum");
}

//    argument ↓
printLetter("Alice");

//             parameters ↓
function printSum(first, second, third) {
  const sum = first + second + third;
  console.log("The sum of your numbers is: " + sum);
}
//   arguments ↓
printSum(3, 6, 9);

Variable Scope

Scope defines where variables are available and where they can be referenced (or used) in your code.

Variables declared inside a function are local to that function and can only be accessed from within it. They are not available outside of the function.

function printLetter() {
  // local variable
  const name = "Alice";
  console.log("Hi " + name + ", hope you are fine. Your Mum");
}
printLetter(); // Output: "Hi Alice, hope you are fine. Your Mum"
console.log(name); // 🚫 Error! The variable is not available outside of  the function

If the same named variable is declared inside the function, it shadows the outer one.
The local variable takes precedence, and the global variable is not accessible within that function.
The outer variable remains unchanged and accessible outside the function.

const name = "Alice";

function printLetter() {
  const name = "Max";
  console.log("Hi " + name + ", hope you are fine. Your Mum");
}

printLetter(); // Output: "Hi Max, hope you are fine. Your Mum"
console.log(name); // Output: "Alice"

*It's good practice to minimize the use of global variables.

Returning a value

Some functions don't return a value, but others do.

A function can return a value back into the calling code, (or variable) as the result.

Return values are values that a function sends back when it completes

To return a value from a function, use the return keyword, followed by an expression (anything that produces a value)

The return keyword can be placed anywhere in the function.
When the execution reaches return, the function stops, and the value is returned to the calling code.

function calculateSum(a, b) {
  const sum = a + b;

  return sum;
}

const firstSum = calculateSum(2, 3);
// The return value is stored in "firstSum", namely 5

const secondSum = calculateSum(4, 123);
// The return value is stored in "secondSum", namely 127

A function can return only one expression value, but there can be multiple return statements, in a single function.

For example, in combination with if-else statements.

function checkInputLength(inputString) {
  if (inputString.length > 3) {
    return true;
  } else {
    return false;
  }
}

const isValid = checkInputLength("Hey!");