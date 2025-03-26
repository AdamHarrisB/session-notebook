Using Props

Props is short for properties. They are a way to pass data to a child component. A component receives a props object as the first function parameter.

Props are passed to a component as attributes.

function UserCard(props) {
  return <div>{props.name}</div>;
}

For convenience the props object is often destructured in the function parameter.

function UserCard({ name }) {
  return <div>{name}</div>;
}

You can choose any names for your props.

There are some naming conventions though. Boolean props are often prefixed with is, has, or should. For example isDisabled, hasError or shouldShow. Props that take functions are often prefixed with on. For examples onClick, onSubmit or onHover. Following these conventions makes it easier to understand the purpose of the prop.

Props can be any type (string, number, array, object, function, ...).

You should treat the props object as immutable and read-only.

Passing Props to a Component

Props are passed to a component as attributes.

<UserCard name="Alex" />

You can pass any type of data as a prop.

<UserCard
  name="Alex"
  age={25}
  onContact={() => console.log("let's chat!")}
  isFavorite={true}
  favoriteFoods={["Pasta", "Salad"]}
  contactDetails={{ email: "alex@neuefische.de", phone: "123456789" }}
/>

String props can be passed using double quotes. All other props must be passed using curly brackets.

*Notice the double curly brackets for the object. This is is because the outer brackets are used to signify a JavaScript expression.

*There is a shorthand syntax for boolean props. If the value should be true, you can omit the value.

<UserCard isFavorite />

Omitting any attribute will result in the value undefined for that prop.

Conditional Rendering

You can use props to conditionally render parts of a component.

function UserCard({ name, isFavorite }) {
  let favoriteStar = null;
  if (isFavorite) {
    favoriteStar = <span>🌟</span>;
  }

  return (
    <div>
      {name}
      {favoriteStar}
    </div>
  );
}

*In JSX null is a way to render nothing.

You can not use an if statement within JSX because only expressions are allowed. You can use an if statement outside of the JSX though.

function UserCard({ name, isFavorite }) {
  let favoriteStar = null;
  if (isFavorite) {
    favoriteStar = <span>🌟</span>;
  }

  return (
    <div>
      {name}
      {favoriteStar}
    </div>
  );
}