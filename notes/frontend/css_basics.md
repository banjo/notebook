# Frontend

## CSS Basics
- [Inline editing: change color](#inline-editing--change-color)
- [Style block](#style-block)
- [Stylize classes](#stylize-classes)
- [Stylize headers](#stylize-headers)
- [Import font from Google](#import-font-from-google)
- [Multiple classes](#multiple-classes)
- [Stylize ID](#stylize-id)
- [Stylize type](#stylize-type)
- [Colors](#colors)
  * [RGB](#rgb)
  * [Hex](#hex)
  * [By color](#by-color)
- [CSS variables](#css-variables)
  * [Root](#root)
  * [Fallback value](#fallback-value)

## Inline editing: change color

```h
<h2 style="color: blue;">Other color on heading</h2>
```

## Style block
Best way to use CSS is with a style block.

```h
<style>
  h2 {color: blue;}
</style>
```

## Stylize classes
Create a class to use on different elements.
```h
<style>
  .red-text {
    color: red;
  }
</style>
```

Use it on an element.
```h
<h2 class="red-text">CatPhotoApp</h2>
```

## Stylize headers
Change to font and size of all H2. Use Helvetica if possible, else use sans-serif.
```h
h2 {
  font-family: Helvetica, sans-serif;
  font-size: 16px;
}
```

## Import font from Google
Import font from google to use on webpage. Do before style segment.
```h
<link href="https://fonts.googleapis.com/css?family=Lobster" rel="stylesheet" type="text/css">
```

## Multiple classes
Create multiple classes for a single element. Separate with space.
```h
<style>
  .smaller-image {
    width: 100px;
  }
  
  .thick-green-border{
    border-color: green;
    border-width: 5px;
    border-style: solid;
    border-radius: 10px (or 50%); 
  }
</style>
```
Apply it to an element. This case a picture. 
```h
<a href="#"><img class="smaller-image thick-green-border" src="https://bit.ly/fcc-relaxing-cat" alt="A cute orange cat lying on its back."></a>
```

## Stylize ID
Create a certain style. An ID should only be applied to ONE element.
```h
<style>
  #cat-photo-element {
    background-color: green;
  }
</style>
```
Apply it to the element with the id-tag.
```h
<a href="#"><img id="cat-photo-element" src="https://bit.ly/fcc-relaxing-cat" alt="A cute orange cat lying on its back."></a>
```

## Stylize type
Create a style for a certain type of an ojbect. This case for a checkboc of type radio.
```h
<style>
  [type="radio"]{
    margin-top: 10px;
    margin-bottom: 15px;
  }
</style>
```

## Colors
You can choose colors with hex, RGB, normal colors or variables.
### RGB
```h
background-color: rgb(255, 165, 0);
```
### Hex
```h
background-color: #00FF00;
```

### By color
```h
background-color: black;
```

## CSS variables
It is possible to use variables in CSS. A variable called variable skin.
```h
--penguin-skin: blue;
```

Use it like this;
```h
.penguin-top {
  background: var(--penguin-skin);
}
```

### Root
Declare the variables in the root to use them in the whole document. The root should be at the top.
```h
<style>
  :root {
    --penguin-skin: black;
  }
</style>
```

### Fallback value
It is still possible to use a fallback value in variables. 
```h
background: var(--penguin-skin, black);
```
