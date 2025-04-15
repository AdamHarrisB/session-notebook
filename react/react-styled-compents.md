React Styled Components

What is CSS-in-JS and Why do we use it?

CSS-in-JS is a collection of ideas, used in a number of libraries, to solve complex problems in CSS. 

Styled components is one such library.

All implementations of CSS-in-JS use JavaScript as a language for creating styles.

Advantages of CSS-in-JS include:

    The critical CSS is used, and nothing else is added
    There are no class name bugs
    It is easier to delete CSS
    Dynamic styling is made more simple
    Maintenance is easier
    Automatic vendor prefixing (so that browsers can recognise the styling - WebKit for Chrome and Safari, moz for Firefox, ms for Internet Explorer)

Basic Styling

To create a component:

    Import styled
    Use it to create a styled component, like ListItem (see below)
    Implement the styled component in the return statement of your component

//components/List.js
        //1. Import styled
import styled from "styled-components";

export default function List() {
        //3. Use the styled component in the return statement
  return (
    <StyledList>
      <ListItem>Item 1</ListItem>
      <ListItem>Item 2</ListItem>
      <ListItem>Item 3</ListItem>
    </StyledList>
  );
}
        //2. Create these styled components
const ListItem = styled.li`
  background-color: crimson;
`;

const StyledList = styled.ul`
  list-style-type: none;
`;

*We use Pascal Case for the name of the styled component. Common naming convention is to included the word styled.

Styling a Custom Component

You might have a component with predefined styles that you want to further extend. 

For example the Link component from the next framework.

import styled from "styled-components";
import Link from "next/link";

export default function List() {
  return (
    <ul>
      <li>
        <StyledLink>Let's go somewhere!</StyledLink>
      </li>
    </ul>
  );
}

const StyledLink = styled(Link)`
  text-decoration: none;
`;

    OR

You've styled a component, and want to style it further, as below:

// The Button from the last section without the interpolations
const Button = styled.button`
  color: #BF4F74;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid #BF4F74;
  border-radius: 3px;
`;

// A new component based on Button, but with some override styles
const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;

Adapting Based on Props

You can adapt styling based on props (properties). To do so, you need to pass the props to the styled component. You typically prefix the prop with a $. This lets styled components know that the prop should not be passed to the underlying DOM element or component, and exists solely for styling.

import styled from "styled-components";

export default function List() {
  return (
    <StyledList $isOnFire>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </StyledList>
  );
}

You can use the props to change the style by interpolating a function into the styling. The function receives the props as an argument.

For example, a ternary operator to see if the property is true or false:

const StyledList = styled.ul`
  list-style-type: ${(props) => (props.$isOnFire ? "🔥" : "❄️")};
  /* or with destructuring: */
  list-style-type: ${({ $isOnFire }) => ($isOnFire ? "🔥" : "❄️")};
`;

You can set several CSS properies based on the same props using the css helper

import styled, { css } from "styled-components";

const StyledList = styled.ul`
  ${({ $isOnFire }) =>
    $isOnFire &&
    css`
      list-style-type: "🔥";
      background-color: red;
      color: white;
    `}
`;

Pseudoelements and Pseudoselectors

To apply a pseudoelement or selector you use the ampersand:

const StyledLink = styled(Link)`
  text-decoration: none;
  &:hover {
    color: red;
  }
`;

Global Styling

Global styling is implemented by creating a global styled component. This is housed in a styles.js file in the root of the project.

// styles.js
import { createGlobalStyle } from "styled-components";

export default createGlobalStyle`
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
      Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  }
	// more global styles here...
`;

Then import this into the pages/_app.js file and render it above the component:

// pages/_app.js
import GlobalStyle from "../styles";

export default function App({ Component, pageProps }) {
  return (
    <>
      <GlobalStyle />
      <Component {...pageProps} />
    </>
  );
}

Google Fonts GDPR- (DSGVO-) Compliant Integration

Next.js includes the @next/font npm package. It automatically optimizes your fonts and removes the need for external network requests, increasing privacy and performance by self hosting.

Install the font, and then implement it into the project where needed:

import { createGlobalStyle } from "styled-components";
import { Open_Sans } from "@next/font/google";

const openSans = Open_Sans({ subsets: ["latin"] });

export default createGlobalStyle`
  // ... some globals styles here...
  }
  body {
    margin: 0;
    font-family: ${openSans.style.fontFamily}; 
    padding: 2rem;
  }
	// ... some more global styles here ...
`;
