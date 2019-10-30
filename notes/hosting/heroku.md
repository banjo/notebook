# Deploy React + Express to Heroku

### 1. Add endpoint for `index.html` file in Express

Be sure that it points to the correct `dist`/`build` folder.
```javascript
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, '../../dist/index.html'));
});
```

### 2. Add proxy to localhost

If your server, for example, listens to port `5000`, make the proxy listen to that port.

**Express**:
```javascript
server.listen(process.env.PORT || 5000, () => {
  console.log(`Server running on port ${process.env.PORT || 5000}`);
});
```

**package.json**:
```javascript
"proxy": "http://localhost:5000"
```

### 3. Add scripts

These are the important scripts:

```javascript
"scripts": {
        "build": "webpack --mode production",
        "start": "node src/server/index.js",
        "heroku-postbuild": "npm install && npm run build"
```

### 4. Deploy to Heroku
```bash
# remove git build (optional)
$ rm -rf .git

# make new git config
$ git init
$ git add .
$ git commit -m "Initial commit"

# create heroku server
$ heroku create

# add environment variables (optional)
$ heroku config:set VAR1=variable1

# push to server
$ git push heroku master
```

If you already have a server and need to add that remote instead of creating a new one:
```bash
$ heroku git:remote -a <name-of-server>
```
