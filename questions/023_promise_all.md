# [23 - Promise.all()](https://bigfrontend.dev/quiz/Promise-all)

## ❓ Question
```javascript
(async () => {
  await Promise.all([]).then((value) => {
    console.log(value)
  }, (error) => {
    console.log(error)
  })
  
  await Promise.all([1,2,Promise.resolve(3), Promise.resolve(4)]).then((value) => {
    console.log(value)
  }, (error) => {
    console.log(error)
  })
  
  await Promise.all([1,2,Promise.resolve(3), Promise.reject('error')]).then((value) => {
    console.log(value)
  }, (error) => {
    console.log(error)
  })
})()
```

---

## ✅ Output

```
[]
[1, 2, 3, 4]
error
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. **First `Promise.all([])`** with **empty array**:
   - `Promise.all([])` resolves immediately with an empty array `[]`.
   - The success handler logs `[]`.

2. **Second `Promise.all([1,2,Promise.resolve(3), Promise.resolve(4)])`**:
   - Non-promise values (`1`, `2`) are automatically wrapped in `Promise.resolve()`.
   - All promises resolve successfully: `[1, 2, 3, 4]`.
   - The success handler logs `[1, 2, 3, 4]`.

3. **Third `Promise.all([1,2,Promise.resolve(3), Promise.reject('error')])`**:
   - Contains one rejected promise: `Promise.reject('error')`.
   - `Promise.all()` **fails fast** - if any promise rejects, the entire operation rejects.
   - The error handler logs `'error'` (the rejection value).

### 🔍 Internal Mechanics

- `Promise.all([])` resolves immediately with `[]` (edge case behavior).
- Non-promise values are **auto-wrapped** in resolved promises.
- `Promise.all()` uses **fail-fast behavior** - one rejection fails everything.
- Results maintain the **same order** as the input array, regardless of resolution timing.
- `await` waits for the entire `.then()` chain to complete before moving to the next statement.

---

## ⚠️ Things to Remember / Gotchas

- **Empty array** resolves immediately to `[]`, not undefined.
- **Fail-fast behavior**: One rejection cancels everything, even if other promises succeed.
- Non-promise values are automatically converted to resolved promises.
- Results **preserve input order**, not resolution order.
- `Promise.all()` is **all-or-nothing** - use `Promise.allSettled()` if you want all results regardless of failures.
