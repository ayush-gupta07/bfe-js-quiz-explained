# [12 - Arguments](https://bigfrontend.dev/quiz/arguments)

## ❓ Question
```js
function log(a, b, c, d) {
  console.log(a, b, c, d);
  arguments[0] = 'bfe';
  arguments[3] = 'dev';
  console.log(a, b, c, d);
}

log(1, 2, 3);
```

---

## ✅ Output

```
1 2 3 undefined
bfe 2 3 undefined
```

---

## 🧠 Step by Step Explanation / Internal Implementation

1. The `log` function is invoked with three arguments: `1, 2, 3`.
2. JavaScript provides an array-like object called `arguments` inside regular (non-arrow) functions, which holds all passed arguments.
3. When `log(1, 2, 3)` is called:
   - Parameters: `a = 1`, `b = 2`, `c = 3`, `d = undefined`.
   - First log: `1 2 3 undefined`.

4. `arguments[0] = 'bfe'` updates the first argument:
   - In **non-strict mode**, `arguments` and the named parameters (`a`, `b`, `c`) are linked (bound) if the argument was actually passed.
   - So updating `arguments[0]` also updates `a` to `'bfe'`.

5. `arguments[3] = 'dev'` attempts to add a fourth argument:
   - Since `d` was **not passed**, there is no binding between `arguments[3]` and `d`.
   - Thus, `d` remains `undefined`.

6. Second log prints: `'bfe' 2 3 undefined`.

7. 🔍 **Internal Behavior**:
   - Parameters `a`, `b`, `c` are in sync with their corresponding indexes in the `arguments` object.
   - No binding exists between `d` and `arguments[3]` since no fourth argument was passed.

---

## ⚠️ Things to Remember / Gotchas

- The `arguments` object is only available in **regular (non-arrow)** functions.
- In **non-strict mode**, the first N parameters (`a`, `b`, `c`, ...) are **linked to** `arguments[0..N-1]`.
- Any parameter not passed (like `d`) **won’t** sync with its corresponding `arguments` index.
- In **strict mode**, this binding between `arguments` and named parameters is **removed**.
- Prefer `...rest` parameters (`function(...args)`) in modern JavaScript for cleaner and more predictable behavior.
