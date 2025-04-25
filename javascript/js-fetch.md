Asynchronous Code

Asynchronous code runs in the background, and is used for tasks that will take a long time to complete, but shouldn't block the main thread.

JavaScript is a single threaded language, so only one thing can happen at a time.

Blocking the main thread is bad, as it prevents the user from interacting with the page, as no other JavaScript code can be executed. Examples of asyncronous code include: network requests, file system access, animations and timers.

Promises

Asynchronous functions will NOT return their return value directly, but a promise instead. A promise is an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value. Most of the time, it is returned by a function that performs an asynchronous operation. There are two ways to work with asynchronous functions: promises or async/await.

Asynchronous Code with Promises

You can use the then method with a callback function to react to the completion of the asynchronous operation.

asynchronousFunction().then((value) => {
  console.log(value);
});

*Promises are usually created by other asynchronous APIs. If you're creating a new promise yourself, you need to know what your doing, and might be on the wrong track.

Asynchronous Code with Async/Await

Async functions are a syntactic sugar for Promises (I don't know what this means). Using the await keyword, you can write asynchronous code, that looks like synchronous code. Any function can be prefixed with the async keyword.

async function myAsyncFunction() {
  // ...
}

const myAsyncArrowFunction = async () => {
  // ...
};

Inside an async function you can use the await keyword to wait for a promise to be resolved:

async function myAsyncFunction() {
  const value = await otherAsynchronousFunction();
  console.log(value);
}

What is an API

An API is a Application Programming Interface.

An API provides a way that one piece of software can interact with other software. Therefore, an application can define a set of features, and rules on how other software can interact with it. This is called an interface.

It's like a contract between two softwares, outlining how they will work together.

API can be seen from different perspectives, and occur on various levels (again, I don't know what this means).

A browser provides a lot of Web APIs. Each Web API defines a way in which a JavaScript application can use a feature of the browser, for instance:

    Web Animations API
    Battery API
    Fetch API

APIs running on a server environment are a different type of API. They are provided by a server, rather than an API provided by the browser (also called the client). A common use-case for these server APIs is to read and load data. Other operations like writing or deleting data are also possible. There are common approaches regarding the architecture of server-side APIs. One such approach is REST-APIs.

Fetch API (with async & await)

fetch is a web API to asynchronously fetch (load) resources from the network, like text documents.

async function fetchData() {
  const response = await fetch("/url/to/something");
  const data = await response.json();
  return data;
}

The example above does the following:

    The function is marked with the async keyword as we want to use await in the function.
    A variable called response is defined. It stores the response object returned by fetch.
    Once this promise resolves we call the .json method on the response variable. This function returns another Promise.
    This second promise resolves with the actual data (payload) converted from JSON (a formatted string) to a JavaScript value or object. This result is stored in the variable named data.
    The function returns the value stored in the data variable.

JSON

JavaScript Object Notation (JSON) is a standard text based format for representing structured data based on JavaScript object syntax. It is commonly used to transmitting data between a client (browser) and a server in web applications.

JSON is very close to being a subset of JavaScript syntax. Most valid JSON is also valid JavaScript code. This means you can copy JSON into any .js file, put a const myData = in front of it, and then watch Prettier turn it into real looking JavaScript.

However. Valid JavaScript is NOT valid JSON.

An example of JSON:

{
  "groupName": "Students",
  "groupSize": 100,
  "students": [
    {
      "name": "John Doe",
      "age": 42,
      "location": "Pleasantville",
      "member": true,
      "groups": ["students", "citizens", "new"]
    },
    {
      "name": "Jane Doe",
      "age": 44,
      "location": "Pleasantville",
      "member": true,
      "groups": ["students", "citizens", "new"]
    },
    {
      "name": "Sam Doe",
      "age": 24,
      "location": "Pleasantville",
      "member": true,
      "groups": ["students", "citizens", "new"]
    }
  ]
}

Even though it closely resembles JavaScript object literal syntax, if can be used outside of JavaScript. Other programming languages have the ability to read (parse) JSON.

JSON exists as a string that needs to be converted to a native JavaScript object when you need to access the data. We can do this through two conversion methods:

JSON.parse() - This method parses a JSON string and constructs the JavaScript value or object described by the string.

JSON.stringify() - This methods converts a JavaScript value or object to a JSON string.

HTTP Response Status Codes

HTTP Response Status Codes indicate whether a specific HTTP request has been successfully completed. By and large ANY sort of response is considered a successful completion of the request.

With the exception of custom server software, these responses are standardized: 404 not found, 200 OK, 301 Moved Permanently, etc.

Rest API

When you create an API, you need to come up with ideas on how to structure your own API, shape the features you provide and the rules that you apply. This is referred to as the architecture of your API.

There are different common approaches used, a popular one is REST API or RESTful API.

REST (REpresentational State Transfer) is a set of architectural constraints, not protocol or a standard. You as an API developer have a variety of ways that you can implement REST.

The overall idea is:

    A client requests a resource from a server.

    The server formulates a response that represents the resource in a format the client understands.

    This transfer of data changes the state of the web application.

Each resource has a unique address. All of the communication is done via HTTP, and uses different HTTP methods, like GET/POST/PUT/DELETE.


