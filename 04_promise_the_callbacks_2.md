# [04 - Promise then callbacks 2](https://bigfrontend.dev/quiz/4-Promise-then-callbacks-II)

## ❓ Question

What does the following code output?

```js
Promise.resolve(1)
  .then((val) => {
    console.log(val);
    return val + 1;
  })
  .then((val) => {
    console.log(val);
  })
  .then((val) => {
    console.log(val);
    return Promise.resolve(3).then((val) => {
      console.log(val);
    });
  })
  .then((val) => {
    console.log(val);
    return Promise.reject(4);
  })
  .catch((val) => {
    console.log(val);
  })
  .finally((val) => {
    console.log(val);
    return 10;
  })
  .then((val) => {
    console.log(val);
  });
```

---

## ✅ Output

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

## 🔍 Explanation (Step-by-Step)

1. `Promise.resolve(1)` creates a resolved promise with value `1`.
2. First `.then()` logs `1` and returns `2`.
3. Second `.then()` receives `2`, logs it, but returns `undefined`.
4. Third `.then()` receives `undefined`, logs it, then returns a **nested** promise:
   - `Promise.resolve(3).then(...)` logs `3`, but does not return anything ⇒ resolves with `undefined`.
5. Fourth `.then()` receives `undefined`, logs it, and returns `Promise.reject(4)` ⇒ the chain enters the **rejected** state.
6. `.catch()` catches the rejection value `4`, logs it, and **implicitly returns `undefined`**, making the chain resolved again.
7. `.finally()` always runs regardless of state:
   - Logs `undefined` (it receives nothing or previous state’s value).
   - Returns `10` but doesn't change chain value (finally always passes through).
8. Final `.then()` receives **previous value**, which is `undefined`, and logs it.

---

## 🧠 Things to Remember

- If a `.then()` doesn’t return anything, it passes `undefined` to the next handler.
- A nested promise chain needs explicit return values to propagate results.
- `finally()` does **not** affect the resolved value of the chain.
- `catch()` changes state back to fulfilled unless it throws/rejects again.

---

## ⚠️ Gotchas

- **Nested Promise Resolution**: Returning `Promise.resolve(3).then(...);` but the inner `.then()` doesn't return anything ⇒ full chain gets `undefined`.
- **finally() Return Value Is Ignored**: Even if `finally()` returns `10`, the next `.then()` still receives the original value (in this case, `undefined`).
- **Multiple Chained .then()**: Make sure to **always return** something if next handler relies on value.
- **Returning Rejected Promises**: `Promise.reject(4)` inside `.then()` will directly skip the next `.then()` and move to `.catch()`.

---

## 📌 Summary Checklist

- [x] First promise resolved immediately.
- [x] Explicit return of `val + 1`.
- [x] Implicit `undefined` propagation.
- [x] Nested Promise resolved without returning ⇒ `undefined`.
- [x] Error recovery with `catch`.
- [x] `finally` doesn’t alter resolved value.
- [x] Final value remains `undefined`.

---

## 🎓 Learning Outcome

This question teaches the **importance of return values**, how **nested promises** affect chain resolution, and the **subtle behavior of `.finally()`**. These are crucial for writing robust and predictable asynchronous code.

---