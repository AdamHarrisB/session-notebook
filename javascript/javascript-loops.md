A loop executes a respective block of code over and over again until a criteria is met.

In JavaScript there are two basic types of loops:

while: used when a task needs to be executed until a specific criteria is met.

for: commonly used when a task needs to be executed a certain number of times or for each element in an object or array.

While

The while loop is the most fundemental type of loop. It repeats a code block as long as the stated criteria is true.

let string = "a";

while (string.length <= 8) {
  console.log(string);
  string = string + string;
}

// 'a'
// 'aa'
// 'aaaa'
// 'aaaaaaaa'

This loop repeats itself 4 times, until the string becomes too long and the loop criteria changes to false.

For

For loops are intended for repeating a task as long as a certain condition is fullfilled. They consist of four internal parts:

The initialization expression: The expression (if any) is executed. It usually initialized one or more loop counters, but it can execute any degree of expression, even variable declarations.

The condition expression: As long as the condition evaluates to "true", the loop statement executes, otherwise the loop terminates. If there is no condition expression specified, the condition is assumed to be true.

The loop statement: Is executed as long as the value of the condition is true. To execute multiple statement, use a block statement ({}).

The afterthought expression: If present, the afterthought expression is executed after the loop statement.

for (initialization; condition; afterthought) statement;

or

for (initialization; condition; afterthought) {
  statement;
  statement;
}

For example:

for (let counter = 0; counter < 4; counter++) {
  console.log(counter);
}
// 0
// 1
// 2
// 3

For...in

The For...in is a shorthand notation to loop through all keys of an object:

const user = {
  name: "Alex",
  age: 28,
  email: "alex@mail.com",
};

for (const key in user) {
  console.log(user[key]);
}

// 'Alex'
// 28
// 'alex@mail.com'

The loop has an iterator variable, in this case "key" which is assigned the respective key value in each iteration (first 'name', then 'age' and finally 'email')

For...of

Similar to for...in, the for...of loop is a shorthand notation, but for looping through all items of an array.

const fruits = ["apple", "banana", "melon"];

for (const fruit of fruits) {
  console.log(fruit);
}

// 'apple'
// 'banana'
// 'melon'

This time the iterator variable "fruit" is assigned the respective array item in each iteration.