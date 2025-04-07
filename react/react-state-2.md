Sharing State Between Components

Passing State Down

The value of a state variable and the function set can be passed down to child components as props. They are functions and values, so they can be passed down like any other data.

function Parent() {
  const [count, setCount] = useState(0);

  function handleIncrement() {
    setCount(count + 1);
  }

  return <Child count={count} onIncrement={handleIncrement} />;
}

function Child({ count, onIncrement }) {
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={onIncrement}>increment</button>
    </>
  );
}

Lifting State Up

When we have multiple components that need to share state, we can lift the state up to the parent component and pass it down as props. This is called "lifting state up" because you usually start with the state directly in the child component, and then move it up to the parent components as you need it.

A state variable can be passed down to multiple child components. The child components can then update the state variable by calling the setter function.

A state variable should live as low in the component tree as possible but obviously as high as is needed. If the whole app needs to know about the state variable then it should be in the app component. If only child components of an article need to access it, then it should be in that article component.

Handling Form Data

Using Form Data onSubmit

We can use the event handler onSubmit to handle form data. The on submit event handler is called when the user submits the form. We can get the form date from the event object. (As in regular JavaScript).

function SearchForm() {
  function handleSubmit(event) {
    event.preventDefault();
    const form = event.target;
    const searchTerm = form.elements.searchTerm.value;
    console.log("A new search term was submitted:", searchTerm);
  }
  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="searchTerm">Search</label>
      <input name="searchTerm" id="searchTerm" />
      <button>Search</button>
    </form>
  );
}

In this example the input elements value is not manually controlled by React: this input is an "uncontrolled input". Its value is managed by the browser. The submit event handler peeks at the input field and read the value from the Document Object Model.

Using Controlled Inputs

We can use React to control the value of an input element. This is called a "controlled input".

This means we set the value attribute of the input element manually. We can link a state variable to the value attribute of the input elment. This way the input element will always have the same value as the state variable.

This, combined with the onChange event handler allows us to update the state variable when the user types in the input field

function SearchForm() {
  const [searchTerm, setSearchTerm] = useState("");

  function handleSubmit() {
    event.preventDefault();
    console.log("A new search term was submitted:", searchTerm);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="searchTerm">Search</label>
      <input
        name="searchTerm"
        id="searchTerm"
        value={searchTerm}
        onChange={(event) => setSearchTerm(event.target.value)}
      />
      <button>Search for {searchTerm}</button>
    </form>
  );
}

In the above example we know the value of the search term input. As it is a state variable, we can reuse it in other places in the application.

*Preferably use uncontrolled inputs, but there are times where using a controlled input is necessary.

For instance:

Showing search results as a user is typing
Autocompleting a user's input
Validating the user's input

State Updates are NOT Immediate

When we call the setter function of a state variable, React will not update the state variable immediately. It will update its internal value and schedule a re-render of the component.

This behaviour can be hard to predict, but it is vital to understand that state values aren't refreshed immediately.

This code is broken:

function Counter() {
  const [count, setCount] = useState(0); // count is 0 initially

  function handleIncrement() {
    // when this is first called, count is still 0
    console.log(count); // → 0

    // this will set reacts internal state to 1,
    // but does not update the count variable
    setCount(count + 1);
    console.log(count); // → 0

    // the count variable is still 0, thus count + 1 is still 1,
    // so react's internal state will still be 1
    setCount(count + 1);
    console.log(count); // → 0

    // since setter functions were called
    // react will schedule a re-render of
    // the component with the new count value of 1
  }

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>increment by 2</button>
    </>
  );
}

You could fix this code by calling setCount(count + 2), but if we need to call setCount tweice, we can use the function form of the setter function, as it provides the current internal value of a state variable as an argument.

// ⚠️ This code is unnecessary complicated, but it works!
function Counter() {
  const [count, setCount] = useState(0); // count is 0 initially

  function handleIncrement() {
    // when this is first called, count is still 0
    console.log(count); // → 0

    // this will set reacts internal state to 1,
    // but does not update the count variable
    setCount((prevCount) => prevCount + 1);
    console.log(count); // → 0

    // the internal value of count is 1,
    // we get it as the the first parameter of the function we pass to the setter.
    // 1 + 1 is 2, so react's internal state will now be _2_
    setCount((prevCount) => prevCount + 1);
    console.log(count); // → 0

    // since setter functions were called
    // react will schedule a re-render of
    // the component with the new count value of _2_
  }

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>increment by 2</button>
    </>
  );
}

The prefix prev indicates that the value is the previous value of the state variable. A common convention is to use just the first letter of the state variable as the parameter name: setCount(c => c + 1)

React Hooks

useState is part of a broader set of features that provide components with more functionality.

Hooks are functions that allow component functions to hook into React features (like state) and allow components to do more than a standard JavaScript function can.

They follow the naming convention: useXyz

Like, useState and useEffect.

When using a hook you must obey the following rules:

Only call hooks at the top level. Not inside loops, conditions or nested functions.

Only call hooks from React function components or custom hooks. Don't call hooks from regular JavaScript functions.
