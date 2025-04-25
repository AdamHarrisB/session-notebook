JavaScript Modules

Sometimes called ECMAScript Modules or ESM, JavaScript Modules are a way to organise code into separate files. 

They allow you to import and export statements, but change a few things about haow your browser treats the code, in a way that is different from standard scripts.

To use them, you need to let the browser know that you are using them, with the type="module" attribute added to the <script> tag.

<script type="module" src="./my-module.js"></script>

Exporting using export Statements

The export statement exports a variable or function to make it available to other modules. You can use named exports to do this to multiple variables or functions, or one default export per module to export the main functionality of the module.

Named Exports

Usually, named exports are created using the keyword export before a const, let, or function. You can also do this after variables have been declared.

Default Exports

Default exports are created by using the keyword export default before the function declaration. There can only be one per module.

export default function sayHello() {
  console.log("Hello");
}

To export a variable or an arrow function, you only need to declare the value:

export default "Alex";

export default () => {
  console.log("Hello");
};

Default exports are nameless, and constants (const) by default.

As with named exports, you can export the default after it has been declared.

const name = "Alex";

export default name;

Having no clear name, they should semantically correspond to the name of the module. For example name.js for the export above.

Named and default exports can be mixed (both used from the same module).

Importing using import Statements

Code from other modules can be imported with the import statement. Import statements should always be placed at the top of the file. Everything that can be exported from a module should be imported by another module.

Importing Named Exports

If another module exports a named export, it is imported so:

import { name, age } from "./my-module.js";

Importing default Exports

If another module exports a default export, you need to now give it a name when importing it. This does not have to match the name of the module.

import myModule from "./my-module.js";

You can import named and default imports together like so:

import myModule, { name, age } from "./my-module.js";

and rename an import using the "as" syntax, though you must be explicit when renaming.

import { name as firstName, age as yearsSinceBorn } from "./my-module.js";

Structuring JavaScript Code

Utility Functions and Constants

Utility functions are smaller functions that perform a specific task. They should not have any side effects.

Shared constants are ones, as the name suggests, used multiply times in you code.

These should all be grouped together, and can be imported from say, a utils "utility" folder.

Vanilla JavaScript Components

Vanilla JavaScript doesn't use a framework, like React.

Even though there's no set standard, it is recommended (by Spiced Academy):

    To create a folder for each component
    Name component files and functions with PascalCase
    Each component has a default export for the component function
    Components can take arguments that are called prop or properties a convention
    Components should not depend on the outside world and create their own DOM elements
    Components should return a single DOM element

These are just recommendations.

A component that creates a button:

export default function Button(props) {
  const button = document.createElement("button");
  button.classList.add("button");
  button.textContent = props.text;
  return button;
}

And an advanced use case, a component that calls another component

import Button from "../Button/Button.js";

export default function ButtonGroup(props) {
  const buttonGroup = document.createElement("div");
  buttonGroup.classList.add("button-group");
  for (const buttonProps of props.buttons) {
    const button = Button(buttonProps);
    buttonGroup.append(button);
  }
  return buttonGroup;
}

And how to use them in another file:

import ButtonGroup from "./ButtonGroup/ButtonGroup.js";
import Button from "./Button/Button.js";

const myButtonGroup = ButtonGroup({
  buttons: [{ text: "Button 1" }, { text: "Button 2" }, { text: "Button 3" }],
});
document.body.append(myButtonGroup);

const myButton = Button({ text: "Button" });
document.body.append(myButton);

