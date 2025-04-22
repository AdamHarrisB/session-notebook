THE Web Storage API

*The Web Storage API is NOT part of React, it's a browser API available in all modern browsers.

The Web Storage API offers two methods for storing data on the client:

    localStorage - stores data with no expiration date
    sessionStorage - stores data for a single session, lost once the browser tab is closed

Data that is stored by a website in the browser is done so by domain. i.e. data from example.com can be accessed by www.example.com, and subdomain.example.com, but not by others.org.

This means that it is possible to store data across page reloads and browser restarts securely.

To store data the API uses key-value pairs. The key is a string, and the value can be a string, a number or a boolean.

*The examples are for localStorage, but apply to sessionStorage as well

Storing Data

To store data, use the setItem() method:

localStorage.setItem("name", "Alex");
localStorage.setItem("age", 28);
localStorage.setItem("isOnline", true);

Retrieving Data

To retrieve data, use the getItem method:

const name = localStorage.getItem("name"); // → "Alex"
const age = localStorage.getItem("age"); // → 28
const isOnline = localStorage.getItem("isOnline"); // → true

Calling get Item will return null if the key does not exist

const nope = localStorage.getItem("nope"); // → null

Removing Data

To remove data, use the removeItem() method:

localStorage.removeItem("name");

Clearing All Data

To remove all data, use the clear() method:

localStorage.clear();

Storing Complex Data

The Web Storage API only supports strings, numbers, and booleans. To store more complex data, you need to serialize it. This can be does using the JSON.stringify() method:

const user = {
  name: "Alex",
  age: 28,
  isOnline: true,
};

localStorage.setItem("user", JSON.stringify(user));

To then retrieve the data you need to parse it using the JSON.parse() method:

const user = JSON.parse(localStorage.getItem("user"));

Helper Functions

To make working with the Web Storage API easier, you can create helper functions that encapsulate the serialization and deserialization:

// store data
function setItem(key, value) {
  localStorage.setItem(key, JSON.stringify(value));
}

// retrieve data
function getItem(key) {
  return JSON.parse(localStorage.getItem(key));
}

These functions work with simple data types such as strings and numbers, as well as complex ones:

setItem("user", {
  name: "Alex",
  age: 28,
  isOnline: true,
});
setItem("count", 42);

const user = getItem("user");
const count = getItem("count");

React with Local Storage

You can also use the Web Storage API in React. Most commonly you will want the state to persist in local storage, so that it will survive the page being reloaded.

React has several ways to synchronise state with local storage. The general concept is to retrieve the initial state from the local storage and to store the state in local storage whenever it changes.

Because it can be quite difficult to wire up all of these pieces yourself, we can use a library hook instead.

use-local-storage-state

The use-local-storage-state library provides us with a hook that allows you to persist state in local storage.

You can use it as a drop-in replacement for the useState hook. This has been commented out in the below example:

// import { useState } from "react";
import useLocalStorageState from "use-local-storage-state";

function Counter() {
  // const [count, setCount] = useState(0);
  const [count, setCount] = useLocalStorageState("count", { defaultValue: 0 });

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

React Custom Hooks

The useLocalStorageState hook is not part of React, but is a custom hook from a third party library. You can also create your own hooks to abstract away common logic that uses other hooks (useState, useEffect, ...).