# 01 - Promise Order

## 🧪 Question

What is the output of the following code?

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

## 🔍 Step-by-Step Explanation

1. **`console.log(1);`** → Immediately logs `1`.
2. **New Promise creation** → Executes the executor function synchronously:
   - `console.log(2);` → logs `2`
   - `resolve();` → schedules `.then()` callbacks (microtasks)
   - `console.log(3);` → logs `3` (runs **after** resolve)
3. **`console.log(4);`** → logs `4`
4. **First `then()` is scheduled** → waits in microtask queue.
5. **Second `then()` is chained** → also queued as microtask after the first.
6. **`console.log(7);`** → logs `7`
7. **Microtask Queue runs**:
   - `console.log(5);` → logs `5`
   - `console.log(6);` → logs `6`
8. **Macro tasks (timers)**:
   - `setTimeout(..., 0)` → logs `9`
   - `setTimeout(..., 10)` → logs `8`

---

## 📌 Key Learnings

- Promise executors run synchronously.
- `.then()` callbacks run asynchronously in **microtask queue**, after the main stack is empty.
- `setTimeout(fn, 0)` is a **macrotask** and runs **after microtasks**.
- Even after `resolve()` is called, the remaining code in the executor continues to run.

---

## 🧠 Things to Remember

- Microtasks (like `.then()`) run before macrotasks (`setTimeout`).
- Code after `resolve()` still runs unless returned.
- `.then().then()` chains microtasks one after another.
- `setTimeout(..., 0)` still doesn’t run before microtasks.

---

## ⚠️ Gotchas to Watch Out For

- **Post-resolve Execution**: Code after `resolve()` still executes. If you want to prevent further code from executing after resolving, use `return resolve();`
  ```js
  resolve();
  console.log('this will still run'); // YES
  return resolve(); // preferred if nothing should run afterward
  ```
- **Order Confusion**: `.then()`s may look sequential but run after the call stack clears.

---

## 🧭 Summary Checklist

- [x] `new Promise()` runs immediately.
- [x] `.then()` goes to microtask queue.
- [x] `setTimeout()` goes to macrotask queue.
- [x] Microtasks flush **before** next macrotask.
- [x] Executor runs all lines unless interrupted with `return`.

---

## 📺 Visual Timeline

```
Call Stack:
1
2
3
4
7

Microtasks:
5
6

Macrotasks:
9
8
```