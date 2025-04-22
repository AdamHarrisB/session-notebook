A Developing Language: JavaScript

JavaScript is not finished - it's still in development. The tc39 group is a bimonthly meetup to discuss proposals regarding ECMAScript (which JavaScript is based on) specifications. 

Destructuring Assignment

The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables. Destructuring does NOT mutate the original array or object.

    Destructuring Arrays

const greekLetters = ["alpha", "beta", "gamma", "delta"];

To declare the values of greekLetters as distinct variables, accessing them would be quite tedious.

Without Destructuring

const firstLetter = greekLetters[0];
const secondLetter = greekLetters[1];
const thirdLetter = greekLetters[2];
const fourthLetter = greekLetters[3];
// firstLetter → 'alpha'
// secondLetter → 'beta'
// etc.

With Destructuring

const [firstLetter, secondLetter, thirdLetter, fourthLetter] = greekLetters;
// firstLetter → 'alpha'
// secondLetter → 'beta'
// etc.

The results of the two code snippets is the same, but destructuring makes for more readable and concise code.

If you don't want or need the second and fourth values in our initial array greekLetters, there's an option to skip values as a part of the destructuring process.

const [firstLetter, , thirdLetter] = greekLetters;
// firstLetter → 'alpha'
// thirdLetter → 'gamma'

thirdLetter now contains the third value of greekLetters. The extra comma causes the constant to skip the value at the respective position in the greekLetters array. The fourth value is excluded, as the destructing assignment has ended.

Skipping values with extra commas can quickly become unreadable so we should be mindful of using this. if you wanted to skip five values:

const [a, , , , , , g] = x;

Destructuring Objects

const coachObject = {
  name: "Sam",
  mood: "great",
  skills: "amazing",
  score: 9999,
};

You can use a destructuring assignment like this:

const { name, mood, skills, score } = coachObject;
// name → 'Sam'
// mood → 'great'
// etc.

Now you have the individual keys in the object as distinct variables.

In contrast to array destructuring, the variable names are NOT arbitrary and do not depend on order. The names of variables have to match the keys of the object properties.

You can rename the variable while destructuring:

const { name: firstName } = coachObject;
// firstName → 'Sam'
// name → undefined

You can also set a default property, if it does not already exist:

const { isAdmin = true } = coachObject;
// isAdmin → true

Rest and Spread Syntax

The rest and spread syntax look deceptively similar: both are identified by three dots. The have two different functions, depending on the context in which the ... is used.

Rest Syntax (...)
The rest syntax says "put the rest into this variable" when using destructuring assignment or declaring function parameters.

You can use it with arrays:

const greekLetters = ["alpha", "beta", "gamma", "delta"];
const [firstLetter, ...allTheOtherLetters] = greekLetters;
// firstLetter → "alpha"
// allTheOtherLetters → ["beta", "gamma", "delta"]

Or with objects:

const coachObject = {
  name: "Sam",
  mood: "great",
  skills: "amazing",
  score: 9999,
};

const { name, score, ...theRestOfTheCoachObject } = coachObject;
// name → "Sam"
// score → 9999
// theRestOfTheCoachObject → { mood: 'great', skills: 'amazing' }

And even with function parameters:

function logLetters(firstLetter, ...moreLetters) {
  console.log("the first letter is", firstLetter);
  console.log("even more letters", moreLetters);
}

logLetters("alpha", "beta", "gamma", "delta");
// logs:
// the first letter is alpha
// even more letters (3) ['beta', 'gamma', 'delta']

Spread Syntax (...)

The spread syntax allows you to say "spread everything inside this variable into here" when declaring array or object literals or calling functions.

It works like this with array literal declarations:

const greekLetters = ["alpha", "beta", "gamma", "delta"];
const moreGreekLetters = [...greekLetters, "epsilon", "zeta"];
// moreGreekLetters → ['alpha', 'beta', 'gamma', 'delta', 'epsilon', 'zeta']

You can spread two (or more) arrays into another array...

const redColors = ["crimson", "pink", "purple"];
const blueColors = ["navy", "teal", "sky"];
const mixedColors = [...redColors, ...blueColors];
// mixedColors → ['crimson', 'pink', 'purple', 'navy', 'teal', 'sky']

...and it matters respectively where you spread one array into another:

const cats = ["cat", "cat", "cat"];
const dogs = ["dog", "dog", "dog"];

const catsAndDogs = [...cats, ...dogs];
// catsAndDogs → ['cat', 'cat', 'cat', 'dog', 'dog', 'dog']

