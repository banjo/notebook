# Frontend

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
