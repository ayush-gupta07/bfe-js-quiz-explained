# [01 - Promise Order](https://bigfrontend.dev/quiz/1-promise-order)

---

## ❓ Question

```js
console.log(1);
const promise = new Promise((resolve, reject) => {
    console.log(2);
    resolve();
    console.log(3); 
});

console.log(4);

promise.then(() => {
    console.log(5);
}).then(() => {
    console.log(6);
});

console.log(7);

setTimeout(() => {
    console.log(8);
}, 10);

setTimeout(() => {
    console.log(9);
}, 0);
```

---

## ✅ Output

```
1
2
3
4
7
5
6
9
8
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. **Synchronous phase** (Runs immediately on the call stack):
   - `console.log(1)` → prints `1`
   - `new Promise(...)` is instantiated:
     - Logs `2`
     - `resolve()` is called → this queues the `.then()` callbacks in **microtask queue**
     - Logs `3`
   - `console.log(4)` → prints `4`
   - `promise.then(...)` and `.then(...)` chained → callbacks registered to run after microtasks
   - `console.log(7)` → prints `7`
   - Two `setTimeout()` calls queued in **macrotask queue**

2. **Microtask phase (after call stack is empty):**
   - `.then(() => console.log(5))` → prints `5`
   - `.then(() => console.log(6))` → prints `6`

3. **Macrotask phase:**
   - `setTimeout(..., 0)` → prints `9`
   - `setTimeout(..., 10)` → prints `8`

### 🔍 Internal Mechanics

- Microtasks (like `.then`) always run **after the current script finishes** but **before** any macrotasks.
- `resolve()` is synchronous — it schedules the `.then()` callbacks but **does not stop further synchronous execution**.
- The code after `resolve()` (i.e., `console.log(3)`) still runs synchronously.

---

## ⚠️ Things to Remember / Gotchas

- `resolve()` **does not return** or halt execution inside the Promise executor.
  → You must explicitly use `return resolve()` if you want to stop execution after resolving.
- `.then()` chains are microtasks, and **always execute after** the current call stack is clear.
- Even `setTimeout(..., 0)` is placed in the **macrotask queue**, meaning it runs **after all microtasks**.
- Console output order tests your knowledge of **execution phases**, **promise resolution**, and **event loop**.