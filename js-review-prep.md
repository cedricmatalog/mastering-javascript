# Mastering JavaScript: A Comprehensive Guide (Basics to Advanced)

## Introduction

Welcome to the comprehensive guide to JavaScript! This document aims to take you from the absolute basics to understanding advanced concepts and the surrounding ecosystem.

*   **What is JavaScript?**
    *   JavaScript (JS) is a high-level, interpreted (or just-in-time compiled), multi-paradigm programming language. It's best known as the scripting language for Web pages, but it's used in many non-browser environments as well (like Node.js for servers).
    *   **History and Evolution (ECMAScript):** JavaScript was created by Brendan Eich at Netscape in 1995. To standardize the language, it was submitted to ECMA International. ECMAScript is the *specification*, while JavaScript is the most popular *implementation* of that specification. New versions (ES6/ES2015, ES2016, etc.) add features annually.
    *   **Role in Web Development:**
        *   **Client-side:** Runs in the user's browser to make web pages interactive (handle events, manipulate HTML/CSS (DOM), make requests, etc.).
        *   **Server-side:** With environments like Node.js, JS can run on servers to build backends, APIs, interact with databases, etc.
    *   **JavaScript Engines:** These programs execute JS code. Examples include V8 (Chrome, Node.js), SpiderMonkey (Firefox), JavaScriptCore (Safari).

