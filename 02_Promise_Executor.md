# 02 – Promise Executor

## ❓ Question: What is the output of the following code?

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

## ✅ Output:
```
1
```

---

## 🧠 Step-by-Step Explanation:

1. **Promise executor function** is called immediately when the promise is created.
2. The first call to `resolve(1)` **settles the promise as fulfilled** with the value `1`.
3. Any further calls to `resolve(2)` or `reject('error')` are **ignored** because a promise can be settled only once.
4. The `.then()` method is triggered with the resolved value:
   - `value => console.log(value)` → prints `1`.
5. The rejection handler in `.then()` is not executed because the promise was resolved, not rejected.

---

## 📌 Things to Remember

- A Promise can be **settled only once** – either resolved or rejected.
- Further calls to `resolve` or `reject` are ignored silently once the first one is executed.
- Both `resolve(2)` and `reject('error')` have **no effect** here.

---

## ⚠️ Gotchas to Watch Out For

- **No error is thrown** for calling `resolve`/`reject` multiple times – they are simply ignored.
- If you're expecting multiple results, use an array or another mechanism — Promises are strictly **one-time-settle**.
- **Order matters** – only the first `resolve` or `reject` is honored.

---

## ✅ Summary Checklist

- [x] Promise executor runs immediately.
- [x] Only the first call to `resolve`/`reject` is respected.
- [x] `.then()` only responds to the first settled state.
- [x] Use external control structures for multiple values (e.g., arrays, streams).
