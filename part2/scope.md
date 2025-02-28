# Function Scope, Block Scope and Lexical Scope

## Concept Introduction
Scope in JavaScript defines the accessibility and visibility of variables throughout your code. It determines where variables can be accessed or referenced. JavaScript has three primary types of scope:

1. **Function Scope**: Variables defined within a function are only accessible within that function.
2. **Block Scope**: Variables defined within a block (code inside curly braces) are only accessible within that block (introduced with ES6 via `let` and `const`).
3. **Lexical Scope**: Variables are accessible based on where they are defined in the source code.

Understanding scope is crucial for writing predictable code, preventing variable conflicts, and managing data throughout your application.

## Deep Dive

### Function Scope
In JavaScript, variables declared with `var` have function scope, meaning they are accessible anywhere within the function where they are declared, including nested blocks.

```javascript
function showExample() {
  var functionScoped = "I'm available throughout the function";
  
  if (true) {
    var alsoFunctionScoped = "I too am available throughout the function";
    console.log(functionScoped); // Accessible here
  }
  
  console.log(alsoFunctionScoped); // Also accessible here
}

showExample();
console.log(functionScoped); // Error: functionScoped is not defined
```

Function scope creates a "bubble" of visibility around variables, confining them to the function where they're declared. This helps prevent polluting the global scope and creating name collisions.

### Block Scope
Introduced in ES6, `let` and `const` declarations provide block scope, meaning variables are only accessible within the block (curly braces) where they are defined:

```javascript
function blockScopeExample() {
  if (true) {
    let blockScoped = "I'm only available in this block";
    const alsoBlockScoped = "Me too!";
    var notBlockScoped = "I'm available throughout the function";
    
    console.log(blockScoped); // Accessible
    console.log(alsoBlockScoped); // Accessible
  }
  
  console.log(notBlockScoped); // Accessible
  console.log(blockScoped); // Error: blockScoped is not defined
}
```

Block scope provides more predictable variable behavior and helps prevent issues like variable hoisting problems and accidental redeclarations.

### Lexical Scope
Lexical scope (also called static scope) means that variable access is determined by where variables are declared in the source code. Inner functions have access to variables in their outer/parent functions:

```javascript
function outer() {
  const outerVar = "I'm in the outer function";
  
  function inner() {
    const innerVar = "I'm in the inner function";
    console.log(outerVar); // Can access outerVar
  }
  
  inner();
  console.log(innerVar); // Error: innerVar is not defined
}
```

Lexical scope forms the basis for closures in JavaScript (covered in the next chapter).

### Global Scope
Variables declared outside any function or block have global scope and are accessible throughout your entire program:

```javascript
const globalVar = "I'm available everywhere";

function anyFunction() {
  console.log(globalVar); // Accessible
}
```

Excessive use of global variables is generally considered poor practice as it can lead to naming conflicts and code that's difficult to maintain.

### The Temporal Dead Zone
With `let` and `const`, variables exist in a "temporal dead zone" from the start of the block until the declaration is executed:

```javascript
function temporalExample() {
  console.log(usingVar); // undefined (due to hoisting)
  console.log(usingLet); // ReferenceError: Cannot access before initialization
  
  var usingVar = "I'm hoisted but initialized here";
  let usingLet = "I exist but am not accessible before this line";
}
```

This is an important distinction that helps catch potential errors in your code.

## Mental Model
Think of scope as a series of nested containers:

1. The outermost container is the global scope.
2. Each function creates its own container inside the parent container.
3. Each block (with `let`/`const`) creates an even smaller container.
4. Code can "look outward" from its container to access variables in larger containers.
5. Code cannot "look inward" to access variables in more deeply nested containers.

You can visualize this as a set of nested boxes, where each box can see outward but not inward. Variable lookup always starts in the innermost container and works outward until a match is found (or an error occurs).

## Common Pitfalls

### 1. Confusion with Hoisting
Variables declared with `var` are hoisted (moved to the top of their containing function during execution), but their initialization isn't:

```javascript
function hoistingExample() {
  console.log(hoisted); // undefined, not a ReferenceError
  var hoisted = "This variable was hoisted";
}
```

### 2. Forgetting That `var` Ignores Block Scope
Unlike `let` and `const`, `var` declarations are function-scoped, not block-scoped:

```javascript
if (true) {
  var functionScoped = "I'm available outside the block";
  let blockScoped = "I'm not";
}

console.log(functionScoped); // Works
console.log(blockScoped); // ReferenceError
```

