# Quick JavaScript Primitive Types Guide

## Core Concept
- Primitive types are JavaScript's simplest, most basic data types that are immutable (cannot be changed after creation)
- 🧱 Mental model: Think of primitives as the atomic building blocks of JavaScript data
- Visual representation:
  ```
  ┌──────────────────────────────────┐
  │ JavaScript Primitive Types       │
  ├──────────────┬───────────────────┤
  │ String       │ "Hello"           │
  │ Number       │ 42, 3.14          │
  │ Boolean      │ true, false       │
  │ null         │ null              │
  │ undefined    │ undefined         │
  │ Symbol       │ Symbol('id')      │
  │ BigInt       │ 9007199254740991n │
  └──────────────┴───────────────────┘
  ```

## Key Mechanics
```javascript
// Primitives are passed by value
let a = 5;
let b = a;
a = 10;
console.log(a); // 10
console.log(b); // 5 (unchanged)

// Primitives are immutable
let str = "hello";
str[0] = "H"; // This does nothing
console.log(str); // "hello" (unchanged)

// typeof operator with primitives
console.log(typeof "hello");     // "string"
console.log(typeof 42);          // "number"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof Symbol());    // "symbol"
console.log(typeof 42n);         // "bigint"
console.log(typeof null);        // "object" (a known JavaScript bug)
```

- 📦 Primitives are **passed by value**, not by reference
- 🔒 Primitives are **immutable** - their values cannot be changed after creation
- 🏷️ Each primitive has a corresponding **object wrapper** (e.g., String, Number, Boolean)
- ⚠️ `typeof null` returns "object" (a historical bug in JavaScript)

## Interview Mastery
**Q1: Why does `typeof null` return "object" instead of "null"?**  
A: This is a historical bug in JavaScript. In the first implementation, JavaScript values were represented as type tags and values, with the "object" type tag being 0. Null was represented as NULL pointer (0x00), so it incorrectly returned "object".

**Q2: What's the difference between primitive types and objects in JavaScript?**  
A: Primitives are immutable, passed by value, and compared by value. Objects are mutable, passed by reference, and compared by reference. Primitives have no methods (though they appear to via autoboxing).

**Related Concepts:**
- 🔄 **Type Coercion** - JavaScript's automatic conversion between types
- 📦 **Autoboxing** - Automatic wrapping of primitives in their object counterparts when methods are called

**Remember:** Every primitive in JavaScript is immutable and passed by value, meaning when you pass a primitive to a function or assign it to a new variable, you're working with a copy, not the original.
