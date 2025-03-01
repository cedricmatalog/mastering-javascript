# Partial Applications, Currying, Compose and Pipe Guide

## Core Concept

- **Partial Application**: Converting a function that takes multiple arguments into a function that takes fewer arguments by pre-filling some values.
- **Currying**: Transforming a function that takes multiple arguments into a sequence of functions, each taking a single argument.
- **Compose/Pipe**: Functions that combine multiple functions into a single function, with data flowing right-to-left (compose) or left-to-right (pipe).

🧩 **Mental Model**: Think of these as LEGO bricks for functions—small, reusable pieces that snap together to build complex structures.

```
// Visual Representation

┌─────────┐     ┌─────────┐     ┌─────────┐
│ func1   │────▶│ func2   │────▶│ func3   │    Pipe: Left to Right
└─────────┘     └─────────┘     └─────────┘

┌─────────┐     ┌─────────┐     ┌─────────┐
│ func3   │◀────│ func2   │◀────│ func1   │    Compose: Right to Left
└─────────┘     └─────────┘     └─────────┘

┌─────────────────┐
│ add(a,b,c)      │     Original Function
└─────────────────┘
        ↓
┌─────────────────┐
│ add(5)(b)(c)    │     Curried Function
└─────────────────┘
        ↓
┌─────────────────┐
│ add5(b,c)       │     Partially Applied
└─────────────────┘
```

---

## Key Mechanics

```javascript
// Currying
const multiply = (a) => (b) => a * b;
const double = multiply(2);
console.log(double(5)); // Output: 10

// Partial Application
const greet = (greeting, name) => `${greeting}, ${name}!`;
const sayHello = greeting.bind(null, "Hello");
console.log(sayHello("World")); // Output: "Hello, World!"

// Compose
const compose = (f, g) => (x) => f(g(x));
const addOne = x => x + 1;
const double = x => x * 2;
const addOneThenDouble = compose(double, addOne);
console.log(addOneThenDouble(5)); // Output: 12 (5+1=6, 6*2=12)

// Pipe
const pipe = (f, g) => (x) => g(f(x));
const doubleThenAddOne = pipe(double, addOne);
console.log(doubleThenAddOne(5)); // Output: 11 (5*2=10, 10+1=11)
```

🔄 **Function Transformation**: Currying and partial application **transform** functions without changing their behavior, making them more **composable**.

🧰 **Reusability**: These techniques create specialized functions from general ones, promoting **DRY** (Don't Repeat Yourself) principles.

🔍 **Purity**: These patterns work best with **pure functions** that have no side effects and always return the same output for the same input.

⚡ **Performance**: Partially applied functions can **memoize** values, potentially improving performance for repeated operations.

---

## Interview Mastery

**Q: What's the difference between partial application and currying?**
A: Partial application creates a new function by fixing some parameters of the original function, while currying transforms a function to return a series of unary (single-argument) functions. Currying always produces a unary function chain, while partial application can fix any number of arguments.

**Q: Implement a compose function that works with any number of functions.**
```javascript
const compose = (...fns) => (x) => fns.reduceRight((acc, fn) => fn(acc), x);
```

🔗 **Related Concept**: **Higher-Order Functions** 🚀 - Functions that take other functions as arguments or return functions. Currying, partial application, compose, and pipe are all examples of higher-order functions.

🔄 **Related Concept**: **Function Pipelining** 📊 - A software design pattern that chains operations together, with the output of one function becoming the input of the next, similar to Unix pipes.

**Remember**: Functional programming techniques like currying, partial application, compose, and pipe allow you to build complex logic from simple, reusable pieces—transforming functions into versatile building blocks that can be assembled in countless ways.