*   **Setting Up Your Environment**
    *   **Browser Developer Console:** The easiest way to start. Right-click on a webpage -> Inspect -> Console tab. You can type JS code directly.
    *   **Node.js:** Download and install from [nodejs.org](https://nodejs.org/). This allows you to run JS files from your terminal (`node yourfile.js`). It also includes `npm` (Node Package Manager).
    *   **Code Editors:** Use a text editor designed for code. Popular choices: VS Code (recommended, free, great extensions), Sublime Text, Atom, WebStorm (paid).
    *   **Linking JS to HTML:**
        *   **Internal:** `<script> // JS code here </script>` (usually placed before `</body>`)
        *   **External:** `<script src="path/to/your/script.js"></script>` (preferred for organization)

*   **Basic Syntax**
    *   **Statements & Semicolons (;):** Statements are instructions. Semicolons terminate statements. They are often *optional* due to Automatic Semicolon Insertion (ASI), but it's good practice to include them to avoid ambiguity.
    *   **Case Sensitivity:** `myVariable` is different from `myvariable`.
    *   **Comments:** Ignored by the engine. Used for explanations.
        *   Single-line: `// This is a comment`
        *   Multi-line: `/* This is a
                       multi-line comment */`
    *   **Whitespace:** Spaces, tabs, newlines are mostly ignored, used for readability.

---

## I. JavaScript Fundamentals

### 1. Variables & Data Types

*   **Variables:** Named containers for storing data values.
    *   **Declaring Variables:**
        *   `var`: Function-scoped (or global), hoisted. Older way, generally avoid.
        *   `let`: Block-scoped (`{}`), hoisted but not initialized (Temporal Dead Zone - TDZ). Allows reassignment. Preferred for variables that might change.
        *   `const`: Block-scoped, hoisted (TDZ). **Must** be initialized upon declaration. Cannot be *reassigned*. Preferred for variables that shouldn't change. (Note: for objects/arrays, the *contents* can still change, just not the variable assignment itself).

        ```javascript
        var oldVar = "I'm old";
        let changeableVar = 10;
        const constantVar = true;

        changeableVar = 15; // OK
        // constantVar = false; // TypeError: Assignment to constant variable.

        if (true) {
          let blockScoped = "Visible only here";
          var functionScoped = "Visible outside if"; // Avoid this pattern
        }
        console.log(blockScoped); // ReferenceError
        console.log(functionScoped); // "Visible outside if"
        ```
    *   **Variable Naming Conventions:** Use `camelCase`. Start with letters, `_`, or `$`. Cannot start with numbers. Cannot use reserved keywords (`if`, `let`, `const`, `function`, etc.).
    *   **Scope:** Determines the accessibility of variables.
        *   **Global Scope:** Declared outside any function/block. Accessible everywhere. (Avoid polluting the global scope).
        *   **Function Scope:** Declared inside a function (`var`). Accessible only within that function.
        *   **Block Scope:** Declared inside a block (`{}`) using `let` or `const`. Accessible only within that block.
    *   **Hoisting:** JavaScript's default behavior of moving declarations (not initializations) to the top of their current scope (function for `var`, block for `let`/`const`). `let`/`const` are hoisted but enter a "Temporal Dead Zone" until the declaration line, preventing access before declaration.

*   **Data Types:** The kind of value a variable holds.
    *   **Primitive Types:** Immutable (their value cannot be changed directly).
        *   `string`: Sequence of characters. Use single (`'`) or double (`"`) quotes, or backticks (`` ` ``) for template literals.
            ```javascript
            let greeting = "Hello";
            let name = 'World';
            let message = `Greeting: ${greeting}, Name: ${name}!`; // Template literal
            console.log(message.toUpperCase()); // Methods like toUpperCase()
            ```
        *   `number`: Numeric values (integers, floats). Includes special values `NaN` (Not-a-Number), `Infinity`, `-Infinity`.
            ```javascript
            let age = 30;
            let price = 99.99;
            let result = 0 / 0; // NaN
            let big = Infinity;
            ```
        *   `boolean`: Logical entity, can be `true` or `false`.
            ```javascript
            let isActive = true;
            let isLoggedIn = false;
            ```
        *   `null`: Represents the intentional absence of any object value. It's an assigned value.
            ```javascript
            let emptyValue = null;
            ```
        *   `undefined`: A variable that has been declared but not assigned a value. Also the default return value of functions that don't explicitly return anything.
            ```javascript
            let notAssigned; // undefined
            ```
        *   `symbol` (ES6): Unique and immutable primitive value, often used as object property keys.
            ```javascript
            const id = Symbol('uniqueId');
            const obj = { [id]: 123 };
            ```
        *   `bigint` (ES2020): Represents whole numbers larger than the maximum safe integer for `number`. Add `n` to the end.
            ```javascript
            const veryLargeNumber = 900719925474099199n;
            ```
    *   **Reference Type:** Mutable (their value *can* be changed). Variables hold a reference (memory address) to the value.
        *   `object`: Collection of key-value pairs (properties). Keys are usually strings (or Symbols), values can be any data type (including other objects or functions). Arrays, Functions, Dates, etc., are specialized objects.
            ```javascript
            let person = {
              firstName: "John",
              lastName: "Doe",
              age: 30
            };
            let numbers = [1, 2, 3, 4]; // Array is an object
            function greet() { console.log("Hi"); } // Function is an object
            ```

*   **Type Checking (`typeof`)**: Operator returns a string indicating the type of the unevaluated operand.
    ```javascript
    console.log(typeof "hello");   // "string"
    console.log(typeof 100);       // "number"
    console.log(typeof true);      // "boolean"
    console.log(typeof undefined); // "undefined"
    console.log(typeof null);      // "object" (historical quirk)
    console.log(typeof Symbol());  // "symbol"
    console.log(typeof 9n);        // "bigint"
    console.log(typeof {});        // "object"
    console.log(typeof []);        // "object" (Arrays are objects)
    console.log(typeof function(){}); // "function" (Functions are special objects)
    ```
    *Note the quirk with `typeof null` returning `"object"`. Use `value === null` for specific null checks.*

*   **Type Coercion & Conversion**: JavaScript often implicitly converts types (coercion). You can also explicitly convert them.
    *   **Implicit Coercion:** Automatic conversion during operations. Can lead to unexpected results.
        ```javascript
        console.log('5' + 3);     // "53" (String concatenation)
        console.log('5' - 3);     // 2 (String '5' coerced to number 5)
        console.log('5' * 3);     // 15
        console.log(5 + null);    // 5 (null coerced to 0)
        console.log(5 + true);    // 6 (true coerced to 1)
        console.log('5' == 5);    // true (== performs type coercion)
        console.log('5' === 5);   // false (=== checks type and value, no coercion)
        ```
    *   **Explicit Conversion:** Manually changing types.
        ```javascript
        let numStr = "123";
        let num = Number(numStr);         // 123 (number)
        let numInt = parseInt("45.6px"); // 45 (number)
        let numFloat = parseFloat("45.6"); // 45.6 (number)

        let val = 0;
        let boolVal = Boolean(val);       // false
        let strVal = String(100);         // "100" (string)
        ```

### 2. Operators

Operators perform operations on values (operands).

*   **Assignment Operators**: Assign values to variables.
    *   `=`: Assign (`let x = 5;`)
    *   `+=`, `-=`, `*=`, `/=`, `%=`, `**=`: Compound assignment (`x += 3;` is `x = x + 3;`)
*   **Arithmetic Operators**: Perform mathematical calculations.
    *   `+` (Addition), `-` (Subtraction), `*` (Multiplication), `/` (Division)
    *   `%` (Modulus - remainder of division)
    *   `**` (Exponentiation - ES2016)
    *   `++` (Increment - adds 1), `--` (Decrement - subtracts 1) - Can be prefix (`++x`) or postfix (`x++`).
*   **Comparison Operators**: Compare two values, return `true` or `false`.
    *   `==` (Equal value - performs type coercion) - *Avoid using*
    *   `===` (Strict equal value and type) - *Prefer this*
    *   `!=` (Not equal value - performs type coercion) - *Avoid using*
    *   `!==` (Strict not equal value and type) - *Prefer this*
    *   `>` (Greater than), `<` (Less than)
    *   `>=` (Greater than or equal to), `<=` (Less than or equal to)
*   **Logical Operators**: Combine boolean expressions.
    *   `&&` (Logical AND): `true` if *both* operands are true. (Short-circuits: if first is false, second is not evaluated).
    *   `||` (Logical OR): `true` if *at least one* operand is true. (Short-circuits: if first is true, second is not evaluated).
    *   `!` (Logical NOT): Inverts boolean value (`!true` is `false`).
    *   *(Used often for default values: `const setting = userValue || defaultValue;`)*
*   **Bitwise Operators**: Operate on the binary representation of numbers (less common in web dev).
    *   `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (Left shift), `>>` (Sign-propagating right shift), `>>>` (Zero-fill right shift)
*   **Ternary Operator**: Conditional operator, shorthand for `if/else`.
    *   `condition ? valueIfTrue : valueIfFalse`
    ```javascript
    let age = 20;
    let status = (age >= 18) ? "Adult" : "Minor"; // status is "Adult"
    ```
*   **Other Operators**:
    *   `typeof`: Returns the type of a variable (see above).
    *   `instanceof`: Checks if an object is an instance of a particular constructor/class. `obj instanceof Array`
    *   `in`: Checks if a property exists in an object (or its prototype chain). `'name' in person`
    *   `delete`: Removes a property from an object. `delete person.age;`
    *   `new`: Creates an instance of an object from a constructor function or class. `const today = new Date();`
    *   `void`: Evaluates an expression and returns `undefined`.

### 3. Control Flow

Determines the order in which code is executed.

*   **Conditional Statements**: Execute code based on conditions.
    *   **`if`**: Executes code if a condition is true.
        ```javascript
        let temp = 15;
        if (temp < 20) {
          console.log("It's cool.");
        }
        ```
    *   **`else`**: Executes code if the `if` condition is false.
        ```javascript
        if (temp > 30) {
          console.log("It's hot.");
        } else {
          console.log("It's not hot.");
        }
        ```
    *   **`else if`**: Chain multiple conditions.
        ```javascript
        if (temp < 0) {
          console.log("Freezing!");
        } else if (temp < 20) {
          console.log("Cool.");
        } else {
          console.log("Warm or Hot.");
        }
        ```
    *   **`switch`**: Efficient alternative to long `if/else if` chains for checking a single variable against multiple values.
        ```javascript
        let day = new Date().getDay(); // 0 = Sunday, 1 = Monday, ...
        let dayName;

        switch (day) {
          case 0:
            dayName = "Sunday";
            break; // IMPORTANT: Stops execution from falling through
          case 6:
            dayName = "Saturday";
            break;
          default: // Executes if no case matches
            dayName = "Weekday";
            // No break needed here if it's the last one
        }
        console.log(`Today is ${dayName}.`);
        ```

*   **Loops**: Repeat a block of code.
    *   **`for` loop**: Good when you know the number of iterations.
        *   Syntax: `for (initialization; condition; final-expression)`
        ```javascript
        for (let i = 0; i < 5; i++) { // i from 0 to 4
          console.log(`Iteration ${i}`);
        }
        ```
    *   **`while` loop**: Good when the number of iterations is unknown, loop continues as long as the condition is true.
        ```javascript
        let count = 0;
        while (count < 3) {
          console.log(`While count: ${count}`);
          count++;
        }
        ```
    *   **`do...while` loop**: Similar to `while`, but the code block executes *at least once* before the condition is checked.
        ```javascript
        let input;
        do {
          // input = prompt("Enter 'quit' to exit:"); // Example for browser
          console.log("Processing input..."); // Runs at least once
          input = (input === 'quit') ? 'quit' : 'continue'; // Simulate input for demo
        } while (input !== 'quit');
        ```
    *   **`for...in` loop**: Iterates over the *enumerable property keys* (usually strings) of an object. Order not guaranteed. Avoid using on Arrays.
        ```javascript
        const user = { name: "Alice", role: "Admin", active: true };
        for (const key in user) {
          // It's good practice to check if the property is directly on the object
          if (Object.hasOwnProperty.call(user, key)) {
            console.log(`${key}: ${user[key]}`);
          }
        }
        ```
    *   **`for...of` loop** (ES6): Iterates over the *values* of iterable objects (Arrays, Strings, Maps, Sets, etc.). Preferred for iterating over array values.
        ```javascript
        const colors = ["red", "green", "blue"];
        for (const color of colors) {
          console.log(color);
        }

        const message = "Hi";
        for (const char of message) {
          console.log(char);
        }
        ```
    *   **`break`**: Exits the current loop or switch statement entirely.
    *   **`continue`**: Skips the rest of the current loop iteration and proceeds to the next one.

*   **Truthy and Falsy Values**: In boolean contexts (like `if` conditions), values are implicitly coerced to `true` or `false`.
    *   **Falsy values:** `false`, `0`, `-0`, `0n` (BigInt zero), `""` (empty string), `null`, `undefined`, `NaN`.
    *   **Truthy values:** Everything else (including `"0"`, `"false"`, `[]`, `{}`).
    ```javascript
    if ([]) { // Array is truthy
        console.log("Empty array is truthy");
    }
    if (0) { // 0 is falsy
        console.log("This won't print");
    } else {
        console.log("Zero is falsy");
    }
    ```

### 4. Functions

Reusable blocks of code that perform a specific task.

*   **Defining Functions**:
    *   **Function Declaration:** Hoisted. Can be called before definition in the code.
        ```javascript
        function greet(name) {
          console.log(`Hello, ${name}!`);
        }
        ```
    *   **Function Expression:** Not hoisted (variable declaration is, but assignment isn't). Often assigned to variables or passed as arguments. Can be anonymous.
        ```javascript
        const farewell = function(name) {
          console.log(`Goodbye, ${name}.`);
        }; // Semicolon often used here

        const add = function sum(a, b) { // Named function expression (name 'sum' useful for debugging)
            return a + b;
        }
        ```
    *   **Arrow Functions (ES6):** Concise syntax. Lexical `this` binding (inherits `this` from the surrounding scope). Implicit return for single expressions. Not suitable for methods that need their own `this` or constructor functions.
        ```javascript
        // Basic syntax
        const multiply = (a, b) => {
          return a * b;
        };

        // Implicit return (if only one expression)
        const square = x => x * x;

        // Single parameter doesn't need parentheses
        const log = message => console.log(message);

        // No parameters need empty parentheses
        const getRandom = () => Math.random();

        // Returning an object literal needs parentheses
        const createUser = (name, age) => ({ name: name, age: age });
        ```

*   **Calling Functions**: Execute the function's code. Use the function name followed by parentheses `()`, passing any required arguments.
    ```javascript
    greet("Bob"); // Output: Hello, Bob!
    farewell("Alice"); // Output: Goodbye, Alice.
    let product = multiply(5, 4); // product is 20
    console.log(square(3)); // Output: 9
    ```

*   **Parameters vs. Arguments**:
    *   **Parameters:** Variables listed inside the parentheses in the function definition.
    *   **Arguments:** Actual values passed to the function when it is called.
    *   **Default Parameters (ES6):** Assign default values if an argument is not provided or is `undefined`.
        ```javascript
        function registerUser(username, plan = "Free") {
          console.log(`Registering ${username} with plan: ${plan}`);
        }
        registerUser("Charlie"); // Output: Registering Charlie with plan: Free
        registerUser("Dana", "Premium"); // Output: Registering Dana with plan: Premium
        ```
    *   **Rest Parameters (`...`) (ES6):** Collects an indefinite number of arguments into an array. Must be the *last* parameter.
        ```javascript
        function sumAll(...numbers) { // 'numbers' will be an array
          let total = 0;
          for (const num of numbers) {
            total += num;
          }
          return total;
        }
        console.log(sumAll(1, 2, 3)); // Output: 6
        console.log(sumAll(10, 20, 30, 40)); // Output: 100
        ```

*   **Return Values (`return` statement)**: Functions often compute a value. The `return` statement specifies the value the function should output. If omitted, the function returns `undefined`. Execution stops after `return`.
    ```javascript
    function calculateArea(width, height) {
      if (width <= 0 || height <= 0) {
        return 0; // Return early for invalid input
      }
      const area = width * height;
      return area; // Return the calculated area
    }
    let myArea = calculateArea(10, 5); // myArea is 50
    ```

*   **Function Scope Revisited (Lexical Scoping)**: Functions create their own scope. Variables defined inside a function are not accessible from outside. Inner functions can access variables from their outer (parent) function scopes. This is called Lexical Scoping (or Static Scoping).

*   **Immediately Invoked Function Expressions (IIFE)**: Define and execute a function immediately. Used to create a private scope, avoiding global namespace pollution. Less common now with ES6 modules.
    ```javascript
    (function() {
      // Variables here are private to this IIFE
      var privateVar = "Secret";
      console.log("IIFE executed!");
      console.log(privateVar);
    })(); // The final () executes the function

    // Arrow function IIFE
    (() => {
        console.log("Arrow IIFE executed!");
    })();
    ```

*   **Closures**: A closure is the combination of a function and the lexical environment (the scope) within which that function was declared. This means an inner function has access to its outer function's variables and parameters, *even after the outer function has finished executing*.
    ```javascript
    function createCounter() {
      let count = 0; // This variable is "closed over"

      return function() { // This inner function is the closure
        count++;
        console.log(count);
        return count;
      };
    }

    const counter1 = createCounter(); // counter1 holds the inner function
    const counter2 = createCounter(); // counter2 holds a *different* inner function with its own count

    counter1(); // Output: 1
    counter1(); // Output: 2
    counter2(); // Output: 1 (independent count)
    ```
    *Closures are fundamental for concepts like data privacy, callbacks, and functional programming.*

*   **Higher-Order Functions**: Functions that operate on other functions, either by taking them as arguments or by returning them (or both). Array methods like `map`, `filter`, `reduce` are common examples. `createCounter` above is also a higher-order function because it returns a function.
    ```javascript
    function multiplier(factor) {
      // Returns a new function that multiplies by 'factor'
      return function(number) {
        return number * factor;
      };
    }

    const double = multiplier(2); // double is now a function
    const triple = multiplier(3); // triple is now a function

    console.log(double(5)); // Output: 10
    console.log(triple(5)); // Output: 15
    ```

### 5. Data Structures

Ways to organize and store data.

*   **Objects**: Unordered collections of key-value pairs. Keys are usually strings (or Symbols).
    *   **Object Literals (`{}`):** Most common way to create objects.
        ```javascript
        const car = {
          make: "Toyota",
          model: "Camry",
          year: 2021,
          isRunning: false,
          start: function() { // Method (function as a property)
            this.isRunning = true;
            console.log("Engine started.");
          },
          stop() { // Shorthand method syntax (ES6)
            this.isRunning = false;
            console.log("Engine stopped.");
          }
        };
        ```
    *   **Properties and Methods:** Properties store data values, methods store functions that operate on the object's data (often using `this`).
    *   **Accessing Properties:**
        *   Dot Notation: `objectName.propertyName` (Use when key is a valid identifier and known)
        *   Bracket Notation: `objectName['propertyNameString']` (Use when key is dynamic, has spaces/special chars, or is a variable)
        ```javascript
        console.log(car.make); // Toyota
        console.log(car['model']); // Camry

        let propName = 'year';
        console.log(car[propName]); // 2021
        ```
    *   **Adding, Modifying, Deleting Properties:**
        ```javascript
        car.color = "Blue"; // Add new property
        car.year = 2022;   // Modify existing property
        delete car.isRunning; // Remove property
        ```
    *   **Object Methods:** Built-in functions for working with objects.
        *   `Object.keys(obj)`: Returns an array of the object's own enumerable property keys (strings).
        *   `Object.values(obj)`: Returns an array of the object's own enumerable property values.
        *   `Object.entries(obj)`: Returns an array of `[key, value]` pairs for the object's own enumerable properties.
        *   `Object.assign(target, ...sources)`: Copies enumerable own properties from source objects to a target object.
        *   `Object.freeze(obj)`: Prevents modifications to the object's direct properties.
        *   `Object.hasOwnProperty.call(obj, prop)`: Checks if an object has a specific *own* property (not inherited).
        ```javascript
        console.log(Object.keys(car));   // ["make", "model", "year", "start", "stop", "color"] (order might vary)
        console.log(Object.values(car)); // ["Toyota", "Camry", 2022, ƒ, ƒ, "Blue"]
        console.log(Object.entries(car)); // [["make", "Toyota"], ["model", "Camry"], ...]
        ```
    *   **Iterating over Objects:** Use `for...in` (checks inherited properties too, use `hasOwnProperty`) or `Object.keys/values/entries` with `forEach` or `for...of`.
        ```javascript
        // Using Object.keys and forEach
        Object.keys(car).forEach(key => {
          console.log(`${key} -> ${car[key]}`);
        });
        ```

*   **Arrays**: Ordered, zero-indexed lists of values. Arrays are a special type of object in JavaScript.
    *   **Array Literals (`[]`):** Most common way to create arrays.
        ```javascript
        const fruits = ["Apple", "Banana", "Cherry"];
        const mixed = [1, "two", true, null, { id: 3 }, [4, 5]]; // Can hold mixed types
        const empty = [];
        ```
    *   **Accessing Elements:** Use bracket notation with the zero-based index.
        ```javascript
        console.log(fruits[0]); // Apple
        console.log(fruits[2]); // Cherry
        console.log(fruits[3]); // undefined (index out of bounds)
        fruits[1] = "Blueberry"; // Modify element
        ```
    *   **Array Properties:**
        *   `length`: Gets or sets the number of elements in the array.
        ```javascript
        console.log(fruits.length); // 3
        fruits.length = 2; // Truncates the array
        console.log(fruits); // ["Apple", "Blueberry"]
        ```
    *   **Common Array Methods:** (Many mutate the original array, others return a new one)
        *   **Mutation (Modify original array):**
            *   `push(item1, ...)`: Adds items to the *end*. Returns new length.
            *   `pop()`: Removes item from the *end*. Returns removed item.
            *   `shift()`: Removes item from the *beginning*. Returns removed item.
            *   `unshift(item1, ...)`: Adds items to the *beginning*. Returns new length.
            *   `splice(startIndex, deleteCount, item1, ...)`: Powerful tool to add/remove items anywhere. Returns array of removed items.
            *   `sort(compareFunction)`: Sorts items in place. Default sort is lexicographical (string-based)! Provide `compareFunction` for numbers.
            *   `reverse()`: Reverses items in place.
            *   `fill(value, start, end)`: Fills part of the array with a static value.
        *   **Iteration (Don't modify original array directly, often use callbacks):**
            *   `forEach(callback(element, index, array))`: Executes a function for each element. Doesn't return anything meaningful.
            *   `map(callback(element, index, array))`: Creates a *new* array populated with the results of calling a provided function on every element.
            *   `filter(callback(element, index, array))`: Creates a *new* array with all elements that pass the test implemented by the provided function (callback returns true/false).
            *   `reduce(callback(accumulator, currentValue, index, array), initialValue)`: Executes a reducer function on each element, resulting in a single output value (e.g., sum, combined object).
            *   `reduceRight(...)`: Same as `reduce`, but starts from the end of the array.
            *   `every(callback(...))`: Tests whether *all* elements pass the test. Returns boolean.
            *   `some(callback(...))`: Tests whether *at least one* element passes the test. Returns boolean.
        *   **Access/Searching (Don't modify original array):**
            *   `indexOf(item, fromIndex)`: Returns the first index of an item, or -1 if not found. Uses strict equality (`===`).
            *   `lastIndexOf(item, fromIndex)`: Returns the last index of an item, or -1 if not found.
            *   `includes(item, fromIndex)`: Returns `true` or `false` if an item exists. Handles `NaN` correctly (unlike `indexOf`).
            *   `find(callback(...))`: Returns the *value* of the first element that satisfies the provided testing function. Returns `undefined` if none found.
            *   `findIndex(callback(...))`: Returns the *index* of the first element that satisfies the provided testing function. Returns -1 if none found.
            *   `slice(startIndex, endIndex)`: Returns a *shallow copy* of a portion of an array into a new array object. `endIndex` is *not* included. Doesn't modify original.
            *   `concat(array2, ...)`: Returns a *new* array merging this array with other arrays/values.
            *   `join(separator)`: Joins all elements into a string, separated by the specified separator (default is comma `,`).
        *   **ES6+ Array Methods:**
            *   `Array.from(iterableOrArrayLike)`: Creates a new array instance from an iterable (like Set, Map, String) or array-like object (like `arguments` or NodeList).
            *   `Array.of(item1, item2, ...)`: Creates a new array instance with a variable number of arguments, regardless of number or type.
            *   `copyWithin(targetIndex, startIndex, endIndex)`: Shallow copies part of an array to another location *within the same array* and returns it, without modifying its length. (Mutates)
            *   `flat(depth)`: Creates a new array with all sub-array elements concatenated into it recursively up to the specified depth (default 1).
            *   `flatMap(callback)`: Equivalent to `map()` followed by `flat(1)`. Efficient.
        ```javascript
        const numbers = [1, 2, 3, 4, 5];

        // map: Create new array with doubled values
        const doubled = numbers.map(num => num * 2); // [2, 4, 6, 8, 10]

        // filter: Create new array with only even numbers
        const evens = numbers.filter(num => num % 2 === 0); // [2, 4]

        // reduce: Calculate sum
        const sum = numbers.reduce((total, num) => total + num, 0); // 15

        // find: Find first number greater than 3
        const found = numbers.find(num => num > 3); // 4

        // forEach: Log each number
        numbers.forEach(num => console.log(`Processing ${num}`));

        // push (mutates)
        numbers.push(6); // numbers is now [1, 2, 3, 4, 5, 6]

        // slice (doesn't mutate)
        const firstThree = numbers.slice(0, 3); // [1, 2, 3]
        ```

---

## II. Intermediate JavaScript

### 6. `this` Keyword

One of the most confusing aspects of JavaScript. The value of `this` depends on *how* a function is called (its execution context).

*   **Understanding Context:** `this` refers to the object that is currently executing the code.
*   **`this` in Global Scope:**
    *   In browsers (non-strict mode): `this` refers to the `window` object.
    *   In Node.js: `this` refers to `module.exports` (initially an empty object) in the top level of a module, or `global` inside functions in non-strict mode.
    *   **Strict Mode (`'use strict';`):** `this` is `undefined` in the global scope and inside functions called without an explicit context. *Always use strict mode to avoid confusion.*
*   **`this` inside Functions (Non-Method Calls):**
    *   Non-Strict Mode: `this` refers to the global object (`window` in browsers).
    *   Strict Mode: `this` is `undefined`.
    ```javascript
    'use strict';
    function showThis() {
      console.log(this);
    }
    showThis(); // undefined
    ```
*   **`this` inside Methods (Object Context):** When a function is called *as a method* of an object (`object.method()`), `this` refers to the object the method was called on (the object before the dot).
    ```javascript
    'use strict';
    const user = {
      name: "Alice",
      greet() {
        console.log(`Hello, my name is ${this.name}.`); // 'this' refers to 'user'
      }
    };
    user.greet(); // Hello, my name is Alice.

    const greetFunc = user.greet; // Get reference to the function
    // greetFunc(); // TypeError: Cannot read properties of undefined (reading 'name') - 'this' is undefined here
    ```
*   **`this` in Constructor Functions (`new` keyword):** When a function is called with the `new` keyword (a constructor call):
    1.  A new empty object `{}` is created.
    2.  This new object is set as the `this` context for the function call.
    3.  The function body executes, modifying `this`.
    4.  If the function doesn't explicitly return an object, the new object created in step 1 is returned.
    ```javascript
    'use strict';
    function Person(name, age) {
      // 'this' is the new empty object being created
      this.name = name;
      this.age = age;
      // implicitly returns 'this'
    }
    const person1 = new Person("Bob", 40);
    console.log(person1.name); // Bob
    ```
*   **`this` in Arrow Functions:** Arrow functions do *not* have their own `this` binding. Instead, they inherit `this` from the *lexical scope* in which they were defined (the surrounding code's `this` value). This is often very useful, especially in callbacks.
    ```javascript
    'use strict';
    const counter = {
      count: 0,
      start() {
        console.log("Start method 'this':", this); // 'this' is 'counter'
        setInterval(() => {
          // Arrow function inherits 'this' from 'start' method
          this.count++;
          console.log(this.count); // 'this' correctly refers to 'counter'
        }, 1000);
      }
    };
    // counter.start(); // Uncomment to run

    // Compare with a regular function callback (would lose 'this')
    const counterBroken = {
        count: 0,
        start() {
            console.log("Start method 'this':", this); // 'this' is 'counterBroken'
            setInterval(function() { // Regular function callback
                 // 'this' here is likely window (non-strict) or undefined (strict)
                 console.log("Regular func this:", this);
                 // this.count++; // Would cause an error in strict mode
            }, 1000);
        }
    };
    // counterBroken.start(); // Uncomment to see the difference
    ```
*   **Explicit Binding (`call()`, `apply()`, `bind()`):** Allow you to manually set the value of `this` when calling a function.
    *   `function.call(thisArg, arg1, arg2, ...)`: Calls the function with `this` set to `thisArg`, passing arguments individually.
    *   `function.apply(thisArg, [argsArray])`: Calls the function with `this` set to `thisArg`, passing arguments as an array.
    *   `function.bind(thisArg, arg1, ...)`: Creates a *new function* that, when called, will have its `this` keyword set to `thisArg`. You can also pre-set arguments ("partial application"). The original function is not called immediately.
    ```javascript
    'use strict';
    function introduce(greeting, punctuation) {
      console.log(`${greeting}, I'm ${this.name}${punctuation}`);
    }

    const personA = { name: "Charlie" };
    const personB = { name: "Dana" };

    // Using call
    introduce.call(personA, "Hi", "!"); // Hi, I'm Charlie!

    // Using apply
    introduce.apply(personB, ["Hello", "."]); // Hello, I'm Dana.

    // Using bind
    const introduceCharlie = introduce.bind(personA, "Hey"); // Create a new function bound to personA with 'Hey' pre-filled
    introduceCharlie("?"); // Hey, I'm Charlie?
    ```

### 7. Object-Oriented Programming (OOP) in JavaScript

JavaScript uses a *prototypal inheritance* model, different from classical inheritance found in languages like Java or C++. ES6 Classes provide a more familiar syntax but are essentially syntactic sugar over prototypes.

*   **Prototypes & Prototypal Inheritance:**
    *   Every JavaScript object has a hidden internal property (often accessible via `__proto__`, but officially via `Object.getPrototypeOf()`) that links it to another object called its *prototype*.
    *   **Prototype Chain:** When you try to access a property or method on an object, JavaScript first looks at the object itself. If it doesn't find it, it looks at the object's prototype. If not found there, it looks at the prototype's prototype, and so on, up the chain until it finds the property/method or reaches `null` (the end of the chain).
    *   `Object.create(proto)`: Creates a new object with the specified prototype object.
        ```javascript
        const animal = {
          type: 'Unknown',
          makeSound() {
            console.log('Some generic sound');
          }
        };

        const dog = Object.create(animal); // 'dog' inherits from 'animal'
        dog.breed = 'Labrador';
        dog.makeSound = function() { // Overrides the inherited method
          console.log('Woof!');
        };

        console.log(dog.breed); // Labrador (own property)
        console.log(dog.type);  // Unknown (inherited from animal prototype)
        dog.makeSound();       // Woof! (own method)

        const cat = Object.create(animal);
        cat.type = 'Feline';
        // cat.makeSound(); // Some generic sound (inherited method)

        console.log(Object.getPrototypeOf(dog) === animal); // true
        console.log(Object.getPrototypeOf(animal)); // Points to Object.prototype
        ```

*   **Constructor Functions:** Functions used with the `new` keyword to create multiple objects with similar properties and methods. By convention, they start with a capital letter. Methods are typically added to the constructor's `prototype` property to be shared among all instances (saving memory).
    ```javascript
    function Vehicle(make, model) {
      // Properties set directly on the instance
      this.make = make;
      this.model = model;
      // Avoid putting methods directly here for efficiency
    }

    // Methods added to the prototype - shared by all instances
    Vehicle.prototype.getInfo = function() {
      return `${this.make} ${this.model}`;
    };

    Vehicle.prototype.startEngine = function() {
        console.log(`${this.make} ${this.model}'s engine starting...`);
    }

    const car1 = new Vehicle("Honda", "Civic");
    const car2 = new Vehicle("Ford", "Focus");

    console.log(car1.getInfo()); // Honda Civic
    car2.startEngine();          // Ford Focus's engine starting...

    // Both car1 and car2 share the same getInfo and startEngine functions via the prototype chain
    console.log(car1.getInfo === car2.getInfo); // true
    console.log(Object.getPrototypeOf(car1) === Vehicle.prototype); // true
    ```

*   **ES6 Classes:** A more modern syntax for creating objects and handling inheritance, built on top of the existing prototypal inheritance mechanism.
    *   **`class` syntax:** Defines a class.
    *   **`constructor` method:** Special method for creating and initializing objects created with a class. Executed when `new ClassName()` is called.
    *   **Instance Methods & Properties:** Defined directly inside the class body. They become part of the class's `prototype`. Instance properties are usually set inside the `constructor`.
    *   **Static Methods & Properties (`static` keyword):** Belong to the class itself, not to instances. Called using `ClassName.staticMethod()`. Often used for utility functions related to the class.
    *   **Getters and Setters (`get`, `set`):** Special methods for getting and setting property values, allowing more control or calculated properties.
    *   **Inheritance (`extends` keyword):** Creates a subclass that inherits from a parent class.
    *   **`super()` keyword:** Used in the subclass `constructor` to call the parent class's constructor. Also used to call methods from the parent class (`super.parentMethod()`).

    ```javascript
    class Book {
      // Private fields (newer syntax, check browser/Node compatibility)
      #discountRate = 0.10; // Example private field

      // Static property
      static publisher = "Generic Books Inc.";

      constructor(title, author, price) {
        this.title = title;
        this.author = author;
        this._price = price; // Convention for "private" property before # syntax
      }

      // Instance method
      getSummary() {
        return `${this.title} by ${this.author}`;
      }

      // Getter
      get price() {
        return this._price * (1 - this.#discountRate);
      }

      // Setter
      set price(newPrice) {
        if (newPrice > 0) {
          this._price = newPrice;
        } else {
          console.error("Price must be positive.");
        }
      }

      // Static method
      static compareAuthors(book1, book2) {
        return book1.author === book2.author;
      }
    }

    // Inheritance
    class Ebook extends Book {
      constructor(title, author, price, format) {
        super(title, author, price); // Call parent constructor
        this.format = format;
      }

      // Override method
      getSummary() {
        // Call parent method using super
        return `${super.getSummary()} [${this.format}]`;
      }

      // Ebook specific method
      read() {
          console.log(`Opening ${this.title} in ${this.format} format...`);
      }
    }

    // Usage
    const book1 = new Book("The Hobbit", "J.R.R. Tolkien", 20);
    console.log(book1.getSummary()); // The Hobbit by J.R.R. Tolkien
    console.log(book1.price); // Access via getter (applies discount): 18
    book1.price = 25; // Access via setter
    console.log(book1.price); // 22.5

    const ebook1 = new Ebook("Dune", "Frank Herbert", 15, "PDF");
    console.log(ebook1.getSummary()); // Dune by Frank Herbert [PDF]
    ebook1.read(); // Opening Dune in PDF format...

    console.log(Book.publisher); // Access static property: Generic Books Inc.
    // console.log(book1.publisher); // undefined - static props are not on instances

    const book2 = new Book("Another Book", "J.R.R. Tolkien", 30);
    console.log(Book.compareAuthors(book1, book2)); // true (using static method)
    ```

### 8. Asynchronous JavaScript

JavaScript is single-threaded, meaning it can only execute one piece of code at a time. Asynchronous operations (like network requests, timers, file system operations in Node.js) allow the program to continue running other code while waiting for these long tasks to complete, preventing the main thread from blocking (becoming unresponsive).

*   **Synchronous vs. Asynchronous Code:**
    *   **Sync:** Code executes line by line, one after another. If a line takes a long time, the entire program waits.
    *   **Async:** Operations are initiated, but the program doesn't wait for them to finish. It continues executing subsequent code. A callback function, Promise, or async/await is used to handle the result when the async operation completes.
*   **The Event Loop:** The core mechanism enabling async behavior in JS environments (browsers, Node.js). It orchestrates the execution of code, handling events and callbacks.
    *   **Call Stack:** Where function calls are pushed onto when executed and popped off when completed. Follows LIFO (Last-In, First-Out).
    *   **Web APIs / C++ APIs (Node):** Interfaces provided by the environment (browser/Node) for async operations (e.g., `setTimeout`, `fetch`, DOM events, `fs.readFile`). These run outside the JS main thread.
    *   **Callback Queue (Task Queue):** When an async operation completes (e.g., timer finishes, data arrives), its associated *callback function* is placed in this queue. Follows FIFO (First-In, First-Out).
    *   **Microtask Queue:** Holds callbacks for Promises (`.then`, `.catch`, `.finally`) and other microtasks (`queueMicrotask`). Has *higher priority* than the Callback Queue.
    *   **Event Loop Process:** Continuously checks if the Call Stack is empty. If it is, it first processes *all* tasks in the Microtask Queue, moving them one by one to the Call Stack for execution. Only after the Microtask Queue is empty does it take *one* task from the Callback Queue and move it to the Call Stack.

*   **Callbacks (The "Old" Way):** Functions passed as arguments to other functions, to be executed later when an async operation completes or an event occurs.
    *   **"Callback Hell" / Pyramid of Doom:** Nested callbacks can become deeply indented and hard to read/manage, especially with error handling at each level.
    ```javascript
    // Simulating async operations with setTimeout
    function step1(callback) {
      setTimeout(() => {
        console.log("Step 1 Complete");
        // Assume some result from step 1
        const result1 = 10;
        callback(null, result1); // Convention: error first, then result
      }, 500);
    }

    function step2(dataFrom1, callback) {
      setTimeout(() => {
        console.log("Step 2 Complete using data:", dataFrom1);
        const result2 = dataFrom1 * 2;
        callback(null, result2);
      }, 500);
    }

    function step3(dataFrom2, callback) {
       setTimeout(() => {
        console.log("Step 3 Complete using data:", dataFrom2);
        const result3 = dataFrom2 + 5;
        callback(null, result3);
       }, 500);
    }

    // Callback Hell Example
    step1((error1, data1) => {
      if (error1) {
        console.error("Error in Step 1:", error1);
      } else {
        step2(data1, (error2, data2) => {
          if (error2) {
            console.error("Error in Step 2:", error2);
          } else {
            step3(data2, (error3, data3) => {
              if (error3) {
                console.error("Error in Step 3:", error3);
              } else {
                console.log("Final Result:", data3); // Output: Final Result: 25
              }
            });
          }
        });
      }
    });
    ```

*   **Promises (ES6):** An object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. Provides a cleaner way to handle async code than callbacks.
    *   **States:**
        *   `pending`: Initial state, neither fulfilled nor rejected.
        *   `fulfilled` (or `resolved`): The operation completed successfully.
        *   `rejected`: The operation failed.
    *   **`.then(onFulfilled, onRejected)`:** Attaches callbacks to handle the fulfilled or rejected states. Returns a *new* Promise, allowing chaining. `onRejected` is optional; using `.catch` is preferred for error handling.
    *   **`.catch(onRejected)`:** Attaches a callback to handle only the rejected state. Syntactic sugar for `.then(null, onRejected)`.
    *   **`.finally(onFinally)`:** Attaches a callback that executes regardless of whether the Promise was fulfilled or rejected. Useful for cleanup. Returns a Promise.
    *   **Creating Promises (`new Promise(executor)`):** The `executor` function takes two arguments: `resolve` and `reject` (which are themselves functions). Call `resolve(value)` on success, `reject(error)` on failure.
        ```javascript
        function step1Promise() {
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              console.log("Step 1 Promise Complete");
              const result1 = 10;
              // Simulate potential error
              if (Math.random() > 0.8) {
                 reject(new Error("Step 1 Failed!"));
              } else {
                 resolve(result1);
              }
            }, 500);
          });
        }

        // Similary define step2Promise(data), step3Promise(data) returning Promises...
        function step2Promise(data) { return new Promise(res => setTimeout(() => { console.log('Step 2'); res(data * 2); }, 500)); }
        function step3Promise(data) { return new Promise(res => setTimeout(() => { console.log('Step 3'); res(data + 5); }, 500)); }

        // Chaining Promises
        step1Promise()
          .then(data1 => {
            console.log("Received from Step 1:", data1);
            return step2Promise(data1); // Return the next promise
          })
          .then(data2 => {
            console.log("Received from Step 2:", data2);
            return step3Promise(data2);
          })
          .then(data3 => {
            console.log("Final Result:", data3); // Final Result: 25
          })
          .catch(error => { // Catches errors from any preceding step in the chain
            console.error("An error occurred:", error.message);
          })
          .finally(() => {
            console.log("Promise chain finished (success or failure).");
          });
        ```
    *   **Promise Static Methods:**
        *   `Promise.all(iterable)`: Takes an iterable (e.g., array) of Promises. Returns a new Promise that fulfills when *all* promises in the iterable fulfill, with an array of their results. Rejects immediately if *any* promise rejects.
        *   `Promise.race(iterable)`: Returns a new Promise that fulfills or rejects as soon as *one* of the promises in the iterable fulfills or rejects, with the value or reason from that promise.
        *   `Promise.allSettled(iterable)`: Returns a new Promise that fulfills after *all* promises have settled (either fulfilled or rejected), with an array of objects describing the outcome of each promise (`{status: 'fulfilled', value: ...}` or `{status: 'rejected', reason: ...}`).
        *   `Promise.any(iterable)`: Returns a new Promise that fulfills as soon as *any* promise fulfills. Rejects only if *all* promises reject (with an `AggregateError`).

*   **Async/Await (ES2017):** Syntactic sugar built on top of Promises, making asynchronous code look and behave more like synchronous code, improving readability.
    *   **`async` keyword:** Used before a function declaration/expression. Makes the function implicitly return a Promise. The resolved value of the promise is whatever the `async` function returns.
    *   **`await` keyword:** Can *only* be used inside an `async` function. Pauses the execution of the `async` function until the Promise it's waiting for settles (fulfills or rejects). If fulfilled, it returns the resolved value. If rejected, it throws the rejection reason (error).
    *   **Error Handling:** Use standard `try...catch...finally` blocks for handling rejected Promises when using `await`.

    ```javascript
    // Assume step1Promise, step2Promise, step3Promise exist as defined before

    async function runSteps() {
      console.log("Starting async/await sequence...");
      try {
        const data1 = await step1Promise(); // Pauses here until step1 resolves
        console.log("Received from Step 1:", data1);

        const data2 = await step2Promise(data1); // Pauses here...
        console.log("Received from Step 2:", data2);

        const data3 = await step3Promise(data2); // Pauses here...
        console.log("Final Result:", data3); // Final Result: 25

        return data3; // The promise returned by runSteps will resolve with this value

      } catch (error) {
        console.error("An error occurred in async function:", error.message);
        // The promise returned by runSteps will reject with this error
        throw error; // Re-throw if needed

      } finally {
         console.log("Async function finished (try or catch).");
      }
    }

    // Calling the async function
    runSteps()
      .then(result => console.log("Async function succeeded with:", result))
      .catch(error => console.error("Async function failed with:", error.message));

    console.log("Async function initiated, but this logs before it finishes.");
    ```

### 9. Error Handling

Dealing with runtime errors gracefully.

*   **`try...catch...finally` blocks:** Used for handling exceptions in synchronous code and with `async/await`.
    *   **`try`:** Contains the code that might throw an error.
    *   **`catch (error)`:** Executes if an error occurs within the `try` block. The `error` object contains details about the error.
    *   **`finally`:** Executes *regardless* of whether an error occurred or not (even if there's a `return` in `try` or `catch`). Used for cleanup (e.g., closing files, releasing resources).
    ```javascript
    function divide(a, b) {
      try {
        if (b === 0) {
          // Create and throw a custom error
          throw new Error("Division by zero is not allowed.");
        }
        const result = a / b;
        console.log("Result:", result);
        return result; // Return if successful
      } catch (err) {
        console.error("Error caught:", err.name, "-", err.message);
        // Handle the error, maybe return a default value or re-throw
        return undefined; // Indicate failure
      } finally {
        console.log("Division attempt finished."); // Always runs
      }
    }

    divide(10, 2); // Result: 5, Division attempt finished.
    divide(10, 0); // Error caught: Error - Division by zero is not allowed., Division attempt finished.
    ```
*   **The `Error` Object:** When an error occurs, an `Error` object (or an object inheriting from it, like `TypeError`, `ReferenceError`) is created.
    *   `error.name`: The type of error (e.g., "Error", "TypeError").
    *   `error.message`: A human-readable description of the error.
    *   `error.stack`: (Non-standard, but common) A string containing the call stack trace leading to the error. Very useful for debugging.
*   **Throwing Custom Errors (`throw` statement):** You can create and throw your own errors using `throw new Error("Your message")` or custom error classes inheriting from `Error`. This signals an exceptional condition.
*   **Handling Errors in Promises:** Use the `.catch()` method on the promise chain (as shown in the Promises section) or `try...catch` with `async/await` (as shown in the Async/Await section). Unhandled promise rejections can crash Node.js applications or cause silent failures in browsers.
*   **Debugging Techniques:**
    *   **Browser DevTools:** Essential. Use the Console (`console.log`, `console.warn`, `console.error`, `console.table`, etc.), Debugger (set breakpoints, step through code, inspect variables), Network tab (inspect requests), Application tab (check storage).
    *   **`console.log()`:** Simple but effective way to inspect variable values at different points.
    *   **`debugger;` statement:** Inserts a breakpoint in your code. If DevTools is open, execution will pause there.
    *   **Linters (ESLint):** Catch potential errors and enforce code style *before* you run the code.

---

## III. JavaScript in the Browser (Client-Side)

Focuses on how JavaScript interacts with web pages.

### 10. Document Object Model (DOM)

The DOM is a programming interface for HTML and XML documents. It represents the page structure as a tree of objects (nodes). JavaScript can manipulate this tree to change the page's content, structure, and style dynamically.

*   **What is the DOM?** An object-based representation of the HTML document. Each HTML element, attribute, and piece of text is a node in the DOM tree. `document` is the root node representing the entire page.
*   **Selecting Elements:** Getting references to DOM nodes to work with them.
    *   **Legacy Methods:**
        *   `document.getElementById('elementId')`: Selects the single element with the specified ID. Fast.
        *   `document.getElementsByTagName('tagName')`: Selects a *live* HTMLCollection (array-like) of elements with the given tag name (e.g., 'p', 'div').
        *   `document.getElementsByClassName('className')`: Selects a *live* HTMLCollection of elements with the given class name.
        *   *(Live collections update automatically if the DOM changes)*
    *   **Modern Methods (Preferred):** Use CSS selectors.
        *   `document.querySelector('cssSelector')`: Selects the *first* element matching the specified CSS selector (e.g., '#myId', '.myClass', 'div > p'). Returns `null` if none found.
        *   `document.querySelectorAll('cssSelector')`: Selects a *static* NodeList (array-like) of all elements matching the CSS selector. Can iterate using `forEach`.
    ```javascript
    // Example HTML: <div id="main"><p class="content">Hello</p><p class="content">World</p></div>

    const mainDiv = document.getElementById('main');
    const paragraphsLegacy = document.getElementsByClassName('content'); // HTMLCollection

    const firstParagraph = document.querySelector('#main p.content'); // Selects the first <p>
    const allParagraphs = document.querySelectorAll('.content'); // NodeList

    console.log(firstParagraph.textContent); // Hello

    allParagraphs.forEach(p => {
      console.log(p.innerText);
    });
    ```

*   **Traversing the DOM:** Moving between nodes in the tree.
    *   `element.parentNode`, `element.parentElement`: Get the parent node/element.
    *   `element.childNodes`: Get a *live* NodeList of all child nodes (including text nodes, comment nodes).
    *   `element.children`: Get a *live* HTMLCollection of only child *elements*. (Usually preferred over `childNodes`).
    *   `element.firstChild`, `element.lastChild`: Get the first/last child *node*.
    *   `element.firstElementChild`, `element.lastElementChild`: Get the first/last child *element*.
    *   `element.nextSibling`, `element.previousSibling`: Get the next/previous sibling *node*.
    *   `element.nextElementSibling`, `element.previousElementSibling`: Get the next/previous sibling *element*.
    ```javascript
    const secondParagraph = allParagraphs[1]; // Assuming allParagraphs from above
    console.log(secondParagraph.previousElementSibling.textContent); // Hello
    console.log(firstParagraph.parentElement.id); // main
    ```

*   **Manipulating Elements:** Changing the content, attributes, or style.
    *   **Changing Content:**
        *   `element.innerHTML`: Gets or sets the HTML content *inside* the element. Be careful with setting `innerHTML` from untrusted sources due to XSS risks. Parses HTML string. Slower.
        *   `element.textContent`: Gets or sets the raw text content of the element and its descendants, ignoring HTML tags. Faster and safer for plain text.
        *   `element.innerText`: Similar to `textContent`, but takes CSS styling into account (e.g., doesn't include hidden text). Can trigger browser reflows (slower). `textContent` is generally preferred.
    *   **Changing Attributes:**
        *   `element.getAttribute('attrName')`: Gets the value of an attribute.
        *   `element.setAttribute('attrName', 'value')`: Sets the value of an attribute. Adds it if it doesn't exist.
        *   `element.removeAttribute('attrName')`: Removes an attribute.
        *   `element.hasAttribute('attrName')`: Checks if an attribute exists.
        *   *(Direct property access often works for standard attributes: `img.src = 'new.jpg'; input.checked = true;`)*
    *   **Changing Styles:**
        *   `element.style.propertyName = 'value'`: Sets *inline* styles (camelCase CSS properties: `backgroundColor`, `fontSize`). Good for dynamic, specific changes.
        *   `element.classList`: Provides methods to manipulate classes (preferred way to change styles defined in CSS).
            *   `element.classList.add('className1', 'className2')`
            *   `element.classList.remove('className')`
            *   `element.classList.toggle('className')`
            *   `element.classList.contains('className')`
            *   `element.classList.replace('oldClass', 'newClass')`
    ```javascript
    firstParagraph.textContent = "Greetings"; // Change text
    mainDiv.style.backgroundColor = 'lightblue'; // Set inline style
    mainDiv.setAttribute('data-id', 'container-123'); // Set custom data attribute

    allParagraphs.forEach(p => p.classList.add('highlight')); // Add 'highlight' class to all
    ```

*   **Creating and Adding Elements:** Dynamically adding new content.
    *   **Legacy Methods:**
        *   `document.createElement('tagName')`: Creates a new element node.
        *   `document.createTextNode('text')`: Creates a new text node.
        *   `parentElement.appendChild(childElement)`: Adds `childElement` as the *last* child of `parentElement`.
        *   `parentElement.insertBefore(newNode, referenceNode)`: Inserts `newNode` before `referenceNode` within `parentElement`.
        *   `parentElement.removeChild(childElement)`: Removes `childElement` from `parentElement`.
        *   `parentElement.replaceChild(newChild, oldChild)`: Replaces `oldChild` with `newChild`.
    *   **Modern Methods (More convenient):**
        *   `parentElement.append(nodeOrString1, nodeOrString2, ...)`: Appends nodes or strings at the end of the parent.
        *   `parentElement.prepend(nodeOrString1, ...)`: Appends nodes or strings at the beginning.
        *   `element.before(nodeOrString1, ...)`: Inserts nodes or strings before the element.
        *   `element.after(nodeOrString1, ...)`: Inserts nodes or strings after the element.
        *   `element.remove()`: Removes the element itself from the DOM.
        *   `element.replaceWith(nodeOrString1, ...)`: Replaces the element with the given nodes or strings.
    ```javascript
    // Create a new list item
    const newLi = document.createElement('li');
    newLi.textContent = 'New Item';

    // Assume an existing <ul id="myList"></ul>
    const list = document.querySelector('#myList');

    // Add it using modern append
    list.append(newLi);

    // Create another item and add it at the beginning
    const firstLi = document.createElement('li');
    firstLi.textContent = 'First Item';
    list.prepend(firstLi);

    // Add text directly after the list
    list.after("List finished.");
    ```

*   **DOM Events:** Responding to user interactions (clicks, key presses, mouse movements) or browser actions (page load, resize).
    *   **Event Listeners:** The preferred way to handle events.
        *   `element.addEventListener('eventName', callbackFunction, options)`: Attaches an event handler (`callbackFunction`) to an element for a specific event (`eventName`, e.g., 'click', 'mouseover', 'keydown').
        *   `element.removeEventListener('eventName', callbackFunction, options)`: Removes a previously attached listener. *Requires a reference to the exact same function*.
        *   `options`: Optional object, common property is `capture: true/false` (see Bubbling/Capturing). `once: true` makes the listener fire only once. `passive: true` can improve scrolling performance for touch/wheel events.
    *   **The `event` Object:** Passed automatically as an argument to the event handler callback. Contains information about the event (e.g., `event.target` - the element that triggered the event, `event.clientX/Y` - mouse coordinates, `event.key` - key pressed).
    *   **Common Event Types:** `click`, `dblclick`, `mousedown`, `mouseup`, `mouseover`, `mouseout`, `mousemove`, `keydown`, `keyup`, `keypress`, `focus`, `blur`, `change` (for form inputs), `input` (real-time input changes), `submit` (for forms), `load` (window/image loaded), `DOMContentLoaded` (HTML parsed, DOM ready), `scroll`, `resize`.
    *   **Event Bubbling and Capturing:** Phases of event propagation.
        *   **Capturing Phase:** Event travels down from the `window` to the target element. Listeners attached with `capture: true` fire during this phase.
        *   **Target Phase:** Event reaches the target element.
        *   **Bubbling Phase (Default):** Event travels back up from the target element to the `window`. Most event listeners fire during this phase (default `capture: false`).
    *   **Event Delegation:** Instead of adding listeners to many child elements, add a single listener to a common parent. Inside the handler, use `event.target` to identify which child element actually triggered the event. More efficient, especially for dynamically added elements.
    *   **Preventing Default Behavior:** `event.preventDefault()`: Stops the browser's default action for an event (e.g., preventing form submission, preventing link navigation).
    *   **Stopping Propagation:** `event.stopPropagation()`: Prevents the event from traveling further up (bubbling) or down (capturing) the DOM tree. Use sparingly.

    ```javascript
    const button = document.querySelector('#myButton');
    const container = document.querySelector('#container'); // Parent element

    function handleClick(event) {
      console.log('Button clicked!');
      console.log('Event target:', event.target); // The button itself
      console.log('Current target:', event.currentTarget); // The element the listener is attached to (button)
      // event.stopPropagation(); // Uncomment to stop propagation to container
    }

    button.addEventListener('click', handleClick);

    // Event Delegation Example
    container.addEventListener('click', function(event) {
      // Check if the clicked element (event.target) is a button inside the container
      if (event.target.tagName === 'BUTTON' && event.target.classList.contains('dynamic-button')) {
         console.log(`Delegated click on button: ${event.target.textContent}`);
      }
      console.log('Click detected on container (Bubbling)');
    });

    // Prevent form submission
    const form = document.querySelector('#myForm');
    form.addEventListener('submit', function(event) {
      event.preventDefault(); // Stop the default form submission
      console.log('Form submission prevented. Handle with JS.');
      // Process form data here using JavaScript
    });
    ```

### 11. Browser APIs (Web APIs)

Interfaces provided by the browser (beyond the core JS language and DOM) to interact with browser features and the operating system.

*   **`fetch` API:** Modern standard for making network requests (HTTP/S). Promise-based. Replaces the older `XMLHttpRequest`.
    *   Basic GET request: `fetch('/api/data')` returns a Promise resolving to a `Response` object.
    *   Processing the Response: Use methods like `response.json()`, `response.text()`, `response.blob()` which also return Promises.
    *   Configuring Requests: Pass a second argument (options object) to `fetch` for methods (`POST`, `PUT`, etc.), headers, body, etc.
    ```javascript
    // Simple GET request
    fetch('https://jsonplaceholder.typicode.com/todos/1') // Example public API
      .then(response => {
        if (!response.ok) { // Check for HTTP errors (4xx, 5xx)
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json(); // Parse response body as JSON (returns another promise)
      })
      .then(data => {
        console.log('Fetched data:', data);
      })
      .catch(error => {
        console.error('Fetch error:', error);
      });

    // POST request example
    async function postData(url = '', data = {}) {
        try {
            const response = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data) // Convert JS object to JSON string
            });
            if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
            return await response.json(); // Parse JSON response
        } catch (error) {
            console.error("Error posting data:", error);
            throw error; // Re-throw
        }
    }

    postData('https://jsonplaceholder.typicode.com/posts', { title: 'foo', body: 'bar', userId: 1 })
        .then(responseData => console.log('POST response:', responseData))
        .catch(err => console.log("POST failed"));
    ```
*   **Timers:** Execute code after a delay or at regular intervals.
    *   `setTimeout(callback, delayInMilliseconds, arg1, ...)`: Executes `callback` *once* after the specified `delay`. Returns a timer ID.
    *   `setInterval(callback, delayInMilliseconds, arg1, ...)`: Executes `callback` *repeatedly* every `delay` milliseconds. Returns a timer ID. Be cautious, can lead to performance issues if interval is too short or callback is slow.
    *   `clearTimeout(timerId)`: Cancels a `setTimeout`.
    *   `clearInterval(timerId)`: Cancels a `setInterval`.
    ```javascript
    const timeoutId = setTimeout(() => {
      console.log("This runs after 2 seconds.");
    }, 2000);

    // clearTimeout(timeoutId); // Uncomment to cancel it before it runs

    let intervalCount = 0;
    const intervalId = setInterval(() => {
      intervalCount++;
      console.log(`Interval ran ${intervalCount} times.`);
      if (intervalCount >= 5) {
        clearInterval(intervalId); // Stop the interval after 5 runs
        console.log("Interval stopped.");
      }
    }, 1000);
    ```
*   **Web Storage:** Storing key-value pairs locally in the user's browser. Data is specific to the *origin* (protocol, domain, port). Stored as strings.
    *   `localStorage`: Stores data with *no expiration date*. Persists even after the browser window is closed. Accessible from any window/tab from the same origin. Use for user settings, offline data (within limits ~5-10MB).
    *   `sessionStorage`: Stores data for *one session*. Data is cleared when the browser tab/window is closed. Accessible only within the same tab/window. Use for temporary session data.
    *   **API (same for both):**
        *   `setItem(key, value)`: Stores the item (value converted to string).
        *   `getItem(key)`: Retrieves the item (returns string or `null`).
        *   `removeItem(key)`: Removes the item.
        *   `clear()`: Removes all items for that origin.
        *   `key(index)`: Get the key at a specific index.
        *   `length`: Number of items stored.
    ```javascript
    // Using localStorage
    localStorage.setItem('username', 'Alice');
    localStorage.setItem('theme', 'dark');
    const storedUser = localStorage.getItem('username'); // "Alice"
    console.log(`Stored user: ${storedUser}`);

    // Store complex data (needs JSON stringify/parse)
    const settings = { notifications: true, level: 5 };
    localStorage.setItem('userSettings', JSON.stringify(settings));

    const retrievedSettings = JSON.parse(localStorage.getItem('userSettings'));
    console.log(retrievedSettings.notifications); // true

    // localStorage.removeItem('theme');
    // localStorage.clear(); // Clear all for this origin

    // sessionStorage works the same way:
    // sessionStorage.setItem('sessionId', 'xyz789');
    ```
*   **Geolocation API:** Get the user's geographical position (requires user permission). Asynchronous and Promise-based (or callback-based).
    ```javascript
    if ('geolocation' in navigator) {
      navigator.geolocation.getCurrentPosition(
        (position) => { // Success callback
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          console.log(`Location: Latitude ${lat}, Longitude ${lon}`);
          // Use the coordinates (e.g., show on a map)
        },
        (error) => { // Error callback
          console.error(`Geolocation error (${error.code}): ${error.message}`);
        },
        { // Options object (optional)
          enableHighAccuracy: true,
          timeout: 5000,
          maximumAge: 0
        }
      );
    } else {
      console.log('Geolocation is not supported by this browser.');
    }
    ```
*   **Canvas API (`<canvas>` element):** Low-level API for drawing graphics, animations, and image manipulation via JavaScript. Get the 2D rendering context (`getContext('2d')`) and use its methods (`fillRect`, `strokeRect`, `beginPath`, `moveTo`, `lineTo`, `arc`, `drawImage`, etc.).
*   **Web Workers:** Run JavaScript scripts in background threads, separate from the main UI thread. Prevents computationally intensive tasks from freezing the user interface. Communication between the main thread and workers happens via message passing (`postMessage` and `onmessage` event).
*   **(Others):** History API (manipulate browser history), Drag & Drop API, WebSockets (real-time bidirectional communication), IndexedDB (more complex client-side database), WebRTC (peer-to-peer communication), etc.

---

## IV. Modern JavaScript (ES6+ Features Deep Dive)

Many features introduced since ECMAScript 2015 (ES6) have significantly changed how JavaScript is written.

*   **`let` and `const` Revisited:**
    *   **Block Scope:** Confined to the nearest curly braces (`{}`) block (e.g., `if`, `for`, `while`, or just standalone blocks). Prevents accidental variable overwrites common with `var`.
    *   **Temporal Dead Zone (TDZ):** While hoisted (memory allocated), variables declared with `let` and `const` cannot be accessed before their declaration line in the code. Accessing them results in a `ReferenceError`.
*   **Arrow Functions Revisited:**
    *   **Syntax:** Concise (`param => expression`, `(p1, p2) => { statements }`).
    *   **Lexical `this`:** No `this` binding of their own; inherit `this` from the surrounding function or scope. Crucial for callbacks inside methods.
    *   **No `arguments` object:** Use rest parameters (`...args`) instead to capture all arguments.
    *   **Cannot be used as constructors:** Cannot be called with `new`.
    *   **No `prototype` property.**
*   **Template Literals (Backticks `` ` ``):**
    *   **String Interpolation:** Embed expressions directly within strings using `${expression}`.
    *   **Multiline Strings:** Create strings spanning multiple lines without needing `\n`.
    ```javascript
    const name = "World";
    const score = 95;
    const message = `Hello, ${name}!
