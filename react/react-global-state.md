React Global State

Lifting State Up

Often a state that exists in one component is needed in another component. The components have to share a common state. We do this by moving the state up the component hierarchy to the first parent component they share. This is called "lifting state up".

Prop Drilling 

Individual components can be far away from each other in the compoent hierarchy, so the state variables must be passed from the shared ancestor via props until they arrive in the target component.

This is called prop drilling:

function App() {
  const [userIsLoggedIn, setUserIsLoggedIn] = useState(false);

  return <ProductsPage userIsLoggedIn={userIsLoggedIn} />;
}

function ProductsPage({ userIsLoggedIn }) {
  return <ProductsList userIsLoggedIn={userIsLoggedIn} />;
}

function ProductsList({ userIsLoggedIn }) {
  return products.map((product) => (
    <ProductCard {...product} userIsLoggedIn={userIsLoggedIn} />
  ));
}

function ProductCard({ userIsLoggedIn }) {
  return <ProductActions userIsLoggedIn={userIsLoggedIn} />;
}

function ProductActions({ userIsLoggedIn }) {
  return userIsLoggedIn ? (
    <button>One-click Buy</button>
  ) : (
    <button>Add to Basket</button>
  );
}

In the example above, the state variable userIsLoggedIn is defined in the App component.

Prop drilling through a few levels is perfectly fine. However, if the path gets longer and several state variables are passed via props, the complexity increases and the maintainability of the code is reduced. On the way, passing each prop must not be forgotten in any component.

Naming Conventions from Props and Functions

In the React Props handout (https://github.com/spiced-academy/malabar-web-25/blob/main/sessions/react-props/react-props.md) there is general information about the conventions for naming variables and functions that are passed by props.

Avoid renaming props halfway through when prop drilling.

Prefix function names with handle and corresponding props with on.

function App() {
  const [userIsLoggedIn, setUserIsLoggedIn] = useState(false);

  function handleLogIn() {
    setUserIsLoggedIn(true);
  }

  return <Layout handleLogIn={handleLogIn} />;
}

function Layout({ handleLogIn }) {
  return <Header onLogIn={handleLogIn} />;
}

function Header({ onLogIn }) {
  return <button onClick={onLogIn}>Log In</button>;
}

State Management Libraries

In the React ecosystem a number of different libraries have evolved to simplify the handling of complex state. To avoid excessive prop drilling, the concept of "global state" is an established solution.

State is not defined in a component and passed through via props, but defined outside the hierarchy. Each component can access the global state.

There are many libraries that offer implementations for global state. Spiced recommends "Zustand" (https://github.com/pmndrs/zustand)

Below is an example of a global state using Zustand:

import { create } from "zustand";

const useUserStore = create((set) => ({
  isLoggedIn: false,
  logIn: () => set(() => ({ isLoggedIn: true })),
  logOut: () => set(() => ({ isLoggedIn: false })),
}));

function App() {
  return <ProductsPage />;
}

function ProductsPage() {
  return <ProductsList />;
}

function ProductsList() {
  return products.map((product) => <ProductCard {...product} />);
}

function ProductCard() {
  return <ProductActions />;
}

function ProductActions() {
  const userIsLoggedIn = useUserStore((state) => state.isLoggedIn);

  return userIsLoggedIn ? (
    <button>One-click Buy</button>
  ) : (
    <button>Add to Basket</button>
  );
}

Don't use global state exclusively. 

Look at when it might be pertinant to store data as a global state to be used by a number of components.