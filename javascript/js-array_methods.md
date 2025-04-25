Introduction to Array Methods

The array methods here all have a lot in common, and can be used in much the same way.

    You provide a callback function with one parameter
    The array method iterates over an array
    The provided callback function gets called for each element in the array
    With each call to the function the current array element gets passed as an argument

This method allows you to write code and have it apply to each element within an array.

forEach

The array method forEach executes some logic "for each" element within an array:

const pets = ["bird", "cat", "dog", "ferret", "fish"];
pets.forEach((pet) => {
  const petElement = document.createElement("p");
  petElement.textContent = pet;
  document.body.append(petElement);
});

*The callback function provided to forEach must not use a return statement. forEach DOES NOT return a new array.

*Use forEach when using a side-effect, like document.CreateElement

map

The array method for map is used to apply a transformation to each element of an array.

The transformed elements are stored in a NEWLY CREATED ARRAY, returned by map. The elements in the original array remain UNALTERED.

You can define the type of transformation being applied to each element in the callback function and return the transformed element.

The create and the original array have the same length:

const pets = ["bird", "cat", "dog", "ferret", "fish"];
const uppercasePets = pets.map((pet) => {
  return pet.toUpperCase();
});
console.log(uppercasePets); // ['BIRD', 'CAT', 'DOG', 'FERRET', 'FISH']

*The callback funciton provided to map MUST use a return statement to return a transformed element. map returns a new array. In the above example this is uppercasePets.

*You should NOT use map to trigger a side effect. No document.createElement. No.

filter

The array method filter is used to create a new array with a subset of the elements from the old array.

The callback function returns a boolean value to define, if an element is being included in the resulting array or not. The original array is not being altered.

The created array is likely to be shorter than the original array.

const pets = ["bird", "cat", "dog", "ferret", "fish"];
const petsWithF = pets.filter((pet) => {
  return pet.startsWith("f");
});
console.log(petsWithF); // ['ferret', 'fish']

*The callback function provided to filter MUST use a return statement to return a boolean value.

Chaining Array Methods

Often times you need to combin multiple array methods to achieve a desired result. Array methods like map and filter, that return a new array, can be chained. (USED ONE AFTER THE OTHER, presumably). Instead of storing each array in a separated variable, the methods can be directly called, one after another. This reduces the amount of code, and improves readability.

const pets = ["bird", "cat", "dog", "ferret", "fish"];
const uppercasePetsWithF = pets
  .filter((pet) => {
    return pet.startsWith("f");
  })
  .map((pet) => {
    return pet.toUpperCase();
  });
console.log(uppercasePetsWithF); // ['FERRET', 'FISH']

document.querySelectorAll

With document.querySelectorAll you can select a list of elements from the DOM. This is in contrast to the classic document.querySelector, which provides only the first occurrence of an element matching the selector. (Presumably querySelectorAll returns all matching elements)

const pets = document.querySelectorAll('[data-js="pet"]');
console.log(pets.length); // 5

The NodeList returned by document.querySelectorAll is an array-like object. You can use the forEach method to iterate over the DOM elements.

const pets = document.querySelectorAll('[data-js="pet"]');
pets.forEach((pet) => {
  pet.addEventListener("click", () => {
    // [...]
  });
});

*A NodeList is NOT an array. Other array methods like map or filter can't be used. If you need to use array methods, you can convert the NodeList to an array using Array.from().

includes

Use array.includes to check whether the array contains the specified value. If it does, true is returned, otherwise false.

const colors = ["hotpink", "aquamarine", "granite"];

colors.includes("aquamarine"); // true
colors.includes("nemo"); // false

find and findIndex

Use find() to receive the first element of the array that satisfies the provided testing function. Otherwise, it returns undefined.

const colors = ["hotpink", "aquamarine", "granite", "grey"];

colors.find((color) => color.startsWith("g")); // 'granite'
colors.find((color) => color.startsWith("b")); // undefined

Use findIndex() to receive the index of the first element of the array that satisfies the provided testing function. If there is no such element, -1 is returned.

const colors = ["hotpink", "aquamarine", "granite", "grey"];

colors.findIndex((color) => color.startsWith("g")); // 2
colors.findIndex((color) => color.startsWith("b")); // -1

toSorted and toReversed

*Array methods sort() and reverse() mutate the original array. This is BAD. So instead we use toSorted() and toReversed(). These are recent additions to the ECMAScript standard, and require Node.js version 20 or higher. They return a new array that has been reversed or sorted and can be stored in a new variable.

Use toSorted() to sort elements of an array. You need to provide a callback function in order to tell how the array is sorted.

Sorting Numbers

const numbers = [4, 42, 23, 1];

numbers.toSorted((a, b) => a - b); // [1, 4, 23, 42]
numbers.toSorted((a, b) => b - a); // [42, 23, 4, 1]

The sorted order is based on the return value of a - b / b - a:

Return value of a - b 	sort order
> 0 	sort a after b
< 0 	sort a before b
=== 0 	keep original order of a and b

Weird, but seems to return the numbers in ascending or descending order respectively.

*toSorted converts the elements into strings, then compares their sequences of UTF-Code units values. So array.toSorted() is largely useless without a callback.

Sorting Strings

In order to sort strings, you need to tell the toSorted() method two things inside of the callback function:


    lowercase both strings before comparing them (uppercase works as well) (So that letters have values that makes sense in UTF).
    using if-statements, be explicit about the return values dependent on the result of the comparison (nameA < nameB and nameA > nameB)

const strings = ["Xbox", "PlayStation", "GameBoy"];

strings.toSorted((a, b) => {
  const nameA = a.toLowerCase();
  const nameB = b.toLowerCase();
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }
  return 0;
});

console.log(strings); // ['GameBoy', 'PlayStation', 'Xbox']

toReversed

In order to reverse an array, simply use array.toReversed(). This can be combined with toSorted() as well:

const numbers = [4, 42, 23, 1];

const reversedNumbers = numbers.toReversed(); // [1, 23, 42, 4]

some and every

Use some() to test whether at least one element in the array passes the provided test.

const colors = ["hotpink", "aquamarine", "granite"];

colors.some((color) => color.startsWith("g")); // true
colors.some((color) => color.startsWith("i")); // false

In order to check if all elements pass the test, use every()

const colors = ["hotpink", "aquamarine", "granite"];

colors.every((color) => color.length > 5); // true
colors.every((color) => color.length < 3); // false

reduce

Array.reduce() is an array method to reduce a list of values into a single value. Its main use is calculate the sum of an array of numbers:

const numbers = [4, 42, 23, 1];

const sum = numbers.reduce((a, b) => a + b);

console.log(sum); // 70

Avoid doing anything more complex than this with reduce(). Find other solutions for that, for instance:

const myArray = [
  { foo: 1, bar: "hi" },
  { foo: 4, bar: "hey" },
  { foo: 2, bar: "ho" },
];
const myObject = {};
myArray.forEach((element) => {
  myObject[element.bar] = element.foo;
});

console.log(myObject); // {hi: 1, hey: 4, ho: 2}