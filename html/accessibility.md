Accessibility

In web development is is important for us to enable as many people as possible to be able to use our website. This includes people with disabilites.

Semantic HTML

Semantic HTML help screen readers to read structure the website, and improves the readability of our HTML.

ARIA

ARIA stands for Accessible Rich Internet Applications. It is a set of attributes and roles that help make Web sites more accessible to people with disabilities.

An ARIA Role is an attribute that can be added to an HTML element to give semantic meaning. There are six categories of roles, including:

Document structure, like note or tooltip describe the structure of a section of content.

Widget Roles like slider or menu describe the type of element presented on a Web site.

ARIA States and Properties

These provide specific information about elements, their states and relationships to one another.

Two important attributes are:

aria-label - defining the label for an interactive element that might not have any text on it.

<button aria-label="Close" onclick="...">
  <svg ...><path .../></svg>
</button>

aria-labelledby - lets you know which element the label should be applied to.

<nav aria-labelledby="title">
  <h2 id="title">Products</h2>
  ...
</nav>

Accessibility Quick Wins

Use alt attributes on your images
Use high contrast colours so that they're clear on all devices
Makes sure all interactive elements have an accessible name
Use plain and simple language