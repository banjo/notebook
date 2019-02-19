# Frontend

## CSS Basics
- [Frontend](#frontend)
  * [CSS Basics](#css-basics)
  * [Inline editing: change color](#inline-editing--change-color)
  * [Style block](#style-block)
  * [Stylize classes](#stylize-classes)
  * [Stylize headers](#stylize-headers)
  * [Import font from Google](#import-font-from-google)
  * [Multiple classes](#multiple-classes)
  * [Stylize ID](#stylize-id)
  * [Stylize type](#stylize-type)
  * [Colors](#colors)
    + [RGB](#rgb)
    + [Hex](#hex)
    + [By color](#by-color)
  * [CSS variables](#css-variables)
    + [Root](#root)
    + [Fallback value](#fallback-value)
  * [CSS Padding and margin](#css-padding-and-margin)
    + [Example](#example)
    + [Information](#information)
  * [Psuedo classes](#psuedo-classes)
    + [Hover class](#hover-class)
    + [Psuedo to connect elements](#psuedo-to-connect-elements)
  * [Positioning](#positioning)
    + [Relative position](#relative-position)
    + [Absolute position](#absolute-position)
    + [Fixed position](#fixed-position)
    + [Transform](#transform)
  * [Animation](#animation)
    + [Basic animation](#basic-animation)
    + [Animate hover](#animate-hover)
      - [Without Fill Mode](#without-fill-mode)
      - [With Fill Mode](#with-fill-mode)
    + [Movement with CSS](#movement-with-css)
    + [Loop Animations](#loop-animations)
    + [Animation Timing](#animation-timing)
    + [Cubic Bezier](#cubic-bezier)


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

## CSS Padding and margin

### Example

```h
<style>
  .injected-text {
    margin-bottom: -25px;
    text-align: center;
  }
  .box {
    border-style: solid;
    border-color: black;
    border-width: 5px;
    text-align: center;
  }
  .yellow-box {
    background-color: yellow;
    padding: 10px;
  }
  
  .red-box {
    background-color: crimson;
    color: #fff;
    padding: 20px;
    margin-top: 40px;
    margin-right: 20px;
    margin-bottom: 20px;
    margin-left: 40px;
  }
  .blue-box {
    background-color: blue;
    color: #fff;
    padding: 20px 40px 20px 40px;
    margin: 20px;
  }
</style>
```

Place on the website like this:
```h
<h5 class="injected-text">margin</h5>

<div class="box yellow-box">
  <h5 class="box red-box">padding</h5>
  <h5 class="box blue-box">padding</h5>
</div>
```


### Information
Padding is within, margin is outside. 

![](https://i.stack.imgur.com/UHD7W.gif)


## Psuedo classes
Use psudo classes to access specific parts of an element.

### Hover class
This class gets activated when the mouse hovers over said element.
The object is black from the beginning, and turns blue when hovered over.

```h
<style>
  a {
    color: #000;
  }
  
  a:hover {
    color: blue;
  } 
</style>
```

### Psuedo to connect elements
Psuedo is used to connect elements together as well.

```h
  .heart {
    position: absolute;
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: pink;
    height: 50px;
    width: 50px;
    transform: rotate(-45deg);
    animation-name: beat;
    animation-duration: 1s;
    animation-iteration-count: infinite;
    
  }
  .heart:after {
    background-color: pink;
    content: "";
    border-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: 0px;
    left: 25px;
  }
  .heart:before {
    background-color: pink;
    content: "";
    border-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: -25px;
    left: 0px;
  }
```
In this case; whenever the animation name "beat" is accessed, all of heart is accessed. Normal, after and before.

## Positioning

There are several different ways to position elements in CSS.

![](https://image.slidesharecdn.com/positionanditsvalues-170702045148/95/css-position-and-its-values-1-638.jpg?cb=1498971289)

### Relative position
This example is 15 px from the top

```h
<style>
  h2 {
    position: relative;
    top: 15px; 
  }
</style>
```

### Absolute position
Position to other elements
```h
<style>
  #searchbar {
    position: absolute;
    top: 50px;
    right: 50px
  }
</style>
```

### Fixed position
Fixed. Won't move when scroll.
```h
<style>
  #navbar {
    position: fixed;
    top: 0px;
    left: 0px;
</style>
```

### Transform
Example on how to transform an object. Scale makes the object scale up to 150% its size. You can also use a function to transform to object. No animation is done - it loads to that size from the beginning.

```h
transform: scale(1.5);
transform: function(variable);
```

## Animation
Animations are used to make objects move. Its based on **@Keyframes**. 

### Basic animation
The animation is in this case connected to an ID. The name is **colorful** and the duration is 3 seconds.
Once the ID is done - the keyframe connected to the name **colorful** is created.

The keyframe uses 0-100% to choose order. 0 first and 100 last. 

```h
#anim {
  animation-name: colorful;
  animation-duration: 3s;
}

@keyframes colorful {
  0% {
    background-color: blue;
  }
  100% {
    background-color: yellow;
  }
}
```

### Animate hover

#### Without Fill Mode
It's possible to animate only objects that are hovered upon using psuedo classes.
In this case: all pictures that are hovered upon changes size. There is however one problem: the animation keeps on moving again and again. 

```h
<style>
  img:hover {
    animation-name: width;
    animation-duration: 500ms;
  }
  
  @keyframes width {
    100% {
      width: 40px;
    }
  }
</style>


<img src="https://bit.ly/smallgooglelogo" alt="Google's Logo" />
```

#### With Fill Mode
If you want the animation to stay that way while still hovering over the element, you need to use the `animation-fill-mode` and set it to `forwards;`. The full code should look something like this:

```h
<style>
  button {
    border-radius: 5px;
    color: white;
    background-color: #0F5897;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    animation-name: background-color;
    animation-duration: 500ms;
    
    animation-fill-mode: forwards;
  }
  @keyframes background-color {
    100% {
      background-color: #4791d0;
    }
  }
</style>
<button>Register</button>
```

### Movement with CSS
If an element has a specific position (fixed, relative, etc). You can move it.

```h
<style>
  div {
    height: 40px;
    width: 70%;
    background: black;
    margin: 50px auto;
    border-radius: 5px;
    position: relative;
  }

#rect {
  animation-name: rainbow;
  animation-duration: 4s;
}

@keyframes rainbow {
  0% {
    background-color: blue;
    left: 0px;
    top: 0px;
    
  }
  50% {
    background-color: green;
    left: 25px;
    top: 50px;
    
  }
  100% {
    background-color: yellow;
    left: -25px;
    top: 0px;
  }
}
</style>

<div id="rect"></div>
```

### Loop Animations
Its possible to loop animations how many times you want with `animation-iteration-count:`. You can choose a number, like 3, or `infinite`, which will make it go on forever.

```h
#ball {
    animation-name: bounce;
    animation-duration: 1s;
    animation-iteration-count: 3;
  }
```

### Animation Timing
Change animation timing with `animation-timing-function:`. There are several alternatives:

* ease
* ease-out
* ease-in
* linear


### Cubic Bezier
In CSS animations, Bezier curves are used with the cubic-bezier function. The shape of the curve represents how the animation plays out. The curve lives on a 1 by 1 coordinate system. The X-axis of this coordinate system is the duration of the animation (think of it as a time scale), and the Y-axis is the change in the animation.

The cubic-bezier function consists of four main points that sit on this 1 by 1 grid: p0, p1, p2, and p3. p0 and p3 are set for you - they are the beginning and end points which are always located respectively at the origin (0, 0) and (1, 1). You set the x and y values for the other two points, and where you place them in the grid dictates the shape of the curve for the animation to follow. This is done in CSS by declaring the x and y values of the p1 and p2 "anchor" points in the form: (x1, y1, x2, y2). Pulling it all together, here's an example of a Bezier curve in CSS code:

`animation-timing-function: cubic-bezier(0.25, 0.25, 0.75, 0.75);`

In the example above, the x and y values are equivalent for each point (x1 = 0.25 = y1 and x2 = 0.75 = y2), which if you remember from geometry class, results in a line that extends from the origin to point (1, 1). This animation is a linear change of an element during the length of an animation, and is the same as using the linear keyword. In other words, it changes at a constant speed.