Your score is ${score}.
Excellent!`;
    console.log(message);
    ```
*   **Destructuring Assignment:** Extract values from arrays or properties from objects into distinct variables.
    *   **Array Destructuring:**
        ```javascript
        const coordinates = [10, 20, 30];
        const [x, y, z] = coordinates; // x=10, y=20, z=30

        const [a, , c] = coordinates; // Skip element: a=10, c=30

        const [first, ...rest] = coordinates; // Rest syntax: first=10, rest=[20, 30]

        let val1 = 1, val2 = 2;
        [val1, val2] = [val2, val1]; // Easy swap: val1=2, val2=1
        ```
    *   **Object Destructuring:**
        ```javascript
        const user = { id: 101, username: 'jdoe', email: 'jdoe@example.com', profile: { theme: 'dark' } };

        // Basic
        const { username, email } = user; // username='jdoe', email='...'

        // Renaming variables
        const { id: userId, email: userEmail } = user; // userId=101, userEmail='...'

        // Default values
        const { role = 'guest', username: name } = user; // role='guest', name='jdoe'

        // Nested destructuring
        const { profile: { theme } } = user; // theme='dark'

        // Destructuring in function parameters
        function displayUser({ username, email }) {
          console.log(`User: ${username}, Email: ${email}`);
        }
        displayUser(user);
        ```
