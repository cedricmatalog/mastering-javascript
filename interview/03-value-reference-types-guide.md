# Quick JavaScript Value Types and Reference Types Guide

## Core Concept
- JavaScript has two categories of data types: value types (primitives) and reference types (objects)
- 📋 Mental model: Value types are like making a photocopy (complete duplicate), while reference types are like sharing a Google Doc link (pointing to the same data)
- Visual representation:
  ```
  Value Types (Primitives)     Reference Types (Objects)
  ┌────────┐                   ┌────────┐    ┌────────────┐
  │ var a  │                   │ var x  │    │ {name:"Tom"}│
  │   5    │                   │   ◆────┼───►│            │
  └────────┘                   └────────┘    └────────────┘
  ┌────────┐                   ┌────────┐
  │ var b  │                   │ var y  │
  │   5    │                   │   ◆────┘
  └────────┘                   └────────┘
  (Independent copies)         (Both point to same object)
  ```

## Key Mechanics
```javascript
// Value types (primitives)
let a = 5;
let b = a;
a = 10;
console.log(b); // 5 (unchanged)

// Reference types (objects)
let obj1 = { name: "Alice" };
let obj2 = obj1;
obj1.name = "Bob";
console.log(obj2.name); // "Bob" (changed)

// Function parameters
function updateValues(num, obj) {
  num = 100;
  obj.value = 100;
}

let number = 10;
let object = { value: 10 };
updateValues(number, object);
console.log(number); // 10 (unchanged)
console.log(object.value); // 100 (changed)
```

- 🔄 **Value types** include all primitives (String, Number, Boolean, Symbol, null, undefined, BigInt)
- 🔗 **Reference types** include all objects (Object, Array, Function, Date, RegExp, etc.)
- 📦 Value types are **stored on the stack** and copied when assigned or passed
- 📝 Reference types are **stored on the heap** with references stored on the stack

## Interview Mastery
**Q1: How can you create a true copy of an object in JavaScript?**  
A: Several methods exist: `Object.assign({}, obj)`, spread operator `{...obj}`, `JSON.parse(JSON.stringify(obj))` for deep copies (with limitations), or specialized libraries like Lodash's `_.cloneDeep()` for complex nested objects.

**Q2: Why does comparing two identical objects with `==` or `===` return false?**  
A: Object comparisons check if the references point to the same memory location, not if the contents are identical. Two separate objects with identical properties are still distinct references.

**Related Concepts:**
- 🧬 **Deep vs. Shallow Copying** - Understanding the difference between copying just the first level of an object vs. all nested objects
- 🎯 **Immutability Patterns** - Techniques to avoid unintended mutations in objects and arrays

**Remember:** Primitives are compared by their value, while objects are compared by their reference. This fundamental distinction explains many of JavaScript's seemingly odd behaviors with equality and mutation.
