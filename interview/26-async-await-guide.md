# Async/Await Guide

## Core Concept
- **Async/await** is a JavaScript syntax that makes asynchronous code look and behave more like synchronous code, simplifying the handling of Promises
- 🧵 **Mental Model**: Think of async/await as a "pause and resume" button for your code - it pauses execution until a Promise resolves, then resumes where it left off
- **Visual representation**:
  ```
  ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
  │ Start async │────▶│ await       │────▶│ Continue    │
  │ function    │     │ (Pause here)│     │ after await │
  └─────────────┘     └─────────────┘     └─────────────┘
                            │
                            ▼
                      ┌─────────────┐
                      │ Promise     │
                      │ resolves    │
                      └─────────────┘
  ```

---

## Key Mechanics
```javascript
async function getData() {
  console.log('Before await'); // Runs first
  const result = await fetch('/api/data'); // Pauses here until Promise resolves
  console.log('After await'); // Runs after Promise resolves
  return await result.json(); // Returns a Promise that resolves to the JSON data
}

// Output:
// "Before await"
// ... (time passes)
// "After await"
```

- 🔑 **async** functions always return a **Promise**, even if you return a non-Promise value
- ⏳ **await** can only be used inside an **async** function (or at the top level in modern JavaScript)
- 🛑 **Error handling** works with try/catch blocks, making error management more intuitive
- 🔄 Multiple awaits in sequence will execute in order, while Promises can be run in parallel using `Promise.all()`

---

## Interview Mastery

**Q1: What happens if you don't use await inside an async function?**
> Without await, the function will continue execution without pausing. You're essentially not taking advantage of the async/await pattern, and your code will behave like regular Promise-based code.

**Q2: How would you handle errors with async/await?**
> Use try/catch blocks around await statements:
> ```javascript
> async function fetchData() {
>   try {
>     const data = await fetch('/api/data');
>     return await data.json();
>   } catch (error) {
>     console.error('Error fetching data:', error);
>     throw error; // Re-throw or handle appropriately
>   }
> }
> ```

**Critical Connections:**
- 🤝 **Promises**: Async/await is built on Promises; every async function returns a Promise, and await expects a Promise
- 🔄 **Event Loop**: Understanding how async/await interacts with JavaScript's event loop explains its non-blocking behavior

**Remember:** Async/await doesn't make asynchronous operations faster - it just makes them cleaner to write and easier to reason about by providing synchronous-looking code that behaves asynchronously under the hood.
