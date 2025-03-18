Boolean Values

A Boolean value, named after George Boole, only has two states, it can either be true or false.
Booleans are often used in conditional statements which can execute different code depending on their values.

Truthy and Falsy Values

Sometimes you want to have a condition depending on another type of value. JavaScript can transform any value into a boolean with type coercion. That means come values can act as true, and others as if they were false.

Truthy values become true
    Non zero numbers
    Non empty strings
    true

Falsy values become false
    0/-0
    null
    undefined
    empty string: ""

Comparison Operators

Comparison operators produce boolean values by comparing two expressions:

A === B strict equal: is true if both values are equal, including type.
A !== B strict not equal: is true is both values are not equal (including their type)
A > B strictly greater than
A < B strictly less than
A >= B greater than or equal
A <= B less than or equal

*JavaScript uses three equals sign to check equality.
= (const x = 0) is an assignment operator and has nothing to do with comparisons.
== and != are non-strict equality operators. You should avoid this 99% of the time.
Non-strict equality tries to use type coercion to convert both values to the same type:
"3" == 3 is true, which is rarely what you want (they are different types)
=== and !== are strict equality operators. This is what you need almost always. Strict equality checks if type AND value are the same: "3" === 3 is false.

Logical Operator

Logical operators combine up to two booleans into a new boolean.

!A not: flips a true value to a false value, and vice versa.
A || B or: is true if either A or B is true.
A && B and: is true if both A and B is true.

*You can combine logical operators with brackets to define which operator should be evaluated first, e.g:

(A || B && (C || D))
!(A || B)

*Be careful when using && or || with non-boolean values. They actually retun one of the original values. That can be useful but can also quickly lead to confusion. This behaviour is called short-circuit evaluation, and is a more advanced topic.

"some string" || "some other string" evaluates to "some string"
0 || 100 evaluates to 100
null && "yet another string" evaluates to null

Control Flow: if/else

With an if statement we can control whether a part of our code is executed or not, based on a condition.

const isSunShining = true;

if (isSunShining) {
  // code that is executed only if condition "isSunShining" is true
}

The else block is executed only is the condition is false.

const isSunShining = false;

if (isSunShining) {
  // code that is executed only if condition "isSunShining" is true
} else {
  // code that is executed only if condition "isSunShining" is false
}

The condition expression between the () brackets can be composed of logical or comparison operators as well. You can distinguish between more cases by chaining else if statements:

if (hour < 12) {
  console.log("Good Morning.");
} else if (hour < 18) {
  console.log("Good afternoon.");
} else if (hour === 24) {
  console.log("Good night.");
} else {
  console.log("Good evening.");
}

If the condition is not a boolean, it is converted into one by type coercion. This can be used to check whether a value is not a 0 or an empty string:

const name = "Alex";
if (name) {
  console.log("Hi " + name + "!"); 
  // only executed if name is not an empty string
}

Ternary Operator: ? :

With if / else statement whole blocks of code can be controlled. The ternary operator can be used if you want to decide between two expressions, e.g. which value should be stored in a variable:

const greetingText = time < 12 ? "Good morning." : "Good afternoon.";

The ternary operator has the following structure:

condition ? expressionIfTrue : expressionIfFalse;

If the condition is true, the first expression is evaluated, otherwise the second expression. The ternary operator can be used to decide which function should be called:

isUserLoggedIn ? logoutUser() : loginUser();

It can also distinguish which value should be passed as an argument to a function.

moveElement(xPos > 300 ? 300 : xPos); 
// the element can't be moved further than 300.

* The ternary operator can only distinguish between two expression like values, math / logical operations or function calls, not between statements like variable declarations, if / else statements or multi-line code blocks.

Switch Statement

Sometimes, we need to check if a variable or expression matches one of several specific values. In such cases, a switch statement provides a clearer and more efficient solution than using multiple if...else statements.

Here's an example:

console.log("Which is your favorite season of the year?");
const userAnswer = "spring";

switch (userAnswer) {
  case "summer":
    console.log("Heat, sun and waves for you 😎");
    break;
  case "autumn":
    console.log("Crunchy, colorful leaves and cool breezes 🍁");
    break;
  case "winter":
    console.log("Ice, snow, warm clothes and hot drinks ☕️");
    break;
  case "spring":
    console.log("Growth, green, and new beginnings! 🌿");
    break;
  default:
    console.log("Sorry, I don't think that's a season!");
}

*Syntax guidelines for the switch statement:
Similar to an if statement, the evaluated value or expression should be placed inside parentheses ().
The entire body of the switch statement must be enclosed in curly braces {}, just like an if statement.
Each case specifies a single constant value (not an expression) to compare against.
A colon : must follow each case value.
By default, all cases of a switch statement are checked, even if a case already matched before. This "fall-through" behaviour is seldom what we want and can be prevented with a break statement. When executed it terminates the switch statement immediately, similar to the return statement of a function.
It's advisable to include a default case to handle unmatched values; this does not require a break.