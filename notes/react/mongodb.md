# MongoDB as a database with React

## MongoDB

MangoDB is a document database (not a relational database). Document databases are categorized under NoSQL term.
MongoDB can be used locally or on a server - we will use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

## MongoDB Atlas

To use Atlas you need to create a cluster.

-   Create account and login
-   Create a cluster. Use **AWS** and **Frankfurt** for the _free tier_.
-   Create a user at the _security_ tab. Make sure it has _read and write_ priviliges.
-   Go to _IP Whitelist_ to add approved IP adresses. `allow access from anywhere` can be chosen.
-   Connect with `Short SRV connection string`. Save the URL for later.

## Mongoose

MongoDB has an official Node.js driver, but we will use the **Mongoose** library.
Install **Mongoose** with `npm install mongoose --save`.

### Upload to server

```javascript
const mongoose = require("mongoose");

// username and password that was created in the cluster
const url = `mongodb+srv://${username}:${password}@cluster0-ostce.mongodb.net/test?retryWrites=true`;

// establish connection
mongoose.connect(url, { useNewUrlParser: true });

// create note schema for class to save in DB
const noteSchema = newmongoose.Schema({
    content: String,
    date: Date,
    important: Boolean
});

// Create note model
const Note = mongoose.model("Note", noteSchema);

// create the actual note
const note = new Note({
    content: "This is the content",
    date: new Date(),
    important: true
});

// save to database
note.save().then(response => {
    console.log("Note saved");
    mongoose.connection.close();
});
```

Data can be accessed under the **Collections** tab on the web page. If you want to change the name of what you would save, change the first argument in the URL.

`...mongodb.net/test?retryWrites=true` -> `...mongodb.net/newName?retryWrites=true`

### Fetch objects

It is possible to fetch all notes using the Note model's find method. By passing an empty object, everything will be listed.

```javascript
Note.find({}).then(result => {
    result.forEach(note => {
        console.log(note);
    });
    mongoose.connection.close();
});
```

It is possible to restrict the serach by changing the object that is passed.

```javascript
Note.find({ important: true }).then(result => {
    // ...
});
```
