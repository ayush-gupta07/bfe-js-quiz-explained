# [03 - Promise then callbacks](https://bigfrontend.dev/quiz/3-promise-then-callbacks)

## ❓ Question
```js
Promise.resolve(1)
  .then(() => 2)
  .then(3)
  .then((value) => value * 3)
  .then(Promise.resolve(4))
  .then(console.log)
```

---

## ✅ Output

```
4
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

Let's trace through each `.then()` in sequence:

1. `Promise.resolve(1)`
   - Returns a promise that resolves with value `1`.

2. `.then(() => 2)`
   - This function is called with `1` (from above), but ignores it and returns `2`.
   - The promise is resolved with value `2`.

3. `.then(3)`
   - **Gotcha**: Passing a non-function (like number `3`) to `.then()` is effectively a no-op.
   - JavaScript internally treats this as `.then(val => val)`.
   - So the value `2` just passes through.

4. `.then((value) => value * 3)`
   - Gets `2` and returns `6`.

5. `.then(Promise.resolve(4))`
   - **Gotcha**: If you pass a promise instead of a function to `.then()`, JavaScript treats it as `.then(val => Promise.resolve(4))`.
   - So it overrides the `6` with `4`.

6. `.then(console.log)`
   - Logs: `4`

---

## ⚠️ Things to Remember / Gotchas

- If you pass a **non-function** (like a number) to `.then()`, it is treated as `.then(val => val)`.
- If you pass a **promise instead of a function** to `.then()`, it is treated as `.then(() => thatPromise)`.
- Chained `.then()` callbacks are only triggered with functions.
- Always ensure to pass function references or lambdas in `.then()`.
