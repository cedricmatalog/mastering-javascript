# JavaScript Questions 11-20: Advanced Object & Function Patterns

## 11. Constructor Functions and Prototypes

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Lydia', 'Hallie');
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

**Output: `TypeError`**

**Explanation:**
This question tests understanding of prototypes and constructor functions:

1. We create a `Person` constructor function that creates objects with `firstName` and `lastName` properties
2. We create an instance `member` using the `new` keyword
3. We add the `getFullName` method directly to the `Person` constructor function, NOT to its prototype
4. When we try to call `member.getFullName()`, JavaScript looks for this method in the `member` object, then in its prototype chain, but can't find it

The method was added to the constructor function itself, not to its prototype. So while `Person.getFullName()` would work, `member.getFullName()` fails.

**Key Takeaway:** To make methods available to all instances, add them to the prototype: `Person.prototype.getFullName = function() {...}`.

## 12. Constructor Functions and `new` Keyword

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person('Lydia', 'Hallie');
const sarah = Person('Sarah', 'Smith');

console.log(lydia);
console.log(sarah);
```

**Output: `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`**

**Explanation:**
This question illustrates the critical importance of the `new` keyword with constructor functions:

1. For `lydia`, we use `new Person(...)` which:
   - Creates a new empty object
   - Sets `this` to point to that object
   - Executes the constructor function, adding properties to the object
   - Returns the new object

2. For `sarah`, we omit the `new` keyword, so:
   - `this` refers to the global object (window in browsers)
   - Properties are added to the global object
   - The function doesn't explicitly return anything, so it returns `undefined`

**Key Takeaway:** Always use the `new` keyword when working with constructor functions. Consider using ES6 classes which make this requirement more explicit.

## 13. Event Propagation

**What are the three phases of event propagation?**
**Answer: Capturing > Target > Bubbling**

**Explanation:**
This question tests understanding of DOM event propagation:

1. **Capturing Phase**: Events travel from the document root down to the target element
2. **Target Phase**: The event reaches the element that triggered it
3. **Bubbling Phase**: Events travel back up from the target to the document root

Most event handlers are registered for the bubbling phase by default (using `addEventListener` with no third parameter or `false`). You can register for the capturing phase by passing `true` as the third parameter to `addEventListener`.

**Key Takeaway:** Understanding event phases is crucial for managing event handlers in complex UIs, especially when dealing with nested elements.

## 14. Prototypes

**Do all objects have prototypes?**
**Answer: False**

**Explanation:**
This question tests understanding of JavaScript's prototype inheritance:

- Most objects in JavaScript have a prototype, which they inherit properties and methods from
- However, the base object (created by `Object.create(null)`) and the `Object.prototype` object itself have no prototype
- `Object.prototype` is the end of the prototype chain, and its `__proto__` property is `null`

Regular objects created with literals or constructors inherit from `Object.prototype`, but not all objects have a prototype.

**Key Takeaway:** Understanding the prototype chain is essential for JavaScript. Objects inherit properties from their prototype, and the chain ends at `Object.prototype` or at objects created with `Object.create(null)`.

## 15. Type Coercion

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, '2');
```

**Output: `"12"`**

**Explanation:**
This question demonstrates JavaScript's implicit type coercion with the `+` operator:

1. The `+` operator handles both numeric addition and string concatenation
2. When one operand is a string, the other is converted to a string
3. In `sum(1, '2')`, `1` (a number) and `'2'` (a string) are operands for `+`
4. JavaScript converts `1` to the string `"1"`
5. String concatenation occurs: `"1" + "2"` equals `"12"`

**Key Takeaway:** The `+` operator prioritizes string concatenation over addition. To ensure numeric addition, convert string inputs to numbers explicitly using `Number()`, `parseInt()`, `parseFloat()`, or the unary `+` operator.

## 16. Increment/Decrement Operators

```javascript
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

**Output: `0` `2` `2`**

**Explanation:**
This question tests understanding of postfix and prefix increment operators:

1. `number++` (postfix increment):
   - Returns the original value (`0`)
   - Then increments `number` to `1`

2. `++number` (prefix increment):
   - Increments `number` to `2` first
   - Then returns the new value (`2`)

3. `console.log(number)` shows the current value, which is `2`

**Key Takeaway:** Prefix operators (`++number`) change the value first, then return it. Postfix operators (`number++`) return the value first, then change it.

## 17. Tagged Template Literals

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = 'Lydia';
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

**Output: `["", " is ", " years old"]` `"Lydia"` `21`**

**Explanation:**
This question demonstrates tagged template literals, a powerful feature of ES6:

1. When using a tag function with template literals, the first argument is an array of string literals
2. The remaining arguments are the values of the processed expressions

In this case:
- The string is split around the expressions, giving `["", " is ", " years old"]`
- The expressions `${person}` and `${age}` are passed as separate arguments: `"Lydia"` and `21`

**Key Takeaway:** Tagged template literals allow you to process template literals with a function, enabling powerful string manipulation, sanitization, localization, and more.

## 18. Object Equality Comparisons

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log('You are an adult!');
  } else if (data == { age: 18 }) {
    console.log('You are still an adult.');
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

**Output: `Hmm.. You don't have an age I guess`**

**Explanation:**
This question tests object comparison in JavaScript:

1. Objects are compared by reference, not by their contents
2. Each object literal (`{}`) creates a new object with a unique reference
3. When we compare two different objects with `===` or `==`, they're never equal even if they have identical properties

In the code:
- `{ age: 18 } === { age: 18 }` is `false` because they're different objects
- `{ age: 18 } == { age: 18 }` is also `false` for the same reason
- Therefore, the `else` clause executes

**Key Takeaway:** To compare object contents, you must either compare individual properties or use a deep comparison approach (like `JSON.stringify(obj1) === JSON.stringify(obj2)` for simple cases).

## 19. Rest Parameters and typeof

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

**Output: `"object"`**

**Explanation:**
This question combines rest parameters with JavaScript's type system:

1. The rest parameter (`...args`) collects all arguments into an array
2. Arrays in JavaScript are objects
3. `typeof` on an array returns `"object"`, not `"array"`

To check if something is an array:
- Use `Array.isArray(args)` which would return `true`

**Key Takeaway:** JavaScript's `typeof` operator doesn't distinguish arrays from other objects. Use `Array.isArray()` to specifically check for arrays.

## 20. Strict Mode

```javascript
function getAge() {
  'use strict';
  age = 21;
  console.log(age);
}

getAge();
```

**Output: `ReferenceError`**

**Explanation:**
This question demonstrates the impact of JavaScript's strict mode:

1. `'use strict'` enables strict mode, which enforces more rigorous error checking
2. In strict mode, variables must be declared before use
3. Without `var`, `let`, or `const`, `age = 21` attempts to create or modify a global variable
4. Strict mode prohibits this, resulting in a `ReferenceError`

Without strict mode, the code would create a global `age` variable and log `21`.

**Key Takeaway:** Strict mode helps catch common coding mistakes by throwing errors where non-strict code would silently misbehave. It's automatically enabled in ES modules and classes.
