# CSS

## Advanced 
Based on the course from FreeCodeCamp called Applied Visual Design.

### Psuedo classes
Use psudo classes to access specific parts of an element.

#### Hover class
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

### Positioning

There are several different ways to position elements in CSS.

![](https://image.slidesharecdn.com/positionanditsvalues-170702045148/95/css-position-and-its-values-1-638.jpg?cb=1498971289)

#### Relative position
This example is 15 px from the top

```h
<style>
  h2 {
    position: relative;
    top: 15px; 
  }
</style>
```

#### Absolute position
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

#### Fixed position
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

### Animation
Animations are used to make objects move. Its based on **@Keyframes**. 

#### Basic animation
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

#### Animate hover
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
