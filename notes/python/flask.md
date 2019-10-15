# Flask templates and instructions

## Flask

### Template
A basic Flask layout:

```python
from flask import Flask
from flask import render_template, request
app = Flask(__name__)


@app.route("/")
def index():
    return render_template("index.html")

```

### Session locally
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

### Login decorator
Login decorator for endpoints in Flask. Login based on Session required to access page.

```python
def login_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if session.get("user_id") is None:
            return redirect("/login")
        return f(*args, **kwargs)
    return decorated_function
```


## Jinja

### Template
Full template will links to Boostrap, style.css and jQuery.


```html
<!doctype html>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='styles/style.css')}}">
    <script type="text/javascript" src="{{ url_for('static', filename='username.js')}}"></script>

    {% block head %}{% endblock %}
</head>

<body>
    {% block main %}{% endblock %}

    <!-- Optional JavaScript -->

    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"
        integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous">
    </script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"
        integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous">
    </script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"
        integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous">
    </script>
</body>

</html>

```

Create a new HTML page with this:

```html
{% extends "layout.html" %}

{% block head %}
{% endblock %}

{% block main %}
{% endblock %}
```

### Local links

* CSS Files
  * `<link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='styles/style.css')}}">`
* JS Files
  * `<script type="text/javascript" src="{{ url_for('static', filename='main.js')}}"></script>`

### Navbar
The logic in how to use a navbar with a login module, using the `session` method in Flask. Based on CS50 finance project.

```html
<div class="collapse navbar-collapse" id="navbar">
{% if session.user_id %}
<ul class="navbar-nav mr-auto mt-2">
    <li class="nav-item"><a class="nav-link" href="/quote">Quote</a></li>
    <li class="nav-item"><a class="nav-link" href="/buy">Buy</a></li>
    <li class="nav-item"><a class="nav-link" href="/sell">Sell</a></li>
    <li class="nav-item"><a class="nav-link" href="/history">History</a></li>
    <li class="nav-item"><a class="nav-link" href="/change_password">Change Password</a></li>
</ul>
<ul class="navbar-nav ml-auto mt-2">
    <li class="nav-item"><a class="nav-link" href="/logout">Log Out</a></li>
</ul>
{% else %}
<ul class="navbar-nav ml-auto mt-2">
    <li class="nav-item"><a class="nav-link" href="/register">Register</a></li>
    <li class="nav-item"><a class="nav-link" href="/login">Log In</a></li>
</ul>
{% endif %}
</div>
```
