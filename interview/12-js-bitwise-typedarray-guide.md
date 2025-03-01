# JavaScript Bitwise Operators, Typed Arrays, and ArrayBuffers Guide

## Core Concept
- **Bitwise operators** manipulate data at the binary level, while **Typed Arrays** and **ArrayBuffers** provide efficient, low-level memory access for binary data operations
- 🧩 **Mental Model**: Think of bitwise operators as digital switches (on/off), typed arrays as specialized containers with uniform slots, and ArrayBuffers as reserved memory blocks
- **Visual Representation**:
  ```
  Bitwise:  0101 & 1100 = 0100  (AND operation)
  
  ArrayBuffer (raw memory):  [□□□□□□□□□□□□□□□□]
                                ↓
  Typed Arrays (views):     [Int8] [Float32] [Uint16]
  ```

---

## Key Mechanics
```javascript
// Bitwise Operations
const flags = 0b1010;  // Binary: 1010 (decimal 10)
const mask = 0b0011;   // Binary: 0011 (decimal 3)
console.log(flags & mask);  // Output: 2 (binary 0010)

// Typed Arrays with ArrayBuffer
const buffer = new ArrayBuffer(16);  // 16 bytes of memory
const int32View = new Int32Array(buffer);  // View as 4 32-bit integers
int32View[0] = 42;
const int8View = new Uint8Array(buffer);  // View same data as 16 8-bit integers
console.log(int8View[0]);  // Output: 42 (first byte of the first 32-bit integer)
```

- 🔢 **Bitwise Operators**: Include `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (left shift), `>>` (right shift), and `>>>` (**unsigned** right shift) for binary-level manipulation
- 🧠 **ArrayBuffer**: Represents a fixed-length **raw binary data buffer** that cannot be directly manipulated but serves as the foundation for typed arrays
- 📊 **Typed Arrays**: Provide **type-specific views** into ArrayBuffers (Int8Array, Uint32Array, Float64Array, etc.) for efficient binary data processing
- ⚡ **Performance**: These tools enable **high-performance computing** in JavaScript, essential for graphics, audio processing, and complex calculations

---

## Interview Mastery

**Q1: How do ArrayBuffers and Typed Arrays differ, and how do they work together?**  
A: An **ArrayBuffer** is a fixed-size raw binary data buffer that cannot be directly manipulated. **Typed Arrays** are views that provide typed access to that buffer. You create a typed array view that references an ArrayBuffer, allowing you to interact with the same memory using different data types and offsets.

**Q2: When would you use bitwise operations in JavaScript instead of standard arithmetic or logical operations?**  
A: Bitwise operations are ideal for: (1) **flag-based permission systems** where individual bits represent settings, (2) **performance-critical operations** like fast integer division/multiplication (via shifts), (3) **low-level data manipulation** like color processing, and (4) **memory-efficient storage** of multiple boolean values.

- 🔄 **Related Concept**: **Buffer APIs in Node.js** - extends these concepts for server-side I/O operations, allowing efficient file and network operations 
- 🌐 **Related Concept**: **WebGL/WebAssembly** - heavily utilize typed arrays and array buffers for high-performance graphics and computations in the browser

**Remember**: Bitwise operations, Typed Arrays and ArrayBuffers bring native-like performance to JavaScript through low-level memory manipulation. When working with binary data or performance-critical applications, these tools provide efficient alternatives to standard JavaScript objects and operations.
