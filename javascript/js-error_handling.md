Introduction to JavaScript Error Handling

Error handling ensures that code works continuously, even when it encounters errors.

Different Types of Exceptions

JavaScript distinguishes between different types of exceptions, each indicating a different type of error with your code.

Syntax Errors

These occur when you have:

    Misspelled keywords
    Invalid assignment

// Missing closing parenthesis
console.log("Hello, world";

Runtime Errors

Also known as exceptions, these happen during the execution of the code, due to:

    Invalid operations
    Type mismatches
    Referencing non-existent variables
    Calling a function that does not exist

// Get the name of a user object
function getUserName(user) {
  return user.name;
}

getUserName("Marc"); // -> Error: string is not an object

Logical Errors

These occur when the code runs without exceptions, but produces incorrect results, due to flawed logic, or algorithmic errors.

    Incorrect conditions
    Incorrect algorithmic implementation

// Incorrect calculation
function calculateTotalCost(price, quantity) {
  return price * quantity + 10;
  // Incorrectly adds 10 to the total cost
}

const totalCost = calculateTotalCost(20, 5);
// Should be 20 * 5 = 100, but actual result will be 110

Catching Runtime Errors: The Try ... Catch Statement

The try ... catch statement provides a fairly easy solution to handling errors. You can wrap code that may lead to errors in a "try" block and specify how to handle any resulting exceptions in a catch block. You are writing an emergency protocol.

try {
  // Plan A
} catch (error) {
  // Plan B
}

Throwing Custom Errors

In addition to handling built-in exception, JavaScript allows us to "throw" custom errors to indicate specific error conditions in our code. We do this using the throw statement, which interrupts the execution flow to create an error message, which is the caught by a try catch block.

function divide(a, b) {
  if (b === 0) {
    throw new Error("Division by zero is not allowed.");
  }
  return a / b;
}

Throwing custom error messages lets you provide context to aid debugging and troubleshooting.

Handling Errors in a fetch Request Environment

Issue you may encounter when making HTTP requests using the fetch API include:

    Networking issues
    Server error
    Unexpected responses

The fetch function returns what is called a promise, allowing you to use async/await as part of your control flow statements.

async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    if (!response.ok) {
      // "!" => Logical NOT operator === response is NOT okay
      throw new Error(`Failed to fetch data! Status Code: ${response.status}`);
    }
    const data = await response.json();

    return { data: data };
  } catch (error) {
    return { error: error };
  }
}

This allows us to call code, the handleFetchData function for instance, to explicitly check if an error occurred an respond accordingly.

async function handleFetchData() {
  const result = await fetchData();

  // Check if an error has been returned
  if (result.error) {
    console.log("An error occurred:", result.error);
  } else {
    // Log successfully fetched data
    console.log("Fetched data:", result.data);
  }
}

// Invoke the handleFetchData function to process data retrieval
handleFetchData();

It is typically a good idea not to have "un-handled" errors. Knowing when to expect an error, and how to handle them is a specific skillset that every developer should have.



