# Binary

##  Bitwise operators

## And (&)
Compares the bits of the object like and `&&` operator. Returns true if it is the same.

```csharp
var result = 7 & 3  // 3

00000111    // 7
00000011    // 3
========
00000011    // 3
```

## Or (|)
Compares the bits of the object like and `||` operator. Return true if anything is true.

```csharp
var result = 7 | 3  // 7

00000111    // 7
00000011    // 3
========
00000111    // 7
```


## Xor (Exclusive or) (^)
Only true when they are different values.

```csharp
var result = 7 ^ 3  // 4

00000111    // 7
00000011    // 3
========
00000100    // 4
```

## Not (~)
Inverts a value.

```csharp
byte result = ~3  // 252

00000011    // 3
========
11111100    // 252
```

## Bitwise shifting

### Left (<<)
Shifts all values to the left. Doubles an int.

```csharp
byte c = 3;             // 3
byte result = c << 1;   // 6 (shift by one)

00000011    // 3
========
00000110    // 6
```

### Right (>>)
Shifts all the values to the right. Halfes an int.

```csharp
byte c = 3;             // 3
byte result = c >> 1;   // 1 (shift by one)

00000011    // 3
========
00000001    // 6
```

## Usage

### Toggle boolean
Use it to change value of an boolean.
```csharp
var a = true;   // true
a ^= a;         // false
```

### Enum flags
Enums are basically ints.

```csharp
public enum Colors
{
    Red = 1,
    Blue = 2,
    Green = 4
}
```

So, you can compare them with bitwise operators.
```csharp
var blue = Colors.Blue;  //2
00000010

var red = Colors.Red;   //1
00000001

var isRed = Colors.Red & Colors.Red;    //1
00000001
```
The output is not `true` or `false`, its the actual enum `Red`.
