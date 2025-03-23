Flexbox

Flexbox is a tool to layout your HTML elements, especially when you want to align elements horizontally. It is defined on a container element, containing multiple elements whose position will be determined by the flexbox rules. You define it as follows:

.container-element {
  display: flex;
}

Flexbox does the following:

All child elements will be displayed next to each other along the main axis. This is the horizontal axis by default. The perpendicular axis is called the cross axis.

If the width of all of the child elements exceeds the container's width, the child elemets will be shrunk such that they all fit into the available space.

Important Flex Properties

Justify-content - Defines the position of elements along the main axis. Flex-start, flex-end, center, space-between, space-evenly

Align-items - Defines the position of elements along the cross axis: flex-start, flex-end, center

gap - defines the minimum spacing between elements

flex-direction - sets the direction of the main axis. Useful values: row, column

flex-wrap - Modifies how elements can wrap into another row, instead of being squashed into one row. Wrap, no-wrap

Flex-Direction

This is a fundamental property which defines which axis is the main one.

When this is changed, it also changes which direction the align-items and justify-content effect

Flex-Wrap
This is used for responsive layouts. By setting the property to wrap, elements move into another row if there is no space in their current row.

CSS Grid Layout
CSS Grid is another powerful tool to layout your HTML elements. It focuses on two dimensions, rather than Flexbox' one.