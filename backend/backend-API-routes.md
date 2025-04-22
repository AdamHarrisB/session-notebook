Serverless Functions

There are different approaches to creating backend functions for web applications.

A traditional web server built using Express, a Node.js framework, runs of a server or a virtual machine, listening for incoming HTTP requests. 

The code for the Express server is written in monolithic structure, which means all of the different functions and endpoints are managed by the same program.

On the other hand, Serverless Functions are only executed "on-demand", when they are needed. They wait for specific things to happen, like an HTTP request, or a website being updated. 

When that happens, the serverless function runs its code to do a specific job, and then is terminated once it is completed.

Serverless cloud providers like Vercel take care of these details, like setting up the computer resources needed to run the code. This makes it easier for developers to write code without having to worry about managing servers or resources.

What a Server-Side API is Meant for

An API (Application Programming Interface) can be seen from different perspectives and occur on various levels (what does this mean?)

API running on a server environment are called server-side APIs. They are provided by a server, rather than by the browser (also known as the client). A common use-csase for a server-side API is to create read, update and delete data. Known collectively by the amusing acronym CRUD operations.

Next.js API Routes

Our main goal is to build a database and to handle its data in our web application. To do this, we create our own API routes inside of a web application, and then decide what information and data the routes should return. Next.js provides us with a feature, which uses a simple intuitive syntax.

It follows a simple folder structure: any file inside the folder pages/api/test/file.js is mapped to the respective url with the same path e.g. /api/test/file. It is treated as an API endpoint, instead of a page.

In Next.js, an API route is simply a JavaScript module that exports a default function.

pages/api/hello.js creates the API endpoint /api/hello, which responds with a JSON message "hello Web Developer". The handler function takes two arguments, a request object and a response object, which start serverless programs on vercel, and handle incoming requests and send responses back to the client.

export default function handler(request, response) {
  response.status(200).json({ message: "Hello Web Developer!" });
}

Dynamic API Routes

Next.js supports dynamic API routes to create API endpoints that can handle dynamic parameters in the URL path, and follw the same file naming rules used for pages.

An API endpoint that handles requests for individual jokes could be created as a fule call /pages/api/jokes/[id].js This creates a dynamic API route, where the id parameter can be any value.

To get a single joke dependent on the jokes id used in the browser route, we can access the id route parameter by destructuring it from the request.query object.

export default function handler(request, response) {
  const { id } = request.query;
  //...
}

How to Log/Debug with console.log()

You can use console.log() to debug your application and gain understanding of what is happening within your API routes.

As API handlers are executed on the server, the console output will be displayed in the terminal (localhost) where you started the development server, by using npm run dev or in the Vercel web interface.