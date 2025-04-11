Effects in React

Effects are one way to synchronize React components with external systems. 

We interact with external systems when we

    Manipulate the DOM directly
    Make network requests to fetch data
    Work with Web APIs
    Set up or tear down subscriptions and global event handlers
    Set timers
    Integrate third party libraries

Using an effect is a way out of the the declarative coding of React. It allows us to run imperative code, not directly related to the rendering of the User Interface.

Component functions are supposed to be clean, effect functions do not need to be, and can contain side effects.

An effect is a function that is executed AFTER the component has been rendered and the Document Object Model has been updated. It can be synchronized to run on mounting AND when all or only certain values within the component function has changed.

Effect functions can return a cleanup function that is executed before the effect function runs again, or once the component is unmounted.

useEffect

The useEffect hook adds effects to a React component. It takes two arguments:

    a function that defines the effect
    an array of variables that the effect depends on

For example, the following code with update the component title to have the value of the title prop:

import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    // updating the document title is a side effect
    // that is not directly related to rendering the UI
    document.title = title;
  });

  return <h1>{title}</h1>;
}

Effect Dependencies

The above effect runs after the component has been rendered, and the Document Object Model has been updated.

This is more than is necessary, and we only want it to run after the title prop changes. Ensure this, we can pass an array of reactive values to the useEffect() hook. The array will then only run when one of these reactive values changes.

import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    document.title = title;
  }, [title]);

  return <h1>{title}</h1>;
}

This is important when there's more than one prop (property) or state value (changeable value like a desk lamp). Below there is a count state in the component:

import { useEffect, useState } from "react";

function Title({ title }) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = title;
  }, [title]);

  return (
    <div>
      <h1>{title}</h1>
      <p>{count}</p>
      <button type="button" onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}



