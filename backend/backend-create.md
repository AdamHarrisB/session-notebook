Crud and Rest

Crud

The acronym CRUD, covers the four basic operations of persistent storage

    Create
    Read
    Update
    Delete

These operations can be expressed using different terms depending on context or environment.

Create
    MongoDB - insertOne / insertMany
    SQL - INSERT
    HTTP Method - POST
    Rest URL - /todos

Read    
    MongoDB - findOne / find
    SQL - SELECT
    HTTP Method - GET
    Rest URL - /todos/[todoId] (for one) /todos (for all)

Update
    MongoDB - updateOne / updateMany
    SQL - UPDATE
    HTTP Method - PUT / PATCH
    Rest URL - /todos/[todoId]

Delete
    MongoDB - deleteOne / deleteMany
    SQL - DELETE
    HTTP Method - DELETE
    Rest URL - /todos/[todoId]

REST

REST is short for "Representational State Transfer" and refers to architectural principles and constraints how to structure your API.

We use CRUD operations and HTTP methods with a REST API.

Create with Mongoose

To create a new entry in your database, first define a POST API route, then call the .create method:

// pages/api/index.js
if (request.method === "POST") {
  try {
    const jokeData = request.body;
    await Joke.create(jokeData);

    response.status(201).json({ status: "Joke created" });
  } catch (error) {
    console.log(error);
    response.status(400).json({ error: error.message });
  }
}

POST alone doesn't create an entry, you need to tell the form's submit handler to use this route.

Sending POST Requests and Revalidating Data

Since we are mutating our data array (jokes in the example), we need to:

    Send data to our backend to add them to the database
    update our app so that it uses the updated data from the database.

If we don't revalidate our data, the app won't reflect these newly made changes. useSWR has a method called mutate, which triggers this revalidation for a given API endpoint, in the example /api/jokes. We can destructure it from the hook call, as with data, or isLoading:

const { mutate } = useSWR("/api/jokes/");

To then perform a POST HTTP request with fetch, we must provide an options object to the fetch call, which includes the following information:

    method: a word like PUT POST or DELETE to define the type of HTTP request
    the "Content-Type" which is provided in the request headers
    body: the data that is sent to the server

const response = await fetch("/api/jokes", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
});

After a successful "POST" fetch, triggering our new POST API endpoint, we can tell useSWR to revalidate the data by calling the mutate function, so the whole process looks like this:

import useSWR from "swr";

export default function JokeForm() {
  const { mutate } = useSWR("/api/jokes");

  async function handleSubmit(event) {
    event.preventDefault();

    const formData = new FormData(event.target);
    const jokeData = Object.fromEntries(formData);

    const response = await fetch("/api/jokes", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(jokeData),
    });

    if (response.ok) {
      mutate();
    }
  }

  return (
		//...
  );
}
