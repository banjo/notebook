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
  - [Catch requests to non-existing routes](#catch-requests-to-non-existing-routes)
  - [CORS - communicate between ports](#cors---communicate-between-ports)
- [Deploying to internet](#deploying-to-internet)
  - [Only backend](#only-backend)
  - [Frontend as production build with backend](#frontend-as-production-build-with-backend)
    - [Use the build with the backend](#use-the-build-with-the-backend)
    - [Simplify deploying with scripts](#simplify-deploying-with-scripts)
    - [Backend URLs](#backend-urls)
    - [Proxy](#proxy)

# Initiate directory

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

# Nodemon

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

# Express

## Basic configurations

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

## Fetching a single resource

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

## Deleting resources

Almost same as above, how to delete a single resource.

```javascript
app.delete("/notes/:id", (request, response) => {
    const id = Number(request.params.id);
    notes = notes.filter(note => note.id !== id);

    response.status(204).end();
});
```

## Receiving data

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

# REST Client

Use the REST Client plugin in Visual Studio Code to test your HTTP requests.

1. Create a file with `.rest` extension in the working directory, in a folder called `requests`.
2. Write the request you want to try in the follow format: `get http://localhost:3001/notes`.
3. Test it by pressing **Send Request**.

# Using middleware


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
## Catch requests to non-existing routes

A middleware can be used to catch request to non-existing routes.

```javascript
const unknownEndpoint = (req, res) => {
    res.status(404).send({ error: "unknown endpoint" });
};
```

---
## CORS - communicate between ports
By default, apps cannot communicate on different ports (e.g :3000 and :3001) unless you use the CORS middleware. CORS is not limited to node or react - it's an universal principle.

Install cors with the command `npm install cors --save`.

Allow requests from all origins with the following code:

```javascript
const cors = require('cors')

app.use(cors())
```

# Deploying to internet

## Only backend

This part shows how to deploy your application to __Heroku__.

1. Add a *Procfile* to the project root with the following content.
```javascript
web: node index.js
```
<br>

2. Change the port of the application at *index.js*.
```javascript
const PORT = process.env.PORT || 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
})
```
This will use the environment variable for PORT, or 3001 if there is none.

<br>

3. Add `node_modules` to *.gitignore*.
4. Create an Heroku app and push to Heroku. You need have a git repositry with the latest changes commited.
```bash
$ heroku login

$ heroku create

$ git push heroku master
```

## Frontend as production build with backend
React code is often running in *development mode*. When we are going to deploy, the best would be to create a *production build*.

A React app created with `create-react-app` can be built with `npm run build`.

If you run this in your frontend, you create a directory called *build*, which contains the *.html* and a minified version of the JS code in a folder called *static*.

### Use the build with the backend
One option for deploying is copying the *build* folder to the root directory of the backend. `cp -r {source} {dest}` can be used to copy in bash.

To make express show static content, we need to add a built-in middleware from express called **static**.

```javascript
app.use(express.statis('build'))
```

whenever express gets a HTTP GET-request it will first check if the build directory contains a file corresponding to the requests address. If a correct file is found, express will return it.

___

In most cases, the same adress goes for the backend as well as the frontend. E.g. `www.sameforbackendandfrontend.com`. This means we can change all URLs in the frontend to **relative** URLs.

```javascript
import axios from 'axios'
const baseUrl = '/notes' // instead of https://localhost:3001/notes

const getAll = () => {
  const request = axios.get(baseUrl)
  return request.then(response => response.data)
}

```

###  Simplify deploying with scripts
It's easy to add scripts that will make it easier to maintain and deploy your code. Add these scripts to your *backend* `package.json`.

```javascript
{
  "scripts": {
    "build:ui": `rm -rf build && cd ${path-to-frontend} && npm run build --prod && cp -r build ${path-to-backend}`,
    "deploy": "git push heroku master",
    "deploy:full": "npm run build:ui && git add . && git commit -m uibuild && git push && npm run deploy",
    "logs:prod": "heroku logs --tail"
  }
}
```

* `npm run build:ui` removes the earlier version, builds the frontend the copies the build folder to the backend.
* `npm run deploy` releases the backend to to heroku.
* `npm run deploy:full` combines both and adds git to update and deploy it.
* `npm logs:prod` shows the heroku logs.

### Backend URLs
As both the frontend and backend are using the same URLs, it might be smart to update them.

Change all **backend** routes by hand, to add `/api/`. Like this:`/notes` -> `/api/notes`
```javascript
app.get('/api/notes', (request, response) => {
  response.json(notes)
})
```

**Frontend** code usually only needs this change:
```javascript
import axios from 'axios'
const baseUrl = '/api/notes' // change the variable

const getAll = () => {
  const request = axios.get(baseUrl)
  return request.then(response => response.data)
}
```

### Proxy
Changes on the frontend have caused it to no longer work in development mode (when started with command npm start), as the connection to the backend does not work. This is due to changes the adresses to *relative* ones.

This is simple to solve with a proxy. If the **backend** is at *localhost:3001*, add that to the `package.json`, `proxy` part.

```javascript
{
  "dependencies": {
    // ...
  },
  "scripts": {
    // ...
  },
  "proxy": "http://localhost:3001"
}
```