*   **Default Function Parameters:** Assign default values to parameters if no argument or `undefined` is passed.
    ```javascript
    function power(base, exponent = 2) { // exponent defaults to 2
      return Math.pow(base, exponent);
    }
    console.log(power(5));    // 25 (5^2)
    console.log(power(5, 3)); // 125 (5^3)
    ```
*   **Rest Parameter (`...`) vs. Spread Syntax (`...`):** Same syntax, different contexts.
    *   **Rest Parameter:** *Collects* multiple arguments into a single array in a function definition (must be the last parameter).
    *   **Spread Syntax:** *Expands* an iterable (like an array or string) or object properties into individual elements/properties. Used in function calls, array literals, or object literals.
    ```javascript
    // Rest Parameter (in function definition)
    function logArgs(...args) {
      console.log(args); // args is an array
    }
    logArgs(1, 'a', true); // [1, 'a', true]

    // Spread Syntax (in function call)
    const nums = [1, 2, 3];
    console.log(Math.max(...nums)); // Equivalent to Math.max(1, 2, 3) -> 3

    // Spread Syntax (in array literal)
    const arr1 = [1, 2];
    const arr2 = [3, 4];
    const combined = [...arr1, 0, ...arr2]; // [1, 2, 0, 3, 4]

    // Spread Syntax (in object literal - shallow copy/merge)
    const obj1 = { a: 1, b: 2 };
    const obj2 = { b: 3, c: 4 };
    const merged = { ...obj1, ...obj2, d: 5 }; // { a: 1, b: 3, c: 4, d: 5 } (later properties overwrite earlier ones)
    ```
