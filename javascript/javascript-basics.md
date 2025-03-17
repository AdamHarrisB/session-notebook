JavaScript - Your first programming language

JavaScript consists of a series of instructions that are executed sequentially, one after another. For example

console.clear(); //executed first
const text = "Hello World!";
console.log(text); //executed last

JavaScript was originally designed to run in the browser, but since 2009 can also be executed (run) outside of the browser using a program called node.js.

Node interprets the JavaScript syntx and follows the instructions provided.

It is important to follow syntax rules precisely; otherwise, Node.js won't understand your instructions. For example, you must place a "." between console and clear - with nothing in between

console.log("hey"); //works!
consolelog("hey); //wrong syntax - fails
console.log<"hey">; //wrong syntax - fails

Where humans can understand syntax errors, computers cannot!

Learning all of these syntax rules is like learning a new language, a programming language!

---

In JavaScript we can print text to the terminal using console.log()

console.log("Hello World"); // logs into console
console.clear(); // clears console
console.error("Error!"); // logs as error into console

The concept of a variable
A variable is a container for a value.

var - (outdated, not used anymore)
let - (creates a variable that can be changed)
const - (creates a variable that can not be changed)

Normally we use const for variables

const aNewVariable = 1234;

The keyword let is only used when you need to reassign a value, for example when you want to increase a counter

let counter = 0;
counter = counter + 1; //reassigning the value of counter

The equals sign doesn't work quite like the mathematical equality sign that you remember from school. It instead means: "the value of the item on the right of the equal sign is saved in the item on the left of it.

What the itm on the right actually represents is calculated first, and saved afterwards.

Primitive Data Types

JavaScript is a dynamically typed language, which means you don't have to specify what kind of value you want to store, JavaScript detects this automatically.

There are 7 primitive data types:

string - a sequence of characters: "abcd"
number - a number: 1234
boolean - a binary statement, can be true or false
null - represents "nothing", is typically set by developers
undefined - represents the state of "not existing". Anything not specified or not found in JavaScript defaults to the value undefined
BigInt - uncommon, used for integers larger than 90017882547440991
Symbol - uncommon, used for creating unique elements

Two kinds of non-value in variables
undefined - (variable not yet given a value)
null - (an intentional null value)

Variable Naming

Expressive variable names are very important for the readability of the code. The code becomes easier to understand, and needs less comments. There are some key guidelines you should follow when naming a variable.

use camel case
write out all words: error instead of "e"
be very specific, longer names are better than shorter: "updatedFollowerCounter" instead of "counter"

Math and Operators

As a programmer you sometimes have to use mathematical operations to calculate certain widths or positions of elemets. Operators calculate values based on one or two expressions.

+ : adds two numbers together
- : subtracts two numbers
* : multiplies two numbers
/ : divides two numbers
** : potentiates two numbers (raises to a power) <2 ** 4 : 16>
% : The remainder or modulus. Gives you what remains after a whole number division <8 % 3 : 2>

Remainder might not seem it at first but it's a useful operator, and can be used to determine if a number is even or odd:

6 % 2; // 0
5 % 2; // 1 (and 1 for all odd numbers)

or to display 24 hour clock times as 12 hour times

5 % 12; // 5
7 % 12; // 7
12 % 12; // 0
15 % 12; // 3
27 % 12; // 3

Operator Precedence

Will have to return to this (can be gamed with brackets)

Assignment Operators

The default assignment operator is =. This operator just assigns the value on the right of the element to the left. There are other very common assignment operators.

+= : Increased the valuable on the left about the value on the right: count += 6 (increase count value by 6)
-= : Decreases the value of the variable on the left about the value on the right: count -= 6 (decrease count value by 6)
*= : multiplies the variable by value on the right.
/= : divides the variable by the value on the right;
++ : increase the value of the variable by one (count++ is count increased by one)
-- : decreases the value of the a variable by one: count-- (count is decreased by one)

Type Coersion

When you use a variable with an unfitting type, JavaScript with convert (coerse) this variable into the fitting type.

4 / "2"; // 4 / 2

