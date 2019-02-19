# Frontend

## CSS Grid
Turn any HTML element into a grid container by setting its display property to grid. This gives you the ability to use all the other properties associated with CSS Grid.

**Note**
In CSS Grid, the parent element is referred to as the container and its children are called items.

**Example**
```h
<style>
  .d1{background:LightSkyBlue;}
  .d2{background:LightSalmon;}
  .d3{background:PaleTurquoise;}
  .d4{background:LightPink;}
  .d5{background:PaleGreen;}
  
  .container {
    font-size: 40px;
    width: 100%;
    background: LightGray;
    display: grid;
  }
</style>
  
<div class="container">
  <div class="d1">1</div>
  <div class="d2">2</div>
  <div class="d3">3</div>
  <div class="d4">4</div>
  <div class="d5">5</div>
</div>
```

## Add Columns with grid-template-columns
Simply creating a grid element doesn't get you very far. You need to define the structure of the grid as well. To add some columns to the grid, use the grid-template-columns property on a grid container as demonstrated below:

```h
.container {
  display: grid;
  grid-template-columns: 50px 50px;
}
```

This will give your grid two columns that are 50px wide each.

The number of parameters given to the grid-template-columns property indicates the number of columns in the grid, and the value of each parameter indicates the width of each column.

## Add Rows with grid-template-rows
Use the same way as above.

**Example with both**
```h
<style>
  .d1{background:LightSkyBlue;}
  .d2{background:LightSalmon;}
  .d3{background:PaleTurquoise;}
  .d4{background:LightPink;}
  .d5{background:PaleGreen;}
  
  .container {
    font-size: 40px;
    width: 100%;
    background: LightGray;
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 50px 50px;
  }
</style>
  
<div class="container">
  <div class="d1">1</div>
  <div class="d2">2</div>
  <div class="d3">3</div>
  <div class="d4">4</div>
  <div class="d5">5</div>
</div>
```

## CSS Grid Units
You can use absolute and relative units like px and em in CSS Grid to define the size of rows and columns. You can use these as well:

fr: sets the column or row to a fraction of the available space,

auto: sets the column or row to the width or height of its content automatically,

%: adjusts the column or row to the percent width of its container.

Here's the code that generates the output in the preview:
```h
grid-template-columns: auto 50px 10% 2fr 1fr;
```

## Create gaps
So far in the grids you have created, the columns have all been tight up against each other. Sometimes you want a gap in between the columns. To add a gap between the columns, use the grid-column-gap property like this:

You can add a gap in between the rows of a grid using grid-row-gap in the same way that you added a gap in between columns in the previous challenge.

Use `grid-gap` to change both above at the same time.

## Control spacing with grid-column
Up to this point, all the properties that have been discussed are for grid containers. The grid-column property is the first one for use on the grid items themselves.

The hypothetical horizontal and vertical lines that create the grid are referred to as lines. These lines are numbered starting with 1 at the top left corner of the grid and move right for columns and down for rows, counting upward.

To control the amount of columns an item will consume, you can use the grid-column property in conjunction with the line numbers you want the item to start and stop at.

Here's an example:
`grid-column: 1 / 3;`

This will make the item start at the first vertical line of the grid on the left and span to the 3rd line of the grid, consuming two columns.

### grid-row
Use grid-row the same way to change which row it should stay between. 

## justify-self and align-self
In CSS Grid, the content of each item is located in a box which is referred to as a cell. You can align the content's position within its cell horizontally using the justify-self property on a grid item. By default, this property has a value of stretch, which will make the content fill the whole width of the cell. This CSS Grid property accepts other values as well:

* start: aligns the content at the left of the cell,
* center: aligns the content in the center of the cell,
* end: aligns the content at the right of the cell.

**align-self can be used the same way.**  

## justify-items and align-items
Sometimes you want all the items in your CSS Grid to share the same alignment. You can use the previously learned properties and align them individually, or you can align them all at once horizontally by using `justify-items` on your grid container. This property can accept all the same values you learned about in the previous two challenges, the difference being that it will move all the items in our grid to the desired alignment.

