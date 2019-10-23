# CSS Tips

## Center vertically and horizontally
Use this snippet to center a div on the middle of the screen.

```css
div {
	position: absolute;
    left: 50%;
    top: 50%;
    margin: -100px 0 0 -150px;
}
```

## Prevent breaking dimensions
Prevents breaking box dimensions with margin, padding or borders.
```css
* {
  box-sizing: border-box;
}
```

## Button and link transition
Make a nice transition for buttons and links when hovering over them. Use a color that matches the background.

### Button
```css
.button:hover {
	background: rgba(200, 0, 0, 1);
	transition: background 0.2s ease-in-out;
}
```

### Link
```css
.link:hover {
	transition: all 0.2s ease-in-out;
	border-color: yellow;
}
```

## CSS Hack - color all margins, paddings and borders
Use when working with layout. You'll see the depths of the page. Margin and padding. You could easiliy identify inconsistencies.
Its possible to use it as a bookmark with [this](https://gist.github.com/vcastroi/e0d296171842e74ad7d4eef7daf15df6) guide. Updated fork [here](https://gist.github.com/olee/50f0ddac55418f705e0c5759e15e946d).
```css
* { background-color: rgba(255,0,0,.2); }
* * { background-color: rgba(0,255,0,.2); }
* * * { background-color: rgba(0,0,255,.2); }
* * * * { background-color: rgba(255,0,255,.2); }
* * * * * { background-color: rgba(0,255,255,.2); }
* * * * * * { background-color: rgba(255,255,0,.2); }
* * * * * * * { background-color: rgba(255,0,0,.2); }
* * * * * * * * { background-color: rgba(0,255,0,.2); }
* * * * * * * * * { background-color: rgba(0,0,255,.2); }
```

Another quicker variant that also works:

```css
html * {
    background: rgba(255, 0, 0, .1);
    box-shadow: 0 0 0 1px red;
}
```
## Show button when text
Show only the `submit` button when there is text.

```css
button {
    display: none;
}

input:not(:placeholder-shown) + button {
    display: block;
}
```
