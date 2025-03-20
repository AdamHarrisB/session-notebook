Basic Form Setup

<form> tag

The <form> tag must be wrapped around the complete form  with all elements, that are presented as form controls to the user.

<form>
  <!-- All form elements inside -->
</form>

Labels

The <label> always goes together with a form field. It provides a caption to let users understand what kind of data they are asked to enter.

It is required to define, which label and form field belong together. Use the for attribute on the <label> and the id attribute on the form field. Their values need to match.

<label for="first-name">First name</label> <input id="first-name" />

*Always add a label to a form field, otherwise users won't understand the purpose of a field, which makes it unusable.

*Never use the placeholder attribute instead of a label.

Different types of form field

Text

The default type for <input> elements is text. Choose the type based on the kind of data the user is requested to enter. Use type="text" when none of the other types is a better fit.

<label for="first-name">First name</label> <input type="text" id="first-name" />

Email

Use type="email" to let the user enter an email address. The browser can check automatically, whether the entered text is a valid email address.

<label for="email-address">Email address</label>
<input type="email" id="email-address" />

Number

Use type="number" to let the user enter a number.

<label for="age">Age</label> <input type="number" id="age" />

Date

Use type="date" to let the user enter a date with the help of a date picker (calendar) provided by the browser.

<label for="date-of-birth">Date of birth</label>
<input type="date" id="date-of-birth" />

Color

Use type="color" to let the user enter a color with the help of a color picker tool provided by the browser.

<label for="favorite-color">Favorite color</label>
<input type="color" id="favorite-color" />

Multi-line text

Use the tag <textarea> to let the user enter longer text with multiple lines.

<label for="personal-message">Personal Message</label>
<textarea id="personal-message"></textarea>

Select / dropdown menu

The <select> field lets the user choose between different options wrapped into <option> tags that are nested into their parent <select> tag - this renders a dropdown menu. Each <option> has a vlaue attribut defining the data to be submitted. The option's text presented to the user is defined between the opening and closing tag.

<label for="billing-plan">Billing plan</label>
<select id="billing-plan">
  <option value="weekly">Weekly billing</option>
  <option value="monthly">Monthly billing</option>
  <option value="yearly">Monthly billing</option>
</select>

Radio elements

The <input type="radio" /> element is another way of presenting a choice with different options to the user. In many situations it can be used as an alternative to <select>.

*Each radio element that refers to the same choice needs a name attribute, that must be equal among all radio elements. The browser groups them together and ensures that only one radio element can be selected at the same time.

<input
  type="radio"
  id="billing-plan-weekly"
  value="weekly"
  name="billing-plan"
/>
<label for="billing-plan-weekly">Weekly billing</label>

<input
  type="radio"
  id="billing-plan-monthly"
  value="monthly"
  name="billing-plan"
/>
<label for="billing-plan-monthly">Monthly billing</label>

<input
  type="radio"
  id="billing-plan-yearly"
  value="yearly"
  name="billing-plan"
/>
<label for="billing-plan-yearly">Yearly billing</label>

Checkboxes

In contrast to the radio element <input type="checkbox" /> presents individual choices, that are not related to each other. Each choice can either be "on" ("true") or "off" ("false").

*The name attribute must not be equal among the checkbox elements, as they are used to represent individual choices.

HTML Form Validation

Before submitting a form, it is important to ensure all required form fields are filled out, in the correct format. This is called client-side form validation.

HTML provides several form field attributes to enable validation features build into the browser.

required - if present, a form field needs to be filled in before the form can submitted.

minLength/maxlength - minimum and maximum length of textual data (strings)

min/max - minimum and maximum values of numerical input types

type - each input type has its own prefigured validation (like email)

pattern - a regular expression pattern the entered data needs to follow

Example: the following input field is valid if its value exists and it is a string between 3 and 30 characters:

<input id="input-name" type="text" minlength="3" maxlength="30" required />

Buttons

Submit button

The default type for a <button> element is submit. It is used to let users submit the form's data after they filled out all fields.

<button type="submit">Send</button>

*Since it's the default, it would work the same without the type attribute: <button>send</button>.

Reset button

A button with type="reset" lets the user reset all form fields to their default value on click.

<button type="reset">Reset all fields</button>

Other buttons

Since type="submit" is the default for <button> elements, buttons outside of a form element should always be defined with type="button" to be semantically correct.

<button type="button">Click here for more information</button>

This also applies to buttons with diverging functionality within a form.

Form Structure and a11y

Fieldset and Legend

The <fieldset> element is used to group multiple fields together. Use the <legend> element to provide a caption for such a group.

<fieldset>
  <legend>Personal information</legend>

  <label for="first-name">First name</label>
  <input type="text" id="first-name" />

  <label for="email">Email address</label>
  <input type="email" id="email" />
</fieldset>

aria labels

aria-label

The aria-label attribute defines a label for an interactive element. Use it when the accessible name is missing and there's no content visible in the DOM that can be referenced via the aria-labelledby attribute, e.g. a button with no text but only an icon:

<button aria-label="Close form" onClick="...">
  <svg ...><path ... /></svg>
</button>

aria-labelledby

The aria-labelledby attribute identifies which element labels the element it is applied to. Use the id attribute to create the connection:

<h2 id="title">Personal Information Form</h2>
<form aria-labelledby="title">...</form>

aria-describedby

The aria-labelledby attribute allows more verbose information than a label. Use the id attribute to create the connection:

<p id="description">
  We need some personal information about you in order to proceed. Please fill
  in this form so that we can help you.
</p>
<fieldset aria-describedby="description">...</fieldset>