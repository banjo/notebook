# Generics

## What are they

Collections are used to store data. Without defining what type, an ArrayList could store anything that is an object. Meaning, you would have to cast it back to its original type.

A generic would, for example, define what type an ArrayList would hold. So, instead of storing an Object, it would store an integer.

```csharp
// create a new ArrayList
var list = new ArrayList();

// its possible to add all types
list.add("hello");
list.add(5);

// create a generic ArrayList
var genericList = new List<string>();

// now you can only add strings
genericList.add("Hello");
genericList.add("Yes");
```
Meaning, if you use a generic list, you don't need to unpack it like this.

```csharp
int number = (int)list[1];
```

## Creating a generic class
This is a basic example of how you create a generic class.

```csharp
public class CustomList<T>
{
    private List<T> list { get; set; }

    public void Add(T item)
    {
        // Method logic goes here.

    }
    public void Remove(T item)
    {
        // Method logic goes here.
    }
}
```

## Constraining generics to interfaces
If you want to constraint a type parameter in a generic to something that it inheritcs or implements, you can do that with the `where` keyword.

```csharp
public class CustomList<T> where T : ISomeInterface
{
    // some logic
}
```
There are six type so constraints:
* `where T : <name of interface>`
* `where T : <name of base class>`
* `where T : U`
* `where T : new()`
* `where T : struct`
* `where T : class`

It is also possible to use multiple constraints

```csharp
public class CustomList<T> where T : ISomeInterface, IComparable<T>, new()
{
    // some logic
}
```
