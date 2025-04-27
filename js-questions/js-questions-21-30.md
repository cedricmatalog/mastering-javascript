# JavaScript Questions 21-30: Evaluations, Storage & Event Loop

## 21. The `eval()` Function

```javascript
const sum = eval('10*10+5');
```

**Value of `sum`: `105`**

**Explanation:**
This question explores the `eval()` function in JavaScript:

1. `eval()` takes a string as an argument and executes it as JavaScript code
2. The string `'10*10+5'` is interpreted as a mathematical expression
3. JavaScript evaluates `10*10` first (following order of operations), resulting in `100`
4. Then it adds `5`, resulting in `105`

The `eval()` function is powerful but generally discouraged for several reasons:
- It poses security risks (especially with user-provided strings)
- It's slower than regular code (no pre-compilation)
- It can make debugging difficult
- It may lead to unexpected scoping issues

**Key Takeaway:** While `eval()` can execute JavaScript code from strings, it's best avoided in favor of safer alternatives like using functions, objects, or JSON parsing.

## 22. Session Storage Duration

```javascript
sessionStorage.setItem('cool_secret', 123);
```

**How long is `cool_secret` accessible? When the user closes the tab.**

**Explanation:**
This question tests understanding of browser storage mechanisms:

1. `sessionStorage` provides a way to store key-value pairs in the browser
2. Data stored in `sessionStorage` persists only for the duration of the page session
3. When the tab/window is closed, the data is cleared

Contrast with other storage options:
- `localStorage`: Persists until explicitly cleared, even across browser restarts
- Cookies: Persist based on their expiration date, sent with HTTP requests

**Key Takeaway:** Use `sessionStorage` for temporary data needed only during the current session, `localStorage` for longer-term client-side storage, and cookies for data that needs to be sent to the server.

## 23. Variable Redeclaration with `var`

```javascript
var num = 8;
var num = 10;

console.log(num);
```

**Output: `10`**

**Explanation:**
This question demonstrates variable redeclaration behavior with `var`:

1. Variables declared with `var` can be redeclared in the same scope
2. The second declaration essentially overwrites the first
3. The final value of `num` is `10`

Contrast with `let` and `const`:
- `let` and `const` cannot be redeclared in the same scope (would result in `SyntaxError`)
- They follow block scoping rules instead of function scoping

**Key Takeaway:** `var` allows redeclaration, which can lead to unexpected behavior and bugs. Modern JavaScript prefers `let` and `const` for their stricter scoping rules and prevention of redeclaration.

## 24. Object Keys and Set Type Conversion

```javascript
const obj = { 1: 'a', 2: 'b', 3: 'c' };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty('1');
obj.hasOwnProperty(1);
set.has('1');
set.has(1);
```

**Output: `true` `true` `false` `true`**

**Explanation:**
This question tests key type handling in objects and Sets:

Object keys:
1. Object keys are always converted to strings internally
2. `obj.hasOwnProperty('1')` checks for a property named `'1'` (string)
3. `obj.hasOwnProperty(1)` - the number `1` is converted to string `'1'` before lookup
4. Both return `true` because `'1'` exists as a key

Set values:
1. `Set` preserves the type of its values (no automatic conversion)
2. `set.has('1')` looks for string `'1'`, which doesn't exist in the Set
3. `set.has(1)` looks for number `1`, which does exist

**Key Takeaway:** Objects automatically convert keys to strings, while Sets maintain the original type of their values. This distinction is important when working with numeric or other non-string keys.

## 25. Object Property Overrides

```javascript
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);
```

**Output: `{ a: "three", b: "two" }`**

**Explanation:**
This question demonstrates object literal property behavior:

1. When an object has multiple properties with the same name, the last one "wins"
2. The property `a` is defined twice with values `'one'` and `'three'`
3. The later definition (`a: 'three'`) overwrites the earlier one
4. The final object has `a` with value `'three'` and `b` with value `'two'`

This behavior is specified by the ECMAScript standard and works consistently across all browsers.

