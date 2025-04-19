Okay, let's power up this JavaScript review guide with better structure, visual cues, and clearer explanations to make it an effective study companion!

---

## 🚀 Master JavaScript: Your Ultimate Prep Exam Guide! 🚀

Welcome to your enhanced review for the JavaScript portion of the Certified Full Stack Developer Curriculum. Get ready to dive into the language that brings websites to life!

**How to Use This Guide:**

1.  🧠 **Think Actively:** Don't just read definitions. Ask "How does this apply?" or "What's the difference between X and Y?".
2.  🗣️ **Explain & Recall:** Cover sections and try explaining the concepts in your own words.
3.  💻 **Code It Out:** Type out the examples, experiment with them in your browser's console or a code editor. Break things, fix things!
4.  🔗 **Connect the Dots:** See how concepts like scope, closures, asynchronous operations, and the DOM all work together.

Let's get started!

---

### Section 1: 📜 JavaScript Fundamentals - The Core

The absolute basics: what JS is, its role, and foundational concepts.

*   **✨ Role of JavaScript:** While HTML structures content and CSS styles it, JavaScript adds **interactivity and dynamic behavior**. It handles user input, animations, data fetching, complex logic, and makes web applications possible.
*   **💬 Logging (`console.log()`):** Your essential debugging tool! Prints messages or variable values to the browser's developer console (usually opened with F12).
    ```javascript
    console.log("Hello from JavaScript!");
    let user = "Alex";
    console.log(user); // Output: Alex
    ```
*   **✍️ Semicolons (;):** Mark the **end of a statement**. While JavaScript has Automatic Semicolon Insertion (ASI), relying on it can lead to subtle bugs. **Best practice: Always use semicolons.**
    ```javascript
    let message = 'Statement 1'; // Semicolon ends the statement
    let count = 10; // Semicolon ends the statement
    ```
*   **📝 Comments:** Ignored by the engine, used to explain code or temporarily disable it.
    ```javascript
    // This is a single-line comment.

    /*
       This is a
       multi-line comment.
    */
    ```
*   **⚡ Dynamically Typed Language:** You **don't** declare a variable's type explicitly. JavaScript figures it out at runtime based on the assigned value. A variable can hold different types over time (though this can sometimes be confusing!).
    ```javascript
    let value = 42;      // value is a Number
    value = "Hello";   // value is now a String
    value = true;      // value is now a Boolean
    ```
*   **🔍 `typeof` Operator:** Returns a string indicating the data type of a value. Useful for checking types.
    ```javascript
    console.log(typeof 42);         // "number"
    console.log(typeof "hello");    // "string"
    console.log(typeof true);       // "boolean"
    console.log(typeof undefined);  // "undefined"
    console.log(typeof { a: 1 });   // "object"
    console.log(typeof [1, 2]);     // "object" (Arrays are objects)
    console.log(typeof function(){});// "function" (Functions are objects)
    console.log(typeof null);       // "object" (⚠️ Historical quirk!)
    ```

---

### Section 2: 🏷️ Data Types - The Building Blocks of Information

The different kinds of values JavaScript can work with.

