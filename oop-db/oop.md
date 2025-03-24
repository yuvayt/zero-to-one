# Object-Oriented Programming (OOP)

Object-oriented programming is a programming paradigm based on the concept of "objects" which contain data (attributes) and code (methods). OOP uses these objects to design applications.

## Core Concepts

### Class

> A blueprint or template for creating objects.
>
> - **Attributes**: Data that describes the object
> - **Methods**: Functions that define object behavior

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

### Object

> An instance of a class - a concrete entity created from the class blueprint.
>
> - **State**: Values of the object's attributes
> - **Behavior**: Actions the object can perform

```csharp
// Creating objects from the Car class
Car myCar = new Car();
Car yourCar = new Car();
```

## Four Pillars of OOP

### 1. Encapsulation

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

**Why?**:
- Improves data security
- Makes code maintenance easier
- Prevents unintended modifications

### 2. Abstraction

> Hiding complex implementation details and exposing only necessary features.

- Focus on *what* an object does rather than *how*
- Implemented through abstract classes and interfaces

**Why?**:
- Simplifies complex systems
- Focuses on essential features

### 3. Inheritance

> A mechanism allowing a class to inherit properties and methods from another class. Creating a parent-child relationship between classes.

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

**Why?**:
- Promotes code reuse
- Establishes logical relationships
- Enhances maintainability

### 4. Polymorphism

> Allows objects of different classes to be treated as objects of a common base class. Same action but different output.

#### Method Overloading (Compile-time)

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

#### Method Overriding (Runtime)

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

**Why?**:
- Makes code more flexible
- Simplifies maintenance

## Important OOP Concepts

### Access Modifiers

> Control the visibility and accessibility of class members.

| Modifier | Description |
|----------|-------------|
| `public` | Accessible from anywhere |
| `private` | Accessible only within the containing class |
| `protected` | Accessible within the class and its subclasses |
| `internal` | Accessible within the same assembly |

### Constructors

> Special methods used to initialize objects when created.

```csharp
public class Person {
    public string Name { get; set; }
    public int Age { get; set; }

    // Default constructor
    public Person() {
        Name = "Unknown";
        Age = 0;
    }

    // Parameterized constructor
    public Person(string name, int age) {
        Name = name;
        Age = age;
    }
}
```

### Static Members

> Members that belong to the class itself, not to instances.

- Shared across all instances
- Accessed using the class name
- Cannot access non-static members directly

**Uses**:
- Utility methods
- Constants
- Singleton pattern

### Immutability

> An immutable object's state cannot change after creation.

**Why?**:
- Thread safety
- Simpler code
- Prevents unexpected modifications

```csharp
public class ImmutablePerson {
    public string Name { get; }
    public int Age { get; }

    public ImmutablePerson(string name, int age) {
        Name = name;
        Age = age;
    }

    // Returns new instance instead of modifying
    public ImmutablePerson WithName(string newName) {
        return new ImmutablePerson(newName, this.Age);
    }
}
```
