Default Behaviour for Form Submit

If you click the submit button of a form, it triggers the following default behaviour:

The form sends a GET request with names and their values as prop inside an URL like:
/?firstName=value1&lastName=value2&...

The page is reloaded and thus the data is lost for us.

Listening to the submit event and preventing the Default Behaviour

In order to prevent this behaviour of the submit event, you need to:

receive the event object as an argument of the event listener arrow function
call event.preventDefault()

const form = document.querySelector('[data-js="form"]');

form.addEventListener("submit", (event) => {
  event.preventDefault();
});

By calling event.preventDefault() the browser will not perform a GET request that would cause the page to reload on submit.

The event Object and event.target

The event object is created whenever an event is triggered. You can accept it as the first parameter in the callback function and thus access it inside the function body. (e.g. via event.preventDefault())

For now, the most important method of the event object is .preventDefault().

event.target is a reference to the element to which the event originated from - in this case - the form.

form.addEventListener("submit", (event) => {
  event.preventDefault();

  console.log(event.target);
});
// Output:
// <form data-js="form">
//		<fieldset>...</fieldset>
//		...
//		<button type="submit">Submit</button>
//	</form>

Form field names

Forms are created to request information from the user. Each fragment of information (each form field) requires a unique name, which can be set with the name attribute in HTML. This attribute pairs up with the entered data, when submitting the form.

<input name="firstName" />

Accessing Interactive Fields: event.target.elements and the name Attribute

While event.target represents the entire form, event.target.elements is a collection of all form elements (form fields, field sets and buttons).

You get access to a specific form field via its name attribute and dot notation:

form.addEventListener("submit", (event) => {
  event.preventDefault();

  const formElements = event.target.elements;

  console.log(formElements.firstName);
  console.log(formElements.firstName.value);
});

Note that:

event.target.elements is stored in the variable formElements for better readability.

firstName is the string value of the corresponding name attribute, as in <input name ="firstName"/>, and

firstName.value returns the user input for the field with name="firstName".

Using Input Values

You can access all input values of the form by using FormData(). This constructor uses event.target and can be transformed into a useable object afterwards:

form.addEventListener("submit", (event) => {
  event.preventDefault();

  const formData = new FormData(event.target);
  const data = Object.fromEntries(formData);

  console.log(data);
});

This is very useful to easilt access the input data of an entire form.

Despite the fact that using FormData is much less verbose, event.target.elements is very useful if you want to access a single form field. (In case you want to focus a specific field after resetting the form, for example.)

Exception Reading Values from Checkboxes

Checkboxes have two states: checked ("true") and not checked ("false"). In contrast to other input types, the value attribute does not reflect this change, but is only used as an identifier for the checkbox.

You can access the checkbox's state via the .checked property instead.

Imagine the following checkbox

<input type="checkbox" name="colorBlue" value="blue" data-js="blue" />

and its corresponding JavaScript:

console.log(formElements.colorBlue.checked); // output: true or false
console.log(formElements.colorBlue.value); // output (always): blue

You can also react to every checking / unchecking of the checkbox:

const checkbox = document.querySelector('[data-js="blue"]');

checkbox.addEventListener("input", (event) => {
  console.log(event.target.checked); // output: true or false
});

The input Event

Occasionally, you may want to do something if the value of a single field changes even before the form is submitted.

The input event is fired every time when the value of a form field has been changed. For example, a <textarea /> will fire this event with every keystroke.

const messageInput = document.querySelector('[data-js="message"]');

messageInput.addEventListener("input", (event) => {
  console.log(event.target.value);
});

*Don't confus the input event with the change event, which is only fired after a field's content has been committed by the user by pressing enter or moving the focus to the next field.

Focus Input Fields

You can focus an input field with the .focus() method. This can be used to improve the user experience after submitting a form.

form.addEventListener("submit", (event) => {
  event.preventDefault();
  // [...] handle form data
  event.target.elements.message.focus();
});

This will focus a form field with the attribute name="message"

Resetting Forms

You can reset all form fields to their default value with the .resest() method.

form.addEventListener("submit", (event) => {
  event.preventDefault();
  // [...] handle form data
  event.target.reset();
});

This often comes in handy in combination with .focus(). Think of a chat: After the message was sent, the input field is cleared and refocussed, so users can write the next message.