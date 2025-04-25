Update

To update an entry in your database, you need to:

    Define a PUT API route
    Connect the submit handler of an edit form to this API route

Update with Mongoose

First, define a PUT API route:

// /api/jokes/[id].js
if (request.method === "PUT") {
  const jokeData = request.body;
  // Get the joke data from the request body
  await Joke.findByIdAndUpdate(id, jokeData);
  // Find the joke by its ID and update the joke using its ID and the new data.
  return response.status(200).json({ status: `Joke ${id} updated!` });
  // Return an OK status on successful update
}

PUT using fetch

Next we tell the submit handler to:

    use the put API route.
    wait for the database to respond and update the UI
    navigate the user to a different page via push

*PUT and PATCH are semantically different, according to conventionm, we would use PUT to update our entire document, and patch to update individual fields. In our demo, we're using PUT, simply because we only ever have ONE field to update.

Go to the page or component where you want to write the submit handler of your edit form. We need the mutate method to update the component after a successful update:

// /components/Joke/index.js
export default function Joke() {
  //...
  const { data, isLoading, mutate } = useSWR(`/api/jokes/${id}`);

  async function handleEdit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const jokeData = Object.fromEntries(formData);

    const response = await fetch(`/api/jokes/${id}`, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(jokeData),
    });

    if (response.ok) {
      mutate();
    }
  }
  return; //...
}

Delete

To delete an entry in your database:

    Define a delete an API route
    Connect a handler function which uses this API route.

Delete with Mongoose

First, define a DELETE API route:

if (request.method === "DELETE") {
  await Joke.findByIdAndDelete(id);
  // Find and delete the joke by its ID.
  response.status(200).json({ status: `Joke ${id} successfully deleted.` });
  // Confirm deletion with a status message.
}

DELETE using fetch

We write a handler function which calls fetch() with the appropriate arguments and pass it to a delete button:

// /components/Joke/index.js

  async function handleDelete() {
    const response = await fetch(`/api/jokes/${id}`, {
      method: "DELETE",
    });
    // Send a DELETE request to the server for a specific joke.
    if (response.ok) {
      // If the response is successful redirect to the home page
      router.push("/");
    }
  }

return (
  <button type="button" onClick={handleDelete}>
    Delete
  </button>
);

We don't want to use mutate with DELETE requests, since the delete data cannot be refetched and a revalidation would result in an error.
