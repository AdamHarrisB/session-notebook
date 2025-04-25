Introduction: Databases

What is a Database?

A server:
    Is a program running 24/7 to provide services to other computers or devices. It's in the name, server.
    Can host a variety of services: an email server, a file server, web server, or a DATABASE server.
    Can serve data, as in our case, from a data.js file, using Next.js API routes.

So a DATABASE server:
    Is a program specifically designed to host and manage a database.
    Manages the data stored in the database.
    Ensures that it is available to users and applications that need to access it.
    Has persistent storage.

Relational vs. Non-relational Databases

There are some differences between relational and non-relational databases (SQL vs NoSQL):

Relational:
    Data is stored in tables, like excel
    The tables are connected to each other
    Has constraint: we decide what to do with a column if not all entries have data

Non-Relational:
    Data is stored in JSON-like structures
    Data is stored in key/value pairs
    Each data set in the database can have unique keys

MongoDB

A non-relational database, MongoDB is less strict, and easier to use.

MongoDB Terminology

Database
    A MongoDB database is a collection of data organized and stored in a specifc way, using their database management system
    A MongoDB database can have multiply sets of data called collections

Collection
    A collection is a grouping of MongoDB entries, called documents
    A collection is equivalent to a table in a relational database.
    A collection exists within a single database.

Document
    A MongoDB document is a JSON-like data structure that consists of key-value pairs.
    These key-value pairs are called fields
    Documents can have different fields

Field
    As mentioned above, in MongoDB, a field is a key pair value, stored in a document
    The field key is a string that identifies the field, and the field value is data stored in the field

Database Design

General Guidance
    Design your collections and documents around the data you need to store, and the queries you need to perform.
    Use arrays to store lists of related data within a single document.
    Try to avoid deeply nested data structures. If your documents are too complex, try to split them into multiple collections and connect the data with references.
    If you want to reference an object that's stored in a different collection (group of entries) you can use what is called foreign keys:
        If you have a users collection, and a jokes collection, you can use a foreign key in the jokes collection to store a reference to the user who created each joke.
        This allows you to store information about the user who created each joke, without duplicating data in the jokes collection.

Database Relationships

There are three different relationships between documents (JSON-like data structure holding pair of key-values)

One-To-One
    One document in one collection is exactly related to one document in another collection
    This is implementated by storing a reference to the related document in either of the two collections. The direction (where) does not matter. This type of relationship only makes sense in certain circumstances. Usually simplifying is better.

One-To-Many
    One document in a collection is related to multiple documents in another collection.
    The reference should be stored in the many collection documents.

Many-To-Many
    Multiple documents in one collection are related to multiple documents in another
    Often achieved with an intermediary collection, the documents of which reference the connected collections as several one to many relationships.

Example Visualisation

The following three collections are visualisations for best practices of the the relationships mentioned above.

// Jokes collection:
{
  "_id": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "joke": "Why do programmers hate nature? It has too many bugs.",
}

// Users collection:
{
  "_id": ObjectId("user1ID"),
  "username": "jane.doe",
  "email": "jane.doe@example.com",
}

// Comments collection:
{
  "_id": ObjectId("comment1ID"),
  "jokeId": ObjectId("joke1ID"),
  "userId": ObjectId("user1ID"),
  "comment": "That's a good one!"
}

For the above:
    Each document in the collections has an _id field, which is unique.
    Each joke document has a joke filed that stores the text of a joke, and a userId field that stores the ID of the user who created the joke. This establishes a one-to-many relationship between the joke and the user collection. A user can make many jokes.
    Each user document has a username field that stores the user's username and an email field that stores the user's email address.
    Each comment has a jokeId field that stores the ID of the joke that the comment is associated with, a userId field that stores the ID of the user, who created the comment, and a comment field that stores the text of the comment.
    The jokeId field and userId field implement one to many relationships between the comments jokes and users collections as a joke can have multiple comments, and a user can create multiple comments, but each comment can only have one joke or user.

MongoDB Atlas Introduction
    We want our app to be accessible from the internet, so we need to make our database accessible from the internet.
    External providers host our database, and MongoDB Atlas is a cloud provider for Mongo databases that does just that.