const dogsAndCats = [...dogs, ...cats];
// dogsAndCats → ['dog', 'dog', 'dog', 'cat', 'cat', 'cat']

const catsBetweenBirds = ["bird", ...cats, "bird"];
// catsBetweenBirds → ['bird', 'cat', 'cat', 'cat', 'bird']

Here is how the spread works with object declarations:

const circle = { radius: 5, shape: "circle" };

const greenCircle = { ...circle, color: "green" };
// greenCircle → { radius: 5, shape: 'circle', color: 'green' }

Notice that the oders of spread operations is important, as you can override properties:

const circle = { radius: 5, shape: "circle" };

const largeCircle = { ...circle, radius: 20 };
// largeCircle → { radius: 20, shape: 'circle' }

const notALargeCircle = { radius: 20, ...circle };
// notALargeCircle → { radius: 5, shape: 'circle' }

The spread syntax is helpful for creating a shallow copy of arrays and objects:

const book = { title: "Ulysses", author: "James Joyce" };
const shallowCopyOfBook = { ...book };
shallowCopyOfBook.year = "1920";

// book → { title: 'Ulysses', author: 'James Joyce' }
// shallowCopyOfBook → { title: 'Ulysses', author: 'James Joyce', year: '1920' }

const greekLetters = ["alpha", "beta", "gamma", "delta", "epsilon", "zeta"];
const sortedGreekLetters = [...greekLetters].sort((a, b) => a.localeCompare(b));
// this is an alternative to greekLetters.slice() which also creates a shallow copy

// greekLetters → ['alpha', 'beta', 'gamma', 'delta', 'epsilon', 'zeta']
// sortedGreekLetters → ['alpha', 'beta', 'delta', 'epsilon', 'gamma', 'zeta']

You can also use the spread syntax when calling functions:

const numbers = [4534, 3411, 2455, 4952];
const smallestNumber = Math.min(...numbers);
// smallestNumber → 2455

Optional Chaining

The operational chaining operator ?. is like the chaining operator . except that instead of throwing an error if a reference is nullish (null or undefined), the expression "short-circuits" with a value of undefined. This is useful if you're not sure if a property, method or index exists or if something is call-able.

function feedCats(cats) {
  return cats.forEach((cat) => console.log(cat, "says meow"));
}

feedCats(["Garfield", "Tom", "Grumpy Cat"]);
// logs:
// Garfield says meow
// Tom says meow
// Grumpy Cat says meow

feedCats();
// throws:
// Uncaught TypeError: Cannot read properties of undefined (reading 'forEach')

function feedCats(cats) {
  return cats?.forEach((cat) => console.log(cat, "says meow"));
}

feedCats();
// logs nothing, but also does not throw

The ?. short-circuits the expression and evaluates the return statement to undefined. This way the error is avoided without the need to explicitly use if statements or ternaries to check values.

Optional chaining is useful when targeting a property in an object that has a deeply nested structure. For example:

const person = {
  name: "Sam",
  skills: [
    {
      name: "HTML",
      level: 9999,
      category: {
        name: "coding",
      },
    },
    {
      name: "Agile",
      level: 1337,
      category: {
        name: "projects",
      },
    },
  ],
};

console.log(person.skills[1].category.name);
// logs: projects

console.log(person.skills[2].level);
// throws: Uncaught TypeError: Cannot read properties of undefined (reading 'level')

console.log(person.skills?.[2]?.level);
// logs: undefined

console.log(person.skills[0].partner.name);
// throws: Uncaught TypeError: Cannot read properties of undefined (reading 'name')

console.log(person.skills[0].partner?.name);
// logs: undefined

Nullish Coalescing

The nullish coalescing operator ?? is a logical operator that returns its right-hand-side operand when its left-hand-side operand is null or undefined, and otherwise returns its left-hand-side operand.

const chocolate = true;

function chocolateCheck() {
  return chocolate ?? "No chocolate :(";
}

const result = chocolateCheck();

In this example our function returns the value of chocolate because the value of chocolate is neither null or undefined.

const chocolate = undefined;

function chocolateCheck() {
  return chocolate ?? "No chocolate :(";
}

const result = chocolateCheck();

In this example, our function would return 'No chocolate :(' as the value is undefined (and would do the same for a value of null as well).

Written as an if/else statement, the code will look like this:

const chocolate = true;

function chocolateCheck() {
  if (chocolate === null || chocolate === undefined) {
    return "No chocolate :(";
  }

  return true;
}

const result = chocolateCheck();