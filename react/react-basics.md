dWhat is React, and why do we use it?

React is a JavaScript library for building user interfaces. Presumably one of many.

Using React allows developers to:

Create reusable components to organize and simplify their code.

Focus on what the UI should look like (declarative), while React handles how things are done behind the scenes.

Unlike vanilla JavaScript where you manage the DOM (Document Object Model) manually, React abstracts this process for efficiency.

Introduction to JSX

JSX is a syntax extention for JavaScript. It looks like HTML but behaves like JavaScript. It allows you to describe the UI declaratively.

const element = <p>Hello World!</p>;

JSX looks like HTML, but is transformed into JavaScript that the browser can understand.
Files containing this syntax extension are typically labelled with the .jsx file extension.
JSX expressions can include JavaScript code if it is wrapped in curly brackets {}

const name = "React";
const element = <p>Hello {name}!</p>; 
// Outputs: Hello React!

Imperative vs Declarative Programming

To understand the difference between imperative and declarative programming let's look at a button.

*Declarative code describes what needs to be built, imperative describes how something should be built.

Imperative Code in Vanilla JavaScript

You describe how the UI is built step by step.

const button = document.createElement("button");
button.type = "button";
button.textContent = "click me";
button.addEventListener("click", () => console.log("Hello World"));
document.body.append(button);

    We create the element with document.createElement()
    We set the button type
    We set the text content
    We add the event listener
    We append the button to the body

Declarative Code in React + JSX

You describe what the UI should look like.

const element = (
  <button type="button" onClick={() => console.log("Hello World")}>
    click me
  </button>
);

    We describe in JSX what element we want (a button)
    React figures out how to update the DOM according to our description

*A metaphor:
    The Vanilla JavaScript is how you would cook a meal for yourself. You go to the grocery store, buy the ingredients, prepare them, cook them, and finally eat them.

    The React way: you order your food from a restaurant. You just have to tell them what you want to eat, and they take care of the rest.

React Components

React components are reusable, independent building blocks of a React application. Each component combines logic and appearance, representing a part of the user interface that can be used multiple times. They could be a button, or an entire page.

Creating a Component

A component is a FUNCTION the returns JSX (JavaScript formatted in HTML)

function Button() {
  return (
    <button type="button" onClick={() => console.log("Hello World")}>
      click me
    </button>
  );
}

Using Components

export default function App() {
  return (
    <div>
      <Button />
      <Button />
      <Button />
    </div>
  );
}

Components must have names in PascalCase
They must return JSX with ONE parents element.

Nesting Elements

JSX elements in a React component can be nested in the same way we have been nesting our HTML elements. ie Parent Elements with multiple children

function Card() {
  return (
    <div>
      <p>Some Text</p>
      <p>Some more Text</p>
    </div>
  );
}

Attributes

In most cases the names for attributes are the same as in HTML, but there are some exception. Class is called className in JSX for instance.

String values are passed to attributes using double quotes ". JavaScript is passed with curly brackets {}.

const myValue = "This is a string";
const input = <input type="text" value={myValue} minLength={5} />;

Dynamic values in JSX

To make components dynamic, you can insert JavaScript expressions into JSX using curly brackets.

export default function App() {
  const buttonText = "click with React";
  return (
    <button type="button" onClick={() => console.log("Hello React!")}>
      {buttonText}
    </button>
  );
}

const name = "Pawtricia";
const element = <p>My cat's name is {name}</p>;

const a = 5;
const b = 10;

const element = (
  <p>
    {a} + {b} = {a + b}
  </p>
);

You cannot use if/else or for- loops in JSX.

How React Renders

React needs a root element in the DOM to render your application. This root acts as the entry point where React mounts its components.

HTML 
<div id="root"></div>

In some projects, this code is already provided in templates or starters. A typical setup looks like this:

const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

root.render(
  <StrictMode>
    <App />
  </StrictMode>
);

    App: The root React component of your application.

    StrictMode: A development-only tool that highlights potential issues in your code without affecting the visible UI.

How React Updates the DOM

React works smart, not hard. It uses the Virtual DOM to track changes and efficiently updates only the parts of the DOM that have changed compared to the last render.

Benefits to this include:

    Avoiding unnecessary updates, ensuring fast rendering.
    Focus remains consistent, and inputs keep their values.
    Declarative code is easier to write and understand.

Nice to Know: React, JSX, Transpilers and Bundlers

React uses JSX, which is not standard JavaScript, so it needs to be transformed for browsers using either Transpilers like Babel, which convert the code directly, or bundlers like Vite or Rollup, which combine all project files into optimized bundles, run the transpiler when needed and provide a development server.

Importing CSS Files

Bundlers allow you to use non-standard feature, like importing CSS directly into JavaScript

import "./styles.css";

This becomes a <link> tag in the final HTML.

npm

Node Package Manager is a registry for JavaScript projects.

You can install and manage libraries

  npm install package-name

and run project scripts defined in package.json, like a development server

  npm run dev

package.json

The package.json file is the configuration file for your project. It includes:

    Metadata: Project name, version, and description.
    dependencies: Libraries your app needs to run
    devDependencies: Tools needed for development
    scripts: Shortcuts for running commands like starting a development server

A package.json may look something like this:

{
  "name": "my-app",
  "version": "1.0.0",
  "description": "A description of my app",
  "scripts": {
    "test": "npm run …"
  },
  "author": "Alex Newfish",
  "license": "UNLICENSED",
  "dependencies": {
    "my-dependency": "^10.4.1",
    "my-other-dependency": "^2.0.0"
  },
  "devDependencies": {
    "my-dev-dependency": "^8.0.105",
    "my-other-dev-dependency": "^0.1.6"
  }
}

Installing dependencies

To do this, run 
 npm install

Always do this after cloning a project to set up its dependencies.

node_modules:
    Contain all installed packages (dependencies)
    Do NOT commit this folder to your repository as it is large and can be regenerated using npm install.
    Add node_modules to your .gitignore file to exclude it from version control.

package-lock.json:
    Stores the exact versions of installed dependencies to ensure consistency across different environments and team members.
    Should be committed to the repository to avoid unexpected changes caused by newer versions of a package.

Setting Up a React Project with Vite

Vite automates project scaffolding and setup, saving time.

*In principle, you could create a new React project from scratch. However this would be a lot of work and we would have to set up a lot of things ourselves.

*Vite, by the way, works quite similar to the ghcd tool you have probably already used.

A new project is created by running the following command in the terminal:

  npm create vite@latest my-react-app

If running this command for the first time, you need to install the create-vite package, accept and continue.

Select React as the framework and the JavaScript template (without SWC - speedy web compiler).

Navigate into your project folder:

  cd my-first-react-app
  npm install
  npm run dev

Project Structure

Here's a quick overview of key files and folders:

README.md - general info about project
package.json - project configuration
vite.config.js - configuration for vite
node_modules folder - dependencies
index.html - root html file, don't mess with the div id="root"></div>
public folder - static assets that are not processed by the bundler
src folder - all the source code that will go through Rollup processing
main.jsx/index.jsx - JavaScript entry point where ReactDOM renders the App component into the DOM
App.jsx - The root component of the Reach app
App.css - CSS file for the App component
index.css - CSS file for global styles