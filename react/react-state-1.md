What is state

State is data that changes over the time. Like the lamp on your desk, if can be switched on or off. It is at a particular state at a give time, and that can be changed.

Another example would be money in your wallet. It can increase and decrease dependent on the exercise your are carrying out. Going to the ATM vs going to the store.

This concept also applies to software. Your app can have data that changes over time.

Think of a post on social media: it can be liked or unliked, like the lamp on your desk.

Your bank's website contains a digital representation of your analog purse. Your balance is displayed and you can use the banking software to change that state. Transferring money to increase or decrease this balance.

Often this state changes with a user interaction. LIKE CLICKING A BUTTON.

State in React

In React we work with state by using the useState hook function.

We call the function, and pass the initial state as argument.  This is the value that the app uses until something changes.

Calling the useState function gives us two things in return:

    a variable with the current state as value
    the set function to set a new state

import { useState } from "react";

    //The function is Social Media Post
function SocialMediaPost() {
  const [liked, setLiked] = useState(false);
    //The initial state value is unliked, presented as an argument 

  function toggleLiked() {
    setLiked(!liked);
  }

  return (
    <article>
      <p>Liked: {liked ? "Yes" : "No"}</p>
      <button type="button" onClick={toggleLiked}>
        {liked ? "Remove like" : "Add like"}
      </button>
    </article>
  );
}

*THERE IS ALWAYS A NAMING CONVENTION FOR REACT APPS THAT THE STATE VARIABLE AND THE FUNCTION ALWAYS FOLLOW THE PATTERN OF X and setX

In React state is encapsulated per instance of a component. Think of a feed in a social media app. The feed is a list of posts. Each post is an individual state. When change the "liked" state of one of the posts, all the other posts stay as they are.

A React component can have multiple states. You can use the useState function as often as you need.

You can store all kinds of data in state (like booleans, numbers, strings, objects or arrays).

import { useState } from "react";

function SocialMediaPost() {
    //a boolean
  const [liked, setLiked] = useState(false);
    //an array
  const [comments, setComments] = useState([]);
    //a number
  const [views, setViews] = useState(0);

  /* ... */

  return <article>{/* ... */}</article>;
}

What happens when state changes?

To handle state in React we can not simply use a normal variable and assign a new value. React needs to be informed that the data was changed.

This is related to the render cycle of React components.

When React renders a component it executes the component function, which returns JSX. If the JSX includes a state variable, it uses the variable's value at that time to place into the JSX. Calling the set function with a new value informs React, that the state has changed.

*Changing a state triggers a re-render of the component. (GOOD TO KNOW)

When re-rendering the component, React executes the component function again from top to bottom, which will again return JSX. However this time the variable has a new value - the value that was passed with the call of the set function. This means the return JSX includes the new value.

