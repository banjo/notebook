# React backend using Express

Basic initiation of a backend server using Express and node.js. From Fullstack Open by Helsinki University.

- [React backend using Express](#react-backend-using-express)
  - [Initiate directory](#initiate-directory)
  - [Nodemon](#nodemon)
  - [Express](#express)
    - [Basic configurations](#basic-configurations)
    - [Fetching a single resource](#fetching-a-single-resource)
    - [Deleting resources](#deleting-resources)
    - [Receiving data](#receiving-data)
  - [REST Client](#rest-client)
  - [Using middleware](#using-middleware)

## Initiate directory

1. Navigate to directory and use `npm init` to initiate the folder.
2. Edit `package.json` to something like this.

```javascript
{
  "name": "backend",
  "version": "0.0.1",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Anton Ödman"
}
```

3. Add `start` script to `package.json`. This will allow project to be started with `npm start`.

```javascript
{
  // ...
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  // ...
}
```

4. Install Express and add to `package.json` with `npm install express --save`. The following will be added to the file:

```javascript
{
  // ...
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

5. (Update with `npm update` and install on new computer with `npm install`)

## Nodemon

Install nodemon to automatically restart the web server on changes.

1. Install and add to developer dependencies with `npm install --save-dev nodemon`.

```javascript
{
  //...
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^1.19.1"
  }
}
```

2. Add running script to `scripts` in `package.json`.

```javascript
{
  // ..
  "scripts": {
    "start": "node index.js",
    "watch": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  // ..
}
```

3. Run with `npm run watch`

## Express

### Basic configurations

A basic application looks like this.

```javascript
const express = require('express')
const app = express()

let notes = [
  ...
]

app.get('/', (req, res) => {
  res.send('<h1>Hello World!</h1>')
})

app.get('/notes', (req, res) => {
  res.json(notes)
})

const PORT = 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
})
```

### Fetching a single resource

In this case, fetch one of the notes in the `notes` array. Returns `404` if nothing is found.

```javascript
app.get("/notes/:id", (request, response) => {
    const id = Number(request.params.id);
    const note = notes.find(note => note.id === id);

    if (note) {
        response.json(note);
    } else {
        response.status(404).end();
    }
});
```

### Deleting resources

Almost same as above, how to delete a single resource.

```javascript
app.delete("/notes/:id", (request, response) => {
    const id = Number(request.params.id);
    notes = notes.filter(note => note.id !== id);

    response.status(204).end();
});
```

### Receiving data

To easily access data, we need the `body-parser` library. The example below will use it to get the contect of a `POST` request. Then, we will either return `400` if the content is missing, or create a new note and store it in the `notes` array.

```javascript
const express = require("express");
const app = express();
const bodyParser = require("body-parser");

app.use(bodyParser.json());

//...

app.post("/notes", (request, response) => {
    const note = request.body;
    if (!body.content) {
        return response.status(400).json({
            error: "content missing"
        });
    }

    const note = {
        content: body.content,
        important: body.important || false,
        date: new Date(),
        id: generateId()
    };

    notes = notes.concat(note);

    response.json(note);
});
```

The generateId function is a simple one used to get the max id of the current `notes` array and return it with an increment of 1.

```javascript
const generateId = () => {
    const maxId = notes.length > 0 ? Math.max(...notes.map(n => n.id)) : 0;
    return maxId + 1;
};
```

## REST Client

Use the REST Client plugin in Visual Studio Code to test your HTTP requests.

1. Create a file with `.rest` extension in the working directory, in a folder called `requests`.
2. Write the request you want to try in the follow format: `get http://localhost:3001/notes`.
3. Test it by pressing **Send Request**.

## Using middleware

the `body-parser` that was used previously is a **middleware**. They are used for `request` and `response` objects. You can use several at the same time. They are executed in the order they were takin into express.

Implement your own middleware like this:

```javascript
const requestLogger = (request, response, next) => {
    console.log("Method:", request.method);
    console.log("Path:  ", request.path);
    console.log("Body:  ", request.body);
    console.log("---");
    next();
};
```

Activate it like this with the `app.use(requestLogger)` keyword.

---

A middleware can be used to catch request to non-existsing routes.

```javascript
const unknownEndpoint = (req, res) => {
    res.status(404).send({ error: "unknown endpoint" });
};
```

---
By default, apps cannot communicate on different ports (e.g :3000 and :3001) unless you use the CORS middleware. CORS is not limited to node or react - it's an universal principle.

Install cors with the command `npm install cors --save`.

Allow requests from all origins with the following code:

```javascript
const cors = require('cors')

app.use(cors())
```
