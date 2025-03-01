# Quick JavaScript Expression vs Statement Guide

## Core Concept
- Expressions produce values while statements perform actions
- 🧮 Mental model: Expressions are like math calculations that give you an answer; statements are like sentences that give instructions
- Visual representation:
  ```
  ┌───────────────────────────────────────────┐
  │ JavaScript Code Structure                 │
  ├─────────────────┬─────────────────────────┤
  │ Expressions     │ Evaluate to a value     │
  │                 │ Can be assigned         │
  │                 │ Can be passed as args   │
  ├─────────────────┼─────────────────────────┤
  │ Statements      │ Perform actions         │
  │                 │ Cannot be assigned      │
  │                 │ Control program flow    │
  └─────────────────┴─────────────────────────┘
  ```

## Key Mechanics
```javascript
// Expressions (produce a value)
5 + 5                // Arithmetic expression → 10
"Hello " + "world"   // String expression → "Hello world"
x = 10               // Assignment expression → 10
functionCall()       // Function call expression → return value
isTrue ? "Yes" : "No" // Conditional expression → "Yes" or "No"

// Statements (perform actions)
let x = 5;           // Variable declaration statement
if (x > 0) {         // If statement
  console.log(x);
}
for (let i = 0; i < 3; i++) { // For loop statement
  // Do something
}
function doSomething() {} // Function declaration statement
return x;            // Return statement

// Expression statements
console.log("Hi");   // Expression used as a statement
x++;                 // Expression used as a statement
```

- 💡 **Expressions** always **produce a value** and can be used anywhere a value is expected
- 📝 **Statements** are about **performing actions** and form the basic structure of a program
- 🔄 **Expression statements** are expressions used where statements are expected (followed by `;`)
- ⚙️ Not all statements can be expressions, but expressions can be used as statements

## Interview Mastery
**Q1: What's the difference between function declarations and function expressions?**  
A: Function declarations are statements (`function foo() {}`) that are hoisted entirely. Function expressions (`const foo = function() {}`) produce a value (the function) that can be assigned to a variable, passed as an argument, or returned from another function. Only the variable name is hoisted, not the function body.

**Q2: Why can't you use statements like `if` or `for` in certain contexts?**  
A: Statements don't produce values, so they can't be used where JavaScript expects an expression, such as inside template literals, as arguments to functions, on the right side of assignments, or in array/object literals. Only expressions work in these contexts.

**Related Concepts:**
- 🔄 **IIFE (Immediately Invoked Function Expression)** - A function expression that's executed immediately after creation
- 📦 **Expression-oriented programming** - A style favoring expressions over statements for more composable code

**Remember:** Understanding the distinction between expressions and statements is crucial for writing correct JavaScript, especially when working with function expressions, arrow functions, and modern features like destructuring. A good rule of thumb: if it produces a value, it's an expression; if it performs an action, it's a statement.