**Key Takeaway:** Duplicate property names in object literals are allowed but result in only the last value being kept. This is rarely used intentionally and is usually the result of a coding error.

## 26. JavaScript Global Execution Context

**The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.**

**Answer: True**

**Explanation:**
This question verifies understanding of JavaScript's execution context:

1. When JavaScript code begins execution, it creates a global execution context
2. The global execution context provides:
   - The global object (`window` in browsers, `global` in Node.js)
   - The `this` keyword (which points to the global object in the global context)

This forms the foundation for JavaScript's runtime environment and is where global variables are stored.

**Key Takeaway:** Understanding execution context is crucial for grasping JavaScript's scope and `this` behavior. The global execution context is the baseline environment where your code operates.

## 27. Loop Control with `continue`

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

**Output: `1` `2` `4`**

**Explanation:**
This question examines loop control flow with the `continue` statement:

1. The loop counts from 1 to 4 (`i < 5`)
2. For each iteration, it checks if `i === 3`
3. When `i` equals `3`, the `continue` statement skips the rest of the loop body for that iteration
4. As a result, `3` is never logged, but all other values (1, 2, and 4) are

Other loop control statements:
- `break`: Exits the loop entirely
- `return`: Exits the entire function (if inside a function)

**Key Takeaway:** The `continue` statement allows you to skip the current iteration without terminating the entire loop, which is useful for filtering or conditional processing within loops.

## 28. Prototype Modification

```javascript
String.prototype.giveLydiaPizza = () => {
  return 'Just give Lydia pizza already!';
};

const name = 'Lydia';

console.log(name.giveLydiaPizza())
```

**Output: `"Just give Lydia pizza already!"`**

**Explanation:**
This question demonstrates prototype modification and primitive wrapping:

1. We add a method `giveLydiaPizza` to the `String.prototype`
2. All string instances inherit properties and methods from `String.prototype`
3. When we call a method on a string primitive, JavaScript temporarily wraps it in a `String` object
4. This wrapper object has access to the prototype methods
5. The method executes and returns the string `'Just give Lydia pizza already!'`

**Key Takeaway:** You can extend built-in types like String by adding methods to their prototype, but this is generally discouraged as it can lead to unexpected behavior in shared codebases and conflicts with future JavaScript features.

## 29. Object Properties with Object Keys

```javascript
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

**Output: `456`**

**Explanation:**
This question explores object property names when using objects as keys:

1. When you use an object as a property key, JavaScript converts it to a string using `toString()`
2. For regular objects, `toString()` returns `"[object Object]"`
3. Both `b` and `c` are converted to the same string: `"[object Object]"`
4. `a[b]` and `a[c]` both refer to the same property: `a["[object Object]"]`
5. First, we set `a["[object Object]"] = 123`
6. Then, we set `a["[object Object]"] = 456`, overwriting the previous value
7. When we log `a[b]`, we're accessing `a["[object Object]"]`, which is `456`

**Key Takeaway:** Objects used as property keys are converted to strings. To use objects as unique keys, consider using a `Map` object, which allows objects as keys without conversion.

## 30. Event Loop and Asynchronous JavaScript

```javascript
const foo = () => console.log('First');
const bar = () => setTimeout(() => console.log('Second'));
const baz = () => console.log('Third');

bar();
foo();
baz();
```

**Output: `First` `Third` `Second`**

**Explanation:**
This question demonstrates JavaScript's event loop and execution order:

1. `bar()` is called first, which sets up a `setTimeout` callback but doesn't execute it immediately
2. The callback function is sent to the Browser API to be executed after the specified delay (1ms)
3. JavaScript continues execution with `foo()`, which immediately logs `'First'`
4. Next, `baz()` runs and logs `'Third'`
5. After the main execution stack is empty and the timer has elapsed, the callback from `setTimeout` is moved to the task queue
6. The event loop picks up the callback from the queue and executes it, logging `'Second'`

**Key Takeaway:** JavaScript's event loop processes the main execution stack first, then handles callbacks from asynchronous operations (like timers, I/O, promises) after the stack is empty. Understanding this model is crucial for working with asynchronous code.
