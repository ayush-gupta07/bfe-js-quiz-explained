# [04 - Promise then callbacks 2](https://bigfrontend.dev/quiz/4-Promise-then-callbacks-II)

---

## ❓ Question

```js
Promise.resolve(1)
.then((val) => {
  console.log(val)
  return val + 1
}).then((val) => {
  console.log(val)
}).then((val) => {
  console.log(val)
  return Promise.resolve(3)
    .then((val) => {
      console.log(val)
    })
}).then((val) => {
  console.log(val)
  return Promise.reject(4)
}).catch((val) => {
  console.log(val)
}).finally((val) => {
  console.log(val)
  return 10
}).then((val) => {
  console.log(val)
})
```

---

## 🧾 Output

```
1
2
undefined
3
undefined
4
undefined
undefined
```

---

## 🔍 Step-by-step Explanation / Internal Implementation

1. `Promise.resolve(1)` — returns a promise resolved with `1`.

2. First `.then((val) => { console.log(val); return val + 1 })`
   - Logs `1`
   - Returns `2`

3. Second `.then((val) => { console.log(val) })`
   - Logs `2`
   - Returns `undefined` implicitly

4. Third `.then((val) => { ... })`
   - `val` is `undefined`, logs `undefined`
   - Returns a **nested** promise: `Promise.resolve(3).then(console.log)`
     - Logs `3` (inside nested `.then`)
     - Since that inner `.then()` has no return, the outer `.then()` also resolves to `undefined`

5. Fourth `.then((val) => { ... })`
   - Receives `undefined`, logs `undefined`
   - Returns `Promise.reject(4)` → goes to the `catch`

6. `.catch((val) => { console.log(val) })`
   - Logs `4`
   - Implicitly returns `undefined`, resolves chain again

7. `.finally((val) => { console.log(val); return 10 })`
   - `finally` receives `undefined` (but argument is ignored)
   - Logs `undefined`
   - Returns `10`, but it's **ignored** (finally doesn't affect the resolved value)

8. Final `.then((val) => { console.log(val) })`
   - Receives `undefined` (from previous `.catch()`)
   - Logs `undefined`

---

## 🧠 Things to Remember / Gotchas

- A `.then()` with no `return` resolves with `undefined`.
- Nested `.then()` without a return causes outer promise to resolve with `undefined`.
- `.catch()` transforms rejection → resolution with the return value (`undefined` here).
- `.finally()` does not affect the promise chain’s value unless it throws.
- Even if `finally` returns a value, it **does not override** the existing resolution/rejection.
- Internal implementation: Each `.then()` creates a microtask; nested promises also return microtasks. JavaScript schedules them accordingly using the microtask queue.