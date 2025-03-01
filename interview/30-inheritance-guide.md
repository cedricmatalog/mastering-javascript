# Inheritance, Polymorphism and Code Reuse Guide

## Core Concept
- **Inheritance** is a mechanism where a new class/object acquires properties and behaviors from an existing class/object, while **polymorphism** allows methods to do different things based on the object they are acting upon, both enabling efficient **code reuse**.
- 🌳 Think of inheritance like a family tree: children inherit traits from parents while developing their own unique characteristics.
- Visual representation:
```
       🏛️ BaseClass
       /      \
      /        \
🔹 SubClass1   🔸 SubClass2
    |             |
 Inherits      Inherits
 properties    properties
 & methods     & methods
```

---

## Key Mechanics

```javascript
// Parent class
class Vehicle {
  constructor(make) {
    this.make = make;
    this.isRunning = false;
  }
  
  start() {
    this.isRunning = true;
    return `${this.make} engine started`;
  }
}

// Child class inherits from Vehicle
class Car extends Vehicle {
  constructor(make, model) {
    super(make); // Call parent constructor
    this.model = model;
  }
  
  // Polymorphic method - overrides parent's method
  start() {
    super.start(); // Call parent's method
    return `${this.make} ${this.model} engine purrs quietly`;
  }
}

const civic = new Car('Honda', 'Civic');
console.log(civic.start()); // Output: "Honda Civic engine purrs quietly"
```

- 🧬 **Prototype Chain**: JavaScript uses a **prototype chain** to implement inheritance, allowing objects to inherit properties and methods from their prototype objects.
- 🔄 **Method Overriding**: Child classes can **redefine** methods inherited from the parent class to provide specialized behavior.
- 🧩 **Constructor Inheritance**: The `super()` keyword is used to call the constructor of the parent class and access its properties and methods.
- 🔗 **Code Reuse**: Inheritance promotes **DRY** (Don't Repeat Yourself) by defining common functionality in a parent class that multiple child classes can use.

---

## Interview Mastery

### Common Interview Questions

**Q: What are the differences between classical inheritance and prototypal inheritance in JavaScript?**  
A: Classical inheritance is class-based (using ES6 `class` syntax), creating rigid parent-child hierarchies where subclasses inherit from superclasses. Prototypal inheritance is object-based, where objects inherit directly from other objects through the prototype chain. JavaScript's `class` syntax is syntactic sugar over its prototypal inheritance system.

**Q: How would you implement multiple inheritance in JavaScript?**  
A: JavaScript doesn't support true multiple inheritance, but you can simulate it with:
1. **Composition**: Favoring object composition over inheritance by combining multiple objects
2. **Mixins**: Using Object.assign() to copy methods from multiple source objects
3. **Prototype chaining with care**: Creating complex inheritance chains

### Critical Connections

🔌 **Closures** - Both closures and inheritance are mechanisms for code reuse, but closures maintain private state while inheritance shares functionality across objects.

🏗️ **Design Patterns** - Inheritance enables patterns like Factory, Template Method, and Strategy, which promote flexible, maintainable code structures.

### Remember
> 💡 Inheritance and polymorphism are tools, not goals. Use them to reduce duplication and increase flexibility, but favor composition over inheritance when it leads to simpler, more maintainable code.
