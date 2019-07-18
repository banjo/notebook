# Ajax request with jQuery

## jQuery basic GET request
A simple GET request using jQuery.

```js
function check_username() {
    var username = document.getElementById("user_input").value;
    var label = document.getElementById("username_status");
    $.get("/check", {username: username}, function (data) {
        if (data == true) {
            label.innerHTML = "Username available";
        } else {
            label.innerHTML = "Username taken";
            event.preventDefault();
        }
    })
}
```
The GET request happens in: `$.get()` followed by the link. In this case it sends a username as an argument to `/check`. The full query looks like: `/check?username=exampleusername`.

A function is created that takes the returned data as a variable. If the response was `true`, it changes a label on the document.