### 3. Shadowing Variables
Variables in inner scopes can shadow (override) variables with the same name in outer scopes:

```javascript
const value = "global";

function shadowExample() {
  const value = "local";
  console.log(value); // "local", not "global"
}
```

This can create confusion if not managed carefully.

### 4. Loop Variables with `var`
Using `var` in loops creates a single variable that's shared across all iterations:

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // Logs 3, 3, 3
}

// Using let fixes this:
for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 100); // Logs 0, 1, 2
}
```

## Best Practices

### 1. Prefer `const` and `let` Over `var`
Use `const` by default, `let` when you need to reassign, and avoid `var` in modern JavaScript:

```javascript
// Good practice
const pi = 3.14159; // Won't change
let counter = 0;    // Will change
```

### 2. Minimize Global Variables
Avoid polluting the global namespace. Instead, use modules, functions, or IIFE patterns:

```javascript
// Instead of global variables
const myApp = (function() {
  const privateVar = "Not accessible outside";
  return {
    publicMethod: function() {
      console.log(privateVar);
    }
  };
})();
```

### 3. Keep Functions Pure When Possible
Try to use parameters and local variables rather than accessing outer scope variables:

```javascript
// Less ideal
let total = 0;
function addToTotal(value) {
  total += value; // Side effect
}

// Better
function add(a, b) {
  return a + b; // Pure function
}
let total = add(total, value);
```

### 4. Be Explicit About Scope
Use clear naming conventions and structure to make variable scope obvious:

```javascript
function processUser(userData) {
  const user = {
    name: userData.name,
    // Other user properties
  };
  
  function formatUserName() {
    // Clearly depends on the outer user variable
    return user.name.toUpperCase();
  }
  
  // Rest of the function
}
```

## Practice Problems

### Problem 1: Identify the Scope
For each variable in the following code, identify its scope and explain why:

```javascript
const globalVar = "I'm global";

function outer() {
  const outerVar = "I'm in outer";
  let counter = 0;
  
  if (true) {
    const blockVar = "I'm in a block";
    var functionVar = "I'm function-scoped";
    counter++;
  }
  
  function inner() {
    const innerVar = "I'm in inner";
    console.log(outerVar); // What can be accessed here?
  }
}
```

### Problem 2: Fix the Loop
Fix the following code so it correctly logs 0, 1, 2, 3, 4 (with a 1-second delay between each):

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}
```

### Problem 3: Closures and Scope
What will the following code output and why?

```javascript
function createFunctions() {
  const functions = [];
  
  for (var i = 0; i < 3; i++) {
    functions.push(function() {
      console.log(i);
    });
  }
  
  return functions;
}

const fns = createFunctions();
fns[0]();
fns[1]();
fns[2]();
```

## Real-World Application
Understanding scope is fundamental in many real-world scenarios:

1. **Module Patterns**: Modern JavaScript modules use scope to encapsulate code and expose only what's necessary, following the principle of least privilege.

2. **React Hooks**: Hooks like `useState` leverage lexical scope to maintain state between renders while keeping implementation details private.

3. **Closures in Event Handlers**: UI frameworks frequently use closures (based on lexical scope) to create event handlers that retain access to component state.

4. **Library Design**: Well-designed libraries use scope to avoid polluting the global namespace while providing a clean public API.

Example from React:
```javascript
function UserProfile() {
  // State is scoped to this component
  const [user, setUser] = useState(null);
  
  // This effect has access to the user state via lexical scope
  useEffect(() => {
    async function fetchUser() {
      const response = await fetch('/api/user');
      const userData = await response.json();
      setUser(userData);
    }
    fetchUser();
  }, []);
  
  // The JSX has access to the user state
  return (
    <div>
      {user ? user.name : 'Loading...'}
    </div>
  );
}
```

## Key Takeaways

1. **Function Scope**: Variables declared with `var` are accessible throughout the function, regardless of block nesting.

2. **Block Scope**: Variables declared with `let` and `const` are accessible only within the block where they're defined.

3. **Lexical Scope**: Variables are accessible based on where they are defined in the source code, with inner functions having access to outer function variables.

4. **Hoisting Behavior**: `var` declarations are hoisted (initialized as `undefined`), while `let` and `const` declarations are hoisted but not initialized (temporal dead zone).

5. **Best Practices**: Prefer `const` and `let` over `var`, minimize global variables, and be explicit about scope.

6. **Global Scope**: Variables declared outside any function or block are globally accessible, but should be used sparingly.

7. **Scoping Rules**: JavaScript's scope rules form the foundation for advanced patterns like closures and module systems.
