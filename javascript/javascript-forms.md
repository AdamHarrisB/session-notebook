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

