# JavaScript `this`, `call`, `apply` and `bind` Guide

## Core Concept
- **`this`** in JavaScript refers to the execution context of a function - the object that "owns" the currently executing code
- 🧭 Mental model: Think of `this` as a dynamic compass that points to different "owners" depending on how a function is called
- Visual representation:
  ```
  ┌─────────────────┐
  │ Function        │
  │                 │      ┌───────────┐
  │  this ─────────┼─────▶│ Owner     │
  │                 │      │ Object    │
  └─────────────────┘      └───────────┘
  ```

---

## Key Mechanics

```javascript
// Basic example showing different `this` values
const person = {
  name: 'Alex',
  greet() { 
    console.log(`Hello, I'm ${this.name}`);
  }
};

person.greet();                  // Output: Hello, I'm Alex
const greetFn = person.greet;
greetFn();                       // Output: Hello, I'm undefined
greetFn.call(person);            // Output: Hello, I'm Alex
greetFn.apply(person);           // Output: Hello, I'm Alex
const boundGreet = greetFn.bind(person);
boundGreet();                    // Output: Hello, I'm Alex
```

- 🔄 **Default binding**: When a function is called directly, `this` points to the **global object** (or `undefined` in strict mode)
- 🎯 **`call` and `apply`** methods invoke a function with a specified `this` value, but `call` takes **individual arguments** while `apply` takes **array of arguments**
- 🔒 **`bind`** returns a new function permanently **bound** to the provided `this` value, which cannot be changed later
- 🏛️ **Order of precedence**: `bind` > `call`/`apply` > method call > default binding

---

## Interview Mastery

**Q1: What's the difference between `call` and `apply`?**  
A1: Both methods invoke a function with a specified `this` value, but `call` accepts arguments individually (comma-separated), while `apply` accepts arguments as an array.

**Q2: Why does `this` behave differently in arrow functions?**  
A2: Arrow functions don't have their own `this` context. They inherit `this` from the enclosing lexical scope where they are defined, not where they are called.

**Related Concepts:**
- 🏹 **Arrow Functions** (`() => {}`) lexically bind `this` to the enclosing context, making them immune to context changes
- 🔍 **Execution Context** determines the value of `this`, variable scope, and function arguments during function execution

**Remember:** `this` is not fixed - it's determined by how a function is called, not where it's defined (except for arrow functions). The methods `call`, `apply`, and `bind` give you explicit control over `this`.
