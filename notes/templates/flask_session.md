# Flask-Session on Filesystem
Run a flask session locally on the server, instead of client side.

```python
# import flask and session module
from flask import Flask,...
from flask_session import Session
```

Configurations:

```python
# init flask
app = Flask(__name__)

# use filesystem instead of cookies for sessions
app.config["SESSION_FILE_DIR"] = mkdtemp()
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)
```
