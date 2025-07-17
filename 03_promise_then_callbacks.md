# [03 - Promise then callbacks](https://bigfrontend.dev/quiz/3-promise-then-callbacks)

## 🧪 Question

**What will be the output of the following code?**

```js
Promise.resolve(1)
  .then(() => 2)
  .then(3)
  .then((value) => value * 3)
  .then(Promise.resolve(4))
  .then(console.log);
```

---

## 🧾 Output

```
4
```

---

## 📖 Step-by-Step Explanation

### Line-by-line breakdown:

```js
Promise.resolve(1)
```
- This returns a resolved promise with value `1`.

```js
.then(() => 2)
```
- The callback returns `2` directly, so it wraps it in a resolved promise: `Promise.resolve(2)`.

```js
.then(3)
```
- 🚨 This is a key part: you passed a **non-function value** (`3`) to `.then()`. JavaScript will **ignore it** and pass the previous resolved value (`2`) through to the next `.then()`.

```js
.then((value) => value * 3)
```
- Receives `2` and returns `2 * 3 = 6`.

```js
.then(Promise.resolve(4))
```
- 🚨 Another gotcha: you passed a **promise instead of a function**.
- When you write `.then(Promise.resolve(4))`, it immediately **executes `Promise.resolve(4)`**, and the return value is `Promise { 4 }`. But this is **not a function**, so it's ignored.
- Hence, the value from the previous `.then()` — which was `6` — is passed down unchanged.

```js
.then(console.log)
```
- Receives the value `6` and logs it.

BUT WAIT...

### ❗ The confusion:

This would be correct **if** `.then(Promise.resolve(4))` were interpreted as a thenable. But **it's ignored** because `Promise.resolve(4)` is not a function.

However, due to **a mistake in the previous reasoning**, let’s walk through what **actually happens** again with correction:

### 🔁 Real Chain Flow:

1. `Promise.resolve(1)` → resolves to `1`
2. `.then(() => 2)` → returns `2`
3. `.then(3)` → ignored → value `2` continues
4. `.then((value) => value * 3)` → gets `2`, returns `6`
5. `.then(Promise.resolve(4))` → interpreted as `.then(non-function)` → ignored → value `6` continues
6. `.then(console.log)` → logs `6`

✅ So **final output is `6`**, not `4`.

---

## ✅ Final Answer

```
6
```

---

## 📌 Key Learnings

- `then(non-function)` → ignored; previous value is passed to the next `.then()`
- `then(Promise.resolve(...))` → immediately invokes `Promise.resolve(...)`, but since it’s not a function, it's **ignored**
- Each `.then()` expects a function. If you pass anything else, it will be skipped

---

## 🧠 Things to Remember

- Always pass a function to `.then()`, not a value or a promise
- A promise passed **as a value**, not as a function, is ignored
- Chain continues with last resolved value if the current `.then()` has an invalid handler

---

## ⚠️ Gotchas

- **Non-function values in `.then(...)` are ignored**
- **Passing `Promise.resolve(...)` directly as a `.then()` argument** will NOT unwrap or wait for the promise — it's treated as a value, **not a function**
- JS does **not** throw errors when you misuse `.then()`, but silently ignores misused handlers

---
