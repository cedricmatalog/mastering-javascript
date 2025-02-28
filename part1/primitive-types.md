# Primitive Types in JavaScript

## Concept Introduction

JavaScript primitive types are the basic building blocks of the language. They represent the simplest data values and are immutable (cannot be changed once created). Understanding primitives is fundamental to mastering JavaScript, as they form the foundation upon which all other data structures are built.

JavaScript has seven primitive data types:

1. **String**: Represents textual data
2. **Number**: Represents both integer and floating-point numbers
3. **Boolean**: Represents logical entities (true/false)
4. **Undefined**: Represents a variable that has been declared but not assigned a value
5. **Null**: Represents the intentional absence of any object value
6. **Symbol**: Represents a unique identifier
7. **BigInt**: Represents integers with arbitrary precision

## Deep Dive

### String

Strings are sequences of characters enclosed in single quotes (`'`), double quotes (`"`), or backticks (`` ` ``).

```javascript
const singleQuoted = 'Hello, world!';
const doubleQuoted = "Hello, world!";
const templateLiteral = `Hello, world!`;

// Template literals allow for expressions and multi-line strings
const name = 'JavaScript';
const greeting = `Hello, ${name}!
This is a multi-line string.`;

console.log(greeting);
// Output:
// Hello, JavaScript!
// This is a multi-line string.
```

Strings have various built-in methods for manipulation:

```javascript
const str = "JavaScript is amazing";

// Getting the length
console.log(str.length); // 22

// Accessing characters
console.log(str[0]); // "J"
console.log(str.charAt(0)); // "J"

// Finding substrings
console.log(str.indexOf("Script")); // 4
console.log(str.includes("amazing")); // true

// Transforming
console.log(str.toUpperCase()); // "JAVASCRIPT IS AMAZING"
console.log(str.replace("amazing", "awesome")); // "JavaScript is awesome"
console.log(str.split(" ")); // ["JavaScript", "is", "amazing"]
```

### Number

The Number type represents both integers and floating-point numbers.

```javascript
const integer = 42;
const float = 3.14;
const exponent = 2.998e8; // 299,800,000
const binary = 0b1010; // 10 in decimal
const octal = 0o744; // 484 in decimal
const hex = 0xFF; // 255 in decimal

// Special numeric values
const infinity = Infinity;
const negInfinity = -Infinity;
const notANumber = NaN;

console.log(1 / 0); // Infinity
console.log(-1 / 0); // -Infinity
console.log("not a number" / 2); // NaN
```

JavaScript has only one numeric type, which is based on the IEEE 754 standard (double-precision 64-bit binary format). This means:

- It can represent integers up to ±2^53 - 1 precisely
- Floating-point arithmetic can lead to precision issues

```javascript
console.log(0.1 + 0.2); // 0.30000000000000004, not exactly 0.3
console.log(0.1 + 0.2 === 0.3); // false

// To work around this issue:
console.log(Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON); // true
```

### Boolean

Booleans represent logical values: `true` or `false`.

```javascript
const isActive = true;
const isLoggedIn = false;

// Boolean operators
console.log(!isActive); // false (NOT)
console.log(isActive && isLoggedIn); // false (AND)
console.log(isActive || isLoggedIn); // true (OR)
```

Many values in JavaScript are "truthy" or "falsy" - they can be coerced to `true` or `false` in boolean contexts:

```javascript
// Falsy values:
console.log(Boolean(0)); // false
console.log(Boolean("")); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN)); // false
console.log(Boolean(false)); // false

// Everything else is truthy:
console.log(Boolean(1)); // true
console.log(Boolean("hello")); // true
console.log(Boolean({})); // true
console.log(Boolean([])); // true
```

### Undefined

`undefined` represents a variable that has been declared but not assigned a value.

```javascript
let variable;
console.log(variable); // undefined

// Functions that don't return a value implicitly return undefined
function doSomething() {
  // No return statement
}
console.log(doSomething()); // undefined

// Accessing non-existent properties returns undefined
const obj = {};
console.log(obj.nonExistentProperty); // undefined
```

### Null

`null` represents the intentional absence of any object value.

```javascript
const emptyValue = null;

console.log(typeof null); // "object" - this is actually a historical bug in JavaScript
console.log(null === undefined); // false
console.log(null == undefined); // true - loose equality performs type coercion
```

### Symbol

Symbols are unique and immutable primitive values introduced in ES6. They're often used as property keys to avoid name collisions.

```javascript
const sym1 = Symbol();
const sym2 = Symbol("description"); // optional description
const sym3 = Symbol("description"); // another symbol with the same description

console.log(sym2 === sym3); // false - each Symbol is unique

// Using Symbols as object keys
const HIDDEN_PROP = Symbol("hiddenProperty");
const obj = {
  [HIDDEN_PROP]: "This property won't appear in typical iterations"
};

console.log(obj[HIDDEN_PROP]); // "This property won't appear in typical iterations"
console.log(Object.keys(obj)); // [] - Symbol keys aren't included in ordinary iterations
```

### BigInt

BigInt was added to handle integers beyond the safe integer limit of Number.

```javascript
const maxSafeInteger = Number.MAX_SAFE_INTEGER; // 9007199254740991
console.log(maxSafeInteger + 1 === maxSafeInteger + 2); // true - imprecision with regular Numbers

// BigInt literals are written with an 'n' suffix
const bigInt = 9007199254740991n;
console.log(bigInt + 1n === bigInt + 2n); // false - BigInt maintains precision

