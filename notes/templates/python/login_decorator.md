# Login decorator

## Login Decorator in Flask
How to create a login decorator using the `session` method in Flask. Based on the CS50 finance project.

```python
def login_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if session.get("user_id") is None:
            return redirect("/login")
        return f(*args, **kwargs)
    return decorated_function
```
