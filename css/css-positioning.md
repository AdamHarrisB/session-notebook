Positioning

The position property comes in handy if you want to place an HTML element manually. There are five values to define position:

position: static - The position is determined by the document flow (default)

position: relative - Position the element relative to where the element would be placed normally

position: absolute - Position the element absolutely inside the nearest non-static ancestory element

position: fixed - Position the element on a fixed position on the screen

position: sticky - The element is placed normally in the document flow, but keeps an offset relative to its nearest scrolling ancestor

The position is then specified with top, bottom, right and left.

Position: Static
The properties top, bottom, right, left, have no effect.

Position: Relative
Top, bottom, right, left, are used to move the element relative to where it would be by default.

Position: Absolute
Elements are removed from the normal document flow. They're positioned using the top, bottom, right, left relative to the last no static ancestor element, or if non is present, than the page itself.

Position: Fixed
These elements are removed from the the normal flow, defined with top, bottom, right, left. Used for navigation bars or back to the top buttons

Position: Sticky
This element is not affected by the positioning, until it comes near the border of a scrolling container, at which point it behaves like a fixed element.

Z-Index
The z-index defines the stacking order of html elements. Elements with a higher stacking order appear on top if they overlap with other elements. The z-index only effect positioned elements - those with a non-static position.
