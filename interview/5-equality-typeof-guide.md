# Quick JavaScript == vs === vs typeof Guide

## Core Concept
- JavaScript provides different operators for comparing values and checking their types
- ⚖️ Mental model: `==` is like comparing ingredients after cooking (transformation allowed), `===` is comparing raw ingredients (must be identical), and `typeof` is identifying the food group
- Visual representation:
  ```
  ┌───────────────────────────────────────────────────────┐
  │ JavaScript Comparison & Type Checking                 │
  ├───────────┬───────────────────────────────────────────┤
  │ ==        │ Loose/Abstract equality (with coercion)   │
  │ ===       │ Strict equality (no coercion)             │
  │ typeof    │ Type checking operator                    │
  └───────────┴───────────────────────────────────────────┘
  ```

## Key Mechanics
```javascript
// == vs === comparison
console.log(5 == "5");     // true (values equal after coercion)
console.log(5 === "5");    // false (different types)
console.log(0 == false);   // true (both coerce to falsy)
console.log(0 === false);  // false (number vs boolean)
console.log(null == undefined);  // true
console.log(null === undefined); // false

// typeof examples
console.log(typeof 42);           // "number"
console.log(typeof "hello");      // "string"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof null);         // "object" (historical bug)
console.log(typeof {});           // "object"
console.log(typeof []);           // "object" (arrays are objects)
console.log(typeof function(){}); // "function"
```

- 🔄 **Double equals** (`==`) performs **type coercion** before comparison
- 🎯 **Triple equals** (`===`) compares both **value and type** without coercion
- 🏷️ **typeof** returns a string indicating the **primitive type** of a value
- ⚠️ `typeof null` returns "object" and `typeof []` returns "object" (use `Array.isArray()` for arrays)

## Interview Mastery
**Q1: When would you prefer to use == over === in JavaScript?**  
A: Rarely. The strict equality operator (`===`) is generally preferred as it avoids unexpected type coercion. However, `==` could be useful when intentionally checking for either null or undefined with `x == null`, which is equivalent to `x === null || x === undefined`.

**Q2: How would you correctly check if a variable is an array in JavaScript?**  
A: Use `Array.isArray(variable)` rather than `typeof`, since `typeof []` returns "object". Alternatives include `variable instanceof Array` or `Object.prototype.toString.call(variable) === '[object Array]'`, but `Array.isArray()` is the most reliable.

**Related Concepts:**
- 📊 **Type Coercion Rules** - Understanding JavaScript's complex ruleset for implicit type conversion
- 🔍 **instanceof Operator** - An alternative way to check for complex types and inheritance

**Remember:** `===` compares values without type conversion and is generally safer, while `==` allows comparison across different types with coercion. The `typeof` operator helps identify primitive types but has limitations with complex objects, arrays, and null.
