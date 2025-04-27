
# JavaScript Questions 1-10: Core Concepts Explained

## 1. Hoisting and Variable Declarations

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}

sayHi();
```

**Output: `undefined` and `ReferenceError`**

**Explanation:**
This question demonstrates the key difference between `var` and `let/const` when it comes to hoisting:

- Variables declared with `var` are hoisted to the top of their scope and initialized with `undefined`
- Variables declared with `let` and `const` are also hoisted but remain in a "temporal dead zone" until their declaration is reached

In the function execution:
1. When `console.log(name)` runs, `name` exists in memory (hoisted) but has the value `undefined`
2. When `console.log(age)` runs, JavaScript knows `age` exists (hoisted) but it cannot be accessed yet (temporal dead zone), resulting in a `ReferenceError`

**Key Takeaway:** `var` variables can be accessed before declaration (with value `undefined`), while `let` and `const` variables cannot be accessed before declaration.

## 2. Block Scope vs. Function Scope with Closures

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

**Output: `3 3 3` and `0 1 2`**

**Explanation:**
This question illustrates function scope vs. block scope and how closures capture variables:

- First loop uses `var`: `i` is function-scoped, and there's only one `i` in memory
- Second loop uses `let`: `i` is block-scoped, so each iteration creates a new `i` variable

The `setTimeout` callbacks execute after the loops finish:
1. In the first loop, all three callbacks reference the same `i` variable, which is 3 when they execute
2. In the second loop, each callback captures a different block-scoped `i` variable (0, 1, and 2)

**Key Takeaway:** `let` creates a new variable binding for each loop iteration, which is particularly important with asynchronous operations like `setTimeout`.

## 3. Regular Functions vs. Arrow Functions (`this` context)

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

**Output: `20` and `NaN`**

**Explanation:**
This question highlights the critical difference in how `this` works between regular and arrow functions:

- Regular functions: `this` is determined by how the function is called (the object before the dot)
- Arrow functions: `this` is inherited from the surrounding scope where the function is defined

1. When `shape.diameter()` is called, `this` refers to the `shape` object, so `this.radius` is 10
2. When `shape.perimeter()` is called, the arrow function doesn't have its own `this` but inherits it from the surrounding scope (global/window), where `this.radius` is undefined

**Key Takeaway:** Use regular functions when you need `this` to refer to the object the method is called on. Use arrow functions when you want to preserve the `this` value from the surrounding context.

## 4. Unary Operators and Type Coercion

```javascript
+true;
!'Lydia';
```

**Output: `1` and `false`**

**Explanation:**
This question demonstrates unary operators and type coercion in JavaScript:

- The unary `+` operator converts its operand to a number
  - `+true` converts `true` to the number `1`
- The logical NOT operator `!` converts its operand to a boolean and then negates it
  - `'Lydia'` is a truthy value, so `!'Lydia'` evaluates to `false`

**Key Takeaway:** Unary operators can force type conversion in JavaScript, which is essential to understand when working with dynamic typing.

## 5. Object Properties and Access Methods

```javascript
const bird = {
  size: 'small',
};

const mouse = {
  name: 'Mickey',
  small: true,
};
```

**Which one is true? `mouse.bird.size` is not valid**

**Explanation:**
This question tests your understanding of object property access:

- Dot notation (`object.property`): Accesses a property with the exact name specified
- Bracket notation (`object[expression]`): Evaluates the expression and uses the result as the property name

1. `mouse.bird` tries to access a property named "bird" on the mouse object, which doesn't exist, so it's `undefined`
2. Trying to access `undefined.size` results in an error

Other expressions:
- `mouse[bird.size]` is valid - evaluates to `mouse["small"]`, which is `true`
- `mouse[bird["size"]]` is valid - evaluates to `mouse["small"]`, which is `true`

**Key Takeaway:** Be careful with property access chains; if any part evaluates to `undefined`, accessing further properties will cause an error.

## 6. Object References

```javascript
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```

**Output: `Hello`**

**Explanation:**
This question illustrates how objects are passed by reference in JavaScript:

1. We create an object `c` with a property `greeting`
2. We assign `c` to `d` - this doesn't create a copy; both variables now reference the same object in memory
3. We modify the object via the `c` reference
4. When we access the object via the `d` reference, we see the changes

**Key Takeaway:** When you assign an object to a variable, you're assigning a reference to that object, not creating a copy. Multiple variables can reference the same object.

## 7. Primitive vs. Object Equality

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

**Output: `true` `false` `false`**

**Explanation:**
This question explores equality comparisons between primitives and objects:

- `==` (loose equality): Performs type coercion before comparison
- `===` (strict equality): Compares without type coercion

1. `a == b`: The object `b` is coerced to a primitive number `3`, which equals `a` (3)
2. `a === b`: `a` is a primitive number, but `b` is an object, so they are different types
3. `b === c`: `b` is an object, but `c` is a primitive number, so they are different types

**Key Takeaway:** Primitives and their object wrapper counterparts are different types in JavaScript. Use `===` when you want to ensure both value and type equality.

## 8. Static Methods in Classes

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
console.log(freddie.colorChange('orange'));
```

**Output: `TypeError`**

**Explanation:**
This question demonstrates how static methods work in JavaScript classes:

- Static methods are called on the class itself, not on instances of the class
- Static methods use `this` to refer to the class constructor, not the instances

When we try to call `freddie.colorChange('orange')`:
1. JavaScript looks for a method named `colorChange` on the `freddie` instance
2. The method doesn't exist on the instance (it's static, so it exists on the `Chameleon` class)
3. A `TypeError` is thrown because we're trying to call a function that doesn't exist

To call the static method correctly: `Chameleon.colorChange('orange')`

**Key Takeaway:** Static methods belong to the class, not instances. They're useful for utility functions related to the class that don't depend on instance properties.

## 9. Global Variables and Typos

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

**Output: `{}`**

**Explanation:**
This question reveals a common pitfall in JavaScript: accidental global variable creation.

1. We declare a variable `greeting` but never assign a value to it
2. We try to assign an empty object to what we think is `greeting` but due to a typo, it's `greetign`
3. Since `greetign` is not declared, JavaScript creates it as a property on the global object (window)
4. Logging `greetign` outputs the empty object

This behavior only happens in non-strict mode. In strict mode (`"use strict";`), this would throw a `ReferenceError`.

**Key Takeaway:** Always use `let`, `const`, or `var` when declaring variables, and consider using strict mode to catch these kinds of errors.

## 10. Functions as Objects

```javascript
function bark() {
  console.log('Woof!');
}

bark.animal = 'dog';
```

**Output: Nothing, this is totally fine!**

**Explanation:**
This question illustrates that functions in JavaScript are first-class objects:

1. Functions are objects and can have properties just like any other object
2. We add a property `animal` with the value `'dog'` to the `bark` function

This doesn't affect how the function executes; you can still call `bark()` and it will log `'Woof!'`.

**Key Takeaway:** Functions in JavaScript are objects that can be invoked. You can add properties to them, pass them as arguments, return them from other functions, and do anything else you can do with objects.
