How the Web works

The "world wide web is a network of computers that can exchange information with each other. There are many different protocols that define the rules on how machines communicate. Browsers use HTTP (Hypertext Transfer Protocol) to communicate with web servers.

URL (Uniform Resource Locator) is the unique addres of a resource on the web contains a human readable domain name, that needs to be resoved to the technical IP (Internet Protocol) address of the web server via a DNS (Domain Name Server)
The brower sends a GET (an HTTP method) request to load a HTML (Hyper Text Markup Language) document from a web server
The web server sends a response containing the document
Often the HTML code contains references to additional resources (CSS (Cascading Style Sheet) files, images, etc.) which the browser then also requests from the server
The browser renders the received content to the screen and makes it interactive
Browsers might also request additional data from servers later via subsequent GET or POST requests

Web Protocols

There are many different protocols that define the rules on how two machines communicate with each other, for example:

Requesting and displaying html files via http
Accessing the shell of other computer via ssh or cloing repositories from GitHub via a ssh connection
Sending and receiving email via TLS/SSL
Accessing files on a server via FTP (File Transfer Protocol)

For now we are focusing on the most commonly used feature of the web: displaying and interacting websites.

In order to view a specific website:

Get the address of the server that provides the html file
Send a GET request
Request additional resources (CSS files, images, etc.)
Render the received content

Most computers can be reached with an IPv4 address consisting of four numbers between 0 and 255 separated by a dot.

Websites are reached via URL, the browser then requests the IP address from a DNS (Domain Name Server). Think of this as like a phone book for domains.

Then the browser fetches all necessary content for the website. Once downloaded, the browser displays it.

HTML Basics

<h1>Headline</h1>
Text is wrapped with an opening and closing tag
These can be nested to create structure and hierarchy.

<h1>I am a <em>headline</em></h1>

Some elements don't contain any other elements, and therefore don't have a closing tag. These are called empty elements.
<hr />
<br />

HTML Tag Attributes

Some elements require more information to work properly. Like a link:

<img src="logo.png" alt="the logo of the company."/>

<a href="https://example.com">Click me</a>

Layout of an HTML File

<!doctype html>
<html>
  <head>
    … meta information, additional links to CSS / JavaScript files …
  </head>
  <body>
    … elements displayed on the web page …
  </body>
</html>

Structuring a Website

There are two tools to express a meaningful structure in a website:

1. Using semantic HTML elements
2. Nesting/grouping of HTML elements

Semantic HTML

Divides the document into distinct parts AND describes what their purpose is.

This is more understandable for other developers, and more accessible for users and search engines.

<main></main>
<session></section>
<ul></ul>
<ol></ol>
<nav></nav>
<aside></aside>
<article></aside>
<header></header>
<footer></footer>

Nesting HTML elements

Nesting groups elements in a meaningful way. The element containing other elements is the parent element, which contains one or more child elements.

