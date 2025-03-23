Mobile First Design

When authoring CSS it's a helpful convention to define all of your mobile style, and then add media queries to adjust the styles for larger screens.

Most users are on mobile devices, and this practice also helps you to focus on the most important information first.

Responsive Units

These units are relative to the viewport, font size or parent element

vh - viewport height
vw - viewport width
em - 1em is the font size of the current element
rem - 1rem is the font size of the root element
% - is relative to the related property of the parent or current element
    width 1% - 1% of the parent element's width
    padding-top 10% - 10% of the parent's height
    font-size: 50% half as big as the parent font-size
    transform: translateX(50%) - translate on the x axis by 50% of the current element's width.
Calc() - allows you to combine multiple units and do math
    calc(100vh - 100px)
    calc(50% - 10rem)

Media Queries

Media Queries allow you to write CSS for specific media types, screen sizes, orientations and more.

They follow this syntax:

@media (media feature) {
  /* CSS rules */
}

You can target a specific media type with the screen and print media types.

@media screen {
  /* CSS rules that are only applied on screens */
}

@media print {
  /* CSS rules that are only applied when printing */
}

Specific screen sizes can be targeted with min-width and max-width.

@media (min-width: 600px) {
  /* CSS rules that are only applied when the screen is at least 600px wide */
}

@media (max-width: 600px) {
  /* CSS rules that are only applied when the screen is at most 600px wide */
}

You can target a specific orientation with the orientation feature

@media (orientation: portrait) {
  /* CSS rules that are only applied when the screen is in portrait orientation */
}

@media (orientation: landscape) {
  /* CSS rules that are only applied when the screen is in landscape orientation */
}

Pointer

You can target specific pointer types with any-pointer media feature.

@media (any-pointer: none) {
  /*
		CSS rules that are only applied when the device has no pointer
		(neither touch nor cursor)
	*/
}

@media (any-pointer: coarse) {
  /*
		CSS rules that are only applied when the device has a coarse pointer
		(mostly touch)
	*/
}

@media (any-pointer: fine) {
  /*
		CSS rules that are only applied when the device has a fine pointer
		(cursor)
	*/
}

You can also target specific pixel ratios:

@media (device-pixel-ratio: 1) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 1
		(mostly older screens)
	*/
}

@media (device-pixel-ratio: 2) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 2
		(newer screens like the retina screen on your MacBook)
	*/
}

@media (device-pixel-ratio: 3) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 3
		(some high resolution tablets and phones)
	*/
}

Or the user's preferred color scheme, reduced motion settings, high contrast, etc.

@media (prefers-color-scheme: dark) {
  /* CSS rules that are only applied when the user prefers a dark color scheme */
}

@media (prefers-color-scheme: light) {
  /* CSS rules that are only applied when the user prefers a light color scheme */
}

@media (prefers-reduced-motion: reduce) {
  /* CSS rules that are only applied when the user prefers reduced motion */
}

@media (prefers-contrast: more) {
  /* CSS rules that are only applied when the user prefers a higher contrast */
}

You can combine these Media Features with "and" or use a comma when the user only needs to match one of the criteria:

@media (min-width: 600px) and (orientation: landscape) {
  /* CSS rules that are only applied when the screen is at least 600px wide and in landscape orientation */
}

@media (min-width: 600px), (orientation: portrait) {
  /* CSS rules that are only applied when the screen is either at least 680px high or in portrait orientation */
}

Common Breakpoints

It can be helpful to reference common breakpoints: min-width: 600px, 900px, 1200px, 1536px etc.

:root {
  --font-size: 12px;
}

@media (min-width: 600px) {
  :root {
    --font-size: 16px;
  }
}

@media (min-width: 1200px) {
  :root {
    --font-size: 20px;
  }
}

body {
  font-size: var(--font-size);
}

Showing different images based on media queries

You can use media queries to show different images based on screen size.

The HTML picture element allows you to definte multiple source elements for an image, the browser will choose the first that matches the given media query. If none of these match, then the img element, which is required, will be used as a fallback.