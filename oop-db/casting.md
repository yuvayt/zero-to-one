# Casting

Casting refers to the process of converting a variable from one data type to another. It's a common operation in statically-typed programming languages.

## Upcasting

Upcasting is the process of converting a reference from a derived class to a base class. This is considered safe and is often done implicitly by the compiler.

**Example:**
```java
// In Java
class Animal {}
class Dog extends Animal {}

// Upcasting
Dog myDog = new Dog();
Animal myAnimal = myDog;  // Implicit upcast - no explicit cast required
```

**Key characteristics:**
- Always safe (no runtime errors)
- Implicit (no explicit casting required)
- May lose access to the specific methods/properties of the derived class

## Downcasting

Downcasting is the process of converting a reference from a base class to a derived class. This operation is potentially unsafe and typically requires explicit syntax.

**Example:**
```java
// In Java
Animal someAnimal = new Dog();
// Downcasting
Dog myDog = (Dog) someAnimal;  // Explicit downcast required
```

**Key characteristics:**
- Potentially unsafe (may cause runtime errors if the object isn't actually of the target type)
- Requires explicit syntax
- Allows access to the specific methods/properties of the derived class
- Often requires runtime type checking (e.g., using `instanceof` in Java)

In languages with dynamic typing (like Python or JavaScript), casting works differently and is often less explicit, as these languages perform type checking at runtime.