*   **Enhanced Object Literals:** Syntactic sugar for defining objects.
    *   **Property Shorthand:** If key name matches variable name.
    *   **Method Definition Shorthand:** Omitting `function` keyword.
    *   **Computed Property Names:** Using `[]` to evaluate an expression as a property name.
    ```javascript
    const make = "Ford";
    const model = "Mustang";
    const propKey = "engineType";

    const car = {
      // Property shorthand
      make,
      model,
      // Method shorthand
      start() {
        console.log("Vroom!");
      },
      // Computed property name
      [propKey]: "V8",
      ['year' + 'Built']: 2023 // Computed property name
    };

    console.log(car.make); // Ford
    car.start(); // Vroom!
    console.log(car.engineType); // V8
    console.log(car.yearBuilt); // 2023
    ```
*   **Modules (`import`, `export`, `export default`):** Native JavaScript module system for organizing code into separate files. Each file is a module. Helps manage dependencies and namespaces.
    *   **`export`:** Makes variables, functions, or classes available to other modules. Can have multiple named exports.
    *   **`export default`:** Exports a single default value from a module. Only one default export per module.
    *   **`import`:** Brings exported functionality into another module.
    ```javascript
    // --- lib/math.js ---
    export const PI = 3.14159;

    export function add(a, b) {
      return a + b;
    }

    export function subtract(a, b) {
        return a - b;
    }

    // --- lib/utils.js ---
    export default function logMessage(msg) { // Default export
        console.log(`LOG: ${msg}`);
    }
    export const version = "1.0"; // Named export alongside default

    // --- main.js ---
    // Import named exports (need curly braces)
    import { PI, add as sum } from './lib/math.js'; // Can rename with 'as'
    // Import default export (can use any name) and named export
    import logger, { version as utilVersion } from './lib/utils.js';

    console.log(PI); // 3.14159
    console.log(sum(5, 3)); // 8
    logger(`App started. Util version: ${utilVersion}`); // LOG: App started. Util version: 1.0

    // Import everything as a namespace object
    import * as mathLib from './lib/math.js';
    console.log(mathLib.subtract(10, 4)); // 6
    ```
    *Note: In browsers, you typically need `<script type="module" src="main.js"></script>` to use ES Modules.*

