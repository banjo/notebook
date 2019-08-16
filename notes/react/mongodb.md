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

## Connect backend to a database

Start with copying over the Mongoose definition to your applications `index.js` file.

```javascript
const mongoose = require("mongoose");

// DO NOT SAVE YOUR PASSWORD TO GITHUB!!
const url =
    "mongodb+srv://fullstack:sekred@cluster0-ostce.mongodb.net/note-app?retryWrites=true";

mongoose.connect(url, { useNewUrlParser: true });

const noteSchema = new mongoose.Schema({
    content: String,
    date: Date,
    important: Boolean
});

const Note = mongoose.model("Note", noteSchema);
```

Change the handler for fetching all notes to use the Mongoose database instead:

```javascript
app.get("/api/notes", (request, response) => {
    Note.find({}).then(notes => {
        response.json(notes);
    });
});
```

Just to be safe, lets turn the each objects ID to a string instead of an object, as well as removing the `__v` field, as we don't need it.

Let's modify the `toJSON`method of the object.

```javascript
noteSchema.set("toJSON", {
    transform: (document, returnedObject) => {
        returnedObject.id = returnedObject._id.toString();
        delete returnedObject._id;
        delete returnedObject.__v;
    }
});
```

After that, let's change the `GET`request to use the new JSON with a map function.

```javascript
app.get("/api/notes", (request, response) => {
    Note.find({}).then(notes => {
        response.json(notes.map(note => note.toJSON()));
    });
});
```

## Database config on its own module

It's possible to extract Mongoose onto its own module.

Create a new directory called `models` in your project folder and add a file called `note.js` to store your notes.

```javascript
const mongoose = require("mongoose");

const url = process.env.MONGODB_URI;

console.log("connecting to", url);

mongoose
    .connect(url, { useNewUrlParser: true })
    .then(result => {
        console.log("connected to MongoDB");
    })
    .catch(error => {
        console.log("error connecting to MongoDB:", error.message);
    });

const noteSchema = new mongoose.Schema({
    content: String,
    date: Date,
    important: Boolean
});

noteSchema.set("toJSON", {
    transform: (document, returnedObject) => {
        returnedObject.id = returnedObject._id.toString();
        delete returnedObject._id;
        delete returnedObject.__v;
    }
});

module.exports = mongoose.model("Note", noteSchema);
```

By using the `module.exports` command, we'll export only the note model, not anything else in the file.

To import the module in another file (e.g. `index.js`), use this following syntax:

```javascript
const Note = require("./models/note");
```

New environment variables were used in this example. We'll add environment variables to keep certain information safe. We'll use the **dotenv** module.

```bash
npm install dotenv --save
```

To use the library, we create a `.env` file in the root of the project. Define the variables inside it. Like this:

```
MONGODB_URI=mongodb+srv://fullstack:sekred@cluster0-ostce.mongodb.net/note-app?retryWrites=true
PORT=3001
```

The PORT is also stored in this file.

It's important to **add the .env file to your .gitignore file**.

At the top of your `index.js` file, import your configurations:

`require("dotenv").config()`

To use an environment variable, use `process.env.PORT` for example.

## Updateing thre rest of the backend

### Changing the POST request

```javascript
app.post("/api/notes", (request, response) => {
    const body = request.body;

    if (body.content === undefined) {
        return response.status(400).json({ error: "content missing" });
    }

    const note = new Note({
        content: body.content,
        important: body.important || false,
        date: new Date()
    });

    note.save().then(savedNote => {
        response.json(savedNote.toJSON());
    });
});
```

Notice that we are using the modified `toJSON` method to save it.

### changing GET for indivual notes

```javascript
app.get("/api/notes/:id", (request, response) => {
    Note.findById(request.params.id).then(note => {
        response.json(note.toJSON());
    });
});
```
