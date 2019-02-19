# Frontend

## HTML Basics
- [Standard layout](#standard-layout)
- [Paragraph](#paragraph)
- [Image](#image)
- [Anchor elements](#anchor-elements)
  * [Standard element in new tab](#standard-element-in-new-tab)
  * [Internal anchor element](#internal-anchor-element)
  * [Anchor element with picture](#anchor-element-with-picture)
- [Unordered list](#unordered-list)
- [Ordered list](#ordered-list)
- [Input elements](#input-elements)
  * [Text box](#text-box)
  * [Input elements within form](#input-elements-within-form)
- [Div element](#div-element)

## Standard layout
```html
<!DOCTYPE html>
<html>
  <head>
    <!-- metadata elements -->
  </head>
  <body>
    <!-- page contents -->
  </body>
</html>
```

## Paragraph
```html
<p> normal text within a paragraph </p>
```

## Image
```html
<img src="html source here" alt="text here">
```

## Anchor elements

### Standard element in new tab
```html
<a href="www.google.se" target="_blank">text here</a>
```

### Internal anchor element
First the text that is the anchor element.
```html
<a href="#footer"> Jump to bottom </a>
```
And also, the ID of what it will go to.
```html
<footer id="footer"> footer here </footer>
```

### Anchor element with picture
```html
<a href="www.google.se"><img src="www.google.se/logo.png" alt="Google logo"></a>
```

## Unordered list
```html
<ul>
  <li> One thing </li>
  <li> Two tings </li>
  <li> Three things </li>
</ul>
```

## Ordered list
```html
<p>Top 3 things cats hate:</p>
<ol>
  <li> Hello </li>
  <li> Hello </li>
  <li> Hello </li>
</ol>
```

## Input elements

### Text box
```html
<input type="text" placeholder="Placeholder text"> 
```

### Input elements within form
A label created for each input element. Those with same name are connected to each other. 
Checked means that it is already checked.

```html
<form id="cat-photo-app" action="/submit-cat-photo">
    <label><input type="radio" name="indoor-outdoor" checked> Indoor</label>
    <label><input type="radio" name="indoor-outdoor"> Outdoor</label><br>
    <label><input type="checkbox" name="personality" checked> Loving</label>
    <label><input type="checkbox" name="personality"> Lazy</label>
    <label><input type="checkbox" name="personality"> Energetic</label><br>
    <input type="text" placeholder="cat photo URL" required>
    <button type="submit">Submit</button>
  </form>

```

## Div element
Usually you place stuff in div elements.
```html
<div>
  <ul>
    <li></li>
  </ul>
</div>
```




