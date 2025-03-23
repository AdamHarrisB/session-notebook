CSS Cascade

The cascade is the algorithm that defines which CSS rules are being applied when there are conflicting rules.

When styling an element the browser:

Searches for all rules with matching selectors
Sorts the rules by their importance (taking into account whether the declaration is followed by !important)
Sorts rules by their specificity
Chooses the last declaration over previous ones, if there are multiple rules with the same importance and the same specificity.

Specificity
Universal
Type
Class
ID

CSS Structure Best Practices

Keep your CSS consistent throughout a project. In collaborative projects, there will be style guidelines.
Separate global and local styles into different files (or sections of files)
Create multiple stylesheets for different parts of your application
Structure your code by thinking in reusable components. You can write your CSS for every component in its own CSS file.

You can import a stylesheet into another stylesheet like so:

@import "customer-card.css";

BEM

A popular naming convention is BEM. Blocks, Elements, Multipliers.

<article class="product">
  <h2 class="product__title">Amazing Article</h2>
  <span class="product__price">Price: 66</span>
</article>
<article class="product product--in-offer">
  <h2 class="product__title">Intrepid Item</h2>
  <span class="product__price">Price: 99</span>
</article>
<article class="product">
  <h2 class="product__title">Pretty Product</h2>
  <span class="product__price">Price: 54</span>
</article>

The article is a block
The h2 and span are elements, and are named {block}__{elementName}
The second <article> is displayed differently, thanks to the product--in-offer modifier class, that is named {block}--{modifierName}.

This use of hyphens to separate words in  variables is called kebab case.

Custom Properties (CSS Variables)

You can store values in custom properties, so you can use them again multiple times, without having to type out the value again.

It is common to store these variables in the :root pseudo class selctor:

:root {
  --primary-color: #ff00ff;
  --secondary-color: #f00f0f;
}

Custom properties must start with --

You can then use these properties elsewhere in your stylesheet.

.customer-card {
  color: var(--primary-color);
  background-color: var(--secondary-color);
}