*   **Iterators and Generators (`function*`, `yield`):**
    *   **Iterator Protocol:** Defines a standard way to produce a sequence of values (e.g., `for...of` loops). Requires an object to implement a `next()` method that returns `{ value: ..., done: boolean }`.
    *   **Iterable Protocol:** Requires an object to implement a `[Symbol.iterator]()` method that returns an iterator object. Arrays, Strings, Maps, Sets are built-in iterables.
    *   **Generators:** Special functions (`function*`) that can be paused and resumed using the `yield` keyword. They simplify the creation of iterators. When called, they return a generator object (which is an iterator).
    ```javascript
    // Generator function
    function* idGenerator() {
      let id = 1;
      while (true) {
        yield id++; // Pauses here, returns the value, resumes on next .next() call
      }
    }

    const gen = idGenerator(); // Get the generator object (iterator)

    console.log(gen.next()); // { value: 1, done: false }
    console.log(gen.next().value); // 2
    console.log(gen.next().value); // 3

    // Using generator with for...of
    function* range(start, end) {
        for (let i = start; i <= end; i++) {
            yield i;
        }
    }

    for (const num of range(1, 5)) {
        console.log(num); // 1, 2, 3, 4, 5
    }
    ```
*   **`Map` and `Set` Data Structures:**
    *   **`Set`:** Collection of *unique* values of any type. Order is based on insertion order. Useful for removing duplicates.
        *   Methods: `add(value)`, `has(value)`, `delete(value)`, `clear()`, `size` property. Iterates values directly.
        ```javascript
        const mySet = new Set();
        mySet.add(1);
        mySet.add(5);
        mySet.add(5); // Ignored, already exists
        mySet.add("text");
        console.log(mySet.has(1)); // true
        mySet.forEach(value => console.log(value)); // 1, 5, "text"
        const uniqueNums = [...new Set([1, 2, 2, 3, 4, 3])]; // [1, 2, 3, 4]
        ```
    *   **`Map`:** Collection of key-value pairs where *keys can be any type* (including objects, functions), unlike plain objects where keys are strings/Symbols. Remembers original insertion order of keys.
        *   Methods: `set(key, value)`, `get(key)`, `has(key)`, `delete(key)`, `clear()`, `size` property. Iterates `[key, value]` pairs.
        ```javascript
        const myMap = new Map();
        const keyObj = { id: 1 };
        const keyFunc = () => {};

        myMap.set('a string', 'value for string');
        myMap.set(keyObj, 'value for object');
        myMap.set(keyFunc, 'value for function');

        console.log(myMap.get(keyObj)); // value for object
        console.log(myMap.size); // 3
        myMap.forEach((value, key) => console.log(`${typeof key}: ${value}`));
        ```
