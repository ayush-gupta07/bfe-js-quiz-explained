# [02 – Promise Executor](https://bigfrontend.dev/quiz/2-promise-executor)

## ❓ Question

```js
new Promise((resolve, reject) => {
  resolve(1)
  resolve(2)
  reject('error')
}).then((value) => {
  console.log(value)
}, (error) => {
  console.log('error')
})
```

---

### ✅ Output

```
1
```

---

### 🧠 Step-by-Step Explanation / Internal Implementation

1. `new Promise(...)` is invoked with an executor function. This function receives two arguments: `resolve` and `reject`.
2. `resolve(1)` is called first — this settles the promise into a "fulfilled" state with the value `1`.
3. The second call `resolve(2)` is **ignored** because a promise can only be settled once. Further calls to `resolve` or `reject` are no-ops.
4. Similarly, `reject('error')` is **ignored** as well, since the promise is already fulfilled.
5. The `then()` method is attached with two handlers:
   - `.then(onFulfilled, onRejected)`
   - Since the promise was fulfilled with value `1`, the first handler `onFulfilled` is invoked with `value = 1`, and `"1"` is printed.
6. The second handler `onRejected` is not invoked.

---

### ⚠️ Things to Remember / Gotchas

- A promise can only be settled once — either fulfilled or rejected. Any subsequent calls to `resolve()` or `reject()` are ignored.
- The executor function inside a `Promise` runs **synchronously**, but the `.then()` handlers are executed **asynchronously** (microtask queue).
- Even if `reject()` is called after `resolve()`, it will be ignored because the promise is already settled.
- This is why only `1` gets printed, not `2` or `'error'`.