# The Ultimate JavaScript Map, Reduce, Filter Guide

## Core Concept
- **Map**: Transforms each element of an array using a function, returning a new array of the same length
- **Reduce**: Accumulates array elements into a single value using a function and an initial value
- **Filter**: Creates a new array with elements that pass a test function

🧠 **Mental Model**: Think of these as assembly line workers with specific jobs:
- Map: 🔄 Assembly line worker who modifies each item exactly once
- Reduce: 📊 Accountant who combines all items into a final tally
- Filter: 🧹 Quality inspector who removes items that don't meet standards

```
Original Array: [1, 2, 3, 4, 5]
     |
     ↓
┌─────────┐  ┌─────────┐  ┌─────────┐
│   MAP   │  │ REDUCE  │  │ FILTER  │
│  x => x²│  │ sum all │  │ x > 3   │
└─────────┘  └─────────┘  └─────────┘
     |           |           |
     ↓           ↓           ↓
[1,4,9,16,25]    15        [4,5]
```

---

## Key Mechanics

### Map
```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
// doubled: [2, 4, 6, 8]
```

- 🔍 Takes a **callback function** that receives `(element, index, array)`
- 🆕 **Always returns** a new array of the **same length** as the original
- ⛓️ Can be **chained** with other array methods for complex transformations

### Reduce
```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
// sum: 10
```

- 🏁 Requires an **initial value** (after the callback) that seeds the accumulator
- 🧩 Callback receives `(accumulator, currentValue, index, array)`
- 🔄 Can return **any data type**, not just primitives (objects, arrays, etc.)

### Filter
```javascript
const numbers = [1, 2, 3, 4, 5];
const evens = numbers.filter(num => num % 2 === 0);
// evens: [2, 4]
```

- ✅ Callback must return a **boolean** or value that coerces to boolean
- 🏗️ Returns a **new array** that may be shorter than the original
- 🔍 Perfect for **query operations** like finding items that match criteria

---

## Interview Mastery

### Top Interview Questions

**Q: How would you use all three methods together in a practical example?**  
A: To calculate the sum of squares of even numbers:
```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const sumOfEvenSquares = numbers
  .filter(num => num % 2 === 0)  // [2, 4, 6]
  .map(num => num * num)         // [4, 16, 36]
  .reduce((sum, square) => sum + square, 0);  // 56
```

**Q: How would you implement your own version of reduce?**  
A:
```javascript
function myReduce(array, callback, initialValue) {
  let accumulator = initialValue !== undefined ? initialValue : array[0];
  const startIndex = initialValue !== undefined ? 0 : 1;
  
  for (let i = startIndex; i < array.length; i++) {
    accumulator = callback(accumulator, array[i], i, array);
  }
  
  return accumulator;
}
```

### Critical Connections

🔄 **forEach**: Unlike map, doesn't return a new array, just iterates through each element (side effects only)

📦 **Array Destructuring**: Often used with map to transform objects or extract specific properties
```javascript
const users = [{name: 'Alice', age: 25}, {name: 'Bob', age: 30}];
const names = users.map(({name}) => name); // ['Alice', 'Bob']
```

### Remember
> 💡 Map, reduce, and filter are powerful declarative tools that let you describe **what** you want to accomplish rather than **how** to do it. They promote immutability and functional programming patterns that lead to more predictable, testable code.
