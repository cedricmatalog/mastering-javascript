# JavaScript Data Structures Guide

## Core Concept
- **Data structures** are specialized formats for organizing, storing, and manipulating data efficiently
- 🧱 Mental model: Think of data structures as different types of containers - each designed to store items in specific ways for specific use cases
- Visual representation:

```
Array: [📦, 📦, 📦, 📦]  
Object: { 🔑: 📦, 🔑: 📦 }
Set: { 📦, 📦, 📦 } (no duplicates)
Map: { 🔑↔️📦, 🔑↔️📦 } (any key type)
```

---

## Key Mechanics

```javascript
// Common data structures in JavaScript
const array = [1, 2, 3];                      // Ordered collection
const object = { name: "Alice", age: 30 };    // Key-value pairs
const set = new Set([1, 2, 2, 3]);            // Unique values: {1, 2, 3}
const map = new Map([["key", "value"]]);      // Key-value with any key type

// Methods example (array)
array.push(4);     // Add to end: [1, 2, 3, 4]
array.pop();       // Remove from end: [1, 2, 3]
array.unshift(0);  // Add to start: [0, 1, 2, 3]
array.shift();     // Remove from start: [1, 2, 3]
```

- 🔢 **Arrays**: Ordered, integer-indexed collections with **O(1)** access time but potentially **O(n)** for insertions/deletions
- 🔍 **Objects/Maps**: Key-value pairs with **O(1)** average access, insertion, and deletion time
- 🧮 **Sets**: Collections of **unique values** with **O(1)** average time for adding, deleting, and checking membership
- 🌲 **Custom structures** (trees, linked lists, etc.) must be implemented manually for specific performance requirements

---

## Interview Mastery

**Q1: When would you choose a Map over an Object in JavaScript?**  
A: Choose Map when: (1) keys aren't strings/symbols, (2) you need to preserve key insertion order, (3) you need to frequently add/remove properties, or (4) you need to easily determine the size.

**Q2: How would you implement a Stack in JavaScript?**  
A: Using an array with push/pop methods for LIFO (Last In, First Out) behavior:
```javascript
class Stack {
  constructor() { this.items = []; }
  push(item) { this.items.push(item); }
  pop() { return this.items.pop(); }
  peek() { return this.items[this.items.length - 1]; }
  isEmpty() { return this.items.length === 0; }
}
```

- 🔄 **Time Complexity**: Understanding the performance characteristics of operations on different data structures is crucial for **optimization** and **scaling** 
- 🧩 **Array Methods**: Knowledge of built-in array methods (map, filter, reduce) unlocks **functional programming** patterns and **declarative code**

**Remember**: Choose the right data structure based on the operations you'll perform most frequently—this single decision often determines whether your algorithm will be efficient or sluggish.
