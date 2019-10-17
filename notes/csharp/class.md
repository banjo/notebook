# Class basics in C#

- [Class basics in C](#class-basics-in-c)
  - [Basic class](#basic-class)
    - [Where in program](#where-in-program)
    - [Create class](#create-class)
    - [Partial class](#partial-class)
    - [Init class](#init-class)
  - [Static class](#static-class)
    - [Example](#example)
    - [Call static class](#call-static-class)
    - [Static members in non-static classes](#static-members-in-non-static-classes)
  - [Anonymous classes](#anonymous-classes)
  - [Inheritance](#inheritance)
  - [Abstract classes](#abstract-classes)
  - [Sealed classes](#sealed-classes)
  - [Interface](#interface)
    - [Interface polymorphishm](#interface-polymorphishm)

## Basic class

### Where in program
Declare it after the Program class, if in the main program.

```csharp
namespace DEV204
{
    class Program
    {
        static void Main(string[] args)
        {

        }

    }

    // here
    class DrinksMachine
    {
        // logic
    }
}
```


### Create class
A basic class.

```csharp
public class DrinksMachine
{

    // underscore before private
    private string _location;

    // getter and setter manually
    public string Location
    {
        get
        {
            return _location;
        }
        set
        {
            if (value != null)
            {
                _location = value;
            }
        }
    }

    // automatic getter and setter
    public int Age { get; internal set; }

    // constructor without argument
    public DrinksMachine()
    {
        this.Age = 10;
    }

    // constuctor with argument
    public DrinksMachine(int age)
    {
        this.Age = age;
    }

    // create method
    public void MakeCappucino()
    {
        Console.WriteLine("Cappu");
    }

}
```
### Partial class
Use a partial class to split up a class into several parts.

```csharp
public partial class DrinksMachine
{
    public void MakeTea()
    {
        // logic for tea
        Console.WriteLine("Tea");
    }
}
```

### Init class
Initiate class and use it

```csharp
// with age
DrinksMachine dm = new DrinksMachine(age: 10);
// or...
DrinksMachine dm = new DrinksMachine(10);

// set property
dm.Age = 20;

// call method
dm.MakeCappucino();

// get property
Console.WriteLine(dm.Age);
```

## Static class
Static classes cannot be initiated, just directly used. Any members of the class must also use the `static` keyword.

### Example
```csharp
public static class Conversions
{
   public static double PoundsToKilos(double pounds)
   {
      // Convert argument from pounds to kilograms
      double kilos = pounds * 0.4536;
      return kilos;
   }
   public static double KilosToPounds(double kilos)
   {
      // Convert argument from kilograms to pounds
      double pounds = kilos * 2.205;
      return pounds;
   }
}
```

### Call static class
```csharp
double weightInKilos = 80;
double weightInPounds = Conversions.KilosToPounds(weightInKilos);
```

### Static members in non-static classes
Static properties are often used to return data that is common to all instances, or to keep track of how many instances of a class have been created. Static methods are often used to provide utilities that relate to the type in some way, such as comparison functions.

```csharp
public class DrinksMachine
{
   public int Age { get; set; }
   public string Make { get; set; }
   public string Model { get; set; }

   private static int instances = 0;

   public DrinksMachine()
   {
       // every time the class is initiated, increase the count.
       instances++;
   }

   // static method within class
   public static int CountDrinksMachines()
   {
      return instances;
   }
}
```
There is only one instance of a static class. Regardsless of how many instances the class has. Access is through the class name, not the instance.

```csharp
int drinksMachineCount = DrinksMachine.CountDrinksMachines();
```

## Anonymous classes
Class without a name. Read only without defining type.

```csharp
var anonObject = new { Name = "Dafe", Age = "23" };
```

Access with dot notation.

```csharp
string anonName = anonObject.Name;
```

If you have the same fields, same order, same type and so on, they are the same anonymous class and can be assigned to each other.

```csharp
var anonObject = new { Name = "Dafe", Age = "23" };
var anonObject2 = new { Name = "Dofe", Age = "233" };
anonObject = anonObject2;
```

## Inheritance
C# does not support multiple inheritance. A derived class can only have one base class. Use colon to decide where to inherit from.

In this case, the manager class inherits from Employee.

```csharp
class Manager : Employee
{
    private char payRateIndicator;
    private Employee[] emps;
}
```

The Employee could look like this:

```csharp
class Employee
{
    private string empNumber;
    private string firstName;
    private string lastName;
    private string address;

    public string EmpNumber
    {
        get
        {
            return empNumber;
        }

        set
        {
            empNumber = value;
        }
    }

    public string FirstName
    {
        get
        {
            return firstName;
        }

        set
        {
            firstName = value;
        }
    }

    public string LastName
    {
        get
        {
            return lastName;
        }

        set
        {
            lastName = value;
        }
    }

    public string Address
    {
        get
        {
            return address;
        }

        set
        {
            address = value;
        }
    }
}
```
The manager would then get all the properties and attributes.

## Abstract classes
Abstract classes cannot be initited, only inherited. Use the `abstract` keyword for the class.

```csharp
abstract class Employee
    {
        private string empNumber;
        private string firstName;
        private string lastName;
        private string address;

        // .....

        public virtual void Login()
        {
        }

        public virtual void LogOff()
        {
        }

        public abstract void EatLunch();

    }
```
Use the `virtual` keyword if the class can be overrideen in the sub class. Meaning, that you will implement a new version in the sub class.

Use the `abstract` keyword to make it abstract, which has some contstraints:
- An abstract method cannot exist in non-abstract class
- An abstract method is not permitted to have any implementation, including curly braces
- An abstract method signature must end in a semi-colon
- An abstract method MUST be implemented in any sub class. Failure to do so will generate a compiler warning in C#.

## Sealed classes
Sealed classes cannot be inherited.

```csharp
sealed class Phone
{
    // logic
}
```

## Interface
An interface is like a class without implementation. It has methods, properties, events, and indexers, without specifying how any of these members are implemented. When a class implements an interface, the class provides an implementation for each member of the interface. Starts with capital I.

A class `implements` an interface, and `inherits` a class.

```csharp
public interface IBeverage
{
  // Methods, properties, events, and indexers go here.
}
```
Implementations:

```csharp
// method
int GetServingTemperature(bool includesMilk);

// property
bool IsFairTrade { get; set; }

// event
event EventHandler OnSoldOut;

// indexer
string this[int index] { get; set; }
```
You do not include access modifiers.

Example:

```csharp
public interface ILoyaltyCardHolder
{
   int TotalPoints { get; }
   int AddPoints(decimal transactionValue);
   void ResetPoints();
}
```

How to implement an interface:

```csharp
public class Customer : ILoyaltyCardHolder
{
   private int totalPoints;
   public int TotalPoints
   {
      get { return totalPoints; }
   }
   public int AddPoints(decimal transactionValue)
   {
      int points = Decimal.ToInt32(transactionValue);
      totalPoints += points;
      return totalPoints;
   }
   public void ResetPoints()
   {
      totalPoints = 0;
   }
   // Other members of the Customer class.
}
```

You can also implement an interface explicitly to make it easier to understand.

```csharp
public class Customer : ILoyaltyCardHolder
{
   private int totalPoints;
   public int TotalPoints
   {
      get { return totalPoints; }
   }
   public int ILoyaltyCardHolder.AddPoints(decimal transactionValue)
   {
      int points = Decimal.ToInt32(transactionValue);
      totalPoints += points;
      return totalPoints;
   }
   public void ILoyaltyCardHolder.ResetPoints()
   {
      totalPoints = 0;
   }
   // Other members of the Customer class.
}
```

### Interface polymorphishm
Write code that works with the interface instead of the classes. So all classes that implements the interface can use it.
Example:

```csharp
// Representing an Object as an Interface Type
Coffee coffee1 = new Coffee();
IBeverage coffee2 = new Coffee();

// Cast to an interface
IBeverage beverage = coffee1;

//Cast an interface type to a derived class type
Coffee coffee3 = beverage as Coffee;
// OR
Coffee coffee4 = (Coffee)beverage;

```

Implement mupltiple interfaces with coma-separation:

```csharp
public class Coffee: IBeverage, IInventoryItem
{
    // class
}
```
