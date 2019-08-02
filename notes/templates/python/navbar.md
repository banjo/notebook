# Navbar using Jinja

## Navbar Jinja
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

`session`has a user ID stored in the variable `session.user_id`. This is only accesible when the user has signed in. Therefore, the navbar under `{% if session.user_id %}` is only available when signed in. Else, another navbar is available.
