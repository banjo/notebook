# Ajax Request

## Ajax Post
A basic way to send an Ajax Post request without jquery.

```js
function ajax_request() {
    var aj = new XMLHttpRequest();
    var p = document.getElementById('result');

    aj.onreadystatechange = function () {
        if (aj.readyState == 4 && aj.status == 200) {
            p.innerHTML = aj.responseText;
        }
    }

    var username = document.getElementById('username').value;

    aj.open("POST", "/_check_username", true)
    aj.setRequestHeader("Content-type", "application/x-www-form-urlencoded")
    aj.send("username=" + username)

};
```

How flask should handle it.

```python
from flask import Flask
from flask import render_template, request
app = Flask(__name__)


@app.route("/")
def index():
    return render_template("index.html")


@app.route("/_check_username", methods=["POST"])
def check():
    name = request.form["username"]
    return "Hello " + name

```
