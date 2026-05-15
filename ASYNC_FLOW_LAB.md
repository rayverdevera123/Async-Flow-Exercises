# Async Flow Exercises (JavaScript Event Loop / Promises / async-await)

## Learning Objectives
- Understand synchronous execution
- Identify asynchronous operations
- Predict output of async code
- Explain Event Loop behavior
- Differentiate between Microtasks and Macrotasks
- Debug async execution flow

---

## How to use this lab
For each subtask:
1. Copy the code into a single JavaScript file (e.g., `lab.js`).
2. Run it (Node.js) or open in your browser console.
3. Predict the output **before** you run.
4. Compare with the real output.

> Tip (Node.js):
> - Save as `lab.js` and run `node lab.js`.

---

## Step 1: Understanding Synchronous Execution

### Subtask 1.1: Write Basic Sync Code
**Task:** Write simple `console.log` statements.

```js
console.log("A");
console.log("B");
console.log("C");
```

---

## Step 2: Introduction to `setTimeout` (Macrotask)

### Subtask 2.1: Basic `setTimeout` Example
**Task:** Use `setTimeout` with `0ms` delay.

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

**What to think about:**
- `setTimeout` callbacks are scheduled as **macrotasks**.
- Synchronous code runs to completion before queued macrotasks run.

---

## Step 3: Introduction to Promises (Microtask)

### Subtask 3.1: Basic Promise Example
**Task:** Use `Promise.resolve()` with `.then()`.

```js
console.log("Start");

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**What to think about:**
- Promise `.then(...)` handlers are queued as **microtasks**.
- Microtasks run **before** the next macrotask.

---

## Step 4: Microtask vs Macrotask Comparison

### Subtask 4.1: Combine Promise & `setTimeout`
**Task:** Write code including both Promise and `setTimeout`.

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Goal:** Determine the order:
- Synchronous logs happen first.
- Then all microtasks.
- Then macrotasks.

---

## Step 5: Async/Await Flow

### Subtask 5.1: Create Async Function
**Task:** Use `async` function with `await Promise`.

```js
async function test() {
  console.log("1");
  await Promise.resolve();
  console.log("2");
}

console.log("3");
test();
console.log("4");
```

**What to think about:**
- `await` pauses the async function.
- `await Promise.resolve()` schedules the continuation as a microtask.

---

## Step 6: Advanced Flow Challenge (Predict the Output)

### Subtask 6.1: Predict the Output
Analyze the following code:

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```

---

## Answer Key (for instructors / after learners predict)

### Step 1.1
Expected:
- A
- B
- C

### Step 2.1
Expected:
- Start
- End
- Timeout

### Step 3.1
Expected:
- Start
- End
- Promise

### Step 4.1
Expected:
- Start
- End
- Promise
- Timeout

### Step 5.1
Expected:
- 3
- 1
- 4
- 2

### Step 6.1
Expected:
- A
- D
- C
- B

---

## Quick Reference (Interview-ready)
- **Synchronous**: runs immediately, in order.
- **Microtasks** (Promises): run after the current call stack empties, before macrotasks.
- **Macrotasks** (`setTimeout`, `setInterval`, I/O): run after microtasks.
- `async/await` continues via Promise microtasks.

