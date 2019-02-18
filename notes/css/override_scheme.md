# CSS

## Override Scheme

Which element goes first?

### 1. !important
```h
color: green !important;
```

### 2. inline style
```h
<h1 style="color: green;">
```

### 3. ID
```h
#header2 {
  color: blue;
}
```

```h
<h1 id="header2"></h1>
```

### 4. Class
```h
.orange-text{
  color: orange;
}
```

```h
<h1 class"orange-text"></h1>
```


### 5. Class above a class
The document is read in order. Any change of class above another is not applied. The lowest one is the active one.

### 6. in Body
