What is, and why do we use Mongoose

In order to access a MongoDB from your app, we'll need a JavaScript API, this is sometimes called a database driver (imagine it like your printer drive).

We will use a library called mongoose, which is an ODM (Object Document Mapper).

Difference between ORM and ODM

ORM - Object Relation Mapping
    Technique to perform CRUD operations to mainly relational databases (MySQL, PostgreSQL, etc.)
    Uses an object-oriented paradigm
    Like an excel spreadsheet, has rows and columns, you can't add a field to one entry that doesn't exist for all of them.
    Is mapped to a single object for all entries.

ODM - Object Document Mapping
    Like ORM, but for non-relational databases (MongoDB)
    Uses a document-oriented paradigm

Reasons to use mongoose as ODM
    It helps in building a schema and querying the database (it's also our db driver)
    It has to run on the server, because database access is not secure in browser.
        We already have a server (Next.js API routes)

DB Connect

In order to read data from a database and consume it in our app, we need:

    A database with documents

    A connection between this database and the Next.js app (with mongoose)

To create a connection, follow these steps:


    install mongoose with npm install mongoose

    create a .env.local file at the root of your project with the following content: MONGODB_URI=mongodb+srv://<user>:<password>@<cluster-name>/jokes-database?retryWrites=true&w=majority

        Files called .env contain environment variables: secrets like usernames and passwords you don't want to share with anybody.

        These files should be ignored by git inside of the .gitignore file.

        Note the structure of the content: the variable is called MONGODB_URI and has the value MONGODB_URI=mongodb+srv://<user>:<password>@<cluster-name>/jokes-database?retryWrites=true&w=majority.

            user is the name of the database user you have created in the MongoDB Atlas interface.
            password is the password you have chosen for this user.

            cluster-name is the name of your cluster: this value can vary and will look something like cluster0.mu12zrz.mongodb.net.

            jokes-database is the name of your database.
            Replace the placeholders, including the < and > characters, with the actual values.

    create a db/connect.js file and copy the content from the Next.js mongoose example

        Note that this file uses the MONGODB_URI we have just set up in .env.local to create a connection.

        No need to change anything here.

Schema and Models

We need to declare a Schema that describes the data type of the documents in a collection.

The schema creates a model that we can use to interact with the database.

Note the difference between Schema and Model

    the schema describes the structure of a document

    the model gives us a programming interface for interacting with the database.

Writing a Schema

We write a schema in the corresponding file in the db/model folder, as in this example below:

When creating a new Schema, we pass an object with the key-value-pairs we want our documents to have, like joke which is a String and required.

We don't need to define the id because mongoose will automatically create one.

Export the Schema to make it available in our application.

// db/models/Joke.js
import mongoose from "mongoose";

const { Schema } = mongoose;

const jokeSchema = new Schema({
  joke: { type: String, required: true },
});

const Joke = mongoose.models.Joke || mongoose.model("Joke", jokeSchema);

export default Joke;

Further notes:

the name of the collection the model work on is generated from the models name, in the case of this example "Joke" => "jokes"

You can call the mongoose.model method with a third argument that holds the collection name.

We have to check whether the model with the name "Joke" has already been compiled and if so, use the already compiled model. Hence the logical operator (||)

Using the Model: Querying the DB (.find, .findByld)

In our Next.js API Route we can now write a request handler which

    Connects to the database with dbConnect(),
    Uses the Model to search a document, and
    Returns the data

// api/jokes/index.js
import dbConnect from "../../../db/connect";
import Joke from "../../../db/models/Joke";

export default async function handler(request, response) {
  await dbConnect();

  if (request.method === "GET") {
    const jokes = await Joke.find();
    return response.status(200).json(jokes);
  } else {
    return response.status(405).json({ message: "Method not allowed" });
  }
}

Mongoose has a built in .findById() that can be used in a dynamic route:

// api/jokes/[id].js
import dbConnect from "../../../db/connect";
import Joke from "../../../db/models/Joke";

export default async function handler(request, response) {
  await dbConnect();
  const { id } = request.query;

  if (request.method === "GET") {
    const joke = await Joke.findById(id);

    if (!joke) {
      return response.status(404).json({ status: "Not Found" });
    }

    response.status(200).json(joke);
  }
}

Note that MongoDB returns an _id instead of id, so you might need to adapt your frontend accordingly.

Gathering linked collections with .populate()

Imagine your MongoDB has two collections: jokes and comments on these jokes. They are linked with commentIds

When reading the jokes, you want to get the comments as well. You can easily achieve this by linking both schemas and then adding .populate () when querying the database, in an example of method chaining.

First link the schemas for Joke and Comment:

// link the schemas
const jokeSchema = new Schema({
  joke: { type: String, required: true },
  comments: { type: [Schema.Types.ObjectId], ref: "Comment" },
});

const commentSchema = new Schema({
  _id: Schema.Types.ObjectId,
  comment: { type: String, required: true },
  author: { type: String, required: true },
});

const Joke = mongoose.models.Joke || mongoose.model("Joke", jokeSchema);
const Comment =
  mongoose.models.Comment || mongoose.model("Comment", commentSchema);

Then when reading the database, populate the comments:

const joke = await Joke.findById(id).populate("comments");