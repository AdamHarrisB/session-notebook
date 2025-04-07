Arrays in JSX

To Render elements from an array in React, use the method .map()

This method applies a transformation to all items of an array. When rendering array items in JSX we transform every item of the array into a JSX tag. This is why we use .map() specifically.

function Drinks() {
  const drinks = ["water", "lemonade", "coffee", "tee"];

  return (
    <ul>
      {drinks.map((drink) => (
        <li>{drink}</li>
      ))}
    </ul>
  );
}

Key Property

The example above misses a tiny BUT VERY IMPORTANT part: the key prop.

    Warning: Each child in a list should have a unique "key" prop.

When rendering an array in JSX you need to pass a unique identifier as a value for the key prop. This is so that React can keep track of changes that happen to the data when re-rendering.

function Drinks() {
  const drinks = [
    { id: 0, name: "water" },
    { id: 1, name: "lemonade" },
    { id: 2, name: "coffee" },
    { id: 3, name: "tea" },
  ];

  return (
    <ul>
      {drinks.map(({ id, name }) => (
        <li key={id}>{name}</li>
      ))}
    </ul>
  );
}

*If you pass the key prop to a component, you cannot access it in the component. It is a special prop that React only uses internally.

function Drink({ name, key }) {
  console.log(key); // → undefined
  return <li>{name}</li>;
}

function Drinks() {
  const drinks = [
    { id: 0, name: "water" },
    { id: 1, name: "lemonade" },
    { id: 2, name: "coffee" },
    { id: 3, name: "tea" },
  ];

  return (
    <ul>
      {drinks.map(({ id, name }) => (
        <Drink key={id} name={name} />
      ))}
    </ul>
  );
}

*To access the id in the above example, you can pass it again as a prop:

 <Drink key={id} id={id} name={name} />.

 Keyed Fragments

 If render a list of items that are not wrapped in a single JSX tag you can wrap them with a <fragment>

 You can't use the shortened syntax <> for the fragment because you need to pass the key prop to the fragment, as in the example below:

 import { Fragment } from "react";

function Drinks() {
  const drinks = [
    { id: 0, name: "water", description: "very wet" },
    { id: 1, name: "lemonade", description: "quite sweet" },
    { id: 2, name: "coffee", description: "cold brew" },
    { id: 3, name: "tea", description: "earl grey, hot" },
  ];

  return (
    <dl>
      {drinks.map(({ id, name, description }) => (
        <Fragment key={id}>
          <dt>{name}</dt>
          <dd>{description}</dd>
        </Fragment>
      ))}
    </dl>
  );
}


