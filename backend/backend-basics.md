JavaScript Outside of the Browser

Up until now we have only used JavaScript in the browser, but it can also be used outside of the browser. Using a runtime environment called Node.js.

Node.js does have some differences to the the browser. For example, Node.js doesn't have a DOM (document object model) but provides some APIs (Application Programming Interface) that aren't available for the browser. For example, Node provodes an API to access the file system.

Node can create a web server, which is a program that listens for requests and sends responses back to the client. The web server can be used to serve web pages or to provide an API for a web application.

Running a Node Progam

To run a Node program you need to use the node command. The node command takes the path to a JavaScript file as an argument. The node command "node index.js" will execute the JavaScript file index.js.

For the sake of convenience our templates include a script in the package.json that allows you to run the program with npm run start. The template includes a development mode, automatically restarting the program when changes are made to the code: npm run dev. You can see how these are defined in the package.json file to see how the scripts are defined.

A Basic Node.js Program

A Node.js program can be almost anything. A web server, a command line tool or a script that does calculations. 

This one prints Hello World:

console.log("Hello World");

This one does a calculation:

const answer = 32 + 4;
console.log(answer);

We run the program with the node command. As outlined above.

*In node, console log displays in the console terminal, and not the browser console.

Node.js Servers

Node.js can be used to create web servers. To do so you can use the http module provided.

You can import a native node module by using the node: prefix, for instance:

import { createServer } from "node:http";

You don't need to install the http module it is included in Node.js.

Creating a Server

The http module provides a function called createServer, which takes a callback function as an argument. The callback function is called whenever a request is made to the server. The callback function is called with two arguments: request, and response. 

The request object contains information about the request that was made to the server. 

The response object is used to send a response back to the client.

import { createServer } from "node:http";

export const server = createServer((request, response) => {
  response.statusCode = 200;
  response.end("Hello World");
});

The response.statusCode property sets the status code of the response. response.end takes a string as an argument. The string is then sent back to the client.

You can access the request object to get information about the request that was made to the server. For example you can access the url property of the request object to get the URL that was requested:

import { createServer } from "node:http";

export const server = createServer((request, response) => {
  if (request.url === "/") {
    response.statusCode = 200;
    response.end("Hello World");
  } else {
    response.statusCode = 404;
    response.end("Not Found");
  }
});

Response and Request are often abbreviated as res and req.

Starting the Server (Listening for Requests)

To start the server you need to call the listen method on the server object. The listen method takes two arguments: the port number and an optional callback function. The callback function is called when the server is ready to accept requests.

To separate the code that creates the server from the code that starts the server you can export the server object from a server.js and then start the server in index.js

// index.js
import { server } from "./server.js";

const port = 8000;
server.listen(port, () => {
  console.log(`Server running at http://127.0.0.1:${port}/`);
});

*When the listen method is called, node.js will keep the program running instead of exiting. This is necessary, as the program needs to be running in order for requests to be accepted.