## Divide grid into Area Template
You can group cells of your grid together into an area and give the area a custom name. Do this by using grid-template-areas on the container like this:
```h
grid-template-areas:
  "header header header"
  "advert content content"
  "footer footer footer";
```
The code above merges the top three cells together into an area named header, the bottom three cells into a footer area, and it makes two areas in the middle row; advert and content.

**Note**
Every word in the code represents a cell and every pair of quotation marks represent a row.

In addition to custom labels, you can use a period (.) to designate an empty cell in the grid.

## Place item in Grid Area
After creating an areas template for your grid container, as shown in the previous challenge, you can place an item in your custom area by referencing the name you gave it. To do this, you use the grid-area property on an item like this:

`.item1 { grid-area: header; }`
This lets the grid know that you want the item1 class to go in the area named header. In this case, the item will use the entire top row because that whole row is named as the header area.

### Use Grid Areas without Creating Area Templates
The grid-area property you learned in the last challenge can be used in another way. If your grid doesn't have an areas template to reference, you can create an area on the fly for an item to be placed like this:

`item1 { grid-area: 1/1/2/4; }`
This is using the line numbers you learned about earlier to define where the area for this item will be. The numbers in the example above represent these values:

grid-area: horizontal line to start at / vertical line to start at / horizontal line to end at / vertical line to end at;
So the item in the example will consume the rows between lines 1 and 2, and the columns between lines 1 and 4.


## Repeat Function
Create many columns and rows without repeating.
`grid-template-rows: repeat(100, 50px);`
`grid-template-columns: repeat(2, 1fr 50px) 20px;`

## Minmax Function
`grid-template-columns: 100px minmax(50px, 200px);`
There are two columns in the above example. One is 100px, the other one is between 50 and 200 px. 

## Auto-fill combined with Repeat
`repeat(auto-fill, minmax(60px, 1fr));`
The repeat function comes with an option called auto-fill. This allows you to automatically insert as many rows or columns of your desired size as possible depending on the size of the container.

When the container changes size, this setup keeps inserting 60px columns and stretching them until it can insert another one.

## Auto-fit combined with Repeat
` grid-template-columns: repeat(auto-fit, minmax(60px, 1fr));`


auto-fit works almost identically to auto-fill. The only difference is that when the container's size exceeds the size of all the items combined, auto-fill keeps inserting empty rows or columns and pushes your items to the side, while auto-fit collapses those empty rows or columns and stretches your items to fit the size of the container.

**Note**
If your container can't fit all your items on one row, it will move them down to a new one.


`grid-template-columns: 100px minmax(50px, 200px);`

## Use Media Queries to create responsive layout
CSS Grid can be an easy way to make your site more responsive by using media queries to rearrange grid areas, change dimensions of a grid, and rearrange the placement of items.

In the preview, when the viewport width is 300px or more, the number of columns changes from 1 to 2. The advertisement area then occupies the left column completely.

```h
<style>
  .item1 {
    background: LightSkyBlue;
    grid-area: header;
  }
  
  .item2 {
    background: LightSalmon;
    grid-area: advert;
  }
  
  .item3 {
    background: PaleTurquoise;
    grid-area: content;
  }
  
  .item4 {
    background: lightpink;
    grid-area: footer;
  }
  
  .container {
    font-size: 1.5em;
    min-height: 300px;
    width: 100%;
    background: LightGray;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 50px auto 1fr auto;
    grid-gap: 10px;
    grid-template-areas:
      "header"
      "advert"
      "content"
      "footer";
  }
  
  @media (min-width: 300px){
    .container{
      grid-template-columns: auto 1fr;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "advert header"
        "advert content"
        "advert footer";
    }
  }
  
  @media (min-width: 400px){
    .container{
      /* change the code below this line */
      grid-template-columns: auto 1fr;
      grid-template-rows: auto 1fr auto;

      grid-template-areas:
        "header header"
        "advert content"
        "footer footer";
    
    /* change the code above this line */
    }
  }
</style>
  
<div class="container">
  <div class="item1">header</div>
  <div class="item2">advert</div>
  <div class="item3">content</div>
  <div class="item4">footer</div>
</div>
```

## Grid Within Grids
Turning an element into a grid only affects the behavior of its direct descendants. So by turning a direct descendant into a grid, you have a grid within a grid.

For example, by setting the display and grid-template-columns properties of the element with the item3 class, you create a grid within your grid.

