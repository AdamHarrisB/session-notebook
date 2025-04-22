Asynchronous Code

Asynchronous code runs in the background, and is used for tasks that will take a long time to complete, but shouldn't block the main thread.

JavaScript is a single threaded language, so only one thing can happen at a time.

Blocking the main thread is bad, as it prevents the user from interacting with the page, as no other JavaScript code can be executed. Examples of asyncronous code include: network requests, file system access, animations and timers.

Promises

Asynchronous functions will NOT return their return value directly, but a promise instead. A promise is an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value. Most of the time, it is returned by a function that performs an asynchronous operation. There are two ways to work with asynchronous functions: promises or async/await.

Asynchronous Code with Promises

