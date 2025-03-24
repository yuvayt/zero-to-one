# Access Modifiers

> Control the visibility and accessibility of class members.

| Modifier | Description |
|----------|-------------|
| `public` | Accessible from anywhere |
| `private` | Accessible only within the containing class |
| `protected` | Accessible within the class and its subclasses |
| `internal` | Accessible within the same assembly |

# Constructors

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

# Static Members

> Members that belong to the class itself, not to instances.

- Shared across all instances
- Accessed using the class name
- Cannot access non-static members directly

**Uses**:
- Utility methods
- Constants
- Singleton pattern

# Immutability

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