*   **Primitive Types (Immutable):** Represent single, simple values.
    *   **🔢 `Number`:** Represents both integers (e.g., `10`, `-5`) and floating-point numbers (e.g., `3.14`, `-0.5`). Includes special values `Infinity`, `-Infinity`, and `NaN` (Not a Number).
    *   **📜 `String`:** A sequence of characters (text) enclosed in single (`' '`), double (`" "`), or backticks (`` ` ``). **Strings are immutable** – you can't change individual characters within an existing string; you create new strings instead.
    *   **✅ `Boolean`:** Represents logical values: `true` or `false`. Used for conditions.
    *   **🤷 `undefined`:** Represents a variable that has been declared but **not yet assigned a value**. It's the default value of uninitialized variables.
    *   **⚫ `null`:** Represents the **intentional absence of any object value**. It's an assigned value, meaning "no value". Often used to explicitly clear a variable.
    *   **<0xF0><0x9F><0x94><0x91> `Symbol`:** Unique and immutable primitive value, often used as identifiers for object properties to avoid naming collisions. `Symbol('id') !== Symbol('id')`.
    *   **🐘 `BigInt`:** Represents integers of **arbitrary length**, larger than the standard `Number` type can safely handle. Created by appending `n` to an integer literal (e.g., `12345678901234567890n`).
*   **Non-Primitive Type (Mutable):**
    *   **📦 `Object`:** A collection of key-value pairs (properties). Keys are usually strings (or Symbols), values can be any data type (including other objects, arrays, functions). Objects are mutable – their properties can be changed.
        ```javascript
        let car = {
          make: "Toyota", // key: "make", value: "Toyota"
          model: "Camry", // key: "model", value: "Camry"
          year: 2022,
          start: function() { console.log("Engine started!"); } // Method
        };
        console.log(car.make); // Access using dot notation: "Toyota"
        console.log(car["model"]); // Access using bracket notation: "Camry"
        car.year = 2023; // Modify property
        ```
        *(Arrays and Functions are technically special types of objects)*

---

### Section 3: 📦 Variables - Storing Data

Containers for holding data values.

*   **Declaration (`let`, `const`):**
    *   **`let`:** Declares a **block-scoped** variable that **can be reassigned**.
        ```javascript
        let score = 100;
        score = 150; // Allowed
        console.log(score); // 150
        ```
    *   **`const`:** Declares a **block-scoped** variable that **cannot be reassigned** after initialization. Must be initialized when declared. Use for values that shouldn't change (constants, references to objects/arrays you don't want to reassign).
        ```javascript
        const PI = 3.14159;
        // PI = 3.14; // TypeError: Assignment to constant variable.

        const user = { name: "Alice" };
        user.name = "Bob"; // Allowed! Modifying the *object's property* is okay.
        // user = { name: "Charlie" }; // TypeError: Cannot reassign const variable.
        ```
    *   **`var` (Legacy):** The *old* way. **Avoid using `var`** in modern JavaScript due to its quirky function-scoping (not block-scoping) and hoisting behavior (covered later). Use `let` and `const` instead.
*   **Assignment (`=`):** The assignment operator assigns a value to a variable.
    ```javascript
    let city;         // Declaration
    city = "London"; // Assignment
    ```
*   **🏷️ Naming Conventions:**
    *   Use descriptive names (`userAge`, `calculateTotal`).
    *   Use **camelCase** (e.g., `firstName`, `itemsInCart`).
    *   Start with a letter, underscore (`_`), or dollar sign (`$`). Cannot start with a number.
    *   Only contain letters, numbers, `_`, `$`. No spaces or other special characters.
    *   Case-sensitive (`age` is different from `Age`).
    *   Don't use reserved keywords (`let`, `const`, `if`, `function`, etc.).

---

### Section 4: 📜 String Manipulation - Working with Text

Handling sequences of characters.

*   **Immutable Nature:** Remember, strings can't be changed in place. Methods that seem to modify strings actually return *new* strings.
*   **🔗 Concatenation (Joining Strings):**
    *   **`+` Operator:** Joins strings together.
        ```javascript
        let greeting = "Hello";
        let name = "World";
        let message = greeting + ", " + name + "!"; // "Hello, World!"
        ```
    *   **`+=` Operator:** Appends to an existing string.
        ```javascript
        let sentence = "Learning JavaScript";
        sentence += " is fun."; // "Learning JavaScript is fun."
        ```
    *   **`concat()` Method:** Another way to join strings.
        ```javascript
        let str1 = "Web";
        let str2 = "Development";
        let combined = str1.concat(" ", str2); // "Web Development"
        ```
    *   **`` ` `` Template Literals (🏆 Modern & Preferred!):** Use backticks. Allows:
        *   **String Interpolation:** Easily embed variables/expressions using `${...}`.
        *   **Multiline Strings:** Create strings spanning multiple lines without `\n`.
        ```javascript
        let item = "Coffee";
        let price = 3.50;
        let receipt = `Item: ${item}
        Price: $${price.toFixed(2)}
        Total: $${(price * 1.08).toFixed(2)} (incl. tax)`;
        console.log(receipt);
        ```
*   **Accessing Characters:** Use zero-based index with bracket notation `[]`.
    ```javascript
    let language = "JavaScript";
    console.log(language[0]); // "J"
    console.log(language[4]); // "S"
    ```
*   **Escaping Characters (`\`):** Use backslash to include special characters like quotes within a string defined with the same quotes, or characters like `\n` (newline).
    ```javascript
    let quote = 'He said, \'Hi there!\''; // Use \' inside single quotes
    let path = "C:\\Users\\Docs";       // Use \\ for a literal backslash
    ```
*   **ASCII & Character Codes:**
    *   `charCodeAt(index)`: Returns the numeric ASCII/Unicode value of the character at `index`.
    *   `String.fromCharCode(code)`: Returns the character corresponding to the numeric code.
    ```javascript
    console.log("B".charCodeAt(0)); // 66
    console.log(String.fromCharCode(67)); // "C"
    ```
*   **✂️ Common String Methods (Return *New* Strings):**
    *   `length`: (Property, not method) Returns the number of characters.
    *   `indexOf(substring)`: Returns index of the *first* occurrence (-1 if not found).
    *   `includes(substring)`: Returns `true` if the string contains the substring, `false` otherwise.
    *   `slice(startIndex, endIndex)`: Extracts a portion (end index is non-inclusive).
    *   `toUpperCase()` / `toLowerCase()`: Convert case.
    *   `replace(searchValue, newValue)`: Replaces the *first* occurrence of `searchValue` (can be string or regex).
    *   `replaceAll(searchValue, newValue)`: Replaces *all* occurrences (requires global regex flag `/g` if using regex).
    *   `trim()`: Removes whitespace from *both* ends.
    *   `trimStart()` / `trimEnd()`: Remove whitespace from beginning/end only.
    *   `split(separator)`: Splits the string into an array of substrings based on the `separator`. `"".split("")` splits into individual characters.
    *   `repeat(count)`: Repeats the string `count` times.

---

### Section 5: 🔢 Numbers & Math - Calculations

Working with numeric values and operations.

*   **Types:** Includes integers, decimals, `Infinity`, `-Infinity`, `NaN`.
*   **➕ Arithmetic Operators:** `+` (addition), `-` (subtraction), `*` (multiplication), `/` (division), `%` (remainder/modulo), `**` (exponentiation).
*   **⚠️ Division by Zero:** Results in `Infinity` (or `-Infinity`).
*   **🔄 Type Coercion with Operators:**
    *   `+` with a String: Converts number to string and concatenates (`5 + '10'` -> `"510"`).
    *   `-`, `*`, `/` with a String: Tries to convert string to number (`'10' - 5` -> `5`, `'hello' * 2` -> `NaN`).
    *   `null` treated as `0`.
    *   `undefined` treated as `NaN`.
*   **🥇 Operator Precedence:** Order of operations (Parentheses `()` first, then `**`, then `* / %`, then `+ -`). Use parentheses `()` for clarity and control.
*   **↔️ Associativity:** Determines order for operators of same precedence (most are left-to-right, `**` is right-to-left).
*   **📈 Increment (`++`) / Decrement (`--`):**
    *   **Prefix (`++x`):** Increments/decrements *before* returning the value.
    *   **Postfix (`x++`):** Increments/decrements *after* returning the original value.
*   **+= Compound Assignment Operators:** Shorthand (e.g., `x += 5` is `x = x + 5`). Others: `-=`, `*=`, `/=`, `%=`, `**=`.
*   **🧮 The `Math` Object:** Provides properties and methods for mathematical constants and functions.
    *   `Math.random()`: Random float between 0 (inclusive) and 1 (exclusive).
    *   `Math.floor(x)`: Rounds *down* to nearest integer.
    *   `Math.ceil(x)`: Rounds *up* to nearest integer.
    *   `Math.round(x)`: Rounds to nearest integer (.5 rounds up).
    *   `Math.trunc(x)`: Removes decimal part (no rounding).
    *   `Math.max(a, b, ...)` / `Math.min(a, b, ...)`: Returns largest/smallest value.
    *   `Math.pow(base, exponent)`: `base` to the power of `exponent`.
    *   `Math.sqrt(x)` / `Math.cbrt(x)`: Square/cube root.
    *   `Math.abs(x)`: Absolute value.
    *   `Math.PI`: Constant for Pi.
*   **🔢 Common Number Methods/Functions:**
    *   `Number.isNaN(value)`: **Reliable** way to check if a value is *specifically* `NaN`. Better than global `isNaN()`.
    *   `isNaN(value)` (Global): Tries to convert value to number first, then checks if it's `NaN`. Can give surprising results (`isNaN("hello")` is `true`). Use `Number.isNaN()` preferably.
    *   `parseInt(string, radix)`: Parses a string and returns an integer. Stops at first non-digit. `radix` (base, usually 10) is important!
    *   `parseFloat(string)`: Parses a string and returns a floating-point number.
    *   `num.toFixed(digits)`: Formats a number using fixed-point notation (returns a string) with a specified number of decimal places.

---

### Section 6: ✅ Booleans & Comparisons - True or False

Working with logical values and comparing data.

*   **Values:** `true` and `false`.
*   **⚖️ Equality Operators:**
    *   **Strict Equality (`===`):** Checks if values are equal **WITHOUT** type coercion. **🏆 Always prefer strict equality!**
        ```javascript
        console.log(5 === 5);   // true
        console.log(5 === '5'); // false (different types)
        ```
    *   **Loose Equality (`==`):** Checks if values are equal **AFTER** performing type coercion. Can lead to unexpected results. **Avoid if possible.**
        ```javascript
        console.log(5 == 5);   // true
        console.log(5 == '5'); // true (string '5' coerced to number 5)
        console.log(0 == false); // true (false coerced to 0)
        console.log(null == undefined); // true (special case)
        ```
*   **≠ Inequality Operators:**
    *   **Strict Inequality (`!==`):** Checks if values are *not* equal **WITHOUT** type coercion. **🏆 Preferred!**
    *   **Loose Inequality (`!=`):** Checks if values are *not* equal **AFTER** type coercion. **Avoid.**
*   **< > Comparison Operators:** `>`, `>=`, `<`, `<=`. Compare values (numerically or lexicographically for strings).
*   **🔄 Unary Operators:**
    *   **Unary Plus (`+`):** Tries to convert operand to a number (`+'42'` -> `42`).
    *   **Unary Negation (`-`):** Tries to convert operand to number and negates it (`-'42'` -> `-42`).
    *   **Logical NOT (`!`):** Flips the boolean value (`!true` -> `false`, `!0` -> `true`).
*   **🔗 Binary Logical Operators:**
    *   **Logical AND (`&&`):** Returns the *first falsy* value, or the *last truthy* value if all are truthy. Used for checking multiple conditions (`if (isLoggedIn && isAdmin)`).
    *   **Logical OR (`||`):** Returns the *first truthy* value, or the *last falsy* value if all are falsy. Used for providing defaults (`let name = receivedName || "Guest"`).
    *   **Nullish Coalescing (`??`):** Returns the right-hand operand **only if** the left-hand operand is `null` or `undefined`. Otherwise, returns the left-hand operand. Safer for defaults when `0` or `false` are valid intended values.
        ```javascript
        let volume = 0;
        let setting = volume ?? 50; // setting is 0 (because 0 is not null/undefined)
        let oldSetting = volume || 50; // oldSetting is 50 (because 0 is falsy)
        ```
*   **👍 Truthy & Falsy Values:** In boolean contexts (like `if` statements), values are coerced to `true` or `false`.
    *   **Falsy Values:** `false`, `0`, `-0`, `""` (empty string), `null`, `undefined`, `NaN`, `0n` (BigInt zero).
    *   **Truthy Values:** Everything else (including non-empty strings `"hello"`, numbers like `42`, objects `{}`, arrays `[]`).

---

### Section 7: 🚦 Control Flow - Making Decisions & Repeating Actions

Directing the execution path of your code.

*   **`if / else if / else` Statements:** Execute code blocks conditionally.
    ```javascript
    let hour = 14;
    if (hour < 12) {
      console.log("Good morning!");
    } else if (hour < 18) {
      console.log("Good afternoon!"); // This runs
    } else {
      console.log("Good evening!");
    }
    ```
*   **❓ Ternary Operator (`condition ? valueIfTrue : valueIfFalse`):** A concise shorthand for simple `if/else` assignments.
    ```javascript
    let age = 20;
    let status = (age >= 18) ? "Adult" : "Minor";
    console.log(status); // "Adult"
    ```
*   **`switch` Statement:** Evaluates an expression and matches its value against `case` clauses. Often cleaner than multiple `else if` for specific value checks. Remember `break`!
    ```javascript
    let day = "Monday";
    switch (day) {
      case "Monday":
        console.log("Start of the week.");
        break; // Exit the switch
      case "Friday":
        console.log("Almost weekend!");
        break;
      default: // Optional: if no case matches
        console.log("It's some other day.");
    }
    ```
*   **🔄 Loops (Repeating Code):**
    *   **`for` Loop:** Repeats a block a specific number of times. Good when you know the count. (Initialization; Condition; Final-expression)
        ```javascript
        for (let i = 0; i < 3; i++) { // i=0, i=1, i=2
          console.log(`Iteration ${i}`);
        }
        ```
    *   **`for...of` Loop:** Iterates over the **values** of an *iterable* object (Arrays, Strings, Maps, Sets). **🏆 Preferred for iterating over array values.**
        ```javascript
        const colors = ["red", "green", "blue"];
        for (const color of colors) {
          console.log(color); // red, then green, then blue
        }
        ```
    *   **`for...in` Loop:** Iterates over the **keys (property names)** of an object. Order not guaranteed. Use with caution on arrays (iterates indices and potentially other properties).
        ```javascript
        const user = { name: "Alice", city: "London" };
        for (const key in user) {
          console.log(`${key}: ${user[key]}`); // name: Alice, then city: London
        }
        ```
    *   **`while` Loop:** Repeats a block as long as a condition is `true`. Condition checked *before* each iteration.
        ```javascript
        let count = 3;
        while (count > 0) {
          console.log(count); // 3, then 2, then 1
          count--;
        }
        ```
    *   **`do...while` Loop:** Like `while`, but the condition is checked *after* the block executes. Guarantees the block runs **at least once**.
        ```javascript
        let input;
        do {
          input = prompt("Enter 'quit' to exit:");
        } while (input !== "quit");
        ```
*   **🛑 `break` Statement:** Exits the innermost loop (`for`, `while`, `do...while`, `switch`) immediately.
*   **⏭️ `continue` Statement:** Skips the rest of the current loop iteration and proceeds to the next one.

---

### Section 8: ⚙️ Functions - Reusable Code Blocks

Defining blocks of code that perform tasks and can be called multiple times.

*   **Declaration:** Using the `function` keyword. Function declarations are *hoisted*.
    ```javascript
    function greet(name) { // 'name' is a parameter
      console.log(`Hello, ${name}!`);
    }
    greet("Bob"); // "Bob" is an argument
    ```
*   **Expression:** Assigning an anonymous or named function to a variable. Not fully hoisted (variable declaration is, assignment isn't).
    ```javascript
    const add = function(a, b) {
      return a + b;
    };
    let sum = add(5, 3); // 8
    ```
*   **Arrow Functions (`=>`) (Modern & Concise):** Shorter syntax.
    *   Implicit return for single expressions (no `{}` or `return`).
    *   Parentheses `()` optional for single parameter.
    *   Lexical `this` binding (doesn't create its own `this` context, inherits from surrounding scope - important for object methods and callbacks).
    ```javascript
    // Basic
    const multiply = (x, y) => {
      return x * y;
    };

    // Single expression, implicit return
    const square = num => num * num;

    // No parameters
    const logTime = () => console.log(new Date());

    console.log(multiply(4, 5)); // 20
    console.log(square(7));      // 49
    logTime();
    ```
*   **Parameters vs. Arguments:** Parameters are variables listed in the function definition. Arguments are the actual values passed to the function when it's called.
*   **Return Value:** Functions use the `return` keyword to send a value back. If `return` is omitted or used without a value, the function returns `undefined`. `return` also exits the function immediately.
*   **🔄 Higher-Order Functions:** Functions that operate on other functions, either by taking them as arguments or by returning them (e.g., `map`, `filter`, `reduce`, `forEach`, `setTimeout`).
*   **📞 Callback Functions:** Functions passed as arguments to other functions, to be executed later (e.g., the function passed to `addEventListener` or `setTimeout`).

---

### Section 9: 🎯 Scope & Closures - Where Variables Live

Understanding variable visibility and function memory.

*   **Scope:** Determines the accessibility (visibility) of variables.
    *   **Global Scope:** Variables declared outside any function or block. Accessible from anywhere. Avoid polluting the global scope!
    *   **Function (Local) Scope:** Variables declared inside a function (`var`, `let`, `const`). Accessible only within that function.
    *   **Block Scope:** Variables declared inside a block `{}` (`let`, `const`). Accessible only within that block (e.g., inside `if`, `for`). `var` does *not* have block scope.
*   **🧱 Closures:** A function "remembers" and continues to access variables from its **outer (enclosing) lexical scope**, even after the outer function has finished executing and returned. Powerful for creating private data and stateful functions.
    ```javascript
    function createCounter() {
      let count = 0; // Variable in outer scope
      return function() { // Inner function forms a closure
        count++;
        console.log(count);
      };
    }

    const counter1 = createCounter();
    const counter2 = createCounter();

    counter1(); // 1
    counter1(); // 2 (remembers its own 'count')
    counter2(); // 1 (has its own separate 'count')
    ```
*   ** hoisting ( `var` Behavior - Avoid!):** During compilation, `var` declarations (but not initializations) are moved to the top of their scope (function or global). Function declarations are also hoisted (name and body). `let` and `const` are hoisted but enter a "temporal dead zone" (TDZ) - they cannot be accessed before their actual declaration line, preventing errors caused by using uninitialized variables.
    ```javascript
    console.log(myVar); // undefined (declaration hoisted, initialization isn't)
    var myVar = 10;

    // console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization (TDZ)
    let myLet = 20;
    ```

---

### Section 10: 📋 Arrays - Ordered Collections

Storing lists of data.

*   **Definition:** Ordered, zero-indexed collection of values. Can hold mixed data types. Arrays are objects.
    ```javascript
    const fruits = ["Apple", "Banana", "Cherry"];
    const mixed = [1, "two", true, null, { id: 3 }];
    ```
*   **Accessing Elements:** Use zero-based index in square brackets `[]`.
    ```javascript
    console.log(fruits[0]); // "Apple"
    console.log(fruits[2]); // "Cherry"
    console.log(fruits[3]); // undefined (index out of bounds)
    ```
*   **`length` Property:** Get the number of elements.
    ```javascript
    console.log(fruits.length); // 3
    ```
*   **Updating Elements:** Assign a new value using the index.
    ```javascript
    fruits[1] = "Blueberry";
    console.log(fruits); // ["Apple", "Blueberry", "Cherry"]
    ```
*   **Nested Arrays (2D Arrays):** Arrays containing other arrays. Access using multiple indices `array[row][column]`.
    ```javascript
    const matrix = [ [1, 2], [3, 4] ];
    console.log(matrix[0][1]); // 2
    ```
*   **Destructuring Assignment:** Easily extract array values into variables.
    ```javascript
    const points = [10, 20, 30];
    const [x, y, z] = points;
    console.log(y); // 20
    ```
*   **Rest Syntax (`...`):** Collect remaining elements into a new array during destructuring.
    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    const [first, second, ...others] = numbers;
    console.log(others); // [3, 4, 5]
    ```
*   **Spread Syntax (`...`):** Expands an iterable (like an array) into individual elements. Useful for creating shallow copies, merging arrays, or passing array elements as function arguments.
    ```javascript
    const arr1 = [1, 2];
    const arr2 = [3, 4];
    const combined = [...arr1, 0, ...arr2]; // [1, 2, 0, 3, 4]
    const copy = [...arr1]; // Shallow copy
    console.log(Math.max(...numbers)); // Equivalent to Math.max(1, 2, 3, 4, 5)
    ```
*   **🧬 Common Array Methods:**
    *   **Mutating (Modify Original Array):**
        *   `push(item1, ...)`: Adds to the **end**. Returns new length.
        *   `pop()`: Removes from the **end**. Returns removed item.
        *   `shift()`: Removes from the **beginning**. Returns removed item.
        *   `unshift(item1, ...)`: Adds to the **beginning**. Returns new length.
        *   `splice(startIndex, deleteCount, item1, ...)`: Versatile! Removes/replaces/adds elements *in place*. Returns array of removed items.
        *   `reverse()`: Reverses the order *in place*.
        *   `sort(compareFn)`: Sorts *in place*. **Needs a compare function for numbers!** Default sort is lexicographical (string-based).
            ```javascript
            // Sort numbers numerically (ascending)
            numbers.sort((a, b) => a - b);
            // Sort numbers numerically (descending)
            numbers.sort((a, b) => b - a);
            ```
    *   **Non-Mutating (Return New Array/Value):**
        *   `indexOf(item)`: Returns first index of `item` (-1 if not found).
        *   `includes(item)`: Returns `true`/`false` if `item` exists.
        *   `slice(startIndex, endIndex)`: Returns a *shallow copy* of a portion (end index non-inclusive).
        *   `concat(arr1, arr2, ...)`: Merges arrays, returns a new array.
        *   `join(separator)`: Joins elements into a string using `separator`.
        *   **Higher-Order Methods (Very Common!):**
            *   `forEach(callbackFn)`: Executes `callbackFn` for each element. Doesn't return anything useful (`undefined`).
            *   `map(callbackFn)`: Creates a **new array** by applying `callbackFn` to each element and collecting the results.
            *   `filter(callbackFn)`: Creates a **new array** containing only elements for which `callbackFn` returns `true`.
            *   `reduce(callbackFn, initialValue)`: Reduces the array to a **single value** by applying `callbackFn` cumulatively. `callbackFn(accumulator, currentValue, index, array)`.
            *   `every(callbackFn)`: Returns `true` if `callbackFn` returns `true` for **all** elements.
            *   `some(callbackFn)`: Returns `true` if `callbackFn` returns `true` for **at least one** element.
            *   `find(callbackFn)`: Returns the **first element** for which `callbackFn` returns `true`.
            *   `findIndex(callbackFn)`: Returns the **index** of the first element for which `callbackFn` returns `true`.

---

### Section 11: 📦 Objects - Key-Value Collections

Storing structured data with named properties.

*   **Definition:** Unordered collection of key-value pairs. Keys are strings or Symbols. Values can be anything.
    ```javascript
    const book = {
      title: "The Hobbit",
      author: "J.R.R. Tolkien",
      pages: 310,
      "ISBN-10": "054792822X", // Keys with hyphens need quotes
      read: function() { console.log(`Reading ${this.title}...`); } // Method
    };
    ```
*   **Accessing Properties:**
    *   **Dot Notation (`object.key`):** Simple, common. Only works for valid identifier keys (no spaces, hyphens, starting numbers).
    *   **Bracket Notation (`object['key']`):** Works for *any* string key (including those with spaces/hyphens). Required when the key is stored in a variable.
    ```javascript
    console.log(book.title);         // "The Hobbit"
    console.log(book["author"]);     // "J.R.R. Tolkien"
    console.log(book["ISBN-10"]);    // Access key with hyphen
    let propertyName = "pages";
    console.log(book[propertyName]); // Access using variable: 310
    ```
*   **Setting/Updating Properties:** Use dot or bracket notation with the assignment operator `=`.
    ```javascript
    book.genre = "Fantasy";
    book["year"] = 1937;
    ```
*   **Removing Properties:** Use the `delete` operator.
    ```javascript
    delete book.year;
    ```
*   **Checking Property Existence:**
    *   `hasOwnProperty(key)`: Checks if object has the property *directly* (not inherited). Returns `true`/`false`.
    *   `in` Operator: Checks if property exists in object *or its prototype chain*. Returns `true`/`false`.
    ```javascript
    console.log(book.hasOwnProperty("title")); // true
    console.log("title" in book);             // true
    console.log("toString" in book);          // true (inherited from Object prototype)
    ```
*   **Nested Objects:** Objects containing other objects. Access properties by chaining `.` or `[]`.
    ```javascript
    const user = { info: { address: { city: "Paris" } } };
    console.log(user.info.address.city); // "Paris"
    ```
*   **Object Methods:** Functions stored as object properties. Use `this` keyword inside the method to refer to the object itself.
    ```javascript
    book.read(); // Calls the read method
    ```
*   **`this` Keyword:** Its value depends on *how* a function is called (more complex topic, but in object methods called like `object.method()`, `this` usually refers to `object`). Arrow functions handle `this` differently (lexically).
*   **Optional Chaining (`?.`):** Safely access nested properties or call methods without causing an error if an intermediate property is `null` or `undefined`. Returns `undefined` instead of erroring.
    ```javascript
    console.log(user.profile?.address?.street); // undefined (if profile or address is missing)
    user.getPreferences?.(); // Calls method only if it exists
    ```
*   **Object Destructuring:** Extract object properties into variables. Can rename variables and provide default values.
    ```javascript
    const { title, author: writer, pages = 0 } = book;
    console.log(title);  // "The Hobbit"
    console.log(writer); // "J.R.R. Tolkien" (renamed)
    console.log(pages);  // 310
    ```
*   **JSON (JavaScript Object Notation):** Lightweight text-based data format, looks like JS object literals. Used for data exchange (e.g., with servers). Keys *must* be double-quoted strings.
    *   `JSON.stringify(object)`: Converts a JavaScript object/value to a JSON string.
    *   `JSON.parse(jsonString)`: Converts a JSON string back into a JavaScript object/value.

---

### Section 12: 🌐 The DOM & Web APIs - Interacting with the Browser

Making web pages dynamic by manipulating HTML and accessing browser features.

*   **API (Application Programming Interface):** A set of rules allowing software components to communicate.
*   **Web APIs:** APIs specifically for web development.
    *   **Browser APIs:** Built into the browser (DOM, Geolocation, Fetch, Web Storage, Console).
    *   **Third-Party APIs:** Provided by external services (Google Maps API, Twitter API).
*   **DOM (Document Object Model):** A programming interface for HTML documents. Represents the page structure as a tree of objects (nodes). JavaScript can manipulate this tree to change page content and structure dynamically.
*   **Selecting Elements:**
    *   `document.getElementById(id)`: Gets the single element with the given ID. Fast.
    *   `document.querySelector(cssSelector)`: Gets the **first** element matching the CSS selector. Very versatile.
    *   `document.querySelectorAll(cssSelector)`: Gets a **NodeList** (array-like) of *all* elements matching the CSS selector.
*   **Manipulating Elements:**
    *   `element.innerHTML`: Gets or sets the HTML content *inside* an element. **Use with caution for setting** – can create security risks (XSS) if setting untrusted content. Re-parses HTML.
    *   `element.textContent`: Gets or sets the *text* content (no HTML tags). Safer for setting text.
    *   `element.innerText`: Gets the *rendered* text content (considers CSS styles like `display:none`). Setting it is similar to `textContent`.
    *   `document.createElement(tagName)`: Creates a new HTML element node.
    *   `parentNode.appendChild(childNode)`: Adds `childNode` to the end of `parentNode`'s children.
    *   `parentNode.removeChild(childNode)`: Removes `childNode` from `parentNode`.
    *   `element.setAttribute(name, value)`: Sets an attribute's value.
    *   `element.getAttribute(name)`: Gets an attribute's value.
    *   `element.removeAttribute(name)`: Removes an attribute.
    *   `element.style.property = value`: Accesses/sets *inline* styles (e.g., `element.style.color = 'blue'`). Property names are camelCased (e.g., `backgroundColor`).
    *   `element.classList`: Provides methods to manage classes: `add()`, `remove()`, `toggle()`, `contains()`. **🏆 Preferred way to change styles via CSS classes.**
*   **Events:** Actions that happen in the browser (user clicks, key presses, page loads, etc.).
    *   **Event Object:** Passed to the event handler function, contains information about the event (e.g., `event.target`, `event.key`, `event.clientX`).
    *   **`element.addEventListener(eventType, callbackFn, options)`:** The standard way to attach an event listener. `eventType` is a string like `"click"`, `"mouseover"`, `"keydown"`. `callbackFn` is the function to run when the event occurs.
    *   **`element.removeEventListener(eventType, callbackFn, options)`:** Removes a listener (must reference the *exact same* function).
    *   **Inline Event Handlers (`onclick="..."`):** Attributes in HTML. **Avoid** - mixes HTML and JS, less flexible.
    *   **Common Events:** `click`, `mouseover`, `mouseout`, `mousedown`, `mouseup`, `keydown`, `keyup`, `keypress`, `focus`, `blur`, `change` (for inputs), `input` (for inputs), `submit` (for forms), `load`, `DOMContentLoaded`.
*   **`DOMContentLoaded` Event:** Fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading. Good place to run setup JavaScript that needs the DOM ready.
*   **Event Bubbling:** When an event occurs on an element, it first runs handlers on that element, then "bubbles up" to its parent, then the parent's parent, and so on, up to the `window`.
*   **Event Delegation:** Attach a single event listener to a *parent* element to manage events for multiple child elements. Uses event bubbling. Efficient, especially for dynamically added elements. Check `event.target` inside the handler to see which child triggered the event.
*   **`event.preventDefault()`:** Stops the browser's default action for an event (e.g., stops a link from navigating, stops a form from submitting).
*   **`event.stopPropagation()`:** Stops the event from bubbling further up the DOM tree. Use sparingly.

---

### Section 13: ⏳ Asynchronous JavaScript - Handling Delays

Performing operations (like network requests, timers) without blocking the main thread.

*   **Synchronous vs. Asynchronous:**
    *   **Sync:** Code executes line by line, one operation finishes before the next starts. Long operations block everything else.
    *   **Async:** Operations can start, run in the background, and finish later without blocking the main thread. Essential for responsive UIs.
*   **Callbacks (Traditional):** Passing a function to another function to be executed when an async operation completes. Can lead to "Callback Hell" (deeply nested, hard-to-read code).
*   **Promises (Modern):** An object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. Can be in one of three states:
    1.  `pending`: Initial state, neither fulfilled nor rejected.
    2.  `fulfilled`: Operation completed successfully.
    3.  `rejected`: Operation failed.
    *   **`.then(onFulfilled, onRejected)`:** Attaches callbacks for fulfillment and rejection. Returns a *new* Promise, allowing **chaining**.
    *   **`.catch(onRejected)`:** Shorthand for handling only rejections. Catches errors from the preceding chain.
    *   **`.finally(onFinally)`:** Executes a callback when the promise settles (either fulfilled or rejected). Good for cleanup.
    ```javascript
    fetch('/api/data') // fetch returns a Promise
      .then(response => {
        if (!response.ok) { throw new Error('Network response was not ok'); }
        return response.json(); // .json() also returns a Promise
      })
      .then(data => {
        console.log('Data fetched:', data);
      })
      .catch(error => {
        console.error('Fetch error:', error);
      })
      .finally(() => {
        console.log('Fetch attempt finished.');
      });
    ```
*   **`async`/`await` (Syntactic Sugar for Promises - 🏆 Preferred):** Makes async code look and behave more like synchronous code, improving readability.
    *   **`async function`:** Declares a function that implicitly returns a Promise.
    *   **`await`:** Pauses the execution of an `async` function **until** a Promise settles. Can only be used *inside* an `async` function. Returns the fulfilled value or throws the rejected reason.
    *   **Error Handling:** Use standard `try...catch...finally` blocks.
    ```javascript
    async function fetchData() {
      console.log("Fetching data...");
      try {
        const response = await fetch('/api/data'); // Pause until fetch resolves/rejects
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json(); // Pause until json() resolves
        console.log("Data received:", data);
        return data; // Resolved value of the async function's promise
      } catch (error) {
        console.error("Could not fetch data:", error);
        // Handle error or re-throw
      } finally {
        console.log("Fetch attempt finished.");
      }
    }
    fetchData().then(result => console.log("Async function finished."));
    ```
*   **Timers:**
    *   `setTimeout(callbackFn, delayInMs)`: Executes `callbackFn` *once* after `delayInMs`. Returns a timer ID.
    *   `setInterval(callbackFn, intervalInMs)`: Executes `callbackFn` *repeatedly* every `intervalInMs`. Returns an interval ID.
    *   `clearTimeout(timerId)` / `clearInterval(intervalId)`: Cancels the scheduled timer/interval.
*   **`requestAnimationFrame(callbackFn)`:** Tells the browser you wish to perform an animation. Requests that `callbackFn` be called before the next repaint. Smoother animations than `setInterval`. Returns an ID cancelable with `cancelAnimationFrame()`.

---

### Section 14: 🏗️ Classes & Object-Oriented Concepts (OOP Basics)

Blueprints for creating objects with shared properties and methods.

*   **Class Definition:** Uses the `class` keyword.
    ```javascript
    class Player {
      // Constructor: Special method for creating and initializing objects
      constructor(name, score = 0) {
        this.name = name; // 'this' refers to the new instance being created
        this.score = score;
      }

      // Method: Function defined within the class
      incrementScore(points) {
        this.score += points;
        console.log(`${this.name}'s score: ${this.score}`);
      }

      // Static Method: Called on the class itself, not instances
      static description() {
        return "A class representing a game player.";
      }
    }
    ```
*   **Constructor:** Initializes new objects created from the class. Called automatically with `new`.
*   **`this` Keyword:** Inside constructor and methods, `this` refers to the specific instance of the class being worked on.
*   **Creating Instances:** Use the `new` keyword.
    ```javascript
    const player1 = new Player("Alice");
    const player2 = new Player("Bob", 50);
    player1.incrementScore(10); // Alice's score: 10
    console.log(Player.description()); // Access static method via class name
    ```
*   **Inheritance (`extends`, `super`):** Create child classes that inherit properties/methods from a parent class.
    *   `extends`: Keyword to specify the parent class.
    *   `super()`: Calls the parent class's constructor (must be called in child constructor *before* using `this` if inheriting).
    *   `super.methodName()`: Calls a method from the parent class.
    ```javascript
    class Mage extends Player {
      constructor(name, score, mana) {
        super(name, score); // Call parent constructor
        this.mana = mana;
      }

      castSpell() {
        if (this.mana >= 10) {
          this.mana -= 10;
          console.log(`${this.name} casts a spell! Mana left: ${this.mana}`);
        } else {
          console.log(`${this.name} needs more mana!`);
        }
      }

      // Override parent method (optional)
      incrementScore(points) {
        super.incrementScore(points * 1.1); // Call parent method + bonus
        console.log("Mage bonus applied!");
      }
    }
    const mage1 = new Mage("Gandalf", 100, 50);
    mage1.castSpell(); // Gandalf casts a spell! Mana left: 40
    mage1.incrementScore(10); // Gandalf's score: 111, Mage bonus applied!
    ```
*   **Static Methods & Properties:** Belong to the class itself, not instances. Accessed via `ClassName.staticMember`. Useful for utility functions or class-level constants.

---

### Section 15: 🧩 Modules & Code Organization - Imports & Exports

Breaking code into reusable, self-contained files.

*   **Module:** A JavaScript file treated as a module. Variables/functions inside are scoped to the module by default (not global).
*   **`export`:** Makes variables, functions, or classes available for use in *other* modules.
    *   **Named Export:** Export specific items by name. Can have multiple per module.
        ```javascript
        // utils.js
        export const PI = 3.14;
        export function calculateCircumference(radius) {
          return 2 * PI * radius;
        }
        ```
    *   **Default Export:** Export a single "main" value from the module. Only *one* default export per module.
        ```javascript
        // User.js
        export default class User {
          // ... class definition ...
        }
        ```
*   **`import`:** Brings exported items from another module into the current module. Must typically be at the top level.
    *   **Named Import:** Import specific items using curly braces `{}`. Names must match exports. Can use `as` to rename.
        ```javascript
        // main.js
        import { PI, calculateCircumference as calcCirc } from './utils.js';
        console.log(calcCirc(10));
        ```
    *   **Default Import:** Import the default export. You choose the name.
        ```javascript
        // main.js
        import CustomUser from './User.js';
        const user = new CustomUser();
        ```
    *   **Namespace Import:** Import *all* named exports as properties of a single object.
        ```javascript
        // main.js
        import * as utils from './utils.js';
        console.log(utils.PI);
        console.log(utils.calculateCircumference(5));
        ```
*   **Usage in HTML:** Link your main JS file using `<script type="module" src="main.js"></script>`.

---

### Section 16: ⚙️ Advanced Concepts & APIs

More specialized features and browser capabilities.

*   **Recursion:** A function calling itself until a base case is met. Useful for problems with self-similar structures (trees, factorials). Be careful with base cases to avoid infinite loops and stack overflow.
*   **Pure vs. Impure Functions:**
    *   **Pure:** Given the same input, always returns the same output. Has no side effects (doesn't modify external state). Easier to test and reason about.
    *   **Impure:** May produce different outputs for the same input or have side effects (modify external variables, log to console, make network requests).
*   **Functional Programming:** Paradigm emphasizing pure functions, immutability, avoiding side effects. Array methods like `map`, `filter`, `reduce` are functional concepts.
*   **Currying:** Transforming a function with multiple arguments into a sequence of nested functions, each taking a single argument.
*   **Regular Expressions (Regex):** Patterns used to match character combinations in strings. Powerful for searching, validation, and manipulation. Uses special syntax (`/pattern/flags`). Common methods: `test()`, `match()`, `matchAll()`, `replace()`, `replaceAll()`, `search()`.
*   **Error Handling (`try...catch...finally`, `throw`):**
    *   `try`: Wrap code that might throw an error.
    *   `catch (error)`: Execute if an error is thrown in the `try` block. Access error details via the `error` object.
    *   `finally`: Execute *always* after `try` (and `catch`, if applicable), regardless of errors. Good for cleanup.
    *   `throw`: Manually create and throw an error (`throw new Error("Something went wrong!")`).
*   **Debugging Techniques:** `console.log`, `console.dir`, `console.table`, Browser DevTools (Breakpoints, Watchers, Call Stack, Profiling), `debugger` statement.
*   **Sets & Maps:**
    *   **`Set`:** Collection of **unique** values (primitive or object references). Good for removing duplicates. Methods: `add()`, `delete()`, `has()`, `clear()`, `size`.
    *   **`Map`:** Collection of key-value pairs where keys can be **any data type** (unlike plain objects where keys are strings/Symbols). Remembers insertion order. Methods: `set()`, `get()`, `delete()`, `has()`, `clear()`, `size`.
    *   **`WeakSet` / `WeakMap`:** Hold "weak" references to objects. If an object is only referenced by a WeakSet/WeakMap, it can be garbage collected. Keys must be objects. Not iterable.
*   **Persistent Storage (Browser):**
    *   **`localStorage`:** Stores key-value pairs (strings only!) **persistently** across browser sessions. Data remains until explicitly cleared. (~5-10MB limit).
    *   **`sessionStorage`:** Stores key-value pairs (strings only!) for the **current browser session only**. Data cleared when tab/window is closed. (~5-10MB limit).
    *   **Cookies:** Small pieces of data sent between server and browser. Used for session management, tracking. Can have expiration dates, security flags (`HttpOnly`, `Secure`). Accessible via `document.cookie` (complex) or server headers. Size limit (~4KB).
    *   **IndexedDB:** Low-level API for client-side storage of significant amounts of structured data, including files/blobs. Transactional database. More complex than Web Storage.
    *   **Cache API:** Part of Service Workers. Stores network Request/Response pairs. Used for offline support and performance.
*   **Web APIs (More Examples):**
    *   **`fetch` API:** Modern way to make network requests (replacement for older `XMLHttpRequest`). Promise-based.
    *   **Geolocation API (`navigator.geolocation`):** Request user's location (requires permission).
    *   **Web Audio API:** Process and synthesize audio.
    *   **Canvas API:** Draw graphics dynamically via script.
    *   **Media APIs (Audio/Video, MediaStream, Screen Capture):** Control media playback, access camera/microphone, record screen.

---

### 🎉 Final Checklist & Good Luck! 🎉

1.  ❓ **Review Key Differences:** `let`/`const`/`var`, `==`/`===`, `null`/`undefined`, `map`/`forEach`, `localStorage`/`sessionStorage`.
2.  🔄 **Understand Async:** Explain Promises and `async/await`. How do they prevent blocking?
3.  🖱️ **DOM Manipulation:** How do you select elements? How do you change their content, attributes, or styles? How do events work?
4.  🧩 **Practice Problems:** Work through coding exercises involving arrays, objects, functions, and control flow.
5.  🛠️ **Use DevTools:** Inspect variables, step through code, check network requests.
6.  😴 **Rest Your Brain!**

You've covered a massive amount of JavaScript! Believe in your preparation and tackle that exam! 💪
