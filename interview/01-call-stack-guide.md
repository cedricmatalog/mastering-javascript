# Quick JavaScript Call Stack Guide

## Core Concept

- The call stack is JavaScript's mechanism for keeping track of function calls and their execution contexts
- 📚 Mental model: Think of it as a stack of books where you can only add or remove from the top
- Visual representation:
  ```
  ┌───────────────┐
  │ function3()   │ ← Most recently called (top)
  ├───────────────┤
  │ function2()   │
  ├───────────────┤
  │ function1()   │
  ├───────────────┤
  │ main()        │ ← First called (bottom)
  └───────────────┘
  ```

## Key Mechanics

```javascript
function first() {
  console.log("Inside first function");
  second();
  console.log("Back to first");
}

function second() {
  console.log("Inside second function");
}

first();
// Output:
// "Inside first function"
// "Inside second function"
// "Back to first"
```

- 🔄 JavaScript is **single-threaded** - can only execute one piece of code at a time
- 📥 Each function call creates a new **execution context** that's pushed onto the stack
- 📤 When a function completes, its context is **popped** off the stack
- 💥 Stack Overflow occurs when too many functions pile up without returning (e.g., infinite recursion)

## Interview Mastery

**Q1: What happens if the call stack exceeds its size limit?**  
A: JavaScript throws a "Maximum call stack size exceeded" error (stack overflow), typically caused by infinite recursion or extremely deep function nesting.

**Q2: How does asynchronous code execution work with the call stack?**  
A: Async operations (like setTimeout or fetch) are delegated to the Web APIs environment, then their callbacks are queued in the callback queue and only pushed onto the call stack when it's empty, via the event loop.

**Related Concepts:**

- 🔄 **Event Loop** - Monitors the call stack and callback queue to handle async operations
- 🧩 **Execution Context** - The environment where JavaScript code is evaluated and executed

**Remember:** The call stack is JavaScript's "memory" of where it is in code execution—functions are pushed when called and popped when completed, always following a Last In, First Out (LIFO) order.
