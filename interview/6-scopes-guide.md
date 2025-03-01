# Quick JavaScript Scope Guide

## Core Concept
- Scope defines the accessibility and visibility of variables in JavaScript code
- 🏠 Mental model: Think of scope as nested houses - each inner house can see items from outer houses, but outer houses can't see inside inner ones
- Visual representation:
  ```
  ┌─────────────────── Global Scope ───────────────────┐
  │                                                    │
  │ let globalVar = 'visible everywhere';              │
  │                                                    │
  │ ┌─────────────── Function Scope ─────────────────┐ │
  │ │                                                │ │
  │ │ function myFunc() {                            │ │
  │ │   let functionVar = 'only visible in myFunc';  │ │
  │ │                                                │ │
  │ │   ┌───────────── Block Scope ─────────────────┐│ │
  │ │   │                                           ││ │
  │ │   │ if (true) {                               ││ │
  │ │   │   let blockVar = 'only in this block';    ││ │
  │ │   │ }                                         ││ │
  │ │   └───────────────────────────────────────────┘│ │
  │ │                                                │ │
  │ └────────────────────────────────────────────────┘ │
  │                                                    │
  └────────────────────────────────────────────────────┘
  ```

## Key Mechanics
```javascript
// Function scope (var)
function testFunctionScope() {
  var functionScoped = "I'm function scoped";
  
  if (true) {
    var alsoFunctionScoped = "I'm also function scoped";
  }
  
  console.log(functionScoped);      // "I'm function scoped"
  console.log(alsoFunctionScoped);  // "I'm also function scoped"
}

// Block scope (let/const)
function testBlockScope() {
  let functionScoped = "I'm function scoped";
  
  if (true) {
    let blockScoped = "I'm block scoped";
    const alsoBlockScoped = "I'm also block scoped";
    console.log(functionScoped);    // "I'm function scoped"
  }
  
  console.log(blockScoped);         // ReferenceError: blockScoped is not defined
}

// Lexical scope (closures)
function outer() {
  let outerVar = "I'm from outer function";
  
  function inner() {
    console.log(outerVar);  // Can access outerVar due to lexical scoping
  }
  
  return inner;
}

const innerFunc = outer();
innerFunc();  // "I'm from outer function"
```

- 🌍 **Global scope** variables are accessible throughout the entire program
- 🔒 **Function scope** (`var`) variables are accessible anywhere within the function
- 📦 **Block scope** (`let`/`const`) variables are only accessible within their block `{}`
- 🧠 **Lexical scope** (static scope) means functions can access variables from their containing scope

## Interview Mastery
**Q1: What's the key difference between var, let, and const regarding scope?**  
A: `var` is function-scoped (accessible throughout the function regardless of blocks), while `let` and `const` are block-scoped (only accessible within their declaring block). Additionally, `var` declarations are hoisted with initial value `undefined`, `let` and `const` are hoisted but not initialized (Temporal Dead Zone), and `const` cannot be reassigned.

**Q2: What is the Temporal Dead Zone in JavaScript?**  
A: The Temporal Dead Zone (TDZ) is the period between entering a scope where a variable is declared with `let`/`const` and the actual declaration line. During this zone, accessing the variable results in a ReferenceError, unlike `var` which returns `undefined`.

**Related Concepts:**
- 🔄 **Hoisting** - JavaScript's behavior of moving declarations to the top of their scope
- 📚 **Closures** - Functions that maintain access to variables from their parent scope even after the parent function has executed

**Remember:** JavaScript uses lexical scoping, meaning a function can access variables from its own scope, any parent scopes, and the global scope—but not from sibling or child scopes. Block scoping with `let`/`const` provides better control over variable visibility compared to function scoping with `var`.
