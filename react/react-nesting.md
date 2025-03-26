Passing JSX as Props

Elements created by JSX are just objects. They can be passed around like any other object: for example, as props.

function UserCard({ avatar }) {
  return <div className="card">{avatar}</div>;
}

function App() {
  return <UserCard avatar={<Avatar />} />;
}

The children Prop

You are already familiar with nesting built-in browser tags:

<div>
  <img />
</div>

Oftentimes you'd want your own components to be nestable as well.

<UserCard>
  <Avatar />
</UserCard>

If you nest a component inside of another component, the nested component is passed as a prop to the parent component. This special prop is called children.

function UserCard({ children }) {
  return <div className="card">{children}</div>;
}

This component will render the nested element(s) as a child of the div element.

Fragments

Sometimes you want to return multiple elements from a component function without wrapping them in a div or other element. You can use a fragment (<></> or <Fragment></Fragment>) for this.

This is necessary because React components can only return a single element from a component function.

function UserList() {
  return (
    <>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </>
  );
}

This is equivalent to the following, but the shorthand version above is generally preferred.

import { Fragment } from "react";

function UserList() {
  return (
    <Fragment>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </Fragment>
  );
}

*The <Fragment></Fragment> syntax is only necessary if you want to pass the special key prop to the fragment, which will become important when you start working with lists.

*When researching you might sometimes see <React.Fragment></React.Fragment>, which is the same thing.

Composition

When we build React applications, we often want to build complex components from simpler components. This is called composition.

To do so you need to break down your application into components. You can then compose these components to build more complex components.

It is important to figure out which components you need and how they should be composed. This is called application design.