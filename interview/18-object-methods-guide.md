# Object.create and Object.assign Guide

## Core Concept
- **Object.create()** creates a new object with a specified prototype object and optional property descriptors, while **Object.assign()** copies all enumerable properties from one or more source objects to a target object.
- 🧬 **Mental Model**: Think of Object.create as **cloning DNA** (inheriting prototype) while Object.assign is like **transplanting organs** (copying properties directly).

```
     Object.create                    Object.assign
     ┌───────────┐                   ┌───────────┐
     │ Prototype │                   │  Source   │
     └─────┬─────┘                   └─────┬─────┘
           │                               │
           ▼                               ▼
    ┌─────────────┐               ┌────────────────┐
    │ New Object  │               │ Target Object  │
    │ (Inherits)  │               │ (Gets copies)  │
    └─────────────┘               └────────────────┘
```

---

## Key Mechanics

```javascript
// Object.create example
const parent = { greet() { return "Hello" } };
const child = Object.create(parent);
console.log(child.greet());  // "Hello"
console.log(child.__proto__ === parent);  // true

// Object.assign example
const target = { a: 1 };
const source = { b: 2, c: 3 };
const result = Object.assign(target, source);
console.log(result);  // { a: 1, b: 2, c: 3 }
console.log(target === result);  // true (modified in-place)
```

- 🔄 Object.create establishes **prototype chain inheritance** but doesn't copy properties directly
- 📝 Object.assign performs **shallow copying** only (nested objects are copied by reference)
- 🎯 Object.assign **modifies the target object in-place** and also returns it
- 🚫 Properties with values like **undefined**, **non-enumerable properties**, and **Symbol properties** are handled differently by these methods

---

## Interview Mastery

**Q1: What's the difference between `Object.create(null)` and `{}`?**  
A: `Object.create(null)` creates a "pure dictionary" object with no inherited properties (not even from Object.prototype), so no `.toString()`, `.hasOwnProperty()`, etc. Empty object literals `{}` inherit from Object.prototype.

**Q2: How would you perform a deep clone of an object using these methods?**  
A: Neither method performs deep cloning alone. For deep cloning, you would need to recursively apply Object.assign for each nested object, use a custom recursion function, or use `JSON.parse(JSON.stringify(obj))` (with limitations on functions, dates, etc).

- 🔗 **Prototypal Inheritance**: Object.create is fundamental to JavaScript's prototype chain, allowing cleaner inheritance patterns than constructor functions
- 🔄 **Spread Syntax**: Modern alternative to Object.assign: `const merged = {...obj1, ...obj2}` which is more readable but functionally similar

**Remember:** Object.create builds relationships (inheritance), while Object.assign builds compositions (mixing properties) - choose based on whether you need an "is-a" or "has-a" relationship.