*   **`WeakMap` and `WeakSet`:**
    *   Similar to `Map` and `Set`, but hold *weak references* to their keys (for `WeakMap`) or values (for `WeakSet`), specifically for objects.
    *   If an object used as a key/value is the *only* reference remaining, it can be garbage collected, and the corresponding entry in the WeakMap/WeakSet is automatically removed.
    *   Use cases: Caching, managing metadata associated with objects without preventing garbage collection.
    *   Cannot iterate over them, no `size` property. `WeakMap` keys *must* be objects. `WeakSet` values *must* be objects.
*   **`Symbol` Primitive Type Revisited:** Creates unique identifiers. Useful for:
    *   Unique object property keys to avoid name clashes (e.g., in libraries or when adding metadata).
    *   Implementing well-known Symbols like `Symbol.iterator` to customize object behavior.
    ```javascript
    const id1 = Symbol('desc');
    const id2 = Symbol('desc');
    console.log(id1 === id2); // false

    const myObj = {};
    myObj[id1] = 'Private data'; // Property key is a symbol
    console.log(Object.keys(myObj)); // [] (Symbol keys are not enumerated by default)
    console.log(Object.getOwnPropertySymbols(myObj)); // [ Symbol(desc) ]
    ```
*   **Optional Chaining (`?.`):** Safely access nested properties or call methods without explicitly checking if each intermediate property exists. If any part of the chain before `?.` is `null` or `undefined`, the expression short-circuits and returns `undefined` instead of throwing an error.
    ```javascript
    const user = {
      name: "Alice",
      address: {
        street: "123 Main St",
        // city: "Wonderland" // city is missing
      },
      getProfile() {
        return { bio: "Loves JS" };
      }
    };

    const city = user.address?.city; // undefined (no error)
    const zip = user.address?.zip?.code; // undefined
    const bio = user.getProfile?.().bio; // "Loves JS"
    const contact = user.getContact?.(); // undefined (method doesn't exist)

    console.log(city);
    ```
