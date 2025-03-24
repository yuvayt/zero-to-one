# OOP

Object-oriented programming is a programming paradigm based on the concept of "objects" which contain data (attributes) and code (methods). OOP uses these objects to design applications.

## Class

 A blueprint or template for creating objects.

- **Attributes**: Data that describes the object
- **Methods**: Functions that define object behavior

```csharp
class Car {
    // Attributes
    private string color;
    private string model;
    private int year;

    // Methods
    public void Accelerate() { /* implementation */ }
    public void Brake() { /* implementation */ }
    public string GetInfo() { return $"{year} {color} {model}"; }
}
```

## Object

An instance of a class - a concrete entity created from the class blueprint.

- **State**: Values of the object's attributes
- **Behavior**: Actions the object can perform

```csharp
// Creating objects from the Car class
Car myCar = new Car();
Car yourCar = new Car();
```

## Encapsulation

> Bundling data and behavior into a single unit (class), while controlling access to the internal state.

- Hides implementation details
- Controls access through modifiers

```csharp
class BankAccount {
    // Private data
    private double balance;

    // Public interface
    public void Deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public double GetBalance() {
        return balance;
    }
}
```

**Why?**
- Improves data security
- Makes code maintenance easier
- Prevents unintended modifications

## Abstraction

Hiding complex implementation details and exposing only necessary features.

- Focus on *what* an object does rather than *how*
- Implemented through abstract classes and interfaces

**Why?**
- Simplifies complex systems
- Focuses on essential features

## Inheritance

A mechanism allowing a class to inherit properties and methods from another class. Creating a parent-child relationship between classes.

```csharp
// Base class
public class Animal {
    public string Name { get; set; }

    public void Eat() {
        Console.WriteLine($"{Name} is eating");
    }
}

// Derived class
public class Dog : Animal {
    public void Bark() {
        Console.WriteLine($"{Name} says woof!");
    }
}

// Usage
Dog myDog = new Dog();
myDog.Name = "Rex";
myDog.Eat();   // Inherited
myDog.Bark();  // Defined in Dog
```

**Why?**
- Promotes code reuse
- Establishes logical relationships
- Enhances maintainability

## Polymorphism

> Allows objects of different classes to be treated as objects of a common base class. Same action but different output.

### Method Overloading (Compile-time)

- Multiple methods with the same name but different parameters

```csharp
public class Calculator {
    public int Add(int a, int b) {
        return a + b;
    }

    public double Add(double a, double b) {
        return a + b;
    }
}
```

### Method Overriding (Runtime)

- Redefines a method in a derived class

```csharp
public class Shape {
    public virtual double CalculateArea() {
        return 0;
    }
}

public class Circle : Shape {
    public double Radius { get; set; }

    public override double CalculateArea() {
        return Math.PI * Radius * Radius;
    }
}
```

**Why?**
- Makes code more flexible
- Simplifies maintenance