// Converting between Number and BigInt
const num = Number(123n); // 123
const big = BigInt(123); // 123n

// Cannot mix BigInt and Number in operations
// console.log(123n + 456); // TypeError: Cannot mix BigInt and other types
console.log(123n + 456n); // 579n
```

## Mental Model

Think of JavaScript's primitive types as the fundamental building blocks:

- **Strings**: Sequences of characters for text representation
- **Numbers**: Numeric values (both whole and decimal numbers)
- **Booleans**: Logical switches (on/off, yes/no)
- **Undefined**: A variable that exists but has no assigned value yet
- **Null**: An intentionally empty or non-existent value
- **Symbols**: Unique identifiers to prevent naming collisions
- **BigInts**: Precise representations of very large integers

Primitive values are **immutable** and passed by **value**, not reference. This means that when you "change" a primitive, you're actually creating a new value rather than modifying the existing one.

## Common Pitfalls

### 1. Mistaking primitive wrapper objects for primitives

```javascript
const primitiveString = "hello";
const objectString = new String("hello");

console.log(typeof primitiveString); // "string"
console.log(typeof objectString); // "object"
console.log(primitiveString === objectString); // false
```

### 2. Confusion with `typeof` results

```javascript
console.log(typeof null); // "object" - historical bug
console.log(typeof NaN); // "number" - despite meaning "Not a Number"
console.log(typeof (function() {})); // "function" - though functions are objects
```

### 3. Precision issues with floating-point numbers

```javascript
console.log(0.1 + 0.2); // 0.30000000000000004
console.log(3.0 - 2.1); // 0.9000000000000001
```

### 4. Confusing null and undefined

```javascript
// undefined often indicates something unintentional:
let someVar;
console.log(someVar); // undefined - variable declared but not assigned

// null usually indicates deliberate absence:
const userSettings = {
  theme: "dark",
  notifications: null // explicitly set to no value
};
```

## Best Practices

1. **Use literals instead of constructors**: Prefer `"string"` over `new String("string")`.

2. **Be careful with numeric comparisons**: Use techniques like `Math.abs(a - b) < Number.EPSILON` for floating-point comparisons.

3. **Use strict equality (`===`)**: This prevents unexpected type coercion.

4. **Be explicit with null and undefined**:
   - Use `undefined` when a variable has not been assigned a value
   - Use `null` when you want to explicitly indicate "no value"

5. **Use appropriate methods for string operations**: Strings have many built-in methods that are optimized for common operations.

6. **Be aware of truthy and falsy values**: Understand how JavaScript coerces values in boolean contexts.

## Practice Problems

1. Write a function that accurately adds decimal numbers (like 0.1 + 0.2) to get the expected mathematical result.

2. Create a function that counts the number of unique characters in a string. How would you use a Set to accomplish this?

3. Write a function that determines whether a value is a primitive type or not.

4. Create a function that takes a string and returns a new string with the first letter of each word capitalized.

5. Implement a function that safely retrieves nested properties from an object without throwing errors if a property doesn't exist.

## Real-World Application

### Form validation in a web application

```javascript
function validateForm(formData) {
  // Validating string (must be non-empty)
  if (!formData.username || formData.username.trim() === "") {
    return { valid: false, error: "Username is required" };
  }
  
  // Validating number (must be within range)
  const age = Number(formData.age);
  if (isNaN(age) || age < 18 || age > 120) {
    return { valid: false, error: "Age must be a number between 18 and 120" };
  }
  
  // Validating email format using a regular expression
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(formData.email)) {
    return { valid: false, error: "Email is invalid" };
  }
  
  return { valid: true };
}

// Example usage:
const userInput = {
  username: "JohnDoe",
  age: "25",
  email: "john.doe@example.com"
};

console.log(validateForm(userInput)); // { valid: true }
```

### Data sanitization in a chat application

```javascript
function sanitizeChatMessage(message) {
  // Convert to string if not already
  if (typeof message !== "string") {
    message = String(message);
  }
  
  // Trim whitespace
  message = message.trim();
  
  // Replace potentially harmful characters
  message = message.replace(/</g, "&lt;").replace(/>/g, "&gt;");
  
  // Check if message is empty after sanitization
  if (message === "") {
    return null; // Using null to represent "no valid message"
  }
  
  return message;
}

console.log(sanitizeChatMessage("  Hello!  ")); // "Hello!"
console.log(sanitizeChatMessage("<script>alert('XSS')</script>")); // "&lt;script&gt;alert('XSS')&lt;/script&gt;"
console.log(sanitizeChatMessage("   ")); // null
```

## Key Takeaways

1. JavaScript has seven primitive types: String, Number, Boolean, Undefined, Null, Symbol, and BigInt.

2. Primitive values are immutable - once created, they cannot be changed.

3. Primitives are passed by value, not by reference, meaning that when you assign a primitive to a new variable or pass it to a function, a copy is created.

4. JavaScript's type system has some quirks to be aware of:
   - `typeof null` returns "object" (a historical bug)
   - Floating-point arithmetic can lead to precision issues
   - Type coercion can create unexpected results when using loose equality (`==`)

5. Understanding primitives thoroughly provides a solid foundation for JavaScript programming, as they form the basis of all other data structures in the language.

6. Each primitive type has corresponding wrapper objects (String, Number, Boolean, etc.) that provide useful methods and properties.

7. JavaScript performs automatic boxing (wrapping primitives in objects) when you call methods on primitive values, which is why `"hello".toUpperCase()` works despite `"hello"` being a primitive.