*   **Nullish Coalescing Operator (`??`):** Logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined` *only*. Otherwise, it returns the left-hand side operand. Useful for providing default values when `0` or `""` (empty string) are valid inputs (unlike `||` which treats them as falsy).
    ```javascript
    let volume = 0;
    let defaultVolume = 50;

    const setting1 = volume || defaultVolume; // 50 (because 0 is falsy)
    const setting2 = volume ?? defaultVolume; // 0 (because 0 is not null/undefined)

    let userText = "";
    const displayText1 = userText || "Default Text"; // "Default Text"
    const displayText2 = userText ?? "Default Text"; // "" (empty string is valid)

    let config = null;
    const finalConfig = config ?? { default: true }; // { default: true }

    console.log(setting1, setting2);
    console.log(displayText1, displayText2);
    console.log(finalConfig);
    ```
*   **`Promise` improvements:** See Promises section above for `Promise.allSettled`, `Promise.any`, `Promise.finally`.
*   **`BigInt`:** See Data Types section above. For arbitrary-precision integers.
*   **Dynamic `import()`:** Allows loading ES modules asynchronously on demand. Returns a Promise that resolves to the module namespace object. Useful for code splitting (loading code only when needed).
    ```javascript
    // Assuming button with id="loadModuleBtn" exists
    const loadButton = document.querySelector('#loadModuleBtn');

    loadButton.addEventListener('click', async () => {
      try {
        // Dynamically import the module when the button is clicked
        const module = await import('./lib/heavy-module.js');
        module.doSomething(); // Call function from the loaded module
        // Or use default export: const defaultExport = module.default;
      } catch (error) {
        console.error("Failed to load module:", error);
      }
    });
    ```
*   **Private Class Fields (`#`) (ES2022):** Native way to declare private instance fields and methods within classes. Truly private, cannot be accessed from outside the class.
    ```javascript
    class Counter {
      #count = 0; // Private instance field

      #increment() { // Private instance method
        this.#count++;
      }

      // Public method that uses private members
      click() {
        this.#increment();
        console.log(`Current count: ${this.#count}`);
      }

      getCount() { // Public getter for the private field (controlled access)
          return this.#count;
      }
    }

    const c = new Counter();
    c.click(); // Current count: 1
    c.click(); // Current count: 2
    // console.log(c.#count); // SyntaxError: Private field '#count' must be declared in an enclosing class
    // c.#increment(); // SyntaxError
    console.log(c.getCount()); // 2 (Accessed via public method)
    ```

---

## V. Advanced Topics & Ecosystem

Beyond the core language features, understanding the surrounding tools and advanced concepts is crucial.

### 12. Code Quality & Organization

*   **Modules Revisited:**
    *   **ES Modules (ESM):** The standard (`import`/`export`). Used natively in modern browsers (`<script type="module">`) and Node.js (using `.mjs` extension or `"type": "module"` in `package.json`). Preferred for modern development.
    *   **CommonJS (CJS):** The traditional module system used in Node.js (`require()`/`module.exports`). Still widely used in the Node ecosystem, but ESM is the future standard.
*   **Module Bundlers (Webpack, Parcel, Rollup):**
    *   **Why?** Browsers historically didn't support modules well, and loading many small files is inefficient. Bundlers solve this.
    *   **What they do:** Take your source code (including modules, CSS, images, etc.), process it (transpiling, minifying), resolve dependencies, and output optimized static assets (often a single JS file or fewer files) suitable for browsers.
    *   **Webpack:** Highly configurable, powerful, large ecosystem. Steeper learning curve.
    *   **Parcel:** Zero-configuration (mostly), easier to start with, fast.
    *   **Rollup:** Often preferred for bundling libraries (good at code splitting and tree-shaking).
*   **Linters & Formatters:** Tools to improve code quality and consistency.
    *   **Linters (ESLint):** Analyze code for potential errors, bugs, stylistic issues, and anti-patterns based on configurable rules. Helps catch errors early and maintain standards.
    *   **Formatters (Prettier):** Automatically format code according to a predefined style (indentation, spacing, quotes, etc.). Enforces a consistent look and feel, reducing arguments about style. Often used together with ESLint.
*   **Transpilers (Babel):**
    *   **Why?** To use the latest JavaScript features (ES6+) in environments (like older browsers) that don't support them natively.
    *   **What they do:** Convert modern JavaScript code into an older, more compatible version (usually ES5). Babel uses plugins for specific syntax transformations and presets (collections of plugins). Often integrated into the build process (Webpack, Parcel).
*   **Package Managers (npm, yarn):** Tools for managing project dependencies (external libraries and tools).
    *   **`npm` (Node Package Manager):** Bundled with Node.js. Manages packages listed in `package.json`, installs them into `node_modules`. Commands: `npm install <pkg>`, `npm run <script>`, `npm init`.
    *   **`yarn`:** Alternative package manager, often praised for speed and reliability features (though npm has caught up significantly). Uses `package.json` too. Commands: `yarn add <pkg>`, `yarn <script>`, `yarn init`.
    *   **`package.json`:** File describing the project, its dependencies (`dependencies`, `devDependencies`), scripts (`scripts`), etc.
    *   **`package-lock.json` / `yarn.lock`:** Lock files that record the exact versions of dependencies installed, ensuring consistent builds across different machines/environments.

### 13. Performance Optimization

Writing efficient JavaScript code, especially for client-side applications.

*   **Minimizing DOM Manipulation:** Accessing and modifying the DOM is relatively slow. Batch updates, use document fragments for multiple changes, avoid unnecessary DOM reads/writes within loops.
*   **Efficient Event Handling:**
    *   **Event Delegation:** Use fewer listeners (see DOM Events section).
    *   **Debouncing:** Group multiple sequential calls to a function (e.g., on window resize or search input) into a single call after a period of inactivity. Prevents excessive function executions.
    *   **Throttling:** Ensure a function is called at most once within a specified time interval (e.g., for scroll event handlers). Prevents the handler from firing too rapidly.
*   **Code Splitting / Lazy Loading:** Break down large JavaScript bundles into smaller chunks using bundlers and dynamic `import()`. Load chunks only when they are actually needed (e.g., for specific routes or features), improving initial page load time.
*   **Memory Management & Garbage Collection (GC):**
    *   **Concept:** JavaScript engines automatically manage memory allocation and deallocation. When objects are no longer reachable (no references point to them), the Garbage Collector reclaims that memory.
    *   **Avoiding Leaks:** Be mindful of closures holding unnecessary references, detached DOM elements with listeners still attached, uncleared timers/intervals, large global variables. Chrome DevTools Memory tab helps identify leaks.
*   **Web Workers for Heavy Tasks:** Offload CPU-intensive computations (complex calculations, data processing) to background threads using Web Workers to keep the main UI thread responsive.
*   **Performance Profiling (Browser DevTools):** Use the Performance tab in browser DevTools to record and analyze runtime performance, identify bottlenecks (slow functions, layout thrashing, paint issues), and measure memory usage.

### 14. Design Patterns in JavaScript

Reusable solutions to common software design problems within the context of JavaScript. Understanding patterns improves code organization, readability, maintainability, and communication among developers.

*   **Creational Patterns:** Deal with object creation mechanisms.
    *   **Constructor:** Using constructor functions or classes with `new` (covered earlier).
    *   **Factory:** A function or method that creates and returns objects, often hiding the specific constructor logic. Useful for creating different types of objects based on input.
    *   **Singleton:** Ensures a class has only one instance and provides a global point of access to it (e.g., configuration manager, logger). Use with caution, can introduce global state.
    *   **Builder:** Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
*   **Structural Patterns:** Deal with object composition and relationships.
    *   **Adapter:** Allows objects with incompatible interfaces to collaborate. Wraps an existing class with a new interface.
    *   **Decorator:** Attaches additional responsibilities or behaviors to an object dynamically without altering its code. Wraps the original object.
    *   **Facade:** Provides a simplified, unified interface to a complex subsystem (e.g., a library with many parts). Hides complexity.
    *   **Proxy:** Provides a surrogate or placeholder for another object to control access to it (e.g., for lazy loading, access control, logging). ES6 has a native `Proxy` object.
    *   **Module:** Encapsulating a piece of code into a reusable unit, controlling visibility (public/private members). Achieved via IIFEs (older way) or native ES Modules (modern way).
*   **Behavioral Patterns:** Deal with communication between objects and assignment of responsibilities.
    *   **Observer:** Defines a one-to-many dependency between objects. When one object (subject) changes state, all its dependents (observers) are notified automatically (e.g., event listeners, reactive programming).
    *   **Command:** Encapsulates a request as an object, allowing parameterization of clients with different requests, queuing or logging requests, and supporting undoable operations.
    *   **Iterator:** Provides a way to access the elements of an aggregate object (collection) sequentially without exposing its underlying representation (covered with Iterators/Generators).
    *   **Mediator:** Defines an object that encapsulates how a set of objects interact. Promotes loose coupling by keeping objects from referring to each other explicitly.
    *   **State:** Allows an object to alter its behavior when its internal state changes. The object appears to change its class.
    *   **Strategy:** Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Lets the algorithm vary independently from clients that use it.

### 15. Testing

Verifying that your code works as expected and continues to work as it evolves.

*   **Why Test?** Catch bugs early, prevent regressions (breaking existing functionality), provide documentation, facilitate refactoring, improve code design.
*   **Types of Tests:**
    *   **Unit Tests:** Test individual functions or components (units) in isolation. Fast and numerous. Focus on verifying logic within the unit.
    *   **Integration Tests:** Test the interaction *between* multiple units or components (e.g., function A calling function B, component interacting with a service). Slower than unit tests.
    *   **End-to-End (E2E) Tests:** Test the entire application flow from the user's perspective, typically by simulating user interactions in a browser. Slowest but provide highest confidence in the overall system.
*   **Testing Frameworks & Libraries:**
    *   **Test Runners/Frameworks:** Provide structure for writing and running tests (e.g., `describe`, `it`, assertions). (Jest, Mocha, Jasmine, Vitest).
    *   **Assertion Libraries:** Provide functions to make claims about your code's behavior (`expect(value).toBe(...)`). (Chai, Jest's built-in `expect`).
    *   **Mocking/Spying Libraries:** Create test doubles (mocks, stubs, spies) to isolate units being tested from their dependencies. (Sinon.js, Jest's built-in mocking).
    *   **E2E Testing Tools:** Automate browser interactions. (Cypress, Playwright, Selenium).
    *   **Popular Choices:**
        *   **Jest:** All-in-one framework (runner, assertions, mocking), popular for React/Node.js. Zero-config focus.
        *   **Mocha + Chai + Sinon:** Flexible combination, choose your own assertion/mocking libraries.
        *   **Cypress/Playwright:** Leading E2E testing tools.
*   **Writing Testable Code:** Design code with testing in mind. Use pure functions, dependency injection, clear interfaces, and avoid tight coupling and side effects where possible.

### 16. Security Considerations

Writing secure JavaScript, especially for client-side code interacting with user input and external data.

*   **Cross-Site Scripting (XSS):** Attacker injects malicious scripts into a website, which then execute in the victim's browser.
    *   **Prevention:** *Never* trust user input. Sanitize input before rendering it (convert `<`, `>`, `&` etc. to HTML entities). Use `textContent` instead of `innerHTML` when inserting text. Use frameworks with built-in XSS protection (React, Vue, Angular often handle this). Implement Content Security Policy (CSP) HTTP headers to restrict where scripts can be loaded/executed from.
*   **Cross-Site Request Forgery (CSRF):** Attacker tricks a logged-in user into submitting a malicious request to a website they are authenticated with, without their knowledge.
    *   **Prevention (Mostly server-side):** Use anti-CSRF tokens (unique, unpredictable tokens included in forms/requests that the server validates). Check the `Origin` or `Referer` header (less reliable). Use SameSite cookies (`Strict` or `Lax`).
*   **Data Exposure:** Avoid storing sensitive information (API keys, passwords, private data) directly in client-side JavaScript code, as it's visible to anyone inspecting the source. Fetch sensitive data from secure backend endpoints when needed. Use environment variables for configuration.
*   **Dependency Security:** Third-party packages (from npm/yarn) can contain vulnerabilities. Regularly audit dependencies (`npm audit`, `yarn audit`) and update them promptly. Use tools like Snyk or Dependabot.

### 17. Beyond the Browser: Node.js & Frameworks

JavaScript's reach extends far beyond the browser.

*   **Node.js Basics:** A JavaScript runtime built on Chrome's V8 engine. Allows running JS on the server or for command-line tools.
    *   **Event-driven, Non-blocking I/O:** Efficiently handles many concurrent connections using the event loop and asynchronous operations (especially for I/O like network requests, database access, file system).
    *   **`require`/`module.exports`:** The CommonJS module system (though ES Modules are also supported).
    *   **`npm`:** Integrated package manager, vast ecosystem of libraries.
    *   **Use Cases:** Building web servers/APIs (with frameworks like Express, Koa, Fastify), command-line tools, build tools, real-time applications (WebSockets), microservices.
*   **JavaScript Frameworks/Libraries (Frontend):** Provide structure, abstractions, and tools to build complex user interfaces more efficiently.
    *   **React (Library):** Component-based UI library developed by Facebook. Uses a virtual DOM for efficient updates. Large ecosystem, focuses on the view layer. Requires other libraries for routing, state management (e.g., Redux, Zustand). Uses JSX (XML-like syntax extension).
    *   **Angular (Framework):** Comprehensive framework developed by Google. Uses TypeScript. Provides solutions for components, routing, state management, HTTP requests, etc., out-of-the-box. More opinionated structure.
    *   **Vue.js (Framework):** Progressive framework known for its approachability and flexibility. Can be adopted incrementally. Offers core library for the view layer plus official companion libraries for routing/state management. Uses template syntax similar to HTML.
    *   **Svelte (Compiler/Framework):** Shifts work from the browser (runtime) to the build step (compile time). Compiles components into highly optimized imperative JavaScript. Results in smaller bundles and potentially faster performance. Reactive by default.
*   **TypeScript:** A typed superset of JavaScript developed by Microsoft that compiles to plain JavaScript.
    *   **Static Typing:** Add type annotations (`let name: string; function add(a: number, b: number): number;`) to catch type-related errors during development (compile time) rather than at runtime.
    *   **Benefits:** Improved code quality and maintainability, better tooling (autocompletion, refactoring), enhanced developer experience, especially for large codebases and teams.
    *   Integrates well with existing JavaScript code and popular frameworks.

---

## Conclusion

*   **Recap of Key Concepts:** You've journeyed through JavaScript's core syntax, data types, control flow, functions, object-oriented principles (prototypes, classes), asynchronous handling (callbacks, Promises, async/await), DOM manipulation, browser APIs, modern ES6+ features, and essential ecosystem topics like modules, tooling, testing, performance, and security.
*   **The Importance of Continuous Learning:** The JavaScript landscape evolves rapidly. New features are added to the language, tools improve, and frameworks come and go. Stay curious, follow reputable sources (MDN, JS blogs, conference talks), and keep learning.
*   **Practice, Practice, Practice!:** Reading is not enough. Build projects! Start small (interactive components, simple apps) and gradually increase complexity. Contribute to open source. Solve coding challenges. Practical application solidifies understanding.
*   **Community Resources:**
    *   **MDN Web Docs:** The ultimate reference for JavaScript and Web APIs.
    *   **Stack Overflow:** Ask and answer questions.
    *   **JavaScript Info (javascript.info):** Excellent tutorial website.
    *   **FreeCodeCamp, Codecademy, etc.:** Interactive learning platforms.
    *   **Blogs, Twitter, Dev.to:** Follow influential developers and communities.

Mastering JavaScript is a marathon, not a sprint. Enjoy the process, embrace the challenges, and build amazing things! Good luck!
